# Basic Script Building


1. Creating a Script File
2. Displaying Messages
3. Using Variables
4. Redirecting Input and Output
5. Pipes
6. Performing Math
7. Performin floating-point
8. Exiting the Script


# 1. Creating a Script File




## 1) shell script 선언하기

#### #!/bin/bash


#### [첫번째줄에 사용되는 #은 일반적인 #의 사용법과 달리 와 달리 !와 합쳐저 이 file이 shell script임을 설정해준다.]()


## 2) shell script실행하기

#### [다른 command의 경우 file 이름만 입력하면 실행이 되는데 이는 입력된 file의 경로를 shell이 자동으로 찾아주기 때문에 가능하다.]() 

그럼으로 shellscript를 실행하기 위해서는 $PATH에 shell script 경로를 추가해 주어야 한다. 
<pre>
$ export PATH=$PATH:/home/user
$ shellscript
</pre>

혹은 경로를 수동으로 입력해 사용한다. 
<pre>
$ ./shellscript
</pre>


|shell script |||
|-|-|-|
|; |semicolon| chain commands together into a single step|
|# |pound sign| is used as a comment line |

# 2. Displaying Messages
 
#### string 을 출력해 보자. 
|command ||
|-|-|
|echo "string"|string 출력|
|echo -n "string"|다음 command 의 output 과 같은 라인에 string 출력|

# 3. Using Variables

Variable : temporarily store information within the shell script for use with other commands in the script 
|shell script ||
|-|-|
|varialbe=value|varaible에 값 할당(assign)|
|varialbe=&(command)|command의 output을 variable에 할당|
|$variable|variable을 참조할때 사용(reference)|
|${variable}|위와 동일|

## 1) Environment variables


> $set : list of environment variables 

**<$ 과 함께 사용하여 script 내부에서 원하는 환경 변수를 참조할수 있음>**
<pre>
$ echo "user info for userid : $USER , $UID , $HOME"
</pre>

**<escape 문자/ 사용 예시>**
<pre>
$ echo "cost is $15"
cost is 5
</pre>
*# 위의 경우 쉘이$를 변수를 참조하는 $로 인식하기 때문에 \$ 를 사용하여 이를 방지하여야 한다.*

## 2) User variables


#### = 을  통해 변수설정 가능 

중간에 공백이 있으면 안됨 , 변수를 설정할때는 $ 사용 x , 변수를 참조할때만 $ 사용

<pre>
value=10
echo value is $value
</pre>

## 3) Command substitution


#### [command 의 output 을 변수에 저장하기]() 

**value=$(command)**

*변수참조에 사용하는 ${valiable}와 다름!!!*

<pre>
test_value=$(date)
echo "the date is " $test_value
echo test > log.$test_value
#파일 이름에도 value를 참조하여 사용할수 있음. 
</pre>

**Caution**

script를 실행하는 shell위에 새로운 subshell을 생성하여 comand substitution을 수행하기 때문에 
sub shell 에서 선언한 변수의 경우 script shell에서는 선언이 되지 않음.

이와 별개로 script를 실행할때도 teminal shell위에 새로운 subshell을 생성하여 script를 수행하고 있는 것임. 

# 4. Redirection Input and Output


#### [stdout인 teminal 이 아니라 지정한 file에 ouput을 출력해보자. ]()

|command ||command||
|-|-|-|-|
|>| overwrite to file |<| input redirection |
|>>|appand to file| |  |


**(#) inline input redirection** : 파일을 redirection 하는게 아닌 command line 을 순차적으로 input으로 사용해줌
<pre>
$ sort << EOF
> b
> d
> a 
>EOF
</pre>
*text marker를 설정하여 입력의 시작과 끝을 구분해줘야함 ( 관례상으로 EOF를 사용 )*

# 5. Pipes

#### [1번command의 output을 2번command 의 입력으로 redirection해줌]()
<pre>
$ 1st_command | 2st_command
$ ls -l | sort 
</pre>

# 6. Performing Math

#### [hell script 안에서 mathmatical operation 을 사용해보자. ]()
## 1) The expr command 

<pre>
$ expr 1 + 5
$ 6
</pre>
*shell 에서는 사용이 편리할수 있지만 script안에서는 expr의 operator들이 다른 의미를 갖기때문에 \과 함께 사용해야 하는 불편함이 있음*

## 2) Using brackets

[expr보다 편하게 사용해보자. ]()
<pre>
$  var1=$[1 + 5]
$  var2=$[$var1 * 6]
</pre>
*shell에서의 계산은 오직 정수에 한정된다.*

# 7. Performin floating-point 


## 1) The basics of bc

<pre>
bc  -q   # bc calculator 로 access , -q : 인삿말 삭제 
scale=2  # bc calculator의 한경변수 scale로 decimal place를 지정할수 있음.
12 * 5.4
64.8
quit     # quite bc calculator
</pre>

## 2) Using bc in script 

[pipe를 통해 bc에 input을 넣어주자. ]()
<pre>
#!/bin/bash
var1=$(echo "scale =4 ; 3.44 / 5 "| bc)
</pre>

긴 input에 경우 위에서 봤던 inline redirection을 통해 input을 넣어주자. 
<pre>
variable=$(bc << EOF
options
statements
expressions
EOF
)
</pre>

# 8. Exiting the Script 

#### [enviroment variable인 exit status 는 쉘에서 실행된는 모든 command가 끝날때 마다 command의 실행여부에 따라 특정 값이(0 - 255) exit에 전달됨.]() 
**$?** 를 사용하여 참조 가능. 

|Code| Description|
|-|-|
|0 |Successful completion of the command|
|1 |General unknown error|
|2 |Misuse of shell command|
|126 |The command can’t execute|
|127 |Command not found|
|128 |Invalid exit argument|
|128+x |Fatal error with Linux signal x|
|130 |Command terminated with Ctrl+C|
|255| Exit status out of range|

**exit** : command를 사용해 script 종료시 exit status 를 변경할수 있음
<pre>
#!/bin/bash
echo test 
exit 5
</pre>
