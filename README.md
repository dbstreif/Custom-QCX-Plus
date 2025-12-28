# Custom-QCX-Plus
QRP Labs QCX+ 5W CW Radio Transceiver modified for 15m band (21MHz) frequency range. This project includes Custom Frontplate/Backplate parametric part designs, and specs/calculations for inductance and capacitance values for the transformer and low pass filter.


## Motivation
When I first began building this kit from QRP Labs, I was only a Technician Class Operator. This meant that if I wanted to get on the air and communicate globally via ionospheric propagation, I had to choose a high frequency (HF) band that I could legally transmit on. I also was restricted to only Morse Code operation on said bands, which meant that the QCX+ was the lowest barrier of entry to the world of HF and long-range communication. Now as a General Class Operator, I have more operating privileges; yet I find myself fascinated with the most pure form of radio communication, the continuous wave.

My operating band options at the time came down to 40m and 15m. The reason being, firstly, I would most likely use an end fed half wave antenna for my usual portable operation, and anything greater than a 20m antenna is quite long for all intensive purposes; and secondly, I was resitricted to operating on certain bands and in-band frequency ranges. I decided that the 15m band would be best fit for me as it would give me a real design constraint, and challenge me to learn electrical principles. Also, a 15m half wave is only 7.5m, which is a small enough antenna to be portable and easily deployable.


## QCX+ Limitations
160m is not possible on the QCX+ due to crystal characteristics and 10m would introduce significant phase tuning challenges as the imaging algorithm used to display phase tuning metrics would be quite finnicky near the edges of the local oscillator range. The QCX family uses an Si5351A clock generator to create the required quadrature local oscillator (LO) signals for its direct-conversion receiver. The Si5351A can only produce two outputs with a 90deg quadrature phase difference down to about 3.2MHz. This sets the lower frequency limit for the QCX design to operate in the 80m band. The other challenge with operating at the LO edges is the phase noise introduced. When the output frequency is far from the VCO center, high divider ratios are used. At the edges, CW notes may sound unclean or raspy, weak signals might smear together, and it wouldn't be a great experience.

Here is the [datasheet](https://cdn-shop.adafruit.com/datasheets/Si5351.pdf) for the Si5351A.


## Repository Items
This repository contains a variety of different projects and calculations related to this project. Firstly, it contains inductance and capacitance values needed for proper harmonic rejection during the low pass filter stage. Secondly, it describes my thought processes and reflections of this journey, including reasoning about the [seven element Chebyshev Pi LC Low Pass Filter](https://en.wikipedia.org/wiki/Chebyshev_filter). Lastly, it includes my FreeCad parametric part designs for the Frontplate and Backplate of the custom case I built. As for the body and top, I give credit to oe7mbt for designing these. Though, because they were not designed parametrically (at least I think based on some inaccuracies), I faced problems with screw-hole alignment. You can find his creation [here](https://www.printables.com/model/65299-qrp-labs-qcx-plus-housing/files).


## Frontplate and Backplate
Here are some images of my part designs. The corner holes have countersinks so that M2.5 countersunk screws could sit flush against the plates. These plates were printed in PLA by my brother's Creality Ender-3 S1 Plus. We had just set up [Moonraker](https://moonraker.readthedocs.io/en/latest/) and [Klipper](https://github.com/Klipper3d/klipper) before printing this project, which made monitoring and adjusting print parameters really convenient.

![frontplate](https://github.com/dbstreif/Custom-QCX-Plus/blob/main/assets/frontplate.png "STL Slice Frontplate Preview")
![backplate](https://github.com/dbstreif/Custom-QCX-Plus/blob/main/assets/backplate.png "STL Slice Backplate Preview")
![front](https://github.com/dbstreif/Custom-QCX-Plus/blob/main/assets/front.jpg "QCX+ Front Preview")
![back](https://github.com/dbstreif/Custom-QCX-Plus/blob/main/assets/back.jpg "QCX+ Back Preview")
![power](https://github.com/dbstreif/Custom-QCX-Plus/blob/main/assets/power.jpg "QCX+ Powered On Preview")


## Low Pass Filter Behavior
Tuning the LPF is crucial in order to maximize peak power envelope power (PEP) on transmission. On the first transmit test, the QCX+ was barely outputting 1.02W of power. After playing around with the characteristic inductance and impedance the toroidal inductors, I was able to increase output power to 3.24W with a 12V power supply. A significant increase, and close to optimal. Now the QCX+ is advertised to output around 5W PEP, however with a 12V power supply around 4W is considered maximal. If I decide to switch to a 13.8V power supply at some point, I could easily squeeze out an extra 2W. Though, I want to keep heat dissipation of the final stage power transistor low as my case is made of low polymer plastic after all.

The PEP was calculated using the Root Mean Square Voltage (RMS) PEP variant Formula: $P_{\mathrm{PEP}} = \frac{V_{\mathrm{RMS,\,peak}}^{2}}{R}$

Han's Summers uses the Omega system shortcut (8R) as we measure $V_{PP}$ using an oscope: $P_{\mathrm{PEP}} = \frac{V_{\mathrm{pp}}^{2}}{400}$

I wanted to share something interesting that I found interesting. When trying to increase inductance on L2 by "bunching up" the coil on the toroid significantly, I found that I had accidentally introduced stray capacitance and other noise. Even though output power increased to around 4.1W, the LPF was unable to correctly reject harmonic frequencies. We can observe a "double" sine wave on the oscope. 

![oscope](https://github.com/dbstreif/Custom-QCX-Plus/blob/main/assets/lpf_optim_behavior.JPEG "LPF Optimization Interesting Behavior")

By spacing the coil turns again, I was able to restore one clean frequency transmission or sine wave if you will. Though final tuned output power was 3.24W. I'm sure that if I were to add some turns on L2, I would have been able to squeeze more output power, however I thought that it was too much of a hassle to rewind the inductor and felt satisfied with my results.


## Conclusion
I learned a lot from this project. I have been so excited by it, that I am considering pursuing a Master's in Electrical Engineering. I find the world of RF absolutely magical and have grown a lot through this experience.
