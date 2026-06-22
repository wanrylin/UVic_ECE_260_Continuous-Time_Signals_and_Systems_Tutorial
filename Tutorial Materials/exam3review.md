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

## 1. Exam Scope

Exam 3 is focused on:

- Chapter 5: Continuous-Time Fourier Series
- MATLAB basics from Appendix D

The main Chapter 5 ideas are:

- CTFS terminology;
- Fourier series analysis and synthesis equations;
- computing Fourier series coefficients;
- convergence properties;
- basic Fourier series properties and proof ideas;
- frequency spectra, magnitude spectra, and phase spectra;
- frequency response of LTI systems;
- lowpass, highpass, and bandpass filters.

The textbook contains more Fourier series properties than the lectures covered.
For Exam 3, focus on the properties explicitly covered in lecture and listed in
the study guide.

---

## 2. High-Yield Study Strategy

The fastest way to prepare is to sort problems by type:

1. Identify $T$, $\omega_{0}$, and harmonics.
2. Compute $c_{k}$ from a time-domain definition.
3. Read $c_{k}$ directly from a sum of complex exponentials.
4. Use convergence rules to find values at discontinuities.
5. Use CTFS properties such as linearity, time shift, and time reversal.
6. Interpret or plot magnitude and phase spectra.
7. Use $d_{k}=H(k\omega_{0})c_{k}$ for LTI systems.
8. Recognize what lowpass, highpass, and bandpass filters keep or remove.
9. Use MATLAB arrays and element-wise operations correctly.

Because there is no formula sheet unless the official exam page says otherwise,
memorize the core CTFS equations and the three Dirichlet conditions.

---

## 3. Core Formulas

### CTFS Pair

For a periodic signal $x$ with fundamental period $T$,

```math
\omega_{0}=\frac{2\pi}{T}.
```

The synthesis equation is

```math
x(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t}.
```

The analysis equation is

```math
c_{k}
=
\frac{1}{T}
\int_{T}
x(t)e^{-jk\omega_{0}t}\,dt.
```

The notation is

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k}.
```

### Useful Identities

```math
\cos(\omega t)
=
\frac{1}{2}e^{j\omega t}
+
\frac{1}{2}e^{-j\omega t}.
```

```math
\sin(\omega t)
=
\frac{1}{2j}e^{j\omega t}
-
\frac{1}{2j}e^{-j\omega t}.
```

Impulse sifting:

```math
\int_{T}\delta(t-a)f(t)\,dt=f(a),
```

as long as the impulse at $a$ is included in the chosen period.

### LTI System Output in CTFS Form

If

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k},
```

and an LTI system has frequency response $H(\omega)$, then

```math
y(t)\ \mathrm{CTFS}\longleftrightarrow\ d_{k},
\qquad
d_{k}=H(k\omega_{0})c_{k}.
```

---

## 4. Important Knowledge Points With Examples

### 4.1 Terminology: Period, Fundamental Frequency, Harmonics, and DC

A harmonic is a frequency component at $k\omega_{0}$, where $k$ is an integer.
The DC component is the zeroth harmonic, corresponding to $k=0$.

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

is harmonically related because all frequencies are integer multiples of the
same fundamental frequency $\omega_{0}$.

The coefficient $c_{0}$ is the average value over one period:

```math
c_{0}
=
\frac{1}{T}
\int_{T}x(t)\,dt.
```

#### Example

For

```math
x(t)=3+2\cos(4t)-\sin(6t),
```

the component frequencies are $0$, $4$, and $6$. The greatest common frequency
is

```math
\omega_{0}=2.
```

Therefore,

```math
T=\frac{2\pi}{\omega_{0}}=\pi.
```

The term $3$ is the DC component, so

```math
c_{0}=3.
```

The terms at $4$ and $6$ correspond to the second and third harmonics,
respectively, because

```math
4=2\omega_{0},
\qquad
6=3\omega_{0}.
```

---

### 4.2 What Signals Can Fourier Series Represent?

Fourier series represent periodic signals. If a signal is not periodic, CTFS is
not the right representation unless we explicitly form a periodic extension.

#### Example

The signal

