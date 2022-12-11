
<span style="font-weight: bold; color: #FE5C2B;font-size:17px;">Группировка по функциональности или маршруту</span>

```
feed/
  index.js
  Feed.js
  Feed.css
  FeedStory.js
  FeedStory.test.js
  FeedAPI.js
profile/
  index.js
  Profile.js
  ProfileHeader.js
  ProfileHeader.css
  ProfileAPI.js
```

<span style="font-weight: bold; color: deepskyblue;font-size:17px;">Группировка по типу файла</span>

```
api/
  APIUtils.js
  APIUtils.test.js
  ProfileAPI.js
  UserAPI.js
components/
  Avatar.js
  Avatar.css
  Feed.js
  Feed.css
  FeedStory.js
  FeedStory.test.js
  Profile.js
  ProfileHeader.js
  ProfileHeader.css
```

<span style="font-weight: bold; color: #FFB514;">Это все субъективно, и лучше начать писать код, чем долго выбирать подход.</span> Можно вообще скинуть все в одну папку и работать до тех пор, пока не станет очевидным сортировка файлов по папкам. 
Как правило, файлы, которые часто меняются вместе, следует держать ближе друг к другу. Этот принцип называется «совместное размещение».

Еще крутой метод — реэкспортировать файлы в index.js файле, чтобы экономить строки кода при множественных импортах.

```js
export { default as Pyramid } from './Charts/Pyramid';
export { default as Stacked } from './Charts/Stacked';


```