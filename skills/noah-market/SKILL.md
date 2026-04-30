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

## Dependency

This skill depends on the Noah CLI project:
- repository: `https://github.com/summer-sk2026/noah-cli/tree/main`
- binary: `noah`
- all runtime commands in this skill must use the globally installed `noah` command
- do not execute this project through local project scripts or local entry points as a substitute for the global CLI
- the build step depends on development tooling, so install dependencies with devDependencies included before building

## Preflight

Before running any command:
- verify the `noah` command exists by running `noah --version`
- if `noah --version` prints output, treat the globally installed CLI as available
- if `noah --version` does not print output or the command is missing, follow the install instructions declared in this skill's frontmatter
- when installing from source, use a dependency installation method that includes devDependencies before running `npm run build`
- after installation, always execute commands as `noah ...`, not through project-local script entry points
- use `noah inspect <namespace> <command>` before guessing arguments
- if inspect output shows bearer authentication, ensure `noah init --token <bearerToken>` has already been completed

## Install

This skill declares its dependency and install commands directly in frontmatter:
- package: `summer-sk2026/noah-cli`
- bins: `noah`
- install label: `Install Noah CLI`

Verification command:

```bash
noah --version
```

If `noah --version` does not produce output, install the CLI using the frontmatter `agent.install` steps, then rerun `noah --version`. Use `npm install --include=dev` before `npm run build` so required build tools such as `tsup` are available. After installation succeeds, always run the global command form such as `noah market ...` or `noah trade ...`.

---

## Command Index

| # | Command | Summary | Source |
|---|---|---|---|
| 1 | `market fixed-income` | 用户固收类资产通用查询接口 | openapi.yaml |
| 2 | `market total-asset` | 资产信息汇总 | openapi.yaml |
| 3 | `market hold-share-list` | 公募信息获取 | openapi.yaml |
| 4 | `market query-private-contract-asset-list` | 私募查询接口 | openapi.yaml |
| 5 | `market cash-total-asset` | 现金宝 | openapi.yaml |
| 6 | `market bank-deposit-hold-detail` | 银行定存存续或到期详情 | openapi.yaml |
| 7 | `market user-asset-query-detail` | 用户固收类存量-存续详情接口 | openapi.yaml |
| 8 | `market balance-list` | 用户余额列表 | openapi.yaml |
| 9 | `market get-stock-rank` | 获取排行榜数据 | openapi.yaml |
| 10 | `market shareholder-inc-red-hold` | 股东增减持明细榜单按市场范围 | openapi.yaml |
| 11 | `market shareholder-inc-red-hold-by-date` | 股东增减持明细榜单按时间范围 | openapi.yaml |
| 12 | `market shareholder-inc-red-hold-by-ucode` | 股东增减持明细榜单按股票代码范围 | openapi.yaml |
| 13 | `market get-finance-us-infos` | 获取美股财务数据 | openapi.yaml |
| 14 | `market get-finance-hk-infos` | 获取港股财务数据 | openapi.yaml |
| 15 | `market get-us-analysis` | 获取美股分析信息 | openapi.yaml |
| 16 | `market get-capital-flow` | 获取个股资金流向 | openapi.yaml |
| 17 | `market get-market-state` | 获取股票对应市场的市场状态 | openapi.yaml |
| 18 | `market get-market-snapshot` | 获取市场快照信息 | openapi.yaml |
| 19 | `market get-rt-data` | 获取实时分时 | openapi.yaml |
| 20 | `market get-cur-kline` | 获取实时 K 线 | openapi.yaml |
| 21 | `market get-cur-kline-date` | 获取实时 K 线,根据时间范围筛选 | openapi.yaml |
| 22 | `market get-rt-ticker` | 获取实时逐笔 | openapi.yaml |
| 23 | `market get-broker-queue` | 获取实时经纪队列 | openapi.yaml |
| 24 | `market get-stock-basicinfo` | 获取指定市场中特定类型或特定股票的基本信息 | openapi.yaml |
| 25 | `market get-stock-filter` | 条件选股 | openapi.yaml |
| 26 | `market get-ipo-list` | 获取指定市场的 IPO 列表 | openapi.yaml |
| 27 | `market get-global-state` | 获取全局市场状态 | openapi.yaml |
| 28 | `market request-trading-days` | 获取交易日历 | openapi.yaml |

---

## Operation Flow

### Step 1 — Identify request type and load reference

| User intent | Reference to load |
|---|---|
| Basic Data | {baseDir}/references/basic-data-commands.md |
| F10 Infos | {baseDir}/references/f10-infos-commands.md |
| Market | {baseDir}/references/market-commands.md |
| Rank Data | {baseDir}/references/rank-data-commands.md |
| Real Time Quotes | {baseDir}/references/real-time-quotes-commands.md |
| wealth Data | {baseDir}/references/wealth-data-commands.md |
| 跨步骤组合与典型调用顺序 | {baseDir}/references/workflows.md |

### Step 2 — Verify the CLI exists and inspect the command

Run `noah --version` first. If it prints output, continue with `noah inspect market <command>` to confirm required parameters, body shape, response shape, and authentication requirements. If it does not print output, use the install steps declared in frontmatter, make sure devDependencies are installed, and rerun `noah --version` before continuing.

### Step 3 — Run commands immediately

Always invoke the globally installed CLI with `noah ...`. Do not replace the documented commands with local project execution forms.

All commands in this skill are read-only or read-dominant. No write confirmation is needed unless a command clearly changes server-side state.

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
