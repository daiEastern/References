

# Fast Response Time Fiber Optical pH and Oxygen Sensors

Jan Werner<sup>abc</sup>, Mathias Belz<sup>a</sup>, Karl-Friedrich Klein<sup>ac</sup>, Tong Sun<sup>b</sup> and K.T.V. Grattan<sup>b</sup>

<sup>a</sup>World Precision Instruments Germany GmbH, Pfingstweide 16, 61169 Friedberg, Germany

<sup>b</sup>School of Mathematics, Computer Science and Engineering, City, University of London,  
Northampton Square, EC1V 0HB, London, U.K.

<sup>c</sup>THM, University of Applied Science, Wilhelm-Leuschner-Strasse 13, 61169 Friedberg, Germany

## ABSTRACT

While fluorescence-based fiber optic sensors for measuring both pH and oxygen concentration ( $O_2$ ) are well known, current sensors are often limited by their response time and drift, which limits the use of existing fiber optic sensors of this type in wider applications, for example in physiology and other fields. Several new fiber optical sensors have been developed and optimized, with respect to key features such as tip shape and coating layer thickness. In this work, preliminary results on the performance of a suite of pH sensors with fast response times,  $< 3$  second and oxygen sensors ( $O_2$ ) with response times  $< 0.2$  second. The sensors have been calibrated and their performance analyzed using the Henderson–Hasselbalch equation (pH) and classic Lehrer-model ( $O_2$ ).

**Keywords:** optical fibers, fiber optics, fluorescence, luminescence, decay time, sensor, pH, oxygen,  $O_2$ , fast response time

## 1. INTRODUCTION

The determination of pH level and oxygen concentration ( $O_2$ ) is very important in a broad range of applications in life sciences, industry, environmental monitoring and biomedical research. For example, there is particular interest in detecting both parameters in the clinical analysis of blood<sup>1</sup>, for quality control in food industry<sup>2</sup>, for process control in bioreactors<sup>3, 4</sup> or seawater analysis<sup>5, 6</sup>. Classical electrochemical sensors, like the Clark electrode<sup>7</sup> and the pH glass electrode<sup>8</sup>, are well known for the measurements of  $O_2$  concentration and the pH. However, these types of sensors have the disadvantages of being subject to interference from stray electromagnetic fields and as they consume the analyte, this can cause problems in some situations. In addition, they often are bulky and their glass surface makes them fragile and likely to break unless which can have a handled very carefully. Optical, and especially fiber optical sensors have become attractive for these sorts of measurements in recent times since these sensors do not consume the analyte (e.g. oxygen), are reversible and easy to miniaturize ( $< 50\mu\text{m}$ ). Further, they can be used to measure the analyte in either the gas or the liquid phase, they are inexpensive and can be used where there is electromagnetic interference<sup>9</sup>. Therefore, there is increasing demand for such fiber optic pH and  $O_2$  sensors, for a wide range of commercial and industrial uses.

The most widely used optical techniques to detect pH or  $O_2$  concentration are absorbance/reflectance or luminescence based. Many kinds of indicator dyes are available for pH monitoring (e.g. SNARF, SNAFL, HPTS and fluorescein)<sup>10</sup> and  $O_2$  concentration (e.g. complexes of Ru(II), Ir(II), Pt(II) and Pd(II)) that offer a luminescence intensity, luminescence decay time or ratiometric (absorbance or luminescence) based measurement of the analyte<sup>9, 11</sup>. In comparison to ratiometric measurements, the detection of luminescence intensity or decay time is preferable, since only one type of indicator dye is required. This reduces the complexity of the detection systems, for example in reducing the number of excitation sources and emission detectors needed and thus the overall system cost. However, direct luminescence measurements have the disadvantages that they can be strongly influenced by problems such as photobleaching, stray light and the drift of the electronic components used in the instrumentation<sup>11</sup>.

In a typical fiber optic sensor, the indicator dye is immobilized in a supporting matrix (often a polymer) and firmly attached to the sensor tip<sup>12</sup>. The sensor performance (exemplified in the response time, drift and detection range) is mainly influenced by the combination of the sensor platform (in this case, the fiber tip), the polymer and the indicator dye<sup>13</sup>. One parameter which can offer a significant improvement in the sensor performance is to optimize the design of the fiber tip, with the potential to reduce the response time as a result. Further, the physical parameters of the optical fiber chosen need to be taken fully into account, since these significantly influence the light guidance in the optical fiber chosen<sup>14, 15</sup>.

