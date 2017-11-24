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
>
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
> These methods are called when an instance of a component is being created and inserted into the DOM:
>
-	**constructor()**
-	**componentWillMount()**
-	**render()**
-	**componentDidMount()**

----------

Updating
-------------
> An update can be caused by changes to props or state. These methods are called when a component is being re-rendered:
>
- **componentWillReceiveProps()**
- **shouldComponentUpdate()**
- **componentWillUpdate()**
- **render()**
- **componentDidUpdate()**

----------

Unmounting
-------------
> This method is called when a component is being removed from the DOM:
>
- **componentWillUnmount()**

----------

Error Handling
-------------
> This method is called when there is an error during rendering, in a lifecycle method, or in the constructor of any child component.
>
- **componentDidCatch()**

----------


componentWillMount()
-------------
```componentWillMount()```
> **componentWillMount()** is invoked immediately before mounting occurs. It is called before **render()** (and re-rendered), therefore calling **setState()** synchronously in this method will not trigger an extra rendering. Generally, we recommend using the **constructor()** instead.
>
> Avoid introducing any side-effects or subscriptions in this method. For those use cases, use **componentDidMount()** instead.
>
> This is the only lifecycle hook called on server rendering.
>
> Can be a good place if you are fetching data using an ajax call.


componentDidMount()
-------------

```componentDidMount()```
> **componentDidMount()** is invoked immediately after a component is mounted. Initialization that requires DOM nodes should go here. If you need to load data from a removed endpoint, this is a good place to instantiate the network request.
>
> This method is a good place to set up any subscriptions. If you do that, don't forget to unsubscribe in **componentWillUnmount()**.
>
> Calling **setState()** in this method will trigger an extra rendering, but it is guaranteed to flush during the same tick. This guarantees that even though the **render()** will be called twice in the case, the user won't see the intermediate state. Use this pattern with caution because it often causes performance issues. It can, however, be necessary for cases like modals and tooltips when you need to measure a DOM node before rendering something that depends on its size or position.

----------

Refs
-------------
> In the typical React dataflow, **props** are the only way that parent components interact with their children. To modify a child, you re-render it with new props. However, there are a few cases where you need to imperatively modify a child outside of the typical dataflow. The child ro be modified could be an instance of a React component, or it could be a DOM element. For both of these cases, React provides an escape hatch.

 **When to Use Refs**
>	There are a few good use cases for refs:
>
- Managing focus, text selection, or media playback.
- Triggering imperative animations.
- Integrating with third-party DOM libraries.
> Avoid using refs for anything can be done declaratively.
> For example, instead of exposing **open()** and **close()** methods on a **Dialog** component, pass an **isOpen** prop to it.

**Don't Overuse Refs**
> Your first inclination may be to use refs to "make things happen" in your app. If this is the case, take a moment and *think more critically about where state should be owned in the component hierarchy*. Often, it becomes clear that the proper place to "own" that state is at a higher level in the hierarchy.

**Adding a Ref to a DOM Element**
> React supports a special attribute that you can attach to any component. The **ref** attribute takes a callback function, and the callback will be executed immediately after the component is mounted or unmounted.
>
> When the **ref** attribute is used on an HTML element, the **ref** callback receives the underlying DOM element as its argument.
>
> React will call the **ref** callback with the DOM element when the component mounts, and call it with **null** when it unmounts. **ref** callbacks are invoked before **componentDidMount** or **componentDidUpdate** lifecycle hooks.
>
> Using the **ref** callback just to set a property on the class is a common pattern for accessing DOM elements. The preferred way is to set the property in the **ref** callback. There is even a shorter way to write it: ```ref={input => this.textInput = input}```.

**Adding a Ref to a Class Component**
> When the **ref** attribute is used on a custom component declared as a class, the **ref** callback receives the mounted instance of the component as its argument.

**Legacy API: String Refs**
> In React's older API, the **ref** attribute is a string (i.e. **"textInput"**), and the DOM node is accessed as **this.refs.textInput**. We advise against it because string refs have *some issues*, are considered legacy, and **are likely to be removed in one of the future releases**. If you're currently using **this.refs.textInput** to access refs, it is recommended to use the callback pattern instead.

----------

propTypes
-------------
> Using **propTypes** property can help catch bugs with typechecking. Here is an example typechecking on a prop for a component:
>
```

import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};

```
> **PropTypes** exports a range of validators that can be used to make sure the data you receive is valid. When an invalid value is provided for a prop, a warning will be shown in the JavaScript console. For performance reasons, **propTypes** is only ckecked in development.


>
> Here is a [link](https://stackoverflow.com/questions/43302963/how-to-fix-react-15-5-3-proptypes-deprecated-warning-when-using-create-react-app) to a stack overflow that has an example of how to convert to a support way of using propTypes.
>
> Using the depreciated syntax will produce this error:
```React.PropTypes is deprecated since React 15.5.0, use the npm module prop-types instead  react/no-deprecated```
>
> Here is an example of the warning received when **propTypes** catches the incorrect property type: ```array``` when **propTypes** for the ```projects```  component is set to ```string```:
>
```
index.js:2177 Warning: Failed prop type: Invalid prop `projects` of type `array` supplied to `Projects`, expected `string`.
```
>
> Here is an example documenting the different validators:
>
```

import PropTypes from 'prop-types';

MyComponent.propTypes = {
  // You can declare that a prop is a specific JS primitive. By default, these
  // are all optional.
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,

  // Anything that can be rendered: numbers, strings, elements or an array
  // (or fragment) containing these types.
  optionalNode: PropTypes.node,

  // A React element.
  optionalElement: PropTypes.element,

  // You can also declare that a prop is an instance of a class. This uses
  // JS's instanceof operator.
  optionalMessage: PropTypes.instanceOf(Message),

  // You can ensure that your prop is limited to specific values by treating
  // it as an enum.
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),

  // An object that could be one of many types
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),

  // An array of a certain type
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),

  // An object with property values of a certain type
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),

  // An object taking on a particular shape
  optionalObjectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),

  // You can chain any of the above with `isRequired` to make sure a warning
  // is shown if the prop isn't provided.
  requiredFunc: PropTypes.func.isRequired,

  // A value of any data type
  requiredAny: PropTypes.any.isRequired,

  // You can also specify a custom validator. It should return an Error
  // object if the validation fails. Don't `console.warn` or throw, as this
  // won't work inside `oneOfType`.
  customProp: function(props, propName, componentName) {
    if (!/matchme/.test(props[propName])) {
      return new Error(
        'Invalid prop `' + propName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  },

  // You can also supply a custom validator to `arrayOf` and `objectOf`.
  // It should return an Error object if the validation fails. The validator
  // will be called for each key in the array or object. The first two
  // arguments of the validator are the array or object itself, and the
  // current item's key.
  customArrayProp: PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) {
    if (!/matchme/.test(propValue[key])) {
      return new Error(
        'Invalid prop `' + propFullName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  })
};


```
