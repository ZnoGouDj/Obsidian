По умолчанию действия Redux обрабатываются синхронно, и этого недостаточно для приложений, т.к. надо как-то взаимодействовать с внешним миром.
Поэтому Redux позволяет использовать промежуточное ПО между обрабатываемым действием и действием, которое достигает редюсеров.

Существует две очень популярные библиотеки промежуточного ПО, поддерживающие побочные эффекты и асинхронные действия: Redux Thunk & Redux Saga

Redux Thunk — это [[Middleware]], позволяющее вызывать [[action creator]], которые возвращают функцию вместо объекта. Функция принимает метод dispatch как аргумент, чтобы после того, как асинхронная операция завершится, использовать его для диспатчинга обычного синхронного экшена, внутри тела функции.