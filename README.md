# Wikipedia State and City Article Quality Analysis

## Goal
The goal of this project is to investigate bias in U.S. city Wikipedia articles and observe the variation among states. I combine a dataset of U.S. city Wikipedia articles with a dataset of state populations, and use a machine learning service called ORES to predict each article's quality. I analyze how the coverage of U.S. cities and quality of articles on Wikipedia vary among states.

## Data
Please see below for a list of datasets used and produced in this project. 

### Data Inputs
- U.S. Cities by State (*us_cities_by_state_SEPT.2023.csv*): This dataset was accessed at this [link](https://drive.google.com/file/d/1khouDmMaZyKo0y5WkFj4lu7g8o35x_98/view?usp=drive_link). It contains a column for *state*, *page_title*, and *url* for each Wikipedia article. This dataset was originally created by crawling this Wikipedia [page](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state).
- U.S. State Population Data (*NST-EST2022-ALLDATA.csv*): This dataset is provided by the U.S. Census Bureau and contains population estimates for each state and region in the United States as of 2022. The dataset was accessed at this [link](https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html).
- U.S. States by Region (*US States by Region - US Census Bureau.xlsx*): This dataset originates from the U.S. Census Bureau and lists states by each regional division in the United States. I accessed this spreadsheet as this [link](https://docs.google.com/spreadsheets/d/14Sjfd_u_7N9SSyQ7bmxfebF_2XpR8QamvmNntKDIQB0/edit#gid=0).

### Data Outputs
- Scored City Articles by State (*wp_scored_city_articles_by_state.csv*): This dataset was produced in my analysis and is a comprehensive data frame that includes additional information for each article, such as the corresponding state, population, and estimated quality. Each field is outlined below.
  - *state* (object): The state corresponding to the city of the Wikipedia article.
  - *regional_division* (object): The regional division that the state belongs to.
  - *population* (int64): The population of the state.
  - *article_title* (object): The title of the Wikipedia article.
  - *revision_id* (object): The revision ID of the article page.
  - *article_quality* (object): The quality of the article, as estimated by the ORES machine learning system.

### Special Considerations
Please note that this analysis only contains 48 out of the 50 U.S. states (excludes Connecticut and Nebraska) due to limitations in the original *U.S. Cities by State* dataset. Additionally, this dataset contains over 600 duplicates and subsequently requires additional data cleaning. These steps are outlined in the analysis notebook in this repository.

## API
Please see below for the APIs used in this project:

- MediaWiki REST API: This API accesss summary page info for the EN Wikipedia. A summary of this API is available [here](https://www.mediawiki.org/wiki/API:Main_page) and documentation can be accessed at this [link](https://www.mediawiki.org/wiki/API:Info).
- ORES API: This API utilizes the [ORES machine learning system](https://www.mediawiki.org/wiki/ORES), and makes labeled predictions about the quality of Wikipedia articles, using these [content assessment procedures](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment). For my analysis, I use the Liftwing version of ORES, and documentation is available at this [link](https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing/Usage). General ORES documentation can also be accessed [here](https://ores.wikimedia.org/docs).

## Code
Code used in this analysis is detailed in the *Wikipedia State and City Article Quality Analysis.ipynb* file in this repository. 

Some code has been modified from code examples provided by Dr. David McDonald under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/):

- Article Page Info MediaWiki API Example (Revision 1.1 - August 14, 2023): This example describes how to request article page info using the MediaWiki API. It can be accessed at this [link](https://drive.google.com/file/d/15UoE16s-IccCTOXREjU3xDIz07tlpyrl/view?usp=drive_link).
- Requesting ORES scores through LiftWing ML Service API (Revision 1.0 - August 15, 2023): This example describes how to use the ORES API to obtain an article quality estimate for each article. It can be accessed at this [link](https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=drive_link).

## Research Implications
***Reflection***

Through the process of this project, I learned about the MediaWiki REST API and ORES API and gained hands-on experience using them. As shown in the *Results* section of my analysis file, I found the states with the highest and lowest articles per capita, the states with the highest and lowest high-quality articles per capita, a ranked list of census divisions by total articles per capita, and a ranked list of census divisions by high-quality articles per capita. Personally, I was surprised to find California on the list of states with the lowest high-quality articles per capita. I realized this was due to my own inherent bias as I grew up in California and expected my home state to produce more high-quality articles relative to other states.

***What (potential) sources of bias did you discover in the course of your data processing and analysis?***

In the course of my data processing and analysis, I found a few sources of bias. The *U.S. Cities by State* dataset only contains data for 48 out of the 50 states. The dataset excludes [Connecticut](https://en.wikipedia.org/wiki/List_of_municipalities_in_Connecticut) and [Nebraska](https://en.wikipedia.org/wiki/List_of_municipalities_in_Nebraska), even though the corresponding Wikipedia pages for these states exist. Furthermore, as a complete set of states is not used in this analysis, aggregations by regional census divisions will not be accurate. In addition, this dataset does not include all current Wikipedia articles for each city. For example, it only includes a list of the top 50 cities in [North Carolina](https://en.wikipedia.org/wiki/List_of_municipalities_in_North_Carolina), whereas there are more according to the page dedicated to the state. Another bias lies in the fact that this analysis uses articles per capita as a metric for coverage. Even though California has a complete set of city Wikipedia articles (as it contains 482 cities and 482 corresponding articles), it will likely consistently be in the list of bottom states by coverage because it is the most populous state in the nation.

***How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?***

In order to correct for the limitations and biases I observed, a researcher could double-check the Wikipedia sites for each city and state to ensure no articles are missed. They could also create a new coverage metric looking at the ratio of Wikipedia articles per city in each state (for example, a state that had 100 cities and 100 corresponding articles would have a coverage of 1). This new metric could subsequently be used to measure high-quality articles per state as well.

***Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?***

A team of data scientists may attempt to use ratios of high-quality articles per capita as a proxy to measure literacy and educational attainment in states, hypothesizing that these measures are correlated. In this case, using this data would create biased and misleading results, due to the missing data outlined above. In addition, Wikipedia’s standards for [featured articles](https://en.wikipedia.org/wiki/Wikipedia:Featured_article_criteria/another_level_of_detail#:~:text=A%20featured%20article%20exemplifies%20our,factually%20accurate%2C%20neutral%20and%20stable.) and [good articles](https://en.wikipedia.org/wiki/Wikipedia:Good_article_criteria) are quite abstract and can not accurately measure the education and writing level of the general population. For example, the site states that a featured article must be "well-written": *Whoever reading it must immediately be reminded of their favorite writer. For example, if the person reading it enjoys science fiction, it should be written in the style of Isaac Asimov, Bradbury, or Larry Niven. If the person reading it is a fan of Shakespeare, then it should read like Shakespeare. Yes it may be difficult to be all things to all people, but that is what writing an FA is all about. EVERYBODY should be reminded of their favorite writer regardless.*

