# SDE

**Section:** 1. Basic differential-equation types

## 1. Meaning

Stochastic Differential Equation: a differential equation driven by random noise processes.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

Itô form:

$$dX=a(X,t)dt+b(X,t)dW_t.$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

Use this term to classify the mathematical problem before choosing a solver. The type determines whether you need an ODE solver, PDE discretization, DAE solver, delay solver, or stochastic simulator.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Conceptual workflow for SDE:

```text
Identify the mathematical role of the term in the model
Write the governing equation and the required data
Choose an analytical, qualitative, or numerical tool
Compute or reason about the solution behavior
Check whether the result is stable, accurate, and physically meaningful
```

## 6. Simple MATLAB example

```matlab
% Euler-Maruyama for dX = a X dt + b X dW
rng(1);
a = -1; b = 0.3; T = 2; N = 2000; dt = T/N;
t = linspace(0,T,N+1); X = zeros(1,N+1); X(1)=1;
for n = 1:N
    dW = sqrt(dt)*randn;
    X(n+1) = X(n) + a*X(n)*dt + b*X(n)*dW;
end
plot(t,X,'LineWidth',1.2); grid on
xlabel('t'); ylabel('X(t)'); title('Euler-Maruyama sample path');
```

## 7. Practical notes

- Do not confuse the mathematical property of the continuous problem with the numerical property of a specific method.
- Always check units, scaling, and the meaning of each variable before interpreting solver results.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `SDE` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Differential equation`, `ODE`, `PDE`, `DAE`
