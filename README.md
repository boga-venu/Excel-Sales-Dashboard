# Excel Sales Dashboard
 This project showcases an intersting Excel sales dashboard that provides insights into sales data with interesting Visializations using just Four pivot tables. 
 
![Excel Dashboard 03](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/1e87f43c-7712-49dc-8c3f-ea6660994787)

## Features
- Total sales and revenue overview
- Monthly sales trends
- Regional sales distribution
- Product category performance

## Files
- `Online Sales Dashboard.xlsx`: The Excel file containing the dashboard.
- `Excel Dashboard 01.png`,`Excel Dashboard 02.png`,`Excel Dashboard 03.png`: Screenshots of the Dashboard in different scenarios.

## How to Use
1. Download the `Sales Dashboard.xlsx` file.
2. Open it in Excel to explore the dashboard.

## Detailed Information
- The section without background represent overall sales and revenue performance
  
  ![Excel Dasshboard Overall](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/6694afdb-5bf1-49ff-b62c-f7131a341871)

- the section with background represent Category Performance
  
  ![Excel Dashboard Category](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/c9b7cd0a-e05e-43e0-ae26-779f2ccbcc68)

- As you can see in the picture all the charts and cards give the information regarding a category(Electronics) performance which is selected in the slicer
- If we select different category(Clothing) the information in this section also changes as below
  
  ![Excel Dasshboard Category 02](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/280564e1-ecef-426a-90cf-383749e1bea5)

- Titles are also change according to the selection for more clarity.

## Working 

Tables section 
- As mentioned in the description we use only 4 pivot tables to create the Dashboard
- We create normal Tables fetched from pivot tables to create the visuals
- `Pivot table 1` is created as shown below 
  
  ![Pivot table 1](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/e302de74-1862-4693-b32f-ee861c300bcb)

- It is connected to category slicer. The selection of the category affects it as shown below

  ![Pivot Table 1 Category selected](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/a5fc2e63-4025-4b85-9324-fc4bae98a743)

- `Pivot Table 2` is not connected to any slicer and the information is used to compare the data.
  
  ![Pivot table 2](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/955194e7-327e-4b82-a0af-da2253bdf091)

- `Table 1` is created by using "Grand Total" from `Pivot table 1` and "Units Sold" from `Pivot Table 2` using `GETPIVOTDATA` formula

  ![Table 1](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/860367e2-7ad4-417f-8e40-71d5289328da)

- It is used to compare the total sales to the sales of individual category

- `Pivot table 3` is connected to month slicer and `Pivot table 4` is not connected to any slicer for comparition

  ![Pivot Table 3](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/bd25fb34-4a32-4eeb-b390-e80460a7f900) ![Pivot table 4](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/55817e2e-5b83-4bd8-9f63-1fef5f00517f)

- `Table 2` is created from these two pivot tables but a lot of things are needed to create this table

  ![Table 2](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/99b269f6-deb3-40f8-89d6-6c6a9ecadbe3)

- "Category" column can be directly fetched from `Pivot table 3` by "Direct Refencing" to "Row Lables"
  
- For "Region" we use "Filter formula" as `FILTER($B$50:$G$50,(B52:G52>0)*($B$50:$G$50<>""))`
- "($B$50:$G$50,(B52:G52>0)" This section gives values from "$B$50:$G$50" whose column values are non zero
- "($B$50:$G$50<>""))" This section omits any blank cells in "$B$50:$G$50"
- As the order of the categories are dinamically changed in `Table 2` if changed in `Pivot Table 3` due to refencing the data in "Region" column will be accurate with this formula

- "Total Sales" can be fetched from "Units Sold" from `Pivot Table 3` using "GetPivotdata" formula
- If we use referencing to get the formula then it gives `GETPIVOTDATA("Units Sold",$A$49,"Product Category","Beauty Products")` we have to change the last attribute from `Beauty Products` to `[@Category]`(By selecting category column from `Table 2`

- "Actual sales", "Actual revenue" and "Average Unit Price" are fetched from `Pivot table 4` and "Total revenue" from `Pivot table 3` using same the process as "Total Sales"

- `Table 3` is created from `Table 2` as shown below

  ![Table 3](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/c430e5ac-db5a-477d-8152-e0aeb3c38099)


- "Region" Column is fetched using `UNIQUE(Table2[Region])` Formula
- "Sales" Column using `SUMIF(Table2[Region],A40#,Table2[Total Sales])`
- "Revenue" Column using `SUMIF(Table2[Region],A40#,Table2[@[Total Revenue]])`

Information Section
- Chart titles and the information for the cards in the dashboard are fetched from the table below
  
  ![Information](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/38bccbea-64e0-4860-95b1-1104870d8990)

- "Total Sales" chart title is obtained using `IF(C5="Grand total","Total Sales from "&B5,"Sales from the Categories")` - as `Pivot table 1` is affected by slicer, If only one category is selected then "Grand Total" will be in "B5" cell. Using this we can find the category selected in the "Category Slicer"  in the Dashboard
- "Contribution" chart title is obtained similarly by using `IF(C5="Grand total","Contribution of "&B5&" in Total Sales","Contribution of Categories in Total Sales")`

- "Most Valuable Region" is obtained by checking from which region maximum revenue generated by using formula `SWITCH(MAX(C40#),C40,A40,C41,A41,C42,A42)` on "Revenue" Column fSalesrom `Table 3`
- "Most Valuable Category" is obtained similarly by using `SWITCH(MAX(Table2[Total Revenue]),J40,E40,J41,E41,J42,E42,J43,E43,J44,E44,J45,E45)` on "Total Revenue" Column from `Table 2'
- "Total Revenue" by using `GETPIVOTDATA("Total Revenue",$A$49)` referencing to "Grand Total" from `Pivot Table 1`
- "Needs Attention" by using `SWITCH(MIN(Table2[Total Sales]),G40,E40,G41,E41,G42,E42,G43,E43,G44,E44,G45,E45)`
- "Most Selling Category" by using `SWITCH(MAX(Table2[Total Sales]),G40,E40,G41,E41,G42,E42,G43,E43,G44,E44,G45,E45)`

Finally For highliting the selected category in the charts as shown below

 ![Highlight](https://github.com/boga-venu/Excel-Sales-Dashboard/assets/174999641/fd9dc496-d327-4b43-823f-69230893d617)

- The last two columns from `Table 2` are used for highliting them
- "Avgprice Highlight" is obtained by using `IF(AND($L$20<>"All",$L$21=[@Category]),[@[Average Unit Price]],NA())`
- It gives the value from "Average Unit Price" column if the category value matches the value of selected category otherwise gives #N/A
- By using this column and "Average unit price" column we can create a combo chart resulting in the above highlighting effect.

## Conclusion  

 Go through all the sections and all the tables from the file 'Sales Dasboard' mainly go through Sheet `Pivot Tables` all the fun is happening there itself

  ---Happy Exploring---
