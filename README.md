# E-Commerce Customer Analytics: Acquisition, Retention and Revenue Optimization

## Project overview

This project analyzes an e-commerce company's 2019 customer, transaction, coupon, marketing, tax and demographic data. The objective is to convert transactional data into practical recommendations for customer acquisition, retention, revenue growth, promotion design and pricing.

The notebook combines exploratory data analysis, customer-level metrics, cohort analysis, RFM segmentation and statistical testing. Each analysis is followed by a business interpretation or recommendation.

## Business problem

The company wants to use data-driven insights to:

- stabilize customer acquisition across the year;
- improve repeat purchases and customer retention;
- balance revenue from new and existing customers;
- optimize coupons without unnecessarily reducing margins;
- identify and nurture valuable customer segments;
- understand cohort-level retention and observed customer value;
- evaluate demographic and pricing-related differences in purchasing;
- understand the effects of delivery charges and taxes;
- prepare for seasonal, category, location and daily demand patterns.

## Analysis scope

| # | Business question | Analysis performed |
|---:|---|---|
| 1 | Which months have the highest and lowest customer acquisition? | Monthly first-purchase counts and peak/trough identification |
| 2 | Which months show stronger or weaker acquisition? | Above/below-average classification and monthly visualization |
| 3 | Which periods have the strongest and weakest retention? | Consecutive-month customer retention rates |
| 4 | What characterizes high-retention months? | Revenue, category, coupon and quantity behavior in high-retention periods |
| 5 | How does revenue from new and existing customers compare? | Month-over-month customer-type revenue comparison |
| 6 | How is coupon usage related to revenue? | Coupon/non-coupon revenue, transaction value and quantity comparison |
| 7 | Which products perform best? | Category performance is examined within high-retention-period analysis; a separate product-level ranking is not included |
| 8 | How does monthly marketing spend relate to revenue? | Dataset is loaded, but a completed standalone ROI analysis is not included |
| 9 | How effective are marketing campaigns? | A completed standalone campaign-allocation analysis is not included |
| 10 | How can customers be segmented? | RFM scoring with Premium, Gold, Silver and Standard segments |
| 11 | How much revenue does each customer segment contribute? | Segment revenue, customer count and average customer value |
| 12 | Which acquisition cohorts retain best? | Cohort retention matrix by first-purchase month |
| 13 | How does customer value differ by acquisition month? | Observed customer value by acquisition cohort |
| 14 | Do coupon users have a different average transaction value? | Independent two-sample t-test |
| 15 | Does purchasing differ by demographic or pricing group? | Group summaries and inferential tests across location and delivery-charge tiers |
| 16 | Does customer tenure affect purchase frequency? | Spearman correlation and tenure-normalized purchase frequency |
| 17 | How do delivery charges relate to order behavior? | Correlation and delivery-tier comparison |
| 18 | How do taxes and delivery charges affect spending? | Invoice-component and order-behavior analysis |
| 19 | What seasonal patterns appear by category and location? | Monthly category and location trend analysis |
| 20 | Which days perform best or worst? | Daily and weekday sales analysis |

## Analytical methodology

### Data preparation

- Standardized column names and product-category labels.
- Converted transaction dates into valid datetime values.
- Corrected the `Product_Cateogry` field name where required.
- Combined transaction, coupon and tax data using month and product category.
- Applied discounts only when `Coupon_Status` indicated that a coupon was used.
- Calculated transaction revenue as:

```text
Revenue = (Quantity × Average Price) × (1 − Effective Discount) × (1 + GST)
          + Delivery Charges
```

### Customer analytics

- Acquisition month is defined using each customer's first transaction.
- Month-to-month retention measures the proportion of customers active in one month who return in the immediately following month.
- New customers are customers purchasing in their first observed month; all later purchases are classified as existing-customer activity.
- Cohorts group customers by their first-purchase month and track activity over subsequent months.
- Customer value by cohort is the revenue observed within the available 2019 window, not an unlimited-horizon lifetime-value prediction.

