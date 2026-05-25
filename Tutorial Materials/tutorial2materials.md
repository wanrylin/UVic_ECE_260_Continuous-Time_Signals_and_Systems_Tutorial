# ECE 260 Tutorial 2 Materials

Assignment 2: Preliminaries and Continuous-Time Signals and Systems

This file is the classroom-facing tutorial material. It starts with a compact
recap of the core CT signal and system ideas, followed by selected worked
questions and MATLAB demo code.

---

## Quick Recap

### 1. Signals, Functions, and System Operators

- A signal $x$ is a whole function; $x(t)$ is one value of that function.
- A system operator $\mathcal{H}$ maps a function to a function:
```math
  y=\mathcal{H}x.
```

- Use $(\mathcal{H}x)(t)$ when you mean "apply the system first, then evaluate
  at time $t$."
- In cascaded systems, the rightmost operator acts first.

### 2. Time and Amplitude Transformations

- $x(t-b)$ shifts the signal right by $b$.
- $x(at)$ compresses the signal if $|a|>1$ and stretches it if $0<|a|<1$.
- $x(-t)$ reflects the signal in time.
- $Ax(t)+C$ scales and shifts the signal vertically.
- For graphing, transform breakpoints by solving the new argument equal to each
  old breakpoint.

### 3. Periodicity and Symmetry

- A signal is periodic if $x(t+T)=x(t)$ for some $T>0$ and all $t$.
- For $\cos(\omega t)$, $\sin(\omega t)$, and $e^{j\omega t}$:
```math
  T=\frac{2\pi}{|\omega|}.
```

- A sum of periodic signals is periodic only when the periods have rational
  ratios.
- Even: $x(-t)=x(t)$. Odd: $x(-t)=-x(t)$.

### 4. Unit Step and Delta Function

- A unit-step window on $[a,b)$ is
```math
  u(t-a)-u(t-b).
```

- Use these windows to collapse piecewise functions into one expression.
- The delta function samples an integrand at the impulse location:
```math
  \int_{-\infty}^{\infty}f(t)\delta(t-t_{0})\,dt=f(t_{0}).
```

- Remember the scaling rule:
```math
  \delta(at-b)=\frac{1}{|a|}\delta\left(t-\frac{b}{a}\right).
```

### 5. CT System Properties

- Memoryless: output at $t_{0}$ depends only on input at $t_{0}$.
- Causal: output at $t_{0}$ depends only on input values for $t\le t_{0}$.
- Invertible: different inputs always produce different outputs.
- BIBO stable: every bounded input produces a bounded output.
- Time invariant: shifting the input shifts the output by the same amount.
- Linear: $\mathcal{H}(a_{1}x_{1}+a_{2}x_{2})=a_{1}\mathcal{H}(x_{1})+a_{2}\mathcal{H}(x_{2})$.
- Eigenfunction: $\mathcal{H}x=\lambda x$, where $\lambda$ is a constant.

### 6. MATLAB Basics

- Use element-wise operators for vector or matrix inputs:
  `.*`, `./`, and `.^`.
- Logical expressions such as `t >= 0` can be used as masks.
- A MATLAB identifier must start with a letter and can contain letters, digits,
  and underscores.

---

## Questions

## Q1. Exercise 2.1(b): Operator Notation

### Problem

Let each of $\mathcal{G}$ and $\mathcal{H}$ denote a system operator that maps a
function to a function; let $x$ and $y$ denote functions; and assume that all
other variables denote numbers. Fully parenthesize the expression below in order
to show the implied grouping of all operations:
```math
\mathcal{G}\mathcal{H}y(t).
```

### Big Idea

System operators act on whole functions. Evaluation at $t$ happens after the
operators have acted.

### Knowledge Needed

- $\mathcal{H}y$ means apply $\mathcal{H}$ to the whole function $y$.
- $\mathcal{G}\mathcal{H}y$ means apply $\mathcal{H}$ first, then
  $\mathcal{G}$.
- $(\cdot)(t)$ means evaluate the final function at time $t$.

### Solution

The rightmost operator acts first:
```math
y \xrightarrow{\mathcal{H}} \mathcal{H}y
\xrightarrow{\mathcal{G}} \mathcal{G}(\mathcal{H}y).
```

Then evaluate the resulting function at $t$:
```math
\boxed{(\mathcal{G}(\mathcal{H}y))(t)}.
```

