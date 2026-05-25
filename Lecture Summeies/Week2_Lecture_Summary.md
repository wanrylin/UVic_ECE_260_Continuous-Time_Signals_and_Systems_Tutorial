# ECE 260 Week 2 Lecture Summary

Continuous-Time Signals and Systems  
Videos 4-10: mappings, signal properties, transformations, elementary signals

This summary is meant as a compact reference after watching the lectures. It is
not a replacement for the tutorial handout. The tutorial will focus more on how
to apply these ideas to assignment-style questions.

---

## 1. Signals, Functions, and Mappings

A mapping assigns each element in a domain to exactly one element in a codomain:

$$
f: A \to B
$$

In signals and systems, the main objects are all mappings in different forms:

- A function maps an independent variable to a value.
- A sequence maps an integer index to a value.
- A system operator maps an input signal to an output signal.
- A transform maps one representation of a signal to another representation.

### Function vs. Function Value

This distinction is important throughout the course:

- $x$ is the whole signal or function.
- $x(t)$ is the value of that signal at one time instant.

For example, convolution acts on complete functions, not on isolated scalar
values. A careful notation is

$$
y = x_1 * x_2
$$

or, when evaluating the result at time $t$,

$$
y(t) = (x_1 * x_2)(t).
$$

The common shorthand $y(t)=x_1(t)*x_2(t)$ is often seen in engineering, but it is
not mathematically precise.

### System Operators

A continuous-time SISO system can be represented as an operator $H$ that maps an
input function to an output function:

$$
H: \mathcal{F} \to \mathcal{F}.
$$

If the input signal is $x$, then:

- $Hx$ denotes the whole output signal.
- $(Hx)(t)$ denotes the value of the output signal at time $t$.

For cascaded systems, the rightmost operator acts first:

$$
H_2H_1x = H_2(H_1x).
$$

---

## 2. Signal Symmetry

### Even Signals

A signal $x$ is even if

$$
x(t)=x(-t), \qquad \forall t.
$$

Even signals are symmetric about the vertical axis.

### Odd Signals

A signal $x$ is odd if

$$
x(t)=-x(-t), \qquad \forall t.
$$

Odd signals have origin symmetry. If an odd signal is defined and finite at
$t=0$, then

$$
x(0)=0.
$$

### Conjugate-Symmetric Signals

For a complex-valued signal, conjugate symmetry means

$$
x(t)=x^*(-t), \qquad \forall t.
$$

Equivalently:

- $\mathrm{Re}\{x(t)\}$ is even.
- $\mathrm{Im}\{x(t)\}$ is odd.

The complex exponential $e^{j\omega t}=\cos(\omega t)+j\sin(\omega t)$ is a
standard example.

---

## 3. Periodicity

A continuous-time signal $x$ is periodic if there exists a positive number
$T>0$ such that

$$
x(t+T)=x(t), \qquad \forall t.
$$

The fundamental period $T_0$ is the smallest positive period. Then

$$
f_0=\frac{1}{T_0},
\qquad
\omega_0=\frac{2\pi}{T_0}.
$$

Here $f_0$ is measured in Hz, while $\omega_0$ is measured in rad/s.

### Sum of Periodic Signals

If $x_1$ and $x_2$ have fundamental periods $T_1$ and $T_2$, then

$$
y(t)=x_1(t)+x_2(t)
$$

is periodic if the ratio $T_1/T_2$ is rational. If

$$
\frac{T_1}{T_2}=\frac{q}{r},
$$

where $q$ and $r$ are positive coprime integers, then a common period is

$$
T_0 = rT_1 = qT_2.
$$

In practice: find the smallest time at which all components repeat together.

---

## 4. Time Transformations

Independent-variable transformations change the time axis.

### Time Shift

$$
y(t)=x(t-b).
$$

- If $b>0$, the signal is shifted right by $b$.
- If $b<0$, the signal is shifted left by $|b|$.

### Time Reversal

$$
y(t)=x(-t).
$$

This reflects the signal across the vertical axis.

### Time Scaling

$$
y(t)=x(at), \qquad a>0.
$$

- If $a>1$, the signal is compressed in time.
- If $0<a<1$, the signal is stretched in time.

If $a<0$, time reversal is also involved.

### Combined Transformation

For

$$
y(t)=x(at-b),
$$

factor the argument when helpful:

$$
at-b = a\left(t-\frac{b}{a}\right).
$$

Two equivalent ways to think about the transformation:

1. Shift first, then scale:

   $$
   v(t)=x(t-b), \qquad y(t)=v(at).
   $$

2. Scale first, then shift:

   $$
   w(t)=x(at), \qquad y(t)=w\left(t-\frac{b}{a}\right).
   $$

The second view is often easier for graphing because the final time shift is
$b/a$.

### Amplitude Transformations

Dependent-variable transformations change the vertical values:

$$
y(t)=a x(t)
$$

scales the amplitude, and

$$
y(t)=x(t)+b
$$

shifts the signal vertically.

---

## 5. Even/Odd Decomposition

Every signal can be written as the sum of an even part and an odd part:

$$
x(t)=x_e(t)+x_o(t).
$$

The formulas are

$$
x_e(t)=\frac{1}{2}\left[x(t)+x(-t)\right],
$$

$$
x_o(t)=\frac{1}{2}\left[x(t)-x(-t)\right].
$$

Quick checks:

$$
x_e(-t)=x_e(t),
\qquad
x_o(-t)=-x_o(t).
$$

