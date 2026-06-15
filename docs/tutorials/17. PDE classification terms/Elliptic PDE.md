# Elliptic PDE

**Section:** 17. PDE classification terms

## 1. Meaning

A PDE class often associated with steady-state spatial equilibrium problems.

In differential-equation work, this term matters because it affects how the model is written, how the solution is interpreted, and which numerical method is appropriate. A good habit is to classify the equation first, then decide whether the main difficulty is mathematical modeling, qualitative analysis, numerical stability, numerical accuracy, or computational cost.

## 2. Mathematical form

Canonical PDE examples are

$$\nabla^2 u=0 \quad \text{(elliptic)},$$

$$u_t=\alpha u_{xx} \quad \text{(parabolic)},$$

$$u_{tt}=c^2u_{xx} \quad \text{(hyperbolic)}.$$

The formula above is not the only possible notation, but it is the standard notation used in numerical analysis, control engineering, scientific computing, and MATLAB-based simulation work.

## 3. Interpretation

PDE classification gives immediate information about boundary conditions, propagation behavior, and appropriate numerical methods.

For this specific term, the key practical question is: *what does this concept change in the workflow?* Sometimes it changes the mathematical problem type. Sometimes it changes only the diagnostics used after solving. In numerical integrator benchmarking, even conceptual terms become useful because they explain why two solvers can behave very differently on the same model.

## 4. Minimal example

Consider the simple decay model

$$\dot{x}=-a x,\qquad x(0)=x_0,$$

with exact solution

$$x(t)=x_0 e^{-a t}.$$

This small model is useful because it exposes many fundamental ideas: solution behavior, stability, step-size sensitivity, error, stiffness for large $a$, and solver efficiency.

## 5. Pseudocode

PDE discretization sketch:

```text
Define spatial domain and boundary conditions
Create grid or mesh
Approximate spatial derivatives or fluxes
Choose time step according to stability/accuracy requirements
for each time level:
    update interior unknowns
    enforce boundary conditions
    monitor stability, conservation, and error indicators
end
```

## 6. Simple MATLAB example

```matlab
% Explicit finite-difference heat equation demo
alpha = 0.1; L = 1; Nx = 51; dx = L/(Nx-1);
x = linspace(0,L,Nx)';
dt = 0.4*dx^2/alpha;  % stable for 1-D explicit heat equation
Nt = 200;
u = sin(pi*x);        % initial condition
u(1) = 0; u(end) = 0; % Dirichlet boundaries
for n = 1:Nt
    un = u;
    u(2:end-1) = un(2:end-1) + alpha*dt/dx^2 * ...
        (un(1:end-2) - 2*un(2:end-1) + un(3:end));
end
plot(x,u,'LineWidth',1.5); grid on
xlabel('x'); ylabel('u(x,t)'); title('Heat equation approximation');
```

## 7. Practical notes

- Boundary conditions and mesh resolution can dominate the quality of PDE simulations.
- Violating a CFL-type condition can cause blow-up even if the differential equation is physically stable.

## 8. How this connects to integrator benchmarks

When benchmarking differential-equation integrators, `Elliptic PDE` should be treated as either a modeling classification, a solver property, or a diagnostic quantity. For example, a benchmark report may compare final-time error, trajectory error, accepted steps, rejected steps, function evaluations, Jacobian evaluations, positivity preservation, energy drift, and behavior under larger step sizes. The correct interpretation depends on the mathematical role of the term.

## 9. Related terms in this section

`Parabolic PDE`, `Hyperbolic PDE`, `Advection`, `Diffusion`
