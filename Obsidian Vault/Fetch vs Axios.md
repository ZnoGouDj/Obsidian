<span style="font-weight: bold; color: mediumvioletred;">AXIOS</span> лучше, если приложение большое, много HTTP-запросов, где надо хендлить ошибки или использовать HTTP-interceptors
<span style="font-weight: bold; color: deepskyblue;">FETCH</span> для мелких проектов, где несколько простых запросов. Чтобы не загружать проект библиотекой.

<span style="font-weight: bold; color: gold;">JSON</span>

При получении данных в ответ они автоматически stringified (нужен только 1 **.then**)
```js 
fetch(url)
	.then((res) => res.json())
	.then((data) => console.log(data))
	.catch((error) => console.log(error))

//vs

axios.get(url)
	.then((res) => console.log(res))
	.catch((err) => console.log(err))
```

<span style="font-weight: bold; color: gold;">Error Handling</span>

При получении ответа с FETCH, надо проверять успешен ли статус, потому что мы получим ответ даже если он не успешен. Промис НЕ БУДЕТ заресолвлен только когда запрос не будет выполнен.
В случае AXIOS, если будет "плохой" ответ (типа 404), тогда промис будет отклонен и вернется ошибка. И нам нужно ее словить и проверить, какого она типа.

```js
fetch(url)
	.then((res) => {
		if (!res.ok) {
			throw new Error(res.statusText);
		}
		return res.json();
	})
	.then((data) => console.log(data))
	.catch((err) => console.log(err))

//vs

axios.get(url)
	.then((res) => console.log(res))
	.catch((err) => {
		if (err.response) {
			// When response status code is out of 2xx range
			console.log(err.response.data)
			console.log(err.response.status)
			console.log(err.response.headers)
		} else if (err.request) {
			// When no response was received after request
			console.log(err.request)
		} else {
			// Error
			console.log(err.message)
		}
	})
```

<span style="font-weight: bold; color: gold;">Download Progress</span>

Чтобы отследить прогресс загрузки в FETCH, можно использовать один из пропсов response.body - объект readableStream. Он дает ответ порциями и позволяет считать получение даты за единицу времени. 
В AXIOS это проще, потому что существует готовый модуль, который можно установить (AXIOS PROGRESS BAR)

<span style="font-weight: bold; color: gold;">HTTP Interception</span>

(когда нам надо проверить или изменить наш HTTP запрос на сервер, или с сервера. Например для аутентификации)

В FETCH по умолчанию отсутствует. Можно переписать, но долго и трудно.
В случае AXIOS есть готовое решение (и это вроде как одна из ключевых фич).
```js
axios.interceptors.request.use((config) => {
	console.log('REQUEST SENT');
})

axios.interceptors.response.use((response) => {
	return response
})

axios.get(url)
	.then((response) => console.log(response))
	.catch((error) => console.log(error));
```