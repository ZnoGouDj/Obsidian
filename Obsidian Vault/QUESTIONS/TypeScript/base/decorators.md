Можно сказать что декораторы ОБОРАЧИВАЮТ декорируемую сущность и изменяют ее поведение. 

**ИДЕЯ ТАКАЯ:**
Мы можем обернуть функцией другую функцию, класс или объект. Эта обертка вызовет то что внутри нее с теми же параметрами, как если бы обертки не было. То есть ни функция, ни вызывающий ее код не почувствуют разницы. ЗАЧЕМ ЭТО НУЖНО?! 
**Во-первых**, можно обернуть уже обернутую в другую обертку (емае) функцию, сделать это сколько угодно раз и по идее ничего не сломается.
**Во-вторых**, можно гибко добавлять такие обертки хоть в рантайме и код отработает также.

Эта идея реализуется в разных крутых штуках и имеет много названий: [[HOC]] в React, [[Middleware]] в Node.js и получется **Декораторы** в TypeScript 

Если оберток много, может произойти callback-hell, поэтому используют различные функции-комбинаторы, в которую первым аргументом передают массив декораторов, а вторым функцию, которую надо этим всем обернуть. А комбинатор уже внутри проходится по массиву и поочередно все оборачивает. 
TypeScript же пошел далее и создал специальный синтаксис: когда компилятор встречает @, то он ищет функцию с именем, указанным после @, оборачивает в нее то, что следующей строкой: передает в нее соответствующие аргументы и обеспечивает вызов обернутой функции со всеми аргументами вызова после отработки обертки, при условии, что из нее вернулся undefined.

**4 основных типа декораторов:**
<p style="text-align: center; font-weight: bold;">Класса</p>
```ts
// Class Decorator
const logClass = (constructor: Function) => {
	console.log(constructor); // => class User {}
}

@logClass // <-- Apply decorator for the following class
class User {
	constructor(public name: string, public age: number) {}

	public getPass(): string {
		return `${this.name}${this.age}`;
	}
}
```
<p style="text-align: center; font-weight: bold;">Свойства</p>
Принимает два аргумента: таргет (прототип класса) и проперти кей (имя поля, к которому применяется декоратор)
```ts
// Prop decorator
const logProperty = (target: Object, propertyKey: string | symbol) => {
	console.log(propertyKey); // => 'secret'
}

class User {
	@logProperty // <-- Apply decorator for prop
	secret: number;

	constructor(public name: string, public age: number, secret: number) {
		this.secret = secret;
	}

	public getPass(): string {
		return `${this.name}${this.age}`;
	}
}
```
<p style="text-align: center; font-weight: bold;">Метода</p>
Принимает два аргумента: таргет (прототип класса), проперти кей (имя метода) и дескриптор со специальным типом, и возвращает либо NULL, либо ДЕСКРИПТОР
```ts
// Method Decorator
const logMethod = (
	target: Object,
	propertyKey: string | symbol,
	descriptor: PropertyDescriptor
) => {
	console.log(propertyKey); // => 'getPass'
}

class User {
	constructor(public name: string, public age: number) {}

	@logMethod
	public getPass(): string {
		return `${this.name}${this.age}`;
	}
}
```
<p style="text-align: center; font-weight: bold;">Аксессора</p>
Принимает такие же аргументы, как метод, и возвращает либо NULL, либо ДЕСКРИПТОР
```ts
//...
class User {
	@logSet 
	set MyAge(age: number) {
		this.age = age;
	}
}
```

## Композиция декораторов
```ts
// Decorator composition syntax
// Apply decorators (one line)
@f @g x

// Apply decorators (multiple lines)
@f
@g
x
```

Сначала выражение для каждого декоратора вычисляется СВЕРХУ-ВНИЗ, затем результаты вызываются как функции СНИЗУ-ВВЕРХ

```ts
const first = () => {
	console.log('first() completing');
	return (target: any, propKey: string | symbol, descriptor: PropertyDescriptor) => {
		console.log('first() called');
	};
}

const second = () => {
	console.log('second() completing');
	return (target: any, propKey: string | symbol, descriptor: PropertyDescriptor) => {
		console.log('second() called');
	}
}

class User {
//..

	@first()
	@second()
	public getPass(): string {
		return `${this.name}${this.age}`;
	}
}

// Call results;
// "first() completing"
// "second() completing"
// "second() called"
// "first() called"
```

## Фабрика декораторов (Factory Decorator)
Это функция, которая возвращает выражение, и которая будет вызвана декоратором во время исполнения программы.  
Вместо того, чтобы создать декоратор, мы просто создаем обертку над ним в виде функции:
```ts
function factory(value: any) {           // Factory
	return function (target: any) {      // Decorator
		console.log(target);             // Decorator logic
	}
}
```