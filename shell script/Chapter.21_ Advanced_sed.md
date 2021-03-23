# In This Chapter

#### sed command를 이용해 test 문서를 우리가 원하는 format으로 자동으로 처리해 보자. 
 

1. Manipulating Text
2. Commanding at the sed Editor Basics
3. Summary

## 1) Getting to know the sed editor
#### The sed editor is called a stream editor, A stream editor edits a stream of data based on a set of rules you supply ahead of time, before the editor processes the data.

**< sed editor >**
a. Reads one data line at a time from the input
b. Matches that data with the supplied editor commands
c. Changes data in the stream as specified in the commands
d. Outputs the new data to STDOUT

![image](https://user-images.githubusercontent.com/78835559/112078885-8834a580-8bc2-11eb-8405-82ab1afc06f4.png)




> **sed** *options script file*

|Option |Description|
|-|-|
|-e script| Adds commands specified in the script to the commands run while processing the input|
|-f file| Adds the commands specified in the file to the commands run while processing the input|
|-n| Doesn’t produce output for each command, but waits for the print command|
