Метод **fetch** — XMLHttpRequest нового поколения, встроен в window object, позволяет асинхронно получать данные без установки библиотек. Построен на промисах.

<span style="font-weight: bold; color: mediumvioletred;">Первый аргумент</span> — url (откуда берем данные), затем обрабатываем его через .then, или ошибку через .catch.

```js
let response = await fetch(url, options); // завершается с заголовками ответа let 
result = await response.json(); // читать тело ответа в формате JSON

// OR WITHOUT AWAIT

fetch(url, options)   
	.then(response => response.json())   
	.then(result => /* обрабатываем результат */)
```

<span style="font-weight: bold; color: deepskyblue;">Второй аргумент</span> — options (опциональный). Если мы его не передаем, то нам просто скачивается дата с url. Если хотим использовать POST метод или любой другой, то должны передать этот аргумент

```js
fetch(url, {
	method: 'POST', 
	headers: {
		'Content-Type': 'application/json'
	},
	body: JSON.stringify(data)
})
.then((response) => response.json())
.catch((error) => console.log(error))
```

Методы для получения тела ответа:
-   **`response.json()`** – преобразовывает ответ в JSON-объект, (TOP POPULAR)
-   **`response.text()`** – возвращает ответ как обычный текст,
-   **`response.formData()`** – возвращает ответ как объект FormData (кодировка form/multipart, см. следующую главу),
-   **`response.blob()`** – возвращает объект как [Blob](https://learn.javascript.ru/blob) (бинарные данные с типом),
-   **`response.arrayBuffer()`** – возвращает ответ как [ArrayBuffer](https://learn.javascript.ru/arraybuffer-binary-arrays) (низкоуровневые бинарные данные),

Параметры ответа:

-   `response.status` – HTTP-код ответа,
-   `response.ok` – `true`, если статус ответа в диапазоне 200-299.
-   `response.headers` – похожий на `Map` объект с HTTP-заголовками.

[[Fetch vs Axios]]