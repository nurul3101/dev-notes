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

- Interfaces - Creates a new type, describing the property names and value types of an object.
- While defining interface we can use complex types as well and are not confined to using primitive types, 
```javascript
  interface {
  summary(): string;
  year: Date;
  }
  
```
- Interface is kind of a gatekeeper, An object must implement an interface so that it could be passed to a function. This is the general idea for reusing code.

---
- Classes: 3 modifiers , public , private , protected.
- By default all the properties and methods are protected.`
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwODY3MDY1MDcsMTU1MDAzMjAyOSw5OD
A0ODgzODcsLTE0NzUxODcxNjAsLTc1MzUxNzE5MCwyODY3OTAw
NzMsMjA1NjYyMzM1NywtMTkzODg0MTA4MywxNjMyMzI5NjI3LD
E0MzIzOTI5NTksLTExNDYyMzkxMTQsLTE1Njc1MTA2NjAsLTIw
ODMwODAyMDAsMTQ2NzYwMDA0Niw1NjY1MTg1MDIsMTEyODg1ND
I0Nl19
-->