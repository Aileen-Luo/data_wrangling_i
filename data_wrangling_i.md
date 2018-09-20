data\_wrangling\_i
================
Man Luo
2018-09-18

Impot FAS cs file
-----------------

import my data

``` r
library(tidyverse)
```

    ## -- Attaching packages --------------------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts ------------------------------------------------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
littles_data = read_csv(file ="./data/FAS_litters.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_integer(),
    ##   `Pups born alive` = col_integer(),
    ##   `Pups dead @ birth` = col_integer(),
    ##   `Pups survive` = col_integer()
    ## )

``` r
littles_data = janitor::clean_names(littles_data)
```

Import second data

``` r
pups_data = read_csv(file = "./data/FAs_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_integer(),
    ##   `PD ears` = col_integer(),
    ##   `PD eyes` = col_integer(),
    ##   `PD pivot` = col_integer(),
    ##   `PD walk` = col_integer()
    ## )

``` r
pups_data_absolute = read_csv(file = "C:/Users/Luo/Desktop/2018/P8105 ds/Project/Lec4 data_wrangling_i/data_wrangling_i/data/FAs_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_integer(),
    ##   `PD ears` = col_integer(),
    ##   `PD eyes` = col_integer(),
    ##   `PD pivot` = col_integer(),
    ##   `PD walk` = col_integer()
    ## )

Look at the data
----------------

``` r
head(littles_data)
```

    ## # A tibble: 6 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2         NA          NA            20               6
    ## # ... with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
tail(littles_data)
```

    ## # A tibble: 6 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Low8  #79                 25.4        43.8          19               8
    ## 2 Low8  #100                20          39.2          20               8
    ## 3 Low8  #4/84               21.8        35.2          20               4
    ## 4 Low8  #108                25.6        47.5          20               8
    ## 5 Low8  #99                 23.5        39            20               6
    ## 6 Low8  #110                25.5        42.7          20               7
    ## # ... with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
skimr::skim(littles_data)
```

    ## Skim summary statistics
    ##  n obs: 49 
    ##  n variables: 8 
    ## 
    ## -- Variable type:character -----------------------------------------------------------------------------------------------
    ##       variable missing complete  n min max empty n_unique
    ##          group       0       49 49   4   4     0        6
    ##  litter_number       0       49 49   3  15     0       49
    ## 
    ## -- Variable type:integer -------------------------------------------------------------------------------------------------
    ##         variable missing complete  n  mean   sd p0 p25 p50 p75 p100
    ##      gd_of_birth       0       49 49 19.65 0.48 19  19  20  20   20
    ##  pups_born_alive       0       49 49  7.35 1.76  3   6   8   8   11
    ##  pups_dead_birth       0       49 49  0.33 0.75  0   0   0   0    4
    ##     pups_survive       0       49 49  6.41 2.05  1   5   7   8    9
    ##      hist
    ##  <U+2585><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>
    ##  <U+2582><U+2582><U+2583><U+2583><U+2587><U+2585><U+2581><U+2581>
    ##  <U+2587><U+2582><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581>
    ##  <U+2582><U+2582><U+2583><U+2583><U+2585><U+2587><U+2587><U+2585>
    ## 
    ## -- Variable type:numeric -------------------------------------------------------------------------------------------------
    ##     variable missing complete  n  mean   sd   p0   p25   p50   p75 p100
    ##   gd0_weight      15       34 49 24.38 3.28 17   22.3  24.1  26.67 33.4
    ##  gd18_weight      17       32 49 41.52 4.05 33.4 38.88 42.25 43.8  52.7
    ##      hist
    ##  <U+2581><U+2583><U+2587><U+2587><U+2587><U+2586><U+2581><U+2581>
    ##  <U+2582><U+2583><U+2583><U+2587><U+2586><U+2582><U+2581><U+2581>

skip some rows and ignore variable names

``` r
litters_data = read_csv(file = "./data/FAS_litters.csv", skip = 10, col_names = FALSE)
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   X2 = col_character(),
    ##   X3 = col_double(),
    ##   X4 = col_double(),
    ##   X5 = col_integer(),
    ##   X6 = col_integer(),
    ##   X7 = col_integer(),
    ##   X8 = col_integer()
    ## )

Take a look at pups
-------------------

``` r
pups_data = read_csv(file = "./data/FAS_pups.csv", col_types = "ciiiii")
pups_data = janitor::clean_names(pups_data)
skimr::skim(pups_data)
```

    ## Skim summary statistics
    ##  n obs: 313 
    ##  n variables: 6 
    ## 
    ## -- Variable type:character -----------------------------------------------------------------------------------------------
    ##       variable missing complete   n min max empty n_unique
    ##  litter_number       0      313 313   3  15     0       49
    ## 
    ## -- Variable type:integer -------------------------------------------------------------------------------------------------
    ##  variable missing complete   n  mean   sd p0 p25 p50 p75 p100     hist
    ##   pd_ears      18      295 313  3.68 0.59  2   3   4   4    5 <U+2581><U+2581><U+2585><U+2581><U+2581><U+2587><U+2581><U+2581>
    ##   pd_eyes      13      300 313 12.99 0.62 12  13  13  13   15 <U+2582><U+2581><U+2587><U+2581><U+2581><U+2582><U+2581><U+2581>
    ##  pd_pivot      13      300 313  7.09 1.51  4   6   7   8   12 <U+2583><U+2586><U+2587><U+2583><U+2582><U+2581><U+2581><U+2581>
    ##   pd_walk       0      313 313  9.5  1.34  7   9   9  10   14 <U+2581><U+2585><U+2587><U+2585><U+2583><U+2582><U+2581><U+2581>
    ##       sex       0      313 313  1.5  0.5   1   1   2   2    2 <U+2587><U+2581><U+2581><U+2581><U+2581><U+2581><U+2581><U+2587>

Other format
------------

read in mlb data

``` r
mlb_data = readxl::read_excel(path = "./data/mlb11.xlsx")
mlb_data = readxl::read_excel(path = "./data/mlb11.xlsx",range = "A1:E11")
```
