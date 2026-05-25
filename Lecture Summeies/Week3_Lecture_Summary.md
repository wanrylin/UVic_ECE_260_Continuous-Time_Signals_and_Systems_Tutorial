# ECE 260 Week 3 Lecture Summary

Continuous-Time Systems and LTI Analysis  
Slides 82-108: CT systems, system properties, LTI motivation, convolution

This summary focuses on the main ideas and examples from the lectures. The goal
is to help you recognize system properties and set up convolution problems.

---

## 1. Continuous-Time Systems

A continuous-time system maps an input signal to an output signal:

$$
y = Hx.
$$

Here $H$ is an operator. It maps a function to a function, not a number to a
number.

Equivalent notation:

$$
x \xrightarrow{H} y.
$$

If the system is clear from context, this is sometimes shortened to

$$
x \to y.
$$

Important notation warning:

- $=$ means "equals".
- $\to$ means "produces".
- $Hx$ is the whole output signal.
- $(Hx)(t)$ is the output value at time $t$.

### Block Diagrams

A system is often represented as a block:

$$
x \longrightarrow [H] \longrightarrow y.
$$

Two common interconnections are:

### Cascade / Series

The output of $H_{1}$ becomes the input of $H_{2}$:

$$
y = H_{2}(H_{1}x).
$$

The rightmost system acts first.

### Parallel

The same input enters both systems and the outputs are added:

$$
y = H_{1}x + H_{2}x.
$$

---

## 2. How to Test System Properties

For most system properties, there are two possible proof styles:

- To prove the property holds, show it works for arbitrary input signals and
  arbitrary times/constants.
- To prove the property fails, find one counterexample.

This is a major theme in the lecture examples.

---

## 3. Memory

A system is memoryless if the output at time $t_{0}$ depends only on the input at
that same time $t_{0}$.

In other words, $(Hx)(t_{0})$ may depend on $x(t_{0})$, but not on $x(t)$ for
$t\ne t_{0}$.

### Example Pattern

Memoryless:

$$
y(t)=a x(t).
$$

At time $t_{0}$,

$$
y(t_{0})=a x(t_{0}),
$$

so only the current input value is needed.

Has memory:

$$
y(t)=\int_{-\infty}^{t}x(\tau)\,d\tau.
$$

At time $t_{0}$,

$$
y(t_{0})=\int_{-\infty}^{t_{0}}x(\tau)\,d\tau,
$$

so the output depends on many previous input values.

### Check

Ask: to compute the output at one time, do I need input values from other
times?

---

## 4. Causality

A system is causal if the output at time $t_{0}$ depends only on input values at
times $t\le t_{0}$.

It cannot depend on future input values.

Memoryless systems are always causal, but causal systems can still have memory.

### Example Pattern

Causal:

$$
y(t)=\int_{-\infty}^{t}x(\tau)\,d\tau.
$$

At time $t_{0}$, the integral uses only $\tau\le t_{0}$.

Noncausal:

$$
y(t)=\int_{t-1}^{t+1}x(\tau)\,d\tau.
$$

At time $t_{0}$, the integral uses values up to $t_{0}+1$, which are future values.

### Check

Ask: does the formula require any value of $x(\tau)$ with $\tau>t_{0}$?

---

## 5. Invertibility

A system is invertible if the input can always be uniquely determined from the
output.

Equivalently, distinct inputs must always produce distinct outputs:

$$
x_{1}\ne x_{2} \implies Hx_{1}\ne Hx_{2}.
$$

To prove invertibility, find the inverse system.  
To disprove invertibility, find two different inputs that give the same output.

### Example Pattern

Invertible time shift:

$$
y(t)=x(t-T).
$$

Recover the input by shifting back:

$$
x(t)=y(t+T).
$$

So the inverse system is another time shift.

Not invertible:

$$
y(t)=\sin(x(t)).
$$

For example,

$$
x_{1}(t)=0,\qquad x_{2}(t)=2\pi
$$

produce the same output:

$$
\sin(0)=\sin(2\pi)=0.
$$

Therefore the original input cannot be uniquely recovered.

---

## 6. BIBO Stability

BIBO means bounded-input bounded-output.

A system is BIBO stable if every bounded input produces a bounded output.

If

