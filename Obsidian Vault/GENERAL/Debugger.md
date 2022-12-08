<p style="color: #FA9BBB; font-weight: bold; text-align: center;">Ставим брейкпойнт, и когда программа дойдет до этого места, она ОСТАНОВИТ скрипт и мы сможем посмотреть на текущие данные</p>

![[breakpoint.png]]
Мы можем наводить на определенные переменные курсор, и видеть их текущие значения. 
В скриншоте выше в values будет undefined, т.к. breakpoint останавливает код ДО выполнения строчки, на которой он стоит. 
<p style="color: deepskyblue; font-weight: bold;text-align: center;">Чтобы двигать выполнение кода, используем кнопки справа от окна с кодом:</p>
1) F8 - Resume script execution - продолжает выполнение до след. breakpoint, если он есть.
2) F10 - Step over next function call - переходит на следующую строчку
3) F11 - Step into next function call - переходит в следующую функцию
4) F9 - Step - шаги внутри функции ПОСЛЕ нажатия F11

В момент остановки кода, можем ЗАЙТИ В КОНСОЛЬ и ввести нужное значение для проверки
```bash
values[0]
"30"
```
Либо можно нажать ESC (возможно дважды) и **вызвать консоль прямо под вкладкой Sources.**
<p style="color: #FA9BBB; font-weight: bold;text-align: center;">Если хотим перейти к функции, которая нас интересует, можно навести на нее и нажать на ссылку (app.js:9)</p>

![[DEBUG_enter_the_func 1.png]]

<p style="color: deepskyblue; font-weight: bold;text-align: center;">Можем нажимать на Call Stack и перемещаться по слоям выполнения функций</p>
<p style="color: #FA9BBB; font-weight: bold;text-align: center;">Можем прямо в моменте breakpoint редактировать файлы, предполагая что это решит проблему например, и смотреть результат</p>

![[DEBUG_edit_file.png]]\
Тут например мы добавили **"+"** после назначения value1 и **parseInt** после value2.
Затем жмем **CTRL+S** и можем продолжить выполнение (F8).
Если при этом хотим временно пропускать breakpoints, то можем нажать CTRL+F8 для игнора.
<p style="color: deepskyblue; font-weight: bold;text-align: center;">Можем в поле Watch на "+" добавить переменную и следить за ее состоянием всю дорогу дебага</p>
Также можно еще и условия прописывать, например **values[0] + values[1]** и он будет следить за результатом данного выражения.

<p style="color: #FA9BBB; font-weight: bold;text-align: center;">Можем создавать breakpoint по условию:</p>

![[DEBUG_conditional_break.png]]

И там в поле **"Expression to check before pausing"** пишем например **x > 50**

<p style="color: deepskyblue; font-weight: bold;text-align: center;">Debugger и breakpoint по событию</p>

![[DEBUG_debugger.png]]
Добавив debugger. Удобно, когда кода МНОГО, и искать нужное место для breakpoint проще в редакторе кода, а не внутри devtools.

ЛИБО можем обратиться к вкладке справа **"Event Listener Breakpoints"**. И выбрав например Mouse > click код будет останавливаться на клике **СЛУШАТЕЛЬ ДЛЯ КОТОРОГО ЕСТЬ У ТЕБЯ В НАПИСАННОМ КОДЕ** (А НЕ НА КАЖДОМ КЛИКЕ ПО СТРАНИЦУ)

<p style="color: #FA9BBB; font-weight: bold;text-align: center;">Можем отследить маршрут до конкретного места, добавив console.trace() в коде:</p>
В таком случае в консоли вызовется список вызовов функций до текущей (в которой стоит этот console.trace()) и ссылки к ним.

<p style="color: deepskyblue; font-weight: bold;text-align: center;">Можем отображать html-элемент в консоли, вписывая $0 - $4 (запоминает максимум 5 кликнутых элементов во вкладке Elements)</p>
А также например **$('.current-class')**