Позволяет выбрать коммит из ОДНОЙ ветки и применить его к другой ветке. 
В противовес MERGE & REBASE, которые применяют много коммитов на другую ветку по сути.

1.  Make sure you are on the branch you want to apply the commit to.
    
    ```
     git switch master
    ```
    
2.  Execute the following:
    
    ```
     git cherry-pick <commit-hash>
    ```