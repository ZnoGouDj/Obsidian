![[git_merge.gif]]
![[git_rebase.gif]]

<b style="color: mediumvioletred;">Merge</b>
Если мы создали ветку для фичи и хотим слить ее с мастером, то нам не нужны все эти промежуточные коммиты и мы можем вмержить.
```bash
git checkout master
git merge --squash cool-feature 
```

<b style="color: deepskyblue;">Rebase</b>
Если происходит то же самое, но кто-то сделал изменение в уже влил его в мастер, то следует подстроиться под эти изменения, спулить мастер, и перевести (rebase) указатель на вот этот последний спулленный коммит, чтобы не терять хронологию.
```bash
git checkout master 
git pull 

git checkout feature
git rebase master

git checkout master
git rebase feature

git push
```

Отличия:
1) Итоговая структура истории будет отличаться (в случае <b style="color: mediumvioletred">merge</b> будут ветки, в случае <b style="color: deepskyblue;">rebase</b> нет)
2) <b style="color: mediumvioletred">Merge</b> создаст новый дополнительный коммит (узел в дереве)
3) <b style="color: mediumvioletred">Merge</b> и <b style="color: deepskyblue;">rebase</b> отображают конфликты по-разному. <b style="color: mediumvioletred">Merge</b> вываливает все конфликты сразу, а  <b style="color: deepskyblue;">rebase</b> из каждого коммита по очереди

Выбираем мерж или ребейз в зависимости от того, как хотим чтобы выглядела наша ИСТОРИЯ. 
Теоретически, если проект огромный, может быть неудобно отслеживать историю, так как остается много веток после мержей и лучше выбирать rebase. 

https://www.youtube.com/watch?v=f1wnYdLEpgI
https://stackoverflow.com/questions/804115/when-do-you-use-git-rebase-instead-of-git-merge