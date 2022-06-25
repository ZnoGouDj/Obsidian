(Миксины в препроцессорах CSS)

Кусочек CSS-свойств, который можно переиспользовать в других селекторах.

```css
@mixin transform($property) {
	-webkit-transform: $property;
	-ms-transform: $property;
	transform: $property;
}
.box { @include transform(rotate(30deg)); }
```