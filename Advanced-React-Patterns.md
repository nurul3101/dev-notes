## Advanced React Patterns

```javascript
this.setState((currentState)=>{
  return { on : !currentState.on}
},()=>{
  // Callback Functions
});
```

- this.setState() usually takes an object as input but it can also take a function as an input which will have its current state as an input. It is used when we have to change the state based on what was the value of a parameter in the previous state. The second parameter is a callback function which is executed after the state is changed.

```javascript
this.setState({ on : !this.state.on},()=>{
  //callback function
});
```
- we can also use the above way but we should use the state updater function to avoid issues with batching 

- The Children API i.e {this.props.children} will render the component which is passed between <> and </>
- E.g
```javascript
const Picture = (props) => {
  return (
    <div>
      <img src={props.src}/>
      {props.children}
    </div>
  )
}

//App.js
render () {
  return (
    <div className='container'>
      <Picture key={picture.id} src={picture.src} >
          //what is placed here is passed as props.children  
      </Picture>
    </div>
  )
}
```

- React.Children.map() will map over all the children and React.cloneElement will take the children and add the props that we passed in the second argument.
```javascript
    return React.Children.map(this.props.children, childElement => {
      return React.cloneElement(childElement, {
        on: this.state.on,
        toggle: this.toggle,
      })
    })
```

- The props will be added to the immediate children only
- Example
```javascript
  return (
    <Toggle onToggle={onToggle}>
      <Toggle.On>The button is on</Toggle.On>
      <Toggle.Off>The button is off</Toggle.Off>
      <div>
        <Toggle.Button />
      </div>
    </Toggle>
  )
```

- Here in the div the props will be passed and not in the Toggle.Button.

- When we are using compound components then we should use Static Properties on the class.

- we should never mutate our props. like this.props.x='abc' instead we should pass props as {...props} and if we will pass a prop which is in props object then it will be overridden.


---

- Context API is used when we do not want to explicitly pass props to deeply nested components. In context API we use Provider and Consumer to pass props.

- If Consumer is used outside the Provider then the value which is passed in React.createContext('this_Value') will be passed to the Consumer.
- Provider takes an value attribute which we initialize it with state generally.
- When we want to use the props we passed in the Provider we use the Consumer tag
- And we evalaute a function between those two tags which takes a parameter.
- we use that parameter to access our props.
- Before using Consumer and Provider we need to create a context using React.createContext().

---

- *If we are not using this in a function in class it does not need to be in the class.*
- we can make it a static method or can move it out of the class and make it a const.

#### children is the implict prop which is passed between opening and closing of a tag.

- whenever we want to pass data to child component in the form of props instead of directly passing the value if we pass the state then the component will render only when the value changes instead of initializing everytime.

## render props pattern

- in render props pattern we pass a prop named render which is a function and returns another component.
- A render prop is a function prop that a component uses to know what to render.
- If we want we can pass the props between opening and closing tag. Instead of specifying them as an attribute.
- The main concept to understand here is that the Mouse component essentially exposes its state to the App component by calling its render prop. Therefore, App can render whatever it wants with that state
- In render props we will find the render function inline between the  opening and the closing tag. and that can be refernced as this.props.children

```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import PropTypes from 'prop-types'

// Instead of using a HOC, we can share code using a
// regular component with a render prop!
class Mouse extends React.Component {
  static propTypes = {
    render: PropTypes.func.isRequired
  }

  state = { x: 0, y: 0 }

  handleMouseMove = (event) => {
    this.setState({
      x: event.clientX,
      y: event.clientY
    })
  }

  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>
        {this.props.render(this.state)}
      </div>
    )
  }
}

const App = React.createClass({
  render() {
    return (
      <div style={{ height: '100%' }}>
        <Mouse render={({ x, y }) => (
          // The render prop gives us the state we need
          // to render whatever we want here.
          <h1>The mouse position is ({x}, {y})</h1>
        )}/>
      </div>
    )
  }
})

ReactDOM.render(<App/>, document.getElementById('app'))
```








<!--stackedit_data:
eyJoaXN0b3J5IjpbMzc4MTYwMTI2LDE1NTEzNzgyOTNdfQ==
-->