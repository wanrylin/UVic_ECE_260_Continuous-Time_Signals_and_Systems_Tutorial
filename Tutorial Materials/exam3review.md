# ECE 260 Exam 3 Review Guide

Continuous-Time Fourier Series  
Exam 3: Chapter 5 and MATLAB  
Last updated: 2026-06-22

This guide is a student-friendly review document for Exam 3 and is intended to
support tutorial review. It is based on the posted Exam 3 study guide, lecture
slides, lecture summaries, tutorial materials, and assignment topics.

This is not an official course document. For exact exam logistics, permitted
materials, grading rules, and due-date/exam-date information, use the official
course website, Brightspace announcements, lecture slides, and textbook.

---

## 0. Exam Map

Exam 3 is mainly about continuous-time Fourier series (CTFS), plus MATLAB
basics from Appendix D.

The main CTFS workflow is

```math
x(t)
\quad\longrightarrow\quad
c_{k}
\quad\longrightarrow\quad
|c_{k}|,\ \angle c_{k},\ d_{k}=H(k\omega_{0})c_{k}.
```

In words:

1. Start with a periodic signal.
2. Find or read off its Fourier series coefficients.
3. Use those coefficients to discuss spectra, convergence, symmetry, or LTI
   system output.

Most Exam 3 questions fall into one of these routes:

1. Identify $T$, $\omega_{0}$, harmonics, and DC component.
2. Compute $c_{k}$ from a time-domain formula or graph.
3. Read $c_{k}$ directly from a sum of sinusoids.
4. Use convergence rules at discontinuities.
5. Use CTFS properties such as linearity, time shift, and time reversal.
6. Interpret magnitude and phase spectra.
7. Use $d_{k}=H(k\omega_{0})c_{k}$ for LTI systems.
8. Recognize lowpass, highpass, and bandpass filters.
9. Avoid MATLAB array and element-wise operation mistakes.

---

## 1. Core CTFS Formulas

The continuous-time Fourier series is used for periodic signals. If a signal is
not periodic, CTFS is not the right representation unless the problem explicitly
defines a periodic extension.

For a periodic signal $x$ with fundamental period $T$,

```math
\omega_{0}=\frac{2\pi}{T}.
```

The complex exponential Fourier series is

```math
x(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t}.
```

This is the synthesis equation. It rebuilds the signal from its coefficients.

The coefficients are found from

```math
c_{k}
=
\frac{1}{T}
\int_{T}
x(t)e^{-jk\omega_{0}t}\,dt.
```

This is the analysis equation. The notation $\int_{T}$ means integration over
any interval of length $T$. Choose the interval that makes the work easiest.

