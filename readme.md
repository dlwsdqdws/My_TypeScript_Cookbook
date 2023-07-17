# My TypeScript Cookbook

- [My TypeScript Cookbook](#my-typescript-cookbook)
  - [Why TS](#why-ts)
  - [Variable Types](#variable-types)
    - [Basic Types](#basic-types)
    - [Array and Tuple](#array-and-tuple)
    - [Any, Enum and Union](#any-enum-and-union)

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
let numbers : number[] = [1,2,3,4,5]
numbers.push(6)

// tuple
let user : [string, number] = ["Lei Lu", 1]

// array-like object
function test(){
    console.log(arguments.length);
    console.log(arguments[1]);

    arguments.forEach();        // wrong
    let arr: any[] = arguments; // wrong
}
```

### Any, Enum and Union
```ts
// any
let notSure : any = 3;
notSure = 'Now is a string';
notSure = false;

// union type
let numberOrString: number | string = 3;
numberOrString = 'Now is a string';

// enum
enum Direction {
    Left = 5,
    Right,  // default = 6
    Up, 
    Down,
}

enum Direction {
    Left = 'LEFT',
    Right = 'RIGHT',  
    Up = 'UP', 
    Down = 'DOWN',
}
```
