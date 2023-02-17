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
``` mongoimport -u root -p xxxxxx --authenticationDatabase admin -db xxx --collection xxx -- file xxx.json```  
##### 2.1.2 List out all the databases  
``` show dbs```  
##### 2.1.3 List out all the collections in the database  
``` show collections ```  
##### 2.1.4 Create an index on the field  
``` db.collection.CreateIndex({"field:1}) ```  
##### 2.1.5 Write a query to find the count of laptops   
``` db.collection.count({type:"laptop"})```  
##### 2.1.6 Write a query to find the number of smartphone with screen size of 6 inches   
##### 2.1.7 Export the 3 fields from the 'electronics' collection into a file named eletronics.csv. 

## Module 3 Part 1: Data Warehousing Reporting

Tools/Software: ERD Design Tool of pgAdmin , PostgreSQL Database Server

- design the schema for a data warehouse based on the schema  of the OLTP and NoSQL databases. You’ll then create the schema and load the data into fact and dimension tables, automate the daily incremental data insertion into the data warehouse, and create Cubes and Rollups to make the reporting easier.

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
### 3.1: Prepare the lab environment  

### 3.2: Loading Data
#### 3.2.1: Load data into the dimension table DimDate  
#### 3.2.2: Load data into the dimension table DimCategory  
#### 3.2.3: Load data into the dimension table DimCountry
#### 3.2.4: Load data into the fact table FactSales  

### 3.3: Queries for data analytics 
#### 3.3.1: Create a grouping sets query  
<img src="https://imgur.com/RgPo2H8.png">  
#### 3.3.2: Create a rollup query  
<img src ="https://imgur.com/xMrnf82.png">  
#### 3.3.3: Create a cube query  
<img src ="https://imgur.com/cA4WFQ1.png">  
#### 3.3.4: Create an MQT  
<img src ="https://imgur.com/UIt1Hts.png">  

## Module 4: Data Analytics (Cognos Analytics)
you will create a Cognos data source that points to a data warehouse table, 
create a bar chart of Quarterly sales of cell phones, create a pie chart of sales of electronic 
goods by category, and create a line chart of total sales per month for the year 2020.  

### 4.1: Load data into data warehouse 
#### 4.1.1: Import Data 
#### 4.1.2: List top 10 rows  

### 4.2: Create data source in Cognos
#### 4.2.1: create a data source in Cognos that points to the table in your IBM DB2 database 

### 4.3: Create dashboard  
#### 4.3.1: Create a line chart
#### 4.3.2: Create a pie chart
#### 4.3.3: Create a bar chart

## Module 5: ETL & Data Pipelines
tools/software: MySQL Server, IBM DB2 database running on IBM Cloud 

you will extract data from OLTP, NoSQL, and MongoDB databases into CSV format. 
You will then transform the OLTP data to suit the data warehouse schema and then load 
the transformed data into the data warehouse. Finally, you will verify that the data is loaded properly
##
you need to keep data synchronized between different databases/data warehouses as a part of your daily routine. One task that is routinely performed is the sync up of staging data warehouse and production data warehouse. Automating this sync up will save you a lot of time and standardize your process.
##
you will be given a set of python scripts to start with. You will use/modify them to perform the incremental data load from MySQL server which acts as a staging warehouse to the IBM DB2 which is a production data warehouse. This script will be scheduled by the DE to sync up the data between the staging and production data warehouse. 

##  5.1: ETL 
### 5.1.1 : Set up Staging Data Warehouse (MySQL) and load the file ```sales.sql``` into the sales database. 
#### Step 1: Start MySQL server using linux terminal and create a database named ```sales```
#### Step 2: Import the data in the file ```sales.sql``` into ```sales``` database  
#### Step 3: Python and make sure youre able to connect to the MySQL server instance on the Theia Environment  
##  
### 5.2: Set up Production Data Warehouse (IBM Db2)
#### 5.2.1: how to connect to the cloud instance of IBM DB2 using Python. 
##
### 5.3: Automate loading of incremental data into the data warehouse 

## 5.2: Data Pipelines Using Apache Airflow  
tools/software: Apache Airflow, python 

Write a pipeline that analyzes the web server log file, extracts that required lines(ending with html) and fields(time stamp, size) and transforms (bytes to mb) and load (append to an exisiting file).

### 5.2.1: Prepare the Environment 

### 5.2.2: Create a DAG  
#### 5.2.2.1: Define the DAG arguments
<img src=".png">  

#### 5.2.2.2: Define the DAG   
<img src=".png">    
#### 5.2.2.3: Create a task to extract data , transform the data in the txt file  ,load the data   
<img src=".png">   
#### 5.2.2.6: Define the task pipeline   
<img src =".png">   

### 5.2.3: Getting the DAG operational 
#### 5.2.3.1: Submit the DAG
#### 5.2.3.2: Unpause the DAG
#### 5.2.3.3: Monitor the DAG

## Module 6:
Use your skills in Big Data Analytics to create a Spark connection to the data warehouse, and then deploy a machine learning model on SparkML for making sales projections







