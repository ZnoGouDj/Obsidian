(миксины)

Это специальные КЛАССЫ, которые содержат комбинацию методов, которые могут использоваться другими классами. 
Позволяют переиспользовать код и избегать ограничений множественных наследованностей. Хороши для приложений, которые планируют разрастаться.

Делаем базовый класс для применения Миксинов:

```js
class Block {
    name = "";
    length = 0;
    breadth = 0;
    height = 0;
    constructor(name: string, length: number, breadth: number, height: number, ) {
        this.name = name;
        this.length = length;
        this.breadth = breadth;
        this.height = height;
    }
}
```

Затем делаем классы для расширения базового класса:

```js
class Moulder {
  moulding = true;
  done = false
  mould() {
    this.moulding = false;
    this.done = true;
  }
}
class Stacker {
  stacking = true;
  done = false
  stack() {
    this.stacking = false;
    this.done = true;
  }
}
```

Делаем интерфейс, который свяжет их (ВАЖНО! сделать такое же имя "Block"):

```js
interface Block extends Moulder, Stacker {}
```

И благодаря [[Слияние типов]], Block класс сольется с Block интерфейсом ☝

## Создание функций

Можно использовать функцию из коробки **applyMixins**:

```js
function applyMixins(derivedCtor: any, constructors: any[]) {
  constructors.forEach((baseCtor) => {
    Object.getOwnPropertyNames(baseCtor.prototype).forEach((name) => {
      Object.defineProperty(
        derivedCtor.prototype,
        name,
        Object.getOwnPropertyDescriptor(baseCtor.prototype, name) ||
          Object.create(null)
      );
    });
  });
}
```

она проходится по **Moduler** & **Stacker** классам, потом по их списку свойств и задает эти же свойства в класс **Block**

```js
applyMixins(Block, [Moulder, Stacker]);
```