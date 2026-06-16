# Differential Equation Integrator Benchmarks in MATLAB

A MATLAB benchmark framework for studying, implementing, and comparing numerical integration methods for differential equations.

This repository started as an ODE integrator benchmark suite, but it has been reorganized into a broader numerical-solver catalog covering:

- classical and modern ODE initial-value integrators,
- stiff, implicit, multistep, Rosenbrock, exponential, IMEX, splitting, and geometric methods,
- nonlinear solvers and linear algebra machinery used inside implicit methods,
- DAE, PDE, SDE, DDE, fractional, BVP, hybrid, multirate, and parallel-in-time benchmark directions,
- MATLAB implementations and future implementation scaffolds organized by method and benchmark family.

The repository is intended for numerical-analysis education, control engineering, robotics simulation, computational physics, chemical kinetics, and scientific-computing benchmark development.

---

## Current status

The repository contains two related layers:

1. **Runnable MATLAB benchmark framework**  
   Implemented methods and benchmarks can be executed through `run_all.m` and `run_one_benchmark.m`.

2. **Expanded documentation and implementation roadmap**  
   Many additional methods and benchmark problems are documented and organized in category folders. Some of these are planned/scaffolded and are not executed by default until their MATLAB implementations are completed.

By default, the runner excludes planned methods and planned benchmarks. This keeps the repository runnable while the catalog grows.

---

## Quick start

Open MATLAB in the repository root and run:

```matlab
run_all
```

Run a single benchmark by registry name:

```matlab
run_one_benchmark('LinearTestEquation')
run_one_benchmark('LorenzSystem')
run_one_benchmark('RobertsonKinetics')
run_one_benchmark('KeplerTwoBody')
```

Use options explicitly:

```matlab
opts = default_options();
opts.h = 1e-2;
opts.write_plots = true;
opts.write_tables = true;
opts.include_planned_methods = false;
opts.include_planned_benchmarks = false;

results = run_all(opts);
```

Results are written under:

```text
results/
```

or, depending on the benchmark runner, under benchmark-specific result folders such as:

```text
results/<BenchmarkName>/
```

---

## Repository structure

```text
.
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── CITATION.cff
├── run_all.m
├── run_one_benchmark.m
├── docs/
│   ├── methods/
│   │   ├── 01_ODE_initial_value_integrators/
│   │   ├── 02_DAE_integrators_and_constraint_methods/
│   │   ├── 03_PDE_time_integration_and_spatial_discretization_methods/
│   │   ├── 04_stochastic_differential_equation_methods/
│   │   ├── 05_delay_differential_equation_methods/
│   │   ├── 06_fractional_differential_equation_methods/
│   │   ├── 07_boundary_value_problem_methods/
│   │   └── 08_multirate_and_parallel_in_time_methods/
│   ├── benchmarks/
│   │   ├── 01_ODE_nonstiff_accuracy_and_nonlinear_dynamics/
│   │   ├── 02_ODE_stiff_multiscale_and_chemical_kinetics/
│   │   ├── 03_Hamiltonian_geometric_and_long_time_mechanics/
│   │   ├── 04_DAE_constrained_systems_and_circuits/
│   │   ├── 05_PDE_method_of_lines_and_conservation_laws/
│   │   ├── 06_SDE_stochastic_differential_equations/
│   │   ├── 07_DDE_delay_differential_equations/
│   │   └── 08_Fractional_BVP_hybrid_and_event_driven_systems/
│   ├── tutorials/
│   └── references.md
├── src/
│   ├── config/
│   │   ├── default_options.m
│   │   ├── method_registry.m
│   │   └── benchmark_registry.m
│   ├── core/
│   │   ├── run_benchmark.m
│   │   ├── compute_metrics.m
│   │   ├── newton_solve.m
│   │   └── other shared execution utilities
│   ├── methods/
│   │   ├── 01_ODE_initial_value_integrators/
│   │   ├── 02_DAE_integrators_and_constraint_methods/
│   │   ├── 03_PDE_time_integration_and_spatial_discretization_methods/
│   │   ├── 04_stochastic_differential_equation_methods/
│   │   ├── 05_delay_differential_equation_methods/
│   │   ├── 06_fractional_differential_equation_methods/
│   │   ├── 07_boundary_value_problem_methods/
│   │   └── 08_multirate_and_parallel_in_time_methods/
│   ├── benchmarks/
│   │   ├── 01_ODE_nonstiff_accuracy_and_nonlinear_dynamics/
│   │   ├── 02_ODE_stiff_multiscale_and_chemical_kinetics/
│   │   ├── 03_Hamiltonian_geometric_and_long_time_mechanics/
│   │   ├── 04_DAE_constrained_systems_and_circuits/
│   │   ├── 05_PDE_method_of_lines_and_conservation_laws/
│   │   ├── 06_SDE_stochastic_differential_equations/
│   │   ├── 07_DDE_delay_differential_equations/
│   │   └── 08_Fractional_BVP_hybrid_and_event_driven_systems/
│   └── plotting/
├── tests/
│   └── test_smoke.m
└── results/
```

