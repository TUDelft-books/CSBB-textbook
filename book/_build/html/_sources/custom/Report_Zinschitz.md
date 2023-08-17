# Report: Final Assignment NB2211 - colorimeter 

# ![Diagram Description automatically generated](media/image1.png){width="5.3384142607174105in" height="4.276332020997375in"}Zinschitz Verena No. 5240794** **

# 

# Contents {#contents .TOC-Heading}

[Report: Final Assignment EI -- colorimeter
[1](#report-final-assignment-nb2211---colorimeter)](#report-final-assignment-nb2211---colorimeter)

[Introduction: [3](#introduction)](#introduction)

[General setup: [3](#general-setup)](#general-setup)

[Reaction 1 -- extinction coefficient measurement of red food dye:
[3](#reaction-1-extinction-coefficient-measurement-of-red-food-dye)](#reaction-1-extinction-coefficient-measurement-of-red-food-dye)

[Reaction 2 -- measurement of pH change in exothermic acid-base
reaction:
[4](#reaction-2-measurement-of-ph-change-in-exothermic-acid-base-reaction)](#reaction-2-measurement-of-ph-change-in-exothermic-acid-base-reaction)

[Integrated setup: [6](#integrated-setup)](#integrated-setup)

[Electronics: [8](#electronics)](#electronics)

[LED current provider:
[8](#led-current-provider)](#led-current-provider)

[Light sensing circuit
[8](#light-sensing-circuit)](#light-sensing-circuit)

[Temperature sensing circuit
[9](#temperature-sensing-circuit)](#temperature-sensing-circuit)

[General: noise reduction
[9](#general-noise-reduction)](#general-noise-reduction)

[Python code: [10](#python-code)](#python-code)

[Experiment 1: [10](#experiment-1)](#experiment-1)

[Experiment 2: [11](#experiment-2)](#experiment-2)

[Results: [11](#results)](#results)

[Experiment 1: [11](#experiment-1-1)](#experiment-1-1)

[Experiment 2: [12](#experiment-2-1)](#experiment-2-1)

[Part 2 -- pH change over time:
[14](#part-2-ph-change-over-time)](#part-2-ph-change-over-time)

[Discussion: [15](#discussion)](#discussion)

[Experiment 1: [15](#experiment-1-2)](#experiment-1-2)

[Experiment 2: [16](#experiment-2-2)](#experiment-2-2)

[Conclusion: [17](#conclusion)](#conclusion)

[Appendix: further setup pictures
[19](#appendix-further-setup-pictures-for-assignments)](#appendix-further-setup-pictures-for-assignments)

## Introduction:

A colorimeter is a device used to measure the absorbance of a certain
colour (wavelength) of light of a sample. A simple colorimeter can be
built from basic circuit components. Such a setup will be explored in
this report. Further, the colorimeter is then used for calculating the
extinction coefficient of red food colouring, as well as live pH
measurements of an acid-base reaction.

## General setup:

### Reaction 1 -- extinction coefficient measurement of red food dye:

For this experiment the objective was to determine the extinction
coefficient of red food dye for the colours red, blue, and green. This
would be done by measuring absorption at different concentrations of the
food dye, and then using the Beer-Lambert law
$I_{c} = I_{b}e^{- C\epsilon d}$, which $\epsilon$ the extinction
coefficient, $I_{c}\ $the measured intensity through sample of
concentration $C$, $I_{b}$ the baseline intensity and $d$ the path
length of the light.

The setup was as follows[^1]:

A LED rgb was connected to the Cria output pins, with current regulated
by a current regulator based on a transistor and comparator. The LED
lights can be regulated via python code on a connected notebook. Each
colour was turned on for 500 measurements in the order red, blue, green.
The intensity of light was measured when passing through air, an empty
cuvette, a water filled cuvette, a cuvette with sample concentration of
1.25µM, one of 2.5µM and finally of 5µM. Measurement took place via a
light-sensitive photodiode, which produces a current in response to
light. That current was converted to voltage via a converter circuit and
amplified before being processed digitally in a jupyter notebook.

After acquisition of the readings, an average intensity was taken per
colour and concentration. Average absorbance per colour was plotted
against concentration. This data was then used to manually compute the
extinction coefficients.

![Diagram, schematic Description automatically
generated](media/image2.png){width="3.625in"
height="2.879166666666667in"}Dilutions of the sample were obtained by
diluting 2ml of the 5µM sample with 2ml water, and repeating this
process with 2mL of the resulting 2.5µM to get the third 1.25µM sample
concentration.

### Reaction 2 -- measurement of pH change in exothermic acid-base reaction:

The second reaction was to monitor the change in pH for an exothermic
acid-base reaction. The reaction itself consisted of mixing solutions of
bicarbonate of soda (NaHCO3, 84g/mol) and citric acid (C6H8O7,
192.124g/mol). This reaction proceeds as follows:

H3C6H5O7(aq)+3NaHCO3(aq)→Na3C6H5O7(aq)+3H2O(l)+3CO2(g)

This reaction is exothermic and results in sodium citrate (in aqueous
solution), H2O and CO2. The latter forms a gas which leaves the solution
once formed, leading to intense bubbling. This limited the
concentrations and amounts of solution which could be used for the
reaction, as overflowing of the used cuvettes could have cause damage to
the electronic circuitry. After several trials, I settled on a mixture
of 2mL water and 0.5mL 10% NaHCO3, to which 0.5mL 10% C6H8O7 was added
(percentages in weight). This allowed for a strongly visible reaction
without excessive bubbling.

Bicarbonate of soda (also known as baking soda) is a base (pKa = 6.34)
while citric acid is acidic (pKa1 = 3.13, pKa2 = 4.76, pKa3 = 6.39).
Upon reaction therefore, the total pH of the mixture should be different
from either solution alone. Further, I hypothesized that mixture should
be the most acidic right after combining the two chemicals, and then
drop to a more basic pH over time. This last assumption was based on the
fact that CO2 is in itself acidic -- therefore, evaporation of CO2 from
the mixture should -- in theory - lead to a rising pH.

To follows the pH of the solutions, a pH-indicator was obtained by
boiling 50g of chopped red cabbage in about 200mL of water, which after
straining left me with a dark purple mixture. When combining with an
acid, the pigment anthocyanin present in red cabbage turns red, while
becoming a blue colour after combining with a base. The solutions of
citric acid and baking soda where then obtained by dissolving 1g of the
respective substance in 9mL of the indicator liquid, leading to two 10%
solutions.

Part 1 of the experiment consisted of live measurements of the reaction
described above, to see short term changes in pH. To monitor the
reaction, I decided to implement a temperature sensor, which would use a
live plotting feature to provide information about the heat released,
and therefore the progress of the reaction. Further, measurement of
temperature ensures that the measured change in pH is indeed due to the
correct reaction, which is known to be strongly exothermic, and not any
other reactions accidentally taking place.

The change in pH was monitored by the change of the solutions colour
upon combining the liquids, using the same basic setup as for
measurement of the extinction coefficient above. However, instead of
subsequently measuring short time intervals of each colour, the
experiment was instead repeated 3 times, once for each colour. The data
was then stored and processed via Python code to produce graphs, showing
the change in light intensity over time.

Part 2 of the experiment was to see whether, with time, the solution
would indeed adopt a slightly more basic pH. For this, two cuvettes were
measured shortly after and several hours after initial reaction. These
measurements were obtained by a single round of light intensity
measurements for rgb as in experiment 1. The readings were then plotted
against time and average intensities calculated for each colour and
time. Further, photos were taken for visual references. The measurements
at different timepoints were then compared to judge whether a change in
pH had taken place.

![](media/image3.png){width="6.591062992125984in"
height="2.1909722222222223in"}![](media/image4.png){width="6.591062992125984in"
height="2.1909722222222223in"}![Diagram, schematic Description
automatically generated](media/image7.png){width="5.336111111111111in"
height="5.895138888888889in"}

###  Integrated setup[^2]: 

The previously mentioned reaction setups were implemented into a
colorimeter as seen in the picture below:

![Diagram Description automatically
generated](media/image8.png){width="6.3in" height="4.784027777777778in"}

Figure\
Completed setup of the measurement device/colorimeter

To prevent noise pollution as much as possible, the measuring process
took place in a box, which was tightly sealed by putting an ipad on top.
This was effective in eliminating background light from influencing the
results.

For experiment 2, the iPad cover could not be used, as the two solutions
needed to be combined during active measurement. Instead, a cardboard
cover was used to seal the chamber. A small 3x3mm hole was cut into the
top, which could be used to deliver the citric acid solution into the
cuvette while in a dark box. Measurements showed that the introduction
of the hole did not lead to increased noise pollution of the
measurements.

##  

## ![](media/image9.png){width="6.490277777777778in" height="2.1493055555555554in"}![](media/image10.png){width="6.490277777777778in" height="2.1493055555555554in"}![](media/image13.png){width="6.598611111111111in" height="4.764583333333333in"}![](media/image14.png){width="6.598611111111111in" height="4.764583333333333in"}![](media/image15.png){width="6.598611111111111in" height="4.764583333333333in"}![](media/image16.png){width="6.598611111111111in" height="4.764583333333333in"} Electronics[^3]:

The electronics used for this project can be split into 3 parts:

### LED current provider:

For providing each of the subparts of the light emitting diode (LED)
with the ideal current, a system of a transistor amplifier was used for
current regulation.

From the DAC-A pin on the Alpaca a constant voltage of DC = 2.2V was
supplied to a current divider made up of two resistors (10kΩ and 3.3kΩ)
was used to supply a voltage of 0.546V to the non-inverting input of the
comparator. The inverting input then matched that voltage and led it
over a 39Ω resister at the emitter of the transistor. This led to a 14mA
current to be supplied to the LEDs. Latter were subsequently turned on
by the respective Dout pins on the Cria, controlled by Python code (see
attachment).

![Diagram, schematic Description automatically
generated](media/image22.png){width="5.842760279965004in"
height="3.3277712160979878in"}

Figure7\
Use of transistor/amplifier current regulation for the LEDs was achieved
by connecting the two components in series and utilizing negative
feedback.

*Following components were used*[^4]*:\
Opamp LM358P; transistor 2N3904; LEDrgb; resistors 000039, 001000,
003300, 010000*

### Light sensing circuit

For picking up the light after passing through the medium a
light-sensitive photodiode was used. The resulting current was converted
into voltage by a current-voltage converter based around a OPAMP. The
current was input into the inverting input, which was also connected to
the output voltage of the amplifier. Due to the noninverting input being
grounded a virtual ground point was created, leading to a voltage
through the feedback resistor and thus to Vout, where the value of the
Voltage can be obtained by $V_{out} = I_{led} \cdot R_{f}$ -- hence gain
is regulated by the resistor value. After some initial trials a
capacitor with C=220nF was added to the circuit for noise reduction.

Using a 10kΩ resistor for limiting the output current, the output is
connected to the signal+ pin of the AMP0, and this inbuild amplifier in
the alpaca was used with a gain of 10 (offset = 0, attenuation = 0) to
supply a voltage directly the the Ain0 pin of the Cria.

![Schematic Description automatically generated with medium
confidence](media/image23.png){width="6.3in"
height="2.4784722222222224in"}

Figure8\
Light-sensing circuit, build using a photodiode and comparator with
negative feedback.

*Following components were used:\
Opamp LM358P; photodiode; resistors 010000 (2x); capacitor 220nF*

### Temperature sensing circuit

For live measurement of experiment temperature, a simple connection
between a temperature sensor and the AMP1 signal+ pin on the Alpaca was
established. The sensor was powered by +5V and connected to ground. The
output was passed through the inbuilt amplifier of the Aplaca (gain = 2,
offset = 0, attenuation = 0) directly to the Cria.

![Diagram Description automatically
generated](media/image24.png){width="3.8438429571303585in"
height="2.271900699912511in"}

Figure 9\
Temperature sensing circuit using a sensor connected to the built-in
amplifier of the Alpaca

*Following components were used:\
LM35 temperature sensor*

### General: noise reduction

To reduce noise following measurements were taken:

-   The length of connection and use of additional cables was reduced as
    much as possible. For example, in the light sensing circuit, the
    feedback resistor was connected directly through the breadboard with
    one pin to the inverting input and the other to the output. That way
    the need for connecting jumpers was eliminated. Additional cables
    are very sensitive to noise interference from the surroundings and
    can be a major source of signal error. This was greatly reduced by
    taking away some cables

-   To further prevent interference from other components, jumpers
    carrying output information were twisted with grounded jumpers or
    those with currents flowing in the opposite direction (s.a. -12V
    supply) to create a shielding effect. This was deployed for the
    jumpers

```{=html}
<!-- -->
```
-   *Temp sensor output to AMP1 Signal +* twisted with *Scope ground to
    AMP1 ground*

-   *Vout amplifier light sensing circuit from 10kOhm resistor to AMP0
    signal+* and *Scope ground to AMP1 ground*

```{=html}
<!-- -->
```
-   A capacitor was connected in parallel to the negative feedback
    resistor of the light-sensing circuit. Such a capacitor can help
    short-circuit high, noise-producing frequencies, preventing them
    from influencing the measured signal. In Figure 10, you will find
    the data for signal measured with and without the capacitor present.

![Chart, histogram Description automatically
generated](media/image25.png){width="6.3in"
height="2.3243055555555556in"}

Figure\
Background measurements of closed black box (cardboard on top) with the
capacitor (left) and without the capacitor (right). A strong reduction
in noise is seen upon introduction of the capacitor, most prominent in
the blue colour measurement (colours from left to right: red, green,
blue)

Further, background light was filtered out by the previously described
setup of a "black box" in which the measurements were taken.

## Python code[^5]:

### Experiment 1:

For experiment 1 the code was adapted from Notebook
"3_Basic_Circuit_Photodiode" as provided through Vocareum folder "Final
Assignment".

The code was changed for use with the transistor current regulator.
Further, I have decided to automate the measuring in such a way that the
6 cycles of 1500 measurements now take place in succession, separated by
enough time to change the cuvettes. This allows for saving all
measurements together in a single matrix, which makes it easier to
process the data.

Due to issues with retrieving such a matrix via Python 3 at the time of
measurement, the graph of average absorbance per colour against
concentration was instead plotted directly using the Alpaca.

The final approximate extinction coefficients were computed by hand from
the obtained data.

### Experiment 2:

For this a piece of code was written that would monitor the real time
change in temperature while the reaction was underway, using the alpaca
live plotting feature.

First, the background measurements were again obtained via an adapted
form of the code from notebook "3_Basic_Circuit_Photodiode", adjusted
for use with the current regulator.

For the measurement of intensity as a function of time as the reaction
proceeded, I used code to live plot the reaction temperature while
saving measurements of the intensity ever 0.2s. This code needs to be
manually interrupted to stop measuring. This allows for greater freedom
in deciding the time range over which measurements are taken. The
obtained samples where then stored and retrieved in Python 3 for
plotting purposes. A plot of voltage from the light measuring circuit
against time was used to assess the pH change in the reaction.

Unfortunately, the reaction was not exothermic enough to create
necessary heat for detection by the temperature sensor, making this part
of the circuitry obsolete. However, much time was spent on this circuit,
and I believe that for more exothermic reactions, or with the reaction
taking place at a larger scale, this method would've been very useful.
As thus, I decided to leave this part in the coding and circuitry.

## Results:

### Experiment 1:

This measurement was repeated in its entirety two times.

![Chart, line chart Description automatically
generated](media/image26.png){width="4.340277777777778in"
height="2.8333333333333335in"}The first time, mislabelling of the
solutions led to unplausible results, as shown in Figure 11. From these
measurements, a proper extinction coefficient could not be obtained.

The second measurement was done after fixing the issues in
measurement 1. The results of absorption against concentration are
plotted in Figure 12

![Chart, line chart Description automatically
generated](media/image27.png){width="6.3in"
height="2.9055555555555554in"}

Figure\
Measurement 2 of absorption of the 3 colours against concentration.
X-Axis: concentration in M; y-Axis: Absorbance; Graph colours correspond
to the respective rgb colour.

Absorbance was calculated by the code using
$A = log\left( \frac{I_{0}}{I} \right)$ with I~0~ and I representing the
intensity of a baseline water measurement and the intensity value at
$c = 5 \cdot 10^{- 6}\mu M$ respectively.

The absorbance coefficients where then obtained by hand, using a
pathlength of 1cm and the absorbance value at
$c = 5 \cdot 10^{- 6}\mu M$ (see figure 11). The final results are:

-   Extinction coefficient for red: $\epsilon = 0{\ M}^{- 1}cm^{- 1}$

-   Extinction coefficient for green:
    $\epsilon = 30\ 000{\ M}^{- 1}cm^{- 1}$

-   Extinction coefficient for blue:
    $\epsilon = 90\ 000{\ M}^{- 1}cm^{- 1}$\#

Note that while the graph does show that we have a linear trend, the
measurements do not result in a perfectly linear outcome. This is most
likely due to several factors: For one, the solutions where diluted via
hand using 1mL single-use pipets, making it very likely that the
concentrations are not exactly as wished; Reflections of light or
adjustment of relative positions of LEDs, photodiodes, and jumpers, can
all lead to noise in the measurements, altering the readings; Finally,
imperfect sealing could have lead to additional light entering the box,
explaining for example the seemingly negative absorbance for red light
at 2.5µM.

### Experiment 2:

#### Part 1: active reaction monitoring:

The first part of experiment 2 was to see how the absorption of the rgb
colours, indicative of the pH change of the reaction, would change over
time. Reaction process was supposed to be measured via a live plotting
of data received by a temperature sensor. While this sensor worked for
sensing temperature when tested with freshly boiled water in the cuvette
(see figure 2), for the actual reaction no significant temperature
changes could be measured during the reaction:

![Chart, line chart Description automatically
generated](media/image28.png){width="5.375in"
height="3.861111111111111in"}

Figure\
Live plot of temperature change during the reaction on a range from 55s
to 80s after measurement start. Note that the y-Axis, which represents
the temperature, is off by a factor of 2. However, as only relative
changes are needed to monitor the reaction this is not an issue.

![](media/image29.png){width="5.847222222222222in"
height="4.596527777777778in"}![](media/image30.png){width="5.847222222222222in"
height="4.596527777777778in"}![](media/image31.png){width="5.847222222222222in"
height="4.596527777777778in"}The reaction was conducted 3 times, once
for each colour. The intensities of light reaching the LED are as
follows:

All three graphs show strong, sudden changes in Intensity at about 10s
after the start of the measurement, which is the time at which the acid
was added to the cuvette. Further, we see that the intensities continued
to change during the time of measurement, with a trend towards a value
closer to their initial intensities.

Unfortunately, the graph for the colour red is very noisy -- still, an
overall trend can be determined from the graph.

#### Part 2 -- pH change over time:

Part two consisted of taking measurements of the absorption at greater
intervals after the reaction, to observe whether changes in pH continued
due to evaporation of CO2 from the liquid. On the first day, absorbance
of the colours was measured on 2 cuvettes 5 and 70 min after reaction
resp.\
The average absorbance values for cuvette 2 (5 min. after reaction)
were: 0.41 (red), 0.14 (green), 0.66 (blue)\
The average absorbance values for cuvette 1 (70 min. after reaction)
were: 0.38 (red), 0.19 (green), 0.68 (blue)

Photos were taken of these two cuvettes and a freshly reacted one about
15 mins after these measurements.

![](media/image35.jpeg){width="6.2875in"
height="4.569444444444445in"}![](media/image36.png){width="6.2875in"
height="4.569444444444445in"}![](media/image37.png){width="6.2875in"
height="4.569444444444445in"}

The cuvettes were again measured for rgb absorbance 20h (cuvette 1) and
21h (cuvette 2) after their initial measurements. A photo was further
taken next to a freshly reacted sample.

The average absorbance values for cuvette 2 (20h after reaction) were:
0.41 (red), 0.23 (green), 0.65 (blue)\
The average absorbance values for cuvette 1 (21h after reaction) were:
0.32 (red), 0.29 (green), 0.70 (blue)

The average change in absorbance for cuvette 2 over 20 hours was: 0%
(red), +64% (green), -1.5% (blue)\
The average absorbance values for cuvette 1 (21h after reaction) were:
-15.8% (red), +52.6% (green), +2.9% (blue)

![](media/image41.png){width="6.631944444444445in"
height="4.456944444444445in"}![](media/image42.png){width="6.631944444444445in"
height="4.456944444444445in"}![](media/image43.jpeg){width="6.631944444444445in"
height="4.456944444444445in"}

## Discussion:

### Experiment 1:

In experiment 1 the extinction coefficients of the red food dye were
successfully obtained for the three colours red, green, and blue
($\epsilon = 0{\ M}^{- 1}cm^{- 1}$, $\epsilon = 30k{\ M}^{- 1}cm^{- 1}$
and $\epsilon = 90k{\ M}^{- 1}cm^{- 1}$ resp.)

We can see that the differences in extinction coefficient are quite
large between the individual colours. More precisely, while red does not
seem to be absorbed at all, blue has a very large extinction
coefficient, while green lies somewhere in the middle ground. However,
these results were expected following the theory of light in Physics.
Blue and red light present two opposite ends of the visible light
spectrum, with blue having the shorter and red the longer wavelengths,
while green lies in between. When blue light gets absorbed, the
wavelengths most dominant to detection will be those at the opposite end
of the spectrum, thus red light. On the other hand, if red were to be
the dominant absorbed colour, we would mainly detect blue. This can be
observed in nature by the fact that the oceans seem to be blue, and red
light is not visible starting a few meters deep into the water, due to
prevalent absorption of red light by the bonds of H~2~O molecules.

Conversely, if the colour of a sample is red that must mean that red is
not absorbed by the sample. This is reflected in the fact that the
extinction coefficient, a measure of absorbance, is 0 for the red light.
The fact that a red sample absorbs most of the blue light is represented
by a very high extinction coefficient for blue. Hence, the results for
our extinction coefficients, with blues the highest and red the lowest,
seem quite plausible.

However, the extinction coefficients of both blue and green are still
lower than was expected (around $\epsilon = 150k{\ M}^{- 1}cm^{- 1}$).
This is most likely due to reflections of the light from the LED inside
the box, which will lead some light to arrive at the photodiode without
passing through the cuvette. The amount of this light can vary between
measurements, leading to differences in relative intensity of received
light. A more accurate setup would therefore be to have a narrow canal
the width of the cuvette around the led, cuvette and photodiode, to
prevent the presence of stray light which can influence the measurement.

### Experiment 2:

#### Part 1:

As mentioned earlier, the temperature monitoring of part 1 in experiment
2 unfortunately failed. This is most likely due to the reaction not
producing enough heat to be sensed by the temperature sensor, which
worked well in control measurements with bigger changes in temperature.
A way to fix this error without influencing absorbance (as direct
immersion of the sensor into the liquid would), might be to use higher
concentrations of reactants, or larger amount of reaction fluid.
Unfortunately, both options where not viable for in this case, due to
limited sizes of the cuvettes and the fact that higher concentrations of
reactants would have led to stronger bubbling and overflowing of the
liquid, possible damaging the electronics. However, this is definitely
something to be explored when repeating this experiment, as temperature
sensing is a way to not only follow the reaction, but also make sure
that the right reaction is being measured.

For the change in intensity detected during the reaction, we can see
that initially, detection of red is very low (ca. 0.125V), while that of
blue and green is at 0.72V and 0.4V respectively. This is supported by
the fact that the initial fluid consists of a mixture of water and
bicarbonate of soda, leading to a basic pH, which is represented by a
blue colour using the red cabbage juice as pH indicator, as described
above.

At about 10s, which is the time of addition of citric acid, the change
in colour from blue to red (reflecting a change from basic to acidic pH)
is reflected by a fall in intensity of blue and green light, and a
strong rise in intensity of red light measured. This, again, corresponds
to colour theory in physics. Further, as proposed, as the reaction
continued the intensities seemed to slightly revert towards their
original values. This trend was most strongly seen for blue, although we
can observe it in green and red as well. This reflects the gradual
colour change as CO2, a by-product of the reaction, leaves the fluid,
leading to an increase in pH of the overall sample, and thus to a colour
shift towards a bluer tone (a purplish - pink). The long-term effects of
this CO2 evaporation are monitored in part 2 of this experiment.

Unfortunately, from the graphs it is visible that noise for these
reactions was quite high, especially when measuring the experiment under
red light. Other than system noise, the fact that the solutions where
bubbling led to disturbances in the measurement. This bubbling was
extremely prominent in the last reaction (red), which we can see has a
lot of noise as a result. However, I have decided to keep these results
as they are still able to show the overall trend in intensity, and
further visualize quite well issues and challenges encountered doing
these measurements.

While not something that was done in this experiment, data concerning
the change in pH during the reaction can be useful in determining factor
such as reaction and particularly CO2 evaporation speed and the
influence of relative substance concentrations on the former.
Unfortunately, due to previously mentioned issues of inability to vary
substrate concentrations without posing danger to the electronics (as
well as time restraints), this was left to future investigations.

Finally, I also want to note that the use of regular (not distilled)
water, as well as (impure) juice of a supermarket vegetable, means that
there are possibly several side reactions going on, influencing the
results

#### Part 2:

Part 2 of this experiment focused on whether CO2 evaporation from and
thus continued reaction within the substance was taking place over a
longer period of time (here:19 hours). Both samples measured show a
significant change in intensity of green light between the two time
points, while slight changes are also present for the other colours.
This indicates a change in colour of the samples. This change can also
be observed by the naked eye, when comparing the colours of the samples.
Especially for cuvette 1 we see a strong shift towards a darker purple
colour. However, cuvette 2 also showed a slight shift towards purple.
This indicates that indeed, there is a reaction continuing inside the
cuvettes which leads to slow change in acidity over time. The samples
where still bubbling lightly after 20 hours, meaning that CO2 was still
produced. Hence, it is very likely that this colour change was due to
the ongoing reaction and not environmental influences. This is further
supported by the fact that colour change ceased after this time, and
monitoring was stopped after 5 days of constant pH.

However, what is to be noted is the strong difference in colour between
cuvette 1 and cuvette 2. There seems to be a disparity in pH, even
though the same chemicals at the same concentrations were used. I
propose that this is due to human error when handling the reaction.
Oversaturation of Baking soda in the solution led to precipitation of
solid crystals. Hence, the mixture was not homogenous and had to be
shaken by hand before every use. It is possible that when preparing
cuvette 1 a sample with denser concentration was taken from the original
solution, leading to the overall more basic pH. Further, due to the
strong nature of the reactants a slight inaccuracy in relative amounts
of substance could have also led to differences in pH.

## Conclusion:

In conclusion, we have shown that indeed, a reaction of baking soda and
citric acid can be monitored by a colorimeter with the use of a
pH-indicator. Further, it was shown that this reaction continues even
after initial mixing. This was prominent for the first minute (s)
immediately after reaction, but also noticeable 20 hours later.

We have also successfully found the extinction coefficients for red food
colouring for red, green, and blue LED light.

In general, construction of the colorimeter worked well with the
provided components, after some initial problems with properly setting
the gain and reducing noise to the current level were solved. In the end
however, a functioning colorimeter useful for simple home experiments
was obtained. This colorimeter can be controlled via the PicoPi Alpaca
setup.

## Appendix: further setup pictures (for assignments)

![A picture containing text, electronics Description automatically
generated](media/image47.jpeg){width="6.252083333333333in"
height="5.013194444444444in"}

![Chart Description automatically
generated](media/image48.png){width="4.103472222222222in"
height="2.6972222222222224in"}Figure\
open setup, in colour, with visible electronics (assignment 3b)

![](media/image49.jpeg){width="4.217391732283464in"
height="3.163043525809274in"}

![A picture containing text Description automatically
generated](media/image50.jpeg){width="4.217361111111111in"
height="3.163020559930009in"}Figure\
Weighted cardboard closed box with hole, used for Part 1 of Experiment 2

[^1]: For precise information on electronics, see the "Electronics"
    section. For information on the coding, refer to the provided
    jupyter notebook.

[^2]: Further pictures of the (covered and uncovered) setup can be found
    in the Appendix, additionally to the basic light tightness test

[^3]: For a photo of the electronics, please refer to the appendix
    figure 18

[^4]: For more precise information on components consult provided "Parts
    list1"

[^5]: For full code with comments look at the further uploads for this
    report
