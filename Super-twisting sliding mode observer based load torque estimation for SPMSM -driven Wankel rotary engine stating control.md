

###### PAPER • **OPEN ACCESS**

# Super-twisting sliding mode observer based load torque estimation for SPMSM -driven Wankel rotary engine stating control

To cite this article: Yunfeng Guo *et al* 2025 *J. Phys.: Conf. Ser.* **3043** 012119

###### You may also like

- [The 4th International Conference on Water Resource and Environment \(WRE 2018\)](#)
- [Development of a Wire Reference Electrode for Lithium All-Solid-State Batteries with Polymer Electrolyte: FEM Simulation and Experiment](#)  
Fabian J. Simon, Leonard Blume, Matthias Hanauer *et al.*
- [Preface](#)

View the [article online](#) for updates and enhancements.

# Super-twisting sliding mode observer based load torque estimation for SPMSM -driven Wankel rotary engine starting control

Yunfeng Guo\*, Zhou Zhao, Yi Zhu and Zhenyu Liu

School of Mechanical Engineering, Beijing Institute of Technology, Beijing 100081, China

\*Corresponding author's e-mail: 3220220280@bit.edu.cn

**Abstract.** The Wankel rotary engine (WRE), known for its high power density and compact structure, encounters challenges in starting performance due to periodic load torque fluctuations. This study introduces a super-twisting sliding mode observer (STSMO) specifically designed to estimate periodic load torque disturbances, enabling real-time feedforward compensation. Simulation results validate that the proposed approach ensures smooth starting from standstill to target speed, achieving a 7.3% reduction in speed overshoot and suppressing steady-state speed fluctuations by 78.6% compared to conventional methods. These improvements significantly enhance the dynamic response accuracy, steady-state stability, and operational robustness of the WRE. The proposed solution offers a scalable and efficient method for high-performance WRE control, particularly suitable for compact, weight-sensitive applications requiring high power accuracy and reliability.

## 1. Introduction

The Wankel rotary engine (WRE) is widely recognized for its exceptional power density and compact design, offering significant benefits in applications where space is limited [1]. In contrast to conventional reciprocating engines, the WRE operates with fewer moving components, resulting in smoother performance, reduced vibration levels, and enhanced efficiency. These attributes have driven its extensive use across various fields, including automotive industries, unmanned aerial vehicles (UAVs), and power generation systems [2-4].

During the startup phase of the WRE, the internal gas pressure experiences cyclical variations due to the intake, compression, expansion, and exhaust cycles, leading to substantial periodic oscillations in the load torque. These oscillations result in pronounced speed fluctuations, reduced operational stability, and associated vibration and noise problems. Conventional speed PI controllers are inadequate for effectively mitigating such periodic load torque disturbances. To address this, a load torque observer is employed to estimate and compensate for these disturbances in real time. Common approaches for load torque observer design include full-order and reduced-order Luenberger observers [5-6], model reference adaptive systems [7], sliding mode observers [8], and Kalman filters [9]. Among these, the sliding mode observer is particularly favored for load torque estimation due to its robustness against system parameter variations and external disturbances, as well as its straightforward implementation. Nonetheless, the conventional first-order sliding mode observer is prone to chattering, which adversely affects system accuracy and dynamic performance. Consequently, the development of a super-twisting sliding mode observer for load torque estimation is crucial, as it can significantly improve the system's overall performance.

![Creative Commons Attribution 4.0 International License logo](669865256db7d33e9cb759eac2e226c8_img.jpg)

The image shows the Creative Commons Attribution 4.0 International License logo, which consists of two circular icons: one with 'cc' and another with a person symbol, followed by the text 'BY'.

Creative Commons Attribution 4.0 International License logo

Content from this work may be used under the terms of the [Creative Commons Attribution 4.0 licence](https://creativecommons.org/licenses/by/4.0/). Any further distribution of this work must maintain attribution to the author(s) and the title of the work, journal citation and DOI.

## 2. Analysis of starting resistance torque in Wankel rotary engine

Developing a resistance torque model (compression and friction components) is critical for WRE control system design. Compression torque is derived from WRE mechanism dynamics; friction torque is determined experimentally.

### 2.1. Modeling of compression torque

The study focuses on a 0.3 cc WRE developed by our team, with key specifications in Table 1 and a structural schematic in Figure 1(a).

**Table 1.** Specifications of the WRE.

| Parameter                        | Symbol | Value              |
|----------------------------------|--------|--------------------|
| Generating radius                | R      | 9 mm               |
| Eccentricity                     | e      | 1.2 mm             |
| Width of rotor                   | B      | 6 mm               |
| Shape parameter                  | K      | 7.5                |
| Cylinder profile offset          | a      | 0.5 mm             |
| Combustion chamber recess volume | $V_r$  | 14 mm <sup>3</sup> |

![Figure 1: Schematic of WRE configuration and resultant gas pressure forces on rotor. (a) shows the 3D configuration with labels: Intake port, Exhaust port, Cylinder wall, Eccentric shaft, Rotor, Working chamber 1, Working chamber 2, Working chamber 3, and Rotating direction. (b) shows a 2D cross-section of the rotor and cylinder, illustrating the resultant gas pressure forces (P_g1, P_g2, P_g3) acting on the rotor, the center of pressure (O), the resultant force (T), and the rotation angles (alpha_1, alpha_2, alpha_3).](b48d146cf1d6e0a01791f52572be6767_img.jpg)

Figure 1: Schematic of WRE configuration and resultant gas pressure forces on rotor. (a) shows the 3D configuration with labels: Intake port, Exhaust port, Cylinder wall, Eccentric shaft, Rotor, Working chamber 1, Working chamber 2, Working chamber 3, and Rotating direction. (b) shows a 2D cross-section of the rotor and cylinder, illustrating the resultant gas pressure forces (P\_g1, P\_g2, P\_g3) acting on the rotor, the center of pressure (O), the resultant force (T), and the rotation angles (alpha\_1, alpha\_2, alpha\_3).

**Figure 1.** Schematic of WRE configuration and resultant gas pressure forces on rotor.

The area  $F$  enclosed by the working surface profile of the rotor and the cylinder profile can be expressed as:

$$F = \left[ \frac{\pi}{3} + 2(K'^2 - 9)^{\frac{1}{2}} + \frac{3\sqrt{3}}{2} K' \cos \frac{2}{3} \alpha + \left( \frac{2}{9} K'^2 + 4 \right) \phi'_{\max} \right] e^2 \quad (1)$$

where  $K'$  is the actual shape parameter,  $K' = (R + a)e^{-1}$ ;  $\phi'_{\max}$  is the actual maximum swing angle,  $\phi'_{\max} = \sin^{-1}(3e(R + a)^{-1})$ ;  $\alpha$  is the eccentric shaft angle.

The single cylinder chamber volume can be expressed as:

$$V = FB + V_r = \left[ \frac{\pi}{3} + 2(K'^2 - 9)^{\frac{1}{2}} + \frac{3\sqrt{3}}{2} K' \cos \frac{2}{3} \alpha + \left( \frac{2}{9} K'^2 + 4 \right) \phi'_{\max} \right] e^2 B + V_r \quad (2)$$

In a WRE, the rotor's three working faces, cylinder profile, and end covers form three isolated chambers sealed by radial seals at the rotor apexes. Each chamber completes a full working cycle per rotor rotation. Since the eccentric shaft rotates three times faster than the rotor, each chamber requires 1080° of eccentric shaft rotation to complete one cycle. The total gas pressure on the rotor is the resultant of pressures in the three chambers, which share identical variation patterns but differ in phase distribution. For analysis, the eccentric shaft rotation angle is defined as the angle between the eccentric arm and the cylinder's major axis.  $\alpha_1$ ,  $\alpha_2$ , and  $\alpha_3$  represent the rotation angles for the three chambers, with  $\alpha_1$  as the reference.

$$\begin{cases} \alpha_2 = \alpha_1 + 4\pi \\ \alpha_3 = \alpha_1 + 2\pi \end{cases} \quad (3)$$

Based on the relationship given in Equation (3), both  $p_{g2}$  and  $p_{g3}$  can be expressed in terms of the gas pressure  $p_{g1}$  of the first chamber. The in-cylinder pressure calculation assumes:

$$p_{g1} = \begin{cases} P_{in}, & \text{gas exchange strokes} \\ P_{in} \left( \frac{V_{in}}{V_c} \right)^\gamma, & \text{compression/expansion strokes} \end{cases} \quad (4)$$

where  $\gamma$  is the adiabatic index;  $V_c$  is instantaneous volume during compression/expansion;  $P_{in}$  and  $V_{in}$  are initial pressure and volume at intake stroke termination.

The instantaneous gas force acting on the rotor for each chamber can be expressed as:

$$P_{gi} = \sqrt{3}B(R+a)p_{gi}, \quad i=1,2,3 \quad (5)$$

The resultant gas force  $P_g$  on the rotor (Figure 1(b)) is the vector sum of instantaneous forces from three  $120^\circ$  phase-shifted working surfaces. Its tangential component  $T$ , perpendicular to the eccentric arm and aligned with rotation direction, generates compression torque about the eccentric shaft:

$$\begin{cases} T_c = -\sum_{i=1}^{3} T_i \cdot e \\ T_i = -P_{gi} \sin\left(\frac{2}{3}\alpha_i\right), \quad i=1,2,3 \end{cases} \quad (6)$$

where  $T_i$  is the instantaneous tangential force of each working surface.

### 2.2. Experimental measurement of friction torque

The WRE friction torque  $T_f$ , comprising rotor end faces, radial seals, bearings, and phase gears, was experimentally determined via motoring tests using the Figure 2 platform. By maintaining stable starting speeds through motor controller adjustments, torque sensor measurements yielded  $T_f = 0.023 \text{ N} \cdot \text{m}$ . The total starting resistance torque  $T_L = T_c + T_f$  exhibits angular dependency as shown in Figure 3.

![A photograph of the experimental test platform for the WRE. The setup includes a WRE unit mounted on a base, a torque sensor attached to the WRE's shaft, a dynamometer connected to the torque sensor, and a motor driving the system. Red arrows and labels point to the 'WRE', 'Torque sensor', 'Dynamometer', and 'Motor' components.](c97b176986d994192dd844e17cd08e3a_img.jpg)

A photograph of the experimental test platform for the WRE. The setup includes a WRE unit mounted on a base, a torque sensor attached to the WRE's shaft, a dynamometer connected to the torque sensor, and a motor driving the system. Red arrows and labels point to the 'WRE', 'Torque sensor', 'Dynamometer', and 'Motor' components.

**Figure 2.** Test platform for the WRE.

![Figure 3: A line graph showing the starting resistance torque (T_L) in N·m versus the angle alpha (rad). The torque oscillates between approximately -0.05 and 0.1 N·m with a period of about 5 radians. The x-axis ranges from 0 to 20 rad, and the y-axis ranges from -0.05 to 0.1 N·m.](b15e3860e0c96ed16ce77f032da6f107_img.jpg)

Figure 3: A line graph showing the starting resistance torque (T\_L) in N·m versus the angle alpha (rad). The torque oscillates between approximately -0.05 and 0.1 N·m with a period of about 5 radians. The x-axis ranges from 0 to 20 rad, and the y-axis ranges from -0.05 to 0.1 N·m.

**Figure 3.** Starting resistance torque of the WRE.

## 3. Control strategy with STSMO-based torque observation

### 3.1. PMSM mathematical model

The surface-mounted PMSM (SPMSM) dynamics in the d-q reference frame are characterized by:

$$\begin{cases} u_d = R_s i_d + L_s \dot{i}_d - \omega_e L_s i_q \\ u_q = R_s i_q + L_s \dot{i}_q + \omega_e L_s i_d + \omega_e \psi_f \\ J \dot{\omega}_m = T_e - T_L - B \omega_m \\ T_e = 1.5 p_n \psi_f i_q \end{cases} \quad (7)$$

The SPMSM parameters include stator d-q axis voltages ( $u_d, u_q$ ) and currents ( $i_d, i_q$ ), stator resistance  $R_s$ , stator inductance  $L_s$ , permanent magnet flux linkage  $\psi_f$  and electrical angular velocity  $\omega_e$  which relates to mechanical speed  $\omega_m$  through pole pairs  $p_n$  ( $\omega_e = p_n \omega_m$ ). The electromechanical dynamics involve electromagnetic torque  $T_e$ , total inertia  $J$  combining motor and load, load torque  $T_L$ , and viscous damping coefficient  $B$ .

### 3.2. Super-twisting sliding mode observer-based torque estimation

The WRE exhibits periodic torque fluctuations during cold-start conditions, inducing significant speed oscillations. To mitigate these disturbances, a super-twisting sliding mode observer (STSMO) is developed for real-time load torque estimation. The observed torque is fed forward into the current control loop, enabling dynamic stator current compensation. The state equation of SPMSM can be derived as:

$$\begin{cases} \dot{\omega}_e = \frac{1.5 p_n^2 \psi_f i_q}{J} - \frac{p_n T_L}{J} - \frac{B \omega_e}{J} \\ \dot{T}_L = 0 \end{cases} \quad (8)$$

The state variables are defined as  $x_1 = \omega_e$  and  $x_2 = -p_n T_L / J$ . The STSMO is then constructed:

$$\begin{cases} \dot{\hat{x}}_1 = \hat{x}_2 - \frac{B}{J} \hat{x}_1 + \frac{1.5 p_n^2 \psi_f i_q}{J} - k_1 |e_1|^{\frac{1}{2}} \operatorname{sgn}(e_1) \\ \dot{\hat{x}}_2 = -k_2 \operatorname{sgn}(e_1) \end{cases} \quad (9)$$

The observation error dynamic is given by:

$$\begin{cases} \dot{e}_1 = -k_1 |e_1|^{\frac{1}{2}} \operatorname{sgn}(e_1) + e_2 + \rho_1(e, t) \\ \dot{e}_2 = -k_2 \operatorname{sgn}(e_1) + \rho_2(e, t) \end{cases} \quad (10)$$

where  $e_1 = \hat{x}_1 - x_1$ ,  $e_2 = \hat{x}_2 - x_2$ ;  $\rho_1(e, t) = -B/J$ ,  $\rho_2(e, t) = 0$  are perturbation terms. Equation (10) represents the standard form of the Super-Twisting Algorithm. As rigorously proved in [10] using Lyapunov stability theory, the closed-loop system achieves finite-time convergence if the perturbation terms satisfy the boundedness condition  $|\rho_1| \le \delta_1 |e_1|^{1/2}$ ,  $|\rho_2| \le \delta_2$  and the control gains satisfy the following relationships:

$$k_1 > 2\delta_1$$

$$k_2 > k_1 \frac{5\delta_1 k_1 + 6\delta_2 + 4(\delta_1 + \delta_2 k_1^{-1})^2}{2(k_1 - 2\delta_1)} \quad (11)$$

Figure 4 illustrates the block diagram of the load torque STSMO.

![](1d27fed9c01eb99f6535283f35fe3bbf_img.jpg)

**Figure 4.** Schematic diagram of load torque STSMO.

The observed load torque is fed forward into the torque current reference for periodic disturbance suppression, with compensation value:

$$i_q^{comp} = \frac{\hat{T}_L}{K_t} \quad (12)$$

where  $K_t = 1.5 p_n \psi_f$  represents the motor torque constant. Figure 5 presents the control block diagram of the starting system.

![Block diagram of a sensorless vector control system for a permanent magnet synchronous motor (PMSM). The diagram shows the flow from mechanical sensors (encoder) to the motor model, through current and voltage loops, and finally to the inverter and motor terminals.](68ca7669d38a3c31f5a2c3a06fa802e3_img.jpg)

The diagram illustrates a sensorless vector control system for a Permanent Magnet Synchronous Motor (PMSM). The system architecture is as follows:

- Encoder (WRE):** Provides speed feedback ( $\omega_e$ ) and rotor position ( $\theta_e$ ) to the system.
- Speed Control Loop:**
  - The speed error ( $\omega_m^* - \omega_m$ ) is fed into a PI controller.
  - The output of the PI controller is multiplied by a gain  $\frac{1}{K_s}$  to produce the torque command  $T_e^{*comp}$ .
  - The torque command  $T_e^{*comp}$  is fed into a **Load torque STSMO** block, which also receives the stator current  $i_q$  and rotor speed  $\omega_e$  as inputs.
- Current Control Loop:**
  - The stator current  $i_q^*$  is compared with the measured stator current  $i_q$  to produce the current error  $i_q^{*comp}$ .
  - The current error  $i_q^{*comp}$  is fed into a PI controller.
  - The output of the PI controller is multiplied by a gain  $\frac{1}{L_q}$  to produce the voltage command  $u_q^*$ .
  - The voltage command  $u_q^*$  is fed into an **Ipark** block, which also receives the rotor speed  $\omega_e$  and the d-axis voltage command  $u_d^*$ .
- Clark and SVPWM:**
  - The output of the **Ipark** block is fed into a **Clark** block, which also receives the rotor speed  $\omega_e$ .
  - The output of the **Clark** block is fed into an **SVPWM** (Space Vector Pulse Width Modulation) block, which also receives the rotor speed  $\omega_e$ .
- Inverter and Motor:**
  - The output of the **SVPWM** block is fed into an **Inverter** block.
  - The Inverter is connected to the PMSM terminals, which are labeled with voltage  $U_{dc}$  and current  $i_q$ .
- Encoder (WRE) Feedback:**
  - The rotor speed  $\omega_e$  is measured by the encoder and fed back to the speed loop.
  - The rotor position  $\theta_e$  is measured by the encoder and fed back to the current control loop.

Block diagram of a sensorless vector control system for a permanent magnet synchronous motor (PMSM). The diagram shows the flow from mechanical sensors (encoder) to the motor model, through current and voltage loops, and finally to the inverter and motor terminals.

**Figure 5.** Control block diagram of starting strategy with load torque STSMO.

## 4. Simulation results and analysis

The proposed control strategy is implemented in a MATLAB/Simulink environment utilizing an SPMSM with key parameters: stator resistance  $R_s = 1.13\Omega$ , stator inductance  $L_s = 0.16\text{mH}$ , pole pairs  $p_n = 1$ , flux linkage  $\psi_f = 0.0078289\text{Wb}$ , and mechanical inertia  $J = 8.01\text{e-7 kg}\cdot\text{m}^2$ . Implemented

with an ode23 variable-step solver under 10 kHz PWM switching, the test operates at 1000 r/min with a DC bus voltage of 32 V.

![Figure 6: Simulation results of STSMO performance. (a) Load torque estimation comparing Actual, SMO, and STSMO. (b) Torque observation error comparing SMO and STSMO. (c) Speed response comparing NON, SMO, and STSMO. (d) Speed tracking error comparing NON, SMO, and STSMO.](4279c8be6ec4ed56f4b3349be98bb426_img.jpg)

Figure 6 consists of four subplots (a, b, c, d) showing simulation results for STSMO performance. Subplot (a) shows Load torque (N·m) vs Time (s) for Actual, SMO, and STSMO. Subplot (b) shows Torque observation error (N·m) vs Time (s) for SMO and STSMO. Subplot (c) shows Speed (r/min) vs Time (s) for NON, SMO, and STSMO. Subplot (d) shows Speed tracking error (r/min) vs Time (s) for NON, SMO, and STSMO. All plots show a periodic disturbance starting at t=0.05s.

Figure 6: Simulation results of STSMO performance. (a) Load torque estimation comparing Actual, SMO, and STSMO. (b) Torque observation error comparing SMO and STSMO. (c) Speed response comparing NON, SMO, and STSMO. (d) Speed tracking error comparing NON, SMO, and STSMO.

**Figure 6.** Simulation results of STSMO performance.

Figure 6(a) compares the load torque estimation performance between the conventional sliding mode observer (SMO) and super-twisting sliding mode observer (STSMO), where STSMO demonstrates significantly reduced chattering ( $\pm 2 \times 10^{-4}$  N·m) compared to SMO's  $\pm 8 \times 10^{-3}$  N·m oscillations. The corresponding error analysis in Figure 6(b) validates the 97.5% amplitude suppression achieved by STSMO. These findings robustly demonstrate that the STSMO exhibits significant advantages in suppressing observation errors and enhancing measurement accuracy.

The speed response and steady-state error under different strategies are shown in Figure 6(c) and Figure 6(d). “NON” (no compensation) exhibits the largest overshoot (157.91 r/min) and steady-state fluctuation (29.63 r/min). “SMO” reduces overshoot to 145.37 r/min (7.9% reduction) and fluctuation to 12.69 r/min (57.2% reduction). “STSMO” further minimizes fluctuation to 6.34 r/min (78.6% reduction) with a similar overshoot (146.46 r/min, 7.3% reduction). Results show that STSMO with feedforward compensation effectively suppresses overshoot and steady-state fluctuations, outperforming traditional methods in enhancing speed tracking accuracy and dynamic performance.

## 5. Conclusion

The proposed control strategy effectively addresses the challenges of periodic load torque fluctuations and enhances system reliability during the starting process of the Wankel rotary engine. A super-twisting sliding mode observer is designed to accurately estimate the periodic load torque disturbances, enabling real-time feedforward compensation. This approach significantly improves load torque accuracy and electromagnetic torque stability, achieving a 7.3% reduction in speed overshoot and suppressing steady-state fluctuations by 78.6% compared to traditional methods. The strategy effectively mitigates speed ripples and vibrations caused by periodic load disturbances, ensuring robust operation under harsh conditions. Furthermore, the proposed framework demonstrates strong robustness against parameter

variations and external disturbances, making it particularly suitable for compact, weight-sensitive systems requiring high power density and operational reliability.

## References

- [1] Ozcanli M, Bas O, Akar M A, Yildizhan S and Serin H. (2018) Recent studies on hydrogen usage in Wankel SI engine. *Int. J. Hydrogen Energy*, 43: 18037–18045. [\[CrossRef\]](#)
- [2] Sadiq G A, Al-Dadah R and Mahmoud S. (2019) Development of rotary Wankel devices for hybrid automotive applications. *Energy Convers. Manag*, 202: 112159. [\[CrossRef\]](#)
- [3] Kucuk M, Surmen A and Sener R. (2022) Influence of hydrogen enrichment strategy on performance characteristics, combustion and emissions of a rotary engine for unmanned aerial vehicles (UAVs). *Energies*, 15: 9331. [\[CrossRef\]](#)
- [4] Antonelli M, Baccioli A, Francesconi M, Desideri U and Martorano L. (2014) Operating maps of a rotary engine used as an expander for micro-generation with various working fluids. *Appl. Energy*, 113: 742–750. [\[CrossRef\]](#)
- [5] Tuovinen T and Hinkkanen M. (2014) Signal-injection-assisted full-order observer with parameter adaptation for synchronous reluctance motor drives. *IEEE Trans. Ind. Appl.*, 50: 3392–3402. [\[CrossRef\]](#)
- [6] Lu W, Ji K, Dong H, Zhang J, Wang Q and Guo L. (2017) Double position servo synchronous drive system based on cross-coupling integrated feedforward control for broacher. *Chin. J. Mech. Eng.*, 30: 272–285. [\[CrossRef\]](#)
- [7] Sun K, Shi Y, Huang L, Li Y and Xiao X. (2014) A 2-D fuzzy logic based MRAS scheme for sensorless control of interior permanent magnet synchronous motor drives with cyclic fluctuating loads. In: 2014 IEEE Applied Power Electronics Conference and Exposition - APEC 2014. Fort Worth, TX, USA. pp. 2475-2481. [\[CrossRef\]](#)
- [8] Lu W, Zhang Z, Wang D, Lu K, Wu D, Ji K and Guo L. (2019) A new load torque identification sliding mode observer for permanent magnet synchronous machine drive system. *IEEE Trans. Power Electron.*, 34: 7852–7862. [\[CrossRef\]](#)
- [9] Shi T, Wang Z and Xia C. (2015) Speed measurement error suppression for PMSM control system using self-adaption Kalman observer. *IEEE Trans. Ind. Electron.*, 62: 2753–2763. [\[CrossRef\]](#)
- [10] Moreno J A and Osorio M. (2008) A Lyapunov approach to second-order sliding mode controllers and observers. In: 2008 47th IEEE Conference on Decision and Control. Cancun, Mexico. pp. 2856-2861. [\[CrossRef\]](#)