```ts
// Array Type
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3]; // Generic type
```
[[tuple]]
```ts
// Tuple Type
// Multiple lines
let x: [string, number];
x = ['hello', 10];

// Single line
ley y: [string, number] = ['goodbye', 42];

// Error case
x = [10, 'hello']; // Type 'string' is not assignable to type 'number'

// если 100 элементов string, а 101 - number
const arr: Array<string|number> = ['str_1', ... , 'str_100', 101];
```

[[enum]]
[[type Never]]