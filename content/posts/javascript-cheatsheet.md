---
title: "JavaScript Cheatsheet"
date: 2019-10-18T00:23:00+05:30
description: "Javascript cheat sheet contains most commonly used javascript functions and es6 & es7 features"
tags: [javascript]
---

This page contains some JavaScript functions I use regularly, if you want to test it while reading, you can use browser console or launch `node` in Terminal/Command prompt and paste that code to see the output

## ES6 Find


This section contains some examples of ES6 find.

### Find by value
Find a value in an array of integers. Returns first values in array that satisfied condition


```js
let numbers = [1, 4, 9, 16, 25];
let number = numbers.find(number => number > 10);

// Output: 16
```
---
```js
// About syntax for find will expand to
let number = numbers.find(number => {
    return number > 10;
});

// And above syntax will expand to
let number = numbers.find(function(number) => {
    return number > 10;
});
```

# Find by object property

Find a value in an array of objects. Returns first object in array that satisfied condition


```js
let persons = [
    { name: 'John Doe', age: 24 },
    { name: 'Jane Doe', age: 22 },
    { name: 'Alice', age: 32 },
    { name: 'Bob', age: 45 }
];

let person = persons.find( ({ name }) => name === 'John Doe' )

// Output: { name: 'John Doe', age: 24 }
```
---
```js
// About syntax for find will expand to
let person = persons.find(person => person.name == 'John Doe');
```

## References
<ul>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find" target="_blank" rel="noopener">MDN: Array.prototype.find()</a></li>
</ul>



JavaScript is awesome and confusing, There are many things about JavaScript that can be done in an easy ways and I am here to take notes about all of those.

# Arrow Functions

Arrow functions are great, They are shorter and can access calling context as this which makes it great for using it in promises. The following is a list of arrow functions and trandional function.

```js
// Traditional
function(x) {
	console.log(x);
}

// Arrow Function
x => {
	console.log(x);
}
```

```js
// Traditional
function(x) {
	return x * x;
}

// Arrow Function
x => x * x
```

```js
// Traditiona
function() {
	console.log("Hello")
}

// Arrow Function
() => {
	console.log("Hello");
}
```

```js
// Traditiona
function(a, b) {
	return a + b;
}

// Arrow Function
(a, b) => a +b;
```

# XHR Post in 3 lines (For Sending Data only)
```js
var formData = new FormData();
// ... add stuff to from data

// Actual XHR Code
var xhr = new XMLHttpRequest;
xhr.open('POST', 'https://example.com', true);
xhr.send(formData);
```

# JavaScript Array Filter
```js
// Return all the array with transaction_type debit
let array = this.objects.data.filter((object) => (object.transaction_type === "debit"))
```

# JavaScript Reduce
```js
// Calculate Amount in an array (array is a JS Array)
array.reduce((accumulator, currentValue) => {
    return accumulator + parseInt(currentValue.amount);
}, 0)
```

### Prevent Form Submit on Enter (jQuery)
```javascript
$(document).keypress(function(e){
    // Get keycode
    var keyCode = e.keyCode || e.which;

    // If keycode is 13 prevent event
    if (keyCode == '13') {
        e.preventDefault();
    }
});
```