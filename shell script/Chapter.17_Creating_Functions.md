# In This Chapter

1. Basic script functions
2. Returning a value
3. Using variables in functions
4. Array and variable functions
5. Function recursion
6. Creating a library
7. Using functions on the command line



# 1. Basic script functions
#### [This section describes how to create and use functions in your shell scripts.]()

## 1) Creating a function
#### There are two formats


> **function** *name* {
> *commands*
> }



> **name()** {
> *commands*
> }

## 2) Using functions

> *fuc_name*

just specify the name

**NOTICE**  _The function definition doesn’t have to be the first thing in your shell script, but be
careful. If you attempt to use a function before it’s defined, you’ll get an error message:


# 2. Returning a value
#### [The bash shell treats functions like mini-scripts, complete with an exit status (seeChapter11). ]()

#### There are three different ways you can generate an exit status for your functions.

## 1) The default exit status

By default, the exit status of a function is the exit status returned by the last command in the function

[So that you have no way of knowing if any of the other commands in the function completed successfully or not.]()

**<exit 값 예시>**
<pre>
#!/bin/bash
func1() {
ls -l badfile
echo “This was a test of a bad command”
}

func1
echo “The exit status is: $?”
</pre>
*# [$?]() exit 값을 참조할수 있는 변수*

## 2) Using the return command
#### exit a function with a specific exit status.
> **return** *#*

## 3) Using function output
#### [Just as you can capture the output of a command to a shell variable, you can also capture the output of a function to a shell variable.]()

**<echo 를 이용한 계산값 전달 예시>**
<pre>
#!/bin/bash
function dbl {
read -p “Enter a value: ” value
echo $[ $value * 2 ]
}
result=$(dbl)
</pre>
*# 단순하게 $() 을 이용하여 script 의 output을 변수에 redirection 해주자.*

# 3. Using variables in functions
# 4. Array and variable functions
# 5. Function recursion
# 6. Creating a library
# 7. Using functions on the command line
