```js
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

Хук, похожий по принципу работы на [[useMemo]], только возвращает функцию (колбэк), которая изменяется ТОЛЬКО если изменяются зависимости. 

**useMemo: возвращает и хранит вычисленное значение функции в переменной**
**useCallBack: возвращает и хранит саму функцию в переменной**