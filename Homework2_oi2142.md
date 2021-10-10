Onyeka Isamah, oi2142, Homework 2
================

### Problem 1, Mr Trash Wheel Dataset:

##### Reading and cleaning Mr. Trash Wheel data set using read\_excel and janitor::clean\_names()

##### Omitting rows that do not include dumpster specific data

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

##### Rounding the number of sports balls to nearest integer

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

##### Reading & Cleaning Precipitation 2018

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

##### Reading & Cleaning Precipitation 2019

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

##### Combining precipitation datasets

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
`sports_balls`. The median number of `sports_balls` in `year` 2019 is 8

The Precipitation data set has 18 observations for the amount of
rainfall that occurred and 4 variables - which were `month`, `year`, and
the `total` amount of rainfall. The total amount of precipitation in
2018 is 70.33.

### Problem 2 - FiveThirtyEight Dataset

##### Clean the data in pols-month.csv.

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
    pols_df
```

    ## # A tibble: 822 × 9
    ##    year  month     gov_gop sen_gop rep_gop gov_dem sen_dem rep_dem president
    ##    <chr> <chr>       <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl> <chr>    
    ##  1 1947  January        23      51     253      23      45     198 dem      
    ##  2 1947  February       23      51     253      23      45     198 dem      
    ##  3 1947  March          23      51     253      23      45     198 dem      
    ##  4 1947  April          23      51     253      23      45     198 dem      
    ##  5 1947  May            23      51     253      23      45     198 dem      
    ##  6 1947  June           23      51     253      23      45     198 dem      
    ##  7 1947  July           23      51     253      23      45     198 dem      
    ##  8 1947  August         23      51     253      23      45     198 dem      
    ##  9 1947  September      23      51     253      23      45     198 dem      
    ## 10 1947  October        23      51     253      23      45     198 dem      
    ## # … with 812 more rows

##### Cleaning the snp\_csv file

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
snp_df
```

    ## # A tibble: 787 × 4
    ##    month       day year  close
    ##    <chr>     <int> <chr> <dbl>
    ##  1 january       3 1950   17.0
    ##  2 february      1 1950   17.2
    ##  3 march         1 1950   17.3
    ##  4 april         3 1950   18.0
    ##  5 may           1 1950   18.8
    ##  6 june          1 1950   17.7
    ##  7 july          3 1950   17.8
    ##  8 august        1 1950   18.4
    ##  9 september     1 1950   19.5
    ## 10 october       2 1950   19.5
    ## # … with 777 more rows

##### Tidying unemployment data, before merging

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

``` r
unemployment_df
```

    ## # A tibble: 816 × 3
    ##    year  month     unemployment
    ##    <chr> <chr>            <dbl>
    ##  1 1948  january            3.4
    ##  2 1948  february           3.8
    ##  3 1948  march              4  
    ##  4 1948  april              3.9
    ##  5 1948  may                3.5
    ##  6 1948  june               3.6
    ##  7 1948  july               3.6
    ##  8 1948  august             3.9
    ##  9 1948  september          3.8
    ## 10 1948  oct                3.7
    ## # … with 806 more rows

##### Merging

###### Merging pols\_df and snp\_df (left join), then merging the result to the unemployment\_df

``` r
snp_pol_combo = left_join(pols_df,snp_df)
```

    ## Joining, by = c("year", "month")

``` r
five_thirty_eight_joined = left_join(snp_pol_combo, unemployment_df) 
```

    ## Joining, by = c("year", "month")

``` r
five_thirty_eight_joined
```

    ## # A tibble: 822 × 12
    ##    year  month   gov_gop sen_gop rep_gop gov_dem sen_dem rep_dem president   day
    ##    <chr> <chr>     <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl> <chr>     <int>
    ##  1 1947  January      23      51     253      23      45     198 dem          NA
    ##  2 1947  Februa…      23      51     253      23      45     198 dem          NA
    ##  3 1947  March        23      51     253      23      45     198 dem          NA
    ##  4 1947  April        23      51     253      23      45     198 dem          NA
    ##  5 1947  May          23      51     253      23      45     198 dem          NA
    ##  6 1947  June         23      51     253      23      45     198 dem          NA
    ##  7 1947  July         23      51     253      23      45     198 dem          NA
    ##  8 1947  August       23      51     253      23      45     198 dem          NA
    ##  9 1947  Septem…      23      51     253      23      45     198 dem          NA
    ## 10 1947  October      23      51     253      23      45     198 dem          NA
    ## # … with 812 more rows, and 2 more variables: close <dbl>, unemployment <dbl>

