# Market 工作流

以下工作流描述了用户常见请求对应的命令编排。每条命令执行前必须先 `noah inspect market <command>` 确认参数。

---

## 工作流：全面了解一只股票

用户说："帮我看看腾讯现在什么情况"

### 并行执行（互不依赖）：

```bash
noah market get-market-state --code_list HK.00700
noah market get-market-snapshot --code_list HK.00700
noah market get-capital-flow --code_list HK.00700
```

### 串行执行（依赖上一步确认市场已开盘）：

```bash
noah market get-rt-data --code_list HK.00700
noah market get-rt-ticker --code_list HK.00700
```

### 汇总输出：
- 市场状态（是否开盘）
- 最新价、涨跌幅、成交量（快照）
- 资金流向（净流入/流出）
- 分时走势
- 最近逐笔成交

---

## 工作流：我的资产全貌

用户说："看看我现在有多少钱"

### 并行执行：

```bash
noah market total-asset --toCurrency HKD
noah market balance-list
noah market hold-share-list
noah market fixed-income
noah market cash-total-asset
```

### 汇总输出：
- 总资产（按币种汇总）
- 现金余额
- 公募持仓
- 固收类资产
- 现金宝余额

---

## 工作流：今天有什么涨得好的股票

用户说："看看港股今天涨幅榜"

### 串行执行：

```bash
# 第 1 步：获取排行榜
noah market get-stock-rank --market HK --rank_type 1

# 第 2 步：对排行榜前几名获取快照详情（从第 1 步结果中取 code）
noah market get-market-snapshot --code_list HK.00700,HK.09988,HK.01024
```

### 汇总输出：
- 涨幅排行列表
- 排名靠前个股的实时快照

---

## 工作流：某只股票最近走势如何

用户说："看看苹果最近一个月的 K 线"

### 串行执行：

```bash
# 第 1 步：获取基本信息确认股票代码有效
noah market get-stock-basicinfo --market US --stock_type 1

# 第 2 步：获取时间范围 K 线
noah market get-cur-kline-date --code_list US.AAPL --start_time 2025-04-01 --end_time 2025-05-01
```

### 汇总输出：
- K 线数据（开高低收、成交量）
- 区间涨跌幅

---

## 工作流：股东最近有没有增减持

用户说："看看腾讯最近有没有大股东减持"

### 并行执行：

```bash
noah market shareholder-inc-red-hold-by-ucode --code HK.00700
noah market get-market-snapshot --code_list HK.00700
```

### 汇总输出：
- 增减持明细（时间、股东、方向、数量）
- 当前股价作为参考

---

## 编排原则

- **并行**：命令之间无数据依赖时，同时执行以提高效率
- **串行**：后续命令需要前一步的输出结果（如 code_list 来自排行榜结果）时，必须等前一步完成
- 每条命令执行前都必须先 inspect 确认参数
- 汇总时将多条命令的结果整合为用户可理解的摘要
