# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
The first step for this peer assessment is be the loading and preprocessing of the data (if needed). Please, keep in mind here that I'm assuming that the markdown file is in the same directory as the zipped data file. If this is not the case, the code chunks will not run properly.

After forking and clonning the repository, the data will be in a zipped file called *activity.zip*. Thus, we need to unzip the file in order to read it properly. I will use *unz* for this. Besides, I'm using variables to store the names of the files, as this allow me to re-use code chunks for similar problems. 


```r
zipFilePath <- "./activity.zip"
csvFileName <- "activity.csv"
unzippedFile <- unz(zipFilePath, csvFileName)
rawActData <- read.csv(unzippedFile)
```

After loading the data, we can take a kick look at how the data looks like. For example, we can see the head of the dataset:


```r
head(rawActData)
```

```
##   steps       date interval
## 1    NA 2012-10-01        0
## 2    NA 2012-10-01        5
## 3    NA 2012-10-01       10
## 4    NA 2012-10-01       15
## 5    NA 2012-10-01       20
## 6    NA 2012-10-01       25
```

And, since we see some *NAs* in there, we can use *summary* in order to have some information about relevant parameters about the data:


```r
summary(rawActData)
```

```
##      steps                date          interval     
##  Min.   :  0.00   2012-10-01:  288   Min.   :   0.0  
##  1st Qu.:  0.00   2012-10-02:  288   1st Qu.: 588.8  
##  Median :  0.00   2012-10-03:  288   Median :1177.5  
##  Mean   : 37.38   2012-10-04:  288   Mean   :1177.5  
##  3rd Qu.: 12.00   2012-10-05:  288   3rd Qu.:1766.2  
##  Max.   :806.00   2012-10-06:  288   Max.   :2355.0  
##  NA's   :2304     (Other)   :15840
```

With this, we have a clear idea about how the data like, and we can move forward to the next step of the processing, which is calculating the mean total number of steps taken per day. No pre-processing has been needed, since the data seems to be in a pretty good shape. 

## What is mean total number of steps taken per day?
In order to get the mean total number of steps taken per day, I will follow the instructions in the description of the assessment. Besides, I will also ignore the missing values in the dataset.

1. Calculate the total number of steps taken per day: 
I'll use some of the functions that are available in the dplyr library, thus, I need to load this library first in order to make use of them. After that I will use a combination of summarise and group_by to get the total number of steps taken per day. Finally, I will use more 'friendly' names for the data.frame containing the total number of steps per day, so it can be used later to calculate the histogram. Again, I show the head of the data.frame with the total steps per day to see how it looks like.


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
totalStepsByDay <- summarise(group_by(rawActData,date),sum(steps))
names(totalStepsByDay) <- c("date","steps")
head(totalStepsByDay)
```

```
## Source: local data frame [6 x 2]
## 
##         date steps
## 1 2012-10-01    NA
## 2 2012-10-02   126
## 3 2012-10-03 11352
## 4 2012-10-04 12116
## 5 2012-10-05 13294
## 6 2012-10-06 15420
```


2. The next step is to make a histogram of the total number of steps taken each day
For this, I only need to plot the histogram of the total steps taken each day, usign *hist*. I've used 10 breaks since this value allows a clean representation of the histogram. Besides, I've used colors and put a nice main title and xaxis title, so the figure is more readable. I will use the base plotting system since it gives good enough results.


```r
hist(totalStepsByDay$steps,10, col="blue", main = "Histogram for the total number of steps taken each day", xlab="Total number of steps taken each day")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png) 

## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
