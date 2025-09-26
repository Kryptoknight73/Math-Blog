+++
title = 'A Proof of the Fundamental Theorem of Algebra'
date = 2025-08-25
math = true
+++

In this blog post, I'll discuss a proof of the Fundamental Theorem of Algebra that I came up with about a year ago.

> <span class = "both">The Fundamental Theorem of Algebra:</span> $\bb{C}$ is an algebraically closed field.

**<span class = "both">Proof:</span>** Assume that $\bb{C}$ is not algebraically closed. Consider any non-trivial finite extension $\bb{K}/\bb{C}$. The field extension $\bb{K}/\bb{R}$ has degree $n > 2$. We may assume that $\bb{K}/\bb{R}$ is Galois after replacing $\bb{K}$ with its Galois closure over $\bb{R}$. Endow $\bb{K}$ with the structure of a smooth $n$-manifold using its $\bb{R}$-vector space structure.

> <span class = "both">Lemma 1:</span> The following maps are smooth:
> - The multiplication map $m: \bb{K} \times \bb{K} \to \bb{K}$.
> - The Galois conjugation maps $\sigma: \bb{K} \to \bb{K}$ for $\sigma \in \mathrm{Gal}(\bb{K}/\bb{R})$.
> - The norm map $N: \bb{K} \to \bb{R}$.
> - The inverse map $i: \bb{K}^{\times} \to \bb{K}^{\times}$.
>
> Thus, $\bb{K}^{\times}$ is a Lie group under the subspace topology.

**<span class = "both">Proof of Lemma 1:</span>** The multiplication map is $\R$-bilinear and the Galois conjugation maps are $\R$-linear, so they are both smooth. The norm map $N$ can be obtained from composing these functions appropriately and restricting the codomain, so it is smooth. Finally, the inverse map can be written as:
$$i(\alpha) = \frac{1}{N(\alpha)}\prod\_{\sigma \in \mathrm{Gal}(\bb{K}/\bb{R})} \sigma(\alpha)$$
making it smooth. Given that $m: \bb{K}^{\times} \times \bb{K}^{\times} \to \bb{K}^{\times}$ and $i: \bb{K}^{\times} \to \bb{K}^{\times}$ are smooth, $\bb{K}^{\times}$ must be a Lie group. $\square$

> <span class = "both">Lemma 2:</span> The squaring map $F: \bb{K}^{\times} \to \bb{K}^{\times}$, given by $\alpha \mapsto \alpha^2$, is open.

**<span class = "both">Proof of Lemma 2:</span>** By the inverse function theorem, it suffices to show that for any $\alpha \in \bb{K}^{\times}$, the map $dF\_{\alpha}: \bb{K} \to \bb{K}$ is an isomorphism of $\R$-vector spaces. Indeed, the derivative of the map $F: \alpha \mapsto \alpha^2$ is simply $dF\_{\alpha}: x \mapsto 2\alpha x$, which is indeed an isomorphism of $\R$-vector spaces. $\square$

We now prove the Fundamental Theorem of Algebra. The homomorphism $F: \bb{K}^{\times} \to \bb{K}^{\times}$ induces a homomorphism $f: \bb{K}^{\times}/\bb{R}^+ \to \bb{K}^{\times}/\bb{R}^+$. We claim $f$ has the following properties:
- **Open**: This is equivalent to saying that the image of a saturated open set under $F$ is also saturated and open. Indeed, such an image must be saturated since $F: \bb{R}^+ \to \bb{R}^+$ is surjective and must be open by Lemma 2.
- **Closed**: This is because $\bb{K}^{\times}/\bb{R}^+ \cong S^{n-1}$ is compact Hausdorff.
- **Surjective**: The image of $f$ is non-empty, open, and closed. Since $S^{n-1}$ is connected, the image must be  $S^{n-1}$.
- **$2$-to-$1$**: The kernel of $f$ corresponds to elements of $\bb{K}^{\times}$ whose squares are elements of $\bb{R}^+$. These are precisely the elements of $\bb{R}^{\times}$, so $\ker f = \bb{R}^{\times}/\bb{R}^+ \cong \\{\pm 1\\}$.

This means that the map $f: S^{n-1} \to S^{n-1}$ must be a double cover. However, for $n > 2$, the space $S^{n-1}$ is simply-connected, so we have the required contradiction. $\square$