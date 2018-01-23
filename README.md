# Model-Shift
The Kepler DR25 Model-Shift runs a suite of planet vetting tests to detect false positives due to systematic noise, seconday eclipses, odd/even eclipse differences, asymmetric transit shape, transit depth variations, and non-planetary shapes. It uses the photometric light curve data along with a best-fit transit model to esentially find the best-fit depth of the transit model at every phase and produce a high-SNR convolved light curve. Using the measured depths from this light curve, the suite of tests are performed and results outputted to the command line, with a plot displaying the results, light curves, and events optionally produced.

A detailed description can be found starting on page 23 of the DR25 TCERT Vetting Reports description document (http://adsabs.harvard.edu/abs/2017ksci.rept...15C) as well as section A.3.4 of The DR25 Catalog paper (Thompson et al. 2017; http://adsabs.harvard.edu/abs/2017arXiv171006758T).



## Compiling and Running the Code

The DR25 Robovetter code is provided, along with a sample input data file and a sample output plot.

### Prerequisites

The code is written in C++11 and only requires the standard C++ library (specifically, the required libraries are iomainip, iostream, fstream, algorithim, and sstream). It has been tested to work with the g++ compiler, but should work with any standard C++ compiler with the -std=c++11 option.

There is an option to produce a PDF plot that graphically shows the results of Model-Shift. This option requires that Gnuplot (http://www.gnuplot.info/) be installed on your system, and includes the 'pdfcairo' terminal option.


### Compiling

To compile the code, use your available C++ compiler with the -std=c++11 option, and a recommended O2 level of optimization. For example:

```
g++ -std=c++11 -Wno-unused-result -O3 -o modshift -O modshift.cpp
```

### Running

To run Model-Shift, provide it the following arguments, in order:

- A text file that has three columns: Time, Flux, and Modeled Flux. See 006307521-01.txt as an example (KOI 1126.01).
- A name that will form the basename of the output file and be output to the command line.
- A name that will be used in the plot to identify the object.
- The period of the object in the same time units as provided in the input file (usually Days).
- The epoch of the object in the same time units as provided in the input file (usually Days).
- A variable to produce the corresponding plot. A value of "1" will produce a plot. A value of "0" (or anything besides "1") will not produce a plot.

For example, for DR25 TCE 006307521-01 (i.e., KOI 1126.01), one would run

```
./modshift 006307521-01.txt 006307521-01 KOI-1126.01 29.744936 157.388555 1
```

to run Model-Shift, print results to the standard output / command line, and produce the included example plot, 006307521-01-modshift.pdf, with a given period of 29.744936 days and an epoch of 157.388555 BKJD. The printed results are as follows (and can be redirected to a file via the standard ">" operator in linux/unix/mac):

- The given input basename.
- The significane of the primary event.
- The significance of the second deepest (secondary) event.
- The significance of the third deepest (tertiary) event.
- The significance of the most postive flux event.
- The significance of the odd/even test.
- The result of the depth mean-to-median ratio test.
- The result of the shape test.
- The significance of the asymmetry test.
- The threshold at which any event is considered to be significant when taking into account the measured systematic noise level.
- The threshold at which the differenec in signifcnce between two events is considered to be significant when taking into account the measured systematic noise level.
- The measured ratio of the systematic "red" noise at the duration of the transit compared to the "white" noise.
- The measured phase of the primary event.
- The measured phase of the secondary event.
- The measured phase of the tertiary event.
- The measured phase of the positive event.
- The measured depth of the secondary event.
- The error in the measured depth of the secondary event.

In the above example, the output should be:

```
006307521-01 74.8408874699 16.6389529120 4.0169529566 4.4924498316 0.2712002206 1.0595297919 0.0702039832  0.5052345164 4.7983653500 2.1444960914 1.8802464536 0.0001730113 0.5031546113 -0.1912675518 0.2062202755 0.0001663586 0.0000099981
```


## Citing Model-Shift

If using Model-Shift, please cite the following papers:

http://adsabs.harvard.edu/abs/2017ksci.rept...15C

http://adsabs.harvard.edu/abs/2017arXiv171006758T


## Future Updates

Ideally this code would be re-written in Python (instead of as-is, poorly written in C++11), and I hope to do so one day. -Jeff

