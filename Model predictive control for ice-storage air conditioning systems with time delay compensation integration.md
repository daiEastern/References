

![Elsevier tree logo](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier tree logo

![Energy journal cover](390120de4fe440c42fea8154fcaad334_img.jpg)

Energy journal cover

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Model predictive control for ice-storage air conditioning systems with time delay compensation integration

Yan Ding<sup>a,b,\*</sup>, Long Hu<sup>a</sup>, Qiaochu Wang<sup>a</sup>, Yang Bai<sup>a</sup>, Zhe Tian<sup>a,b,10</sup>, Caixia Yang<sup>c</sup>

<sup>a</sup> School of Environmental Science and Engineering, Tianjin University, Tianjin, 300072, China

<sup>b</sup> Tianjin Key Laboratory of Built Environment and Energy Application, Tianjin University, Tianjin, 300072, China

<sup>c</sup> China Academy of Building Research Tianjin Institute, Tianjin, 300384, China

## ARTICLE INFO

### Keywords:

Ice storage tank  
Heat transfer modeling  
Time delay  
Model predictive control  
Dual-objective optimization  
Building demand response

## ABSTRACT

Under the optimized control of building demand response, the ice storage air conditioning system can mitigate peak electrical grid pressure and intermittent renewable energy integration issues. However, due to the complex phase-change characteristics of the ice melting and cooling process, such as nonlinearity and significant inertia, current heat transfer and control models fail to optimize the dynamic response performance of the equipment considering these time-delay properties. In this study, an enthalpy-based model is employed to piecewise linearize the nonlinear phase-change process of the ice storage tank. By utilizing the state-space approach to transform the differential equations into transfer function-based dynamic heat transfer equations, the dynamic delay times for the ice storage system are characterized from inertia and flow delay times. Thereby, a time-delay compensation module is embedded into the Model Predictive Control (MPC). Then a dual-objective operational control strategy considering both cost-effectiveness and dynamic response performance is proposed. The results show that, compared to traditional Proportional-Integral-Derivative (PID) controllers, the MPC strategy respectively reduces the response time during the initial, middle, and final phases of ice melting by 43.3 %, 47.1 %, and 50.5 % and contributes to a reduction of peak electrical load and operating costs by 6.5 % and 8.5 %.

æ

(continued)

| Abbreviation |                                                    | $T_{ci}$      | cooling water return temperature, °C                             |
|--------------|----------------------------------------------------|---------------|------------------------------------------------------------------|
| MPC          | Model Predictive Control                           | $T_{ei}$      | refrigerant inlet temperature, °C                                |
| PID          | Proportional-Integral-Derivative Control           | $T_m$         | phase transition temperature, °C                                 |
| HVAC         | Heating Ventilation and Air Conditioning           | $T_{hf,i}$    | inlet temperature of the i-th unit cell of the ice storage, °C   |
| LSTM         | Long Short-Term Memory                             | $T_{hf,i+1}$  | inlet temperature of the i+1-th unit cell of the ice storage, °C |
| CV-RMSE      | Coefficient of Variation of Root Mean Square Error | $T_{ws}$      | chilled water supply temperature, °C                             |
| NMBE         | Normalized Mean Bias Error                         | $U$           | overall heat transfer coefficient, W/m <sup>2</sup> ·K           |
| PSO          | Particle Swarm Optimization Algorithm              | $V_{pcm}$     | volume of phase change material, m <sup>3</sup>                  |
| Symbols      |                                                    | Greek symbols |                                                                  |

|              |                                                                         |                 |                                                         |
|--------------|-------------------------------------------------------------------------|-----------------|---------------------------------------------------------|
| $A_t$        | the inner surface area of the coil tube, m <sup>2</sup>                 | $\rho_{hf}$     | refrigerant density, kg/m <sup>3</sup>                  |
| $A_p$        | cross-sectional area of the coil tube, m <sup>2</sup>                   | $\rho_{pcm}$    | phase change material density, kg/m <sup>3</sup>        |
| $c_i$        | electricity tariff                                                      | $\lambda_{pcm}$ | thermal conductivity of phase change materials, W/(m·K) |
| $E$          | operational electricity consumption                                     | $\tau_{c,hf}$   | inertial time delay of refrigerants, s                  |
| $G_{hf}$     | refrigerant flow rate, kg/s                                             | $\tau_{c,pcm}$  | inertial time delay of phase change material, s         |
| $H$          | enthalpy, kJ/kg                                                         | $\tau_p$        | pure time delay, s                                      |
| $H_i$        | enthalpy value of the i-th unit cell within the ice storage tank, kJ/kg | Subscripts      |                                                         |
| $\Delta H_m$ | specific latent heat of phase transition, kJ/kg                         | ch              | related to chiller                                      |
| $J$          | objective function                                                      | in              | related to inlet parameter                              |

(continued on next page)

(continued on next column)

\* Corresponding author. School of Environmental Science and Engineering, Tianjin University, Tianjin, 300072, China.

E-mail address: [jensxing@126.com](mailto:jensxing@126.com) (Y. Ding).

(continued)

|                      |                                                         |          |                                  |
|----------------------|---------------------------------------------------------|----------|----------------------------------|
| $L_p$                | coil length, m                                          | out      | related to outlet parameter      |
| $N$                  | number of unit cells in the ice storage tank            | $hf$     | related to refrigerant           |
| $Q_{chiller}$        | the hourly cooling capacity of the chiller plant, kW    | $pcm$    | related to phase change material |
| $Q_{chiller, rated}$ | rated cooling capacity of the chiller unit, kW          | $pump$   | related to pump                  |
| $Q_{icecapacity}$    | total nighttime ice storage capacity, kW                | $solid$  | solid state                      |
| $Q_{icem}$           | the hourly cooling capacity of the ice storage tank, kW | $mix$    | ice-water mixture state          |
| $Q_{pre}$            | total cooling load of the building, kW                  | $liquid$ | liquid state                     |
| $T$                  | temperature, °C                                         |          |                                  |

## 1. Introduction

With the continuous proliferation of renewable energy sources and the increasing global demand for electricity, challenges have arisen in ensuring the reliability and stability of the electrical grid due to the intermittency and uncertainty of renewable energy, as well as the growth in peak power demand [1]. Buildings stand out as one of the largest energy consumers among end-users, constituting over 30 % of the global total energy consumption [2]. As a significant component of building energy consumption, HVAC (Heating, Ventilation, and Air Conditioning) systems can actively engage in demand response strategies to achieve load reduction, transfer, and balance power shortages and surpluses in the grid, thereby enhancing grid operational stability [3]. In the face of the dual challenges of escalating energy demand and an oversupply of renewable energy, ice storage technology within the framework of power demand-side management has garnered widespread attention [4].

Ice storage air conditioning systems, leveraging the high energy density of phase change latent heat, can store energy during low electricity prices and release it during peak pricing, actively participating in demand response scheduling, which is increasingly crucial in reducing user electricity costs [5], enhancing grid reliability [6] and integrating renewable energy sources such as wind [7] and solar [8]. Therefore, exploring ice storage systems is essential for improving electricity reliability and promoting sustainable development in green energy sources. However, when responding to control signals, ice storage systems undergo a dynamic process transitioning from one steady state to another. Steady-state mathematical models fail to capture the dynamic response characteristics in the presence of control signal variations, which can affect the precise control and achievement of optimization goals for the system. Hence, it is crucial to explore the dynamic response characteristics of phase-change heat transfer processes at the equipment control level, commencing with the heat transfer mechanism model of the ice storage tank.

Previous researches on phase-change heat transfer modeling primarily focused on analyzing heat transfer phenomena and characteristics during solidification/melting processes, optimizing heat transfer conditions and device structures. To address the challenge of solving moving boundaries, previous studies recommended latent heat methods focusing on sensible heat capacity and enthalpy. By applying numerical analysis for approximate solutions, these methods effectively navigate the complexities of moving boundaries, resulting in an enhancement in computational efficiency [9]. The heat capacity method represents latent heat with a larger heat capacity within the phase-change range, transforming multiphase phase-change problems into single-phase heat transfer issues. Abu-Hamdeh et al. utilized the heat capacity method to represent the latent heat of fusion for ice-water as sensible heat within a

narrow temperature range, simulating the ice melting processes and numerically analyzing the impact of refrigerant flow rate on the transient heat transfer of the shell-and-tube ice storage system [10]. Zhang et al. characterized the heat capacity of water-ice during solidification by applying heat capacity formulas, constructing a thermal model for ice storage units, and examining the influence of fin height and spacing on solidification rate [11]. Ouali et al. established a dynamic model for ice storage tanks based on a specific heat method, where the relationship between the specific heats of solid and liquid phases characterizes the phase change process. Through numerical analysis, it was found that the melting time increased with the height of the ice tank [12]. However, when the phase change temperature range of the medium is too narrow, a slightly larger time step may skip the phase change region, thereby neglecting the latent heat of phase change and leading to significant errors when using the heat capacity method [13]. Unlike the heat capacity method, the enthalpy-based model characterizes the variation of latent heat using enthalpy and the linear relationship between enthalpy and temperature to avoid nonlinear issues during phase-change heat transfer processes. Huang et al. pointed out that the enthalpy method does not track the phase-change boundary when simulating the heat transfer model for melting/solidification. Instead, it introduces the volume percentage of the liquid phase to characterize the physical properties of mushy zone water-ice, thereby describing the segmented linear relationship between temperature and enthalpy [14]. Liu provided formulas for the enthalpy versus temperature of water-ice at different phase-change stages, established a three-dimensional model of an ice storage tank based on the enthalpy-porosity method and investigated temperature distribution, liquid phase composition, and ice growth evolution during the solidification processes [15]. Hamzeh et al. defined the enthalpy of the medium with a segmented definition of the universal liquid fraction, simulated the ice storage/melting process, and analyzed the impact of the size and arrangement of coil-type ice storage tanks on the phase-change process through numerical simulations [16]. Chang et al. developed a heat transfer model for the solidification process of ice tanks and revealed that the ice storage rate of vertically arranged ice storage tanks increased by 13.33 % compared to horizontally arranged ones through experiments and numerical simulations [17]. The enthalpy method uses enthalpy and temperature as the solution variables to establish a unified control equation across the entire heat transfer region, which offers high computational efficiency and excels in handling both rapid and gradual phase transitions [18]. In summary, most of these studies focus on examining the influence of different operating conditions and geometric parameters on heat transfer efficiency. However, the heat capacity method requires establishing separate control equations for different phase states, leading to complex boundary conditions. When using the enthalpy method to construct phase-change heat transfer models, it achieves high accuracy but results in lower computational speed [19].

In thermal energy storage systems, time delays are commonly observed, which significantly impact the implementation of timing predictions and control commands [20]. Time delay characterization in energy systems primarily falls into two categories: empirical-based and parameter identification methods. Empirical-based time delay characterization is predominantly applied in fluid transport processes. Jie et al. employed a dynamic model of district heating systems and introduced peak-valley data analysis to analyze the trend differences in temperature curves, identifying the time lag in measured data based on comparisons of inlet and outlet temperatures [21]. Zhao also proposed a Model Predictive Control (MPC) approach considering time delays for energy systems, estimating the time lag by analyzing the periods during which the power consumption of chillers, pump power, and indoor temperature lag behind the modified system equipment parameters [22]. However, for dynamic continuous systems, time delays are typically not constant, making it difficult for empirical methods to accurately capture its dynamic characteristics [23]. Additionally, demand response scenarios in energy storage systems require rapid response characteristics

from the equipment, and empirical time delay characterization methods are often ineffective. Hence, some scholars employ parameter identification methods to characterize time delays. For instance, Li et al. introduced transfer entropy to the HVAC field, developing a model-free identification method based on an information theory framework to discern time delay characteristics by mining monitoring data [24]. Li et al. pinpointed the challenges of time-varying delays in indoor temperature variations of variable air volume systems, employing the Elman neural network algorithm for nonlinear model time delay identification and comprehensive response characteristic analysis within the MPC [25]. Su used a Markov chain to model uncertain information delays and studied the impact of information delays on the performance of distributed optimization control strategies for HVAC systems [26]. Sun et al. employed the cross-correlation function method to identify the dynamic delay times. The daily adjustment time points were determined to maintain the indoor average temperature within the range of  $20 \pm 1$  °C during winter, significantly reducing the indoor temperature non-uniformity coefficient [27]. Sun developed a dynamic heat transfer model for long-distance pipelines to simulate outlet water temperature and assess the effects of operating conditions, structural features, and insulation parameters on delay times in heat supply [28]. Li et al. established a lighting heat dissipation model based on the law of energy conservation and Laplace transformation, using experimental data and order reduction analysis to identify transfer function model parameters for describing delay effects. The results showed that within 1 h of lighting activation, the proposed transfer function model achieved a MAPE of 3.31 %, significantly outperforming the empirical fixed ratio

method, which had a MAPE of 69.36 % [29]. It can be observed that parameter identification methods are superior to empirical-based methods. However, due to the significant thermal inertia and nonlinear phase change process of ice storage air conditioning systems, researches specifically targeting their dynamic time delay are rather limited. Time delay causes misalignment between input and output signals, reducing model accuracy [30]. When input delay occurs, if the control signal fails to promptly feedback error information, it limits the controller's performance and compromises the stability of the closed-loop system [31]. Furthermore, this is especially crucial when these systems participate in grid demand-side response regulation. Establishing a model based on heat transfer mechanisms to capture the dynamic response of building energy storage systems for system control becomes even more critical in this context.

The optimization control of ice storage cooling systems for demand response has been extensively studied from the perspectives of cost-effectiveness, and grid frequency regulation. In terms of economic considerations, demand response strategies for ice storage air conditioning systems are typically formulated with the optimization objectives of maximizing energy efficiency or minimizing operating costs [32]. For instance, Candanedo investigated an optimal control strategy for commercial building integrated ice storage cooling systems with a refrigeration unit, aiming to provide the required cooling load within the transient power curve at the lowest cost [33]. Jia developed a thermodynamic model for ice storage cooling systems, aiming to minimize daily operating costs, utilizing a branch-and-bound algorithm based on linear programming to solve the optimization problem and

![Research framework diagram showing the integration of Phase Change Heat Transfer Model, Ice Thermal Storage Experiment, Ice Storage System MPC Optimization Design, and MPC Strategy Case Validation.](d244183a8ff3d94b0dcf30140f51020d_img.jpg)

The diagram illustrates a comprehensive research framework for ice storage cooling systems, organized into four main vertical sections:

- Phase Change Heat Transfer Model (Top Left):** This section details the theoretical foundation. It starts with the **Phase Change Heat Transfer Mechanism**, leading to an **Enthalpy-Based Model**. This is followed by the **Heat Transfer Differential Equation**, which can be represented as a **State-Space Equation** or a **Transfer Function**. The **Transfer Function** is linked to the **Time Delay Mechanism**.
- Time Delay Mechanism (Top Center):** This section explains the physical causes of delays. It includes **Thermal Inertia** leading to **Inertial Delay** and **Flow Process** leading to **Flow Delay**. Both types of delay contribute to the **Time Delay at Different Phase Transitions**, which occurs during the **Solid, Liquid, Solid-Liquid Coexistence State**.
- Ice Thermal Storage Experiment (Top Right):** This section outlines the experimental validation process. It includes **Ice Thermal Storage Experiment Design**, followed by the **Ice Melting/ Ice Storage Experiment**. The results are used for **Energy Storage/Discharge Power Analysis**, leading to **Model Accuracy Validation**.
- Ice Storage System MPC Optimization Design (Middle):** This section focuses on the control and optimization strategy. It integrates the **Phase Change Heat Transfer Model** and **Time Delay Mechanism** into the **Phase Change Energy Storage Devices**. The **Cost Function** is defined by **Dynamic Response Performance** and **Demand Response Economics**. The **Reference Trajectory** is compared with **Prediction Outputs** (from the **Building Cooling Load Prediction Model LSTM**) to inform **Rolling Optimization**. **Control Parameters** are then used for **Time Delay Compensation**. The system also incorporates **Energy-Consuming Equipment** and **Measured Data** (via **Least Squares Regression**) for feedback.
- MPC Strategy Case Validation (Bottom):** This section validates the proposed strategy. It uses **Commercial Office Buildings** as a case study, involving **MATLAB Modeling and Simulation**. The results are compared between **MPC** and **PID** controllers in the **Comparison and Analysis of Simulation Results**. The final outcomes are evaluated for **Economic Viability**, **Compliance**, and **Accuracy**.

Research framework diagram showing the integration of Phase Change Heat Transfer Model, Ice Thermal Storage Experiment, Ice Storage System MPC Optimization Design, and MPC Strategy Case Validation.

Fig. 1. Research framework.

![Fig. 2. Schematic diagram of ice storage tank structure. The figure consists of three separate technical diagrams. The top diagram shows a cross-section of a tank with a central vertical column and multiple horizontal pipes or tubes running through it, with some pipes coiled around the column. The middle diagram shows a cross-section of a tank with a central vertical column and multiple horizontal pipes or tubes running through it, with some pipes coiled around the column. The bottom diagram shows a cross-section of a tank with a central vertical column and multiple horizontal pipes or tubes running through it, with some pipes coiled around the column.](ddfe517a5ad9c77c89a57a5e780b24ca_img.jpg)

Fig. 2. Schematic diagram of ice storage tank structure. The figure consists of three separate technical diagrams. The top diagram shows a cross-section of a tank with a central vertical column and multiple horizontal pipes or tubes running through it, with some pipes coiled around the column. The middle diagram shows a cross-section of a tank with a central vertical column and multiple horizontal pipes or tubes running through it, with some pipes coiled around the column. The bottom diagram shows a cross-section of a tank with a central vertical column and multiple horizontal pipes or tubes running through it, with some pipes coiled around the column.

Fig. 2. Schematic diagram of ice storage tank structure.

revealing a cost reduction of 11.2 % compared to the baseline case [34]. Al-Aali et al. established a dual-layer optimization model for optimal equipment and storage scheduling in ice storage multiple chiller systems. By comparing two commonly used heuristic storage dispatch strategies, the optimal control can reduce cost and energy by 11–14 % and 10–12 %, respectively, relative to storage priority control, and 16–33 % and 1–9%, respectively, relative to chiller priority control [35]. Regarding grid frequency regulation, energy storage systems, including ice storage systems, have garnered significant attention as controllable energy resources. For instance, Yan proposed an ice storage cooling system operation strategy that integrated different time scales to address grid demand response, aiming to flatten the grid load curve, and the effectiveness of achieving power balance across multiple time scales was validated through case studies [36]. Nie developed a dual-time-scale optimization model with ice storage cooling, presenting a control strategy to shift a significant amount of electricity from non-peak hours to peak hours, which effectively resulted in reduced power costs [37]. Cui et al. investigated the demand response potential of a building with ice storage devices and developed a control strategy to mitigate immediate and stepwise power demands by shutting down chillers as needed, thus enhancing grid stability [38]. Additionally, researchers have investigated the relationship between local conditions and the ice storage efficiency of ice storage systems under demand response. For instance, Sephehri et al. used regions with significant day-night temperature differences and arid climates as case studies. They revealed that the larger diurnal temperature variation and below-freezing nighttime temperatures led to higher average round-trip energy efficiency [39]. Furthermore, studies have indicated that over 100 % effective round-trip efficiency could create a strong case for ice thermal energy storage as an energy storage approach for reducing primary energy consumption and carbon emissions, particularly if fleet efficiencies are higher and carbon intensities are lower overnight [40]. Nevertheless, a considerable body of research on the participation of ice storage systems in demand response predominantly emphasized optimal operational strategies and

expected benefits, overlooking the dynamic response processes during actual implementation. This gap in focus may present challenges in ensuring the swift adherence of the entire system to control plans [41].

In summary, current research in ice storage modeling and optimization control of HVAC systems encounters critical challenges. Consequently, the MPC for ice-storage air conditioning systems with time delay compensation integration is proposed to bridge the previous research gaps. The existing research gaps and critical contributions are as follows.

- 1) Complex Phase-change heat transfer models: traditional models are complex, computationally heavy, and difficult to couple with system control models. To mitigate this, a novel enthalpy-based model is proposed that simplifies this process by piecewise linearizing the nonlinear phase change process. Subsequently, by employing the state-space method, dynamic heat transfer differential equations are transformed into transfer functions form for application in system control.
- 2) Time delay in system control: the delay times in ice storage cooling systems significantly impact temporal predictions and control. Due to the significant thermal inertia and nonlinear phase change process of ice storage air conditioning systems, their delay times are challenging to characterize. A dynamic method for calculating inertia and flow delay times is formulated by utilizing transfer functions. Additionally, an improved MPC embedded a time-delay compensation module is proposed.
- 3) Optimization of control strategies: prior research on the control of ice storage focused on economic aspects of system control, with little consideration given to the dynamic response processes at the equipment level or optimizing dynamic response performance. To bridge this gap, a dual-objective operational control strategy is proposed, which balances the economic efficiency of demand response strategies and the dynamic response control performance.

