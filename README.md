# Sales Dashboards created in Excel and Power BI

## Project Overview
This project consists of two dashboards made using [sample data from microsoft](https://learn.microsoft.com/en-us/power-bi/create-reports/sample-sales-and-marketing#get-the-pbix-file-for-this-sample). Both dashboards use Power Query to create a realtional data model from which the dashboards are created. The model schema diagram is shown below.

![Model Schema Diagram](https://github.com/MauriceBrown/sales_dashboard/blob/main/model_schema.png)

### Additional Tables
* revenue_units_selection: used for slicers to allow for dynamic switching between revenue or unit sales measures on charts

### Calculated Columns
* Product Table
  1. **ProductLine**: Two character code derived from the "Product" column using the "LEFT()" and "RIGHT()" functions
  2. **ManufacturerProductLine**: String denoting the manufacturer and product line derived from the "Product" column using the "LEFT()" function

### DAX Measures
* **Total Revenue**: calculated as the sum of sales_fact(Revenue As Decimal)
* **Total Unit Sales**: calculated as the sum of sales_fact(Units)
* **Total**: Returns either the "Total Revenue" measure or the "Total Unit Sales" measure, based a the slicer selection which filters the "revenue_unit_sales_table"
* **Total (All Manufacturers)**: Uses the "Calculate()" function to calulate "Total Revenue" when removing all filters for the "manufacturer" table from the filter context
* **Total (All Other Manufacturers)**: Calculated as the difference between the "Total (All Manufacturers)" and "Total" measures
* **Total YoY Growth**: Uses the "DateAdd()" time intellegence function to get the value of the "Total" measure for the previous year and then returns year-on-year growth as the ratio of this year to last year minus 1 (i.e. Total YoY = (Current Year/Previous Year) - 1)

## Downloading and using the dashboards
The data for these projects is hosted in the [tsv_files folder of this repo](https://github.com/MauriceBrown/sales_dashboard/tree/main/tsv_files) making it easy to share the Excel and PowerBI files. In order to use the dashboards, just [download the Excel file](https://github.com/MauriceBrown/sales_dashboard/raw/main/Sales%20Dashboard.xlsx) or [download the Power BI file](https://github.com/MauriceBrown/sales_dashboard/raw/main/Sales%20Dashboard.pbix) and start interacting with the dashboards. Any data they require will be automatically downloaded from this repo.

## Excel Dashboard
This dashboard shows revenue and unit sales by manufacturer over time. There is a slicer to select manufacturers (multi-select is enabled) as well as a timelime to select a date range.

## Power BI Report
The Power BI report shows a series of dashboards including custom tooltips, drill-through pages and custom measures calculated using DAX.


