

## Article

# Adaptive Backstepping Control with Time-Delay Compensation for MR-Damper-Based Vehicle Seat Suspension

Heting Feng <sup>1</sup>, Yunhu Zhou <sup>1</sup>, Shaoqi Li <sup>1,\*</sup> ![ORCID icon](c3d993ca47bfe2a953c700506ce31fa0_img.jpg), Gongxun Cheng <sup>1</sup>, Shang Ma <sup>1</sup> and Yancheng Li <sup>1,2,\*</sup>

<sup>1</sup> Centre for Innovative Structures, College of Civil Engineering, Nanjing Tech University, Nanjing 211816, China; 202261126011@njtech.edu.cn (H.F.); m15655508415@163.com (Y.Z.); chengongxun@njtech.edu.cn (G.C.); 17766049159@163.com (S.M.)

<sup>2</sup> School of Civil and Environmental Engineering, Faculty of Engineering and Information Technology, University of Technology Sydney, Ultimo, NSW 2007, Australia

\* Correspondence: shaoqi@njtech.edu.cn (S.L.); yancheng.li@uts.edu.au (Y.L.)

**Abstract:** Long-term vibrations endanger driver health and affect ride performance. Semi-active seat suspension systems equipped with magnetorheological (MR) dampers can effectively reduce vibrations transmitted to drivers, exhibiting excellent potential for widespread applications owing to their outstanding performance characteristics. In this paper, we propose an adaptive backstepping control system with time-delay compensation (ABC-C) for an MR-damper-based semi-active seat suspension system to enhance ride comfort and stability in commercial vehicles. The control framework integrates a reference model, an adaptive backstepping controller, a time-delay compensator, and an MR damper inverse model. The reference model balances ride comfort and stability using high-pass and low-pass filters, while the adaptive controller ensures robustness against parameter uncertainties and disturbances. A time-delay compensator mitigates delays in the control loop, improving system stability and performance. Numerical simulations under harmonic, bump, and random excitations demonstrated the superior performance of the ABC-C controller. The experimental results show that under random road excitation conditions, the frequency-weighted root mean square (FW-RMS) of acceleration was reduced by 26.9%, the vibration dose value (VDV) decreased by 29.3%, and the root mean square of relative displacement (RMS\_rd) was reduced by 58.46%. The results highlight the practical effectiveness of the ABC-C controller in improving ride comfort and safety for drivers of commercial vehicles, offering significant potential for real-world applications.

**Keywords:** seat suspension; magnetorheological dampers; adaptive backstepping control; time-delay compensation; stability analysis

![Check for updates icon](1d7527f4316cfe2d342b08d1653d1592_img.jpg)

Check for updates icon

Academic Editor: Moon Kyu Kwak

Received: 1 February 2025

Revised: 28 March 2025

Accepted: 4 April 2025

Published: 6 April 2025

**Citation:** Feng, H.; Zhou, Y.; Li, S.; Cheng, G.; Ma, S.; Li, Y. Adaptive Backstepping Control with Time-Delay Compensation for MR-Damper-Based Vehicle Seat Suspension. *Actuators* **2025**, *14*, 178. <https://doi.org/10.3390/act14040178>