```math
x(t)=e^{-t}u(t)
```

is not periodic, so it does not have a CTFS representation as a periodic
signal.

But

```math
x(t)=\cos(3t)
```

is periodic. Since its angular frequency is $3$,

```math
T=\frac{2\pi}{3},
\qquad
\omega_{0}=3.
```

Thus, it can be represented by a Fourier series.

---

### 4.3 Reading Coefficients From a Sum of Sinusoids

When the signal is already a sum of sinusoids, use Euler's formulas instead of
doing an integral.

#### Example

Find the CTFS coefficients for

```math
x(t)=\cos(4t)\sin(t).
```

Use the product-to-sum identity:

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
\frac{1}{2}\sin(5t)-\frac{1}{2}\sin(3t).
\end{aligned}
```

The frequencies are $3$ and $5$, so

```math
\omega_{0}=1,
\qquad
T=2\pi.
```

Using

```math
\sin(mt)
=
\frac{1}{2j}
\left(e^{jmt}-e^{-jmt}\right),
```

we get

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

---

### 4.4 Computing Coefficients by Direct Integration

Use the analysis equation when the signal is given by a piecewise formula or a
graph.

#### Example

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

For $k=0$,

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
\int_{0}^{1}e^{-jk\pi t}\,dt\\
&=
\frac{1-e^{-jk\pi}}{j2\pi k}\\
&=
\frac{1-(-1)^{k}}{j2\pi k}.
\end{aligned}
```

Therefore,

```math
c_{k}=
\begin{cases}
\dfrac{1}{2}, & k=0,\\
-\dfrac{j}{\pi k}, & k\ \mathrm{odd},\\
0, & k\ne0\ \mathrm{even}.
\end{cases}
```

---

### 4.5 Computing Coefficients for Periodic Impulse Signals

For impulses, the integral turns into a finite sum.

If one period contains impulses $A_{m}\delta(t-t_{m})$, then

```math
c_{k}
=
\frac{1}{T}
\sum_{m}A_{m}e^{-jk\omega_{0}t_{m}}.
```

#### Example

Let $T=3$ and, over one period,

```math
x(t)=\delta(t)+6\delta(t-1)+6\delta(t-2).
```

Then

```math
\omega_{0}=\frac{2\pi}{3}.
```

So

```math
\begin{aligned}
c_{k}
&=
\frac{1}{3}
\left[
1
+
6e^{-jk2\pi/3}
+
6e^{-jk4\pi/3}
\right]\\
&=
\frac{1}{3}
\left[
1
+
12\cos\left(\frac{2\pi k}{3}\right)
\right].
\end{aligned}
```

Equivalently,

```math
c_{k}=
\begin{cases}
\dfrac{13}{3}, & k=3m,\ m\in\mathbb{Z},\\
-\dfrac{5}{3}, & \mathrm{otherwise}.
\end{cases}
```

---

### 4.6 Convergence: Continuous, Finite Energy, and MSE

Fourier series are infinite sums, so convergence matters.

The truncated series is

```math
x_{N}(t)
=
\sum_{k=-N}^{N}
c_{k}e^{jk\omega_{0}t}.
```

Important convergence facts:

- If $x$ is continuous and the coefficients are absolutely summable, the
  Fourier series converges uniformly.
- If $x$ has finite energy over one period, the Fourier series converges in the
  MSE sense.
- MSE convergence does not necessarily guarantee equality at every individual
  point.

#### Example

For

```math
x(t)=\cos(t),
```

the Fourier series has only two nonzero coefficients:

```math
c_{1}=\frac{1}{2},
\qquad
c_{-1}=\frac{1}{2}.
```

Since this is a finite Fourier series, it converges uniformly to $x(t)$.

For a periodic rectangular pulse, the signal has finite energy over one
period, so the Fourier series converges in the MSE sense. However, at jump
discontinuities, the Fourier series does not converge to the original endpoint
value if the endpoint value is defined differently from the midpoint.

---

### 4.7 Dirichlet Conditions and Discontinuity Values

The three Dirichlet conditions are:

