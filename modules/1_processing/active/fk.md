# Frequency-Wavenumber Transform

> Joseph P. Vantassel, The University of Texas at Austin

## Basic Concept

The frequency-wavenumber (f-k) approach as applied to 1D arrays is typically
attributed to Gabriels et al. (1987), however it is important to point out that
Gabriels et al. (1987) were using a simplification of the frequency-wavenumber
approach developed by Nolet and Panza (1976) for 2D arrays. Note that whether
the f-k approach is actually the earliest depends on whether you attribute its
development to Nolet and Panza (1976) or Gabriels et al. (1987). As in the later
case it could be argued that the slant-stack by McMechan and Yedlin (1981) was
the earliest. Regardless, the f-k approach is one of earliest methods developed
for processing 1D array data to produce estimates of surface wave dispersion.
The f-k approach in application is quite simple as it only involves
transforming the data from the time-distance domain _u(x,t)_ to the
frequency-wavenumber domain _U(f,k)_. This is typically accomplished with two
Fourier Transforms. The first to transform time to frequency and the second to
transform distance to wavenumber. This is further simplified, in recent years
with nearly all modern programming languages including a fast and user-friendly
implementation of a 2D Fast Fourier Transform (FFT), which avoids even the
complexity of performing 2 - 1D FFTs. However, the two notable disadvantages of
using a 2D FFT (and not a more custom implementation) is that (1) it cannot be
easily extended to arrays with non-equal spacing and (2) cannot readily be used
to develop dispersion estimates above the [array resolution limit](https://github.com/jpvantassel/sw-course/blob/master/modules/0_acquisition/array_res_1d.md). However, these disadvantages are small in comparison to the
ease with which a 2D FFT can be implemented in nearly all modern programing
languages.

## References

> Gabriels, P., Snieder, R., Nolet, G., 1987. In situ measurements of
> shear-wave velocity in sediments with higher-mode rayleigh waves. Geophys
> Prospect 35, 187–196. https://doi.org/10.1111/j.1365-2478.1987.tb00812.x

> McMechan, G.A., Yedlin, M.J., 1981. Analysis of dispersive waves by wave field
> transformation. GEOPHYSICS 46, 869–874. https://doi.org/10.1190/1.1441225

> Nolet, G., Panza, G.F., 1976. Array analysis of seismic surface waves: Limits
> and possibilities. PAGEOPH 114, 775–790. https://doi.org/10.1007/BF00875787
