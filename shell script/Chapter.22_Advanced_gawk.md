# In This Chapter
#### [ produce formatted reports from raw data files]()

1. Reexamining gawk
2. Using Variables
3. Using Patterns
4. Structured Commands
5. Formatted Printing
6. Built-In Functions
7. User-Defined Functions
8. Working through a Practical Example
9. Summary


# 1. Reexamining gawk

#### [ sed와 유사하게 하나의 input에서 라인단위로 입력을 받아 각각의 라인을 지정한 fomat으로 처리해 주는 자동화 기능 제공]()
#### [ 단순 command로 동작하는 sed와 달리 사용환경을 하나의 gwak-language로 제공하기 때문에 (c-language와 유사) 여러가지 작업이 가능]()
#### [ 위의 특성으로 데이터 처리에 유용하게 사용됨]()

## 1) data의 구분


|fild(column)| 하나의 자료형 데이터를 저장하는 장소|
|-|-|
|**record(row)**| **다른 자료형에 속할수 있는 필드의 모임**|


|$0|represents the entire line of text.|
|-|-|
|**$1**|**represents the first data field in the line of text**|
|**$n**|**represents the nth data field in the line of text.**|

![image](https://user-images.githubusercontent.com/78835559/111578303-3de4aa80-87f7-11eb-8806-ef81ab025d09.png)


## 2) gawk-command format

#### [**gawk**   *options   program   file*]() 
<pre>
$ gawk ‘{print $1}’ linux.txt
Chap.1 
Chap.2  
Chap.3  
Chap.4 
</pre>
*# program part가 gawk-language 로 작성된 문자열임으로 ''이 필요*

## 3) gawk Options




|Option |Description|
|-|-|
|-F fs |Specifies a file separator for delineating data fields in a line|
|-f file| Specifies a file name to read the program from|
|-v var=value| Defines a variable and default value used in the gawk program|
|-mf N |Specifies the maximum number of fields to process in the data file|
|-mr N |Specifies the maximum record size in the data file|
|-W keyword| Specifies the compatibility mode or warning level for gawk|

### (a) **-f**  *file*
#### ‘progrem’ 부분이 길어질수 있음으로 별도의 파일로 gawk-language 를 작성하여 사용

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



### (b) **-F** *field separator* 
#### field가 default-separator(space or tab)가 아닌 다른 문자로 구분될 경우 사용
 
<pre>
$ gawk      -F:       ‘{print $1}’         /etc/passwd
root
daemon
bin
sys
</pre>


## 4) Using multiple commands in the program script


### (a) ;   
#### shell 에서 mutiple command를 사용하는 경우와 동일

<pre> 
$ gawk ‘{ command1   ; command2 }’ input-file
</pre>

### (b) in-line
#### shell 에서 in-line redirection을 사용하는 경우와 비슷
<pre>
$ gawk ‘{
>  command1
>  command2
>  }’ input-file
</pre>



## 5) Running scripts before processing data


#### [ script를 BEGIN, PATTERN, END section으로 나누어 실행하자. ]()

#### [ 각 sectino은 {}을 통해 구분됨]()
<pre>
$ gawk -F: 'BEGIN {print "HELLO"} {print $1, $2 } END{ print "BY"}' data
HELLO
root x
daemon x
...
BY
</pre>
PATTERN section : data를 record 기준으로 불러오고 처리하는 section  ( begin, end section은 date를 읽어들이지 않음 )


# 2. Using variables in gawk

#### [ gawk-languale는 shell commnad와 달리 $1 같은 field 를 나타내는 변수 이외에는 $를 쓰지 않고 사용 ( 햇갈림 ) ]()


## 1) Built-in variables

|Variable| Description|
|-|-|
|FIELDWIDTHS| A space-separated list of numbers defining the exact width (in spaces) of|
|each| data field|
|FS| Input field separator character|
|RS |Input record separator character|
|OFS |Output field separator character|
|ORS |Output record separator character|

### (a) FS,OFS
#### passwd(FS 가 : 인 파일)를 * 로 구분되게 변환 
<pre>
$ gawk '  BEGIN{FS=":"; OFS="*"}          {print $1,$2} ' data
root*x
daemon*x
bin*x
sys*x
</pre>

### (b) FIELDWIDTHS
#### gawk ignores the FS and calculates data fields based on the provided field width sizes
<pre>
$ cat data2
abc123
def789
$ gawk 'BEGIN{FIELDWIDTHS="3 3"} {print $1 "--" $2} ' data2
abc--123
def--789
</pre>
*# this method can not accommodate variable-length data fields.*


## #) Data의 record가  \n으로 구분되어 있는경우  

#### set the RS variable to an empty string, and leave a blank linebetween data 	records in the data stream

<pre>
$ cat data2
Riley Mullen
(312)555-1234

Frank Williams
(317)555-9876
$ gawk ‘BEGIN{FS=”\n”; RS=””} {print $1,$2}’ data2
Riley Mullen (312)555-1234
Frank Williams (317)555-9876
Haley Snell (313)555-4938
</pre>
*# The gawk program interprets each blank line as arecord separator.*

|Variable |Description|
|-|-|
|ARGC |The number of command line parameters present|
|ARGIND |The index in ARGV of the current file being p|rocessed|
|ARGV| An array of command line parameters||
|CONVFMT | The conversion format for numbe|rs (see the printf statement), with a default value of %.6 g|
|ENVIRON| An associative array of the curren|t shell environment variables and their values|
|ERRNO |The system error if an error occurs w|hen reading or closing input files|
|FILENAME |The filename of the data file used |for input to the gawk program|
|FNR| The current record number in the data fil|e|
|IGNORECASE |If set to a non-zero value, ignores| the case of characters in strings used in the gawk command|
|NF| The total number of data fields in the data |file|
|NR| The number of input records processed||
|OFMT| The output format for displaying num|bers, with a default of %.6 g|
|RLENGTH |The length of the substring matche|d in the match function|
|RSTART| The start index of the substring mat|ched in the match function|

[ **associative array** ]() : uses text for the array index values instead of numeric values.
<pre>
$ gawk 'BEGIN{  print ENVIRON["HOME"]    }'
</pre>

## #) FNR vs NR

FNR : value was reset when gawk processed the other data file.
NR :maintain its count into the other data file
     
## 2) User-difined variables  

### (a) Assigning variables in scripts 

#### Assigning values to variables in gawk programs is similar to doing so in a shell script, using an assignment statement

<pre>
$ gawk ‘
> BEGIN{
> testing=“This is a test”
> print testing
> testing=45
> print testing
> }’
This is a test
45
</pre>
*# gawk variables can hold either numeric or text values*

### (b) Assigning variables on the command line

<pre>
$ gawk -F: '{print $n}' n=1  /etc/passwd
root
daemon
...
</pre>
*# -v option을 사용하고 변수를 선언해야 BEGIN-section에서 사용가능*

### (c) Working with associative arrays

<pre>
$ gawk 'BEGIN{
var["a"] ="A"
var["b"] ="B"
for (test in var )
{
print  “index:”, test ," value:", var[test]
}}'

