# Salvaged ferrite cores characterization

Notice that these measurements are for HF only. My VNA does not go below 50kHz.
For power applications in SMPS, these calculations are ok as they operate at 100kHz-1MHz
For power applications at 50/60Hz these can't be used.

## Measure and compute

 **Take measurements of the core**

See [Jupyter notebook](FerriteCore-core4-fixtureA.ipynb)

See [Jupyter notebook](FerriteCore-core4-fixtureB.ipynb)

See [Jupyter notebook](FerriteCore-core5.ipynb)

See [Jupyter notebook](inductor-sweep.ipynb)

## Theory

There are ferrite cores (classic) and there are iron powder cores.
It seems that typical ferrite manufacturers are
[Fair-Rite](http://www.fair-rite.com)<br/>
[Amidon](http://www.amidoncorp.com)

**For powder cores**

[Micrometals](http://www.micrometals.com)<br/>
[Ferroxcube (Yageo)](http://www.yageo.com)<br/>
[Magnetics](http://www.mag-inc.com)


**Advantages of using a ferrite core inductor**

* The magnetic field is magnified, and we can make an inductor with fewer turns leading to reduced copper losses.
* The magnetic field is constrained to the ferrite core, thus reducing interference with close-by components and circuits.

**Disadvantages of ferrite core inductors**

* Core saturation can be a problem. A magnetic flux density of 0.4T brings saturation losses. Newer materials like nanocrystalline have the magnetic flux density of 1.2T 
* The upper operating frequency is limited due to other (eddy current) core losses.
* Temperature drift causes inductance change and can alter how a tuned filter might perform.

Not very relevant for DIY winding, but different materials have different Curie Temperature points. Once exceeded, ferrite permanently loses its magnetic properties.

**Manganese Zinc Ferrite (MnZn)**

Ideal for applications with an operating frequency of less than 5MHz. The impedance of these cores makes them suitable for inductors up to 70 MHz.

MnZn material is conductive i.e. can scrape the coating off and measure conductivity with a multimeter. If there is a reading - it is the best indicator that the core is MnZn ferrite.
MnZn has very high permutability, mu_initial in the range 1 .. 10k. Compare with a typical NiZn ferrites 50-800.

**Nickel Zinc Ferrite (NiZn)** 

Used in applications where frequencies range from 2MHz to several hundred MHz. NiZn is considered ideal for inductors above 70 MHz
NiZn saturates at double Field Strength in comparison to MnZn 


For low current - you want high permeability cores to keep dimensions small and the number of turns low. As the current gets higher and higher ferrite cores start to saturate. To prevent saturation you need fewer turns or smaller permeability. Fewer turns mean smaller inductance. There are also resistive losses in the windings, too many turns that are needed to get target inductance might be too much resistance. You can increase the wire gauge, but then wires might not dimensionally fit into the toroid hole. You can do multiple layers, now stray capacitance shoots up and the toroid inductor has a self-resonance frequency at lower and lower frequencies. At the self-resonance frequency, the inductor looks like an open circuit.
As the temperature goes up ferrite loses permeability (i.e. inductance goes down), bad for RF filters

**Powdered Iron cores**

If you need temp stability, or lower loss or higher current till saturation you might trade give ferrite cores high permeability (i.e. fewer loops needed for the same inductance) and go with powdered iron cores. These are the "classical" cores.

Interestingly, due to lower losses, Powdered Iron cores have a much higher Q factor (150-250). See [Iron_Powder_Cores_for_High_Q_Inductors](Iron_Powder_Cores_for_High_Q_Inductors.pdf)
Good thing to have for a “narrow-band” circuit - a filter, a tuned transformer, and an oscillator. Another application is flux-coupled RF transformers that transfer high power (>100 watts) through the core, to minimize loss and heating. 

This is not the case with coax chokes, or transmission-line transformers, the power stays in the cable and does not travel through the core. Common mode power travel on the outside of the coax braid and the high impedance of the core is important so ferrite cores are better there.

(In transmitting chokes made of coaxial cable wound on a core—a transmission-line transformer—the power stays in the cable and does not travel through the core. High impedance is the most important thing, so ferrite cores are used here.)


www.micrometals.com calls these materials "RADIO FREQUENCY IRON POWDER"

* Carbonyl Iron formulations.
* Ideal for High Q applications from 0.1 to 700 MHz including radio communications, video communication and broadband transformers
* Permeabilities from 1 to 35

-2, -4, -6 & -7 Powdered Iron materials: These are the most popular carbonyl iron mixes. They will provide high Q up to 40 MHz and (are) the most popular for amateur radio and variety of other communication applications. They are also useful for moderate band (width) transformers in the 200 to 400 MHz frequency range.

‐10 & ‐17 Powdered Iron materials: These materials are the highest frequency carbonyl irons. They will provide high Q up to 150 MHz and are a popular material for cable television applications. They will produce moderate band transformers covering 400 to 700 MHz.

https://www.onallbands.com/powdered-iron-cores-how-do-they-compare-to-ferrite/


# Interpreting S11 measurement from NanoVNA

* Option #1 - use https://scikit-rf.readthedocs.io/en/latest/
* Option #2 - DIY, see examples here https://pa3a.nl/wp-content/uploads/2022/07/Math-for-nanoVNA-S2Z-and-Z2S-Jul-2021.pdf


## Interesting findings

Fixture leads add capacitance, compare measurements [FerriteCore-core4-fixtureA](FerriteCore-core4-fixtureA.ipynb) vs [FerriteCore-core4-fixtureB](FerriteCore-core4-fixtureB.ipynb). Due to crocodile clamps LC circuit (2 loops over toroid + stray capacitance between loops + stray capacitance between clamps) move the resonant frequency lower. When the Z plot starts to dive vertically - it's the self-resonant frequency. The whole circuit looks like an open circuit at this point.





https://www.everythingrf.com/community/what-is-self-resonant-frequency



## References

https://owenduffy.net/blog/?p=16124


## Other notes

Rule of thumb for RFC chokes - present at least 500Ohm impedance at the lowest freq of operations. For a step-by-step approach to selecting an RF choke, use these steps:

1. Make sure the DC current capability matches the required bias current.
1. Select a sufficiently high inductance value. (Z = 2 * pi * f * L) Select an impedance (Z) that is much larger than the load resistance. 
1. Decide the maximum allowable DC resistance so that the voltage drop on the inductor is small compared to the voltage swing of the amplifier stage.  A resistance of between 1 and 10 Ohms is usually OK.
1. Select a small package size.
1. Look for a low Q inductor (High L and small physical size usually means Low Q).
1. Make sure the core material is useable in the frequency range of interest. 

---

Three general rules about the use of ferrites as chokes. 

1.  More impedance is better.
2.  All ferrite chokes should be designed to operate in the frequency range where their series equivalent resistance is large and their series equivalent reactance is small. 
3.  These conditions are satisfied at or near the choke's resonant frequency. We do this by selecting a suitable material, core size, and number of turns. These rules apply to both single turn and multi-turn chokes, and they apply to chokes (but not transformers) used for transmitting as well. 

--- 

* For a typical RFC choke on the collector pin of a BJT, its inductance is in mH range, like ~1mH or so.

* For ferrite beads - the longer the bead (dimensionally), the greater the impedance

* A classic text (Soft Ferrites, Properties and Applications, by E. C. Snelling, published in 1969), shows that 
... for any given material, the smaller the core, the higher will be the frequency of this resonance,
and to a first approximation, the resonant frequency will double if the core dimension is halved.

* For frequencies below resonance, inductance follows almost linearly N^2 ratio of turns to the inductance value

* We see that µ varies with frequency and is complex, yet those who don't understand this often use a single number for µ. When a single number for µ is quoted, it is
the value of µ at frequencies well below resonance, where losses are small and the graph of impedance is a straight line increasing linearly with frequency. 

* There are two resonant freq for a ferrite inductor (choke), the first is trivial LC, the second is dimensional - standing wave in the ferrite. Second resonant freq is in Ghz range for a typical rf choke

* When you look at the datasheet plots of RS, XL, and Z for a standard ferrite part, you are looking at the series equivalent parameters of their
dominant resonance. For most MnZn materials, it is dimensional resonance, while, for most NiZn materials, it is circuit resonance. 


