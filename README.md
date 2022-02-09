# FrontEnd

## Micro-Frontends

Independent Deployments
Less Interdependency

Mosaic9, Single-SPA, Piral or Module Federation in webpack 5.

### Module Federation in Webpack 5

Module federation allows a Javascript application to dynamically load code from another applications and in the process, share dependencies.

An application has libraries(react, redux,material-ui), store, components. \
Need: Share components betwwen different applications/projects. \
Other solutions: As a library and import as package in both projects. \
Dynamic import: Component stay in one project. Externalize it so that another application can use it. \
Assume 3 applications home,search and nav(shared header)
In webpack.config.js of home. We are exposing carousel and importing nav.
```
  new ModuleFederationPlugin({
    name: 'home,
    filename: 'remoteEntry.js'
    remotes: { nav: 'nav' },
    exposes: { carousel: 'src/carousel'},
    shared: ['react','react-dom','@material-ui/core']
    })
 ```
 To bring header from nav in home, in index,html of home we import remoteEntry.js of nav project. And in App.js import Header and use.
 ```
  <script src="http://localhost:3003/remoteEntry.js" ></script>     //Nav project is running on port 3003
  ```
  
  Angular vs React vs Next
  
  React: Is a library \
  Next: Is a framework \
 
Both develop components.
Angular is a Framework
React is a library.(View and Syncing the View). For other functionalties like routing, calling http service we need to use other librares. 

  
  ### React

- components **react** to state and props change
- The basic theory in React is that a piece of UI can "react" in response to state changes.


Components - Nav Bar,Profile, Feed, Tweet, Like
Root Component(App)
Child Components
Tree of comopnents

Component
- Java Class with state and render

class Tweet {
 state = {};
 render () {
 }
}


state - data to be displayed
render - ui

React keeps light weight DOM in memory which is called Virtual DOM(React Element).
DOM in memory
Cheap to create


No need to write code to manipulate the dom or attch event handlers to DOM.
Do state changes in React. React will automatically update the DOM.
React - Reacts to state changes and update the DOM.

NodeJs is a JavaScript runtime built on Chrome's V8 Javascript engine.

Node Package Manager - 

npm i -g create-react-app

npx create-react-app my-app
cd my-app
npm start

Simple React Snippets
Prettier - Code Formatter


create-react-app react-app
	Development Server
	Webpack for bundling files
	Babel compiling js code
cd react-app
run npm
localhost:3000

node_modules - react libraries and third party libraries

index.html
- Container for React Application

src/App.js

Object oriented programming in javaScript - Mosh
JavaScript Tutorials for React Developers

JSX - JavaScript XML

class App extends Component {
	render(){
		return (
			<div></div>
		);
	}
	
}

Bable will take this JSX sytax and convert to javascript that browser can understand.

bablejs/io

const element = <h1>Hello World</h1> 
convert this to React code.
var element = React.createElement("h1", null, "Hello World");--Plain React Code

Components
always use Jsx
Babel will conver to React code.

index.js - Entry point for application
<div id=root />

ES6 modules


import modules
u should import React module ( Needed for bable to convery JSX to React )
So even if u are not using it, It should be imported.

import ReactDOM

react.element - virtual dom
ReactDOM.render(element, document.getElementByid('root')) -- Will render inside index.html . 


For complex applications react.element will be components.


-----------------------------------------------------------

Bootstrap - CSS 
npm install bootstrap

index.js
import bootstrap.css


components folder
counterComponents.jsx


shortcuts - imrc
cc

class CounterComponent extends Component
export default CounterComponent; 

or

export default class Counter extends Component {}

index.js

import CounterComponent from ./components/counter

ReactDOM.render(<App />, document.getElementByid('root')) 
ReactDOM.render(<Counter />, document.getElementByid('root')) 

-----------------------------------------------------------------

Embedding Expressions

return ();

When javascript sees return <empty> it adds a ; and return. Will not execute after that.

<React.Fragment> instead of <div>

state = {}; //any data that component needs.

state = {
   count: 0,
   address: {"city":""	},
   imageUrl : ''
}

{this.state.count}


