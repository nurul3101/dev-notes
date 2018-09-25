## TDD with Jest

- In TDD you write your tests first and then we develop the feature.
- TDD reduces errors and defects in long-run
- It leads to higher quality code
- Jest automatically runs the tests having extension of test.js
- Enzyme is a library by airbnb which allows us to test componets of React and duplicate behaviour like user-click , change etc

---

1) we write the test
2) we watch the test fail
3) we write code for the test to pass

- We use a global it() to run a unit test. it => Initialize
- we can also use test()
- #### *snapshots* keep a recorded history of your react components. we can test the entire component as a whole and there is no need to test the parts of the component individually.
- In enzyme we can obtain the state of the componenet with state() method and accessing properties of state with state().name
- Argument in expect() will be compared with toEqual()
- Each test should run in isolation from another test.
- In TDD we usually hard-code the values and then test.
- when simulating a function , the actual function is not called.

---

## Behaviour Driven Development(BDD)

- A variation of TDD  that tests for user scenarios
- *Given , when , then* are the keywords to depict BDD
- we use describe keyword to group tests.
- In each describe block beforeEach() and afterEach() will be executed on every tests.


---
```javascript
- describe() function groups certain related testcases.
- toMatchSnapshot() is used to confirm whether our component is
 properly rendered or not.
- we use find() to access a element in DOM and use simulate() to 
 replicate behaviour like change and click.
- state() gives us access to the componenets state
- exists() checks whether a DOM can be found for the JSX passed.
- we use toBe() with exists() and it accepts boolean value 
- contains() to check whether passed content exists in DOM
- we use jest.fn() to mock a function. 
- toHaveBeenCalledWith() used when we want to test that a function is 
 called with a specific parameter.
- Actions and reducers are pure functions so we dont need to mock 
 them.
- when we are calling an API at that time we generally mock 
 the functions.
```

---

## Enzyme

```javascript

Enzyme is a JavaScript Testing utility for React that makes it easier 
to assert, manipulate, and traverse your React Components' output.

npm i --save-dev enzyme enzyme-adapter-react-16

For configuring enzyme put following code in root of src

import Enzyme from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

Enzyme.configure({ adapter: new Adapter() });



- Shallow Rendering
- Full Rendering
- Static Rendering

```

### Relevant link : [Shallow Rendering · Enzyme](http://airbnb.io/enzyme/docs/api/shallow.html)

- We use test coverage to check how much of our ocde is covered by our test cases and which lines are affected by our test-cases
- npm run test -- --coverage command is used to watch our coverage.


- when our component is connected to redux then for testing purpose we need to add pass props manually in our test file and instead of exporting the connected version of our component we export the unconnected one.

```javascript
console.log(app.debug());
```
- To debug what is being rendered.
- we test reducers , actions and componenets.

- To test actions -> actions basically return an object so we create an expectedAction and then we actually call the function of actual file from our test.js file 
- we actually hard-code the value returned from our function (type and payload) and keep it in toEqual(part)

```javascript
it('creates an action to withdraw from the balance', () => {
  const withdraw = 10;

  const expectedAction = { type: constants.WITHDRAW, withdraw };
  expect(actions.withdraw(withdraw)).toEqual(expectedAction);
});
```
- To test the reducers
- We hard code the state and the action to be sent to the reducer and expect the value of the state to be returned.
```javascript
  it('withdraws from the balance', () => {
    const initialState = 10;
    const withdraw = 5;

    expect(
      balanceReducer(initialState, { type: constants.WITHDRAW, withdraw })
    ).toEqual(initialState - withdraw);
  });
  ```
  
- To test the actual componenets we first test the toMatchSnapshot() test
- Then finding the node test and then our buisness logic test.
- If componenet needs props we need to pass it manually from our test file.
- There is no need to test third party libraries and our index.js files

#### *Imp ->while testing action creators and reducers we actually call the functions by importing them and not by mocking them but while integration testing i.e action creators are called from the component then we mock them*

- Jest provides us mock window object and so we have access to cookies.
- We can provide mock functions with jest.fn() to the props interface of a component to check whether or not redux action creators are dispatched.


- For testing asynchronus redux code we need to mock the store. Thsese async actions will create pure action objects that our store will use.
- In actual cases we do not have access to the pure action objects that are created by these actions. But by mocking the store we can track that action objects that eventually get sent to the store

- redux-mock-store's default export is a function which allows us to configure mock store.
- For working with async code we need to use certain middlewares that allows us to return actions that are not objects.
- In Async API request we want to return a promise.
- Middlewares allow us to return other than plain objects like a function or promise.
- we do not need to make full-blown Http Request because that would waste API resources
- so to avoid that we use fetch-mock library.

- As we know createMockStore returns a function which we can use to initialize a store.can pass an array of middlewares as a param to createMockStore.
- fetchMock allows us to mock an endpoint and also we can try to return our custom data whenever user tries to fetch from it.
- Generally while testing redux we can test it easily as it returns a plain object but while working with async actions we have to deal with an extra layer of a middleware.
- For testing async action we use store.dispatch() to eventually send the actions and store.getActions() which returns an array of all the actions dispatched.
- when we use fetchmock then whenever we are using that url the rsponse specified in the second parameter will be returned.

- In fetchMock.get('url',{response})
- If the url is invokded then response will be returned. 
- FOr testing the combineReducers we need to pass empty object in state and actions while testing it.
- 


- We have unit-testing , integration testing and end-to-end testing.
- For end-to-end testing we use cypress.
- we have also static code-analysis like flow






<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUxNTQ2OTcwM119
-->