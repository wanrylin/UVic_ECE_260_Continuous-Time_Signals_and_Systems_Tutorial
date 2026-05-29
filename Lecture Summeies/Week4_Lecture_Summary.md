# ECE 260 Week 4 Lecture Summary

Continuous-Time LTI Systems and Impulse Response  
Slides 108-115: impulse response, step response, LTI interconnections, memory,
and causality

This summary focuses on how LTI systems are represented and analyzed through
their impulse responses. The goal is to connect the convolution idea from the
previous lectures to practical system analysis.

---

## 1. Impulse Response

The impulse response of a system is the output produced when the input is the
Dirac delta function.

For a system $\mathcal{H}$, the impulse response $h$ is

```math
h=\mathcal{H}\delta.
```

For a general system, the impulse response is only one special output. For a
linear time-invariant system, it is much more powerful:

> An LTI system is completely characterized by its impulse response.

This means that if we know $h$, then we can determine the output for any input
$x$.

---

## 2. The Key LTI Result

For an LTI system with input $x$, output $y$, and impulse response $h$,

```math
y=x\ast h.
```

Equivalently, at time $t$,

```math
y(t)=(x\ast h)(t)
=
\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
```

So an LTI system simply computes a convolution between the input and its impulse
response.

### Why This Is True

The input signal can be written using the convolutional identity:

```math
x=x\ast\delta.
```

In evaluated form,

```math
x(t)=
\int_{-\infty}^{\infty}x(\tau)\delta(t-\tau)\,d\tau.
```

Now pass this input through an LTI system:

```math
y=\mathcal{H}x.
```

The proof idea has two ingredients:

- Linearity lets the system act through the integral and scaling by
  $x(\tau)$.
- Time invariance turns the response to $\delta(t-\tau)$ into a shifted
  impulse response $h(t-\tau)$.

Therefore,

```math
y(t)=
\int_{-\infty}^{\infty}x(\tau)h(t-\tau)\,d\tau.
```

This is exactly convolution.

### Teaching Point

The theorem is not saying every system computes convolution. It is saying every
LTI system computes convolution with its own impulse response.

---

## 3. Example: Integrator as an LTI System

Suppose an LTI system has impulse response

```math
h(t)=u(t).
```

Then the output is

```math
y(t)=
\int_{-\infty}^{\infty}x(\tau)u(t-\tau)\,d\tau.
```

The factor $u(t-\tau)$ acts as a switch:

```math
u(t-\tau)=1
\quad \mathrm{when} \quad
\tau\le t,
```

and

```math
u(t-\tau)=0
\quad \mathrm{when} \quad
\tau>t.
```

So the integral reduces to

```math
y(t)=
\int_{-\infty}^{t}x(\tau)\,d\tau.
```

Thus, the LTI system with impulse response $u(t)$ is an integrator.

### Common Check

When a unit step appears inside an integral, use it to determine the active
range of integration.

---

## 4. Step Response

The step response $s$ of a system is the output produced when the input is the
unit step function:

```math
s=\mathcal{H}u.
```

For an LTI system,

```math
s=u\ast h.
```

Since convolution with $u$ integrates a signal,

```math
s(t)=
\int_{-\infty}^{t}h(\tau)\,d\tau.
```

Therefore,

```math
h(t)=\frac{ds(t)}{dt}.
```

### Why Step Response Matters

A true impulse $\delta(t)$ is not physically realizable. In practice, it is
often easier to measure the step response and then differentiate it to obtain
the impulse response.

---

## 5. Block Diagrams for LTI Systems

Because an LTI system is completely characterized by $h$, we often label an LTI
system block by its impulse response.

The block diagram

```math
x \longrightarrow [h] \longrightarrow y
```

means

```math
y=x\ast h.
```

This is a more concrete version of the general system notation
$y=\mathcal{H}x$.

---

## 6. Interconnection of LTI Systems

LTI interconnections can be simplified using convolution properties.

### Series / Cascade

If two LTI systems with impulse responses $h_{1}$ and $h_{2}$ are connected in
series, the overall impulse response is

```math
h_{\mathrm{series}}=h_{1}\ast h_{2}.
```

