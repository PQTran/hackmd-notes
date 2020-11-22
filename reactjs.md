# React.js
[ToC]

## Step-by-Step Guide
[source](https://reactjs.org/docs/introducing-jsx.html)

### JSX
JSX is a language that extends javascript with features similar to templating.

#### Notes
- emphasizes separation of concerns (components) over separation of technologies
- JSX expressions turn into function calls and evaluate to javascript objects
  - embedded expressions (within {...}) are evaluated when JSX expressions evaluates
- JSX escapes inputs before rendering (safe from injections)
- babel transcribes JSX to javascript (React.createObject())

#### Examples
*specifying attributes:*
```javascript
const element = <img src={user.avatarUrl} />;
```

*JSX formats:*
```javascript
const element = (
  <div>
    <h1>Hello World!</h1>
  </div>
);
```

### Rendering
React DOM handles rendering JSX elements.

#### Notes
- ReactDOM.render() gets called once
- updates only changes affected areas (html, attribute, tag content)

#### Elements
Elements are the smallest blocks of React apps.
- elements are immutable
- represents UI at single point of time

#### Examples
*binding elements to ReactDOM:*
```javascript
const element = <h1>Hello World!</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### Components and Props
Components are independent reusable isolated pieces.
Props are the properties provided to Components.

#### Components
- UI pieces used in multiple places
- complex UI pieces

#### Props
- stands for properties
- props are read-only
- Components act as pure functions to props

#### Examples
*function components:*
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

*class components:*
```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

*rendering components:*
```javascript
const element = <Welcome name="Sara" />;
```

### State and Lifecycle
State is a private and fully Component-controlled variable space.

#### State
- local and encapsulated (inaccessible by others)
- data flows uni-directional (top-down)
- must be modified by Component.setState()
  - only explict state properties overriden (shallow merge)
  - state updates are handled asynchronously
    - use Component.setState((state, props) => {}) for logic using prev state and props

#### Lifecyle
==mount==: initial component render
==unmount==: component removal

#### Examples
*creating state for class component:*
```javascript
class Welcome extends React.Component {
  constructor(props) {
    super(props);
    this.state = {};
  }
}
```

*using lifecycle hooks:*
```javascript
componentDidMount() {
  this.timerID = setInterval(() => this.tick(), 1000);
}

componentWillUnmount() {
  clearInterval(this.timerID);
}
```

*updating state of components:*
```javascript
this.setState({date: new Date()});
```

### Events
React event handling is similar to DOM event handling.

#### Examples
*DOM event handling:*
```javascript
<button onclick="activateLasers()">Activate Lasers</button>
```

*React event handling:*
```javascript
<button onClick={activateLasers}>Activate Lasers</button>
```

*binding class instance to event handler:*
```javascript
constructor(props) {
  super(props);
  this.state = {isToggleOn: true};
  // handleClick must also be defined within class
  this.handleClick = this.handleClick.bind(this);
}
```

*passing parameter to event handler:*
```javascript
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

### Conditional Rendering
Conditional rendering allows for selectively creating and displaying elements.

Hiding components does not affect lifecyles.

#### Examples
*assigning JSX elements to variables:*
```javascript
let button;
if (isLoggedIn) {
  button = <LogoutButton onClick={this.handleLogoutClick} />
} else {
  button = <LoginButton onClick={this.handleLoginClick} />
}
```

*embedded expressions in JSX:*
```javascript
return (
  <div>
    <h1>Hello!</h1>
    {unreadMessages.length > 0 &&
    <h2>You have {unreadMessages.length} unread messages.</h2>}
  </div>
);
```

*hiding components:*
```javascript
render() {
  return null;
}
```

### Lists and Keys
Lists of Components can be placed in JSX elements directly using {...}.

#### Keys
- helps React handle list changes (addition, removal, updates of list items)
- keys:
  - unique amongst siblings (not globally unique)
  - default key: item index (not recommended)
  - must be specified in direct children of list

#### Examples
*creating a list with JSX:*
```javascript
const listItems = [<li key="1">1</li>, <li key="2">2</li>];
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

### Forms
(HTML) forms work differently from DOM elements because they keep interal state.

#### Controlled Components
- input form element controlled by React
- value is controlled by state
  - uses onChange event handler to update state

#### Uncontrolled Components
- input with read-only values
  - example: file input

#### Examples
*form:*
```javascript
render() {
  return (
    <form onSubmit={this.handleSubmit}>
      <label>
        Name:
        <input type="text" value={this.state.value} onChange={this.handleChange} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}
```

*textarea:*
```javascript
<textarea value={this.state.value} onChange={this.handleChange} />
```

*form event handlers:*
```javascript
handleChange(event) {
  this.setState({value: event.target.value});
}

handleSubmit(event) {
  // do action
  event.preventDefault();
}
```

*drop-down list:*
```javascript
<select value={this.state.value} onChange={this.handleChange}>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

*multiple selection input:*
```javascript
<select multiple={true} value={['B', 'C']}>
```

*multiple inputs sharing event handler:*
```javascript
handleInputChange(event) {
  const target = event.target;
  const value = target.type === 'checkbox' ? target.checked : target.value;
  const name = target.name;
  this.setState({[name]: value});
}

<input
  name="numberOfGuests"
  type="number" 
  value={this.state.numberOfGuests} 
  onChange={this.handleInputChange} />
```

### Lifting State Up
Technique of sharing state with multiple Components to reflect the same changing data.

#### State
- only one source of truth (SoT) exists
  - uncontrolled components: owns SoT
  - controlled components: parent owns SoT

#### Technique
- replace this.state with this.props
- event handlers call this.props.eventHandler

### Composition and Inheritance
#### Composition
- containment
  - container component has variable children elements
- specialization
  - special case of another component

#### Inheritance
- no use-cases
  - reusable non-UI functionality can be extracted to separate javascript module

#### Examples
*containment with props.children:*
```javascript
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}

<FancyBorder color="blue">
  <h1 className="Dialog-title">Welcome</h1>
  <p className="Dialog-message">Thank you for visiting our spacecraft!</p>
 </FancyBorder>
```

*containment with holes:*
```javascript
function App() {
  return (
    <SplitPane
      left={<Contacts />}
      right={<Chat />} />
  );
}
```
