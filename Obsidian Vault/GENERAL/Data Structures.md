(Структуры данных на примере [[JavaScript]])

[Stack](#stack)
[Queue](#queue)
[Linked List](#linked_list)
[Set](#set)
[Hash Table](#hash_table)
[Tree](#tree)
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

### Linked_List ###
![[data-structure-linked-list.gif]]

Представляет "цепочную" структуру данных, где каждый узел состоит из 2х частей: данных и указателя на следующий узел. 
Сравнивая с условным массивом, можно выделить отличия:
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

**Методы:**
-   size: вернуть количество узлов
-   head: вернуть первый элемент (head — голова)
-   add: добавить элемент в конец (tail — хвост)
-   remove: удалить несколько узлов
-   indexOf: вернуть индекс узла
-   elementAt: вернуть узел по индексу
-   addAt: вставить узел в определенное место (по индексу)
-   removeAt: удалить определенный узел (по индексу)

**Реализация:**

```js
function Node(element) { 
	// данные 
	this.element = element 
	// указатель на следующий узел 
	this.next = null 
} 

function LinkedList() { 
	let length = 0 
	let head = null 
	this.size = function() { 
		return length 
	} 
	
	this.head = function() { 
		return head 
	} 
	
	this.add = function(element) { 
		let node = new Node(element) 
		if (head === null) { 
			head = node 
		} else { 
			let currentNode = head 
			while (currentNode.next) { 
				currentNode = currentNode.next 
			} 
			currentNode.next = node 
		} 
		length++ 
	} 
	
	this.remove = function(element) { 
		let currentNode = head 
		let previousNode 
		if (currentNode.element !== element) { 
			head = currentNode.next 
		} else { 
			while (currentNode.element !== element) { 
				previousNode = currentNode 
				currentNode = currentNode.next 
			} 
			previousNode.next = currentNode.next 
		} 
		length-- 
	} 
	
	this.isEmpty = function() { 
		return length === 0 
	} 
	
	this.indexOf = function(element) { 
		let currentNode = head 
		let index = -1 
		while (currentNode) { 
			index++ 
			if (currentNode.element === element) { 
				return index 
			} 
			currentNode = currentNode.next 
		} 
		return -1 
	} 
	
	this.elementAt = function(index) { 
		let currentNode = head 
		let count = 0 
		while (count < index) { 
			count++ 
			currentNode = currentNode.next 
		} 
		return currentNode.element 
	} 
	
	this.addAt = function(index, element) { 
		let node = new Node(element) 
		let currentNode = head 
		let previousNode 
		let currentIndex = 0 
		if (index > length) return false 
		if (index === 0) { 
			node.next = currentNode 
			head = node 
		} else { 
			while (currentIndex < index) { 
				currentIndex++ 
				previousNode = currentNode 
				currentNode = currentNode.next 
			} 
			node.next = currentNode 
			previousNode.next = node 
		} 
		length++ 
	} 
	
	this.removeAt = function(index) { 
		let currentNode = head 
		let previousNode 
		let currentIndex = 0 
		if (index < 0 || index >= length) return null 
		if (index === 0) { 
			head = currentIndex.next 
		} else { 
			while (currentIndex < index) { 
				currentIndex++ 
				previousNode = currentNode 
				currentNode = currentNode.next 
			} 
			previousNode.next = currentNode.next 
		} 
		length-- 
		return currentNode.element 
	} 
}
```

### Set ###
![[data-structure-set.png]]

Коллекция, которая не допускает повторов элементов и не содержит индексов.

**Методы:**
-   values: вернуть все элементы в коллекции
-   size: вернуть количество элементов
-   has: проверить, имеется ли элемент в коллекции
-   add: добавить элемент
-   remove: удалить элемент
-   union: вернуть область пересечения двух коллекций
-   difference: вернуть отличия двух коллекций
-   subset: проверить, является ли одна коллекция подмножеством другой

**Реализация:**
```js
function MySet() { 
	let collection = [] 
	this.has = function(element) { 
		return (collection.indexOf(element) !== -1) 
	}
	
	this.values = function() { 
		return collection 
	} 
	
	this.size = function() { 
		return collection.length 
	} 
	
	this.add = function(element) { 
		if (!this.has(element)) { 
			collection.push(element) 
			return true 
		} 
		return false 
	} 
	
	this.remove = function(element) { 
		if (this.has(element)) { 
			index = collection.indexOf(element) 
			collection.splice(index, 1) 
			return true 
		} 
		return false 
	} 
	
	this.union = function(otherSet) { 
		let unionSet = new MySet() 
		let firstSet = this.values() 
		let secondSet = otherSet.values() 
		firstSet.forEach(i => unionSet.add(i)) 
		secondSet.forEach(i => unionSet.add(i)) 
	} 
	
	this.intersection = function(otherSet) { 
		let intersectionSet = new MySet() 
		let firstSet = this.values() 
		firstSet.forEach(function(e) { 
			if (otherSet.has(e)) { 
				intersectionSet.add(e) 
			} 
		}) 
		return intersectionSet 
	} 
	
	this.difference = function(otherSet) { 
		let differenceSet = new MySet() 
		let firstSet = this.values() 
		firstSet.forEach(function(e) { 
			if (!otherSet.has(e)) { 
				differenceSet.add(e) 
			} 
		}) 
		return differenceSet 
	} 
	
	this.subset = function(otherSet) { 
		let firstSet = this.values() 
		return firstSet.every(value => otherSet.has(value)) 
	} 
}
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

#### Двоичноe дерево поиска
Binary Search Tree — структура, где каждый узел имеет ТОЛЬКО двоих потомков, левый (дочерний) узел меньше текущего (родительского), правый — больше

![[data-structure-binary-tree.png]]

**Методы:**
-   add: добавить узел
-   findMin: получить минимальный узел
-   findMax: получить максимальный узел
-   find: найти определенный узел
-   isPresent: проверить наличие определенного узла
-   remove: удалить узел

**Реализация:**
```js
class Node { 
	constructor(data, left = null, right = null) { 
		this.data = data 
		this.left = left 
		this.right = right 
	} 
} 

class BST { 
	constructor() { 
		this.root = null 
	} 
	
	add(data) { 
		const node = this.root 
		if (node === null) { 
			this.root = new Node(data) 
			return 
		} else { 
			const searchTree = function(node) { 
				if (data < node.data) { 
					if (node.left === null) { 
						node.left = new Node(data) 
						return 
					} else if (node.left !== null) { 
						return searchTree(node.left) 
					} 
				} else if (data > node.data) { 
					if (node.right === null) { 
						node.right = new Node(data) 
						return 
					} else if (node.right !== null) { 
						return searchTree(node.right) 
					} 
				} else { 
					return null 
				} 
			} 
			return searchTree(node) 
		} 
	} 
	
	findMin() { 
		let current = this.root 
		while (current.left !== null) { 
			current = current.left 
		} 
		return current.data 
	} 
	
	findMax() { 
		let current = this.root 
		while (current.right !== null) { 
			current = current.right 
		} 
		return current.data 
	} 
	
	find(data) { 
		let current = this.root 
		while (current.data !== data) { 
			if (data < current.data) { 
				current = current.left 
			} else { 
				current = current.right 
			} 
			if (current === null) { 
				return null 
			} 
		} 
		return current 
	} 
	
	isPresent(data) { 
		let current = this.root 
		while (current) { 
			if (data === current.data) { 
				return true 
			} 
			data < current.data ? current = current.left : current = current.right 
		} 
		return false 
	} 
	
	remove(data) { 
		const removeNode = function(node, data) { 
			if (node === null) return null 
			if (data === node.data) { 
				// потомки отсутствуют 
				if (node.left === null && node.right === null) return null 
				// отсутствует левый узел 
				if (node.left === null) return node.right 
				// отсутствует правый узел 
				if (node.right === null) return node.left 
				// имеется два узла 
				let tempNode = node.right 
				while (tempNode.left !== null) { 
					tempNode = tempNode.left 
				}
				node.data = tempNode.data 
				node.right = removeNode(node.right, tempNode.data) 
				return node 
			} else if (data < node.data) { 
				node.left = removeNode(node.right, data) 
				return node 
			} else { 
				node.right = removeNode(node.right, data) 
				return node 
			} 
		} 
		this.root = removeNode(this.root, data) 
	} 
}
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