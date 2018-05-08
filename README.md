
# Ride Sharing Application
Millions of rides are taken every year in United states and most of the solutions that were extensively used till recently including New York yellow taxi mainly served single ride. This is inefficient considering how many passengers books single rides with source and destination that are close or on the way. The primary goal of this implementation is to efficiently combine rides arising from single prominent source and destinations which are close-by or on the way while experimenting with user score model which would encourage the passengers to invest in this system by providing them with rewards over time. Rewards would include priority in pooling, route selection and savings with respect to time and money.

### Dependecy and enviroment
#### Language
The entire project was implemented in Python 3.6 on Anaconda Platform using Jupyter Notebook. 
#### Libraries
Multiple libraries were used starting from initial preprocessing till obtaining the results. Listed below:
##### To access external data stored in database, file and external services.
* pymysql: Database Connector, enables python programs to talk to MySQL Server. 
*	 urllib: This module provides a high-level interface for fetching data across the World Wide Web, here to make calls to OSRM service. 
*	 csv: The csv module implements classes to read and write tabular data in CSV format. 
##### Routing and Pooling 
*	 bresenham: An implementation of Bresenham’s line drawing algorithm.
*	 scikit-learn:  Used sklearn.cluster.DBSCAN to implement the clustering. 
##### Data Processing 
*	 numpy: A fundamental package for computing supports N-dimensional array objects. 
*	 json: To support JSON (JavaScript Object Notation) is a lightweight data-interchange format
*	 datetime: Has classes for manipulating dates and times in both simple and complex ways.
*	 collections: Implements specialized container datatypes. 

#### Data
The data considered for this implemetetion was taken from NYC yellow cab data from feb 2016
https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2016-02.csv

#### SQL DB table creation query
    use rideshare;

	create table customer_table(
	customer_id int not null primary key auto_increment,
	user_rating float
	);

	create table taxi_data(
	trip_id int not null auto_increment primary key,
	customer_id int not null,
	ptime time,
	pdate date,
	dtime time,
	ddate date,
	pcount int,
	tripDistance float,
	plongitude float8,
	platitude float8,
	dlongitude float8,
	dlatitude float8,
	fare float8,
	FOREIGN KEY fk_cust_id(customer_id)
	REFERENCES customer_table(customer_id)
	ON UPDATE CASCADE
	ON DELETE RESTRICT
	);

	create table new_taxi_data(
	trip_id int not null  primary key,
	customer_id int not null,
	pool_id int not null,
	ptime time,
	pdate date,
	dtime time,
	ddate date,
	pcount int,
	tripDistance float,
	dlongitude float8,
	dlatitude float8,
	saving float8,
	fare float8,
	FOREIGN KEY fk_cust_id(customer_id)
	REFERENCES customer_table(customer_id)
	ON UPDATE CASCADE
	);

	CREATE TABLE `rideshare`.`customer_preference` (
	  `customer_id` INT NOT NULL,
	  `booking_id` INT NULL,
	  `delay` INT NULL,
	  `save_money_yn` VARCHAR(1) NULL,
	  `save_time_yn` VARCHAR(1) NULL );

## Execution
1. Create sql DB and run the above mentioned SQL command
2. Assuming Python 3.6, Anacond are installed open jupyter notebook
3.  Run CSVtoBD.ipynb in sequence
4. Run PoolingandRouting.ipynb in sequence
