+++
title = 'LED and GCD'
date = 2025-02-08
draft = true
math = true
+++

The following problem is from my university's Putnam Club problem set for this week. It was pulled from one of Northwestern's practice sets, where the problem is given without a source, but my friend Pramana and I suspect it to be an old classic problem.

> **Problem**: A circle contains $n$ lights, with exactly one initially on. You are permitted to do the following: given any proper divisor $d$ of $n$, consider any $\tfrac{n}{d}$ lights arranged at regular intervals (every $d$th light). If they are all in the same state, you may swap all their states simultaneously. For which positive integers $n$ is it possible to turn all the lights off?

**Solution**: We claim that the given task is impossible for all $n$. Label the lights clockwise by $\ell_0, \ldots, \ell_{n-1}$ and let $\zeta$ be a primitive $n$th root. Define:
$$C := \sum_{\text{$\ell_i$ is on}} \zeta^i$$
Assuming the lights are uniformly spaced, $C$ denotes the center of mass of the lights which are on. At any step, we either add or subtract $\Delta = \zeta^k + \zeta^{k+d} + \cdots + \zeta^{k+(n-1)d}$ to $C$, where $0 \leqslant k < d$, and $\Delta = 0$ since $d$ is a proper divisor of $n$. Thus, $C$ is invariant.

Initially, we begin with $C$ equal to some $n$th root of unity. However, if we were to turn all the lights off, then we would have $C = 0$. Thus, it is not possible to go from the given initial setup to the target setup. $\square$

My natural follow-up was to relax the condition that the $\tfrac{n}{d}$ lights must be in the same state. Thus, we have the new question:

> **Problem**: A circle contains $n > 1$ lights, with exactly one initially on. You are permitted to do the following: given any proper divisor $d$ of $n$, you may swap the states of any $\tfrac{n}{d}$ lights arranged at regular intervals. For which positive integers $n$ is it possible to turn all the lights off?

The original proof breaks down since $C$ is no longer an invariant. You might realize that the new problem may be rephrased purely as a question in linear algebra:

> **Reformulated Problem**: Consider the set $S$ in $\mathbb{F}_2^n$ consisting of vectors where the $i$th coordinate is $1$ if and only if $i \equiv k \bmod{d}$ for some choice of proper divisor $d$ of $n$ and $0 \leqslant k < d$. Does $S$ span $\mathbb{F}_2^n$?

Initially, this seems plausible since the number of vectors equals the sum of the proper divisors of $n$, which is equal to $n$ for perfect numbers and greater than $n$ for *abundant* numbers. However, we shall prove that the answer is still negative for all positive integers $n$. Clearly, $n = 1$ is impossible, so we shall henceforth assume that $n > 1$.

During the Putnam Club meeting, Dima and I came up with two distinct solutions.

**Solution 1**: *Proposed by Dima Arinkin*. We shall construct a non-trivial linear equation satisfied by all vectors in $S$. Write $n = p_1^{\alpha_1}\cdots p_r^{\alpha_r}$, where the primes $p_j$ are distinct and the exponents $\alpha_j$ are positive integers. By the Chinese Remainder Theorem, for every function $f: \\{1, 2, \ldots, r \\} \to \\{0, 1\\}$, there exists a unique integer $0 \leqslant s_f < n$ such that for all $1 \leqslant j \leqslant r$, we have $s_f \equiv f(j)p^{j-1} \bmod{p^j}$. Our linear equation will be:
$$\sum_f x_{s_f} = 0$$
where $f$ ranges over all functions $\\{1, 2, \ldots, r \\} \to \\{0, 1\\}$. Consider the vector in $S$ corresponding to the proper divisor $d \mid n$ and remainder $0 \leqslant k < d$. Since $d < n$, there exists some $1 \leqslant j_d \leqslant r$ such that $p_{j_d}^{\alpha_{j_d}} \nmid d$. For any $f: \\{1, 2, \ldots, r \\} \to \\{0, 1\\}$, define $f\'$ such that $f\'(j) = f(j)$ if and only if $j \neq j_d$. It is easy to check that $d \mid (s_f - s_{f\'})$, so the vector satisfies $x_f + x_{f\'} = 0$. Adding these equations over all pairs $f$ and $f\'$ proves that any vector in $S$ satisfies the provided linear equation. $\square$

