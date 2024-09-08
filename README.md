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
