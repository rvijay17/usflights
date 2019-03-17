# US Flight Data
## 01 Data Cleansing
This Python notebook cleanses the data, chooses appropriate data types and performs conversions to fit into PostgreSQL data type. For example, ARRTIME and DEPUTISE were in the format _nnnn_ which had to be converted to the format _nn:nn:00_ so that it could be saved as **time** datatype.
The resulting data frame is stored in the disk as a parquet file format.

## 02 Data Loading
The parquet file is read and then loaded into PostgreSQL database. The schema has two dimension tables and one fact table.

![](star.png)


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

## Issues with the dataset
* Missing Arrival Date - Although ARRTIME, DEPTIME and FLIGHTDATE are in the datafile, it could have been great if Arrival date was also there. We can assume that if Arrival Time (say 21:00) is greater than Departure time (say 16:00), it is a same day flight. If Arrival Time (say 11:00) is less than Departure time (23:00), we can assume that the flight arrived at the destination the next day. We’ll have issues if we have flights greater than 24 hours.