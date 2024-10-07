---
title: 'Week 5: Demographics'
author: Package Build
date: '2024-10-05'
slug: week-5-demographics
categories: []
tags: []
---




``` r
# Load in libraries
library(car)
```

```
## Loading required package: carData
```

``` r
library(caret)
```

```
## Loading required package: ggplot2
```

```
## Loading required package: lattice
```

``` r
library(CVXR)
```

```
## 
## Attaching package: 'CVXR'
```

```
## The following object is masked from 'package:stats':
## 
##     power
```

``` r
library(foreign)
library(glmnet)
```

```
## Loading required package: Matrix
```

```
## Loaded glmnet 4.1-8
```

``` r
library(haven)
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

``` r
library(kableExtra)
library(maps)
library(mlr3)
library(randomForest)
```

```
## randomForest 4.7-1.2
```

```
## Type rfNews() to see new features/changes/bug fixes.
```

```
## 
## Attaching package: 'randomForest'
```

```
## The following object is masked from 'package:ggplot2':
## 
##     margin
```

``` r
library(ranger)
```

```
## 
## Attaching package: 'ranger'
```

```
## The following object is masked from 'package:randomForest':
## 
##     importance
```

``` r
library(RColorBrewer)
library(sf)
```

```
## Linking to GEOS 3.11.0, GDAL 3.5.3, PROJ 9.1.0; sf_use_s2() is TRUE
```

``` r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ lubridate 1.9.3     ✔ tibble    3.2.1
## ✔ purrr     1.0.2     ✔ tidyr     1.3.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::combine()       masks randomForest::combine()
## ✖ tidyr::expand()        masks Matrix::expand()
## ✖ dplyr::filter()        masks stats::filter()
## ✖ dplyr::group_rows()    masks kableExtra::group_rows()
## ✖ dplyr::id()            masks CVXR::id()
## ✖ purrr::is_vector()     masks CVXR::is_vector()
## ✖ dplyr::lag()           masks stats::lag()
## ✖ purrr::lift()          masks caret::lift()
## ✖ purrr::map()           masks maps::map()
## ✖ randomForest::margin() masks ggplot2::margin()
## ✖ tidyr::pack()          masks Matrix::pack()
## ✖ dplyr::recode()        masks car::recode()
## ✖ purrr::some()          masks car::some()
## ✖ tidyr::unpack()        masks Matrix::unpack()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

``` r
library(viridis)
```

```
## Loading required package: viridisLite
## 
## Attaching package: 'viridis'
## 
## The following object is masked from 'package:maps':
## 
##     unemp
```

