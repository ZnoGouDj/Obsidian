(Как использовать store внутри любого компонента? VUE)
(To use store inside any component? VUE)

После того как мы глобально зарегистрировали store в приложении, внутри любого компонента можем обратиться к нему так:
```js
getFromState() {
	return this.$store;
}
```

Также в [[Vuex]] есть возможность ЗАМАПИТЬ стейт, геттеры, экшны и мутации. 
После этого все замапленные функции будут доступны в компоненте.
```js
computed: {
	...mapState(),
	...mapGetters()
},
methods: {
	...mapMutations(),
	...mapActions()
}
```