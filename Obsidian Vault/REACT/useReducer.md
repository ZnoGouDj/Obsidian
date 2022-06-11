```js
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

Альтернатива для useState, и предпочтительнее useState, если логика состояния сложная. (например логика включает в себя несколько значений, или когда следующее состояние зависит от предыдущего)

Аналогичные указания:

```js
const [state, dispatch] = useReducer(reducer, { count: 0 });
const [count, setCount] = useState(0);
```

Стандартный пример со счетчиком:

```js
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```