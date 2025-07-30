# Chapter 01 Discrete Sequences and Systems

## 1.1

This problem gives us practice in thinking about 
sequences of numbers. For centuries mathematicians 
have developed clever ways of computing $π$.
In 1671 the Scottish mathematician James Gregory 
proposed the following very simple series for 
calculating $π$:

$$ 
π = 4 \cdot
\left\{ 
1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots
 \right\}
$$

Thinking of the terms inside the parentheses as a 
sequence indexed by the variable $n$, where
$n = 0, 1, 2, 3, . . ., 100$, write Gregory’s algorithm in the form

$$ 
π = 4 \cdot
\sum_{n = 0}^{100} (-1)^? ?
$$

replacing the “?” characters with expressions in 
terms of index $n$.

**Solution**:

$$ 
π = 4 \cdot
\sum_{n = 0}^{100} (-1)^n \frac{1}{2n+1}
$$

$\square$

## 1.2

One of the ways to obtain discrete sequences, for 
follow-on processing, is to digitize a continuous 
(analog) signal with an analog-to-digital (A/D) con-
verter. A 6-bit A/D converter’s output words (6-bit 
binary words) can only represent 26=64 different 
numbers. (We cover this digitization, sampling, and
A/D converters in detail in upcoming chapters.) Thus 
we say the A/D converter’s “digital” output can only 
represent a finite number of amplitude values. Can 
you think of a continuous time-domain electrical 
signal that only has a finite number of amplitude 
values? If so, draw a graph of that continuous-time 
signal.

**Solution**:
Maybe a electrical piano.

## 1.3

On the Internet, the author once encountered the following line of C-language code

```python
PI = 2 * asin(1.0)
```

whose purpose was to define the constant $π$. In 
standard mathematical notation, that line of code can be described by

$$ 
π = \sin ^{-1} (1.0)
$$

Under what assumption does the above expression 
correctly define the constant $π$?

**Solution**: The assumption should be we have 
infinite precision.

## 1.4

Many times in the literature of signal processing you 
will encounter the identity

$$ 
x^0 = 1
$$

That is, $x$ raised to the zero power is equal to 
one. Using the Laws of Exponents, prove the above 
expression to be true.

**Proof**:

$$ 
1 = x^1 x^{-1} = x^{1 + (-1)} = x^0
$$

$\square$

## 1.5

Recall that for discrete sequences the $t_s$ sample 
period (the time period between samples) is the 
reciprocal of the sample frequency $f_s$.
Write the equations, as we did in the text’s Eq. (1–3)
, describing time-domain sequences for
unity-amplitude cosine waves whose $f_o$ frequencies 
are

(a) $f_o = f_s / 2$, one-half the sample rate.

**Solution**:

$$ 
x(n) = \cos 2 \pi f_o n t_s \\
= \cos 2 \pi (f_s / 2) n (1 / f_s) \\
= \cos n \pi = (-1)^n
$$

$\square$

(b) $f_o = f_s / 4$, one-fourth the sample rate.

**Solution**:

$$ 
x(n) = \cos 2 \pi f_o n t_s \\
= \cos 2 \pi (f_s / 4) n (1 / f_s) \\
= \cos \frac{n}{2} \pi
$$

$\square$

(c) $f_o = 0$ (zero) Hz

**Solution**:

$$ 
x(n) = \cos 2 \pi f_o n t_s = \cos 0 = 1
$$

$\square$

## 1.6

Draw the three time-domain cosine wave sequences, 
where a sample value is represented by a dot, 
described in Problem 1.5. The correct solution to 
Part (a) of this problem is a useful sequence used to 
convert some lowpass digital filters into highpass 
filters. (Chapter 5 discusses that topic.) The 
correct solution to Part (b) of this problem is an 
important discrete sequence used for frequency
translation (both for signal down-conversion and 
up-conversion) in modern-day wireless communications 
systems. The correct solution to Part (c) of this
problem should convince us that it’s perfectly valid 
to describe a cosine sequence whose frequency is zero 
Hz.

**Solution**

