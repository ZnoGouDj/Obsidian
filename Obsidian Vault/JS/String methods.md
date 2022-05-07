**.length**
**[index]** для получения определенного символа
**includes / startsWith() / endsWith()** для поиска подстроки
**indexOf()** для получения индекса подстроки
**slice(start, end)** для получения подстроки
**toLowerCase() / toUpperCase()**
**replace()** 
```js
const browserType = 'mozilla';
const updated = browserType.replace('moz','van');

console.log(updated);      // "vanilla"
console.log(browserType);  // "mozilla"
```