# Mass conservation

**Section:** 23. Structure-preserving concepts

## 1. Meaning

A property where total mass or total amount is preserved.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

If $I(x)$ is an invariant of the exact system, then

$$\frac{d}{dt}I(x(t))=\nabla I(x)^T f(x)=0.$$

An invariant-preserving method tries to enforce

$$I(x_{n+1})=I(x_n).$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

Structure preservation matters when physical properties such as energy, mass, or positivity should not be destroyed by the algorithm.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Conceptual workflow for Mass conservation:

```text
Identify the mathematical role of the term in the model
Write the governing equation and the required data
Choose an analytical, qualitative, or numerical tool
Compute or reason about the solution behavior
Check whether the result is stable, accurate, and physically meaningful
```

## 6. Simple MATLAB example

```matlab
% Energy drift diagnostic for harmonic oscillator
f = @(t,x) [x(2); -x(1)];
[t,x] = ode45(f,[0 50],[1;0]);
E = 0.5*(x(:,1).^2 + x(:,2).^2);
plot(t,E - E(1),'LineWidth',1.5); grid on
xlabel('t'); ylabel('energy drift'); title('Invariant drift diagnostic');
```

## 7. Practical notes

- Do not confuse the mathematical property of the continuous problem with the numerical property of a specific method.
- Always check units, scaling, and the meaning of each variable before interpreting solver results.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Mass conservation` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Energy preservation`, `Symplectic method`, `Positivity preservation`, `Momentum conservation`
