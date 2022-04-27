Метод **fetch** — **это** XMLHttpRequest нового поколения. 
Он предоставляет улучшенный интерфейс для осуществления запросов к серверу: как по части возможностей и контроля над происходящим, так и по синтаксису, так как построен на промисах.

Типичный запрос с помощью `fetch` состоит из двух операторов `await`:

```js
let response = await fetch(url, options); // завершается с заголовками ответа let 
result = await response.json(); // читать тело ответа в формате JSON
```

Или, без `await`:

```js
fetch(url, options)   
	.then(response => response.json())   
	.then(result => /* обрабатываем результат */)
```

Параметры ответа:

-   `response.status` – HTTP-код ответа,
-   `response.ok` – `true`, если статус ответа в диапазоне 200-299.
-   `response.headers` – похожий на `Map` объект с HTTP-заголовками.

Методы для получения тела ответа:

-   **`response.text()`** – возвращает ответ как обычный текст,
-   **`response.json()`** – преобразовывает ответ в JSON-объект,
-   **`response.formData()`** – возвращает ответ как объект FormData (кодировка form/multipart, см. следующую главу),
-   **`response.blob()`** – возвращает объект как [Blob](https://learn.javascript.ru/blob) (бинарные данные с типом),
-   **`response.arrayBuffer()`** – возвращает ответ как [ArrayBuffer](https://learn.javascript.ru/arraybuffer-binary-arrays) (низкоуровневые бинарные данные),

Опции `fetch`, которые мы изучили на данный момент:

-   `method` – HTTP-метод,
-   `headers` – объект с запрашиваемыми заголовками (не все заголовки разрешены),
-   `body` – данные для отправки (тело запроса) в виде текста, `FormData`, `BufferSource`, `Blob` или `UrlSearchParams`.