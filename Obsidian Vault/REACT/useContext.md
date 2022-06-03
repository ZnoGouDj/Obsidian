это хук, который позволяет передавать данные по дереву компонентов, не перегружая код пропс-дриллингом. Хорош, когда надо например передать выбранный язык или UI-тему во многие компоненты. Иначе говоря, глобальные данные. 

```js
class App extends React.Component {
  render() {
    return <Toolbar theme="dark" />;
  }
}

function Toolbar(props) {
	return (
		<div>
		  <ThemedButton theme={props.theme} />    
		</div>
	  );
}

class ThemedButton extends React.Component {
  render() {
    return <Button theme={this.props.theme} />;
  }
} // и так далее === пропс дриллинг
```

```js
const ThemeContext = React.createContext('light');
class App extends React.Component {
  render() {
	  return (
		  <ThemeContext.Provider value="dark">    // обозначили только в одном месте     
			  <Toolbar />						 // остальные компоненты внизу уже в курсе
		  </ThemeContext.Provider>
    );
  }
}

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
	static contextType = ThemeContext;
  	render() {
    	return <Button theme={this.context} />;  
	}
}
```

**Важно не использовать контекст где попало!** Управление текущим языком, UI темой или кешем данных — это пример тех случаев, когда реализация с помощью контекста будет проще использования альтернативных подходов.

**Но обычно композиция компонентов (составление целого из частей) является более простым решением, чем контекст.** Так, вместо пропс-дриллинга можно передавать сам компонент (если только он использует конкретные пропсы).

```js
function Page(props) {
  const user = props.user;
  const userLink = (
    <Link href={user.permalink}>
      <Avatar user={user} size={props.avatarSize} />
    </Link>
  );
  return <PageLayout userLink={userLink} />;
}
```
вместо 
```js
<Page user={user} avatarSize={avatarSize} />
// ... который рендерит ...
<PageLayout user={user} avatarSize={avatarSize} />
// ... который рендерит ...
<NavigationBar user={user} avatarSize={avatarSize} />
// ... который рендерит ...
<Link href={user.permalink}>
  <Avatar user={user} size={avatarSize} />
</Link>
```

Можно передавать сразу несколько компонентов, создать для них разные «слоты»

```js
function Page(props) {
  const user = props.user;
  const content = <Feed user={user} />;
  const topBar = (
    <NavigationBar>
      <Link href={user.permalink}>
        <Avatar user={user} size={props.avatarSize} />
      </Link>
    </NavigationBar>
  );
  return (
    <PageLayout
      topBar={topBar}
      content={content}
    />
  );
}
```