Create store метод может подписывать на себя слушателей. Это массив функций, которые будут вызваны при обновлении [[store]]. 

```javascript
const store = createStore(reducer);
store.subscribe(state => console.log(state)); // add function into listeners
store.dispatch(action);
```

console.log вызовется после изменения стейта.