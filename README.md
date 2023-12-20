# TypeScript Tutorial

## Getting Started

install compiler
`$ npm install typescript --save-dev`

show list of common commands
`$ npx tsc`

## configure the compiler
create 'tsconfig.json'

`$ npm tsc --init`

add to tsconfig.json
```json
{
  "include": ["src"],
  "compilerOptions": {
    "outDir": "./build"
  }
}
```

## Type Assignment
### Simple Types
- `boolean` - true or false values
- `number` - whole numbers and floating point values
- `string` - text values like "TypeScript Rocks"
- `bigint` - whole numbers and floating point values, but allows larger negative and positive numbers than the number type.
- `symbol` are used to create a globally unique identifier.

### Special Types
- `any` - a type that disables type checking and effectively allows all types to be used.
- `unknown` - TypeScript will prevent unknown types from being used
- `never` - effectively throws an error whenever it is defined
- `undefined` and `null` - types that refer to the JavaScript primitives undefined and null respectively.

### Arrays
```ts
const names: string[] = [];
names.push("Dylan"); // no error
// names.push(3); // Error: Argument of type 'number' is not assignable to parameter of type 'string'.

const names: readonly string[] = ["Dylan"];
names.push("Jack"); // Error: Property 'push' does not exist on type 'readonly string[]'.
// try removing the readonly modifier and see if it works?

const numbers = [1, 2, 3]; // inferred to type number[]
numbers.push(4); // no error
numbers.push("2"); // Error: Argument of type 'string' is not assignable to parameter of type 'number'.
```

### Tuples
a typed array with **a pre-defined length and types** for each index
```ts
let ourTuple: [number, boolean, string];

// initialize correctly
ourTuple = [5, false, 'Coding God was here'];
// initialized incorrectly which throws an error
ourTuple = [false, 'Coding God was mistaken', 5];

// Named Tuple
const graph: [x: number, y: number] = [55.2, 41.3];
const [x, y] = graph;
```

### Object Types
```ts
const car: { type: string, model: string, year: number } = {
  type: "Toyota",
  model: "Corolla",
  year: 2009
};

// Null Safety
// Error: Property 'mileage' is missing in type '{ type: string; }' .
const car: { type: string, mileage: number } = {
  type: "Toyota",
};
const car: { type: string, mileage?: number } = { // no error
  type: "Toyota"
};

// Index Signiture
const nameAgeMap: { [index: string]: number } = {};
nameAgeMap.Jack = 25;
```

### Enums
represents a group of constants
```ts
enum CardinalDirections {
  North,
  East,
  South,
  West
}
let currentDirection = CardinalDirections.North;
console.log(currentDirection);

enum StatusCodes {
  NotFound = 404,
  Success = 200,
  Accepted = 202,
  BadRequest = 400
}
console.log(StatusCodes.NotFound); // logs 404
console.log(StatusCodes.Success); // logs 200
```

### Type Aliases
```ts
type CarYear = number
type CarType = string
type CarModel = string
type Car = {
    year: CarYear,
    type: CarType,
    model: CarModel
}

const carYear: CarYear = 2001
const carType: CarType = "Toyota"
const carModel: CarModel = "Corolla"
const car: Car = {
  year: carYear,
  type: carType,
  model: carModel
};
```

### Interface
```ts
interface Rectangle {
    height: number,
    width: number
}
const rectangle: Rectangle = {
    height: 20,
    width: 10
}
```

### Union Types
```ts
function printStatusCode(code: string | number) {
  console.log(`My status code is ${code}.`)
}
printStatusCode(404);
printStatusCode('404');
```

### Function
```ts
// Optional Parameter
function add(a: number, b: number, c?: number) {
  return a + b + (c || 0);
}

// Default Parameters
function pow(value: number, exponent: number = 10) {
  return value ** exponent;
}

// Named Parameters
function divide({ dividend, divisor }: { dividend: number, divisor: number }) {
  return dividend / divisor;
}

// Type Alias
type Negate = (value: number) => number;
const negateFunction: Negate = (value) => value * -1;
```

### Partial
https://zenn.dev/tommykw/articles/d7ce0b4efdabc4
```ts
type Person = {
  name: string
  age: number
  location: string
}

function updatePerson(person: Partial<Person>) {
  // 更新処理
}

updatePerson({ name: 'tommykw' }) // Partial changes all the properties in an object to be optional
```

### Required
```ts
interface Car {
  make: string;
  model: string;
  mileage?: number;
}

let myCar: Required<Car> = {
  make: 'Ford',
  model: 'Focus',
  mileage: 12000 // `Required`
};
```