### Common Mistake

Do not read this as $\mathcal{G}(\mathcal{H}(y(t)))$. The expression $y(t)$ is a
number, but $\mathcal{H}$ expects a function.

---

## Q2. Exercise 2.2(d): Strict Mathematical Notation

### Problem

Let $\mathcal{H}$ denote a system operator that maps a function to a function;
let $x$ and $y$ denote functions; and let all other variables denote numbers.
Using strictly-correct mathematical notation, write an expression for:

the output of the system $\mathcal{H}$ evaluated at $5t$ when the input to the
system is $x+y$.

### Big Idea

First identify the input function. Then apply the system. Then evaluate the
output at the requested time.

### Knowledge Needed

The output of $\mathcal{H}$ for input $x+y$ is
```math
\mathcal{H}(x+y).
```

Evaluating this output at $5t$ gives
```math
[\mathcal{H}(x+y)](5t).
```

### Solution

Input:
```math
x+y.
```

Output function:
```math
\mathcal{H}(x+y).
```

Output value at $5t$:
```math
\boxed{(\mathcal{H}(x+y))(5t)}.
```

---

## Q3. Exercise 3.1(e): Time and Amplitude Transformations

### Problem

Identify the independent- and dependent-variable transformations that must be
applied to the function $x$ in order to obtain the function $y$ below. Choose
the transformations such that time shifting precedes time scaling and amplitude
scaling precedes amplitude shifting.
```math
y(t)=-3x(2[t-1])-1.
```

### Big Idea

Separate transformations inside $x(\cdot)$ from transformations outside
$x(\cdot)$.

### Knowledge Needed

- Inside $x(\cdot)$: time-axis transformations.
- Outside $x(\cdot)$: amplitude transformations.
- To describe "shift first, scale second," write the argument as
  $a(t-b)$ or as $at-b$ and identify the equivalent first shift.

### Solution

The argument of $x$ is
```math
2[t-1]=2t-2.
```

To describe the time operations with shifting first:

1. Shift $x(t)$ right by 2:
```math
   v(t)=x(t-2).
```

2. Time scale by 2:
```math
   v(2t)=x(2t-2)=x(2[t-1]).
```

Then apply the amplitude transformations:

3. Amplitude scale by $-3$:
```math
   -3x(2[t-1]).
```

4. Shift vertically down by 1:
```math
   -3x(2[t-1])-1.
```

### Final Result

To obtain $y$ from $x$:
```math
\boxed{
\text{shift right by }2,\ 
\text{compress in time by }2,\ 
\text{scale amplitude by }-3,\ 
\text{shift down by }1.}
```

The negative amplitude scale means a vertical reflection plus a factor of 3.

---

## Q4. Exercise 3.2(b): Find $y$ in Terms of $x$

### Problem

For the pair of functions $x$ and $y$ shown in Exercise 3.2(b), find $y$ in
terms of $x$. The expression for $y$ should have a minimal number of terms.

In this subproblem, $x(t)$ is the unit-height rectangular pulse supported on
approximately $[-1,1]$, and $y(t)$ is the plotted staircase-like signal.

### Big Idea

Use shifted and scaled copies of the rectangular pulse $x$ to build the
staircase signal.

### Knowledge Needed

If $x(t)=1$ on $[-1,1]$ and zero otherwise, then:
```math
x(t-a)
```

is a width-2 pulse centered at $a$, and
```math
x(bt+c)
```

can create shifted and scaled pulses.

### Solution

From the graph:

- $y(t)=-1$ on approximately $[-4,0]$;
- $y(t)=1$ on approximately $[0,1]$;
- $y(t)=2$ on approximately $[1,2]$;
- $y(t)=1$ on approximately $[2,3]$;
- $y(t)=-1$ on approximately $[3,4]$;
- $y(t)=0$ elsewhere.

Build each part using copies of $x$:

1. A negative wide pulse on $[-4,0]$:
```math
   -x\left(\frac{t+2}{2}\right).
```

2. Two overlapping positive pulses:
```math
   x(t-1)+x(t-2).
```

   These give height 1 on $[0,1]$, height 2 on $[1,2]$, and height 1 on
   $[2,3]$.

3. A negative width-1 pulse on $[3,4]$:
```math
   -x(2t-7).
```

