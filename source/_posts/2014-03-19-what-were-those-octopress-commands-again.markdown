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
<pre>
	$ rake new_post["What were those Octopress commands again?"]
</pre>

Incorporate that post into your site:
<pre>
	$ rake generate
</pre>

If POW is setup, you can just run:
<pre>
	$ rake watch
</pre>

Load the following in your browser to see how things look.
<pre>
http://octopress.dev
</pre>

Happy with how everything looks?  Commit your code and push to the livesite.  

If you are working on two different blogs, you will need to switch back and forth in POW the directory that is being looked at:
<pre>
	$ cd ~/.pow
	$ ln -s /path/to/octopress octopress
</pre>

On that rare occasion that you change your _config.yml, you will need to run a special command, since rake generate doesn't do what is needed.
<pre>
	$ rake update_source
</pre>

Thanks
=======
Thank you to the Octopress docs site for well written and easy to follow documentation.  This is my most frequently refered to page, now that my site is up and running, [http://octopress.org/docs/blogging/](http://octopress.org/docs/blogging/)
