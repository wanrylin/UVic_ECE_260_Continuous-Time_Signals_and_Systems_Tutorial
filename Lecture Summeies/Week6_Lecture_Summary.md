# ECE 260 Week 6-7 Lecture Summary

Continuous-Time Fourier Series  
Slides 120-155: CTFS definition, coefficient calculation, convergence,
properties, and frequency spectra

This summary is intended as a student-facing review aid. It is not a substitute
for the textbook, lecture slides, course website, or official announcements.

---

## 1. Where This Topic Fits

In Chapter 4, complex exponentials appeared because they are eigenfunctions of
continuous-time LTI systems. Fourier series uses this fact in a systematic way:
instead of studying a periodic signal directly in time, we represent it as a
sum of harmonically related complex exponentials.

The key idea is:

- periodic signals can be decomposed into frequency components;
- each component is a complex sinusoid;
- the Fourier series coefficients tell us how much of each component is
  present.

This gives a bridge from the time domain to the frequency domain.

---

## 2. Harmonically Related Complex Sinusoids

A set of complex sinusoids is harmonically related if all frequencies are
integer multiples of one fundamental frequency $\omega_{0}$.

The standard set is

```math
\phi_{k}(t)=e^{jk\omega_{0}t},
\qquad
k\in\mathbb{Z}.
```

The frequency of the $k$th component is $k\omega_{0}$. A linear combination of
these components is periodic with period

```math
T=\frac{2\pi}{\omega_{0}}.
```

For a periodic signal with fundamental period $T$,

```math
\omega_{0}=\frac{2\pi}{T}.
```

---

## 3. CT Fourier Series Equations

For a periodic signal $x$ with fundamental period $T$, the complex exponential
Fourier series is

```math
x(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t}.
```

This is the synthesis equation: it reconstructs the signal from the
coefficients.

The coefficients are found from

```math
c_{k}
=
\frac{1}{T}
\int_{T}
x(t)e^{-jk\omega_{0}t}\,dt.
```

Here $\int_{T}$ means integration over any interval of length $T$. This is the
analysis equation: it extracts the coefficient sequence.

