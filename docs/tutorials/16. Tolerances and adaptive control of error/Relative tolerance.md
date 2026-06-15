# Relative tolerance

**Section:** 16. Tolerances and adaptive control of error

## 1. Meaning

An error tolerance scaled relative to the magnitude of the solution.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

A common adaptive-solver error test is

$$|e_i|\le \text{AbsTol}_i+\text{RelTol}\,|x_i|.$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

Tolerances are the user-facing way of telling adaptive solvers how much local error is acceptable.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Adaptive error-control sketch:

```text
choose initial h, AbsTol, and RelTol
while t < tf:
    compute high-order and low-order approximations
    estimate local error e
    scale error using AbsTol + RelTol*abs(x)
    if scaled error <= 1:
        accept step and advance solution
    else:
        reject step
    update h based on error estimate
end
```

## 6. Simple MATLAB example

```matlab
% Absolute and relative tolerance in ode45
f = @(t,x) -x;
opts = odeset('RelTol',1e-6,'AbsTol',1e-9);
[t,x] = ode45(f,[0 10],1,opts);
plot(t,x,'LineWidth',1.5); grid on
title('ode45 with RelTol and AbsTol');
```

## 7. Practical notes

- Do not confuse the mathematical property of the continuous problem with the numerical property of a specific method.
- Always check units, scaling, and the meaning of each variable before interpreting solver results.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Relative tolerance` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Absolute tolerance`, `Error norm`, `Adaptive step-size control`, `Minimum step size`
