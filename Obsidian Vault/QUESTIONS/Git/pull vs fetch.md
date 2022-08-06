**Git pull** - забирает изменения или коммиты из конкретной ветки и обновляет ветку в локальном репо
**Git fetch** - делает то же самое, но он забирает ВСЕ НОВЫЕ коммиты из нужной ветки и хранит их в новой ветке в твоем локальном репо. Если ты хочешь увидеть эти изменения в твоей ветке - надо еще сверху прописать git merge

То есть пулл - сразу в чистовик, а фетч - в черновик а затем если все ок в чистовик



**git fetch** updates your remote-tracking branches under `refs/remotes/<remote>/`. This operation is safe to run at any time since it never changes any of your local branches under `refs/heads`.

**git pull**  brings a local branch up-to-date with its remote version, while also updating your other remote-tracking branches.

From the Git documentation for [`git pull`](http://git-scm.com/docs/git-pull):

> In its default mode, `git pull` is shorthand for `git fetch` followed by `git merge FETCH_HEAD`.