

# Fuel-to-air ratio control under short-circuit conditions through UEGO sensor signal analysis

International J of Engine Research

1–7

© IMechE 2019

Article reuse guidelines:

sagepub.com/journals-permissions

DOI: 10.1177/1468087418820747

journals.sagepub.com/home/jer

![SAGE logo](d3102649f02e825ddb76dc3de0190154_img.jpg)

Carlos Guardiola<sup>1</sup>, Benjamín Pla<sup>1</sup> ![ORCID icon](4b7a79268f6ba26c1471d4232fffa85a_img.jpg), Marcelo Real<sup>1</sup> ![ORCID icon](87d978583253c9bde1db2d6dfafe8de0_img.jpg), Cyril Travaillard<sup>2</sup> and Frederic Dambricourt<sup>2</sup>

## Abstract

The impact of short-circuit pulses on the after-treatment system of a spark-ignited engine must be taken into account to keep the fuel-to-air equivalence ratio within the three-way catalyst window, thereby reducing pollutant emissions. The fuel-to-air equivalence ratio overestimation that suffers the wide-range  $\lambda$ -sensor upstream three-way catalyst in the presence of short circuit is especially relevant. In this study, a novel approach to deal with the fuel-to-air equivalence ratio control under short-circuit conditions is introduced. Under this scope, this work proposes a strategy for the on-board correction of the aforementioned fuel-to-air equivalence ratio overestimation, by means of the information regarding short-circuit level that provides the frequency content of the  $\lambda$ -sensor at the engine frequency. Finally, the potential of this approach to minimize pollutant emissions, in particular the  $\text{NO}_x$  penalty arisen as a consequence of running the engine under leaner conditions than expected, is assessed through experimental tests.

## Keywords

Spark-ignited engine, fuel-to-air ratio control, three-way catalyst, short circuit, emission control

Date received: 14 February 2018; accepted: 27 November 2018

## Introduction

With the popularization of small turbocharged and spark-ignited (SI) engines, the low-end torque issues have grown in prominence in the last few years, and thus the use of scavenging strategies to increase torque at low engine speeds has been extended. The effect of fresh air short circuit (SC) on  $\lambda$ -sensor and three-way catalyst (TWC) performance is pointed out in the previous work of the authors.<sup>1</sup> In this article, the authors deal with the control of the fuel-to-air equivalence ratio (FAR) under SC conditions in order to minimize its negative impact on  $\text{NO}_x$  emissions. Note that little is published on this issue since SC is only actively used at low engine speed and high load conditions, which is a very particular operating area. Nevertheless, today it seems very convenient to address the issue of emission control under SC conditions due to the intensive use of small turbocharged engines that tend to work under these conditions more often.<sup>2–5</sup>

Typically, state-of-the-art engines have a wideband  $\lambda$ -sensor upstream and a switch-type  $\lambda$ -sensor downstream of the TWC. The second one is mainly used for two purposes: on-board diagnostics (OBD) and closed-

loop control under some operating conditions, mainly steady state. Due to the strong nonlinearity of that type of sensor, as well as to the storing dynamics of the TWC, the controller must be very slow. Otherwise, the action of the closed-loop control (downstream of the TWC) could cause FAR instabilities. Under transient conditions, the FAR disturbances caused by the different path of fresh air and fuel, like intake manifold dynamics, wall-wetting or SC, exceed the capabilities of the downstream closed-loop control.<sup>6,7</sup>

As it is well known, the closed-loop FAR control using the feedback provided by the wideband  $\lambda$ -sensor upstream of the TWC is the typical approach without SC, that is, in normal operation.<sup>8–18</sup> However, when a

<sup>1</sup>CMT-Motores Tèrmicos, Universitat Politècnica de València, Valencia, Spain

<sup>2</sup>PSA Peugeot Citroën, Paris, France

###### Corresponding author:

Marcelo Real, CMT-Motores Tèrmicos, Universitat Politècnica de València, Camino de Vera, s/n, 46022 Valencia, Spain.

Email: marreami@mot.upv.es

gasoline direct injection engine is operated under SC conditions, the FAR upstream TWC tends to be leaner as the percentage of SC increases (if in-cylinder FAR is kept stoichiometric), which is not acceptable from the pollutant emissions point of view, due to the behavior of the TWC ( $\text{NO}_x$  emissions under lean conditions). Thus, stoichiometric FAR at the TWC inlet is needed even under SC conditions. This means that in-cylinder FAR must be richer as SC increases in order to compensate for the fresh air pulses and getting stoichiometric FAR at the TWC inlet. The issue is that, under these conditions, the wideband  $\lambda$ -sensor upstream of the TWC tends to overestimate the FAR, which disables this sensor to provide a proper feedback for the closed-loop control. To take actions about FAR control under SC conditions and therefore to avoid negative effects on the after-treatment system, all the possible solutions pass through an estimation of the SC rate. Of course, if SC is known, the proper correction of the wide-range  $\lambda$ -sensor signal may be addressed in order to counteract its effect. One feasible choice goes through mapping the appropriate offset to increase the FAR provided by the  $\lambda$ -sensor depending on SC. Nevertheless, if SC is just mapped depending on the operating conditions, the success of such an approach relies on the accuracy of calibration and it is subjected to the impact of aging or any other disturbance, as it happens with all systems based on static calibrations. Controlling with a wideband  $\lambda$ -sensor downstream the TWC under SC conditions would be another possibility, since the catalyst filters the SC pulses. But then, the TWC dynamics and the effect of the exhaust gas composition downstream the catalyst on the  $\lambda$ -sensor must be taken into account.<sup>19</sup>