**Copyright:** © 2025 by the authors. Licensee MDPI, Basel, Switzerland. This article is an open access article distributed under the terms and conditions of the Creative Commons Attribution (CC BY) license (<https://creativecommons.org/licenses/by/4.0/>).

## 1. Introduction

Drivers of commercial vehicles face prolonged exposure to harmful vibrations from poor road conditions and extended operating h, leading to chronic physical and mental health risks [1,2]. To address this, seat suspension systems, comprising springs, dampers, actuators, or combinations thereof, have emerged as critical solutions, isolating drivers by absorbing and dissipating road-induced vibrations. These systems attenuate vibration transmission, enhancing comfort and safety. Seat suspension systems are categorized as passive, active, or semi-active. Passive systems [3,4], though cost-effective and simple, lack adaptability due to fixed damping properties. Active suspension systems [5] excel in vibration isolation using external power sources but suffer from complexity, high energy use, and cost barriers. Semi-active systems bridge this gap by modulating damping or

stiffness in response to driving conditions, offering effective vibration control without requiring substantial external energy, making them reliable and practical for real-world applications [6,7]. By balancing performance and efficiency, semi-active suspension systems represent a promising solution to safeguarding driver well-being while maintaining operational feasibility in commercial vehicles.

In recent decades, MR materials have emerged as a key enabling material for semi-active suspension systems [8–10]. MR fluids consist of micron-sized ferromagnetic particles suspended in a carrier fluid. Their rheological properties can be rapidly and reversibly altered by applying an external magnetic field [11–13]. MR dampers, which utilize MR fluids, offer several advantages, including a wide range of controllable damping forces, fast response times, and low energy consumption [14]. These characteristics have made MR dampers a popular choice for semi-active seat suspension systems, attracting significant research interest [15–17]. McManus et al. [18] integrated an MR damper into a seat suspension system to mitigate end-stop impacts. The vibration dose value (VDV) was reduced by approx. 40% compared to traditional dampers, demonstrating that the use of an MR damper can result in considerably less severe impacts and correspondingly lower vibration exposure levels. Hiemenz et al. [19] implemented semi-active MR dampers in helicopter seat suspension systems, reducing vertical vibration by 76% compared to passive seats, highlighting the excellent performance of MR dampers in seat suspension systems.

MR dampers can be categorized into linear dampers [20] and rotary dampers [7,21] according to their motion modes. Linear dampers produce damping force through the linear motion of the piston, making them ideal for linear vibration control. They are characterized by a simple structure, rapid response times, and the capacity for accurate damping force adjustment. Rotary MR dampers produce damping force through rotational motion, making them suitable for rotational vibration control. They feature a compact design and no stroke limitations but have some limitations in terms of control complexity and response speed. A linear MR damper was used in the seat suspension system in this research in order to utilize its fast response and precise control capabilities to improve vibration isolation performance.

The performance of MR-damper-based seat suspension systems heavily depends on the semi-active control strategy employed. Numerous control methods have been explored to optimize vibration isolation and ride comfort. For instance, Yao et al. [22] proposed a control strategy based on Lyapunov functional theory and linear matrix inequalities, giving rise to a 39.25% reduction in the root mean square value of body vertical acceleration. Shin et al. [23] introduced an adaptive fuzzy controller. Integrating this controller with a sliding mode controller further enhanced robustness against mass uncertainty and external disturbances. The results demonstrated that the hybrid controller effectively reduced the vertical acceleration of the seat under bump-related, random, and sinusoidal conditions. Additionally, Dong et al. [24] compared five semi-active control algorithms, i.e., skyhook, hybrid, LQG, sliding mode, and fuzzy logic control. The five control algorithms attenuated sprung mass acceleration by 13.82%, 0.71%, 3.15%, 14.31%, and 4.6%, respectively.

Despite these advancements, many existing studies rely on overly simplified seat suspension models that fail to capture the inherent nonlinearities and uncertainties of real-world suspension systems. Semi-active seat suspension systems are inherently nonlinear, with suspension springs and dampers exhibiting complex behaviors under varying road conditions and vehicle speeds, posing challenges for accurate suspension control modeling. Furthermore, changes in passenger load or dynamic forces introduce parametric uncertainties, leading to modeling inaccuracies and potential instability in control systems. To address these challenges, Astolfi et al. [25] systematically proposed a backstepping method for nonlinear systems, utilizing recursive Lyapunov-based design and adaptive laws to

estimate unknown parameters, ensuring global stability. Pang et al. [26] further developed a constrained adaptive backstepping controller for nonlinear active suspension systems, mitigating road disturbances and safety constraints. Simulations demonstrated reductions in vertical acceleration by 87.91% (bumpy roads), 85.26% (random roads), and 95.92% (harmonic excitation). Sun et al. [27] introduced an adaptive backstepping control strategy for active suspension systems subject to hard constraints. Simulation results showed that the vehicle's vertical acceleration was reduced by up to 98.29%.

However, the time delay of seat suspension systems is not addressed in the previous studies on backstepping control strategies. The time delay in these systems primarily arises from two sources: (1) the inherent response time of the MR fluid and electromagnetic coil in the MR damper, and (2) the delay caused by the time needed for signal processing and computational output when the MR damper operates in conjunction with external control systems (e.g., sensors and controllers). These delays may impair control performance and lead to system instability [28–30]. Majdoub et al. [31] developed dual observers specifically for MR damper time-delay compensation, enabling real-time estimation of hysteretic internal states and stable adaptive state feedback regulation. While enabling high-accuracy tracking control with guaranteed stability, this approach necessitates precise Bouc–Wen model parameterization and consumes additional computational resources for state observation. Consequently, its practical implementation is subject to non-negligible constraints. Jin et al. [32] adopted radial basis function (RBF) neural networks for approximating the uncertain time-delay function, while they employed Lyapunov–Krasovskii functionals to rigorously analyze the stability of delayed system components. The proposed methodology synthesizes backstepping control, sliding mode control, neural network approximation, and delay compensation schemes, creating a sophisticated theoretical framework that amalgamates cutting-edge control techniques, albeit with increased complexity in terms of controller realization and practical deployment. Gao et al. [33] introduced a compensated backstepping controller utilizing an adaptive radial basis function (RBF) neural network inverse model. The Smith predictor compensation strategy was employed to resolve the time delay problem. This approach integrates multiple modules, such as the development of an RBF neural network inverse model, PID compensator design, and Smith predictor compensation. Despite its comprehensive functionality, this method necessitates training the neural network and adjusting multiple compensation parameters, leading to increased complexity.

In this research, a combined strategy of backstepping control and time delay integral compensation was employed to tackle the time delay problem. The time delay integral compensator adds an integral term to the error definition (i.e., the difference between the ideal and actual trajectories), enabling the accumulation of control inputs from a previous time interval. By leveraging the cumulative effect of the integral term, the controller can preemptively adjust the control input to mitigate the lag induced by time delay. This approach eliminates the need for intricate model prediction or parameter tuning and guarantees global stability in the presence of time delay and nonlinear disturbances via Lyapunov stability analysis. Consequently, this solution offers a simplified design, robust performance, and improved adaptability for real-time seat suspension control.

Building on these developments, in this study, we propose an adaptive backstepping control strategy with time-delay compensation to address the challenges of damping force control in MR-damper-based semi-active seat suspension systems. The proposed approach accounts for different types of excitations, mass variations, and input delays, ensuring robust and stable performance. The remainder of this paper is organized as follows: Section 2 presents the experimental setup and modeling of the MR seat suspension system; Section 3 details the design and simulation of the proposed controller; Section 4 describes

the construction of a seat suspension vibration test system and the experimental validation of the controller; and Section 5 concludes the study.

## 2. Seat Suspension System Modelling

At this stage, a dynamic model of the scissor-type MR seat suspension was constructed based on the structure and geometric specification. Subsequently, the mechanical properties of the main components of the suspension, i.e., an air spring and an MR damper, were tested and modelled. By substituting the models for the air spring and MR damper into the suspension model, we could then apply the model in the simulation and test the vibration control of the scissor-type seat suspension system.

### 2.1. Scissor-Type Seat Suspension Model

Figure 1a,b present the physical structure of the scissor-type seat suspension system and a corresponding schematic diagram, respectively. The suspension system includes upper and lower plates, with the upper plate supported by two pairs of scissor lever arms. An air spring and an MR damper are arranged in parallel to connect the lever arm and the lower plate. Specifically, the air spring was installed between pivot points  $F$  and  $G$  to provide spring force  $F_s$ , while the MR damper is positioned between points  $D$  and  $E$  to provide controllable damping force  $F_d$ . The mechanical guide mechanism comprises a scissor-shaped bracket with two pivots,  $A$  and  $B$ , attached by a hinge to the upper and lower plates, respectively, and pivot points  $C$  and  $D$ , equipped with rollers that slide in the rails. This configuration enables smooth vertical motion of the seat. Table 1 displays the dimensional parameters measured when the seat suspension was loaded with 60 kg and in static equilibrium. Figure 1c illustrates the equivalent model of the seat suspension system. Since the sensors in subsequent tests primarily monitor the state variables of the seat suspension system in the vertical direction, all representations were transformed into the vertical direction for consistency. Through a force analysis of the seat suspension system, the equivalent spring force  $F_{se}$  and damping forces  $F_{de}$  in the vertical direction were derived, enabling the development of a comprehensive seat suspension model. In this case,  $F_{de}$  denotes the equivalent damping forces of the MR damper without an applied current.  $u(t - \tau)$  is the control force of the MR damper with time delay.  $x$  and  $z$  are the displacement of the mass of the driver and the input displacement induced by vehicle vibration, respectively.  $M$  is the mass of the driver.

![Figure 1: (a) Physical structure of the seat suspension system showing the air spring and MR damper. (b) Schematic diagram of the seat suspension system with geometric parameters and forces. (c) Equivalent model of the seat suspension system showing the mass M, equivalent spring force Fse, equivalent damping force Fde, and control force u(t - tau).](451417078c55730b2f3f9ea924407f78_img.jpg)

Figure 1 consists of three sub-figures. (a) is a photograph of the physical seat suspension system, showing the air spring and MR damper components. (b) is a schematic diagram of the system, showing the upper and lower plates, scissor lever arms, and the air spring and MR damper. It includes geometric parameters such as  $h_0$ ,  $\theta$ ,  $\phi$ ,  $\alpha$ ,  $\beta$ , and  $\gamma$ , and forces  $F_s$ ,  $F_d$ ,  $F_{se}$ , and  $F_{de}$ . (c) is an equivalent model of the system, showing a mass  $M$  connected to a base by an equivalent spring  $F_{se}$  and an equivalent damper  $F_{de}$ . The control force  $u(t - \tau)$  is applied to the damper. The displacement  $x$  of the mass and the input displacement  $z$  are shown.

Figure 1: (a) Physical structure of the seat suspension system showing the air spring and MR damper. (b) Schematic diagram of the seat suspension system with geometric parameters and forces. (c) Equivalent model of the seat suspension system showing the mass M, equivalent spring force Fse, equivalent damping force Fde, and control force u(t - tau).

**Figure 1.** (a) Physical structure of the seat suspension system. (b) Schematic diagram of the seat suspension system. (c) Equivalent model of the seat suspension system. The black arrow shows the left and right movement of the roller. The red arrow represents the damping force direction of the MR damper. The blue arrow denotes the spring force direction of the air spring. The dashed line serves as a reference in the force analysis.

**Table 1.** Parameters of the seat suspension system.

| Parameters | Value/m | Parameters | Value/° |
|------------|---------|------------|---------|
| $l_{AD}$   | 0.33    | $\alpha$   | 35.26   |
| $l_{BC}$   | 0.33    | $\beta$    | 81.24   |
| $l_{BF}$   | 0.14    | $\gamma$   | 39.60   |
| $l_{BE}$   | 0.21    | $\theta$   | 13.56   |
| $h_0$      | 0.20    | $\varphi$  | 8.10    |

The dynamics of the seat suspension system are described by the following equation:

$$M(t)\ddot{x} = -F_{se}(x, z, \dot{x}, \dot{z}, t) - F_{de}(\dot{x}, \dot{z}, t) + u(t - \tau) \quad (1)$$

Through a dynamics analysis of the entire seat suspension system, the equivalent elastic force of the air spring and equivalent damping force of the MR damper in the vertical direction can be derived:

$$F_{se} = \frac{F_s l_{BF} (\mu \sin \alpha + \cos \alpha) [\sin \beta \cos(\alpha + \theta) + \cos \beta \sin(\alpha + \theta)]}{l_{BC} (\cos \alpha)^2} \quad (2)$$

$$F_{de} = \frac{F_d l_{BE} (\mu \sin \alpha + \cos \alpha) [\sin \gamma \cos(\alpha + \varphi) + \cos \gamma \sin(\alpha + \varphi)]}{l_{BC} (\cos \alpha)^2} \quad (3)$$

where  $\mu$  is the rolling friction coefficient of rollers C and D, which is 0.1. Other parameters are shown in Table 1.

Define the state variables as  $x_1(t) = x(t)$ ,  $x_2(t) = \dot{x}(t)$ . Then, based on (1), the state-space equation of seat suspension can be expressed as follows:

$$\begin{cases} \dot{x}_1(t) = x_2(t) \\ \dot{x}_2(t) = \frac{1}{M(t)} (-F_{se}(x, z, \dot{x}, \dot{z}, t) - F_{de}(\dot{x}, \dot{z}, t) + u(t - \tau)) \end{cases} \quad (4)$$

### 2.2. Experimental Testing and Modeling of MR Damper and Air Spring

Experimental tests were conducted to investigate the mechanical properties of the MR damper and air spring. The testing system is illustrated in Figure 2a. A six-degree-of-freedom (6-DOF) vibration platform (HT78-150 KG, Suzhou Dongling Vibration Test Instrument (Suzhou, China) Co., Ltd.) was employed to produce horizontal excitation. The angle steel was secured to the platform using bolts. The test objects, i.e., the MR damper and air spring, were mounted between the steel angle and steel column using two clamps, ensuring the applied force was axial. A displacement sensor (MPS-XXS-600 mm-R, Hubei Miran Technology (Zaoyang, Hubei, China) Co., Ltd.) and a force sensor (PTST-500 KG, Force Sensing Technology (Nanjing, China) Co., Ltd.) were attached to the steel angle, measuring the relative displacement between the vibration platform and the steel angle as well as the force produced by the test objects during movement. The measured signals were collected using a Speedgoat real-time system (Speedgoat Inc. (Bern–Liebefeld, Switzerland)) with a sampling frequency of 1000 Hz and saved for further analysis. Based on the experimental results, suitable theoretical models were computed to describe the behavior of the MR damper and air spring.

Figure 2b shows the detailed test setup for the MR damper. The MR damper was tested under harmonic excitation with amplitudes of 4 mm, 8 mm, 12 mm, and 16 mm, while the excitation frequency was varied from 1 Hz to 2 Hz, 3 Hz, and 4 Hz. Current inputs of 0 A, 0.4 A, 0.8 A, 1.2 A, 1.6 A, and 2.0 A were applied to the damper during the test, using a DC power supply (UDP5306, Unit Technology (Guangzhou, Guangdong, China) Co., Ltd.). Figure 2c illustrates the detailed test setup for the air spring. The air

spring was tested under harmonic excitation with amplitudes of 4 mm, 6 mm, 8 mm, and 10 mm; frequencies of 1 Hz, 2 Hz, 3 Hz, and 4 Hz; and air pressures of 0.2 MPa, 0.3 MPa, and 0.4 MPa. The air pressure was supplied by an air compressor (EV-65, Xiamen East Asia Machinery Industrial Co., Ltd., Xiamen, China).

![Figure 2: (a) Schematic of the performance-testing system showing a 6-DOF vibration platform, a steel column, clamps, an MR damper, a displacement sensor, a force sensor, and a steel angle. (b) Detailed test setup for the MR damper showing the damper connected to a DC power supply. (c) Detailed test setup for the air spring showing the air spring connected to an air compressor.](0e62b4ac2303ba5f3ff10123a7c0f273_img.jpg)

Figure 2 consists of three parts: (a) a schematic diagram of the performance-testing system, (b) a photograph of the detailed test setup for the MR damper, and (c) a photograph of the detailed test setup for the air spring. Part (a) shows a 6-DOF vibration platform supporting a steel angle, which is connected to a force sensor and a displacement sensor. The steel angle is also connected to a steel column via clamps. An MR damper is also shown connected to the steel angle. Part (b) shows a photograph of the MR damper setup, where the damper is connected to a DC power supply. Part (c) shows a photograph of the air spring setup, where the air spring is connected to an air compressor.

Figure 2: (a) Schematic of the performance-testing system showing a 6-DOF vibration platform, a steel column, clamps, an MR damper, a displacement sensor, a force sensor, and a steel angle. (b) Detailed test setup for the MR damper showing the damper connected to a DC power supply. (c) Detailed test setup for the air spring showing the air spring connected to an air compressor.

**Figure 2.** (a) Performance-testing system. (b) Detailed test setup for the MR damper. (c) Detailed test setup for the air spring.

#### 2.2.1. MR Damper

The MR damper employed in this study comprises a piston rod, a casing, a piston head, a coil, MR fluid, and an accumulator. As illustrated in Figure 3, the casing was fully filled with MR fluid and divided into upper and lower chambers by the piston head. The accumulator, containing nitrogen gas, compensates for volumetric changes during piston movement. Operating in flow mode, the MR damper generates substantial damping forces even under small-stroke conditions. When external loads act on the piston rod, MR fluid through the channel in the piston head. A coil integrated into the piston head is energized with direct current to generate a magnetic field, which induces magnetic flux across the channel, as indicated by the red dashed lines in Figure 3. This flux alters the rheological properties of the MR fluid in the channel, enabling precise control of the damping force. The designed MR seat damper has the following specifications: cylinder's inner diameter, 46 mm; outer diameter of the piston assembly (including the piston ring sleeve and outer shell), 46 mm; outer diameter of the piston components, 38 mm; outer diameter of the piston rod, 16 mm; number of coil turns, 80; diameter of the coil, 0.5 mm; orifice gap, 2 mm; orifice length, 33 mm; and total height of the piston with upper and lower pressure plates, 49.75 mm.

Figure 4 presents the experimental results for the MR damper, which showed significant nonlinear behavior and dependencies on all excitation amplitudes, frequencies, and input currents. Figure 4a,b depict the force-displacement and force-velocity characteristics at a frequency of 2 Hz, a current of 0.8 A, and different displacement levels. The area enclosed by the force-displacement curve and the force level grow with the excitation amplitude, indicating higher energy dissipation capabilities. Figure 4c,d illustrate the

force–displacement and force–velocity characteristics at an amplitude of 4 mm, a current of 0.4 A, and different frequency levels. The maximum damping force rises as the frequency increases. Figure 4e,f illustrate the force–displacement and force–velocity characteristics at an amplitude of 8 mm, a frequency of 2 Hz, and varying current levels. When the current is 0 A, the maximum damping force is 216.61 N; when the current increases to 2 A, the maximum damping force reaches 1151.91 N, amounting to an increase of 431.79%. This indicates that the MR damper has a wide damping force adjustment range. Moreover, it can be gleaned from the figure that the increase in the maximum damping force from 1.6 A to 2.0 A is minimal, indicating that when the current surpasses 1.6 A, the magnetic field strength produced by the electromagnetic coil nears magnetic saturation, leading to a decrease in the damping force increment for the MR damper.

![Figure 3: Schematic configuration of the MR damper. The diagram shows a cross-section of the damper with labels: Bottom block, MR fluid, Coil, Casing, Nitrogen, Floating piston, Piston head, and Piston rod. Red dashed lines indicate the direction of the magnetic flux within the coil.](c1c7af7ea36be0323047962df57d75b0_img.jpg)

Figure 3: Schematic configuration of the MR damper. The diagram shows a cross-section of the damper with labels: Bottom block, MR fluid, Coil, Casing, Nitrogen, Floating piston, Piston head, and Piston rod. Red dashed lines indicate the direction of the magnetic flux within the coil.

**Figure 3.** Schematic configuration of the MR damper. The red dashed lines represent the direction of the magnetic flux. This explanation is explained in the 1st paragraph of Section 2.2.1.

![Figure 4: Experimental results of the MR damper. Six subplots (a-f) show force-displacement and force-velocity curves. (a) and (b) show force-displacement curves for amplitudes of 4mm, 8mm, 12mm, and 16mm. (c) and (d) show force-displacement and force-velocity curves for frequencies of 1Hz, 2Hz, 3Hz, and 4Hz. (e) and (f) show force-displacement and force-velocity curves for currents of 0A, 0.4A, 0.8A, 1.2A, 1.6A, and 2.0A.](4279c8be6ec4ed56f4b3349be98bb426_img.jpg)

Figure 4: Experimental results of the MR damper. Six subplots (a-f) show force-displacement and force-velocity curves. (a) and (b) show force-displacement curves for amplitudes of 4mm, 8mm, 12mm, and 16mm. (c) and (d) show force-displacement and force-velocity curves for frequencies of 1Hz, 2Hz, 3Hz, and 4Hz. (e) and (f) show force-displacement and force-velocity curves for currents of 0A, 0.4A, 0.8A, 1.2A, 1.6A, and 2.0A.

**Figure 4.** Experimental results of the MR damper. (a,b) the force–displacement and force–velocity curves under varying displacements. (c,d) the force–displacement and force–velocity curves under varying frequencies. (e,f) the force–displacement and force–velocity curves under varying currents.

To facilitate simulation and controller design, the hyperbolic tangent model [34] was adopted to describe the behaviors of the MR damper. This model is advantageous because it has fewer parameters, allows easy identification, and can capture the hysteresis and dual-viscosity characteristics of an MR damper. The model can be expressed as follows:

$$F_d = \alpha_1 \tanh(\alpha_3(\dot{x}_d + kx)) + \alpha_2(\dot{x}_d + kx_d) + f_0 \quad (5)$$

where  $f_0$  is the damper force offset,  $k = V_0 / X_0$  (where  $V_0$  and  $X_0$  are the critical velocity and critical displacement at  $F_d = 0$ ),  $\alpha_1$  is the shear stress,  $\alpha_2$  and  $\alpha_3$  are parameters associated with the damping coefficients of the pre-yield and post-yield zones, and  $x_d$  and  $\dot{x}_d$  are the axial relative displacement and axial relative velocity of the damper, respectively.

Based on the experimental results, the genetic algorithm in MATLAB 2022b was used to identify the parameters of the hyperbolic tangent model. Due to their insensitivity, the mean values of the parameters  $\alpha_3$ ,  $k$ , and  $f_0$  were used for analysis. The other parameters were linearly fitted, with  $\alpha_1 = k_1 I + b_1$ , and  $\alpha_2 = k_2 I + b_2$ . For the subsequent simulations and tests, the random excitation amplitude averaged 8 mm, and the resonance frequency of seat suspension was around 2 Hz. Thus, experimental results with an amplitude of 8 mm and a frequency of 2 Hz were chosen for fitting. The results of parameter identification are provided in Table 2, and the curve-fitting results are shown in Figure 5 as dashed lines. The good agreement between the results from modelling and testing validates the accuracy of the adopted hyperbolic tangent model.

**Table 2.** Identification results for the hyperbolic tangent model.

| Parameters | Value | Parameters | Value |
|------------|-------|------------|-------|
| $b_1$      | 100   | $k$        | 3     |
| $b_2$      | 1.8   | $k_1$      | 0.1   |
| $\alpha_3$ | 0.03  | $k_2$      | 0.05  |
| $f_0$      | 5     | N/A        | N/A   |

![Figure 5: Experimental and fitted responses of the MR damper. (a) Force-displacement curve showing Force (N) vs Displacement (mm) for various current levels (0A, 0.4A, 0.8A, 1.2A, 1.6A, 2.0A). (b) Force-velocity curve showing Force (N) vs Velocity (mm/s) for the same current levels. Both plots compare experimental data (solid lines) with fitted model results (dashed lines).](27b22513fc27a0ff5f230b062ad3112f_img.jpg)

Figure 5: Experimental and fitted responses of the MR damper. (a) Force-displacement curve showing Force (N) vs Displacement (mm) for various current levels (0A, 0.4A, 0.8A, 1.2A, 1.6A, 2.0A). (b) Force-velocity curve showing Force (N) vs Velocity (mm/s) for the same current levels. Both plots compare experimental data (solid lines) with fitted model results (dashed lines).

**Figure 5.** Experimental and fitted responses of the MR damper. (a) Force-displacement curve. (b) Force-velocity curve.

In semi-active control systems, the controller processes vibration inputs and system responses to determine the required damping force; however, the MR damper requires a specific control current  $I$  to generate this force. Thus, an inverse model that maps the desired control force to the corresponding current is essential for controller design. This model compensates for the nonlinear hysteresis and dynamic dependencies of dampers. Based on the hyperbolic tangent model and the current-dependent variation in its parameters, the inverse model of the damper can be derived as follows.

Substituting  $\alpha_1$  and  $\alpha_2$  into Equation (5) yields

$$F_d = (k_1 I + b_1) \tanh(\alpha_3(\dot{x}_d + kx_d)) + (k_2 I + b_2)(\dot{x}_d + kx_d) + f_0 \quad (6)$$

Let  $m = \tanh(\alpha_3(\dot{x}_d + kx_d))$ , and  $n = \dot{x}_d + kx_d$ . Then, Formula (2) becomes

$$F_d = (k_1 I + b_1)m + (k_2 I + b_2)n + f_0 \quad (7)$$

so

$$I = \frac{F_d - b_1 m - b_2 n - f_0}{m k_1 + n k_2} \quad (8)$$

To validate the precision of the hyperbolic tangent inverse model, a joint simulation was performed, as illustrated in Figure 6. Identical excitation conditions and current were applied to the hyperbolic tangent model and its inverse model, with the output force of the hyperbolic tangent model serving as the input for the inverse model to derive the expected current  $\tilde{I}$ . The expected current was subsequently fed back into the hyperbolic tangent model to generate the expected damping force  $\tilde{F}_d$ . The input current was compared and analyzed against the expected current, and the input damping force was compared and analyzed against the expected damping force.

![Figure 6: Simulation framework for the hyperbolic tangent inverse model's fitting accuracy. The diagram shows a flow of signals between three main blocks: 'Hyperbolic tangent model' (orange box), 'Hyperbolic tangent inverse model' (blue box), and another 'Hyperbolic tangent model' (orange box). Inputs to the first orange box are motion states x_d and x_dot_d, and current I. Its output is damping force F_d, which goes to the blue box. The blue box outputs the expected current I_tilde, which goes to the second orange box. The second orange box outputs the expected damping force F_d_tilde. A feedback loop also exists from the second orange box back to the first orange box.](367926125450c2bc3f4bdca9d59a62ba_img.jpg)

Figure 6: Simulation framework for the hyperbolic tangent inverse model's fitting accuracy. The diagram shows a flow of signals between three main blocks: 'Hyperbolic tangent model' (orange box), 'Hyperbolic tangent inverse model' (blue box), and another 'Hyperbolic tangent model' (orange box). Inputs to the first orange box are motion states x\_d and x\_dot\_d, and current I. Its output is damping force F\_d, which goes to the blue box. The blue box outputs the expected current I\_tilde, which goes to the second orange box. The second orange box outputs the expected damping force F\_d\_tilde. A feedback loop also exists from the second orange box back to the first orange box.

**Figure 6.** Simulation framework for the hyperbolic tangent inverse model's fitting accuracy. The orange boxes in the figure represent the hyperbolic tangent model, while the blue boxes denote the inverse hyperbolic tangent model, with arrows indicating signal transmission of motion states, current, and damping force.

Figure 7 presents the inverse model's fitting results for sinusoidal current variations in the range of 0–2 A. Figure 7a illustrates the current fitting results, demonstrating a strong agreement between the input current and the expected current. Figure 7b depicts the damping force fitting results, showing a close match between the input damping force and the expected damping force. The results demonstrate that the driving current obtained from the hyperbolic tangent inverse model can effectively regulate the output of the MR damper.

![Figure 7: (a) Current fitting results and (b) Damping force fitting results. Both plots show sinusoidal signals over a 5-second period. Plot (a) shows 'Current (A)' on the y-axis ranging from -0.4 to 2.4, with 'Applied current' (solid line) and 'Desired current' (dashed line) overlapping. Plot (b) shows 'Force (N)' on the y-axis ranging from -800 to 1200, with 'Applied damping force' (solid line) and 'Desired damping force' (dashed line) overlapping.](0d5fdb87a392819c7d2e3b6230912a0b_img.jpg)

Figure 7: (a) Current fitting results and (b) Damping force fitting results. Both plots show sinusoidal signals over a 5-second period. Plot (a) shows 'Current (A)' on the y-axis ranging from -0.4 to 2.4, with 'Applied current' (solid line) and 'Desired current' (dashed line) overlapping. Plot (b) shows 'Force (N)' on the y-axis ranging from -800 to 1200, with 'Applied damping force' (solid line) and 'Desired damping force' (dashed line) overlapping.

**Figure 7.** (a) The current fitting results. (b) The damping force fitting results.

#### 2.2.2. Air Spring

The air spring employed in this research had an initial length of 75 mm and an effective area of 5500 mm<sup>2</sup>. Figure 8 presents the experimental results pertaining to the air spring. Figure 8a illustrates the force–displacement curve at a frequency of 2 Hz, an air pressure of 0.3 MPa, and different amplitudes. It is evident that the spring force grows with the excitation amplitude, while the spring's stiffness remains constant. Figure 8b depicts the force–displacement curve at an amplitude of 8 mm, an air pressure of 0.3 MPa, and

different frequencies. It is clear that the spring force shows little variation with frequency, indicating that the influence of frequency on spring force is negligible. Figure 8c illustrates the force–displacement curve at an amplitude of 8 mm, a frequency of 2 Hz, and different air pressures. It is evident that the spring's stiffness and spring force rise markedly as the air pressure increases. From the aforementioned characteristics of the air spring, it is clear that the air spring demonstrates significant nonlinear behavior. The spring's stiffness depends solely on the air pressure, whereas the spring force is influenced by both the excitation amplitude and air pressure.

![Figure 8: Experimental results pertaining to the air spring. (a) Force-displacement under varying displacements (4mm, 6mm, 8mm, 10mm). (b) Force-displacement under varying frequencies (1Hz, 2Hz, 3Hz, 4Hz). (c) Force-displacement under varying air pressure (0.2MPa, 0.3MPa, 0.4MPa).](f519a5be118c846f631c992412353fb9_img.jpg)

Figure 8 consists of three subplots (a), (b), and (c) showing Force (N) versus Displacement (mm).  
 (a) Force-displacement under varying displacements: Curves for 4mm, 6mm, 8mm, and 10mm show increasing stiffness and force with displacement.  
 (b) Force-displacement under varying frequencies: Curves for 1Hz, 2Hz, 3Hz, and 4Hz are nearly identical, showing minimal frequency dependence.  
 (c) Force-displacement under varying air pressure: Curves for 0.2MPa, 0.3MPa, and 0.4MPa show that stiffness and force increase significantly with air pressure.

Figure 8: Experimental results pertaining to the air spring. (a) Force-displacement under varying displacements (4mm, 6mm, 8mm, 10mm). (b) Force-displacement under varying frequencies (1Hz, 2Hz, 3Hz, 4Hz). (c) Force-displacement under varying air pressure (0.2MPa, 0.3MPa, 0.4MPa).

**Figure 8.** Experimental results pertaining to the air spring. (a) the force–displacement under varying displacements. (b) the force–displacement under varying frequencies. (c) the force–displacement under varying air pressure.

For the subsequent theoretical simulations and tests, the random excitation amplitude averaged 8 mm, and the resonance frequency of the seat suspension was around 2 Hz, and an air pressure of 0.3 MPa was applied to maintain fixed stiffness. Thus, the experimental data at an amplitude of 8 mm, a frequency of 2 Hz, and an air pressure of 0.3 MPa were chosen for fitting to develop a theoretical mathematical model of the air spring. Based on the measured force–displacement characteristics, a modified Kelvin–Voigt model [35] was used to describe the behaviors of the air spring. The model can be expressed as follows:

$$F_s = K_1 x_s + K_2 x_s^2 + K_3 x_s^3 + K_4 + C_r \dot{x}_s \quad (9)$$

where  $x_s$  and  $\dot{x}_s$  are the axial relative displacement and axial relative velocity of the air spring, respectively. Using a genetic algorithm, the mechanical parameters were obtained:  $K_1 = 68.9$  kN/m,  $K_2 = 50.1$  kN/m,  $K_3 = 8782.4$  kN/m,  $K_4 = -35$  kN/m, and  $C_r = 500$  Ns/m. Figure 9 shows the close agreement between the experimental and fitted results, confirming the accuracy of the model.

![Figure 9: Experimental and fitted responses of the air spring. The plot shows Force (N) versus Displacement (mm). The experimental data (solid red line) and simulation (dashed red line) are nearly identical, showing a cubic-like relationship.](df476ed6ad0bb890c67aa63e7647d071_img.jpg)

Figure 9 is a plot of Force (N) versus Displacement (mm). The x-axis ranges from -8 to 8 mm, and the y-axis ranges from -800 to 800 N. The plot compares experimental data (solid red line) and simulation results (dashed red line). The two lines are nearly identical, showing a cubic-like relationship where force increases with displacement, with a noticeable inflection point around zero displacement.

Figure 9: Experimental and fitted responses of the air spring. The plot shows Force (N) versus Displacement (mm). The experimental data (solid red line) and simulation (dashed red line) are nearly identical, showing a cubic-like relationship.

**Figure 9.** Experimental and fitted responses of the air spring.



# 3. Design of a Semi-Active Control System

This Section presents the design of a semi-active control system for an MR-damper-based seat suspension system, addressing challenges relating to time delays, parameter uncertainties, and nonlinear hysteresis. The control framework, illustrated in Figure 10, integrates five core components: the controlled seat suspension system, which models the physical dynamics of the seat; a reference model combining high-pass and low-pass filters to balance ride comfort and stability, where the high-pass filter attenuates high-frequency vibrations critical for ride comfort, and the low-pass filter suppresses low-frequency oscillations essential for stability; an adaptive backstepping controller that dynamically adapts to disturbances, including driver mass variations, through real-time parameter adaptation; a time-delay compensator that mitigates delays arising from signal processing and actuator response; and an MR damper inverse model, which translates the force command from the controller into the precise control current required to achieve the desired damping force, accounting for the hysteresis and velocity-dependent behavior of the damper. Simulations under harmonic, bump-related, and random excitations validate the effectiveness in enhancing vibration isolation and stability across diverse operating conditions. The control process is initiated by feeding the displacement error  $e_1$  (between the actual response  $x_1$  of the seat system and the ideal trajectory  $x_{1r}$  of the reference model) into the virtual controller and ABC-C controller. The ideal velocity reference trajectory  $x_2^d$  of the virtual controller, combined with the error  $e_2$  between the seat response velocity  $\dot{x}_2$  and a historical control input integral term  $\theta \int_{t-\tau}^{t} u(s) ds$ , is fed into the mass parameter estimator  $\hat{\theta}(t)$  to generate adaptive parameters for the ABC-C controller. The optimal control force  $u(t)$  from the ABC-C controller is partially routed to a delay module, where the generated delayed control force signal simulates actuator time delays. Simultaneously, the control force is input into an inverse MR damper model, converting it into control current  $i$  applied to the MR damper for seat suspension vibration control.

![Schematic diagram of semi-active control frame. The diagram shows a control loop with several interconnected blocks. A blue dashed box on the left contains the 'Adaptive Backstepping Controller with time-delay compensation', which includes a 'Projection Adaptive Law' and an 'Active Control Force' block. The 'Projection Adaptive Law' outputs an estimate $\hat{\theta}(t) = 1/M(t)$. The 'Active Control Force' block outputs the control force $u(t)$. The $u(t)$ signal is fed into a 'Delay' block and an 'MRD inverse model' block. The 'Delay' block outputs $u(t-\tau)$. The 'MRD inverse model' block is defined by the equation $I = \frac{F_d - b_1 m - b_2 n}{m k_1 + n k_2}$. The output of the 'MRD inverse model' is the control current $i$. The $u(t)$ signal is also fed into an integral block $\theta \int_{t-\tau}^{t} u(s) ds$. The output of this integral block is added to the delayed signal $u(t-\tau)$ to produce the seat response velocity $\dot{x}_2$. The seat response velocity $\dot{x}_2$ and the control current $i$ are fed into a 'Seat suspension' block (green dashed box), which outputs the seat displacement $x_1$. The displacement $x_1$ is compared with the reference displacement $x_{1r}$ (from the 'Model-reference System' block, which contains a 'High-pass filter' and a 'Low-pass filter') to produce the displacement error $e_1$. The displacement error $e_1$ is fed into a 'Virtual Controller' block and the 'Adaptive Backstepping Controller'. The 'Virtual Controller' also receives the control current $i$ and produces the ideal velocity reference trajectory $x_2^d$. The seat response velocity $\dot{x}_2$ and the ideal velocity reference trajectory $x_2^d$ are compared to produce the velocity error $e_2$. The velocity error $e_2$ is fed into a mass parameter estimator block $\hat{\theta}(t) = r(-F_{se} - F_{de} + u(t))e_2$. The output of this block is fed back into the 'Adaptive Backstepping Controller'.](d26959f4514c26ca19c3d6f00da85956_img.jpg)

Schematic diagram of semi-active control frame. The diagram shows a control loop with several interconnected blocks. A blue dashed box on the left contains the 'Adaptive Backstepping Controller with time-delay compensation', which includes a 'Projection Adaptive Law' and an 'Active Control Force' block. The 'Projection Adaptive Law' outputs an estimate \$\hat{\theta}(t) = 1/M(t)\$. The 'Active Control Force' block outputs the control force \$u(t)\$. The \$u(t)\$ signal is fed into a 'Delay' block and an 'MRD inverse model' block. The 'Delay' block outputs \$u(t-\tau)\$. The 'MRD inverse model' block is defined by the equation \$I = \frac{F\_d - b\_1 m - b\_2 n}{m k\_1 + n k\_2}\$. The output of the 'MRD inverse model' is the control current \$i\$. The \$u(t)\$ signal is also fed into an integral block \$\theta \int\_{t-\tau}^{t} u(s) ds\$. The output of this integral block is added to the delayed signal \$u(t-\tau)\$ to produce the seat response velocity \$\dot{x}\_2\$. The seat response velocity \$\dot{x}\_2\$ and the control current \$i\$ are fed into a 'Seat suspension' block (green dashed box), which outputs the seat displacement \$x\_1\$. The displacement \$x\_1\$ is compared with the reference displacement \$x\_{1r}\$ (from the 'Model-reference System' block, which contains a 'High-pass filter' and a 'Low-pass filter') to produce the displacement error \$e\_1\$. The displacement error \$e\_1\$ is fed into a 'Virtual Controller' block and the 'Adaptive Backstepping Controller'. The 'Virtual Controller' also receives the control current \$i\$ and produces the ideal velocity reference trajectory \$x\_2^d\$. The seat response velocity \$\dot{x}\_2\$ and the ideal velocity reference trajectory \$x\_2^d\$ are compared to produce the velocity error \$e\_2\$. The velocity error \$e\_2\$ is fed into a mass parameter estimator block \$\hat{\theta}(t) = r(-F\_{se} - F\_{de} + u(t))e\_2\$. The output of this block is fed back into the 'Adaptive Backstepping Controller'.

**Figure 10.** Schematic diagram of semi-active control frame. The blue dashed box in the figure represents the adaptive backstepping controller with experimental compensator; The purple dashed box indicates the inverse model of the MR damper; The orange dashed box shows the reference model system; The green dashed box demonstrates the seat suspension system. Arrows illustrate signal transmission of system states, reference model states and errors.

## 3.1. Reference Model Design

This Section details the design of a reference model for generating ideal trajectories for driver mass displacement and vertical velocity, ensuring a balance between ride comfort and stability. The reference model incorporates a performance function that adapts to road disturbances while maintaining stability through Lyapunov analysis.

The reference state vector  $x_r$  is defined as  $[x_{1r}, x_{2r}]$ . Then, the filter performance function is adopted. The performance function  $J_1(t)$  is formulated as follows [36]:

$$J_1(t) = W_1 x_{1r}(t) + W_2(x_{1r}(t) - z(t)) \quad (10)$$

The transfer functions of these filters are defined as follows:

$$W_1 = \frac{s}{s + \varepsilon_{10} + c_1 f_1(x_{1r}(t) - z(t))} \quad (11)$$

$$W_2 = \frac{\varepsilon_{20} + c_2 f_2(x_{1r}(t) - z(t))}{s + \varepsilon_{20} + c_1 f_1(x_{1r}(t) - z(t))} \quad (12)$$

where  $W_1$  represents a high-pass filter, while  $W_2$  denotes a low-pass filter.  $f_1(x_{1r}(t) - z(t))$  and  $f_2(x_{1r}(t) - z(t))$  are nonlinear functions used to adapt the cutoff frequency of the filters according to the relative displacement of the seat suspension system. They are defined as follows:

$$f_1(x_{1r}(t) - z(t)) = \begin{cases} \left( \frac{x_{1r}(t) - z(t) - l_1}{l_2} \right)^3 & x_{1r}(t) - z(t) > l_1 \\ 0 & |x_{1r}(t) - z(t)| \le l_1 \\ -\left( \frac{x_{1r}(t) - z(t) + l_1}{l_2} \right)^3 & x_{1r}(t) - z(t) < -l_1 \end{cases} \quad (13)$$

$$f_2(x_{1r}(t) - z(t)) = \begin{cases} \left( \frac{x_{1r}(t) - z(t) - n_1}{n_2} \right)^3 & x_{1r}(t) - z(t) > n_1 \\ 0 & |x_{1r}(t) - z(t)| \le n_1 \\ -\left( \frac{x_{1r}(t) - z(t) + n_1}{n_2} \right)^3 & x_{1r}(t) - z(t) < -n_1 \end{cases} \quad (14)$$

where  $c_1$  and  $c_2$  are positive constants.  $\varepsilon_{10}$  and  $\varepsilon_{20}$  are the design parameters of the high-pass filter and low-pass filter, respectively.  $l_1$ ,  $l_2$ ,  $n_1$ , and  $n_2$  are positive constants satisfying  $l_1 > n_1$ . When the relative displacement of seat suspension is large, the cutoff frequency of the high-pass filter increases to minimize the transmission of low-frequency vibrations, improving comfort, while the cutoff frequency of the low-pass filter decreases to reduce high-frequency vibration transmission, enhancing stability. When the relative displacement of seat suspension is small, the cutoff frequency of the high-pass filter decreases to permit more low-frequency vibrations, improving stability, while the cutoff frequency of the low-pass filter increases to allow more high-frequency vibrations, enhancing comfort.

Next, the backstepping adaptive control technique is adopted to minimize  $J_1$ . The second performance function  $J_2(t)$  is defined as follows:

$$J_2(t) = x_{2r}(t) - x_{2r}^d(t) \quad (15)$$

The expected velocity of the reference model  $x_{2r}^d(t)$  can be calculated as follows:

$$x_{2r}^d(t) = -d_1 J_1 + \varepsilon_1 y_1(t) - \varepsilon_2(x_{1r}(t) - z_r(t) - y_2(t)) \quad (16)$$

where  $d_1$  is a positive constant.  $y_1 = W_1 x_{1r}(t)$ ,  $y_2 = W_2(x_{1r}(t) - z(t))$ ,  $\varepsilon_1 = \varepsilon_{10} + c_1 f_1(x_{1r}(t) - z(t))$ , and  $\varepsilon_2 = \varepsilon_{20} + c_1 f_1(x_{1r}(t) - z(t))$ .

Considering the Lyapunov functional candidate below,

$$V(J_1, J_2) = \frac{1}{2}J_1^2(t) + \frac{1}{2}J_2^2(t) \quad (17)$$

by taking the derivative of Equation (17), one can obtain

$$\dot{V}(J_1, J_2) = J_1(t)\dot{J}_1(t) + J_2(t)\dot{J}_2(t) \quad (18)$$

where

$$\begin{cases} \dot{J}_1(t) = x_{2r}(t) - \varepsilon_1 y_1(t) + \varepsilon_1(x_{1r}(t) - z(t) - y_2(t)) \\ \dot{J}_2(t) = -\frac{1}{M_s(t)}(F_{se}(x, z, \dot{x}, \dot{z}, t) + F_{de}(\dot{x}, \dot{z}, t) - u_m(t)) - \dot{x}_{2r}^d(t) \end{cases} \quad (19)$$

The control input function  $u_m(t)$  is designed in the following manner:

$$u_m(t) = -M(t)d_2J_2(t) - M(t)J_1(t) + F_{se}(x, z, \dot{x}, \dot{z}, t) + F_{de}(\dot{x}, \dot{z}, t) + M(t)\dot{x}_{2r}^d(t) \quad (20)$$

where  $d_2$  is a positive constant. Substituting (20) into (19) yields, Equation (19) can be rewritten as

$$\begin{cases} \dot{J}_1(t) = -d_1J_1(t) + J_2(t) \\ \dot{J}_2(t) = -d_2J_2(t) - J_1(t) \end{cases} \quad (21)$$

Then, the Lyapunov functional candidate can be defined as follows:

$$\dot{V}(J_1, J_2) = -d_1J_1^2(t) - d_2J_2^2(t) < 0 \quad (22)$$

Since  $V(J_1, J_2)$  is positive-definite while  $\dot{V}(J_1, J_2)$  is negative,  $J_1(t)$  and  $J_2(t)$  will achieve global asymptotic stability; i.e., when  $t \to \infty$ ,  $J_1(t) \to 0$ ,  $J_2(t) \to 0$ . In summary, the reference model inputs the designed control force  $u_m(t)$  into the seat suspension system to generate ideal displacement and velocity reference trajectories. By minimizing the errors between the displacement and velocity of the seat suspension system under ABC-C control and the ideal reference trajectories, excellent control performance can be achieved.

## 3.2. Adaptive Backstepping Tracking Controller Design

This Section presents the design and stability analysis of an adaptive backstepping controller with a compensator (ABC-C) for a semi-active seat suspension system. The ABC-C controller ensures precise tracking of the trajectories of the reference model while compensating for time delays and parameter uncertainties (e.g., driver mass variations). The design process is structured into two phases: (1) the derivation of the control input and adaptive laws and the introduction of a time delay compensator, and (2) a Lyapunov-based stability analysis.

In the first step, the objective is to derive the control input  $u(t)$  and the adaptive control law  $\hat{\theta}(t)$ . Time-delay is unavoidable in a real-world control system, so the control capacity of the controlled seat suspension system will be affected. At this point, compensation is needed. The tracking error between the vertical displacement of the seat system  $x_1(t)$  and the ideal vertical displacement of the reference model  $x_{1r}(t)$  is defined as  $e_1(t) = x_1(t) - x_{1r}(t)$ . If  $e_1(t)$  tends to be zero,  $x_1(t)$  can track the reference trajectory  $x_{1r}(t)$  more accurately. The vertical motion of the control object is defined below:

$$\begin{cases} \dot{x}_1(t) = x_2(t) \\ \dot{x}_2(t) = \theta(t)(-F_{se}(x, z, \dot{x}, \dot{z}, t) - F_{de}(\dot{x}, \dot{z}, t) + u(t - \tau)) \end{cases} \quad (23)$$

where the uncertain parameter  $\theta(t) = \frac{1}{M} \in [\theta_{\min}, \theta_{\max}]$   $\theta_{\min} = \frac{1}{M_{\max}}$  and  $\theta_{\max} = \frac{1}{M_{\min}}$ .

By taking the derivative of  $e_1(t)$ , one will find that

$$\dot{e}_1(t) = x_2(t) - \dot{x}_{1r}(t) \quad (24)$$

Similarly, a compensator is designed by defining the error between the reference trajectory  $x_2^d(t)$ , the virtual control input  $x_2(t)$  in (24), and the integration of the historical control input  $\theta \int_{t-\tau}^t u(s) ds$ , as shown below:

$$e_2(t) = x_2(t) - x_2^d(t) + \theta \int_{t-\tau}^t u(s) ds \quad (25)$$

Substituting Equation (25) into Equation (24) yields

$$\dot{e}_1(t) = e_2(t) + x_2^d(t) - \dot{x}_{1r}(t) - \theta \int_{t-\tau}^t u(s) ds \quad (26)$$

By taking the derivative of  $e_2(t)$ , one arrives at

$$\begin{aligned} \dot{e}_2(t) &= \theta(t)(-F_{se}(x, z, \dot{x}, \dot{z}, t) - F_{de}(\dot{x}, \dot{z}, t) + u(t - \tau)) - x_2^d(t) + \theta[u(t) - u(t - \tau)] \\ &= \theta(t)[-F_{se}(x, z, \dot{x}, \dot{z}, t) - F_{de}(\dot{x}, \dot{z}, t) + u(t)] - x_2^d(t) \end{aligned} \quad (27)$$

Next,  $x_2^d(t)$  is defined as follows:

$$x_2^d(t) = \dot{x}_{1r}(t) - k_1 e_1(t) \quad (28)$$

where  $k_1$  is a positive constant. To achieve the control objectives,  $u(t)$  is designed in the following manner:

$$u(t) = \frac{1}{\hat{\theta}(t)}(x_2^d - k_2 e_2(t) - e_1(t)) + F_{se}(z_s, z_r, \dot{z}_s, \dot{z}_r, t) + F_{de}(\dot{z}_s, \dot{z}_r, t) \quad (29)$$

where  $k_2$  is a positive constant and  $\hat{\theta}(t)$  is the estimation value of  $\theta(t)$ . The adaptive control law based on the *proj.* operator is designed in the following manner [26]:

$$\hat{\theta}(t) = \text{Projection}_{\hat{\theta}(t)}(r\tau(t)) \quad (30)$$

where  $r > 0$  is the tuning parameter for the adaptive control law and  $\tau(t) = (-F_s(z_s, z_r, \dot{z}_s, \dot{z}_r, t) - F_d(\dot{z}_s, \dot{z}_r, t) + u(t))e_2(t)$ .

The *proj.* operator  $\text{Projection}_{\hat{\theta}(t)}(r\tau(t))$  is given by the following equation:

$$\text{Projection}_{\hat{\theta}(t)}(r\tau(t)) = \begin{cases} 0, & \text{if } \hat{\theta}(t) = \theta_{\max} \text{ and } r\tau(t) > 0 \\ 0, & \text{if } \hat{\theta}(t) = \theta_{\min} \text{ and } r\tau(t) < 0 \\ r\tau(t), & \text{otherwise} \end{cases} \quad (31)$$

In the second step, a stability analysis of the designed controller is conducted to prove the global asymptotic stability of the closed-loop system. Toward this end, the Lyapunov function must be defined as follows:

$$V = \frac{1}{2}e_1^2(t) + \frac{1}{2}e_2^2(t) + \frac{1}{2}\left(\int_{t-\tau}^t u(s) ds\right)^2 + \frac{1}{2}r^{-1}\tilde{\theta}^2(t) \quad (32)$$

where  $\tilde{\theta}(t) = \hat{\theta}(t) + \theta(t)$ . For any  $\zeta > 0$ , a set  $A$  is always a compact set:

$$A = \left\{ e, \int_{t-\tau}^t u(s) ds, \tilde{\theta} : v \le \zeta \right\} \quad (33)$$

In a compact set  $A$ ,  $\left\| \int_{t-\tau}^{t} u(s) ds \right\|$  has a maximum value. Given that  $u(t)$  is continuous,  $\|u(t) - u(t - \tau)\|$  also has a maximum value. In addition, considering the perfect nature of the square, it can be expressed as follows:

$$e_1 \int_{t-\tau}^{t} u(s) ds \le e_1^2 + \frac{1}{4} \left( \int_{t-\tau}^{t} u(s) ds \right)^2 \quad (34a)$$

$$(u(t) - u(t - \tau)) \int_{t-\tau}^{t} u(s) ds \le \left( \int_{t-\tau}^{t} u(s) ds \right)^2 + \frac{1}{4} [u(t) - u(t - \tau)]^2 \quad (34b)$$

After taking the derivative of  $V$  and substituting it into Equations (27)–(31), one obtains

$$\begin{aligned} \dot{V} &= e_1 \dot{e}_1 + e_2 \dot{e}_2 + \theta [u(t) - u(t - \tau)] \int_{t-\tau}^{t} u(s) ds + r^{-1} \hat{\theta} \hat{\theta} \\ &= -k_1 e_1^2 - k_2 e_2^2 - e_1 \theta \int_{t-\tau}^{t} u(s) ds + \theta [u(t) - u(t - \tau)] \int_{t-\tau}^{t} u(s) ds \\ &\le -(k_1 - \theta) e_1^2 - k_2 e_2^2 + 2\theta \left( \int_{t-\tau}^{t} u(s) ds \right)^2 + \alpha \end{aligned} \quad (35)$$

where  $\alpha = \frac{1}{4} [u(t) - u(t - \tau)]^2$ . As can be seen from Equation (35), if

$$\lambda = \min\{k_1 - \theta_{\max}, k_2, -2\theta_{\max}, 0\} \quad (36)$$

it can be formulated as

$$\dot{V} \le -2\lambda v + \alpha \quad (37)$$

to obtain

$$V(t) \le \frac{\alpha}{2\lambda} + \left( v(0) - \frac{\alpha}{2\lambda} \right) e^{-2\lambda t} \quad (38)$$

According to Equation (38), when  $t \to \infty$ ,  $e_1(t)$ ,  $e_2(t)$ , and  $\int_{t-\tau}^{t} u(s) ds$  have a boundary. By inputting the ideal control force computed through the semi-active controller into the inverse model of the MR damper, the control current, and subsequently the semi-active control law, can thus be determined as follows:

$$I = \begin{cases} I_{\max} & I > I_{\max} \\ I & 0 < I < I_{\max} \\ 0 & \text{else} \end{cases} \quad (39)$$

where  $I$  is the calculated control current, and  $I_{\max}$  is the maximum current output of the MR damper, which is 2A.

## 3.3. Numerical Simulation Results and Analysis

Numerical simulations were conducted in MATLAB/Simulink to evaluate the performance of the MR seat suspension system under harmonic, bumpy, and random road excitation conditions. The following controller parameters were selected:  $r = 0.001$ ,  $k_1 = k_2 = 10$ ,  $\theta_{\min} = 1/50\text{kg}$ ,  $\theta_{\max} = 1/110\text{kg}$ , and  $\hat{\theta}(t) = 80$ . The reference model parameters were set to  $l_1 = 0.05$ ,  $l_2 = 0.03$ ,  $n_1 = 0.005$ ,  $n_2 = 0.02$ ,  $d_1 = d_2 = 200$ ,  $c_1 = 0.02$ ,  $c_2 = 0.1$ ,  $\varepsilon_{10} = 1\text{ Hz}$ , and  $\varepsilon_{20} = 2\text{ Hz}$ . Four control strategies were compared to validate the effectiveness of damping variability:

- (1) Passive control—conventional seat suspension with constant damping, with  $I = 0\text{ A}$ .
- (2) Skyhook control—classical on-off logic is used to regulate damping forces.
- (3) Adaptive backstepping control (ABC)—control forces are adjusted in real-time based on passenger mass variations, but time delays are neglected.
- (4) ABC-C control—ABC is enhanced by incorporating a time-delay compensator for improved system stability.

### 3.3.1. Simulation of Harmonic Excitation

A frequency sweep test was conducted on the seat suspension system, and the results are shown in Figure 11. Figure 11a shows the sweep excitation with a displacement of  $\pm 8$  mm and a frequency range of 0.1–5 Hz. Figure 11b presents the excitation acceleration and response (for the seat's upper plate) acceleration. Figure 11c shows the results of a frequency domain analysis of the response acceleration, revealing that the seat suspension system's resonance frequency is approximately 2 Hz. Therefore, a 2 Hz harmonic excitation was selected for simulation and testing.

![Figure 11: (a) Sweep signal showing displacement (mm) vs time (s). (b) Comparison between excitation acceleration and response acceleration vs time (s). (c) Response acceleration in the frequency domain showing amplitude (m/s²) vs frequency (Hz) with a peak at (2.03, 0.21).](e95f47f7a4c01c8889d6d46919b4c73d_img.jpg)

Figure 11 consists of three subplots. Subplot (a) shows Displacement (mm) on the y-axis ranging from -10 to 10, and time (s) on the x-axis ranging from 0 to 50. The signal is a high-frequency sine wave with an amplitude of 8 mm. Subplot (b) shows Acceleration (m/s²) on the y-axis ranging from -10 to 10, and time (s) on the x-axis ranging from 0 to 50. It compares Excitation acceleration (black line) and Response acceleration (red line). The response acceleration is significantly lower in amplitude than the excitation acceleration. Subplot (c) shows Amplitude (m/s²) on the y-axis ranging from 0.00 to 0.25, and Frequency (Hz) on the x-axis ranging from 0 to 50. The curve shows a sharp peak at approximately 2.03 Hz with an amplitude of 0.21 m/s², marked by a red dot and a red line indicating the value (2.03, 0.21).

Figure 11: (a) Sweep signal showing displacement (mm) vs time (s). (b) Comparison between excitation acceleration and response acceleration vs time (s). (c) Response acceleration in the frequency domain showing amplitude (m/s²) vs frequency (Hz) with a peak at (2.03, 0.21).

**Figure 11.** (a) Sweep signal. (b) Comparison between excitation acceleration and response acceleration. (c) Response acceleration in the frequency domain. Red dots in the figure mark the peaks of the curve, with its value indicated by red lines.

The results of the simulation under harmonic excitation conditions are presented in Figure 12. As shown in Figure 12a,b, the acceleration and relative displacement amplitude under ABC-C control were significantly reduced, by 67.21% and 63.11%, respectively, compared to the passive case. This is a good trade-off between ride comfort and stability. To illustrate the time-delay phenomenon, the peak acceleration moment at  $t = 2.22$  s of the passive suspension was selected for analysis (marked by the red dashed box in Figure 12a). Figure 12d displays a magnified view of the 2.18–2.28 s time interval with the time delay explicitly marked. The results show that at the peak acceleration moment ( $t = 2.22$  s), the ABC-C control current had already reached its maximum in advance, while the ABC control current exhibited a 40 ms lag and was still in its rising phase, indicating significant lag in ABC control and demonstrating that ABC-C control can achieve advanced current

application through time-delay compensation. Compared to ABC control, the acceleration and displacement amplitudes of ABC-C control are 20.67% and 31.93% lower, respectively. This improvement is attributed to the time-delay compensation mechanism in the ABC-C control system.

![Figure 12: Harmonic excitation simulation results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). (d) Control current (magnified view) vs Time (s), showing a 40ms time delay between Skyhook and ABC-C.](fed39b841ae2dce01088b84bfc1e2789_img.jpg)

Figure 12 consists of four subplots (a, b, c, d) showing simulation results for harmonic excitation. The legend for all plots is: Passive (grey), Skyhook (green), ABC (blue), and ABC-C (red).

- (a) Seat acceleration (m/s²) vs Time (s). The y-axis ranges from -4 to 4, and the x-axis from 0 to 5. All four control methods show periodic oscillations. ABC-C (red) has the lowest amplitude.
- (b) Seat relative displacement (mm) vs Time (s). The y-axis ranges from -10 to 10, and the x-axis from 0 to 5. ABC-C (red) shows the smallest displacement peaks.
- (c) Command current (A) vs Time (s). The y-axis ranges from 0 to 2, and the x-axis from 0 to 5. Skyhook (green) shows high-frequency switching between 0 and 2A. ABC (blue) and ABC-C (red) show lower, more continuous current levels.
- (d) Control current (magnified view) vs Time (s). The y-axis ranges from 0 to 2, and the x-axis from 5.18 to 5.28. This plot shows the initial response of the control systems. A 40ms time delay is indicated between the start of the ABC-C (red) and ABC (blue) current responses.

Figure 12: Harmonic excitation simulation results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). (d) Control current (magnified view) vs Time (s), showing a 40ms time delay between Skyhook and ABC-C.

**Figure 12.** Harmonic excitation simulation results. (a) Seat acceleration. (b) Seat relative displacement. (c) Command current. (d) Control current (magnified view). The bidirectional arrows in the figure are used to indicate the time delay of control input.

### 3.3.2. Simulation of Bump Excitation

Impact excitation simulations were performed to assess the instantaneous dynamic response characteristics of the seat suspension system. The simulated excitation signal shown in Figure 13 was derived from experimentally acquired vehicle speed bump traversal data. The figure shows that the 1.38–1.78 s period corresponds to the vehicle crossing the speed bump. The simulation results are presented in Figure 14. Figure 14a,b demonstrate that ABC-C control exhibits significantly smaller oscillation amplitudes than passive control. The current command profiles in Figure 14c reveal a fixed 2A current output of skyhook control before and after crossing the speed bump. During these periods, the seat response velocity aligns with relative velocity direction, requiring maximum damping force output for stability. When crossing the speed bump, skyhook control employs switching strategies to rapidly adjust current based on seat state changes for vibration attenuation. The ABC and ABC-C control systems generate larger and denser current outputs during bump crossing to stabilize the seat while maintaining lower current levels otherwise. The peak-to-peak data in Table 3 confirm that ABC-C control demonstrates superior performance compared to all the other control systems. Compared with passive control, acceleration decreased by 37.54%, and relative displacement reduced by 27.22%. Compared with ABC control, acceleration and relative displacement decreased by 8.72% and 10.99%, respectively.

![Figure 13: (a) Displacement of bump excitation. (b) Acceleration of bump excitation. Both plots show time (s) on the x-axis from 0 to 4. Plot (a) shows Displacement (mm) from -2 to 2. Plot (b) shows Acceleration (m/s²) from -4 to 6.](b6750d26d3dd287a4a4d49b3670a44bd_img.jpg)

Figure 13: (a) Displacement of bump excitation. (b) Acceleration of bump excitation. Both plots show time (s) on the x-axis from 0 to 4. Plot (a) shows Displacement (mm) from -2 to 2. Plot (b) shows Acceleration (m/s²) from -4 to 6.

**Figure 13.** (a) Displacement of bump excitation. (b) Acceleration of bump excitation.

![Figure 14: Bump excitation simulation results. (a) Seat acceleration. (b) Seat relative displacement. (c) Command current. All plots show time (s) on the x-axis from 0.0 to 4.0. Plot (a) shows Acceleration (m/s²) from -1 to 2. Plot (b) shows Displacement (mm) from -4 to 8. Plot (c) shows Current (A) from 0 to 2. Each plot compares four control methods: Passive (black), Skyhook (green), ABC (blue), and ABC-C (red).](ef25c3cf1fdb334fc8679e85ab5265ca_img.jpg)

Figure 14: Bump excitation simulation results. (a) Seat acceleration. (b) Seat relative displacement. (c) Command current. All plots show time (s) on the x-axis from 0.0 to 4.0. Plot (a) shows Acceleration (m/s²) from -1 to 2. Plot (b) shows Displacement (mm) from -4 to 8. Plot (c) shows Current (A) from 0 to 2. Each plot compares four control methods: Passive (black), Skyhook (green), ABC (blue), and ABC-C (red).

**Figure 14.** Bump excitation simulation results. (a) Seat acceleration. (b) Seat relative displacement. (c) Command current.

**Table 3.** Peak-to-peak data for four kinds of control methods during the simulation.

|                                            | Passive | Skyhook | ABC    | ABC-C  |
|--------------------------------------------|---------|---------|--------|--------|
| Peak-to-peak acceleration                  | 2.85    | 2.14    | 1.95   | 1.78   |
| Acceleration reduction proportion          | NA      | 24.91%  | 31.57% | 37.54% |
| Peak-to-peak relative displacement         | 18.38   | 7.12    | 9.01   | 8.02   |
| Relative displacement reduction proportion | NA      | 35.39%  | 18.24% | 27.22% |

### 3.3.3. Simulation of Random Road Excitation

The comprehensive performance of the seat suspension system was finally evaluated through a random excitation simulation. We adopted ISO 7096 [37] to generate random road excitation (Figure 15a), which is specifically applicable to seat vibration testing for engineering vehicles and can effectively evaluate seat suspension damping performance. Figure 15b,c illustrate the time-domain analysis results for seat acceleration and relative displacement. The results demonstrate that the skyhook, ABC, and ABC-C control systems effectively reduce vibrations, with ABC-C control achieving the best vibration suppression. Figure 15d displays the command current. In contrast to skyhook, the command current of the ABC-C control system peaks when there are large vibration amplitudes in order to deliver adequate damping force for vibration reduction, but it remains at a lower

level when there are small vibration amplitudes. This indicates that the applied current should be adjusted based on the intensity of the vibration. The frequency-domain results regarding seat acceleration in Figure 15e reveal that the dominant vibration frequency is 2 Hz. Compared to the passive seat suspension system, ABC-C control decreases the seat acceleration amplitude at this frequency by 62%, further demonstrating its superior performance in comparison to all the other control strategies.

![Figure 15: Random excitation simulation results. (a) Displacement excitation: Displacement (mm) vs Time (s). (b) Seat acceleration: Acceleration (m/s²) vs Time (s). (c) Seat relative displacement: Displacement (mm) vs Time (s). (d) Command current: Current (A) vs Time (s). (e) Seat acceleration in the frequency domain: Amplitude (m/s²) vs Frequency (Hz). All plots compare Passive (black), Skyhook (green), ABC (blue), and ABC-C (red) control strategies.](1c427123350e0e73e2a109b79069314b_img.jpg)

Figure 15 consists of five subplots (a) through (e) showing simulation results for a seat suspension system under random excitation. The x-axis for all plots is Time (s) from 0 to 14.

- (a) Displacement excitation: The y-axis is Displacement (mm) ranging from -10 to 10. The plot shows a high-frequency, low-amplitude signal.
- (b) Seat acceleration: The y-axis is Acceleration (m/s²) ranging from -6 to 6. The plot shows a high-frequency signal with a legend: Passive (black), Skyhook (green), ABC (blue), and ABC-C (red).
- (c) Seat relative displacement: The y-axis is Displacement (mm) ranging from -10 to 20. The plot shows a high-frequency signal with a legend: Passive (black), Skyhook (green), ABC (blue), and ABC-C (red).
- (d) Command current: The y-axis is Current (A) ranging from 0 to 2. The plot shows a high-frequency signal with a legend: Skyhook (green), ABC (blue), and ABC-C (red).
- (e) Seat acceleration in the frequency domain: The y-axis is Amplitude (m/s²) ranging from 0.0 to 1.0, and the x-axis is Frequency (Hz) ranging from 0 to 20. The plot shows a sharp peak at 2 Hz for the Passive system, which is significantly reduced for the other systems. The legend is: Passive (black), Skyhook (green), ABC (blue), and ABC-C (red).

Figure 15: Random excitation simulation results. (a) Displacement excitation: Displacement (mm) vs Time (s). (b) Seat acceleration: Acceleration (m/s²) vs Time (s). (c) Seat relative displacement: Displacement (mm) vs Time (s). (d) Command current: Current (A) vs Time (s). (e) Seat acceleration in the frequency domain: Amplitude (m/s²) vs Frequency (Hz). All plots compare Passive (black), Skyhook (green), ABC (blue), and ABC-C (red) control strategies.

**Figure 15.** Random excitation simulation results. (a) Displacement excitation. (b) Seat acceleration. (c) Seat relative displacement. (d) Command current. (e) Seat acceleration in the frequency domain.

We utilized the ISO 2631-1 [38] standard to assess seat suspension comfort, wherein the frequency-weighted root mean square (FW-RMS) of seat acceleration was used to evaluate the ride comfort. Furthermore, the VDV, a metric more sensitive to peak acceleration, was incorporated into the evaluation framework. Additionally, the root mean square value of the relative displacement (RMS-rd) of the seat suspension system was used as a stability indicator to assess its performance. The evaluation was based on three metrics, namely, FW-RMS, VDV, and RMS-rd, for which lower values signify superior vibration damping performance of the seat suspension system. The results depicted in Figure 16 indicate that the ABC-C control system, denoted by the red bar, yielded the smallest magnitudes for all the evaluation metrics. In comparison to the passive seat suspension system, the ABC-C control system had a 48.6% lower FW-RMS, a 62.3% lower VDV, and a 56.69% lower RMS-rd. Compared to ABC control, ABC-C control achieved a 31.52% lower FW-RMS, a 35.14% lower VDV, and a 20.5% lower RMS-rd. The results conclusively show that ABC-C, through time delay compensation, significantly enhanced the vibration performance of the seat suspension system, markedly reducing both seat acceleration and relative displacement, thereby effectively balancing ride comfort and stability.

To study the impact of load mass variation on the seat suspension system, simulations were conducted with four different masses under the three signal types. The adaptability of the ABC-C controller to mass changes was validated through comparison with passive control. The results are recorded in Table 4. It was observed that, in passive seat suspension

systems, as the mass increases, seat acceleration decreases, potentially causing vehicle instability. Under ABC-C control, the seat acceleration remains relatively constant as the mass increases. This demonstrates that the adaptive backstepping method can adjust the control force output based on load mass changes, enabling the system to adapt to external disturbances and maintain efficient and robust vibration control performance.

![Bar chart showing performance comparison based on simulation results. The Y-axis is Magnitude (0 to 5) and the X-axis is Evaluation index (FW-RMS, VDV, RMS-rd). Four methods are compared: Passive (dark grey), Skyhook (green), ABC (blue), and ABC-C (red).](9260ae281f6b6470331f4a0f82dbc2b1_img.jpg)

| Evaluation index | Passive | Skyhook | ABC  | ABC-C |
|------------------|---------|---------|------|-------|
| FW-RMS           | 1.07    | 1.04    | 0.84 | 0.55  |
| VDV              | 3.82    | 2.72    | 2.22 | 1.44  |
| RMS-rd           | 5.01    | 3.49    | 2.73 | 2.17  |

Bar chart showing performance comparison based on simulation results. The Y-axis is Magnitude (0 to 5) and the X-axis is Evaluation index (FW-RMS, VDV, RMS-rd). Four methods are compared: Passive (dark grey), Skyhook (green), ABC (blue), and ABC-C (red).

**Figure 16.** Performance comparison based on the simulation results.

**Table 4.** Simulation results for seat suspension performance evaluation indicators under varying loads.

| Signal Type         | Control Methods | Acceleration Response at Varying Load Mass ( $\text{m/s}^2$ ) |        |        |        |
|---------------------|-----------------|---------------------------------------------------------------|--------|--------|--------|
|                     |                 | 50 kg                                                         | 70 kg  | 90 kg  | 110 kg |
| Harmonic (Peak)     | Passive         | 1.48                                                          | 1.25   | 1.01   | 0.96   |
|                     | ABC-C           | 0.98                                                          | 0.98   | 0.97   | 0.96   |
| Bump (Peak-to-peak) | Passive         | 3.05                                                          | 2.86   | 2.54   | 2.48   |
|                     | ABC-C           | 1.77                                                          | 1.78   | 1.81   | 1.79   |
| Random road (RMS)   | Passive         | 1.5663                                                        | 1.5006 | 1.4862 | 1.4739 |
|                     | ABC-C           | 0.7863                                                        | 0.7854 | 0.7869 | 0.7760 |

# 4. Experiments

This Section presents an experimental validation of the effectiveness of the proposed control algorithm through seat suspension tests. Firstly, a vibration test system for the seat suspension was established. Subsequently, the time delay parameters for the time delay compensator were measured experimentally. Lastly, harmonic, bump, and random excitations were employed to validate the performance of the control algorithm under various operating conditions.

## 4.1. Testing Setup

A schematic diagram of the experimental setup is shown in Figure 17. A 6-DOF vibration platform was employed to generate vertical vibration excitations. One acceleration sensor (819-10, Senter Tech Development Co., Ltd., Shenzhen, China) installed on the upper plate of the seat was used to measure the response acceleration of the seat. A 60 kg dummy model was placed on the upper plate to provide load mass (the following tests under three working conditions were conducted using this mass). Another acceleration sensor (819-50, Senter Tech Development Co., Ltd., Shenzhen, China) installed on the lower plate of the seat was used to measure the excitation acceleration. A displacement sensor placed 

between the upper and lower plates was used to measure the relative displacement of the suspension system. These signals were collected by the Speedgoat system and transmitted to the control algorithm on the computer. The control algorithm outputs control commands in real-time. The control commands are then transmitted by the Speedgoat system to the OPA549 power amplifier module. This module converts the commands into a control current, driving the MR damper to achieve semi-active control.

![Figure 17: Vibration test system applied to the seat suspension system. The diagram shows a physical setup with a seat on a suspension system. Red arrows point to physical entities: a Displacement sensor, an Acceleration sensor, and an OPA549 module. Green arrows indicate the signal acquisition process: from the sensors to the Speedgoat system, and from the Speedgoat system to the Computer. Blue arrows show the control command application process: from the Computer to the Speedgoat system, and from the Speedgoat system to the OPA549 module, which then provides Current to the suspension system.](79e1709a7317ead45379cbb8ff3ba802_img.jpg)

Figure 17: Vibration test system applied to the seat suspension system. The diagram shows a physical setup with a seat on a suspension system. Red arrows point to physical entities: a Displacement sensor, an Acceleration sensor, and an OPA549 module. Green arrows indicate the signal acquisition process: from the sensors to the Speedgoat system, and from the Speedgoat system to the Computer. Blue arrows show the control command application process: from the Computer to the Speedgoat system, and from the Speedgoat system to the OPA549 module, which then provides Current to the suspension system.

**Figure 17.** Vibration test system applied to the seat suspension system. Red arrows represent physical entities, green arrows indicate the signal acquisition process, blue arrows show the control command application process.

## 4.2. Determination of Time Delay Parameters

To ensure accurate real-time control, the inherent time delay of a system must be quantified prior to experimental validation. This subsection details the methodology for measuring and optimizing the delay parameter for the ABC-C system. A 2 Hz harmonic excitation was applied to the system, simulating a baseline vibration scenario. The time delay between control signal generation and its physical effect on the MR damper was measured. For example, a measured delay of 0.48 s results in the control signal being applied 20 ms earlier in the subsequent vibration cycle to offset the lag. Figure 18 demonstrates that when the control signal is delayed by 0.46 s (i.e., it is applied 40 ms earlier), the acceleration and displacement of the upper plate of the seat suspension system are minimized. Thus, the time delay parameter in the ABC-C controller was set as  $\tau = 40\text{ms}$ .

![Figure 18: Seat suspension response at varying delay times. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). Each plot shows four sinusoidal waveforms for different delay times: delay=0.50s (black), delay=0.48s (green), delay=0.46s (blue), and delay=0.44s (red). The delay=0.46s case shows the smallest amplitude for acceleration and displacement, and the lowest current peaks.](812b773680b611c18d49243e102b895a_img.jpg)