1. Over one period, $x$ is absolutely integrable.
2. Over one period, $x$ has a finite number of maxima and minima.
3. Over any finite interval, $x$ has a finite number of finite
   discontinuities.

The first condition is

```math
\int_{T}|x(t)|\,dt<\infty.
```

If $x$ satisfies the Dirichlet conditions, the Fourier series converges to
$x(t)$ at continuity points. At a jump discontinuity $t_{a}$, it converges to

```math
\frac{x(t_{a}^{-})+x(t_{a}^{+})}{2}.
```

#### Example

Suppose a periodic signal jumps from $1$ to $0$ at $t=1/4$. Then

```math
x(1/4^{-})=1,
\qquad
x(1/4^{+})=0.
```

The Fourier series converges at the jump to

```math
\frac{1+0}{2}
=
\frac{1}{2}.
```

This is also why truncated Fourier series plots show ringing near jump
discontinuities. That ringing is the Gibbs phenomenon.

---

### 4.8 Linearity Property and Proof Idea

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

#### Proof Example

Let

```math
z(t)=\alpha x(t)+\beta y(t).
```

Using the analysis equation,

```math
\begin{aligned}
z_{k}
&=
\frac{1}{T}
\int_{T}
\left[\alpha x(t)+\beta y(t)\right]
e^{-jk\omega_{0}t}\,dt\\
&=
\alpha
\frac{1}{T}
\int_{T}x(t)e^{-jk\omega_{0}t}\,dt
+
\beta
\frac{1}{T}
\int_{T}y(t)e^{-jk\omega_{0}t}\,dt\\
&=
\alpha a_{k}+\beta b_{k}.
\end{aligned}
```

So the property follows directly from linearity of the integral.

---

### 4.9 Time Shift Property and Proof Idea

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

A time shift changes the phase of the coefficients, but not their magnitudes.

#### Proof Example

Let

```math
z(t)=x(t-t_{0}).
```

Then

```math
\begin{aligned}
z_{k}
&=
\frac{1}{T}
\int_{T}x(t-t_{0})e^{-jk\omega_{0}t}\,dt.
\end{aligned}
```

Use $\lambda=t-t_{0}$, so $t=\lambda+t_{0}$ and $dt=d\lambda$. Since the
integral is over one full period, shifting the interval does not change the
coefficient integral:

```math
\begin{aligned}
z_{k}
&=
\frac{1}{T}
\int_{T}
x(\lambda)
e^{-jk\omega_{0}(\lambda+t_{0})}\,d\lambda\\
&=
e^{-jk\omega_{0}t_{0}}
\frac{1}{T}
\int_{T}
x(\lambda)e^{-jk\omega_{0}\lambda}\,d\lambda\\
&=
e^{-jk\omega_{0}t_{0}}c_{k}.
\end{aligned}
```

---

### 4.10 Time Reversal Property and Proof Idea

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

#### Proof Example

Let

```math
z(t)=x(-t).
```

Using the synthesis equation,

```math
\begin{aligned}
z(t)
&=
x(-t)\\
&=
\sum_{m=-\infty}^{\infty}
c_{m}e^{jm\omega_{0}(-t)}\\
&=
\sum_{m=-\infty}^{\infty}
c_{m}e^{-jm\omega_{0}t}.
\end{aligned}
```

Let $k=-m$. Then $m=-k$, and

```math
z(t)
=
\sum_{k=-\infty}^{\infty}
c_{-k}e^{jk\omega_{0}t}.
```

Therefore, the coefficient sequence for $x(-t)$ is $c_{-k}$.

---

### 4.11 Real, Even, and Odd Signal Relationships

The frequency spectrum is the coefficient sequence $c_{k}$.

Important relationships:

```math
x(t)\ \mathrm{real}
\quad\Longleftrightarrow\quad
c_{k}=c_{-k}^{*}.
```

For a real and even signal,

```math
c_{k}=c_{-k},
\qquad
c_{k}\ \mathrm{is\ real}.
```

For a real and odd signal,

```math
c_{k}=-c_{-k},
\qquad
c_{k}\ \mathrm{is\ purely\ imaginary}.
```

#### Example: Real Even

Let

```math
x(t)=2\cos(3t).
```

