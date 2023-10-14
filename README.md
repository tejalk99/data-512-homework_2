# Wikipedia State and City Article Quality Analysis

## Goal
The goal of this project is to investigate bias in U.S. city and state Wikipedia articles. I combine a dataset of U.S. city Wikipedia articles with a dataset of state populations, and use a machine learning service called ORES to predict each article's quality. I analyze how the coverage of U.S. cities and quality of articles on Wikipedia vary among states.

## Data
Please see below for a list of datasets used in this project:

- U.S. Cities by State (*us_cities_by_state_SEPT.2023.csv*): This dataset was accessed at this [link](https://drive.google.com/file/d/1khouDmMaZyKo0y5WkFj4lu7g8o35x_98/view?usp=drive_link). It contains a column for *state*, *page_title*, and *url* for each Wikipedia article. This dataset was originally created by crawling this Wikipedia [page](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state).
- U.S. State Population Data (*NST-EST2022-ALLDATA.csv*): This dataset is provided by the U.S. Census Bureau and contains population estimates for each state and region in the United States as of 2022. The dataset was accessed at this [link](https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html).
- U.S. States by Region (*US States by Region - US Census Bureau.xlsx*): This dataset originates from the U.S. Census Bureau and lists the state by each regional division in the United States. I accessed this spreadsheet as this [link](https://docs.google.com/spreadsheets/d/14Sjfd_u_7N9SSyQ7bmxfebF_2XpR8QamvmNntKDIQB0/edit#gid=0).

## API
Please see below for the APIs used in this project:

- MediaWiki REST API: This API accesss summary page info for the EN Wikipedia. A summary of this API is available [here](https://www.mediawiki.org/wiki/API:Main_page) and documentation can be accessed at this [link](https://www.mediawiki.org/wiki/API:Info).
- ORES API: This API utilizes the [ORES machine learning system](https://www.mediawiki.org/wiki/ORES), and makes labeled predictions about the quality of Wikipedia articles, using these [content assessment procedures](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment). For my analysis, I use the Liftwing version of ORES, and documentation is available at this [link](https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing/Usage). General ORES documentation can also be accessed [here](https://ores.wikimedia.org/docs).

