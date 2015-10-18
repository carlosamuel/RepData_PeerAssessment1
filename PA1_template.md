# Peer Assessment 1
By Carlos Figueroa

Setting Global Options for always show code:


```r
knitr::opts_chunk$set(echo=TRUE)
```

Reading data from working directory:


```r
data<-read.csv("repdata-data-activity\\activity.csv", na.strings="NA")
```

```
## Warning in file(file, "rt"): cannot open file 'repdata-data-activity
## \activity.csv': No such file or directory
```

```
## Error in file(file, "rt"): cannot open the connection
```

Data summary (includes count of NA's):


```r
summary(data)
```

```
## Error in object[[i]]: object of type 'closure' is not subsettable
```

```r
str(data)
```

```
## function (..., list = character(), package = NULL, lib.loc = NULL, 
##     verbose = getOption("verbose"), envir = .GlobalEnv)
```

Summarizing steps by day and plotting histogram (Choosing not to ignore NA's since we can or cannot):


```r
library(plyr)
y<-ddply(data, ~date, summarise, sum=sum(steps))
```

```
## Error in if (empty(.data)) return(.data): missing value where TRUE/FALSE needed
```

```r
y
```

```
## Error in eval(expr, envir, enclos): object 'y' not found
```

```r
hist(y$sum)
```

```
## Error in hist(y$sum): object 'y' not found
```

Summarizing steps by day and calculating mean and median for each one (Choosing not to ignore NA's since we can or cannot):


```r
x<-ddply(data, ~date, summarise, mean=mean(steps), median=median(steps))
```

```
## Error in if (empty(.data)) return(.data): missing value where TRUE/FALSE needed
```

```r
x
```

```
## Error in eval(expr, envir, enclos): object 'x' not found
```

Summarizing steps by 5-minute interval and calculating mean (changing NA's to zeros which counts for the "Imputing missing values" and creating a new data set ): 


```r
newdata<-data
summary(newdata)
```

```
## Error in object[[i]]: object of type 'closure' is not subsettable
```

```r
## Same as the original data
newdata[is.na(newdata)]<-0
```

```
## Warning in is.na(newdata): is.na() applied to non-(list or vector) of type
## 'closure'
```

```
## Error in newdata[is.na(newdata)] <- 0: object of type 'closure' is not subsettable
```

```r
z<-ddply(newdata, ~interval, summarise, mean=mean(steps))
```

```
## Error in if (empty(.data)) return(.data): missing value where TRUE/FALSE needed
```

```r
z
```

```
## Error in eval(expr, envir, enclos): object 'z' not found
```

Plotting mean steps by interval:


```r
with(z, {plot(interval, mean, type="l")})
```

```
## Error in with(z, {: object 'z' not found
```

The maximum mean is on interval 835

The total number of NA's was already informed in the summary after reading data, there are 2,304 lines with NA, a new set with imputation was created also prevously for summarizing data by interval and step average so will go straight to the new mean, median and histogram


Strategy
I replaced all NA's with zeros because I assume they came from a non measure caused by inmovility, i.e. the test subject was still for a long time inducing a measurement error which caused NA instead of zero


Histogram


```r
y2<-ddply(newdata, ~date, summarise, sum=sum(steps))
```

```
## Error in if (empty(.data)) return(.data): missing value where TRUE/FALSE needed
```

```r
y2
```

```
## Error in eval(expr, envir, enclos): object 'y2' not found
```

```r
hist(y2$sum)
```

```
## Error in hist(y2$sum): object 'y2' not found
```


Mean and median


```r
x2<-ddply(newdata, ~date, summarise, mean=mean(steps), median=median(steps))
```

```
## Error in if (empty(.data)) return(.data): missing value where TRUE/FALSE needed
```

```r
x2
```

```
## Error in eval(expr, envir, enclos): object 'x2' not found
```

There is no difference because of the specific way I did Things (sorry, didnt' read the whole assignment first) but as we replace NA's with imputed values above or below the mean we slightly increase or decrase it (in this case, as I used zeros, everything decrease)


Since Im in a hurry i will skip the last part, sorry, my bad! :( 

