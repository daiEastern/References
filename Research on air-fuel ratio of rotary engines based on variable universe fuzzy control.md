

PAPER • OPEN ACCESS

# Research on air-fuel ratio of rotary engines based on variable universe fuzzy control

To cite this article: Xiaocan Chai *et al* 2024 *J. Phys.: Conf. Ser.* **2782** 012022

View the [article online](#) for updates and enhancements.

You may also like

- [Study on Composite Control Strategy of Transient Air-Fuel Ratio for Gasoline Engine Based on Model](#)  
Dandan Song and Yuelin Li
- [Predictive Control Of Transient Air-Fuel Ratio for Gasoline Engine Based on Wavelet Network Inversion](#)  
Dandan Song and Yuelin Li
- [Monitoring the air-fuel ratio of internal combustion engines using a neural network](#)  
S D Walters, M M De Zoysa and R J Howlett

# Research on air-fuel ratio of rotary engines based on variable universe fuzzy control

Xiaocan Chai, Jinxiang Liu\* and Wenchao Pan

Beijing Institute of Technology, Beijing 100081, China

\*Corresponding author's e-mail: liujx@bit.edu.cn

**Abstract.** A study on the air-fuel ratio control system for the Wankel rotary engine was conducted, where the overall model of the engine was developed in MATLAB/Simulink based on the mean value model. The variable universe fuzzy integral composite control algorithm was applied to feedback control, and the construction and simulation of the control algorithm were completed in MATLAB/Simulink. The results indicate that compared to PID control, variable universe fuzzy control reduced the engine's fuel injection error by 60.37% and 35.7% under steady-state and transient conditions, respectively. This demonstrates the favorable control effectiveness of variable universe fuzzy control in rotary engines, providing insights and methods for future research on rotary engine control systems.

## 1. Introduction

The Wankel rotary engine (WRE), propelled by triangular rotors in a rotary piston configuration [1, 2], offers advantages over traditional reciprocating piston engines, including high power-to-weight ratio, compact structure, reduced part count, smooth operation, easy maintenance, and suitability for miniaturization [3–4]. These attributes make it highly suitable as a power source for medium and small unmanned aerial vehicles (UAVs) and other flight equipment.

The air-fuel ratio (AFR) is the mass flow ratio of air to fuel of the mixture in the cylinder, often described by the ratio of AFR in the cylinder to the stoichiometric value of AFR, denoted by the excess air ratio  $\lambda$ , to indicate the concentration of the mixture. Some methods were put forward to control the engine [5] and fuzzy control is widely used in the control of the engine [6, 7]. The inherent drawbacks of small rotary engines, such as poor combustion, low efficiency, and high fuel consumption, pose significant challenges. Traditional carburetor-based fuel supply systems fail to precisely regulate the fuel injection process. However, the introduction of electronic control technologies like AFR control can effectively enhance combustion conditions, thereby improving the performance of rotary engines. WRE differs from traditional engines in control logic, necessitating specialized research and exploration.

## 2. Formulation of model

The mean value model (MVM) [8, 9] has been widely employed in modeling reciprocating piston engines, enabling the description of dynamic processes such as intake, injection, and combustion. However, there has been relatively less focus on the specific dynamic modeling of rotary engines. A WRE of a single rotor operates similarly to the four-stroke engine of two cylinders [10], thus rendering the average model suitable for the overall modeling of rotary engines. The overall model structure for small rotary engines is depicted in **Figure 1**.

![Creative Commons Attribution 4.0 International License logo](a4c38758d2beb7324d786510e83609ec_img.jpg)

The image shows the Creative Commons Attribution 4.0 International License logo, which consists of two circles: one with 'cc' and another with a person icon.

Creative Commons Attribution 4.0 International License logo

Content from this work may be used under the terms of the [Creative Commons Attribution 4.0 licence](#). Any further distribution of this work must maintain attribution to the author(s) and the title of the work, journal citation and DOI.

![Schematic diagram of the MVM of a Wankel engine. The diagram shows an ECU connected to an EFI (Electronic Fuel Injection) system. The EFI system controls the fuel flow (m_dot_fi) and the throttle valve angle (alpha). The intake pipe (Intake Pipe) leads to a combustion chamber (Combustion Chamber) with a wet wall. The throttle valve controls the air flow (m_dot_at). The combustion chamber is connected to an exhaust pipe (Exhaust Pipe) which leads to an out load (Out Load) and an oxygen sensor (Oxygen Sensor). The out load is connected to a load (I) and has a rotational speed (n) and temperature (T_L). The combustion chamber also has an inlet temperature (T_i) and outlet temperature (T_f). The fuel flow is split into fuel vapor (m_dot_fv) and fuel film (m_dot_ff). The total air-fuel mixture flow is m_dot_ac + m_dot_fi.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

Schematic diagram of the MVM of a Wankel engine. The diagram shows an ECU connected to an EFI (Electronic Fuel Injection) system. The EFI system controls the fuel flow (m\_dot\_fi) and the throttle valve angle (alpha). The intake pipe (Intake Pipe) leads to a combustion chamber (Combustion Chamber) with a wet wall. The throttle valve controls the air flow (m\_dot\_at). The combustion chamber is connected to an exhaust pipe (Exhaust Pipe) which leads to an out load (Out Load) and an oxygen sensor (Oxygen Sensor). The out load is connected to a load (I) and has a rotational speed (n) and temperature (T\_L). The combustion chamber also has an inlet temperature (T\_i) and outlet temperature (T\_f). The fuel flow is split into fuel vapor (m\_dot\_fv) and fuel film (m\_dot\_ff). The total air-fuel mixture flow is m\_dot\_ac + m\_dot\_fi.

**Figure 1.** Schematic of MVM of wankel engine.

The throttle flow rate model's construction primarily relies on the following formula:

$$\left\{ \begin{array}{l} \dot{m}_{at} = c_{at} \frac{P_a}{\sqrt{T_a}} \beta_1(\theta) \beta_2(P_r) \\ \beta_1(\theta) = 1 - 1.4073 \cos(\theta) + 0.4087 \cos^2(\theta) \\ \beta_2(P_r) = \begin{cases} \frac{1}{0.74} \sqrt{P_r^{0.4404} - P_r^{2.3143}}, & P_r \ge 0.4125 \\ 1, & P_r < 0.4125 \end{cases} \\ P_r = \frac{P_m}{P_a} \end{array} \right. \quad (1)$$

The inlet flow rate model is as follows:

$$\left\{ \begin{array}{l} \dot{m}_{ac} = \frac{V_h \eta_v P_m n}{60 R T_m} \\ \dot{p}_m = \frac{R T_m}{V_m} (\dot{m}_{at} - \dot{m}_{ac}) \end{array} \right. \quad (2)$$

The fuel evaporation model is represented as follows:

$$\left\{ \begin{array}{l} \dot{m}_{fv} = (1 - x_f) \dot{m}_{fi} \\ \dot{m}_{ff} = -\frac{1}{\tau_f} \dot{m}_{ff} + x_f \dot{m}_{fi} \\ \dot{m}_f = \dot{m}_{fv} + \dot{m}_{ff} \end{array} \right. \quad (3)$$

The output response delay of a sensor is typically described as a first-order inertial element, and the transfer function is represented as follows:

$$G(s) = \frac{1}{\tau_\lambda s + 1} \quad (4)$$

The power output model is given by

$$\dot{n} = \frac{T_i - T_f - T_L}{I} \quad (5)$$

The  $\dot{m}_{ac}$  represents air mass flow rate into the cylinder,  $\theta$  is throttle degree of throttle,  $\dot{m}_{am}$  represents intake manifold air mass flow rate,  $P_m$  represents manifold pressure,  $V_h$  represents rotary engine displacement,  $V_m$  represents total volume of intake manifold,  $X_f$  represents of fuel portion deposited on the manifold wall  $\tau_f$  represents the fuel film constant,  $\dot{m}_{fi}$  represents injected fuel mass flow rate,  $\dot{m}_{fv}$  represents mass flow rate of evaporated fuel,  $m_f$  represents the fuel mass on the wall,  $\eta_v$  represents volumetric efficiency,  $n$  represents engine speed.

![Figure 2: A line graph showing Throttle Opening Degree (°) on the y-axis (ranging from 30 to 90) versus Time (s) on the x-axis (ranging from 0 to 14). The throttle opening is constant at 40° from t=0 to t=5s. At t=5s, it jumps to 75° and remains constant until t=10.5s. At t=10.5s, it begins to decrease, reaching 40° by t=12s, and remains at 40° until t=14s.](09af5b86cf9391543d22db5f2129b3ca_img.jpg)

Figure 2: A line graph showing Throttle Opening Degree (°) on the y-axis (ranging from 30 to 90) versus Time (s) on the x-axis (ranging from 0 to 14). The throttle opening is constant at 40° from t=0 to t=5s. At t=5s, it jumps to 75° and remains constant until t=10.5s. At t=10.5s, it begins to decrease, reaching 40° by t=12s, and remains at 40° until t=14s.

**Figure 2.** Throttle opening degree in the experiment.

We made a validation and the results are shown in **Figure 2**. The results of the air-fuel ratio and speed obtained through experiments and simulations are shown in **Figure 3**. When the throttle degree increases, the mass of intake air increases while the fuel injection mass lags behind, resulting in an increase in the air-fuel ratio. After 10 seconds, the throttle degree decreases, and the intake of air decreases, resulting in a decrease in the AFR due to hypoxia. The results show that the MVM of the WRE does not differ by more than 5% from the actual air-fuel ratio, which is in agreement with the accuracy of the model.

![Figure 3: Two side-by-side line graphs. Graph (a) shows Engine Speed (r/min) on the y-axis (4000 to 7500) versus Time (s) on the x-axis (0.0 to 14.0). It compares Experiment Speed (solid line) and Simulation Speed (dashed line), showing a peak around 7000 r/min at t=7s. Graph (b) shows Air Fuel Ratio on the y-axis (13.5 to 15.5) versus Time (s) on the x-axis (0.0 to 14.0). It compares Experiment AFR (solid line) and Simulation AFR (dashed line), showing a peak around 15.2 at t=6s and a dip around 14.0 at t=10s.](2db53d6ef524be5cde118e647f73ed90_img.jpg)

Figure 3: Two side-by-side line graphs. Graph (a) shows Engine Speed (r/min) on the y-axis (4000 to 7500) versus Time (s) on the x-axis (0.0 to 14.0). It compares Experiment Speed (solid line) and Simulation Speed (dashed line), showing a peak around 7000 r/min at t=7s. Graph (b) shows Air Fuel Ratio on the y-axis (13.5 to 15.5) versus Time (s) on the x-axis (0.0 to 14.0). It compares Experiment AFR (solid line) and Simulation AFR (dashed line), showing a peak around 15.2 at t=6s and a dip around 14.0 at t=10s.

(a) Engine Speed change with time      (b) Engine AFR change with time

**Figure 3.** Experiment validation results.

Based on experimentally calibrated fuel injection quantities, different operating points are defined by varying throttle positions and engine speeds. By calibrating experiments, a basic fuel injection flow rate map (MAP) is obtained in **Figure 4**.

![Figure 4: A 3D surface plot representing the fuel injection map of a Wankel engine. The vertical axis is 'Fuel flow (g/s)' ranging from 0.0 to 0.7. The horizontal axis is 'Speed (r/min)' ranging from 3000 to 8000. The depth axis is 'Throttle degree (°)' ranging from 20 to 90. The surface shows a complex, non-linear relationship between these three variables, with fuel flow generally increasing with speed and throttle position.](6bbc398f520a7bcc5491cab18d3e4cac_img.jpg)

Figure 4: A 3D surface plot representing the fuel injection map of a Wankel engine. The vertical axis is 'Fuel flow (g/s)' ranging from 0.0 to 0.7. The horizontal axis is 'Speed (r/min)' ranging from 3000 to 8000. The depth axis is 'Throttle degree (°)' ranging from 20 to 90. The surface shows a complex, non-linear relationship between these three variables, with fuel flow generally increasing with speed and throttle position.

**Figure 4.** Fuel injection map of Wankel engine.

## 3. Controller design and simulation

### 3.1 Fuzzy Controller Design

For the complex and highly nonlinear operating conditions of rotary engines, to achieve better control over the AFR, a variable universe fuzzy control (VUFC) method, and an intelligent integral controller are introduced based on fuzzy control to enhance control accuracy. Thus, a variable universe fuzzy integral composite control strategy illustrated in **Figure 5** is proposed.

![Figure 5: Schematic of Wankel Engine AFR Control System. The diagram shows a control loop where 'Target lambda' is compared with 'Sensor lambda' (from an 'Oxygen sensor'). The error signal goes into a 'Feedforward control' block (using 'Speed' and 'Throttle') and a 'Feedback control' block. The 'Feedback control' block contains three fuzzy controllers (1, 2, 3) that process 'du/dt' and 'lambda' to calculate 'alpha' and 'beta', which are then used in an 'Integral regulator' along with 'Delta K_I'. The outputs of the feedforward and feedback controllers are summed to produce 'Calculated injection', which is then sent to the 'Injector' and the 'Wankel Engine'. A feedback loop from the engine to the oxygen sensor completes the system.](01141eb99b707de5aead56f84afe3b1f_img.jpg)

Figure 5: Schematic of Wankel Engine AFR Control System. The diagram shows a control loop where 'Target lambda' is compared with 'Sensor lambda' (from an 'Oxygen sensor'). The error signal goes into a 'Feedforward control' block (using 'Speed' and 'Throttle') and a 'Feedback control' block. The 'Feedback control' block contains three fuzzy controllers (1, 2, 3) that process 'du/dt' and 'lambda' to calculate 'alpha' and 'beta', which are then used in an 'Integral regulator' along with 'Delta K\_I'. The outputs of the feedforward and feedback controllers are summed to produce 'Calculated injection', which is then sent to the 'Injector' and the 'Wankel Engine'. A feedback loop from the engine to the oxygen sensor completes the system.

**Figure 5.** Schematic of Wankel Engine AFR Control System.

The fuel injection expression of feedforward control is represented by the following formula.

$$m_{oc} = m_B \times K_{OS} (1 + K_T + K_P + K_S) + K_{BAT} \quad (6)$$

$m_B$  is the basic fuel injection quantity,  $K_{OS}$  is the overspeed condition correction factor,  $K_T$  is the intake temperature correction factor,  $K_P$  is the atmospheric pressure correction factor,  $K_S$  is the start-up condition enrichment factor,  $K_{BAT}$  is the battery voltage correction for fuel injection

In controller design, the basic domain for the input variable air-fuel ratio deviation, denoted as  $e$ , is set to  $[-0.2, 0.2]$ . The basic domain for the rate of change of air-fuel ratio deviation, denoted as  $e'$ , is set to  $[-0.03, 0.03]$ . The basic domain for the controller output compensatory fuel injection quantity, denoted as "u," is set to  $[-0.1, 0.1]$ . The fuzzy domains for all variables are defined as  $[-6, 6]$ . The fuzzy sets for  $e$ ,  $e'$ , and  $u$  are shown in **Figure 6(a)**.

![Figure 6: Membership function plots for fuzzy controller variables. (a) Membership of e, e', and u: Three plots showing triangular membership functions for input variables e (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB) and e' (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB), and output variable u (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB). (b) Membership of ΔK, α and β: Three plots showing triangular membership functions for output variable ΔK (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB), output variable α (ranging from 0 to 1 with sets VB, B, M, S), and output variable β (ranging from 0 to 1 with sets VB, B, M, S, VS).](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

(a) Membership of  $e$ ,  $e'$ , and  $u$

(b) Membership of  $\Delta K$ ,  $\alpha$  and  $\beta$

Figure 6: Membership function plots for fuzzy controller variables. (a) Membership of e, e', and u: Three plots showing triangular membership functions for input variables e (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB) and e' (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB), and output variable u (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB). (b) Membership of ΔK, α and β: Three plots showing triangular membership functions for output variable ΔK (ranging from -6 to 6 with sets NB, NM, NS, ZO, PS, PM, PB), output variable α (ranging from 0 to 1 with sets VB, B, M, S), and output variable β (ranging from 0 to 1 with sets VB, B, M, S, VS).

**Figure 6.** Membership of Fuzzy Controller.

To enable fuzzy controller 2 in **Figure 5** to achieve a variable domain, fuzzy controller 1 is employed as the domain adjustment mechanism. The variables of controller 3's input are  $e$  and  $e'$ , and the output control quantities are domain scaling factors  $\alpha$  and  $\beta$ . The fuzzy domains for both  $\alpha$  and  $\beta$  are set to  $[0, 1]$ , and the fuzzy sets for  $\Delta K$ ,  $\alpha$  and  $\beta$  are shown in **Figure 6(b)**.

### 3.2 Simulation and discussion

We analyze two common operating modes: steady-state adjustment and transient adjustment. We establish an extended average model for the rotary engine as the object and incorporate a variable-domain fuzzy integral composite control algorithm model. The air-fuel ratio control model is depicted in **Figure 7**.

![Figure 7: Model of wankel engine with variable universe fuzzy control. The diagram shows a control system for a Wankel rotary engine. It includes a 'Throttle Degree' input, a 'Fuel Injection of Feedforward MAP' block with a 2-D T(u) surface, a 'Mean Value Model of Wankel Rotary Engine' block with inputs alpha(') and in_l_w(ms) and outputs afr and speed(r/min), and a 'Fuzzy Composite Control of Variable Domain' block. The system also features a 'Feedback Control Switch' and an 'Air Fuel Ratio MAP' block. The final outputs are 'out:airout' (Air Fuel Ratio) and 'out:airout1' (Speed).](1d27fed9c01eb99f6535283f35fe3bbf_img.jpg)

Figure 7: Model of wankel engine with variable universe fuzzy control. The diagram shows a control system for a Wankel rotary engine. It includes a 'Throttle Degree' input, a 'Fuel Injection of Feedforward MAP' block with a 2-D T(u) surface, a 'Mean Value Model of Wankel Rotary Engine' block with inputs alpha(') and in\_l\_w(ms) and outputs afr and speed(r/min), and a 'Fuzzy Composite Control of Variable Domain' block. The system also features a 'Feedback Control Switch' and an 'Air Fuel Ratio MAP' block. The final outputs are 'out:airout' (Air Fuel Ratio) and 'out:airout1' (Speed).

**Figure 7.** Model of wankel engine with variable universe fuzzy control.

We set up two operating conditions: steady-state and acceleration, as shown respectively in **Figure 8**.

![Figure 8: Throttle Degrees of Steady-State and Acceleration Conditions. Two line graphs showing throttle degree over time. The left graph shows a steady-state condition with a red line increasing from 30 to 35 degrees and then decreasing back to 30 degrees over 14 seconds. The right graph shows an acceleration condition with a red line jumping between 24 and 40 degrees at 2, 6, 10, and 14 seconds.](4279c8be6ec4ed56f4b3349be98bb426_img.jpg)

Figure 8: Throttle Degrees of Steady-State and Acceleration Conditions. Two line graphs showing throttle degree over time. The left graph shows a steady-state condition with a red line increasing from 30 to 35 degrees and then decreasing back to 30 degrees over 14 seconds. The right graph shows an acceleration condition with a red line jumping between 24 and 40 degrees at 2, 6, 10, and 14 seconds.

**Figure 8.** Throttle Degrees of Steady-State and Acceleration Conditions.

![Figure 9: Air-Fuel Ratio Response of Steady-State and Acceleration Condition. Two line graphs comparing PID and Variable Universe Fuzzy Control (VUFC) methods against a target AFR. The left graph shows steady-state response with PID having a large overshoot and VUFC being more stable. The right graph shows acceleration response with PID having a significant overshoot and VUFC having a much smaller overshoot.](84e2ac543ffc4145dc85b05a48ec62e3_img.jpg)

Figure 9: Air-Fuel Ratio Response of Steady-State and Acceleration Condition. Two line graphs comparing PID and Variable Universe Fuzzy Control (VUFC) methods against a target AFR. The left graph shows steady-state response with PID having a large overshoot and VUFC being more stable. The right graph shows acceleration response with PID having a significant overshoot and VUFC having a much smaller overshoot.

**Figure 9.** Air-Fuel Ratio Response of Steady-State and Acceleration Condition.

Figure 9 illustrates the results of two AFR control methods. For the steady-state condition, significant steady-state errors of PID control occur at throttle openings of  $30^\circ$  and  $35^\circ$ . The maximum AFR error of the PID method is 0.93%. However, the variable-domain fuzzy integral composite control demonstrates higher stability, with smaller steady-state errors in the excess air coefficient response, indicating its superior ability to maintain desired operating conditions and minimize deviations from the target AFR. The maximum steady-state error is significantly reduced by 60.37% compared to PID control. The designed algorithm exhibits excellent control effectiveness, seamlessly combining both stable performance and dynamic adjustment capability, thus ensuring precise and responsive control over the system under steady-state operating conditions.

For acceleration conditions, PID control exhibits overshoot errors of around 2.23% when throttle opening undergoes a step transition. In comparison, the variable-domain fuzzy integral composite control algorithm demonstrates smaller overshoots, with maximum overshoot errors of around 1% during throttle step changes. The maximum AFR error is reduced by 35.7% compared to PID control. Additionally, the adjustment of the VUFC method is shorter, returning to steady-state in approximately 0.6 seconds. This reflects the strong dynamic adjustment capability of the composite control algorithm. The designed method shows a good ability to maintain the AFR in ideal value under different conditions.

## 4. Conclusion

This study delves into the fuzzy control strategy and integrates both feedforward and feedback strategies for controlling the AFR of WRE. By establishing an MVM of the WRE, a VUFC algorithm is devised, which incorporates both fuzzy feedback control and feedforward control mechanisms. Simulation tests of this composite control algorithm for the air-fuel ratio are conducted under various conditions encountered during the normal operation of rotary engines, including steady-state and transient scenarios. The simulation outcomes illustrate that the variable-domain fuzzy integral composite control algorithm

not only demonstrates stable performance but also exhibits dynamic adjustment capabilities. In comparison to traditional PID algorithms, this approach shows a remarkable reduction in maximum error, up to 60.37% in steady-state conditions. These findings suggest its suitability for feedback control in rotary engines, thereby laying a solid groundwork for future research on rotary engine control systems.

## References

- [1] Kutlar, O. A.; Cihan, Ö. (2022) Investigation of Parameters Affecting Rotary Engine by Means of a One Zone Thermodynamic Model. *Journal of Energy Resources Technology*, 144 (4), 042304. [[Crossref](#)].
- [2] Wang, H.; Ji, C.; Shi, C.; Ge, Y.; Meng, H.; Yang, J.; Chang, K.; Yang, Z.; Wang, S.; Wang, X. (2022) Modeling and Parametric Study of the Performance-Emissions Trade-off of a Hydrogen Wankel Rotary Engine. *Fuel*, 318, 123662. [[Crossref](#)].
- [3] Fan, B.; Wang, J.; Pan, J.; Zeng, Y.; Fang, J.; Lu, Q.; Wu, X.; Chen, W.; Qi, X. (2022) Computational Study of Hydrogen Injection Strategy on the Combustion Performance of a Direct Injection Rotary Engine Fueled with Natural Gas/Hydrogen Blends. *Fuel*, 328, 125190. [[Crossref](#)].
- [4] Wang, H.; Ji, C.; Shi, C.; Yang, J.; Wang, S.; Ge, Y.; Chang, K.; Meng, H.; Wang, X. (2023) Multi-Objective Optimization of a Hydrogen-Fueled Wankel Rotary Engine Based on Machine Learning and Genetic Algorithm. *Energy*, 263, 125961. [[Crossref](#)].
- [5] Ma, P.; Niu, Q.; Mao, H.; Jia, Q.; Liu, X., 2018. Simulation of Fuzzy Control System for Unmanned Aerial Vehicle Engine Throttle Opening. In 2018 3rd International Conference on Mechanical, Control and Computer Engineering (ICMCCE); pp 400–404. [[Crossref](#)].
- [6] Mohammed, N. F.; Song, E.; Ma, X.; Hayat, Q., 2014. D6114 Diesel Engine Speed Control: A Case between PID Controller and Fuzzy Logic Controller. In 2014 IEEE International Conference on Mechatronics and Automation; Tianjin; pp 275–279. [[Crossref](#)].
- [7] Tran, T. A.; Yan, X.; Yuan, Y., 2017. Marine Engine Rotational Speed Control Automatic System Based on Fuzzy PID Logic Controller. In 2017 4th International Conference on Transportation Information and Safety (ICTIS); Banff; pp 1099–1104. [[Crossref](#)].
- [8] Aquino, C. F. (1981) Transient A/F Control Characteristics of the 5 Liter Central Fuel Injection Engine; p 810494. [[Crossref](#)].
- [9] Hendricks, E.; Chevalier, A.; Jensen, M.; Sorenson, S. C.; Trumpy, D.; Asik, J. (1996) Modelling of the Intake Manifold Filling Dynamics; p 960037. [[Crossref](#)].
- [10] Drbal, M. (2019) Computational Model of Rotary Engine Thermodynamic Cycle. *Acta Mechanica Slov.* 23 (2), 26–29. [[Crossref](#)].