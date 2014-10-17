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
<pre>
  $ git init
</pre>

Ready to stage your commits?  Here is the long way:
<pre>
  $ git add .
  $ git commit -m "Initial commit"
</pre>

Here is a useful short way to do both of the above commands at once:
<pre>
  $ git commit -am "Initial commit"
</pre>

### Set up remote repository
Point to a new repo on github.  Note: must create this new repo on github first!
<pre>
  $ git remote add origin https://github.com/&ltusername>/&ltyour_new_app_name>.git
</pre>

Show the remote repositories that are being pointed to:
<pre>
  $ git remote -v
</pre>

List remote and local branches:
<pre>
  $ git branch -a
</pre>

Push to github:
<pre>
  $ git push -u origin master
</pre>

### Set up Heroku
First, go to Heroku and create a new repo.
Next, push to heroku:
<pre>
  $ heroku create
  $ git push heroku master
  $ heroku run rake db:migrate
</pre>

Further pushes to heroku
<pre>
  $ git push heroku master
</pre>

If you encounter problems, this will show you the logs on Heroku for diagnostics
<pre>
  $ heroku logs
</pre>

## Frequent staging, commiting, and pushing
Even better is that if you are working offline, you can keep staging and committing.  Then push all to the remote repository at once when you have internet connectivity again.
<pre>
  $ git add .
  $ git commit -m "brief explanation of changes here"
  $ git push
</pre>

### What is the status of your files
How is git looking (you will find some useful guidance printed out with this command too):
<pre>
  $ git status
</pre>


Branching
=======

###New branch exists on remote
####New branches on github
So, your teammate has been working on a new branch they just created and then commited to github.  You now want to start working locally on that new branch.
<pre>
  $ git fetch origin bug-request-id
  $ git checkout bug-request-id
</pre>

####Several new branches on github
You've been heads down on your work on a branch and your team has created several new branches remotely on github and now you need to start contributing to those branches.  To get look at what the remote branches are,
<pre>
  $ git fetch
</pre>

Now you will see everything on the remote when you want to list your local and remote branches with this command:
<pre>
  $ git branch -a
</pre>

Finally, to bring the remote branch code down to your local, once you fetched:
<pre>
  $ git checkout bug-request-id
</pre>


###Create new branch locally
####Starting the new branch locally
First, create the branch locally.  This automatically changes you to this branch locally.
<pre>
  $ git checkout -b new_branch_name
</pre>

####Pushing the new branch to github
To check this into github, do this and the new branch will automatically get created on github,
then your code will get pushed into that branch.
<pre>
  $ git push origin new_branch_name
</pre>

###Good git references
Also very useful are these links:
http://www.ndpsoftware.com/git-cheatsheet.html#loc=workspace;
http://git-scm.com/book
http://techblog.susanprestage.com/blog/2013/12/02/my-personal-git-command-reference/


###Working with a branch
Use this to confirm WHICH branch you are on.
<pre>
  $ git branch
  $ git add .
  $ git commit -m "a good commit message"
  $ git push origin new_branch_name
</pre>

Very important tips for switching between branches.  ALWAYS commit your changes to your current branch before changing branches.  I assumed the files would stay in the old branch as I switched to the new branch, but NO.  The changes will follow you around like a lost puppy until you commit them.

###Merging your branch(es)
Ok, I've got this branch (or worse, several branches).  I'm done working on them.  They are all checked in, as branches.  But now, I need to get the master branch back up to date.  How do I do this with FIVE branches.  Don't panic, we can do this thing.  First, make sure everything is up to date and checked in.
<pre>
  $ git status
</pre>

Then, get onto the master branch.
<pre>
  $ git checkout master
</pre>

Now we are going to merge each branch in, push it to github, and then delete the branch since we are done with them.  Skip the last step if you aren't quite done with the branch.
<pre>
  $ git merge chapter_2
  $ git push origin master    (also can just usually say 'git push' here)
  $ git branch -d chapter_2

  $ git merge chapter_3
  $ git push
  $ git branch -d chapter_3
</pre>
Repeat until you've merged in each branch.  Yeay!  This worked for me and I saw what I wanted on github.  I have both the branches I expect as well as each branch merge present as a commit on the master.  Excellent!  Git is starting to be a Very useful tool instead of an occasional impediment.  :)


