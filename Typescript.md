# Typescript

- Javascript superset
- Building up on javascript, adds new features.
- Cannot be executed by browsers, so typescript needs to be converted into javascript before executing.
- run time errors can be avoided and caught during development
- ts-node allows us to compile typescript into javascript and execute it in the same step.
---
Type - Easy way to refer to different properties and functions that a value has.

If variable declaration and initialization is one the same line then typescript inference can detect the type.

- any is a Type, which means typescript has no idea what it is, Avoid variables with any at all costs
- We will add type annotations in functions which returns type any
- When we cannot infer the type of a variable then we need to add a type annotation.
- void is used when we don't have a return statement and never is used when we know that function will never reach the end, e.g throwing an error.
- when we destructure from object and want to add the annotation to the destructured variable the annotation should follow the structure of value from which it was destructured and not just the destructured value.
- Type alias, we can define our own types
```javascript
type Drink = [string,number]

const pepsi: Drink = ['carbonated',500];
```

- 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQwNDc4MzI2NywtNzUzNTE3MTkwLDI4Nj
c5MDA3MywyMDU2NjIzMzU3LC0xOTM4ODQxMDgzLDE2MzIzMjk2
MjcsMTQzMjM5Mjk1OSwtMTE0NjIzOTExNCwtMTU2NzUxMDY2MC
wtMjA4MzA4MDIwMCwxNDY3NjAwMDQ2LDU2NjUxODUwMiwxMTI4
ODU0MjQ2XX0=
-->