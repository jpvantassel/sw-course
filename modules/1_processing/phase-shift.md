# Phase-Shift Transform

> Joseph P. Vantassel, The University of Texas at Austin

## Basic Concept

This module summarizes the Phase-Shift Transform developed by Park et al.
(1998) with further details presented in Ryden et al. (2004). The Phase-Shift
Transform is used to convert measurements in the offset-time (x-t) domain to the
circular frequency-phase velocity domain (w, c). As Park et al. (1998) detail in
their paper, the Phase-Shift Transform was developed to provide improved
resolution over the frequency-wavenumber (f-k) (Gabriels et al. 1987) and the
slowness-frequency (p-w) (McMechan and Yedlin, 1981) approaches, particularly
for relatively short arrays with a limited number of receivers. For a sense of
scale, two arrays presented in Park et al. (1998) that are shown to perform
better than the p-w transform include a 48 m array with 24 receivers and a
15 m array with 32 receivers. Importantly, Park et al. (1998) concede that when
the number of receivers and length of the array increases the resolution of the
p-w transformation improves to be similar to that of the Phase-Shift
(refer to Figs. 2 and 3 in Park et al. (1998) for a direct comparison). However,
for near-surface applications where relatively short arrays with a limited
number of receivers are quite common it is not unreasonable to expect the
Phase-Shift Transform to outperform the p-w in terms of mode resolution.

## Mathematical Details

Performing the Phase-Shift Transform is a three step process:

1. Transform the data from the offset-time domain _u(x,t)_ to the
offset-frequency domain _U(x,f)_ using the Fourier transform. This is
represented mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=U(x,w)=\int_{}^{} u(x,t)e^{i2 \pi ft} dt">

2. Sum the transformed waveforms after they have been shifted
according to their offset. This is represented mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=V(f,\phi)=\int_{}^{} e^{i \phi x} \frac{U(x,f)}{| U(x,f) |}dx">

where 𝟇 is the trial wavenumber defined as:

<img src="https://render.githubusercontent.com/render/math?math=\phi=\frac{2 \pi f}{c_{trial}}">

3. Perform a change of variables to transform from the frequency-wavenumber
domain to the frequency-phase velocity.

## Implementation

The Phase-Shift Transform can be implemented using several basic steps:

1. Use the Fast Fourier Transform (FFT) to transform each trace from the time
domain to the frequency domain.

2. Loop across the frequency values of interest (typically some subset of the
positive frequencies from the FFT).

3. Inside the frequency loop, loop across a range of user-defined trial phase
velocities.

4. For each frequency-trial phase velocity pair, scale the frequency-domain
representation of each trace according to its offset and numerically integrate
the result (refer to the equation from Park et al. (1998) presented in step 2
above). Store the absolute value of the complex valued results in a 2D tensor
(i.e., matrix).

5. Normalize the results of step 4. Note this normalization is typically
performed across all frequencies and velocities, and is not performed on a
frequency-by-frequency basis as is common with other transformations (e.g.,
Xia et al. 2007).

6. Plot the results as a 2D image (phase velocity with respect to frequency).

7. Peaks in the 2D image can be used to estimate the phase velocity of
the site's fundamental and (in some cases) higher surface wave modes.

## References

> Gabriels, P., Snieder, R., Nolet, G., 1987. In situ measurements of
> shear-wave velocity in sediments with higher-mode rayleigh waves. Geophys
> Prospect 35, 187–196. https://doi.org/10.1111/j.1365-2478.1987.tb00812.x

> McMechan, G.A., Yedlin, M.J., 1981. Analysis of dispersive waves by wave field
> transformation. GEOPHYSICS 46, 869–874. https://doi.org/10.1190/1.1441225

> Park, C.B., Miller, R.D., Xia, J., 1998. Imaging dispersion curves of surface
> waves on multi‐channel record, in: SEG Technical Program Expanded Abstracts
> 1998. Presented at the SEG Technical Program Expanded Abstracts 1998, Society
> of Exploration Geophysicists, pp. 1377–1380. https://doi.org/10.1190/1.1820161

> Ryden, N., Park, C.B., Ulriksen, P., Miller, R.D., 2004. Multimodal Approach
> to Seismic Pavement Testing. J. Geotech. Geoenviron. Eng. 130, 636–645.
> https://doi.org/10.1061/(ASCE)1090-0241(2004)130:6(636)

> Xia, J., Xu, Y., Miller, R.D., 2007. Generating an Image of Dispersive Energy
> by Frequency Decomposition and Slant Stacking. Pure appl. geophys. 164,
> 941–956. https://doi.org/10.1007/s00024-007-0204-9
