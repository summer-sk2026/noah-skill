# Market

## get-stock-basicinfo

- 命令：`noah market get-stock-basicinfo`
- 查看详情：`noah inspect market get-stock-basicinfo`
- 摘要：获取指定市场中特定类型或特定股票的基本信息
- 描述：对应 Futu get_stock_basicinfo / GetStaticInfo
- 标签：Market
- 鉴权：需要 bearer 鉴权。

---

## get-stock-filter

- 命令：`noah market get-stock-filter`
- 查看详情：`noah inspect market get-stock-filter`
- 摘要：条件选股
- 描述：对应 Futu get_stock_filter / StockFilter。
请求参数通过 JSON 请求体（application/json）传递，避免 GET query 无法绑定复杂筛选列表的问题。

- 标签：Market
- 鉴权：需要 bearer 鉴权。

---

## get-ipo-list

- 命令：`noah market get-ipo-list`
- 查看详情：`noah inspect market get-ipo-list`
- 摘要：获取指定市场的 IPO 列表
- 描述：对应 Futu get_ipo_list / GetIpoList
- 标签：Market
- 鉴权：需要 bearer 鉴权。

---

## get-global-state

- 命令：`noah market get-global-state`
- 查看详情：`noah inspect market get-global-state`
- 摘要：获取全局市场状态
- 描述：对应 Futu get_global_state / GetGlobalState
- 标签：Market
- 鉴权：需要 bearer 鉴权。

---

## request-trading-days

- 命令：`noah market request-trading-days`
- 查看详情：`noah inspect market request-trading-days`
- 摘要：获取交易日历
- 描述：对应 Futu request_trading_days / RequestTradeDate
- 标签：Market
- 鉴权：需要 bearer 鉴权。
