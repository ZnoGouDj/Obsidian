Оператор выводит все публичные нестатические ключи, принадлежащие типу и возвращает [[union]]. Полезен при работе с [[Mapped types]].

```ts
type Point = {x: number, y: number};
type P = keyof Point; // type P = 'x' | 'y'

type Arrayish = {[n: number]: unknown};
type A = keyof Arrayish; // type A = number;

type Mapish = {[k: string]: boolean};
type M = keyof Mapish; // type M = string | number;
// M is number too, because js object keys are always 
// coerced to a string (obj[0] => obj["0"])
```

Если бы мы пытались с помощью keyof вернуть class с например статическими или приватными полями, то он бы их не вернул. 
Оператор может использоваться с ЛЮБЫМ типом данных и если тип не содержит ключей, либо они все статические либо приватные, то будет определен тип never