### RFM segmentation

Customers receive quartile-based scores for:

- **Recency:** days since the most recent purchase;
- **Frequency:** number of unique transactions;
- **Monetary value:** total calculated revenue.

The combined RFM score maps customers to Premium, Gold, Silver and Standard segments. This supports differentiated retention, cross-selling and reactivation strategies.

### Statistical analysis

The notebook uses:

- an independent two-sample t-test for coupon versus non-coupon transaction values;
- ANOVA or related group comparisons for demographic and pricing groups;
- Spearman correlation for tenure, delivery-charge and order-behavior relationships.

A significance level of `0.05` is used when interpreting p-values. Statistical association is not treated as proof of causation.

## Business recommendations

- Maintain year-round acquisition through personalized promotions, referral incentives, remarketing and monthly KPI monitoring rather than depending only on seasonal peaks.
- Recreate high-retention conditions using successful categories, personalized recommendations, loyalty rewards and time-bound second-purchase offers.
- Balance acquisition with retention: strong new-customer revenue is valuable only when new buyers are converted into repeat customers.
- Replace broad couponing with targeted offers, category-specific promotions and minimum-spend thresholds.
- Protect Premium and Gold customers with high-touch loyalty benefits while using automated, lower-cost progression campaigns for Silver and Standard segments.
- Prioritize the first 30–60 days after acquisition with onboarding and second-purchase incentives for weak cohorts.
- Use free-shipping thresholds and targeted delivery discounts where delivery sensitivity is supported by the data.
- Prepare inventory and marketing before category/location demand peaks; use bundles, cross-selling and localized campaigns in off-peak periods.
- Support low-performing weekdays with flash sales, loyalty-point multipliers and personalized promotions.

## Repository structure

```text
ecommerce-customer-analytics/
├── Business_case.ipynb   # Complete analysis notebook
├── README.md             # Project documentation
├── requirements.txt      # Python dependencies
└── .gitignore            # Files excluded from version control
```

## Datasets

The source data is not duplicated in this repository. Download it from the provided project resources and place the files in the notebook's working directory.

- [Dataset folder](https://drive.google.com/drive/folders/1Qt1HfSoTyCKiyDy2frR-hYOT9UvfwGq7?usp=sharing)
- [Dataset description](https://docs.google.com/document/d/1u2gedRtVaCqTQNylaohI9WO6m3pA8rnc/edit?usp=drive_link)
- [Suggested analytical approach](https://docs.google.com/document/d/1CubX27YSJSpQJyuc5kBagfPa8AjhsQJFYaE0XgH0KoQ/edit?usp=sharing)

Expected input files include:

```text
Online_Sales.csv
Discount_Coupon.csv
Marketing_Spend.csv
CustomersData.xlsx
Tax_amount.xlsx
```

## How to run

### Google Colab

1. Open `Business_case.ipynb` in Google Colab.
2. Upload the five source data files when prompted.
3. Run the cells sequentially from top to bottom.

### Local Jupyter environment

```bash
git clone https://github.com/geeky5999/ecommerce-customer-analytics.git
cd ecommerce-customer-analytics
python -m venv .venv
```

Activate the environment, then install and launch:

```bash
pip install -r requirements.txt
jupyter notebook Business_case.ipynb
```

## Limitations

- The data covers one year, so observed monthly patterns should not be presented as proven multi-year seasonality.
- Later acquisition cohorts have less time to accumulate revenue and retention observations than earlier cohorts.
- Coupon, tax and delivery analyses identify associations; causal conclusions require controlled experiments or stronger causal designs.
- Questions 8 and 9 require a completed marketing-spend ROI/campaign analysis in a future notebook revision.

## Technologies used

Python, Pandas, NumPy, Matplotlib, SciPy, Jupyter Notebook and Microsoft Excel/CSV data sources.

## Author

**Shivani Agrahari**  
[GitHub](https://github.com/geeky5999)
