# In This Chapter
#### [ Various control methods include sending signals to your script, modifying a script’s priority, and switching the run mode while a script is running. This chapter examines the different ways you can control your shell scripts.]()

1. Handling signals
2. Running scripts in the background
3. Forbidding hang-ups
4. Controlling a Job
5. Modifying script priority
6. Automating script execution




# 1. Handling signals     [trap]()
#### [script 안에서 signal에 따른user_defiend_operation 을 설정해 보자]()

##### ( Table 16.1 Linux Signals )
|Signal| Value| Description|
|-|-|-|
|1| SIGHUP| Hangs up the process|
|2| SIGINT |Interrupts the process|
|3| SIGQUIT |Stops the process|
|9 |SIGKILL| Unconditionally terminates the process|
|15| SIGTERM| Terminates the process if possible|
|17 |SIGSTOP| Unconditionally stops, but doesn’t terminate, the process|
|18| SIGTSTP| Stops or pauses the process, but doesn’t terminate|
|19 |SIGCONT| Continues a stopped process|

*# Ctrl + C : 2 SIGINT*

*# Ctrl + Z : 18 SIGSTOP*




> **trap** *commands  signals*
<pre> #!/bin/bash

trap      “echo ‘ Sorry! I have trapped Ctrl-C”’            SIGINT

count=1
while [ $count -le 10 ]
do
echo “Loop : $count”
sleep 1
count=$[ $count + 1 ]
done
</pre>

*# trap이 설정되지 않았으면 defalut 로 설정된 작업을 수행*
*# trap을 설정하면 shell 로 부터 signal을 받았을떼 수행할 작업을 선택할수 있음.* 


## 1) 일반적인 종료상황 
#### siganl자리에 EXIT를 사용하면 모든 종료 signal에 대하여 지정한 작업을 수행

<pre>
#!/bin/bash
trap      “echo ‘ script exit ”’           EXIT
</pre> 

## 2) trap 수정 or 삭제

<pre>
#!/bin/bash
trap       “echo ‘ Sorry! I have trapped Ctrl-C”’       SIGINT

section 1

trap      “echo ‘ i modified the trap ”’            SIGINT

section 2
</pre> 
*# 각 section마다 위에 있는 trap중 가장 가까운 trap에서 signal을 trap함

<pre>
#!/bin/bash
trap      “echo ‘ script exit ”’            SIGINT

section 1

trap      -          SIGINT

section 2
</pre> 
*# - 을 사용하여 삭제할수 있음*


# 2. Running scripts in the background    [$]()
> **command** & 
# 3. Forbidding hang-ups     [nohup]()
#### script 가 hang-up signal 을 무시하여 터미널이 종료되더라도 작업을 유지

**hangup signal ( signal num 1 )** : 로그아웃과 같이 터미널에서 접속이 끊겼을 때 보내지는 시그널 
command 의 출력이 STDOUT에서 자동으로 nohup.out 으로 redirect됨.

> $ **nohup** *command* & 


# 4. Controlling a Job  [bg fg jobs]()

> **bg** *1*  : job_# 1번을 bg로 실행
> 
> **fg** *1* : job_# 1번을 fg로 실행
> 
> **jobs** : current_user의 ps를 보여줌

<pre>
$ jobs 
[1]+ 200 stop
[2]-  201 running 
</pre> 
*# + : default process ( job # 없이 fg, bg등을 사용시 적용대상 )*

*# - : next default process  ( + ps 종료시 다음 default process )*

**<Table 16.2 The jobs Command Parameters>**
|Parameter |Description|
|-|-|
|-l| Lists the PID of the process along with the job number|
|-n |Lists only jobs that have changed their status since the last notification from the shell|
|-p |Lists only the PIDs of the jobs|
|-r| Lists only the running jobs|
|-s |Lists only stopped jobs|



# 5. Modifying script priority  [nice, renice]()
**priority** :  kernel이 ps 에 cpu를 할당해주는데 priority 를 보고 상대적인 cpu time 을 할당해줌
**nice** : user가 실제 priority 값을 조정하여 ps에 os 보다 높은 우선 순위를 주게 되는 경우와 같이 priority 값을 direct로 조정하는것은 위험함으로 priority값을 이렇게 should 해달라고 제안하는 값

range from –20(most favorable scheduling priority) to 19 (least favorable scheduling priority)

>**nice** **-n** *nie_#* *command*
>**renice** **-n** *nice_#* **-p** *pid*
<pre><code>
$ renice -n 10 $(pgrep sleep)
24 (process ID) old priority 0, new priority 10
$ ps -o user,nice,command
USER      NI COMMAND
seungwoo 10 sleep 100
</code></pre> 


# 6. Automating script execution [at crontab anacron]()
#### [ps예약 (at), 지속적인 ps예약 (crontab)을 지정해 보자.]()

## 1) at
### a) script 예약 실행 
>**$at   -f** *filename     time*
### b) command 예약 실행 
>$ at now +1 min
> at> updatedb
> at> <Ctrl+d> <EOT>

### #) 추가

|추가||
|-|-|
|$ atq|check the queue of at jobs that are set to run|
|$ atrm 11|Delete at job number 11|
|# service atd start|start atd|


## 2) batch
as soon as possible run the process
<pre>
$ batch 
at> find /mnt/isos | grep jpg$ > /tmp/mypics
at> <Ctrl+d> <EOT>
</pre> 


## 2) Crontap  
### a) user’s crontab 설정하기 
각 유저는 고유의 crontab 파일이 존재 하고 이를 조작하여 예약을 설정 

|crontab||
|-|-|
|$ crontab -e|edite a personal crontab file|
|$ crontab -l|List contents of your crontab file|
|$ crontab -r|Delete your crontab file|
| $ sudo service cron start| start cron|
\
**<crontab file 설정 방법>**
<pre>
min    hour   dayofmonth    month     dayofweek        command 
0-60   0 -24    1-31        1-12     0-6 or sun - sat
</pre>



### b) linux’s crontab 설정하기

**crontab folder 안에 script들이 주기적으로 실행됨**
<pre>
/etc/cron.daily/ 
/etc/cron.monthly/
/etc/cron.weekly/
/etc/cron.hourly/
</pre>


## 3) ancron
#### linux’s crontab folder 에 있는 script들이  system이 꺼저있어서 수행이 되지 않았다면  system이 켜젔을때 이를 확인하고 여유시간을 갖고 재실행 해주는 별도의 program

`$ sudo cat /var/spool/anacron/cron.*` : (timestamp file)  언제 crontab folder 의 script들이 실행 됬는지 기록해 놓은 file

`$ sudo cat /etc/anacrontab` : anacron setup file

<pre>
* period   delayinminutes    identifier   command
</pre>