$$
|x(t)| < \infty \quad \forall t,
$$

then a BIBO stable system must guarantee

$$
|(Hx)(t)| < \infty \quad \forall t.
$$

### Example Pattern

Integrator is not BIBO stable:

$$
y(t)=\int_{-\infty}^{t}x(\tau)\,d\tau.
$$

Use the bounded input

$$
x(t)=u(t).
$$

For $t>0$,

$$
y(t)=\int_{0}^{t}1\,d\tau=t,
$$

which grows without bound.

BIBO stable nonlinear example:

$$
y(t)=\sin(x(t)).
$$

Since

$$
|\sin(\theta)|\le1
$$

for all real $\theta$, the output is always bounded by 1.

### Check

To show stable: start with an arbitrary bounded input and bound the output.  
To show unstable: find one bounded input that creates an unbounded output.

---

## 7. Time Invariance

A system is time invariant if delaying or advancing the input produces the same
delay or advance in the output.

Let $S_{t_{0}}$ be the shift operator:

$$
(S_{t_{0}}x)(t)=x(t-t_{0}).
$$

Then $H$ is time invariant if

$$
H(S_{t_{0}}x) = S_{t_{0}}(Hx)
$$

for every input $x$ and every shift $t_{0}$.

### Testing Procedure

1. Shift the input first, then apply the system.
2. Apply the system first, then shift the output.
3. Compare the two expressions.

### Example Pattern

Time-invariant delay system:

$$
y(t)=x(t-T).
$$

Use $T$ for the system's fixed delay and $t_{0}$ for the test shift.

Shift input first:

$$
x'(t)=x(t-t_{0}),
\qquad
(Hx')(t)=x(t-T-t_{0}).
$$

System first, then shift output:

$$
y(t)=x(t-T),
\qquad
y(t-t_{0})=x(t-t_{0}-T).
$$

Both are the same, so the system is time invariant.

Time-varying example:

$$
y(t)=t x(t).
$$

Shift input first:

$$
(Hx')(t)=t x(t-t_{0}).
$$

System first, then shift output:

$$
y(t-t_{0})=(t-t_{0})x(t-t_{0}).
$$

These are not equal in general, so the system is time varying.

---

## 8. Linearity

A system is linear if it satisfies superposition:

$$
H(a_{1}x_{1}+a_{2}x_{2})=a_{1}Hx_{1}+a_{2}Hx_{2}
$$

for all inputs $x_{1},x_{2}$ and all complex constants $a_{1},a_{2}$.

This combines two properties:

- Additivity: $H(x_{1}+x_{2})=Hx_{1}+Hx_{2}$.
- Homogeneity: $H(ax)=aHx$.

### Example Pattern

Linear but time-varying:

$$
y(t)=t x(t).
$$

Apply the system to a linear combination:

$$
H(a_{1}x_{1}+a_{2}x_{2})(t)
=t[a_{1}x_{1}(t)+a_{2}x_{2}(t)]
=a_{1}t x_{1}(t)+a_{2}t x_{2}(t).
$$

This equals

$$
a_{1}(Hx_{1})(t)+a_{2}(Hx_{2})(t),
$$

so the system is linear.

Not linear:

$$
y(t)=|x(t)|.
$$

Let $x(t)=1$ and $a=-1$.

Then

$$
H(ax)=|-1|=1,
$$

but

$$
aHx=-|1|=-1.
$$

The system fails homogeneity, so it is not linear.

### Check

Do not confuse linearity with time invariance. A system can be linear and
time-varying, or nonlinear and time-invariant.

---

## 9. Eigenfunctions of Systems

A signal $x$ is an eigenfunction of system $H$ if applying the system only
multiplies the signal by a constant:

$$
Hx=\lambda x.
$$

The constant $\lambda$ is the eigenvalue.

The key word is constant. If the multiplier depends on time, then the signal is
not an eigenfunction.

### Example Pattern

Consider

$$
y(t)=\frac{d^2}{dt^2}x(t).
$$

For

$$
x(t)=\cos(2t),
$$

we get

$$
\frac{d^2}{dt^2}\cos(2t)=-4\cos(2t).
$$

So $\cos(2t)$ is an eigenfunction with eigenvalue $-4$.

For

$$
x(t)=t^3,
$$

we get

$$
\frac{d^2}{dt^2}t^3=6t.
$$

Although

$$
6t=\frac{6}{t^2}t^3,
$$

the multiplier $6/t^2$ is not a constant. Therefore $t^3$ is not an
eigenfunction.

---

## 10. Why LTI Systems Matter

LTI means linear time-invariant.

LTI systems are important because:

- They are much easier to analyze than general systems.
- Many physical systems can be approximated by LTI models.
- Powerful tools such as convolution, Fourier analysis, and Laplace analysis are
  built around LTI systems.

The rest of the course gives special attention to LTI systems because their
input-output behavior has a clean mathematical structure.

---

## 11. Continuous-Time Convolution

The convolution of two functions $x$ and $h$ is

$$
(x*h)(t)=\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
$$

Convolution produces a new function. The value at time $t$ is obtained by
integrating over the dummy variable $\tau$.

Notation warning:

- $x*h$ is the convolution function.
- $(x*h)(t)$ is the value of that function at time $t$.
- The star $*$ denotes convolution here, not multiplication.

### Interpretation

The expression

$$
h(t-\tau)
$$

is a time-reversed and shifted version of $h(\tau)$, viewed as a function of
$\tau$.

The integral measures the area of the product

$$
x(\tau)h(t-\tau).
$$

As $t$ changes, the shifted function sweeps across $x(\tau)$, and the overlap
area changes.

---

## 12. Practical Convolution Procedure

To compute

$$
(x*h)(t)=\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau,
$$

use this workflow:

1. Plot $x(\tau)$ and $h(t-\tau)$ as functions of $\tau$.
2. Start with $t$ very negative, so $h(t-\tau)$ is far to the left.
3. Identify the overlap region.
4. Write the integral expression for that interval of $t$.
5. Increase $t$ until the overlap pattern changes.
6. Repeat until $t$ is very positive.
7. Combine all intervals into one piecewise answer.

### Common Example Pattern

In examples such as a finite-duration pulse convolved with a causal exponential,
the answer changes form when the moving edge of $h(t-\tau)$ crosses a breakpoint
of $x(\tau)$.

Typical intervals come from overlap changes such as:

- no overlap,
- partial overlap,
- overlap with one segment,
- overlap with multiple segments,
- full overlap.

The main skill is not memorizing the final formula. The main skill is finding
the correct integration limits for each interval.

### Piecewise Linear Convolution

For piecewise linear functions, carefully substitute $t-\tau$ into the formula
for $h$.

For example, if one piece of $h$ is

$$
h(s)=-s-2,
$$

then in convolution,

$$
h(t-\tau)=-(t-\tau)-2=\tau-t-2.
$$

This substitution is a common place for sign mistakes.

---

## 13. Properties of Convolution

Convolution is commutative:

$$
x*h=h*x.
$$

Convolution is associative:

$$
(x*h_{1})*h_{2}=x*(h_{1}*h_{2}).
$$

Convolution is distributive over addition:

$$
x*(h_{1}+h_{2})=x*h_{1}+x*h_{2}.
$$

These properties are useful for simplifying LTI system interconnections.

---

## 14. Impulses and Convolutional Identity

The impulse $\delta$ is the identity element for convolution:

$$
x*\delta=x.
$$

To see this,

$$
(x*\delta)(t)
=\int_{-\infty}^{\infty}x(\tau)\delta(t-\tau)\,d\tau
=x(t).
$$

This result is the basis for representing general signals using shifted
impulses. It also prepares for the key LTI result:

> An LTI system is completely characterized by its impulse response.

That result begins after slide 108.

---

## Common Checks for This Week

- Are you treating $H$ as an operator on functions?
- For memory, does the output at $t_{0}$ need input values at times other than
  $t_{0}$?
- For causality, does the output at $t_{0}$ use any future input values?
- For invertibility, can two different inputs produce the same output?
- For BIBO stability, can you either bound the output or find one bounded-input
  counterexample?
- For time invariance, did you compare "shift input first" with "shift output
  after"?
- For linearity, did you test a general linear combination, or find a clean
  counterexample?
- For eigenfunctions, is the multiplier a constant?
- For convolution, did you use $\tau$ as the integration variable and find the
  correct overlap intervals?
