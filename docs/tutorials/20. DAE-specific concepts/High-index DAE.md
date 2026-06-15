# High-index DAE

**Section:** 20. DAE-specific concepts

## 1. Meaning

A DAE requiring more differentiations of constraints and more specialized numerical treatment.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

A semi-explicit DAE can be written as

$$\dot{x}=f(t,x,y),\qquad 0=g(t,x,y),$$

where $x$ is differential and $y$ is algebraic.

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

DAE concepts appear in constrained mechanics, circuits, multibody systems, and process models.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Conceptual workflow for High-index DAE:

```text
Identify the mathematical role of the term in the model
Write the governing equation and the required data
Choose an analytical, qualitative, or numerical tool
Compute or reason about the solution behavior
Check whether the result is stable, accurate, and physically meaningful
```

## 6. Simple MATLAB example

```matlab
% Simple index-1 DAE with mass matrix: x1' = x2, 0 = x1 + x2 - 1
M = [1 0; 0 0];
f = @(t,x) [x(2); x(1) + x(2) - 1];
opts = odeset('Mass',M,'MassSingular','yes');
x0 = [1; 0];  % consistent because x1 + x2 - 1 = 0
[t,x] = ode15s(f,[0 5],x0,opts);
plot(t,x,'LineWidth',1.5); grid on
legend('x_1','x_2'); title('Simple DAE with ode15s');
```

## 7. Practical notes

- Do not confuse the mathematical property of the continuous problem with the numerical property of a specific method.
- Always check units, scaling, and the meaning of each variable before interpreting solver results.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `High-index DAE` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Algebraic constraint`, `Differential variable`, `Algebraic variable`, `Index`
