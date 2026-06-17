# `n_linear_solve`

## Meaning

`n_linear_solve` counts linear systems solved inside implicit, linearly implicit, Rosenbrock, Newton-Krylov, DAE, or PDE-derived methods.

## Mathematical context

A typical implicit method repeatedly solves systems of the form

$$
A\Delta z=b.
$$

For stiff ODEs, a common matrix form is

$$
A=I-h\gamma J.
$$

## Interpretation

This metric is important because linear solves often dominate the runtime of stiff and large-scale problems.

## Limitations

Dense LU, sparse LU, Krylov solves, preconditioned solves, and matrix-free solves have very different costs. Count this metric together with factorization and preconditioning details when available.
