# `max_error`

## Meaning

`max_error` measures the largest trajectory error over all reported output times.

## Mathematical definition

For output times $t_i$, numerical states $y_i$, and reference states $y_{\mathrm{ref}}(t_i)$, define the pointwise error as

$$
e_i=\left\lVert y_i-y_{\mathrm{ref}}(t_i)\right\rVert_2.
$$

Then

$$
\texttt{max\_error}=\max_i e_i.
$$

## Interpretation

This metric detects the worst error over the entire comparison window, not only at the endpoint.

## Limitations

It can be sensitive to a single local spike, interpolation mismatch, or transient layer. Use it with `rmse_error` and plots of error versus time.
