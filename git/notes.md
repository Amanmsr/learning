# GIT

## Starting with Git
git config --global user.email "you@example.com"<br />
git config --global user.name "Your Name"<br />
git config --global core.editor nvim<br />

git config --list          (for current repo)
git config --global --list (only the globals)

(NOTE: omit --global to have this info only for the current repo)

> git log     (show all commits and commit messages)
> git status  (status of the local repo)

## Getting help
> git help <command>
ex: git help commit

## Remotes
we can add remotes which is a tracked repo
remote can be a URL for a remote repo on github or it can be a local repo (bare repo)

git remote -v (list remotes)
git remote get-url <remote_name> (get the url for a remote)
git remote rename <old> <new> (rename a remote)
git remote set-url remote_name <new_url> (change the url)

**NOTE**: for a repo that is tracking a bare repo on local machine, the URL is just the path to the bare repo
when the entire thing is moved into a new machine the old path may be invalidated, in that case we need to 
use set-url to update the url for 'origin'

## Bare Repo
### git init --bare <reponame>
bare repo does not have a worktree which means we can't do work in this directory.
Its there for several people to collaborate and use the 'bare repo' as a remote repo.
we can clone the bare repo and do our work, then push those changes into the bare repo.
Someone else can pull these changes.

Example: 
### git clone <barerepo> <nonbarerepo>
### cd <nonbarerepo>
### touch filename
### git add filename
### git commit -m "msg"
### git push
(now bare repo will contain this info)
anyone else who clones the bare repo now will see the added files

Example:
barerepo
repo1
repo2
...

repo1 can make changes and do 'git push' 
repo2 (also cloned from 'barerepo') can do 'git pull' to see changes done by repo1
similarly, repo1 can run 'git pull' to see changes by repo2
we can have repo1, ..., repoN cloned from barerepo

## Remote Repo
we can create a new repo in a remote repo hosting website like gitlab.com
we get a URL such as gitlab.com/auxmsr/dotfiles
we can add this remote repo as 'origin' with:
### git remote add origin <URL>
we can push changes from local repo to remote repo with:
### git push -u origin master (or simply git push)

when we create a new repo (ex. in a different machine) we can pull the changes from remote repo:
### git remote add origin <URL>
### git pull -u origin master

to list the 'origin' url (fetch and push):
### git remote -v

## Merge Conflict
most of the time git merges the code from local and remote repo automatically.
when there are conflicting versions of the same line of code, there is a merge conflict and we need to resolve it.
merge conflict only arises when we make changes to local repo and then pull from remote repo to get the latest codebase.
this is just like doing a p4 sync while local files also have updates.

to resolve, we need to :
### delte meta data lines (yours, their) and keep the correct line (the actual resolution of the conflict)

## Revert code back to the version thats in the remote repo
We have made some confusing updates and need to revert back to the remote repo version (start again)
### git reset --hard origin/master
this is just like p4 revert ...

### git reset --hard <commit_number> (number can be copied from git log)

## Branches
### git branch                (list branches)
### git branch branch_name    (create new branch)
### git checkout branch_name  (switch to branch_name)
### git merge branch_name     (merge branch_name into CURRENT BRANCH)

'master' is the default branch and is always there.
git log shows from which branch the changes were committed.
merge will work automatically provided there are no conflicts
merge conflicts will only occur when both branches (that are being merged) are updated.

## Auth with github
password based auth is no longer supported.
We have to create 'personal access token'
github -> settings -> developer settings -> Personal access tokens -> Generate new token
then copy the generated token.
token is valid for 30 days.

use this token in place of the password.
