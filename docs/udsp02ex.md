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

## 2.10

Consider the two continuous signals defined by

$$ 
a(t) = \cos (4000 \pi t) \text{ and } b(t) = \cos (200 \pi t)
$$

whose product yields the $x(t)$ signal shown in Figure P2–10.
What is the minimum $f_s$ sample rate, measured in Hz, that would result in a sequence $x(n)$
with no aliasing errors (no spectral replication overlap)?

**Solution**:

Use the trigonometric identities

$$ 
\cos (x) \cos (y) = \frac{1}{2} [\cos (x-y) + \cos (x+y)]
$$

So

$$ 
x(t) = a(t) \times b(t) = \frac{1}{2} [ \cos (4200 \pi t) + \cos (3800 \pi t)]
$$

So the max frequency component is $f_o = 2100$ Hz.
Then we need to have $f_s \geq 2 \times 2100 = 4200$ Hz.

$\square$

## 2.11

Consider a discrete time-domain sinewave sequence defined by

$$ 
x(n) = \sin (n \pi / 4)
$$

that was obtained by sampling an analog $x(t) = \sin(2π f_o t)$ sinewave signal
whose frequency is $f_o$ Hz.
If the sample rate of $x(n)$ is $fs = 160$ Hz, what are
three possible positive frequency values, measured in Hz,
for $f_o$ that would result in sequence $x(n)$?

**Solution**:

$$ 
x(n) = \sin 2 \pi (f_o + k f_s) n \frac{1}{f_s} = \sin (n \pi / 4) \\
\Rightarrow \\
8 (f_o + k f_s) = f_s \\
\Rightarrow \\
8 (f_o + k f_s) = f_s \\
\Rightarrow \\
f_o + k \cdot 160 = 20 \\
$$

Let $k = 0, -1, -2$ we can get $f_o = 20, 180, 340$ Hz.

$\square$

## 2.12

In the text we discussed the notion of spectral folding that can take place when an
$x_a(t)$ analog signal is sampled to produce a discrete $x_d(n)$ sequence.
We also stated that all of the analog spectral energy contained in $X_a(f)$ will reside
within the frequency range of $\pm f_s/2$ of the $X_d(f)$ spectrum of the sampled
$x_d(n)$ sequence.

Given those concepts, consider the spectrum of an analog signal shown in Figure
P2–12(a) whose spectrum is divided into the six segments marked as 1 to 6. Fill
in the following table showing which of the A-to-F spectral segments of $X_d(f)$,
shown in Figure P2–12(b), are aliases of the 1-to-6 spectral segments of $X_a(f)$.

**Solution**:

$$ 
A \rightarrow 3 \\
B \rightarrow 4 \\
C \rightarrow 5 \\
D \rightarrow 2 \\
E \rightarrow 1 \\
F \rightarrow 6 \\
$$

$\square$

## 2.13

Consider the simple analog signal defined by $x(t)=\sin (2π700t)$ shown in Figure P2–13.
Draw the spectrum of $x(n)$ showing all spectral components, labeling their frequency 
locations, in the frequency range $[-2 f_s, 2 f_s]$

**Solution**: We have alias for $700$ at $[-1300, 300, 700, 1700]$ and
alias for $-700$ Hz at $[-1700, -700, 300, 1300]$.

$\square$

## 2.14

The Nançay Observatory, in France, uses a radio astronomy receiver that generates a wideband analog $s(t)$ signal whose spectral magnitude is represented
in Figure P2–14. The Nançay scientists bandpass sample the analog $s(t)$ signal, using an analog-to-digital (A/D) converter to produce an $x(n)$ discrete sequence,
at a sample rate of $f_s = 56$ MHz.

(a) Draw the spectrum of the $x(n)$ sequence, $X(f)$, showing its spectral energy
over the frequency range –70 MHz to 70 MHz.

**Solution**:

We have alias for $[70-7, 70+7]$ at $[14-7, 14+7], [-42-7,-42+7]$.
We have alias for $[-70-7, -70+7]$ at $[-14-7, -14+7], [42-7,42+7]$.

(b) What is the center frequency of the first positive-frequency spectral replication in $X(f)$?

**Solution**: It's 14 MHz.

(c) How is your solution to Part (b) related to the $f_s$ sample rate?

**Solution**:

$f_s = 56$ MHz, then it's $f_s / 4$.

$\square$

## 2.15