Currently available luminescence-based pH sensors typically have response times from ~13 seconds to an extreme of 54 minutes<sup>12</sup>. As in many applications a much shorter response time is important, in this work the focus has been on the reduction of this parameter. Here the first results of a fiber optic pH and O<sub>2</sub> sensor, showing a faster response time than has been reported has been developed, based on new tip designs for luminescence-based sensors. Firstly, the pH-sensitive coating used is associated with an indicator dye suitable for the pH range from pH 5 to pH 8.5, this being immobilized in a hydrogel. The sensor method used detects pH changes through measuring the luminescence intensity, using a newly developed instrument that also reduces the effect of photobleaching and stray light, problems in many conventional sensors. Secondly, the O<sub>2</sub> sensitive coating has been created using an indicator dye optimized for the range 0% to 21% O<sub>2</sub>, where the dye is physically entrapped in a polymer matrix. The approach to detection of the O<sub>2</sub> concentration changes is through monitoring the luminescence decay time, using a commercially available instrument.

## 2. THEORETICAL BACKGROUND: DETERMINATION OF pH AND O<sub>2</sub>

The fiber optic sensors designed and reported in this paper are based on luminescence signal measurements (either optical intensity or decay time). A brief theoretical discussion on how these parameters can be related to the determination of the pH and O<sub>2</sub> concentration is given below.

### 2.1 Henderson-Hasselbalch equation

Classical electrochemical sensors directly measure the activity of hydrogen ions in aqueous solutions and optical pH sensors the concentrations of the protonated and deprotonated form of the indicator dye. For luminescence-based sensors, this effect results in a change of the luminescence intensity observed.

The well-known Henderson-Hasselbalch equation is commonly used to determine pH from the changes of the deprotonated [A<sup>-</sup>] and protonated [HA] form optically<sup>12</sup> where:

$$\text{pH} = \text{pK}_a - \log \frac{[\text{HA}]}{[\text{A}^-]} \quad (1)$$

and pK<sub>a</sub> is the acid-base constant of the indicator dye.

Defining I<sub>max</sub> as the maximum luminescence intensity signal of the deprotonated form and I<sub>min</sub> as the minimum luminescence intensity signal of the protonated form, pH can be calculated using the following equation:

$$\text{pH} = \text{pK}_a - b \cdot \log \left( \frac{I_{\text{max}} - I_m}{I_m - I_{\text{min}}} \right) \quad (2)$$

where I<sub>m</sub> is the measured luminescence intensity and b the numerical coefficient to determine the slope of the function<sup>16</sup>.

### 2.2 Lehrer quenching model

To describe the photophysical effect caused by collision quenching by O<sub>2</sub>, the most familiar approach is through the Stern-Volmer equation. During this process, the luminescence decay time is reduced due to dynamic collisions of molecular O<sub>2</sub> in an excited electronic state. However, the Stern-Volmer model is only true for an ideal quenching system<sup>11</sup>. Since many luminescence sensor coatings used show non-linear behaviors, two other models (Lehrer and Demas) are well-known and can be used to describe the effect of a quenchable and a non-quenchable side. To calibrate the O<sub>2</sub> sensors discussed in this paper, the simplified Lehrer model has been used<sup>17</sup>:

$$\frac{\tau_0}{\tau} = \left( \frac{x}{1 + K_{\text{SV}}[\text{O}_2]} + (1 - x) \right)^{-1} \quad (3)$$

where τ<sub>0</sub> is the decay time (in the absence of O<sub>2</sub>), and τ is the measured decay time in the presence of O<sub>2</sub>, K<sub>SV</sub> is the Stern-Volmer constant, x the relative contribution of the two sides, while [O<sub>2</sub>] is the concentration of the quenching agent, (O<sub>2</sub>).

## 3. SENSOR DESIGN AND EXPERIMENTAL SETUP

Figure 1 shows a schematic of the fiber optic sensor design (for pH and O<sub>2</sub>) used in this research. For both sensors, commercial available fibers were combined with new tip designs, where the pH or O<sub>2</sub> sensitive materials selected were attached to the fiber tip.

