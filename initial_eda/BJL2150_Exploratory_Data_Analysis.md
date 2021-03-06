BJL2150\_Exploratory\_Data\_Analysis
================
Briana Lettsome
November 19, 2018

``` r
# Reading in of the DOHMH_HIV_AIDS_Annual_Report csv file.

hiv_data = read_csv(file = "./data/DOHMH_HIV_AIDS_Annual_Report.csv") %>%
  janitor::clean_names()
```

    ## Parsed with column specification:
    ## cols(
    ##   Year = col_integer(),
    ##   Borough = col_character(),
    ##   UHF = col_character(),
    ##   Gender = col_character(),
    ##   Age = col_character(),
    ##   Race = col_character(),
    ##   `HIV diagnoses` = col_integer(),
    ##   `HIV diagnosis rate` = col_double(),
    ##   `Concurrent diagnoses` = col_integer(),
    ##   `% linked to care within 3 months` = col_integer(),
    ##   `AIDS diagnoses` = col_integer(),
    ##   `AIDS diagnosis rate` = col_double(),
    ##   `PLWDHI prevalence` = col_double(),
    ##   `% viral suppression` = col_integer(),
    ##   Deaths = col_integer(),
    ##   `Death rate` = col_double(),
    ##   `HIV-related death rate` = col_double(),
    ##   `Non-HIV-related death rate` = col_double()
    ## )

``` r
hiv = hiv_data %>%
  filter(borough == "All") %>%
  select(year, race, hiv_diagnosis_rate, gender) %>%
  filter(!race == "All")

 # Spaghetti Plot showing the HIV Diagnosis Rates per race, faceted by gender.

hiv %>%
  ggplot(aes(x = year, y = hiv_diagnosis_rate, color = race, group = race)) +
  geom_line() +
  facet_grid(~gender)
```

![](BJL2150_Exploratory_Data_Analysis_files/figure-markdown_github/unnamed-chunk-2-1.png)

Other/Unknown category includes people of Native American, multiracial, and unknown races.

PLWDHI prevalence
=================

``` r
  race_prevalence = hiv_data %>%
    select(age,plwdhi_prevalence, year, uhf, gender, borough, race) %>%
    filter(uhf =="All") %>%
  filter(!race == "All") %>%
  filter(borough == "All") %>%
  select(-age, -uhf, -borough)

 two_race_prevalence = hiv_data %>%
    select(age,plwdhi_prevalence, year, uhf, gender, borough, race) %>%
    filter(uhf =="All") %>%
  filter(!race == "All") %>%
  filter(borough == "All") %>%
  select(-age, -uhf, -borough)

  
  ggplot(race_prevalence, aes(x = year, fill = race)) + 
  geom_histogram(position = "dodge", binwidth = 2) +
    facet_grid(~ gender)
```

![](BJL2150_Exploratory_Data_Analysis_files/figure-markdown_github/unnamed-chunk-3-1.png)

``` r
race_prevalence %>%
  ggplot(aes(x = year, y = plwdhi_prevalence, color = race)) + 
  geom_line() +
  facet_grid(~gender)
```

![](BJL2150_Exploratory_Data_Analysis_files/figure-markdown_github/unnamed-chunk-3-2.png)

Prevalence by borough
---------------------

Making of spaghetti plot showing persons diagnosed HIV infection by borough over the years.

``` r
 borough_prevalence = hiv_data %>%
    select(age,plwdhi_prevalence, year, borough, uhf, gender, race) %>%
    filter(uhf =="All") %>%
   filter(race == "All") %>%
   filter(gender == "All") %>%
   filter(!borough == "All") %>%
  group_by(year, borough)

borough_prevalence %>%
  ggplot(aes(x = year, y = plwdhi_prevalence, color = borough)) + 
  geom_line() 
```

![](BJL2150_Exploratory_Data_Analysis_files/figure-markdown_github/unnamed-chunk-4-1.png)

EDAs to keep:

Bryce - Bar graph - Death rate type over the years Death rate line graph - Will talk about in paper but not include Percent viral suppression by race and faceted by gender

Briana- HIV diagnosis rates by race and faceted by gender (can link this with Bryce’s percent viral suppression by race and gender)

Noah - HIV diagnosis by borough

David - HIV diagnosis rates by age and faceted by gender
