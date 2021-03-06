---
layout: post
title:  Sampling intact colonies in wetlab
date:  2017-02-15 09:31:09
---

These colonies have been collected from various locations (Emerald, Port Miami, Palm Beach Co., ?) and have been held in Baker Lab tanks. Goal here is to sample each colony in three different places, extract DNA, and run clades A-D qPCR on each sample to (1) see which symbionts are present in which colonies and (2) troubleshoot any potential issues in DNA extraction/qPCR methods.

Samples were collected from each colony using a new razor blade to extract tissue from ~1 polyp (for *O. faveolata* and *S. siderea*, and the ridge of a polyp in *M. cavernosa*). Tissue samples were placed in tubes containing 500 µL 1% SDS in DNAB, and heated to 65°C for 90 min. DNA was extracted following CTAB-chloroform protocol and eluted in 100 µL TE buffer (10 mM Tris and 0.1 mM EDTA).


{% highlight r %}
df<- read.csv("2017-02-15-sampling.csv")
knitr::kable(df)
{% endhighlight %}



| Tag..|Species         | No..samples.taken|Date.Time     |Sampler |
|-----:|:---------------|-----------------:|:-------------|:-------|
|   946|Ofav (franksi?) |                 3|2/15/17 9:00  |RC      |
|   945|Ssid            |                 3|2/15/17 9:00  |RC      |
|   947|Mcav            |                 3|2/15/17 9:00  |RC      |
|   944|Mcav            |                 3|2/15/17 9:00  |RC      |
|   948|Ssid            |                 3|2/15/17 9:00  |RC      |
|   943|Ofav            |                 3|2/15/17 9:00  |RC      |
|   949|Ssid            |                 3|2/15/17 9:00  |RC      |
|   942|Ofav (franksi?) |                 3|2/15/17 9:00  |RC      |
|   950|Ssid            |                 3|2/15/17 9:00  |RC      |
|   936|Mcav            |                 3|2/15/17 16:00 |RK      |
|   937|Mcav            |                 3|2/15/17 16:00 |RK      |
|   938|Mcav            |                 3|2/15/17 16:00 |RK      |
|   941|Ssid            |                 3|2/15/17 16:00 |RK      |
|   939|Ssid            |                 3|2/15/17 16:00 |RK      |
|   940|Ssid            |                 3|2/15/17 16:00 |RK      |
|   935|Ssid            |                 3|2/15/17 16:00 |RK      |
|   934|Ssid            |                 3|2/15/17 16:00 |RK      |
|   933|Ssid            |                 3|2/15/17 16:00 |RK      |
|   932|Mcav            |                 3|2/15/17 16:00 |RK      |
