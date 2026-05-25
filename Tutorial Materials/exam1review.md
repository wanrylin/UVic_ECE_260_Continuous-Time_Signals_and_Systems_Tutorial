# ECE 260 Exam 1 Review Guide

Continuous-Time Signals and Systems  
Exam 1: CT Signals and Systems  
Last updated: 2026-05-25

This guide is a student-friendly review document for Exam 1. It is based on
the official Exam 1 scope, lecture summaries, tutorial materials, and released
Assignment 1, Assignment 2A, and Assignment 2B solutions.

This is not an official course document. For exact exam logistics, permitted
materials, grading rules, and due-date/exam-date information, use the official
course website, Brightspace announcements, lecture slides, and textbook.

---

## 1. Exam Scope and Study Strategy

Exam 1 covers the first major block of the course:

- Appendix A: Complex Analysis review
- Chapter 1: Introduction to signals and systems
- Chapter 2: Preliminaries, notation, functions, mappings, and operators
- Chapter 3: Continuous-time signals and systems
- MATLAB basics may also appear, since MATLAB is fair game for all exams

For the last 1-2 days, prioritize active problem solving:

1. Review definitions only until you can use them.
2. Rework representative problems from Assignments 1, 2A, and 2B.
3. For each problem, write the route before doing algebra.
4. Check common mistakes: notation, time-scaling direction, delta scaling,
   and system-property proof logic.

High-yield released assignment topics:

- Assignment 1: A.1, A.2, A.3, A.4, A.5, A.6, A.11, A.13
- Assignment 2A: 2.1, 2.2, 3.1, 3.2, 3.4, 3.6, 3.9, 3.10, 3.17, 3.20, D.1, D.2
- Assignment 2B: 3.22, 3.24, 3.25, 3.26, 3.27, 3.28, 3.29, 3.33, 3.201, D.3, D.4

---

## 2. Key Topics and Concepts

### 2.1 Complex Analysis Review

You should be comfortable moving between rectangular, polar, and exponential
forms:

```math
z = x + jy = r e^{j\theta} = r(\cos\theta + j\sin\theta).
```

Key meanings:

- $x=\Re\{z\}$ is the real part.
- $y=\Im\{z\}$ is the imaginary part.
- $r=|z|$ is the magnitude.
- $\theta=\arg z$ is the phase angle.

Important routes:

- Rectangular to polar: compute $r=\sqrt{x^2+y^2}$ and choose the angle using
  the correct quadrant.
- Polar to rectangular: expand with Euler's formula.
- Multiplication/division: easiest in polar form.
- Addition/subtraction: easiest in rectangular form.
- Complex conjugation: flip the sign of the imaginary part.

Zeros and poles are usually found from a rational complex function:

```math
F(z)=\frac{N(z)}{D(z)}.
```

- Zeros are values of $z$ that make the numerator zero after simplification.
- Poles are values of $z$ that make the denominator zero after simplification.
- The order or multiplicity comes from repeated factors.
- A common factor in both numerator and denominator may cancel; after
  cancellation, it is usually treated as a removable point rather than a pole.

Example pattern:

```math
F(z)=\frac{(z-1)(z+2)}{(z-3)(z+2)^2}
=
\frac{z-1}{(z-3)(z+2)}.
```

For the simplified function, the zero is $z=1$, and the poles are $z=3$ and
$z=-2$. The cancelled factor changes the interpretation of $z=-2$ compared
with the unsimplified expression, so always simplify first unless the problem
specifically asks about the original expression.

### 2.2 Signals, Functions, and Operators

A signal is a function. The notation distinction matters:

- $x$ means the whole signal.
- $x(t)$ means one value of the signal.
- $\mathcal{H}$ is a system operator.
- $\mathcal{H}x$ is the whole output signal.
- $(\mathcal{H}x)(t)$ is the output value at time $t$.

For cascaded systems, the rightmost operator acts first:

```math
\mathcal{H}_{2}\mathcal{H}_{1}x
=
\mathcal{H}_{2}(\mathcal{H}_{1}x).
```

### 2.3 Time and Amplitude Transformations

For $y(t)=x(at-b)$, factor the argument:

```math
at-b=a\left(t-\frac{b}{a}\right).
```

Interpretation:

- $x(t-b)$ shifts right by $b$.
- $x(t+b)$ shifts left by $b$.
- $x(at)$ compresses if $|a|>1$.
- $x(at)$ stretches if $0<|a|<1$.
- $x(-t)$ reverses time.
- $Ax(t)+C$ scales and shifts amplitude.

For graphing, transform important breakpoints by solving:

```math
at-b=t_{\mathrm{old}}.
```

### 2.4 Periodicity

A signal $x$ is periodic if there exists $T>0$ such that

```math
x(t+T)=x(t)
\qquad \forall t.
```

For sinusoids and complex exponentials:

```math
T=\frac{2\pi}{|\omega|}.
```

For sums of periodic signals, check whether the period ratios are rational. If
$T_{1}/T_{2}$ is irrational, the sum is not periodic.

### 2.5 Symmetry

Even:

```math
x(-t)=x(t).
```

Odd:

```math
x(-t)=-x(t).
```

Even/odd decomposition:

```math
x_{\mathrm{e}}(t)=\frac{x(t)+x(-t)}{2},
\qquad
x_{\mathrm{o}}(t)=\frac{x(t)-x(-t)}{2}.
```

Then

```math
x(t)=x_{\mathrm{e}}(t)+x_{\mathrm{o}}(t).
```

### 2.6 Elementary Signals

Unit step:

```math
u(t)=
\begin{cases}
0, & t<0,\\
1, & t\ge 0.
\end{cases}
```

Window on $[a,b)$:

```math
u(t-a)-u(t-b).
```

Rectangular pulse:

```math
\mathrm{rect}(t)=
\begin{cases}
1, & |t|<\frac{1}{2},\\
0, & |t|>\frac{1}{2}.
\end{cases}
```

Signum:

```math
\mathrm{sgn}(t)=
\begin{cases}
-1, & t<0,\\
0, & t=0,\\
1, & t>0.
\end{cases}
```

### 2.7 Dirac Delta

Sifting property:

```math
\int_{-\infty}^{\infty} f(t)\delta(t-t_{0})\,dt=f(t_{0}).
```

Scaling rule:

```math
\delta(at-b)=\frac{1}{|a|}
\delta\left(t-\frac{b}{a}\right).
```

Shifted impulse:

```math
f(t)\delta(t-t_{0})=f(t_{0})\delta(t-t_{0}).
```

### 2.8 Continuous-Time System Properties

Given $y=\mathcal{H}x$, know how to test:

- Memoryless: output at $t_{0}$ depends only on input at $t_{0}$.
- Causal: output at $t_{0}$ depends only on input values for $t\le t_{0}$.
- Invertible: different inputs always produce different outputs.
- BIBO stable: every bounded input gives a bounded output.
- Time invariant: input shift causes the same output shift.
- Linear: superposition holds.
- Eigenfunction: output is a constant multiple of the input.

### 2.9 MATLAB Basics

High-priority MATLAB ideas:

- Valid identifiers must start with a letter.
- Use `.*`, `./`, and `.^` for element-wise vector operations.
- Logical masks such as `t >= 0` can define signals.
- A MATLAB function should handle scalar and vector inputs when requested.
- For plotting, define a time vector, compute the signal vector, then use
  `plot`, `xlabel`, `ylabel`, and `grid on`.

---

## 3. High-Priority Concept Checklist

| Priority | Topic | What You Should Be Able To Do |
|---|---|---|
| High | Complex numbers | Convert between rectangular, polar, and exponential form |
| High | Zeros and poles | Factor rational complex functions and identify zeros/poles with multiplicity |
| High | Operator notation | Fully parenthesize expressions involving $\mathcal{H}$ and $\mathcal{G}$ |
| High | Time transformations | Sketch or describe $x(at-b)$ from $x(t)$ |
| High | Periodicity | Determine whether a signal or sum of signals is periodic |
| High | Symmetry | Test even/odd and compute even/odd parts |
| High | Unit step | Represent piecewise signals with unit-step windows |
| High | Delta | Evaluate integrals involving impulses and scaling |
| High | System properties | Test memoryless, causal, invertible, stable, time invariant, and linear |
| Medium | Energy and power | Classify simple signals and compute basic quantities |
| Medium | Eigenfunctions | Check whether $\mathcal{H}x=\lambda x$ |
| Medium | MATLAB | Write vectorized expressions and simple functions |
| Quick Review | Introduction | Know examples of signal processing, communication, and control systems |

