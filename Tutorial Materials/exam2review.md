# ECE 260 Exam 2 Review Guide

Continuous-Time LTI Systems  
Exam 2: Chapter 4 and MATLAB  
Last updated: 2026-06-04

This guide is a student-friendly review document for Exam 2 and is intended to
support tutorial review. It is based on the posted Exam 2 information, the
posted study guide, lecture summaries, tutorial materials, and assignment
topics.

This is not an official course document. For exact exam logistics, permitted
materials, grading rules, and due-date/exam-date information, use the official
course website, Brightspace announcements, lecture slides, and textbook.

---

## 1. Exam Format and Scope

Exam 2 is focused on:

- Chapter 4: Continuous-Time Linear Time-Invariant Systems
- MATLAB basics from Appendix D

Exam conditions:

- 50 minutes
- closed book
- no calculators
- no formula sheet

MATLAB questions are fair game for all exams in the course, but an individual
exam may or may not include MATLAB questions.

The general answering advice from Exam 1 still applies: write clearly, define
your route, show enough work for partial credit, and do not skip the setup.

You are not responsible for periodic convolution from Section 4.4 if it was not
covered in lecture.

---

## 2. High-Yield Study Strategy

The most important preparation step is to compare your assignment answers with
the posted solutions. Do this actively:

1. Rework the problem without looking.
2. Compare your route with the posted route.
3. Mark where your setup first differs.
4. Redo the problem from that point.

For the last few days before the exam, prioritize:

- posted practice exam;
- Assignment 3 solutions and any posted solutions;
- old assignment problems;
- textbook end-of-chapter problems with answer keys;
- video lecture examples;
- skipped textbook examples;
- worked-through lecture exercises;
- tutorial examples and extra practice problems.

Because there is no formula sheet, spend time memorizing the small set of core
tests and formulas in this guide.

---

## 3. Core Formulas to Know

### Convolution

```math
(x\ast h)(t)
=
\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
```

Main properties:

```math
x\ast h=h\ast x,
```

```math
x\ast(h_{1}+h_{2})=x\ast h_{1}+x\ast h_{2},
```

```math
(x\ast h_{1})\ast h_{2}
=
x\ast(h_{1}\ast h_{2}).
```

### LTI System Output

For an LTI system with impulse response $h$,

```math
y=x\ast h.
```

The impulse response is the response to $\delta(t)$:

```math
h=\mathcal{H}\delta.
```

The step response is the response to $u(t)$:

```math
s=\mathcal{H}u.
```

For an LTI system,

```math
s(t)=
\int_{-\infty}^{t}h(\lambda)\,d\lambda,
```

so

```math
h(t)=\frac{ds(t)}{dt}.
```

### Delta Convolution

```math
x(t)\ast\delta(t)=x(t).
```

```math
x(t)\ast\delta(t-t_{0})=x(t-t_{0}).
```

```math
\delta(t-a)\ast\delta(t-b)=\delta(t-a-b).
```

### LTI Interconnections

Series/cascade:

```math
h_{\mathrm{series}}=h_{1}\ast h_{2}.
```

Parallel:

```math
h_{\mathrm{parallel}}=h_{1}+h_{2}.
```

A direct path from input to output contributes $\delta(t)$.

### LTI System Property Tests

Memoryless:

```math
h(t)=K\delta(t)
```

for some constant $K$.

Causal:

```math
h(t)=0
\qquad \mathrm{for}\ t<0.
```

BIBO stable:

```math
\int_{-\infty}^{\infty}|h(t)|\,dt<\infty.
```

Invertible:

```math
h\ast h_{\mathrm{inv}}=\delta.
```

Complex exponential eigenfunction:

```math
\mathcal{H}\{e^{st}\}(t)=H(s)e^{st}.
```

System function:

```math
H(s)=
\int_{-\infty}^{\infty}h(t)e^{-st}\,dt.
```

If

