# Market

## get-stock-basicinfo

- 命令：`noah market get-stock-basicinfo`
- 查看详情：`noah inspect market get-stock-basicinfo`
- 摘要：获取指定市场中特定类型或特定股票的基本信息
- 描述：对应 Futu get_stock_basicinfo / GetStaticInfo
- 标签：Market
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-stock-basicinfo
摘要: 获取指定市场中特定类型或特定股票的基本信息
描述: 对应 Futu get_stock_basicinfo / GetStaticInfo
请求: GET /quote/get_stock_basicinfo
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getStockBasicInfo
Path 参数:
无
Query 参数:
--market <EnumMarket> [必填] 市场 可选值: "HK", "US", "SH", "SZ", "BK", "SG", "JPN", "FRA", "GER", "FX", "BKHK", "BKUS", "UK", "CC", "PJ"
--stock_type <EnumSecurityType> [可选] 证券类型，不传则返回全部 可选值: "STOCK", "IDX", "ETF", "WARRANT", "BOND", "ALL"
--code_list <string> [可选] 股票代码列表，逗号分隔；不传则返回该市场该类型下全部
```

---

## get-stock-filter

- 命令：`noah market get-stock-filter`
- 查看详情：`noah inspect market get-stock-filter`
- 摘要：条件选股
- 描述：对应 Futu get_stock_filter / StockFilter。
请求参数通过 JSON 请求体（application/json）传递，避免 GET query 无法绑定复杂筛选列表的问题。

- 标签：Market
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-stock-filter
摘要: 条件选股
描述: 对应 Futu get_stock_filter / StockFilter。
请求参数通过 JSON 请求体（application/json）传递，避免 GET query 无法绑定复杂筛选列表的问题。
请求: POST /quote/get_stock_filter
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getStockFilter
Path 参数:
无
Query 参数:
无
Header 参数:
```

---

## get-ipo-list

- 命令：`noah market get-ipo-list`
- 查看详情：`noah inspect market get-ipo-list`
- 摘要：获取指定市场的 IPO 列表
- 描述：对应 Futu get_ipo_list / GetIpoList
- 标签：Market
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-ipo-list
摘要: 获取指定市场的 IPO 列表
描述: 对应 Futu get_ipo_list / GetIpoList
请求: GET /quote/get_ipo_list
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getIpoList
Path 参数:
无
Query 参数:
--market <EnumMarket> [必填] 市场 可选值: "HK", "US", "SH", "SZ", "BK", "SG", "JPN", "FRA", "GER", "FX", "BKHK", "BKUS", "UK", "CC", "PJ"
Header 参数:
无
```

---

## get-global-state

- 命令：`noah market get-global-state`
- 查看详情：`noah inspect market get-global-state`
- 摘要：获取全局市场状态
- 描述：对应 Futu get_global_state / GetGlobalState
- 标签：Market
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-global-state
摘要: 获取全局市场状态
描述: 对应 Futu get_global_state / GetGlobalState
请求: GET /quote/get_global_state
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getGlobalState
Path 参数:
无
Query 参数:
无
Header 参数:
无
```

---

## request-trading-days

- 命令：`noah market request-trading-days`
- 查看详情：`noah inspect market request-trading-days`
- 摘要：获取交易日历
- 描述：对应 Futu request_trading_days / RequestTradeDate
- 标签：Market
- 鉴权：需要 bearer 鉴权。

```text
命令: market request-trading-days
摘要: 获取交易日历
描述: 对应 Futu request_trading_days / RequestTradeDate
请求: GET /quote/request_trading_days
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: requestTradingDays
Path 参数:
无
Query 参数:
--market <EnumMarket> [必填] 市场 可选值: "HK", "US", "SH", "SZ", "BK", "SG", "JPN", "FRA", "GER", "FX", "BKHK", "BKUS", "UK", "CC", "PJ"
--start <string> [必填] 开始日期 yyyyMMdd
--end <string> [必填] 结束日期 yyyyMMdd
```