This signal is real and even. With $\omega_{0}=3$,

```math
x(t)=e^{j3t}+e^{-j3t}.
```

So

```math
c_{1}=1,
\qquad
c_{-1}=1.
```

The coefficients are real and even.

#### Example: Real Odd

Let

```math
x(t)=2\sin(3t).
```

With $\omega_{0}=3$,

```math
x(t)
=
\frac{1}{j}e^{j3t}
-
\frac{1}{j}e^{-j3t}.
```

Since $1/j=-j$,

```math
c_{1}=-j,
\qquad
c_{-1}=j.
```

The coefficients are purely imaginary and odd:

```math
c_{1}=-c_{-1}.
```

---

### 4.12 Frequency, Magnitude, and Phase Spectra

The frequency spectrum is the sequence $c_{k}$ plotted against frequency
$k\omega_{0}$.

The magnitude spectrum is $|c_{k}|$.

The phase spectrum is $\angle c_{k}$.

Do not assign a phase where $c_{k}=0$.

#### Example

For the periodic rectangular pulse from Section 4.4,

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

For this signal, $\omega_{0}=\pi$, so the lines occur at

```math
\omega=k\pi.
```

---

### 4.13 Frequency Response of an LTI System

For an LTI system with impulse response $h$,

```math
\mathcal{H}\{e^{j\omega t}\}(t)=H(\omega)e^{j\omega t},
```

where

```math
H(\omega)
=
\int_{-\infty}^{\infty}
h(t)e^{-j\omega t}\,dt.
```

The function $H(\omega)$ is the frequency response.

#### Example: Compute $H(\omega)$

Let

```math
h(t)=\delta(t)-\delta(t-1).
```

Then

```math
\begin{aligned}
H(\omega)
&=
\int_{-\infty}^{\infty}
\left[\delta(t)-\delta(t-1)\right]
e^{-j\omega t}\,dt\\
&=
1-e^{-j\omega}.
\end{aligned}
```

This system removes frequency components where $H(\omega)=0$. For example,

```math
H(0)=0,
\qquad
H(2\pi)=1-e^{-j2\pi}=0.
```

---

### 4.14 LTI Output From CTFS Coefficients

If

```math
x(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t},
```

then the output of an LTI system is

```math
y(t)=
\sum_{k=-\infty}^{\infty}
c_{k}H(k\omega_{0})e^{jk\omega_{0}t}.
```

So

```math
d_{k}=H(k\omega_{0})c_{k}.
```

#### Example

Let

```math
h(t)=\delta(t)-\delta(t-1),
```

so

```math
H(\omega)=1-e^{-j\omega}.
```

Let

```math
x(t)=1+2\cos(\pi t)+\cos(2\pi t).
```

Here

```math
\omega_{0}=\pi.
```

The input has components at $\omega=0$, $\pm\pi$, and $\pm2\pi$.

Evaluate the frequency response:

```math
H(0)=0,
\qquad
H(\pi)=2,
\qquad
H(-\pi)=2,
\qquad
H(2\pi)=0.
```

The DC term and the $\pm2\pi$ terms are removed. The $\pm\pi$ terms are
multiplied by $2$. Since $2\cos(\pi t)$ has coefficients $c_{1}=1$ and
$c_{-1}=1$, the output coefficients are $d_{1}=2$ and $d_{-1}=2$.

Therefore,

```math
y(t)
=
2e^{j\pi t}+2e^{-j\pi t}
=
4\cos(\pi t).
```

---

### 4.15 Lowpass, Highpass, and Bandpass Filters

An ideal lowpass filter keeps frequencies with small magnitude:

```math
H(\omega)=
\begin{cases}
1, & |\omega|\le\omega_{c},\\
0, & \mathrm{otherwise}.
\end{cases}
```

An ideal highpass filter keeps frequencies with large magnitude:

```math
H(\omega)=
\begin{cases}
1, & |\omega|\ge\omega_{c},\\
0, & \mathrm{otherwise}.
\end{cases}
```

An ideal bandpass filter keeps frequencies in a band:

