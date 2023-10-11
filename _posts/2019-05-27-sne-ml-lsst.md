---
layout: post
title:  PS1-MDS SNe Classification
date: 2019-05-27 09:56:00-0400
description: classification of ~3,000 supernovae
categories: research
tags: astronomy, research
giscus_comments: false
related_posts: false
related_publications: villar2019supernova
---


Today I'm going to write about a [new paper](https://iopscience.iop.org/article/10.3847/1538-4357/ab418c/meta) we recently submitted to the Astrophysical Journal. We present a machine learning pipeline trained using a set of spectroscopically identified supernovae found within Pan-STARRS Medium Deep Survey.

![sample slsn light curves](/images/jun2019/sne_all.png)

We currently discover around 10,000 supernovae per year. I illustrate this in the plot above, which uses the latest supernova (SNe) count from [sne.space](sne.space), to show number of SNe as a function of discovery year (on a logarithmic scale!). I’ve highlighted several wide-field surveys which have dominated the discovers in the past few years. Wide-field surveys (as opposed to galaxy-targeted surveys) like Pan-STARRS and ZTF have changed the game for discovering new extragalactic transients!

However, in several years, the Large Synoptic Survey Telescope (LSST) will come online and is expected to find nearly *one million* extragalactic transients, increasing our annual discovery rate by two orders of magnitude. This is a shift larger than anything we’ve seen in the past, opening a new era of data-driven time-domain astronomy! 

I like to think of this new era of as looking for "needles" in a haystack of events. Of the 1 million supernovae per year, and maybe tens of thousands of these will get spectroscopic classifications. Of these, maybe only 100 “interesting” needles will have multi-wavelength studies and receive the person-hours necessary to study them in real time. 

Searching for needles is an important problem, but I actually want to talk about the *haystack* in this blog post -- the millions of light curves without followup and maybe without spectroscopic classification. Our new paper specifically addresses the question: given a redshift and "complete" optical light curve, can we classify the light curves of supernovae as their spectroscopic class? 

To answer this question, we conducted a study using the Panstarrs Medium deep survey which ran from 2010-2014 over 70-square degrees. Previous [work](https://iopscience.iop.org/article/10.3847/1538-4357/aa767b/meta) by David Jones identified 5200 supernova-like transients in the survey, and followup efforts have allowed us to measure the host redshifts to 3100 objects. 518 objects had “high-confidence’ spectroscopic classification which we can use as SN “true labels” to train a classifier on the photometric light curves. So we want to train a machine learning algorithm to classify the 518 griz light curves into 5 supernova types: Types Ia, IIn, IIp, Ibc and superluminous. We don't actually publish the light curves in this work -- but we hope to do that soon!

We need to extract light curve features from our dataset to train our machine learning algorithm. In this case, we developed a new analytical model which better accounts for the plateau shape of Type IIP SNe while still being able to nicely fit other classes with smooth unimodal shapes. In the image below, I’m comparing our model to other similar models from Bazin and Karpenka. To be totally fair, however, we can't actually reproduce the 2nd bump that you often see in the redder bands of Type Ia SNe. This feature instead shows up as a plateau in our model.

![sample fits to our model](/images/jun2019/f1.png)

We fit each of the 518 LCs with a MCMC, using an iterative algorithm to tie all filters together. Here I am showing example fits, and you can see the more poorly-sample LCs, like the SLSN, have broader posteriors. This is important, because we can actually use the breadth of these fits to quantify the uncertainty of our classifier.

![example fits](/images/jun2019/f3.png)

We test a number of feature extraction techniques, data augmentation techniques, and classifiers. We find that PCA decomposition on our LCs along with a random forest classifier leads to best results. Below I show our our final confusion matrix, which tells you how well your photometric (machine-learned) labels match your spectroscopic labels. 

![confusion matrix](/images/jun2019/f2.png)


It turns out that we do pretty well! If compare several metrics to models which are (1) trained on simulated data or (2) trained to just do Ia-vs-nonIa classification, we do comparable in both cases. 

We're excited to expand on this project by fitting and classifying the remaining ~3000 SNe-like light curves. This summer, an REU student will be working on this project while we simultaneous create a totally independent way of doing this classification using neural networks!


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

