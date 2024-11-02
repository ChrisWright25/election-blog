---
title: 'Week 8: Unexpected Shocks'
author: 'Chris Wright '
date: '2024-11-02'
slug: week-8-unexpected-shocks
categories: []
tags: []
---

This week, the focus is on unexpected events and shocks. These are events that are out of the control of the candidate but still have an effect on the election outcome. Since these events do not happen systematically, they are difficult to model and predict their impact. Quantitatively, the academic literature is split on the impact of "October Surprises". [Achen and Bartels](https://muse-jhu-edu.ezp-prod1.hul.harvard.edu/book/64646) famously unearthed a connection between shark attacks and the vote-share of the then incumbent Woodrow Wilson in the 1916 election. However, [Fowler and Hall's](https://www-journals-uchicago-edu.ezp-prod1.hul.harvard.edu/doi/full/10.1086/699244) research finds little connection between the two when more shark attacks are considered.

Unexpected events have also shaped recent elections including the Access Hollywood tapes and the [Comey Letter](https://fivethirtyeight.com/features/the-comey-letter-probably-cost-clinton-the-election/)) which was released days before the 2016 election. In the 2024 election, some unexpected events include the assassination attempts on Trump and recent hurricanes Helene and Milton. To analyze unexpected events and see what effect they will have on the 2024 election, this blog post will look into data on hurricanes and abortion.  


## Hurricanes

On the surface natural disasters like hurricanes can influence an election as they can diminish locals faith and trust in government thus hurting the incumbent. Natural disasters can also lower turnout in places directly impacted. However, what does the data say?

The chart below shows the prevalence of hurricanes leading up to the election. The data is subsetted to only include presidential election years since 1996. Interestingly, the graph shows that relatively few hurricanes happen in October. If you believe in a voter behavior model where recent events have the most impact, then this coudl be seen as reducing the effect of hurricanes on elections. However, the damage from hurricanes could be long-lasting.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />


Since the effect of hurricanes on elections is probably localized, I subset the data by states and included states with 20 or more hurricanes in an election year. The chart below shows the six states that meet the threshold and includes the count per year. For most states, 2004 was a year that saw many hurricanes, so 2004 could be a useful year to look at to determine the effect of hurricanes. Additionally, the year 1996 saw a large amount of hurricanes in North Carolina. The outcomes in 1996 could be helpful to understanding the 2024 election as North Carolina is still dealing with the effects of Hurricane Milton.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />


To try to tease out the effect of hurricanes, I plotted VEP turnout in the six states with the most election year hurricanes. The line charts below don't tell much of a story either way as turnout data is missing for some states. However, the Florida and Louisiana charts show that turnout in the 2004 Presidential election increased from the 2000 Presidential Election. Since 2004 was a year with many hurricanes, the increased turnout could be a reflection of hurricanes impacting the election.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

## Supreme Court and Ballot Measures

Another unexpected event that can shake up elections are Supreme Court decisions. One of the most recent court cases with the biggest impact is the reversal of Roe v. Wade in the Dobbs v. Jackson decision. In response to the decision, many states voted on ballot measures in the 2022 midterms to determine the state of abortion care. One way of seeing the impact of the Supreme Court's decision is to analyze turnout in the 2022 midterms compared to previous midterms.

The charts below do exactly this. The states selected are the [five states that had abortion on the ballot in the 2022 midterm cycle](https://ballotpedia.org/2022_abortion-related_ballot_measures). Interestingly, the turnout in every state dropped from the 2018 midterms to the 2022 cycle. However, in most states the turnout was also some of the highest since the start of the 21st century. The decline from 2018 to 2022 could be partially explained by the Covid pandmeic as it was still prevalent. Further research on demographics in the 2022 midterms could potentially unearth the effects of landmark Supreme court cases.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />




## Electoral College Prediction

Once again, I am predicting the Electoral College by creating models for the swing states below


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />



The prediction model combines polling data and fundamental economic data. The model uses historical polling in each state to predict based on the 2024 polling averages. The model also uses GDP quarter two growth and inflation (CPI). For the final prediction the model weighs polling data 3/4 and fundamental economic data 1/4 due to polling data being more in tune with 2024 events.






The individual state models predict a close election with Kamala Harris winning __Michigan, Wisconsin, Pennsylvania__ and Trump winning __Arizona, Georgia, Nevada, North Carolina__. This would result in Harris winning the Electoral College with exactly __270__ votes.



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

Listed below are the predicted two-party vote shares from the state models.


State | Harris Predicted Two-Party Vote | Trump Predicted Two-Party Vote
------------- | ------------- | -------------
Arizona | 44.6% | 55.4%
Georgia | 49.2% | 50.8%
Michigan | 50.9% | 49.1%
Nevada | 47.0% | 53.0%
North Carolina | 45.7% | 54.3%
Pennsylvania | 53.0% | 47.0%
Wisconsin | 51.8% | 48.2%
