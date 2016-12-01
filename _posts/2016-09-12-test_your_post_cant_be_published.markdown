---
layout: post
title:  "Adding CSS To My First Sinatra App"
date:   2016-09-11 21:04:36 -0400
---

When I started building my own Sinatra web app, I didn't bother thinking the design of the. It did not seem important. Then when I saw other Sinatra web apps, I decided I must add CSS to my own app because I saw what a difference it made. 

At first, I thought it would be easy -  link the ERB file to the CSS file.  But whatever I would do, I could not get the ERB page to link to the CSS stylepage. I did not know what was wrong and so I made a quick Google search. 

I found a page on stackoverflow that said “by default Sinatra will allow CSS files to be accessed only if they are in a directory in the root of the app named public”. So, I created a public directory in the root of the app and moved the CSS stylesheet in to it. I was sure that now everything will run smoothly.  But CSS stylesheet was still not loading. So, I tried some different ideas, and then made another Google search.

After reading the Sinatra documentation I found the problem. The public directory name is not supposed to be included in the URL that is in the link tag in the ERB. I removed the public directory from the path and then the CSS loaded. 

I also learned that it is a good idea to use a direct path to the CSS file if you will be linking one stylesheet to many ERB files and they are at different levels in the path.

For the actual CSS I used, I found a site called [Web Design in 4 minutes](http://http://jgthms.com/web-design-in-4-minutes/#content) that saved me a lot of time. 
