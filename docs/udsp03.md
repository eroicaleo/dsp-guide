# Chapter 03 The Discrete Fourier Transform

* The discrete Fourier transform (DFT) is one of the two most common, and 
  powerful, procedures encountered in the field of digital signal processing.
  (Digital filtering is the other.)

Continuous Fourier Transform

$$ 
\tag{3-1}
X(f) =\int_{-\infty }^{+\infty}
x(t) e^{-j2πft} dt
$$

> A prominent quote from Lord Kelvin better states this sentiment: 
> “Fourier’s theorem is not only one of the most beautiful results 
> of modern analysis, but it may be said to furnish an 
> indispensable instrument in the treatment of nearly every 
> recondite question in modern physics.

DFT equation (exponential form):

$$
\tag{3-2}
X(m) = \sum_{n = 0}^{N-1} x(n) e^{-j2πnm/N}
$$

## 3.1 UNDERSTANDING THE DFT EQUATION

DFT equation (rectangular form):

$$
\tag{3-3}
X(m) = \sum_{n = 0}^{N-1} x(n) [\cos (2πnm/N) -j \sin (2πnm/N)]
$$

* $X(m) =$ the $m$th DFT output component
    * $m =$ the index of the DFT output in the frequency domain.
    * $m = 0, 1, 2, 3, . . ., N–1$.
* $x(n) =$ the sequence of input samples
    * $n =$ the time-domain index of the input samples.
    * $n = 0, 1, 2, 3, . . ., N–1$.
* $N =$ the number of samples of the input sequence and the number 
  of frequency points in the DFT output.
    * The value $N$ is an important parameter because it determines 
      how many input samples are needed, the resolution of the 
      frequency-domain results, and the amount of processing time
      necessary to calculate an $N$-point DFT.

* The exact frequencies of the different sinusoids depend on both 
  the sampling rate $f_s$ at which the original signal was sampled, and the number of samples $N$.
* For example, if we are sampling a continuous signal at a rate of 
  500 samples/second and, then, perform a $16$-point DFT on the 
  sampled data, the fundamental frequency of the sinusoids is
  $f_s/N = 500/16$ or $31.25$ Hz.

The $N$ separate DFT analysis frequencies are

$$
\tag{3-5}
f_{\text{analysis}}(m) = \frac{m f_s}{N}.
$$

### The magnitude

$$ 
\tag{3-6}
X(m) = X_\text{real} + j X_{\text{imag}}
$$

Then the magnitude of $X(m)$ is

$$ 
\tag{3-7}
X_{\text{mag}} = |X(m)| = \sqrt[]{X_{\text{real}}(m)^2 + X_{\text{imag}}(m)^2}
$$

### 3.1.1 DFT Example 1

Consider performing an 8-point DFT on a continuous input signal containing
components at 1 kHz and 2 kHz a input signal:

$$ 
x_{in}(t) = \sin(2π⋅1000⋅t) + 0.5\sin(2π⋅2000⋅t+3π/4)
$$

And we use $f_s = 8000$ samples/second.

Then

$$ 
x(n) = \sin(2π⋅1000⋅n⋅t_s) + 0.5\sin(2π⋅2000⋅n⋅t_s+3π/4),
\quad
t_s = \frac{1}{8000}
$$

our eight $x(n)$ samples are:

```python
from scipy.fft import fft, fftfreq
import numpy as np

fs = 8000  # Sampling rate in Hz
n = np.arange(0, 8, 1)  # Time vector
ts = 1.0 / fs
# Signal with 1000 Hz and 2000 Hz components
x = 1.0*np.sin(2*np.pi*1000*n*ts) + 0.5*np.sin(2*np.pi*2000*n*ts + (3/4)*np.pi)

x
array([ 0.35355339,  0.35355339,  0.64644661,  1.06066017,
0.35355339, -1.06066017, -1.35355339, -0.35355339])
```

We can either use `scipy.fft` or manual:

```python
X = fft(x)
np.around(X,4)

array([ 0.    -0.j    , -0.    -4.j    ,  1.4142+1.4142j,
0.    +0.j    ,-0.    -0.j    ,  0.    -0.j    ,  1.4142-1.4142j, -0.    +4.j    ])

N = 8
Y = np.array([0+0*1j]*N)
for m in range(N):
    Y[m] = 0 + 0*1j
    for n in range(N):
        Y[m] = Y[m] + x[n] * (np.cos(-2*np.pi*n*m/N) + 1j*np.sin(-2*np.pi*n*m/N))

np.around(Y,4)

array([ 0.    +0.j    , -0.    -4.j    ,  1.4142+1.4142j,
0.    -0.j    , -0.    -0.j    ,  0.    +0.j    ,  1.4142-1.4142j, -0.    +4.j    ])

np.allclose(X, Y)

True
```

