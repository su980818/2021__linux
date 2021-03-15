
[Chapter 11 demonstrated how to redirect the
output of a command to a file.]()

[This chapter expands on that topic by showing you
how you can redirect the output of your script to different locations on your Linux
system.]()


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
