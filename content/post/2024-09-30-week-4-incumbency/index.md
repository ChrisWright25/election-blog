---
title: 'Week 4: Incumbency'
author: Chris Wright
date: '2024-09-30'
slug: week-4-incumbency
categories: []
tags: []
---

## Incumbency Advantage

The term incumbency is always brought up when discussing forecasting elections, but why? In elections, incumbency is often seen as a boost In other words, those in office tend to stay in office. The graph below shows the percentage of congress members reelected since 1964. The graph supports the idea of an incumbency advantage as both Senators and Representatives have higher  than 60% reelection rate. 



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

However, incumbency at the presidential level is more nuanced and can be analyzed many different ways. One way of defining incumbency is the exact candidate. For example, Obama in the 2012 election would be an incumbent. In the __11__ presidential elections since 1948 with at least one incumbent running, __7__ incumbents have won reelection. Another way of considering incumbency is through party affiliation. For example, Kamala Harris would be an incumbent under this definition. This definition gives less power to the idea of an incumbency advantage as only __8__ of the __18__  presidential elections have been won by the incumbent party. Lastly, a broad definition of incumbency could be candidates that have served in past presidential administrations. This definition captures candidates like Hillary Clinton who was Obama's secretary of state. Under this advantage the incumbency advantage shrinks even more as only __27%__ of presidential winners since 1948 have served in past administrations.  

Even if we agree that the incumbency advantage exists, where does it come from? One explanation for incumbents having an advantage is their use of federal grants to increase favorability amongst voters. This is often termed __pork barrel spending__. The chart below gives some credence to this idea as federal grant spending increases significantly when comparing swing states to non-electorally competitive states.



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />


## Who is the Incumbent in the 2024 Election?

The issue of who is the incumbent in the 2024 election is easily answerable on the surface. Joe Biden isn't running so there is no incumbent. However, this question gets complicated under the surface. One could claim that Kamala Harris is the incumbent. This would align with the earlier definition of incumbents being from previous presidential administrations. However, the Vice President is not the President, so voters may not assign the same incumbency advantage to Kamala. Donald Trump also has a claim to incumbency. His steady presence in the media since the 2020 election has kept his name recognition in line with those of incumbents. Trump's claim to  incumbency is also validated by looking at past presidents who have sought nonconsecutive terms. Although Grover Cleveland is the only president to serve nonconsecutive terms, other past presidents have received an [outsized portion](https://www.pewresearch.org/short-reads/2022/11/16/few-former-presidents-have-run-for-their-old-jobs-or-anything-else-after-leaving-office/) of the popular vote when they ran. This includes Martin Van Buren __(10%)__, Millard Fillmore __(21.6%)__, and Theodore Roosevelt __(27.4%)__. Their ability to capture large portions of the popular vote hint that they benefited from the incumbency advantage.

Interestingly though, the 2024 election seems to be defined by both candidates not wanting to be deemed the incumbent. Each campaign is seeking to be the "change" candidate. Polling has been conflicted on who is better distancing themselves from incumbency. A recent [NYTimes / Sienna poll](https://www.nytimes.com/interactive/2024/09/08/us/politics/times-siena-poll-likely-electorate-crosstabs.html) indicates that Trump better represents change while an [NBC News poll](https://www.nbcnews.com/politics/2024-election/poll-newly-popular-harris-challenging-trump-change-rcna171308) has Harris leading by 9 points on the question of representing change. 


## Time for a Change Model

One election model that is built around the idea of incumbents is the [Time for Change model](https://centerforpolitics.org/crystalball/time-for-change-model-predicts-close-election-with-slight-edge-for-kamala-harris/). The model only uses three inputs: __GDP growth in the second quarter, whether an incumbent is running, and the june approval polling of the incumbent president__. The model has been very accurate in predicting post war elections as seen in the chart below. The model's predictions are _triangles_ and the actual results are _circles_. Only in 1968 and 2016 did the model get the popular vote wrong. In addition to these election years, the model missed on the electoral college in 2000. 
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />





While the Time for Change model is highly accurate and has a high R-squared (.82), my preferred model uses more inputs centered around the economy and using regularization to prevent overfitting which is an issue that election models are highly susceptible to due to the limited observations available. Although the time for change model favors Harris more than mine, both my model and the Time for Change model predict Kamala Harris to get below 50% of the two-party popular vote share in the 2024 election.

Model | Predicted Harris Voteshare
------------- | -------------
Time for Change | 48.9%
My Model | 47.6% 










