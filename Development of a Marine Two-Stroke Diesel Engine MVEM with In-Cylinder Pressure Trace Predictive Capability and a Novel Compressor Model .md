

# Article

# Development of a Marine Two-Stroke Diesel Engine MVEM with In-Cylinder Pressure Trace Predictive Capability and a Novel Compressor Model

Haosheng Shen <sup>1</sup>, Jundong Zhang <sup>1,\*</sup>, Baicheng Yang <sup>2</sup> and Baozhu Jia <sup>3</sup>

<sup>1</sup> College of Marine Engineering, Dalian Maritime University, Dalian 116026, China; shen7231591@126.com

<sup>2</sup> College of Navigation, Dalian Maritime University, Dalian 116026, China; yangbaicheng@dlmu.edu.cn

<sup>3</sup> Marine College, Guangdong Ocean University, Zhanjiang 524088, China; skysky@dlmu.edu.cn

\* Correspondence: zhjundong@dlmu.edu.cn; Tel.: +86-134-7894-8607

Received: 15 February 2020; Accepted: 13 March 2020; Published: 16 March 2020

![Check for updates icon](1d7527f4316cfe2d342b08d1653d1592_img.jpg)

Check for updates icon

**Abstract:** In this article, to meet the requirements of marine engine room simulator on both the simulation speed and simulation accuracy, a mean value engine model (MVEM) for the 7S80ME-C9.2 marine two-stroke diesel engine was developed and validated in the MATLAB/Simulink environment. In consideration of the significant influence of turbocharger compressor on both the engine steady state performance and transient response, a novel compressor model (mass flow rate and isentropic efficiency model) based on a previous study carried out by the first author was proposed with the aim of achieving satisfactory simulation accuracy within the whole engine operating envelope. The predictive and extrapolative capability of the proposed compressor model was validated by carrying out simulation experiments and analyzing the simulation results under steady state condition and during transient process. To make the traditional MVEM capable of predicting in-cylinder pressure trace, the cylinder pressure analytic model proposed by Eriksson and Andersson for the four-stroke SI (spark ignition) engine was adapted to the 7S80ME-C9.2 marine two-stroke diesel engine based on the characteristic of in-cylinder pressure trace of this type of engine and then coupled to the MVEM developed in this paper. Since there is no need to solve any differential equation as it is done in the 0-D model, the advantage of MVEM in running speed is not impaired. For achieving satisfactory simulation accuracy by using the analytic model, the model parameters were calibrated elaborately by using engine measured data and a 0-D model and the relevant tuning procedure was discussed in detail.

**Keywords:** marine two-stroke diesel engine; mean value engine model; compressor model; in-cylinder pressure trace; model calibration

## 1. Introduction

The marine large scale two-stroke diesel engine is widely adopted as the prime mover for the large merchant ships mainly because of its high thermal efficiency, reliability as well as the ability of burning low grade fuel, i.e., heavy fuel oil (HFO). For complying with the stringent international environmental legislations and obtaining improved fuel efficiency, engine manufacturers have developed new versions of marine engines, mainly including marine electronically controlled diesel engines and marine dual-fuel engines [1–3].

In consideration of the large size and weight of marine large scale two-stroke diesel engines as well as the substantial manpower and financial power required for carrying out experimental studies, various engine simulation techniques have been widely adopted for investigating engine performance, designing and testing the fault diagnosis algorithm, as well as developing the engine control system.

Among these simulation models, 0-D models and mean value engine model (MVEM) are widely adopted by researchers mainly because of their fast running speed and satisfactory simulation accuracy. The difference between the 0-D model and MVEM lies in the modeling approach for the cylinder. For the 0-D model, the cylinder is assumed as an open thermodynamic system, where the working medium is uniformly distributed in it. By applying mass and energy conservation laws and incorporating several relevant sub-models, the in-cylinder pressure trace can be predicted. Furthermore, the 0-D model is also capable of predicting engine performance at varying settings (e.g., varying the start of injection timing, exhaust valve opening/closing timing, turbine area, etc.), which is a special advantage in comparison to the MVEM [1]. In the book published by Eriksson and Nielsen, the MVEM is defined as “Mean value engine models are models where the signals, parameters, and variables that are considered are averaged over one or several cycles” [4]. In this respect, the mass and energy flow through the cylinder is assumed continuous for the MVEM, and the engine average performance over one or several cycles can be obtained. Consequently, the MVEM is able to run much faster than the 0-D model, which is therefore very suitable for cases that require fast running speed, such as the simulation of engine transients for a long period. On the other hand, despite similar predictive accuracy can be achieved by the two models, the in-cylinder pressure trace cannot be predicted by the MVEM, which is its major limitation [1,5].

In the literature, researchers tried to improve the predictive ability of the MVEM and the running speed of the 0-D model by adopting a “hybrid” modeling approach, meaning that different modeling approaches can be adopted for different engine components or different phases of the engine cycle. This approach can effectively overcome the limitation caused by using only a single modeling approach. In the study carried out by Altosole et al., for meeting the requirement of real-time ship maneuvering simulation, the cylinder simulation was entirely based on a set of five-dimensional numerical matrices, each of which was generated by a 0-D model [6]. It was revealed from the simulation results that this modeling approach can achieve similar transient response but reduce the simulation time of about 99%; however, the in-cylinder pressure trace cannot be predicted. Nikzadfar and Shamekhi developed an extended MVEM for control-oriented modeling of diesel engines transient performance and emissions by replacing the cylinder model with two artificial neural networks (ANN). One is for predicting aspirated air mass flow, torque and exhaust gas temperature and the other for predicting soot and  $\text{NO}_x$  emission [7]. Despite the fact that satisfactory predictive accuracy and running speed can be achieved with this extended MVEM, it still cannot predict the in-cylinder pressure trace. Based on the modular MVEM developed by Theotokatos [8], Baldi et al. proposed a combined mean value-zero dimensional model for a large marine four-stroke diesel engine, where the closed part of the cycle was represented by the 0-D model and the open part by the MVEM. The combined model fully takes the respective advantage of the 0-D model (ability to predict in-cylinder pressure trace) and MVEM (fast running speed) [9]. Nevertheless, it was pointed out by Theotokatos et al. that the 0-D model still needed to be called at each calculation step for the combined mean value-zero dimensional model, which made its running speed still scant for cases where engine transient simulation for a long period was required [1]. In the study carried out by Tang et al., the hybrid modeling approach was further improved by simplifying the in-cylinder pressure calculation during the scavenging and exhausting phases with two linear functions and abandoning engine cycles at certain intervals [5]. It was revealed that the modified model was able to predict the in-cylinder pressure trace and run as fast as the MVEM at steady state condition; however, during the transient process, the improvement in running speed is at the expense of predictive precision.

For practical applications that have high requirement on both predictive accuracy and running speed, the MVEM seems to be the best choice. However, due to the absence of a detailed mathematical description of in-cylinder working process, the in-cylinder pressure trace cannot be predicted with MVEM, which limits its practical value to some extent. This is the reason why 0-D model was incorporated into the MVEM in several studies [5,9]. However, it should be noted that even limited 0-D modeling will increase the model complexity and thus affect the running speed of the MVEM

obviously. To solve this problem, the cylinder pressure analytic model proposed by Eriksson and Andersson for the four-stroke SI (spark ignition) engine was modified and adapted to the 7S80ME-C9.2 marine two-stroke diesel engine in this paper [10]. By coupling the cylinder pressure analytic model to the MVEM, the MVEM is able to estimate the in-cylinder pressure trace. Furthermore, as the running speed of the cylinder pressure analytic model is much faster than the 0-D model, the merit of the MVEM in running speed is not affected significantly.

In consideration of the significant influence of compressor model on the simulation accuracy of the whole engine model, a novel compressor mass flow rate and isentropic efficiency model was proposed in this paper based on the research results of a previous paper published by the first author, which compared and analyzed the predictive and extrapolative ability of several classical and recent proposed compressor mass flow rate and isentropic efficiency empirical models. The incorporation of the novel compressor model will be very helpful for the MVEM to achieve satisfactory predictive accuracy in the whole engine operating envelope under both steady and transient conditions.

The MVEM developed in this paper is very suitable for applications that require both fast running speed and in-cylinder pressure trace predictive capability, for example, this MVEM has been attempted to be used in a VLCC (Very Large Crude Carrier) marine engine room simulator [11].

## 2. Model Description

### 2.1. Engine Specification and MVEM Structure

The marine large scale two-stroke electronically controlled diesel engine MAN B&W 7S80ME-C9.2 is selected as the simulation object in the paper. This type of engine is widely adopted as the prime mover of merchant ships, especially the VLCC. The engine main technical parameters at the MCR (Maximum Continuous Rating) point are presented in Table 1. The MVEM is implemented in MATLAB/Simulink environment following a block oriented modeling approach, as it is depicted in Figure 1. Benefitting from the sub-system creation function of MATLAB/Simulink, the structure of the MVEM is very similar with that of the real engine, each component of which is represented by an individual block. The modeling approaches of these engine components will be introduced in the following sub-sections.

![Figure 1: Mean value engine model (MVEM) structure. The diagram shows a block-oriented model of a marine diesel engine. It starts with ambient conditions (T_amb, P_amb) on the left. Air enters through a 'Wastegate' block at the top, then through a 'Turbine' block. The exhaust from the turbine goes to an 'Exhaust Manifold' block, which contains variables T, P, and x. From the exhaust manifold, the flow goes to a 'Cylinder' block (represented by a row of cylinders) and then to a 'Propeller' block, which outputs crankshaft speed N_e. The crankshaft speed N_e is also shown at the bottom right. The cylinder block has inputs from a 'Scavenging Manifold' (containing P_s and T) and a 'Blower' block. The cylinder block also receives a target speed N_e,set. The exhaust from the cylinder goes back to the exhaust manifold. The intake side of the cylinder block is connected to a 'Compressor' block, which is driven by the crankshaft. The compressor output goes through an 'Air Cooler' block and then to the cylinder block. There are also two 'Blower' blocks and another 'Air Cooler' block in the intake path. The entire model is represented by interconnected dashed-line blocks.](b612b838f94982799a69461ffb078a73_img.jpg)

Figure 1: Mean value engine model (MVEM) structure. The diagram shows a block-oriented model of a marine diesel engine. It starts with ambient conditions (T\_amb, P\_amb) on the left. Air enters through a 'Wastegate' block at the top, then through a 'Turbine' block. The exhaust from the turbine goes to an 'Exhaust Manifold' block, which contains variables T, P, and x. From the exhaust manifold, the flow goes to a 'Cylinder' block (represented by a row of cylinders) and then to a 'Propeller' block, which outputs crankshaft speed N\_e. The crankshaft speed N\_e is also shown at the bottom right. The cylinder block has inputs from a 'Scavenging Manifold' (containing P\_s and T) and a 'Blower' block. The cylinder block also receives a target speed N\_e,set. The exhaust from the cylinder goes back to the exhaust manifold. The intake side of the cylinder block is connected to a 'Compressor' block, which is driven by the crankshaft. The compressor output goes through an 'Air Cooler' block and then to the cylinder block. There are also two 'Blower' blocks and another 'Air Cooler' block in the intake path. The entire model is represented by interconnected dashed-line blocks.

Figure 1. Mean value engine model (MVEM) structure.

**Table 1.** Main Technical parameters of 7S80ME-C9.2 engine at MCR (Maximum Continuous Rating).

| Parameters                             | Value         |
|----------------------------------------|---------------|
| Number of cylinder (–)                 | 7             |
| Cylinder bore (mm)                     | 800           |
| Stroke (mm)                            | 3450          |
| Speed (rpm)                            | 72            |
| Power (kW)                             | 25190         |
| Maximum pressure (MPa)                 | 17.1          |
| Mean brake effective pressure (bar)    | 17.3          |
| Firing order                           | 1-7-2-5-4-3-6 |
| Specific fuel oil consumption (g/kW·h) | 165.9         |

### 2.2. Cylinder

For the MVEM, the actual intermittent gas flowing process through the scavenging ports and exhaust valve is simplified as a flowing process through an equivalent orifice with fixed area under sub-sonic flow consideration. Consequently, the cylinder inflowing air mass flow rate  $\dot{m}_{sz}$  can be calculated with the following equation [5,8,9,12,13]:

$$\dot{m}_{sz} = C_z A_z \frac{p_s}{\sqrt{R_s T_s}} \sqrt{\frac{2k_s}{k_s - 1} \left[ \left( \frac{p_e}{p_s} \right)^{\frac{2}{\gamma_s}} - \left( \frac{p_e}{p_s} \right)^{\frac{\gamma_s + 1}{\gamma_s}} \right]} \quad (1)$$

where  $C_z$  and  $A_z$  are the flow coefficient and the equivalent orifice area, respectively;  $R_s$ ,  $T_s$ ,  $p_s$  and  $\gamma_s$  are the gas constant, temperature, pressure and specific heat ratio of the air in the scavenging manifold, respectively;  $p_e$  is the exhaust manifold pressure.

As the exhaust valve lifting curve is not provided by the engine manufacturer and the orifice flow coefficient is also unknown, therefore, the product of  $C_z$  and  $A_z$  ( $C_z A_z$ ), is treated as a calibration parameter in this paper.  $C_z A_z$  can be approximated as a linear function of the brake power, that is  $C_z A_z = k_{CA0} + k_{CA1} P_b$ .

As similar with the engine air inflowing process, the MVEM also treats the fuel injection as a continuous process. According to the mass conservation law, the mass flow rate of exhaust gas exiting the cylinders  $\dot{m}_{ze}$  can be calculated by adding  $\dot{m}_{sz}$  and the fuel injection rate  $\dot{m}_f$ .

The energy released by the fuel burning cannot be fully exploited by the engine and converted to the mechanical energy directly, therefore, a portion of the thermal energy still remains in the exhaust gas. Consequently, based on the energy conservation law, the thermal energy of the exhaust gas exiting the cylinders can be written as [8,12,13]:

$$\dot{m}_{ze} h_{ze} = \dot{m}_{sz} c_{p,s} T_s + \zeta \eta_{comb} \dot{m}_f H_{LHV} \quad (2)$$

where  $h_{ze}$  is the specific enthalpy of exhaust gas;  $\eta_{comb}$  is the combustion efficiency, which is a function of the air-fuel ratio ( $A/F = \dot{m}_{sz}/\dot{m}_f$ );  $c_{p,s}$  is the constant pressure specific heat of the scavenging air;  $H_{LHV}$  is the fuel lower heating value;  $\zeta$  is the fuel chemical energy proportion in the exhaust gas, which can be fitted as a linear function of the brake power, that is  $\zeta = k_{\zeta 0} + k_{\zeta 1} P_b$ .

The mean indicated effective pressure  $\bar{p}_i$  is fitted as a linear function of the fuel index. According to the engine shop trial report, the mean friction effective pressure  $\bar{p}_f$  is always 1 bar for all the tested loading conditions, therefore, a constant value of  $\bar{p}_f$  is assumed in this paper. Having obtained  $\bar{p}_i$  and  $\bar{p}_f$ , the mean brake effective pressure  $\bar{p}_b$  can be calculated as  $\bar{p}_b = \bar{p}_i - \bar{p}_f$ .

