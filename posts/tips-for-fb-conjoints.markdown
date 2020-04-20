---
layout: page
title:  Tips for Fielding Conjoint Experiments using Facebook Advertising (PART 1)
parent: Musings
mathjax: true
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
 
The process of fielding a web survey can be roughly split into two distinct components: using the service that hosts the survey and deployment of your survey on a distrbution platform. With many services (like Qualtrics), there often exists an option to combine these steps, so that you may be minimally concerned about the sampling process. This guide specifically tackles the practical implementation of conjoint experiments on Qualtrics, disseminated through Facebook advertisements.
 
 
## PART 1: Constructing Conjoints Surveys
 
### i) Set-up in Qualtrics

There are a few of ways of doing this. The option that works for you depends on the resources available at your disposal, the amount of time you're willing to dedicate to the project, your familiarity with web-languages (i.e. `Javascript`, `HTML`, `PHP`, etc.), and how flexible you are with the design. I present them in order of decreasing $$$, though the approach most suitable for your purposes might not prioritize this factor. 
 
 - [Qualtrics' Product Experience package](https://www.qualtrics.com/marketplace/conjoint-package-analysis/): _"I'm rolling in the big bucks"_
 
   + Full disclosure: I have no experience using this service. This is Qualtrics' built-in product for conjoints; it is the expertly-design, albeit, pricey option. If your institution has the money to spare and you're looking to an easy-to-use tool, then this could be the way to go.
   
   
 - [Anton Strezhnev's Conjoint Survey Design Tool](https://github.com/astrezhnev/conjointsdt): _"Let's not break the bank (server-side method)"_ 
 
    + A popular option among many political scientists is to use this software written by Strezhnev and company, Conjoint SDT. It's an open-source tool that has a straight-forward installation and design interface. It relies on a simple Python script (the authors have recently ported the Python 2 code to Python 3), which outputs a `PHP` file. The catch is that the `PHP` needs to be hosted on a web server that can then be directly integrated into the Survey Flow of your Qualtrics survey. This requires some basic knowledge of web development, including purchasing a domain, a web hosting plaform, and navigating web hosting management software like cPanel. 
    
    + As you might have noticed, this is not an entirely costless operation (both in terms of price and time). Granted, the price is peanuts compared to using the Qualtrics product. I should also mention that the process of setting up a web server itself can be more or less complicated depending on what you can afford. For instance, buying a domain from a separate company (say, GoDaddy) from your web host entails connecting the domain to the host server (say, Interserver; see changing NameServers [here](https://www.interserver.net/tips/kb/change-nameservers-godaddy/)). This is can be considerably more involved (especially if this is new to you -- as it was for me) than simply purchasing both from the same source. The tradeoff is price, though not by much if you shop around. Web hosting services usually go for something like US$ 5.00 monthly, or slightly discounted if you opt for an annual subscription.  
 
 - [Thomas Leeper's Javascript-based solution](https://github.com/leeper/conjoint-example): _"Let's not break the bank (client-side method)"_
 
   + An alternative to the above, and my preferred option, is to insert custom Javascript directly into Qualtrics. Essentially, you create an empty `HTML` table in the body of the survey question, and let the `Javascript` do the randomization behind the scenes to fill in the table. Leeper provides an excellent guide and code to do this with ease. I see a few advantages of this approach. First, the learning curve to implementing server-side solutions (option #2) can be steep, particularly if you have to learn how to use multiple softwares (and how they work in tandem) at once (all to accomplish a relatively simple task). While Leeper's approach necessitates some coding in `Javascript` and `HTML`, it is minimal, as the template provides all the structural components and customization is only a matter of "filling in the blanks" (adapting the attributes for your inquiry). The decision to adopt this client-side solution (meaning, it executes on the browser) or the server-side solution could depend, in part, on your familiarity with either scripting language (`Javascript` vs `PHP`), which directly influences your ability to customize the conjoint design. Nevertheless, a client-side fix is attractive because you don't have to deal with the overhead of web server maintenance. Additionally, one can presumably mobilize Node.js to reap server-side benefits using JS code -- but that's beyond my paygrade. 
   
   + Leeper's instructions are fairly extensive, so I leave the basic implementation to him. However, I will mention a couple additional tips that are not addressed by Leeper.
 
 - [Shiny Application](https://medium.com/@joyplumeri/using-r-shiny-to-create-web-surveys-display-instant-feedback-and-store-data-on-google-drive-68f46eea0f8b): _"Flat broke, but rich in time"_
 
   + Okay, so I include this option just to say that it is feasible. I've linked a more generic guide on creating and hosting surveys using a Shiny app (not a conjoint), and then storing responses on Google Drive. Perhaps not ideal for academic research (for security reasons), and usurps more time and effort than you'd like, but maybe worth exploring if you'd like to develop a new skill. 

 
 
### ii) Optimizing conjoints for mobile devices

Luckily, Qualtrics does most of the work for you. In general, Qualtrics automatically presents participants with a mobile-friendly version of your survey. There are even branching options that you can create in the Survey Flow specifically for participants on mobile.    


##### _Stay tuned for PART 2, which will detail survey distribution through Facebook Advertising._ 
 
{% comment %}
### II. Facebook Targeted Advertising
 
 
 
 - One word of caution: a challenge of relying on a social media platform is that researchers are at the mercy of its everchanging advertising guidelines, procedures, and algorithmic delivery system. 
 
 - There already exist a few resources that detail the process:
 
  
#### Cost 

{% endcomment %}