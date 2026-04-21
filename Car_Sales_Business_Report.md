# 🚗 Car Sales Data — Business Analysis Report

> **Analyst:** Data Analytics Team  
> **Dataset:** Car_Sales_xlsx_-_car_data.csv  
> **Report Date:** April 2026  
> **Records Analyzed:** 23,906 transactions

---

## 1. Problem Statement

The automotive retail industry relies on understanding buyer behavior, regional performance, and product mix to drive revenue. This report investigates a multi-brand car dealership dataset to uncover sales patterns, identify high-performing segments, and generate actionable business recommendations. Key questions addressed:

- Which brands and body styles drive the most revenue?
- How does customer income relate to vehicle price?
- Which regions and dealerships are the top performers?
- What demographic patterns characterize the customer base?

---

## 2. Dataset Description

The dataset contains **23,906 car sales transactions** spanning 16 columns across multiple brands, dealerships, and U.S. regions.

| Attribute | Details |
|---|---|
| **Records** | 23,906 rows |
| **Columns** | 16 features |
| **Date Range** | 2022 (inferred from `Date` field) |
| **Brands Covered** | 30 unique companies (Chevrolet, Dodge, Ford, Volkswagen, Mercedes-B, Cadillac, etc.) |
| **Regions** | 7 dealer regions: Austin, Janesville, Scottsdale, Pasco, Aurora, Middletown, Greenville |
| **Price Range** | $1,200 – $85,800 |
| **Annual Income Range** | $10,080 – $11,200,000 |

**Columns include:** Car ID, Date, Customer Name, Gender, Annual Income, Dealer Name, Company, Model, Engine Type, Transmission, Color, Price, Dealer No., Body Style, Phone, Dealer Region.

---

## 3. Data Wrangling Steps

### 3.1 Handling Missing Values
- **Customer Name**: 1 missing value found — filled with `'Unknown'` to preserve the record.
- All other columns had **zero missing values**.

### 3.2 Duplicate Removal
- Checked for full-row duplicates: **0 duplicates found**. No rows were removed.

### 3.3 Data Type Corrections
- `Date` column converted from `object` → `datetime` using `pd.to_datetime()`.
- `Price ($)` and `Annual Income` confirmed as `int64` (numeric) — no conversion needed.
- `Engine` column contained a hidden non-breaking space character (`\xa0`) embedded in "Double Overhead Camshaft" — cleaned using `.str.replace('\xa0', ' ').str.strip()`.

### 3.4 Filtering & Transformations
- For the scatter plot (Income vs Price), records with `Annual Income > $5,000,000` were excluded to reduce the impact of extreme outliers on visual interpretation — these ultra-high-income buyers represent less than 1% of the dataset.
- A random sample of 2,000 records was used for scatter plot rendering performance.

### 3.5 New Columns Created
- **No new columns were strictly required** for this analysis. However, the following derived aggregations were computed during analysis:
  - Average price per brand (`Company`)
  - Average price per dealer region
  - Sales volume per body style
  - Transmission split by gender

---

## 4. Visualizations

### Figure 1 — Bar Chart: Top 10 Car Companies by Sales Volume

![Bar Chart - Top 10 Companies](fig1_bar_sales_volume.png)

**Key Finding:** Chevrolet leads with **1,819 units** sold, followed by Dodge (1,671) and Ford (1,614). These three American brands together account for over 21% of all sales. European and luxury brands like Mercedes-Benz and Volkswagen also make the top 5, reflecting a diverse buyer base.

---

### Figure 2 — Pie Chart: Sales by Body Style

![Pie Chart - Body Style](fig2_pie_body_style.png)

**Key Finding:** SUVs are the most popular body style at **26.7%**, closely followed by Hatchbacks (25.6%). Together, SUVs and Hatchbacks make up over half of all vehicles sold. Hardtops are the least popular at 12.4%.

---

### Figure 3 — Histogram: Distribution of Car Prices

![Histogram - Price Distribution](fig3_hist_price.png)

**Key Finding:** Car prices are right-skewed. The **median price is $23,000** while the **mean is $28,090**, indicating a long tail of premium-priced vehicles pulling the average up. Most sales cluster in the **$14,000–$35,000** range, suggesting the dealership network primarily serves middle-market buyers.

---

### Figure 4 — Scatter Plot: Annual Income vs Car Price (by Gender)

![Scatter Plot - Income vs Price](fig4_scatter_income_price.png)

**Key Finding:** There is a very **weak correlation (r = 0.012)** between annual income and car price. This is a surprising insight — customers across all income levels are purchasing vehicles at similar price points. This could indicate the prevalence of financing/leasing, or that the dealership's price range is narrow enough to serve all income segments.

---

### Figure 5 — Bar Chart: Average Car Price by Dealer Region

![Bar Chart - Region Price](fig5_bar_region_price.png)

**Key Finding:** **Middletown** has the highest average car price (~$29,000+), while **Greenville** has the lowest. However, the spread across regions is relatively modest (within ~$2,000), suggesting consistent national pricing with minor regional variation.

---

