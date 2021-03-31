# In This Chapter

1. Managing processes (ps , top , kill , killall)
2. Mounting new disks ( mount , umount)
3. Monitor disk space ( df , du)
4. process data ( sort , grep )
5. Archiving data ( gzip , tar )

# 1. Managing processes
ps have 3 types style
+ Unix-style parameters, which are preceded by a dash
+ BSD-style parameters, which are not preceded by a dash
+ GNU long parameters, which are preceded by a double dash

### a. Unix-style parameters


매우 많은 옵션 parameter 들이 있지만. 
The key to using the ps command is not to memorize all the available parameters, 대신 유용한 parameter 조합을 기억하자.

> $ ps -ef
<pre>
$ ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  2 10:04 ?        00:00:00 /init
root         8     1  0 10:04 tty1     00:00:00 /init
seungwoo     9     8  2 10:04 tty1     00:00:00 -bash
seungwoo    69     9  0 10:04 tty1     00:00:00 ps -ef
</pre>
###### *# 현재 running system을 중요한 정보와 함께 보여줌*


|information||
|-|-|
|UID| The user responsible for launching the process|
|PID| The process ID of the process|
|PPID| The PID of the parent process (if a process is started by another process)|
|C| Processor utilization over the lifetime of the process|
|STIME| The system time when the process started|
|TTY|The terminal device from which the process was launched|
|TIME| The cumulative CPU time required to run the process|
|CMD| The name of the program that was started|

더 많은 정보를 보고싶다면
> $ ps -l
<pre>
$ ps -el
F S   UID   PID  PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
0 S     0     1     0  0  80   0 -  2235 ?      ?        00:00:00 init
0 S     0     8     1  0  80   0 -  2235 -      tty1     00:00:00 init
0 S  1000     9     8  0  80   0 -  4554 -      tty1     00:00:00 bash
0 R  1000    72     9  0  80   0 -  4644 -      tty1     00:00:00 ps
</pre>

## 2) Stopping processes
process 는 signal을 통해서 관리됨 


|Signal| Name |Description|
|-|-|-|
|1 |HUP| Hangs up|
|2 |INT |Interrupts|
|3 |QUIT |Stops running|
|9 |KILL |Unconditionally terminates|
|11| SEGV| Produces segment violation|
|15 |TERM |Terminates if possible|
|17| STOP |Stops unconditionally, but doesn’t terminate|
|18 |TSTP |Stops or pauses, but continues to run in background|
|19 |CONT |Resumes execution after STOP or TSTP|

##### kill command allows you to send signals to process based on their process ID

> $ kill 3940

3940 pid 에 defalut로 TERM 을 보내는데 일반적으로 무시되는 signal

> $ kill -s HUP 3940

HUP signal을 보냄


##### The killall command is a powerful way to stop processes by using their names rather than the PID numbers.

> $ killall http*
wildcard 를 사용할수 있음으로 여러 process를 처리하기에 유용함


# 2. Mounting new disks
linux system은 물리적인 저장소를 virtual directory에 저장함으로써 물리적인 경로와 가상경로를 다르게 할수있음. 

#### Before you can use a new media disk on your system, you must place it in the virtual directory. This task is called mounting.


By default, the mount
command displays a list of media devices currently mounted on the system:
> $ mount

<pre>
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
C:\ on /mnt/c type drvfs (rw,noatime,uid=1000,gid=1004,case=off)
D:\ on /mnt/d type drvfs (rw,noatime,uid=1000,gid=1004,case=off)
E:\ on /mnt/e type drvfs (rw,noatime,uid=1000,gid=1004,case=off)
</pre>

provides four pieces of information

+ The device filename of the media
+ The mount point in the virtual directory where the media is mounted
+ The filesystem type
+ The access status of the mounted media


### a. Basic command for manually mounting a media device:
> **mount** *-t type device directory*

### b. Unmount

> **umount** *directory*


# 3. Monitor disk space

### a. How much disk space 

