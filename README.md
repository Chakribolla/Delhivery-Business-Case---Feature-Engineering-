# Delhivery-Business-Case---Feature-Engineering-

# About Delhivery

Delhivery is the largest and fastest-growing fully integrated player in India by revenue in Fiscal 2021. They aim to build the operating system for commerce, through a combination of world-class infrastructure, logistics operations of the highest quality, and cutting-edge engineering and technology capabilities.

The Data team builds intelligence and capabilities using this data that helps them to widen the gap between the quality, efficiency, and profitability of their business versus their competitors.

How can you help here?

The company wants to understand and process the data coming out of data engineering pipelines:

• Clean, sanitize and manipulate data to get useful features out of raw fields

• Make sense out of the raw data and help the data science team to build forecasting models on it

# Dataset

data - tells whether the data is testing or training data
trip_creation_time – Timestamp of trip creation
route_schedule_uuid – Unique Id for a particular route schedule
route_type – Transportation type
FTL – Full Truck Load: FTL shipments get to the destination sooner, as the truck is making no other pickups or drop-offs along the way
Carting: Handling system consisting of small vehicles (carts)
trip_uuid - Unique ID given to a particular trip (A trip may include different source and destination centers)
source_center - Source ID of trip origin
source_name - Source Name of trip origin
destination_cente – Destination ID
destination_name – Destination Name
od_start_time – Trip start time
od_end_time – Trip end time
start_scan_to_end_scan – Time taken to deliver from source to destination
is_cutoff – Unknown field
cutoff_factor – Unknown field
cutoff_timestamp – Unknown field
actual_distance_to_destination – Distance in Kms between source and destination warehouse
actual_time – Actual time taken to complete the delivery (Cumulative)
osrm_time – An open-source routing engine time calculator which computes the shortest path between points in a given map (Includes usual traffic, distance through major and minor roads) and gives the time (Cumulative)
osrm_distance – An open-source routing engine which computes the shortest path between points in a given map (Includes usual traffic, distance through major and minor roads) (Cumulative)
factor – Unknown field
segment_actual_time – This is a segment time. Time taken by the subset of the package delivery
segment_osrm_time – This is the OSRM segment time. Time taken by the subset of the package delivery
segment_osrm_distance – This is the OSRM distance. Distance covered by subset of the package delivery
segment_factor – Unknown field

# Concept Used:

Feature Creation
Relationship between Features
Column Normalization /Column Standardization
Handling categorical values
Missing values - Outlier treatment / Types of outliers

