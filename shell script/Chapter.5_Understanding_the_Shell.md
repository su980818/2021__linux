# In This Chapter

### [This chapter takes you through learning about the shell process.]()

1.Investigating Shell Types

2.Understanding the Parent/Child Shell Relationship

3.Using Subshells Creatively

4.Investigating Built-in Shell Commands

1.Investigating Shell Types
----

**/etc/passwd**  : 각 user의 default shell을 확인할수있음.

**/bin/bash**   : 원하는 shell을 실행하여 사용하자.


2.Understanding the Parent/Child Shell Relationship
----
### [shell_process 위에 shell_process 를 실행하는 경우에 각각을 parent, child shell로 구분 할수 있음.]()

parent shell 이 생성한 child shell ( sub shell )에 parent의 환경 context 의 일부분이 상속됨. (chapter6 참조)

### 1) sub_shell이 생성되는 경우
-----------
#### a) shell 을 command를 통해 실행.
<pre>
$ bash
bash start
$ pstree
init─┬─init───bash───bash───pstree
     └─{init}
</pre>

#### b) shell_script 를 실행하면 자동으로 sub shell을 생성하여 이를 이용해 shell_script를 실행시킴.

#### c) process list : `$ (command1 ; command2)`
<pre>
$ (sleep 1 ; pstree)
init─┬─init───bash───bash───pstree
     └─{init}
</pre>



`$BASH_SUBSHELL` :  sub_shell depth를 return 하는 variable




3.Using Subshells Creatively
-----
### [현재 shell에서 sub_shell을 back_ground로 실행함으로서 shell의 생산성을 향상시키는 것이 목적.]()
 [이러한 sub_shell 을 interactive_shell 이라고 부름.]()
 
**background mod** : 하나의 process가 완료될때까지 shell 이 $를 반환해주지 않는데 background에서 실행하게 함으로 현재 shell이 하나의 process에만 잡혀있지 않게 process를 실행하는 방법
 

### 1) start background sub_shell
-------

#### a)  Putting process lists into the background

`$ (command1 ; command2)&`

#### b)  Co-processing 
COPROC 라는 이름의 subshell을 back ground로 생성하고 이 안에서 command를 실행. 

`$ coproc *command`

*# process list 를 자동으로 back ground로 실행하는것과 비슷한 효과*

4.Investigating Built-in Shell Commands
-----
### 1) Looking at external commands
------
#### [Whenever an external command is executed, a child process is created . This action is termed forking]()
<pre>
$ ps -f
UID        PID  PPID  C STIME TTY          TIME CMD
seungwoo   159   158  4 21:47 tty1     00:00:00 -bash       
seungwoo   172   159  0 21:47 tty1     00:00:00 ps -f      
</pre>
*# ppid 가 bash 인 ps -f process가 실행됨*



### 2) Looking at built-in commands
------
#### [When using a built-in command, no forking is required. Therefore, built-in commands are less expensive]()

`type command` 
`which commnand` : 이를 이용하여 external <-> built-in command를 구분할수 있음.

*# external command program is typically located in /bin, /usr/bin, /sbin, or /usr/sbin.*

*# 몇몇 경우에 두가지 flavor을 모두 가지는 command 존재 ( type -a 를 통해 확인가능 )*


### #) Using the history command
------
`history` :  show a recently used commands list (built-in)

~~Command history is kept in the hidden .bash_history file, which is located in the user’s
home directory. Be careful here. The bash command history is stored in memory and then
written out into the history file when the shell is exited:~~

### #) Using command aliases
-------
`alias -p` : alias 된 command 출력

`alias alias_variable=command` : command 를 variable을 통해 빠르게 사용가능.
