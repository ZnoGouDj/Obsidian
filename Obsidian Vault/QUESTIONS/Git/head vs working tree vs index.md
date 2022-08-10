**Working tree** — (рабочее дерево) — это файлы, над которыми мы сейчас работаем.
**Index** — это место, где мы располагаем файлы, которые хотим коммитить в репозиторий git. 
```bash
git ls-files -s 
```
**HEAD** указывает на текущую ссылку на ветку, которая является указателем на последний коммит, сделанный в этой ветке.
```bash
git ls-tree -r HEAD
```
![[git_data_transport.jpg]]