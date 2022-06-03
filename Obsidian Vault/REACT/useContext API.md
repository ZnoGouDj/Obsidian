Создает объект Context. 
defaultValue используется только если нет подходящего Provider выше в дереве.

```js
const MyContext = React.createContext(defaultValue);
```

Provider компонент позволяет дочерним подписаться на его изменения. Принимает value, который будет передан во все компоненты-потомки.
Также Provider можно вкладывать друг в друга.
**все потребители-потомки будут ре-рендериться, когда value изменяется**. Походу даже сквозь shouldComponentUpdate.

```js
<MyContext.Provider value={/* некоторое значение */}>
```

Consumer подписывается на изменения контекста. Он принимает функцию как дочерний компонент. 
Передаваемый аргумент `value` будет равен ближайшему (вверх по дереву) значению этого контекста, а именно пропу `value` компонента `Provider`.

```js
<MyContext.Consumer>
  {value => /* отрендерить что-то, используя значение контекста */}
</MyContext.Consumer>
```

displayName позволяет задать строковое свойство. React DevTools использует его при отображении контекста.

```js
const MyContext = React.createContext(/* некоторое значение */);
MyContext.displayName = 'MyDisplayName';
<MyContext.Provider> // "MyDisplayName.Provider" в DevTools
<MyContext.Consumer> // "MyDisplayName.Consumer" в DevTools
```

Примеры https://ru.reactjs.org/docs/context.html#contextprovider