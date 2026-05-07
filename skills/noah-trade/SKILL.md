---
name: "noah-trade"
description: "Use this skill when the user asks for account info, positions, stock availability, order history, deal history, fees, capital flow, push data, or trading-related asset queries through the noah command. Do NOT use for market snapshot, ticker, kline, rankings, IPO, or stock metadata queries."
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

# Noah Trade CLI

Command-driven noah trade skill for the globally installed Noah CLI.

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
| 1 | `trade get-account-info` | 获取账户信息 |
| 2 | `trade get-positions` | 获取持仓列表 |
| 3 | `trade get-stock-amount` | 获取证券可买可卖数量 |
| 4 | `trade max-enable-buy-amt` | 查询融资最大可买数量 |
| 5 | `trade get-sec-asset` | 获取证券资产 |
| 6 | `trade get-sec-capital-flow` | 获取证券资金流水 |
| 7 | `trade get-order-list` | 获取当日订单列表 |
| 8 | `trade get-today-order-list` | 获取当日未完成委托订单列表 |
| 9 | `trade get-history-order-list` | 获取历史订单列表 |
| 10 | `trade get-today-deal-list` | 获取当日成交列表 |
| 11 | `trade get-history-deal-list` | 获取历史成交列表 |
| 12 | `trade get-finished-order-list` | 获取已完成订单列表 |
| 13 | `trade get-order-detail` | 获取订单详情 |
| 14 | `trade get-order-fee-detail` | 获取订单费用详情 |
| 15 | `trade order-fee-query` | 查询下单预估费用 |
| 16 | `trade convert-ufg-money-balance` | 不同币种汇率换算 |
| 17 | `trade query-push-data` | 查询推送数据 |

---

## Operation Flow

### Step 1 — Identify request type and load reference

| User intent | Reference to load |
|---|---|
| Trade | {baseDir}/references/trade-commands.md |
| 跨步骤组合与典型调用顺序 | {baseDir}/references/workflows.md |

### Step 2 — Verify the CLI exists and inspect the command

Run `noah --version` first. If it prints output, continue with `noah inspect trade <command>` to confirm required parameters, body shape, response shape, and authentication requirements. If it does not print output, use the install steps declared in frontmatter, make sure devDependencies are installed, and rerun `noah --version` before continuing.

### Step 3 — Run commands immediately

Always invoke the globally installed CLI with `noah ...`. Do not replace the documented commands with local project execution forms.

Many commands in this skill depend on authenticated trade data. Inspect first, confirm required query/body fields, and then execute with validated parameters.

---

## Edge Cases

- trade skill 下大多数命令都需要鉴权；执行前优先 inspect，并确认 `noah init --token <bearerToken>` 已完成。
- 如果用户请求属于行情、榜单、K 线、F10 或标的信息，不要路由到 trade skill，应改用 market skill。
- 历史订单、历史成交类命令可能返回较大结果集，必要时提醒用户缩小时间范围。
- 如 inspect 输出包含必填 body 字段，应严格按字段要求构造请求，不要猜测。

## Global Notes

- 本 skill 默认依赖全局可用的 `noah` 命令。
- 默认命令入口为 `noah`。
- 实际执行时始终使用全局安装后的 `noah ...` 命令，不使用项目内脚本或本地入口替代。
- 如果构建依赖未安装，优先使用会安装 devDependencies 的方式安装项目依赖。
- trade skill 以账户、持仓、订单、成交、费用等交易相关命令为主。
