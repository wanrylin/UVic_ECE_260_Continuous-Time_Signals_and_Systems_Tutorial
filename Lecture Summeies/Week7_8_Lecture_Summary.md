# ECE 260 Week 7-8 Lecture Summary

Fourier Series with LTI Systems and Continuous-Time Fourier Transform  
Slides 156-206: frequency response, filtering, CTFT definition, convergence,
properties, periodic functions, spectra, and bandwidth

This summary is intended as a student-facing review aid. It is not a substitute
for the textbook, lecture slides, course website, video lectures, or official
announcements.

---

## 1. Where These Lectures Fit

Continuous-time Fourier series represents a periodic signal as a sum of
harmonically related complex sinusoids:

```math
x(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t}.
```

This representation is especially useful for LTI systems because complex
sinusoids are eigenfunctions of every LTI system. Each frequency component
passes through the system independently and is multiplied by one complex
number.

Fourier series is limited to periodic signals. The continuous-time Fourier
transform extends the same frequency-domain viewpoint to both aperiodic and
periodic signals.

The main progression is

```math
\mathrm{CTFS}
\quad\longrightarrow\quad
\mathrm{LTI\ filtering}
\quad\longrightarrow\quad
\mathrm{CTFT}.
```

---

## 2. Frequency Response of an LTI System

Let an LTI system have impulse response $h$. If the input is the complex
sinusoid

```math
x(t)=e^{j\omega t},
```

then the output is

```math
y(t)=H(\omega)e^{j\omega t},
```

where

```math
H(\omega)
=
\int_{-\infty}^{\infty}
h(t)e^{-j\omega t}\,dt.
```

The function $H$ is the **frequency response** of the system.

The important interpretation is:

- the output remains at the same frequency $\omega$;
- $|H(\omega)|$ changes the amplitude;
- $\angle H(\omega)$ changes the phase.

The system does not create a new frequency when the input is one complex
sinusoid.

---

## 3. Fourier Series Through an LTI System

Suppose the input is $T$-periodic and has the CTFS representation

```math
x(t)
=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t},
\qquad
\omega_{0}=\frac{2\pi}{T}.
```

Each harmonic is an eigenfunction of the LTI system, so

```math
y(t)
=
\sum_{k=-\infty}^{\infty}
c_{k}H(k\omega_{0})e^{jk\omega_{0}t}.
```

