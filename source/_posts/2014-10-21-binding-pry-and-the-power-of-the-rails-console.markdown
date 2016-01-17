---
layout: post
title: "Binding pry and the power of the rails console"
date: 2014-10-21 13:13:17 -0700
comments: true
categories:
- rails
- rails console
- binding pry
---
The most powerful tool I use on a daily basis is the binding.pry gem.

## Setup
Put the pry-rails gem into your Gemfile for dev and test.

###### Gemfile
```
group :test, :development do
  gem 'pry-rails'
end
```

You will now need to run
```
  $ bundle install
```

at the command line.

## How to use

Put the phrase 'binding.pry' without the quotes into a piece of your code that you want to investigate and binding.pry will open up a rails console at your command line.  This even works in test files.  If you need this in the middle of a haml file, be sure to obey the tabbing convention required by haml, and also put a '-' dash in front of the binding.pry, like so:
###### Ruby file syntax
```
  binding.pry
```

###### Haml file syntax
```
  - binding.pry
```

Remember, you will need to type exit out of the rails console and to return your server to  whatever it was doing before it hit the binding.pry.

This is particularly useful to see the current scope of variables and also to look at what is in the database.
```
Company.find(7).users.find(24)

Company.find(7).team_memberships

Company.find(7).users.find(26)

Company.find(7).users

Company.all

c = Company.find(7)

c.users

User.where(id: 45)

User.where(email: "susan@example.com")

User.where(id: 73).pluck(:first_name, :last_name)
```
