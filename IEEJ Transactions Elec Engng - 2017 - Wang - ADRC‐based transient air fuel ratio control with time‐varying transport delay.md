

# ADRC-Based Transient Air/Fuel Ratio Control with Time-Varying Transport Delay Consideration for Gasoline Engines

Zhijing Wang, Non-member

Xiaohong Jiao<sup>a</sup>, Non-member

This paper presents a fuel injection controller based on the modified active disturbance rejection control (ADRC) algorithm to maintain the air/fuel ratio (AFR) at the stoichiometric value in the presence of a transport time delay. The factors affecting the dynamics of the AFR include the variations of the intake manifold pressure, engine speed, and load torque, as well as uncertain parameters existing in the fuel film evaporation and the oxygen sensor aging, which are viewed as the 'total disturbance' to the AFR system and estimated by the extended state observer (ESO). Thus, based on the Lyapunov–Krasovskii functional stability theory, the ADRC fuel injection controller is designed with the gain matrices of the controller and observer and solved by employing linear matrix inequalities. Considering the time-varying transport delay, a time delay block is added to the ESO. By synchronizing the input signals of the ESO, the performance in terms of the timely compensation for the disturbance is improved. The effectiveness of the proposed control strategy is validated through simulation of a V6 spark ignition engine model developed by the Society of Instrument and Control Engineers (SICE) Research Committee on Advanced Powertrain Control Theory. © 2017 Institute of Electrical Engineers of Japan. Published by John Wiley & Sons, Inc.

**Keywords:** spark ignition engine; air/fuel ratio; active disturbance rejection control; time-varying delay; linear matrix inequality

*Received 19 May 2016; Revised 19 November 2016*

## 1. Introduction

In consideration of energy saving and environmental protection, maintaining the air/fuel ratio (AFR) at the stoichiometric value seems more and more important because of the great influence AFR has on the conversion efficiency of the three-way catalyst and fuel economy of a spark ignition (SI) engine. The main challenges in the precise control of the AFR, especially during the transient operations of the engine, involve the transport time delay in the AFR system, which varies with the switching of engine operations, variations of the intake manifold pressure, engine speed, and load torque, as well as plant uncertainties due to the wall-wetting phenomenon and aging of the universal exhaust gas oxygen (UEGO) sensor.

In view of the impact of the transport time delay on the dynamics of the AFR, several studies have been made. For example, in [1] the internal model control and its application to the AFR control system are presented. This method handles the time delay in the AFR system under the condition that the structure of the plant is already known in the absence of any disturbance to the system. The Smith predictor shown in [2,3] is widely used for time delay, which can remove the time delay from the main loop. But the predictor is available only when the parameters in the model match those in the plant, and the performance may decrease when modeling errors exist. Moreover, other challenges in maintaining the AFR at the stoichiometric value involve the complications in the model construction of the engine and some physicochemical processes such as the air intake [4], fuel delivery, and the combustion. Thus, many algorithms have been proposed to get an appropriate solution, such as the neural network control algorithm applied in [5–7], which can identify the engine model for controlling the AFR. However, this

method definitely requires much training in practice. For reducing the canister purge disturbance, [8] has derived a sliding-mode controller. In [9], to reduce the influence of the uncertainties caused by the wall-wetting phenomenon and the variations of the intake manifold and engine speed, an extended state observer (ESO) was constructed. But the time-varying transport delay in the AFR system, which leads to the deviation of the fuel command, is ignored. As for the parameter uncertainties in the AFR control plant, the adaptive control algorithm is widely employed, typical examples being given in [10–13]. On the basis of the mean value engine model, adaptive fuel injection controllers are derived in [10,11] to remove the influence of the uncertain parts caused by the fuel film evaporation and the system description. Adaptive update laws are derived on the Lyapunov design for the uncertain parameters [12,13]. In [14], to deal with the biofuel parameters, the adaptive algorithm is applied to estimate the biofuel content for internal combustion engines. Taking the time-varying parameters into consideration, [15] applies the switching linear parameter varying (LPV) controller to the AFR control system for managing the dynamics of the fuel path.

In this paper, a modified active disturbance rejection control (ADRC) algorithm for the accurate regulation of the AFR is derived, which can deal with the transport time delay generated from the fuel injection to the AFR measurement and tries to diminish the influence caused by the change of the engine operation and the uncertain parameters in the AFR system. An ESO is designed to estimate the 'total disturbance' that is associated with the unmeasurable air mass flow rate into the cylinder, the uncertainties in the fuel film evaporation process, and the change of the engine torque for the port-injected SI engine. The modified part for the transport delay makes the control signal and the system output to synchronize and removes the time delay from the ESO, thus improving the performance of the estimations. The gain matrices of the ADRC controller and the ESO can be solved by linear matrix inequalities (LMIs), which ensures the stability of the augmented error system.

<sup>a</sup> Correspondence to: Xiaohong Jiao. E-mail: jiaoxh@ysu.edu.cn

School of Electrical Engineering, Yanshan University, Hebei 066004, China

In Section 2, the description of the AFR control problem is presented with the analysis of the AFR dynamics. In Section 3, a fuel injection controller based on the modified ADRD considering the time-varying transport delay for the regulation of the transient AFR is designed. In Section 4, stability analysis of the closed-loop system is presented. The validation of the designed controller on engine simulation developed by the SICE Research Committee on Advanced Powertrain Control Theory is shown in Section 5. Section 6 concludes the paper.

## 2. Problem Description

The architecture of the port-injected SI engine is shown in Fig. 1. The processes of SI engine mainly consist of air intake, fuel delivery, combustion—which provides power for crankshaft rotation and produces the engine torque—and exhaust. After the mixture is discharged, the AFR in the cylinder can be measured by the UEGO located in the exhaust tail pipe.

Generally, AFR represents the ratio of the air and the fuel mass flow into the cylinder. For the design of the fuel injection controller, the equivalent AFR is defined as

$$\lambda_c = \frac{\text{AFR}}{L_{\text{th}}} = \frac{\dot{m}_{\text{ao}}}{L_{\text{th}} \dot{m}_{\text{f}}} \quad (1)$$

where  $\dot{m}_{\text{ao}}$ ,  $\dot{m}_{\text{f}}$  are the air and fuel mass flow rate into the cylinder, respectively, which cannot be measured directly and have complex relationship with the engine operation.  $L_{\text{th}}$  is the stoichiometric value and is defined as  $L_{\text{th}} = 14.67$ . Based on the mean-value engine model,  $\dot{m}_{\text{ao}}$  is mainly affected by the intake manifold pressure  $p_m$  and the engine speed  $\omega_e$ , which can be described as

$$\dot{m}_{\text{ao}} = \frac{\rho_a V_c \eta}{4\pi p_a} p_m \omega_e \quad (2)$$