### Final Result
```math
\boxed{
y(t)
=
-x\left(\frac{t+2}{2}\right)
+x(t-1)
+x(t-2)
-x(2t-7).}
```

Boundary values at jump discontinuities depend on plotting convention and are
not the main point of the problem.

---

## Q5. Exercise 3.4(d): Sketch a Transformed Signal

### Problem

Given the function $x$ shown in Exercise 3.4, plot and label:
```math
x(2t+1).
```

From the graph, $x$ can be modeled as
```math
x(t)=
\begin{cases}
2, & -2\le t<0,\\
t-2, & 0\le t\le2,\\
0, & \text{otherwise}.
\end{cases}
```

### Big Idea

Do not guess the new graph visually. Transform the breakpoints.

### Knowledge Needed

If the transformed signal is $x(s(t))$, then each old breakpoint $s_{0}$ moves to
a new time $t$ found from
```math
s(t)=s_{0}.
```

### Solution

Here
```math
s(t)=2t+1.
```

The first active interval of $x$ is $-2\le s<0$:
```math
-2\le 2t+1<0.
```

Subtract 1 and divide by 2:
```math
-3\le2t<-1
\quad\Rightarrow\quad
-\frac32\le t<-\frac12.
```

On this interval, the value is still 2.

The second active interval of $x$ is $0\le s\le2$:
```math
0\le2t+1\le2.
```

Thus
```math
-1\le2t\le1
\quad\Rightarrow\quad
-\frac12\le t\le\frac12.
```

On this interval,
```math
x(s)=s-2=(2t+1)-2=2t-1.
```

### Final Result
```math
\boxed{
x(2t+1)=
\begin{cases}
2, & -\frac32\le t<-\frac12,\\
2t-1, & -\frac12\le t\le\frac12,\\
0, & \text{otherwise}.
\end{cases}}
```

---

## Q6. Exercise 3.6(d): Periodicity

### Problem

Determine whether the function $x$ below is periodic, and if it is, find its
fundamental period:
```math
x(t)=1+\cos(2t)+e^{j5t}.
```

### Big Idea

The constant term does not affect periodicity. Check whether the nonconstant
components have a common period.

### Knowledge Needed

For
```math
\cos(\omega t),\qquad e^{j\omega t},
```

the period is
```math
T=\frac{2\pi}{|\omega|}.
```

The sum of periodic signals is periodic only if the individual periods have a
rational ratio.

### Solution

For $\cos(2t)$:
```math
T_{1}=\frac{2\pi}{2}=\pi.
```

For $e^{j5t}$:
```math
T_{2}=\frac{2\pi}{5}.
```

The ratio is
```math
\frac{T_{1}}{T_{2}}
=
\frac{\pi}{2\pi/5}
=\frac52,
```

which is rational. Therefore the signal is periodic.

Find the smallest common period:
```math
T=m\pi=n\frac{2\pi}{5}.
```

This requires
```math
5m=2n.
```

The smallest positive solution is $m=2$, $n=5$, so
```math
T_{0}=2\pi.
```

### Final Result
```math
\boxed{x(t)\text{ is periodic with fundamental period }T_{0}=2\pi.}
```

---

## Q7. Exercise 3.9(b): Even/Odd Symmetry

### Problem

Determine whether the function below is even, odd, or neither even nor odd:
```math
x(t)=t^3|t|.
```

### Big Idea

Compute $x(-t)$ and compare with $x(t)$ and $-x(t)$.

### Knowledge Needed

- $x$ is even if $x(-t)=x(t)$.
- $x$ is odd if $x(-t)=-x(t)$.
- $|t|$ is even.

### Solution

Compute:
```math
x(-t)=(-t)^3|-t|.
```

Since $|-t|=|t|$,
```math
x(-t)=-t^3|t|.
```

But
```math
x(t)=t^3|t|,
```

so
```math
x(-t)=-x(t).
```

### Final Result
```math
\boxed{x(t)=t^3|t|\text{ is odd}.}
```

---

## Q8. Exercise 3.10(c): Symmetry of Sums

### Problem

Prove the assertion:

The sum of an even function and an odd function, where neither function is
identically zero, is neither even nor odd.

### Big Idea

Use contradiction or direct comparison with the definitions of even and odd.

### Knowledge Needed

