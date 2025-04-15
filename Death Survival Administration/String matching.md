# String matching

## definition
+ $\sum^*$: a set, stands for all strings consist of the characters in the set. (null string included)
+ $xy$: concatenation of x and y
+ $x⊏y$: x is the prefix of y
+ $x⊐y$: x is the suffix of x
	+ null string is all strings' prefix & suffix
	+ for all string x, y and char a, $x⊐y$ iff $xa⊐ya$
	+ prefix and suffix are both transitive operator
		+ $x⊐y$ and $y⊐z$, then $x⊐z$

text length: $n$
pattern length: $m$
## naive

complexity: $O((n-m+1)m)$
no explanation needed

$\sqsupset$
$\sqsubset$

## The Knuth-Morris-Pratt Algo (KMP)