Figure 18: Seat suspension response at varying delay times. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). Each plot shows four sinusoidal waveforms for different delay times: delay=0.50s (black), delay=0.48s (green), delay=0.46s (blue), and delay=0.44s (red). The delay=0.46s case shows the smallest amplitude for acceleration and displacement, and the lowest current peaks.

**Figure 18.** Seat suspension response at varying delay times. (a) Seat acceleration. (b) Seat displacement. (c) Command current.

## 4.3. Experiment Results

### 4.3.1. Harmonic Excitation Test

Experimental validation at a resonant frequency of 2 Hz with a 10 mm excitation amplitude confirmed simulation consistency. Figure 19a,b show that compared to passive control, ABC-C control reduced the vibration amplitudes of acceleration and relative displacement by 31.28% and 27.61%, respectively. Figure 19c shows that ABC-C control maintained high current levels for longer durations compared to ABC control. Compared with ABC control, ABC-C control achieved an additional attenuation of 21.11% in acceleration and 11.01% in relative displacement. The findings indicate that a persistently elevated current improves seat dynamics, yet matching the command current of the skyhook control system's duration threshold could deteriorate control performance.

![Figure 19: Harmonic excitation test results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). All plots compare Passive (black), Skyhook (green), ABC (blue), and ABC-C (red) control strategies over a 5-second period.](0add961f6fd54a7ae5391d00c7e58f3c_img.jpg)

