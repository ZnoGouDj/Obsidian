Сущность, которая позволяет лучше структурировать однотипные элементы.
Похожа на смесь объекта и массива
```ts
enum Directions {
	Up,
	Down,
	Left,
	Right
}
// При обращении к значению enum возвращается его ИНДЕКС.
Directions.Up; // 0
// Естественно можно получать и значения
Directions[0]; // "Up"
```

По умолчанию индексация происходит по порядку, но мы можем ее нарушать
```ts
enum Directions {
	Up = 2,
	Down = 4,
	Left = 6, 
	Right = 8
}
Directions.Up; // 2
Directions[6]; // "Left"
```
или вообще задавать свои индексы
```ts
enum links {
	youtube = 'https://youtube.com/',
	facebook = 'https://facebook.com/'
}
links.youtube; // 'https://youtube.com/'
```