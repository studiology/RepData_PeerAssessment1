# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
Load data from `activity.csv` - if not present in working directory, unzip `activity.zip`. If neither are present or unzipping fails, throw an error.

```r
if (!file.exists('activity.csv')) {
    # CSV is not in the working directory - unzip if possible
    if (!file.exists('activity.zip')) {
        # neither CSV nor ZIP are in the working directory
        errmsg <- paste('activity file was not found in',getwd())
        stop(errmsg)
    }
    # unzip activity.csv from activity.zip
    filesUnzipped <- unzip('activity.zip')
    if (!'./activity.csv' %in% filesUnzipped) {
        errmsg <- paste(
            file.path(getwd(),'activity.zip'),
            'did not contain activity.csv or something went wrong unzipping.\n',
            'Check the zip, and try unzipping manually before trying again'
            )
        stop(errmsg)
    }
    rm(filesUnzipped)
}
activity <- read.csv('activity.csv',stringsAsFactors=FALSE)
```

Preprocess by converting string dates and integer times to POSIXct datetimes. This step requires the [Lubridate][Lubridate] package. If not present, install it using `install.packages('lubridate')`. Lubridate requires R Version >= 3.0.0 - This document was knitted on R version 3.2.1 (2015-06-18).

```r
if (!require(lubridate)) {
    stop('Lubridate package not installed')
}
```

```
## Loading required package: lubridate
```

```r
activity$ymdhm <- paste(activity$date,formatC(x=activity$interval,width=4,flag='0',format='d'))
activity$datetime <- ymd_hm(activity$ymdhm)
```




## What is mean total number of steps taken per day?



## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?


## References
[Lubridate]: https://cran.r-project.org/package=lubridate "Lubridate package at CRAN"
