

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the International Journal of Electronics and Communications (AEU)](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the International Journal of Electronics and Communications (AEU)

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# An enhanced sliding window Fourier analysis with a time delay compensation for single-phase active power filter<sup>☆</sup>

Chakrit Panpean<sup>a</sup>, Phonsit Santiprapan<sup>b,\*</sup>, Jeerawan Homjan<sup>c</sup>, Kongpol Areerak<sup>d</sup>

<sup>a</sup> Department of Instrumentation and Electronics Engineering, King Mongkut's University of Technology North Bangkok, Bangkok 10800, Thailand

<sup>b</sup> Department of Electrical and Biomedical Engineering, Faculty of Engineering Prince of Songkla University, Songkhla 90110, Thailand

<sup>c</sup> Department of Mechatronics Engineering, Rajamangala University of Technology Suvarnabhumi, Nonthaburi 11000, Thailand

<sup>d</sup> School of Electrical Engineering, Institute of Engineering, Suranaree University of Technology, Nakhon Ratchasima 30000, Thailand

## ARTICLE INFO

### Keywords:

Harmonic detection  
Time delay compensation  
Active power filter  
Sliding window with Fourier analysis

## ABSTRACT

The performance of an active power filter (APF) to eliminate the harmonic in the power system depends, firstly, on the harmonic detection process. An accurate reference current calculation and time delay compensation for the harmonic detection process are therefore focused. This paper introduces the enhanced sliding window Fourier analysis (SWFA). The proposed technique is to combine the SWFA with Lagrange's equation. Herein, the amplitude-phase calculation of the SWFA method and the reference current prediction at two sampling times are the key techniques to improve harmonic detection for digital implementation. The hardware-in-the-loop simulation on an eZdsp™ F28335 board is used to verify and evaluate the performance of the proposed harmonic detection technique. The testing results indicated that the APF with the enhanced SWFA approach can compensate the time delay and calculate the harmonic and reactive currents. After compensation, it would also improve the power factor and reduce the percentage of total harmonic distortion within the IEEE standard 519 even though the voltage source is in sinusoidal or distorted conditions.

## 1. Introduction

Nowadays, power quality in generation, transmission, and distribution systems is an essential factor in modern power systems. A power converter in DG [1–7] has been increasing rapidly, and power quality issues have become more concerning. In the utilization, power electronic devices are an important part of converters such as DC/AC, AC/DC, and DC/DC power converters. These power converters generate harmonics in power systems [8]. Harmonics can significantly affect the efficiency and reliability of overall power systems [9]. For this problem, international standards have been established to define the permissible levels of THD in electrical systems at PCC, such as IEEE 519 [10] and EN50160 [11] standards. The aim of this work is to reduce the THD following the standards.

As mentioned before, the harmonic elimination is necessary. Presently, an APF is widely used because it provides high performance and can eliminate the harmonic in the various load conditions. However, the performance of harmonic elimination using the APF depends on four important components: APF structure, harmonic detection,

compensating current control, and DC bus voltage control. In order to perfectly eliminate the harmonic, accurate harmonic detection techniques are firstly required. Therefore, the objective of this work is to improve the harmonic detection performance.

In terms of harmonic detection techniques, from the literature reviews, it was found that harmonic detection can be classified into two main groups. The first group is the traditional approach. This group is operated in the ideal voltage source system, such as the PQ, SD [12], SRF [13], SWFA [14], PHF, and NN [15] techniques. The second group is the combined approach. This group is applied in the distorted voltage source system, such as RPQF, RSDF, RDQF, and RPHC techniques. However, in practice, these harmonic detection processes require a large numerical computation on a digital signal processor. The computational burden of the digital control platform leads to the delay time of harmonic detection. If there is a delay time between measurement and the reference current calculation, it can directly affect the performance of harmonic elimination using APF. In order to overcome this problem, a suitable time delay compensation should be considered carefully.

The strategies of time delay compensation are required. From the literature reviews, typically, the delay compensation for digital control

<sup>☆</sup> This article is part of a special issue entitled: 'from ECTI-CON 2024' published in AEUE - International Journal of Electronics and Communications.

\* Corresponding author.

E-mail address: [phonsit.s@psu.ac.th](mailto:phonsit.s@psu.ac.th) (P. Santiprapan).

| Nomenclature    |                                            |                                                                                                        |
|-----------------|--------------------------------------------|--------------------------------------------------------------------------------------------------------|
| APF             | active power filter                        | $i_C^*$ reference current                                                                              |
| SWFA            | sliding window Fourier analysis            | $A_1$ and $B_1$ coefficients of the fundamental current                                                |
| DG              | distributed generation                     | $N$ data points in one period                                                                          |
| THD             | total harmonic distortion                  | $N_0$ old data point                                                                                   |
| PCC             | points of common coupling                  | $N_0 + N$ new data point                                                                               |
| PQ              | instantaneous power theory                 | $T_s$ sampling time                                                                                    |
| SD              | synchronous detection                      | $C_h$ amplitude of Fourier series                                                                      |
| SRF             | synchronous reference frame                | $\phi_h$ phase angle of Fourier series                                                                 |
| PHF             | perfect harmonic compensation              | $\theta_v$ phase angle of the voltage                                                                  |
| NN              | neural network                             | $A_0$ DC component                                                                                     |
| RPQF            | robust instantaneous power with Fourier    | $i_{L1}$ fundamental load current                                                                      |
| RSDF            | robust synchronous detection with Fourier  | $A_1^{\text{old}}$ and $B_1^{\text{old}}$ coefficients old value of the fundamental current            |
| RDQF            | robust DQ axis with Fourier                | $i_C(n)$ compensating current                                                                          |
| RPHC            | robust perfect harmonic cancellation       | $i_C^*(n)$ reference current                                                                           |
| DB              | deadbeat control                           | $i_C^*(n+1), i_C^*(n+2), i_C^*(n+3)$ predictive reference current at the sampling time $n+1, n+2, n+3$ |
| RCG             | reference current generation               | $v_S$ source voltage                                                                                   |
| PC              | predictive control                         | $v_{PCC}$ PCC voltage                                                                                  |
| MPC             | model predictive control                   | $i_C$ compensating current                                                                             |
| M2PC            | modulated model predictive control         | $f_s$ source frequency                                                                                 |
| PLL             | phase locked-loop                          | $R_L$ total load resistance                                                                            |
| LPF             | low-pass filter                            | $R_{L1}$ and $R_{L2}$ load resistances                                                                 |
| PD              | phase detector                             | $R_T$ transmission line resistance                                                                     |
| multi-SOGI      | multi-second order generalized integrator  | $L_L$ total load inductance                                                                            |
| PLL             | frequency locked loop                      | $L_{L1}$ and $L_{L2}$ load inductances                                                                 |
| HIL             | hardware-in-the-loop                       | $L_T$ transmission line inductance                                                                     |
| $i_L$           | load current                               | $i_C(n+1), i_C(n+2), i_C(n+3)$ predictive compensating current at the sampling time $n+1, n+2, n+3$    |
| $A_h$ and $B_h$ | coefficients of the even and odd harmonics | $i_S$ source current                                                                                   |
| $i_{L1}(nT_s)$  | fundamental current                        | %THD percentage of total harmonic distortion                                                           |
| $i_{Lh}(nT_s)$  | harmonic current                           |                                                                                                        |

platforms has been presented in the predictive control approach, such as DB with Improved RCG method [16], PC, MPC with current signal generation [17,18], and M2PC with SD method [12] and current signal generation [19], which can be observed that the reference signal prediction at one sampling time in the harmonic detection process is necessary for the predictive control approaches. However, the prediction at one sampling time is not enough to achieve an accurate reference signal because the delay time from the computational burden of the harmonic detection process on the microcontroller board and the

transferring data between the microcontroller board and the external circuits can lead to one more delay time. Therefore, the reference signal prediction in the harmonic detection process should be considered at one more sampling times. This is an interesting point for this paper.

Focusing on an accurate harmonic detection performance, the reference current generation [16–18] requires the PLL [20] to generate a phase synchronization angle for the phase of the source current. Considering the conventional PLL algorithm, this process is used to calculate the reference source current. In the case of the distorted

Table 1

Comparative study of harmonic detection method for the delay compensation in single phase system.

| Publication Year | APF Structure                          | Harmonic Detection           | Prediction Horizon | Compensation Strategy                                                                                 | Conditions                                                                                                                                         |
|------------------|----------------------------------------|------------------------------|--------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| 2015 [21]        | Single-Phase Full-Bridge NPC Converter | Reference current generation | Not considered     | <ul style="list-style-type: none"> <li>Harmonic detection</li> <li>Power factor correction</li> </ul> | <ul style="list-style-type: none"> <li>Nonlinear load</li> <li>Load variation (Motor load connection)</li> <li>Ideal Voltage Source</li> </ul>     |
| 2018 [14]        | Single-Phase Full-Bridge               | SWFA                         | Not considered     | <ul style="list-style-type: none"> <li>Harmonic detection</li> </ul>                                  | <ul style="list-style-type: none"> <li>Nonlinear load</li> <li>Load changedIdeal and Distorted Voltage Source</li> </ul>                           |
| 2020 [22]        | Five-level Modified Packed U-Cell      | Reference current generation | Not considered     | <ul style="list-style-type: none"> <li>Harmonic detectionPower factor correction</li> </ul>           | <ul style="list-style-type: none"> <li>Nonlinear load</li> <li>Load changedIdeal Voltage Source</li> </ul>                                         |
| 2020 [16]        | Single-Phase Full-Bridge Inverter      | Improved RCG                 | One sampling time  | <ul style="list-style-type: none"> <li>Harmonic detectionPower factor correction</li> </ul>           | <ul style="list-style-type: none"> <li>Nonlinear load</li> <li>Load changedIdeal Voltage Source</li> </ul>                                         |
| 2021 [12]        | Single-Phase Full-Bridge               | SD                           | Not mentioned      | <ul style="list-style-type: none"> <li>Harmonic detection</li> <li>Power factor correction</li> </ul> | <ul style="list-style-type: none"> <li>Nonlinear load</li> <li>Load change (Electric railway application)</li> <li>Ideal Voltage Source</li> </ul> |
| 2022 [19]        | Single-Phase Two-Level                 | Reference current generation | One sampling time  | <ul style="list-style-type: none"> <li>Harmonic detectionPower factor correction</li> </ul>           | <ul style="list-style-type: none"> <li>Nonlinear load</li> <li>Load changedIdeal Voltage Source</li> </ul>                                         |
| This work        | Single-Phase Full-Bridge               | Enhanced SWFA                | Two sampling times | <ul style="list-style-type: none"> <li>Harmonic detectionPower factor correction</li> </ul>           | <ul style="list-style-type: none"> <li>Nonlinear load</li> <li>Load changedIdeal and Distorted Voltage Source</li> </ul>                           |

![Figure 1: Considered system with the improved harmonic detection approach. The diagram shows a single-phase power system. A Sinusoidal/Distorted Voltage Source (Vs) is connected to a series resistor (R_T) and inductor (L_T) at the Point of Common Coupling (PCC). The PCC voltage is v_PCC and the load current is i_L. A PLL block calculates the voltage angle theta_v from Vs. An APF block calculates the reference current i_C*(n+2) from the voltage angle theta_v and the load current i_L. The Enhanced SWFA block calculates the reference current i_C*(n+2) from the load current i_L and the APF output. A full-wave rectifier converts the reference current into a DC signal. This signal is used to control a load consisting of resistors R_L1 = 40 Ohm and R_L2 = 40 Ohm, and inductors L_L1 = 0.2 H and L_L2 = 0.2 H. Time markers t = 1.0 s and t = 0.7 s are indicated on the load current waveform.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

Figure 1: Considered system with the improved harmonic detection approach. The diagram shows a single-phase power system. A Sinusoidal/Distorted Voltage Source (Vs) is connected to a series resistor (R\_T) and inductor (L\_T) at the Point of Common Coupling (PCC). The PCC voltage is v\_PCC and the load current is i\_L. A PLL block calculates the voltage angle theta\_v from Vs. An APF block calculates the reference current i\_C\*(n+2) from the voltage angle theta\_v and the load current i\_L. The Enhanced SWFA block calculates the reference current i\_C\*(n+2) from the load current i\_L and the APF output. A full-wave rectifier converts the reference current into a DC signal. This signal is used to control a load consisting of resistors R\_L1 = 40 Ohm and R\_L2 = 40 Ohm, and inductors L\_L1 = 0.2 H and L\_L2 = 0.2 H. Time markers t = 1.0 s and t = 0.7 s are indicated on the load current waveform.

Fig. 1. Considered system with the improved harmonic detection approach.

voltage source condition, it affects the PLL performance. As a result, the calculation of the reference source current is incorrect. A LPF in the SD process [12] is used to suppress the harmonic components from the PD. However, the LPF cannot perfectly draw the fundamental component. This point should be concerned. According to the improved RCG method [16], this method comprises the multi-SOGI and the FLL. Here, the use of multiple terms in SOGI can cause a large number of numerical computations and more complexity. This factor also affects the time delay of the harmonic detection. In order to obtain an accurate reference current, the SWFA is therefore chosen in this study. From our previous works [14], the precise fundamental component can be calculated by the SWFA. In addition, the SWFA still provides an accurate reference current even though the distorted voltage source is considered in the system. However, the SWFA cannot extract the instantaneous reactive component to correct the power factor. In this work, the coefficient calculations of SWFA have been enhanced to extract the instantaneous reactive component. The proposed harmonic detection is called the enhanced SWFA.

Based on the existing studies introduced above, a comparative study of the harmonic detection method between the related work and the proposed work is also presented in Table 1. The APF with proposed harmonic detection in a single-phase power system is depicted in Fig. 1. This study has the following main advantages:

- The digital control operation by the HIL technique causes the time delay in the process of harmonic detection of APF. This issue and approaches to addressing harmonic detection delay at two sampling times will be studied in this work. Therefore, in this paper, the major contribution is the SWFA combined with the Lagrange's equation. This approach provides a clear and simple for resolving delays from harmonic detection. The proposed technique is demonstrated to compensate the time delay in a single-phase system. Furthermore, this work allows the developed approach to be applied to other harmonic detection methods. Thus, the harmonic elimination performance of the APF can also be improved.
- The enhanced SWFA can provide better compensation compared to that extracted using conventional SWFA. Both harmonic detecting accuracy and power factor correction can also be achieved.

According to the details in this paper, Section II explains the coefficient calculations and procedure of the harmonic detection based on SWFA. The time delay compensation by the predictive reference current is presented in Section III. For Section IV, the HIL setup of the harmonic elimination in a single-phase system is used to verify the performance of the enhanced SWFA. Conclusions are presented in Section V.

## 2. Harmonic detection method

### 2.1. Sliding window with Fourier analysis (SWFA)

The harmonic detection of APF using the SWFA technique was first introduced in 2001 [22], initially applied to three-phase systems. In 2020, it was adapted for use in single-phase systems [14]. The harmonic extraction by SWFA measures only the load current, unlike other methods that require measuring both current and voltage. Therefore, the SWFA technique is an effective approach to harmonic detection because it has less computational calculations than other methods. The SWFA technique utilizes Fourier series to analyze the  $i_L$  for the harmonic current calculation. Considering the  $i_L$  using the relationship of the Euler-Fourier series equation, it can be shown as (1). This equation consists of the DC and AC components. The AC component is considered for this work. The coefficients of  $A_h$  and  $B_h$  can be calculated from (2) and (3), respectively.

$$i_L(nT_s) = \underbrace{A_0}_{\text{DC component}} + \underbrace{\sum_{h=1}^{\infty} [A_h \cos(h\omega nT_s) + B_h \sin(h\omega nT_s)]}_{\text{AC component}} \quad (1)$$

$$A_h = \frac{2}{N} \sum_{n=N_0}^{N_0+N-1} i_L(nT_s) \underbrace{\cos(h\omega nT_s)}_{F(n\omega T_s)} \quad (2)$$

$$B_h = \frac{2}{N} \sum_{n=N_0}^{N_0+N-1} i_L(nT_s) \underbrace{\sin(h\omega nT_s)}_{F(n\omega T_s)} \quad (3)$$

The AC component is divided into two terms: the  $i_{L1}(nT_s)$  and the  $i_{Lh}(nT_s)$ , as expressed in (4).

$$i_L(nT_s) = i_{L1}(nT_s) + i_{Lh}(nT_s) \quad (4)$$

From (4),  $i_{Lh}(nT_s)$  can be calculated as shown in (5). This term serves as the  $i_C^*$  for the APF. Therefore, the performance of the harmonic extraction using the SWFA technique depends on  $i_{L1}(nT_s)$  calculation, as calculated in (6). The coefficients of  $A_1$  and  $B_1$  of the  $i_{L1}(nT_s)$  are shown in (7) and (8), respectively.

$$i_{Lh}(nT_s) = i_L(nT_s) - i_{L1}(nT_s) = i_C^* \quad (5)$$

$$i_{L1}(nT_s) = A_1 \cos(\omega nT_s) + B_1 \sin(\omega nT_s) \quad (6)$$

$$A_1 = \frac{2}{N} \sum_{n=N_0}^{N_0+N-1} i_L(nT_s) \cos(\omega nT_s) \quad (7)$$

$$B_1 = \frac{2}{N} \sum_{n=N_0}^{N_0+N-1} i_L(nT_s) \sin(\omega nT_s) \quad (8)$$

The procedure of the harmonic detection using the SWFA technique

![Figure 2: Coefficient calculation diagram of SWFA for the harmonic detection process. (a) Conventional SWFA technique: A flowchart starting with 'Start', followed by 'Receive i_L', 'Calculate A_1, B_1', 'Calculate i_L1', and 'Calculate i_C*'. A feedback loop returns 'Return value A_1, B_1 (A_1^old, B_1^old)' to the 'Calculate A_1, B_1' step. (b) Enhanced SWFA technique: Similar to (a), but with an 'Enhanced Part' (dashed blue box) containing 'Calculate A_1, B_1' and 'Calculate C_1'. It also includes 'Calculate i_L1' and 'Calculate i_C*'. A feedback loop returns 'Return value A_1, B_1 (A_1^old, B_1^old)' to the 'Calculate A_1, B_1' step.](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

Figure 2: Coefficient calculation diagram of SWFA for the harmonic detection process. (a) Conventional SWFA technique: A flowchart starting with 'Start', followed by 'Receive i\_L', 'Calculate A\_1, B\_1', 'Calculate i\_L1', and 'Calculate i\_C\*'. A feedback loop returns 'Return value A\_1, B\_1 (A\_1^old, B\_1^old)' to the 'Calculate A\_1, B\_1' step. (b) Enhanced SWFA technique: Similar to (a), but with an 'Enhanced Part' (dashed blue box) containing 'Calculate A\_1, B\_1' and 'Calculate C\_1'. It also includes 'Calculate i\_L1' and 'Calculate i\_C\*'. A feedback loop returns 'Return value A\_1, B\_1 (A\_1^old, B\_1^old)' to the 'Calculate A\_1, B\_1' step.

Fig. 2. Coefficient calculation diagram of SWFA for the harmonic detection process.

![Figure 3: The sliding window technique for the Fourier coefficient calculation. A diagram showing a sliding window of N data points. The window starts at n=N_0 and ends at n=N_0+N-1. The data is labeled 'leaving i_L(nT_s)' at the start and 'entering i_L(nT_s)' at the end. Each data point is processed by a block F(noT_s). The outputs of these blocks are summed (Σ) and then multiplied by 2/N to produce A_1 or B_1.](d62e2e2281009c16f4ee61660e716cd9_img.jpg)

Figure 3: The sliding window technique for the Fourier coefficient calculation. A diagram showing a sliding window of N data points. The window starts at n=N\_0 and ends at n=N\_0+N-1. The data is labeled 'leaving i\_L(nT\_s)' at the start and 'entering i\_L(nT\_s)' at the end. Each data point is processed by a block F(noT\_s). The outputs of these blocks are summed (Σ) and then multiplied by 2/N to produce A\_1 or B\_1.

Fig. 3. The sliding window technique for the Fourier coefficient calculation.

can be summarized in Fig. 2(a), which contains five steps as follows:

Step 1: Receive the  $i_L$  data in one period ( $N$  data set).

Step 2: Calculate the Fourier coefficients of  $A_1$  and  $B_1$  using the sliding window technique. For the next sampling time, this technique leaves the old data on the  $i_L$  (position at  $N_0$ ) for the  $N$  data set ( $N_0 - 1$ ). Then, slide the new data (position at  $N_0 + N$ ) from the sum to the old data, as shown in (9) and (10), respectively. The calculations of  $A_1$  and  $B_1$  in each  $T_s$  of receiving new data result in updating the  $i_{L1}(nT_s)$  in every round of computation. The Computational mechanism of the Fourier coefficient calculation can be summarized as shown in Fig. 3.

$$A_1 = A_1^{\text{old}} + \frac{2}{N} [i_L((N_0 + N)T_s) \cos \omega((N_0 + N)T_s) - i_L((N_0 - 1)T_s) \cos \omega((N_0 - 1)T_s)] \quad (9)$$

$$B_1 = B_1^{\text{old}} + \frac{2}{N} [i_L((N_0 + N)T_s) \sin \omega((N_0 + N)T_s) - i_L((N_0 - 1)T_s) \sin \omega((N_0 - 1)T_s)] \quad (10)$$

Step 3: Calculate the  $i_{L1}$  using (6).

Step 4: Calculate the  $i_C^*$  of APF by subtracting the  $i_{L1}$  in (6) from the  $i_L$ , as shown in (5).

### 2.2. Enhance sliding window with Fourier analysis (Enhanced SWFA)

The enhanced SWFA method is based on the concept of the Fourier series. This method relied on the amplitude-phase ( $C_h - \phi_h$ ) terms, as shown in (11). These terms can be replaced to the Fourier series in (1) by  $C_h$  and  $\phi_h$ , as detailed in (12) and (13), respectively. As a result, the enhanced SWFA method differs from the conventional SWFA method in the calculation of  $i_{L1}$  (step 3), as presented in (14). Additionally, the enhanced SWFA method provides to improve the power factor by aligning the phase angle of the current with the  $\theta_v$  using the PLL technique. The process of harmonic detection using the enhanced SWFA method is summarized in Fig. 2(b).

$$i_L(nT_s) = \underbrace{A_0}_{\text{DC component}} + \underbrace{\sum_{h=1}^{\infty} [C_h \sin(h\omega nT_s + \phi_h)]}_{\text{AC component}} \quad (11)$$

$$C_h = \sqrt{A_h^2 + B_h^2} \quad (12)$$

$$\phi_h = \tan^{-1} \left( \frac{B_h}{A_h} \right) \quad (13)$$

$$i_{L1}(nT_s) = C_1 \sin(\theta_v) \quad (14)$$

![Figure 4: Reference current prediction by the first-order Lagrange method. The diagram shows a reference current waveform i_c^*(n) over time. A horizontal axis marks sampling times n-2, n-1, n, n+1, n+2, and n+3. A vertical dashed line at time n separates the 'Past' (left) from the 'Future' (right). The waveform is shown as a series of connected points. Predictions are made at time n for the future value i_c^*(n+1) and at time n+1 for the future value i_c^*(n+2). These predictions are labeled as 'Lagrange's prediction' and are shown as dashed lines. The prediction at time n is i_cp^*(n+1) and at time n+1 is i_cp^*(n+2). The sampling time T_s is indicated between n and n+1.](7a3561af571faf036baa93f5f4b1bdb9_img.jpg)

Figure 4: Reference current prediction by the first-order Lagrange method. The diagram shows a reference current waveform i\_c^\*(n) over time. A horizontal axis marks sampling times n-2, n-1, n, n+1, n+2, and n+3. A vertical dashed line at time n separates the 'Past' (left) from the 'Future' (right). The waveform is shown as a series of connected points. Predictions are made at time n for the future value i\_c^\*(n+1) and at time n+1 for the future value i\_c^\*(n+2). These predictions are labeled as 'Lagrange's prediction' and are shown as dashed lines. The prediction at time n is i\_cp^\*(n+1) and at time n+1 is i\_cp^\*(n+2). The sampling time T\_s is indicated between n and n+1.

Fig. 4. Reference current prediction by the first-order Lagrange method.

![Figure 5: The overall detection structure on the eZdsp™ F28335 board. The diagram is divided into two main sections: 'First-Order Lagrange's Equation' and 'Enhanced-SWFA'. The 'First-Order Lagrange's Equation' section calculates the predictive reference current i_cp^*(n+2) using a summing junction and three gain blocks (6, 8, 3) that take inputs i_cp^*(n), i_cp^*(n-1), and i_cp^*(n-2) respectively. These inputs are delayed by 'Unit Delay' blocks. The 'Enhanced-SWFA' section calculates the fundamental current i_c^* using a summing junction that subtracts the load current i_L from the reference current i_c^*. This result is then processed by 'Fourier coefficient calculations (A1, B1, C1) (Fundamental Current Extraction)'. A 'PLL' block receives the output and the voltage V_PCC to provide a phase angle theta_v. The entire structure is labeled 'Enhanced-SWFA'.](53f1f7d17b3e7aae62169c41d2a88a77_img.jpg)

Figure 5: The overall detection structure on the eZdsp™ F28335 board. The diagram is divided into two main sections: 'First-Order Lagrange's Equation' and 'Enhanced-SWFA'. The 'First-Order Lagrange's Equation' section calculates the predictive reference current i\_cp^\*(n+2) using a summing junction and three gain blocks (6, 8, 3) that take inputs i\_cp^\*(n), i\_cp^\*(n-1), and i\_cp^\*(n-2) respectively. These inputs are delayed by 'Unit Delay' blocks. The 'Enhanced-SWFA' section calculates the fundamental current i\_c^\* using a summing junction that subtracts the load current i\_L from the reference current i\_c^\*. This result is then processed by 'Fourier coefficient calculations (A1, B1, C1) (Fundamental Current Extraction)'. A 'PLL' block receives the output and the voltage V\_PCC to provide a phase angle theta\_v. The entire structure is labeled 'Enhanced-SWFA'.

Fig. 5. The overall detection structure on the eZdsp™ F28335 board.

## 3. Delay time compensation for harmonic detection

The harmonic detection process in the digital control results in a time delay. It will affect the performance of the harmonic elimination using an APF. From previous studies, delay time compensation can be performed using predictive control approaches. However, these approaches

do not carefully consider the delay time effect of the reference current calculation. Based on the delay time compensation, the reference current calculation using SWFA technique is presented in this section. The use of HIL (eZdsp™ F28335 board with MATLAB/Simulink Software) causes the delay time from the computational burden of the harmonic detection process on the microcontroller board and the transferring data

![Figure 6(a): configuration of the HIL. This block diagram shows a single-phase system. A source voltage v_s is connected to a series resistor R_T and inductor L_T, then to a point labeled PCC. The PCC is connected to a load current i_L through a full-wave rectifier. A reference current i_c^* is fed into an Active Power Filter (APF) block. The APF output is i_c^*. The system is connected to a host computer via a USB JTAG emulator. Data is transferred between the host computer and the eZdsp F28335 board via 'To RTDX' and 'From RTDX' blocks. The eZdsp F28335 board is shown in a docking station, running a 'harmonic detection program' in Code Composer Studio.](b4a7906eddfd40aaa750e19e56c94a8b_img.jpg)

Figure 6(a): configuration of the HIL. This block diagram shows a single-phase system. A source voltage v\_s is connected to a series resistor R\_T and inductor L\_T, then to a point labeled PCC. The PCC is connected to a load current i\_L through a full-wave rectifier. A reference current i\_c^\* is fed into an Active Power Filter (APF) block. The APF output is i\_c^\*. The system is connected to a host computer via a USB JTAG emulator. Data is transferred between the host computer and the eZdsp F28335 board via 'To RTDX' and 'From RTDX' blocks. The eZdsp F28335 board is shown in a docking station, running a 'harmonic detection program' in Code Composer Studio.

(a) configuration of the HIL

![Figure 6(b): experimental of the HIL. This photograph shows a laptop displaying MATLAB/Simulink and Code Composer Studio software. The laptop is connected to an eZdsp F28335 board via a USB JTAG emulator. The board is mounted on a docking station. The software displays waveforms and system models.](e6751f2eb226d6663ce80a2cb1603dec_img.jpg)

Figure 6(b): experimental of the HIL. This photograph shows a laptop displaying MATLAB/Simulink and Code Composer Studio software. The laptop is connected to an eZdsp F28335 board via a USB JTAG emulator. The board is mounted on a docking station. The software displays waveforms and system models.

(b) experimental of the HIL

Fig. 6. HIL model for the harmonic elimination using the APF in the single-phase system.

**Table 2**  
 System Parameters.

| Parameter                    | Value                                                                                  |
|------------------------------|----------------------------------------------------------------------------------------|
| Source voltage and frequency | $v_s = 220 \text{ V}, f_s = 50 \text{ Hz}, \% \text{ THDTHD} = 10\%$                   |
| Transmission line impedance  | $R_T = 0.1\Omega, L_T = 1 \text{ mH}$                                                  |
| Load impedance               | $R_{L1} = 40\Omega, R_{L2} = 40\Omega, L_{L1} = 0.2 \text{ H}, L_{L2} = 0.2 \text{ H}$ |
| Sampling time                | $10 \mu\text{s}$                                                                       |

between the control platform (eZdsp<sup>TM</sup> F28335 board) and the power system (MATLAB Simulink / host computer). It causes a delay time of two sampling times. Therefore,  $i_c(n+2)$  can properly compensate the delay time of two sampling times. Here, an accurate harmonic detection can be achieved by predicting the reference current. The predictions of future reference currents at the sampling times  $n+1$ ,  $n+2$ , and  $n+3$  ( $i_c^*(n+1), i_c^*(n+2), i_c^*(n+3)$ ) are tested in this work. The first-order Lagrange method [23] is applied to predict the reference current because it has been mathematically proven to be reliable and accurate in predicting future values. The reference currents at the time instant  $n$  ( $i_c^*(n)$ ) and the previous reference currents at the sampling times  $n-1, n-2$

( $i_c^*(n-1), i_c^*(n-2)$ ) are considered to predict the  $i_c^*(n+1), i_c^*(n+2)$ , and  $i_c^*(n+3)$ . The first-order Lagrange equations are used to calculate the predictive reference currents at the next sampling periods ( $i_{cp}^*(n+1), i_{cp}^*(n+2), i_{cp}^*(n+3)$ ) as given in (15) to (17), respectively. To achieve a predictive reference current,  $i_{cp}^*(n+1), i_{cp}^*(n+2)$ , and  $i_{cp}^*(n+3)$  must be equal to  $i_c^*(n+1), i_c^*(n+2)$ , and  $i_c^*(n+3)$ , respectively. The concept and structure of reference current prediction is shown in Figs. 4 and 5, respectively.

$$i_{cp}^*(n+1) = 3i_c^*(n) - 3i_c^*(n-1) + i_c^*(n-2) \quad (15)$$

$$i_{cp}^*(n+2) = 6i_c^*(n) - 8i_c^*(n-1) + 3i_c^*(n-2) \quad (16)$$

$$i_{cp}^*(n+3) = 10i_c^*(n) - 15i_c^*(n-1) + 6i_c^*(n-2) \quad (17)$$

![Figure 7: Waveforms of the enhanced SWFA at different prediction horizons. The figure consists of five subplots. The top subplot shows a large graph with four situations: situation 1 (sinusoidal voltage, R_L = 40 Ω, L_L = 0.2 H), situation 2 (sinusoidal voltage, R_L = 20 Ω, L_L = 0.2 H), situation 3 (distorted voltage, R_L = 20 Ω, L_L = 0.2 H), and situation 4 (distorted voltage, R_L = 20 Ω, L_L = 0.1 H). The y-axis is current (A) from -15 to 15, and the x-axis is time (s) from 0 to 1.2. Four reference current waveforms are plotted: i_c^*(n) (black), i_c^*(n+1) (blue), i_c^*(n+2) (red), and i_c^*(n+3) (green). Labels a, b, c, and d point to specific features in each situation. Below this are four smaller subplots (a, b, c, d) showing zoomed-in views of the waveforms starting at 'start APF'. Subplot (a) shows sinusoidal voltage with R_L = 40 Ω, L_L = 0.2 H. Subplot (b) shows distorted voltage with R_L = 40 Ω, L_L = 0.2 H. Subplot (c) shows distorted voltage with R_L = 20 Ω, L_L = 0.2 H. Subplot (d) shows distorted voltage with R_L = 20 Ω, L_L = 0.1 H. The y-axis for these subplots is current (A) from -10 to 10, and the x-axis is time (s) from 0.8998 to 0.9002 for (c) and (d), and from 0.2998 to 0.3002 for (a) and (b).](92c6488dfdf125bc1b7bb6a235394652_img.jpg)

Figure 7: Waveforms of the enhanced SWFA at different prediction horizons. The figure consists of five subplots. The top subplot shows a large graph with four situations: situation 1 (sinusoidal voltage, R\_L = 40 Ω, L\_L = 0.2 H), situation 2 (sinusoidal voltage, R\_L = 20 Ω, L\_L = 0.2 H), situation 3 (distorted voltage, R\_L = 20 Ω, L\_L = 0.2 H), and situation 4 (distorted voltage, R\_L = 20 Ω, L\_L = 0.1 H). The y-axis is current (A) from -15 to 15, and the x-axis is time (s) from 0 to 1.2. Four reference current waveforms are plotted: i\_c^\*(n) (black), i\_c^\*(n+1) (blue), i\_c^\*(n+2) (red), and i\_c^\*(n+3) (green). Labels a, b, c, and d point to specific features in each situation. Below this are four smaller subplots (a, b, c, d) showing zoomed-in views of the waveforms starting at 'start APF'. Subplot (a) shows sinusoidal voltage with R\_L = 40 Ω, L\_L = 0.2 H. Subplot (b) shows distorted voltage with R\_L = 40 Ω, L\_L = 0.2 H. Subplot (c) shows distorted voltage with R\_L = 20 Ω, L\_L = 0.2 H. Subplot (d) shows distorted voltage with R\_L = 20 Ω, L\_L = 0.1 H. The y-axis for these subplots is current (A) from -10 to 10, and the x-axis is time (s) from 0.8998 to 0.9002 for (c) and (d), and from 0.2998 to 0.3002 for (a) and (b).

**Fig. 7.** Waveforms of the enhanced SWFA at different prediction horizons.

![Figure 8: Results of harmonic elimination using the enhanced SWFA at different prediction horizons. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0 to 1.2. A legend at the top indicates four situations: situation 1 (sinusoidal voltage, R_L = 40 Ω, L_L = 0.2 H), situation 2 (sinusoidal voltage, R_L = 20 Ω, L_L = 0.2 H), situation 3 (distorted voltage, R_L = 20 Ω, L_L = 0.2 H), and situation 4 (distorted voltage, R_L = 20 Ω, L_L = 0.1 H). The top subplot shows the source voltage v_s (V) oscillating between -200 and 200. The subsequent five subplots show the load current i_L (A) and source current i_s (A) for each situation, with the source current plots labeled with their respective prediction horizons: (by i_c(n) injection), (by i_c(n+1) injection), (by i_c(n+2) injection), (by i_c(n+3) injection), and (by i_c(n+4) injection). The source current plots show the effectiveness of harmonic elimination, with higher prediction horizons resulting in cleaner sinusoidal waveforms.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 8: Results of harmonic elimination using the enhanced SWFA at different prediction horizons. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0 to 1.2. A legend at the top indicates four situations: situation 1 (sinusoidal voltage, R\_L = 40 Ω, L\_L = 0.2 H), situation 2 (sinusoidal voltage, R\_L = 20 Ω, L\_L = 0.2 H), situation 3 (distorted voltage, R\_L = 20 Ω, L\_L = 0.2 H), and situation 4 (distorted voltage, R\_L = 20 Ω, L\_L = 0.1 H). The top subplot shows the source voltage v\_s (V) oscillating between -200 and 200. The subsequent five subplots show the load current i\_L (A) and source current i\_s (A) for each situation, with the source current plots labeled with their respective prediction horizons: (by i\_c(n) injection), (by i\_c(n+1) injection), (by i\_c(n+2) injection), (by i\_c(n+3) injection), and (by i\_c(n+4) injection). The source current plots show the effectiveness of harmonic elimination, with higher prediction horizons resulting in cleaner sinusoidal waveforms.

Fig. 8. Results of harmonic elimination using the enhanced SWFA at different prediction horizons.

## 4. Results and Discussions

### 4.1. Hardware in the loop (HIL) technique

The hardware-in-the-loop (HIL) simulation technique is used to validate the proposed harmonic detection. For HIL setup, the enhanced SWFA coding with the C programming language and Code Composer Studio on the eZdsp™ F28335 board is connected to the power system with APF using Simscape blocks in the MATLAB/Simulink program. The advantages of this technique indicate that our designed control strategy can be digitally operated on a real experimental platform. Here, the technical hardware problems are not taken into consideration. We can clearly study and analyze the enhanced SWFA as well as the performance results (i.e., the harmonic elimination). Its testing results (i.e., system responses, compensating currents, etc.) can be followed before the real experimental platform setup. This can help to prevent any damage to real electronic devices and power equipment. The configuration and implementation of the HIL technique are illustrated in Fig. 6.

In Fig. 6, it is observed that the MATLAB/Simulink program on a host computer and the eZdsp™ F28335 board are connected via the USB port

using the JTAG emulator (joint test action group) interface. Data exchange between the MATLAB/Simulink program and the eZdsp™ F28335 board uses the RTDX (real-time data exchange) blocks. The  $v_s$  and  $i_L$  measured from the considered single-phase system are transmitted from the MATLAB/Simulink program through the "From RTDX" block to the processing on the eZdsp™ F28335 board via the USB port. The SWFA and enhanced SWFA are implemented using C programming on the eZdsp™ F28335 board. After the reference current calculation in one cycle of eZdsp™ F28335 board operation, the eZdsp™ F28335 board will send the  $i_c^*$  obtained from the processing back to the MATLAB/Simulink program through the "To RTDX" block. The  $i_c^*$  is used as a reference current for the APF. To clearly investigate the performance of harmonic elimination in the system, the ideal current source is used as the APF. This ideal current completely injects the  $i_c$  into the PCC of the considered system (the  $i_c^*$  equals the  $i_c$ ). In addition, the system parameters for the HIL simulation model are addressed in Table 2.

### 4.2. Delay time compensation performance

The HIL results of the enhanced SWFA for the APF at different pre-

![Figure 9(a): Waveforms of voltage (v_s) and currents (i_L, i_s) before compensation in situation 1. The top plot shows a clean sinusoidal voltage waveform v_s (V) from 0.285 to 0.32 seconds. The middle plot shows a square current waveform i_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i_s (A) that follows the shape of i_L but with significant harmonic content. The x-axis is labeled 'time (s)'.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 9(a): Waveforms of voltage (v\_s) and currents (i\_L, i\_s) before compensation in situation 1. The top plot shows a clean sinusoidal voltage waveform v\_s (V) from 0.285 to 0.32 seconds. The middle plot shows a square current waveform i\_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i\_s (A) that follows the shape of i\_L but with significant harmonic content. The x-axis is labeled 'time (s)'.

(a) before compensation in situation 1

![Figure 9(b): Waveforms of voltage (v_s) and currents (i_L, i_s) before compensation in situation 2. The top plot shows a distorted voltage waveform v_s (V) from 0.58 to 0.62 seconds. The middle plot shows a square current waveform i_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i_s (A) that follows the shape of i_L but with significant harmonic content. The x-axis is labeled 'time (s)'.](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 9(b): Waveforms of voltage (v\_s) and currents (i\_L, i\_s) before compensation in situation 2. The top plot shows a distorted voltage waveform v\_s (V) from 0.58 to 0.62 seconds. The middle plot shows a square current waveform i\_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i\_s (A) that follows the shape of i\_L but with significant harmonic content. The x-axis is labeled 'time (s)'.

(b) before compensation in situation 2

![Figure 9(c): Waveforms of voltage (v_s) and currents (i_L, i_s) before compensation in situation 3. The top plot shows a distorted voltage waveform v_s (V) from 0.88 to 0.92 seconds. The middle plot shows a square current waveform i_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i_s (A) that follows the shape of i_L but with significant harmonic content. The x-axis is labeled 'time (s)'.](27b22513fc27a0ff5f230b062ad3112f_img.jpg)

Figure 9(c): Waveforms of voltage (v\_s) and currents (i\_L, i\_s) before compensation in situation 3. The top plot shows a distorted voltage waveform v\_s (V) from 0.88 to 0.92 seconds. The middle plot shows a square current waveform i\_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i\_s (A) that follows the shape of i\_L but with significant harmonic content. The x-axis is labeled 'time (s)'.

(c) before compensation in situation 3

![Figure 9(d): Waveforms of voltage (v_s) and currents (i_L, i_s) before compensation in situation 4. The top plot shows a distorted voltage waveform v_s (V) from 1.18 to 1.22 seconds. The middle plot shows a square current waveform i_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i_s (A) that follows the shape of i_L but with significant harmonic content. The x-axis is labeled 'time (s)'.](643d86ebba41e16a88461bfcb3741de6_img.jpg)

Figure 9(d): Waveforms of voltage (v\_s) and currents (i\_L, i\_s) before compensation in situation 4. The top plot shows a distorted voltage waveform v\_s (V) from 1.18 to 1.22 seconds. The middle plot shows a square current waveform i\_L (A) with a 50% duty cycle. The bottom plot shows a distorted current waveform i\_s (A) that follows the shape of i\_L but with significant harmonic content. The x-axis is labeled 'time (s)'.

(d) before compensation in situation 4

Fig. 9. Waveforms of the voltage ( $v_s$ ) and currents ( $i_L$ ,  $i_s$ ) before compensation in each situation.

prediction horizons ( $n$ ,  $n + 1$ ,  $n + 2$ , and  $n + 3$ ) are depicted in Fig. 7. From the figure, it is observed that the waveforms of reference current at the different prediction horizons ( $i_C^*(n)$ ,  $i_C^*(n + 1)$ ,  $i_C^*(n + 2)$ ,  $i_C^*(n + 3)$ ) appear similar in shape. However, considering the waveforms of reference current at  $t = 0.3$  seconds (sinusoidal voltage and  $R_L = R_{L1} = 40\Omega$ ,  $L_L = L_{L1} = 0.2$  H),  $t = 0.6$  seconds (distorted voltage and  $R_L = R_{L1} = 40\Omega$ ,  $L_L = L_{L1} = 0.2$  H),  $t = 0.9$  seconds (distorted voltage and  $R_L = R_{L1}||R_{L2} = 20\Omega$ ,  $L_L = L_{L1} = 0.2$  H) and  $t = 1.2$  seconds (distorted voltage and  $R_L = R_{L1}||R_{L2} = 20\Omega$ ,  $L_L = L_{L1}||L_{L2} = 0.1$  H), it is found that the waveform of  $i_C^*(n)$  appears to have a signal delay compared to the waveforms of  $i_C^*(n + 1)$ ,  $i_C^*(n + 2)$ , and  $i_C^*(n + 3)$ , respectively. This result confirms that the  $i_C^*(n + 1)$ ,  $i_C^*(n + 2)$ , and  $i_C^*(n + 3)$  are predicted from the  $i_C^*(n)$ , when considering at the prediction horizons ( $n + 1$ ,  $n + 2$ , and  $n + 3$ ), respectively. The  $i_C^*(n)$ ,  $i_C^*(n + 1)$ ,  $i_C^*(n + 2)$ , and  $i_C^*(n + 3)$  are used as the reference currents for testing the performance of the harmonic elimination using APF.

### 4.3. Harmonic elimination performance

The testing of the harmonic elimination performance based on the enhanced SWFA at the different prediction horizons is divided into three situations. In the first situation, from 0 to 0.4 s, the voltage source is a pure sinusoidal waveform and the  $R_L = R_{L1} = 40\Omega$ ,  $L_L = L_{L1} = 0.2$  H. In the second situation, from 0.4 to 0.7 s, the voltage source is distorted, and the  $R_L = R_{L1} = 40\Omega$ ,  $L_L = L_{L1} = 0.2$  H. In the third situation, from

0.7 to 1.0 s, the voltage source is distorted, and the  $R_L$  is changed to  $20\Omega$  ( $R_L = R_{L1}||R_{L2} = 20\Omega$ ,  $L_L = L_{L1} = 0.2$  H). In the fourth situation, from 1.0 to 1.3 s, the voltage source is distorted, and the  $R_L$  is still equal to  $20\Omega$ , the  $L_L$  is changed to 0.1 H ( $R_L = R_{L1}||R_{L2} = 20\Omega$ ,  $L_L = L_{L1}||L_{L2} = 0.1$  H). These results are illustrated in Fig. 8, which can be explained as follows:

- Before compensation, the waveform of  $i_s$  is similar to the waveform of  $i_L$ , as shown in Fig. 9. This resulted in the  $i_s$  distortion. The total harmonic distortion of source currents (%THD) [10] in situations 1, 2, 3, and 4 are equal to 43.14 %, 46.87 %, 47.70 %, and 46.30 % respectively. These values exceed the IEEE 519 standard requirements. Additionally, the power factor values before compensation for all situations were equal to 0.91, 0.89, 0.89, and 0.89, respectively.
- After compensation, the APF injects the compensating currents at the different prediction horizon ( $i_C(n)$ ,  $i_C(n + 1)$ ,  $i_C(n + 2)$ ,  $i_C(n + 3)$ ) into the PCC point at 0.1 s. Additionally, we also employ the SWFA and enhanced SWFA to compare the performance of harmonic elimination. These compensating current injections provide a more sinusoidal waveform of  $i_s$  compared with before compensation. However, the compensating currents at the different prediction horizons affect being a complete sinusoidal waveform of  $i_s$ , as shown in Fig. 10 (situation 1), 11 (situation 2), 12 (situation 3), and 13 (situation 4), respectively.

![Figure 10: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 1. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0.28 to 0.32. The top subplot shows the source voltage v_s (V) as a sinusoidal wave between -200 and 200. The second subplot shows the load current i_L (A) as a square wave between 0 and -10. The subsequent four subplots show the source current i_s (A) for different prediction horizons: 'by i_c(n) injection', 'by i_c(n+1) injection', 'by i_c(n+2) injection', and 'by i_c(n+3) injection'. Each i_s plot shows a sinusoidal wave with red dashed circles highlighting specific harmonic components that are progressively eliminated as the prediction horizon increases from n to n+3.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 10: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 1. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0.28 to 0.32. The top subplot shows the source voltage v\_s (V) as a sinusoidal wave between -200 and 200. The second subplot shows the load current i\_L (A) as a square wave between 0 and -10. The subsequent four subplots show the source current i\_s (A) for different prediction horizons: 'by i\_c(n) injection', 'by i\_c(n+1) injection', 'by i\_c(n+2) injection', and 'by i\_c(n+3) injection'. Each i\_s plot shows a sinusoidal wave with red dashed circles highlighting specific harmonic components that are progressively eliminated as the prediction horizon increases from n to n+3.

Fig. 10. Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 1.

Table 3

Performance Indices of Harmonic Elimination and Power Factor Correction.

| Case                                                                        | Harmonic detection method | Performance index | Prediction horizon of compensating current |              |              |              |
|-----------------------------------------------------------------------------|---------------------------|-------------------|--------------------------------------------|--------------|--------------|--------------|
|                                                                             |                           |                   | $i_c(n)$                                   | $i_c(n + 1)$ | $i_c(n + 2)$ | $i_c(n + 3)$ |
| <b>Situation 1:</b> sinusoidal voltage and $R_L = 40\Omega$ , $L_L = 0.2$ H |                           |                   |                                            |              |              |              |
| Before                                                                      |                           | %THD              | 43.14 %                                    |              |              |              |
|                                                                             |                           | PF                | 0.91                                       |              |              |              |
| After                                                                       | SWFA                      | %THD              | 4.19 %                                     | 2.60 %       | 0.13 %       | 2.59 %       |
|                                                                             |                           | PF                | 0.93                                       | 0.93         | 0.93         | 0.93         |
|                                                                             | Enhanced SWFA             | %THD              | 4.12 %                                     | 2.60 %       | 0.11 %       | 2.60 %       |
|                                                                             |                           | PF                | 1.00                                       | 1.00         | 1.00         | 1.00         |
| <b>Situation 2:</b> distorted voltage and $R_L = 40\Omega$ , $L_L = 0.2$ H  |                           |                   |                                            |              |              |              |
| Before                                                                      |                           | %THD              | 46.87 %                                    |              |              |              |
|                                                                             |                           | PF                | 0.89                                       |              |              |              |
| After                                                                       | SWFA                      | %THD              | 4.84 %                                     | 2.73 %       | 0.13 %       | 2.76 %       |
|                                                                             |                           | PF                | 0.92                                       | 0.92         | 0.92         | 0.92         |
|                                                                             | Enhanced SWFA             | %THD              | 4.41 %                                     | 2.70 %       | 0.11 %       | 2.69 %       |
|                                                                             |                           | PF                | 1.00                                       | 1.00         | 1.00         | 1.00         |
| <b>Situation 3:</b> distorted voltage and $R_L = 20\Omega$ , $L_L = 0.2$ H  |                           |                   |                                            |              |              |              |
| Before                                                                      |                           | %THD              | 47.70 %                                    |              |              |              |
|                                                                             |                           | PF                | 0.89                                       |              |              |              |
| After                                                                       | SWFA                      | %THD              | 5.07 %                                     | 2.76 %       | 0.13 %       | 2.74 %       |
|                                                                             |                           | PF                | 0.92                                       | 0.92         | 0.92         | 0.92         |
|                                                                             | Enhanced SWFA             | %THD              | 4.48 %                                     | 2.76 %       | 0.11 %       | 2.71 %       |
|                                                                             |                           | PF                | 1.00                                       | 1.00         | 1.00         | 1.00         |
| <b>Situation 4:</b> distorted voltage and $R_L = 20\Omega$ , $L_L = 0.1$ H  |                           |                   |                                            |              |              |              |
| Before                                                                      |                           | %THD              | 46.30 %                                    |              |              |              |
|                                                                             |                           | PF                | 0.89                                       |              |              |              |
| After                                                                       | SWFA                      | %THD              | 4.73 %                                     | 2.81 %       | 0.13 %       | 2.63 %       |
|                                                                             |                           | PF                | 0.92                                       | 0.92         | 0.92         | 0.92         |
|                                                                             | Enhanced SWFA             | %THD              | 4.39 %                                     | 2.61 %       | 0.11 %       | 2.59 %       |
|                                                                             |                           | PF                | 1.00                                       | 1.00         | 1.00         | 1.00         |

![Figure 11: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 2. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0.58 to 0.62. The top subplot shows the source voltage v_s (V) as a sinusoidal wave with a peak of 200V. The second subplot shows the load current i_L (A) as a square wave switching between 0 and 10A. The subsequent four subplots show the source current i_s (A) for different prediction horizons: (by i_c(n) injection), (by i_c(n+1) injection), (by i_c(n+2) injection), and (by i_c(n+3) injection). Each i_s plot shows a sinusoidal waveform with three red dashed circles highlighting harmonic components. As the prediction horizon increases, the harmonics become less pronounced, indicating better harmonic elimination.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 11: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 2. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0.58 to 0.62. The top subplot shows the source voltage v\_s (V) as a sinusoidal wave with a peak of 200V. The second subplot shows the load current i\_L (A) as a square wave switching between 0 and 10A. The subsequent four subplots show the source current i\_s (A) for different prediction horizons: (by i\_c(n) injection), (by i\_c(n+1) injection), (by i\_c(n+2) injection), and (by i\_c(n+3) injection). Each i\_s plot shows a sinusoidal waveform with three red dashed circles highlighting harmonic components. As the prediction horizon increases, the harmonics become less pronounced, indicating better harmonic elimination.

Fig. 11. Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 2.

![Figure 12: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 3. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0.88 to 0.92. The top subplot shows the source voltage v_s (V) as a sinusoidal wave with a peak of 200V. The second subplot shows the load current i_L (A) as a square wave switching between 0 and 20A. The subsequent four subplots show the source current i_s (A) for different prediction horizons: (by i_c(n) injection), (by i_c(n+1) injection), (by i_c(n+2) injection), and (by i_c(n+3) injection). Each i_s plot shows a sinusoidal waveform with three red dashed circles highlighting harmonic components. Similar to Figure 11, the harmonics are more prominent in the (by i_c(n) injection) plot and decrease in magnitude as the prediction horizon increases.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 12: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 3. The figure consists of six vertically stacked subplots sharing a common x-axis labeled 'time (s)' ranging from 0.88 to 0.92. The top subplot shows the source voltage v\_s (V) as a sinusoidal wave with a peak of 200V. The second subplot shows the load current i\_L (A) as a square wave switching between 0 and 20A. The subsequent four subplots show the source current i\_s (A) for different prediction horizons: (by i\_c(n) injection), (by i\_c(n+1) injection), (by i\_c(n+2) injection), and (by i\_c(n+3) injection). Each i\_s plot shows a sinusoidal waveform with three red dashed circles highlighting harmonic components. Similar to Figure 11, the harmonics are more prominent in the (by i\_c(n) injection) plot and decrease in magnitude as the prediction horizon increases.

Fig. 12. Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 3.

- After compensation in the case of  $i_c(n)$ , the waveform of  $i_s$  has a transient response because  $i_c^*(n)$  has a time delay of two sampling times. This delay is produced by the computational burden of the reference current calculation process and the data exchange between the eZdsp<sup>TM</sup> F28335 board and the MATLAB/Simulink program. %THD values of the  $i_s$  in all situations are shown in Table 3.

The  $i_c^*(n+1)$  is the  $i_c^*(n)$  prediction at sampling time  $n+1$ . This current can compensate for the one sampling delay time in the harmonic detection process. After compensation, the waveform of  $i_s$  is a more sinusoidal waveform compared with  $i_s$  in the case of  $i_c(n)$  injection. The  $i_c(n+1)$  injection provides a lower %THD value in harmonic elimination, as shown in Table 3. However, the time delay compensation in the one sampling time is not appropriate, the waveform of  $i_s$  has still a 



![Figure 13: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 4. The figure consists of five vertically stacked subplots sharing a common x-axis representing time in seconds (s), ranging from 1.18 to 1.22. The top subplot shows the source voltage v_s (V) as a distorted waveform. The second subplot shows the load current i_L (A) as a square wave with two pulses. The third subplot, labeled '(by i_c(n) injection)', shows the source current i_s (A) with three vertical red dashed lines indicating harmonic components. The fourth subplot, labeled '(by i_c(n+1) injection)', shows i_s (A) with two red dashed lines. The fifth subplot, labeled '(by i_c(n+2) injection)', shows i_s (A) with one red dashed line. The bottom subplot, labeled '(by i_c(n+3) injection)', shows i_s (A) as a clean sinusoidal waveform with no red dashed lines.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 13: Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 4. The figure consists of five vertically stacked subplots sharing a common x-axis representing time in seconds (s), ranging from 1.18 to 1.22. The top subplot shows the source voltage v\_s (V) as a distorted waveform. The second subplot shows the load current i\_L (A) as a square wave with two pulses. The third subplot, labeled '(by i\_c(n) injection)', shows the source current i\_s (A) with three vertical red dashed lines indicating harmonic components. The fourth subplot, labeled '(by i\_c(n+1) injection)', shows i\_s (A) with two red dashed lines. The fifth subplot, labeled '(by i\_c(n+2) injection)', shows i\_s (A) with one red dashed line. The bottom subplot, labeled '(by i\_c(n+3) injection)', shows i\_s (A) as a clean sinusoidal waveform with no red dashed lines.

Fig. 13. Testing results of harmonic elimination using the enhanced SWFA at different prediction horizons in situation 4.

transient response in this case (Fig. 11).

- After compensation in the case of  $i_c(n + 2)$ , this current predicts two sampling delay times in the harmonic detection process. The waveform of  $i_s$  has a pure sinusoidal waveform. The results indicate that the time delay obtained from the computation of the reference current calculation and the data exchange on the eZdsp<sup>TM</sup> F28335 board are perfectly compensated. The waveform of  $i_s$  in this case has a minimum of %THD compared with the other cases at different prediction horizons, as shown in Table 3.
- Considering to  $i_c(n + 3)$ , the APF with  $i_c(n + 3)$  can eliminate the harmonic for two sampling delay times. However, this current has been over predicted at one sampling time. Thus, the waveform of  $i_s$  has a transient sinusoidal waveform. The results of %THD after compensation in this case are shown in Table 3.
- According to situation 3 and 4 in Figs. 12 and 13, the enhanced SWFA technique can also operate in a distorted voltage source and load changing conditions. After compensation, the %THD adheres to the IEEE 519 standard. This means that these conditions do not affect the performance indices of harmonic elimination by the proposed technique.

From the presented results above, based on the enhanced SWFA technique at the sampling time  $n + 2$ , it confirms that the time delay compensation in harmonic detection can improve the efficacy of harmonic elimination, as observed from the waveform of the  $i_s$ . This waveform depicts a pure sinusoidal waveform. The %THD is reduced to the standard and the lowest %THD compared with the other prediction horizon, as addressed in Table 3. Furthermore, the comparison study of harmonic elimination using the SWFA and enhanced SWFA techniques is presented in Table 3. This table shows that the %THD values for both techniques are approximately the same. However, the SWFA technique cannot improve the power factor to 1, whereas the enhanced SWFA technique can achieve a unity power factor. The improvement in the power factor can be demonstrated by examining the phase angle between the unit voltage and the unit current waveforms, as shown in

Fig. 14. Consequently, the results of time delay compensation and power factor correction clearly show that the advantages of the enhanced –SWFA technique are an interesting approach

# 5. Conclusion

In this paper, the SWFA used in conjunction with the proposed controller first-order Lagrange method has been proposed. The objective of this proposed technique is to calculate the accurate reference current and compensate the time delay. The coefficient calculation of SWFA is modified to provide both the harmonic and reactive power compensations. The prediction of future reference current by Lagrange's equation is applied to compensate the time delay in the digital control platform. The proposed technique was verified on an eZdsp<sup>TM</sup> F28335 board. After compensation, the HIL results confirm that the predictive current at the two sampling times provides an accurate reference current compared with the other prediction horizons. The proposed technique keeps the minimum %THD of the source current compared with the conventional technique. Even though the distorted voltage source and the load-changing conditions are considered in the system. In addition, the unity power factor is achieved by the enhanced SWFA approach.

In future work, the proposed technique should be tested on a real experimental platform with a realistic time delay. Also, to further study in practice, the process of data acquisition consisting of the current and voltage transducers and signal conditioning circuits can also cause additional delay time. Therefore, the proposed technique should be redesigned to compensate the time delay in any condition.

# CRediT authorship contribution statement

**Chakrit Panpean:** Writing – review & editing, Writing – original draft, Visualization, Validation, Methodology, Funding acquisition, Data curation, Conceptualization. **Phonsit Santiprapan:** Writing – review & editing, Writing – original draft, Validation, Methodology, Data curation, Conceptualization. **Jeerawan Homjan:** Writing – review & editing, Writing – original draft, Visualization, Validation, Methodology,

![Figure 14: Comparison waveforms of power factor correction using SWFA and enhanced SWFA techniques. The figure consists of five subplots: (a) before compensation, (b) after compensation in situation 1, (c) after compensation in situation 2, (d) after compensation in situation 3, and (e) after compensation in situation 4. Each subplot shows the source voltage v_s (black solid line), the current i_s at i_c*(n+2) from SWFA (blue solid line), and the current i_s at i_c*(n+2) from Enhanced-SWFA (red dashed line). The y-axis for all plots ranges from -1 to 1. The x-axis represents time in seconds. In subplot (a), the current waveform is distorted with high-frequency harmonics. In subplots (b) through (e), the current waveform is significantly improved, closely following the sinusoidal voltage waveform, demonstrating the effectiveness of the enhanced SWFA technique.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 14: Comparison waveforms of power factor correction using SWFA and enhanced SWFA techniques. The figure consists of five subplots: (a) before compensation, (b) after compensation in situation 1, (c) after compensation in situation 2, (d) after compensation in situation 3, and (e) after compensation in situation 4. Each subplot shows the source voltage v\_s (black solid line), the current i\_s at i\_c\*(n+2) from SWFA (blue solid line), and the current i\_s at i\_c\*(n+2) from Enhanced-SWFA (red dashed line). The y-axis for all plots ranges from -1 to 1. The x-axis represents time in seconds. In subplot (a), the current waveform is distorted with high-frequency harmonics. In subplots (b) through (e), the current waveform is significantly improved, closely following the sinusoidal voltage waveform, demonstrating the effectiveness of the enhanced SWFA technique.

Fig. 14. Comparison waveforms of power factor correction using SWFA and enhanced SWFA techniques.

Investigation, Data curation. **Kongpol Areerak:** Writing – review & editing, Validation, Supervision, Investigation, Conceptualization.

# Funding

This work was supported by the National Research Council of Thailand (NRCT) (contract number N42A660919).

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgments

This project is funded by the National Research Council of Thailand (NRCT) (contract number N42A660919) and was supported by King Mongkut's University of Technology North Bangkok. A preliminary version of this work has been published in ECTI-CON 2024 [24].

# Appendix A. Supplementary data

Supplementary data to this article can be found online at <https://doi.org/10.1016/j.aeue.2024.155647>.

# Data availability

Data will be made available on request.

# References

- [1] Srita S, Somkun S. Implementation and performance comparison of harmonic mitigation schemes for three-phase grid-connected voltage-source converter under grid voltage distortion: Hil and experimental validation. *AEU - Int J Electron Commun* 2023;161:154552. <https://doi.org/10.1016/j.aeue.2023.154552>.
- [2] Zhang G, Jin N, Yu SS, Zhang Y. An X-shaped-switching-network high-step-up converter for grid integration of renewable energy sources. *AEU - Int J Electron Commun* 2021;136:153776. <https://doi.org/10.1016/j.aeue.2021.153776>.
- [3] Sen D, Saha TK, Dey J. Development, implementation and performance analysis of decoupler based control of dual source DC-DC converter. *AEU - Int J Electron Commun* 2020;117:153136. <https://doi.org/10.1016/j.aeue.2020.153136>.
- [4] Gayen PK. An enhanced high-boost active-switched quasi Z-source inverter having shorter range of shoot-through duty ratio for solar energy conversion applications. *AEU - Int J Electron Commun* 2021;137:153822. <https://doi.org/10.1016/j.aeue.2021.153822>.
- [5] Kulkarni SV, Gaonkar DN. Improved droop control strategy for parallel connected power electronic converter based distributed generation sources in an Islanded Microgrid. *Electr Pow Syst Res* 2021;201:107531. <https://doi.org/10.1016/j.epsr.2021.107531>.
- [6] Ding G, Wei R, Zhou K, Gao F, Y. tang.. Communication-less harmonic compensation in a multi-bus microgrid through autonomous control of distributed generation grid-interfacing converters. *J Modern Power Syst Clean Energy* 2015;3 (4):597–609. <https://doi.org/10.1007/s40565-015-0158-3>.
- [7] Rivera S, Kouro S, Vazquez S, Goetz SM, Lizana R, Romero-Cadaval E. Electric vehicle charging infrastructure: From grid to battery. *IEEE Ind Electron Mag* June 2021;15(2):37–51. <https://doi.org/10.1109/MIE.2020.3039039>.
- [8] Ghorbani MJ, Mokhtari H. Impact of harmonics on power quality and losses in power distribution systems. *Int J Electr Comput Eng (IJECE)* 2015;5(1):166–74. <http://doi.org/10.11591/ijece.v5i1.pp166-174>.

- [9] Afonso JL, Tanta M, Pinto JGO, Monteiro LFC, Machado L, Sousa TJC, et al. A review on power electronics technologies for power quality improvement. *Emergies* 2021;14:8585. <https://doi.org/10.3390/en14248585>.
- [10] IEEE Standard for Harmonic Control in Electric Power Systems. IEEE Std 519-2022 (Revision of IEEE Std 519-2014), pp. 1-31, 2022.
- [11] European Norm. Voltage Characteristics of Electricity Supplied by Public Distribution Systems-EN 50160. European Committee for Electrotechnical Standardization (CENELEC): Brussel, Belgium, 2010 July; Available online.
- [12] Panpean C, Areerak K-L, Santiprapan P, Areerak K-N, Yeoh SS. Harmonic mitigation in electric railway systems using improved model predictive control. *Energies* 2021;14(7):2012. <https://doi.org/10.3390/en14072012>.
- [13] P. Santiprapan, K.-L. Areerak and K.-N. Areerak. An Adaptive Gain of Proportional-Resonant Controller for an Active Power Filter. *IEEE Transactions on Power Electronics*. vol. 39, no. 1, pp. 1433-1446, 2024. <https://doi.org/10.1109/TPEL.2023.3319476>.
- [14] M. Padungsin, T. Narongrit and K.-L. Areerak. The Comparison Study of Harmonic Detection Algorithms for Single-Phase Power Systems. 2018 5th International Conference on Electric Power and Energy Conversion Systems (EPECS), Kitakyushu, Japan, 2018, pp. 1-6, <https://doi.org/10.1109/EPECS.2018.8443548>.
- [15] Sarawut J, Areerak K-L, Areerak K-N. Harmonic detection for shunt active power filter using ADALINE neural network. *Energies* 2021;14(14):4351. <https://doi.org/10.3390/en14144351>.
- [16] M. -S. Karbasforooshan and M. Monfared. An Improved Reference Current Generation and Digital Deadbeat Controller for Single-Phase Shunt Active Power Filters. *IEEE Transactions on Power Delivery*. vol. 35, no. 6, pp. 2663-2671, Dec. 2020. <https://doi.org/10.1109/TPWRD.2020.2974155>.
- [17] P. Acuña, L. Morán, M. Rivera, R. Aguilera, R. Burgos and V. G. Agelidis. A Single-Objective Predictive Control Method for a Multivariable Single-Phase Three-Level NPC Converter-Based Active Power Filter. *IEEE Transactions on Industrial Electronics*, vol. 62, no. 7, pp. 4598-4607, July 2015. <https://doi.org/10.1109/TIE.2015.2393556>.
- [18] Sahli A, Krim F, Laib A, Talbi B. Model predictive control for single phase active power filter using modified packed U-cell (MPUC5) converter. *Electr Pow Syst Res* 2020;180:106139. <https://doi.org/10.1016/j.epsr.2019.106139>.
- [19] Morales-Caporal R. Optimal indirect model predictive control for single-phase two-level shunt active power filters. *J Power Electron* 2022;22:84-93. <https://doi.org/10.1007/s43236-021-00343-4>.
- [20] Hoon Y, Radzi MAM, Mohd Zainuri MAA, Zawawi MAM. Shunt active power filter: a review on phase synchronization control techniques. *Electronics* 2019;8(7):791. <https://doi.org/10.3390/electronics8070791>.
- [21] M. El-Habrout and M.K. Darwish. Design and implementation of a modified Fourier analysis harmonic current computation technique for power active filters using DSPs. *Electric Power Applications, IEE Proc.-Electr. Power Appl*, vol. 148, No. 1, January 2001. <https://doi.org/10.1049/ip-epa:20010014>.
- [22] Odavic M, Biagini V, Zanchetta P, Sumner M, Degano M. One-sample-period-ahead predictive current control for high-performance active shunt power filters. *IET Power Electron* 2011;4(4):414-23. <https://doi.org/10.1049/iet-pel.2010.0137>.
- [23] Panpean C, Santiprapan P, Homjan J. In: Improved Harmonic Detection Delay for Active Power Filter. Thailand: Telecommunications and Information Technology (ECTI-CON), Khon Kaen; 2024. p. 1-5. <https://doi.org/10.1109/ECTI-CON60892.2024.10595041>.