---
layout: post
title:  Testing new extractions of KI Platy SDS archives
date:  2017-10-26 21:07:01
---

# Import data

{% highlight r %}
library(reshape2)
df <- read.delim("RC_20171026_KI_Platy_newextract_test_data.txt", skip=8)[, 1:7]
df <- df[!df$Well %in% c("A1", "A12", "H1", "H12"), ]
df <- df[!df$Sample.Name %in% c("+", "NEC1", "NTC"), ]
df$CT <- as.numeric(as.character(df$Cт))
{% endhighlight %}



{% highlight text %}
## Warning: NAs introduced by coercion
{% endhighlight %}



{% highlight r %}
df <- droplevels(df)

res <- dcast(df, Sample.Name ~ Target.Name, value.var = "CT", fun.aggregate=mean, na.rm=T)
res$C.H <- 2^(res$PaxC - res$C)
res$D.H <- 2^(res$PaxC - res$D)
res$S.H <- apply(res[, c("C.H", "D.H")], 1, sum, na.rm=T)
res$Date <- substr(res$Sample.Name, 1, 4)
res
{% endhighlight %}



{% highlight text %}
##    Sample.Name        C        D     PaxC          C.H          D.H
## 1   KI14-FQ019 32.49840      NaN 30.82860 3.142969e-01          NaN
## 2   KI14-FQ037 32.28820      NaN 26.46685 1.768475e-02          NaN
## 3   KI14-FQ072 25.47790      NaN 19.49565 1.581843e-02          NaN
## 4   KI14-FQ098      NaN 31.18990 33.10480          NaN 3.770877e+00
## 5   KI14-FQ104      NaN      NaN 38.62230          NaN          NaN
## 6   KI14-FQ107 26.92495 34.22640 29.35480 5.388374e+00 3.415877e-02
## 7  KI15c-FQ253 23.41830      NaN 18.04090 2.405699e-02          NaN
## 8  KI15c-FQ254 24.95570 28.68870 18.14780 8.925199e-03 6.712324e-04
## 9  KI15c-FQ261 29.57985      NaN 29.85110 1.206853e+00          NaN
## 10 KI15c-FQ273 24.51605 33.47675 17.92110 1.034480e-02 2.076265e-05
## 11 KI15c-FQ385 23.87770 35.37940 18.26200 2.039416e-02 7.033138e-06
## 12 KI15c-FQ404 32.10775 33.02630 29.94700 2.236400e-01 1.183146e-01
## 13 KI15c-FQ415 29.92285      NaN 35.22380 3.942257e+01          NaN
## 14 KI15c-FQ428 34.58480 31.87200 31.66045 1.317295e-01 8.636089e-01
## 15 KI15c-FQ436      NaN 32.09475 30.31860          NaN 2.919615e-01
## 16 KI15c-FQ460      NaN 36.34370      NaN          NaN          NaN
## 17 KI16a-FQ260 37.60260 30.09315 30.60265 7.812771e-03 1.423557e+00
## 18 KI16a-FQ261 37.72010 30.41870 34.94690 1.462796e-01 2.307406e+01
## 19 KI16a-FQ264 38.00685 30.94800 30.66955 6.183760e-03 8.244763e-01
## 20 KI16a-FQ265 35.61260 29.83415 34.35865 4.192986e-01 2.301496e+01
## 21 KI16a-FQ272 35.96250 25.35010 17.26545 2.353028e-06 3.683646e-03
##             S.H Date
## 1   0.314296911 KI14
## 2   0.017684754 KI14
## 3   0.015818428 KI14
## 4   3.770876757 KI14
## 5   0.000000000 KI14
## 6   5.422532812 KI14
## 7   0.024056991 KI15
## 8   0.009596431 KI15
## 9   1.206853033 KI15
## 10  0.010365566 KI15
## 11  0.020401195 KI15
## 12  0.341954574 KI15
## 13 39.422572044 KI15
## 14  0.995338356 KI15
## 15  0.291961491 KI15
## 16  0.000000000 KI15
## 17  1.431369514 KI16
## 18 23.220340016 KI16
## 19  0.830660101 KI16
## 20 23.434258144 KI16
## 21  0.003685999 KI16
{% endhighlight %}

# Plot S/H against PaxC CT values

{% highlight r %}
with(res, plot(S.H ~ PaxC, log="y"))
{% endhighlight %}



{% highlight text %}
## Warning in xy.coords(x, y, xlabel, ylabel, log): 2 y values <= 0
## omitted from logarithmic plot
{% endhighlight %}



{% highlight r %}
abline(h=0.3, lty=2)
{% endhighlight %}

![plot of chunk plot_SH](/labnotebook/figure/source/2017-10-26-testing-new-extractions-of-ki-platy-sds-archives/2017-10-26-testing-new-extractions-of-ki-platy-sds-archives/plot_SH-1.png)

Two groups of samples are visible: those where the host locus (PaxC) amplified in less than 20 cycles, and those in which it amplified after 30 cycles. For those that amplified earlier, S/H ratios are reasonable, whereas for those that amplified later, S/H ratios are all unrealistically high (above 0.3, which is biologically improbable). 

Next steps: for those samples that amplified late, test dilutions and different MasterMixes.

```
