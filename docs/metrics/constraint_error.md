# `constraint_error`

## Meaning

`constraint_error` measures violation of algebraic, geometric, or DAE constraints.

## Mathematical definition

For constraints

$$
g(y)=0,
$$

a typical diagnostic is

$$
\texttt{constraint\_error}=\max_i \left\lVert g(y_i)\right\rVert_2.
$$

For DAE residuals written as

$$
F(t,y,y')=0,
$$

one may also monitor

$$
\max_i \left\lVert F(t_i,y_i,y_i')\right\rVert_2.
$$

## Interpretation

This metric is central for constrained mechanics, circuit DAEs, index-reduced systems, projection methods, SHAKE/RATTLE-type schemes, and geometric constraints.

## Limitations

The scale of the constraint matters. A normalized residual may be needed when different constraints have different physical units.
