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
<pre>
  > u = User.create password: "mypasswd", first_name: "test", last_name: "testovich"
</pre>

####Update
<pre>
  > u = User.find(30)
  > u.update_attributes(roles_mask: 3)
</pre>
If the above doesn't work, this may:
<pre>
  > User.where(id: 27)[0].update(age: 42, next_birthday: "2014-10-14")
</pre>

####Destroy
<pre>
  > User.find(30).destroy
</pre>


###Backup & Restore
<pre>
  $ pg_dump -U featherlight featherlight_development -Fc > backup.dump
</pre>

The first command seems to be the one that works
<pre>
  $ pg_restore -c -C -F c -v -U postgres backup.dump
  $ pg_restore -U featherlight -d featherlight_development backup.dump
</pre>


###Creating a database and user
<pre>
  $ createuser portfolio
  Shall the new role be a superuser? (y/n) n
  Shall the new role be allowed to create databases? (y/n) n
  Shall the new role be allowed to create more new roles? (y/n) n
  CREATE ROLE
  $
</pre>

<pre>
  $ createdb portfolio_test -O portfolio
</pre>
* -O owner name is the option in the command line.

