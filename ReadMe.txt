NorthWind Trader project is Power Bi reporting project in which I showed insight deduction from raw data.
The dataset was provided by mavenanalytics for their monthly challenge.
The dataset consists of seven tables namely:
Categories
Customers
Employees
Orderdetails
Orders
Although the data came readily cleaned, some modifications still needed to be done to make the dataset satisfactory.
For example, In order to be able to model the tables as a star-schema, it was necessary to merge the two fact tables namely: 
orders and orderdetails tables. Thetime was removed from the date and discarded because the were all 00:00:00, not very useful.
The date were also separated into the day,month, year columns to enable creation of hierarchy in the form of year->quarter->month->day.
This also allowed the creation of quarter and month number that is used for sorting month of the year in the correct order.
measures 
ETL Procedures
The dataset came as xlsx files that contains tables for each dimension and fact tables. The dataset consist of 6 dimension tables and 2 fact tables.
They were download a zipped file from mavenanalytics, unzipped inside a folder and loaded to powerquery for further tansformation.

Modelling
The dimension table did not contain duplicates and were readily good for one-to-many relationships. To make modelling a star-schema possible, the orderdetails table was merged with the orders table
and loading of the former to the data model was disabled. A date table was also created and marked as date table to be used for time intelligent calculations.
The remaining six dimensions were linked to the orders with one-to-many relationships to form a star schema. Because there was no need for refresh, the import option was used.
Foreign keys were hidden in the fact table to conform with industry best practices.

Measures
Measures were extensively used where possible and calculated columns were avoided as much as possible to minimise the size of the models in memory.
Total Revenue = SUM(orders[Revenue])
This calculates the total revenue for an order.

Overall Revenue = CALCULATE([Total Revenue],ALL(orders))
This calculates the total revenue for all order without any filter whatsoever.

Total Selected Revenue = CALCULATE( [Total Revenue], ALLSELECTED(orders))
This calculates the total revenue for a group of dimensions of interest e.g customers or products

Percentage Selected Revenue = DIVIDE([Total Revenue],[Total Selected Revenue],0)
This calculates the percentage of the overall revenue represented by the total revenue.

Month on Month = CALCULATE([Total Revenue],PARALLELPERIOD('Date'[Date],-1,MONTH  ))
Calculates the revenue for the previous month. This allows a comparism with the month after.

Visuals

Table
The visual shows the all the months for which the business has been in operation and list the revenue for the previous month. The next column then calculates the percentage increase 
or decrease. If there was an increase, the percentage is coloured green, otherwise red.

Bar Chart
The first bar chart shows the first 8 customers of the business by revenue and the proportion of the revenue they represent of the eight.
On hovering on the bars, a tooltip show the first five products by revenue that the customer buys.

The next bar chart shows the top eight products by revenue and the proprtion of the revenue they generate.
Hovering on the bars also shows the top 5 customers buying the products.

Slicers
There are slices that filters for dimensions. For example, There are slicers for month, year, employee, shipper, country etc.
The slicer allows the report to be studied from varying point of view.

Cards
There are three cards in the report showing the proportion of revenue, orders, and shipping charges compared to the total for the selection. If no selection is made,
the card displays 100%.

This report allows NorthWind Traders to know the top customers and the products the buy in order to alway stock up those product.
It also allows NorthWind Traders to know who buys what more so they can decide the best location of the warehouse to store the product to reduce delivery time to their customers