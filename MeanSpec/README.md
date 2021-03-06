This directory contains all average spectra and standard deviation spectra of Stripped-Envelope SNe (SESN) from [Liu et al. (2016)](http://adsabs.harvard.edu/abs/2015arXiv151008049L), and [Modjaz et al. (2016)](http://adsabs.harvard.edu/abs/2015arXiv150907124M). Average spectra and standard deviation spectra can be used to quantify SN diversity, determine if a new transient is a novel type of explosion, and so on. See the README file in the folder for details of average spectra.


The average spectra are constructed using code from [Blondin & Tonry 2007](http://adsabs.harvard.edu/abs/2007ApJ...666.1024B) and from  [Liu et al. (2016)](http://adsabs.harvard.edu/abs/2015arXiv151008049L). 

#### Name Convention:

meanspec + <b>type</b> + <b>spectral inclusion method</b> + <b>phase</b> + <b>smoothing method</b>
- type: Ib (SN Ib), Ic (SN Ic), Icbroad (SN Ic-bl), Icbroad_nogrb (SN Ic-bl without GRB), Icbroad_withgrb (SN Ic-bl with GRB, or SN-GRB), cosmsngrb (high luminosity, cosmological SN-GRB), llsngrb (low luminosity SN-GRB)
- spectral inclusion method: presence of "1specperSN" means that only 1 spectrum per SN is included in an average spectrum for the required phase range, while absence of "1specperSN" means that all spectra of that SN within the required phase range are included in the average spectra.
- phase: in the rest-frame with respect to date of V band maximum light (includes spectra at +/- 2 days with respect to the target phase)
- smoothing method: presence of "ft" means that spectra are smoothed using FFT method from [Liu et al. (2016)](http://adsabs.harvard.edu/abs/2015arXiv151008049L) and [Modjaz et al. (2016)](http://adsabs.harvard.edu/abs/2015arXiv150907124M), while absence of "ft" means that spectra are smoothed using band-pass filter in [Blondin & Tonry 2007](http://adsabs.harvard.edu/abs/2007ApJ...666.1024B). The spectra of SNe Ic-bl and of SNe Ic (as presented in Modjaz et al. 2016) were smoothed by the FFT method.

#### Key Words:
- fmean: mean spectrum constructed using smoothed spectra
- fsdev: standard deviation of data
- fmed: median spectrum
- fmeanp: maximum positive excursion from mean
- fmeann: maximum negative excursion from mean
- fmedp: maximum positive excursion from median
- fmedn: maximum negative excursion from median
- wlog: rest wavelength
- nsn: number of spectra that were used to construct mean spectrum, at each wavelength bin
- smean: mean spline
- SNsave: SN names and phases of the spectra that were used to construct mean spectrum
- tmin: minimum phase
- tmax: maximum phase

#### Examples 

In IDL:
```
IDL> restore, 'meanspecIc_1specperSN_0.sav'
IDL> plot, wlog, fmean
IDL> oplot, wlog, fmean + fsdev
IDL> oplot, wlog, fmean - fsdev
```
In Python:
```
from scipy.io.idl import readsav
import pylab as pl
s = readsav('meanspecIc_1specperSN_0.sav')
pl.fill_between(s.wlog, s.fmean + s.fsdev, s.fmean - s.fsdev, color = 'k', alpha = 0.5)
pl.plot(s.wlog, s.fmean, label="mean Ic phase = 0", color="DarkGreen", lw=2)
pl.ylabel(r"relative flux", fontsize = 18)
pl.xlabel(r"Rest Wavelength $\AA$", fontsize = 18)
pl.legend(fontsize = 18)
pl.savefig("AverageIcPhase0.png")
```

which will generate the following figure

![alt tag](https://raw.githubusercontent.com/nyusngroup/SESNtemple/master/MeanSpec/MeanIcPhase0.png)
