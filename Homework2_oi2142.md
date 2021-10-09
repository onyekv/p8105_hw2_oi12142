Onyeka Isamah, oi2142, Homework 2
================

## Problem 1, Mr Trash Wheel Dataset:

\#Reading and cleaning Mr. Trash Wheel data set using read\_excel and
janitor::clean\_names()

\#Omitting rows that do not include dumpster specific data

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
library(skimr)
```

``` r
trash_wheel = 
  read_excel("./data/NEW_mr_trash_wheel", sheet = "Mr. Trash Wheel", range = "a2:n408")
trash_wheel = 
    janitor::clean_names(trash_wheel)
trash_wheel = drop_na(trash_wheel)
```

\# Rounding the number of sports balls to nearest integer

``` r
trash_wheel$sports_balls <- round(trash_wheel$sports_balls)
trash_wheel
```

    ## # A tibble: 345 × 14
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
    ## # … with 335 more rows, and 8 more variables: plastic_bottles <dbl>,
    ## #   polystyrene <dbl>, cigarette_butts <dbl>, glass_bottles <dbl>,
    ## #   grocery_bags <dbl>, chip_bags <dbl>, sports_balls <dbl>,
    ## #   homes_powered <dbl>

\# Reading & Cleaning Precipitation 2018

``` r
precipitation_2018 = 
  read_excel("./data/mr_trash_wheel.xlsx", sheet = "2018 Precipitation", range = "a2:B14")

precipitation_2018 = 
  janitor::clean_names(precipitation_2018)

precipitation_2018$year <- 2018
  
precipitation_2018  
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

\#Reading & Cleaning Precipitation 2019

``` r
precipitation_2019 = 
  read_excel("./data/mr_trash_wheel.xlsx", sheet = "2019 Precipitation", range = "a2:b8") 

precipitation_2019 = 
  janitor::clean_names(precipitation_2019)

precipitation_2019$year <- 2019
  precipitation_2019  
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

\#Combining precipitation datasets

``` r
combined_precipitation <- bind_rows(precipitation_2018, precipitation_2019)
                                   
combined_precipitation<- mutate (combined_precipitation, MonthName = month.name[month])

combined_precipitation
```

    ## # A tibble: 18 × 4
    ##    month total  year MonthName
    ##    <dbl> <dbl> <dbl> <chr>    
    ##  1     1  0.94  2018 January  
    ##  2     2  4.8   2018 February 
    ##  3     3  2.69  2018 March    
    ##  4     4  4.69  2018 April    
    ##  5     5  9.27  2018 May      
    ##  6     6  4.77  2018 June     
    ##  7     7 10.2   2018 July     
    ##  8     8  6.45  2018 August   
    ##  9     9 10.5   2018 September
    ## 10    10  2.12  2018 October  
    ## 11    11  7.82  2018 November 
    ## 12    12  6.11  2018 December 
    ## 13     1  3.1   2019 January  
    ## 14     2  3.64  2019 February 
    ## 15     3  4.47  2019 March    
    ## 16     4  1.46  2019 April    
    ## 17     5  3.58  2019 May      
    ## 18     6  0.42  2019 June

The Mr. Trashwheel dataset has 345 observations and 14 variables. The
variables account for each `dumpster` number, `weight`, and `volume` as
well as the `month`, `year`, and `date`. The dataset also includes
variables of the type of trash: `plastic`, `polystyrene`,
`cigarette_butts`, `glass_bottles`, `grocery_bags`, `chip_bags`, and
`sports_balls`.

The Precipiation data set has 18 observations for the amount of rainfall
that occurred and 4 variables - which were `month`, `year`, and the
`total` amount of rainfall.

Find sum and median\*\*

### Problem 2 - FiveThirtyEight Dataset

\#\#\#Clean the data in pols-month.csv.

``` r
pols_df = 
  read_csv(file = "./data/fivethirtyeight_datasets/pols-month.csv") %>% 
  
  separate(mon, c("year", "month", "day")) %>% 
  
  mutate(
    month = month.name[as.numeric(month)],

    president = recode(prez_dem, "0" = "gop", "1"="dem"))   
```

    ## Rows: 822 Columns: 9

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl  (8): prez_gop, gov_gop, sen_gop, rep_gop, prez_dem, gov_dem, sen_dem, r...
    ## date (1): mon

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
    pols_df = select(pols_df, -prez_dem, -prez_gop, -day)
```

\#\#\# Cleaning the snp\_csv file

``` r
snp_df = 
  read_csv(file = "./data/fivethirtyeight_datasets/snp.csv")
```

    ## Rows: 787 Columns: 2

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): date
    ## dbl (1): close

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
  janitor::clean_names(snp_df)  
```

    ## # A tibble: 787 × 2
    ##    date    close
    ##    <chr>   <dbl>
    ##  1 7/1/15  2080.
    ##  2 6/1/15  2063.
    ##  3 5/1/15  2107.
    ##  4 4/1/15  2086.
    ##  5 3/2/15  2068.
    ##  6 2/2/15  2104.
    ##  7 1/2/15  1995.
    ##  8 12/1/14 2059.
    ##  9 11/3/14 2068.
    ## 10 10/1/14 2018.
    ## # … with 777 more rows

``` r
snp_df=  separate(snp_df, "date", into =  c("month", "day", "year"), convert = TRUE) %>% 
  mutate( 
    year, year = if_else( year<= 15, year + 2000, year + 1900)) %>% 
      arrange(year, month, .by_group = TRUE) %>% 
 mutate(
    year = as.character(year),  
      month = month.name[as.numeric(month)], 
      month = str_to_lower(month))
```

\#\#\# Tidying unemployment data, before merging

``` r
unemployment_df = 
  read_csv("./data/fivethirtyeight_datasets/unemployment.csv") %>% 

  janitor::clean_names() %>% 
  
  pivot_longer(jan:dec,
    names_to = "month", 
    values_to = "unemployment") %>% 

  mutate(
  
  month = recode(month, 
    jan = "january", feb = "february", mar = "march", apr = "april", may = "may", jun = "june", jul = "july", aug =  "august", sep = "september", nov = "november", dec = "december"),
  
    year = as.character(year)
)
```

    ## Rows: 68 Columns: 13

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (13): Year, Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

### Merging

\#\#Merging pols\_df and snp\_df (left join), then merging the result to
the unemployment\_df

``` r
snp_pol_combo = left_join(pols_df,snp_df)
```

    ## Joining, by = c("year", "month")

``` r
five_thirty_eight_joined = left_join(snp_pol_combo, unemployment_df) 
```

    ## Joining, by = c("year", "month")

### Describing the data
