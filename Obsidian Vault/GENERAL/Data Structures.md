(Структуры данных на примере [[JavaScript]])

[Stack](#stack)
[Queue](#queue)
[Array](#array)
[Linked List](#linked_list)
[Set & Map](#set_&_map)
[Hash Table](#hash_table)
[Tree](#tree)
[Binary Tree](#binary_tree)
[Graph](#graph)
[Нагруженное (префиксное) дерево (trie)](#trie)

### Stack ###
![[data-structure-stack.gif]]

Следует принципу Last In First Out (последний вошел, первый вышел). 
Представить можно как сложенные **Pringles** в тубус Pringles - ты не сможешь достать нижнюю не достав все остальные. 
Более реальный пример - кнопка "назад" в браузере, которая возвращает предыдущую страницу и так далее.

**Методы:**
-   push: добавить новый элемент
-   pop: удалить верхний элемент, вернуть его
-   peek: вернуть верхний элемент
-   isEmpty: проверить на пустоту
-   size: вернуть количество элементов в стеке

**Реализация:**
```js
function Stack() { 
	this.count = 0 
	this.storage = {} 
	
	this.push = function(value) { 
		this.storage[this.count] = value 
		this.count++ 
	} 
	
	this.pop = function() { 
		if (this.count === 0) return undefined 
		this.count-- 
		let result = this.storage[this.count] 
		delete this.storage[this.count] 
		return result 
	} 
	
	this.peek = function() { 
		return this.storage[this.count - 1] 
	} 
	
	this.size = function() { 
		return this.count 
	} 
}
```

### Queue ###
![[data-structure-queue.gif]]

Следует принципу First In First Out (Первый вошел, первый вышел).
Пример - обычная будничная ОЧЕРЕДЬ.

**Методы:**
-   enqueue: войти в очередь, добавить элемент в конец
-   dequeue: покинуть очередь, удалить первый элемент и вернуть его
-   front: получить первый элемент
-   isEmpty: проверить, пуста ли очередь
-   size: получить количество элементов в очереди

**Реализация:**
```js
function Queue() { 
	let collection = [] 
	
	this.print = function() { 
		console.log(collection)
	} 
	
	this.enqueue = function(element) { 
		collection.push(element) 
	} 
	
	this.dequeue = function() { 
		return collection.shift() 
	} 
	
	this.front = function() { 
		return collection[0] 
	} 
	
	this.isEmpty = function() { 
		return collection.length === 0 
	} 
	
	this.size = function() { 
		return collection.length 
	} 
}
```

### Array ###
Последовательный набор каких-то объектов
Занимает конкретный участок в памяти и изначально определено, сколько элементов в нем будет находиться.

**Плюсы этого подхода** - знаем позицию каждого элемента и можем получить его за КОНСТАНТНОЕ время (мгновенно)

**Минусы подхода** - чтобы добавить новый элемент в массив, нам нужно создавать НОВЫЙ МАССИВ на одну ячейку больше, перекидывать значения из старого массива, добавлять новый элемент и удалять старый массив.

Поэтому хорошо подходит для случаев, где НЕЧАСТО надо изменять размер массива и часто обращаться к данным 

### Linked_List ###
Каждый элемент занимает отдельное место в памяти 
Связность происходит потому, что каждый ПРЕДЫДУЩИЙ элемент хранит ссылку на СЛЕДУЮЩИЙ элемент в списке

![[data-structure-linked-list.gif]]

<div class="table table_wrapped"><table>
<tbody><tr>
<th>Критерий</th>
<th>Массив</th>
<th>Список</th>
</tr>
<tr>
<td>Выделение памяти</td>
<td>Статическое, происходит последовательно во время компиляции </td>
<td>Динамическое, происходит асинхронно во время запуска (выполнения)</td>
</tr>
<tr>
<td>Получение элементов</td>
<td>Поиск по индексу, высокая скорость</td>
<td>Поиск по всем узлам очереди, скорость менее высокая</td>
</tr>
<tr>
<td>Добавление/удаление элементов</td>
<td>В связи с последовательным и статическим распределением памяти скорость ниже</td>
<td>В связи с динамическим распределением памяти скорость выше</td>
</tr>
<tr>
<td>Структура</td>
<td>Одно или несколько направлений</td>
<td>Однонаправленный, двунаправленный или циклический</td>
</tr>
</tbody></table></div>

**Плюс этого подхода** - можем добавлять элементы в конец и начало списка
**Минус подхода** - чтобы ПОЛУЧИТЬ какой-то элемент, нам с самого начала списка надо итерироваться с сравнивать 

Хорошо подходит если редко обращаемся к данным, и часто этот список дополняем

```js
class LinkedList {
	constructor() {
		this.size = 0;
		this.root = null;
	}
	add(value) {
		if (this.size === 0) {
			this.root = new Node(value);
			this.size += 1;
			return true;
		}
		let node = this.root;
		while (node.next) {
			node = node.next
		}
		let newNode = new Node(value);
		node.next = newNode;
		this.size += 1;
	}
	
	getSize() {
		return this.size;
	}
	
	print() {
		let result = []
		let node = this.root;
		while (node) {
			result.push(node.value);
			node = node.next;
		}
		console.log(result);
		return result;
	}
}

class Node {
	constructor(value) {
		this.value = value;
		this.next = null;
	}
}

const list = new LinkedList()
list.add(5)
list.add(3)
list.add(2)
list.add(5)
list.add(7)

list.print() // [5, 3, 2, 5, 7]
```

**Методы:**
-   size: вернуть количество узлов
-   head: вернуть первый элемент (head — голова)
-   add: добавить элемент в конец (tail — хвост)
-   remove: удалить несколько узлов
-   indexOf: вернуть индекс узла
-   elementAt: вернуть узел по индексу
-   addAt: вставить узел в определенное место (по индексу)
-   removeAt: удалить определенный узел (по индексу)



### Set_&_Map ###
Хранят в себе пары ключ : значение, где значение мы получаем ПО КЛЮЧУ.
По сути обычный объект JS уже является Map

Основное преимущество структуры - мы можем за константное время добавлять объекты в структуру и извлекать.

**Map** - можем как КЛЮЧ использовать не только строки, но и объекты. 

```js
const map = new Map()

map.set('name', 'znogoud');

console.log(map.get('name')); // znogoud

// но такая запись не отличается от обычного объекта. Делаем ключ-объект

const objKey = {id: 5};
map.set(objKey, 'znogoud');

console.log(map.get(objKey)); // znogoud
```

**Set** - хранит в себе ТОЛЬКО уникальные значения. 

```js
const set = new Set();

set.add(5);
set.add(5);
set.add(5);
set.add(5);
set.add(4);
set.add(3);

console.log(set); // {5, 4, 3}
```

### Hash_Table ###
![[data-structure-hash-table.png]]

Строится по принципу ключ-значение. Имеет высокую скорость поиска значений по ключам (*поэтому используется в структурах Map, Dictionary & Object.*)

Имеет HASH FUNCTION, которая преобразует ключи в список номеров, которые используются как имена ключей. 
Время поиска значения по ключу может достигать О(1).

Одинаковые ключи должны возвращать одинаковые значения - суть хэширования. 

**Методы:**
-   add: добавить пару ключ/значение
-   remove: удалить пару
-   lookup: найти значение по ключу

**Реализация:**
```js
function hash(string, max) { 
	let hash = 0 
	for (let i = 0; i < string.length; i++) { 
		hash += string.charCodeAt(i) 
	} 
	return hash % max 
} 

function HashTable() { 
	let storage = [] 
	const storageLimit = 4 
	
	this.add = function(key, value) { 
		let index = hash(key, storageLimit) 
		if (storage[index] === undefined) { 
			storage[index] = [ [key, value] ] 
		} else { 
			let inserted = false 
			for (let i = 0; i < storage[index].len; i++) { 
				if (storage[index][i][0] === key) { 
					storage[index][i][1] = value 
					inserted = true 
				} 
			} 
			if (inserted === false) { 
				storage[index].push([key, value]) 
			} 
		} 
	} 
	
	this.remove = function(key) { 
		let index = hash(key, storageLimit) 
		if (storage[index].length === 1 && storage[index][0][0] === key) { 
			delete storage[index] 
		} else { 
			for (let i = 0; i < storage[index]; i++) { 
				if (storage[index][i][0] === key) { 
					delete storage[index][i] 
				} 
			} 
		} 
	} 
	
	this.lookup = function(key) { 
		let index = hash(key, storageLimit) 
		if (storage[index] === undefined) { 
			return undefined 
		} else { 
			for (let i = 0; i < storage[index].length; i++) { 
				if (storage[index][i][0] === key) { 
					return storage[index][i][1] 
				} 
			} 
		} 
	} 
}
```

### Tree ###
![[data-structure-tree.png]]

Рекурсивная структура данных, где каждый узел является также деревом, но для данного дерева каждый узел является ПОДДЕРЕВОМ. 
Многоуровневая, нелинейная структура, которая эффективна в плане добавления и поиска элементов.

**Концепции:**
-   root: корневой элемент, не имеет «родителя»
-   parent node: прямой узел верхнего слоя (уровня), может быть только одним
-   child node: прямой узел (узлы) нижнего уровня, может быть несколько
-   siblings: дочерние элементы одного родительского узла
-   leaf: узел без «детей»
-   Edge: ветка или ссылка (связь) между узлами
-   Path: путь (совокупность ссылок) от начального узла до целевого элемента
-   Height of Tree (высота дерева): количество ссылок самого длинного пути от определенного элемента до узла, не имеющего потомков
-   Depth of Node (глубина узла): количество ссылок от корневого узла до определенного элемента
-   Degree of Node: количество потомков

### Binary_tree ### 
Структура данных, где каждый узел также является деревом (то есть структура рекурсивна). И основаня суть В ТОМ, что у каждого узла может быть ТОЛЬКО два потомка.

![[data-structure-binary-tree.png]]

Добавляются эти узлы тоже особым способом: если добавляемое в дерево значения МЕНЬШЕ, чем текущий узел, то значение идет в левое поддерево. Если БОЛЬШЕ - в правое.

Сравнение происходит с каждым узлом, и получается что правая часть поддерева выстраивается с бОльшими значениями, левая - с меньшими. 

Называется бинарным, потому что здесь также как в бинарном поиске, можно находить ДАННЫЕ за логарифмическое время (O(log2n))

```js
class BinaryTree {
	constructor() {
		this.root = null;
	}
	
	add(value) {
		if (!this.root) {
			this.root = new TreeNode(value);
		} else {
			let node = this.root;
			let newNode = new TreeNode(value);
			while(node) {
				if (value > node.value) {
					if (!node.right) {
						break;
					}
					node = node.right;
				} else {
					if (!node.left) {
						break;
					}
					node = node.left;
				}
			}
			if (value > node.value) {
				node.right = newNode
			} else {
				node.left = newNode
			}
		}
	}
	
	print(root = this.root) {
		if (!root) {
			return true;
		}
		console.log(root.value);
		this.print(root.left);
		this.print(root.right);
	}
}

class TreeNode {
	constructor(value) {
		this.value = value;
		this.left = null;
		this.right = null;
	}
}

const tree = new BinaryTree() 

tree.add(5)
tree.add(2)
tree.add(6)
tree.add(2)
tree.add(1)

tree.print()  // 5 2 2 1 6
// ! вначале вывелось левое поддерево (т.е. значения меньше 5) и затем только правое (в него ушла 6)
```

### Graph ###
![[data-structure-graph.png]]

Коллекция связанных узлов. 
Бывает ориентированный и неориентированный (== имеют ли ссылки направление)
Используются например для расчета лучшего маршрута в навигации, или для списка рекомендаций в соц сетях.

![[data-structures-graph-2.png]]

**Реализация BFS:**
```js
function bfs(graph, root) { 
	let nodesLen = {} 
	for (let i = 0; i < graph.length; i++) { 
		nodesLen[i] = Infinity 
	} 
	nodesLen[root] = 0 
	let queue = [root] 
	let current 
	while (queue.length !== 0) { 
		current = queue.shift() 
		let curConnected = graph[current] 
		let neighborIdx = [] 
		let idx = curConnected.indexOf(1) 
		while (idx !== -1) { 
			neighborIdx.push(idx) 
			idx = curConnected.indexOf(1, idx + 1) 
		} 
		for (let i = 0; i < neighborIdx.length; i++) { 
			if (nodesLen[neighborIdx[i]] === Infinity) { 
				nodesLen[neighborIdx[i]] = nodesLen[current] + 1 
				queue.push(neighborIdx[i]) 
			} 
		} 
	} 
	return nodesLen 
}
```

### Trie ###
![[data-structure-trie.png]]

Разновидность поискового дерева. 
Данные сохраняются последовательно (шаг за шагом) — каждый узел дерева представляет собой один шаг. 
*Префиксное дерево используется в словарях, поскольку существенно ускоряет поиск. *
  
Каждый узел дерева — буква алфавита, следование по ветке приводит к формированию слова. Оно также содержит «булевый индикатор» для определения того, что текущий узел является последней буквой.  
  
**Методы:**
-   add: добавить слово в словарь
-   isWord: проверить наличие слова
-   print: вернуть все слова