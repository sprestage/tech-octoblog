---
layout: post
title: "My favorite unix commands"
date: 2013-12-03 16:03:22 -0800
comments: true
categories:
- unix
- command line
---

Where is the command I'm trying to use stored.  This is good for when you are not sure which version of something is being used.  Or which of two different installations of something is being used.
```
type (for when where doesn't tell me what I want)
```

This gives a nice recursive directory listing in a tree format.
```
tree
```

Erase this whole line that I am at the end of.
```
[ctrl] + u
```

Jump to the beginning of this line I'm on.
```
[ctrl] + a
```

Jump to the end of this line I'm on.
```
[ctrl] + e
```

Stop this program I'm in.
```
[ctrl] + c
```

No really, stop the danged program.
```
[ctrl] + d
```

Give me various different verbosity levels of a process listing.
```
ps
ps -ef
ps -x
ps -a
```

How to kill a process.  This command can be different for different unix systems.
```
kill <process_id>
kill <process_id>
```

Path shortcut representations.

For my own (current user) directory, usually something like /Users/susanprestage.
```
~
```
Where `cd ~` will change in the the current user's root directory.

The current directory is represented by `.`.  For example, `./my_script` would run the copy of my_script that is stored in the current directory.

The parent directory to the current directory is represented by `..`.  For example, if I were currently in /Users/susanprestage/workspace but wanted to change into /Users/susanprestage/bin, I could use `cd ../bin` to get there.

Print the full path of the current aka working directory.
```
pwd
```

## Fini

Thank you for reading.  I hope you found this useful.  I invite you to read my next post if you are interested in learning how to use the unix .alias file to make your command line experience more pleasurable.
