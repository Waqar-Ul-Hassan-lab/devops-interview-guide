## Git Clone vs Fork
- Clone makes a local copy like when to execute some code or have to use a repo as tool.
- Fork make a new replica repo on your account separately and you make changes to it and then raise a PR.

## Git Fetch vs Pull
- When a repo is forked, some new changes might have made by owner, so to fetch them locally and save track in the .git file, git fetch is uesd and them git merget or git rebase to combine the whole code and gets the updated one.
- The whole work of all phases of fetch command is done at once by using one command only Git Pull. It fetches the new changes of code and also merge it automatically by one command.

## Git Merge vs Rebase 
- For git rebase, first chekcout to the specified branch, then run `git rebase origin/main`, it will first show the all latest commits of main branch and then your current working branch commits. This is also called as Linear commit approach.
- Similarly for the `git merge origin/main`, all of the commits will be shown in the choronological orders like the order in wihch they were done. Unlike the rebase, which shows the list of main branch commits first, then your current working branch commits.
- Merge combines two branches by creating a new commit and preserving the chronological order.
- Rebase reapplies your branch's commit to other branch to rewrite history in a clean linear fashbion.
- `Git merge combines two branches and creates a new merge commit, preserving the full history`
- Merge is not destructive and good for collaborations and teamworks where history matters like in public projects.
- Rebase is good for local and hobby projects as it rewrites the history.
- `Git rebase moves your branch commits on top of another branch, creating a cleaner, linear history.`

## Git Branch
- The basic workflow of brancing is : 
- `Main branch` is for the stable production code & active development.
- `Feature branch` is for the development of new features
- `Release branch` is for the release of new features. Also release a tag.
- `Hotfix branch` is for the quick bug fixes

- Trunk based development: is a branching model in which developers merge small changes into a central "trunk" (main) branch frequently. This approach emphasizes continuous integration and minimizes the risks associated with large, infrequent merges.

## 3 Git challenges:
- Git branching 
- Git Access Control
- .git, .gitignore and Webhooks

## Git Access Control
- Who can Read the code
- Who can write : Push and create branches
- Who can review the code
- Who will maintain the code
- Who will be the maintainer
- Who will be the owner/Admin

## WebHooks
- Webhooks are used to notify a specified URL when a specific event happens in a repository.
- They are mostly used for the CI/CD piplines.
- Example include:
    - Jenkins
    - ArgoCD
    - TeamCity

## Git Merge Conflict
- A merge conflict occurs when Git cannot automatically resolve differences between two branches during a merge or rebase operation.
- Conflict occurs when both branches have modified the same section of the same file, or one branch has deleted a file that the other branch modified.
- To resolve the conflict:
    - Identify the conflicting files
    - Open the conflicting files and look for conflict markers (<<<<<<<, =======, >>>>>>>)
    - Edit the file to keep the changes you want
    - Remove the conflict markers
    - `git add <file>` to stage the resolved file
    - `git commit` to complete the merge
- If it is not you who did make the changes to these files, then tell those two persons, 10 min communication, Resolve the conflicts, Test the code and raise the PR.

## Our and Their Merge Strategy
- If accept current branch change, it is called our strategy.
- If accept incoming branch change, it is called their strategy.

## Git Tags
- Git tags are used to mark specific points in the repository's history as important.
- They are like the bookmarks in the code to mark specific version of the code.
- Mostly used for the version control.

## Combine Multiple Commits into One Commit
- use the command `git rebase -i HEAD~n` where n is the number of commits you want to combine.
- for example : `git rebase -i HEAD~3` will show the last 3 commits in the editor
- For the three commits, keep the first `pick` and make the other two to `squash`
- After this it will ask for the commit to write , write it and save it
- Now use the command `git push -f` to push the changes.
- This work for local as well as remote

## Ten Git Daily Used Commands
- git clone : to make local copy
- git status : to check the status of the code
- git add : to add the code to the staging area
- git commit : to commit the code
- git push : to push the code to the remote repository
- git pull : to pull the code from the remote repository
- git checkout : to switch between branches
- git branch : to create a branch
- git merge : to merge two branches
- git log : to see logs and commit history

## .gitignore File
- It is used to ignore the files that are not to be pushed to the remote repository.
- Example : node_modules, .env files, logs, etc
- In the exampler.txt file, i have added the node_modules and .env files to be ignored.

## .git directory
- The brain of the git
- Stores the entire commit history, branches, configuration, tags etc
- Created automatically when you run `git init`
- It is a hidden directory, so you need to run `ls -la` to see it
- Lossing .git will loss all tracking and all

## One can or cannot restore the .git directory

## Secret pushed accidentally
- The simplest solution is to remove the secret from the file, commit the change, and then force push the commit to the remote repository.
- `git rm --cached <file>`
- `git commit -m "Removed sensitive data from <file>"`
- `git push -f origin <branch_name>`

- find the path of the secret 
- find that specific commit
- clean that specific commit
- push the changes

- Use the pre-commit hooks
- use the git secret management tools
- Add checks by CodeRabbit & GitHub Secret Scanner