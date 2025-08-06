# Chapter 02 Periodic Sampling

* Our primary concern is just how fast a given continuous signal
  must be sampled in order to preserve its information content.

## 2.1 ALIASING: SIGNAL AMBIGUITY IN THE FREQUENCY DOMAIN

If a signal can be defined by

$$ 
\tag{2-1}
x(t) = \sin (2 \pi f_o t)
$$

and

$$ 
\tag{2-2}
x(n) = \sin (2 \pi f_o n t_s)
$$

Then we can have

$$ 
\tag{2-3}
x(n) = \sin (2 \pi f_o n t_s)
= \sin (2 \pi f_o n t_s + 2 \pi m)
= \sin (2 \pi (f_o + \frac{m}{n t_s}) n t_s )
$$

So if we consider a sine wave with frequency of $f_o + k f_s, k \in \mathbb{Z}$, then

$$
\tag{2-5}
x'(n) = \sin (2 \pi (f_o + k f_s) t_s) = \sin (2 \pi f_o n t_s + 2 \pi k)
= \sin (2 \pi f_o n t_s) = x(n)
$$

When sampling at a rate of $f_s$ samples/second, if $k$ is any positive or negative
integer, we cannot distinguish between the sampled values of a sinewave of
$f_o$ Hz and a sinewave of $(f_o + kf_s)$ Hz.

The frequency $f_s / 2$ is an important quantity in sampling theory and is referred to by 
different names in the literature, such as critical Nyquist, half Nyquist, and folding
frequency.

## 2.2 SAMPLING LOWPASS SIGNALS

If we reduce the $f_s = 1.5 B < 2 B$, the we see the lower edge and upper edge of the
spectral replications centered at $+f_s$ and $–f_s$ now lie in our band of interest.
The spectral information in the bands of $–B$ to $–B/2$ and
$B/2$ to $B$ Hz has been corrupted.

The entire spectral content of the original continuous signal is now residing in the band
of interest between $–f_s/2$ and $+f_s/2$.
This key property was true in Figure 2–4(b) and will always be true, regardless of the 
original signal or the sample rate.

This problem is solved in practice by using an analog low-pass anti-aliasing filter prior to
A/D conversion to attenuate any unwanted
signal energy above $+B$ and below $–B$ Hz as shown in Figure 2–6.

## 2.3 SAMPLING BANDPASS SIGNALS

Use the following figure, we can derive the relation between $f_s$ and $f_c$.

![alt text](./assets/ch0208.png)

From (a) it's

$$ 
2 f_c - B = m f_s
$$

From (b) it's

$$ 
2 f_c + B = (m + 1) f_s
$$

And also $f_s \geq 2B$, so overall

$$
\tag{2-10}
\frac{2 f_c + B}{m + 1} \leq f_s \leq \frac{2 f_c - B}{m}
$$

The figure 2-9 is interesting.

![alt text](./assets/ch0209.png)

## 2.4 PRACTICAL ASPECTS OF BANDPASS SAMPLING

### 2.4.1 Spectral Inversion in Bandpass Sampling

When $m$ is odd number in equation 2-10, the positive-frequency sampled baseband will have
the inverted shape of the negative half from the original analog spectrum.

The discrete spectrum of any digital signal can be inverted by multiplying the signal’s
discrete-time samples by a sequence of alternating plus ones and minus ones
($1, –1, 1, –1$, etc.), indicated in the literature by the succinct expression $(–1)^n$.

We need to remember at this point is the simple rule that multiplication of real signal 
samples by $(–1)^n$ flips the positive-frequency band of
interest, from zero to $+f_s/2$ Hz, where the center of the flipping is $f_s/4$ Hz.
As shown in the figure 2-10.

![alt text](./assets/ch0210.png)

### 2.4.2 Positioning Sampled Spectra at $f_s/4$

In some application, we are required to sample at the $f_s$ such that the
ampled spectra to be centered exactly at $\pm f_s/4$.

As we’ll see in later chapters, this scenario greatly simplifies certain common operations 
such as:
* digital filtering
* complex down-conversion
* Hilbert transformations

When $f_c = f_s/4$ already, we do not have to do anything. Otherwise we can use the following
equation

$$ 
f_c + \frac{f_s}{4} = k f_s, k = 1, 2, \cdots \\
\text{ or } \\
f_c - \frac{f_s}{4} = k f_s, k = 1, 2, \cdots \\
$$

So overall, we have

$$ 
f_s = \frac{4 f_c}{2k - 1}, k = 1, 2, \cdots
$$

### 2.4.3 Noise in Bandpass-Sampled Signals

The spectrum of an analog lowpass signal, output from an analog anti-aliasing lowpass filter
contains some amount of background noise power.

The bandpass-sampled signal will have an increased level of background noise
because all of the background spectral noise
must now reside in the range of $–f_s/2$ to $f_s/2$.

The bandpass-sampled background noise power increases by a factor of m + 1.

The bandpass-sampled signal’s SNR, measured in decibels, is reduced by

$$
\tag{2-12}
D_{\text{SNR}} = 10 \cdot \log_{10} (m + 1) \text{dB}
$$

![alt text](./assets/ch0211.png)