This article shows a brief review of the main SC effects on FAR control in section “Problem description.” Section “Experimental setup” describes the engine, test bench and the other facilities used. Next, section “The SC effect on  $\lambda$ -sensor” points out the SC effect on  $\lambda$ -sensor. Then, section “SC effect correction strategy” proposes a strategy for instantaneous on-board SC estimation, using the frequency content of the  $\lambda$ -sensor signal upstream TWC. The validation of the introduced strategy is carried out in section “Results and discussion.” Finally, section “Conclusion” summarizes the main contributions of this article.

## Problem description

The SC effect on the TWC of SI engines can be mainly explained as the superposition of two simultaneous phenomena, one of which is related to the  $\lambda$ -sensor and the other one is associated with the TWC, both quantitatively dependent on the SC amount. On the one hand,  $\lambda$ -sensor upstream catalyst tends to overestimate the actual FAR under SC conditions, presumably because of the impact on the in-cycle dynamics of exhaust gas composition generated by SC pulses.

On the other hand, the fact that in-cylinder FAR affects the generation of the main pollutant species, that is,  $\text{CO}$ ,  $\text{NO}_x$  and  $\text{HC}$ , leads to important changes in the exhaust gas concentration of these species at the TWC inlet, when stoichiometric FAR is imposed in the presence of SC. Under these circumstances, the TWC is forced to operate simultaneously with fresh air and residual gases, the composition of which is typical of rich combustion. In order to keep stoichiometric FAR at the TWC inlet with SC, a fairly rich FAR at the cylinder is necessary, which leads to high  $\text{HC}$  and  $\text{CO}$  emissions at the TWC inlet. Comparing to an operating point with the same FAR but without SC, the prime consequence of experimentally observed SC is the improvement of  $\text{NO}_x$  efficiency together with the decrease of  $\text{CO}$  oxidation capabilities. In this sense, the TWC window, that is, the optimal FAR range for TWC performance, is moved on to slightly leaner conditions.

Although the effects explained above behave in an opposite way, it is important to highlight that their consequences do not counteract themselves reciprocally as shown in Figure 1. In this figure, three different approaches have been implemented while making an SC swept. Light circles correspond to keeping constant the FAR provided by the  $\lambda$ -sensor ( $\text{FAR}_\lambda$ ); as SC increases,  $\lambda$ -sensor overestimates progressively the actual FAR and TWC operates under leaner conditions; the aftereffect is a noticeable increase in  $\text{NO}_x$  emissions. Dark circles display the consequence of

![Figure 1: Four stacked plots showing the effect of SC [%] on engine parameters. The x-axis for all plots is SC [%] from 0 to 7. The y-axes are: NOx emissions [ppm] (0 to 1500), CO emissions [ppm] (0 to 1500), FAR_GA [-] (0.97 to 1.03), and FAR_lambda [-] (1.01 to 1.02). The legend indicates three data series: Min. emissions (dark circles), ISO-FAR_GA (medium gray circles), and ISO-FAR_lambda (light gray circles).](1ac0e11d90bece49015adc89be472a39_img.jpg)

Figure 1 consists of four vertically stacked plots sharing a common x-axis representing the Short Circuit (SC) percentage from 0 to 7. The legend in the top plot identifies three data series: 'Min. emissions' (dark circles), 'ISO-FAR<sub>GA</sub>' (medium gray circles), and 'ISO-FAR<sub>λ</sub>' (light gray circles).  
 - Top plot: NO<sub>x</sub> emissions [ppm] vs SC [%]. The y-axis ranges from 0 to 1500. The 'Min. emissions' series (dark circles) remains near zero. The 'ISO-FAR<sub>GA</sub>' series (medium gray circles) also remains near zero. The 'ISO-FAR<sub>λ</sub>' series (light gray circles) shows a sharp increase, reaching approximately 1500 ppm at SC = 7%.

| SC [%] | Min. emissions | ISO-FAR <sub>GA</sub> | ISO-FAR <sub>λ</sub> |
|--------|----------------|-----------------------|----------------------|
| 0      | 0              | 0                     | 0                    |
| 1      | 0              | 0                     | 500                  |
| 2      | 0              | 0                     | 1000                 |
| 3      | 0              | 0                     | 1500                 |
| 4      | 0              | 0                     | 1500                 |
| 5      | 0              | 0                     | 1500                 |
| 6      | 0              | 0                     | 1500                 |
| 7      | 0              | 0                     | 1500                 |

- Second plot: CO emissions [ppm] vs SC [%]. The y-axis ranges from 0 to 1500. The 'Min. emissions' series (dark circles) remains near zero. The 'ISO-FAR<sub>GA</sub>' series (medium gray circles) shows a slight increase, reaching approximately 1000 ppm at SC = 7%. The 'ISO-FAR<sub>λ</sub>' series (light gray circles) remains near zero.

