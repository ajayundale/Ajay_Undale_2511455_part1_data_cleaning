# Part 1: Business Data Cleaning, Validation & Excel Reporting

## Problem Summary
The retail company exported order-level sales data from multiple systems. The raw dataset contained issues such as inconsistent text formatting, mixed date formats, duplicate records, missing values, invalid discounts, and order status mismatches.  
The goal was to clean, validate, and prepare the dataset for business analysis.

## Dataset Description
- **Raw file:** `data/raw_orders.xlsx` (unchanged)
- **Cleaned file:** `data/cleaned_orders.xlsx` (analysis-ready)
- ~100+ order records across multiple regions, categories, and customer segments.

## Tools Used
- Microsoft Excel (TRIM, SUBSTITUTE, Flash Fill, PivotTables)
- Excel formulas for calculated columns
- Manual review and business rule validation

## Cleaning Steps Performed
- Standardized text fields (customer names, categories, ship modes, statuses).
- Converted all dates to consistent format (DD-MMM-YYYY).
- Added `shipping_delay_days` column.
- Identified and flagged duplicates.
- Applied business rules for missing/invalid values.
- Created calculated columns (sales, profit, margin, month, year, quality flag).

## Business Rules Applied
- Missing region/ship_mode → filled as "Unknown" and flagged.
- Missing discount → treated as 0 if other fields valid.
- Negative/above-range discounts → flagged invalid.
- Cancelled/failed orders → excluded from completed sales.
- Refunded orders → summarized separately.
- Ship date before order date → flagged invalid.

## Data Quality Issues Found
- Mixed date formats (e.g., `07/27/2024`, `2024-07-27`).
- Negative discounts (e.g., `ORD-2024-10020`).
- Discounts above 70% (e.g., `ORD-2024-10118`).
- Orders with cancelled/failed/refunded statuses.
- Duplicate order IDs with conflicting details.

## Pivot Report Summaries
- **Sales & Profit by Region:** South region highest sales, West region highest profit margin.
- **Category/Sub-category:** Furniture contributed most revenue, Office Supplies had highest order count.
- **Ship Mode Analysis:** Standard Class most common, Same Day least used.
- **Segment Analysis:** Corporate segment had highest profit margin.
- **Refunded/Cancelled Orders:** Concentrated in South and East regions.
- **Monthly Trend:** Seasonal peaks in July and December.

## Key Business Insights
- Profitability varies significantly by region and segment.
- High refund/cancellation rates in South region indicate possible logistics/payment issues.
- Discount misuse (negative/above-range) needs stricter system validation.
- Same Day shipping is rare, suggesting limited adoption.

## Assumptions & Limitations
- Missing discounts treated as 0 may understate true values.
- Manual cleaning may not catch all anomalies.
- Business rules applied uniformly; edge cases may exist.

## Screenshots Included
- `screenshots/raw_data_preview.png`
- `screenshots/cleaned_data_preview.png`
- `screenshots/pivot_summary_1.png`
- `screenshots/pivot_summary_2.png`
