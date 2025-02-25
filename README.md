# 2024 Udacity Data Scientist Project 1

## Libraries used

- pandas
- seaborn
- matplotlib
- sklearn
  - sklearn.linear_model.LinearRegression
  - sklearn.model_selection.train_test_split
  - sklearn.metrics.r2_score
  - sklearn.metrics.mean_squared_error
- itertools
  - itertools.combinations
- tqdm
  - tqdm.tqdm

## Motivation

I was interested in exploring the Airbnb datasets to see if there were any features that could be used to try and determine what the price for a rental could or should be.

## Files

- airbnb_exploration.ipynb
  - This notebook contains my exploration of the Seattle and Boston 2017 Airbnb data sets found on Kaggle. It also contains the modeling work done for price estimation.

## Results Summary

I was first interested in how the Superhost status might affect the price. I began with whether the host would have Superhost status if they had a better response rate to find if maybe Superhosts might have a higher price, but better reviews due to a better response rate. This led me to look at the review scores in addition to their response rate. Since the review scores and response rates were mostly above 70%, I decided to use letter grades to categorize the reviews. While doing this I also decided to look at what the average price is purely by Superhost status and found that Superhosts actually do not charge much more on average. I continued my analysis on the average price per Superhost status and review grade. I found that Boston and Seattle hosts tend to do the opposite. Boston Superhosts tend to charge more when their reviews are lower than an 'A' grade (90% to 100%) and they always charge more than regular hosts. But non-Superhosts do charge less the lower their review grade is. Seattle Superhosts tend to charge less the lower their review grade is. Seattle non-Superhosts tend to charge a bit more when they have an 'A' grade, but will charge more at a 'C' than a 'B' and even higher than at an 'A' level if they are lower than a 'C' grade. I ignored those listings without a review score since that is what I was analyzing.

For the next part of my analysis, I looked at the response and review grades per Superhost status to see if maybe a higher response rate correlates with a higher review score. For the most part this correlates well. Superhosts and non-Superhosts for both cities tend to have an 'A' grade for both response rate and reviews. Notably, Superhosts tend to be more likely to have an 'A' grade in both, with very few having less than an 'A' grade. For non-Superhosts, the trend is about the same, but it is much more evident that hosts can have an excellent response rate, but still have a lower review score. For this analysis, since I was looking at these two values, I ignored those that did not have a review score or a response rate.

For my last part of the analysis, I decided to try and see what other columns could be used to estimate the price. Going by the material in the lessons, I decided to use a linear regression model for estimating and using the R^2 score and mean squared error to score the models. At first, I was iterating through the columns and adding additional columns to see how much the score would improve. It was taking a while and the highest R^2 score I received was 0.62 and involved almost all of the numerical and categorical columns (besides the ones I had excluded due to high numbers of null values). I decided to try different combinations of columns to see if I could get a close or even higher score by using less columns meaning the model would take less time to run. I get a list of all possible combinations and ended up reaching a combination of 5 columns as the maximum without having to wait too long on my computer. This actually yielded great results because I was able to get the column combination of ('neighbourhood_cleansed', 'room_type', 'accommodates', 'bedrooms', 'review_scores_communication') to get a score of 0.63, higher than my score when I was using 15 columns. It also ran in about 5 minutes, instead of the 3 hours that it took the model to run for 15 columns. Most of these columns are expected to increase the price, but notably, the review score for the host's communication is among these columns. As when I was looking at the response rates by Superhost status, it seems to be important for pricing, but again, lower review scores tend to have higher prices. Below a score of 6.0, there are fewer listings though, so the results are definitely more skewed than the average prices for higher communication scores.

The explanation of my analysis with graphs is located in this [blog post](https://meeby280.github.io/UdacityDataScienceProject1/2025/02/09/Project-1.html).

## Acknowledgements

- Multiple examples within the pandas API documentation for getting the syntax right. [pandas API](https://pandas.pydata.org/docs/reference/index.html)
- Multiple examples within the matplotlib documentation for creating the graphs used. [matplotlib API](https://matplotlib.org/stable/api/index.html)
- Multiple examples within the seaborn documentation for creating the graphs used. [seaborn API](https://seaborn.pydata.org/api.html)
- This answer for adjusting the location of the legend within graphs. [stackoverflow](https://stackoverflow.com/a/34579525)
- This stack overflow answer for calculating the number of verficiation methods in the listing. [stackovervlow](https://stackoverflow.com/a/52247415)
