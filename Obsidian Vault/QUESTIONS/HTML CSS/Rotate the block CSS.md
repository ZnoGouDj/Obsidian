(Как повернуть блок на 45 градусов? CSS)

```css
div {
	height: 200px;
	width: 200px;
	background-color: green;
}

.block1 {
	transform: rotateX(45deg);
}
/* По Х не очень заметно на двухмерной странице*/
.block2 {
	transform: rotateY(45deg);
}
/* По Y тоже*/
.block3 {
	transform: rotateZ(45deg);
}
/* Так заметно*/
```

<div style="display: flex; justify-content: space-between;">
	<div style="transform: rotateX(45deg); height:200px; width: 200px; background-color: green; display: inline-block; text-align: center; vertical-align: center; line-height: 200px;">ПО ОСИ Х</div>
	<div style="transform: rotateY(45deg); height:200px; width: 200px; background-color: green; display: inline-block; text-align: center; vertical-align: center; line-height: 200px;">ПО ОСИ Y</div>
	<div style="transform: rotateZ(45deg); height:200px; width: 200px; background-color: green; display: inline-block; text-align: center; vertical-align: center; line-height: 200px;">ПО ОСИ Z</div>
</div>

### Как сделать вращения по осям заметными?
(to make rotation noticeable? CSS)

```css 
body {
	display: flex; 
	justify-content: center;
	align-items: center;
	height: 100vh;
	width: 100vh;
	/* СТАВИМ ВОТ ЭТО -- КАК БЫ ОТДАЛЯЕМСЯ ОТ СТРАНИЦЫ И БУДЕМ СМОТРЕТЬ НА НЕЕ СО СТОРОНЫ*/
	perspective: 500px;
}
div {
	height: 200px;
	width: 200px;
	background-color: green;
	/*И СТАВИМ ВОТ ЭТО*/
	transition: 1s all;
}
div:hover {
	/*И ВОТ ЭТО*/
	transform: rotateX(45deg);
}
```

Теперь элемент поворачивается при наведении, и у этого есть глубина.

<div style="display: flex; justify-content: center; align-items: center; height: 100px; perspective: 500px;">
	<div style="height: 200px; width: 200px; background-color: green; transition: 1s all; transform: rotateX(45deg)">
	</div>
</div>