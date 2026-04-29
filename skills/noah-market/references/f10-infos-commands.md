# F10 Infos

## shareholder-inc-red-hold

- 命令：`noah market shareholder-inc-red-hold`
- 查看详情：`noah inspect market shareholder-inc-red-hold`
- 摘要：股东增减持明细榜单按市场范围
- 标签：F10 Infos
- 鉴权：需要 bearer 鉴权。

```text
命令: market shareholder-inc-red-hold
摘要: 股东增减持明细榜单按市场范围
描述: 股东增减持明细榜单按市场范围
请求: GET /infos/shareholder_inc_red_hold
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosShareholderIncRedHold
Path 参数:
无
Query 参数:
--current_page <number> [必填] 页码
--page_size <number> [必填] 页数
--market <EnumMarkets> [必填] 市场 可选值: "HK", "SG", "US"
```

---

## shareholder-inc-red-hold-by-date

- 命令：`noah market shareholder-inc-red-hold-by-date`
- 查看详情：`noah inspect market shareholder-inc-red-hold-by-date`
- 摘要：股东增减持明细榜单按时间范围
- 标签：F10 Infos
- 鉴权：需要 bearer 鉴权。

```text
命令: market shareholder-inc-red-hold-by-date
摘要: 股东增减持明细榜单按时间范围
描述: 股东增减持明细榜单按时间范围
请求: GET /infos/shareholder_inc_red_hold_by_date
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosShareholderIncRedHoldByDate
Path 参数:
无
Query 参数:
--current_page <number> [必填] 页码
--page_size <number> [必填] 页数
--market <EnumMarkets> [必填] 市场 可选值: "HK", "SG", "US"
```

---

## shareholder-inc-red-hold-by-ucode

- 命令：`noah market shareholder-inc-red-hold-by-ucode`
- 查看详情：`noah inspect market shareholder-inc-red-hold-by-ucode`
- 摘要：股东增减持明细榜单按股票代码范围
- 标签：F10 Infos
- 鉴权：需要 bearer 鉴权。

```text
命令: market shareholder-inc-red-hold-by-ucode
摘要: 股东增减持明细榜单按股票代码范围
描述: 股东增减持明细榜单按股票代码范围
请求: GET /infos/shareholder_inc_red_hold_by_ucode
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosShareholderIncRedHoldByUcode
Path 参数:
无
Query 参数:
--current_page <number> [必填] 页码
--page_size <number> [必填] 页数
--stock_code <string> [必填] 股票代码
```

---

## get-finance-us-infos

- 命令：`noah market get-finance-us-infos`
- 查看详情：`noah inspect market get-finance-us-infos`
- 摘要：获取美股财务数据
- 标签：F10 Infos
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-finance-us-infos
摘要: 获取美股财务数据
描述: 获取美股财务数据
请求: GET /infos/get_finance_us_infos
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosGetFinanceUsInfos
Path 参数:
无
Query 参数:
--stock_code <string> [必填] 股票代码
--type_code <EnumDateTypeConvertUtil> [必填] 数据类型 可选值: 1, 2, 3, 4, 5, 7
--year <number> [必填] 年份
```

---

## get-finance-hk-infos

- 命令：`noah market get-finance-hk-infos`
- 查看详情：`noah inspect market get-finance-hk-infos`
- 摘要：获取港股财务数据
- 标签：F10 Infos
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-finance-hk-infos
摘要: 获取港股财务数据
描述: 获取港股财务数据
请求: GET /infos/get_finance_hk_infos
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosGetFinanceHkInfos
Path 参数:
无
Query 参数:
--stock_code <string> [必填] 股票代码
--type_code <EnumDateTypeConvertUtil> [必填] 数据类型 可选值: 1, 2, 3, 4, 5, 7
--year <number> [必填] 年份
```

---

## get-us-analysis

- 命令：`noah market get-us-analysis`
- 查看详情：`noah inspect market get-us-analysis`
- 摘要：获取美股分析信息
- 标签：F10 Infos
- 鉴权：需要 bearer 鉴权。

```text
命令: market get-us-analysis
摘要: 获取美股分析信息
描述: 获取美股分析信息
请求: GET /infos/get_us_analysis
命名空间: market
来源规范: openapi.yaml
默认 Base URL: https://securities-open-api.t2.test.noahgrouptest.com
operationId: getInfosGetUsAnalysis
Path 参数:
无
Query 参数:
--stock_code <string> [必填] 股票代码
Header 参数:
无
```

