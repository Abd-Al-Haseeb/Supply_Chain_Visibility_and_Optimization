# Supply Chain Visibility and Optimization

A Power BI-based supply chain analytics project focused on turning e-commerce order, delivery, supplier, transportation, and geolocation data into practical business insights.

## Project Overview

This project was developed as a milestone-based analytics journey. The work progressed from data preprocessing and validation to Power BI dashboards, supplier and route analysis, transportation cost analysis, and advanced KPI visualization.

The analysis uses a cleaned Brazilian e-commerce dataset together with supporting Olist datasets for customer, seller, and geolocation enrichment.

## Project Objectives

- Clean and prepare the raw supply chain dataset for analysis.
- Build a reliable Power BI analytical model.
- Monitor order, inventory movement, delivery, and customer experience performance.
- Evaluate supplier performance using scorecards and performance categories.
- Analyze routes, transportation distance, carrier transit performance, and freight cost.
- Develop advanced KPIs and visualizations that support operational decision-making.
- Present findings in a clear business-oriented format.

## Milestone 1 — Data Preprocessing

The first milestone focused on preparing the raw dataset for reliable analysis.

### Key activities

- Inspected the raw dataset structure, columns, missing values, and data quality.
- Removed irrelevant fields where appropriate.
- Handled missing and inconsistent values.
- Evaluated delivery-time outliers using the IQR method.
- Created the `delivery_delay` feature.
- Filtered the dataset to a cleaned analytical dataset.
- Preserved the cleaned dataset for the later Power BI milestones.

### Main output

`Milestone_1_Data_Preprocessing/Cleaned_Dataset/Supply_Chain_Cleaned_Dataset.csv`

## Milestone 2 — Power BI Dashboards

The cleaned dataset was brought into Power BI and developed into a supply chain visibility dashboard suite.

### Dashboards

- Executive Supply Chain Overview
- Inventory Movement Intelligence
- Delivery Performance
- Region & Product Drilldown
- Trends & Variance Analysis

### Key analytical areas

- Total orders
- Units moved
- Movement value
- Delivery duration
- On-time delivery
- Inventory and movement trends
- Regional and product-level performance
- Delivery and operational variance

The Milestone 2 dashboards established the core analytical view that was later extended in Milestone 3.

## Milestone 3 — Advanced Analytics

Milestone 3 extended the Power BI model with additional Olist supporting datasets and advanced analytical views.

### Supporting Data

The following supporting datasets were used for enrichment and route/geolocation analysis:

- `olist_customers_dataset.csv`
- `olist_sellers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `Milestone3_Geolocation_ZIP_Lookup.csv`

These files support the enrichment of customer and seller ZIP information and the ZIP-to-geolocation analysis used for route distance calculations.

### Supplier Performance Scorecards

The Supplier Performance Scorecards dashboard evaluates eligible sellers and categorizes their performance into:

- Excellent Sellers
- Good Sellers
- Watchlist Sellers
- Needs Improvement

The scorecard combines delivery reliability, customer experience/review performance, freight efficiency, and delivery speed. Seller eligibility is based on sellers with at least 50 delivered orders.

Key dashboard views include:

- Eligible seller count
- Seller performance category counts
- Top performing sellers
- Sellers needing improvement
- Delivery reliability vs customer experience
- Seller-level scorecard detail
- Seller state and city filters

### Route & Carrier Performance

The Route & Carrier Performance dashboard focuses on transportation movement and route-level efficiency.

Key analytical views include:

- Unique routes
- Average approximate route distance
- Average carrier transit time
- On-time delivery percentage
- Average freight per movement
- Freight cost per 100 KM
- Long-transit movements
- Maximum transit time
- Top routes by units moved
- On-time delivery by route
- Distance vs freight cost
- Transit time by distance band
- Route performance detail

Because a dedicated carrier identifier is not available in the Olist dataset, carrier performance is evaluated using transit-stage information rather than an individual carrier identity.

### Transportation Cost Analysis

This dashboard area examines the relationship between transportation activity, freight cost, distance, and movement volume.

The analysis supports investigation of:

- Freight cost patterns
- Cost per movement
- Distance-related cost behavior
- Route-level transportation efficiency
- High-cost transportation areas

### Advanced KPI Visualization

Advanced KPI views extend the core dashboard with more detailed performance indicators and visual comparisons to support operational interpretation and decision-making.

## Important DAX Measures

The Power BI model uses DAX measures to calculate and standardize the analytical KPIs shown in the dashboards. Examples include measures for:

- Delivered Orders
- On-Time Delivery %
- Average Review Score
- Average Freight per Movement
- Average Delivery Time
- Seller Performance Score
- Unique Routes
- Average Route Distance KM
- Average Carrier Transit Days
- Total Freight Cost
- Average Freight per Movement
- Freight Cost per 100 KM
- Units Moved

The DAX measures are used to keep dashboard calculations consistent across visuals and filters.

## Key Project Findings

The completed dashboards provide several important business-level observations:

- The cleaned analytical dataset supports approximately 56K orders and around 63K units moved in the validated Power BI model.
- On-time delivery performance is approximately 93.91% in the validated dashboard analysis.
- Average delivery duration is approximately 11.52 days in the Milestone 2 analysis.
- Supplier performance varies considerably, allowing sellers to be separated into strong performers, watchlist sellers, and sellers requiring improvement.
- The supplier scorecard highlights the relationship between delivery reliability and customer review experience.
- Route analysis shows substantial differences in movement volume, distance, and transit time between origin-destination routes.
- Longer transportation distances generally provide an important area for investigating freight-cost behavior.
- The route dashboard identifies long-transit movements and distance bands that can be examined for transportation efficiency improvements.

## Tools & Technologies

- Python
- Google Colab
- Pandas
- Power BI
- DAX
- GitHub
- Git LFS

## Repository Structure

```text
Supply_Chain_Visibility_and_Optimization/
│
├── Milestone_1_Data_Preprocessing/
│   └── Cleaned_Dataset/
│       └── Supply_Chain_Cleaned_Dataset.csv
│
├── Milestone_2_PowerBI_Dashboards/
│   └── Power BI project files
│
├── Milestone_3_Advanced_Analytics/
│   └── Supporting_Data/
│       ├── olist_customers_dataset.csv
│       ├── olist_sellers_dataset.csv
│       ├── olist_geolocation_dataset.csv
│       └── Milestone3_Geolocation_ZIP_Lookup.csv
│
├── Milestone_4/
├── Documentation/
├── Presentation/
├── .gitattributes
├── LICENSE
└── README.md
```

## Team Project

This project was completed as a group internship project, with responsibilities covering data preparation, Power BI development, analytics, presentation, and documentation.

## Project Status

**Completed — Milestones 1, 2, 3, and 4.**

The repository is being organized to preserve the datasets, analytical work, dashboards, documentation, and presentation materials produced throughout the project.