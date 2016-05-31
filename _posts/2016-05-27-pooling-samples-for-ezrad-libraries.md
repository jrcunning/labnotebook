---
layout: post
title:  Pooling samples for ezRAD libraries
date: 2016-05-27
---

###Pooling samples
I will pool individual samples from each of the three groups (Bleached clade C ("BC"), Not bleached clade C ("NC"), Not bleached clade D ("ND")) for ezRAD library preparation. 

Each group has 14 samples, and the library should have a total of 1300ng DNA going into the digest. Conservatively assuming 50% loss during a bead clean, I will create pools of 2600 ng DNA. Therefore, we need 185.7142857 ng of each sample. Using the DNA concentrations from the AccuClear assay, the volumes of 185.7142857 ng for each sample are: 


{% highlight r %}
samples <- read.csv("samples.csv")
dnaconc <- read.csv("dnaconc.csv")
data <- merge(samples, dnaconc, by="colony")
data$needvol <- (2600/14) / data$ng.uL
data <- with(data, data[order(group, sample.date, colony), ])
knitr::kable(data, row.names=F)
{% endhighlight %}



| colony|group                  |sample.date |     ng.uL|   needvol|
|------:|:----------------------|:-----------|---------:|---------:|
|     25|Bleached - clade C     |10/24/14    | 13.474193| 13.782962|
|     39|Bleached - clade C     |10/24/14    | 17.506443| 10.608339|
|     53|Bleached - clade C     |10/24/14    | 20.293764|  9.151298|
|    125|Bleached - clade C     |10/24/14    | 25.706850|  7.224311|
|    131|Bleached - clade C     |10/24/14    | 17.045585| 10.895155|
|     71|Bleached - clade C     |11/4/14     | 18.074391| 10.274995|
|     77|Bleached - clade C     |11/4/14     | 31.690745|  5.860206|
|    119|Bleached - clade C     |11/4/14     | 20.586117|  9.021336|
|     51|Bleached - clade C     |5/6/15      | 19.600638|  9.474910|
|     57|Bleached - clade C     |5/6/15      | 17.826591| 10.417824|
|     65|Bleached - clade C     |5/6/15      | 14.086899| 13.183476|
|     79|Bleached - clade C     |5/6/15      | 17.728595| 10.475409|
|    127|Bleached - clade C     |5/6/15      | 14.393660| 12.902506|
|    137|Bleached - clade C     |5/6/15      |  8.571116| 21.667456|
|    132|Not bleached - clade C |1/14/15     | 20.110238|  9.234813|
|     40|Not bleached - clade C |10/24/14    | 17.256394| 10.762056|
|     44|Not bleached - clade C |10/24/14    | 14.461410| 12.842060|
|     66|Not bleached - clade C |10/24/14    | 10.931096| 16.989539|
|     72|Not bleached - clade C |10/24/14    | 18.695170|  9.933811|
|    110|Not bleached - clade C |10/24/14    | 14.609477| 12.711905|
|    124|Not bleached - clade C |10/24/14    | 22.247964|  8.347473|
|    128|Not bleached - clade C |10/24/14    | 14.615914| 12.706306|
|     54|Not bleached - clade C |12/17/14    | 41.904109|  4.431887|
|     80|Not bleached - clade C |12/17/14    | 35.535688|  5.226134|
|     92|Not bleached - clade C |12/17/14    | 46.357364|  4.006144|
|    122|Not bleached - clade C |12/17/14    | 33.199109|  5.593954|
|    130|Not bleached - clade C |12/17/14    | 17.877173| 10.388348|
|     84|Not bleached - clade C |5/6/15      | 17.155741| 10.825197|
|      2|Not bleached - clade D |10/24/14    | 21.161934|  8.775866|
|      8|Not bleached - clade D |10/24/14    | 17.712654| 10.484837|
|     12|Not bleached - clade D |10/24/14    | 28.459938|  6.525463|
|     32|Not bleached - clade D |10/24/14    | 14.751208| 12.589768|
|     52|Not bleached - clade D |10/24/14    | 19.731844|  9.411907|
|     58|Not bleached - clade D |10/24/14    | 22.344530|  8.311398|
|     70|Not bleached - clade D |10/24/14    | 13.823668| 13.434515|
|    120|Not bleached - clade D |10/24/14    | 13.082822| 14.195278|
|    126|Not bleached - clade D |10/24/14    | 17.553857| 10.579686|
|    138|Not bleached - clade D |10/24/14    | 15.025782| 12.359709|
|     20|Not bleached - clade D |12/17/14    | 44.167012|  4.204819|
|     78|Not bleached - clade D |12/17/14    | 38.870929|  4.777717|
|    112|Not bleached - clade D |12/17/14    | 26.649309|  6.968822|
|     26|Not bleached - clade D |5/6/15      | 19.619133|  9.465978|
  
***  

###Total volume of pooled DNA for each group:

{% highlight r %}
groupvols <- with(data, aggregate(data.frame(vol_DNA=needvol), by=list(group=group), FUN=sum))
knitr::kable(groupvols)
{% endhighlight %}



|group                  |  vol_DNA|
|:----------------------|--------:|
|Bleached - clade C     | 154.9402|
|Not bleached - clade C | 133.9996|
|Not bleached - clade D | 132.0858|

PIPET ERROR: 8.8 µL of sample 20 (in "ND" pool) was added instead of 4.2 µL, so this sample will be overrepresented in the library.
