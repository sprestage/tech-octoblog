---
layout: post
title: "My personal Git command reference"
date: 2013-12-02 18:47:42 -0800
comments: true
categories:
- git
- github
- heroku
- command line
- prune
- branch
- stash
---

Git Basics
=======

## Setting up a new project
### Set up the local repository
Brand new project.  Start in the project directory.  Then:
```
  $ git init
```

Ready to stage your commits?  Here is the long way:
```
  $ git add .
  $ git commit -m "Initial commit"
```

Here is a useful short way to do both of the above commands at once:
```
  $ git commit -am "Initial commit"
```

### Set up remote repository
Point to a new repo on github.  Note: must create this new repo on github first!
```
  $ git remote add origin https://github.com/&ltusername>/&ltyour_new_app_name>.git
```

Show the remote repositories that are being pointed to:
```
  $ git remote -v
```

List remote and local branches:
```
  $ git branch -a
```

Push to github:
```
  $ git push -u origin master
```

### Set up Heroku
First, go to Heroku and create a new repo.
Next, push to heroku:
```
  $ heroku create
  $ git push heroku master
  $ heroku run rake db:migrate
```

Further pushes to heroku
```
  $ git push heroku master
```

If you encounter problems, this will show you the logs on Heroku for diagnostics
```
  $ heroku logs
```

## Frequent staging, commiting, and pushing
Even better is that if you are working offline, you can keep staging and committing.  Then push all to the remote repository at once when you have internet connectivity again.
```
  $ git add .
  $ git commit -m "brief explanation of changes here"
  $ git push
```

### What is the status of your files
How is git looking (you will find some useful guidance printed out with this command too):
```
  $ git status
```


Branching
=======

### New branch exists on remote
#### New branches on github
So, your teammate has been working on a new branch they just created and then committed to github.  You now want to start working locally on that new branch.
```
  $ git fetch origin bug-request-id
  $ git checkout bug-request-id
```

#### Several new branches on github
You've been heads down on your work on a branch and your team has created several new branches remotely on github and now you need to start contributing to those branches.  To get look at what the remote branches are,
```
  $ git fetch
```

Now you will see everything on the remote when you want to list your local and remote branches with this command:
```
  $ git branch -a
```

Finally, to bring the remote branch code down to your local, once you fetched:
```
  $ git checkout bug-request-id
```


### Create new branch locally
#### Starting the new branch locally
First, create the branch locally.  This automatically changes you to this branch locally.
```
  $ git checkout -b new_branch_name
```

Note, you can do this even if you already have changes made.  They'll simply still be there, unstaged and uncommitted in the new branch.

#### Pushing the new branch to github
To check this into github, do this and the new branch will automatically get created on github,
then your code will get pushed into that branch.
```
  $ git push origin new_branch_name
```

### Good git references
Also very useful are these links:
http://www.ndpsoftware.com/git-cheatsheet.html#loc=workspace;
http://git-scm.com/book
http://techblog.susanprestage.com/blog/2013/12/02/my-personal-git-command-reference/


### Working with a branch
Use this to confirm WHICH branch you are on.
```
  $ git branch
  $ git add .
  $ git commit -m "a good commit message"
  $ git push origin new_branch_name
```

Very important tips for switching between branches.  ALWAYS commit your changes to your current branch before changing branches.  I assumed the files would stay in the old branch as I switched to the new branch, but NO.  The changes will follow you around like a lost puppy until you commit them.

### Merging your branch(es)
Ok, I've got this branch (or worse, several branches).  I'm done working on them.  They are all checked in, as branches.  But now, I need to get the master branch back up to date.  How do I do this with FIVE branches.  Don't panic, we can do this thing.  First, make sure everything is up to date and checked in.
```
  $ git status
```

Then, get onto the master branch.
```
  $ git checkout master
```

Now we are going to merge each branch in, push it to github, and then delete the branch since we are done with them.  Skip the last step if you aren't quite done with the branch.
```
  $ git merge chapter_2
  $ git push origin master    (also can just usually say 'git push' here)
  $ git branch -d chapter_2

  $ git merge chapter_3
  $ git push
  $ git branch -d chapter_3
```

Repeat until you've merged in each branch.  Yeay!  This worked for me and I saw what I wanted on github.  I have both the branches I expect as well as each branch merge present as a commit on the master.  Excellent!  Git is starting to be a Very useful tool instead of an occasional impediment.  :)


Stashing
=======

In the middle of some work on another branch and have to interrupt and get back to the master for some reason?  Do this.  First see what you are working on
```
  $ git diff
```

Save working directory and index state WIP on my_branch and restores last commit.
```
  $ git stash save
```

