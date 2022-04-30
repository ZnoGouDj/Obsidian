это метод для отправки [[Action]] в [[store]]. Вызов `store.dispatch()` и передача значения, вернувшегося из [[action creator]], отправляет action в store.

Одинаковые:
```js
store.dispatch(actionCreator());
store.dispatch({ type: 'LOGIN' });
```

