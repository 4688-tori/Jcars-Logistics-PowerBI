# JCars Logistics Power BI Analysis

## Project Overview

The JCars Logistics Power BI project analyses vehicle sales, profitability, customer activity, branch performance, delivery and logistics operations, returns, cancellations, ratings, discounts, and other business performance indicators.

The project follows a complete Business Intelligence workflow:

**Raw Dataset → Data Quality Investigation → Data Cleaning → Transformation → Data Modelling → DAX Development → Dashboard Development → Analysis → Business Insights → Management Recommendations**

The final solution is designed to help management understand business performance, identify areas of value generation and inefficiency, investigate unusual patterns, and support evidence-based decision-making.

---

## Project Objectives

The main objectives of this project were to:

* Investigate the quality and reliability of the raw JCars dataset.
* Identify missing, inconsistent, invalid, duplicated, and incorrectly formatted data.
* Clean and transform the dataset using Power Query.
* Standardise monetary and categorical fields.
* Document assumptions and business rules used during data preparation.
* Build an analytical star-schema data model.
* Develop DAX measures for sales, profitability, customers, vehicles, operations, and time analysis.
* Design an interactive Power BI report for management and analytical users.
* Investigate unusual records and business patterns.
* Generate meaningful business insights.
* Develop evidence-based management recommendations.

---

## Dataset

The project uses the **JCars Logistics vehicle sales and operations dataset** supplied for the assessment.

The original dataset was provided as a flat CSV file and contained vehicle, customer, transaction, financial, operational, and location-related information.

The repository contains the original dataset used as the source for the analysis.

### Main Data Areas

The dataset supports analysis of:

* Vehicle information
* Customer information
* Sales transactions
* Revenue and costs
* Discounts
* Delivery and logistics
* Branch and location performance
* Payment methods
* Customer ratings and reviews
* Returns and cancellations
* Order dates
* Vehicle characteristics

---

## Data Quality Investigation

Before modelling, the raw dataset was investigated to identify data-quality issues that could affect analysis.

The investigation considered:

* Missing and blank values
* Null values
* Duplicate or repeated records
* Invalid numerical values
* Negative values
* Text stored in numerical fields
* Currency symbols and currency labels
* Currency abbreviations
* Values containing `K` and `M` suffixes
* Invalid or inconsistent dates
* Placeholder values such as `-` and `TBD`
* Ratings outside the expected range
* Inconsistent discount representations
* Inconsistent categorical text
* Invalid or incomplete transaction information

The purpose of the audit was not simply to remove problematic records, but to determine whether values could be corrected, standardised, replaced using an explicit business rule, or retained for further investigation.

---

## Data Cleaning and Transformation

Power Query was used to prepare the dataset for analysis.

The major transformation activities included:

1. Promoting the correct row to column headers.
2. Standardising column data types.
3. Cleaning text fields and removing unnecessary spaces.
4. Handling blank, null, and placeholder values.
5. Standardising numerical fields.
6. Cleaning monetary values.
7. Handling negative values according to the defined business rules.
8. Standardising discount values.
9. Standardising customer ratings.
10. Cleaning and standardising date fields.
11. Creating analytical keys required for the data model.
12. Preparing dimension and fact tables.
13. Validating the cleaned dataset before modelling.

The cleaned data was then used as the basis for the Power BI analytical model.

---

## Currency Handling

The dataset contained monetary values represented using different symbols, labels, and formats.

The final analysis uses **Kenyan Shillings (KES)** as the reporting currency.

Currency-related text and symbols were cleaned during Power Query transformation. Values represented using suffixes such as `K` and `M` were interpreted according to their numerical meaning.

Where the source contained foreign-currency labels but did not provide sufficient information to establish a reliable exchange-rate conversion, unsupported conversion was not introduced into the model.

This limitation is documented as part of the project's assumptions.

---

## Key Assumptions and Business Rules

The analysis uses documented business rules to provide consistent treatment of incomplete or inconsistent records.

Examples include:

| Field           | Business Rule                         |
| --------------- | ------------------------------------- |
| Discount        | Missing discount treated as 0         |
| Units Sold      | Missing units treated as 1            |
| Review Count    | Missing review count treated as 0     |
| Delivery Fee    | Missing delivery fee treated as 0     |
| Logistics Cost  | Missing logistics cost treated as 0   |
| Customer Rating | Missing rating treated as 3           |
| Customer Age    | Missing age treated as 35             |
| Vehicle Year    | Missing vehicle year treated as 2022  |
| Order ID        | Missing order ID treated as `UNKNOWN` |

