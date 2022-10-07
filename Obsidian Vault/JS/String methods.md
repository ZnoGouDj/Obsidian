<span style="font-weight: bold; color: mediumvioletred;">.length</span>
<span style="font-weight: bold; color: deepskyblue;">[index]</span> для получения определенного символа
<span style="font-weight: bold; color: gold;">includes / startsWith() / endsWith()</span> для поиска подстроки
<span style="font-weight: bold; color: mediumvioletred;">indexOf()</span> для получения индекса подстроки
<span style="font-weight: bold; color: deepskyblue;">slice(start, end)</span> для получения подстроки
<span style="font-weight: bold; color: gold;">toLowerCase() / toUpperCase()</span>
<span style="font-weight: bold; color: mediumvioletred;">replace()</span>

```js
const browserType = 'mozilla';
const updated = browserType.replace('moz','van');

console.log(updated);      // "vanilla"
console.log(browserType);  // "mozilla"
```