1.Working with the if-then Statement
------
조건문이 command의 exit status에 의해 

*If the exit status of the command is zero , command list under the then section are executed.

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


*If the exit status of the command is non-zero , command list under the else section are executed.
<pre>
if command  ; then
  commands
else
  commands
fi
</pre>

*else if 
<pre>
if command  ; then
  commands
elif command ; then
  commands
else
  commands
fi
</pre>
