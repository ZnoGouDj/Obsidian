**useEffect** представляет собой совокупность методов `componentDidMount`, `componentDidUpdate`, и `componentWillUnmount`.

Существует два распространённых вида побочных эффектов в компонентах React: компоненты, которые требуют и не требуют сброса.

**ТРЕБУЮТ** Например, **нам может потребоваться установить подписку** на какой-нибудь внешний источник данных. В этом случае очень важно выполнять сброс, чтобы не случилась [[утечка памяти]]

**НЕ ТРЕБУЮТ** Сетевые запросы, изменения DOM вручную, логирование. После того, как мы запустили их, можно сразу забыть о них, ведь больше никаких дополнительных действий не требуется.

```js
 useEffect(() => {    
	 function handleStatusChange(status) {      
		 setIsOnline(status.isOnline);    
	 }    
	 ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);    
	 // Указываем, как сбросить этот эффект:    
	 return function cleanup() {      
		 ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);    
	 };  
 });
```

В примере выше return очистит подписку при демонтировании компонента.