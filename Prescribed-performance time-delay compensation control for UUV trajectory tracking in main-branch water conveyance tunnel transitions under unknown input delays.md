

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the journal Ocean Engineering](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the journal Ocean Engineering

## Research paper

![Check for updates button](4f4b52340aaccb1bcf733468dca9ee03_img.jpg)

Check for updates button

# Prescribed-performance time-delay compensation control for UUV trajectory tracking in main-branch water conveyance tunnel transitions under unknown input delays<sup>☆</sup>

Liwen Zhang ![ORCID icon](faf942dc3e59ce8eb64b4ac481eca7e0_img.jpg), Yushan Sun<sup>\*</sup>, Puxin Chai, Jiehui Tan, Haotian Zheng ![ORCID icon](f6b0299e0b5e4340e509b71914970da0_img.jpg)

National Key Laboratory of Autonomous Marine Vehicle Technology, Harbin Engineering University, Harbin, 150001, China

## ARTICLE INFO

### Keywords:

Unmanned underwater vehicles (UUVs)  
Water conveyance tunnel inspection  
Prescribed performance control  
Unknown input delays  
Lyapunov-Krasovskii functional

## ABSTRACT

This study presents a novel control framework with delay compensation and prescribed performance guarantees for unmanned underwater vehicles (UUVs) trajectory tracking control in main-branch water conveyance tunnel transitions inspection tasks, addressing systems subject to uncertain time-varying input delays. The methodology integrates prescribed performance functions with a backstepping technique to develop virtual control laws, thereby ensuring bounded transient and steady-state tracking errors. Additionally, the study implements a delay compensator based on the integral of historical control inputs and estimation of uncertain input delays, effectively mitigating the adverse effects of unknown time-varying delays on trajectory tracking performance. Through the construction of Lyapunov-Krasovskii (L-K) functionals and Lyapunov theory, uniform ultimate boundedness of all closed-loop signals is rigorously proven. Simulation and field test results demonstrate that the proposed method maintains tracking errors within prescribed bounds, ensure both transient and steady-state control performance, and significantly enhance navigation safety for UUVs in tunnel entry/exit scenarios.

## 1. Introduction

Water conveyance tunnels are critical infrastructure for optimizing water resource allocation, necessitating regular safety inspections. Unmanned underwater vehicles (UUVs) have recently emerged as a novel solution for autonomous tunnel inspections, offering enhanced flexibility and underwater operational capabilities (Chen et al., 2022; Wang et al., 2020a; Zhang et al., 2023a). However, tunnel inspection tasks present substantial challenges for UUV control systems, including wall effects, unsteady flow fields, and complex hydrodynamic disturbances. Karras et al. (2013) proposed a robust sonar servo control scheme for autonomous underwater vehicle (AUV) wall following based on imaging sonar, with validation through water tank experiments. Wang et al. (2019) introduced a wall-following controller for water conveyance tunnel inspection AUVs based on a slow time-varying adaptive disturbance observer(ADO). This method employs the ADO to estimate and compensate for disturbances such as wall effects during tracking, while obtaining the real-time optimal heading of the AUV through an optimal weight distribution algorithm. To overcome inaccurate ranging caused

by acoustic echo interference in narrow tunnels, Wang et al. (2020b) devised a multi-sonar dynamic weighted polling algorithm combined with reinforcement learning for optimal wall tracking. de Cerqueira Gava et al. (2020) established an autonomous navigation framework integrating guidance systems with state feedback linearization to generate smooth trajectories in tunnels. Xia et al. (2023) enhanced long-distance tunnel control performance through a sonar-ranging feedback control method that combines autonomous heading planning with adaptive proportion-integral-derivative (PID) control.

Despite these advancements, existing studies primarily focus on main tunnel tracking control, neglecting the challenges posed by bifurcated tunnel junctions—narrow, geometrically complex environments requiring rapid response and ultra-high precision during entry/exit transitions. Furthermore, UUVs performing high-mobility tasks typically employ multiple actuators with heterogeneous hysteresis characteristics. The resulting input delays, caused by actuator hysteresis amplify system oscillations and overshoot, severely degrading control performance. Models including the Preisach (P) (Vasquez-Beltran et al., 2021), Prandtl-Ishlinskii (PI) (Liu et al., 2016; Huang et al., 2016), and

<sup>☆</sup> This work was supported in part by the Key Science and Technology Program of Shaanxi Province (2020skj-5), in part by the Natural Science Foundation of Heilongjiang Province Key Project under Grant ZD2020E005, in part by the National Natural Science Foundation of China under Grant 52071104.

<sup>\*</sup> Corresponding author.

E-mail address: [sunyushan@hrbeu.edu.cn](mailto:sunyushan@hrbeu.edu.cn) (Y. Sun).

Bouc-Wen (BW) (Liu et al., 2014; Wang et al., 2016) are commonly employed to characterize the hysteretic nonlinear behavior of actuators. While hysteresis compensation methods exist—including the asymmetric saturation model for biomimetic robotic fish (Wang et al., 2023) and adaptive neural network tracking control for BW hysteresis model with unknown parameters and direction conditions (Namadchian and Rouhani, 2018), they face limitations in modeling multi-actuator UUV delays. A common approach converts hysteresis effects into input delay problems, prompting extensive research on time-delay system stability for single time-varying delay systems (Yue, 2004), multiple time-varying delay systems (Niculescu et al., 1998), interval time-varying delay systems (Peng and Tian, 2008), neutral time-varying delay systems (Dong et al., 2018), and switched time-varying delay systems with actuator/controller failures (Guo et al., 2022). However, these generalized mathematical models inadequately address the nonlinear strong coupling inherent in UUV dynamics.

Notable efforts to mitigate input delays include a recurrent neural network predictive controller with a modified Smith predictor for nonlinear systems (Huang and Lewis, 2003) and a predictor-based method for AUV region tracking under known constant input delay (Mukherjee et al., 2015). Nevertheless, these methods require prior knowledge of time-delay parameters. Zhao and Hu (2017) designed a neural network-based predictor for discrete-time AUV path following, while Qiao et al. (2018) developed a robust  $H_2$  optimal depth controller for elevators with known delays. In (Sharma et al., 2011), researchers proposed a delay prediction-based compensation strategy for an Euler-Lagrange system with known input delays. Zhao (2018) similarly introduced a predictive controller to mitigate input delays in AUV path tracking, integrating adaptive neural networks to handle the nonlinear model uncertainty. Yan et al. (2019) designed a proportional-derivative (PD) controller for time-delayed systems, utilizing Lyapunov-Krasovskii (L-K) functions for stability analysis to establish sufficient tracking convergence conditions. Zhou et al. (2020) developed an integral time-delay sliding mode controller (TDSMC), achieving convergent trajectory tracking errors for underactuated AUVs under input delays. Chen et al. (2022) addressed horizontal-plane trajectory tracking control under unknown control directions and input delays, incorporating Nussbaum functions and prescribed performance functions into the controller design. Zhou et al. (2021) proposed a dual closed-loop control structure comprising an outer-loop kinematic controller based on integral sliding mode control (ISMC) and an inner-loop dynamic controller with adaptive robust time-delay control (ARTDC). The stability was verified through Razumikhin-type functionals, with control parameters optimized via linear matrix inequality (LMI) techniques. Simulations and experiments confirmed the method's effectiveness in vertical-plane tracking control under hydrodynamic uncertainties and actuator delays. Ghrab et al. (2021) presented a novel robust discrete-time sliding mode control (DT-SMC) scheme for linear systems, assuming known, bounded, and time-varying delays. Through slack variables and LMI theory, they derived less conservative delay-dependent stability criteria, validated experimentally on AUV platforms. Zhang et al. (2023b) formulated first-order differential equations to characterize actuator hysteresis dynamics, applying Nussbaum gain techniques to resolve unknown parameters in AUV path following.

Prescribed performance control (PPC) incorporates predefined transient and steady-state performance specifications into the controller design framework. Zhao et al. (2023) developed a dynamic prescribed performance function to address scenarios where tracking errors may violate preset performance boundaries under significant disturbances. Zhang et al. employed a tuning function (Zhang et al., 2024a) and a reverse tuning function (Zhang et al., 2024b) to generate prescribed performance boundaries, these were applied to fault-tolerant control of wheeled mobile robots (WMRs) and tracking control of time-delay nonlinear systems with output constraints, respectively. Li et al. (2022) designed a prescribed-performance-based robust delay-tolerant tracking controller for underactuated AUV seabed missions,

approximating unmodeled terms using radial basis function (RBF) neural networks. Numerous scholars have integrated sliding mode control with prescribed performance techniques (Sun et al., 2022, 2023), demonstrating superior transient performance and robustness in UUV trajectory tracking. However, practical implementation faces challenges such as the difficulty in obtaining precise hydrodynamic coefficients. Li et al. (2021) designed a prescribed performance function with user-assignable steady-state convergence time and devised a robust adaptive neural network control scheme. Rong et al. (2022) developed a piecewise performance function for trajectory tracking of underactuated UUVs, effectively alleviating controller output saturation during the initial phase. Guo et al. (2025) introduced predefined-time convergence piecewise functions to construct performance boundaries and modified the error transformation equation to prevent potential tracking error overshoot. Hu et al. (2023) proposed a novel sliding surface that allows pre-setting of performance on both tracking errors and their derivatives, with adaptive laws handling unknown compounded disturbances. Although numerous solutions exist, they primarily target delay-free systems or state-delayed systems and thus may fail under uncertain time-varying input delays. Unlike existing PPC frameworks, this work integrates delay compensation with PPC, simultaneously resolving transient performance bounds and delay-induced oscillations.

This study addresses the critical challenge of trajectory tracking control for UUVs in water conveyance tunnel inspection scenarios, particularly during entry/exit transitions through complex bifurcated tunnel junctions. Existing researches on tunnel tracking control has primarily focused on straight main tunnels (Wang et al., 2019; Xia et al., 2023), neglecting the compounded effects of asymmetric wall effects, unsteady flow disturbances, and heterogeneous actuator hysteresis characteristics in confined bifurcation zones. Additionally, conventional delay compensation methods often assume constant delay (Mukherjee et al., 2015; Zhou et al., 2020), rendering them inadequate for multi-actuator UUVs with unknown time-varying delays. To address these limitations, the primary contributions of this work are summarized as follows:

- (1) Compared with existing approaches (Sun et al., 2022, 2023), this work combines prescribed performance functions with time-delay compensation using backstepping techniques. The resultant controller eliminates the need for complex hydrodynamic coefficients, requiring only inertia matrix information, thereby significantly enhancing practical deployment.
- (2) A novel delay compensator is proposed, leveraging the integral of past control inputs and estimation of unknown time-varying input delays. This mechanism dynamically mitigates oscillations induced by input delays, eliminating the dependency on constant or known delay assumptions prevalent in existing methods (Mukherjee et al., 2015; Zhou et al., 2020).
- (3) Unlike stability proofs for systems with known constant input delays, we introduce three L-K functionals corresponding to time-delay variables. Through Lyapunov stability analysis, we establish sufficient conditions to ensure the uniform ultimate boundedness of all closed-loop signals. These conditions explicitly relate critical parameters, including input delay estimations, controller gains, and the upper bounds of auxiliary functions.

The remainder of this paper is organized as follows: Section 2 formulates the UUV dynamics and control challenges in bifurcated tunnel environments, explicitly modeling environmental disturbances and input time delays. Section 3 details the controller design and provides rigorous stability proofs. Sections 4 and 5 validate the effectiveness of the proposed method through simulation and field experimental results, respectively. Finally, Section 6 concludes the study and outlines future research directions.

![Figure 1: The coordinate system of UUV. The diagram shows two coordinate systems: an earth-fixed frame E-ξηζ and a body-fixed frame G-xyz. The earth-fixed frame has axes ξ, η, and ζ. The body-fixed frame has axes x, y, and z. The origin G of the body-fixed frame is located at the center of mass of the UUV. The orientation of the body-fixed frame is defined by roll (ψ), pitch (θ), and yaw (φ) angles relative to the earth-fixed frame. The UUV is shown in a side view, with velocity components u, v, w and angular velocity components p, q, r indicated.](7e2f2d03a5dda38b038fd4884629a2b4_img.jpg)

Figure 1: The coordinate system of UUV. The diagram shows two coordinate systems: an earth-fixed frame E-ξηζ and a body-fixed frame G-xyz. The earth-fixed frame has axes ξ, η, and ζ. The body-fixed frame has axes x, y, and z. The origin G of the body-fixed frame is located at the center of mass of the UUV. The orientation of the body-fixed frame is defined by roll (ψ), pitch (θ), and yaw (φ) angles relative to the earth-fixed frame. The UUV is shown in a side view, with velocity components u, v, w and angular velocity components p, q, r indicated.

Fig. 1. The coordinate system of UUV.

## 2. Problem statement

### 2.1. The UUV model

For the analysis of the three-dimensional motion of the vehicle, two coordinate systems are defined as illustrated in Fig. 1. The  $E$ – $\xi\eta\zeta$  and  $G$ – $xyz$  represent the earth-fixed and body-fixed coordinate systems of the UUV, respectively.

Based on the mathematical model established by Professor Fossen from the Norwegian University of Science and Technology (NTNU), this study adopts the fundamental assumption that the gravity acting on the UUV maintains equilibrium with its buoyancy, while the dynamic effects associated with roll motion are deliberately disregarded in the theoretical framework. The five-degree-of-freedom (5-DOF) kinematics and dynamics of a UUV operating in water conveyance tunnels can be described as (Fossen, 2011)

$$\dot{\eta} = J(\eta)\nu \quad (1)$$

$$\mathbf{M}\ddot{\nu} + \mathbf{C}(\nu)\dot{\nu} + \mathbf{D}(\nu)\dot{\nu} + \mathbf{g}(\eta) + \mathbf{d}_{\text{env}} = \tau(t - t_d) \quad (2)$$

where  $\eta = [\xi, \eta, \zeta, \theta, \psi]^T \in \mathbf{R}^5$  denotes the position and attitude vector of the UUV in the earth-fixed frame.  $\nu = [u, v, w, q, r]^T \in \mathbf{R}^5$  denotes velocity vector in the body-fixed frame.  $J(\eta) \in \mathbf{R}^{5 \times 5}$  is the transformation matrix between the two frames.  $\mathbf{M} \in \mathbf{R}^{5 \times 5}$  is the inertia matrix, which includes additional mass.  $\mathbf{C}(\nu) \in \mathbf{R}^{5 \times 5}$  denotes the centripetal and Coriolis matrix, including centripetal force and Coriolis force generated by additional mass.  $\mathbf{D}(\nu) \in \mathbf{R}^{5 \times 5}$  denotes the hydrodynamic damping matrix.  $\mathbf{g}(\eta) \in \mathbf{R}^5$  denotes the vector of static restoring forces and moments.  $\mathbf{d}_{\text{env}} \in \mathbf{R}^5$  denotes the environmental disturbance signals exist at the main-branch tunnel junction;  $\tau(t - t_d) \in \mathbf{R}^5$  denotes the corresponding control input vector with unknown time-varying delays  $t_d$  caused by actuator hysteresis characteristics, where

$$\mathbf{J}(\eta) = \begin{bmatrix} \cos \psi \cos \theta & -\sin \psi & \sin \theta \cos \psi & 0 & 0 \\ \sin \psi \cos \theta & \cos \psi & \sin \theta \sin \psi & 0 & 0 \\ -\sin \theta & 0 & \cos \theta & 0 & 0 \\ 0 & 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 0 & 1/\cos \theta \end{bmatrix} \quad (3)$$

$$\mathbf{M} = \mathbf{M}_{RB} + \mathbf{M}_A = \text{diag}(m, m, m, I_y, I_z) - \text{diag}(X_u, Y_v, Z_w, M_q, N_r) \quad (4)$$

$$\mathbf{C}(\nu) = \begin{bmatrix} 0 & -mr & 0 & 0 & Y_v \dot{v} \\ mr & 0 & 0 & 0 & -X_u \dot{u} \\ -mq & 0 & 0 & X_{u}u & 0 \\ Z_w w & 0 & -X_u u & 0 & 0 \\ -Y_v \dot{v} & X_u \dot{u} & 0 & 0 & 0 \end{bmatrix} \quad (5)$$

$$\mathbf{D}(\nu) = \text{diag}(X_u, Y_v, Z_w, M_q, N_r) + \text{diag}(X_{u|u}|u|, Y_{v|v}|v|, Z_{w|w}|w|, M_{q|q}|q|, N_{r|r}|r|) \quad (6)$$

**Table 1**  
Model parameters of the UUV.

| Additional mass                     | Linear damping coefficient                  | Quadratic damping coefficient           | Other parameters                   |
|-------------------------------------|---------------------------------------------|-----------------------------------------|------------------------------------|
| $X_u = -30\text{kg}$                | $X_u = 70\text{kg/s}$                       | $X_{u u } = 100\text{kg/m}$             | $m = 185\text{kg}$                 |
| $Y_v = -80\text{kg}$                | $Y_v = 100\text{kg/s}$                      | $Y_{v v } = 200\text{kg/m}$             | $I_y = 40\text{kg}\cdot\text{m}^2$ |
| $Z_w = -80\text{kg}$                | $Z_w = 100\text{kg/s}$                      | $Z_{w w } = 200\text{kg/m}$             | $I_z = 40\text{kg}\cdot\text{m}^2$ |
| $M_q = -40\text{kg}\cdot\text{m}^2$ | $M_q = 50\text{kg}\cdot\text{m}^2/\text{s}$ | $M_{q q } = 50\text{kg}\cdot\text{m}^2$ | $W = B = 1813\text{N}$             |
| $N_r = -40\text{kg}\cdot\text{m}^2$ | $N_r = 50\text{kg}\cdot\text{m}^2/\text{s}$ | $N_{r r } = 50\text{kg}\cdot\text{m}^2$ | $\overline{GM}_L = 0.02\text{m}$   |

$$\mathbf{g}(\eta) = [0, 0, 0, \overline{GM}_L W \sin \theta, 0]^T \quad (7)$$

The mass, metacentric height and hydrodynamic coefficient of the UUV in this paper are shown in Table 1 (Petterson and Egeland, 1999).

### 2.2. Environmental disturbance modeling

The environmental disturbance model is defined as consisting of the superposition of the wall effect disturbance forces  $\mathbf{d}_{\text{wall}}$ , the water flow disturbance forces  $\mathbf{d}_{\text{flow}}$ , and other external disturbance forces  $\mathbf{d}_{\text{other}}$ :

$$\mathbf{d}_{\text{env}} = \mathbf{d}_{\text{wall}} + \mathbf{d}_{\text{flow}} + \mathbf{d}_{\text{other}} \quad (8)$$

During navigation in confined near-wall waters, the UUV is subjected to disturbance forces and moments induced by wall effects. Studies indicate that within confined channels, the wall-effect disturbance forces acting on marine vessels are approximately inversely proportional to the reciprocal of the distance from the wall surface (Liu et al., 2018). Based on this empirical relationship, the wall effect-induced disturbance force is modeled as a function of the UUV velocity and proximity to tunnel walls:

$$\mathbf{d}_{\text{wall}} = [0, f_r(d_q) \cdot u^2, f_c(d_z) \cdot u^2, f_b(d_z) \cdot u^2, f_w(d_y) \cdot u^2]^T \quad (9)$$

where  $d_q$  and  $d_z$  denote the minimum distances to the side wall and bottom wall, respectively.  $f_i(*) = k_i \cdot *^{-1}$  ( $i = \eta, \zeta, \theta, \psi$ ) characterizes the nonlinear function, with  $k_i > 0$  as empirical coefficients.

When the UUV transitions from the main tunnel, which contains a longitudinal flow parallel to the tunnel axis with a velocity  $\mathbf{v}_{\text{main}}$ , to a branch tunnel with quiescent water conditions, the surrounding flow field undergoes an abrupt velocity change, consequently generating transitional flow-induced disturbance forces between the main and branch tunnels. The flow disturbance during this transition is expressed as:

$$\mathbf{d}_{\text{flow}} = -\frac{1}{2} \rho C_D A (\nu_r \circ |\nu_r|) \quad (10)$$

where  $\rho$  denotes the water density,  $C_D$  denotes the drag coefficient,  $A$  denotes the UUV cross-sectional area,  $\nu_r = \nu - \nu_c$  denotes the relative velocity vector between UUV and water flow, and  $\circ$  denotes the Hadamard product.

The spatial-dependent water velocity  $\nu_c$  is modeled using a sigmoid transition function:

$$\mathbf{v}_c = \mathbf{v}_{\text{main}} \cdot \left( 1 - \frac{1}{1 + e^{-k(x-x_0)}} \right) \quad (11)$$

where  $x_0$  is the transition start point, and  $k > 0$  controls the gradient steepness.

### 2.3. Control problem formulation

For subsequent analysis, transforming equations (1) and (2) to the earth-fixed frame, we have

![Figure 2: The architecture of the controller. The diagram shows a control loop starting with a 'Desired trajectory' block. This is compared with the actual state $\eta$ to produce an error signal $e$. This error signal is fed into 'Error constraints' and a 'Virtual control law' block. The 'Virtual control law' block also receives input from a 'main-branch water conveyance tunnel' image. The output of the 'Virtual control law' is $\alpha$, which is fed into a 'PPTDC' (Prescribed Performance Time Delay Compensation) block. The 'PPTDC' block also receives input from an 'Integrator' and a 'Delay estimator and compensation' block. The output of the 'PPTDC' block is the control signal $\tau(t)$. This signal is fed into an 'Unknown time delay' block, which outputs the delayed control signal $\tau(t-t_d)$. This delayed signal is then fed into the 'Unmanned underwater vehicle' block. The vehicle's output is the state $\eta$, which is fed back into the system. The 'Delay estimator and compensation' block also receives the delayed signal $\tau(t-t_d)$ and the state $\eta$ to estimate and compensate for the delay. The 'Integrator' block receives the control signal $\tau(t)$ and the state $\eta$.](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

Figure 2: The architecture of the controller. The diagram shows a control loop starting with a 'Desired trajectory' block. This is compared with the actual state \$\eta\$ to produce an error signal \$e\$. This error signal is fed into 'Error constraints' and a 'Virtual control law' block. The 'Virtual control law' block also receives input from a 'main-branch water conveyance tunnel' image. The output of the 'Virtual control law' is \$\alpha\$, which is fed into a 'PPTDC' (Prescribed Performance Time Delay Compensation) block. The 'PPTDC' block also receives input from an 'Integrator' and a 'Delay estimator and compensation' block. The output of the 'PPTDC' block is the control signal \$\tau(t)\$. This signal is fed into an 'Unknown time delay' block, which outputs the delayed control signal \$\tau(t-t\_d)\$. This delayed signal is then fed into the 'Unmanned underwater vehicle' block. The vehicle's output is the state \$\eta\$, which is fed back into the system. The 'Delay estimator and compensation' block also receives the delayed signal \$\tau(t-t\_d)\$ and the state \$\eta\$ to estimate and compensate for the delay. The 'Integrator' block receives the control signal \$\tau(t)\$ and the state \$\eta\$.

Fig. 2. The architecture of the controller.

$$\nu = J^{-1}(\eta)\dot{\eta} \quad (12)$$

$$\mathbf{M}_\eta(\eta)\ddot{\eta} + \mathbf{C}_\eta(\nu, \eta)\dot{\eta} + \mathbf{D}_\eta(\nu, \eta)\dot{\eta} + \mathbf{g}_\eta(\eta) + \mathbf{d}_\eta = \tau_\eta(t - t_d) \quad (13)$$

where

$$\begin{aligned} \mathbf{M}_\eta(\eta) &= J^{-T}(\eta)\mathbf{M}J^{-1}(\eta) \\ \mathbf{C}_\eta(\nu, \eta) &= J^{-T}(\eta)[\mathbf{C}(\nu) - \mathbf{M}J^{-1}(\eta)\dot{\mathbf{J}}(\eta)]J^{-1}(\eta) \\ \mathbf{D}_\eta(\nu, \eta) &= J^{-T}(\eta)\mathbf{D}(\nu)J^{-1}(\eta) \\ \mathbf{g}_\eta(\eta) &= J^{-T}(\eta)\mathbf{g}(\eta) \\ \tau_\eta(t - t_d) &= J^{-T}(\eta)\tau(t - t_d) \\ \mathbf{d}_\eta &= J^{-T}(\eta)\mathbf{d}_{env} \end{aligned} \quad (14)$$

The control design adheres to the following assumptions:

**Assumption 1.** The time-varying input time delays  $t_d$  are bounded and differentiable, with their derivatives satisfying  $|\dot{t}_d| < 1$  (Zhou et al., 2021). The estimates of the uncertain input time delays are denoted as  $\hat{t}_d$ , and the estimation errors are bounded such that  $|\tilde{t}_d| \le \tilde{t}_d$ , where  $\tilde{t}_d = t_d - \hat{t}_d$  and  $\tilde{t}_d$  is a known positive constant.

**Assumption 2.**  $\mathbf{M}_\eta(\eta)$ ,  $\mathbf{C}_\eta(\nu, \eta)$ ,  $\mathbf{D}_\eta(\nu, \eta)$ ,  $\mathbf{g}_\eta(\eta)$  are bounded, and their first-order time derivatives exist and remain bounded (Qiao et al., 2017). Furthermore,  $m_m \le \|\mathbf{M}_\eta(\eta)\| \le m_M$ ,  $\|\mathbf{M}_\eta(\eta)^{-1}\| \le \varsigma$ , where,  $m_m, m_M, \varsigma \in R^+$  are known positive constants.

**Assumption 3.** The desired trajectory  $\eta_d$  is continuous and bounded (Li et al., 2021), with bounded first-, second-, and third-order derivatives.

**Assumption 4.** The external disturbance  $\mathbf{d}_\eta$  is smooth and bounded (Hu et al., 2023), and its first-order derivative is continuous and bounded.

**Remark 1.** These assumptions are physically justified as follows:

- (1) **Assumption 1:** In practical UUV applications, the input delay of the thruster system exhibits a physical upper bound due to actuator dynamics, where mechanical inertia constrains it to vary slowly. The prior knowledge of the estimation error bound  $\tilde{t}_d$  solely facilitates stability analysis and does not need to be incorporated into the subsequent control law design.
- (2) **Assumption 2:** The positive definiteness of  $\mathbf{M}_\eta(\eta)$  originates from rigid-body mass distribution and added mass effects, while the boundedness of  $\mathbf{C}_\eta(\nu, \eta)$ ,  $\mathbf{D}_\eta(\nu, \eta)$ ,  $\mathbf{g}_\eta(\eta)$  derives from hydrodynamic properties. The existence of a bounded inverse  $\mathbf{M}_\eta(\eta)^{-1}$  follows directly from its uniform positive definiteness.
- (3) **Assumption 3:** In practical engineering applications, to ensure safe navigation in geometrically constrained environments, the target trajectory is usually set as a continuous bounded function.
- (4) **Assumption 4:** Disturbance energies in realistic scenarios, including wall effects and hydrodynamic disturbances, are bounded by fundamental physical constraints.

The goal of this paper is to design the controller, so that the UUV satisfies  $\lim_{t \to \infty} \eta \to \eta_d$  in the presence of unknown time-varying input delays and external environmental disturbance.

## 3. Controller design and analysis

The development of trajectory tracking controllers for UUVs operating in water conveyance tunnels must address two interconnected challenges: (1) the strict transient and steady-state performance requirements imposed by confined bifurcated geometries, and (2) the destabilizing effects of unknown time-varying input delays arising from multi-actuator hysteresis. Conventional methods relying on constant delay assumptions and lacking explicit error constraints prove inadequate for main-branch transitions. To overcome these limitations, this section proposes a prescribed performance time delay compensation controller (PPTDC) that integrates error constraints for bounded tracking performance, estimation of unknown delays, and the integral of historical control inputs. The closed-loop stability is mathematically proven through appropriate L-K functionals. Fig. 2 illustrates the controller architecture.

### 3.1. Controller design

Define the trajectory tracking error as

$$\mathbf{e}(t) = \eta_d - \eta = [\tilde{\xi}_d, \eta_d, \zeta_d, \theta_d, \psi_d]^T - [\xi, \eta, \zeta, \theta, \psi]^T \quad (15)$$

The state variables are defined as  $\mathbf{x}_1 = \mathbf{e}(t) = \eta_d - \eta$ ,  $\mathbf{x}_2 = \dot{\mathbf{e}}(t) = \dot{\eta}_d - \dot{\eta}$ . Thus, Equation (13) can be expressed as

$$\begin{cases} \dot{\mathbf{x}}_1 = \mathbf{x}_2 \\ \dot{\mathbf{x}}_2 = \mathbf{M}_\eta(\eta)^{-1}[\mathbf{C}_\eta(\nu, \eta)\dot{\eta} + \mathbf{D}_\eta(\nu, \eta)\dot{\eta} + \mathbf{g}_\eta(\eta) + \mathbf{d}_\eta] - \mathbf{M}_\eta(\eta)^{-1}\tau_\eta(t - t_d) + \tilde{\eta}_d \end{cases} \quad (16)$$

To ensure both transient and steady-state performance of the tracking error, prescribed performance functions  $\rho^i(t)$  are employed to constrain  $\mathbf{e}(t)$

$$-\rho^i(t) < \mathbf{e}_i(t) < \rho^i(t), \forall t \ge 0, i \in \{\xi, \eta, \zeta, \theta, \psi\} \quad (17)$$

where  $\rho^i(t) = (\rho_0^i - \rho_\infty^i)e^{-\kappa_i t} + \rho_\infty^i$ , with  $\rho_0^i > \max\{|\mathbf{e}_i(0)|, \rho_\infty^i\}$  and  $\kappa_i > 0$ .

**Remark 2.** To ensure the prescribed performance bounds within acceptable limits, the selection of  $\rho_0^i$  must enforce  $\rho_0^i > |\mathbf{e}_i(0)|$ . In trajectory tracking within water conveyance tunnels, UUVs inherently maintain small initial errors to meet inspection precision demands, thus making this strategy operationally viable.

Transform the constrained error into an unconstrained variable via

$$\mathbf{e}_i(t) = \frac{1}{2} \ln \left( \frac{e_i + \rho^i}{\rho^i - e_i} \right) \quad (18)$$

The derivation of (18) is obtained as follows

$$\begin{aligned} \dot{\mathbf{e}}_i(t) &= \frac{\rho^i \dot{e}_i - \dot{\rho}^i e_i}{(\rho^i - e_i)(\rho^i + e_i)} \\ &= \frac{\rho^i}{(\rho^i - e_i)(\rho^i + e_i)} \left( \dot{e}_i - \frac{\dot{\rho}^i e_i}{\rho^i} \right) \\ &= \Gamma_i \left( \dot{e}_i - \frac{\dot{\rho}^i e_i}{\rho^i} \right) \end{aligned} \quad (19)$$

where  $\Gamma_i^{\Delta} = \frac{\beta^i}{(\rho^i - e_i)(\rho^i + e_i)}$ .

Construct the Lyapunov function candidate as follows

$$V_1 = \frac{1}{2} \mathbf{e}^T \mathbf{e} \quad (20)$$

Taking the time derivative of (20) and substituting (19) yields

$$\dot{V}_1 = \mathbf{e}^T \dot{\mathbf{e}} = \mathbf{e}^T \Gamma (\dot{\mathbf{x}}_1 - \rho^{-1} \dot{\rho} \mathbf{x}_1) \quad (21)$$

where  $\Gamma = \text{diag}(\Gamma_\xi, \Gamma_\eta, \Gamma_\zeta, \Gamma_\theta, \Gamma_\psi)$ ,  $\rho^{-1} \dot{\rho} \mathbf{x}_1 = \left[ \frac{\dot{\rho}^i e_i}{\rho^{2i}}, \frac{\dot{\rho}^i e_i}{\rho^i}, \frac{\dot{\rho}^i e_i}{\rho^i}, \frac{\dot{\rho}^i e_i}{\rho^i}, \frac{\dot{\rho}^i e_i}{\rho^i} \right]^T$

Design the virtual control law as

$$\alpha = \rho^{-1} \dot{\rho} \mathbf{x}_1 - \mathbf{K}_\alpha \Gamma^{-1} \mathbf{e} \quad (22)$$

where  $\mathbf{K}_\alpha \in \mathbf{R}^{5 \times 5}$  denotes a positive definite constant diagonal matrix.

Define the error variable  $\beta$  as

$$\beta = \alpha - \mathbf{x}_2 \quad (23)$$

Substituting (22) and (23) into (21) yields

$$\begin{aligned} \dot{V}_1 &= -\mathbf{e}^T \mathbf{K}_\alpha \mathbf{e} + \mathbf{e}^T \Gamma (\dot{\mathbf{x}}_1 - \alpha) \\ &= -\mathbf{e}^T \mathbf{K}_\alpha \mathbf{e} - \mathbf{e}^T \Gamma \beta \end{aligned} \quad (24)$$

In order to compensate the effect of input delays on the control system, the compensation variable is designed as

$$\begin{aligned} \mathbf{r} &= \dot{\beta} + \mathbf{K}_\beta \mathbf{M}_\eta(\eta)^{-1} \beta - \mathbf{M}_\eta(\eta)^{-1} \int_{t-\tau_d}^{t} \dot{\tau}_\eta(s) ds \\ &= \dot{\beta} + \mathbf{K}_\beta \mathbf{M}_\eta(\eta)^{-1} \beta - \mathbf{M}_\eta(\eta)^{-1} (\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d)) \end{aligned} \quad (25)$$

where  $\mathbf{K}_\beta \in \mathbf{R}^{5 \times 5}$  denotes a positive definite constant diagonal matrix.

Combined with the subsequent stability analysis, the control inputs of the prescribed performance control method based on unknown time-varying input delay compensation are designed as follows

$$\begin{aligned} \tau_\eta &= \mathbf{K}_\gamma \int_0^t \mathbf{r}(s) ds \\ &= \mathbf{K}_\gamma \left[ \int_0^t (\mathbf{K}_\beta \mathbf{M}_\eta(\eta)^{-1} \beta(s) - \mathbf{M}_\eta(\eta)^{-1} (\tau_\eta(s) - \tau_\eta(s - \hat{\tau}_d))) ds \right] \\ &\quad + \mathbf{K}_\beta \beta(t) - \mathbf{K}_\beta \beta(0) \end{aligned} \quad (26)$$

where  $\mathbf{K}_\gamma \in \mathbf{R}^{5 \times 5}$  denotes a positive definite constant diagonal matrix

Substituting (23) into (25) yields

$$\begin{aligned} \mathbf{r} &= \dot{\alpha} - \dot{\mathbf{x}}_2 + \mathbf{K}_\beta \mathbf{M}_\eta(\eta)^{-1} \beta - \mathbf{M}_\eta(\eta)^{-1} (\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d)) \\ &= \dot{\alpha} - \mathbf{M}_\eta(\eta)^{-1} [\mathbf{C}_\eta(\nu, \eta) \dot{\eta} + \mathbf{D}_\eta(\nu, \eta) \ddot{\eta} + \mathbf{g}_\eta(\eta) + \mathbf{d}_\eta] - \ddot{\eta}_d \\ &\quad + \mathbf{K}_\beta \mathbf{M}_\eta(\eta)^{-1} \beta - \mathbf{M}_\eta(\eta)^{-1} \tau_\eta(t - \tau_d) - \mathbf{M}_\eta(\eta)^{-1} \tau_\eta(t) + \mathbf{M}_\eta(\eta)^{-1} \tau_\eta(t - \hat{\tau}_d) \end{aligned} \quad (27)$$

