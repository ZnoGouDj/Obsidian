это встроенный в браузер объект для взаимодействия с серверами, позволяет получать данные с адреса без необходимости полной перезагрузки страницы. 

Может получать любой тип данных, не только XML. 

Существует другой, более современный метод [[Fetch]].

*Типичный код GET-запроса с использованием <span style="font-weight: bold; color: gold;">XMLHttpRequest</span>*

```javascript
let xhr = new XMLHttpRequest(); 

xhr.open('GET', '/my/url'); 

xhr.send(); 

xhr.onload = function() { 
	if (xhr.status != 200) { // HTTP ошибка? 
		// обработаем ошибку 
		alert( 'Ошибка: ' + xhr.status); 
		return; 
	} 
	// получим ответ из xhr.response 
}; 

xhr.onprogress = function(event) { 
	// выведем прогресс 
	alert(`Загружено ${event.loaded} из ${event.total}`); 
}; 

xhr.onerror = function() { 
	// обработаем ошибку, не связанную с HTTP (например, нет соединения) 
};
	```