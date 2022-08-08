```ts
// ES6 syntax
const getter = <T>(data: T): T => data; // may use any letter, but usually it's <T>

// ES5 syntax
function getter<T>(data: T): T {
	return data;
}
```

Распознает типы на лету:

```ts
const getter = <T>(data: T): T => data;

getter(10).length; // Property 'length' doesn't exist on type 'number'
getter('test').length; // 4
```

В классах:

```ts
class User<T> {
	constructor(public name: T, public age: T) {}

	public getPass(): string {
		return `${this.name}${this.age}`;
	}
}

const egor = new User('Egor', '26'); // string, string
const max = new User(123, 321); // number, number

egor.getPass(); 'Egor26'
max.getPass(); '123321' // на выходе преобразуется в строки
```

А если надо передать разные типы?

```ts
class User<T, K> {
	constructor(public name: T, public age: K) {}

	public getPass(): string {
		return `${this.name}${this.age}`;
	}
}

const leo = new User('Leo', 22); // string, number

let.getPass(); 'Leo22'
```

А если в некоторых методах нельзя все типы подряд принимать?!

```ts
class User<T, K extends number> { // <-- тогда задаем EXTENDS к нужному типу
	//...
	public getSecret(): number {
		return this.age**2; // <-- CAN'T be a string
	}
}
```