# Robertson Stiff Chemical Kinetics

## Equation

The Robertson problem is a classic stiff chemical kinetics system involving three chemical species. Let the species concentrations be

$$ y_1(t),\qquad y_2(t),\qquad y_3(t). $$

A standard form of the Robertson system is

$$ y_1'=-0.04y_1+10^4y_2y_3, $$

$$ y_2'=0.04y_1-10^4y_2y_3-3\times 10^7y_2^2, $$

$$ y_3'=3\times 10^7y_2^2. $$

The usual initial condition is

$$ y_1(0)=1, \qquad y_2(0)=0, \qquad y_3(0)=0. $$

In compact vector form,

$$ \dot{y}=f(y), \qquad y=[y_1; y_2; y_3]. $$

This system represents a three-species autocatalytic reaction model.

### Reaction interpretation

The terms can be interpreted through reaction rates. The first process converts species $y_1$ into $y_2$ at a slow rate:

$$ y_1 \longrightarrow y_2, \qquad rate=0.04y_1. $$

The second interaction consumes $y_2$ and $y_3$ and regenerates $y_1$:

$$ y_2+y_3 \longrightarrow y_1, \qquad rate=10^4y_2y_3. $$

The third process converts two units of $y_2$ into $y_3$:

$$ 2y_2 \longrightarrow y_3, \qquad rate=3\times 10^7y_2^2. $$

The important numerical feature is not just the chemical interpretation. It is the enormous separation between the coefficients

$$ 0.04, \qquad 10^4, \qquad 3\times10^7. $$

These rates generate very different time scales.

### Conservation of total mass

Add the three equations:

$$ y_1'+y_2'+y_3'=(-0.04y_1+10^4y_2y_3)+(0.04y_1-10^4y_2y_3-3\times10^7y_2^2)+(3\times10^7y_2^2)=0. $$

All terms cancel:

$$ y_1'+y_2'+y_3'=0. $$

Therefore

$$ \frac{d}{dt}(y_1+y_2+y_3)=0. $$

So the total concentration is conserved:

$$ y_1(t)+y_2(t)+y_3(t)=y_1(0)+y_2(0)+y_3(0). $$

For the standard initial condition,

$$ y_1(t)+y_2(t)+y_3(t)=1. $$

This invariant is one of the most important diagnostics in the benchmark. A numerical method should not significantly create or destroy total mass.

### Positivity

Because $y_1$, $y_2$, and $y_3$ represent concentrations, physically meaningful solutions satisfy

$$ y_i(t)\geq 0, \qquad i=1,2,3. $$

The continuous system preserves nonnegativity for nonnegative initial data. For example, if $y_1=0$ and $y_2,y_3\geq0$, then

$$ y_1'=10^4y_2y_3\geq0. $$

So the vector field points back into the nonnegative region. Similarly, if $y_2=0$, then

$$ y_2'=0.04y_1\geq0. $$

If $y_3=0$, then

$$ y_3'=3\times10^7y_2^2\geq0. $$

Thus the nonnegative orthant is invariant.

A numerical method can violate this property if the time step is too large or if the method is not positivity-preserving. Negative concentrations are physically meaningless and can also trigger numerical instability.

### Why the system is stiff

Stiffness comes from the coexistence of very fast and very slow dynamics. The variable $y_2$ is usually very small, but it participates in reactions with very large coefficients. This creates rapid transients followed by slow evolution.

The Jacobian matrix is

$$ J(y)= [-0.04,10^4y_3,10^4y_2; 0.04,-10^4y_3-6\times10^7y_2,-10^4y_2; 0,6\times10^7y_2,0]. $$

The eigenvalues of this Jacobian can have widely separated magnitudes. Some modes decay extremely fast, while others evolve slowly. Explicit methods must often take tiny steps to remain stable on the fast modes even when the solution itself is changing slowly on the visible scale.

This is the core stiffness mechanism.

### Fast transient and slow manifold

At the beginning, the initial condition is

$$ y(0)=(1,0,0)^T. $$

Initially,

$$ y_1'(0)=-0.04, $$

$$ y_2'(0)=0.04, $$

$$ y_3'(0)=0. $$

So $y_2$ begins to increase. But as soon as $y_2$ becomes nonzero, the quadratic term

$$ 3\times10^7y_2^2 $$

can become important. This rapidly converts $y_2$ into $y_3$.

After the fast transient, $y_2$ remains very small and the system evolves slowly as mass transfers from $y_1$ to $y_3$. The trajectory is then constrained near a slow manifold.

This fast-transient/slow-evolution structure is exactly what makes the Robertson problem difficult for non-stiff solvers.

### Accuracy versus physical admissibility

For this benchmark, numerical quality is not only pointwise error. A solver should also preserve important physical properties:

1. nonnegative concentrations,
2. total mass conservation,
3. correct slow evolution,
4. stable handling of fast transient layers.

The total mass error can be measured by

$$ M(t)=y_1(t)+y_2(t)+y_3(t), $$

and

$$ \Delta M(t)=M(t)-M(0). $$

For the exact solution,

$$ \Delta M(t)=0. $$

A positivity violation can be measured by

$$ min_i y_i(t). $$

If this value becomes negative, the numerical solution has left the physically admissible region.

### Implicit methods and Jacobians

Stiff chemical kinetics problems often favor implicit or linearly implicit methods. An implicit step may require solving nonlinear equations such as

$$ y_{n+1}=y_n+h f(y_{n+1}). $$

Newton's method for this equation involves the matrix

$$ I-hJ(y_{n+1}). $$

Therefore, the number of Jacobian evaluations, LU factorizations, nonlinear iterations, accepted steps, and rejected steps can be more informative than CPU time alone.

Two solvers may produce similar errors, but one may require far fewer right-hand-side calls or Jacobian evaluations. This is especially important for chemical kinetics systems where evaluating the reaction network can be expensive.

### Pseudocode for the right-hand side

```text
Given state y = [y1, y2, y3]:
    dy1dt = -0.04 * y1 + 1.0e4 * y2 * y3
    dy2dt =  0.04 * y1 - 1.0e4 * y2 * y3 - 3.0e7 * y2^2
    dy3dt =  3.0e7 * y2^2
    return [dy1dt, dy2dt, dy3dt]
```

For invariant and positivity diagnostics:

```text
Given state y = [y1, y2, y3] and initial mass M0:
    mass = y1 + y2 + y3
    mass_error = mass - M0
    minimum_concentration = min(y1, y2, y3)
    return mass_error, minimum_concentration
```

### Main benchmark lesson

The Robertson problem tests stiff-solver robustness, positivity preservation, and conservation of total mass. It is a strong benchmark because the solution combines rapid initial transients with long slow evolution. A method that performs well here must control both numerical stability and physical admissibility.

## Implemented MATLAB file

```text
src/benchmarks/benchmark_robertson.m
```

## Historical background

The Robertson problem is a classic stiff chemical kinetics benchmark. Its widely separated reaction rates create fast transients followed by slow evolution.

## Mathematical properties

It tests stiff-solver robustness, positivity, conservation of total mass, and efficiency of implicit or linearly implicit methods.

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
