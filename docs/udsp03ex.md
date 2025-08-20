# Chapter 03 The Discrete Fourier Transform

## 3.1

Let’s assume that we have performed a 20-point DFT on a sequence 
of real-valued time-domain samples, and we want to send our $X(m)$ 
DFT results to a  colleague using e-mail. What is the absolute 
minimum number of (complex) frequency-domain sample values we will 
need to type in our e-mail so that our colleague has complete 
information regarding our DFT results?

**Solution**:

Since it is symmetric, we will just need send 10.

$\square$

## 3.2

Assume a systems engineer directs you to start designing a system 
that performs spectrum analysis using DFTs. The systems engineer 
states that the spectrum analysis system’s input data sample rate, 
$f_s$, is $1000$ Hz and specifies that the DFT’s frequency-domain sample spacing must be exactly $45$ Hz.

(a) What is the number of necessary input time samples, $N$, for a 
single DFT operation?

**Solution**:

If we want to achive $45$ Hz, we know the DFT’s frequency spacing 
(resolution) is $f_s/N$.

So $f_s / N \leq 45$, then $N \geq 23$.

$\square$

(b) What do you tell the systems engineer regarding the spectrum 
analysis system’s specifications?

**Solution**:

The $f_s$ needs to be $900$ Hz.

$\square$

## 3.3

We want to compute an $N$-point DFT of a one-second-duration 
compact disc (CD) audio signal $x(n)$, whose sample rate is
$fs = 44.1$ kHz, with a DFT sample spacing of $1$ Hz.

(a) What is the number of necessary $x(n)$ time samples, $N$?

**Solution**: Again, we know the DFT’s frequency spacing 
(resolution) is $f_s/N$. So

$$ 
\frac{f_s}{N} = \frac{44100}{N} = 1
$$

Then $N = 441000$.

$\square$

(b) What is the time duration of the $x(n)$ sequence measured in 
seconds?
Hint: This Part (b) of the problem is trickier than it first 
appears. Think carefully.

**Solution**:

It should be

$$ 
1 \text{ second} \cdot \frac{44100 - 1}{44100} \approx 0.99997732
\text{ second}
$$

$\square$

## 3.4

Assume we have a discrete $x(n)$ time-domain sequence of samples 
obtained from lowpass sampling of an analog signal, $x(t)$.
If $x(n)$ contains $N = 500$ samples, and it was obtained at a 
sample rate of $f_s = 3000$ Hz:

(a) What is the frequency spacing of $x(n)$’s DFT samples, $X(m)$, 
measured in Hz?

**Solution**:

Again, it is

$$ 
\frac{f_s}{N} = \frac{3000}{500} = 6 \text{ Hz}
$$

$\square$

(b) What is the highest-frequency spectral component that can be 
present in the analog $x(t)$ signal where no aliasing errors occur 
in $x(n)$?

**Solution**:

The highest-frequency spectral component has to be $\leq \frac{f_s}
{2}$.

$\square$

(c) If you drew the full $X(m)$ spectrum and several of its 
spectral replications, what is the spacing between the spectral 
replications measured in Hz?

**Solution**:

I am not exactly sure. Let's say the original signal has the
frequency component of $1500 - 6 = 1494$ Hz. Then the spacing
between spectral replications is $(1500 + 6) - (1500-6) = 12$ Hz.

$\square$
