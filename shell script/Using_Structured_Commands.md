1.Working with the if-then Statement
------
**조건문이 command의 exit status에 의해 조작됨**

* If the exit status of the command is zero , command list under the then section are executed.

<pre>
if command
then 
  commands
fi
</pre>
or
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
* if 문에 들어가는 조건문을 알아보자. 

variable에 값이 있는지 판단 하기 
<pre>
variable=""
if test $varaible
if [ variable ]
</pre>
*둘다 값의 여부를 판단 , brackets에 경우 variable과 공백이 무조건 있어야함. *

1) Numeric comparisons
