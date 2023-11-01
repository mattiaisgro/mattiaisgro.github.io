---
title: 'The Generalized Euler-Lagrange Equation'
date: 2023-11-01
permalink: /posts/2023/11/generalized-euler-lagrange/
tags:
  - maths
  - classical mechanics
  - classical field theory

abstract: "The generalized Euler-Lagrange equation is derived in the context of classical mechanics and classical field theory through the principle of stationary action. The physical relevance of the formula is briefly discussed."
---

_Abstract:_ The generalized Euler-Lagrange equation is derived in the context of classical mechanics and classical field theory through the principle of stationary action. The physical relevance of the formula is briefly discussed.

_Prerequisites:_ Classical Mechanics, Classical Field Theory, Tensor Calculus


## The first order Euler-Lagrange equation

One of the most important equations in any classical mechanics course is surely the Euler-Lagrange equation, stated in one coordinate $q$ as:

$$
\frac{d}{dt} \frac{\partial L}{\partial \dot q} - \frac{\partial L}{\partial q} = 0
$$

This equation can be derived from the principle of stationary action and is a cornerstone of physics and a fundamental equation in the calculus of variations. In this context, it is the differential equation whose solutions make a given *functional* stationary:

$$
\delta I = \int \delta +L(q, \dot q) \ dt = 0
$$

It is important to note that the Euler-Lagrange equation (in this form) can only work for a functional with explicit dependency up to the first derivative, as it doesn't take into account higher derivatives. It is the objective of this article to derive higher order formulas and consider the applicability of such models. This limitation is usually not a problem in classical mechanics, where systems are commonly first order, as the Lagrangian and the energy do not depend on the acceleration but only on positions and velocities. We can easily derive the Euler-Lagrange equation for the Lagrangian by exchanging the time derivative from $\delta q$ to the partial derivative in $L$ (at first order in the expansion):

$$
\delta I = \delta \int L(q, \dot q) dt = \int \delta L \ dt \\
\delta L = L(t, q + \delta q, \dot q + \delta \dot q) - L(t, q, \dot q) = \\
= \frac{\partial L}{\partial q} \delta q + \frac{\partial L}{\partial \dot q} \delta (\dot q) = \frac{\partial L}{\partial q}\delta q + \frac{\partial L}{\partial \dot q} (\frac{d}{dt} \delta q)
$$

Substituting the equivalence from the derivative of the product (the variation and the derivative commute):

$$
\frac{\partial L}{\partial \dot q} (\frac{d}{dt} \delta q) = \frac{d}{dt} (\frac{\partial L}{\partial \dot q} \delta q) - \frac{d}{dt} \frac{\partial L}{\partial \dot q} \delta q
$$

We have:

$$
\delta L = \frac{\partial L}{\partial q} \delta q + \frac{d}{dt} (\frac{\partial L}{\partial \dot q} \delta q) - \frac{d}{dt} \frac{\partial L}{\partial \dot q} \delta q
$$

When integrating with the extremes fixed and vanishing variations on the boundary ($\delta q(t_a) = \delta q(t_b) = 0$):

$$
\int_{t_a}^{t_b} \frac{d}{dt} (\frac{\partial L}{\partial \dot q} \delta q) dt = \frac{\partial L}{\partial \dot q}(t_b) \delta q(t_b) - \frac{\partial L}{\partial \dot q}(t_a) \delta q(t_a) = 0
$$

The resulting formula is:

$$
\int dt (\frac{\partial L}{\partial q} - \frac{d}{dt} \frac{\partial L}{\partial \dot q}) \delta q = 0
$$

Considering that this equation must hold for all variations $\delta q$, we can deduce that:

$$
\frac{\partial L}{\partial q} - \frac{d}{dt} \frac{\partial L}{\partial \dot q} = 0
$$


## Second order derivatives

When confronted with a problem of higher order, we need a more advanced formula to correctly solve it. Consider for example the functional:

$$
I = \int dt (q^2 - \ddot q^2)
$$

We want to make this functional stationary, but the Euler-Lagrange equation does not give us enough information on how to solve it. We can repeat the whole process of making the functional stationary, this time taking into account a dependence on second order derivatives:

$$
\delta I = \int \delta L(q, \frac{dq}{dt}, \frac{d^2q}{dt^2}) dt = 0
$$

$$
\delta L = \frac{\partial L}{\partial q} \delta q + \frac{\partial L}{\partial \dot q} (\frac{d}{dt} \delta q) + \frac{\partial L}{\partial \ddot q} (\frac{d^2}{dt^2} \delta q)
$$

