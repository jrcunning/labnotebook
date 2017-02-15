---
layout: post
title:  Core inventory
date:  2017-02-14 15:48:56
---

Inventorying coral cores that have been held long term in experimental tanks in the Baker Lab at RSMAS.


{% highlight r %}
cores <- read.csv("cores_draft.csv")
cores$dup <- ifelse(duplicated(cores), T, F)
knitr::kable(cores)
{% endhighlight %}



|Species | Genotype|Frag |dup   |
|:-------|--------:|:----|:-----|
|Mc      |        1|26   |FALSE |
|Mc      |        1|28   |FALSE |
|Mc      |        1|3    |FALSE |
|Mc      |        1|1    |FALSE |
|Mc      |        1|24   |FALSE |
|Mc      |        1|30   |FALSE |
|Mc      |        1|19   |FALSE |
|Mc      |        1|9    |FALSE |
|Mc      |        1|8    |FALSE |
|Mc      |        1|4    |FALSE |
|Mc      |        1|13   |FALSE |
|Mc      |        1|11   |FALSE |
|Mc      |        1|5    |FALSE |
|Mc      |        1|6    |FALSE |
|Mc      |        1|14   |FALSE |
|Mc      |        1|32   |FALSE |
|Mc      |        1|12   |FALSE |
|Mc      |        1|21   |FALSE |
|Mc      |        1|15   |FALSE |
|Mc      |        2|15   |FALSE |
|Mc      |        2|36   |FALSE |
|Mc      |        2|7    |FALSE |
|Mc      |        2|27   |FALSE |
|Mc      |        2|17   |FALSE |
|Mc      |        2|2    |FALSE |
|Mc      |        2|25   |FALSE |
|Mc      |        2|16   |FALSE |
|Mc      |        2|7    |TRUE  |
|Mc      |        2|45   |FALSE |
|Mc      |        2|6    |FALSE |
|Mc      |        2|35   |FALSE |
|Mc      |        2|9    |FALSE |
|Mc      |        2|11   |FALSE |
|Mc      |        2|18   |FALSE |
|Mc      |        2|20   |FALSE |
|Mc      |        2|22   |FALSE |
|Mc      |        2|12   |FALSE |
|Mc      |        2|5    |FALSE |
|Mc      |        2|28   |FALSE |
|Mc      |        2|4    |FALSE |
|Mc      |        2|20   |TRUE  |
|Mc      |        2|10   |FALSE |
|Mc      |        3|5    |FALSE |
|Mc      |        3|22   |FALSE |
|Mc      |        3|20   |FALSE |
|Mc      |        3|15   |FALSE |
|Mc      |        3|24   |FALSE |
|Mc      |        3|26   |FALSE |
|Mc      |        3|?    |FALSE |
|Mc      |        3|1    |FALSE |
|Mc      |        3|29   |FALSE |
|Mc      |        3|13   |FALSE |
|Mc      |        3|?    |TRUE  |
|Mc      |        3|16   |FALSE |
|Mc      |        3|19   |FALSE |
|Mc      |        3|1    |TRUE  |
|Mc      |        3|?    |TRUE  |
|Mc      |        3|18   |FALSE |
|Mc      |        3|32   |FALSE |
|Mc      |        3|10   |FALSE |
|Mc      |        3|18   |TRUE  |
|Mc      |        3|4    |FALSE |
|Mc      |        3|2?   |FALSE |
|Mc      |        3|3    |FALSE |
|Mc      |        3|?    |TRUE  |
|Mc      |        3|6    |FALSE |
|Mc      |        3|27   |FALSE |
|Mc      |        4|21   |FALSE |
|Mc      |        4|15   |FALSE |
|Mc      |        4|19   |FALSE |
|Mc      |        4|12   |FALSE |
|Mc      |        4|11   |FALSE |
|Mc      |        4|9    |FALSE |
|Mc      |        4|24   |FALSE |
|Mc      |        4|7    |FALSE |
|Mc      |        4|18   |FALSE |
|Mc      |        4|17   |FALSE |
|Mc      |        4|10   |FALSE |
|Mc      |        4|22   |FALSE |
|Mc      |        4|20   |FALSE |
|Mc      |        4|6    |FALSE |
|Mc      |        4|13   |FALSE |
|Mc      |        4|?    |FALSE |
|Mc      |        4|23   |FALSE |
|Mc      |        4|?    |TRUE  |
|Mc      |        4|8    |FALSE |
|Mc      |        4|5    |FALSE |
|Mc      |        5|8    |FALSE |
|Mc      |        5|10   |FALSE |
|Mc      |        5|15   |FALSE |
|Mc      |        5|12   |FALSE |
|Mc      |        5|12   |TRUE  |
|Mc      |        5|20   |FALSE |
|Mc      |        5|2    |FALSE |
|Mc      |        5|14   |FALSE |
|Mc      |        5|24   |FALSE |
|Mc      |        5|2    |TRUE  |
|Mc      |        5|6    |FALSE |
|Mc      |        5|6    |TRUE  |
|Mc      |        6|18   |FALSE |
|Mc      |        6|5    |FALSE |
|Mc      |        6|14   |FALSE |
|Mc      |        6|?    |FALSE |
|Mc      |        6|12   |FALSE |
|Mc      |        6|23   |FALSE |
|Mc      |        6|22   |FALSE |
|Mc      |        6|4    |FALSE |
|Mc      |        6|8    |FALSE |
|Mc      |        6|?    |TRUE  |
|Mc      |        6|3    |FALSE |
|Mc      |        6|13   |FALSE |
|Mc      |        6|10   |FALSE |
|Mc      |        8|8    |FALSE |
|Ss      |       12|2    |FALSE |
|Ss      |       12|5    |FALSE |
|Ss      |       12|6    |FALSE |
|Ss      |       12|16   |FALSE |
|Ss      |       12|13   |FALSE |
|Ss      |       12|6    |TRUE  |
|Ss      |       12|11   |FALSE |
|Ss      |       11|?    |FALSE |
|Ss      |       11|?    |TRUE  |
|Ss      |       11|15   |FALSE |
|Ss      |        9|18   |FALSE |
|Ss      |        9|15   |FALSE |
|Ss      |        9|12   |FALSE |
|Ss      |        9|9    |FALSE |
|Ss      |        9|25   |FALSE |
|Ss      |        9|6    |FALSE |
|Ss      |        9|7    |FALSE |
|Ss      |        9|16   |FALSE |
|Ss      |        9|5    |FALSE |
|Ss      |        9|57   |FALSE |
|Of      |        2|6    |FALSE |
|Of      |        2|8    |FALSE |
|Of      |        4|9    |FALSE |
|Of      |        4|33   |FALSE |
|Of      |        4|4    |FALSE |
|Of      |        4|5    |FALSE |
|Of      |        4|18   |FALSE |
|Of      |        4|6    |FALSE |
|Of      |        4|11   |FALSE |
|Of      |        4|16   |FALSE |
|Of      |        4|38   |FALSE |
|Of      |        4|7    |FALSE |
|Of      |        4|1    |FALSE |
|Of      |        4|35   |FALSE |
|Of      |        4|25   |FALSE |