The CTFS pair is written as

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k}.
```

The coefficient $c_{0}$ is the DC component, or average value:

```math
c_{0}
=
\frac{1}{T}
\int_{T}x(t)\,dt.
```

The index $k$ is not itself the physical angular frequency. The actual angular
frequency is

```math
\omega=k\omega_{0}.
```

A complex sinusoid has the form

```math
e^{j\omega t}.
```

The set

```math
e^{jk\omega_{0}t},
\qquad
k\in\mathbb{Z},
```

is harmonically related because every frequency is an integer multiple of the
same fundamental frequency $\omega_{0}$.

---

## 2. Route 1: Read Coefficients From Sinusoids

If the signal is already written using sinusoids, avoid integration. Rewrite it
using Euler's formulas and read off the coefficients.

Useful identities:

```math
\cos(\omega t)
=
\frac{1}{2}e^{j\omega t}
+
\frac{1}{2}e^{-j\omega t},
```

```math
\sin(\omega t)
=
\frac{1}{2j}e^{j\omega t}
-
\frac{1}{2j}e^{-j\omega t}.
```

### Example

Find the CTFS coefficients for

```math
x(t)=\cos(4t)\sin(t).
```

Use

```math
\sin(a)\cos(b)
=
\frac{1}{2}
\left[
\sin(a+b)+\sin(a-b)
\right].
```

Then

```math
\begin{aligned}
x(t)
&=
\cos(4t)\sin(t)\\
&=
\frac{1}{2}\left[\sin(5t)+\sin(-3t)\right]\\
&=
\frac{1}{2}\sin(5t)-\frac{1}{2}\sin(3t).
\end{aligned}
```

The angular frequencies are $3$ and $5$, so the greatest common frequency is

```math
\omega_{0}=1,
\qquad
T=2\pi.
```

Since $\omega_{0}=1$, the CTFS synthesis form is

```math
x(t)=
\sum_{k=-\infty}^{\infty}c_{k}e^{jkt}.
```

So the coefficient multiplying $e^{jkt}$ is $c_{k}$.

Rewrite the signal in terms of the basis functions $e^{jkt}$:

```math
\begin{aligned}
x(t)
&=
\frac{1}{2}\sin(5t)-\frac{1}{2}\sin(3t)\\
&=
-\frac{j}{4}e^{j5t}
+
\frac{j}{4}e^{-j5t}
+
\frac{j}{4}e^{j3t}
-
\frac{j}{4}e^{-j3t}.
\end{aligned}
```

Now match each exponential term to the CTFS pair:

```math
\begin{array}{c|c|c}
\mathrm{term} & k & c_{k}\\
\hline
\dfrac{j}{4}e^{j3t} & 3 & \dfrac{j}{4}\\
-\dfrac{j}{4}e^{-j3t} & -3 & -\dfrac{j}{4}\\
-\dfrac{j}{4}e^{j5t} & 5 & -\dfrac{j}{4}\\
\dfrac{j}{4}e^{-j5t} & -5 & \dfrac{j}{4}
\end{array}
```

Therefore,

```math
c_{k}=
\begin{cases}
\dfrac{j}{4}, & k=3,\\
-\dfrac{j}{4}, & k=-3,\\
-\dfrac{j}{4}, & k=5,\\
\dfrac{j}{4}, & k=-5,\\
0, & \mathrm{otherwise}.
\end{cases}
```

Route summary: simplify the sinusoidal expression, identify $\omega_{0}$, then
match each exponential term to its coefficient.

---

## 3. Route 2: Compute Coefficients by Direct Integration

If the signal is given by a graph or a piecewise definition, use the analysis
equation.

### Example

Let $x$ be periodic with period $T=2$, and over one period

```math
x(t)=
\begin{cases}
1, & 0\le t<1,\\
0, & 1\le t<2.
\end{cases}
```

Then

```math
\omega_{0}=\frac{2\pi}{2}=\pi.
```

For $k=0$, use the average value:

```math
c_{0}
=
\frac{1}{2}
\int_{0}^{1}1\,dt
=
\frac{1}{2}.
```

For $k\ne0$,

```math
\begin{aligned}
c_{k}
&=
\frac{1}{2}
\int_{0}^{1}
e^{-jk\pi t}\,dt\\
&=
\frac{1}{2}
\left[
\frac{e^{-jk\pi t}}{-jk\pi}
\right]_{0}^{1}\\
&=
\frac{1-e^{-jk\pi}}{j2\pi k}\\
&=
\frac{1-(-1)^{k}}{j2\pi k}.
\end{aligned}
```

So even nonzero $k$ gives zero. Odd $k$ gives

```math
c_{k}=-\frac{j}{\pi k}.
```

The final result is

```math
c_{k}=
\begin{cases}
\dfrac{1}{2}, & k=0,\\
-\dfrac{j}{\pi k}, & k\ \mathrm{odd},\\
0, & k\ne0\ \mathrm{even}.
\end{cases}
```

Key exam habit: handle $k=0$ separately whenever the formula for $k\ne0$ has
$k$ in the denominator.

---

## 4. Route 3: Compute Coefficients for Impulse Signals

For impulse signals, the analysis integral becomes a finite sum. If one period
contains impulses $A_{m}\delta(t-t_{m})$, then

```math
c_{k}
=
\frac{1}{T}
\sum_{m}A_{m}e^{-jk\omega_{0}t_{m}}.
```

### Example

Let $T=3$ and, over one period,

```math
x(t)=\delta(t)+6\delta(t-1)+6\delta(t-2).
```

Then $\omega_{0}=2\pi/3$, and

```math
c_{k}
=
\frac{1}{3}
\left[
1
+
6e^{-jk2\pi/3}
+
6e^{-jk4\pi/3}
\right].
```

Since $e^{-jk4\pi/3}=e^{jk2\pi/3}$ for integer $k$, this can also be written as

```math
c_{k}
=
\frac{1}{3}
\left[
1
+
12\cos\left(\frac{2\pi k}{3}\right)
\right].
```

Equivalently,

```math
c_{k}=
\begin{cases}
\dfrac{13}{3}, & k=3m,\ m\in\mathbb{Z},\\
-\dfrac{5}{3}, & \mathrm{otherwise}.
\end{cases}
```

Main point: impulses sample the exponential factor. Do not turn this into a
long integration problem.

---

## 5. Convergence and Discontinuities

The truncated Fourier series is

```math
x_{N}(t)
=
\sum_{k=-N}^{N}
c_{k}e^{jk\omega_{0}t}.
```

The exam-relevant convergence facts are:

- If $x$ is continuous and the coefficients are absolutely summable, the
  Fourier series converges uniformly.
- If $x$ has finite energy over one period, the Fourier series converges in the
  mean-squared-error sense.
- If $x$ satisfies the Dirichlet conditions, then the Fourier series converges
  to $x(t)$ at continuity points and to the midpoint at jump discontinuities.

The three Dirichlet conditions are:

1. Over one period, $x$ is absolutely integrable.
2. Over one period, $x$ has a finite number of maxima and minima.
3. Over any finite interval, $x$ has a finite number of finite
   discontinuities.

At a jump discontinuity $t_{a}$,

```math
\widetilde{x}(t_{a})
=
\frac{x(t_{a}^{-})+x(t_{a}^{+})}{2}.
```

### Example

If a periodic signal jumps from $1$ to $0$ at $t=1/4$, then the Fourier series
converges at that point to

```math
\frac{1+0}{2}
=
\frac{1}{2}.
```

At a jump, the Fourier series converges to the midpoint, not necessarily to the
value drawn at the endpoint.

Gibbs phenomenon is the ringing near jump discontinuities in truncated Fourier
series. As $N$ increases, the ringing becomes compressed closer to the jump, but
the peak overshoot does not disappear for finite $N$.

Pointwise convergence means equality at each individual time. MSE convergence
means the energy of the error goes to zero. Pointwise convergence is stronger
than MSE convergence.

---

## 6. Basic CTFS Properties and Proof Ideas

The study guide specifically mentions being familiar with proofs of linearity,
time shift, and time reversal. For this exam, the important thing is to know the
property and the proof route.

### Linearity

If

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ a_{k},
\qquad
y(t)\ \mathrm{CTFS}\longleftrightarrow\ b_{k},
```

