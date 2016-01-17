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
<pre>
  $ xcode-select --install
</pre>

Then install Home Brew:
<pre>
  $ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
</pre>

Complete Home Brew setup:
<pre>
  $ brew doctor
  $ brew update
</pre>

At this point you'll be able to install rbenv and ruby-build:
<pre>
  $ brew install rbenv ruby-build
</pre>

Add the following to your .bash_profile:
<pre>
  eval "$(rbenv init -)"
</pre>

Reload your bash profile settings:
<pre>
  $ source ~/.bash_profile
</pre>

Then you can install Ruby:
<pre>
  $ rbenv install 2.1.2
</pre>

Thanks to John O. at TeamTreeHouse for giving this well written response to this inquiry.

To set as your current version of Ruby run the following command:
<pre>
  $ rvm use 2.0.0
</pre>

To make it the default Ruby:
<pre>
  $ rvm default 2.0.0
</pre>
or
<pre>
  $ rvm use 2.0.0 --default
</pre>
