# Git Cheatsheet

## Table of contents
* [Configuration](https://github.com/declon/git-basics#configuration)
* [Starting work](https://github.com/declon/git-basics#starting-work)
* [Branch](https://github.com/declon/git-basics#branch)
* [Status](https://github.com/declon/git-basics#status)
* [Tracking/Staging](https://github.com/declon/git-basics#trackingstaging)
* [Commit](https://github.com/declon/git-basics#commit)
* [Revert Commit](https://github.com/declon/git-basics#revert-commit)
* [Merge](https://github.com/declon/git-basics#merge)
* [Merge Conflicts](https://github.com/declon/git-basics#merge-conflicts)
* [Rebase](https://github.com/declon/git-basics#rebase)
* [Remote Sync](https://github.com/declon/git-basics#remote-sync)
* [Tags](https://github.com/declon/git-basics#tags)
* [Push](https://github.com/declon/git-basics#push)
* [View Difference](https://github.com/declon/git-basics#view-difference)
* [Commit History/Logs](https://github.com/declon/git-basics#commit-historylogs)
* [Git Files](https://github.com/declon/git-basics#git-files)
* [Other Notes](https://github.com/declon/git-basics#other-notes)
___

## Configuration
#### Global:
__NOTE:__ Minimum settings are username and email.
~~~bash
git config --global user.name "Jane Doe"
git config --global user.email "hello@example.com"
git config --global core.editor "/usr/bin/vim" #default editor
~~~

#### Project specific:
__NOTE:__ Must be run within repo.
~~~bash
git config user.email "hello@example.com"
~~~

#### Show config (full):
~~~bash
git config --list
~~~

#### Show config-item value:
~~~bash
git config user.email
~~~

#### Automatic garbage collection:
Cleans out old objects and compresses contents in _.git_ folder.
~~~bash
git config gc.prunexpire "30 days"
~~~

###### Run garabage collection (manual):
~~~bash
git gc --prune
~~~

###### Check if garbage collection required (manual):
~~~bash
git gc --auto
~~~
___

## Starting Work

#### Create a local repo:
~~~bash
git init /path/to/directory
~~~

#### Clone a local repo:
~~~bash
git clone repoName repoCloneName
~~~

#### Clone a remote repo:
~~~bash
git clone https://github.com/username/repoName
~~~

___

## Branch
#### List:
~~~bash
git branch --list
~~~

#### Create:
~~~bash
git branch branchName
~~~

#### Use:
~~~bash
git checkout branchName
~~~

#### Create + Use:
~~~bash
git checkout -b branchName
~~~

#### Delete:
~~~bash
git branch -d branchName
~~~

___


## Status
#### Show modified/new files to be added to tracking:
~~~bash
git status
~~~

#### Shortened:
~~~bash
git status -s
~~~

#### Verbose:
Shows file modifications.
~~~bash
git status -v
~~~

___

## Tracking/Staging
#### Add:
~~~bash
git add README.md
~~~

#### Remove (staging only):
~~~bash
git rm --cached README.md
~~~

#### Remove (staging and file):
~~~bash
git rm README.md
~~~
__NOTE:__ Commit required after a removal.

___

## Commit
#### Simple:
~~~bash
git commit -m "message text"
~~~

#### Commit + Add:
~~~bash
git commit -a -m "message text: auto add modified files"
~~~

___

## Revert Commit

#### Last commit:
~~~bash
git revert HEAD
~~~

#### Specific commit:
~~~bash
git log --oneline # use to calculate the commit index (current commit is 0)
git revert HEAD~2 # where 2 is the commit index
~~~

___

## Merge
~~~bash
git checkout destinationBranch
git merge sourceBranch
~~~

___

## Merge Conflicts
#### Abort:
~~~bash
git merge --abort
~~~

#### Review:
~~~bash
git status # review affected files
# resolve conflicts
git add fileName # add the file to stage after resolving conflict
git commit -m "message text"
~~~

#### Revert post-review:
~~~bash
git reset --hard
~~~

___


## Rebase
~~~bash
git checkout destinationBranch
git rebase sourceBranch
~~~

___

## Remote Sync
#### Remote server alias:
~~~bash
git remote # this is usually the alias 'origin'
~~~

#### Remote server value:
~~~bash
git remote -v
~~~

#### Show updates on remote repo/tracked branches:
~~~bash
git remote show origin
~~~

#### Update the above info:
~~~bash
git fetch origin
~~~

#### Pull and attempt merge for any new files in remote repo:
~~~bash
git pull
~~~

___

## Tags
Used to mark a specific commit in your project. Version numbers are often used as tags to mark a particular state of the product for release.

#### Lightweight:
To be used as a temporary marker.
~~~bash
git tag v0.0 -m "optional message"
~~~

#### Annotated:
Preferred tag.
~~~bash
git tag -a v0.1 -m "Tag annotation/message"
~~~

#### List:
~~~bash
git tag
~~~

#### Show details:
~~~bash
git show v0.1
~~~

#### Delete:
~~~bash
git tag -d tagName
~~~
___

## Push
~~~bash
git push -u origin branchName
~~~

___

## View Difference

#### Show changes since the last commit:
~~~bash
git diff
~~~

#### Show changes between two commits:
~~~bash
git log --oneline # use to identify the the two commit ref IDs
git diff 4a0d421 bd64218 # earlier ref first then later ref
~~~

#### Show changes between two commits (short):
~~~bash
git diff --summary 4a0d421 bd64218
~~~

___

## Commit History/Logs

#### Review info for all commits:
~~~bash
git log
~~~

#### Review only commit ref and message:
~~~bash
git log --oneline --decorate
~~~

#### Textual graph of commit history:
~~~bash
git log --graph
~~~

#### Show file stats for each commit:
~~~bash
git log --stat
git log --shortstat # shorter variant
~~~

#### Show logs from a limited time period:
~~~bash
git log --since="4 days ago"
~~~

#### Search logs for a string:
~~~bash
git log -S string
~~~

#### Custom format log output:
~~~bash
git log --pretty=format:"%h - %an - %ar - %am"
~~~
For further detail/options review man page for _git-log_.

___


## Git Files
__COMMIT_EDITMSG__ - Contains messages for each commit to the repository. (local)

__HEAD__ - Reference to the current branch you are working in.

__config__ - Config info about repo (username, email address).

__description__ - Name of repository (typically used by GitWeb).

__hooks__ - _(dir)_ Contians scripts to automate tasks for phases of the git process.

__index__ - Tracks items in the staging area.

__info__ - _(dir)_ Contains an ignore file.

__logs__ - _(dir)_ Contains logs.

__objects__ - Database of compressed files that are hashed versions of the contents of files that have been commited to the repository.

__refs__ - Reference files for the branches and tags of repo.

__.gitignore__
* Create file in the root of the project
* Add to repository (git add, git commit)
* Anything listed in the file will not be tracked
* File globing can be used
* One entry on each line

#### Show files caught by regex pattern:
~~~bash
git check-ignore pattern
~~~

___

## Other Notes
* Git ignores empty directories (if you want to track/add an empty dir, creat a .keep file in the dir and add the file to the staging area).
* Only commit or merge to the master branch code that is deployment ready.
* Mergetools can be used to resolve conflicts when merging branches
