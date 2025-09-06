# insert_title_here
<!-- MENTAL NOTE: MAKE SURE TO ACTUALLY WRITE AN ACTUAL TITLE BEFORE SUBMISSION -->

Project for DSC 80 @ UC San Diego

By Neil Bango and Jaden Goelkel

<!-- Insert a table of contents with hyperlinks -->

## Introduction


Power outages are defined as the loss of electrical power serving a community. These are usually harmful and indicative of an underlying deeper problems. Considering how reliant we are on electricity in the 21st century these power outages  could potentially cost lives, destroy infrastructure, and create widespread problems.

Which is why in this project, we decide to explore when and where these power outages occur and just how severe they can be. To do this, we use a dataset provided by Purdue's LASCI (Laboratory for Advancing Sustainable Critical Infrastructure) which contains information on power outages from 2000 to 2016.

The dataset titled 'Major Power Outage Risks in the U.S.' contains 1534 different observations from outages lasting minutes to major world wide events like when Hurrican Rita caused a loss of power in Louisiana for over 13 days in 2005.

On top of the 1534 rows, there are 56 columns worth of data that explain characteristics from where the storm happened to the population density of the area affected by the power outage. While this is extremely helpful, we won't be needing all of the columns therefore we dropped unneeded information and kept the following columns.

<!-- Insert a table of columns and what they mean -->

## Data Cleaning and Exploratory Data Analysis
### • Data Cleaning
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
### • Univariate analyses

Now that our data is ready we can finally do some analysis!

Let's go back to our first question. When and where do these power outages occur? A question like that should be easy. Since our dataset tells us the state the outage occurs in, we can simply read these from the table. We plot it below as a heatmap of the United States. 

<iframe src="assets/power_outage_loss_by_state.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Well this doesn't look to helpful, in fact it seems pretty similar to a heatmap of the U.S. Population. In fact, let's take a look at a map like that

<iframe src="assets/population_by_state.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

They almost look the exact same!

But it wouldn't feel right to just say more people equals more power outage. It could just mean that higher population areas also require more electricity and infrastructure and therefore this causes more power outages. But it doesn't explicitly mean that more people cause power outages. But remember this dataset includes even the most minute outages that could last a minute or less. Theses kinds of disruptions, while annoying, don't exactly deserve the same amount of attention of more destructive outages.

Thankfully, the U.S. Department of Energy has an item called Form DOE-417, or The Electric Emergency Incident and Disturbance Report. Here's <!-- put hyperlink --> an example of one, and in that form, it gives certain importance to events where more than `50,000` people are affected, `300` Megawatts or more power is loss. Furthermore, outages with over `72` or more hours of power loss correlate to severe power outages. Let's save this filtered dataset under `severe`

With this new more exclusive dataset, let's redo our plots.

<iframe src="assets/severe_power_outage_loss_by_state.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Now this plot looks more informative. Less importance is given to more populous states just because of their size and it outlines states such as Michigan and Texas as being prone to severe power outages. But these "severe locations" can be difficult to discern from a map alone, let's try making a more objective metric,

Looking at reasons why these power outages occur, it's clear that `severe weather` is the biggest reason, but there seems to be a variety of possibilites that could affect power. But once again, most such as `intentional attack` and `system operability disruption` stem from power disruptions that are more likely to occur in heaily populated areas. 

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



### • Performed bivariate analyses and aggregations

## Assessment of Missingness
### • Addressed NMAR question

• Performed permutation tests for missingness

• Interpreted missingness test results

Hypothesis Testing

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