![Schematic diagram of a fiber optic sensor-based design for pH and O2 sensors. The diagram shows a fiber optic cable with a connector at the left end. The cable is labeled 'opt. connector' and 'opt. fiber'. The fiber has a shaped tip at the right end, labeled 'tip (pH or O2 coating)'. A red segment is highlighted on the fiber near the tip, representing the incorporated sensitive layer.](7e2f2d03a5dda38b038fd4884629a2b4_img.jpg)

Schematic diagram of a fiber optic sensor-based design for pH and O2 sensors. The diagram shows a fiber optic cable with a connector at the left end. The cable is labeled 'opt. connector' and 'opt. fiber'. The fiber has a shaped tip at the right end, labeled 'tip (pH or O2 coating)'. A red segment is highlighted on the fiber near the tip, representing the incorporated sensitive layer.

Figure 1. Schematic of the fiber optic sensor-based design for pH and O<sub>2</sub> sensors with the new sensor tip with incorporated sensitive layer (red).

### 3.1 Preparation of pH sensors

Preparing the pH sensitive coating, an indicator dye with a detection range from pH 5.0 to pH 8.5 and exhibiting a strong luminescence signal was chosen. A hydrogel approach was chosen where the dye itself and the appropriate chemicals needed to create the hydrogel were dissolved and the solution formed coated on the shaped fiber tip. Through extensive research, the coating process was optimized for this specific fiber design and thus the polymerization proceeded quickly – only a short time was required (< 30s) to finish the polymerization process. After polymerization the pH sensitive material was mechanically connected to the fiber tip to create the sensor.

### 3.2 Preparation of O<sub>2</sub> sensors

In preparing the O<sub>2</sub> sensitive coating, an indicator dye with an optimized detection range from 0% to 21% O<sub>2</sub> was used, achieving a strong luminescence signal and a relative long luminescence decay time which allows for an easier measurement in the associated instrumentation. As above, the dye was dissolved in the polymer and a sample of the solution attached to the shaped fiber tip, via a standard dip-coating process. After 12h drying under constant environmental conditions (stable humidity and temperature), the O<sub>2</sub> sensitive coating was mechanically connected to the fiber tip.

### 3.3 Experimental setup for pH measurement and calibration

Figure 2 shows a schematic of the experimental setup used for evaluating the pH sensors developed. This newly designed instrument was able to monitor the weak luminescence emission signals from the pH-sensitive coating attached to the fiber tip. This new instrument thus can work with very low excitation intensities, important to reduce photobleaching of the dye which is the active element of the sensor. Further, the design of the electronics and the optics used were optimized, to minimize the effect of stray light and drift in the electronic signals processed. In order to characterize the pH sensors produced in this way, each fiber optic sensor was connected to the optical port and the output monitored when the probe was dipped into 5 different pH buffers (pH 5, pH 6, pH 7, pH 8 and pH 8.5). Each measurement was performed under constant environmental conditions (stable temperature and pressure) and the pH values of the buffer solutions used were checked, both before and after each measurement (using a reference glass electrode).

In the course of the experiment, first the relative intensity (in arbitrary units (a.u.)) was measured in each buffer solution and the system calibrated using the Henderson-Hasselbalch equation (Eq. 2). To analyze the response time,  $\Delta t_{90}$ , the pH sensors were first dipped into the pH 6 buffer solution and then quickly (< 1s) transferred to the pH 7 buffer solution. Finally, a measurement of any drift in the sensor response when the probe was maintained in the pH 7 buffer solution was performed, over a 12h period, with a continuous irradiation of the sensor tip to determine if any evidence of photobleaching could be seen (given these extreme irradiation conditions for 12 h).

![Schematic of the experimental setup for calibrating the pH sensors. A glass bottle labeled 'pH Buffers (pH5 – pH8.5)' is connected via a blue tube to a 'pH sensor'. The sensor is inserted into the bottle. The other end of the blue tube is connected to an 'optical port' on a grey rectangular 'Instrument'.](5f18c728fc511750ffcaa626716b920e_img.jpg)

Schematic of the experimental setup for calibrating the pH sensors. A glass bottle labeled 'pH Buffers (pH5 – pH8.5)' is connected via a blue tube to a 'pH sensor'. The sensor is inserted into the bottle. The other end of the blue tube is connected to an 'optical port' on a grey rectangular 'Instrument'.

