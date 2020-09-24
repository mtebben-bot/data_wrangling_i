Tidy Data
================

``` r_setup
library(tidyverse)
```

## `pivot_longer`

``` r_import_pulse_data
pulse_data = 
  haven:: read_sas("./data_import_examples/public_pulse_data.sas7bdat") %>% 
  janitor:: clean_names()
```

Wide format to long format

``` r_pulse_data_tidy
pulse_data_tidy = 
  pulse_data %>% 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit",
    names_prefix = "bdi_score_",
    values_to = "bdi"
  )
```

Names to sends column names under new label as given. Names prefix
indicates what of the column names is a prefix that can be removed.
Values to creates a new column for the values under new label as given.

#### Rewrite and combine, add mutate step.

``` r_clean_and_import
pulse_data = 
  haven:: read_sas("./data_import_examples/public_pulse_data.sas7bdat") %>% 
  janitor:: clean_names() %>% 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit",
    names_prefix = "bdi_score_",
    values_to = "bdi"
  ) %>% 
  relocate(id, visit) %>% 
  mutate(visit = recode(visit, "bl" = "00m"))
```

## `pivot_wider`

Make up some data\!

``` r_pivot_wider
analysis_result = 
  tibble(
    group = c("treatment", "treatment", "placebo", "placebo"),
    time = c("pre", "pre", "post", "post"),
    mean = c(4, 8, 3.5, 4)
  )

analysis_result %>% 
  pivot_wider(
    names_from = "time",
    values_from = "mean"
  )
```
