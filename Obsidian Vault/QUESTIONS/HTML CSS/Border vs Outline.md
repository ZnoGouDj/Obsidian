(ГРАНИЦА ПРОТИВ КОНТУРА)

<p style="font-size: xx-large; forn-weight: bold; text-align: center">BORDER</p>
<div class="border" style=" width: 200px; height: 200px; background-color: red; border: 8px ridge rgba(170, 50, 220, .6); border-radius: 2rem;"></div>

```css
.border {
	width: 200px;
	height: 200px;
	background-color: red;
	border: 8px ridge rgba(170, 50, 220, .6);
	border-radius: 2rem;
}
```

Рамка через BORDER является частью элемента и занимает место в макете.

<p style="font-size: xx-large; forn-weight: bold; text-align: center">OUTLINE</p>
<div class="outline" style="width: 200px; height: 200px; background-color: red; outline: 8px ridge rgba(170, 50, 220, .6); border-radius: 2rem;"></div>

```css
.outline {
	width: 200px;
	height: 200px;
	background-color: red;
	outline: 8px ridge rgba(170, 50, 220, .6); 
	border-radius: 2rem; // радиус может задаться только тут, outline-radius нет
}
```

Outline (контуры) не занимают места, поэтому они никак не влияют на макет документа.
