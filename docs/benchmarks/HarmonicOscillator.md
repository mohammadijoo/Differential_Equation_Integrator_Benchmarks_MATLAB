# Harmonic Oscillator

## Equation

The harmonic oscillator is the canonical mathematical model of motion around a stable equilibrium. In its first-order form, the benchmark equation is

$$ q' = v, \qquad v' = -\omega^2 q. $$

Here:

- $q(t)$ is position or displacement,
- $v(t)$ is velocity,
- $\omega$ is the natural angular frequency in radians per unit time.

The same model can be written as one second-order ODE. Since

$$ v=q', $$

we have

$$ v'=q''. $$

Therefore the first-order system becomes

$$ q'' = -\omega^2q, $$

or

$$ q''+\omega^2q=0. $$

This is the standard undamped harmonic oscillator equation.

### Mechanical interpretation

The most common physical example is a mass attached to a linear spring. Let:

- $m$ be the mass,
- $k$ be the spring stiffness,
- $q(t)$ be displacement from equilibrium.

Hooke's law gives the restoring force

$$ F=-kq. $$

Newton's second law gives

$$ F=mq''. $$

Therefore

$$ mq''=-kq, $$

or

$$ mq''+kq=0. $$

Dividing by $m$ gives

$$ q''+\frac{k}{m}q=0. $$

Thus

$$ \omega = \sqrt{\frac{k}{m}}. $$

A larger stiffness $k$ produces faster oscillations. A larger mass $m$ produces slower oscillations.

### Exact analytical solution

The ODE is

$$ q''+\omega^2q=0. $$

Assume a trial solution

$$ q(t)=e^{rt}. $$

Then

$$ q'(t)=re^{rt}, \qquad q''(t)=r^2e^{rt}. $$

Substitution gives

$$ r^2e^{rt}+\omega^2e^{rt}=0. $$

Since $e^{rt}\neq0$,

$$ r^2+\omega^2=0. $$

The characteristic roots are

$$ r=\pm i\omega. $$

Therefore the general real-valued solution is

$$ q(t)=C_1\cos(\omega t)+C_2\sin(\omega t). $$

The velocity is

$$ v(t)=q'(t)=-C_1\omega\sin(\omega t)+C_2\omega\cos(\omega t). $$

For initial conditions

$$ q(0)=q_0, \qquad v(0)=v_0, $$

we get

$$ C_1=q_0, \qquad C_2=\frac{v_0}{\omega}. $$

So the initial-condition solution is

$$ q(t)=q_0\cos(\omega t)+\frac{v_0}{\omega}\sin(\omega t). $$

The velocity is

$$ v(t)=-q_0\omega\sin(\omega t)+v_0\cos(\omega t). $$

### Amplitude, phase, period, and frequency

The solution can also be written as

$$ q(t)=A\cos(\omega t+\phi), $$

where $A$ is the amplitude and $\phi$ is the phase shift.

For the initial conditions $q_0$ and $v_0$,

$$ A=\sqrt{q_0^2+(\frac{v_0}{\omega})^2}. $$

The period is

$$ T=\frac{2\pi}{\omega}. $$

The ordinary frequency is

$$ f=\frac{1}{T}=\frac{\omega}{2\pi}. $$

Thus $\omega$ determines how rapidly the oscillator cycles, while the initial condition determines the amplitude and phase.

### Matrix form

Define the state vector

$$ y=(q,v)^T. $$

Then

$$ q'=v,\qquad v'=-\omega^2 q. $$

This can be written as a linear system

$$ \dot{y}=Ay, $$

where

$$ A=[0,1; -\omega^2,0]. $$

The eigenvalues of $A$ satisfy

$$ det(rI-A)=0. $$

That gives

$$ r^2+\omega^2=0, $$

so

$$ r_{1,2}=\pm i\omega. $$

The eigenvalues are purely imaginary. This means the continuous system is oscillatory and non-decaying.

### Energy conservation

For the mass-spring oscillator, the total energy is

$$ E=T+V, $$

where

$$ T=\frac{1}{2}mv^2 $$

is kinetic energy and

$$ V=\frac{1}{2}kq^2 $$

is spring potential energy. Therefore

$$ E=\frac{1}{2}mv^2+\frac{1}{2}kq^2. $$

In normalized form with $m=1$ and $k=\omega^2$,

$$ E(q,v)=\frac{1}{2}v^2+\frac{1}{2}\omega^2q^2. $$

