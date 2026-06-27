# Cleaning Log

## 1. Issues Found
- Raw dataset contained 932 rows and 21 columns.
- Exact duplicate row copies found: 40 rows; duplicate copies removed: 20.
- Rows with duplicate `order_id`: 63 across 31 unique order IDs.
- Conflicting duplicate `order_id` values: 12 unique order IDs.
- Missing `region`: 26 rows.
- Missing `ship_mode`: 22 rows.
- Missing `discount`: 18 rows.
- Negative discounts: 16 rows.
- Discounts above allowed range: 15 rows.
- Ship date earlier than order date: 22 rows.
- Sales mismatch rows: 34.
- Profit mismatch rows: 35.

## 2. Cleaning Actions Performed
- Preserved the original file unchanged as `data/raw_orders.xlsx`.
- Created cleaned output in `data/cleaned_orders.xlsx`.
- Standardized text fields by trimming spaces, removing unnecessary special characters, collapsing multiple spaces, and converting inconsistent case.
- Standardized category-like values such as `Office  Supplies`, `OFFICE SUPPLIES`, and `office supplies` to `Office Supplies`.
- Converted mixed date formats to a consistent `yyyy-mm-dd` format.
- Created calculated fields: `cleaned_discount`, `calculated_sales`, `calculated_profit`, `profit_margin`, `shipping_delay_days`, `order_month`, `order_year`, and `data_quality_flag`.
- Removed only exact duplicate row copies. Conflicting duplicate order IDs were kept and flagged for review.

## 3. Business Rules Applied
- Missing `region` was filled as `Unknown` and flagged.
- Missing `ship_mode` was filled as `Unknown` and flagged.
- Missing `discount` was treated as 0 only when quantity, unit price, sales, and cost were valid.
- Negative discounts were marked invalid.
- Discounts greater than 50% were marked invalid.
- Cancelled orders and failed payments were excluded from final completed sales summaries.
- Refunded/returned orders were separately summarized.
- Ship dates before order dates were marked invalid shipping records.

## 4. Assumptions Made
- The allowed maximum discount was assumed to be 50% because the assignment did not provide a numeric maximum. Values above 50% were treated as unusually high and invalid.
- Slash dates such as `08/31/2024` were interpreted in month/day/year format because the dataset includes dates where the second number is greater than 12.
- Dash dates such as `28-11-2024` were interpreted in day/month/year format.
- Profit was recalculated as `calculated_sales - cost`.
- A sales/profit mismatch was flagged when the absolute difference was greater than ₹1.00.

## 5. Records Removed
- 20 exact duplicate records were removed from `cleaned_orders.xlsx`.
- No conflicting duplicate `order_id` records were silently deleted.

## 6. Records Flagged
- Clean records: 505.
- Warning records: 296.
- Invalid records: 111.

## 7. Limitations
- Some business decisions, especially the discount threshold, required assumptions because the instructions did not specify exact numeric rules.
- Conflicting duplicate order IDs need business-owner review before final deletion or correction.
- Data entries marked invalid were kept in the cleaned file with flags for auditability instead of being deleted.
