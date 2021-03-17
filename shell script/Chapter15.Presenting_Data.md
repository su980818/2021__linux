
# Chapter 15: Presenting Data

### [ Chapter 11 demonstrated how to redirect the output of a command to a file. This chapter expands on that topic by showing you how you can redirect the output of your script to different locations on your Linux system.]()


1. Understanding Input and Output
2. Redirecting Output in Scripts
3. Redirecting Input in Scripts
4. Creating Your Own Redirection
5. Listing Open File Descriptors
6. Suppressing Command Output
7. Using Temporary Files
8. Logging Messages
9. Practical Example



1.Understanding Input and Output
---

### 1) Standard file descriptors
+ [linux system handles everty object as a file. so that input and output process also are treated using file descriptor.]()
+  The bash shell reserves the first three file descriptors (0, 1, and 2) for special purposes

|File Descriptor| Abbreviation| Description| 
|-|-|-|
|0 |STDIN |Standard input| 
|1 |STDOUT |Standard output|
|2| STDERR |Standard error|

2.Redirecting Output in Scripts
---
~~(Chepter11)~~
|||
|-|-|
|1>| STDOUT으로 가던 output이 redirect됨|
|2>| STDERR로 가던 error가 redirect됨|
|&>| STDOUT STDERR로 가던 output,error가 redirect됨|



3.Redirecting Input in Scripts
---

### 1) Temporary redirections
### [ descriptor number만 가지고 file_descriptor을 대표할수 있음]()

**precede the file descriptor number with an ampersand (&)**
<pre>
#!/bin/bash
echo “This is an error” >&2
echo “This is normal output”
</pre>
<pre>
$ ./script 2> aa.txt
This is normal output
$ cat aa.txt
This is an error
</pre>

### 2) Permanent redirections
### [ shell에게 특정 파일에 descriptor number을 부여함 for the duration of the script by using the exec command]()

**exec** *descriptor_num>*  *destination*
**a)** output permanent redirect
</pre>
#!/bin/bash
exec 1> output.txt
echo "It is originally directed to STDOUT "
</pre>
<pre>
$ cat output.txt
It is originally directed to STDOUT
</pre>
*# 1>은 exec 에서 사용될때는  destination에 file_descriptor_num을 부여 하는것으로 사용되고 redirection을 위해 사용될때는 정상출력 output을 redirect하는것을 의미* 

**b)** input permanaet redirect
<pre>
#!/bin/bash
exec 0< input.txt
while read line
do
echo $line
done
</pre>
*# STDIN에서 input을 받아오는 read가 input.txt에서 input을 받아옴*


4.Creating Your Own Redirection
-----

5.Listing Open File Descriptors
----

6.Suppressing Command Output
----

7.Using Temporary Files
----

8.Logging Messages
-----

9.Practical Example
-----