![](./assets/ch0304.png)

We have the following observations from this figure:

* By looking at the $|X(m)|$, we can see, $|X(0)| = 0$, that means
$x(n)$ has no DC component.

* Looking at Figure 3–4(b), we might notice that the phase of
  $X(1)$ is $–90$ degrees. It compares against a $\cos$ wave at
  frequency $\frac{m f_s}{N}$.
    * At the frequency $1 f_s / N = 8000 / 8 = 1000$, the phase is
      $-90$, which corresponds to $\sin(2π⋅1000⋅t)$. This is
      correct, because $\cos (2π⋅1000⋅t - 90) = \sin (2π⋅1000⋅t)$.
    * At the frequency $2 f_s / N = 8000 / 8 = 2000$, the phase is
      $+45$, which corresponds to $\sin(2π⋅2000⋅t + 3/4 \pi)$. 
      This is correct, because $\cos \theta = \sin (\theta + \pi / 2)$, so $\cos (2π⋅1000⋅t + 45) = \sin 
      (2π⋅1000⋅t + 45 + 90)$.

* 2 open questions:
    * What are the components when $m = 6, 7$.
    * Why the max magnitude is $4$ instead of $1$.

> 2 very important characteristics of the DFT that we should never forget.
* any individual $X(m)$ output value is nothing more than the sum 
  of the term-by-term products, a correlation, of an input signal 
  sample sequence with a cosine and a sinewave whose frequencies 
  are $m$ complete cycles in the total sample interval of $N$ 
  samples. This is true no matter what the $f_s$ sample rate is 
  and no matter how large $N$ is in an $N$-point DFT.
* The second important characteristic of the DFT of real input 
  samples is the symmetry of the DFT output terms.

### 3.2 DFT SYMMETRY

Consider $x(n)$ is a real signal. Using equation (3-2), we have

$$
\begin{split}
X(N-m)
&= \sum_{n = 0}^{N-1} x(n) e^{-j2πn(N-m)/N} \\
&= \sum_{n = 0}^{N-1} x(n) e^{-j2πn} e^{j2πnm/N} \\
&= \sum_{n = 0}^{N-1} x(n) e^{j2πnm/N} \\
&= \left(\sum_{n = 0}^{N-1} x(n) e^{-j2πnm/N}\right)^*  \\
&= (X(m))^* \\
\end{split}
$$

* If that real input function is even, then $X(m)$ is
  always real and even.
* If the real input function is odd, then $X(m)$ is always
  pure imaginary.

### 3.3 DFT LINEARITY

$$
\begin{split}
X_1(m) + X_2(m)
&= \sum_{n = 0}^{N-1} x_1(n) e^{-j2πnm/N}
+ \sum_{n = 0}^{N-1} x_2(n) e^{-j2πnm/N} \\
&= \sum_{n = 0}^{N-1} (x_1(n) + x_2(n)) e^{-j2πnm/N} \\
&= X_{\text{sum}}(m)
\end{split}
$$

## 3.4 DFT MAGNITUDES

* When a real input signal contains a sinewave component,
  whose frequency is less than half the $f_s$ sample rate, of peak 
  amplitude $A_o$ with an integral number of cycles over $N$ input samples, the output magnitude of the DFT for that particular sinewave is $M_r$ where

$$
\tag{3-17}
M_r = \frac{A_o N}{2}
$$

* If the DFT input is a complex sinusoid of magnitude Ao (i.e., 
  $A_o e^{j2πfnt_s}$) with an integer number of cycles over $N$
  samples, the $M_c$ output magnitude of the DFT for that 
  particular sinewave is

