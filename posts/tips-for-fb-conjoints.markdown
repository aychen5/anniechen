---
layout: page
title:  Tips for Fielding Conjoint Experiments using Facebook Advertising (PART 1)
parent: Musings
mathjax: true
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
 
The process of fielding a web survey can be split into two distinct components: using the service that hosts the survey and deployment of your survey on a distrbution platform. With many services (like Qualtrics), there often exists an option to combine these steps, so that you may be minimally concerned about the sampling process. This guide specifically tackles the practical implementation of conjoint experiments on Qualtrics disseminated through Facebook advertisements. 

If you are reading this, I assume you have some knowledge of the aims of conjoint analysis, have deemed that this design is appropriate for your research goals, and seek the means to carry it out. I also assume that you have a working knowledge of Qualtrics. 

Obligatory caveat: I am by no means an expert in web development. These tips are derived from my experience figuring out how to do this, and may not reflect the most efficient modes of implementation.
 
 
## PART 1: Building Conjoints Surveys in Qualtrics
 
### i) The options 

There are a few of ways of doing this. The option that works for you depends on the resources available at your disposal, the amount of time you're willing to dedicate to the project, your familiarity with web-languages (i.e. `Javascript`, `HTML`, `PHP`, etc.), and how flexible you are with the design. I present them in order of decreasing $$$, though the approach most suitable for your purposes might not prioritize this factor. 
 
 - [Qualtrics' Product Experience package](https://www.qualtrics.com/marketplace/conjoint-package-analysis/): _"I'm rolling in the big bucks"_
 
   + Full disclosure -- I have no experience using this service. This is Qualtrics' built-in product for conjoints; it is the expertly-design, albeit, pricey option. If your institution has the money to spare and you're looking to an easy-to-use tool, then this could be the way to go.

<br>
   
 - [Anton Strezhnev's Conjoint Survey Design Tool](https://github.com/astrezhnev/conjointsdt): _"Let's not break the bank (server-side method)"_ 
 
    + A popular option among many political scientists is to use this software written by Strezhnev and company, Conjoint SDT. It's an open-source tool that has a straight-forward installation and design interface. It relies on a simple Python script (the authors have recently ported the Python 2 code to Python 3), which outputs a `PHP` file. The catch is that the `PHP` needs to be hosted on a web server that can then be directly integrated into the Survey Flow of your Qualtrics survey. This requires some basic knowledge of web development, including purchasing a domain, a web hosting plaform, and navigating web hosting management software like cPanel. 
    
    + As you might have noticed, this is not an entirely costless operation (both in terms of price and time). Granted, the price is peanuts compared to using the Qualtrics product. I should also mention that the process of setting up a web server itself can be more or less complicated depending on what you can afford. For instance, buying a domain from a separate company (say, GoDaddy) from your web host entails connecting the domain to the host server (say, Interserver; see changing NameServers [here](https://www.interserver.net/tips/kb/change-nameservers-godaddy/)). This is can be considerably more involved (especially if this is new to you -- as it was for me) than simply purchasing both from the same source. The tradeoff is price, though not by much if you shop around. Web hosting services usually go for something like US$ 5.00 monthly, or slightly discounted if you opt for an annual subscription.  
 
 - [Thomas Leeper's Javascript-based solution](https://github.com/leeper/conjoint-example): _"Let's not break the bank (client-side method)"_
 
   + An alternative to the above, and my preferred option, is to insert custom Javascript directly into Qualtrics. Essentially, you create an empty `HTML` table in the body of the survey question, and let the `Javascript` do the randomization behind the scenes to fill in the table. Leeper provides an excellent guide and code to do this with ease. I see a few advantages of this approach. First, the learning curve to implementing server-side solutions (option #2) can be steep, particularly if you have to learn how to use multiple softwares (and how they work in tandem) at once (all to accomplish a relatively simple task). While Leeper's approach necessitates some coding in `Javascript` and `HTML`, it is minimal, as the template provides all the structural components and customization is only a matter of "filling in the blanks" (adapting the attributes for your inquiry). The decision to adopt this client-side solution (meaning, it executes on the browser) or the server-side solution could depend, in part, on your familiarity with either scripting language (`Javascript` vs `PHP`), which directly influences your ability to customize the conjoint design. Nevertheless, a client-side fix is attractive because you don't have to deal with the overhead of web server maintenance. Additionally, one can presumably mobilize Node.js to reap server-side benefits using JS code -- but that's beyond my paygrade. 
   
   + Leeper's instructions are fairly extensive (which borrows from Kyle Dropp's guide), so I leave the basic implementation to him. However, I will mention a couple additional tips that are not addressed by Leeper.
  
      * The first is randomizing the order of the attributes. The code snippet below is adapted from Dropp's solution. Here, I have an array of 4 attributes (Family, Occupation, Ethnicity and Religion) and an empty array of length equal to the number of attributes. We then loop through and populate the empty array with randomly drawn attributes. 
      
```js
Qualtrics.SurveyEngine.addOnload(function()
{
// These are the attributes
var attRaw = ["Family", "Occupation", "Ethnicity", "Religion"];
var att = ["Family", "Occupation", "Ethnicity", "Religion"];
var attributes = ["","","",""];

// Randomize the order of the attributes
for (i=0; i < attRaw.length; i++) {
  var random1 = Math.floor(Math.random()*((attRaw.length-i)-0));
  attributes[i] = att[random1];
  att.splice(random1,1);
}
});
```
      
      
  * Sometimes, researchers would like to keep elements constant within subject, but allow them to vary across subjects. In the context of conjoint analysis, this means retaining the order of attributes across tasks for each respondent, while randomizing the order that they are presented per survey. To accomplish this, we can create an embedded data variable that captures the order, then pipe this variable into subsequent tasks. Say, your experiment consists of 2 conjoint tasks. In the first task, it is business as usual. Copy and paste the code above into the addOnload segment of the JS (in addition to the rest of the conjoint code). Then, two commands are key: `setEmbeddedData()` and `getEmbeddedData()`. I create a new variable, `attrorder` that saves the order from the first task like so: 
  
      
```js
// Store values as embedded data fields
Qualtrics.SurveyEngine.setEmbeddedData('attrorder', attributes); 
```
  
     
  * Then, in the second task on the next survey page, you can omit the re-randomization of attributes and grab the order variable you created in the previous step. Note that this will not work unless the tasks are on separate pages, because the JS is executed and updated by page. Also, a friendly reminder that you also need to declare the embedded data variable in your Survey Flow (leaving the value empty).
  
     
```js
// Attribute order from previous conjoint task
var attributes = Qualtrics.SurveyEngine.getEmbeddedData('attrorder');
```     
 
 - [Shiny Application](https://medium.com/@joyplumeri/using-r-shiny-to-create-web-surveys-display-instant-feedback-and-store-data-on-google-drive-68f46eea0f8b): _"Flat broke, but I got time"_
 
   + Okay, so I include this option just to say that it is feasible. I've linked a more generic guide on creating and hosting surveys using a Shiny app (not a conjoint), and then storing responses on Google Drive. Perhaps not ideal for academic research (for security reasons), and usurps more time and effort than you'd like, but maybe worth exploring if you'd like to develop a new skill. 

 
 
### ii) Optimizing conjoints for mobile devices

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



### iii) Additional remarks




##### _Stay tuned for PART 2, which will detail survey distribution through Facebook Advertising._ 
 
{% comment %}
### II. Facebook Targeted Advertising
 
 
 
 - One word of caution: a challenge of relying on a social media platform is that researchers are at the mercy of its everchanging advertising guidelines, procedures, and algorithmic delivery system. 
 
 - There already exist a few resources that detail the process:
 
  
#### Cost 

{% endcomment %}