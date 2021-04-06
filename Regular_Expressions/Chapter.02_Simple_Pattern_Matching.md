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

# 4. Characters of any kind


> [**\W**]() is negiate of /w

> [**[^a-zA-Z0-9]**]() 

###### < Character shorthands > 
|Character Shorthand | Description|
|-|-|
|\a |Alert|
|\b |Word boundary|
|[\b] |Backspace character|
|\B |Non-word boundary|
|\c x| Control character|
|\d |Digit character|
|\D |Non-digit character|
|\d |xxx Decimal value for a character|
|\f |Form feed character|
|\r |Carriage return|
|\n| Newline character|
|pass:[<literal>\o</literal><replaceable>\xxx</replaceable>] |Octal value for a character|
|\s |Space character|
|\S |Non-space character|
|\t |Horizontal tab character|
|\v |Vertical tab character|
|\w |Word character|
|\W |Non-word character|
|\0 |Nul character|
|\ xxx |Hexadecimal value for a character|
|\u xxxx |Unicode value for a character|

> [**\s**]()
match whitespace ( space , tab , new line , carriage returns )
> [**[ \t\n\r]**]()


###### < Character shorthands for whitespace characters > 

|Character Shorthand Description|
|\f |Form feed|
|\h |Horizontal whitespace|
|\H |Not horizontal whitespace|
|\n |Newline|
|\r |Carriage return|
|\t |Horizontal tab|
|\v| Vertical tab (whitespace)|
|\V| Not vertical whitespace|

> [**.**]() **dot_operation** matches all characters but  line ending characters , except under certain circumstances.


