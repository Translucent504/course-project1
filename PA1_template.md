---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

```r
library(tidyverse)
```

```
## -- Attaching packages ------------------------------------------------------------ tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.0     v purrr   0.3.3
## v tibble  3.0.0     v dplyr   0.8.5
## v tidyr   1.0.2     v stringr 1.4.0
## v readr   1.3.1     v forcats 0.5.0
```

```
## -- Conflicts --------------------------------------------------------------- tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```
## Loading and preprocessing the data

```r
data <- tbl_df(read.csv("activity.csv"))
```

## What is mean total number of steps taken per day?

```r
hist(data$steps)
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
mean(data$steps, na.rm = TRUE)
```

```
## [1] 37.3826
```

```r
median(data$steps, na.rm = TRUE)
```

```
## [1] 0
```

## What is the average daily activity pattern?
Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
data <- group_by(data, interval)
tmp <- summarize(data, mean(steps, na.rm = TRUE))
names(tmp) <- c("interval", "avgsteps")
ggplot(tmp, aes(interval, avgsteps)) + geom_line() + xlab("Interval") + ylab("Average Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
top_n(tmp, 1)
```

```
## Selecting by avgsteps
```

```
## # A tibble: 1 x 2
##   interval avgsteps
##      <int>    <dbl>
## 1      835     206.
```
The interval **835** has the highest average steps taken at **206**.


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
