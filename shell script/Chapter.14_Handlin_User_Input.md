# Handling User Input
#### [you need to write a script that has to interact with the person running the script, so let learn retrieving data from people.]()

1. Passing Parameters
2. Using Special Parameter Variables
3. Being Shifty
4. Working with Options
5. Standardizing Options
6. Getting User Input



# 1. Passing Parameters

+ space separator로 분리됨.
+ string , numerical_value 둘다 parameter로 pass할수 있음.
+ $1 부터 시작해서 separate된 순으로  각각 $num에 저장됨.
<pre>
#!/bin/bash
echo  $1  ${2}
</pre>
<pre>
$ ./script 100 "SEUNGWOO"
100 SEUNGWOO
</pre>


## 1) Reading the script name ( $0 and basname_command)
#### [ basename command를 이용하여 (전체 실행 경로 + command)가 저장된 $0 에서 (command)만 추출할수 있음. ]()
<pre>
#!/bin/bash
echo  $0  $(basename $0)
</pre>
<pre>
$ ./xx.sh aa "bb"
./xx.sh xx.sh
</pre>

## 2) Testing parameters

#### If the script is run without the parameters, bad things can happen so  check your parameters to make sure the data is there before using it:
<pre>
#!/bin/bash
if [ -n “$1” ] ; then
echo Hello $1, glad to meet you.
else
echo “Sorry, you did not identify yourself. “
fi
</pre>

# 2. Using Special Parameter Variable


|variable||
|-|-|
| $# | number of parameters |
| $* | takes all the parameters supplied on the command line as a single word. |
| $@ | takes all the parameters supplied on the command line as separate words in the same string.(for 문에서 사용)|
  
*# 마지막 parameter을  ${$#}으로 참조할수 있을꺼 같지만 ${!#}을 사용해야 사용가능 ( 이유불명 )*

# 3. Being Shifty with shift_command
----
#### The shift command literally shifts the command line parameters in their relative positions.
#### This is another great way to iterate through command line parameters, especially if you don’t know how many parameters are available. 

> **shift** *# (default 1)*
<pre>
#!/bin/bash
# parameter를 left shift를 하여 $1로 모든 parameter 을 사용할수 있음.
echo
count=1
while [ -n “$1” ]
do
echo $1
shift
done
</pre>

# 4. Working with Options

#### [ 위에서 사용된 shift  + if(or case) 를 조합하여 parameter 과 -가 붙은 option을 구분해서 입력으로 받아보자. ]()

<pre>
#!/bin/bash
while [ -n "$1" ]
do
        if [[ "$1" == "-a" ]] ; then
                echo "$1 is option "

        elif [[ "$1" == "-b" ]] ; then
                echo "$1 is option"
                if [ -n "$2" ] ; then
                        echo "$2 is parameter of $1"
                        shift
                else
                        echo "$1 not have parameter"
                fi


        else
                echo "$1 is not option "
        fi

        shift
done
</pre>

#### [**But** this doesn’t work if you try to combine multiple options in one parameter: ]() 
<pre> 
$ ./test17.sh -ac 
-ac is not options
</pre>

## SOLUTION 1) Using the getopt command
#### [ 입력 parameter 을 separate 하여 정리된 문자열로 출력해보자. ]()

> **getopt** *optstring parameters*
 
list each command line option letter you’re going to use in your script in the optstring. Then place a colon after each option letter that requires a parameter value. 


<pre>
$ getopt ab:c  -a -b "b's_parameter"  -c -d xx
getopt: invalid option -- 'd'
 -a -b b's_parameter -c -- xx
</pre>
*# invalid parameter는 오류를 출력( -q : 출력을 quit ) ,  추가적인 parameter는 -- 를 통해 option과 구분해서 보여줌* 

 
#### [**But** It interpreted the space as the parameter separator, instead of following the double quotation marks ](http)
<pre>
$ ./script "test2 test3”  
"test2
test3"
</pre>  



## SOLUTION 2) Advancing to getopts
#### [ 입력 parameter 을 separate 하여 list로 출력해보자. ]()

> **getopts** *optstring variable*  
<pre>
#!/bin/bash

while  getopts ab:c opt
do
        if [[ "$opt" == "a" ]] ; then
                echo "$opt is option "

        elif [[ "$opt" == "b" ]] ; then
                echo "$opt is option"
                if [ -n "$OPTARG" ] ; then
                        echo "$OPTARG is parameter of $opt"
                        shift
                else
                        echo "$opt not have parameter"
                fi


        else
                echo "$opt is not option "
        fi

done
</pre>
*# getopt 와 다르게 -a -> a로 변경해서 저장하고있음*

## #) Standardzing Options (관행 표현)

|Option| Description|
|-|-|
|-a |Shows all objects|
|-c |Produces a count|
|-d |Specifies a directory|
|-e |Expands an object|
|-f| Specifies a file to read data from|
|-h|Displays a help message for the command|
|-i |Ignores text case|
|-l| Produces a long format version of the output|
|-n| Uses a non-interactive (batch) mode|
|-o| Specifies an output file to redirect all output to|
|-q| Runs in quiet mode|
|-r| Processes directories and files recursively|
|-s| Runs in silent mode|
|-v| Produces verbose output|
|-x| Excludes an object|
|-y| Answers yes to all questions|

# 6. Getting User Input

#### [ 시작할때 parameter을 전달하는게 아닌 running 상태의 프로세스에 입력을 전달해보자.]()

> **read** *variables*

## 1) options
|options|-|
|-|-|
|-p "string" | specify a string directly in the read command line|
|-t #|  The -t option specifies the number of seconds for the read command to wait for input ( if falis , exit 0 ) |
|-n# |  When a preset number of characters has been entered, it automatically exits. |
|-s | sets the text color to the same as the background color |

<pre>
#!/bin/bash
read -p "ENTER[Y/N] :"n1 test
if [ $test = 'y' ] || [ $test = 'Y' ] ; then
        echo "yes!"
elif [ $test = 'N' ] || [ $test = 'n' ]   ; then
        echo "no!"
fi
</pre>


## 2) Reading from a file
#### [file에서 line 단위로 읽어들임 (pipe를 통해 입력해줘야함)]()
<pre>
#!/bin/bash
cat test | while read line
do
echo “Line : $line”
done
</pre>
