# Allen-Cahn Equation Method-of-Lines Stiff ODE

## Equation

The Allen-Cahn PDE is

$$ u_t=\epsilon^2u_{xx}+u-u^3. $$

After spatial discretization, it becomes a stiff ODE system

$$ U'=A U+U-U^{\circ 3}. $$

### Benchmark type

This is a **stiff semilinear ODE from PDE discretization** benchmark proposed for future simulations in this repository.

### Reference solution or diagnostic quantity

A reference solution is usually computed using a very small time step or a high-accuracy stiff/exponential method. The stiffness increases as the spatial mesh is refined.

### Mathematical properties emphasized

- PDE-induced stiffness
- semilinear structure
- interface dynamics
- large sparse Jacobian

### Numerical difficulty

This benchmark is useful because it exposes numerical behavior that is not fully visible in the current small set of benchmark equations. Depending on the method family, the main difficulty may be accuracy, stiffness, invariant drift, positivity, constraint preservation, event handling, or long-time qualitative behavior.

### Pseudocode for the right-hand side or residual

```text
compute diffusion = A*U
reaction = U - U.^3
dUdt = diffusion + reaction
return dUdt
```

### Main benchmark lesson

This benchmark tests stiff and exponential methods on a problem whose stiffness comes from spatial discretization.

## Proposed MATLAB file

```text
src/benchmarks/benchmark_allen_cahn_m_o_l_stiff_o_d_e.m
```

This file is proposed for a future implementation. The present Markdown file is documentation for the benchmark definition and intended numerical diagnostics.

## Historical background

This equation or model is commonly used as a representative benchmark in numerical analysis, scientific computing, control engineering, computational physics, chemical kinetics, or applied mathematics. It is included here because it exercises solver behavior that is different from the currently implemented benchmark set.

## Mathematical properties

The most relevant mathematical properties for this benchmark are:

- PDE-induced stiffness
- semilinear structure
- interface dynamics
- large sparse Jacobian

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

Applications include phase-field models, material science, reaction-diffusion systems, and PDE method-of-lines testing.

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
