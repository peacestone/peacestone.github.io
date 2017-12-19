---
layout: post
title:      "onOutsideClick Events with React"
date:       2017-12-19 01:15:22 +0000
permalink:  onoutsideclick_events_with_react
---


A recent feature I added to my react app was a popup panel that would appear when the user clicks on a button in the menu bar and would disappear when the user clicks outside of the popup panel.

To implement this feature I added a ref attribute to the panel element with a callback function. The callback function gets passed in as an arguement the underlying DOM element that contains the popup panel. It then stores that element as this.popupNode which will be used for the logic in the event handlers:


```   
 setWrapperRef = (node) => this.popupNode = node

render() {
 return(

      <div id='whereWeFlyPopupPanel'  ref={this.setWrapperRef}  >
      <ul>
        {airportCityList}
      </ul>
      </div>

    )
}
```

Immediately after the component mounts, an onMouseDown event listener is added on the document node and it gets removed when the component unmounts:

```
componentDidMount = () => {
    this.props.getAirports()
    document.addEventListener('mousedown', this.handleOutsideClick)
  }

  componentWillUnmount = () => {
    document.addEventListener('mousedown', this.handleOutsideClick)
  }
```


The mouseDown event listener triggers a function that determines from which node the event was triggered. 

If the triggering node is not a descendant of the popup panel node, then we know that the click event was outside of the popup and we should deactivate the popup panel. And if the node is a descendant of the panel node, then we know the click event transpired inside the popup and we should do nothing. 

To evaluate if a node is a descendant of another node we use the node.contains method which returns a boolean. In our case we use this.popupNode.contains(eventNode) to see if the click event happened inside the popup panel node:


```

handleOutsideClick = (event) => {
    if(this.popupNode && !this.popupNode.contains(event.target)  ){
      this.props.toggleOffPannel()
    }
  }

```



[Click here to checkout the apps github repo to see it in action.
](https://github.com/peacestone/juillet_airways_client/blob/master/src/containers/whereWeFly.js)






