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
# Number (int float)

```ts
const myNumber: number = 3;
```
+++
# String

```ts
const myString: string = 'toto';
```
+++
# Boolean
```ts
const isThisPresentationAwesome: boolean = true;
```
+++
# Enum

```ts
enum MediaType { Movie, Music, Audiobook, Book = 22 };
const mediaType: MediaType = MediaType.Book;
```
+++
# Void

```ts
function setUserName(name: string): void
```
--- 
# Types (Reference)
+++
# Array

```ts
const employees: Array<IEmployee> = [];
employees.push({ name: 'Charle Patenaude' });
```
+++
# Object (class, interface, module)
--- 
# Functions
+++
# Types for parameters
```ts
function setUser(user: { name: string, type: UserType }): boolean {
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
# Optionnal and Default Parameter
```ts
function setUser(user: { name: string, type?: UserType }): boolean {
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
# Function Overloads
```ts
class UserService {
  public save(user: IUser): void;
  public save(user: IUser, callback?: Function): void {

  }
}
```
+++ 
# Fat Arrow functions
```ts
const userService = new UserService();
userService.save(user, () => {

});
```
+++ 
# Rest parameters
```ts
function iTakeItAll(first, second, ...allOthers) {
  console.log(allOthers);
}
iTakeItAll('foo', 'bar'); // []
iTakeItAll('foo', 'bar', 'bas', 'qux'); // ['bas','qux']
```

