# Basic Script Building

; (semicolon) chain commands together into a single step
#(pound sign) is used as a comment line 

Creating a Script File
---------

#!/bin/bash
*첫번째줄에 사용되는 #! 는 일반적인 경우와 달리 사용되는shell script를 표시한다.*


shell script실행하기
다른 command의 경우 file 이름만 입력하면 실행이 되는데 이는 입력된 file의 경로를 shell이 자동으로 찾아주기 때문에 가능하다. 
그럼으로 실행하기 위해서는 $PATH에 shell script 경로를 설정하기 

혹은 경로를 수동으로 입력해 사용한다. 
