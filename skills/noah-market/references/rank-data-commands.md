# Rank Data

## get-stock-rank

- 命令：`noah market get-stock-rank`
- 查看详情：`noah inspect market get-stock-rank`
- 摘要：获取排行榜数据
- 标签：Rank Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-stock-rank
摘要: 获取排行榜数据
描述: 获取排行榜数据
请求: GET /rank/get_stock_rank
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getRankGetStockRank
Path 参数:
无
Query 参数:
--market_codes <EnumMarkets> [必填] 市场代码 可选值: "HK", "SG", "US"
--rank_field <EnumQuoteSortField> [必填] 排行字段 可选值: "lastPrice", "raisePercent", "raise", "exchange", "raiseSpeed", "mainNetInflow", "totalTradeVol", "totalTurnover", "volumeRatio", "entrustRatio", "amplitude", "highPrice", "lowPrice", "openPrice", "preClose", "peDynamic", "peRatio", "circulationValue", "marketValue", "iopv", "nominalPrice", "stockRaisePercent", "increaseNum", "roe", "pnaRatio", "raisePercentOneYear", "leverageRatio", "maturityDay", "exercisePrice", "percOfStillOut", "premiumRatio", "effectiveGearing", "pStrPrice", "pStrPriceSpread", "bid1Price", "ask1Price", "currencyOneCode", "currencySecondCode", "orderNum", "baseOrderNum", "raisePercent1y", "raisePercent1m", "raisePercentYtd", "assetSize", "shareIssued"
--ascend <boolean> [必填] 排行顺序
```

