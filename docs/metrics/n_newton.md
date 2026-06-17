# `n_newton`

## Meaning

`n_newton` counts Newton or Newton-like nonlinear iterations used inside implicit methods.

## Mathematical context

For an implicit step residual $G(z)=0$, Newton iteration has the form

$$
J_G(z_k)\Delta z_k=-G(z_k),
$$

$$
z_{k+1}=z_k+\Delta z_k.
$$

## Interpretation

More Newton iterations usually mean a harder nonlinear solve, a poor initial guess, a large time step, stiffness, or insufficient Jacobian reuse strategy.

## Limitations

Different methods use full Newton, modified Newton, inexact Newton, chord iterations, or fixed-point iterations. Compare only when the nonlinear-solve strategy is documented.
