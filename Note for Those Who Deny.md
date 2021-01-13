# The `git`-low
For those who say I do not know how to use git to `git push`, and `git add`, and `git commit --amend` ... I actually do know how to do this, but my build is broken, as macOS has their only required git on my system messing with my new repos, and has taken over my git. I can do everything but push to github, for fear of sending my entire macOS to git, which, by the way, I know I can `.gitignore` a lot of files. I am not using it as an excuse, but, as long as you know why I have simply `git commit`ed these small changes here and there, it because I can not access github via git, which means I can not use `git commit --amend` to make the small changes without creating a huge backlog of history.

**More recently,** I found a way to circumvent this without sharing everything, and while remaining within. You can have a repo inside another repo.

### Do you `git` it yet?

# Initial Setup of `.git` on the **Terminal**
(Avoid using _gitHub Desktop_ during this process.)
1.  Set up your workspace.
1.  Initialize a new repository with:
    *   `git init`.
1.  Create your '.gitignore' file, and commit this first:
    *   `git add .gitignore`
    *   `git commit -m "Defining the repository.`
1.  Then, add the rest of your files to your repository:
    *   `git add .`
    *   `git commit -m "The intitial content commit."`
1.  Remote with **_https_** and verify that your **_https_** remote is correct:
    *   `git remote add origin https://github.com/yourhandle/yourrepo.git`
    *   `git remote -v` will show you your gitHub remote **_https_** addresses.
1.  Git names your local default branch to 'master'. Verify your default branch **_on gitHub_** is also 'master' (https://github.com/yourhandler/yourrepo/settings/branches).
1.  Push your master(default) branch to git:
    *   `git push -u --force origin master`
    
# The Basics of Using `git`
### Branches
*   Branches do not have folders, they are just references, but you can make it look like they have folders by naming them with forward slashes like 'features/thisfeature.'
*   Add new branches with:
    *   `git branch <newbranchname>`
    *   `git checkout -b <newbranchname>`
*   Navigate branches with:
    *   `git checkout <branchname>`
*   See a current branch and existing branches with:
    *   `git branch`
*   In _intelliJ_, at the very bottom LEFT corner, there is a very small tab that says .git. This will show you everything about your git. It will make branches look like folders if that is how you have structured it.
*   You can delete a branch, recommended after merging:
    *   `git branch -d localBranchName` for local repos, and
    *   `git push origin --delete remoteBranchName` for remote.

### Stashing
*   Save all current progress without committing:
    *   `git stash`
*   See list of stashes, top to bottom, newest to oldest:
    *   `git stash list`
*   Load saved progress / stashes to keep working:
    *   `git stash apply <stash#here>`
    
### Merging
*   This combines the two branches into one:
    *   `git merge <BranchComingIntoCurrentBranch>`, and make sure you are in the branch you want everything merged **_into_**.
*   You can only merge if all files **_with changes_** are committed to the branch you are adding to the current branch.

### Rebasing
*   You can create a base commit out of many smaller commits by:
    *   `git rebase --interactive <[>commit-hash>`, where <commit-hash> is the commit directly **_before_** (linearly in real time) the commit you want to start combing up to the current one. So, when combining the last 10 changes, you would use the commit code from the 11th one.

# Troubleshooting/Advice
### Conflicts
*   Sometimes a `git merge` can not complete, and it has errors:
    *   Try to merge, it fails, says resolve conflicts.
    *   Go into the files in question, they will now have <<<< and HEAD written at places in there. One is the original, one is the added content. Fix the file up to look exactly how you want it to look, save it, add it, commit it. Then, try the merge again.
*   You can avoid them by only editing and committing on one machine. This is not practical if multiple people are working on it.

### Commit behind Remote/Branch
*   Sometimes a `git push` will fail, because your commit is behind the remote or other branch. If this is the case:
    *   In the main branch, `git fetch origin` and the `git pull` will download the latest remote repo, and create conflicts. Follow guide above for conflicts, and then push again. If git ask for confirmation of old/vs new, accept. Good for seeing what conflicts exist before fixing them.
    *   Or, in a new branch `git fetch origin` and then `git checkout -b <newbranch> origin/<newbranch>` will add it to a new branch. Then, edit it, save it, add it, commit it, merge it into master, then `git push`.

### Unsorted
*   Access is denied while pushing, verify remote is **_https_**, not ssh. If so:
    *   `git remote set-url origin YourHttpsAddressHere` will sometimes work.
    *   `rm -rf .git` will remove git, in your working directory, and then setup again.
*   Remote **_https_**  is the browser address on your main **_gitHub repo_** page, at https://github.com/yourhandle/yourrepo.git.
*   When **_copying and pasting_** a project folder, the git contents also follow. If you do this, use `rm -rf .git`, and setup as described above. Best to '_create new project from an existing_' using your IDE. Do not use _gitHub Desktop_ to 'add an existing repository' until you have removed the old and set up the new git.
*   When updating your .gitignore file, use `git rm -r --cached .`. This corrects the files in your repo. Follow this up with `git add .` and `git commit`. **_This will not remove the file from the commit history,_**, so they will remain accessible to all who can view your commit history.
*   Remote with `--force` will work above, when both branch names match, but it will not work when erasing history, shown below, if the remote branch is the default branch. So, follow number 6 in the setup process.
*   You can only navigate to different branches when uncommitted changes are `git stash`.



# Warnings
*   Using _gitHub Desktop_ to revert commits is nice, but it does a hard reset, and all changes will be removed, including files added.  It does, however, create a new commit, so you can revert to any commit before it with `git reset --hard <commit>`.
*   Careful when using `--hard` in any context. It usually removes all changes, additions, deletions, that are not stopped by your .gitignore file.
*   Using `rm -rf .git` will probably remove stashes and branches not checked out. Existing files in your working directory will not be deleted.

# Wipe Your git Repository Commit History
(See warnings above **_before_** attempting this.)
*   If sensitive info has been added to your repo, and your commit history, or if you only have very few commit histories, you can do the following to remove all commit histories from your entire repo (do not do this on older repos with history, your story will be lost): 
    ```
    cd myrepo
    rm -rf .git
    
    git init
    git add .
    git commit -m "Removed history, due to sensitive data"
    
    git remote add origin https://github.com/yourhandle/yourrepo.git
    git push -u --force origin master
    ```
*   However, you can do it one file at a time if need be, to preserve the rest of the history of your repo history (I have not tested this) ([Link to Source](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/removing-sensitive-data-from-a-repository)):
    ```
    1.  Filter it out:    
        git filter-branch --force --index-filter
        git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA --prune-empty --tag-name-filter cat -- --all```
    
    2.  Add it to .gitignore:
        git add .gitignore
        git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"
    
    3.  Force-push to overwrite github repository:
        git push origin --force --all
    
    4.  Verify over days or weeks that everything is perfect, be very sure, and then dereference and garbage collect:
        git for-each-ref --format="delete %(refname)" refs/original | git update-ref --stdin
        git reflog expire --expire=now --all
        git gc --prune=now
    ```
