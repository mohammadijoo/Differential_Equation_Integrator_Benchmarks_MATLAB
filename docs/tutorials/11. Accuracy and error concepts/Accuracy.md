# Accuracy

**Section:** 11. Accuracy and error concepts

## 1. Meaning

Closeness of a numerical or approximate solution to the exact solution.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

If $x(t_n)$ is the exact solution and $x_n$ is the numerical solution, the error is

$$e_n=x(t_n)-x_n.$$

A method has global order $p$ if

$$\|e_n\|=O(h^p).$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

Accuracy measures closeness to truth; error analysis explains whether reducing the step size improves the solution as expected.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Conceptual workflow for Accuracy:

```text
Identify the mathematical role of the term in the model
Write the governing equation and the required data
Choose an analytical, qualitative, or numerical tool
Compute or reason about the solution behavior
Check whether the result is stable, accurate, and physically meaningful
```

## 6. Simple MATLAB example

```matlab
% Accuracy/error example for x'=-x with exact solution exp(-t)
f = @(t,x) -x;
[t,xnum] = ode45(f,[0 5],1);
xexact = exp(-t);
err = abs(xexact - xnum);
plot(t,err,'LineWidth',1.5); grid on
xlabel('t'); ylabel('|error|'); title('Numerical error');
```

## 7. Practical notes

- Small local error does not automatically mean small global error over long integrations.
- Round-off error can dominate when the step size is made excessively small.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Accuracy` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Error`, `Local truncation error`, `Global error`, `Round-off error`