Figure 19 consists of three vertically stacked subplots, (a), (b), and (c), each showing a time-series plot from 0 to 5 seconds. All subplots compare four control strategies: Passive (black line), Skyhook (green line), ABC (blue line), and ABC-C (red line).  
 (a) Acceleration (m/s²): The y-axis ranges from -3 to 3. The Passive control shows the largest amplitude oscillations, while ABC-C shows the smallest. The legend indicates: Passive (black), Skyhook (green), ABC (blue), ABC-C (red).  
 (b) Displacement (mm): The y-axis ranges from -8 to 12. The Passive control shows the largest amplitude oscillations, while ABC-C shows the smallest. The legend indicates: Passive (black), Skyhook (green), ABC (blue), ABC-C (red).  
 (c) Current (A): The y-axis ranges from 0.0 to 2.5. The Skyhook control (green) shows a constant current of approximately 2.0 A. The ABC control (blue) shows a current that drops to 0.0 A during the negative half-cycles of the displacement. The ABC-C control (red) shows a current that remains high, around 2.0 A, during the negative half-cycles. The legend indicates: Skyhook (green), ABC (blue), ABC-C (red).

Figure 19: Harmonic excitation test results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). All plots compare Passive (black), Skyhook (green), ABC (blue), and ABC-C (red) control strategies over a 5-second period.

