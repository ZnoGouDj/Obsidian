#### Группировка по функциональности или маршруту

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

#### Группировка по типу файла

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

Это все субъективно, и лучше начать писать код, чем долго выбирать подход. Можно вообще скинуть все в одну папку и работать до тех пор, пока не станет очевидным сортировка файлов по папкам. 
Как правило, файлы, которые часто меняются вместе, следует держать ближе друг к другу. Этот принцип называется «совместное размещение».

Еще крутой метод — реэкспортировать файлы в index.js файле, чтобы экономить строки кода при множественных импортах.

```js
export { default as Pyramid } from './Charts/Pyramid';
export { default as Stacked } from './Charts/Stacked';


```