(выбрать элемент span, который следует ПРЯМО за элементом input?)
(to select the span that's placed right after input?)

```html
<input type="text" />
<span>some text</span>
```
```css 
input + span { /* Такое применится ТОЛЬКО к span */
	color: red;
	font-size: 50px;
}
```