then

```math
\alpha x(t)+\beta y(t)
\ \mathrm{CTFS}\longleftrightarrow\
\alpha a_{k}+\beta b_{k}.
```

Proof idea: substitute $\alpha x(t)+\beta y(t)$ into the analysis equation and
use linearity of the integral.

### Time Shift

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

Proof idea: use the substitution $\lambda=t-t_{0}$. The exponential produces
the factor $e^{-jk\omega_{0}t_{0}}$. A time shift changes phase, but not
magnitude.

### Time Reversal

If

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k},
```

then

```math
x(-t)
\ \mathrm{CTFS}\longleftrightarrow\
c_{-k}.
```

Proof idea: start from the synthesis equation, substitute $-t$, and relabel the
summation index:

```math
\begin{aligned}
x(-t)
&=
\sum_{m=-\infty}^{\infty}
c_{m}e^{jm\omega_{0}(-t)}\\
&=
\sum_{m=-\infty}^{\infty}
c_{m}e^{-jm\omega_{0}t}.
\end{aligned}
```

Let $k=-m$. Then

```math
x(-t)
=
\sum_{k=-\infty}^{\infty}
c_{-k}e^{jk\omega_{0}t}.
```

So the coefficient sequence is $c_{-k}$.

---

## 7. Symmetry and Spectra

The frequency spectrum is the coefficient sequence $c_{k}$, usually plotted
against the actual frequency $k\omega_{0}$.

The magnitude spectrum is $|c_{k}|$.

The phase spectrum is $\angle c_{k}$.

For real signals,

```math
c_{k}=c_{-k}^{*}.
```

This means the magnitude spectrum is even and the phase spectrum is odd.

For real and even signals,

```math
c_{k}=c_{-k},
\qquad
c_{k}\ \mathrm{is\ real}.
```

For real and odd signals,

```math
c_{k}=-c_{-k},
\qquad
c_{k}\ \mathrm{is\ purely\ imaginary}.
```

### Examples

The signal $2\cos(3t)$ is real and even. With $\omega_{0}=3$,

```math
2\cos(3t)=e^{j3t}+e^{-j3t},
```

so

```math
c_{1}=1,
\qquad
c_{-1}=1.
```

The coefficients are real and even.

The signal $2\sin(3t)$ is real and odd. With $\omega_{0}=3$,

```math
2\sin(3t)
=
-je^{j3t}
+
je^{-j3t},
```

so

```math
c_{1}=-j,
\qquad
c_{-1}=j.
```

The coefficients are purely imaginary and odd.

For the rectangular pulse example from Section 3,

```math
c_{k}=
\begin{cases}
\dfrac{1}{2}, & k=0,\\
-\dfrac{j}{\pi k}, & k\ \mathrm{odd},\\
0, & k\ne0\ \mathrm{even}.
\end{cases}
```

The magnitude spectrum is

```math
|c_{k}|=
\begin{cases}
\dfrac{1}{2}, & k=0,\\
\dfrac{1}{\pi |k|}, & k\ \mathrm{odd},\\
0, & k\ne0\ \mathrm{even}.
\end{cases}
```

The phase spectrum is

```math
\angle c_{k}=
\begin{cases}
0, & k=0,\\
\dfrac{\pi}{2}, & k<0\ \mathrm{odd},\\
-\dfrac{\pi}{2}, & k>0\ \mathrm{odd},\\
\mathrm{undefined}, & c_{k}=0.
\end{cases}
```

Do not assign a phase where $c_{k}=0$.

---

## 8. LTI Systems and Filters

For an LTI system,

```math
\mathcal{H}\{e^{j\omega t}\}(t)=H(\omega)e^{j\omega t}.
```

The frequency response is

```math
H(\omega)
=
\int_{-\infty}^{\infty}
h(t)e^{-j\omega t}\,dt.
```

If

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k},
```

