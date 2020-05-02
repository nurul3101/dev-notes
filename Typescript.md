# Typescript Notes

- Typescript is Javascript's superset
- Building up on javascript, adds new features.
- Cannot be executed by browsers, so typescript needs to be converted into javascript before executing. E.g Parcel
- run time errors can be avoided and caught during development
- ts-node allows us to compile typescript into javascript and execute it in the same step.
---
Type - Easy way to refer to different properties and functions that a value has.

If variable declaration and initialization is one the same line then typescript inference can detect the type.

- any is a Type, which means typescript has no idea what it is, Avoid variables with any at all costs
- We will add type annotations in functions which returns type any. Usually we should avoid any.
- When we cannot infer the type of a variable then we need to add a type annotation.
- void is used when we don't have a return statement and never is used when we know that function will never reach the end, e.g throwing an error.
- when we destructure from object and want to add the annotation to the destructured variable the annotation should follow the structure of value from which it was destructured and not just the destructured value.
- Type alias, we can define our own types
```javascript
type Drink = [string,number]

const pepsi: Drink = ['carbonated',500];
```

- Interfaces - Creates a new type, describing the property names and value types of an object.
- We can also use type instead of interface. One Advantage of using interface is that classes can implement them.
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

We can make sure that instances of a class follows the interface requirements by using implement clause.
```javascript
export class User implements Mappable {
///
}
```

While defining an interface if we add an ? if the property is optional.
```javascript
export interface Mappable  {
location:{
 lat:  number;
 lng:  number;
};
markerContent():  string;
color?:  string;
gradient?: string;
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzI1MTA2Mzk5LC01ODc4MzA3MzYsMTE5NT
Q0NzM1NiwtNDUxNTYzMjQ3LC0xODg2ODk0NTg0LDEzMzU4NjI0
MTIsLTE3NjU1NTAwMjgsLTQ2OTc5NzMzMCwxMjMwNzEwMTY5LD
UzMjk0NjY2OCw4OTIyMjE1NzUsLTIwODY3MDY1MDcsMTU1MDAz
MjAyOSw5ODA0ODgzODcsLTE0NzUxODcxNjAsLTc1MzUxNzE5MC
wyODY3OTAwNzMsMjA1NjYyMzM1NywtMTkzODg0MTA4MywxNjMy
MzI5NjI3XX0=
-->
