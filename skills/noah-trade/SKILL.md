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

Command-driven skill for the globally installed Noah CLI.

---

## CLI 依赖（必读）

**本 skill 完全依赖全局安装的 `noah` 命令运行，没有替代执行路径。**

- 仓库：`https://github.com/summer-sk2026/noah-cli/tree/main`
- 可执行文件：`noah`（全局安装后系统可直接调用）
- **要求版本：`0.1.0`**（必须严格匹配，版本不符必须重装）
- 所有命令必须以 `noah ...` 形式调用，禁止使用 `npx`、`node src/...` 或项目内脚本

### 版本校验与安装策略

执行任何业务命令前必须先运行 `noah --version` 并检查输出：

- **输出为空 / 命令不存在** → 按下方 "安装步骤" 全新安装
- **输出 `0.1.0`** → 版本正确，可继续执行后续步骤
- **输出其他版本（例如旧版本）** → 版本不匹配，必须按下方 "重装步骤" 拉取最新代码重装

### 安装步骤（首次安装）

```bash
git clone https://github.com/summer-sk2026/noah-cli.git
cd noah-cli
npm install --include=dev   # 必须 --include=dev，否则构建工具 tsup 不会被安装
npm run build                # 编译 TypeScript 源码
npm install -g .             # 全局安装，使 noah 可用
noah --version               # 应输出 0.1.0
```

### 重装步骤（版本不匹配）

如果 `noah --version` 输出的版本不是 `0.1.0`，执行：

```bash
# 1. 清理旧的全局安装
npm uninstall -g noah-cli

# 2. 如果本地已有 noah-cli 目录，拉取最新代码；否则重新 clone
cd noah-cli 2>/dev/null && git pull || git clone https://github.com/summer-sk2026/noah-cli.git
cd noah-cli

# 3. 重新构建并全局安装
npm install --include=dev
npm run build
npm install -g .

# 4. 验证版本已更新
noah --version   # 应输出 0.1.0
```

若 `noah --version` 仍不是 `0.1.0`，检查：系统 PATH 是否指向正确的全局 npm 目录，是否存在多个 noah 安装。

---

## Operation Flow

**用户提出任何请求时，按以下顺序处理：**

### Step 1 — 验证 CLI 版本

```bash
noah --version
```

- 输出 `0.1.0` → 继续 Step 2
- 输出为空或命令不存在 → 执行 "安装步骤"，完成后重新验证
- 输出其他版本 → 执行 "重装步骤"，完成后重新验证

**版本不匹配时禁止继续执行任何业务命令。**

### Step 2 — 优先匹配工作流

**这是最重要的一步。** 加载 {baseDir}/references/workflows.md，判断用户请求是否匹配预定义的工作流场景：

1. 下单前确认（账户 + 可买数量 + 融资额度 → 预估费用）
2. 今日交易情况（委托单 + 成交 + 未完成）
3. 订单完整信息（订单详情 + 费用明细）
4. 历史交易回顾（历史订单 + 成交 + 资金流水）
5. 持仓和资产（持仓 → 资产总览）

- **匹配到工作流** → 必须按工作流定义的命令编排（并行/串行）执行全部命令，禁止只执行其中一条
- **没有匹配** → 再从 Command Index 选单条命令

### Step 3 — Inspect 每条目标命令

对每条要执行的命令都必须先运行：

```bash
noah inspect trade <command>
```

从输出中获取必填参数、可选参数、enum 可选值、鉴权要求。禁止凭记忆猜测参数。

### Step 4 — 鉴权（若 inspect 输出含 `bearerAuth`）

```bash
noah init --token <bearerToken>
```

### Step 5 — 执行并汇总

- 工作流模式：按定义的并行/串行规则执行所有命令
- 单命令模式：直接执行
- 汇总所有结果为用户可理解的摘要

---

## Command Index

| # | Command | Summary |
|---|---|---|
| 1 | `noah trade get-account-info` | 获取账户信息 |
| 2 | `noah trade get-positions` | 获取持仓列表 |
| 3 | `noah trade get-stock-amount` | 获取证券可买可卖数量 |
| 4 | `noah trade max-enable-buy-amt` | 查询融资最大可买数量 |
| 5 | `noah trade get-sec-asset` | 获取证券资产 |
| 6 | `noah trade get-sec-capital-flow` | 获取证券资金流水 |
| 7 | `noah trade get-order-list` | 获取当日订单列表 |
| 8 | `noah trade get-today-order-list` | 获取当日未完成委托订单列表 |
| 9 | `noah trade get-history-order-list` | 获取历史订单列表 |
| 10 | `noah trade get-today-deal-list` | 获取当日成交列表 |
| 11 | `noah trade get-history-deal-list` | 获取历史成交列表 |
| 12 | `noah trade get-finished-order-list` | 获取已完成订单列表 |
| 13 | `noah trade get-order-detail` | 获取订单详情 |
| 14 | `noah trade get-order-fee-detail` | 获取订单费用详情 |
| 15 | `noah trade order-fee-query` | 查询下单预估费用 |
| 16 | `noah trade convert-ufg-money-balance` | 不同币种汇率换算 |
| 17 | `noah trade query-push-data` | 查询推送数据 |

---

## 注意事项

- trade skill 下所有命令都需要 bearer 鉴权；执行前确认 `noah init --token <bearerToken>` 已完成。
- 如果用户请求属于行情、榜单、K 线、F10 或标的信息，不要路由到 trade skill，应改用 market skill。
- 历史订单、历史成交类命令可能返回较大结果集，必要时提醒用户缩小时间范围。
- 如 inspect 输出包含必填 body 字段，应严格按字段要求构造请求，不要猜测。
- trade skill 以账户、持仓、订单、成交、费用等交易相关命令为主。
