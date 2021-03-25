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












# 2. Looking at the basics

# 3. Extending our patterns

# 4. Creating expressions
