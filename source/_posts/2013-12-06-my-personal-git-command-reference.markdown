---
layout: post
title: "My personal Git command reference"
date: 2013-12-06 18:47:42 -0800
comments: true
categories: 
---
## Set up the repository for your new project
Brand new project.  Start in the project directory.  Then:  
<pre>
  $ git init
</pre>

How is git looking (you will find some useful guidance printed out with this command too):
  $ git status
 
Ready to stage your commits?  Here is the long way:
  $ git add .
  $ git commit -m "Initial commit"
 
Here is a useful short way: 
  $ git commit -am "Initial commit"
 
Point to a new repo on github.  Note: Must create this new repo on github first!
  $ git remote add origin https://github.com/<username>/demo_app.git
 
Which remote repositories are being pointed to:
  $ git remote -v
 
List remote and local branches:
  $ git branch -a
 
Push to github:
  $ git push -u origin master
 
First push to heroku:
  $ heroku create
  $ git push heroku master
  $ heroku run rake db:migrate
 
 
Further pushes to heroku
  $ git push heroku master

##create a new local repo

##create a new github repo

##checking in (locally)

##pushing to github

##pulling, when and why

##branching

##merging

 
 
Advanced
=======
 
Show the last 3 commits:
  $ git log --oneline
  
Want to get the new stuff from master into your branch, but before your commited changes?  Do 
this.  First switch to the branch 'unicorns'
  $ git checkout unicorns
  
  $ git rebase master
  
In the middle of some work on another branch and have to interrupt and get back to the master 
for some reason?  Do this.  First see what you are working on
  $ git diff
  
Save working directory and index state WIP on my_branch: b2bdead Add dogs.  And restores last 
commit.
  $ git stash save
  
Now these return nothing
  $ git diff
  $ git status
  
Now get back to master and update:
  $ git checkout master
  $ git pull
  
When done, get back to our stashed work:
  $ git checkout my_branch
  $ git stash apply
 
Verify we are in the same place:
  $ git diff
  
  $ git stash list
  $ git stash apply stash@{1}
  $ git stash drop
 
 
Branching, this scares me...
=======
 
First, create the branch locally.  This automatically changes you to this branch locally.
  $ git checkout -b new_branch_name
  
To check this into github, do this and the new branch will automatically get created on github, 
then your code will get pushed into that branch.
  $ git push origin new_branch_name
  
Also very useful are these links:
http://www.ndpsoftware.com/git-cheatsheet.html#loc=workspace;
http://git-scm.com/book
 
Use this to confirm WHICH branch you are on.
  $ git branch
  $ git add .
  $ git commit -m "a good commit message"
  $ git push origin new_branch_name  
  
Very important tips for switching between branches.  ALWAYS commit your changes to your current 
branch before changing branches.  I assumed the files would stay in the old branch as I switched 
to the new branch, but NO.  The changes will follow you around like a lost puppy until you commit 
them.
 
Ok, I've got this branch (or worse, several branches).  I'm done working on them.  They are all checked in, as branches.  But now, I need to get the master branch back up to date.  How do I do this with FIVE branches.  Don't panic, we can do this thing.  First, make sure everything is up to date and checked in.  For me, everything is check in locally and remotely.
  $ git status
  
Then, get onto the master branch.
  $ git checkout master
  
Now we are going to merge each branch in, push it to github, and then delete the branch since we are done with them.  Skip the last step if you aren't quite done with the branch.
  $ git merge chapter_2
  $ git push origin master    (also can just usually say 'git push' here)
  $ git branch -d chapter_2
  
  $ git merge chapter_3
  $ git push 
  $ git branch -d chapter_3
Repeat until you've merged in each branch.  Yeay!  This worked for me and I saw what I wanted on github.  I have both the branches I expect as well as each branch merge present as a commit on the master.  Excellent!  Git is starting to be a Very useful tool instead of an occasional impediment.  :)
 
  