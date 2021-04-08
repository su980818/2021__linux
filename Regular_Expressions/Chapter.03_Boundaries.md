# In this chapter

##### [This chapter focuses on assertions. A zero-width assertion doesn’t match a character, perse, but rather a location in a string.]()


####  I'll talk about in this chapter are:
+ The beginning and end of a line or string
+ Word boundaries (two kinds)
+ The beginning and end of a subject
+ Boundaries that quote string literals

## 1. The Beginning and End of a Line

To match the beginning of a line or string, use the caret or circumflex (U+005E)
> [**^**]()
 
To match the end of a line or string, use the dollar sign:
> [**$**]()

## 2. Word boundaries and Non-Word boundaries (two kinds)

>[**\b \b**]()

<pre> \bthe\b </pre>
![image](https://user-images.githubusercontent.com/78835559/113671224-092a8b80-96f1-11eb-82d4-49a01c252b8f.png)

>[**\B \B**]()

<pre> \Batter\B </pre>
![image](https://user-images.githubusercontent.com/78835559/113671166-f6b05200-96f0-11eb-8693-cba6f64bc7a2.png)

## 3. Quoting a Group of Characters as Literals

> [**\Q \E**]()

Between of Q and E , Regular expression dont use metacharacter.  