``` r
# Voterfile

# Loading in 1% voterfile
voterfile.sample.files <- list.files("state_1pc_samples_aug24")

# Making one voterfile dataset
voterfile.complete <- read_csv(paste0("state_1pc_samples_aug24/", voterfile.sample.files[1]))
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 7029 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
for (i in 2:length(voterfile.sample.files)) {
  temp <- read_csv(paste0("state_1pc_samples_aug24/",voterfile.sample.files[i]))
  voterfile.complete <- rbind(voterfile.complete, temp)
}
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 49546 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (19): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (8): svi_vh_2020pp_party, svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 26833 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 65896 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (19): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (8): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 308200 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 56291 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 32957 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 10658 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 216941 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 103165 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 11188 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 29728 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (19): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (8): svi_vh_2020pp_party, svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 15745 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 113382 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (19): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (8): svi_vh_2020pp_party, svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 63101 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2020pp_party, svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 26403 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 45265 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 41539 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 64215 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 58375 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## Rows: 14924 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (23): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (4): svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g, svi_vh_2024g
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 100527 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## Rows: 50590 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (23): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (4): svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g, svi_vh_2024g
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 57639 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2020pp_party, svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 28719 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (23): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (4): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023g, svi_vh_2024g
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 10268 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 101796 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 5956 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (19): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (8): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 16962 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2020pp_party, svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## Rows: 13017 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (23): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (4): svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g, svi_vh_2024g
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 84097 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 18327 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 30038 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (18): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (9): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## Rows: 167782 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (23): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (4): svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g, svi_vh_2024g
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 112444 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 34340 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (20): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (7): svi_vh_2020pp_party, svi_vh_2021p, svi_vh_2021p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 44102 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 118713 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## Rows: 10183 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (23): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (4): svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g, svi_vh_2024g
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 50621 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (23): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (4): svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g, svi_vh_2024g
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 8539 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (18): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (9): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 65825 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 253672 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 20310 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 81119 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 6576 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023g, svi_vh_2024pp_part...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 69830 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (18): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (9): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2022p_party, svi_v...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 85513 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 16631 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (22): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (5): svi_vh_2020pp_party, svi_vh_2023p, svi_vh_2023p_party, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 4518 Columns: 43
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (21): sii_state, sii_age_range, sii_gender, sii_race, svi_party_registra...
## dbl (16): sii_deceased, sii_age, sii_married, svi_vote_all_general, svi_vote...
## lgl  (6): svi_vh_2020pp_party, svi_vh_2021p_party, svi_vh_2023p, svi_vh_2023...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
# Analyzing homeownership in swing states (AZ, PA, GA, NV, MI, NC, WI) 


## Recodes homeownership on a 0-2 scale ~ 1 is renters, 2 is homeowners
voterfile.complete <- voterfile.complete %>% mutate(sii_homeowner=case_when(sii_homeowner == "H" ~ 2, sii_homeowner == "R" ~ 1, TRUE ~ 0)) 

#N.B. This section is repetitive for each state as I couldn't figure out a for loop
# Arizona (Repeats for each swing state; couldn't figure out a for loop)

# Homeowners and first-time voters
vf_az_subset_renters <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 1 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "AZ")

# Subset to see how many renters and first time voters
vf_az_subset_homeowners <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 2 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "AZ")

# number of first time renters voters
az_percent_homeowners <- count(vf_az_subset_homeowners) / count(voterfile.complete[voterfile.complete$sii_state == "AZ", ])
az_percent_renters <- count(vf_az_subset_renters) / count(voterfile.complete[voterfile.complete$sii_state == "AZ", ])

# Pennsylvania

# Homeowners and first-time voters
vf_pa_subset_renters <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 1 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "PA")

# Subset to see how many renters and first time voters
vf_pa_subset_homeowners <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 2 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "PA")

# number of first time renters voters
pa_percent_homeowners <- count(vf_pa_subset_homeowners) / count(voterfile.complete[voterfile.complete$sii_state == "PA", ])
pa_percent_renters <- count(vf_pa_subset_renters) / count(voterfile.complete[voterfile.complete$sii_state == "PA", ])

# Georgia

# Homeowners and first-time voters
vf_ga_subset_renters <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 1 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "GA")

# Subset to see how many renters and first time voters
vf_ga_subset_homeowners <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 2 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "GA")

# number of first time renters voters
ga_percent_homeowners <- count(vf_ga_subset_homeowners) / count(voterfile.complete[voterfile.complete$sii_state == "GA", ])
ga_percent_renters <- count(vf_ga_subset_renters) / count(voterfile.complete[voterfile.complete$sii_state == "GA", ])

# Nevada

# Homeowners and first-time voters
vf_nv_subset_renters <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 1 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "NV")

# Subset to see how many renters and first time voters
vf_nv_subset_homeowners <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 2 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "NV")

# number of first time renters voters
nv_percent_homeowners <- count(vf_nv_subset_homeowners) / count(voterfile.complete[voterfile.complete$sii_state == "NV", ])
nv_percent_renters <- count(vf_nv_subset_renters) / count(voterfile.complete[voterfile.complete$sii_state == "NV", ])

# Michigan

# Homeowners and first-time voters
vf_mi_subset_renters <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 1 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "MI")

# Subset to see how many renters and first time voters
vf_mi_subset_homeowners <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 2 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "MI")

# number of first time renters voters
mi_percent_homeowners <- count(vf_mi_subset_homeowners) / count(voterfile.complete[voterfile.complete$sii_state == "MI", ])
mi_percent_renters <- count(vf_mi_subset_renters) / count(voterfile.complete[voterfile.complete$sii_state == "MI", ])

# North Carolina

# Homeowners and first-time voters
vf_nc_subset_renters <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 1 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "NC")

# Subset to see how many renters and first time voters
vf_nc_subset_homeowners <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 2 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "NC")

# number of first time renters voters
nc_percent_homeowners <- count(vf_nc_subset_homeowners) / count(voterfile.complete[voterfile.complete$sii_state == "NC", ])
nc_percent_renters <- count(vf_nc_subset_renters) / count(voterfile.complete[voterfile.complete$sii_state == "NC", ])

# Wisconsin

# Homeowners and first-time voters
vf_wi_subset_renters <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 1 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "WI")

# Subset to see how many renters and first time voters
vf_wi_subset_homeowners <- subset(voterfile.complete, voterfile.complete$svi_vote_all_general_pres == 0 & voterfile.complete$sii_homeowner == 2 & voterfile.complete$sii_deceased == 0 & voterfile.complete$sii_state == "WI")

# number of first time renters voters
wi_percent_homeowners <- count(vf_wi_subset_homeowners) / count(voterfile.complete[voterfile.complete$sii_state == "WI", ])
wi_percent_renters <- count(vf_wi_subset_renters) / count(voterfile.complete[voterfile.complete$sii_state == "WI", ])





# Create table to get other demographics (Age and Marriage)

age_marraiage_voterstats  <- voterfile.complete %>%
     group_by(sii_state) %>%
     summarize(mean_age = mean(sii_age, na.rm = TRUE), mean_married = mean(sii_married, na.rm = TRUE))



# Get the states map
states_map <- map_data("state")


# Creating voterfile statistics dataset to merge onto states map (I decided to hard code the variables because I wanted to see ever state on the map)
voterfile_stats <- data.frame(region = c("alabama", "arizona", "arkansas", "california", "colorado", "connecticut", "delaware", "florida", "georgia", "idaho", "illinois", "indiana", "iowa", "kansas", "kentucky", "louisiana", "maine", "maryland", "massachusetts", "michigan", "minnesota", "mississippi", "missouri", "montana", "nebraska", "nevada", "new hampshire", "new jersey", "new mexico", "new york", "north carolina", "north dakota", "ohio", "oklahoma", "oregon", "pennsylvania", "rhode island", "south carolina", "south dakota", "tennessee", "texas", "utah", "vermont", "virginia", "washington", "west virginia", "wisconsin", "wyoming"), percent_renters = c(0, 6.32, 0, 0, 0, 0, 0, 0, 4.55, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 3.28, 0, 0, 0, 0, 0, 72.2, 0, 0, 0, 0, 3.86, 0, 0, 0, 0, 3.33, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1.71, 0), percent_homeowners = c(0, 21.1, 0, 0, 0, 0, 0, 0, 21.4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 21.4, 0, 0, 0, 0, 0, 23.2, 0, 0, 0, 0, 18.8, 0, 0, 0, 0, 21.5, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 10.7, 0), age = c(51.49048, 52.12933, 51.46218, 51.20815, 48.76015, 52.78880, 53.75013, 53.12383, 49.11917, 51.34345, 53.09734, 51.55012, 51.70926, 51.91467, 51.72577, 51.31758, 51.36451, 51.49227, 54.27671, 51.27594, 52.29159, 51.04434, 57.96184, 52.55765, 50.26209, 58.67459, 51.57028, 58.87460, 51.66325, 52.37447, 49.55601, 52.23367, 52.11677, 52.01195, 50.74921, 52.42373, 51.24957, 52.94089, 57.14923, 51.59457, 49.26600, 50.81513, 50.29708, 52.96750, 51.09090, 61.30506, 52.15955, 57.95986), marriage = c(0.4540023, 0.4238810, 0.3750152, 0.3609961, 0.4221279, 0.4108384, 0.4194033, 0.3963197, 0.4210343, 0.5021192, 0.5326135, 0.4307386, 0.4718467, 0.4920653, 0.4640893, 0.4236982, 0.4157751, 0.4119058, 0.4098767, 0.4725696, 0.4801542, 0.4568782, 0.2946830, 0.4302688, 0.4302920, 0.3770987, 0.4865582, 0.3912576, 0.3989679, 0.3633983, 0.3205606, 0.3569513, 0.4526876, 0.4156086, 0.3695071, 0.4358748, 0.3863302, 0.4904684, 0.3694812, 0.4554652, 0.4176023, 0.4085672, 0.4426213, 0.3897506, 0.4114707, 0.3471870, 0.4410438, 0.3466135))

# Merge onto states_map
voterstats_map <- merge(states_map, voterfile_stats, by = "region")

# Maps of Demographics
my_custom_theme <- 
  theme_light() + 
  theme(panel.border = element_blank(),
        plot.title = element_text(size = 15, hjust = 0.5), 
        axis.text = element_blank(),
        strip.text = element_text(size = 18),
        legend.title = element_text(size = 8),
        legend.text = element_text(size = 7),
        text = element_text(family = "Georgia"),
        axis.line = element_blank(), 
        axis.ticks = element_blank(), 
        axis.title = element_blank())

# Map of Age of Registered Voters
voterstats_map |> 
     ggplot(aes(long, lat, group = group)) + 
     geom_polygon(aes(fill = age)) + scale_fill_gradient(name = "% Married", low = "white", high = "lightblue", na.value = NA,) + my_custom_theme + theme(panel.background = element_rect(fill = "lightgrey"))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

``` r
# Map of Married Registered Voters
voterstats_map |> 
     ggplot(aes(long, lat, group = group)) + 
     geom_polygon(aes(fill = marriage)) + scale_fill_gradient(name = "% Married", low = "white", high = "lightblue", na.value = NA,) + my_custom_theme + theme(panel.background = element_rect(fill = "lightgrey"))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-2.png" width="672" />

