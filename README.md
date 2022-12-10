# Salvaged ferrite cores characterization

## Measure and compute
 **Take measurements of the bead with VNA**


* Callibrate the VNA with the testing fixture
* Setup the bead in the testing fixture
* Notice that there 3 ways of doing it - see [youtube link](https://www.youtube.com/watch?v=1UbEz73FGCU)

<img src="three-methods.png" width="400">

Pick the one that gives you the least amount of measurement error

<img src="three-methods-error.png" width="400">

* Run nano-VNA, record measurements into *.s1p file (Touchstone file format)
* Use the Jupyter notebook for processing and plotting
* Use the bead in it's resistive (green) region

See [Jupyter notebook](./FerriteBeadCharacterization.ipynb)

## Theory
**Ferrite bead response characteristics**

Ferrite beads are categorized by three response regions: inductive,
resistive, and capacitive. These regions can be determined by
looking at a ZRX plot, where Z is the impedance, R is the
resistance, and X is the reactance of the bead. To reduce high
frequency noise, the bead must be in the resistive region; this is
especially desirable for electromagnetic interference (EMI) filtering
applications. The component acts like a resistor, which impedes
the high frequency noise and dissipates it as heat. The resistive
region occurs after the bead crossover frequency (X = R) and up
to the point where the bead becomes
capacitive. This capacitive point occurs at the frequency where
the absolute value of capacitive reactance is equivalent to R.

<img src="bead-characteristics.png" width="400">

## References

https://owenduffy.net/blog/?p=16124
