Обычно описывает функцию, которая ничего не возвращает (не возвращает undefined или вроде того, а вообще не возвращает)
```ts
function foo(): never {
	while(true) {
		// NEVER returns, infinite loop
	}
}
// либо
function throws(): never {
	throw new Error('Something went wrong!');
}
```

TS по дефолту описывает это как :void