# Marginal stability

**Section:** 10. Stability concepts

## 1. Meaning

A bounded response that neither decays nor grows unboundedly.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

For the linear system

$$\dot{x}=Ax,$$

local stability is closely related to the eigenvalues of $A$. If

$$\operatorname{Re}(\lambda_i)<0$$

for all eigenvalues, the system is asymptotically stable.

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

A stable continuous system can still be unstable numerically if the step size is too large for the chosen method.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Conceptual workflow for Marginal stability:

```text
Identify the mathematical role of the term in the model
Write the governing equation and the required data
Choose an analytical, qualitative, or numerical tool
Compute or reason about the solution behavior
Check whether the result is stable, accurate, and physically meaningful
```

## 6. Simple MATLAB example

```matlab
% Stability and eigenvalue check for x' = A x
A = [-2 0; 0 -20];
lambda = eig(A)
% Forward Euler stability requires |1 + h*lambda_i| < 1
h = 0.05;
amplification = abs(1 + h*lambda)
isStableFE = all(amplification < 1)

```

## 7. Practical notes

- A stable physical system can produce an unstable numerical simulation if the step size is too large.
- Stability is not the same as accuracy: a stable result can still be inaccurate.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Marginal stability` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Stability`, `Instability`, `Lyapunov stability`, `Asymptotic stability`
