# Robustness

**Section:** 24. Benchmarking and solver-performance terms

## 1. Meaning

A solver or benchmark property describing reliable behavior across many problems and settings.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

A benchmark often compares numerical error against computational work:

$$\text{work}=N_f+\alpha N_J+\beta N_{\text{lin}},$$

where $N_f$ is function evaluations and $N_J$ is Jacobian evaluations.

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

Benchmarking terms help compare solvers beyond final error, especially when comparing explicit, implicit, stiff, and adaptive methods.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

Benchmarking sketch:

```text
for each benchmark problem:
    compute or load a high-accuracy reference solution
    for each solver and tolerance/step-size setting:
        run the solver
        record CPU time, accepted steps, rejected steps, function calls
        compute final-time error and trajectory error
        compute invariant or positivity diagnostics when relevant
    create tables and work-precision plots
end
```

## 6. Simple MATLAB example

```matlab
% Simple benchmark skeleton: CPU time and error
f = @(t,x) -x;
opts = odeset('RelTol',1e-8,'AbsTol',1e-10);
tic;
[t,x] = ode45(f,[0 5],1,opts);
cpuTime = toc;
errFinal = abs(x(end) - exp(-t(end)));
fprintf('CPU time = %.6f s\n',cpuTime);
fprintf('final-time error = %.3e\n',errFinal);
```

## 7. Practical notes

- CPU time alone can be misleading because implementation language, vectorization, and hardware affect timing.
- Final-time error may miss large errors earlier in the trajectory.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Robustness` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`CPU time`, `Function evaluations`, `Jacobian evaluations`, `Accepted steps`
