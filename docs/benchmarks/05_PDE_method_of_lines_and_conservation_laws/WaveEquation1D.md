# One-Dimensional Wave Equation

## Equation

The wave equation is

$$ u_{tt}=c^2u_{xx}. $$

As a first-order system,

$$ u_t=v, $$

$$ v_t=c^2u_{xx}. $$

### Benchmark type

This is a **second-order hyperbolic PDE** benchmark proposed for future simulations in this repository.

### Reference solution or diagnostic quantity

For suitable initial data and boundary conditions, the solution is a superposition of traveling waves. The continuous energy

$$ E=\int \left(\frac{1}{2}v^2+\frac{1}{2}c^2u_x^2\right)dx $$

is conserved.

### Mathematical properties emphasized

- hyperbolic dynamics
- energy conservation
- CFL stability
- phase error

### Numerical difficulty

This benchmark is useful because it exposes numerical behavior that is not fully visible in the current small set of benchmark equations. Depending on the method family, the main difficulty may be accuracy, stiffness, invariant drift, positivity, constraint preservation, event handling, or long-time qualitative behavior.

### Pseudocode for the right-hand side or residual

```text
dUdt = V
dVdt = c^2 * D2 * U
return [dUdt; dVdt]
```

### Main benchmark lesson

This benchmark tests time integrators for second-order wave systems and long-time energy behavior.

## Proposed MATLAB file

```text
src/benchmarks/benchmark_wave_equation1_d.m
```

This file is proposed for a future implementation. The present Markdown file is documentation for the benchmark definition and intended numerical diagnostics.

## Historical background

This equation or model is commonly used as a representative benchmark in numerical analysis, scientific computing, control engineering, computational physics, chemical kinetics, or applied mathematics. It is included here because it exercises solver behavior that is different from the currently implemented benchmark set.

## Mathematical properties

The most relevant mathematical properties for this benchmark are:

- hyperbolic dynamics
- energy conservation
- CFL stability
- phase error

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

Applications include vibrating strings, acoustics, electromagnetics, structural waves, and hyperbolic PDEs.

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
