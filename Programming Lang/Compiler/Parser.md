FIRST set:
1. if x is terminal, FIRST(x) = {'x'}
2. if $x-> \epsilon$ is a production rule, add $\epsilon$ to FIRST(x)
3. if $x-> Y_1 Y_2 Y_3 ... Y_n$ is a production
	1. FIRST(x) = FIRST($Y_1$)
	2. FIRST($Y_1$) contains  $\epsilon$ , FIRST(x) = {FIRST($Y_1$) - $\epsilon$ } $\cup$ {FIRST(Y2)}
	3. FIRST($Y_i$) contains $\epsilon$ for all i=1 to n, then add $\epsilon$  to FIRST(x)

FOLLOW set:
1. FOLLOW(S) = { $ }
2. If $A -> pBq$ is a production, where p, B and q are grammer symbol, everything in FIRST(q) except $\epsilon$  in FOLLOW(B)
3. If $A->pB$ is a production, then everything in FOLLOW(A) is in FOLLOW(B)
4. If $A->pBq$ is a production and FIRST(q) contains $\epsilon$ then FOLLOW(B) contains {FIRST(q) - $\epsilon$ } $\cup$ FOLLOW(A)
