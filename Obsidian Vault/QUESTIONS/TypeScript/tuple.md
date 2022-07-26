Позволяет обозначить разные типы данных.

```ts
var empId: number = 1; 
var empName: string = "Steve";        

// TUPLE 👇
var employee: [number, string] = [1, "Steve"];
```

Больше примеров:

```ts
var employee: [number, string] = [1, "Steve"];
var person: [number, string, boolean] = [1, "Steve", true];

var user: [number, string, boolean, number, string]; // declare tuple variable
user = [1, "Steve", true, 20, "Admin"]; // initialize tuple variable
```

Массив tuple: 

```ts
var employee: [number, string][];
employee = [[1, "Steve"], [2, "Bill"], [3, "Jeff"]];
```

Можно добавить элементы:

```ts
var employee: [number, string] = [1, "Steve"];
employee.push(2, "Bill"); // valid for the "employee" typle 👍
console.log(employee); //Output: [1, 'Steve', 2, 'Bill']
```