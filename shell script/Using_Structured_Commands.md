1.Working with the if-then Statement
------
**조건문이 command의 exit status에 의해 조작됨**

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
<span style="color:red">" if 문에 들어가는 조건문을 알아보자.(조건이 맞을시 exit value를 0로 return) "</span>

* variable에 값이 있는지 판단 하기 + comparisons의 기본 format으로 사용됨. 
<pre>
variable=""
if test $varaible
</pre>
<pre>
variable=""
if [ variable ]
</pre>

*둘다 값의 여부를 판단 , brackets에 경우 variable과 공백이 무조건 있어야함.*


### 1) Numeric comparisons
* perform a comparison of two numeric values

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
*shell에서는 integers operation밖에 못하기 때문에 floating_point는 비교 불가.*

### 2) String comparisons
|Comparison |Description|
|-|-|
|str1 = str2 |Checks if str1 is the same as string str2|
|str1 != str2 |Checks if str1 is not the same as str2|
|str1 < str2| Checks if str1 is less than str2|
|str1 > str2| Checks if str1 is greater than str2|
|-n str1 |Checks if str1 has a length greater than zero|
|-z str1 |Checks if str1 has a length of zero|

