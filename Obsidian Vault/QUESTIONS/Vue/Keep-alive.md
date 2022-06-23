Допустим есть компонент родитель и два ребенка:

### App.vue
```html
<div>
	<button @click="currentComponent = 'FirstComponent'">First</button>
	<button @click="currentComponent = 'SecondComponent'">Second</button>
	
	<component :is="currentComponent"></component>
</div>
```
```js
import FirstComponent from '@/FirstComponent'
import SecondComponent from '@/SecondComponent'

export default {
	components: {
		SecondComponent, FirstComponent
	},
	data() {
		return {
			currentComponent: 'FirstComponent'
		}
	}
}
```

### First/SecondComponent идентичные - просто счетчики
```html
<div>
	<h1>1st component</h1>
	<h3>{{count}}</h3>
	<button @click="count++">Increment</button>
</div>
```

И если мы добавим каунт в First - а затем переключим на Second - счетчик сбросится, так как произошла перерисовка

### Решение - keep alive 
```html
<keep-alive>
	<component :is="currentComponent"></component>
</keep-alive>
```
При этом компонент не демонтируется, а живет вечно.