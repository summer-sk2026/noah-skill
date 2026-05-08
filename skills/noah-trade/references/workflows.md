# Trade 工作流

以下工作流描述了用户常见交易请求对应的命令编排。每条命令执行前必须先 `noah inspect trade <command>` 确认参数。trade 下所有命令都需要 bearer 鉴权。

---

## 工作流：我想买一只股票，先看看能不能买

用户说："我想买腾讯，看看能买多少"

### 并行执行（互不依赖）：

```bash
noah trade get-account-info
noah trade get-stock-amount --code HK.00700
noah trade max-enable-buy-amt --code HK.00700
```

### 串行执行（依赖上一步获取的可买数量和价格）：

```bash
# 用上一步结果中的数量和当前价格预估费用
noah trade order-fee-query --code HK.00700 --qty 100 --price 350
```

### 汇总输出：
- 账户状态
- 可买数量
- 融资可买数量
- 预估交易费用

---

## 工作流：看看我今天的交易情况

用户说："今天下了哪些单，成交了多少"

### 并行执行：

```bash
noah trade get-order-list
noah trade get-today-deal-list
noah trade get-today-order-list
```

### 汇总输出：
- 当日全部委托单
- 未完成委托
- 已成交列表

---

## 工作流：查看某笔订单的完整信息

用户说："帮我看看订单 123456 的详情和费用"

### 并行执行（order_id 已知）：

```bash
noah trade get-order-detail --order_id 123456
noah trade get-order-fee-detail --order_id 123456
```

### 汇总输出：
- 订单状态、方向、价格、数量
- 手续费、印花税等费用明细

---

## 工作流：回顾上个月的交易记录

用户说："看看我上个月的交易记录"

### 并行执行：

```bash
noah trade get-history-order-list --start_date 2025-04-01 --end_date 2025-04-30
noah trade get-history-deal-list --start_date 2025-04-01 --end_date 2025-04-30
noah trade get-sec-capital-flow --start_date 2025-04-01 --end_date 2025-04-30
```

### 汇总输出：
- 历史委托列表
- 历史成交列表
- 资金流水（入金、出金、交易扣款）

---

## 工作流：看看我的持仓和资产

用户说："我港股持仓是什么情况"

### 串行执行：

```bash
# 第 1 步：获取持仓列表
noah trade get-positions --market HK

# 第 2 步：获取证券资产总览（与持仓对照）
noah trade get-sec-asset
```

### 汇总输出：
- 持仓列表（股票、数量、成本、市值、盈亏）
- 证券资产总览

---

## 编排原则

- **并行**：命令之间无数据依赖时，同时执行以提高效率
- **串行**：后续命令需要前一步的输出结果（如 order_id、code、数量）时，必须等前一步完成
- 每条命令执行前都必须先 inspect 确认参数
- 汇总时将多条命令的结果整合为用户可理解的摘要
