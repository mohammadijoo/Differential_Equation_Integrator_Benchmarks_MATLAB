# `nfev`

## Meaning

`nfev` counts right-hand-side evaluations of the differential equation model.

## Mathematical context

For an ODE

$$
y'=f(t,y),
$$

`nfev` counts calls to $f(t,y)$.

## Interpretation

This is a direct work metric for explicit methods and remains important for implicit, adaptive, and multistage methods.

## Limitations

One function evaluation may have very different cost depending on the benchmark. For stiff implicit methods, Jacobian evaluations and linear solves may dominate the cost.
