---
layout: post
title: "Why I like VI"
date: 2013-12-06 13:08:54 -0800
comments: true
categories:
- unix
- vi
- command line
---
## What is VI

VI is a powerful, but brutal, command line text editor available on all unix-based systems.  

I discovered VI while at university studying for my computer engineering degree.  The joke at the time was that VI is 'user VIolent'.  It is hard to deny this perspective, especially as I share it.  After my first couple of stumblings into inadvertent launchings of vi, my unix mentor sat down with me and first taught me how to get the heck out of there, and then taught me how to leverage it to my own benefit.

The biggest benefits to me are:

1. The ease with which I can jump around my document by line/word/page.

2. The ability to copy/paste/delete my chosen number of words or lines.

For any quick little documents I need to write, I am usually happiest in vi.  


## Understanding Command mode vs Insert mode
Vi has two modes of operation.  Command mode and Insert mode.  Command mode takes commands which cause action to be taken on the file you are working on.  Insert mode is where entered text is inserted into the file.

#### Command mode
* In the command mode, every character typed is a command that does something to the text file being edited; a character typed in the command mode may even cause the vi editor to enter the insert mode.

#### Insert mode
* In the insert mode, every character typed is added to the text in the  file; pressing the \<Esc> (Escape) key turns off the Insert mode.


## Using VI Commands

#### * Starting/exiting vi
How to get into vi in the first place.  From your command line:
```
vi your_filename
```

To exit vi and save changes:
```
:wq
```

To exit vi without saving changes:
```
:q!
```

And most importantly, to enter vi command mode:
```
[esc]
```

#### * Cursor movement (to be written)

#### * Screen movement (to be written)

#### * Alter text (to be written)
###### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*   Insert or add text (to be written)
###### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*   Change text (to be written)
###### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*   Delete text (to be written)

#### * Search (to be written)

---
### NOTE
Both UNIX and vi are case-sensitive. Be sure not to use a capital letter in place of a lowercase letter; the results will not be what you expect.

## Fini

Thank you for reading.  I hope you found this useful.  I invite you to read my next post if you are interested in learning how to create a basic rails application with two resources, some minitests, a bit of security lockdown, and some useful views for the app.
