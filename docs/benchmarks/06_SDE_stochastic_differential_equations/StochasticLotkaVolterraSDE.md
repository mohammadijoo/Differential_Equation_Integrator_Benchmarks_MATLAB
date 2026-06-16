# Stochastic Lotka-Volterra SDE

## Equation

A stochastic predator-prey system may be written as

$$ dX=(\alpha X-\beta XY)dt+\sigma_1X\,dW_1, $$

$$ dY=(\delta XY-\gamma Y)dt+\sigma_2Y\,dW_2. $$

### Benchmark type

This is a **multiplicative-noise population SDE** benchmark proposed for future simulations in this repository.

### Reference solution or diagnostic quantity

No closed-form trajectory solution is generally used. Diagnostics include positivity, sample moments, extinction probability, and comparison with Monte Carlo references.

### Mathematical properties emphasized

- nonlinear drift
- multiplicative noise
- positivity
- Monte Carlo statistics

### Numerical difficulty

This benchmark is useful because it exposes numerical behavior that is not fully visible in the current small set of benchmark equations. Depending on the method family, the main difficulty may be accuracy, stiffness, invariant drift, positivity, constraint preservation, event handling, or long-time qualitative behavior.

### Pseudocode for the right-hand side or residual

```text
dX = (alpha*X - beta*X*Y)*dt + sigma1*X*dW1
dY = (delta*X*Y - gamma*Y)*dt + sigma2*Y*dW2
```

### Main benchmark lesson

This benchmark tests stochastic nonlinear population dynamics where physical admissibility is important.

## Proposed MATLAB file

```text
src/benchmarks/benchmark_stochastic_lotka_volterra_s_d_e.m
```

This file is proposed for a future implementation. The present Markdown file is documentation for the benchmark definition and intended numerical diagnostics.

## Historical background

This equation or model is commonly used as a representative benchmark in numerical analysis, scientific computing, control engineering, computational physics, chemical kinetics, or applied mathematics. It is included here because it exercises solver behavior that is different from the currently implemented benchmark set.

## Mathematical properties

The most relevant mathematical properties for this benchmark are:

- nonlinear drift
- multiplicative noise
- positivity
- Monte Carlo statistics

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

Applications include ecology, stochastic biology, risk analysis, and nonlinear SDE integration.

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
