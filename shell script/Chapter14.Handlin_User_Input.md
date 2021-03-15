# Handling User Input
you need to write a script that has to interact with the person running the script,
so let learn retrieving data from people.

1.Passing Parameters
-----
+ space separator로 분리됨 string , numerical_value 둘다 pass 가능 
+ $1 부터 시작해서 separate된 순으로 $num에 저장됨 
<pre>
#!/bin/bash
echo  $1  ${2}
</pre>
<pre>
$ ./script 100 "SEUNGWOO"
100 SEUNGWOO
</pre>


### 1) Reading the script name : $0 and basname_command
+ basename command 로 스크립트 실행 command가 저장된 $0 에서 실행경로를 뺄수 있음. 
<pre>
#!/bin/bash
echo  $0  $(basename $0)
</pre>
<pre>
$ ./xx.sh aa "bb"
./xx.sh xx.sh
</pre>

### 2) Testing parameters

+ If the script is run without the parameters, bad things can happen so  check your parameters to make sure the data is there before using it:
<pre>
#!/bin/bash
if [ -n “$1” ] ; then
echo Hello $1, glad to meet you.
else
echo “Sorry, you did not identify yourself. “
fi
</pre>

2.Using Special Parameter Variable
----

|variable||
|-|-|
| $# | number of parameters |
| $* | takes all the parameters supplied on the command line as a single word. |
| $@ | takes all the parameters supplied on the command line as separate words in the same string.(for 문에서 사용)|
  
*# 마지막 parameter을  ${$#}으로 참조할수 있을꺼 같지만 ${!#}을 사용해야 사용가능 ( 이유불명 )*

3.Being Shifty with shift_command
----
+ The shift command literally shifts the command line parameters in their relative positions.
+ This is another great way to iterate through command line parameters, especially if you don’t know how many parameters are available. 

*shift # (default 1)*
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

4.Working with Options
-----
+ 위에서 사용된 shift  + if(or case) 를 사용하여 입력 parameter 중에 option을 입력으로 받아보자. 

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

**But** this doesn’t work if you try to combine multiple options in one parameter:  ` $ ./test17.sh -ac `

### SOLUTION 1) Using the getopt command
+ 입려 parameter 을 separate 하여 문자열로 출력해보자. 
 **getopt** *optstring parameters*
 
list each command line option letter you’re going to use in your script in the optstring. Then place a colon after each option letter that requires a parameter value. 

+  invalid parameter는 오류를 출력( -q 출력 quit ) ,  추가적인 parameter는 -- 를 통해 option과 구분해서 보여줌 
<pre>
$ getopt ab:c  -a -b "b's_parameter"  -c -d xx
getopt: invalid option -- 'd'
 -a -b b's_parameter -c -- xx
</pre>
 
**But** It interpreted the space as the parameter separator, instead of following the double quotation marks 
<pre>
$ ./script "test2 test3”  
"test2
test3"
</pre>  
### SOLUTION 2) Advancing to getopts
+ 입력 parameter 을 separate 하여 list로 출력해보자. 

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
