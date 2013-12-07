---
layout: post
title: "My personal Git command reference"
date: 2013-12-02 18:47:42 -0800
comments: true
categories: 
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
 
Here is a useful short way: 
<pre>
  $ git commit -am "Initial commit"
</pre>

### Set up remote repository 
Point to a new repo on github.  Note: Must create this new repo on github first!
<pre>
  $ git remote add origin https://github.com/<username>/demo_app.git
</pre>
 
Which remote repositories are being pointed to:
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

 
Branching, this scares me...
=======
 
First, create the branch locally.  This automatically changes you to this branch locally.
<pre>
  $ git checkout -b new_branch_name
</pre>
  
To check this into github, do this and the new branch will automatically get created on github, 
then your code will get pushed into that branch.
<pre>
  $ git push origin new_branch_name
</pre>
  
Also very useful are these links:
http://www.ndpsoftware.com/git-cheatsheet.html#loc=workspace;
http://git-scm.com/book
 
Use this to confirm WHICH branch you are on.
<pre>
  $ git branch
  $ git add .
  $ git commit -m "a good commit message"
  $ git push origin new_branch_name  
</pre>
  
Very important tips for switching between branches.  ALWAYS commit your changes to your current 
branch before changing branches.  I assumed the files would stay in the old branch as I switched 
to the new branch, but NO.  The changes will follow you around like a lost puppy until you commit 
them.
 
Ok, I've got this branch (or worse, several branches).  I'm done working on them.  They are all checked in, as branches.  But now, I need to get the master branch back up to date.  How do I do this with FIVE branches.  Don't panic, we can do this thing.  First, make sure everything is up to date and checked in.  For me, everything is check in locally and remotely.
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

 
Advanced
=======
 
Show the last 3 commits:
<pre>
  $ git log --oneline
</pre>
  
Want to get the new stuff from master into your branch, but before your commited changes?  Do 
this.  First switch to the branch 'unicorns'
<pre>
  $ git checkout unicorns
  
  $ git rebase master
</pre>
  
In the middle of some work on another branch and have to interrupt and get back to the master 
for some reason?  Do this.  First see what you are working on
<pre>
  $ git diff
</pre>
  
Save working directory and index state WIP on my_branch: b2bdead Add dogs.  And restores last 
commit.
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
 
 
## Fini

Thank you for reading.  I hope you found this useful.  I invite you to read my next post if you are interested in the unix commands that I find most useful.