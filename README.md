# Building a Data Platform for an E-Commerce Company (SoftCart.com) 

## Introduction 

As part of *IBM Data Engineering Capstone Project*, I will assume as an Associate Data Engineer who has recently joined e-commerce organzation, to build data platform for retailer data analytics. 

To implement a data warehouse system into a business, I then have to complete builiding the following five parts in the diagram below. 
<img src="https://imgur.com/KYh4fIU.png">

The Process of Building a Data Plaform
- Part A - Establish ```Data Staging Area``` for temporary storing data from data source
- Part B - Build a ```Staging Data Warehouse``` to aggregate disparate source data into a cohensive one before loading data into production data warehouse 
- Part C - Design a ```Sales Reporting Dashboard``` that reflects the key metrics of business 
- Part D - ```Synchronize data``` between staging and production warehouse by automate incremental loading process of sales data 
- Part E - Develop a ```ETL pipeline``` that analyzes the web server log file, extracts the required lines and fields, transforms and loads into a file for further analysis

This project is sectioned into 6 parts:
1. ```OLTP database``` - Design a data platform that uses MySQL as an OLTP database and MongoDB as a NoSQL database
2. ```MongoDB``` 
3. ```Data Warehouse Design, Setup, and Reporting``` - Design and implement a data warehouse and generate reports from the data 
4. ```Data Analytics Overview and Preparation``` - Design a reporting dashboard that reflects the key metrics of the business
5. ```ETL & Data Pipelines``` - Extract data from OLTP and NoSQL databases, transform it and load it into the data warehouse, and then create an ETL pipeline
6. ```Big Data Analytics with Spark``` - Create a Spark connection to the data warehouse, and then deploy a machine learning model


# Part A : Designing Data Staging Areas ( MySQL + MongoDB )

### A1: OLTP Database
```Tools/ Software: MySQL 8.0.22 , phpMyAdmin 5.0.4``` 
- Design the OLTP database for an E-Commerce website, populate the OLTP Database with the data provided and automate the export of the daily incremental data into the data warehouse. 
+ Design a data platforms that uses MySQL as an OLTP databases. You will be using MySQL to store the OLTP data. 

#### 1) ```Design OLTP database in MySQL Server ```  
##### 1.1) Create a database & design a table named sales_data  
 >```INPUT:``` *CREATE DATABASE _name_*    

<img src="https://imgur.com/ncx7DVb.png">

##### 1.2) Design a table named sales_data  
> ```INPUT:``` *CREATE TABLE _name_(columns1 data_type, columns2 data_type, columns3 data_type);*

<img src ="https://imgur.com/phLi05N.png" title="hunnn" >   

#### 2)```Loading data into MySQL database using phpMyAdmin```
##### 2.1) Import the data in the file oltpdata.csv   
> loading csv.files into database using phpMyAdmin  
<img src="https://imgur.com/f5jrp5q.png" width = 600 height =300>

##### 2.2) List the tables in the database  
> ```INPUT:``` *SHOW TABLES IN sales ;*
<img src ="https://imgur.com/Bht5B8y.png">

##### 2.3) Write a query to find out the count of records in the tables sales_data  
> ```INPUT:``` *select count(*) from table_name;* 
<img src ="https://imgur.com/i65xe7t.png">

#### 3) ```Set up Admin Tasks``` 
##### 3.1) Create an index  
> ```INPUT:``` *CREATE INDEX index_name ON table_name(column);*
<img src ="https://imgur.com/gyMA68C.png">

##### 3.2) List Indexes  
> ```INPUT:``` *SHOW INDEXES FROM sales_data;*   
<img src ="https://imgur.com/6SZ6XOI.png">     

##### 1.3.3) Write a bash script to export data  
> create a bash script and using ```mysqldump``` command to export data 


### A2: NoSQL database     
- design a data platform that uses MongDB as a NoSQL database and use it to store the e-commerce catalog data. 
+ set up a NoSQL database to store the catalog data for an E-Commerce website, load the E-Commerce catalog data into the NoSQL database, and query the E-Commerce catalog data in the NoSQL database.   
```Tools/Software: MongoDB Server, MongoDB Command Line Backup Tools ```

#### 1) ```Working with MongoDB```  
##### 1.1) prepare the environment in linux terminal 
> ```INPUT:``` *start mongo db*
<img src="https://imgur.com/bXcP5jD.png">

##### 1.2) Import 'catalog.json' into mongodb server in a database named 'catalog' and collection named 'eletronics'  
> ```INPUT:``` * mongoimport -u root -p xxxxxx --authenticationDatabase admin -db xxx --collection xxx -- file xxx.json* 

