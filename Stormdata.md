Storm Data Analysis - Types of Event


Sysnopis
This is an R Markdown document which is used to analyze the Storm Data based on the National Weather Service Storm Data. The document is focus in answering the two question which are:

1. Across the United States, which types of events (as indicated in the EVTYPE variable) are most harmful with respect to population health?

2. Across the United States, which types of events have the greatest economic consequences? 
The basic goal of this document is to explore the NOAA Storm Database and understand some basic concepts about weather events.

Data Processing
Set the working directory:

my.path <- "D:/Online Courses/Coursera/Data Science/5. Reproducible Research/Lab/Lab 2";
setwd(my.path);
Downloading data from the website: Storm Data

or you can download file using the file URL

fileUrl <- "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2FStormData.csv.bz2";
fileZip <- "./repdata-data-StormData.csv.bs2";
if (file.exists(fileZip) == F) {
    download.file(fileUrl, fileZip, mode = "wb")
}
Reading data from the raw file:

data <- read.csv("repdata-data-StormData.csv.bz2", header = TRUE, sep=",")
Question 1: Across the United States, which types of events (as indicated in the EVTYPE variable) are most harmful with respect to population health?
Find the most harmful with respect to population health by FALITIES and INJURIES variable

harm <- data$FATALITIES + data$INJURIES
maxharm <- max(harm)
maxharm
## [1] 1742
Subsetting data to find the most harmful with respect to population health

mostharm <- data$EVTYPE[which(data$INJURIES + data$FATALITIES == maxharm)]
mostharm
## [1] TORNADO
## 985 Levels:    HIGH SURF ADVISORY  COASTAL FLOOD ... WND
Question 2: Across the United States, which types of events have the greatest economic consequences?
Property Damage estimate in Billion dollar

prop <- data$PROPDMG[which(data$PROPDMGEXP == "B")]
prop
##  [1]   5.00   0.10   2.10   1.60   1.00   5.00   2.50   1.20   3.00   1.70
## [11]   3.00   1.50   5.15   1.00   1.04   2.50   5.42   1.30   4.83   4.00
## [21]   1.00   1.50  10.00  16.93  31.30   4.00   7.35  11.26   5.88   2.09
## [31] 115.00   1.00   4.00   1.50   1.80   1.00   1.50   2.80   1.00   2.00
The maximum property damage:

a <- max(prop)
a
## [1] 115
Crop Damage estimate in Billion dollar

crop <- data$CROPDMG[which(data$CROPDMGEXP == "B")]
crop
## [1] 0.40 5.00 0.50 0.20 5.00 1.51 1.00 0.00 0.00
The maximum property damage:

b <- max(crop)
b
## [1] 5
We can clearly see that the property damage is 115 billion dollar, which is the the largest amount.

The type of event which creates the greatest economic consequences:

econ <- data$EVTYPE[which((data$PROPDMG == a) & (data$PROPDMGEXP == "B"))]
econ
## [1] FLOOD
## 985 Levels:    HIGH SURF ADVISORY  COASTAL FLOOD ... WND
Plotting
Number of injuries and fatalities caused by Storm

tornado <- data[which(data$EVTYPE == "TORNADO"),]
par(mfrow=c(1,2))
boxplot(tornado$INJURIES, main ="Injuries caused by Tornado"
        ,xlab="Storm", ylab="Number of Injuries")
boxplot(tornado$FATALITIES, main ="Fatalities caused by Tornado"
        ,xlab="Storm", ylab="Number of Injuries")
plot of chunk unnamed-chunk-11

The Property Damage caused by Flood

boxplot(data$PROPDMG[data$EVTYPE=="FLOOD"]
        , main ="Property Damage caused by Flood"
        ,xlab="FLOOD", ylab="Billions of Dollar")
plot of chunk unnamed-chunk-12

Results
Question 1: Across the United States, which types of events (as indicated in the EVTYPE variable) are most harmful with respect to population health?

mostharm <- data$EVTYPE[which(data$INJURIES + data$FATALITIES == maxharm)]
mostharm
## [1] TORNADO
## 985 Levels:    HIGH SURF ADVISORY  COASTAL FLOOD ... WND
The answer is TORNADO.

Question 2: Across the United States, which types of events have the greatest economic consequences?

econ <- data$EVTYPE[which((data$PROPDMG == a) & (data$PROPDMGEXP == "B"))]
econ
## [1] FLOOD
## 985 Levels:    HIGH SURF ADVISORY  COASTAL FLOOD ... WND
The answer is FLOOD.