Figure 2. Schematic of the experimental setup for calibrating the pH sensors, used with the newly developed detection instrument, allowing luminescence intensity measurements to undertake the calibration. Five different pH buffer solutions (from pH 5 to pH 8.5) in glass bottles were used for sensor system characterization.

### 3.4 Experimental setup for O<sub>2</sub> measurement and calibration

Figure 3 shows the schematic of the experimental setup used for evaluating the performance of the O<sub>2</sub> sensors developed. The fiber optic sensor probes developed in this work were connected to a commercially available instrument for luminescence decay time measurements and placed in a closed chamber, together with a reference O<sub>2</sub> sensor. The evaluation chamber was temperature-regulated and equipped with a gas input, connected with two gas flow controllers to allow known quantities of O<sub>2</sub> and N<sub>2</sub> to be delivered to the chamber. With this setup, different O<sub>2</sub> concentrations could be generated fully automatically using a PC controller, connected to proprietary software. In the experiment carried out, first the luminescence decay times (in the  $\mu$ s range) were measured and calibrated for each known concentration of O<sub>2</sub> used, using the Lehrer quenching model (Eq. 3). The results of the O<sub>2</sub> measurement thus obtained were compared with the quantities of gas delivered using the regulated O<sub>2</sub> supply (using the gas flow controllers) and for comparison, the output of a conventional reference gas sensor. To establish the speed of response of the O<sub>2</sub> probe, a rapid change in the O<sub>2</sub> fraction (from 21% to 0% O<sub>2</sub>) was generated inside the closed chamber using the gas control mechanism discussed.

![Schematic of the experimental setup for the calibration of the O2 sensors. A central cylindrical chamber is shown. A blue tube labeled 'O2 sensor' connects to the top of the chamber and leads to an 'Instrument'. A grey rod labeled 'ref. sensor' extends from the side of the chamber. The chamber has a 'gas input' and a 'gas output' on opposite sides. A 'temp. regulation' label points to a cooling/heating mechanism at the bottom of the chamber.](b615ff07e8a0f467f0a6f4783c4463eb_img.jpg)

Schematic of the experimental setup for the calibration of the O2 sensors. A central cylindrical chamber is shown. A blue tube labeled 'O2 sensor' connects to the top of the chamber and leads to an 'Instrument'. A grey rod labeled 'ref. sensor' extends from the side of the chamber. The chamber has a 'gas input' and a 'gas output' on opposite sides. A 'temp. regulation' label points to a cooling/heating mechanism at the bottom of the chamber.

Figure 3. Schematic of the experimental setup for the calibration of the O<sub>2</sub> sensors. The sensors were connected to an instrument for luminescence decay time measurements and placed with a reference sensor in a temperature and gas regulated chamber.

## 4. EXPERIMENTAL RESULTS AND DISCUSSION

This section shows the response and thus the characterization of the newly developed fiber optic pH and O<sub>2</sub> sensors, with respect to key parameters which include system calibration, accuracy, long-term stability and response time.

### 4.1 Characterization of the pH sensors

Figure 4 shows the measured steady state signal intensities obtained from the fiber optic pH sensor when immersed in the pH 5, pH 6, pH 7, pH 8 and pH 8.5 buffer solutions. For each pH value the relative intensity was determined by averaging the signals over a time interval of 10 seconds. The dashed line represents the fitted titration curve, applying Equation (2) with  $pK_a = 8.01$ ,  $I_{max} = 9.47$ ,  $I_{min} = 1.23$  and  $b = 1.72$ . The equation used describes the experimental results very precisely (with a very high correlation coefficient,  $R^2 = 0.9999$ ). Further tests carried out that the calibrated pH sensors have excellent repeatability. The evaluation undertaken shows a sensor accuracy of about  $\pm 0.04$  pH units (@ pH 7), using a glass pH electrode as reference standard. Figure 5 shows the measured changes in pH over the range from pH 5 to pH 8, for a sensor after calibration and showing a maximum signal variation which is equivalent to  $< 0.01$  pH units, obtained for pH values greater than pH 6.

