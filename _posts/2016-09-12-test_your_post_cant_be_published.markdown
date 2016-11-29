---
layout: post
title:  "Adding CSS To My First Sinatra App"
date:   2016-09-11 21:04:36 -0400
---

When I started building my own Sinatra web app, I didn't bother thinking about how the format and design of the page would be. It just was not important. But when I saw other Sinatra web apps, I decided I must add CSS to my own app because I realized how much more pleasant a designed web app is. 

At first I thought it would be easy -  link the CSS file to the ERB file. Turns out, that I hadn't read the documentation on were exactly the CSS file belongs, and that got me in to some trouble. 

Whatever I would try to do, I could not get the CSS stylepage to link to my ERB page. I did not know what was wrong.  That's when I decided to make a Google search. 

I Googled `sinatra CSS` and I found a page on stackoverflow that said that by default Sinatra will allow CSS files to be accessed only if they are in a dirctory in the root of the app named public. When I read this, I created a public directory in the root of the app and moved the CSS stylesheet in to it. I was sure that now everything will run smoothly, and I will finally have a gorgeous web application.  But I still was in trouble. The CSS stylesheet was not loading. So I tried some different ideas, and then made a Google search.

After a few minutes, I found out that there was an issue with the way I was requiring the stylesheet in the link tag of my ERB file. Even though the stylesheet is inside a directory name public, when you require that stylesheet at the at the link tag of the ERB file, you do not add to the href atribute a direct path that includes the public directory.  Instead, you need to ommit the public directory altogether. So I went to the link tag in my ERB file, and by the href attribute, I changed it to: `href="/style.css"` making sure to skip the public directory. 

Finally my web app was loading the CSS Stylesheet and it looked awesome.

For the actual fun part of cutomizing the page with CSS, I found a site called [Web Design in 4 minutes](http://http://jgthms.com/web-design-in-4-minutes/#content) that saved me a lot of time. 