If $e$ is even,
```math
e(-t)=e(t).
```

If $o$ is odd,
```math
o(-t)=-o(t).
```

### Solution

Let
```math
z(t)=e(t)+o(t),
```

where $e$ is even, $o$ is odd, and neither is identically zero.

Then
```math
z(-t)=e(-t)+o(-t)=e(t)-o(t).
```

If $z$ were even, then $z(-t)=z(t)$, so
```math
e(t)-o(t)=e(t)+o(t).
```

Therefore
```math
o(t)=0
```

for all $t$, contradicting the assumption that $o$ is not identically zero.

If $z$ were odd, then $z(-t)=-z(t)$, so
```math
e(t)-o(t)=-e(t)-o(t).
```

Therefore
```math
e(t)=0
```

for all $t$, contradicting the assumption that $e$ is not identically zero.

### Final Result
```math
\boxed{e(t)+o(t)\text{ is neither even nor odd}.}
```

---

## Q9. Exercise 3.17(b): Reconstruct a Signal from Properties

### Problem

For the function $x$ having the properties stated below, find $x(t)$ for all
$t$:

- $x(t)=t-1$ for $0\le t\le1$;
- the function $v$ is causal, where $v(t)=x(t-1)$; and
- the function $w$ is odd, where $w(t)=x(t)+1$.

### Big Idea

Convert each verbal property into an equation or a zero region. Then combine
the constraints.

### Knowledge Needed

A causal signal is zero before the origin:
```math
v(t)=0 \quad \text{for } t<0.
```

An odd signal satisfies
```math
w(-t)=-w(t).
```

### Solution

Since $v(t)=x(t-1)$ is causal,
```math
x(t-1)=0
\quad \text{for } t<0.
```

Let
```math
s=t-1.
```

Then $t<0$ means $s<-1$, so
```math
x(s)=0 \quad \text{for } s<-1.
```

Thus
```math
x(t)=0 \quad \text{for } t<-1.
```

Since $w(t)=x(t)+1$ is odd,
```math
w(-t)=-w(t).
```

Substitute $w(t)=x(t)+1$:
```math
x(-t)+1=-(x(t)+1).
```

Therefore
```math
x(-t)=-x(t)-2.
```

The given middle piece is
```math
x(t)=t-1,\qquad 0\le t\le1.
```

Use the oddness of $w$ to reflect it to $-1\le t\le0$. The result is
```math
x(t)=t-1,\qquad -1\le t\le0.
```

So
```math
x(t)=t-1,\qquad -1\le t\le1.
```

For $t>1$, we have $-t<-1$, so $x(-t)=0$. Then
```math
0=-x(t)-2,
```

which gives
```math
x(t)=-2,\qquad t>1.
```

### Final Result
```math
\boxed{
x(t)=
\begin{cases}
0, & t<-1,\\
t-1, & -1\le t\le1,\\
-2, & t>1.
\end{cases}}
```

Quick check:
```math
w(t)=x(t)+1
```

is odd, and
```math
v(t)=x(t-1)
```

is zero for $t<0$.

---

## Q10. Exercise 3.20(a): Delta Function

### Problem

Fully simplify:
```math
\int_{-\infty}^{\infty}
\sin\left(2t+\frac{\pi}{4}\right)\delta(t)\,dt.
```

### Big Idea

The delta function samples the rest of the integrand at the impulse location.

### Knowledge Needed

Sifting property:
```math
\int_{-\infty}^{\infty}f(t)\delta(t-t_{0})\,dt=f(t_{0}).
```

Here
```math
\delta(t)=\delta(t-0),
```

so the impulse location is $t=0$.

### Solution

Apply the sifting property:
```math
\int_{-\infty}^{\infty}
\sin\left(2t+\frac{\pi}{4}\right)\delta(t)\,dt
=
\sin\left(2(0)+\frac{\pi}{4}\right).
```

Therefore
```math
\sin\left(\frac{\pi}{4}\right)=\frac{\sqrt2}{2}.
```

### Final Result
```math
\boxed{\frac{\sqrt2}{2}}.
```

---

## Q11. MATLAB D.1(a-e): Valid Identifiers

### Problem

Indicate whether each of the following is a valid MATLAB identifier
(variable/function name):
```matlab
(a) 4ever
(b) $rich$
(c) foobar
(d) foo_bar
(e) _foobar
```

