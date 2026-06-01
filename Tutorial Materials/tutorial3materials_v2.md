# ECE 260 Tutorial 3 Materials, Version 2

Continuous-Time LTI Systems and Convolution

This classroom version includes final results and additional worked examples.
It is intended as tutorial support. The textbook, lecture slides, and course
website remain the authoritative course materials.

---

## Quick Recap

### 1. CT LTI Systems and Convolution

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

If an LTI system maps $x_{1}$ to $y_{1}$, then

```math
x_{1}(t-t_{0})
\longrightarrow
y_{1}(t-t_{0}),
```

and scaled sums behave the same way:

```math
a_{1}x_{1}(t-t_{1})+a_{2}x_{1}(t-t_{2})
\longrightarrow
a_{1}y_{1}(t-t_{1})+a_{2}y_{1}(t-t_{2}).
```

### 4. Delta Convolution Facts

The impulse $\delta(t)$ is the identity for convolution:

```math
x(t)\ast\delta(t)=x(t).
```

A shifted impulse shifts the signal:

```math
x(t)\ast\delta(t-t_{0})=x(t-t_{0}).
```

Two shifted impulses convolve by adding their shifts:

```math
\delta(t-a)\ast\delta(t-b)=\delta(t-a-b).
```

These facts are especially useful for block diagrams and cascaded LTI systems.

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

### Solution

For $-1\le t<0$,

```math
y(t)=
2\int_{0}^{t+1}(-1)\,d\tau
=
-2(t+1).
```

For $0\le t<1$,

```math
\begin{aligned}
y(t)
&=
2\int_{0}^{t}1\,d\tau
+
2\int_{t}^{1}(-1)\,d\tau\\
&=
4t-2.
\end{aligned}
```

For $1\le t<2$,

```math
y(t)=
2\int_{t-1}^{1}1\,d\tau
=
4-2t.
```

### Final Result

```math
(x\ast h)(t)=
\begin{cases}
0, & t<-1,\\
-2(t+1), & -1\le t<0,\\
4t-2, & 0\le t<1,\\
4-2t, & 1\le t<2,\\
0, & t\ge 2.
\end{cases}
```

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

The signal $x(\tau)$ is active for $\tau\le0$. The shifted signal
$h(t-\tau)$ is active when

```math
1\le t-\tau<2,
```

or

```math
t-2<\tau\le t-1.
```

The overlap changes at $t=1$ and $t=2$.

### Solution

Inside the active interval of $h(t-\tau)$,

```math
h(t-\tau)=t-1-\tau.
```

For $t<1$, the whole active interval of $h(t-\tau)$ lies to the left of zero:

```math
\begin{aligned}
y(t)
&=
\int_{t-2}^{t-1}
e^{\tau}(t-1-\tau)\,d\tau\\
&=
e^{t-1}-2e^{t-2}.
\end{aligned}
```

For $1\le t<2$, the overlap is from $t-2$ to $0$:

```math
\begin{aligned}
y(t)
&=
\int_{t-2}^{0}
e^{\tau}(t-1-\tau)\,d\tau\\
&=
t-2e^{t-2}.
\end{aligned}
```

For $t\ge2$, there is no nonzero overlap.

### Final Result

```math
(x\ast h)(t)=
\begin{cases}
e^{t-1}-2e^{t-2}, & t<1,\\
t-2e^{t-2}, & 1\le t<2,\\
0, & t\ge2.
\end{cases}
```

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

### Solution

Compare with

```math
y(t)=
\int_{-\infty}^{\infty}x(\lambda)h(t-\lambda)\,d\lambda.
```

Let

```math
\lambda=-\tau-b.
```

Then

```math
\tau=-\lambda-b,
\qquad
d\tau=-d\lambda.
```

The limits reverse:

```math
\tau=-\infty \Rightarrow \lambda=\infty,
\qquad
\tau=\infty \Rightarrow \lambda=-\infty.
```

Therefore,

```math
\begin{aligned}
v(t)
&=
\int_{\infty}^{-\infty}
x(\lambda)h(a-b-\lambda)(-d\lambda)\\
&=
\int_{-\infty}^{\infty}
x(\lambda)h(a-b-\lambda)\,d\lambda.
\end{aligned}
```

This is the convolution $x\ast h$ evaluated at $a-b$.

### Final Result

```math
\boxed{v(t)=y(a-b).}
```

The result is independent of $t$.

---

## Q4. Exercise 4.6(a): Periodicity of Convolution

