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
## intuition
Given a pattern $P$ and and text $T$, if we find $P[1:q]$ matches $T[1+s:s+q]$, we can skip some shiftings by memorizing "something". More practically, we want to find the longest prefix of $P$ such that it match the suffix of $T[1+s:s+q]$. In other words, what we need to do is find the smallest shift $s'$ such that some $k<q$ satisfies $P[1:k]$ matches $T[1+s':s'+k]$. There $s'=s+q-k$.

## The Rabin-Karp Algo

**Average** running time is $O(n)$.

Let $\sum=\{0,1,2,\dots,9\}$, we can convert a string into a decimal number (checksum), let $t_s$ stands for $T[s+1,s+m]$, p is decimal of pattern $P$, $t_s=p$ iff $T[s+1,s+m]=P$, i.e, $P$ is a valid shift of $T$ . 

$p$ can be calculated within $O(m)$ (like below)
![[Pasted image 20250415143355.png]]

$t_{s+1}$ can be calculated from $t_s$ in constant time:
![[Pasted image 20250415144151.png]]

In short: $O(m)$ preprocessing time, $O(n-m)$ matching time
### non-digit string?

Let $|\sum|=d$, we may consider a $d$ numeral system, for each character, we assign it an index$\in[1,d]$, then the process that convert pattern $P$ to checksum $p$ would become:

$p=idx(P[m])+d*(idx(P[m-1])+d*(idx(P[m-2]+d*\dots)))$

### modular arithmetic

1. $a_1\equiv b_1(mod\ n)$ and $a_2\equiv b_2(mod\ n)$, then $a_1+a_2\equiv b_1+b_2(mod\ n)$ and $a_1a_2\equiv b_1b_2(mod\ n)$
2. $a\%b$ means the least positive number that subtracted from a to make it divisible by $b$

We can take $q$ that $dq$ is within 32-bit or 64-bit, so the algorithm becomes:
+ if $t_s\ not\ \equiv p (mod\ q)$, then s is invalid shift
+ if $t_s\equiv p(mod\ q)$, then $O(m)$ check. ($t_s\neq p$ is called spurious hit)

It would be better if $(q,d)=1$, since the result of modular operation will me *more* discrete.