| SC [%] | Min. emissions | ISO-FAR <sub>GA</sub> | ISO-FAR <sub>λ</sub> |
|--------|----------------|-----------------------|----------------------|
| 0      | 0              | 0                     | 0                    |
| 1      | 0              | 0                     | 0                    |
| 2      | 0              | 0                     | 0                    |
| 3      | 0              | 0                     | 0                    |
| 4      | 0              | 0                     | 0                    |
| 5      | 0              | 0                     | 0                    |
| 6      | 0              | 0                     | 0                    |
| 7      | 0              | 1000                  | 0                    |

- Third plot: FAR<sub>GA</sub> [-] vs SC [%]. The y-axis ranges from 0.97 to 1.03. The 'Min. emissions' series (dark circles) shows a slight decrease from 0.99 to 0.985. The 'ISO-FAR<sub>GA</sub>' series (medium gray circles) shows a slight increase from 0.99 to 1.005. The 'ISO-FAR<sub>λ</sub>' series (light gray circles) shows a slight decrease from 0.99 to 0.985.

| SC [%] | Min. emissions | ISO-FAR <sub>GA</sub> | ISO-FAR <sub>λ</sub> |
|--------|----------------|-----------------------|----------------------|
| 0      | 0.99           | 0.99                  | 0.99                 |
| 1      | 0.99           | 0.99                  | 0.99                 |
| 2      | 0.99           | 0.99                  | 0.985                |
| 3      | 0.99           | 0.99                  | 0.985                |
| 4      | 0.985          | 0.995                 | 0.98                 |
| 5      | 0.985          | 0.995                 | 0.98                 |
| 6      | 0.985          | 1.005                 | 0.98                 |
| 7      | 0.985          | 1.005                 | 0.98                 |

- Fourth plot: FAR<sub>λ</sub> [-] vs SC [%]. The y-axis ranges from 1.01 to 1.02. The 'Min. emissions' series (dark circles) shows a slight increase from 1.01 to 1.015. The 'ISO-FAR<sub>GA</sub>' series (medium gray circles) shows a slight increase from 1.01 to 1.015. The 'ISO-FAR<sub>λ</sub>' series (light gray circles) shows a slight decrease from 1.01 to 1.005.

| SC [%] | Min. emissions | ISO-FAR <sub>GA</sub> | ISO-FAR <sub>λ</sub> |
|--------|----------------|-----------------------|----------------------|
| 0      | 1.01           | 1.01                  | 1.01                 |
| 1      | 1.01           | 1.01                  | 1.01                 |
| 2      | 1.01           | 1.01                  | 1.005                |
| 3      | 1.01           | 1.01                  | 1.005                |
| 4      | 1.015          | 1.015                 | 1.005                |
| 5      | 1.015          | 1.015                 | 1.005                |
| 6      | 1.015          | 1.015                 | 1.005                |
| 7      | 1.015          | 1.015                 | 1.005                |

Figure 1: Four stacked plots showing the effect of SC [%] on engine parameters. The x-axis for all plots is SC [%] from 0 to 7. The y-axes are: NOx emissions [ppm] (0 to 1500), CO emissions [ppm] (0 to 1500), FAR\_GA [-] (0.97 to 1.03), and FAR\_lambda [-] (1.01 to 1.02). The legend indicates three data series: Min. emissions (dark circles), ISO-FAR\_GA (medium gray circles), and ISO-FAR\_lambda (light gray circles).

**Figure 1.** The SC effect on  $\lambda$ -sensor and TWC window (from top to bottom:  $\text{NO}_x$  emissions;  $\text{CO}$  emissions; FAR provided by gas analyzer; FAR provided by  $\lambda$ -sensor).

**Table 1.** Engine setup.

|                      |                            |
|----------------------|----------------------------|
| Bore $\times$ stroke | 75 mm $\times$ 90.5 mm     |
| Number of cylinders  | 3                          |
| Total displacement   | 1199.9 cm <sup>3</sup>     |
| Compression ratio    | 10.5:1                     |
| Maximum power        | 96 kW at 5500 r/min        |
| Maximum torque       | 230 N m at 1750–3500 r/min |

keeping constant the FAR provided by the gas analyzer ( $FAR_{GA}$ ); the reductant species at the TWC inlet rises with the increase of in-cylinder FAR ( $FAR_{CYL}$ ), and thus the TWC window moves to leaner conditions and CO emissions increase with the SC raise. Finally, black circles are the result of imposing the optimum FAR in order to minimize the pollutant emissions (addition of CO and NO<sub>x</sub>), which means to operate with a FAR within the previous cases to compensate for both effects.

Under this scope, the online estimation of the instantaneous amount of SC could be really helpful to improve the FAR control. This article proposes an approach to deal with this issue with the focus on the pollutant emission reduction.

## Experimental setup

The engine is a state-of-art three-cylinder turbocharged gasoline direct injection (GDI) with a displacement of 1.2 L. Table 1 shows its main features.

Considering that TWC is the main element of the after-treatment system, it has been especially instrumented in order to measure pressure, temperature, gas composition and FAR with  $\lambda$ -sensors at the inlet and outlet. Two exhaust gas analysers, Horiba MEXA-ONE and Cambustion NDIR500 Fast CO and CO<sub>2</sub>, have been used to quantify the concentration of the different species. The main advantage of the latter is the sampling frequency that allows to capture transient evolutions besides steady measurements. An encoder is also used to synchronize these measurements with the crank angle. In addition, pressure and temperature sensors complete the engine instrumentation at the inlet and outlet of each element along intake and exhaust lines.