Equation (27) is multiplied by  $\mathbf{M}_\eta(\eta)$  on both sides, and differentiating yields

$$\begin{aligned} \dot{\mathbf{M}}_\eta(\eta) \mathbf{r} + \mathbf{M}_\eta(\eta) \dot{\mathbf{r}} &= \dot{\mathbf{M}}_\eta(\eta) \dot{\alpha} + \mathbf{M}_\eta(\eta) \ddot{\alpha} - \dot{\mathbf{C}}_\eta(\nu, \eta) \dot{\eta} - \mathbf{C}_\eta(\nu, \eta) \ddot{\eta} \\ &\quad - \dot{\mathbf{D}}_\eta(\nu, \eta) \dot{\eta} - \mathbf{D}_\eta(\nu, \eta) \ddot{\eta} - \dot{\mathbf{g}}_\eta(\eta) - \dot{\mathbf{d}}_\eta - \mathbf{M}_\eta(\eta) \ddot{\eta}_d \\ &\quad - \mathbf{M}_\eta(\eta) \ddot{\eta}_d + \mathbf{K}_\beta \dot{\beta} - (1 - \dot{\tau}_d) \dot{\tau}_\eta(t - \tau_d) - \dot{\tau}_\eta(t) + \dot{\tau}_\eta(t - \hat{\tau}_d) \end{aligned} \quad (28)$$

