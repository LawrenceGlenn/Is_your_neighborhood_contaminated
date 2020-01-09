# Is Your Neighborhood Contaminated?
#### An EDA analysis of the health and potential contamination of california neighborhoods by exploring hospital diagnosis rates.
#### By Lawrence Glenn

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

According to the World Health Organization global rates of chronic dieseases are increasing and expected to reach 57% by 2020. Similarly cancer rates continue to increase, as well incidences of autoimmune conditions. With facts like that it is more important than ever to determine the causes of these conditions and one thing they all have in common is that they can be brought about by environmental conditions.

We can gain insight in factors effecting local health y looking at the rate of certain diagnosis in local hospitals. This helps people from individuals trying to decide where to move, to alerting the EPA to locations with possible issues, informing realtors on factors that should influence housing prices, and letting insurance companies know if they should raise or lower rates in certain regions. After all who wouldn't want to know if their neighborhood was contaminated?

## DATA Overview
My data comes from census.gov, epa.gov, or data.chhs.ca.gov
These sources have very clean entries thought many of them have to be combined to provide a more complete view

My primary source was a list of diagnosis groups from california hospital and included the features:
| Year | OSHPD ID | Facility Name | Type of Control | County Name | Principal Diagnosis Group |	Count |
| ---- | -------- | ------------- | --------------- | ----------- | ------------------------- | ----- |

By adding data from California's Office of Statewide Health Planning and Development I was about to add Longitude and Latitude of each hospital to this data.

This primary data has more than 40000 entries from more than 500 diffierent hospitals across california during the time period 2009-2014

One of the things we will be most interested in are the different types of diagnosis which are 
['Infections', 'Neoplasms', 'Endocrine/Metabolism',
       'Blood/Blood-forming Organs', 'Psychoses & Neurosis',
       'Nervous & Sensory Systems', 'Circulatory', 'Respiratory',
       'Digestive', 'Genitourinary', 'All Pregnancies', 'Skin Disorders',
       'Musculoskeletal', 'Congenital Anomalies (Birth Defects)',
       'Symptoms', 'Injuries/Drugs/Complications',
       'Other Reasons for Health Services', 'Perinatal Disorders',
       'Births']

### Limitations
This data only includes information from California, which can limit our understanding, especially for locations that are near a boarder. Patients could be coming from or going to locations outside the state. Likewise the data only includes OSHPD certified hospitals, which is almost all health providers in California but doesn't include some private locations such as the Shriners hospitals. To conform to HIPPA limitations our data doesn't list individual patients but rather the total number of patients who recieved a given diagnosis catigory at each hospital per year.

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
