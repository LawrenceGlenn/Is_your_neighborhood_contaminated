# Is_your_neighborhood_contaminated
An EDA analysis of the health and potential contamination of california neighborhoods by exploring hospital diagnosis.


# DATA
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


# Cleaning
My data was already free of null values and the like, but I did remove unneeded info (like accidents) and combined info I needed together (like adding longitude and latitude of hospitals)

# Process
After understanding and looking through the data I did a hypothesis test comparison of the rate of hospital diagnosis (neoplasms) vs california wide neoplasim diagnosis rates, then isolated the hopsitals that have a rate so high they have a less than 0.5% chance of being from random chance. One of these hospitals was far higher than all others but it is a nationwide leader in cancer treatments so it is reasonable to assume that people are traveling to that location and can be dismissed as an outlier.

![alt text](/img/FacilityVsCountOfNeoplasm_2009.png "")
