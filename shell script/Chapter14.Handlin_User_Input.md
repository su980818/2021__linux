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


2.Reading the script name : $0 and basname_command
-----
+ basename command 로 스크립트 실행 command가 저장된 $0 에서 실행경로를 뺄수 있음. 
<pre>
#!/bin/bash
echo  $0  $(basename $0)
</pre>
<pre>
$ ./xx.sh aa "bb"
./xx.sh xx.sh
</pre>

3.Testing parameters
----
+ If the script is run without the parameters, bad things can happen so  check your parameters to make sure the data is there before using it:
<pre>
#!/bin/bash
if [ -n “$1” ] ; then
echo Hello $1, glad to meet you.
else
echo “Sorry, you did not identify yourself. “
fi
</pre>

4.Using Special Parameter Variable
----

|variable||
|-|-|
| $# | number of parameters |
| $* | takes all the parameters supplied on the command line as a single word. |
| $@ | takes all the parameters supplied on the command line as separate words in the same string.(for 문에서 사용)|
  
*# 마지막 parameter을  ${$#}으로 참조할수 있을꺼 같지만 ${!#}을 사용해야 사용가능 ( 이유불명 )*

5.Being Shifty with shift_command
----
+ The shift command literally shifts the command line parameters in their relative positions.
+ This is another great way to iterate through command line parameters, especially if you don’t know how many parameters are available. 

<pre>
#!/bin/bash
echo
count=1
while [ -n “$1” ]
do
echo $1
shift
don
</pre>




  
