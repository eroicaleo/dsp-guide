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