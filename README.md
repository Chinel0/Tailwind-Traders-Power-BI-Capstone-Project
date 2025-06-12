Tailwind Traders Power BI Capstone Project
Project Overview
This capstone project is the culmination of my Microsoft Power BI Data Analyst Professional Certificate on Coursera. It demonstrates my ability to apply end-to-end Power BI skills in a realistic business scenario. 
The project simulates a real-world analytics task where I worked with Tailwind Traders’ sales, purchases, currency exchange, and calendar data to develop interactive reports and executive dashboards.
The primary goal was to transform raw sales and financial data from multiple sources into insightful, visually compelling reports that help Tailwind Traders make data-driven decisions about their global sales and profits.

Key Features and Deliverables
Data Preparation and Transformation:
Imported and cleaned data from Excel sources.
Applied data type corrections and handled inconsistent formats.
Conducted data profiling to determine error, distinct and unique values, and statistical analysis
Filtered and refined data by excluding refunded purchases.
Integrated currency exchange data using a Python script to standardize values to USD.

Data Modeling:
Designed a snowflake schema connecting Sales, Purchases, Countries, Exchange Rates, and Calendar tables.
Created and managed relationships with appropriate cardinality and bidirectional filtering.
Developed a dedicated Calendar table for advanced time intelligence.

Calculations and DAX Measures:
Created calculated columns and measures for Gross Revenue, Total Tax, Net Revenue, and Profit.
Developed time-based DAX measures for Yearly Profit Margin, Quarterly Profit, and Year-to-Date Profit.
Calculated Median Sales for robust performance analysis.

Visualization and Reporting:
Built comprehensive Sales and Profit Overview reports featuring bar charts, column charts, pie charts, line charts, area charts, cards, and KPIs.
Created interactive dashboards enabling slicing by country and date.
Employed advanced features like trend lines, data labels, sorting, and detailed donut chart labels.
Configured mobile-friendly dashboard layouts for executive access on the go.

Security and Data Governance:
Configured row-level security (RLS) for role-based data access.
Applied data sensitivity labels to classify confidential information.
Set up data alerts and report subscriptions to keep stakeholders informed in real time.

```Key DAX Measures and Formulas
Yearly Profit Margin (Calculates the ratio of total profit to net revenue as a percentage.)
Yearly Profit Margin = 
DIVIDE(
    SUM('Sales in USD'[Profit USD]),
    SUM('Sales in USD'[Net Revenue USD])
) 

Quarterly Profit (Aggregates total profit for the current quarter.)
Quarterly Profit = 
CALCULATE(
    SUM('Sales in USD'[Profit USD]),
    DATESQTD('CalendarTable'[Date])
)

Year-to-Date Profit (Calculates running total profit from the start of the year to the current date.)
YTD Profit = 
TOTALYTD(
    SUM('Sales in USD'[Profit USD]),
    'CalendarTable'[Date]
)

Median Sales (Identifies the middle sales value to assess performance stability.)
Median Sales = 
MEDIAN('Sales in USD'[Gross Revenue USD])

Calendar Table Creation (DAX) (Creates a comprehensive date table with useful date parts for time intelligence.)
CalendarTable = 
ADDCOLUMNS(
    CALENDAR(DATE(2020, 1, 1), DATE(2023, 12, 31)),
    "Year", YEAR([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "MMMM"),
    "Quarter", QUARTER([Date]),
    "Weekday", WEEKDAY([Date]),
    "Day", DAY([Date])
)

Sales in USD Calculated Table (Converts all sales figures into USD using related exchange rates.)
Sales in USD = 
ADDCOLUMNS(
    Sales,
    "Country Name", RELATED(Countries[Country]),
    "Exchange Rate", RELATED('Currency Exchange'[ExchangeRate]),
    "Exchange Currency", RELATED('Currency Exchange'[Exchange Currency]),
    "Gross Revenue USD", [Gross Revenue] * RELATED('Currency Exchange'[ExchangeRate]),
    "Net Revenue USD", [Net Revenue] * RELATED('Currency Exchange'[ExchangeRate]),
    "Total Tax USD", [Total Tax] * RELATED('Currency Exchange'[ExchangeRate])
)

Power Query Transformations
Python Script for Currency Exchange Date
import pandas as pd
from io import StringIO

data = """Exchange ID;ExchangeRate;Exchange Currency
1;1;USD
2;0,75;GBP
3;0,85;EUR
4;3,67;AED
5;1,3;AUD"""
df = pd.read_csv(StringIO(data), sep=';')

Power Query M snippet for data type transformation (Assigns correct data types to columns for accurate processing and analysis.)
#"Changed Type" = Table.TransformColumnTypes(
    #"Previous Step",
    {
        {"OrderID", Int64.Type},
        {"Gross Product Price", type number},
        {"Tax Per Product", type number},
        {"Quantity Purchased", Int64.Type},
        {"Loyalty Points", Int64.Type},
        {"Stock", Int64.Type},
        {"Product Category", type text},
        {"Rating", type number}
    }
)
```

Tools & Technologies
Power BI Desktop & Power BI Service: Core platform for data loading, modeling, and visualization.
Microsoft Excel: Initial data source preparation.
Python (within Power BI): Used for transforming and loading historical currency exchange data.
DAX (Data Analysis Expressions): Advanced formula language for custom calculations and aggregations.
Power BI Features: Dataflows, relationships, performance analyzer, bookmarks, Q&A visual, drillthrough, and more.

Project Structure & Workflow
Data Import & Cleaning: Imported Excel sales and purchases data, set correct data types, and cleaned inconsistencies.
Currency Data Preparation: Loaded currency exchange rates via Python script for accurate USD conversion.
Data Modeling: Defined relationships, created a calendar table, and built a robust snowflake schema.
DAX Calculations: Developed measures for revenue, profit, tax, and median sales.
Report Design: Built visually rich reports with various charts and KPIs, optimized for different audiences.
Dashboard Assembly: Curated executive dashboards with pinned visuals, configured mobile layouts.
Security Setup: Applied RLS and data sensitivity labels, configured alerts and subscriptions for timely updates.

Key Learnings & Skills Demonstrated
Mastery of Power BI’s end-to-end analytics capabilities — from data ingestion through to actionable insights.
Hands-on experience with real-world challenges like data cleaning, modeling complexities, and dynamic security.
Proficient use of DAX for advanced calculations and time intelligence.
Designing user-friendly, insightful reports and dashboards that facilitate business decision-making.
Understanding of data governance principles, security best practices, and report automation features.

How to Explore the Project
Open the provided Power BI report file (Tailwind Traders Report.pbix) using Power BI Desktop.
Navigate through the Sales Overview and Profit Overview report pages.
Explore interactive visuals such as slicers and filters to analyze sales and profit data by country, product, and time.
Review the executive dashboard and try switching to the mobile layout for responsive design insights.
Check the data model view to understand the relationships and calculated columns/measures implemented.
Review the configured RLS roles and data sensitivity labels (if applicable).

Next Steps
Further optimize performance by exploring aggregation tables and incremental refresh.
Extend security configurations with dynamic RLS for scalable user access management.
Integrate additional data sources for a more comprehensive business view.
Share the project on Power BI Service for collaborative team analysis and stakeholder engagement.

Contact
For questions, collaborations, or feedback, feel free to reach out:

Name: Chinelo Lydia Nweke
Email: Nwekecl16046@gmail.com
LinkedIn: www.linkedin.com/in/chinelo-nweke 

