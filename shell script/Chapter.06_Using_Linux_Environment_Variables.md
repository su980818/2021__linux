# In This Chapter

programs and scripts use environment variables to obtain system information and
store temporary data and configuration information.

1. Looking at environment variables
2. Creating your own local variables
3. Removing variables
4. Exploring default shell environment variables
5. Setting the PATH environment variable
6. Locating environment files
7. Using variable arrays








# 1. Looking at environment variables

Two type environment variable
#### A. Global environment variables
are visible from the shell session and from any spawned child subshells. 

<pre>
$ printenv
SHELL=/bin/bash
WSL_DISTRO_NAME=Ubuntu-20.04
PWD=/home/seungwoo
LOGNAME=seungwoo
</pre>
*# The system environment variables almost always use all capital letters to differentiate them from normal user environment variables.*


#### B. Local  environment variables 
are available only in the shell that creates them

<pre>
$ set
BASH=/bin/bash[…]
[…]
colors=/etc/DIR_COLORS
my_variable=‘Hello World’
[…]
$
</pre>
*# local env + Global env  + user defiend variable 모두 등장*
# 2. Creating your own variables

#### Create local variable
> **my_variable=** *Hello*

<pre>
$ haha="LOCAL"
$ echo $haha
LOCAL
$ bash
bash start~$ echo $haha
</pre>

#### [After you set a local variable, it’s available for use anywhere within your shell process. However, if you spawn another shell, it’s not available in the child shell]()

#### Create Global variable
> **exprot** *my_varaible=HELLO*
<pre>
$ my_variable=“I am Global now”
$ export my_variable
$
$ echo $my_variable
I am Global now
$
$ bash
$
$ echo $my_variable
I am Global now
$
$ my_variable=“Null”
$
$ export my_variable
$
$ echo $my_variable
Null
$
$ exit
exit
$
$ echo $my_variable
I am Global now
</pre>

#### [parent->child 로 변수가 넘어가는건 가능하지만 반대는 항상 불가능!]()

# 3. Removing variables
> **unset** *my_variable*

# 4. Exploring default shell environment variables

###### |< The bash Shell Bourne Variables >
|Variable |Description|
|-|-|
|CDPATH A |colon-separated list of directories used as a search path for the cd command|
|HOME| The current user’s home directory|
|IFS A |list of characters that separate fields used by the shell to split text strings|
|MAIL |The filename for the current user’s mailbox (The bash shell checks this file for new mail.)|
|MAILPATH |A colon-separated list of multiple filenames for the current user’s mailbox (The bash shell checks each file in this list for new mail.)|
|OPTARG |The value of the last option argument processed by the getopt command|
|OPTIND |The index value of the last option argument processed by the getopt command|
|PATH |A colon-separated list of directories where the shell looks for commands|
|PS1| The primary shell command line interface prompt string|
|PS2| The secondary shell command line interface prompt string|

###### < The bash Shell Environment Variables >
~~추가~~

# 5. Setting the PATH environment variable
When you enter an external command (see Chapter 5) in the shell command line interface
(CLI), the shell must search the system to find the program. The PATH environment
variable defines the directories it searches looking for commands and programs.


All you need to do is reference the original PATH value and add any new
directories to the string. This looks something like this:

<pre>
PATH=$PATH":/home/seungwoo/"
seungwoo@DESKTOP-3QDOT80:~$ echo $PATH
/usr/local/sbin:/snap/bin:/home/seungwoo/
</pre>



# 6. Locating environment files

## 1) Understanding the login shell process


Linux system, the bash shell starts as a login shell. The login shell typically looks for five different startup files to process commands from:

+ /etc/profile
+ $HOME/.bash_profile
+ $HOME/.bashrc
+ $HOME/.bash_login
+ $HOME/.profile


### a. Viewing the /etc/profile file
The /etc/profile file is the main default startup file for the bash shell on the system. [All
users]() on the system execute this startup file when they log in.
<pre>
$ cat /etc/profile
 for i in /etc/profile.d/*.sh
 do
    if [ -r $i ]; then
      . $i
    fi
  done
</pre>
*# etc/profile.d 안에 script를 모두 실행시키는것을 볼수 있음.*


### b. Viewing the $HOME startup files

$HOME/.bashrc provide a [user-specific]() startup file for defining user-specific environment variables.


### c. BASH_ENV

login_shell 에서느 profile , bashrc 가 모두 실행되지만 bash를 통해 실행되는 interactive_shell에서는 bashrc만 실행됨

<pre>
PROFILE START
bash start
$ bash
bash start
</pre>

[script를 실행하면 생성되는 non-interactive_shell 은 아무것도 실행하지 않음.]()

[대신 non-interactive_shell에서는 BASH_ENV 를 확인하여 BASH_ENV안에 있는 commnad를 자동실행함]()
###### < script에서 .bashrc 를 startup파일로 지정하는 예시 >
<pre>
$ export BASH_ENV=$HOME/.bashrc
$ ./script.sh
bash start
script start
</pre>
###### *# non-interactive_sub_shell을 실행시 export를 해야 변수가 상속이 됨으로 export를 꼭 쓰자!*

## 2) Making environment variables persistent

위에서 배운 startup file 중에 하나에다가 선언하면 영구적으로 사용가능


# 7. Using variable arrays

