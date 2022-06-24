Определяет ключевые кадры, по которым будет работать анимация

Указывается начальная точка, что будет в ней происходить, и конечная точка. 
Также их можно указывать в процентах, и можно на каждом этапе создавать отдельный ключевой кадр. 

Допустим есть блок **div**:
```css
.item {
	width: 200px;
	height: 200px;
	background: lightgray;
	font-size: 50px;
	animation: rotate 1s infinite;
}

@keyframes rotate {
	from {
		transform: rotateX(0deg);
	}
	to {
		transform: rotateX(360deg);
	}
}
```

Теперь блок будет вращаться по оси Х.