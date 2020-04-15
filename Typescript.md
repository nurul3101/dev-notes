# Typescript

- Javascript superset
- Building up on javascript, adds new features.
- Cannot be executed by browsers, so typescript needs to be converted into javascript before executing. E.g Parcel
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
- Classes: 3 modifiers , public , private and protected.
- private properties/methods can be accessed only inside the class.
- protected properties can be accessed only in the class and child classes
- By default all the properties and methods are protected.

Shorthand syntax to create and instantiate properties while creating an instance 
```javascript
class Vehicle{
constructor(public color:string){}
}
```
Type definition file is kind of an adapter between javascript files and typescript files.
Type definition files are going to tell the typescript compiler which functions are available in javascript file, what arguments they take.
DefinitelyTyped is a project that maintains type definitions for all the popular libraries.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDQ2MTU0MDgyLC00Njk3OTczMzAsMTIzMD
cxMDE2OSw1MzI5NDY2NjgsODkyMjIxNTc1LC0yMDg2NzA2NTA3
LDE1NTAwMzIwMjksOTgwNDg4Mzg3LC0xNDc1MTg3MTYwLC03NT
M1MTcxOTAsMjg2NzkwMDczLDIwNTY2MjMzNTcsLTE5Mzg4NDEw
ODMsMTYzMjMyOTYyNywxNDMyMzkyOTU5LC0xMTQ2MjM5MTE0LC
0xNTY3NTEwNjYwLC0yMDgzMDgwMjAwLDE0Njc2MDAwNDYsNTY2
NTE4NTAyXX0=
-->