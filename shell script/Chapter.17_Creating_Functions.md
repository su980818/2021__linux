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

**NOTICE** *_The function definition doesn’t have to be the first thing in your shell script, but be careful. If you attempt to use a function before it’s defined, you’ll get an error message:*


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
#### This section goes over a few techniques for handling variables both inside and outside your shell script functions.
## 1) Passing parameters to a function
#### [the bash shell treats functions just like mini-scripts. This means that you can pass parameters to a function just like a regular script]()
> **fuc_name** *parameter.1 parameter.2 ....*

**NOTICE** *_fuc 과 fuc 을 실행하는 script는 별개의 script임으로 $1 과 같은 parameter 변수는 공유되지 않음*


## 2) Handling variables in a function
#### Functions use two types of variables
**a. Global**

: are valid anywhere within the shell script
By default, any variables you define in the script are global variables. Variables defined
outside of a function can be accessed within the function just fine:

**b. Local**

: The local keyword ensures that the variable is limited to only within the function. If a
variable with the same name appears outside the function in the script, the shell keeps the
two variable values separate.

> **local** *var*





# 4. Array and variable functions

## 1) Passing arrays to functions
#### The art of passing an array variable to a script function can be confusing.


**<변수 명을 이용해 전달>**
<pre>
#!/bin/bash
array=(1 2 3 4 5)
echo ${array[*]}
echo ${array}
</pre>
*# array[*]와 다르게 array만 입력하면 array[0]이 출력되는걸 볼수 있음*

**SOLUTION)**_ To solve this problem, you must disassemble the array variable into its individual values
and use the values as function parameters. 

**<분해후 $@을 이용해 조립>**
<pre>
#!/bin/bash
function testit {
local newarray=$(echo $@)
echo ${newarray[*]}
}
array=(1 2 3 4 5)
testit ${array[*]}
</pre>


## 2) Returning arrays from functions

**<echo를 통한 output전달 이용( 2. 3) 확인 )>**
<pre>
#!/bin/bash
function testit {
newarray=(1 2 3 4 5)
echo ${newarray[*]}
}
array=$(testit)
echo ${array[*]}
</pre>


# 5. Function recursion

**<factorial을 이용한 예시>**
<pre>
function factorial {
if [ $1 -eq 1 ]
then
echo 1
else
local temp=$[ $1 - 1 ]
local result=‘factorial $temp’
echo $[ $result * $1 ]
fi
}
</pre>
*# local 을 이용하여 변수를 지정해야 실수를 방지할수 있음*

 


# 6. Creating a library
The first step in the process is to create a common library file that contains the functions you need in your scripts.

<pre>
# my script functions
function addem {
echo $[ $1 + $2 ]
}
function multem {
echo $[ $1 * $2 ]
}
</pre>

The next step is to include the myfuncs library file in your script files that want to use any
of the functions.

<pre>
#!/bin/bash
./myfuncs
addem 10 20
</pre>

#### [BUT If you try to just run the library file as a regular script file, the functions don’t appear in your script:]()

#### [The key to using function libraries is the source command.]()
The source command executes commands within the current shell context instead of creating a new shell to execute them.
The source command has a shortcut alias, called the dot operator.
> .  root/myfuncs



# 7. Using functions on the command line

#### function을 command line에서 바로 사용하는 방법
#### [PROS : script와 달리 , you can use it from any directory on the system; you don’t have to worry about a script being in your PATH environment variable.]()



## 1) Creating functions on the command line

**< define a function directly on the command line >**
<pre>
$ function divem { echo $[ $1 / $2 ]; }
</pre>

**< Defining functions in the .bashrc file >**
<pre>
cat .bashrc
# .bashrc
. /home/rich/libraries/myfuncs
</pre>
*# dot command를 사용해야 command라인이 있는 bash에서 사용할수 있음*