**Solution 2**: Enrich the vector space $\mathbb{F}_2^n$ with the structure of the ring $\mathbb{F}_2[x]/(x^n-1)$, where the coordinate basis is $1, x, \ldots, x^{n-1}$. The vectors in $S$ are precisely the elements of the subspace spanned by $x^k(1+x^d+\cdots+x^{n-d}) = x^k \cdot \tfrac{x^n-1}{x^d-1}$, where $d$ ranges over proper divisors and $0 \leqslant k < d$. However, this is precisely the *ideal*:
$$I_n = \left\langle\frac{x^n-1}{x^d-1} : \text{$d$ is a proper divisor of $n$}\right\rangle$$
Thus, the question reduces to proving that $\mathbb{F}_2[x]/I_n \neq 0$ for all $n > 1$. We shall prove more generally that $\mathbb{F}_p[x]/I_n \neq 0$ for any prime $p$, where $I_n$ is defined analogously. Write $n = p^{\alpha}m$, where $p \nmid m$. The $\overline{\mathbb{F}}_p$-roots of the GCD of the generators of $I_n$ satisfy the equation $(x^m-1)^{p^{\alpha}} = x^n - 1$, so they must be $m$th roots of unity. We analyze the multiplicity of primitive $e$th roots of unity for each $e \mid m$.

- If $e < m$, then consider $d = p^{\alpha}e$. Any $e$th root of unity has multiplicity $p^{\alpha}$ in both $x^n-1 = (x^m-1)^{p^{\alpha}}$ and $x^d-1 = (x^e-1)^{p^{\alpha}}$. Thus, none of the roots of $\tfrac{x^n-1}{x^d-1}$ (and hence the GCD) are equal to $e$th roots of unity.

- Any primitive $m$th root of unity has multiplicity $p^{\alpha}$ in $x^n-1$. For proper $d \mid n$, a primitive $m$th root has multiplicity $p^{\beta}$ in $x^d-1$ if $d = p^{\beta}m$ for some non-negative integer $\beta$ and multiplicity $0$ otherwise. Thus, the minimum multiplicity of a primitive $m$th root of unity in $\tfrac{x^n-1}{x^d-1}$ is exactly $p^{\alpha}-p^{\alpha-1}$ if $\alpha > 0$ and $1$ otherwise. Thus, the multiplicity of a primitive $m$th root of unity in the GCD is $\varphi(p^{\alpha})$.

It follows that $I_n = \langle \Phi_m(x)^{\varphi(p^{\alpha})}\rangle$, where $\Phi_m$ is the $m$th cyclotomic polynomial. However, since we are working in characteristic $p$, $\Phi_m(x)^{\varphi(p^{\alpha})} = \Phi_n(x)$, and we may simplify our answer as $I_n = \langle \Phi_n(x) \rangle$. This is a proper ideal of $\mathbb{F}_p[x]$ as required. $\square$

**Remark**: Consider the ideals $I_n = \langle \tfrac{x^n-1}{x^d-1} : \text{$d$ is a proper divisor of $n$} \rangle$ and $J_n = \langle \Phi_n(x) \rangle$ in $\mathbb{Z}[x]$. We have proven that $I_n$ and $J_n$ are equal modulo $p$ for all primes $p$. This proves that $I_n = J_n$ as ideals in $\mathbb{Z}[x]$. Indeed, since $I_n + J_n$ is contained in $\bigcap_{p \text{ prime}} (p) = 0$ in the quotient $\mathbb{Z}[x]/J_n$, we have $I_n + J_n = J_n$, and we similarly get $I_n + J_n = I_n$.

**Silly Remark**: We previously brought up perfect numbers in our conversation. They are interesting in the context of Solution 2 for reasons completely different to why they were initially mentioned. When $n$ is an even perfect number - as all perfect numbers are conjectured to be - it must be of the form $n = 2^{q-1}(2^q-1)$, where $2^q-1$ is a Mersenne prime. Consider the affine scheme $X_n := \mathrm{Spec} \\, \mathbb{F}_2[x]/I_n$:

- We have $I_n = \langle \Phi_{2^q-1}(x)\rangle^{2^{q-1}}$. Geometrically, the points of $X_n$ are very fuzzy.
- Observe that $\mathrm{ord}\_{2^q-1} (2) = q$ is unusually small. Consequently, $\Phi_{2^q-1}(x)$ factors as $\tfrac{2^q-1}{q}$ irreducible factors of degree $q$ in $\mathbb{F}_2[x]$. Thus, $X_n$ has several (small) points.

Just as I thought I was finished writing this blog post, I realized that there is another way to approach this problem. So here we go again...

**Solution 3**: Our argument will be motivated by the result of Solution 2 - the codimension of the span of $S$ is equal to $\varphi(n)$. Combinatorially, this is saying that there are $2^{\varphi(n)}$ subsets $T \subset \mathbb{Z}/n$ such that for any proper divisor $d$ of $n$, the fibers of the projection $T \to \mathbb{Z}/d$ have even cardinality. We shall prove this fact again. Note that it suffices to look at proper divisors of the form $d = \tfrac{n}{p_j}$, where $n = p_1^{\alpha_1} \cdots p_r^{\alpha_r}$.

For each $1 \leqslant j \leqslant r$, construct $A_j \subseteq \mathbb{Z}/p_j^{\alpha_j}$ by picking exactly one element from each fiber of the natural projection $\mathbb{Z}/p_j^{\alpha_j} \to \mathbb{Z}/p_j^{\alpha_j-1}$ and let $B_j$ be the complement of $A_j$. We interpret $B = B_1 \times \cdots \times B_r$ as a subset of $\mathbb{Z}/n$ of cardinality $\varphi(n) = \prod_j \varphi(p_j^{\alpha_j})$ using the Chinese Remainder Theorem. Define the *weight* of an element $s \in \mathbb{Z}/n$ to be the number of $1 \leqslant j \leqslant r$ for which $s$ projects to $A_j$ in $\mathbb{Z}/p_j^{\alpha_j}$. For example, the elements of weight $0$ are precisely the elements of $B$.

We show that for every subset $T\' \subset B$, there exists a unique $T \subset \mathbb{Z}/n$ satisfying the required properties with $T \cap B = T\'$. This will complete the proof since $|2^B| = 2^{\varphi(n)}$. For any $d = \tfrac{n}{p_j}$, each fiber of $\mathbb{Z}/n \to \mathbb{Z}/d$ has a unique element of highest weight by construction, since there is a unique lift which projects to $A_j$ by the Chinese Remainder Theorem. On the other hand, for any element $s \in \mathbb{Z}/n$ of positive weight, we can pick $1 \leqslant j \leqslant r$ such that $s$ projects to $A_j$. Then, for $d = \tfrac{n}{p_j}$, the map $\mathbb{Z}/n \to \mathbb{Z}/d$ has a fiber in which $s$ is the unique element of highest weight.

Now, given a subset $T\' \subset B$, we have determined the elements of $T$ with weight $0$. Then, for each element $s$ of weight $1$ in $\mathbb{Z}/n$, there exists some $d$ for which $\mathbb{Z}/n \to \mathbb{Z}/d$ has a fiber with $s$ as the element of highest weight. This determines whether $s$ is in $T$ or not since the fiber must have an even number of elements from $T$. We can similarly induct on weight to see that we are forced into at most one possibility for $T$.

Now, we shall explicitly construct $T$ to show existence. For each $s \in \mathbb{Z}/n$, let $x_s \in \mathbb{F}_2$ be $1$ if and only if $s \in T$. For each $s \in \mathbb{Z}/n$ of positive weight, define the subset $B(s) \subset \mathbb{Z}/n$ to consist of all elements $s\' \in \mathbb{Z}/n$ not equal to $s$ such that for each $1 \leqslant j \leqslant r$: 
- If $s$ projects to $A_j$, then $s\' \equiv s \bmod{p_j^{\alpha_j-1}}$, or 
- If $s$ projects to $B_j$, then $s\' \equiv s \bmod{p_j^{\alpha_j}}$.

Note that $B(s)$ only contains elements of strictly lower weight than $s$. We define the values of $x_s$ by induction on the weight of $s$. The weight $0$ case is already determined by $T\'$. For positive weight $s$, define $x_s = \sum_{s\' \in B(s)} x_{s\'}$. We leave it as an exercise to the reader to see that this works! $\square$