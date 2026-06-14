# 🛍️ Retail & Marketing Analytics
## Customer Segmentation, RFM Analysis & Growth Strategy

An end-to-end retail analytics project analyzing 10,000 orders from 1,986 customers across 4 product categories. Built a complete analytics pipeline covering data cleaning, EDA, RFM segmentation, K-Means clustering, cohort analysis, CLV calculation, and KPI reporting.

---

## 💡 Key Results

| Metric | Result |
|--------|--------|
| 💰 Total Revenue | **$1,078,670** |
| 📦 Total Orders | **10,000** |
| 👥 Total Customers | **1,986** |
| 🔁 Repeat Customer Rate | **96.27%** |
| 📈 Average CLV | **$7,521** |
| 🏆 CLV to CAC Ratio | **150.43x** |
| ⏱️ CAC Payback Period | **4.4 months** |
| 📉 Churn Rate | **10.88%** |
| 🛒 Average Order Value | **$107.87** |
| 💹 Profit Margin | **18.38%** |

---

## 🎯 Business Objectives

1. **Customer Segmentation** — Identify distinct customer groups using RFM analysis and K-Means clustering
2. **Sales Analysis** — Analyze revenue trends, seasonality, and category performance
3. **CLV Optimization** — Calculate customer lifetime value and improve marketing efficiency
4. **KPI Framework** — Build a comprehensive metrics dashboard for business monitoring
5. **Retention Strategy** — Identify at-risk customers and recommend targeted interventions

---

## 📁 Project Structure

```
retail-marketing-analytics/
│
├── data/
│   ├── raw/
│   │   └── retail_sales_data.csv          # Original dataset (10,000 orders)
│   └── processed/
│       ├── cleaned_retail_sales.csv        # Preprocessed dataset
│       ├── customer_segments.csv           # K-Means segment assignments
│       ├── rfm_analysis.csv                # RFM scores per customer
│       ├── customer_clv.csv                # CLV calculations
│       └── monthly_kpis.csv                # Monthly KPI tracking
│
├── outputs/
│   ├── figures/                            # 27 visualizations (PNG + interactive HTML)
│   │   ├── 17_rfm_segments.html
│   │   ├── 19_customer_segments_pca.html
│   │   ├── 20_customer_segments_3d.html
│   │   ├── 23_cohort_retention.png
│   │   ├── 24_clv_distribution.html
│   │   └── ... (27 total)
│   └── reports/
│       ├── executive_summary.txt           # Full executive report
│       ├── kpi_summary.csv                 # 25 KPIs tracked
│       ├── category_kpis.csv               # Performance by category
│       └── regional_kpis.csv               # Performance by region
│
├── docs/
│   └── data_dictionary.csv                 # Field definitions
│
├── Capstone2_Retail_and_Marketing_Analytics_Project.ipynb
├── retail_marketing_project.md
└── README.md
```

---

## 🔬 Analytics Pipeline

### Phase 1 — Data Acquisition & Cleaning
- Loaded 10,000 retail transactions across 416-day analysis period (Jan 2022 – Feb 2023)
- Treated missing values, detected and handled outliers
- Engineered date/time features, category encodings, and customer-level aggregations
- Generated `cleaned_retail_sales.csv` for downstream analysis

### Phase 2 — Exploratory Data Analysis
- Univariate and bivariate analysis across numerical and categorical features
- Identified Electronics as top revenue category at 30.4% share
- Correlation matrix across 499 SKUs and 4 product categories
- Monthly sales trend analysis with seasonal pattern detection

### Phase 3 — RFM Segmentation & K-Means Clustering
- Computed Recency, Frequency, Monetary scores for all 1,986 customers
- Applied K-Means clustering → **2 distinct customer segments identified:**

| Segment | Customers | Revenue Share | Avg Frequency | Avg Recency |
|---------|-----------|--------------|---------------|-------------|
| VIP Customers | 924 (46.5%) | **$713,664 (66.2%)** | 6.89 orders | 45.8 days |
| At Risk | 1,062 (53.5%) | $365,007 (33.8%) | 3.42 orders | 112.8 days |

- 3D PCA visualization of customer segments (`20_customer_segments_3d.html`)

### Phase 4 — Cohort & Retention Analysis
- Built cohort retention matrix tracking customer behavior over 14 months
- Customer retention rate: **89.12%** | Churn rate: **10.88%**
- Only 74 customers (3.7%) made a single purchase — strong engagement signal
- Average days since last purchase: **81.6 days**

