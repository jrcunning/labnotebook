---
layout: post
title:  Testing frozen KI Platygyra samples
date:  2017-11-12 21:08:05
---

# Import data

{% highlight r %}
options(stringsAsFactors = FALSE)
library(reshape2)
library(tidyr)
{% endhighlight %}



{% highlight text %}
## 
## Attaching package: 'tidyr'
{% endhighlight %}



{% highlight text %}
## The following object is masked from 'package:reshape2':
## 
##     smiths
{% endhighlight %}



{% highlight r %}
df <- read.delim("CH_20171110_KIFMDTest_data.txt", skip=8)[, 1:7]
df <- df[!df$Well %in% c("A1", "A12", "H1", "H12"), ]
df <- df[!df$Sample.Name %in% c("NEC", "NTC", "+ KI14-FQ72)"), ]
df$CT <- as.numeric(as.character(df$Cт))
{% endhighlight %}



{% highlight text %}
## Warning: NAs introduced by coercion
{% endhighlight %}



{% highlight r %}
df <- droplevels(df)
df <- separate(df, Sample.Name, into=c("time", "sample", "size"), fill="right")
res <- dcast(df, time + sample + size ~ Target.Name, value.var = "CT", fun.aggregate=mean)
colnames(res)[6] <- "H"
res$C.H <- 2^(res$H - res$C)
res$D.H <- 2^(res$H - res$D)
res$S.H <- apply(res[, c("C.H", "D.H")], 1, sum, na.rm=T)
print(res, digits=3)
{% endhighlight %}



{% highlight text %}
##     time sample size    C    D    H      C.H      D.H      S.H
## 1  KI15b  FMD23    B 24.8   NA 19.1 1.94e-02       NA 1.94e-02
## 2  KI15b  FMD23    L 24.9   NA 18.9 1.60e-02       NA 1.60e-02
## 3  KI15b FMD231    B   NA 24.9 19.3       NA 2.10e-02 2.10e-02
## 4  KI15b FMD231    L   NA 27.3 20.9       NA 1.16e-02 1.16e-02
## 5  KI15b FMD288    B 25.5 35.1 19.3 1.40e-02 1.83e-05 1.40e-02
## 6  KI15b FMD288    L 28.6   NA 21.8 8.78e-03       NA 8.78e-03
## 7  KI15c  FMD18    B 28.3   NA 18.4 1.02e-03       NA 1.02e-03
## 8  KI15c  FMD18    L 28.9   NA 18.6 8.11e-04       NA 8.11e-04
## 9  KI15c FMD254    B 25.3 27.9 18.0 6.71e-03 1.10e-03 7.82e-03
## 10 KI15c FMD254    L 26.7 30.1 19.2 5.76e-03 5.47e-04 6.31e-03
## 11 KI15c FMD468    B   NA 24.1 18.4       NA 1.93e-02 1.93e-02
## 12 KI15c FMD468    L   NA 26.4 18.7       NA 4.85e-03 4.85e-03
## 13 KI15c FMD488    B 30.5   NA 18.3 2.12e-04       NA 2.12e-04
## 14 KI15c FMD488    L 32.7   NA 19.2 8.11e-05       NA 8.11e-05
## 15 KI16a FMD116    B   NA 25.1 17.8       NA 6.50e-03 6.50e-03
## 16 KI16a FMD116    L 38.1 28.4 20.3 4.41e-06 3.69e-03 3.70e-03
## 17 KI16a  FMD17    B   NA 24.4 18.0       NA 1.16e-02 1.16e-02
## 18 KI16a  FMD17    L   NA 27.7 21.5       NA 1.36e-02 1.36e-02
## 19 KI16a  FMD49    L   NA 26.3 20.3       NA 1.56e-02 1.56e-02
## 20 KI16a  FMD89    B   NA 24.3 18.0       NA 1.29e-02 1.29e-02
## 21 KI16a  FMD89    L   NA 26.0 19.4       NA 1.01e-02 1.01e-02
{% endhighlight %}



{% highlight r %}
ggplot2::qplot(time, S.H, data=res, colour=size)
{% endhighlight %}

![plot of chunk unnamed-chunk-1](/labnotebook/figure/source/2017-11-12-testing-frozen-ki-platygyra-samples/2017-11-12-testing-frozen-ki-platygyra-samples/unnamed-chunk-1-1.png)

* All samples worked well, with host CT values from ~18-21.  
* There are lower S.H ratios at the 15c time point compared to 15b and 16a.  
* There does not appear to be a difference between the 'big' (B) and 'little' (L) samples.  



