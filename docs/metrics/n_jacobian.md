# `n_jacobian`

## Meaning

`n_jacobian` counts Jacobian evaluations used by implicit, linearly implicit, Newton, Rosenbrock, DAE, or stiff solver components.

## Mathematical context

For an ODE right-hand side $f(t,y)$, the Jacobian is

$$
J(t,y)=\frac{\partial f}{\partial y}(t,y).
$$

For a residual equation $F(t,y,y')=0$, a solver may need derivatives such as

$$
\frac{\partial F}{\partial y}
\qquad\text{and}\qquad
\frac{\partial F}{\partial y'}.
$$

## Interpretation

Frequent Jacobian recomputation can increase cost but may improve nonlinear convergence and robustness.

## Limitations

Analytic, finite-difference, sparse, dense, and reused Jacobians have very different costs. Interpret this metric together with `cpu_time`, `n_newton`, and `n_linear_solve`.
