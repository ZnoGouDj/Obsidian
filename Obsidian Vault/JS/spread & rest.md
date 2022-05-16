**rest** позволяет собирать "оставшиеся" параметры и сделать из них массив.

```js
function showName(firstName, lastName, ...titles) { 
	alert( firstName + ' ' + lastName ); // Юлий Цезарь 
	// Оставшиеся параметры пойдут в массив 
	// titles = ["Консул", "Император"] 
	alert( titles[0] ); // Консул 
	alert( titles[1] ); // Император 
	alert( titles.length ); // 2 
}
```
 
`...rest` должен всегда быть последним.

*Зачем, если есть arguments?*
1) arguments - псевдомассив (без методов)
2) arguments берет в себя вообще все аргументы, rest - только те, которые не "заняты" перед ним



 **spread** «расширяет» перебираемый объект `arr` в список аргументов, и с помощью него можно вставить массив в функцию, которая по умолчанию работает с обычным списком аргументов.
 
 ```js
let arr = [3, 5, 1]; 
alert( Math.max(arr) ); // NaN
alert( Math.max(...arr) ); // 5 (оператор "раскрывает" массив в список аргументов)
```

Также можно:
1) копировать массив

```js
const fruits = ['🍏','🍊','🍌','🍉','🍍']

const moreFruits = [...fruits]; // Array(5) [ "🍏", "🍊", "🍌", "🍉", "🍍" ]
```

2) соединять массивы 

```js
console.log(...[...fruits, '...', ...moreFruits]) // 🍑 🍊 🍌 🍉 🍍 ... 🍏 🍊 🍌 🍉 🍍
```

3) использовать Math функции

```js
const numbers = [37, -17, 7, 0]

console.log(Math.min(numbers)) // NaN

console.log(Math.min(...numbers)) // -17

console.log(Math.max(...numbers)) // 37
```

4) использовать массив как аргументы

```js
const fruitStand = ['🍏','🍊','🍌']

const sellFruit = (f1, f2, f3) => { console.log(`Fruits for sale: ${f1}, ${f2}, ${f3}`) }

sellFruit(...fruitStand) // Fruits for sale: 🍏, 🍊, 🍌
```

5) добавить элемент в список

```js
const fewFruit = ['🍏','🍊','🍌']

const fewMoreFruit = ['🍉', '🍍', ...fewFruit]

console.log(fewMoreFruit) // Array(5) [ "🍉", "🍍", "🍏", "🍊", "🍌" ]
```

6) добавить к Стейту в Реакт

```js
function App() {
	const [searches, setSearches] = useState([])
	const [query, setQuery] = useState("")

	const handleClick = () => {
		setSearches(searches => [...searches, query])
	}
```

7) комбинирование объектов

```js
const objectOne = {hello: "🤪"}
const objectTwo = {world: "🐻"}
const objectThree = {...objectOne, ...objectTwo, laugh: "😂"}
console.log(objectThree) // Object { hello: "🤪", world: "🐻", laugh: "😂" }

const objectFour = {...objectOne, ...objectTwo, laugh: () => {console.log("😂".repeat(5))}}
objectFour.laugh() // 😂😂😂😂😂
```

8) конвертирование NodeList в массив

```js
[...document.querySelectorAll('div')]
```