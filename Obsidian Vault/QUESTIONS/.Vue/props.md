(what is props?)

Некоторые входные параметры, которые может принимать компонент.
Являются свойствами компонента, и мы можем их использовать и в методах, и в любом месте компонента. 

```js
Vue.component('blog-post', {
	// Список ожидаемых пропсов прописывается в "пропс", может быть любое количество
	props: ['title'], 
	template: '<h3>{{ title }} </h3>'
})
```
```html
<blog-post title="My journey with Vue"></blog-post>
<blog-post title="Blogging with Vue"></blog-post>
<blog-post title="Why Vue is so fun"></blog-post>
```

С помощью пропсов мы можем использовать компонентный подход и передавать данные из родителя в ребенка.