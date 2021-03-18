
# Chapter 15: Presenting Data

#### [ Chapter 11 demonstrated how to redirect the output of a command to a file. This chapter expands on that topic by showing you how you can redirect the output of your script to different locations on your Linux system.]()


1. Understanding Input and Output
2. Redirecting Output in Scripts
3. Redirecting Input in Scripts
4. Creating Your Own Redirection
5. Listing Open File Descriptors
6. Suppressing Command Output
7. Using Temporary Files
8. Logging Messages
9. Practical Example



# 1. Understanding Input and Output


## 1) Standard file descriptors
+ [linux system handles everty object as a file. so that input and output process also are treated using file descriptor.]()
+  The bash shell reserves the first three file descriptors (0, 1, and 2) for special purposes

|File Descriptor| Abbreviation| Description| 
|-|-|-|
|0 |STDIN |Standard input| 
|1 |STDOUT |Standard output|
|2| STDERR |Standard error|

# 2. Redirecting Output in Scripts

~~(Chepter11)~~
|||
|-|-|
|1>| STDOUT으로 가던 output이 redirect됨|
|2>| STDERR로 가던 error가 redirect됨|
|&>| STDOUT STDERR로 가던 output,error가 redirect됨|



# 3. Redirecting Input in Scripts


## 1) Temporary redirections
#### [ descriptor number만 가지고 file_descriptor을 대표할수 있음]()

**precede the file descriptor number with an ampersand (&) [ <,> 와 &사이에 space가 없어야함!! ]() **
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

## 2) Permanent redirections

#### [ shell에게 특정 파일에 descriptor number을 부여함 for the duration of the script by using the exec command]()

> **exec** *descriptor_num>  destination*

### a) output permanent redirect

<pre>
#!/bin/bash
exec 1> output.txt
echo "It is originally directed to STDOUT "
</pre>


<pre>
$ cat output.txt
It is originally directed to STDOUT
</pre>


*# 1>은 exec 에서 사용될때는  destination에 file_descriptor_num을 부여 하는것으로 사용되고 redirection을 위해 사용될때는 정상출력 output을 redirect하는것을 의미* 

### b) input permanaet redirect
<pre>
#!/bin/bash
exec 0< input.txt
while read line
do
echo $line
done
</pre>
*# STDIN에서 input을 받아오는 read가 input.txt에서 input을 받아옴*


# 4. Creating Your Own Redirection


#### [위에서 사용된 exec를 사용해 file_descriptor_num(3-8)을 file에 부여하자]()
<pre>
#!/bin/bash
exec 3>test13out
echo “HELLO” >&3
</pre>


## #) Creating a read/write file descriptor
As you read and write data to and from a file, the shell maintains an internal pointer, indicating where it is in the file. Any reading or writing occurs where the file pointer last left off
<pre>
#!/bin/bash
exec 3<> input.txt
read line <&3
echo $line
echo "new line" >&3
</pre>

<pre>
cat input.txt
This is line1
new line
ine2
This is line3
</pre>
*# 1번 line을 읽고 그다음 줄로 internal pointer가 지정되있는 상태에서 new line이 write되어 원래있던 line2에 append됨*


## #) Closing file descriptors
If you create new input or output file descriptors, the shell automatically closes them when the script exit
There are situations, however, when you need to manually close a file descriptor before the end of the script.

`exec 3>&-`: Initialization internal pointer

# 5. Listing Open File Descriptors

#### [ command lists all the open file descriptors on the entire Linux system]()

**exec** : 모든 running process에 열려있는 file_descriptor를 출력  

<pre>
#!/bin/bash
exec 3> output.txt
exec 4< input.txt
exec 5<> in_out.txt
# (-a): 뒤에 option을 AND (-p): pid ($$): ps의 pid (-d): print descriptor_number
lsof -a  -p $$ -d0,1,2,3,4,5
</pre>
<pre>
$ ./script
COMMAND PID     USER   FD   TYPE DEVICE SIZE              NODE NAME
xx.sh   314 seungwoo    0u   CHR    4,2      18858823440106205 /dev/tty2
xx.sh   314 seungwoo    1u   CHR    4,2      18858823440106205 /dev/tty2
xx.sh   314 seungwoo    2u   CHR    4,2      18858823440106205 /dev/tty2
xx.sh   314 seungwoo    3w   REG    0,2    0 18858823440083396 /home/seungwoo/output.txt
xx.sh   314 seungwoo    4r   REG    0,2    0 30680772461793615 /home/seungwoo/input.txt
xx.sh   314 seungwoo    5u   REG    0,2    0 22236523160630176 /home/seungwoo/in_out.txt
</pre>

# 6. Suppressing Command Output

**/dev/null** :  null context file 

 #) [file 을 clear out 할때도 일반적으로 사용됨]()
<pre>
$ ERROR-command 2> /dev/null
$ cat /dev/null > testfile
</pre>

# 7. Using Temporary Files

#### [ 임시파일을 만드는 2가지 방법]()

## 1) **tmp directory** 
automatically remove any files in the /tmp directory at bootup.
## 2)  **$ mktemp** *name.XXXXXX* 
creating a temporary file have unique name  in  local directory and return file.name (with no path)
<pre>
tempfile=$(mktemp test19.XXXXXX)
</pre>

|option | |
|-|-|
| -t  | forces mktemp to create the file in the temporary directory of the system(/temp)|
|-d| create a temporary directory instead of a file.|
 
# 8. Logging Messages

#### [output을 STDOUT과 file 두곳 모두에 출력하고 싶을때]()

tee command: T-connector for pipes , STDIN 으로 부터 입력을 받아옴.

**tee** *filename*      ==     ( 1> &1 ) +  ( 1> *filename* )

|-a| append data to the file|
|-|-|

<pre>
$ echo HELLO | tee tempfile
HELLO
$ echo BY | tee -a tempfile
BY
</pre>



# 9. Practical Example

