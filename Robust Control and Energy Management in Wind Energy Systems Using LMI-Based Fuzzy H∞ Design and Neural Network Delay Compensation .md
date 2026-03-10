

## Article

# Robust Control and Energy Management in Wind Energy Systems Using LMI-Based Fuzzy $H_\infty$ Design and Neural Network Delay Compensation <sup>†</sup>

Kaoutar Lahmadi <sup>1,\*</sup> ![ORCID icon](c3d993ca47bfe2a953c700506ce31fa0_img.jpg), Oumaima Lahmadi <sup>2</sup>, Soufiane Jounaidi <sup>3</sup> and Ismail Boumhidi <sup>4</sup>

<sup>1</sup> Laboratory of Innovation in Management and Engineering (LIMIE), Edvantis Higher Education Group, ISGA, Fez 30050, Morocco

<sup>2</sup> Engineering Systems and Applications Laboratory, National School of Applied Sciences, Sidi Mohamed Ben Abdellah University, Fez 30050, Morocco; lahmadiumaima6@gmail.com

<sup>3</sup> Laboratory of Innovation in Management and Engineering (LIMIE), Edvantis Higher Education Group, ISGA, Casablanca 20250, Morocco; soufiane.jounaidi@isga.ma

<sup>4</sup> Department of physics, Faculty of Sciences Dhar el Mahraz, University Sidi Mohammed Ben Abdellah, Fez 30050, Morocco; ismail.boumhidi@usmba.ac.ma

\* Correspondence: kaoutar.lahmadi@isga.ma

<sup>†</sup> Note: This article is an extended and revised version of the paper presented at the '5th Winter IFSA Conference on Automation, Robotics & Communications for Industry 4.0/5.0 (ARCI' 2025), Granada, Spain, 19–21 February 2025: "Fuzzy  $H_\infty$  Robust Control and Neural Network-Based Delayed-Input Strategies for Uncertain Wind Energy Systems Using LMI Approach", published in the conference proceedings of <http://dx.doi.org/10.13140/RG.2.2.13085.63208>.

![Check for updates icon](d3294dc879b451b369c0b06f42e9b39f_img.jpg)

Check for updates icon

Academic Editor: Sergey Y. Yurish

Received: 7 April 2025

Revised: 26 May 2025

Accepted: 6 June 2025

Published: 2 July 2025

**Citation:** Lahmadi, K.; Lahmadi, O.; Jounaidi, S.; Boumhidi, I. Robust Control and Energy Management in

Wind Energy Systems Using LMI-Based Fuzzy  $H_\infty$  Design and Neural Network Delay Compensation. *Processes* **2025**, *13*, 2097. <https://doi.org/10.3390/pr13072097>

**Copyright:** © 2025 by the authors.

Licensee MDPI, Basel, Switzerland.

This article is an open access article

