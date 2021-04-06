# In this chapter

#### Regular expressions are all about matching and finding patterns in text, from simple patterns to the very complex

you can match patterns using

+ String literals
+ Digits
+ Letters
+ Characters of any kind


# 2. Digits

## 1) matche all  the Arabic digits


> [**\d**]()
shorthand of Digits 



> [**[0-9]**]()
character classes and range 


## 2) Matching Non-Digits
> [**\D**]()  

> [**[^0-9]**]() 
^ is  "match all but these"

# 3. Letters

> [**\w**]() is match only letters and numbers

>  [**[a-zA-Z0-9]**]() 

> [**\W**]() is negiate of /w


