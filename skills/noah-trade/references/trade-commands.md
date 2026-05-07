# Trade

## get-account-info

- 命令：`noah trade get-account-info`
- 查看详情：`noah inspect trade get-account-info`
- 摘要：获取账户信息
- 描述：返回当前交易账户的基础信息以及开户状态。
请求 header 需传入 `Authorization: Bearer <token>`。
统一响应中的业务结果位于 `data` 字段。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-positions

- 命令：`noah trade get-positions`
- 查看详情：`noah inspect trade get-positions`
- 摘要：获取持仓列表
- 描述：查询当前持仓数据。
请求 header 需传入 `Authorization: Bearer <token>`。
`market` 为必填参数，用于向下游传递查询市场并返回对应市场持仓。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-stock-amount

- 命令：`noah trade get-stock-amount`
- 查看详情：`noah inspect trade get-stock-amount`
- 摘要：获取证券可买可卖数量
- 描述：查询指定证券在指定委托属性和交易时段下的可买数量、可卖数量。
请求 header 需传入 `Authorization: Bearer <token>`。
`code` 使用开放接口格式 `MARKET.CODE`，内部会转换为 sec-trade 所需的市场和证券代码。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## max-enable-buy-amt

- 命令：`noah trade max-enable-buy-amt`
- 查看详情：`noah inspect trade max-enable-buy-amt`
- 摘要：查询融资最大可买数量
- 描述：查询指定证券在指定委托属性、委托价格和交易时段下的融资最大可买数量。
请求 header 需传入 `Authorization: Bearer <token>`。
`code` 使用开放接口格式 `MARKET.CODE`，内部会转换为 sec-trade 所需的市场和证券代码。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-sec-asset

- 命令：`noah trade get-sec-asset`
- 查看详情：`noah inspect trade get-sec-asset`
- 摘要：获取证券资产
- 描述：查询当前交易账户对应分组下的证券资产信息。
请求 header 需传入 `Authorization: Bearer <token>`。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-sec-capital-flow

- 命令：`noah trade get-sec-capital-flow`
- 查看详情：`noah inspect trade get-sec-capital-flow`
- 摘要：获取证券资金流水
- 描述：查询当前交易账户对应分组下的证券资金流水明细。
请求 header 需传入 `Authorization: Bearer <token>`。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-order-list

- 命令：`noah trade get-order-list`
- 查看详情：`noah inspect trade get-order-list`
- 摘要：获取当日订单列表
- 描述：查询当前当日有效订单或当日订单记录。
请求 header 需传入 `Authorization: Bearer <token>`。
`market` 为必填参数，用于向下游传递查询市场。
返回结果经过统一封装，订单数组位于 `data` 字段。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-today-order-list

- 命令：`noah trade get-today-order-list`
- 查看详情：`noah inspect trade get-today-order-list`
- 摘要：获取当日未完成委托订单列表
- 描述：查询当日未完成委托订单列表。
请求 header 需传入 `Authorization: Bearer <token>`。
当未传 `order_status` 时，默认按未完成状态集合过滤：`0,1,2,3,4,7,A,B,C,D,E,H,W,N,O,P`。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-history-order-list

- 命令：`noah trade get-history-order-list`
- 查看详情：`noah inspect trade get-history-order-list`
- 摘要：获取历史订单列表
- 描述：查询历史委托订单列表。
请求 header 需传入 `Authorization: Bearer <token>`。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-today-deal-list

- 命令：`noah trade get-today-deal-list`
- 查看详情：`noah inspect trade get-today-deal-list`
- 摘要：获取当日成交列表
- 描述：查询当日成交数据。
请求 header 需传入 `Authorization: Bearer <token>`。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-history-deal-list

- 命令：`noah trade get-history-deal-list`
- 查看详情：`noah inspect trade get-history-deal-list`
- 摘要：获取历史成交列表
- 描述：查询历史成交数据。
请求 header 需传入 `Authorization: Bearer <token>`。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-finished-order-list

- 命令：`noah trade get-finished-order-list`
- 查看详情：`noah inspect trade get-finished-order-list`
- 摘要：获取已完成订单列表
- 描述：查询指定日期范围内的已完成订单记录。
请求 header 需传入 `Authorization: Bearer <token>`。
本接口提供分页参数，并同时支持常用过滤条件。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-order-detail

- 命令：`noah trade get-order-detail`
- 查看详情：`noah inspect trade get-order-detail`
- 摘要：获取订单详情
- 描述：查询指定订单的详细信息，包括成交记录、费用明细和时间线。
请求 header 需传入 `Authorization: Bearer <token>`。
订单详情统一封装在 `data` 字段中返回。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## get-order-fee-detail

- 命令：`noah trade get-order-fee-detail`
- 查看详情：`noah inspect trade get-order-fee-detail`
- 摘要：获取订单费用详情
- 描述：查询指定订单的费用信息。
请求 header 需传入 `Authorization: Bearer <token>`。
成功时仅返回订单 ID、总费用和费用明细。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## order-fee-query

- 命令：`noah trade order-fee-query`
- 查看详情：`noah inspect trade order-fee-query`
- 摘要：查询下单预估费用
- 描述：在正式下单前预估交易费用。
请求 header 需传入 `Authorization: Bearer <token>`。
成功时返回市场、证券代码、数量、价格、费用明细以及总费用。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## convert-ufg-money-balance

- 命令：`noah trade convert-ufg-money-balance`
- 查看详情：`noah inspect trade convert-ufg-money-balance`
- 摘要：不同币种汇率换算
- 描述：根据源币种、目标币种和金额，基于结算汇率进行换算。
请求 header 需传入 `Authorization: Bearer <token>`。
成功时返回换算后的金额。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。

---

## query-push-data

- 命令：`noah trade query-push-data`
- 查看详情：`noah inspect trade query-push-data`
- 摘要：查询推送数据
- 描述：查询 sec-trade 推送数据。
请求 header 需传入 `Authorization: Bearer <token>`。
成功时返回底层推送记录列表。

- 标签：Trade
- 鉴权：需要 bearer 鉴权。
