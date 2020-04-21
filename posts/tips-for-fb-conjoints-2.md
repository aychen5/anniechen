---
layout: page
title:  Tips for Fielding Conjoint Experiments using Facebook Advertising (PART 2)
parent: Musings
mathjax: true
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

In [PART 1](https://aychen5.github.io//anniechen/posts/tips-for-fb-conjoints.html), we reviewed some of the ways to fashion conjoint experiments on Qualtrics. There is one more (optional, but recommended) step before we move on to survey circulation through Facebook -- designing conjoints for mobile distribution. 

But first, an bligatory caveat, which should go without saying, but in case you skipped PART 1: I am not an app developer.

## PART 2: Optimizing Conjoints for Mobile Devices

Making your web survey as mobile-friendly as possible allows you tap into a much larger pool of participants. Think -- external validity. This seems particularly important if you plan on deploying the survey as Facebook ads (more on this in PART 3). For an anecdotal example taken from my own experience, metrics from our survey targeting Nigerians in Ghana indicates that more than three quarters of Facebook users entered the survey through a mobile device.

Luckily, Qualtrics does most of the work for you. Qualtrics will generally present participants with a mobile-friendly version of your survey automatically. There are branching options that you can create in the Survey Flow specifically for participants on mobile. If you want to get fancy, it is also possible to "manually" manipulate the `CSS` such that you obtain the desired look for mobile devices. For example, using the `@media` rule in the code chunk below. Check out [this](https://css-tricks.com/responsive-data-tables/) post for more on creating responsive data tables.

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

Additionally, reducing the complexity of the experiment may be more critical on mobile devices than on desktop. For example, smartphone users tend to skip more questions and take longer to reach survey completion ([Tourangeau et al. (2017)](https://academic-oup-com.proxy3.library.mcgill.ca/poq/article/81/4/896/4718546) provides a good summary). Also see [Couper, Antoun, and Mavletova (2017)](https://onlinelibrary.wiley.com/doi/10.1002/9781119041702.ch7)). Yet, as researchers, our concern lies primarily with data quality. The good news is that the literature suggests there is little to be concerned about regarding data quality from smartphone vs desktop participants ([Tourangeau et al. (2017)](https://academic-oup-com.proxy3.library.mcgill.ca/poq/article/81/4/896/4718546); [Antoun, Couper, and Conrad (2017)](https://academic.oup.com/poq/article-abstract/81/S1/280/3091905?redirectedFrom=fulltext)). The fear is that a design that becomes too minimal might fail to convey the appropriate information. Therefore, the aim is to elicit responses in a manner that preserves the integrity of the conjoint while also ensuring that the conjoint is sufficiently simple in order to maximize number of responses. As it will become evident in my list of tips, there are some research inquiries that are simply not suitable for mobile adaptation.  

  1. Reduce length of attribute descriptions. Ditto for descriptors of the levels within each attribute item.
  
  2. Minimize the number of attributes tested. Together, the goal of number 1. and 2. is to limit the amount of scrolling necessary to access all the information required to answer questions.
  
  3. Take advantage of Qualtrics' ["request response" feature](https://www.qualtrics.com/support/survey-platform/survey-module/editing-questions/validation/#RequestResponse). If there is some unavoidable degree of scrolling involved, consider accompanying the question(s) with a reminder validating empty responses (a pop-up when Qualtrics detects unanswered questions). It has been shown that response-order effects are more substantial in smartphone-collected data, partly due to the scrolling issue. Validation is one way of combatting that.
  
  4. Incorporate imagery. This does not have to take the form of pictures embedded in profiles themselves. Instead, you might add a photo to the vignette introducing the conjoint experiment. 
  
  5. Implement a forced-choice conjoint. In a related vein, consider sticking with the dual-profile design. A significant departure from tasks with 2 profiles risks greater cognitive taxation.

All these points speak to what [Tourangeau et al. (2017)](https://academic-oup-com.proxy3.library.mcgill.ca/poq/article/81/4/896/4718546) call "visual prominence -- the idea that respondents are more likely to notice and consider information that is easy to see." While these aren't hard and fast rules, it's implicit that, taken together, a 10-attribute, 10-task, 4-profile rating-based conjoint -- that's (\\(10 \times 10 \times 4 \times 8 = 3,200\\)) observations _per respondent_ -- is probably not a good idea. The rule-of-thumb, then, is that with increasing design complexity (i.e., more profiles, more tasks), XXX

### Sources:

[Antoun, Couper, and Conrad (2017)](https://academic.oup.com/poq/article-abstract/81/S1/280/3091905?redirectedFrom=fulltext)

[Mick P. Couper  Christopher Antoun  Aigul Mavletova. 2017.](https://onlinelibrary.wiley.com/doi/10.1002/9781119041702.ch7)] Mobile Web Surveys: A Total Survey Error Perspective. _Total Survey Error in Practice, Chapter 7._

[Tourangeau et al. (2017)](https://academic-oup-com.proxy3.library.mcgill.ca/poq/article/81/4/896/4718546) Web Surveys by Smartphone and Tablets: Effects on Survey Responses. _Public Opinion Quarterly._

#### _Articles are gated. Sorry!_

<br>

#### _Stay tuned for [PART 3](https://aychen5.github.io//anniechen/posts/tips-for-fb-conjoints-3.html), which will detail survey distribution through Facebook Advertising._ 