Reason:

```math
y=(x\ast h_{1})\ast h_{2}
=
x\ast(h_{1}\ast h_{2}).
```

### Parallel

If two LTI systems with impulse responses $h_{1}$ and $h_{2}$ are connected in
parallel and their outputs are added, the overall impulse response is

```math
h_{\mathrm{parallel}}=h_{1}+h_{2}.
```

Reason:

```math
y=x\ast h_{1}+x\ast h_{2}
=
x\ast(h_{1}+h_{2}).
```

### Direct Path

A direct wire from input to output is equivalent to an impulse response
$\delta$ because

```math
x\ast\delta=x.
```

So when simplifying block diagrams, a direct pass-through branch contributes
$\delta(t)$ to the overall impulse response.

---

## 7. Example Pattern: Simplifying an LTI Block Diagram

Suppose the input $x$ splits into three parallel branches:

- a direct path;
- a system with impulse response $h_{1}$;
- a system with impulse response $h_{2}$.

The branch outputs are added to form $v$, and then $v$ passes through another
LTI system with impulse response $h_{3}$.

The parallel part has impulse response

```math
h_{\mathrm{left}}=\delta+h_{1}+h_{2}.
```

Then the series connection with $h_{3}$ gives

```math
h_{\mathrm{overall}}
=
(\delta+h_{1}+h_{2})\ast h_{3}.
```

Using distributivity and the identity property,

```math
h_{\mathrm{overall}}
=
h_{3}+h_{1}\ast h_{3}+h_{2}\ast h_{3}.
```

### Route for Block Diagram Problems

1. Replace each LTI block by its impulse response.
2. Replace each direct wire by $\delta$.
3. Combine parallel branches by addition.
4. Combine cascade branches by convolution.
5. Use convolution identity, associativity, commutativity, and distributivity
   to simplify.

---

## 8. LTI Memory Test Using $h(t)$

For an LTI system, memorylessness can be tested directly from the impulse
response.

An LTI system is memoryless if and only if

```math
h(t)=0
\quad \mathrm{for\ all} \quad
t\ne 0.
```

Equivalently, the impulse response must have the form

```math
h(t)=K\delta(t),
```

where $K$ is a complex constant.

Then

```math
y=x\ast(K\delta)=Kx.
```

So every memoryless LTI system is just an ideal amplifier.

### Examples

If

```math
h(t)=e^{-at}u(t),
```

then the system is not memoryless, because $h(t)$ is generally nonzero for
$t>0$.

If

```math
h(t)=\delta(t),
```

then the system is memoryless, because the impulse response is concentrated at
$t=0$.

---

## 9. LTI Causality Test Using $h(t)$

For an LTI system, causality can also be tested directly from the impulse
response.

An LTI system is causal if and only if

```math
h(t)=0
\quad \mathrm{for\ all} \quad
t<0.
```

In other words, the impulse response itself must be a causal function.

### Examples

If

```math
h(t)=e^{-at}u(t),
```

then the system is causal, because $u(t)$ forces $h(t)=0$ for $t<0$.

If

```math
h(t)=\delta(t+t_{0}),
\qquad
t_{0}>0,
```

then the impulse occurs at $t=-t_{0}<0$. Therefore, the system is not causal.

### Intuition

For an LTI system, the output is built by shifting and weighting copies of
$h(t)$. If $h(t)$ reaches into negative time, the system response depends on
future input values, so the system is noncausal.

---

## 10. Common Checks for This Week

You should be able to:

- define the impulse response $h$ of a system;
- explain why $y=x\ast h$ for an LTI system;
- derive the integrator example from $h(t)=u(t)$;
- connect step response and impulse response using differentiation;
- simplify LTI block diagrams using convolution and addition;
- treat a direct path as $\delta(t)$;
- test memorylessness of an LTI system from $h(t)$;
- test causality of an LTI system from $h(t)$.

---

## Key Takeaway

For general CT systems, properties are usually tested from the system equation.
For LTI systems, many important properties can be tested directly from the
impulse response. This is why $h(t)$ becomes one of the central objects in the
rest of the course.
