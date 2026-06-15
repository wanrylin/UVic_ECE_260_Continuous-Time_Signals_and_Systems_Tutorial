# ECE 260 Tutorial 4 Materials

Continuous-Time Fourier Series

This tutorial handout focuses on Fourier series computation, coefficient
interpretation, odd-harmonic symmetry, frequency-domain filtering, and MATLAB
visualization of Fourier series convergence. It is intended as tutorial
support. The textbook, lecture slides, and course website remain the
authoritative course materials.

---

## Quick Recap

### 1. CT Fourier Series Form

For a periodic signal $x$ with fundamental period $T$,

```math
\omega_{0}=\frac{2\pi}{T}.
```

The complex exponential Fourier series is

```math
x(t)=
\sum_{k=-\infty}^{\infty}c_{k}e^{jk\omega_{0}t}.
```

The coefficient sequence is found from

```math
c_{k}
=
\frac{1}{T}
\int_{t_{0}}^{t_{0}+T}
x(t)e^{-jk\omega_{0}t}\,dt,
```

where the integration interval can be any interval of length $T$.

### 2. Common Shortcuts

Cosine:

```math
\cos(\omega t)
=
\frac{1}{2}e^{j\omega t}
+
\frac{1}{2}e^{-j\omega t}.
```

Sine:

```math
\sin(\omega t)
=
\frac{1}{2j}e^{j\omega t}
-
\frac{1}{2j}e^{-j\omega t}.
```

Impulse:

```math
\int_{t_{0}}^{t_{0}+T}
\delta(t-a)e^{-jk\omega_{0}t}\,dt
=
e^{-jk\omega_{0}a},
```

as long as the impulse at $a$ is included in the chosen period.

### 3. LTI Systems in the Fourier Series Domain

If

```math
x(t)\ \mathrm{CTFS}\longleftrightarrow\ c_{k},
```

and the input passes through an LTI system with frequency response $H(\omega)$,
then

```math
y(t)\ \mathrm{CTFS}\longleftrightarrow\ d_{k},
\qquad
d_{k}=H(k\omega_{0})c_{k}.
```

This is the key reason Fourier series are useful: filtering becomes coefficient
multiplication.

---

## Selected Questions

## Q1. Exercise 5.1(b): Find Fourier Series

### Problem

Find the Fourier series representation in complex exponential form for

```math
x(t)=\cos(4t)\sin(t).
```

Explicitly identify the fundamental period and Fourier series coefficient
sequence.

### Route

Use a product-to-sum identity or Euler's formulas to rewrite the product as a
sum of sinusoids. Then identify the fundamental frequency.

### Knowledge Needed

```math
\sin(a)\cos(b)
=
\frac{1}{2}
\left[
\sin(a+b)+\sin(a-b)
\right].
```

### Solution

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

The frequencies are $3$ and $5$, so the fundamental frequency is

```math
\omega_{0}=1,
\qquad
T=2\pi.
```

Now use

```math
\sin(mt)=
\frac{1}{2j}
\left(e^{jmt}-e^{-jmt}\right).
```

Thus,

```math
\frac{1}{2}\sin(5t)
=
\frac{1}{4j}e^{j5t}
-
\frac{1}{4j}e^{-j5t},
```

and

```math
-\frac{1}{2}\sin(3t)
=
-\frac{1}{4j}e^{j3t}
+
\frac{1}{4j}e^{-j3t}.
```

### Final Result

```math
x(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jkt},
```

where

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

## Q2. Exercise 5.2(b): Fourier Series from Graph

### Problem

Find the Fourier series coefficient sequence for the periodic rectangular pulse
shown in Exercise 5.2(b).

From the figure, the signal has period $T$, height $1$, and is active on

```math
-\frac{A}{2}\le t<\frac{A}{2}
```

in each period.

### Route

Choose the centered interval $[-T/2,T/2)$ and integrate only over the active
part of the pulse.

### Knowledge Needed

Use

```math
c_{k}
=
\frac{1}{T}
\int_{-A/2}^{A/2}
e^{-jk\omega_{0}t}\,dt,
\qquad
\omega_{0}=\frac{2\pi}{T}.
```

The textbook sinc convention is

```math
\mathrm{sinc}(x)=\frac{\sin x}{x}.
```

### Solution

For $k=0$,

```math
c_{0}
=
\frac{1}{T}
\int_{-A/2}^{A/2}1\,dt
=
\frac{A}{T}.
```

For $k\ne0$,