Since working in the presence of SC is not feasible in all the engine operating conditions, the selected point to carry out all the tests is 1750 r/min and 65% load, that is, one belonging to low engine speed and high load area. Under these conditions, the air mass flow and fuel consumption are 90 and 6.4 kg/h, respectively, while the engine provides a torque of 140 N m. In order to keep the TWC under its thermal limits, the SC applied ranges from 0% up to 10%. The nomenclature used hereinafter to refer to the different overlap levels is shown in Table 2.

The tracer gas method<sup>20–23</sup> has been used to experimentally quantify the air mass short-circuited,

**Table 2.** Predefined valve overlap levels.

| Valve overlap (°) | Waste gate (%) | Nomenclature | Measured SC rate (%) |
|-------------------|----------------|--------------|----------------------|
| -21               | 100            | a            | 0.0                  |
| 24.9              | 44             | b            | 0.8                  |
| 37.6              | 43             | c            | 1.9                  |
| 50.2              | 40.5           | d            | 3.7                  |
| 59.9              | 39             | e            | 5.6                  |
| 69.6              | 37.5           | f            | 7.5                  |
| 80.1              | 36             | g            | 9.5                  |

SC: short circuit.

![Figure 2: In-cycle averaged CO2 and lambda waveforms. The figure consists of two vertically stacked line plots. The top plot shows CO2 concentration in % on the y-axis (ranging from 10 to 14) against crank angle in degrees on the x-axis (ranging from 0 to 600). Three curves are shown: SCa (black), SCe (dark grey), and SCg (light grey). A grayscale bar on the right indicates SC values from 0 to 12%. The bottom plot shows the FAR_lambda signal on the y-axis (ranging from 0.96 to 1.02) against crank angle in degrees on the x-axis. The same three curves (SCa, SCe, SCg) are shown, with SCa being the highest and SCg the lowest. The curves show periodic fluctuations corresponding to the engine cycles.](ed14725db41dc9fb8e9460b1478f8366_img.jpg)

Figure 2: In-cycle averaged CO2 and lambda waveforms. The figure consists of two vertically stacked line plots. The top plot shows CO2 concentration in % on the y-axis (ranging from 10 to 14) against crank angle in degrees on the x-axis (ranging from 0 to 600). Three curves are shown: SCa (black), SCe (dark grey), and SCg (light grey). A grayscale bar on the right indicates SC values from 0 to 12%. The bottom plot shows the FAR\_lambda signal on the y-axis (ranging from 0.96 to 1.02) against crank angle in degrees on the x-axis. The same three curves (SCa, SCe, SCg) are shown, with SCa being the highest and SCg the lowest. The curves show periodic fluctuations corresponding to the engine cycles.

**Figure 2.** In-cycle averaged CO<sub>2</sub> and  $\lambda$  waveforms measured for each predefined SC.

particularly, the gas employed is CH<sub>4</sub>. From the methane measurements, SC is calculated as follows

$$SC = \frac{([CH_4]_{w/inj} - [CH_4]_{w/oinj})^{exh}}{([CH_4]_{w/inj} - [CH_4]_{w/oinj})^{int}}$$

where the term CH<sub>4</sub> refers to the methane concentration, the indexes w/inj and w/oinj represent the tests with and without methane injection, respectively, and the indexes int and exh stand for the engine intake and exhaust manifolds, respectively.

## The SC effect on $\lambda$ -sensor

Taking into account the sensitivity of the  $\lambda$ -sensor to the SC, this article proposes to analyze the  $\lambda$ -sensor signal in two different time scales to estimate both the FAR and the SC.

In this sense, Figure 1 shows the effect of the SC on the  $\lambda$ -sensor signal, while Figure 2 show that SC pulses involve a characteristic waveform in the  $\lambda$ -sensor signal during each engine cycle. The plot at the top of Figure 2 displays the SC effect on in-cycle raw CO<sub>2</sub> concentration, SC fresh air pulses tend to dilute the residual combustion gases, and therefore the average CO<sub>2</sub> concentration decreases with SC increase, causing the

