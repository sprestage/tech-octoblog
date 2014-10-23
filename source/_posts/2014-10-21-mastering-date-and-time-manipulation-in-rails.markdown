---
layout: post
title: "Mastering date and time manipulation in rails."
date: 2014-10-21 13:14:02 -0700
comments: true
categories:
---
There are several different ways of manipulating time in rails.  Instead of searching for them everytime I need them, I will keep there here in one easy location.

Rails gives built-in ways to add days (which will suit for weeks as well) and also to add months.  This means that using rails to add a month (which will suit for years as well) has built into it accomodations for February, leap years, leap centuries, etc.  Use Rails for this magic.  Do Not roll your own dating.

##Future and Past
###By month
<pre>
  > DateTime.now
=> Tue, 21 Oct 2014 13:08:17 -0700

  > DateTime.now >> 1
=> Fri, 21 Nov 2014 13:08:44 -0700

  > DateTime.now >> -2
=> Thu, 21 Aug 2014 13:09:23 -0700
</pre>

###By week
<pre>
  > DateTime.now
=> Tue, 21 Oct 2014 15:00:17 -0700

  > DateTime.now + (2 * 7)
=> Tue, 04 Nov 2014 15:00:52 -0700

  > DateTime.now - (1 * 7)
=> Tue, 14 Oct 2014 15:04:16 -0700
</pre>


##Past
<pre>
  > 1.week.ago
=> Tue, 14 Oct 2014 20:20:14 UTC +00:00

  > 2.weeks.ago
=> Tue, 07 Oct 2014 20:20:27 UTC +00:00

  > 1.month.ago
=> Sun, 21 Sep 2014 20:20:34 UTC +00:00

  > 2.months.ago
=> Thu, 21 Aug 2014 20:20:41 UTC +00:00
</pre>

##Date only
<pre>
  > Date.today
=> Wed, 22 Oct 2014

  > Date.today+2
=> Fri, 24 Oct 2014
</pre>
