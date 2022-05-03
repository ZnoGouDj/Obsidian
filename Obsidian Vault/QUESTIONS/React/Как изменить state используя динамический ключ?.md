```js
inputChangeHandler(event) {
	this.setState({
		[event.target.name]: event.target.value
	})
}
```