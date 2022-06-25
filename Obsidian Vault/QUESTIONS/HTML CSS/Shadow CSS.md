#### Как сделать тень падающую от блока? CSS
(to make the shadow from the block? CSS)

```css
div {
	height: 200px;
	width: 200px;
	background-color: green;
	/* and here we go */
	box-shadow: 4px 4px 8px yellow;
	/* 4px - смещение по оси Х и У, 8px - размытие тени и цвет */
}
```

<div style="display:flex; justify-content: center;"><div style="height: 200px; width: 200px; background-color: green; box-shadow: 4px 4px 8px yellow;"></div></div>

#### Как сделать тень падающую от текста? CSS
(to make the shadow from the text? CSS)

```css
h1 {
	text-shadow: 2px 2px 4px yellow;
}
```

<h1 style="text-shadow: 4px 4px 8px yellow; text-align: center;">Hello world!</h1>