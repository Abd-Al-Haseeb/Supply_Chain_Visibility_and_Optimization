# DAX Measures — Supply Chain Visibility & Optimisation

This document records the key DAX measures used in the Power BI analysis across the project, with emphasis on Milestones 2 and 3.

> **Note:** The exact DAX stored in each `.pbix` file remains the authoritative implementation. This file provides a readable reference for the main analytical calculations.

## 1. Core Supply Chain KPIs

### Units Moved
```DAX
Units Moved =
DISTINCTCOUNT(
    'Supply_Chain_Cleaned_Dataset'[Movement Line Key]
)
```

### Total Sales
```DAX
Total Sales =
SUMX(
    VALUES('Supply_Chain_Cleaned_Dataset'[Movement Line Key]),
    CALCULATE(
        MAX('Supply_Chain_Cleaned_Dataset'[price])
    )
)
```

### Total Shipments
```DAX
Total Shipments =
DISTINCTCOUNT(
    'Supply_Chain_Cleaned_Dataset'[order_id]
)
```

### Delivered Orders
```DAX
Delivered Orders =
CALCULATE(
    DISTINCTCOUNT('Supply_Chain_Cleaned_Dataset'[order_id]),
    NOT ISBLANK(
        'Supply_Chain_Cleaned_Dataset'[order_delivered_customer_date]
    )
)
```

### On-Time Delivered Orders
```DAX
On-Time Delivered Orders =
CALCULATE(
    DISTINCTCOUNT('Supply_Chain_Cleaned_Dataset'[order_id]),
    'Supply_Chain_Cleaned_Dataset'[delivery_delay] <= 0
)
```

### On-Time Delivery %
```DAX
On-Time Delivery % =
DIVIDE(
    [On-Time Delivered Orders],
    [Delivered Orders]
)
```

### Average Delivery Time
```DAX
Average Delivery Time =
AVERAGEX(
    FILTER(
        'Supply_Chain_Cleaned_Dataset',
        NOT ISBLANK(
            'Supply_Chain_Cleaned_Dataset'[order_delivered_customer_date]
        )
    ),
    DATEDIFF(
        'Supply_Chain_Cleaned_Dataset'[order_purchase_timestamp],
        'Supply_Chain_Cleaned_Dataset'[order_delivered_customer_date],
        DAY
    )
)
```

### Average Supplier Rating
```DAX
Average Supplier Rating =
AVERAGE(
    'Supply_Chain_Cleaned_Dataset'[review_score]
)
```

## 2. Supplier Performance Scorecard

Supplier scoring uses four equally weighted dimensions: delivery reliability, customer review, freight efficiency and delivery speed. Only sellers meeting the minimum delivered-order threshold are included in the formal ranking.

### Seller Performance Score
```DAX
Seller Performance Score =
DIVIDE(
    [Seller Delivery Score]
        + [Seller Review Score]
        + [Seller Freight Score]
        + [Seller Speed Score],
    4
)
```

### Seller Performance Status
```DAX
Seller Performance Status =
SWITCH(
    TRUE(),
    [Seller Performance Score] >= 3, "Excellent",
    [Seller Performance Score] >= 2.5, "Good",
    [Seller Performance Score] >= 2, "Watchlist",
    "Needs Improvement"
)
```

The component scores are based on the eligible-seller performance distribution rather than relying only on arbitrary fixed thresholds.

## 3. Transportation Cost Analysis

### Total Transportation Cost
```DAX
Total Transportation Cost =
SUM('Supply_Chain_Cleaned_Dataset'[freight_value])
```

For duplicate-sensitive calculations, freight should be evaluated at the unique movement-line grain so repeated payment rows do not inflate totals.

### Average Freight per Movement
```DAX
Avg Freight / Movement =
DIVIDE(
    [Total Transportation Cost],
    [Units Moved]
)
```

## 4. Route & Carrier Performance

### Route
```DAX
Route =
[Seller State] & " → " & [Customer State]
```

### Freight Cost per 100 KM
```DAX
Freight Cost per 100 KM =
DIVIDE(
    [Total Freight Cost],
    [Total Route Distance KM]
) * 100
```

### Average Carrier Transit Days
```DAX
Avg Carrier Transit Days =
AVERAGEX(
    VALUES('Supply_Chain_Cleaned_Dataset'[order_id]),
    MAX('Supply_Chain_Cleaned_Dataset'[Carrier Transit Days])
)
```

### Transit Over 60 Days
```DAX
Transit > 60 Days =
CALCULATE(
    DISTINCTCOUNT('Supply_Chain_Cleaned_Dataset'[order_id]),
    'Supply_Chain_Cleaned_Dataset'[Carrier Transit Days] > 60
)
```

### Maximum Transit Days
```DAX
Max Transit Days =
MAX(
    'Supply_Chain_Cleaned_Dataset'[Carrier Transit Days]
)
```

## 5. Methodology Notes

- `Movement Line Key` is used to protect movement and financial calculations from duplicate payment rows.
- Seller performance is evaluated only after applying the minimum delivered-order threshold.
- Route distance is an approximate geographic distance calculated from seller and customer coordinates using the Haversine approach; it is not road distance.
- The dataset does not provide reliable named carrier identities. Therefore, carrier analysis represents carrier-stage transit performance rather than comparison between named carrier companies.
- The Olist dataset does not contain actual warehouse on-hand inventory. Product movement is therefore treated as an inventory/activity proxy where applicable.
