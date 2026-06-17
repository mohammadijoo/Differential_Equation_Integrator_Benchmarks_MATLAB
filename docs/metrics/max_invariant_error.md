# `max_invariant_error`

## Meaning

`max_invariant_error` measures the maximum drift of a conserved or monitored quantity, such as energy, angular momentum, mass, or another invariant.

## Mathematical definition

For an invariant or diagnostic quantity $I(y)$, define

$$
I_i=I(y_i).
$$

Then the maximum invariant drift is

$$
\texttt{max\_invariant\_error}=\max_i \left| I_i-I_0 \right|.
$$

## Interpretation

This is especially important for Hamiltonian mechanics, orbital dynamics, conservative oscillators, mass-conserving PDEs, and geometric integration tests.

## Limitations

Some systems are dissipative or forced, so the monitored quantity may not be conserved. In those cases, compare against the expected diagnostic behavior instead of assuming zero drift.
