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
* started_at ; string
* ended_at ; string
* start_station_name ; string
* start_station_id ; string
* end_station_name ; string
* end_station_id ; string
* start_lat ; float
* start_lng ; float
* end_lat ; float
* end_lng ; float
* member_casual ; string

### Data Cleaning/Analysis:

##### Processing Plan:
Before analysis can begin, I had to ensure that the data was cleaned and organized before I could start transforming it. In order to achieve this, I had a six step plan. First, I would combine all 12 csv files into one data frame. Next, I would change any null values in float columns to zero to prevent any errors from occuring in calculations later. Once the data was cleaned, I would aggregate the data into new calculated columns. Once the columns were finished and calulated, I would have to export the final data frame into a csv whereby I can upload it to Tableau and perform some visualization of the data. Lastly I would use tableau to generate visualization that will support and drive my findings.  

##### Documentation of cleaning data
1. The first task to tackle was to combine all 12 months of data into a single data frame in python. To do this we simply created a variable that lists all the files needed, and concatenated all the csv's read into a data frame, iterated over all the files within the list.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Clean1.JPG)

2. After combining all the csv's into one data frame, we then looked at the columns and determined that five of the columns won't be useful in this analysis. Once these columns were identified, all we had to do was simply drop the columns using the drop method.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Clean2.JPG)

3. Once all the uneeded columns were dropped, I renamed the usable columns to those which made more sense.
* rideable_type ; bike_type
* member_casual ; member_type
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Clean3.JPG)

4. Lastly, after our columns and workspace is set up, we identified prior to starting analysis that there were some N/A values in the loat and long columns which would interfere with our calculations later on. In order to fix this, we sumply used the fillna method to replace any na values with an integer value of zero.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Clean4.JPG)

##### Documentation of analyzing cleaned data
1. Once the data was cleaned, I proceeded to answer the first subquestion and began aggregating data into columns in which I could load the prepared final CSV into Tableau. To start off, I created a new calculated column "travel_time" which was the difference between the trip end time and start time. Additionally, I used the pandas method to_datetime to pass in the string values in these columns and convert them to a date time format.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis1.JPG)

2. After the total travel time was calculated, I then proceded to prepare some calculated columns for the second subquestion. In order to see how far each member type travelled we would need to determine the distance in miles between two points. Thankfully using the start and end latitudes and longitudes we can calculate the distance by using the [Distance between two points formula](https://byjus.com/maths/distance-between-two-points-formula/)
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis2.JPG)

3. Once I had the final distance calculated, I saved the data frame into a new data where I dropped the unnecessary calculated columns as a result of our calculations in the previous step.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis3.JPG)

4. Now that everything was starting to fall in place for the next step, the visualization process, I had some final casts that I needed to make for the data to play nicely with Tableau. Within the travel_time column, the data type in this column was a datetime. Since I would be exporting this final csv to Tableau, I know that I would have troubles aggregating this column unless I did a data type recasting. using the numpy method of timedelta64, I casted the travel_time data from a datetime to a float value.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis4.JPG)

