<span style="font-weight: bold; color: #FE5C2B;">.length</span>
<span style="font-weight: bold; color: deepskyblue;">[index]</span> для получения определенного символа
<span style="font-weight: bold; color: #FFB514;">includes / startsWith() / endsWith()</span> для поиска подстроки
<span style="font-weight: bold; color: #FE5C2B;">indexOf()</span> для получения индекса подстроки
<span style="font-weight: bold; color: deepskyblue;">slice(start, end)</span> для получения подстроки
<span style="font-weight: bold; color: #FFB514;">toLowerCase() / toUpperCase()</span>
<span style="font-weight: bold; color: #FE5C2B;">replace()</span>

```js
const browserType = 'mozilla';
const updated = browserType.replace('moz','van');

console.log(updated);      // "vanilla"
console.log(browserType);  // "mozilla"
```