We write the CTFS pair as

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k}.
```

### Important Note About the Integral

The integration interval can be chosen for convenience. For a rectangular pulse
centered at the origin, a centered interval is often easiest. For a signal
defined on $0\le t<T$, the interval $[0,T)$ is often easiest.

Endpoint values at isolated discontinuities do not change the coefficient
integral.

---

## 4. Example: Square Wave Coefficients

Suppose $x$ has period $T$ and

```math
x(t)=
\begin{cases}
A, & 0\le t<T/2,\\
-A, & T/2\le t<T.
\end{cases}
```

Then

```math
c_{k}
=
\frac{1}{T}
\left[
\int_{0}^{T/2}Ae^{-jk\omega_{0}t}\,dt
+
\int_{T/2}^{T}(-A)e^{-jk\omega_{0}t}\,dt
\right].
```

For $k=0$, the average value is zero:

```math
c_{0}=0.
```

For $k\ne0$, using $\omega_{0}=2\pi/T$ gives

```math
c_{k}
=
\frac{A}{j\pi k}
\left[1-(-1)^{k}\right].
```

Therefore,

```math
c_{k}
=
\begin{cases}
-j\dfrac{2A}{\pi k}, & k\ \mathrm{odd},\\
0, & k\ \mathrm{even}.
\end{cases}
```

This square wave has only odd harmonics. The coefficient magnitudes decay like
$1/|k|$.

---

## 5. Example: Periodic Impulse Train

Suppose $x$ has period $T=3$, and over one centered period
$-1.5\le t<1.5$,

```math
x(t)=\delta(t-1)-\delta(t+1).
```

Then

```math
\omega_{0}=\frac{2\pi}{3}.
```

Using the CTFS analysis equation,

```math
\begin{aligned}
c_{k}
&=
\frac{1}{3}
\int_{-1.5}^{1.5}
\left[\delta(t-1)-\delta(t+1)\right]
e^{-jk\omega_{0}t}\,dt\\
&=
\frac{1}{3}
\left[
e^{-jk\omega_{0}}
-
e^{jk\omega_{0}}
\right].
\end{aligned}
```

Therefore,

```math
c_{k}
=
-j\frac{2}{3}
\sin\left(\frac{2\pi k}{3}\right).
```

The main skill here is recognizing that an impulse inside an integral samples
the other factor.

---

## 6. Convergence of Fourier Series

Because the Fourier series may have infinitely many terms, convergence matters.

Define the truncated Fourier series

```math
x_{N}(t)=
\sum_{k=-N}^{N}
c_{k}e^{jk\omega_{0}t}.
```

We ask whether $x_{N}$ approaches $x$ as $N\to\infty$.

### Pointwise Equality

Pointwise equality means the signals agree at every time:

```math
x(t)=y(t)
\qquad
\mathrm{for\ all}\ t.
```

### MSE Equality

MSE equality means the squared error has zero energy:

```math
\int |x(t)-y(t)|^{2}\,dt=0.
```

Pointwise equality is stronger than MSE equality. Two signals can differ at an
isolated point and still be equal in the MSE sense.

### Uniform Convergence

If convergence is pointwise and the rate of convergence is the same everywhere,
the convergence is uniform.

This is a strong condition. Signals with jump discontinuities usually do not
have uniform convergence.

### Two Useful Convergence Facts

If $x$ is continuous and the coefficients are absolutely summable,

```math
\sum_{k=-\infty}^{\infty}|c_{k}|<\infty,
```

then the Fourier series converges uniformly.

If $x$ has finite energy over one period,

```math
\int_{T}|x(t)|^{2}\,dt<\infty,
```

then the Fourier series converges in the MSE sense. This condition is often
easy to satisfy in practice, but it does not tell us the exact pointwise value
at each time.

---

## 7. Dirichlet Conditions

The Dirichlet conditions are a practical test for pointwise Fourier-series
convergence.

Over one period, $x$ should:

- be absolutely integrable;
- have a finite number of maxima and minima;
- have a finite number of finite jump discontinuities.

In formula form, the first condition is

```math
\int_{T}|x(t)|\,dt<\infty.
```

If $x$ satisfies the Dirichlet conditions, then the Fourier series converges to
$x(t)$ at points where $x$ is continuous.

At a jump discontinuity $t_{a}$, the Fourier series converges to the average of
the left and right limits:

```math
\widetilde{x}(t_{a})
=
\frac{1}{2}
\left[
x(t_{a}^{-})+x(t_{a}^{+})
\right].
```

For example, if a signal jumps from $0$ to $1$, the Fourier series converges to
$1/2$ exactly at the jump.

---

## 8. Gibbs Phenomenon

For signals with discontinuities, a truncated Fourier series often has ripples
near the jump.

As $N$ increases in

```math
x_{N}(t)=
\sum_{k=-N}^{N}
c_{k}e^{jk\omega_{0}t},
```

the ripples become more compressed toward the discontinuity. However, the peak
overshoot does not disappear for any finite $N$.

This behavior is called Gibbs phenomenon.

Key interpretation:

- away from discontinuities, the approximation improves quickly;
- near discontinuities, convergence is slow;
- at the discontinuity, the limiting value is the midpoint of the jump.

---

## 9. Useful CTFS Properties

The slides include a longer table of CTFS properties. The properties below are
the most useful first-pass tools for this part of the course.

Assume

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ a_{k},
\qquad
y(t)\ \mathrm{CTFS}\longleftrightarrow\ b_{k}.
```

### Linearity

If $x$ and $y$ have the same period, then

```math
\alpha x(t)+\beta y(t)
\ \mathrm{CTFS}\longleftrightarrow\
\alpha a_{k}+\beta b_{k}.
```

This is useful when a signal is built as a sum of simpler periodic signals.

### Time Shifting

