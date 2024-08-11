# A130229
Code for computing the OEIS sequence A130229

Sequence <a href="https://oeis.org/A130229">A130229</a> in the OEIS consists of primes $p \equiv 5 \bmod 8$ for which the Pellian equation 

$x^2 - p y^2 = -4$

no solutions in odd integers. Equivalently, let $K = \mathbb{Q}(\sqrt{p})$ with ring of integers $\mathcal{O}_K = \mathbb{Z}[\frac{1+\sqrt{p}}{2}]$ and fundamental unit $\varepsilon_p = \frac{x_0 + y_0\sqrt{p}}{2}$. Here $(x_0, y_0)$ is a fundamental solution to the Pellian equation above and $p$ is an element of A130229 if and only if $x_0$ and $y_0$ are even, equivalently $\varepsilon_p \equiv 1 \bmod 2\mathcal{O}_K$. 

Note that $2$ is inert in $K/\mathbb{Q}$, so there are three possible non-zero residue classes for $\varepsilon_p \bmod 2\mathcal{O}_K$. Heuristically, one thus expects about one third of all primes $p \equiv 5 \bmod 8$ to be members of this sequence.

The present notebook contains code to test this heuristic. We define two counting functions for the sequence A130229. The naive counting function is

$\pi_1(x) = \sum_{p\in A130229, \; p\leq x} 1.$

For a better counting function, first define

$\chi(p) = \left\{ \begin{array}{ll} 
1 & \text{if $p \equiv 5 \bmod 8$ and $\varepsilon_p \equiv 1 \bmod 2\mathcal{O}_K$} \\
-\frac{1}{2} & \text{if $p \equiv 5 \bmod 8$ and $\varepsilon_p \not\equiv 1 \bmod 2\mathcal{O}_K$} \\
0 & \text{if $p \not\equiv 5 \bmod 8$.}
\end{array}
\right.$

Now set 

$
\theta_\chi(x) := \sum_{p \leq x} \chi(p)\log p.
$

Our heuristc leads us to expect that $\theta_\chi(x) = o(x)$, i.e. that the terms mostly cancel out.

The code computes the fundamental solution $(x_0, y_0) \bmod 2$ using the continued fraction method, with $B_i$ and $G_i$ reduced mod 2 at each step. The code computes this in parallel for many primes $p$ on a GPU. 
