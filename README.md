# Model-Shift
The Kepler DR25 Model-Shift runs a suite of planet vetting tests to detect false positives due to systematic noise, seconday eclipses, odd/even eclipse differences, asymmetric transit shape, transit depth variations, and non-planetary shapes. It uses the photometric light curve data along with a best-fit transit model to esentially find the best-fit depth of the transit model at every phase and produce a high-SNR convolved light curve. Using the measured depths from this light curve, the suite of tests are performed.


## Compiling and Running the Code

The DR25 Robovetter code is provided, along with a sample input data file and a sample output plot.

### Prerequisites

The code is written in C++11 and only requires the standard C++ library (specifically, the required libraries are iomainip, iostream, fstream, algorithim, and sstream). It has been tested to work with the g++ compiler, but should work with any standard C++ compiler with the -std=c++11 option.

### Compiling

To compile the code, use your available C++ compiler with the -std=c++11 option, and a recommended O2 level of optimization. For example:

```
g++ -std=c++11 -Wno-unused-result -O3 -o modshift -O modshift.cpp
```

### Running

To run Model-Shift, provide it the following arguments, in order:

- A text file that has three columns: Time, Flux, and Modeled Flux. See 006307521-01.txt as an example (KOI 1126.01).
- A name that will form the basename of the output file.
- A name that will be used in the plot to identify the object.
- The period of the object in the same time units as provided in the input file (usually Days).
- The epoch of the object in the same time units as provided in the input file (usually Days).
- A variable to produce the corresponding plot. 1 will produce a plot. 0 (or anything besides 1) will not produce a plot.

For example, for DR25 TCE 006307521-01 (i.e., KOI 1126.01):

```
./modshift 006307521-01.txt 006307521-01 KOI-1126.01 29.744936 157.388555 1
```

will run modshift and produce the included example plot, 006307521-01.pdf.



