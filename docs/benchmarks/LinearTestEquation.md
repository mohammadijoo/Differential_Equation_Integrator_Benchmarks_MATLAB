# Linear Decay / Dahlquist Test Equation

## Equation

The scalar linear test equation, often called the Dahlquist test equation, is

$$ \frac{dx}{dt}=\lambda x, \qquad x(0)=x_0, $$

or, using the compact ODE notation,

$$ x' = \lambda x. $$

Here $x(t)$ is the scalar state and $\lambda$ is a constant parameter. In numerical analysis, $\lambda$ is allowed to be real or complex because the modes of a linearized multidimensional system are governed by eigenvalues, and eigenvalues may be complex.

This equation looks extremely simple, but it is one of the most important equations in numerical ODE theory. The reason is that many nonlinear systems behave locally like linear systems after linearization. If a nonlinear system is written as

$$ \dot{x}=f(x), $$

and $x^\ast$ is an equilibrium satisfying

$$ f(x^\ast)=0, $$

then small perturbations $\eta=x-x^\ast$ satisfy approximately

$$ \dot{\eta}=J_f(x^\ast)\eta, $$

where $J_f(x^\ast)$ is the Jacobian matrix of $f$ at the equilibrium. If the Jacobian has an eigenvalue $\lambda_i$, then the corresponding modal component behaves like

$$ \dot{z}_i = \lambda_i z_i. $$

So the scalar test equation is the basic building block for understanding stability, decay, growth, stiffness, and numerical amplification.

### Exact analytical solution

The equation is separable:

$$ \frac{dx}{dt}=\lambda x. $$

For $x\neq 0$,

$$ \frac{1}{x}\frac{dx}{dt}=\lambda. $$

Integrating with respect to time gives

$$ \ln |x(t)| = \lambda t + C. $$

Therefore,

$$ x(t)=C_1 e^{\lambda t}. $$

Using the initial condition $x(0)=x_0$,

$$ x_0=C_1 e^0=C_1, $$

so the exact solution is

$$ x(t)=x_0 e^{\lambda t}. $$

This formula is the reference solution used to judge numerical behavior.

### Meaning of the lambda parameter

If $\lambda$ is real, there are three basic cases.

If

$$ \lambda < 0, $$

then

$$ \lim_{t\to\infty} x_0 e^{\lambda t}=0. $$

The solution decays exponentially. This is the most common version used in stability tests.

If

$$ \lambda = 0, $$

then

$$ x(t)=x_0, $$

so the solution is constant.

If

$$ \lambda > 0, $$

then

$$ |x(t)|=|x_0|e^{\lambda t} $$

grows exponentially, and the continuous problem itself is unstable.

If $\lambda$ is complex, write

$$ \lambda = \alpha + i\beta. $$

Then

$$ x(t)=x_0 e^{(\alpha+i\beta)t} =x_0 e^{\alpha t}e^{i\beta t}. $$

Using Euler's formula,

$$ e^{i\beta t}=\cos(\beta t)+i\sin(\beta t). $$

So $\alpha$ controls exponential growth or decay, while $\beta$ controls oscillation. For example:

- $\alpha < 0$ gives damped oscillation,
- $\alpha = 0$ gives pure oscillation,
- $\alpha > 0$ gives growing oscillation.

### Stability of the continuous equation

For the continuous ODE,

$$ x(t)=x_0e^{\lambda t}. $$

The equilibrium $x=0$ is asymptotically stable if and only if

$$ Re(\lambda)<0. $$

It is neutrally stable for pure imaginary $\lambda$ and unstable if

$$ Re(\lambda)>0. $$

This simple condition becomes the reference against which numerical methods are compared. A good numerical method should reproduce the qualitative behavior of the continuous solution. If the exact solution decays, the numerical solution should also decay. If the exact solution remains bounded, the numerical solution should not artificially blow up.

### Numerical amplification factor

For a one-step numerical method with step size $h$, the numerical approximation is written as

$$ x_n \approx x(t_n), \qquad t_n=nh. $$

When a one-step method is applied to the linear test equation, the update usually takes the form

$$ x_{n+1}=R(z)x_n, $$

where

$$ z=h\lambda. $$

The function $R(z)$ is called the numerical stability function or amplification factor. The exact solution over one time step satisfies

$$ x(t_{n+1}) = e^{h\lambda}x(t_n)=e^z x(t_n). $$

Therefore the exact amplification factor is

$$ R_{exact}(z)=e^z. $$

A numerical method is trying to approximate $e^z$ by its own $R(z)$.

After $n$ steps,

$$ x_n = R(z)^n x_0. $$

The exact value at the same time is

$$ x(t_n)=e^{nz}x_0. $$

The global error is therefore

$$ e_n=x_n-x(t_n)=(R(z)^n-e^{nz})x_0. $$

This expression makes the test equation extremely useful because it separates the numerical method's behavior from the physical model.

### Absolute stability

For the decay case, assume

$$ Re(\lambda)<0. $$

Then the exact solution decays. The numerical solution will decay only if

$$ |R(z)|<1. $$

