# In This Chapter


1. Automating backups
2. Managing user accounts
3. Watching disk space



# 1. Automating backups
#### [This section shows you how to create an automated shell script that can take snapshots of specified directories and keep an archive of your data’s past versions.]()
### a. Obtaining archive
<pre>
$ tar -cf archive.tar /home/seungwoo/project/*  2>/dev/null
## 공간 절약을 위해 zip으로 , 확장자를 써서 파일 형태를 표시하는게 좋음
$ tar -zcf archive.tar.gz /home/seungwoo/project/*.* 2>/dev/null
</pre>

#### 하나의 폴더만 backup하는게 아닌 여러 군대의 file을 backup하고 싶다면? [USE configuration file!]()
<pre>
$ cat Files_to_backup
/home/seungwoo/Project
/home/seungwoo/NULLFILE
/home/seungwoo/Downloads
</pre>

#### for 문을 통해 압축하고 싶은 file 들을 불러오고 이 과정에서 file이 있는지 없는지 확인해줘야함
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



# 2. Managing user accounts

# 3. Watching disk space
