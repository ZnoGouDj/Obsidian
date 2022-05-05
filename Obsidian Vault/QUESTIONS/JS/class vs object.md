**Класс** — шаблон для объектов. Он определяет все методы, разные свойства, значения по умолчанию и тд. Но он не дает никакой информации или данных — это просто структура того, как будет выглядеть объект.

**Объект** — созданная версия класса. У него есть состояние, в котором содержатся введенные данные, либо те данные по умолчанию из класса.

```js
class Animal {
	static type = 'ANIMAL'; // static доступен только у самого класса
	//...
}

const animal = new Animal({
	name: 'Animal', 
	age: 5, 
	hasTail: true
})

console.log(Animal.type); // ANIMAL
console.log(animal.type); // undefined

```

Почему классы в принципе удобны? НАСЛЕДОВАНИЯ!

```js 
class Cat extends Animal {
	static type = 'CAT';
	
	constructor(options) { // расширяем конструктор (2)
		super(options); // вызываем конструктор Animal, передаем options (3)
		this.color= options.color; // добавляем нужное (4)
	}
	
	voice() {
		super.voice(); // а если вот так, то вывыедет оба по порядку (1.3)
		console.log('I am cat'); // метод в дочернем классе приоритетнее! (1.1)
	}
}

const cat = new Cat({
	name: 'Cat', 
	age: 7, 
	hasTail: true,
	color: 'black' // отсутствует в Animal, но нужен здесь (1)
})

console.log(cat.voice()); // I am cat (1.2)
```

getters/setters

```js
class Cat extends Animal {
	// ... the same
	get ageInfo() {
		return this.age * 7;
	}
	
	set ageInfo(newAge) {
		this.age = newAge;
	}
}

console.log(cat.ageInfo); // 49
// change the age with SETTER
cat.ageInfo = 8;
console.log(cat.ageInfo); // 56
```