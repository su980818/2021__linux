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
+ IFS=;
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
for (( a = 1; a < 10; a++ ))