![Figure 4: A scatter plot showing the relative intensity [a.u.] versus pH. The x-axis ranges from 5 to 9, and the y-axis ranges from 0 to 8. Data points are plotted at pH 5, 6, 7, 8, and 8.5, showing an increasing trend. A dashed curve represents the fitted titration curve.](b15e3860e0c96ed16ce77f032da6f107_img.jpg)

| pH  | rel. intensity [a.u.] |
|-----|-----------------------|
| 5   | 1.23                  |
| 6   | 1.45                  |
| 7   | 2.65                  |
| 8   | 5.35                  |
| 8.5 | 7.25                  |

Figure 4: A scatter plot showing the relative intensity [a.u.] versus pH. The x-axis ranges from 5 to 9, and the y-axis ranges from 0 to 8. Data points are plotted at pH 5, 6, 7, 8, and 8.5, showing an increasing trend. A dashed curve represents the fitted titration curve.

Figure 4. pH dependency of the luminescence intensity recorded over the range from pH 5 – pH 8.5. The dashed curve represents the fit using Equation (2) with  $R^2 = 0.9999$ .

![Figure 5: A line graph showing measured pH changes in aqueous solutions over time. The x-axis is time [sec.] from 0 to 160, and the y-axis is pH from 4 to 9. The pH value steps up from 5 to 6, then to 7, then to 8, and finally back down to 5, with small fluctuations around each level.](6f1efa91fb9b476380af7a35db4f14bf_img.jpg)

| time [sec.] | pH  |
|-------------|-----|
| 0           | 5.0 |
| 30          | 5.0 |
| 35          | 5.8 |
| 40          | 5.8 |
| 50          | 6.0 |
| 60          | 6.0 |
| 70          | 6.8 |
| 80          | 6.8 |
| 90          | 7.0 |
| 100         | 7.0 |
| 110         | 7.8 |
| 120         | 7.8 |
| 130         | 5.0 |
| 140         | 5.0 |
| 160         | 5.0 |

Figure 5: A line graph showing measured pH changes in aqueous solutions over time. The x-axis is time [sec.] from 0 to 160, and the y-axis is pH from 4 to 9. The pH value steps up from 5 to 6, then to 7, then to 8, and finally back down to 5, with small fluctuations around each level.

Figure 5. Measured pH changes in aqueous solutions after calibration over the range pH 5 to pH 8.

Figure 6 shows the response time of the newly developed pH sensor probe. The sensor has a very fast response to pH changes, of  $\Delta t_{90} < 3$  s (1s buffer changes included) which was observed over the entire detection range (although for clarity here it is only shown over the range from pH 6 to pH 7). In this case, it was observed unexpectedly that the sensor needed an additional 10s to reach the steady state. This phenomenon was not observed for all the sensor designs studied and it could therefore be assumed that this was related to an inhomogeneous layer distribution and irregular thickness on the fiber tip that influences the pH changes locally. However, it is considered that this very low, and important response time is unique when compared to the wide range of pH sensors reported in the literature and described in other publications. Figure 7 shows a measurement made of the probe in a pH 7 buffer solution for 12h, under continuous irradiation to examine if drift or photobleaching occurred. It was pleasing to note that the pH sensors are very stable over this long period of time (the drift seen was  $< 0.05$  pH/h), even though the determination of pH is based on a luminescence intensity measurement. In addition, this small value of drift can be reduced further by changing the duty cycle with longer ‘off-phases’ of the excitation light source.

![Figure 6: Response time of pH sensors from pH 6 to pH 7. The graph plots pH on the y-axis (5.5 to 7.5) against time in seconds on the x-axis (60 to 90). A blue curve shows a rapid rise from pH 6 to pH 7. Two vertical dashed lines mark the start and end of the response, with a horizontal double-headed arrow between them. A text box indicates Δt90 < 3 sec.](431b8889a0e7f676f0eef40859590349_img.jpg)

Figure 6: Response time of pH sensors from pH 6 to pH 7. The graph plots pH on the y-axis (5.5 to 7.5) against time in seconds on the x-axis (60 to 90). A blue curve shows a rapid rise from pH 6 to pH 7. Two vertical dashed lines mark the start and end of the response, with a horizontal double-headed arrow between them. A text box indicates Δt90 < 3 sec.

Figure 6. Response time of pH sensors from pH 6 to pH 7, showing  $\Delta t_{90} < 3s$ .

