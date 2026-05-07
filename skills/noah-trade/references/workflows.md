# 组合工作流

以下是 trade 命令的典型组合使用场景。每个工作流都假设 `noah --version` 已验证通过且 `noah init --token <bearerToken>` 已完成鉴权。

**重要：trade 下所有命令都需要 bearer 鉴权，执行前必须确保已完成 token 初始化。**

**注意：执行前务必先用 `noah inspect trade <command>` 确认实际参数名和格式。**

---

## 工作流 1：账户与持仓总览

场景：用户想了解当前账户状态和持仓情况。

```bash
# 1. 获取账户基础信息
noah trade get-account-info

# 2. 获取证券资产概览
noah trade get-sec-asset

# 3. 获取当前持仓列表（market 为必填参数）
noah trade get-positions --market HK
```

---

## 工作流 2：下单前确认可买可卖

场景：用户想买入或卖出某只股票，先确认可操作数量。

```bash
# 1. 先 inspect 确认参数
noah inspect trade get-stock-amount
noah inspect trade order-fee-query

# 2. 查询该股票可买可卖数量
noah trade get-stock-amount --code HK.00700

# 3. 查询融资最大可买数量（如需融资）
noah trade max-enable-buy-amt --code HK.00700

# 4. 查询下单预估费用（参数名以 inspect 输出为准）
noah trade order-fee-query --code HK.00700 --qty 100 --price 350
```

---

## 工作流 3：订单跟踪

场景：用户想查看今天的委托和成交情况。

```bash
# 1. 获取当日订单列表
noah trade get-order-list

# 2. 获取当日未完成委托
noah trade get-today-order-list

# 3. 获取当日成交列表
noah trade get-today-deal-list

# 4. 查看某个订单的详情（从上面结果中获取 order_id）
noah trade get-order-detail --order_id 123456

# 5. 查看该订单的费用明细
noah trade get-order-fee-detail --order_id 123456
```

---

## 工作流 4：历史订单与成交回顾

场景：用户想回顾一段时间内的交易记录。

```bash
# 先 inspect 确认时间参数名
noah inspect trade get-history-order-list
noah inspect trade get-history-deal-list

# 获取历史订单列表（参数名以 inspect 为准）
noah trade get-history-order-list --start_date 2025-04-01 --end_date 2025-04-30

# 获取历史成交列表
noah trade get-history-deal-list --start_date 2025-04-01 --end_date 2025-04-30

# 获取已完成订单列表
noah trade get-finished-order-list
```

---

## 工作流 5：资金流水与汇率

场景：用户想查看资金变动或做币种换算。

```bash
# 先 inspect 确认参数
noah inspect trade get-sec-capital-flow
noah inspect trade convert-ufg-money-balance

# 获取证券资金流水
noah trade get-sec-capital-flow --start_date 2025-04-01 --end_date 2025-04-30

# 不同币种汇率换算
noah trade convert-ufg-money-balance --from_currency USD --to_currency HKD --amount 10000
```

---

## 通用原则

- trade 下所有命令都需要 bearer 鉴权，执行前确认 `noah init --token <bearerToken>` 已完成
- 每个命令执行前，先用 `noah inspect trade <command>` 确认实际参数名和是否必填
- 参数名和可选值以 inspect 输出为准，不要猜测
- 历史查询类命令可能返回大量数据，建议限定时间范围
- 涉及金额、数量的操作要特别注意参数准确性
