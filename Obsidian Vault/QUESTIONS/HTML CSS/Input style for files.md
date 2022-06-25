(Как стилизовать инпут для загрузки файлов? CSS)

Пишем:
```html
<input type="file" />
```
Получаем:
<input type="file" />

Выглядит не очень.

Можем сделать **label**, стилизовать его и скрыть **input**:
```html
<input id="file" type="file" />
<label for="file">Click to upload</label>
```
```css
input {
	display: none;
}
label {
	padding: 20px;
	border: 2px black dashed;
}
```
Получаем:
<input id="file" type="file" style="display: none;"/>
<label for="file" style="padding: 20px; border: 2px black dashed;">Click to upload</label>