### Big Idea

MATLAB identifiers have syntax rules. This is not about whether the name is a
good name, only whether MATLAB accepts it.

### Knowledge Needed

A MATLAB identifier:

- must start with a letter;
- may contain letters, digits, and underscores after the first character;
- cannot contain symbols such as `$`;
- cannot start with a digit or underscore.

### Solution

| Part | Identifier | Valid? | Reason |
|---|---|---|---|
| (a) | `4ever` | No | starts with a digit |
| (b) | `$rich$` | No | contains `$` and does not start with a letter |
| (c) | `foobar` | Yes | letters only |
| (d) | `foo_bar` | Yes | underscore is allowed after the first character |
| (e) | `_foobar` | No | starts with underscore |

---

## Q12. MATLAB D.2(a-d): Vectorized Expressions

### Problem

Consider the vector
```matlab
v = [0 1 2 3 4 5]
```

Write an expression in terms of `v` that yields a new vector of the same
dimensions as `v`, where each element $t$ of the original vector has been
replaced by the quantity below:
```matlab
(a) 2t - 3
(b) 1/(t + 1)
(c) t^5 - 3
(d) |t| + t^4
```

### Big Idea

When a formula should apply to each element of a vector, use element-wise
operators.

### Knowledge Needed

- `.^` means element-wise power.
- `./` means element-wise division.
- `abs(v)` gives element-wise absolute value.

### Solution
```matlab
v = [0 1 2 3 4 5];

a = 2*v - 3;
b = 1./(v + 1);
c = v.^5 - 3;
d = abs(v) + v.^4;

disp(a)
disp(b)
disp(c)
disp(d)
```

### Results
```matlab
a =
    -3    -1     1     3     5     7

b =
    1.0000    0.5000    0.3333    0.2500    0.2000    0.1667

c =
    -3    -2    29   240  1021  3122

d =
     0     2    18    84   260   630
```

---

## Q13. Exercise 3.22(a): Unit-Step Representation

### Problem

For the function $x$ given below, find a single expression for $x$, i.e., an
expression that does not involve multiple cases. Group similar unit-step
function terms together.
```math
x(t)=
\begin{cases}
-t-3, & -3\le t<-2,\\
-1, & -2\le t<-1,\\
t^3, & -1\le t<1,\\
1, & 1\le t<2,\\
-t+3, & 2\le t<3,\\
0, & \text{otherwise}.
\end{cases}
```

### Big Idea

Write one window for each active interval, then collect common unit-step terms.

### Knowledge Needed

A window on $[a,b)$ is
```math
u(t-a)-u(t-b).
```

### Solution

Start with interval windows:
```math
\begin{aligned}
x(t)=&
(-t-3)[u(t+3)-u(t+2)]\\
&- [u(t+2)-u(t+1)]\\
&+t^3[u(t+1)-u(t-1)]\\
&+[u(t-1)-u(t-2)]\\
&+(-t+3)[u(t-2)-u(t-3)].
\end{aligned}
```

Now collect coefficients for each unit-step term:
```math
\boxed{
\begin{aligned}
x(t)=&
(-t-3)u(t+3)
+(t+2)u(t+2)\\
&+(t^3+1)u(t+1)
+(1-t^3)u(t-1)\\
&+(2-t)u(t-2)
+(t-3)u(t-3).
\end{aligned}}
```

### Check

Pick one interval, for example $-2\le t<-1$. The active terms are
$u(t+3)$ and $u(t+2)$:
```math
(-t-3)+(t+2)=-1,
```

which matches the original piece.

---

## Q14. Exercise 3.24(e): Memoryless System

### Problem

Determine whether the system $\mathcal{H}$ below is memoryless:
```math
(\mathcal{H}x)(t)
=
\int_{-\infty}^{\infty}x(\tau)\delta(\tau)\,d\tau.
```

### Big Idea

First simplify the system. Then ask whether the output at time $t$ depends only
on $x(t)$.

### Knowledge Needed

Sifting:
```math
\int_{-\infty}^{\infty}x(\tau)\delta(\tau)\,d\tau=x(0).
```

### Solution

The system output is
```math
(\mathcal{H}x)(t)=x(0).
```

This output is the same for every $t$, but it depends on the input at time
$0$.

