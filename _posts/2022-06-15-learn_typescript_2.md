---
layout: post
title:  "Learn TypeScript #2 2022-06-15"
---

This is my journey to learn **TypeScript** part 2.

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
- **TypeScript** includes the _readonly_ keyword that makes a property as read-only in the class, type or interface.
- Read-only members can be accessed outside the class, but their value cannot be changed. Since read-only members cannot be changed outside the class, they either need to be initialized at declaration or initialized inside the class constructor.

```
interface CraftBeer {
  readonly brand: string;
}
```

```
let myBeer: CraftBeer = {
  brand: 'Belgian Monk'
};
myBeer.brand = 'Korean Carpenter'; // error!
```

 3. **Function Type**

```
let loginUser: login;
loginUser = function(id: string, pw: string) {
  console.log('user login');
  return true;
}
```

4. **Class Type**

```
interface CraftBeer {
  beerName: string;
  nameBeer(beer: string): void;
}

class myBeer implements CraftBeer {
  beerName: string = 'Baby Guinness';
  nameBeer(b: string) {
    this.beerName = b;
  }
  constructor() {}
}
```

5. **Interface inheritance**

```
interface Person {
  name: string;
}
interface Developer extends Person {
  skill: string;
}
let fe = {} as Developer;
fe.name = 'josh';
fe.skill = 'TypeScript';
```

### Usage
1. **Indexing**

```
interface StringArray {
  [index: number]: string;
}

const arr: StringArray = ['Thor', 'Hulk'];
arr[0]; // 'Thor'
```

```
interface ReadonlyStringArray {
  readonly [index: number]: string;
}

const arr: ReadonlyStringArray = ['Thor', 'Hulk'];
arr[2] = 'Capt'; // Error!
```

2.  **Dictionary Pattern**

```
interface StringRegexDictionary {
  [key: string]: RegExp;
}

var obj: StringRegexDictionary = {
  sth: /abc/
}
```

### Enum

*Enums* or enumerations are a new data type supported in **TypeScript**. *Enums* allow us to declare a set of named constants i.e. a collection of related values that can be numeric or string values. There are three types of *enums*.

*1. Numeric enum*

```
enum Direction {
  Up = 1,
  Down,
  Left,
  Right
}
```
- Default value is 0 when no value is assigned.
- It is incremented by 1 going downwards.

*2. String enum*

```
enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT",
}
```

*3. Heterogeneous enum*

```
enum BooleanLikeHeterogeneousEnum {
    No = 0,
    Yes = "YES",
}
```

### Class

- *readonly*

```
class Developer {
    readonly name: string;
    constructor(theName: string) {
        this.name = theName;
    }
}
let john = new Developer("John");
john.name = "John"; // error! name is readonly.
```

- **Abstract class**
Abstract classes are mainly for inheritance where other classes may derive from them. We cannot create an instance of an abstract class.

```
abstract class Developer {
  abstract coding(): void; // 'abstract'가 붙으면 상속 받은 클래스에서 무조건 구현해야 함
  drink(): void {
    console.log('drink sth');
  }
}

class FrontEndDeveloper extends Developer {
  coding(): void {
    // Developer 클래스를 상속 받은 클래스에서 무조건 정의해야 하는 메서드
    console.log('develop web');
  }
  design(): void {
    console.log('design web');
  }
}
const dev = new Developer(); // error: cannot create an instance of an abstract class
const josh = new FrontEndDeveloper();
josh.coding(); // develop web
josh.drink(); // drink sth
josh.design(); // design web
```
