1.Working with the if-then Statement
------
### [조건문은 command의 exit status에 의해 조작됨](http)


* If the exit status of the command is zero , command list under the then section are executed.

* 기본 format 
<pre>
if command
then 
  commands
fi
</pre>
<pre>
if command ; then
  commands
fi
</pre> 


* If the exit status of the command is non-zero , command list under the else section are executed.
<pre>
if command  ; then
  commands
else
  commands
fi
</pre>

* else if 
<pre>
if command  ; then
  commands
elif command ; then
  commands
else
  commands
fi
</pre>

2.Trying the test Command
-------
### [if 문에 들어가는 조건문을 알아보자.(조건이 맞을시 exit = 0 , 조건이 틀릴시 exit != 0 을 반환하는 커맨드 )](http)

* variable에 값이 있는지 판단 하기 
* 아래에 나오는 1)2)3)의 if문 comparisons을 사용하기 위해서 둘중 하나를 사용하여 표현해야함. 

|**1**|**$ if test $varaible**|
|-|-|
|**2**|**$ if [ variable ]**|


### 1) Numeric comparisons
*perform a comparison of two numeric values

|Comparison| Description|
|-|-|
|n1 -eq n2 |Checks if n1 is equal to n2|
|n1 -ge n2| Checks if n1 is greater than or equal to n2|
|n1 -gt n2 |Checks if n1 is greater than n2|
|n1 -le n2 |Checks if n1 is less than or equal to n2|
|n1 -lt n2 |Checks if n1 is less than n2|
|n1 -ne n2 |Checks if n1 is not equal to n2|

<pre>
#!/bin/bash
value=10
if [ $value -gt 5 ] ; then
  echo "$value is grater than 5 "
fi
</pre>

<pre>
#!/bin/bash
value=10
if test $value -gt 5  ; then
  echo "$value is grater than 5 "
fi
</pre>
*#shell에서는 integers operation밖에 못하기 때문에 floating_point는 비교 불가.*

### 2) String comparisons
+ 문자열을 비교해 보자. 

|Comparison |Description|
|-|-|
|str1 = str2 |Checks if str1 is the same as string str2|
|str1 != str2 |Checks if str1 is not the same as str2|
|str1 < str2| Checks if str1 is less than str2|
|str1 > str2| Checks if str1 is greater than str2|
|-n str1 |Checks if str1 has a length greater than zero|
|-z str1 |Checks if str1 has a length of zero|


<pre>
#!/bin/bash
testuser=su980818
if[ $USER = $testuser ] ; then
  echo "welcom $testuser"
fi
</pre>

<pre>
#!/bin/bash
val1=a
va12=A
if[ $val \> $val2 ] ; then                        #  < , > redirection으로 인식됨으로 \을 추가해야함.  
  echo "$val1 is greater than $val2"              
fi
</pre>
*#string comparison에 경우 ASCII를 사용하여 (A=65 a=97) 대문자가 소문자보다 작다. (이와 다르게 sort에 경우는 일반적인 영어 순서를 따른다.)*

 <pre>
#!/bin/bash
val=""
if[ -z $val ] ; then                        
  echo "val is empty"          
fi
</pre>
*#항상 value값이 있는지 없는지 따지는건 오류를 줄이기 위해 중요함.*



### 3) Using file comparisons
+ test the status of file or directories

|Comparison| Description|
|-|-|
|-d file| Checks if file exists and is a directory|
|-e file| Checks if file exists|
|-f file| Checks if file exists and is a file|
|-r file |Checks if file exists and is readable|
|-s file |Checks if file exists and is not empty|
|-w file |Checks if file exists and is writable|
|-x file |Checks if file exists and is executable|
|-O file |Checks if file exists and is owned by the current user|
|-G file|Checks if file exists and the default group is the same as the current user|
|file1 -nt file2 | Checks if file1 is newer than file2|
|file1 -ot file2| Checks if file1 is older than file2|
*#-G에 경우 file이 current user의 그냥 그룹이 아닌 defalut group에 속하는지만을 알아낼수 있다.*
*#모든 comparison은 file이 존재하지 않는다면 fail을 return함으로 file exist를 먼저 확인하는게 좋다.*
*# script에서 파일을 지정할때는 절대 경로를 이용하는게 좋다. (script에서 pwd를 이용해보면 script가 있는 directory로 설정되 있음)*

<pre>
 #!/bin/bash
 #home에 a.txt file이 있는지 확인하고 없으면 생성
  file='a.txt'
  if [ -d $HOME ] ; then
          echo $HOME is directory
          if [ -f $HOME/$file ] ; then
                  echo $file is file
         else
                echo $file is not file or exit
                touch a.txt
          fi
  else
          echo $HOME is not directory or exit
  fi
</pre>

