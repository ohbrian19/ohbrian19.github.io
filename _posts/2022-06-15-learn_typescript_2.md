---
layout: post
title:  "Learn TypeScript #2 2022-06-15"
---

### Interface
In **TypeScript**, an **interface** is an abstract type that tells the compiler which property names a given object can have.

For example,
```
let person = { name: 'Capt', age: 28 };

function logAge(obj: { age: number }) {
  console.log(obj.age); // 28
}
logAge(person); // 28
```
can be changed to 
```
interface personAge {
  age: number;
}

function logAge(obj: personAge) {
  console.log(obj.age);
}
let person = { name: 'Capt', age: 28 };
logAge(person);
```

 1. **Optional Property**
- When using the interface, using all declared properties is not necessary. This is called optional property.
```
interface CraftBeer {
  name: string;
  hop?: number;  
}

let myBeer = {
  name: 'Saporo'
};
function brewBeer(beer: CraftBeer) {
  console.log(beer.name); // Saporo
}
brewBeer(myBeer);
```
- Interfaces with optional properties are written similar to other interfaces, with each optional property denoted by a "**?**" at the end of the property name in the declaration.

 2. **Readonly Property**
