# Stiff problem

**Section:** 12. Stiffness and time-scale concepts

## 1. Meaning

A problem where stability forces much smaller time steps than accuracy alone would require.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

For the test equation

$$\dot{x}=\lambda x,$$

Forward Euler gives

$$x_{n+1}=(1+h\lambda)x_n.$$

For real negative $\lambda$, stability requires approximately

$$0<h<\frac{2}{|\lambda|}.$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

Stiffness is common when fast stable modes coexist with slow dynamics, as in chemical kinetics or damped mechanical systems.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Conceptual workflow for Stiff problem:

```text
Identify the mathematical role of the term in the model
Write the governing equation and the required data
Choose an analytical, qualitative, or numerical tool
Compute or reason about the solution behavior
Check whether the result is stable, accurate, and physically meaningful
```

## 6. Simple MATLAB example

```matlab
% Stiff test: compare ode45 and ode15s behavior
f = @(t,x) -1000*(x - cos(t)) - sin(t); % exact solution near cos(t)
tspan = [0 5]; x0 = 0;
opts = odeset('RelTol',1e-6,'AbsTol',1e-9);
tic; [t45,x45] = ode45(f,tspan,x0,opts); time45 = toc;
tic; [t15,x15] = ode15s(f,tspan,x0,opts); time15 = toc;
fprintf('ode45 steps = %d, time = %.4g s\n',numel(t45),time45);
fprintf('ode15s steps = %d, time = %.4g s\n',numel(t15),time15);
```

## 7. Practical notes

- A smooth-looking solution can still be stiff because hidden fast modes restrict explicit methods.
- Using a high-order explicit method does not automatically solve stiffness.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Stiff problem` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Non-stiff problem`, `Fast mode`, `Slow mode`, `Multiple time scales`
