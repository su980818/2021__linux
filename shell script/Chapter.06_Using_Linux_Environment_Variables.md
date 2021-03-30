# In This Chapter

programs and scripts use environment variables to obtain system information and
store temporary data and configuration information.

1. Looking at environment variables
2. Creating your own local variables
3. Removing variables
4. Exploring default shell environment variables
5. Setting the PATH environment variable
6. Locating environment files
7. Using variable arrays








# 1. Looking at environment variables

Two type environment variable
#### A. Global environment variables
are visible from the shell session and from any spawned child subshells. 

<pre>
$ printenv
SHELL=/bin/bash
WSL_DISTRO_NAME=Ubuntu-20.04
PWD=/home/seungwoo
LOGNAME=seungwoo
</pre>
*# The system environment variables almost always use all capital letters to differentiate them from normal user environment variables.*


#### B. Local  environment variables 
are available only in the shell that creates them

<pre>
$ set
BASH=/bin/bash[…]
[…]
colors=/etc/DIR_COLORS
my_variable=‘Hello World’
[…]
$
</pre>
*# local env + Global env  + user defiend variable 모두 등장*
# 2. Creating your own local variables
> my_variable=Hello

#### After you set a local variable, it’s available for use anywhere within your shell process. However, if you spawn another shell, it’s not available in the child shell:




# 3. Removing variables
# 4. Exploring default shell environment variables
# 5. Setting the PATH environment variable
# 6. Locating environment files
# 7. Using variable arrays