**Figure 19.** Harmonic excitation test results. (a) Seat acceleration. (b) Seat relative displacement. (c) Command current.

### 4.3.2. Road Bump Excitation Test

The impact excitation applied in the tests matched the configuration shown in Figure 13. The test results are presented in Figure 20. Figure 20a,b demonstrate that ABC and ABC-C controllers achieved lower seat acceleration amplitudes and reduced relative displacements compared to the passive and skyhook control strategies. The peak-to-peak data are summarized in Table 5. The ABC-C controller exhibited a mere 7.77% reduction in maximum interpeak acceleration and a 2.23% decrease in relative displacement compared to the conventional ABC control. The transient characteristics of the bump excitation likely compromised the performance of the ABC-C time-delay compensation mechanism. As evidenced by the command currents in Figure 20c, ABC-C and ABC exhibited nearly overlapping current profiles during the 7.31–7.65 s interval, though ABC-C maintained marginally higher current levels. However, compared with passive control, ABC-C achieved significant reductions of 35.76% in acceleration and 16.70% in relative displacement. This comprehensive evaluation confirms the superior performance of the ABC-C controller.

![Figure 20: Bump excitation test results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). The figure compares four control methods: Passive (grey), Skyhook (green), ABC (blue), and ABC-C (red).](9b5411fa2d169b66f6185fbf67b49766_img.jpg)

