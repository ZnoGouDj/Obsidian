Библиотека для асинхронных [[HTTP]]-запросов к серверу. Построена на Promise API. В отличие от [[Fetch]] надо установить.

<span style="font-weight: bold; color: #FFB514; ">Типичный запрос</span>

```js
axios.get(url)
	.then(res => console.log(res))
	.catch((err) => console.log(err));
```

Если нам нужен какой-то другой метод, просто меняем GET после точки на POST, PUT и т.д.

Можем создать <span style="font-weight: bold; color: mediumvioletred;">config object</span> и определить в нем пропсы, например baseUrl, params, headers, auth, responseType.

<span style="font-weight: bold; color: deepskyblue;">В ответ</span> axios возвращает промис, который надо заресолвить, и в полученном объекте у нас будут следующие значения:
1) data - тело ответа
2) status - HTTP статус (типа 200 или 404)
3) statusText - HTTP статус текстом (ОК например)
4) headers - такие же как в запросе 
5) config - конфигурация из запроса
6) request - XMLHttpRequest объект

<span style="font-weight: bold; color: #FFB514;">Запрос с POST</span>

```js
axios.post({
	'/url',
	{ name: 'John', age: 22 },
	{ options }
})
```
либо можем создать <span style="font-weight: bold; color: mediumvioletred;">config object</span> и передать его как переменную:
```js
const config = {
	url: 'http://api.com',
	method: 'POST', 
	header: {
		'Content-Type': 'application/json'
	},
	data: { name: 'John', age: 22 }
}

axios(config);
```

[[Fetch vs Axios]]