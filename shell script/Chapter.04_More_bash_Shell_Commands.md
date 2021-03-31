# In This Chapter

1. Managing processes (ps , top , kill , killall)
2. Mounting new disks
3. Sorting data
4. Archiving data

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


###  Basic command for manually mounting a media device:
> **mount** *-t type device directory*

### Unmount

> **umount** *directory*


### How much disk space 

> $ df
<pre>
$ df
Filesystem     1K-blocks      Used Available Use% Mounted on
C:\            243619296 165992956  77626340  69% /mnt/c
D:\            976629756 312019052 664610704  32% /mnt/d
E:\              5230592   3442332   1788260  66% /mnt/e
</pre>

###### *-h : print human-readable form*

### the disk usage for a specific directory (by default, the current directory)

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



# 3. Sorting data
> $ sort file_name

+ defalut : 문자를 기준으로 sort 
+ -n : 숫자순으로 sort
+ -M : 3글자의(Feb) month순으로 sort

+ -t : field separater
+ -k : 어느 field를 기준으로 sort하는지 

> $ sort -t ':' -k 3 -n  /etc/passwd

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



# 4. Archiving data
