---
layout: post
title:  "Learn TypeScript #3 2022-06-16"
---

This is my journey to learn **TypeScript** part 3.

### Generics
*Generics* offer a way to create reusable components. Generics provide a way to make components work with any data type and not restrict to one data type.

```
function getText<T>(text: T): T {
  return text;
}
```

```
function logText<T>(text: T): T {
  console.log(text.length); // Error: T doesn't have .length
  return text;
}
```

```
function logText<T>(text: T[]): T[] {
  console.log(text.length); 
  return text;
}
```

```
function logText<T>(text: Array<T>): Array<T> {
  console.log(text.length);
  return text;
}
```

**Generic Interface**

```
interface GenericLogTextFn<T> {
  (text: T): T;
}
function logText<T>(text: T): T {
  return text;
}
let myString: GenericLogTextFn<string> = logText;
```

- Generic can be applied to *Class* as well

**Class Generic**

```
class GenericMath<T> {
  pi: T;
  sum: (x: T, y: T) => T;
}

let math = new GenericMath<number>();
```

**Generic Constraint**

```
function logText<T>(text: T): T {
  console.log(text.length); // Error: T doesn't have .length
  return text;
}
```

- Since parameter T does not have specific type, error occurs in `length`.

```
interface LengthWise {
  length: number;
}

function logText<T extends LengthWise>(text: T): T {
  console.log(text.length);
  return text;
}
```

- Also, we can restrict object property

```
function getProperty<T, O extends keyof T>(obj: T, key: O) {
  return obj[key];  
}
let obj = { a: 1, b: 2, c: 3 };

getProperty(obj, "a"); // okay
getProperty(obj, "z"); // error
```

### Type Inference (Predicates)

In TypeScript, there are several places where type inference is used to provide type information when there is no explicit type annotation. For example, in this code.

```
let x = 3;
// typeof x === "number"
```

**Best common type**

When a type inference is made from several expressions, the types of those expressions are used to calculate a “best common type”. For example,

```
let arr = [0, 1, null];
// let arr: (number | null)[];
```

### Type Assertion

In **Typescript**, Type assertion is a technique that informs the compiler about the type of a variable. Type assertion is similar to typecasting but it doesn’t reconstruct code. You can use type assertion to specify a value’s type and tell the compiler not to deduce it. When we want to change a variable from one type to another such as any to number etc, we use Type assertion.

### Type Guard

Type Guards allow you to narrow down the type of an object within a conditional block.

```
interface Developer {
  name: string;
  skill: string;
} 

interface Person {
  name: string;
  age: number;
}

// Type Guard
function isDeveloper(target: Developer | Person): target is Developer {
  return (target as Developer).skill !== undefined;
}

let brian = { name: 'brian', skill: 'SWE', age: 99};

if (isDeveloper(brian)) {
  console.log(brian.skill);
} else {
  console.log(brian.age);
}
```

### Type Compatibility

Type compatibility in TypeScript is based on structural subtyping. Structural typing is a way of relating types based solely on their members. This is in contrast with nominal typing.

```
interface Ironman {
  name: string;
}

class Avengers {
  name: string;
}

let i: Ironman;
i = new Avengers(); // OK, because of structural typing
```

- Type compatibility in interface

```
interface Developer {
  name: string;
  skill: string;
}  

interface Person {
  name: string;
}

var a: Developer;
var b: Person;

a = b; // Error
b = a; // Okay
```

- Type compatibility in function

```
var add = function(a: number) {}
var sum = function(a: number, b: number) {}

// sum = add; // ERROR
// add = sum; // O
```

- Type compatibility in generic

```
interface Empty<T> {}

let x: Empty<number>;
let y: Empty<string>;

x = y;  // OK, because y matches structure of x
```

```
interface NotEmpty<T> {
  data: T;
}
let x: NotEmpty<number>;
let y: NotEmpty<string>;

x = y;  // Error, because x and y are not compatible
```
