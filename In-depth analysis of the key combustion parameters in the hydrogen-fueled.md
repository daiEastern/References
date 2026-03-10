

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the International Journal of Hydrogen Energy](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the International Journal of Hydrogen Energy

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# In-depth analysis of the key combustion parameters in the hydrogen-fueled Wankel rotary engine

Shanshan Guo<sup>a</sup>, Hao Meng<sup>a,\*</sup>, Qiang Zhan<sup>a</sup>, Changwei Ji<sup>b</sup>, Du Wang<sup>c,\*\*</sup>

<sup>a</sup> School of Machinery and Automation, Weifang University, Weifang, 261000, PR China

<sup>b</sup> College of Mechanical and Energy Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

<sup>c</sup> Institute of Engineering Thermophysics, Chinese Academy of Sciences, Beijing, 100190, PR China

## ARTICLE INFO

Handling Editor: Dr M Mahdi Najafpour

### Keywords:

Hydrogen  
Wankel rotary engine  
Combustion parameters  
NO emission  
Support vector machine

## ABSTRACT

Hydrogen-fueled Wankel rotary engine is considered the potential carbon-free power device. Due to the special structure and operating mode, the heat release process of the Wankel rotary engine is significantly different from the piston engine. To understand the heat release process and further optimize its combustion, the present work conducts a series of experiments, such as engine speed, excess air ratio and qualitative control experiments, to analyze the key combustion parameters under different conditions. The main results are as follows: Both engine speed and excess air ratio play important roles in flame development and propagation. In particular, the excess air ratio only affects the early stage of flame propagation due to its impact on the later stage is covered by in-cylinder turbulence. CA0-10 is prolonged from 15.9 to 11.2°CA while CA50-90 does not show regular changes when the excess air ratio is reduced from 2.0 to 1.2. For qualitative control mode, variation of combustion parameters will become the obstacle to expanding lean flammable limits. In particular, the distribution of CA10 and CA50 or CA90 and CA50 can be fitted by linear regression, and the gradient and intercept of the fitted line can be used to represent engine speed and excess air ratio. 1000 r/min corresponds to 1.07 gradient and 2500 r/min is 1.27. NO emission is closely related to time-based CA0-10 and CA10-90 that can be applied as the independent variable of the Support Vector Machine with radial basis function kernel function to predict NO emission, and the maximum coefficient of determination is 0.92.

## 1. Introduction

Wankel rotary engine (WRE) [1], as a type of ICE, has the merits of high power density, smooth operation, and simple and compact structure [2]. Compared with common reciprocating piston engines, WRE has significant advantages in powertrain assembly [3]. However, WRE fueled with traditional fossil fuels, such as gasoline or diesel, usually has low combustion efficiency and poor HC and CO emissions [4]. In addition, the unidirectional in-cylinder flow field causes an unfavorable unburnable zone in the combustion engine, which further deteriorates the efficiency and emission of WRE [5].

Recently, like many measures [6,7] to reduce carbon emissions from ICEs, hydrogen has been considered an eco-friendly ICE fuel due to its carbon-free characteristics [8], which can completely eliminate carbon-based emissions like with lithium-ion batteries [9] and fuel cells

[10] and is conducive to solving the CO<sub>2</sub> emission issues in the ICE application [11]. Besides, hydrogen has fast laminar burning velocity [12], low ignition energy [13], wide flammable limits [14] and short quenching distance [15], which leads to excellent combustion characteristics of hydrogen-fueled ICEs [16]. In particular, hydrogen-fueled WRE has been proven to be a potential carbon-free power system. On the one hand, hydrogen significantly improves the poor combustion [17] and emission characteristics [18] of WRE, such as serious quenching effect and hostile ignition atmosphere [19]. On the other hand, the structure and operation mode of WRE effectively solve the problems of high-tendency backfire [20] and poor power characteristics [21] when hydrogen is considered as the fuel of reciprocating piston engines. Meng et al. found that hydrogen-fueled WRE has completely different backfire mechanisms compared to hydrogen-fueled reciprocating piston engines [22] and similar power per liter to gasoline-fueled

\* Corresponding author.

\*\* Corresponding author.

E-mail addresses: [menghaowfu@163.com](mailto:menghaowfu@163.com), [menghao@wfu.edu.cn](mailto:menghao@wfu.edu.cn) (H. Meng), [wangdu@iet.cn](mailto:wangdu@iet.cn) (D. Wang).

reciprocating piston engines [23]. Especially, hydrogen has been proven to be satisfactorily applied in WRE with few modifications [24].

Although hydrogen has above-mentioned advantages as the fuel of WRE, its extremely fast burning velocity makes the hydrogen-fueled WRE heat release process have a more significant impact on the performance of WRE. Especially, inappropriate heat release processes can cause severe knock [25], which frequently occurs in hydrogen-fueled ICEs. The heat release process is closely related to the efficiency and emission of ICEs. A suitable heat release process is conducive to approaching to ideal Otto cycle and thus achieving high output power and brake thermal efficiency. Yang et al. [26] found that ignition timing influences the power, efficiency, stability and reliability of hydrogen-fueled WRE by changing the heat release process. Wang et al. [27] numerically concluded by an ammonia-hydrogen dual-fueled WRE that different flame development and propagation process corresponds to different indicated thermal efficiency and indicated mean effective pressure of tested WRE engine. In particular, due to different structures and operation modes, the flame development and propagation process of WRE and reciprocating piston engine are obviously distinguishing and the optimal CA50 of hydrogen-fueled WRE and reciprocating piston engine is 35–40°CA after top dead center (ATDC) [28] and 8–10°CA ATDC [29], respectively. In addition, NOx emission is the main pollutant emission, and according to the extended Zeldovich mechanism [30], the NOx in hydrogen-fueled ICEs is closely influenced by the combustion temperature, which is the main parameter of the heat release process. Chen et al. [31] found that the combustion process induced by different in-cylinder mixture stratification leads to different thermal efficiency and NOx emission and a suitable combustion process can enable NOx emission to meet emission regulations. In addition, Bao et al. [32] concluded that variable valve timing (VVT) also affects thermal efficiency and NOx emission by influencing the heat release process. Meng et al. [33] found that since the in-cylinder combustion velocity and temperature of hydrogen-fueled WRE are close to the excess air ratio, the heat release process plays an important role in the NOx formation, and so does ignition timing [34]. In particular, the performance of hydrogen-fueled ICE is limited by knock, one of abnormal combustion in ICEs, the occurrence and intensity of which greatly depends on the in-cylinder heat release process. The fast heat release process usually corresponds to severe knock and some methods such as exhaust gas recirculation (EGR) [35], lean combustion [36], blending inertial gas [37] or fuel [38], etc. can suppress the knock by prolonging the heat release process.

Overall, the heat release process significantly impacts the performance of hydrogen-fueled ICE. However, most of the research are conducted based on the qualitative relationship between the heat release process and performance, and less pays attention to in-depth research about the heat release process, especially for WRE. Due to excellent power performance and high reliability, hydrogen-fueled WRE has been proven to be a potential carbon-free power device. However, it has a special heat release process due to its unique structure and operation mode, and there is still limited research in related areas. Hence, the present work aims to conduct detailed research work relevant to the heat release process of hydrogen-fueled WRE and analyze the key combustion parameters. This work can be divided into three parts: The first and the second parts experimentally investigate the heat release process under varied engine speed and excess air ratio, respectively; the third part experimentally discusses the heat release process during the operation of qualitative-control hydrogen-fueled WRE from 1000 r/min to 2500 r/min. In particular, this work establishes the quantitative relationship between the heat release process and NO emission to understand the formation of NO emission in hydrogen-fueled WRE.

| Nomenclature |                        |             |                             |
|--------------|------------------------|-------------|-----------------------------|
| <i>ATDC</i>  | After top dead center  | <i>HC</i>   | Hydrocarbon                 |
| <i>BTDC</i>  | Before top dead center | <i>ICEs</i> | Internal combustion engines |

(continued on next column)

(continued)

| Nomenclature   |                                                              |            |                              |
|----------------|--------------------------------------------------------------|------------|------------------------------|
| <i>CO</i>      | Carbon monoxide                                              | <i>LBV</i> | Laminar burning velocity     |
| <i>CO2</i>     | Carbon dioxide                                               | <i>MBT</i> | Maximum brake thermal        |
| <i>CA0-10</i>  | Crank angle intervals between 0 and 10% total heat release   | <i>NO</i>  | Nitric oxide                 |
| <i>CA10</i>    | Crank angle of 10% total heat release                        | <i>NOx</i> | Nitrogen oxides              |
| <i>CA10-50</i> | Crank angle intervals between 10% and 50% total heat release | <i>RBf</i> | Radial basis function        |
| <i>CA10-90</i> | Crank angle intervals between 10% and 90% total heat release | <i>R2</i>  | Coefficient of determination |
| <i>CA50</i>    | Crank angle of 50% total heat release                        | <i>SVM</i> | Support vector machine       |
| <i>CA50-90</i> | Crank angle intervals between 50% and 90% total heat release | <i>TDC</i> | Top dead center              |
| <i>CA90</i>    | Crank angle of 90% total heat release                        | <i>VVT</i> | Variable valve timing        |
| <i>ECU</i>     | Electronic control unit                                      | <i>WOT</i> | Wide-open throttle           |
| <i>EGR</i>     | Exhaust gas recirculation                                    | <i>WRE</i> | Wankel rotary engine         |

## 2. Experimental methodology and apparatus

### 2.1. Methodology

The present work aims to conduct detailed work relevant to the heat release process in the hydrogen-fueled WRE. The main content includes the heat release process at varied operating conditions, the relationship between key combustion parameters, and the relationship between NO emission and key combustion parameters. This work can be divided into three parts: (1) The first part discusses the heat release process at varied engine speeds from 1000 r/min to 3000 r/min. In this part, hydrogen-fueled WRE operates under wide-open throttle conditions, and the ignition timing and excess air ratio are fixed at the top dead center (TDC) and 1.4; (2) The second part analyzes the heat release process at varied excess air ratio from 1.2 to 2.0. In this part, hydrogen-fueled WRE also operates under wide-open throttle (WOT) conditions, and engine speed and ignition timing are fixed at 2000 r/min and TDC; (3) The third part investigates the heat release process during the operation of qualitative control hydrogen-fueled WRE. In this part, the engine speed is changed from 1000 r/min to 2500 r/min at intervals of 500 r/min while the excess air ratio is changed from 1.0 to 3.0 at intervals of 0.2, and hydrogen-fueled WRE is operated under WOT, maximum brake torque (MBT) ignition timing conditions. In particular, to guarantee the reliability of data, 1000 consecutive cycles of each case were recorded.

Due to the lack of readily available hydrogen-fueled WRE, a gasoline-fueled WRE was refitted to achieve work objectives, including the following modifications: Firstly, a self-developed port injection hydrogen supply system is added and the original gasoline supply system is completely removed; Secondly, a self-developed electronic control unit (ECU) is applied and connected with original ECU in series. The self-developed ECU can control the ignition timing and hydrogen injection; Thirdly, to obtain in-cylinder pressure signals, an in-cylinder pressure sensor is installed on the leading spark plug. In particular, since the original trigger wheel of the tested WRE is special, which is asymmetrical 36-2-2-2, and the applied combustion analyzer can not recognize it, a self-designed trigger wheel with 24-1 gears is installed on the eccentric shaft. The modifying details are shown in Fig. 1.

Some key combustion parameters are discussed in this work, including CA10, CA50, CA90 (10%, 50% and 90% total heat release corresponding crank angle, respectively), CA0-10, CA10-50, CA50-90, CA10-90 (crank angle intervals between 0 and 10%, 10% and 50%, 50% and 90%, 10% and 90% total heat release, respectively). Besides, since the same crank angle interval at different engine speeds corresponds to different times, this work defines standardized combustion parameters based on 1000 r/min. Take standardized CA0-10 as an example, the calculation formula is as Eq. (1):

![A photograph of a modified WRE engine setup. Labels with yellow arrows point to various components: '22 gears trigger wheel' at the top left, 'Intake manifold' in the center, 'Hydrogen nozzle' below the intake manifold, 'Piezoelectric pressure sensor' to the right of the hydrogen nozzle, and 'Photocurrent magnetic sensor' on the left side of the engine block.](7e2f2d03a5dda38b038fd4884629a2b4_img.jpg)

A photograph of a modified WRE engine setup. Labels with yellow arrows point to various components: '22 gears trigger wheel' at the top left, 'Intake manifold' in the center, 'Hydrogen nozzle' below the intake manifold, 'Piezoelectric pressure sensor' to the right of the hydrogen nozzle, and 'Photocurrent magnetic sensor' on the left side of the engine block.

Fig. 1. Modifying details of tested WRE.

$$\text{Standardized CA}0-10 = \frac{N}{1000} * \text{CA}0-10_{(N)} \quad (1)$$

where  $N$  is engine speed and  $\text{CA}0-10_{(N)}$  is the  $\text{CA}0-10$  at  $N$  engine speed.

### 2.2. Apparatus

A Mazda 13B WRE produced in 2002 is applied in the present work, which is double cylinders, water cooling, natural aspiration, side intake and exhaust, port injection, and double spark plugs. The specification of the tested WRE is shown in Table 1.

Some apparatuses are used in this work to monitor engine operation and record experimental data: (1) Engine speed and throttle percentage are controlled by Powerlink CAC6 AC dynamometer. In particular, the whole experiment is carried out based on  $n1/P$  mode; (2) Hydrogen flow rate is monitored by a smart gas system, which includes Sevenstar D07-60B thermal mass flow meter, and air flow rate is monitored by Tociel 20N060 thermal mass flow meter; (3) In-cylinder pressure is measured by Kistler 6117BFD17 piezoelectric pressure sensor and recorded by Kibox combustion analyzer; (4) NO emission is monitored by Horiba MEXA-7100DEGR emission analyzer; (5) The real-time excess air ratio is measured by Horiba MEXA-730λ wide-range lambda analyzer and the oxygen sensor is installed on the exhaust pipe near exhaust port. The detailed information and error analysis are shown in Table 2 and the schematic diagram of the experimental system is shown in Fig. 2.

## 3. Results and discussion

### 3.1. Engine speed

Fig. 3 shows the normal (a) and standardized (b) key combustion parameters at varied engine speeds. It can be found from Fig. 3a that based on crank angle, there is no significant difference in  $\text{CA}0-10$  as the engine speed is changed from 1000 r/min to 3000 r/min, while  $\text{CA}50$  and  $\text{CA}10-90$  are retarded and prolonged, respectively. The reasons are as follows: In WRE, limited by the structure, the spark plug electrode needs to be located in the spark plug hole opened on the cylinder body

**Table 2**  
Experimental apparatus and errors.

| Parameter                             | Uncertainty                                                                | Manufacturer | Type          |
|---------------------------------------|----------------------------------------------------------------------------|--------------|---------------|
| Engine speed                          | $\le \pm 1$ rpm                                                            | Power link   | CAC6          |
| Torque                                | $\le \pm 0.4\%$ F.S.                                                       | Power link   | CAC6          |
| Hydrogen and methane volume flow rate | $\le \pm 0.02$ L/min                                                       | Seven star   | D07-60B       |
| Air volume flow rate                  | $\le \pm 0.1$ L/min                                                        | Tociel       | 20N060        |
| Air-to-fuel ratio                     | $\le \pm 0.007$                                                            | Horiba       | MEXA-730λ     |
| In-cylinder pressure                  | $\le \pm 0.3$ bar                                                          | Kistler      | 6117BFD17     |
| NO emissions                          | Deviation: $\le \pm 0.1\%$ of the measured value<br>Sensitivity: 1 ppm vol | Horiba       | MEXA-7100DEGR |

[39]. To reduce cylinder-to-cylinder leakage, the spark plug hole usually has a small hole diameter [40], resulting in weaker turbulence intensity and poor charge exchange. With increasing the engine speed, enhanced in-cylinder turbulent intensity promotes charge exchange between the combustion chamber and spark plug hole, thus shortening standardized  $\text{CA}0-10$  as shown in Fig. 3b. However, the promoting impacts are balanced by increasing engine speed, hence  $\text{CA}0-10$  shows no significant change, that is, when only considering the crank angle, the engine speed has no significant effect on the formation of the flame kernel. On the other hand, since flame propagation is mainly located in the combustion chamber,  $\text{CA}50$  and  $\text{CA}10-90$  are significantly affected by in-cylinder turbulence, therefore, a retarded  $\text{CA}50$  and a prolonged  $\text{CA}10-90$  are obtained at high engine speed. However,  $\text{CA}10-90$  is shortened based on the time as shown in Fig. 3b. When engine speed is increased from 1000 r/min to 3000 r/min, standardized  $\text{CA}0-10$  and  $\text{CA}10-90$  are shortened by 64.6% and 59.1%, respectively.

### 3.2. Excess air ratio

Fig. 4a illustrates the key combustion parameters at varied excess air ratios and Fig. 4b is the laminar burning velocity (LBV) of hydrogen/air at normal temperature and pressure, which is calculated by the Chemkin software using the Burke mechanism [41]. It can be found that both  $\text{CA}0-10$  and  $\text{CA}10-90$  are shortened as the excess air ratio is reduced. When the excess air ratio is reduced from 2.0 to 1.2,  $\text{CA}0-10$  is reduced from 18.9°CA to 11.2°CA with about 41% reduction and  $\text{CA}10-90$  is reduced from 38.5°CA to 35.0°CA with about 9.1% reduction, indicating that the excess air ratio has a more significant impact on the flame development process. In addition,  $\text{CA}50$  is advanced with the decrease of excess air ratio. The shortening of  $\text{CA}0-10$  and  $\text{CA}10-90$  and the advancing of  $\text{CA}50$  are mainly due to shortened ignition delay and accelerated combustion velocity as shown in Fig. 4b. However, when the excess air ratio is reduced from 2.0 to 1.2, the LBV is increased from 48.9 cm/s to 166.8 cm/s with a 2.4 times increase, while the  $\text{CA}10-90$  is only shortened by 9.1%. This indicates that the in-cylinder flow field has a significant influence on flame propagation, thereby weakening the influence of changes in flame velocity itself.

Fig. 5 shows the  $\text{CA}10-50$  and  $\text{CA}50-90$  and their corresponding variance in 1000 consecutive cycles. It can be concluded from Fig. 5 that as the excess air ratio is increased from 1.2 to 2.0,  $\text{CA}10-50$  is gradually prolonged from 15.9°CA to 11.2°CA while  $\text{CA}50-90$  does not show regular changes, which indicates that the fuel characteristic can only affect the early stage of flame propagation, and as the eccentric shaft rotates away from the TDC, turbulence intensity in the combustion chamber increases in the later stage of flame propagation [42], thereby greatly weakening the influence of fuel itself burning velocity on the flame propagation. Hence, it is important to focus on strengthening the early stage of the flame propagation to improve performance for hydrogen-fueled WRE. In addition, it also can be illustrated from Fig. 5 that both variances of  $\text{CA}10-50$  and  $\text{CA}50-90$  are decreased first and

**Table 1**  
Engine specification.

| Specification        | Value/Form                      |
|----------------------|---------------------------------|
| Number of rotors     | 2                               |
| Cooling method       | Water-cooled                    |
| Ignition source      | Spark plug                      |
| Intake method        | Side-ported, natural aspiration |
| Exhaust method       | Side-ported                     |
| Generating radius/mm | 105                             |
| Width of rotor/mm    | 80                              |
| Displacement/L       | 0.654L                          |
| Compression ratio    | 10                              |
| Eccentricity/mm      | 15                              |
| Power output         | 121 kW/5500 rpm                 |
| Intake timing/(°CA)  | 3° ATDC, 38° ABDC               |
| Exhaust timing/(°CA) | 80° BBDC, 3° BTDC               |

![Schematic diagram of the experimental system. The diagram shows a hydrogen supply system (3, 4, 5, 6, 7, 8) connected to an injector (10) on an engine (14). The engine is equipped with sensors (18, 19, 20, 21) and a Lambda analyzer (13). The HECU (11) controls the system, with data lines (a1, a2) connecting to a calibration computer (12).](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

----- Signal line    ----- Data line

Schematic diagram of the experimental system. The diagram shows a hydrogen supply system (3, 4, 5, 6, 7, 8) connected to an injector (10) on an engine (14). The engine is equipped with sensors (18, 19, 20, 21) and a Lambda analyzer (13). The HECU (11) controls the system, with data lines (a1, a2) connecting to a calibration computer (12).

**Fig. 2.** The schematic diagram of the experimental system

1. Air cleaner 2. Mass flow meter of air 3. Container of hydrogen 4. Pressure regulating valve of hydrogen 5. Pressure meter of hydrogen 6. Hydrogen flow display 7. Volumetric flowmeter of hydrogen 8. Backfire arrestor of hydrogen 9. Smart gas box 10. Injector of hydrogen 11. HECU (Hydrogen Electronic Control Unit) 12. Calibration computer 13. Kibox 14. Trailing plug 15. Leading plug 16. Charger amplifier 17. Analog-digital converter 18. Exhaust sampling 19. Emissions analyzer 20. Oxygen sensor 21. Lambda analyzer a1. Data signals from HECU to calibration computer a2. Control signals from calibration computer to HECU b. Signals from sensors to HECU.

![Figure 3: Normal (a) and standardized (b) combustion parameters at varied engine speed. Graph (a) shows CA0-10, CA10-90, and CA50 vs Engine speed (r/min). Graph (b) shows Standardized CA0-10 and CA10-90 vs Engine speed (r/min).](09af5b86cf9391543d22db5f2129b3ca_img.jpg)

(a)

(b)

Figure 3: Normal (a) and standardized (b) combustion parameters at varied engine speed. Graph (a) shows CA0-10, CA10-90, and CA50 vs Engine speed (r/min). Graph (b) shows Standardized CA0-10 and CA10-90 vs Engine speed (r/min).

**Fig. 3.** Normal (a) and standardized (b) combustion parameters at varied engine speed.

![Figure 4: Key combustion parameters at varied excess air ratios (a) and laminar burning velocity of hydrogen/air at normal temperature and pressure (b). Graph (a) shows CA0-10, CA10-90, and CA50 vs Excess air ratio. Graph (b) shows Laminar burning velocity (cm/s) vs Excess air ratio.](a30a7877bf2f45b837a9382e22067ad0_img.jpg)

(a)

(b)

Figure 4: Key combustion parameters at varied excess air ratios (a) and laminar burning velocity of hydrogen/air at normal temperature and pressure (b). Graph (a) shows CA0-10, CA10-90, and CA50 vs Excess air ratio. Graph (b) shows Laminar burning velocity (cm/s) vs Excess air ratio.

**Fig. 4.** Key combustion parameters at varied excess air ratios (a) and laminar burning velocity of hydrogen/air at normal temperature and pressure (b).

then increased with reducing the excess air ratio. The high variance at 2.0 excess air ratio is mainly caused by slow burning velocity while the high variance at 1.2 excess air ratio is attributed to the knock [43]. In addition, all variances of CA50-90 are higher than that of corresponding CA10-50, which further explains that unstable in-cylinder turbulence

has a more significant impact on the later stage of flame propagation. In particular, severe knock caused by auto-ignition end gas usually occurs in the later stage of flame propagation, therefore, the variance of CA50-90 is about 1.7 times that of CA10-50 at 1.2 excess air ratio.

![Figure 5: A dual-axis line graph showing CA10-50 and CA50-90 (left axis, 10 to 30) and their variance (right axis, 0.0 to 2.8) versus excess air ratio (1.2 to 2.0). CA10-50 is represented by a solid red line, CA50-90 by a solid blue line, and their respective variances by dashed lines. The variance of CA10-50 increases from approximately 0.4 to 1.2, while the variance of CA50-90 decreases from approximately 2.7 to 1.3 as the excess air ratio increases.](7a3561af571faf036baa93f5f4b1bdb9_img.jpg)

Figure 5: A dual-axis line graph showing CA10-50 and CA50-90 (left axis, 10 to 30) and their variance (right axis, 0.0 to 2.8) versus excess air ratio (1.2 to 2.0). CA10-50 is represented by a solid red line, CA50-90 by a solid blue line, and their respective variances by dashed lines. The variance of CA10-50 increases from approximately 0.4 to 1.2, while the variance of CA50-90 decreases from approximately 2.7 to 1.3 as the excess air ratio increases.

Fig. 5. CA10-50 and CA50-90 and their variance at varied excess air ratio.

### 3.3. Qualitative control

Fig. 6 shows the standardized CA0-10 and CA10-90 at varied engine speeds and excess air ratio with MBT ignition timing. It can be found from Fig. 6 that for all engine speeds, standardized CA0-10 and CA10-90 are gradually prolonged with the rise of excess air ratio. This indicates that even if the ignition timing is adjusted (high excess air ratio usually corresponds to an advanced MBT ignition timing, which can improve the combustion thermal atmosphere and thus promote combustion), the excess air ratio still shows dominating impacts on ignition delay and burning velocity. Besides, both standardized CA0-10 and CA10-90 are also gradually prolonged as engine speed is decreased, which is mainly due to the enhanced charge exchange and fastened flame propagation caused by accelerated in-cylinder turbulence. It is worth noting that the sensitivities of standardized CA0-10 and CA10-90 to engine speed are gradually reduced when the charge is changed from lean to stoichiometric ratio combustion. Taking standardized CA0-10 as the example, when engine speed is raised from 1000 r/min to 2500 r/min, standardized CA0-10 is shortened from 49.1°CA to 10.1°CA with a decrease of 79.4% at 3.0 excess air ratio while standardized CA0-10 is only shortened from 4.6°CA to 2.9°CA with a decrease of 36.7% at stoichiometric ratio.

Fig. 7 illustrates the variance of standardized CA0-10 and CA10-90 under qualitative control. It can be found that on the premise of constant excess air ratio, except for 2500 r/min, there is no obvious

![Figure 6: A dual-axis line graph showing standardized CA0-10 (left axis, 0 to 50) and CA10-90 (right axis, 10 to 50) versus excess air ratio (1.0 to 3.0) for engine speeds of 1000, 1500, 2000, and 2500 r/min. Both metrics increase with excess air ratio, with higher engine speeds resulting in shorter durations.](3ef2266eb61ae3929cdae1742c1f526e_img.jpg)

Figure 6: A dual-axis line graph showing standardized CA0-10 (left axis, 0 to 50) and CA10-90 (right axis, 10 to 50) versus excess air ratio (1.0 to 3.0) for engine speeds of 1000, 1500, 2000, and 2500 r/min. Both metrics increase with excess air ratio, with higher engine speeds resulting in shorter durations.

Fig. 6. Standardized CA0-10 and CA10-90 under qualitative control.

![Figure 7: A dual-axis line graph showing the variance of standardized CA0-10 (left axis, 0.0 to 2.5) and CA10-90 (right axis, 0.0 to 1.5) versus excess air ratio (1.0 to 3.0) for engine speeds of 1000, 1500, 2000, and 2500 r/min. The variance of CA10-90 generally increases with excess air ratio, while the variance of CA0-10 shows a more complex trend, particularly at 2500 r/min.](bec3b1d6f15b643228b0da0a7d47bdbd_img.jpg)

Figure 7: A dual-axis line graph showing the variance of standardized CA0-10 (left axis, 0.0 to 2.5) and CA10-90 (right axis, 0.0 to 1.5) versus excess air ratio (1.0 to 3.0) for engine speeds of 1000, 1500, 2000, and 2500 r/min. The variance of CA10-90 generally increases with excess air ratio, while the variance of CA0-10 shows a more complex trend, particularly at 2500 r/min.

Fig. 7. The variance of standardized CA0-10 and CA10-90 under qualitative control.

difference in the variance of CA0-10 at varied engine speeds and the variance of CA0-10 at 2500 r/min is slightly lower than that of those three. In addition, there is also no obvious difference in the variance of CA0-10 when the excess air ratio is lower than 2.0, however, the variance of CA0-10 is gradually increased as the excess air ratio is increased from 2.0 to 3.0. This means that high engine speed and approaching stoichiometric ratio conditions are conducive to slightly improving the stability of flame kernel formation. It also can be concluded that unlike CA0-10, engine speed and excess air ratio have significant influences on the variance of CA10-90. As the excess air ratio is increased or engine speed is decreased, a more stable flame propagation will be obtained. In general, although qualitative control is an excellent control load method for hydrogen-fueled WRE [44], the negative effect on the heat release process also needs to be considered, especially for low engine speed and ultra-lean combustion conditions.

Fig. 8 discusses the relationship between CA10 and CA50 of 1000 consecutive cycles at varied excess air ratios under 1000 r/min conditions in the qualitative control hydrogen-fueled WRE. It can be illustrated in Fig. 8 that the distribution of CA10 and CA50 of 1000 consecutive cycles conforms to linear distribution well, and the linear distribution with a similar gradient gradually moves away from the Y-axis as the excess air ratio is decreased. According to the fitted data, the

![Figure 8: A scatter plot showing the relationship between CA10/°CA ATDC (X-axis, 12 to 34) and CA50/°CA ATDC (Y-axis, 32 to 44) for 1000 consecutive cycles at various excess air ratios. Data points are color-coded by excess air ratio (3.0, 2.8, 2.6, 2.4, 2.2, 2.0) and fitted with linear regression lines. The lines show a positive correlation, with the gradient becoming less steep as the excess air ratio decreases.](d6226b6d22b1babc1eeeb93e07cc9cc4_img.jpg)

Figure 8: A scatter plot showing the relationship between CA10/°CA ATDC (X-axis, 12 to 34) and CA50/°CA ATDC (Y-axis, 32 to 44) for 1000 consecutive cycles at various excess air ratios. Data points are color-coded by excess air ratio (3.0, 2.8, 2.6, 2.4, 2.2, 2.0) and fitted with linear regression lines. The lines show a positive correlation, with the gradient becoming less steep as the excess air ratio decreases.

Fig. 8. The relationship between CA10 and CA50 at varied excess air ratios under 1000 r/min and MBT ignition timing.

gradient of 3.0, 2.0 and 1.0 excess air ratio is 0.94, 1.11 and 1.05, respectively. This may mean that this gradient and intercept can be used to represent the engine speed and excess air ratio, and thus simplifying the monitor system of hydrogen-fueled WRE.

Fig. 9a and b display the fitted line gradient and intercept of CA10 and CA50 data distribution in qualitative control hydrogen-fueled WRE, respectively. It can be found from Fig. 9a that the gradients of varied excess air ratio randomly fluctuate with a certain range at the constant engine speed, and except for 2500 r/min, the gradients of the other three engine speeds have no significant difference. According to the mean value calculation, the mean gradient of engine speed sorted by increase are 1.07, 1.08, 1.12 and 1.27, respectively, which are positively correlated with engine speed. This indicates that engine speed may be represented by this parameter, which needs more experiment and data. In Fig. 9b, the intercept of the fitted line is globally decreased as the excess air ratio is increased, and high engine speed usually corresponds to a low intercept at a given excess air ratio. In particular, the intercept data can be fitted by linear regression [45] and the fitted lines of intercept have similar gradients as shown in the legend of Fig. 9b. Therefore, for the given engine speed, the excess air ratio can be represented by the intercept of the fitted line. On the whole, the impacts of engine speed and excess air ratio can be quantitatively reflected through the derivative parameters of the combustion parameters, meaning that the monitor of engine speed and excess air ratio may be replaced by the combustion monitor to a certain extent.

Similar to the relationship between CA10 and CA50, the data distribution of CA90 and CA50 also can be fitted by linear regression, and the fitting results are shown in Fig. 10. It can be found from Fig. 10 that the mean gradients are increased as the excess air ratio is decreased, and the mean gradient of engine speed sorted by increase are 0.61, 0.77, 0.79 and 0.82, respectively. The intercepts are globally decreased with rising excess air ratio. This is completely opposite to the results in Fig. 10b, which is due to the sequence of combustion parameters, where CA0-10 is earlier than CA50 while CA90 is later than CA50. Compared with the results in Figs. 9 and 10, the data in Fig. 9 has smaller fluctuation, which is mainly due to the faster burning velocity of burning early stage as shown in Fig. 5 and thus lower variation possible.

### 3.4. NO emission and combustion parameters

Fig. 11 illustrates the NO emission of qualitative control hydrogen-fueled WRE at varied standardized CA0-10 and CA10-90. It can be concluded from Fig. 11 that short standardized CA0-10 or CA10-90 usually corresponds to high NO emission. In hydrogen-fueled WRE, due to the lack of N atoms in fuel, the NO<sub>x</sub> mainly is thermal NO<sub>x</sub> [46]. According to the extended Zeldovich mechanism [47], the NO formation in hydrogen-fueled is mainly relevant to the temperature, oxygen

concentration and nitrogen concentration, where the influence of nitrogen can be neglected due to excess nitrogen in air. Qualitative control hydrogen-fueled WRE operates at lean or stoichiometric combustion, therefore, oxygen concentration can satisfy the formation of NO well. Short standardized CA0-10 and CA10-90 mean that the combustion occurs at a small space of the combustion chamber and thus generates high combustion temperature [48].

It can be concluded from Fig. 11 that there is a regular relationship between NO emissions and standardized CA0-10 and CA10-90, therefore, the present work applies Machine Learning methods to predict NO emission based on CA10, CA90 and engine speed (standardized CA0-10 and CA10-90 are calculated by these three parameters). Machine Learning methods are powerful data processing techniques [49,50]. Support Vector Machine (SVM) [51] with radial basis function (RBF) kernel function [52] is used in this work. The data was randomly divided 100 times and used for training different independent variable parameters to compare the effectiveness of the training. Fig. 12a displays the coefficient of determination (R2) of three cases, and the independent variables of each case are shown in the legend of Fig. 12. In particular, the gradient is the mean gradient in Fig. 9a to verify its substitutability for engine speed. The calculation equation of R2 is as Eq. (2):

$$R2 = 1 - \frac{\sum_{i=1}^{n} (y_{i,real} - y_{i,pre})^2}{\sum_{i=1}^{n} (y_{i,real} - y_{mean})^2} \quad (2)$$

where n is the number of the test set, i is the sequence number of data in the test set,  $y_{i,real}$  is the real value of ith data in the test set,  $y_{i,pre}$  is the prediction value corresponding to  $y_{i,real}$ , and  $y_{mean}$  is the mean value of test set.

In Fig. 12a, it can be concluded that all three cases can achieve satisfactory prediction accuracy, and the case with engine speed is globally better than the other two and the case with gradient is slightly globally better than the case only with CA10 and CA90. The maximum R2 of the case with engine speed, case with gradient and case only with CA10 and CA90 are 0.92, 0.94 and 0.92. The case with gradient being worse than the case with engine speed may mainly be attributed to the small amount of experimental data in this work, resulting in biased gradients. In particular, all three cases have some R2 lower than zero. This is mainly due to the fact that a large number of data without NO emissions are included in the training set when dividing the training and testing sets. Therefore, the model recommends separately dividing high NO emissions and low NO emissions when dividing the training set. Fig. 12b shows the prediction of NO emission and its corresponding test NO emission, it can be found although there is a significant deviation under high NO emission conditions, this deviation does not significantly affect the judgment of whether NO emissions are high due to its actual high NO emissions. Overall, SVM using the RBF kernel function can

![Figure 9: (a) Gradient of the fitted line vs. Excess air ratio and (b) Intercept of the fitted line vs. Excess air ratio. Both plots show data for engine speeds of 1000, 1500, 2000, and 2500 r/min.](096d7a8a21933900dad68d82ae8a97fb_img.jpg)

Figure 9 consists of two line graphs, (a) and (b), plotted against the Excess air ratio (ranging from 1.0 to 3.0).  
 Graph (a) shows the Gradient of the fitted line (y-axis, ranging from 0.8 to 1.5). Four data series are plotted for engine speeds: 1000 r/min (red squares), 1500 r/min (blue circles), 2000 r/min (green triangles), and 2500 r/min (purple inverted triangles). The gradients generally increase with engine speed and show some fluctuation with excess air ratio.  
 Graph (b) shows the Intercept of the fitted line (y-axis, ranging from -5 to 25). The same four engine speed data series are plotted. The intercepts generally decrease as the excess air ratio increases, and the values are higher for higher engine speeds.

Figure 9: (a) Gradient of the fitted line vs. Excess air ratio and (b) Intercept of the fitted line vs. Excess air ratio. Both plots show data for engine speeds of 1000, 1500, 2000, and 2500 r/min.

Fig. 9. The gradient (a) and intercept (b) of the fitted distribution of CA10 and CA50 in qualitative control hydrogen-fueled WRE.

![Figure 10: (a) Gradient and (b) Intercept of the fitted distribution of CA90 and CA50. Both plots show data for engine speeds of 1000, 1500, 2000, and 2500 rpm against the Excess air ratio (1.0 to 3.0).](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 10 consists of two line plots. Plot (a) shows the 'Gradient of the fitted line' on the y-axis (0.0 to 1.2) versus 'Excess air ratio/' on the x-axis (1.0 to 3.0). Plot (b) shows the 'Intercept of the fitted line' on the y-axis (-30 to 40) versus 'Excess air ratio/' on the x-axis (1.0 to 3.0). Both plots include data series for engine speeds of 1000, 1500, 2000, and 2500 rpm, represented by different line styles and markers. In plot (a), the gradient generally decreases as the excess air ratio increases. In plot (b), the intercept generally decreases as the excess air ratio increases.

Figure 10: (a) Gradient and (b) Intercept of the fitted distribution of CA90 and CA50. Both plots show data for engine speeds of 1000, 1500, 2000, and 2500 rpm against the Excess air ratio (1.0 to 3.0).

Fig. 10. The gradient (a) and intercept (b) of the fitted distribution of CA90 and CA50 in qualitative control hydrogen-fueled WRE.

![Figure 11: NO emission at varied standardized CA0-10 and CA10-90. A contour plot showing NO emission (ppm) as a function of Standardized CA0-10/°CA (0 to 25) and Standardized CA10-90/°CA (10 to 30).](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 11 is a contour plot titled 'NO emission/ppm'. The x-axis is 'Standardized CA0-10/°CA' (0 to 25) and the y-axis is 'Standardized CA10-90/°CA' (10 to 30). The color scale represents NO emission values from 0.000 (blue) to 7340 (red). The contours show that NO emission increases as both standardized crank angles increase, with higher values concentrated in the upper right region.

Figure 11: NO emission at varied standardized CA0-10 and CA10-90. A contour plot showing NO emission (ppm) as a function of Standardized CA0-10/°CA (0 to 25) and Standardized CA10-90/°CA (10 to 30).

Fig. 11. NO emission at varied standardized CA0-10 and CA10-90.

effectively predict the NO emissions during the operation of qualitative control hydrogen-fueled WRE based on CA10, CA90 and engine speed.

## 4. Conclusion

The present work experimentally analyzes the key combustion parameters in hydrogen-fueled WRE. The main conclusions are as follows.

1. Based on the crank angle, engine speed has no significant effect on the formation of the flame kernel while increasing engine speed will prolong the CA10-90. Based on the time, short CA0-10 and CA10-90 will be obtained at high engine speed.
2. Both CA0-10 and CA10-90 are shortened as the excess air ratio is decreased, and the impact of the excess air ratio on CA0-10 is significantly larger than that on CA10-90. The influence of excess air ratio on flame propagation is mainly reflected in the early stage of flame propagation. As the excess air ratio is increased, CA10-50 is gradually prolonged while CA50-90 shows no obvious changes.
3. When the ignition timing is fixed at MBT ignition timing, CA0-10 and CA10-90 based on time are shortened with increasing engine speed and decreasing excess air ratio. The sensitivities of CA0-10 and CA10-90 to engine speed are gradually reduced as changing from lean to stoichiometric combustion.
4. When the ignition timing is fixed at MBT ignition timing, the distribution of CA10 and CA50 or CA90 and CA50 can be fitted by linear regression. The gradient of the fitted line is related to engine speed

![Figure 12: (a) Training accuracy and (b) Comparison of prediction and test data. (a) shows the Coefficient of determination (R^2) vs. Number of serial. (b) shows Prediction NO emission vs. Test NO emission.](112f3fc5dde002caf1c91da443844204_img.jpg)

Figure 12 consists of two subplots. Subplot (a) shows the 'Coefficient of determination/' on the y-axis (-5 to 1) versus 'Number of serial/' on the x-axis (0 to 100). It includes data for 'CA10 and CA90', 'CA10 and CA90 with gradient', and 'CA10 and CA90 with speed'. Subplot (b) shows 'Prediction NO emission/ppm' on the y-axis (0 to 7000) versus 'Test NO emission/ppm' on the x-axis (0 to 7000). It compares prediction results with test data, showing R-squared values of 0.925, 0.748, and 0.551, and a dashed line for Y=X.

Figure 12: (a) Training accuracy and (b) Comparison of prediction and test data. (a) shows the Coefficient of determination (R^2) vs. Number of serial. (b) shows Prediction NO emission vs. Test NO emission.

Fig. 12. The training accuracy (a) and comparison of prediction and test data (b).

and the intercept of the fitted line is related to excess air ratio. For the fitted line relevant to both distributions, high engine speed corresponds to the large gradient. However, for the fitted line relevant to CA10 and CA50, the high excess air ratio corresponds to a large intercept, while for the fitted line relevant to CA90 and CA50, the high excess air ratio corresponds to a small intercept.

5. NO emission is closely related to CA0-10 and CA10-90 based on time. Short CA0-10 or CA10-90 based on time usually corresponds to high NO emission. SVM using RBF kernel function can effectively predict the NO emissions of qualitative control hydrogen-fueled WRE based on CA10, CA90 and engine speed.

This work experimentally analyzes the key combustion parameters and the relationship between the heat release process and NO emission. Overall, this work contributes to a deeper understanding of the combustion process in hydrogen-fueled WRE and provides important assistance for its optimization.

## CRediT authorship contribution statement

**Shanshan Guo:** Writing – original draft, Investigation. **Hao Meng:** Writing – original draft, Methodology, Investigation, Conceptualization. **Qiang Zhan:** Investigation. **Changwei Ji:** Validation, Supervision. **Du Wang:** Project administration.

## Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Acknowledgements

This work was supported by the Youth Fund of the National Natural Science Foundation of China (52406169).

## References

- [1] Fan B, Wu X, Pan J, Qi X, Fang J, Lu Q, et al. Research on the structure of pre-chamber and jet orifice of a turbulent jet ignition rotary engine fueled with methanol/gasoline blends. Appl Therm Eng 2023;229:120588. <https://doi.org/10.1016/j.applthermaleng.2023.120588>.
- [2] Fan B, Song A, Liu W, Jiang P, Xu L, Pan J, et al. Potential improvement in combustion performance of a natural gas rotary engine mixed with hydrogen by novel bluff-body. Energy 2024;295:131077. <https://doi.org/10.1016/j.energy.2024.131077>.
- [3] Bao J, Lei J, Tian G, Wang X, Wang H, Shi C. A review of the application development and key technologies of rotary engines under the background of carbon neutrality. Energy 2024;311:133447. <https://doi.org/10.1016/j.energy.2024.133447>.
- [4] Amrouche F, Erickson P, Park J, Varnhagen S. An experimental investigation of hydrogen-enriched gasoline in a Wankel rotary engine. Int J Hydrogen Energy 2014;39:8525–34. <https://doi.org/10.1016/j.ijhydene.2014.03.172>.
- [5] Ji C, Meng H, Wang S, Wang D, Yang J, Shi C, et al. Realizing stratified mixtures distribution in a hydrogen-enriched gasoline Wankel engine by different compound intake methods. Energy Convers Manag 2020;203. <https://doi.org/10.1016/j.enconman.2019.112230>.
- [6] Chen Z, Wang L, Wei Z, Wang Y, Deng J. Effect of components on the emulsification characteristic of glucose solution emulsified heavy fuel oil. Energy 2022;244. <https://doi.org/10.1016/j.energy.2022.123147>.
- [7] Chen Z, Li K, Liu J, Wang X, Jiang S, Zhang C. Optimal design of glucose solution emulsified diesel and its effects on the performance and emissions of a diesel engine. Fuel 2015;157:9–15. <https://doi.org/10.1016/j.fuel.2015.04.049>.
- [8] Zhang Y, Xiao Y, Abuelgasim S, Liu C. A brief review of hydrogen production technologies. Clean Energy Sci Technol 2024;2:117. <https://doi.org/10.18686/cest.v2i1.117>.
- [9] Zhang C, Luo L, Yang Z, Zhao S, He Y, Wang X, et al. Battery SOH estimation method based on gradual decreasing current, double correlation analysis and GRU. Green Energy Intell Transp 2023;2:100108. <https://doi.org/10.1016/j.geits.2023.100108>.
- [10] Waseem M, Amir M, Lakshmi GS, Harivardhagini S, Ahmad M. Fuel cell-based hybrid electric vehicles: an integrated review of current status, key challenges, recommended policies, and future prospects. Green Energy Intell Transp 2023;2:100121. <https://doi.org/10.1016/j.geits.2023.100121>.
- [11] Wang X, Gao J, Chen H, Chen Z, Zhang P, Chen Z. Diesel/methanol dual-fuel combustion: an assessment of soot nanostructure and oxidation reactivity. Fuel Process Technol 2022;237:107464. <https://doi.org/10.1016/j.fuproc.2022.107464>.
- [12] Zhu XM, Sun ZY, Liu XY. Impacts of hydrogen fraction and equivalence ratio on the explosion characteristics of ethanol/hydrogen mixtures. Fuel 2024;375:132620. <https://doi.org/10.1016/j.fuel.2024.132620>.
- [13] Liu XY, Sun ZY, Yi Y. Progress in spontaneous ignition of hydrogen during high-pressure leakage with the considerations of pipeline storage and delivery. Appl Energy Combust Sci 2024;20. <https://doi.org/10.1016/j.jaecs.2024.100290>.
- [14] Sun ZY, Liu SY. A comparative study on the turbulent explosion characteristics of syngas between CO-enriched and H<sub>2</sub>-enriched. Energy 2022;241:122941. <https://doi.org/10.1016/j.energy.2021.122941>.
- [15] Wang Y, Gao J, Gao J, Wang X, Song J, Tian G. Parametric modeling and optimization of the intake port in a naturally aspirated opposed rotary piston engine across the full speed range. Energy 2024;311:133326. <https://doi.org/10.1016/j.energy.2024.133326>.
- [16] Gurbuz H. The effect of H<sub>2</sub> purity on the Combustion, Performance, emissions, and energy costs in an spark ignition engine. Therm Sci 2020;24:37–49. <https://doi.org/10.2298/TSCI180705315G>.
- [17] Fan B, Li W, Zeng Y, Fan M, Yang H, Pan J, et al. The coupling effect of turbulent jet ignition and injection strategy on the combustion performance of a pure methanol rotary engine. Appl Therm Eng 2025;258:124544. <https://doi.org/10.1016/j.applthermaleng.2024.124544>.
- [18] Zhan Q, Meng H, Ji C, Yang J, Wang S. Realizing high-efficiency and low-emission load control of Wankel rotary engine by CH<sub>4</sub>/H<sub>2</sub> synergy, vol. 86; 2024. p. 427–33.
- [19] Wu L, Wu Y, Fan B, Pan J, Fan M, Yang H, et al. Evaluation of blunt body setting for improving the combustion performance of a jet ignition hydrogen/natural gas rotary engine. Int J Hydrogen Energy 2024;92:494–505. <https://doi.org/10.1016/j.ijhydene.2024.10.305>.
- [20] Gao J, Wang X, Song P, Tian G, Ma C. Review of the backfire occurrences and control strategies for port hydrogen injection internal combustion engines. Fuel 2022;307:121553. <https://doi.org/10.1016/j.fuel.2021.121553>.
- [21] Verhelst S, Wallner T. Hydrogen-fueled internal combustion engines. Prog Energy Combust Sci 2009;35:490–527. <https://doi.org/10.1016/j.pecs.2009.08.001>.
- [22] Meng H, Ji C, Su T, Yang J, Chang K, Xin G, et al. Analyzing characteristics of knock in a hydrogen-fueled Wankel rotary engine. Energy 2022;250:123828. <https://doi.org/10.1016/j.energy.2022.123828>.
- [23] Meng H, Ji C, Xin G, Yang J, Chang K, Wang S. Comparison of combustion, emission and abnormal combustion of hydrogen-fueled Wankel rotary engine and reciprocating piston engine. Fuel 2022;318:123675. <https://doi.org/10.1016/j.fuel.2022.123675>.
- [24] Meng H, Ji C, Wang S, Yang J. A review : centurial progress and development of Wankel rotary engine. Fuel 2023;335:127043. <https://doi.org/10.1016/j.fuel.2022.127043>.
- [25] Meng H, Ji C, Yang J, Xin G, Wang S. Statistically discussing impacts of knock type on the heat release process in hydrogen-fueled Wankel rotary engine. Int J Hydrogen Energy 2022. <https://doi.org/10.1016/j.ijhydene.2022.11.259>.
- [26] Yang J, Ji C, Wang S, Meng H. An experimental study on ignition timing of hydrogen Wankel rotary engine. Int J Hydrogen Energy 2022;47:17468–78. <https://doi.org/10.1016/j.ijhydene.2022.03.223>.
- [27] Wang S, Sun Y, Yang J, Wang H. Effect of excess air ratio and ignition timing on the combustion and emission characteristics of the ammonia-hydrogen Wankel rotary engine. Energy 2024;302:131779. <https://doi.org/10.1016/j.energy.2024.131779>.
- [28] Meng H, Ji C, Yang J, Wang S, Xin G, Chang K, et al. Experimentally investigating the asynchronous ignition on a hydrogen-fueled Wankel rotary engine. Fuel 2022;312:122988. <https://doi.org/10.1016/j.fuel.2021.122988>.
- [29] Heywood JB. Internal combustion engine fundamentals. 2018.
- [30] Glarborg P, Miller JA, Ruscic B, Klippenstein SJ. Modeling nitrogen chemistry in combustion. Prog Energy Combust Sci 2018;67:31–68. <https://doi.org/10.1016/j.pecs.2018.01.002>.
- [31] Chen W, Lu C, Zuo Q, Kou C, Shi R, Wang H, et al. Combustion characteristics analysis and performance evaluation of a hydrogen engine under direct injection plus lean burn mode. J Clean Prod 2024;470:143323. <https://doi.org/10.1016/j.jclepro.2024.143323>.
- [32] Lai F yu, Sun B gang, Zhang S wei, Wang K da, Luo Q he, Bao L zhi, et al. Experimental analysis and optimization of the variable valve timing on attaining high efficiency with low NOx emission of a direct-injected hydrogen engine. Fuel 2025;381:133199. <https://doi.org/10.1016/j.fuel.2024.133199>.
- [33] Meng H, Ji C, Yang J, Wang S, Chang K, Xin G. Experimental study of the effects of excess air ratio on combustion and emission characteristics of the hydrogen-fueled rotary engine. Int J Hydrogen Energy 2021;46:32261–72. <https://doi.org/10.1016/j.ijhydene.2021.06.208>.
- [34] Yun H, Bu Z, Yang Z, Wang L, Zhang B. Optimization of fuel injection timing and ignition timing of hydrogen fueled SI engine based on DOE-MPGA. Int J Hydrogen Energy 2023;48:9462–73. <https://doi.org/10.1016/j.ijhydene.2022.12.068>.
- [35] Safari H, Jazayeri SA, Ebrahimi R. Potentials of NOx emission reduction methods in SI hydrogen engines: simulation study. Int J Hydrogen Energy 2009;34:1015–25. <https://doi.org/10.1016/j.ijhydene.2008.10.029>.
- [36] Gürbüz H, Akçay H, Demirtürk S, Topalçı Ü. Techno-enviro-economic comparison analysis of a PEMFC and a hydrogen-fueled SI engine. Appl Therm Eng 2024;243:122528. <https://doi.org/10.1016/j.applthermaleng.2024.122528>.
- [37] Meng H, Ji C, Liu S, Yang J, Xin G, Hong H, et al. Research on the behavior of CO<sub>2</sub> on hydrogen-fueled Wankel rotary engine performance. Fuel 2023;335:127036. <https://doi.org/10.1016/j.fuel.2022.127036>.

- [38] Dinesh MH, Kumar GN. Effects of compression and mixing ratio on NH<sub>3</sub>/H<sub>2</sub> fueled Si engine performance, combustion stability, and emission. *Energy Convers Manag* 2022;15:100269. <https://doi.org/10.1016/j.enconman.2022.100269>.
- [39] Kawahara N, Tomita E, Hayashi K, Tabata M, Iwai K, Kagawa R. Cycle-resolved measurements of the fuel concentration near a spark plug in a rotary engine using an in situ laser absorption method. *Proc Combust Inst* 2007;31(III):3033–40. <https://doi.org/10.1016/j.proci.2006.08.088>.
- [40] Picard M, Tian T, Nishino T. Predicting gas leakage in the rotary engine-Part I: apex and corner seal. *J Eng Gas Turbines Power* 2016;138:1–8. <https://doi.org/10.1115/1.4031873>.
- [41] Burke MP, Chaos M, Ju Y, Dryer FL, Klippenstein SJ. Comprehensive H<sub>2</sub>/O<sub>2</sub> kinetic model for high-pressure combustion. *Int J Chem Kinet* 2012;44:444–74. <https://doi.org/10.1002/kin.20603>.
- [42] Bao J, Qu P, Wang H, Zhou C, Zhang L, Shi C. Implementation of various bowl designs in an HPDI natural gas engine focused on performance and pollutant emissions. *Chemosphere* 2022;303:135275. <https://doi.org/10.1016/j.chemosphere.2022.135275>.
- [43] Meng H, Ji C, Yang J, Chang K, Xin G, Wang S. A knock study of hydrogen-fueled Wankel rotary engine. *Fuel* 2022;321:124121. <https://doi.org/10.1016/j.fuel.2022.124121>.
- [44] Meng H, Ji C, Wang D, Xin G, Chang K, Yang J, et al. Research on the load control of hydrogen-fueled Wankel rotary engine. *Int J Hydrogen Energy* 2022;47: 16665–75. <https://doi.org/10.1016/j.ijhydene.2022.03.118>.
- [45] Zarei M, Bayati MR, Ebrahimi-Nik M, Rohani A, Hejazi B. Modelling the removal efficiency of hydrogen sulfide from biogas in a biofilter using multiple linear regression and support vector machines. *J Clean Prod* 2023;404:136965. <https://doi.org/10.1016/j.jclepro.2023.136965>.
- [46] Lu C, Chen W, Zuo Q, Kou C, Wang H, Xiao G, et al. Numerical investigation on gaseous fuel injection strategies on combustion characteristics and NO emission performance in a pure hydrogen engine. *Fuel* 2024;363:130911. <https://doi.org/10.1016/j.fuel.2024.130911>.
- [47] Ma DS, Sun ZY. Progress on the studies about NOx emission in PFI-H<sub>2</sub>ICE. *Int J Hydrogen Energy* 2020;45:10580–91. <https://doi.org/10.1016/j.ijhydene.2019.11.065>.
- [48] Chen W, He W, Ma Y, Yu S, Zuo Q, Kou C, et al. Numerical Investigation of flow and combustion process in a hydrogen direction injection rotary engine. *Fuel* 2025; 379. <https://doi.org/10.1016/j.fuel.2024.133100>.
- [49] Guo S, Ma L. A comparative study of different deep learning algorithms for lithium-ion batteries on state-of-charge estimation. *Energy* 2023;263:125872. <https://doi.org/10.1016/j.energy.2022.125872>.
- [50] Yu Q, Nie Y, Guo S, Li J, Zhang C. Machine learning enables rapid state of health estimation of each cell within battery pack. *Appl Energy* 2024;375:124165. <https://doi.org/10.1016/j.apenergy.2024.124165>.
- [51] Meng H, Zhan Q, Ji C, Yang J, Wang S. Identification, prediction and classification of hydrogen-fueled Wankel rotary engine knock by data-driven based on combustion parameters. *Energy* 2024;308:133029. <https://doi.org/10.1016/j.energy.2024.133029>.
- [52] Onyelowe KC, Gnananandarao T, Ebid AM. Estimation of the erodibility of treated unsaturated lateritic soil using support vector machine-polynomial and -radial basis function and random forest regression techniques. *Clean Mater* 2022;3. <https://doi.org/10.1016/j.clema.2021.100039>.