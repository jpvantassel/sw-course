# Slant-Stack Transform

> Joseph P. Vantassel, The University of Texas at Austin

## Basic Concept

The Slant-Stack Transform also known as the τ-p or ω-p Transform was proposed
by McMechan and Yedlin (1981). The Slant-Stack Transformation converts
data from the time-distance domain to the circular frequency-slowness domain.
As slowness is the inverse of velocity, we can equivalently consider
the transform to be between the time-distance to the linear frequency-velocity
domain without any loss of generality. The Slant-Stack's key advantage over
previous methods is that it did not require manual picking or windowing to
produce estimates of surface wave phase velocity. By doing so, the
Slant-Stack is one of, if not the, earliest of the wavefield transformations
which could produce automatic estimates of surface wave dispersion. Note it is
arguable that the Frequency-Wavenumber (f-k) Transform predates the Slant-Stack
Transform, however this depends on whether you consider the origins of the f-k
transform to originate with the work of Nolet and Panza (1976) where they first
applied the f-k approach to 2D arrays or to Gabriels et al. (1987) where the
f-k approach of Nolet and Panza (1976) was applied to 1D arrays. The Slant-Stack
Transform has been utilized in a number of studies since its development
as a basis for comparison of new approaches (e.g., Park et al. 1998) and as a
starting point for subsequent extension (e.g., Louie 2001).

## Mathematical Details

The Slant-Stack Transform involves a relatively simple two-step process:

1. First, somewhat confusingly, the time-distance data _u(x,t)_ is transformed
to the τ-p domain _u(p,τ)_ using a slant-stack transformation. This is somewhat confusing
because a slant-stack, which is a common operation in geophysics, is the first
step, but not the only step, of the Slant-Stack Transform used to developed
experimental dispersion data. The slant-stack operation is represented
mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=u(p, \tau )=\int_{}^{} u(x, t=\tau+px) dx">

2. Second, the τ-p domain _u(p,τ)_ data is transformed to the ω-p domain
_u(p,ω)_ using the Fourier transform. This is represented mathematically as:

<img src="https://render.githubusercontent.com/render/math?math=u(p, \omega)=\int_{}^{} e^{-i \omega \tau} u(p, \tau) d\tau">

## Implementation

The Slant-Stack Transform can be implemented in several simple steps:

1. A range of trial velocities (or equivalently slownesses) are selected. Care
must be taken to ensure the minimum trial velocity (or maximum slowness) is not
too small (or large). A reasonable minimum would 75 m/s, however this should be
modified to correspond to the anticipated site conditions.

2. Perform the slant-stack operation (i.e., integrate across the traces
following the _t=τ+px_ line). Note that this will involve two nested `for`
loops. The outer `for` loop iterates over the trial values of _p_ from step 1,
and an inner `for` loop which iterates over the trial values of _τ_. Note that
the trial values of _τ_ is defined using the time step of the experimental data
and the minimum trial velocity (or maximum trial slowness). _Note when
performing the slant-stack Louie (2001) recommends performing linear
interpolation between time domain samples._ The result of this stage will be a
2D tensor (i.e., matrix) corresponding to every _τ_-_p_ pair.

3. Apply the Fast Fourier Transform (FFT) with respect to _τ_ to the result of
step 2 to produce a new 2D tensor corresponding to every _ω_-_p_ pair
(or equivalently _f_-_v_ pair).

4. Normalize the matrix either at each frequency (recommended) or across all
frequencies.

5. Plot the matrix as a 2D image (e.g., phase velocity with respect to
frequency).

6. Peaks in the 2D image can be used to estimate the dispersive properties of
the site's fundamental and (in some cases) higher surface wave modes.

## References

> Gabriels, P., Snieder, R., Nolet, G., 1987. In situ measurements of
> shear-wave velocity in sediments with higher-mode rayleigh waves. Geophys
> Prospect 35, 187–196. https://doi.org/10.1111/j.1365-2478.1987.tb00812.x

> Louie, J.N., 2001. Faster, Better: Shear-Wave Velocity to 100 Meters Depth
> from Refraction Microtremor Arrays. Bulletin of the Seismological Society of
> America 91, 347–364. https://doi.org/10.1785/0120000098

> McMechan, G.A., Yedlin, M.J., 1981. Analysis of dispersive waves by wave field
> transformation. GEOPHYSICS 46, 869–874. https://doi.org/10.1190/1.1441225

> Nolet, G., Panza, G.F., 1976. Array analysis of seismic surface waves: Limits
> and possibilities. PAGEOPH 114, 775–790. https://doi.org/10.1007/BF00875787

> Park, C.B., Miller, R.D., Xia, J., 1998. Imaging dispersion curves of surface
> waves on multi‐channel record, in: SEG Technical Program Expanded Abstracts
> 1998. Presented at the SEG Technical Program Expanded Abstracts 1998, Society
> of Exploration Geophysicists, pp. 1377–1380. https://doi.org/10.1190/1.1820161