```math
H(\omega)=
\begin{cases}
1, & \omega_{c1}\le|\omega|\le\omega_{c2},\\
0, & \mathrm{otherwise}.
\end{cases}
```

#### Example

Let

```math
x(t)
=
1+2\cos(2t)+2\cos(4t)+\frac{1}{2}\cos(6t).
```

The frequency components are

```math
0,\quad \pm2,\quad \pm4,\quad \pm6.
```

If the system is an ideal lowpass filter with cutoff $\omega_{c}=3$, it keeps
$0$ and $\pm2$:

```math
y_{\mathrm{LP}}(t)=1+2\cos(2t).
```

If the system is an ideal highpass filter with cutoff $\omega_{c}=5$, it keeps
$\pm6$:

```math
y_{\mathrm{HP}}(t)=\frac{1}{2}\cos(6t).
```

If the system is an ideal bandpass filter with $3\le|\omega|\le5$, it keeps
$\pm4$:

```math
y_{\mathrm{BP}}(t)=2\cos(4t).
```

When sketching filter shapes, draw lowpass as one passband around zero,
highpass as two outer passbands, and bandpass as two passbands away from zero.

---

## 5. MATLAB Review With Examples

### 5.1 Arrays and Subscripts

MATLAB indexing starts at $1$, not $0$.

#### Example

```matlab
k = -3:3;
c = zeros(size(k));

% Put c0 = 1 at the location where k equals 0.
c(k == 0) = 1;

% Put c1 = 2 and cminus1 = 2.
c(k == 1) = 2;
c(k == -1) = 2;
```

The expression `k == 0` creates a logical array. MATLAB uses it to select the
entry corresponding to $k=0$.

Useful size functions:

```matlab
numEntries = length(k);
shape = size(c);
```

---

### 5.2 Element-Wise Operations

Use `.*`, `./`, and `.^` when operating entry-by-entry on arrays.

#### Example

Suppose

```math
c_{k}=
\frac{1}{2}
\frac{\sin(\pi k/2)}{\pi k/2}
```

for $k\ne0$, with $c_{0}=1/2$.

In MATLAB:

```matlab
k = -10:10;
c = 0.5 * ones(size(k));

idx = k ~= 0;
arg = pi * k / 2;
c(idx) = 0.5 * sin(arg(idx)) ./ arg(idx);
```

The division must be `./` because `sin(arg(idx))` and `arg(idx)` are arrays.

---

### 5.3 Relational and Logical Operators

Use relational operators to build conditions:

- `==`, `~=`, `<`, `<=`, `>`, `>=`

Use logical operators to combine them:

- `&`, `|`, `~`

#### Example

Create an ideal bandpass response that keeps $3\le|\omega|\le5$.

```matlab
w = -8:0.01:8;
pass = (abs(w) >= 3) & (abs(w) <= 5);
H = double(pass);

plot(w, H);
grid on;
xlabel('omega');
ylabel('H(omega)');
```

The parentheses matter. Write each comparison separately before combining with
`&`.

---

### 5.4 Loops and Conditionals

Loops and `if` statements are useful, but many array problems can be written
more cleanly using logical indexing.

#### Example: Loop Version

```matlab
k = -5:5;
c = zeros(size(k));

for n = 1:length(k)
    if k(n) == 0
        c(n) = 0.5;
    elseif mod(k(n), 2) ~= 0
        c(n) = -1j / (pi * k(n));
    else
        c(n) = 0;
    end
end
```

#### Example: Vectorized Version

```matlab
k = -5:5;
c = zeros(size(k));

c(k == 0) = 0.5;
idx = (k ~= 0) & (mod(k, 2) ~= 0);
c(idx) = -1j ./ (pi * k(idx));
```

Both versions compute the same coefficient sequence, but the vectorized version
is shorter and usually easier to check.

#### Example: While Loop

Find the smallest $N$ such that $1/N<0.01$.

```matlab
N = 1;
while 1/N >= 0.01
    N = N + 1;
end
```

After the loop, `N` is the first integer that satisfies the condition.

---

### 5.5 Basic Functions for Spectra

For complex coefficients:

