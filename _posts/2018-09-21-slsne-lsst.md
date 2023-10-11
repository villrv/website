---
layout: post
title:  SLSNe in LSST
date: 2018-09-21 09:56:00-0400
description: counting superluminous supernovae
categories: research
tags: astronomy, research
giscus_comments: false
related_posts: false
related_publications: villar2018superluminous
---


We recently submitted a [new paper](https://arxiv.org/abs/1805.08192)  to the Astrophysical Journal which presents detailed simualtions of Type I superluminous supernovae obseved with the upcoming Large Synoptic Survey Telescope.

We fit the light curves of 58 known SLSNe at z~0.1-1.6, using an analytical magnetar spin-down model implemented in MOSFiT. We then use the posterior distributions of the magnetar and ejecta parameters to generate thousands of synthetic SLSN light curves, and we inject those into the OpSim to generate realistic ugrizy light curves. 

![sample slsn light curves](/images/slsn_lsst/f1.png)
*Sample SLSN light curves*

We define simple, measurable metrics to quantify the detectability and utility of the light curve, and to measure the efficiency of LSST in returning SLSN light curves satisfying these metrics. 

![efficienies as function of redshift](/images/slsn_lsst/f2.png)
*Recovery efficiency as a function of redshift*

We combine the metric efficiencies with the volumetric rate of SLSNe to estimate the overall discovery rate of LSST, and we find that ~10^4 SLSNe per year with >10 data points will be discovered in the WFD survey at z<3.0, while only ~15 SLSNe per year will be discovered in each DDF at z<4.0. 

![number of discovered slsne as function of redshift](/images/slsn_lsst/f3.png)
*Number of discovered SLSNe as a function of redshift*


To evaluate the information content in the LSST data, we refit representative output light curves with the same model that was used to generate them. 


![refitted light curves](/images/slsn_lsst/f4.png)
*Sample SLSN light curves with best-fit magnetar models*

We correlate our ability to recover magnetar and ejecta parameters with the simple light curve metrics to evaluate the most important metrics. We find that we can recover physical parameters to within 30% of their true values from ~18% of WFD light curves. Light curves with measurements of both the rise and decline in gri-bands, and those with at least fifty observations in all bands combined, are most information rich, with ~30% of these light curves having recoverable physical parameters to ~30% accuracy. WFD survey strategies which increase cadence in these bands and minimize seasonal gaps will maximize the number of scientifically useful SLSN light curves. Finally, although the DDFs will provide more densely sampled light curves, we expect only ~50 SLSNe with recoverable parameters in each field in the decade-long survey.

![lc recovery rate as function of number of points](/images/slsn_lsst/f5.png)
*Recovered parameter accuracy as a function function of number of observations*

So what's the bottom line? LSST is going to be a beast when it comes to discovering SLSNe, although only about 20% of the light curves will be useful on their own (assuming we know the redshift). The DFFs, in their current form, aren't going to help us a lot compared to the WFD. If the WFD survey could (1) occasionally observe between seasons or (2) stack late-time SLSN observations, we could extend the light curves of SLSNe, which would help us extract the most science without additional followup. 


{% if page.comments %}
<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = 'https://ashleyvillar-com.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
{% endif %}

