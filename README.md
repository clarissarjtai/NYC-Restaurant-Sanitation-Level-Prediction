# NYC Restaurant Sanitation Level Prediction
AML Spring 2022 Final Project

# Collaborators
Elijah Flomen - ef2681, Clarissa Tai - rt2822, Nicolo Ricca - nr2810, Xinyu Huang - xh2511

Background and context to the problem statement. 
As students who recently moved to NYC, we wanted to examine datasets to help us drive insights about the city we live in. From living here, we have all noticed the sheer amount of food options available to us at all times of the day – we have come to the realization that restaurants and food are definitely integral parts of NYC culture. Additionally, something that we noticed in this city is that many restaurants have signage posted on their front window, showcasing their sanitation grade. As a result, we wanted to focus on specifically restaurants in NYC and various factors regarding restaurants’ cleanliness and sanitation grades. We learned that at least once a year, The Health Department conducts an examination of a restaurant’s various practices and then assigns them a grade/score, where lower is better. All of this data is recorded in a public database and our main goal is to train a model to predict the resulting score of a restaurant’s sanitation practices, based on features such as the location of the restaurant, the type of cuisine, features about the area, as well as previous inspection grades. Given that NYC Open Data has information on not only restaurants, but general cleanliness-related data on areas, we will attempt to incorporate these external datasets in the development of our model. For instance, we will consider data regarding rodents, water quality as well as Yelp reviews to train and test our model. Therefore, our problem statement is to see if we can form accurate predictions regarding the sanitation grades of restaurants in NYC. 
Identification and description of the dataset(s) and their source

NYC OpenData: Restaurant Inspection Results
https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j
This would be our main dataset in the analysis, the dataset contains 345k rows. Each row in this dataset is a restaurant citation, with 26 columns. Most of the features are categorical, since they describe the nature of the inspection, information regarding the restaurant and a description of the findings. The resulting score of the inspection is an integer and this is the label our model will be trained to predict. It is important that this dataset contains latitude and longitude data, since we will be able to link this set with external ones and compare inspection results, based on other factors regarding their physical coordinate location.

NYC OpenData: Rodent Inspection
https://data.cityofnewyork.us/Health/Rodent-Inspection/p937-wjvj 
As we can easily imagine, a massive rodent presence in a zone can impact the businesses nearby in a negative way. This impact can even be worse if we are talking about restaurants. It is not uncommon for rats to wander in search of something to eat,and there is no doubt that a restaurant can provide a stable source of food. This dataset includes 2.05 million rows and 20 attributes. Apart from inspections identifiers and internal documentation codes the most interesting features for our project are location data, time data and result.Location data include: Borough, ZIP code, Street Name, X coordinates, Y coordinates, Latitude, Longitude . Then we have an inspection date, and we have an attribute result that assesses the outcome of the inspection. We are going to use our location to link the inspection zone with the restaurant zone in a predetermined radius. In this way we will be able to use rat infestation as a predictor.

NYC OpenData: Water Tank Inspection
https://data.cityofnewyork.us/Health/Self-Reported-Drinking-Water-Tank-Inspection-Resul/gjm4-k24g 
Similar to rodent inspection, we are also aware of the water quality nearby. It is clear that water quality may impact restaurant inspection scores and customers’ health in some way. This dataset contains 37.4k rows and 49 columns, including the longitude, latitude and all other columns we need to concat with the main dataset. Other than geographical features, the dataset owns sufficient binary features to indicate the quality of the water tank. In addition, this dataset is self-reported and collected by the Department of Health and Mental Hygiene (DOHMH), and thus exists some issues in recording date and inspection date. 

3. Proposed ML techniques you are proposing on applying to solve the problem
The dataset contains both numerical and categorical features, and our goal is to predict the sanitation grade of the restaurants. After some feature engineering processes, such as extracting distance from coordinates or encoding categorical features, we would like to explore different supervised learning techniques. However, We are not sure about the level of nonlinearity in the datasets at this point. Thus, we can first compare the prediction results between random forest(tree-based) model and SVM(linear regression) model, with logistic regression model as a baseline. For advanced study, we may try to optimize our model using gradient descent techniques. If time permits, we will try to build a Deep Neural Network to see if we can improve the regression performance. Besides, with the datasets we have, we will also consider constructing a NYC restaurant recommendation system. 
