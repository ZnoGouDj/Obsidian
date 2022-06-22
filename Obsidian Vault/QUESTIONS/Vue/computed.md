(как работают эти свойства)

Позволяет закешировать результат каких-то вычислений, и он будет вычисляться вновь только в том случае, если изменилась какая-то модель внутри COMPUTED свойства.

<p style="text-align: center; font-weight: bold; font-size: xx-large;">ПРИМЕР</p>

Допустим есть счетчик, кнопка которая его увеличивает, есть блок с количеством элементов в массиве и кнопка, добавляющая что-то в этот массив. 

```html
<div>
	<h1>Counter = {{ counter }}</h1>
	<button @click="counter++">Increase</button>
	
	<h1>Array length = {{ list.length }}</h1>
	<button @click="list.push(list.length + 1)">Add to array</button>
	
	<div :key="item" v-for="item in list">{{ item }}</div>
</div>
```

И допустим мы захотели выводить в **h1** УДВОЕННУЮ длину массива:

```js
export default {
	data() {
		return {
			counter: 0,
			list: [1, 2]
		}
	},
	methods: {
		doubleLength() { // и создаем ф-ю, которая умножает на два
			console.log('CALL')
			return this.list.length * 2
		}
	}
}
```
контент h1 также поменяем на:
```html
<h1>Array length = {{ doubleLength() }}</h1>
```

Оно действительно выведет удвоенное значение, НО при клике на <button>Increase</button>в консоль будет выводиться 'CALL', хотя при этом кол-во элементов массива оставалось прежним

Так что теперь мы делаем по-другому, чтобы ф-я вызывалась только при изменении длины массива. Просто меняем 'methods' на 'computed':
```js
	computed: { // <=====
		doubleLength() { // и создаем ф-ю, которая умножает на два
			console.log('CALL')
			return this.list.length * 2
		}
	}
```
И в h1 убираем круглые скобки в **doubleLength**:
```html
<h1>Array length = {{ doubleLength }}</h1>
```

Теперь все работает как надо, **this.list** является такой зависимостью для изменения.