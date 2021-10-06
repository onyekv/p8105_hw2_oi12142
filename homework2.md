p8105\_hw2\_oi2142
================

## Problem 1:

-Reading and cleaning Mr. Trash Wheel data set using read\_excel and
janitor::clean\_names()

-Omitting rows that d o not include dumpster specific data

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library (readxl)
```

``` r
trash_wheel = 
  read_excel("./data/mr_trash_wheel.xlsx", sheet = "Mr. Trash Wheel", range = "a2:n408")

trash_wheel = 
    janitor::clean_names(trash_wheel)

trash_wheel = drop_na(trash_wheel)
```

Rounding the number of sports balls to nearest integer

``` r
trash_wheel$sports_balls <- round(trash_wheel$sports_balls)
trash_wheel
```

    ## # A tibble: 344 × 14
    ##    dumpster month  year date                weight_tons volume_cubic_yards
    ##       <dbl> <chr> <dbl> <dttm>                    <dbl>              <dbl>
    ##  1        1 May    2014 2014-05-16 00:00:00        4.31                 18
    ##  2        2 May    2014 2014-05-16 00:00:00        2.74                 13
    ##  3        3 May    2014 2014-05-16 00:00:00        3.45                 15
    ##  4        4 May    2014 2014-05-17 00:00:00        3.1                  15
    ##  5        5 May    2014 2014-05-17 00:00:00        4.06                 18
    ##  6        6 May    2014 2014-05-20 00:00:00        2.71                 13
    ##  7        7 May    2014 2014-05-21 00:00:00        1.91                  8
    ##  8        8 May    2014 2014-05-28 00:00:00        3.7                  16
    ##  9        9 June   2014 2014-06-05 00:00:00        2.52                 14
    ## 10       10 June   2014 2014-06-11 00:00:00        3.76                 18
    ## # … with 334 more rows, and 8 more variables: plastic_bottles <dbl>,
    ## #   polystyrene <dbl>, cigarette_butts <dbl>, glass_bottles <dbl>,
    ## #   grocery_bags <dbl>, chip_bags <dbl>, sports_balls <dbl>,
    ## #   homes_powered <dbl>

-   Reading & Cleaning Precipitation 2018

``` r
precipation_2018 = 
  read_excel("./data/mr_trash_wheel.xlsx", sheet = "2018 Precipitation", range = "a2:B14") 

precipation_2018 = 
  janitor::clean_names(precipation_2018)

precipation_2018$year <- 2018
  
precipation_2018  
```

    ## # A tibble: 12 × 3
    ##    month total  year
    ##    <dbl> <dbl> <dbl>
    ##  1     1  0.94  2018
    ##  2     2  4.8   2018
    ##  3     3  2.69  2018
    ##  4     4  4.69  2018
    ##  5     5  9.27  2018
    ##  6     6  4.77  2018
    ##  7     7 10.2   2018
    ##  8     8  6.45  2018
    ##  9     9 10.5   2018
    ## 10    10  2.12  2018
    ## 11    11  7.82  2018
    ## 12    12  6.11  2018

-   Reading & Cleaning Precipitation 2019

``` r
precipation_2019 = 
  read_excel("./data/mr_trash_wheel.xlsx", sheet = "2019 Precipitation", range = "a2:b8") 

precipation_2019 = 
  janitor::clean_names(precipation_2019)

 precipation_2019$year <- 2019
  precipation_2019  
```

    ## # A tibble: 6 × 3
    ##   month total  year
    ##   <dbl> <dbl> <dbl>
    ## 1     1  3.1   2019
    ## 2     2  3.64  2019
    ## 3     3  4.47  2019
    ## 4     4  1.46  2019
    ## 5     5  3.58  2019
    ## 6     6  0.42  2019
