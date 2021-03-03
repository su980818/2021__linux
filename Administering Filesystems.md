# Administering Filesystems

파일 시스템(file system)은 컴퓨터에서 파일이나 자료를 쉽게 발견 및 접근할 수 있도록 보관 또는 조직하는 체제를 가리키는 말이다.

구조 : 파일 시스템은 일반적으로 크기가 일정한 블록들의 배열(섹터라고도 불리며 통상 512바이트, 1키비바이트, 2키비바이트같은 - 2를 제곱한 수만큼의 크기를 갖는다)에 접근할 수 있는 자료 보관 장치 위에 생성되어 이러한 배열들을 조직함으로 파일이나 디렉터리를 만들며 어느 부분이 파일이고 어느 부분이 공백인지를 구분하기 위하여 각 배열에 표시를 해 둔다

----
파티션 : 하나의 물리적인 드라이브( ssd , 하드디스크 )를 논리적으로 여러 부분으로 분할하는 것.

리눅스를 설치한 드라이브는 default 로 3가지의 파티션으로 분할 되어 있음. 

|제목|내용|
|-----------------|---|
|1. Boot partition |부팅을 위한 file (such as the kernel, initrd, and boot loader GRUB) 들을 저장하기 위한 공간 . linux 안에서는 /boot/ 로 마운트 되어있음.  |
|2. system partion |operating system file, 사용자가 사용하는 file 들을 저장하는 공간 . linux 에서 root 로 마운트 되어 있는 공간. |
|3. swap partition |memory 에서 swap을 위한 여유공간을 미리 구해놓기 위한 partiton  |

* partition 은 파일관리를 쉽게 하기위해 구분해서 분할한 것으로 그냥 드라이브 하나에 모든 file 을 저장해도 상관 없음.  


-------

fdisk
--------
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