---

## 4. Important Properties and Tests

### 4.1 Periodicity Test

For a single sinusoid:

```math
x(t)=A\cos(\omega t+\phi)
\quad \Rightarrow \quad
T=\frac{2\pi}{|\omega|}.
```

For a sum:

1. Find each component period.
2. Check whether all period ratios are rational.
3. If yes, find the smallest common period.

### 4.2 Energy and Power

Signal energy:

```math
E_{x}=\int_{-\infty}^{\infty}|x(t)|^2\,dt.
```

Average power:

```math
P_{x}=
\lim_{T\to\infty}
\frac{1}{2T}
\int_{-T}^{T}|x(t)|^2\,dt.
```

Typical patterns:

- Finite-duration bounded signal: usually energy signal.
- Nonzero periodic signal: usually power signal.
- Growing unbounded signal: usually neither.

### 4.3 Memoryless Test

Check whether $(\mathcal{H}x)(t_{0})$ requires $x(\tau)$ for any
$\tau\ne t_{0}$.

Memoryless example:

```math
y(t)=x^2(t).
```

Has memory example:

```math
y(t)=x(t-1).
```

### 4.4 Causality Test

At time $t_{0}$, ask whether the formula uses any $x(\tau)$ with
$\tau>t_{0}$.

Causal:

```math
y(t)=\int_{-\infty}^{t}x(\tau)\,d\tau.
```

Noncausal:

```math
y(t)=x(t+1).
```

### 4.5 Invertibility Test

To prove invertible: construct the inverse system.

To disprove invertible: find two distinct inputs with the same output.

Example of not invertible:

```math
y(t)=x^2(t)
```

because $x_{1}(t)=1$ and $x_{2}(t)=-1$ give the same output.

### 4.6 BIBO Stability Test

Assume the input is bounded:

```math
|x(t)|\le M<\infty.
```

Then test whether the output must also be bounded for every bounded input.

To disprove stability, find one bounded input that produces an unbounded output.

### 4.7 Time-Invariance Test

Use the two-path method. Let

```math
x_{s}(t)=x(t-t_{0}).
```

Path 1: shift input, then apply system:

```math
\mathcal{H}(x_{s}).
```

Path 2: apply system, then shift output:

```math
S_{t_{0}}(\mathcal{H}x).
```

The system is time invariant if the two outputs match for arbitrary $x$ and
arbitrary $t_{0}$.

### 4.8 Linearity Test

A system is linear if

```math
\mathcal{H}(a_{1}x_{1}+a_{2}x_{2})
=
a_{1}\mathcal{H}(x_{1})+a_{2}\mathcal{H}(x_{2})
```

for arbitrary signals $x_{1}$, $x_{2}$ and arbitrary constants $a_{1}$,
$a_{2}$.

Common ways linearity fails:

- constant offset, such as $y(t)=x(t)+1$;
- squaring, such as $y(t)=x^2(t)$;
- absolute value, such as $y(t)=|x(t)|$;
- multiplying the input by itself or another input-dependent quantity.

### 4.9 Eigenfunction Test

$x$ is an eigenfunction of $\mathcal{H}$ if

```math
\mathcal{H}x=\lambda x
```

where $\lambda$ is a constant independent of $t$. If the multiplier depends on
$t$, then it is not an eigenvalue.

---

## 5. Common Problem Types and Solution Routes

### Type 1: Convert Complex Numbers

Usually asks: express a complex number in Cartesian, polar, or exponential form.

Route:

1. Identify the current form.
2. Use Euler's formula if converting from exponential/polar to Cartesian.
3. Use magnitude and quadrant-correct angle if converting to polar.
4. Simplify using special-angle values when possible.

Common mistake: using $\tan^{-1}(y/x)$ without checking the quadrant.