``` r
# Map of % of First-Time voters who are renters or homeowners
voterstats_map |> 
     ggplot(aes(long, lat, group = group)) + 
     geom_polygon(aes(fill = percent_renters + percent_homeowners)) + scale_colour_manual(values = c(0:100)) + scale_fill_gradient(name = "% First-Time Voters Renters or Homeowners", low = "white", high = "red", na.value = NA) + my_custom_theme + theme(panel.background = element_rect(fill = "lightgrey"))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-3.png" width="672" />










``` r
d_popvote <- read_csv("popvote_1948_2020.csv")
```

```
## Rows: 40 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): party, candidate
## dbl (5): year, pv, pv2p, deminc, juneapp
## lgl (4): winner, incumbent, incumbent_party, prev_admin
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
d_fred <- read_csv("fred_econ copy.csv")
```

```
## Rows: 387 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (14): year, quarter, GDP, GDP_growth_quarterly, RDPI, RDPI_growth_quarte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
d_fred$sp500move <- d_fred$sp500_high - d_fred$sp500_low
d_fred_housing <- read_csv("fred_housing.csv")
```

```
## Rows: 284 Columns: 5
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl  (4): homeowner_vacancy, year, quarter, rental_vacancy
## date (1): observation_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
fundamentals <- d_popvote |> 
  filter(incumbent_party == TRUE) |> 
  select(year, pv, pv2p, winner) |> 
  left_join(d_fred |> filter(quarter == 2)) |> 
  left_join(d_fred_housing |> filter(quarter == 2))
