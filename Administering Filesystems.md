# Administering Filesystems

파일 시스템(file system)은 컴퓨터에서 파일이나 자료를 쉽게 발견 및 접근할 수 있도록 보관 또는 조직하는 체제를 가리키는 말이다.

구조 : 파일 시스템은 일반적으로 크기가 일정한 블록들의 배열(섹터라고도 불리며 통상 512바이트, 1키비바이트, 2키비바이트같은 - 2를 제곱한 수만큼의 크기를 갖는다)에 접근할 수 있는 자료 보관 장치 위에 생성되어 이러한 배열들을 조직함으로 파일이나 디렉터리를 만들며 어느 부분이 파일이고 어느 부분이 공백인지를 구분하기 위하여 각 배열에 표시를 해 둔다

Partiion
------------
하나의 물리적인 드라이브( ssd , 하드디스크 )를 논리적으로 여러 부분으로 분할하는 것.

리눅스를 설치한 드라이브는 default 로 3가지의 파티션으로 분할 되어 있음. 

|제목|내용|
|-----------------|---|
|1. Boot partition |부팅을 위한 file (such as the kernel, initrd, and boot loader GRUB) 들을 저장하기 위한 공간 . linux 안에서는 /boot/ 로 마운트 되어있음.  |
|2. system partion |operating system file, 사용자가 사용하는 file 들을 저장하는 공간 . linux 에서 root 로 마운트 되어 있는 공간. |
|3. swap partition |memory 에서 swap을 위한 여유공간을 미리 구해놓기 위한 partiton  |

*\*partition 은 파일관리를 쉽게 하기위해 구분해서 분할한 것으로 그냥 드라이브 하나에 모든 file 을 저장해도 상관 없음.*




1.Changing Disk Partitions with fdisk
-------------
<pre>
$ sudo fdisk -l List disk partitions for every disk
Disk /dev/sda: 82.3 GB, 82348277760 bytes
255 heads, 63 sectors/track, 10011 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes

 Device Boot Start End Blocks Id System
/dev/sda1 * 1 13 104391 83 Linux
/dev/sda2 14 9881 79264710 83 Linux
/dev/sda3 9882 10011 1044225 82 Linux swap
</pre>
sda 라는 하나의 디스크에 1 , 2 , 3 의 파티션으로 구분해서 보여주고 boot , system , swap 파티션을 보여준다.

실습을 위해 usb를 희생하자.
<pre>
sudo fdisk /dev/sdb
</pre>
*\*sdb 의 file system 을 관리하는 문답형식의 command ( m을 눌러서 manual을 참고하자 )*

*\*설정을 하고 w를 눌러야만 적용이 완료됨*




2.Changing Disk Partitions with parted
-----
*\*fdisk와 같이 partion을 관리하지만 유용한 기능이 추가된 command*

|commnad||
|--|--|
|$ sudo parted /dev/sda print | $fdisk -l |
|$ sudo parted /dev/sdc | fdisk /dev/sdc |

**Warning** Unlike fdisk, parted immediately incorporates changes you make
to your partitions, without explicitly writing the changes to disk.




3.Working with Filesystem Labels
---
|label|disk 나 partiton (sda, sdb, sda1 ..)에 이름을 지정하여 사용성을 높임 |
|--|--|
|1.disk label| can be used as another name for a partition table, as seen in parted output. |
|2.partition| label can also be the name of an individual partition that contains an ext filesystem.|

|commnad||
|--|--|
|$ sudo e2label /dev/sda2 | To see a partition’s label (if it has one)|
|$ sudo e2label /dev/sda2 mypartition | To set the label on a partition:|
|/etc/fstab  |  be set up to use the partition label to mount the partition |
|$ sudo findfs LABEL=mypartition | To find a partition when you know only the label|




4.Copying Partition Tables with sfdisk
----
partition table 을 백업 복구하는 방법
|commnad||
|--|--|
|$ sudo sfdisk –d /dev/sda > sda-table |Back up partition table to file|
|$ sudo sfdisk /dev/sda < sda-table| Restore partition table from file|
|$ sudo sfdisk –d /dev/sda \| sfdisk /dev/sdb |Copy part table from a to b|





5.Creating a Filesystem on a Disk Partition
----
각 partion 에 filesystem 을 지정해주자. 
|commnad||
|--|--|
|$ sudo mkfs -t ext4 /dev/sdb1 |Create ext4 file system on sba1|
|$ sudo mkfs -t ext4 -v -c /dev/sdb1 |More verbose/scan for bad blocks|
|$ sudo mkfs|.ext4 -c /dev/sdb1| Same result as previous command|
|$ sudo mkfs.ext4 -c -L mypartition /dev/sdb1 | Add mypartition label|




$ mount
----



<pre>
$ mount 
proc on /proc type proc (rw,noexec,nosuid,nodev)
/dev/mapper/abc-root on / type ext4 (rw,errors=remount-ro)
/dev/sda1 on /boot type ext2 (rw)
192.1.0.9:/volume1/books on /mnt/books type nfs (rw,addr=192.1.1.9)
/dev/sdb1 on /media/myusb type ext4 (rw,nosuid,nodev,uhelper=udisks)
</pre>
*\*derive , 마운트된 folder , file system을 보여준다.*

<pre>

</pre>



----
virtual box 에 경우 usb를 꽃고 
![화면 캡처 2021-03-03 110002](https://user-images.githubusercontent.com/78835559/109741041-a5073a00-7c0f-11eb-80bc-58e91d43e3ee.png)

설정창-> usb -> 오른쪽 +모양 펜을 클릭해서 usb장치를 인식 시켜 주자. 