For $t\ne0$, the output at time $t$ depends on $x(0)$, not only on $x(t)$.

### Final Result
```math
\boxed{\mathcal{H}\text{ has memory}.}
```

---

## Q15. Exercise 3.25(d): Causality

### Problem

Determine whether the system $\mathcal{H}$ below is causal:
```math
(\mathcal{H}x)(t)=\int_{t}^{\infty} x(\tau)\,d\tau.
```

### Big Idea

At time $t_{0}$, check whether the formula needs any input value after $t_{0}$.

### Knowledge Needed

A system is causal if $(\mathcal{H}x)(t_{0})$ depends only on $x(\tau)$ for
$\tau\le t_{0}$.

### Solution

At time $t_{0}$,
```math
(\mathcal{H}x)(t_{0})=\int_{t_{0}}^{\infty}x(\tau)\,d\tau.
```

This integral uses $x(\tau)$ for $\tau>t_{0}$, which are future input values.

### Final Result
```math
\boxed{\mathcal{H}\text{ is not causal}.}
```

---

## Q16. Exercise 3.26(c): Invertibility

### Problem

Determine whether the system $\mathcal{H}$ below is invertible, and if it is,
specify its inverse:
```math
(\mathcal{H}x)(t)
=
\mathrm{Even}(x)(t)-\mathrm{Odd}(x)(t).
```

### Big Idea

Use the formulas for even and odd parts. This system has a simpler hidden form.

### Knowledge Needed
```math
\mathrm{Even}(x)(t)=\frac12[x(t)+x(-t)],
```
```math
\mathrm{Odd}(x)(t)=\frac12[x(t)-x(-t)].
```

### Solution

Compute:
```math
\begin{aligned}
(\mathcal{H}x)(t)
&=
\frac12[x(t)+x(-t)]
-\frac12[x(t)-x(-t)]\\
&=
x(-t).
\end{aligned}
```

So $\mathcal{H}$ is simply time reversal.

To undo it, time-reverse again:
```math
y(t)=x(-t)
\quad\Rightarrow\quad
y(-t)=x(t).
```

### Final Result
```math
\boxed{\mathcal{H}\text{ is invertible},\qquad
(\mathcal{H}^{-1}y)(t)=y(-t).}
```

---

## Q17. Exercise 3.27(b): BIBO Stability

### Problem

Determine whether the system $\mathcal{H}$ below is BIBO stable:
```math
(\mathcal{H}x)(t)=\frac12x^2(t)+x(t).
```

### Big Idea

Assume the input is bounded. Then show the output is also bounded.

### Knowledge Needed

BIBO stability means:

if
```math
|x(t)|\le A<\infty
```

for all $t$, then there must be some finite $B$ such that
```math
|(\mathcal{H}x)(t)|\le B
```

for all $t$.

### Solution

Assume
```math
|x(t)|\le A.
```

Then
```math
\begin{aligned}
|(\mathcal{H}x)(t)|
&=
\left|\frac12x^2(t)+x(t)\right|\\
&\le
\frac12|x(t)|^2+|x(t)|\\
&\le
\frac12A^2+A.
\end{aligned}
```

This is finite.

### Final Result
```math
\boxed{\mathcal{H}\text{ is BIBO stable}.}
```

---

## Q18. Exercise 3.28(c): Time Invariance

### Problem

Determine whether the system $\mathcal{H}$ below is time invariant:
```math
(\mathcal{H}x)(t)
=
\int_{t}^{t+1}x(\tau-\alpha)\,d\tau,
```

where $\alpha$ is a constant.

### Big Idea

Compare two paths:

1. shift input first, then apply the system;
2. apply the system first, then shift the output.

### Knowledge Needed

Let the shifted input be
```math
x_{s}(t)=x(t-t_{0}).
```

The system is time invariant if
```math
\mathcal{H}(x_{s})=S_{t_{0}}(\mathcal{H}x).
```

### Solution

Shift input first:
```math
\begin{aligned}
(\mathcal{H}x_{s})(t)
&=
\int_{t}^{t+1}x_{s}(\tau-\alpha)\,d\tau\\
&=
\int_{t}^{t+1}x(\tau-\alpha-t_{0})\,d\tau.
\end{aligned}
```

System first, then shift output:
```math
(\mathcal{H}x)(t-t_{0})
=
\int_{t-t_{0}}^{t-t_{0}+1}x(\tau-\alpha)\,d\tau.
```

