# `rmse_error`

## Meaning

`rmse_error` is the root-mean-square trajectory error over all reported output times.

## Mathematical definition

For pointwise errors

$$
e_i=\left\lVert y_i-y_{\mathrm{ref}}(t_i)\right\rVert_2,
$$

the root-mean-square error is

$$
\texttt{rmse\_error}=\sqrt{\frac{1}{N}\sum_{i=1}^{N}e_i^2}.
$$

## Interpretation

This metric summarizes overall trajectory accuracy and is less dominated by one isolated error spike than `max_error`.

## Limitations

RMSE can hide short but important events, positivity violations, constraint drift, or qualitative failures.
