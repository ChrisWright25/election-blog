---
title: 'Week 6: Campaign Ads'
author: "Chris Wright"
date: "2024-10-14"
output: pdf_document
categories: []
tags: []
slug: "week-6-campaign-ads"
---



<iframe width="560" height="315" src="https://www.youtube.com/watch?v=riDypP1KfOU" frameborder="0" allowfullscreen> </iframe>

The above video is the famous [Daisy girl ad from the 1964 election](https://www.livingroomcandidate.org/commercials/1964/peace-little-girl-daisy) between Lyndon B. Johnson and Barry Goldwater. The ad has a direct message: Electing Barry Goldwater will lead to nuclear catastrophe. The ad is often cited as one of the most effective ads as it remained in the public conscience despite only being aired once. Additionally, the ad is often regarded as the first political attack ad.

U.S. Presidential campaigns spend billions of dollars running advertisements across various forms of media including TV, Radio, and Social Media. Although they are a key component of the campaign strategy, the constant barrage of political ads in some key states has the opposite effect of [motivating voters](https://azmirror.com/2024/10/09/the-blitz-of-political-attack-ads-youre-seeing-may-be-doing-candidates-more-harm-than-good/). This week I will analyze data from the [Wesleyan Media Project](https://mediaproject.wesleyan.edu/) to better understand the composition and effect of political ads.


## What Type of Political Ads are Being Aired?

The term political ad is a broad umbrella and not all politcal ads are made the same. One way to break down politcal ads is how the position the candidate. In this breakdown, there are three way to categorize an ad: promoting a candidate, contrasting two candidates, attacking a candidate. The chart below shows how Democrats and Republicans have run ads within these categories from 2000-2012. The first trend that stands out is the decline in ads that directly promote a candidate. Another key takeaway is the significant amount of contrasting ads in the 2008 cycle by both parties. This could indicate that the parties thought the two candidates were very similar and needed to be diffrentiated to voters.


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />


Another way to categorize politcal ads is whether they focus on the candidate or their policies. The chart below shows the breakdown of this between Democrats and Republicans from 2000-2016. The interesting takeaway from this chart is the rise of personal ads in the 2016 cycle by Democrats. This rise was probably driven by personal scandals that surrounded Donald Trump. However, the data is not broken down into promote v. attack, so it is unclear if the ads were about Hillary or Trump as a person.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />


## When to Buy Political Ads

Another part of the strategy around political ads beyond what type of ad to run is when to air the ads. The graphs below chart the amount of ad spending in the elections from 2000-2012. The graphs all show that spending increases as the election gets closer. This trend indicates that campaigns believe in a voter behavior model where voters have a short term memory and make their mind up shortly before voting.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

# Bellweather Ad States

In elections, the term bellweather refers to locations that swing back and forth to accurately pick the winner. One of the most famous examples of a bellweather county in U.S. Presidential elections is [Clallam County in Washington](https://www.seattletimes.com/opinion/clallam-county-sure-knows-how-to-pick-em/) which has picked the Presidential winner accurately since 1976. In the same vein, the map below show which states are the "bellweathers" for ad spending from 2000-2012. The key takeaway from the map is that no state's ad buy has correctly predicted every election in the time frame. However, the states of Washington and Maine predicted 3 out of 4. Diving deeper into the data, most states had higher ad buys by Democrats in 2004; however, Kerry lost the election.




<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

## Updating Model

In the future, I may update my model to take into account campaign ad spending; however, I decided against it for now. This week, I updated my model with the latest national polling averages to get a national popular vote prediction. In the future, I will predict the electoral college to get a more accurate perception of the race. I used GDP Q2 growth, difference in S&P 500 open and close, and inflation (CPI) data to calculate a model. I then combined this model with a simple model using historical national polling averages to get a popular vote prediction. The ensemble model has Kamala Harris winning the popular vote __52%__ of the popular vote. This vote total should be enough to propel her to the White House as it is higher than Biden's in 2020 and Obama's in 2012.



