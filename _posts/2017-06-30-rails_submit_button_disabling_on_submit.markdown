---
layout: post
title:  "Rails Submit Button Disabling on Submit"
date:   2017-06-30 18:32:46 +0000
---


By default, a rails form submit button will disable on submit. This is a great feature for preventing multiple of the same resources being created. But that is not always what is wanted. I was creating a form to create resources through a jquery ajax request and then have the response rendered without a page refresh. I wanted this to happen multiple times  and disabling the submit button on submit was exactly what I did not want to happen. I addded the follwing line of code to my submit button:

`data: { disable_with: false }`

And that's how I disabled the unobtrusive Java Script. 

