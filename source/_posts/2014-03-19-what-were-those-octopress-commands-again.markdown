---
layout: post
title: "What were those Octopress commands again?"
date: 2014-03-19 12:30:59 -0700
comments: true
categories:
- Octopress
- rake commands
- command line
- blogging
---
Create a new post:
```
	$ rake new_post["What were those Octopress commands again?"]
```

Incorporate that post into your site:
```
	$ rake generate
```

If POW is setup, you can just run:
```
	$ rake watch
```

Load the following in your browser to see how things look.
```
http://octopress.dev
```
Or possibly
```
http://<name_of_blog>.dev
```

Happy with how everything looks?  Commit your code and push to the livesite.

If you are working on two different blogs, you will need to switch back and forth in POW the directory that is being looked at:
```
$ cd ~/.pow
$ ln -s /path/to/octopress octopress
```

On that rare occasion that you change your `_config.yml`, you will need to run a special command, since rake generate doesn't do what is needed.  Look out though, if you've customized your blog such as with Octostrap3, this will undo your changes, so use with caution.
```
$ rake update_source
```

## How to restart the POW server
```
$ touch ~/.pow/restart.txt
```

Thanks
=======
Thank you to the Octopress docs site for well written and easy to follow documentation.  This is my most frequently referred to page, now that my site is up and running, [http://octopress.org/docs/blogging/](http://octopress.org/docs/blogging/)
