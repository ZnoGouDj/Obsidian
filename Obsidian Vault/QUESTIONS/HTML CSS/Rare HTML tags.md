1) <span style="font-weight: bold; color: #FE5C2B;">datalist</span>

<input type="text" list="techs" />

<datalist id="techs">
	<option value="HTML"></option>
	<option value="CSS"></option>
	<option value="JavaScript"></option>
</datalist>

2) <span style="font-weight: bold; color: deepskyblue;">sub & sup</span>

H<sub>2</sub>O
E = MC<sup>2</sup>

3) <span style="font-weight: bold; color: #FE5C2B;">details & summary</span>

```html
<details open>
	<summary>You sure you want to open it?</summary>

	<p>Lorem ipsum dolor sit amet consectetur</p>
</details>
```

Should open/close p tag, not working here though

4) <span style="font-weight: bold; color: deepskyblue;">dialog</span>

```html
<style>
	dialog::backdrop {
		background: rgba(0,0,0,0.5);
	}
</style>

<button id="open">Show</button>

<dialog open>
	<h2>Header</h2>

	<p>Lorem ipsum bla bla </p>
</dialog>

<button>Close</button>

<script>
	const openBtn = document.querySelector('#open');
	const dialog = document.querySelector('dialog');
	const closeBtn = dialog.querySelector('button');
	openBtn.onclick = () => dialog.showModal();
	closeBtn.onclick = () => dialog.close();
</script>
```

Создает затемняющее фон модальное окно.

5) <span style="font-weight: bold; color: #FE5C2B;">figure</span>

<figure>
	<img src="https://source.unsplash.com/random/100x100" alt="" />

	<figcaption>This is random picture</figcaption>
</figure>

6) <span style="font-weight: bold; color: deepskyblue;">picture</span>

```html
<picture>
	<source media="(max-width: 500px)" srcset="https://source.unsplash.com/random/100x100"/>
	
	<img src="https://source.unsplash.com/random/200x200" alt="" />
<picture/>
```

To show different content with different dimensions

<span style="font-weight: bold; color: #FFB514;">Поддержка тегов по caniuse: </span>
datalist **97%** 
sub, sup **51%** 
details **97%** 
summary **80%** 
Dialog **92%** (к сожалению сафари только с 15 версии поддерживает) 
figure **95%**
picture **97%**