Substituting (26) into (28) yields

$$\begin{aligned} \dot{\mathbf{M}}_\eta(\eta) \mathbf{r} + \mathbf{M}_\eta(\eta) \dot{\mathbf{r}} &= \dot{\mathbf{M}}_\eta(\eta) \dot{\alpha} + \mathbf{M}_\eta(\eta) \ddot{\alpha} - \dot{\mathbf{C}}_\eta(\nu, \eta) \dot{\eta} - \mathbf{C}_\eta(\nu, \eta) \ddot{\eta} \\ &\quad - \dot{\mathbf{D}}_\eta(\nu, \eta) \dot{\eta} - \mathbf{D}_\eta(\nu, \eta) \ddot{\eta} - \dot{\mathbf{g}}_\eta(\eta) - \dot{\mathbf{d}}_\eta - \mathbf{M}_\eta(\eta) \ddot{\eta}_d \\ &\quad - \mathbf{M}_\eta(\eta) \ddot{\eta}_d + \mathbf{K}_\beta \dot{\beta} + \dot{\tau}_d \mathbf{K}_\gamma \mathbf{r}(t - \tau_d) - \mathbf{K}_\gamma \mathbf{r}(t) \\ &\quad + \dot{\tau}_\eta(t - \hat{\tau}_d) - \dot{\tau}_\eta(t - \tau_d) \end{aligned} \quad (29)$$

