# Chapter 01 Discrete Sequences and Systems

## 1.1 DISCRETE SEQUENCES AND THEIR NOTATION

* Think of a continuous sinewave with a
  peak amplitude of $1$ at a frequency $f_o$ 
  described by the equation

$$ 
\tag{1-1}
x(t) = \sin 2 \pi f_o t
$$

* Those sample values can be represented 
  collectively, and concisely, by the 
  discrete-time expression

$$ 
\tag{1-3}
x(n) = \sin 2 \pi f_o n t_s
$$

## 1.2 SIGNAL AMPLITUDE, MAGNITUDE, POWER

If we assume that the proportionality constant is one, we can 
express the power of a sequence in the time or frequency domains as

$$ 
\tag{1-8}
x_{pwr}(n) = |x(n)|^2
$$

or

$$ 
\tag{1-8'}
X_{pwr}(m) = |X(m)|^2
$$

## 1.3 SIGNAL PROCESSING OPERATIONAL SYMBOLS

* Addition

$$ 
a(n) = b(n) + c(n)
$$

* Subtraction

$$ 
a(n) = b(n) - c(n)
$$

* Summation

$$ 
\begin{split}
a(n)
&= \sum_{k=n}^{n+3} b(k) \\
&= b(n) + b(n+1) + b(n+2) + b(n+3)
\end{split}
$$

* Multiplication

$$ 
a(n) = b(n)c(n) = b(n) \cdot c(n)
$$

## 1.8 ANALYZING LINEAR TIME-INVARIANT SYSTEMS

* If we know the unit impulse response of an LTI system, we
  can calculate everything there is to know about the system; 
  that is, the system’s unit impulse response completely characterizes the system.

* By “unit impulse response” we mean the system’s time-domain 
  output sequence when the input is a single unity-valued 
  sample (unit impulse) preceded and followed by zero-valued 
  samples as shown in Figure 1–11(b).

* The concepts in the two following sentences are among the 
  most important principles in all of digital signal processing!
    * ***Knowing the (unit) impulse response of an LTI system, 
      we can determine the system’s output sequence for any 
      input sequence because the output is equal to the 
      convolution of the input sequence and the system’s impulse response.***
    * ***Given an LTI system’s time-domain impulse response, we 
      can find the system’s frequency response by taking the 
      Fourier transform in the form of a discrete Fourier 
      transform of that impulse response***

* In the world of DSP, an impulse sequence called a unit 
  impulse takes the form

$$
\tag{1-26}
x(n) = \cdots,0,0,0,0,0,A,0,0,0,0,0,\cdots 
$$

* The leading 0 must be long enough, so the system is outputing
  0.
* The trailing 0 must also be long enough, so it's longer than
  the transient response.
