# In this chapter

ASCII( American Standard Code for Information Interchange) : 영어 문자를 표현하기 위한 code로  1Byte ( 실제 사용은 7bit ) 의 code로 문자를 표현

국가마다 독자적으로 ASCII (00000000 - 01111111) 이외에 부분 ( 11111111 - 10000000 )혹은 1byte를 더해 더 넓은 범위를 자국의 문자를 표현하기 위해 사용했는데 이로 인해 문자의 code가 서로 중복되고 
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







 1. Matching a Unicode Character 
 2. Using vim 
 3. Matching Characters with Octal Numbers 
 4. Matching Unicode Character Properties 
 5. Matching Control Characters 


# 1. Matching a Unicode Character 
# 2. Using vim 
# 3. Matching Characters with Octal Numbers 
# 4. Matching Unicode Character Properties 
# 5. Matching Control Characters 
