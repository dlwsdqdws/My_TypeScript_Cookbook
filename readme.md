# My TypeScript Cookbook

- [My TypeScript Cookbook](#my-typescript-cookbook)
  - [Why TS](#why-ts)
  - [Variable Types](#variable-types)
    - [Basic Types](#basic-types)
    - [Array and Tuple](#array-and-tuple)
    - [Any and Union](#any-and-union)
    - [Enum](#enum)
  - [Object](#object)
    - [Function](#function)
    - [Class](#class)
    - [Interface](#interface)

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
  Up,
  Down,
}

enum Direction {
  Left = "LEFT",
  Right = "RIGHT",
  Up = "UP",
  Down = "DOWN",
}
```

## Object

### Function

1. Function declaration

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

2. Function expression

```ts
const add = function (x: number, y: number, z?: number): number {};

const add2: (x: number, y: number, z?: number) => number = add;
```

### Class

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
console.log(snake.run());

// Inheritance
class Dog extends Animal {
  bark() {
    return `${this.name} is barking`;
  }
}

const dog = new Dog("Greyhound");
console.log(dog.run());
console.log(dog.bark());

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

const cat = new Cat("Siamese");
console.log(cat.run());
```

Modifiers:

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
console.log(Animal.isAnimal(bird));
```

### Interface

1. Used to describe the shape of an object.

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

Note: When using an interface, all properties must have an **_exact_** match unless the property is marked with the "?" modifier.

2. Used to abstract a `class`.

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

