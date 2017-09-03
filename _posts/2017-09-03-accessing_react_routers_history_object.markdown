---
layout: post
title:  "Accessing React Router's History Object"
date:   2017-09-03 11:35:34 -0400
---

On my recent react project, I had a child component that unfortunately did not have react routers history props passed down into it. I was able to solve this by importing  `withRouter`  from the `react-router` module, and exporting my component with the `withRouter` function. This  fuction takes an arguement of a componet and returns a [higher order component](https://facebook.github.io/react/docs/higher-order-components.html) that has react routers props passed down into it (much like the beloved `connect` function from Redux). Here is what my `withRouter` function looks like:

```export default withRouter(myAwesomeComponent)```

Then I was finaly able to push a new entry in to the history object. Awesome!  

