---
title: 'Dual Algebras and Automatic Differentiation'
date: 2023-03-08
permalink: /posts/2023/03/dual-algebras-autodiff/
tags:
  - maths
  - autodiff

abstract: "This is a short introduction to dual algebras and their computational application for automatic differentiation"
---

_Abstract:_ This is a short introduction to dual algebras and their computational application for automatic differentiation.

_Prerequisites:_ Calculus


Different approaches to differentiation
------
An all-encompassing problem in science and mathematics is the computation of derivatives. There are three main families of computational techniques to evaluate the derivative of a function:
  - Symbolic
  - Numerical
  - Automatic

Symbolic differentiation works by considering the function as a composition of symbols, usually converted from a string of characters written by a user, and successively applying derivation rules on the symbols, giving as result a symbolic representation of the derivative of the function. This method is useful when such a result is needed for further study but may not be immediate to obtain by hand. For example, in a hypothetical symbolic representation:

$$
f(x) = x^2 e^x \ \stackrel{symbol}{\rightarrow} \  mul(pow(x, 2), exp(x)) \\
\stackrel{\frac{d}{dx}}{\rightarrow} \ sum(mul(mul(2, x), exp(x)), mul(pow(x, 2), exp(x))) \\
\stackrel{string}{\rightarrow} \ 2x e^x + x^2 e^x
$$

This process gives back the exact formula for the derivative but is more computationally demanding, especially if the only interest is to evaluate the derivative at few points.

Numerical differentiation works by approximating the derivative of the function at a given point, evaluating certain points to estimate the slope of the tangent. The simplest way to achieve this is to use the mathematical definition of derivative and using a finite value for the variation (hence the name *"finite differences"*), to obtain the central difference method, for example:

$$
\frac{df}{dx}(x_0) \approx \frac{f(x_0 + h) - f(x_0 - h)}{2h}
$$

Rounding error usually dominates the accuracy of the method, because of catastrophic cancellation. A refinement of this idea is Ridder's method, which uses more evaluations of the function to get a better result (an implementation is available in [Theoretica](https://github.com/chaotic-society/theoretica/blob/master/src/calculus/derivation.h) as *deriv_ridders2*). This class of methods is faster but is only an approximation and is not always reliable.

Automatic differentiation is a distinct approach which evaluates the function in a special way giving an exact result, without considering the function's symbolic representation. There are two categories of automatic differentiation, **forward** and **backward**. They are both valuable, but in this article I will discuss a possible construction of methods of the first category, leaving backward differentiation for a future post.

Dual algebras
------
Complex numbers are usually introduced by defining $i^2 = -1$ and considering its mathematical consequences. For instance, we can find how complex addition, multiplication and division work. After some calculations we can even arrive at Euler's identity, $e^{iz} = \cos(z) + i\sin(z)$.

Following a similar idea, we can start from the *Ansatz* :

$$
\epsilon^2 = 0
$$

(It can be demonstrated that the only interesting cases with power 2 are $k^2 \in \{-1, 0, 1\}$, where $k$ is the new basis element $i$, $\epsilon$ or $j$, giving rise to imaginary, dual or hyperbolic numbers)

Considering a number $z = a + \epsilon b$ and $w = c + \epsilon d \ $ ($a, b, c, d \in \mathbb{R}$), we can compute its multiplication rules:

$$
z \cdot w = (a + \epsilon b) \cdot (c + \epsilon d) = ac + \epsilon bc + \epsilon ad = ac + \epsilon (bc + ad)
$$

It's interesting how the real part of the result is just the multiplication of the real parts of the starting numbers, while the "new" part of the result **mixes** the components. How about division? Can we compute it like with complex numbers?

$$
\frac{a + \epsilon b}{c + \epsilon d} = \frac{a + \epsilon b}{c + \epsilon d} \cdot \frac{c - \epsilon d}{c - \epsilon d} = \frac{ac + \epsilon (bc - ad)}{c^2} = \frac{a}{c} + \epsilon \frac{bc - ad}{c^2}
$$

We see that it works unless $c = 0$, so we can't divide by a "pure" dual number. The formula we obtain is suspisciouly similar to another important equation.

