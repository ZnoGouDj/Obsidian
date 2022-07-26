Интерфейсы предпочтительнее Типов. Хоть они и похожи, возможностей больше у интерфейсов, например [[слияние типов]] (merged declarations):



## Когда использовать Type:
1) при определении примитивов
2) при определении [[tuple]]
3) при определении [[union]]
4) при определении сопоставленных типов (mapped types)
5) *when trying to overload functions in object types via composition*?

## Когда Interface:
1) для всех типов объектов, где использование type необязательно
2) если хочешь заюзать declaration merging ([[слияние типов]])

**Только ТИП может обозначить примитив**
```ts
type Nullish = null | undefined;
type Fruit = 'apple' | 'pear' | 'orange';
type Num = number | bigint;
```
**Только ТИП может обозначить Tuple**
```ts
type row = [colOne: number, colTwo: string];
```
**Только ТИП может обозначить Union**
```ts
type Fruit = 'apple' | 'pear' | 'orange';
type Vegetable = 'broccoli' | 'carrot' | 'lettuce';

// 'apple' | 'pear' | 'orange' | 'broccoli' | 'carrot' | 'lettuce';
type HealthyFoods = Fruit | Vegetable;
```

**Функции можно обозначить и ТИПОМ и ИНТЕРФЕЙСОМ**
```ts
// via type
type Sum = (x: number, y: number) => number;

// via interface
interface Sum {
  (x: number, y: number): number;
}
```

Про обеъкты тут:

https://stackoverflow.com/questions/37233735/interfaces-vs-types-in-typescript#:~:text=the%20type%20keyword-,object%20types,-An%20object%20in