Use the change of variable
```math
\nu=\tau+t_{0},
\qquad
\tau=\nu-t_{0}.
```

Then the limits become $t$ to $t+1$, and
```math
(\mathcal{H}x)(t-t_{0})
=
\int_{t}^{t+1}x(\nu-t_{0}-\alpha)\,d\nu.
```

This matches the shift-input-first expression.

### Final Result
```math
\boxed{\mathcal{H}\text{ is time invariant}.}
```

---

## Q19. Exercise 3.29(b): Linearity

### Problem

Determine whether the system $\mathcal{H}$ below is linear:
```math
(\mathcal{H}x)(t)=e^{x(t)}.
```

### Big Idea

A quick test for linearity: a linear system must send the zero input to the zero
output.

### Knowledge Needed

If $\mathcal{H}$ is linear, then
```math
\mathcal{H}0=0.
```

### Solution

Let
```math
x(t)=0.
```

Then
```math
(\mathcal{H}x)(t)=e^{0}=1.
```

The zero input produces the constant-one output, not the zero output.

### Final Result
```math
\boxed{\mathcal{H}\text{ is not linear}.}
```

---

## Q20. Exercise 3.33(a): Eigenfunctions

### Problem

For the system $\mathcal{H}$ and the functions $\{x_{k}\}$ below, determine if
each $x_{k}$ is an eigenfunction of $\mathcal{H}$, and if it is, state the
corresponding eigenvalue:
```math
(\mathcal{H}x)(t)=x^2(t),
```
```math
x_{1}(t)=a,\qquad
x_{2}(t)=e^{-at},\qquad
x_{3}(t)=\cos t,
```

where $a$ is a complex constant.

### Big Idea

An eigenfunction must come back as a constant multiple of itself:
```math
\mathcal{H}x=\lambda x.
```

The multiplier $\lambda$ must not depend on $t$.

### Solution

### For $x_{1}(t)=a$
```math
(\mathcal{H}x_{1})(t)=a^2.
```

If $a\ne0$,
```math
a^2=a\cdot a=\lambda x_{1}(t)
```

with
```math
\lambda=a.
```

So $x_{1}$ is an eigenfunction for $a\ne0$ with eigenvalue $a$.

If $a=0$, this is the zero function; depending on convention, the zero function
is usually excluded from being called an eigenfunction.

### For $x_{2}(t)=e^{-at}$
```math
(\mathcal{H}x_{2})(t)=\left(e^{-at}\right)^2=e^{-2at}.
```

Compare with
```math
\lambda x_{2}(t)=\lambda e^{-at}.
```

This would require
```math
\lambda=e^{-at},
```

which depends on $t$ unless $a=0$.

For generic $a\ne0$, $x_{2}$ is not an eigenfunction. If $a=0$, then $x_{2}(t)=1$
and it is an eigenfunction with eigenvalue $1$.

### For $x_{3}(t)=\cos t$
```math
(\mathcal{H}x_{3})(t)=\cos^2 t.
```

This is not a constant multiple of $\cos t$ for all $t$.

### Final Result

For generic $a\ne0$:
```math
\boxed{
x_{1} \text{ is an eigenfunction with }\lambda=a,\quad
x_{2} \text{ is not},\quad
x_{3} \text{ is not}.}
```

---

## Q21. MATLAB D.3: Temperature Conversion Table

### Problem

Let $T_{C}$, $T_{F}$, and $T_{K}$ denote the temperature measured in units of Celsius,
Fahrenheit, and Kelvin, respectively. These quantities are related by
```math
T_{F}=\frac{9}{5}T_{C}+32,
\qquad
T_{K}=T_{C}+273.15.
```

Write a program that generates a temperature conversion table. The first column
should contain Celsius values from $-50$ to $50$ in steps of $10$. The second
and third columns should contain the corresponding Fahrenheit and Kelvin values.

### Classroom Demo Code
```matlab
% D3_temperature_table.m
% Generate a Celsius/Fahrenheit/Kelvin conversion table.

Tc_values = -50:10:50;
tableData = zeros(numel(Tc_values), 3);

for k = 1:numel(Tc_values)
    Tc = Tc_values(k);
    Tf = (9/5)*Tc + 32;
    Tk = Tc + 273.15;

    tableData(k, :) = [Tc, Tf, Tk];
end

fprintf('   Celsius   Fahrenheit      Kelvin\n');
fprintf('------------------------------------\n');

for k = 1:size(tableData, 1)
    fprintf('%10.2f %12.2f %11.2f\n', ...
        tableData(k, 1), tableData(k, 2), tableData(k, 3));
end
```

