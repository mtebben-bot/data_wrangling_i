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

``` r_excel_import
mlb_df = read_excel("./data_import_examples/mlb11.xlsx")
mlb_df
mlb_df = read_excel("./data_import_examples/mlb11.xlsx", range = "A1:F7")
```

Can always use the function View(mlb\_df) in the CONSOLE to view the
entire data frame. Use range to select cells to import.

## Other file format - SAS

Read in a SAS file.

``` r_sas_import
pulse_df = read_sas("./data_import_examples/public_pulse_data.sas7bdat")
pulse_df
```

## Comparison with base R

what about `read.csv`…?

``` {r_read.csv}
litters_base = read.csv("./data_import_examples/FAS_litters.csv")
litters_readr = read_csv("./data_import_examples/FAS_litters.csv")
litters_base
litters_readr
```

## Exporting data

Export mlb sub-table

``` r_write_csv
write_csv(mlb_df, "./data_import_examples/mlb_subtable.csv")
```