![Fig. 3. Schematic diagram of internal-melt coil ice storage tank structure. The diagram shows a cross-section of a tank. At the top, a refrigerant HTF flows through a coil of length L_p. Below the coil is a layer of water-ice. The coil is submerged in the water-ice. The refrigerant inlet is labeled T_{hf,in}, G_{hf,in} and the outlet is T_{hf,out}, G_{hf,out}. The coil is labeled 'Heat Exchanger Coil'. The water-ice layer is labeled 'Water-Ice'. The refrigerant HTF is labeled 'Refrigerant HTF'. The coil length L_p is indicated with a double-headed arrow. The coil area A_p is indicated with a circle. The temperature and enthalpy of the phase-change material (PCM) are labeled T_{PCM}, H_{PCM}.](e394c2b5c61344f6a12397f430086072_img.jpg)

Fig. 3. Schematic diagram of internal-melt coil ice storage tank structure. The diagram shows a cross-section of a tank. At the top, a refrigerant HTF flows through a coil of length L\_p. Below the coil is a layer of water-ice. The coil is submerged in the water-ice. The refrigerant inlet is labeled T\_{hf,in}, G\_{hf,in} and the outlet is T\_{hf,out}, G\_{hf,out}. The coil is labeled 'Heat Exchanger Coil'. The water-ice layer is labeled 'Water-Ice'. The refrigerant HTF is labeled 'Refrigerant HTF'. The coil length L\_p is indicated with a double-headed arrow. The coil area A\_p is indicated with a circle. The temperature and enthalpy of the phase-change material (PCM) are labeled T\_{PCM}, H\_{PCM}.

Fig. 3. Schematic diagram of internal-melt coil ice storage tank structure.

The structure of this paper is as follows: Section 2 describes the modeling of ice storage tank heat transfer and the MPC method for ice storage cooling systems. In Section 3, the experimental design and the case building are introduced. Section 4 involves model validation and analyzes the dynamic response performance of ice storage tank cooling scenarios and the control effectiveness in demand response scenarios. The conclusion is drawn in Section 5. The framework of the research approach is illustrated in Fig. 1.

## 2. Methodology

### 2.1. Heat transfer differential equations

The enthalpy-based model is a classical model in numerical analysis for addressing the variation of solid-liquid interface shape and position over time during phase-change processes [42], which employs linear processes in the enthalpy-temperature space to circumvent the nonlinearity associated with phase change heat transfer. Furthermore, in the temperature-enthalpy relationship, a small temperature band ( $0.2^\circ\text{C}$ ) is introduced to describe the piecewise linear relationship between the two variables [43], ensuring a one-to-one correspondence between the two variables and determining the temperature of the control volume using Eq (1).

$$T_{pcm} = \begin{cases} (T_m - 0.1) + \frac{H}{c_{pcm}}, & H \le 0 \\ \frac{0.2}{\Delta H_m} \cdot H + (T_m - 0.1), & 0 < H < \Delta H_m \\ (T_m + 0.1) + \frac{H - \Delta H_m}{c_{pcm}}, & H \ge \Delta H_m \end{cases} \quad (1)$$

In Eq. (1), when  $H \le 0$ , the phase-change material is in the solid state, namely ice.  $H \ge \Delta H_m$  corresponds to the liquid state, namely water. And for  $0 < H < \Delta H_m$ , the phase-change material is in a phase transition process, which is the solid-liquid coexistence region known as the mushy zone.

The internal ice-melting coil storage tank is widely applied across various engineering projects for its fast melting rate, high reliability, and efficient ice production, which consists of a water-filled tank and a coil submerged in the water. During ice storage, a low-temperature chiller cools the refrigerant to approximately  $-5^\circ\text{C}$ , causing the water around the coil to gradually cool and freeze along the coil walls. During ice melting, the higher-temperature refrigerant flows through the coil within the ice storage tank, melting the ice to supply cooling to the end users. The internal melt-coil ice storage tank and fluid structure are depicted in Figs. 2 and 3. To simplify the analysis, the one-dimensional heat transfer model for the ice storage tank is based on the following assumptions.

- (1) Neglecting the axial heat transfer effects of the refrigerant solution, heat transfer occurs radially only.

- (2) Assuming the ice storage tank body is entirely adiabatic, with no heat exchange between the tank body and the external environment.
- (3) Assume the phase-change interface during the cooling process varies concentric and circularly, exhibiting symmetric distribution throughout the entire process.
- (4) Assume a uniform water temperature distribution outside the coil, disregarding the influence of the deadband inside the tank.
- (5) Considering the presence of melting constraints, disregarding the motion of solid ice.
- (6) Assuming that, except for the density and thermal conductivity in the mushy zone, all other properties in the system are considered constant.

