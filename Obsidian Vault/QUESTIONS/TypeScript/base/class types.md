💩💩💩💩💩💩💩💩
```ts
class User {
	name: string;
	age: number;
	nickName: string = webdev; // *default val

	constructor(name: string, age: number, nickName: string) {
		this.name = name;
		this.age = age;
		this.nickName = nickName;
	}
}

const person = new User('Egor', 26, 'znogoud');
```

✅✅✅✅✅✅✅✅
```ts
// Краткая версия. Писать this.name = name и тд более не нужно.
// Но надо обязательно указать модификатор!
class User {
	constructor(
		public name: string,
		public age: number,
		public nickName: string,
		public pass: number
	) {}
}
```

### Приватные и публичные данные (private and public data):
Есть 4 модификатора доступа:

```ts
class User {
	public name: string;
	private nickName: string;
	protected age: number;
	readonly pass: number;

	constructor(name: string, age: number, nickName: string, pass: number) {
		this.name = name;
		this.age = age;
		this.nickName = nickName;
		this.pass = pass;
	}
}

const person = new User('Egor', 26, 'znogoud');

person.name; // 'Egor'
person.nickName; // Prop 'nickName' is private and only accessible within class 'User'
person.age; // protected and only accessible within class 'User' and its subclasses
person.pass = 42; // Cannot assign to 'pass' because it is a read-only prop
```

**public** - дефолтное значение, установлено везде где ничего не задано. свободный доступ.
**private** - недоступен за пределами класса. Ни классам-наследникам, ни объекты созданные с его помощью не получают доступ
**protected** - доступ могут получить только наследники. Экземпляры класса - не могут.
**readonly** - только для чтения
**static** - свойства которые видны без создания экземпляра класса

### Getters / setters
(геттеры и сеттеры)

Это специальный метод класса, который ведет себя как свойство снаружи этого класса, и служит либо для чтения, либо для установки значения внутри него.

```ts
class User {
	private age: number = 20;
	constructor(public name: string) {}
// изменять приватные свойства можем не только с помощью СЕТ, но и с помощью обычного метода
	setAge(age: number) {
		this.age = age;
	}

	set myAge(age: number) {
		this.age = age;
	}
}

const person = new User('Egor');

person.setAge(25); // 25
person.myAge(99999); // 99999
```

А ЗАЧЕМ ВООБЩЕ ИЗМЕНЯТЬ ПРИВАТНОЕ СВОЙСТВО?

В JS нет классов в классическом их понимании. Под капотом идут прототипы. И в разработке в ООП подходе возможно изменить что-то на верхнем уровне случайно. Поэтому напрямую свойства стараются не изменять, а использовать геттеры / сеттеры. Это дает больший контроль над объектами. А в ТайпСкрипт можно еще и навесить протекторов, чтобы сделать это все надежнее. 