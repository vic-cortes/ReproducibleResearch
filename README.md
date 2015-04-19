# Reproducible Research
This file contains the **Peer Assessment 1** of the Reproducible Research


## Loading and preprocessing the data
First we have to set the work directory and load the data, then we transform the **date** variable "factor" to "Date". Also we have to remove all the **NA's** of the data set. 
````{r}
setwd("C:/Users/Vic/Documents/Coursera Courses/Data Analysis Specialization/Reproducible Research/Week 2")
dat <- read.csv("activity.csv")
NAnum <- sum(is.na(dat[,1]))
dat[,2] <- as.Date(dat[,2])
dat[,3] <- as.factor(dat[,3])
dat <- dat[!is.na(dat[,1]),] #Remove all the NA's of the first column of the dataset
head(dat)
````


## Total number of steps taken per day

In order to see the total steps per day, we use **tapply**. Now we can visualized the data with a bar plot.   

````{r}
stepsDay <- tapply(dat[,1],dat[,2],sum)
par(mfrow = c(1,2))
barplot(stepsDay, main="Barplot - Total steps per day")
hist(stepsDay, main = "Histogram - Total Steps per day")
````

We can compute the **mean** and **median** of the total number of steps per day

```{r}
mean(stepsDay)
median(stepsDay)

```


## Daily activity pattern

```{r}
intLab <- as.character(unique(dat[,3]))
meanInt <- tapply(dat[,1],dat[,3],mean)
plot( meanInt, type ='l',main = "Daily activity pattern",xlab = "Interval", ylab = "Mean steps", xaxt='n')

```

## Imputing missin values
We can know the total of **NA's** of the first column.
```{r, echo=FALSE}
print(NAnum)
```

