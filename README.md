# Study Run by Power Outages: When Do They Happen the Most?

**Name(s)**: Iain Roman Bustillos

**Website Link**: [https://ikrvbustil.github.io/poweroutages-sum24/
](https://ikrvbustil.github.io/poweroutages-sum24/)

## Introduction

**Purpose**: The purpose of this analysis will be to get to know which time of the year, month, is most vulnerable to power outages. This will be useful to know so that we can take some measures in order to prevent these outages from happening, or to be aware and prepared that power outages rates are higher at a certain time.

We will be looking at a `.csv' file made by Purdue University, available [here](https://engineering.purdue.edu/LASCI/research-data/outages/outagerisks). The original dataset has **1540 rows** and **57 columns**. The most important columns will be:
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
        <th>Column</th>
      <th>Description(Data Type)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <th>OUTAGE.START</th>
        <td>The date and time of the start of the outage (DateTime object)</td>
    </tr>
    <tr>
      <th>CUSTOMERS.AFFECTED</th>
      <td>Amount of customers without power during the outage (int)</td>
    </tr>
    <tr>
      <th>MONTH</th>
      <td>The month in which the power outage occured (DateTime Object)</td>
    </tr>
    <tr>
      <th>YEAR</th>
      <td>The year in which the outage happened (DateTime Object)</td>
    </tr>
    <tr>
      <th>U.S._STATE</th>
      <td>The state in which the power outage happened (str)</td>
    </tr>
  </tbody>
</table>

Note: This project was made as a final project for DSC80 at UCSD during SS2.

## Data Cleaning and Exploratory Data Analysis

**Cleaning**: Since the original data was given as an excel file, the very first thing I did was turn it into a `.csv` file. Then, the first step I took in order to actually clean this data was to sort of play around with everything to get a basic understanding of what everything means. When I opened the `.csv` file, I noticed that there was 4 rows that were empty, so my first step was to remove any sort of empty spaces. After this, I began to look at the `np.Nan` values of each column and removed any rows which didn't have a month or a year since that's the months that we are looking for. And, since there's no way of guessing/predicting which month/year the power outage belongs to, I decided to drop those rows. Next, I converted the `YEAR` and `MONTH` columns into int-types. After that, I was able to combine the `OUTAGE.START.DATE` column with the `OUTAGE.START.TIME` column in order to make it to a DateTime object for easier use. Lastly, I filtered by the columns I needed and this is the first five rows of the cleaned data:

|OUTAGE.START |	YEAR	| MONTH	| U.S._STATE	| CUSTOMERS.AFFECTED |
|:------------|:------|:-----:|------------:|-------------------:|
|	2014-05-11  | 18:38:00	2014	| 5	| Minnesota	| NaN |
|	2010-10-26  | 20:00:00	2010	| 10	| Minnesota	| 70000.0 |
|	2012-06-19  | 04:30:00	2012	| 6	| Minnesota	| 68200.0 |
|	2015-07-18  | 02:00:00	2015	| 7	| Minnesota	| 250000.0 |
|	2010-11-13  | 15:00:00	2010	| 11	| Minnesota	| 60000.0 |

**Univariate Analysis**: For this analysis, I chose to see the power outage counts by month in order to get a little visual of how the counts look like per month, which is our question. This gave us a good visual that the the power outages spike during June and the lowest being the month of November. This surprised me since I thought it would be December given all the Christmas lights that are put up during that time.

**PLOT1**

**Bivariate Analysis**: For this analysis, I modified the cleaned data in order to get the total number of customers affted per year. To do this I grouped by `YEAR` and summed up the `CUSTOMERS.AFFECTED` column then reset the index. This helped me see that power outages affected the most amount of customers in the year 2008, with many increases in power outages between the year 2001 to 2003 and 2009-2011. This helps us see and maybe even wonder what could have happened during those years. Infinite amount of possibilites.

**PLOT2**

**Interesing Aggregates**: Something interesing we can see about this data by grouping/pivoting it is that Florida had a really big spike in power outages in 2004. They had the most power outages by any state in any given year (in the data). Also, it had the most amount of customers affected with a whopping 7 million customers (this could be repeated people, but it is still outstanding that it happened so many times), a staggering million ahead of second place Texas in 2008 and more than 4 million to third place California in 2008.

## Assessment of Missingness

**NMAR analysis**: Based on the data, we can infer that there is a sense of NMAR happening. Not missing at random (NMAR) is when the missingness of a value is given by the column itself. One might say that the `HURRICANE.NAME` column is NMAR. However, this is closer to MD (missing by design) since if the hurricane doesn't have a name, then that means that there was no hurricane. A better column to show NMAR would by the `CUSTOMERS.AFFECTED` column since this would make sense since it's very hard to keep an accurate record of how many people were affected by the outage. Or maybe the amount was so low that it didn't make sense to include it. Or, it could be that the number was too large to estimate. 

**Missingness Dependency**: We can see this data 

## Hypothesis Testing
Now, to further analyze the data, we can perform a permutation test on it to get a better feel for it. We can ask a question first. 

**Null Hypothesis**: The distribution of power outages is the same before and after 12 PM.

**Alternative Hypothesis**: The distribution of power outages after 12 is higher than the distribution of power outages before.

I chose these hypotheses because I would think that because we use more electricity throughout the day, since we sleep throughout the night, that the power could go out more oftenly during the day. For this test, the best columns to choose is the `OUTAGE.START` column which we created earlier. For this, we can have a permutation test by shuffling the times and finding the differences in mean. 

**PLOT3**

**Result** Since the p-value is bigger than 0.05, we fail to reject the null hypothesis, meaning that the distribution of power outages are equal throughout the day.

## Framing a Prediction Problem

Now, we will try to answer a question which we will try to predict. That question will be to be able to predict the total amount of consumption of a state given the different factors. It will be a pipeline with `StandardScaler()` to standardize the features and `LinearRegression()` for prediction. The factors will be `YEAR` and `TOTAL.CUSTOMERS`. And for performance I will use `Mean Absolute Error (MAE)` to indicate the average magnitude of errors. And also, I'll be using `R-squared` in order to show the proportion of variance. 

## Baseline Model

The model is like the one described, with a pipline with a `StandarSscaler()` which standardizes the two features, `YEAR` and `TOTAL.CUSTOMERS`. And the model I used was a `LinearRegression()`I believe that it is a good model because it has a really good `R-squared` at an average of 0.75.


