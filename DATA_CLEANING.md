# Data Cleaning & Preparation Documentation

## 1. Project Dataset

The project uses an Indian retail sales CSV dataset containing 100,000 records and 25 columns, covering the period 2019–2023.

Data preparation was performed using Power Query in Microsoft Power BI Desktop.

## 2. Initial Data Inspection

The dataset was inspected using Power Query's data profiling features:

- Column Quality
- Column Distribution
- Column Profile

The profiling results showed no missing values or data errors in the inspected columns.

## 3. Data Type Corrections

The following data types were reviewed and applied:

| Column | Data Type |
|---|---|
| Sales Date | Date |
| Order Date | Date |
| Ship Date | Date |
| Sales | Decimal Number |
| Profit | Decimal Number |
| Quantity | Whole Number |
| Discount | Decimal Number |
| Postal Code | Text |

Postal Code was converted to Text because it represents an identifier rather than a value used in mathematical calculations.

## 4. Date Validation

Date columns were examined to identify inconsistencies.

### Shipping Date Validation

The condition `Ship Date < Order Date` was checked.

| Result | Records |
|---|---:|
| Valid | 100,000 |
| Invalid | 0 |

No shipping dates were found earlier than their corresponding order dates.

### Sales Date vs Order Date

The two date columns were compared.

| Result | Records |
|---|---:|
| Matching | 63 |
| Not Matching | 99,937 |

This showed that Sales Date and Order Date were not interchangeable.

### Original Year Column Validation

The original Year column was compared with both date columns.

**Against Order Date:**

| Result | Records |
|---|---:|
| Matching | 19,977 |
| Not Matching | 80,023 |

**Against Sales Date:**

| Result | Records |
|---|---:|
| Matching | 20,112 |
| Not Matching | 79,888 |

Because the original Year column contained substantial inconsistencies, it was removed from the analytical dataset.

## 5. Analytical Date Selection

Order Date was selected as the primary date for time-based reporting.

This decision was made to establish a consistent date basis for monthly and yearly sales analysis.

The selection represents an analytical convention because the original business meaning of the date fields was not independently verified.

## 6. Final Power Query Transformations

The following preparation steps were completed:

1. Reviewed dataset structure and column quality.
2. Verified data types.
3. Converted Postal Code to Text.
4. Validated shipping dates.
5. Compared Sales Date and Order Date.
6. Investigated inconsistencies in the original Year column.
7. Removed the unreliable Year column.
8. Removed temporary validation columns after completing the checks.
9. Renamed the final query to `Fact_Sales`.
10. Applied transformations using Close & Apply.

## 7. Final Outcome

The prepared dataset was loaded into Power BI for data modelling and dashboard development.

The final analytical model uses:

- `Fact_Sales` as the main sales table.
- `Dim_Date` as the supporting date dimension.
- `Order Date` as the active relationship date.

## 8. Data Quality Considerations

Although the dataset passed the inspected missing-value, error and shipping-date checks, date inconsistencies were identified and documented.

The original dataset's provenance and real-world accuracy have not been independently verified. Therefore, the analysis is presented as a portfolio and practice project rather than an audited retail business analysis.