---
layout: post
title: "How to do database stuff from within Rails"
date: 2014-10-13 11:52:35 -0700
comments: true
categories:
- rails
- rails console
- database
- postgres
- command line
---
### Rails Console
The rails console is one of the most powerful debug and development tools.  Most particularly, for database manipulation.

Here are some of my most frequently used commands:

Here are some of my much less frequently used, but very powerful and sometimes necessary.  As a rule, I try to only examine what is in my database from the console.  Creating and deleting records from the command line really isn't the way you want to manipulate your database.  That said, sometimes to have to:

#### Create
```
  > u = User.create password: "mypasswd", first_name: "test", last_name: "testovich"
```

#### Update
```
  > u = User.find(30)
  > u.update_attributes(roles_mask: 3)
```
If the above doesn't work, this may:
```
  > User.where(id: 27)[0].update(age: 42, next_birthday: "2014-10-14")
```

#### Destroy
```
  > User.find(30).destroy
```


### Backup & Restore
```
  $ pg_dump -U featherlight featherlight_development -Fc > backup.dump
```

The first command seems to be the one that works
```
  $ pg_restore -c -C -F c -v -U postgres backup.dump
  $ pg_restore -U featherlight -d featherlight_development backup.dump
```


### Creating a database and user
```
  $ createuser portfolio
  Shall the new role be a superuser? (y/n) n
  Shall the new role be allowed to create databases? (y/n) n
  Shall the new role be allowed to create more new roles? (y/n) n
  CREATE ROLE
  $
```

```
  $ createdb portfolio_test -O portfolio
```
* -O owner name is the option in the command line.


### Queries with date ranges
```
  FeedbackRequest.where(created_at: 5.days.ago..4.days.ago)
```
