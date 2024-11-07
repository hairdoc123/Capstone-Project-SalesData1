# Capstone-Project-SalesData1

### Project Topic: SalesData Analysis

### Project Overview

This project analysed the sales performance of a retail store, identify trends, sales performance of each products and the region that makes the highest sales.

### Column Description
- OrderID: A unique identfier for each order placed by a customer

- CustomerID: A distinct identifier for each customer placing order

- Region: The geographical location (North, South, East, West)

 - OrderDate: The date in which order was made

- Quantity: The number of item/product purchased for each product

- UnitPrice: The price per unit of the product

### Data Sources

The primary source of Data used here is DataSales.csv

### Tools Used

- Microsoft Excel [Download Here](https://www.microsoft.com)
    1. For Data Cleaning,
    2. For Analysis
    3. For Visualization

- SQL- Structured query Language for quering of Data

- Power BI: For Data Cleaning And Visualization

- GitHub for Portfolio Building

### Data Clening And Preparation

In the initial phase of the data cleaning and preparation, we perform the following actions;

1. Data loading and Inspection
2. Removing Duplicates
3. Data cleaning and Formating

### Exploratory Data Analysis (EDA)

EDA involved the exploration of the Data to answer some questions above the Data such as;

- retrieve the total sales for each product category.
  
- find the number of sales transactions in each region.

- find the highest-selling product by total sales value.

- calculate total revenue per product.

- calculate monthly sales totals for the current year.
  
- find the top 5 customers by total purchase amount.
  
- calculate the percentage of total sales contributed by each region.
  
- identify products with no sales in the last quarter.

### Data Analysis

This is where we include  some basic lines of queries and some of the DAX expressions used during your analysis;

.....SALESDATA PROJECT........ 
```
Select * from [dbo].[SalesDatacsv1]
```

1..... Total number of each product category....

```SQL
Select Product, SUM(Total_Revenue) As Total_Sales
From [dbo].[SalesDatacsv1]
Group By Product
```

2. 	.....NUMBER OF SALES TRANSACTIONS PER REGION....
   
```SQL
Select Region, COUNT(OrderID) As Number_Of_SalesTrans
From [dbo].[SalesDatacsv1]
Group By Region
```

3. .....The highest selling product by total sales value..... 

```SQL
Select Top(1) Product, Sum(Total_Revenue) As Total_Sales
From [dbo].[SalesDatacsv1]
Group By Product
```

4. .....TOTAL REVENURE PER PRODUCT.....

```SQL
Select Product, SUM(Total_Revenue) As Total_sales
From [dbo].[SalesDatacsv1]
Group By Product
```
 
5.  ....Monthly sales total for the current year....

```SQL
Select Month(OrderDate) As Month, SUM(Total_Revenue) AS MonthlySales_Total
From [dbo].[SalesDatacsv1]
	WHERE
		YEAR(OrderDate) = 2024
GROUP BY MONTH(OrderDate)
```

6. ....Top 5 customers by total purchase amount....

```SQL
Select Top (5) Customer_id, SUM(Total_Revenue) As TotalPurchase_Amount
From [dbo].[SalesDatacsv1]
Group By Customer_id
Order By TotalPurchase_Amount DESC
```

7.   ..... Calculate the Percentage of Total sales Contribution By Region....

```SQL
SELECT Region, sum(Total_Revenue) AS Regional_Sales,
CONCAT(ROUND(SUM(Total_Revenue)/ (Select sum(Total_Revenue) from [dbo].[SalesDatacsv1]) * 100,2), '%') As Sales_Percentage
From [dbo].[SalesDatacsv1]
Group By Region
Order By Regional_Sales DESC
```

8. .....identify product with no sales in the last quarder....

```SQL
SELECT PRODUCT from [dbo].[SalesDatacsv1]
where product NOT IN (select distinct product from [dbo].[SalesDatacsv1]
where orderDate>=DateAdd(Quarter, -1, GETDATE()))
group by product;
```

### Data Visualization


