# Chapter 02 Periodic Sampling

## 2.1

Suppose you have a mechanical clock that has a minute hand, but no hour
hand. Next, suppose you took a photograph of the clock when the minute
hand was pointed at 12:00 noon and then took additional photos every 55
minutes. Upon showing those photos, in time order, to someone:

(a) What would that person think about the direction of motion of the
minute hand as time advances?

**Solution**: He or she will think it is going counter-clock wise

(b) With the idea of lowpass sampling in mind, how often would you need to
take photos, measured in photos/hour, so that the successive photos
show proper (true) clockwise minute-hand rotation?

**Solution**: He or she just needs to take photos > photos/hour. Since we need to
have $f_s > 2 B$.

$\square$

## 2.2

Assume we sampled a continuous $x(t)$ signal and obtained 100 $x(n)$ time-
domain samples. What important information (parameter that we need to
know in order to analyze $x(t)$) is missing from the $x(n)$ sequence?

**Solution**: The frequency of $x(t)$ is missing.

$\square$

## 2.3

National Instruments Corporation produces an analog-to-digital (A/D) converter
(Model #NI-5154) that can sample (digitize) an analog signal at a sample rate of fs=2.0 GHz 
(gigahertz).

(a) What is the $t_s$ period of the output samples of such a device?

**Solution**: The $t_s = 500 \text{ ps}$.

(b) Each A/D output sample is an 8-bit binary word (one byte), and the converter is able to 
store 256 million samples. What is the maximum time interval over which the converter can continuously sample an analog signal?

**Solution**: It can sample $2 \times 10^9$ samples per second. Then it can only sample for

$$ 
\frac{256 \cdot 10^6}{2 \times 10^9} = 0.128 \text{ second}
$$

$\square$

## 2.4

Consider a continuous time-domain sinewave, whose cyclic frequency is 500 Hz, defined by

$$ 
x(t) = \cos [2 \pi (500) t + \pi / 7]
$$

Write the equation for the discrete $x(n)$ sinewave sequence that results from
sampling $x(t)$ at an $f_s$ sample rate of 4000 Hz.

**Solution**:

$f_o = 500, f_s = 4000$, so $t_s = 1/4000$.

Then

$$ 
x(n) = \cos [2 \pi \frac{n}{8} + \pi / 7]
$$

$\square$

## 2.5

If we sampled a single continuous sinewave whose frequency is $f_o$ Hz, over
what range must $t_s$ (the time between digital samples) be to satisfy the
Nyquist criterion? Express that $t_s$ range in terms of $f_o$.

**Solution**:

We need to have $f_s \geq 2 f_o$, i.e. $\frac{1}{t_s} \geq 2 f_o$. So

$$ 
t_s \leq \frac{1}{2 f_o}
$$

$\square$

## 2.6

Suppose we used the following statement to describe the Nyquist criterion
for lowpass sampling: “When sampling a single continuous sinusoid (a single
analog tone), we must obtain no fewer than $N$ discrete samples per continu-
ous sinewave cycle.” What is the value of this integer $N$?

**Solution** $N = 2$.

$\square$

## 2.7

The Nyquist criterion, regarding the sampling of lowpass signals, is sometimes stated as “The 
sampling rate fs must be equal to, or greater than, twice
the highest spectral component of the continuous signal being sampled.” Can
you think of how a continuous sinusoidal signal can be sampled in accordance
with that Nyquist criterion definition to yield all zero-valued discrete
samples?

**Solution**: Consider

$$ 
x(t) = \sin 2 \pi \frac{f_s}{2} t
$$

Then

$$ 
x(n) = \sin 2 \pi \frac{f_s}{2} n \frac{1}{f_s}
= \sin n \pi = 0
$$

$\square$

## 2.8

Stock market analysts study time-domain charts (plots) of the closing price of
stock shares. A typical plot takes the form of that in Figure P2–8, where in-
stead of plotting discrete closing price sample values as dots, they draw
straight lines connecting the closing price value samples. What is the $t_s$ period
for such stock market charts?

**Solution**:

The $t_s$ is one day, 24 hours.

$\square$

## 2.9

Consider a continuous time-domain sinewave defined by

$$ 
x(t) = \cos (4000 \pi t)
$$

that was sampled to produce the discrete sinewave sequence defined by

$$ 
x(n) = \cos (n \pi / 2)
$$

What is the $f_s$ sample rate, measured in Hz, that would result in sequence $x(n)$?

**Solution**:

$x(t) = \cos (2 f_o \pi t) = \cos (4000 \pi t)$, so $f_o = 2000$ Hz.
Then

$$ 
x(n) = \cos 2 \pi f_o n \frac{1}{f_s} = \cos 4000 \pi n \frac{1}{f_s}
$$

So

$$ 
4000 \pi n \frac{1}{f_s} = n \pi / 2 \\
\Rightarrow 
f_s = 8000 \text{ Hz}
$$

$\square$