formatCount() {
 return this.state.count === 0 ? 'Zero' : this.state.count;
}

formatCount() {
 const { count } = this.state;
 return count === 0 ? 'Zero' : count;
}

formatCount() {
 const { count } = this.state;
 return count === 0 ? <h1>Zero</h1> : count;
}

{this.formatCount()}


JSX can be returned from a function.

---------------------------------------------

Setting Attributes

<img src={this.state.imageUrl} />

to apply class

<span className="badge badge-primary m-2">{this.formatCount()}</span> //from bootstrap css

Applying styles

styles= {
  fontWeight: 10,
  fontSize: 10
}

<span style={this.styles}>

define property and refer it

<span style={{ fontSize: 10 }}>  inline styling

1. Bootsrap using className
2. Defne property and refer it
3. Inline
4. Dynamic Styliing

render () {
  let classes = "class1";
  classes += (this.state.cout ===0) ? "class2" : "class3";
  
  return(){}

}

<span className={classes}>{this.formatCount()}</span>

---------------------------

Rendering Lists
define tags in state

<ul>
  { this.stage.tags.map( tag => <li key={tag}>{tag}</li>) }
</ul>

Conditional

There is no if and else in JSX. Angular supports if else. JSX is not a template engine. U need to use plain java scrit.

if(this.state.length === 0)
 return <p>No Items Selected</p>
else
 return <ul>... </ul>


return (<div>
 { exp1 && "SomeString"}
 </div>

);


JS

true && 'Hi'
'Hi'
------------------------------

Handling Events

<button onClick={this.handleIncrement} />

All DOM events

handleIncrement() {
  console.log(this);
}


"this" in JS can refer to different objects
depending on how a function is called
obj.method(); //this refers to obj
function(); //this refers to reference to window object. Strict mode undefined.

constructor () {
  super();
  this --- Counter Object 
  this.handleIncrement.bind(this); -- will return a new instance of handleIncrement function with "this" referencing to current Counter object. Always. Never change. 
}


to bind event handlers with "this" - using bind

Another Solution

convert into an arrow function. Arro function inherit "this"

handleIncrement = () => {
}

--------------------------------------------------------

this.setState() --- to say React that state is changed. Angular automatically detects changes.
All browser events are notified. In react we need to explicitly say state is changed.
Override the properties or merge the properties on calling setState().

React compare Virtual DOM with real dom. And update the span.

-----------------------------------------------------------

onClick={this.handleIncrement) -- to pass parameters

handleIncrement = product => {
}

dohandleIncrement = () => {
   this.handleIncrement ( {id:1 });
}

onClick={this.dohandleIncrement)

or 

onClick={() => {
   this.handleIncrement ( product);
})
------------------------------

Composing Components

counter.jsx
counters.jsx
index.jsx - render Counters. ReactDOM.render(<Counters>)

------------------------------

Passig values to components

Every React compenent has a property called "props". Includes all attributes we set in Counter component.

<Counter key="" value="" selected >

this.props  --- value and selected. Key wont be a part.



Passing Children
special prop called children
To pass complex properties to components child.


React Developer Tools.

State vs Prop

State: Internal to component. Local state of a component.
Prob : Input to components. Read only. React doesnt allow to change the property of a component.

--------------------------Pass data parent to child-----------------------------------------
https://www.freecodecamp.org/news/pass-data-between-components-in-react/

- USING this.props

----- Child ---------

import React,{Component} from 'react'

export default function Child({parentToChildProperty}){
	return(<div>{parentToChildProperty}</div>);
}

export class Child expends Component{
	render(){
		return (
			<div>{this.props.parentToChildProperty}
		)
	}
}

-------Parent--------

import React from 'react'
import Child from './Child'

export default function Parent(){

const data = '';
const parentTochild = () => {
	data = "Hi from Parent";
}
	return(
		<div>
		<Child parentToChildProperty={data}/>
		<Button onClick = {() => parentTochild()}>Click me </Button>
		</div>);
}
--------------------------Pass data from child to parent-----------------------------------------

- SET A FUNCTION AS PROPERTY.PASS FUNCTION TO CHILD. CHILD invokes FUNCTION WITH DATA.FUNCTION SET DATA TO PARENT FUNCTION.

