# E-Commerce Sales Dashboard
### Amazon India Fashion Sales Analysis | Mar–Jun 2022

![Dashboard Preview](dashboard_overview.png)

---

## Project Overview

This project analyzes **128,943 orders** from an Amazon India fashion e-commerce store 
to uncover insights across financial performance, customer behavior, logistics, 
product management, and customer satisfaction.

The analysis follows the full data pipeline:
**Raw Data → Python EDA → Data Cleaning → Power BI Dashboard**

---

## Business Problems Solved

| Area | Question Answered |
|------|------------------|
| Financial | Which months and categories drive the most revenue? |
| Customer | Which states have the highest order volume? |
| Logistics | How does Amazon vs Merchant fulfillment compare? |
| Product | Which categories and sizes are in highest demand? |
| Satisfaction | What is the cancellation and return rate? |

---

## Dataset

| Column | Description |
|--------|-------------|
| Order ID | Unique order identifier |
| Date | Order date (Mar–Jun 2022) |
| Status | Order status (Shipped, Cancelled, Delivered etc.) |
| Fulfilment | Amazon or Merchant fulfilled |
| Category | Product category (Kurta, Set, Western Dress etc.) |
| Amount | Transaction amount in INR |
| ship-state | Delivery state |
| B2B | Business-to-business order flag |

**Source:** Amazon India Sales Dataset · 128,949 rows · 23 columns

---

## Data Cleaning Approach
```python
# Step 1 — Set Cancelled orders → Amount = 0
df.loc[df["Status"] == "Cancelled", "Amount"] = 0

# Step 2 — Compute median from valid orders only (non-zero, non-null)
valid = df[(df["Amount"] > 0) & (df["Amount"].notnull())]
median_amount = valid["Amount"].median()  # ₹625

# Step 3 — Fill remaining null values with median
df["Amount"].fillna(median_amount, inplace=True)
```

**Key cleaning decisions:**
- 6 duplicate rows removed
- 7,563 cancelled orders with null Amount correctly set to 0
- Only 231 genuine null Amount rows filled with median ₹625
- Median computed after zeroing cancelled rows to avoid bias

---

## Key Findings

### Financial Performance
- **Total Revenue: ₹7.18 Cr** across 4 months
- **April** was the peak month — ₹2.63 Cr (highest orders: 49,056)
- **Set** and **Kurta** categories contribute ~76% of total revenue
- Average Order Value: ₹556.76

### Customer Insights
- **Maharashtra** is the #1 state by both orders and revenue
- **Cancellation rate: 14.22%** — April had highest cancellations (7,137)
- B2C dominates at 99.3% of revenue; B2B has higher AOV (₹642 vs ₹556)

### Logistics & Fulfillment
- **Amazon fulfills 69.5%** of orders — higher revenue per order
- **68.7% of customers** prefer Expedited shipping over Standard

### Product & Inventory
- **M and L sizes** are the highest demand — stock these most
- Top problematic SKU: **JNE3797** (most cancellations + returns)

### Customer Satisfaction
- Cancellation rate: **14.22%**
- Return rate: **1.63%**
- Successful delivery rate: **84.15%**

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Python (Pandas, Matplotlib, Seaborn) | EDA and data cleaning |
| Jupyter Notebook | Analysis documentation |
| Power BI Desktop | Interactive dashboard |
| Power BI Service | Publishing and sharing |
| GitHub | Version control and portfolio |

---

## Repository Structure

ecommerce-sales-dashboard/

├── README.md
├── sales_dataset.xlsx          # Raw dataset
├── Amazon_EDA_Final.ipynb      # Python EDA notebook
├── ecommerce_dashboard.pbix    # Power BI dashboard file
└── dashboard_overview.png



## Recommendations

1. **Investigate April cancellations** — root cause analysis needed
2. **Audit SKU JNE3797** — highest issue count across all statuses  
3. **Stock M and L sizes more** — top demand across all categories
4. **Target Maharashtra and Karnataka** — highest revenue states
5. **Grow B2B segment** — lower volume but higher order value
6. **Run Sunday promotions** — highest revenue day of the week

---

## 👤 Author

**Tharun Kumar Srinivasan**  
AI & Data Science Enthusiast
[LinkedIn](https://www.linkedin.com/in/tharunkumarsrini/) · [GitHub](https://github.com/Tharun-Design)
