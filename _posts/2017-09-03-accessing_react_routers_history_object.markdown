---
layout: post
title:  "Accessing React Router's History Object"
date:   2017-09-03 15:35:33 +0000
---


On my recent react project, I had a component that did have react routers history props passed in to it. I was able to get those props passed down to the component by  importing  `withRouter`   from `react-router` and exporting my component with `withRouter` taking my component as an argument.

```export default withRouter(myAwesomeComponent)```

