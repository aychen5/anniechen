---
layout: page
title:  Tips for Fielding Conjoint Experiments using Facebook Advertising (PART 2)
parent: Musings
mathjax: true
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

In [PART 1](https://aychen5.github.io//anniechen/posts/tips-for-fb-conjoints.html), we reviewed some of the ways to fashion conjoint experiments on Qualtrics. There is one more (optional, but recommended) step before we move on to survey circulation through Facebook.

## PART 2: Optimizing Conjoints for Mobile Devices

Making your web survey as mobile-friendly as possible allows you tap into a much larger pool of participants. Think -- external validity. This is particularly important if you plan on deploying the survey as Facebook ads. For an anecdotal example taken from my own experience, metrics from our survey targeting Nigerians in Ghana indicates that more than three quarters of Facebook users entered the survey through a mobile device.

Luckily, Qualtrics does most of the work for you. In general, Qualtrics automatically presents participants with a mobile-friendly version of your survey. There are even branching options that you can create in the Survey Flow specifically for participants on mobile. If you want to get fancy, it is also possible to "manually" manipulate the `CSS` such that you obtain the desired look for mobile devices. For example, using the `@media` rule. Check out [this](https://css-tricks.com/responsive-data-tables/) resource for more on creating responsive data tables.

```css
/* This is a striped table without an outer border */
table tr td {
  padding: 5px;
}
table td:last-child {
    border-right: none;
}
tr:nth-of-type(odd) { 
  background: #eee; 
}
/* Change the look for specific device */
@media only screen and (max-width: 600px) {
  table {
    padding: 2px; 
    ...
  }
}
```

Additionally, reducing the complexity of the experiment may be more critical on mobile devices than on desktop. There is some evidence to this effect (Couper, Antoun, and Mavletova (2017)). Yet, as researchers, our concern lies primary with data quality. The fear is that a design that becomes too minimal could fail to convey the appropriate information. Therefore, the aim is to elicit responses in a manner that preserves the integrity of the conjoint while also ensuring ___. Here are a few tips:
  
  - Minimize 


#### _Stay tuned for PART 3, which will detail survey distribution through Facebook Advertising._ 


