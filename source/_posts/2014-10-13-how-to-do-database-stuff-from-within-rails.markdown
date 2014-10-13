---
layout: post
title: "How to do database stuff from within Rails"
date: 2014-10-13 11:52:35 -0700
comments: true
categories:
---
### Rails Console
The rails console is one of the most powerful debug and development tools.  Most particularly, for database manipulation.

Here are some of my most frequently used commands:

Here are some of my much less frequently used, but very powerful and sometimes necessary.  As a rule, I try to only examine what is in my database from the console.  Creating and deleting records from the command line really isn't the way you want to manipulate your database.  That said, sometimes to have to:

####Create
  > u = User.create password: "mypasswd", first_name: "test", last_name: "testovich"

####Update

  > u = User.find(30)
  > u.update_attributes(roles_mask: 3)

####Destroy

  > User.find(30).destroy
