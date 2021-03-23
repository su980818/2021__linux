# In This Chapter

#### sed command를 이용해 test 문서를 우리가 원하는 format으로 자동으로 처리해 보자. 
 


# 1. Getting to know the sed editor
#### The sed editor is called a stream editor, A stream editor edits a stream of data based on a set of rules you supply ahead of time, before the editor processes the data.

**< sed editor >**
1. Reads one data line at a time from the input
2. Matches that data with the supplied editor commands
3. Changes data in the stream as specified in the commands
4. Outputs the new data to STDOUT

![image](https://user-images.githubusercontent.com/78835559/112078885-8834a580-8bc2-11eb-8405-82ab1afc06f4.png)




> **sed** *options script file*

|Option |Description|
|-|-|
|-e script| Adds commands specified in the script to the commands run while processing the input|
|-f file| Adds the commands specified in the file to the commands run while processing the input|
|-n| Doesn’t produce output for each command, but waits for the print command|


# 2. Commanding at the sed Editor Basics

## 1) Introducing  substitution options
#### 특정 문자를 다른 문자로 바꾸는 script
> s/pattern/replacement/
<pre>
$ sed 's/test/trial/' << EOF
> 1. test is test
> 2. Test is test
> EOF
1. trial is test
2. Test is trial
</pre>
*# it replaces only the first occurrence in each line*

**SOLUTION**_ use a substitution flag!
> s/pattern/replacement/flags

|flags||
|number| indicating the pattern occurrence for which new text should be substituted|
|g| indicating that new text should be substituted for all occurrences of the existing text|
|p| indicating that the contents of the original line should be printed|
|w file| which means to write the results of the substitution to a file|

<g 를 이용해 모든 test substitude>
<pre>
$ sed 's/test/trial/g' << EOF
1. test is test
2. Test is test
EOF
1. trial is trial
2. Test is trial
</pre>

<옵션-n과 flag p 를 이용해 처리가 이루어진 line출력>
<pre>
$ sed -n 's/test/trial/p' << EOF
> 1. this is test
> 2. this is line
> EOF
1. this is trial
</pre>

