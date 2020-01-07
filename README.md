# Is_your_neighborhood_contaminated
An EDA analysis of the health and potential contamination of california neighborhoods by exploring hospital diagnosis.


# DATA
my data comes from census.gov, epa.gov, or data.chhs.ca.gov

# Cleaning
My data was already free of null values and the like, but I did remove unneeded info (like accidents) and combined info I needed together (like adding longitude and latitude of hospitals)

# Process
After understanding and looking through the data I did a hypothesis test comparison of the rate of hospital diagnosis (neoplasms) vs california wide neoplasim diagnosis rates, then isolated the hopsitals that have a rate so high they have a less than 0.5% chance of being from random chance. One of these hospitals was far higher than all others but it is a nationwide leader in cancer treatments so it is reasonable to assume that people are traveling to that location and can be dismissed as an outlier.