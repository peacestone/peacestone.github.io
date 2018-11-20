---
layout: post
title:      "JavaScript Quirks"
date:       2018-11-18 21:14:39 -0500
permalink:  wierd_javascript_cases
---

Recently I attended a JavaScript meetup in Montreal and I learned about some interesting JavaScript quirks and decided to write about some of them.

**Template Literal Interpolation with an Object**
--------------------------------------------------

With template literals, we are able to interpolate expressions in our templates by using `${}` notation. An interesting case is that if we insert an object or array to interpolate the `.toString()` method is called on that item. In the code below we have an empty object literal that we are interpolating. The results are the same as if we were to call `.toString()` on it.

```js
const a = {}
a.toString();
// results ‘[object Object]’

`${{}}`
//results: '[object Object]'
```

What is important to remember when it comes to interpolation is that it is really a shorthand for calling the `toString()` method on that expression. An even weirder case is if we call `toString()` (or it's shorthand `${}`) on an array with null and undefined in it. The result is an array with nothing in it.

```js
`${[null,undefined]}`
//results: [,]
```

**Labels**
-------
Labels allow us to name a JavaScript block or loop in order to reference it in a `continue` or `break` statement. In the example below, I named the block of the if statement as fooLabel. I then am able to break out of the fooLabel block by using the `break` statement referencing the fooLabel block to break out of. That's why the second console.log doesn’t get executed.

```js
fooLabel:
    If (true) {
        console.log(‘started executing block’)
        Break fooLabel;
        console.log(‘this won’t be executed’)
    }
```

If we had a labeled block nested in another labeled block we can use the label to specify which block we would like to break or continue from. In the example below I wrote a nested for loop with labeled loops. I’m now able to specify which block I would like to continue on to:

```js
let variable = 'a let variable';
    barLoop:
        for(let i = 0; i < 3; i++){
            fooLoop:
                for(let j = 0; j < 3; j++){
                        continue barLoop
                        variable = 'this line will never be executed'
                }
            }
console.log(variable)
```

In general, labels aren't used in JavaScript code and [MDN’s page](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label) about labels has a note saying it is uncommon and usually a function could be returned to jump loops.

**ParseInt Function with a string of letters**
---------------------------------------------
I've used `parseInt` for converting strings with numbers to integers. What I didn't know is that if the radix is set above 10 (in the optional second argument), it will also consider letters to represent numbers from 10 and above. If the letter is out of range it will return NaN. If the letter that is out of range is together with a letter that is in range it will evaluate the first letter and ignore the letters out or range. Here are a few examples:

```js
parseInt('a', 16);
//results: 10

parseInt('b', 16);
//results: 11

parseInt('g', 16);
//results: NaN. The letter g is out of range for our set radix.

parseInt('foo', 16);
//results: 15. The letters oo our out of range and are ignored.
```

 If the radix were to be set to 25, the string foo would be converted to the number 9999. This is because the letter o now has meaning and represents the number 24.

```js
parseInt(‘foo’, 25);
//results: 9999
```

Neat!

I doubt I would ever write code this type of code but it's important to know in case you ever find it.