----- Child ---------

import React,{Component} from 'react'

export default function Child({parentToChildFn}){
	const data =" This is from Child"
	return(<div><Button onClick = {() => parentToChildFn(data)}>Click me </Button></div>);
}

export class Child expends Component{
	render(){
		return(<div><Button onClick = {() => this.props.parentToChildFn(data)}>Click me </Button></div>);
	}
}
-------Parent--------

import React from 'react'
import Child from './Child'

export default function Parent(){

const data = '';
const parentTochild = (childData) => {
	setData(childData);
}
	return(
		<div>
		<Child parentToChildFn={parentTochild}/>		
		</div>);
}

export default class Parent extends Component{

const data = '';
const parentToChild = (childData) => {
	setData(childData);  or this.setState({data:childData});
}

render () {
	return( <div>
		<Child parentToChildFn={this.parentTochild.bind(this)}/>	
	</div>)
	}
}

----------Pass value between other components----------------
child to child
	- Parent - define function
			Child1 pass function as property
			Child2 pass this.state.data as a property to child

------------------------------------ES6------------------------------------https://www.youtube.com/watch?v=NCwa_xi0Uuc

let/const
--------
	var - var declared in a block is accessible inside the function it is defined. scoped to function
	let - only accessible inside that block. scoped to block. New keyword in ES6
        const - scoped to block. New keyword in ES6. cannot be reassigned.
objects
--------
Key value pair. Contains fields and methods. Methods can skip () and function key word.
person = { 
	name : "Lakshmi",
	talk : function () { console.log(this);},
	walk () { }
} 

this
-----

1. person.talk(); //this refers to person
2. const newTalk = person.talk; newTalk() // this refers to windows obeject. In strict mode this refers to undefined.
3. In newTalk(), "this" is not referencing to person object. We can bind newTalk() with person object using bind methos.
	In javascript functions are objects.It got properties and methods eg. Bind
	bind - first parameter - determine value of this. //sets the value of "this"
	So when we do const newTalk = person.talk.bind(person); newTalk(); 
	Now in newTalk(), "this" is referencing to person object.
		

strict mode - execute JS in restrictive way to prevent issues.



arrow functions
---------------
Old JS:

const square = function(number) {
	return number * number;
}

New Style
const square = (number) => {
	return number * number;
}

if only one parameter - () not required
eg: const square = number => {return number * number; }
if no parameter - only () is required
eg: const square = () => {return 2* 2}
if only one return statement
eg: const square = number => number * number;

Another example

const jobs = [
	{id:1, isActive: true},
	{id:2, isActive: true},
	{id:3, isActive: false},
]

const activeJobs = jobs.filter(function(job) { return job.isActive;});
const activeJobs = jobs.filter(job => job.isActive);

callbacks and this and Arrow functions and this:
const person = {
	walk(){
		setTimeout(function(){ console.log(this); }, 1000);
	}
}

person.walk(); // setTimeout is a callback function. it is not assocaited to person object. "this" returns windows object

Old JS: We use "that"/"self"
const person = {
	walk(){
		var that = this;
		setTimeout(function(){ console.log(that); }, 1000);
	}
}

If we use arrow function in callback function, then "this" inherits the context. "this" returns person object

Array map()
---------------
Transform each item in array and return a new array.
eg: jobs.map();

Template
---------
'<li>' + color + '</li>'
`<li>${color}</li>` // templating

Object destructing
---------------------

const address = {
	street: '',
	city: '',
	country:''
}

Before
const street = address.street;
const city = address.city;
const country = address.country;


New:
const {street, city, country } = address;
const {street:st, city, country } = address;


Spread
-------

const first =[]
const second= []

Before
const combined = fisrt.concat(second);

New
const combined = [...first, ...second];
const combined = [...first, 'abc', ...second]; //allows to add an element at middle
const clone = [...first]; //to clone an array

Can be used for combining objects.
const first ={name:"Lak"}
const second= {job:"Dev"}

const combined = {...fisrt, ...second, location:"India"}


Objects
---------
Objecs can exist without a class. Class helps to reuse methods.

