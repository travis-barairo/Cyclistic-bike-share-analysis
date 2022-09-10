# Cyclistic-bike-share-analysis
## Google Data Certification Capstone Project: Analyzing 1 Year of Trip Data  

### Business Task:
Cyclistic, a bike sharing company is looking to maximize the number of annual members that are signed up for their membership program. In order to accomplish this, Moreno and executive stakeholders need to understand the differences between casual riders and annual members.  

### Questions to answer:
* Principle question: What are the differences between casual riders and members?
  + Sub Question 1: Between casuals and members, how long do the rides usually last (in minutes)?
  + Sub Question 2: How far do casual users travel in comparison to members (in miles)?
  + Sub Question 3: What type of bikes do casual users prefer compared to members?

### Data Sourcing:
In order to see how I sourced my data please click and follow this [link](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/data_source.md) to find the library I pulled the CSV files from and how to set them up in the same way I did.  

### Data Structure:
Within the CSV files, all of the data was organized into several columns as follows:
* ride_id ; string
* rideable_type ; string
* started_at ; Datetime
* start_station_name ; string
* start_station_id ; string
* end_station_name ; string
* end_station_id ; string
* start_lat ; float
* start_lng ; float
* end_lat ; float
* end_lng ; float
* member_casual ; string

### Data Cleaning:

##### Processing Plan:
Before analysis can begin, I had to ensure that the data was cleaned and organized before I could start transforming it. In order to achieve this, I had a six step plan. First, I would combine all 12 csv files into one data frame. Next, I would change any null values in float columns to zero to prevent any errors from occuring in calculations later. Once the data was cleaned, I would aggregate the data into new calculated columns. Once the columns were finished and calulated, I would have to export the final data frame into a csv whereby I can upload it to Tableau and perform some visualization of the data. Lastly I would use tableau to generate visualization that will support and drive my findings.  

##### Documentation of cleaning data
1. The first task to tackle was to combine all 12 months of data into a single data frame in python.
