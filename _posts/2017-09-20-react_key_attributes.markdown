---
layout: post
title:  "React Key Attributes"
date:   2017-09-19 23:35:00 -0400
---

Anytime you transform an array to a list of components in React,  you need to add a key attribute to each item:

```
const names = ['Emma', 'Liam', 'Olivia', 'Noah']

const namesList = names.map((name, index) => <li key={index}>{name}</li> 

```

If you forget to add the key attribute, React will gently remind you with a warning message in the browser console. But why does React need a key attribute? 

It's about rebuilding the children a DOM node efficiently. React recurses over each child in the DOM node. If the child is the same as it was at its previous state, it will keep it. If the child is different from it's previous state, React will mutate the current child and all future children that have not yet been evaluated. For example lets say we have two children in a node:

```
<ul>
      <li>Emma</li>
			<li>Liam</li>
	</ul>

```

We then insert a third child to the beginning of the list:

```
<ul>
			<li>Olivia</li>
      <li>Emma</li>
			<li>Liam</li>
	</ul>
```

Since the first child has no longer the value of Emma, React will mutate all of the children in the node. This is inefficient, and can be problematic.

The reason all future children get mutated is because each child is not unique. Therefore, when comparing the previous and current trees, React can't figure out if a child was in previous state and only need to be reordered, or if it needs to be inserted into the parent node.

In our example, React can not know that `<li>Emma</li> <li>Liam</li>` were in the previous tree. Because`<li>Emma</li> <li>Liam</li>` are both not unique,  they may have been removed from the parent node and the  `<li>Emma</li> <li>Liam</li>` that are after after `<li>Olivia</li>`  are new children. 

When we add a unique identifier (key attribute) for each child, React is able to know by using the key attribute if  `<li>Emma</li> <li>Liam</li>` should be kept or destroyed:

```
<ul>
			<li key='3' >Olivia</li>
      <li key='1' >Emma</li>
			<li key='2' >Liam</li>
	</ul>
```


This all took me some time to comprehend. Now that I have my mind wrapped around this, I find it fascinating the amount of logic that goes behind deciding when to update a component, and I of course enjoy adding keys to lists of children. 

You can check out the React docs about keys by [clicking here](https://facebook.github.io/react/docs/reconciliation.html#recursing-on-children).


