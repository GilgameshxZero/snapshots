<!-- emilia-snapshot-properties
The Recurrence Detanglement Conjecture and the Harmonic Series
2022/12/23
utulek
emilia-snapshot-properties -->

# The Recurrence Detanglement Conjecture and the Harmonic Series

December 23, 2022
Útulek Series, 3 | 1761D Arc, 3

I want to start this post by addressing something obvious that I missed in the [previous post](utulek-series-2), which only occurred to me in my sleep.

## 1 Detangling the Pell Recurrence

Recall we were solving Pell equations, and came up with this general recurrence ($(4.1)$):

$$x_i=x_{i-1}x_1+Dy_{i-1}y_1,\\
y_i=x_1y_{i-1}+x_{i-1}y_1.\tag{1.1}$$

which we stated in corollary $(4.3)$ lends itself quite easily to a matrix exponentiation solution:

$$\begin{bmatrix}
x_i\\
y_i
\end{bmatrix}=\begin{bmatrix}
x_1&Dy_1\\
y_1&x_1
\end{bmatrix}^{i-1}\begin{bmatrix}
x_1\\
y_1
\end{bmatrix}.$$

I also put forth the observation that the non-recursive Pell equation solution, derived from eigenvalue decomposition of corollary $(4.3)$ in [Pell Equations Have Infinite Solutions](utulek-series-2), is remarkably similar to Binet’s formula for the Fibonacci sequence:

$$\begin{aligned}
x_i&=\frac{(x_1+y_1\sqrt{D})^i+(x_1-y_1\sqrt{D})^i}{2}\\
y_i&=\frac{(x_1+y_1\sqrt{D})^i-(x_1-y_1\sqrt{D})^i}{2\sqrt{D}}\\
\end{aligned}$$

$$S_i=\frac{1}{\sqrt{5}}((\frac{1+\sqrt{5}}{2})^i	-(\frac{1-\sqrt{5}}{2})^i).$$

In hindsight, it is obvious why this is the case. I put forth the hypothesis in [2D Recurrences and Combinatorial Arguments](utulek-series-1) that “all twin (and likely higher orders) two-dimensional recurrences can be simplified into single two-dimensional recurrences via repeated substitution”. Allow me to state this conjecture more rigorously:

**Conjecture 1.2 (Recurrence Detanglement)**: $n$-variate, $z$-order, $k$-degree, $d$-dimensional recurrences may always be reduced to $n$ disjoint single-variable, $z$-order, $k$-degree, $d$-dimensional recurrences.

Here, I use the terminology $n$-variable to mean $n$ sequences of variables, order to denote the number of terms to be added together for each recurrence, degree to denote the maximum power of terms we see multiplied together, and dimension to denote the number of indices we use to label each variable sequence.

I do not have the proof ready for this claim (I suspect it reduces to eigenvalue decomposition on some $n$-by-$n$ matrix), but I will first demonstrate conjecture $(1.2)$’s viability in the Pell equation $D=3$. Starting with bivariate recurrences $(1.1)$

$$\begin{aligned}
x_i&=2x_{i-1}+3y_{i-1}\\
y_i&=x_{i-1}+2y_{i-1}
\end{aligned}$$

we may make the repeated substitution

$$\begin{aligned}
x_i&=2x_{i-1}+3y_{i-1}\\
&=2x_{i-1}+3x_{i-2}+6y_{i-2}\\
&=2x_{i-1}+3x_{i-2}+6x_{i-3}+12y_{i-3}\\
&=2x_{i-1}+3x_{i-2}+6x_{i-3}+\ldots+3\cdot2^{i-1}\\
\implies x_{i-1}&=2x_{i-2}+3x_{i-3}+6x_{i-4}+\ldots+3\cdot2^{i-2}\\
\implies x_i&=2x_{i-1}+2(x_{i-1}-2x_{i-2})+3x_{i-2}\\
&=4x_{i-1}-x_{i-2}
\end{aligned}\tag{1.3}$$

and similarly for $y_i$:

$$\begin{aligned}
y_i&=2y_{i-1}+x_{i-1}\\
&=2y_{i-1}+3y_{i-2}+2x_{i-2}\\
&=2y_{i-1}+3y_{i-2}+6y_{i-3}+4x_{i-3}\\
&=2y_{i-1}+3y_{i-2}+6y_{i-3}+\ldots+3\cdot2^{i-2}+2^i\\
\implies y_{i-1}&=2y_{i-2}+3y_{i-3}+6y_{i-4}+\ldots+3\cdot2^{i-3}+2^{i-1}\\
\implies y_i&=2y_{i-1}+2(y_{i-1}-2y_{i-2})+3y_{i-2}\\
&=4y_{i-1}-y_{i-2}.
\end{aligned}$$

