## console.log
💩💩💩💩💩💩💩💩

```js
	console.log(foo);
	console.log(bar);
	console.log(baz); // we don't have name of the variable in console
```

✅✅✅✅✅✅✅✅

```js
	console.log({ foo, bar, baz }); // {foo: {...}, bar: {...}, baz: {...}}
```

Computed property names:

```js 
	console.log('%c My Friends', 'color: orange; font-weight: bold');
	console.log({ foo, bar, baz }); 
```

Console.table(...):

```js
	console.table([foo, bar, baz]);
```

Если отслеживаете производительность, можно засекать время в консоли:

```js
	console.time('looper');

	let i = 0;
	while (i < 1000000) { i++ } // takes 4-5ms to loop 1mln times

	console.timeEnd('looper');
```

Отследить откуда возник console.log:

```js
	const deleteMe = () => console.trace('bye bye database');

	deleteMe();
	deleteMe();
```

![[console.trase.png]]

## destructuring
💩💩💩💩💩💩💩💩

```js
const turtle = {
	name: 'Bob',
	legs: 4, 
	shell: true,
	type: 'amphibious', 
	meal: 10,
	diet: 'berries'
}

function feed(animal) {
	return `Feed ${animal.name} ${animal.meal} kilos of ${animal.diet}`; // 'animal' repeat
}
```

✅✅✅✅✅✅✅✅

```js
function feed({ name, meal, diet }) {
	return `Feed ${name} ${meal} kilos of ${diet}`;
}
```
OR
```js
function feed(animal) {
	const { name, meal, diet} = animal;
	return `Feed ${name} ${meal} kilos of ${diet}`;
}
```

## template literals
💩💩💩💩💩💩💩💩

```js
const horse = {
	name: 'Topher', 
	size: 'large', 
	skills: ['jousting', 'racing'],
	age: 7
}

let bio = horse.name + ' is a ' + horse.size + ' horse skilled in ' + horse.skill;
```

✅✅✅✅✅✅✅✅

```js
const { name, size, skills } = horse;

bio = `${name} is a ${size} skilled in ${skills.join(' & ')`;
```
Advanced Tag Example:
```js
function horseAge(str, age) {
	const ageStr = age > 5 ? 'old' : 'young';
	return `${str[0]}${ageStr} at ${age} years`
}

const bio2 = horseAge`
	This horse is ${horse.age} 
`; // This horse is old at 7 years
```

## spread syntax
💩💩💩💩💩💩💩💩

```js
const pikachu = { name: 'Pikachu' };
const stats = { hp: 40, attack: 60, defense: 45 };

pikachu['hp'] = stats.hp;
pikachu['attack'] = stats.attack;
pikachu['defense'] = stats.defense;

// OR

const lvl0 = Object.assign(pikachu, stats);
const lvl1 = Object.assign(pikachu, { hp: 45 });
```

✅✅✅✅✅✅✅✅

```js
const lvl0 = { ...pikachu, ...stats };
const lvl1 = { ...pikachu, hp: 45 };
```

Arrays:
💩💩💩💩💩💩💩💩

```js
let pokemon = ['Arbok', 'Raichu', 'Sandshrew'];

pokemon.push('Bulbasaur');
pokemon.push('Metapod');
pokemon.push('Weedle');
```

✅✅✅✅✅✅✅✅

```js
pokemon = [...pokemon, 'Bulbasaur', 'Metapod', 'Weedle'];
//OR
pokemon = ['Bulbasaur', 'Metapod', 'Weedle', ...pokemon]; // like unshift
//OR 
pokemon = ['Bulbasaur', 'Metapod', ...pokemon, 'Weedle']; // like whatever
```

## loops
💩💩💩💩💩💩💩💩

```js
const orders = [500, 30, 99, 15, 223];

const total = 0;
const withTax = [];
const highValue = [];
for (i = 0; i < orders.length; i++) {
	// Reduce
	total += orders[i];
	
	// Map
	withTax.push(orders[i] * 1.1);
	
	// Filter 
	if (orders[i] > 100) {
		highValue.push(orders[i]);
	}
}
```

✅✅✅✅✅✅✅✅

```js
// Reduce
const total = orders.reduce((acc, cur) => acc + cur);

// Map
const withTax = orders.map(v => v * 1.1);

// Filter
const highValue = orders.filter(v => v > 100);
```

## async/await
💩💩💩💩💩💩💩💩

```js
const random = () => {
	return Promise.resolve(Math.random());
}

const sumRandomAsyncNums = () => {
	let first;
	let second;
	let third;
	
	return random()
		.then(v => {
			first = v;
			return random();
		})
		.then(v => {
			second = v;
			return random();
		})
		.then(v => {
			third = v;
			return first + second + third;
		})
}
```

✅✅✅✅✅✅✅✅

```js
const sumRandomAsyncNums = async() => {
	const first = await random();
	const second = await random();
	const third = await random();
	
	console.log(`Result ${first + second + third}`);
}
```


## variables naming
💩💩💩💩💩💩💩💩

```js
for (let i = 0; i < 86400; i++) {} // WTF is 86400 ??
```

✅✅✅✅✅✅✅✅

```js
const SECONDS_IN_A_DAY = 86400;

for (let i = 0; i < SECONDS_IN_A_DAY; i++) {}
```

## avoid large functions
💩💩💩💩💩💩💩💩

```js
const addMultiplySubtract = (a, b, c) => {
	const addition = a + b + c;
	const multiplication = a * b * c;
	const subtraction = a - b - c;
	
	return `${addition} ${multiplication} ${subtraction}`; 
	//yes it should be bigger, just an axample
}
```

✅✅✅✅✅✅✅✅

```js
const add = (a, b, c) => a + b + c;
const multiply = (a, b, c) => a * b * c;
const subtract = (a, b, c) => a - b - c;
```