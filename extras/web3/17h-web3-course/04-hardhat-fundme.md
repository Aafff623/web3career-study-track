---
type: course-note
source:
  platform: bilibili
  url: https://www.bilibili.com/video/BV1RFsfe5Ek5
  bibigpt: https://bibigpt.co/video/BV1RFsfe5Ek5
  series: "17 小时最全 Web3 教程 — ERC20 / NFT / Hardhat / CCIP 跨链"
  lesson: "第 4 课 — Hardhat 开发框架：完成 FundMe"
  duration: "约 2 小时"
extracted_by: biliGPT
cleaned_at: 2026-06-02
tags: [Hardhat, Web3 开发, 智能合约部署, Solidity, 本地开发环境, FundMe]
---

# 第四课：Hardhat 开发框架：完成 FundMe

![](https://i1.hdslb.com/bfs/archive/6737b980ef62367a2de8dd77070b1ca428fd4bdc.jpg)

### 本课核心摘要

本课从 Remix 迁移到本地 Hardhat 开发框架，围绕 FundMe 合约完成一套更接近真实项目的开发流程：本地环境配置、Hardhat 项目初始化、合约编译、脚本部署、Sepolia 测试网部署、合约验证、脚本交互、自定义 Task，以及最后将代码推送到 GitHub。核心目标不是单纯"会部署一个合约"，而是建立一套可复用、可维护、可协作的 Web3 工程化流程。

> *本课的重点在于从"网页上点按钮写合约"过渡到"本地工程化开发"。Hardhat 的价值不只是部署合约，而是让合约开发具备版本管理、自动化部署、测试、配置隔离和团队协作能力。*

---

## 一、为什么从 Remix 切换到 Hardhat

### Remix 的局限

| 问题 | 具体表现 |
|------|---------|
| 批量部署困难 | 每次都需要手动点击 compile、deploy、调用函数 |
| 批量测试困难 | 多合约、多函数、多场景测试时，靠 UI 点击效率极低 |
| 项目协作不友好 | 团队成员难以统一依赖、编译器版本和部署流程 |
| 依赖版本不可控 | OpenZeppelin、Chainlink 的 import 可能随远程版本变化 |
| 不适合长期维护 | 合约升级后需要反复完整测试，人工操作不可持续 |

> *Remix 更像"教学和原型工具"，Hardhat 更像"工程项目工具"。当合约需要反复部署、测试、验证、协作时，工程框架几乎是必需品。*

## 二、主流智能合约开发框架对比

| 框架 | 主要语言生态 | 特点 |
|------|------------|------|
| Hardhat | JavaScript / TypeScript | 插件生态丰富，适合 JS 开发者 |
| Truffle | JavaScript | 已停止主动维护，转向与 Hardhat 合作 |
| Foundry | Rust | 执行效率高，测试速度快，近年来增长明显 |
| Brownie | Python | 适合 Python 开发者 |

Hardhat 和 Foundry 不是互斥关系。一个项目可以同时使用：Hardhat 适合插件、部署、验证、脚本化交互；Foundry 适合高频测试、大量 fuzz test。

> *框架没有绝对最优，只有适合当前团队、语言栈和项目阶段的选择。*

---

## 三、本地开发环境配置

| 工具 | 用途 |
|------|------|
| Node.js | 运行 JavaScript，Hardhat 基于 Node.js 生态 |
| VS Code | 本地代码编辑器 |
| Git | 代码版本管理 |
| Homebrew | macOS 下的软件包管理器 |
| nvm | Node.js 版本管理工具 |
| WSL | Windows 用户推荐安装 Linux 子系统 |

### 安装 nvm 与 Node.js

不推荐直接从 Node.js 官网安装固定版本，推荐通过 nvm 管理多个 Node.js 版本。

```bash
brew install nvm
mkdir ~/.nvm
# 将 nvm 配置加入 ~/.zprofile
source ~/.zprofile
nvm install 20
nvm use 20
node -v
```

### 安装 VS Code

```bash
brew install --cask visual-studio-code
```

推荐安装 Solidity 插件（Nomic Foundation / Hardhat 相关），`.sol` 文件会恢复关键字高亮。

---

## 四、创建第一个 Hardhat 项目

### Step 1：初始化项目

```bash
mkdir web3-tutorial && cd web3-tutorial
npm init
npm install hardhat --save-dev
npx hardhat
# 选择 Create a JavaScript project
```

初始化后生成：

| 文件 / 文件夹 | 作用 |
|--------------|------|
| `hardhat.config.js` | Hardhat 核心配置文件 |
| `contracts/` | Solidity 合约目录 |
| `scripts/` | 脚本目录 |
| `test/` | 测试文件目录 |
| `ignition/` | Hardhat Ignition 部署模块目录 |

`package.json` 中会新增 `@nomicfoundation/hardhat-toolbox`，包含 ethers、测试工具、验证插件等常用工具组合。

### Step 2：Git 基础

```bash
git init
git add .
git commit -m "project init"
```

`.gitignore` 通常包含 `node_modules`、`.env`、`coverage`、`artifacts`、`cache` 等。

> *凡是可以本地重新生成的内容，不应该进 Git；凡是包含私钥、密码、API Key 的内容，更不应该进 Git。*

---

## 五、迁移 FundMe 合约并编译

将 Remix 中的 FundMe 合约复制到 `contracts/FundMe.sol`。如果合约引用了 Chainlink Data Feed：

```bash
npm install @chainlink/contracts --save-dev
```

注意 Chainlink 包版本升级后 import 路径可能变化：

```solidity
// 旧路径
import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";
// 新路径
import "@chainlink/contracts/src/v0.8/shared/interfaces/AggregatorV3Interface.sol";
```

编译：

```bash
npx hardhat compile
```

编译成功后生成 `artifacts/`（ABI、bytecode）和 `cache/`（编译缓存）。

---

## 六、编写部署脚本

### 部署脚本核心逻辑

```javascript
const { ethers } = require("hardhat");

async function main() {
  const fundMeFactory = await ethers.getContractFactory("FundMe");
  console.log("Contract deploying...");
  const fundMe = await fundMeFactory.deploy(10);
  await fundMe.waitForDeployment();
  console.log("Contract has been deployed successfully.");
  console.log(`Contract address is ${fundMe.target}`);
}

main().catch((error) => {
  console.error(error);
  process.exit(1);
});
```

| 代码 | 说明 |
|------|------|
| `ethers.getContractFactory("FundMe")` | 获取合约工厂 |
| `deploy(10)` | 部署合约，`10` 是构造函数参数（lockTime） |
| `waitForDeployment()` | 等待部署交易真正上链 |
| `fundMe.target` | 获取部署后的合约地址 |

执行部署：

```bash
npx hardhat run scripts/deployFundMe.js
```

不指定网络时，Hardhat 默认使用本地临时网络（in-process），脚本结束后网络消失。

---

## 七、配置 Sepolia 网络

### 获取 RPC URL

在 Alchemy 创建 App：登录 → Apps → Create New App → Chain: Ethereum → Network: Sepolia → 复制 HTTPS RPC URL。

### 配置 `hardhat.config.js`

```javascript
require("@nomicfoundation/hardhat-toolbox");

module.exports = {
  solidity: "0.8.24",
  networks: {
    sepolia: {
      url: "你的 Sepolia RPC URL",
      accounts: ["你的测试账户私钥"],
    },
  },
};
```

部署到 Sepolia：

```bash
npx hardhat run scripts/deployFundMe.js --network sepolia
```

> *测试私钥也应该当成敏感信息处理。不要在测试账户里存真实资产，更不要把真实钱包私钥用于开发项目。*

---

## 八、使用环境变量与加密配置

### 方式一：`.env`

```env
SEPOLIA_URL=你的 RPC URL
PRIVATE_KEY=你的私钥
```

```bash
npm install dotenv --save-dev
```

```javascript
require("dotenv").config();
const sepoliaUrl = process.env.SEPOLIA_URL;
const privateKey = process.env.PRIVATE_KEY;
```

### 方式二：`@chainlink/env-enc` 加密

```bash
npm install @chainlink/env-enc --save-dev
npx env-enc set-pw    # 设置加密密码
npx env-enc set        # 写入变量：SEPOLIA_URL, PRIVATE_KEY, ETHERSCAN_API_KEY
```

生成 `.env.enc`（加密存储），在 config 中改为：

```javascript
require("@chainlink/env-enc").config();
```

> *加密环境变量比明文 `.env` 更安全，但并不意味着可以随意泄露。开发钱包和资产钱包必须隔离。*

---

## 九、合约验证 Verify

### 为什么要验证

验证后区块链浏览器会显示源代码，提供 Read Contract、Write Contract、ABI、源码浏览，提升外部用户可读性和可信度。

### 命令行验证

```bash
npx hardhat verify --network sepolia 合约地址 构造函数参数
```

### 部署脚本中自动验证

```javascript
const { ethers, run, network } = require("hardhat");

async function verifyFundMe(fundMeAddress, args) {
  await run("verify:verify", {
    address: fundMeAddress,
    constructorArguments: args,
  });
}
```

部署成功后，如果是 Sepolia 网络且有 Etherscan API Key，等待 5 个区块确认后执行验证：

```javascript
if (network.config.chainId === 11155111 && process.env.ETHERSCAN_API_KEY) {
  console.log("Waiting for 5 confirmations...");
  await fundMe.deploymentTransaction().wait(5);
  await verifyFundMe(fundMe.target, [300]);
}
```

等待确认是为了避免合约刚上链但 Etherscan 尚未索引完成，导致验证失败。

---

## 十、脚本中与合约交互

### 获取多个账户

```javascript
const [firstAccount, secondAccount] = await ethers.getSigners();
```

在 `hardhat.config.js` 中配置多个私钥：

```javascript
accounts: [privateKey, privateKey1],
```

### 第一个账户调用 fund

```javascript
const fundTx = await fundMe.fund({
  value: ethers.parseEther("0.5"),
});
await fundTx.wait();
```

### 查询合约余额

```javascript
const balanceOfContract = await ethers.provider.getBalance(fundMe.target);
console.log(`Balance of the contract is ${balanceOfContract}`);
```

### 第二个账户调用 fund

```javascript
const fundTxWithSecondAccount = await fundMe
  .connect(secondAccount)
  .fund({
    value: ethers.parseEther("0.5"),
  });
await fundTxWithSecondAccount.wait();
```

### 读取 mapping

```javascript
const firstAccountBalance = await fundMe.fundersToAmount(firstAccount.address);
const secondAccountBalance = await fundMe.fundersToAmount(secondAccount.address);
```

> *课程中一开始部署参数设置为 10 秒，导致验证后 FundMe 时间窗口关闭，调用 fund 报错 `Execution reverted: window is closed`。解决方式是把构造函数参数调大，例如 300。*

---

## 十一、自定义 Hardhat Task

### Task 的意义

Hardhat Task 是异步 JavaScript 函数，可以把常用逻辑封装成命令行任务。

| 优点 | 说明 |
|------|------|
| 标准化 | 用户不用读脚本细节，直接运行任务 |
| 可读性强 | `deploy-fundme`、`interact-fundme` 语义清楚 |
| 易复用 | 不同脚本逻辑可以拆成多个任务 |
| 面向协作更友好 | 新开发者更容易上手 |

### 部署 Task

```javascript
const { task } = require("hardhat/config");
task("deploy-fundme", "Deploy and verify FundMe contract").setAction(
  async (taskArgs, hre) => {
    const fundMeFactory = await hre.ethers.getContractFactory("FundMe");
    console.log("Contract deploying...");
    const fundMe = await fundMeFactory.deploy(300);
    await fundMe.waitForDeployment();
    console.log(`Contract address is ${fundMe.target}`);

    if (hre.network.config.chainId === 11155111 && process.env.ETHERSCAN_API_KEY) {
      console.log("Waiting for 5 confirmations...");
      await fundMe.deploymentTransaction().wait(5);
      await hre.run("verify:verify", {
        address: fundMe.target,
        constructorArguments: [300],
      });
    } else {
      console.log("Verification skipped.");
    }
  }
);
module.exports = {};
```

运行：

```bash
npx hardhat deploy-fundme --network sepolia
```

### 交互 Task

```javascript
const { task } = require("hardhat/config");
task("interact-fundme", "Interact with FundMe contract")
  .addParam("addr", "FundMe contract address")
  .setAction(async (taskArgs, hre) => {
    const fundMeFactory = await hre.ethers.getContractFactory("FundMe");
    const fundMe = fundMeFactory.attach(taskArgs.addr);
    const [firstAccount, secondAccount] = await hre.ethers.getSigners();

    const fundTx = await fundMe.fund({ value: hre.ethers.parseEther("0.5") });
    await fundTx.wait();

    const balanceAfterFirstFund = await hre.ethers.provider.getBalance(fundMe.target);
    console.log(`Balance of contract is ${balanceAfterFirstFund}`);

    const fundTxWithSecondAccount = await fundMe
      .connect(secondAccount)
      .fund({ value: hre.ethers.parseEther("0.5") });
    await fundTxWithSecondAccount.wait();

    const balanceAfterSecondFund = await hre.ethers.provider.getBalance(fundMe.target);
    console.log(`Balance of contract is ${balanceAfterSecondFund}`);

    const firstAccountBalance = await fundMe.fundersToAmount(firstAccount.address);
    const secondAccountBalance = await fundMe.fundersToAmount(secondAccount.address);
    console.log(`Balance of first account ${firstAccount.address} is ${firstAccountBalance}`);
    console.log(`Balance of second account ${secondAccount.address} is ${secondAccountBalance}`);
  });
module.exports = {};
```

运行：

```bash
npx hardhat interact-fundme --addr 合约地址 --network sepolia
```

### 统一导出

`tasks/index.js`：

```javascript
require("./deployFundMe");
require("./interactFundMe");
exports.deployContract = require("./deployFundMe");
exports.interactContract = require("./interactFundMe");
```

在 `hardhat.config.js` 中只需 `require("./tasks");`。查看所有任务：`npx hardhat help`。

---

## 十二、最终推荐项目结构

```
web3-tutorial/
├── contracts/
│   └── FundMe.sol
├── scripts/
│   └── deployFundMe.js
├── tasks/
│   ├── deployFundMe.js
│   ├── interactFundMe.js
│   └── index.js
├── test/
├── artifacts/
├── cache/
├── hardhat.config.js
├── package.json
├── package-lock.json
├── .gitignore
└── .env.enc
```

| 路径 | 是否提交 Git |
|------|------------|
| `contracts/`、`scripts/`、`tasks/` | 是 |
| `hardhat.config.js`、`package.json`、`package-lock.json` | 是 |
| `node_modules/`、`.env`、`.env.enc` | 否 |
| `artifacts/`、`cache/` | 通常可忽略 |

---

## 十三、推送代码到 GitHub

```bash
git remote add origin https://github.com/你的用户名/web3-tutorial.git
git add .
git commit -m "finish lesson 4"
git push --set-upstream origin master
```

> *GitHub 不只是代码备份工具，也是开发履历的一部分。持续把课程项目、练习项目和完整作品沉淀到 GitHub，对后续求职、协作和展示能力都有价值。*

---

## 十四、本课关键命令汇总

### 环境安装

```bash
brew update && brew install nvm
nvm install 20 && nvm use 20
node -v
```

### Hardhat 项目

```bash
npm init
npm install hardhat --save-dev
npx hardhat
npm install @chainlink/contracts --save-dev
npx hardhat compile
```

### 部署与验证

```bash
npx hardhat run scripts/deployFundMe.js
npx hardhat run scripts/deployFundMe.js --network sepolia
npx hardhat verify --network sepolia 合约地址 构造函数参数
```

### 环境变量加密

```bash
npm install @chainlink/env-enc --save-dev
npx env-enc set-pw
npx env-enc set
```

### 自定义 Task

```bash
npx hardhat deploy-fundme --network sepolia
npx hardhat interact-fundme --addr 合约地址 --network sepolia
```

---

## 十五、本课核心结论

1. **Remix vs Hardhat**：Remix 适合快速学习和小型实验，Hardhat 适合工程项目开发。
2. **环境配置**：Node.js + nvm + VS Code + Git 是基础；Windows 用户推荐 WSL。
3. **Hardhat 项目结构**：contracts / scripts / tasks / test / hardhat.config.js 是核心。
4. **依赖管理**：Chainlink、OpenZeppelin 等第三方包通过 npm 安装，版本记录在 package.json 和 lock 文件中。
5. **网络配置**：本地 Hardhat 网络用于快速测试，Sepolia 用于真实测试网部署。
6. **环境变量**：`.env` 或 `@chainlink/env-enc` 管理私钥和 API Key，绝不提交到 Git。
7. **合约验证**：通过 Etherscan API Key 验证合约，提升可信度和可交互性。
8. **脚本交互**：JavaScript 脚本可以调用合约函数、读取状态、模拟多账户操作。
9. **自定义 Task**：封装常用逻辑为命令行任务，提升标准化和可复用性。
10. **工程化思维**：代码可复现、配置可隔离、部署可自动化、交互可脚本化、任务可封装、版本可追踪。

> *这一课最重要的不是记住每一条命令，而是理解一套真实开发流程。后续无论写 ERC20、NFT、跨链合约，都会复用这套底层开发习惯。*

---

> *清洗说明：biliGPT 原始输出结构规范。清洗动作：补全 YAML frontmatter（lesson / duration / cleaned_at）、移除 Mermaid 代码块（内容已在正文中以文字/伪代码覆盖）、表格格式统一、代码块语言标注统一。未改写表述。*

#BibiGPT https://bibigpt.co