```math
x(t)=\sum_{k}a_{k}e^{s_{k}t},
```

then

```math
y(t)=\sum_{k}a_{k}H(s_{k})e^{s_{k}t}.
```

---

## 4. How to Approach Common Problem Types

### 4.1 Graphical Convolution

Use the same route every time:

1. Write

```math
y(t)=
\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
```

2. Identify the support of $x(\tau)$.
3. Flip and shift $h$ to get $h(t-\tau)$.
4. Find the overlap interval in $\tau$.
5. Find the breakpoints where the overlap changes.
6. Set up one integral for each interval of $t$.
7. Check that the result is zero outside the support sum.

For finite-duration signals, if $x$ is supported on $[A,B]$ and $h$ is
supported on $[C,D]$, then $x\ast h$ can only be nonzero on

```math
[A+C,\ B+D].
```

Common mistake: forgetting that $h(t-\tau)$ is the flipped-and-shifted version
of $h$, not simply $h(\tau-t)$.

#### Matched Example: Exercise 4.1(c)

Compute $x\ast h$ graphically, where

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

The support of $x$ is $[0,1]$, and the support of $h$ is $[-1,1]$, so
$x\ast h$ can only be nonzero on $[-1,2]$. The overlap changes at

```math
t=-1,\ 0,\ 1,\ 2.
```

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

Thus,

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

### 4.2 Impulse Response from a System Equation

If the problem gives a system equation, set the input to $\delta$:

```math
h(t)=(\mathcal{H}\delta)(t).
```

Then simplify using the sifting property:

```math
\int_{-\infty}^{\infty}f(\tau)\delta(\tau-\tau_{0})\,d\tau
=
f(\tau_{0}).
```

If the system equation already looks like convolution,

```math
(\mathcal{H}x)(t)=
\int_{-\infty}^{\infty}x(\tau)g(t-\tau)\,d\tau,
```

then the impulse response is $g(t)$.

#### Matched Example: Exercise 4.11(b)

Find the impulse response of the LTI system

```math
(\mathcal{H}x)(t)=
\int_{-\infty}^{\infty}
x(\tau+5)e^{\tau-t+1}u(t-\tau-2)\,d\tau.
```

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

Therefore,

```math
\boxed{h(t)=e^{-t-4}u(t+3).}
```

### 4.3 Step Response and Unit-Step Inputs

If the step response is given as $s(t)$, use

```math
h(t)=\frac{ds(t)}{dt}.
```

Watch for jumps in $s(t)$. A jump of size $A$ at $t=t_{0}$ contributes

```math
A\delta(t-t_{0})
```

to the derivative.

If the input is $x(t)=u(t)$ and the system is LTI, then the output is the step
response of that system:

```math
s(t)=u(t)\ast h(t).
```

#### Matched Example: Exercise 4.13(b)

This example is a unit-step input through a series LTI system, so it is a
step-response-style calculation for the overall system.

The input is

```math
x(t)=u(t),
```

and

```math
h_{1}(t)=\delta(t+1),
\qquad
h_{2}(t)=\delta(t+1).
```

For a series LTI system,

```math
y=x\ast h_{1}\ast h_{2}.
```

First combine the impulse responses:

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
\boxed{y(t)=u(t+2).}
```

### 4.4 Block Diagrams

Translate the diagram into convolution and addition:

- series means convolution;
- parallel means addition;
- direct path means $\delta(t)$;
- a splitter sends the same signal to multiple branches;
- a summer adds the branch outputs.

For example, if one direct path and two filtered branches meet at a summer, the
overall impulse response has the pattern

```math
h=\delta+\mathrm{branch}_{1}+\mathrm{branch}_{2}.
```

#### Matched Example: Exercise 4.12

The system has a direct path to the final summer. The input also passes through
$h_{1}$, then splits into branches through $h_{2}$ and $h_{3}$.

The direct path contributes

```math
\delta.
```

The two filtered branches contribute

```math
h_{1}\ast h_{2}
\qquad \mathrm{and} \qquad
h_{1}\ast h_{3}.
```

So the overall impulse response is

```math
\boxed{
h=\delta+h_{1}\ast h_{2}+h_{1}\ast h_{3}
}.
```

For the specific case

```math
h_{1}(t)=\delta(t+1),
\qquad
h_{2}(t)=\delta(t),
\qquad
h_{3}(t)=\delta(t),
```

we get

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
\boxed{\delta(t)+2\delta(t+1)}.
\end{aligned}
```

