**Редюсер (reducer)** — это чистая функция, которая принимает предыдущее состояние и экшен (state и action) и возвращает следующее состояние (новую версию предыдущего).

 
 В нем НЕЛЬЗЯ:
-   Непосредственно изменять то, что пришло в аргументах функции;
-   Выполнять какие-либо сайд-эффекты: обращаться к API или осуществлять переход по роутам;
-   Вызывать не чистые функции, например `Date.now()` или `Math.random()`.


Упрощённо базовую структуру Redux можно представить так:

**Состояние**

```javascript
{
  list: [
    { title: "First item" },
    { title: "Second item" },
  ],
  title: 'Grocieries list'
}
```

**Список действий**

```javascript
{ type: 'ADD_ITEM', title: 'Third item' }
{ type: 'REMOVE_ITEM', index: 1 }
{ type: 'CHANGE_LIST_TITLE', title: 'Road trip list' }
```

**Редюсер для каждой части состояния**

```javascript
const title = (state = '', action) => {
  if (action.type === 'CHANGE_LIST_TITLE') {
    return action.title
  } else {
    return state
  }
}
const list = (state = [], action) => {
  switch (action.type) {
    case 'ADD_ITEM':
      return state.concat([{ title: action.title }])
    case 'REMOVE_ITEM':
      return state.map((item, index) =>
        action.index === index
          ? { title: item.title }
          : item
    default:
      return state
  }
}
```

**Редуктор для общего состояния**

```javascript
const listManager = (state = {}, action) => {
  return {
    title: title(state.title, action),
    list: list(state.list, action),
  }
}
```