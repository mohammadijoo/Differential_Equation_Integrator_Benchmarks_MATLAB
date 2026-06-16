# Planar Circular Restricted Three-Body Problem

## Equation

In a rotating frame, the planar circular restricted three-body problem is

$$ x''-2y'=\frac{\partial \Omega}{\partial x}, $$

$$ y''+2x'=\frac{\partial \Omega}{\partial y}, $$

where

$$ \Omega(x,y)=\frac{1}{2}(x^2+y^2)+\frac{1-\mu}{r_1}+\frac{\mu}{r_2}. $$

### Benchmark type

This is a **Hamiltonian celestial mechanics ODE** benchmark proposed for future simulations in this repository.

### Reference solution or diagnostic quantity

The Jacobi integral is conserved:

$$ C=2\Omega(x,y)-(x'^2+y'^2). $$

### Mathematical properties emphasized

- celestial mechanics
- Jacobi invariant
- sensitive orbits
- long-time behavior

### Numerical difficulty

This benchmark is useful because it exposes numerical behavior that is not fully visible in the current small set of benchmark equations. Depending on the method family, the main difficulty may be accuracy, stiffness, invariant drift, positivity, constraint preservation, event handling, or long-time qualitative behavior.

### Pseudocode for the right-hand side or residual

```text
compute distances r1 and r2
compute Omega_x and Omega_y
dxdt = vx
dydt = vy
dvxdt = 2*vy + Omega_x
dvydt = -2*vx + Omega_y
return [dxdt; dydt; dvxdt; dvydt]
```

### Main benchmark lesson

This benchmark extends the Kepler problem to a more complex gravitational system with nontrivial invariant structure.

## Proposed MATLAB file

```text
src/benchmarks/benchmark_planar_restricted_three_body_problem.m
```

This file is proposed for a future implementation. The present Markdown file is documentation for the benchmark definition and intended numerical diagnostics.

## Historical background

This equation or model is commonly used as a representative benchmark in numerical analysis, scientific computing, control engineering, computational physics, chemical kinetics, or applied mathematics. It is included here because it exercises solver behavior that is different from the currently implemented benchmark set.

## Mathematical properties

The most relevant mathematical properties for this benchmark are:

- celestial mechanics
- Jacobi invariant
- sensitive orbits
- long-time behavior

## Why it is a benchmark

This problem is proposed because it can help compare:

- accuracy,
- stability,
- stiffness handling,
- phase error,
- conservation-law drift,
- positivity or physical admissibility,
- constraint or algebraic residuals when applicable,
- event handling when applicable,
- computational cost.

## Real-world applications

Applications include astrodynamics, orbital mechanics, mission design, and long-time geometric integration.

## Metrics emphasized in this repository

- final error against exact or high-accuracy reference solution,
- maximum trajectory error,
- RMS trajectory error,
- CPU time,
- number of right-hand-side evaluations,
- accepted and rejected step counts when adaptive methods are used,
- Jacobian evaluations, Newton iterations, and linear solves for implicit methods,
- invariant drift or constraint violation when applicable,
- positivity or physical-admissibility violation when applicable,
- qualitative trajectory behavior.

## Recommended plots

- solution versus time,
- error versus time,
- work-precision diagram,
- phase portrait, orbit plot, or state-space projection when applicable,
- invariant, mass, energy, constraint, or positivity error when applicable.

## Suggested default simulation setup

A useful initial implementation should include:

- a clearly documented initial condition,
- a moderate final time for basic tests,
- a longer final time for qualitative or invariant-drift tests,
- at least one easy parameter regime,
- at least one difficult parameter regime,
- a high-accuracy reference solution when no exact solution is available.

## Implementation notes

When implementing this benchmark in MATLAB, keep the benchmark function interface consistent with the existing repository conventions. The benchmark should define the right-hand side or residual, initial condition or history function, default time interval, reference-solution strategy, diagnostic metrics, and plot labels.

## References

See [`../references.md`](../references.md).
