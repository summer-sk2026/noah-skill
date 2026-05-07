# 组合工作流

以下是 market 命令的典型组合使用场景。每个工作流都假设 `noah --version` 已验证通过。

**注意：执行前务必先用 `noah inspect market <command>` 确认实际参数名和格式。**

---

## 工作流 1：查看某只股票的实时行情全貌

场景：用户想了解一只股票当前的完整行情状态。

```bash
# 1. 先确认市场是否开盘（code_list 为必填参数）
noah market get-market-state --code_list HK.00700

# 2. 获取该股票的市场快照（最新价、涨跌幅、成交量等）
noah market get-market-snapshot --code_list HK.00700

# 3. 获取实时分时数据
noah market get-rt-data --code_list HK.00700

# 4. 获取实时逐笔成交
noah market get-rt-ticker --code_list HK.00700
```

---

## 工作流 2：K 线分析

场景：用户想查看某只股票的 K 线走势做技术分析。

```bash
# 1. 先 inspect 确认参数（不同 K 线命令参数不同）
noah inspect market get-cur-kline
noah inspect market get-cur-kline-date

# 2. 获取实时 K 线
noah market get-cur-kline --code_list US.AAPL

# 3. 获取指定时间范围的 K 线（参数名以 inspect 输出为准）
noah market get-cur-kline-date --code_list US.AAPL --start_time 2025-01-01 --end_time 2025-03-01
```

---

## 工作流 3：排行榜与选股

场景：用户想找涨幅靠前的股票，再查看具体信息。

```bash
# 1. 先 inspect 确认排行榜参数
noah inspect market get-stock-rank

# 2. 获取排行榜数据
noah market get-stock-rank --market HK --rank_type 1

# 3. 对感兴趣的股票做条件选股
noah inspect market get-stock-filter
noah market get-stock-filter --market HK

# 4. 查看选中股票的基本信息
noah market get-stock-basicinfo --market HK --stock_type 1
```

---

## 工作流 4：股东增减持追踪

场景：用户想了解某只股票或某个时间段的股东增减持情况。

```bash
# 先 inspect 确认各命令的参数要求
noah inspect market shareholder-inc-red-hold-by-ucode
noah inspect market shareholder-inc-red-hold-by-date
noah inspect market shareholder-inc-red-hold

# 按股票代码查询
noah market shareholder-inc-red-hold-by-ucode --code HK.00700

# 或按时间范围查询（参数名以 inspect 为准）
noah market shareholder-inc-red-hold-by-date --start_date 2025-01-01 --end_date 2025-03-01

# 或按市场范围查询
noah market shareholder-inc-red-hold --market HK
```

---

## 工作流 5：用户资产总览

场景：用户想查看自己的资产汇总和各类持仓。

```bash
# 1. 查看资产汇总
noah market total-asset --toCurrency HKD

# 2. 查看公募持仓
noah market hold-share-list

# 3. 查看固收类资产
noah market fixed-income

# 4. 查看余额列表
noah market balance-list
```

---

## 工作流 6：IPO 与交易日历

场景：用户想了解近期 IPO 和交易日安排。

```bash
# 1. 先 inspect 确认参数
noah inspect market get-ipo-list
noah inspect market request-trading-days

# 2. 获取 IPO 列表
noah market get-ipo-list --market HK

# 3. 获取交易日历
noah market request-trading-days --market HK

# 4. 获取全局市场状态
noah market get-global-state
```

---

## 通用原则

- 每个命令执行前，先用 `noah inspect market <command>` 确认实际参数名和是否必填
- 如果 inspect 显示需要 bearer 鉴权，先执行 `noah init --token <bearerToken>`
- 参数名和可选值以 inspect 输出为准，不要猜测
- 结果较大时考虑缩小时间范围或添加过滤条件
