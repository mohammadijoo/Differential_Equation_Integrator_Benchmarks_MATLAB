# Rigid Body Euler Equations

## Equation

For a torque-free rigid body in body coordinates,

$$ I_1\omega_1'=(I_2-I_3)\omega_2\omega_3, $$

$$ I_2\omega_2'=(I_3-I_1)\omega_3\omega_1, $$

$$ I_3\omega_3'=(I_1-I_2)\omega_1\omega_2. $$

### Benchmark type

This is a **three-dimensional nonlinear ODE** benchmark proposed for future simulations in this repository.

### Reference solution or diagnostic quantity

The system conserves rotational kinetic energy

$$ E=\frac{1}{2}(I_1\omega_1^2+I_2\omega_2^2+I_3\omega_3^2) $$

and angular momentum magnitude

$$ L^2=I_1^2\omega_1^2+I_2^2\omega_2^2+I_3^2\omega_3^2. $$

### Mathematical properties emphasized

- quadratic nonlinearity
- two invariants
- long-time drift
- intermediate-axis instability

### Numerical difficulty

This benchmark is useful because it exposes numerical behavior that is not fully visible in the current small set of benchmark equations. Depending on the method family, the main difficulty may be accuracy, stiffness, invariant drift, positivity, constraint preservation, event handling, or long-time qualitative behavior.

### Pseudocode for the right-hand side or residual

```text
dw1dt = ((I2 - I3)/I1)*w2*w3
dw2dt = ((I3 - I1)/I2)*w3*w1
dw3dt = ((I1 - I2)/I3)*w1*w2
return [dw1dt; dw2dt; dw3dt]
```

### Main benchmark lesson

This benchmark checks whether integrators respect multiple invariants in nonlinear rotational dynamics.

## Proposed MATLAB file

```text
src/benchmarks/benchmark_rigid_body_euler_equations.m
```

This file is proposed for a future implementation. The present Markdown file is documentation for the benchmark definition and intended numerical diagnostics.

## Historical background

This equation or model is commonly used as a representative benchmark in numerical analysis, scientific computing, control engineering, computational physics, chemical kinetics, or applied mathematics. It is included here because it exercises solver behavior that is different from the currently implemented benchmark set.

## Mathematical properties

The most relevant mathematical properties for this benchmark are:

- quadratic nonlinearity
- two invariants
- long-time drift
- intermediate-axis instability

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

Applications include spacecraft attitude, robotics, gyroscopes, rigid-body mechanics, and geometric integration.

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