### Problem

Consider the convolution

```math
y=x\ast h.
```

Assuming that the convolution exists, prove that if $x$ is periodic, then $y$
is periodic.

### Solution

Let $T$ be a period of $x$, so

```math
x(t+T)=x(t).
```

Compare $y(t-T)$ with $y(t)$:

```math
y(t-T)=
\int_{-\infty}^{\infty}
x(\tau)h(t-T-\tau)\,d\tau.
```

Use the change of variable

```math
\lambda=\tau+T.
```

Then

```math
\tau=\lambda-T,
\qquad
d\tau=d\lambda.
```

Substitute into the integral:

```math
\begin{aligned}
y(t-T)
&=
\int_{-\infty}^{\infty}
x(\lambda-T)h(t-\lambda)\,d\lambda\\
&=
\int_{-\infty}^{\infty}
x(\lambda)h(t-\lambda)\,d\lambda\\
&=
y(t).
\end{aligned}
```

The second equality uses the periodicity of $x$.

### Final Result

```math
\boxed{y(t-T)=y(t).}
```

So $y$ is periodic with period $T$.

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

### Solution

Since $x_{1}$ is a unit-height pulse on $[0,1)$,

```math
x_{2}(t)=
2x_{1}(t+2)+x_{1}(t+1)+x_{1}(t)-2x_{1}(t-1).
```

The system is LTI, so the same shifts and scalings apply to the output:

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

---

## Q6. MATLAB D.5: Plot Magnitude and Phase

### Problem

Let

```math
F(\omega)=\frac{1}{j\omega+1}.
```

Plot $|F(\omega)|$ and $\arg F(\omega)$ for $\omega\in[-10,10]$. Use
`subplot` to place both plots on the same figure.

### MATLAB Code

```matlab
% D.5
% Plot magnitude and phase of F(w) = 1 / (j*w + 1)

w = linspace(-10, 10, 2000);
F = 1 ./ (1j*w + 1);

magF = abs(F);
phaseF = angle(F);

figure;

subplot(2, 1, 1);
plot(w, magF, 'LineWidth', 1.5);
grid on;
xlabel('\omega');
ylabel('|F(\omega)|');
title('Magnitude of F(\omega)');

subplot(2, 1, 2);
plot(w, phaseF, 'LineWidth', 1.5);
grid on;
xlabel('\omega');
ylabel('arg F(\omega) [rad]');
title('Phase of F(\omega)');
```

### Formula Check

```math
|F(\omega)|=\frac{1}{\sqrt{1+\omega^2}},
\qquad
\arg F(\omega)=-\tan^{-1}(\omega).
```

---

## Q7. Exercise 4.11(b): Find Impulse Response

### Problem

Find the impulse response of the LTI system $\mathcal{H}$ characterized by

```math
(\mathcal{H}x)(t)=
\int_{-\infty}^{\infty}
x(\tau+5)e^{\tau-t+1}u(t-\tau-2)\,d\tau.
```

### Route

The impulse response is the output when the input is $\delta$:

```math
h=\mathcal{H}\delta.
```

### Solution

Set $x=\delta$:

```math
h(t)=
\int_{-\infty}^{\infty}
\delta(\tau+5)e^{\tau-t+1}u(t-\tau-2)\,d\tau.
```

The impulse $\delta(\tau+5)$ samples the integrand at $\tau=-5$:

```math
h(t)=
e^{-5-t+1}u(t+5-2).
```

Thus,

```math
h(t)=e^{-t-4}u(t+3).
```

### Final Result

```math
\boxed{h(t)=e^{-t-4}u(t+3).}
```

---

## Q8. Exercise 4.12: LTI Block Diagram

### Problem

The system is an LTI block diagram. The input has a direct path to the final
summer. The input also passes through $h_{1}$, and then splits into two branches
through $h_{2}$ and $h_{3}$. Find the overall impulse response.

### Delta Convolution Review

For block diagrams:

- series LTI systems correspond to convolution;
- parallel LTI systems correspond to addition;
- a direct path contributes $\delta(t)$;
- convolution with $\delta(t)$ leaves a signal unchanged.

### Part (a)

The direct path contributes

```math
\delta.
```

The two lower branches contribute

```math
h_{1}\ast h_{2}
\qquad \mathrm{and} \qquad
h_{1}\ast h_{3}.
```

Therefore,

```math
h=\delta+h_{1}\ast h_{2}+h_{1}\ast h_{3}.
```