![Figure 3: Engine instrumentation diagram. The diagram shows a schematic of an engine's exhaust system. Air enters through an AIR FILTER and undergoes [CH4] Injection. The exhaust then passes through a TWC (Three-Way Catalyst) and a Horiba MEXA-ONE exhaust gas analyser. A Wideband λ-sensor is positioned in the exhaust manifold. A CAC (Canister Control Actuator) is also shown. Various measurement points are indicated: [CH4] Exhaust measurement, [CO] & [CO2] measurements by a Fast Analyser, and [CH4] Intake measurement.](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

Figure 3: Engine instrumentation diagram. The diagram shows a schematic of an engine's exhaust system. Air enters through an AIR FILTER and undergoes [CH4] Injection. The exhaust then passes through a TWC (Three-Way Catalyst) and a Horiba MEXA-ONE exhaust gas analyser. A Wideband λ-sensor is positioned in the exhaust manifold. A CAC (Canister Control Actuator) is also shown. Various measurement points are indicated: [CH4] Exhaust measurement, [CO] & [CO2] measurements by a Fast Analyser, and [CH4] Intake measurement.

**Figure 3.** Engine instrumentation diagram.

appearance of a characteristic waveform because of the gases transport through the asymmetrical exhaust manifold (Figure 3). Similarly, the FAR provided by the  $\lambda$ -sensor at the exhaust (bottom plot) also presents a waveform when SC increases, but in this case the in-cycle average value is kept constant due to the SC effect on the sensor and the fact that a closed-loop control is carried out. Then, the  $\lambda$ -sensor signal content at the engine frequency may be used to estimate the SC, while the signal content at low frequencies provides a first estimation of the FAR that can be corrected with the value of SC and the relation shown in Figure 1.

## The SC effect correction strategy

The scheme of the proposed strategy is shown in Figure 4. With the  $\lambda$ -sensor signal, the amplitude of the frequency content at engine frequency ( $\hat{A}_{\lambda,f_0}$ ) can be calculated via discrete Fourier transform (DFT) as follows

$$\hat{A}_{\lambda,f_0} = |\text{DFT}_k(f_0)|_{k=1}^K \quad (1)$$

with

$$\text{DFT}_k(f_0) = \frac{2}{K} \sum_{n=1}^{N} \widehat{x}_n^k e^{-2\pi i f_0 \widehat{t}_n^k} \quad (2)$$

where  $f_0$  is the engine frequency,  $\widehat{x}_n^k$  is the element  $n$  in the  $\lambda$ -sensor signal window  $k$ ,  $N$  is the window size,  $p = N(1 - (\text{window overlapping } (\%)/100))$ ,  $L$  is the signal size,  $K$  is the number of windows ( $K = (L - N)/p$ ) and  $\widehat{t}_n^k$  is the element  $n$  in the time window  $k$ .

Note that the complete spectrum is not needed, and just the engine cycle harmonic must be calculated. The computational cost of the proposed method is not too demanding and its main advantage is that just a time-based sampling is needed. Of course, if the sampling in the crank angle domain is available, other approaches exist with even less computational demand for on-board DFT calculation as the one shown in Macián et al.<sup>24,25</sup> In such case, the DFT can be calculated in real

![Figure 4: The proposed strategy to avoid the SC effect on the FAR control. The diagram is a block diagram. At the top, a 'λ-sensor signal' is input to a 'FARλ' block. This signal also goes into a 'DFT' block, which shows a plot of amplitude vs frequency with a peak at f0. The output of the DFT is 'Aλ,f0'. This value is input to an 'SC' block, which shows a plot of SC vs Aλ,f0. The output of the 'SC' block is also 'Aλ,f0'. This value is then input to a 'ΔFAR' block, which shows a plot of ΔFAR vs SC. The output of the 'ΔFAR' block is 'ΔFAR'. Finally, 'ΔFAR' and 'FARλ' are summed in a circle to produce the final output 'FAR'.](f5e131a3fffe09aa98db055df84e4378_img.jpg)

Figure 4: The proposed strategy to avoid the SC effect on the FAR control. The diagram is a block diagram. At the top, a 'λ-sensor signal' is input to a 'FARλ' block. This signal also goes into a 'DFT' block, which shows a plot of amplitude vs frequency with a peak at f0. The output of the DFT is 'Aλ,f0'. This value is input to an 'SC' block, which shows a plot of SC vs Aλ,f0. The output of the 'SC' block is also 'Aλ,f0'. This value is then input to a 'ΔFAR' block, which shows a plot of ΔFAR vs SC. The output of the 'ΔFAR' block is 'ΔFAR'. Finally, 'ΔFAR' and 'FARλ' are summed in a circle to produce the final output 'FAR'.

**Figure 4.** The proposed strategy to avoid the SC effect on the FAR control.

time using a circular buffer in which the signal samples are stored, to calculate the DFT from its value in the previous step.<sup>26</sup> The size of the buffer must contain an integer number of engine cycles, and the sampling frequency must be proportional to the engine speed. The buffer must be filled orderly, substituting the old samples with the new ones, allowing the calculation of the frequency content of the signal for the corresponding harmonic.

Next, the previous signal ( $\hat{A}_{\lambda,f_0}$ ) can be used to estimate the SC with the aid of an experimental correlation, in which the actual SC has been measured by means of the tracer gas method at steady state, for example. Once the instantaneous SC is known,  $\lambda$ -sensor overestimation can be corrected using the experimental correlation shown in Figure 1 (bottom plot), where FAR error ( $\Delta\text{FAR}$ ) is calibrated as a function of SC. Finally, the FAR error estimation can be applied over the FAR value provided by the  $\lambda$ -sensor to get the actual FAR.

## Results and discussion

The SC estimation based on the  $\lambda$ -sensor has several advantages in comparison with the tracer gas method. On the one hand, it is not intrusive since no reacting substances may be introduced. On the other hand, it allows to obtain the dynamic evolution of the SC under transient conditions, while the gas analyser time

![Figure 5: Scatter plot showing the correlation between SC [%] (y-axis, 0 to 10) and the amplitude of the instantaneous frequency content at the engine frequency of the lambda-sensor signal (x-axis, 10 to 25). The data points show a strong linear correlation with R^2 = 0.95206.](7a3561af571faf036baa93f5f4b1bdb9_img.jpg)

Figure 5: Scatter plot showing the correlation between SC [%] (y-axis, 0 to 10) and the amplitude of the instantaneous frequency content at the engine frequency of the lambda-sensor signal (x-axis, 10 to 25). The data points show a strong linear correlation with R^2 = 0.95206.

**Figure 5.** Correlation between the SC measured with the tracer gas method and the amplitude of the instantaneous frequency content at the engine frequency of  $\lambda$ -sensor signal.

response prevents from a proper dynamic evolution. In addition, the  $\lambda$ -sensor is available in all the automotive SI engines, and thus the SC estimation could be performed online, in contrast to the tracer gas method that needs complex and expensive experimental facilities.

Figure 5 shows how the correlation between the SC measured with the tracer gas method and the amplitude of the harmonic corresponding to the engine frequency for  $\lambda$ -sensor signal fits quite well for a linear approximation, at least in the SC range tested.

As the first approach, for the implementation of this methodology the SC estimation via  $\lambda$ -sensor has been calculated offline. The test shown in Figure 6 consists in the transition from the valve overlap levels “d” to “e” in two different ways. First (black lines), the FAR provided by the  $\lambda$ -sensor is kept constant around the optimum value for the SC level “d” in terms of emissions. Next (gray lines), the test is repeated but the FAR is corrected with the proposed method to take into account the  $\lambda$ -sensor overestimation with the SC increase. The SC evolution during the transition from “d” to “e” is displayed for both the SC measurement with the tracer gas method (dashed line) and the SC estimation provided by the  $\lambda$ -sensor (continuous line).

Of course, the SC evolution measured with the tracer gas method is not useful for on-board control purposes, since it needs the simultaneous measurement of  $\text{CH}_4$  at intake and exhaust with and without  $\text{CH}_4$  injection. Moreover, the gas analyzer imposes an important delay as displayed in the top plot in Figure 6. In this test, the closing retard of the exhaust valve is gradually increased, then, the wastegate is partially opened to keep the engine load constant. Thus, both SC measurement (tracer gas method) and estimation (frequency analysis of  $\lambda$ -sensor) are totally consistent with the actuators operation. From level “d” SC rises instantaneously when the overlap increases. Next, SC is reduced due to the wastegate operation giving as a result the SC at level “e”, since the pressure difference between intake and exhaust manifolds drops off slightly.

Regarding the case with FAR correction, the test shows how FAR has an impact on the SC level for the same valve overlap, particularly SC is lower when FAR rises according to the SC measurement and estimation. It is due to the fact that in-cylinder FAR ( $\text{FAR}_{\text{CYL}}$ ) drives the combustion temperature, as shown in Figure

![Figure 6: Three stacked plots showing SC and FAR over time. Top plot: SC [%] vs Time [s] (0 to 120). It compares Tracer Gas Method (dashed lines) and lambda-sensor estimation (solid lines) with and without FAR correction (W/O Correction in black, W/ Correction in gray). Middle plot: FAR_lambda vs Time [s]. Bottom plot: FAR_GA vs Time [s].](bec3b1d6f15b643228b0da0a7d47bdbd_img.jpg)

Figure 6: Three stacked plots showing SC and FAR over time. Top plot: SC [%] vs Time [s] (0 to 120). It compares Tracer Gas Method (dashed lines) and lambda-sensor estimation (solid lines) with and without FAR correction (W/O Correction in black, W/ Correction in gray). Middle plot: FAR\_lambda vs Time [s]. Bottom plot: FAR\_GA vs Time [s].

**Figure 6.** Top: SC measurement with the tracer gas method (dashed lines) and SC estimation with  $\lambda$ -sensor via DFT (continuous lines) for two different cases, that is, with and without FAR correction (gray and black lines, respectively); center: FAR provided by the  $\lambda$ -sensor; bottom: actual FAR provided by the gas analyzer.

7, where the normalized exhaust temperature is plotted on the  $\text{FAR}_{\text{CYL}}$ - $\text{FAR}_{\text{GA}}$  map. Maximum temperatures are reached with  $\text{FAR}_{\text{CYL}} \approx 1$  independently on the exhaust  $\text{FAR}_{\text{GA}}$  provided by the gas analyzer. As a consequence, the turbocharging compression ratio ( $r_C$ ) decreases when the exhaust temperature ( $T_3$ ) is reduced, pushed by rich  $\text{FAR}_{\text{CYL}}$ . Equation (3) shows the dependence between  $T_3$  and  $r_C$ . The enrichment due to the FAR correction with SC involves a decline on exhaust temperature that leads to a reduction in the pressure difference between intake and exhaust, hence involving a slight reduction in the SC shown with both the tracer gas and frequency analysis methods. That is why, compared with the case without FAR correction, SC decreases slightly when FAR increases to reach the proper TWC window, thereby reducing  $\text{NO}_x$  emissions

$$r_C = \left\{ 1 + (1 + F)C_1 \frac{T_3}{T_1} \eta \left[ 1 - \left( \frac{1}{r_T} \right)^{C_2} \right] \right\}^{C_3} \quad (3)$$

where  $r_C = P_2/P_1$  is the compression ratio (compressor),  $r_T = P_3/P_4$  is the expansion ratio (turbine),  $\eta = \eta_C \cdot \eta_T \cdot \eta_m$  is the overall efficiency,  $T_3$  is the turbine inlet temperature,  $T_1$  is the compressor inlet temperature,  $C_1 = c_{pT}/c_{pC}$ ,  $C_2 = (\gamma_T - 1)/\gamma_T$  and  $C_3 = \gamma_C/(\gamma_C - 1)$ .

Finally, Figures 8 and 9 show  $\text{NO}_x$  and CO emissions upstream and downstream TWC, respectively. According to the previous work of the authors,<sup>1</sup> raw emissions are mainly led by  $\text{FAR}_{\text{CYL}}$ , and thus when SC rises and the FAR upstream TWC is controlled in a closed loop, CO and  $\text{NO}_x$  increase and decrease, respectively, at the engine exhaust as expected. In addition, it

![Figure 7: A 3D surface plot showing the relationship between in-cylinder FAR (FAR_CYL) on the vertical axis, gas analyzer FAR (FAR_GA) on the horizontal axis, and manifold temperature on the depth axis. The colorbar indicates normalized exhaust manifold temperature ranging from 0.9 to 1.0. Several overlapping surfaces are labeled SCg, SCf, SCe, SCd, SCc, SCb, and SCa, representing different operating conditions.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 7: A 3D surface plot showing the relationship between in-cylinder FAR (FAR\_CYL) on the vertical axis, gas analyzer FAR (FAR\_GA) on the horizontal axis, and manifold temperature on the depth axis. The colorbar indicates normalized exhaust manifold temperature ranging from 0.9 to 1.0. Several overlapping surfaces are labeled SCg, SCf, SCe, SCd, SCc, SCb, and SCa, representing different operating conditions.

**Figure 7.** The FAR effect on exhaust temperature by comparing  $FAR_{GA}$  provided by the gas analyzer at the exhaust with the in-cylinder  $FAR_{CYL}$  for several overlapping levels.

![Figure 8: Two stacked line plots showing emissions over time (0 to 120 seconds). The top plot shows NOx emissions (ppm) with a scale factor of 10^4, and the bottom plot shows CO emissions (ppm). Both plots compare 'W/O Correction' (black line) and 'W/ Correction' (grey line). A sharp drop in both emissions occurs around 60 seconds, followed by a recovery. The 'W/ Correction' case shows a more stable recovery to the initial levels.](ac99eff233b8fe51d30f499e7413c345_img.jpg)

Figure 8: Two stacked line plots showing emissions over time (0 to 120 seconds). The top plot shows NOx emissions (ppm) with a scale factor of 10^4, and the bottom plot shows CO emissions (ppm). Both plots compare 'W/O Correction' (black line) and 'W/ Correction' (grey line). A sharp drop in both emissions occurs around 60 seconds, followed by a recovery. The 'W/ Correction' case shows a more stable recovery to the initial levels.

**Figure 8.** Top:  $NO_x$  emissions upstream TWC; bottom: CO emissions upstream TWC.

can be observed how, despite the fact that upstream TWC emissions are quite similar by comparing the cases with and without FAR correction, downstream TWC the  $\lambda$ -sensor overestimation causes an important penalty in  $NO_x$  emissions when the effect of SC on  $\lambda$ -sensor is not corrected. In this sense, the FAR correction allows to keep the emissions almost constant around the optimum value after the SC step, avoiding the FAR overestimation produced by SC pulses on the  $\lambda$ -sensor.

## Conclusion

Concerning the SC effects on after-treatment systems for SI engines, a correction to cope with the  $\lambda$ -sensor

![Figure 9: Two stacked line plots showing emissions downstream TWC over time (0 to 120 seconds). The top plot shows NOx emissions (ppm) and the bottom plot shows CO emissions (ppm). Both plots compare 'W/O Correction' (black line) and 'W/ Correction' (grey line). A sharp increase in NOx emissions occurs around 60 seconds, which is significantly higher in the 'W/O Correction' case. The 'W/ Correction' case shows a much smaller increase, remaining closer to the initial levels.](92c6488dfdf125bc1b7bb6a235394652_img.jpg)

Figure 9: Two stacked line plots showing emissions downstream TWC over time (0 to 120 seconds). The top plot shows NOx emissions (ppm) and the bottom plot shows CO emissions (ppm). Both plots compare 'W/O Correction' (black line) and 'W/ Correction' (grey line). A sharp increase in NOx emissions occurs around 60 seconds, which is significantly higher in the 'W/O Correction' case. The 'W/ Correction' case shows a much smaller increase, remaining closer to the initial levels.

**Figure 9.** Top:  $NO_x$  emissions downstream TWC; bottom: CO emissions downstream TWC.

overestimation in the presence of SC has been proposed. The idea arises from the need to measure or at least estimate the SC on-board, in order to improve the FAR control under these circumstances beyond which it is allowed by mapping the SC as a static calibration.

The signal provided by the  $\lambda$ -sensor upstream TWC is employed for two different purposes. As usual, the content at a low frequency allows measuring FAR. The amplitude of the  $\lambda$ -sensor signal at engine frequency, in turn, provides information related to the SC level. In this way, with the strategy proposed, it could be feasible to correct online the FAR overestimation that appears when the engine runs under SC conditions.

Finally, the experimental tests carried out in this study highlight the potential of this approach to reduce pollutant emissions, especially  $NO_x$ , since the FAR overestimation involves operating under leaner conditions than expected.

## Declaration of conflicting interests

The author(s) declared no potential conflicts of interest with respect to the research, authorship and/or publication of this article.

## Funding

The author(s) disclosed receipt of the following financial support for the research, authorship, and/or publication of this article: The authors acknowledge the support of Spanish Ministerio de Economía, Industria y Competitividad through project TRA2016-78717-R.

## ORCID iDs

Benjamín Pla ![ORCID icon](f9f168a9979beed8b01f8750d577d508_img.jpg) <https://orcid.org/0000-0001-9238-2939>  
 Marcelo Real ![ORCID icon](b1ac1d1e1abb0e6ef93ffe234a7377a4_img.jpg) <https://orcid.org/0000-0003-4845-3239>

## References

1. Guardiola C, Pla B, Real M, Travillard C and Dambri-court F. Short-circuit effects on spark ignition engine

- after-treatment and fuel-to-air ratio control. *Int J Engine Res*. Epub ahead of print 17 September 2018. DOI: 10.1177/1468087418796705.
- Martin S, Beidl C and Mueller R. Responsiveness of a 30 bar BMEP 3-cylinder engine: opportunities and limits of turbocharged downsizing. *SAE technical paper* 2014-01-1646, 2014.
  - Pagot A, Duparchy A, Gautrot X, Leduc P and Monnier G. Combustion approach for downsizing: the IFP concept. *Oil Gas Sci Technol* 2006; 61(1): 139–153.
  - Ranini A and Monnier G. Turbocharging a gasoline direct injection engine. SAE technical report 2001-01-0736, 2001.
  - Leduc P, Dubar B, Ranini A and Monnier G. Downsizing of gasoline engine: an efficient way to reduce CO<sub>2</sub> emissions. *Oil Gas Sci Technol* 2003; 58(1): 115–127.
  - Auckenthaler T. *Modelling and control of three-way catalytic converters*. PhD Thesis, Swiss Federal Institute of Technology Zurich, Zurich, 2005.
  - Takubo H, Umeno T and Goto H. New lambda-lambda air-fuel ratio feedback control. SAE technical paper 2007-01-1340, 2007.
  - Turin RC and Geering HP. Model-based adaptive fuel control in an SI engine. *SAE technical paper* 940374, 1994.
  - Powell JD, Fekete N and Chang CF. Observer-based air fuel ratio control. *IEEE Control Syst* 1998; 18(5): 72–83.
  - Guzzella L. Models and modelbased control of IC-engines: a nonlinear approach. *SAE Trans* 1995; 104(3): 1439–1447.
  - Roduner C, Onder C and Geering HP. Automated design of an air/fuel controller for an SI engine considering the three-way catalytic converter in the H approach. In: *Proceedings of the 5th Mediterranean conference on control and systems*, Paphos, Cyprus, (July, 1997).
  - Takiyama T, Shiomi E and Morita S. Air-fuel ratio control system using pulse width and amplitude modulation at transient state. *JSAE Rev* 2001; 22(4): 537–544.
  - Chang CF, Fekete NP, Amstutz A and Powell JD. Air-fuel ratio control in spark-ignition engines using estimation theory. *IEEE T Control Syst Technol* 1995; 3(1): 22–31.
  - Shafai E, Roduner C and Geering HP. Indirect adaptive control of a three-way catalyst. *SAE technical paper* 961038, 1996.
  - Balenovic M, Backx A and Hoebink J. On a model-based control of a three-way catalytic converter. SAE technical paper 2001-01-0937, 2001.
  - Balenovic M, Backx T and De Bie T. Development of a model-based controller for a three-way catalytic converter. SAE technical paper 2002-01-0475, 2002.
  - Yildiz Y, Annaswamy AM, Yanakiev D and Kolmanovsky I. Spark ignition engine fuel-to-air ratio control: an adaptive control approach. *Control Eng Pract* 2010; 18(12): 1369–1378.
  - Tomforde M, Drewelow W and Schultalbers M. Air-fuel ratio control with respect to oxygen storage dynamics. In: *Proceedings of the 16th international conference on methods and models in automation and robotics*, Miedzyzdroje, 22–25 August 2011, pp.242–247. New York: IEEE.
  - Germann H, Tagliaferrri S and Geering HP. Differences in pre- and post-converter lambda sensor characteristics. *SAE technical paper* 960335, 1996.
  - Olsen DB. *Experimental and theoretical development of a tracer gas method for measuring trapping efficiency in internal combustion engines*. PhD Thesis, Colorado State University, Fort Collins, CO, 1999.
  - Olsen DB, Hutcherson GC, Willson BD and Mitchell CE. Development of the tracer gas method for large bore natural gas engines. Part I: method validation. *J Eng Gas Turbine Power* 2002; 124(3): 678–685.
  - Schweitzer P. *Scavenging of two-stroke cycle diesel engines*. Macmillan Co., New York, 1949.
  - McGough MG and Fanick ER. Experimental investigation of the scavenging performance of a two-stroke opposed-piston diesel tank engine. SAE technical paper 2004-01-1591, 2004.
  - Macián V, Lujan JM, Guardiola C and Yuste P. DFT-based controller for fuel injection unevenness correction in turbocharged diesel engines. *IEEE T Control Syst Technol* 2006; 14(5): 819–827.
  - Macián V, Galindo J, Luján J and Guardiola C. Detection and correction of injection failures in diesel engines on the basis of turbocharger instantaneous speed frequency analysis. *Proc IMechE, Part D: J Automobile Engineering* 2005; 219(5): 691–701.
  - García CG. *Detección y compensación de irregularidades de inyección a través de la medida del régimen instantáneo del turbogrupo*. Reverté, Barcelona, 2005.