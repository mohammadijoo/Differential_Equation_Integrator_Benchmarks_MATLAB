# Kepler Two-Body Problem

## Equation

The Kepler two-body problem describes the motion of a body under an inverse-square central gravitational force. In first-order vector form, the benchmark equation is

$$ r' = v, \qquad v' = -\mu \frac{r}{|r|^3}. $$

Here:

- $r(t) \in \mathbb{R}^2$ or $R^3$ is the position vector,
- $v(t) \in \mathbb{R}^2$ or $R^3$ is the velocity vector,
- $\mu>0$ is the gravitational parameter,
- $|r|$ is the Euclidean distance from the attracting center.

The parameter $\mu$ is often written as

$$ \mu=G(M+m), $$

where $G$ is the gravitational constant, $M$ is the central mass, and $m$ is the orbiting mass. In many normalized numerical tests, $\mu$ is set to $1$.

Since

$$ r'=v, $$

we have

$$ r''=v'. $$

Therefore the second-order equation is

$$ r''=-\mu\frac{r}{|r|^3}. $$

This is Newton's inverse-square law in vector form.

### Meaning of the force term

The vector

$$ \frac{r}{|r|} $$

points radially outward from the central body. The acceleration term

$$ -\mu\frac{r}{|r|^3} $$

points radially inward because of the negative sign.

The magnitude of the acceleration is

$$ |-\mu\frac{r}{|r|^3}| = \mu\frac{|r|}{|r|^3} = \frac{\mu}{|r|^2}. $$

Thus the force magnitude decays like the inverse square of distance.

### Hamiltonian structure

The Kepler problem is a conservative Hamiltonian system. The total specific mechanical energy is

$$ E(r,v)=\frac{1}{2}|v|^2-\frac{\mu}{|r|}. $$

The first term is kinetic energy per unit mass. The second term is gravitational potential energy per unit mass.

To prove conservation of energy, differentiate:

$$ \frac{dE}{dt} = v\cdot v' - \mu \frac{d}{dt}(\frac{1}{|r|}). $$

Now

$$ \frac{d}{dt}(\frac{1}{|r|}) = -\frac{r\cdot r'}{|r|^3}. $$

Since $r'=v$,

$$ \frac{d}{dt}(\frac{1}{|r|}) = -\frac{r\cdot v}{|r|^3}. $$

Therefore

$$ \frac{dE}{dt} = v\cdot(-\mu\frac{r}{|r|^3}) +\mu\frac{r\cdot v}{|r|^3}. $$

The two terms cancel:

$$ \frac{dE}{dt}=0. $$

So

$$ E(t)=E(0). $$

Energy drift is one of the most important diagnostics for this benchmark.

### Angular momentum conservation

In three dimensions, angular momentum per unit mass is

$$ L=r\times v. $$

Differentiate:

$$ \frac{dL}{dt}=r'\times v+r\times v'. $$

Since $r'=v$,

$$ r'\times v=v\times v=0. $$

Also,

$$ v'=-\mu\frac{r}{|r|^3}, $$

so

$$ r\times v'=r\times(-\mu\frac{r}{|r|^3})=0, $$

because the cross product of parallel vectors is zero. Therefore

$$ \frac{dL}{dt}=0. $$

Angular momentum conservation implies that the motion stays in a fixed plane. In two-dimensional simulations, the scalar angular momentum is

$$ L_z = x v_y - y v_x. $$

A numerical method should preserve this quantity well over long integrations.

### Orbit types

The sign of the energy determines the orbit type.

If

$$ E<0, $$

the orbit is bounded and elliptical.

If

$$ E=0, $$

the trajectory is parabolic escape.

If

$$ E>0, $$

the trajectory is hyperbolic escape.

For an elliptical orbit, the semi-major axis $a$ satisfies

$$ E=-\frac{\mu}{2a}. $$

Thus energy error translates directly into orbital size error. A numerical integrator with systematic energy drift may cause an artificial inward spiral or outward spiral.

### Circular orbit as a special case

For a circular orbit of radius $R$, the gravitational acceleration magnitude is

$$ \frac{\mu}{R^2}. $$

Centripetal acceleration is

$$ \frac{v^2}{R}. $$

Equating them gives

$$ \frac{v^2}{R}=\frac{\mu}{R^2}. $$

Therefore

$$ v=\sqrt{\frac{\mu}{R}}. $$

The angular frequency is

$$ \omega=\frac{v}{R}=\sqrt{\frac{\mu}{R^3}}. $$

The period is

$$ T=2\pi\sqrt{\frac{R^3}{\mu}}. $$

This is the circular-orbit version of Kepler's third law.

### Phase and orbital drift

For long-time integration, the most important error may not be immediate blow-up. Instead, a solver may produce a slowly drifting orbit:

- the ellipse may precess artificially,
- the orbital period may be wrong,
- the radius may slowly grow or shrink,
- energy may drift monotonically,
- angular momentum may drift.

Even if the final position error is small for one orbit, a tiny period error can accumulate over hundreds or thousands of orbits. This makes the Kepler problem a strong long-time benchmark.

### Why symplectic methods matter

The Kepler problem is Hamiltonian. Hamiltonian systems have geometric structure, including conservation laws and phase-space volume preservation. Symplectic numerical methods are designed to preserve the symplectic structure.

A symplectic method does not necessarily conserve the exact energy at every step, but it often keeps the energy error bounded over long times. Non-symplectic methods may show monotone energy drift.

This distinction may not appear in short simulations, but it becomes clear in long orbital integrations.

### Singular behavior near collision

The acceleration term

$$ -\mu\frac{r}{|r|^3} $$

becomes singular as

$$ |r|\to 0. $$

Close approaches create large accelerations and may require small time steps. In many benchmark setups, initial conditions are chosen to avoid collision but still produce nontrivial orbital dynamics.

Highly eccentric orbits are harder than nearly circular ones because velocity and acceleration change rapidly near periapsis.

### Pseudocode for the right-hand side

```text
Given state y = [r, v] and parameter mu:
    radius = norm(r)
    drdt = v
    dvdt = -mu * r / radius^3
    return [drdt, dvdt]
```

For invariant diagnostics:

```text
Given position r, velocity v, and parameter mu:
    energy = 0.5 * dot(v, v) - mu / norm(r)
    angular_momentum = cross(r, v)
    return energy, angular_momentum
```

### Main benchmark lesson

The Kepler problem tests long-time orbital fidelity. It is not enough for a method to give a small short-time error. A high-quality integrator should avoid artificial spiraling, preserve angular momentum well, control energy drift, and maintain the correct orbital period and geometry over long integrations.

## Implemented MATLAB file

```text
src/benchmarks/benchmark_kepler_two_body.m
```

## Historical background

The Kepler problem is the central-force two-body problem associated with Kepler's planetary laws and Newtonian gravitation.

## Mathematical properties

It tests long-term orbital stability, energy conservation, angular momentum conservation, and phase/orbital drift. Symplectic methods should perform well.

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
