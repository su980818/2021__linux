# In This Chapter
### [ produce formatted reports from raw data files]()

1. Reexamining gawk
2. Using variables in gawk
3. Using structured commands
4. Formatting your printing
5. Working with functions


1.Reexamining gawk
---
### [- sed와 유사하게 하나의 input에서 라인단위로 입력을 받아 각각의 라인을 지정한 fomat으로 처리해 주는 자동화 기능 제공]()
### [- 단순 command로 동작하는 sed와 달리 사용환경을 하나의 gwak-language로 제공하기 때문에 (c-language와 유사) 여러가지 작업이 가능]()
### [- 위의 특성으로 데이터 처리에 유용하게 사용됨]()

### 1) data의 구분

|fild(column)| 하나의 자료형 데이터를 저장하는 장소|
|-|-|
|**record(row)**| **다른 자료형에 속할수 있는 필드의 모임**|

![image](https://user-images.githubusercontent.com/78835559/111578303-3de4aa80-87f7-11eb-8806-ef81ab025d09.png)

|$0|represents the entire line of text.|
|-|-|
|**$1**|**represents the first data field in the line of text**|
|**$n**|**represents the nth data field in the line of text.**|

### 2) gawk-command format
**gawk**   *options   program   file* : program part가 gawk-language 로 작성된 문자열임으로 ''이 필요
<pre>
$ gawk ‘{print $1}’ linux.txt
Chap.1 
Chap.2  
Chap.3  
Chap.4 
</pre>


### 3) gawk Options




|Option |Description|
|-|-|
|-F fs |Specifies a file separator for delineating data fields in a line|
|-f file| Specifies a file name to read the program from|
|-v var=value| Defines a variable and default value used in the gawk program|
|-mf N |Specifies the maximum number of fields to process in the data file|
|-mr N |Specifies the maximum record size in the data file|
|-W keyword| Specifies the compatibility mode or warning level for gawk|

----
-f file : ‘progrem’ 부분이 길어질수 있음으로 별도의 파일로 gawk-language 를 작성하여 사용
<pre>
$cat gawk.txt
 {print $1}
 </pre>
 
 <pre>
 $ gawk   -f gawk.txt    linux.txt
Chap.1 
Chap.2  
...
</pre>

----
 -F field separator : field가 default-separator(space or tab)가 아닌 다른 문자로 구분될 경우 사용
 
 <pre>
$ gawk      -F:       ‘{print $1}’         /etc/passwd
root
daemon
bin
sys
</pre>



2.Using variables in gawk
---

3.Using structured commands
---

4.Formatting your printing

---
5.Working with functions
----
