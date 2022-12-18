<span style="font-weight: bold; color: #FE5C2B;">Local storage</span> и <span style="font-weight: bold; color: deepskyblue;">Session storage</span> позволяют хранить пары ключ/значение в браузере. 

<span style="font-weight: bold; color: #FE5C2B;">Local storage</span> сохраняются после перезапуска браузера, используется гораздо чаще.
<span style="font-weight: bold; color: deepskyblue;">Session storage</span> сохраняются только после обновления страницы.

Обa предоставляют одинаковые методы и свойства:

-  <span style="font-weight: bold; color: #FFB514;">setItem(key, value)</span> – сохранить пару ключ/значение.
-  <span style="font-weight: bold; color: #FFB514;">getItem(key)</span> – получить данные по ключу `key`.
-  <span style="font-weight: bold; color: #FFB514;">removeItem(key)</span> – удалить данные с ключом `key`.
-  <span style="font-weight: bold; color: #FFB514;">clear()</span> – удалить всё.
-  <span style="font-weight: bold; color: #FFB514;">key(index)</span> – получить ключ на заданной позиции.
-  <span style="font-weight: bold; color: #FFB514;">length</span> – количество элементов в хранилище.

<span style="font-weight: bold; color: #39d353;">Но ведь у нас уже есть куки. Зачем тогда эти объекты?</span>
-   В отличие от куки, объекты веб-хранилища не отправляются на сервер при каждом запросе. Поэтому мы можем хранить гораздо больше данных. Большинство браузеров могут сохранить как минимум 2 мегабайта данных (или больше), и этот размер можно поменять в настройках.
-   Сервер не может манипулировать объектами хранилища через HTTP-заголовки. Всё делается при помощи JavaScript.
-   Хранилище привязано к источнику (домен/протокол/порт). Это значит, что разные протоколы или поддомены определяют разные объекты хранилища, и они не могут получить доступ к данным друг друга.