The `docs/` and `src/` folders intentionally mirror each other: method documentation categories correspond to method implementation categories, and benchmark documentation categories correspond to benchmark implementation categories.

---

## Method documentation categories

The methods catalog is organized by numerical method family, not by implementation status.

| Folder | Meaning |
|---|---|
| `01_ODE_initial_value_integrators/` | ODE IVP methods, including explicit RK, adaptive RK, implicit methods, BDF/NDF, Adams, Rosenbrock, exponential, IMEX, splitting, symplectic, structural dynamics, adaptivity, nonlinear solves, and linear algebra/backsolve machinery. |
| `02_DAE_integrators_and_constraint_methods/` | DAE integrators, mass-matrix methods, constraint stabilization, SHAKE/RATTLE-type methods, and DAE initialization ideas. |
| `03_PDE_time_integration_and_spatial_discretization_methods/` | PDE method-of-lines, finite difference, finite volume, finite element, spectral, WENO/TVD, ADI, semi-Lagrangian, and related PDE schemes. |
| `04_stochastic_differential_equation_methods/` | SDE and stochastic reaction methods, including Euler-Maruyama, Milstein, stochastic RK, tau-leaping, and Gillespie-style simulation. |
| `05_delay_differential_equation_methods/` | DDE method-of-steps, RK with history interpolation, neutral DDEs, and state-dependent delay methods. |
| `06_fractional_differential_equation_methods/` | Fractional ODE/PDE and memory-kernel methods such as L1, Grünwald-Letnikov, convolution quadrature, and fast memory approximations. |
| `07_boundary_value_problem_methods/` | Shooting, multiple shooting, collocation, finite-difference BVP, continuation, and pseudo-arclength continuation methods. |
| `08_multirate_and_parallel_in_time_methods/` | Multirate RK, MRI-GARK, waveform relaxation, Parareal, PFASST, and parallel-in-time approaches. |

The ODE folder contains additional subfolders for more precise method families:

```text
01_explicit_one_step_and_low_order_RK
02_adaptive_high_order_extrapolation_and_stabilized_RK
03_implicit_one_step_collocation_and_DIRK
04_linear_multistep_BDF_NDF_Adams_and_predictor_corrector
05_Rosenbrock_Wanner_and_linearly_implicit_stiff_methods
06_exponential_and_integrating_factor_methods
07_IMEX_additive_and_operator_splitting_methods
08_geometric_symplectic_and_energy_preserving_methods
09_second_order_mechanical_and_structural_dynamics_methods
10_adaptivity_events_jacobians_and_mass_matrix_support
11_nonlinear_solvers_for_implicit_methods
12_linear_algebra_backsolves_and_preconditioners
```

---

## Benchmark documentation categories

The benchmark catalog is also organized by problem family.

| Folder | Benchmark focus |
|---|---|
| `01_ODE_nonstiff_accuracy_and_nonlinear_dynamics/` | Smooth nonlinear ODEs, chaos, oscillation, predator-prey dynamics, epidemic models, and exact-solution tests. |
| `02_ODE_stiff_multiscale_and_chemical_kinetics/` | Stiff ODEs, chemical kinetics, multiscale transients, stiff reaction-diffusion reductions, and solver robustness tests. |
| `03_Hamiltonian_geometric_and_long_time_mechanics/` | Hamiltonian systems, conservative mechanics, orbital problems, geometric integration, energy drift, and long-time qualitative behavior. |
| `04_DAE_constrained_systems_and_circuits/` | Differential-algebraic equations, constrained mechanics, circuit DAEs, equilibrium constraints, and algebraic residual diagnostics. |
| `05_PDE_method_of_lines_and_conservation_laws/` | PDE-derived ODE systems, heat/wave/advection problems, Burgers-type equations, reaction-diffusion, conservation laws, and stiffness from spatial discretization. |
| `06_SDE_stochastic_differential_equations/` | Stochastic differential equations, stochastic population models, Langevin-type dynamics, and sample-path/statistical error diagnostics. |
| `07_DDE_delay_differential_equations/` | Retarded and delayed systems, delayed feedback control, delayed epidemic models, and history interpolation tests. |
| `08_Fractional_BVP_hybrid_and_event_driven_systems/` | Fractional dynamics, boundary-value problems, event handling, hybrid dynamics, switching systems, and discontinuities. |

