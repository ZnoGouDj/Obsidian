(как получить DOM-элемент? VUE)
(to receive DOM-element? VUE) 

Рефом

В template:
```html
<input ref="inputref" type="text" />
<button @click="getRef">Get element</button>
```

В script:
```js
export default {
	methods: {
		getRef() {
			this.$refs.inputref.focus()
			console.log(this.$refs.inputref)
		}
	}
}
```

И при клике на кнопку будет отрабатывать консоль лог и фокусироваться на инпут.