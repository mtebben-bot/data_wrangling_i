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
