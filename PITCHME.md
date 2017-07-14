---
# TypeScript

https://gitpitch.com/RPDeshaies/typescript-presentation-1
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
class Person {}
const person = new Person();
```
+++
## Constructor
```ts
class Person {
  constructor(name:string, personType: PersonType) {
    // do stuff...
  }
}
const person = new Person(name, personType);
```
+++
## Constructor shortcuts...
```ts
class Person {
  constructor(public name:string, 
    private socialSecurityNumber: number) {
  }
}
const person = new Person(name, socialSecurityNumber);
```
+++
## Properties
```ts
class Person {
  public name: string; // undefined
  private socialSecurityNumber: number;
  private readonly PERSON_NAME_MAX_LENGTH: number = 50;
  private readonly HAVE_SUPER_POWER: boolean = false;

  constructor(name:string) {
    this.name = name;

    if(name === 'Spiderman') {
      this.HAVE_SUPER_POWER = true;
    }
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
## Functions (protected)
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
---
# Interface
+++
### Usefull for objects coming from the server or when you want to valid very basic types
+++
## Syntax
```ts
interface IAnimal {
  name?: string;
  color?: string;
  speak?: () => string;
}

let tiger: IAnimal = {}; // valid because `?`
let tiger: IAnimal = {
  name: 'Bouyah',
  color: 'white',
  speak: () => {
    console.log('I love bananas');
  },
};
tiger.name // = 'Bouyah', etc...
let tiger: IAnimal = new IAnimal(); // invalid ! not a class.
```
---
# Inheritance
+++
## There's 2 types : extends vs implements
+++
## Extends
A `class` **`extends`** another `class`.

* It needs to call the parent's constructor
* It needs to implement all of its `abstract` functions if the parent class is itself `abstract`
* You can only `extend` ONE class
+++
![](http://www.programmerinterview.com/images/Diamond_inheritance.png)
+++
```ts
abstract class Animal {
  constructor(public name:string) {}
  
  protected speak(): void {
    console.log(`Wubba Lubba Dub Dub ${this.name}`);
  }

  // I don't know how to move
  abstract public move(): void;
}

class Tiger extends Animal{
  constructor(public name: string, public color: Color) {
    super(name); // mandatory
    this.speak();
  }

  // Hey ! I know how a tiger moves !
  public move(): void{
    // do stuff... like walking !
  }
}
```
+++

![](https://media.giphy.com/media/GWx7HFtKBAV3O/giphy.gif)

+++
## Implements
+++

A `class` **`implements`** one-to-many `interface`

* It needs to implement all of its `interfaces` methods and properties
* In the case of implementing an interface, it is basically the same thing as `extending`  a `fully abstract class`
+++
```ts
interface IAnimal {
  // I don't know how to move
  // no need for the `abstract` keyword
  // everything is public in interfaces !
  move(): void;
}

class Duck implements IAnimal{
  constructor(public name: string, public color: Color) {
    // not important
  }

  // Hey ! I know how a duck moves !
  public move(): void{
    // waddle waddle
  }
}
```
+++

![](https://media.giphy.com/media/cLYaf1ExHsxX2/giphy.gif)
---
# Generics
+++
Being able to create a component that can work over a variety of types rather than a single one.
+++
## Use them in functions
```ts
function isArrayEmpty<T>(array: Array<T>): boolean {
  if (array.length === 0) {
    return true;
  }
  return false;
}
```
+++
## Use them in class
```ts
class HashMap<T>{
  private hash: any;
  constructor() {
    this.hash = {};
  }

  public get(key: string): T {
    return this.hash[key] as T;
  }

  public set(key: string, value: T) {
    this.hash[key] = value;
  }
}

const foo = new HashMap<number>();
foo.set('key1', 25); // valid
foo.set('key1', '25'); // invalid !
console.log(foo.get('key1')) // 25
```
+++
## You can also use contraints

```ts
class HashMap<T extends Animal> {}
```
---
# Async/Await
+++
## Details

You wait for function using the `await` keyword

You can only wait for a function if : 

* That function is `async`
* You are `async`
* That function is returning a `Promise<T>`

You don't need to use the `.then` or `.catch` syntax since it will create a `callback hell`
+++
Example : 

```ts
class AnimalService {
  public static async getAnimalDetail(name: string): Promise<any> {
    //return httpClient.get('/some-url', { name: name });

    return new Promise((resolve) => {
      resolve({
        name: 'Robert',
        color: 'white'
      })
    });
  }
}

async function doStuff(): Promise<void> {
  const details = await AnimalService.getAnimalDetail('Robert');
  console.log(details);
}

```

---
# Thank you !
### Questions ?
