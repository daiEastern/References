

###### ORIGINAL RESEARCH **OPEN ACCESS**

# A Combined Compensation Strategy for Steady-State Performance Improvement of Proportional-Proportional-Delay Controller

Di Wu | Yan Fu ![ORCID icon](e3f8612927870f2e0f9f5989e6dd3064_img.jpg) | Mingming Li | Luoming OuYang

School of Electronic Engineering, Jiangsu Ocean University, Lianyungang, Jiangsu, China

**Correspondence:** Mingming Li ([limm@jou.edu.cn](mailto:limm@jou.edu.cn))

**Received:** 7 November 2024 | **Revised:** 7 February 2025 | **Accepted:** 1 March 2025

**Funding:** Supported by Jiangsu Provincial Department of Education General Project (1020241450).

## ABSTRACT

Within control system architectures, the proportional-proportional-delay (PPD) controller is theoretically characterized by enhanced dynamic responsiveness, a streamlined control structure, and reduced computational demands. Nevertheless, this control strategy demonstrates heightened dependence on system model accuracy coupled with compromised robustness, thus imposing significant constraints on its practical deployment in industrial control scenarios. To improve steady-state control performance of the PPD controller against circuit parameters variations, this paper investigates quantity relationships between circuit parameters variations and grid current amplitude changes first, and a dominant factor and some minor factors affecting the grid current are found out successfully. As a result, linear control of the PPD controller against model parameters changes has been proposed based on a linear function. Meanwhile, an integral controller composed has been integrated into the control strategy to eliminate the residual steady-state error of the proposed linear controller. Finally, a combined control structure with both linear and integral controllers has been proposed, and experimental results have been presented to verify the correctness and effectiveness of the combined control.

## 1 | Introduction

Along with renewable energy sources expanding around the globe at record rates, grid-connected inverters play much important roles as interface units between distributed generation and the power grid. The control performance of grid-connected inverters not only determines the quality of grid-in current and operational safety [1–3], but also has an important impact on grid operation, such as broadband resonances, active power-frequency, and reactive power-voltage issues [4–6], et al. From the perspective of control, critical requirements for grid-in current controllers include fast dynamic performance, high tracking accuracy and strong robustness [7–8].

It is difficult for existing current controllers to satisfy the aforementioned requirements simultaneously. For instance, the classic proportional-integral (PI) controller in the stationary frame has better robustness but poor dynamic and steady-state characteristics; on the contrary, the PI controller in the rotating frame and proportional-resonant (PR) controller can improve tracking accuracy, but decrease robustness [9–10]; the repetitive control has high tracking accuracy but poor dynamic performance [11].

Hysteresis control is a nonlinear control method that has advantages in dynamic response, tracking accuracy, and robustness, but an uncertain switching frequency resulting in difficulty in filter design, which in turn limits its application in grid-connected inverters [12]. Some researchers attempted to limit the switching

