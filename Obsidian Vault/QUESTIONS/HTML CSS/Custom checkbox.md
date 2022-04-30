```html
<div>
	<input type="checkbox" name="" id="check">
	<label for="check"></label>
</div>
```
```css
<style>
	input {
		display: none;
	}
	input:checked + label {
		color: red
	}
</style>
```

Or

```css
.red-input {
    accent-color: #9d3039;
    height: 20px; /* not needed */
    width: 20px; /* not needed */
}
```
```xml
<input class="red-input" type="checkbox" />
<!-- Radio button example -->
<input class="red-input" type="radio" />
```
```