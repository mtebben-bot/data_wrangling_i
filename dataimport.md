Data Import
================

``` r
library(tidyverse)
```

    ## ── Attaching packages ──────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ─────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
library(haven)
```

## Read in some data

Read in the litters dataset.

``` {r_read)csv}
litters_df = read_csv("./data_import_examples/FAS_litters.csv")
litters_df = janitor::clean_names(litters_df)
```

## Take a look at the data

Printing in the console

``` r_print_df
litters_df
```

``` r_head_df
head(litters_df)
```

``` r_tail_df
tail(litters_df)
```

``` r_skimr_skim_df
skimr::skim(litters_df)
```

## Options to read csv files

Check out `?read_csv` for more information\!

``` r_read_csv_options
litters_df = read_csv("./data_import_examples/FAS_litters.csv", skip = 10, col_names = FALSE, na = c("", "NA", 999))
```

Skipping rows can be useful if descriptions got included or the first
few rows are blank. Column names option can be useful when you do not
have column names in the file. NA option can be useful in defining what
is categorized as NA in R from the original dataset.

## Other file format - Excel

Read in an excel file.

``` r
mlb_df = read_excel("./data_import_examples/mlb11.xlsx")
mlb_df
```

    ## # A tibble: 30 x 12
    ##    team   runs at_bats  hits homeruns bat_avg strikeouts stolen_bases  wins
    ##    <chr> <dbl>   <dbl> <dbl>    <dbl>   <dbl>      <dbl>        <dbl> <dbl>
    ##  1 Texa…   855    5659  1599      210   0.283        930          143    96
    ##  2 Bost…   875    5710  1600      203   0.28        1108          102    90
    ##  3 Detr…   787    5563  1540      169   0.277       1143           49    95
    ##  4 Kans…   730    5672  1560      129   0.275       1006          153    71
    ##  5 St. …   762    5532  1513      162   0.273        978           57    90
    ##  6 New …   718    5600  1477      108   0.264       1085          130    77
    ##  7 New …   867    5518  1452      222   0.263       1138          147    97
    ##  8 Milw…   721    5447  1422      185   0.261       1083           94    96
    ##  9 Colo…   735    5544  1429      163   0.258       1201          118    73
    ## 10 Hous…   615    5598  1442       95   0.258       1164          118    56
    ## # … with 20 more rows, and 3 more variables: new_onbase <dbl>, new_slug <dbl>,
    ## #   new_obs <dbl>

Can always use the function View(mlb\_df) in the CONSOLE to view the
entire data frame.

## Other file format - SAS

``` r
pulse_df = read_sas("./data_import_examples/public_pulse_data.sas7bdat")
pulse_df
```

    ## # A tibble: 1,087 x 7
    ##       ID   age Sex    BDIScore_BL BDIScore_01m BDIScore_06m BDIScore_12m
    ##    <dbl> <dbl> <chr>        <dbl>        <dbl>        <dbl>        <dbl>
    ##  1 10003  48.0 male             7            1            2            0
    ##  2 10015  72.5 male             6           NA           NA           NA
    ##  3 10022  58.5 male            14            3            8           NA
    ##  4 10026  72.7 male            20            6           18           16
    ##  5 10035  60.4 male             4            0            1            2
    ##  6 10050  84.7 male             2           10           12            8
    ##  7 10078  31.3 male             4            0           NA           NA
    ##  8 10088  56.9 male             5           NA            0            2
    ##  9 10091  76.0 male             0            3            4            0
    ## 10 10092  74.2 female          10            2           11            6
    ## # … with 1,077 more rows
