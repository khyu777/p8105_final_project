EDA\_Markdown\_NK
================
Noah Kreski
November 19, 2018

``` r
HIV_data = read_csv("./data/DOHMH_HIV_AIDS_Annual_report.csv")
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
Linkage_data_male = HIV_data%>%
               janitor::clean_names()%>%
               filter(borough %in% c("All"))%>%
               filter(!(age %in% c("All")))%>%
               filter(gender == "Male")
Linkage_data_male%>%
               ggplot(aes(x = year, y = percent_linked_to_care_within_3_months, group = age, color = age))+geom_point() + geom_line()
```

![](EDA_NK_Markdown_files/figure-markdown_github/eda%20linkage-1.png)

``` r
Linkage_data_female = HIV_data%>%
               janitor::clean_names()%>%
               filter(borough %in% c("All"))%>%
               filter(!(age %in% c("All")))%>%
               filter(gender == "Female")
Linkage_data_female%>%
               ggplot(aes(x = year, y = percent_linked_to_care_within_3_months, group = age, color = age))+geom_point() + geom_line()         
```

![](EDA_NK_Markdown_files/figure-markdown_github/eda%20linkage-2.png)

``` r
HIV_data = read_csv("./data/DOHMH_HIV_AIDS_Annual_report.csv")
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
diagnosis_data = HIV_data%>%
               janitor::clean_names()%>%
               filter(borough %in% c("All"))%>%
               filter((age %in% c("All")))%>%
               filter(!(gender %in% c("Transgender")))%>%
               filter(race %in% c("All"))
diagnosis_data%>%
               ggplot(aes(x = year, y = aids_diagnosis_rate, group = gender, color = gender))+geom_point() + geom_line()
```

![](EDA_NK_Markdown_files/figure-markdown_github/eda%20aids%20diagnosis%20rate-1.png)
