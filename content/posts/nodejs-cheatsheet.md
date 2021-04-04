---
title: "NodeJS Cheatsheet"
date: 2019-12-21T17:00:00+05:30
description: "NodejS cheatsheet conatins stuff related to nodejs that old and new devs may find helpful"
tags: [nodejs, javascript]
category: [Node, JavaScript]
---

This page contains nodejs related stuff to help you write better code or understand nodejs.

## Variable Assignment
```js
var john = {
  name: 'John Doe',
  email: 'john@example.com',
  age: 28
}

var { name, email, age } = john
```

## Promises

Promises are used for async code in node, it helps in avoid callback hell, let's start understanding promises.

### Async tasks without promises
```js
// Delay function
// Takes 2 argument: timeout, callback
// Calls callback function after timeout
function delay(seconds, callback) {
    setTimeout(callback, seconds*1000);
}

// Call delay function with 2 arguments
// A timeout and a closure
delay(1, () => {
    console.log('one second');
})

console.log('end first tick');
```

### Async functions with promises
```js
// Delay function is using promise now
// Promises are part of javascript
// Promse takes two argument
// resolve, this function will be called on success
// reject, this function will be called on error
var delay = (seconds) => new Promise((resolves, rejects) => {
    setTimeout(() => {
    	// This value be returned by promsie
        resolves('the long delay has ended')
    }, time);
});

// Then function will run after promise will resolve
// Catch will run on error
delay(1)
	// This will log 'the long delay has ended' since it was returned by promise
   .then(console.log)
   // This will return 42 to next then
   .then(() => 42)
   // This will print 'Hello world: 42'
   .then((number) => console.log('Hello world: ${number}'));
   // This will run on errors so it will never execute in this code
   .catch(() => {
   		console.error('something went wrong')
   })

// This line will execute in the last
console.log('end first tick');
```

### Parallel execution
```js
Promise.all([
	// These all tasks runs parallely with Promise.all
	// .then will run when all of the tasks will be completed
	task1(),
	task2(),
	task3()
]).then(res => {
	// do something
})
```

```js
Promise.race([
	// These all tasks runs parallely with Promise.all
	// .then will run when any of the tasks will be completed
	task1(),
	task2(),
	task3()
]).then(res => {
	// do something
})
```

