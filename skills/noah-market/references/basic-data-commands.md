# Basic Data

## get-capital-flow

- 命令：`noah market get-capital-flow`
- 查看详情：`noah inspect market get-capital-flow`
- 摘要：获取个股资金流向
- 标签：Basic Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-capital-flow
摘要: 获取个股资金流向
描述: 获取个股资金流向
请求: GET /infos/get_capital_flow
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosGetCapitalFlow
Path 参数:
无
Query 参数:
--stock_code <string> [必填] 股票代码
--num <number> [必填] 数量
Header 参数:
```

---

## get-market-state

- 命令：`noah market get-market-state`
- 查看详情：`noah inspect market get-market-state`
- 摘要：获取股票对应市场的市场状态
- 标签：Basic Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-market-state
摘要: 获取股票对应市场的市场状态
描述: 获取股票对应市场的市场状态
请求: GET /infos/get_market_state
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosGetMarketState
Path 参数:
无
Query 参数:
--code_list <EntityCodeList> [必填]
Header 参数:
无
```

