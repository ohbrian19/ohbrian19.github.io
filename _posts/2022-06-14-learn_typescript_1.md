---
layout: post
title:  "Learn TypeScript #1 2022-06-14"
---

This is my journey to learn **TypeScript**.

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

## Other tips

 1. How to compile ts file to js
	 - `npm i typescript -g`
	 - `tsc filename.ts`
	 - create `tsconfig.json` to set configuration details
		 - https://www.typescriptlang.org/tsconfig