where  $\rho_a$  is the atmospheric density, and  $p_a$  is the ambient air pressure.  $V_c$  and  $\eta$  denote the total cylinder volume of the engine and the volumetric efficiency, respectively. The dynamics of  $p_m$  and  $\omega_e$  are shown as follows under the assumption of the ideal gas law and the First Law of thermodynamics:

$$\dot{p}_m = \frac{RT_m}{V_m} (\dot{m}_{\text{ai}} - \dot{m}_{\text{ao}}) \quad (3)$$

where  $\dot{m}_{\text{ai}}$  is the air mass flow rate past the throttle plate, which is determined by the throttle opening.  $R$  [J/(kg K)] is the gas constant.  $T_m$  [K] and  $V_m$  [m<sup>3</sup>] are the temperature and volume of the intake manifold, respectively.

$$J \dot{\omega}_e = \frac{\rho_a V_c \eta Q \eta_{\text{f}}}{4\pi p_a} p_m - D \omega_e - T_L \quad (4)$$

![Simplified architecture of the AFR system. The diagram shows a central engine block with a piston and crankshaft. An intake manifold is connected to the engine, with a throttle valve and a sensor for intake air mass flow rate (m_ai) and intake manifold pressure (p_m). A fuel injector is positioned to spray fuel into the intake manifold. The exhaust manifold is connected to the engine and has a Universal Exhaust Gas Oxygen (UEGO) sensor. The ECU (Electronic Control Unit) is connected to the intake manifold, fuel injector, and UEGO sensor to process signals and control the fuel injection command (u_fi). The engine speed (omega_e) is also measured and fed into the ECU.](df2831c8008b5d236f97e4133f08a22a_img.jpg)

Simplified architecture of the AFR system. The diagram shows a central engine block with a piston and crankshaft. An intake manifold is connected to the engine, with a throttle valve and a sensor for intake air mass flow rate (m\_ai) and intake manifold pressure (p\_m). A fuel injector is positioned to spray fuel into the intake manifold. The exhaust manifold is connected to the engine and has a Universal Exhaust Gas Oxygen (UEGO) sensor. The ECU (Electronic Control Unit) is connected to the intake manifold, fuel injector, and UEGO sensor to process signals and control the fuel injection command (u\_fi). The engine speed (omega\_e) is also measured and fed into the ECU.

Fig. 1. Simplified architecture of the AFR system

where  $Q$  is the heat released from the complete combustion of one unit of air,  $\eta_{\text{f}}$  is the engine efficiency per cycle,  $J$  [kg m<sup>2</sup>] is the equivalent inertia of the crankshaft,  $D$  denotes the damping coefficient of the crankshaft, and  $T_L$  [N m] is the load torque.

As for the port-injection engine system, a widely used fuel film dynamic model describing the fuel film evaporation process is as follows:

$$\begin{cases} \dot{m}_{\text{f}} = \epsilon u_{\text{fi}} + \dot{m}_{\text{ff}} \\ \tau_{\text{f}} \dot{m}_{\text{ff}} + \dot{m}_{\text{ff}} = (1 - \epsilon) u_{\text{fi}} \end{cases} \quad (5)$$

where  $u_{\text{fi}}$  is the fuel injection command, and  $\dot{m}_{\text{ff}}$  is the mass flow rate of fuel entering the cylinder from the fuel puddle. The parameters  $\epsilon$  and  $\tau_{\text{f}}$  represent the portion of the fuel entering the cylinder directly as vapor and the time constant of the fuel film evaporation, respectively. The parameters are difficult to obtain, and vary with changing engine operations.

By combining (1)–(5), the dynamic of the AFR in cylinder is derived as

$$\dot{\lambda}_c = b' u_{\text{fi}} + f'(t) \quad (6)$$

$$\text{where } b' = -\frac{L_{\text{th}} \lambda_c^2}{\dot{m}_{\text{ao}} \tau_{\text{f}}},$$

$$f'(t) = -\frac{L_{\text{th}} \lambda_c^2}{\dot{m}_{\text{ao}}} \epsilon u_{\text{fi}} + \frac{RT_m \lambda_c}{V_m p_m} \dot{m}_{\text{ai}} - \frac{RT_m \rho_a V_c \eta}{4V_m \pi p_a} \lambda_c \omega_e + \frac{\lambda_c}{\tau_{\text{f}}} + \frac{\rho_a \eta V_c \eta_{\text{f}} Q \lambda_c p_m}{4\pi p_a J \omega_e} - \frac{\lambda_c D}{J} - \frac{\lambda_c T_L}{J \omega_e}$$

After the exhaust stroke, the AFR will be measured by the UEGO sensor located in the tail pipe of the engine, and its dynamics can be written as

$$\dot{\lambda}_s = -\frac{1}{\tau_s} \lambda_s + \frac{1}{\tau_s} \lambda_c(t - \tau(t)) \quad (7)$$

where  $\lambda_s$  is the measured value, and  $\tau_s$  is the sensor time constant which is affected by sensor aging.

The time delay  $\tau(t)$  in the AFR system is composed of the cycle delay describing the time it takes from the induction stroke to the exhaust stroke and the transport delay showing the elapsed time of the gas reaching the tailpipe UEGO sensor. The total time delay from the fuel injection to the AFR measurement is mainly related to the engine speed and varies with the engine operation. Though the accurate value of the delay cannot be known, it can be approximately estimated as [15]

$$\tau(t) = \frac{60}{N} \left( 1 + \frac{1}{n_{\text{cyl}}} \right) \quad (8)$$

where  $N$  is the engine speed (rpm), and  $n_{\text{cyl}}$  is the number of cylinders in the engine. When the engine operates above the idle speed, obviously  $0 < \tau(t) \le h$  and the maximum value of  $h$  can be obtained.

In the AFR system,  $p_m$ ,  $\omega_e$ ,  $\dot{m}_{\text{ai}}$ , and  $\lambda_s$  can be measured by the sensors installed on the engine, but the air and fuel mass flow rate into the cylinder  $\dot{m}_{\text{ao}}$ ,  $\dot{m}_{\text{f}}$  cannot be measured directly because of the required environment for sensors. The parameters  $\eta$ ,  $\eta_{\text{f}}$ ,  $\epsilon$ ,  $\tau_{\text{f}}$  are unknown and vary when the engine operates in different states.

Combining (7) with (6), the dynamics from the fuel injection command to the measured AFR can be described as

$$\begin{aligned} \ddot{\lambda}_s &= -\frac{1}{\tau_s} \dot{\lambda}_s + \frac{1}{\tau_s} b' u_{\text{fi}}(t - \tau(t)) + \frac{1}{\tau_s} f'(t - \tau(t)) \\ &= b u(t - \tau(t)) + f(t) \end{aligned} \quad (9)$$

