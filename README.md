# Sarthak-Kapil_2511237_part1_data_cleaning
# Order Data Cleaning and Pivot Analysis Assignment

## 1. Problem Summary
This project cleans and validates the raw order dataset while preserving the original data. The cleaned dataset, data quality report, pivot summary report, and cleaning log were created as required by the assignment.

## 2. Dataset Description
- Source file: `data/raw_orders.xlsx`
- Main sheet: `raw_orders`
- Rows in raw dataset: 932
- Columns in raw dataset: 21
- Key fields: `order_id`, `order_date`, `ship_date`, `customer_name`, `segment`, `region`, `state`, `city`, `category`, `sub_category`, `ship_mode`, `quantity`, `unit_price`, `discount`, `sales`, `cost`, `profit`, `payment_status`, and `order_status`.

## 3. Tools Used
- Microsoft Excel / Excel-compatible `.xlsx` files
- Python for repeatable cleaning and validation
- Pivot tables/summaries for business analysis

## 4. Cleaning Steps Performed
1. Preserved the original workbook in `data/raw_orders.xlsx`.
2. Created a separate cleaned workbook: `data/cleaned_orders.xlsx`.
3. Cleaned text fields using trimming, case standardization, special-character handling, and value mapping.
4. Standardized dates into `yyyy-mm-dd` format.
5. Created `shipping_delay_days` from `ship_date - order_date`.
6. Parsed discounts including percentage values such as `85%`.
7. Created calculated columns for sales, profit, margin, month, year, and quality flags.
8. Removed exact duplicate row copies.
9. Kept conflicting duplicate order IDs and flagged them instead of deleting them silently.

## 5. Business Rules Applied
- Missing `region` → filled as `Unknown` and flagged.
- Missing `ship_mode` → filled as `Unknown` and flagged.
- Missing `discount` → treated as 0 only when other sales fields were valid.
- Negative discounts → invalid.
- Discounts above 50% → invalid.
- Cancelled orders → excluded from completed sales summary.
- Failed payments → excluded from completed sales summary.
- Refunded/returned orders → separately summarized.
- Ship date before order date → invalid shipping record.

## 6. Summary of Data Quality Issues Found
| Issue | Count |
|---|---:|
| Original raw rows | 932 |
| Cleaned rows after exact duplicate removal | 912 |
| Exact duplicate rows found | 40 |
| Exact duplicate records removed | 20 |
| Rows with duplicate order IDs | 63 |
| Conflicting duplicate order IDs | 12 |
| Missing region filled | 26 |
| Missing ship mode filled | 22 |
| Missing discounts treated as 0 | 18 |
| Negative discounts | 16 |
| Discounts above 50% | 15 |
| Ship date before order date | 22 |
| Sales mismatch rows | 34 |
| Profit mismatch rows | 35 |
| Clean rows | 505 |
| Warning rows | 296 |
| Invalid rows | 111 |

## 7. Summary of Final Pivot Reports
The file `outputs/pivot_summary.xlsx` contains the required pivot summaries:
1. Sales and profit by region
2. Sales and profit by category and sub-category
3. Order count by ship mode
4. Profit margin by customer segment
5. Refunded/cancelled/failed orders by region
6. Monthly sales trend

At least two pivot outputs include sorting/filtering through sorted summary tables.

## 8. Key Business Insights
- Completed sales summaries use only clean, paid, completed orders.
- Cancelled, failed, returned, and refunded orders are excluded or separately summarized to avoid overstating revenue.
- Duplicate order IDs with conflicting data should be reviewed before final business use.
- Discount quality issues can materially affect sales and profit calculations.

## 9. Assumptions and Limitations
- Discount above 50% was treated as invalid because no exact maximum was specified.
- Slash dates were interpreted as month/day/year; dash dates were interpreted as day/month/year.
- Calculation mismatches were flagged when the difference exceeded ₹1.00.
- Invalid rows were not deleted; they were retained with clear flags for evaluator review.

## 10. Screenshots Included
Add screenshots of the following files/sheets before submission:
- `data/cleaned_orders.xlsx` → `cleaned_orders` sheet
- `outputs/data_quality_report.xlsx` → `Summary`, `Duplicate Summary`, `Invalid Discounts`, and `Clean vs Flagged`
- `outputs/pivot_summary.xlsx` → each pivot summary sheet and charts
