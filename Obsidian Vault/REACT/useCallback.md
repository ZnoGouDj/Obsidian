```js
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

Хук, похожий по принципу работы на [[useMemo]], только возвращает функцию (колбэк), которая изменяется ТОЛЬКО если изменяются зависимости. 

**<span style="font-weight: bold; color: #FE5C2B;">useMemo:</span> возвращает и хранит вычисленное значение функции в переменной**
**<span style="font-weight: bold; color: deepskyblue;">useCallback:</span> возвращает и хранит саму функцию в переменной**