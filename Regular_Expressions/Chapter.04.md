CHAPTER 4 Alternation, Groups, and Backreferences


# 1. Alternation
alternation gives you a choice of alternate patterns to match.

> (match1|match2)

###### < the or The 를 match >
<pre>
$ echo the The THE | grep -E '(the|The)'
the The THE
</pre>

