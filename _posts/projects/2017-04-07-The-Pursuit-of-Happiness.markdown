---
layout: project
title:  "The Pursuit of Happiness"
date:   2017-04-07 17:08:35 -0400
categories: projects
---


## About
This was my 2017 science fair project. This project had two goals. The first of which is to analze and compare, on an average, what life events make people particularly happy. The second obejctive of the project was to compare the similarity of life events. To complete this analysis, I used the R programming language. In R, I used the Hellinger distance, which lets you compare two discrete random variables, in my case, the distribution of happiness for life events.
## Code
### Averages
```R
lifeEvents = read.csv("life_events.csv");
# store data set
counter <- numeric(25);
# counter for valid responses for each life event
totalHappiness <- numeric(25);
# Added up all of the happiness levels for all of the respondents who answered.
average <- numeric(25);
for(j in 28:52){
# Cycles through all of the life events.
  for (i in 1:10054) {
# Cycles through all of the respondents.
    if (lifeEvents[i,j] > -1)
    {
      counter [j-27] <- counter[j-27] + 1;
# Increments the counter, j-27 to get back to the correct row of column, because life event data starts in the 28th row.
      totalHappiness[j-27] <- totalHappiness[j-27] + lifeEvents[i,j];
# Increments total happiness. j-27 for the same reason.      
      
    }
    
  }
}


for(k in 1:25){
  
  average[k]= totalHappiness[k]/counter[k];
#Standard average function. Total divided by the number of people.
}
```
### Hellinger Distance
```R
lifeEvents = read.csv("life_events.csv");
# store data set
counter <- numeric(25);
# counter for valid responses for each life event
peoplePerLevel <- matrix(0, nrow = 10, ncol = 25);
# Counts number of people per happiness level - 10 rows by 25 columns
distributionTable <- matrix(0, nrow = 10, ncol = 25);
# Distribution for each happiness level - 10 rows by 25 columns
hellingerSum <- matrix(0, nrow = 25, ncol = 25);
# Data frame to store the Hellinger distances for each life event.

#This double for loop calculates the number of people for each happiness level, for each life event.
for(j in 28:52){
#
  for (i in 1:10054){
# Cycles through all of the respondents
    if(lifeEvents[i,j] > -1){
# Eliminates all of the missing responses in the counter variable      
      counter[j-27] <- counter[j-27] + 1;
# Assigns the counter number found to the appropriate slot in the array. (Which life event)      
      if(lifeEvents[i,j] == 1) {
        peoplePerLevel[1,j-27] <- peoplePerLevel[1,j-27] + 1;
        
      }
# If a respondent gave 1 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.   
      if(lifeEvents[i,j] == 2) {
        peoplePerLevel[2,j-27] <- peoplePerLevel[2,j-27] + 1;
        
      }    
# If a respondent gave 2 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.
      if(lifeEvents[i,j] == 3) {
        peoplePerLevel[3,j-27] <- peoplePerLevel[3,j-27] + 1;
        
      }     
# If a respondent gave 3 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.
      if(lifeEvents[i,j] == 4) {
        peoplePerLevel[4,j-27] <- peoplePerLevel[4,j-27] + 1;
# If a respondent gave 4 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.        
      }   
      if(lifeEvents[i,j] == 5) {
        peoplePerLevel[5,j-27] <- peoplePerLevel[5,j-27] + 1;
# If a respondent gave 5 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.
      }
      if(lifeEvents[i,j] == 6) {
        peoplePerLevel[6,j-27] <- peoplePerLevel[6,j-27] + 1;
# If a respondent gave 6 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.
      }
      if(lifeEvents[i,j] == 7) {
        peoplePerLevel[7,j-27] <- peoplePerLevel[7,j-27] + 1;
# If a respondent gave 7 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.       
      }
      if(lifeEvents[i,j] == 8) {
        peoplePerLevel[8,j-27] <- peoplePerLevel[8,j-27] + 1;
# If a respondent gave 8 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.      
      }
      if(lifeEvents[i,j] == 9) {
        peoplePerLevel[9,j-27] <- peoplePerLevel[9,j-27] + 1;
# If a respondent gave 9 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.        
      }
      if(lifeEvents[i,j] == 10) {
        peoplePerLevel[10,j-27] <- peoplePerLevel[10,j-27] + 1;
        
      }
# If a respondent gave 1 for life event j, in the matrix peoplePerLevel is incremented by 1. J will cycle from 1-25.
      
      
      
      
    }
  }
}

#This double for loop calculates the percentage of people for each happiness level, for each life event. 
for(j in 1:25){
  
  for(i in 1:10){
    
    distributionTable[i,j] <- peoplePerLevel[i,j]/counter[j];
    
    
    
  }
  
  
}
# Takes the number of people who had a happiness level of i for life event j, and divides it by the total number of people for life event j.
for(j in 1:25){
  
  k=j+1;
# Makes the starting number for the second life event of the pair of life events.
  while (k <= 25){
  
    for(i in 1:10){
    
    hellingerSum[j,k] <- hellingerSum[j,k] + (sqrt(distributionTable[i,j]) - sqrt(distributionTable[i,k]))^2
# Equation of the Hellinger Distance - Take the sqrt of percentage of people who chose level "i" for life event j
# subtract it from percentage of people who chose level "i" for life event k.
  }
  k=k+1;
# Increment k by 1 to generate a new pair. ie, 1,2 to 1,3
  }
  
}

hellingerSum <- 1/sqrt(2)*sqrt(hellingerSum)
# Take the final sqrt and multiply by 1/sqrt 2. Do this to the whole equation.
```
## Awards

This project won first place at the Worcester Regional Science and Engineering Fair, and third place at the Massachusetts State Science and Engineering Fair. I am honored to say that this project was placed as one of the top 300 in the United States, in the Broadcoam MASTERS National Science and Engineering Fair.