# INSIGHTS
The Given data has 144867 Rows and 24 Columns The given data has two kinds of data that Training and test data No of rows in training data : 104858 , No of rows in test data : 40009 , We can see that majority of the data is training data Each Trip_uuid has more than one stops or relay points in its journey to reach from source to destination , hence group-by and Aggregate functions should be used careful i,e while grouping ["trip_uuid","source_name","destination_name"] use “last()” as we have multiple sources and destinations for each trip and while grouping ("trip_uuid") use sum() , also while using the grouping of segmented values we can directly use sum() as each value is individual recording . Columns Source-name and Destination-name have missing values with less than 0.2% , dropping off these rows as such minor percent of values may not affect the data. After dividing Source-name and Destination-name into city, place , code , state , it is seen that the address format is not the same for all orders and missing values can be found in place -1.5% , code-10% , state-10% , filling the null values with value of column city of the same respective rows Column trip_creation_time can be divided into Trip_Year, Trip_Month, Trip_Day , from these we can infer that data is from year 2018, month september(9) but data from days 4 to 11 are not present in data . Column start_scan_to_end_scan contains time taken to deliver from source to destination in Mins Using columns 'od_end_time','od_start_time' a new feature can be created Total time taken but checking the difference between 'od_end_time','od_start_time' . Before grouping the data by trip_uuid Route type FTL comprises 67.95% and Carting comprises 32.05% of the total orders . Top cities that have more number of Trips are Bangalore, Gurgaon, Kolkata, Hyderabad, Bhiwandi, Delhi. FTL deliveries are mostly Inter-state and Carting are mostly Intra-state services. After grouping the data by trip_uuid Route type FTL comprises 57.84% and Carting comprises 42.16% of the total orders . From the above difference between before and after grouping by trip_uuid we can infer that FTL type has more relay point although it is not making no other pickups or drop-offs along the way Among the given data Training data comprises 72.49% and test data comprises 27.51% Grouping data on trip_uuid to perform Visual Analysis Univariate Analysis : The most number of trips are from source code “D” & “HB” The most number of trips are to destination code “D” , “HB”,”H” & ”I” The most number of trips are from source state “Karnataka” , “Maharashtra”, “Haryana” The most number of trips are to Destination state “Karnataka” , “Maharashtra”, “Haryana” We can see that there is a slight decline in number of trips at the end of month Bivariate Analysis : Although Karnataka has the highest number of trips from Source district still the majority of those trips come under non-dominant route-type i,e Carting , whereas Maharashtra has highest FTL type trips still which is dominated by Carting . Insights that are observed in trips from source district resemble the insights observed in trips to destination district Source codes D and HB are quiet opposite when it comes to dominance of FTL and carting, D has more number of FTL’s whereas HB has more number of Carting’s In Destination codes D , HB are same as source codes and H , I codes have FTL in dominance By comparing source code and destination code we can understand that these codes are again divided internally as sub-codes . Multivariate Analysis : Haryana doesn't have any outliers even though it has one of the highest number of trips from source district West Bengal took the highest number of minutes to complete the trip from source district by which we can also conclude West bengal also has the most number of far away destinations Carting type took very less time to complete the trip when compared to FTL even though FTL does not have any other pickups or drop-offs along the way . In Destination district West bengal doesn't have any outliers Maharashtra took the highest number of minutes to complete the trip to destination district by which we can also conclude Maharashtra receives from most number of far away source districts Carting type took very less time to complete the trip when compared to FTL even though FTL does not have any other pickups or drop-offs along the way . Source code HB has the highest number of minutes to complete the trip by which we can also conclude HB also has the most number of far away destinations Carting type took very less time to complete the trip when compared to FTL even though FTL does not have any other pickups or drop-offs along the way . Destination code HB has the highest number of minutes to complete the trip by which we can also conclude HB receives from most number of far away source districts Carting type took very less time to complete the trip when compared to FTL even though FTL does not have any other pickups or drop-offs along the way . From the scatter plot of osrm_time, osrm_distance (Aggregate values ) we can see the trend is linear as the distance increases time increases Outliers are found in Columns actual_time_y, segment_actual_time_y, segment_osrm_distance_y, segment_osrm_time_y, start_scan_to_end_scan_y, Total_timetaken_y. NOTE : the letter “_y” after each Column name represents its Aggregated data . Visual analysis of Total_timetaken & start_scan_to_end_scan shows that both the data are similar & Hypothesis test Result - H0 Null hypothesis rejected , there is significant difference between the two groups Visual analysis of actual_time_y & osrm_time_y shows that both the data are similar & Hypothesis test Result - H1 failed to reject Null hypothesis , actual_time = osrm_time Visual analysis of actual_time_y & segment_actual_time_y shows that both the data are similar & Hypothesis test Result - H0 Null hypothesis rejected , there is significant difference between the two groups. Visual analysis of osrm_distance_y & segment_osrm_distance_y shows that both the data are similar & Hypothesis test Result - H1 failed to reject Null hypothesis , osrm_distance = segment_osrm_distance Visual analysis of osrm_time_y & segment_osrm_time_y shows that both the data are similar & Hypothesis test Result - H0 Null hypothesis rejected , there is significant difference between the two groups

  # Recommendations
States and cities that have Higher traffic of Orders like Maharashtra, Karnataka ,Haryana also Bangalore , Hyderabad etc need to check and increase warehouse capacity and workers. States and cities that have Lower traffic of Orders like Jummu & Kashmir, Uttarakhand etc , the company has to increase their exposure for their services by using difference means of advertising . Delhivary mostly provides services in Bulk and B to B , so creating weight margin discounts can increase sales dramatically. Reviewing the used OSRM can be beneficial as it failed to match the actual observations in some cases like osrm_time & segment_osrm_time .

​
