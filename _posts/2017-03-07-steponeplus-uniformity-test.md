---
layout: post
title:  StepOnePlus Uniformity Test
date:  2017-03-07 13:26:34
---

# Rationale
Testing the Baker Lab StepOnePlus machine for any potential variation among wells due to machine error/variability. Machine was calibrated (spatial, background, and dye) on 03/06/2017. To test for any variability, I will run a plate with 96 technical replicates, i.e., the same reaction in each well, that includes amplification of both C and D actin loci.

# Methods
* Prepare DNA template: (210 µL total)
  + 10 µL Mc16-47t0 (Rivah's sample, contains clade C)
  + 10 µL 942-1 (see previous entry, contains clade D)
  + 180 µL H2O

* Prepare qPCR MasterMix:
  + Each reaction: 5 µL GTMM; 0.5 µL each of CFor, CRev, CProbe, DFor, DRev, DProbe; (no water)
  + MasterMix (n=98): 490 µL GTMM; 49 µL each oligo

* Add 8 µL MasterMix to each well
* Add 2 µL mixed C+D DNA template to each well

# Results

### Raw data files:  

[.eds]({{ site.baseurl }}/_source/2017-03-07-steponeplus-uniformity-test/20170307_RC_UniformityTest.eds)  
[.txt]({{ site.baseurl }}/_source/2017-03-07-steponeplus-uniformity-test/20170307_RC_UniformityTest_data.txt)


{% highlight r %}
library(reshape2)
df <- read.delim("20170307_RC_UniformityTest_data.txt", skip=8)
df <- dcast(df, formula=Well~Target.Name, value.var="Cт")
{% endhighlight %}

### Visualize plates: 

{% highlight r %}
library(platetools)
raw_map(data=df$C, well=df$Well, plate=96)
{% endhighlight %}

![plot of chunk visualize_plates](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/visualize_plates-1.png)

{% highlight r %}
raw_map(data=df$D, well=df$Well, plate=96)
{% endhighlight %}

![plot of chunk visualize_plates](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/visualize_plates-2.png)

### Run some stats:

{% highlight r %}
library(effects)
library(lsmeans)
{% endhighlight %}



{% highlight text %}
## Loading required package: estimability
{% endhighlight %}



{% highlight text %}
## Loading required package: methods
{% endhighlight %}



{% highlight r %}
df$row <- substr(df$Well, 1,1)
df$col <- substr(df$Well, 2,3)
df$corner <- factor(ifelse(df$Well %in% c("A1", "A12", "H1", "H12"), "corner", "not_corner"))
df$border <- factor(ifelse(df$row %in% c("A", "H") | df$col %in% c(1, 12), "border", "not_border"))
str(df)
{% endhighlight %}



{% highlight text %}
## 'data.frame':	96 obs. of  7 variables:
##  $ Well  : Factor w/ 96 levels "A1","A10","A11",..: 1 2 3 4 5 6 7 8 9 10 ...
##  $ C     : num  27.4 26.5 26.2 27.2 26.6 ...
##  $ D     : num  28.4 27.4 27.4 28.3 27.6 ...
##  $ row   : chr  "A" "A" "A" "A" ...
##  $ col   : chr  "1" "10" "11" "12" ...
##  $ corner: Factor w/ 2 levels "corner","not_corner": 1 2 2 1 2 2 2 2 2 2 ...
##  $ border: Factor w/ 2 levels "border","not_border": 1 1 1 1 1 1 1 1 1 1 ...
{% endhighlight %}



{% highlight r %}
# Are corners different?
mod <- lm(C ~ corner, data=df)
anova(mod)  # YES
{% endhighlight %}



{% highlight text %}
## Analysis of Variance Table
## 
## Response: C
##           Df Sum Sq Mean Sq F value    Pr(>F)    
## corner     1 6.0001  6.0001  178.52 < 2.2e-16 ***
## Residuals 94 3.1593  0.0336                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
{% endhighlight %}



{% highlight r %}
plot(effect("corner", mod), main="Corner effect - C assay")
{% endhighlight %}

![plot of chunk platestats](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/platestats-1.png)

{% highlight r %}
# Pairwise comparison
pairs(lsmeans(mod, specs="corner"))
{% endhighlight %}



{% highlight text %}
##  contrast            estimate         SE df t.ratio p.value
##  corner - not_corner   1.2511 0.09363602 94  13.361  <.0001
{% endhighlight %}



{% highlight r %}
mod <- lm(D ~ corner, data=df)
anova(mod)  # YES
{% endhighlight %}



{% highlight text %}
## Analysis of Variance Table
## 
## Response: D
##           Df Sum Sq Mean Sq F value    Pr(>F)    
## corner     1 6.4562  6.4562  119.04 < 2.2e-16 ***
## Residuals 94 5.0982  0.0542                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
{% endhighlight %}



{% highlight r %}
plot(effect("corner", mod), main="Corner effect - D assay")
{% endhighlight %}

![plot of chunk platestats](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/platestats-2.png)

{% highlight r %}
# Pairwise comparison
pairs(lsmeans(mod, specs="corner"))
{% endhighlight %}



{% highlight text %}
##  contrast            estimate        SE df t.ratio p.value
##  corner - not_corner 1.297778 0.1189481 94   10.91  <.0001
{% endhighlight %}



{% highlight r %}
# Are borders different?
mod <- lm(C ~ border, data=df)
anova(mod)  # YES
{% endhighlight %}



{% highlight text %}
## Analysis of Variance Table
## 
## Response: C
##           Df Sum Sq Mean Sq F value    Pr(>F)    
## border     1 2.6017 2.60171  37.294 2.272e-08 ***
## Residuals 94 6.5577 0.06976                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
{% endhighlight %}



{% highlight r %}
plot(effect("border", mod), main="Border effect - C assay")
{% endhighlight %}

![plot of chunk platestats](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/platestats-3.png)

{% highlight r %}
# Pairwise comparison
pairs(lsmeans(mod, specs="border"))
{% endhighlight %}



{% highlight text %}
##  contrast             estimate         SE df t.ratio p.value
##  border - not_border 0.3400467 0.05568279 94   6.107  <.0001
{% endhighlight %}



{% highlight r %}
mod <- lm(D ~ border, data=df)
anova(mod)  # YES
{% endhighlight %}



{% highlight text %}
## Analysis of Variance Table
## 
## Response: D
##           Df Sum Sq Mean Sq F value    Pr(>F)    
## border     1 4.1140  4.1140  51.975 1.402e-10 ***
## Residuals 94 7.4405  0.0792                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
{% endhighlight %}



{% highlight r %}
plot(effect("border", mod), main="Border effect - D assay")
{% endhighlight %}

![plot of chunk platestats](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/platestats-4.png)

{% highlight r %}
# Pairwise comparison
pairs(lsmeans(mod, specs="border"))
{% endhighlight %}



{% highlight text %}
##  contrast             estimate         SE df t.ratio p.value
##  border - not_border 0.4276022 0.05931226 94   7.209  <.0001
{% endhighlight %}



{% highlight r %}
# Are borders different without corners included?
mod <- lm(C ~ border, data=subset(df, corner=="not_corner"))
anova(mod)  # YES
{% endhighlight %}



{% highlight text %}
## Analysis of Variance Table
## 
## Response: C
##           Df  Sum Sq Mean Sq F value    Pr(>F)    
## border     1 0.98039 0.98039  49.752 3.464e-10 ***
## Residuals 90 1.77351 0.01971                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
{% endhighlight %}



{% highlight r %}
plot(effect("border", mod), main="Border effect (w/o corners) - C assay")
{% endhighlight %}

![plot of chunk platestats](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/platestats-5.png)

{% highlight r %}
# Pairwise comparison
pairs(lsmeans(mod, specs="border"))
{% endhighlight %}



{% highlight text %}
##  contrast             estimate         SE df t.ratio p.value
##  border - not_border 0.2167415 0.03072829 90   7.053  <.0001
{% endhighlight %}



{% highlight r %}
mod <- lm(D ~ border, data=subset(df, corner=="not_corner"))
anova(mod)  # YES
{% endhighlight %}



{% highlight text %}
## Analysis of Variance Table
## 
## Response: D
##           Df Sum Sq Mean Sq F value    Pr(>F)    
## border     1 1.9483  1.9483  63.263 5.076e-12 ***
## Residuals 90 2.7718  0.0308                      
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
{% endhighlight %}



{% highlight r %}
plot(effect("border", mod), main="Border effect (w/o corners) - D assay")
{% endhighlight %}

![plot of chunk platestats](/labnotebook/figure/source/2017-03-07-steponeplus-uniformity-test/2017-03-07-steponeplus-uniformity-test/platestats-6.png)

{% highlight r %}
# Pairwise comparison
pairs(lsmeans(mod, specs="border"))
{% endhighlight %}



{% highlight text %}
##  contrast             estimate         SE df t.ratio p.value
##  border - not_border 0.3055456 0.03841505 90   7.954  <.0001
{% endhighlight %}


