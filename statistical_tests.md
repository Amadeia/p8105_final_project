statistical testing
================
Courtney Chan
December 3, 2018

Trying linear regression with dataset merged\_nyt\_searches
===========================================================

First creating the dataset
--------------------------

scraping election results from the web
--------------------------------------

### New York Times voting results by county

This seems to have created two tables from the website data.

Tidying overall table for exploratory analysis
----------------------------------------------

Bar Plot of Votes per Candidate
-------------------------------

![](statistical_tests_files/figure-markdown_github/bar_plot-1.png)

This plot illustrates how it was a close race between the top two candidates, O'Rourke and Cruz. As Dikeman had very few votes, we decided to omit Dikeman from further analyses.

Made the first table that which we have final results for the state of texas.

Tidying county table
--------------------

Made the second table which has all of the 254 county level data for Texas!

Plots for all counties
----------------------

![](statistical_tests_files/figure-markdown_github/point%20county-1.png)

comparing these county level election results to highly searched voter election interests in google
---------------------------------------------------------------------------------------------------

-using search terms "Midterms" and selecting dataset from top result

uploading county congressional district txt file
------------------------------------------------

plot for topics search per county
=================================

Still figuring out how to display this ideas: 1) interactive barchart in the current long format, if we use shiny we could show how the top topics vary among counties through use of drop-down menu to select county, etc. 2) figure out we can juxtapose how the counties voted vs. topics. Use of plotly for interactivity? 3) Alternative to first option, how can we show the distribution of topics among counties instead? 4)focus on 5 biggest counties or districts? but this would be biased as it may be a metropolitan area
