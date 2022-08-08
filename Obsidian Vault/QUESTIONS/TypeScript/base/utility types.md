TS предоставляет утилиты для упрощения БАЗОВЫХ преобразований типов.

### Readonly
```ts
interface User {
	name: string;
}

const user: Readonly<User> = { // помечаем ТОЛЬКО ДЛЯ ЧТЕНИЯ
	name: 'Egor',
}

user.name = 'Max'; // Error
```

### Required
```ts
interface Props {
	a?: number;
	b?: string;
}

const obj: Props = { a: 5 }; // OK
const obj2: Required<Props> = { a: 5 }; // Error: prop 'b' missing
```

### Record
```ts
interface PageInfo {
	title: string;
}

type Page = 'home' | 'about' | 'contact';

const x: Record<Page, PageInfo> = { // создает набор свойств
	about: { title: 'about' },
	contact: { title: 'contact' },
	home: { title: 'home' },
}
```

### Pick
```ts 
interface Todo {
	title: string;
	description: string;
	completed: boolean;
}

type TodoPreview = Pick<Todo, 'title' | 'completed'>; // отбирает типы из Туду, похож на рекорд

const todo: TodoPreview = {
	title: 'Workout',
	completed: false,
}
```

### Omit
```ts
interface Todo {
	title: string;
	description: string;
	completed: boolean;
}

type TodoPreview = Omit<Todo, 'description'>; // удаляет тип из Туду
const todo: TodoPreview = {
	title: 'Workout',
	completed: false,
}
```

### Exclude / Extract / NonNullable
```ts
// Исключает ВСЕ типы, которые передаются ВТОРЫМ АРГУМЕНТОМ
type T0 = Exclude<"a" | "b" | "c", "a">; // "b" | "c"
type T1 = Exclude<"a" | "b" | "c", "a" | "b">; // "c"
type T2 = Exclude<string | number | (() => void), Function>; // string | number

// Включает ВСЕ типы, которые передаются ВТОРЫМ АРГУМЕНТОМ
type T0 = Extract<"a" | "b" | "c", "a" | "f">; // "a"
type T1 = Extract<string | number | (() => void), Function>; // () => void

// Выбрасывает все несуществующие типы (null & undefined)
type T0 = NonNullable<string | number | undefined>; // string | number
type T1 = NonNullable<string[] | null | undefined>; // string[]
```

### ReturnType
```ts
declare function f1(): { a: number, b: string };

// создает тип из ВОЗВРАЩАЕМОГО ФУНКЦИЕЙ ТИПА
type T0 = ReturnType<() => string>; // string
type T1 = ReturnType<(s: string) => void>; // void
type T2 = ReturnType<(<T>() => T)>; // {}
type T3 = ReturnType<(<T extends X, X extends number[]>() => T)>; // number[]
type T4 = ReturnType<typeof f1>; // { a: number, b: string }
type T5 = ReturnType<string>; // Error
```

### InstanceType
```ts
class C {
	x = 0;
	y = 0;
}

// создаем тип из ТИПА ЭКЗЕМПЛЯРА функции конструктора
type T0 = InstanceType<typeof C>; // C
type T1 = InstanceType<any>; // any
type T2 = InstanceType<never>; // any
type T3 = InstanceType<string>; // Error
type T4 = InstanceType<Function>; // Error
```