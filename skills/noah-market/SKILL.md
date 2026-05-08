---
name: "noah-market"
description: "Use this skill when the user asks for market data, asset snapshots, tickers, kline data, market status, rankings, shareholder changes, trading calendars, IPO data, or stock metadata through the noah command. Do NOT use for account, positions, orders, fees, or trade execution."
license: "MIT"
metadata:
  author: "summer-sk2026"
  version: "local"
  homepage: "https://github.com/summer-sk2026/noah-cli/tree/main"
agent:
  requires:
    - id: "github"
      kind: "node"
      package: "summer-sk2026/noah-cli"
      bins:
        - "noah"
      label: "Install Noah CLI"
  install: |
    git clone https://github.com/summer-sk2026/noah-cli.git
    cd noah-cli
    npm install --include=dev
    npm run build
    npm install -g .
---

# Noah Market CLI

Command-driven noah market skill for the globally installed Noah CLI.

## CRITICAL: CLI Dependency

**This skill CANNOT function without the `noah` CLI being installed and globally available.**

This skill is entirely driven by the `noah` command-line tool. Every operation listed below requires the `noah` binary to be installed globally on the system. There is NO alternative execution path — without a working `noah` command, this skill has zero capability.

- repository: `https://github.com/summer-sk2026/noah-cli/tree/main`
- git clone URL: `https://github.com/summer-sk2026/noah-cli.git`
- binary name: `noah`
- all runtime commands MUST use the globally installed `noah` command
- do NOT execute through local project scripts, `npx`, `node src/...`, or any other local entry point
- do NOT skip the build step — the CLI must be compiled from TypeScript source before global installation
- the build step requires devDependencies (e.g. `tsup`), so they MUST be installed

## Preflight

Before running any command in this skill, you MUST complete these checks in order:

1. Run `noah --version` to verify the CLI is globally available
2. If `noah --version` produces version output → the CLI is ready, proceed to step 5
3. If `noah --version` fails or command not found → you MUST install the CLI following the **Install** section below. Do NOT skip this step. Do NOT attempt to run any other noah command until installation succeeds.
4. After installation, run `noah --version` again to confirm success. If it still fails, do NOT proceed — report the installation failure.
5. Before executing any business command, run `noah inspect <namespace> <command>` to confirm required parameters, body shape, and authentication requirements. Do NOT guess arguments.
6. If inspect output shows bearer authentication is required, ensure `noah init --token <bearerToken>` has been completed before executing the command.

## Install

**When to install:** Install the CLI if `noah --version` does not produce output, returns an error, or the command is not found.

**Installation method:** Clone from source, build, and install globally. You MUST follow ALL steps below in exact order. Do NOT skip any step. Do NOT substitute alternative approaches.

### Step-by-step installation commands:

```bash
# Step 1: Clone the repository
git clone https://github.com/summer-sk2026/noah-cli.git

# Step 2: Enter the project directory
cd noah-cli

# Step 3: Install ALL dependencies including devDependencies
# IMPORTANT: You MUST use --include=dev because the build tool (tsup) is a devDependency
# Using plain "npm install" without --include=dev may skip build tools and cause build failure
npm install --include=dev

# Step 4: Build the TypeScript source into executable JavaScript
# This step WILL FAIL if devDependencies were not installed in Step 3
npm run build

# Step 5: Install the built CLI globally so "noah" is available system-wide
npm install -g .
```

### Post-installation verification:

```bash
# MUST succeed before proceeding with any other command
noah --version
```

### Common installation mistakes to avoid:
- ❌ Do NOT run `npm install` without `--include=dev` — build will fail due to missing `tsup`
- ❌ Do NOT skip `npm run build` — the CLI source is TypeScript and cannot run directly
- ❌ Do NOT skip `npm install -g .` — without global install, `noah` command won't be available
- ❌ Do NOT use `npx`, `node dist/...`, or project-local scripts as a substitute for global `noah`
- ❌ Do NOT attempt to run business commands before `noah --version` succeeds
- ✅ Always use the globally installed `noah ...` command form after installation

### If installation fails:
1. Ensure Node.js >= 18 and npm are available
2. Ensure git is available for cloning
3. Check that `npm install --include=dev` completed without errors
4. Check that `npm run build` completed without errors (look for `tsup` related errors)
5. Check that `npm install -g .` completed without permission errors (use sudo on Linux/macOS if needed)
6. If all steps pass but `noah --version` still fails, check your system PATH

---

## Command Index

