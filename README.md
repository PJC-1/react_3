React JS Crash Course
===================
> Following **Traversy Media**'s Reactjs tutorial on youtube, here's the [link](https://www.youtube.com/watch?v=A71aqufiNtQ&t=121s).


----------


Some Advantages Of React
-------------
>
-	Design simple declarative views for each state in your application
-	Encapsulated components
-	Dynamic properties & state
-	Virtual DOM
-	Completely independent of the rest of your application
-	Can render on the client or server

----------

Virtual DOM
-------------
> React abstracts away the DOM and creates its own version which is simplified and only includes the things that you need.
>
-	Helps identify which parts have changed
-	Determines how to upload the browsers DOM more efficiently
-	Much more lightweight / Works faster

----------

JSX - JavaScript Syntax Extension
-------------
> A preprocessor step that adds XML syntax to JavaScript
-	Looks like XML/HTML
-	Defines a familiar syntax for defining tree structures with attributes
-	Is not required but makes things **much** easier

----------

Component Lifecyle
-------------
> Each component has several **"livecycle methods"** that you can override to run code at particular times in the process. Methods prefixed with **will** are called right before something happens, and methods prefixed with **did** are called right after something happens.

----------

Mounting
-------------
> These methods are called when an instance of a component is being created and inserted into the DOML:
-	**constructor()**
-	**componentWillMount()**
-	**render()**
-	**componentDidMount()**

----------

Updating
-------------
> An update can be caused by changes to props or state. These methods are called when a component is being re-rendered:
- **componentWillReceiveProps()**
- **shouldComponentUpdate()**
- **componentWillUpdate()**
- **render()**
- **componentDidUpdate()**

----------

Unmounting
-------------
> This method is called when a component is being removed from the DOM:
- **componentWillUnmount()**

----------

Error Handling
-------------
> This method is called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.
- **componentDidCatch()**

----------


componentWillMount()
-------------
```componentWillMount()```
> **componentWillMount()** is invoked immediately before mounting occurs. It is called before **render()** (and re-rendered), therefore calling **setState()** synchronously in this method will not trigger an extra rendering. Generally, we recommend using the **constructor()** instead.
> Avoid introducing any side-effects or subscriptions in this method. For those use cases, use **componentDidMount()** instead.
> This is the only lifecycle hook called on server rendering.
> Can be a good place if you are fetching data using an ajax call.


----------

Refs
-------------
> In the typical React dataflow, **props** are the only way that parent components interact with their children. To modify a child, you re-render it with new props. However, there are a few cases where you need to imperatively modify a child outside of the typical dataflow. The child ro be modified could be an instance of a React component, or it could be a DOM element. For both of these cases, React provides an escape hatch.

 **When to Use Refs**
>	There are a few good use cases for refs:
- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.
> Avoid using refs for anything can be done declaratively.
> For example, instead of exposing **open()** and **close()** methods on a **Dialog** component, pass an **isOpen** prop to it.

**Don't Overuse Refs**
> Your first inclination may be to use refs to "make things happen" in your app. If this is the case, take a moment and *think more critically about where state should be owned in the component hierarchy*. Often, it becomes clear that the proper place to "own" that state is at a higher level in the hierarchy.

**Adding a Ref to a DOM Element**
> React supports a special attribute that you can attach to any component. The **ref** attribute takes a callback function, and the callback will be executed immediately after the component is mounted or unmounted.
> When the **ref** attribute is used on an HTML element, the **ref** callback receives the underlying DOM element as its argument.
> React will call the **ref** callback with the DOM element when the component mounts, and call it with **null** when it unmounts. **ref** callbacks are invoked before **componentDidMount** or **componentDidUpdate** lifecycle hooks.
> Using the **ref** callback just to set a property on the class is a common pattern for accessing DOM elements. The preferred way is to set the property in the **ref** callback. There is even a shorter way to write it: ```ref={input => this.textInput = input}```.

**Adding a Ref to a Class Component**
> When the **ref** attribute is used on a custom component declared as a class, the **ref** callback receives the mounted instance of the component as its argument.

**Legacy API: String Refs**
> In React's older API, the **ref** attribute is a string (i.e. **"textInput"**), and the DOM node is accessed as **this.refs.textInput**. We advise against it because string refs have *some issues*, are considered legacy, and **are likely to be removed in one of the future releases**. If you're currently using **this.refs.textInput** to access refs, it is recommended to use the callback pattern instead.

----------