```

```
## Joining with `by = join_by(year)`
## Joining with `by = join_by(year, quarter)`
```

``` r
# Training set with 2020
fund_train <- fundamentals |> 
  filter(year < 2024 & year > 1952)
# Training set without 2020
fund_train_2 <- fundamentals |> 
  filter(year < 2024 & year > 1952 & year != 2020)
fund_test <- fundamentals |> 
  filter(year == 2024)

# With 2020
fund_model <- lm(pv2p ~ GDP_growth_quarterly + sp500move + CPI + homeowner_vacancy + rental_vacancy, data = fund_train)
summary(fund_model)
```

```
## 
## Call:
## lm(formula = pv2p ~ GDP_growth_quarterly + sp500move + CPI + 
##     homeowner_vacancy + rental_vacancy, data = fund_train)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -6.809 -2.962  1.341  2.447  7.302 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          57.45722    6.40693   8.968 2.17e-06 ***
## GDP_growth_quarterly  0.48383    0.24827   1.949   0.0773 .  
## sp500move             0.03630    0.03669   0.989   0.3438    
## CPI                  -0.02919    0.03548  -0.823   0.4281    
## homeowner_vacancy    -1.16095    4.90204  -0.237   0.8171    
## rental_vacancy       -0.37101    1.16174  -0.319   0.7554    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.921 on 11 degrees of freedom
## Multiple R-squared:  0.3897,	Adjusted R-squared:  0.1123 
## F-statistic: 1.405 on 5 and 11 DF,  p-value: 0.2959
```

``` r
fund.predict <- predict(fund_model, fund_test)

