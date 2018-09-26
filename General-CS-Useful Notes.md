## General

- By using get and set in ES6 we can access those functions as a property
- Web-Workers are used to offload intense compute operations onto another execution thread.(Different than service-workers)
- Web-Workers good for Parallelism and Service-Worker good for offline 
- workers run in another global context that is different from the current window
- [Using Web Workers - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)
- Basically we use postMessage() adn onmessage() to communicate with main js file and worker. 
- Workers may spawn more workers if they wish.
- A shared worker is accessible by multiple scripts
- A dedicated worker is accessible only to the script which called it.
- Redux -> createStore , applyMiddleware
- react-redux -> connect , Provider
- redux-devtools-extension -> Compose with Devtools

- Try to find the preferred medium of learning.
- Improve foundational skills
- Do not try to learn everything at the same time
- Example learning React + Redux + Styled Components etc
- Try to learn one thing at a time like just react
- Because if you learn + redux and then you want to replace redux with Apollo you have to relearn concepts.
- Get excited about what you are learning maybe like create an app which gives you quote from GOT
- Dont try to follow all best practices while learning. They will follow
- While learning you will have to start from scratch multiple times. ( Iteration Driven development)
- Follow style guides after you are comfortable



- mapStateToProps and mapDispatchToProps both return an object whose key will be injected in props.
 i.e this.props.state and this.props.actions
 - As we import Action Creators there is no need to import the reducers because we can automatically access them as we have wrapped our main component inside the Provider which has access to the store.
 - Provider gives access to the store/Reducers to the connect function.
 - mapStateToProps -> As the name suggests it takes the state from the store and maps it to props of the connected component.

Action Creators returns an Object -> we import those action creators in our component -> In connect function in the second argument we pass these action creators -> Now connect function can access the reducers because it is wrapped by the Provider component which has store as an attribute.
In the store createStore() we pass our rootReducer/combineReducer -> so our action will pass through all the reducers and the state will be updated.
As the state changes our mapStateToProps will be invoked and our component will re-render.

```javascript
import React from 'react';
import { string } from 'prop-types';
const Link = ({ title, url }) => <a href={url}>{title}</a>;
Link.propTypes = {
  title: string.isRequired,
  url: string.isRequired
};
export default Link;
```
- we use prop-types to make sure that props are passed and are of a specific-type.
- The most easiest way to mock files is using the jest.mock function which automatically mocks the file by returning mocked functions. Let try to mock react-dom and check whether the render function has been called.
```javascript
import React from 'react';
import { render } from 'react-dom';
import Link from './Link';
jest.mock('react-dom');
describe('Link', () => {
  it('should render correctly', () => {
    expect(render).toHaveBeenCalledWith(
      <Link title="mockTitle" url="mockUrl" />, 'element-node'
    );
    expect(render).toHaveBeenCalledTimes(1);
  });
});
```
- Important Http Status Codes
- 200 Series - Success
- 300 Series - Redirection
- 400 Series - Client Side Error
- 500 Series - Server Side Error

- 200 - Ok
- 201 - Created
- 204 - No ContentBody

- 300 - Moved Permanently

- 400 - Bad Request
- 401 - Unauthorized
- 403 - Forbidden
- 404 - Not Found

- 500 - Internal Server Error


---
- Do not mutate the state.
- in combineReducers function the key can be anything and value will be the reducer. The key which we have mentioned should be the same in state.key_name value in mapStateToProps and the key could be anything which will be accessible through this.props

- Read StackTrace
- Do not debug production. make sure it is not cached
- While Debugging APIs make sure to check network tabs.
- 


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI1NTAyMDcxM119
-->