If

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k},
```

then

```math
x(t-t_{0})
\ \mathrm{CTFS}\longleftrightarrow\
e^{-jk\omega_{0}t_{0}}c_{k}.
```

A time shift changes phase, but not magnitude.

### Frequency Shifting

If $M$ is an integer, then

```math
e^{jM\omega_{0}t}x(t)
\ \mathrm{CTFS}\longleftrightarrow\
c_{k-M}.
```

Multiplication by a harmonically related complex exponential shifts the
coefficient sequence.

### Time Reversal

```math
x(-t)
\ \mathrm{CTFS}\longleftrightarrow\
c_{-k}.
```

### Conjugation

```math
x^{*}(t)
\ \mathrm{CTFS}\longleftrightarrow\
c_{-k}^{*}.
```

### Symmetry

Even and odd symmetry match between the time-domain signal and the coefficient
sequence:

```math
x(t)\ \mathrm{even}
\quad\Longleftrightarrow\quad
c_{k}\ \mathrm{even},
```

```math
x(t)\ \mathrm{odd}
\quad\Longleftrightarrow\quad
c_{k}\ \mathrm{odd}.
```

For a real-valued signal,

```math
c_{k}=c_{-k}^{*}.
```

This is conjugate symmetry. As a result,

```math
|c_{k}|=|c_{-k}|,
\qquad
\angle c_{k}=-\angle c_{-k}.
```

So for real signals, the magnitude spectrum is even and the phase spectrum is
odd.

### Zeroth Coefficient

The coefficient $c_{0}$ is the average value of $x$ over one period:

```math
c_{0}
=
\frac{1}{T}
\int_{T}x(t)\,dt.
```

This is often the fastest way to find $c_{0}$.

---

## 10. Trigonometric Forms for Real Signals

If $x$ is real, the complex exponential Fourier series can also be written in
real trigonometric forms.

Combined trigonometric form:

```math
x(t)
=
c_{0}
+
2\sum_{k=1}^{\infty}
|c_{k}|
\cos(k\omega_{0}t+\theta_{k}),
```

where

```math
\theta_{k}=\angle c_{k}.
```

Trigonometric form:

```math
x(t)
=
c_{0}
+
\sum_{k=1}^{\infty}
\left[
\alpha_{k}\cos(k\omega_{0}t)
+
\beta_{k}\sin(k\omega_{0}t)
\right],
```

where

```math
\alpha_{k}=2\mathrm{Re}\{c_{k}\},
\qquad
\beta_{k}=-2\mathrm{Im}\{c_{k}\}.
```

These forms contain only real-valued sinusoids, so they are often easier to
interpret physically.

---

## 11. Frequency Spectra

The Fourier series coefficients describe how the signal's information is
distributed across frequency.

Write each coefficient in polar form:

```math
c_{k}=|c_{k}|e^{j\angle c_{k}}.
```

Then

```math
x(t)
=
\sum_{k=-\infty}^{\infty}
|c_{k}|e^{j(k\omega_{0}t+\angle c_{k})}.
```

The $k$th term is a complex sinusoid at frequency $k\omega_{0}$.

- $|c_{k}|$ is the strength of that frequency component.
- $\angle c_{k}$ gives its phase.
- Frequencies occur only at integer multiples of $\omega_{0}$.

Because the spectrum has values only at discrete frequencies, CTFS spectra are
usually plotted as line spectra.

### Square Wave Spectrum

For the square wave from Section 4,

```math
c_{k}
=
\begin{cases}
-j\dfrac{2A}{\pi k}, & k\ \mathrm{odd},\\
0, & k\ \mathrm{even}.
\end{cases}
```

The magnitude spectrum is

```math
|c_{k}|
=
\begin{cases}
\dfrac{2A}{\pi |k|}, & k\ \mathrm{odd},\\
0, & k\ \mathrm{even}.
\end{cases}
```

For odd nonzero $k$, the phase is

```math
\angle c_{k}
=
\begin{cases}
-\dfrac{\pi}{2}, & k>0,\\
\dfrac{\pi}{2}, & k<0.
\end{cases}
```

The largest nonzero magnitudes occur at $k=\pm1$, so the fundamental harmonic
is the dominant frequency component.

---

## 12. Common Pitfalls

- Do not forget the factor $1/T$ in the analysis equation.
- Do not confuse $k$ with frequency. The actual frequency is $k\omega_{0}$.
- Do not assume the Fourier series equals the original signal at jump
  discontinuities. It converges to the midpoint of the jump.
- Do not plot phase where $c_{k}=0$; phase is undefined there.
- For real signals, negative-index coefficients are not new information; they
  are determined by conjugate symmetry.
- For $c_{0}$, use the average value whenever possible.

---

## 13. Review Checklist

After these lectures, you should be able to:

- state the CTFS synthesis and analysis equations;
- identify the fundamental period $T$ and fundamental frequency $\omega_{0}$;
- compute CTFS coefficients using direct integration;
- use impulse sifting inside CTFS coefficient integrals;
- explain pointwise, uniform, and MSE convergence;
- apply the Dirichlet discontinuity midpoint rule;
- describe Gibbs phenomenon;
- use basic CTFS properties such as linearity, shifting, reversal, conjugation,
  and symmetry;
- recognize that $c_{0}$ is the average value;
- convert between complex exponential and real trigonometric forms for real
  signals;
- interpret magnitude and phase spectra as line spectra.
