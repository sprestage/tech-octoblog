---
layout: post
title: "String manipulation in Ruby"
date: 2014-03-21 12:12:17 -0700
comments: true
categories:
- Ruby
- strings
---
Set vs concatenate
=======
Set variable equal to this string.  No initialization needed.
```
farewell = "Good"  
```

Print out that string.
```
puts farewell
```

This will be the output.
```
  => Good
```

Concatenation requires the variable to be initialized.  This only works because the variable was initialized above.
```
farewell << "bye!"  
```

Print out that string.
```
puts farewell
```

This will be the output.
```
  => Goodbye!
```

String operations
=======
Find where a substring is within the source string using index.
```
"hello".index('e')             #=> 1
"hello".index('lo')            #=> 3
"hello".index('a')             #=> nil
"hello".index(?e)              #=> 1
"hello".index(/[aeiou]/, -3)   #=> 4
```

Take input from the user:
```
puts "Please input some text: "
foo = gets.chomp
puts foo
```

If you are using ARGV to bring in command line arguments when you launch your app, you will run into conflict when using gets.  You can work around this two ways.  First is to use perform whatever tasks you need to on ARGV, then:
```
ARGV.clear
foo = gets.chomp
```

Otherwise, everytime you call gets, you will need to specify that it is from IO, not Kernal:
```
foo = $stdin.gets.chomp
```

Replace the first instance of the sub_string, "replace_me", with the contents of foo.
```
bar = bar.sub("replace_me", foo)
```

Globally replace the sub_string, "replace_me", with the contents of foo.
```
bar = bar.<b>g</b>sub("replace_me", foo)
```

Find the first example of substring, "find_me".  This is most often used with regex in place of the "find_me" string.  Returns a string.
```
bing = bar.match("find_me")
```

Find the every example of substring, "find_me".  This is most often used with regex in place of the "find_me" string.  Returns an array of strings.
```
bing = bar.scan("find_me")
```