### More MATLAB-Style Version
```matlab
Tc = (-50:10:50).';
Tf = (9/5)*Tc + 32;
Tk = Tc + 273.15;

T = table(Tc, Tf, Tk, ...
    'VariableNames', {'Celsius', 'Fahrenheit', 'Kelvin'});

disp(T)
```

---

## Q22. MATLAB D.4(a-c): Unit-Step Function

### Problem

(a) Write a function called `unitstep` that takes a single real argument $t$ and
returns $u(t)$, where
```math
u(t)=
\begin{cases}
1, & t\ge0,\\
0, & \text{otherwise}.
\end{cases}
```

(b) Modify the function from part (a) so that it takes a single vector argument
$t=[t_{1},t_{2},\dots,t_{n}]^T$ and returns
```math
[u(t_{1}),u(t_{2}),\dots,u(t_{n})]^T.
```

The solution must employ a looping construct.

(c) Find a solution using only two lines of code, without a loop.

### D.4(a): Scalar Version
```matlab
function y = unitstep_scalar(t)
%UNITSTEP_SCALAR Unit-step function for scalar input.

if t >= 0
    y = 1;
else
    y = 0;
end

end
```

### D.4(b): Vector Version with Loop
```matlab
function y = unitstep_loop(t)
%UNITSTEP_LOOP Unit-step function for vector input using a loop.

y = zeros(size(t));

for k = 1:numel(t)
    if t(k) >= 0
        y(k) = 1;
    else
        y(k) = 0;
    end
end

end
```

### D.4(c): Vectorized Version
```matlab
function y = unitstep_vec(t)
%UNITSTEP_VEC Vectorized unit-step function.

y = double(t >= 0);

end
```

### Demo Script
```matlab
t = [-2 -1 0 1 2];

unitstep_scalar(0)
unitstep_loop(t)
unitstep_vec(t)
```

---

## Q23. MATLAB Exercise 3.201(a): Element-Wise Function

### Problem

Write a MATLAB function that takes an $m\times n$ matrix $t$ and returns a matrix
$x$ of the same dimensions where $x_{i,j}=f(t_{i,j})$. The function is not
permitted to use conditional statements or loops.

For part (a):
```math
f(t)=
\left(\frac{t^2-1}{t^2+1}\right)e^{-|t|/10}
\cos\left(\frac{t}{2\pi}\right).
```

The cosine term is multiplied by the preceding factors.
```matlab
function x = f201a(t)
%F201A Element-wise implementation of Exercise 3.201(a).

x = ((t.^2 - 1)./(t.^2 + 1)) .* exp(-abs(t)./10) ...
    .* cos(t./(2*pi));

end
```

### Teaching Point

The important MATLAB idea is not the exact constants. It is that powers,
division, and multiplication between arrays must be element-wise:
```matlab
.^
./
.*
```

---

## Q24. MATLAB Exercise 3.201(f): Element-Wise Piecewise Function

### Problem

Write a MATLAB function that takes an $m\times n$ matrix $t$ and returns a matrix
$x$ of the same dimensions where $x_{i,j}=f(t_{i,j})$. The function is not
permitted to use conditional statements or loops.

For part (f):
```math
f(t)=
\begin{cases}
e^t, & t<0,\\
1, & 0\le t<1,\\
e^{1-t}, & t\ge1.
\end{cases}
```

### Big Idea

Use logical masks. In MATLAB, expressions like `t < 0` produce arrays of
logical values that can be used as 0/1 masks.

### Solution Code
```matlab
function x = f201f(t)
%F201F Element-wise implementation of Exercise 3.201(f).

x = exp(t).*(t < 0) ...
    + (t >= 0 & t < 1) ...
    + exp(1 - t).*(t >= 1);

end
```

### Demo Script
```matlab
t = [-2 -1 0 0.5 1 2;
     -3 -0.1 0.2 0.9 1.5 3];

x_f = f201f(t);
disp(x_f)
```
