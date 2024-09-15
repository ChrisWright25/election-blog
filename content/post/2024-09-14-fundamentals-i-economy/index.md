---
title: 'Fundamentals I: Economy'
author: Package Build
date: '2024-09-14'
slug: fundamentals-i-economy
categories: []
tags: []
---




<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

```
## [1] 0.4336956
```

```
## 
## Call:
## lm(formula = pv2p ~ GDP_growth_quarterly, data = d_inc_econ)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -6.7666 -3.3847 -0.7697  2.9121  8.8809 
## 
## Coefficients:
##                      Estimate Std. Error t value Pr(>|t|)    
## (Intercept)           51.2580     1.1399  44.968   <2e-16 ***
## GDP_growth_quarterly   0.2739     0.1380   1.985   0.0636 .  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.834 on 17 degrees of freedom
## Multiple R-squared:  0.1881,	Adjusted R-squared:  0.1403 
## F-statistic: 3.938 on 1 and 17 DF,  p-value: 0.06358
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-2.png" width="672" />

```
## [1] 0.1880919
```

```
## [1] 0.1403326
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-3.png" width="672" />

```
## [1] 20.90708
```

```
## [1] 4.572426
```

```
## [1] 2.166803
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-4.png" width="672" />

```
##        1 
## 52.07966
```

```
##        fit      lwr      upr
## 1 52.07966 41.61124 62.54808
```


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

```
## [1] -0.1368118
```

```
## 
## Call:
## lm(formula = pv2p ~ unemployment, data = d_inc_econ)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -7.9906 -2.6616 -0.9256  2.4016  9.9399 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   53.6260     3.4614  15.493 1.85e-11 ***
## unemployment  -0.3117     0.5475  -0.569    0.577    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.314 on 17 degrees of freedom
## Multiple R-squared:  0.01872,	Adjusted R-squared:  -0.03901 
## F-statistic: 0.3243 on 1 and 17 DF,  p-value: 0.5765
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-2.png" width="672" />

```
## [1] 0.01871748
```

```
## [1] -0.03900502
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-3.png" width="672" />

```
## [1] 25.26856
```

```
## [1] 5.026784
```

```
## [1] 2.222199
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-4.png" width="672" />

```
##        1 
## 52.37907
```

```
##        fit      lwr      upr
## 1 52.37907 40.66441 64.09372
```




<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-2.png" width="672" />

```
## [1] 0.7320144
```

```
## 
## Call:
## lm(formula = pv2p ~ CPI + sp500move, data = d_inc_econ)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.4419 -3.6724  0.0844  2.6027  8.8449 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 53.456624   2.247535  23.785 6.51e-14 ***
## CPI         -0.011194   0.022038  -0.508    0.618    
## sp500move   -0.008195   0.021502  -0.381    0.708    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.291 on 16 degrees of freedom
## Multiple R-squared:  0.08463,	Adjusted R-squared:  -0.02979 
## F-statistic: 0.7397 on 2 and 16 DF,  p-value: 0.4929
```

```
## [1] 0.08463345
```

```
## [1] -0.02978737
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-3.png" width="672" />

```
## [1] 23.57119
```

```
## [1] 4.855017
```

```
## [1] 2.293806
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-4.png" width="672" />

```
##       1 
## 48.1426
```

```
##       fit      lwr      upr
## 1 48.1426 34.96623 61.31897
```