And indeed, this is now a single-variable, 1-order, 1-dimensional recurrence as hypothesized in conjecture $(1.2)$, which is also the same type of recurrence as the Fibonacci. The similarity in form, then, can fully be explained from this point with the observation that both the Fibonacci recurrence and $(1.3)$ may be written in similar matrix form and decomposed into eigenvalues.

A proper exploration into the recurrence detanglement in conjecture $(1.2)$ will likely lead us onto the path to discover why the bivariate, 3-order, 1-degree, 2-dimensional recurrence $(1.1)$ of 1761D in [2D Recurrences and Combinatorial Arguments](utulek-series-1) 

$$A_{i,j}=3A_{i-1,j}+3A_{i-1,j-1}-8A_{i-1,j-2}$$

results in a sum over combinations. But we will take our time getting there.

First, we must cover the linear sieve.

## 2 A Short Historical Note

Legend has it that in the 1600s, Fermat gave the Pell equation with $D=151$,

$$x^2-151y^2=1,$$

to his clergyman friend Wallis as a challenge, of which the minimal solution is

$$\begin{aligned}
x&=1728148040,\\
y&=140634693.
\end{aligned}$$

Wallis (and another friend of Fermat’s, who also received the challenge) did manage to solve it,  but I imagine it was not without trudging through much manual arithmetic. I’m uncertain if the method of continued fractions was known at the time, but even then, it is no easy task to come up with the solution above.

It is impressive for a clergyman! And perhaps saddening, when one considers the clergymen of the modern times. This incident also harkons to the problem-sharing happening in my competitive programming (CP) circles, between me and Neal, Tony, Sanjeev, Wyatt, Zac, and others. Perhaps one of us will be in the textbooks of the future as the idiot who spent a whole week on a problem that his (much more experienced) friend posed as a joke.