### 3.2. System stability analysis

To carry out the stability analysis, the following Lyapunov candidate was chosen

$$V_2 = V_1 + \frac{1}{2} \beta^T \beta + \frac{1}{2} \mathbf{r}^T \mathbf{M}_\eta(\eta) \mathbf{r} + Q_1 + Q_2 + Q_3 \quad (30)$$

where  $Q_1, Q_2, Q_3$  denote the designed L-K functionals, defined by

$$\begin{aligned} Q_1 &= \int_{t-\tau_d}^{t} \|\mathbf{r}(s)\|^2 ds \\ Q_2 &= \int_{t-\tau_d}^{t} \|\mathbf{r}(s)\|^2 ds \\ Q_3 &= \int_{t-(\hat{\tau}_d + \tau_d)}^{t} \left( \int_{\lambda}^{t} \|\dot{\tau}_\eta(s)\|^2 ds \right) d\lambda \end{aligned} \quad (31)$$

The upper bound of  $Q_3$  can be expressed as

$$\begin{aligned} Q_3 &\le (\tilde{\tau}_d + \hat{\tau}_d) \sup_{s \in [t-(\hat{\tau}_d + \tau_d), t]} \left[ \int_{\lambda}^{t} \|\dot{\tau}_\eta(s)\|^2 ds \right] \\ &\le (\tilde{\tau}_d + \hat{\tau}_d) \left[ \int_{t-(\hat{\tau}_d + \tau_d)}^{t} \|\dot{\tau}_\eta(s)\|^2 ds \right] \end{aligned} \quad (32)$$

Differentiating (30) yields

$$\dot{V}_2 = \dot{V}_1 + \beta^T \dot{\beta} + \mathbf{r}^T \mathbf{M}_\eta(\eta) \dot{\mathbf{r}} + \frac{1}{2} \mathbf{r}^T \dot{\mathbf{M}}_\eta(\eta) \mathbf{r} + \dot{Q}_1 + \dot{Q}_2 + \dot{Q}_3 \quad (33)$$

From (25), we have

$$\dot{\beta} = \mathbf{r} - \mathbf{K}_\beta \mathbf{M}_\eta(\eta)^{-1} \beta + \mathbf{M}_\eta(\eta)^{-1} (\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d)) \quad (34)$$

To facilitate the subsequent stability analysis, an auxiliary term  $\mathbf{R}(\mathbf{e}, \beta, \mathbf{r}, t) \in \mathbf{R}^5$  is defined as follows

$$\begin{aligned} \mathbf{R} &= -(\mathbf{r}^T)^{-1} \mathbf{e}^T \Gamma \beta - \frac{1}{2} \dot{\mathbf{M}}_\eta(\eta) \mathbf{r} + \dot{\mathbf{M}}_\eta(\eta) \dot{\alpha} + \mathbf{M}_\eta(\eta) \dot{\alpha} \\ &\quad - \dot{\mathbf{C}}_\eta(\nu, \eta) \dot{\eta} - \mathbf{C}_\eta(\nu, \eta) \ddot{\eta} - \dot{\mathbf{D}}_\eta(\nu, \eta) \dot{\eta} - \mathbf{D}_\eta(\nu, \eta) \ddot{\eta} \\ &\quad - \dot{\mathbf{g}}_\eta(\eta) - \mathbf{M}_\eta(\eta) \ddot{\eta}_d - \mathbf{M}_\eta(\eta) \ddot{\eta}_d + \mathbf{K}_\beta \beta \end{aligned} \quad (35)$$

Thus, Equation (29) can be rearranged to obtain

$$\begin{aligned} \mathbf{M}_\eta(\eta) \dot{\mathbf{r}} &= -\frac{1}{2} \dot{\mathbf{M}}_\eta(\eta) \mathbf{r} + \dot{\tau}_d \mathbf{K}_\gamma \mathbf{r}(t - \tau_d) - \mathbf{K}_\gamma \mathbf{r}(t) \\ &\quad + \dot{\tau}_\eta(t - \hat{\tau}_d) - \dot{\tau}_\eta(t - \tau_d) + (\mathbf{r}^T)^{-1} \mathbf{e}^T \Gamma \beta + \mathbf{R} - \dot{\mathbf{d}}_\eta \end{aligned} \quad (36)$$

It is evident that the auxiliary term  $\mathbf{R}(\mathbf{e}, \beta, \mathbf{r}, t)$  is unmeasurable. To address this, an auxiliary function  $R_d(\eta_d, \dot{\eta}_d, \ddot{\eta}_d, \dddot{\eta}_d, t)$  is defined as

$$\begin{aligned} R_d(\eta_d, \dot{\eta}_d, \ddot{\eta}_d, \dddot{\eta}_d, t) &= -\dot{\mathbf{C}}_\eta(\dot{\eta}_d, \eta_d) \dot{\eta}_d - \mathbf{C}_\eta(\dot{\eta}_d, \eta_d) \ddot{\eta}_d - \dot{\mathbf{D}}_\eta(\dot{\eta}_d, \eta_d) \dot{\eta}_d \\ &\quad - \mathbf{D}_\eta(\dot{\eta}_d, \eta_d) \ddot{\eta}_d - \dot{\mathbf{g}}_\eta(\eta_d) - \dot{\mathbf{M}}_\eta(\eta_d) \ddot{\eta}_d - \mathbf{M}_\eta(\eta_d) \ddot{\eta}_d \end{aligned} \quad (37)$$

Substituting (37) into (36) and rearranging yields the following expression

$$\begin{aligned} \mathbf{M}_\eta(\eta) \dot{\mathbf{r}} &= -\frac{1}{2} \dot{\mathbf{M}}_\eta(\eta) \mathbf{r} + \dot{\tau}_d \mathbf{K}_\gamma \mathbf{r}(t - \tau_d) - \mathbf{K}_\gamma \mathbf{r}(t) \\ &\quad + \dot{\tau}_\eta(t - \hat{\tau}_d) - \dot{\tau}_\eta(t - \tau_d) + (\mathbf{r}^T)^{-1} \mathbf{e}^T \Gamma \beta + \tilde{\mathbf{R}} + \mathbf{S} - \beta \end{aligned} \quad (38)$$

where the auxiliary terms  $\tilde{\mathbf{R}}(\mathbf{e}, \beta, \mathbf{r}, t)$  and  $\mathbf{S}(\eta_d, \dot{\eta}_d, \ddot{\eta}_d, \dddot{\eta}_d, t)$  are defined as follows

$$\begin{aligned} \tilde{\mathbf{R}}(\mathbf{e}, \beta, \mathbf{r}, t) &= \mathbf{R} - R_d + \beta \\ \mathbf{S}(\eta_d, \dot{\eta}_d, \ddot{\eta}_d, \dddot{\eta}_d, t) &= \mathbf{R}_d - \dot{\mathbf{d}}_\eta \end{aligned} \quad (39)$$

Applying the intermediate value theorem, the boundedness constraint of  $\tilde{\mathbf{R}}$  is obtained as follows

$$\tilde{\mathbf{R}} \le \bar{\mathbf{R}}(\|\mathbf{z}\|) \|\mathbf{z}\| \quad (40)$$

where  $\mathbf{z} = [\mathbf{e}^T, \beta^T, \mathbf{r}^T]^T \in \mathbf{R}^{15}$ ,  $\bar{\mathbf{R}}(\|\mathbf{z}\|)$  is a positive, globally invertible, non-decreasing bounding function.

![Fig. 3. Schematic of UUV navigation at tunnel junctions. The diagram shows a 3D perspective of a tunnel junction with three branches: Main Tunnel, Other Branch Tunnel, and Exit Branch Tunnel. A Tunnel Detection UUV is shown in the Main Tunnel. A Desired Trajectory (blue line) and an Actual Trajectory (red line) are plotted. A coordinate system (ξ, η) is shown at the top left.](8e592c58b5074d79831ff650c2c636df_img.jpg)

Fig. 3. Schematic of UUV navigation at tunnel junctions. The diagram shows a 3D perspective of a tunnel junction with three branches: Main Tunnel, Other Branch Tunnel, and Exit Branch Tunnel. A Tunnel Detection UUV is shown in the Main Tunnel. A Desired Trajectory (blue line) and an Actual Trajectory (red line) are plotted. A coordinate system (ξ, η) is shown at the top left.

Fig. 3. Schematic of UUV navigation at tunnel junctions.

Under Assumptions 2, 3 and 4, the function  $S(\eta_d, \dot{\eta}_d, \ddot{\eta}_d, \dddot{\eta}_d, t)$  is bounded such that

---


$$\begin{aligned} |\beta^T(\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d))| &\le \frac{1}{2}\|\beta\|^2 + \frac{1}{2}\|\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d)\|^2 \\ \|\mathbf{r}(t)\|\|\mathbf{r}(t - \hat{\tau}_d)\| &\le \frac{1}{2}\|\mathbf{r}(t)\|^2 + \frac{1}{2}\|\mathbf{r}(t - \hat{\tau}_d)\|^2 \\ \delta\|\mathbf{r}(t)\| &\le \frac{1}{2}\|\delta\|^2 + \frac{1}{2}\|\mathbf{r}(t)\|^2 \\ \bar{R}(\|\mathbf{z}\|)\|\mathbf{z}\|\|\mathbf{r}(t)\| &\le \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|)\|\mathbf{z}\|^2 + \frac{1}{2}\|\mathbf{r}(t)\|^2 = \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|)(\|\mathbf{e}\|^2 + \|\beta\|^2 + \|\mathbf{r}(t)\|^2) + \frac{1}{2}\|\mathbf{r}(t)\|^2 \end{aligned} \quad (47)$$


---

$$\|S\| \le \delta \quad (41)$$

where  $\delta \in \mathbb{R}^+$  is a known positive constant.

Substituting (24), (34) and (38) into (33) gives

$$\begin{aligned} \dot{V}_2 = & -e^T \mathbf{K}_a \mathbf{e} - e^T \mathbf{r} \beta + \beta^T (\mathbf{r} - \mathbf{K}_p \mathbf{M}_\eta(\eta)^{-1} \beta + \mathbf{M}_\eta(\eta)^{-1} (\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d))) \\ & + \mathbf{r}^T \left( -\frac{1}{2} \mathbf{M}_\eta(\eta) \mathbf{r} + \hat{\tau}_d \mathbf{K}_r \mathbf{r}(t - \hat{\tau}_d) - \mathbf{K}_r \mathbf{r}(t) + \dot{\tau}_\eta(t - \hat{\tau}_d) - \dot{\tau}_\eta(t - \hat{\tau}_d) + (\mathbf{r}^T)^{-1} e^T \Gamma \beta \right) \\ & + \frac{1}{2} \mathbf{r}^T \mathbf{M}_\eta(\eta) \mathbf{r} + \mathbf{r}^T (\tilde{\mathbf{R}} + \mathbf{S} - \beta) + \dot{Q}_1 + \dot{Q}_2 + \dot{Q}_3 \end{aligned} \quad (42)$$

According to the Leibniz-Newton theorem, the derivatives of  $Q_1$ ,  $Q_2$  and  $Q_3$  are

$$\begin{aligned} \dot{Q}_1 &= \|\mathbf{r}(t)\|^2 - \|\mathbf{r}(t - \hat{\tau}_d)\|^2 \\ \dot{Q}_2 &= \|\mathbf{r}(t)\|^2 - (1 - \hat{\tau}_d)\|\mathbf{r}(t - \hat{\tau}_d)\|^2 \\ \dot{Q}_3 &= (\tilde{\tau}_d + \hat{\tau}_d)\|\mathbf{K}_r\|\|\mathbf{r}(t)\|^2 - \int_{t-(\tilde{\tau}_d+\hat{\tau}_d)}^{t} \|\dot{\tau}_\eta(s)\|^2 ds \end{aligned} \quad (43)$$

Substituting into equation (42) yields