Figure 20 consists of three vertically stacked subplots, (a), (b), and (c), each showing a time-series plot from 7.0 to 8.0 seconds. Subplot (a) shows Acceleration in m/s², ranging from -2 to 3. Subplot (b) shows Displacement in mm, ranging from -12 to 8. Subplot (c) shows Current in A, ranging from 0 to 2. Each plot contains four data series: Passive (grey line), Skyhook (green line), ABC (blue line), and ABC-C (red line). In (a), all series show similar oscillations, with ABC-C showing slightly lower peaks. In (b), the Passive series shows the largest displacement peaks, while ABC-C shows the smallest. In (c), the command current is a step function that increases in discrete steps, with ABC-C showing the highest current values.

Figure 20: Bump excitation test results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). The figure compares four control methods: Passive (grey), Skyhook (green), ABC (blue), and ABC-C (red).

**Figure 20.** Bump excitation test results. (a) Seat acceleration. (b) Seat relative displacement. (c) Command current.

**Table 5.** Peak-to-peak data for four control methods under experimental conditions.

|                                            | Passive | Skyhook | ABC    | ABC-C  |
|--------------------------------------------|---------|---------|--------|--------|
| Peak-to-peak acceleration                  | 4.25    | 3.2     | 2.96   | 2.73   |
| Acceleration reduction proportion          | NA      | 24.71%  | 30.35% | 35.76% |
| Peak-to-peak relative displacement         | 18.38   | 18.01   | 15.66  | 15.31  |
| Relative displacement reduction proportion | NA      | 2.01%   | 14.80% | 16.70% |