```math
\begin{aligned}
c_{k}
&=
\frac{1}{T}
\int_{-A/2}^{A/2}
e^{-jk\omega_{0}t}\,dt\\
&=
\frac{1}{T}
\left[
\frac{e^{-jk\omega_{0}t}}{-jk\omega_{0}}
\right]_{-A/2}^{A/2}\\
&=
\frac{1}{T}
\frac{
e^{-jk\omega_{0}A/2}
-
e^{jk\omega_{0}A/2}
}{-jk\omega_{0}}\\
&=
\frac{2\sin(k\omega_{0}A/2)}{Tk\omega_{0}}.
\end{aligned}
```

Since $\omega_{0}=2\pi/T$,

```math
c_{k}
=
\frac{A}{T}
\frac{\sin(\pi kA/T)}{\pi kA/T}.
```

### Final Result

```math
c_{k}
=
\frac{A}{T}
\mathrm{sinc}\left(\frac{\pi kA}{T}\right),
\qquad
k\in\mathbb{Z}.
```

This formula also gives $c_{0}=A/T$ by the limiting value
$\mathrm{sinc}(0)=1$.

---

## Q3. Exercise 5.3(b): Fourier Series of an Impulse Train

### Problem

Find the Fourier series coefficient sequence $c$ for

```math
x(t)=\delta(t)+6\delta(t-1)+6\delta(t-2),
\qquad
T=3.
```

Express $c$ in terms of sine and cosine to whatever extent possible.

### Route

Use the Fourier series analysis equation and the sifting property.

### Knowledge Needed

For impulses in one period,

```math
c_{k}
=
\frac{1}{T}
\sum_{m}A_{m}e^{-jk\omega_{0}t_{m}}.
```

### Solution

Here

```math
\omega_{0}=\frac{2\pi}{3}.
```

Therefore,

```math
\begin{aligned}
c_{k}
&=
\frac{1}{3}
\left[
1
+
6e^{-jk\omega_{0}}
+
6e^{-j2k\omega_{0}}
\right]\\
&=
\frac{1}{3}
\left[
1
+
6e^{-j2\pi k/3}
+
6e^{-j4\pi k/3}
\right].
\end{aligned}
```

Since

```math
e^{-j4\pi k/3}=e^{j2\pi k/3}
```

for integer $k$,

```math
c_{k}
=
\frac{1}{3}
\left[
1+12\cos\left(\frac{2\pi k}{3}\right)
\right].
```

### Final Result

```math
c_{k}
=
\frac{1}{3}
\left[
1+12\cos\left(\frac{2\pi k}{3}\right)
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

---

## Q4. Exercise 5.7(a): Odd-Harmonic Proof

### Problem

A periodic function $x$ with period $T$ and Fourier series coefficient sequence
$c$ is said to be odd harmonic if

```math
c_{k}=0
\qquad
\mathrm{for\ all\ even}\ k.
```

Show that if $x$ is odd harmonic, then

```math
x(t)=-x\left(t-\frac{T}{2}\right)
\qquad
\mathrm{for\ all}\ t.
```

### Route

Start from the synthesis equation for $x(t-T/2)$ and use the fact that only odd
harmonics are nonzero.

### Solution

The synthesis equation is

```math
x(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t},
\qquad
\omega_{0}=\frac{2\pi}{T}.
```

Now shift by $T/2$:

```math
\begin{aligned}
x\left(t-\frac{T}{2}\right)
&=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}(t-T/2)}\\
&=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t}e^{-jk\omega_{0}T/2}\\
&=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t}e^{-jk\pi}\\
&=
\sum_{k=-\infty}^{\infty}
c_{k}(-1)^k e^{jk\omega_{0}t}.
\end{aligned}
```

Since $x$ is odd harmonic, $c_{k}=0$ for even $k$. Therefore, only odd $k$
contribute. For odd $k$,

```math
(-1)^k=-1.
```

Thus,

```math
x\left(t-\frac{T}{2}\right)
=
-
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t}
=
-x(t).
```

### Final Result

```math
\boxed{
x(t)=-x\left(t-\frac{T}{2}\right).
}
```

---

## Q5. Exercise 5.9: Frequency Spectrum

### Problem

Find the Fourier series coefficient sequence $c$ of the periodic rectangular
pulse train shown in Exercise 5.9. Plot the frequency spectrum of $x$, including
the first five harmonics.

From the figure, one period is

```math
T=2,
```

with

```math
x(t)=
\begin{cases}
1, & 0\le t<1,\\
0, & 1\le t<2.
\end{cases}
```

### Route

Use the analysis equation with $\omega_{0}=\pi$.

### Solution

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
\int_{0}^{1}
e^{-jk\pi t}\,dt\\
&=
\frac{1-e^{-jk\pi}}{j2\pi k}\\
&=
\frac{1-(-1)^k}{j2\pi k}.
\end{aligned}
```

Therefore, if $k$ is even and nonzero, $c_{k}=0$. If $k$ is odd,