with  $f(t) = (-b + b'/\tau_s) u_{\text{fi}}(t - \tau(t)) - \frac{1}{\tau_s} \dot{\lambda}_s + \frac{1}{\tau_s} f'(t - \tau(t))$ . Here,  $u = u_{\text{fi}}$  represents the control input signal, and  $\hat{b}$  is an estimate of the nominal value of the gain  $b'/\tau_s$ .

It should be noted that in the context of ADRC [16],  $f(t)$  in the system (9) can be treated as the total disturbance, which includes not only the external disturbances  $T_L$  but also the unknown internal dynamics resulting from the unmeasurable air mass flow rate into the cylinder, the uncertainties in the fuel film evaporation process, and the change of the engine torque while the engine is operating in the transient state. Then the state vector of the system (9) is defined as  $x = [x_1 \ x_2 \ x_3]^T = [\lambda_s - L_{th} \ \dot{\lambda}_s \ f(t)]^T$ , where  $x_3 = f(t)$  is augmented to the regular design, which is called the extended state representing the total disturbance. The control-oriented system model for the AFR can be obtained as

$$\dot{x} = Ax + bB_1 u(t - \tau(t)) + B_2 \eta \quad (10)$$

with

$$A = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 0 & 0 & 0 \end{bmatrix}, \quad B_1 = \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, \quad B_2 = \begin{bmatrix} 0 \\ 0 \\ 1 \end{bmatrix}, \quad \eta = \dot{f}(t)$$

## 3. Controller Design

To deal with the variable input time delay in the AFR system, a modification is added to the regular ADRC control as shown in Fig. 2. As the measured AFR  $\lambda_s$ , an input signal of the ESO, is delayed by  $\tau(t)$  from the fuel injection command  $u_{fi}$ , the modified part delayed  $u_{fi}$  and synchronized the input signals. Consequently, the time delay is removed from the ESO, improving the performance of the estimations [16].

The ESO for the AFR system (10) can be described as

$$\dot{\hat{x}} = A\hat{x} + B_1 u(t - \tau(t)) + LC(x - \hat{x}) \quad (11)$$

The modified ADRC controller is designed as

$$u = -b^{-1}K(r - \hat{x}) \quad (12)$$

with  $K = [k_1 \ k_2 \ k_3]$ ,  $r = [0 \ 0 \ 0]^T$

By solving the LMI described in (13), the observer gain can be obtained by  $L = P_1^{-1}Q$ . Based on the calculated  $L$  and  $\varepsilon$ , the controller gain  $K$  can be obtained by solving the LMI described in (14):

$$\begin{bmatrix} A^T P_1 + P_1 A - QC - C^T Q^T + \varepsilon I & P_1 \\ * & -\frac{\gamma^2}{2} I \end{bmatrix} < 0 \quad (13)$$

![Block diagram of the Modified ADRC for AFR control system. The system is divided into two main sections: 'Fuel injection controller' and 'SI engine'. The 'Fuel injection controller' section contains an 'ESO' (Extended State Observer) block. The reference signal 'r' is fed into the 'Controller' block. The 'Controller' block outputs the fuel injection command 'u_fi'. This command is fed into the 'ESO' block, which also receives a delayed version of 'u_fi' through a block labeled '-tau(t)'. The 'ESO' block outputs three estimated states: x1-hat, x2-hat, and x3-hat. The 'SI engine' section includes blocks for 'Intake str.', 'Comp str.', 'Expan str.', and 'Exaus str.'. The output of the engine is measured by a 'UEGO' (Universal Exhaust Gas Oxygen) sensor, which provides the measured AFR 'lambda_s'. 'lambda_s' is fed back into the 'ESO' block. The 'ESO' block also receives 'lambda_s' through a block labeled '-tau(t)'. The 'Controller' block also receives 'lambda_s'.](2a16bc72fa4d0150523532baaa0ecfad_img.jpg)

Block diagram of the Modified ADRC for AFR control system. The system is divided into two main sections: 'Fuel injection controller' and 'SI engine'. The 'Fuel injection controller' section contains an 'ESO' (Extended State Observer) block. The reference signal 'r' is fed into the 'Controller' block. The 'Controller' block outputs the fuel injection command 'u\_fi'. This command is fed into the 'ESO' block, which also receives a delayed version of 'u\_fi' through a block labeled '-tau(t)'. The 'ESO' block outputs three estimated states: x1-hat, x2-hat, and x3-hat. The 'SI engine' section includes blocks for 'Intake str.', 'Comp str.', 'Expan str.', and 'Exaus str.'. The output of the engine is measured by a 'UEGO' (Universal Exhaust Gas Oxygen) sensor, which provides the measured AFR 'lambda\_s'. 'lambda\_s' is fed back into the 'ESO' block. The 'ESO' block also receives 'lambda\_s' through a block labeled '-tau(t)'. The 'Controller' block also receives 'lambda\_s'.

Fig. 2. Modified ADRC for AFR control system

$$\begin{bmatrix} \phi & hG & hF & hH \\ * & -hP_2 & 0 & 0 \\ * & * & -hP_2 & 0 \\ * & * & * & -2hP_2 \end{bmatrix} < 0 \quad (14)$$

where  $\phi = \phi_1 + \phi_2 + \phi_2^T$

$$\phi_1 = \begin{bmatrix} W & B_1 K & 2hP_2^{-1} A^T & 0 \\ * & 0 & 2hK^T B_1^T & 0 \\ * & * & -2hP_2^{-1} & 0 \\ * & * & * & -R \end{bmatrix},$$

with

$$W = P_2^{-1} A^T + A P_2^{-1} + T + \frac{1}{2} \bar{P} + \varepsilon^{-1} L C C^T L^T$$

$$T = P_2^{-1} R P_2^{-1}, \bar{P} = P_2^{-1} P_2^{-1}$$

$$\phi_2 = [G + F \quad -G + H \quad 0 \quad -F - H],$$

$$G = \begin{bmatrix} N'_1 \\ N'_2 \\ 0 \\ N_3 \end{bmatrix}, F = \begin{bmatrix} M'_1 \\ M'_2 \\ 0 \\ M_3 \end{bmatrix}, H = \begin{bmatrix} S'_1 \\ S'_2 \\ 0 \\ S_3 \end{bmatrix},$$

$N'_i = P_2^{-1} N_i$ ,  $M'_i = P_2^{-1} M_i$ ,  $S'_i = P_2^{-1} S_i$ .  $P_1, P_2, P_3 \in R^{3 \times 3}$  are all positive symmetric matrices, and  $N_i, M_i, S_i \in R^{3 \times 3} (i = 1, 2, 3)$  are free matrices. \* denotes the symmetric terms in a symmetric matrix. The constant  $\varepsilon > 0$ .  $\gamma$  is the level of interference suppression.

**Remark 1.** It should be noted that instead of setting the controller gain matrix based on some apparent meanings to shape the ideal response [9], both ESO and controller gain matrices of the modified ADRC control applied in this paper are obtained directly by solving the LMIs, ensuring the stability of the augmented system according to the Lyapunov–Krasovskii functional theory.

## 4. Stability Analysis

The stability of the closed-loop system with time-varying delay will be proved by the Lyapunov–Krasovskii functional theory. Considering (10)–(12) and defining  $e = x - \hat{x}$ ,  $z = \hat{x}$  the augmented system can be written as

$$\begin{cases} \dot{e} = (A - LC)e + B_2 \eta \\ \dot{z} = Az + B_1 K z(t - \tau) + LCe \end{cases} \quad (15)$$

In order to analyze the stability of the closed-loop system, a Lyapunov–Krasovskii functional is constructed as

$$V = e^T P_1 e + z^T P_2 z + \int_{t-h}^{t} z^T(s) R z(s) ds + 2 \int_{-h}^{0} \int_{t+\theta}^{t} \dot{z}^T(s) P_2 \dot{z}(s) ds d\theta \quad (16)$$

With the definitions  $z_\tau = z(t - \tau)$ ,  $z_h = z(t - h)$ , the time derivative of  $V$  along the system (15) is derived as

$$\begin{aligned} \dot{V} = & 2e^T P_1 [(A - LC)e + B_2 \eta] + z^T R z - z_h^T R z_h \\ & + 2z^T P_2 (Az + B_1 K z_\tau + LCe) + 2h \dot{z}^T P_2 \dot{z} \\ & - \int_{t-\tau}^{t} \dot{z}^T(s) P_2 \dot{z}(s) ds - \int_{t-h}^{t-\tau} \dot{z}^T(s) P_2 \dot{z}(s) ds \\ & - \int_{t-h}^{t} \dot{z}^T(s) P_2 \dot{z}(s) ds \end{aligned} \quad (17)$$

According to the Newton–Leibniz formula

$$x(t - \tau) - x(t - 2\tau) - \int_{t-\tau}^{t} \dot{x}(s) ds = 0 \quad (18)$$

![Block diagram of the Supplemented V6 engine simulation model. The diagram shows a control loop for engine speed (sa) and fuel injection (fi). Inputs include: 2 (st), 3 (ECU_sa), 4 (ECU_fi), 1 (int_mc), 5 (Tp), 6 (Tv), and 7 (rps). The 'st' signal is converted to 'rad' and multiplied by 'K' to produce 'deg'. This is compared with 'deg_fi' and 'deg_inc' to determine 'fi_req'. The 'ECU_sa' and 'ECU_fi' blocks also contribute to 'sa_req'. The 'int_mc' block feeds into 'MC' and 'fc' blocks. The 'fc' block outputs 'fi' and 'Tp', 'Tv', 'rps' signals. The 'MC' block outputs 'sa' and 'fi'. The 'sa' signal is compared with 'sa_req' to produce an error signal. The 'fi' signal is compared with 'fi_req' to produce an error signal. These error signals are fed into a 'Time delay' block, which then feeds into a 'UEGO' block (AFRc AFRs). The 'UEGO' block outputs 'λs', which is compared with 'λc' to produce 'To'. The 'To' signal is fed back into the 'MC' block. A 'Delay' block is also present in the feedback path.](2fa4a1bf91d0f34e87c689fbc1211fe3_img.jpg)

Block diagram of the Supplemented V6 engine simulation model. The diagram shows a control loop for engine speed (sa) and fuel injection (fi). Inputs include: 2 (st), 3 (ECU\_sa), 4 (ECU\_fi), 1 (int\_mc), 5 (Tp), 6 (Tv), and 7 (rps). The 'st' signal is converted to 'rad' and multiplied by 'K' to produce 'deg'. This is compared with 'deg\_fi' and 'deg\_inc' to determine 'fi\_req'. The 'ECU\_sa' and 'ECU\_fi' blocks also contribute to 'sa\_req'. The 'int\_mc' block feeds into 'MC' and 'fc' blocks. The 'fc' block outputs 'fi' and 'Tp', 'Tv', 'rps' signals. The 'MC' block outputs 'sa' and 'fi'. The 'sa' signal is compared with 'sa\_req' to produce an error signal. The 'fi' signal is compared with 'fi\_req' to produce an error signal. These error signals are fed into a 'Time delay' block, which then feeds into a 'UEGO' block (AFRc AFRs). The 'UEGO' block outputs 'λs', which is compared with 'λc' to produce 'To'. The 'To' signal is fed back into the 'MC' block. A 'Delay' block is also present in the feedback path.

Fig. 3. Supplemented V6 engine simulation model

for any matrix  $N, S, M \in R^{9 \times 3}$ , the following equalities [17] hold:

$$\xi_1^T(t)N(z - z_\tau) = \xi_1^T(t)N \int_{t-\tau}^{t} \dot{z}(s) ds \quad (19)$$

$$\xi_1^T(t)S(z - z_\tau) = \xi_1^T(t)S \int_{t-\tau}^{t} \dot{z}(s) ds \quad (20)$$

$$\xi_1^T(t)M(z - z_\tau) = \xi_1^T(t)M \int_{t-\tau}^{t} \dot{z}(s) ds \quad (21)$$

where

$$N = \begin{bmatrix} N_1 \\ N_2 \\ N_3 \end{bmatrix}, S = \begin{bmatrix} S_1 \\ S_2 \\ S_3 \end{bmatrix}, M = \begin{bmatrix} M_1 \\ M_2 \\ M_3 \end{bmatrix}, \xi_1(t) = \begin{bmatrix} z \\ z_\tau \\ z_h \end{bmatrix}$$

Furthermore, the term  $-\int_{t-\tau}^{t} \dot{z}^T(s)P_2\dot{z}(s) ds$  in (17) can be rewritten as

$$\begin{aligned} & -\int_{t-\tau}^{t} \dot{z}^T(s)P_2\dot{z}(s) ds \\ & = 2\xi_1^T(t)N(z - z_\tau) - \int_{t-\tau}^{t} \dot{z}^T(s) ds - \int_{t-\tau}^{t} \dot{z}^T(s)P_2\dot{z}(s) ds \\ & = 2\xi_1^T(t)N(z - z_\tau) + \int_{t-\tau}^{t} \xi_1^T(t)NP_2^{-1}N^T\xi_1(t) ds \\ & - \int_{t-\tau}^{t} [\xi_1^T(t)N + \dot{z}^T(s)P_2]P_2^{-1}[N^T\xi_1(t) + P_2\dot{z}(s)] ds \end{aligned} \quad (22)$$

Consequently, the following inequality holds:

$$\begin{aligned} & -\int_{t-\tau}^{t} \dot{z}^T(s)P_2\dot{z}(s) ds \\ & \le 2\xi_1^T(t)N(z - z_\tau) + h\xi_1^T(t)NP_2^{-1}N^T\xi_1(t) \end{aligned} \quad (23)$$

Similarly, the other integral terms in (17) can be derived to satisfy the following inequalities:

$$\begin{aligned} & -\int_{t-h}^{t-\tau} \dot{z}^T(s)P_2\dot{z}(s) ds \\ & \le 2\xi_1^T(t)S(z_\tau - z_h) + h\xi_1^T(t)SP_2^{-1}S^T\xi_1(t) \end{aligned} \quad (24)$$

$$-\int_{t-h}^{t} \dot{z}^T(s)P_2\dot{z}(s) ds \quad (25)$$

$$\le 2\xi_1^T(t)M(z - z_h) + h\xi_1^T(t)MP_2^{-1}M^T\xi_1(t)$$

Moreover

$$2e^T P_1 B_2 \eta \le \frac{2}{\gamma^2} e^T P_1 P_1 e + \frac{\gamma^2}{2} \eta^T \eta \quad (26)$$

$$2z^T P_2 L C e \le \varepsilon^{-1} z^T P_2 L C C^T P_2 z + \varepsilon e^T e \quad (27)$$

Selecting the error of the AFR as the evaluation signal for the demand of the AFR precise control, obviously one can obtain  $\frac{1}{2}z_1^2 \le \frac{1}{2}z^T z$ . Then the time derivative of  $V(t)$  satisfies the following inequality:

$$\dot{V} \le e^T \Xi_1 e + \xi_1^T(t) \Xi_2 \xi_1(t) + \frac{\gamma^2}{2} \eta^T \eta - \frac{1}{2} z_1^2 \quad (28)$$

where

$$\Xi_1 = A^T P_1 + P_1 A - P_1 L C - C^T L^T P_1 + \frac{2}{\gamma^2} P_1 P_1^T + \varepsilon I$$

$$\Xi_2 = \Gamma + h N P_2^{-1} N^T + h S P_2^{-1} S^T + h M P_2^{-1} M^T$$

with

$$\Gamma = \begin{bmatrix} \Sigma_1 & \Sigma_2 & N_3^T - S_1 - M_1 + M_3^T \\ * & \Sigma_3 & -N_3^T - S_2 + S_3^T - M_2 \\ * & * & -R - S_3 - S_3^T - M_3 - M_3^T \end{bmatrix}$$

$$\Sigma_1 = A^T P_2 + P_2 A + R + N_1 + N_1^T + \frac{1}{2} I + M_1 + M_1^T + \varepsilon^{-1} P_2 L C C^T L^T P_2 + 2h A^T P_2 A$$

$$\Sigma_2 = P_2 B_1 K - N_1 + N_2^T + S_1 + M_2^T + 2h A^T P_2 B_1 K$$

$$\Sigma_3 = -N_2 - N_2^T + S_2 + S_2^T + 2h K^T B_1^T P_2 B_1 K$$

According to the Schur component, the linear matrix inequality (13) is equivalent to  $\Xi_1 < 0$ . Meanwhile, the observer gain matrix  $L = P_1^{-1} Q$  and the positive parameter  $\varepsilon$  can be obtained by solving the LMI (13).

![Figure 4: Throttle opening and load torque in case 1. The plot shows throttle opening (deg) on the left y-axis (7.05 to 8.55) and load torque (Nm) on the right y-axis (50 to 70) over time t (s) from 0 to 50. Throttle opening is a step function from 7.5 to 8.5 degrees at t=10 and t=35. Load torque is a step function from 50 to 60 Nm at t=10 and t=35. A horizontal dashed green line is at 60 Nm.](e0d425c8e4eef259e4c52d81426d93fa_img.jpg)

Figure 4: Throttle opening and load torque in case 1. The plot shows throttle opening (deg) on the left y-axis (7.05 to 8.55) and load torque (Nm) on the right y-axis (50 to 70) over time t (s) from 0 to 50. Throttle opening is a step function from 7.5 to 8.5 degrees at t=10 and t=35. Load torque is a step function from 50 to 60 Nm at t=10 and t=35. A horizontal dashed green line is at 60 Nm.

Fig. 4. Throttle opening and load torque in case 1

![Figure 5: Throttle opening and load torque in case 2. The plot shows throttle opening (deg) on the left y-axis (8 to 10) and load torque (Nm) on the right y-axis (20 to 120) over time t (s) from 0 to 50. Throttle opening is a step function from 8.5 to 9.5 degrees at t=10 and t=35. Load torque is a step function from 40 to 100 Nm at t=10 and t=35. A horizontal dashed green line is at 80 Nm.](6de7dcb072cef2388026fb0f504084b2_img.jpg)

Figure 5: Throttle opening and load torque in case 2. The plot shows throttle opening (deg) on the left y-axis (8 to 10) and load torque (Nm) on the right y-axis (20 to 120) over time t (s) from 0 to 50. Throttle opening is a step function from 8.5 to 9.5 degrees at t=10 and t=35. Load torque is a step function from 40 to 100 Nm at t=10 and t=35. A horizontal dashed green line is at 80 Nm.

Fig. 5. Throttle opening and load torque in case 2

Similarly, by the Schur component, the equivalent inequality for  $\Xi_2 < 0$  can be obtained:

$$\begin{bmatrix} \phi' & hG' & hF' & hH' \\ * & -hP_2 & 0 & 0 \\ * & * & -hP_2 & 0 \\ * & * & * & -hP_2 \end{bmatrix} < 0 \quad (29)$$

where  $\phi' = \phi'_1 + \phi'_2 + \phi_2^T$

$$\phi'_1 = \begin{bmatrix} W' & P_2 B_1 K & 2hA^T P_2 & 0 \\ * & 0 & 2hK^T B_1^T P_2 & 0 \\ * & * & -2hP_2 & 0 \\ * & * & * & -R \end{bmatrix},$$

with

$$W' = A^T P_2 + P_2 A + R + \frac{1}{2} I + \varepsilon^{-1} P_2 L C C^T L^T P_2$$

$$\phi'_2 = \begin{bmatrix} G' + F' & -G' + H' & 0 & -F' - H' \end{bmatrix}$$

$$G' = \begin{bmatrix} N_1 \\ N_2 \\ 0 \\ N_3 \end{bmatrix}, F' = \begin{bmatrix} M_1 \\ M_2 \\ 0 \\ M_3 \end{bmatrix}, H' = \begin{bmatrix} S_1 \\ S_2 \\ 0 \\ S_3 \end{bmatrix}.$$

Pre-multiplying and post-multiplying both sides of (29) with  $\text{diag}\{P_2^{-1}, I, P_2^{-1}, I, I, I, I\}$  yields the inequality (14). Substituting the computed  $L$  and  $\varepsilon$ , and solving the LMI (14), the ADRC controller gain  $K$  can be obtained.

Consequently, it can be seen from (16) and (28) that when  $\eta = 0$ , the time derivative satisfies

$$\dot{V} \le e^T \Xi_1 e + \xi_1^T(t) \Xi_2 \xi_1(t)$$

As the matrix  $\Xi_1$ ,  $\Xi_2$  are negative, the closed-loop system is asymptotically stable, and  $e \to 0, z \to 0$  as  $t \to \infty$ .

![Figure 6: Engine speed N and intake manifold pressure p_m in case 1. The top plot shows engine speed N (rpm) on the y-axis (1300 to 1800) over time t (s) from 0 to 50. The speed is constant at 1400 rpm until t=10, then jumps to 1550 rpm, drops to 1400 rpm at t=20, jumps to 1750 rpm at t=35, and drops back to 1400 rpm at t=40. The bottom plot shows intake manifold pressure p_m (Pa) on the y-axis (1.8 to 2.8) over the same time period. The pressure is constant at approximately 2.2 Pa until t=10, then jumps to 2.4 Pa at t=15, drops to 2.0 Pa at t=20, jumps to 2.6 Pa at t=30, and drops back to 2.2 Pa at t=40.](a6a79139513e8df64dfc0b986a556f5f_img.jpg)

Figure 6: Engine speed N and intake manifold pressure p\_m in case 1. The top plot shows engine speed N (rpm) on the y-axis (1300 to 1800) over time t (s) from 0 to 50. The speed is constant at 1400 rpm until t=10, then jumps to 1550 rpm, drops to 1400 rpm at t=20, jumps to 1750 rpm at t=35, and drops back to 1400 rpm at t=40. The bottom plot shows intake manifold pressure p\_m (Pa) on the y-axis (1.8 to 2.8) over the same time period. The pressure is constant at approximately 2.2 Pa until t=10, then jumps to 2.4 Pa at t=15, drops to 2.0 Pa at t=20, jumps to 2.6 Pa at t=30, and drops back to 2.2 Pa at t=40.

Fig. 6. Engine speed  $N$  and intake manifold pressure  $p_m$  in case 1![Figure 7: Engine speed N and intake manifold pressure p_m in case 2. The top plot shows engine speed N (rpm) on the y-axis (1700 to 2100) over time t (s) from 0 to 50. The speed is constant at 2000 rpm until t=10, then drops to 1800 rpm, jumps back to 2000 rpm at t=20, drops to 1850 rpm at t=35, and jumps back to 2000 rpm at t=40. The bottom plot shows intake manifold pressure p_m (Pa) on the y-axis (1.8 to 2.8) over the same time period. The pressure is constant at approximately 2.3 Pa until t=10, then drops to 2.1 Pa at t=15, jumps to 2.5 Pa at t=20, drops to 2.2 Pa at t=35, and jumps back to 2.3 Pa at t=40.](0f92e96694face0b13a687ec21fb9101_img.jpg)

Figure 7: Engine speed N and intake manifold pressure p\_m in case 2. The top plot shows engine speed N (rpm) on the y-axis (1700 to 2100) over time t (s) from 0 to 50. The speed is constant at 2000 rpm until t=10, then drops to 1800 rpm, jumps back to 2000 rpm at t=20, drops to 1850 rpm at t=35, and jumps back to 2000 rpm at t=40. The bottom plot shows intake manifold pressure p\_m (Pa) on the y-axis (1.8 to 2.8) over the same time period. The pressure is constant at approximately 2.3 Pa until t=10, then drops to 2.1 Pa at t=15, jumps to 2.5 Pa at t=20, drops to 2.2 Pa at t=35, and jumps back to 2.3 Pa at t=40.

Fig. 7. Engine speed  $N$  and intake manifold pressure  $p_m$  in case 2

When  $\eta \neq 0$ , the following inequality holds:

$$\dot{V} \le -\frac{1}{2} z_1^2 + \frac{\gamma^2}{2} \eta^T \eta$$

i.e. if the  $L_2$  gain from  $\eta$  to  $z_1$  is less than  $\gamma$ , and  $\Xi_1$ ,  $\Xi_2$  are negative definite,  $\eta$  can be restrained under the given disturbance attenuation level.

**Remark 2.** That is to say, when the total disturbance in the AFR dynamic caused by the switching of the engine operations remains constant, the modified ADRC controller can compensate the disturbance entirely and handle the input time delay for

![Fig. 8: Three stacked plots showing AFR, fuel injection, and estimation of the total disturbance in case 1 over 50 seconds. The top plot shows AFR (λ_s) fluctuating around 1.0 with a scale factor of 10^-3. The middle plot shows fuel injection (u_f) in kg/s with a step change at 10s and 30s. The bottom plot shows the estimation of the total disturbance (f-hat) fluctuating around 4.75.](c54b3ca7603d65d4589151bc3a49d054_img.jpg)

Fig. 8: Three stacked plots showing AFR, fuel injection, and estimation of the total disturbance in case 1 over 50 seconds. The top plot shows AFR (λ\_s) fluctuating around 1.0 with a scale factor of 10^-3. The middle plot shows fuel injection (u\_f) in kg/s with a step change at 10s and 30s. The bottom plot shows the estimation of the total disturbance (f-hat) fluctuating around 4.75.

Fig. 8. AFR, fuel injection, and estimation of the total disturbance in case 1

achieving the precise control of the AFR. For the case where the engine operates in the transient state and the total disturbance is correspondingly changed, the effect of the various disturbances on the AFR can be suppressed so as that the AFR converges to the ideal value shortly.

## 5. Validation on Engine Simulator of SICE

The effectiveness of the modified ADRC fuel injection controller is validated by using the engine simulator developed by the SICE Research Committee on Advanced Powertrain Control Theory in the environment of MATLAB/Simulink. The simulator is a full-scale V6 SI engine consisting of the air path, the fuel path, and the engine torque rotation, the detailed model construction of which is presented in [18]. To reproduce the engine's dynamic behavior, the simulator is constructed as a 46th-order hybrid discrete-continuous time dynamical system model, in which the thermal and fluid dynamics are individually modeled for each cylinder [19]. Besides, for the control of the AFR, the UEGO sensor dynamic and time-varying transport delay are added to the simulator, as shown in Fig. 3.

In the simulation, two typical operations of the engine are considered to validate the controller design.

Case 1: The throttle opening is increased at 10 and 30 s and decreased at 20 and 40 s with the load torque remaining constant as shown in Fig. 4, which simulates the fast accelerated and decelerated engine, respectively.

Case 2: The load torque is raised at 10 and 30 s and dropped at 20 and 40 s, while the throttle opening is kept constant, as shown in Fig. 5, which implies that there exists load torque disturbance.

![Fig. 9: Three stacked plots showing AFR, fuel injection, and estimation of the total disturbance in case 2 over 50 seconds. The top plot shows AFR (λ_s) fluctuating around 1.0 with a scale factor of 10^-6. The middle plot shows fuel injection (u_f) in kg/s with a step change at 10s and 30s. The bottom plot shows the estimation of the total disturbance (f-hat) fluctuating around 4.8.](92c6488dfdf125bc1b7bb6a235394652_img.jpg)

Fig. 9: Three stacked plots showing AFR, fuel injection, and estimation of the total disturbance in case 2 over 50 seconds. The top plot shows AFR (λ\_s) fluctuating around 1.0 with a scale factor of 10^-6. The middle plot shows fuel injection (u\_f) in kg/s with a step change at 10s and 30s. The bottom plot shows the estimation of the total disturbance (f-hat) fluctuating around 4.8.

Fig. 9. AFR, fuel injection, and estimation of the total disturbance in case 2

The engine speed  $N$  and the intake manifold pressure  $p_m$  corresponding to cases 1 and 2 are shown in Figs 6 and 7, respectively.

In simulation, the level parameter  $\gamma$  is chosen as  $\gamma = 0.2$ . The engine idle speed in the SICE engine simulator is about 650 rpm, so the maximum transport delay can be approximately set as  $h = 0.2$ . The parameter  $b$  is chosen as  $b = -5$  based on experience. Solving the LMIs described in (13) and (14) using the MATLAB tool, the observer gain matrix and the controller gain matrix can be obtained:

$$L = [ 34.12 \ 136.24 \ 105.46 ]^T, K = [ 6.76 \ 5.2 \ 1.04 ]$$

The simulation results of the closed-loop system with the designed ADRC controller under the two operation modes are shown in Figs 8 and 9, respectively.

From Figs 8 and 9, the following conclusions can be drawn:

1. The ADRC-based controller can regulate the AFR in a narrow range around the stoichiometric value within the error band of 2% in the steady state and 5% in the transient process.
2. It seems that the control performance for the case with load torque change is slightly better than that for the case with throttle opening change; especially, there exist sharp peaks at the inflection points with large amplitude throttle opening change. This might well arise from the pump fluctuation acting on the air mass flow rate past the throttle plate while the throttle opening changes abruptly.

For fully validating the effectiveness of the designed fuel injection control scheme on the improvement of the transient AFR control performance and the attenuation level for the disturbance, the comparison results are also given between the AFR control

![Figure 10: Comparison between ADRC and PI control in the case of fast acceleration-deceleration without random fluctuation. The figure consists of three vertically stacked subplots. The top subplot shows 'Throttle opening (deg)' on the y-axis (7 to 9) versus time 't (s)' on the x-axis (0 to 50). A blue solid line (ADRC) shows a step increase from 7.5 to 8.5 at t=10 and a step decrease back to 7.5 at t=30. A red dashed line (PI) follows the ADRC but with significant overshoot and oscillation, reaching a peak of about 8.8 at t=10 and a trough of about 7.2 at t=30. The middle subplot shows the stoichiometric ratio 'lambda_s' on the y-axis (0.9 to 1.1) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 1.0, with the PI line showing more noise and a small peak at t=10. The bottom subplot shows the fuel injection signal 'u_fi (kg/s)' on the y-axis (4.5 to 7 x 10^-6) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 5.2 x 10^-6, with the PI line showing more noise and a small peak at t=10.](73c3e4508cae529acf4e6c7fa70b361a_img.jpg)

Figure 10: Comparison between ADRC and PI control in the case of fast acceleration-deceleration without random fluctuation. The figure consists of three vertically stacked subplots. The top subplot shows 'Throttle opening (deg)' on the y-axis (7 to 9) versus time 't (s)' on the x-axis (0 to 50). A blue solid line (ADRC) shows a step increase from 7.5 to 8.5 at t=10 and a step decrease back to 7.5 at t=30. A red dashed line (PI) follows the ADRC but with significant overshoot and oscillation, reaching a peak of about 8.8 at t=10 and a trough of about 7.2 at t=30. The middle subplot shows the stoichiometric ratio 'lambda\_s' on the y-axis (0.9 to 1.1) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 1.0, with the PI line showing more noise and a small peak at t=10. The bottom subplot shows the fuel injection signal 'u\_fi (kg/s)' on the y-axis (4.5 to 7 x 10^-6) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 5.2 x 10^-6, with the PI line showing more noise and a small peak at t=10.

Fig. 10. Comparison between ADRC and PI control in the case of fast acceleration–deceleration without random fluctuation

![Figure 11: Comparison between ADRC and PI control in the case of throttle opening with random disturbance. The figure consists of three vertically stacked subplots. The top subplot shows 'Throttle opening (deg)' on the y-axis (7 to 9) versus time 't (s)' on the x-axis (0 to 50). A blue solid line (ADRC) shows a step increase from 7.5 to 8.5 at t=10 and a step decrease back to 7.5 at t=30. A red dashed line (PI) follows the ADRC but with significant noise and oscillation, reaching a peak of about 8.8 at t=10 and a trough of about 7.2 at t=30. The middle subplot shows the stoichiometric ratio 'lambda_s' on the y-axis (0.85 to 1.1) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 1.0, with the PI line showing more noise and a small peak at t=10. The bottom subplot shows the fuel injection signal 'u_fi (kg/s)' on the y-axis (4.5 to 7 x 10^-6) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 5.2 x 10^-6, with the PI line showing more noise and a small peak at t=10.](a6a8016b231533e7f34b550f4676afc6_img.jpg)

Figure 11: Comparison between ADRC and PI control in the case of throttle opening with random disturbance. The figure consists of three vertically stacked subplots. The top subplot shows 'Throttle opening (deg)' on the y-axis (7 to 9) versus time 't (s)' on the x-axis (0 to 50). A blue solid line (ADRC) shows a step increase from 7.5 to 8.5 at t=10 and a step decrease back to 7.5 at t=30. A red dashed line (PI) follows the ADRC but with significant noise and oscillation, reaching a peak of about 8.8 at t=10 and a trough of about 7.2 at t=30. The middle subplot shows the stoichiometric ratio 'lambda\_s' on the y-axis (0.85 to 1.1) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 1.0, with the PI line showing more noise and a small peak at t=10. The bottom subplot shows the fuel injection signal 'u\_fi (kg/s)' on the y-axis (4.5 to 7 x 10^-6) versus time 't (s)'. Both ADRC (blue solid) and PI (red dashed) lines are centered around 5.2 x 10^-6, with the PI line showing more noise and a small peak at t=10.

Fig. 11. Comparison between ADRC and PI control in the case of throttle opening with random disturbance

systems installed at the presented ADRC-based controller (12) with (11) and the conventional PI controller. The conventional PI controller is designed as

$$u = K_p(\lambda_{sf} - \lambda_s) + K_I \int_0^t (\lambda_{sf}(s) - \lambda_s(s)) ds$$

The simulation results of both the modified ADRC controller and the conventional PI controller under the two operation modes are shown in Figs 10 and 11, respectively. For clarity of comparison of the transient and static performance between the two control strategies, Fig. 10 shows the case of an acceleration–deceleration process with longer static time, while for the illustration of the disturbance attenuation level comparison between two control strategies, Fig. 11 shows the case of the throttle opening variation as the same as Fig. 10 but with the additional random fluctuation.

From the comparison results shown in Figs 10 and 11, it can be seen that

on the transient A/F control performance while the engine is subjected to acceleration–deceleration and suffering from random disturbance, the presented ADRC-based controller has an advantage over the conventional PI controller. This benefits from the ADRC-based controller possessing the compensation for the ‘total disturbance’ associated with the changes of the engine speed, intake manifold pressure, parameters in the fuel film evaporation process, and the time delay, and as well as the random disturbance in the closed-loop system.

## 6. Conclusion

In this paper, a modified ADRC fuel injection controller was designed to maintain the AFR of the port-injected SI engine at the stoichiometric value both during steady and transient operations. To deal with the factors affecting the dynamics of the AFR, which

are generated by the variation of the intake manifold, engine speed, and load torque, as well as the perturbation of parameters in the processes of the fuel film evaporation and the oxygen sensor aging, the ADRC algorithm was applied. An ESO was constructed to estimate the total disturbance of the system. The gains matrices of the controller and the observer could be obtained by solving the LMIs employed in the analysis of the augmented error system. Considering the time-varying transport delay in the AFR system, the input fuel injection signal was delayed before entering the ESO. This modification could effectively improve the performance of the estimation by synchronizing the input signals of the ESO. Simulations were performed by a V6 SI engine simulator at two transient operation modes involving acceleration–deceleration and load variations of the engine for validating the control strategy’s effectiveness against injection and transport time delay and parameter uncertainties. Simulations showed that the ADRC-based fueling controller was more effective on improving the transient and static control performance of the stoichiometric A/F, which could maintain the AFR within a narrow range around the stoichiometric value through the compensation of the total disturbance.

## Acknowledgments

This work was supported by the National Natural Science Foundation of China (No. 61573304).

## References

- (1) Kahveci NE, Impram ST, Gene AU. Air–fuel ratio regulation using a discrete-time internal model controller. *IEEE International Conference on Intelligent Transportation Systems*, 2014; 2459–2464.

- (2) Bresch-Pietri D, Chauvin J, Petit N. Adaptive backstepping controller for uncertain systems with unknown input time-delay. Application to SI Engines. *IEEE Conference on Decision and Control*, Atlanta, GA, USA, December 15-17, 2010; 3680–3687.
- (3) Postma M, Nagamune R. Air–fuel ratio control of spark ignition engines using a switching LPV controller. *IEEE Transactions on Control Systems Technology* 2012; **20**(5):1175–1187.
- (4) Yang J, Shen T, Jiao X. Stochastic adaptive air–fuel ratio control of spark ignition engines. *IEEJ Transactions on Electrical and Electronic Engineering* 2014; **9**(4):442–447.
- (5) Gerasimov DN, Pshenichnikova EI. Neural network data-driven engine torque and air–fuel ratio control. *IEEE Mediterranean Electrotechnical Conference (MELECON)*, 2012; 524–527.
- (6) Alippi C, De Russis C, Piuri V. A neural-network based control solution to air–fuel ratio control for automotive fuel-injection systems. *IEEE Transactions on Systems, Man, and Cybernetics, Part C: Applications and Reviews* 2003; **33**(2):259–268.
- (7) Hou Z, Sen Q, Wu Y. Air fuel ratio identification of gasoline engine during transient conditions based on Elman Neural Networks. *IEEE International Conference on Intelligent Systems Design and Applications*, 2006; 32–36.
- (8) Ebrahimi B, Tafreshi R, Mohammadpour J. Second-order sliding mode strategy for air–fuel ratio control of lean-burn SI engines. *IEEE Transactions on Control Systems Technology* 2014; **22**(22):1374–1384.
- (9) Xue W, Bai W, Yang S. ADRC with adaptive extended state observer and its application to air–fuel Ratio control in gasoline engines. *IEEE Transactions on Industrial Electronics* 2015; **62**(9):5847–5857.
- (10) Tang H, Weng L, Dong ZY. Adaptive and learning control for SI engine model with uncertainties. *IEEE/ASME Transactions on Mechatronics* 2009; **14**(1):93–104.
- (11) Yildiz Y, Annaswamy AM, Yanakiev D. Spark ignition engine fuel-to-air ratio control: an adaptive control approach. *Control Engineering Practice* 2010; **18**(12):1369–1378.
- (12) Jiao X, Zhang J, Shen T. Adaptive air–fuel ratio control scheme and its experimental validations for port-injected spark ignition engines. *International Journal of Adaptive Control and Signal Processing* 2015; **29**(1):41–63.
- (13) Wang Z, Jiao X. Adaptive fueling control considering effect of time-delay for air–fuel ratio regulation of spark ignition engines. *Society of Instrument and Control Engineers of Japan (SICE) Annual Conference*, 2015; 1311–1315.
- (14) Chen X, Wang Y, Haskara I. Optimal air-to-fuel ratio tracking control with adaptive biofuel content estimation for LNT regeneration. *IEEE Transactions on Control Systems Technology* 2014; **22**(2):428–439.
- (15) Postma M, Nagamune R. Air–fuel ratio control of spark ignition engines using a switching LPV controller. *IEEE Transactions on Control Systems Technology* 2012; **20**(5):1175–1187.
- (16) Zhao S, Gao Z. Modified active disturbance rejection control for time-delay systems. *ISA Transactions* 2014; **53**(4):882–888.
- (17) Ariba Y, Gouaisbaut F. An augmented model for robust stability analysis of time-varying delay systems. *International Journal of Control* 2009; **82**(9):1616–1626.
- (18) Shen T, Ohata A. Modeling and Control Design for Automotive Engines. Coronasha: Japan; 2011 (in Japanese).
- (19) Shen T, Zhang J. SICE benchmark problem of engine control and a challenging result. *World Congress on Intelligent Control and Automation (WCICA)*, 2012; 2340–2345.

**Zhijing Wang** (Non-member) received the B.S. degree from Yanshan University, China, in 2013. She is currently pursuing the M.S. degree in the same university. Her research interests include intelligent control strategies and their applications to the air/fuel ratio control of spark ignition engines.

![Portrait photo of Zhijing Wang, a young woman with short dark hair, wearing a white turtleneck sweater.](efca2dce0095c9dc2a68e9af6b2bfd40_img.jpg)

Portrait photo of Zhijing Wang, a young woman with short dark hair, wearing a white turtleneck sweater.

**Xiaohong Jiao** (Non-member) received the Ph.D. degree in mechanical engineering from Sophia University, Tokyo, Japan, in 2004. She is now a Professor with the Institute of Electrical Engineering, Yanshan University, China. Her research interests include robust adaptive control of nonlinear systems and time-delay systems and their applications to hybrid distributed generation systems and automotive powertrain.

![Portrait photo of Xiaohong Jiao, a woman with short dark hair, wearing a dark jacket.](af54a0b30d50f3f8620b331cdc59ae3a_img.jpg)

Portrait photo of Xiaohong Jiao, a woman with short dark hair, wearing a dark jacket.