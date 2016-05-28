---
layout: post
title:  Pooling samples for ezRAD libraries
date: 2016-05-27 15:20:06
---

I will pool individual samples from each of the three groups (Bleached clade C, Not bleached clade C, Not bleached clade D) for ezRAD library preparation. 

Each group has 14 samples, and the library should have a total of 1300ng DNA. Therefore, we need 92.8571429 ng of each sample. Using the DNA concentrations from the AccuClear assay, calculate the volume of 92.8571429 ng for each sample:


{% highlight r %}
samples <- read.csv("samples.csv")
dnaconc <- read.csv("dnaconc.csv")
data <- merge(samples, dnaconc, by="colony")
data$needvol <- (1300/14) / data$ng.uL
data <- with(data, data[order(group, sample.date, colony), ])
knitr::kable(data, row.names=F)
{% endhighlight %}



| colony|group                  |sample.date |     ng.uL|   needvol|
|------:|:----------------------|:-----------|---------:|---------:|
|     71|Bleached - clade C     |2014-11-04  | 18.074391|  5.137498|
|     77|Bleached - clade C     |2014-11-04  | 31.690745|  2.930103|
|    119|Bleached - clade C     |2014-11-04  | 20.586117|  4.510668|
|     25|Bleached - clade C     |2014-20-24  | 13.474193|  6.891481|
|     39|Bleached - clade C     |2014-20-24  | 17.506443|  5.304170|
|     53|Bleached - clade C     |2014-20-24  | 20.293764|  4.575649|
|    125|Bleached - clade C     |2014-20-24  | 25.706850|  3.612156|
|    131|Bleached - clade C     |2014-20-24  | 17.045585|  5.447577|
|     51|Bleached - clade C     |2015-05-06  | 19.600638|  4.737455|
|     57|Bleached - clade C     |2015-05-06  | 17.826591|  5.208912|
|     65|Bleached - clade C     |2015-05-06  | 14.086899|  6.591738|
|     79|Bleached - clade C     |2015-05-06  | 17.728595|  5.237705|
|    127|Bleached - clade C     |2015-05-06  | 14.393660|  6.451253|
|    137|Bleached - clade C     |2015-05-06  |  8.571116| 10.833728|
|     40|Not bleached - clade C |2014-10-24  | 17.256394|  5.381028|
|     44|Not bleached - clade C |2014-10-24  | 14.461410|  6.421030|
|     66|Not bleached - clade C |2014-10-24  | 10.931096|  8.494770|
|     72|Not bleached - clade C |2014-10-24  | 18.695170|  4.966906|
|    110|Not bleached - clade C |2014-10-24  | 14.609477|  6.355953|
|    124|Not bleached - clade C |2014-10-24  | 22.247964|  4.173737|
|    128|Not bleached - clade C |2014-10-24  | 14.615914|  6.353153|
|     54|Not bleached - clade C |2014-12-17  | 41.904109|  2.215944|
|     80|Not bleached - clade C |2014-12-17  | 35.535688|  2.613067|
|     92|Not bleached - clade C |2014-12-17  | 46.357364|  2.003072|
|    122|Not bleached - clade C |2014-12-17  | 33.199109|  2.796977|
|    130|Not bleached - clade C |2014-12-17  | 17.877173|  5.194174|
|    132|Not bleached - clade C |2015-01-14  | 20.110238|  4.617407|
|     84|Not bleached - clade C |2015-05-06  | 17.155741|  5.412599|
|      2|Not bleached - clade D |2014-10-24  | 21.161934|  4.387933|
|      8|Not bleached - clade D |2014-10-24  | 17.712654|  5.242419|
|     12|Not bleached - clade D |2014-10-24  | 28.459938|  3.262732|
|     32|Not bleached - clade D |2014-10-24  | 14.751208|  6.294884|
|     52|Not bleached - clade D |2014-10-24  | 19.731844|  4.705954|
|     58|Not bleached - clade D |2014-10-24  | 22.344530|  4.155699|
|     70|Not bleached - clade D |2014-10-24  | 13.823668|  6.717258|
|    120|Not bleached - clade D |2014-10-24  | 13.082822|  7.097639|
|    126|Not bleached - clade D |2014-10-24  | 17.553857|  5.289843|
|    138|Not bleached - clade D |2014-10-24  | 15.025782|  6.179855|
|      2|Not bleached - clade D |2014-12-17  | 21.161934|  4.387933|
|     78|Not bleached - clade D |2014-12-17  | 38.870929|  2.388858|
|    112|Not bleached - clade D |2014-12-17  | 26.649309|  3.484411|
|     26|Not bleached - clade D |2015-05-06  | 19.619133|  4.732989|

