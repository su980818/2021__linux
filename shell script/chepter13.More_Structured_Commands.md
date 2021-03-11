1.The for Command
------------
### [반복문을 사용해 보자. (C언어 형식 , bash 형식)](http)
<pre>
for var in list
do
  command
done
</pre>
### 1) Reading value in a list
[most basic use of the for command is to iterate through a list of value](http)

<pre>
for test in Alabama Alaska Arizona Arkansas California Colorado
do
  echo The next state is $test
done
</pre>
*# c언어와 다르게 for문 안에서만 사용되는 변수가 아님*
### 2) Reading complex values in a list
[list 에 value들을 잘 구분해 보자](http)
#### a. Use the escape character (the backslash)
<pre>
$ cat test2
#!/bin/bash
for test in I don't know if \“this’ll\” work
do
  echo “word:$test”
done

</pre>
#### b. Use double quotation marks to define the values

<pre>
#!/bin/bash
for test in Nevada “New Hampshire” “New Mexico” “New York”
do
  echo “Now going to $test”
done
</pre>

### 3) Reading a list from a variable
<pre>
#!/bin/bash
list=“Alabama Alaska Arizona Arkansas Colorado”

list=$list” Connecticut”                            #  variable 의 마지막에 추가할수있음  ( variable이 string임으로 "를 사용해서 이어 붙임 )

for state in $list
do
echo “Have you ever visited $state?”
done
</pre>

### 4) Reading values from a command
> command 의 output을 입력으로 바꿔주는 $(command)를 사용하자!
<pre>
#!/bin/bash
for variable in $(ls)                             # space로 구분되는 ls의 output을 입력
do
  echo "$variable”
done
</pre>

2.Changing the field separator
-----
[IFS(internal field separator) : 문자열이 입력될때 구분자로 사용되는 character들을 저장하고 있는 환경변수 ](http) 
+ defalut로 space , tab , newline 이 지정되어 있음. 

+ IFS=$IFS$'characters'  를 통해 separator을 추가할수 있음. 
+ IFS=; 를 통해 하나의 character (;) 만 선언할수 있음. 
<pre>
   #!/bin/bash
  
  IFS=\n                                         #only use ENTER as seperator

   for x in $(cat file.txt)
  do
          echo $x
 done
 </pre>
3.Reading a directory using wildcards
------
[*를 사용하여 Directory 내부에 파일을 list로 전달해보자.](http)
<pre>
   #!/bin/bash
   #user의 모든 file을 재귀적으로 출력하는 script 
   for file in $1/*                              # $1/* = /home/user/*
   do
           if [ -d "$file" ] ; then
                   echo $file
                   $HOME/xx.sh $file
           elif [ -f "$file" ] ; then
                   echo $file
          fi
  done
</pre>


4.The C-Style for Command
-----
<pre>
for (( a = 1; a < 10; a++ ))
do
  echo $a
done
</pre>

**WARNING** 
a. The assignment of the variable value can contain spaces.
b. The variable in the condition isn’t preceded with a dollar sign.
c. The equation for the iteration process doesn’t use the expr command format( or bracket [ ] ).

5.The while Command
-----


<pre>
#!/bin/bash
var1=10
#while test $var1 -gt 0
while [ $var1 -gt 0 ]
do
echo $var1
var1=$[ $var1 - 1 ]
done
</pre>
*# while에 경우 조건문이 루프에 따라 변화가 있어야만 종료가 됨*

<pre>
!/bin/bash
var1=10
while echo $var1
[ $var1 -ge 0 ]
do
var1=$[ $var1 - 1 ]
done
</pre>
*# 조건문 안에 조건과 상관없는 command도 동시에 사용가능(같은 줄에다 사용하면 안됨)*

6.The until Command
-----
<pre>
until test commands
do
other commands
done
</pre>
*# while과 동일한 format*


7.Controlling the Loop
-----
### 1)break
<pre>
#!/bin/bash
while [ $var1 -lt 10 ]
do
  if [ $var1 -eq 5 ] ; then  
   break
  fi
  echo “Iteration: $var1”
  var1=$[ $var1 + 1 ]
done
</pre>

+ break n : where n indicates the level of the loop to break out of
<pre>
#!/bin/bash
for (( a = 1; a < 4; a++ ))
do
  echo “Outer loop: $a”
  for (( b = 1; b < 100; b++ ))
    do
     if [ $b -gt 4 ]; then
      break 2
     fi
     echo “ Inner loop: $b”
    done
done
</pre>
### 2)continue
same format whit break
<pre>
#!/bin/bash
do
echo “Iteration $a:”
  for (( b = 1; b < 3; b++ ))
  do
    if [ $a -gt 2 ] && [ $a -lt 4 ] ; then
      continue 2
    fi
   var3=$[ $a * $b ]
   echo “ The result of $a * $b is $var3”
  done
done
</pre>