<img src="https://imgur.com/llrHOB3.png">

##### 1.3) List out all the databases  
> ```INPUT:``` *show dbs* 

<img src="https://imgur.com/akrRTR8.png">

##### 1.4) List out all the collections in the database  
> ```INPUT:``` *show collections*

<img src="https://imgur.com/peGOmN4.png">

##### 1.5) Create an index on the field  
> ```INPUT:``` *db.collection.CreateIndex({"field:1})*

<img src="https://imgur.com/3CSz1xk.png">

##### 1.6) Write a query to find the count of laptops   
> ```INPUT:``` *db.collection.count({type:"laptop"})* 

<img src="https://imgur.com/TYXKDGW.png">

##### 1.7) Export the 3 fields from the 'electronics' collection into a file named eletronics.csv
> ```INPUT:``` *mongoexport -u root -p --authentionDatabase admin --db catalog --collection electronics -- out electronic.csv*
<img src="https://imgur.com/GejdghR.png">

# Part B: Build Staging Data Warehouse for Reporting Dashboard ( PostgreSQL )

```Tools/Software: ERD Design Tool of pgAdmin , PostgreSQL Database Server```

+ design the schema for a data warehouse based on the schema  of the OLTP and NoSQL databases. You’ll then create the schema and load the data into fact and dimension tables, automate the daily incremental data insertion into the data warehouse, and create Cubes and Rollups to make the reporting easier

### B1) ```Design a Reporting Data Warehouse using ERD design tool ```  
#### 1.1) Design the relationships of fact table(SoftcartFactSales) and dimension tables(DimDate, DimCategory, DimItem, DimCountry)
<img src="https://imgur.com/xpt6rNG.png" height ="450" width ="600">

#### 1.2) ```Create Schema```    
<img src="https://imgur.com/wFuBfkN.png" height ="450" width ="600">

### B2) Generate Report 

```Tools/software: PostgreSQL UI```

#### 1) ```Loading Data via PostgreSQL UI```
##### 1.1) Load data into the dimension table DimDate, table DimCategory, table DimCountry
<img src="https://imgur.com/ZBYEzm6.png" height ="450" width ="600" >   

##### 1.2) Load data into FactSales table 
<img src ="https://imgur.com/TMjqOC1.png" height ="450" width ="600" >  

#### 2) ```Queries for Data Analytics ```    
##### 2.1) Create a Grouping sets query 
```sql 
select c.country, a.category, sum(f.amount) as total sales
from public."FactSales" f 
left join public."DimCountry" c on f.countryid = c.countryid 
left join public."DimCategory" a on a.categoryid = f.categoryid
group by grouping sets (a.category, c.country)
```
<img src="https://imgur.com/RgPo2H8.png" height ="450" width ="600">  

##### 2.1) Create a Rollup query 
```sql
SELECT c.country, a.year, sum(f.amount) as totalsales
from public."FactSales" f
left join public."DimCountry" c on f.countryid = c.countryid
left join public."DimDate" a on a.dateid = f.dateid
group by roll up (a.year, c.country):
```
<img src ="https://imgur.com/xMrnf82.png" height ="450" width ="600">  

##### 2.2) Create a Cube query
```sql 
SELECT c.country, a.year, avg(f.amount) as average_sales
from public."FactSales" f
left join public."DimCountry" c on f.country.id = c.countryid
left join pubic."DimDate" a on a.dateid = f.dateid
group by cube (a.year, c.country);
```    
<img src ="https://imgur.com/cA4WFQ1.png" height ="450" width ="600" >   

##### 2.3) Create an MQT  
```sql 
create table total_sales_per_country as (SELECT c.country, sum(f.amount) as total_sales
from public."FactSales" f
left join public."DimCountry" c on f.countryid = c.countryid
group by country 
order by country asc;
```
<img src ="https://imgur.com/UIt1Hts.png" height ="450" width ="600">  

# Part C : Design a ```Sales Reporting Dashboard``` that reflects the key metrics of business 

### C1) Data Analytics (Cognos Analytics)
- you will create a Cognos data source that points to a data warehouse table, 
+ create a bar chart of Quarterly sales of cell phones, create a pie chart of sales of electronic, goods by category, and create a line chart of total sales per month for the year 2020.  
 
#### 1) ```Load data into Data Warehouse```
##### 1.1) Import Data 
<img src ="https://imgur.com/3bf4WX5.png">

##### 1.2: List top 10 rows  
 <img src="https://imgur.com/pAQPAUT.png">

#### 2) ```Create Dashboard```  
##### 2.1) Create a line chart
<img src="https://imgur.com/vULM9xJ.png">    

##### 2.2) Create a pie chart   
<img src="https://imgur.com/1igjVov.png">    

##### 2.3) Create a bar chart
<img src ="https://imgur.com/XUn1gdz.png">


# Part D : ```Synchronize data``` between staging and production warehouse by automate incremental loading process of sales data 

### D1. Sync up between staging and production data warehouse
```tools/software: MySQL Server, IBM DB2 database running on IBM Cloud ```

you will extract data from OLTP, NoSQL, and MongoDB databases into CSV format. 
You will then transform the OLTP data to suit the data warehouse schema and then load the transformed data into the data warehouse. Finally, you will verify that the data is loaded properly.

you need to keep data synchronized between different databases/data warehouses as a part of your daily routine. One task that is routinely performed is the sync up of staging data warehouse and production data warehouse. Automating this sync up will save you a lot of time and standardize your process.
you will be given a set of python scripts to start with. You will use/modify them to perform the incremental data load from MySQL server which acts as a staging warehouse to the IBM DB2 which is a production data warehouse. This script will be scheduled by the DE to sync up the data between the staging and production data warehouse. 

#### 1) Set up Staging Data Warehouse (MySQL) and load the file ```sales.sql``` into the sales database. 

##### Step 1: Start MySQL server using linux terminal and create a database named ```sales```   
Use ```start_mysql``` to connect MySQL server and ``` create database name``` to create a db as staging area before loading into production data warehouse.   
<img src="https://imgur.com/dTHyB8O.png">

##### Step 2: Import the data in the file ```sales.sql``` into ```sales``` database    
Use ```source``` command to load the dataset into staging data warehouse(MySQL)   
<img src ="https://imgur.com/beOJade.png">

##### Step 3: Make sure your are able to connect to the MySQL server instance on the Theia Environment   
Use query statement to examine whether the data has loaded in MySQL server   
<img src = "https://imgur.com/8Nyu1Hy.png">

#### 2)  ```Set up Production Data Warehouse (IBM Db2)``` 
##### 2.1) Load csv file into production data warehouse using IBM DB2 UI   
<img src="https://imgur.com/y3MQeR0.png" height ="450" width ="800">  

##### 2.2) ```Automate loading of incremental data into the Data Warehouse```   
write a python script that automatically load additional values from staging warehouse(MySQL) that doesnt have in production warehouse(IBM DB2)

##### 2.3) Import necessary library and create connection for each database   
<img src="https://imgur.com/RBNG8WI.png" width ="800">  
<img src="https://imgur.com/DHUuVmc.png" width ="800"> 

##### 2.4) Load incremental data into production data warehouse by comparing the data from two different datawarehouse (Staging Data Warehouse vs Production Data Warehouse.   

In the following diagram, we find the last row of row_id in sales_data from production data warehouse and then load the rows that are greater than last_rowid from staging data warehouse into production data warehouse. The additional rows are the incremental data and we automate it using python script. After we have completed the process, we close the connection from both data warehouse.   

<img src="https://imgur.com/lKrhqTX.png">
<img src="https://imgur.com/w6qG5qk.png">


# Part E : Develop a ```ETL pipeline``` that analyzes the web server log file, extracts the required lines and fields, transforms and loads into a file for further analysis

### E) ```Data Pipelines Using Apache Airflow```      
```Tools/Technologise: Apache Airflow, Python``` 

- Write a pipeline that analyzes the web server log file, extracts that required lines(ending with html) and fields(time stamp, size) and transforms (bytes to mb) and load (append to an exisiting file).   

#### 1) Prepare the Environment 
type ```start_airflow``` onto linux terminal to start the Apache Airflow tools  
<img src ="https://imgur.com/7gYrQ3I.png">  

#### 2): Create a DAG  
##### 2.1)  Define the DAG arguments  
<img src="https://imgur.com/kC0ufNc.png">   

##### 2.2) Define the DAG  
<img src="https://imgur.com/Qz2Wxvn.png">  

##### 2.3) Create a task to extract data, transform the data in the txt file, load the data   
<img src="https://imgur.com/6iA5pTq.png">  

##### 2.4) Define the Task Pipeline    
<img src ="https://imgur.com/HQgZU2k.png">    

#### 3) Getting the DAG operational 
##### 3.1) Submit the DAG    
<img src ="https://imgur.com/aso0xxd.png">   

##### 3.2) Unpause the DAG      
<img src="https://imgur.com/EL7KBMP.png"> 

##### 3.3) Monitor the DAG     
<img src = "https://imgur.com/PW9nFIV.png">     

# Module 6:
Use your skills in Big Data Analytics to create a Spark connection to the data warehouse, and then deploy a machine learning model on SparkML for making sales projections







