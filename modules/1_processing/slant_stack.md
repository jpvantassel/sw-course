# Slant-Stack Transform

> Joseph P. Vantassel, The University of Texas at Austin

## Basic Concept

This module summarizes the Slant-Stack Transform developed by Park et al.
(1998), full citation below. The Slant-Stack Transform is used to take
measurements from the offset-time (x-t) domain to the circular frequency-
phase velocity domain (w, c). As Park et al. (1998) detail in their paper,
the Slant-Stack Transform was developed to provide improved resolution over the
frequency-wavenumber (f-k) and the slowness-frequency (p-w) (McMechan and
Yedlin, 1981) approaches, particularly when relatively short arrays with only a
limited number of receivers. For a sense of scale, two noteworthy examples
from Park et al. (1998) include a 48 m array with 24 receivers and a 15 m array
with 32 receivers. Importantly, Park et al. (1998) concede that when the number
of receivers and length of the array increases the resolution of the p-w
transformation improves to be similar to that of newly proposed transformation
(refer to Figs. 2 and 3 in Park et al. (1998) for a direct comparison). However,
for near-surface applications where relatively short arrays with a limited
number of receivers are quite common it is not unreasonable to expect the
Slant-Stack Transform to outperform the p-w in terms of mode resolution.

## Mathematical Details

Performing the Slant-Stack Transform is a three step process:

1. Transform the data from the offset-time domain _u(x,t)_ to the
offset-frequency domain _U(x,f)_ using the Fourier transform. This is
represented mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=U(x,w)=\int_{}^{} u(x,t)e^{i2 \pi ft} dt">

2. Stack (i.e., sum) the transformed waveforms after they have been shifted
according to their offset. This is represented mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=V(f,\phi)=\int_{}^{} e^{i \phi x} \frac{U(x,f)}{| U(x,f) |}dx">

where 𝟇 is the trial wavenumber defined as:

<img src="https://render.githubusercontent.com/render/math?math=\phi=\frac{2 \pi f}{c_{trial}}">

3. Perform a change of variables to transform from the frequency-wavenumber
domain to the frequency-phase velocity.

## Implementation

The Slant-Stack Transform can be implemented using several basic steps:

1. Use the Fast Fourier Transform (FFT) to transform each trace from the time
domain to the frequency domain.

2. Loop across the frequency values of interest (typically some subset of the
positive frequencies from the FFT).

3. Inside the frequency loop, loop across a range of user-defined trial phase
velocities.

4. For each frequency-trial phase velocity pair, scale the frequency-domain
representation of each trace according to its offset and numerically integrate
the result (refer to the equation from Park et al. (1998) presented in step 2
above). Store the results as a 2D tensor (i.e., matrix).

5. Normalize the results of step 4 at each frequency (recommended) or across
all frequencies.

6. Plot the results as a 2D image (phase velocity with respect to frequency).

7. Peaks in the 2D image can be used to estimate the phase velocity of
the site's fundamental and (in some cases) higher modes.

## References

> McMechan, G.A., Yedlin, M.J., 1981. Analysis of dispersive waves by wave field
> transformation. GEOPHYSICS 46, 869–874. https://doi.org/10.1190/1.1441225

> Park, C.B., Miller, R.D., Xia, J., 1998. Imaging dispersion curves of surface
> waves on multi‐channel record, in: SEG Technical Program Expanded Abstracts
> 1998. Presented at the SEG Technical Program Expanded Abstracts 1998, Society
> of Exploration Geophysicists, pp. 1377–1380. https://doi.org/10.1190/1.1820161
