Это паттерн для управления состоянием
И он служит централизованным хранилищем данных для всех компонентов
При этом нам не нужно передавать данные по иерархии сверху-вниз (пропс-дриллинг)

Vuex гарантирует, что состояние может быть изменено только предсказуемым образом, а именно с помощью МУТАЦИЙ и [[Action]]

### State & Getters 

Vuex использует единое дерево состояние (когда один объект содержит все состояние приложения и служит единственным источником истины). 
Это также означает, что в приложении будет одно хранилище. 

 В **State** мы храним данные
 
 **Getters** это некоторые [[computed]] свойства, аналогичные свойствам из компонента. 
 Внутри себя они проводят вычисления над данными из State и аналогичным образом кеширует результат до тех пор, пока одна из зависимостей не изменится
 
### Mutations и actions - отличия

Грубо говоря МУТАЦИИ - для синхронностей, ACTIONS - для асинхронностей.

**Мутации** - единственный способ изменить состояние.
Представляет из себя функцию, которая внутри себя изменяет поля и состояние.
Позволяют сделать процесс изменения состояния более прозрачным и явным.
Являются синхронными, не могут содержать асинхрон. 

**Actions** - похожи на мутации, но он содержит сайд-эффекты, запросы на сервер, таймеры. 
Но при этом внутри себя вызывают мутации, чтобы как-то изменить состояние.
