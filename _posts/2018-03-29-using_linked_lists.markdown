---
layout: post
title:      "Using Linked Lists "
date:       2018-03-29 16:54:08 +0000
permalink:  using_linked_lists
---


One of the data structures I recently learned about is linked lists. Linked lists are a bunch of nodes that besides for containing its own data reference the next node in the list. We start off with the head node and move on to the next node using the head node. From the second node, we can access its own data and the next node in the list. This cycle continues until we reach a node that its next node points to null indicating that we have reached the end of the linked list. 

A JavaScript implementation of a linked list would look like this: 

```
class Node {
	constructor(data){
		this.data = data
		this.next = null
	}
	
	appendToTail(data) {
		let node = this
		while(node.next !== null){
			node = node.next
			console.log(node.data)
		}
		return node.next = new Node(data)
		
	}
}
```
An advantage of using a linked list is that we can insert or delete from the list in constant time(big O(1)). This is superior to arrays where Inserting or deleting elements in the middle of an array are big O(n). 

The reason for this is because arrays are essentially blocks of memory. Index 0 points to the first section of the memory block and index 1 points to the next section of memory. Every time we insert or delete an element in the middle of the array we must shift all the memory addresses in order to maintain order.

Now suppose we want to find the fourth or third (any number) element from the end of the linked list. Being that every node only knows its next node, finding this node can be tricky. 

There are multiple ways to solve this problem but the way that I was most fascinated by was through writing a recursive function. 

We write a function we can call nodeFromKthToLast that will take as an argument a node and a number specifying the offset from the end of the list. We then check to see if the passed in node is the end of the list. We do this by checking to see if the next property on the current node equals to null. If it does we return the number zero. If it does not, we get the current nodes offset from the end of the list by storing in a variable the return value nodeFromKthToLast function and then adding one to it. 

Then we check to see if the offset equals the offset number passed into our function. If it does we console.log it. We then finally return our offset number. 

Here is what an implementation of this looks like:

```
const nodeFromKthToLast = (linkedListHead, offset) => {
	let currentNode = linkedListHead
	if (currentNode.next === null){
		return 0
	}
	
	currentOffset = nodeFromKthToLast(currentNode.next, offset) + 1
	if(currentOffset === offset){
		console.log(currentNode)
	}
	
	return currentOffset
}
```


What I love about programming is learning about solutions that I would never come up with on my own. Recursion made me think about how the call stack works. Now that I understand it, I'm always trying to think about where else I use a recursive function. 


[Please feel free to reach out to me on Linkedin for any comments or questions about this post.
](https://www.linkedin.com/in/sholom-steinmetz/)
