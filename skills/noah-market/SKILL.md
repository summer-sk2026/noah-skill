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

Command-driven skill for the globally installed Noah CLI.

---

## CLI 依赖（必读）

**本 skill 完全依赖全局安装的 `noah` 命令运行，没有替代执行路径。**

- 仓库：`https://github.com/summer-sk2026/noah-cli/tree/main`
- 可执行文件：`noah`（全局安装后系统可直接调用）
- 所有命令必须以 `noah ...` 形式调用，禁止使用 `npx`、`node src/...` 或项目内脚本
- 执行任何业务命令前必须先 `noah --version` 验证 CLI 可用

### 安装（仅当 `noah --version` 失败时执行）

```bash
git clone https://github.com/summer-sk2026/noah-cli.git
cd noah-cli
npm install --include=dev   # 必须 --include=dev，否则构建工具 tsup 不会被安装
npm run build                # 编译 TypeScript 源码
npm install -g .             # 全局安装，使 noah 可用
noah --version               # 验证安装成功
```

若安装失败，检查：Node.js >= 18、git 可用、每一步无报错、系统 PATH 包含全局 npm 目录。

---

## Operation Flow

**用户提出任何请求时，按以下顺序处理：**

### Step 1 — 验证 CLI

```bash
noah --version
```

无输出则先按上面安装步骤完成安装。

### Step 2 — 优先匹配工作流

**这是最重要的一步。** 加载 {baseDir}/references/workflows.md，判断用户请求是否匹配预定义的工作流场景：

1. 全面了解一只股票（市场状态 + 快照 + 资金流向 + 分时 + 逐笔）
2. 我的资产全貌（总资产 + 余额 + 公募 + 固收 + 现金宝）
3. 今天涨幅榜（排行榜 → 快照）
4. 某只股票走势（基本信息 → K 线）
5. 股东增减持追踪（增减持明细 + 当前股价）

- **匹配到工作流** → 必须按工作流定义的命令编排（并行/串行）执行全部命令，禁止只执行其中一条
- **没有匹配** → 再从 Command Index 选单条命令

### Step 3 — Inspect 每条目标命令

对每条要执行的命令都必须先运行：

```bash
noah inspect market <command>
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

## 注意事项

- 如用户未明确 market 命令名，先运行 inspect 查看命令详情，再决定具体命令。
- 部分查询命令可能要求 bearer 鉴权，inspect 显示需要时先提示执行 `noah init --token <bearerToken>`。
- 涉及时间范围、大结果集或高频行情时，先提醒结果可能较大，再视情况缩小参数范围。
- 不要把账户、持仓、订单、费用等交易请求路由到 market skill，应改用 trade skill。
- market skill 以查询、读取、分析型命令为主。