```python
import numpy as np
import matplotlib.pyplot as plt

# 1.6.(a)

n = np.arange(10);
fs = 2.0
fo = fs / 2.0
ts = 1.0 / fs
x = np.cos(2 * np.pi * fo * n * ts)
plt.xlabel('n');
plt.ylabel('x[n]');
plt.title(r'Plot of DT signal $x[n] = \cos (2\pi 1.0 n \Delta t)$');
plt.stem(n, x);

# 1.6.(b)

n = np.arange(10);
fs = 2.0
fo = fs / 4.0
ts = 1.0 / fs
x = np.cos(2 * np.pi * fo * n * ts)
plt.xlabel('n');
plt.ylabel('x[n]');
plt.title(r'Plot of DT signal $x[n] = \cos (2\pi 0.5 n \Delta t)$');
plt.stem(n, x);

# 1.6.(c)

n = np.arange(10);
fs = 2.0
fo = 0
ts = 1.0 / fs
x = np.cos(2 * np.pi * fo * n * ts)
plt.xlabel('n');
plt.ylabel('x[n]');
plt.title(r'Plot of DT signal $x[n] = \cos (2\pi 0 n t_s)$');
plt.stem(n, x);
```

## 1.7

Draw the three time-domain sequences of 
unity-amplitude sinewaves (not cosine waves) whose 
frequencies are

(a) $f_o = f_s / 2$, one-half the sample rate.

(b) $f_o = f_s / 4$, one-fourth the sample rate.

(c) $f_o = 0$ (zero) Hz

The correct solutions to Parts (a) and (c) show us 
that the two frequencies, 0 Hz and fs/2 Hz, are 
special frequencies in the world of discrete signal 
processing. What is special about the sinewave 
sequences obtained from the above Parts (a) and (c)?

**Solution**:

```python
# 1.7.(a)

n = np.arange(10);
fs = 2.0
fo = fs / 2.0
ts = 1.0 / fs
x = np.sin(2 * np.pi * fo * n * ts)
plt.xlabel('n');
plt.ylabel('x[n]');
plt.title(r'Plot of DT signal $x[n] = \sin (2\pi 1.0 n 0.5)$');
plt.stem(n, x);
plt.ylim(-1, 1)

# 1.7.(b)

n = np.arange(10);
fs = 2.0
fo = fs / 4.0
ts = 1.0 / fs
x = np.sin(2 * np.pi * fo * n * ts)
plt.xlabel('n');
plt.ylabel('x[n]');
plt.title(r'Plot of DT signal $x[n] = \sin (2\pi 2.0 n 0.5)$');
plt.stem(n, x);

# 1.7.(c)

n = np.arange(10);
fs = 2.0
fo = 0
ts = 1.0 / fs
x = np.sin(2 * np.pi * fo * n * ts)
plt.xlabel('n');
plt.ylabel('x[n]');
plt.title(r'Plot of DT signal $x[n] = \sin (2\pi 0.0 n 0.5)$');
plt.stem(n, x);
```

Part (a) and (c) are special because they sampled
all 0.

## 1.8

Consider the infinite-length time-domain sequence
$x(n)$ in Figure P1–8. Draw the first eight samples of a shifted time sequence defined by

$$ 
x_{shift}(n) = x(n+1)
$$

```python
# 1.8

n = np.arange(7);
nz = np.arange(0, 7, 0.01);
fs = 4
fo = 1
ts = 1.0 / fs
x = -np.sin(2 * np.pi * fo * n * ts)
z = -np.sin(2 * np.pi * fo * nz * ts)

plt.xlabel('n');
plt.ylabel('$x_{shift}[n]$');
plt.title(r'Plot of DT signal $x[n] = \sin (2\pi 1.0 n 0.25)$');
plt.plot(n, x, 'o');
plt.plot(nz, z, '--');
plt.show()
```

## 1.9

Assume, during your reading of the literature of DSP, 
you encounter the process shown in Figure P1–9. The
$x(n)$ input sequence, whose $f_s$ sample rate
is 2500 Hz, is multiplied by a sinusoidal $m(n)$ 
sequence to produce the $y(n)$ output sequence. What 
is the frequency, measured in Hz, of the sinusoidal
$m(n)$ sequence?

**Solution**:

Assume

$$ 
m(n) = \sin (2 \pi f_o n t_s)
$$

Then we know

$$ 
2 \pi f_o n t_s = 0.8 \pi n \\
\Rightarrow \\
f_o = 0.4 f_s = 1000
$$

