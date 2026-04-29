# wealth Data

## fixed-income

- 命令：`noah market fixed-income`
- 查看详情：`noah inspect market fixed-income`
- 摘要：用户固收类资产通用查询接口
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market fixed-income
摘要: 用户固收类资产通用查询接口
描述: 用户固收类资产通用查询接口
请求: POST /wealth/fixed_income
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: postWealthFixedIncome
Path 参数:
无
Query 参数:
无
Header 参数:
无
```

---

## total-asset

- 命令：`noah market total-asset`
- 查看详情：`noah inspect market total-asset`
- 摘要：资产信息汇总
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market total-asset
摘要: 资产信息汇总
描述: 资产信息汇总
请求: GET /wealth/total_asset
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getWealthTotalAsset
Path 参数:
无
Query 参数:
--toCurrency <EntityCashCurrencyCode> [必填] 币种 可选值: "CNY", "HKD", "USD", "EUR", "JPY", "GBP", "TWD", "KRW", "CAD", "CNH", "CHF", "SEK", "SGD", "AUD", "ZAR", "NZD", "OTH"
Header 参数:
无
```

---

## hold-share-list

- 命令：`noah market hold-share-list`
- 查看详情：`noah inspect market hold-share-list`
- 摘要：公募信息获取
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market hold-share-list
摘要: 公募信息获取
描述: 公募信息获取
请求: GET /wealth/hold_share_list
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getWealthHoldShareList
Path 参数:
无
Query 参数:
--toCurrency <EntityCashCurrencyCode> [必填] 币种 可选值: "CNY", "HKD", "USD", "EUR", "JPY", "GBP", "TWD", "KRW", "CAD", "CNH", "CHF", "SEK", "SGD", "AUD", "ZAR", "NZD", "OTH"
Header 参数:
无
```

---

## query-private-contract-asset-list

- 命令：`noah market query-private-contract-asset-list`
- 查看详情：`noah inspect market query-private-contract-asset-list`
- 摘要：私募查询接口
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market query-private-contract-asset-list
摘要: 私募查询接口
描述: 私募查询接口
请求: POST /wealth/query_private_contract_asset_list
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: postWealthQueryPrivateContractAssetList
Path 参数:
无
Query 参数:
无
Header 参数:
无
```

---

## cash-total-asset

- 命令：`noah market cash-total-asset`
- 查看详情：`noah inspect market cash-total-asset`
- 摘要：现金宝
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market cash-total-asset
摘要: 现金宝
描述: 现金宝
请求: GET /wealth/cash_total_asset
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getWealthCashTotalAsset
Path 参数:
无
Query 参数:
无
Header 参数:
无
```

---

## bank-deposit-hold-detail

- 命令：`noah market bank-deposit-hold-detail`
- 查看详情：`noah inspect market bank-deposit-hold-detail`
- 摘要：银行定存存续或到期详情
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market bank-deposit-hold-detail
摘要: 银行定存存续或到期详情
描述: 银行定存存续或到期详情
请求: GET /wealth/bank_deposit_hold_detail
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getWealthBankDepositHoldDetail
Path 参数:
无
Query 参数:
--purchaseSubOrderNo <string> [必填] 买入子订单号
--redeemSubOrderNo <string> [可选] 赎回订单号 非必须
Header 参数:
```

---

## user-asset-query-detail

- 命令：`noah market user-asset-query-detail`
- 查看详情：`noah inspect market user-asset-query-detail`
- 摘要：用户固收类存量-存续详情接口
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market user-asset-query-detail
摘要: 用户固收类存量-存续详情接口
描述: 用户固收类存量-存续详情接口
请求: POST /wealth/user_asset_query_detail
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: postWealthUserAssetQueryDetail
Path 参数:
无
Query 参数:
无
Header 参数:
无
```

---

## balance-list

- 命令：`noah market balance-list`
- 查看详情：`noah inspect market balance-list`
- 摘要：用户余额列表
- 标签：wealth Data
- 鉴权：需要 bearer 鉴权。

```text
命令: market balance-list
摘要: 用户余额列表
描述: 用户余额列表
请求: GET /wealth/balance_list
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getWealthBalanceList
Path 参数:
无
Query 参数:
无
Header 参数:
无
```

