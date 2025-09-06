# Data Gone Dark: Understanding power outages in the U.S.

Project for DSC 80 @ UC San Diego

By Neil Bango and Jaden Goelkel

## Introduction

Power outages are defined as the loss of electrical power serving a community. These are usually harmful and indicative of underlying deeper problems. Considering how reliant we are on electricity in the 21st century these power outages  could potentially cost lives, destroy infrastructure, and create widespread problems.

Which is why in this project, we decide to explore when and where these power outages occur and just how severe they can be. To do this, we use a dataset provided by Purdue's LASCI (Laboratory for Advancing Sustainable Critical Infrastructure) which contains information on power outages from 2000 to 2016.

The dataset titled ['Major Power Outage Risks in the U.S.'](https://engineering.purdue.edu/LASCI/research-data/outages) contains 1534 different observations from outages lasting minutes to major worldwide events like when Hurricane Rita caused a loss of power in Louisiana for over 13 days in 2005.

On top of the 1534 rows, there are 56 columns worth of data that explain characteristics from where the storm happened to the population density of the area affected by the power outage. While this is extremely helpful, we won't be needing all of the columns therefore we dropped unneeded information and kept the following columns.

<!-- Insert a table of columns and what they mean -->

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
To answer the question we defined, we must first clean the data. We start by dropping the columns we didn't use as mentioned earlier. 

Then to reduce redundancy in the dataset, we combined the columns `'OUTAGE.START.DATE'` and `'OUTAGE.START.TIME'` into one cohesive `'OUTAGE.START'` column as a pandas DateTime object. Then dropped the redundant information. 

<!-- np.nan needed data -->

Finally, to adhere to Python's PEP 8 style guide, we made the column names `snake_case`.

This is what the first few rows and columns of the new cleaned DataFrame look like. 

|   obs |   year |   month | us_state   | 
|------:|-------:|--------:|:-----------|
|     1 |   2011 |       7 | Minnesota  |
|     2 |   2014 |       5 | Minnesota  |
|     3 |   2010 |      10 | Minnesota  |
|     4 |   2012 |       6 | Minnesota  |
|     5 |   2015 |       7 | Minnesota  |

## Exploratory Data Analysis
### Univariate analyses

Now that our data is ready we can finally do some analysis!

Let's go back to our first question. When and where do these power outages occur? A question like that should be easy. Since our dataset tells us the state the outage occurs in, we can simply read these from the table. We plot it below as a heatmap of the United States. 

<iframe src="assets/power_outage_loss_by_state.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Well this doesn't look too helpful, in fact it seems pretty similar to a heatmap of the U.S. Population. In fact, let's take a look at a map like that

<iframe src="assets/population_by_state.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

They almost look the exact same!

But it wouldn't feel right to just say more people equals more power outage. It could just mean that higher population areas also require more electricity and infrastructure and therefore this causes more power outages. But it doesn't explicitly mean that more people cause power outages. But remember this dataset includes even the most minute outages that could last a minute or less. These kinds of disruptions, while annoying, don't exactly deserve the same amount of attention as more destructive outages.

Thankfully, the U.S. Department of Energy has an item called Form DOE-417, or The Electric Emergency Incident and Disturbance Report. [Here's](https://doe417.pnnl.gov/files/DOE-417_Form.pdf) an example of one, and in that form, it gives certain importance to events where more than `50,000` people are affected, `300` Megawatts or more power is lost. Furthermore, outages with over `72` or more hours of power loss correlate to severe power outages. Let's save this filtered dataset under `severe`

###     The severe DataFrame

Before we proceed, this DataFrame contains some interesting aggregates. If we pivot the tables on `'us_state'` and find the mean `'outage_duration'`, and the sum of `'customers_affected'` and `'demand_loss_mw'` you will see the table below. It gives us a sense of scale how much more damaging an outage is once we compare it to other other occurrences in its class.

| us_state       |   customers_affected |   demand_loss_mw |   outage_duration |
|:---------------|---------------------:|-----------------:|------------------:|
| Florida        |          1.27322e+07 |            32183 |           4094.67 |
| Georgia        |          1.93088e+06 |             7916 |           1345.41 |
| Indiana        |          2.36475e+06 |             6332 |           3521.64 |
| Louisiana      |          3.02006e+06 |             3816 |           4084.55 |
| Maryland       |          5.42407e+06 |            11440 |           2313.09 |
| Michigan       |          1.3759e+07  |            35524 |           5302.98 |
| Ohio           |          4.92417e+06 |            23261 |           2867.86 |
| South Carolina |          2.0153e+06  |            11898 |           3135    |
| Texas          |          2.09838e+07 |            33125 |           2704.82 |
| Virginia       |          5.08059e+06 |            15639 |           1051.19 |
| Washington     |          4.48554e+06 |             8782 |           1508.15 |

With this new more exclusive dataset, let's redo our plots.

<iframe src="assets/severe_power_outage_loss_by_state.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Now this plot looks more informative. Less importance is given to more populous states just because of their size and it outlines states such as Michigan and Texas as being prone to severe power outages. But these "severe locations" can be difficult to discern from a map alone, let's try making a more objective metric.

### Bivariate analysis

Plotting the data in `severe`, we can compare outages that are caused by severe weather compared to a state's population. After applying a log filter to make the data more visible, there are clear outlier states which deal with more disruptive power outages vs the rest of the country. This finally allows us to answer, where do major power outages occur and that would be in `Texas`, `Michigan`, `Florida`, `Virginia`, `Maryland`, `Georgia`, `Ohio`, `South Carolina`, `Indiana`, `Washington`, `Louisiana`. These were the states above the trendline when it came to their population vs how much severe outages they should be experiencing.

Looking at reasons why these power outages occur, it's clear that `severe weather` is the biggest reason, but there seems to be a variety of possibilities that could affect power. But once again, most such as `intentional attack` and `system operability disruption` stem from power disruptions that are more likely to occur in heavily populated areas. 

<iframe src="assets/category_causes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This changes once again if we use our custom `severe` DataFrame, and the real reason why major power outages happen become more apparent.

<iframe src="assets/severe_category_causes_detailed.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Clearly mother nature is the biggest determiner of more serious power outages.

But arguably just as important as where is when these power outages occur. 

<iframe src="assets/outages_per_month.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



There seems to be a clear spike in power outages from June to September. This would support our idea that disruptive outages occur mostly because of severe weather effects since June 1 to November 30 is considered as [Hurricane Season](https://www.weather.gov/safety/hurricane#:~:text=On%20average%2C%2014%20tropical%20storms,to%20November%2030%20each%20year) by the National Weather Service



## Assessment of Missingness

### NMAR Analysis
The dataset contained missing values on a variety of columns. Most prevalently on `'hurricane_names'` with 95.31% of values missing. Although this is easily explained since not every outage is related to a hurricane. Although something like `'demand_loss_mw'` is more difficult to explain with 45.96% of values missing. We believe that this is NMAR since it would be difficult to estimate how much demand is lost when the instruments possibly used to measure this well... loses power. Therefore missing values can be attributed to reasons not connected to the other columns.

### Permutation test for missingness

To assess missingness, we chose to identify if `'cause_category_detail'` and its missingness has something to do with `'customers_affected'`. In other words, we wanted to see if the cause of an outage has something to do with the number of customers being missing. 

To do this, let's formalize a hypothesis:

* Null Hypothesis: The distribution of '`cause_category_detail`' is independent of whether customers_affected is missing.

* Alternative Hypothesis: The distribution of '`cause_category_detail`' is different between outages where customers_affected is missing and those where it is not.

<iframe src="assets/proportion_missingness_by_cause_detail.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


We find an observed TVD between `'cause_category_detail'` and `'customer_missing'` as `0.66`. Which after running a permutation test, find that its p-value is `0.0`. This means we reject the null and understand that there is a difference between the distribution of `'cause_category_detail'` when `'customers_affected'` is missing.

<iframe src="assets/permutation_test_tvd.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Let's do this test again but this time we choose to identify if `'climate_category'` and its missingness has something to do with `'customers_affected'`. In other words, we wanted to see if the cause of an outage has something to do with the climate category of the outage. 

To do this, let's formalize a hypothesis:

* Null Hypothesis:The distribution of climate_category is independent of whether '`customers_affected`' is missing.

* Alternative Hypothesis: The distribution of `'climate_category'` depends on whether `'customers_affected'` is missing.

<iframe src="assets/proportion_missingness_by_climate_category.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This time, we find an observed TVD between `'climate_category'` and `'customer_missing'` as `0.03`. Which after running a permutation test, find that its p-value is `0.35`. This means we fail to reject the null and understand that there isn't a significant difference between the distribution of `'climate_category'` when `'customers_affected'` is missing.

<iframe src="assets/permutation_test_tvd_climate.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Hypothesis Testing

While this assessment of missingness has shown how powerful hypothesis testing is, one aspect where we thought we could also apply it is a population problem. Going back to our Exploratory Data Analysis, we saw how initially we thought that higher population areas had more chances of power outages. This was before we filtered out severe outages first. However, we came to that conclusion by looking at a map and guesstimating. Let's try being more objective about it.

* Null Hypothesis: The average number of customers affected by an outage is the same in high-population and low-population areas.

* Alternative Hypothesis: The average number of customers affected by an outage is different between high-population and low-population areas.

In our population sample, we split it into two samples depending on if the outage occurred in a high population area or not. We did this by placing them in different bins depending on if the population is above/below the median.

Our test statistic would be the difference of means between customers affected in high population areas and low population areas. Our significance level would be placed at `p=0.05`

With this in mind, we proceed with a permutation test with 1000 repetitions, and found that our observed test statistic is `99034`. and our p-value is at 0. This means  that with a p-value so small, we reject the null hypothesis since it's below our designated significance level. This does prove our estimate that higher population areas have differing amounts of customers affected compared to low population areas.

<iframe src="assets/permutation_test_diff_of_means.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


• Selected relevant columns for a hypothesis or permutation test

• Explicitly stated a null hypothesis

• Explicitly stated an alternative hypothesis

• Performed a hypothesis or permutation test

• Used a valid test statistic

• Computed a p-value and made a decision

Framing a Prediction Problem

Baseline Model

Final Model

Fairness Analysis