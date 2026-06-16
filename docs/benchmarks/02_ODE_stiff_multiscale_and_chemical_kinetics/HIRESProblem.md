# HIRES Stiff ODE Problem

## Equation

The HIRES problem is a classical stiff test system with eight coupled variables. A standard form is

$$ y_1'=-1.71y_1+0.43y_2+8.32y_3+0.0007, $$

$$ y_2'=1.71y_1-8.75y_2, $$

$$ y_3'=-10.03y_3+0.43y_4+0.035y_5, $$

with additional coupled equations for $y_4,\ldots,y_8$.

### Benchmark type

This is a **eight-dimensional stiff ODE** benchmark proposed for future simulations in this repository.

### Reference solution or diagnostic quantity

A high-accuracy implicit reference solution is normally used. The benchmark is valuable because the state components evolve on different time scales and the system has a moderately large dimension for a hand-written test.

### Mathematical properties emphasized

- stiffness
- multiscale transients
- moderate dimension
- implicit solver efficiency

### Numerical difficulty

This benchmark is useful because it exposes numerical behavior that is not fully visible in the current small set of benchmark equations. Depending on the method family, the main difficulty may be accuracy, stiffness, invariant drift, positivity, constraint preservation, event handling, or long-time qualitative behavior.

### Pseudocode for the right-hand side or residual

```text
evaluate the eight coupled HIRES right-hand-side components
return dy
```

### Main benchmark lesson

This benchmark tests stiff integrators on a larger chemical/biochemical-style system than Robertson.

## Proposed MATLAB file

```text
src/benchmarks/benchmark_h_i_r_e_s_problem.m
```

This file is proposed for a future implementation. The present Markdown file is documentation for the benchmark definition and intended numerical diagnostics.

## Historical background

This equation or model is commonly used as a representative benchmark in numerical analysis, scientific computing, control engineering, computational physics, chemical kinetics, or applied mathematics. It is included here because it exercises solver behavior that is different from the currently implemented benchmark set.

## Mathematical properties

The most relevant mathematical properties for this benchmark are:

- stiffness
- multiscale transients
- moderate dimension
- implicit solver efficiency

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

Applications include stiff biochemical kinetics, reaction networks, and solver-regression tests.

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
