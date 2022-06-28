(Структуры данных) (the most popular ones)

### Массив ###
Последовательный набор каких-то объектов
Занимает конкретный участок в памяти и изначально определено, сколько элементов в нем будет находиться.

**Плюсы этого подхода** - знаем позицию каждого элемента и можем получить его за КОНСТАНТНОЕ время (мгновенно)

**Минусы подхода** - чтобы добавить новый элемент в массив, нам нужно создавать НОВЫЙ МАССИВ на одну ячейку больше, перекидывать значения из старого массива, добавлять новый элемент и удалять старый массив.

Поэтому хорошо подходит для случаев, где НЕЧАСТО надо изменять размер массива и часто обращаться к данным 

### Связный список ###
Каждый элемент занимает отдельное место в памяти 
Связность происходит потому, что каждый ПРЕДЫДУЩИЙ элемент хранит ссылку на СЛЕДУЮЩИЙ элемент в списке

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

### Бинарное дерево ### 
Структура данных, где каждый узел также является деревом (то есть структура рекурсивна). И основаня суть В ТОМ, что у каждого узла может быть ТОЛЬКО два потомка.

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

### Set & Map ###
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