$$ 
\tag{3-17'}
M_c = A_o N
$$

The other 2 forms of DFT

$$
\tag{3-18}
X'(m) = \frac{1}{N} \sum_{n = 0}^{N-1} x(n) e^{-j2πnm/N}
$$

Or

$$
\tag{3-18'}
X'(m) = \frac{1}{\sqrt[]{N}} \sum_{n = 0}^{N-1} x(n) e^{-j2πnm/N} \\
x'(n) = \frac{1}{\sqrt[]{N}} \sum_{m = 0}^{N-1} X(m) e^{j2πnm/N} \\
$$

## 3.5 DFT FREQUENCY AXIS

* Just remember that the DFT’s frequency spacing (resolution) is 
  $f_s/N$.

> * Each DFT output term is the sum of the term-by-term products of an
input time-domain sequence with sequences representing a sine and a
cosine wave.
> * For real inputs, an $N$-point DFT’s output provides only $N/2+1$ independent terms.
> * The DFT is a linear operation.
> * The magnitude of the DFT results is directly proportional to $N$.
> * The DFT’s frequency resolution is $f_s/N$.

## 3.6 DFT SHIFTING THEOREM

Consider $x'(n) = x(n+k), x(n) = x(n+N), 0 \leq k < N$ and

$$
\tag{3-19}
\begin{split}
X'(m) 
&= \sum_{n = 0}^{N-1} x'(n) e^{-j2πnm/N} \\
&= \sum_{n = 0}^{N-1} x(n+k) e^{-j2πnm/N} \\
&= e^{j2πkm/N} \sum_{n = 0}^{N-1} x(n+k) e^{-j2π(n+k)m/N} \\
&= e^{j2πkm/N} \sum_{l = k}^{N-1+k} x(l) e^{-j2πlm/N} \\
&= e^{j2πkm/N} \sum_{l = 0}^{N-1} x(l) e^{-j2πlm/N} \\
\end{split}
$$

$\square$

### 3.6.1 DFT Example 2

We still use the same example in 3.1.1

$$
x_{in}(t) = \sin(2π⋅1000⋅t) + 0.5\sin(2π⋅2000⋅t+3π/4)
$$

And let $x'(n) = x(n+3)$, here is the python code

```python
from scipy.fft import fft, fftfreq
import numpy as np

fs = 8000  # Sampling rate in Hz
n = np.arange(0, 8, 1)  # Time vector
ts = 1.0 / fs
# Signal with 1000 Hz and 2000 Hz components
x = 1.0*np.sin(2*np.pi*1000*n*ts) + 0.5*np.sin(2*np.pi*2000*n*ts + (3/4)*np.pi)

x_1 = np.roll(x, -3)
x_1

array([ 1.06066017,  0.35355339, -1.06066017, -1.35355339, -0.35355339, 0.35355339,  0.35355339,  0.64644661])

X_1 = fft(x_1)
np.around(X_1,4)

array([ 0.    -0.j    ,  2.8284+2.8284j,  1.4142-1.4142j, -0.    +0.j    ,
        0.    -0.j    , -0.    -0.j    ,  1.4142+1.4142j,  2.8284-2.8284j])

X_2 = np.array([0+0*1j]*N)
for m in range(N):
    X_2[m] = np.exp(1j * 2 * np.pi * 3 * m / N) * X[m]
np.around(X_2,4)

array([ 0.    +0.j    ,  2.8284+2.8284j,  1.4142-1.4142j, -0.    +0.j    ,
        0.    -0.j    , -0.    -0.j    ,  1.4142+1.4142j,  2.8284-2.8284j])

np.allclose(X_1, X_2)
True
```

$\square$

## 3.7 INVERSE DFT

$$
\tag{3-23}
x(n) = \frac{1}{N} \sum_{m = 0}^{N-1} x(m) e^{j2πmn/N}
$$

$$
\tag{3-23'}
x(n) = \frac{1}{N} \sum_{m = 0}^{N-1} X(m) [\cos (2πmn/N) + j \sin(2πmn/N)]
$$

Here is the python code to implement it

```python
from scipy.fft import fft, fftfreq, ifft
import numpy as np

fs = 8000  # Sampling rate in Hz
n = np.arange(0, 8, 1)  # Time vector
ts = 1.0 / fs
# Signal with 1000 Hz and 2000 Hz components
x = 1.0*np.sin(2*np.pi*1000*n*ts) + 0.5*np.sin(2*np.pi*2000*n*ts + (3/4)*np.pi)

X = fft(x)
x_ifft = ifft(X)
np.around(x_ifft,4)

array([ 0.3536+0.j,  0.3536+0.j,  0.6464+0.j,  1.0607+0.j,  0.3536+0.j,
       -1.0607+0.j, -1.3536-0.j, -0.3536+0.j])

Y_inv = np.array([0+0*1j]*N)
for m in range(N):
    Y_inv[m] = 0 + 0*1j
    for n in range(N):
        Y_inv[m] = Y_inv[m] + (1 / N) * X[n] * (np.cos(2*np.pi*n*m/N) + 1j*np.sin(2*np.pi*n*m/N))
np.around(Y_inv, 4)

array([ 0.3536+0.j,  0.3536+0.j,  0.6464+0.j,  1.0607+0.j,  0.3536+0.j,
       -1.0607+0.j, -1.3536-0.j, -0.3536+0.j])

np.allclose(x_ifft, Y_inv)
True
```

$\square$
