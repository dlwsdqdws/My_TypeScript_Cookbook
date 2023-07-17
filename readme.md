# My TypeScript Cookbook

- [My TypeScript Cookbook](#my-typescript-cookbook)
  - [Why TS](#why-ts)
  - [Variable Types](#variable-types)
    - [Basic Types](#basic-types)
    - [Array and Tuple](#array-and-tuple)
    - [Any and Union](#any-and-union)
    - [Enum](#enum)
  - [Function](#function)
    - [Function Declaration](#function-declaration)
    - [Function Expression](#function-expression)
  - [Object](#object)
    - [Class](#class)
      - [Object-oriented Programming](#object-oriented-programming)
      - [Modifiers](#modifiers)
    - [Interface](#interface)
      - [Shape Object](#shape-object)
      - [Abstract Class](#abstract-class)
      - [Describe Function](#describe-function)
  - [Generics](#generics)
    - [Placeholders For Types](#placeholders-for-types)
    - [Generic Constraints](#generic-constraints)
    - [Generic in Class](#generic-in-class)
    - [Generic in Interface](#generic-in-interface)
  - [File](#file)

## Why TS

- Stronger readability.
- Fewer errors.
- Higher inclusiveness.

## Variable Types

### Basic Types

```ts
let check: boolean = true;
let age: number = 10;
let binaryNumber: number = 0b101;
let firstName: string = "Lei";
let name: string = `My name is ${firstName}`;
let n: null = null;
let u: undefined = undefined;
let number: number = undefined;
```

Note: `undefined` typically represents absence or lack of definition, while `null` represents an explicitly assigned empty value.

### Array and Tuple

```ts
// array
let numbers: number[] = [1, 2, 3, 4, 5];
numbers.push(6);

// tuple
let user: [string, number] = ["Lei Lu", 1];

// array-like object
function test() {
  console.log(arguments.length);
  console.log(arguments[1]);

  arguments.forEach(); // wrong
  let arr: any[] = arguments; // wrong
}
```

### Any and Union

```ts
// any
let notSure: any = 3;
notSure = "Now is a string";
notSure = false;

// union type
let numberOrString: number | string = 3;
numberOrString = "Now is a string";
```

### Enum

```ts
// enum
enum Direction {
  Left = 5,
  Right, // default = 6
  Up, // default = 7
  Down, // default = 8
}

enum Direction {
  Left = "LEFT",
  Right = "RIGHT",
  Up = "UP",
  Down = "DOWN",
}
```

## Function

### Function Declaration

```ts
function add(x: number, y: number, z?: number): number {
  if (typeof z === "number") return x + y + z;
  return x + y;
}

let res1 = add(1, 2, 3);
let res2 = add(1, 2);
```

Note: Optional parameters can also be set with default values.

```ts
function add(x: number, y: number, z: number = 10): number {}
```

### Function Expression

```ts
const add = function (x: number, y: number, z?: number): number {};

const add2: (x: number, y: number, z?: number) => number = add;
```

## Object

### Class

#### Object-oriented Programming

```ts
// Encapsulation
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  run() {
    return `${this.name} is running`;
  }
}

const snake = new Animal("Cobra");
console.log(snake.run()); // Cobra is running

// Inheritance
class Dog extends Animal {
  bark() {
    return `${this.name} is barking`;
  }
}

const dog = new Dog("Greyhound");
console.log(dog.run()); // Greyhound is running
console.log(dog.bark()); // Greyhound is barking

// Polymorphism
class Cat extends Animal {
  constructor(name) {
    super(name);
    console.log(this.name);
  }

  run() {
    return "Meow, " + super.run();
  }
}

const cat = new Cat("Siamese"); // Siamese
console.log(cat.run()); // Siamese is running
```

#### Modifiers

1. In TypeScript, `public`, `private`, and `protected` are modifiers used to define the accessibility of class members.

- The `public` modifier indicates that a member can be accessed by **_instances of the class, subclasses, and external code_**. If no modifier is explicitly specified, the member is treated as public by default.
- The `private` modifier indicates that a member can only be accessed **_within the class itself_**. Private members cannot be accessed by instances of the class, subclasses, or external code.
- The `protected` modifier indicates that a member can be accessed **_within the class itself and its subclasses_**, but not by instances of the class or external code directly.

2. The `readonly` modifier indicates that a property can only be assigned a value once and cannot be modified afterwards.

3. The `static` modifier allows properties and methods to be accessed directly on the class itself, rather than through an instance of the class.

```ts
class Animal {
  static catagories: string[] = ["mammal", "bird"];
  static isAnimal(a) {
    return a instanceof Animal;
  }
}

let bird = new Animal("Pigeon");
console.log(Animal.catagories); // right
console.log(bird.catagories); // wrong, can only access static property directly on the class
console.log(Animal.isAnimal(bird)); // right
```

### Interface

Duck Typing: If an object or value has the required properties and methods needed for a particular operation or behavior, it can be treated as if it belongs to a specific type, regardless of its actual type.

#### Shape Object

```ts
interface IUser {
  readonly id: number;
  name: string;
  gender?: string;
}

let user: IUser = {
  id: 0,
  name: "Lei Lu",
};

user.id = 2; // wrong
```

Note: When using an interface, all properties must have an **_exact_** match unless the property is marked with the `?` modifier.

#### Abstract Class

```ts
interface IRadio {
  switchRadio(): void;
}

interface IRadioWithBattery extends IRadio {
  checkStatus();
}

class Car implements IRadio {
  switchRadio() {}
}

class Cellphone implements IRadioWithBattery {
  switchRadio() {}
  checkStatus() {}
}
```

#### Describe Function

```ts
interface IPlus {
  (a: number, b: number) : number
}

function plus: (a: number, b: number) : number {
  return a+b;
}

const newFun: IPlus = plus;
```

## Generics

### Placeholders For Types

Generics allows creating reusable code components that can work with different types.

```ts
function echo<T>(arg: T): T {
  return arg;
}

let str: string = echo("str");
let num: number = echo(123);

function swap<T, U>(tuple: [T, U]): [U, T] {
  return [tuple[1], tuple[0]];
}

let res: [number, string] = swap("string", 123);
```

### Generic Constraints

```ts
function echoWithArray<T>(arg: T[]): T[] {
  console.log(arg.length);
  return arg;
}

const args1 = echoWithArray([1, 2, 3]); // right
const args2 = echoWithArray("123"); // wrong

interface IWithLength {
  length: number;
}

function echoWithLength<T extends IWithLength>(arg: T): T {
  console.log(arg.length);
  return arg;
}

const arr = echoWithLength([1, 2, 3]); // right
const str = echoWithLength("123"); // right
const obj = echoWithLength({ length: 10, width: 10 }); // right
const num = echoWithLength(123); // wrong
```

### Generic in Class

```ts
class Queue<T> {
  private data = [];
  push(item: T) {
    return this.data.push(item);
  }
  pop(): T {
    return this.data.shift();
  }
}

let queue1 = new Queue<number>();
queue1.push(1);
console.log(queue1.pop().toFixed()); // 1

let queue2 = new Queue<string>();
queue2.push("123");
console.log(queue2.pop().length); // 3
```

### Generic in Interface

```ts
interface IKeyPair<T, U> {
  key: T;
  value: U;
}

let kp1: IKeyPair<number, string> = { key: 1, value: "str" };
let kp2: IKeyPair<string, number> = { key: "str", value: 1 };
```

Note:

1. Built-in interfaces can also use generics.

```ts
let arrNum: Array<number> = [1, 2, 3];
```

2. Interfaces also support generics for functions.

```ts
interface IPlus<T> {
  (a: T, b: T) : T
}

function plus: (a: number, b: number) : number {
  return a+b;
}

function connect: (a: string, b: string) : string {
  return a+b;
}

const fun1: IPlus<number> = plus;
const fun2: IPlus<string> = connect;
```

## File
