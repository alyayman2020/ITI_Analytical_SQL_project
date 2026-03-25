# 🛒 E-Commerce Platform — Analytical SQL & KPI Project

<div align="center">

![DuckDB](https://img.shields.io/badge/DuckDB-FFF000?style=flat-square&logo=duckdb&logoColor=black)
![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-3F4F75?style=flat-square&logo=plotly&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![mlxtend](https://img.shields.io/badge/mlxtend-Apriori-orange?style=flat-square)
![Star Schema](https://img.shields.io/badge/Schema-Star%20Schema-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![ITI](https://img.shields.io/badge/ITI-Data%20Science%20Track-red?style=flat-square)

**Information Technology Institute (ITI) · Data Science Track 2025/2026**
**Analytical SQL Module — Capstone Project**

*A complete analytical data warehouse with 21 window-function queries, 7 core KPIs,
and a hybrid SQL + ML product recommendation system.*

</div>

---

## 📌 Project Overview

E-commerce platforms generate millions of transactional records daily — but raw data
without analytical infrastructure is just noise. This project designs and implements a
**Star Schema data warehouse** from scratch, answers **21 complex business questions**
using advanced analytical SQL (window functions, CTEs, statistical functions), and builds
a **hybrid recommendation engine** that combines rule-based SQL scoring with machine
learning pattern discovery.

> **Core Question:** How can window functions, ranking logic, and ML-driven
> association mining be combined to extract actionable business intelligence and
> power a product recommendation system for an e-commerce platform?

---

## 🏆 Key Results

| Metric | Value |
|---|---|
| **Fact Table Rows** | 15,000 order lines |
| **Products Catalogued** | 100 across 8 categories |
| **Customers Analysed** | 500 across 5 regions |
| **Time Span** | 4 years (2022–2025) |
| **Analytical Queries** | 21 window-function questions |
| **Core KPIs** | 7 with Plotly visualizations |
| **Recommendation Coverage** | 100% of products (400 recommendations) |
| **Hybrid Scoring Factors** | 6 SQL + 3 ML features |

### Headline Findings

| Finding | Source |
|---|---|
| **~20% of products drive 80% of revenue** | Pareto Analysis (Q9) |
| **Q4 generates 40% above-average revenue** | Cumulative Revenue (Q1) + MoM (Q5) |
| **Central region outperforms by 15% margin** | Region Profitability (Q10) |
| **Premium segment produces 2x AOV** | AOV Segmentation (KPI 3) |
| **50%+ customers are repeat buyers** | Repeat Purchase Rate (KPI 5) |
| **3 products in sustained decline detected** | Consecutive Decline (Q21) |

---

## 📂 Repository Structure

```
ecommerce-analytical-sql/
│
├── 📓 Notebooks — Core Analytics
│   ├── 01_ddl_data_generation.ipynb          ← Schema DDL + Faker data generation + validation
│   ├── 02_core_kpis.ipynb                    ← 7 KPIs with Plotly dashboards
│   ├── 03a_time_based_analysis.ipynb         ← Q1–Q6: Cumulative, MTD, YTD, moving avg, MoM
│   ├── 03b_ranking_contribution.ipynb        ← Q7–Q11: RANK, Pareto, RATIO_TO_REPORT
│   ├── 03c_customer_behavior.ipynb           ← Q12–Q16: CLV, recency, NTILE, PERCENT_RANK
│   └── 03d_advanced_analytics.ipynb          ← Q17–Q21: STDDEV, seasonality, decline detection
│
├── 📓 Notebooks — Recommendation System
│   ├── 04a_sql_scoring_engine.ipynb          ← 6-factor SQL co-purchase scoring
│   ├── 04b_ml_content_engineering.ipynb      ← Apriori + Content-Based Filtering
│   ├── 04c_hybrid_recommendation.ipynb       ← 55% SQL + 45% ML fusion + top-4 ranking
│   └── 04d_model_evaluation.ipynb            ← Precision@4, Recall, Coverage, Diversity
│
├── 📊 Data
│   ├── ecommerce_project.db                  ← DuckDB database (star schema)
│   ├── sql_scores.csv                        ← SQL scoring output
│   ├── content_similarity_scores.csv         ← ML similarity scores
│   └── final_hybrid_recommendations.csv      ← Final top-4 recommendations per product
│
├── 🔧 Utilities
│   └── shared_setup.py                       ← Shared DB connection helper
│
├── 📑 Documentation
│   ├── Analytical_Reasoning_Documentation.docx  ← Full analytical reasoning (20 pages)
│   └── ERD_Star_Schema.png                      ← Star Schema ERD diagram
│
├── requirements.txt
├── LICENSE
└── README.md
```

---

## 🏗️ Star Schema Architecture

```
                          ┌──────────────┐
                          │   Dim_Date   │
                          │──────────────│
                          │ date_key (PK)│
                          │ full_date    │
                          │ day, month   │
                          │ quarter, year│
                          └──────┬───────┘
                                 │
    ┌──────────────┐    ┌────────┴────────┐    ┌───────────────┐
    │ Dim_Customer │    │                 │    │  Dim_Product  │
    │──────────────│    │                 │    │───────────────│
    │ customer_key │◄───┤                 ├───►│ product_key   │
    │ customer_id  │    │                 │    │ product_name  │
    │ gender, city │    │ Fact_Order_Line │    │ brand         │
    │ region       │    │─────────────────│    │ subcategory   │
    │ segment      │    │ order_line_id   │    │ stock_quantity│
    └──────────────┘    │ order_id        │    └───────────────┘
                        │ quantity        │
    ┌──────────────┐    │ gross_amount    │    ┌───────────────┐
    │ Dim_Category │    │ discount_amount │    │  Dim_Payment  │
    │──────────────│    │ net_amount      │    │───────────────│
    │ category_key │◄───┤ cost_amount     ├───►│ payment_key   │
    │ category_name│    │ profit_amount   │    │ payment_method│
    │ parent_cat   │    │                 │    └───────────────┘
    │ seasonal_flag│    │ 6 Foreign Keys  │
    └──────────────┘    │                 │    ┌───────────────┐
                        │                 ├───►│ Dim_Shipping  │
                        │                 │    │───────────────│
                        └─────────────────┘    │ shipping_key  │
                                               │ shipping_type │
                           15,000 rows         │ delivery_days │
                           1 Fact + 6 Dims     └───────────────┘
```

---

## 🔬 Methodology

### 1. 🗄️ Data Warehouse Design
- **Star Schema** with 1 fact table (order-line grain) and 6 dimension tables
- **DuckDB** as the analytical SQL engine — full window function support
- **15,000 fact rows** generated via Faker with `seed=42` for reproducibility
- **7 intentional patterns** engineered into the data for analytical discovery

### 2. 📊 Core KPIs (7 Metrics)

| KPI | SQL Technique | Visualization |
|---|---|---|
| Total Revenue | `SUM(net_amount)` by month | Line chart + 3-month MA |
| Gross Profit | `SUM(profit_amount)` trend | Dual-axis line chart |
| Average Order Value | `SUM / COUNT(DISTINCT order_id)` | Segment comparison |
| Customer Lifetime Value | `SUM` per customer, all-time | Top-20 bar + histogram |
| Repeat Purchase Rate | Customers with >1 order / total | Stacked area chart |
| Profit Margin | `SUM(profit) / SUM(net)` by category | Horizontal bar chart |
| Revenue Growth Rate | `LAG()` month-over-month | Green/red bar chart |

### 3. 📈 Analytical SQL Questions (21 Queries)

#### Section A — Time-Based Performance (Q1–Q6)
| # | Question | Key Window Function |
|---|---|---|
| Q1 | Cumulative revenue over time | `SUM() OVER (ROWS UNBOUNDED PRECEDING)` |
| Q2 | Month-to-Date performance | `SUM() OVER (PARTITION BY year, month)` |
| Q3 | Year-to-Date profit | `SUM() OVER (PARTITION BY year)` |
| Q4 | 3-month moving average | `AVG() OVER (ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)` |
| Q5 | Month-over-month comparison | `LAG()` with percentage change |
| Q6 | Revenue acceleration / deceleration | Double `LAG()` (second derivative) |

#### Section B — Ranking & Contribution (Q7–Q11)
| # | Question | Key Window Function |
|---|---|---|
| Q7 | Product ranking by category | `RANK() OVER (PARTITION BY category)` |
| Q8 | Product contribution to category | `SUM() OVER (PARTITION BY category)` ratio |
| Q9 | Pareto analysis (80/20 rule) | Cumulative `SUM()` percentage |
| Q10 | Region profitability ranking | `DENSE_RANK()` across multiple metrics |
| Q11 | Brand ranking within category | `DENSE_RANK() OVER (PARTITION BY category)` |

#### Section C — Customer Behavior (Q12–Q16)
| # | Question | Key Window Function |
|---|---|---|
| Q12 | Cumulative customer spending | `SUM() OVER (PARTITION BY customer)` |
| Q13 | Inter-purchase time analysis | `LAG(full_date)` with `DATE_DIFF()` |
| Q14 | Customer recency ranking | `DENSE_RANK()` on `MAX(full_date)` |
| Q15 | Spending tiers (quartiles) | `NTILE(4)` → Bronze/Silver/Gold/Platinum |
| Q16 | Top percentile high-value customers | `PERCENT_RANK()` filtered to top 10% |

#### Section D — Advanced Analytics (Q17–Q21)
| # | Question | Key Technique |
|---|---|---|
| Q17 | Revenue volatility per product | `STDDEV_SAMP()` + Coefficient of Variation |
| Q18 | Trending categories | Recent 3-month avg vs historical avg |
| Q19 | Seasonality (YoY same-month) | `LAG() OVER (PARTITION BY category, month)` |
| Q20 | Profit consistency across time | Monthly margin `STDDEV` + swing range |
| Q21 | Consecutive decline detection | Running group technique with 5-CTE pipeline |

### 4. 🤖 Recommendation System — Hybrid SQL + ML

```
┌─────────────────────────────────────────────────────────────────┐
│                    RECOMMENDATION PIPELINE                       │
│                                                                  │
│   ┌──────────────┐    ┌───────────────┐    ┌────────────────┐   │
│   │  Stage 1:    │    │  Stage 2:     │    │  Stage 3:      │   │
│   │  SQL Scoring │───►│  ML Scoring   │───►│  Hybrid Fusion │   │
│   │  Engine      │    │  Engine       │    │  & Ranking     │   │
│   └──────────────┘    └───────────────┘    └────────────────┘   │
│                                                                  │
│   6 Factors:           3 Components:        Final Output:        │
│   • Co-purchase freq   • Apriori rules     • 55% SQL + 45% ML   │
│   • Recency weight     • Content similarity • Top 4 per product  │
│   • Category match     • Lift normalized    • 400 recommendations│
│   • Profitability                                                │
│   • Popularity                                                   │
│   • Lift score                                                   │
└─────────────────────────────────────────────────────────────────┘
```

#### SQL Scoring Factors (Stage 1)

| Factor | Weight | Description |
|---|---|---|
| Co-purchase Frequency | 25% | How often products are bought together |
| Recency | 20% | Recent co-purchases weighted 2x |
| Category Match | 15% | Same category = 1.0, same parent = 0.5 |
| Profitability | 15% | Profit margin of recommended product |
| Popularity | 10% | Total units sold |
| Lift Score | 15% | Statistical association strength |

#### ML Enhancement (Stage 2)

| Component | Weight | Method |
|---|---|---|
| Association Rules | 35% | Apriori (mlxtend) — confidence metric |
| Lift Normalized | 30% | Apriori — lift above random chance |
| Content Similarity | 35% | Cosine similarity on product features |

#### Evaluation Metrics (Stage 4)

| Metric | What It Measures |
|---|---|
| Precision@4 | Of top-4 recs, how many were actually purchased? |
| Recall | Of all test purchases, how many appeared in recs? |
| Coverage | % of catalog appearing in at least one rec list |
| Diversity | Avg unique categories in each product's top-4 |

Evaluation uses an **80/20 temporal train/test split** — recommendations built on historical orders, validated against future purchases.

---

## 🛠️ Tech Stack

```
Python 3.10+
├── duckdb            ← Analytical SQL engine (full window function support)
├── faker             ← Synthetic data generation
├── pandas / numpy    ← Data manipulation
├── plotly            ← Interactive KPI dashboards
├── scikit-learn      ← Content-based filtering (cosine similarity, preprocessing)
├── mlxtend           ← Association rule mining (Apriori algorithm)
├── matplotlib        ← Static visualizations
├── seaborn           ← Statistical plots (heatmaps, distributions)
└── jupyter           ← Interactive notebooks
```

---

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/alyayman2020/ecommerce-analytical-sql.git
cd ecommerce-analytical-sql

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the data warehouse setup (creates DB + loads 15K rows)
jupyter notebook 01_ddl_data_generation.ipynb

# 4. Explore KPIs and analytics
jupyter notebook 02_core_kpis.ipynb

# 5. Run the recommendation system pipeline
jupyter notebook 04a_sql_scoring_engine.ipynb
jupyter notebook 04b_ml_content_engineering.ipynb
jupyter notebook 04c_hybrid_recommendation.ipynb
jupyter notebook 04d_model_evaluation.ipynb
```

---

## 📋 Requirements

```
duckdb>=0.9.0
faker>=20.0.0
pandas>=2.0.0
numpy>=1.24.0
plotly>=5.15.0
scikit-learn>=1.3.0
mlxtend>=0.23.0
matplotlib>=3.7.0
seaborn>=0.12.0
jupyter>=1.0.0
kaleido>=0.2.1
```

---

## 💡 Key Design Decisions

| Decision | Rationale |
|---|---|
| **Star Schema over normalized** | Window functions require flat, denormalized fact rows — star schema provides this naturally |
| **Order-line grain (not order)** | Preserves product-level detail for per-item ranking, cross-product association, and profitability |
| **DuckDB over SQLite** | Full support for NTILE, PERCENT_RANK, RANGE intervals, NTH_VALUE |
| **Explicit frame clauses** | Prevents implicit RANGE default from producing unexpected results with duplicate sort keys |
| **CTE-only style** | No nested subqueries deeper than 1 level — every transformation is independently testable |
| **Hybrid recommendation** | SQL captures business logic (profitability, relevance); ML discovers hidden co-purchase patterns |
| **Temporal train/test split** | Mirrors real deployment — prevents data leakage from future-to-past |
| **Intentional data patterns** | 7 engineered patterns ensure analytics discover verifiable insights, not random noise |

---

## 📑 Documentation

The project includes a comprehensive **20-page analytical reasoning document** covering:

- Executive Summary with key findings
- Data warehouse architecture rationale
- Window function taxonomy and frame clause strategy
- Technique + reasoning for all 21 analytical queries
- Recommendation system 3-stage architecture
- 7 strategic business recommendations with evidence, action, and expected impact
- Limitations and 5 future extensions

See [`Documentation/Analytical_Reasoning_Documentation.docx`](Documentation/Analytical_Reasoning_Documentation.docx)

---

## 📚 Academic Context

| | |
|---|---|
| **Institution** | Information Technology Institute (ITI) |
| **Program** | Data Science Track — 2025/2026 |
| **Module** | Analytical SQL |
| **Schema** | Star Schema (1 Fact + 6 Dimensions) |
| **Engine** | DuckDB |
| **Data** | Synthetic (Faker, seed=42, 15K rows) |

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

## 👥 Team

<table>
  <tr>
    <td align="center"><b>Aly Ayman Ibrahim</b></td>
    <td align="center"><b>Abdelrahman Ashraf Omar</b></td>
    <td align="center"><b>Mohamed Magdy</b></td>
  </tr>
  <tr>
    <td align="center">
      <a href="https://linkedin.com/in/alyayman"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white" /></a>
      <a href="https://github.com/alyayman2020"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white" /></a>
      <a href="https://www.kaggle.com/alyaymanai"><img src="https://img.shields.io/badge/Kaggle-20BEFF?style=flat-square&logo=kaggle&logoColor=white" /></a>
    </td>
    <td align="center">
      <a href="https://github.com/abdelrahmanashrafomar-bit"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white" /></a>
    </td>
    <td align="center">
      <a href="https://github.com/Mohamedmagdy21"><img src="https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white" /></a>
    </td>
  </tr>
</table>

**ITI Data Science Track — Analytical SQL Module — 2026**
