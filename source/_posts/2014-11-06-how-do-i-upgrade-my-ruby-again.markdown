---
layout: post
title: "How do I upgrade my Ruby again?"
date: 2014-11-06 08:47:02 -0800
comments: true
categories:
- ruby
- rvm
---
If you want to use Rbenv on OS X you'll need to install the Xcode command-line tools:
```
  $ xcode-select --install
```

Then install Home Brew:
```
  $ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

Complete Home Brew setup:
```
  $ brew doctor
  $ brew update
```

At this point you'll be able to install rbenv and ruby-build:
```
  $ brew install rbenv ruby-build
```

Add the following to your .bash_profile:
```
  eval "$(rbenv init -)"
```

Reload your bash profile settings:
```
  $ source ~/.bash_profile
```

Then you can install Ruby:
```
  $ rbenv install 2.1.2
```

Thanks to John O. at TeamTreeHouse for giving this well written response to this inquiry.

To set as your current version of Ruby run the following command:
```
  $ rvm use 2.0.0
```

To make it the default Ruby:
```
  $ rvm default 2.0.0
```
or
```
  $ rvm use 2.0.0 --default
```