# Without 2020
fund_model_2 <- lm(pv2p ~ GDP_growth_quarterly + sp500move + CPI + homeowner_vacancy + rental_vacancy, data = fund_train_2)
summary(fund_model_2)
```

```
## 
## Call:
## lm(formula = pv2p ~ GDP_growth_quarterly + sp500move + CPI + 
##     homeowner_vacancy + rental_vacancy, data = fund_train_2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -7.0330 -2.4816  0.3904  2.9747  6.7620 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)          53.56635    6.96324   7.693 1.66e-05 ***
## GDP_growth_quarterly  0.71337    0.30275   2.356   0.0402 *  
## sp500move            -0.01808    0.05602  -0.323   0.7535    
## CPI                  -0.01411    0.03658  -0.386   0.7077    
## homeowner_vacancy     0.55143    4.96518   0.111   0.9138    
## rental_vacancy       -0.30369    1.13308  -0.268   0.7941    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.794 on 10 degrees of freedom
## Multiple R-squared:  0.4469,	Adjusted R-squared:  0.1704 
## F-statistic: 1.616 on 5 and 10 DF,  p-value: 0.2421
```

``` r
fund2.predict <- predict(fund_model_2, fund_test)


# Polling Data Based Prediction

polling <- read_csv("national_polls_1968-2024 copy.csv")
```

```
## Rows: 7378 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): state, party, candidate
## dbl  (4): year, weeks_left, days_left, poll_support
## lgl  (1): before_convention
## date (1): poll_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
# Adjust popular vote dataset for merging
d_popvote$party[d_popvote$party == "democrat"] <- "DEM"
d_popvote$party[d_popvote$party == "republican"] <- "REP"

# Create dataset of polling average by week until the election. 
d_poll_weeks <- polling |> 
  group_by(year, party, weeks_left) |>
  summarize(mean_poll_week = mean(poll_support)) |> 
  filter(weeks_left <= 30 & party == "DEM") |> 
  pivot_wider(names_from = weeks_left, values_from = mean_poll_week) |> 
  left_join(d_popvote, by = c("year", "party"))
```

```
## `summarise()` has grouped output by 'year', 'party'. You can override using the
## `.groups` argument.
```

``` r
# Split into training and testing data based on inclusion or exclusion of 2024. 
d_poll_weeks_train <- d_poll_weeks |> 
  filter(year <= 2020)
d_poll_weeks_test <- d_poll_weeks |> 
  filter(year == 2024)

# Extra training set without 2016 and 2020 (Removing years that the polling "went wrong")
d_poll_weeks_train2 <- d_poll_weeks |> 
  filter(year <= 2012)

colnames(d_poll_weeks)[3:33] <- paste0("poll_weeks_left_", 0:30)
colnames(d_poll_weeks_train)[3:33] <- paste0("poll_weeks_left_", 0:30)
colnames(d_poll_weeks_train2)[3:33] <- paste0("poll_weeks_left_", 0:30)
colnames(d_poll_weeks_test)[3:33] <- paste0("poll_weeks_left_", 0:30)

# Normal training and testing
x.train <- d_poll_weeks_train |>
  ungroup() |> 
  select(all_of(paste0("poll_weeks_left_", 7:30))) |> 
  as.matrix()
y.train <- d_poll_weeks_train$pv2p
x.test <- d_poll_weeks_test |>
  ungroup() |> 
  select(all_of(paste0("poll_weeks_left_", 7:30))) |> 
  as.matrix()

# Training without 2016 and 2020
x.train2 <- d_poll_weeks_train2 |>
  ungroup() |> 
  select(all_of(paste0("poll_weeks_left_", 7:30))) |> 
  as.matrix()
y.train2 <- d_poll_weeks_train2$pv2p

# Using elastic-net for normal poll predictions
set.seed(02138)
enet.poll <- cv.glmnet(x = x.train, y = y.train, alpha = 0.5)
```

```
## Warning: Option grouped=FALSE enforced in cv.glmnet, since < 3 observations per
## fold
```

``` r
lambda.min.enet.poll <- enet.poll$lambda.min

# Predict 2024 national pv2p share
poll.predict <- (predict(enet.poll, s = lambda.min.enet.poll, newx = x.test))


# Predicting with excluded data
set.seed(02138)
enet.poll2 <- cv.glmnet(x = x.train2, y = y.train2, alpha = 0.5)
```

```
## Warning: Option grouped=FALSE enforced in cv.glmnet, since < 3 observations per
## fold
```

``` r
lambda.min.enet.poll2 <- enet.poll2$lambda.min

# Predict 2024 national pv2p share using elastic-net. 
poll.predict2 <- (predict(enet.poll2, s = lambda.min.enet.poll2, newx = x.test))

# Ensemble Prediction
ensemble_with_all <- (fund.predict * 2/3 + poll.predict * 1/3)
ensemble_without_outliers <- (fund2.predict * 2/3 + poll.predict2 * 1/3)
```





