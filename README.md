# NYC Restaurant Sanitation Level Prediction
AML Spring 2022 Final Project

## Collaborators
Elijah Flomen - ef2681, Clarissa Tai - rt2822, Nicolo Ricca - nr2810, Xinyu Huang - xh2511

## Problem Description

For our project, we decided to focus our analysis on restaurant sanitation in New York City. As people who have just recently moved to New York, we noticed that many restaurants showcase their sanitation grades on their front door. Upon further research, we found that each restaurant in New York City is subject to a random inspection where health officials examine the restaurant, looking for compliance with a long list of potential violations. After conducting this inspection, the restaurant then receives a score of A, B, or C, which indicates their level of cleanliness. 

Our main problem is to see if we are able to accurately identify a restaurant as high-risk or low-risk regarding their sanitation. Given such a tool, we see the practical use in that the health department of New York City can use this program to gain prior knowledge regarding the sanitation-level of a restaurant before actually sending an inspector. As a result, by having some sort of prior intelligence regarding the cleanliness of a restaurant, the city can save resources as well as improve public health by allocating capital according to the predicted risk levels of restaurants in the 5 boroughs of New York. 

## Key Insights

A crucial finding in our data exploration was that our dataset is highly imbalanced. The highly imbalanced nature of our dataset was found to be a key cause for its poor performance, despite significant efforts attempting sampling techniques and applying class-weights. The vast majority of restaurants receive an ‘A’ score. As a result, we will need to conduct some sort of sampling techniques to ensure proper performance of our model. As a first step, we decided to convert our dataset from a multi-class problem to a binary problem, by grouping together the B and C classes. Given that the practical use of this tool would be to identify a restaurant as high-risk, or low-risk, we figured that it makes sense for our model to be trained as a binary problem and not a multi-class problem. Even after making this conversion, we were still left with an imbalanced dataset, with the majority of the examples being low-risk (or grade-A restaurants). In this binary classification problem, we have ~40k negative labels and ~5k positive samples. Given that our dataset had a fair amount of missing values, it had been cut down significantly from the original dataset due to missing values, we decided it is probably best to conduct an oversampling strategy as to not overly cut the number of training examples. 

Regarding missing data, in our data exploration, we noticed that there was no immediately discernable pattern for rows containing missing data. Additionally, as a result of the majority of our data being categorical (from the main Restaurant Dataset), forms of imputing are difficult and hence we elected to simply drop all the rows that contained a missing value in the column that was important for our analysis.  

## Data Sources

1. NYC OpenData: Restaurant Inspection Results
https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j
This would be our main dataset in the analysis, the dataset contains 345k rows. Each row in this dataset is a restaurant citation, with 26 columns. Most of the features are categorical, since they describe the nature of the inspection, information regarding the restaurant and a description of the findings. The resulting score of the inspection is an integer and this is the label our model will be trained to predict. It is important that this dataset contains latitude and longitude data, since we will be able to link this set with external ones and compare inspection results, based on other factors regarding their physical coordinate location.

2. NYC OpenData: Rodent Inspection
https://data.cityofnewyork.us/Health/Rodent-Inspection/p937-wjvj 
As we can easily imagine, a massive rodent presence in a zone can impact the businesses nearby in a negative way. This impact can even be worse if we are talking about restaurants. It is not uncommon for rats to wander in search of something to eat,and there is no doubt that a restaurant can provide a stable source of food. This dataset includes 2.05 million rows and 20 attributes. Apart from inspections identifiers and internal documentation codes the most interesting features for our project are location data, time data and result.Location data include: Borough, ZIP code, Street Name, X coordinates, Y coordinates, Latitude, Longitude . Then we have an inspection date, and we have an attribute result that assesses the outcome of the inspection. We are going to use our location to link the inspection zone with the restaurant zone in a predetermined radius. In this way we will be able to use rat infestation as a predictor.

3. NYC OpenData: Water Tank Inspection
https://data.cityofnewyork.us/Health/Self-Reported-Drinking-Water-Tank-Inspection-Resul/gjm4-k24g 
Similar to rodent inspection, we are also aware of the water quality nearby. It is clear that water quality may impact restaurant inspection scores and customers’ health in some way. This dataset contains 37.4k rows and 49 columns, including the longitude, latitude and all other columns we need to concat with the main dataset. Other than geographical features, the dataset owns sufficient binary features to indicate the quality of the water tank. In addition, this dataset is self-reported and collected by the Department of Health and Mental Hygiene (DOHMH), and thus exists some issues in recording date and inspection date. 

4. NYC Census Data:
https://www.kaggle.com/datasets/muonneutrino/new-york-city-census-data
Upon initial models' poor performance, we decided to add additional features, related to the demographics of the surrounding restaurant area. We made use of NYC Census data to get information about ethnic and socio-economical features. We joined these datasets by examining longitude and latitude data of the reported census data and then assigning each restaurant with the data associated to the closest census report, by Euclidean distance. From the census data, we chose to keep data regarding the ethnicities in the vicinity of the restaurant, as well as population density, income and unemployment. 
