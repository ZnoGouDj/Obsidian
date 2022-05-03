## А че такое глобальный стор?

Стор это сам объект, который содержит в себе стейт, диспатч (по сути все что есть в редаксе, объединение всей модели приложения, и у него происходит изменение в предсказуемый момент времени, там при помощи экшнов, редюсеров)

**Store**:
-   содержит состояние приложения;
-   отображает состояние через `getState()`;
-   может обновлять состояние через `dispatch()`;
-   регистрировать изменения через  `subscribe()`.

Хранилище в приложении всегда уникально. Так создаётся хранилище для приложения listManager:

```javascript
import { createStore } from 'redux'
import listManager from './reducers'
let store = createStore(listManager)
```

Хранилище можно инициировать через серверные данные:

```javascript
let store = createStore(listManager, preexistingState)
```

**Функции хранилища**

Получение состояния:

```javascript
store.getState()
```

Обновление состояния:

```javascript
store.dispatch(addItem('Something'))
```

Прослушивание изменений состояния:

```javascript
const unsubscribe = store.subscribe(() =>
  const newState = store.getState()
)
unsubscribe()
```