Let's try to exponentiate this new kind of number:

$$
e^{\epsilon z} = \sum_{n=0}^{\infty} \frac{1}{n!} \epsilon^n z^n = 1 + \epsilon z
$$

The series is **truncated** because $\epsilon^n = 0$ for any $n \geq 2$. Adding a real part to the exponential gives:

$$
e^{x + \epsilon b} = e^x + \epsilon b e^x
$$

This should begin to give away something about the way this algebra works... Let's see what happens if we feed these new numbers to a function and compute its Taylor expansion with respect to the "new" component $\epsilon$ :

$$
f(x + \epsilon b) = \sum_{n=0}^{\infty} \frac{\epsilon^n b^n}{n!} \frac{d^n}{dx^n} f(x) = f(x) + \epsilon b \frac{d}{dx} f(x)
$$

The series is again truncated and we clearly see that for $b = 1$, the real part of the result is just the function evaluated at $x$ and what we will now call its **dual** part is the derivative of $f$ at $x$.

How about function composition? Remembering that $f(x + \epsilon b) = f(x) + \epsilon b f'(x)$:

$$
f(g(x + \epsilon)) = f(g(x) + \epsilon g'(x)) = f(g(x)) + \epsilon g'(x) f'(g(x))
$$

The dual part is just the chain rule for the derivative of function composition! It is now clear that this new algebra behaves exactly like the derivative, keeping the primitive function in the real "slot" and its derivative in the dual "slot". The intuition behind evaluating the function at $x + \epsilon$ is that this dual number corresponds to $x$ with its derivative $1$ as dual part. Other properties of the derivative can be easily demonstrated:

$$
a \cdot f(x + \epsilon) = a (f(x) + \epsilon f'(x)) = a f(x) + \epsilon a f'(x) \\
f(x + \epsilon) \pm g(x + \epsilon) = f(x) \pm g(x) + \epsilon(f'(x) \pm g'(x)) \\
f(x + \epsilon) \cdot g(x + \epsilon) = f(x)g(x) + \epsilon (f'(x) g(x) + f(x) g'(x))
$$

Thus by evaluating any regular function with a dual variable, we obtain its value and its derivative at any (non-singular) given point. The validity of dual numbers is quickly evident by considering polynomials: $f(z) = 3 z^3 + 5 z^2 + 2 z \in P[\mathbb{R}_{\epsilon}]$ (dual numbers are often labeled $\mathbb{R}_{\epsilon}$), $f(x + \epsilon) = 3 x^3 + 5 x^2 + 2 x + \epsilon (9 x^2 + 10 x + 2)$. This result depends only on the multiplication rule we have found.

Automatic differentiation
------

After all of these formulas, this may appear as yet another mathematical abstraction, but it's quite the opposite. We can program a class (or generic construct) following the rules of this dual algebra in any programming language and define common mathematical functions to operate on such numbers, getting as result of our computations the value of the function at a given point and its derivative, at the same time!

```cpp
class dual {

	real a, b;
    
    ...
}

dual sqrt(dual x) {
	return dual(sqrt(x.a), epsilon * x.b / (2 * sqrt(x.a)));
}

dual f(dual x) {
	return x * x * sqrt(x);
}

real df(real x) {
	return f(x + epsilon).b;
}
```

All we have to do is evaluate the target function at $x + \epsilon$, for any $x$ we want, and we automatically get the (hoping no cosmic ray bursts into our laptop) correct result. Automatic differentiation is thus a powerful middle ground between symbolic and numerical differentiation.

Dual numbers have been extensively developed in [Theoretica](https://www.github.com/chaotic-society/theoretica). The *dual.h* and *dual_functions.h* files include a complete implementation of the ideas inside this post. Other files in the *autodiff* folder implement more advanced algebras which I will cover in future posts.

Additional notes
------
- A matrix representation of this dual algebra is, for $z = a + \epsilon b$: $\begin{pmatrix} a & b \\ 0 & a \end{pmatrix}$
- It is also possible to construct n-order dual algebras which compute the n-th derivative, using the *Ansatz* : $\epsilon^n = 0$ (but new rules have to be added).
- Dual numbers and their generalizations find applications in physics, for the study of fermions for example.