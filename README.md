# Is Your Neighborhood Contaminated?
#### An EDA analysis of the health and potential contamination of california neighborhoods by exploring hospital diagnosis rates.
#### By Lawrence Glenn

## Links to Presentation
[Is your neighborhood contaminated?](www.???????)

## Table Of Contents
- [Introduction](#Introduction)
- [Overview of the Data](#Data-Overview)
- [Initial Exploratory Data Analysis](#Initial-Exploratory-Data-Analysis)
- [U-Testing](#U-Testing)
- [T-Test Comparison](#T-Test-Comparison)
- [County Analysis](#County-Analysis)
- [Conclusions](#Conclusions)
- [Going Foward](#Going-Forward)

## Introduction

According to the World Health Organization global rates of chronic dieseases are increasing and expected to reach 57% by 2020. Similarly cancer rates continue to increase, as well incidences of autoimmune conditions. With facts like that it is more important than ever to determine the causes of these conditions and one thing they all have in common is that they can be brought about by environmental conditions.

We can gain insight in factors effecting local health y looking at the rate of certain diagnosis in local hospitals. This helps people from individuals trying to decide where to move, to alerting the EPA to locations with possible issues, informing realtors on factors that should influence housing prices, and letting insurance companies know if they should raise or lower rates in certain regions. After all who wouldn't want to know if their neighborhood was contaminated?

## DATA Overview
My data comes from census.gov, epa.gov, or data.chhs.ca.gov
These sources have very clean entries thought many of them have to be combined to provide a more complete view

My primary source was a list of diagnosis groups from california hospital and included the features:
* Year
* OSHPD ID
* Facility Name
* Type of Control
* County Name
* Principal Diagnosis Group
* Count

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

## Initial Exploratory Data Analysis

Since the data includes the number of patients that recieved a diagnosis but not the number of people that the hospital services it will be useful to normalize this data. By dividing the count of each diagnosis by the total number of diagnosis a hospital performed for each year we arrive at a yearly rate of diagnosis.

We are most interested in conditions that have a large environmental causal factor so we will focus our analysis on the catagories Neoplasms, Endocrine/Metabolism, Nervous & Sensory Systems, and Congenital Anomalies (Birth Defects)


![alt text](/img/TotalPatientsVsDiagnosis.png "")
Here we have total patients comapred to diagnosis rates. As we can see the rate change is largely flat, this suggests that our normalized rates don't change much just because more people attend the hospital, which is exactly what we would want to see. There is a large spike in the begining of each chart but we would expect more variation at smaller sample sizes. Lets just zoom in to be sure.


![alt text](/img/TotalPatientsVsDiagnosisZoom.png "")
We don't have anything too strange (like values at a count of 0) and the lower sample counts will simply lower our confidence in future analysis. Nothing to worry about.


![alt text](/img/ControlTypeVsDiagnosis.png "")
Next we have the type of control of hospitals vs the normalized diagnosis. It seems that there are higher rates of neoplasms, Edocrine conditions and somewhat birth defects at non profit hospitals. This may have something to do with non profits being more available in lower income regions which also tend to be less healthy. There is an interesting spike of nervous and sensory system conditions at investor led hospitals. Perhaps those types of diagnosis are more profitable to diagnose? This would be an interesting deep dive for an EDA focused on income inequality and health but for our purposes we will simply make note of it and move on.

![alt text](/img/CountyVsDiagnosis.png "")
Above is a graph of the Various counties of California and their diagnosis rates. Its a bit crowded so lets focus on only those counties which have a higher rate.

![alt text](/img/CountyVsDiagnosisZoom.png "")
Here we can see that certain counties are probably less healthy than others. Los Angeles, Orange County, Fresno, and San Bernandino counties have much higher rates of Neoplasms, Nervous system, Endocrine, and Birth defect rates respectively. We will anaylize this health information by location and attempt to determine which areas have the largest problems. Why different counties have higher rates of very specific conditions is an interesting fact that will require more research to address.


Below is a graph of Neoplasm rates for 2009-2014
![alt text](/img/FacilityNormalizedCountOfNeoplasm_2009_2014.png "Facililties vs normalized count of neoplasm diagnosis in 2009 to 2014")

Looking at the facilities that have the highest Neoplasm diagnosis rates we see that the highest, City of Hope Helford Clinical Research Hospital, is a national leader in cancer treatments. This means people are traveling to this location for those diagnosis and we will remove it as an outlier from all analysis of neoplasms.

We see a similar graph for Endocrine/Metabolism rate for 2009-2014.
![alt text](/img/FacilityNormalizedCountOfEndocrine_2009_2014.png "Facililties vs normalized count of endocrine/metabolism diagnosis in 2009 to 2014")

Just as before we have a few locations with very high relative values but after some research these locations do not appear to be specialist so they can remain in the data.

Again for Nervous & Sensory Systems rates 2009-2014.
![alt text](/img/FacilityNormalizedCountOfNervous_2009_2014.png "Facililties vs normalized count of nervous & sensory system diagnosis in 2009 to 2014")

These too don't seem to be specialists so their values can remain.

Last but not least Birth Defect rates 2009-2014.
![alt text](/img/FacilityNormalizedCountOfBirthDefects_2009_2014.png "Facililties vs normalized count of nervous & sensory system diagnosis in 2009 to 2014")

These high values all came from childrens hospitals and as such should be removed as data skewing specialists.

We can also graph the locations with the highest rates as a line over time to look for trends

Neoplasm, Endocrine/Metabolism, and Nervous System rates (only highest, non filtered locations)
![alt text](/img/NeoplasmEndocrineNervousHigh_LinesOverTime.png "")

we can see that Endocrine diagnosis spike after 2013 at the Fresno Heart and Surgical Hospital. Nervous System Diagnosis also raise since 2010 at Healthbridge Children's Hopsital-Orange. This is only a few years so these may be anomolies but they are locations that if expanding out data we should keep an eye on.


## U-Testing

Null Hypothesis: A patient at a hospital is diagnosed with a condition at the same or lower rate then a patient in the rest of california
Alternate Hypothesis: A patient is diagnosed with a condition at a higher rate than the rest of california
Alpha = .05

By looking at the data for every patient in california and their either being diagnosed with a particular condition or not we can treat everyone in California as a sample. Then doing the same but only for the patients at each hospital we can compare those samples to determine if the number of people being diagnosed with a condition at a location is highly unlikely as compared to the state as a whole.

I selected the U test because I had the available processing power and U testing has no distirubtion assumptions. I believe that a T test would also have been valid since the average of these values would be a normal distribution I decided that a U test would be more through.

What follows is a map of the locations of hospitals that have a less than 0.5% likelihood of having such a high diagnosis rate by random chance. Though neoplasms, Nervous & Sensory Systems, Edocine/Metabolism and birth defects are displayed. 

![alt text](/img/Diagnosis_2009_2014_onCalifornia.png "")

It is important to note that this showed 2009-2014 with a low alpha for each "hit" so we can see how consistant high diagnosis were at a location based on how solid the location looks and the size of a "hit" is purportional to how extreme the diagnosis rate was.

Another approach was also used for birth defect analysis, to compare only childrens hospitals since people would be most likely to take a child to their nearest childrens hospital if they had a serious birth defect. Unfortunately that limits the available data to only 6 locations and makes drawing statistically significant conclusions difficult.

Here is a comparative graph all those diagnosis at once from 2009-2014 using the same size and alpha dot scheme as the previous graph

![alt text](/img/CaliLocHighBirthDefectAndNeoplasm_2009_2014_overlapped.png "")

As we can see there is high concentration of multiple conditions near Los Angeles and to a less extent, San Francisco

## T-Test-Comparison

The same samples were used on a T test and the results compared. There were only a handful of values that differed, as displayed below.

![alt text](/img/T_U_Diff_Map.png "")

This shows that the varience between the approachs was very small. The main difference between the tests is the T test assumes a normal distribution (which the data should be) and the U test does not. We can be fairly confident in our U test results however it is interesting to note that most of the values that differ were endocrine diagnosis. This may suggest that their results are just barely defeating our null hypothosis and perhaps we should give them a more critical look than the others.

## County Analysis

Taking the same U test aproach used above we can create samples from every county rather than every hospital and compare it to the rest of the state. After performing this consolidation we observed no diagnosis rates that were higher than the state by a statistically significant margin for Endocrine, Nervous System, and birth defects.

This may be the result of our data not being detailed enough to provide adaquit information on the counties. May counties do not even have a hospital in them, which will alter the overall result quite a bit.

We do however see a county level variation of neoplasm diagnosis, shown below

![alt text](/img/neoplasm_by_county.png "")

As we can see there is still a large effect in some areas, especially in the Los Angeles region. It is possible that there are smaller loctations that have large health concerns but not enough population to effect the values of the county. It is also possible that the counties that have high values are because of localized conditions that are very bad and the rest of the county is relatively unaffected.

Combining the data from this and the hospital level it is reasonable to conclude that Los Angeles and to a lesser extent the bay area are not healthy places to live. Other locations like San Diego or more isolated hot spots may be from more random flutuations or data limitations.

## Conclusions

There are many things that we can infer from this information. The most obvious is that major cities are the least healthy locations and more than likely have several factors influencing contamination and health of people who live there.

Its also worth noting the even among major cities Los Angeles is particularly unhealthy. However it seems almost every hospital has a high rate of at least one of the conditions, so it is possible that our data is too broad (only the sum of diagnosis catigories per year) if draw detailed conclusions.

Something also interesting is there is consistently high values for neoplasms and endcrine diagnosis near redding, a much smaller location with lower density of hospitals than other locations with large values. This could mean there are health issues to investigate near that location.

### Limitations

This approach assumes that people generally visit whatever hospital is nearest to where they live or work. It lacks information outside of california so values near the boarder may be disporportionally effected. Also we only have diagnosis catigories not individual diagnosis which would be far more instructive. There is also the problem that high density of hospitals could allow for more variation in which hospitals patients visit for a particular condition. Also These diagnosis are not nessicarily the first and only time someone is diagnosed with a condition, so there could be duplicates in the data skewing the results. There is also the limitation of the data coming only from hospitals. This will poorly reporesent all population that do not have access to full hospital facilities. There are also a large number of factors that our data doesn't adjust for, like income.

## Going Forward

Compare the data to known health factors to see if they corralate (like air or water pollution maps)
If more data could be located on wealth, or other states more factors could be accounted for.
A machine learning algorithm coudl be used to try to find unnoticed connections within the data.
A greater granularity of data from more sources (such as doctors offices) could go a long way to providing more accurate estimations.
Natural language processesing could be used to analyze EPA reports and isolate known contamination events and use them as a learning basis for a supervised classifier AI.