Stashing
=======

In the middle of some work on another branch and have to interrupt and get back to the master for some reason?  Do this.  First see what you are working on
<pre>
  $ git diff
</pre>

Save working directory and index state WIP on my_branch and restores last commit.
<pre>
  $ git stash save
</pre>

Now these return nothing
<pre>
  $ git diff
  $ git status
</pre>

Now get back to master and update:
<pre>
  $ git checkout master
  $ git pull
</pre>

When done, get back to our stashed work:
<pre>
  $ git checkout my_branch
  $ git stash apply
</pre>

Verify we are in the same place:
<pre>
  $ git diff

  $ git stash list
  $ git stash apply stash@{1}
  $ git stash drop
</pre>


## Whoops!  Now what do I do?
To check out a particular commit, use
<pre>
  $ git checkout &ltsha1>
</pre>

To revert changes made to your working copy, do this
<pre>
  $ git checkout .
</pre>

This will create three separate revert commits:

<pre>
  $ git revert 0766c053 25eee4ca a867b4af
</pre>

It also takes ranges. This will revert the last two commits:

<pre>
  $ git revert HEAD~2..HEAD
</pre>

To get just one, you could use `rebase -i` to squash them afterwards  Or, you could do it manually (be sure to do this at top level of the repo) get your index and work tree into the desired state, without changing HEAD:

<pre>
  $ git checkout 0d1d7fc32 .
</pre>

and then commit

<pre>
  $ git commit    # be sure and write a good message describing what you just did
</pre>

I don't like my past several commits.  I want to go back to a particular commit.  Reset may be a BAD, BAD way of doing things, so look out!
<pre>
  $ git reset --hard HEAD~5
</pre>


## Powerful commands
Stuff I'm using regularly these days

### Unstage
Reset the staging area to match the most recent commit, but leave the working directory unchanged. This unstages all files without overwriting any changes, giving you the opportunity to re-build the staged snapshot from scratch.
<pre>
  $ git reset
</pre>

Reset the staging area and the working directory to match the most recent commit. In addition to unstaging changes, the --hard flag tells Git to overwrite all changes in the working directory, too. Put another way: this obliterates all uncommitted changes, so make sure you really want to throw away your local developments before using it.
<pre>
  $ git reset --hard
</pre>

### Merge
How to merge the master branch into the feature branch? Easy:
<pre>
  $ git checkout feature1
  $ git merge master
</pre>

Merge branch back into master
<pre>
  $ git checkout master
  $ git merge my_branch
</pre>

###Merge conflict
When there is a conflict during a merge, you have to finish the merge commit manually. It sounds like you've done the first two steps, to edit the files that conflicted and then run
<pre>
  $ git add
</pre>
on them to mark them as resolved.

Finally, you need to actually commit the merge with
<pre>
  $ git commit
</pre>
after which you will be able to switch branches again.

###Have I forgotten to push?
How do I tell if my commited changes have been pushed to github?
<pre>
  $ git log origin/master..HEAD
</pre>
You can also view the diff using the same syntax
<pre>
  $ git diff origin/master..HEAD
</pre>

###Duplicate a branch
Copy old_branch into a new_branch.  (Useful for trying out a merge you are worried about.)
<pre>
  $ git checkout old_branch
  $ git branch new_branch
  $ git checkout new_branch
</pre>

###Destroy local branch
Get rid of a branch and everything in it changed or not.  (Useful after you've tried out a merge on a temporary branch.)

First, you have to get rid of the changes:
<pre>
  $ git reset --hard HEAD
</pre>

Next, change to a different, good branch
<pre>
  $ git checkout master
</pre>

Lastly, delete the branch
<pre>
  $ git branch -d temporary_branch
</pre>
you may need to use a -D option to force this.  BE CAREFUL not to delete something you care about.  Really!

###Tidy up leftovers
Once you delete the branch from the remote, you can prune to get rid of remote tracking branches with:
<pre>
  $ git branch -r -d origin/newfeaturebranch
</pre>

This will prune All of your old references to already-deleted-on-github branches.
<pre>
  $ git remote prune origin
</pre>

## Fini

Thank you for reading.  I hope you found this useful.  I invite you to read my next post if you are interested in the unix commands that I find most useful.
