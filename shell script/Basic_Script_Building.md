# Basic Script Building



Creating a Script File
---------

#!/bin/bash
*첫번째줄에 사용되는 #! 는 일반적인 경우와 달리 사용되는 shell script를 표시한다.*


shell script실행하기
-------
다른 command의 경우 file 이름만 입력하면 실행이 되는데 이는 입력된 file의 경로를 shell이 자동으로 찾아주기 때문에 가능하다. 

그럼으로 shellscript를 실행하기 위해서는 $PATH에 shell script 경로를 설정해준다. 
<pre>
$ export PATH=$PATH:/home/user
$ shellscript
</pre>

혹은 경로를 수동으로 입력해 사용한다. 
<pre>
$ ./shellscript
</pre>

-------
|shell script |||
|-|-|-|
|; |semicolon| chain commands together into a single step|
|# |pound sign| is used as a comment line |
|$variable||variable을 참조할때 사용|
|${variable}||

|command ||
|-|-|
|echo "string"|string 출력|
|echo -n "string"|다음 command 의 output 과 같은 라인에 string 출력|

Using Variables
----
Variable : temporarily store information within the shell script for use with other commands in the script 

### 1. Environment variables
|command ||
|-|-|
|$set | list of environment variables |

<pre>
$ echo "user info for userid : $USER , $UID , $HOME"
</pre>
*$( dollar sing ) 과 함께 사용하면 script 내부에서 원하는 환경 변수를 참조할수 있음*

<pre>
$ echo "cost is $15"
$ cost is 5
</pre>
*위의 경우 쉘이$를 변수를 참조하는 $로 인식하기 때문에 \$ 를 사용하여 이를 방지하여야 한다.*

### 2. User variables