The absolute stability region of a numerical method is defined as

$$ S=\{z \in \mathbb{C}: |R(z)|\leq 1\}. $$

A method is stable for a particular step size $h$ and eigenvalue $\lambda$ if

$$ z=h \lambda \in S. $$

This is why the product $z=h\lambda$ is so important. The method does not respond to $h$ and $\lambda$ independently. It responds to their product.

### Forward Euler example

Forward Euler gives

$$ x_{n+1}=x_n+h\lambda x_n. $$

So

$$ x_{n+1}=(1+h\lambda)x_n. $$

Therefore

$$ R(z)=1+z. $$

The absolute stability condition is

$$ |1+z|\leq 1. $$

This is a disk in the complex plane centered at $-1$ with radius $1$.

For real negative $\lambda$, $z=h\lambda$ is also real and negative. The condition becomes

$$ -2\leq h\lambda \leq 0. $$

Since $\lambda<0$, this gives

$$ 0<h\leq \frac{2}{|\lambda|}. $$

This explains why explicit methods can fail on stiff decay problems. Even if the exact solution is smooth and almost zero after the fast transient, Forward Euler must use a very small step size to remain stable.

### Backward Euler example

Backward Euler gives

$$ x_{n+1}=x_n+h\lambda x_{n+1}. $$

Solving for $x_{n+1}$,

$$ (1-h\lambda)x_{n+1}=x_n, $$

so

$$ x_{n+1}=\frac{1}{1-h\lambda}x_n. $$

Thus

$$ R(z)=\frac{1}{1-z}. $$

For all $z$ with

$$ Re(z)\leq 0, $$

Backward Euler satisfies

$$ |R(z)|\leq 1. $$

This is why Backward Euler is called A-stable. It can take large stable steps on negative real decay modes. It may still be inaccurate if the step is too large, but it does not suffer the same stability restriction as Forward Euler.

### Accuracy versus stability

This equation clearly separates two ideas that beginners often confuse.

Accuracy asks:

$$ R(z) \approx e^z? $$

Stability asks:

$$ |R(z)|\leq 1? $$

A method can be stable but inaccurate. For example, Backward Euler with a very large step on a rapidly decaying mode may remain bounded, but it may overdamp the transient.

A method can also be accurate for small steps but unstable for larger steps. Forward Euler has a correct first-order Taylor approximation:

$$ e^z = 1+z+\frac{z^2}{2}+\cdots, $$

while

$$ R_{FE}(z)=1+z. $$

So Forward Euler is accurate when $|z|$ is small, but it becomes unstable when $z$ leaves its stability disk.

### Stiffness interpretation

Consider

$$ x'=\lambda x, \qquad \lambda=-1000. $$

The exact solution is

$$ x(t)=x_0 e^{-1000t}. $$

The solution decays extremely quickly. After a short time, the state is almost zero. However, Forward Euler requires

$$ h\leq \frac{2}{1000}=0.002 $$

for stability.

This means the step size is limited by stability, not by the visual smoothness of the solution. That is a key signature of stiffness.

A stiff problem is not merely a problem with a fast transient. It is a problem where stability restrictions force explicit methods to use much smaller time steps than accuracy alone would require.

### Pseudocode for the right-hand side

```text
Given state x and parameter lambda:
    dxdt = lambda * x
    return dxdt
```

For an exact reference solution:

```text
Given x0, lambda, and time t:
    x_exact = x0 * exp(lambda * t)
    return x_exact
```

### Main benchmark lesson

The scalar linear equation is the minimal model for numerical stability. It tells us how a method amplifies or damps individual modes. In a large system, every eigenmode behaves locally like a version of this equation. Therefore, if a numerical integrator fails on this simple test, it will likely fail on more complicated systems with similar eigenvalue structure.

## Implemented MATLAB file

```text
src/benchmarks/benchmark_linear_decay.m
```

## Historical background

The scalar linear test equation is the classical model for absolute stability analysis. It reveals how the product z=h*lambda controls numerical amplification.

## Mathematical properties

It is used for stability regions, convergence order, and stiff decay experiments. Real systems with locally linear stable modes often reduce to this behavior near an equilibrium.

## Why it is a benchmark

This problem is included because it exposes numerical behavior that may be hidden in simpler tests. It allows comparison of:

- accuracy,
- stability,
- stiffness handling,
- phase error,
- conservation-law drift,
- positivity or physical admissibility,
- computational cost.

## Real-world applications

Depending on the equation, applications include control systems, mechanical vibration, circuits, chemical kinetics, atmospheric dynamics, celestial mechanics, robotics, and computational physics.

## Metrics emphasized in this repository

- final error,
- maximum trajectory error,
- RMS error,
- CPU time,
- function evaluations,
- failure/blow-up status,
- invariant drift when applicable,
- qualitative plots such as phase portraits or attractor projections.

## Recommended plots

- solution versus time,
- error versus time,
- work-precision diagram,
- invariant error versus time when applicable,
- phase portrait or orbit plot when applicable.

## References

See [`../references.md`](../references.md).