### 4.5 Causality and Memory

For LTI systems, do not go back to the original input-output definition unless
you have to. Use the impulse response.

Causal:

- allowed support: $t\ge0$;
- any nonzero part of $h$ for $t<0$ means not causal.

Memoryless:

- only allowed impulse response shape is $K\delta(t)$;
- shifted impulses like $\delta(t+1)$ or ordinary functions like $u(t)$ are not
  memoryless.

#### Matched Example: Exercise 4.14(b)

Determine whether the LTI system with impulse response

```math
h(t)=2\delta(t+1)
```

is causal and/or memoryless.

The impulse $\delta(t+1)$ is located at $t=-1$, which is negative time. So the
impulse response is not zero for all $t<0$. Therefore the system is not causal.

Also,

```math
x(t)\ast 2\delta(t+1)=2x(t+1).
```

The output at time $t$ depends on the input at time $t+1$, not only on $x(t)$.
So the system is not memoryless.

Final answer:

```math
\boxed{\mathrm{not\ causal,\ not\ memoryless}.}
```

### 4.6 BIBO Stability

Use the absolute-integrability test:

```math
\int_{-\infty}^{\infty}|h(t)|\,dt<\infty.
```

Useful patterns:

- finite-width rectangular or triangular signals are stable;
- decaying exponentials on a half-line can be stable;
- growing exponentials are not stable;
- $u(t)$ is not stable because its integral over $[0,\infty)$ diverges;
- impulses have finite area and are usually stable in this LTI context.

#### Matched Example: Exercise 4.15(c)

Determine whether the LTI system with impulse response

```math
h(t)=e^{t}u(t)
```

is BIBO stable.

Use the absolute-integrability test:

```math
\int_{-\infty}^{\infty}|h(t)|\,dt
=
\int_{0}^{\infty}e^{t}\,dt.
```

But

```math
\int_{0}^{\infty}e^{t}\,dt=\infty.
```

Therefore,

```math
\boxed{\mathrm{not\ BIBO\ stable}.}
```

### 4.7 Invertibility

For an LTI system, an inverse system must satisfy

```math
h\ast h_{\mathrm{inv}}=\delta.
```

For shifted/scaled impulses,

```math
h(t)=a\delta(t-t_{0}),
\qquad
a\ne0,
```

the inverse is

```math
h_{\mathrm{inv}}(t)=\frac{1}{a}\delta(t+t_{0}).
```

#### Matched Example: Exercise 4.16

Suppose two LTI systems have impulse responses

```math
h_{1}(t)=\frac{1}{2}\delta(t-1),
\qquad
h_{2}(t)=2\delta(t+1).
```

They are inverses if their cascade has impulse response $\delta(t)$.

```math
\begin{aligned}
h_{1}\ast h_{2}
&=
\left(\frac{1}{2}\delta(t-1)\right)
\ast
\left(2\delta(t+1)\right)\\
&=
\delta(t-1)\ast\delta(t+1)\\
&=
\delta(t).
\end{aligned}
```

Therefore,

```math
\boxed{\mathrm{Yes,\ the\ systems\ are\ inverses}.}
```

### 4.8 Eigenfunctions and System Functions

If the input is a sum of constants, cosines, sines, or complex exponentials,
try the eigenfunction route instead of convolution.

Constants are exponentials with $s=0$:

```math
1=e^{0t}.
```