index: a value: A
index: b value: B
</pre>

*# var[index] 값이 아닌 index값이  test 에  저장됨*

*# for () 을 사용해야함!!*

#### (#) delete array[index] 




# 3. Using Patterns


## 1) Regular expressions 

#### [ 일치하는 expresson을 갖는 record 찾기]()
|/expression/{print $0}'|
|-|
<pre>
$ gawk -F: '/root/{print $0}' /etc/passwd
root:x:0:0:root:/root:/bin/bash
</pre>


## 2) The matching operator 

#### [ 원하는 field 에 일치하는 expresson을 갖는 record 찾기]()
|부분 일치 |‘$field_num ~ /expression/{print $0}' |‘$field_num !~ /expression/{print $0}'|
|-|-|-|
|**완전 일치**|**‘$field_num == “expression”{print $0}'** |**‘$field_num != “expression”{print $0}'** |

<pre>
$ gawk -F: '$5 ~/root/{print $0}' /etc/passwd
root:x:0:0:root:/root:/bin/bash
</pre>

## 3) Mathematical expressions  

#### [ mathematical 조건에 맞는 record 찾기]()

|$field_num  == y {print $0}|$field_num  != y {print $0}|
|-|-|
<pre>
$ gawk -F: '$3  <=10{print $0}' /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
</pre>
 
# 4. Structured Commands

### [c언어와 동일한 format 사용]()
<pre>
if (condition) { statement 1 } 
else { statement 2 } 
</pre>
<pre>
while (condition) { statements } 
</pre>
<pre>
for( variable assignment; condition; iteration process)
</pre>

# 5. Formatted Printing

#### **printf** *“format string“, var1, var2*

<pre><cod>$ gawk '{ printf "%s  \n",$0 }' </code></pre>

# 6. Built-In Functions

## 1) Mathematical functions



## 2) String functions 



## 3) Time functions



7.User-Defined Functions
---
#### [ 일반적으로 BEGIN section 위에다가 선언]()

**function name (variables)  { statements }**

<pre>
$ gawk '
function myprint(variable){
        print variable
}
BEGIN{
        myprint(20)
}'
</pre>


### #) body/pattern/end section 으로 구성된 script 와 user_difiend_funtion 으로 구성된 libarary 를 따로따로 작성해서 합칠수 있음

<pre>
$ cat library
function myprint()
{
printf “%-16s - %s\n”, $1, $4
}
$ gawk -f library -f script data2
</pre>


8.Working through a Practical Example
---

team 1에 속하는 record의 필드 3,4,5 값을 모두 더해 6으로 나눈값 과 team2의 값을 구하는 script
<pre>
Rich Blum,team1,100,115,95
Barbara Blum,team1,110,115,100
Christine Bresnahan,team2,120,115,118
Tim Bresnahan,team2,125,112,116
</pre>

<pre>
#!/bin/bash
for team in $(gawk –F, ‘{print $2}’ scores.txt | uniq)
do
 gawk –v team=$team ‘

 BEGIN{
  FS=”,”
  total=0
 }

 {
  if ($2==team)
  {
   total += $3 + $4 + $5;
  }
 }

 END {
  avg = total / 6;
  print “Total for”, team, “is”, total, “,the average is”,avg
  }’ scores.txt
done
</pre>
