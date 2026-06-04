# ECE 260 Week 5 Lecture Summary

LTI System Properties and the Motivation for Transforms  
Slides 116-122: invertibility, BIBO stability, eigenfunctions, and the start of
continuous-time Fourier series

This summary is intended as a student-facing review aid. It is not a substitute
for the textbook, lecture slides, course website, or official announcements.

---

## 1. Where This Week Fits

Last week, we used impulse responses to describe continuous-time LTI systems:

```math
y=x\ast h.
```

This week adds three important questions:

- When can an LTI system be undone?
- When is an LTI system BIBO stable?
- How can we avoid computing convolution directly?

The final question motivates the next major topic: transforms, beginning with
continuous-time Fourier series.

---

## 2. Invertibility of LTI Systems

An LTI system is invertible if there exists another LTI system that reverses
its effect.

Let $h$ be the impulse response of the original system, and let
$h_{\mathrm{inv}}$ be the impulse response of the inverse system. Cascading the
two systems should produce the identity system, whose impulse response is
$\delta(t)$.

Therefore, the condition for invertibility is

```math
h\ast h_{\mathrm{inv}}=\delta.
```

So an LTI system with impulse response $h$ is invertible if and only if we can
find some $h_{\mathrm{inv}}$ satisfying this convolution equation.

### Example: Scaled and Shifted Delta

Suppose

```math
h(t)=a\delta(t-t_{0}),
\qquad
a\ne0.
```

This system scales the input by $a$ and delays it by $t_{0}$:

```math
x(t)\ast a\delta(t-t_{0})=a x(t-t_{0}).
```

To undo it, we need to scale by $1/a$ and shift in the opposite direction:

```math
h_{\mathrm{inv}}(t)=\frac{1}{a}\delta(t+t_{0}).
```

Check:

```math
\begin{aligned}
h\ast h_{\mathrm{inv}}
&=
a\delta(t-t_{0})
\ast
\frac{1}{a}\delta(t+t_{0})\\
&=
\delta(t-t_{0})\ast\delta(t+t_{0})\\
&=
\delta(t).
\end{aligned}
```

Thus the system is invertible.

### Key Takeaway

Invertibility for LTI systems becomes a convolution problem:

```math
h\ast h_{\mathrm{inv}}=\delta.
```

In simple delta-function cases, this is easy. In general, it can be difficult.

---

## 3. BIBO Stability of LTI Systems

For an LTI system, BIBO stability has a clean impulse-response test.

An LTI system is BIBO stable if and only if

```math
\int_{-\infty}^{\infty}|h(t)|\,dt<\infty.
```

In words: the impulse response must be absolutely integrable.

### Example: Exponential Impulse Response

Consider

```math
h(t)=e^{at}u(t),
```

where $a$ is real.

Since $u(t)$ restricts the signal to $t\ge0$,

```math
\int_{-\infty}^{\infty}|h(t)|\,dt
=
\int_{0}^{\infty}e^{at}\,dt.
```

Now check cases:

- If $a<0$, the exponential decays and the integral is finite.
- If $a=0$, the integral becomes $\int_{0}^{\infty}1\,dt$, which diverges.
- If $a>0$, the exponential grows and the integral diverges.

Therefore,

```math
h(t)=e^{at}u(t)
```

is BIBO stable if and only if $a<0$.

### Example: Integrator

The integrator

```math
y(t)=\int_{-\infty}^{t}x(\tau)\,d\tau
```

has impulse response

```math
h(t)=u(t).
```

But

```math
\int_{-\infty}^{\infty}|u(t)|\,dt
=
\int_{0}^{\infty}1\,dt
=
\infty.
```

So the ideal integrator is not BIBO stable.

### Common Pitfall

Do not decide BIBO stability only by looking at whether $h(t)$ is bounded. The
correct test is absolute integrability.

---

## 4. Complex Exponentials as Eigenfunctions

For LTI systems, complex exponentials are special.

For an LTI system $\mathcal{H}$ with impulse response $h$,

```math
\mathcal{H}\{e^{st}\}(t)=H(s)e^{st},
```

where

```math
H(s)=
\int_{-\infty}^{\infty}h(t)e^{-st}\,dt.
```

The function $e^{st}$ is an eigenfunction of the LTI system, and $H(s)$ is the
corresponding eigenvalue. The function $H$ is called the system function or
transfer function.

### Why This Helps

If the input can be written as a linear combination of complex exponentials,

```math
x(t)=\sum_{k}a_{k}e^{s_{k}t},
```

then the output is

```math
y(t)=\sum_{k}a_{k}H(s_{k})e^{s_{k}t}.
```

This avoids direct convolution. Each exponential term simply gets multiplied by
$H(s_{k})$.

---

## 5. Example: Delay System

Suppose the impulse response is

```math
h(t)=\delta(t-1).
```

This system delays the input by $1$:

```math
y(t)=x(t-1).
```

The system function is

```math
\begin{aligned}
H(s)
&=
\int_{-\infty}^{\infty}\delta(t-1)e^{-st}\,dt\\
&=
e^{-s}.
\end{aligned}
```

Now let

```math
x(t)=\cos(\pi t).
```

Using Euler's formula,

```math
\cos(\pi t)
=
\frac{1}{2}e^{j\pi t}
+
\frac{1}{2}e^{-j\pi t}.
```

The system multiplies each exponential by $H(s)$:

```math
H(j\pi)=e^{-j\pi},
\qquad
H(-j\pi)=e^{j\pi}.
```

Therefore,

```math
\begin{aligned}
y(t)
&=
\frac{1}{2}e^{-j\pi}e^{j\pi t}
+
\frac{1}{2}e^{j\pi}e^{-j\pi t}\\
&=
\cos(\pi t-\pi).
\end{aligned}
```

This matches the time-domain interpretation:

```math
y(t)=x(t-1)=\cos(\pi(t-1))=\cos(\pi t-\pi).
```

---

## 6. Why Transforms Are Useful

In the time domain, an LTI system output is computed by convolution:

```math
y=x\ast h.
```

Convolution is powerful, but it is often algebraically tedious and easy to get
wrong.

Transforms give a different strategy:

1. Transform the input and system into another domain.
2. Replace convolution with multiplication.
3. Transform the answer back to the time domain.

The basic idea is

```math
y=x\ast h
\quad \longleftrightarrow \quad
Y(s)=X(s)H(s).
```

This is the motivation for studying the major transform tools in the rest of
the course:

- continuous-time Fourier series (CTFS);
- continuous-time Fourier transform (CTFT);
- Laplace transform.

---

## 7. Beginning of CT Fourier Series

The continuous-time Fourier series is a representation for periodic functions.

The main idea is to write a periodic signal as a linear combination of complex
sinusoids.

Complex sinusoids are useful because they are:

- easy to differentiate;
- easy to integrate;
- mathematically well behaved;
- eigenfunctions of LTI systems.

This last point is the big connection to LTI systems. If a periodic input can be
written as a sum of complex sinusoids, then an LTI system acts on each sinusoid
by multiplying it by the corresponding value of the system function.

---

## 8. Review Checklist

After this week, you should be able to:

- state the invertibility condition $h\ast h_{\mathrm{inv}}=\delta$;
- find the inverse of simple shifted-delta impulse responses;
- use absolute integrability to test BIBO stability;
- explain why the integrator is not BIBO stable;
- state why $e^{st}$ is an eigenfunction of any LTI system;
- use $H(s)$ to compute outputs for sums of complex exponentials;
- explain why transforms are introduced after convolution;
- describe CTFS as a representation of periodic signals using complex
  sinusoids.