Finally, the engine brake torque  $Q_b$ , brake power  $P_b$  and brake specific fuel consumption (BSFC) can be derived as per the following equations:

$$Q_b = \frac{n_z V_d \bar{p}_b}{2\pi}, P_b = \frac{\pi N_e Q_b}{30}, \text{BSFC} = \frac{\dot{m}_f}{P_b} \quad (3)$$

where  $V_d$  is the engine displacement volume of a single cylinder.

### 2.3. Turbocharger

The power absorbed by the compressor can be written as:

$$P_c = \dot{m}_c c_{p,a} (T_{c,out} - T_{c,in}) \quad (4)$$

where  $\dot{m}_c$  is the compressor mass flow rate;  $c_{p,a}$  is the air constant pressure specific heat;  $T_{c,in}$  and  $T_{c,out}$  are the temperature of air entering and exiting the compressor, respectively.

The compressor mass flow rate depends on not only the turbocharger rotational speed but also the pressure ratio across it with the latter can be written as:

$$\Pi_c = \frac{p_s + \Delta p_{ac} - \Delta p_{bl}}{p_{amb} - \Delta p_{af}} \quad (5)$$

where  $p_s$ ,  $\Delta p_{ac}$ ,  $\Delta p_{bl}$ ,  $p_{amb}$  and  $\Delta p_{af}$  are the scavenging manifold pressure, air cooler pressure drop, auxiliary blower pressure increase, ambient pressure and compressor air filter pressure drop, respectively. In this paper,  $\Delta p_{af}$  is fitted as a second-order polynomial of  $\dot{m}_c$ . Modeling approaches for  $\Delta p_{ac}$  and  $\Delta p_{bl}$  will be introduced in Section 2.5.

The temperature of air exiting the compressor can be calculated by the following equation, which is derived based on the definition of compressor isentropic efficiency:

$$T_{c,out} = T_{c,in} (1 + (\Pi_c^{(\gamma_a-1)/\gamma_a} - 1) / \eta_c) \quad (6)$$

where  $\gamma_a$  is the air specific heat ratio;  $\eta_c$  is the isentropic efficiency.

The power generated by the turbine can be written as:

$$P_t = \dot{m}_t c_{p,e} (T_{t,in} - T_{t,out}) \quad (7)$$

where  $\dot{m}_t$  is the turbine mass flow rate;  $c_{p,e}$  is the exhaust gas constant pressure specific heat;  $T_{t,in}$  and  $T_{t,out}$  are the temperature of exhaust gas entering and exiting the turbine.

In this paper, the turbine is simplified as a nozzle and the exhaust gas mass flow rate flowing through it can be calculated based on the assumption of one-dimensional isentropic adiabatic flow with the input data including the gas thermodynamic properties in the exhaust manifold, the pressure ratio across the turbine as well as the turbine equivalent flow area and flow coefficient.

The pressure ratio  $\Pi_t$  is calculated by the following equation:

$$\Pi_t = \frac{p_{amb} + p_{t,back}}{p_e} \quad (8)$$

where  $p_{t,back}$  is the turbine back-pressure and it is fitted as an exponential function of the turbine mass flow rate in this paper.

The turbine equivalent flow area  $A_t$  can be computed as per the following equation:

$$A_t = \sqrt{\frac{(A_D \cdot A_S)^2}{A_D^2 + A_S^2}} \quad (9)$$

where  $A_D$  and  $A_S$  are the flow area of the turbine impeller and nozzle ring, respectively.

For the turbocharger turbine investigated in this paper, its flow coefficient  $C_t$  and isentropic efficiency  $\eta_t$  only depend on the expansion ratio  $\Gamma_t$  ( $\Gamma_t = 1/\Pi_t$ ) and are not influenced by the turbocharger rotational speed. Therefore,  $C_t$  and  $\eta_t$  are modeled by using look-up table in this paper based on the turbine performance map.

The temperature of exhaust gas exiting the turbine can be calculated based on the definition of turbine isentropic efficiency as the following equation:

$$T_{t,out} = T_{t,in}(1 - \eta_t(1 - \Pi_t^{(\gamma_e-1)/\gamma_e})) \quad (10)$$

where  $\gamma_e$  is the specific heat ratio of exhaust gas.

Finally, the turbocharger shaft angular speed  $\omega_{tc}$  can be calculated by integrating the following equation, which is derived based on the angular momentum conservation law:

$$\frac{d\omega_{tc}}{dt} = \frac{1}{J_{tc}} \left( \frac{P_t}{\omega_{tc}} \eta_{tc,m} - \frac{P_c}{\omega_{tc}} \right) \quad (11)$$

where  $J_{tc}$  is the moment of inertia of the turbocharger rotating part;  $\eta_{tc,m}$  is the turbocharger mechanical efficiency.

### 2.4. Scavenging and Exhaust Manifolds

The scavenging and exhaust manifolds are treated as control volumes in the MVEM. By applying the mass conservation law, the mass changing rate in the manifold can be computed as:

$$\frac{dm}{dt} = \dot{m}_{in} - \dot{m}_{out} \quad (12)$$

where  $\dot{m}_{in}$  and  $\dot{m}_{out}$  are the mass flow rate entering and exiting the manifold, respectively.

The temperature changing rate in the manifold can be derived by applying the energy conservation law. The differential equation governing the temperature changing rate in the manifold can be written as:

$$\frac{dT}{dt} = \frac{\dot{m}_{in}c_v(T_{in} - T) + R(T_{in}\dot{m}_{in} - T\dot{m}_{out}) + \dot{Q}_{ht}}{mc_v} \quad (13)$$

where  $T_{in}$  is the gas temperature entering the manifold;  $\dot{Q}_{ht}$  is the heat dissipation;  $c_v$  is the gas constant volume specific heat.

Due to the negligible temperature difference between the scavenging air and the surrounding, the heat dissipation in the scavenging manifold is neglected, whereas the heat dissipation in the exhaust manifold must be taken into account because the exhaust gas temperature is much higher than the surrounding.  $\dot{Q}_{ht}$  is computed as it was done in Theotokatos and Tzelepis by using the overall heat transfer coefficient and heat transfer area [12].

Having obtained the stored mass and gas temperature by integrating Equations (12) and (13), the gas pressure in the manifold can be derived by using the ideal gas state equation.

### 2.5. Air cooler, Auxiliary Blower and Wastegate

The air temperature exiting the air cooler  $T_{ac,out}$  can be written as:

$$T_{ac,out} = T_{ac,in} - \eta_{ac}(T_{ac,in} - T_{cw}) \quad (14)$$

where  $T_{ac,in}$  is the air temperature entering the air cooler;  $\eta_{ac}$  is the cooling efficiency;  $T_{cw}$  is the cooling water temperature, which is assumed to be constant and equals to 300 K in this paper.

In this paper, the air cooler cooling efficiency and the pressure drop is fitted as a second-order polynomial of the air mass flow rate flowing through it.

Auxiliary blower of the centrifugal type, which is driven by an induction motor running at fixed rotational speed, is commonly adopted for marine large scale two-stroke diesel engines. Consequently, the auxiliary blower can be modeled as a centrifugal compressor that runs at fixed rotational speed. Following this idea, the pressure increase across the blower  $\Delta p_{bl}$  and blower efficiency  $\eta_{bl}$  thus only

depend on the air volume flow rate  $\dot{V}_{bl}$ . Therefore,  $\Delta p_{bl}$  and  $\eta_{bl}$  are fitted as a second and third order polynomial of  $\dot{V}_{bl}$ , respectively, based on the auxiliary blower performance map in this paper. Having obtained  $\Delta p_{bl}$  and  $\eta_{bl}$ , the air temperature exiting the blower can be computed by using Equation (6), which is originally used to calculate the air temperature existing the compressor.

To prevent the compressor from entering into the unstable surging area, many marine large scale two-stroke diesel engines are equipped with a wastegate in recent years, which is a bypass configuration in parallel with the turbine. In this paper, the wastegate is simplified as an ideal nozzle and the gas mass flow rate is calculated based on the assumption of one-dimensional isentropic adiabatic flow. It should be noted that the wastegate shares the same upstream and downstream condition with the turbine.

### 2.6. Engine Speed Governor

In this paper, the governor is modeled as a proportional-integral (PI) controller with the actual engine rotational speed as the feedback signal [1,5,8,9,12,13]. In addition, scavenging air and torque limiters are also incorporated in the governor model for protecting the engine integrity during fast transients.

As similar with the turbocharger shaft, the engine crankshaft rotational speed  $N_e$  can be calculated by integrating the following equation:

$$\frac{dN_e}{dt} = \frac{60}{2\pi} \cdot \frac{Q_b - Q_p}{J_e + J_{sh} + J_p} \quad (15)$$

where  $Q_p$  is the propeller resisting torque;  $J_e$ ,  $J_{sh}$  and  $J_p$  are the moment of inertia of the engine, shaft system and propeller, respectively.

As the main focus of this paper is to investigate the engine steady-state performance and transient response by using MVEM, the extra propeller moment of inertia caused by the entrained water is neglected; in addition, the hydrodynamic characteristic of the propeller and ship hull is also neglected. For simplicity, the propeller resisting torque is calculated by using the propeller propulsive characteristic curve that passes through the engine MCR point [13]:

$$Q_p = K_p N_e^2, \quad K_p = Q_{b,MCR} / N_{e,MCR}^2 \quad (16)$$

### 2.7. Compressor Model Improvement

#### 2.7.1. Compressor Performance Map

The working characteristic of a compressor is usually represented by the performance map as shown in Figure 2 with the mass (or volume) flow rate and pressure ratio as the horizontal and vertical coordinate, respectively.

As shown in Figure 2, most of the compressor performance maps provided by the manufacturers only contain several discrete iso-speed and iso-efficiency curves in the design operating zone. However, for marine turbocharger compressor, its actual rotational speed may be lower than the lowest rotational speed presented in the performance map, or higher than the highest one; in addition, its pressure ratio may approach to unity under certain operating conditions, such as slow steaming, activation of the auxiliary blower and ship maneuvering [14]. Therefore, it is necessary for the developed compressor model to be capable of extrapolating to these off-design operating zones accurately and robustly. In addition, the developed compressor model is also required to accurately interpolate within the unknown areas between these discrete curves.