### Phase 5 — Customer Lifetime Value
- Calculated CLV for all 1,986 customers
- Average CLV: **$7,521** | CAC: **$50** | CLV:CAC ratio: **150.43x**
- CAC payback period: **4.4 months**
- Profit per customer: **$99.84**

### Phase 6 — KPI Framework & Reporting
- Designed 25+ KPI tracking metrics across financial, customer, and operational dimensions
- Built category performance treemap and regional KPI breakdown
- Generated executive summary, KPI CSV, and dashboard-ready data files

---

## 📊 Revenue by Category

| Category | Revenue | Share |
|----------|---------|-------|
| Electronics | $328,423 | 30.4% |
| Office Supplies | $321,281 | 29.8% |
| Furniture | $214,958 | 19.9% |
| Clothing | $214,009 | 19.8% |

---

## 📈 Key Findings

**Strengths**
- CLV:CAC ratio of **150.43x** — exceptionally healthy unit economics (benchmark: >3x)
- **96.3%** repeat purchase rate signals strong product-market fit
- VIP segment (46.5% of customers) drives **66.2% of total revenue**
- Average daily revenue: **$2,593** across 416 analysis days

**Areas for Improvement**
- **1,062 At Risk customers** represent $365,007 in vulnerable revenue
- 10.88% churn rate needs active retention program
- 74 one-time buyers present a quick win for re-engagement campaigns

---

## 🎯 Strategic Recommendations

**Immediate (0–30 days)**
1. Launch loyalty program targeting the 924 VIP customers to protect $713K revenue
2. Deploy win-back campaign for 216 churned customers
3. Set up automated churn alerts for customers inactive >90 days

**Short-term (2–3 months)**
1. Personalized email campaigns by RFM segment
2. Dynamic pricing strategy for Electronics (highest revenue category)
3. Referral program leveraging the high repeat purchase rate

**Long-term (6–12 months)**
1. Build predictive churn model (target 20–25% churn reduction)
2. AI-powered product recommendation engine
3. Expected impact: 15–20% revenue increase, 25–30% retention improvement

---

## 💻 Code Highlights

### RFM Analysis
```python
import pandas as pd
from datetime import datetime

reference_date = df['order_date'].max()

rfm = df.groupby('customer_id').agg({
    'order_date': lambda x: (reference_date - x.max()).days,  # Recency
    'order_id': 'count',                                        # Frequency
    'revenue': 'sum'                                            # Monetary
})
rfm.columns = ['recency', 'frequency', 'monetary']
# Result: 1,986 customers scored and segmented
```

### K-Means Customer Segmentation
```python
from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
rfm_scaled = scaler.fit_transform(rfm[['recency', 'frequency', 'monetary']])

kmeans = KMeans(n_clusters=2, random_state=42)
rfm['segment'] = kmeans.fit_predict(rfm_scaled)
# Result: VIP (924) vs At Risk (1,062) customers
```

### CLV Calculation
```python
# Average Purchase Value × Purchase Frequency × Customer Lifetime
avg_order_value = 107.87
avg_purchase_frequency = 5.04
avg_customer_lifetime = 13.84  # months

clv = avg_order_value * avg_purchase_frequency * avg_customer_lifetime
# Result: Average CLV = $7,521 | CLV:CAC = 150.43x
```

---

## 🛠️ Installation & Setup

```bash
# Clone the repository
git clone https://github.com/Ruturaj2601/Retail-Marketing-Analytics.git
cd Retail-Marketing-Analytics

# Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn plotly scipy

# Run the analysis
jupyter notebook Capstone2_Retail_and_Marketing_Analytics_Project.ipynb
```

---

## 📦 Dependencies

```
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.4.0
seaborn>=0.11.0
scikit-learn>=0.24.0
plotly>=5.0.0
scipy>=1.7.0
```

---

## 🚀 Future Enhancements

- [ ] Power BI / Tableau interactive dashboard
- [ ] Predictive churn model (Logistic Regression + Random Forest)
- [ ] AI-powered product recommendation engine
- [ ] Real-time KPI monitoring pipeline
- [ ] A/B testing framework for marketing campaigns
- [ ] Geographic expansion analysis

---

## 📚 Dataset

- **Source:** Kaggle Retail Sales Dataset
- **Size:** 10,000 transactions | 1,986 unique customers | 499 SKUs
- **Period:** January 2022 – February 2023 (416 days)
- **Categories:** Electronics, Office Supplies, Furniture, Clothing

---

*Built with Python | Pandas | Scikit-learn | Plotly | Matplotlib | Seaborn*
