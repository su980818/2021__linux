# In this chapter
+ linux 는 하나의 컴퓨터를 여러명이 사용하는 Multi-user system.
+ root 유저와 일반 유저를 구분하여 os의 중요 기능 접근을 막아 os를 안전하게 사용. 
+  root 의 UID(user ID)  = 0 일반 유전의 UID >= 1000 

###### GUI로도 쉽게 USER정보를 접근할 수 있음. 
![image](https://user-images.githubusercontent.com/78835559/113229266-945ee800-92d1-11eb-85f8-5fb5899aeac0.png)


# 1.User Acounts
#### User acount를 관리해 보자. 
## 1) root 유저가 일반 유저를 관리하는 방법 

> [**useradd**]()

![image](https://user-images.githubusercontent.com/78835559/113229331-be180f00-92d1-11eb-85eb-6a64f058800a.png)
*# user acount의 경우 password expire이 존재함*

> [**usermod**]()

![image](https://user-images.githubusercontent.com/78835559/113229429-eef84400-92d1-11eb-87f5-a8f91d60d35e.png)
*# User LOCK UNLOCK의 경우 user 정보를 삭재하지 않고 접근만 막아놈*

> [**userdel**]()

![image](https://user-images.githubusercontent.com/78835559/113229941-efdda580-92d2-11eb-93d8-71cebf78377a.png)

**WARNING** _ userdel 사용시 user가 소유한 파일은 삭제 되지 않고 삭제된 user의 uid를 그대로 갖고 있다가 삭제된 uid와 같은 uid를 갖는 user가 생성되면 소유권이 넘어감

###### < 파일을 남겨놓고 user을 삭재한 경우 >
<pre>
-rw-r--r-- 1 1001 1001 0 Feb 19 10:56 HELLO
-rw-rw-r-- 1 1001 1001 0 Apr  1 10:19 jangs_data
</pre>
###### *# 소유자의 이름이 아닌 uid로 소유자가 지정되어 있음*


## 2) 일반 유저가 자신의 계정을 관리하는 방법 
![image](https://user-images.githubusercontent.com/78835559/113229826-b3aa4500-92d2-11eb-8169-60d728877c21.png)

# 2. Managin Passwords
> [**passwd**]()
![image](https://user-images.githubusercontent.com/78835559/113230551-31228500-92d4-11eb-87d0-3a8fb66d3fe9.png)
###### *# usermod -L 을 사용하여 LOCK 하는것과 동일한 작업*

![image](https://user-images.githubusercontent.com/78835559/113230588-48fa0900-92d4-11eb-8b09-a2191b5798d3.png)
###### *# x : 사용자 계정의 비밀번호 (암호화방식이면 x로 표시)*

###### < passwd expire 관리 >
![image](https://user-images.githubusercontent.com/78835559/113230664-78107a80-92d4-11eb-9d3e-3ed64f76868c.png)

> [**change**]()

passwd command보다 더 추가적인 기능 지원
![image](https://user-images.githubusercontent.com/78835559/113230736-9c6c5700-92d4-11eb-88ff-623521e077be.png)
*# -d 0 를 활용해서 passwd를 바로 만료 시킬수 있음*

# 3. Adding Groups
#### useradd , mod , del 과 동일


> [**groupadd**]()
![image](https://user-images.githubusercontent.com/78835559/113230843-db021180-92d4-11eb-89b3-30d5c6e20071.png)

> [**groupmod**]()
![image](https://user-images.githubusercontent.com/78835559/113230850-ddfd0200-92d4-11eb-8217-4964d81d97ba.png)

> [**groupdel**]()
![image](https://user-images.githubusercontent.com/78835559/113230863-e1908900-92d4-11eb-9b4b-54bb6d185984.png)

#### group 에 user추가 , gruop 에 속한 user보기  
![image](https://user-images.githubusercontent.com/78835559/113230909-0127b180-92d5-11eb-8310-2e6fd67f3f85.png)

![image](https://user-images.githubusercontent.com/78835559/113230923-097fec80-92d5-11eb-85d2-8aa2a66b1093.png)

# 4. Checking on Users
#### [user들의 로그인 log를 확인하자]()
> [**last , lastb , who , users**]()

![image](https://user-images.githubusercontent.com/78835559/113230986-2c120580-92d5-11eb-89fb-8445e3a1815c.png)


# 5. Configuring the Built-In Firewall
#### 방화벽이란?
+ FIREWALL: 컴퓨터 네트워크를 통하여 들어오거나 나가는 모든 패킷을 검사하여 패킷을 필터링 하는것 
+ iptable : 방화벽의 규칙을 명시하는 테이블 
+ Chain  : iptable의 규칙을 수행하는 유닛

<pre>
filter table  
①Chain INPUT - 서버로 들어오는 규칙을 수행
②Chain FORWARD - 서버에서 forarding 규칙을 수행
③Chain OUTPUT - 서버에서 나가는 규칙을 수행 
</pre>

> [**iptable**]()

![image](https://user-images.githubusercontent.com/78835559/113231166-97f46e00-92d5-11eb-8b5b-48953c95c875.png)
*REFECT 동작 DROP 동작 모두 접근을 차단하는것은 동일하지만 경고메시지를 띠우냐 안띠우냐의 차이*

<pre>
$ iptables -A INPUT -d 192.168.10.10 -p tcp –dport 22 -j DROP
## 외부 모든 출발지에서 내부 192.168.10.10 목적지 서버의 tcp/80 포트로의 접근을 차단
</pre>
