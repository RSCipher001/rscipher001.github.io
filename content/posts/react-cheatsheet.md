---
title: "React Cheatsheet"
date: 2019-11-10T23:16:00+05:30
description: "React Cheatsheet"
tags: [react]
---

This is a under development kind of thing for react concept I have been learning.

### Create a new react app
We are going to use `npx`, it allows us to scaffold all required config files with one command, It comes pre-installed with `npm` 5.5 or later (Just use latest because I am not sure)

```bash
npx create-react-app react-training
cd react-training
code .			# Open project in VS Code
npm start		# Start React live server
```

### This is what we get.
![React first screen](/assets/images/in-post/react-cheatsheet/react-first-screen.webp)

Few points
- This is initial screen
- It uses react components
- All source code is available inside `src` directory

### There are so many files.
- `/node_modules` - Node modules, created by `npm/npx` command
- `public` - Contains compiled files, don't modify anything inside this directory for now.
- `src` - Contains source code, we will play with it.
	- `App.css` - A simple stylesheet.
	- `App.js` - A react component file.
		- Import statements are for importing other components and files (images, css, etc).
		- Every react component extends `React.Component` class, since it is imported in first line we write `class App extends Component` where `App` is component name in this case.
		- `render` function will return html which will be rendered.
		- `export default App`, it allows other files to import this file, App is our component name, if you use `class TodoListItem extends Component` then you have to write `export default TodoListItem`
	- `App.test.js` - I don't know/care.
	- `index.css` - Another CSS file.
	- `index.js` - This is our main JavaScript file, we will explore it later.
	- `logo.svg` - A logo in SVG format.
	- `serviceWorker` - A service worker works in the background and allows you web app to behave like native app, this is advanced level thing so don't touch it if you don't understand what is happening.

### Explore `App.js`
```js
import React from 'react';				// Import react from node_modules folder
import ReactDOM from 'react-dom';		
import './index.css';					// Import index.css from current folder
import App from './App';				// Import App.js from current folder, Importing js files doesn't require extension
import * as serviceWorker from './serviceWorker';	// Import everything from serviceWorker in current folder, It will import everything which is being exported for SW.

ReactDOM.render(<App />, document.getElementById('root'));	// Render App component, on #root element, in our index.html #root is a div.

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```


### Our initial app architecture
- index.html: It is importing index.js.
	- index.js: It is importing App component.
		- App.js: It is our only component for now.

### Let's create a todo app to understand more

A todo app is perfect example for learning any JavaScript frameworks, it helps us learning the following concepts.
- How to handle form input
- How to handle button clicks
- How to add elements dynamically
- How to remove elements dynamically
- How to handle events on dynamically created elements
- May be one or two nice concepts about framework.

### Steps
- We are going to create two new elements, `TodoList` and `TodoListItem`, it's like `ul` and `li`.


#### Create two new files `TodoList.js` & `TodoListItem.js`
```js
// TodoList.js
import React, { Component } from `react`

class TodoList extends Component {

}

export default TodoList;
```
