**Эндпоинт** — принимает параметры и возвращают данные Клиенту. Это обращение к маршруту отдельным [[HTTP]] методом.  

**Разберем URL**
<span style="font-weight: bold; color: #FFB514;">http://example.com/wp-json/wp/v2/posts/123</span>

Здесь <span style="font-weight: bold; color: deepskyblue;">wp/v2/posts/123</span> — это маршрут, а <span style="font-weight: bold; color: deepskyblue;">/wp-json</span> — это базовый путь самого [[RestAPI]].

Этот маршрут имеет 3 эндпоинта:
    -   <span style="font-weight: bold; color: greenyellow;">GET</span> — запускает метод <span style="font-weight: bold; color: #FE5C2B;">get_item()</span> и возвращает данные поста Клиенту.
    -   <span style="font-weight: bold; color: greenyellow;">PUT|PATCH|POST</span> — запускает метод <span style="font-weight: bold; color: #FE5C2B;">update_item()</span>, обновляет данные и возвращает их Клиенту.
    -   <span style="font-weight: bold; color: greenyellow;">DELETE</span> — запускает метод <span style="font-weight: bold; color: #FE5C2B;">delete_item()</span>, удаляет пост и возвращает только что удаленные данные Клиенту.

Если сделать GET запрос к корневому маршруту <span style="font-weight: bold; color: #FFB514;">http://example.com/wp-json/</span>, мы получим JSON ответ, в котором видно какие доступны маршруты, и какие доступны эндпоинты для каждого из них. При этом маршрут тут это `/` (корень), а при GET запросе он становится эндпоинтом (конечной точкой).