Differentiate the energy:

$$ \frac{dE}{dt}=v v' + \omega^2 q q'. $$

Using

$$ q'=v, \qquad v'=-\omega^2q, $$

we obtain

$$ \frac{dE}{dt}=v(-\omega^2q)+\omega^2q(v)=0. $$

Thus

$$ E(t)=E(0). $$

This is the defining feature of the undamped oscillator: it exchanges kinetic and potential energy, but the total energy remains constant.

### Phase portrait

The energy equation

$$ \frac{1}{2}v^2+\frac{1}{2}\omega^2q^2=E $$

can be rewritten as

$$ v^2+\omega^2q^2=2E. $$

This is an ellipse in the $(q,v)$ phase plane. Therefore, exact trajectories are closed curves. The oscillator repeatedly returns to the same state after one period.

This makes the harmonic oscillator a strong benchmark for phase accuracy and long-time qualitative behavior. A numerical method may produce the correct short-time motion but slowly spiral outward or inward in the phase plane. Outward spiraling corresponds to artificial energy growth. Inward spiraling corresponds to artificial numerical damping.

### Stability interpretation

The undamped harmonic oscillator is Lyapunov stable but not asymptotically stable.

It is stable because small initial conditions stay small. Energy conservation implies

$$ \frac{1}{2}v(t)^2+\frac{1}{2}\omega^2q(t)^2 = \frac{1}{2}v_0^2+\frac{1}{2}\omega^2q_0^2. $$

So the solution remains bounded for all time.

However, the solution does not converge to zero unless the initial condition is exactly zero. Therefore

$$ (q(t),v(t))\not\to(0,0) $$

for nonzero initial conditions. This is why the system is not asymptotically stable.

### Numerical integration issues

For a time step $h$, Forward Euler gives

$$ q_{n+1}=q_n+h v_n, $$

$$ v_{n+1}=v_n-h\omega^2q_n. $$

This method does not preserve the energy ellipse. In fact, for the harmonic oscillator it tends to increase energy, causing the numerical phase portrait to spiral outward.

A symplectic Euler variant can be written as

$$ v_{n+1}=v_n-h\omega^2q_n, $$

$$ q_{n+1}=q_n+h v_{n+1}. $$

This method does not conserve the exact energy, but it better respects the geometric structure of Hamiltonian motion and often produces bounded long-time energy error.

This difference is one reason the harmonic oscillator is more revealing than a simple final-time error test.

### Pseudocode for the right-hand side

```text
Given state y = [q, v] and parameter omega:
    dqdt = v
    dvdt = -omega^2 * q
    return [dqdt, dvdt]
```

For the normalized invariant:

```text
Given state y = [q, v] and parameter omega:
    E = 0.5 * v^2 + 0.5 * omega^2 * q^2
    return E
```

### Main benchmark lesson

The harmonic oscillator tests whether a numerical method can preserve oscillatory structure. Good performance is not only about small pointwise error. It is also about correct period, correct phase, bounded energy behavior, and a faithful phase portrait over long integrations.

## Implemented MATLAB file

```text
src/benchmarks/benchmark_harmonic_oscillator.m
```

## Historical background

The harmonic oscillator is one of the fundamental models of mechanics, vibration, circuits, and wave phenomena. Its exact solution is periodic and conserves quadratic energy.

## Mathematical properties

It is ideal for comparing energy drift, phase error, and phase portraits. Symplectic and energy-preserving methods should show clear advantages over dissipative or unstable methods.

## Why it is a benchmark

This problem is included because it exposes numerical behavior that may be hidden in simpler tests. It allows comparison of:

- accuracy,
- stability,
- stiffness handling,
- phase error,
- conservation-law drift,
- positivity or physical admissibility,
- computational cost.

## Real-world applications

Depending on the equation, applications include control systems, mechanical vibration, circuits, chemical kinetics, atmospheric dynamics, celestial mechanics, robotics, and computational physics.

## Metrics emphasized in this repository

- final error,
- maximum trajectory error,
- RMS error,
- CPU time,
- function evaluations,
- failure/blow-up status,
- invariant drift when applicable,
- qualitative plots such as phase portraits or attractor projections.

## Recommended plots

- solution versus time,
- error versus time,
- work-precision diagram,
- invariant error versus time when applicable,
- phase portrait or orbit plot when applicable.

## References

See [`../references.md`](../references.md).