Based on the abovementioned assumptions, the energy balance equations are established for the cooling/charging process within the ice storage tank, which are referred to the one-dimensional heat transfer equation in the [44]. Considering the variations in the phase-change material, and in conjunction with the enthalpy-based model, the heat transfer process can be divided into three distinct stages: the liquid phase stage, the solid-liquid mushy stage, and the solid phase stage.

- (1) The liquid phase stage (water):

Energy balance equation on the refrigerant side:

$$c_{hf}\rho_{hf}A_p \frac{L_p}{N} \frac{dT_{hf,i+1}}{dt} = G_{hf}c_{hf}(T_{hf,i} - T_{hf,i+1}) + \frac{UA_i}{N} \left( \frac{H_i - \Delta H_m}{c_{pcm}} - T_{hf,i} \right) \quad (3)$$

Energy balance equation for the liquid phase zone outside the coil:

$$\rho_{pcm} \frac{V_{pcm}}{N} \frac{dH_{i+1}}{dt} = \lambda_{pcm} \frac{NA_{pcm}}{L_p c_{pcm}} (H_i - H_{i+1}) + \frac{UA_i}{N} \left( T_{hf,i} - \frac{H_i - \Delta H_m}{c_{pcm}} \right) \quad (4)$$

- (2) The solid-liquid mushy stage (ice-water mixture):

Energy balance equation on the refrigerant side:

$$c_{hf}\rho_{hf}A_p \frac{L_p}{N} \frac{dT_{hf,i+1}}{dt} = G_{hf}c_{hf}(T_{hf,i} - T_{hf,i+1}) + \frac{UA_i}{N} (T_{pcm,m} - T_{hf,i}) \quad (5)$$

Energy balance equation for the ice-water mushy zone outside the coil:

$$\rho_{pcm} \frac{V_{pcm}}{N} \frac{dH_{i+1}}{dt} = \lambda_{pcm} \frac{NA_{pcm}}{L_p c_{pcm}} (H_i - H_{i+1}) + \frac{UA_i}{N} (T_{hf,i} - T_{pcm,m}) \quad (6)$$

- (3) The solid phase stage (ice):

Energy balance equation on the refrigerant side:

$$c_{hf}\rho_{hf}A_p \frac{L_p}{N} \frac{dT_{hf,i+1}}{dt} = G_{hf}c_{hf}(T_{hf,i} - T_{hf,i+1}) + \frac{UA_i}{N} \left( \frac{H_i}{c_{pcm}} - T_{hf,i} \right) \quad (7)$$

Energy balance equation for the solid phase zone outside the coil:

$$\rho_{pcm} \frac{V_{pcm}}{N} \frac{dH_{i+1}}{dt} = \lambda_{pcm} \frac{NA_{pcm}}{L_p c_{pcm}} (H_i - H_{i+1}) + \frac{UA_i}{N} \left( T_{hf,i} - \frac{H_i}{c_{pcm}} \right) \quad (8)$$

### 2.2. Ice storage tank heat transfer modeling

Transfer functions are utilized to formulate a simplified heat transfer model, with a specific focus on the state of the medium at the inlet and outlet of the device to analyze the power variations during the storage/release process of the cooling capacity. Using the state-space method, the initially established multi-input, multi-output state-space equations are transformed into transfer function form in the s-domain. The expression for the coefficient matrices of the linear state-space equations is derived by solving the steady-state solutions of the corresponding

steady-state differential equations, where the steady-state equations refer to the algebraic equation set corresponding to the derivative terms being zero. The linearization of the total heat transfer coefficient,  $U$ , is achieved through a first-order Taylor expansion formula, leading to the following linearized results.

#### (1) The liquid phase stage (water):

Energy balance equation on the refrigerant side:

$$\begin{aligned} \frac{d\delta T_{hf,i+1}}{dt} &= \left( \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} - \frac{\bar{U}A_l}{c_{hf}\rho_{hf}A_pL_p} \right) \delta T_{hf,i} \\ &\quad - \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} \delta T_{hf,i+1} + \frac{\bar{U}A_l}{c_{hf}\rho_{hf}A_pL_p} \frac{\delta H_i}{c_{pcm}} \\ &+ \left( \frac{N(\bar{T}_{hf,i} - \bar{T}_{hf,i+1})}{\rho_{hf}A_pL_p} + \frac{A_l}{c_{hf}\rho_{hf}A_pL_p} \left( \frac{\bar{H}_i - \Delta H_m}{c_{pcm}} - \bar{T}_{hf,i} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \right) \delta G_{hf} \end{aligned} \quad (9)$$

Energy balance equation for the liquid phase zone outside the coil:

$$\begin{aligned} \frac{d\delta H_{i+1}}{dt} &= \left( \lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} - \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm} c_{pcm}} \right) \delta H_i \\ &\quad - \lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} \delta H_{i+1} \\ &+ \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm}} \delta T_{hf,i} + \frac{A_l}{\rho_{pcm} V_{pcm}} \left( \bar{T}_{hf,i} - \frac{\bar{H}_i - \Delta H_m}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \delta G_{hf} \end{aligned} \quad (10)$$

#### (2) The solid-liquid mushy stage (ice-water mixture):

Energy balance equation on the refrigerant side:

$$\begin{aligned} \frac{d\delta T_{hf,i+1}}{dt} &= \left( \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} - \frac{\bar{U}A_l}{c_{hf}\rho_{hf}A_pL_p} \right) \delta T_{hf,i} - \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} \delta T_{hf,i+1} \\ &+ \left( \frac{N(\bar{T}_{hf,i} - \bar{T}_{hf,i+1})}{\rho_{hf}A_pL_p} + \frac{A_l}{c_{hf}\rho_{hf}A_pL_p} \left( \frac{T_{pcm,m} - \bar{T}_{hf,i}}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \right) \delta G_{hf} \end{aligned} \quad (11)$$

Energy balance equation for the ice-water mushy zone outside the coil:

$$\begin{aligned} \frac{d\delta H_{i+1}}{dt} &= \lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} \delta H_i - \lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} \delta H_{i+1} \\ &+ \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm}} \delta T_{hf,i} + \frac{A_l}{\rho_{pcm} V_{pcm}} \left( \bar{T}_{hf,i} - T_{pcm,m} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \delta G_{hf} \end{aligned} \quad (12)$$

#### (3) The solid phase stage (ice):

Energy balance equation on the refrigerant side:

$$\begin{aligned} \frac{d\delta T_{hf,i+1}}{dt} &= \left( \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} - \frac{\bar{U}A_l}{c_{hf}\rho_{hf}A_pL_p} \right) \delta T_{hf,i} - \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} \delta T_{hf,i+1} \\ &+ \frac{\bar{U}A_l}{c_{hf}\rho_{hf}A_pL_p} \frac{\delta H_i}{c_{pcm}} + \left( \frac{N(\bar{T}_{hf,i} - \bar{T}_{hf,i+1})}{\rho_{hf}A_pL_p} + \frac{A_l}{c_{hf}\rho_{hf}A_pL_p} \left( \frac{\bar{H}_i - \bar{T}_{hf,i}}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \right) \delta G_{hf} \end{aligned} \quad (13)$$

Energy balance equation for the solid phase zone outside the coil:

$$\begin{aligned} \frac{d\delta H_{i+1}}{dt} &= \left( \lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} - \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm} c_{pcm}} \right) \delta H_i \\ &\quad - \lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} \delta H_{i+1} \\ &+ \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm}} \delta T_{hf,i} + \frac{A_l}{\rho_{pcm} V_{pcm}} \left( \bar{T}_{hf,i} - \frac{\bar{H}_i}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \delta G_{hf} \end{aligned} \quad (14)$$

Based on the transformed linear heat transfer equation, the coefficient matrices of the state-space equations are represented as Eqs. (15)–(22).

$$a_1 = \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} - \frac{\bar{U}A_l}{c_{hf}\rho_{hf}A_pL_p} \quad (15)$$

$$a_2 = - \frac{N\bar{G}_{hf}}{\rho_{hf}A_pL_p} \quad (16)$$

$$a_3 = \frac{\bar{U}A_l}{c_{hf}\rho_{hf}A_pL_p c_{pcm}} \quad (17)$$

$$a_4 = \begin{cases} \frac{\lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} - \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm} c_{pcm}}}{\lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}}}, & H > \Delta H_m \\ \frac{\lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}}}{\lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}}}, & 0 < H < \Delta H_m \\ \frac{\lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} - \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm} c_{pcm}}}{\lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}}}, & H < 0 \end{cases} \quad (18)$$

$$a_5 = - \lambda_{pcm} \frac{N^2 A_{pcm}}{\rho_{pcm} V_{pcm} L_p c_{pcm}} \quad (19)$$

$$a_6 = \frac{\bar{U}A_l}{\rho_{pcm} V_{pcm}} \quad (20)$$

$$b_{11,j} = \begin{cases} \left( \frac{N(\bar{T}_{hf,i} - \bar{T}_{hf,i+1})}{\rho_{hf}A_pL_p} + \frac{A_l}{c_{hf}\rho_{hf}A_pL_p} \left( \frac{\bar{H}_i - \Delta H_m}{c_{pcm}} - \bar{T}_{hf,i} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \right), & H > \Delta H_m \\ \left( \frac{N(\bar{T}_{hf,i} - \bar{T}_{hf,i+1})}{\rho_{hf}A_pL_p} + \frac{A_l}{c_{hf}\rho_{hf}A_pL_p} \left( \frac{T_{pcm,m} - \bar{T}_{hf,i}}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \right), & 0 < H < \Delta H_m \\ \left( \frac{N(\bar{T}_{hf,i} - \bar{T}_{hf,i+1})}{\rho_{hf}A_pL_p} + \frac{A_l}{c_{hf}\rho_{hf}A_pL_p} \left( \frac{\bar{H}_i - \bar{T}_{hf,i}}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}} \right), & H < 0 \end{cases} \quad (21)$$

$$b_{21,j} = \begin{cases} \frac{A_l}{\rho_{pcm} V_{pcm}} \left( \bar{T}_{hf,i} - \frac{\bar{H}_i - \Delta H_m}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}}, & H > \Delta H_m \\ \frac{A_l}{\rho_{pcm} V_{pcm}} \left( \bar{T}_{hf,i} - T_{pcm,m} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}}, & 0 < H < \Delta H_m \\ \frac{A_l}{\rho_{pcm} V_{pcm}} \left( \bar{T}_{hf,i} - \frac{\bar{H}_i}{c_{pcm}} \right) \left( \frac{\partial U}{\partial G_{hf}} \right)_{\bar{G}_{hf}}, & H < 0 \end{cases} \quad (22)$$

By selecting  $T_{hf,in}$ ,  $G_{hf,in}$  and  $H_{in}$  as input parameters and considering  $T_{hf,i}$  and  $H_i$  with differentials as the state variables during the heat transfer process, with the outlet temperature of the refrigerant inside the ice storage tank coil,  $T_{hf,out}$ , as the output variable, the two heat transfer differential equations mentioned above can be transformed into the following linear state-space model:

$$\frac{dT}{dt} = AT + B_1 G_{in} + B_2 T_{hf,in} + B_3 H_{in} \quad (23)$$

$$T_{hf,out} = CT \quad (24)$$

In Eqs. (23) and (24),  $T = [T_{hf,1} \ T_{hf,2} \ \dots \ T_{hf,N} \ H_1 \ H_2 \ \dots \ H_N]^T$ ,  $A$ ,  $\{B_1, B_2, B_3\}$  and  $C$  represent the state matrix, input matrix, and output matrix of the state-space equations, respectively, represented as Eqs. (25)–(31).

![Fig. 4. Input-output structure of ice storage cooling system. The diagram shows a vertical flow from Input Variable to Transfer Function to Calculation of Time Delay, and finally to System Output. Input variables are G_in, T_hf,in, and T_pcm,in. Transfer functions are G_1(s), G_2(s), and G_3(s). Time delay calculations are tau_pure, tau_ther,1, and tau_ther,2. The system output is T_hf,out.](a738993919a50143787084ee7ce6e2f2_img.jpg)

Fig. 4. Input-output structure of ice storage cooling system. The diagram shows a vertical flow from Input Variable to Transfer Function to Calculation of Time Delay, and finally to System Output. Input variables are G\_in, T\_hf,in, and T\_pcm,in. Transfer functions are G\_1(s), G\_2(s), and G\_3(s). Time delay calculations are tau\_pure, tau\_ther,1, and tau\_ther,2. The system output is T\_hf,out.

