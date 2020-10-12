# Frequency-Domain Beamformer

> Joseph P. Vantassel, The University of Texas at Austin

## Basic Concept

To whom exactly the idea of beamforming should be attributed remains unclear
to the author at the time of writing. However, the earliest application of
frequency-domain beamforming in geophysics is typically attributed to Capon
(1969) with his development of a high-resolution frequency-wavenumber approach
for analyzing data from two-dimensional surface arrays. The work to apply and
improve frequency-domain beamforming for use with 1D arrays can be attributed
to a number of researchers including Gabriels et al. (1967), Zywicki (1999),
and Zywicki and Rix (2005). The basic concept of beamforming is rather
simple. A time-domain recording made on a number of receivers can be understood
to be composed of signal and noise. The purpose of beamforming is to combine the
time-domain recordings in such a way as to maximize the signal and minimize the
noise. For computational efficiency this process is performed in the frequency
domain, hence the name frequency-domain beamforming. The process of beamforming
involves: systematically guessing trial velocity vectors (i.e., steering
vectors), calculating their inner product with the stations' frequency-domain
representation, and summing the result. After beamforming a given array, the
frequency-velocity pairs with the largest relative amplitude indicate the
frequency-velocity pairs composing the signal.

## Mathematical Details

Frequency-domain beamforming involves a multi-step process:

1. The time-domain signals _s(x,t)_ are transformed into the frequency
domain using the Fourier Transform. This is represented mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=S(x,w)=\int_{}^{} s(x,t)e^{i2 \pi ft} dt">

2. We use the frequency-domain representation of the signal, _S(x,w)_,
to compute the spatiospectral correlation matrix. This is represented
mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=R(\omega) =  SS^{H}">

where the superscript _H_ denotes the Hermitian transpose of the vector _S_.

Note, that _R_ is a three-dimensional tensor
`(# sensor, # sensor, # frequencies)` that will generally be complex valued.

3. We now beamform the spatiospectral correlation matrix by performing the
inner product between our trial vector _e_ and spatiospectral correlation
matrix at each frequency.

<img src="https://render.githubusercontent.com/render/math?math=P(\omega, k) =  e^{H} R e">

## Implementation Details

There are two additional details worth discussing with respect to the use of
the frequency-domain beamformer for performing MASW. The first is the
application of sensor specific amplitude weighting. The weighting can be applied
at any point in the process, however it is typically applied immediately after
frequency-domain transformation (before the dimensionality increases) or during
the beamforming itself. In practice, users typical use either no weight (this
produces the same results as the FK transform (Gabriels et al. 1967)), inverse
amplitude weighting (this, as pointed out by Foti et al. (2015), produces the
same results as the phase-shift transform (Park et al. 1998)), or square root of
the receiver-source distance (this is the optimal weighting to compensate for
the cylindrical spreading of surface waves (Zywicki 1999)). The second
implementation detail worth discussing is the
functional form of the beamforming steering vector. Two options are used in
practice. They include a plane wave steering vector as used by all of the transforms
previously discussed (Gabriels et al. 1967; McMechan and Yedlin, 1981;
Park et al., 1998)
or the cylindrical wave vector which appropriately models the cylindrical spread
of surface-waves (Zywicki 1999; Zywicki and Rix 2004). As the cylindrical
steering verctor appropriately models the cylindrical spreading of surface
waves it should outperform its counterparts, particularly in the near-field
(i.e., offsets close to the recording array).

## References

> Foti, S., Lai, C., Rix, G.J., Strobbia, C., 2015. Surface Wave Methods for
> Near-Surface Site Characterization, 0 ed. CRC Press.
> https://doi.org/10.1201/b17268

> Gabriels, P., Snieder, R., Nolet, G., 1987. In situ measurements of
> shear-wave velocity in sediments with higher-mode rayleigh waves. Geophys
> Prospect 35, 187–196. https://doi.org/10.1111/j.1365-2478.1987.tb00812.x

> McMechan, G.A., Yedlin, M.J., 1981. Analysis of dispersive waves by wave field
> transformation. GEOPHYSICS 46, 869–874. https://doi.org/10.1190/1.1441225

> Park, C.B., Miller, R.D., Xia, J., 1998. Imaging dispersion curves of surface
> waves on multi‐channel record, in: SEG Technical Program Expanded Abstracts
> 1998. Presented at the SEG Technical Program Expanded Abstracts 1998, Society
> of Exploration Geophysicists, pp. 1377–1380. https://doi.org/10.1190/1.1820161

> Zywicki, D.J., 1999. Advanced Signal Processing Methods Applied to Engineering
> Analysis of Seismic Surface Waves. Georgia Institute of Technology, Atlanta,
> Georgia, United States.

> Zywicki, D.J., Rix, G.J., 2005. Mitigation of Near-Field Effects for Seismic
> Surface Wave Velocity Estimation with Cylindrical Beamformers. J. Geotech.
> Geoenviron. Eng. 131, 970–977.
> https://doi.org/10.1061/(ASCE)1090-0241(2005)131:8(970)
