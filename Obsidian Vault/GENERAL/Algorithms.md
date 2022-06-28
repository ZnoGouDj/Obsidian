(Алгоритмы)

Это набор последовательных действий, решающий какую-то задачу. 
В принципе любой фрагмент кода можно назвать алгоритмом. 

[Big O Notation](#big_o_notation)
[Linear Search](#linear_search)
[Binary Search](#binary_search)
[Selection Sort](#selection_sort)
[Bubble Sort](#bubble_sort)
[Quick Sort](#quick_sort)
[Breadth-first search](#breadth_first_search)
[Tree Count Algorithm](#tree_algorithm)
[Caching Function](#caching_function)


### BIG_O_NOTATION ###
Скорость работы алгоритма описывается с помощью **большого О()**.
В скобках указывается количество операций, за которое этот алгоритм приходит к финальному результату. Причем указывается всегда НАИХУДШИЙ сценарий.

Одни алгоритмы эффективнее других, причем эффективность не всегда равна скорости работы алгоритма, поскольку в некоторых ситуациях более медленный алгоритм может оказаться на определенной выборке данных более эффективным. 

![[big-o-notation.png]]

На рисунке - основные примеры функций, которыми описывается сложность алгоритмов.
По оси X - количество операций. По оси Y - время.

<p style="text-align: center; font-size: large; font-weight: bold;">Example</p>

Допустим нам нужно найти конкретный элемент в массиве.

ОДИН из подходящих алгоритмов - **линейный поиск**:

### Linear_search ###
Мы начинаем с первого элемента и сравниваем каждый элемент с нужным.
В лучшем случае мы найдем элемент за 1 операцию, если он находится в списке первым.
В худшем - элемент будет в самом конце списка. И нам нужно будет обойти весь массив. 

```js
const arr = [7, 6, 1, 4, 0, 2, 3, 5, 8, 5]

function linearSearch(arr, item) {
	for (let i = 0; i < arr.length; i++) {
		if (arr[i] === item) {
			return i;
		}
	}
	return null;
}
```

Оценка сложности производится по худшему сценарию. Поэтому сложность данного алгоритма будет O(n), где n - количество элементов в массиве. 

ДРУГОЙ подходящий алгоритм - **бинарный поиск**:

### Binary_search ###
Он работает в разы быстрее, но подразумевается что массив отсортирован.
**Пример с телефонной книгой из CS50** (открываем посередине, отрываем ненужное, повторить до нахождения)
Таким образом, с каждым шагом мы отсеиваем ПОЛОВИНУ ненужных результатов. 

```js
const arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

function binarySearch(arr, item) {
	let start = 0;
	let end = arr.length;
	let middle;
	let found = false;
	let position = -1;
	
	while(found === false && start <= end) {
		middle = Math.floor((start + end) / 2);
		if (arr[middle] === item) {
			found = true;
			position = middle;
			return position;
		}
		if (item < arr[middle]) {
			end = middle - 1;
		} else {
			start = middle + 1;
		}
	}
	return position;
}
```
BONUS - recursive binary search:
```js
function recursiveBinarySearch(array, item, start, end) {
	let middle = Math.floor((start + end) / 2);
 	if (item === array[middle]) {
		return middle;
	}
	if (item < array[middle]) {
		return recursiveBinarySearch(array, item, start, middle - 1);
	} else {
		return recursiveBinarySearch(array, item, middle + 1, end);
	}
}
```

Сложность такого алгоритма - O(log2n) или О большое от логарифм N по основанию 2. 
Логарифм - обратная возведению в степень функция. 

Теперь если сравнивать эти алгоритмы, то получим:
<div style="display: flex; justify-content: center;">
<table border="1">
<tbody style="text-align: right;">
<tr>
<td></td>
<td>Линейный</td>
<td>Бинарный</td>
</tr>
<tr>
<td>100 элементов</td>
<td>100 мс</td>
<td>7 мс</td>
</tr>
<tr>
<td>10 000 элементов</td>
<td>10 сек</td>
<td>14 мс</td>
</tr>
<tr>
<td>1 000 000 элементов</td>
<td>11 дней</td>
<td>32 мс</td>
</tr>
</tbody>
</table>
</div>

Но важно понимать, что бинарный алгоритм работает только с отсортированным списком! 
И в несортированном массиве мы ничего не найдем. 
И сортировать перед поиском тоже не имеет смысла, поскольку время сортировки ГОРАЗДО длительнее, чем время работы линейного поиска. 

### Selection_Sort ###
(Сортировка выбором)

Есть массив неупорядоченных элементов.
Мы находим МИНИМАЛЬНЫЙ и меняем местами с 1м элементом. 
Затем снова находим ДРУГОЙ МИНИМАЛЬНЫЙ и меняем местами со 2м элементом (и тд)

```js
function selectionSort(array) {
	for (let i = 0; i < array.length; i++) {
		let indexMin = i;
		for (let j = i + 1; j < array.length; j++) {
			if (array[i] < array[indexMin]) {
				indexMin = j;
			}
		}
		let tmp = array[i];
		array[i] = array[indexMin];
		array[indexMin] = tmp;
	}
	return array;
}
```

Сложность - O(n*n)

### Bubble_Sort ###
(Сортировка пузырьком)

Очень известный и очень неэффективный лол.

Принцип - пробегаемся по всему массиву и сравниваем попарно лежащие элементы. 
Если следующий элемент массива меньше, чем предыдущий - меняем местами. 
И получается такое "всплытие" - самый БОЛЬШОЙ элемент с каждой итерацией потихоньку всплывает наверх. 

```js
function bubbleSort(array) {
	for (let i = 0; i < array.length; i++) {
		for (let j = 0; j < array.length; j++) {
			if (array[j + 1] < array[j]) {
				let tmp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = tmp;
			}
		}
	}
	return array;
}
```
```js
// mine
function bubbleSort(array) {
	let isSorted = false;
	let switchQty = 0;
	while (!isSorted) {
		let switchQtyHere = switchQty;
		for (let i = 0; i < array.length; i++) {
			if (array[i] > array[i + 1]) {
				let tmp = array[i];
				array[i] = array[i + 1];
				array[i + 1] = tmp;
				switchQtyHere++;
			}
		}
		if (switchQtyHere === switchQty) isSorted = true;
		switchQty = switchQtyHere;
	}
	return array;
}
```
Сложность - O(n*n)

### Quick_Sort ###
(Быстрая сортировка)

Один из самых эффективных
Сложность O(log2n * n) или О большое от логарифм по основанию 2 от N умноженное на N.

Если сравнивать скорость:
<div style="display: flex; justify-content: center;">
<table border="1">
<tbody style="text-align: right;">
<tr>
<td></td>
<td>O(log2n * n)</td>
<td>O(n*n)</td>
</tr>
<tr>
<td>n = 128</td>
<td>0.6 секунд</td>
<td>16 секунд</td>
</tr>
<tr>
<td>n = 1024</td>
<td>10 секунд</td>
<td>17 минут</td>
</tr>
</tbody>
</table>
</div>
Одна операция условно за 1мс.

Работает по принципу "РАЗДЕЛЯЙ И ВЛАСТВУЙ". 
Мы разделяем массив на подмассивы. 
И каждый раз рекурсивно мы выбираем опорный элемент каждого массива (можно случайный, но чаще всего берут центрально)
Пробегаемся по массиву, и все элементы, которые по значению меньше, чем ОПОРНЫЙ, добавляем в ОДИН МАССИВ, которые больше - В ДРУГОЙ МАССИВ.
Получаем два массива - с меньшими и большими, чем опорное число. 
Затем для каждого из этих массивов выполняется такая же операция. 
И это продолжается до тех пор, пока длина массива не будет === 1.
Затем останется только СКЛЕИТЬ массивы-малютки в один большой массив. 

```js
function quickSort(array) {
	if (array.length <= 1) {
		return array;
	}
	let currentIndex = Math.floor(array.length / 2); // currentIndex - опорный элемент
	let current = array[currentIndex];
	let less = [];
	let greater = [];
	for (let i = 0; i < array.length; i++) {
		if (i === currentIndex) continue;
		if (array[i] < current) {
			less.push(array[i]);
		} else {
			greater.push(array[i]);
		}
	}
	return [...quickSort(less), current, ...quickSort(greater)]
}
```

### Breadth_first_search ###
Поиск в ширину. ГРАФЫ.

Граф - абстрактная структура данных, представляющая собой множество вершин и набор ребер (соединения между парами вершин). 
То есть это (например) КАРТА, на которой есть города и города соединены маршрутами.
Маршруты тогда получаются ребра, а города - вершины. 

Ребра бывают однонаправленными и двунаправленными, то есть из точки А можно попасть в точку Б и наоборот. 

*но сейчас будем считать что однонаправленные, и обратно возвращаться мы не можем*
И будем разбирать задачу - определить кратчайший путь из А в Б, если таковой имеется. 

```js
const graph = {}
// в коде граф выражается так
// создается объект, поля которого - вершины
// и каждое поле равняется массиву вершин, в которые есть ПУТЬ 
graph.a = ['b', 'c']; // то есть из А мы имеем путь в Б и С
graph.b = ['f']; // из Б имеем путь в Ф и т.д.
graph.c = ['d', 'e'];
graph.d = ['f'];
graph.e = ['f'];
graph.f = ['g'];
```

В этом алгоритме будет использоваться структура данных ОЧЕРЕДЬ

```js
function breadthSearch(graph, start, end) {
	let queue = [];
	queue.push(start);
	while (queue.length > 0) {
		const current = queue.shift();
		if (!graph[current]) {
			graph[current] = []
		}
		if (graph[current].includes(end)) {
			return true;
		} else {
			queue = [...queue, ...graph[current]]
		}
	}
	return false;
}
```

Также граф можно представить в виде матрицы смежности, составляется ТАБЛИЧКА, где столбцы и строчки - это вершины. И если путь из одной вершины в другую есть, то на их перекрестии ставится 1, если пути нет - 0. 

```js
const matrix = [ // Граф выше может быть представлен такой матрицей
	[0, 1, 1, 0, 0, 0, 0],
	[0, 0, 0, 0, 1, 0, 0],
	[0, 0, 0, 1, 0, 1, 0],
	[0, 0, 0, 0, 1, 0, 0],
	[0, 0, 0, 0, 0, 0, 1],
	[0, 0, 0, 0, 1, 0, 0],
	[0, 0, 0, 0, 0, 0, 0]
]
```
Теперь реализуем алгоритм Дейкстры (Dijkstra's algorithm) для поиска кратчайшего пути:

![[Dijkstra's algorithm.png]]

В поиске в ширину мы проходим по вершинам графа и не важно, длительный он или нет
Главное - кол-во пройденных участков 
НО в алгоритме ДЕЙКСТРЫ учитывается длина пройденного ребра, т.н. ВЕС лол

За стартовую точку принимаем А, за конечную G
Составляется табличка, в которую на первом этапе записываются значения ТЕХ вершин, в которые мы МОЖЕМ попасть из стартовой точки
Все остальные вершины являются недостижимыми и мы их помечаем знаком Infinity

На втором этапе мы помечаем эти вершины как уже РАССМОТРЕННЫЕ 
На третьем этапе мы рассматриваем вершины, в которые мы можем попасть из точек B и С, и в таблицу записываем значения от точки А до точек, которые мы достигаем из вершин B и С
ОПЯТЬ помечаем эти точки как уже рассмотренные 

На следующем этапе мы достигаем точки G, НО у нас происходит ПЕРЕРАСЧЕТ -- мы находим путь до точки F, который оказывается КОРОЧЕ, и перезаписываем значение в таблице

И на следующем этапе мы проделываем все то же самое и находим оптимальный путь и узнаем, что из точки А в точку G можно добраться за 5 условных единиц

Реализация:
```js
const graph = {}
// теперь вершины не массивы, а объекты с расстоянием между 2х вершин
graph.a = {b: 2, c: 1}; 
graph.b = {f: 7}; 
graph.c = {d: 5, e: 2};
graph.d = {f: 2};
graph.e = {f: 1};
graph.f = {g: 1};
graph.g = {};

function shortPath(graph, start, end) {
	const costs = {}; // создаем объект для хранения минимальных стоимостей
	const processed = []; // массив для хранения обработанных объектов
	let neighbors = {}; // объект для добавления ближайших соседей
	Object.keys(graph).forEach(node => {
		if (node !== start) {
			let value = graph[start][node]; 
			// добавили значения тех вершин, в которые можем попасть со стартовой вершины
			costs[node] = value || 1000000000; 
		}
	})
	let node = findNodeLowestCost(costs, processed)
	while (node) {
		const cost = costs[node]; // затем нашли узел с минимальной стоимостью 
		neighbors = graph[node];
		// и перебирая узлы с мин стоимостями обновляем значения в таблице с мин путями
		Object.keys(neightbors).forEach(neighbor => {
			let newCost = cost + neighbors[neighbor];
			if (newCost < cost[neighbor]) {
				costs[neighbor] = newCost
			}
		})
		processed.push(node)
		// в конце цикла мы каждый узел помечали как обработанный 
		node = findNodeLowestCost(costs, processed)
		// и искали новый узел 
	}
	return costs;
}

function findNodeLowestCost(costs, processed) {
	let lowestCost = 1000000000;
	let lowestNode;
	Object.keys(costs).forEach(node => {
		let cost = costs[node];
		if (cost < lowestCost && !processed.includes(node)) {
			lowestCost = cost;
			lowestNode = node;
		}
	})
	return lowestNode;
}
```

### Tree_algorithm ###
Поскольку дерево является массивом узлов, мы по нему можем проитерироваться: 

Рекурсивная версия:
```js
const recursive = (tree) => {
	let sum = 0;
	tree.forEach(node => {
		sum += node.v;
		if (!node.c) {
			return node.v;
		}
		sum += recursive(node.c);
	})
	return sum;
}
```

Цикличная версия:
```js
const iteration = (tree) => {
	if (!tree.length) {
		return 0;
	}
	
	let sum = 0;
	let stack = []; // использовать будем как стэк
	tree.forEach(node => stack.push(node));
	while(stack.length) {
		const node = stack.pop();
		sum += node.v;
		if (node.c) {
			node.c.forEach(child => stack.push(child));
		}
	}
	return sum;
}
```

### Caching_function ###
(функция кеширования)

```js
function factorial(n) { // эта функция для того, чтобы было что кэшировать
	let result = 1;
	while (n != 1) {
		result *= n;
		n -= 1;
	}
	return result;
}

function cashFunction(fn) {
	const cash = {}
	return function(n) {
		console.log('cached', cash[n]); // проверим что взято кешированием...
		if (cash[n]) {
			return cash[n]
		}
		let result = fn(n);
		console.log('counted by fn = ', result); // а что посчитано функцией
		cash[n] = result;
		return result;
	}
}

// создадим функцию которая будет кешировать факториал
const cashFactorial = cashFunction(factorial) 

cashFactorial(5) // counted by fn = 120
cashFactorial(4) // counted by fn = 24
cashFactorial(3) // counted by fn = 6
cashFactorial(4) // cached 24
cashFactorial(5) // cached 120
cashFactorial(1) // counted by fn = 1

```