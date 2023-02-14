# Data Engineering Capstone Project (SoftCart.com) 

## Introduction 
I will assume the role of an Associate Data Engineer who has recently joined an e-commerce organization, Softcart.com. I will be presented with a business challenge that requires building a data platform for retailer data analytics. 

Tasks to perform on organization data platform: 
-	Design a data platform that uses MySQL as an OLTP database and MongoDB as a NoSQL database
-	Design and implement a data warehouse and generate reports from the data 
-	Design a reporting dashboard that reflects the key metrics of the business 
-	Extract data from OLTP and NoSQL databases, transform it and load it into the data warehouse, and then create an ETL pipeline 
-	Create a Spark connection to the data warehouse, and then deploy a machine learning model 

This project is sectioned into 6 parts:
1. OLTP database 
2. MongoDB 
3. Data Warehouse Design, Setup, and Reporting 
4. Data Analytics Overview and Preparation 
5. ETL & Data Pipelines 
6. Big Data Analytics with Spark

## Module 1: OLTP Database

Tools/ Software: MySQL 8.0.22 , phpMyAdmin 5.0.4

- Design the OLTP database for an E-Commerce website, populate the OLTP Database with the data provided and automate the export of the daily incremental data into the data warehouse. 
- Design a data platforms that uses MySQL as an OLTP databases. You will be using MySQL to store the OLTP data. 

### 1.1: Design the OLTP database   
####  1.1.1: Create a database  
``` CREATE DATABASE _name_```   
<img src="https://imgur.com/ncx7DVb.png">

####  1.1.2: Design a table named sales_data  
``` CREATE TABLE _name_(columns1 data_type, columns2 data_type, columns3 data_type);```
<img src ="https://imgur.com/phLi05N.png">


### 1.2: Load the data  
#### 1.2.1: Import the data in the file oltpdata.csv  
import provided csv.file into table using phpMyAdmin  
<img src="https://imgur.com/f5jrp5q.png">
#### 1.2.2: List the tables in the database  
``` SHOW TABLES IN sales ;```  
<img src ="https://imgur.com/Bht5B8y.png">
#### 1.2.3: Write a query to find out the count of records in the tables sales_data  
``` select count(*) from table_name;```  
<img src ="https://imgur.com/i65xe7t.png">

### 1.3 Set up Admin Tasks  
#### 1.3.1: Create an index  
``` CREATE INDEX index_name ON table_name(column) ```  
<img src ="https://imgur.com/gyMA68C.png">


#### 1.3.2: List Indexes  
``` SHOW INDEXES FROM sales_data;```   
<img src ="https://imgur.com/6SZ6XOI.png">  
#### 1.3.3: Write a bash script to export data  
create a bash script and using ```mysqldump``` command to export data 

## Module 2: NoSQL databases
- design a data platform that uses MongDB as a NoSQL database and use it to store the e-commerce catalog data. 
- set up a NoSQL database to store the catalog data for an E-Commerce website, load the E-Commerce catalog data into the NoSQL database, and query the E-Commerce catalog data in the NoSQL database.   
Tools/Software: MongoDB Server, MongoDB Command Line Backup Tools 

### 2.1 Working with MongoDB  
##### 2.1.1 Import 'catalog.json' into mongodb server in a database named 'catalog' and collection named 'eletronics'  
##### 2.1.2 List out all the databases  
##### 2.1.3 List out all the collections in the database  
##### 2.1.4 Create an index on the field  
##### 2.1.5 Write a query to find the count of laptops   
##### 2.1.6 Write a query to find the number of smartphone with screen size of 6 inches   
##### 2.1.7 Export the 3 fields from the 'electronics' collection into a file named eletronics.csv. 

## Module 3 Part 1: Data Warehousing

Tools/Software: ERD Design Tool of pgAdmin , PostgreSQL Database Server

- design the schema for a data warehouse based on the schema 
of the OLTP and NoSQL databases. You’ll then create the schema and load the data into fact and dimension tables, automate the daily incremental data insertion into the data warehouse, and create Cubes and Rollups to make the reporting easier.

### 3.1: Design a Data Warehouse  
#### 3.1.1: Design the dimension table softcartDimDate 
#### 3.1.2: Design the dimension table softcartDimCategory
#### 3.1.3: Design the dimension table softcartDimItem
#### 3.1.4: Design the dimension table softcartDimCountry
#### 3.1.5: Design the fact table softcartFactSales 
#### 3.1.6: Design the relationships

### 3.2: Create the schema
#### 3.2.1: Create the schema

## Module 3 Part 2: Data Warehousing


## Module 4: 
you will create a Cognos data source that points to a data warehouse table, 
create a bar chart of Quarterly sales of cell phones, create a pie chart of sales of electronic 
goods by category, and create a line chart of total sales per month for the year 2020. 


## Module 5:
you will extract data from OLTP, NoSQL, and MongoDB databases into CSV format. 
You will then transform the OLTP data to suit the data warehouse schema and then load 
the transformed data into the data warehouse. Finally, you will verify that the data is loaded properly


## Module 6:
, you will use your skills in Big Data Analytics to create 
a Spark connection to the data warehouse, and then deploy a machine learning model on 
SparkML for making sales projections







