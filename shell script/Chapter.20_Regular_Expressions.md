# In This Chapter
#### This chapter describes how to create regular expressions in both the sed editor and the gawk program that can filter out just the data you need

1. Defining regular expressions
2. Looking at the basics
3. Extending our patterns
4. Creating expressions


# 1. Defining regular expressions
A regular expression is a pattern template you define that a Linux utility uses to filter text.


if the data doesn’t match the pattern, it’s rejected.
![image](https://user-images.githubusercontent.com/78835559/112401314-96fb9380-8d4d-11eb-9c40-dacca0d9fb3f.png)


A regular expression is implemented using a regular expression engine.
The biggest problem with using regular expressions is that there isn’t just one set of them.

The Linux world has two popular regular expression engines

+ The POSIX Basic Regular Expression (BRE) engine
+ The POSIX Extended Regular Expression (ERE) engine

BRE에 비해 ERE가 더 많은 pattern을 제공하는반면 속도가 느리기 때문에
sed에 경우 속도가 빠른 BRE를 사용하고 gawk 와 같은 programming languages는 더 많은 pattern_match를 위해 ERE를 사용!


### wildcard characters
represent one or more characters 
<pre>
$ ls *.txt
a.txt  b.txt  c.txt
</pre>

# 2. Looking at the basics


text matching 을 실험하기 위해 
> $ echo “test” | sed -n ‘/test/p’ 

input stream에 test라는 pattern이 포함되면 출력하는 command 를 사용하자. 

## 1) Plain text

###### <대소문자x>

<pre>
$ echo “This” | sed -n ‘/this/p’
$
$ echo “This” | sed -n ‘/This/p’
This is a test
</pre>


###### <matching text anywhere in the data stream>


<pre>
$ echo “books” | sed -n ‘/book/p’
books
</pre>


###### <You can include spaces>
  
  
<pre>
$ echo “This is line number 1” | sed -n ‘/ber 1/p’
This is line number 1
</pre>




## 2) Special characters

Regular expression patterns assign a special meaning to a few characters
These special characters are recognized by regular expressions
#### .  *  []  ^$  {}  \  +  ?  |  ()

If you want to use one of the special characters as a text character, you need to escape character(\).

### [a. Anchor characters]()
You can use two special characters to anchor a pattern to either the beginning or the end of lines in the data stream.

#### The caret character (∧) defines a pattern that starts at the beginning of a line of text in the data stream.

<pre>
$ echo “The book store” | sed -n ‘/^book/p’
$
$ echo “books are great” | sed -n ‘/^book/p’
books are great
</pre>

If you position the caret character in any place other than at the beginning of the pattern, it
acts like a normal character and not as a special character:
<pre>
$ echo “This ^ is a test” | sed -n ‘/s ^/p’
This ^ is a test
</pre>

#### The opposite of looking for a pattern at the start of a line is looking for it at the end of a line. The dollar sign ($) special character defines the end anchor

<pre>
$ echo “This is a good book” | sed -n ‘/book$/p’
This is a good book
</pre>

#### Combining anchors
look for a line of data containing only a specific text pattern

<pre>
$ echo "This is text" | sed -n '/^This$/p'
$ echo "This" | sed -n '/^This$/p'
This
</pre>

you can filter blank lines from the data stream.

<pre>
$ echo "" | sed -n '/^$/p'

</pre>



### [b. The dot character]()

The dot special character is used to match **any single character** except a newline character.
<pre>
$ cat data
cat
hat
at
 at
$ sed -n '/.at/p' data
cat
hat
 at
</pre>
*# space 도 single character로 인식*


### [c. Character classes]()
The dot special character is great for matching a character position against any character,
but what if you want to limit what characters to match?

<pre>
$ sed -n ‘/[ch]at/p’ data
cat
hat
</pre>


you can use e more than one character class and also use numbers in them.
<pre>
$ echo 603 | sed -n '/[0123456789][0123456789][0123456789]/p'
603
</pre>


### [d. Negating character classes]()

you can also reverse the effect of a character class
<pre>
$ sed -n '/[^ch]at/p' data
 at
</pre>
*# c, h 이외에 다른 문자가 무조건 하나 있어야함*

### [e. Using ranges]()
You can use a range of characters within a (c. character class)
<pre>
$ echo 603 | sed -n '/^[0-9][0-9][0-9]$/p'
603
</pre>

You can also specify multiple, non-continuous ranges in a single character class:
<pre>
$ sed -n ‘/[a-ce-m]at/p’ data
cat
hat
</pre>

### [f. Special character classes]()

|Class| Description|
|-|-|
|[[:alpha:]] |Matches any alphabetical character, either upper or lower case|
|[[:alnum:]]| Matches any alphanumeric character 0–9, A–Z, or a–z|
|[[:blank:]]| Matches a space or Tab character|
|[[:digit:]]| Matches a numerical digit from 0 through 9|
|[[:lower:]]| Matches any lowercase alphabetical character a–z|
|[[:print:]]| Matches any printable character|
|[[:punct:]]| Matches a punctuation character|
|[[:space:]]| Matches any whitespace character: space, Tab, NL, FF, VT, CR|
|[[:upper:]]| Matches any uppercase alphabetical character A–Z|

###### <example>
<pre>
$ echo “abc” | sed -n ‘/[[:alpha:]]/p’
abc
</pre>
  




### [g. The asterisk]()

Placing an asterisk after a character signifies that the character must appear zero or more
times in the text to match the pattern: **(It's different from the * used alone.)**
<pre>
$ echo “ik” | sed -n ‘/ie*k/p’
ik
$ echo “iek” | sed -n ‘/ie*k/p’
iek
$ echo “ieek” | sed -n ‘/ie*k/p’
ieek
</pre>







# 3. Extending our patterns

# 4. Creating expressions
