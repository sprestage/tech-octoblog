---
layout: post
title: "Overcoming my fear of Git through knowledge"
date: 2013-12-01 18:59:42 -0800
comments: true
categories: 
---
## Getting past my fear of Git
Git kept scaring me.  Mostly, this fear is based on how wonderfully powerful a tool that Git (and github) can be and my lack of easy comfort with the commands.  So, I've made a list of my most used commands and any notes I need for use.  This goes a bit long, since as I learned more and more commands, I added more that I was starting to use.  Good luck!

## What is Git
#### Basics
Git is a version control system, VCS.  Don't think too carefully about the other VCSs you know, like Perforce or Subversion.  Git is much different and trying to compare will likely cause confusion.

#### Snapshots, instead of differences
Most other systems tend to store data as changes to a base version of each file.  Git doesn't think of it's data that way.  Instead, Git thinks of its data more like a set of snapshots of a mini-filesystem.  And, to be efficient, Git only takes a snapshot of the files that have changed, simply linking to all the other files that have not changed.

#### Local
Most operations you perform with Git will be local. The entire history of your repository will be right there on your machine, which means that diffs and browsing the history of your project is very quick.  This also means that working offline is not a problem.  You simply commit all you like while offline, then push your work up to the remote repository server when you get back to a network connection. 

#### The Three States of Git
###### 1. The Working Directory
###### 2. The Staging Area
###### 3. The Git Repository
<a target="_blank" href="#blog"><img class="img-portfolio img-responsive" src="https://s3-us-west-2.amazonaws.com/technicalblog/three_states_of_git.png" width="340" height="284"></a>

Git has three main states that your files can reside in: commited, modified, and staged.  Commited means that the data is safely stored in your local repository.  Modified means that you have changed the file, but not yet commited it to your local repository.  Staged means that you have marked a modified file to go into your next commit snapshot.

* Check out the project to bring the files from the git repository into your working directory.

* Stage your files to bring those changes from your working directory to the staging area. 

* Commit your files to bring the changes from the staging area to the git repository.

Your workflow will be something like this:

1. Modify files in your working directory.
2. Stage the files.  This adds snapshots of them to the staging area.
3. Commit your changes.  This takes the files as they are in the staging area and stores that snapshot in your git repository.

## Getting started with Git
To install and setup Git, go here and follow the very good instructions.  

* http://git-scm.com/book/en/Getting-Started-Installing-Git 
* http://git-scm.com/book/en/Getting-Started-First-Time-Git-Setup

I highly recommend the entire http://git-scm.com/documentation site.  For a more thorough explanation of Git, what it is and how it works, I particularly recommend this chapter http://git-scm.com/book/en/Getting-Started-Git-Basics.  

## Final notes on Git
I have found that it is important to stage and commit your files often and in small increments.  Any time you have a change that makes sense as its own commit, do so.  If what you are working on is so big that you think you ought to wait to commit, then I strongly recommend branching and then again you should be able to break down your commits within that branch.  You really want to be able to track what you did later, both for yourself and for others trying to maintain your code.
 
## Fini

Thank you for reading.  I hope you found this useful.  I invite you to read my next post if you are interested in the Git commands that I find most useful.