The last term can be reduced to a function multiplied by $\delta q$, by repeating the same process used before:

$$
\frac{\partial L}{\partial \ddot q} (\frac{d^2}{dt^2} \delta q)= \frac{d}{dt} (\frac{\partial L}{\partial \ddot q} (\frac{d}{dt} \delta q)) - (\frac{d}{dt} \frac{\partial L}{\partial \ddot q}) (\frac{d}{dt} \delta q)
$$

We reiterate the same process to move the time derivative:

$$
(\frac{d}{dt} \frac{\partial L}{\partial \ddot q})(\frac{d}{dt} \delta q) = \frac{d}{dt} (\frac{d}{dt} \frac{\partial L}{\partial \ddot q} \delta q) - (\frac{d^2}{dt^2} \frac{\partial L}{\partial \ddot q}) \delta q
$$

Substituting in the previous equations, we obtain:

$$
\delta L = \frac{\partial L}{\partial q} \delta q + \frac{d}{dt} (\frac{\partial L}{\partial \dot q} \delta q) - \frac{d}{dt} \frac{\partial L}{\partial \dot q} \delta q + \frac{d}{dt} (\frac{\partial L}{\partial \ddot q} (\frac{d}{dt} \delta q)) \\ - \frac{d}{dt} (\frac{d}{dt} \frac{\partial L}{\partial \ddot q} \delta q) + (\frac{d^2}{dt^2} \frac{\partial L}{\partial \ddot q}) \delta q
$$

All terms which are a total derivative vanish when integrating (supposing that $\delta q$ and $\delta \dot q$ are zero at the extremes):

$$
\delta I = \int dt (\frac{\partial L}{\partial q} - \frac{d}{dt} \frac{\partial L}{\partial \dot q} + \frac{d^2}{dt^2} \frac{\partial L}{\partial \ddot q}) \delta q = 0
$$

From which we get:

$$
\frac{\partial L}{\partial q} - \frac{d}{dt} \frac{\partial L}{\partial \dot q} + \frac{d^2}{dt^2} \frac{\partial L}{\partial \ddot q} = 0
$$

Going back to our previous problem, we can apply our new formula:

$$
L = q^2 - \ddot q^2 \\
\frac{\partial L}{\partial q} = 2q, \ \frac{\partial L}{\partial \dot q} = 0, \ \frac{\partial L}{\partial \ddot q} = -2 \ddot q
$$

Applying the derivative to the last term and summing up we get:

$$
2q - 2 \frac{d^4}{dt^4} q = 0
$$

So the function we are searching for is the solution to the differential equation:

$$
q^{(4)} = q
$$

Which in general is:

$$
q(t) = A \sin (t) + B \cos (t) + C e^x + D e^{-x}
$$

## The generalized Euler-Lagrange equation
The previous proof for the second order formula was pretty straightforward, considering that we only repeated the same process of moving the time derivative from $\delta q$ to act on $\partial L / \partial \ddot q$. The only difference in the new formula is that a new term is added, with second order derivatives with respect to time. We can reiterate the same process over and over again for higher order derivatives, keeping in mind that every time we move the derivative, we must multiply by $-1$. This is a more general property of integration by parts whenever the total derivative vanishes at the boundaries (which is the case if $\delta q$ and the various $\delta q^{(j)}$ are zero at the extremes):

$$
\int a (\frac{d^n}{dx^n} b) dx = - \int (\frac{d}{dx} a)(\frac{d^{n-1}}{dx^{n-1}} b) dx = + \int (\frac{d^2}{dx^2} a)(\frac{d^{n-2}}{dx^{n-2}} b) dx
$$

After reiterating the same process $n$ times, we get:

$$
\int a (\frac{d^n}{dx^n} b) dx = (-1)^n \int b(\frac{d^n}{dx^n} a) dx
$$

This same result is used when dealing with distributions and weak solutions of PDEs. We can now apply this formula to the $n$-th term of the variation of the Lagrangian:

$$
\int \frac{\partial L}{\partial q^{(n)}} \delta q^{(n)} dt = (-1)^n \int dt \ \delta q\frac{d^n}{dt^n} \frac{\partial L}{\partial q^{(n)}}
$$

Let's consider a Lagrangian which explicitly depends on time derivatives of $q$ up to the $n$-th derivative and compute the variation of its action:

$$
\int \delta L \ dt = \int dt \ \delta q [\frac{\partial L}{\partial q} - \frac{d}{dt} \frac{\partial L}{\partial \dot q} + \ ... \ + \ (-1)^n \frac{d^n}{dt^n} \frac{\partial L}{\partial q^{(n)}}] = 0
$$