Fig. 4. Input-output structure of ice storage cooling system.

![Fig. 5. Connections between density, thermal conductivity, temperature, and enthalpy. The graph plots rho_pcm (kg/m^3), lambda_pcm (W/(m.K)), and T_pcm (°C) against H (kJ/kg). The x-axis ranges from 0 to 390 kJ/kg, divided into three phases: Solid-ice (0-91.7 kJ/kg), Solid-liquid coexistence zone (91.7-390 kJ/kg), and Liquid-water (390-400 kJ/kg). Density rho_pcm increases from 917 to 999 kg/m^3. Thermal conductivity lambda_pcm decreases from 2.1 to 0.55 W/(m.K). Temperature T_pcm increases from -12 to 12 °C.](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Fig. 5. Connections between density, thermal conductivity, temperature, and enthalpy. The graph plots rho\_pcm (kg/m^3), lambda\_pcm (W/(m.K)), and T\_pcm (°C) against H (kJ/kg). The x-axis ranges from 0 to 390 kJ/kg, divided into three phases: Solid-ice (0-91.7 kJ/kg), Solid-liquid coexistence zone (91.7-390 kJ/kg), and Liquid-water (390-400 kJ/kg). Density rho\_pcm increases from 917 to 999 kg/m^3. Thermal conductivity lambda\_pcm decreases from 2.1 to 0.55 W/(m.K). Temperature T\_pcm increases from -12 to 12 °C.

Fig. 5. Connections between density, thermal conductivity, temperature, and enthalpy.

$$C = [0_{N-1} \ 1 \ 0_N]^T \quad (31)$$

Applying a Laplace transform to the state-space equations of the system results in the input-output model of the ice storage tank, represented as Eq. (32):

$$T_{hf,out} = G_1(s)G_{in} + G_2(s)T_{hf,in} + G_3(s)H_{in} \quad (32)$$

In Eq. (32),  $G_1(s)$ ,  $G_2(s)$  and  $G_3(s)$  represent transfer functions.

Fig. 4 illustrates the transfer function structure of the ice storage tank, featuring multiple inputs and a single output.

### 2.3. Representation of time delay in ice storage cooling system

In the context of ice storage cooling systems participating in energy system regulation processes, the overall time delay is the coupled effect of thermal inertia and flow delay [21,43]. The energy storage unit within the ice storage cooling system is the ice storage tank, utilizing two heat transfer media (refrigerant: ethylene glycol solution; phase-change medium: water-ice), whose thermal inertia is related to the coefficients of the partial derivatives  $dT_{hf}/dt$  and  $dH/dt$  in the partial differential equations [45]. Due to the relatively stable physical properties of the ethylene glycol solution within a certain temperature range, its physical properties can be treated as constants. The temperature and enthalpy variations during the ice melting process in the ice storage tank can be represented in a piecewise linearized form, corresponding to three phases: solid ice, the solid-liquid mushy zone, and liquid water. Fig. 5 illustrates the magnitude of variations in the physical properties during diverse heat transfer processes in the ice storage tank.

As shown in Fig. 5, it is evident that the variations in physical properties during sensible heat exchange within both solid and liquid phases can be neglected and treated as constants. Conversely, the properties of the ice-water mixture in the mushy zone undergo significant changes during the phase-change process, with density ranging from 917 to 999.8 kg/m<sup>3</sup> and thermal conductivity varying from 0.55 to 2.1 W/(m·K). Through curve fitting, equations describing the density and thermal conductivity of the phase-change medium as functions of enthalpy within the temperature range of -10 to 15 °C (corresponding to an enthalpy change range of -20 kJ/kg to 400 kJ/kg) can be obtained as represented by Eqs. (33) and (34):

$$\begin{cases} \rho_{pcm,solid} = 917 \\ \rho_{pcm,mix} = 0.2435 \times H + 916.9 \\ \rho_{pcm,liquid} = 999 \end{cases} \quad (33)$$

$$\begin{cases} \lambda_{pcm,solid} = 2.1 \\ \lambda_{pcm,mix} = -0.004521 \times H + 2.1 \\ \lambda_{pcm,liquid} = 0.55 \end{cases} \quad (34)$$

The inertial time constant and pure time delay of the medium can be calculated from the transfer function, as shown in Eqs. (35) and (36).

$$G(s) = \frac{1}{\tau_c s + 1} \quad (35)$$

$$G(s) = \frac{1}{e^{\tau_p s}} \quad (36)$$

Based on Eqs. (32)–(36), expressions for the inertial time delay of the phase-change medium can be formulated.

When  $H \le 0$ , the phase-change medium is in the solid ice state:

$$\begin{cases} \tau_{c,hf,solid} = \left( \frac{C_{hf} \rho_{hf} A_p L_p}{U A_i} \right)_{solid} \\ \tau_{c,pcm,solid} = \left( \frac{V_{pcm} \rho_{pcm}}{U A_i} \right)_{solid} \end{cases} \quad (37)$$

When  $H = 0$ , the phase-change medium is in the solid-liquid coexisting mushy zone:

![Figure 6: Predictive control model structure diagram. The diagram illustrates a closed-loop control system. A 'Reference Trajectory' block receives a setpoint $T_{set}$ and outputs a signal to a summing junction. The summing junction also receives a 'Predicted Output' signal, resulting in a 'Deviation $e(t)$'. This deviation is fed into a 'min J(k) PSO' block, which generates a 'Control Sequence $U(k)$'. This sequence is then processed by a 'Calculation of Delay Time' block (indicated by a dashed red box), which outputs the 'Actual Control Sequence $U(k - \tau_p)$'. This actual sequence is fed into a 'Mathematical Modeling of Equipment' block, which produces a 'Predicted Output' signal. This predicted output is fed back into the summing junction. Additionally, the 'Mathematical Modeling of Equipment' block outputs $Q_{pre}$, which is compared with $Q_s$ (from the 'Building Cooling System Model LSTM') at a second summing junction to produce $Q_e$. The 'Building Cooling System Model LSTM' also outputs $T_{out}$. The 'Predicted Output' block also receives $Q_e$ and $T_{out}$ as inputs for feedback correction.](990567efebf979be51f56d1150012c9d_img.jpg)

Figure 6: Predictive control model structure diagram. The diagram illustrates a closed-loop control system. A 'Reference Trajectory' block receives a setpoint \$T\_{set}\$ and outputs a signal to a summing junction. The summing junction also receives a 'Predicted Output' signal, resulting in a 'Deviation \$e(t)\$'. This deviation is fed into a 'min J(k) PSO' block, which generates a 'Control Sequence \$U(k)\$'. This sequence is then processed by a 'Calculation of Delay Time' block (indicated by a dashed red box), which outputs the 'Actual Control Sequence \$U(k - \tau\_p)\$'. This actual sequence is fed into a 'Mathematical Modeling of Equipment' block, which produces a 'Predicted Output' signal. This predicted output is fed back into the summing junction. Additionally, the 'Mathematical Modeling of Equipment' block outputs \$Q\_{pre}\$, which is compared with \$Q\_s\$ (from the 'Building Cooling System Model LSTM') at a second summing junction to produce \$Q\_e\$. The 'Building Cooling System Model LSTM' also outputs \$T\_{out}\$. The 'Predicted Output' block also receives \$Q\_e\$ and \$T\_{out}\$ as inputs for feedback correction.

Fig. 6. Predictive control model structure diagram.

$$\begin{cases} \tau_{c,hf,mix} = \left( \frac{C_{hf}\rho_{hf}A_pL_p}{UA_i} \right)_{mix} \\ \tau_{c,pcm,mix} = \left( \frac{V_{pcm}\rho_{pcm}}{UA_i} \right)_{mix} \end{cases} \quad (38)$$

When  $H \ge 0$ , the phase-change medium is in the liquid water state:

$$\begin{cases} \tau_{c,hf,liquid} = \left( \frac{C_{hf}\rho_{hf}A_pL_p}{UA_i} \right)_{liquid} \\ \tau_{c,pcm,liquid} = \left( \frac{V_{pcm}\rho_{pcm}}{UA_i} \right)_{liquid} \end{cases} \quad (39)$$

The pure time delay, caused by fluid flow, can be determined as the flow time for the refrigerant to travel from the actuation execution position to the control output position. The expression for the pure time delay is given by Eq. (40):

$$\tau_p = \frac{L}{v} = \frac{\rho_{hf} \cdot \pi r_i^2 \cdot L}{G_{hf}} \quad (40)$$

### 2.4. Model predictive control of the ice storage cooling system

The MPC is the optimization control based on predicting the system's performance over a future time horizon, which primarily consists of three key components: model prediction, rolling optimization, and feedback correction [46]. Because the Long Short-Term Memory (LSTM) demonstrates better accuracy and robustness in short-term load forecasting [47], in order to obtain better dynamic load characteristics, the LSTM network model is employed for load prediction in this study [48]. Within the cost function of rolling optimization, the total daily operational expenses of the system are considered, which also embodies the system's flexibility through demand response. Moreover, the squared deviation between the predicted control output temperature and the set point is also considered, thereby fortifying the system's accuracy and responsiveness. The Particle Swarm Optimization (PSO) algorithm is applied to address the rolling optimization problem in the MPC.

Furthermore, a dynamic time delay compensation component is incorporated to mitigate time delays, ensuring the swift and precise response of the ice storage cooling system across various potential demand response scenarios. The control increment signal of the time delay compensation module is calculated from Eqs. (37)–(40), along with the state of refrigerant temperature and flow rate. This yields the anticipatory control signal for the actuator to implement feedforward control on the controlled process, effectively minimizing the time delay in the HVAC system.

The established optimization objective function is formulated as shown in Eq. (41):

$$J = \min \left[ \left[ \sum_{i=1}^{24} \left( \sum_{m=1}^{N1} E_{ch,m,i} + \sum_{n=1}^{N2} E_{pump,n,i} \right) \times c_i \right] + \sum_{i=k+1}^{N} \left( \hat{T}_{ws,set} - T_{ws} \right)^2 \right] \quad (41)$$

Where  $E_{ch}$  represents the energy consumption of the chiller unit,  $E_{pump}$

represents the energy consumption of the water pump.

In the allocation of cooling capacity, the combined cooling capacities from both the chiller unit and the ice storage tank should be equal to the value of  $\dot{q}_{pre}$  at that particular moment. The equipment capacity constraints dictate that  $q_{chiller}$  should be greater than or equal to 30 % of  $q_{chiller, rated}$  and less than or equal to  $q_{chiller, rated}$ . Additionally,  $q_{icem}$  should not exceed the maximum ice melting cooling capacity at that moment. Considering the effective utilization of ice storage, the daytime ice melting demand is set to 95 % of  $Q_{icecapacity}$ , and the cooling rate of ice melting does not exceed the maximum cooling capacity of the ice storage tank. At the control level, the rolling-optimized control input parameters include  $T_{ei}$ ,  $M_g$  and  $T_{ci}$ , with the controlled variable  $T_{ws}$ .

Specifically, the mathematical expressions for the constraints of the optimization problem are given by Eq. (42).

$$u_{opt}(k) = \underset{u(k)}{\operatorname{argmin}} J(k)$$

$$\left\{ \begin{array}{l} \text{always} \left\{ \begin{array}{l} \dot{q}_{pre,k} = q_{chiller,k} + q_{icem,k} \\ M_{g,min} \le M_g \le M_{g,max} \\ \sum_{i=1}^{N} q_{icem,k} = 0.95 \times \sum_{i=1}^{N} q_{ices,k} \le Q_{icecapacity} \\ q_{icem,k} \le q_{icem,max} \\ T_{ws} = T_{set} \end{array} \right. \\ \text{s.t.} \left\{ \begin{array}{l} \text{daytime} \left\{ \begin{array}{l} 0.3 \times q_{chiller,day,rated} \le q_{chiller,day,k} \le q_{chiller,day,rated} \\ T_{ei,day,min} \le T_{ei} \le T_{ei,day,max} \\ T_{ci,day,min} \le T_{ci} \le T_{ci,day,max} \\ q_{icem,k} \ge 0 \end{array} \right. \\ \text{nighttime} \left\{ \begin{array}{l} 0.3 \times q_{chiller,night,rated} \le q_{chiller,night,k} \le q_{chiller,night,rated} \\ T_{ei,night,min} \le T_{ei} \le T_{ei,night,max} \\ T_{ci,day,min} \le T_{ci} \le T_{ci,day,max} \\ q_{icem,k} \le 0 \end{array} \right. \end{array} \right. \end{array} \right. \quad (42)$$

Utilizing the time delay expressions, a time delay compensation module is embedded into the MPC controller as illustrated in Fig. 6. At each control node, the time delay is calculated based on the control increments  $\Delta t_k$ , which is then transmitted to the control sequence signal, thereby achieving the elimination of time delays in the subsequent response.

## 3. Case study

This study proposes a method for calculating the time delay in ice storage systems and an MPC with an embedded time delay compensation module. The experimental testbed validates the accuracy of the time

![Flowchart of the ice storage cooling system. The diagram shows a closed-loop system with several components: an Air Source Heat Pump, an Ice Storage Tank (divided into six sections: 1, 2, 3, 4, 5, 6), a Bladder Expansion Tank, a Refrigerant Pump, a Plate Heat Exchanger, a Hot Water Tank, and a Temperature-Controlled Cabinet. A Computer and Data Logger are connected to Temperature Measuring Instruments. Flow is controlled by various valves (V1-V6) and flow control valves. Flow Meters are also present. A legend defines the symbols for valves, flow control valves, and flow meters.](562f471e8153729557e6a4ee6343c32c_img.jpg)

Flowchart of the ice storage cooling system. The diagram shows a closed-loop system with several components: an Air Source Heat Pump, an Ice Storage Tank (divided into six sections: 1, 2, 3, 4, 5, 6), a Bladder Expansion Tank, a Refrigerant Pump, a Plate Heat Exchanger, a Hot Water Tank, and a Temperature-Controlled Cabinet. A Computer and Data Logger are connected to Temperature Measuring Instruments. Flow is controlled by various valves (V1-V6) and flow control valves. Flow Meters are also present. A legend defines the symbols for valves, flow control valves, and flow meters.

Fig. 7. Flowchart of the ice storage cooling system.

Table 1

Valve status for different system operating conditions.

| Operating conditions | Valve 1 | Valve 2 | Valve 3 | Valve 4 | Valve 5 | Valve 6 | Flow control valve 1 | Flow control valve 2 |
|----------------------|---------|---------|---------|---------|---------|---------|----------------------|----------------------|
| Ice storage          | on      | off     | on      | off     | on      | off     | on                   | off                  |
| Ice release          | off     | on      | off     | on      | off     | on      | on                   | on                   |

Table 2

Main experimental instruments and equipment.

| Equipment name       | Equipment model | Equipment capacity | Equipment size           |
|----------------------|-----------------|--------------------|--------------------------|
| Ice storage tank     | /               | 25RT               | 2072cm × 1149cm × 780 cm |
| Air source heat pump | KCL-010DA       | 17.6 kW            | 1300cm × 780cm × 1335 cm |
| Hot water tank       | /               | 5 kW–20 kW         | 177L                     |
| Plate heat exchanger | K050M-34        | 17 kW              | 106mm × 81.4mm × 302 mm  |

delay calculations, while the engineering demonstration evaluates the effectiveness of the proposed method in practical applications.

### 3.1. Experimental design

To validate the delay time accuracy of the ice storage tank, an experimental testbed with a coiled internal melting ice storage tank is constructed in this study. The system schematic is illustrated in Fig. 7, comprising the ice storage tank, the cooling and heating sources, the circulating and ancillary systems, and the data acquisition systems. The coiled internal melting ice storage tank consists of three sets of tank bodies, each containing two sets of ice storage coils. Cooling for ice storage within the tank is facilitated by an air-cooled heat pump, while heating during ice melting is provided by a heating water tank equipped with an embedded heating rod. The circulation and ancillary systems comprise the ice melting circulation pump, expansion tank, plate heat exchanger, thermostat, circulation pump for the circulating heat source, flow control valve, exhaust valve, and pressure gauge. And the valve on/off states corresponding to different system operating conditions are shown in Table 1.

The main experimental instruments are listed in Table 2.

The required experimental parameters include the inlet and outlet

Table 3

Testing instruments and accuracy.

| Instrument model                              | Measured parameters                   | Measurement accuracy | Measurement range                      |
|-----------------------------------------------|---------------------------------------|----------------------|----------------------------------------|
| PT100 Resistance thermometer (WAP-187)        | Refrigerant temperature               | ±0.3 °C              | –200~450 °C                            |
| K-type thermocouple thermometer (JQ1032T)     | Ice storage tank temperature          | ±1.5 °C              | –50~220 °C                             |
| Rotor flowmeter (LZT-15G)                     | Refrigerant flow rate                 | 4 %                  | Flow velocity: 1~10GPM                 |
| Turbine flowmeter (LWYC-20)                   | Refrigerant and heat source flow rate | ±1 %                 | Flow velocity: 0.7~7 m <sup>3</sup> /h |
| Low constant temperature water bath (DC-0520) | Temperature                           | ±0.1 °C              | –5~95 °C                               |

temperatures of the refrigerant flowing through the ice storage tank, refrigerant flow rate, external water temperature of the ice storage coils, inlet and outlet water temperatures, and flow rate of the hot water tank. The equipment involved and measurement accuracy are detailed in Table 3.

The physical configuration of the experimental platform for the dynamic characteristics of the ice storage/melting process in the ice storage system is illustrated in Fig. 8.

### 3.2. Case introduction

In addition to experimental research, an extensive engineering demonstration is conducted. A comprehensive commercial office building located in Beijing, which has a total area of 96,983 m<sup>2</sup>, a height of 80 m, and comprises 22 floors, is selected to validate the practical

![Figure 8: Ice storage system experiment physical illustration. The image shows a laboratory setup with several large, black, rectangular ice storage tanks. These tanks are interconnected by a complex network of black and white pipes. Some pipes are wrapped in white insulation. Various valves, gauges, and a red container are also visible on the floor. The setup is located in a room with large windows in the background.](349ca0a6a9c2e2651a4deeeaf8be6da1_img.jpg)

Figure 8: Ice storage system experiment physical illustration. The image shows a laboratory setup with several large, black, rectangular ice storage tanks. These tanks are interconnected by a complex network of black and white pipes. Some pipes are wrapped in white insulation. Various valves, gauges, and a red container are also visible on the floor. The setup is located in a room with large windows in the background.

Fig. 8. Ice storage system experiment physical illustration.

![Figure 9: Exterior view of the case building. The image shows a tall, modern skyscraper with a glass and steel facade. The building has a distinctive stepped design, with each floor slightly offset from the one below it. The sky is blue with some light clouds. Some green trees are visible in the foreground at the base of the building.](e9b30aeb317ed964fa6de36804acf24c_img.jpg)

Figure 9: Exterior view of the case building. The image shows a tall, modern skyscraper with a glass and steel facade. The building has a distinctive stepped design, with each floor slightly offset from the one below it. The sky is blue with some light clouds. Some green trees are visible in the foreground at the base of the building.

Fig. 9. Exterior view of the case building.

**Table 4**  
Beijing Time-of-Use electricity pricing policy.

| Electricity price (RMB/kWh) | 1.293                      | 0.7673                                   | 0.2939     |
|-----------------------------|----------------------------|------------------------------------------|------------|
| Corresponding periods       | 10:00~15:00<br>18:00~21:00 | 7:00~10:00<br>15:00~18:00<br>21:00~23:00 | 23:00~7:00 |

performance of the proposed control method. The thermal conductivity of the walls is  $0.36 \text{ W}/(\text{m}^2 \cdot \text{K})$ , with normal working hours of the building from 8:00 to 21:00. Fig. 9 illustrates the exterior view of the case building. The current time-of-use electricity pricing in Beijing is detailed in Table 4.

The case building adopts a combined cooling mode of electric refrigeration and ice storage, which primarily consists of three dual-mode chiller units, four chilled water pumps, three ice storage tanks, and four thawing circulation pumps. The schematic diagram of the ice-storage HVAC system is shown in Fig. 10. The dual-mode refrigeration unit operates under the conditions of  $-1.64 \text{ }^\circ\text{C}/-5.0 \text{ }^\circ\text{C}$  during ice storage and  $10.1 \text{ }^\circ\text{C}/5.05 \text{ }^\circ\text{C}$  in air conditioning mode, utilizing ethylene glycol solution as the refrigerant. The total cooling capacity of the building's ice storage tank is 9250 kWh, with the ice coils providing a supply/return water temperature of  $3.3 \text{ }^\circ\text{C}/11 \text{ }^\circ\text{C}$ . The design temperature for the supply and return of chilled water at the building's air conditioning terminal is  $5 \text{ }^\circ\text{C}/12 \text{ }^\circ\text{C}$ . Additionally, the building adopts an entire energy storage cooling system with a 24-h cooling and releasing cycle. Hence, based on the design daily load distribution, during the off-peak electricity period (23:00~7:00), three dual-mode refrigeration units operate for ice storage. During the day, the dual-mode chiller units and the ice storage tank collaborate for cooling supply. The test parameters encompass indoor dry-bulb temperature, outdoor meteorological parameters, air conditioning load-side flow rates, and indoor equipment power consumption, within the testing period from July 24, 2020, to September 25, 2020. The data collection instruments and their precision employed in the case building are detailed in Table 5.

By conducting Pearson correlation analysis on factors influencing building cooling load and ranking the hourly cooling load correlations in descending order, five parameters, namely historical load values, lighting electricity consumption, outdoor dry-bulb temperature, water vapour pressure, and indoor dry-bulb temperature, are utilized as input variables for the LSTM. A total of 980 valid measured data samples are selected, with 75 % used for training and 25 % for validation. The error evaluation metrics of the model, NMBE and CV-RMSE, are 7.3 % and 11.9 %, respectively, both meeting the accuracy assessment criteria set by ASHRAE for hourly load values [49].

## 4. Results and discussion

### 4.1. Validation of time delay results

To investigate the dynamic response to the control signals in the ice storage system, experiments were conducted on the ice storage platform by dynamically adjusting the refrigerant flow rate during the ice melting process. Fig. 11 depicts a representative ice melting process at 5540 s, clearly capturing the variations in the outlet water temperature of the plate heat exchanger during the adjustment of the refrigerant flow rate.

As shown in Fig. 11, it can be inferred that at the initial moment of 



![Schematic diagram of the ice-storage HVAC system. The diagram shows a dual-mode chiller connected to a cooling tower. Glycol supply and return lines (orange and green) enter an ice storage tank containing three ice storage tanks. A valve controls the flow from the glycol supply to the ice storage tank. Glycol return lines from the ice storage tank pass through a heat exchanger before returning to the chiller. Chilled water supply and return lines (blue and red) from the chiller pass through a heat exchanger before being distributed to buildings. A water pump circulates the chilled water. A legend at the bottom identifies the line colors: Glycol supply (orange), Glycol return (green), Chilled water supply (blue), Chilled water return (red), Condenser water supply (purple), and Condenser water return (red).](e9314c83043183351ed74908e9bf2f90_img.jpg)

Schematic diagram of the ice-storage HVAC system. The diagram shows a dual-mode chiller connected to a cooling tower. Glycol supply and return lines (orange and green) enter an ice storage tank containing three ice storage tanks. A valve controls the flow from the glycol supply to the ice storage tank. Glycol return lines from the ice storage tank pass through a heat exchanger before returning to the chiller. Chilled water supply and return lines (blue and red) from the chiller pass through a heat exchanger before being distributed to buildings. A water pump circulates the chilled water. A legend at the bottom identifies the line colors: Glycol supply (orange), Glycol return (green), Chilled water supply (blue), Chilled water return (red), Condenser water supply (purple), and Condenser water return (red).

Fig. 10. Schematic diagram of the ice-storage HVAC system.

ice melting, the flow control valve transitions from a closed state to an open state, leading to a sudden increase in flow rate to  $1.35 \text{ kg/s}$ . The outlet water temperature of the plate heat exchanger does not immediately follow the rapid cooling and temperature reduction with the change in refrigerant flow rate. Instead, it gradually decreases and only starts stabilizing after  $125 \text{ s}$ , which indicates a significant time lag of approximately  $125 \text{ s}$  in the ice storage cooling system. In the middle of the ice melting process, by continuing to change the flow rate to  $2.28 \text{ kg/s}$ , the outlet water temperature of the plate heat exchanger does not immediately rise with the increased flow rate, which takes until  $280 \text{ s}$  to reach a relatively stable state again. The time lag during this period is approximately  $280 \text{ s}$ . Therefore, the experimental data shows that the delay time during the early stage of ice melting is shorter than that during the mid-melting stage. When the inner-fused ice storage coil has a diameter of DN15, a length of  $40 \text{ m}$ , is made of stainless steel, and the refrigerant flowing inside the pipe is a  $32\%$  ethylene glycol aqueous solution, with water as the phase-change medium outside the pipe, the time delays in the initial and middle stages of the melting process are calculated as  $115 \text{ s}$  and  $259 \text{ s}$ , respectively, based on Eqs. (32)–(38). The relative errors for the time lag in the early and mid-melting stages are only  $8.0\%$  and  $7.5\%$ , respectively.

## 4.2. Comparative analysis of dynamic response effects in ice storage tank cooling scenarios

### 4.2.1. Tracking performance

Under three distinct phase-change thermal stages, step signals are

introduced into the set trajectory of controlled parameters to compare the tracking performance of the ice storage tank during different ice melting periods. The initial controlled temperature is set at  $10^\circ \text{C}$ . Step signals are applied to the system temperature at different phases of external ice, namely solid, mushy, and liquid. The temperature is progressively decreased to  $8^\circ \text{C}$  and  $6^\circ \text{C}$ . The corresponding tracking performance is illustrated in Fig. 12.

As shown in Fig. 12(a), it is evident that during the initial melting phase, under PID control, the temperature takes an average of  $226 \text{ s}$  to stabilize, accompanied by a noticeable steady-state error. By advancing the output signal to eliminate pure time delay, the MPC controller exhibits a response time  $98 \text{ s}$  shorter than the PID controller when controlled parameters undergo a step change.

As shown in Fig. 12(b), it can be observed that during the mid-stage of ice melting, the response time under MPC control is  $47.1\%$  faster than the  $278 \text{ s}$  under the PID controller. It is worth noting that during the mid-term melting phase, when there is a step change in the controlled output, both PID and MPC controllers exhibit a deviation from the set point temperature. However, the deviation in the PID controller is more pronounced compared to that in the MPC controller.

As shown in Fig. 12(c), it can be observed that during the final stage of ice melting, when the temperature undergoes a step change from  $10^\circ \text{C}$  to  $8^\circ \text{C}$ , the MPC controller, with its advance action due to time delay compensation, allows the temperature to quickly follow the set point. In contrast, the outlet temperature under PID control begins to rise only after  $81 \text{ s}$  and takes  $244 \text{ s}$  to stabilize.

The two controllers exhibit significant differences in the average

**Table 5**  
Testing instruments and accuracy.

| Instrument model                                    | Measured parameters                                          | Measurement accuracy         | Measurement range                                                       |
|-----------------------------------------------------|--------------------------------------------------------------|------------------------------|-------------------------------------------------------------------------|
| Meteorological station (FT-QC7)                     | Outdoor dry bulb temperature                                 | ±0.2 °C                      | -50-100 °C                                                              |
|                                                     | Outdoor dew-point temperature                                | ±0.2 °C                      | -73-60 °C                                                               |
|                                                     | Outdoor relative humidity                                    | ±2 % (≤80 %)<br>±5 % (>80 %) | 0-100 %                                                                 |
|                                                     | Atmospheric pressure                                         | ±0.3 hPa                     | 450-1100 hPa                                                            |
| Digital anemometer (EC-9S)                          | Wind direction                                               | ±3°                          | 0-360°                                                                  |
| Spectral radiometer (TBQ-4-3, TBQ-4-5)              | Cumulative daily diffuse radiation                           | ≤±2 %                        | 0-1.4 kW/m <sup>2</sup>                                                 |
| Longwave radiometer (TBL-1)                         | Cumulative daily direct radiation                            | ±2 %                         | 0-2000W/m <sup>2</sup>                                                  |
| Solar total radiation Sensor (TBQ-2)                | Cumulative daily total radiation                             | ±2 %                         | 0-2000 W/m <sup>2</sup>                                                 |
| Ultrasonic flowmeter (TDS-100P)                     | Air condition load-side flow rate                            | ±1 %                         | Pipe diameter r: DN15mm-6000mm<br>Flow velocity: 0-32 m/s<br>-40-100 °C |
| Temperature data logger with Sensors (HOBO U12-014) | Air condition load-side supply and return water temperatures | ±0.4 °C                      | -                                                                       |
| Building energy consumption monitoring platform     | Building electricity consumption for various components      | ±2 %                         | -                                                                       |

![Figure 11: A dual-axis line graph showing the variations in the outlet temperature of the plate heat exchanger and the refrigerant flow rate during the ice melting control stage. The x-axis represents Time(h) from 12:43 to 14:24. The left y-axis represents the Refrigerant flow rate (kg/s) from 0 to 6. The right y-axis represents the Plate heat exchanger outlet temperature (°C) from 0 to 18. A solid blue line represents the outlet temperature, which fluctuates between approximately 3.5 and 4.5 °C. A dashed red line represents the refrigerant flow rate, which is mostly at 0 kg/s with a step increase to approximately 2.5 kg/s around 12:57. Vertical dashed lines indicate the start and end of the ice melting process. Annotations point to 'time delay during the initial ice-melting process' and 'time delay during the mid-phase ice-melting process'.](252ea48d02dce93965b91746fb376f35_img.jpg)

Figure 11: A dual-axis line graph showing the variations in the outlet temperature of the plate heat exchanger and the refrigerant flow rate during the ice melting control stage. The x-axis represents Time(h) from 12:43 to 14:24. The left y-axis represents the Refrigerant flow rate (kg/s) from 0 to 6. The right y-axis represents the Plate heat exchanger outlet temperature (°C) from 0 to 18. A solid blue line represents the outlet temperature, which fluctuates between approximately 3.5 and 4.5 °C. A dashed red line represents the refrigerant flow rate, which is mostly at 0 kg/s with a step increase to approximately 2.5 kg/s around 12:57. Vertical dashed lines indicate the start and end of the ice melting process. Annotations point to 'time delay during the initial ice-melting process' and 'time delay during the mid-phase ice-melting process'.

**Fig. 11.** Variations in the outlet temperature of the plate heat exchanger with refrigerant flow rate during the ice melting control stage.

response time required to return to a new steady state when the controlled parameters undergo a step change under different ice melting phases, as shown in Fig. 13.

Fig. 13 illustrates that, compared to the traditional non-optimized PID controller without handling time delay, the MPC controller reduces the average response time in the three thawing stages by 43.3 %, 47.1 %, and 50.5 %, respectively, improving response speed.

### 4.2.2. Accuracy performance

To quantitatively describe the improvement in the dynamic performance of the ice melting cooling process using different controllers, two indicators, namely, steady-state error within the regulation period and dynamic response relative error, are used to compare the proximity of

![Figure 12(a): A line graph showing the response curves of outlet water temperature during the early stage of ice melting. The x-axis is Time(s) from 0 to 1200. The y-axis is Outlet Water Temperature (°C) from 5 to 11. Three curves are shown: Setpoint trajectory (solid black line), MPC (dotted red line), and PID (dashed blue line). The setpoint steps up from 8 to 10 °C at 100s and down to 6 °C at 900s. The MPC controller follows the setpoint more closely than the PID controller, which shows a significant overshoot and delay.](79d61011f426d34fb542d86176482d2c_img.jpg)

Figure 12(a): A line graph showing the response curves of outlet water temperature during the early stage of ice melting. The x-axis is Time(s) from 0 to 1200. The y-axis is Outlet Water Temperature (°C) from 5 to 11. Three curves are shown: Setpoint trajectory (solid black line), MPC (dotted red line), and PID (dashed blue line). The setpoint steps up from 8 to 10 °C at 100s and down to 6 °C at 900s. The MPC controller follows the setpoint more closely than the PID controller, which shows a significant overshoot and delay.

(a) Response curves of outlet water temperature during the early stage of ice melting

![Figure 12(b): A line graph showing the response curves of outlet water temperature during the mid-stage of ice melting. The axes and legend are the same as in (a). The setpoint steps up from 8 to 10 °C at 100s and down to 6 °C at 900s. The MPC controller again shows a faster and more accurate response compared to the PID controller.](d7346a28f4ba53888f72648cface9da9_img.jpg)

Figure 12(b): A line graph showing the response curves of outlet water temperature during the mid-stage of ice melting. The axes and legend are the same as in (a). The setpoint steps up from 8 to 10 °C at 100s and down to 6 °C at 900s. The MPC controller again shows a faster and more accurate response compared to the PID controller.

(b) Response curves of outlet water temperature during the mid-stage of ice melting

![Figure 12(c): A line graph showing the response curves of outlet water temperature during the late stage of ice melting. The axes and legend are the same as in (a). The setpoint steps up from 8 to 10 °C at 100s and down to 6 °C at 900s. The MPC controller continues to outperform the PID controller in terms of response speed and accuracy.](44dae7af88a534136c7de6b942e7266c_img.jpg)

Figure 12(c): A line graph showing the response curves of outlet water temperature during the late stage of ice melting. The axes and legend are the same as in (a). The setpoint steps up from 8 to 10 °C at 100s and down to 6 °C at 900s. The MPC controller continues to outperform the PID controller in terms of response speed and accuracy.

(c) Response curves of outlet water temperature during the late stage of ice melting

**Fig. 12.** Response curves of plate heat exchanger outlet temperature at various phases of ice melting.

the real-time supply water temperature on the plate heat exchanger side to the set supply water temperature for the two controllers. The calculation results are shown in Table 6. Meanwhile, the dynamic response relative error is represented as the ratio of the integral average of the absolute error to the steady-state change value before and after the step change, as shown in Eq. (43).

$$\epsilon_r = \frac{\int_{t_1}^{t_2} |e| dt}{(t_2 - t_1) \Delta T} \quad (43)$$

Table 6 shows that the steady-state deviation of the controlled

![Bar chart showing Average Response Time (s) for PID and MPC controllers across three ice melting stages: Initial, Middle, and Final. PID values are 226, 278, and 325. MPC values are 128, 147, and 161.](b05a8a3551db31147979064952179990_img.jpg)

| Stage                        | PID (s) | MPC (s) |
|------------------------------|---------|---------|
| Initial stage of ice melting | 226     | 128     |
| Middle stage of ice melting  | 278     | 147     |
| Final stage of ice melting   | 325     | 161     |

Bar chart showing Average Response Time (s) for PID and MPC controllers across three ice melting stages: Initial, Middle, and Final. PID values are 226, 278, and 325. MPC values are 128, 147, and 161.

**Fig. 13.** Average response time in different ice melting stages for two controllers.

**Table 6**  
Deviations of response curves under different conditions for the two controllers.

| Operating condition                          | Controller | Maximum steady-state deviation (°C) | Dynamic relative deviation (%) |
|----------------------------------------------|------------|-------------------------------------|--------------------------------|
| Operating condition 1: melting initial stage | PID        | 0.096                               | 17.7 %                         |
|                                              | MPC        | 0.037                               | 5.19 %                         |
| Operating condition 2: melting middle stage  | PID        | 0.093                               | 18.3 %                         |
|                                              | MPC        | 0.063                               | 6.86 %                         |
| Operating condition 3: melting final stage   | PID        | 0.140                               | 19.2 %                         |
|                                              | MPC        | 0.046                               | 8.42 %                         |

system under MPC control is significantly smaller than that under PID control, which reduces the steady-state error by 61 %, 35 %, and 67 % in the three operating conditions, respectively. Additionally, the dynamic relative deviation under MPC is 12.5 %, 11.4 %, and 10.7 % smaller than that under PID control in the respective conditions. Clearly, the MPC controller with embedded time-delay compensation can rapidly and accurately achieve real-time control of systems with large inertia and time delays, thereby reducing the error.

## 4.3. Comparison of control effects in demand response scenarios

### 4.3.1. Control performance of system supply water temperature

Under demand response scenarios, the indoor set temperature is expected to be maintained within the comfort range. This study addresses this requirement by ensuring the stability of controlled water temperature through variable flow adjustment in the refrigerant loop, thereby minimizing fluctuations in the temperature set point. To visually assess the stability of the water temperature supply, Fig. 14 illustrates the controlled supply water temperature throughout a working day under the two control methods.

Fig. 14 shows that the dual-objective optimized MPC control method achieves the set point for the controlled water temperature more rapidly compared to the PID control method. The MPC approach showcases faster attainment of the temperature set point, followed by maintaining relatively stable conditions within a narrower fluctuation range. Although the average temperature between the two methods doesn't show a substantial variance, the MPC remarkably reduces the fluctuation amplitude of the controlled temperature by 60.9 % compared to the PID. Furthermore, the Root Mean Square Error (RMSE) of the supply water temperature under the PID control method is 0.88 °C. In contrast, the dual-objective optimized MPC control method achieves a temperature RMSE of only 0.42 °C, representing a 52.2 % reduction compared to the former. Both in terms of the temperature fluctuation range during the operation of the ice storage air conditioning and the accuracy of temperature tracking represented by the RMSE indicator, the dual-objective optimized MPC control method has demonstrated superior performance compared to the PID control method.

### 4.3.2. Matching of cooling supply and load demand

The control criteria for maintaining the regulated water temperature entail providing a stable water supply temperature amidst varying cooling load demands. A heightened control precision and swift response in maintaining the controlled temperature indicate that the cooling supply effectively aligns with the dynamic cooling load requirements. To visually assess the system's cooling performance under varying load conditions throughout different times of the day, Fig. 15 illustrates the system's cooling capacity and actual load demand curves during the period from 8:00 to 21:00 for both the proposed dual-objective optimization MPC control method and the PID control method.

As shown in Fig. 15, it can be observed that the dual-objective optimization MPC control method proposed in this study can quickly adjust the cooling capacity to the load demand value when following the

![Line graph comparing supply water temperature (°C) over time (h) for Set temperature, MPC, and PID. The Set temperature is a constant green line at 5°C. The MPC (red dotted line) and PID (blue dashed line) start at 10°C at 8:00 and drop to 5°C. The MPC curve is much flatter and closer to the set point than the PID curve, which shows significant fluctuations.](fe12ed09aa1cede0ba7e4c11715dcba4_img.jpg)

Line graph comparing supply water temperature (°C) over time (h) for Set temperature, MPC, and PID. The Set temperature is a constant green line at 5°C. The MPC (red dotted line) and PID (blue dashed line) start at 10°C at 8:00 and drop to 5°C. The MPC curve is much flatter and closer to the set point than the PID curve, which shows significant fluctuations.

**Fig. 14.** Comparison of temperature control effects under the two control methods.

![Figure 15: Simulation comparison of chilled water output tracking performance under the two control methods. The main plot shows Cooling Capacity (kW) on the y-axis (1500 to 3500) versus Time (h) on the x-axis (8:00 to 20:00). Three lines are plotted: Actual Load (solid black), MPC (dashed red), and PID (solid blue). The MPC line closely follows the Actual Load line, while the PID line shows a noticeable delay. An inset plot zooms in on the time period 18:45 to 19:30, showing a sharp drop in cooling capacity for both methods, with the MPC method reaching a lower minimum capacity faster than the PID method. Two red boxes highlight specific time intervals on the main plot where the MPC method shows better performance in terms of load tracking and reduction.](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 15: Simulation comparison of chilled water output tracking performance under the two control methods. The main plot shows Cooling Capacity (kW) on the y-axis (1500 to 3500) versus Time (h) on the x-axis (8:00 to 20:00). Three lines are plotted: Actual Load (solid black), MPC (dashed red), and PID (solid blue). The MPC line closely follows the Actual Load line, while the PID line shows a noticeable delay. An inset plot zooms in on the time period 18:45 to 19:30, showing a sharp drop in cooling capacity for both methods, with the MPC method reaching a lower minimum capacity faster than the PID method. Two red boxes highlight specific time intervals on the main plot where the MPC method shows better performance in terms of load tracking and reduction.

Fig. 15. Simulation comparison of chilled water output tracking performance under the two control methods.

load demand curve. In contrast, the PID control method shows a noticeable delay in the change of cooling capacity, resulting in a less effective response to changes in cooling load. The cumulative cooling load deviation for the MPC control method is calculated to be 294.9 kWh, which is 34.8 % lower than that of the PID control method, which is 463.2 kWh.

To quantitatively observe the load matching situation, Fig. 16 presents a comparison of the hourly average cooling supply and the predicted hourly cooling load demand curves.

As shown in Fig. 16, it can be observed that the relative error between the cooling supply of the proposed dual-objective optimization MPC control method and the actual cooling load demand throughout the day is only 2.1 %, while the PID control method has a relative error of 4.3 %. The cumulative hourly average cooling load deviation for the MPC control method, calculated in this study, is 629.13 kWh, which is 43.4 % lower than that of the PID control method, which is 1113.3 kWh.

### 4.3.3. Demand response benefits of energy consumption and operation cost

The engineering significance of demand response optimization strategies is determined by their ability to mitigate the peak electricity demand pressure on the grid. In this study, using full-load cooling with chillers only as the baseline scenario in the case building, the electricity load reduction capability, and economic benefits of the ice storage cooling system under demand response scenarios are evaluated for both control methods. Fig. 17 presents the cooling capacity allocation results, illustrating the optimization for economic efficiency using MPC for both the chiller and ice storage tank.

As shown in Fig. 17, it can be observed that under time-of-use electricity pricing, the total cost reduction achieved by the dual-objective optimized MPC control method is 11.7 %, with a 24.3 % reduction in costs during peak periods. Under the PID control, peak electricity consumption is reduced by 22.7 %, total daily costs decrease by 10.7 %, and costs during peak periods decrease by 22.7 %. The MPC control method saves an additional 8.5 % in electricity costs compared to the PID control method.

With the optimal strategy for hourly cooling load control instructions, the actual effects of demand response control differ between the two controllers. Fig. 18 illustrates the electricity consumption under the same demand response optimization control strategy for both the proposed dual-objective optimization MPC and PID control methods. The aim is to assess the electricity consumption reduction achieved by the combined cooling supply from both the chiller and ice storage tank.

As shown in Fig. 18, it can be observed that, compared to the baseline scenario, the PID control method and the proposed dual-objective

optimization MPC control method exhibit similar overall electricity consumption. However, there is a noticeable difference in the reduction amount. During the high electricity price periods highlighted in the two red boxes, the MPC control method reduced peak electricity consumption by 24.3 %, while the PID control method achieved a slightly lower reduction of 22.7 %. Compared to the PID control method, the MPC control method shifted an additional 6.5 % of the peak load. Moreover, the moment with the most significant difference in the reduction of electrical load between the two control methods is at 12:00. During this period, the PID control method only reduced by 126.91 kWh, while the MPC control method reduced by 156.88 kWh, resulting in an almost 30 kWh greater peak shaving effect.

# 5. Conclusion

Exploring the optimized control of ice storage systems is crucial for achieving peak load shaving, load leveling, and maintaining a stable electricity consumption profile. This study initiates with dynamic heat transfer modeling based on transfer functions and the representation of time delays, validating the model's accuracy through a self-constructed experimental setup. Subsequently, a dual-objective optimization MPC design is proposed for ice storage systems, taking into account both economic efficiency and dynamic response characteristics. The methodology is applied to a commercial office building for a comparative analysis of control accuracy, responsiveness, and economic efficiency. The key conclusions drawn from the investigation are as follows.

- (1) The nonlinear phase change process is linearized using the enthalpy method model, facilitating the establishment of dynamic heat transfer differential equations. Then, by employing the state-space method, dynamic heat transfer differential equations are transformed into transfer functions for application in system control.
- (2) A dynamic calculation method for the delay times of ice storage in terms of inertia and flow delay times is established. By embedding a time-delay compensation module in MPC and comparing it with traditional PID controllers, the MPC controller demonstrates a substantial reduction in the response time of the ice storage tank when subjected to step signals in the initial, middle, and final stages of melting by 43.3 %, 47.1 %, and 50.5 %, respectively. Moreover, following the attainment of stable step responses, the MPC control exhibits a remarkable decrease of 61 %, 35 %, and 67 % in steady-state errors during the three melting stages, in contrast to the PID control.

![Figure 16: Alignment of hourly cooling supply and building load demand under the two control methods. The figure consists of three subplots. The top-left subplot shows the cooling load (kW) from 8:00 to 21:00 for PID (blue area), MPC (yellow area), and Actual load demand (red line). The top-right subplot shows the cooling load (kW) from 8:00 to 21:00 for MPC (yellow area) and Actual load demand (red line). The bottom subplot shows the hourly cooling load mean deviation (kW) from 8:00 to 21:00 for PID (blue bars) and MPC (yellow bars).](177e8bc1c595b7fe3461d9919f87e044_img.jpg)

Figure 16 displays the alignment of hourly cooling supply and building load demand under two control methods: PID and MPC. The top-left plot shows the cooling load (kW) over time (h) for PID (blue area), MPC (yellow area), and the actual load demand (red line). The top-right plot shows the cooling load (kW) over time (h) for MPC (yellow area) and the actual load demand (red line). The bottom plot shows the hourly cooling load mean deviation (kW) over time (h) for PID (blue bars) and MPC (yellow bars).

Figure 16: Alignment of hourly cooling supply and building load demand under the two control methods. The figure consists of three subplots. The top-left subplot shows the cooling load (kW) from 8:00 to 21:00 for PID (blue area), MPC (yellow area), and Actual load demand (red line). The top-right subplot shows the cooling load (kW) from 8:00 to 21:00 for MPC (yellow area) and Actual load demand (red line). The bottom subplot shows the hourly cooling load mean deviation (kW) from 8:00 to 21:00 for PID (blue bars) and MPC (yellow bars).

Fig. 16. Alignment of hourly cooling supply and building load demand under the two control methods.

![Figure 17: Distribution of cooling capacity for chiller and ice storage tank. The figure is a dual-axis bar chart showing Refrigeration cooling capacity (kW) on the left y-axis and Electricity price (RMB) on the right y-axis, both over time (h) from 0 to 22. The legend indicates: Electricity price (red dashed line), Ice melting cooling capacity (yellow hatched bars), and Refrigerator cooling capacity (blue hatched bars).](fe753d01ad5fe6cf150018c958173c6d_img.jpg)

Figure 17 illustrates the distribution of cooling capacity for the chiller and ice storage tank. The chart shows the refrigeration cooling capacity (kW) on the left y-axis and the electricity price (RMB) on the right y-axis over a 24-hour period. The legend identifies the electricity price (red dashed line), ice melting cooling capacity (yellow hatched bars), and refrigerator cooling capacity (blue hatched bars).

Figure 17: Distribution of cooling capacity for chiller and ice storage tank. The figure is a dual-axis bar chart showing Refrigeration cooling capacity (kW) on the left y-axis and Electricity price (RMB) on the right y-axis, both over time (h) from 0 to 22. The legend indicates: Electricity price (red dashed line), Ice melting cooling capacity (yellow hatched bars), and Refrigerator cooling capacity (blue hatched bars).

Fig. 17. Distribution of cooling capacity for chiller and ice storage tank.

![Figure 18: Comparison of actual demand response electric load curtailment under MPC and PID. The chart shows Electrical Load (kWh) on the y-axis (0 to 900) and Time (h) on the x-axis (7 to 22). Three series are plotted: Base Line (purple), PID (blue), and MPC (yellow). Vertical dashed red lines indicate peak periods. The MPC series consistently shows the lowest load during these peak periods, demonstrating its effectiveness in demand response.](b3df5964338063224492c01f09e4fed6_img.jpg)

| Time (h) | Base Line (kWh) | PID (kWh) | MPC (kWh) |
|----------|-----------------|-----------|-----------|
| 7        | 0               | 0         | 0         |
| 8        | 610             | 610       | 620       |
| 9        | 640             | 640       | 650       |
| 10       | 680             | 680       | 680       |
| 11       | 720             | 230       | 220       |
| 12       | 770             | 640       | 610       |
| 13       | 770             | 630       | 650       |
| 14       | 680             | 650       | 630       |
| 15       | 780             | 780       | 790       |
| 16       | 740             | 740       | 750       |
| 17       | 680             | 680       | 690       |
| 18       | 730             | 680       | 670       |
| 19       | 690             | 580       | 590       |
| 20       | 530             | 190       | 180       |
| 21       | 470             | 470       | 480       |
| 22       | 0               | 0         | 0         |

Figure 18: Comparison of actual demand response electric load curtailment under MPC and PID. The chart shows Electrical Load (kWh) on the y-axis (0 to 900) and Time (h) on the x-axis (7 to 22). Three series are plotted: Base Line (purple), PID (blue), and MPC (yellow). Vertical dashed red lines indicate peak periods. The MPC series consistently shows the lowest load during these peak periods, demonstrating its effectiveness in demand response.

Fig. 18. Comparison of actual demand response electric load curtailment under MPC and PID.

(3) The dual-objective optimized MPC not only aligns cooling capacity precisely with real-time demand but also significantly reduces energy consumption during peak periods. Compared to the PID controllers, the dual-objective optimized MPC reduces the fluctuation magnitude and RMSE of the controlled supply water temperature by 60.9 % and 52.2 %, respectively. Additionally, it contributes to a reduction of peak electrical load and operating costs by 6.5 % and 8.5 %.

The simplified one-dimensional heat transfer model proposed in this study applies to internally melted ice storage tanks but will not be appropriate for encapsulated or externally melted ice storage tanks. The delay times differ for different building energy systems, but the time-delay calculation method and dual-objective optimization strategy are universal.

Future efforts may involve establishing different phase change materials' heat transfer models to formulate operational optimization strategies for diverse energy storage systems. Meanwhile, based on the method proposed in this study, intermittent renewable energy integration and grid frequency regulation can be utilized as optimization objectives to formulate operational optimization strategies for multi-energy coupled building energy systems, aiming to integrate renewable energy and enhance building sustainability.

# CRediT authorship contribution statement

**Yan Ding:** Writing – review & editing, Methodology, Conceptualization. **Long Hu:** Writing – original draft, Visualization. **Qiaochu Wang:** Formal analysis, Data curation. **Yang Bai:** Software, Investigation. **Zhe Tian:** Writing – review & editing. **Caixia Yang:** Resources.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Data availability

The authors are unable or have chosen not to specify which data has been used.

# References

- [1] Dalala Z, Al-Omari M, Al-Addous M, Bdour M, Al-Khasawneh Y, Alkasrawi M. Increased renewable energy penetration in national electrical grids constraints and solutions. *Energy* 2022;246:123361. <https://doi.org/10.1016/J.ENERGY.2022.123361>.
- [2] International Energy Agency. Global Alliance for Buildings and Construction. 2019 global status report for buildings and construction. International Energy Agency; 2019.
- [3] Sepehri A, Pavlak GS. Evaluating optimal control of active insulation and HVAC systems in residential buildings. *Energy Build* 2023;281:112728. <https://doi.org/10.1016/J.ENBUIBLD.2022.112728>.
- [4] Thiem S, Born A, Danov V, Vandersickel A, Schäfer J, Hamacher T. Automated identification of a complex storage model and hardware implementation of a model-predictive controller for a cooling system with ice storage. *Appl Therm Eng* 2017;121:922–40. <https://doi.org/10.1016/J.APPLTHERMALENG.2017.04.149>.
- [5] Cao H, Lin J, Li N. Optimal control and energy efficiency evaluation of district ice storage system. *Energy* 2023;276:127598. <https://doi.org/10.1016/J.ENERGY.2023.127598>.
- [6] Nie Z, Cheng W, Zhou G, Chen X, Yan CB, Gao F. Consistency guaranteed two-timescale decision and optimization of HVAC system with ice storage. *Int J Electr Power Energy Syst* 2022;141:108115. <https://doi.org/10.1016/J.IJEPES.2022.108115>.
- [7] Dai W, Xia W, Li B, Goh HH, Zhang Z, Wen F, et al. Increase the integration of renewable energy using flexibility of source-network-load-storage in district cooling system. *J Clean Prod* 2024;441:140682. <https://doi.org/10.1016/J.JCLEPRO.2024.140682>.
- [8] Ghaith FA, Onur Dag R. Performance and feasibility of utilizing solar powered ice storage system for space cooling applications. *Energy Convers Manag* X 2022;16:100319. <https://doi.org/10.1016/J.ECMX.2022.100319>.
- [9] Stefan-Kharicha M, Kharicha A, Wu M, al Zheng Y. Mathematical modelling of solidification and melting: a review You may also like Observation of flow regimes and transitions during a columnar solidification experiment the phase field technique for modeling multiphase materials I Singer-Loginova and H M Singer-Incorporation of fragmentation into a volume average solidification model, vol. 4; 1996.
- [10] Abu-Hamdeh NH, Salilih EM. A case study in the field of sustainability energy: transient heat transfer analysis of an ice thermal storage system with boiling heat transfer process for air-conditioning application. *Energy Rep* 2022;8:1034–45. <https://doi.org/10.1016/J.EGYR.2021.12.036>.
- [11] Zhang Y, Yuan G, Wang Y, Gao P, Fan C, Wang Z. Solidification of an annular finned tube ice storage unit. *Appl Therm Eng* 2022;212:118567. <https://doi.org/10.1016/J.APPLTHERMALENG.2022.118567>.
- [12] El Ouali A, Khattari Y, Lamrani B, El Rhafiki T, Zeraouli Y, Kousksou T. Apparent heat capacity method to describe the thermal performances of a latent thermal storage system during discharge period. *J Energy Storage* 2022;52. <https://doi.org/10.1016/J.est.2022.104960>.
- [13] Hu H, Argyropoulos SA. Mathematical modelling of solidification and melting: a review, vol. 4; 1996.
- [14] Huang Y, Sun Q, Yao F, Zhang C. Performance optimization of a finned shell-and-tube ice storage unit. *Appl Therm Eng* 2020;167:114788. <https://doi.org/10.1016/J.APPLTHERMALENG.2019.114788>.
- [15] Liu Z, Quan Z, Zhao Y, Jing H, Wang L, Liu X. Numerical research on the solidification heat transfer characteristics of ice thermal storage device based on a compact multichannel flat tube-closed rectangular fin heat exchanger. *Energy* 2022;239:122381. <https://doi.org/10.1016/J.ENERGY.2021.122381>.
- [16] Hamzeh HA, Miensari M. Numerical study of tube arrangement and fin effects on improving the ice formation in ice-on-coil thermal storage systems. *Int Commun*

- Heat Mass Tran 2020;113:104520. <https://doi.org/10.1016/J.ICHEATMASSTRANSFER.2020.104520>.
- [17] Chang C, Xu X, Guo X, Yu R, Rasakhodzhayev B, Bao D, et al. Experimental and numerical study during the solidification process of a vertical and horizontal coiled ice storage system. Energy 2024;298:131325. <https://doi.org/10.1016/J.ENERGY.2024.131325>.
- [18] Al-Saadi SN, Zhai Z. Modeling phase change materials embedded in building enclosure: a review. Renew Sustain Energy Rev 2013;21:659–73. <https://doi.org/10.1016/J.RSER.2013.01.024>.
- [19] Jin X, Hu H, Shi X, Zhou X, Yang L, Yin Y, et al. An improved heat transfer model for building phase change material wallboard. J Therm Anal Calorim 2018;134: 1757–63. <https://doi.org/10.1007/s10973-018-7357-x>.
- [20] Verbeke S, Audenaert A. Thermal inertia in buildings: a review of impacts across climate and building use. Renew Sustain Energy Rev 2018;82:2300–18. <https://doi.org/10.1016/J.RSER.2017.08.083>.
- [21] Jie P, Tian Z, Yuan S, Zhu N. Modeling the dynamic characteristics of a district heating network. Energy 2012;39:126–34. <https://doi.org/10.1016/J.ENERGY.2012.01.055>.
- [22] Zhao J, Shi L, Li J, Li H, Han Q. A model predictive control regulation model for radiant air conditioning system based on delay time. J Build Eng 2022;62:105343. <https://doi.org/10.1016/J.JOBME.2022.105343>.
- [23] Wang W, Yang C, Han J, Li W, Li Y. A soft sensor modeling method with dynamic time-delay estimation and its application in wastewater treatment plant. Biochem Eng J 2021;172:108048. <https://doi.org/10.1016/J.BEJ.2021.108048>.
- [24] Li Z, Wang P, Zhang J, Guan H. A model-free method for identifying time-delay characteristics of HVAC system based on multivariate transfer entropy. Build Environ 2022;217:109072. <https://doi.org/10.1016/J.BUILDENV.2022.109072>.
- [25] Li X, Zhao T, Zhang J, Chen T. Prediction control for indoor temperature time-delay using Elman neural network in variable air volume system. Energy Build 2017;154:545–52. <https://doi.org/10.1016/J.ENBUILD.2017.09.005>.
- [26] Su B, Wang S, Li W. Impacts of uncertain information delays on distributed real-time optimal controls for building HVAC systems deployed on IoT-enabled field control networks. Appl Energy 2021;300:117383. <https://doi.org/10.1016/J.APENERGY.2021.117383>.
- [27] Sun C, Liu Y, Cao S, Chen J, Xia G, Wu X. Identification of control regularity of heating stations based on cross-correlation function dynamic time delay method. Energy 2022;246:123329. <https://doi.org/10.1016/J.ENERGY.2022.123329>.
- [28] Sun X, Zheng W, Wang F, Wang H, Jiang Y, Bai Z, et al. Analysis of operation regulation on delay time in long-distance heating pipe systems for practical engineering. Sustainable Energy, Grids and Networks 2024;40:101526. <https://doi.org/10.1016/J.SEGAN.2024.101526>.
- [29] Li R, Zhang J. A transfer function model of lighting heat dissipation for detecting time-delay effect and dynamic cooling demand during the real-time operation of buildings. Energy Build 2022;254:111538. <https://doi.org/10.1016/J.ENBUILD.2021.111538>.
- [30] Gu Y, Chen L, Li C, Yin S. Multiple-model state-space system identification with time delay using the EM algorithm. J Franklin Inst 2024;361:107113. <https://doi.org/10.1016/J.FRANKLIN.2024.107113>.
- [31] Zhai J, Wang H, He Z. Fixed-time tracking control for high-order nonlinear systems with unknown time-varying input delay. Appl Math Comput 2023;452. <https://doi.org/10.1016/j.amc.2023.128027>.
- [32] Tang H, Yu J, Geng Y, Liu X, Lin B. Optimization of operational strategy for ice thermal energy storage in a district cooling system based on model predictive control. J Energy Storage 2023;62:106872. <https://doi.org/10.1016/J.EST.2023.106872>.
- [33] Candanedo JA, Dehkordi VR, Stylianou M. Model-based predictive control of an ice storage device in a building cooling system. Appl Energy 2013;111:1032–45. <https://doi.org/10.1016/J.APENERGY.2013.05.081>.
- [34] Jia L, Liu J, Chong A, Dai X. Deep learning and physics-based modeling for the optimization of ice-based thermal energy systems in cooling plants. Appl Energy 2022;322:119443. <https://doi.org/10.1016/J.APENERGY.2022.119443>.
- [35] Al-Aali I, Narayanaswamy A, Modi V. A novel algorithm for optimal equipment scheduling and dispatch of chilled water systems with ice thermal storage. Energy Build 2022;274:112422. <https://doi.org/10.1016/J.ENBUILD.2022.112422>.
- [36] Yan C, Wang F, Pan Y, Shan K, Kosonen R. A multi-timescale cold storage system within energy flexible buildings for power balance management of smart grids. Renew Energy 2020;161:626–34. <https://doi.org/10.1016/J.RENENE.2020.07.079>.
- [37] Nie Z, Cheng W, Zhou G, Chen X, Yan CB, Gao F. Consistency guaranteed two-timescale decision and optimization of HVAC system with ice storage. Int J Electr Power Energy Syst 2022;141:108115. <https://doi.org/10.1016/J.IJEPES.2022.108115>.
- [38] Cui B, Wang S, Yan C, Xue X. Evaluation of a fast power demand response strategy using active and passive building cold storages for smart grid applications. Energy Convers Manag 2015;102:227–38. <https://doi.org/10.1016/J.ENCONMAN.2014.12.025>.
- [39] Sephiri A, Nelson B. Analysis of round trip efficiency of thermal energy storage in Northern Arizona. 2019.
- [40] Sephiri A, Nelson B. Energy and emissions analysis of ice thermal energy storage in the western US. Energy Build 2019;202:109393. <https://doi.org/10.1016/J.ENBUILD.2019.109393>.
- [41] Liu C, Wang C, Yin Y, Yang P, Jiang H. Bi-level dispatch and control strategy based on model predictive control for community integrated energy system considering dynamic response performance. Appl Energy 2022;310:118641. <https://doi.org/10.1016/J.APENERGY.2022.118641>.
- [42] Fang X, Huang K, Feng G, Cai W, Song J, Li H, et al. Experimental and numerical research on the performance of a seasonal ice storage device in summer residential rooms of Northeast China. Sustain Cities Soc 2021;75. <https://doi.org/10.1016/j.scs.2021.103334>.
- [43] Jiang Z, Hlanze P, Cai J. Optimal predictive control of phase change material-based energy storage in buildings via mixed-integer convex programming. Appl Therm Eng 2022;215:118821. <https://doi.org/10.1016/J.APLTHERMALENG.2022.118821>.
- [44] Yao Y, Wang W, Huang M. A state-space dynamic model for vapor compression refrigeration system based on moving-boundary formulation. Int J Refrig 2015;60: 174–89. <https://doi.org/10.1016/J.IJREFRIG.2015.07.027>.
- [45] Prakash SA, Hariharan C, Arivazhagan R, Sheeja R, Raj VAA, Velraj R. Review on numerical algorithms for melting and solidification studies and their implementation in general purpose computational fluid dynamic software. J Energy Storage 2021;36:102341. <https://doi.org/10.1016/J.JEST.2021.102341>.
- [46] He H, Wang Y, Han R, Han M, Bai Y, Liu Q. An improved MPC-based energy management strategy for hybrid vehicles using V2V and V2I communications. Energy 2021;225. <https://doi.org/10.1016/j.energy.2021.120273>.
- [47] Cui M. District heating load prediction algorithm based on bidirectional long short-term memory network model. Energy 2022;254:124283. <https://doi.org/10.1016/J.ENERGY.2022.124283>.
- [48] Ding Y, Huang C, Liu K, Li P, You W. Short-term forecasting of building cooling load based on data integrity judgment and feature transfer. Energy Build 2023;283: 112826. <https://doi.org/10.1016/J.ENBUILD.2023.112826>.
- [49] 2023ANSI/ASHRAE. Standard 55, thermal environmental conditions for human occupancy, American society of heating, refrigerating and air-conditioning engineers. ASHRAE; 2020.