---

## Implemented versus planned entries

Registry entries distinguish between runnable implementations and planned/scaffolded entries.

- **Implemented** means the MATLAB runner can execute the method or benchmark by default.
- **Planned** means the documentation and file structure exist, but the method or benchmark should not be treated as a validated implementation yet.
- **Solver-internal components** such as Newton iterations, Jacobian strategies, LU factorizations, Krylov methods, and preconditioners are not always time integrators by themselves. They are included because they are essential for serious stiff, implicit, DAE, and PDE solver benchmarking.

To inspect the current registry from MATLAB:

```matlab
methods = method_registry();
benchmarks = benchmark_registry();

implementedMethods = methods([methods.implemented]);
implementedBenchmarks = benchmarks([benchmarks.implemented]);

{implementedMethods.name}'
{implementedBenchmarks.name}'
```

---

## How execution works

`run_all.m` performs the following steps:

1. Loads default options from `default_options.m`.
2. Adds the repository root and subfolders to the MATLAB path.
3. Loads method and benchmark registries.
4. Filters out planned methods and planned benchmarks by default.
5. Runs applicable method/benchmark combinations.
6. Writes tables and plots when enabled.
7. Optionally writes a global summary table.

Default behavior:

```matlab
opts.include_planned_methods = false;
opts.include_planned_benchmarks = false;
```

This protects normal runs from failing on future scaffold files.

---

## Differential equation classes represented

| Type | Example form | Typical benchmark use |
|---|---|---|
| ODE | `y' = f(t,y)` | control, mechanics, circuits, chemical kinetics, chaos |
| Stiff ODE | `y' = f(t,y)` with separated time scales | implicit methods, BDF/NDF, Rosenbrock, Radau, SDIRK |
| Hamiltonian ODE | `q' = ∂H/∂p`, `p' = -∂H/∂q` | symplectic methods, energy drift, long-time orbits |
| DAE | `F(t,y,y') = 0` | constrained mechanics, circuits, process systems |
| PDE after discretization | `u_t = L(u)` or `M y' = f(y)` | method of lines, stiffness, conservation laws |
| SDE | `dX = a(X)dt + b(X)dW` | stochastic stability, weak/strong convergence |
| DDE | `x'(t)=f(t,x(t),x(t-τ))` | delay systems, history interpolation |
| Fractional DE | Caputo or Grünwald-Letnikov derivatives | memory effects and fractional diffusion |
| BVP | `y' = f(x,y)`, boundary constraints | shooting, collocation, continuation |
| Hybrid/event-driven system | continuous flow plus jumps/switching | event detection and discontinuity handling |

---

## Metrics emphasized

The benchmark framework is designed to compare both numerical accuracy and solver mechanics.

| Metric | Meaning |
|---|---|
| `final_error` | Error at final time against exact or high-accuracy reference solution. |
| `max_error` | Maximum trajectory error over the comparison window. |
| `rmse_error` | Root-mean-square trajectory error. |
| `cpu_time` | MATLAB wall-clock execution time. |
| `n_steps` | Accepted step count or output-step count, depending on method. |
| `nfev` | Number of right-hand-side evaluations. |
| `n_rejected` | Rejected adaptive steps. |
| `n_jacobian` | Jacobian evaluations. |
| `n_newton` | Newton or nonlinear iterations for implicit methods. |
| `n_linear_solve` | Linear solves/backsolves used inside implicit or linearly implicit methods. |
| `max_invariant_error` | Drift in mass, energy, angular momentum, or other invariants. |
| `positivity_violation` | Violation of nonnegative state constraints, when applicable. |
| `constraint_error` | DAE or geometric constraint residual, when applicable. |
| `status` | Success, skipped, non-applicable, blow-up, or failure status. |

CPU time alone is not enough for solver comparison. For stiff and implicit methods, Jacobian evaluations, Newton iterations, rejected steps, linear solves, and factorization/backsolve counts are often more informative.

