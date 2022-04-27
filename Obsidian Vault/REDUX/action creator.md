## Экшн креатор че это?

Просто функция, которая возвращает объект.
С заданным типом и с каким-то может, динамическим аргументом, если он нужен. 
Ну под аргументом я какой-то Пейлод подразумеваю, который мы хотим в стейт прокинуть.



Генераторы действий (actions creators) — это функции, создающие действия.

```javascript
function addItem(t) {
  return {
    type: ADD_ITEM,
    title: t
  }
}
```

Обычно инициируются вместе с функцией отправки действия:

```javascript
dispatch(addItem('Milk'))
```

Или при определении этой функции:

```javascript
const dispatchAddItem = i => dispatch(addItem(i))
dispatchAddItem('Milk')
```