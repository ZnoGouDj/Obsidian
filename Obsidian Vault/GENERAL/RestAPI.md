[[протокол]], по которому устройства обмениваются данными. 

У Rest приложения есть некий список URL-адресов, с помощью которых можно будет общаться с нашим сервером. 

Сервер с их помощью может получать запросы на:
1) получение
2) обновление
3) добавление
4) удаление

С помощью списка таких адресов мы предоставляем некий интерфейс, с помощью которого другие сервисы могут с ним взаимодействовать. Обращаясь к списку таких адресов мы можем выполнять:
1) GET — read from DB
2) PUT — update/replace in DB
4) POST — create new record in DB
5) DELETE — delete

![[restAPI-scheme.png]]
