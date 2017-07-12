---
# TypeScript
---
# Au menu...

* What is TypeScript
* Types (Value vs Ref)
* Functions
* Class
* Interface
* Inheritance
* Generics
* Async/Await
--- 
# What is TypeScript

TypeScript is a **superset** of JavaScript which primarily provides optional static **typing**, **classes** and **interfaces**. 

One of the big benefits is to enable IDEs to provide a richer environment for spotting **common errors** as you type the code.
--- 
# Types (Value or Primitive)
+++
## Number (int float)

```ts
// `var` is valid, but don't use it
let myNumber: number = 3;
const myNumber: number = 3;
const myNumber: number = 3.44;

// `null` is valid, but don't use it
const myNumber: number | undefined = 3;
// don't abuse of the `|` operator for types
const myNumber: number | undefined = undefined;
```
+++
## String

```ts
const myString: string = 'toto';
const myString: string = "toto";
```
+++
## Boolean
```ts
const isThisPresentationAwesome: boolean = true;
```
+++
## Enum

```ts
// index starts at `0`, but you can change it
enum MediaType { Movie, Music, Audiobook, Book = 22 };
const mediaType: MediaType = MediaType.Book;
```
+++
## Void

```ts
function setUserName(name: string): void
```
--- 
# Types (Reference)
+++
## Array

```ts
const employees: Array<IEmployee> = [];
employees.push({ name: 'Charle Patenaude' });
```
+++
## Object (class, interface, module)
--- 
# Functions
+++
## Types for parameters & return value
```ts
function setUser(user: { name: string, userType: UserType }): boolean {
  try {
    //call api...
    return true;
  }
  catch (error) {
    return false;
  }
}
```
+++ 
## Optionnal and Default Parameter
```ts
function setUser(user: { name: string, userType?: UserType }): boolean {
  try {
    //call api...
    return true;
  }
  catch (error) {
    return false;
  }
}
```
+++ 
## Function Overloads
```ts
class UserService {
  public save(user: IUser): void;
  public save(user: IUser, callback?: Function): void {

  }
}
```
+++ 
## Fat Arrow functions
```ts
const userService = new UserService();
userService.save(user, () => {

});
```
+++ 
## Rest parameters
```ts
function iTakeItAll(first, second, ...allOthers) {
  console.log(allOthers);
}
iTakeItAll('foo', 'bar'); // []
iTakeItAll('foo', 'bar', 'bas', 'qux'); // ['bas','qux']
```
---
# Class
+++
## Declaration
```ts
class Employee {}
const employee = new Employee();
```
+++
## Constructor
```ts
class Employee {
  constructor(name:string, employeeType: EmployeeType) {
    // do stuff...
  }
}
const employee = new Employee(name, employeeType);
```
+++
## Constructor shortcuts...
```ts
class Employee {
  constructor(public name:string, 
    public employeeType: EmployeeType, 
    private socialSecurityNumber: number) {
  }
}
const employee = new Employee(name, employeeType, socialSecurityNumber);
```
+++
## Properties
```ts
class Employee {
  public name: string; // undefined
  public employeeType: EmployeeType;
  private socialSecurityNumber: number;

  constructor(name:string) {
    this.name = name;
  }
}
```
+++
## Functions (public)
```ts
class Animal {
  constructor(public name:string) {
  }
  
  public sayHello(): void {
    console.log(`Wubba Lubba Dub Dub ${this.name}`);
  }
}
```
+++
## Functions (private)
```ts
class Animal {
  constructor(public name:string) {
    this.sleep();
  }
  
  private sleep(): void {
    // ...
  }
}
```
+++
## Functions (procted)
```ts
class Animal {
  constructor(public name:string) {
  }
  
  protected speak(): void {
    console.log(`Wubba Lubba Dub Dub ${this.name}`);
  }
}

class Tiger extends Animal{
  constructor(public name: string, public color: Color) {
    super(name); // mandatory
    this.speak();
  }
}
```
+++
