## prototype vs __proto__

<span style="font-weight: bold; color: mediumvioletred;">prototype</span> является свойством объекта <span style="font-weight: bold; color: #FFB514;">Function</span>.
<span style="font-weight: bold; color: deepskyblue;">__proto__</span> внутреннее свойство <span style="font-weight: bold; color: #FFB514;">объектов</span>, указывающее на прототип.

То есть <span style="font-weight: bold; color: mediumvioletred;">prototype</span> — это объект, который используется для построения __proto__ при создании объекта с помощью new, а
<span style="font-weight: bold; color: deepskyblue;">__proto__</span> — это фактический объект, который используется в цепочке поиска для разрешения методов и т. д.


```js
( new Foo ).__proto__ === Foo.prototype
( new Foo ).prototype === undefined
```