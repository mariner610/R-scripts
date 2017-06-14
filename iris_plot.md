iris_plot
========================================================
author: 오정희
date: 2017. 6. 14
autosize: true

First Slide
========================================================



Slide With Code
iris 데이터요약..
========================================================


```r
summary(iris)
```

```
  Sepal.Length    Sepal.Width     Petal.Length    Petal.Width   
 Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
 1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
 Median :5.800   Median :3.000   Median :4.350   Median :1.300  
 Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199  
 3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
 Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
       Species  
 setosa    :50  
 versicolor:50  
 virginica :50  
                
                
                
```

Slide With Plot
========================================================


```r
library(ggplot2)
ggplot(iris, aes(Sepal.Length, Sepal.Width, col=Species)) +
  geom_point(size=2) +
  theme_bw() +
  facet_wrap(~Species)  
```

![plot of chunk unnamed-chunk-2](iris_plot-figure/unnamed-chunk-2-1.png)

이것참..고약하구먼..