class Person {
	constructor(name){
		this.name = name;
	}
	walk(){
	}
}

const person = new Person('Mosh');

Inheritance
-----------------

class Teacher extends Person(){ }

- super()

Modules
---------
Write in different files. Each file is called modules.
person.js, teacher.js
By default private.
to make in public, export it. 
add "export".
add import {Person } from './person';

We can export one or more objects from a module.


export default - main thing we are exporting from module.
import Person from './person'; //No curly brace needed.
import {Person } from './person'; //Named export

import React, {Component} from 'react'; //'react' is a third party module under node modules.



-------------------------------JSX-------------------------------

JSX is an extension to javascript.
JSX parse javascript file. Look for mark ups. Convert mark up to React code.

const element = <h1>Hello World</h1> 
var element = React.createElement("h1", null, "Hello World");--Plain React Code


---------------------------------TypeScript---------------------------------

TypeScript is a superset of java script.
Every JS is a TS.
Every TS is not a valid JS.

TypeScript developed by Microsoft.

Browsers dont know how to run TypeScript.We need a transpiler to convert to JS.
tsconfig.js - CompilerOptions. target es5.

Advantage: Identify issues before.Catch errors early in development. Automatic Documentation.

-----------------------------------------------------------------

React Hook
https://www.valentinog.com/blog/hooks/

import React, { Component } from "react";

export default class Button extends Component {
  constructor() {
    super();
    this.state = { buttonText: "Click me, please" };
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(() => {
      return { buttonText: "Thanks, been clicked!" };
    });
  }

  render() {
    const { buttonText } = this.state;
    return <button onClick={this.handleClick}>{buttonText}</button>;
  }
}

With React hooks its possible to express the same logic without an ES6 class.

import React, { useState } from "react";

export default function Button() {
  const [buttonText, setButtonText] = useState("Click me, please"); //array destructuring
				//the parameter is the initial state
				//usestate returns two bindings - The value of state, a function for updating state

  return (
    <button onClick={() => setButtonText("Thanks, been clicked!")}>
      {buttonText}
    </button>
  );
}

To fetch data:

import React, { Component } from "react";

export default class DataLoader extends Component {
  state = { data: [] };

  componentDidMount() {
    fetch("http://localhost:3001/links/")
      .then(response => response.json())
      .then(data =>
        this.setState(() => {
          return { data };
        })
      );
  }

  render() {
    return (
      <div>
        <ul>
          {this.state.data.map(el => (
            <li key={el.id}>{el.title}</li>
          ))}
        </ul>
      </div>
    );
  }
}

Another approach:
render() {
    return this.props.render(this.state.data);
  }

<DataLoader
        render={data => {
          return (
            <div>
              <ul>
                {data.map(el => (
                  <li key={el.id}>{el.title}</li>
                ))}
              </ul>
            </div>
          );
        }}
      />

Using Hooks:useEffect

import React, { useState, useEffect } from "react";

export default function DataLoader() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch("http://localhost:3001/links/")
      .then(response => response.json())
      .then(data => setData(data));
  }, []); // second argument empty array - When the array is empty, the effect runs only once.

  return (
    <div>
      <ul>
        {data.map(el => (
          <li key={el.id}>{el.title}</li>
        ))}
      </ul>
    </div>
  );
}


useReducer

 const [data, dispatch] = useReducer(apiReducer, initialState); //read more

React hooks make render props and HOCs almost obsolete and provide a nicer ergonomics for sharing stateful logic.




-------------------------------------
Node
Webpack
Babel
EsLint


Code Formatting -Prettier

--------------------------------

package.json - list all your dependencies
	dependencies
	devDependencies
webpack - bundle your assets into single files
		multiple js files into one minified file
			one .js, .css, .jpg and .png file
