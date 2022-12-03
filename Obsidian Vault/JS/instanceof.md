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
Обычные объекты приводятся к строке в виде <span style="font-weight: bold; color: #FFB514;">[object Object]</span>, но мы можем также использовать этот метод как альтернативу **typeof** & **instanceof**:

- для чисел возвращает <span style="font-weight: bold; color: mediumvioletred;">[object Number]</span>
- для булевых <span style="font-weight: bold; color: deepskyblue;">[object Boolean]</span>
- для null <span style="font-weight: bold; color: mediumvioletred;">[object Null]</span>
- для undefined <span style="font-weight: bold; color: deepskyblue;">[object Undefined]</span>
- для массивов <span style="font-weight: bold; color: mediumvioletred;">[object Array]</span>

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