![Figure 7: Measured signal decrease in pH 7 for 12h and continuous irradiation. The graph plots pH on the y-axis (6.2 to 7.2) against time in hours on the x-axis (0 to 12). A blue curve shows a steady linear decrease from pH 7.0 to approximately 6.45 over 12 hours.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 7: Measured signal decrease in pH 7 for 12h and continuous irradiation. The graph plots pH on the y-axis (6.2 to 7.2) against time in hours on the x-axis (0 to 12). A blue curve shows a steady linear decrease from pH 7.0 to approximately 6.45 over 12 hours.

Figure 7. Measured signal decrease in pH 7 for 12h and continuous irradiation (measured drift:  $< 0.05 \text{ pH/h}$ ).

### 4.2 Characterization of the O<sub>2</sub> sensors

Figure 8 shows the measured steady state decay times of the fiber optic O<sub>2</sub> sensor signal obtained using known concentrations of O<sub>2</sub> (in this case 0%, 4%, 8%, 16% and 20% O<sub>2</sub>). For each O<sub>2</sub> concentration used, the decay time was determined by averaging the signals over a time interval of 10 seconds. The dashed line in the figure represents the curve fit obtained by applying Equation (3), with  $\tau_0 = 10.62 \mu\text{s}$ ,  $K_{SV} = 0.1106$  and  $x = 0.9998$ . The equation used shows a good correlation with the experimental results obtained (with a correlation coefficient,  $R^2 = 0.9986$ ). Further, comparing the measured O<sub>2</sub> concentrations with data from a reference sensor and the flow meter regulated O<sub>2</sub> values, the accuracy of the sensor was determined to be better than  $\pm 0.05\%$  O<sub>2</sub>. Figure 9 shows the response of the sensor to the known O<sub>2</sub> concentration changes, over the range between 0% and 20% O<sub>2</sub>, for a sensor probe used after calibration.

![Figure 8: Measurement of the luminescence decay time (phase monitored in μs) over the gas concentration range between 0% and 20% O2. The graph plots phase in μs on the y-axis (2 to 12) against O2 concentration in % on the x-axis (0 to 20). Red data points show a decreasing trend, fitted by a dashed red line.](e1dda754c2c88a8ad0b968aea4fc0786_img.jpg)

Figure 8: Measurement of the luminescence decay time (phase monitored in μs) over the gas concentration range between 0% and 20% O2. The graph plots phase in μs on the y-axis (2 to 12) against O2 concentration in % on the x-axis (0 to 20). Red data points show a decreasing trend, fitted by a dashed red line.

Figure 8. Measurement of the luminescence decay time (phase monitored in  $\mu\text{s}$ ) over the gas concentration range between 0% and 20% O<sub>2</sub>. The dashed curve represents the fit using equation (3) with  $R^2 = 0.9986$ .

![Figure 9: Response of the sensor to the known O2 concentration changes, over the range between 0% and 20% O2, for a sensor probe used after calibration. The graph plots O2 concentration in % on the y-axis (0 to 24) against time in seconds on the x-axis (0 to 200). A red step function shows the sensor response jumping between 0% and 20% O2 at various time intervals.](80530169c7b6298ce012a85b906caeb3_img.jpg)

Figure 9: Response of the sensor to the known O2 concentration changes, over the range between 0% and 20% O2, for a sensor probe used after calibration. The graph plots O2 concentration in % on the y-axis (0 to 24) against time in seconds on the x-axis (0 to 200). A red step function shows the sensor response jumping between 0% and 20% O2 at various time intervals.

Figure 9. Response of the sensor to the known O<sub>2</sub> concentration changes, over the range between 0% and 20% O<sub>2</sub>, for a sensor probe used after calibration.

Figure 10 shows the response time of the newly developed O<sub>2</sub> sensor. It can be seen that the sensor has an extremely fast response to O<sub>2</sub> changes, with  $\Delta t_{90} < 200\text{ms}$  observed over the entire detection range; here only data are shown with a gas concentration change from 20% to 0% O<sub>2</sub>. This very fast response probe has as a result a number of new application opportunities. To evaluate some of these, a preliminary experiment to detect O<sub>2</sub> in breath was carried out and Figure 11 shows the results. The measurement was done under room temperature conditions, without environmental compensation being applied and the changes in O<sub>2</sub> concentrations were determined when the subject breathed directly on the sensor tip. At this stage, this preliminary result is not cross-calibrated but indicative: it shows the excellent performance of the sensor to a gas (breath) sample where the level of O<sub>2</sub> has fallen by several percent from the ambient ( $\sim 21\%$ ) level. This does, however, show the potential of the sensor for biomedical measurements.

![Figure 10: A line graph showing the response time of an O2 sensor. The y-axis is 'Oxygen [%]' ranging from -4 to 24. The x-axis is 'time [sec.]' ranging from 181 to 184. A red line starts at 20% at time 181.5, drops sharply to 0% at time 182.0, and remains at 0% until time 183.0. A dashed black line indicates the transition. A red arrow points to the start of the drop at 182.0, and a black arrow points to the end of the drop at 182.0. The text Δt90 < 200ms is written in red above the graph.](4086a572c080354982c11f1de4d6921d_img.jpg)

Figure 10: A line graph showing the response time of an O2 sensor. The y-axis is 'Oxygen [%]' ranging from -4 to 24. The x-axis is 'time [sec.]' ranging from 181 to 184. A red line starts at 20% at time 181.5, drops sharply to 0% at time 182.0, and remains at 0% until time 183.0. A dashed black line indicates the transition. A red arrow points to the start of the drop at 182.0, and a black arrow points to the end of the drop at 182.0. The text Δt90 < 200ms is written in red above the graph.

Figure 10. Response time of the O<sub>2</sub> sensor monitoring a drop in O<sub>2</sub> percentage from 20% to 0%, with  $\Delta t_{90} < 200\text{ms}$ .

![Figure 11: A line graph showing the detection of exhaled breath. The y-axis is 'Oxygen [%]' ranging from 17 to 22. The x-axis is 'time [sec.]' ranging from 40 to 90. A red line shows a baseline around 20.5% with small fluctuations. At approximately 48s, 58s, 68s, 78s, and 88s, the signal drops sharply to about 18.5% for a short duration, labeled 'breath out'. The signal returns to the baseline after each drop.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 11: A line graph showing the detection of exhaled breath. The y-axis is 'Oxygen [%]' ranging from 17 to 22. The x-axis is 'time [sec.]' ranging from 40 to 90. A red line shows a baseline around 20.5% with small fluctuations. At approximately 48s, 58s, 68s, 78s, and 88s, the signal drops sharply to about 18.5% for a short duration, labeled 'breath out'. The signal returns to the baseline after each drop.

Figure 11. Preliminary experiment showing the detection of exhaled breath and the fast response time of the sensor to the sample.

## 5. SUMMARY AND OUTLOOK

New fiber optic pH and O<sub>2</sub> sensor systems have been developed, based on new probe tip designs and using luminescence coatings. The preliminary results reported are highly promising and show a significant improvement of sensor performance on current devices, with extreme fast response times to O<sub>2</sub> ( $\Delta t_{90} < 200\text{ms}$ ) and pH ( $\Delta t_{90} < 3\text{s}$ ) changes. With these sensor designs, highly accurate measurements of pH and O<sub>2</sub> are possible using very small gas volumes, because of the design with small optical fibers and small fiber tip diameters. In combination with newly developed instrumentation, the pH sensors have been shown to be very stable over a long period of time, as during a measurement for 12 hours at pH 7 with continuous irradiation, a low signal drift (of less than 0.05 pH/h) and a negligible influence of stray light were observed. Looking to future developments, the drift could be reduced by changing the duty cycle used, with longer ‘off phases’ of the excitation light source. Further R&D activities are planned to optimize the sensor further, for example to analyze the distribution and thickness of the sensor layers and evaluate and reduce any cross-sensitivities to other parameters (e.g. temperature, pressure and ionic strength).

The work has clearly showed that this new sensor design has the potential to extend the breadth of applications for fiber optic pH and O<sub>2</sub> sensors, especially where fast response times are required. As has been shown in the preliminary experiments reported, the O<sub>2</sub> concentration in breath could readily be measured in human subjects. Further, the detection range of the pH sensors is ideal for measurements in seawater, where a pK<sub>a</sub> value from 7 to 9 is necessary, to support better environmental monitoring. A further benefit is that the manufacturing process for these sensors is relatively simple and thus mass-production seems to be feasible, which will also suit a range of applications.

## ACKNOWLEDGEMENT

The authors wish to acknowledge Alexander Schäfer for the great support in software development and Rob Randelman and Tiana Riggi for their continuing support during the development of the sensors and the instrumentation. Grattan and Sun acknowledge support from the Royal Academy of Engineering.

## REFERENCES

- [1] Kojima, S. and Suzuki, H., “A Micro Sensing System for Blood Gas Analysis Constructed With Stacked Modules,” *IEEJ Trans. SM* 124(4), 111–116 (2004).
- [2] Papkovsky, D. B., Papkovskaia, N., Smyth, A., Kerry, J. and Ogurtsov, V. I., “Phosphorescent Sensor Approach for Non-Destructive Measurement of Oxygen in Packaged Foods. Optimisation of Disposable Oxygen Sensors and their Characterization Over a Wide Temperature Range,” *Analytical Letters* 33(9), 1755–1777 (2000).

- [3] Jeevarajan, A. S., Vani, S., Taylor, T. D. and Anderson, M. M., "Continuous pH monitoring in a perfused bioreactor system using an optical pH sensor," *Biotechnology and bioengineering* 78(4), 467–472 (2002).
- [4] Kostov, Y., Harms, P., Randers-Eichhorn, L. and Rao, G., "Low-cost microbioreactor for high-throughput bioprocessing," *Biotechnol. Bioeng.* 72(3), 346–352 (2001).
- [5] Gouin, J. F., Baros, F., Birot, D. and André, J. C., "A fibre-optic oxygen sensor for oceanography," *Sensors and Actuators B: Chemical* 39(1-3), 401–406 (1997).
- [6] Schröder, C. R., Weidgans, B. M. and Klimant, I., "pH fluoresensors for use in marine systems," *The Analyst* 130(6), 907–916 (2005).
- [7] CLARK, L. C., WOLF, R., GRANGER, D. and TAYLOR, Z., "Continuous recording of blood oxygen tensions by polarography," *Journal of applied physiology* 6(3), 189–193 (1953).
- [8] Kerridge, P. T., "The Use of the Glass Electrode in Biochemistry," *The Biochemical journal* 19(4), 611–617 (1925).
- [9] Wang, X.-D. and Wolfbeis, O. S., "Fiber-optic chemical sensors and biosensors (2008-2012)," *Analytical chemistry* 85(2), 487–508 (2013).
- [10] Wencel, D., MacCraith, B. D. and McDonagh, C., "High performance optical ratiometric sol-gel-based pH sensor," *Sensors and Actuators B: Chemical* 139(1), 208–213 (2009).
- [11] Wang, X.-D. and Wolfbeis, O. S., "Optical methods for sensing and imaging oxygen: materials, spectroscopies and applications," *Chemical Society reviews* 43(10), 3666–3761 (2014).
- [12] Wencel, D., Abel, T. and McDonagh, C., "Optical chemical pH sensors," *Analytical chemistry* 86(1), 15–29 (2014).
- [13] McDonagh, C., Burke, C. S. and MacCraith, B. D., "Optical chemical sensors," *Chemical reviews* 108(2), 400–422 (2008).
- [14] K.-F. Klein, C.P. Gonschior, X.Ruan, M.Bloos, G.Hillrichs, H.Poisel, "Transmission of skew modes in polymer- and silica-based step-index fibers," *Proc. 18th POF-conference* (45) (2009).
- [15] Arne Wilhelm Zimmer, Philipp Raithel, Mathias Belz, Karl-Friedrich Klein, "Analysis of spectral light guidance in specialty fibers," in *Proc. SPIE* 9886-34 (2016).
- [16] Vasylevska, A. S., Karasyov, A. A., Borisov, S. M. and Krause, C., "Novel coumarin-based fluorescent pH indicators, probes and membranes covering a broad pH range," *Analytical and bioanalytical chemistry* 387(6), 2131–2141 (2007).
- [17] Medina-Rodríguez, S., La Torre-Vega, Á. de, Medina-Rodríguez, C., Fernández-Sánchez, J. F. and Fernández-Gutiérrez, A., "On the calibration of chemical sensors based on photoluminescence. Selecting the appropriate optimization criterion," *Sensors and Actuators B: Chemical* 212, 278–286 (2015).