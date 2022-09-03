(особенности использования v-model в Vue 2 и Vue 3)

<p style="text-align: center; font-weight: bold; font-size: xx-large;">V-MODEL</p>

В Vue 2 можно использовать ВСЕГО ОДИН **v-model**
```js
v-model // ⬅️➡️ value (по умолчанию работает с атрибутом value)
```
Т.к. он позволяет сделать двустороннее связывание, также необходимо прослушивать некоторые события. 
По умолчанию в Vue 2 это **onInput()**

В Vue 3 можно использовать сколько угодно v-model
При этом можно его использовать с ЯВНЫМ указанием атрибута 
```js
v-model:title // ⬅️➡️ title
v-model:body // ⬅️➡️ body
v-model:email // ⬅️➡️ email
```
или оставить без указания 
```js
v-model // ⬅️➡️ modelValue (по умолчанию тогда будет modelValue)
```

<p style="text-align: center; font-weight: bold; font-size: xx-large;">COMPONENT CHANGE</p>


В Vue 2 для того, чтобы компонент изменять, компонент, к которому применяем **v-model** должен Эмитить событие Инпут:
```js 
this.$emit('input', newValue)  // в дочернем компоненте
```

В Vue 3 для того, чтобы изменить значение модели, нам необходимо Эмитить событие, которое задается ПО ШАБЛОНУ: 
```js
this.$emit('update:title', newVal)
this.$emit('update:body', newVal)
this.$emit('update:email', newVal)
```
Если же название атрибута мы не указали, то Эмитим значение modelValue:
```js
this.$emit('update:modelValue', newValue)
```