Think about the continuous (analog) signal $x(t)$ that has the spectral magnitude shown in Figure P2–15. What is the minimum $f_s$ sample rate for lowpass
sampling such that no spectral overlap occurs in the frequency range of 2 to 9
kHz in the spectrum of the discrete $x(n)$ samples?

**Solution**:

If $f_s = 20$ kHz, then there will be no overlap at all.
Since we can tolerate the overlap in the range of 9 to 10, we can reduce $f_s$ further to
$f_s = 19$ kHz. Then there is overlap for $[9,10]$, but no overlap between $[2,9]$.

$\square$

## 2.16

If a person wants to be classified as a soprano in classical opera, she must be
able to sing notes in the frequency range of 247 Hz to 1175 Hz. What is the
minimum $f_s$ sampling rate allowable for bandpass sampling of the full audio
spectrum of a singing soprano?

**Solution**:

In this case,

$$ 
f_c = 711, B = 1175 - 247 = 928
$$

So

$$ 
f_s = \frac{2 f_c+B}{1} = 2350 \text{ Hz} 
$$

## 2.17

This problem requires the student to have some knowledge of electronics and
how a mixer operates inside a radio. (The definition of a bandpass filter is
given in Appendix F.) Consider the simplified version of what is called a su-
perheterodyne digital radio depicted in Figure P2–17.

(a) For what local oscillator frequency, $f_{\text{LO}}$, would an image
(a copy, or duplication) of the $w(t)$ signal’s spectrum be centered at 15 MHz
(megahertz) in signal $u(t)$?

**Solution**: Since the analog bandpass filter #1's Center frequency = 50 MHz
and bandwidth = 10 MHz, then we can assume 

$$ 
w(t) = \sin (2 \pi 40 t) + \sin (2 \pi 30 t)
$$

Then since $m(t) = \sin (2 \pi l t)$, then

$$
u(t) = w(t) m(t) =
\frac{1}{2} [
\cos (2 \pi t (40 - l)) - \cos (2 \pi t (40 + l))
]
+
\frac{1}{2} [
\cos (2 \pi t (30 - l)) - \cos (2 \pi t (30 + l))
]
$$

So if $f_{\text{LO}} = 20$, we can have an image of the $w(t)$ signal’s spectrum be centered at 15 MHz in signal $u(t)$.

$\square$

(b) What is the purpose of the analog bandpass filter #2?

**Solution**: filter out all the signals beyond $[12.5, 17.5]$ MHz.

(c) Fill in the following table showing all ranges of acceptable fs bandpass
sampling rates to avoid aliasing errors in the discrete $x(n)$ sequence. Also
list, in the rightmost column, for which values of $m$ the sampled spectrum, centered at
15 MHz, will be inverted.

**Solution**:

Since $f_c = 15, B = 5$

$$
\left[ 
    \frac{2 f_c + B}{m+1},
    \frac{2 f_c - B}{m}
 \right] =
\begin{cases}
    [17.5, 25.0] &\text{if } m = 1 \text{ inverted }\\
    [11.7, 12.5] &\text{if } m = 2 \text{ not inverted }\\
    [8.75, 8.33] &\text{if } m = 3 \text{ invalid!!} \\
\end{cases}
$$

Note here, when $m = 3$, $f_s < 2B$, then it's not
valid.

