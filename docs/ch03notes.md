# Chapter 3 ADC and DAC

## Selecting The Antialias Filter

* The Chebyshev optimizes the roll-off, the Butterworth optimizes the passband flatness, and the Bessel optimizes the step response.

* 2 common ways for information to be encoded in an analog waveform, only two methods are common:
    * **time domain encoding**
        * time domain encoding uses the shape of the waveform to store information
            * Example: electrocardiogram of EKG, Images.
    * **frequency domain encoding**
        * the information is contained in sinusoidal waves that combine to form the signal
            * Example: Audio / Music
            * changes the phase of the various sinusoids, looks 
              different on scope, but sounds the same
            * We need antialias filter with a sharp cutoff, such as 
              a Chebyshev, Elliptic, or Butterworth.
            * Step response is not important.

## Multirate Data Conversion

* Digital recorder example:
    * Capture the frequencies between about 100 and 3000 hertz with 
      40 kHz noise
* Analog solution:
    * 8-pole low-pass Chebyshev at 3 kHz, then sample at 8 kHz
    * the DAC reconstructs the analog signal at 8 kHz with a zeroth 
      order hold.
* Multirate techniques:
    * sample the data at 64 kHz
    * remove these unusable frequencies in software, by using a 
      digital low-pass filter at 3 kHz
    * resample the digital signal from 64 kHz to 8 kHz by simply 
      discarding every seven out of eight samples, a procedure 
      called decimation.
    * 8 kHz data converter to 64 kHz with interpolation.
    * Everything above 3 kHz is then removed with a digital low-pass 
      filter.
    * a simple RC network is all that is required to produce the 
      final voice signal.
* The advantages for multirate data conversion:
    * mass produced products
    * digital filters outperform analog filters by hundreds of times 
      in key areas.

## Single Bit Data Conversion

* Delta modulation
    * Use a comparator, if input voltage is bigger than the voltage
      on the capacitor, output 1 and feedback to capacitor to increase the voltage
    * if input voltage is smaller than the voltage
      on the capacitor, output 0 and feedback to capacitor to decrease the voltage
* Continuously Variable Slope Delta (CVSD) modulator
    * If detected 4 consecutive 0/1 increase the charging/
      discharging rate.
    * At the receiver, the analog signal is reconstructed by 
      incorporating a syllabic filter that is identical to the one 
      in the transmission circuit.