| # | Command | Summary |
|---|---|---|
| 1 | `noah market fixed-income` | 用户固收类资产通用查询接口 |
| 2 | `noah market total-asset` | 资产信息汇总 |
| 3 | `noah market hold-share-list` | 公募信息获取 |
| 4 | `noah market query-private-contract-asset-list` | 私募查询接口 |
| 5 | `noah market cash-total-asset` | 现金宝 |
| 6 | `noah market bank-deposit-hold-detail` | 银行定存存续或到期详情 |
| 7 | `noah market user-asset-query-detail` | 用户固收类存量-存续详情接口 |
| 8 | `noah market balance-list` | 用户余额列表 |
| 9 | `noah market get-stock-rank` | 获取排行榜数据 |
| 10 | `noah market shareholder-inc-red-hold` | 股东增减持明细榜单按市场范围 |
| 11 | `noah market shareholder-inc-red-hold-by-date` | 股东增减持明细榜单按时间范围 |
| 12 | `noah market shareholder-inc-red-hold-by-ucode` | 股东增减持明细榜单按股票代码范围 |
| 13 | `noah market get-finance-us-infos` | 获取美股财务数据 |
| 14 | `noah market get-finance-hk-infos` | 获取港股财务数据 |
| 15 | `noah market get-us-analysis` | 获取美股分析信息 |
| 16 | `noah market get-capital-flow` | 获取个股资金流向 |
| 17 | `noah market get-market-state` | 获取股票对应市场的市场状态 |
| 18 | `noah market get-market-snapshot` | 获取市场快照信息 |
| 19 | `noah market get-rt-data` | 获取实时分时 |
| 20 | `noah market get-cur-kline` | 获取实时 K 线 |
| 21 | `noah market get-cur-kline-date` | 获取实时 K 线,根据时间范围筛选 |
| 22 | `noah market get-rt-ticker` | 获取实时逐笔 |
| 23 | `noah market get-broker-queue` | 获取实时经纪队列 |
| 24 | `noah market get-stock-basicinfo` | 获取指定市场中特定类型或特定股票的基本信息 |
| 25 | `noah market get-stock-filter` | 条件选股 |
| 26 | `noah market get-ipo-list` | 获取指定市场的 IPO 列表 |
| 27 | `noah market get-global-state` | 获取全局市场状态 |
| 28 | `noah market request-trading-days` | 获取交易日历 |

---

## Operation Flow

**执行任何命令前必须严格按以下步骤顺序操作，禁止跳过任何步骤。**

### Step 1 — 验证 CLI 可用

```bash
noah --version
```

如果无输出或命令不存在，必须先完成 Install 部分的安装步骤。

### Step 2 — 匹配工作流

**首先**加载 {baseDir}/references/workflows.md，判断用户请求是否匹配其中定义的工作流场景。

- 如果匹配到工作流 → 按该工作流定义的命令编排（并行/串行）执行，跳到 Step 3
- 如果没有匹配的工作流 → 从 Command Index 中选择合适的单条命令，跳到 Step 3

### Step 3 — 对每个目标命令执行 inspect

**禁止跳过此步骤。禁止凭记忆或猜测直接执行命令。**

对本次需要执行的每一条命令，都必须先运行：

```bash
noah inspect market <command>
```

从 inspect 输出中获取：
- 必填参数名和类型
- 可选参数
- enum 可选值
- 是否需要 bearer 鉴权

### Step 4 — 鉴权（如 inspect 显示需要）

如果 inspect 输出的鉴权部分包含 `bearerAuth`，确保已执行：

```bash
noah init --token <bearerToken>
```

### Step 5 — 执行命令

按 Step 3 inspect 输出的参数定义构造并执行命令：
- 如果是工作流模式：按工作流定义的并行/串行规则执行多条命令
- 如果是单命令模式：直接执行该命令
- 参数名和值必须严格按 inspect 输出构造

### Step 6 — 汇总结果

将所有命令的执行结果整合为用户可理解的摘要返回。

---

## Edge Cases

- 如用户未明确 market 命令名，先运行 inspect 查看命令详情，再决定具体命令。
- market 下部分命令虽然偏查询，但 inspect 可能显示 bearer 鉴权；如需要，先提示执行 `noah init --token <bearerToken>`。
- 涉及时间范围、大结果集或高频行情时，先提醒结果可能较大，再视情况缩小参数范围。
- 不要把账户、持仓、订单、费用等交易请求路由到 market skill。

## Global Notes

- 本 skill 默认依赖全局可用的 `noah` 命令。
- 默认命令入口为 `noah`。
- 实际执行时始终使用全局安装后的 `noah ...` 命令，不使用项目内脚本或本地入口替代。
- 如果构建依赖未安装，优先使用会安装 devDependencies 的方式安装项目依赖。
- market skill 以查询、读取、分析型命令为主。
