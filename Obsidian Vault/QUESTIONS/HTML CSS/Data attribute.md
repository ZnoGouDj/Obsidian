(Для чего предназначен атрибут data?)

Для хранения значений. Например, для создания всплывающих подсказок без применения [[JavaScript]]. 

<p style="text-align: center; font-size: large; font-weight: bold;">Правило создания</p>

Пишем ключевое слово **data**, затем **название** через дефис 
```html
<div data-description="file description"></div>
```

Теперь попробуем сделать так, чтобы при наведении на блок, выпадала ПОДСКАЗКА

Для этого воспользуемся [[Псевдоклассы CSS]] и [[Псевдоэлементы CSS]] соответственно, и в значение **content** с помощью функции **attr** поместим значение **data-description**

```css
div:hover::after {
	content: attr(data-description);
	position: absolute;
	top: 100%;
	background-color: lightgray;
}
```

И теперь при наведении на блок будет выпадать снизу подсказка "file description"