- `real(c)` gives the real part.
- `imag(c)` gives the imaginary part.
- `abs(c)` gives magnitude.
- `angle(c)` gives phase.
- `plot` or `stem` can be used to display values.

#### Example

```matlab
k = -5:5;
c = zeros(size(k));

c(k == 0) = 0.5;
idx = (k ~= 0) & (mod(k, 2) ~= 0);
c(idx) = -1j ./ (pi * k(idx));

figure;
subplot(2, 1, 1);
stem(k, abs(c), 'filled');
grid on;
xlabel('k');
ylabel('|ck|');

subplot(2, 1, 2);
stem(k, angle(c), 'filled');
grid on;
xlabel('k');
ylabel('angle(ck)');
```

Remember that phase is not meaningful when the coefficient is zero.

---

### 5.6 User-Defined Functions

A user-defined function lets you package repeated calculations.

#### Example

This function can be saved in `mysinc.m`, or placed at the end of a MATLAB
script that calls it.

```matlab
function y = mysinc(x)
    y = ones(size(x));
    idx = x ~= 0;
    y(idx) = sin(x(idx)) ./ x(idx);
end
```

Then a coefficient sequence can be computed as

```matlab
k = -10:10;
c = 0.5 * mysinc(pi * k / 2);
```

This uses the course convention

```math
\mathrm{sinc}(x)=\frac{\sin x}{x}.
```

MATLAB's built-in `sinc` uses a normalized convention, so check which convention
the problem expects.

---

### 5.7 Plotting a Truncated Fourier Series

To plot

```math
x_{N}(t)=
\sum_{k=-N}^{N}
c_{k}e^{jk\omega_{0}t},
```

use a vector of $t$ values and a vector of $k$ values.

#### Example

```matlab
N = 20;
k = -N:N;
omega0 = pi;
t = linspace(-2, 2, 2000);

c = zeros(size(k));
c(k == 0) = 0.5;
idx = (k ~= 0) & (mod(k, 2) ~= 0);
c(idx) = -1j ./ (pi * k(idx));

E = exp(1j * (k(:) * omega0 * t));
xN = real(c(:).' * E);

plot(t, xN, 'LineWidth', 1.2);
grid on;
xlabel('t');
ylabel('xN(t)');
```

The expression `k(:) * omega0 * t` forms a matrix whose rows correspond to
different harmonics and whose columns correspond to different time samples.

---

## 6. Common Pitfalls

- Forgetting the factor $1/T$ in the analysis equation.
- Using the wrong fundamental period.
- Confusing the index $k$ with the actual frequency $k\omega_{0}$.
- Treating a nonperiodic signal as if it had a CTFS.
- Forgetting to handle $k=0$ separately when an expression has $k$ in the
  denominator.
- Assigning a phase value when $c_{k}=0$.
- Forgetting conjugate symmetry for real signals.
- Saying a Fourier series must equal the original signal at a jump
  discontinuity. The limiting value is the midpoint.
- In MATLAB, using `*`, `/`, or `^` when the intended operation is element-wise.
- In MATLAB, forgetting parentheses in logical conditions such as
  `(abs(w) >= 3) & (abs(w) <= 5)`.

---

## 7. Final Review Checklist

Before the exam, make sure you can:

- define harmonics, DC component, fundamental frequency, and fundamental
  period;
- state the CTFS synthesis and analysis equations;
- explain why CTFS applies to periodic signals;
- compute $c_{k}$ from a graph, piecewise formula, sinusoidal expression, or
  impulse train;
- state the main convergence facts for continuous signals, finite-energy
  signals, and Dirichlet signals;
- list the three Dirichlet conditions;
- compute the Fourier series value at a jump discontinuity;
- prove or outline proofs for linearity, time shift, and time reversal;
- use real/even/odd symmetry to check coefficient sequences;
- plot or describe frequency, magnitude, and phase spectra;
- compute a frequency response from an impulse response;
- use $d_{k}=H(k\omega_{0})c_{k}$ to find an LTI system output;
- identify what lowpass, highpass, and bandpass filters keep or remove;
- write MATLAB code using arrays, indexing, element-wise operations, logical
  indexing, loops, functions, and plotting.
