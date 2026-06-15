# Van der Pol Oscillator

## Equation

The Van der Pol oscillator is a nonlinear second-order oscillator with state-dependent damping. In the benchmark's first-order form, it is written as

$$ x' = y, \qquad y' = \mu(1-x^2)y - x. $$

Here:

- $x(t)$ is the oscillator position-like state,
- $y(t)$ is the velocity-like state,
- $\mu\geq 0$ controls the strength of the nonlinear damping and the degree of stiffness.

Since

$$ y=x', $$

we have

$$ y'=x''. $$

Substituting into the first-order system gives

$$ x''=\mu(1-x^2)x'-x. $$

Equivalently,

$$ x''-\mu(1-x^2)x'+x=0. $$

Another common form is

$$ x''+\mu(x^2-1)x'+x=0. $$

Both forms are identical.

### Relationship to the harmonic oscillator

If

$$ \mu=0, $$

then the equation becomes

$$ x''+x=0. $$

This is the simple harmonic oscillator with natural frequency

$$ \omega_0=1. $$

So the Van der Pol oscillator can be viewed as a nonlinear modification of the harmonic oscillator. The term

$$ \mu(x^2-1)x' $$

is a nonlinear damping term. Unlike ordinary linear damping, its sign depends on the amplitude.

### State-dependent damping

The equation

$$ x''+\mu(x^2-1)x'+x=0 $$

contains the damping coefficient

$$ \mu(x^2-1). $$

When

$$ |x|<1, $$

we have

$$ x^2-1<0. $$

So the damping term is effectively negative. Negative damping injects energy into the system. This causes small oscillations to grow.

When

$$ |x|>1, $$

we have

$$ x^2-1>0. $$

So the damping is positive. Positive damping removes energy from the system. This prevents large oscillations from growing without bound.

This combination creates a self-sustained oscillation. Small motions are amplified, large motions are damped, and the system approaches a stable closed orbit called a limit cycle.

### First-order vector field

Define the state vector

$$ z=(x,y)^T. $$

Then

$$ \dot{z}=f(z)=(y, \mu(1-x^2)y-x)^T. $$

The equilibrium point satisfies

$$ y=0, $$

and

$$ \mu(1-x^2)y-x=0. $$

Since $y=0$, the second equation gives

$$ -x=0. $$

Therefore the only equilibrium is

$$ (x,y)=(0,0). $$

### Linearization near the equilibrium

The Jacobian of the vector field is

$$ J(x,y)= [\frac{\partial f_1}{\partial x},\frac{\partial f_1}{\partial y}; \frac{\partial f_2}{\partial x},\frac{\partial f_2}{\partial y}]. $$

Since

$$ f_1=y, $$

and

$$ f_2=\mu(1-x^2)y-x, $$

we get

$$ J(x,y)= [0,1; -2\mu xy-1,\mu(1-x^2)]. $$

At the origin,

$$ J(0,0)= [0,1; -1,\mu]. $$

The characteristic equation is

$$ \lambda^2-\mu\lambda+1=0. $$

For $\mu>0$, the trace is positive:

$$ tr(J)=\mu>0. $$

The origin is unstable. This agrees with the negative damping interpretation: small oscillations near the origin grow.

### Limit cycle behavior

Although the origin is unstable, the solution does not grow without bound. For large $|x|$, positive damping dominates and reduces the energy. This creates a stable attracting periodic orbit.

A qualitative energy-like function is

$$ E(x,y)=\frac{1}{2}x^2+\frac{1}{2}y^2. $$

Differentiate:

$$ \frac{dE}{dt}=xx'+yy'. $$

Using

$$ x'=y, \qquad y'=\mu(1-x^2)y-x, $$

we get

$$ \frac{dE}{dt}=xy+y[\mu(1-x^2)y-x]. $$

The $xy$ and $-xy$ terms cancel:

$$ \frac{dE}{dt}=\mu(1-x^2)y^2. $$

Therefore

$$ \frac{dE}{dt}=\mu(1-x^2)y^2. $$

When $|x|<1$, energy increases. When $|x|>1$, energy decreases. This explains the self-regulating amplitude of the Van der Pol oscillator.

### Small-mu behavior

For small $\mu$, the system behaves like a weakly nonlinear oscillator. The motion is close to sinusoidal, and the limit cycle resembles the circular or elliptical phase portrait of the harmonic oscillator.

In this regime, non-stiff explicit methods often work well. Step-size control is mostly driven by accuracy rather than severe stability restrictions.

### Large-mu behavior and relaxation oscillation

For large $\mu$, the system becomes a fast-slow problem. The motion consists of:

1. slow drift along attracting branches,
2. rapid jumps between branches,
3. sharp transition layers.

This is called a relaxation oscillation.

The second-order equation can be transformed into a Lienard form. Introduce

$$ F(x)=\frac{x^3}{3}-x. $$

The Van der Pol equation can be represented in fast-slow structure by variables that separate slow evolution from fast jumps. The essential point for numerical integration is that large $\mu$ introduces widely separated time scales.

The slow part evolves over a time scale roughly proportional to $\mu$, while the fast jumps occur over much shorter time intervals. A solver must resolve the fast jumps without wasting too much effort on the slow portions.

### Stiffness transition

The benchmark is especially useful because changing $\mu$ changes the numerical character of the problem.

For

$$ \mu \ll 1, $$

the system is non-stiff and oscillatory.

For

$$ \mu \gg 1, $$

the system becomes stiff because the Jacobian has eigenvalues associated with very different time scales. Explicit methods may be forced to take very small steps near the fast layers for stability, while implicit methods can often handle the stiffness more efficiently.

This makes the Van der Pol oscillator a bridge between simple oscillation benchmarks and genuinely stiff nonlinear dynamics.

### Phase-plane interpretation

In the phase plane $(x,y)$, trajectories starting away from the origin tend toward the same closed curve. This closed curve is the stable limit cycle.

A good numerical method should reproduce:

- the correct amplitude of the limit cycle,
- the correct period,
- the correct shape of the relaxation oscillation,
- the timing of fast jumps,
- the long-time phase behavior.

Final-time error alone may be misleading because a small phase shift can produce a large pointwise error even if the computed limit cycle is qualitatively correct.

### Pseudocode for the right-hand side

```text
Given state z = [x, y] and parameter mu:
    dxdt = y
    dydt = mu * (1 - x^2) * y - x
    return [dxdt, dydt]
```

For the energy-like diagnostic:

```text
Given state z = [x, y]:
    E = 0.5 * x^2 + 0.5 * y^2
    return E
```

### Main benchmark lesson

The Van der Pol oscillator tests nonlinear oscillation, limit-cycle behavior, and the transition from non-stiff to stiff dynamics. It is valuable because the same equation can be easy or difficult depending on $\mu$. That makes it useful for comparing adaptive step-size control, stiffness detection, rejected steps, Jacobian usage, and qualitative phase-plane accuracy.

## Implemented MATLAB file

```text
src/benchmarks/benchmark_vanderpol.m
```

## Historical background

Balthasar van der Pol introduced this nonlinear oscillator in the context of vacuum-tube electrical oscillations and relaxation oscillations.

## Mathematical properties

It tests nonlinear oscillation and stiffness transition. Small mu is non-stiff; large mu produces fast-slow behavior that favors stiff solvers.

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