This decomposition is useful when a problem asks for symmetry, sketching, or
integral simplification.

---

## 6. Bounded, Energy, and Power Signals

### Bounded Signals

A signal $x$ is bounded if there exists a finite constant $M>0$ such that

$$
|x(t)| \le M, \qquad \forall t.
$$

Examples:

- $\sin t$ and $\cos t$ are bounded.
- $t^2$ is unbounded.
- $\tan t$ is unbounded because it has vertical asymptotes.

### Energy

The total energy of a continuous-time signal is

$$
E = \int_{-\infty}^{\infty}|x(t)|^2\,dt.
$$

A signal is an energy signal if

$$
0<E<\infty.
$$

Finite-energy signals have average power equal to zero.

### Average Power

The average power is

$$
P = \lim_{T\to\infty}\frac{1}{2T}
\int_{-T}^{T}|x(t)|^2\,dt.
$$

A signal is a power signal if

$$
0<P<\infty.
$$

Periodic nonzero signals, such as sinusoids, are typical power signals.

---

## 7. Complex Exponentials

The general continuous-time complex exponential has the form

$$
x(t)=Ae^{\lambda t},
$$

where $A$ and $\lambda$ may be complex. If

$$
\lambda=\sigma+j\omega,
$$

then

$$
x(t)=Ae^{(\sigma+j\omega)t}
=Ae^{\sigma t}e^{j\omega t}.
$$

Using Euler's formula,

$$
e^{j\omega t}=\cos(\omega t)+j\sin(\omega t).
$$

Interpretation:

- $\sigma>0$: exponential envelope grows.
- $\sigma=0$: constant envelope.
- $\sigma<0$: exponential envelope decays.
- $\omega\ne0$: oscillation is present.

So $\sigma$ controls growth/decay, while $\omega$ controls oscillation.

---

## 8. Elementary Signals

### Unit Step

The unit step is

$$
u(t)=
\begin{cases}
1, & t\ge0,\\
0, & t<0.
\end{cases}
$$

In this course, the convention is $u(0)=1$.

### Signum Function

$$
\mathrm{sgn}(t)=
\begin{cases}
1, & t>0,\\
0, & t=0,\\
-1, & t<0.
\end{cases}
$$

For $t\ne0$,

$$
\mathrm{sgn}(t)=2u(t)-1.
$$

This identity does not hold at $t=0$ under the convention $u(0)=1$.

### Rectangular Pulse

The unit rectangular pulse is commonly defined as

$$
\mathrm{rect}(t)=
\begin{cases}
1, & -\frac{1}{2}\le t<\frac{1}{2},\\
0, & \text{otherwise}.
\end{cases}
$$

### Cardinal Sine

In these lectures, the sinc function is defined as

$$
\mathrm{sinc}(t)=\frac{\sin t}{t}, \qquad t\ne0.
$$

At the origin, define the value by the limit:

$$
\mathrm{sinc}(0)=
\lim_{t\to0}\frac{\sin t}{t}=1.
$$

Note: some DSP texts use the normalized definition
$\sin(\pi t)/(\pi t)$. Always check the course convention.

---

## 9. Dirac Delta

The Dirac delta $\delta(t)$ is not an ordinary function. It is treated as a
generalized function or distribution.

Its two key properties are

$$
\delta(t)=0, \qquad t\ne0,
$$

and

$$
\int_{-\infty}^{\infty}\delta(t)\,dt=1.
$$

The number attached to an impulse arrow is its weight or area, not its height.
For example, $5\delta(t)$ has impulse weight $5$.

### Equivalence Property

If $x$ is continuous at $t_0$, then

$$
x(t)\delta(t-t_0)=x(t_0)\delta(t-t_0).
$$

### Sifting Property

If the impulse lies inside the integration interval, then

$$
\int_{-\infty}^{\infty}x(t)\delta(t-t_0)\,dt=x(t_0).
$$

For a running integral,

$$
\int_{-\infty}^{t}\delta(\tau-2)\,d\tau
=
\begin{cases}
0, & t<2,\\
1, & t\ge2,
\end{cases}
=u(t-2).
$$

The boundary value is consistent with the course convention $u(0)=1$.

---

## 10. Representing Piecewise Signals with Unit Steps

Unit steps can turn pieces of a signal on and off. A window active on
$[a,b)$ is

$$
u(t-a)-u(t-b).
$$

Therefore, a piecewise signal can often be written as a sum of windowed pieces.

Example:

$$
x(t)=
\begin{cases}
t, & 0\le t<1,\\
1, & 1\le t<2,\\
3-t, & 2\le t<3,\\
0, & \text{otherwise}.
\end{cases}
$$

Use one window for each active interval:

$$
x(t)
=t[u(t)-u(t-1)]
+[u(t-1)-u(t-2)]
+(3-t)[u(t-2)-u(t-3)].
$$

After collecting terms,

$$
x(t)
=t u(t)
-(t-1)u(t-1)
-(t-2)u(t-2)
+(t-3)u(t-3).
$$

This form is useful because it removes explicit cases and makes later
operations, such as integration or transforms, easier to organize.

---

## Common Checks for This Week

- Are you treating $x$ as a whole signal and $x(t)$ as one value?
- For $x(at-b)$, did you account for both scaling and shifting?
- For symmetry, did you compare $x(t)$ with $x(-t)$?
- For periodic sums, did all components repeat at the same time?
- For impulses, are you using area/weight rather than height?
- For unit-step expressions, do the windows turn on and off at the correct
  breakpoints?
