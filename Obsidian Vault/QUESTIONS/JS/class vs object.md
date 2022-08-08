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
		this.color = options.color; // добавляем нужное (4)
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
Геттер — это метод, который получает значение свойства. 
Сеттер — это метод, который устанавливает значение свойства. 
Есть некоторые разногласия по поводу их эффективности, но в целом точки зрения таковы, что они кайфовые для:
1) полноты инкапсуляции (чтобы скрыть приватное поле от публичности (вы можете избежать прямого доступа к полю))
2) поддержки [согласованного интерфейса](https://stackoverflow.com/questions/812961/getters-setters-for-dummies#:~:text=%20setters%20can%20also%20be%20used%20to%20update%20other%20values.) в случае изменения внутренних деталей

Наиболее полезно, когда вам нужно например добавить валидацию перед установкой значения (чтобы число не было меньше нуля и тд)
