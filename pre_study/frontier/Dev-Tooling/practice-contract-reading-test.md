# Practice: 合约阅读 + 测试建议工具设计

> 模块：前沿探索 · Dev-Tooling

## 目标

设计一个"合约阅读 + 测试建议"最小工具，输出合约分析、关键权限、测试不变量和用例建议。

## 场景

选择一个开源 ERC20 带权限控制的合约（如 OpenZeppelin AccessControlExample），进行分析和测试建议。

## 流程

### 1. 合约职责与关键权限

```
合约：AccessControlToken (ERC20 + AccessControl)
职责：
  - 标准 ERC20 代币功能（transfer, approve, balanceOf）
  - 基于角色的权限管理（MINTER_ROLE, BURNER_ROLE, ADMIN_ROLE）
  - 铸造和销毁受角色控制

关键权限：
  - DEFAULT_ADMIN_ROLE: 管理所有角色分配
  - MINTER_ROLE: 可铸造新代币
  - BURNER_ROLE: 可销毁代币
  - 无 pause 权限（假设）
  - 无 upgrade 权限（假设）
```

### 2. 会移动资产的函数

| 函数 | 移动方向 | 权限要求 | 风险 |
|------|---------|---------|------|
| `transfer(to, amount)` | 用户→用户 | 持有者 | 正常转移 |
| `transferFrom(from, to, amount)` | 用户→用户 | 被授权者 | 无限授权风险 |
| `mint(to, amount)` | 无中生有 | MINTER_ROLE | 超额铸造风险 |
| `burn(from, amount)` | 销毁 | BURNER_ROLE | 未授权销毁风险 |
| `grantRole(role, account)` | 权限分配 | ADMIN_ROLE | 权限提升风险 |

### 3. 最值得测试的不变量

```
不变量 1: totalSupply 永远等于所有 address.balanceOf 之和
  → 铸造增加 totalSupply，销毁减少，转账不改变总量

不变量 2: 非 MINTER_ROLE 不能调用 mint
  → 只有持有 MINTER_ROLE 的地址能铸造新代币

不变量 3: 单个地址余额不能超过 totalSupply
  → 任何时刻 balanceOf(addr) <= totalSupply
```

### 4. 测试用例建议

```solidity
// 权限测试
function test_mint_revert_non_minter() public {
    vm.prank(nonMinter);
    vm.expectRevert();
    token.mint(addr, 100);
}

// 状态转换测试
function test_grantRole_only_admin() public {
    vm.prank(nonAdmin);
    vm.expectRevert();
    token.grantRole(MINTER_ROLE, newMinter);
}

// 数值边界测试
function test_mint_max_uint() public {
    token.mint(addr, type(uint256).max);
    assertEq(token.totalSupply(), type(uint256).max);
}

// 资产安全测试
function test_transferFrom_insufficient_balance() public {
    token.approve(spender, 1000);
    vm.prank(spender);
    vm.expectRevert();
    token.transferFrom(owner, spender, 2000);
}

// 角色管理测试
function test_revokeRole_prevents_mint() public {
    token.revokeRole(MINTER_ROLE, minter);
    vm.prank(minter);
    vm.expectRevert();
    token.mint(addr, 100);
}
```

### 5. 需要人工复核的安全问题

| 问题 | 为什么需要人工复核 |
|------|------------------|
| DEFAULT_ADMIN_ROLE 权限过大 | 单点控制所有角色，需确认是否需要多签 |
| mint 无上限 | 需确认是否有通胀控制机制 |
| 无 pause 功能 | 紧急情况下无法暂停铸造/转账 |
| 无 timelock | 角色变更立即生效，无延迟窗口 |

### 6. 工具链引用

- Foundry: 测试框架（forge test）
- Slither: 静态分析（权限检查、重入检测）
- OpenZeppelin Defender: 部署后监控

## 验收标准

- [ ] 合约职责和关键权限清晰列出
- [ ] 会移动资产的函数标注权限和风险
- [ ] 3 个不变量明确且可测试
- [ ] 5 条测试用例覆盖权限/边界/资产安全
- [ ] 安全问题标注为什么需要人工复核
