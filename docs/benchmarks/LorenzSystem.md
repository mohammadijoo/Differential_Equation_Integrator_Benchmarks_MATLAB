# Lorenz System

## Equation

The Lorenz system is a three-dimensional nonlinear autonomous ODE system:

$$ x'=\sigma(y-x), $$

$$ y'=x(\rho-z)-y, $$

$$ z'=xy-\beta z. $$

Here:

- $x(t)$, $y(t)$, and $z(t)$ are the three state variables,
- $\sigma>0$ is the Prandtl-like parameter,
- $\rho>0$ is the Rayleigh-like forcing parameter,
- $\beta>0$ is a geometric or dissipation parameter.

In vector form, define

$$ X=(x,y,z)^T. $$

Then

$$ \dot{X}=f(X)=(\sigma(y-x), x(\rho-z)-y, xy-\beta z)^T. $$

The classical chaotic parameter choice is

$$ \sigma=10, \qquad \rho=28, \qquad \beta=\frac{8}{3}. $$

### Physical and mathematical interpretation

The Lorenz system originated as a reduced model of thermal convection. In that interpretation:

- $x$ is related to convective motion intensity,
- $y$ is related to horizontal temperature variation,
- $z$ is related to vertical temperature variation.

For numerical benchmarking, the exact physical meaning is less important than the mathematical structure. The system is nonlinear, dissipative, and capable of chaotic motion. This combination makes it a useful test for short-time accuracy and long-time qualitative behavior.

### Equilibria

Equilibrium points satisfy

$$ x'=0, \qquad y'=0, \qquad z'=0. $$

From

$$ \sigma(y-x)=0, $$

we get

$$ y=x. $$

From

$$ x(\rho-z)-y=0, $$

using $y=x$, we get

$$ x(\rho-z)-x=0, $$

or

$$ x(\rho-z-1)=0. $$

From

$$ xy-\beta z=0, $$

using $y=x$, we get

$$ x^2=\beta z. $$

One equilibrium is always

$$ E_0=(0,0,0). $$

For nonzero $x$, the equation

$$ \rho-z-1=0 $$

gives

$$ z=\rho-1. $$

Then

$$ x^2=\beta(\rho-1). $$

If $\rho>1$, there are two additional equilibria:

$$ E_{\pm}=(\pm\sqrt{\beta(\rho-1)}, \pm\sqrt{\beta(\rho-1)}, \rho-1). $$

### Linearization and local behavior

The Jacobian matrix is

$$ J(x,y,z)= [-\sigma,\sigma,0; \rho-z,-1,-x; y,x,-\beta]. $$

At the origin,

$$ J(0,0,0)= [-\sigma,\sigma,0; \rho,-1,0; 0,0,-\beta]. $$

One eigenvalue is

$$ \lambda_3=-\beta. $$

The other two eigenvalues come from

$$ [-\sigma,\sigma; \rho,-1]. $$

The origin changes stability when $\rho$ passes through $1$. For $\rho<1$, the origin is stable. For $\rho>1$, the origin becomes unstable and the two nonzero equilibria appear.

This equilibrium analysis is useful, but it does not fully explain the chaotic attractor. Chaos is a global nonlinear phenomenon, not just a local eigenvalue effect.

### Dissipativity and volume contraction

The divergence of the vector field is

$$ D_f =\frac{\partial x'}{\partial x} +\frac{\partial y'}{\partial y} +\frac{\partial z'}{\partial z}. $$

Using the Lorenz equations,

$$ \frac{\partial x'}{\partial x}=-\sigma, $$

$$ \frac{\partial y'}{\partial y}=-1, $$

and

$$ \frac{\partial z'}{\partial z}=-\beta. $$

Therefore

$$ D_f=-(\sigma+1+\beta). $$

Since

$$ \sigma+1+\beta>0, $$

we have

$$ D_f<0. $$

This means infinitesimal volumes in phase space contract exponentially. If $V(t)$ is a small volume transported by the flow, then roughly

$$ V(t)=V(0)e^{-(\sigma+1+\beta)t}. $$

The system is dissipative: trajectories are eventually attracted to a lower-dimensional set. For chaotic parameters, this set is the Lorenz attractor.

### Sensitive dependence on initial conditions

The Lorenz system is famous for sensitive dependence on initial conditions. Suppose two trajectories start very close:

$$ \delta X(0)=X_a(0)-X_b(0), \qquad |\delta X(0)|\ll 1. $$

For chaotic dynamics, the separation often grows approximately like

$$ |\delta X(t)|\approx C e^{\lambda_L t}|\delta X(0)|, $$

where $\lambda_L>0$ is a positive Lyapunov exponent.

This does not mean the numerical solution is useless. It means long-time pointwise trajectory agreement is not a fair sole metric. After enough time, even two highly accurate solutions computed with tiny differences can be far apart in phase space.

Therefore, for Lorenz-type systems, one should examine:

- short-time trajectory error,
- qualitative attractor shape,
- statistical properties,
- boundedness,
- step rejection behavior,
- sensitivity to tolerances,
- phase-space projections.

### Why final-time error can be misleading

For non-chaotic systems, the error at final time

$$ |X_N-X(t_N)| $$

can be a reasonable summary. For chaotic systems, this value may become large even when the solver is doing a good job locally.

Assume a method has a tiny local perturbation. The chaotic dynamics may amplify it as

$$ |e(t)|\sim e^{\lambda_L t}|e(0)|. $$

Thus, after a sufficiently long integration time, pointwise error loses direct interpretability. The benchmark should therefore separate:

1. short-time accuracy, where reference trajectory comparison is meaningful,
2. long-time qualitative behavior, where attractor geometry and statistics matter more.

### Boundedness and qualitative correctness

Although the Lorenz system is chaotic for classical parameters, trajectories do not simply diverge to infinity. The dissipative structure tends to confine long-time trajectories to an attracting region.

A poor numerical method may produce:

- artificial blow-up,
- excessive damping into an equilibrium,
- distorted attractor wings,
- wrong switching frequency between lobes,
- sensitivity to step size that changes qualitative behavior.

A good method should preserve the broad attractor structure over long simulation times even though exact pointwise matching eventually becomes impossible.

### Pseudocode for the right-hand side

```text
Given state X = [x, y, z] and parameters sigma, rho, beta:
    dxdt = sigma * (y - x)
    dydt = x * (rho - z) - y
    dzdt = x * y - beta * z
    return [dxdt, dydt, dzdt]
```

For a separation diagnostic between two nearby trajectories:

```text
Given trajectories Xa(t) and Xb(t):
    delta = norm(Xa - Xb)
    return delta
```

### Main benchmark lesson

The Lorenz system tests a solver's behavior on nonlinear chaotic dynamics. It is not primarily a conservation-law benchmark and not simply a final-time error benchmark. It is a benchmark for short-time accuracy, adaptive step robustness, boundedness, and the preservation of qualitative attractor geometry.

## Implemented MATLAB file

```text
src/benchmarks/benchmark_lorenz.m
```

## Historical background

Edward Lorenz introduced this three-dimensional system in 1963 as a simplified model of deterministic nonperiodic flow.

## Mathematical properties

It tests chaotic sensitivity. Long-time pointwise error is not a fair sole metric; short-time error and attractor-level qualitative behavior are more meaningful.

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