![Figure 2: Compressor performance map. The graph plots Pressure Ratio on the vertical axis against Mass (or Volume) Flow Rate on the horizontal axis. It features several curves: a dashed 'Surging Line' at the top left, a dashed 'Choking Line' at the bottom right, and solid 'Iso-speed Lines' (blue) and 'Iso-efficiency Lines' (red) that form closed loops. The 'Design Operating Zone' is the central area bounded by these loops. The 'Surging Zone' is the area to the left of the surging line, and the 'Choking Zone' is the area to the right of the choking line.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 2: Compressor performance map. The graph plots Pressure Ratio on the vertical axis against Mass (or Volume) Flow Rate on the horizontal axis. It features several curves: a dashed 'Surging Line' at the top left, a dashed 'Choking Line' at the bottom right, and solid 'Iso-speed Lines' (blue) and 'Iso-efficiency Lines' (red) that form closed loops. The 'Design Operating Zone' is the central area bounded by these loops. The 'Surging Zone' is the area to the left of the surging line, and the 'Choking Zone' is the area to the right of the choking line.

Figure 2. Compressor performance map.

#### 2.7.2. Compressor Mass Flow Rate Model

In a previous study, the first author of this paper carried out an applicable and comparative research of compressor mass flow rate empirical models to two marine large-scale compressors (A270-L59 and TCA88-25070 marine compressor) [15]. The range of applicable and comparative analysis included both the predictive accuracy in the design operating area and the extrapolative ability to the off-design operating areas. These off-design operating areas include the area with rotational speed lower than the lowest speed available in the performance map, the area with rotational speed higher than the highest speed as well as the area to the right of the curve that connects the points with maximum flow rate at each iso-speed curve. These off-design operating areas are named as LS (Low Speed), HS (High Speed) and LPR (Low Pressure Ratio) area, respectively, for convenience of expression. By analyzing the applicable and comparative results, it can be found that none of these compressor empirical models was able to achieve satisfactory predictive and extrapolative accuracy in the whole operating area simultaneously. To solve this problem, a zonal compressor mass flow rate model is proposed in this paper, which selects the model with the best accuracy for each operating area.

Based on the applicable and comparative results presented in Shen et al. [15], it can be found that for the A270-L59 turbocharger compressor, GuanCong model achieves the best predictive accuracy in the design operating area, Leufvén and Llamas ellipse model is capable of capturing the compressor choking phenomenon accurately, whereas the Karlson-II exponential model is able to extrapolate to the LS and HS area robustly and reliably. The detail description of the three models can be found in Shen et al. [15], which will be not introduced in this paper.

For implementing the zonal compressor mass flow rate model, it is necessary to define the zone division standard firstly. As shown in Figure 3, the lowest and highest iso-speed curve available in the compressor performance map is used as the border between the LS and HS area and the design operating area, respectively, whereas the curve connecting the points with maximum flow rate at each iso-speed curve is used to divide the LPR area from the other areas.

![Figure 3: Zone division standard of the compressor performance map. The graph plots Pressure Ratio (-) on the y-axis (1 to 5) against Mass Flow Rate [kg/s] on the x-axis (0 to 35). It shows several curves representing different operating zones: Design Operating Area (top left), High Speed (HS) Area (top right), Low Pressure Ratio (LPR) Area (bottom right), and Low Speed (LS) Area (bottom left).](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 3: Zone division standard of the compressor performance map. The graph plots Pressure Ratio (-) on the y-axis (1 to 5) against Mass Flow Rate [kg/s] on the x-axis (0 to 35). It shows several curves representing different operating zones: Design Operating Area (top left), High Speed (HS) Area (top right), Low Pressure Ratio (LPR) Area (bottom right), and Low Speed (LS) Area (bottom left).

**Figure 3.** Zone division standard of the compressor performance map.

The changing trend of pressure ratio  $\Pi_{lb}$  and mass flow rate  $\dot{m}_{lb}$  with rotational speed on this curve can be represented by using Equations (17) and (18), respectively. As shown in Figure 4, the exponential function is capable of capturing the changing trend of  $\Pi_{lb}$  with rotational speed accurately, which increases slowly under low rotational speed conditions and then rapidly under high rotational speed conditions; on the other hand, the changing trend of  $\dot{m}_{lb}$  can be described satisfactorily with the arc-tangent function. It is also found that the changing trend of the pressure ratio  $\Pi_{sur}$  and mass flow rate  $\dot{m}_{sur}$  with rotational speed on the surging line can be captured satisfactorily by using Equations (17) and (18) as shown in Figure 4.

$$\Pi_{lb} = a_1 e^{a_2 N_{tc}} + a_3 \quad (17)$$

$$\dot{m}_{lb} = b_1 + b_2 \arctan(b_3 N_{tc} + b_4) \quad (18)$$

![Figure 4: Measured pressure ratio and mass flow rate at the boundary of surging zone and low pressure ratio zone and corresponding fitting result. (a) Pressure Ratio [-] vs Rotational Speed [RPM] (0 to 2 x 10^4). (b) Mass Flow Rate [kg/s] vs Rotational Speed [RPM] (0 to 2 x 10^4). Both plots show measured values (circles for pressure ratio, diamonds for mass flow rate) and fitting results (dashed lines).](e8ff6e66c77a8e96203c9f8db8f0986f_img.jpg)

Figure 4: Measured pressure ratio and mass flow rate at the boundary of surging zone and low pressure ratio zone and corresponding fitting result. (a) Pressure Ratio [-] vs Rotational Speed [RPM] (0 to 2 x 10^4). (b) Mass Flow Rate [kg/s] vs Rotational Speed [RPM] (0 to 2 x 10^4). Both plots show measured values (circles for pressure ratio, diamonds for mass flow rate) and fitting results (dashed lines).

**Figure 4.** Measured pressure ratio and mass flow rate at the boundary of surging zone and low pressure ratio zone and corresponding fitting result: (a) pressure ratio; (b) mass flow rate.

To increase the reliability of Equations (17) and (18) when extrapolating to the LS area, two additional data points are added when parameterizing the two equations, that is the value of  $\Pi_{lb}$ ,  $\Pi_{sur}$ ,  $\dot{m}_{lb}$  and  $\dot{m}_{sur}$  when the rotational speed is equal to zero. It is assumed that  $\Pi_{lb} = \Pi_{sur} = 1$  and  $\dot{m}_{lb} = \dot{m}_{sur} = 0$  in this paper.

For the area to the left of the surging line, it is assumed that the mass flow rate is equal to  $\dot{m}_{sur}$  if the current pressure ratio is larger than the respective  $\Pi_{sur}$  under the current rotational speed condition.

Note that the mass flow rate predicted by the GuanCong model (or Karlson-II exponential model) when the pressure ratio is equal to  $\Pi_{lb}$  is usually different from the one predicted by the Leufvén and Llamas ellipse model. Therefore, to prevent the possible discontinuity phenomenon during the

simulation process when the operating point enters into the LPR area, a simple curve blending method is proposed in this paper with the following steps:

- (1) Estimate the mass flow rate by using the GuanCong model (or Karlson-II model) and the Leufvén and Llamas ellipse model, respectively, that is  $\dot{m}_{\text{GuanOrKarl}}$  and  $\dot{m}_{\text{ell}}$ ;
- (2) Calculate the weighting coefficient  $z$  according to Equations (19) and (20):

$$z = 3q^2 - 2q^3 \quad (19)$$

$$q = \frac{\Pi - 1}{\Pi_{\text{lb}} - 1} \quad (20)$$

where the range of  $z$  and  $q$  is between 0 and 1.

- (3) Blend  $\dot{m}_{\text{GuanOrKarl}}$  and  $\dot{m}_{\text{ell}}$  by using the weighting coefficient  $z$  according to Equation (21) to obtain the mass flow rate  $\dot{m}_{\text{LPR}}$  under the current pressure ratio and rotational speed condition.

$$\dot{m}_{\text{LPR}} = z \cdot \dot{m}_{\text{GuanOrKarl}} + (1 - z) \cdot \dot{m}_{\text{ell}} \quad (21)$$

By applying this curve blending method, it can guarantee the smooth transition of the iso-speed curve when the operating point enters into the LPR area from the other areas; in addition, it can fully take the advantage of the GuanCong model (or Karlson-II exponential model) and the Leufvén and Llamas ellipse model, which presents satisfactory predictive capability at the operating point with pressure ratio equal to  $\Pi_{\text{lb}}$  and 1, respectively.

Figure 5 presents the blending results in the LPR area as well as two extrapolated iso-speed curves in the LS and HS area, respectively. As can be observed from this figure, the zonal compressor mass flow rate model is capable of not only predicting the available measured data points accurately but also extrapolating to the off-design operating area robustly and reasonably, which can effectively improve the steady and transient simulation accuracy of the MVEM developed in this paper. In addition, as also can be observed in Figure 5, under low and medium speed conditions, obvious difference exists between the blended curve and the original curve, indicating the deficiency of GuanCong model (or Karlson-II exponential model) in capturing the choking phenomenon; however, the difference gets less obvious with the increase in rotational speed and this is because that under high speed conditions, the measured data points available in the compressor map are very close to the choking point or have already choked, which can be estimated accurately by the GuanCong model (or Karlson-II exponential model), so the blending manipulation is unnecessary.

![Figure 5: Prediction and extrapolation result of the zonal compressor mass flow rate model. The graph plots Pressure Ratio [-] on the y-axis (ranging from 1 to 5) against Mass Flow Rate [kg/s] on the x-axis (ranging from 0 to 30). Several iso-speed curves are shown for different rotational speeds: 6600 RPM (pink), 9000 RPM (black), 11400 RPM (black), 13800 RPM (black), 16200 RPM (black), and 17200 RPM (cyan). Measured data points are represented by open circles. The GuanCong Model is shown as a solid black line, the Leufvén & Llamas ellipse model as a solid blue line, and the Curve Blending as a solid green line. The blending is applied in the Low Pressure Ratio (LPR) region, where the GuanCong model and the ellipse model are combined to provide a more accurate prediction of the mass flow rate.](71d82d389da5fe06a4aefb661ea17af9_img.jpg)

Figure 5: Prediction and extrapolation result of the zonal compressor mass flow rate model. The graph plots Pressure Ratio [-] on the y-axis (ranging from 1 to 5) against Mass Flow Rate [kg/s] on the x-axis (ranging from 0 to 30). Several iso-speed curves are shown for different rotational speeds: 6600 RPM (pink), 9000 RPM (black), 11400 RPM (black), 13800 RPM (black), 16200 RPM (black), and 17200 RPM (cyan). Measured data points are represented by open circles. The GuanCong Model is shown as a solid black line, the Leufvén & Llamas ellipse model as a solid blue line, and the Curve Blending as a solid green line. The blending is applied in the Low Pressure Ratio (LPR) region, where the GuanCong model and the ellipse model are combined to provide a more accurate prediction of the mass flow rate.

**Figure 5.** Prediction and extrapolation result of the zonal compressor mass flow rate model.



### 2.7.3. Compressor Isentropic Efficiency Model

The compressor isentropic efficiency model developed in this paper is based on the one originally proposed by Hadef et al., which is referred to as “Hedef model” herein [16]. The theoretical foundation of the Hedef model is the Euler equation for turbo-machinery, meanwhile, two assumptions are made: (1) air is only accelerated when flowing through the compressor impeller without being any compressed, thus, the air density at the impeller inlet and outlet can be assumed to be identical; (2) under given rotational speed condition, the airflow angle at the impeller outlet does not change with the mass flow rate. Based on the two assumptions, it can be concluded that under given rotational speed condition, the actual specific enthalpy change varies linearly with the mass flow rate as can be observed in Figure 6. Consequently, the Euler equation can be re-written as:

$$\Delta h_{act} = b(N_{tc}) - a(N_{tc})\dot{m}_c \quad (22)$$

$$a(N_{tc}) = 0 + a_1N_{tc} + a_2N_{tc}^2 \quad (23)$$

$$b(N_{tc}) = 0 + b_1N_{tc} + b_2N_{tc}^2 \quad (24)$$

where  $a$  and  $b$  are the slope and intercept, respectively.

![Figure 6: A scatter plot showing the relationship between Actual Specific Enthalpy Change (J/kg) on the y-axis (scaled by 10^5) and Mass Flow Rate (kg/s) on the x-axis. The plot displays multiple iso-speed curves for rotational speeds N_tc = 16800 RPM and N_tc = 7200 RPM. Measured data points are shown as open circles, and linear fitting results are shown as dashed lines. The plot is divided into two zones: Zone 1 (lower flow rates) and Zone 18 (higher flow rates).](0ac183e926716c7de215c87c38e61dbc_img.jpg)

Figure 6: A scatter plot showing the relationship between Actual Specific Enthalpy Change (J/kg) on the y-axis (scaled by 10^5) and Mass Flow Rate (kg/s) on the x-axis. The plot displays multiple iso-speed curves for rotational speeds N\_tc = 16800 RPM and N\_tc = 7200 RPM. Measured data points are shown as open circles, and linear fitting results are shown as dashed lines. The plot is divided into two zones: Zone 1 (lower flow rates) and Zone 18 (higher flow rates).

**Figure 6.** Relationship between actual specific enthalpy change and mass flow rate at each rotational speed condition (interval between each iso-speed curve is 600 RPM).

By applying Equations (22)–(24) with the model parameters calibrated by using Least Square Method (LSM), the actual specific enthalpy change can be calculated under the given rotational speed and mass flow rate condition. On the other hand, the specific enthalpy change under the ideal isentropic process can be derived by Equation (25). Subsequently, the compressor isentropic efficiency can be calculated according to its definition ( $\eta_c = \Delta h_{is} / \Delta h_{act}$ ).

$$\Delta h_{is} = c_{p,a}T_{c,in} \left( \Pi_c^{\frac{y_a-1}{y_a}} - 1 \right) \quad (25)$$

As can be observed from Figure 6, under high rotational speed conditions, distinguishable non-linear decreasing trend in the actual specific enthalpy change occurs as the mass flow rate gradually approaches to the choking point. As a result, the model’s predictive accuracy will be polluted if the model parameters are calibrated by using all the available measured data points in the compressor map. To solve this problem, a zonal modeling approach based on the Hedef model is proposed, which is referred to as “zonal isentropic efficiency model” in this paper. The basic idea is to divide the whole  $\Delta h_{act} - \dot{m}_c$  plane as shown in Figure 6 into several zones depending on the iso-speed curves available

in the performance map, and then each zone is individually calibrated by using the measured data points at the current zone's upper and lower iso-speed curve.

To compare the predictive accuracy of the Hedef model and the zonal isentropic efficiency model proposed in this paper, five error evaluation criteria, including  $R_c^2$ ,  $RD_{\max}$ ,  $MAPE$ ,  $PEB_{\pm 5\%}$  and  $PEB_{\pm 10\%}$ , are adopted, the definitions of which can be found in Shen et al. [15].

Figures 7 and 8 present the predictive results and the relative error distribution for the two isentropic efficiency models, respectively, whereas Table 2 presents respective error evaluation criteria results. Note that for depicting the predictive results clearly, only five iso-speed curves (7200, 9600, 12000, 14400, 16800 rpm) are presented in Figures 7a and 8a. As can be observed from Figures 7a and 8a, both models are capable of capturing the changing trend of the isentropic efficiency with mass flow rate. Nevertheless, it can be found from Figures 7b and 8b as well as Table 2 that the predictive accuracy of the zonal isentropic efficiency model is better than the Hedef model with lower  $RD_{\max}$  and  $MAPE$  and higher  $R_c^2$ ; in addition, the relative errors of all the predictive results are within  $\pm 5\%$ . The better predictive accuracy of the zonal isentropic efficiency model mainly benefits from the zonal modeling approach. With this approach, the working characteristic of the compressor within different speed range can be captured much more accurately.

![Figure 7: Predictive result and error distribution for Hedef isentropic efficiency model. (a) Predictive result: A line graph showing Isentropic Efficiency [-] on the y-axis (0.6 to 0.9) versus Mass Flow Rate [kg/s] on the x-axis (0 to 30). It features five iso-speed curves for 7200, 9600, 12000, 14400, and 16800 RPM, along with measured data points. (b) Error distribution: A scatter plot of Predicted Isentropic Efficiency [-] versus Measured Isentropic Efficiency [-], showing the distribution of relative errors with various error bands.](602ada2a012ff3cc38d91de2eec5b450_img.jpg)

Figure 7: Predictive result and error distribution for Hedef isentropic efficiency model. (a) Predictive result: A line graph showing Isentropic Efficiency [-] on the y-axis (0.6 to 0.9) versus Mass Flow Rate [kg/s] on the x-axis (0 to 30). It features five iso-speed curves for 7200, 9600, 12000, 14400, and 16800 RPM, along with measured data points. (b) Error distribution: A scatter plot of Predicted Isentropic Efficiency [-] versus Measured Isentropic Efficiency [-], showing the distribution of relative errors with various error bands.

**Figure 7.** Predictive result and error distribution for Hedef isentropic efficiency model: (a) predictive result; (b) error distribution.

![Figure 8: Prediction result and error distribution for compressor zonal isentropic efficiency model. (a) Predictive result: A line graph similar to Figure 7a, showing Isentropic Efficiency [-] versus Mass Flow Rate [kg/s] for the same RPM values and measured data points. (b) Error distribution: A scatter plot similar to Figure 7b, showing Predicted Isentropic Efficiency [-] versus Measured Isentropic Efficiency [-] for the zonal model, with tighter error bands indicating higher predictive accuracy.](6279fafb3a874e174648eb907385c954_img.jpg)

Figure 8: Prediction result and error distribution for compressor zonal isentropic efficiency model. (a) Predictive result: A line graph similar to Figure 7a, showing Isentropic Efficiency [-] versus Mass Flow Rate [kg/s] for the same RPM values and measured data points. (b) Error distribution: A scatter plot similar to Figure 7b, showing Predicted Isentropic Efficiency [-] versus Measured Isentropic Efficiency [-] for the zonal model, with tighter error bands indicating higher predictive accuracy.

**Figure 8.** Prediction result and error distribution for compressor zonal isentropic efficiency model: (a) predictive result; (b) error distribution.

**Table 2.** Error evaluation criteria result for Hadef model and zonal compressor isentropic efficiency model.

| Model                             | $R_c^2$ | $RD_{\max}(\%)$ | $MAPE(\%)$ | $PEB_{\pm 5\%}(\%)$ | $PEB_{\pm 10\%}(\%)$ |
|-----------------------------------|---------|-----------------|------------|---------------------|----------------------|
| Hadef model                       | 0.9675  | 6.7967          | 0.9038     | 98.9619             | 100                  |
| Zonal isentropic efficiency model | 0.9858  | 2.5535          | 0.6428     | 100                 | 100                  |

As similar with the compressor mass flow rate model, the isentropic efficiency model is also required to extrapolate to the off-design operating area robustly and accurately. When extrapolating to the LS and HS area, the model parameters belonging to the first and last zone is adopted, respectively. As the definition of isentropic efficiency is directly adopted, the isentropic efficiency value will necessarily be zero when the pressure ratio is equal to 1, which guarantees the model's LPR area extrapolative accuracy to a certain extent.

For the compressor isentropic efficiency model, besides the pressure ratio and rotational speed, the mass flow rate is also required as the input variable. By incorporating the compressor mass flow rate model developed in Section 2.7.2, which is capable of extrapolating to the off-design operating area robustly and accurately, the extrapolative ability of the zonal isentropic efficiency model can be investigated. Figure 9 presents the corresponding isentropic efficiency extrapolative results. As can be observed from this figure, when extrapolating to the LPR area, each iso-speed curve is capable of achieving a smooth transition to the operating point with pressure ratio and isentropic efficiency equal to 1 and 0, respectively; when extrapolating to the LS and HS area, the changing trend of the extrapolated iso-speed curve is similar with the other iso-speed curves available in the compressor performance map, respectively, which verifies the rationality of the extrapolative strategy in this paper to a certain extent.

To further verify the extrapolative ability of the zonal isentropic efficiency model in the LS and HS area, the first and last iso-speed curves in the performance map are removed firstly, and then the model is calibrated with the remaining measured data points and the removed iso-speed curves are extrapolated by using the model, finally the removed iso-speed curves are compared with the extrapolated results to evaluate the model's extrapolative ability. Figure 10 shows the extrapolative results in the LS and HS area, respectively. As can be observed from Figure 10b, satisfactory HS area extrapolative results are achieved with an  $MAPE$  of only 0.8422%; on the other hand, although it is slightly inferior with respect to that in the HS area, the model's LS area extrapolative accuracy is still satisfactory with an  $MAPE$  of 2.0318%.

![Figure 9: A line graph showing the prediction and extrapolation results of the zonal compressor isentropic efficiency model. The y-axis is 'Isentropic Efficiency [-]' ranging from 0 to 0.9. The x-axis is 'Mass Flow Rate [kg/s]' ranging from 0 to 30. The legend includes: 6600 RPM (LS Extrapolation Iso-Speed Curve) in cyan, 7200 RPM in red, 9600 RPM in green, 12000 RPM in magenta, 14400 RPM in black, 16800 RPM in blue, 17200 RPM (HS Extrapolation Iso-Speed Curve) in dark blue, and Measured Data Points in open circles. The graph shows several bell-shaped curves representing different RPMs, with the extrapolated curves (LS and HS) matching the trend of the measured data points and other RPM curves.](c222a9006d6d60a8d81e6ffbfc0e74ad_img.jpg)

Figure 9: A line graph showing the prediction and extrapolation results of the zonal compressor isentropic efficiency model. The y-axis is 'Isentropic Efficiency [-]' ranging from 0 to 0.9. The x-axis is 'Mass Flow Rate [kg/s]' ranging from 0 to 30. The legend includes: 6600 RPM (LS Extrapolation Iso-Speed Curve) in cyan, 7200 RPM in red, 9600 RPM in green, 12000 RPM in magenta, 14400 RPM in black, 16800 RPM in blue, 17200 RPM (HS Extrapolation Iso-Speed Curve) in dark blue, and Measured Data Points in open circles. The graph shows several bell-shaped curves representing different RPMs, with the extrapolated curves (LS and HS) matching the trend of the measured data points and other RPM curves.

**Figure 9.** Prediction and extrapolation result of the zonal compressor isentropic efficiency model.

![Figure 10: Extrapolation result of the zonal compressor isentropic efficiency model. (a) LS (Low Speed) area extrapolation result: A scatter plot of measured data points (open circles) and a dashed line representing the LS extrapolation result. The x-axis is Mass Flow Rate [kg/s] (4.5 to 9.5) and the y-axis is Isentropic Efficiency [-] (0.66 to 0.86). (b) HS (High Speed) area extrapolation result: A scatter plot of measured data points (open circles) and a dashed line with downward-pointing triangle markers representing the HS extrapolation result. The x-axis is Mass Flow Rate [kg/s] (22.5 to 27) and the y-axis is Isentropic Efficiency [-] (0.6 to 0.9).](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 10: Extrapolation result of the zonal compressor isentropic efficiency model. (a) LS (Low Speed) area extrapolation result: A scatter plot of measured data points (open circles) and a dashed line representing the LS extrapolation result. The x-axis is Mass Flow Rate [kg/s] (4.5 to 9.5) and the y-axis is Isentropic Efficiency [-] (0.66 to 0.86). (b) HS (High Speed) area extrapolation result: A scatter plot of measured data points (open circles) and a dashed line with downward-pointing triangle markers representing the HS extrapolation result. The x-axis is Mass Flow Rate [kg/s] (22.5 to 27) and the y-axis is Isentropic Efficiency [-] (0.6 to 0.9).

**Figure 10.** Extrapolation result of the zonal compressor isentropic efficiency model: (a) LS (Low Speed) area extrapolation result; (b) HS (High Speed) area extrapolation result.

# 3. Model Calibration and Results

## 3.1. Model Calibration

As can be found from Section 2, there are several model parameters to be calibrated. Engine geometrical parameters are extracted from the engine project guide. For the model parameters available in the turbocharger model, they are calibrated by using the performance map. Model parameters in several engine component sub-models, such as air cooler cooling efficiency and pressure drop, are estimated by using the engine shop trial report, which provides the measured engine performance parameters at several steady loading conditions. The last four model parameters remained to be determined include  $k_{CA0}$ ,  $k_{CA1}$ ,  $k_{\zeta 0}$  and  $k_{\zeta 1}$ , which have significant influences on the MVEM's predictive accuracy. For estimating the four model parameters based on the measured data provided in engine shop trial report, the Parameter Estimation toolbox provided by MATLAB/Simulink is used, which converts the model parameter estimation problem to numerical optimization problem. In general, the model parameter calibration procedure is carried out in three steps as following:

(1) Initialization of  $k_{CA0}$  and  $k_{CA1}$ . In this step, it is assumed that  $\dot{m}_{sz}$  is equal to the compressor mass flow rate  $\dot{m}_c$ , which, in turn, can be estimated by using the compressor model. Based on this assumption, the initial value of  $C_z A_z$  at each engine loading condition can be estimated by using Equation (1), and then the initial value of  $k_{CA0}$  and  $k_{CA1}$  can be estimated;

(2) Initialization of  $k_{\zeta 0}$  and  $k_{\zeta 1}$ . For estimating the initial value of  $\zeta$  at each engine loading condition, the Parameter Estimation toolbox is adopted for the whole engine model. Non-linear least square method is selected as the optimization method. The initial value of  $C_z A_z$  obtained in step 1 is regarded as known quantity in this step. The input variable required only includes the engine speed, whereas the output variables include pressure and temperature in the scavenging and exhaust manifolds as well as the turbocharger rotational speed. The sum of squares of the errors between the predicted and measured value of the selected output variables is used as the cost function. As a result, the initial value of  $\zeta$  at each engine loading condition can be estimated. Consequently,  $k_{\zeta 0}$  and  $k_{\zeta 1}$  can be initialized;

(3) Final calibration of  $k_{CA0}$ ,  $k_{CA1}$ ,  $k_{\zeta 0}$  and  $k_{\zeta 1}$ . The four model parameters are calibrated simultaneously in this step, the values of which obtained in step 2 are used as the initial values. Note that the calibration process in this step is carried out by using the measured data at all the engine loading conditions simultaneously with the cost function as shown in Equation (26).

$$V(\varphi) = \frac{1}{NS} \sum_{i=1}^{S} \sum_{n=1}^{N} (e^i[n])^2 \quad (26)$$

where  $N$  is the number of measured loading points available in the engine shop trial report;  $S$  is number of selected output variables;  $\varphi$  represents the parameters to be estimated.

## 3.2. Engine Steady State Performance

In order to validate the MVEM developed in this paper, the engine steady state operation was simulated at 15%, 25%, 50%, 75%, 80% and 100% of the engine MCR point. The predicted engine performance parameters were compared to the respective measured values provided in the engine shop trial report, whereas their relative errors are presented in Table 3. To assess the prediction accuracy of the MVEM developed in this paper, the simulation results shown in the paper published by Tang et al. from the same research group is also presented in Table 3 for comparison [5]. The same engine was adopted as the simulation object in Tang et al. but the engine model was developed by using the 0-D modeling approach [5].

**Table 3.** Relative error of the engine performance parameters.

| Engine Load (%)                  | 15        | 25    | 50    | 75    | 80    | 100   |
|----------------------------------|-----------|-------|-------|-------|-------|-------|
|                                  | Error (%) |       |       |       |       |       |
| Brake Power                      | 0.74      | -0.94 | 0.63  | 0.55  | 0.35  | 0.04  |
| Brake Power [5]                  | null      | 1.61  | 2.21  | 0.38  | 0.46  | 0.56  |
| BSFC                             | -0.18     | 0.58  | -0.47 | -0.50 | -0.06 | -0.74 |
| BSFC [5]                         | null      | 3.02  | 1.70  | 0.38  | 0.46  | 0.56  |
| Scavenging manifold pressure     | 1.43      | 1.80  | 3.45  | 1.94  | 2.14  | 1.16  |
| Scavenging manifold pressure [5] | null      | -3.23 | -1.27 | 0     | 0.28  | 0     |
| Exhaust manifold pressure        | -3.20     | -5.21 | -3.19 | -2.63 | -1.26 | -0.89 |
| Exhaust manifold temperature     | -0.02     | -1.70 | -2.38 | -2.27 | -1.92 | -1.87 |
| Exhaust manifold temperature [5] | null      | 0.73  | 1.75  | 1.31  | -1    | -0.22 |
| Turbocharger speed               | -0.043    | -0.55 | 1.69  | 0.14  | 0.74  | 0.49  |
| Turbocharger speed [5]           | null      | -2.43 | -0.98 | -1.14 | -2.08 | -1.34 |
| Compressor outlet temperature    | 1.21      | -0.42 | 2.68  | 0.23  | 0.60  | -0.22 |
| Turbine outlet temperature       | 3.59      | 2.85  | 3.42  | 2.31  | 2.23  | 3.09  |

As can be observed from Table 3, satisfactory predictive accuracy was obtained at each investigated engine loading condition with all the relative errors of brake power and BSFC (Brake Specific Fuel Consumption) less than 1%, whereas most of the relative errors of the other engine performance parameters are less than 4%. The measured turbocharger rotational speed is 4981 rpm at 15% engine load, which is lower than the lowest speed available in the compressor performance map. On the other hand, the predicted turbocharger rotational speed is 4979 rpm at this load condition with an extreme low relative error of only -0.043%, indicating the fidelity of the novel compressor model when extrapolating to the LS area. In addition, except for the 50% engine load, the relative errors of the compressor outlet temperature are all around 1%, indicating the satisfactory predictive accuracy of the zonal compressor isentropic efficiency model.

In the research carried out by Tang et al., only the relative errors of brake power, BSFC, scavenging manifold pressure, exhaust manifold temperature and turbocharger speed are presented; in addition, the relative errors at 15% engine load are not provided, perhaps it is because unsatisfactory simulation accuracy was achieved at this load condition [5]. For brake power, BSFC and turbocharger rotational speed, better simulation accuracy is generally obtained with the MVEM. The compressor model developed in this paper contributes to the better simulation accuracy of the MVEM in turbocharger rotational speed with respect to the 0-D model developed by Tang et al. where the compressor is modeled by using look-up table method [5]. Although better simulation accuracy is achieved with the 0-D model for scavenging manifold pressure and exhaust manifold temperature, the difference is not significant and they all meet the requirement on simulation accuracy; on the other hand, it should be noted that the MVEM runs much faster than the 0-D model.

As the model calibration procedure was carried out based on the measured engine performance parameters provided by the engine shop trial report and the model validation was also implemented by comparing the predicted results to these measured ones, therefore, in order to further validate the fidelity of the MVEM, the Computerized Engine Application System-Engine Room Dimensioning tool provided in the official website of MAN Diesel & Turbo is used to generate engine performance parameters within the engine load region from 15% to 100%. However, it should be noted that the engine performance parameters generated by using CEAS (Computerized Engine Application System) tool is for 7S80ME-C9.5 engine and the respective LHV (Lower Heating Value) of fuel is 42700 kJ/kg, whereas the investigated engine in this paper is 7S80ME-C9.2 and the LHV is 42151 kJ/kg, which will inevitably cause deviations on the engine performance parameters between the engine shop trial report and the CEAS. Despite these limitations, the results generated by CEAS is very valuable for reference in investigating the qualitative changing trend of engine performance parameters with engine load condition.

Figure 11 presents the engine performance parameters predicted by the MVEM and calculated by the CEAS within the load region from 15% to 100%. In addition, the measured values obtained from the engine shop trial report are also plotted in Figure 11 for reference. As can be observed from Figure 11, despite the existing of deviations, the simulation results for brake power, SFOC, scavenging manifold pressure and temperature and the turbine outlet temperature all agree well with the results obtained from the CEAS qualitatively. In addition, the other engine performance parameters also vary reasonably with the engine load.

At 65% engine load, the BSFC and turbine outlet temperature predicted by the MVEM reaches the minimum, indicating that the engine and turbocharger achieves the optimal operating state, which is consistent with the fitted BSFC curve based on the measured data as shown in Figure 11b. It should be noted that this optimal load is obviously lower than that of marine two-stroke diesel engines designed in earlier years. One reason of this relatively low optimal engine load is that low steaming is taken into account during the ship design phase in recent years. Noticeable discontinuity is observed at 35% engine load and this is because that below this load, the auxiliary blower is activated, which results in a larger amount of scavenging air supplied to the cylinder and thus lowers the fuel-air equivalence ratio as shown in Figure 11j. Consequently, with respect to 35% engine load, the fuel-air equivalence ratio at 30% load decreases from 0.3182 to 0.2872, the exhaust gas manifold temperature decreases from 573.3 K to 542.2 K and the turbine outlet temperature decreases form 515 K to 492.5 K; in addition, the scavenging manifold temperature increases from 299.2 K to 304.8 K mainly owing to the compression effect by the auxiliary blower. When the engine load decreases from 25% to 20%, the exhaust outlet temperature increases slightly from 486.9 K to 488.4 K, whereas it decreases from 488.4 K to 486 K when the engine load decreases from 20% to 15%. The opposite phenomenon in the two engine load interval (25%–20% and 20%–15%) is caused probably by the different changing rate of fuel injection rate and air mass flow rate with engine load, which is represented by the changing trend of fuel-air equivalence ratio as shown in Figure 11j.

![Figure 11. Cont. showing six subplots (a-f) comparing engine performance metrics against load percentage for CEAS, Engine Shop Trial Report, and MVEM models.](f4d72193f77f6646a2a1f4baaa927154_img.jpg)

Figure 11. Cont. displays six subplots (a-f) comparing engine performance metrics against Load [%] (ranging from 10 to 100) for three models: CEAS (red asterisks), Engine Shop Trial Report (blue triangles), and MVEM (black circles). The plots show:

- (a) Power [kW]:** Power increases linearly with load. The y-axis is scaled by  $\times 10^4$ . CEAS and MVEM show a nearly identical linear increase from approximately 0.4 to 2.5  $\times 10^4$  kW. The Engine Shop Trial Report shows a slightly higher power output at low loads and a lower output at high loads compared to the other two models.
- (b) BSFC [g/kWh]:** Brake Specific Fuel Consumption decreases with load, reaching a minimum around 60-70% load. CEAS shows a parabolic trend with a minimum at approximately 70% load. The Engine Report shows a higher BSFC at low loads and a lower BSFC at high loads. MVEM shows a relatively flat curve. A fitting equation is provided:  $y = 0.00559 \times x^2 - 0.7161 \times x + 184.1$  with  $R^2 = 0.9867$ .
- (d) Exhaust Manifold Temperature [K]:** Temperature increases with load. CEAS and MVEM show a similar increasing trend. The Engine Shop Trial Report shows a lower temperature at low loads and a higher temperature at high loads compared to the other two models.
- (e) Scavenging Manifold Pressure [bar]:** Pressure increases with load. CEAS and MVEM show a similar increasing trend. The Engine Shop Trial Report shows a lower pressure at low loads and a higher pressure at high loads compared to the other two models.
- (f) Scavenging Manifold Temperature [K]:** Temperature increases with load. CEAS and MVEM show a similar increasing trend. The Engine Shop Trial Report shows a lower temperature at low loads and a higher temperature at high loads compared to the other two models.

Figure 11. Cont. showing six subplots (a-f) comparing engine performance metrics against load percentage for CEAS, Engine Shop Trial Report, and MVEM models.

Figure 11. Cont.

![Figure 11: Steady state simulation results and comparison with engine shop trial report and CEAS. The figure consists of four subplots: (g) Compressor Outlet Temperature [K] vs Load [%], (h) Turbine Outlet Temperature [K] vs Load [%], (i) Turbocharger Rotational Speed [RPM] vs Load [%], and (j) Fuel-Air Equivalence Ratio [-] vs Load [%]. Each plot compares Engine Shop Trial Report (blue triangles), MVEM (black circles), and CEAS (red stars).](b6750d26d3dd287a4a4d49b3670a44bd_img.jpg)

Figure 11 consists of four subplots (g), (h), (i), and (j) showing steady-state simulation results for various engine parameters against Load [%] from 10% to 100%.

- (g) Compressor Outlet Temperature [K]:** The temperature increases linearly from approximately 305 K at 10% load to 465 K at 100% load. All three data series (Engine Shop Trial Report, MVEM, and CEAS) are in close agreement.
- (h) Turbine Outlet Temperature [K]:** The temperature starts at ~465 K, peaks at ~520 K around 35% load, and then fluctuates between 475 K and 540 K. The Engine Shop Trial Report (blue triangles) shows a lower temperature profile compared to MVEM (black circles) and CEAS (red stars).
- (i) Turbocharger Rotational Speed [RPM] (scaled by  $\times 10^4$ ):** The speed increases from ~0.5  $\times 10^4$  RPM at 10% load to ~1.6  $\times 10^4$  RPM at 100% load. All three data series are in close agreement.
- (j) Fuel-Air Equivalence Ratio [-]:** The ratio starts at ~0.285, drops to a minimum of ~0.28 at 25% load, peaks at ~0.32 at 35% load, and then increases to ~0.37 at 100% load. The MVEM (black circles) data shows significant fluctuations, while the other two series are smoother.

Figure 11: Steady state simulation results and comparison with engine shop trial report and CEAS. The figure consists of four subplots: (g) Compressor Outlet Temperature [K] vs Load [%], (h) Turbine Outlet Temperature [K] vs Load [%], (i) Turbocharger Rotational Speed [RPM] vs Load [%], and (j) Fuel-Air Equivalence Ratio [-] vs Load [%]. Each plot compares Engine Shop Trial Report (blue triangles), MVEM (black circles), and CEAS (red stars).

**Figure 11.** Steady state simulation results and comparison with engine shop trial report and CEAS (Computerized Engine Application System): (a) brake power; (b) brake specific fuel consumption (BSFC); (c) exhaust manifold pressure; (d) exhaust manifold temperature; (e) scavenging manifold pressure; (f) scavenging manifold temperature; (g) compressor outlet temperature; (h) turbine outlet temperature; (i) turbocharger rotational speed; (j) fuel-air equivalence ratio.

## 3.3. Engine Transient Response

For the purpose of investigating the transient response of the MVEM as well as the compressor model developed in this paper, two simulation experiments are carried out in this paper. In the first experiment, the engine setting speed steps down from 72 rpm to 66.8 rpm at 500 s, from 66.8 rpm to 60.7 rpm at 1000 s, from 60.7 rpm to 57.1 rpm at 1500 s, from 57.1 rpm to 50.7 rpm at 2000 s, from 57.1 rpm to 45.4 rpm at 3000 s, from 45.4 rpm to 38.3 rpm at 4000 s. These engine speeds correspond to 100%, 80%, 60%, 50%, 35%, 25% and 15% engine load, respectively, thus covering the whole engine operating envelope. As shown in Figure 12, the engine rotational speed, brake power and fuel index are able to stabilize in a short time, whereas it takes more time for the other engine performance parameters until stabilization. This phenomenon is caused mainly by the turbocharger inertia as well as the relatively large volume of the scavenging and exhaust manifolds. As shown in Figure 12b, with the decrease in engine setting speed, the turbocharger rotational speed gradually decreases. Starting from 4050 s, the turbocharger rotational speed becomes lower than 7200 rpm, which is the lowest speed available in the compressor performance map, and then enters into the LS off-design operating area, finally the turbocharger rotational speed stabilizes at 4990 rpm. As can be inferred from the trajectory of the compressor operating points as shown in Figure 12j, the compressor model developed in this paper is capable of interpolating within the design operating area and extrapolating to the LS off-design operating area reasonably and robustly.

![Figure 12: Simulation results for engine transient operation. The figure consists of ten subplots (a-j) showing various engine parameters over time (0 to 5000 seconds). (a) Engine Speed [RPM] vs Time [s]: Engine Speed Transient Response (red line) and Engine Setting Speed (blue dashed line). (b) Turbocharger Speed [RPM] vs Time [s]: Turbocharger Speed Transient Response (red line). (c) Temperature [K] vs Time [s]: Exhaust Manifold Temperature Transient Response (red line) and Turbine Outlet Temperature Transient Response (blue line). (d) Temperature [K] vs Time [s]: Scavenging Manifold Temperature Transient Response (red line) and Compressor Outlet Temperature Transient Response (blue line). (e) Pressure [bar] vs Time [s]: Scavenging Manifold Pressure Transient Response (red line) and Exhaust Manifold Pressure Transient Response (blue line). (f) Fuel Air Equivalence Ratio [-] vs Time [s]: Fuel Air Equivalence Ratio Transient Response (red line). (g) Power [W] vs Time [s]: Brake Power Transient Response (red line). (h) Fuel Index [-] vs Time [s]: Fuel Index Transient Response (red line). (i) BSFC [g/kWh] vs Time [s]: Brake Specific Fuel Consumption Transient Response (red line). (j) Compressor operating points trajectory: Pressure Ratio [-] vs Mass Flow Rate [kg/s]. The trajectory shows simulated compressor operating points (blue circles) and iso-speed curves (red lines) for 7200 RPM and 16900 RPM.](7bed2d7c96d86bf922295a1252da52a5_img.jpg)

Figure 12: Simulation results for engine transient operation. The figure consists of ten subplots (a-j) showing various engine parameters over time (0 to 5000 seconds). (a) Engine Speed [RPM] vs Time [s]: Engine Speed Transient Response (red line) and Engine Setting Speed (blue dashed line). (b) Turbocharger Speed [RPM] vs Time [s]: Turbocharger Speed Transient Response (red line). (c) Temperature [K] vs Time [s]: Exhaust Manifold Temperature Transient Response (red line) and Turbine Outlet Temperature Transient Response (blue line). (d) Temperature [K] vs Time [s]: Scavenging Manifold Temperature Transient Response (red line) and Compressor Outlet Temperature Transient Response (blue line). (e) Pressure [bar] vs Time [s]: Scavenging Manifold Pressure Transient Response (red line) and Exhaust Manifold Pressure Transient Response (blue line). (f) Fuel Air Equivalence Ratio [-] vs Time [s]: Fuel Air Equivalence Ratio Transient Response (red line). (g) Power [W] vs Time [s]: Brake Power Transient Response (red line). (h) Fuel Index [-] vs Time [s]: Fuel Index Transient Response (red line). (i) BSFC [g/kWh] vs Time [s]: Brake Specific Fuel Consumption Transient Response (red line). (j) Compressor operating points trajectory: Pressure Ratio [-] vs Mass Flow Rate [kg/s]. The trajectory shows simulated compressor operating points (blue circles) and iso-speed curves (red lines) for 7200 RPM and 16900 RPM.

**Figure 12.** Simulation results for the engine transient operation with setting speed changes: (a) engine rotational speed; (b) turbocharger rotational speed; (c) exhaust manifold and turbine outlet temperature; (d) scavenging manifold and compressor outlet temperature; (e) scavenging and exhaust manifold pressure; (f) fuel-air equivalence ratio; (g) brake power; (h) fuel index; (i) BSFC; (j) compressor operating points trajectory.

Figure 13 presents the engine transient response with a setting speed of 72 RPM when the resistant torque steps up at the 100th s. As can be observed from this figure, the engine rotational speed drops down quickly when the resistant torque increases. Then, under the control of engine governor, more fuel will be injected into the cylinders to balance the increased resistant torque for stabilizing the engine speed. Consequently, more thermal energy will be stored in the exhaust gas, which drives the turbocharger to work with higher rotational speed. Finally, the scavenging manifold pressure increases and more air flows into the engine cylinders. In addition, as can be inferred from the trajectory of the

compressor operating points as shown in Figure 13j, the compressor model is able to extrapolate to the HS off-design operating area reasonably and robustly.

![Figure 13: Simulation results for engine transient operation. The figure consists of 10 subplots (a-j) showing various engine parameters over time (0 to 300 seconds). (a) Engine Speed [RPM] vs Time [s]. (b) Turbocharger Speed [RPM] vs Time [s]. (c) Exhaust Manifold Temperature [K] and Turbine Outlet Temperature [K] vs Time [s]. (d) Scavenging Manifold Temperature [K] and Compressor Outlet Temperature [K] vs Time [s]. (e) Scavenging Manifold Pressure [bar] and Exhaust Manifold Pressure [bar] vs Time [s]. (f) Fuel Air Equivalence Ratio [λ] vs Time [s]. (g) Brake Power [W] vs Time [s]. (h) Fuel Index [l] vs Time [s]. (i) BSFC [g/kWh] vs Time [s]. (j) Compressor operating points trajectory showing Pressure Ratio [l] vs Mass Flow Rate [kg/s] and RPM. The trajectory shows iso-speed curves and simulated operating points for 7200 RPM and 16800 RPM.](9260ae281f6b6470331f4a0f82dbc2b1_img.jpg)

Figure 13: Simulation results for engine transient operation. The figure consists of 10 subplots (a-j) showing various engine parameters over time (0 to 300 seconds). (a) Engine Speed [RPM] vs Time [s]. (b) Turbocharger Speed [RPM] vs Time [s]. (c) Exhaust Manifold Temperature [K] and Turbine Outlet Temperature [K] vs Time [s]. (d) Scavenging Manifold Temperature [K] and Compressor Outlet Temperature [K] vs Time [s]. (e) Scavenging Manifold Pressure [bar] and Exhaust Manifold Pressure [bar] vs Time [s]. (f) Fuel Air Equivalence Ratio [λ] vs Time [s]. (g) Brake Power [W] vs Time [s]. (h) Fuel Index [l] vs Time [s]. (i) BSFC [g/kWh] vs Time [s]. (j) Compressor operating points trajectory showing Pressure Ratio [l] vs Mass Flow Rate [kg/s] and RPM. The trajectory shows iso-speed curves and simulated operating points for 7200 RPM and 16800 RPM.

**Figure 13.** Simulation results for the engine transient operation with resistant torque changes: (a) engine rotational speed; (b) turbocharger rotational speed; (c) exhaust manifold and turbine outlet temperature; (d) scavenging manifold and compressor outlet temperature; (e) scavenging and exhaust manifold pressure; (f) fuel-air equivalence ratio; (g) brake power; (h) fuel index; (i) BSFC; (j) compressor operating points trajectory.

# 4. Coupling of MVEM with Cylinder Pressure Analytic Model

As discussed in the Introduction section, MVEM is unable to predict the in-cylinder pressure trace, which weakens MVEM's practical value to some extent. To solve this problem, the cylinder pressure analytic model proposed by Eriksson and Andersson for the four-stroke spark ignition (SI) engine was adapted to the 7S80ME-C9.2 marine two-stroke diesel engine and coupled to the MVEM developed in 

this paper [10]. The major merit of this analytic model is that the calculation of in-cylinder pressure is completely based on algebraic equations without needing to solve any differential equation as it is done in the 0-D model, thus greatly accelerating the model's simulating speed in predicting in-cylinder pressure trace.

In this section, the cylinder pressure analytic model is firstly adapted to the marine two-stroke diesel engine with its basic idea shown in Figure 14; then, the model parameter calibration procedure is discussed in detail; finally, the model is coupled to the MVEM and its in-cylinder pressure trace predictive ability is evaluated by comparing with the measured indicator diagram.

![Figure 14: Basic idea of the cylinder pressure analytic model. The main plot shows Pressure [bar] on the y-axis (0 to 20) versus Crank Angle [deg] on the x-axis (-150 to 150). The cycle is divided into phases: Scavenging (approx. -150 to -100), Compression, Combustion, Expansion (approx. -100 to 50), and Blow-Down (approx. 50 to 150). The plot includes: Measured In-Cylinder Pressure (solid black line), Compression Polytropic Process (dashed red line), Expansion Polytropic Process (dashed blue line), Combustion Process (solid green line), Blow-Down Process (dashed magenta line), and Scavenging & Post-Exhaust Processes (dashed black line). Two insets show valve timing: the left inset shows Scavenging Ports Closing (SPC) and Exhaust Valve Closing (EVC) between -180 and -100 degrees; the right inset shows Scavenging Ports Opening (SPO) and Exhaust Valve Opening (EVO) between 130 and 180 degrees.](79cb7fa0e9c78ec5cd0b0de977824f8d_img.jpg)

Figure 14: Basic idea of the cylinder pressure analytic model. The main plot shows Pressure [bar] on the y-axis (0 to 20) versus Crank Angle [deg] on the x-axis (-150 to 150). The cycle is divided into phases: Scavenging (approx. -150 to -100), Compression, Combustion, Expansion (approx. -100 to 50), and Blow-Down (approx. 50 to 150). The plot includes: Measured In-Cylinder Pressure (solid black line), Compression Polytropic Process (dashed red line), Expansion Polytropic Process (dashed blue line), Combustion Process (solid green line), Blow-Down Process (dashed magenta line), and Scavenging & Post-Exhaust Processes (dashed black line). Two insets show valve timing: the left inset shows Scavenging Ports Closing (SPC) and Exhaust Valve Closing (EVC) between -180 and -100 degrees; the right inset shows Scavenging Ports Opening (SPO) and Exhaust Valve Opening (EVO) between 130 and 180 degrees.

**Figure 14.** Basic idea of the cylinder pressure analytic model (SPC: Scavenging ports closing; SPO: Scavenging ports opening; EVC: Exhaust valve closing; EVO: Exhaust valve opening).

## 4.1. Cylinder Pressure Analytic Model

### (1) Compression Phase (EVC to SOC)

The actual compression process can be approximated by a polytropic process with a polytropic index of  $n_{comp}$ . Based on this assumption, the instantaneous in-cylinder pressure  $p_{comp}$  and temperature  $T_{comp}$  during this phase can be calculated as:

$$p_{comp}(\theta) = p_{evc} \left( \frac{V_{evc}}{V(\theta)} \right)^{n_{comp}} \quad (27)$$

$$T_{comp}(\theta) = T_{evc} \left( \frac{V_{evc}}{V(\theta)} \right)^{n_{comp}-1} \quad (28)$$

where  $p_{evc}$ ,  $V_{evc}$  and  $T_{evc}$  are the pressure, volume and temperature at EVC, respectively, and the EVC is treated as the reference point of the compression polytropic process.

As there is no mass exchange between the cylinder and surrounding during this phase, the in-cylinder trapped mass  $m_{trap}$  can be calculated by using ideal gas state equation.

### (2) Expansion Phase (EOC to EVO)

The expansion phase is also treated as a polytropic process. The calculation method of instantaneous in-cylinder pressure  $p_{exp}$  and temperature  $T_{exp}$  during this phase is also as similar with the compression phase. The main difference lies in the determination of polytropic index and the pressure and temperature of the reference point.

The temperature at the reference point of expansion phase can be estimated by adding an additional temperature increment based on  $T_{comp}(0^\circ)$ :

$$\Delta T = \frac{m_{f,cycle} H_{LHV} \eta_{comb}}{c_v(T_{comp}(0^\circ), \phi_{trap})(m_{trap} + m_{f,cycle})} \quad (29)$$

$$T_{exp,ref} = T_{comp}(0^\circ) + \Delta T \quad (30)$$

The theoretical foundation of Equations (29) and (30) is the constant volume heating process in the ideal Otto cycle. Once  $T_{exp,ref}$  is determined,  $p_{exp,ref}$  can be calculated by using ideal gas state equation.

### (3) Combustion Phase

During the combustion phase, the in-cylinder instantaneous pressure  $p_{comb}$  can be calculated by interpolating between  $p_{comb}$  and  $p_{exp}$  with the Wiebe function  $f_{wiebe}$  selected as the interpolating function:

$$p_{comb} = (1 - f_{wiebe}) \cdot p_{comp} + f_{wiebe} \cdot p_{exp} \quad (31)$$

### (4) Blow-down Phase (EVO to SPO)

As can be observed from Figure 14, the instantaneous in-cylinder pressure  $p_{exh}$  during this phase presents linear variation trend roughly, which, thus, can be approximated by a straight line crossing the points of  $(\theta_{evo}, p_{evo})$  and  $(\theta_{spo}, p_{spo})$  as the following equation:

$$p_{exh} = p_{evo} + \frac{p_{spo} - p_{evo}}{\theta_{spo} - \theta_{evo}} (\theta - \theta_{evo}) \quad (32)$$

### (5) Scavenging and Post Exhaust Phase (SPO to EVC)

As can be observed from Figure 14, the instantaneous in-cylinder  $p_{scav\_pe}$  during this phase does not fluctuate significantly, which is always between the scavenging and exhaust manifold pressure. Consequently,  $p_{scav\_pe}$  can be approximated by a straight line with a constant pressure value.

## 4.2. Model Parameters Calibration

There are several model parameters in the cylinder pressure analytic model to be calibrated as following:

1. The compression and expansion polytropic index;
2. The pressure and temperature at the reference point of the compression polytropic process;
3. Wiebe function model parameters.

### 4.2.1. Calibration of Polytropic Index

The polytropic process can be expressed as  $pV^n = const$  and it can be transformed to  $\ln p + n \ln V = const$  by taking the logarithm of each side. Consequently, by setting  $\ln V$  and  $\ln p$  as the horizontal and vertical coordinate, respectively, a straight line can be obtained with the negative of its slope equal to the polytropic index [17]. Figure 15 presents the estimation result of  $n_{comp}$  and  $n_{exp}$  for a certain operating condition. As can be observed from this figure, strong linear relationship exists between  $\ln V$  and  $\ln p$  with  $R^2$  larger than 0.999 for both the compression and expansion phase, which verifies the rationality of the assumption that the actual compression and expansion process can be approximately by the polytropic process.

![Figure 15: A scatter plot showing the relationship between log(V) on the x-axis and log(p) on the y-axis. The x-axis ranges from -3.5 to 0, and the y-axis ranges from 0 to 5. Measured results are shown as open circles. Two linear fitting lines are plotted: a red line for the compression process and a blue line for the expansion process. The red line has the equation y = 1.393*x - 0.1906, R^2 = 0.9996, and n_c = 1.393. The blue line has the equation y = 1.298*x + 0.9359, R^2 = 0.9997, and n_e = 1.298.](9b5411fa2d169b66f6185fbf67b49766_img.jpg)

Figure 15: A scatter plot showing the relationship between log(V) on the x-axis and log(p) on the y-axis. The x-axis ranges from -3.5 to 0, and the y-axis ranges from 0 to 5. Measured results are shown as open circles. Two linear fitting lines are plotted: a red line for the compression process and a blue line for the expansion process. The red line has the equation y = 1.393\*x - 0.1906, R^2 = 0.9996, and n\_c = 1.393. The blue line has the equation y = 1.298\*x + 0.9359, R^2 = 0.9997, and n\_e = 1.298.

**Figure 15.** Relationship between  $\log(V)$  and  $\log(p)$  and linear fitting result for the compression and expansion process.

Figure 16 provides the compression and expansion polytropic index estimation results for 29 known engine operating points. These operating points are measured on-board a ship and cover a wide range of operating conditions, which are named as A1 to A29 in this paper. For  $n_{comp}$ , its maximum and minimum value is 1.416 and 1.391, respectively, with a standard deviation of 0.0058; for  $n_{exp}$ , its maximum and minimum value is 1.321 and 1.280, respectively, with a standard deviation of 0.0076. The results indicate that the polytropic index will not change significantly with the engine operating conditions. Actually, it was revealed by Brunt and Platts that the polytropic index was influenced by many factors including engine speed, working medium temperature, heat transfer, etc. [18]. However, due to lacking of experimental conditions especially for the marine large scale diesel engine investigated in this paper, it is difficult to derive correlations between the polytropic index and other engine performance parameters. Therefore, in this paper a 2-D look-up table is established to calculate the polytropic index with the engine speed and brake power as the input variables.

![Figure 16: A scatter plot showing the Polytrropic Index [n] on the y-axis versus Operating Point on the x-axis. The y-axis ranges from 1.28 to 1.42, and the x-axis ranges from 0 to 30. The plot shows two sets of data points: red circles for the Compression Polytropic Index and blue triangles for the Expansion Polytropic Index. Horizontal dashed lines represent the Maximum, Minimum, and Average values for both indices. The legend lists: Compression Polytropic Index (red circle), Expansion Polytropic Index (blue triangle), Maximum Compression Polytropic Index (red dashed line), Minimum Compression Polytropic Index (red dash-dot line), Maximum Expansion Polytropic Index (blue dashed line), Minimum Expansion Polytropic Index (blue dash-dot line), Average Compression Polytropic Index (red solid line), and Average Expansion Polytropic Index (blue solid line).](65f66758012e229247953202e8adf35d_img.jpg)

Figure 16: A scatter plot showing the Polytrropic Index [n] on the y-axis versus Operating Point on the x-axis. The y-axis ranges from 1.28 to 1.42, and the x-axis ranges from 0 to 30. The plot shows two sets of data points: red circles for the Compression Polytropic Index and blue triangles for the Expansion Polytropic Index. Horizontal dashed lines represent the Maximum, Minimum, and Average values for both indices. The legend lists: Compression Polytropic Index (red circle), Expansion Polytropic Index (blue triangle), Maximum Compression Polytropic Index (red dashed line), Minimum Compression Polytropic Index (red dash-dot line), Maximum Expansion Polytropic Index (blue dashed line), Minimum Expansion Polytropic Index (blue dash-dot line), Average Compression Polytropic Index (red solid line), and Average Expansion Polytropic Index (blue solid line).

**Figure 16.** Compression and expansion polytropic index results for the 29 known operating conditions.

### 4.2.2. Calibration of $p_{evc}$ and $T_{evc}$

In Figure 17, the measured value of  $p_s$  and  $p_{evc}$  for the 29 known engine operating points are presented and compared. It can be observed from this figure that  $p_s$  is always greater than  $p_{evc}$ . In order to evaluate the quantitative relationship between  $p_s$  and  $p_{evc}$ , they are set as the horizontal and vertical coordinate, respectively, as shown in Figure 18. It can be found from this figure that strong

linear relationship exists between them with a  $R^2$  greater than 0.99. Consequently,  $p_{evc}$  can be expressed as a linear function of  $p_{sm}$ , that is  $p_{evc} = 0.9749p_s - 0.1029$  in this paper.

![Figure 17: Comparison between scavenging manifold pressure and in-cylinder pressure at exhaust valve closing (EVC) based on measured data. The graph plots Pressure [bar] on the y-axis (1.2 to 3.2) against Operating Point on the x-axis (0 to 30). Two data series are shown: Scavenging Manifold Pressure (black line with circles) and In-cylinder Pressure at EVC (red dashed line with squares). The two series are very close, showing a fluctuating but generally increasing trend from approximately 1.4 bar to 2.8 bar.](45329c7d9aa2bd1290af5b2027f08d7e_img.jpg)

Figure 17: Comparison between scavenging manifold pressure and in-cylinder pressure at exhaust valve closing (EVC) based on measured data. The graph plots Pressure [bar] on the y-axis (1.2 to 3.2) against Operating Point on the x-axis (0 to 30). Two data series are shown: Scavenging Manifold Pressure (black line with circles) and In-cylinder Pressure at EVC (red dashed line with squares). The two series are very close, showing a fluctuating but generally increasing trend from approximately 1.4 bar to 2.8 bar.

**Figure 17.** Comparison between scavenging manifold pressure and in-cylinder pressure at exhaust valve closing (EVC) based on measured data.

![Figure 18: Fitting result between scavenging manifold pressure and in-cylinder pressure at EVC based on measured data. This is a scatter plot with a linear fit. The x-axis is Scavenging Manifold Pressure [bar] (1.5 to 3.0) and the y-axis is In-cylinder Pressure at EVC [bar] (1.2 to 3.2). Measured values are shown as black circles, and the fitting result is a solid black line. The equation for the fit is y = 0.9749x - 0.1029, with an R-squared value of 0.9915.](b6bd6d8ee5821226bc79251ca5937e07_img.jpg)

Figure 18: Fitting result between scavenging manifold pressure and in-cylinder pressure at EVC based on measured data. This is a scatter plot with a linear fit. The x-axis is Scavenging Manifold Pressure [bar] (1.5 to 3.0) and the y-axis is In-cylinder Pressure at EVC [bar] (1.2 to 3.2). Measured values are shown as black circles, and the fitting result is a solid black line. The equation for the fit is y = 0.9749x - 0.1029, with an R-squared value of 0.9915.

**Figure 18.** Fitting result between scavenging manifold pressure and in-cylinder pressure at EVC based on measured data.

To guarantee the continuity of the simulated in-cylinder pressure trace during the scavenging and post-exhaust phase and also to reduce the model complexity, it is assumed that the in-cylinder pressure during the scavenging and post-exhaust phase is equal to  $p_{evc}$ . Although it can be observed from Figure 14 that this assumption will make the predicted in-cylinder pressure during the two phases slightly lower than the measured pressure, this will not significantly influence the model's predictive accuracy because the pressure during the two phases is only about 0.5% of the in-cylinder maximum pressure. Based on this assumption, the slope and intercept of Equation (32) can be determined.

The research carried out by Tang et al [5] and Kharroubi and Söğüt [19] all indicated that relationship exists between the scavenging air temperature  $T_s$  and  $T_{evc}$ . As  $T_{evc}$  is not measured both during the engine shop trial and on-board the ship, a 0-D engine model is adopted to investigate the relationship between  $T_s$  and  $T_{evc}$  in this paper. In Figure 19, the simulated results of  $T_s$  and  $T_{evc}$  are set as the horizontal and vertical coordinate. It can be found from this figure that a second-order polynomial is sufficient to capture the changing trend of  $T_{evc}$  with  $T_s$  with a  $R^2$  of 0.9958, indicating satisfactory fitting results.

![Figure 19: A scatter plot showing the relationship between Scavenging Manifold Temperature [K] on the x-axis and Temperature at EVC [K] on the y-axis. The x-axis ranges from 305 to 315, and the y-axis ranges from 335 to 380. The plot includes 'Simulation Results by Zero-Dimensional Model' represented by open circles and 'Fitting Results' represented by a solid line. A quadratic regression equation is displayed: y = 0.3069*x^2 - 186.45*x + 28655, with an R^2 value of 0.9958. The data points and the fitted curve show a strong positive correlation.](5500ab73cf84ccc0055eecf28889b4db_img.jpg)

Figure 19: A scatter plot showing the relationship between Scavenging Manifold Temperature [K] on the x-axis and Temperature at EVC [K] on the y-axis. The x-axis ranges from 305 to 315, and the y-axis ranges from 335 to 380. The plot includes 'Simulation Results by Zero-Dimensional Model' represented by open circles and 'Fitting Results' represented by a solid line. A quadratic regression equation is displayed: y = 0.3069\*x^2 - 186.45\*x + 28655, with an R^2 value of 0.9958. The data points and the fitted curve show a strong positive correlation.

**Figure 19.** Fitting result between scavenging manifold temperature and in-cylinder temperature at EVC based on the 0-D model.

### 4.2.3. Calibration of Wiebe Function Model Parameters

In order to predict the in-cylinder pressure trace during the combustion phase, the Wiebe function is used to interpolate between the compression and expansion pressure. The general form of the single Wiebe function can be written as:

$$\chi = 1 - \exp\left[-a\left(\frac{\theta - \theta_{soc}}{\Delta\theta_{CD}}\right)^{m+1}\right] \quad (33)$$

where  $\chi$  is the mass fraction burned (MFB);  $\varphi_{soc}$  is the start of combustion crank angle;  $\Delta\varphi_{CD}$  is the combustion duration;  $a$  is the efficiency factor;  $m$  is the form factor.

#### Step 1: Derive the MFB based on the measured in-cylinder pressure trace

Several classical MFB estimation methods can be found in the literature, such as the Apparent Heat Release model, the Gatowski model, the RW model, as well as the pressure ratio management (PRM) model [20]. In this paper, the PRM model is adopted to derive the MFB:

$$PR(\theta) = \frac{p_z(\theta)}{p_m(\theta)} - 1 \quad (34)$$

$$\chi(\theta) = \frac{PR(\theta)}{PR_{max}(\theta)} \quad (35)$$

where  $PR$  is referred to as the pressure ratio;  $p_z$  is the measured in-cylinder pressure;  $p_m$  is the motored in-cylinder pressure;  $PR_{max}$  is the maximum value of  $PR$ , which is used to normalize  $PR$  to obtain the MFB.

In this paper, the motored in-cylinder pressure  $p_m$  is estimated by assuming the motored process as a polytropic process as it was done by many researchers [21–23]. In addition, it is assumed that the expansion polytropic index is equal to that of the compression process, the value of which can be estimated by following the calibration procedure as described in Section 4.2.1. Consequently,  $p_m$  can be determined by using the following equation:

$$p_m(\theta) = p_{ref} \left( \frac{V_{ref}}{V(\theta)} \right)^{n_m} \quad (36)$$

where  $p_{ref}$  and  $V_{ref}$  are the pressure and volume at the reference point, which can be an arbitrary crank angle position between the EVC and SOC.

#### **Step 2: Determine the number of single Wiebe function needed to be superposed**

Ghojel pointed out that the form factor  $m$  in Wiebe function can reflect the distribution of combustion process, thus, the variation of  $m$  can be exploited to determine the number of single Wiebe function to be superposed [24]. Following this idea, the original single Wiebe function as shown in Equation (33) can be transformed to the following form by appropriate mathematical manipulation:

$$\ln[\ln(1 - \chi) / \ln 0.5] = (m + 1) \ln(\theta - \theta_{soc}) - (m + 1) \ln(\theta_{50} - \theta_{soc}) \quad (37)$$

where  $\theta_{50}$  is the crank angle corresponding to 50% MFB.

Set the  $\ln(\theta - \theta_{soc})$  and  $\ln[\ln(1 - \chi) / \ln 0.5]$  as the horizontal and vertical coordinate, respectively. If a straight line is obtained, a single Wiebe function is sufficient to simulate the combustion process accurately, otherwise, two or more single Wiebe functions are needed, the number of which can be estimated by the number of broken lines in the plane of  $\ln(\theta - \theta_{soc}) \sim \ln[\ln(1 - \chi) / \ln 0.5]$ . For the 7S80ME-C9.2 marine engine, it is found that superposing two single Wiebe functions is sufficient in the whole engine operating envelope.

#### **Step 3: Estimate the Wiebe function model parameters by using LSM**

As mentioned in Step 2, double Wiebe function is sufficient to simulate the actual combustion process, which can be written as:

$$\chi = (1 - \beta) \left\{ 1 - \exp \left[ -a_p \left( \frac{\theta - \theta_{soc,p}}{\Delta\theta_{CD,p}} \right)^{m_p+1} \right] \right\} + \beta \left\{ 1 - \exp \left[ -a_d \left( \frac{\theta - \theta_{soc,d}}{\Delta\theta_{CD,d}} \right)^{m_d+1} \right] \right\} \quad (38)$$

where subscript  $p$  and  $d$  represents premixed and diffusive combustion, respectively;  $\beta$  is the fraction of fuel burned during the diffusive combustion phase.

There are totally 9 model parameters in the double Wiebe function as shown in equation (38), making the model calibration process relatively laborious. Therefore, to reduce the number of Wiebe function model parameters to be calibrated, two assumptions are made herein:

(1) The premixed combustion duration is assumed to be equal to that of diffusive combustion. In addition, the crank angle range between 1% and 99% MFB is defined as the combustion duration by taking into account that the Signal to Noise Ratio (SNR) is relatively lower and the combustion is unstable at the start and end of the combustion;

(2) The crank angle at the start of premixed combustion is also assumed to be equal to that of diffusive combustion.

Based on the two assumptions, the number of Wiebe function model parameters to be calibrated reduces from 9 to 7; in addition,  $\Delta\theta_{CD}$  and  $\theta_{SOC}$  can be estimated from the MFB curve beforehand. As a result, only 5 Wiebe function model parameters remain to be estimated.

Table 4 presents the calibration results of the Wiebe function model parameters for four operating points as well as the relevant predictive errors in MFB. As can be observed from this table,  $PE$  is less than 1.07 %, whereas  $MAE$  is less than 0.31 %, indicating the sufficient accuracy of double Wiebe function in simulating the actual combustion process in CI engines as well as the satisfactory calibration results.

To obtain an overall accurate Wiebe function, a 2-D look-up table is established for the Wiebe function model parameters with the engine speed and brake power as the inputs. In addition, it is found that the combustion duration can be well approximated by a linear function of the fuel injection rate.

**Table 4.** Wiebe parameters and predictive error.

| Operating Point      | A2     | A8     | A14    | A25    |
|----------------------|--------|--------|--------|--------|
| $a_p$                | 3.415  | 3.769  | 3.45   | 3.319  |
| $a_d$                | 23.8   | 23.72  | 17.28  | 12.71  |
| $m_p$                | 1.148  | 1.292  | 1.578  | 2.2    |
| $m_d$                | 1.006  | 0.9729 | 0.9035 | 0.7247 |
| $\beta$              | 0.6749 | 0.6481 | 0.6992 | 0.8023 |
| PE (%) <sup>1</sup>  | 1.07   | 0.81   | 0.95   | 0.78   |
| MAE (%) <sup>2</sup> | 0.31   | 0.27   | 0.19   | 0.25   |

<sup>1</sup> PE: Peak Error; <sup>2</sup> MAE: Mean Absolute Error.

## 4.3. Results

In this section, the in-cylinder pressure trace simulated by the analytic model under four different operating conditions are compared with the measured ones to validate its correctness as shown in Figure 20. It can be observed from this figure that the simulation results agree well with the measured results and can capture the variation trend of in-cylinder pressure trace with crank angle during each working phase. During the gas exchange phase (blow-down, scavenging and post-exhaust), the relative errors of the simulation results are relatively higher than the other phases, which is mainly caused by the simplifications and assumptions made for these phases, i.e., two simple linear functions are adopted to approximate the in-cylinder pressure trace; however, it should be noted that the absolute errors during the gas exchange phase are less than 0.15 bar, which is still satisfactory with respect to the variation range of in-cylinder pressure during the whole working cycle. During the combustion phase, the relative errors of most of the simulation results are less than 5%, which is mainly benefiting from the effective calibration of Wiebe function model parameters as introduced in Section 4.2.3. It should be noted that by superposing more single Wiebe functions, the simulation accuracy during the combustion phase will improve, but this will make the Wiebe function model parameters calibration process laborious. Actually, the current simulation accuracy is already satisfactory to some extent. At the start of compression phase, the relative errors of part of the simulation results approach 20%, which is maybe attributed to two reasons: (1) the absolute value of in-cylinder pressure is relatively lower and small absolute errors will lead to obvious relative errors; (2) the actual compression process is approximated by a polytropic process. Note that as part of the input variables of the analytic model are from the MVEM, thus the predictive errors of MVEM will transform to the analytic model and lead to predictive errors.

![Figure 20. Cont. shows two plots for operating point A1. The left plot displays the In-cylinder Pressure [bar] versus Crank Angle [deg], comparing Measured Value (red crosses) and Predicted Value (black line). The pressure peaks at approximately 82 bar at 0 degrees crank angle. The right plot shows the Relative Error [%] versus Crank Angle [deg], with the same Measured Value (red crosses) and Predicted Value (black line). The error is highest during the Gas-Exchange phases, reaching up to 20% relative error, and is lowest during the Combustion phase, staying below 5%.](27b3968bf5ede712f8defd1a7ed30a7a_img.jpg)

Figure 20. Cont. shows two plots for operating point A1. The left plot displays the In-cylinder Pressure [bar] versus Crank Angle [deg], comparing Measured Value (red crosses) and Predicted Value (black line). The pressure peaks at approximately 82 bar at 0 degrees crank angle. The right plot shows the Relative Error [%] versus Crank Angle [deg], with the same Measured Value (red crosses) and Predicted Value (black line). The error is highest during the Gas-Exchange phases, reaching up to 20% relative error, and is lowest during the Combustion phase, staying below 5%.

**Figure 20. Cont.**

![Figure 20: Prediction result and error distribution of the cylinder pressure analytic model. (a) Predictive results showing In-Cylinder Pressure [bar] vs Crank Angle [deg] for cases A3, A14, and A25. (b) Error distribution showing Relative Error [%] vs Crank Angle [deg] for the same cases, with vertical lines indicating Gas-Exchange, Compression, Combustion, and Expansion phases.](abc0eb594f9d2c0daa0e60df05f2a666_img.jpg)

Figure 20 consists of six subplots arranged in a 3x2 grid. The left column (a) shows the predictive results, and the right column (b) shows the error distribution.

**Subplots (a): Predictive Results**

- A3:** In-Cylinder Pressure [bar] vs Crank Angle [deg]. The pressure peaks at approximately 105 bar at 0 degrees crank angle. The x-axis ranges from -150 to 150 degrees, and the y-axis ranges from 0 to 120 bar.
- A14:** In-Cylinder Pressure [bar] vs Crank Angle [deg]. The pressure peaks at approximately 115 bar at 0 degrees crank angle. The x-axis ranges from -150 to 150 degrees, and the y-axis ranges from 0 to 120 bar.
- A25:** In-Cylinder Pressure [bar] vs Crank Angle [deg]. The pressure peaks at approximately 125 bar at 0 degrees crank angle. The x-axis ranges from -150 to 150 degrees, and the y-axis ranges from 0 to 140 bar.

**Subplots (b): Error Distribution**

- A3:** Relative Error [%] vs Crank Angle [deg]. The error is generally low, around 0%, with some fluctuations between -10% and 10% during the Gas-Exchange and Expansion phases. Vertical lines at approximately -100, 0, and 100 degrees mark the boundaries of Gas-Exchange, Compression, Combustion, and Expansion.
- A14:** Relative Error [%] vs Crank Angle [deg]. The error is generally low, around 0%, with some fluctuations between -10% and 10% during the Gas-Exchange and Expansion phases. Vertical lines at approximately -100, 0, and 100 degrees mark the boundaries of Gas-Exchange, Compression, Combustion, and Expansion.
- A25:** Relative Error (%) vs Crank Angle [deg]. The error is generally low, around 0%, with some fluctuations between -10% and 10% during the Gas-Exchange and Expansion phases. Vertical lines at approximately -100, 0, and 100 degrees mark the boundaries of Gas-Exchange, Compression, Combustion, and Expansion.

Legend for (a): + Measured Value, — Predicted Value.

Figure 20: Prediction result and error distribution of the cylinder pressure analytic model. (a) Predictive results showing In-Cylinder Pressure [bar] vs Crank Angle [deg] for cases A3, A14, and A25. (b) Error distribution showing Relative Error [%] vs Crank Angle [deg] for the same cases, with vertical lines indicating Gas-Exchange, Compression, Combustion, and Expansion phases.

**Figure 20.** Prediction result and error distribution of the cylinder pressure analytic model: (a) predictive results; (b) error distribution.

For practical engineering practice, the marine engineers normally judge the engine's operation status by checking the compression pressure  $p_{comp}$ , maximum pressure  $p_{max}$  and its crank angle position  $\theta_{p,max}$ . Table 5 compares the predicted and measured results of  $p_{comp}$ ,  $p_{max}$  and  $\theta_{p,max}$ . As can be observed from this table, the cylinder pressure analytic model is capable of predicting  $p_{comp}$  and  $p_{max}$  satisfactorily with relative errors less than 1%. Although the relative errors of  $\theta_{p,max}$  are relatively higher, the absolute errors are generally less than one crank angle, indicating that the predictive accuracy can be accepted to some extent.

**Table 5.** Prediction error of the cylinder pressure analytic model.

|     |                            | <i>p</i> <sub>comp</sub> (bar) | <i>p</i> <sub>max</sub> (bar) | $\theta_{p_{max}}$ (deg) |
|-----|----------------------------|--------------------------------|-------------------------------|--------------------------|
| A1  | <i>PD</i> <sup>1</sup>     | 62.1                           | 81.6                          | 9.0                      |
|     | <i>MD</i> <sup>2</sup>     | 62.2                           | 82.3                          | 9.5                      |
|     | <i>RD</i> (%) <sup>3</sup> | −0.16                          | −0.85                         | −5.26                    |
| A3  | <i>PD</i>                  | 73.9                           | 102.2                         | 9.0                      |
|     | <i>MD</i>                  | 73.8                           | 102.7                         | 8.6                      |
|     | <i>RD</i> (%)              | 0.14                           | −0.49                         | 4.65                     |
| A14 | <i>PD</i>                  | 89.5                           | 114.5                         | 11.1                     |
|     | <i>MD</i>                  | 89.7                           | 114.1                         | 10.3                     |
|     | <i>RD</i> (%)              | −0.22                          | 0.35                          | 7.77                     |
| A25 | <i>PD</i>                  | 100.3                          | 125.8                         | 10.8                     |
|     | <i>MD</i>                  | 101.3                          | 126.2                         | 9.7                      |
|     | <i>RD</i> (%)              | −0.99                          | −0.32                         | 11.34                    |

<sup>1</sup> Predicted value; <sup>2</sup> Measured value; <sup>3</sup> Relative error.

The inputs of the analytic model, such as scavenging air pressure and temperature and engine speed, are completely from the MVEM and the calculation process does not influence the MVEM; however, it should be noted that the MVEM and the cylinder pressure analytic model have different simulation speed, which must be handled when they are coupled together and applied in the engine room simulator. Aiming at this problem, two threads are adopted to depart the analytic model from the MVEM as shown in Figure 21. At steady state conditions, the simulation results of the MVEM are the same in every engine cycle, meaning that the engine performance parameters transformed to the analytic model also remain unchanged, therefore, the in-cylinder pressure trace simulated by the analytic model will also be the same in every engine cycle; on the other hand, the in-cylinder pressure trace is not required to be updated in real-time in the engine room simulator, and the “Pressure-Crank Angle” diagram or the “Pressure-Volume” diagram need to be displayed only when the user switches to the corresponding simulation interfaces. Based on the two factors, at steady state conditions, the in-cylinder pressure trace only needs to be calculated for one engine cycle by the analytic model, therefore, the running speed of the whole model can be as fast as the MVEM.

![Figure 21: Synchronization approach for the MVEM and the cylinder pressure analytic model. The diagram shows three scenarios: (a) X = 0, where the analytic model runs once per cycle; (b) X = 1, where the analytic model runs once per cycle but the MVEM runs faster; (c) the calculation frequency of the MVEM is many times the analytic model, where the MVEM runs much faster than the analytic model.](f0a97d0d3818a253c1d2a009966081b1_img.jpg)

The diagram illustrates three synchronization approaches between the MVEM (Main thread) and the Cylinder Pressure Analytic Model (Slave thread).  
 (a) X = 0: The MVEM and the analytic model run at the same frequency. The analytic model calculates once per cycle, and the MVEM waits for the analytic model to complete before starting its next cycle.  
 (b) X = 1: The MVEM runs faster than the analytic model. The analytic model calculates once per cycle, but the MVEM starts its next cycle before the analytic model completes its current one.  
 (c) The calculation frequency of the MVEM is many times the analytic model: The MVEM runs much faster than the analytic model. The analytic model calculates once per cycle, but the MVEM starts many cycles before the analytic model completes its current one.

Figure 21: Synchronization approach for the MVEM and the cylinder pressure analytic model. The diagram shows three scenarios: (a) X = 0, where the analytic model runs once per cycle; (b) X = 1, where the analytic model runs once per cycle but the MVEM runs faster; (c) the calculation frequency of the MVEM is many times the analytic model, where the MVEM runs much faster than the analytic model.

**Figure 21.** Synchronization approach for the MVEM and the cylinder pressure analytic model: (a)  $X = 0$ ; (b)  $X = 1$ ; (c) the calculation frequency of the MVEM is many times the analytic model.

During the transient process, the engine performance parameters and the in-cylinder pressure trace are different in every engine cycle; on the other hand, the MVEM and the cylinder pressure analytic model have different simulation speed. Therefore, in order to keep the simulation results in sync, the MVEM has to wait for some time before analytic model completes the calculation of an engine cycle as shown in Figure 21a, as a result, the simulation speed of the whole engine model is

determined by the cylinder pressure analytic model, which is actually slower than the MVEM. To accelerate the simulation speed of the whole model, the idea of abandoning engine cycles is adopted. Figure 21b presents the case where the calculation frequency of the MVEM is two times the analytic model, meaning that the MVEM has already completed the calculation of two engine cycles when the analytic model only completes the calculation of one engine cycle. Figure 21c presents the case where the calculation frequency of the MVEM is many times the analytic model. By adopting this method, we can keep the MVEM and the cylinder pressure analytic model in sync, furthermore, the simulation speed of the whole model will get faster if more engine cycles are abandoned by the analytic model. The relationship between the number of abandoned cycles  $X$  and the reduced time  $Y$  can be expressed as  $Y=X/(X+1)$ . It should be noted that the synchronization mentioned above is a fake synchronization during the transient process and this is because that the current simulated in-cylinder pressure trace simulated by the analytic model does not correspond to the current engine operating conditions outputted by the MVEM but falls behind to some extent.

To assess the improvement in simulation speed of the extended MVEM developed in this paper, it is compared with the merged model developed by Tang et al., where the 0-D model was adopted to calculate the in-cylinder pressure and the MVEM was used to simulate other engine performance parameters with the similar synchronization approach as shown in Figure 21 [5]. The comparison of actual execution time for a 100 s simulation time is presented in Table 6.

**Table 6.** Comparison of simulation speed.

| Model           | Abandoned Cycles | Execution Time (s) | Simulation Time (s) |
|-----------------|------------------|--------------------|---------------------|
| Tang et al. [5] | 49               | 1.002              | 100                 |
| This paper      | 4                | 0.946              | 100                 |

As can be found from Table 6, the engine model developed in this paper is able to achieve similar actual execution time of about one second but only four cycles are abandoned, whereas it is 49 for the merged model developed by Tang et al. [5]. This is due to the fact that the cylinder pressure analytic model runs much faster than the 0-D model and therefore similar actual execution time can be obtained by abandoning less number of engine cycles. As a result, the model developed in this paper can capture the transient response of the in-cylinder pressure trace more accurately.

# 5. Conclusions

In this article, a marine two stroke diesel engine MVEM with in-cylinder pressure trace predictive capability and a novel compressor model was developed.

A previous study carried out by the first author indicated that none of the compressor empirical mass flow rate models existing in the literature appears to achieve satisfactory predictive accuracy in the whole operating area. To solve this problem, the compressor whole operating area was divided into design, LS, HS and LPR operating areas by defining zonal division standard with appropriate functions, and then the compressor mass flow rate model that achieved the best predictive accuracy was selected for each operating area. In addition, an appropriate blending function was applied when the operating point enters into the LRP area from other areas to avoid the possible discontinuity.

The zonal compressor isentropic efficiency model proposed in this paper was based on the Hadef model. By dividing the whole “Mass flow rate—actual specific enthalpy change” plane into several zones by using the iso-speed curves available in the performance map, the working characteristics of compressor within different speed range can be captured much more accurately. It was revealed from the simulation results that with respect to the original Hadef model, the predictive accuracy of the zonal isentropic efficiency model was effectively improved. In addition, satisfactory extrapolation accuracy was obtained with this zonal compressor isentropic efficiency model.




As can be found from the trajectory of the compressor operating points during the transient process, the compressor model proposed in this paper is able to extrapolate to the LS and HS off-design operating areas reasonably and robustly; in addition, by comparing with the measured data provided in the engine shop trial report, the predictive accuracy of the engine performance parameters relevant to the turbocharger were all satisfactory at each steady state loading condition. Based on these simulation results, the fidelity of the proposed compressor model was validated. Due to the significant influence of the compressor on the engine steady state performance and transient response, the compressor model proposed in this paper is very helpful for improving the MVEM's predictive accuracy in the whole engine operating envelope.

By adapting the cylinder pressure analytic model to the 7S80ME-C9.2 marine two-stroke diesel engine, the MVEM is able to predict the in-cylinder pressure trace without impairing its merit in running speed. For achieving satisfactory predictive accuracy, the model parameters of the analytic model were finely calibrated by using the measured data and a 0-D engine model. At steady state condition, the extended MVEM runs as fast as the MVEM. During the transient process, the extended MVEM is able to achieve the running speed as similar as the MG model (0D + MVEM) proposed by Tang et al. [5] but captures the transient response of the in-cylinder pressure trace more accurately.

Although some sub-models of the MVEM are needed to be re-calibrated if another engine is to be modeled, they can be calibrated readily by only using the engine shop trial report and relevant performance maps. As a result of the lack of engine measured data, 2-D look-up tables were developed to calculate Wiebe function model parameters as well as the compression and expansion polytropic index. Although rapid calculation speed and satisfactory interpolation accuracy can be achieved with the 2-D look-up table, its extrapolative ability is big issue. In the future study, more measured engine data will be gathered to develop correlations between the model parameters and the engine performance parameters to enhance their extrapolative ability.

**Author Contributions:** H.S. contributed to the development of mathematical models, analysis of simulation results and the writing of the manuscript. J.Z. provided research conditions, team support and financial support. B.Y. and B.J. gave some useful suggestions. All authors have read and agreed to the published version of the manuscript.

**Funding:** This work was supported by the National Natural Science Foundation of China, grant number 51479017, and the Fundamental Research Funds for the Central Universities, grant number 3132019315.

**Acknowledgments:** The authors are especially grateful to Tang, who provided important technical support.

**Conflicts of Interest:** The authors declare no conflict of interest.

# Nomenclature

|           |                                                          |                |                                         |
|-----------|----------------------------------------------------------|----------------|-----------------------------------------|
| $a$       | Wiebe function efficiency factor (–)/model parameter (–) | $n$            | polytropic index (–)/number (–)         |
| $b$       | model parameter (–)                                      | $N$            | rotational speed (RPM)                  |
| $A$       | area ( $m^2$ )                                           | $p$            | pressure (pa)                           |
| $C$       | flow coefficient (–)                                     | $P$            | power (W)                               |
| $c_p$     | constant pressure specific heat (J/kg K)                 | $\bar{p}$      | mean effective pressure (pa)            |
| $c_v$     | constant volume specific heat (J/kg K)                   | $Q$            | torque (N m)                            |
| $h$       | specific heat (J/kg)                                     | $\dot{Q}_{ht}$ | heat transfer rate (W)                  |
| $H_{LHV}$ | fuel lower heating value (J/kg)                          | $R$            | gas constant (J/kg K)                   |
| $J$       | moment of inertia ( $kg m^2$ )                           | $T$            | temperature (K)                         |
| $K_p$     | propeller torque coefficient (–)                         | $V_d$          | cylinder displacement volume ( $m^3$ )  |
| $k$       | model parameter (–)                                      | $\dot{V}$      | volume flow rate ( $m^3/s$ )            |
| $\dot{m}$ | mass flow rate (kg/s)                                    | $V$            | cylinder instantaneous volume ( $m^3$ ) |
| $m$       | Wiebe function form factor (–)/mass (kg)                 |                |                                         |

## Greek symbols

|          |                                                        |          |                               |
|----------|--------------------------------------------------------|----------|-------------------------------|
| $\gamma$ | specific heat ratio (–)                                | $\Gamma$ | expansion ratio (–)           |
| $\theta$ | crank angle (deg)                                      | $\omega$ | angular velocity (rad/s)      |
| $\zeta$  | fuel chemical energy proportion in the exhaust gas (–) | $\phi$   | fuel air equivalent ratio (–) |
| $\eta$   | efficiency (–)                                         | $\chi$   | mass fraction burned (–)      |
| $\Pi$    | pressure ratio (–)                                     |          |                               |

## Subscripts

|      |                                     |      |                     |
|------|-------------------------------------|------|---------------------|
| a    | air                                 | i    | indicated           |
| ac   | air cooler                          | in   | inlet               |
| af   | air filter                          | is   | isentropic          |
| amb  | ambient                             | lb   | lower bound         |
| act  | actual                              | m    | motored             |
| b    | brake                               | out  | outlet              |
| bl   | blower                              | p    | propeller/premixed  |
| c    | compressor                          | pe   | post exhaust        |
| cw   | cooling water                       | ref  | reference           |
| comp | compression                         | s    | scavenging manifold |
| comb | combustion                          | sur  | surging             |
| CD   | combustion duration                 | sh   | shaft               |
| d    | diffusive                           | scav | scavenging          |
| e    | exhaust manifold/engine/exhaust gas | soc  | start of combustion |
| ell  | ellipse                             | t    | turbine             |
| exp  | expansion                           | tc   | turbocharger        |
| exh  | exhaust                             | z    | cylinder            |
| f    | fuel/fricative                      |      |                     |

# References

1. Theotokatos, G.; Guan, C.; Chen, H.; Lazakis, I. Development of an extended mean value engine model for predicting the marine two-stroke engine operation at varying settings. *Energy* **2018**, *143*, 533–545. [\[CrossRef\]](#)
2. Mavrellos, C.; Theotokatos, G. Numerical investigation of a premixed combustion large marine two-stroke dual fuel engine for optimising engine settings via parametric runs. *Energy Convers. Manag.* **2018**, *160*, 48–59. [\[CrossRef\]](#)
3. Stoumpos, S.; Theotokatos, G.; Boulougouris, E.; Vassalos, D.; Lazakis, I.; Livanos, G. Marine dual fuel engine modelling and parametric investigation of engine settings effect on performance-emissions trade-offs. *Ocean Eng.* **2018**, *157*, 376–386. [\[CrossRef\]](#)
4. Eriksson, L.; Nielsen, L. *Modeling and Control of Engines and Drivelines*; John Wiley and Sons Ltd.: Hoboken, NJ, USA, 2014.
5. Tang, Y.Y.; Zhang, J.D.; Gan, H.B.; Jia, B.Z.; Xia, Y. Development of a real-time two-stroke diesel engine model with in-cylinder pressure prediction capability. *Appl. Energy* **2017**, *194*, 55–70. [\[CrossRef\]](#)
6. Altosole, M.; Campora, U.; Figari, M.; Laviola, M.; Martelli, M. A diesel engine modelling approach for ship propulsion real-time simulators. *J. Mar. Sci. Eng.* **2019**, *7*, 138. [\[CrossRef\]](#)
7. Nikzadfar, K.; Shamekhi, A.H. An extended mean value model (EMVM) for control-oriented modeling of diesel engines transient performance and emissions. *Fuel* **2015**, *154*, 275–292. [\[CrossRef\]](#)
8. Theotokatos, G. On the cycle mean value modelling of a large two-stroke marine diesel engine. *Proc. Inst. Mech. Eng. Part M J. Eng. Marit. Environ.* **2010**, *224*, 193–205. [\[CrossRef\]](#)
9. Baldi, F.; Theotokatos, G.; Andersson, K. Development of a combined mean value-zero dimensional model and application for a large marine four-stroke diesel engine simulation. *Appl. Energy* **2015**, *154*, 402–415. [\[CrossRef\]](#)
10. Eriksson, L.; Andersson, I. An analytic model for cylinder pressure in a four stroke SI engine. In Proceedings of the SAE 2002 World Congress, Detroit, MI, USA, 4–7 March 2002.
11. Shen, H.S.; Zhang, J.D.; Yang, B.C.; Jia, B.Z. Development of an educational virtual reality training system for marine engineers. *Comput. Appl. Eng. Educ.* **2019**, *27*, 580–602. [\[CrossRef\]](#)

12. Theotokatos, G.; Tzelepis, V. A computational study on the performance and emission parameters mapping of a ship propulsion system. *J. Eng. Marit. Environ.* **2015**, *229*, 58–76. [\[CrossRef\]](#)
13. Tu, H. Investigation on the Performance Optimization Method for Large Containership Propulsion Engine at Slow Steaming Conditions. Ph.D. Thesis, Wuhan University of Technology, Wuhan, China, 2015.
14. Llamas, X.; Eriksson, L. Parameterizing compact and extensible compressor models using orthogonal distance minimization. *J. Eng. Gas Turbines Power* **2017**, *139*, 012601. [\[CrossRef\]](#)
15. Shen, H.S.; Zhang, C.; Zhang, J.D.; Yang, B.C.; Jia, B.Z. Applicable and comparative research of compressor mass flow rate and isentropic efficiency empirical models to marine large-scale compressor. *Energies* **2020**, *13*, 47. [\[CrossRef\]](#)
16. Hadef, J.E.; Colin, G.; Chamaillard, Y.; Talon, V. Physical-based algorithms for extrapolation and interpolation of turbocharger data maps. *SAE Int. J. Engines* **2012**, *5*, 363–378. [\[CrossRef\]](#)
17. Baratta, M.; Misul, D. Development and assessment of a new methodology for end of combustion detection and its application to cycle resolved heat release analysis in IC engines. *Appl. Energy* **2012**, *98*, 174–189. [\[CrossRef\]](#)
18. Brunt, M.F.; Platts, K.C. Calculation of heat release in direct injection diesel engines. In Proceedings of the SAE 1999 International Congress and Exposition, Detroit, MI, USA, 1–4 March 1999.
19. Kharroubi, K.; Söğüt, O.S. Modelling of the propulsion plant of a large container ship by the partition of the cycle the main diesel engine. *J. Eng. Marit. Environ.* **2019**. [\[CrossRef\]](#)
20. Eriksson, L.; Thomasson, A. Cylinder state estimation from measured cylinder pressure traces—A survey. *IFAC PapersOnLine* **2017**, *50*, 11029–11039. [\[CrossRef\]](#)
21. Oh, S.; Min, K.; Sunwoo, M. Real-time start of a combustion detection algorithm using initial heat release for direct injection diesel engines. *Appl. Therm. Eng.* **2015**, *89*, 332–345. [\[CrossRef\]](#)
22. Choe, D.; Lee, M.; Lee, K.; Sunwoo, M.; Jin, K.K.; Chang, K.; Shin, K. SOC detection of controlled auto-ignition engine. In Proceedings of the 14th Asia Pacific Automotive Engineering Conference, Hollywood, CA, USA, 5–8 August 2007.
23. Zhu, G.; Daniels, C.F.; Winkelmann, J. MBT timing detection and its closed-loop control using in-cylinder pressure signal. In Proceedings of the 2003 Powertrain and Fluid Systems Conference and Exhibition, Pittsburgh, PA, USA, 27–30 October 2003.
24. Ghojel, J.I. Review of the development and applications of the Wiebe function: A tribute to the contribution of Ivan Wiebe to engine research. *Int. J. Engine Res.* **2010**, *11*, 297–312. [\[CrossRef\]](#)

![Creative Commons Attribution (CC BY) license logo](a1fad9ca0c696e710c9a7ae5622401e4_img.jpg)

The image shows the Creative Commons Attribution (CC BY) logo, which consists of two circular icons: one with 'cc' and another with a person symbol, followed by the text 'BY'.

Creative Commons Attribution (CC BY) license logo