$$\begin{aligned} \dot{V}_2 = & -\|\mathbf{K}_a\|\|\mathbf{e}\|^2 - \|\mathbf{K}_\beta\|\|\mathbf{M}_\eta(\eta)^{-1}\|\|\beta\|^2 - \|\mathbf{K}_r\|\|\mathbf{r}(t)\|^2 \\ & + \|\mathbf{M}_\eta(\eta)^{-1}\|\beta^T(\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d)) \\ & + \hat{\tau}_d \|\mathbf{K}_r\|\|\mathbf{r}^T \mathbf{r}(t - \hat{\tau}_d) + \|\mathbf{K}_r\|\|\mathbf{r}^T(\mathbf{r}(t - \hat{\tau}_d) - \mathbf{r}(t - \hat{\tau}_d)) + \mathbf{r}^T \tilde{\mathbf{R}} + \mathbf{r}^T \mathbf{S} \\ & + \|\mathbf{r}(t)\|^2 - \|\mathbf{r}(t - \hat{\tau}_d)\|^2 + \|\mathbf{r}(t)\|^2 - (1 - \hat{\tau}_d)\|\mathbf{r}(t - \hat{\tau}_d)\|^2 \\ & + (\tilde{\tau}_d + \hat{\tau}_d)\|\mathbf{K}_r\|\|\mathbf{r}(t)\|^2 - \int_{t-(\tilde{\tau}_d+\hat{\tau}_d)}^{t} \|\dot{\tau}_\eta(s)\|^2 ds \end{aligned} \quad (44)$$

Based on assumptions 1 and 2,  $\|\dot{\tau}_d\| < 1$ ,  $1 - \hat{\tau}_d > 0$ ,  $\|\mathbf{M}_\eta(\eta)^{-1}\| \le \varsigma$  can be obtained. Substituting the inequalities into (44) yields

$$\begin{aligned} \dot{V}_2 \le & -\|\mathbf{K}_a\|\|\mathbf{e}\|^2 - \varsigma \|\mathbf{K}_\beta\|\|\beta\|^2 - \|\mathbf{K}_r\|\|\mathbf{r}(t)\|^2 + \varsigma \beta^T(\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d)) \\ & + \|\mathbf{K}_r\|\|\mathbf{r}^T \mathbf{r}(t - \hat{\tau}_d) + \mathbf{r}^T \tilde{\mathbf{R}} + \mathbf{r}^T \mathbf{S} + \|\mathbf{r}(t)\|^2 - \|\mathbf{r}(t - \hat{\tau}_d)\|^2 + \|\mathbf{r}(t)\|^2 \\ & + (\tilde{\tau}_d + \hat{\tau}_d)\|\mathbf{K}_r\|\|\mathbf{r}(t)\|^2 - \int_{t-(\tilde{\tau}_d+\hat{\tau}_d)}^{t} \|\dot{\tau}_\eta(s)\|^2 ds \end{aligned} \quad (45)$$

Combining (40), (41), and (45), we obtain

$$\begin{aligned} \dot{V}_2 \le & -\|\mathbf{K}_a\|\|\mathbf{e}\|^2 - \varsigma \|\mathbf{K}_\beta\|\|\beta\|^2 - \|\mathbf{K}_r\|\|\mathbf{r}(t)\|^2 + \varsigma |\beta^T(\tau_\eta(t) - \tau_\eta(t - \hat{\tau}_d))| \\ & + \|\mathbf{K}_r\|\|\mathbf{r}(t)\|\|\mathbf{r}(t - \hat{\tau}_d)\| + \bar{R}(\|\mathbf{z}\|)\|\mathbf{z}\|\|\mathbf{r}(t)\| + \delta\|\mathbf{r}(t)\| \\ & + \|\mathbf{r}(t)\|^2 - \|\mathbf{r}(t - \hat{\tau}_d)\|^2 + \|\mathbf{r}(t)\|^2 + (\tilde{\tau}_d + \hat{\tau}_d)\|\mathbf{K}_r\|\|\mathbf{r}(t)\|^2 \end{aligned} \quad (46)$$

According to Young's inequality and Cauchy-Schwarz inequality, it follows that

Substituting (47) into (46), we obtain

$$\begin{aligned} \dot{V}_2 \le & -\left(\|\mathbf{K}_a\| - \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|)\right)\|\mathbf{e}\|^2 \\ & - \left(\varsigma \|\mathbf{K}_\beta\| - \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|) - \frac{1}{2}\right)\|\beta\|^2 \\ & - \left(\frac{1}{2}\|\mathbf{K}_r\| - \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|) - 3 - (\tilde{\tau}_d + \hat{\tau}_d)\|\mathbf{K}_r\|\right)\|\mathbf{r}(t)\|^2 \\ & + \left(\frac{1}{2}\|\mathbf{K}_r\| - 1\right)\|\mathbf{r}(t - \hat{\tau}_d)\|^2 + \frac{1}{2}\|\mathbf{r}(t - \hat{\tau}_d)\|^2 \le -\alpha V_2 + \beta \end{aligned} \quad (48)$$

$$\begin{aligned} \text{where } \beta = & \left(\frac{1}{2}\|\mathbf{K}_r\| - 1\right)\|\mathbf{r}(t - \hat{\tau}_d)\|^2 + \frac{1}{2}\|\mathbf{r}(t - \hat{\tau}_d)\|^2 + \frac{1}{2}\|\mathbf{r}(t - \hat{\tau}_d)\|^2, \alpha = \\ & \min \left[ \|\mathbf{K}_a\| - \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|), \varsigma \|\mathbf{K}_\beta\| - \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|) - \frac{1}{2}, \frac{1}{2}\|\mathbf{K}_r\| - \frac{1}{2}\bar{R}^2(\|\mathbf{z}\|) - 3 - \right. \\ & \left. (\tilde{\tau}_d + \hat{\tau}_d)\|\mathbf{K}_r\| \right] \end{aligned}$$

By setting reasonable control parameters such that  $\alpha > 0$  and  $\beta > 0$ , the closed-loop system is bounded for all signals according to the Lyapunov stability lemma.

## 4. Simulation results and analysis

To validate the proposed control framework, comprehensive nu-

![Figure 4: 3D plot showing trajectory tracking results of different algorithms. The plot displays four trajectories in a 3D space defined by axes ξ (m), η (m), and ζ (m). The trajectories are: Desired (dashed black line), Proposed (PPTDC) (solid red line), Compared (TDC) (solid blue line), and ASMC-PPS (solid cyan line). The trajectories start at (0, 0, 0) and follow a similar path, with the ASMC-PPS algorithm showing the highest deviation from the desired path.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 4: 3D plot showing trajectory tracking results of different algorithms. The plot displays four trajectories in a 3D space defined by axes ξ (m), η (m), and ζ (m). The trajectories are: Desired (dashed black line), Proposed (PPTDC) (solid red line), Compared (TDC) (solid blue line), and ASMC-PPS (solid cyan line). The trajectories start at (0, 0, 0) and follow a similar path, with the ASMC-PPS algorithm showing the highest deviation from the desired path.

Fig. 4. Trajectory tracking results of different algorithms.

![Figure 5: Position tracking results of different algorithms. Three subplots show the tracking of ξ (m), η (m), and ζ (m) over 100 seconds. Each subplot compares the Desired trajectory (dashed black line) with PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). Insets show zoomed-in views of the initial 5 seconds for each subplot, highlighting the transient response and steady-state error.](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 5: Position tracking results of different algorithms. Three subplots show the tracking of ξ (m), η (m), and ζ (m) over 100 seconds. Each subplot compares the Desired trajectory (dashed black line) with PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). Insets show zoomed-in views of the initial 5 seconds for each subplot, highlighting the transient response and steady-state error.

Fig. 5. Position tracking results of different algorithms.

![Figure 6: Attitude angle tracking results of different algorithms. Two subplots show the tracking of θ (°) and ψ (°) over 100 seconds. Each subplot compares the Desired trajectory (dashed black line) with PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). The θ (°) plot shows significant oscillations for the TDC and ASMC-PPS algorithms, while PPTDC remains stable. The ψ (°) plot shows a step change in the desired trajectory at t=50s, which is tracked well by all algorithms.](01da0d212fb571933f10f96556157745_img.jpg)

Figure 6: Attitude angle tracking results of different algorithms. Two subplots show the tracking of θ (°) and ψ (°) over 100 seconds. Each subplot compares the Desired trajectory (dashed black line) with PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). The θ (°) plot shows significant oscillations for the TDC and ASMC-PPS algorithms, while PPTDC remains stable. The ψ (°) plot shows a step change in the desired trajectory at t=50s, which is tracked well by all algorithms.

Fig. 6. Attitude angle tracking results of different algorithms.

![Figure 7: Position tracking errors of different algorithms. Three subplots show the tracking errors ξ_e (m), η_e (m), and ζ_e (m) over 100 seconds. Each subplot compares the errors for PPB (dashed magenta), PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). The ASMC-PPS algorithm consistently shows the lowest error across all three axes.](023b142f90e1253702ac88b18380d3ec_img.jpg)

Figure 7: Position tracking errors of different algorithms. Three subplots show the tracking errors ξ\_e (m), η\_e (m), and ζ\_e (m) over 100 seconds. Each subplot compares the errors for PPB (dashed magenta), PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). The ASMC-PPS algorithm consistently shows the lowest error across all three axes.

Fig. 7. Position tracking errors of different algorithms.

merical simulations were conducted under tunnel transition scenarios. As depicted in Fig. 3, the test environment involves a bifurcated tunnel network consisting of a main tunnel and a branch tunnel interconnected by a 90-degree transitional junction. The main tunnel has a diameter of 4.5 m and is characterized by a steady longitudinal flow velocity denoted as  $v_{\text{main}} = 0.5\text{m/s}$ , while the branch tunnel maintains quiescent water conditions. This section systematically evaluates the controller's transient/steady-state performance, robustness to unknown time-varying input delays, and comparative advantages over existing methods.

Based on engineering blueprints of a main-branch tunnel junction, the desired trajectory was designed as follows

$$\xi_d = \begin{cases} 0.5t, & t < 48 \\ 24 + 6 \sin\left(\frac{1}{12}(t - 48)\right), & 48 \le t < 48 + 6\pi \\ 30, & 48 + 6\pi \le t \le 100 \end{cases} \quad (49)$$

$$\eta_d = \begin{cases} 0, & t < 48 \\ 6 - 6 \cos\left(\frac{1}{12}(t - 48)\right), & 48 \le t < 48 + 6\pi \\ 6 + 0.5(t - 48 - 6\pi), & 48 + 6\pi \le t \le 100 \end{cases} \quad (50)$$

$$\zeta_d = \begin{cases} 2, & t < 48 \\ 2 - \frac{1}{52}(t - 48), & 48 \le t \le 100 \end{cases} \quad (51)$$

$$\theta_d = 0 \quad (52)$$

$$\psi_d = \begin{cases} 0, & t < 48 \\ \frac{1}{12}(t - 48), & 48 \le t < 48 + 6\pi \\ \frac{\pi}{2}, & 48 + 6\pi \le t \le 100 \end{cases} \quad (53)$$

Control performance was quantified using the integral time-weighted absolute error (ITAE)

$$\text{ITAE} = \int_0^t t|e(t)|dt \quad (54)$$

### 4.1. Simulation results of different algorithms

To evaluate the impact of unknown time-varying input delays on

![Figure 8: Attitude angle tracking errors of different algorithms. Two subplots show the tracking error for roll angle (phi_e) and pitch angle (theta_e) over 100 seconds. The algorithms compared are PPB (dashed magenta), PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). The errors for PPTDC, TDC, and ASMC-PPS are very close to zero, while PPB shows significant oscillations.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 8: Attitude angle tracking errors of different algorithms. Two subplots show the tracking error for roll angle (phi\_e) and pitch angle (theta\_e) over 100 seconds. The algorithms compared are PPB (dashed magenta), PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). The errors for PPTDC, TDC, and ASMC-PPS are very close to zero, while PPB shows significant oscillations.

Fig. 8. Attitude angle tracking errors of different algorithms.

