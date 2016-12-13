SFDAT28 Final Project - Ryan Cohen

#Intro:
My project is to examine the election results at the county level based on demographic data of high school cohorts in school districts within the county and census data.  The goal is to be able to predict whether a school district is likely to vote for or against President-Elect Trump.  Based on demographic data, school districts with polarizing cohort compositions than that of their peers will fall into the errors of the prediction model.

#Data Sets:
1. AT&T Data for Diplomas - Graduation Statistics
Contains high school cohort and graduation statistics merged with 2010 census data for school districts in the US.  (9907, 580)
Obtained from https://datafordiplomas.devpost.com/details/resources which contains data wrangled by Data for Diplomas and Everyone graduates center at John Hopkins.
2. United States General Election 2016 by County
Contains voting results (integer), by county (FIPS #), and by candidate (each candidate has its own row per county).  (15565, 8)
Obtained from https://data.world/aaronhoffman/us-general-election-2016, which contains scraped data from the NY Times website.


#Pre-processing:
The two data sets, Graduation/Census and Election Data, needed to be merged together.  In order to do that, a CountyFips column needed to be feature engineered as a common column to join on.  After the data sets were merged, more columns that described the school district cohorts needed to be feature engineered for county level aggregation.  The data needed to be cleaned of missing/null data as well as data that was non-uniformly logged.  


#Feature Selection:
Feature selection was done by dimension reduction using DecisionTreeClassifier across all of the features of the data set.  Then, feature tuning was done by hand, to pick which features seem most relevant to the topic/question being posed.  This was a balance  between model performance, error reduction, and perceived feature relevance.

#Exploratory Data Analysis
Through exploratory data analysis, I learned that while a high percentage of white students in the cohort of the school district was positively correlated with the percentage of votes that the_Donald received.  The opposite (negative correlation) was true for school districts where the black student cohort was larger.  These correlations seemed obvious though.  Surprisingly, it was much less polarizing when it came to the hispanic cohort populations.  Furthermore, race related demographics were not necessarily the most important features.  Percentage of adults who hold college degrees and the percentage of the population within the county that lived in a "rural" area were also very important features of the data set.

#Modeling:
The response/target for my data set is a binary, so classification models were used.  Logistic regression, DecisionTreeClassifier, and RandomForestClassifier ended up being the most consistent and accurate models.  Each model was cross-validated 5-10 times.

  * RandomForestClassifier - accuracy: 0.843339323478
  * DecisionTreeClassifier - accuracy: 0.830989728204
  * LogisticRegression - accuracy: 0.849257013678
 
Then a voting classifier ensembles the models above which gave an accuracy of: ~93%.
The models beat the null accuracy of ~73% alone, but performs even better when ensembled.
Predicting at the county level using the a weighted score (binary multiplied by the percentage of the county that the cohort represents) results in an accuracy of 95.9%.


#Conclusions:
In conclusion, I found that there were school districts where the diversity of the cohort were not representative of their county within the errors.  However, not every county that was not representative was in the errors.  This means that there are certain features that, while they significantly increase the accuracy of the model, introduces noise in determining whether or not the district was representative.  Another conclusion was that hispanics around the country did not vote as a monolith or did not turn out to vote.


#Next Steps:
To make the model perform better, I plan to add 2012 and 2014 voting results by county in order to get some historical data into the mix.  I would also need to get more complete/updated school district and census data to gain a more accurate representation of the population.
 * 