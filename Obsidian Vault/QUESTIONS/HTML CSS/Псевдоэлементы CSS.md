(pseudoelements CSS)

Позволяют стилизовать определенную часть псевдоэлемента.

<div>
	<ul style="column-count: 2;">
		<li>::after</li>
		<li>::before</li>
		<li>::cue</li>
		<li>::first-letter</li>
		<li>::first-line</li>
		<li>::selection</li>
		<li>::slotted</li>
		<li>::backdrop</li>
		<li>::placeholder</li>
		<li>::marker</li>
		<li>::spelling-error</li>
		<li>::grammar-error</li>
	</ul>
</div>

```css
/* Добавить стрелки после ссылок */
a::after {
  content: "→";
}

/* Добавить сердце перед ссылками */
a::before {
  content: "♥";
}

/* Стили для первой буквы элемента <p> */
p::first-letter {
  font-size: 130%;
}

/* Стили для первой строки элемента <p> */
p::first-line {
  color: red;
}
```

[[Псевдоклассы CSS]]