### Part (b)

For

```math
h_{1}(t)=\delta(t+1),
\qquad
h_{2}(t)=\delta(t),
\qquad
h_{3}(t)=\delta(t),
```

use the result from part (a):

```math
\begin{aligned}
h(t)
&=
\delta(t)
+
\delta(t+1)\ast\delta(t)
+
\delta(t+1)\ast\delta(t)\\
&=
\delta(t)+2\delta(t+1).
\end{aligned}
```

### Final Result

```math
\boxed{
h=\delta+h_{1}\ast h_{2}+h_{1}\ast h_{3}
}
```

and, for the specific case,

```math
\boxed{
h(t)=\delta(t)+2\delta(t+1).
}
```

---

## Q9. Exercise 4.13(b): Series LTI System

### Problem

The system is a series interconnection of two LTI systems with input

```math
x(t)=u(t).
```

For part (b),

```math
h_{1}(t)=\delta(t+1),
\qquad
h_{2}(t)=\delta(t+1).
```

Find the output $y$.

### Delta Convolution Review

The impulse $\delta(t+1)=\delta(t-(-1))$ advances a signal by $1$:

```math
x(t)\ast\delta(t+1)=x(t+1).
```

Also,

```math
\delta(t+1)\ast\delta(t+1)=\delta(t+2).
```

### Solution

For a series LTI system,

```math
y=x\ast h_{1}\ast h_{2}.
```

First combine the two impulse responses:

```math
h_{1}\ast h_{2}
=
\delta(t+1)\ast\delta(t+1)
=
\delta(t+2).
```

Then

```math
y(t)=u(t)\ast\delta(t+2).
```

Convolution with $\delta(t+2)$ advances the input by $2$:

```math
y(t)=u(t+2).
```

### Final Result

```math
\boxed{y(t)=u(t+2).}
```

---

## Q10. Exercise 4.14(b): Causality and Memory

### Problem

Determine whether the LTI system with impulse response

```math
h(t)=2\delta(t+1)
```

is causal and/or memoryless.

### Knowledge Needed

For an LTI system:

- causal iff $h(t)=0$ for all $t<0$;
- memoryless iff $h(t)=K\delta(t)$ for some constant $K$.

### Solution

The impulse $\delta(t+1)$ is located at $t=-1$, which is negative time. So the
impulse response is not zero for all $t<0$. Therefore the system is not causal.

Also,

```math
x(t)\ast 2\delta(t+1)=2x(t+1).
```

The output at time $t$ depends on the input at time $t+1$, not only on $x(t)$.
So the system is not memoryless.

### Final Result

```math
\boxed{\mathrm{not\ causal,\ not\ memoryless}.}
```

---

## Q11. Exercise 4.15(c): BIBO Stability

### Problem

Determine whether the LTI system with impulse response

```math
h(t)=e^{t}u(t)
```

is BIBO stable.

### Knowledge Needed

An LTI system is BIBO stable iff its impulse response is absolutely integrable:

```math
\int_{-\infty}^{\infty}|h(t)|\,dt<\infty.
```

### Solution

Since $u(t)$ restricts the signal to $t\ge0$,

```math
\int_{-\infty}^{\infty}|h(t)|\,dt
=
\int_{0}^{\infty}e^{t}\,dt.
```

But

```math
\int_{0}^{\infty}e^{t}\,dt=\infty.
```

### Final Result

```math
\boxed{\mathrm{not\ BIBO\ stable}.}
```

---

## Q12. Exercise 4.16: Inverse Systems

### Problem

Suppose we have two LTI systems with impulse responses

```math
h_{1}(t)=\frac{1}{2}\delta(t-1),
\qquad
h_{2}(t)=2\delta(t+1).
```

Determine whether these systems are inverses of one another.

### Route

Two LTI systems are inverses if their cascade has impulse response $\delta(t)$.
So compute

```math
h_{1}\ast h_{2}.
```

### Solution

```math
\begin{aligned}
h_{1}\ast h_{2}
&=
\left(\frac{1}{2}\delta(t-1)\right)
\ast
\left(2\delta(t+1)\right)\\
&=
\delta(t-1)\ast\delta(t+1).
\end{aligned}
```

The shifts add:

```math
\delta(t-1)\ast\delta(t+1)
=
\delta(t).
```

Therefore,

```math
h_{1}\ast h_{2}=\delta(t).
```

Another way to read this:

```math
x(t)\ast h_{1}(t)=\frac{1}{2}x(t-1),
```

and then

```math
\left(\frac{1}{2}x(t-1)\right)\ast h_{2}(t)=x(t).
```

### Final Result

```math
\boxed{\mathrm{Yes,\ the\ systems\ are\ inverses}.}
```

---

## Q13. Exercise 4.17(a): System Function and Eigenfunctions

### Problem

For the LTI system with system function

```math
H(s)=\frac{1}{s+1},
\qquad
\Re\{s\}>-1,
```

find the response to

```math
x(t)=10+4\cos(3t)+2\sin(5t).
```

### Knowledge Needed

For an LTI system, complex exponentials are eigenfunctions:

```math
\mathcal{H}\{e^{st}\}=H(s)e^{st}.
```

The values $s=0$, $s=j3$, and $s=j5$ are all in the region of convergence since
their real parts are $0>-1$.

If

```math
H(j\omega)=a+jb,
```

then

```math
A\cos(\omega t)
\longrightarrow
A[a\cos(\omega t)-b\sin(\omega t)],
```

and

```math
A\sin(\omega t)
\longrightarrow
A[a\sin(\omega t)+b\cos(\omega t)].
```

### Solution

For the constant term,

```math
H(0)=1,
```

so

```math
10 \longrightarrow 10.
```

For the $\cos(3t)$ term,

```math
H(j3)=\frac{1}{1+j3}
=
\frac{1-j3}{10}.
```

Thus $a=1/10$ and $b=-3/10$, so

```math
\begin{aligned}
4\cos(3t)
&\longrightarrow
4\left[
\frac{1}{10}\cos(3t)
-
\left(-\frac{3}{10}\right)\sin(3t)
\right]\\
&=
\frac{2}{5}\cos(3t)+\frac{6}{5}\sin(3t).
\end{aligned}
```

For the $\sin(5t)$ term,

```math
H(j5)=\frac{1}{1+j5}
=
\frac{1-j5}{26}.
```

Thus $a=1/26$ and $b=-5/26$, so

```math
\begin{aligned}
2\sin(5t)
&\longrightarrow
2\left[
\frac{1}{26}\sin(5t)
+
\left(-\frac{5}{26}\right)\cos(5t)
\right]\\
&=
-\frac{5}{13}\cos(5t)+\frac{1}{13}\sin(5t).
\end{aligned}
```

Add the three responses.

### Final Result

```math
\boxed{
y(t)=
10
+
\frac{2}{5}\cos(3t)
+
\frac{6}{5}\sin(3t)
-
\frac{5}{13}\cos(5t)
+
\frac{1}{13}\sin(5t)
}.
```

---

## Q14. MATLAB D.8: Draw Pattern

### Problem

Write a MATLAB function called `drawpattern` that takes $n$ and $\theta$ as
input arguments, with $\theta$ specified in degrees. The function computes and
plots points $p_{0},p_{1},\ldots,p_{n-1}$ in the plane. The first point is
$p_{0}=[0\ 0]^T$, and the remaining points satisfy

```math
p_{i}
=
p_{i-1}
+
\begin{bmatrix}
\cos\theta & \sin\theta\\
-\sin\theta & \cos\theta
\end{bmatrix}^{i-1}
\begin{bmatrix}
i\\
0
\end{bmatrix}.
```

For part (b), generate the plots with $n=100$ and

```math
\theta=89^\circ,\quad 144^\circ,\quad 154^\circ.
```

### Route Only

Use a loop because each new point depends on the previous point.

Recommended implementation idea:

1. Convert $\theta$ from degrees to radians.
2. Form the rotation matrix

```math
R=
\begin{bmatrix}
\cos\theta & \sin\theta\\
-\sin\theta & \cos\theta
\end{bmatrix}.
```

3. Allocate a matrix to store the points.
4. Start with $p_{0}=[0\ 0]^T$.
5. Keep a running matrix power. Start with $R^{0}=I$.
6. For each $i=1,\ldots,n-1$, compute the step

```math
R^{i-1}
\begin{bmatrix}
i\\
0
\end{bmatrix},
```

add it to the previous point, and then update the running power of $R$.
7. Plot the stored points with straight lines and use `axis equal`.

### Recurrence vs Recursion Note

The formula is a recurrence relation because $p_{i}$ is defined using
$p_{i-1}$. A MATLAB `for` loop is an iterative way to compute this recurrence.
It is not recursive programming unless the function calls itself.

