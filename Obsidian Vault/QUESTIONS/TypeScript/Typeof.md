Уже есть в [[JavaScript]] в контексте выражения
```ts
const message = {
	id: 1,
	text: 'JavaScript'
}

const t = typeof message;

console.log(t); // object
```

в TypeScript добавлен в контексте типов. 
```ts
type MessageType = typeof message; // скопирует типы изнутри 

const userMessage: MessageType = { 
	id: 123,
	text: 'Hi!'
}
```

Его можно например использовать в связке с [[Keyof]]. 
```ts
type MessageType = typeof message;
type MessageKeys = keyof MessageType; // type MessageKeys = 'id' | 'text'
```

Этот прием широко используется в [[enum]]
```ts
enum Colors {
	white = '#fff',
	black = '#000'
}
// определяем тип, который будет указывать на доступные цвета
type AvailableColors = keyof typeof Colors; // 'white' | 'black'
// и далее можем использовать его в переменной
let color: AvailableColors = 'black';
```
То есть используем сначала typeof для получения типа, затем keyof для получения ключей этого типа.