### Type 2: Find Zeros and Poles

Usually asks: find the zeros and poles of a rational complex function, and
possibly sketch them in the complex plane.

Route:

1. Write the function as $F(z)=N(z)/D(z)$.
2. Factor the numerator and denominator completely.
3. Cancel common factors only if the problem asks for the simplified function
   or standard zeros/poles of the function.
4. Zeros come from remaining numerator factors.
5. Poles come from remaining denominator factors.
6. Record multiplicity from repeated factors.
7. Plot zeros with circles and poles with crosses if a complex-plane sketch is
   requested.

Useful factor patterns:

```math
z^2-a^2=(z-a)(z+a)
```

```math
z^2+2az+a^2=(z+a)^2
```

```math
z^2-2r\cos(\theta)z+r^2
=
(z-re^{j\theta})(z-re^{-j\theta})
```

Common mistakes:

- forgetting to simplify common factors;
- treating a constant multiplier as a zero;
- losing repeated roots;
- forgetting that real-coefficient polynomials have complex roots in conjugate
  pairs.

### Type 3: Fully Parenthesize Operator Expressions

Usually asks: show the implied grouping of system operators, functions, and
evaluations.

Route:

1. Identify which symbols are functions and which are numbers.
2. Apply system operators to whole functions.
3. Apply the rightmost operator first in cascades.
4. Evaluate at time only after the output function is formed.

Example pattern:

```math
\mathcal{G}\mathcal{H}y(t)
\quad \Rightarrow \quad
(\mathcal{G}(\mathcal{H}y))(t).
```

Common mistake: writing $\mathcal{H}(y(t))$, which feeds a number into a system
operator.

### Type 4: Strict Mathematical Notation

Usually asks: express a verbal description using strict notation.

Route:

1. Identify the input function.
2. Apply the system operator.
3. Evaluate the output at the requested time.
4. Use parentheses generously.

Example pattern: the output of $\mathcal{H}$ for input $x+y$, evaluated at
$5t$, is

```math
(\mathcal{H}(x+y))(5t).
```

### Type 5: Time and Amplitude Transformations

Usually asks: describe or sketch a transformed signal.

Route:

1. Rewrite the argument as $a(t-b/a)$.
2. Track time reversal if $a<0$.
3. Transform key breakpoints by solving $at-b=t_{\mathrm{old}}$.
4. Apply amplitude scaling and shifting last.

Common mistake: saying $x(2t)$ is stretched. It is compressed by a factor of 2.

### Type 6: Find $y$ in Terms of $x$

Usually gives graphs or expressions for $x$ and $y$ and asks for an expression
such as $y(t)=Ax(at-b)+C$.

Route:

1. Match important time locations.
2. Solve for the time argument $at-b$.
3. Match amplitudes.
4. Check using one or two easy points.

### Type 7: Determine Periodicity

Usually asks: determine if a signal is periodic and find the fundamental period.

Route:

1. Break the signal into sinusoidal/exponential components if possible.
2. Compute component periods.
3. Check rational period ratios.
4. Find the smallest common period.

Common mistake: assuming every sum of periodic signals is periodic.

### Type 8: Even/Odd Symmetry

Usually asks: determine whether a signal is even, odd, both, or neither.

Route:

1. Compute or sketch $x(-t)$.
2. Compare $x(-t)$ with $x(t)$ and $-x(t)$.
3. For sums, remember:
   - even + even = even;
   - odd + odd = odd;
   - even + odd is usually neither.

### Type 9: Reconstruct from Properties

Usually gives constraints such as even/odd, periodicity, or values over one
interval.

Route:

1. Draw the known portion first.
2. Apply symmetry to fill the reflected portion.
3. Apply periodicity to repeat the signal.
4. Check endpoint conventions if step functions or intervals are involved.

### Type 10: Delta-Function Integrals

Usually asks: evaluate an integral involving $\delta(\cdot)$.

Route:

1. Rewrite the impulse in standard shifted form.
2. Apply the scaling rule if needed.
3. Check whether the impulse location is inside the integration interval.
4. Evaluate the non-impulse part at the impulse location.

Common mistake: forgetting the factor $1/|a|$ in $\delta(at-b)$.

