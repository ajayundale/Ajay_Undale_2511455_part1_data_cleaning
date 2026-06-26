# Data Cleaning Log

## Issues Found
- Inconsistent text formatting (e.g., "STANDARD CLASS" vs "Standard Class").
- Mixed date formats across records.
- Negative discounts (e.g., -0.19, -0.23).
- Discounts above 70% (invalid).
- Ship dates earlier than order dates.
- Duplicate order IDs with conflicting details.
- Cancelled, failed, refunded orders present.

## Cleaning Actions Performed
- Applied TRIM, PROPER, SUBSTITUTE to text fields.
	- TRIM function applied to ~customer_name~, ~segment~, 
		- Sample Formula used - =TRIM(E2)
	- IF function was used to identify blank regions and populated them with "Unknown". Also converted all regions to standard case.
		- Sample Forumla used - =IF(TRIM(I2)="","Unknown",PROPER(TRIM(I2)))
- Calculated cells sometimes cause issues in data analysis. Hence all the corrected columns were copy pasted so that only the values remain in the cell.
- Standardized fields `order_date` and `ship_date` columns to `yyyy/mm/dd` format. If any date is not fitting the format, it is kept blank.
- Added `shipping_delay_days` column. Shipping delay days are calculated only if the `order_date` and `ship_date`, both are not blank after standardizing date formats.
- Flagged invalid discounts, shipping records, order dates, ship dates, missing regions, 
- Flagged exact duplicates and conflicting duplicate order ids.
- Filled missing region/ship_mode with "Unknown".

## Business Rules Applied
- Missing region → "Unknown" + flagged.
- Missing ship_mode → "Unknown" + flagged.
- Missing discount → treated as 0 if other fields valid.
- Negative/above-range discounts → flagged invalid.
- Cancelled/failed orders → excluded from completed sales.
- Refunded orders → summarized separately.
- Ship date < order date → flagged invalid.

## Assumptions Made
- Discount percentage recalculated based on sales value given.
- Profit margin calculated as profit ÷ sales.
- Cancelled/failed orders assumed to have no financial impact.

## Records Removed
- Exact duplicate rows flagged.
- Conflicting duplicates flagged, not deleted.

## Records Flagged
- Category correction
- Duplicate order id
- Duplicate Record
- Invalid Dates
- Invalid Discount
- Invalid Discount, Duplicate order id
- Invalid Discount, Invalid Order Date
- Invalid Discount, Invalid Ship Date
- Invalid Discount, Ship date earlier than order date
- Invalid Discount, Ship date earlier than order date, Duplicate order id
- Invalid Order Date
- Invalid Ship Date
- Invalid Ship Date, Duplicate order id
- Invalid Ship Date, Duplicate Record
- Invalid Ship Mode
- Invalid Ship Mode, Duplicate order id
- Invalid Ship Mode, Duplicate Record
- Invalid Ship Mode, Invalid Dates
- Invalid Ship Mode, Invalid Order Date
- Invalid Ship Mode, Invalid Ship Date
- Missing Region
- Missing Region, Invalid Discount, Invalid Dates
- Missing Region, Invalid Discount, Invalid Dates, Duplicate record
- Missing Region, Invalid Order Date
- Missing Region, Invalid Ship Date
- Missing Region, Invalid Ship Mode
- Ship date earlier than order date

## Limitations
- Manual cleaning may miss rare anomalies.
- Business rules simplified for assignment context.
- Further automation (Power Query, VBA) could improve scalability.
