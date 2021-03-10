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

list=$list” Connecticut”                            #  list의 마지막에 추가할수있음 ( " " 

for state in $list
do
echo “Have you ever visited $state?”
done
</pre>
