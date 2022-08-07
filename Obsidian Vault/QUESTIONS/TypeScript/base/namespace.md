Это отдельная сущность, которая напоминает объект.  Она инкапсулирует все добавленные в нее сущности и создает СВОЕ пространство имен, к которому можно обратиться.

Но есть нюанс. Если мы обратимся к какой нибудь константе как к обычному свойству объекта, то получим ошибку. И это основное отличие от объекта. 

```ts
namespace Utils {
	const SECRET: string = '123123';
	const PI: number = 3.14;

	const getPass = (name: string, age: number): string => `${name}${age}`;

	const isEmpty = <T>(data: T): boolean => !data;
}

const myPass = Utils.getPass('Egor', 26); //prop 'getPass' doesn't exist on type 'typeof Utils'
```

Чтобы получить доступ, надо экспортировать данные

```ts
namespace Utils {
	export const SECRET: string = '123123';
	const PI: number = 3.14;

	export const getPass = (name: string, age: number): string => `${name}${age}`;

	export const isEmpty = <T>(data: T): boolean => !data;
}

const myPass = Utils.getPass('Egor', 26); // 'Egor26'
const PI = 3; // no errors -> can't see PI in the Utils
```