distributed under the terms and conditions of the Creative Commons Attribution (CC BY) license (<https://creativecommons.org/licenses/by/4.0/>).

## Abstract

This study presents advanced control and energy management strategies for uncertain wind energy systems using a Takagi-Sugeno (T-S) fuzzy modeling framework. To address key challenges, such as system uncertainties, external disturbances, and input delays, the study integrates a fuzzy  $H_\infty$  robust control approach with a neural network-based delay compensation mechanism. A fuzzy observer-based  $H_\infty$  tracking controller is developed to enhance robustness and minimize the impact of disturbances. The stability conditions are rigorously derived using a quadratic Lyapunov function,  $H_\infty$  performance criteria, and Young's inequality and are expressed as Linear Matrix Inequalities (LMIs) for computational efficiency. In parallel, a neural network-based controller is employed to compensate for the input delays introduced by online learning processes. Furthermore, an energy management layer is incorporated to regulate the power flow and optimize energy utilization under varying operating conditions. The proposed framework effectively combines control and energy coordination to improve the systems' performance. The simulation results confirm the effectiveness of the proposed strategies, demonstrating enhanced stability, robustness, delay tolerance, and energy efficiency in wind energy systems.

**Keywords:** wind energy systems; management energy system;  $H_\infty$  control; neural networks; delayed-input compensation; fuzzy observer; Takagi-Sugeno model; robust control; Linear Matrix Inequalities (LMIs); tracking control; PDC strategy

## 1. Introduction

Wind energy technology has rapidly advanced over the last few decades, emerging as one of the most competitive and cost-effective sources of renewable energy globally. Wind turbine systems, which consist of turbines, driving shafts, and double-fed induction machines, are essential for efficiently converting wind energy into electricity [1]. The

primary objective of controlling these systems is to maximize energy extraction while minimizing operational stresses and disturbances. Due to the unpredictable and fluctuating nature of wind, effective control strategies are crucial to ensuring optimal performance, enhanced energy conversion efficiency, improved power quality, and system reliability.

In the context of wind turbine control, the Takagi–Sugeno (T-S) fuzzy model has gained significant attention due to its ability to handle complex nonlinear systems with uncertain parameters. This approach utilizes if–then rules and membership functions to create a piece-wise linear approximation of a nonlinear system, providing a flexible and efficient solution for wind turbine control [2]. The T-S fuzzy model has proven effective in addressing uncertainties in dynamic systems, making it highly suitable for wind turbine applications. For a detailed understanding of T-S fuzzy modeling, the work of Tanaka and Wang can be referenced [3].

A key challenge in wind turbine control is the need for robust tracking control to minimize errors between the desired reference trajectories and the actual system outputs while ensuring stability under external disturbances [4]. Despite the substantial body of research on stability conditions for T-S fuzzy models, few studies have directly addressed the tracking problem. The challenge lies in reducing the tracking error between the desired reference trajectories and the actual system outputs while maintaining system stability in the presence of disturbances [5]. This paper aims to address the tracking control problem by proposing a fuzzy observer-based tracking control law that guarantees the asymptotic tracking of reference signals, ensuring system stability under various external disturbances, such as wind speed fluctuations [6]. A unique aspect of this study is the integration of neural networks into the T-S fuzzy approach to manage disturbances and uncertainties in the wind energy system [6]. Neural networks offer an intelligent approach to online learning and adaptive control, providing the flexibility to estimate and compensate for system uncertainties [7]. However, a significant challenge when incorporating neural networks into control systems is the delay introduced by the online learning process. This delay must be accounted for to ensure the systems' stability and performance [8].

To address this issue, this work develops new stabilization conditions for delayed-input systems, ensuring both robustness and performance, despite the delay. These stabilization conditions are derived using a Lyapunov function and combined with  $H_\infty$  tracking criteria to guarantee system stability and performance in the presence of disturbances, such as variations in wind speed [9]. The proposed methodology is formulated as a Linear Matrix Inequality (LMI) problem, which can be efficiently solved using convex optimization techniques [10]. This approach ensures the robustness of the control system while minimizing the tracking errors caused by disturbances, improving the overall performance of the wind turbine systems [11,12]. In addition to the control strategies, this study proposes an energy management strategy for wind energy systems, particularly addressing the intermittent nature of wind power. The proposed strategy aims to optimize the energy output while ensuring the safety and reliability of the wind turbine system. The strategy integrates fuzzy control techniques for maximum power extraction from the wind system, while battery storage is used to supply energy when the wind system cannot meet the energy demand. The energy management system also includes a backup battery and a diesel generator to protect the battery from overcharging and deep discharging, thus extending its lifespan [13,14]. To model and simulate the energy management strategy, the Stateflow approach in MATLAB/Simulink is used, providing a graphical interface for interactions with the models and simulations. This tool allows for testing various load scenarios and demonstrating the behavior of the management algorithm under different operating conditions.

The proposed integrated control and energy management strategies provide significant improvements in the stability, robustness, energy efficiency, and tracking performance of wind energy systems, contributing to the growth and sustainability of wind energy as a clean and reliable renewable energy source [15].

The paper is organized as follows: Section 2 introduces the T-S fuzzy model for wind turbine systems with external disturbances and tracking control criteria. Section 3 discusses the design of the neural network-based fuzzy observer and tracking control law. Section 4 presents the development of sufficient conditions for stabilization, utilizing Lyapunov functions. Section 5 focuses on energy management strategies, including the optimization of energy extraction, battery storage management, and protection mechanisms. Section 6 demonstrates the effectiveness of the proposed approach through simulation results, while Section 7 concludes the paper.

## 2. Problem Formulation

### 2.1. T-S Fuzzy Model

Let us consider the T-S fuzzy system with uncertainties parameters. The if-then rule is described as follows:

Plant rule:

If  $z_1(t)$  is  $N_{i1}$  and ... and  $z_p(t)$  is  $N_{ip}$ ,

$$\text{then } \begin{cases} \dot{x}(t) = (A_i + \Delta A_i)x(t) + (B_i + \Delta B_i)u(t) + B_{2i}\phi(t) \\ y(t) = C_i x(t) \end{cases} \quad (1)$$

where  $N_{ij}$  is a fuzzy set,  $x(t) \in R^n$  is the system state vector,  $u(t) \in R^m$  is the control input vector,  $\phi(t) \in R^p$  is the disturbance input vector,  $y(t) \in R^p$  is the system output,  $A_i, B_i, C_i$  are known constant matrices that describe the nominal system, and  $z_1(t) = [z_1(t), z_2(t), \dots, z_p(t)]$  are the premise variables. The Lebesgue measurable uncertainties are defined as  $\Delta A_i(t) = H_i F_i(t) E_{ai}$ ,  $\Delta B_i(t) = H_i F_i(t) E_{bi}$ , where matrices  $H_i, E_{ai}$ , and  $E_{bi}$  are constants of appropriate dimensions, and  $F(t)$  is an unknown matrix function, which is bounded by  $F_i^T(t) F_i(t) \le I$ .

Given a pair of  $(x(t), u(t))$ , the final outputs of the fuzzy systems are inferred as follows:

$$\dot{x}(t) = \frac{\sum_{i=1}^{r} \mu_i(z(t)) [(A_i + \Delta A_i(t))x(t) + (B_i + \Delta B_i(t))u(t) + B_{2i}\omega(t)]}{\sum_{i=1}^{r} \mu_i(z(t))}$$

where  $\mu_i = \prod_{j=1}^{n} N_{ij}(z_j(t))$  and  $h_i(z(t)) = \frac{\mu_i(z(t))}{\sum_{i=1}^{r} \mu_i(z(t))}$

The defuzzification process of the TS fuzzy model (1) with uncertainties parameters can be represented as follows:

$$\begin{cases} \dot{x}(t) = \sum_{i=1}^{r} h_i(z(t)) [(A_i + \Delta A_i(t))x(t) + (B_i + \Delta B_i(t))u(t) + B_{2i}\phi(t)] \\ y(t) = \sum_{i=1}^{r} h_i(z(t)) C_i x(t) \\ i = 1, 2, \dots, r \end{cases} \quad (2)$$

### 2.2. Wind System

In this study, the wind energy conversion system (WECS) comprises a wind turbine connected to an electrical generator via a drive train. Due to fluctuations in wind speed caused by climatic variations, the natural rotational speed of the turbine is often insufficient for optimal energy production. To address this, a mechanical speed multiplier represented as a gain factor, is introduced between the turbine and the generator. This component helps the system operate near its optimal rotational speed [16,17]. Additionally, to ensure the tur-

turbine consistently functions at the maximum power point, a control system is implemented, as illustrated in Figure 1.

![Block diagram of the control strategy for a wind energy conversion system (WECS). The diagram shows the flow of signals between several components: Wind Speed, Wind Turbine Model, Mass Drive Train and multiplier, Generator Model, Power System, and Control System. Wind Speed enters the Wind Turbine Model. The Wind Turbine Model outputs torque (Tm) and angular velocity (omega_r) to the Mass Drive Train and multiplier. The Mass Drive Train and multiplier outputs torque (Te) and angular velocity (omega_g) to the Generator Model. The Generator Model outputs voltage (V) and current (I) to the Power System. The Control System receives feedback from the Wind Turbine Model (beta), the Mass Drive Train and multiplier (Teref), and the Generator Model (Te). The Control System outputs a reference pitch angle (beta_ref) to the Wind Turbine Model. The Wind Turbine Model also outputs the actual pitch angle (beta).](d3ca266c298aeb34b019960c6c36f187_img.jpg)

Block diagram of the control strategy for a wind energy conversion system (WECS). The diagram shows the flow of signals between several components: Wind Speed, Wind Turbine Model, Mass Drive Train and multiplier, Generator Model, Power System, and Control System. Wind Speed enters the Wind Turbine Model. The Wind Turbine Model outputs torque (Tm) and angular velocity (omega\_r) to the Mass Drive Train and multiplier. The Mass Drive Train and multiplier outputs torque (Te) and angular velocity (omega\_g) to the Generator Model. The Generator Model outputs voltage (V) and current (I) to the Power System. The Control System receives feedback from the Wind Turbine Model (beta), the Mass Drive Train and multiplier (Teref), and the Generator Model (Te). The Control System outputs a reference pitch angle (beta\_ref) to the Wind Turbine Model. The Wind Turbine Model also outputs the actual pitch angle (beta).

Figure 1. Control strategy of wind energy conversion system [18].

To illustrate the proposed fuzzy robust tracking control condition, a control problem of a wind generator is considered.

By defining the state vector as  $x(t) = [\theta_s \quad \Omega_r \quad \Omega_g \quad \beta]^T$  and the control signal as

$$u = [\beta_d, \Omega_z]^T,$$

the reference state vector to track can be defined as

$$x_r(t) = [\theta_{rs} \quad \Omega_{rr} \quad \Omega_{gr} \quad \beta_r]^T$$

and the fuzzy model of the WECS can be described as

$$\begin{cases} \dot{x}(t) = A(z)x(t) + Bu(t) + B_2V(t) \\ y(t) = Cx(t) \end{cases} \quad (3)$$

where

$$A(z) = \begin{bmatrix} 0 & 1 & -1 & 0 \\ -\frac{K_s}{J_r} & -\frac{B_s}{J_r} & \frac{B_s}{J_r} & \frac{T_r\beta(z_0)}{J_r} \\ \frac{K_s}{J_g} & \frac{B_s}{J_g} & -\frac{(B_s+B_g)}{J_g} & 0 \\ 0 & 0 & 0 & -\frac{1}{\tau} \end{bmatrix}$$

$$B = \begin{bmatrix} 0 & 0 \\ 0 & 0 \\ 0 & \frac{B_s}{J_g} \\ \frac{1}{\tau} & 0 \end{bmatrix} \quad B_2 = \begin{bmatrix} 0 \\ \frac{T_{r0}(z_0)}{J_r} \\ 0 \\ 0 \end{bmatrix}$$

$$C = \begin{bmatrix} 0 & 0 & 1 & 0 \end{bmatrix}$$

where  $\theta_s$  denotes the torsion angle,  $\Omega_r$  is the angular velocity of the rotor,  $\Omega_g$  is the angular velocity of the generator,  $K_s$  is the stiffness of the transmission,  $B_s$  is the damping of the transmission, and  $J_r$  and  $J_g$  are the inertia of the rotor and the generator, respectively.

$T_r$  is the aerodynamic torque.  $\beta$  and  $\beta_d$  are the actual and desired pitch angles, respectively.

### 2.3. T-S Fuzzy Representation

The wind generator system is then described by the following four if-then rules:

If  $\beta$  is  $F_1^1$ , and  $V$  is  $F_2^1$ , then

$$\begin{cases} \dot{x} = A_1x + B_1u + B_{21}\phi \\ y = Cx \end{cases}$$

If  $\beta$  is  $F_1^1$ , and  $V$  is  $F_2^2$ , then

$$\begin{cases} \dot{x} = A_2x + B_2u + B_{22}\phi \\ y = Cx \end{cases}$$

If  $\beta$  is  $F_1^2$ , and  $V$  is  $F_2^1$ , then

$$\begin{cases} \dot{x} = A_3x + B_3u + B_{23}\phi \\ y = Cx \end{cases}$$

If  $\beta$  is  $F_1^2$ , and  $V$  is  $F_2^2$ , then

$$\begin{cases} \dot{x} = A_4x + B_4u + B_{24}\phi \\ y = Cx \end{cases}$$

### 2.4. Observer Design

In this study, we address the scenario where the state variables required for feedback control are unavailable due to an unmeasurable premise variable. To tackle this, a T-S observer is proposed to estimate the states of the T-S nonlinear system described in Equation (2).

$$\begin{cases} \dot{\hat{x}}(t) = \sum_{i=1}^{r} A_i \hat{x}(t) + B_i u(t) + G_i (y(t) - \hat{y}(t)) \\ \hat{y}(t) = \sum_{i=1}^{r} C_i \hat{x}(t) \end{cases} \quad (4)$$

where  $G_i (i = 1, \dots, r)$  are the observers' gains to be determined, and  $\hat{x}(t)$  is the state estimation.

Let us define the state estimation error,  $e_x(t)$ , as follows:

$$e_x(t) = x(t) - \hat{x}(t) \quad \dot{e}_x(t) = \dot{x}(t) - \dot{\hat{x}}(t) \quad (5)$$

### 2.5. Tracking Criteria

To deal with the tracking problem for the T-S fuzzy system, we consider the following reference model:

$$\dot{x}_r(t) = A_r(t)x_r(t) + r(t) \quad (6)$$

$x_r(t)$  is the reference state;

$A_r(t)$  is a specified asymptotically stable matrix;

$r(t)$  is a bounded reference input.

Then the objective is to design a T-S fuzzy model-based controller, which stabilizes the fuzzy system (2) and achieves the  $H_\infty$  tracking performance related to the tracking error,  $e_r(t)$ , as follows:

$$\int_0^{t_f} e_r^T(t) Q e_r(t) d(t) \le \eta^2 \int_0^{t_f} \bar{\varphi}^T(t) \bar{\varphi}(t) d(t) \quad (7)$$

where  $t_f$  denotes the final time,  $Q$  is a positive definite weighting matrix, and  $\eta$  is a specified attenuation level.

The tracking error is defined by

$$e_r(t) = x(t) - x_r(t) \quad \dot{e}_r(t) = \dot{x}(t) - \dot{x}_r(t) \quad (8)$$

### 2.6. Tracking Control

Suppose the following fuzzy controller is employed to deal with the above control system design, then the control structure is chosen as a PDC law:

$$u(t) = -\sum_{i=1}^{r} h_i(z(t)) k_i (x_r(t) - \hat{x}(t)) \quad (9)$$

where  $k_i$  represents the gain matrices with appropriate dimensions.

Let us consider the estimation error  $e_x(t) = x(t) - \hat{x}(t)$  and the tracking error state reference  $e_r(t) = x(t) - x_r(t)$ .

Some easy manipulations lead to the following augmented system:

$$\dot{x}_a(t) = \sum_{i=1}^{r} \sum_{j=1}^{r} h_i(z(t)) h_j(z(t)) (\bar{A}_{ij}(t) x_a(t) + \bar{S} \bar{\varphi}(t)) \quad (10)$$

where

$$\bar{\varphi}(t) = \begin{bmatrix} r(t) \\ \phi(t) \end{bmatrix}, \quad \bar{S}(t) = \begin{bmatrix} -I & B_{2i} \\ 0 & B_{2i} \\ I & 0 \end{bmatrix}$$

$$\bar{A}_{ij}(t) = \begin{bmatrix} A_i + \Delta A_i(t) + B_i k_j + \Delta B_i(t) k_j & -B_i k_j - \Delta B_i(t) k_j & A_i - A_r + \Delta A_i(t) \\ \Delta A_i(t) + \Delta B_i(t) k_j & A_i - L_j C_i - \Delta B_i(t) k_j & \Delta A_i(t) \\ 0 & 0 & A_r \end{bmatrix}$$

Hence, the tracking criteria  $H_\infty$  (6) with the augmented vector  $x_a(t)$  can be modified as follows:

$$\int_0^{t_f} x_a^T(t) Q_a x_a(t) d(t) \le \eta^2 \int_0^{t_f} \bar{\varphi}^T(t) \bar{\varphi}(t) d(t) \quad (11)$$

with

$$Q_a = (Q, 0, 0, 0) \text{ and } \bar{\varphi}^T(t) \bar{\varphi}(t) = r^T(t) r(t) + \phi^T(t) \phi(t)$$

## 3. Neural Network Representation

To eliminate errors and uncertainties arising from modeling, the neural network approach is employed to minimize the error between the nominal system output and the actual system output. The unknown term, estimated by the neural networks, is added to the nominal system to make it more representative of reality [19,20].

$$e_{RN} = y_r(t) - y(t) \quad (12)$$

where  $y(t)$  is the output of the nominal system.

$$y_r(t) = y_n(t) + \hat{\xi}(x, w)$$

The neural network considered is a multi-layer perceptron (MLP), a type of predictive network. Figure 1 illustrates the proposed neural network architecture, with the output variable calculated using the following equation:

$$\hat{\xi}(x, w) = \sum_{k=1}^{N} (w_k \sigma_c(\sum_{j=1}^{n} w_j x_j)) \quad (13)$$

In this study, a neural network—specifically a multi-layer perceptron (MLP)—is employed as an intelligent estimation and compensation mechanism to address input delays and modeling uncertainties within the wind energy system. The main objective is not to directly control the system but to enhance the accuracy of the control strategy by minimizing the mismatch between the nominal system output and the actual system behavior.

The neural network estimates unknown nonlinearities or uncertainties that are not captured by the nominal Takagi–Sugeno fuzzy model. These unknown components may stem from unmodeled dynamics, time-varying disturbances, or approximation errors. By learning these deviations in real-time, the neural network produces an adaptive corrective signal, which is then integrated back into the control input to compensate for delays and improve the tracking accuracy.

Equation (12) reflects the error between the nominal and the actual system outputs; the neural network works to minimize this error using a gradient descent-based online learning algorithm. The learning updates are computed iteratively to ensure the neural network adapts to changing system conditions.

The structure of the MLP is shown in Figure 2, where

- The input layer receives measured system variables.
- The hidden layer processes the input using a tanh activation function, offering nonlinearity.
- The output layer generates the estimated compensation signal.

The weights between the layers are continuously updated to optimize performance during real-time operation. This adaptive learning ensures that the neural network maintains an accurate model of the delay-induced uncertainty, even under varying operating conditions or in the presence of non-Gaussian disturbances.

By embedding this learned compensation term into the control framework, the overall system gains improved robustness, delay tolerance, and dynamic performance, without requiring an exact analytical model of the uncertainties or delays. The neural network thus plays a supporting, but crucial, role in ensuring the robustness and adaptability of the overall control scheme [21].

![Diagram of a Multi-Layer Perceptron (MLP) neural network architecture. It consists of three layers: an input layer with nodes x1, x2, ..., xn; a hidden layer with nodes sigma_c(.), sigma_c(.), ..., sigma_c(.); and an output layer with a summation node Sigma. A bias node labeled -1 is connected to the hidden layer. Weights w_j are shown connecting the input layer to the hidden layer, and weights w_k are shown connecting the hidden layer to the output layer. The output is labeled as the estimated compensation signal, z-hat(x, w).](9791722d75115ddcc599b07d7bc35d73_img.jpg)

Diagram of a Multi-Layer Perceptron (MLP) neural network architecture. It consists of three layers: an input layer with nodes x1, x2, ..., xn; a hidden layer with nodes sigma\_c(.), sigma\_c(.), ..., sigma\_c(.); and an output layer with a summation node Sigma. A bias node labeled -1 is connected to the hidden layer. Weights w\_j are shown connecting the input layer to the hidden layer, and weights w\_k are shown connecting the hidden layer to the output layer. The output is labeled as the estimated compensation signal, z-hat(x, w).

**Figure 2.** The neural network's architecture [22].

Where something is the activation function, considered as a hyperbolic tangent function (tanh),  $N$  and  $n$  are, respectively, the number of hidden layer nodes and the number of network inputs. In addition, something and something are, respectively, the weights between the hidden layer and the output layer and the weights between the hidden layer and that of the input network.

The network weights are adjusted during the online implementation. The method used is based on the gradient descent method (GD). The essence of the GD method consists of iteratively adjusting the weights in the direction opposite to the gradient of  $E$ , so as to reduce the discrepancy according to the following:

$$\frac{dw}{dt} = -\eta_k \frac{\partial E}{\partial w} = -\eta_k \frac{1}{2} \frac{\partial}{\partial w} (e_{RN}^2) \quad (14)$$

### The Delayed PDC Control

The most widely used control strategy for stabilizing nonlinear systems represented by T-S models is the Parallel Distributed Compensation (PDC) control approach [23]. The control law employed in this method is similar to that of a standard PDC controller [24], with the key difference being that it depends on the delayed state of the system. It is expressed as follows:

$$u(t) = -\sum_{i=1}^{r} h_i(z(t-\tau(t))) k_i x(t-\tau(t)) \quad (15)$$

## 4. Robust Control with a Delayed Input

In this section, we address the problem of control with a delayed input. First, let us consider the system (2). The system, along with its control law, can be rewritten in the following form:

$$\dot{x}(t) = \sum_{i=1}^{r} \sum_{j=1}^{r} h_i(z(t)) h_j(z(t-\tau(t))) [A_i x(t) - B_i k_j x(t-\tau(t)) + B_{2i} \delta(t)] \quad (16)$$

$$\begin{cases} \dot{x}(t) = \sum_{i=1}^{r} \sum_{j=1}^{r} h_i(z(t)) h_j(z(t-\tau(t))) [A_i x(t) - B_i k_j x(t-\tau(t)) + B_{2i} \delta(t)] \\ \dot{e}(t) = \sum_{i=1}^{r} \sum_{j=1}^{r} h_i(z(t)) h_j(z(t)) [(A_i - L_j C_i) e(t) + B_{2i} \delta(t)] \end{cases}$$

**Theorem 1.** For the two given scalars,  $\gamma > 0$  and  $\tau > 0$ , the system is asymptotically stable if there exist positive, definite, symmetric matrices,  $X > 0$ ,  $Q > 0$ ,  $S > 0$ ,  $R > 0$ , and appropriately dimensioned matrices,  $M_i (i = 1, 2, 3)$ ,  $Y_j (j = 1, 2, \dots, r)$ ,  $L_j (j = 1, 2, \dots, r)$ , such that the following LMI condition is satisfied.

$$\bar{\Omega}_{ij} = \begin{bmatrix} \bar{\Omega}_{11} & 0 & 0 & \bar{\Omega}_{14} & 0 & \bar{\Omega}_{16} & 0 & X & B_{2i}X \\ * & \bar{\Omega}_{22} & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\ * & * & \bar{\Omega}_{33} & 0 & 0 & 0 & 0 & 0 & S B_{2i} \\ * & * & * & \bar{\Omega}_{44} & T_2 - T_1^T & M_3 - M_2^T & T_3 - T_1^T & 0 & 0 \\ * & * & * & * & -Q - T_2 - T_2^T & 0 & -T_3 - T_2^T & 0 & 0 \\ * & * & * & * & * & \bar{\Omega}_{66} & 0 & 0 & 0 \\ * & * & * & * & * & * & \bar{\Omega}_{77} & 0 & 0 \\ * & * & * & * & * & * & * & -Q^{-1} - Z^{-1} & 0 \\ * & * & * & * & * & * & * & * & -\gamma^2 I \end{bmatrix} < 0$$

## 5. Energy Management Algorithm

The algorithm presented in Figure 3 outlines the energy management system we implemented using the Stateflow tool. This system is designed to handle various operational scenarios that may arise. The wind energy management strategy proposed here effectively manages both the wind power input and energy storage, ensuring the battery is safeguarded against excessive discharge and overcharging.

**The control logic** relies on three key input parameters:

**Pwind:** The available wind power.

**Pload:** The power demand from the load.

**SOC** (state of charge): The battery charge level, where the SOC is constrained between a minimum of 20% (to prevent deep discharging) and a maximum of 80% (to avoid overcharging).

![Flowchart of the management energy algorithm of the wind system. The process starts with 'Measure Pwind, Pload'. It then checks if 'SOC min <= SOC <= SOC max'. If 'Yes', it checks 'Pwind > Pload'. If 'Yes' to this, it leads to 'Case 1: Connection Pwind with Load and Battery (S1+S2)'. If 'No' to 'Pwind > Pload', it leads to 'Case 2: Connection Battery with Load (S1+S2)'. If 'No' to 'SOC min <= SOC <= SOC max', it checks 'SOC > SOC max'. If 'Yes' to this, it leads to 'Case 3: Connection Battery with Load and Pwind with Battery_backup (S1+S2+S3)'. If 'No' to 'SOC > SOC max', it checks 'Pwind > Pload'. If 'Yes' to this, it leads to 'Case 4: Connection Pwind with Load and Battery (S1+S2)'. If 'No' to 'Pwind > Pload', it leads to 'Case 5: Connection PLoad with Diesel Generator (S4)'. All cases lead to a 'Return' block.](562f471e8153729557e6a4ee6343c32c_img.jpg)

```

graph TD
    Start[Measure Pwind, Pload] --> SOC{SOC min <= SOC <= SOC max}
    SOC -- Yes --> Pwind{Pwind > Pload}
    Pwind -- Yes --> Case1[Case 1  
Connection Pwind with Load and Battery (S1+S2)]
    Pwind -- No --> Case2[Case 2  
Connection Battery with Load (S1+S2)]
    SOC -- No --> SOCmax{SOC > SOC max}
    SOCmax -- Yes --> Case3[Case 3  
Connection Battery with Load and Pwind with Battery_backup (S1+S2+S3)]
    SOCmax -- No --> Pwind2{Pwind > Pload}
    Pwind2 -- Yes --> Case4[Case 4  
Connection Pwind with Load and Battery (S1+S2)]
    Pwind2 -- No --> Case5[Case 5  
Connection PLoad with Diesel Generator (S4)]
    Case1 --> Return[Return]
    Case2 --> Return
    Case3 --> Return
    Case4 --> Return
    Case5 --> Return
  
```

Flowchart of the management energy algorithm of the wind system. The process starts with 'Measure Pwind, Pload'. It then checks if 'SOC min <= SOC <= SOC max'. If 'Yes', it checks 'Pwind > Pload'. If 'Yes' to this, it leads to 'Case 1: Connection Pwind with Load and Battery (S1+S2)'. If 'No' to 'Pwind > Pload', it leads to 'Case 2: Connection Battery with Load (S1+S2)'. If 'No' to 'SOC min <= SOC <= SOC max', it checks 'SOC > SOC max'. If 'Yes' to this, it leads to 'Case 3: Connection Battery with Load and Pwind with Battery\_backup (S1+S2+S3)'. If 'No' to 'SOC > SOC max', it checks 'Pwind > Pload'. If 'Yes' to this, it leads to 'Case 4: Connection Pwind with Load and Battery (S1+S2)'. If 'No' to 'Pwind > Pload', it leads to 'Case 5: Connection PLoad with Diesel Generator (S4)'. All cases lead to a 'Return' block.

**Figure 3.** The management energy algorithm of the wind system [25].

The system accounts for five distinct operating scenarios:

### **Case 1:**

When the battery's state of charge (SOC) is within the safe range (20–80%), and the wind power output exceeds the load demand, the wind energy is sufficient to meet the load requirements and simultaneously recharge the battery.

### **Case 2:**

If the SOC remains between 20% and 80%, but the wind power is lower than the load demand, the available wind energy is inadequate. In this situation, the battery compensates for the energy shortfall to ensure the load is fully supplied.

### **Case 3:**

To prevent overcharging, once the SOC reaches the upper threshold of 80%, the system redirects the wind power to a backup battery. Meanwhile, the load remains connected to the primary battery.

### **Case 4:**

When the battery is deeply discharged (SOC falls below 20%), and the wind power exceeds the load demand, the wind source supplies sufficient energy to power the load and begin recharging the battery.

### **Case 5:**

If the SOC drops below 20%, and the wind source cannot provide enough power for the load, the available wind energy becomes insufficient. In this scenario, both the load and the battery are powered by a diesel generator.

### 5.1. Model of Battery

A dynamic battery model was implemented in MATLAB/Simulink. This generic model, detailed in [24], is based on a lead-acid battery and described by the equations provided in [25]. The model parameters were derived from the battery's discharge characteristics, with the same values assumed for the charging process.

### 5.2. Diesel Generator Model

Figure 4 illustrates the energy management architecture of the wind-based power system. This setup integrates several components: the wind energy source, battery storage, electrical loads, a backup battery, and a diesel generator. The system also includes four switches (S1, S2, S3, and S4), which regulate the connections between the energy sources and the various subsystems, such as the battery and the load. All the components are coordinated through an energy management system. The core objective of this system is to implement a control algorithm using the Stateflow tool (Matlab/Simulink, MATLAB R2010a), enabling the efficient handling of operational constraints and dynamic decision-making within the hybrid energy setup.

![Figure 4: The wind energy management model in Matlab/Simulink. The diagram shows a block diagram of a hybrid energy system. On the left, there are five input blocks: 'Pload' (green), 'Pwind' (orange), 'SOC' (pink), 'P_BACKUP' (blue), and 'P_DG' (yellow). These are connected to four switches (S1, S2, S3, S4) represented by colored icons. S1 is connected to Pwind and SOC; S2 is connected to P_BACKUP; S3 is connected to P_BACKUP; S4 is connected to P_DG. The outputs of these switches are connected to a central 'Management Of Wind System' block. This block contains internal logic for 'wind', 'Battery', 'bat_char', 'bat_dischar', 'bat_backup', and 'DG'. The outputs of the management system are connected to a 'Scope' block on the right. The management system also has internal feedback loops between the battery and charge/discharge/backup states.](daa4a6fa7e2ba1954258f86b4928eb32_img.jpg)

Figure 4: The wind energy management model in Matlab/Simulink. The diagram shows a block diagram of a hybrid energy system. On the left, there are five input blocks: 'Pload' (green), 'Pwind' (orange), 'SOC' (pink), 'P\_BACKUP' (blue), and 'P\_DG' (yellow). These are connected to four switches (S1, S2, S3, S4) represented by colored icons. S1 is connected to Pwind and SOC; S2 is connected to P\_BACKUP; S3 is connected to P\_BACKUP; S4 is connected to P\_DG. The outputs of these switches are connected to a central 'Management Of Wind System' block. This block contains internal logic for 'wind', 'Battery', 'bat\_char', 'bat\_dischar', 'bat\_backup', and 'DG'. The outputs of the management system are connected to a 'Scope' block on the right. The management system also has internal feedback loops between the battery and charge/discharge/backup states.

**Figure 4.** The wind energy management model in Matlab/Simulink [25].

The model comprises the following:

$P_{DG}$ : The power supplied by the diesel generator.

$P_{BACKUP}$ : The power supplied by the battery backup.

Stateflow variables:

System inputs

$P_{load}$ : The load power requested.

$P_{wind}$ : The power supplied by the wind.

$SOC$ : The state of charge of a battery.

System outputs

Wind: The On/Off relay of the wind.

Battery: The On/Off relay of the battery.

$bat\_char$ : The On/Off relay of the charge.

$bat\_dischar$ : The On/Off relay of the discharge.

$bat\_backup$ : The On/Off relay of the battery backup.

DG: The On/Off relay of the diesel generator.

In standalone renewable energy systems, such as wind-based installations, incorporating energy storage or integrating one or more diesel generators is often essential to ensure reliability.

A typical diesel generator system consists of two primary components: a diesel engine and a synchronous generator. The diesel engine supplies the mechanical power needed to drive the generator while maintaining a constant rotational speed ( $\omega$ ) to ensure a stable output frequency. Electrical power is produced by the synchronous generator, and the output voltage is regulated by an excitation system to remain within its nominal range.



The dynamic behavior of the diesel engine is modeled using control system transfer functions, which also include the actuator's response characteristics, as described in [26].

$$H_c = K \frac{T_3 s + 1}{T_1 T_2 s^2 + T_1 s + 1} \quad (17)$$

$$H_a = \frac{T_4 s + 1}{(1 + T_5 s) \cdot (1 + T_6 s) \cdot s} \quad (18)$$

where  $H_c$  represents the transfer function of the governor's control system, while  $H_a$  is the transfer function for the actuator.  $T_1$ ,  $T_2$ , and  $T_3$  are the time constants of the regulator.  $T_4$ ,  $T_5$ , and  $T_6$  are the time constants of the actuator, and  $K$  is the regulator gain; Figure 5 illustrates the diesel generator system, as implemented in MATLAB/Simulink. This model includes the diesel engine, the governor system, the synchronous generator, and its excitation system, which together determine the dynamic response and power output of the generator.

![Figure 5: Model of diesel generator in MATLAB/Simulink. The diagram shows a control loop for a diesel generator system. It includes a Diesel Engine Governor block, a Synchronous Machine (SM) block, and an EXCITATION block (AC1A). The governor block takes a reference speed wref (pu) and calculates the mechanical power Pmec (pu) and speed w (pu). The SM block takes Pm and Vf as inputs and outputs mechanical power Pm and terminal voltage Vt. The excitation block takes Vt and Ifd as inputs and outputs field current Ifd. The system also includes a Three-Phase Programmable Voltage Source, Current Measurement, and Voltage Measurement blocks, leading to a Scope and RMS calculations. Various signals like Wm, Vd, Vq, Id, Iq, and Ifd are also shown.](5e92d9e8e9ce204e405bff2367f88176_img.jpg)

Figure 5: Model of diesel generator in MATLAB/Simulink. The diagram shows a control loop for a diesel generator system. It includes a Diesel Engine Governor block, a Synchronous Machine (SM) block, and an EXCITATION block (AC1A). The governor block takes a reference speed wref (pu) and calculates the mechanical power Pmec (pu) and speed w (pu). The SM block takes Pm and Vf as inputs and outputs mechanical power Pm and terminal voltage Vt. The excitation block takes Vt and Ifd as inputs and outputs field current Ifd. The system also includes a Three-Phase Programmable Voltage Source, Current Measurement, and Voltage Measurement blocks, leading to a Scope and RMS calculations. Various signals like Wm, Vd, Vq, Id, Iq, and Ifd are also shown.

Figure 5. Model of diesel generator [25].

# 6. Example and Simulation

To illustrate the proposed fuzzy robust tracking control condition, a control problem of a wind generator is considered.

By defining the state vector as  $x(t) = [\theta_s \quad \Omega_r \quad \Omega_g \quad \beta]^T$  and the control signal as

$$u = [\beta_d, \Omega_z]^T,$$

the reference state vector to track can be defined as

$$x_r(t) = [\theta_{rs} \quad \Omega_{rr} \quad \Omega_{gr} \quad \beta_r]^T$$

and the fuzzy model of the WECS can be described as

$$\begin{cases} \dot{x}(t) = A(z)x(t) + Bu(t) + B_2V(t) \\ y(t) = Cx(t) \end{cases} \quad (19)$$

where

$$A(z) = \begin{bmatrix} 0 & 1 & -1 & 0 \\ -\frac{K_s}{J_r} & -\frac{B_s}{J_r} & \frac{B_s}{J_r} & \frac{T_{r\beta}(z_0)}{J_r} \\ \frac{K_s}{J_g} & \frac{B_s}{J_g} & -\frac{(B_s+B_g)}{J_g} & 0 \\ 0 & 0 & 0 & -\frac{1}{\tau} \end{bmatrix}$$

$$B = \begin{bmatrix} 0 & 0 \\ 0 & 0 \\ 0 & \frac{B_s}{J_g} \\ \frac{1}{\tau} & 0 \end{bmatrix} \quad B_2 = \begin{bmatrix} 0 \\ \frac{T_{ro}(z_0)}{J_r} \\ 0 \\ 0 \end{bmatrix}$$

$$C = \begin{bmatrix} 0 & 0 & 1 & 0 \end{bmatrix}$$

where  $\theta_s$  denotes the torsion angle,  $\Omega_r$  is the angular velocity of the rotor,  $\Omega_g$  is the angular velocity of the generator,  $K_s$  is the stiffness of the transmission,  $B_s$  is the damping of the transmission, and  $J_r$  and  $J_g$  are the inertia of the rotor and the generator, respectively.

$T_r$  is the aerodynamic torque.  $\beta$  and  $\beta_d$  are the actual and the desired pitch angles, respectively.

## T-S Fuzzy Modeling

The wind generator system is then described by the following four if-then rules:

If  $\beta$  is  $F_1^1$ , and  $V$  is  $F_2^1$ , then

$$\begin{cases} \dot{x} = A_1 x + B_1 u + B_{21} \phi \\ y = Cx \end{cases}$$

If  $\beta$  is  $F_1^1$ , and  $V$  is  $F_2^2$ , then

$$\begin{cases} \dot{x} = A_2 x + B_2 u + B_{22} \phi \\ y = Cx \end{cases}$$

If  $\beta$  is  $F_1^2$ , and  $V$  is  $F_2^1$ , then

$$\begin{cases} \dot{x} = A_3 x + B_3 u + B_{23} \phi \\ y = Cx \end{cases}$$

If  $\beta$  is  $F_1^2$ , and  $V$  is  $F_2^2$ , then

$$\begin{cases} \dot{x} = A_4 x + B_4 u + B_{24} \phi \\ y = Cx \end{cases}$$

In order to obtain the best performance from this nonlinear system (16), the following T-S fuzzy model is given:

$$\begin{cases} \dot{x}(t) = \sum_{i=1}^{4} h_i(z(t)) [(A_i + \Delta A_i(t))x(t) + (B_i + \Delta B_i(t))u(t) + B_{2i}\phi(t)] \\ y(t) = \sum_{i=1}^{4} h_i(z(t)) C_i x(t) \end{cases} \quad (20)$$

The parameter uncertainties,  $\Delta A_i(t), \Delta B_i(t)$ , represent the impossibility of an exact mathematical model of a dynamic system due to the system complexity. If the wind generator is a complex system, then the presence of uncertainties is possible.

Where

$$\begin{aligned}\phi(t) &= V(t)h_1(z) = F_1^1(\beta)F_2^1(V), \\ h_2(z) &= F_1^1(\beta)F_2^2(V) \\ h_3(z) &= F_1^2(\beta)F_2^1(V), \\ h_4(z) &= F_1^2(\beta)F_2^2(V) \quad h_1(z) = F_1^1(\beta)F_2^1(V), \\ h_2(z) &= F_1^1(\beta)F_2^2(V) \\ h_3(z) &= F_1^2(\beta)F_2^1(V), \\ h_4(z) &= F_1^2(\beta)F_2^2(V)\end{aligned}$$

$$A_1 = \begin{bmatrix} 0 & 1 & -1 & 0 \\ -\frac{K_s}{J_r} & -\frac{B_s}{J_r} & \frac{B_s}{J_r} & \frac{T_{r\beta 1}}{J_r} \\ \frac{K_s}{J_g} & \frac{B_s}{J_g} & -\frac{(B_s+B_g)}{J_g} & 0 \\ 0 & 0 & 0 & -\frac{1}{\tau} \end{bmatrix}$$

$$A_3 = \begin{bmatrix} 0 & 1 & -1 & 0 \\ -\frac{K_s}{J_r} & -\frac{B_s}{J_r} & \frac{B_s}{J_r} & \frac{T_{r\beta 2}}{J_r} \\ \frac{K_s}{J_g} & \frac{B_s}{J_g} & -\frac{(B_s+B_g)}{J_g} & 0 \\ 0 & 0 & 0 & -\frac{1}{\tau} \end{bmatrix}$$

$$A_2 = A_1, A_4 = A_3$$

$$B = \begin{bmatrix} 0 & 0 \\ 0 & 0 \\ 0 & \frac{B_s}{J_g} \\ \frac{1}{\tau} & 0 \end{bmatrix} \quad B_{21} = B_{23} = \begin{bmatrix} 0 \\ \frac{T_{rv1}}{J_r} \\ 0 \\ 0 \end{bmatrix} \quad B_{22} = B_{24} = \begin{bmatrix} 0 \\ \frac{T_{rv2}}{J_r} \\ 0 \\ 0 \end{bmatrix}$$

$$C = \begin{bmatrix} 0 & 0 & 1 & 0 \end{bmatrix}$$

$$B = B_1 = B_2 = B_3 = B_4$$

$$C = C_1 = C_2 = C_3 = C_4$$

Numerical value:

$$\begin{aligned}K_s &= 1.566 * 10^6 \text{ N/m}, \tau = 100 \text{ ms} \\ B_s &= 3029.5 \text{ Nms/rad}, B_g = 15.993 \text{ Nms/rad} \\ J_r &= 830000 \text{ Kg.m}^2, J_g = 5.9 \text{ Kg.m}^2 \\ T_{r\beta 1} &= 723980, T_{r\beta 2} = 376070 \\ T_{rv1} &= 106440, T_{rv2} = 85370\end{aligned}$$

The control objective we aimed to attain was the best tracking of the rated power while regulating the rotor speed.

We considered a network-based T-S fuzzy system for output tracking control, and we showed the effectiveness of the proposed method by performing output tracking control simulations for the T-S fuzzy system.

The simulation results of the wind system control method and energy system management are presented in this section.

In solving the LMI problem stated in Theorem 1, we obtained the results in terms of gains; it is clear that the proposed approach gives better results.

$$\begin{aligned}
 k_1 &= 1.0e + 04 * \begin{bmatrix} 0.0000 & 0.0000 & -0.0000 & -0.0000 \\ 5.8638 & 0.0112 & -0.0112 & 0.0015 \end{bmatrix} \\
 k_2 &= 1.0e + 04 * \begin{bmatrix} 0.0000 & 0.0000 & -0.0000 & -0.0000 \\ 5.8638 & 0.0112 & -0.0112 & 0.0015 \end{bmatrix} \\
 k_3 &= 1.0e + 04 * \begin{bmatrix} 0.0000 & 0.0000 & -0.0000 & -0.0000 \\ 5.8638 & 0.0112 & -0.0112 & 0.0015 \end{bmatrix} \\
 k_4 &= 1.0e + 04 * \begin{bmatrix} 0.0000 & 0.0000 & -0.0000 & -0.0000 \\ 5.8638 & 0.0112 & -0.0112 & 0.0015 \end{bmatrix}
 \end{aligned}$$

$$\begin{aligned}
 L_1 &= \begin{bmatrix} 0.0120 \\ 0.0008 \\ 0.1804 \\ 0.0000 \end{bmatrix} & L_2 &= \begin{bmatrix} 0.0120 \\ 0.0008 \\ 0.1804 \\ 0.0000 \end{bmatrix} \\
 L_3 &= \begin{bmatrix} 0.0120 \\ 0.0008 \\ 0.1804 \\ 0.0000 \end{bmatrix} & L_4 &= \begin{bmatrix} 0.0120 \\ 0.0008 \\ 0.1804 \\ 0.0000 \end{bmatrix}
 \end{aligned}$$

The simulation results of the LMI problem show that the attenuation level is 0.3442, so we can deduce that the designed T-S fuzzy controller ensures a good tracking performance and can guarantee stability.

For the simulation, we considered the wind speed input profile ( $11 \text{ m/s} < V < 29 \text{ m/s}$ ), as given in Figure 6.

![Figure 6: A line graph showing the profile of the wind input speed. The x-axis represents time from 0 to 1.8, and the y-axis represents wind speed in m/s from 10 to 30. The plot shows a highly fluctuating blue line representing the wind speed, which oscillates between approximately 12 and 28 m/s.](89dcb02be40d2949bb93de93bbf213d5_img.jpg)

Figure 6: A line graph showing the profile of the wind input speed. The x-axis represents time from 0 to 1.8, and the y-axis represents wind speed in m/s from 10 to 30. The plot shows a highly fluctuating blue line representing the wind speed, which oscillates between approximately 12 and 28 m/s.

Figure 6. The profile of the wind input speed [24].

The Figure 7 above illustrates the rotor speed tracking performance.

![Figure 7: A line graph showing rotor speed (rd/s) with H∞ observer. The x-axis represents time from 0 to 50, and the y-axis represents rotor speed in rd/s from -100 to 300. The plot shows four curves: 'y' (blue solid line), 'yest' (dashed line), 'yr' (red solid line), and 'x3-optimal' (green solid line). The 'y' and 'yest' curves are very close to each other, oscillating around the 'yr' curve, which is a reference signal. The 'x3-optimal' curve is a constant horizontal line at approximately 150 rd/s.](70f5f44cb855bbb0c203c00187b2113e_img.jpg)

Figure 7: A line graph showing rotor speed (rd/s) with H∞ observer. The x-axis represents time from 0 to 50, and the y-axis represents rotor speed in rd/s from -100 to 300. The plot shows four curves: 'y' (blue solid line), 'yest' (dashed line), 'yr' (red solid line), and 'x3-optimal' (green solid line). The 'y' and 'yest' curves are very close to each other, oscillating around the 'yr' curve, which is a reference signal. The 'x3-optimal' curve is a constant horizontal line at approximately 150 rd/s.

Figure 7. Rotor speed (rd/s) with  $H_\infty$  observer, based on [24].

The Figure 7 above illustrates the rotor speed tracking performance. It is evident that the actual speed closely follows the reference trajectory, even under varying wind speed conditions. This indicates that the implemented Takagi–Sugeno (T-S) fuzzy controller provides effective and accurate tracking. The next Figure 8 displays the corresponding membership functions used in the controller design.

![Figure 8: Membership function plot showing five curves: h1 (dashed blue), h2 (solid blue), h3 (solid red), h4 (solid red), and h-activation (solid red). The x-axis ranges from 0 to 100, and the y-axis ranges from 0 to 1. h1 is a low curve near the bottom. h2 is a high curve near the top. h3 and h4 are bell-shaped curves that overlap, with h3 peaking around x=25 and h4 peaking around x=45. h-activation is a solid red line that follows the peaks of h3 and h4.](0a8d173734e4e46c344178e8d21bcbc3_img.jpg)

Figure 8: Membership function plot showing five curves: h1 (dashed blue), h2 (solid blue), h3 (solid red), h4 (solid red), and h-activation (solid red). The x-axis ranges from 0 to 100, and the y-axis ranges from 0 to 1. h1 is a low curve near the bottom. h2 is a high curve near the top. h3 and h4 are bell-shaped curves that overlap, with h3 peaking around x=25 and h4 peaking around x=45. h-activation is a solid red line that follows the peaks of h3 and h4.

Figure 8. Membership function [24].

# 7. Conclusions

In this study, a sufficient condition for the robust stabilization of uncertain, nonlinear wind turbine systems subject to external disturbances and input delays was proposed. Building upon previous research, the proposed framework integrates advanced control strategies using Takagi–Sugeno (T-S) fuzzy modeling to effectively handle system uncertainties and delay effects. A robust fuzzy observer-based tracking controller was designed to minimize tracking errors and mitigate the impact of disturbances. The control design was formulated using a quasi-Linear Matrix Inequality (LMI) approach, enabling its practical implementation and scalability. Additionally, a delayed-state feedback control law based on Parallel Distributed Compensation (PDC) was developed, supported by an observer, to ensure the system’s stability. The stability conditions were rigorously established using a quadratic Lyapunov function and expressed as LMIs, allowing for computational efficiency in the controller’s synthesis. The simulation results demonstrate that the proposed method successfully stabilizes the wind energy system, enhancing its robustness, delay tolerance, and control accuracy in the presence of external disturbances. Overall, this study contributes to a unified and effective control strategy for the reliable operation of wind turbine systems under real-world uncertainties.

**Author Contributions:** Methodology, K.L.; Software, K.L. and S.J.; Validation, K.L.; Formal analysis, K.L. and O.L.; Data curation, O.L.; Writing—original draft, K.L.; Writing—review and editing, K.L. and S.J.; Supervision, S.J. and I.B. All authors have read and agreed to the published version of the manuscript.

**Funding:** This research received no external funding.

**Data Availability Statement:** Data are contained within the article.

**Conflicts of Interest:** The authors declare no conflict of interest.

# References

1. Sumbekov, S.; Phuc, B.D.H.; Do, T.D. Takagi–Sugeno fuzzy-based sliding mode control for wind energy conversion systems with disturbance observer. *Electr. Eng.* **2020**, *102*, 1141–1151. [\[CrossRef\]](#)
2. Tidjani, N.; Guessoum, A. Augmented robust T-S fuzzy control based PMSG wind turbine improved with  $H_\infty$  performance. *Int. J. Power Electron. Drive Syst. (IJPEDS)* **2021**, *12*, 585–596. [\[CrossRef\]](#)
3. Wang, L.; Liu, Y. Robustification of the  $H_\infty$  controller combined with fuzzy logic and PI&PID-Fd for hybrid control of Wind Energy Conversion System connected to the power grid based on DFIG. *Energy Rep.* **2021**, *7*, 7539–7550. [\[CrossRef\]](#)

4. Brunner, J.; Fortmann, J.; Schulte, H. Model Reference Control for Wind Turbine Systems in Full Load Region based on Takagi-Sugeno Fuzzy Systems. *arXiv* **2024**, arXiv:2405.06829. [\[CrossRef\]](#)
5. Jeon, T.; Song, Y.; Paek, I. A Study on  $H_\infty$ -Fuzzy Controller for a Non-Linear Wind Turbine with Uncertainty. *Appl. Sci.* **2023**, *13*, 11930. [\[CrossRef\]](#)
6. Takagi, T.; Sugeno, M. Fuzzy identification of systems and its application to modelling and control. *IEEE Trans. Syst. Man Cybern.* **1985**, *15*, 116–132. [\[CrossRef\]](#)
7. Tong, S.; Wang, T.; Li, H.X. Fuzzy robust tracking control for uncertain nonlinear systems. *Int. J. Syst. Sci.* **2002**, *33*, 521–530. [\[CrossRef\]](#)
8. Lee, K.R.; Jeung, E.T.; Park, H.B. Robust fuzzy  $H_\infty$  control for uncertain nonlinear systems via state feedback: An LMI approach. *Fuzzy Sets Syst.* **2001**, *120*, 123–133.
9. Mansouri, B.; Manamanni, N.; Hamzaoui, A.; Zaytoon, J. Tracking control for uncertain Takagi-Sugeno fuzzy systems with external disturbances. *J. Intell. Fuzzy Syst.* **2005**, *16*, 23–34. [\[CrossRef\]](#)
10. Bououden, S.; Chadli, M.; Filali, S.; El Hajjaji, A. Fuzzy model-based multivariable predictive control of a variable speed wind turbine: LMI approach. *Energy Convers. Manag.* **2012**, *56*, 118–130. [\[CrossRef\]](#)
11. Tanaka, K.; Wang, K.O. *Fuzzy Control Systems Design and Analysis: A Linear Matrix Inequality Approach*; John Wiley & Sons, Inc.: Hoboken, NJ, USA, 2001.
12. Boyd, S.; El Ghaoui, L.; Feron, E.; Balakrishnan, V. *Linear Matrix Inequalities in System and Control Theory*, SIAM Studies in Applied Mathematics; Society for Industrial and Applied Mathematics (SIAM): Philadelphia, PA, USA, 1994; Volume 15.
13. Mansouri, B.; Manamanni, N.; Gueltou, K.; Kruszewski, A.; Guerra, T.M. Output feedback LMI tracking control conditions with  $H_\infty$  criterion for uncertain and disturbed T-S models. *Fuzzy Sets Syst.* **2008**, *159*, 3307–3326. [\[CrossRef\]](#)
14. Harrabi, N.; Kharrat, M.; Souissi, M.; Aitouche, A. Maximum Power Point Tracking of a Wind Generation System Based on T-S Fuzzy Model. *Renew. Energy* **2015**, *83*, 511–522.
15. Tseng, C.; Chen, B.; Uang, H. Fuzzy Tracking Control Design for Nonlinear Dynamic Systems via T-S Fuzzy Model. *IEEE Trans. Fuzzy Syst.* **2001**, *9*, 23–33.
16. Zhang, D.; Han, Q.; Jia, X. Tracking Control for Network-Based T-S Fuzzy Systems With Asynchronous Constraints. *IEEE Trans. Fuzzy Syst.* **2012**, *20*, 420–432.
17. Bezzaoucha, S.; Marx, B.; Maquin, D.; Ragot, J. Model Reference Tracking Control for Nonlinear Systems Described by Takagi-Sugeno Structure. *Int. J. Syst. Sci.* **2013**, *44*, 1937–1950.
18. Abdelkrim, A.; Ghorbel, C.; Benrejeb, M. LMI-Based Tracking Control for Takagi-Sugeno Fuzzy Model. *J. Autom. Control Eng.* **2010**, *2*, 126–132.
19. Khaber, F.; Hamzaoui, A.; Zehar, K. State Feedback Controller Design via Takagi-Sugeno Fuzzy Model: A Linear Matrix Inequalities Approach. *Int. J. Fuzzy Syst.* **2014**, *16*, 239–250.
20. Zhang, J.; Fei, M.; Yang, T.; Tan, Y. Robust Fuzzy Tracking Control of Nonlinear Systems with Uncertainty via T-S Fuzzy Model. *Fuzzy Sets Syst.* **2006**, *157*, 310–325.
21. Yue, D.; Han, Q.L.; Lam, J. Network-Based Robust  $H_\infty$  Control of Systems with Uncertainty. *Automatica* **2005**, *41*, 999–1007. [\[CrossRef\]](#)
22. Pierreval, H.; Huntsinger, R. An Investigation on Neural Network Capabilities as Simulation Metamodels. In Proceedings of the 1992 Summer Computer Simulation Conference, Reno, NV, USA, 27–30 July 1992; pp. 413–417.
23. Bouharchouche, A.; Berkouk, E.M.; Ghennam, T. Control and energy management of a grid connected hybrid energy system PV-wind with battery energy storage for residential applications. In Proceedings of the 2013 Eighth International Conference and Exhibition on Ecological Vehicles and Renewable Energies (EVER), Monte Carlo, Monaco, 27–30 March 2013; pp. 1–11.
24. Lahmadi, K.; Lahmadi, O.; Boumhidi, I. Fuzzy  $H_\infty$  Robust Control and Neural Network-Based Delayed-Input Strategies for Uncertain Wind Energy Systems Using LMI Approach. In Proceedings of the 5th Winter IFSA Conference on Automation, Robotics & Communications for Industry 4.0/5.0 (ARCI' 2025), Granada, Spain, 19–21 February 2025; pp. 27–29. Available online: [https://arci-conference.com/arci\\_2025\\_proceedings.html](https://arci-conference.com/arci_2025_proceedings.html) (accessed on 5 April 2025). [\[CrossRef\]](#)
25. Lahmadi, K.; Boumhidi, I. Optimizing Control and Energy Management in a TS Fuzzy Wind System using LMI Approach. *J. Electr. Syst.* **2024**, *20*, 1322–1329.
26. Lahmadi, K.; Boumhidi, I. Robust Control of Delayed-Input T-S Models Based on Neural Networks: Application to Wind Energy Systems. In Proceedings of the Third International Conference on Intelligent Computing in Data Sciences (ICDS), Marrakech, Morocco, 28–30 October 2019. [\[CrossRef\]](#)

**Disclaimer/Publisher's Note:** The statements, opinions and data contained in all publications are solely those of the individual author(s) and contributor(s) and not of MDPI and/or the editor(s). MDPI and/or the editor(s) disclaim responsibility for any injury to people or property resulting from any ideas, methods, instructions or products referred to in the content.