

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Results in Engineering journal cover](390120de4fe440c42fea8154fcaad334_img.jpg)

Results in Engineering journal cover

## Research paper

# Model predictive control with delay compensation for enhanced frequency regulation in hybrid virtual synchronous generators-synchronous generator microgrids

Mohammadreza Najafi, Mohammadreza Toulabi ![ORCID icon](17413706fd4997a1a4bdf85c6864eee1_img.jpg)*Department of Electrical Engineering, K. N. Toosi University of Technology, 163171419 Tehran, Iran*![Check for updates icon](1d7527f4316cfe2d342b08d1653d1592_img.jpg)

Check for updates icon

## A R T I C L E I N F O

### Keywords:

Advanced delay compensator (ADC)  
Distributed generation units  
Frequency regulation  
Model predictive control (MPC)  
Virtual synchronous generator (VSG)

## A B S T R A C T

The integration of distributed generation units, particularly inverter-based renewable energy sources (RESs) and electric vehicles (EVs), reduces grid inertia due to the lack of rotating mass, posing significant challenges to frequency stability in islanded microgrids. This paper addresses this critical issue through a novel control strategy combining virtual synchronous generator (VSG) technology with model predictive control (MPC). We present a comprehensive dynamic model of a hybrid system featuring parallel VSGs and synchronous generator (SG), and propose a centralized MPC-based VSG controller integrated with an advanced delay compensator (ADC) for enhanced frequency regulation. The proposed system is rigorously evaluated under various disturbance scenarios, including step changes in active and reactive power references. Simulation results demonstrate superior performance compared to conventional VSG control, with the MPC-based strategy achieving a 80% reduction in frequency overshoot and a 45% improvement in settling time. These findings highlight the robustness and effectiveness of the MPC-ADC approach in maintaining frequency stability in low-inertia islanded microgrids, offering a promising solution for modern power systems with high renewable penetration.

## 1. Introduction

Growing concerns over environmental impacts from fossil fuels have highlighted the importance of integrating renewable energy sources (RESs) into power systems [1,2]. To facilitate the effective integration of renewable generation units into the grid, the use of inverters is usually necessary [3]. However, as the penetration of renewable sources continues to rise, the absence of rotating mass in inverters significantly reduces the overall system's inertia, making the network vulnerable to disturbances and prone to instability [4,5]. Recent works have emphasized advanced modeling and control methods to address these challenges in inverter-dominated grids [6,7]. As an alternative solution, the concept of a virtual synchronous generator (VSG) has emerged, which mimics the inertia and damping properties of a synchronous generator on a virtual basis [8–12]. The VSG is also known by other names such as synchronous inverter [13]. Different VSG structures are described in detail in [14].

Various control mechanisms are employed for VSGs based on the characteristics of the inverter architecture [2,15,16]. These control methods range from simple approaches to more complex mathematical procedures. The commonly used control approach is the proportional-

integral-derivative (PID) controller, but it suffers from performance degradation during disruptions [17]. In [18], a hierarchical control method is presented for managing the point of common coupling demand in an active distribution network, which may incentivize investments in VSG-based demand regulation. To enhance proportional reactive power sharing among distributed generators (DGs), an adaptive virtual impedance control scheme based on fuzzy secondary controller (FSC) is suggested for grid-connected and islanded microgrids in [19]. The work in [9] proposes an AVR integrated VSG control approach for plug-in electric vehicles, aimed at providing ancillary services and enhancing voltage and frequency stability in microgrid environments. This work corroborates the increasing interest in VSG-based control as a means to support inverter-dominated systems and motivates our approach, which combines model predictive control (MPC)-based VSG coordination with delay compensation for improved regulation under dynamic disturbances. In [20], the application of a state feedback controller is considered in the VSG system to ensure robust D-stable operation in both grid-connected and islanded modes. Additionally, a novel transient equivalent motion model is introduced in [21] using the VSG control approach to investigate the transient synchronization stability of

\* Corresponding author.

E-mail addresses: [mohammadreza.najafi@email.kntu.ac.ir](mailto:mohammadreza.najafi@email.kntu.ac.ir) (M. Najafi), [toulabi@kntu.ac.ir](mailto:toulabi@kntu.ac.ir) (M. Toulabi).

### Nomenclature

|            |                                                 |               |                                                        |
|------------|-------------------------------------------------|---------------|--------------------------------------------------------|
| $\omega_0$ | Reference frequency                             | $D_{SG}$      | Damping coefficient of SG                              |
| $D_i$      | Damping coefficient of $i^{th}$ VSG             | $M_{SG}$      | Inertia constant of SG                                 |
| $M_i$      | Inertia constant of $i^{th}$ VSG                | $T_{dq0SG}$   | SG's open-circuit time constant along $dq$ axis        |
| $T_{d_i}$  | Governor delay of $i^{th}$ VSG                  | $X_{SG}$      | SG's reactance along $dq$ axis                         |
| $K_{p_i}$  | Active droop coefficient of $i^{th}$ VSG        | $X'_{SG}$     | SG's transient reactance along $dq$ axis               |
| $K_{q_i}$  | Reactive droop coefficient of $i^{th}$ VSG      | $T_{dSG}$     | SG's governor delay                                    |
| $K_i$      | Integral controller coefficient of $i^{th}$ VSG | $K_{pSG}$     | SG's active droop coefficient                          |
| $R_{v_i}$  | Virtual resistance of $i^{th}$ VSG              | $\theta_i$    | Phase angle difference between VSG and reference frame |
| $L_{v_i}$  | Virtual inductance of $i^{th}$ VSG              | $\theta_{SG}$ | Phase angle difference between SG and reference frame  |
| $K_P$      | Proportional coefficient of PI controller       | $R_i, L_i$    | Line resistance and inductance of $i^{th}$ VSG         |
| $K_I$      | Integral coefficient of PI controller           | $R_x, L_x$    | SG's line resistance and inductance                    |
| $R_{f_i}$  | Filter's resistance of $i^{th}$ VSG             | $R_L$         | Load's resistance                                      |
| $L_{f_i}$  | Filter's inductance of $i^{th}$ VSG             | $L_L$         | Load's inductance                                      |
| $C_{f_i}$  | Filter's capacitance of $i^{th}$ VSG            | $\tau_d$      | Amount of delay                                        |
| $N_p$      | Prediction horizon                              | $N_c$         | Control horizon                                        |

grid-forming converters. Furthermore, the impedance model of the VSC-VSG system is developed in [22] to establish a VSG-based control system as a viable method for integrating voltage source converters (VSCs) into weak AC grids. The work in [23] studies the dynamic stability of the multiple grid-connected VSC controlled by VSG and proposes an additional power system stabilizer (PSS) method to improve the damping characteristics of multi-VSG grid-connected systems.

The MPC is an online optimization-based control strategy that aims to determine the optimal control actions for a system by predicting its future behavior [24,25]. Unlike traditional feedback control approaches, MPC is capable of handling strict nonlinear constraints and providing effective control solutions for complex systems and multi-input multi-output nonlinear dynamic systems. In [26], a novel approach combining fuzzy control with an MPC-based VSG control scheme is proposed to address frequency deviations in an islanded microgrid. To enhance the fault ride-through capability and current limiting capacity of the VSG, [27] introduces a finite-set MPC method based on VSG control, which effectively suppresses unbalanced and non-sinusoidal currents in the VSG system. Similarly, [28] investigates an MPC-based VSG control technique for an energy storage system in an islanded microgrid, with a focus on predicting the optimal output active power of the VSG. In the context of an islanded AC microgrid, [29] proposes an MPC-based virtual inertia approach to optimize traditional primary control. However, it should be noted that the issue of communication delay in MPC command transmission can lead to system overshoot and instability. The type of communication link, distance, and communication loads are crucial factors contributing to the delay [30]. Unfortunately, the mentioned research does not take into account the MPC communication delay, which may result in system instability.

In islanded microgrids, incorporating a small synchronous generator (SG) like a diesel or gas generator alongside DGs powered by RESs is a common practice. Consequently, there has been a growing inclination towards the parallel operation of VSGs and SGs within microgrids. As a result, it is essential to explore inverter-based DG control methods for effectively managing such systems.

In recent years, there has been a notable increase in research focusing on the integration of parallel SG-VSG systems [31]. In [32], a small signal model was developed for a VSG unit, considering the governor characteristics, to obtain a mathematical model for a two-zone system comprising both VSG and SG components. The study investigated the impact of the VSG on the low-frequency oscillation damping properties of the transmission power grid, comparing it with a SG. Transient energy analysis was employed in [33] to examine the damping effect of the parallel VSG-SG system. However, it is important to note that the studies mentioned above primarily focused on experimental modeling of the paralleled SG-VSGs system, lacking a comprehensive theoretical

model. In [34], the transient stability of two islanded systems was investigated, including a paralleled SG-VSGs configuration and two parallel VSGs supplying a resistive load. Nonetheless, the examination did not address the appropriate control mechanism for adjusting the system's frequency. Given the increasing utilization of VSGs in microgrids, it is imperative to conduct further researches into modeling systems comprised of multiple VSGs and an SG. In this regards, this study makes several key contributions to the field of islanded microgrid control. First, we develop a comprehensive full state-space model of a microgrid comprising multiple VSGs operating in parallel with a SG, explicitly incorporating the dynamics of filters, grid lines, and loads – addressing critical gaps in prior researches. Second, to enhance frequency stability and mitigate power fluctuations, we propose a centralized MPC-based VSG controller that coordinates the frequency response of both VSGs and SG. Third, we systematically analyze the impact of VSG parameters (e.g., inertia constant and damping coefficient) and communication delay durations on system dynamics, providing insights for parameter optimization. Finally, we integrate an advanced delay compensator (ADC) into the MPC framework to mitigate communication latency effects. Collectively, these contributions offer a robust, scalable solution for improving frequency regulation in modern islanded microgrids with high penetration of inverter-based resources.

## 2. Cooperative operation of VSGs and SG

### 2.1. State-space representation of SG behavior

The dynamic model of the SG is derived from a fifth-order dynamic model. The dynamic equations governing the SG are as follows [35,36]:

$$\begin{cases} \dot{\delta}_{SG} = \omega_0 \omega_{SG}, \\ \dot{\omega}_{SG} = -\frac{D_{SG}}{M_{SG}}(\omega_{SG} - \omega_0) + \frac{1}{M_{SG}}(P_m - P_e), \\ \dot{E}_{SG_d} = \frac{1}{T_{d0SG}}(-E_{SG_d} + (X_{SG_q} - X'_{SG_q})i_{SG_q}), \\ \dot{E}_{SG_q} = \frac{1}{T_{d0SG}}(-E_{SG_q} + E_f + (X_{SG_d} - X'_{SG_d})i_{SG_d}), \\ \dot{P}_m = \frac{1}{T_{dSG}}(-K_{SG}(\omega_{SG} - \omega_0) - P_m + P_{0SG}). \end{cases} \quad (1)$$

Note that the expressions for the terminal voltage of the synchronous generator along the  $d$  and  $q$  axes are given by:

$$\begin{cases} V_{SG_d} = E_{SG_d} - X'_{SG_q} i_q, \\ V_{SG_q} = E_{SG_q} - X'_{SG_d} i_d. \end{cases} \quad (2)$$

Besides, the output power of the synchronous generator is:

![Figure 1: The conceptual structure of VSG. The diagram shows a central 'Virtual Synchronous Generator' block. To its left, 'Wind Farms' (wind turbine icon) and 'PV Farms' (solar panel icon) feed into a 'DC Source/ Energy Storage' block (represented by a battery symbol). This DC source feeds into an 'Inverter' block (represented by a circuit symbol). The inverter output goes through an 'RLC Filter' block (represented by a circuit with R, L, and C components) before connecting to the 'Utility Grid' (represented by a power line tower icon) and the 'Microgrid' (represented by a sine wave icon). The 'VSG Control' block is positioned below the inverter, with arrows indicating control signals from the DC source, inverter, and RLC filter back to the VSG control unit.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

Figure 1: The conceptual structure of VSG. The diagram shows a central 'Virtual Synchronous Generator' block. To its left, 'Wind Farms' (wind turbine icon) and 'PV Farms' (solar panel icon) feed into a 'DC Source/ Energy Storage' block (represented by a battery symbol). This DC source feeds into an 'Inverter' block (represented by a circuit symbol). The inverter output goes through an 'RLC Filter' block (represented by a circuit with R, L, and C components) before connecting to the 'Utility Grid' (represented by a power line tower icon) and the 'Microgrid' (represented by a sine wave icon). The 'VSG Control' block is positioned below the inverter, with arrows indicating control signals from the DC source, inverter, and RLC filter back to the VSG control unit.

#### Virtual Synchronous Generator

Fig. 1. The conceptual structure of VSG.

$$P_e = V_{SG_d} i_{SG_d} + V_{SG_q} i_{SG_q}. \quad (3)$$

By utilizing the equations of the SG model, i.e., equations (1) to (3), it is possible to establish the nonlinear model of the synchronous generator.

### 2.2. Dynamic modeling and analysis of VSGs

The conceptual structure of VSG is depicted in Fig. 1. As shown, the control strategy plays a central role in the VSG, serving as the interface between various storage units, generation units, and the utility grid. This control strategy is depicted in Fig. 2. The selection of controller parameters follows practical engineering guidelines. As explained later, the inertia constant  $H$  is chosen to provide adequate virtual inertia, thereby limiting the rate of frequency change following disturbances. The damping coefficient  $D$  is set to reduce oscillations and overshoot in the frequency response, enhancing transient stability. The droop gain establishes the steady-state relationship between power and frequency, ensuring appropriate load sharing. In this study, these parameters are initially selected based on representative values reported in the literature and subsequently fine-tuned through simulation to achieve an optimal balance between dynamic performance and system stability.

The VSG control algorithm relies on a current control-type inverter. Importantly, the swing equation, as described in [20], is a fundamental component of the VSG. As shown in Fig. 2 (governor model), the swing equation for  $i^{th}$  VSG can be expressed as follows:

$$\dot{\omega}_{VSG_i} = -\frac{D_i}{M_i}(\omega_{VSG_i} - \omega_0) + \frac{1}{M_i}(P_{in_i} - P_{out_i}). \quad (4)$$

It is worth noting that the governor model generates the input power for the VSG through the utilization of the frequency-active power droop characteristic. The dynamic equation governing the input power of  $i^{th}$  VSG is as follows:

$$\dot{P}_{in_i} = \frac{1}{T_{d_i}}(-K_{p_i}(\omega_{VSG_i} - \omega_0) - P_{in_i} + P_{0_i}). \quad (5)$$

The excitation controller emulates the behavior of an automatic voltage regulator and captures the characteristics of the field windings in a SG. The regulation of reactive power in the VSG is accomplished through the utilization of a voltage-reactive power droop characteristic and an integral controller. Referring to Fig. 2 (excitation controller), the state equation for  $i^{th}$  VSG can be represented as follows:

$$\dot{E}_i = \frac{-K_{q_i}}{K_i}(E_i - E_{0_i}) + \frac{1}{K_i}(Q_{0_i} - Q_{out_i}). \quad (6)$$

By aligning the  $q$  axis parallel to  $E_i$ , the electromotive force of  $i^{th}$  VSG can be expressed along the  $d$  and  $q$  axes as follows:

$$\begin{cases} E_{i_d} = 0, \\ E_{i_q} = E_i. \end{cases} \quad (7)$$

In addition, the equations governing the output current of the virtual impedance can be derived by applying (7) together with the output voltage of  $i^{th}$  VSG, as illustrated in Fig. 2 (virtual impedance model), as follows:

$$\begin{cases} i_{v_{i_d}} = \frac{E_{i_d} - V_{i_d} - R_{v_i} i_{v_{i_d}} + \omega_0 L_{v_i} i_{v_{i_q}}}{L_{v_i}}, \\ i_{v_{i_q}} = \frac{E_{i_q} - V_{i_q} - R_{v_i} i_{v_{i_q}} - \omega_0 L_{v_i} i_{v_{i_d}}}{L_{v_i}}. \end{cases} \quad (8)$$

The state equations describing the output voltage of the inner loop control, as depicted in Fig. 2, can be given as follows:

$$\begin{cases} \dot{V}_{v_{i_d}} = K_{I_{i_1}}(i_{v_{i_d}} - i_{o_{i_d}}), \\ \dot{V}_{v_{i_q}} = K_{I_{i_2}}(i_{v_{i_q}} - i_{o_{i_q}}), \end{cases} \quad (9)$$

$$\begin{cases} V_{o_{i_d}} = V_{v_{i_d}} + K_{P_{i_1}}(i_{v_{i_d}} - i_{o_{i_d}}) - \omega_0 L_{f_i} i_{o_{i_q}}, \\ V_{o_{i_q}} = V_{v_{i_q}} + K_{P_{i_2}}(i_{v_{i_q}} - i_{o_{i_q}}) + \omega_0 L_{f_i} i_{o_{i_d}}. \end{cases} \quad (10)$$

According to the output voltage and current of VSG, the active and reactive powers can be obtained as follows:

$$\begin{cases} P_{out_i} = V_{o_{i_d}} i_{o_{i_d}} + V_{o_{i_q}} i_{o_{i_q}}, \\ Q_{out_i} = V_{o_{i_d}} i_{o_{i_q}} - V_{o_{i_q}} i_{o_{i_d}}. \end{cases} \quad (11)$$

It is important to note that the dynamics of the inverter are faster compared to the oscillation equation in low-frequency studies and ignoring these dynamics does not impact the accuracy of the model. Therefore, the proposed model does not take these dynamics into consideration.

### 2.3. Unified dynamic model of VSGs-SG system

The system, composed of  $n$  VSGs, a SG, filters, and an RL load, is represented by the equivalent circuit shown in Fig. 3. Each VSG is connected to node  $i$  through an RLC filter, which consists of a series RL branch and a shunt capacitor. The dynamic equations governing the output current of  $i^{th}$  VSG can be expressed as follows:

![Figure 2: VSG control strategy block diagram. The diagram shows three main control loops: Governor Model, Swing Equation, and Excitation Controller. The Governor Model and Swing Equation are connected to the VSG control block, which outputs the virtual impedance model (eθ) and inner loop control (dq). The Excitation Controller also outputs to the VSG control block. The VSG control block then feeds into the PWM block, which drives the abc phase currents.](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

Figure 2: VSG control strategy block diagram. The diagram shows three main control loops: Governor Model, Swing Equation, and Excitation Controller. The Governor Model and Swing Equation are connected to the VSG control block, which outputs the virtual impedance model (eθ) and inner loop control (dq). The Excitation Controller also outputs to the VSG control block. The VSG control block then feeds into the PWM block, which drives the abc phase currents.

Fig. 2. VSG control strategy.

![Figure 3: Equivalent circuit of VSGs-SG system. The circuit shows multiple VSGs (VSG1 to VSGn) connected in parallel to a synchronous generator (SG). Each VSG is represented by a voltage source (Voi) in series with a resistor (Rfi) and an inductor (Lfi), followed by a capacitor (Cfi). The SG is represented by a voltage source (VSG) in series with a resistor (Rs) and an inductor (Ls). The common node is labeled V1, and the output node is labeled Vn.](d62e2e2281009c16f4ee61660e716cd9_img.jpg)

Figure 3: Equivalent circuit of VSGs-SG system. The circuit shows multiple VSGs (VSG1 to VSGn) connected in parallel to a synchronous generator (SG). Each VSG is represented by a voltage source (Voi) in series with a resistor (Rfi) and an inductor (Lfi), followed by a capacitor (Cfi). The SG is represented by a voltage source (VSG) in series with a resistor (Rs) and an inductor (Ls). The common node is labeled V1, and the output node is labeled Vn.

Fig. 3. Equivalent circuit of VSGs-SG system.

$$\begin{cases} i_{o_{id}} = \frac{1}{L_{fi}}(V_{o_{id}} - V_{i_d} - R_{fi}i_{o_{id}} + \omega_0 L_{fi}i_{o_{iq}}), \\ i_{o_{iq}} = \frac{1}{L_{fi}}(V_{o_{iq}} - V_{i_q} - R_{fi}i_{o_{iq}} - \omega_0 L_{fi}i_{o_{id}}). \end{cases} \quad (12)$$

Furthermore, the voltage of node  $i$  along the  $d$  and  $q$  axes can be described as:

$$\begin{cases} \dot{V}_{i_d} = \frac{1}{C_{fi}}(i_{o_{id}} - i_{i_d} + \omega_0 C_{fi} V_{i_d}), \\ \dot{V}_{i_q} = \frac{1}{C_{fi}}(i_{o_{iq}} - i_{i_q} - \omega_0 C_{fi} V_{i_d}). \end{cases} \quad (13)$$

To derive the system model, it is necessary to ensure that the voltages and currents of both VSGs and SG are in a common reference frame. This can be achieved by employing transformation equations defined as follows:

$$\begin{bmatrix} F_D \\ F_Q \end{bmatrix} = \begin{bmatrix} \cos \theta & -\sin \theta \\ \sin \theta & \cos \theta \end{bmatrix} \begin{bmatrix} f_d \\ f_q \end{bmatrix}, \quad (14a)$$

$$\begin{bmatrix} F_d \\ F_q \end{bmatrix} = \begin{bmatrix} \cos \theta & \sin \theta \\ -\sin \theta & \cos \theta \end{bmatrix} \begin{bmatrix} f_D \\ f_Q \end{bmatrix}. \quad (14b)$$

As shown in the Fig. 4,  $\theta_i$  and  $\theta_{SG}$  and their associated derivatives are calculated as follows:

$$\begin{cases} \theta_i = \delta_{VSG_i} - \delta_{VSG_1}, \\ \dot{\theta}_i = \dot{\delta}_i - \dot{\delta}_1 = \omega_0(\omega_i - \omega_{VSG_1}). \end{cases} \quad (15)$$

$$\begin{cases} \theta_{SG} = \delta_{SG} - \delta_{VSG_1}, \\ \dot{\theta}_{SG} = \dot{\delta}_{SG} - \dot{\delta}_1 = \omega_0(\omega_{SG} - \omega_{VSG_1}). \end{cases} \quad (16)$$

![Figure 4: Relationship between the reference frames of VSGs and SG. The diagram shows a common origin with multiple reference frames. VSG1 is the reference frame (d1, q1). Other VSGs (VSG2 to VSGn) and the SG have their own frames (di, qi) and (dSG, qSG). The angles between these frames are indicated by dashed lines and labels: θi, θSG, ωi, ωSG, ωVSG1, ωVSG2, ωVSGn, and ωSG.](476d6fb9044a040636d52619c7c43b1a_img.jpg)

Figure 4: Relationship between the reference frames of VSGs and SG. The diagram shows a common origin with multiple reference frames. VSG1 is the reference frame (d1, q1). Other VSGs (VSG2 to VSGn) and the SG have their own frames (di, qi) and (dSG, qSG). The angles between these frames are indicated by dashed lines and labels: θi, θSG, ωi, ωSG, ωVSG1, ωVSG2, ωVSGn, and ωSG.

Fig. 4. Relationship between the reference frames of VSGs and SG.

The reference frame of  $d_{VSG_1}$  is regarded as the common reference frame of the system. By utilizing the transformation matrix (14), the voltages and currents of  $i^{th}$  VSG in this reference frame can be obtained as illustrated:

$$\begin{cases} V_{i_D} = V_{i_d} \cos \theta_i - V_{i_q} \sin \theta_i, \\ V_{i_Q} = V_{i_q} \sin \theta_i + V_{i_d} \cos \theta_i. \end{cases} \quad (17)$$

$$\begin{cases} I_{i_D} = i_{i_d} \cos \theta_i - i_{i_q} \sin \theta_i, \\ I_{i_Q} = i_{i_q} \sin \theta_i + i_{i_d} \cos \theta_i. \end{cases} \quad (18)$$

Likewise, the voltages and currents of the SG in the reference frame are represented by:

$$\begin{cases} V_{SG_D} = V_{SG_d} \cos \theta_{SG} - V_{SG_q} \sin \theta_{SG}, \\ V_{SG_Q} = V_{SG_d} \sin \theta_{SG} + V_{SG_q} \cos \theta_{SG}. \end{cases} \quad (19)$$

$$\begin{cases} I_{SG_D} = i_{SG_d} \cos \theta_{SG} - i_{SG_q} \sin \theta_{SG}, \\ I_{SG_Q} = i_{SG_d} \sin \theta_{SG} + i_{SG_q} \cos \theta_{SG}. \end{cases} \quad (20)$$

The state equations governing the line current for  $i^{th}$  line connected between nodes  $i$  and  $b$  are as follows:

$$\begin{cases} \dot{i}_{i_D} = \frac{1}{L_i}(V_{i_D} - V_{b_D} - R_i I_{i_D} + \omega_0 L_i I_{i_Q}), \\ \dot{i}_{i_Q} = \frac{1}{L_i}(V_{i_Q} - V_{b_Q} - R_i I_{i_Q} - \omega_0 L_i I_{i_D}). \end{cases} \quad (21)$$

Similarly, the state equations governing the line current between the SG and node  $i$  can be expressed as follows:

$$\begin{cases} \dot{i}_{SG_D} = \frac{1}{L_x}(V_{SG_D} - V_{b_D} - R_x I_{SG_D} + \omega_0 L_x I_{SG_Q}), \\ \dot{i}_{SG_Q} = \frac{1}{L_x}(V_{SG_Q} - V_{b_Q} - R_x I_{SG_Q} - \omega_0 L_x I_{SG_D}). \end{cases} \quad (22)$$

Moreover, the equations that dictate the state of the RL load at node  $b$  are as follows:

$$\begin{cases} \dot{i}_{L_D} = \frac{1}{L_L}(V_{b_D} - R_L I_{L_D} + \omega_0 L_L I_{L_Q}), \\ \dot{i}_{L_Q} = \frac{1}{L_L}(V_{b_Q} - R_L I_{L_Q} - \omega_0 L_L I_{L_D}). \end{cases} \quad (23)$$

By applying Kirchhoff's current law (KCL) equations and focusing on node  $b$  in Fig. 3, the following equations are derived:

$$\begin{cases} I_{L_D} = \sum_{i=1}^{n} I_{i_D} + I_{SG_D}, \\ I_{L_Q} = \sum_{i=1}^{n} I_{i_Q} + I_{SG_Q}. \end{cases} \quad (24)$$

By taking the derivative with respect to time of (24), the following equations are obtained:

$$\begin{cases} \dot{I}_{L_D} = \sum_{i=1}^{n} \dot{I}_{i_D} + \dot{I}_{SG_D}, \\ \dot{I}_{L_Q} = \sum_{i=1}^{n} \dot{I}_{i_Q} + \dot{I}_{SG_Q}. \end{cases} \quad (25)$$

By substituting (24) and (25) into (23), these equations can be rewritten as below:

$$\begin{cases} \sum_{i=1}^{n} \dot{I}_{i_D} + \dot{I}_{SG_D} = \frac{1}{L_L}(V_{b_D} - R_L(I_{i_D} + I_{SG_D}) + \omega_0 L_L(I_{i_Q} + I_{SG_Q})), \\ \sum_{i=1}^{n} \dot{I}_{i_Q} + \dot{I}_{SG_Q} = \frac{1}{L_L}(V_{b_Q} - R_L(I_{i_Q} + I_{SG_Q}) - \omega_0 L_L(I_{i_D} + I_{SG_D})). \end{cases} \quad (26)$$

By substituting (21) and (22) into (26), the following system of equations are derived:

$$\begin{cases} (V_{b_D} - R_L(\sum_{i=1}^{n} I_{i_D} + I_{SG_D}) + \omega_0 L_L(\sum_{i=1}^{n} I_{i_Q} + I_{SG_Q})) \\ - \sum_{i=1}^{n} (\frac{1}{L_i}(V_{i_D} - V_{b_D} - R_i I_{i_D} + \omega_0 L_i I_{i_Q})) \\ - \frac{1}{L_x}(V_{SG_D} - V_{b_D} - R_x I_{SG_D} + \omega_0 L_x I_{SG_Q}) = 0, \\ (V_{b_Q} - R_L(\sum_{i=1}^{n} I_{i_Q} + I_{SG_Q}) - \omega_0 L_L(\sum_{i=1}^{n} I_{i_D} + I_{SG_D})) \\ - \sum_{i=1}^{n} (\frac{1}{L_i}(V_{i_Q} - V_{b_Q} - R_i I_{i_Q} - \omega_0 L_i I_{i_D})) \\ + \frac{1}{L_x}(V_{SG_Q} - V_{b_Q} - R_x I_{SG_Q} - \omega_0 L_x I_{SG_D}) = 0. \end{cases} \quad (27)$$

The voltage at bus  $b$  can be determined by solving the aforementioned system of equations. Subsequently, the state equations for the currents of the VSGs and the SG can be rewritten in terms of the voltage at bus  $b$ .

It should be noted that by combining the aforementioned equations, a nonlinear state-space model of the VSGs-SG system can be developed. From this nonlinear model, a corresponding linearized state-space model can be constructed as expressed in the following:

$$\begin{cases} \Delta \dot{X}(t) = A \Delta X(t) + B \Delta U(t), \\ \Delta Y(t) = I \Delta X(t), \end{cases} \quad (28)$$

where

$$\begin{cases} \Delta X = \begin{bmatrix} \sum_{i=1}^{n} \Delta \delta_i, \sum_{i=1}^{n} \Delta \omega_{V, SG_i}, \sum_{i=1}^{n} \Delta E_{i_i}, \sum_{i=1}^{n} \Delta V_{v_{i_d}}, \sum_{i=1}^{n} \Delta V_{v_{i_q}}, \\ \sum_{i=1}^{n} \Delta i_{v_{i_d}}, \sum_{i=1}^{n} \Delta i_{v_{i_q}}, \sum_{i=1}^{n} \Delta i_{o_{i_d}, \sum_{i=1}^{n} \Delta i_{o_{i_q}}, \sum_{i=1}^{n} \Delta V_{i_d}, \\ \sum_{i=1}^{n} \Delta V_{i_q}, \sum_{i=1}^{n} \Delta i_{i_d}, \sum_{i=1}^{n} \Delta i_{i_q}, \sum_{i=1}^{n} \Delta P_{in_i}, \sum_{i=1}^{n} \Delta \delta_{SG_i}, \\ \Delta \omega_{SG}, \Delta E_{SG_d}, \Delta E_{SG_q}, \Delta i_{SG_d}, \Delta i_{SG_q}, \Delta P_m \end{bmatrix}^T, \\ \Delta U = \begin{bmatrix} \sum_{i=1}^{n} \Delta P_{o_i}, \sum_{i=1}^{n} \Delta Q_{o_i}, \Delta P_{o_{SG}} \end{bmatrix}^T. \end{cases} \quad (29)$$

The state-space representation defined by equation (28) depicts the parallel operation of  $n$  VSGs and a SG linearized around the operating point. Note that in (28),  $A$  represents the state matrix, which describes the dynamic behavior of the VSG-SG system, including the effects of filters, grid lines, and loads;  $B$  is the input matrix, mapping control inputs to state changes; and  $I$  is the identity matrix, ensuring all state variables are directly observable as outputs. The matrices  $A$  and  $B$  are fully derived from the dynamic equations presented earlier in the manuscript. However, due to the generalized formulation for a system with  $n$  parallel VSGs and one SG, these matrices are high-dimensional and sparse, making their complete symbolic form impractical to include. Nevertheless, the provided modeling approach and equations allow readers to reconstruct them for any specific configuration, ensuring reproducibility.

## 3. Optimal control-based VSG design via MPC

The MPC is a well-established approach used for achieving optimal control of systems with constraints. This controller selects the best input from a set of possible input sequences within a future horizon or based on specific criteria. The overall strategy of MPC is illustrated in Fig. 5. In each step, the MPC determines the optimal control sequence that minimizes the deviation between the system states and their desired reference values while also minimizing control effort. This optimal control sequence is applied to the system using a receding horizon concept. Subsequently, at each subsequent sampling time, the process is repeated

![Fig. 5. A graphical layout of the MPC concept. The diagram shows a timeline with 'Past' and 'Future' directions. It includes 'Past Output Measurement y(t)' (red dots), 'Past Input Actions u(t)' (red step function), 'Output Setpoint' (green dashed line), 'Predicted Output y(t+k|t)' (blue dots), and 'Future Input Actions u(t+k)' (blue step function). The timeline is marked with time indices t-1, t, t+1, t+Nc, and t+Np. The 'Control Horizon' is the interval from t to t+Nc, and the 'Prediction Horizon' is from t to t+Np.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Fig. 5. A graphical layout of the MPC concept. The diagram shows a timeline with 'Past' and 'Future' directions. It includes 'Past Output Measurement y(t)' (red dots), 'Past Input Actions u(t)' (red step function), 'Output Setpoint' (green dashed line), 'Predicted Output y(t+k|t)' (blue dots), and 'Future Input Actions u(t+k)' (blue step function). The timeline is marked with time indices t-1, t, t+1, t+Nc, and t+Np. The 'Control Horizon' is the interval from t to t+Nc, and the 'Prediction Horizon' is from t to t+Np.

Fig. 5. A graphical layout of the MPC concept.

![Fig. 6. The basic structure of the MPC. The diagram shows a block diagram where a 'Set Point' is compared with 'Predicted Outputs' in a summing junction to produce the 'Predicted Error'. This error is fed into an 'Optimizer' block. The 'Optimizer' also receives 'Constraints' and 'Past Inputs and Outputs'. The 'Optimizer' outputs 'Future Input Actions' which are fed back into the system. The 'System Model' block takes 'Past Inputs and Outputs' and produces 'Predicted Outputs'.](f6d72d7c790e7f585532140f3971639a_img.jpg)

Fig. 6. The basic structure of the MPC. The diagram shows a block diagram where a 'Set Point' is compared with 'Predicted Outputs' in a summing junction to produce the 'Predicted Error'. This error is fed into an 'Optimizer' block. The 'Optimizer' also receives 'Constraints' and 'Past Inputs and Outputs'. The 'Optimizer' outputs 'Future Input Actions' which are fed back into the system. The 'System Model' block takes 'Past Inputs and Outputs' and produces 'Predicted Outputs'.

Fig. 6. The basic structure of the MPC.

with new measurements becoming available. The MPC utilizes a predictive control model, as shown in Fig. 6, which solves a constrained dynamic optimal control problem through iterative online optimization. This approach avoids the need for complex offline computation of the control law. The fundamental structure of MPC employs a state-space model to forecast future system outputs based on past and current values, along with optimal control actions in the future. These control actions are determined by the optimizer, considering the cost function and constraints.

Based on equation (28), the linear equations that describe the state-space representation of the system can be described as follows:

$$x(t+1) = Ax(t) + Bu(t), \quad (30)$$

$$y(t) = Cx(t).$$

To express the model in incremental form and achieve offset-free control, we define the change in control input as  $\Delta u(t) = u(t) - u(t-1)$ , following the approach in [37]. Using this definition, the model can be reformulated as:

$$\begin{bmatrix} x(t+1) \\ u(t) \end{bmatrix} = \begin{bmatrix} A & B \\ 0 & I \end{bmatrix} \begin{bmatrix} x(t) \\ u(t-1) \end{bmatrix} + \begin{bmatrix} B \\ I \end{bmatrix} \Delta u(t), \quad (31)$$

$$y(t) = [C \quad 0] \begin{bmatrix} x(t) \\ u(t-1) \end{bmatrix}.$$

By introducing the new state vector  $\tilde{x}(t) = [x(t) \quad u(t-1)]^T$ , the incremental model can be defined as follows:

$$\tilde{x}(t+1) = M\tilde{x}(t) + N\Delta u(t), \quad (32)$$

$$y(t) = Q\tilde{x}(t),$$

where the values of  $M$ ,  $N$ , and  $Q$  can be determined by comparing equation (30) and equation (32) as functions of  $A$ ,  $B$ , and  $C$ . Once the state-space model is obtained, the cost function is utilized to compute the control law and minimize the system. In the case of multiple-input multiple-output (MIMO) processes, where both the inputs and outputs are vectors, the costs are calculated using quadratic functions. Typically, positive definite weight matrices  $R$  and  $P$  are employed, with  $R$  usually being a diagonal matrix. The cost function can be expressed as follows:

$$J(N_p, N_c) = \sum_{j=1}^{N_p} \|\hat{y}(t+j|t) - \omega(t+j)\|_R^2 + \sum_{j=1}^{N_c} \|\Delta u(t+j-1)\|_P^2, \quad (33)$$

where  $\hat{y}$  represents the prediction of the output,  $\omega(t)$  denotes the reference signal,  $N_p$  represents the prediction horizon,  $N_c < N_p$  indicates the control horizon, and  $\|\cdot\|_R^2$  represents the squared 2-norm. The output predictions utilized in the objective function (33) can be calculated using either equation (30) or equation (32) if an incremental model is employed. The predictions over the horizon are given by:

$$y = \begin{bmatrix} \hat{y}(t+1|t) \\ \hat{y}(t+2|t) \\ \vdots \\ \hat{y}(t+N_p|t) \end{bmatrix} = \begin{bmatrix} QMx(t) + QN\Delta u(t) \\ QM^2x(t) + \sum_{i=0}^{1} QM^{1-i}N\Delta u(t+i) \\ \vdots \\ QM^{N_p}x(t) + \sum_{i=0}^{N_p-1} QM^{N_p-1-i}N\Delta u(t+i) \end{bmatrix}, \quad (34)$$

where the boldface lowercase letters represent vectors composed of elements along the horizon, while the boldface uppercase letters indicate matrices composed of other matrices and vectors. It should be noted that if the state vector  $x(t)$  is not directly accessible, it needs to be estimated using an observer, as mentioned in [37].

## 4. Systematic design of ADC

In practical microgrid implementations, communication delays typically arise from the time required to transmit measured signals (such as active power, reactive power, and frequency) from distributed VSG units and sensors to the central controller as well as the time taken to send control commands back to the VSGs. Such delays can be caused by network latency, sensor sampling intervals, or limited communication bandwidth.

The introduction of MPC can result in communication delays, which may lead to overshoots and instability when transmitting and receiving commands to the model. The extent of the delay is influenced by factors such as the type of communication link, distance, and loads involved. Various types of communication links, including telephone lines, fiber optic links, power line carriers, and microwave networks, can be utilized. To compensate for time-varying communication delays, a weighted combination of multiple compensators is employed. The equation governing the communication delay is determined as follows:

$$D(s) = e^{\tau_d s} = (e^{-\frac{\tau_d}{n} s})^n = \left( \frac{(e^{-\frac{\tau_d}{2n} s})^n}{(e^{\frac{\tau_d}{2n} s})^n} \right) \simeq \frac{(1 - \frac{\tau_d s}{2n})^n}{(1 + \frac{\tau_d s}{2n})^n}, \quad (35)$$

where  $\tau_d$  is the amount of delay. The  $n^{th}$ -order ADC is utilized to counteract the mentioned delay, and its acquisition is described as follows:

![Fig. 7. Basic schematic of ADC block diagram. The diagram shows an MPC block sending an 'Output Command' to a block labeled 'e^{-s\tau_d}' representing 'Communication Delay'. The output of this delay block is the 'Delayed Signal'. This signal is fed into a summing junction. A 'Compensating Signal' is also fed into this junction from an 'Advanced Delay Compensator' block. The output of the summing junction is the 'Input Signal' to a VSG block. The 'Advanced Delay Compensator' block contains a series of weighting factors W_1, W_2, ..., W_m, each multiplied by a transfer function block (1 + sT_i/2n)^{2n}. These are summed together. A separate block (1 + sT_c)^{2n} is also part of the compensator structure.](a738993919a50143787084ee7ce6e2f2_img.jpg)

Fig. 7. Basic schematic of ADC block diagram. The diagram shows an MPC block sending an 'Output Command' to a block labeled 'e^{-s\tau\_d}' representing 'Communication Delay'. The output of this delay block is the 'Delayed Signal'. This signal is fed into a summing junction. A 'Compensating Signal' is also fed into this junction from an 'Advanced Delay Compensator' block. The output of the summing junction is the 'Input Signal' to a VSG block. The 'Advanced Delay Compensator' block contains a series of weighting factors W\_1, W\_2, ..., W\_m, each multiplied by a transfer function block (1 + sT\_i/2n)^{2n}. These are summed together. A separate block (1 + sT\_c)^{2n} is also part of the compensator structure.

Fig. 7. Basic schematic of ADC block diagram.

$$ADC(s) = \sum_{i=1}^{m} W_i(\tau_d) \frac{(1 + \frac{T_i s}{2n})^{2n}}{(1 + \frac{T_c s}{2n})^{2n}}, \quad (36)$$

where  $W_i$  represents the weighting factor, and the counter of each compensator is determined to offset a portion of the phase delay. The time constant  $T_c$  in the denominator is dependent on the system's dynamics and is typically selected within the range of 0.01 s to 0.1 s. By solving the following system of equations,  $W_i(\tau_d)$  can be determined.

$$\left\{ \begin{array}{l} \tau_d^{2n} = \sum_{i=1}^{m} W_i(\tau_d) \times T_i^{2n}, \\ \tau_d^{2n-1} = \sum_{i=1}^{m} W_i(\tau_d) \times T_i^{2n-1}, \\ \vdots \\ \tau_d = \sum_{i=1}^{m} W_i(\tau_d) \times T_i, \\ 1 = \sum_{i=1}^{m} W_i(\tau_d). \end{array} \right. \quad (37)$$

where  $T_1$  and  $T_m$  represent the minimum and maximum delays, respectively, while  $T_2$  and  $T_{m-1}$  represent the intermediate delay values between them. Assuming  $m = 2n + 1$ , and employing Cramer's method, a unique expression for  $W_i(\tau_d)$  can be derived according to (37). The ADC process is depicted in Fig. 7.

## 5. Numerical simulations and performance analysis

To validate the proposed MPC-based VSG control strategy, the state-space model obtained in Section 2 is simulated using MATLAB/Simulink. A fixed-step solver with a sampling time of 0.01 seconds is employed to ensure precise numerical integration of full state-space model (28). For the MPC controller, the prediction and control horizons are set to 20 and 5 steps, respectively, to balance computational efficiency with control performance. The simulation duration spans 50 seconds, encompassing all disturbance scenarios outlined in Table 1. These parameters not only guarantee reproducible results but also align with practical sampling rates for real-time implementation.

The simulations are conducted under various disturbances to assess the effectiveness of the proposed method in a typical VSGs-SG system. Specifically, an islanded microgrid comprising three VSGs and one SG

**Table 1**  
Simulation scenarios associated with typical test VSGs-SG system.

| Time            | $\Delta P_{O_1}$ | $\Delta Q_{O_1}$ | $\Delta P_{O_2}$ | $\Delta Q_{O_2}$ | $\Delta P_{O_3}$ | $\Delta Q_{O_3}$ | $\Delta P_{SG}$ |
|-----------------|------------------|------------------|------------------|------------------|------------------|------------------|-----------------|
| $0 \le t < 5$   | 0                | 0                | 0                | 0                | 0                | 0                | 0               |
| $5 \le t < 10$  | 0.2 pu           | 0                | 0                | 0                | 0                | 0                | 0               |
| $10 \le t < 15$ | 0                | 0                | 0.3 pu           | 0                | 0                | 0                | 0               |
| $15 \le t < 20$ | 0                | 0                | 0                | 0                | 0.1 pu           | 0                | 0               |
| $20 \le t < 30$ | 0                | 0                | 0                | 0                | 0                | 0                | 0.3 pu          |
| $30 \le t < 35$ | 0                | 0.1 pu           | 0                | 0                | 0                | 0                | 0               |
| $35 \le t < 40$ | 0                | 0                | 0                | -0.3 pu          | 0                | 0                | 0               |
| $40 \le t < 50$ | 0                | 0                | 0                | 0                | 0                | 0.2 pu           | 0               |

**Table 2**  
Specifications of typical test VSGs-SG system.

| Parameter  | Value     | Parameter   | Value    | Parameter    | Value  |
|------------|-----------|-------------|----------|--------------|--------|
| $S_{base}$ | 10 kV A   | $L_{f_2}$   | 0.003 pu | $M_1$        | 50 s   |
| $V_{base}$ | 200 V     | $L_{f_3}$   | 0.002 pu | $M_2$        | 40 s   |
| $\omega_0$ | 377 rad/s | $R_1$       | 0.016 pu | $M_3$        | 60 s   |
| $R_L$      | 5 pu      | $R_2$       | 0.040 pu | $M_{SG}$     | 30 s   |
| $L_L$      | 5 pu      | $R_3$       | 0.070 pu | $K_1$        | 0.0125 |
| $R_{v_1}$  | 0.059 pu  | $L_1$       | 0.250 pu | $K_2$        | 0.0225 |
| $R_{v_2}$  | 0.065 pu  | $L_2$       | 0.300 pu | $K_3$        | 0.0325 |
| $R_{v_3}$  | 0.050 pu  | $L_3$       | 0.200 pu | $K_{p_1}$    | 20 pu  |
| $L_{f_1}$  | 0.001 pu  | $R_x$       | 0.016 pu | $K_{p_2}$    | 25 pu  |
| $L_{f_2}$  | 0.003 pu  | $L_x$       | 0.150 pu | $K_{p_3}$    | 15 pu  |
| $L_{f_3}$  | 0.002 pu  | $X_{SG_d}$  | 0.219 pu | $K_{d_1}$    | 5 pu   |
| $C_{f_1}$  | 1 pu      | $X_{SG_q}$  | 0.219 pu | $K_{d_2}$    | 12 pu  |
| $C_{f_2}$  | 0.700 pu  | $X'_{SG_d}$ | 0.027 pu | $K_{d_3}$    | 17 pu  |
| $C_{f_3}$  | 0.800 pu  | $X'_{SG_q}$ | 0.027 pu | $K_{p_{SG}}$ | 25 pu  |
| $R_{f_1}$  | 0.005 pu  | $D_1$       | 17 pu    | $N_c$        | 2      |
| $R_{f_2}$  | 0.001 pu  | $D_2$       | 20 pu    | $N_p$        | 10     |
| $R_{f_3}$  | 0.004 pu  | $D_3$       | 19 pu    | $\tau_d$     | 0.2 s  |
| $L_{f_1}$  | 0.001 pu  | $D_{SG}$    | 15 pu    |              |        |

that supplies an impedance load is considered. Several disturbance scenarios, including changes in the active power reference of VSGs, reactive power reference of VSGs, and active power reference of the SG, are examined to analyze the system's performance. The sequence of the disturbance scenarios and the parameters of the test system are provided in Tables 1 and 2, respectively.

The disturbance sequence presented in Table 1 is systematically designed to evaluate the system's dynamic response to both active and

![Figure 8: Variations in the frequency of VSGs and SG. (a) Basic control method: Frequency variations (Δω) in p.u. (scaled by 10^-3) over 50 seconds. (b) MPC-based VSG control strategy: Frequency variations (Δω) in p.u. (scaled by 10^-5) over 50 seconds. Both plots show the response of VSG1 (red solid), VSG2 (black dashed), VSG3 (green solid), and SG (blue dashed) to disturbances at t=5, 10, 15, 20, 30, and 40 seconds.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 8: Variations in the frequency of VSGs and SG. (a) Basic control method: Frequency variations (Δω) in p.u. (scaled by 10^-3) over 50 seconds. (b) MPC-based VSG control strategy: Frequency variations (Δω) in p.u. (scaled by 10^-5) over 50 seconds. Both plots show the response of VSG1 (red solid), VSG2 (black dashed), VSG3 (green solid), and SG (blue dashed) to disturbances at t=5, 10, 15, 20, 30, and 40 seconds.

**Fig. 8.** Variations in the frequency of VSGs and SG after the disturbances mentioned in Table 1: (a) basic control method, and (b) MPC-based VSG control strategy.

reactive power reference variations, replicating realistic operational scenarios in microgrid environments. This testing approach aligns with contemporary validation methodologies employed in recent studies, including [2] and [26]. The selected disturbance profile enables comprehensive assessment of the proposed control scheme's performance across various operating conditions.

Figs. 8(a) and 9(a) illustrate the variations in frequency and input active power of the VSGs and SG with the basic control, respectively. At  $t = 5$  s, an increase in the active power reference of first VSG results in a higher input power for that unit. Consequently, the frequency of first VSG increases. The increased input power of first VSG causes a decrease in the input power of the SG, leading to a reduction in its frequency. Similarly, at  $t = 10$  s,  $t = 15$  s, and  $t = 20$  s, the frequencies of second VSG, third VSG, and SG increase, respectively, due to increases in their respective active power references. It is evident that second VSG has the highest overshoot in frequency variations because its active power reference is set to 0.3 p.u., which is higher than the references of the other VSGs. At  $t = 30$  s and  $t = 40$  s, the reactive power references of first and second VSGs increase, respectively, resulting in a reduction in their frequencies. Additionally, at  $t = 35$  s, a slight increase in the frequency of third VSG is observed due to a reduction in its reactive power reference.

As shown in Fig. 8(a), the application of the basic VSG control leads to noticeable overshoot and slower settling time following step changes in active power references. Furthermore, the frequencies of the VSGs and SG are not synchronized, which can lead to system instability. To address this issue and effectively control the frequencies of the VSGs and SG, a central MPC-based VSG control strategy is implemented. The proposed central control strategy compares the references and outputs of the VSGs and SG at each sampling time. By considering constraints and weights, the control strategy solves an objective function to determine the optimal values for the system's future inputs. Additionally, an ADC is incorporated into the proposed control to account for communication delays. Figs. 8(b) and 9(b) display the frequency and input active power variations of the VSGs and SG with the suggested control strategy, respectively. It is evident that the proposed MPC-based VSG control effectively suppresses the overshoot and reduces the rate of frequency fluctuation, resulting in a faster stabilization of the system. Specifically, when the active power reference of first VSG increases at  $t = 5$  s, the frequency variations are greatly reduced. Similarly, at  $t = 10$  s,  $t = 15$  s, and  $t = 20$  s, the frequency variations of second VSG, third VSG, and SG exhibit minor increases, respectively. The MPC-based control approach

![Figure 9: Variations in the input active power of VSGs and SG. (a) Basic control method: Input active power variations (ΔP_in) in p.u. over 50 seconds. (b) MPC-based VSG control strategy: Input active power variations (ΔP_in) in p.u. over 50 seconds. Both plots show the response of VSG1 (red solid), VSG2 (black dashed), VSG3 (green solid), and SG (blue dashed) to disturbances at t=5, 10, 15, 20, 30, and 40 seconds.](aa14b9ec884bf40ce06c161be468cd84_img.jpg)

Figure 9: Variations in the input active power of VSGs and SG. (a) Basic control method: Input active power variations (ΔP\_in) in p.u. over 50 seconds. (b) MPC-based VSG control strategy: Input active power variations (ΔP\_in) in p.u. over 50 seconds. Both plots show the response of VSG1 (red solid), VSG2 (black dashed), VSG3 (green solid), and SG (blue dashed) to disturbances at t=5, 10, 15, 20, 30, and 40 seconds.

**Fig. 9.** Variations in the input active power of VSGs and SG after the disturbances mentioned in Table 1: (a) basic control method, and (b) MPC-based VSG control strategy.

![Figure 10: Variations in the frequency of first VSG considering different inertia constants. (a) Basic control method: Frequency variations (Δω) in p.u. (scaled by 10^-3) over 50 seconds. (b) MPC-based VSG control strategy: Frequency variations (Δω) in p.u. (scaled by 10^-5) over 50 seconds. Both plots show the response for different inertia constants M=20 (yellow), M=35 (blue), M=50 (green), M=65 (black), and M=80 (red). Insets show zoomed-in views of the frequency response between t=31 and 34 seconds for (a) and t=5 and 5.8 seconds for (b).](f5e70cbe66e71e65b4ae4aa7816d266a_img.jpg)

Figure 10: Variations in the frequency of first VSG considering different inertia constants. (a) Basic control method: Frequency variations (Δω) in p.u. (scaled by 10^-3) over 50 seconds. (b) MPC-based VSG control strategy: Frequency variations (Δω) in p.u. (scaled by 10^-5) over 50 seconds. Both plots show the response for different inertia constants M=20 (yellow), M=35 (blue), M=50 (green), M=65 (black), and M=80 (red). Insets show zoomed-in views of the frequency response between t=31 and 34 seconds for (a) and t=5 and 5.8 seconds for (b).

**Fig. 10.** Variations in the frequency of first VSG considering different inertia constants following the disturbances listed in Table 1: (a) basic control method, and (b) MPC-based VSG control strategy.

enhances the performance of the VSG. As observed in these figures, when disturbances occur as per Table 1, the MPC approach effectively reduces oscillations, overshoots, and settling time, allowing the frequencies to return to their reference values. Consequently, the input active power variations of the VSGs and SG are mitigated, frequencies become synchronized, and system stability improves.

To investigate the impact of VSG parameters, the frequency variations of first VSG with/without the proposed control strategy are analyzed for different inertia constants and damping coefficients. The results are presented in Figs. 10 and 11, respectively. The figures reveal that increasing the inertia constant reduces the magnitude of frequency overshoot but leads to longer oscillations before reaching steady state, while increasing the damping coefficient significantly improves transient response by decreasing the amplitude of oscillations. These trends support the analytical findings and validate the effectiveness of the proposed MPC with ADC strategy in balancing dynamic performance and stability.

As discussed in Section 3, the MPC control involves communication delays due to the transmission and reception of orders. This delay can

![Figure 11: Variations in the frequency of first VSG. (a) Basic control method showing frequency deviation Δω_Basic (pu) over 50 seconds. (b) MPC-based VSG control strategy showing frequency deviation Δω_MPC (pu) over 50 seconds with an inset of a zoomed-in view from 5 to 5.6 seconds. Both plots compare VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green for damping coefficients D=5, 12, 17, 24, and 31.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 11: Variations in the frequency of first VSG. (a) Basic control method showing frequency deviation Δω\_Basic (pu) over 50 seconds. (b) MPC-based VSG control strategy showing frequency deviation Δω\_MPC (pu) over 50 seconds with an inset of a zoomed-in view from 5 to 5.6 seconds. Both plots compare VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green for damping coefficients D=5, 12, 17, 24, and 31.

Fig. 11. Variations in the frequency of first VSG considering different damping coefficients following the disturbances listed in Table 1: (a) basic control method, and (b) MPC-based VSG control strategy.

![Figure 12: Variations in the frequency of first VSG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω_{VSG_1} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 30-32 second range.](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 12: Variations in the frequency of first VSG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω\_{VSG\_1} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 30-32 second range.

Fig. 12. Variations in the frequency of first VSG considering communication delay of 0.2 s with different control methods after the disturbances mentioned in Table 1.

induce system oscillations and destabilize the system. To compensate for this communication latency, an ADC is introduced. It is important to ensure that the proposed control mechanism remains effective with the inclusion of ADC, as it should be capable of compensating for the delay. To evaluate the effectiveness of the ADC, the VSGs-SG system is simulated considering a communication delay of 0.2 s. Figs. 12, 13, 14, and 15 compare the frequency variations of first VSG, second VSG, third VSG, and SG, respectively, for the basic control, MPC, and ADC-added MPC strategies. By incorporating ADC into the applied MPC, the proposed control effectively mitigates the impact of communication delay and prevents system instability. However, as expected, there is an increase in overshoot and settling time compared to the case without delay. Nevertheless, it still outperforms the basic control in terms of effectiveness and efficiency.

As mentioned earlier, the amount of communication delay depends on various factors, including the communication type. To assess the robustness of the proposed control, the VSGs-SG test system is evaluated with different communication delay values, namely  $\tau_d = 0.2s$ ,  $\tau_d = 0.4s$ , and  $\tau_d = 0.6s$ . The frequency variations of first VSG, second VSG, third VSG, and SG considering different amounts of delay are presented in Figs. 16, 17, 18, and 19, respectively. The results demonstrate that as the communication delay increases, the frequency fluctuates more and the settling time increases. Furthermore, Figs. 20, 21, 22, and 23 illustrate

![Figure 13: Variations in the frequency of second VSG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω_{VSG_2} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 35-37 second range.](0d5fdb87a392819c7d2e3b6230912a0b_img.jpg)

Figure 13: Variations in the frequency of second VSG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω\_{VSG\_2} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 35-37 second range.

Fig. 13. Variations in the frequency of second VSG considering communication delay of 0.2 s with different control methods after the disturbances mentioned in Table 1.

![Figure 14: Variations in the frequency of third VSG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω_{VSG_3} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 40-43 second range.](4495fbec19aac6861f1a0b35c4dc38bc_img.jpg)

Figure 14: Variations in the frequency of third VSG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω\_{VSG\_3} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based VSG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 40-43 second range.

Fig. 14. Variations in the frequency of third VSG considering communication delay of 0.2 s with different control methods after the disturbances mentioned in Table 1.

![Figure 15: Variations in the frequency of SG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω_{SG} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based SG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 5.5-6.5 second range.](ca5f2304ffe22946414ffab54cd3fd93_img.jpg)

Figure 15: Variations in the frequency of SG considering a communication delay of 0.2 s. The plot shows frequency deviation Δω\_{SG} (pu) over 50 seconds. It compares VSG (Basic) in red, MPC-Based SG in blue, and MPC-Based VSG+ADC in green. An inset zooms in on the 5.5-6.5 second range.

Fig. 15. Variations in the frequency of SG considering communication delay of 0.2 s with different control methods after the disturbances mentioned in Table 1.

the input active power variations of first VSG, second VSG, third VSG, and SG, respectively. Similarly, as the communication delay increases, the system exhibits more fluctuations and the damping rate decreases during changes in the reference active power of the VSGs and SG. Consequently, the stability of the system is reduced.

Table 3 summarizes the quantitative performance comparison between the basic control, MPC without delay compensation, and MPC combined with the ADC. The metrics include maximum frequency deviation, settling time, and RMS frequency error over the disturbance period. The results clearly show that the proposed MPC-based strategy significantly reduces maximum deviation and improves settling time

![Figure 16: Frequency variations of first VSG with ADC considering different amounts for communication delay. The main plot shows frequency deviation Δω1SG1 (pu) × 10^-4 from 0 to 10 over 50 seconds. A disturbance occurs at t=5s, causing a peak deviation of ~10 pu. An inset plot shows a zoomed-in view of the frequency response between 30 and 36 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 16: Frequency variations of first VSG with ADC considering different amounts for communication delay. The main plot shows frequency deviation Δω1SG1 (pu) × 10^-4 from 0 to 10 over 50 seconds. A disturbance occurs at t=5s, causing a peak deviation of ~10 pu. An inset plot shows a zoomed-in view of the frequency response between 30 and 36 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.

Fig. 16. Frequency variations of first VSG with ADC considering different amounts for communication delay.

![Figure 17: Frequency variations of second VSG with ADC considering different amounts for communication delay. The main plot shows frequency deviation Δω2SG2 (pu) × 10^-4 from 0 to 15 over 50 seconds. A disturbance occurs at t=10s, causing a peak deviation of ~15 pu. An inset plot shows a zoomed-in view of the frequency response between 35 and 39 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 17: Frequency variations of second VSG with ADC considering different amounts for communication delay. The main plot shows frequency deviation Δω2SG2 (pu) × 10^-4 from 0 to 15 over 50 seconds. A disturbance occurs at t=10s, causing a peak deviation of ~15 pu. An inset plot shows a zoomed-in view of the frequency response between 35 and 39 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.

Fig. 17. Frequency variations of second VSG with ADC considering different amounts for communication delay.

![Figure 18: Frequency variations of third VSG with ADC considering different amounts for communication delay. The main plot shows frequency deviation Δω3SG3 (pu) × 10^-4 from 0 to 4 over 50 seconds. A disturbance occurs at t=15s, causing a peak deviation of ~4 pu. An inset plot shows a zoomed-in view of the frequency response between 40 and 46 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.](33228b4227fa57e1477b27b9e07483e6_img.jpg)

Figure 18: Frequency variations of third VSG with ADC considering different amounts for communication delay. The main plot shows frequency deviation Δω3SG3 (pu) × 10^-4 from 0 to 4 over 50 seconds. A disturbance occurs at t=15s, causing a peak deviation of ~4 pu. An inset plot shows a zoomed-in view of the frequency response between 40 and 46 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.

Fig. 18. Frequency variations of third VSG with ADC considering different amounts for communication delay.

compared to the basic control. Furthermore, the addition of the ADC mitigates the impact of communication delays, maintaining synchronization with only a slight increase in settling time.

It should be noted that the proposed method uses a linearized state-space model derived around a specific equilibrium point. If the system operating point changes significantly over time (e.g., due to large variations in load or generation), the accuracy of the linear model may degrade, potentially reducing the effectiveness of the MPC controller. To address this limitation, future works could search for adaptive or gain-scheduled MPC approaches that update the model parameters based on real-time operating conditions, or implement nonlinear MPC formula-

![Figure 19: Frequency variations of SG with ADC considering different amounts for communication delay. The main plot shows frequency deviation ΔωSG (pu) × 10^-4 from 0 to 15 over 50 seconds. A disturbance occurs at t=20s, causing a peak deviation of ~15 pu. An inset plot shows a zoomed-in view of the frequency response between 30 and 36 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.](58de972a8c79c238b69cbeeafcc8d5fb_img.jpg)

Figure 19: Frequency variations of SG with ADC considering different amounts for communication delay. The main plot shows frequency deviation ΔωSG (pu) × 10^-4 from 0 to 15 over 50 seconds. A disturbance occurs at t=20s, causing a peak deviation of ~15 pu. An inset plot shows a zoomed-in view of the frequency response between 30 and 36 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.

Fig. 19. Frequency variations of SG with ADC considering different amounts for communication delay.

![Figure 20: Active power variations of first VSG with ADC considering different amounts for communication delay. The main plot shows active power deviation ΔPin (pu) from -0.1 to 0.25 over 50 seconds. A disturbance occurs at t=5s, causing a peak deviation of ~0.25 pu. An inset plot shows a zoomed-in view of the active power response between 30 and 36 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.](9a0dacb540bed1811d90cc1555c3fe7a_img.jpg)

Figure 20: Active power variations of first VSG with ADC considering different amounts for communication delay. The main plot shows active power deviation ΔPin (pu) from -0.1 to 0.25 over 50 seconds. A disturbance occurs at t=5s, causing a peak deviation of ~0.25 pu. An inset plot shows a zoomed-in view of the active power response between 30 and 36 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.

Fig. 20. Active power variations of first VSG with ADC considering different amounts for communication delay.

![Figure 21: Active power variations of second VSG with ADC considering different amounts for communication delay. The main plot shows active power deviation ΔPin (pu) from -0.1 to 0.25 over 50 seconds. A disturbance occurs at t=10s, causing a peak deviation of ~0.25 pu. An inset plot shows a zoomed-in view of the active power response between 35 and 39 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.](91b7db8990b37ee7c7646b8df81bc199_img.jpg)

Figure 21: Active power variations of second VSG with ADC considering different amounts for communication delay. The main plot shows active power deviation ΔPin (pu) from -0.1 to 0.25 over 50 seconds. A disturbance occurs at t=10s, causing a peak deviation of ~0.25 pu. An inset plot shows a zoomed-in view of the active power response between 35 and 39 seconds for three delay cases: 200 ms (red solid), 400 ms (blue dashed), and 600 ms (green dotted). The 600 ms delay shows the largest overshoot and slowest settling.

Fig. 21. Active power variations of second VSG with ADC considering different amounts for communication delay.

Table 3

Comparative performance of strategies under different disturbance scenarios.

| Metric                           | Basic Control | MPC     | MPC+ADC |
|----------------------------------|---------------|---------|---------|
| Maximum Frequency Deviation (pu) | 0.0055        | 0.00012 | 0.001   |
| Settling Time (s)                | 13.5          | 6.2     | 7.5     |
| RMS Frequency Error (pu)         | 0.0053        | 0.00    | 0.00    |

tions to better capture the system's dynamic behavior over a wider operating range. Therefore, it can be concluded that despite the promising results, several limitations of the proposed method should be acknowledged. First, the use of linearized full state-space model described in 



![Figure 22: Active power variations of the third VSG with ADC considering different amounts for communication delay. The main plot shows the active power variation ΔP_in (pu) over time (s) from 0 to 50. The y-axis ranges from -0.05 to 0.1. Three curves are shown: Delay 200 ms (red solid line), Delay 400 ms (blue dashed line), and Delay 600 ms (green dotted line). The 200 ms delay curve shows a large overshoot reaching approximately 0.08 pu. The 400 ms delay curve shows a smaller overshoot reaching approximately 0.04 pu. The 600 ms delay curve shows a very small overshoot reaching approximately 0.01 pu. An inset plot zooms in on the time interval from 40 to 44 seconds, showing the detailed response for each delay case. The inset y-axis is scaled by 10^-3 and ranges from 0 to 10.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 22: Active power variations of the third VSG with ADC considering different amounts for communication delay. The main plot shows the active power variation ΔP\_in (pu) over time (s) from 0 to 50. The y-axis ranges from -0.05 to 0.1. Three curves are shown: Delay 200 ms (red solid line), Delay 400 ms (blue dashed line), and Delay 600 ms (green dotted line). The 200 ms delay curve shows a large overshoot reaching approximately 0.08 pu. The 400 ms delay curve shows a smaller overshoot reaching approximately 0.04 pu. The 600 ms delay curve shows a very small overshoot reaching approximately 0.01 pu. An inset plot zooms in on the time interval from 40 to 44 seconds, showing the detailed response for each delay case. The inset y-axis is scaled by 10^-3 and ranges from 0 to 10.

Fig. 22. Active power variations of third VSG with ADC considering different amounts for communication delay.

![Figure 23: Active power variations of the SG with ADC considering different amounts for communication delay. The main plot shows the active power variation ΔP_in (pu) over time (s) from 0 to 50. The y-axis ranges from -0.1 to 0.25. Three curves are shown: Delay 200 ms (red solid line), Delay 400 ms (blue dashed line), and Delay 600 ms (green dotted line). The 200 ms delay curve shows a large overshoot reaching approximately 0.25 pu. The 400 ms delay curve shows a smaller overshoot reaching approximately 0.18 pu. The 600 ms delay curve shows a very small overshoot reaching approximately 0.05 pu. An inset plot zooms in on the time interval from 19.8 to 20.6 seconds, showing the detailed response for each delay case. The inset y-axis ranges from 0 to 0.25.](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

Figure 23: Active power variations of the SG with ADC considering different amounts for communication delay. The main plot shows the active power variation ΔP\_in (pu) over time (s) from 0 to 50. The y-axis ranges from -0.1 to 0.25. Three curves are shown: Delay 200 ms (red solid line), Delay 400 ms (blue dashed line), and Delay 600 ms (green dotted line). The 200 ms delay curve shows a large overshoot reaching approximately 0.25 pu. The 400 ms delay curve shows a smaller overshoot reaching approximately 0.18 pu. The 600 ms delay curve shows a very small overshoot reaching approximately 0.05 pu. An inset plot zooms in on the time interval from 19.8 to 20.6 seconds, showing the detailed response for each delay case. The inset y-axis ranges from 0 to 0.25.

Fig. 23. Active power variations of SG with ADC considering different amounts for communication delay.

(28) is suitable for small-signal analysis and moderate disturbances but may not fully capture the nonlinear dynamics of the system under large or sustained disturbances. Second, the design of the MPC controller employs fixed values for the prediction horizon and the weighting matrices in the cost function (33). While these settings are carefully chosen based on simulation studies, they may not guarantee optimal performance under changing system conditions or operating points. Future works could explore the use of nonlinear MPC formulations or adaptive and self-tuning strategies that dynamically adjust control parameters to enhance robustness and performance under a wider range of scenarios.

# 6. Conclusion

This study presents a comprehensive dynamic model of an islanded power system comprising multiple VSGs and a SG operating in parallel to supply an RL load. The analysis highlights the frequency stability challenges that arise from reduced system inertia and communication delays, which are characteristic of inverter-based distributed generation under islanded conditions. To address these challenges, the study proposes a centralized MPC-based VSG strategy enhanced with an ADC. The performance of the proposed method is evaluated under various disturbance scenarios, including step changes in the active and reactive power references of the VSGs and the SG. Compared to the basic VSG control method, simulation results show that the MPC-based VSG approach reduces frequency overshoot to approximately 0.20 times that of the conventional method and achieves an approximate 45% reduction in settling time. These results highlight the robustness and effectiveness of the MPC in enhancing frequency stability in islanded microgrids. Additionally, the proposed method successfully restores and synchronizes the input active power and frequency, leading to a more stable overall system response. The study also investigates the impact of VSG parameters specifically, the inertia constant and damping coefficient

on system performance. It is shown that increasing virtual inertia can reduce frequency overshoot but may introduce additional oscillations, whereas higher damping improves transient response. By incorporating the ADC, the control strategy effectively mitigates the adverse effects of communication delays, maintaining frequency stability even under varying delay conditions. Overall, the results confirm that the suggested control approach provides a robust and efficient solution for enhancing frequency regulation and dynamic performance in islanded microgrids with high penetration of inverter-based renewable generation. Beyond technical improvements, the proposed MPC-based VSG control strategy also offers potential economic benefits. By effectively reducing frequency overshoot, settling time, and active power oscillations, the system can maintain stability with smaller or lower-capacity energy storage systems. This reduction in required storage size can translate into lower capital costs and operational savings, which is particularly important for microgrids with high renewable penetration where storage is a significant investment. Although this study does not include a detailed cost-benefit analysis, these findings suggest that advanced predictive control and delay compensation techniques can contribute not only to technical resilience but also to improved economic efficiency of islanded microgrids.

# CRediT authorship contribution statement

**Mohammadreza Najafi:** Writing – original draft, Validation, Software, Resources, Investigation, Formal analysis, Data curation, Conceptualization. **Mohammadreza Toulabi:** Writing – review & editing, Visualization, Supervision, Resources, Project administration, Methodology, Investigation, Funding acquisition, Conceptualization.

# Declaration of competing interest

I hereby declare that I have no pecuniary or other personal interest, direct or indirect, in any matter that raises or may raise a conflict with others.

# Data availability

No data was used for the research described in the article.

# References

- [1] A. Pinnarelli, P. Vizza, G. Brusco, D. Menniti, N. Sorrentino, G.V. Shagar, A. Soleimani, Multi-agent approach for synthetic inertia and fast reserve service provided by a distributed energy storage system, *Results Eng.* 27 (Sep. 2025) 105474.
- [2] M.A. Shobug, F. Yang, J. Lu, Stability improvement of microgrids under dynamic load conditions: a new adaptive virtual synchronous generator based virtual inertia control approach, *Results Eng.* 25 (Mar. 2025) 104556.
- [3] M. Mahmoudia, T. Amraee, M. Toulabi, Enhancing security and frequency control: integrating wind turbine participation in power electronics-controlled sustainable grids operation, *IEEE Trans. Consum. Electron.* 71 (1) (Feb. 2025) 1647–1660.
- [4] M. Toulabi, S. Bahrami, A.M. Ranjbar, Optimal supplementary frequency controller design using the wind farm frequency model and controller parameters stability region, *ISA Trans.* 74 (Mar. 2018) 175–184.
- [5] C. Garcia-Ceballos, S. Perez-Londono, J. Mora-Florez, Stability analysis framework for isolated microgrids with energy resources integrated using voltage source converters, *Results Eng.* 19 (Sep. 2023) 101252.
- [6] M. Yessief, B. Bossouti, M. Taoussi, A. Lagrioui, H. Chojae, B. Majout, H. El Alami, Robust control of a wind conversion system based on a doubly-fed induction generator: a comparison between adaptive backstepping and integral sliding mode controllers, in: *Digital Technologies and Applications*, Springer International Publishing, May 2022, pp. 722–732.
- [7] M. Yessief, B. Bossouti, M. Taoussi, A. Lagrioui, H. Chojae, Improved hybrid control strategy of the doubly-fed induction generator under a real wind profile, in: *Digital Technologies and Applications*, Springer International Publishing, Jun. 2021, pp. 1279–1290.
- [8] M. Pourmohammad, M. Toulabi, Designing a central MIMO state feedback controller for a microgrid with multi-parallel VSGs to damp active power oscillations, *Int. J. Electr. Power Energy Syst.* 133 (Dec. 2021) 106984.
- [9] H. Kumar, A. Gafoor Shaik, R. Yadav, Automatic voltage regulator integrated virtual synchronous generator control of plug-in electric vehicles for ancillary services support, *Results Eng.* 25 (Mar. 2025) 104390.

- [10] C. Liu, Z. Chu, Z. Duan, Y. Zhang, VSG-based adaptive optimal frequency regulation for AC microgrids with nonlinear dynamics, *IEEE Trans. Autom. Sci. Eng.* 22 (Feb. 2024) 1471–1482.
- [11] J. Wang, X. Zhang, Transient virtual inertia optimization strategy for virtual synchronous generator based on equilibrium point state assessment, *Int. J. Electr. Power Energy Syst.* 155 (Jan. 2024) 109588.
- [12] J. Sun, X. Xing, C. Zhang, Modeling, analysis, and mitigation of active power oscillation in parallel VSGs system, *IEEE Trans. Power Electron.* (Jul. 2025) 1–12, <https://doi.org/10.1109/TPEL.2025.3589731>, in press.
- [13] Q.C. Zhong, G. Weiss, Synchronverters: inverters that mimic synchronous generators, *IEEE Trans. Ind. Electron.* 58 (4) (Apr. 2011) 1259–1267.
- [14] K.M. Cheema, A comprehensive review of virtual synchronous generator, *Int. J. Electr. Power Energy Syst.* 120 (Sep. 2020) 106006.
- [15] Y. Li, F. Deng, R. Qi, H. Lin, Adaptive virtual impedance regulation strategy for reactive and harmonic power sharing among paralleled virtual synchronous generators, *Int. J. Electr. Power Energy Syst.* 140 (Sep. 2022) 108059.
- [16] X. Gao, Z. Wang, L. Ding, W. Bao, Z. Wang, Q. Hao, A novel virtual synchronous generator control scheme of DFIG-based wind turbine generators based on the rotor current-induced electromotive force, *Int. J. Electr. Power Energy Syst.* 156 (Feb. 2024) 109688.
- [17] K.Y. Yap, C.R. Sarimuthu, J.M.Y. Lim, Virtual inertia-based inverters for mitigating frequency instability in grid-connected renewable energy system: a review, *Appl. Sci.* 9 (24) (Dec. 2019) 5300.
- [18] S. Fahad, A. Goudarzi, J. Xiang, Demand management of active distribution network using coordination of virtual synchronous generators, *IEEE Trans. Sustain. Energy* 12 (1) (Jan. 2021) 250–261.
- [19] X. Liang, C. Andalib-Bin-Karim, W. Li, M. Mitolo, M.N.S.K. Shabbir, Adaptive virtual impedance-based reactive power sharing in virtual synchronous generator controlled microgrids, *IEEE Trans. Ind. Appl.* 57 (1) (Jan. 2021) 46–60.
- [20] M. Pourmohammad, M. Toulabi, A.M. Ranjbar, Application of state feedback controller to ensure robust D-stable operation of virtual synchronous generators, *IEEE Trans. Energy Convers.* 36 (2) (Jun. 2021) 602–610.
- [21] G. Wang, L. Fu, Q. Hu, C. Liu, Y. Ma, Transient synchronization stability of grid-forming converter during grid fault considering transient switched operation mode, *IEEE Trans. Sustain. Energy* 14 (3) (Jul. 2023) 1504–1515.
- [22] A. Asrari, M. Mustafa, M. Ansari, J. Khazaei, Impedance analysis of virtual synchronous generator-based vector controlled converters for weak AC grid integration, *IEEE Trans. Sustain. Energy* 10 (3) (Jul. 2019) 1481–1490.
- [23] P. Sun, J. Yao, Y. Zhao, X. Fang, J. Cao, Stability assessment and damping optimization control of multiple grid-connected virtual synchronous generators, *IEEE Trans. Energy Convers.* 36 (4) (Dec. 2021) 3555–3567.
- [24] Z. Tao, H. Lei, C.H. Tian, M.H. Bhatti, D. Sibtain, T. Rafiq, H. Ahmad, Demand driven distributed model predictive control with linear active disturbance rejection control for frequency management in smart grid environment, *Results Eng.* 26 (Jun. 2025) 105481.
- [25] Z. Li, H. Li, X. Zheng, M. Gao, Virtual model predictive control for virtual synchronous generators to achieve coordinated voltage unbalance compensation in islanded microgrids, *Int. J. Electr. Power Energy Syst.* 146 (Mar. 2023) 108756.
- [26] B. Long, Y. Liao, K.T. Chong, J. Rodríguez, J.M. Guerrero, Enhancement of frequency regulation in ac microgrid: a fuzzy-MPC controlled virtual synchronous generator, *IEEE Trans. Smart Grid* 12 (4) (Jul. 2021) 3138–3149.
- [27] J. Jongudomkarn, J. Liu, T. Ise, Virtual synchronous generator control with reliable fault ride-through ability: a solution based on finite-set model predictive control, *IEEE J. Emerg. Sel. Top. Power Electron.* 8 (4) (Dec. 2020) 3811–3824.
- [28] B. Long, Y. Liao, K.T. Chong, J. Rodríguez, J.M. Guerrero, MPC-controlled virtual synchronous generator to enhance frequency and voltage dynamic performance in islanded microgrids, *IEEE Trans. Smart Grid* 12 (2) (Mar. 2020) 953–964.
- [29] C. Zheng, T. Dragičević, F. Blaabjerg, Model predictive control-based virtual inertia emulator for an islanded alternating current microgrid, *IEEE Trans. Ind. Electron.* 68 (8) (Aug. 2021) 7167–7177.
- [30] B. Naduvathuparambil, M.C. Valenti, A. Feliachi, Communication delays in wide area measurement systems, in: *Proceedings of the Thirty-Fourth Southeastern Symposium on System Theory* (Cat. No. 02EX540), Huntsville, AL, USA, Mar. 2002, pp. 118–122.
- [31] K. Shi, W. Song, H. Ge, P. Xu, Y. Yang, F. Blaabjerg, Transient analysis of microgrids with parallel synchronous generators and virtual synchronous generators, *IEEE Trans. Energy Convers.* 35 (1) (Mar. 2020) 95–105.
- [32] H. Zhang, D. Li, H. Liu, D. Sun, Y. Yang, Y. Shao, Y. Sun, Comparison of low frequency oscillation characteristic differences between VSG and SG, in: *2020 IEEE Sustainable Power and Energy Conference (ISPEC)*, Chengdu, China, Nov. 2020, pp. 668–673.
- [33] J. Alipoor, Y. Miura, T. Ise, Power system stabilization using virtual synchronous generator with alternating moment of inertia, *IEEE J. Emerg. Sel. Top. Power Electron.* 3 (2) (Jun. 2015) 451–458.
- [34] H. Cheng, Z. Shuai, C. Shen, X. Liu, Z. Li, Z.J. Shen, Transient angle stability of paralleled synchronous and virtual synchronous generators in islanded microgrids, *IEEE Trans. Power Electron.* 35 (8) (Aug. 2020) 8751–8765.
- [35] P.S. Kundur, O.P. Malik, *Power System Stability and Control*, McGraw-Hill Education, 1994.
- [36] M. Eremia, M. Shahidehpour, *Handbook of Electrical Power System Dynamics: Modeling, Stability, and Control*, Wiley-IEEE Press, 2013.
- [37] C. Bordons, F. Garcia-Torres, M.A. Ridao, *Model Predictive Control of Microgrids*, Springer, 2020.