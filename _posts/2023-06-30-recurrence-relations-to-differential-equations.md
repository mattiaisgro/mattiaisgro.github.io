---
title: 'Sequence Operators: From Recurrence Relations to Differential Equations'
date: 2023-06-30
permalink: /posts/2023/05/recurrence-relations-to-differential-equations/
tags:
  - maths
  - ode

abstract: "Sequence operators on series expansions are inverted to obtain a differential equation from a recurrence relation. Common sequences are considered and their associated differential equations are calculated."
---

_Abstract:_ Sequence operators on series expansions are inverted to obtain a differential equation from a recurrence relation. Common sequences are considered and their associated differential equations are calculated.

_Prerequisites:_ Real Analysis, Algebra, Operators

## Sequence operators on series expansions

In a previous [article](https://mattiaisgro.github.io/posts/2023/04/sequence-operators-differential-equations/), I introduced a system of operators on power series which proved to be useful for the solution of differential equations by series expansion. The main takeaway was that by considering how different operations act on the solution and by always re-indexing the series index, we can drop the series notation and work with a few operators only:

$$
y \rightarrow a_n \\
\frac{d}{dx} \rightarrow \hat D, \ \ x \rightarrow \hat X
$$

which can be deconstructed into the more fundamental operators:

$$
\hat N f(n) a_{g(n)} = n f(n) a_{g(n)} \\
\hat S^a f(n) a_{g(n)} = f(n + a) a_{g(n + a)} \\
\hat D = \hat S \hat N = (\hat N + 1) \hat S \\
\hat X = \hat S^{-1}
$$

By manipulating these operators the following general result was found:

$$
y^{(n)} = f(x, y, y', ...) \ \rightarrow \ a_n =  \frac{(n - k)!}{n!} \hat S^{-k} [F(n, a_{g(n)})]
$$

where $F(n, a_{g(n)})$ is just $f(x, y, y', ...)$ rewritten using the operators. Applying the operators on the sequence of coefficients of the series expansion of the solution, a recurrence relation may be found.

## Rewriting the fundamental operators

So far, the $\hat N$ and $\hat S$ operators were considered more "fundamental", as they could be used to write all other operators acting on power series. The idea behind this was that differential equations can be expressed using a family of *analytic operators* $\hat D$ and $\hat X$. By mapping these operators to our new family of *sequence operators* $\hat S$ and $\hat N$, recurrence relations could be easily deduced. We can instead try to rewrite them with respect to $\hat D$ and $\hat X$:

$$
\hat N = \hat S^{-1} \hat S \hat N = \hat X \hat D \\
\hat S^a = \hat X^{-a}
$$

This notation is not useful by itself, we only obtained another way to write the operators by algebraic manipulations, instead of the previous definition which worked by only specifying how they acted. The true power of this becomes evident when we try to come back from a recurrence relation which relates the coefficients of the solution to the differential equation we were, hypothetically, trying to solve.

## From recurrence relations to differential equations

Given any linear recurrence relation in the form:

$$
a_n = F(n, a_{g(n)})
$$

we can substitute all occurrences of $n$ with $\hat N$ (except in $a_{g(n)}$), as they are equivalent. Wherever there is a term $a_{n + k}$ we can substitute $a_{n + k} = \hat S^{-k} a_n = \hat X^k a_n$ as they are, again, equivalent notations. After these substitutions, we obtain an equivalent formulation of the recurrence relation expressed only in terms of $\hat D$, $\hat X$ and $a_n$. These objects are the same that were initially mapped from the differential equation to the operator formalism and when the mapping is invertible, we can return to the initial differential equation:

$$
a_n \rightarrow y \\
\hat D \rightarrow \frac{d}{dx} \\
\hat X \rightarrow x
$$

As a result:

$$
a_n = F(n, a_{g(n)}) \\
\rightarrow \ y^{(n)} = f(x, y, y', ...)
$$

The initial differential equation may be recovered, but there does not need to be an initial equation in the first place. We could just have a (linear) recurrence relation and wanted to find a differential equation of which it is a solution by series expansion, giving rise to the concept of *generating differential equation*, analogous to *generating functions*.


## Example 1: Bessel's differential equation
In the previous article, the solution by series expansion of Bessel's differential equation  $x^2 y'' + 2xy' + x^2 y = 0$ was found to be:

$$
a_n = - \frac{1}{n^2}a_{n - 2}
$$

Using the aforementioned substitutions:

$$
\hat N^2 a_n + \hat S^{-2} a_n = 0 \\
(\hat X \hat D)^2 a_n + \hat X^2 a_n = 0
$$

Care should be taken in squaring $(\hat X \hat D)$, as they do not commute and so $(\hat X \hat D)^2 \neq \hat X^2 \hat D^2$.

$$
\hat X \hat D \hat X \hat D a_n + \hat X^2 a_n = 0 \\
x \frac{d}{dx} x \frac{d}{dx} y + x^2 y \\
= x \frac{d}{dx} (xy') + x^2 y \\
= x^2 y'' + xy' + x^2y
$$

Thus the initial equation is recovered.

## Example 2: Catalan's numbers

Catalan's numbers are a beatiful sequence which appears throughout combinatorics. For example, they count how many expressions with $n$ couples of parentheses correctly opened and closed there are, or how many different combinations of triangles can be formed by connecting the vertices of a convex polygon with $n + 2$ sides without crossing. The first Catalan numbers are $1, 1, 2, 5, 14, 42, ...$ and they can be obtained by the recurrence relation:

$$
C_n = \frac{4n - 2}{n + 1} C_{n - 1}
$$

with $a_0 = 1$. Since Catalan's numbers are monotonically increasing, a power series whose coefficients are these will obviously diverge. Such a power series is often called *formal power series* and is widely used in combinatorics. It is "formal" because it does not represent any function (since it diverges everywhere except at 0), but it may be used for further manipulations. Let's try to find a differential equation whose series expansion solution has Catalan's numbers as coefficients:

$$
(n + 1) C_n = (4n - 2) C_{n - 1} \\
(\hat N + 1) C_n = (4 \hat N - 2) \hat S^{-1} C_n \\
(\hat X \hat D + 1) C_n - (4 \hat X \hat D - 2) \hat X C_n = 0 \\
(x \frac{d}{dx} + 1) y - (4x \frac{d}{dx} - 2) x y \\
= x \frac{d}{dx} y + y - 4x \frac{d}{dx} x y + 2 xy \\
= xy' + y - 4x (y + xy') + 2xy \\
$$

Giving as a result the differential equation:

$$
x(1 - 4x) y' + (1 - 2x) y = 0
$$

with (diverging) solution:

$$
y = \sum_{n = 0}^\infty C_n x^n = 1 + x + 2 x^2 + 5 x^3 + \ ...
$$

Its correctness can be demonstrated by using again the series expansion method.

## Edge cases

In this new representation, only the $\hat N$ operator contains a derivative operator $\hat D$, the $\hat S$ does not. The problem this fact poses is that when the given recurrence relation has no dependence on $n$, no derivative operator is included in the equivalent expression, and so the result of the inversion is not a differential equation.

## Example 3: Fibonacci's sequence
Fibonacci's sequence is probably the most famous number sequence. It is commonly defined by:

$$
F_n = F_{n - 1} + F_{n - 2}
$$

The recurrence relation does not depend on $n$. By rewriting it using operators:

$$
\hat X^2 F_n + \hat X F_n - F_n = 0
$$

from which, substituting $F_n$ with $y(x)$:

$$
(x^2 + x - 1) \cdot y(x) = 0
$$

The result is not a differential equation, so the $y(x)$ is indeterminate. We cannot find a differential equation from this recurrence relation because there is no dependence on $n$. The polynomial in front of $y(x)$ has roots $-\phi = -(1 + \sqrt{5})/2$ and $\phi - 1 = (-1 + \sqrt{5})/2$ which are almost identical to the generating constants of the Fibonacci sequence in closed form, which are the roots of the polynomial $x^2 - x - 1$:

$$
F_n = \frac{\phi^n - (1 - \phi)^n}{\sqrt{5}}
$$

The roots of the polynomial we have found could be used in a similar fashion, but because of the minus sign the sequence is alternating and we need to introduce a term $(-1)^n$:

$$
F_n = (-1)^n \frac{(-\phi)^n - (1 - \phi)^n}{\sqrt{5}}
$$

The recurrence relation which gives the correct generating constants is instead $A_n = A_{n-2} - A_{n-1}$, giving $(x^2 - x - 1) \cdot y(x)$.

## Conclusions

Inverting the operators enables us to find new interesting results, especially regarding formal power series and recurrence relations. The relationship between recurrence relations, characteristic polynomials and the polynomials obtained by inversion should be further researched. Another interesting topic may be nonlinear recurrence relations and the conditions for invertibility.