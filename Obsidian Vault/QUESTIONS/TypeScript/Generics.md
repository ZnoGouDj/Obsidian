Предоставляют возможность создать компонент, который может работать с различными типами, а не с одним. 
Можно также рассмотреть дженерик как функцию, которую мы вызываем с определенным типом, и она нам возвращает новую структуру с использованием переданного типа.

При использовании дженериков, ТайпСкрипт распознает типы переменных на лету и можно писать более универсальный код, не переписывая одно и то же с минимальными отличиями несколько раз.

```ts
function identity<T>(arg: T) {
	return arg;
}
```

То есть вместо создания двух похожих интерфейсов, можно создать ОДИН, указать что он будет Дженерик, и передать Дженерик в нужное динамическое поле:
```ts
interface State<T> {
	loading: boolean;
	error: Error | null;
	data: T;
}
// далее можно можно на его основе создавать например типы
type UserState = State<User>
type MessageState = State<Message>

const userState: UserState = {
	loading: false,
	error: null,
	data: {
		id: 1,
		name: 'Name'
	}
} // ...
```

