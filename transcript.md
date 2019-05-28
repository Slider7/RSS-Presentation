## Introduction to React  


Hello everybody! My neme is Kemalkhan Shlembayev, i am a student of RSSchool. 
Today we will talk about React.

### What is React?
React is one of the most popular JavaScript libraries. 
It is an open-source project created by Facebook.
React is not a framework, unlike Angular.
It is a library for build view layer of an MVC application (Model View Controller). So, react is all about the user interface, not model not a controller. 
I will try to give you a basic understanding of React by building a very simple application, so let's get started. 

### The Setup  
There are a few ways to set up React, but I will show you the simplest way. It's not a way to build complex applications, it is just a way to try the React without installing Node.js, Babel, Webpack and so on.
The simplest way is to create HTML file which loads three CDNs in the head - React, React DOM, and Babel. 
In the body of our index.html, we add a div tag with the id of #root. This is the entry point for our app. 
Then, we need to add script tag: <script type="text/babel"> in the body. We will write all our React code inside that tag. The text/babel script type is necessary for using Babel. We need Babel because React uses something called JSX to write components. Babel transforms the JSX into plain JavaScript so that the browser can understand it.
Our index.html:
~~~~
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Hello React!</title>
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
  </head>

  <body>
    <div id="root"></div>
    <script type="text/babel">
      // React code will go here
    </script>
  </body>
</html>	
~~~~
### Components  
React is all about components. Components can be class-based or functional, in this example, we will use class-based components. 
Let's create a component named "Hello" by extending React-Component class:
~~~~
class Hello extends React. Component {
    render() {
        return <h1>Hello world!</h1>;
    }
}
~~~~
Inside class we can define the methods for our component. In this example, we have one method - it's called render().
Inside render() method we return what we want to draw on the page - here we want from React to draw an h1 tag with the text "Hello world!".
To display component on the screen, we use ReactDOM.render() :
~~~~
ReactDOM.render(
    <Hello />, 
    document.getElementById("root")
);
~~~~
The place where we mount our app is `<div id="root"></div>`. So we’re simply saying: "React, render the Hello component, inside the DOM node which has id of root."
### JSX  
The HTML-like strings (`<h1>` and `<Hello />`) is the JSX code. It’s not actually HTML, it is closer to JavaScript. JavaScript expressions can be embedded in JSX using curly braces, including variables, functions, and properties.
Look at this two lines of code: 
JSX:
`const heading = <h1 className="site-heading">Hello, React</h1>`
non-JSX:
`const heading = React.createElement('h1', { className: 'site-heading' }, 'Hello, React!')`
JSX is easier to write and understand than creating and appending many elements in vanilla JavaScript. Probably JSX it is one of the reasons why people love React so much.

### Working with data in React  
React has two types of data: props and state. 
The state is private and can be changed by the component itself. 
Props are external, and not controlled by the component. Props passed down from higher-level components, which also control the data.
A component can change its internal state directly. It can not change its props directly.

### Props  
Our Hello component is totally static - it always renders out the same message. React give us the ability to write a component once, and then reuse it how we want, this is reusability. Let's change our component so it can display different messages. 
To do this, we’ll add a prop called message and give it value "RSS Student":
~~~~
ReactDOM.render(
    <Hello message="RSS Student" />, 
    document.getElementById("root")
);
~~~~
Now we can access this prop inside the Hello component by referencing this.props.message:
~~~~
class Hello extends React.Component {
    render() {
        return <h1>Hello {this.props.message}!</h1>;
    }
}
~~~~
So, we have a reusable component that renders what we give it.

### State  
If we want to change the data in our app - we need to store data in a component’s state.
Initializing state
To initialize the state, we need to set this.state in the constructor() method of the class. Our state is an object, which in our case has one key called message:
~~~~
class Hello extends React. Component {
    constructor(){
        super();
        this.state = {
            message: "RSS Student (from state)!"
        };
    }
    render() {
        return <h1>Hello {this.state.message}!</h1>;
    }
}
~~~~
We have to call super() in the constructor, because it must be called before the first access to the keyword this in the body of the constructor.

### Changing the state  
To modify the state, we add a method updateMessage(), inside of which
we call this.setState(), and pass the new state object as the argument. 
~~~~
class Hello extends React. Component {
    constructor(){
        super();
        this.state = {
            message: "RSS Student (from state)!"
        };
        this.updateMessage = this.updateMessage.bind(this);
   }
    updateMessage() {
        this.setState({
            message: "RSS Student (from CHANGED state)!"
        });
    }    
    render() {
        return <h1>Hello {this.state.message}!</h1>;
    }
}
~~~~
Pay attention that in the constructor we need to bind the this keyword to the updateMessage method. (or we can use arrow function).

### Event Handlers  
Now we need some user control to call the updateMessage() method.
So let’s add a button to our app, we'll add it to the render() method:
~~~~
render() {
  return (
     <div>
       <h1>Hello {this.state.message}!</h1>
       <button onClick={this.updateMessage}>Click me!</button>
     </div>   
  )
}
~~~~
We attach an event listener for the onClick event of our button. 
Note -properties and methods in JSX are camelCase - onclick will become onClick. 
Now, when button will clicked, component will call the updateMessage method. In that method we call this.setState() which changes the value of this.state.message. 
#### The Hello component, final version:  
~~~~
class Hello extends React.Component {
    constructor(){
        super();
        this.state = {
            message: "RSS Student (from state)!"
        };
        this.updateMessage = this.updateMessage.bind(this);
    }
    updateMessage() {
        this.setState({
            message: "RSS Student (from changed state)!"
        });
    }
    render() {
         return (
           <div>
             <h1>Hello {this.state.message}!</h1>
             <button onClick={this.updateMessage}>Click me!</button>
           </div>   
        )
    }
}
~~~~
Important note - calling this.setState() tells React to re-render the component. That is why we see the changes.

Our app is very primitive, but by creating it, we reviewed basic concepts of React: components, props, state and how to change state and how to display component on the page. And that's it! Now you have a very basic understanding of what is the React and how it works. 

Thank you for your attention, and all the best! 