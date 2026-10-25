
# Q2d. 
#### Why `k` doesn't affect the validity:

`k` can be arbitrarily big, but none of the constructions used ever use the ***value*** of `k`, only needing to copy the binary code of `k` over. $L_k \leq N$, so `k` never causes the bounds to be violated.

#### Why empty rows aren't an issue:

Even with empty rows, the sets and rows will still have explicitly listed labels. Consequently, $s \leq N$ holds for the $VC \leq _p SC_2$ direction, and the listed isolated vertices will ensure the bounds are met in the $SC_2 \leq _p VC$ direction.

# Q2c.
#### If $SC_2$ problem has solution, then $VC$ problem has solution:

If there exists $J$ such that $\bigcup _{j \in J} S_j = U, \|J\| \leq k$, then for the constructed $VC$ problem, $X = \{v_j | j \in J\}$ is a valid solution, as $\|X\| = \|J\| \leq k$ and $\forall e \in E = S,\ \exists j \in J\ s.t.\ v_j$ is one of the endpoints to $e$.

#### If $VC$ problem has solution, then $SC_2$ problem has solution:

Choose $J$ as $J = \{j | v_j \in X\}$, if $X$ is a valid solution, $\| J\| = \|X\| \leq k$ and $u \in U = E$, by definition $u$ would have an endpoint in $X$, call this endpoint $v_n$, then $u \in S_n$ (because the edge connects to $v_n$ only if the edge belongs to $S_n$ by the rules of construction).