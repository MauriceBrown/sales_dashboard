# Sales Dashboards created in Excel and Power BI

## Project Overview
### 1) Summary
This project consists of two dashboards made using [sample data from microsoft](https://learn.microsoft.com/en-us/power-bi/create-reports/sample-sales-and-marketing#get-the-pbix-file-for-this-sample). Both dashboards use Power Query to create a realtional data model from which the dashboards are created. The model schema diagram is shown below.

![Model Schema Diagram](https://github.com/MauriceBrown/sales_dashboard/blob/main/model_schema.png)

### 2) Additional Tables
* **revenue_units_selection**: used for slicers to allow for dynamic switching between revenue or unit sales measures on charts.

### 3) Calculated Columns
* Product Table
  1. **ProductLine**: Two character code derived from the "Product" column using the "LEFT()" and "RIGHT()" functions.
  2. **ManufacturerProductLine**: String denoting the manufacturer and product line derived from the "Product" column using the "LEFT()" function.

### 4) DAX Measures
* **Total Revenue**: calculated as the sum of sales_fact(Revenue As Decimal).
* **Total Unit Sales**: calculated as the sum of sales_fact(Units).
* **Total**: Returns either the "Total Revenue" measure or the "Total Unit Sales" measure, based a the slicer selection which filters the "revenue_unit_sales_table".
* **Total (All Manufacturers)**: Uses the "Calculate()" function to calulate "Total Revenue" when removing all filters for the "manufacturer" table from the filter context.
* **Total (All Other Manufacturers)**: Calculated as the difference between the "Total (All Manufacturers)" and "Total" measures.
* **Total YoY Growth**: Uses the "DateAdd()" time intellegence function to get the value of the "Total" measure for the previous year and then returns year-on-year growth as the ratio of this year to last year minus 1 (i.e. Total YoY = (Current Year/Previous Year) - 1).

## Downloading and using the dashboards
The data for these projects is hosted in the [tsv_files folder of this repo](https://github.com/MauriceBrown/sales_dashboard/tree/main/tsv_files) making it easy to share the Excel and PowerBI files. In order to use the dashboards, just [download the Excel file](https://github.com/MauriceBrown/sales_dashboard/raw/main/Sales%20Dashboard.xlsx) or [download the Power BI file](https://github.com/MauriceBrown/sales_dashboard/raw/main/Sales%20Dashboard.pbix) and start interacting with the dashboards. Any data they require will be automatically downloaded from this repo.

## Excel Dashboard
This dashboard shows revenue and unit sales by manufacturer over time. There is a slicer to select manufacturers (multi-select is enabled) as well as a timeline to select a date range.

## Power BI Report
The Power BI report shows a series of dashboards including custom tooltips, drill-through pages and custom measures calculated using DAX.

### Report pages
1. **High Level**: Shows an overview of sales and sentiment. Users can select whether to look at **Revenue** or **Unit Sales** using the slicer in the top left of the page. The date range can also be selected.
2. **Manufacturer Detail**: Shows sales and sentiment breakdowns for each manufacturer. The slicers in the top left allow the user to select **Revenue** or **Unit Sales** as well as the time period and the manufacturer.
  * Note: the manufacturer slicer is set to single select so only **ONE** manufacturer can be viewed at a time.

### Custom Tooltips
* **High Level** page
  1. **Total YoY Growth** chart (top left): Hovering over data bars reveals the custom tool tip showing a breakdown of sales in the selected year by **product line**, **VanArsdel**, **region** and **category**
  2. **Top 10 States** chart (middle left): Hovering over data bars reveals the custom tool tip showing a breakdown of sales in the selected state by **district**
  3. **Product Line** chart (bottom left): Hovering over data bars reveals the custom tool tip showing a breakdown of sales of the product line by **manufacturer**
 
### Drill Throughs
1. **Geography - Drill Through** page: showing further detail for **Revenue** or **Unit Sales** (depending on the user selected filter) as well as **Sentiment** broken down by (manufacturer, segment and product line).