then

```math
y(t)\ \mathrm{CTFS}\longleftrightarrow\ d_{k},
\qquad
d_{k}=H(k\omega_{0})c_{k}.
```

This is the payoff of Fourier series for LTI systems: each harmonic is
multiplied by the frequency response at that harmonic frequency.

### Example

Let

```math
x(t)=1+2\cos(2t)+2\cos(4t)+\frac{1}{2}\cos(6t).
```

The frequencies present are

```math
0,\quad \pm2,\quad \pm4,\quad \pm6.
```

For an ideal highpass filter

```math
H(\omega)=
\begin{cases}
1, & |\omega|\ge5,\\
0, & \mathrm{otherwise},
\end{cases}
```

only the $\pm6$ components pass. Therefore,

```math
y(t)=\frac{1}{2}\cos(6t).
```

The three basic filter types are:

Lowpass:

```math
H(\omega)=
\begin{cases}
1, & |\omega|\le\omega_{c},\\
0, & \mathrm{otherwise}.
\end{cases}
```

Highpass:

```math
H(\omega)=
\begin{cases}
1, & |\omega|\ge\omega_{c},\\
0, & \mathrm{otherwise}.
\end{cases}
```

Bandpass:

```math
H(\omega)=
\begin{cases}
1, & \omega_{c1}\le|\omega|\le\omega_{c2},\\
0, & \mathrm{otherwise}.
\end{cases}
```

The exam route is simple: list the input frequencies, check which ones pass,
then write the remaining time-domain terms.

If $h(t)=\delta(t)-\delta(t-1)$, then

```math
H(\omega)=1-e^{-j\omega}.
```

This follows directly from impulse sifting in the frequency-response integral.

---

## 9. MATLAB Review

The MATLAB part uses the same basic language tools as before, but now the
context may be Fourier coefficients or spectra.

The biggest MATLAB habit is element-wise operations. If `k` is an array, then
formulas involving $k$ usually need `.*`, `./`, and `.^`.

### Example: Coefficient Vector

```matlab
k = -10:10;
c = zeros(size(k));

c(k == 0) = 0.5;
idx = (k ~= 0) & (mod(k, 2) ~= 0);
c(idx) = -1j ./ (pi * k(idx));
```

This builds the rectangular-pulse coefficient sequence from Section 3. The
condition `k == 0` selects the DC term. The condition involving `mod(k, 2)`
selects odd nonzero harmonics.

For spectra:

```matlab
mag = abs(c);
ph = angle(c);
```

For real and imaginary parts:

```matlab
cr = real(c);
ci = imag(c);
```

For a line spectrum:

```matlab
stem(k, abs(c), 'filled');
grid on;
xlabel('k');
ylabel('|ck|');
```

Common MATLAB mistakes:

- using `/` instead of `./`;
- using `^` instead of `.^`;
- forgetting MATLAB indexing starts at 1;
- forgetting parentheses in logical conditions such as
  `(abs(w) >= 3) & (abs(w) <= 5)`;
- assigning phase values at zero coefficients without thinking.

User-defined functions, `for`, `while`, and `if` are fair game. For Fourier
coefficient arrays, logical indexing is often shorter and clearer than a loop.

---

## 10. Final Checklist

Before the exam, make sure you can:

- state the CTFS synthesis and analysis equations;
- use $\omega_{0}=2\pi/T$;
- find $c_{0}$ as the average value;
- compute coefficients by reading from sinusoids, integrating, or using
  impulse sifting;
- handle $k=0$ separately when needed;
- state the Dirichlet conditions and use the midpoint rule at jumps;
- use linearity, time shift, and time reversal;
- use real/even/odd symmetry to check coefficient sequences;
- find magnitude and phase spectra;
- use $d_{k}=H(k\omega_{0})c_{k}$ for LTI systems;
- recognize lowpass, highpass, and bandpass filters;
- use MATLAB element-wise operations and logical indexing carefully.