Cosines and sines can be represented using complex exponentials:

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

Then multiply each exponential by the correct value of $H(s)$.

#### Matched Example: Exercise 4.17(a)

For the LTI system with

```math
H(s)=\frac{1}{s+1},
\qquad
\Re\{s\}>-1,
```

find the response to

```math
x(t)=10+4\cos(3t)+2\sin(5t).
```

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

Thus,

```math
4\cos(3t)
\longrightarrow
\frac{2}{5}\cos(3t)+\frac{6}{5}\sin(3t).
```

For the $\sin(5t)$ term,

```math
H(j5)=\frac{1}{1+j5}
=
\frac{1-j5}{26}.
```

Thus,

```math
2\sin(5t)
\longrightarrow
-\frac{5}{13}\cos(5t)+\frac{1}{13}\sin(5t).
```

Adding the three responses gives

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

## 5. MATLAB Checklist

MATLAB questions may test basic syntax and vectorized thinking.

Know:

- arrays, vectors, and matrices;
- array subscripting;
- arithmetic operators: `+`, `-`, `*`, `/`, `^`, `.*`, `./`, `.^`;
- relational operators: `==`, `~=`, `<`, `<=`, `>`, `>=`;
- logical operators: `&`, `|`, `~`;
- `for` loops and `while` loops;
- `if`, `elseif`, `else`;
- user-defined functions;
- basic functions such as `size`, `length`, `real`, `imag`, `abs`, `angle`,
  and `plot`;
- element-wise operations.

### Vectorization Pattern

Instead of looping through every element of a vector, use element-wise
operations and logical masks.

Example:

```matlab
t = linspace(-5, 5, 1000);
x = exp(-t) .* (t >= 0);
```

Here `(t >= 0)` creates a logical mask that acts like a unit step.

### Common MATLAB Mistakes

- using `*`, `/`, or `^` when `.*`, `./`, or `.^` is needed;
- using `&&` when element-wise `&` is needed;
- forgetting that MATLAB indexes start at `1`;
- writing a function without matching the file name;
- writing unnecessary loops when vector operations would be clearer.

---

## 6. Suggested Tutorial Review Flow

For a 50-minute review tutorial, a reasonable plan is:

1. Five minutes: exam format, no-calculator strategy, and what to memorize.
2. Fifteen minutes: graphical convolution route and one representative setup.
3. Ten minutes: impulse response, step response, and block diagrams.
4. Ten minutes: causality, memory, BIBO stability, and invertibility tests.
5. Five minutes: eigenfunctions and system functions.
6. Five minutes: MATLAB checklist and last-minute study plan.

The goal is not to redo every assignment problem. The goal is to make the
problem routes automatic.

---

## 7. Final Review Checklist

Before the exam, you should be able to do the following without notes:

- write the convolution integral correctly;
- identify overlap intervals for graphical convolution;
- explain why LTI systems are characterized by impulse response;
- compute an impulse response by setting $x=\delta$;
- compute $h$ from a step response $s$ by differentiating;
- simplify series and parallel LTI block diagrams;
- test memoryless, causal, BIBO stable, and invertible from $h$;
- use delta convolution to handle shifts and delays;
- explain what it means for $e^{st}$ to be an eigenfunction;
- compute an LTI output from a weighted sum of complex exponentials;
- recognize when MATLAB code needs element-wise operators.

---

## 8. Last 24-Hour Plan

Use the final day for active review:

1. Rework two graphical convolution problems.
2. Rework one impulse-response problem from a system equation.
3. Rework one block-diagram problem.
4. Rework one causality/memory/stability/invertibility classification problem.
5. Rework one eigenfunction/system-function problem.
6. Review one MATLAB vectorization example.
7. Compare all work against posted solutions and fix route mistakes.

Avoid spending the final hours only rereading notes. The exam is short, closed
book, and no-calculator, so fast setup matters more than long algebra.
