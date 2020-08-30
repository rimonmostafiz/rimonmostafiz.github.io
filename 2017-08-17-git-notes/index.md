# Git Notes

Git cheat sheet for everyday life. Will update this in future...

~~~
$ git init
# transform the current directory into a Git repository. This adds a .git folder to the current directory and makes it possible to start recording revisions

$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
$ git config --global color.status auto
$ git config --global color.diff auto
$ git config --global color.branch auto

$ git clone <git host>:/repo/<project name>.git
# clone repository to local system

$ git add <file name>
# add file to local repository
# the git add command moves changes from the working directory to staging area, staging area is virtual temporary area where we prepare a snapshot of a set of changes before committing them to the official history

$ git add -A
# stages All

$ git add .
# stages new and modified, without deleted

$ git add -u
# stages modified and deleted, without new

$ git status
# check the Status of the file
# the git status command displays the state of the working directory and the staged snapshot

$ git checkout -- <file>
# reverts back the modified file to the one in the repository

$ git commit -m "commit message"
# the git commit takes the staged snapshot(think as all files) and commits it to the project history.

$ git commit --amend
# update the last commit message

$ git push origin <branch name>
# this command specifies that you are pushing to the a branch
# a branch represents an independent line of development for your repository. Think of it as a brand-new working directory, staging area, and project history. Before you create any new branches, you automatically start out with the main branch (called master).

$ git diff <commit id 1> <commit id 2>
# show changes between two different commit

$ git diff
# with no arguments shows the difference between working directory and staging area *

$ git diff --staged
# show the difference between the staging area and latest commit in repository files which are not same

$ git log
# show log

$ git log --stat
# give some statistics about which file have changed in each commit

$ git log --graph --oneline master coins.
#see the visual representation of the commit history is

$ git config --global color.ui auto

$ git checkout <commit id>
# go to specific version of code using commit id

$ git checkout <branch name>
# select the branch

$ git checkout -b <new branch name>
# combine of 2 command [git branch <new branch name>] & [git checkout <new branch name>]

$ git pull --all
# the git pull command merges the file from your remote repository into your local repository with a single command

$ git tag
# normal tag

$ git tag -a
# anotated tag

$ git reset --hard
# discard any changes in the working directory or staging area (very careful for this command, its cant be reversible)

$ git branch
#show all branches

$ git stash
$ git stash list
$ git stash pop
~~~

