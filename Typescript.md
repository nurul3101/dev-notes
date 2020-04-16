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
  interface Reportable{
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
Typescript does not understand that we have a global object available by default.
So we need to install type definitions for that.

When we create a class we can use them to create instances as well as we can use them for Types.

When we are using | operator in a type, only the common properties between them can be accessed.
Implicit typecheck is when typescript checks for us that the properties that we pass to a function follows the interface or not.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE5NTQ0NzM1NiwtNDUxNTYzMjQ3LC0xOD
g2ODk0NTg0LDEzMzU4NjI0MTIsLTE3NjU1NTAwMjgsLTQ2OTc5
NzMzMCwxMjMwNzEwMTY5LDUzMjk0NjY2OCw4OTIyMjE1NzUsLT
IwODY3MDY1MDcsMTU1MDAzMjAyOSw5ODA0ODgzODcsLTE0NzUx
ODcxNjAsLTc1MzUxNzE5MCwyODY3OTAwNzMsMjA1NjYyMzM1Ny
wtMTkzODg0MTA4MywxNjMyMzI5NjI3LDE0MzIzOTI5NTksLTEx
NDYyMzkxMTRdfQ==
-->