# Toronto-Ambulance-Unit-Location-Optimizer
This is a project for a course at the University of Toronto, Analytics in Action (MIE368), utilizing machine learning and optimization libraries in order to predict emergency call data based on population demographics per FSA scraped from Census Canada and optimized to efficiently allocate ambulance resources across fixed stations.

Problem Statement: To make effcient use of Toronto's ambulance resources by minimizing the number of Ambulance units needed to meet predicted call demand

How it Works:

EDA
1) Import emegerency respose data for Toronto in 2016. We then clean up this data by removing any incompletye tuples and only using data for "M" based FSA's to scope the project down. The data is then grouped per FSA per day to have provide ata for the total number of calls an FSA recives per day in 2016. 
2) Existing Ambulance Stations GeoJSON file with longitude an latitude is then read in as a Pandas dataframe.
3) FSA demographic data is scraped from Stats Canada (this code is commented out after all data was intially inputted"
4) Left Join demographic data to paramedic data and check if dispatch times are on weekends, weekdays, or holidays and provide binary indicators if calls are made on a weekend or holiday.
5) Compute centroids of FSA's as the project assumes all calls are made from centroids

Predictive Modelling
1) Find heavily correlated features and create a data frame that will compare 3 types of predictive models: Linear regression, Ridge Regression, and Lasso Regression which are benchmarked against their mean data counterparts. 
2) Features are then standardized and the models are then trained and tested on split data within 2016
3) Use Feature Engineering techniques to improve model accuracy by iterating through combinations of features to create new features with improvment and P-Value thresholds of 1 and 0.05 respectively while also having an overall improvment of over 75 (F-Score in code)
4) Features are then added to the models and used to feed into presciptive analytics 

Optimiztion Model
1) using y-test predictions create a df of total number of calls which is joined with the paramedics and stats canada df to provide a demand fir each FSA for each day with their respective centroids. 
2) define a function that uses the haversine formula to calculate the linear distance between 2 co-oridinates while taking in the earths curvbiture into account
3) greedy algorithm ensures that demand is not double counted meaning that for our deifned radius of 10 km, if an emergency response call is within the radius of 2 or more stations, the algorithm with iterate through the stations and allocate demand to the nearest one. providng a final dataframe of demands for each station for each day.
4) construct an optimization model that minimizes the number of units needed to meet demands to make efficient use of toronto medical resources following constraints that a max of 5 units can be deployed per station, non negative number of units deployed, and less than 242 (total number of units within toronto) are assigned across stations. Additionally we assume each ambulance can respond to 20 calls per day and that calls are sequential. 
5) The resulting model provides a resondable allocation of ambulances acorss FSA stations creating a buffer should the need for more ambulances arise. 



