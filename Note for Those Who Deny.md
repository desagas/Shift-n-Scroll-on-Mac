# The `git` Low
For those who say I do not know how to use git to `git push`, and `git add`, and `git commit --amend` ... I actually do know how to do this, but my build is broken, as MacOS has their only git, and has take over my git. I can do everything but push to github, for fear of sending my entire Mac OS to git, which, by the way, I know I can `.gitignore` a lot of files. I am not using it as an excuse, but, as long as you know why I have simply `git commit`ed these small changes here and there, it because I can not access github via git, which means I can not use `git commit --amend` to make the small changes without creating a huge backlog of history.

So, for now, I will be keeping my files and .git on my local, and will upload what and when I choose to.

### Do you `git` it yet?

# My Unorganized Notes for Git
*   `git rm -r --cached .` so important. If you at one point or another change your .gitignore, this corrects, and makes your repo match the new one. You follow this up with `git add .` and `git commit`.
*   The above point will not remove commit history. If you only have very few commit histories, you can do the following to remove all histories: 
    ```access transformers
    cd myrepo
    rm -rf .git
    
    git init
    git add .
    git commit -m "Removed history, due to sensitive data"
    
    git remote add origin github.com:yourhandle/yourrepo.git
    git push -u --force origin master
    ```
*   You can ONLY `git push -u --force origin master` IF master is NOT the default directory, because `master is friend`. To change the default origin directory, go to gitHub -> Settings -> Branches.
*   However, you can do it one file at a time if need be, to preserve the rest of the history of your repo ([Link to Source](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/removing-sensitive-data-from-a-repository)):
    
    1. Filter it out:
    
    ```access transformers
    git filter-branch --force --index-filter
    git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA --prune-empty --tag-name-filter cat -- --all
    ```
    2. Add it to .gitignore:
    ```    
    echo "YOUR-FILE-WITH-SENSITIVE-DATA" >> .gitignore
    git add .gitignore
    git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"
    ```
    3. Force-push to overwrite github repository:
    ```access transformers
    git push origin --force --all
    ```
    4. Verify over days or weeks that everything is perfect, be very sure, and then  dereference and garbage collect:
    ```access transformers
    git for-each-ref --format="delete %(refname)" refs/original | git update-ref --stdin
    git reflog expire --expire=now --all
    git gc --prune=now
    ```
    
*   Only edit files on one machine if possible. This makes conflicts so much easier to solve.
*   `git checkout branch` to get the branch you want to work on before you start working.
*   `git stash` to store changes to see last commit, and `git stash list / git stash apply #` to see what it is you have stashed. Add ALL files `git add` before commit with the intention of merging.
*   `git merge branch` can only be done if ALL your current files are committed, in both directories, AND, MAKE SURE you do this from the branch you are merging into.
*   