From [his Wikipedia page](https://en.wikipedia.org/wiki/John_Wallis), it seems that Wallis is most famous for the Wallis product

$$\begin{aligned}
\prod_{i=1}^\infty\frac{4i^2}{4i^2-1}&=(\frac{2}{1}\cdot\frac{2}{3})(\frac{4}{3}\cdot\frac{4}{5})(\frac{6}{5}\cdot\frac{6}{7})\cdots\\
&=\frac{\pi}{2}
\end{aligned}$$

which certainly evokes memories of Euler’s derivation of the Riemann zeta function at $2$ (which sounds scary, but is defined simply):

$$\begin{aligned}
\zeta(s)&:=\sum_{n=1}^\infty\frac{1}{n^s}\\
\zeta(2)&:=\sum_{n=1}^\infty\frac{1}{n^2}\\
&=1+\frac{1}{4}+\frac{1}{9}+\frac{1}{16}+\cdots\\
&=\frac{\pi^2}{6}.
\end{aligned}\tag{2.1}$$

Unfortunately this evocation is no coincidence, and Euler’s method for deriving $\zeta(2)$ unfortunately does trivialize Wallis’s derivation of his own product. Luckily, both derivations are tangential to our upcoming investigation into the Linear Sieve and Taylor’s Series, and I intend to discuss $(2.1)$ when the time is right.

First, we need to establish the growth rates of the harmonic and prime harmonic series.

## 3 The Harmonic Series is $\Theta(\ln N)$

In CP, the well-known method to determine the prime numbers is the Sieve of Eratosthenes:

```
is_prime = [true, true, ...]
for i = 2 to N:
	if is_prime[i]:
		for j = i*i to N by i:
			is_prime[j] = false
```

which is quoted to $O(N\ln\ln N)$. Of course, $\ln\ln$s are uncommon and should raise some eyebrows. We can loosen the algorithm a little by starting the inner loop at $2i$ instead of $i^2$, which roughly gives us the big-O runtime estimate

$$\begin{aligned}
P_\infty&:=1+1/2+1/3+1/5+1/7+1/11+\ldots,\\
P_i'&:=1/p_i,\\
P_i&:=\sum_{j=1}^i 1/p_j,
\end{aligned}\tag{3.1}$$

with $p_i$ denoting the $i$-th prime number.

We will use the convention that $S_i'$ denotes the $i$-th term in a sequence, and $S_i$ denotes the sum of the first $i$ terms in the sequence, or alternatively the $i$-th term in the corresponding series. Thus, $S_\infty$ will refer to the (possibly divergent) sum of the infinite series.

$P_i$ is, of course, a subset of the Harmonic Series, which I believe is taught in most high school classes today:

$$\begin{aligned}
\zeta(1):=H_\infty&:=1+1/2+1/3+1/4+1/5+\ldots,\\
H_i'&:=1/i,\\
H_i&:=\sum_{j=1}^i 1/j,
\end{aligned}$$

but only to the extent that the harmonic series diverges. The proof proceeds by grouping the terms of the sequence in groups of size of increasing powers of two:

$$\begin{aligned}
H_\infty&=(1)\\
&+(1/2+1/3)\\
&+(1/4+1/5+1/6+1/7)\\
&+\ldots,
\end{aligned}$$

of which the terms in each group are lower-bounded by subsequently smaller powers of two:

$$\begin{aligned}
H_\infty&>(2^{-1})\\
&+(2^{-2}+2^{-2})\\
&+(2^{-3}+2^{-3}+2^{-3}+2^{-3})\\
&+\ldots,
\end{aligned}$$

whose grouped sum reduces nicely into an arithmetic series, which obviously diverges:

$$\begin{aligned}
H_\infty&=2^{-1}+2\cdot2^{-2}+4\cdot2^{-3}+\ldots\\
&=1/2+1/2+1/2+\ldots\\
&\to\infty.
\end{aligned}$$

The beautiful part about this proof of divergence is that it also gives us the big-O rate of growth of the series $H_i$, which, based on the exponentially increasing size of the groups, is $\Theta(\ln N)$. One can also arrive at this conclusion by examining the integral of series, which approximates the series itself:

$$H_i\approx\int_1^i \frac{1}{j}dj=\ln j\bigg\rbrack_{j=1}^i.$$

In fact, if we are even more precise with our integrals, we can bound $H_i$ fairly closely,

$$\ln(i+1)<H_i<\ln(i)+1,\\[3ex]
H_i=\Theta(\ln N).\tag{3.2}$$

## 4 Intuition for Prime Harmonic Series

Fermat and Euler were unfortunate enough to live at a time where notation to describe the growth rate of functions was not widespread. The great mathematicians of the late 1700s, such as Gauss, Legendre, Fermat, Euler (who, as I have learned, was a student of Bernoulli’s—an unfortunate reality, as I have far more respect for the number theorists than statisticians), Dirichlet, and Chebyshev all almost certainly played with the idea of the prime number theorem (PNT), which is best stated as a theorem of function growth rates.

**Theorem 4.1 (PNT)**: The number of primes less than $N$, $\pi(N)$, is $\Theta(N/\ln N)$. That is, a proportion of approximately $1/\ln N$ of the first $N$ numbers are prime.

Of course, the reason these great mathematicians were unable to prove the PNT is because its proof is fairly involved. Hence, said proof will lie outside the scope of this series of posts, at least until we introduce some ideas from introductory complex analysis. It’s truly a shame, though, since from the PNT one may be able to deduce the importance of complexity analysis to mathematics at large—but of course, complexity analysis was not formalized until more rigorous study of algorithms.

---

The PNT does, however, give some intuition into the growth rate of the prime harmonic series $(3.1)$. We already have that the prime harmonic series $P_i$ is bound by the harmonic series $H_i$ with $O(\ln N)$. Supposing we take $1$ of every $\ln N$ terms in the harmonic series, by PNT, the number of terms we take grows at the same rate as the number of terms in $P_i$. This sieved harmonic series necessarily grows at $\Theta(\ln N/\ln N)=\Theta(1)$.

However, this is a lower bound, since we know by PNT that primes also occur more frequently for smaller numbers. Hence, the growth rate of the prime harmonic series $(3.1)$ must lie between $o(1)$ and $O(\ln N)$.

Few runtimes lie in the real between $o(1)$ and $O(\ln N)$. Most commonly, there are three:

1. The inverse Ackermann, $\Theta(\alpha(N))$, which shows up in the complexity analysis for an optimized disjoint-set-union/union-find.
2. The log-log $\Theta(\ln\ln N)$, which we hope to get here for the Sieve of Eratosthenes, and likely only shows up when primes are involved (which, granted, is almost always).
3. The log-star $\Theta(\ln^* N)$, which is even more obscure, whose appearance I’m only familiar with in the Delaunay/Voronoi triangulation algorithm.

## 5 Euler’s “Golden Bridge”

With little time remaining, I’d like to introduce the “golden bridge” which is Euler’s product formula:

$$\zeta(1):=\sum^\infty\frac{1}{i}=\prod^\infty (1-1/p_i)^{-1}$$

which can actually be easily generalized to integer values of the zeta function.

**Theorem 5.1 (Euler’s Product Formula)**:

$$\zeta(s):=\sum^\infty\frac{1}{i^s}=\prod^\infty (1-1/p_i^s)^{-1}.$$

This is, to understate nothing, a *huge deal*. One may see inklings of the prime harmonic series on the RHS of Euler’s product formula. My proof of it requires the use of the Taylor series for $\ln N$, so I will begin next time by introducing this. In the meantime, it may be a good use of time to review Taylor series from Tony’s blogpost [Taylor expansions: An easy derivation](https://terveisin.tw/posts/taylor-expansions/).