### 4.3.3. Random Road Excitation Test

The random excitation displacement applied in the experiment matches that shown in Figure 15a. Figure 21 presents the outcomes of random excitation testing. Figure 21a,b demonstrate a comparison of the performance regarding seat acceleration and relative displacement across the four control approaches. The vibration control performance of the seat suspension under various control conditions was evaluated based on FW-RMS, VDV and RMS<sub>rd</sub>, with the results presented in Figure 22. Compared to passive control, ABC-C control achieved reductions of 26.9% in FW-RMS, 29.3% in VDV, and 58.46% in RMS<sub>rd</sub>. In comparison to ABC control, ABC-C control further decreased FW-RMS by 4.39%, VDV by 4.18%, and RMS<sub>rd</sub> by 31.56%.

Figure 21c confirms that the input command current aligns with the simulation analysis, validating the practical feasibility of the theoretical approach. Figure 21d illustrates the frequency-domain results regarding seat acceleration, revealing that the dominant vibration frequency is 2.1 Hz. At this frequency, ABC-C control reduces the seat acceleration amplitude by 60.52% and 25.58% compared to passive and ABC control, respectively. The time-domain and frequency-domain analyses demonstrate that the ABC-C controller achieves significant vibration reduction.

![Figure 21: Random road excitation test results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). (d) Acceleration of the seat in the frequency domain (Amplitude (m/s²)) vs Frequency (Hz).](485c57a6add7e0bd7898009db1179ee6_img.jpg)

Figure 21 consists of four subplots (a, b, c, d) showing the results of a random road excitation test for four control methods: Passive (black), Skyhook (green), ABC (blue), and ABC-C (red).  
 (a) Seat acceleration (m/s²) vs Time (s): The y-axis ranges from -8 to 6 m/s², and the x-axis ranges from 0 to 16 s. All methods show high-frequency oscillations between -4 and 4 m/s², with the Passive method exhibiting slightly higher peaks.  
 (b) Seat relative displacement (mm) vs Time (s): The y-axis ranges from -30 to 20 mm, and the x-axis ranges from 0 to 16 s. The Passive method shows large oscillations between -25 and 15 mm, while the other three methods (Skyhook, ABC, ABC-C) show much smaller oscillations between -5 and 5 mm.  
 (c) Command current (A) vs Time (s): The y-axis ranges from 0 to 2 A, and the x-axis ranges from 0 to 16 s. The Passive method shows a constant current of 2 A. The other three methods show high-frequency oscillations between 0 and 2 A.  
 (d) Acceleration of the seat in the frequency domain (Amplitude (m/s²)) vs Frequency (Hz): The y-axis ranges from 0 to 0.8 m/s², and the x-axis ranges from 0 to 16 Hz. The Passive method has a dominant peak at approximately 2.5 Hz with an amplitude of 0.8 m/s². The other three methods have much lower amplitudes across the frequency range.

Figure 21: Random road excitation test results. (a) Seat acceleration (m/s²) vs Time (s). (b) Seat relative displacement (mm) vs Time (s). (c) Command current (A) vs Time (s). (d) Acceleration of the seat in the frequency domain (Amplitude (m/s²)) vs Frequency (Hz).

**Figure 21.** Random road excitation test results. (a) Seat acceleration. (b) Seat relative displacement. (c) Command current. (d) Acceleration of the seat in the frequency domain.

![Figure 22: Performance comparison based on the test results. A bar chart showing Magnitude vs Evaluation index for Passive, Skyhook, ABC, and ABC-C methods.](06ccd604e7eac77c7a5a323b6a913f15_img.jpg)

Figure 22 is a bar chart comparing the performance of four control methods (Passive, Skyhook, ABC, ABC-C) across three evaluation indices: FW-RMS, VDV, and RMS-rd. The y-axis represents Magnitude from 0 to 5.

| Evaluation index | Passive | Skyhook | ABC  | ABC-C |
|------------------|---------|---------|------|-------|
| FW-RMS           | 1.19    | 0.99    | 0.91 | 0.87  |
| VDV              | 3.72    | 3.22    | 2.63 | 2.52  |
| RMS-rd           | 4.96    | 3.71    | 3.01 | 2.06  |

Figure 22: Performance comparison based on the test results. A bar chart showing Magnitude vs Evaluation index for Passive, Skyhook, ABC, and ABC-C methods.

**Figure 22.** Performance comparison based on the test results.

Given the constraints on the experimental conditions and safety concerns, three masses were chosen to test the adaptability of the proposed ABC-C algorithm to mass changes. The results are documented in Table 6. Aligning with the simulation results, the response acceleration of the passive seat suspension in the experiment rose as the mass increased. With ABC-C control, the seat acceleration stayed relatively stable with an increase in mass across the three signal types. This demonstrates that the proposed adaptive control algorithm can handle external disturbances and ensure the stability of seat suspension systems.

**Table 6.** Test results regarding seat suspension performance evaluation indicators under varying loads.

