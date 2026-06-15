# Backward Euler

**Section:** 14. Common ODE numerical methods

## 1. Meaning

A first-order implicit one-step method using the derivative at the next point.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

Update formula:

$$x_{n+1}=x_n+h f(t_{n+1},x_{n+1}).$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

These methods define practical update formulas for moving from t_n to t_{n+1}. Their stability and accuracy differ strongly.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Algorithm sketch for using or implementing Backward Euler:

```text
Define f(t, x), t0, tf, x0, and step-size or tolerances
Initialize t = t0 and x = x0
while t < tf:
    compute the method-specific stage/update formula
    estimate or accept the next state x_next
    store t_next and x_next
    set t = t_next, x = x_next
end
analyze error, stability, and performance
```

## 6. Simple MATLAB example

```matlab
% Backward Euler for x' = -lambda*x
lambda = 10; h = 0.1; t = 0:h:5; x = zeros(size(t)); x(1)=1;
for n = 1:numel(t)-1
    x(n+1) = x(n)/(1 + h*lambda);
end
plot(t,x,'o-',t,exp(-lambda*t),'LineWidth',1.2); grid on
legend('Backward Euler','Exact');
```

## 7. Practical notes

- Do not confuse the mathematical property of the continuous problem with the numerical property of a specific method.
- Always check units, scaling, and the meaning of each variable before interpreting solver results.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Backward Euler` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Forward Euler`, `Trapezoidal method`, `RK2`, `RK4`
