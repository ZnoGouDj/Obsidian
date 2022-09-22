Let's say we've extended the Array:

```ts
Array.prototype.reduce1 = function (process, memo = this.shift()) {
	this.forEach((e) => (memo = process(memo, e)));
	return memo;
};

```
Можем прописать таким образом:
```ts
interface Array<T> {
	reduce1(process: any, initial: any): Array<T>;
}
```

Либо если мы находимся внутри модуля, нужно будет четко указать, что имеем в виду глобальный массив Array, а не создаем локальный интерфейс Array внутри вашего модуля:

```ts
declare global {
    interface Array<T> {
        remove(o: T): Array<T>;
    }
}
```