---

## Generated plots

Depending on benchmark and method applicability, plotting utilities may generate:

- solution trajectories,
- error versus time,
- final-error bar charts,
- CPU-time bar charts,
- function-evaluation bar charts,
- work-precision diagrams,
- invariant drift plots,
- positivity or constraint-error plots,
- phase portraits,
- state-space projections,
- orbit plots,
- attractor projections.

---

## Interpretation guide

There is no universal best integrator.

A meaningful comparison is problem-dependent:

- Explicit RK methods are often strong for smooth non-stiff ODEs.
- Adaptive RK methods are useful when automatic local-error control is needed.
- BDF/NDF, Radau, SDIRK, and Rosenbrock-type methods are important for stiff systems.
- Symplectic and variational methods are important for long-time Hamiltonian mechanics.
- Exponential and IMEX methods are important for split stiff/nonstiff systems and PDE semi-discretizations.
- DAE methods require constraint-residual and consistent-initialization diagnostics.
- SDE methods require strong/weak convergence and statistical diagnostics, not only deterministic trajectory error.
- PDE benchmarks require attention to both spatial and temporal discretization error.

---

## Adding a new method

To add a method consistently:

1. Add or update the Markdown file under the correct folder in `docs/methods/`.
2. Add the MATLAB implementation under the matching folder in `src/methods/`.
3. Register the method in `src/config/method_registry.m`.
4. Set `implemented = true` only after the method is runnable and tested.
5. Define method applicability clearly, for example:
   - `all_first_order`,
   - `stiff_first_order`,
   - `mechanical_separable`,
   - `dae`,
   - `sde`,
   - `dde`,
   - `pde_mol`.
6. Run smoke tests and at least one representative benchmark.

---

## Adding a new benchmark

To add a benchmark consistently:

1. Add or update the Markdown file under the correct folder in `docs/benchmarks/`.
2. Add the MATLAB benchmark definition under the matching folder in `src/benchmarks/`.
3. Register it in `src/config/benchmark_registry.m`.
4. Define:
   - right-hand side or residual,
   - default initial condition,
   - time interval,
   - parameter regimes,
   - exact/reference solution strategy,
   - invariants or constraints,
   - recommended plots,
   - method applicability.
5. Set `implemented = true` only when the benchmark can run through the framework.

---

## Suggested MATLAB workflow

Run a quick smoke test:

```matlab
runtests('tests')
```

Run all currently implemented combinations:

```matlab
run_all
```

Run with custom options:

```matlab
opts = default_options();
opts.h = 5e-3;
opts.n_output = 2001;
opts.write_plots = true;
opts.write_tables = true;

results = run_one_benchmark('VanDerPolOscillator', opts);
```

Inspect registries:

```matlab
methods = method_registry();
benchmarks = benchmark_registry();

sum([methods.implemented])
sum([benchmarks.implemented])
```

---

## Documentation policy

Each method document should describe:

- category,
- intended MATLAB file,
- mathematical formulation,
- update formula or residual form,
- accuracy/order,
- stability behavior,
- solver requirements,
- strengths and weaknesses,
- best-use cases,
- metrics relevant to the method.

Each benchmark document should describe:

- governing equation,
- initial/boundary conditions,
- exact or reference solution if available,
- stiffness, invariants, constraints, positivity, or qualitative behavior,
- pseudocode for the right-hand side or residual,
- proposed/implemented MATLAB file,
- recommended metrics and plots.

---

## Simulation video

A simulation video for the repository is available on YouTube:

<a href="https://www.youtube.com/watch?v=lpxKCCUKyiY" target="_blank">
  <img
    src="https://i.ytimg.com/vi/lpxKCCUKyiY/maxresdefault.jpg"
    alt="Differential Equation Integrator Benchmarks in MATLAB"
    style="max-width: 100%; border-radius: 10px; box-shadow: 0 6px 18px rgba(0,0,0,0.18); margin-top: 0.5rem;"
  />
</a>

---

## MATLAB version

The code is written in plain MATLAB style and avoids Simulink dependencies. It should run on recent MATLAB releases. Some plotting details may require minor adjustment on very old MATLAB versions.

---

## License

This project is released under the MIT License. See [`LICENSE`](LICENSE).

---

## Citation

If this repository helps your teaching, benchmarking, or research workflow, please cite it using the metadata in [`CITATION.cff`](CITATION.cff).