##### Describing the data

The Pols\_df data set has 822 observations and 9 variables related to
politicians who were democratic or republican between the years 1947 and
2015.

The snp\_df data set has 787 observations and 4 variables related to
Standard & Poor’s stock market index (S&P) from 1950 - 2015. The
variables were `month`, `year`, and `close`.

The unemployment\_df data set has 816 observations and 3 variables
related to the percentage of unemployment by `month` (January- February)
from the years 1948-2015.

The resulting data set that joined pols,snp, and unemployment
(five\_thirty\_eight\_joined) has 822 observations and 12 variables.

##### Problem3 NYC Open Data

Cleaning the data set

``` r
babyname_df = distinct(
  read_csv("./data/Popular_baby_names.csv") %>% 
  janitor::clean_names() %>% 
  
  mutate(ethnicity = recode(ethnicity,
   "WHITE NON HISP" = "WHITE NON HISPANIC", 
   "WHITE NON HISPANIC"="WHITE NON HISPANIC",  
   "BLACK NON HISP" =  "BLACK NON HISPANIC",  
   "BLACK NON HISPANIC" = "BLACK NON HISPANIC",
 "ASIAN AND PACI" ="ASIAN AND PACIFIC ISLANDER",  
  "ASIAN AND PACIFIC ISLANDER"= "ASIAN AND PACIFIC ISLANDER"
)) %>% 
  
mutate(
  year_of_birth = as.character(year_of_birth)))
```

    ## Rows: 19418 Columns: 6

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (3): Gender, Ethnicity, Child's First Name
    ## dbl (3): Year of Birth, Count, Rank

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

##### Popularity of the name *Olivia* as a female baby name over the years

``` r
 olivia_rank=(select(babyname_df, childs_first_name, year_of_birth, gender, rank, ethnicity, -count) %>% 
                     
    filter(childs_first_name == "OLIVIA", 
    gender == "FEMALE") %>% 
  
      pivot_wider(
        names_from = "year_of_birth",
        values_from = "rank") %>% 
        group_by(ethnicity))
olivia_rank
```

    ## # A tibble: 4 × 5
    ## # Groups:   ethnicity [4]
    ##   childs_first_name gender ethnicity                  `2012` `2011`
    ##   <chr>             <chr>  <chr>                       <dbl>  <dbl>
    ## 1 OLIVIA            FEMALE ASIAN AND PACIFIC ISLANDER      3      4
    ## 2 OLIVIA            FEMALE BLACK NON HISPANIC              8     10
    ## 3 OLIVIA            FEMALE HISPANIC                       22     18
    ## 4 OLIVIA            FEMALE WHITE NON HISPANIC              4      2

##### Most popular baby names for male children over time

``` r
 male_rank= pivot_wider(
   
  (select(babyname_df, -count) %>% 
  filter(gender == "MALE") %>% 
  pivot_wider(
  names_from = "year_of_birth", 
  values_from = "rank") %>% 
  group_by(ethnicity)))
```

###### Scatter Plot

Creating data frame to be plotted, for white non hispanic males who were
born in 2016

``` r
whitemale_plot = filter(babyname_df, gender == "MALE", ethnicity == "WHITE NON HISPANIC", year_of_birth == 2016)
```

Scatterplot for white non hispanic males who were born in 2016

``` r
ggplot(whitemale_plot, aes(x = rank, y = count)) + 
  geom_point()
```

![](Homework2_oi2142_files/figure-gfm/scatter%20plot-1.png)<!-- -->
