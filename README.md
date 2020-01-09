# Is Your Neighborhood Contaminated?
###An EDA analysis of the health and potential contamination of california neighborhoods by exploring hospital diagnosis rates.
### By Lawrence Glenn

## Links to Presentation
[Is your neighborhood contaminated?](www.???????)

## Table Of Contents
- [Introduction](#Introduction)
- [Overview of the Data](#Data-Overview)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Data Pipeline](#Data-Pipeline)
- [Model Selection](#Model-Selection)
- [Deep Learning](#Deep-Learning)
- [Emotional Analysis](#Emotional-Analysis)
- [Wordclouds](#WordClouds)
- [Conclusion and Next Steps](#Conclusion-and-Next-Steps)

## Introduction

According to the World Health Organization global rates of chronic dieseases are increasing and expected to reach 57% by 2020. Similarly cancer rates continue to increase, as well incidences of autoimmune disease. With facts like that it is more important than ever to determine the causes of these conditions and one thing they all have in common is that they can be brought about by environmental conditions.

We can gain insight in factors effecting local health y looking at the rate of certain diagnosis in local hospitals. This helps people from individuals trying to decide where to move, to alerting the EPA to locations with possible issues, informing realtors on factors that should influence housing prices, and letting insurance companies know if they should raise or lower rates in certain regions. After all who wouldn't want to know if their neighborhood was contaminated?

# DATA Overview
my data comes from census.gov, epa.gov, or data.chhs.ca.gov
my fields include 
Year 	OSHPD ID 	Facility Name 	Type of Control 	County Name 	Principal Diagnosis Group 	Count

I've added Longitude and Latitude to this initial data set.

there are >40000 entries from more than 500 diffierent hospitals across california from 2009-2014

the different types of diagnosis are 
['Infections', 'Neoplasms', 'Endocrine/Metabolism',
       'Blood/Blood-forming Organs', 'Psychoses & Neurosis',
       'Nervous & Sensory Systems', 'Circulatory', 'Respiratory',
       'Digestive', 'Genitourinary', 'All Pregnancies', 'Skin Disorders',
       'Musculoskeletal', 'Congenital Anomalies (Birth Defects)',
       'Symptoms', 'Injuries/Drugs/Complications',
       'Other Reasons for Health Services', 'Perinatal Disorders',
       'Births']
### Limitations

# Cleaning
My data was already free of null values and the like, but I did remove unneeded info (like accidents) and combined info I needed together (like adding longitude and latitude of hospitals)

# Process
After understanding and looking through the data I did a hypothesis test comparison of the rate of hospital diagnosis (neoplasms) vs california wide neoplasim diagnosis rates, then isolated the hopsitals that have a rate so high they have a less than 0.5% chance of being from random chance. One of these hospitals was far higher than all others but it is a nationwide leader in cancer treatments so it is reasonable to assume that people are traveling to that location and can be dismissed as an outlier.

Facililties vs count of neoplasm diagnosis in 2009
![alt text](/img/FacilityVsCountOfNeoplasm_2009.png "Facililties vs count of neoplasm diagnosis in 2009")

Facililties vs normalized count of neoplasm diagnosis in 2009
![alt text](/img/FacilityVsNormalizedCountOfNeoplasm_2009.png "Facililties vs normalized count of neoplasm diagnosis in 2009")

Facililties vs normalized count of neoplasm diagnosis in 2009 to 2014"
![alt text](/img/FacilityNormalizedCountOfNeoplasm_2009_2014.png "Facililties vs normalized count of neoplasm diagnosis in 2009 to 2014")

Facililties vs normalized count of neoplasm diagnosis in 2009 only high values
![alt text](/img/FacilityVsNormalizedCountOfNeoplasm_2009_HighValues.png "Facililties vs normalized count of neoplasm diagnosis in 2009 only high values")

Facililties vs normalized count of birth defects diagnosis in 2009 to 2014 only high values
![alt text](/img/FacilityVsNormalizedCountOfBirthDefects_2009_HighValues.png "Facililties vs normalized count of birth defects diagnosis in 2009 to 2014 only high values")

calculated the mean and variance for all of california neoplasm diagnosis for 2009-2014
neoplasm_all_CA_means_final = np.mean(neoplasm_all_CA_means)
neoplasm_all_CA_var_final = np.var(neoplasm_all_CA_means)
data_all = np.random.normal(neoplasm_all_CA_means_final, neoplasm_all_CA_var_final, size=1000)


yearly average of neoplasm diagnosis in california from 2009 ro 2015
![alt text](/img/Yearly_Avg_All_California_2009_20015.png "yearly average of neoplasm diagnosis in california from 2009 ro 2015")

Map of Califonia, blue is locations of high neoplasm diagnosis, yellow is high birth defect rate
![alt text](/img/CaliLocHighBirthDefectAndNeoplasm_2009.png "Map of Califonia, blue is locations of high neoplasm diagnosis, yellow is high birth defect rate")
