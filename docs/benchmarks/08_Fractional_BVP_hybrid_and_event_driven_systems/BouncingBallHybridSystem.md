# Bouncing Ball Hybrid System

## Equation

Between impacts, the ball follows

$$ y'=v, $$

$$ v'=-g. $$

At the event $y=0$ with $v<0$, the reset is

$$ v^+=-e v^- $$

where $0<e<1$ is the restitution coefficient.

### Benchmark type

This is a **hybrid ODE with events** benchmark proposed for future simulations in this repository.

### Reference solution or diagnostic quantity

The event times can be computed analytically for simple cases, making this useful for testing event detection and reset handling.

### Mathematical properties emphasized

- event detection
- state reset
- hybrid dynamics
- energy loss

### Numerical difficulty

This benchmark is useful because it exposes numerical behavior that is not fully visible in the current small set of benchmark equations. Depending on the method family, the main difficulty may be accuracy, stiffness, invariant drift, positivity, constraint preservation, event handling, or long-time qualitative behavior.

### Pseudocode for the right-hand side or residual

```text
integrate y'=v and v'=-g
detect y=0 crossing with v<0
reset v = -e*v
continue integration
```

### Main benchmark lesson

This benchmark tests whether an integrator can locate events accurately and apply discontinuous state resets.

## Proposed MATLAB file

```text
src/benchmarks/benchmark_bouncing_ball_hybrid_system.m
```

This file is proposed for a future implementation. The present Markdown file is documentation for the benchmark definition and intended numerical diagnostics.

## Historical background

This equation or model is commonly used as a representative benchmark in numerical analysis, scientific computing, control engineering, computational physics, chemical kinetics, or applied mathematics. It is included here because it exercises solver behavior that is different from the currently implemented benchmark set.

## Mathematical properties

The most relevant mathematical properties for this benchmark are:

- event detection
- state reset
- hybrid dynamics
- energy loss

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

Applications include robotics contact, impact mechanics, hybrid systems, and event-driven simulation.

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