(d) In digital receivers, to simplify AM and FM demodulation, it 
is advantageous to have the spectrum of the discrete $x(n)$ 
sequence be centered at one-quarter of the sample rate. The text’s 
Eq. 2–11 describes how to achieve this situation.
If we were constrained to have $f_s$ equal to 12 MHz, what would
be the maximum $f_{\text{LO}}$ local oscillator frequency such that the 
spectra of $u(t)$, $x(t)$, and $x(n)$ are centered at $f_s/4$? 
(Note: In this scenario, the $f_c$ center frequency of analog 
bandpass filter #2 will no longer be 15 MHz.)

**Solution**:

$$
f_s = \frac{4 f_c}{2k - 1} \\
\Rightarrow \\
f_c = \frac{2k-1}{4} f_s = 6k - 3 \\
\Rightarrow \\
f_c = 3, 9, 15, \cdots
$$

The $f_c$ cannot be $3$, since $w(t)$ then bandwidth is $10$.
$9$ is fine. In this case, the $f_{\text{LO}} = 26$ MHz.

$\square$

## 2.18

Think about the analog anti-aliasing filter given in Figure 
P2–18(a), having a one-sided bandwidth of $B$ Hz. A wideband 
analog signal passed through that filter, and then sampled, 
would have an $|X(m)|$ spectrum as shown in Figure
P2–18(b), where the dashed curves represent spectral 
replications.

Suppose we desired that all aliased spectral components in
$|X(m)|$ over our $B$ Hz bandwidth of interest must be 
attenuated by at least $60$ dB. Determine the equation, in 
terms of $B$ and the $f_s$ sampling rate, for the frequency 
at which the anti-aliasing filter must have an attenuation 
value of –60 dB. The solution to this problem gives us a 
useful rule of thumb we can use in specifying the desired 
performance of analog anti-aliasing filters.

**Solution**: let the width of small area be $c$,
then we have $2B + c = f_s$, so

$$ 
B+c = f_s - B
$$

So the anti-aliasing filter needs to have an attenuation 
value of –60 dB at $f_s - B$ Hz.

$\square$

## 2.19

This problem demonstrates a popular way of performing 
frequency down-conversion (converting a bandpass signal into 
a lowpass signal) by way of bandpass sampling. Consider the 
continuous 250-Hz-wide bandpass $x(t)$ signal whose spectral 
magnitude is shown in Figure P2–19. Draw the spectrum,
over the frequency range of –1.3$f_s$ to +1.3$f_s$, of the
$x(n)$ sampled sequence obtained when $x(t)$ is sampled at 
$f_s=1000$ samples/second.

**Solution**:

The results is exactly like the following 2-9 (c).

## 2.20

Here’s a problem to test your understanding of bandpass 
sampling. Think about the continuous (analog) signal $x(t)$ 
that has the spectral magnitude shown in Figure P2–20.

(a) What is the minimum $f_c$ center frequency, in terms of
$x(t)$’s bandwidth $B$, that enables bandpass sampling of $x(t)$? Show your work.

**Solution**: To be able to do the bandpass sampling,
use the figure 2-9 (a) (b) you need at least to have

$$ 
f_c = B + B/2 = \frac{3}{2}B
$$

$\square$

(b) Given your results in Part (a) above, determine if it is 
possible to perform bandpass sampling of the full spectrum 
of the commercial AM (amplitude modulation) broadcast radio band in North America. Explain your solution.

**Solution**:

According to the wiki, the commercial AM broadcast radio band in North America occupies the frequency range 535 to 1705 kHz.

Then $B = 1170, B/2 = 585, f_c = 1120$, so
$f_c < \frac{3}{2}B$.

It is not possible.

$\square$

## 2.21

Suppose we want to perform bandpass sampling of a continuous 5 
kHz-wide bandpass signal whose spectral magnitude is shown in Figure P2–21.

Fill in the following table showing the various ranges of 
acceptable $f_s$ band-pass sampling rates, similar to the text’s 
Table 2–1, to avoid aliasing errors. Also list, in the rightmost 
column, for which values of m the sampled spectrum in the vicinity 
of zero Hz is inverted.

**Solution**:

$f_c = 25, B = 5$ 
$$
\left[ 
    \frac{2 f_c + B}{m+1},
    \frac{2 f_c - B}{m}
 \right] =
\begin{cases}
    [27.5, 45.0] &\text{if } m = 1 \text{ inverted }\\
    [18.3, 22.5] &\text{if } m = 2 \text{ not inverted }\\
    [13.75, 15.0] &\text{if } m = 3 \text{ inverted } \\
    [11, 11.25] &\text{if } m = 4 \text{ not inverted } \\
    [9.17, 9] &\text{if } m = 5 \text{ invalid!! } \\
\end{cases}
$$

$\square$

## 2.22

I recently encountered an Internet website that allegedly gave an 
algorithm for the minimum fs bandpass sampling rate for an analog 
bandpass signal centered at $f_c$ Hz, whose bandwidth is $B$ Hz. The algorithm is

$$ 
f_{s, \min } =
\frac{4 f_c}{2Z - 1}
$$

where

$$ 
Z = \left\lfloor 
\frac{4 f_c + 2B}{4B}
\right\rfloor 
$$

Here’s the problem: Is the above $f_{s,\min}$ algorithm correct in 
computing the absolute minimum possible
nonaliasing $f_s$ bandpass sampling rate for an analog bandpass 
signal centered at $f_c$ Hz, whose bandwidth is $B$ Hz? Verify 
your answer with an example.

**Solution**:

In ex 2.21, $f_c = 25, B = 5, Z = 5$,
then

$$ 
f_{s, \min } =
\frac{100}{9} = 11.11 > 11
$$

So this algorithm is not correct.

$\square$
