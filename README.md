# 📊 E-Commerce Customer Analytics & Segmentation

A complete, end-to-end data science project on the **UK Online Retail dataset** — covering data
cleaning, exploratory data analysis, RFM feature engineering, unsupervised customer segmentation,
a supervised classifier, market basket analysis, and a deployed interactive dashboard.

![Python](https://img.shields.io/badge/Python-3.11-blue)
![Streamlit](https://img.shields.io/badge/Streamlit-App-red)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange)
![License](https://img.shields.io/badge/License-MIT-green)


**[🔗 Live Dashboard](https://customer-segmentation-rfm-kmeans-usmanhaider.streamlit.app/)** &nbsp;·&nbsp; **Author:** Usman Haider

---

## 📌 Overview

This project analyzes ~540,000 transactions from a UK-based online retailer to answer two core
business questions:

1. **Who are our customers, and how should we treat them differently?**
   → Solved with RFM (Recency, Frequency, Monetary) analysis and K-Means clustering.
2. **What products should we recommend or bundle together?**
   → Solved with market basket analysis (Apriori algorithm / association rules).

The result is a set of actionable customer segments (VIP, Loyal, Regular, At-Risk) and product
association rules, both surfaced through a live Streamlit dashboard with a built-in segment
prediction tool for new customers.

---

## 🗂️ Project Structure

```
E-Commerce Customer Analytics & Segmentation/
├── app/
│   └── app.py                      # Streamlit dashboard
├── data/
│   ├── online-retail.xlsx          # Raw dataset
│   ├── rfm_with_clusters.xlsx      # RFM table with cluster labels
│   └── association_rules.xlsx      # Market basket association rules
├── Models/
│   ├── kmeans_model.pkl            # Trained K-Means clustering model
│   ├── scaler.pkl                  # StandardScaler used for RFM features
│   └── random_forest_model.pkl     # Trained classifier (predicts segment)
├── notebook/
│   └── analysis.ipynb              # Full analysis: cleaning → EDA → modeling
├── Pictures/                       # Exported charts used in the dashboard/report
├── requirements.txt
├── LICENSE
└── README.md
```

---

## 🔍 Methodology

### 1. Data Cleaning
- Removed duplicate transactions, cancelled/adjustment orders, non-product stock codes
  (postage, bank charges, manual entries), invalid prices/quantities, and a single extreme
  quantity outlier.
- Final clean dataset: **~522,700 transactions**, **4,334 unique customers**.

### 2. Exploratory Data Analysis
- Revenue, order, and customer summaries.
- Top products by quantity vs. revenue.
- Country-level and monthly sales trends.
- Correlation analysis between `Quantity`, `UnitPrice`, and `TotalPrice`.

### 3. RFM Feature Engineering
For each customer:
- **Recency** — days since last purchase.
- **Frequency** — number of distinct orders.
- **Monetary** — total amount spent.

### 4. Customer Segmentation (Unsupervised Learning)
- Features scaled with `StandardScaler`.
- **K-Means clustering** (k=4, selected via the Elbow Method and validated with a
  **Silhouette Score of 0.62**).
- Segments labeled by business meaning:

| Segment | Recency | Frequency | Monetary | Customers |
|---|---|---|---|---|
| 🏆 VIP / Champions | ~8 days | ~89 orders | ~£122,551 | 12 |
| ⭐ Loyal Customers | ~15 days | ~22 orders | ~£12,285 | 211 |
| 👤 Regular Customers | ~44 days | ~4 orders | ~£1,316 | 3,044 |
| ⚠️ At Risk / Lost | ~249 days | ~2 orders | ~£474 | 1,067 |

### 5. Segment Prediction (Supervised Learning)
- A **Random Forest Classifier** was trained on the RFM features to predict a customer's
  segment, enabling real-time classification of new/unseen customers without re-running
  clustering.
- Validated with an 80/20 train-test split and 5-fold cross-validation
  (mean accuracy ≈ 99.6%, std ≈ 0.001), confirming the result is stable rather than a
  lucky split — though the very high accuracy reflects that the target was derived
  directly from the input features, not evidence of a difficult real-world pattern learned.

### 6. Market Basket Analysis
- Apriori algorithm applied to UK transactions (top 100 products) to mine frequent itemsets
  and association rules (support, confidence, lift).
- Strongest pattern: the Pink / Green / Roses Regency Teacup & Saucer set, purchased
  together far more often than chance (lift ≈ 12–14), suggesting a bundling opportunity.

### 7. Deployment
- Trained models serialized with `joblib`.
- An interactive **Streamlit dashboard** exposes segment KPIs, cluster visualizations,
  market basket results, and a live "predict a new customer's segment" tool.

---

## 🛠️ Tech Stack

- **Language:** Python 3.11
- **Data Processing:** pandas, NumPy
- **Machine Learning:** scikit-learn (KMeans, RandomForestClassifier, StandardScaler)
- **Market Basket Analysis:** mlxtend (Apriori, association rules)
- **Visualization:** matplotlib, networkx
- **Dashboard:** Streamlit
- **Model Persistence:** joblib

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/<your-username>/ecommerce-customer-segmentation.git
cd ecommerce-customer-segmentation
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the analysis (optional)
Open `notebook/analysis.ipynb` to reproduce the full cleaning, EDA, and modeling pipeline.

### 4. Launch the dashboard
```bash
cd app
streamlit run app.py
```
The dashboard will open automatically at `http://localhost:8501`.

---

## 📈 Key Insights

- **84.8%** of total revenue comes from the UK, with the Netherlands and Ireland as the
  next largest markets.
- Customer value is heavily **right-skewed** — a small number of high-frequency customers
  account for a disproportionate share of revenue, which motivated the segmentation approach.
- The **At-Risk / Lost segment (1,067 customers)** represents the largest re-engagement
  opportunity, while the **VIP segment (12 customers)** contributes outsized revenue
  relative to its size.
- The optimal statistical clustering solution (k=2) was not the most useful one — a
  4-segment solution was chosen because it maps to distinct, actionable marketing strategies.

---

## 📄 Dataset

[Online Retail Dataset (UCI Machine Learning Repository)](https://archive.ics.uci.edu/dataset/352/online+retail) —
transactions from a UK-based online gift retailer, December 2010 to December 2011.

---

## 📬 Contact

**Usman Haider**
Feel free to connect for feedback, questions, or collaboration opportunities.

---

## 📃 License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.