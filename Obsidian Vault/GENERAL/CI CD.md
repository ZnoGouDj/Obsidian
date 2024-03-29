**CI/CD (<span style="font-weight: bold; color: #FE5C2B;">CONTINUOUS INTEGRATION</span>, <span style="font-weight: bold; color: deepskyblue;">CONTINUOUS DELIVERY</span>)**

Проверяет, что новый добавленный код не сломал приложение (грубо говоря).

Допустим мы сделали новый функционал, сделали новую ветку для этого, сделали пулл реквест. Затем пулл реквест проверили, но там проверяется КАЧЕСТВО кода, а не ломает ли код приложение. 

<span style="font-weight: bold; color: #FFB514;">Как вообще проверить стабильность работы?</span>
1) Сделать сборку приложения
2) Прогнать тесты
3) Прогнать линтеры (проверить качество написанного)
4) Проверить типизацию (если например используется TypeScript)

Для всех этих действий обычно есть скрипты в package.json (build, test, lint и так далее), и ЕСЛИ ИХ ВСЕХ ПРОГНАТЬ, то мы можем убедиться, что все надежно. 

ПРОБЛЕМА в том, что можно что-то забыть, и в том что прогонять долго и дорого. Проще автоматизировать. 

Поэтому настроенный CI снимает ответственность с разработчиков за забытые проверки, и запретит мержить ветку до тех пор, пока все тесты не будут пройдены. 

ЭТО ВСЕ ПРО ЛЕВУЮ ЧАСТЬ (<span style="font-weight: bold; color: #FE5C2B;">CONTINUOUS INTEGRATION</span>)

С <span style="font-weight: bold; color: deepskyblue;">CONTINUOUS DELIVERY</span> еще проще.

Когда наш код проревьюили, увидели, что все чеки зеленые, тогда мы мержим нашу ветку, ЗАТЕМ идет сборка нашего приложения и дальнейшая публикация этой сборки на тестовый ИЛИ продакшн контур. 
То есть это касается как обычной разработки, так и релизов. При релизе мы также прогоняем тесты, линтеры и только потом делаем резил. 
Например на тестовом контуре мы можем релизиться КАЖДЫЙ день, а на продакшн там РАЗ В НЕДЕЛЮ. Зависит от процессов в команде. 