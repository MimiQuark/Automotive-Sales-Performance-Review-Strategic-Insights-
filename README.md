# 汽车销售经营复盘与策略洞察

[![Syntax CI](https://github.com/MimiJimmy001/Automotive-Sales-Performance-Review-and-Strategic-Insights/actions/workflows/ci.yml/badge.svg)](https://github.com/MimiJimmy001/Automotive-Sales-Performance-Review-and-Strategic-Insights/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

以某汽车经销商 2023–2025 年的 8 万条销售记录为分析样本，围绕"卖什么、什么时候卖、卖给谁、怎么卖、谁来卖"五个业务问题，用 SQL 完成指标计算，用 Python 实现同口径分析并生成图表，最终汇总为一份 Excel BI 看板，形成从数据到经营结论的完整分析闭环。

**技术栈**：MySQL · Python（Pandas / Matplotlib）· Excel（openpyxl）

## 可视化与可解释性

- [完整可视化指南](docs/VISUAL_GUIDE.md)：项目思维导图、数据流程、指标树、结论与限制地图

## 快速开始

```bash
pip install -r requirements.txt
python visualize.py          # 生成 6 张分析图
python excel_dashboard.py    # 生成 Excel BI 看板
```

`analysis.sql` 为 MySQL 建表与 9 组核心分析查询，可按需在数据库中执行。

## 分析框架

| 业务问题 | 分析维度 | 方法 |
|---|---|---|
| 卖什么 | 品牌 / 车型 / 车身类别 | 销售额排行、均价对比、SUV vs 轿车（新能源车型单独标注） |
| 什么时候卖 | 时间趋势 | 月度走势、环比、年度同比、季节性 |
| 卖给谁 | 客户画像 | 年龄段 × 性别交叉、客单价分布 |
| 怎么卖 | 销售方式 | 全款 / 贷款 / 分期结构、折扣率、金融渗透率 |
| 谁来卖 | 团队效能 | 区域对比、销售人员业绩排名 |

## 核心结论

- **品牌格局**：大众、宝马、奔驰营收接近（34.8–35.0 亿元）；大众以 1.39 万台销量居首，宝马、奔驰销量约 1.05 万台，但凭借约 33 万元的均价实现相近营收，呈现"量"与"价"两条路径
- **品类结构**：SUV 是绝对主力，销售额 105.6 亿元（均价 25.3 万），约为轿车（76.1 亿、均价 19.9 万）的 1.4 倍
- **季节规律**：销量呈明显的"年末冲高、春节回落"周期——每年 12 月前后冲量，2 月春节跌入谷底，月度环比波动区间约 -47% 至 +123%
- **客户画像**：26–35 岁为第一大购车人群（约 2.8 万人，占 35.0%），男性客户数量全面高于女性；但各年龄段客单价几乎持平（约 22.6–22.8 万），说明消费力差异主要体现在"买不买"而非"买多贵"
- **支付方式**：贷款占 49.7%、分期占 20.0%、全款占 30.3%，贷款与分期合计 69.7%，金融渗透率高，是影响成交的重要杠杆

## 成果展示

| 品牌营收排名 | 月度趋势 |
|---|---|
| ![品牌营收](output/01_brand_revenue.png) | ![月度趋势](output/02_monthly_trend.png) |

| 区域分析 | 客户画像 |
|---|---|
| ![区域分析](output/03_region_analysis.png) | ![客户画像](output/04_customer_profile.png) |

| 品类与支付 | 年度对比 |
|---|---|
| ![品类支付](output/05_category_payment.png) | ![年度对比](output/06_annual_comparison.png) |

完整的可视化汇总见 `output/汽车销售BI分析看板.xlsx`（含 KPI 指标卡与趋势、区域、品牌图表）。

## 数据集

| 表 | 规模 | 说明 |
|---|---|---|
| `cars` | 46 款车型 | 7 大品牌，覆盖轿车 / SUV，含 12 款新能源车型，提供指导价 |
| `salespersons` | 103 人 | 按区域、城市分布 |
| `sales` | 80,000 条 | 2023–2025 年销售记录，含成交金额、客户性别 / 年龄段、支付方式、折扣率、是否贷款 / 分期 |

## 文件说明

| 文件 | 说明 |
|---|---|
| `analysis.sql` | 全部业务指标的 SQL 实现（MySQL，建表 + 9 组核心分析查询） |
| `visualize.py` | 6 张分析图表的生成代码（Pandas + Matplotlib） |
| `excel_dashboard.py` | Excel BI 看板生成代码（openpyxl 原生图表） |
| `data/` | 三张数据表 |
| `output/` | 分析图表与 Excel 看板成品 |