We can rewrite the whole formula as a sum of all the terms of different order (the "zero-th" derivative being the identity):

$$
\int dt \ \delta q \sum^n_{i = 0} (-1)^n \frac{d^n}{dt^n} \frac{\partial L}{\partial q^{(n)}}
$$

Equating to zero and considering that it must be true for all variations $\delta q$ we finally have the *generalized Euler-Lagrange* equation:

$$
\sum^n_{i = 0} (-1)^n \frac{d^n}{dt^n} \frac{\partial L}{\partial q^{(n)}} = 0
$$

For $n = 1$ we get back the familiar formula of classical mechanics, as expected. Equipped with this formula, we can consider functionals with dependence on derivatives of any order. An example of a higher order Lagrangian is the Pais-Uhlenbeck oscillator$^1$:

$$
L = \frac{1}{2} \gamma [\ddot q^2 - (\omega_1^2 - \omega_2^2) \dot q ^2 + \omega_1^2\omega_2^2 q^2]
$$

The difficulty in the usage of higher order Lagrangians comes from the fact that the $n$-th order term in the Lagrangian corresponds to a $2n$-th order term in the equations of motion, because the partial derivative with respect to $q^{(n)}$ is differentiated $n$ times with respect to time. This means that the simplest higher order Lagrangian containing $\ddot q$ has fourth order equations of motion in $q^{(4)}$. Other problems arise when trying to quantize systems of higher order, like the Pais-Uhlenbeck oscillator itself.

## Field theories of higher order

The Lagrangian formulation of classical mechanics can be extended to theories with infinite degrees of freedom, giving rise to classical field theories. The time derivative is substituted by the four-derivative $\partial_\mu$ and the Lagrangian is substituted by the *Lagrangian density* $\mathscr{L}$, the resulting equation reads:

$$
\frac{\partial \mathscr{L}}{\partial \phi} - \partial_\mu \frac{\partial \mathscr{L}}{\partial (\partial_\mu \phi)} = 0
$$

Where Einstein summation is used. We now want to generalize this equation like before to find the arbitrary-order Euler-Lagrange equation for fields. The first order formula can be derived just like before by making the action stationary, except this time the action is defined as:

$$
I = \int dt \int d^3x \mathscr{L} = \int d^4x \mathscr{L}
$$

Since $\mathscr{L}$ is a density. Let's compute the contribution to the variation of the action of the $n$-th order derivative of the field $\phi$:

$$
\int d^4x \frac{\partial \mathscr{L}}{\partial (\partial_{\mu_1} \partial_{\mu_2} ... \partial_{\mu_n} \phi)} \delta (\partial_{\mu_1} \partial_{\mu_2} ... \partial_{\mu_n} \phi)
$$

Like before, we can exchange the variation operation and the derivatives and then move the derivatives to the other part of the equation:

$$
(-1)^n \int d^4x \ \delta \phi \ \partial_{\mu_1} \partial_{\mu_2} ... \partial_{\mu_n}  \frac{\partial \mathscr{L}}{\partial (\partial_{\mu_1} \partial_{\mu_2} ... \partial_{\mu_n} \phi)}
$$

This formula is correct as long as the variation of $\phi$ and the variation of its derivatives up to order $n - 1$ vanish at the boundaries. Keep in mind that each index $\mu_i$ is summed over and the result is a scalar. The complete formula for the variation of the action of a Lagrangian density with explicit dependency on the $n$-th derivatives of $\phi$ is then:

$$
\int d^4x \ \delta \mathscr{L}(\phi, \partial_{\mu_1}\phi,  \ ..., \ \partial_{\mu_1} ...\partial_{\mu_n}\phi) = \\
\int d^4x \ \delta q \ (\frac{\partial \mathscr{L}}{\partial \phi} + \ ... \ + (-1)^n\partial_{\mu_1} ... \partial_{\mu_n} \frac{\partial \mathscr{L}}{\partial_{\mu_1} ... \partial_{\mu_n} \phi})
$$

As before, we may want to simplify this formula down to a sum, but this time we need to consider the sums on the contracted indices $\mu_i$. To this purpose, we may define a differential operator which computes the $n$-th order derivatives using tensor notation:

$$\Delta^n_{\mu} = \prod_{j = 0}^n \partial_{\mu_j} \\
\Delta^0_{\mu} = 1$$

The subscript $\mu$ is needed to keep track of the **family of indices** which are then contracted in the complete formula. Using this differential operator we may rewrite the previous formula for the action as:

$$
\int d^4x \ \delta \phi \sum_{i = 0}^n (-1)^i \Delta^i \frac{\partial \mathscr{L}}{\partial (\Delta^i_{\mu} \phi)}
$$