### Type 11: Unit-Step Representation

Usually asks: write a piecewise signal as a single expression using $u(t)$.

Route:

1. Write one window for each active interval.
2. Multiply each local expression by its window.
3. Group similar unit-step terms if requested.

Window pattern:

```math
f(t)\ \mathrm{on}\ [a,b)
\quad \Rightarrow \quad
f(t)\,[u(t-a)-u(t-b)].
```

### Type 12: System Property Classification

Usually asks: determine whether a system is memoryless, causal, invertible,
BIBO stable, time invariant, or linear.

Route:

1. Test one property at a time.
2. For "yes", prove using arbitrary input and arbitrary time.
3. For "no", give a counterexample.
4. For time invariance and linearity, use the formal two-path tests.

Common mistake: giving only intuition for time invariance or linearity.

### Type 13: Eigenfunctions

Usually asks: determine whether given signals are eigenfunctions of a system.

Route:

1. Compute $\mathcal{H}x$.
2. Compare the output with $\lambda x$.
3. Decide whether $\lambda$ is a constant.
4. Treat the zero function carefully; it is usually excluded from eigenfunction
   definitions.

### Type 14: MATLAB Vectorization

Usually asks: evaluate expressions, identify valid names, or write functions.

Route:

1. Use `.*`, `./`, and `.^` for vector inputs.
2. Use logical masks for piecewise functions.
3. Test with scalar and vector inputs if the function should support both.

Example:

```matlab
function y = unitstep(t)
    y = double(t >= 0);
end
```

---

## 6. Formula Sheet

### Complex Numbers

```math
e^{j\theta}=\cos\theta+j\sin\theta
```

```math
z=x+jy=re^{j\theta}
```

```math
r=|z|=\sqrt{x^2+y^2}
```

```math
z^*=x-jy
```

```math
z_{1}z_{2}=r_{1}r_{2}e^{j(\theta_{1}+\theta_{2})}
```

```math
\frac{z_{1}}{z_{2}}
=
\frac{r_{1}}{r_{2}}e^{j(\theta_{1}-\theta_{2})}
```

```math
F(z)=\frac{N(z)}{D(z)}
```

```math
N(z_{0})=0
```

$z_{0}$ is a zero if it remains after simplification.

```math
D(p_{0})=0
```

$p_{0}$ is a pole if it remains after simplification.

```math
z^2-2r\cos(\theta)z+r^2
=
(z-re^{j\theta})(z-re^{-j\theta})
```

### Signal Transformations

```math
y(t)=x(t-b)
```

```math
y(t)=x(at-b)
=x\left(a\left(t-\frac{b}{a}\right)\right)
```

```math
at-b=t_{\mathrm{old}}
\quad \Rightarrow \quad
t=\frac{t_{\mathrm{old}}+b}{a}
```

### Symmetry

```math
x\ \mathrm{even} \iff x(-t)=x(t)
```

```math
x\ \mathrm{odd} \iff x(-t)=-x(t)
```

```math
x_{\mathrm{e}}(t)=\frac{x(t)+x(-t)}{2}
```

```math
x_{\mathrm{o}}(t)=\frac{x(t)-x(-t)}{2}
```

### Periodicity

```math
x(t+T)=x(t)
```

```math
T=\frac{2\pi}{|\omega|}
```

```math
f_{0}=\frac{1}{T_{0}},
\qquad
\omega_{0}=\frac{2\pi}{T_{0}}
```

### Energy and Power

```math
E_{x}=\int_{-\infty}^{\infty}|x(t)|^2\,dt
```

```math
P_{x}=
\lim_{T\to\infty}
\frac{1}{2T}\int_{-T}^{T}|x(t)|^2\,dt
```

### Unit Step and Delta

```math
u(t-a)-u(t-b)
```

```math
\int_{-\infty}^{\infty}f(t)\delta(t-t_{0})\,dt=f(t_{0})
```

```math
\delta(at-b)=
\frac{1}{|a|}
\delta\left(t-\frac{b}{a}\right)
```

```math
f(t)\delta(t-t_{0})=f(t_{0})\delta(t-t_{0})
```

### System Properties

