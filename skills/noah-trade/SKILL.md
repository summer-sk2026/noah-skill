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
    npm install
    npm run build
    npm install -g .
---

# Noah Trade CLI

Command-driven noah trade skill for the globally installed Noah CLI.

## Dependency

This skill depends on the Noah CLI project:
- repository: `https://github.com/summer-sk2026/noah-cli/tree/main`
- binary: `noah`
- all runtime commands in this skill must use the globally installed `noah` command
- do not execute this project through local project scripts or local entry points as a substitute for the global CLI

## Preflight

Before running any command:
- verify the `noah` command exists by running `noah --version`
- if `noah --version` prints output, treat the globally installed CLI as available
- if `noah --version` does not print output or the command is missing, follow the install instructions declared in this skill's frontmatter
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

If `noah --version` does not produce output, install the CLI using the frontmatter `agent.install` steps, then rerun `noah --version`. After installation succeeds, always run the global command form such as `noah market ...` or `noah trade ...`.

---

## Command Index

| # | Command | Summary | Source |
|---|---|---|---|
| 1 | `trade get-account-info` | 获取账户信息 | tradeopenapi.yaml |
| 2 | `trade get-positions` | 获取持仓列表 | tradeopenapi.yaml |
| 3 | `trade get-stock-amount` | 获取证券可买可卖数量 | tradeopenapi.yaml |
| 4 | `trade max-enable-buy-amt` | 查询融资最大可买数量 | tradeopenapi.yaml |
| 5 | `trade get-sec-asset` | 获取证券资产 | tradeopenapi.yaml |
| 6 | `trade get-sec-capital-flow` | 获取证券资金流水 | tradeopenapi.yaml |
| 7 | `trade get-order-list` | 获取当日订单列表 | tradeopenapi.yaml |
| 8 | `trade get-today-order-list` | 获取当日未完成委托订单列表 | tradeopenapi.yaml |
| 9 | `trade get-history-order-list` | 获取历史订单列表 | tradeopenapi.yaml |
| 10 | `trade get-today-deal-list` | 获取当日成交列表 | tradeopenapi.yaml |
| 11 | `trade get-history-deal-list` | 获取历史成交列表 | tradeopenapi.yaml |
| 12 | `trade get-finished-order-list` | 获取已完成订单列表 | tradeopenapi.yaml |
| 13 | `trade get-order-detail` | 获取订单详情 | tradeopenapi.yaml |
| 14 | `trade get-order-fee-detail` | 获取订单费用详情 | tradeopenapi.yaml |
| 15 | `trade order-fee-query` | 查询下单预估费用 | tradeopenapi.yaml |
| 16 | `trade convert-ufg-money-balance` | 不同币种汇率换算 | tradeopenapi.yaml |
| 17 | `trade query-push-data` | 查询推送数据 | tradeopenapi.yaml |

---

## Operation Flow

### Step 1 — Identify request type and load reference

| User intent | Reference to load |
|---|---|
| Trade | {baseDir}/references/trade-commands.md |
| 跨步骤组合与典型调用顺序 | {baseDir}/references/workflows.md |

### Step 2 — Verify the CLI exists and inspect the command

Run `noah --version` first. If it prints output, continue with `noah inspect trade <command>` to confirm required parameters, body shape, response shape, and authentication requirements. If it does not print output, use the install steps declared in frontmatter and rerun `noah --version` before continuing.

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
- trade skill 以账户、持仓、订单、成交、费用等交易相关命令为主。
