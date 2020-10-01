 

# The Basics

## Install Git

### Windows Instructions
[Git on Windows](http://git-scm.com/download/win)

### Linux Instructions
[Git on Linux](http://git-scm.com/download/linux)

### Mac Instructions
[Git on Mac](http://git-scm.com/download/mac)

If you have homebrew installed

```bash
$ brew install git
```
### Configure Git
```bash
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
###  Create Repository From Existing Code
```bash
$ cd existing-code-directory
$ git init
$ git add *
$ git commit -m "Initial checkin"
```
### Adding a Remote Server
```bash
$ git remote add https://github.com/cruft/my-repo.git
```

### Cloning Existing Repository
```bash
$ git clone ssh://git@github.com/your-name-here/your-repo.git
$ git add FileThatChanged.java
$ git commit -m "I implemented blah for flurp"
$ git push origin HEAD
```
## Working With Git
### Pulling in Code from Master
```bash
$ git pull origin master
```
### Creating Branches
```bash
$ git checkout -b branch_name
```
### Switching Branches
```bash
$ git checkout master
```
### Checking out Remote Branch
```bash
$ git fetch
$ git checkout remote_branch
```
### Merging Branches
```bash
$ git merge branch_name
```
### Deleting Local Branch
```
$ git branch -d <branch-name>
$ git branch -D <brach-name> # - force delete
```
### Deleting Remote Branch
```
$ git push origin :<branch-name>
$ git push origin --delete <branch-name>
```
### Creating a tag
```
$ git tag V1.0
$ git tag -a v1.1 -m "Creating version 1.1" # Creates a tag with a message
$ git tag -a v1.2 9fceb02 -m "Creating tag for 1.2 from commit hash"
```
### Showing tags
```
$ git tag
$ git tag -l "v1.8.5*" # show tags of a particular pattern
```
### Saving Tags
```
$ git push origin v1.1 # Save tag to remote
$ git push origin --tags # Save all local tags to remote
```
### Deleting Tags
```
$ git tag -d v1.1 # Delete local tag
$ git push origin --delete v1.1 # Delete remote tag
```
### Checking out Tags
```
$ git checkout v1.1 # Check out tag in in “detached HEAD” state
$ git checkout -b version2 v2.0.0 # Checkout tag to branch
```
### Pruning local tracking branches
```
$ git fetch -p <remote-branch> # single branch
$ git fetch -p # Mutiple remote tracking deletes
```
### Getting My Codes Status
```bash
$ git status
```
### Staging Changes
```bash
$ git add path/to/my/file/SomeFile.java
```
### Unstaging a Staged File
```bash
$ git reset HEAD path/to/my/file/SomeFile.java
```
### Unmodifying a Modified File
```bash
$ git checkout -- path/to/my/file/SomeFile.java
```
### Committing Code
```bash
$ git commit -m "I added code"
```
### Staging and Committing Code
```bash
$ git commit -a -m "Commit Message"
```
### Changing Last Commit
This can be used to change a message, add, and/or remove files

```bash
$ git commit --amend -m "Change the commit message"
$ git add NewFile.java
$ git commit --amend
```
### Putting Committed Code on Remote Server
```bash
$ git push origin HEAD
```
### Pulling Code from Remote Server
```bash
$ git pull --rebase
```
### Viewing Difference in Your Code and Repository
```bash
$ git diff
```
### Moving or Renaming a File
```bash
$ git mv /path/to/my/file/SomeFile.java /new/path/SomeFile.java
```
### View Git History
```bash
$ git log
$ git reflog
```
### Removing a file from Git
```bash
$ git rm path/to/my/file/SomeFile.java
```
### Removing a file from Git, but keeping it on Disk
```bash
$ git rm --cached local.file
```
### Revert Commit
Find the commit you want to revert

```bash
$ git log
You should see an output of the repository history
commit 54533995148bc91424b7ca2493230a09f6cb9acb
Author: Homer Simpson <Homer.Simpson@example.com>
Date:   Mon Oct 10 14:19:04 2016 -0400


    Added auto cool of tap.


commit 7de86787eabc55799085a7ab7e22cf04c83d31ab
Author: Krusty.Clown <krusty.clown@example.com>
Date:   Mon Oct 10 14:54:12 2016 -0400


    PUB-1222 - Krusty C, Sideshow B - Added the humor tap squirt feature.
```    
Select the commit hash to revert

```bash
$ git revert 54533995148bc91424b7ca2493230a09f6cb9acb
```
Add your revert message

### Creating Aliases
```bash
$ vi ~/.gitconfig
```
Add entries like below

```bash
[alias]
st = status
pr = pull --rebase
pm = pull origin master
co = checkout
```

## Common Problem
I assume you have git command line installed by now.
### Changing the last commit message
This should only be done prior to pushing to a remote branch. Caveat Emptor
```bash
$ git commit --amend -m "STORY-1234 - Updated commit message"
```
### Showing files staged for commit
```bash
$ git show --name-only
```
### Undoing a Commit
If you have a commit that you want to undo, there is a simple workaround

```bash
$ git reflog
    4c20138 HEAD@{0}: checkout: moving from feature/STORY-1234 to master
    4c20138 HEAD@{1}: checkout: moving from master to feature/STORY-1234
    4c20138 HEAD@{2}: pull origin master: Merge made by the 'recursive' strategy.
    3c3dace HEAD@{3}: commit: STORY-1234 - Bad unit of work
$ git reset --soft HEAD~3
```
### Staging Change Shards
```bash
$ git add -p
```
The output will look something like below:

```bash
diff --git a/README.md b/README.md
    index f00c19d..ef40e35 100644
    --- a/README.md
    +++ b/README.md
    @@ -1,7 +1,7 @@
    # Q Platform Vagrant Setup
  
    ## Prerequisites
    -
    +      
    Stage this hunk [y,n,q,a,d,/,j,J,g,e,?]?
```
### Fixing Merge Conflicts
```bash
$ git mergetool
```
### Showing the History of a File
```bash
$ git log --follow -p -- path/to/file/SomeFile.java
```
### Git Rebase has conflicts
You should resolve the conflicts using your merge tool.  After that continue the rebase

```bash
$ git rebase --continue
```
### Overwrite Local Files on Pull
This will cause local changes to be lost, Caveat Emptor

```bash
$ git fetch --all
$ git reset --hard origin/master
```
### Move untracked changes to a Branch
To see the unstaged file, check the status

```bash
$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Untracked files:
    (use "git add <file>..." to include in what will be committed)


    new_file


    nothing added to commit but untracked files present (use "git add" to track)
```
This shows that new_file is not tracked

```bash
$ git checkout -b new_branch
$ git add new_file
$ git commit -m "Added files to new branch"
```
### Git Ignore
```bash
$ git add .gitignore
$ git commit -m "Added git ignore file"
$ git push origin HEAD
```
Check out the Documentation for information how to set up the file
### Git Clone Tag or Branch
```bash
$ git clone https://my-git-repo.com/my-app.git -b my-tag-1.0
$ git clone https://my-git-repo.com/my-app.git -b my-branch
$ git clone https://my-git-repo.com/my-app.git --branch my-tag-1.0
$ git clone https://my-git-repo.com/my-app.git --branch my-branch
```
### Remove local untracked files
```bash
$ git clean -fd
```
### Undo last local commit
```bash
$ git reset --soft HEAD~
```
## Tips and Tricks
Here are some useful tips and tricks for making working with Git easier.
### Reuse the Previous Commit Message
```bash
$ git commit --reedit-message=HEAD --reset-author
```
### Show the Remote Origin Server
```bash
$ git remote show origin
```
### Amend commit with out updating message
```bash
$ git commit --amend --no-edit
```
### Stash Changes
```bash
$ git stash 
```
This will take all changed files in local repository and stash them locally in a stash stack
### List Stash Changes
```bash
$ git stash list 
```
This will list all of the stashed changes in your stash stack
### Show Stashed Changes
```bash
$ git stash show -p stash@{1}
```
This will show all of the changes on that particular stash stack location
### Un-Stash Changes
```bash
$ git stash pop
```
This will take stashed files and apply them to your working HEAD.  This also removes them from the stash stack.
### Apply Stashed Changes
```bash
$ git stash apply 
```
This will take all changed files stashed and apply them to your local HEAD.  This leaves the stashed changes on the stash stack
### Drop Stashed Changes
```bash
$ git stash drop
```
This will take remove the changes at the top of your stash stack.
### Clear Stashed Changes
```bash
$ git stash clear
```
This clear your stash stack.

### Rename a Branch
```bash
$ git branch -m "new_branch_name" # If you are on the branch locally
$ git branch -m old-name new-name # If you are not on the branch to rename
$ git push origin :old_branch # Delete the old branch
$ git push origin HEAD # Push the renamed branch to origin
```

## DANGER WILL ROBINSON!!
This is when things go awry and you need some help.
### Revert a bunch of commits
Say you pushed code to the `(master)` branch instead of `(develop)` and you need to revert everything back to the last merge down to master.

```bash
$ git log
```
This will show you the commit history, like so:

```bash
commit 6290518ffd80d8dbb393ac144804f1069040f2e7
Merge: f428d60 e39a178
Author: Mickey Mouse  <mickey.mouse@example.com>
Date:   Tue May 2 16:02:16 2017 +0000

    Merge pull request #183 in PRP/de-prp from bugfix/PRP-515-Integration_bug to release/v1.2.0

    * commit 'e39a178c32ff35e41c13437951fbc3a8cfecc9be':
      Fixed integration broken because of prp-515

commit e39a178c32ff35e41c13437951fbc3a8cfecc9be
Author: Donald.Duck <donald.duck@example.com>
Date:   Tue May 2 11:45:52 2017 -0400

    Fixed Broken Tests
commit dc71d964818c382b090bc90cb214d0d0b356c743
Merge: c6f68a8 6290518
Author: Mickey Mouse <mickey.mouse@example.com>
Date:   Tue May 2 13:15:07 2017 -0400

    Merge remote-tracking branch 'origin/release/v1.2.0' into master
```
Find the last good commit hash

```bash
$ git reset dc71d964818c382b090bc90cb214d0d0b356c743 --soft
```
You can do a --hard and it will remove all of the changes that are between where you are and that commit.  A --soft will keep those changes as staged in your local.

```bash
$ git push --force HEAD
```
**THIS IS A BIG NO NO,** *usually*.  Only do this if you are sure that no one is working off of the remote branch.
 