Now these return nothing
```
  $ git diff
  $ git status
```

Now get back to master and update:
```
  $ git checkout master
  $ git pull
```

When done, get back to our stashed work:
```
  $ git checkout my_branch
  $ git stash apply
```

Verify we are in the same place:
```
  $ git diff

  $ git stash list
  $ git stash apply stash@{1}
  $ git stash drop
```


## Whoops!  Now what do I do?  Gentle commands
### How to undo my last commit, not yet pushed
I staged my files `git add .` and then committed them `git commit -m "changes I don't want to make yet"`, but the I realize that I want to undo all that for some reason, like I'm on the wrong branch.

Simple.  Two steps.  First, undo the commit.
```
git reset --soft HEAD~
```

Next, unstage the files.
```
git reset HEAD app/helpers/timezone_helper.rb
```

Do a `git status` before and after each command to better see what is happening.

### Check out a particular commit by SHA
To check out a particular commit, use
```
  $ git checkout &ltsha1>
```

### Revert changes to local working copy
To revert changes made to your working copy, restoring your local copy to the most recently checked in remote copy, do this
```
  $ git checkout .
```


## Powerful commands, use with caution

### Unstage
Reset the staging area to match the most recent commit, but leave the working directory unchanged. This unstages all files without overwriting any changes, giving you the opportunity to re-build the staged snapshot from scratch.
```
  $ git reset
```

Reset the staging area and the working directory to match the most recent commit. In addition to unstaging changes, the --hard flag tells Git to overwrite all changes in the working directory, too. Put another way: this obliterates all uncommitted changes, so make sure you really want to throw away your local developments before using it.
```
  $ git reset --hard
```

Careful: <code>git reset --hard</code> WILL DELETE YOUR WORKING DIRECTORY CHANGES. Be sure to stash any local changes you want to keep before running this command.

Assuming you are sitting on that commit, then this command will wack it...

```
  $ git reset --hard HEAD~1
```

The HEAD~1 means the commit before head.

Or, you could look at the output of git log, find the commit id of the commit you want to back up to, and then do this:

```
  $ git reset --hard <sha1-commit-id>
```

If you REALLY want to rewrite history.  Think very, very carefully about this BEFORE doing it.

```
  $ git reset --hard <old-commit-id>
  $ git push -f
```

### Switch to specific commit
Temporarily switch to a different commit

If you want to temporarily go back to it, fool around, then come back to where you are, all you have to do is check out the desired commit:

```
  # This will detach your HEAD, that is, leave you with no branch checked out:

  $ git checkout 0d1d7fc32
```

Or if you want to make commits while you're there, go ahead and make a new branch while you're at it:

```
  git checkout -b old-state 0d1d7fc32
```

### Merge
How to merge the master branch into the feature branch? Easy:
```
  $ git checkout feature1
  $ git merge master
```

Merge branch back into master
```
  $ git checkout master
  $ git merge my_branch
```

### Merge conflict
When there is a conflict during a merge, you have to finish the merge commit manually. It sounds like you've done the first two steps, to edit the files that conflicted and then run
```
  $ git add
```

on them to mark them as resolved.

Finally, you need to actually commit the merge with
```
  $ git commit
```

after which you will be able to switch branches again.

### Have I forgotten to push?
How do I tell if my committed changes have been pushed to github?
```
  $ git log origin/master..HEAD
```

You can also view the diff using the same syntax
```
  $ git diff origin/master..HEAD
```

### Duplicate a branch
Copy old_branch into a new_branch.  (Useful for trying out a merge you are worried about.)
```
  $ git checkout old_branch
  $ git branch new_branch
  $ git checkout new_branch
```

### Destroy local branch
Get rid of a branch and everything in it changed or not.  (Useful after you've tried out a merge on a temporary branch.)

First, you have to get rid of the changes:
```
  $ git reset --hard HEAD
```

Next, change to a different, good branch
```
  $ git checkout master
```

Lastly, delete the branch
```
  $ git branch -d temporary_branch
```

you may need to use a -D option to force this.  BE CAREFUL not to delete something you care about.  Really!

### Tidy up leftovers
Once you delete the branch from the remote, you can prune to get rid of remote tracking branches with:
```
  $ git branch -r -d origin/newfeaturebranch
```

This will prune All of your old references to already-deleted-on-github branches.
```
  $ git remote prune origin
```

### Restore local master
You've messed things up on your local master and need to get back.

Setting your branch to exactly match the remote branch can be done in two steps:
```
  $ git fetch origin
  $ git reset --hard origin/master
```


## Fini
Thank you for reading.  I hope you found this useful.  I invite you to read my next post if you are interested in the unix commands that I find most useful.
