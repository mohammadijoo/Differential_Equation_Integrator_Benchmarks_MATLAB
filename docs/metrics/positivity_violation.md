# `positivity_violation`

## Meaning

`positivity_violation` measures how strongly a numerical solution violates nonnegative state constraints.

## Mathematical definition

For a state vector whose components should satisfy $y_j(t)\ge 0$, a common diagnostic is

$$
\texttt{positivity\_violation}=\max_{i,j}\max\left(0,-y_{i,j}\right).
$$

## Interpretation

A value of zero means no negative state was observed on the output grid. This is important for concentrations, populations, probabilities, densities, and chemical kinetics.

## Limitations

A method may violate positivity between output times even if output values look nonnegative. For adaptive methods, positivity should ideally be checked at accepted internal steps as well.