![Figure 9: Control input forces of different algorithms. Three subplots show the control forces tau_u, tau_v, and tau_w over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 9: Control input forces of different algorithms. Three subplots show the control forces tau\_u, tau\_v, and tau\_w over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.

Fig. 9. Control input forces of different algorithms.

![Figure 10: Control input moments of different algorithms. Two subplots show the control moments tau_q and tau_r over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.](27b22513fc27a0ff5f230b062ad3112f_img.jpg)

Figure 10: Control input moments of different algorithms. Two subplots show the control moments tau\_q and tau\_r over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.

Fig. 10. Control input moments of different algorithms.

![Figure 11: Velocity response curve of different algorithms. Three subplots show the velocity components u, v, and w over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.](643d86ebba41e16a88461bfcb3741de6_img.jpg)

Figure 11: Velocity response curve of different algorithms. Three subplots show the velocity components u, v, and w over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.

Fig. 11. Velocity response curve of different algorithms.

![Figure 12: Angular velocity response curve of different algorithms. Two subplots show the angular velocity components q and r over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.](2396add2849eccefcbcfbe1c7142a253_img.jpg)

Figure 12: Angular velocity response curve of different algorithms. Two subplots show the angular velocity components q and r over 100 seconds. The algorithms compared are PPTDC (solid red), TDC (solid blue), and ASMC-PPS (solid cyan). PPTDC shows high-frequency oscillations, while TDC and ASMC-PPS show smoother responses.

Fig. 12. Angular velocity response curve of different algorithms.

trajectory tracking performance, a series of simulations were conducted comparing the proposed algorithm with established methods, including adaptive sliding mode control law with pre-specified performance settings (ASMC-PPS) (Hu et al., 2023) and time-delay compensation control (TDC) (Sharma et al., 2011). The transient and steady-state performance under time-varying input delays was systematically analyzed.

The numerical simulations employed parameters representative of typical UUV operations in water conveyance tunnels, with initial states set to  $\eta(0) = [0, 1, 1, 0, 0]^T$  and  $\nu(0) = [0.5, 0, 0, 0]^T$ . Prescribed performance constraints were defined by  $\rho_0 = [0.5, 1.5, 1.5, 0.5, 0.5]^T$ ,  $\rho_\infty = [0.1, 0.1, 0.1, 0.05, 0.05]^T$  and  $\kappa = [0.5, 0.1, 0.1, 0.1, 0.1]^T$  to enforce bounded errors. Controller gains were tuned via Lyapunov stability criteria to  $\mathbf{K}_a = \text{diag}(1.0, 1.5, 1.5, 0.5, 2.0)$ ,  $\mathbf{K}_\beta = \text{diag}(1.0, 0.2, 0.2, 0.2, 0.2)$  and  $\mathbf{K}_\gamma = \text{diag}(1.5, 2.0, 2.0, 1.5, 1.5)$ . Environmental disturbances included wall effects ( $f^{(*)} = 0.05 \cdot s^{-1}$ ), transitional flow forces ( $\rho = 1025 \text{ kg/m}^3$ ;  $C_D = 0.008$ ;  $A = 0.2 \text{ m}^2$ ), and other external disturbance forces  $\mathbf{d}_{\text{other}} = 2 \sin(0.1t)$ . Input delays were

![Bar chart showing ITAE indicators for position and attitude angle errors. The x-axis categories are ξ_e (m), η_e (m), ζ_e (m), θ_e (°), and ψ_e (°). The y-axis is ITAE. The legend indicates PPTDC (orange), TDC (green), and ASMC-PPS (purple).](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

| Error Type     | PPTDC (ITAE) | TDC (ITAE) | ASMC-PPS (ITAE) |
|----------------|--------------|------------|-----------------|
| $\xi_e$ (m)    | 0.30         | 1.91       | 3.25            |
| $\eta_e$ (m)   | 4.07         | 5.82       | 9.89            |
| $\zeta_e$ (m)  | 3.63         | 5.38       | 11.62           |
| $\theta_e$ (°) | 0.21         | 1.33       | 0.61            |
| $\psi_e$ (°)   | 0.17         | 1.15       | 2.94            |

Bar chart showing ITAE indicators for position and attitude angle errors. The x-axis categories are ξ\_e (m), η\_e (m), ζ\_e (m), θ\_e (°), and ψ\_e (°). The y-axis is ITAE. The legend indicates PPTDC (orange), TDC (green), and ASMC-PPS (purple).

Fig. 13. ITAE indicators of position and attitude angle errors.

![3D plot of trajectory tracking results. The axes are ξ (m), η (m), and ζ (m). The plot shows the desired trajectory (dashed line) and the tracking paths for 0.4sPPTDC (red), 0.5sPPTDC (blue), and 0.6sPPTDC (cyan).](891ff9b651838b7f59e9a1612a739e15_img.jpg)

3D plot of trajectory tracking results. The axes are ξ (m), η (m), and ζ (m). The plot shows the desired trajectory (dashed line) and the tracking paths for 0.4sPPTDC (red), 0.5sPPTDC (blue), and 0.6sPPTDC (cyan).

Fig. 14. Trajectory tracking results under different delay estimates.

simulated as  $t_d = 0.1(5 + \cos(0.1t))$  s. These parameters ensured a balance between tracking precision, robustness, and computational feasibility. The control parameters for the comparative methods are configured as specified in their original sources. To ensure impartiality, the prescribed performance parameters are consistent with those used in this study.

Fig. 4 compares the trajectory tracking results of the three algorithms. The ASMC-PPS controller exhibits persistent oscillations during post-turn phases due to its lack of input delay compensation, while TDC and PPTDC maintain stable tracking. Notably, PPTDC achieves faster convergence and higher steady-state accuracy, owing to its explicit error constraints and integrated delay compensation.

Figs. 5 and 6 detail the position and attitude angle tracking performance. As shown in Fig. 5, PPTDC achieves rapid convergence in lateral and vertical positions despite initial deviations, while TDC exhibits slower convergence. For heading and pitch angle tracking, PPTDC reduces steady-state errors by 64 % and 8 %, respectively, compared to TDC (see Fig. 6). This enhanced performance can be attributed to the implementation of prescribed performance bounds. It is noteworthy that, given the constant desired pitch angle, input delays have a diminished impact on pitch control. As evidenced by the ASMC-PPS control outcomes, the prescribed performance function contributes to superior effectiveness compared to TDC.

![Three subplots showing position tracking results (ξ (m), η (m), ζ (m)) over time (0-100s) for different delay estimates (0.4s, 0.5s, 0.6s PPTDC). Each plot includes a zoomed-in view of the initial transient phase.](9d8d3d909d7fdccb631c519df2b86e61_img.jpg)

Three subplots showing position tracking results (ξ (m), η (m), ζ (m)) over time (0-100s) for different delay estimates (0.4s, 0.5s, 0.6s PPTDC). Each plot includes a zoomed-in view of the initial transient phase.

Fig. 15. Position tracking results under different delay estimates.

![Two subplots showing attitude angle tracking results (ψ (°), θ (°)) over time (0-100s) for different delay estimates (0.4s, 0.5s, 0.6s PPTDC). Each plot includes a zoomed-in view of the initial transient phase.](ae21ece48844b14b230832cbb6fcf735_img.jpg)

Two subplots showing attitude angle tracking results (ψ (°), θ (°)) over time (0-100s) for different delay estimates (0.4s, 0.5s, 0.6s PPTDC). Each plot includes a zoomed-in view of the initial transient phase.

Fig. 16. Attitude angle tracking results under different delay estimates.

![Three subplots showing position tracking errors (ξ_e (m), η_e (m), ζ_e (m)) over time (0-100s) for different delay estimates (0.4s, 0.5s, 0.6s PPTDC). Each plot compares PPTDC with PBB (pink dashed line) and includes a zoomed-in view of the initial transient phase.](8f93234090c5bc224e4b9d035018a927_img.jpg)

Three subplots showing position tracking errors (ξ\_e (m), η\_e (m), ζ\_e (m)) over time (0-100s) for different delay estimates (0.4s, 0.5s, 0.6s PPTDC). Each plot compares PPTDC with PBB (pink dashed line) and includes a zoomed-in view of the initial transient phase.

Fig. 17. Position tracking errors under different delay estimates.

![Figure 18: Attitude angle tracking errors under different delay estimates. Two plots show roll error ψ_e (°) and pitch error θ_e (°) over 100 seconds. The legend includes PPB (dashed magenta), 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the error signals between 1-4s and 67-69s.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 18: Attitude angle tracking errors under different delay estimates. Two plots show roll error ψ\_e (°) and pitch error θ\_e (°) over 100 seconds. The legend includes PPB (dashed magenta), 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the error signals between 1-4s and 67-69s.

Fig. 18. Attitude angle tracking errors under different delay estimates.

![Figure 21: Velocity response curve under different delay estimates. Three plots show surge velocity u (m/s), sway velocity v (m/s), and heave velocity w (m/s) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the velocity signals between 0-5s and 66-72s.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 21: Velocity response curve under different delay estimates. Three plots show surge velocity u (m/s), sway velocity v (m/s), and heave velocity w (m/s) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the velocity signals between 0-5s and 66-72s.

Fig. 21. Velocity response curve under different delay estimates.

![Figure 19: Control input forces under different delay estimates. Three plots show surge force T_u (N), sway force T_v (N), and heave force T_w (N) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the force signals between 0-5s and 66-70s.](33228b4227fa57e1477b27b9e07483e6_img.jpg)

Figure 19: Control input forces under different delay estimates. Three plots show surge force T\_u (N), sway force T\_v (N), and heave force T\_w (N) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the force signals between 0-5s and 66-70s.

Fig. 19. Control input forces under different delay estimates.

![Figure 22: Angular velocity response curve under different delay estimates. Two plots show roll angular velocity q (°/s) and pitch angular velocity r (°/s) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the angular velocity signals between 0-3s and 48-52s.](df476ed6ad0bb890c67aa63e7647d071_img.jpg)

Figure 22: Angular velocity response curve under different delay estimates. Two plots show roll angular velocity q (°/s) and pitch angular velocity r (°/s) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the angular velocity signals between 0-3s and 48-52s.

Fig. 22. Angular velocity response curve under different delay estimates.

![Figure 20: Control input moments under different delay estimates. Two plots show roll moment τ_q (N·m) and pitch moment τ_r (N·m) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the moment signals between 0-6s and 48-51s.](58de972a8c79c238b69cbeeafcc8d5fb_img.jpg)

Figure 20: Control input moments under different delay estimates. Two plots show roll moment τ\_q (N·m) and pitch moment τ\_r (N·m) over 100 seconds. The legend includes 0.4sPPTDC (solid red), 0.5sPPTDC (solid blue), and 0.6sPPTDC (solid cyan). Insets show zoomed-in views of the moment signals between 0-6s and 48-51s.

Fig. 20. Control input moments under different delay estimates.

The superiority of PPTDC is further evidenced in Figs. 7–10. From Fig. 7, ASMC-PPS's position tracking errors increase at the turns, while PPTDC confines errors within 0.05 m. Similarly, Fig. 8 indicates that PPTDC limits attitude angle errors to  $|\psi_e| < 2.0^\circ$  and  $|\theta_e| < 2.0^\circ$ , satisfying the safety thresholds for tunnel transitions. Although the control

![Figure 23: ITAE indicators of position and attitude angle errors. A bar chart shows ITAE values for ξ_e (m), η_e (m), ζ_e (m), θ_e (°), and ψ_e (°) for three delay estimates: 0.4sPPTDC (orange), 0.5sPPTDC (green), and 0.6sPPTDC (purple).](07496ee9f5697ea2702f9c108db04713_img.jpg)

| Variable       | 0.4sPPTDC | 0.5sPPTDC | 0.6sPPTDC |
|----------------|-----------|-----------|-----------|
| $\xi_e$ (m)    | 0.239     | 0.212     | 0.267     |
| $\eta_e$ (m)   | 3.968     | 3.917     | 4.020     |
| $\zeta_e$ (m)  | 3.628     | 3.626     | 3.631     |
| $\theta_e$ (°) | 0.166     | 0.147     | 0.185     |
| $\psi_e$ (°)   | 0.130     | 0.115     | 0.147     |

Figure 23: ITAE indicators of position and attitude angle errors. A bar chart shows ITAE values for ξ\_e (m), η\_e (m), ζ\_e (m), θ\_e (°), and ψ\_e (°) for three delay estimates: 0.4sPPTDC (orange), 0.5sPPTDC (green), and 0.6sPPTDC (purple).

Fig. 23. ITAE indicators of position and attitude angle errors.



![Figure 24: Experimental environment and UUV. The top left shows a yellow UUV with labels for Thrusters, Antenna module, Ranging sonar, Stern, Stem, Cameras and lights, and thrusters T1-T8. The top right shows an aerial view of the experimental water area. The bottom left shows a physical test platform with a signal acquisition system and a thruster under hydrodynamic loading.](6d9013c24741e861f3c8e0a763b6da22_img.jpg)

Figure 24: Experimental environment and UUV. The top left shows a yellow UUV with labels for Thrusters, Antenna module, Ranging sonar, Stern, Stem, Cameras and lights, and thrusters T1-T8. The top right shows an aerial view of the experimental water area. The bottom left shows a physical test platform with a signal acquisition system and a thruster under hydrodynamic loading.

Fig. 24. Experimental environment and UUV.

**Table 2**  
Key platform parameters.

| UUV Parameters   | Values | Sensor Parameters          | Specification   |
|------------------|--------|----------------------------|-----------------|
| Weight           | 45 kg  | GPS positioning accuracy   | 1.2m CEP        |
| Length           | 1.96m  | DVL velocity accuracy      | $\pm 0.1$ cm/s  |
| Maximum diameter | 0.336m | AHRS attitude accuracy     | $\pm 0.5^\circ$ |
| Thrusters Number | 8      | Ranging sonar resolution   | 0.01m           |
| Maximum velocity | 3kn    | Control sampling frequency | 10Hz            |

![Figure 25: Input delay characterization experiments. The image shows a physical test platform with a signal acquisition system and a thruster under hydrodynamic loading.](2de51a31da9b0ffd9d017f035d498997_img.jpg)

Figure 25: Input delay characterization experiments. The image shows a physical test platform with a signal acquisition system and a thruster under hydrodynamic loading.

Fig. 25. Input delay characterization experiments.

error of ASMC-PPS remaining within prescribed performance bounds in this scenario, tracking errors may breach these bounds as input delays increase, thereby undermining the effectiveness of the PPC technique. Control input profiles (see Figs. 9 and 10) demonstrate that PPTDC generates smoother force and moment commands, reducing actuator wear. Conversely, ASMC-PPS exhibits chattering phenomena in its control inputs when subjected to significant changes in desired states.

Velocity and angular velocity responses (see Figs. 11 and 12) confirm PPTDC's balanced transient dynamics. The surge velocity stabilizes within 4 s, compared to 8 s for TDC. Quantitatively, the ITAE indicators presented in Fig. 13 demonstrate that, compared to TDC, PPTDC achieves reductions in longitudinal position, lateral position, vertical position, heading angle, and pitch angle errors of 84 %, 30 %, 33 %, 84 %, and 85 %, respectively. Against ASMC-PPS, PPTDC yields error reductions of 91 %, 59 %, 69 %, 66 %, and 94 % for the same metrics, validating its enhanced responsiveness and precision.

## 4.2. Simulation results under different delay estimates

To assess robustness against unknown time-varying input delays, simulations were performed with three delay estimation values (0.4 s, 0.5 s, and 0.6 s), denoted as 0.4s-PPTDC, 0.5s-PPTDC, and 0.6s-PPTDC. Parameters remained consistent with section 4.1.

![Figure 26: Experimental results of horizontal plane trajectory tracking. The graph plots depth η (m) on the y-axis (0 to 50) against horizontal position ξ (m) on the x-axis (0 to 40). It shows a desired trajectory (dashed line), a PID control response (red solid line), and a proposed control response (blue solid line). The PID response shows significant oscillation and overshoot, while the proposed response follows the desired trajectory more closely and smoothly.](fdcbd505a623f39366aa8a18ed847f84_img.jpg)

Figure 26: Experimental results of horizontal plane trajectory tracking. The graph plots depth η (m) on the y-axis (0 to 50) against horizontal position ξ (m) on the x-axis (0 to 40). It shows a desired trajectory (dashed line), a PID control response (red solid line), and a proposed control response (blue solid line). The PID response shows significant oscillation and overshoot, while the proposed response follows the desired trajectory more closely and smoothly.

Fig. 26. Experimental results of horizontal plane trajectory tracking.

![Figure 27: Trajectory tracking response curve. Three subplots show the tracking performance over 100 seconds. The top subplot shows lateral position ξ (m) (0 to 40). The middle subplot shows depth η (m) (0 to 60). The bottom subplot shows heading angle ψ (°) (0 to 120). Each plot compares the desired trajectory (dashed line), PID control (red solid line), and proposed control (blue solid line). The proposed control consistently shows better tracking performance with less error and smoother transitions.](79f6905843b1411f7143697e2c4c7a0e_img.jpg)

Figure 27: Trajectory tracking response curve. Three subplots show the tracking performance over 100 seconds. The top subplot shows lateral position ξ (m) (0 to 40). The middle subplot shows depth η (m) (0 to 60). The bottom subplot shows heading angle ψ (°) (0 to 120). Each plot compares the desired trajectory (dashed line), PID control (red solid line), and proposed control (blue solid line). The proposed control consistently shows better tracking performance with less error and smoother transitions.

Fig. 27. Trajectory tracking response curve.

![Figure 28: Tracking errors for the position and heading angle. The figure consists of three vertically stacked subplots. The top subplot shows the lateral position error ξ_e(m) over 100 seconds, with the Proposed method (blue) staying near zero, while PPB (purple dashed) and PID (red solid) show larger fluctuations. The middle subplot shows the heading error η_e(m) over 100 seconds, where the Proposed method (blue) maintains the smallest error. The bottom subplot shows the heading angle ψ_e(°) over 100 seconds, where the Proposed method (blue) converges to zero most rapidly. All plots include a legend for PPB, PID, and Proposed methods.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 28: Tracking errors for the position and heading angle. The figure consists of three vertically stacked subplots. The top subplot shows the lateral position error ξ\_e(m) over 100 seconds, with the Proposed method (blue) staying near zero, while PPB (purple dashed) and PID (red solid) show larger fluctuations. The middle subplot shows the heading error η\_e(m) over 100 seconds, where the Proposed method (blue) maintains the smallest error. The bottom subplot shows the heading angle ψ\_e(°) over 100 seconds, where the Proposed method (blue) converges to zero most rapidly. All plots include a legend for PPB, PID, and Proposed methods.

Fig. 28. Tracking errors for the position and heading angle.

As shown in Fig. 14, all cases successfully track the reference trajectory, demonstrating the controller's insensitivity to delay estimation errors. Position and attitude tracking results (see Figs. 15 and 16) indicate minimal performance degradation—lateral errors remain within 0.08 m even with a 20 % overestimated delay. The partial enlarged view indicates that 0.4s-PPTDC marginally outperforms others during initial phases, achieving 0.02 m lower lateral errors within the first 10 s.

Figs. 17 and 18 illustrate the positional and attitude tracking errors under different delay estimates. In all three cases, the tracking errors are stabilized within a bounded small neighborhood of the origin attachment, while maintaining compliance with the prescribed performance constraints.

Control forces and moments (see Figs. 19 and 20) maintain smooth profiles. The partial enlarged view demonstrates that control inputs and velocity responses exhibit consistent smoothness, with transient fluctuations confined to initial error phases and trajectory transitions. Velocity responses (see Figs. 21 and 22) further confirm stable transitions, with angular rates converge within 5 s regardless of delay uncertainties.

ITAE indicators in Fig. 23 quantitatively demonstrate system

robustness, with maximum variations of 12.7 % in positional ITAE (surge/sway/heave) and 17.7 % in angular ITAE (pitch/yaw). These results confirm that the prescribed performance mechanism effectively mitigates the impact of delay estimation inaccuracies. In the absence of initial deviations, the surge, pitch, and yaw channels exhibit significantly lower ITAE values compared to sway and heave axes.

# 5. Field test

To validate the practical applicability and reliability of the proposed control method under resource-limited conditions, the controller was deployed on a physical UUV system. Limited by safety requirements and experimental resources, partial validation tests were conducted in an open-water lake environment to simulate tunnel transition scenarios. Fig. 24 illustrates the experimental environment and UUV platform.

The tested UUV is a 6-degree-of-freedom (6-DOF) platform independently developed by our team, equipped with eight vectored thrusters to ensure sufficient propulsion and high maneuverability in confined spaces. The sensor suite includes a Global Positioning System (GPS) for global localization, a Doppler Velocity Log (DVL) for velocity measurement, and a high-precision Attitude and Heading Reference System (AHRS). Two laterally symmetric ranging sonars (RS) enable real-time detection of sidewalls or obstacles, while multiple LED lights and underwater cameras enhance detection capabilities in low-visibility conditions. The UUV's control system operates on a PC104 embedded computer module, with key platform parameters summarized in Table 2.

The input delays of thrusters were empirically estimated using a command-response measurement protocol. As shown in Fig. 25, a high-sampling-rate signal acquisition system recorded the time difference between command signals and thruster feedback signals. The delays  $t_d$  were defined as the time taken for the feedback signal to reach 90 % of the commanded value. Repeated experiments under varying loads yielded  $t_d \in [0.11s, 0.25s]$ .

Comparative field experiments were conducted between the proposed method and a classical PID algorithm for horizontal plane trajectory tracking. In these tests, the estimated unknown input delays were set to  $\hat{t}_d = 0.2s$ , and the prescribed performance parameters were adjusted to  $\rho_0^{\xi} = \rho_0^{\eta} = 1.5$ ,  $\rho_0^{\psi} = 0.5$ ,  $\rho_{\infty}^{\xi} = \rho_{\infty}^{\eta} = 0.25$ ,  $\rho_{\infty}^{\psi} = 0.08$  and  $\kappa^{\xi} = \kappa^{\eta} = \kappa^{\psi} = 0.5$  to accommodate environmental disturbances. Experimental results are shown in Figs. 26–29.

As depicted in Fig. 26, under wind, wave, and current disturbances, the PID controller exhibited steady-state deviations during mid-course tracking, with maximum longitudinal and lateral position errors of 0.84 m and 1.11 m, respectively. In contrast, the proposed method

![Figure 29: Thruster voltage variation in field experiments. The figure consists of eight subplots labeled T1 through T8, arranged in two rows of four. Each subplot shows Voltage (V) on the y-axis (ranging from -4 to 4) versus Time (s) on the x-axis (ranging from 0 to 100). Each plot compares the Proposed method (blue line) and the PID method (red line). The Proposed method consistently shows smoother voltage profiles with less high-frequency noise compared to the PID method across all eight thrusters.](9c2d934b3e757d887c4714eba96b6589_img.jpg)

Figure 29: Thruster voltage variation in field experiments. The figure consists of eight subplots labeled T1 through T8, arranged in two rows of four. Each subplot shows Voltage (V) on the y-axis (ranging from -4 to 4) versus Time (s) on the x-axis (ranging from 0 to 100). Each plot compares the Proposed method (blue line) and the PID method (red line). The Proposed method consistently shows smoother voltage profiles with less high-frequency noise compared to the PID method across all eight thrusters.

Fig. 29. Thruster voltage variation in field experiments.

maintained strict adherence to the reference trajectory, limiting maximum longitudinal and lateral deviations to 0.20 m and 0.15 m, respectively, owing to the prescribed performance constraints.

Figs. 27 and 28 provide further insights into the tracking performance. The PID controller suffered from oscillations and divergence during turns, primarily due to actuator hysteresis characteristics. Conversely, the proposed method suppressed these issues through delay compensation, achieving smooth trajectory tracking. Notably, both position and heading angle errors remained consistently within the prescribed performance bounds throughout the test.

Control input profiles in Fig. 29 demonstrate the enhanced stability of the proposed method. Thruster voltage variations maintained within  $\pm 2$  V despite external disturbances and unknown delays, whereas the PID controller generated irregular voltage spikes, potentially compromising actuator durability and system reliability over extended periods.

The open-water tests validated the controller's robustness to real-world uncertainties while highlighting the influence of environmental factors absent in idealized simulations. Although the lake environment lacks the confined geometry of actual tunnels, the results demonstrate the method's potential for field deployment, with performance degradation within acceptable safety margins. Future work will extend testing to enclosed hydraulic facilities to bridge the gap between open-water and tunnel.

# 6. Conclusion

This study proposes a prescribed-performance time-delay compensation controller (PPTDC) to address trajectory tracking challenges for UUVs in water conveyance tunnel inspection tasks, particularly during transitions between main and branch tunnels. The method integrates prescribed performance functions with historical input information, systematically maintaining transient and steady-state error bounds while compensating for unknown time-varying input delays. Notably, the controller features a simple structure and exhibits insensitivity to delay uncertainties, ensuring practical deployability in real-world UUV systems.

Comparative simulations demonstrate that PPTDC reduces positional and attitude tracking errors by approximately 50 % relative to conventional delay-compensation methods, achieving smoother control inputs and faster convergence rates. Robustness is further validated under  $\pm 20$  % delay estimation errors, where lateral deviations remain constrained within 0.08 m even in overestimated conditions. Field tests under real-world disturbances verify practical viability, limiting maximum positional errors to 0.20 m longitudinal and 0.15 m lateral, while maintaining errors within prescribed performance bounds.

These results bridge the gap between theoretical design and operational reliability in underwater infrastructure inspection. Future work will focus on testing in actual tunnel environments to address confined-space challenges.

# CRediT authorship contribution statement

**Liwen Zhang:** Writing – review & editing, Writing – original draft,

Validation, Methodology, Investigation, Formal analysis, Data curation.

**Yushan Sun:** Supervision, Resources, Project administration, Funding acquisition, Conceptualization. **Puxin Chai:** Validation, Data curation.

**Jiehui Tan:** Software. **Haotian Zheng:** Visualization.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# References

- de Cerqueira Gava, P.D., Jorge, V.A.M., Júnior, C.L.N., Adabo, G.J., 2020. AUV Cruising Auto Pilot for a Long Straight Confined Underwater Tunnel, pp. 1–8. <https://doi.org/10.1109/SysCon47679.2020.9275846>.
- Chen, H., Chen, Y., Wang, M., 2022. Trajectory tracking for underactuated surface vessels with time delays and unknown control directions. IET Control Theory & Appl. 16 (6), 587–599. <https://doi.org/10.1049/cth2.12250>.
- Dong, Y., Guo, L., Hao, J., 2018. Robust exponential stabilization for uncertain neural networks with interval time-varying delays by periodically intermittent control. Neural Comput. Appl. 32 (7), 2651–2664. <https://doi.org/10.1007/s00521-018-3671-2>.
- Fossen, T.I., 2011. *Handbook of Marine Craft Hydrodynamics and Motion Control*. John Wiley & Sons.
- Ghrab, S., Benamor, A., Messaoud, H., 2021. A new robust discrete-time sliding mode control design for systems with time-varying delays on state and input and unknown unmatched parameter uncertainties. Math. Comput. Simulat. 190, 921–945. <https://doi.org/10.1016/j.matcom.2021.06.009>.
- Guo, X., Liu, Z., Gao, C., 2022. Fault-tolerant adaptive control for uncertain switched systems with time-varying delay and actuator faults based on sliding mode technique. J. Franklin Inst. 359 (11), 5231–5250. <https://doi.org/10.1016/j.jfranklin.2022.05.046>.
- Guo, Y., Yu, C., Xiang, X., Liu, C., Lian, L., 2025. Path following control of an underactuated AUV: a prescribed performance and tunable prescribed time-based approach. Nonlinear Dyn. 113 (7), 7013–7028. <https://doi.org/10.1007/s11071-024-10717-5>.
- Hu, Y., Song, Z., Zhang, H., 2023. Adaptive sliding mode control with pre-specified performance settings for AUV's trajectory tracking. Ocean Eng. 287, 115882. <https://doi.org/10.1016/j.oceaneng.2023.115882>.
- Huang, J.Q., Lewis, F.L., 2003. Neural-network predictive control for nonlinear dynamic systems with time-delay. IEEE Trans. Neural Network. 14 (2), 377–389. <https://doi.org/10.1109/TNN.2003.809424>.
- Huang, R., Zhang, J., Zhang, X., 2016. Adaptive tracking control of uncertain switched non-linear systems with application to aircraft wing rock. IET Control Theory & Appl. 10 (15), 1755–1762. <https://doi.org/10.1049/iet-cta.2015.1335>.
- Karras, G.C., Bechlioulis, C.P., Abdella, H.K., Larkworthy, T., Kyriakopoulos, K., Lane, D., 2013. A Robust Sonar Servo Control Scheme for wall-following Using an Autonomous Underwater Vehicle, pp. 3893–3898. <https://doi.org/10.1109/ICRA.2013.6696913>.
- Li, J., Du, J., Chen, C.P., 2021. Command-filtered robust adaptive NN control with the prescribed performance for the 3-D trajectory tracking of underactuated AUVs. IEEE Transact. Neural Networks Learn. Syst. 33 (11), 6545–6557. <https://doi.org/10.1109/TNNLS.2021.3082407>.
- Li, J., Xiang, X., Liu, C., Yang, S., 2022. Robust seabed terrain following control of underactuated AUV with prescribed performance guidance law under time delay of actuator. J. Shanghai Jiao Tong Univ. (Sci.) 56 (7), 944–952. <https://doi.org/10.16183/j.cnki.jstju.2021.375>.
- Liu, Z., Lai, G., Zhang, Y., Chen, X., Chen, C.L., 2014. Adaptive neural control for a class of nonlinear time-varying delay systems with unknown hysteresis. IEEE Transact. Neural Networks Learn. Syst. 25 (12), 2129–2140. <https://doi.org/10.1109/TNNLS.2014.2305717>.
- Liu, Y.J., Tong, S., Chen, C.L., Li, D.J., 2016. Neural controller design-based adaptive control for nonlinear MIMO systems with unknown hysteresis inputs. IEEE Trans. Cybern. 46 (1), 9–19. <https://doi.org/10.1109/TCYB.2015.2388582>.
- Liu, H., Ma, N., Gu, X., 2018. Experimental study on ship-bank interaction of very large crude carrier in shallow water. J. Shanghai Jiaotong Univer. (Sci.) 23 (6), 730–739. <https://doi.org/10.1007/s12204-018-1999-5>.
- Mukherjee, K., Kar, I.N., Bhatt, R.K.P., 2015. Region tracking based control of an autonomous underwater vehicle with input delay. Ocean Eng. 99, 107–114. <https://doi.org/10.1016/j.oceaneng.2015.02.006>.
- Namadchian, Z., Rouhani, M., 2018. Adaptive neural tracking control of switched stochastic pure-feedback nonlinear systems with unknown bouc-wen hysteresis input. IEEE Transact. Neural Networks Learn. Syst. 29 (12), 5859–5869. <https://doi.org/10.1109/TNNLS.2018.2815579>.
- Niculescu, S.I., de Souza, C.E., Dugard, L., Dion, J.M., 1998. Robust exponential stability of uncertain systems with time-varying delays. IEEE Trans. Automat. Control 43 (5), 743–748. <https://doi.org/10.1109/9.668851>.
- Peng, C., Tian, Y.C., 2008. Improved delay-dependent robust stability criteria for uncertain systems with interval time-varying delay. IET Control Theory & Appl. 2 (9), 752–761. <https://doi.org/10.1049/iet-cta.20070362>.
- Pettersen, K.Y., Egeland, O., 1999. Time-varying exponential stabilization of the position and attitude of an underactuated autonomous underwater vehicle. IEEE Trans. Automat. Control 44 (1), 112–115. <https://doi.org/10.1109/9.739086>.
- Qiao, L., Yi, B., Wu, D., Zhang, W., 2017. Design of three exponentially convergent robust controllers for the trajectory tracking of autonomous underwater vehicles. Ocean Eng. 134, 157–172. <https://doi.org/10.1016/j.oceaneng.2017.02.006>.
- Qiao, L., Ruan, S., Zhang, G., Zhang, W., 2018. Robust H2 optimal depth control of an autonomous underwater vehicle with output disturbances and time delay. Ocean Eng. 165, 399–409. <https://doi.org/10.1016/j.oceaneng.2018.07.019>.
- Rong, S., Wang, H., Li, H., Sun, W., Gu, Q., Lei, J., 2022. Performance-guaranteed fractional-order sliding mode control for underactuated autonomous underwater vehicle trajectory tracking with a disturbance observer. Ocean Eng. 263, 112330. <https://doi.org/10.1016/j.oceaneng.2022.112330>.
- Sharma, N., Bhasin, S., Wang, Q., Dixon, W.E., 2011. Predictor-based control for an uncertain Euler-Lagrange system with input delay. Automatica 47 (11), 2332–2342. <https://doi.org/10.1016/j.automatica.2011.03.016>.

- Sun, H., Zong, G., Cui, J., Shi, K., 2022. Fixed-time sliding mode output feedback tracking control for autonomous underwater vehicle with prescribed performance constraint. *Ocean Eng.* 247, 110673. <https://doi.org/10.1016/j.oceaneng.2022.110673>.
- Sun, Y., Zhang, Y., Qin, H., Ouyang, L., Jing, R., 2023. Predefined-time prescribed performance control for AUV with improved performance function and error transformation. *Ocean Eng.* 281, 114817. <https://doi.org/10.1016/j.oceaneng.2023.114817>.
- Vasquez-Beltran, M.A., Jayawardhana, B., Peletier, R., 2021. Recursive algorithm for the control of output remnant of preisach hysteresis operator. *IEEE Contr. Syst. Lett.* 5 (3), 1061–1066. <https://doi.org/10.1109/lcsys.2020.3009423>.
- Wang, F., Liu, Z., Zhang, Y., Chen, C.L.P., 2016. Adaptive fuzzy control for a class of stochastic pure-feedback nonlinear systems with unknown hysteresis. *IEEE Trans. Fuzzy Syst.* 24 (1), 140–152. <https://doi.org/10.1109/tfuzz.2015.2446531>.
- Wang, X., Zhang, G., Sun, Y., Cao, J., Wan, L., Sheng, M., Liu, Y., 2019. AUV near-wall-following control based on adaptive disturbance observer. *Ocean Eng.* 190, 106429. <https://doi.org/10.1016/j.oceaneng.2019.106429>.
- Wang, X., Sun, Y., Wan, L., Bian, H., Ran, X., 2020a. Design and reliability analysis of a tunnel-detection AUV based on a heterogeneous dual CPU hot redundancy system. *Electronics* 10 (1), 22. <https://doi.org/10.3390/electronics10010022>.
- Wang, X., Zhang, G., Sun, Y., Wan, L., Cao, J., 2020b. Research on autonomous underwater vehicle wall following based on reinforcement learning and multi-sonar weighted round robin mode. *Int. J. Adv. Rob. Syst.* 17 (3), 1729881420925311. <https://doi.org/10.1177/1729881420925311>.
- Wang, Z., Lou, J., Yang, H., Chen, T., Wei, Y., Xu, C., Cui, Y., 2023. Underwater dynamic hysteresis modeling and feedforward control of flexible caudal fin actuated by macro fiber composites. *J. Sound Vib.* 556, 117717. <https://doi.org/10.1016/j.jsv.2023.117717>.
- Xia, T., Cui, D., Chu, Z., Yu, X., 2023. Autonomous heading planning and control method of unmanned underwater vehicles for tunnel detection. *J. Mar. Sci. Eng.* 11 (4), 740. <https://doi.org/10.3390/jmse11040740>.
- Yan, J., Gao, J., Yang, X., Luo, X., Guan, X., 2019. Tracking control of a remotely operated underwater vehicle with time delay and actuator saturation. *Ocean Eng.* 184, 299–310. <https://doi.org/10.1016/j.oceaneng.2019.04.041>.
- Yue, D., 2004. Robust stabilization of uncertain systems with unknown input delay. *Automatica* 40 (2), 331–336. <https://doi.org/10.1016/j.automatica.2003.10.005>.
- Zhang, C., Gan, W., Chu, Z., Di, H., 2023a. A Launch Device for Autonomous Underwater Vehicle Used in Water Conveyance Tunnel, pp. 46–51. <https://doi.org/10.1109/CACRES8689.2023.10208443>.
- Zhang, J., Xiang, X., Li, W., Zhang, Q., 2023b. Adaptive saturated path following control of underactuated AUV with unmodeled dynamics and unknown actuator hysteresis. *IEEE Transact. Syst. Man Cybernet.: Syst.* 53 (10), 6018–6030. <https://doi.org/10.1109/tsmc.2023.3280065>.
- Zhang, J.X., Ding, J.L., Chai, T.Y., 2024a. Fault-tolerant prescribed performance control of wheeled Mobile robots: a mixed-gain adaption approach. *IEEE Trans. Automat. Control* 69 (8), 5500–5507. <https://doi.org/10.1109/Tac.2024.3365726>.
- Zhang, J.X., Xu, K.D., Wang, Q.G., 2024b. Prescribed performance tracking control of time-delay nonlinear systems with output constraints. *IEEE-Caa J. Automat. Sinica* 11 (7), 1557–1565. <https://doi.org/10.1109/Jas.2023.123831>.
- Zhao, J., 2018. Neural network predictive control for autonomous underwater vehicle with input delay. *J. Control Sci. Eng.* 2018 (1), 1–8. <https://doi.org/10.1155/2018/2316957>.
- Zhao, J., Hu, Z., 2017. Path Following Control of discrete-time AUV with input-delay, pp. 4648–4652. <https://doi.org/10.1109/CCDC.2017.7979318>.
- Zhao, J., Cai, C., Qiao, R., 2023. Finite-time dynamic prescribed performance control for surface unmanned vehicles with unknown disturbances. *CAAI Transact. Intell. Syst.* 18 (4), 849–857. <https://doi.org/10.11992/tis.202209031>.
- Zhou, J., Zhao, X., Feng, Z., Wu, D., 2020. Trajectory tracking sliding mode control for underactuated autonomous underwater vehicles with time delays. *Int. J. Adv. Rob. Syst.* 17 (3), 1729881420916276. <https://doi.org/10.1177/1729881420916276>.
- Zhou, H., Fu, J., Zeng, Z., Yu, C., Wei, Z., Yao, B., Lian, L., 2021. Adaptive robust tracking control for underwater gliders with uncertainty and time-varying input delay. *Ocean Eng.* 240, 109945. <https://doi.org/10.1016/j.oceaneng.2021.109945>.