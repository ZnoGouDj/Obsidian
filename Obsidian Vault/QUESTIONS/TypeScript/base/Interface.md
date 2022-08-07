Сущность, которая помогает описать форму объекта или БУДУЩЕГО объекта. Похоже на абстрактный класс.

```ts
interface User {
	name: string,
	age: number,
}

type User {
	name: string, 
	age: number,
}
```

**TYPE** задает любую разновидность типа, включая примитивы. 
**INTERFACE** представляет именованный тип объекта и позволяет описывать сущности. Также можно с ним использовать **extends** или **implements**. То есть он может НАСЛЕДОВАТЬСЯ и РАСШИРЯТЬСЯ другими интерфейсами.

```ts
interface User {
	readonly name: string, // <--- Can't be changed
	age?: number, // <--- Optional
	dickSize: number, // <--- Required
	[propName: string]: any, // типы и количество других свойств могут быть произвольными
}
```

<p style="text-align: center; font-size: large; font-weight: bold;">Class & Interface</p>
```ts
interface User {
	name: string,
	age: number,
	getPass(): string,
}

class Egor implements User {
	name: string = 'Egor';
	age: number = 31;
	nickName: string = 'webDev'; // <--- Not in interface

	getPass() {
		return `${this.name}${this.age}`;
	}
}
```

Если в классе есть лишнее относительно интерфейса свойство (nickName in example), то ошибок нет. Интерфейс тут описывает именно хотя бы минимальный набор параметров, но их можно накидывать сверх. 

Также можно имплементить от **нескольких интерфейсов**:
```ts
interface User {
	name: string, 
	age: number,
}

interface Pass {
	getPass(): string,
}

class Egor implements User, Pass {
	name: string = 'Egor',
	age: number = 26,

	getPass() {
		return `${this.name}${this.age}`;
	}
}
```

**Либо можно сделать расширение интерфейсов:**

```ts
interface User {
	name: string,
	age: number,
}

interface Admin extends User {
	getPass(): string,
}

class Egor implements Admin {
...
}
```