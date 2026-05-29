# ECE 260 Tutorial 3 Materials, Version 1

Continuous-Time LTI Systems and Convolution

This pre-tutorial version is for guided practice. Some final simplifications
are intentionally left for tutorial discussion. The textbook, lecture slides,
and course website remain the authoritative course materials.

---

## Quick Recap

### 1. Convolution for CT LTI Systems

For a continuous-time LTI system with input $x$, impulse response $h$, and
output $y$,

```math
y=x\ast h.
```

In evaluated form,

```math
y(t)=
\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
```

### 2. Graphical Convolution Route

To compute $x\ast h$ graphically:

1. Keep $x(\tau)$ fixed.
2. Flip and shift $h$ to get $h(t-\tau)$.
3. Find the overlap interval in $\tau$.
4. Integrate the product over the overlap.
5. Break the answer into cases whenever the overlap changes.

For finite-duration signals, the support of the convolution is found by adding
the support intervals:

```math
\mathrm{support}(x\ast h)
\subset
\mathrm{support}(x)+\mathrm{support}(h).
```

### 3. LTI Superposition and Time Shifts

If an LTI system maps $x_{1}$ to $y_{1}$, then shifted and scaled copies behave
the same way:

```math
x_{1}(t-t_{0})
\longrightarrow
y_{1}(t-t_{0}),
```

and

```math
a_{1}x_{1}(t-t_{1})+a_{2}x_{1}(t-t_{2})
\longrightarrow
a_{1}y_{1}(t-t_{1})+a_{2}y_{1}(t-t_{2}).
```

---

## Selected Questions

## Q1. Exercise 4.1(c): Graphical Convolution

### Problem

Using the graphical method, compute $x\ast h$ for the pair of signals in
Exercise 4.1(c).

From the figure,

```math
x(t)=
\begin{cases}
2, & 0\le t<1,\\
0, & \mathrm{otherwise},
\end{cases}
```

and

```math
h(t)=
\begin{cases}
-1, & -1\le t<0,\\
1, & 0\le t<1,\\
0, & \mathrm{otherwise}.
\end{cases}
```

### Route

Start from

```math
y(t)=(x\ast h)(t)
=
\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
```

The support of $x$ is $[0,1]$, and the support of $h$ is $[-1,1]$, so the
convolution can only be nonzero on

```math
[-1,2].
```

The overlap changes at

```math
t=-1,\ 0,\ 1,\ 2.
```

### Knowledge Needed

For $h(t-\tau)$:

- $h(t-\tau)=1$ when $0\le t-\tau<1$.
- $h(t-\tau)=-1$ when $-1\le t-\tau<0$.

Equivalently, in terms of $\tau$:

```math
h(t-\tau)=1
\quad \mathrm{when} \quad
t-1<\tau\le t,
```

and

```math
h(t-\tau)=-1
\quad \mathrm{when} \quad
t<\tau\le t+1.
```

### Derivation Setup

Since $x(\tau)=2$ on $0\le \tau<1$, the integral only needs the overlap with
$[0,1]$.

For $-1\le t<0$,

```math
y(t)=
2\int_{0}^{t+1}(-1)\,d\tau.
```

For $0\le t<1$,

```math
y(t)=
2\int_{0}^{t}1\,d\tau
+
2\int_{t}^{1}(-1)\,d\tau.
```

For $1\le t<2$,

```math
y(t)=
2\int_{t-1}^{1}1\,d\tau.
```

Outside these intervals, $y(t)=0$.

### In-Class Finish

Evaluate the three integrals above and sketch the resulting piecewise-linear
signal.

---

## Q2. Exercise 4.3(a): Graphical Convolution

### Problem

Using the graphical method, compute $x\ast h$, where

```math
x(t)=e^{t}u(-t)
```

and

```math
h(t)=
\begin{cases}
t-1, & 1\le t<2,\\
0, & \mathrm{otherwise}.
\end{cases}
```

### Route

Use

```math
y(t)=
\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
```

The signal $x(\tau)$ is active for $\tau\le 0$. The shifted signal
$h(t-\tau)$ is active when

```math
1\le t-\tau<2.
```

Solving for $\tau$ gives