```math
\mathcal{H}(a_{1}x_{1}+a_{2}x_{2})
=
a_{1}\mathcal{H}(x_{1})+a_{2}\mathcal{H}(x_{2})
```

```math
x_{s}(t)=x(t-t_{0})
```

```math
\mathcal{H}x=\lambda x
```

---

## 7. Potential Exam Pitfalls

- Confusing $x$ with $x(t)$. A system acts on the whole function $x$, not on one
  scalar value $x(t)$.
- Forgetting that cascaded operators act from right to left.
- Reversing the meaning of $x(t-b)$ and $x(t+b)$.
- Saying $x(at)$ stretches when $a>1$. It compresses.
- Finding sinusoid periods correctly but forgetting to check rational ratios for
  sums.
- Testing even/odd using only one point instead of checking the whole signal.
- Forgetting that an odd finite-valued signal must satisfy $x(0)=0$.
- Forgetting the $1/|a|$ scaling factor for $\delta(at-b)$.
- Applying the delta sifting property when the impulse location is outside the
  integration interval.
- Calling a system time invariant because "there is no explicit $t$" without
  doing the shift test.
- Calling a system linear because it "looks simple" even though it has a
  constant offset, square, absolute value, or product of input values.
- For BIBO stability, testing only one bounded input and concluding stable.
  One counterexample can disprove stability, but proving stability requires all
  bounded inputs.
- In MATLAB, using `*`, `/`, or `^` when element-wise `.*`, `./`, or `.^` is
  needed.

---

## 8. Practice Checklist

Before the exam, you should be able to:

- Convert $re^{j\theta}$ to $x+jy$.
- Convert $x+jy$ to $re^{j\theta}$ with the correct quadrant.
- Use Euler's formula confidently.
- Find zeros and poles of a factored or factorable rational complex function.
- Identify repeated zeros or poles from multiplicity.
- Fully parenthesize expressions such as $\mathcal{G}\mathcal{H}y(t)$.
- Explain the difference between $x$, $x(t)$, $\mathcal{H}x$, and
  $(\mathcal{H}x)(t)$.
- Sketch $x(t-b)$, $x(at)$, $x(-t)$, and $x(at-b)$.
- Determine whether a sinusoid or sum of sinusoids is periodic.
- Test whether a signal is even, odd, both, or neither.
- Compute even and odd components of a signal.
- Represent a piecewise function using unit-step windows.
- Evaluate integrals involving shifted and scaled delta functions.
- Determine whether a system is memoryless.
- Determine whether a system is causal.
- Determine whether a system is invertible, or find a counterexample.
- Determine whether a system is BIBO stable.
- Test time invariance using the two-path method.
- Test linearity using superposition.
- Check whether a function is an eigenfunction of a system.
- Write simple vectorized MATLAB expressions.
- Use logical masks in MATLAB to implement piecewise signals.

---

## 9. Suggested Final Review Plan

### If You Have 48 Hours

1. Spend 30-45 minutes reviewing this guide and marking weak topics.
2. Rework Assignment 1 complex-number questions without looking at solutions.
3. Rework Assignment 2A questions on notation, transformations, periodicity,
   symmetry, and delta functions.
4. Rework Assignment 2B questions on system properties and unit-step
   representation.
5. Do the official practice exam questions if available to you through the
   course website.
6. Make a one-page personal mistake list.

### If You Have 24 Hours

1. Do not reread everything passively.
2. Pick one representative problem from each common problem type.
3. Write the route before solving.
4. Check the released solution only after completing your attempt.
5. Spend the final hour reviewing definitions and common pitfalls.

### Last-Minute Self-Test

Try answering these without notes:

1. What is the difference between $\mathcal{H}x(t)$ and $(\mathcal{H}x)(t)$?
2. Why does $x(2t)$ compress rather than stretch a signal?
3. What condition makes a sum of periodic signals periodic?
4. What is the delta scaling rule?
5. How do you disprove time invariance?
6. How do you disprove linearity?
7. What MATLAB operators should be used for element-wise vector operations?

If you can answer these clearly and solve representative assignment problems
without looking at the solution path, you are in good shape for Exam 1.
