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
1. a OLTP database 
2.  MongoDB 
3. Data Warehouse Design, Setup, and Reporting 
4.  Data Analytics Overview and Preparation 
5. ETL & Data Pipelines 
6.  Big Data Analytics with Spark

## Module 1: OLTP Database

Tools/ Software: MySQL 8.0.22 , phpMyAdmin 5.0.4

- Design the OLTP database for an E-Commerce website, populate the OLTP Database with the data provided and automate the export of the daily incremental data into the data warehouse. 
- Design a data platforms that uses MySQL as an OLTP databases. You will be using MySQL to store the OLTP data. 

### 1.1 Design the OLTP database
#####  1.1.1 create a database
#####  1.1.2 design a table named sales_data

### 1.2 Load the data
##### 1.2.1 Import the data in the file oltpdata.csv
##### 1.2.2 List the tables in the database
##### 1.2.3  Write a query to find out the count of records in the tables sales_data

### 1.3 Set up Admin Tasks 
##### 1.3.1 Create an index 
##### 1.3.2 List Indexes 
##### 1.3.3 Write a bash script to export data 

## Module 2: NoSQL databases

Tools/Software: MongoDB Server, MongoDB Command Line Backup Tools 

- design a data platform that uses MongDB as a NoSQL database and use it to store the e-commerce catalog data. 
-set up a NoSQL database to store the catalog data for an E-Commerce website, load the E-Commerce catalog data into the NoSQL database, and query the E-Commerce catalog data in the NoSQL database. 


### 2.1 Working with MongoDB
##### 2.1.1 Import 'catalog.json' into mongodb server in a database named 'catalog' and collection named 'eletronics
##### 2.1.2 List out all the databases 
##### 2.1.3 List out all the collections in the database 
##### 2.1.4 Create an index on the field 
##### 2.1.5 Write a query to find the count of laptops 
##### 2.1.6 Write a query to find the number of smartphone with screen size of 6 inches 
##### 2.1.7 Export the 3 fields from the 'electronics' collection into a file named eletronics.csv. 