This is an open access article under the terms of the [Creative Commons Attribution](https://creativecommons.org/licenses/by/4.0/) License, which permits use, distribution and reproduction in any medium, provided the original work is properly cited.

© 2025 The Author(s). IET Power Electronics published by John Wiley & Sons Ltd on behalf of The Institution of Engineering and Technology.

![Figure 1: Typical components of a single phase grid-connected inverter. The diagram shows a DC source with voltage U_dc and capacitor C_dc connected to a bridge inverter circuit. The bridge consists of four switches (S1, S2, S3, S4) and four diodes (D1, D2, D3, D4). The output is connected to a grid through an inductor L and a resistor R. Three factors are highlighted: Factor 1 (switches and diodes), Factor 2 (inductor L), and Factor 3 (resistor R).](68ac34ff111db52afaa786afcb8346c3_img.jpg)

Figure 1: Typical components of a single phase grid-connected inverter. The diagram shows a DC source with voltage U\_dc and capacitor C\_dc connected to a bridge inverter circuit. The bridge consists of four switches (S1, S2, S3, S4) and four diodes (D1, D2, D3, D4). The output is connected to a grid through an inductor L and a resistor R. Three factors are highlighted: Factor 1 (switches and diodes), Factor 2 (inductor L), and Factor 3 (resistor R).

**FIGURE 1** | Typical components of a single phase grid-connected inverter.

frequency range by setting the hysteresis width, but precise component parameters are required in proposed methods [13].

The dynamic response of model predictive control (MPC) controllers is fast, but there are some disadvantages, such as a heavy computational burden, high dependence on system models, poor robustness, and uncertain switching frequency [14–16]. A PPD controller combining advantages of MPC and pulse width modulation (PWM) had been proposed to solve the problems of calculation burden and uncertain switching frequency in [17]. However, it still has the disadvantage of poor robustness, because variations of  $L$ - $R$  model parameters will deteriorate steady-state control performances.

In order to improve the static robustness of the PPD controller against component parameter changes, a combined control structure composed of linear and integral controllers has been proposed in this paper. Section 2 analyses the influence of inverter parameter variations on control performance. In Section 3, compensation strategies against parameter changes are presented for the PPD controller proposed in [17]. Section 4 presents the proposed combined control structure with linear and integral controllers. The stability of the system is analysed in Section 5. In order to verify the correctness of the proposed compensation strategy, comprehensive simulation and experimental results from different operational conditions are presented in Section 6, and Section 7, respectively. Finally, a conclusion is drawn in Section 8.

## 2 | Tracking Performance Analysis With Components Parameter Changes

The PPD controller proposed in [17] is essentially an MPC controller based on an  $L$ - $R$  model, which means that the values of inductance and resistance must be known and constant. However, component parameter deviations are unavoidable in real inverters due to the existence of practical factors, such as environmental temperature variation, component replacement, etc.

A typical single-phase grid-connected inverter is illustrated in Figure 1. There are some factors that affect inverter operation parameters, for instance, power devices affect the values of conduction voltage drop  $U_{CE}$  of switches and forward voltage  $U_F$  of diodes, named as Factor 1; operation temperatures and current

![Figure 2: Control block diagram of grid-connected inverters with a PPD controller. The diagram shows a reference current i_ref entering a PPD controller block. The controller output is compared with the grid voltage u_g and the grid current i_g. The PPD controller block contains proportional gains K1 and K2, a delay e^-sT, and a summation node. The output of the PPD controller is used to generate a PWM signal, which is then filtered by a low-pass filter (G_dw) and a gain G_d1 to produce the grid voltage u_g. The grid voltage u_g is then used to generate the grid current i_g through a gain G_z and a PWM block K_pwm. The grid current i_g is measured and fed back to the PPD controller.](0a12cc47f3c5ca76c39d5943ba8661bd_img.jpg)

Figure 2: Control block diagram of grid-connected inverters with a PPD controller. The diagram shows a reference current i\_ref entering a PPD controller block. The controller output is compared with the grid voltage u\_g and the grid current i\_g. The PPD controller block contains proportional gains K1 and K2, a delay e^-sT, and a summation node. The output of the PPD controller is used to generate a PWM signal, which is then filtered by a low-pass filter (G\_dw) and a gain G\_d1 to produce the grid voltage u\_g. The grid voltage u\_g is then used to generate the grid current i\_g through a gain G\_z and a PWM block K\_pwm. The grid current i\_g is measured and fed back to the PPD controller.

**FIGURE 2** | Control block diagram of grid-connected inverters with a PPD controller.

operation points decide variations in inductance  $L$ , as shown by Factor 2; and parasitic resistances of power lines, filter inductors and power devices change equivalent resistance  $R$ , represented by Factor 3.

The PPD controller is characterized as an open-loop model-based controller, as shown in Figure 2, which demonstrates superior dynamic response characteristics compared to alternative model-based approaches, while exhibiting heightened susceptibility to non-ideal operating conditions. As a result, the steady-state control performance of the PPD controller will deteriorate in practice because the control parameters of the PPD controller are unchangeable in [17]. The effects of component parameter variations on inverter control performance are analysed as follows.

The expression of PPD controller is shown as below.

$$\begin{cases} K_1 = \frac{L}{\Delta T} + R \\ K_2 = \frac{L}{\Delta T} \end{cases} \quad (1)$$

where  $K_1$  and  $K_2$  are the two proportional coefficients of PPD controller, respectively, and  $\Delta T$  is the delay time.

### 2.1 | Device Conduction Voltage Drop (Factor 1)

The forward characteristic of power devices can be described by a fixed voltage drop  $U_{CE}$  or  $U_F$  and an on-state resistance  $r$ . The voltage drop changes output voltage amplitude of the inverter bridge. A constant value was used to compensate for the conduction voltage drop in [18], but the reality is that the voltage drop changes with variations in temperature and current ratings [19]. In order to improve the compensation accuracy, the expressions for device conduction voltage drops are listed in (2) and (3).

$$u_{CE} = [R_{CE,25^\circ C} + K_{r-Tr}(T_{J-Tr} - 25)]i + U_{CE,25^\circ C} + K_{v-Tr}(T_{J-Tr} - 25) \quad (2)$$

$$u_F = [R_{F,25^\circ C} + K_{r-D}(T_{J-D} - 25)]i + U_{F,25^\circ C} + K_{v-D}(T_{J-D} - 25) \quad (3)$$

where  $u_{CE}$  and  $u_F$  are the conduction voltage drop of power switches, and the forward voltage drops of diodes, respectively;  $R_{CE,25^\circ C}$  and  $R_{F,25^\circ C}$  are the on-state resistances of power switches and diodes at  $25^\circ C$ , respectively.  $U_{CE,25^\circ C}$  and  $U_{F,25^\circ C}$  are the conduction voltage drops of power switches and diodes at  $25^\circ C$ , respectively. These four coefficients are constant. In addition,  $i$  is the instantaneous output current of the inverter.  $T_{J-Tr}$  and

![Figure 3: A line graph showing the relationship between device conduction voltage drops (V) and operating temperature (°C). The x-axis represents Temperature from 25 to 175 °C. The y-axis represents Device Voltage Drop from 1.4 to 2.4 V. Two curves are plotted: IGBT (blue line) and Diode (pink line). The IGBT curve starts at approximately 1.9 V at 25 °C and increases to 2.1 V at 175 °C. The Diode curve starts at approximately 2.1 V at 25 °C and decreases to 1.7 V at 175 °C.](d9d706121d1c4ba9ad2c793746382361_img.jpg)

Figure 3: A line graph showing the relationship between device conduction voltage drops (V) and operating temperature (°C). The x-axis represents Temperature from 25 to 175 °C. The y-axis represents Device Voltage Drop from 1.4 to 2.4 V. Two curves are plotted: IGBT (blue line) and Diode (pink line). The IGBT curve starts at approximately 1.9 V at 25 °C and increases to 2.1 V at 175 °C. The Diode curve starts at approximately 2.1 V at 25 °C and decreases to 1.7 V at 175 °C.

**FIGURE 3** | Relationship curves between device conduction voltage drops and operating temperature.

**TABLE 1** | Tracking errors of the PPD controller with different device voltage drops.

| $U_{CE}$ and $U_F$ changes (%) | +50  | +30  | +10  | -10   | -30   | -50   |
|--------------------------------|------|------|------|-------|-------|-------|
| Current errors (A)             | 0.94 | 0.57 | 0.15 | -0.18 | -0.59 | -0.92 |

$T_{J,D}$  are the actual junction temperatures of power switches and diodes, respectively.  $K_{r-Tr}$  and  $K_{r-D}$  are temperature coefficients of power switches and diodes, respectively, which represent the influence of temperature on the on-state resistance.  $K_{v-Tr}$  and  $K_{v-D}$  are temperature coefficients of power switches and diodes that influence conduction voltage drops, respectively. Based on the data in [19], the curves of conduction voltage drops in power devices varying with temperature are depicted in Figure 3. It is worth noting that the power switches and diodes have opposite trends.

In addition, the replacement caused by the damages of power devices will also lead to different drops in power devices, because the parameters with the same model number cannot be exactly consistent in different batches limited by material characteristics and production processes [22].

The simulation data of reference current tracking errors with variations of conduction voltage drops are represented in Table 1. Here, the model number of the IGBT used is FGA40N65SMD from Fairchild Semiconductor, and the power rating of the grid-connected inverter is 3 kW.

### 2.2 | Filter Inductance (Factor 2)

Filter inductors of grid-connected inverters produced with a magnetic powder core are efficient, small, and cheap. However, there is a disadvantage that changes in the current working point and operating temperature will lead to obvious variations in the inductance of magnetic powder core inductors [20]. In addition, due to the limitation of fabrication techniques and cost, the tolerance of filter inductances may be higher than 20% [21]. Therefore, the filter inductance of inverters has a wide variation range in practical use, which will obviously affect the control effectiveness of the PPD controller.

Table 2 presents the simulation data of a 3 kW grid-connected

**TABLE 2** | Tracking errors of the PPD controller with different filter inductances.

| $L$ changes (%)    | +50  | +30  | +10  | -10   | -30   | -50   |
|--------------------|------|------|------|-------|-------|-------|
| Current errors (A) | 4.10 | 2.60 | 1.02 | -1.06 | -4.00 | -7.00 |

**TABLE 3** | Tracking errors of the PPD controller with different parasitic resistances.

| $R$ change (%)    | +50  | +30  | +10  | -10   | -30   | -50   |
|-------------------|------|------|------|-------|-------|-------|
| Current error (A) | 0.99 | 0.61 | 0.12 | -0.11 | -0.63 | -1.10 |

inverter when inductance  $L$  deviates. It can be seen that the inductance has a much heavier impact on the current tracking accuracy of the PPD controller compared with the deviations in the conduction voltage drops in Table 1.

### 2.3 | Parasitic Resistance (Factor 3)

Power line resistance, internal resistances of power devices, and parasitic resistances of filter inductors are also affected by the changes in ambient temperature and working temperature, which can be equivalent to the change in resistance  $R$  in Figure 1. Obviously, the  $L$ - $R$  model's parameters of the PPD controller will also change.

Table 3 presents the simulation data of a 3 kW grid-connected inverter when resistance  $R$  deviates. It can be seen that the effect of parasitic resistance variation on the current tracking accuracy of the PPD controller is close to that of voltage drop variations in Table 1 approximately.

## 3 | Compensation Strategies Against Component Parameter Changes

### 3.1 | Equivalent Replacement of Parameter Changes

Based on the data from Table 1 to Table 3, the mathematical relationships between the variations of these three parameters and the current errors can be fitted. The fitting curve of the relationship between the variation of device conduction voltage drop and current errors is

$$\Delta I = 0.0191\Delta U_{CE-F} - 0.0715 \quad (4)$$

The fitting curve of the relationship between the variation of parasitic resistance and current errors is:

$$\Delta I = 0.0186R + 0.0097 \quad (5)$$

![Figure 4: Tracking error curves of the PPD controller under different parameters changes. The graph plots 'Current error/A' on the y-axis (from -10 to 5) against 'Parameters variation /%' on the x-axis (from -60 to 60). Three curves are shown: 'Parasitic resistance' (purple line), 'Device conduction voltage drop' (blue line), and 'Filter inductance' (red line). The red line shows a steep positive slope, while the purple and blue lines are nearly horizontal near zero.](5d92d5c9cc01a262b0389d138caa9aea_img.jpg)

Figure 4: Tracking error curves of the PPD controller under different parameters changes. The graph plots 'Current error/A' on the y-axis (from -10 to 5) against 'Parameters variation /%' on the x-axis (from -60 to 60). Three curves are shown: 'Parasitic resistance' (purple line), 'Device conduction voltage drop' (blue line), and 'Filter inductance' (red line). The red line shows a steep positive slope, while the purple and blue lines are nearly horizontal near zero.

**FIGURE 4** | Figure 4 Tracking error curves of the PPD controller under different parameters changes.

The fitting curve of the relationship between the variation of filter inductance and current errors is:

$$\Delta I = -0.0006\Delta L^2 + 0.1083\Delta L - 0.0494 \quad (6)$$

It is imperative to acknowledge that the relationships depicted in (4), (5), and (6) are exclusively applicable to the 3 kW platform constructed in this study. These relationships may not be universally applicable to platforms of varying power levels. However, it should be noted that the trends observed in these equations are generic and may not be restricted to the specific platform under consideration. Draw the three relationship curves above in one figure, as shown in Figure 4. Two conclusions can be drawn from Figure 4:(i) with the same parameter variations, current errors caused by filter inductance are much higher than device conduction voltage drop and parasitic resistance, i.e., the parameter variations of device conduction voltage drop and parasitic resistance are ignorable compared with the parameter variation of filter inductance in terms of effect on current errors; and (ii) with the same variations, the current error caused by the device conduction voltage drop is very close to the current error caused by the parasitic resistance.

According to the parameter table given below, (7) can be obtained

$$\frac{L}{\Delta T} \gg R \quad (7)$$

Therefore, for the PPD controller, the influences of filter inductance on the parameters of the PPD controller are much greater than those of parasitic resistance. It can be seen from Figure 4 that the influences of parasitic resistance and device conduction voltage drop on current are very close. Therefore, for the PPD controller parameters, the influences of filter inductance are much greater than those of the other two parameters.

Based on the above analysis, the current errors caused by conduction voltage drops and parasitic resistances variations can be equivalent to the variations in filter inductance.

### 3.2 | Relationship Between Inductance Changes and Grid-in Current Amplitude Changes

According to the operation principle of the PPD controller [17], the control variable  $u_{LR}$  applied to the  $L$ - $R$  model generates the target current  $i_L$ . Here, the reference current  $i_{ref}$  is expressed in (8),

$$i_{ref}(t) = A \sin(\omega t) \quad (8)$$

where  $A$  is the amplitude of the reference current, and  $\omega$  is the angular frequency. The theoretical control variable  $u_{LR}$  is expressed in (9) after  $i_{ref}$  passes through the PPD controller.

$$\begin{aligned} u_{LR}(t) &= L \frac{di_{ref}(t)}{dt} + Ri_{ref}(t) \\ &= \omega LA \cos \omega t + RA \sin \omega t \end{aligned} \quad (9)$$

Assuming that the filter inductance is changed to  $L_1$ , and the parasitic resistance is changed to  $R_1$ , the PPD controller still outputs  $u_{LR}$  if the current reference  $i_{ref}$  and parameters  $K_1/K_2$  are unchanged. As a result, the response current will be changed to  $i_{L1}(t) = A_1 \sin(\omega t)$ . The new equation can be obtained.

$$\begin{aligned} u_{LR}(t) &= L_1 \frac{di_{L1}(t)}{dt} + R_1 i_{L1}(t) \\ &= \omega L_1 A_1 \cos \omega t + R_1 A_1 \sin \omega t \end{aligned} \quad (10)$$

By combining (9) and (10), the result is given in (11).

$$\omega LA \cos \omega t = \omega L_1 A_1 \cos \omega t + (R_1 A_1 - RA) \sin \omega t \quad (11)$$

Considering  $\omega L \gg R$ ,  $\omega L_1 \gg R_1$ , the values of  $R_1 A_1$  and  $RA$  are quite small, and the item  $(R_1 A_1 - RA)$  is approximate to zero, expression (12) can be obtained.

$$R_1 A_1 - RA \ll \omega L_1 A_1 \quad (12)$$

Therefore, expression (11) can be further simplified to (13).

$$\omega LA \cos \omega t = \omega L_1 A_1 \cos \omega t \quad (13)$$

The relationship among the actual current amplitude  $A_1$  after the model parameters are changed, the reference current amplitude  $A$ , the theoretical inductance  $L$  and the actual inductance  $L_1$  is expressed in (14).

$$L = \frac{A_1}{A} L_1 \quad (14)$$

After subtracting item  $L_1$  from both sides of (14) simultaneously, formula (15) is obtained.

$$L - L_1 = -\frac{L_1}{A}(A - A_1) \quad (15)$$

It can be seen that the change value of current amplitude is related not only to the inductance variation, but also to the current operating point.

In order to obtain a generic relationship between inductance variations and current changes without operating point restrictions, the variable  $y$  is used to represent the percentage of relative variation in inductance, while  $x$  is used to represent the percentage of relative current variation, as listed in (16) and (17), respectively.

$$y = \frac{L - L_1}{L} * 100 \quad (16)$$

$$x = \frac{A - A_1}{A} * 100 \quad (17)$$

![Figure 5: A graph showing the relationship between the change of inductance (%) on the y-axis and the change of current amplitude (%) on the x-axis. A solid red line represents the theoretical curve. Three sets of data points are plotted: blue triangles for i_ref = 14A, red squares for i_ref = 10A, and purple circles for i_ref = 5A. The data points closely follow the theoretical curve, which is labeled (18).](de6e8b740c69dac308cce9edfec3eff4_img.jpg)

Figure 5: A graph showing the relationship between the change of inductance (%) on the y-axis and the change of current amplitude (%) on the x-axis. A solid red line represents the theoretical curve. Three sets of data points are plotted: blue triangles for i\_ref = 14A, red squares for i\_ref = 10A, and purple circles for i\_ref = 5A. The data points closely follow the theoretical curve, which is labeled (18).

**FIGURE 5** | Relationship curves between inductance change and current amplitude change.

(18) is derived after substituting (16) and (17) into (14).

$$y = \frac{100x}{x - 100} \quad (18)$$

In a similar vein, (18) is applicable exclusively to the experimental platform under consideration in this paper. However, the trends it exhibits are equally applicable to inverters of other power classes. The solid line in Figure 5 is obtained from (18), which is the theoretical curve of the relative variations of inductance and current amplitude. The blue, red, and purple data points are from simulation data with different reference current values set as 14A, 10A, and 5A, respectively. It can be seen that these data points are in accordance with the theoretical curve very well. Therefore, two important conclusions can be drawn here: (1) the theoretical relationship indicated by (18) is correct; and (2) the restriction of current operating points is removed in formula (18).

### 3.3 | Relationship Between $K_1/K_2$ Changes and Grid-in Current Amplitude's Changes

The relationship between inductance variations and current amplitude changes is established in section 3.2, and the relationship between PPD controller parameters  $K_1/K_2$  and current amplitude changes will be further established in this section.

It can be seen from expression (6) that the values of  $K_1/K_2$  have a linear relationship with the inductance of the filter inductor  $L$  when  $\Delta T$  is constant. Therefore, the relative quantity of inductance variations is equal to that of  $K_1/K_2$  variations, and the relationship between the relative quantity of  $K_1/K_2$  variations and the relative quantity of current amplitude changes can also be expressed by (18).

## 4 | On-Line Adjustment Strategy

### 4.1 | Linear Compensation

In the aforementioned analysis, the variation relationship between current amplitudes and the parameters  $K_1/K_2$  of the PPD controller caused by the parameter variations of the inverter components has been established. In particular, the constraint of current operating points can be removed when the relative quantity is used, as illustrated in Figure 5. The main purpose of

![Figure 6: A graph showing the relationship between the change of K1/K2 (%) on the y-axis and the change of current amplitude (%) on the x-axis. Blue asterisks represent simulation data, and a solid red line represents a linear curve fitted to the data. The linear curve is labeled (18).](c82c7d8107cba121734a9cfba891216d_img.jpg)

Figure 6: A graph showing the relationship between the change of K1/K2 (%) on the y-axis and the change of current amplitude (%) on the x-axis. Blue asterisks represent simulation data, and a solid red line represents a linear curve fitted to the data. The linear curve is labeled (18).

**FIGURE 6** | Linear curve fitted from linearization.

this paper is concentrated on improving the robustness of the PPD controller, so that the steady-state accuracy of reference current tracking is maintained well, even when inverter component parameters are varying. According to formula (18) and Figure 5, it is proposed that the relative variation corresponding to the initial  $K_1/K_2$  can be calculated when the error between the response current and its reference current is detected. After that, the parameters  $K_1/K_2$  can be adjusted online to eliminate the current tracking error caused by the change in inverter component parameters.

It is worth noting that the relationship expressed in (18) is non-linear. For fixed-point digital signal processor (DSP), although expression (18) can be achieved, to ensure accuracy, additional processing of the molecule is required, and the division operation consumes more time resources than linear calculation. The error compensation algorithm is implemented in the millisecond interrupt task of the DSP. If the error compensation algorithm can be calculated as soon as possible, the global variable  $K_1/K_2$  can be updated in time. This can ensure that the PPD controller, in real-time interruption, can adopt the new  $K_1/K_2$  in advance of some switching cycles, which will help to reduce the current errors quickly. Therefore, it is worth to linearizing expression (18).

A linearization method for (18) is proposed in this paper. The curve depicting the relative variation relationship between  $K_1/K_2$  and current amplitudes is obtained by the ordinary least squares method, which can be expressed by (19) finally,

$$y = K_{LC}x + M_0 \quad (19)$$

The slope is expressed by  $K_{LC}$  in (19), while  $M_0$  is a constant. The curve of formula (18) and the linear curve of (19) are plotted in Figure 6. It can be seen that they match well with a limited tolerance. Therefore, the rapidity of linear control can be guaranteed.

In detail, the relative variable  $\delta I_{LC}$  of current deviations can be calculated quickly by measuring the error between the real current response and its reference current, and then, the relative variation variable  $\delta K_{LC}$  of  $K_1/K_2$  can be obtained by formula (20).

$$\delta K_{LC} = K_{LC}\delta I_{LC} + M_0 \quad (20)$$

Furthermore, the relative variation of  $\delta K_{LC}$  can be transformed into the absolute variations of  $K_1/K_2$ , which can be added to the present values of  $K_1/K_2$ . Therefore, the on-line adjustment of  $K_1/K_2$  can quickly reduce the response current deviation

![](191a4a245a7d36d03be9a990d0f758f5_img.jpg)

**FIGURE 7** | Combined compensation strategy for robustness improvement of PPD controller.

### 4.2 | Integral Compensation

Although the current tracking error can be reduced quickly by using the proposed linear control described in the previous section, there still exists a part of static errors between the response current and its reference current. It is obvious that the error is mainly caused by the linearization of (18). Therefore, an integral part is introduced to eliminate the residual tracking error, and the expression is listed as follows.

$$\delta K_s = \int K_s \delta I_s(t) dt \quad (21)$$

where  $\delta K_s$  is the output variable of the integral compensation,  $K_s$  is the integral coefficient, and  $\delta I_s$  is the relative tracking error of the response current. In the same way,  $\delta K_s$  is transformed into the absolute variations of  $K_1/K_2$ , and then added to the present values of  $K_1/K_2$ . Finally,  $K_1$  and  $K_2$  can be adjusted online to completely eliminate static errors in reference current tracking.

$$G_i(s) = \frac{i_g}{i_{\text{ref}}} = \frac{K_{1,N}sT + K_{1,N} - K_{2,N}}{(sL + r)(1.5sT + 1)(sT + 1)} \quad (23)$$

$$\frac{I_g}{I_{\text{ref}}} = \frac{k(N_0 K_{\text{LC}} s + N_0 K_s)(s K_{1N} T + K_{1N} - K_{2N})}{s I_0(sL + r)(1.5sT + 1)(sT + 1) + k(sN_0 K_{\text{LC}} + N_0 K_s)(s K_{1N} T + K_{1N} - K_{2N})} \quad (24)$$

$$D(s) = 1.5s^4LT^2 + s^3(2.5I_0LT + 1.5I_0rT^2) + s^2(I_0L + 2.5I_0rT + kK_1TN_0K_{LC}) + s(I_0r + kK_{1-N}TN_0K_s + krN_0K_{LC}) + krN_0K_s \quad (25)$$

$$\begin{array}{ll} s^4 & 1.5LT^2 \quad I_0L + 2.5I_0rT + kK_{1,N}TN_0K_{LC} \quad krN_0K_S \\ s^3 & 2.5I_0LT + 1.5I_0rT^2 \quad I_0r + kK_{1,N}TN_0K_S + krN_0K_{LC} \\ s^2 & b_1 \quad b_2 \\ s^1 & c_1 \\ s^0 & d_1 \end{array} \quad (26)$$

$$b_1 = \frac{2.5I_0^2L^2T + 6.25I_0^2LrT^2 + 2.5I_0LkK_{1,N}T^2N_0K_{1C} + 1.5I_0^2rT^2 + 3.75I_0^2r^2T^3 + 1.5I_0rT^3kK_{1,N}N_0K_{1C}}{2.5I_0LT + 1.5I_0rT^2} - \frac{1.5LT^2I_0r - 1.5LT^3kK_{1,N}N_0K_S - 1.5LT^2krN_0K_{1C}}{2.5I_0LT + 1.5I_0rT^2} \quad (27)$$

The block diagram of the proposed combined compensation strategy with linear and integral controllers for the PPD controller is illustrated in Figure 7. Here,  $N_0$  is a constant for conversion

between absolute values and relative values, and  $K_{10}$  and  $K_{20}$  are the initial values of  $K_1/K_2$  in the PPD controller. It can be seen that the speed of combined compensation is slower than that of the PPD controller.

It should be pointed out that the Integral compensation and linear compensation in Figure 7 are not switched into the system at the same time. Linear compensation can quickly reduce grid-in current error, but it cannot completely eliminate grid-in current error. When the static errors meet the requirements, the integral compensation can be switched off; otherwise, the integral compensation needs to be switched on.

## 5 | The Stability of System

To analyse the stability of the entire control system, we redraw the control block diagram in Figure 8.  $G_{di}(s)$  represents the sampling delay, which is usually one switching cycle, and  $G_z(s)$  represents the PWM modulation delay, which is usually half a switching cycle. Since the switching frequency is high, the switching period  $T$  is small. Therefore, the total delay  $G_d(s)$  in the forward loop can be equivalent to an inertial part.

$$G_d(s) = e^{-1.5sT} \approx \frac{1}{1.5sT + 1} \quad (22)$$

Properly deform the part circled by the blue dotted line in Figure 8 into Figure 9.

Here,  $K_{1,N}$  and  $K_{2,N}$  in Figure 9 represent the PPD controller parameters that are regulated at the present moment by the proposed compensation strategy. According to the expression of the PPD controller, the transfer function of the grid-in current related to the reference current can be obtained.

![Figure 8: System control block diagram. The diagram shows a control loop starting with a reference current I_ref. It passes through a gain block N_0, a current controller block K_LC, and a gain block K_S. The output is then divided by s (1/s) and multiplied by the output current i_ref. This is summed with the output of K_LC. The result is multiplied by K_1 and K_2. The outputs of K_1 and K_2 are summed and then multiplied by e^{-sT}. This is summed with the output of K_S. The final result is multiplied by M_0. The output M_0 is then used to generate a PWM signal u_g through a series of blocks: 1/K_pwm, G_d1, G_z, K_pwm, 1/(sL+r), and a unity gain block. The PWM signal u_g is then used to generate the grid current i_g through a unity gain block and a summation block. The grid current i_g is then used to calculate the RMS current I_g through a summation block and a square root block.](1956f44611abd5c3c41049836aa78ad8_img.jpg)

Figure 8: System control block diagram. The diagram shows a control loop starting with a reference current I\_ref. It passes through a gain block N\_0, a current controller block K\_LC, and a gain block K\_S. The output is then divided by s (1/s) and multiplied by the output current i\_ref. This is summed with the output of K\_LC. The result is multiplied by K\_1 and K\_2. The outputs of K\_1 and K\_2 are summed and then multiplied by e^{-sT}. This is summed with the output of K\_S. The final result is multiplied by M\_0. The output M\_0 is then used to generate a PWM signal u\_g through a series of blocks: 1/K\_pwm, G\_d1, G\_z, K\_pwm, 1/(sL+r), and a unity gain block. The PWM signal u\_g is then used to generate the grid current i\_g through a unity gain block and a summation block. The grid current i\_g is then used to calculate the RMS current I\_g through a summation block and a square root block.

FIGURE 8 | Figure 8 System control block diagram.

![Figure 9: Block diagram of PPD controller obtained after deformation. The diagram shows a reference current I_ref being compared with a reference current I_ref through a gain block N_0. The error signal is then multiplied by K_1 and K_2. The outputs of K_1 and K_2 are summed and then multiplied by e^{-sT}. This is summed with the output of N_0. The final result is multiplied by M_0. The output M_0 is then used to generate a PWM signal u_g through a series of blocks: 1/K_pwm, G_d1, G_z, K_pwm, 1/(sL+r), and a unity gain block. The PWM signal u_g is then used to generate the grid current i_g through a unity gain block and a summation block.](997233d405f0d4b89ddeb7683e047f66_img.jpg)

Figure 9: Block diagram of PPD controller obtained after deformation. The diagram shows a reference current I\_ref being compared with a reference current I\_ref through a gain block N\_0. The error signal is then multiplied by K\_1 and K\_2. The outputs of K\_1 and K\_2 are summed and then multiplied by e^{-sT}. This is summed with the output of N\_0. The final result is multiplied by M\_0. The output M\_0 is then used to generate a PWM signal u\_g through a series of blocks: 1/K\_pwm, G\_d1, G\_z, K\_pwm, 1/(sL+r), and a unity gain block. The PWM signal u\_g is then used to generate the grid current i\_g through a unity gain block and a summation block.

FIGURE 9 | Figure 9 Block diagram of PPD controller obtained after deformation.

![Figure 10: Simplified closed-loop system. The diagram shows a reference current I_ref being compared with a reference current I_ref through a gain block N_0. The error signal is then multiplied by K_LC and K_S. The outputs of K_LC and K_S are summed and then divided by s (1/s). This is summed with the output of N_0. The final result is multiplied by M_0. The output M_0 is then used to generate a PWM signal u_g through a series of blocks: 1/K_pwm, G_d1, G_z, K_pwm, 1/(sL+r), and a unity gain block. The PWM signal u_g is then used to generate the grid current i_g through a unity gain block and a summation block.](d793cf7c174b89eb024d132f00679787_img.jpg)

Figure 10: Simplified closed-loop system. The diagram shows a reference current I\_ref being compared with a reference current I\_ref through a gain block N\_0. The error signal is then multiplied by K\_LC and K\_S. The outputs of K\_LC and K\_S are summed and then divided by s (1/s). This is summed with the output of N\_0. The final result is multiplied by M\_0. The output M\_0 is then used to generate a PWM signal u\_g through a series of blocks: 1/K\_pwm, G\_d1, G\_z, K\_pwm, 1/(sL+r), and a unity gain block. The PWM signal u\_g is then used to generate the grid current i\_g through a unity gain block and a summation block.

FIGURE 10 | Simplified closed-loop system.

a constant value; only represents the relationship between the RMS value  $I_g$  and the instantaneous value  $i_g$  of the grid-in current. However,  $k$  can be determined as a positive value. Finally, Figure 8 can be redrawn as Figure 10.

According to Figure 8, the transfer function of the control system can be determined as expression (24). Considering  $K_{1,N} - K_{2,N} = r$ , The characteristic equation of the control system can be obtained as expression (25).

According to the physical meaning of the coefficients in expression (25), it can be sure that all coefficients in expression (25) are positive.

List the Routh stability criterion array as expression (26). The expression for  $b_1$  can be found as expression (27). Among the above parameters,  $T$  is the switching period, which is smaller than other parameters in value, and furthermore,  $T^2$  and  $T^3$  are much smaller in value. Therefore,  $T^2$  and  $T^3$  can be approximated as zero, and expression (28) can be approximated as (28).

$$b_1 \approx \frac{2.5I_0^2L^2T}{2.5I_0LT} = I_0L \quad (28)$$

Similarly,  $b_2$ ,  $c_1$  and  $d_1$  can be obtained:

$$b_2 = \frac{2.5I_0LTkrN_0K_{LC} + 1.5I_0rT^2krN_0K_{LC}}{2.5I_0LT + 1.5I_0rT^2} \approx krN_0K_{LC} \quad (29)$$

$$c_1 = \frac{I_0^2Lr + I_0LkK_{1,N}TN_0K_S + I_0LkrN_0K_{LC}(1 - 2.5T)}{I_0L} \quad (30)$$

$$d_1 = krN_0K_{LC} \quad (31)$$

Re-list the Routh stability criterion. It can be found that once the switching frequency is higher than 2.5 Hz,  $c_1$  is positive.

TABLE 4 | Main parameters of 3 kW prototype.

| Parameters                | Value       |
|---------------------------|-------------|
| Rated power $P_N$         | 3 kW        |
| DC bus voltage $U_{dc}$   | 360 V       |
| Inductance $L$            | 1.92 mH     |
| Resistance $R$            | 50 mΩ       |
| Power grid $u_g$          | 220 V/50 Hz |
| Switching frequency $f_s$ | 18 kHz      |

Therefore, the above parameters in the first column are all positive. According to the Routh stability criterion, it can be determined that the control system is stable.

## 6 | Simulation Results

To verify the effectiveness of the proposed droop control strategy, a simulation model has been established in Matlab/Simulink according to Figure 1, Figure 2, and Figure 7. The main parameters of the single-phase grid-connected inverter are listed in Table 4.

Figure 11 shows the simulation waveforms of the grid-in current, reference current, and amplitude error when the filter inductance is reduced by 20%. It can be seen that the inductance decrease leads to an amplitude change of the tracking current, which is about 1.5A and higher than the reference current. The current deviation decreases rapidly to less than 0.7A after the linear control is enabled at 0.1s; after 0.2s, the integral control is enabled, and the residual current tracking error gradually decreasing to zero.

## 7 | Experiment Results

In order to verify the correctness of the proposed combined control, equivalent experiments have been conducted on a 3 kW prototype as shown in Figure 12. The combined controllers and PPD controller are implemented based on TI company's DSP TMS320F28035, and the model number of IGBT is FGA40N65SMD, the same as in the previous analysis in Section II. A. Other specific parameters are shown in Table 4, and are in agreement with the simulation model.

### 7.1 | Verification of Filter Inductance Reducing

Figure 13 shows the experimental waveforms of the grid-in current and reference current with an equivalent filter inductance

![Figure 11: Compensation result of filter inductance variation with the proposed combined controller. The figure consists of three main oscilloscope traces and three zoomed-in insets. The main traces are labeled 'No control', 'Linear compensation', and 'Combined compensation' from left to right. The 'No control' trace shows a highly distorted grid current waveform. The 'Linear compensation' trace shows a cleaner waveform but with some residual distortion. The 'Combined compensation' trace shows a nearly perfect sinusoidal waveform. The zoomed-in insets show the grid current (i_g) and reference current (i_ref) waveforms. The first inset (top left) shows i_g and i_ref with a scale of 20A/div. The second inset (top middle) shows i_g and i_ref with a scale of 20A/div. The third inset (top right) shows i_g with a scale of 5ms/div. The bottom trace shows the grid current (i_g) with a scale of 0.5A/div. The time base for the main traces is 50ms/div.](3121afa7ca030b22ee0345864ca6f38b_img.jpg)

Figure 11: Compensation result of filter inductance variation with the proposed combined controller. The figure consists of three main oscilloscope traces and three zoomed-in insets. The main traces are labeled 'No control', 'Linear compensation', and 'Combined compensation' from left to right. The 'No control' trace shows a highly distorted grid current waveform. The 'Linear compensation' trace shows a cleaner waveform but with some residual distortion. The 'Combined compensation' trace shows a nearly perfect sinusoidal waveform. The zoomed-in insets show the grid current (i\_g) and reference current (i\_ref) waveforms. The first inset (top left) shows i\_g and i\_ref with a scale of 20A/div. The second inset (top middle) shows i\_g and i\_ref with a scale of 20A/div. The third inset (top right) shows i\_g with a scale of 5ms/div. The bottom trace shows the grid current (i\_g) with a scale of 0.5A/div. The time base for the main traces is 50ms/div.

**FIGURE 11** | Compensation result of filter inductance variation with the proposed combined controller

![Figure 12: Experimental platform. The image shows a laboratory setup with a laptop, an oscilloscope, and a custom-built electronic circuit board. The circuit board is populated with various components, including an inductor, capacitors, and integrated circuits. Cables connect the circuit board to the oscilloscope and laptop for data acquisition and control.](efca2dce0095c9dc2a68e9af6b2bfd40_img.jpg)

Figure 12: Experimental platform. The image shows a laboratory setup with a laptop, an oscilloscope, and a custom-built electronic circuit board. The circuit board is populated with various components, including an inductor, capacitors, and integrated circuits. Cables connect the circuit board to the oscilloscope and laptop for data acquisition and control.

**FIGURE 12** | Experimental platform.

variation, and the equivalent inductance is reduced by 20% of the nominal inductance. It can be seen that the magnitude of the response current is 5.43A larger than the reference current at the beginning, which is consistent with the trend of previous simulation results. Then, the current deviation decreases rapidly to less than 1.01A after the linear control is introduced, which indicates that the static tracking error can be quickly reduced by the linear control. After enabling the integral control, the current tracking error is decreased to zero gradually.

### 7.2 | Verification of Filter Inductance Increasing

The waveforms of the grid-in current and reference current are shown in Figure 14 when the equivalent filter inductance is 20% of the nominal inductance. It can be seen that the increase in filter inductance leads to an amplitude decrease in the response current, which is about 6.44A, and smaller than the reference current, consistent with the trend of previous simulation results. The current deviation rapidly decreases to less than 0.41A when the linear control is enabled. In the same way, the current deviation decreases gradually to zero with the integral control. Therefore, comprehensive simulation results and equivalent experimental results demonstrate that the proposed combined control is able to eliminate the influence of inverter component parameters' variations on steady-state performance quickly and effectively.

### 7.3 | Dead Time Varying

As dead time is a typical non-ideal factor, the comparative experimental results before and after the implementation of the proposed composite controller, following the modification to account for the dead time change, are presented in Figure 15. To provide a more effective illustration, it is essential to note that dead time pre-compensation is not executed, and the composite controller is not activated during the initial phase. Subsequently, the composite controller is enabled following a duration of operation. It can be seen that when dead-time compensation remains disabled, the grid current waveform demonstrates pronounced distortion near zero-crossing regions, accompanied by an attenuated current amplitude. Upon activation of the composite controller, substantial waveform improvement is achieved, with dead-time variation-induced anomalies effectively mitigated (See Figure 15).

### 7.4 | System Dynamic Characteristic

The composite controller and PPD controller are decoupled via deployment in interrupt priority levels. To verify the decoupling effectiveness, validation is conducted by intentionally varying filter inductance parameters, with system dynamic characteristics being compared under two operational conditions, with and without the composite controller activation. The experimental results are shown in Figure 16.

It can be observed that the system possesses rapid dynamic characteristics, regardless of whether the steady-state error of the system is compensated or not. This demonstrates that the composite controller does not affect the dynamic characteristics of the system.

### 7.5 | System Robustness

To validate the system's fault ride-through capability, experimental verification is conducted through grid voltage sag and recovery scenarios, emulated by a grid simulator. The corresponding experimental results are presented in Figure 17. Experimental

![Figure 13: Compensation results with filter inductance reducing. (a) Overall waveforms showing three channels: grid voltage u_g, grid current i_g, and a third signal. (b) Without Compensation: I_RMS = 12.5A, I_err = 5.43A. (c) Linea compensation only: I_RMS = 6.06A, I_err = 1.01A. (d) Combined compensation: I_RMS = 7.06A, I_err = 0.01A. The waveforms show that as inductance decreases, the grid current i_g tracks the grid voltage u_g more closely, reducing the error current I_err.](b93cbfb52e37619e688175a6aad9edd9_img.jpg)

Figure 13: Compensation results with filter inductance reducing. (a) Overall waveforms showing three channels: grid voltage u\_g, grid current i\_g, and a third signal. (b) Without Compensation: I\_RMS = 12.5A, I\_err = 5.43A. (c) Linea compensation only: I\_RMS = 6.06A, I\_err = 1.01A. (d) Combined compensation: I\_RMS = 7.06A, I\_err = 0.01A. The waveforms show that as inductance decreases, the grid current i\_g tracks the grid voltage u\_g more closely, reducing the error current I\_err.

FIGURE 13 | Compensation results with filter inductance reducing.

![Figure 14: Compensation results with filter inductance increasing. (a) Overall waveforms. (b) Without Compensation: I_RMS = 6.44A, I_err = 0.63A. (c) Linea compensation only: I_RMS = 7.48A, I_err = 0.41A. (d) Combined compensation: I_RMS = 7.06A, I_err = 0.01A. As inductance increases, the grid current i_g becomes more distorted and deviates from the grid voltage u_g, leading to a higher error current I_err.](bedcca5cdf168e3508ef511d94ec514c_img.jpg)

Figure 14: Compensation results with filter inductance increasing. (a) Overall waveforms. (b) Without Compensation: I\_RMS = 6.44A, I\_err = 0.63A. (c) Linea compensation only: I\_RMS = 7.48A, I\_err = 0.41A. (d) Combined compensation: I\_RMS = 7.06A, I\_err = 0.01A. As inductance increases, the grid current i\_g becomes more distorted and deviates from the grid voltage u\_g, leading to a higher error current I\_err.

FIGURE 14 | Compensation results with filter inductance increasing.

![Figure 15: Compensation for dead-time variations implemented by the composite controller. (a) Overall waveforms showing 'Not enabled' and 'Enabled' states. (b) Without Compensation: I_RMS = 11.3A, I_err = 8.00A. (c) Combined compensation: I_RMS = 7.76A, I_err = 0.01A. The composite controller effectively compensates for dead-time variations, resulting in a grid current i_g that closely follows the grid voltage u_g.](925f55ce69802b9d3b00546382663ee2_img.jpg)

Figure 15: Compensation for dead-time variations implemented by the composite controller. (a) Overall waveforms showing 'Not enabled' and 'Enabled' states. (b) Without Compensation: I\_RMS = 11.3A, I\_err = 8.00A. (c) Combined compensation: I\_RMS = 7.76A, I\_err = 0.01A. The composite controller effectively compensates for dead-time variations, resulting in a grid current i\_g that closely follows the grid voltage u\_g.

FIGURE 15 | The compensation for dead-time variations implemented by the composite controller (a) The overall waveforms, (b) Without Compensation, (c) Combined compensation,  $I_{err} = 0.01A$ .

![Figure 16: Compensation for dead-time variations implemented by the composite controller. (a) without composite controller: I_RMS = 7.43A, I_err = 8.00A. (b) with composite controller: I_RMS = 5.91A, I_err = 800mA. The composite controller significantly reduces the error current I_err compared to the case without it.](e8ff6e66c77a8e96203c9f8db8f0986f_img.jpg)

Figure 16: Compensation for dead-time variations implemented by the composite controller. (a) without composite controller: I\_RMS = 7.43A, I\_err = 8.00A. (b) with composite controller: I\_RMS = 5.91A, I\_err = 800mA. The composite controller significantly reduces the error current I\_err compared to the case without it.

FIGURE 16 | The compensation for dead-time variations implemented by the composite controller.

observations demonstrate that the composite controller exhibits no detrimental effect on the system's fault ride-through capability.

## 8 | Conclusion

An on-line adjusting method for parameters of the PPD controller is proposed in this paper, which can improve the robustness of model predictive control against inverter parameter variations. The effectiveness of the proposed combined control has been verified by simulation and experimental results. The main conclusions are drawn as follows.

1. The variation in filter inductances is the dominant factor affecting steady-state tracking performance of the PPD con-

![Figure 17: System's fault ride-through capability. (a) grid voltage sag: shows a green grid voltage waveform (u_g) sagging and a blue grid current waveform (i_g) following it. The grid voltage sag is indicated by a yellow arrow. The bottom panel shows RMS values: 均方根 6.60 A and 均方根 172 V. (b) grid voltage recovery: shows the green grid voltage waveform (u_g) recovering and the blue grid current waveform (i_g) following it. The grid voltage recovery is indicated by a yellow arrow. The bottom panel shows RMS values: 均方根 6.84 A and 均方根 178 V. Both plots have a time scale from 10.0ms to 337.600ms and a frequency scale < 10 Hz.](adb1f42239329fa8283d1a40005f989f_img.jpg)

Figure 17: System's fault ride-through capability. (a) grid voltage sag: shows a green grid voltage waveform (u\_g) sagging and a blue grid current waveform (i\_g) following it. The grid voltage sag is indicated by a yellow arrow. The bottom panel shows RMS values: 均方根 6.60 A and 均方根 172 V. (b) grid voltage recovery: shows the green grid voltage waveform (u\_g) recovering and the blue grid current waveform (i\_g) following it. The grid voltage recovery is indicated by a yellow arrow. The bottom panel shows RMS values: 均方根 6.84 A and 均方根 178 V. Both plots have a time scale from 10.0ms to 337.600ms and a frequency scale < 10 Hz.

FIGURE 17 | The system's fault ride-through capability.

- troller, and a dealing method of equaling the variations of conduction voltage drops and parasitic resistances to inductance variations is proposed.
2. The relative variation relationship between the parameters  $K_1/K_2$  of the PPD controller and grid-in current amplitudes is obtained, which can get rid of the constraint of current working points, and the linear function of the linear control is built.
  3. In order to eliminate the compensation error of the linear control, an integral part is introduced into the combined control structure. The robustness of the PPD controller is improved significantly.

## Author Contributions

**Di Wu:** conceptualization; project administration; supervision; writing – review and editing. **yan fu:** writing – original draft. **Mingming Li:** data curation; formal analysis; funding acquisition; investigation; software; supervision; validation. **Luoming OuYang:** investigation.

## Conflicts of Interest

The authors declare no conflicts of interest.

## Data Availability Statement

The data that support the findings of this study are available from the corresponding author upon reasonable request

## References

1. P. Acuna, R. Aguilera, A. Ghias, et al., "Cascade-Free Model Predictive Control for Single-Phase Grid-Connected Power Converters," *IEEE Transactions on Industrial Electronics* 64, no. 1 (2017): 285–294.
2. W. Wu, Y. Li, Y. He, et al., "Damping Methods for Resonances Caused by LCL-Filter-Based Current-Controlled Grid-Tied Power Inverters," *IEEE Transactions on Industrial Electronics* 64, no. 9 (September 2017): 7402–7413.
3. F. Blaabjerg, Z. Chen, and S. B. Kjaer, "Power Electronics as Efficient Interface in Dispersed Power Generation Systems," *IEEE Transactions on Power Electronics* 19, no. 5 (September 2004): 1184–1194.
4. B. Liu, M. Su, J. Yang, et al., "Combined Reactive Power Injection Modulation and Grid Current Distortion Improvement Approach for H6 Transformer-Less Photovoltaic Inverter," *IEEE Transactions on Energy Conversion* 32, no. 4 (2017): 1456–1467.
5. N. Jin, C. Gan, and L. Guo, "Predictive Control of Bidirectional Voltage Source Converter With Reduced Current Harmonics and Flexible Power Regulation Under Unbalanced Grid," *IEEE Transactions on Energy Conversion* 33, no. 3 (2017): 1118–1131.
6. L. Wang, C.-S. Lam, and M.-C. Wong, "Multifunctional Hybrid Structure of SVC and Capacitive Grid-Connected Inverter (SVC/CGCI) for Active Power Injection and Nonactive Power Compensation," *IEEE Transactions on Industrial Electronics* 66, no. 3 (March 2019): 1660–1670.
7. S. Mukherjee, V. R. Chowdhury, P. Shamsi, et al., "Grid Voltage Estimation and Current Control of Single-Phase Grid-Connected Converter Without Grid Voltage Sensor," *IEEE Transactions on Power Electronics* 33, no. 5 (May 2017): 4407–4418.
8. Y. He, H.-S.-H. Chung, C.-N.-M. Ho, et al., "Modified Cascaded Boundary-Deadbeat Control for a Virtually-Grounded Three-Phase Grid-Connected Inverter With LCL Filter," *IEEE Transactions on Power Electronics* 32, no. 10 (October 2017): 8163–8180.
9. D. G. Holmes, T. A. Lipo, B. P. McGrath, et al., "Optimized Design of Stationary Frame Three Phase AC Current Regulators," *IEEE Transactions on Power Electronics* 24, no. 11 (November 2009): 2417–2426.
10. Q.-N. Trinh, F. H. Choo, and P. Wang, "Control Strategy to Eliminate Impact of Voltage Measurement Errors on Grid Current Performance of Three-Phase Grid-Connected Inverters," *IEEE Transactions on Industrial Electronics* 64, no. 9 (September 2017): 7508–7519.
11. D. Chen, J. Zhang, and Z. Qian, "An Improved Repetitive Control Scheme for Grid-Connected Inverter With Frequency-Adaptive Capability," *IEEE Transactions on Industrial Electronics* 60, no. 2 (February 2013): 814–823.
12. Z. Zou, K. Zhou, Z. Wang, et al., "Frequency Adaptive Fractional-Order Repetitive Control of Shunt Active Power Filters," *IEEE Transactions on Industrial Electronics* 62, no. 3 (March 2015): 1659–1668.
13. C. N.-M. Ho, V. S. P. Cheung, and H. S.-H. Chung, "Constant-frequency Hysteresis Current Control of Grid-Connected VSI Without Bandwidth Control," *IEEE Transactions on Power Electronics* 24, no. 11 (November 2009): 2484–2495.
14. S. Buso, L. Malesani, and P. Mattavelli, "Comparison of Current Control Techniques for Active Filter Applications," *IEEE Transactions on Industrial Electronics* 45, no. 5 (October 1998): 722–729.
15. Y. Zhang, W. Xie, Z. Li, et al., "Model Predictive Direct Power Control of a PWM Rectifier With Duty Cycle Optimization," *IEEE Transaction on Power Electronics* 28, no. 11 (November 2013): 5343–5351.
16. J. Hu and Z. Q. Zhu, "Improved Voltage-Vector Sequences on Dead-Beat Predictive Direct Power Control of Reversible Three-Phase Grid-Connected Voltage-Source Converters," *IEEE Transactions on Power Electronics* 28, no. 1 (January 2013): 254–267.
17. H. Xiao, M. Li, L. Wu, et al., "A Novel Current Controller for Grid-Connected Voltage-Source-Inverters," *IEEE Transactions on Industrial Electronics* 68, no. 1 (2020): 553–562, <https://doi.org/10.1109/TIE.2019.2962441>.
18. G. Grandi, J. Loncarski, and O. Dordevic, "Analysis and Comparison of Peak-to-Peak Current Ripple in Two-Level and Multilevel PWM Inverters," *IEEE Transactions on Industrial Electronics* 62, no. 5 (May 2015): 2721–2730.
19. A. K. Sadigh, V. Dargahi, and K. A. Corzine, "Analytical Determination of Conduction and Switching Power Losses in Flying-Capacitor-Based Active Neutral-Point-Clamped Multilevel Converter," *IEEE Transactions on Power Electronics* 31, no. 8 (August 2016): 5473–5494.
20. R. A. Mastromauro, M. Liserre, and A. Dell'Aquila, "Study of the Effects of Inductor Nonlinear Behavior on the Performance of Current Controllers for Single-Phase PV Grid Converters," *IEEE Transactions on Industrial Electronics* 55, no. 5 (May 2008): 2043–2052.
21. C. Chapelsky, J. Salmon, and A. M. Knight, "Design of the Magnetic Components for High-Performance Multilevel Half-Bridge Inverter Legs," *IEEE Transactions on Magnetics* 45, no. 10 (October 2009): 4785–4788.
22. A. Guha and G. Narayanan, "Impact of Dead Time on Inverter Input Current, DC-Link Dynamics, and Light-Load Instability in Rectifier-Inverter-Fed Induction Motor Drives," *IEEE Transactions on Industry Applications* 54, no. 2 (2018): 1414–1424.