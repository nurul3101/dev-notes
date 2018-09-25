## MobX

### Anything that can be derived from the application state, should be derived. Automatically

- React renders the application state by providing mechanisms to translate it into a tree of renderable components. MobX provides the mechanism to store and update the application state that React then uses

- npm i mobx mobx-react
- .babelrc => transform-decorators-legacy , transform-class-properties

```javascript
import { observable , computed } from 'mobX'

class TodoStore {
  @observable todos = ["buy milk","buy eggs"]
  @observable filter = ""
}

var store = window.store = new TodoStore

export default store

autorun(()=>{
// will run automatically if state changes
})
```

- we import observer from mobx-react
- In the render method we pass store as props.
- And the component which renders them is the observer. 

1) First of all, there is the application state. Graphs of objects, arrays, primitives, references that forms the model of your application. These values are the “data cells” of your application.
2) Secondly there are derivations. Basically, any value that can be computed automatically from the state of your application. These derivations, or computed values, can range from simple values, like the number of unfinished todos, to complex stuff like a visual HTML representation of your todos. In spreadsheet terms: these are the formulas and charts of your application.
3) Reactions are very similar to derivations. The main difference is these functions don't produce a value. Instead, they run automatically to perform some task. Usually this is I/O related. They make sure that the DOM is updated or that network requests are made automatically at the right time.
4) Finally there are actions. Actions are all the things that alter the state. MobX will make sure that all changes to the application state caused by your actions are automatically processed by all derivations and reactions. Synchronously and glitch-free.

[MobX: Ten minute introduction to MobX and React](https://mobx.js.org/getting-started.html)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NDI4MzA2NDRdfQ==
-->