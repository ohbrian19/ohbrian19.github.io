
---
layout: post
title:  "Learn TypeScript #1 2022-06-14"
---

This is my journey to learn **TypeScript** part 1.

I decided to learn **TypeScript** to make my code more stable and to add static typing to JavaScript. Static typing means that the type of a variable cannot be changed at any point in a program.

## Why TypeScript?

- **TypeScript** prevents error before running the code
```
// math.ts
function sum(a: number, b: number) {
  return a + b;
}
sum('10', '20'); // Error: Argument of type 'string' is not assignable to parameter of type 'number'.
```
- With **TypeScript**, everything stays the way it was initially defined. If a variable is declared as a string, it will always be a string and won’t turn into a Boolean. This enhances the likelihood of functions working the way initially intended.

## Fundamentals

### Basic Types

- **String**
	- `let str: string = 'hello world';`
- **Number**
	- `let num: number = 1;`
- **Boolean**
	- `let boo: boolean = false;`
- **Array**
	- `let arr: Array<number> = [1, 2, 3];`
	- `let items: nummber[] = [1, 2, 3];`
- **Object**
	- `let obj: object = {};`
	- `let person: { name: string, age: number} = { name: 'Brian Oh', age: 999 }`
- **Tuple**
	- Tuple can contain two values of different data types.
	- `let address:  [string,  number]  =  ['New York',  11101]`
- **Enum**
- **Any**
	- `let str: any = 'hi';`
	- `let num: any = 10;`
	- `let arr: any = ['a', 2, true];`
- **Void**
	- In variable, allow only *undefined* and *null*.
	- In function, void does not return anything.
```
let unuseful: void = undefined;
function notuse(): void {
  console.log('sth');
}
```
- **Never**


### Function

How to declare basic types in functions.
```
function sum(a: number, b: number): number {
  return a + b;
}
```
- Add types to *parameters* and *return value*.
```
function sum(a: number, b: number): number {
  return a + b;
}
sum(10, 20); // 30
sum(10, 20, 30); // error, too many parameters
sum(10); // error, too few parameters
```
- **TypeScript** limits parameters
```
function sum(a: number, b?: number): number {
  return a + b;
}
sum(10, 20); // 30
sum(10, 20, 30); // error, too many parameters
sum(10); // 10
```
- Optional parameter


### Union Type

- TypeScript allows us to use more than one data type for a variable or a function parameter. This is called union type.
```
function logText(text: string | number) {
  // ...
}
```
- Pros of using Union Type
```
// Using any
function getAge(age: any) {
  age.toFixed(); // ERROR
  return age;
}

// Using union type
function getAge(age: number | string) {
  if (typeof age === 'number') {
    age.toFixed();
    return age;
  }
  if (typeof age === 'string') {
    return age;
  }
  return new TypeError('age must be number or string');
}
```
- **Intersection Type**
	- An intersection type is a type that merges several kinds into one.
```
interface Person {
  name: string;
  age: number;
}
interface Developer {
  name: string;
  skill: number;
}
type Capt = Person & Developer;
```

### Type Aliases

- Type aliases create a new name for a type. Type aliases are sometimes similar to interfaces, but can name primitives, unions, tuples, and any other types that you’d otherwise have to write by hand.
```
// Using string type
const name: string = 'brian';

// Using type aliases
type MyName = string;
const name: MyName = 'brian';
```
```
type Developer = {
  name: string;
  skill: string;
}
```
```
type User<T> = {
  name: T
}
```
- Difference between *Type* and *Interface*
	- *Interfaces* are basically a way to describe data shapes, for example, an object. 
	- *Type* is a definition of a type of data, for example, a union, primitive, intersection, tuple, or any other type.
	- *Interface* allows inheritance, but *Type* does not

## Other tips

 1. How to compile ts file to js
	 - `npm i typescript -g`
	 - `tsc filename.ts`
	 - create `tsconfig.json` to set configuration details
		 - https://www.typescriptlang.org/tsconfig