| Signal Type         | Control Methods | Acceleration Response at Varying Load Mass (m/s <sup>2</sup> ) |        |        |
|---------------------|-----------------|----------------------------------------------------------------|--------|--------|
|                     |                 | 40 kg                                                          | 50 kg  | 60 kg  |
| Harmonic (Peak)     | Passive         | 2.84                                                           | 2.59   | 2.10   |
|                     | ABC-C           | 2.04                                                           | 2.05   | 2.04   |
| Bump (Peak-to-peak) | Passive         | 5.28                                                           | 4.82   | 4.25   |
|                     | ABC-C           | 2.71                                                           | 2.69   | 2.73   |
| Random road (RMS)   | Passive         | 1.268                                                          | 1.258  | 1.248  |
|                     | ABC-C           | 0.8856                                                         | 0.8756 | 0.8923 |

# 5. Conclusions

This study presents the design and validation of an ABC-C controller for an MR-damper-based semi-active seat suspension system. The proposed controller addresses challenges such as vibration isolation, ride comfort, and stability under varying driver masses and system time delays. The key contributions are given below.

- A robust control framework was developed, integrating a reference model, an adaptive backstepping controller, a time-delay compensator, and an MR damper inverse model. The reference model balanced ride comfort and stability, while the adaptive controller ensured robustness against uncertainties.
- The time-delay compensator effectively mitigated delays in the control loop, enhancing system stability. Experimental measurements confirmed its ability to minimize seat acceleration and displacement.
- Simulations and experiments under harmonic, bump, and random excitations demonstrated the superior performance of the ABC-C controller, significantly reducing vibration acceleration and relative displacement.
- The ABC-C controller maintained consistent performance under varying driver masses, ensuring stable suspension behavior across different loading conditions.
- The proposed strategy offers a practical solution for improving ride comfort and stability in commercial-vehicle seat suspension systems, addressing real-world challenges such as system nonlinearities and time delays.

In conclusion, the ABC-C controller represents a significant advancement in semi-active seat suspension systems, providing a robust and adaptive solution for enhancing ride comfort and stability. While improving safety and ride comfort, MR dampers can also extend vehicle service life by reducing undesired mechanical vibrations that cause fatigue of vehicle components. Using MR fluids with excellent biocompatibility to fabricate dampers can further achieve an optimal balance between economic benefits and safety performance. Future work will focus on further optimization and broader application in suspension systems.

**Author Contributions:** Conceptualization, Y.L. and S.L.; methodology and software, H.F. and Y.Z.; validation, H.F., Y.Z., G.C. and S.M.; resources, Y.L. and S.L.; original draft preparation, H.F.; review and editing, S.L.; supervision, Y.L. and S.L.; All authors have read and agreed to the published version of the manuscript.

**Funding:** This research received no external funding.

**Data Availability Statement:** The data is available from the author upon request.

**Conflicts of Interest:** The authors declare that there are no conflicts of interest.

# References

1. Sun, W.; Li, J.; Zhao, Y.; Gao, H. Vibration control for active seat suspension systems via dynamic output feedback with limited frequency characteristic. *Mechatronics* **2011**, *21*, 250–260.
2. Blood, R.P.; Yost, M.G.; Camp, J.E.; Ching, R.P. Whole-body vibration exposure intervention among professional bus and truck drivers: A laboratory evaluation of seat-suspension designs. *J. Occup. Environ. Hyg.* **2015**, *12*, 351–362. [\[CrossRef\]](#) [\[PubMed\]](#)
3. Maciejewski, I.; Meyer, L.; Krzyzynski, T. Modelling and multi-criteria optimisation of passive seat suspension vibro-isolating properties. *J. Sound Vib.* **2009**, *324*, 520–538. [\[CrossRef\]](#)
4. Agharkakli, A.; Sabet, G.S.; Barouz, A. Simulation and analysis of passive and active suspension system using quarter car model for different road profile. *Int. J. Eng. Trends Technol.* **2012**, *3*, 636–644.
5. Ning, D.; Sun, S.; Li, H.; Du, H.; Li, W. Active control of an innovative seat suspension system with acceleration measurement based friction estimation. *J. Sound Vib.* **2016**, *384*, 28–44. [\[CrossRef\]](#)
6. Deng, L.; Sun, S.; Christie, M.; Ning, D.; Jin, S.; Du, H.; Zhang, S.; Li, W. Investigation of a seat suspension installed with compact variable stiffness and damping rotary magnetorheological dampers. *Mech. Syst. Signal Process.* **2022**, *171*, 108802. [\[CrossRef\]](#)
7. Sun, S.; Ning, D.; Yang, J.; Du, H.; Zhang, S.; Li, W. A seat suspension with a rotary magnetorheological damper for heavy duty vehicles. *Smart Mater. Struct.* **2016**, *25*, 105032. [\[CrossRef\]](#)
8. Li, S.; Watterson, P.A.; Li, Y.; Wen, Q.; Li, J. Improved magnetic circuit analysis of a laminated magnetorheological elastomer device featuring both permanent magnets and electromagnets. *Smart Mater. Struct.* **2020**, *29*, 085054.
9. Huang, J.; Li, S.; Zhou, Y.; Xu, T.; Li, Y.; Wang, H.; Wang, S. A heavy-duty magnetorheological fluid mount with flow and squeeze model. *Smart Mater. Struct.* **2021**, *30*, 085012. [\[CrossRef\]](#)
10. Sun, S.; Deng, H.; Li, W.; Du, H.; Ni, Y.Q.; Zhang, J.; Yang, J. Improving the critical speeds of high-speed trains using magnetorheological technology. *Smart Mater. Struct.* **2013**, *22*, 115012. [\[CrossRef\]](#)
11. Li, S.; Liang, Y.; Li, Y.; Li, J.; Zhou, Y. Investigation of dynamic properties of isotropic and anisotropic magnetorheological elastomers with a hybrid magnet shear test rig. *Smart Mater. Struct.* **2020**, *29*, 114001. [\[CrossRef\]](#)
12. Li, S.; Tian, T.; Wang, H.; Li, Y.; Li, J.; Zhou, Y.; Wu, J. Development of a four-parameter phenomenological model for the nonlinear viscoelastic behaviour of magnetorheological gels. *Mater. Des.* **2020**, *194*, 108935. [\[CrossRef\]](#)
13. Li, S.; Li, Y.; Li, J. Thixotropy of magnetorheological gel composites: Experimental testing and modelling. *Compos. Sci. Technol.* **2021**, *214*, 108996.
14. Guo, C.; Gong, X.; Zong, L.; Peng, C.; Xuan, S. Twin-tube-and bypass-containing magneto-rheological damper for use in railway vehicles. *Proc. Inst. Mech. Eng. Part F J. Rail Rapid Transit* **2015**, *229*, 48–57.
15. Dong, X.; Fei, Z.; Zhang, Z.; Deng, X.; Li, P.; Liu, Q. Gray skyhook predictive control of magnetorheological semi-active seat suspension with time delay. *Smart Mater. Struct.* **2023**, *32*, 115010.
16. Liang, Y.; Dong, X.; Ao, W.K.; Ni, Y.-Q. A Novel Application of Magnetorheological Seat Suspension with an Improved Tuning Control Strategy. *Struct. Control Health Monit.* **2023**, *2023*, 3985363.
17. Wu, J.; Zhou, H.; Liu, Z.; Gu, M. A load-dependent PWA-H $\infty$  controller for semi-active suspensions to exploit the performance of MR dampers. *Mech. Syst. Signal Process.* **2019**, *127*, 441–462.
18. McManus, S.; Clair, K.S.; Boileau, P.; Boutin, J.; Rakheja, S. Evaluation of vibration and shock attenuation performance of a suspension seat with a semi-active magnetorheological fluid damper. *J. Sound Vib.* **2002**, *253*, 313–327. [\[CrossRef\]](#)
19. Hiemenz, G.J.; Hu, W.; Wereley, N.M. Semi-active magnetorheological helicopter crew seat suspension for vibration isolation. *J. Aircr.* **2008**, *45*, 945–953.
20. Chen, Q.; Zhang, Y.; Zhu, C.; Wu, J.; Zhuang, Y. A sky-hook sliding mode semiaactive control for commercial truck seat suspension. *J. Vib. Control Eng. Pract.* **2021**, *27*, 1201–1211.
21. Deng, L.; Zhao, J.; Ning, D.; Wong, P.; Zhao, J.; Li, W.; Du, H. *Design of a Dual-Motor Powertrain with Magnetorheological Planetary Transmission for Electric Vehicles*; SAE Technical Paper: Warrendale, PA, USA, 2024.
22. Yao, H.; Fu, J.; Yu, M.; Peng, Y. Semi-active control of seat suspension with MR damper. *J. Phys. Conf. Ser.* **2013**, *412*, 012054. [\[CrossRef\]](#)
23. Shin, D.K.; Phu, D.X.; Choi, S.-M.; Choi, S.-B. An adaptive fuzzy sliding mode control of magneto-rheological seat suspension with human body model. *J. Intell. Mater. Syst. Struct.* **2016**, *27*, 925–934.
24. Dong, X.-m.; Yu, M.; Liao, C.-r.; Chen, W.-m. Comparative research on semi-active control strategies for magneto-rheological suspension. *Nonlinear Dyn.* **2010**, *59*, 433–453.
25. Astolfi, A.; Karagiannis, D.; Ortega, R. *Nonlinear and Adaptive Control with Applications*; Springer: Berlin/Heidelberg, Germany, 2008; Volume 187.
26. Pang, H.; Zhang, X.; Xu, Z. Adaptive backstepping-based tracking control design for nonlinear active suspension system with parameter uncertainties and safety constraints. *ISA Trans.* **2019**, *88*, 23–36.
27. Sun, W.; Gao, H.; Kaynak, O. Adaptive backstepping control for active suspension systems with hard constraints. *IEEE/ASME Trans. Mechatron.* **2012**, *18*, 1072–1079. [\[CrossRef\]](#)

28. Fu, J.; Dai, Z.; Yang, Z.; Lai, J.; Yu, M. Time delay analysis and constant time-delay compensation control for MRE vibration control system with multiple-frequency excitation. *Smart Mater. Struct.* **2019**, *29*, 014001.
29. Zheng, J.; Li, Z.; Koo, J.-H.; Wang, J. Analysis and compensation methods for time delays in an impact buffer system based on magnetorheological dampers. *J. Intell. Mater. Syst. Struct.* **2015**, *26*, 690–700.
30. Du, H.; Zhang, N.; Lam, J. Parameter-dependent input-delayed control of uncertain vehicle suspensions. *J. Sound Vib.* **2008**, *317*, 537–556.
31. El Majdoub, K.; Giri, F.; Chaoui, F.-Z. Adaptive backstepping control design for semi-active suspension of half-vehicle with magnetorheological damper. *IEEE/CAA J. Autom. Sin.* **2020**, *8*, 582–596.
32. Jin, Z.; Liang, Z.; Wang, X.; Zheng, M. Adaptive backstepping sliding mode control of tractor-trailer system with input delay based on RBF neural network. *Int. J. Control Autom. Syst.* **2021**, *19*, 76–87. [\[CrossRef\]](#)
33. Gao, Z.; Wong, P.K.; Zhao, J.; Hua, X.; Ma, X.; Xie, Z. Design of compensatory backstepping controller for nonlinear magnetorheological dampers. *Appl. Math. Model.* **2023**, *114*, 318–337. [\[CrossRef\]](#)
34. Guo, S.; Yang, S.; Pan, C. Dynamic modeling of magnetorheological damper behaviors. *J. Intell. Mater. Syst. Struct.* **2006**, *17*, 3–14.
35. Zhao, L.; Yu, Y.; Zhou, C.; Yang, F. Modelling and validation of a seat suspension with rubber spring for off-road vehicles. *J. Vib. Control* **2018**, *24*, 4110–4121. [\[CrossRef\]](#)
36. Pang, H.; Zhang, X.; Chen, J.; Liu, K. Design of a coordinated adaptive backstepping tracking control for nonlinear uncertain active suspension system. *Appl. Math. Model.* **2019**, *76*, 479–494. [\[CrossRef\]](#)
37. ISO 7096; Earth-Moving Machinery—Laboratory Evaluation of Operator Seat Vibration. International Organization for Standardization: Geneva Switzerland, 2000.
38. ISO 2631-1; Mechanical vibration and Shock—Evaluation of Human Exposure to Whole-Body Vibration—Part 1: General Requirements. International Organization for Standardization: Geneva, Switzerland, 1997.

**Disclaimer/Publisher’s Note:** The statements, opinions and data contained in all publications are solely those of the individual author(s) and contributor(s) and not of MDPI and/or the editor(s). MDPI and/or the editor(s) disclaim responsibility for any injury to people or property resulting from any ideas, methods, instructions or products referred to in the content.