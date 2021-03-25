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

BRE에 비해 ERE가 더 많은 pattern을 제공하여 sed에 경우 속도가 빠른 BRE를 사용하고 gawk 와 같은 programming languages는 더 많은 pattern을 위해 ERE를 사용!



> wildcard characters *  represent one or more characters 

<pre>
$ ls *.txt
a.txt  b.txt  c.txt
</pre>


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
#### .*[]^${}\+?|()

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



# 2. Looking at the basics

# 3. Extending our patterns

# 4. Creating expressions
