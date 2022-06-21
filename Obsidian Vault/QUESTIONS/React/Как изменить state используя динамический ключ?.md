(to change state using dymanic key)

```js
inputChangeHandler(event) {
	this.setState({
		[event.target.name]: event.target.value
	})
}
```