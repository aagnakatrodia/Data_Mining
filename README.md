Data_Mining and Predictive Analytics

<h1><center>Predictive Analysis of crime and real-estate data in the city of Los Angeles</center></h1>

This model  will analyze the criminal incidents/behavior in the Los Angeles City
Department and predict whether there is any impact on real estate prices in crime-affected
neighborhoods. This will help the Los Angeles Police Department to formulate crime prevention policies and assist people in evaluating the safety of various neighborhoods when leasing real estate.

There are two datasets that were used here. The first dataset consists of the records regarding crimes that are committed in the city of Los Angeles. The second dataset consists of the median value of gross rent prices in the different areas of the city. The data is sourced from LA city website. The data is updated every Thursday and is open to the public in order to maintain transparency with the public.

<b>Data source:</b>

Crime Data: https://data.lacity.org/A-Safe-City/Crime-Data-from-2010-to-Present/63jg-8b9z <br>
Rent Data: https://usc.data.socrata.com/Los-Angeles/Rent-Price-LA-/4a97-v5tx

<b>Data Engineering:</b>

<i>Imputing the missing values:</i>
Crime dataset contains huge amount of information which gets updated every Thursday. At the beginning of this project, it had almost 1.9 million observations. Relatively, it had a lot of missing, unreadable and inconclusive variables which had to be taken care of.

<i>Merging Crime with Rent Data:</i>
Census tracts are polygons and cover a well-defined geographic area. They
provide more granularity (73,000 areas) than ZIP Codes (43,000). They are non-changing static
geography from decennial census to census. Rent dataset already has Census Tracts which moved the focus on using tracts to form a correlation between the two. Furthermore, the Rent dataset has 231 different neighborhoods which seemed convincing enough and resulted in a more granular and significant analysis. After a long back breaking research on how to use Tracts, it was found that it can be done via api.census.gov/data by creating an account, getting an API key and calling the API to get the Tract data. We wrote a code in Python to extract the Tract data and a code in R to use the Tract number to merge the datasets.


<b>Methodology</b>

Since Median Rent Price (Amount) is a continuous variable, it was converted into a categorical variable consisting of 10 bins. The range for the rent price is around $250 to $3,500 to each of the bins consists of around 325 values of the rent prices. We then divided the total data into training and test data sets using a ratio of 70:30 respectively using a seed value of 12345. This marked the end of data preparation and engineering.

Using the rent categories as the dependent variable and the crime code, neighborhood where crime took place and the year in which crime was committed as the dependent variable, four data mining models were run to get the predictions on rent categories:

•	Naive Bayes

•	Multinomial Logistic Regression

•	XGBoost


<b>Conclusion</b>

•	The city of Los Angeles is susceptible to a variety of crimes with BATTERY-SIMPLE ASSAULTS being most prevalent across the neighborhoods. <br><br>
•	The BURGLARY FROM VEHICLE ranks second in the list , also consisting of crimes such as THEFT OF IDENTITY , PETTY THEFTS (<$90) , BURGLARY and SIMPLE ASSAULTS BY INTIMATE PARTNER. <br><br>
•	The Female population is more susceptible to Assaults whereas the Male population is more susceptible to Burglaries. <br><br>
•	The analysis of Crime rates reveals that the people in mid-twenties are at high risk in the city. <br><br>
•	These factors serve as important catalyst for change in the socio-economic composition of communities. While such figures are results of analysis over a long period of time, crime is capitalized into local housing markets quickly and thus provides as an early indicator of neighborhood transition.<br><br>



•	The rent prices across the neighborhoods in the city were grouped by the years and the standard deviation of the rent over these years were calculated. <br><br>
•	It is surprising to see that, for the year 2015 there is a boost in the maximum rent price for households. Further analysis reveals that this observation could be attributed to the significant decrease in the number of crimes for the given year. The crimes appear to have decreased up to 75% when compared to the crime rates for previous years.<br><br>
•	A negative correlation between the rate of crime and the rent amounts was noticed.<br><br>



