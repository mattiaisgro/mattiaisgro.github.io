---
title: 'Sequence Operators for the Series Expansion of Differential Equations'
date: 2023-04-12
permalink: /posts/2023/04/sequence-operators-differential-equations/
tags:
  - maths
  - ode

abstract: "We present an operator formalism for the solution of ordinary differential equations using series expansion. These operators make it possible to easily map a differential equation into an algebraic equation."
---

_Abstract:_ We present an operator formalism for the solution of ordinary differential equations using series expansion. These operators make it possible to easily map a differential equation into an algebraic equation.

_Prerequisites:_ Real Analysis, Algebra, Operators

## Series Expansion of Differential Equations
One of the most common approaches to solving an ODE when other methods are not available is to expand the solution as a power series, much like a Taylor series, supposing that, at least for a small interval, the series converges (local solution). For instance, given a differential equation and the initial conditions:

$$
y^{(n)} = f(x, y, y', ..., y^{(n - 1)}) \\
y(0) = a_0 \\
... \\
y^{(n - 1)}(0) = a_{n - 1}
$$

We can suppose that the solution $y(x)$ can be expanded as a power series in $x$:

$$
y(x) = \sum_{n = 0}^\infty a_n x^n
$$

Plugging this sum in the differential equation we can equate terms in different sums with the same degree to obtain a recurrence relation which defines the $a_n$ terms starting from the initial conditions $a_0, a_1, ..., a_{n-1}$.

$$
\frac{d^k}{dx^k} \sum_{n = 0}^\infty a_n x^n = f(x, \sum_{n = 0}^\infty a_n x^n, ...)
$$

from which we can derive an equation for the coefficients:

$$
a_n = F(n, a_{g(n)})
$$

You can skip the following example if you have already used the series expansion method.
{: .notice}

### Example 1: Exponential
We can solve the simplest differential equation:

$$
y' = y
$$

Let's suppose that $y(x)$ can be written as a power series and plug it into the equation:

$$
\frac{d}{dx} \sum_{n = 0}^\infty a_n x^n = \sum_{n = 0}^\infty a_n x^n
$$

We can exchange the sum and the derivative and differentiate $x^n$:

$$
\sum_{n = 1}^\infty n a_n x^{n - 1} = \sum_{n = 0}^\infty a_n x^n
$$

The derivative drops a factor $n$ and shifts the degree of $x$ by $-1$. We can't easily equate the coefficients as the powers of $x$ are different between the two sums. We can fix this by changing the summation index on the left hand side, changing every occurrence of $n$ with $n + 1$ and changing the starting value to $0$:

$$
\sum_{n = 0}^\infty (n + 1) a_{n + 1} x^n = \sum_{n = 0}^\infty a_n x^n
$$

Now we can equate powers of $x$ with the same exponent to obtain:

$$
a_{n + 1} = \frac{a_n}{n + 1}
$$

We can shift all indices by $1$ to obtain a recurrence relation for $a_n$ because the index is arbitrary, as long as we shift all occurrences of $n$ (we could have also changed the index on the right hand side):

$$
a_n = \frac{a_{n - 1}}{n}
$$

The coefficients are defined with respect to the previous one, getting divided by $n$ each time. Considering this division is recursive, it's easy to see that the $1/n$ term generates a factor of $1/n!$ in the overall formula. We can also clearly see that for $n = 0$, we can't evaluate this formula, as both $a_{n - 1}$ and $1/n$ are undefined. This was expected, as the solution of a first order differential equation depends on the given initial condition for $y(0) = a_0$. After these considerations, it is evident that our solution is:

$$
y(x) = \sum_{n = 0}^\infty a_n x^n = \sum_{n = 0}^\infty \frac{a_0}{n!} x^n = a_0 e^x
$$

## Operators on sequences

The point of the series expansion method is that we can get a recurrence relation using only algebraic manipulations to solve a complex ODE. The calculations can be quite tedious and error prone, while being mechanical and repetitive. By examining how different operations change the indices and degrees in the series, we may construct an operator formalism to easily solve problems using this method. Our objective is to map (the biggest possible subset of) ODEs to an expression only in $n$ and $a_{g(n)}$:

$$
y^{(n)} = f(x, y, ...) \rightarrow a_n = F(n, a_{g(n)})
$$

Let's recall how the derivative worked:

$$
\frac{d}{dx} \sum_{n = 0}^\infty a_n x^n = \sum_{n = 1}^\infty n a_n x^{n - 1} \\ = \sum_{n = 0}^\infty (n + 1) a_{n + 1} x^n
$$

First we drop a factor $n$ and divide by $x$, then we shift the whole expression by $1$ in $n$. **By always shifting the sum to get $x^n$, we can equate the terms in different sums immediately**. If we define new operators keeping this in mind, we can drop the sum notation and work directly on the coefficients $a_n$. More formally, we can define a **derivative operator** that acts on the sequence of coefficients like this:

$$
\hat{D} f(n) a_{g(n)}= (n + 1) f(n + 1) a_{g(n + 1)}
$$

where the function of $n$ in front of $a_{g(n)}$ must be shifted as well (the whole expression under summation is shifted).

Another common operation in differential equations is a multiplication by $x$:

$$
x \sum_{n = 0}^\infty a_n x^n = \sum_{n = 0}^\infty a_n x^{n + 1} \\
= \sum_{n = 1}^\infty a_{n - 1} x^n
$$

Multiplication by $x$ shifts the coefficients by $-1$. We should also keep in mind that the sum now starts from $1$, not $0$. The corresponding operator is:

$$
\hat X f(n) a_{g(n)}= f(n - 1) a_{g(n - 1)}
$$

These two operators are already quite useful for many applications. The next step is to further simplify them by looking at how they work. The derivative drops a factor $n$ and shifts the whole expression by $+1$, while multiplication by $x$ shifts the whole expression by $-1$. We can decompose these operators into more fundamental ones which correspond to these actions. The first action is "multiply by  $n$" with the **number operator**:

$$
\hat N f(n) a_{g(n)} = n f(n) a_{g(n)}
$$

The second action is "shift the whole expression by an integer $k$" with the **shift operator**:

$$
\hat S f(n) a_{g(n)} = f(n + 1) a_{g(n + 1)} \\
\hat S^k f(n) a_{g(n)} = f(n + k) a_{g(n + k)}
$$

It should be noted that when a negative shift is applied, terms of the series are truncated, that is, the first $-k$ terms are $0$ because the new sum starts at $-k$. We can now rewrite the previous operators using the new, more fundamental, ones:

$$
\hat D = \hat S \cdot \hat N = (\hat N + 1) \cdot \hat S \\
\hat X = \hat S^{-1}
$$

The $\hat X$ operator is really a negative shift in disguise. Note that the order matters, as these operators do not necessarily commute. In fact $[\hat S, \hat N] = \hat S$ and $[\hat D, \hat X] = 1$. This last commutator is equivalent to **Leibniz's rule**:

$$
\hat D \hat X a_n = (\hat X \hat D + 1) a_n = (n + 1) a_n
$$

Computing powers of these operators proves really useful:

$$
\hat D^k = (\hat N + 1) \hat S (\hat N + 1) \hat S ... \\
= (\hat N + 1) (\hat N + 2) (\hat N + 3) ... \hat S^k \\
\hat D^k a_n = \frac{(n + k)!}{n!} a_{n + k} \\
\hat X^k = \hat S^{-k}
$$

### Example 2: Airy's equation

Airy's equation is a really simple equation which pops up in many fields (quantum mechanics, optics, probability):

$$
y'' = xy
$$

We can solve it straight away by rewriting it as:

$$
\hat D^2 a_n = \hat X a_n
$$

from which, applying the operators:

$$
(n + 1) (n + 2) a_{n + 2} = a_{n - 1} \\
a_n = \frac{a_{n - 3}}{n(n - 1)}
$$

with initial conditions $y(0) = a_0$ and $y'(0) = a_1$. We can't evaluate the recurrence relation for $n = 2$. This is because multiplication by $x$ shifts the sum by $1$, leaving the first term to be $0$. This means that we should set the $a_{n-3}$ factor to $0$ and evaluate the rest of the expression, which is $0$. Hence we have:

$$
a_2 = 0 \\
\forall n > 2: \ \ a_n = \frac{a_{n - 3}}{n(n - 1)}
$$

## Integral equations

We have so far considered only differentiation and multiplication by $x$. Another common operation in calculus is integration, which appears in integral equations:

$$
\int y(x) dx = f(x, y, y', ...)
$$

We can once again try to study the effect of this operation on the power series:

$$
\int y(x)dx = \int \sum_{n = 0}^\infty a_n x^n \\
= \sum_{n = 0}^\infty a_n \frac{x^{n + 1}}{n + 1} = \sum_{n = 1}^\infty \frac{a_{n - 1}}{n} x^n + K
$$

We can then define an **integral operator**:

$$
\hat I = \hat N^{-1} \hat S^{-1}
$$

This operator integrates the series and can be used like the others to solve integral equations by series expansion. Its representation is really similar to the derivative operator, and in fact it is its inverse:

$$
\hat D^{-1} = (\hat S \hat N)^{-1} = \hat N^{-1} \hat S^{-1} = \hat I
$$

It follows immediately that:

$$
\hat D \hat I = \hat I \hat D = 1
$$

which is the **fundamental theorem of calculus** expressed using these operators. Another interesting result, which is a specific case of integration by parts, is:

$$
\hat I \hat X \hat D = \hat X - \hat I
$$

Which can be seen by rewriting it:

$$
\hat I \hat X \hat D = \hat N^{-1} \hat S^{-1} \hat S^{-1} \hat S \hat N = \\ \hat N^{-1} \hat S^{-1} \hat N = \frac{\hat N - 1}{\hat N} \hat S^{-1} \\
= S^{-1} - N^{-1}S^{-1}
$$

In the previous formulas, an important property of the integral was not considered. If we apply indefinite integration, we obtain the primitive of the integrand function plus an arbitrary constant. To account for this constant, which is an arbitrary coefficient of power $0$ in the series expansion, we can use the following notation:

$$
\hat I f(n) a_n = \frac{1}{n} f(n - 1) a_{n - 1} + K_0
$$

Where the subscript is the power in $x$ of the arbitrary constant K (which can change afterwards). Considering how $K$ changes with respect to derivation, multiplication by $x$ and integration:

$$
K x^n \rightarrow K_n \\
\hat D K_n = n K_{n - 1} \\
\hat X K_n = K_{n + 1} \\
\hat I K_n = \frac{1}{n + 1} K_{n + 1} + C_0
$$

A $K_m$ term in the final formula means that **only** for $n = m$ we should consider the arbitrary constant in the evaluation. It may be rewritten as $\delta_{mn}K_m$ for clarity.

### Example 3:

Let's consider the integral equation defined by:

$$
y = \int xy \\
\implies a_n = \hat I \hat X a_n
$$

which gives:

$$
a_n = \frac{1}{n} a_{n - 2} + K_0
$$

Given the initial condition $y(0) = a_0$ we can compute the next coefficients:

$$
a_1 = 0 \\
a_2 = \frac{1}{2} a_0 \\
a_3 = 0 \\
a_4 = \frac{1}{8} a_0 \\
...
$$

## Initial conditions and offsets
In the previous examples we didn't look into how the starting index of the sums changes when applying the operators. When the series is multiplied by $x$, no terms are constant anymore, so the sum is **offset** by $1$. The same happens when integrating, as the constant term is multiplied by $x$, with the difference that a new arbitrary constant has to be accounted for. We can introduce a new notation to keep track of this offset:

$$
\sum_{n = k}^\infty a_n x^n \rightarrow a_n^{(k)}
$$

and consider how the offset changes when applying operators:

$$
\hat X a_n^{(k)} = a_{n - 1}^{(k + 1)} \\
\hat I a_n^{(k)} = \frac{1}{n} a_{n - 1}^{(k + 1)} + K_0 \\
\hat D a_n^{(k)} = (n + 1) a_{n + 1}^{(k - 1)} \\
\hat D a_n^{(0)} = (n + 1) a_{n + 1}^{(0)}
$$

Once we have the recurrence formula for the coefficients, we start by evaluating the terms with the lowest offsets and ignoring the terms with higher offset, obtaining new formulas for each number $n$. Basically, a term $a_n^{(k)}$ means that we should ignore it up until $n = k$. For example, if the recurrence relation is given by

$$
a_n^{(0)} = \frac{1}{n} (a_{n - 1}^{(1)} - a_{n - 2}^{(2)} + a_{n - 3}^{(3)}) \\
n = 1: \ a_1 = a_0 \\
n = 2: \ a_2 = \frac{a_1 - a_0}{2} \\
n = 3: \ a_3 = \frac{a_2 - a_1 + a_0}{3} \\
...
$$

Another thing to keep in mind is that derivation removes the constant term of the series, introducing indeterminate coefficients in the formulas:

$$
\hat D a_n = (n + 1) a_{n + 1} \\
n = -1: \ (n + 1) a_{n + 1} = 0 \cdot a_0 = 0
$$

So we can't recover the value of $a_0$ from the recurrence relation. This is expected, as we need the initial conditions to solve a differential equation. What this teaches us is that derivation introduces forms of indetermination of the coefficients which are constitutive and not pathological.

We may use the previous notation to keep track of the offset, but it really is additional bookkeeping, as we can instead set $a_k = 0 \ \ \forall k < 0 $ and evaluate the rest of the expression. This ensures that we ignore terms which do not appear in the full series expansion only by considering the already available information given by the index. When we get a division by $0$, it means that the coefficient is indeterminate and should be given as initial condition. For example, in the solution of Airy's equation:

$$
a_n = \frac{a_{n - 3}}{n(n - 1)}
$$

for $n = 0$ and $n = 1$ we get a division by $0$, which means $a_0$ and $a_1$ should be given as initial conditions. For $n = 2$ we can evaluate the rest of the expression, but $a_{-1} = 0$, so we get $a_2 = 0$.

## Non-polynomial coefficients
So far we considered only constant or polynomial coefficients in front of $y$ (basically powers of $\hat X$), but we may want to solve more general differential equations. The most straight forward approach is to try to expand the function of $x$ as a Taylor series in the $\hat X$ operator. For example:

$$
y' = e^x y \ \rightarrow \ \hat D a_n = e^{\hat X} a_n \\
= \sum_{k = 0}^\infty \frac{\hat X^k}{k!}a_n = \sum_{k = 0}^\infty \frac{1}{k!} a_{n - k} \\
a_{n + 1} = \frac{1}{n + 1} \sum_{k = 0}^\infty \frac{1}{k!} a_{n - k} \\
a_n = \frac{1}{n} \sum_{k = 0}^\infty \frac{1}{k!} a_{n - 1 - k}
= \frac{1}{n} \sum_{k = 0}^{n - 1} \frac{1}{k!} a_{n - 1 - k}
$$

After the previous considerations, this means that we get an infinite set of equations, with the right hand side being an infinite series which we should evaluate only for the terms so that $k < n - 1$ for a given $n$. This gives:

$$
a_1 = a_0 \\
a_2 = \frac{1}{2} (a_0 + a_1) = a_0 \\
a_3 = \frac{1}{3} (a_2 + a_1 + \frac{1}{2} a_0) = \frac{5}{6} a_0 \\
...
$$

Provided we can expand the variable coefficients as a Taylor series which converges over the interval of resolution, we can still find recurrence relations. The only difference is that now we have an infinite set of equations instead of a finite one, although we can still compute the coefficients iteratively.

The solution to this differential equation is actually known and is $y = e^{e^x}$. We can look at the Taylor expansion of the solution:

$$
y(x) = \sum_{n = 0}^\infty \frac{1}{n!}(\sum_{k = 0}^\infty \frac{x^k}{k!} )^n
$$

which doesn't tell us much about our own solution. We can instead compare the result using the series expansion method:

$$
\sum_{n = 0}^\infty (n + 1) a_{n + 1} x^n = \sum_{k = 0}^\infty \frac{x^k}{k!} \sum_{n = 0}^\infty a_n x^n \\
= \sum_{n = 0}^{\infty} \sum_{k = 0}^n a_k x^k \frac{x^{n - k}}{(n - k)!} \\
= \sum_{n = 0}^{\infty} \sum_{k = 0}^n a_k \frac{x^n}{(n - k)!}
$$

where Cauchy's product formula for series was used. This equation gives:

$$
a_1 + 2 a_2 x + 3a_3 x^2 + \ ... \ \\
= a_0 + x (a_0 + a_1) + x^2 (\frac{a_0}{2} + a_1 + a_2) + \ ...
$$

Equating terms with the same degree, we get the previous coefficients, so our previous solution was correct.

### Example 4: Sinusoidal coefficient

Let's apply the lesson we just learned to another problem:

$$
y' = sin(x) \cdot y
$$

We expand the sine as a Taylor series and apply the operators:

$$
a_{n + 1} = \frac{1}{n + 1} sin(\hat X) a_n \\
= \frac{1}{n + 1} \sum_{k = 0}^\infty (-1)^k \frac{\hat X^{2k + 1}}{2 k + 1} a_n \\
= \frac{1}{n + 1} \sum_{k = 0}^\infty (-1)^k \frac{\hat X^{2k + 1}}{2 k + 1} a_n \\
a_n = \frac{1}{n} \sum_{k = 0}^{n/2 - 1} \frac{(-1)^k}{(2k + 1)!} a_{n - 2k - 2}
$$


## Non-homogeneous differential equations
Another important case is when the differential equation is not homogeneous:

$$
y^{(k)} = f(x, y, y', ...) + g(x)
$$

We can try again to expand the function as a Taylor series, but this time the function does not act on $y$, it is another term entirely. This means that we should consider the coefficients in front of $x^n$ in the Taylor expansion when evaluating the recurrence relation for a given $n$:

$$
g(x) = \sum_{n = 0}^\infty g_n x^n \\
\hat D^k a_n = F(n, a_{g(n)}) + g_n
$$

### Example 5:

Let's consider the non-homogeneous differential equation:

$$
y'' + y' = 2 \sinh(x)\\
\hat D^2 a_n + \hat D a_n = \frac{1}{n!} - (-1)^n \frac{1}{n!} \\
a_{n + 2} = -\frac{1}{n + 2} a_{n + 1} + \frac{(1 - (-1)^n)}{n!(n +1)(n+2)} \\
a_n = - \frac{1}{n} a_{n - 1} + \frac{1}{n!}\frac{(1 - (-1)^n)}{n(n - 1)}
$$

where the second term is non-zero only for even powers of $n$:

$$
a_{2n} = - \frac{1}{2n} a_{2n - 1} \\
a_{2n + 1} = -\frac{1}{2n + 1} a_{2n} + \frac{1}{(2n + 1)!} \frac{1}{n(2n + 1)}
$$

## Wrapping this all together
After defining these operators and rules, we can effectively solve many ODEs by series expansion with little effort. All we have to do is rewrite the equation using the new operators and evaluate the expression to get the recurrence relation:

$$
y^{(k)} = f(x, y, y', ...) \rightarrow \ \hat D^k a_n = F(n, a_{g(n)})
$$

by using the following mapping:

$$
y \rightarrow a_n \\
\frac{d}{dx} \rightarrow \hat D, \ \ x \rightarrow \hat X, \ \ \int \rightarrow \hat I
$$

We can also derive the general form of the solution of a $k$-th order differential equation:

$$
\hat D^k a_n = F(n, a_{g(n)}) \\
\frac{(n + k)!}{n!} a_{n + k} = F(n, a_{g(n)}) \\
\hat S^{-k} [a_{n + k}] = \hat S^{-k} [\frac{n!}{(n + k)!} F(n, a_{g(n)})] \\
a_n =  \frac{(n - k)!}{n!} \hat S^{-k} [F(n, a_{g(n)})]
$$

This general formula for a differential equation in the given form can be easily applied to obtain a recurrence relation with little effort.

### Example 6: Bessel's differential equation

Bessel's equation is an important mathematical result which finds applications in many areas of physics, starting from the vibrations of a string with variable thickness and tension to solutions of Laplace's  and Hemlholtz's equations. Here is the Bessel equation of order $0$:

$$
x^2 y'' + x y' + x^2 y = 0 \\
$$

We can rewrite it in this new formalism and solve it with ease:

$$
\hat X^2 \hat D^2 a_n + \hat X \hat D a_n + \hat X^2 a_n = 0 \\
n(n - 1) a_n + n a_n + a_{n - 2} = 0 \\
a_n = -\frac{a_{n - 2}}{n^2}
$$

Considering that $a_1 = 0$, all even coefficients are zero, so the general formula is:

$$
a_{2n} = (-1)^n \frac{a_0}{4^n (n!)^2}
$$

## Conclusion
I derived these results on my own, as I was reflecting on the mechanical nature of series expansions, so they should be taken with a grain of salt. I am confident that similar results have already been found, although I wasn't able to find existing literature on the topic. This formalism proves really useful for the solution of ODEs, although nonlinear differential equations are not tractable with this method. Numerical applications will be investigated in future articles, as well as a more rigorous formalization of the results and other forms of series expansion.