Therefore, if

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k},
```

then

```math
y(t)\ \mathrm{CTFS}\longleftrightarrow\ d_{k},
\qquad
d_{k}=H(k\omega_{0})c_{k}.
```

This is one of the most useful formulas in the course. It replaces
time-domain convolution with coefficient-by-coefficient multiplication.

### Standard Route

1. Find the input coefficients $c_{k}$.
2. Identify the harmonic frequencies $k\omega_{0}$.
3. Evaluate $H(k\omega_{0})$ at those frequencies.
4. Compute $d_{k}=H(k\omega_{0})c_{k}$.
5. Reconstruct $y(t)$ if a time-domain answer is required.

### Example: Ideal Highpass Filtering

Suppose

```math
x(t)
=
1+2\cos(2t)+2\cos(4t)+\frac{1}{2}\cos(6t)
```

passes through

```math
H(\omega)=
\begin{cases}
1, & |\omega|\ge5,\\
0, & \mathrm{otherwise}.
\end{cases}
```

The input contains components at

```math
\omega=0,\ \pm2,\ \pm4,\ \pm6.
```

The filter removes the components at $0$, $\pm2$, and $\pm4$, while retaining
the components at $\pm6$. Therefore,

```math
y(t)=\frac{1}{2}\cos(6t).
```

---

## 4. Basic Frequency-Selective Filters

Filtering means modifying the frequency spectrum of a signal. A
frequency-selective filter passes some frequency components and attenuates
others.

### Ideal Lowpass Filter

```math
H(\omega)=
\begin{cases}
1, & |\omega|\le\omega_{c},\\
0, & \mathrm{otherwise}.
\end{cases}
```

It keeps low-frequency components near $\omega=0$ and removes sufficiently
high-frequency components.

### Ideal Highpass Filter

```math
H(\omega)=
\begin{cases}
1, & |\omega|\ge\omega_{c},\\
0, & \mathrm{otherwise}.
\end{cases}
```

It removes low-frequency components and keeps sufficiently high-frequency
components.

### Ideal Bandpass Filter

```math
H(\omega)=
\begin{cases}
1, & \omega_{c1}\le|\omega|\le\omega_{c2},\\
0, & \mathrm{otherwise}.
\end{cases}
```

It keeps a selected band of frequencies and removes frequencies outside that
band.

The region where $H(\omega)$ passes components is the **passband**. The region
where it suppresses components is the **stopband**.

---

## 5. Why We Need the Fourier Transform

A Fourier series is inherently periodic, so it cannot directly represent a
general aperiodic signal.

To motivate the Fourier transform, imagine repeating an aperiodic signal with
period $T$. As $T\to\infty$:

- the fundamental frequency $\omega_{0}=2\pi/T$ approaches zero;
- the spacing between harmonics approaches zero;
- the discrete set of Fourier-series frequencies becomes a continuous
  frequency variable;
- the Fourier-series summation becomes an integral.

The resulting representation is the continuous-time Fourier transform.

Fourier series uses a discrete coefficient sequence $c_{k}$. Fourier transform
uses a continuous function $X(\omega)$.

---

## 6. CT Fourier Transform Equations

The forward CT Fourier transform is

```math
X(\omega)
=
\int_{-\infty}^{\infty}
x(t)e^{-j\omega t}\,dt.
```

The inverse CT Fourier transform is

```math
x(t)
=
\frac{1}{2\pi}
\int_{-\infty}^{\infty}
X(\omega)e^{j\omega t}\,d\omega.
```

The transform pair is written as

```math
x(t)\ \mathrm{CTFT}\longleftrightarrow\ X(\omega).
```

The roles of the two equations are:

- **analysis:** use $x(t)$ to find $X(\omega)$;
- **synthesis:** use $X(\omega)$ to reconstruct $x(t)$.

### Classical and Generalized Fourier Transforms

For some important signals, the ordinary transform integral does not converge
as a classical integral. Examples include:

- a nonzero constant;
- a periodic signal;
- the unit step $u(t)$;
- the signum signal $\mathrm{sgn}(t)$.

The generalized Fourier transform uses impulses and related generalized
functions to include these signals. In this course, the classical and
generalized cases use the same transform notation.

---

## 7. Core CTFT Pairs

The following pairs form a useful starting table.

```math
\delta(t)
\ \mathrm{CTFT}\longleftrightarrow\
1
```

```math
1
\ \mathrm{CTFT}\longleftrightarrow\
2\pi\delta(\omega)
```

```math
e^{j\omega_{0}t}
\ \mathrm{CTFT}\longleftrightarrow\
2\pi\delta(\omega-\omega_{0})
```

```math
\cos(\omega_{0}t)
\ \mathrm{CTFT}\longleftrightarrow\
\pi
\left[
\delta(\omega-\omega_{0})
+
\delta(\omega+\omega_{0})
\right]
```

```math
\sin(\omega_{0}t)
\ \mathrm{CTFT}\longleftrightarrow\
\frac{\pi}{j}
\left[
\delta(\omega-\omega_{0})
-
\delta(\omega+\omega_{0})
\right]
```

For $T>0$,

```math
\mathrm{rect}\left(\frac{t}{T}\right)
\ \mathrm{CTFT}\longleftrightarrow\
T\,\mathrm{sinc}\left(\frac{T\omega}{2}\right).
```

For $\mathrm{Re}\{a\}>0$,

```math
e^{-at}u(t)
\ \mathrm{CTFT}\longleftrightarrow\
\frac{1}{a+j\omega}.
```

The sinc convention used here is

```math
\mathrm{sinc}(x)=\frac{\sin x}{x},
\qquad
\mathrm{sinc}(0)=1.
```

Always check the sinc convention. MATLAB's built-in `sinc` uses a different,
normalized definition.

---

## 8. Direct CTFT Examples

### Example 1: Shifted Impulse

Find the Fourier transform of

```math
x(t)=A\delta(t-t_{0}).
```

Substitute into the analysis equation:

```math
\begin{aligned}
X(\omega)
&=
\int_{-\infty}^{\infty}
A\delta(t-t_{0})e^{-j\omega t}\,dt\\
&=
Ae^{-j\omega t_{0}}.
\end{aligned}
```

Therefore,

```math
A\delta(t-t_{0})
\ \mathrm{CTFT}\longleftrightarrow\
Ae^{-j\omega t_{0}}.
```

A time shift of an impulse creates a frequency-dependent phase factor.

### Example 2: Rectangular Pulse

Let

```math
x(t)=\mathrm{rect}\left(\frac{t}{T}\right),
\qquad
T>0.
```

The signal is nonzero on $-T/2\le t\le T/2$, so

```math
\begin{aligned}
X(\omega)
&=
\int_{-T/2}^{T/2}
e^{-j\omega t}\,dt\\
&=
\frac{e^{-j\omega T/2}-e^{j\omega T/2}}{-j\omega}\\
&=
\frac{2\sin(\omega T/2)}{\omega}\\
&=
T\,\mathrm{sinc}\left(\frac{\omega T}{2}\right).
\end{aligned}
```

At $\omega=0$, use the limit $\mathrm{sinc}(0)=1$, giving

```math
X(0)=T.
```

This also equals the area under the time-domain pulse.

---

## 9. Convergence of the Fourier Transform

The inverse transform may reconstruct a signal in different senses. The
convergence results closely resemble those for Fourier series.

### Finite-Energy Case

If

```math
\int_{-\infty}^{\infty}
|x(t)|^{2}\,dt<\infty,
```

then the Fourier-transform representation converges to $x$ in the
mean-squared-error sense.

This guarantees zero error energy, but it does not necessarily guarantee
equality at every individual time.

### Dirichlet Conditions

A practical sufficient set of conditions is:

1. $x$ is absolutely integrable:

```math
\int_{-\infty}^{\infty}|x(t)|\,dt<\infty.
```

2. On every finite interval, $x$ has a finite number of maxima and minima.
3. On every finite interval, $x$ has a finite number of finite
   discontinuities.

If the Dirichlet conditions hold, the inverse transform converges to $x(t)$ at
points where $x$ is continuous.

At a jump discontinuity $t_{a}$, it converges to

```math
\widetilde{x}(t_{a})
=
\frac{1}{2}
\left[
x(t_{a}^{-})+x(t_{a}^{+})
\right].
```

### Example: Edge of a Rectangular Pulse

If a rectangular pulse jumps between $0$ and $1$, then at either edge the
Fourier-transform representation converges to

```math
\frac{0+1}{2}=\frac{1}{2}.
```

Changing the assigned value of the original signal at one isolated
discontinuity does not change its Fourier transform.

---

## 10. CTFT Property Table

Assume

```math
x_{1}(t)\ \mathrm{CTFT}\longleftrightarrow\ X_{1}(\omega),
\qquad
x_{2}(t)\ \mathrm{CTFT}\longleftrightarrow\ X_{2}(\omega).
```

### Linearity

```math
a_{1}x_{1}(t)+a_{2}x_{2}(t)
\ \mathrm{CTFT}\longleftrightarrow\
a_{1}X_{1}(\omega)+a_{2}X_{2}(\omega).
```

### Time Shifting

```math
x(t-t_{0})
\ \mathrm{CTFT}\longleftrightarrow\
e^{-j\omega t_{0}}X(\omega).
```

### Frequency Shifting

```math
e^{j\omega_{0}t}x(t)
\ \mathrm{CTFT}\longleftrightarrow\
X(\omega-\omega_{0}).
```

### Time Scaling

For real $a\ne0$,

```math
x(at)
\ \mathrm{CTFT}\longleftrightarrow\
\frac{1}{|a|}
X\left(\frac{\omega}{a}\right).
```

### Conjugation

```math
x^{*}(t)
\ \mathrm{CTFT}\longleftrightarrow\
X^{*}(-\omega).
```

### Duality

```math
X(t)
\ \mathrm{CTFT}\longleftrightarrow\
2\pi x(-\omega).
```

### Time-Domain Convolution

```math
(x_{1}\ast x_{2})(t)
\ \mathrm{CTFT}\longleftrightarrow\
X_{1}(\omega)X_{2}(\omega).
```

### Time-Domain Multiplication

```math
x_{1}(t)x_{2}(t)
\ \mathrm{CTFT}\longleftrightarrow\
\frac{1}{2\pi}
(X_{1}\ast X_{2})(\omega).
```

### Time-Domain Differentiation

```math
\frac{d}{dt}x(t)
\ \mathrm{CTFT}\longleftrightarrow\
j\omega X(\omega).
```

More generally,

```math
\frac{d^{n}}{dt^{n}}x(t)
\ \mathrm{CTFT}\longleftrightarrow\
(j\omega)^{n}X(\omega).
```

### Frequency-Domain Differentiation

```math
tx(t)
\ \mathrm{CTFT}\longleftrightarrow\
j\frac{d}{d\omega}X(\omega).
```

### Time-Domain Integration

```math
\int_{-\infty}^{t}x(\tau)\,d\tau
\ \mathrm{CTFT}\longleftrightarrow\
\frac{1}{j\omega}X(\omega)
+
\pi X(0)\delta(\omega).
```

### Parseval's Relation

```math
\int_{-\infty}^{\infty}|x(t)|^{2}\,dt
=
\frac{1}{2\pi}
\int_{-\infty}^{\infty}|X(\omega)|^{2}\,d\omega.
```

---

## 11. How to Use the Main Properties

### 11.1 Time Shift Changes Phase

If

```math
x(t)\ \mathrm{CTFT}\longleftrightarrow\ X(\omega),
```

then delaying the signal gives

```math
x(t-t_{0})
\ \mathrm{CTFT}\longleftrightarrow\
e^{-j\omega t_{0}}X(\omega).
```

The magnitude does not change because

```math
\left|e^{-j\omega t_{0}}\right|=1.
```

Therefore, time shifting changes the phase spectrum but not the magnitude
spectrum.

For example,

```math
A\cos(\omega_{0}t+\theta)
\ \mathrm{CTFT}\longleftrightarrow\
\pi A
\left[
e^{j\theta}\delta(\omega-\omega_{0})
+
e^{-j\theta}\delta(\omega+\omega_{0})
\right].
```

### 11.2 Modulation Shifts the Spectrum

Multiplication by a complex sinusoid shifts the spectrum:

```math
e^{j\omega_{c}t}x(t)
\ \mathrm{CTFT}\longleftrightarrow\
X(\omega-\omega_{c}).
```

Since

```math
\cos(\omega_{c}t)
=
\frac{1}{2}e^{j\omega_{c}t}
+
\frac{1}{2}e^{-j\omega_{c}t},
```

we obtain the especially useful result

```math
x(t)\cos(\omega_{c}t)
\ \mathrm{CTFT}\longleftrightarrow\
\frac{1}{2}
\left[
X(\omega-\omega_{c})
+
X(\omega+\omega_{c})
\right].
```

Multiplication by a cosine creates two shifted copies of the original
spectrum.

### 11.3 Time Compression Expands Frequency

If $|a|>1$, then $x(at)$ is compressed in time. Its transform is

```math
\frac{1}{|a|}
X\left(\frac{\omega}{a}\right),
```

which is expanded in frequency and reduced in amplitude.

For example,

```math
\mathrm{rect}(at)
\ \mathrm{CTFT}\longleftrightarrow\
\frac{1}{|a|}
\mathrm{sinc}\left(\frac{\omega}{2a}\right).
```

Do not forget the amplitude factor $1/|a|$.

### 11.4 Duality Produces New Pairs

Starting from

```math
\mathrm{rect}(t)
\ \mathrm{CTFT}\longleftrightarrow\
\mathrm{sinc}\left(\frac{\omega}{2}\right),
```

duality gives

```math
\mathrm{sinc}\left(\frac{t}{2}\right)
\ \mathrm{CTFT}\longleftrightarrow\
2\pi\mathrm{rect}(\omega).
```

Duality exchanges the roles of time and frequency, but it also introduces a
factor of $2\pi$ and a reversal.

### 11.5 Convolution Becomes Multiplication

If

```math
y(t)=x(t)\ast h(t),
```

then

```math
Y(\omega)=X(\omega)H(\omega).
```

This is the CTFT version of frequency-domain LTI-system analysis. The system
frequency response is the Fourier transform of its impulse response:

```math
H(\omega)
=
\int_{-\infty}^{\infty}
h(t)e^{-j\omega t}\,dt.
```

### 11.6 Multiplication Becomes Convolution

If

```math
y(t)=x_{1}(t)x_{2}(t),
```

then

```math
Y(\omega)
=
\frac{1}{2\pi}
(X_{1}\ast X_{2})(\omega).
```

This direction can be tedious because it creates a convolution integral. When
one factor is a sinusoid, frequency shifting is usually the faster route.

### 11.7 Differentiation and Integration

Differentiation in time becomes multiplication by $j\omega$:

```math
\frac{d}{dt}\delta(t)
\ \mathrm{CTFT}\longleftrightarrow\
j\omega.
```

Multiplication by time becomes differentiation in frequency:

```math
t\cos(\omega_{0}t)
\ \mathrm{CTFT}\longleftrightarrow\
j\frac{d}{d\omega}
\left\{
\pi
\left[
\delta(\omega-\omega_{0})
+
\delta(\omega+\omega_{0})
\right]
\right\}.
```

Using the integration property with

```math
\delta(t)\ \mathrm{CTFT}\longleftrightarrow\ 1
```

gives

```math
u(t)
\ \mathrm{CTFT}\longleftrightarrow\
\frac{1}{j\omega}+\pi\delta(\omega).
```

The impulse term must not be omitted.

### 11.8 Parseval's Relation

Parseval's relation allows signal energy to be computed in whichever domain is
easier.

For example,

```math
\mathrm{sinc}\left(\frac{t}{2}\right)
\ \mathrm{CTFT}\longleftrightarrow\
2\pi\mathrm{rect}(\omega).
```

Therefore,

```math
\begin{aligned}
E
&=
\int_{-\infty}^{\infty}
\left|
\mathrm{sinc}\left(\frac{t}{2}\right)
\right|^{2}\,dt\\
&=
\frac{1}{2\pi}
\int_{-\infty}^{\infty}
\left|2\pi\mathrm{rect}(\omega)\right|^{2}\,d\omega\\
&=
2\pi.
\end{aligned}
```

This avoids directly integrating a squared sinc function.

---

## 12. Symmetry Properties

The Fourier transform preserves even and odd symmetry:

```math
x(t)\ \mathrm{even}
\quad\Longleftrightarrow\quad
X(\omega)\ \mathrm{even},
```

```math
x(t)\ \mathrm{odd}
\quad\Longleftrightarrow\quad
X(\omega)\ \mathrm{odd}.
```

If $x$ is real, then

```math
X(\omega)=X^{*}(-\omega).
```

This is conjugate symmetry. It implies

```math
|X(\omega)|=|X(-\omega)|
```

and

```math
\angle X(\omega)=-\angle X(-\omega).
```

Therefore, for a real signal:

- the magnitude spectrum is even;
- the phase spectrum is odd;
- the negative-frequency spectrum is determined by the positive-frequency
  spectrum.

Some useful special cases are:

- real and even $x(t)$ gives real and even $X(\omega)$;
- real and odd $x(t)$ gives imaginary and odd $X(\omega)$.

A real time-domain signal does **not** necessarily have a real Fourier
transform.

---

## 13. Fourier Transform of Periodic Signals

A periodic signal generally does not have a classical Fourier transform
because it has infinite duration and usually infinite energy. Its generalized
Fourier transform is a weighted train of impulses.

Suppose $x$ has period $T$, fundamental frequency

```math
\omega_{0}=\frac{2\pi}{T},
```

and CTFS coefficients $a_{k}$:

```math
x(t)
=
\sum_{k=-\infty}^{\infty}
a_{k}e^{jk\omega_{0}t}.
```

Then

```math
X(\omega)
=
\sum_{k=-\infty}^{\infty}
2\pi a_{k}\delta(\omega-k\omega_{0}).
```

Each Fourier-series harmonic becomes an impulse in the Fourier-transform
domain.

### One-Period Method

Define $x_{T}$ as one period of $x$, set to zero outside that interval, and let

```math
x_{T}(t)\ \mathrm{CTFT}\longleftrightarrow\ X_{T}(\omega).
```

Then

```math
a_{k}
=
\frac{1}{T}X_{T}(k\omega_{0}).
```

Thus, the CTFS coefficients are obtained by:

1. taking the CTFT of one isolated period;
2. sampling it at $\omega=k\omega_{0}$;
3. scaling the samples by $1/T$.

### Example: Periodic Rectangular Pulse Train

Suppose one period contains a centered pulse of width $\tau$ and height $1$.
The isolated pulse is

```math
x_{T}(t)
=
\mathrm{rect}\left(\frac{t}{\tau}\right),
```

so

```math
X_{T}(\omega)
=
\tau\,\mathrm{sinc}\left(\frac{\tau\omega}{2}\right).
```

The CTFS coefficients are

```math
\begin{aligned}
a_{k}
&=
\frac{1}{T}X_{T}(k\omega_{0})\\
&=
\frac{\tau}{T}
\mathrm{sinc}\left(
\frac{k\omega_{0}\tau}{2}
\right)\\
&=
\frac{\tau}{T}
\mathrm{sinc}\left(
\frac{k\pi\tau}{T}
\right).
\end{aligned}
```

Its generalized Fourier transform is

```math
X(\omega)
=
\sum_{k=-\infty}^{\infty}
2\pi a_{k}\delta(\omega-k\omega_{0}).
```

---

## 14. Frequency Spectrum, Magnitude, and Phase

Write the inverse Fourier transform using polar form:

```math
\begin{aligned}
x(t)
&=
\frac{1}{2\pi}
\int_{-\infty}^{\infty}
X(\omega)e^{j\omega t}\,d\omega\\
&=
\frac{1}{2\pi}
\int_{-\infty}^{\infty}
|X(\omega)|
e^{j[\omega t+\angle X(\omega)]}\,d\omega.
\end{aligned}
```

This expresses $x(t)$ as a continuous combination of complex sinusoids.

- $X(\omega)$ is the **frequency spectrum**.
- $|X(\omega)|$ is the **magnitude spectrum**.
- $\angle X(\omega)$ is the **phase spectrum**.

The magnitude describes the relative strength of a frequency component. The
phase describes its relative shift.

For a periodic signal, the CTFT consists of impulses at discrete harmonic
frequencies. For an aperiodic signal, the CTFT can be nonzero over a continuous
range of frequencies.

### Example: Magnitude and Phase

Suppose

```math
X(\omega)=\frac{e^{-j\omega}}{j\omega},
\qquad
\omega\ne0.
```

The magnitude is

```math
|X(\omega)|=\frac{1}{|\omega|}.
```

The phase is

```math
\angle X(\omega)
=
-\omega-\frac{\pi}{2}\mathrm{sgn}(\omega),
```

up to equivalent additions of integer multiples of $2\pi$.

The magnitude is largest near $\omega=0$, so the signal is dominated by its
low-frequency content.

Do not assign or plot phase at a frequency where the spectrum is zero; phase
is undefined there.

---

## 15. Bandlimited Signals and Bandwidth

A signal is bandlimited if there is a finite $B$ such that

```math
X(\omega)=0
\qquad
\mathrm{for}\ |\omega|>B.
```

More generally, if the smallest interval containing the nonzero spectrum is

```math
[\omega_{1},\omega_{2}],
```

then its bandwidth is

```math
B=\omega_{2}-\omega_{1}.
```

For real-valued signals, negative frequencies are redundant because of
conjugate symmetry. Bandwidth is therefore usually described using only the
nonnegative-frequency side.

For a complex-valued signal, the full nonzero frequency interval may be
required because conjugate symmetry is not guaranteed.

An important theoretical fact is that a nonzero signal cannot be both exactly
time limited and exactly bandlimited.

---

## 16. A Reliable CTFT Problem-Solving Route

When asked to find a Fourier transform:

1. Identify whether the signal is periodic or aperiodic.
2. Check whether it matches a known transform pair.
3. Rewrite the signal as a transformed version of a known signal.
4. Apply one property at a time.
5. Track all scale factors, shifts, and signs.
6. Use symmetry and values such as $X(0)$ to check the result.

For a composite signal, intermediate variables can reduce errors:

```math
v_{1}(t)
\quad\longrightarrow\quad
v_{2}(t)
\quad\longrightarrow\quad
v_{3}(t)
\quad\longrightarrow\quad
x(t).
```

Apply the corresponding frequency-domain operation at each step instead of
trying to transform the complete expression mentally.

### Useful Checks

At zero frequency,

```math
X(0)
=
\int_{-\infty}^{\infty}x(t)\,dt.
```

So $X(0)$ should equal the signed area under $x(t)$ whenever the integral
exists.

If $x(t)$ is real, verify

```math
X(\omega)=X^{*}(-\omega).
```

If $x(t)$ is real and even, the final transform should be real and even.

---

## 17. Common Pitfalls

- Do not put the factor $1/(2\pi)$ in the forward transform. It belongs to
  the inverse transform under this course convention.
- Do not forget the absolute value in the scaling factor $1/|a|$.
- A time shift multiplies the spectrum by $e^{-j\omega t_{0}}$; it does not
  shift the spectrum horizontally.
- Multiplication by $e^{j\omega_{0}t}$ shifts the spectrum to
  $X(\omega-\omega_{0})$.
- Time-domain multiplication produces frequency-domain convolution with the
  factor $1/(2\pi)$.
- Time-domain convolution produces ordinary frequency-domain multiplication
  with no extra factor.
- The transform of a constant is an impulse, not another constant.
- The transform of a periodic signal is a harmonic impulse spectrum.
- Do not omit the impulse term in the transform of $u(t)$.
- Do not confuse the discrete CTFS coefficients $c_{k}$ with the continuous
  CTFT spectrum $X(\omega)$.
- Do not plot phase where the magnitude is zero.
- Check which definition of sinc is being used.

---

## 18. Review Checklist

After these lectures, you should be able to:

- define the frequency response $H(\omega)$ of an LTI system;
- use $d_{k}=H(k\omega_{0})c_{k}$ to find the response to a periodic input;
- recognize ideal lowpass, highpass, and bandpass filters;
- explain how the CTFT develops from CTFS as $T\to\infty$;
- state the forward and inverse CTFT equations;
- use basic CTFT pairs involving impulses, sinusoids, rectangular pulses, and
  one-sided exponentials;
- compute simple transforms directly from the analysis equation;
- apply the Dirichlet midpoint rule at discontinuities;
- use linearity, shifting, scaling, conjugation, and duality;
- convert convolution into multiplication and multiplication into
  convolution;
- use differentiation, integration, and Parseval's relation;
- apply conjugate symmetry to real signals;
- relate the CTFS coefficients of a periodic signal to its impulse spectrum;
- interpret frequency, magnitude, and phase spectra;
- determine whether a signal is bandlimited and identify its bandwidth;
- choose a known-pair-and-properties route before attempting direct
  integration.
