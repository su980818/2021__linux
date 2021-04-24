# In this chapter
 
 
 1. Matching a Unicode Character 
 2. Using vim 
 3. Matching Characters with Octal Numbers 
 4. Matching Unicode Character Properties 
 5. Matching Control Characters 
 
 
 
### 들어가기 전에 
--------
#### [a. Unicode 란?]()

ASCII( American Standard Code for Information Interchange) : 영어 문자를 표현하기 위한 code로  1Byte ( 실제 사용은 7bit ) 의 code로 문자를 표현

국가마다 독자적으로 ASCII (00000000 - 01111111) 이외에 부분 ( 11111111 - 10000000 )혹은 1byte를 더해 더 넓은 범위를 자국의 문자를 표현하기 위해 사용했는데 이로 인해 문자의 code가 서로 중복되어 
문자를 다른나라에서 encoding시 설정 값이 달라서 글자가 깨지는 현상이 발생 .  

Unicode : 위의 문제를 해결하기위해 3Byte를 이용하여 모든 문자를 포함하도록 국제 표준으로 설계된 문자 체계

###### < Unicode table >

|평면 블록| 시작 블록| 끝 블록 |크기 블록| 이름 |UTF-8 바이트 수|
|-|-|-|-|-|-|
|BMP| U+0000| U+007F |128자 |Basic Latin |1 |
||U+1100 |U+11FF |256자 |한글 자음 모음 |3|
||U+3040 |U+309F |96자 |Hiragana||
||U+AC00(가) |U+D7AF(힣)| 11184자 |한글 소리 마디| |
###### # 한글 소리마디는 초성 * 중성 * 종성 = 1,638,750개가 필요하지만  실제 필요한 소리마디는 11172자 고 그중에서 실제로 사용되는것은 2~3천개 라고 한다. 

#### [b. 한글 자모음을 소리마디로 변환하는 방법.]() 
U+AC00 + ((초성 값 x 21) + 중성 값) x 28 + 종성 값 = 소리마디 포인트 값

> ex) ㅎ(18) ㅏ(0)  ㄴ(4) 
>
> -> U+AC00 + ((18 x 21) + 0) x 28 + 4 == (한) U+D55C 


#### [c. Unicode incoding 중 하나인 UTF-8이란 ?]()
가장 많이 쓰이는 incoding 방법으로 가변길이를 사용하여 유니코드를 나타낸다. 

1byte를 사용하여 나타낼수 있는 아스키의 경우 4byte를 모두 사용하여 문자를 나타내면 앞의 byte는 쓰래기 값으로 공간만 차지함으로 이를 위해 가변길이를 사용하는 UTF-8이 표준 인코딩 방식으로 자리잡음. 


1) 7bit이내의 코드값 : 0xxxxxxx 
2) 8bit이상 11bit 이하의 코드값 : 110xxxxx 10xxxxxx
3) 12bit이상 16bit 이하의 코드값 : 1110xxxx 10xxxxxx 10xxxxxx
###### # x로 표시된 부분에 원래의 unicode를 표시한다. 


가변길이기 때문에 맨앞의 msb를 통해 몇 byte가 필요한지를 나타낸다. 
+ msb 0 : 뒤에 추가적인 byte가 없음
+ msb 1 : 뒤에 추가적인 byte가 존재 + msb부터 다음 0가 나오기 까지 나오는 1의 갯수가 추가적인 byte의 갯수를 표시 
+ msb 10 : 독립적인 문자가아닌 추가적인 후속 byte임을 표시 


# 1. Matching a Unicode Character 
unicode 값 ( unicode point ) 값을 이용하여 unicode character 을 match할 수 있음. 

>\u00e9
>
>\x{00e9}

#hexadecimal value 를 사용



# 2. Using vim
vim 내부에서 unicode pointer의 사용법

> \%u6c60

###### < 찾기 ( / )  를 이용하여 유니코드 문자 찾기 >
<pre>
古池
蛙飛び込む
水の音
	—芭蕉 (1644–1694)
 
 /\%u6c60
</pre>

# 3. Matching Unicode Character Properties (in Perl)

In some implementations, such as Perl, you can match on Unicode character properties. The properties include characteristics like whether the character is a letter, number, or punctuation mark.

> **ack** *'character'*

A command-line tool written in Perl that acts like grep

**matching property**

> \p{property}

|property|Description|
|-|-|
| \pL |  Letter|
| \p{Lu} | uppercase letter |
| \p{Lu} | lowercase letter |
| \PL | uppercase p do not match a Letter |

###### *# upperacase do not match a property#



# 4. Matching Control Characters (in Perl)
> **\c***x*

x is control character you want to match

<pre>
$ ack '\c@' ascii.txt
0. Null
$ ack '\0' ascii.txt
0. Null
</pre>

<pre>
$ cat  ascii.txt | ack '\c['
27. Escape
$ cat  ascii.txt | ack '\e'
27. Escape
</pre>

<pre>
$ cat ascii.txt | ack '\cH'
8. Backspace
$ cat ascii.txt | ack '[\b]'
8. Backspace
</pre>