### Figure 6 — Grouped Bar Chart: Transmission Preference by Gender

![Grouped Bar - Transmission by Gender](fig6_grouped_transmission_gender.png)

**Key Finding:** Both male and female buyers prefer **Automatic transmission**, but the gap is more pronounced among male buyers. The near-equal split between Auto (52.6%) and Manual (47.4%) across the full dataset suggests Manual still has strong market relevance — a differentiator from many other markets where manual has nearly disappeared.

---

## 5. Key Insights

### 🏆 Brand & Model Performance
- **Chevrolet, Dodge, and Ford dominate by volume** — these three brands represent the affordable-to-mid-range sweet spot of the market.
- **Cadillac commands the highest average price at ~$40,972**, followed by Saab ($36,516) and Lexus ($34,025). These are clear luxury segments to nurture for revenue per unit.
- A long tail of 30 brands means **inventory diversification is high**, which serves varied customer needs but may complicate stock management.

### 📍 Regional Performance
- **Austin is the top-performing region** with 4,135 sales — 8.1% more than the second-largest region (Janesville at 3,821).
- All 7 regions are within ~1,000 units of each other, suggesting **relatively balanced geographic coverage** with no severely underperforming region.
- Middletown achieves the **highest average sale price**, making it a premium revenue driver despite not having the most volume.

### 👥 Customer Demographics
- **78.6% of buyers are male** — a significant gender skew that warrants attention in marketing strategy.
- Female buyers (21.4%) are a growing segment with a **lower average income ($755,973)** versus male buyers ($851,184), yet purchase at similar price points — suggesting female buyers may stretch their budgets more or use financing at higher rates.
- Customer income ranges from under $15,000 to $11.2M, reflecting an extraordinarily **diverse income bracket** being served by the same dealership network.

### 🚗 Product Preferences
- **SUVs and Hatchbacks** together account for 52.3% of sales — the dealership network should prioritize stocking these.
- **Pale White is the most popular color** (47.1%), followed by Black (32.9%) and Red (20.1%). A very limited color palette of just 3 options may be restricting customer choice.
- **Auto transmission edges out Manual (52.6% vs 47.4%)** — unlike many Western markets, manual transmission remains highly relevant here and should be maintained in inventory.

### 💰 Pricing & Revenue
- **Total revenue: $671.5 million** across 23,906 transactions.
- The right-skewed price distribution shows the bulk of transactions are in the $14,000–$35,000 range, but **premium sales ($60,000+) are meaningful revenue contributors** despite lower volume.
- Very weak income-price correlation (r = 0.012) suggests **financing plays a large role** — buyers don't shop based on income bracket alone.

---

## 6. Business Recommendations

**1. Double Down on Top Brands, Nurture Luxury**  
Maintain strong inventory of Chevrolet, Dodge, and Ford for volume. Simultaneously invest in growing Cadillac, Lexus, and Buick stock — these brands generate significantly higher revenue per unit and serve an aspirational buyer segment.

**2. Target Female Buyers with Dedicated Campaigns**  
With only 21.4% female buyers, there is a significant untapped market. Introduce female-targeted marketing, flexible financing options, and inclusive showroom experiences to grow this segment.

**3. Optimize for SUV and Hatchback Demand**  
SUVs and Hatchbacks together represent more than half of all sales. Ensure these body styles are well-stocked across all regions, with emphasis on the top-performing Austin market.

**4. Expand Color Options**  
Currently only 3 colors are available. Expanding the palette to include silver, blue, and grey — among the most popular globally — could capture preference-driven buyers currently lost to competitors.

**5. Prioritize Austin & Leverage Middletown's Premium Mix**  
Austin drives the highest volume; invest in capacity, staff, and marketing there. Middletown, while modest in volume, commands the highest average sale value — consider positioning it as a luxury/premium hub.

**6. Leverage Financing to Close Deals Across All Income Segments**  
The near-zero correlation between income and price suggests buyers across all income levels are purchasing at similar price points — likely through financing. Strengthen financing partnerships and promote low-APR offers to capitalize on this behavior.

**7. Maintain Manual Transmission Inventory**  
Unlike trends in many markets, Manual transmission accounts for 47.4% of sales here. Reducing this inventory could alienate nearly half the customer base. Monitor year-over-year trends before phasing it down.

---

## 7. Conclusion

The car sales dataset reveals a healthy, diversified dealership network with broad brand coverage, stable regional performance, and a primarily male, middle-income buyer base. The standout insights are the dominance of American brands by volume, the luxury premium commanded by Cadillac and Lexus, and the surprising gender imbalance among buyers.

The most impactful near-term opportunities are: investing in SUV/Hatchback inventory, growing the female buyer segment, expanding color options, and positioning Cadillac/Lexus as a deliberate luxury sub-strategy.

With $671.5M in total sales revenue and 30 brands across 7 regions, the operation has a strong foundation — data-driven decisions in inventory, marketing, and regional strategy can meaningfully grow both volume and margin.

---

*Report generated using Python (pandas, matplotlib) · Dataset: 23,906 records · 16 features*