```math
t-2<\tau\le t-1.
```

Therefore, the integration interval is the overlap of

```math
(-\infty,0]
```

and

```math
(t-2,t-1].
```

The overlap changes at

```math
t=1,\ 2.
```

### Knowledge Needed

Inside the active interval of $h(t-\tau)$,

```math
h(t-\tau)=(t-\tau)-1=t-1-\tau.
```

So the integrand is

```math
x(\tau)h(t-\tau)=e^{\tau}(t-1-\tau).
```

### Derivation Setup

For $t<1$, the entire interval $(t-2,t-1]$ lies to the left of $0$, so

```math
y(t)=
\int_{t-2}^{t-1}
e^{\tau}(t-1-\tau)\,d\tau.
```

For $1\le t<2$, only the part from $t-2$ to $0$ overlaps $x(\tau)$, so

```math
y(t)=
\int_{t-2}^{0}
e^{\tau}(t-1-\tau)\,d\tau.
```

For $t\ge 2$, there is no nonzero overlap, so $y(t)=0$.


---

## Q3. Exercise 4.5: Manipulation of Convolution Expressions

### Problem

Let $x$, $y$, $h$, and $v$ be functions such that

```math
y=x\ast h
```

and

```math
v(t)=
\int_{-\infty}^{\infty}
x(-\tau-b)h(\tau+a)\,d\tau,
```

where $a$ and $b$ are real constants. Express $v$ in terms of $y$.

### Route Only

Compare the integral with the standard convolution form

```math
y(t)=
\int_{-\infty}^{\infty}x(\lambda)h(t-\lambda)\,d\lambda.
```

Choose the new variable so that the argument of $x$ becomes $\lambda$:

```math
\lambda=-\tau-b.
```

Then

```math
\tau=-\lambda-b,
\qquad
d\tau=-d\lambda.
```

The rest of the problem is to rewrite the argument of $h$ in terms of
$\lambda$, handle the reversed limits carefully, and identify the resulting
convolution value.

---

## Q4. Exercise 4.6(a): Periodicity of Convolution

### Problem

Consider the convolution

```math
y=x\ast h.
```

Assuming that the convolution exists, prove that if $x$ is periodic, then $y$
is periodic.

### Route Only

Let $T$ be a period of $x$, so

```math
x(t+T)=x(t).
```

It is convenient to compare $y(t-T)$ with $y(t)$:

```math
y(t-T)=
\int_{-\infty}^{\infty}
x(\tau)h(t-T-\tau)\,d\tau.
```

Use the change of variable

```math
\lambda=\tau+T.
```

Finish the proof by substituting this into the integral and using the
periodicity of $x$.

---

## Q5. Exercise 4.9: Meaning of LTI

### Problem

Consider an LTI system whose response to

```math
x_{1}(t)=u(t)-u(t-1)
```

is $y_{1}$. Determine the response $y_{2}$ of the system to the input $x_{2}$
shown in the figure.

From the graph,

```math
x_{2}(t)=
\begin{cases}
2, & -2\le t<-1,\\
1, & -1\le t<1,\\
-2, & 1\le t<2,\\
0, & \mathrm{otherwise}.
\end{cases}
```

### Route

Write $x_{2}$ as a linear combination of shifted copies of $x_{1}$. Then apply
linearity and time invariance.

### Knowledge Needed

The signal $x_{1}(t)$ is a unit-height rectangular pulse on $[0,1)$.

A shifted copy $x_{1}(t+2)$ is active on $[-2,-1)$, and $x_{1}(t-1)$ is active
on $[1,2)$.

### Solution

Build $x_{2}$ interval by interval:

```math
x_{2}(t)=
2x_{1}(t+2)+x_{1}(t+1)+x_{1}(t)-2x_{1}(t-1).
```

Because the system is LTI, the output follows the same shifts and scalings:

```math
y_{2}(t)=
2y_{1}(t+2)+y_{1}(t+1)+y_{1}(t)-2y_{1}(t-1).
```

### Final Result

```math
\boxed{
y_{2}(t)=
2y_{1}(t+2)+y_{1}(t+1)+y_{1}(t)-2y_{1}(t-1)
}.
```

