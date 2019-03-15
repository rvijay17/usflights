# US Flight Data
## 01 Data Cleansing
This Python notebook cleanses the data, chooses appropriate data types and performs conversions to fit into PostgreSQL data type. For example, ARRTIME and DEPTIME were in the format _nnnn_ which had to be converted to the format _nn:nn:00_ so that it could be saved in **time** datatype.
The resulting data frame is stored in the disk as a parquet file format.

## 02 Data Loading
The parquet file is read and then loaded into PostgreSQL database. The schema has two dimension tables and one fact table.

![](&&&SFLOCALFILEPATH&&&star.png)


### DIM_AIRPORT
* airportcode
* airportname
* cityname
* statecode
* statename

### DIM_AIRLINE
* airlinecode
* airline name

### FACT_FLIGHT
* transactionid
* flightdate
* tailnum
* flightnum
* **airlinecode** (FK)
* **originairportcode** (FK)
* **destairportcode** (FK)
* crsdeptime
* deptime
* depdelay
* taxiout
* wheelsoff
* wheelson
* taxiin
* crsarrtime
* arrtime
* arrdelay
* crselapsedtime
* actualelapsedtime
* cancelled
* diverted
* distance
* distance_group
* depdelay_gt15

## 03 Data Analysis
This Jupyter notebook has some analysis. The data is imported from the same  parquet file exported in the 01 Data Cleansing notebook. Similar analysis could also be done using SQL.