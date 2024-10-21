---
title: 'Week 7: The Ground Game'
author: Chris Wright
date: '2024-10-19'
slug: week-6-the-ground-game
categories: []
tags: []
---





## Field Offices






## Campaign Events



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />





<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />
## Electoral College Model


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />



















``` r
# Map for final prediction
prediction_data_final <- data.frame(state = c("AL","AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA", "HI" , "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD","MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC","SD", "TN","TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"), value = c(0, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 1, 0))


plot_usmap(region = "states", 
           data = prediction_data_final,
           values = "value",
           color = "white") + scale_fill_gradient(low = "firebrick", high = "steelblue1")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

State | Harris Predicted Two-Party Vote | Trump Predicted Two-Party Vote
------------- | ------------- | -------------
Arizona | 46.8% | 53.2%
Georgia | 48.5% | 51.5%
Michigan | 52.4% | 47.6%
Nevada | 49.2% | 50.8%
North Carolina | 47.0% | 53.0%
Pennsylvania | 52.4% | 47.6%
Wisconsin | 51.8% | 48.2%


