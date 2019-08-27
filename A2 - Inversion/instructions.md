# Surface-Wave Inversion

>Joseph Vantassel, University of Texas at Austin

## Purpose

The purpose of this assignment is for you gain practice performing
surface-wave inversions using a common inversion algorithm. The inversion
algorithm which you are going to use is called the Neighborhood Algorithm. It
was developed by Sambridge (1999a) and implemented in a C++ framework by
Wathelet (2004; 2005; 2008). The software is open-source and freely available
from [geopsy.org](http://www.geopsy.org)

## Assignment Instructions

1. Download and install, the latest release of geopsy (see link above).
2. Run the program dinver, and load the provided file `siteA.txt` in as a target using the graphical user interface.
3. Decide on an appropriate parameterization using the dispersion data as a guide.
4. Run 20k trial models set Ns0=10000, It=100, and Ns=100. (Note that for real data you will likely want to run between 100k - 150k models by increasing It and Ns).
5. Repeat this process 3 times, comment on the differences between the runs.
6. View and plot the best model(s) and provide an estimate (can be qualitative) of their uncertainty.
7. Repeat steps 2-6 for the other site's provided, if no uncertainty in the experimental data is provided assume a coefficient of variation (COV) of 0.05.
