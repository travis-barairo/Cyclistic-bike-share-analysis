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

5. Before I started working on the visualization I simply converted the data frame into a csv using pandas to_csv method. This file would be what I would upload into tableau to help create a new visualization.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis5.JPG)
*please note: I hashed out data_3.to_csv('final_divvy_tripdata_20220829.csv') because I had run this script a few times and every time I opened it on VSC it would continuously make new files which would take a long time.*

6. Once the final CSV was created, I wanted to also take a look at some pivot tables and averages for the data before I went into Tableau and started creating a visualization. To answer the first subquestion, I took a look at the data grouped by member type compared to the mean final travel time.
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis6.JPG)
  With this pivot table in place we can see that on average, casual members have a longer travel time.

7. Nextly taking a quick look at the data grouped by member type and using the mean travel distance we get a similar result:
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis7.JPG) 

  As expected, since the travel time is, on average, longer for casual users than members we can expect the distance for the trip to be overall larger as well.

8. Lastly, before jumping into visualizing, we needed to see the bike preferences of each member category. Grouping the data by bike_type and member_type, then taking the count of member_type we return a pivot that looks like this:
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Analysis8.JPG)

  From this we can see a few things. The amount of casual riders who use classic bikes lower than the amount of membership users using the classic bikes. Additionally we see that membership users dont ride docked bikes except for one trip within the 12 months of data we are looking at. With all these tables contextualized we can move forward to visualizing the data to see whether or not our assumptions are supported or not.

### Data Visualization
##### The [dashboard](https://public.tableau.com/app/profile/travis.miguel.barairo/viz/divvy_trip_data_final/Dashboard1) I created on Tableau public summarizes all the visualizations I created for this project, but keep reading to take a one by one look at each metric.

##### Sub Question 1: Between casuals and members, how long do the rides usually last (in minutes)?

![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Vis1.JPG)

After uploading the data into tableau I plotted the average travel time in minutes against the type of bike used, grouped by member type. As a result you can see that across the board, casual members are users who take longer timed trips on average than membership users. Additionally the preference for docked bikes becomes more apparent for casual users when compared to members.
* Key Insights
  + **For a trip using a classic bike, we can expect casual users to spend two times as long travelling than members**
  + For a trip using a docked bike, we can assume that only casual members prefer it due to the fact that those in the members category who used the docked bike only accounted for one data point.
  + For a trip using an electrical bike, we can predict that the difference in time travelled would be marginal but slightly higher for casuals.

##### Sub Question 2: How far do casual users travel in comparison to members (in miles)?

Similarly to the previous sub question, I uploaded the data and grouped by bike type and as well as member type. Here is the chart:
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Vis2.JPG)

As one can see there are a few key points to be mentioned here:
* Key Insights
  + Overall casual users travel further distances than the membership users. This makes sense due to their average overall time being higher. Longer the distance longer the time.
  + Using the previous sub questions numbers, we can see an interesting phenomenon whereby the casual members who ride on a classic bike travel a farther distance in a shorter amount of time than those casual users who ride on a docked bike.
  + **To delve further to this point I decided to compare the ratio of average time to average distance between not only casuals and members but to compare them within their own member types grouped by their choice of bike.**

![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Vis3a.JPG)

Comparing the casual points (yellow), from this chart we can see a few Key Insights:
* classic bike casual users travel at a rate of 0.551 miles per hour whereas the docked bike casual users travel at a rate of 0.082 mph.
  + This indicates to us that classic bike casual members are more athletic and proficient in riding the bike
  + This could mean that classic casual users are avid bikers, whereas casual users using docked bikes and electric bikes are using them more for commuting/getting from point A to B without any regard for fitness.
* electric bike casual users and docked bike casual users have similar speeds sitting at a range of 0.08 - 0.1 mph.

Additionally comparing casual (yellow) and membership (purple) users' speeds indicates to us that:
* Overall, membership users are more avid bike riders who can go faster than the casual user.

##### Sub Question 3: What type of bikes do casual users prefer compared to members?


Converting the pivot table shown in python to a tableau visualization produces an interesting result. By using the count of bike types selected by trip and grouping them bey the member type we generate a visualization like this:
![](https://github.com/travis-barairo/Cyclistic-bike-share-analysis/blob/main/images/Vis3b.JPG)

At first glance the chart may look strange, but there are a few key notes to look at:
* Looking at the docked bike type we can see that the majority of trip data in this data set that used a docked bike was primarily a casual member.
  + This supports our previous finding that the casual docked bike user may be someone more focused on commuting to and from placed due to the fact that docked bikes must be picked up and returned to the stations. We can then assume that these users are commuting from station to a station near their destination thus further backing up this idea that they aren't die hard bikers, but rather just your average commuter.
* When comparing the docked bike members to the electric bike members we want to figure out the best way to influence electric bike users to switch to a membership.
  + From the previous chart we know that docked bike and electric bike casual users are most likely people who use the platform to commute to destinations. The distinguishing factor between these two categories is that docked bikes must be returned to a set station, whereas electric bikes can be picked up anywhere that's nearby and dropped off wherever the user decides. This means that those who use electric bikes to commute from the casual users group prefer the flexibility of pick-up and drop-off.



