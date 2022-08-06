(наследование в typescript)

```ts
class User {
	constructor(public name: string, public age: number) {}
}
```
Свойства с **public** появятся в классе после его инициализации. 
Но мы также можем создавать **static** свойства, которые видны и без создания экземпляра.
Это будет ОБЩЕЕ значение для всех объектов. 

```ts 
class User {
	static secret = 12345;
	constructor(public name: string, public age: number) {}

	getPass(): string {
		return `${this.name}${User.secret}`;
	}
}

const user = new User('Egor', 26);
user.getPass(); // 'Egor12345'

// we may JUST CALL static prop by:
User.secret // without ()
```

<p style="text-align: center; font-size: x-large; font-weight: bold;">Теперь к наследованию</p>
```ts
class Egor extends User {
	name: string = 'Egor';
}

const max = new User('Max', 20);
const egor = new Egor(26); // Expected 2 args, but got 1
// to solve this problem we should create new CONSTRUCTOR()

class Egor extends User {
	name: string = 'Egor';

	constructor(age: number) {
		super(name, age);
	}
}
```

<p style="text-align: center; font-size: x-large; font-weight: bold;">Abstract Class</p>
```ts
abstract class User {
	constructor(public name: string, public age: number) {}

	greet(): void {
		console.log(this.name);
	}

	abstract getPass(): string;
}

const max = new User('Max', 20); // Cannot create an instance of an abstract class
```
В нативном JS "создать абстракцию" значит просто создать новый класс по сути, но в TS это отдельная сущность. Абстрактные классы - это классы, от которых наследуются другие. 

Он имеет две основные особенности:
1) содержит детали реализации своих элементов (то есть свойств и методов)
2) от этого типа класса нельзя создать экземпляр, он используется ТОЛЬКО для создания наследников

Сам по себе абстрактный класс это что-то вроде интерфейса, который описывает как должны выглядеть потомки.

```ts
class Egor extends User {
	name: string = 'Egor';

	constructor(age: number) {
		super(name, age);
	}
} // error: Non-abstract class "Egor" doesn't implement inherited abstract member 'getPass' from class 'User'

// Need to implement abstract method

class Egor extends User {
	name: string = 'Egor';

	constructor(age: number) {
		super(name, age);
	}

	getPass(): string {
		return `${this.age}${this.name}`;
	}
} // now no errors
```