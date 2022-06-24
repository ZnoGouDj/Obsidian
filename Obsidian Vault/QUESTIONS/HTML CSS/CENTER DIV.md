(how to center div?! CSS)
(Как отцентровать блок по горизонтали и вертикали?!)

<p style="text-align: center; font-weight: bold; font-size: large;">CLASSIC WITH ABSOLUTE</p>

```html
<article>
	<div class="classic">center me</div>
</article>
```
```css
.classic {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
}
```

<p style="text-align: center; font-weight: bold; font-size: large;">FLEXBOX</p>

```html
<article class="flex">
	<div>center me</div>
</article>
```
```css
.flex {
	display: flex;
	justify-content: center;
	align-items: center;
}
```

<p style="text-align: center; font-weight: bold; font-size: large;">GRID</p>

```html
<article class="grid">
	<div>center me</div>
</article>
```
```css
.grid {
	display: grid;
	place-items: center;
}
```