Equating this to zero to make the action stationary, we obtain the *generalized Euler-Lagrange equation* for classical field theory:

$$
\sum_{i = 0}^n (-1)^i \Delta^i_{\mu} \frac{\partial \mathscr{L}}{\partial (\Delta^i_{\mu} \phi)} = 0
$$

By using the $\Delta^n_{\mu}$ differential operator we are able to abstract away the different indices to recover a formula in the same form of the previous one. Keep in mind that this new formula is significantly more complex when the series is expanded, as each four-derivative corresponds to 4 derivative operations and the indices are summed over.

## Locality and higher order derivatives

A key property of theories of interest in physics is locality. The idea is that, following the postulates of relativity, events happening in spacetime cannot instantly propagate. This means that a change in some variable at a given point in spacetime can only affect the immediate neighborhood. In practice, we do not want any terms in the Lagrangian to depend on different spacetime coordinates separated by space-like intervals. An example of a nonlocal term is:

$$
\mathscr{L} = \phi(x + d)
$$

This would mean that the dynamics of the field at $x$ are instantly determined by the state of the field at $x + d$. To see how this is related to higher order derivatives, we can introduce a *shift operator*:

$$
e^{d \partial_x} = \sum_{n = 0}^\infty \frac{1}{n!} d^n \frac{\partial^n}{\partial x^n}
$$

The action of this operator is to evaluate the field at a displaced position in spacetime:

$$
e^{d \partial_x} \phi(x) = \phi(x + d) \\
\mathscr{L} = \sum_{n = 0}^\infty \frac{d^n}{n!} \frac{\partial^n \phi(x)}{\partial x^n} = \phi(x) + d \frac{\partial \phi}{\partial x} +	\frac{1}{2} d^2 \frac{\partial^2 \phi}{\partial x^2} + \ ...
$$

From the series expansion of the operator we can see that by having **infinite many derivatives** in the Lagrangian, we might get a **nonlocal** term. On the other hand, Lagrangians with a *finite* number of higher order derivatives are still of interest, although as the order increases, we need more and more initial conditions to solve for the field dynamics.

## Ostrogradskij instability
Another concerning problem of higher order Lagrangians is evidenced by Ostrogradskij's theorem, which states that any Lagrangian with finite higher order terms $q^{(j)}$, provided that it is **not degenerate** in the highest order derivatives ($\det (\partial^2 \mathscr{L}/\partial q^{(n)}_i \partial q^{(n)}_j) \neq 0$), has a corresponding Hamiltonian which is not bounded from below. This is caused by the fact that the phase space is of greater dimension and the resulting Hamiltonian is **linear** in one of the momenta of the system$^{2, 3}$. For a system with second order derivatives:

$$H = \mathbf{P_1 Q_2} + P_2 f(Q_1, Q_2, P_2) - L(Q_1, Q_2, P_2)$$

Where the momenta can be defined in a novel way, using a Lagrange multiplier, to be (with $Q_1 = q$, $Q_2 = \dot q$):

$$P_1 = \frac{\partial L}{\partial \dot Q_1} - \frac{d}{dt} \frac{\partial L}{\partial \dot Q_2} \\
P_2 = \frac{\partial L}{\partial \dot Q_2}$$

This instability poses serious problems in the **quantization** of higher order systems, often leading to arbitrarily negative energy levels and negative norms$^4$. A system with infinite negative energy states makes it possible for coupled systems to exchange energy indefinetely, while still having conservation of energy. It should be noted that the Ostrogradskij theorem applies only to non-degenerate Lagrangians with finite order derivatives (although infinite higher order derivatives are not usually desirable as previously explained), and there exist ways to obtain a stable Hamiltonian from a Lagrangian of higher order using constraints to get rid of the terms which are linear in the momenta.


## Bibliography

1. Mannheim, P. D., & Davidson, A. (2005). Dirac quantization of the Pais-Uhlenbeck fourth order oscillator. Physical Review A, 71(4). https://doi.org/10.1103/physreva.71.042110
2. Svanberg, E (2022). Theories with higher-order time derivatives and the Ostrogradsky ghost. Stockholms Universitet
3. Smilga, A. (2005). Benign vs. malicious ghosts in higher-derivative theories. Nuclear Physics B, 706(3), 598–614. https://doi.org/10.1016/j.nuclphysb.2004.10.037
4. Motohashi, H., & Suyama, T. (2020). Quantum Ostrogradsky theorem. Journal of High Energy Physics, 2020(9). https://doi.org/10.1007/jhep09(2020)032