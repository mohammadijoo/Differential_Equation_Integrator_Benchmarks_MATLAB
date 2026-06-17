# `n_steps`

## Meaning

`n_steps` counts the number of accepted integration steps, or the number of output intervals when a method does not expose an internal step counter.

## Typical definition

For a fixed-step method with output times $t_0,t_1,\ldots,t_N$,

$$
\texttt{n\_steps}=N.
$$

For adaptive methods, the preferred value is the number of accepted internal steps:

$$
\texttt{n\_steps}=N_{\mathrm{accepted}}.
$$

## Interpretation

A method requiring fewer accepted steps may be more efficient, but only when accuracy, stability, and rejected-step behavior are also acceptable.

## Limitations

The value is not directly comparable unless the solver interfaces report steps consistently. Use with `n_rejected`, `nfev`, and `cpu_time`.