webpack.config.dev.js
	devServer
	plugins
	module
		rules
			test: /\(js|jsx)
			exclude: node_module
			us: [babel-laoder
			test: (css)
			use:["style-loader, css-loader]
babel
	A JS compiler
	Transpile modern JS
	Transpile JSX to JS
	so that it is supported in all browsers
	can be configured through .bablerc file or package.json
	babel
		presets : bable-preset-react-app
	


npm script
	in package.json script session
	scripts:
		start: webpack serve --config webpack.config.dev 3000

	npm start

debugger; //browser stop at that line//u dont have to hunt the line

ESLint 
	Configure in package.json
	eslintConfig
	modify webpack config to use eslint-loader for js
	ESLint plugin

Create React Components

1. createClass
2. ES class
3. Function
4. Arrow Function

var HellowWorld = React.createClass({
	render: function(){
		return ( <h1>Hi</h1>);

class HelloWorld extends React.Component{

}

function HelloWorld(props) {

}

const HelloWorld - (props) => <h1><h1>
	}
});	


Use Functional Components over Class Components.
 
Container vs Presentation
Contaner - No markups. Passdata and actions down. Knows about Redux. Statefull
Presentation - All marksups. Doesnt know about Redux. No state


React Router - to handle routes at client side


index.html - div element with id "root"
index.js - import React and ReactDOM
	ReactDOM.render(
  <Router>
    <App/>
  </Router>,
  document.getElementById('root')
);

 <Routes>       
        <Route exact path="/" element={<HomePage/>}></Route>
        <Route path="/about" element={<AboutPage/>}></Route>
      </Routes>





Do I need Redux?
React - Reusable components
State Management - React Context or Redux

Child Components at different level want to reuse data. Same data in different components.In this case you may have to write same code two times. To avoid
1. Lift State to common parent node. Pass data down to child using props. Problem: prob Drilling
2. React Context . 
	Toplevel component - export UserContext.Provder
	Consuming Component - UserContext.Consumer
3.Redux
	Centalized Store - Any component connect to redux store.

Redux - Inter component communication. Two components that dont have a parent child components. To handle interation between them.Two components manipulating same data. Many actions. Same data in many places. 


Start with state in a single component
Lift State as needed
Try cotext or Redux when lifting state gets annoying

3 Principles
One immutable store
Actions trigger changes
Reducers update state


Action {type: RATE_COURSE, rating :5 } //type and data
Reducer - a function that retuns new state based on action. Contains a switch based on type
Components are switched to Store using React-Redux library





---------------------------------------

React + TypeScript

npx creat-react-app my-app --template typescript


package.json
tsconfig.json

Convert JSX to TypeScript
	yarn add typescript @types/react @types/react-dom @types/node
	Rename .jsx to ts
	

Error Boundary

class ErrorBoundary extends React.Component<Props,State> {



	constructor(props){
		super(props);
		this.state = { hasError : false } ;
	}

	static getDerivedStateFromError(error) {
		return { hasError: true };
	}
	
	componentDidCatch(error, errorInfo){
	}

	render(){
		if(this.state.hasError){
			return <h1> Something went wrong</h1>
		}
	}
}

----Differentiates TypeScript-----

interface Props {
	children: React.ReactNode;
}

interface State {
	hasError: boolean;
}



-------------------useState--------------

Two way data binding
	Input Field -> Data Model -> Label Text

const results = useState(""); //initialize to empty array
const inputText = results[0]; //state
const setInputText = results[1]; //method to set  state

Or

const [inputText, setInputText] = useState("");


const InputElement = () => {

    const [inputText, setInputText] = useState("");


    return <div><input onChange={(e) => {
        setInputText(e.target.value);
    }} placeholder="Enter Text here"/>
    {inputText}
    </div>
}



Hooks work only with functional components.


npm init -y
	will create package.json
react + next = Server Side Pages. First time to load is very less.



----------------------------------------------

Redux - immutability

Create new objects by copying existing objects

1. Object.assign( {}, state , { role: admin}) ; ---- //creates a new object by copying state object and replacing role property. Shallow Copy
2. const newState = {...state, role: admin}; // Shallow Copy //will not clone nested object
	const newUser = {...user, address: {...user.address}};




redux-immutable-state-invariant



A reducer is a function that takes state and action and returns a new state.

function(state, action) => newstate

function myReducer(state,action){
	switch(action.type){
		case: "INCREMENT_COUNTER":
			state.counter++;
			return state;
		default:
			return state;
	}
}
	

}
  
