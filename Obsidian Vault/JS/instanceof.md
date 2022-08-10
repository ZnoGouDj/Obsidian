проверяет к какому классу принадлежит объект (с учетом наследования).

```js
class Car {}
let ford = new Car();

console.log(ford instanceof Car); // true

// works for func too
function Man() {}

console.log(new Man() instanceof Man); // true

// works for Array too
let arr = [1,2,3];
alert(arr instanceof Array); // true
alert(arr instanceof Object); // true (since Array inherits the Object)
```

### Object.prototype.toString to define the type
Обычные объекты приводятся к строке в виде `[object Object]`, но мы можем также использовать этот метод как альтернативу **typeof** & **instanceof**:

- для чисел возвращает `[object Number]`
- для булевых `[object Boolean]`
- для null `[object Null]`
- для undefined `[object Undefined]`
- для массивов `[object Array]`

```js
let objToStr = Object.prototype.toString;

let arr = [];

console.log(objToStr.call(arr)); // [object Array]
// использовали call чтобы сделать objToStr в контексте this=arr (привязать контекст)

// больше примеров
let s = Object.prototype.toString; 
console.log( s.call(123) ); // [object Number] 
console.log( s.call(null) ); // [object Null] 
console.log( s.call(alert) ); // [object Function]
```

<div style="display: flex; justify-content: center;"><table> <thead> <tr> <th></th> <th>для</th> <th>возвращает</th> </tr> </thead> <tbody> <tr> <td>typeof</td> <td>примитивов</td> <td>строка</td> </tr> <tbody> <tr> <td>{}.toString</td> <td>примитивов, встроенных объектов</td> <td>строка</td> </tr> <tbody> <tr> <td>instanceof</td> <td>объектов</td> <td>true/false</td> </tr> </tbody> </table></div>

То есть технически {}.toString круче чем какой-то typeof. А instanceof подходит для работы с иерархией классов и проверок наследований.