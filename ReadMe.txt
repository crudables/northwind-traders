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
