# Reset all changes after last commit in git

First reset the changes

***git reset HEAD --hard***

then clean out everything untracked. If you want to keep files that are not tracked due to .gitignore, be careful with this command.

***git clean -fd***
