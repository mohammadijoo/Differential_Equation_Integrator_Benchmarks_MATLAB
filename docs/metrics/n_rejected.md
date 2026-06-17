# `n_rejected`

## Meaning

`n_rejected` counts adaptive trial steps rejected by a step-size controller.

## Typical condition

A trial step is rejected when the estimated local error violates the tolerance condition, for example

$$
\mathrm{err}_{\mathrm{loc}}>1.
$$

## Interpretation

Large `n_rejected` often indicates stiffness, discontinuities, poor step-size prediction, tight tolerances, or instability.

## Limitations

Fixed-step methods usually report zero or `NaN`. Rejection counts are most meaningful for adaptive solvers with comparable error controllers.
