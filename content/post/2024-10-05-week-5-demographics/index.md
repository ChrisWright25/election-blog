---
title: 'Week 5: Demographics'
author: Chris Wright
date: '2024-10-05'
slug: week-5-demographics
categories: []
tags: []
---


Demographics and election prediction go hand-in-hand. Demographics refers to statistics about the population (Ex: Gender, Race, Age). Understanding demographics, their voting patterns, and predicting their turnout are key to an election outcome as a shift in key demographics have been the deciding factor in many elections. In the 1920 Presidential election, [Warren G. Harding won the presidency](https://www.womenshistory.org/articles/womens-political-participation-after-1920-myth-and-reality) partially due to the 19th Amendment which introduced a new demographic to the voting population: women. More recently, the 2008 election and 2016 election hinged on high turnout from unlikely demographics. In 2008, [Black voters turned out at a high leve](https://academic.oup.com/poq/article/73/5/995/1868700)l to carry Obama to the White House and in 2016 [large turnout among rural voters](https://www.npr.org/2016/11/14/501737150/rural-voters-played-a-big-part-in-helping-trump-defeat-clinton) catapulted Trump to victory.

Although demographics are a critical part of election prediction they are not everything. In a recent 2022 article, [Seo-young Silvia Kim & Jan Zilinsky](https://link.springer.com/article/10.1007/s11109-022-09816-z) analyzed the predictive power of demographics in elections. The chart below shows the accuracy of demographics alone compared to also including party identification or issue preferences.

<img src="Kim_Zilinsky.png" width="33%" height="33%" style="display: block; margin: auto;" />


The takeaway from the graph and the article is that demographics alone have relatively low predictive power as only around 60% of partisan vote choices were accurately explained by the demographics alone model. However, the graph also shows that demographics are still useful when combined with other variables. So, how do demographics look in the 2024 election and what effect might they have?

## Analyzing the Voterfile

Although it is impossible to know the demographics of voters before the election occurs, there are some tools that we can use to predict to the demographics of the election. One of the tools are lists of registered voters in each state. Although all registered voters will not turnout and some voters will register on election day, the lists give a good hint of potential demographics. Using these lists of registered voters, I will analyze a few demographics: Age, Married, Renters / Homeowners





#### Age

The map below shows the average age of registered voters in each state. Although the range is relatively small as it goes from 50 to 65, there are still some interesting comparative insights. The swing states of Nevada, Georgia, and North Carolina standout. Nevada has one of the oldest voting populations in the U.S., but Georgia and North Carolina have some of the youngest in the country. Understanding voting preferences of the elderly and youth appear to be critical in predicitng the election outcome in these states.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />


#### Married

The map below shows the percent of registered voters in each state that are married. North Carolina once again stands out as it has one of the highest percentage of single voters in the nation. This could hint that the candidate that better addresses issues that are critical to single voters could win the swing state.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />


#### Renters

Due to rising housing prices and its centrality as a political issue during this presidential cycle, I decided to include a graph on housing demographics in swing states. The map below shows the percentage of registered voters in each state that have never voted before and are renters. The map highlights the effect that housing policy could have on the election in Nevada as a large percentage __(72.2%)__ of registered voters rent and have never voted before. Although the percentage of renters is low in other swing states, the demographic could still swing the election as the race is expected to be narrow in each state.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />







## Analyzing New Prediction Model

Centering on the housing issue, I decided to adjust the election prediction model to include data about housing. Using data from [FRED](https://fred.stlouisfed.org/), I added in historical data on rental and housing vacancy rates. Along with the housing data, I used GDP Q2 growth, difference in S&P 500 open and close, and inflation (CPI) data to calculate a model. I then combined this model with a simple model using historical national polling averages to get a popular vote prediction. As I constructed the predictions, I noticed a significant difference based on whether I incldued or excluded "outliers". In the case of the fundamental data the 2020 election is an outlier and in the case of polling averages the 2016 and 2020 elections are excluded as outliers. The two models and their predictions are listed below.

Model | Harris Predicted Vote | Trump Predicted Vote
------------- | ------------- | -------------
Ensemble All Data | 53.4 % | 46.6%
Ensemble Without Outliers | 47.6% | 52.4%