Revenue was calculated using the project's defined business rule:

**Revenue = Units Sold × Unit Selling Price × (1 − Discount) + Delivery Fee**

The project does not introduce unsupported financial costs or causal explanations where the source data does not provide sufficient evidence.

Unusual records were investigated rather than automatically deleted.

---

## Data Model

The final Power BI solution uses a **star-schema data model**.

### Fact Table

**FactSales**

The fact table contains transaction-level information used for quantitative analysis.

### Dimension Tables

**Dim Vehicle**

* Vehicle Key
* Car Make
* Car Model
* Vehicle Type
* Vehicle Year
* Fuel Type
* Transmission
* Colour

**Dim Customer**

Contains customer-related descriptive information.

**Dim Location**

Contains branch and location information used for geographical and branch-level analysis.

**Dim Date**

* Date
* Date Key
* Month
* Year

The Date dimension is connected to the sales fact table using the appropriate date key.

### Relationships

The dimensions use **one-to-many relationships** into the FactSales table, supporting filtering and aggregation while maintaining a structured analytical model.

This approach separates descriptive attributes from transactional measures and makes the report easier to maintain and analyse.

---

## DAX Development

DAX was used to create analytical measures required by the assessment.

The measures cover areas including:

### Sales and Revenue

* Total Revenue
* Units Sold
* Total Orders
* Average Order Value
* Average Selling Price

### Cost and Profitability

* Total Cost
* Gross Profit
* Profit Margin
* Profit Per Vehicle

### Customer Analysis

* Total Customers
* Customer-related performance measures
* Customer activity and review measures

### Operations

* Delivery Fees
* Logistics Costs
* Returns
* Cancellations
* Customer Ratings

### Discounts and Payment Methods

* Average Discount
* Discount-related analysis
* Revenue by Payment Method

### Rankings and Time Analysis

* Vehicle rankings
* Branch/location rankings
* Year and month analysis
* Time-based comparisons

The measures were designed to support both KPI cards and interactive visual analysis.

---

## Report Structure

The final Power BI report is organised into the following pages.

### 1. Executive Dashboard

Provides a high-level management view of:

* Revenue
* Profitability
* Units and orders
* Customer activity
* Key operational indicators
* Overall business performance

### 2. Sales & Analysis

Focuses on sales performance and allows users to analyse sales by relevant business dimensions such as vehicle, branch, location, time, and payment method.

### 3. Profitability & Branches

Examines profitability and branch-level performance.

The page supports comparisons of financial performance across branches and related business dimensions.

### 4. Branch Detail

Provides a more detailed branch-level analysis.

A drill-through experience allows users to move from broader analysis into branch-specific information.

### 5. Operations & Customer Experience

Analyses operational and customer-related indicators including:

* Delivery
* Logistics
* Returns
* Cancellations
* Ratings
* Reviews
* Customer activity

### 6. Investigations & Exceptions

Focuses on unusual records, exceptions, and business patterns requiring further investigation.

This page helps distinguish normal performance from records that may require management attention.

### 7. Management Insights & Recommendations

Translates the analytical findings into business insights and evidence-based recommendations for management.

---

## Interactivity

The report includes interactive filtering and navigation features.

Key slicers include:

* Year
* Month
* Branch
* Location
* Vehicle Type
* Car Make
* Car Model
* Payment Method

The report also uses:

* Cross-filtering
* Drill-through
* Tooltips
* Page navigation
* Dynamic DAX measures
* Interactive visual selections

A dedicated **Branch Detail** drill-through page and **Branch Tooltip** provide additional analytical context without overcrowding the main dashboard pages.

---

## Key Analytical Areas

The final solution allows management to investigate questions such as:

* How is the business performing in terms of revenue and profitability?
* Which branches and locations generate different levels of financial performance?
* Which vehicle types, makes, and models contribute to sales?
* How do discounts relate to sales and profitability?
* How do payment methods contribute to revenue?
* What operational patterns exist around delivery and logistics?
* What patterns exist in returns and cancellations?
* How do customer ratings and reviews relate to business activity?
* Which records or business patterns require further investigation?
* How does performance change over time?

