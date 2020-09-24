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

## Binding rows

Using LOTR data

First step: import each table

``` r_load_lotr_data
fellow = 
  readxl::read_excel("./data_import_examples/LotR_Words.xlsx", range = "B3:D6") %>% 
  mutate(movie = "fellowship_of_the_ring")

two_towers = 
  readxl::read_excel("./data_import_examples/LotR_Words.xlsx", range = "F3:H6") %>% 
  mutate(movie = "two_towers")

return = 
  readxl::read_excel("./data_import_examples/LotR_Words.xlsx", range = "J3:L6") %>% 
  mutate(movie = "return_of_the_king")
```

Bind all of the rows together

``` r_bind_rows
lotr_tidy = 
  bind_rows(fellow, two_towers, return) %>% 
  janitor::clean_names() %>% 
  relocate(movie) %>% 
  pivot_longer(
    female:male,
    names_to = "gender",
    values_to = "words"
  )
```

## Joining data sets

#### Importing FAS datasets.

``` r_importing_fas_datasets
pups_df = 
  read_csv("./data_import_examples/FAS_pups.csv") %>% 
  janitor::clean_names() %>% 
  mutate(sex = recode(sex, `1` = "male", `2` = "female"))

litters_df = 
  read_csv("./data_import_examples/FAS_litters.csv") %>% 
  janitor::clean_names() %>% 
  relocate(litter_number) %>% 
  separate(group, into = c("dose", "day_of_tx"), sep = 3)
```

Litter number variable the same across both, will unite both datasets
together.

#### Time to join\!

``` r_joining
fas_df = 
  left_join(pups_df, litters_df, by = "litter_number") %>% 
  arrange(litter_number) %>% 
  relocate(litter_number, dose, day_of_tx)
```
