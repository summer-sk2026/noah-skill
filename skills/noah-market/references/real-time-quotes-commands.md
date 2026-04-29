# Real Time Quotes

## get-market-snapshot

- 命令：`noah market get-market-snapshot`
- 查看详情：`noah inspect market get-market-snapshot`
- 摘要：获取市场快照信息
- 标签：Real Time Quotes
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-market-snapshot
摘要: 获取市场快照信息
描述: 获取市场快照信息
请求: GET /quotes/get_market_snapshot
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getQuotesGetMarketSnapshot
Path 参数:
无
Query 参数:
--code_list <EntityCodeList> [必填]
Header 参数:
无
```

---

## get-rt-data

- 命令：`noah market get-rt-data`
- 查看详情：`noah inspect market get-rt-data`
- 摘要：获取实时分时
- 标签：Real Time Quotes
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-rt-data
摘要: 获取实时分时
描述: 获取实时分时
请求: GET /quotes/get_rt_data
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getQuotesGetRtData
Path 参数:
无
Query 参数:
--code <string> [必填]
Header 参数:
无
```

---

## get-cur-kline

- 命令：`noah market get-cur-kline`
- 查看详情：`noah inspect market get-cur-kline`
- 摘要：获取实时 K 线
- 标签：Real Time Quotes
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-cur-kline
摘要: 获取实时 K 线
描述: 获取实时 K 线
请求: GET /quotes/get_cur_kline
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getQuotesGetCurKline
Path 参数:
无
Query 参数:
--code <string> [可选]
--name <string> [可选]
--num <number> [必填] K线个数, 负数为向前查询
```

---

## get-cur-kline-date

- 命令：`noah market get-cur-kline-date`
- 查看详情：`noah inspect market get-cur-kline-date`
- 摘要：获取实时 K 线,根据时间范围筛选
- 标签：Real Time Quotes
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-cur-kline-date
摘要: 获取实时 K 线,根据时间范围筛选
描述: 获取实时 K 线,根据时间范围筛选
请求: GET /quotes/get_cur_kline_date
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getQuotesGetCurKlineDate
Path 参数:
无
Query 参数:
--code <string> [可选]
--name <string> [可选]
--from <string> [必填] 时间范围查询 yyyyMMddHHmmssSSS
```

---

## get-rt-ticker

- 命令：`noah market get-rt-ticker`
- 查看详情：`noah inspect market get-rt-ticker`
- 摘要：获取实时逐笔
- 标签：Real Time Quotes
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-rt-ticker
摘要: 获取实时逐笔
描述: 获取实时逐笔
请求: GET /quotes/get_rt_ticker
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getQuotesGetRtTicker
Path 参数:
无
Query 参数:
--code <string> [必填]
--num <number> [必填]
Header 参数:
```

---

## get-broker-queue

- 命令：`noah market get-broker-queue`
- 查看详情：`noah inspect market get-broker-queue`
- 摘要：获取实时经纪队列
- 标签：Real Time Quotes
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-broker-queue
摘要: 获取实时经纪队列
描述: 获取实时经纪队列
请求: GET /quotes/get_broker_queue
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getQuotesGetBrokerQueue
Path 参数:
无
Query 参数:
--code <string> [必填]
Header 参数:
无
```