The report focuses on patterns supported by the available data rather than treating correlation as proof of causation.

---

## Key Insights

The analysis identified several areas that are important for management attention:

1. **Sales and profitability should be analysed together.** High sales activity does not automatically represent the same level of profitability.

2. **Branch performance differs across financial and operational measures.** Revenue, costs, and profitability should therefore be considered together when assessing branch performance.

3. **Vehicle-level analysis provides useful detail beyond overall sales totals.** Comparing vehicle types, makes, models, and characteristics helps identify differences in sales and profitability contribution.

4. **Discounts require monitoring alongside profitability.** A discount can support sales activity while also affecting the amount of value retained by the business.

5. **Operational indicators provide additional context to financial performance.** Delivery, logistics, returns, cancellations, and customer feedback can help explain areas requiring further investigation.

6. **Data quality has a direct effect on analytical reliability.** Standardising currencies, dates, numerical values, categories, and missing values was therefore an important part of the project.

7. **Unusual records should be investigated before being treated as errors.** Some exceptions may represent genuine business activity rather than incorrect data.

---

## Management Recommendations

Based on the analysis, management should:

### 1. Monitor profitability alongside sales

Revenue should not be used as the only performance indicator. Management should review revenue, costs, gross profit, and profit margin together.

### 2. Review branch performance regularly

Branch-level KPIs should be monitored to identify differences in financial and operational performance and determine where additional investigation may be required.

### 3. Evaluate discount effectiveness

Discounting should be monitored against profitability and sales performance so that discounts are not evaluated only on their ability to increase transaction activity.

### 4. Investigate operational exceptions

Returns, cancellations, delivery issues, logistics costs, and unusual records should be reviewed regularly to identify potential process improvements.

### 5. Use vehicle-level analysis for decision-making

Management can use vehicle make, model, type, year, and related performance indicators to support inventory and sales decisions.

---

## Challenges Encountered

Several challenges were encountered during development, including:

* Inconsistent source-data formats
* Missing and invalid values
* Currency inconsistencies
* Date-format inconsistencies
* Numerical fields containing text
* Power Query performance during extensive transformations
* Data modelling and relationship configuration
* Developing DAX measures for different analytical requirements
* Power BI file-saving and recovery issues during development
* Ensuring the final dashboard remained both analytical and management-friendly

These challenges provided practical experience in the complete Power BI development workflow.

---

## Lessons Learned

This project demonstrated that effective Power BI development involves more than creating charts.

Key lessons include:

* Data quality should be investigated before analysis.
* Cleaning decisions should be documented.
* Assumptions should be explicit and reproducible.
* A well-designed data model improves analytical flexibility.
* DAX measures should support meaningful business questions.
* Visuals should communicate insights rather than simply display data.
* Exceptions should be investigated before being removed.
* Validation is necessary at each major stage of the BI workflow.
* Business recommendations should be connected to evidence from the analysis.

---

## Repository Structure

```text
JCars-Logistics-PowerBI/
│
├── Dataset/
│   └── Jcars_data.csv
│
├── Documentation/
│   └── Project Documentation.docx
│
├── PowerBI/
│   └── Jcars.e.pbix
│
├── Screenshots/
│   ├── Branch Details.png
│   ├── Executive Dshboard.png
│   ├── Investigations&Operations.png
│   ├── Management Insights&Expectations.png
│   ├── Model view.png
│   ├── Operations&Customer Experience.png
│   └── Profitabiity &Branches.png
│
└── README.md
```

---

## Tools Used

* **Microsoft Power BI Desktop** — data modelling, DAX, visualisation and report development
* **Power Query** — data cleaning and transformation
* **DAX** — analytical calculations and measures
* **Microsoft Word** — project documentation
* **Git** — version control
* **GitHub** — project repository and submission

---

## Project Outcome

The completed JCars Logistics Power BI solution provides an interactive analytical environment for examining sales, profitability, vehicles, branches, customers, operations, and exceptions.

The project demonstrates the full process of transforming a raw business dataset into a structured analytical model and an interactive management reporting solution.

The final deliverables include the Power BI report, source dataset, supporting documentation, screenshots, and this README.
