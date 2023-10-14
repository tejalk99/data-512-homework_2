# Wikipedia State and City Article Quality Analysis

## Goal
The goal of this project is to investigate bias in U.S. city Wikipedia articles and observe the variation among states. I combine a dataset of U.S. city Wikipedia articles with a dataset of state populations, and use a machine learning service called ORES to predict each article's quality. I analyze how the coverage of U.S. cities and quality of articles on Wikipedia vary among states.

## Data
Please see below for a list of datasets used and produced in this project. 

### Data Inputs
- U.S. Cities by State (*us_cities_by_state_SEPT.2023.csv*): This dataset was accessed at this [link](https://drive.google.com/file/d/1khouDmMaZyKo0y5WkFj4lu7g8o35x_98/view?usp=drive_link). It contains a column for *state*, *page_title*, and *url* for each Wikipedia article. This dataset was originally created by crawling this Wikipedia [page](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state).
- U.S. State Population Data (*NST-EST2022-ALLDATA.csv*): This dataset is provided by the U.S. Census Bureau and contains population estimates for each state and region in the United States as of 2022. The dataset was accessed at this [link](https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html).
- U.S. States by Region (*US States by Region - US Census Bureau.xlsx*): This dataset originates from the U.S. Census Bureau and lists the state by each regional division in the United States. I accessed this spreadsheet as this [link](https://docs.google.com/spreadsheets/d/14Sjfd_u_7N9SSyQ7bmxfebF_2XpR8QamvmNntKDIQB0/edit#gid=0).

### Data Outputs
- Scored City Articles by State (*wp_scored_city_articles_by_state.csv*): This dataset was produced in my analysis and is a comprehensive data frame that includes additional information for each article, such as the corresponding state, population, and estimated quality. Each field is outlined below.
  - *state* (object): The state corresponding to the city of the Wikipedia article.
  - *regional_division* (object): The regional division that the state belongs to.
  - *population* (int64): The population of the state.
  - *article_title* (object): The title of the Wikipedia article.
  - *revision_id* (object): The revision ID of the article page.
  - *article_quality* (object): The quality of the article, as estimated by the ORES machine learning system.

## API
Please see below for the APIs used and produced in this project:

- MediaWiki REST API: This API accesss summary page info for the EN Wikipedia. A summary of this API is available [here](https://www.mediawiki.org/wiki/API:Main_page) and documentation can be accessed at this [link](https://www.mediawiki.org/wiki/API:Info).
- ORES API: This API utilizes the [ORES machine learning system](https://www.mediawiki.org/wiki/ORES), and makes labeled predictions about the quality of Wikipedia articles, using these [content assessment procedures](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment). For my analysis, I use the Liftwing version of ORES, and documentation is available at this [link](https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing/Usage). General ORES documentation can also be accessed [here](https://ores.wikimedia.org/docs).

## Code
Code used in this analysis is detailed in the *Wikipedia State and City Article Quality Analysis.ipynb* file in this repository. 

Some code has been modified from code examples provided by Dr. David McDonald under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/):

- Article Page Info MediaWiki API Example (Revision 1.1 - August 14, 2023): This example describes how to request article page info using the MediaWiki API. It can be accessed at this [link](https://drive.google.com/file/d/15UoE16s-IccCTOXREjU3xDIz07tlpyrl/view?usp=drive_link)
- Requesting ORES scores through LiftWing ML Service API (Revision 1.0 - August 15, 2023): This example describes how to use the ORES API to obtain an article quality estimate for each article. It can be accessed at this [link](https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=drive_link).

## Research Implications
When observing the results...
