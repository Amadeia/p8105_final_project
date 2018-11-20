Testing code
================
Courtney Chan
November 14, 2018

Testing code for the final project
==================================

To accomplish:
--------------

-Looking through the datasets we have available -What kind of analysis do we want to see -Review the sample final projects

Some links to keep in mind: <https://www.cnn.com/election/2018/exit-polls/texas/senate> <https://www.texastribune.org/2018/10/31/ut-tt-poll-texans-say-immigration-border-security-top-issues/>

``` r
library(tidyverse)
library(rvest)
library(httr)
```

scraping election results from the web
--------------------------------------

### New York Times voting results by county

``` r
url = "https://www.nytimes.com/elections/results/texas-senate"
nytimes_data = read_html(url)

nytimes_data
```

    ## {xml_document}
    ## <html lang="en" itemscope="" xmlns:og="http://opengraphprotocol.org/schema/" itemtype="http://schema.org/NewsArticle">
    ## [1] <head>\n<title>Texas Senate Election Results: Beto O’Rourke vs. Ted  ...
    ## [2] <body class="eln-race-page eln-2018-11-06 eln-forecast">\n<script ty ...

``` r
nytimes_data %>% 
  html_nodes(css = "table")
```

    ## {xml_nodeset (2)}
    ## [1] <table class="eln-table eln-results-table">\n<thead><tr>\n<th class= ...
    ## [2] <table class="eln-table eln-county-table">\n<thead><tr>\n<th class=" ...

This seems to have created two tables from the website data.

``` r
table_overall = (nytimes_data %>% html_nodes(css = "table")) %>% 
  .[[1]] %>%
  html_table()
```

Made the first table that which we have final results for the state of texas.

``` r
table_county =  (nytimes_data %>% html_nodes(css = "table")) %>% 
  .[[2]] %>%
  html_table() %>% 
  slice(1:(n() - 1))
```

Made the second table which has all of the 254 county level data for Texas!

comparing these county level election results to highly searched voter election interests in google
---------------------------------------------------------------------------------------------------

``` r
district_searches = read_csv(file =  "./data/Search_Data_US_Congressional_District_04Nov2018.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_double(),
    ##   District = col_character(),
    ##   Code = col_character(),
    ##   State = col_character(),
    ##   FIRST = col_character(),
    ##   SECOND = col_character(),
    ##   THIRD = col_character(),
    ##   FOURTH = col_character(),
    ##   FIFTH = col_character(),
    ##   SIXTH = col_character(),
    ##   SEVENTH = col_character(),
    ##   EIGHTH = col_character(),
    ##   NINTH = col_character(),
    ##   TENTH = col_character(),
    ##   `Gender workplace diversity` = col_integer(),
    ##   `Maternity leave in the United States` = col_integer(),
    ##   `Single-payer healthcare` = col_integer(),
    ##   `Tax Cuts and Jobs Act of 2017` = col_integer(),
    ##   `Transgender people in the military` = col_integer()
    ## )

    ## See spec(...) for full column specifications.

``` r
TX_searches = 
  district_searches %>% janitor::clean_names() %>% 
  filter(state == "TX")
```

uploading county congressional district txt file
------------------------------------------------

``` r
congress_district = read.csv(file = "./data/congress_district2.csv")
```

comparing these county level election results to search results by candidate
----------------------------------------------------------------------------
