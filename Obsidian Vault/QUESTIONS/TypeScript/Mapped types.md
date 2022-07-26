Это когда тип основан на другом типе при нежелании переиспользовать код. Mapped types основаны на синтаксисе сигнатур индексов, которые используются для объявления типов или пропсов не объявленных заранее

```ts
type OnlyBoolsAndHorses = {
	[key: string]: boolean | Horse;
};

const conforms: OnlyBoolsAndHorses = {
	del: true,
	rodney: false,
};
```