Data Manipulation
================

``` r_setup
library(tidyverse)
```

## Load FAS Litters data

``` r_load_litters_data
litters_df = read_csv("./data_import_examples/FAS_litters.csv")
litters_df = janitor::clean_names(litters_df)
litters_df
```

## `select`

Choose some columns, not others.

``` r_select_basic
select(litters_df, group, litter_number)
```

Colons can be used to select all columns between them.

``` r_select_colon
select(litters_df, group, gd0_weight:gd_of_birth)
```

Dashes can be used to omit certain columns.

``` r_select_omit
select(litters_df, -litter_number)
```

Can rename columns

``` r_select_rename
select(litters_df, GROUP = group)
```

or

``` r_rename
rename(litters_df, GROUP = group)
```

#### Select helpers

Select columns that start with…

``` r_select_startswith
select(litters_df, starts_with("gd"))
```

To look at one column first, but keep the rest, use everything()

``` r_select_everything
select(litters_df, litter_number, everything())
```

or…

``` r_relocate
relocate(litters_df, litter_number)
```

## `filter`

``` r_filter
filter(litters_df, gd0_weight >= 22)
filter(litters_df, !(gd_of_birth == 20))
filter(litters_df, group %in% c("Con7", "Mod8"))
```

Logical operators on p8105 website to be used in filter.

## `mutate`

For calculations in dataset

``` r_mutate
mutate(
  litters_df,
  wt_gain = gd18_weight - gd0_weight,
  group = str_to_lower(group))
```

str\_to\_lower gives you lowercase, replaced group with group
