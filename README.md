# Salvaged ferrite cores characterization

## Measure and compute
 **Take measurements of the core**
See [Jupyter notebook](FerriteCore.ipynb)

## Theory

There are ferrite cores (classic) and there are iron powder cores.
It seems that typical ferrite manufacturers are
[Fair-Rite](http://www.fair-rite.com)<br/>
[Amidon](http://www.amidoncorp.com)

**For poweder cores**

[Micrometals](http://www.micrometals.com)<br/>
[Ferroxcube (Yageo)](http://www.yageo.com)<br/>
[Magnetics](http://www.mag-inc.com)


**Advantages of using a ferrite core inductor**

* The magnetic field is magnified, and we can make an inductor with fewer turns leading to reduced copper losses.
* The magnetic field is constrained to the ferrite core, thus reducing interference with close-by components and circuits.

**Disadvantages of ferrite core inductors**

* Core saturation can be a problem. A magnetic flux density of 0.4T brings saturation losses. Newer material like nanocrystaline have magnetic flux density of 1.2T 
* The upper operating frequency is limited due to other (eddy current) core losses.
* Temperature drift causes inductance change and can alter how a tuned filter might perform.

Not very relevant for DIY winding, but different materials has different Curie Temperature point. Once exceeded, ferrite permanently loses it's magnetic properties.

**Manganese Zinc Ferrite (MnZn)**

Ideal for applications with an operating frequency of less than 5MHz. The impedance of these cores makes them suitable for inductors up to 70 MHz.

MnZn material is conductive i.e. can scrape the coating off and measure conductivity with a multimeter. If there are a reading - it is the best indicator that the core is MnZn ferrite.
MnZn has very high permutability, mu_initial in the range 1 .. 10k. Compare with a typical NiZn ferrites 50-800.

**Nickel Zinc Ferrite (NiZn)** 

Used in applications where frequencies range from 2MHz to several hundred MHz. NiZn is considered ideal for inductors above 70 MHz
NiZn saturate at double Field Strength in comparison of MnZn 


For low current - you want high permeability cores to keep dimensions small and number of
widings low. As current gets higher and higher ferrite cores start to saturate. To prevent saturation you need fewer turns or smaller permeability. Fewer turns means smaller inductance. There is also resistive losses in the windings, too many turns that are needed to get target inductance might be too much resistance. You can increase the wire gauge, but then wires might not dimensionally fit into the toroid hole. You can do multiple layers, now stray capacitance shoots up and toroid inductor has self resonance frequnecy at lower and lower frequencies. At self resonance inductor looks like an open circuit.

As temperature goes up ferite loses permeability (i.e. inductance goes down), bad for RF filters


# Interpreting S11 measurement from NanoVNA

* Option #1 - use https://scikit-rf.readthedocs.io/en/latest/
* Option #2 - DIY, see examples here https://pa3a.nl/wp-content/uploads/2022/07/Math-for-nanoVNA-S2Z-and-Z2S-Jul-2021.pdf


## Interesting findings

Fixture leads add capacitance, compare measurements [FerriteCore-core4-fixtureA](FerriteCore-core4-fixtureA.ipynb) vs [FerriteCore-core4-fixtureB](FerriteCore-core4-fixtureB.ipynb). Due to crocodile clamps LC circtuit (2 loops over toroid + stray capacitance between loops + stray capacitance between clamps) move resonant frequency lower. When Z plot starts to dive really vertically - it's self resonant frequency. The whole circuit looks like an open circuit at this point.

https://www.everythingrf.com/community/what-is-self-resonant-frequency



## References

https://owenduffy.net/blog/?p=16124
