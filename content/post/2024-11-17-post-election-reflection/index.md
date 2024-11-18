---
title: Post Election Reflection
author: 'Chris Wright '
date: '2024-11-17'
slug: post-election-reflection
categories: []
tags: []
---


As the last votes for the 2024 US Presidential Election are counted, it is time to reflect on my model. In this reflection, I will go over my predictions for the electoral college and national popular vote. After comparing them with a simple eye test, the post will shift toward more rigorious error analysis. At the end of the post I will discuss what I think went wrong with the model and what I would change in future iterations of the model.


### Prediction vs. Results

Below are electoral college maps for the 2024 election. The map with my predictions is on the left and the correct map is on the right. My map predicts a Harris victory with 276 electoral votes. However, the correcnt map on the right shows a Trump victory with 312 electoral votes. My model incorrectly predicted the winning candidate in Nevada and the Blue Wall states: Pennsylvania, Michigan, and Wisconsin.



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

Digging deeper into the data, below is a graph showing my predictions for Harris' Two-Party vote share in each state and the national vote compared to the actual results. In the graph, the actual result is __green__ and my prediction is __brown__. The graph shows that my national vote prediction was off by several percentage points. 

The graph shows two interesting trends. The first trend is that my prediction was closest in North Carolina and Arizona. In both of these states, I predicted the correct vote share within less of a percentage point. On the surface, the two states have little in common that would easily explain why my model did well in both states. The states are geographically distant, North Carolina has 3 million more people than Arizona and Arizona is much more racially diverse. Another interesting trend is that I overshot the correct vote percentage in all of the predictions except Georgia. What caused this underestimate in Georgia?


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />



### Accuracy

The table below quantifies the error of each of the predictions. The table shows MSE which is one measure that can be used to interpret a predictive model. When it comes to MSE, the lower the value the better. Using MSE, Nevada was the biggest miss and North Carolina was the state where I was the closest in my prediction. MSE reveals "bands" of how large each miss was relatively. Michigan and Nevada were large misses, Pennsylvania and Wisconsin were moderate misses, Georgia was a small miss, and North Carolina and Arizona were relatively spot on. 

The second column on the table shows bias. Bias is useful for thinking about error of a model because it is in the units of prediction, unlike MSE, and also shows the directionality of the miss (over vs under estimate). 



Region | Mean Squared Error (MSE) | Bias
------------- | ------------- | -------------
National | 17.96 | -4.24
Arizona | 0.68 | -0.83
Georgia | 5.83 | 2.41
Michigan | 28.19 | -5.31
Nevada | 33.93 | -5.82
North Carolina | 0.08 | -0.28
Pennsylvania | 14.09 | -3.75
Wisconsin | 10.16 | -3.19


### Why Was the Model Wrong
- weighting of model (fundamentals)

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />


- model was the same for each state
- outliers of data
- polls are more predictive in some states


### What I Would Change Next Time








