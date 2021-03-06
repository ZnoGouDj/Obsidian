Это атрибуты тега *script*, которые решают проблему скорости загрузки.
	
### defer сохраняет порядок скриптов.

```html
<script src="script.js" defer></script>
```

### async выполняется по порядку "кто быстрее загрузится"

```html
<script src="script.js" async></script>
```

Еще можно юзать сразу оба атрибута:
```xml
<script src="script.js" async defer></script>
```
в таком случае будет юзаться **defer** поведение, если не поддерживается **async**

## Вывод

Оба не блокируют отрисовку страницы, то есть оптимизируют ОТРИСОВКУ.

НО:
- отличается порядок загрузки
- *DOMContentLoaded грузится ПОСЛЕ defer, и РАНДОМНО в случае async*

На практике DEFER – для скриптов нуждающихся в DOM целиком, или если нам важен порядок скриптов. ASYNC – для каких нибудь счетчиков или рекламы, порядок которых не важен.

Важно сделать страницу рабочей без скриптов, то есть сделать неработающие кнопки/индикации загрузок и тд.