```math
c_{k}=-\frac{j}{\pi k}.
```

### Final Result

```math
c_{k}=
\begin{cases}
\dfrac{1}{2}, & k=0,\\
-\dfrac{j}{\pi k}, & k\ \mathrm{odd},\\
0, & k\ne0\ \mathrm{even}.
\end{cases}
```

The nonzero coefficients among the first five harmonics are:

```math
\begin{array}{c|ccccccc}
k & -5 & -3 & -1 & 0 & 1 & 3 & 5\\
\hline
c_{k}
&
\dfrac{j}{5\pi}
&
\dfrac{j}{3\pi}
&
\dfrac{j}{\pi}
&
\dfrac{1}{2}
&
-\dfrac{j}{\pi}
&
-\dfrac{j}{3\pi}
&
-\dfrac{j}{5\pi}
\end{array}
```

Magnitude spectrum:

```math
|c_{0}|=\frac{1}{2},
\qquad
|c_{k}|=
\begin{cases}
\dfrac{1}{\pi|k|}, & k\ \mathrm{odd},\\
0, & k\ne0\ \mathrm{even}.
\end{cases}
```

Phase spectrum:

```math
\arg(c_{k})=
\begin{cases}
0, & k=0,\\
\dfrac{\pi}{2}, & k<0\ \mathrm{odd},\\
-\dfrac{\pi}{2}, & k>0\ \mathrm{odd},\\
\mathrm{undefined}, & c_{k}=0.
\end{cases}
```

---

## Q6. Exercise 5.10: Filtering

### Problem

Consider an LTI system with frequency response

```math
H(\omega)=
\begin{cases}
1, & |\omega|\ge5,\\
0, & \mathrm{otherwise}.
\end{cases}
```

Using frequency-domain methods, find the output $y$ if

```math
x(t)=1+2\cos(2t)+2\cos(4t)+\frac{1}{2}\cos(6t).
```

### Route

The system keeps frequency components with $|\omega|\ge5$ and removes the rest.

### Solution

The input contains components at

```math
\omega=0,\ \pm2,\ \pm4,\ \pm6.
```

The highpass filter removes $0,\pm2,\pm4$ and keeps only $\pm6$.

### Final Result

```math
\boxed{
y(t)=\frac{1}{2}\cos(6t).
}
```

---

## Q7. Exercise 5.201(a): Fourier Series Convergence in MATLAB

### Problem

For the periodic rectangular pulse in Exercise 5.2(b) with $T=1$ and
$A=1/2$, the Fourier series is

```math
\hat{x}(t)=
\sum_{k=-\infty}^{\infty}
c_{k}e^{jk\omega_{0}t},
```

where

```math
c_{k}
=
\frac{1}{2}
\mathrm{sinc}\left(\frac{\pi k}{2}\right),
\qquad
\omega_{0}=2\pi.
```

Let

```math
\hat{x}_{N}(t)
=
\sum_{k=-N}^{N}
c_{k}e^{jk\omega_{0}t}.
```

Plot $\hat{x}_{N}(t)$ for

```math
N=1,\ 5,\ 10,\ 50,\ 100.
```

### Route

Compute the finite sum numerically for each $N$. The textbook uses
$\mathrm{sinc}(x)=\sin(x)/x$, while MATLAB's built-in `sinc` is normalized, so
we compute the coefficients directly.

### MATLAB Demo Code

```matlab
% Exercise 5.201(a)
% Plot truncated CTFS approximations for N = 1, 5, 10, 50, 100.

Ns = [1 5 10 50 100];
omega0 = 2*pi;
t = linspace(-1, 1, 4000);

% Original periodic pulse for comparison:
% height 1 for |t - nearest integer| < 1/4, and 0 otherwise.
xtrue = double(abs(t - round(t)) < 0.25);

figure;

for m = 1:numel(Ns)
    N = Ns(m);
    k = -N:N;

    arg = pi*k/2;
    ck = 0.5 * ones(size(k));
    idx = k ~= 0;
    ck(idx) = 0.5 * sin(arg(idx)) ./ arg(idx);

    E = exp(1j * (k(:) * omega0 * t));
    xhat = real(ck(:).' * E);

    subplot(numel(Ns), 1, m);
    plot(t, xhat, 'LineWidth', 1.2);
    hold on;
    plot(t, xtrue, 'k--', 'LineWidth', 1.0);
    grid on;
    ylim([-0.3 1.3]);
    xlabel('t');
    ylabel('xhatN(t)');
    title(sprintf('Truncated Fourier Series, N = %d', N));
end
```

### Expected Observation

As $N$ increases, $\hat{x}_{N}$ better approximates the rectangular pulse.
Near each jump discontinuity, oscillations remain visible. This is the Gibbs
phenomenon.

