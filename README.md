
# Automobile Sales PowerBI Report and Analysis
## Author
**Name:** Adham Sherif Hussein Ebaid  
**Email:** adhamebaid1@gmail.com 
## Description
This project is a comprehensive analysis of automobile sales data. Utilizing the powerful data visualization and business intelligence capabilities of PowerBI and Excel, the project provides insightful reports and dashboards to understand sales trends, customer behavior, and product performance.


![Overview GIF](https://github.com/user-attachments/assets/07b237b4-474f-47c2-8fdb-74566be51ab6)





## Appendix

1. [Data Source](#data-source)
2. [Technologies](#technologies)
3. [Skills](#skills)
4. [About the Dataset](#about-the-dataset)
5. [Initial Analysis Using Excel](#initial-analysis-using-excel)
6. [DAX Measures](#dax-measures)
7. [Main Page](#main-page)
8. [Regional Sales](#regional-sales)
9. [Customers](#customers)
10. [Conclusion](#conclusion)


## Data Source  
This project uses the "Automobile Sales data" dataset from kaggle  
https://www.kaggle.com/datasets/ddosad/auto-sales-data
## Technologies  
- Power BI
- Excel
- DAX 

## Skills
Data Analysis, Data Visualization, Data Cleaning, Excel, Pivot Tables, Pivot Charts, Excel Functions, Conditional Formatting, Power BI, DAX
## About the Dataset  
The dataset used in this project is a comprehensive collection of sales data from the automobile industry. It includes details about each order such as the order number, quantity ordered, price of each unit, sales, order date, and the status of the order.

In addition, the dataset also provides information about the product line, the manufacturer's suggested retail price (MSRP), and the product code.

On the customer side, the dataset includes the customer's name, phone number, address, city, postal code, and country. It also includes the name of the customer's contact person.

Lastly, the dataset categorizes the size of each deal, providing further insights into the nature of each transaction.  

## Initial Analysis Using Excel  
Utilizing Excel, Some initial data exploration and analysis was conducted. 

### Customer Stats  

![Excel GIF](https://github.com/user-attachments/assets/d14d5395-21cc-46fc-b843-ada25f73caa4)  

![Customer Stats](https://github.com/user-attachments/assets/481b61c4-49cf-49a8-9baf-baf7abbb4560)



Using this Excel Sheet, By pasting a Customer's Name at the designated cell You can see some quick statistics and information regarding them as :  
- Country of the Customer
- Total Revenue generated by the customer
- The Customer's Biggest Order in terms of Revenue
- The Product Line the Customer Ordered The most
- The Date of the Customer's Most Recent Order.

### Regional Stats  

![Regional Sales Excel](https://github.com/user-attachments/assets/8e3ea274-6c54-4f7f-acdf-d5ee0c5788ff) 


By Using The Pivot Tables and Pivot Charts features, It can be noted that **USA** is the country that generated the most Revenue and the most Number of Orders.
Further Analysis is possible by expanding any country in the table to show it's cities further diving into the details the data hold.  

### Order Status  

![Order Status Excel](https://github.com/user-attachments/assets/ebeba46f-b797-4309-bb6c-b9a646874624)


Creating a Table Using Excel Functions, It can be noted that **92%** of orders have been sucessfully shipped.
Conditional Formatting was used in the original sheet as well to mark the **Status** column improving it's readability.  

## DAX Measures  
DAX Measures were utilized to extract important information from the data to be used in Visuals.
1. **Top Country by Total Revenue**
   A measure to fetch the country with the Highest Total Revenue Generated.
   
   `Top Country by Total Revenue = 
VAR TopCountry = TOPN(1, VALUES('Auto Sales data'[COUNTRY]), CALCULATE(SUM('Auto Sales data'[SALES])), DESC)
RETURN CONCATENATEX(TopCountry, 'Auto Sales data'[COUNTRY], ", ")`

 2. **Top Customer by Orders**
    A measure to fetch the customer with the highest number of orders.
    
    `Top Customer by Orders = 
VAR TopCustomer = TOPN(1, VALUES('Auto Sales data'[CUSTOMERNAME]), CALCULATE(DISTINCTCOUNT('Auto Sales data'[ORDERNUMBER])), DESC)
RETURN CONCATENATEX(TopCustomer, 'Auto Sales data'[CUSTOMERNAME], ", ")`

3. **Top Customer for every Country by Revenue**
   A measure to fetch the top spending customer in every country.
   
   `Top Customer for every Country by Revenue = 
VAR TopCustomer = TOPN(1, VALUES('Auto Sales data'[CUSTOMERNAME]), CALCULATE(SUM('Auto Sales data'[SALES])), DESC)
RETURN CONCATENATEX(TopCustomer, 'Auto Sales data'[CUSTOMERNAME], ", ")`

5. **Top Customer's Revenue**
   A measure to calculate the Total Revenue generated by the top spending customer of every country previously determined.
   
   `Top Customer's Revenue = 
VAR TopCustomer = [Top Customer for every Country by Revenue]
RETURN
CALCULATE(
    SUM('Auto Sales data'[SALES]),
    FILTER(
        ALL('Auto Sales data'),
        'Auto Sales data'[CUSTOMERNAME] = TopCustomer && 'Auto Sales data'[COUNTRY] = SELECTEDVALUE('Auto Sales data'[COUNTRY])
    )
)`    

7. **Total Revenue per Customer**
   A measure to calculate the total revenue generated by every customer.
   
   `Total Revenue per Customer = 
CALCULATE(
	SUM('Auto Sales data'[SALES]),
	ALLSELECTED('Auto Sales data'[CUSTOMERNAME])
)`    

8. **Average Days Between Orders Per Customer Table**
   A table created using DAX that displays the average days between orders for every customer for every year.

   `Average Days Between Orders Per Customer = 
    SUMMARIZE(
        FILTER(
            'Auto Sales data',
            'Auto Sales data'[DaysBetweenOrders] > 0
        ),
        'Auto Sales data'[CUSTOMERNAME],
        'Auto Sales data'[ORDERDATE].[Year],
        "AvgDays", AVERAGE('Auto Sales data'[DaysBetweenOrders])
    )`  


## Main Page  

![Main Page GIF](https://github.com/user-attachments/assets/58e92265-4a6c-4cb0-885e-e1c4c9ee0e92)


This is the Main Page and the first thing you see when opening this report. It contains a summary of the main questions that could be asked and presents them in a simple concise manner.  
This page includes visuals that display:  
- The Total Income
- The Average Income Per Order
- Number of Orders
- Number of Customers
- Number of Automobiles Sold
- Number of Orders by Order Date
- Best Selling Products according to number of orders
- Top Spending Customer for Every Country

### Key Insights  
- Sales generated a Total Revenue of **$9.8M**.
- The Average Revenue Per Order is **$32.8K**.
- There has been a total of **298** orders.
- The company sold to **89** diffrent customers.
- A total of **96 Thousand** Automobiles have been sold.
- **November 2019** Was the month the company recieved the most number of orders.
- **Classic Cars** is the best selling product line with a total of **198** orders.
- **Euro Shopping Channel** is the highest spending customer in spain and the highest out of all customers with a total revenue of **$912,294**. While **Mini Gifts Distributors Ltd** is the top spending customer in the USA.

## Regional Sales 

![Regional Sales GIF](https://github.com/user-attachments/assets/926fb964-67b3-4906-b645-4162cd19e37d)  


The main goal of this page in the report is to analyze key statistics about sales at a **Regional Level**.  
The page includes the following visuals:  
- A Filled Map Displaying Total Revenue Per Country
- Each City and the Total Revenue generated from it.
- Each Prodcut Line and the Total Revenue Generated from it.
- The Total Revenue by Order Date.

  ### Key Insights
  -  The majority of orders are from the **USA** and it also generates the most revenue, with the most revenue generated through **San Rafael**.
  -  **Madrid** is the city with the most orders at **31** orders.
  -  It is apperant again that **Classic Cars** is the most dominant Product Line generating the most revenue and having the most orders almost everywhere.
  -  The Total Revenue Peaked at **November 2019** with one of the main factors being a noteable increase in sales in **France** and **Australia**.

## Customers  

![Customers GIF](https://github.com/user-attachments/assets/ee205964-63bc-4b1d-96b3-33ebebe45ce6)  



 This page aims to help identify the top customers that the company should focus on and key statistics regarding them.  
 You can filter by Custtomer Name or by a specific year to further breakdown the data using the two slicers at the upper left corner.  
 The page includes the following visuals:  
 - Number of Orders by Order Date
 - A Scatter Plot Showing Customers according to their Average Number of Days Between Orders (representing the frequency by wich the customer orders) and their Average Revenue Per Order.
 - A Pie Chart Showing the Number of Orders by Product Line
 - A Stacked Bar Chart Showing the Top 10 Customers with The Most Number of Orders

   ### Key Insights
   - The customer with the most orders is 'Euro Shopping Channel'.
   - Customers Located at the Bottom Right Quadrant of the Scatter Plot like **Muscle Machine Inc** , **Land of Toys Inc** , **Australian Collectors, Co** and others represent an important segment of customers that order frequently and make relativley high revenue orders.
   - During the Number of Orders and Total Revenue Peak at **November 2019**, **Australian Collectors, Co** and **Mini Gifts Distributors Ltd** had the most number of orders.
   - **Boards & Toys Co.** are outliers ordering every **904 Days** and having a low Average Order Revenue of **$4,565**. That being said they only made 2 orders so a small sample size might be the reason.
  
## Conclusion  
In conclusion, this project successfully utilizes Power BI and Excel to provide a comprehensive view of key sales data, customer behavior, and regional performance in the automobile industry. Through detailed analysis, we gained valuable insights, such as identifying top customers, high-performing product lines, and peak sales periods. This analysis highlights the dominance of the USA in total revenue, the popularity of the Classic Cars product line, and peak sales during November 2019. The report’s dashboards and visuals enable strategic decision-making by pinpointing significant trends and opportunities for revenue growth, optimizing customer focus, and refining sales strategies.
     


 
 

 
    


  
  
  
  
