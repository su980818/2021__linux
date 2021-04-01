# In This Chapter


1. Automating backups
2. Managing user accounts
3. Watching disk space



# 1. Automating backups
#### [This section shows you how to create an automated shell script that can take snapshots of specified directories and keep an archive of your data’s past versions.]()
## Obtaining archive
<pre>
$ tar -cf archive.tar /home/seungwoo/project/*  2>/dev/null
## 공간 절약을 위해 zip으로 , 확장자를 써서 파일 형태를 표시하는게 좋음
$ tar -zcf archive.tar.gz /home/seungwoo/project/*.* 2>/dev/null
</pre>

#### 1. 하나의 폴더만 backup하는게 아닌 여러 군대의 file을 backup하고 싶다면? [USE configuration file!]()
<pre>
$ cat Files_to_backup
/home/seungwoo/Project
/home/seungwoo/NULLFILE
/home/seungwoo/Downloads
</pre>

#### 2. for 문을 통해 압축하고 싶은 file 들을 불러오고 이 과정에서 file이 있는지 없는지 확인해줘야함
<pre>
#!/bin/bash

for file_name in $(cat Files_to_backup)
do
        ## 파일이 or 폴더가 존재하냐?
        if [ -f $file_name -o -d $file_name ] ; then 
                file_sum="$file_sum $file_name"
        else
                echo "$file_name is not exit, i dont include it "
        fi
done
</pre>

## [create an hierarchy archive]()

#### 1. archive 를 저장하는 폴더를 만들자. 
<pre>
##  /archive접근 그룹을 따로 만들어 놓자.  
$ sudo mkdir /archive
$ ls -ld /archive
drwxr-xr-x 1 root root 4096 Apr  1 12:28 /archive
$ sudo chgrp archive /archive/
</pre>

#### 2. script
<pre>
#!/bin/bash
config_file=/archive/Files_to_backup

day=$(date +%d)
month=$(date +%m)
time=$(date +%k%M)
directory="/archive/$month/$day"
mkdir -p $directory
destination=$directory/archive$time.tar.gz

for file_name in $(cat $config_file)
do
        if [ -f $file_name -o -d $file_name ] ; then ## 파일이 or 폴더가 존재하냐?
                file_sum="$file_sum $file_name"
        else
                echo "$file_name is not exit, i dont include it "
        fi
done

tar -zcvf $destination $file_sum 2>/dev/null
</pre>

# 2. Managing user accounts
#### user dell 은 많은 과정을 필요로 함으로 이를 script로 실행하자

1. Obtain the correct user account name to delete.
2. Kill any processes currently running on the system that belongs to that account.
3. Determine all files on the system belonging to the account.
4. Remove the user account.




## 1. Obtain the correct user account name to delete.
<pre>
#!/bin/bash

echo -n "Unser name you want to delte :"
read -t 60 user_name
grep -w $user_name /etc/passwd > /dev/null

if [ $? -eq 0 ]; then
        echo "$user_name name is founded"
else

        echo "sorry  $user_name is not exit"
fi
</pre>


## 2. Kill any processes currently running on the system that belongs to that account.
~~xargs 를 사용~~ 

## 3. Determine all files on the system belonging to the account.
<pre>
$ find / -user $user_name
</pre>
## 4. Remove the user account.



<pre>
if [ $user_name = "seungwoo" ] ; then
        echo "seungwoo is main user"
        exit 1
fi

grep -w $user_name /etc/passwd > /dev/null

if [ $? -eq 0 ]; then
        echo "$user_name name is founded"

        ps -u $user_name --no-heading > /dev/null
        if [ $? -eq 0 ] ; then
                echo " ther is $user_name \'s prcoess running"
        else
                read -p "Do you really want to delete $user_name ?[YES/NO] :" answer
                if [[ $answer == [Yy][Ee][Ss] ]] ; then
                        Date=$(date +%m%d)
                        tar -zcf "/archive/user/$user_name$Date.tar.gz" /home/$user_name
                        sudo userdel -r $user_name
                        echo DELETE COMPLITE
                fi
        fi
else

        echo "sorry  $user_name is not exit"
fi
</pre>

# 3. Watching disk space
