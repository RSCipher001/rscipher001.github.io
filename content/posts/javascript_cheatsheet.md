+++
categories = ["javascript"]
date = "2021-04-04"
description = "JavaScript Cheatsheet"
title = "JavaScript Cheatsheet"
+++

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