# Order

**Section:** 3. Order, dimension, and system size

## 1. Meaning

The highest derivative order appearing in the differential equation.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

An $n$th-order scalar ODE has the form

$$x^{(n)}=f(t,x,\dot{x},\ldots,x^{(n-1)}).$$

It can usually be rewritten as a first-order system by defining

$$z_1=x,\quad z_2=\dot{x},\quad \ldots,\quad z_n=x^{(n-1)}.$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

A second-order mechanical equation can be converted to a first-order state-space system before using standard ODE solvers.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Conceptual workflow for Order:

```text
Identify the mathematical role of the term in the model
Write the governing equation and the required data
Choose an analytical, qualitative, or numerical tool
Compute or reason about the solution behavior
Check whether the result is stable, accurate, and physically meaningful
```

## 6. Simple MATLAB example

```matlab
% Generic ODE demonstration for the concept
f = @(t,x) -x + sin(t);
tspan = [0 10];
x0 = 0;
[t,x] = ode45(f,tspan,x0);
plot(t,x,'LineWidth',1.5); grid on
xlabel('t'); ylabel('x(t)'); title('Simple differential-equation simulation');
```

## 7. Practical notes

- Do not confuse the mathematical property of the continuous problem with the numerical property of a specific method.
- Always check units, scaling, and the meaning of each variable before interpreting solver results.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Order` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`First-order ODE`, `Second-order ODE`, `System of ODEs`, `Dimension`
