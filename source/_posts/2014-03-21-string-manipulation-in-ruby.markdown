---
layout: post
title: "String manipulation in Ruby"
date: 2014-03-21 12:12:17 -0700
comments: true
categories: 
- Ruby
- strings
---
Set vs concantenate
=======
Set equal to this string.  No initialization needed.
<pre>
> farewell = "Good"  
</pre>

<pre>
> puts farewell
</pre>

will return
<pre>
  => Good
</pre>

Concantenation requires the variable to be initialized.  This only works because the variable was initialized above.
<pre>
> farewell << "bye!"  
</pre>

<pre>
> puts farewell
</pre> 

will return
<pre>
  => Goodbye!
</pre>

String operations
=======
Find where a substring is within the source string using index.
<pre>
"hello".index('e')             #=> 1
"hello".index('lo')            #=> 3
"hello".index('a')             #=> nil
"hello".index(?e)              #=> 1
"hello".index(/[aeiou]/, -3)   #=> 4
</pre>

Take input from the user:
<pre>
puts "Please input some text: "
foo = gets.chomp
puts foo
</pre>

If you are using ARGV to bring in command line arguments when you launch your app, you will run into conflict when using gets.  You can work around this two ways.  First is to use perform whatever tasks you need to on ARGV, then:
<pre>
ARGV.clear
foo = gets.chomp
</pre>

Otherwise, everytime you call gets, you will need to specify that it is from IO, not Kernal:
<pre>
foo = $stdin.gets.chomp
</pre>

Replace the first instance of the sub_string, "replace_me", with the contents of foo.
<pre>
bar = bar.sub("replace_me", foo)
</pre>

Globally replace the sub_string, "replace_me", with the contents of foo.
<pre>
bar = bar.<b>g</b>sub("replace_me", foo)
</pre>

Find the first example of substring, "find_me".  This is most often used with regex in place of the "find_me" string.  Returns a string.
<pre>
bing = bar.match("find_me")
</pre>

Find the every example of substring, "find_me".  This is most often used with regex in place of the "find_me" string.  Returns an array of strings.
<pre>
bing = bar.scan("find_me")
</pre>