> $ df
<pre>
$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
C:\            243619296 165992956  77626340  69% /mnt/c
D:\            976629756 312019052 664610704  32% /mnt/d
E:\              5230592   3442332   1788260  66% /mnt/e
</pre>

###### *-h : print human-readable form*

### b. the disk usage for a specific directory (by default, the current directory)

> $ du
<pre>
$ du -h
12K     ./usbip-win/userspace/doc
152K    ./usbip-win/userspace/lib
92K     ./usbip-win/userspace/src/usbip
52K     ./usbip-win/userspace/src/usbipd
144K    ./usbip-win/userspace/src
1.1M    ./usbip-win/userspace
3.4M    ./usbip-win
4.9M    .
</pre>
###### *# The number at the left of each line is the number of disk blocks that each file or directory takes.*



# 4. process data
## 1) Sorting data
> $ **sort** *file_name*

+ defalut : 문자를 기준으로 sort 
+ -n : 숫자순으로 sort
+ -M : 3글자의(Feb) month순으로 sort

+ -t : field separater
+ -k : 어느 field를 기준으로 sort하는지 

`$ sort -t ':' -k 3 -n  /etc/passwd`

###### <활용 예시>
<pre>
 $ du | sort -nr
5012    .
3448    ./usbip-win
1660    ./usbip-win/.git
1596    ./usbip-win/.git/objects/pack
1596    ./usbip-win/.git/objects
1036    ./usbip-win/userspace
</pre>


## 2) Searching for data 
> **grep** *[options] pattern [file]*


+ -v : reverse the search
+ -n : print matching patterns whith line numbers
+ -c :  count how many lines contain the matching pattern
+ -t : If you need to specify more than one matching pattern,

`$ grep -e a -e b file` 보다는 regular expression을 사용가능함으로 `grep [ab] file`을 사용하자. 


+ egrep : extended reglar expression
+ fgrep : matching pattern as a list of fixed-string values

# 5. Archiving data 

## 1) compressing

|Utility| File Extension| Description|
|-|-|-|
|bzip2 |.bz2| Uses the Burrows-Wheeler block sorting text compression algorithm and Huffman coding|
|compress |.Z |Original Unix file compression utility; starting to fade away into obscurity|
|gzip |.gz| The GNU Project’s compression utility; uses Lempel-Ziv coding|
|zip |.zip |The Unix version of the PKZIP program for Windows|


linux use gzip 

+ gzip for compressing files
+ gzcat for displaying the contents of compressed text files
+ gunzip for uncompressing files

## 2) tar 

Although the zip command works great for compressing and archiving data into a single
file, it’s not the standard utility used in the Unix and Linux worlds. By far the most
popular archiving tool used in Unix and Linux is the tar command


> **tar** *function [options] object1 object2 …*

###### < The tar Command Functions >
|Function |Long Name |Description|
|-|-|-|
|-A|—concatenate |Appends an existing tar archive file to another existing tar archive file|
|-c |—create| Creates a new tar archive file|
|-d |—diff |Checks the differences between a tar archive file and the filesystem|
| | —delete| Deletes from an existing tar archive file|
|-r| —append| Appends files to the end of an existing tar archive file|
|-t |—list |Lists the contents of an existing tar archive file|
|-u |—update| Appends files to an existing tar archive file that are newer than a file with the same name in the existing archive|
|-x |—extract| Extracts files from an existing archive file|

###### < The tar Command Options>
|Option| Description|
|-|-|
|-C dir |Changes to the specified directory|
|-f file |Outputs results to file (or device) file|
|-j |Redirects output to the bzip2 command for compression|
|-p |Preserves all file permissions|
|-v| (Verbose) Lists files as they are processed|
|-z |Redirects the output to the gzip command for compression|

`tar -cvf test.tar test/ test2/`
: create test.tar 

`tar -tf test.tar` : lists (but doesn’t extract) the contents of the tar file test.tar. 

`tar -xvf test.tar` : extracts the contents of tar file
