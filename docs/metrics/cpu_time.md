# `cpu_time`

## Meaning

`cpu_time` stores the elapsed MATLAB execution time for one method on one benchmark.

## Measurement

In the current framework, timing is measured around the solver call using MATLAB timing utilities:

$$
\texttt{cpu\_time}=t_{\mathrm{stop}}-t_{\mathrm{start}}.
$$

## Interpretation

Lower values usually indicate faster execution for the same benchmark, tolerances, output grid, and hardware.

## Limitations

Timing is affected by MATLAB overhead, implementation style, hardware, operating system load, JIT warm-up, plotting, and memory allocation. It should not be used alone. Pair it with `nfev`, `n_steps`, `n_rejected`, `n_jacobian`, `n_newton`, and `n_linear_solve`.
