

# Modeling of two-stroke aviation piston engines for control applications

Hanjie Jiang<sup>ID</sup>, Ye Zhou, Hann Woei Ho and  
Elmi Abu Bakar

## Abstract

Two-stroke Aviation Piston Engines are multivariable systems with severe non-linear dynamics, making their modeling challenging for control engineers. Although many studies have been conducted on simplified modeling of four-stroke gasoline engines and large-scale two-stroke diesel engines for automobiles and ships, only a few have focused on the general modeling of small two-stroke aviation engines. Thus, extensive research on a general modeling method for two-stroke aviation engines is required. A general non-linear Mean Value Engine Model (MVEM) of two-stroke aviation piston engines is developed. Various parts of the model are represented by appropriate empirical equations that require little engine data and easily fit different engines. The objective is to develop a general and accurate method for rapid engine modeling that captures the main dynamics and can create control systems for two-stroke aviation piston engines. The model is validated using HIRTH-3203 and NU-57 measurement data, and the results show that the issues of fitting simplicity and general applicability are well addressed. Finally, the air-fuel ratio control based on the model predictive control method is carried out on the HIRTH-3203 MVEM, which demonstrates the effectiveness of the proposed MVEM in the controller design and evaluation. The proposed model may support the application of new control technologies, such as adaptive control and intelligent control, in the two-stroke aviation piston engine systems.

## Keywords

Aviation engine control, dynamic modeling, mean value engine model, model predictive control, two-stroke piston engines

Date received: 14 August 2022; accepted: 15 December 2022

Handling Editor: Chenhui Liang

## Introduction

Two-stroke aviation piston engines have the advantages of being compact, lightweight, producing a high-power output per unit displacement, having a simple structure, being convenient to use, and requiring little maintenance. With the rapid development of Unmanned Aerial Vehicles (UAVs) in recent decades, two-stroke aviation engines have been widely used.<sup>1,2</sup> The development of autopilot flight management has also promoted the automatic control technology for two-stroke aviation engines, such as the exploration of adaptive control,<sup>3</sup> health monitoring,<sup>4,5</sup> and intelligent control with online learning capabilities.<sup>6,7</sup> Dynamic engine models are widely used in the design of engine control systems,<sup>8</sup>

and higher requirements are put forward for the generality of engine modeling methods, in addition to the simulation fidelity of dynamic characteristics and stationary performances.

Engine modeling is an important tool for the development of engine control systems since it provides effective testing and simulation possibilities.<sup>9</sup> Various

School of Aerospace Engineering, Universiti Sains Malaysia, Nibong Tebal, Pulau Pinang, Malaysia

###### Corresponding author:

Ye Zhou, School of Aerospace Engineering, Universiti Sains Malaysia, Engineering Campus, Nibong Tebal, Pulau Pinang 14300, Malaysia.  
Email: zhouye@usm.my

![Creative Commons Attribution 4.0 International License logo](31cdb383e9cc2643a547f2500ed3cd08_img.jpg)

Creative Commons Attribution 4.0 International License logo

Creative Commons CC BY: This article is distributed under the terms of the Creative Commons Attribution 4.0 License (<https://creativecommons.org/licenses/by/4.0/>) which permits any use, reproduction and distribution of the work

without further permission provided the original work is attributed as specified on the SAGE and Open Access pages (<https://us.sagepub.com/en-us/nam/open-access-at-sage>).

engine modeling techniques have been reported to have been used to study engine steady-state performance and transient response in the current literature. These engine models include transfer function models, Mean Value Engine Models (MVEMs), computational fluid dynamics models, and zero-dimensional models.<sup>10</sup> Among them, the more complex modeling methods, such as computational fluid dynamics models, can more accurately represent the engine's working process but require a greater amount of calculation time and input data.<sup>11</sup> MVEM is a type of simple mathematical engine model which is characterized by a good balance between model accuracy and modeling simplicity. The time scale of MVEM is just adequate to describe accurately the change of the mean value of the most rapidly changing engine variable. This feature enables the model to predict engine dynamic performance in time, which is useful for engine control applications.<sup>12</sup> The MVEM has been widely used in the research of real-time simulation and control of automobile and ship engines. Most of these engines are four-stroke gasoline engines and large two-stroke diesel engines.<sup>10,13–16</sup>

The typical MVEM was proposed by Elbert Hendricks in 1990.<sup>12</sup> Since then, various MVEMs have been proposed, most of which are models for specific types of engine control systems.<sup>8,17</sup> MVEMs for given engines can achieve high accuracy, with static performance errors of less than 2%.<sup>10</sup> High precision is achieved by increasing the complexity of the model and customizing some parameters at the expense of the model's generality and simplicity. For example, calculating airflow into the crankcase requires several component parameters, such as the geometry size and elastic modulus of the reed valve.<sup>18</sup> However, these part parameters are difficult to obtain by engine users, which makes modeling more challenging. In the fuel injection dynamics module of those MVEMs, the fuel evaporation time constants and the fuel proportion placed on the intake manifold or close to the intake valve are often given by equations using high order polynomial to obtain more precise results.<sup>19</sup> These equations require a significant amount of data support during the modeling process. In addition, crankshaft torque, the main output of the crankshaft dynamic module, is often written as a function of ignition advance angle, air-fuel ratio, crankshaft rotation speed, and single-cycle intake of the cylinder in these custom MVEMs.<sup>18,20</sup> The parameter identification method often obtains the coefficients of these torque functions based on numerous test data.<sup>21,22</sup> Since the available sources of engine test data are scarce and engine air-borne testing is very expensive, a powerful alternative for developing controllers for aviation engines is to use control-oriented simulation models. Currently, it is

necessary to establish a general MVEM of two-stroke aviation engines for control applications.

This paper is aimed to establish a general model for various types of two-stroke aviation piston engines, which has the advantage of supporting rapid modeling. In the model layout, the crankcase and cylinder module is added to MVEM for two-stroke engines. The modules of the well-known MVEMs are screened according to their generality. In particular, the applicability of the two forms of the engine shaft dynamics module was analyzed and verified using the test data. These two types of shaft dynamics are based on the empirical equations of indicated shaft power and shaft torque. The verification results are combined with the characteristics of the two-stroke piston aviation engine to improve the model's accuracy. Specifically, modifications were made to the engine shaft dynamics module, crankcase, and cylinder module. These adjustments are physical and keep the model generic and easy to use. The shop trial data of two different two-stroke aviation piston engines further verified the revised general model. To further demonstrate the effectiveness and potential of the proposed MVEM in the control field, the air-fuel ratio (AFR) control simulation based on model predictive control (MPC) is carried out for HIRTH-3203. In the Simulink environment, HIRTH-3203 MVEM works well and completes a typical control simulation process.

The main contributions of the paper can be summarized as follows: (1) A general MVEM for a two-stroke piston engine was developed by using full empirical formulas to describe its four submodules. (2) The crankshaft dynamics module and scavenge model of the general model have been adjusted, which makes the MVEM close to the dynamics of a small-displacement two-stroke aviation engine. The relative mean error of the adjusted generic model is within 5%, with good accuracy to support the control study. And (3) the accuracy and potential of the MVEM in the control field are verified by the test data and the control simulation respectively, which is the prospect of the MVEM development in Hendricks.<sup>8</sup>

The rest of this paper is organized as follows: In Section 2, the general MVEM for the two-stroke engine is illustrated and the engine's four dynamic submodules are modeled separately. Sections 3 and 4 of this paper discuss the issue of model accuracy as a result of the simplifications and combinations of the MVEM configuration for two-stroke piston aviation engines. The potential of the proposed general MVEM for control applications is further demonstrated using the MPC-based AFR control simulation in Section 5. In Section 6 concluding remarks and perspectives are provided.

![Figure 1: Schematic diagram of the intake process of a two-stroke gasoline engine. The diagram shows the flow of air and fuel from the ambient environment through the intake manifold, past the throttle and reed valve, into the crankcase. The crankcase contains the piston and scavenging ports. The air-fuel mixture is then forced into the cylinder through the scavenging ports as the piston moves down. The cylinder is connected to the exhaust manifold, where the spent gases are expelled. Labels include: Ambient, P0, T0, Throttle, Reed Valve, Intake Manifold, Pm, Tm, Vm, Crankcase, Ps, Ts, Vs, Scavenging, Cylinder, P, T, V, Exhaust Manifold, Pe, Te, and Fuel Injection.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

Figure 1: Schematic diagram of the intake process of a two-stroke gasoline engine. The diagram shows the flow of air and fuel from the ambient environment through the intake manifold, past the throttle and reed valve, into the crankcase. The crankcase contains the piston and scavenging ports. The air-fuel mixture is then forced into the cylinder through the scavenging ports as the piston moves down. The cylinder is connected to the exhaust manifold, where the spent gases are expelled. Labels include: Ambient, P0, T0, Throttle, Reed Valve, Intake Manifold, Pm, Tm, Vm, Crankcase, Ps, Ts, Vs, Scavenging, Cylinder, P, T, V, Exhaust Manifold, Pe, Te, and Fuel Injection.

**Figure 1.** Schematic diagram of the intake process of a two-stroke gasoline engine. (The P, T, and V in the figure represent the pressure, temperature, and volume, respectively. Subscripts 0, m, s, and e refer to ambient air, intake manifold, crankcase, and exhaust manifold respectively).

## General model

## The generality of MVEM for two-stroke aviation engines

The classical MVEM has already demonstrated good generality as a research foundation. However, the MVEM's generality in this paper is limited to two aspects. The first is to build the general model structure of the two-stroke aviation piston engines based on the MVEMs of those four-stroke and large displacement two-stroke engines. For the general model's details, empirical equations from different MVEMs are selected for combination in this section. The second is to replace the sub-modules of the general model that can be improved in generality by adjusted simple empirical equations. These sub-modules frequently adopt customized expressions in those MVEMs established for specific engine control systems to ensure the high accuracy of the model. Replacing these customized expressions is important for model generalization.

## MVEM configuration for two-stroke piston engines

The implementation of MVEM combines the quasi-static and volumetric models, dividing the engine into several independent volumetric control units.<sup>23</sup> Figure 1 shows the structure diagram of a two-stroke engine. In this paper, the MVEM of a two-stroke engine is divided into four dynamic sub-modules: the dynamics of intake manifold sub-module, the crankcase and cylinder sub-module, the fuel injection dynamics sub-module, and the crankshaft dynamics sub-module.

*The dynamics of the intake manifold.* The ideal gas law and the conservation of air mass in the intake manifold are used to derive the manifold pressure state equation.<sup>8</sup>

$$\dot{p}_m = \frac{RT_m}{V_m}(\dot{m}_{at} - \dot{m}_{as}), \quad (1)$$

where the air mass flow into the engine port is  $\dot{m}_{as} = \dot{m}_{as}(n, p_m)$ , and  $n$  is the engine speed. The air mass flow past the throttle plate is  $\dot{m}_{at} = \dot{m}_{at}(\alpha, p_m)$ , and  $\alpha$  is the throttle opening angle.

The throttle air mass flow is given by the equation<sup>8</sup>

$$\dot{m}_{at}(\alpha, p_r) = \dot{m}_{atl} \frac{p_0}{\sqrt{T_0}} \beta_1(\alpha) \beta_2(p_r), \quad (2)$$

where  $\dot{m}_{atl}$  is the fitting constant,  $p_0$  is the ambient pressure, and  $p_r = p_m/p_0$ . The  $\beta_1$  and  $\beta_2$  equations are<sup>8</sup>

$$\beta_1(\alpha) = 1 - \alpha_1 \cos(\alpha) + \alpha_2 \cos^2(\alpha), \quad (3)$$

$$\beta_2(\alpha) = \begin{cases} \frac{1}{p_n} \sqrt{p_r^{p_1} - p_r^{p_2}}, & p_r \ge p_c \\ 1, & p_r < p_c \end{cases}, \quad (4)$$

$$p_c = \left( \frac{p_1}{p_2} \right)^{1/(p_2-p_1)}, \quad p_n = \sqrt{p_c^{p_1} - p_c^{p_2}}. \quad (5)$$

With  $\alpha_1 = 1.4073$ ,  $\alpha_2 = 0.4087$ ,  $p_1 = 0.4404$ ,  $p_2 = 2.3143$ ,  $p_n = 0.7404$ , and  $p_c = 0.4125$  as constants. A non-linear regression equation in terms of  $n$  and  $p_m$  is used in Hendricks' model<sup>8</sup> to determine the air mass flow into the engine port:

$$\dot{m}_{as} = -0.366 + 0.08979np_m - 0.0337np_m^2 + 0.0001n^2p_m. \quad (6)$$

*Crankcase and cylinder module.* It is different from a four-stroke engine, where the intake air passes through the intake manifold and enters the crankcase before entering the cylinder in a two-stroke engine, as shown in Figure 1. The Crankcase pressure state equation is derived using the conservation of air mass in the crankcase and the ideal gas law:

$$\dot{p}_s = \frac{RT_s}{V_s}(\dot{m}_{as} + \dot{m}_f - \dot{m}_{ac}) + \frac{P_s}{T_s}\dot{T}_s - \frac{P_s}{V_s}\dot{V}_s, \quad (7)$$

where the air mass flows passing through the cylinder  $\dot{m}_{ac} = \dot{m}_{ac}(n, p_s)$ , and  $\dot{m}_f$  is the fuel mass passing through the throttle plate with the air.

The speed-density equation can be used to calculate the mass flow of the mixture swept from the crankcase into the cylinder,

$$\dot{m}_{ac}(n, p_s) = \eta_v \frac{nV_d p_s i}{60\tau RT_s}, \quad (8)$$

where  $\eta_v$  is the engine's volumetric efficiency,  $i$  is the number of cylinders, and  $\tau$  is the stroke number (for a two-stroke engine,  $\tau = 2$ ). The volumetric efficiency  $\eta_v$  can be expressed as<sup>24</sup>:

$$\eta_v = 0.952 - \frac{0.075}{P_m}, \quad (9)$$

and the air mass induced per stroke is  $m_c$

$$m_c = \dot{m}_{ac}(n, p_s) \frac{60}{n}. \quad (10)$$

The temperature in the crankcase affects the engine's charging efficiency, which can be calculated using the following equation:

$$\dot{T}_s = \frac{\kappa}{\dot{m}_{as} + \dot{m}_f - \dot{m}_{ac}} [\dot{m}_{as} T_m - (\dot{m}_{ac} + \frac{1}{\kappa} \frac{d(\dot{m}_{as} + \dot{m}_f - \dot{m}_{ac})}{dt}) T_s], \quad (11)$$

the volume of the crankcase varies with piston displacement and can be expressed as:

$$V_s = V_z - \frac{\pi}{4} D^2 X, \quad (12)$$

where  $V_z$  is the crankcase volume with the piston at the top position,  $D$  is the cylinder diameter, and  $X$  is the piston displacement.

**Fuel injection dynamics.** Aquino<sup>25</sup> proposed the most popular and simple film flow model. This model keeps track of the fuel mass in the intake manifold and can be written as:

$$\dot{m}_{ff} = -\frac{m_{ff}}{\tau_{ff}} + \chi \dot{m}_{fi}, \quad (13)$$

$$\dot{m}_{fv} = 1 - \chi \dot{m}_{fi}, \quad (14)$$

$$\dot{m}_f = \dot{m}_{fv} + \frac{m_{ff}}{\tau_{ff}}. \quad (15)$$

The injected fuel flow is the input of this sub-model, and the engine intake valve fuel mass flow is the

output, which is assumed to be in the vapor phase. This model contains two parameters. The first is the time constant for fuel evaporation, and the second is the fuel proportion placed on the intake manifold or near the intake valves. They are determined by the model's various conditions and can be expressed as the following equations, respectively<sup>17</sup>:

$$\tau_{ff}(n, p_m) = 1.35(-0.672n + 1.68)(p_m - 0.825)^2 + (-0.06n + 0.15) + 0.56, \quad (16)$$

$$\chi(n, p_m) = -0.277p_m - 0.055n + 0.68. \quad (17)$$

**Crankshaft dynamics.** The crankshaft speed state equation can be written as<sup>8</sup>:

$$\dot{\omega} = \frac{H_u \eta_i \dot{m}_f(t - \tau_d)}{J\omega} - \frac{P_f + P_p + P_b}{J\omega}, \quad (18)$$

where  $P_f$  denotes the friction loss,  $P_p$  is pumping loss, and  $P_b$  denotes load.  $\eta_i$  is the thermal efficiency. The time delay  $\tau_d$  is the injection-torque time delay. The friction loss  $P_f$  and the pumping loss  $P_p$  can be expressed as follows<sup>12</sup>:

$$P_f(n) = n(1.673 + 0.272n + 0.0135n^2), \quad (19)$$

$$P_p(n, p_s) = n(-0.969 + 0.206n)p_s. \quad (20)$$

The thermal efficiency is composed of four components, as follows<sup>24</sup>:

$$\eta_i = \eta_{in} \eta_{ip} \eta_{ia} \eta_{ib}, \quad (21)$$

$$\eta_{in} = 0.558(1 - 0.392n^{-0.36}), \quad (22)$$

$$\eta_{ip} = 0.9301 + 0.2154p_s - 0.1657p_s^2, \quad (23)$$

$$\eta_{ia} = \begin{cases} -1.299 + 3.599\lambda - 1.332\lambda^2, & \lambda \le 1 \\ -0.0205 + 1.741\lambda - 0.745\lambda^2, & \lambda > 1 \end{cases}, \quad (24)$$

$$\eta_{ib} = 0.7 + 0.024(\theta - \theta_{mbt}) - 0.00048(\theta - \theta_{mbt})^2, \quad (25)$$

$$\theta_{mbt} = \min(\theta_1, \theta_2, 45), \quad (26)$$

$$\begin{cases} \theta_1 = 47.31p_s + 2.6214 + 4.7n, & n < 4.8 \\ \theta_2 = -56.55p_s + 79.9, & n \ge 4.8 \end{cases} \quad (27)$$

The engine torque can be expressed as<sup>26</sup>:

$$T_{eng} = \frac{H_u \eta_i \dot{m}_f(t - \tau_d)}{\omega} - \frac{P_f + P_p}{\omega}, \quad (28)$$

this crankshaft speed state equation is based on power and efficiency, and the model equipped with this module is referred to as Model-P in this paper.

The equation for crankshaft speed state can also be written directly in terms of the fuel flow and an algebraic equation<sup>8</sup>:

**Table 1.** HIRTH-3203 engine parameters.<sup>27</sup>

|                  |                                  |
|------------------|----------------------------------|
| Type             | Two-cylinder two-stroke (inline) |
| Displacement     | 625cm <sup>3</sup>               |
| Stroke           | 69mm                             |
| Bore             | 76mm                             |
| Max. Performance | 40.4kW at 5500rpm                |
| Max. Torque      | 72Nm at 5000rpm                  |
| Carburation      | Carburetor or fuel injection     |
| Cooling          | Fan cooling                      |
| Ignition system  | CDI                              |
| Weight           | 31kg                             |

$$\dot{\omega} = \frac{T_{eng}(m_c, \lambda, \theta, n)}{J} - \frac{T_l}{J}, \quad (29)$$

the engine torque can be given as below<sup>8</sup>:

$$T_{eng} = -181.3 + 379.36m_c + 21.91\lambda - 0.85\lambda^2 + 0.26\theta - 0.0028\theta^2 + 0.027n - 0.000107n^2 + 0.00048n\theta + 2.55\theta m_c - 0.05\theta^2 m_c, \quad (30)$$

In this paper, the model equipped with this module is referred to as Model-T.

## MVEM performance

The steady-state operation of the two-stroke aviation engine HIRTH-3203 was simulated by using both the Model-P and Model-T developed in the MATLAB-Simulink environment. The main engine characteristics and the required input data were extracted from the engine manufacturer's product data sheet.<sup>27</sup> The steady-state performance data for the engine were derived from engine shop trial measurements. Table 1 contains the primary engine parameters.

The simulations were run under steady-state operating conditions at 34%, 40%, and 46% of the engine throttle position to validate both models. These data were analyzed in the laboratory engine shop tests, as shown in Table 2. The engine torque and fuel consumption performances of both models and the engine shop tests are shown in Figures 2 and 3. Table 3 shows the percentage error between the shop trial data and both models' respective predicted engine performance parameters.

The most striking observation to emerge from the data comparison was:

- (i) The errors between the shop trial data and the initial general models combined with the empirical equations from those MVEMs are large. The performances of Model-P and

**Table 2.** Part steady-state test data of HIRTH-3203 engine.

| TPS (%) | Engine speed (rpm) | $T_{eng}$ (Nm) | $\dot{m}_f$ (g/s) |
|---------|--------------------|----------------|-------------------|
| 34      | 4000               | 28.8           | 1.508             |
| 34      | 4500               | 28.1           | 1.685             |
| 34      | 5000               | 30.1           | 2.163             |
| 34      | 5500               | 33.2           | 2.454             |
| 40      | 4000               | 34.1           | 1.762             |
| 40      | 4500               | 34.8           | 2.150             |
| 40      | 5000               | 34.1           | 2.624             |
| 40      | 5500               | 37.2           | 2.869             |
| 46      | 4500               | 38.6           | 2.435             |
| 46      | 5000               | 38.7           | 3.146             |
| 46      | 5500               | 41.8           | 3.357             |
| 46      | 6000               | 42.9           | 3.931             |

Model-T are insufficient to meet the requirements;

- (ii) The error of model-T is very large. Elbert Hendricks' empirical equation for crankshaft torque should have a suitable application range. It does not apply to the two-stroke aviation piston engine with small displacement;
- (iii) Although the performance of the general Model obtained initially is inaccurate, the torque equation of Model-P is based on energy and efficiency, and relevant physical theories support its generality. Some details of Model-P must be adjusted to improve its accuracy. In this paper, the adjusted model is referred to as Model-PA.

## General model adjustment and validation

The general model adjustment is implemented based on Model-P and includes changes to the engine scavenging and crankshaft dynamics models. The scavenging model was a component of the crankcase and cylinder module, which determined the quality of the fresh air and fuel mixture that ultimately entered the cylinder. The crankshaft dynamics model is adjusted primarily to correct power losses and the effective combustion fuel quality.

### Scavenge model adjustment

Volumetric efficiency is a critical metric for evaluating the engine air exchange process and performance. Compared to a four-stroke engine, the two-stroke engine's air exchange process exhibits the following characteristics.<sup>28–30</sup>

- i. The air change time of a two-stroke engine is relatively short, about half to one-third that of a four-stroke engine;

![Figure 2: Comparison of engine torque measurement and predictions from Model-T and Model-P at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Engine Torque (N*fm) on the y-axis versus Engine Speed (rpm) on the x-axis. The data series include Measurement (red squares), Model-P (blue triangles), and Model-T (green circles).](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 2 consists of three subplots (a), (b), and (c) comparing engine torque measurements and predictions from two models, Model-P and Model-T, at different throttle positions. The x-axis for all plots is Engine Speed (rpm) ranging from 3500 to 6000. The y-axis is Engine Torque (N\*fm).

| Engine Speed (rpm) | Measurement (N*fm) | Model-P (N*fm) | Model-T (N*fm) |
|--------------------|--------------------|----------------|----------------|
| 34% Throttle (a)   | 3900               | 29.5           | 35.5           |
|                    | 4500               | 28.5           | 33.5           |
|                    | 5500               | 33.5           | 41.5           |
| 40% Throttle (b)   | 4000               | 37.5           | 59.5           |
|                    | 5500               | 38.5           | 56.5           |
|                    | 6000               | 39.5           | 65.5           |
| 46% Throttle (c)   | 4500               | 39.5           | 50.5           |
|                    | 5500               | 41.5           | 67.5           |
|                    | 6000               | 43.5           | 67.5           |

Figure 2: Comparison of engine torque measurement and predictions from Model-T and Model-P at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Engine Torque (N\*fm) on the y-axis versus Engine Speed (rpm) on the x-axis. The data series include Measurement (red squares), Model-P (blue triangles), and Model-T (green circles).

**Figure 2.** Comparison of engine torque measurement and predictions from Model-T and Model-P: (a) 34% throttle position, (b) 40% throttle position, and (c) 46% throttle position.

![Figure 3: Comparison of fuel consumption measurement and predictions from Model-T and Model-P at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Fuel Consumption (g/s) on the y-axis versus Engine Speed (rpm) on the x-axis. The data series include Measurement (red squares), Model-P (blue triangles), and Model-T (green circles).](ac99eff233b8fe51d30f499e7413c345_img.jpg)

Figure 3 consists of three subplots (a), (b), and (c) comparing fuel consumption measurements and predictions from two models, Model-P and Model-T, at different throttle positions. The x-axis for all plots is Engine Speed (rpm) ranging from 3500 to 6000. The y-axis is Fuel Consumption (g/s).

| Engine Speed (rpm) | Measurement (g/s) | Model-P (g/s) | Model-T (g/s) |
|--------------------|-------------------|---------------|---------------|
| 34% Throttle (a)   | 4000              | 1.45          | 1.45          |
|                    | 5500              | 2.4           | 2.15          |
|                    | 6000              | 2.6           | 2.25          |
| 40% Throttle (b)   | 4000              | 1.75          | 1.55          |
|                    | 5500              | 2.8           | 2.35          |
|                    | 6000              | 3.0           | 2.55          |
| 46% Throttle (c)   | 4500              | 2.4           | 2.05          |
|                    | 5500              | 3.8           | 2.65          |
|                    | 6000              | 4.0           | 2.75          |

Figure 3: Comparison of fuel consumption measurement and predictions from Model-T and Model-P at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Fuel Consumption (g/s) on the y-axis versus Engine Speed (rpm) on the x-axis. The data series include Measurement (red squares), Model-P (blue triangles), and Model-T (green circles).

**Figure 3.** Comparison of fuel consumption measurement and predictions from Model-T and Model-P: (a) 34% throttle position, (b) 40% throttle position, and (c) 46% throttle position.

- ii. The two-stroke engine has a longer air exchange overlap time, and there is ventilation overlap throughout the scavenging process;
- iii. The loss of fresh air during the scavenging process of a two-stroke engine is more severe.

Therefore, a two-stroke engine's air exchange performance is significantly less than that of a four-stroke

**Table 3.** Errors of the initialized general models.

| State                 | Mean error (%) | Max error (%) |
|-----------------------|----------------|---------------|
| $T_{eng}$ (Model-P)   | 11.70          | 22.28         |
| $T_{eng}$ (Model-T)   | 50.94          | 90.91         |
| $\dot{m}_f$ (Model-P) | 15.95          | 28.19         |
| $\dot{m}_f$ (Model-T) | 18.72          | 35.11         |

![Figure 4: Volumetric efficiency simulation results of Model-P. The graph plots Volumetric efficiency (y-axis, 0.856 to 0.872) against Engine speed (rpm) (x-axis, 3500 to 6500). Three data series are shown: 34% throttle opening (red squares), 40% throttle opening (blue triangles), and 46% throttle opening (green circles). The 46% throttle opening series shows the highest efficiency, peaking around 0.872 at 4500 rpm, while the 34% series shows the lowest, peaking around 0.868 at 4000 rpm.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 4: Volumetric efficiency simulation results of Model-P. The graph plots Volumetric efficiency (y-axis, 0.856 to 0.872) against Engine speed (rpm) (x-axis, 3500 to 6500). Three data series are shown: 34% throttle opening (red squares), 40% throttle opening (blue triangles), and 46% throttle opening (green circles). The 46% throttle opening series shows the highest efficiency, peaking around 0.872 at 4500 rpm, while the 34% series shows the lowest, peaking around 0.868 at 4000 rpm.

**Figure 4.** Volumetric efficiency simulation results of Model-P.

engine. Scavenging loss of a two-stroke engine occurs throughout the operation process, comprised of three components: short-circuit loss, mixing loss, and overflow loss.

Additional exhaust components are frequently added to large displacement two-stroke engines to improve scavenging performance. However, small-displacement two-stroke aviation engines often have strict volume and mass restrictions. As a result, they cannot be equipped with additional exhaust devices.

As shown in Figure 4, the volumetric efficiency of the HIRTH-3203 engine calculated from the Model-P is greater than 0.85. However, previous studies<sup>31–33</sup> indicate that this value should be between 0.38 and 0.72 for a two-stroke engine, and the volumetric efficiency deduced from the test data also falls below 0.7.

The volumetric efficiency calculated by the Model-P does not match the performance characteristics of a small two-stroke engine. The calculated efficiency is significantly greater than the empirical value, which is likely one of the main reasons for the large positive deviation of engine model performance from engine shop tests.

A two-stroke engine operates similarly to a four-stroke engine in terms of intake, compression, combustion, expansion, and exhaust processes, except that a four-stroke engine requires two piston strokes to complete. In contrast, a two-stroke engine requires only one piston stroke. For a two-stroke engine, the volumetric efficiency can also be written as the scavenging efficiency  $\eta_s$ , which is the function of delivery ratio  $l_0(n, p_s)$ .<sup>31,33,34</sup> Figure 5 shows the volumetric efficiency of the HIRTH-3203 engine obtained from equation (31).

$$\eta_v = \eta_s = 1 - \exp^{-l_0(n, p_s)}. \quad (31)$$

### Crankshaft dynamics module adjustment

There is no individual intake and exhaust stroke for a two-stroke engine and its pump loss should be excluded

![Figure 5: Volumetric efficiency simulation results of Model-PA. The graph plots Volumetric efficiency (y-axis, 0.54 to 0.62) against Engine speed (rpm) (x-axis, 3500 to 6500). Three data series are shown: 34% throttle opening (red squares), 40% throttle opening (blue triangles), and 46% throttle opening (green circles). The 46% throttle opening series shows the highest efficiency, peaking around 0.61 at 6000 rpm, while the 34% series shows the lowest, peaking around 0.57 at 4500 rpm.](f6c63daa87b1f2bde4b871f3d540e85b_img.jpg)

Figure 5: Volumetric efficiency simulation results of Model-PA. The graph plots Volumetric efficiency (y-axis, 0.54 to 0.62) against Engine speed (rpm) (x-axis, 3500 to 6500). Three data series are shown: 34% throttle opening (red squares), 40% throttle opening (blue triangles), and 46% throttle opening (green circles). The 46% throttle opening series shows the highest efficiency, peaking around 0.61 at 6000 rpm, while the 34% series shows the lowest, peaking around 0.57 at 4500 rpm.

**Figure 5.** Volumetric efficiency simulation results of Model-PA.

from the calculation of mechanical loss of crankshaft power. Therefore, the crankshaft torque and rotation speed equations can be written as:

$$T_{eng} = \frac{H_u \eta_i \dot{m}_f (t - \tau_d)}{\omega} - \frac{P_f}{\omega}, \quad (32)$$

$$\dot{\omega} = \frac{H_u \eta_i \dot{m}_f (t - \tau_d)}{J\omega} - \frac{P_f + P_b}{J\omega}. \quad (33)$$

The friction loss  $P_f$  is expressed as equation (19). However, for many UAV engines with displacements of a few hundred milliliters or less, the friction loss power calculated using this equation is significantly greater than the maximum output power of the engine. Adjustment is made here based on the idea of the power loss ratio, and friction loss is denoted as:

$$P_f(n) = n(1.673 + 0.272n + 0.0135n^2) \frac{V_d}{1.27} \phi_{vp}, \quad (34)$$

where  $V_d$  is the engine displacement and  $\phi_{vp}$  is the relative power per liter coefficient. For two-stroke aviation engines, the value of is usually between 1.35 and 1.54. The fuel injection is typically performed in the intake manifold of a two-stroke aviation piston engine. In the process of the engine intake, the intake airflow is mixed with fuel, and the normalized air-fuel ratio is

$$\lambda = \frac{\dot{m}_{as}}{\dot{m}_f L_{th}}. \quad (35)$$

Model-P torque is calculated using the combustion energy and thermal efficiency of the fuel-air mixture entering the cylinder. Unlike in-cylinder direct injection engines, a proportion of the injected fuel is wasted during the scavenging process of a two-stroke engine due to short circuits and overflow loss. This must be considered in the two-stroke aviation engine model. Therefore, based on the equation (32) and the equation (33), the following results can be obtained by further adjustment

![Figure 6: Comparison of engine torque measurement and predictions from Model-T and Model-PA at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Engine Torque (N*m) on the y-axis versus Engine Speed (rpm) on the x-axis. The legend indicates: Measurement (red square), Model-P (blue triangle), and Model-PA (green asterisk).](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 6 consists of three subplots (a), (b), and (c) showing Engine Torque (N\*m) versus Engine Speed (rpm) for three throttle positions. The legend for all plots is: Measurement (red square), Model-P (blue triangle), and Model-PA (green asterisk).

| Engine Speed (rpm) | Measurement (N*m) | Model-P (N*m) | Model-PA (N*m) |
|--------------------|-------------------|---------------|----------------|
| 4000               | 28.5              | 30.0          | 28.0           |
|                    |                   | 29.0          | 27.5           |
|                    |                   | 30.0          | 26.5           |
| 4500               | 28.5              | 29.0          | 26.0           |
|                    |                   | 29.5          | 27.0           |
|                    |                   | 30.5          | 26.0           |
| 5000               | 30.0              | 32.5          | 29.0           |
|                    |                   | 33.0          | 29.5           |
|                    |                   | 34.0          | 30.0           |
| 5500               | 33.0              | 35.0          | 31.5           |
|                    |                   | 36.0          | 32.0           |
|                    |                   | 37.0          | 33.0           |

Figure 6: Comparison of engine torque measurement and predictions from Model-T and Model-PA at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Engine Torque (N\*m) on the y-axis versus Engine Speed (rpm) on the x-axis. The legend indicates: Measurement (red square), Model-P (blue triangle), and Model-PA (green asterisk).

**Figure 6.** Comparison of engine torque measurement and predictions from Model-T and Model-PA: (a) 34% throttle position, (b) 40% throttle position, and (c) 46% throttle position.

![Figure 7: Comparison of fuel consumption measurement and predictions from Model-T and Model-PA at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Fuel Consumption (g/s) on the y-axis versus Engine Speed (rpm) on the x-axis. The legend indicates: Measurement (red square), Model-P (blue triangle), and Model-PA (green asterisk).](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 7 consists of three subplots (a), (b), and (c) showing Fuel Consumption (g/s) versus Engine Speed (rpm) for three throttle positions. The legend for all plots is: Measurement (red square), Model-P (blue triangle), and Model-PA (green asterisk).

| Engine Speed (rpm) | Measurement (g/s) | Model-P (g/s) | Model-PA (g/s) |
|--------------------|-------------------|---------------|----------------|
| 4000               | 1.5               | 1.5           | 1.8            |
|                    |                   | 1.6           | 1.9            |
|                    |                   | 1.7           | 2.0            |
| 4500               | 1.7               | 1.7           | 2.0            |
|                    |                   | 1.8           | 2.1            |
|                    |                   | 1.9           | 2.2            |
| 5000               | 2.2               | 2.0           | 2.4            |
|                    |                   | 2.1           | 2.5            |
|                    |                   | 2.2           | 2.6            |
| 5500               | 2.4               | 2.2           | 2.8            |
|                    |                   | 2.3           | 2.9            |
|                    |                   | 2.4           | 3.0            |

Figure 7: Comparison of fuel consumption measurement and predictions from Model-T and Model-PA at three throttle positions: (a) 34%, (b) 40%, and (c) 46%. Each plot shows Fuel Consumption (g/s) on the y-axis versus Engine Speed (rpm) on the x-axis. The legend indicates: Measurement (red square), Model-P (blue triangle), and Model-PA (green asterisk).

**Figure 7.** Comparison of fuel consumption measurement and predictions from Model-T and Model-PA: (a) 34% throttle position, (b) 40% throttle position, and (c) 46% throttle position.

$$T_{eng} = \frac{H_u \eta_i (1 - k_f) \dot{m}_f (t - \tau_d)}{\omega} - \frac{P_f}{\omega}, \quad (36)$$

$$\dot{\omega} = \frac{H_u \eta_i (1 - k_f) \dot{m}_f (t - \tau_d)}{J\omega} - \frac{P_f + P_b}{J\omega}, \quad (37)$$

where  $k_f$  is the proportionality coefficient constant for fuel loss caused by short-circuiting and overflow losses during the scavenging process.

### Model-PA performance

The engine torque and fuel consumption performances from Model-P, Model-PA, and the engine shop tests are shown in Figures 6 and 7. Table 4 shows the percentage error between the predicted engine performance parameters and the respective shop trial data of Model-PA.

**Table 4.** Errors of the adjusted general model.

| State                  | Mean error (%) | Max error (%) |
|------------------------|----------------|---------------|
| $T_{eng}$ (Model-PA)   | 2.29           | 6.39          |
| $\dot{m}_f$ (Model-PA) | 3.89           | 7.71          |

The model's static performance calculation results demonstrate a significant improvement in the accuracy of the crankshaft torque and fuel consumption characteristics after adjustment. The average error in crankshaft torque performance is 2.29%, and the average error in fuel consumption performance is 3.89%. This error range indicates that the performance of Model-PA can meet the accuracy requirements for a general control-oriented model.

The throttle position, fuel injection, and load torque test data from Table 2 were entered into Model-PA to obtain engine speed under various operating conditions, as shown in Figure 8. The simulation results demonstrate that the engine speed calculated by Model-PA is consistent with the test data as in Table 2.

Figure 9 shows the dynamic simulation results for engine output speed when throttle position changes from 46% to 40%. According to the calculations in this work, the dynamic change in speed following throttle mutation is consistent with the actual dynamic change state of the engine, and the simulation results after stabilization are consistent with engine test data.

In addition, the fuel injection map for HIRTH-3203 is determined using Model-PA simulation results, as shown in Figure 10. The results demonstrate a high degree of agreement between the theoretical analysis and the test results. The fuel injection map can be used as the initial manifold absolute pressure (MAP) diagram, which is commonly used in the development of electronic control systems for gasoline engines.<sup>35,36</sup>

The Model-PA performance simulation results indicate that the adjusted general model of the two-stroke engine's power output accurately reflects the HIRTH-3203's static and dynamic characteristics. Model-PA is well suited for studying the power output and speed control algorithms of two-stroke aviation engines because the general model is composed of empirical formulas, significantly reducing the modeling workload.

### Generality validation

A smaller two-stroke kerosene aviation engine with a displacement of 0.057 L is selected for modeling to verify the generality of Model-PA. Compared to HIRTH-3203, the displacement difference is nearly tenfold, posing a challenge to the model's generality. The main parameters of the NU-57 engine are shown in Table 5.

Table 6 summarizes the results of the Model-PA and the engine shop tests.<sup>37</sup> As indicated by the static performance calculation results, the average relative error of crankshaft speed performance is approximately 2.35%, while the maximum relative error is 4.94%. The HIRTH-3203 and NU-57 engines have a large displacement gap and different cylinder layouts. Comparing performance simulation results to test data shows that the model has a high degree of generality for two-stroke aviation engine dynamic modeling.

## Model predictive control of the air-fuel ratio

In addition to the static accuracy and generality requirements, the model used for the preliminary study of a controller is also required to perform continuous and stable simulations within its operating envelope. In this section, the MVEM of the HIRTH-3203 engine will be used to design an air-fuel ratio (AFR)

![Figure 8: Simulation results of engine speed from Model-PA. The graph plots Engine speed (rpm) on the y-axis (1500 to 6500) against Time (s) on the x-axis (0 to 15). Five curves represent different throttle positions and operating points: 46% Throttle (purple, ~6000 rpm), 46% Throttle (orange, ~5500 rpm), 40% Throttle (blue, ~5000 rpm), 40% Throttle (green, ~4500 rpm), and 34% Throttle (red, ~4000 rpm). Each curve shows a rapid increase in speed followed by stabilization.](f09dce76b09a6f332810e5193cc39d56_img.jpg)

Figure 8: Simulation results of engine speed from Model-PA. The graph plots Engine speed (rpm) on the y-axis (1500 to 6500) against Time (s) on the x-axis (0 to 15). Five curves represent different throttle positions and operating points: 46% Throttle (purple, ~6000 rpm), 46% Throttle (orange, ~5500 rpm), 40% Throttle (blue, ~5000 rpm), 40% Throttle (green, ~4500 rpm), and 34% Throttle (red, ~4000 rpm). Each curve shows a rapid increase in speed followed by stabilization.

**Figure 8.** Simulation results of engine speed from Model-PA.

![Figure 9: Dynamic simulation results of engine output speed from Model-PA. The figure consists of four stacked plots over a time axis from 0 to 300 seconds. The top plot shows Throttle Position Signal (TPS) in percentage, which is a step function from 0% to 46% at 150 seconds. The second plot shows the fuel mass flow rate (m_fi) in grams per second (g/s), which follows the TPS step. The third plot shows the engine torque (T_f) in Newton-meters (Nm), which also follows the TPS step. The bottom plot shows the engine speed (n) in RPM, which starts at 2000 RPM, rises to 6000 RPM by 50 seconds, and then drops back to 2000 RPM by 150 seconds.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 9: Dynamic simulation results of engine output speed from Model-PA. The figure consists of four stacked plots over a time axis from 0 to 300 seconds. The top plot shows Throttle Position Signal (TPS) in percentage, which is a step function from 0% to 46% at 150 seconds. The second plot shows the fuel mass flow rate (m\_fi) in grams per second (g/s), which follows the TPS step. The third plot shows the engine torque (T\_f) in Newton-meters (Nm), which also follows the TPS step. The bottom plot shows the engine speed (n) in RPM, which starts at 2000 RPM, rises to 6000 RPM by 50 seconds, and then drops back to 2000 RPM by 150 seconds.

**Figure 9.** Dynamic simulation results of engine output speed from Model-PA.

![Figure 10: Simulation results of fuel injection map from Model-PA. This is a 3D surface plot showing the fuel mass flow rate per cycle (g) as a function of engine speed (RPM) and throttle opening (%). The x-axis represents throttle opening from 0 to 100%. The y-axis represents engine speed from 0 to 6000 RPM. The z-axis represents fuel mass flow rate per cycle from 0.01 to 0.05 g. The surface shows a peak in fuel injection at low throttle openings and high engine speeds.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 10: Simulation results of fuel injection map from Model-PA. This is a 3D surface plot showing the fuel mass flow rate per cycle (g) as a function of engine speed (RPM) and throttle opening (%). The x-axis represents throttle opening from 0 to 100%. The y-axis represents engine speed from 0 to 6000 RPM. The z-axis represents fuel mass flow rate per cycle from 0.01 to 0.05 g. The surface shows a peak in fuel injection at low throttle openings and high engine speeds.

**Figure 10.** Simulation results of fuel injection map from Model-PA.

**Table 5.** NU-57 engine parameters.<sup>37</sup>

| Type              | Two-cylinder two-stroke (Boxer) |
|-------------------|---------------------------------|
| Displacement      | 57cm <sup>3</sup>               |
| Stroke            | 28mm                            |
| Bore              | 36mm                            |
| Max. Performance  | 4kW                             |
| Max. Torque       | 4.6Nm                           |
| Max. Engine speed | 8500rpm                         |
| Carburation       | Carburetor                      |
| Cooling           | Air cooling                     |
| Compression ratio | 6.5 : 1                         |
| Weight            | 1.85 kg                         |

controller, which further demonstrates that the general MVEM established in this paper can support control

**Table 6.** Engine speed from Model-PA and tests of NU-57.

| TPS | $\lambda$ | $\theta$ | $T_{eng}$ | $n$ (Measure) | $n$ (Model-PA) |
|-----|-----------|----------|-----------|---------------|----------------|
| (%) | —         | (deg)    | (Nm)      | (rpm)         | (rpm)          |
| 19  | 1.10      | 9.6      | 1.52      | 3500          | 3327           |
| 28  | 1.07      | 12.9     | 2.06      | 4201          | 4324           |
| 35  | 1.07      | 16.3     | 2.67      | 4901          | 4967           |
| 40  | 0.97      | 19.2     | 3.12      | 5501          | 5399           |
| 51  | 0.95      | 21.1     | 3.58      | 5900          | 5970           |
| 64  | 0.93      | 24.0     | 3.90      | 6500          | 6621           |

![Figure 11: The block diagram of the AFR MPC structure. The diagram shows an MPC Controller block receiving a reference air-fuel ratio (lambda_exp(t)) and a throttle position signal (TPS(t)). The MPC Controller outputs the optimized fuel mass flow rate (m_fi(t)) to an MVEM Simulation block. The MVEM Simulation block also receives TPS(t) and outputs engine speed (n(t)), engine temperature (T_eng(t)), and air-fuel ratio (lambda(t)). A feedback loop labeled Z^1 connects the output lambda(t) back to the MPC Controller.](b10763be31553f31cbb795653b731a43_img.jpg)

Figure 11: The block diagram of the AFR MPC structure. The diagram shows an MPC Controller block receiving a reference air-fuel ratio (lambda\_exp(t)) and a throttle position signal (TPS(t)). The MPC Controller outputs the optimized fuel mass flow rate (m\_fi(t)) to an MVEM Simulation block. The MVEM Simulation block also receives TPS(t) and outputs engine speed (n(t)), engine temperature (T\_eng(t)), and air-fuel ratio (lambda(t)). A feedback loop labeled Z^1 connects the output lambda(t) back to the MPC Controller.

**Figure 11.** The block diagram of the AFR MPC structure.

applications. In this section, model predictive control (MPC) is an advanced process control technique widely adopted in the industry as an effective method to deal with large multi-variable constrained control problems.<sup>38–40</sup> In this section, MPC is engaged to optimize the injected fuel mass flow to keep tracing the desired AFR.

## Control system structure

Based on the obtained MVEM of HIRTH-3203 in section 4, a predictive control strategy was realized for the AFR control, which is illustrated in Figure 11. The throttle position (TPS), as one of the inputs of the MVEM, is set as a step signal. The other input,  $\dot{m}_{fi}$ , is optimized continually by the controller. The objective is to track and maintain the referenced air-fuel ratio,  $\lambda_{ref}$ , during throttle adjustment.<sup>41</sup>

MPC uses a model of the system to predict its future behavior and then optimizes a quadratic performance based on the prediction.<sup>42,43</sup> The main idea is to choose the control input by solving an optimal control problem repeatedly, aiming at minimizing a performance criterion over a future horizon. The cost function can be expressed as<sup>43</sup>:

$$Z(k) = \sum_{j=1}^{N_p} [\lambda_{ref}(k+j) - \hat{\lambda}(k+j)]^2 + \xi \sum_{j=0}^{N_c-1} [\dot{m}_{fi}(k+j) - \dot{m}_{fi}(k+j-1)]^2, \quad (38)$$



![Figure 12: A line graph showing the Throttle Position (TPS) over time. The x-axis represents 'Time' from 0 to 500, and the y-axis represents 'TPS' from 0.3 to 0.5. The TPS is constant at 0.3 until time 250, then jumps to 0.5 and remains constant until time 500.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 12: A line graph showing the Throttle Position (TPS) over time. The x-axis represents 'Time' from 0 to 500, and the y-axis represents 'TPS' from 0.3 to 0.5. The TPS is constant at 0.3 until time 250, then jumps to 0.5 and remains constant until time 500.

**Figure 12.** The step input of the throttle position.

![Figure 13: A line graph showing the fuel injection mass flow (dmf(g/s)) over time. The x-axis represents 'Time' from 0 to 500, and the y-axis represents 'dmf(g/s)' from 1 to 4.5. The mass flow starts at approximately 2.8 g/s, remains constant until time 250, then jumps to approximately 3.4 g/s and continues with minor fluctuations until time 500.](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

Figure 13: A line graph showing the fuel injection mass flow (dmf(g/s)) over time. The x-axis represents 'Time' from 0 to 500, and the y-axis represents 'dmf(g/s)' from 1 to 4.5. The mass flow starts at approximately 2.8 g/s, remains constant until time 250, then jumps to approximately 3.4 g/s and continues with minor fluctuations until time 500.

**Figure 13.** Fuel injection mass flow optimized by the MPC.

where  $k$  represents the current instance,  $\hat{\lambda}$  is the predicted AFR, and  $\xi$  is a control weighting factor that penalizes the excessive change of control inputs. The future horizon  $N_p$ , also called the prediction horizon, defines the number of samples one looks ahead. Similarly, the control horizon  $N_c$  defines the number of samples that the optimal inputs are calculated. MPC is engaged to solve the non-linear optimization problem and generates a series of optimal inputs:  $\hat{m}_f(k)$ ,  $\hat{m}_f(k+1)$ , ...,  $\hat{m}_f(k+N_p-1)$ .<sup>41</sup> The first control variable  $\hat{m}_f(k)$  will be used as the control input at this time instance. Here, the injected fuel mass flow is bounded within the region from 0.001 to 0.005 kg/s. The Quadratic Programming (QP) is used to acquire the accurate solution. The process of increasing the engine TPS from 0.3 to 0.5 was simulated in this section. The desired  $\lambda$  in TPS 0.5 state is set to 1.1, and a smaller desired  $\lambda$  0.95 is given in TPS 0.3 state.

# Simulation results

The HIRTH-3203 MVEM was used in this MPC demonstration. The MPC parameters are manually adjusted to determine the appropriate values by comparing the control performance. The parameters of the nonlinear optimization was chosen as  $N_p = 10$ ,  $N_c = 2$ ,

and  $\xi = 0.449$ . In the control simulation, the Gaussian noise  $\mathcal{N}(0, 0.01)$  was imposed into the measurement of the normalized AFR. The control results and the tracking curve for the desired AFR are shown in Figures 12 to 16. Figure 12 shows the step input of the throttle position. Figure 13 shows the fuel mass flow injected into the engine optimized by MPC. The tracking performance of the desired normalized AFR is illustrated in Figure 14. Figures 15 and 16 are the corresponding engine speed and torque, respectively.

The simulation results show that the HIRTH-3203 MVEM can be used to generate data for controller design and evaluation. In the simulation process, the HIRTH-3203 MVEM can characterize the main input-output characteristics in real-time operation. This simulation and control application demonstrate that this low-cost, fast construction and general MEVM can provide effective support for engine control engineers. These traits will be beneficial, especially in the controller design, evaluation, and comparison in an early stage.

# Conclusion

This paper establishes a general MVEM for two-stroke aviation engines based on the classical MVEMs of piston engines. Considering the convenience of application

![Figure 14: Tracking performance of the desired AFR (normalized). The graph plots lambda (normalized AFR) against Time (0 to 500). A solid red line represents the 'desired AFR', which is 1.0 until time 250 and then jumps to 1.2. A blue dashed line represents the 'output with measurement noise', which follows the desired AFR with high-frequency noise. The y-axis ranges from 0.9 to 1.25.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 14: Tracking performance of the desired AFR (normalized). The graph plots lambda (normalized AFR) against Time (0 to 500). A solid red line represents the 'desired AFR', which is 1.0 until time 250 and then jumps to 1.2. A blue dashed line represents the 'output with measurement noise', which follows the desired AFR with high-frequency noise. The y-axis ranges from 0.9 to 1.25.

**Figure 14.** Tracking performance of the desired AFR (normalized).

![Figure 15: The output of engine crankshaft speed during the control simulation. The graph plots Engine speed (RPM) against Time (0 to 500). The speed is constant at approximately 5400 RPM until time 250, then jumps to approximately 5850 RPM and remains constant. The y-axis ranges from 4200 to 6000 RPM.](252ea48d02dce93965b91746fb376f35_img.jpg)

Figure 15: The output of engine crankshaft speed during the control simulation. The graph plots Engine speed (RPM) against Time (0 to 500). The speed is constant at approximately 5400 RPM until time 250, then jumps to approximately 5850 RPM and remains constant. The y-axis ranges from 4200 to 6000 RPM.

**Figure 15.** The output of engine crankshaft speed during the control simulation.

![Figure 16: The output of engine crankshaft torque during the control simulation. The graph plots Engine torque (N·m) against Time (0 to 500). The torque is constant at approximately 33 N·m until time 250, then jumps to approximately 36 N·m and remains constant. The y-axis ranges from 20 to 40 N·m.](dd330f8b8f6c16eae20c3a676b4eb804_img.jpg)

Figure 16: The output of engine crankshaft torque during the control simulation. The graph plots Engine torque (N·m) against Time (0 to 500). The torque is constant at approximately 33 N·m until time 250, then jumps to approximately 36 N·m and remains constant. The y-axis ranges from 20 to 40 N·m.

**Figure 16.** The output of engine crankshaft torque during the control simulation.

in control research, the general MVEM entirely adopts empirical equations to build the engine sub-models, significantly reducing engine modeling time and cost.

The HIRTH-3203 engine was modeled in MATLAB-Simulink, and the model's details were adjusted based on comparisons between simulation results and test data. These details include the volumetric efficiency calculation, the pump and friction losses corrections, and the fuel flow correction. The adjusted model remains physical, generic, and easy to

use. It is apparent that the modified MVEM is suitable for the limited range of small-displacement two-stroke aviation engines and provides an effective tool for modeling. The simulation results of the modified MVEM are compared to the test results once more, demonstrating that the modified MVEM is reasonable and significantly improves accuracy.

Afterward, the modified general MVEM is used to model a small engine (NU-57) with a displacement of only 0.057 L. The modeling process for NU-57 is very

convenient, although NU-57 and HIRTH-3203 differ greatly in displacement, fuel type, and cylinder layout. The generality of the modified MVEM is verified by comparing the engine performance calculated by the model with the test data. Furthermore, the AFR control simulation based on the MPC method is carried out on the modified MVEM. The simulation results demonstrate the effectiveness of the proposed modeling method in control applications.

Although the general MVEM established in this paper is not as accurate as the model established for a specific engine, it will be extremely useful to control engineers during the engine modeling process, preliminary controller design, and evaluation. The current findings add to a growing body of literature on the MVEM applied in aviation piston engines and its generality. Future research should focus on investigating the control study of two-stroke engines based on this general MVEM, including but not limited to a control scheme based on neural network and machine learning methods.

## Declaration of conflicting interests

The author(s) declared no potential conflicts of interest with respect to the research, authorship, and/or publication of this article.

# Funding

The author(s) disclosed receipt of the following financial support for the research, authorship, and/or publication of this article: This work is sponsored by Malaysian Ministry of Higher Education with the Fundamental Research Grant Scheme (FRGS) [grant number FRGS/1/2020/TK0/USM/03/11].

## ORCID iD

Hanjie Jiang ![ORCID icon](e10db9d69cb0b265e01951fb48872059_img.jpg) <https://orcid.org/0000-0001-5514-7542>

# References

1. Cantore G, Mattarelli E and Rinaldini CA. A new design concept for 2-Stroke aircraft diesel engines. *Energy Proc* 2014; 45: 739–748.
2. Raviteja S, Ramakrishna PA and Ramesh A. Performance enhancement of a small two-stroke engine using nitromethane blends. *J Propulsion Power* 2019; 35: 520–529.
3. Wang Y, Shi Y, Cai M, et al. Optimization of air-fuel ratio control of fuel-powered UAV engine using adaptive fuzzy-PID. *J Franklin Inst* 2018; 355: 8554–8575.
4. Sheng J, Zeng Y, Liu G, et al. Determination of weak knock characteristics for Two-Stroke spark ignition UAV engines based on Mallat decomposition algorithm. *Math Probl Eng* 2021; 2021: 1–11.
5. Baoan L, Zhihua L and Xinjun L. Research of UAV engine fault prediction based on particle filter. In: *9th International Conference on Electronic Measurement Instruments*, 2009, pp.4-813–4-817. New York, NY: IEEE. DOI:10.1109/ICEMI.2009.5274711.
6. Yw A, Yan SA, Mc A, et al. Predictive control of air-fuel ratio in aircraft engine on fuel-powered unmanned aerial vehicle using fuzzy-RBF neural network. *J Franklin Inst* 2020; 357(13): 8342–8363.
7. Olcer FE. Development of a Neural-Network (NNET) Based engine model for a two-stroke engine of a rotary wing UAV. In: *AHS 70th Annual Forum*, 2014, vol. 70, pp. 1–7. AHS.
8. Hendricks E. Engine modelling for control applications: a critical survey. *Meccanica* 1997; 32(5): 387–396.
9. Dias JN, Violato GO and Martins CA. Dynamic model of a two-stroke glow engine from experimental data. *Proc IMechE, Part G: J Aerospace Engineering* 2012; 226(12): 1502–1512.
10. Theotokatos G, Guan C, Chen H, et al. Development of an extended mean value engine model for predicting the marine two-stroke engine operation at varying settings. *Energy* 2018; 143: 533–545.
11. Pasternak M, Mauss F, Sens M, et al. Gasoline engine simulations using zero-dimensional spark ignition stochastic reactor model and three-dimensional computational fluid dynamics engine model. *Int J Engine Res* 2016; 17: 76–85.
12. Hendricks E and Sorenson SC. Mean value modelling of spark ignition engines. *SAE Trans* 1990; 99: 1359–1373.
13. Rajamani R. Mean value modeling of SI and diesel engines. In: *Vehicle dynamics and control*. New York: Springer Science, 2012, 241–265.
14. Yum KK, Taskar B, Pedersen E, et al. Simulation of a two-stroke diesel engine for propulsion in waves. *Int J Nav Archit Ocean Eng* 2017; 9: 351–372.
15. Picerno M, Lee SY, Schaub J, et al. Co-simulation of multi-domain engine and its integrated control for transient driving cycles. *IFAC-PapersOnLine* 2020; 53: 13982–13987.
16. Li X, Liu Y, Shu H, et al. Disturbance Observer-based discrete sliding-mode control for a marine diesel engine with variable sampling control technique. *J Contr Sci Eng* 2020; 2020: 1–17.
17. Nekooei MJ, Priyanto JA and Dehghani Z. A review on engine MVEM models and AFR control methods to developing a new engine model and ziegler Nichols PID fuzzy controller: applied to SI engines. *J Appl Sci Res* 2013; 9: 6710–6725.
18. Chen LL, Wei MX and Yang HQ. Research on fuel injection control strategy of the miniature kerosene aero-engine based on mean value model. *J Univ Electron Sci Technol China* 2015; 44: 869–875.
19. Badmianto T, Firmansyah E and Cahyadi AI. Parameter identification of nonlinear system on combustion engine based MVEM using PEM. *Int J Inform Technol Electr Eng* 2018; 1: 107–116.
20. Crossley P and Cook J. A nonlinear model for drivetrain system development. In: *International Conference on Control*, 1991, vol. 2, pp. 921–925.

21. Chen L, Sun Q, Gao W, et al. Development of a small aviation two-stroke kerosene engine fuel injection controller. *Recent Pat Eng* 2021; 14: 610–619.
22. Liu GX and Liu Y. Simulation study on air-fuel ratio of gasoline engine based on the mean value engine model. *Dev Innov Mach* 2019; 4: 56–58.
23. Tuvesson S. *Tuning and validation of an MVEM for a turbocharged gasoline engine*. Linköping: Linkping University, 2009.
24. Hendricks E, Chevalier A, Jensen M, et al. Modelling of the intake manifold filling dynamics. *Soc Autom Eng* 1996; 1: 1–27.
25. Aquino CF. Transient A/F control characteristics of the 5 liter central fuel injection engine. *SAE Trans* 1981; 90: 1819–1833.
26. Hong M, Shen T, Ouyang M, et al. Torque observers design for Spark Ignition engines with different intake air measurement sensors. *IEEE Trans Control Syst Technol* 2011; 19: 229–237.
27. HIRTH ENGINES. 32 Series air cooled two-stroke engines. <https://hirthengines.com/2-stroke-engines/32-series/> (accessed 12 February 2022).
28. Oka T and Ishihara S. Relation between scavenging flow and its efficiency of a two-stroke cycle engine. *Trans Jpn Soc Mech Eng* 2008; 14: 257–267.
29. Galindo J, Serrano JR, Climent H, et al. Analysis of gas-dynamic effects in compact exhaust systems of small two-stroke engines. *Int J Automot Technol* 2007; 8: 403–411.
30. Stuecke P, Lehmann B and Heider M. Time resolved scavenging analysis for two-stroke engines. In: *Small engine technology conference & exposition*, 2007, vol. 32.
31. Oka T and Ishihara S. Relation between scavenging flow and its efficiency of a Two-Stroke cycle engine. *Bull JSME* 1971; 14: 257–267.
32. Hendricks E and Sorenson S. Mean value SI engine model for control studies. In: *1990 American control conference*, San Diego, CA, 1990, pp.1882–1887. New York, NY: IEEE. DOI: 10.23919/ACC.1990.4791054.
33. Sweeney M, Kenny R, Swann G, et al. Single cycle gas testing method for two-stroke engine scavenging. In: *SAE international congress and exposition*, No. 850178, 1985, pp.1–10. Warrendale, PA: SAE International.
34. Liu Y, Zhang F, Zhao Z, et al. Study on the synthetic scavenging model validation method of opposed-piston two-stroke diesel engine. *Appl Therm Eng Des Process Equip Econ* 2016; 104: 184–192.
35. Zhu T, Wei H and Zhao J. Simulation of the original injection MAP diagram of electronic-controlled gasoline engines based on MATLAB/SIMULINK. In: *2011 International conference on electrical and control engineering*, Yichang, China, 2011, pp.815–819. New York, NY: IEEE. DOI: 10.1109/ICECENG.2011.6057079.
36. Tamaki S, Sakayanagi Y, Sekiguchi K, et al. On-line feed-forward map generation for engine ignition timing control. *IFAC Proc Volumes* 2014; 47: 5691–5696.
37. Wang SF. *Research on control strategy of fuel injection for a two-stroke kerosene aviation piston engine*. Nanjing University of Aeronautics and Astronautics, 2015, pp.22–34.
38. Wang M, An A and Zhao Y. Model predictive control of microbial fuel cell based on Kalman state estimation. *J Phys Conf Ser* 2021; 1848: 012063.
39. Herceg M, Raff T, Findeisen R, et al. Nonlinear model predictive control of a turbocharged diesel engine. In: *2006 IEEE conference on computer aided control system design*, Munich, Germany, 2006, pp.2766–2771. New York, NY: IEEE. DOI: 10.1109/CACSD-CCA-ISIC.2006.4777076.
40. Sankar GS, Shekhar RC, Manzie C, et al. Fast calibration of a robust model predictive controller for diesel engine airpath. *IEEE Trans Control Syst Technol* 2020; 28: 1505–1519.
41. Zhai YJ and Yu DL. Neural network model-based automotive engine air/fuel ratio control and robustness evaluation. *Eng Appl Artif Intell* 2009; 22: 171–180.
42. Alessio A and Bemporad A. *A survey on explicit model predictive control*. Berlin, Heidelberg: Springer, 2009. 345–369.
43. Lee JH. Model predictive control: review of the three decades of development. *Int J Control Autom Syst* 2011; 9: 415–424.

# Appendix

## Notation

---

|                                                          |                                   |
|----------------------------------------------------------|-----------------------------------|
| $\alpha$ throttle plate angle                            | °                                 |
| $\chi$ fraction of fuel deposited on intake manifold     |                                   |
| $\dot{m}_{ac}$ air mass flow into cylinder               | $\text{kg s}^{-1}$                |
| $\dot{m}_{as}$ air mass flow into intake port            | $\text{kg s}^{-1}$                |
| $\dot{m}_{at1}$ fitting constant                         |                                   |
| $\dot{m}_{at}$ air mass flow past throttle plate         | $\text{kg s}^{-1}$                |
| $\dot{m}_{ff}$ fuel film mass flow                       | $\text{kg s}^{-1}$                |
| $\dot{m}_f$ injected fuel mass flow                      | $\text{kg s}^{-1}$                |
| $\dot{m}_{fv}$ fuel vapor mass flow                      | $\text{kg s}^{-1}$                |
| $\dot{m}_f$ fuel mass past the throttle plate            | $\text{kg s}^{-1}$                |
| $\eta_i$ thermal efficiency                              |                                   |
| $\eta_s$ scavenging efficiency                           |                                   |
| $\eta_v$ volumetric efficiency                           |                                   |
| $\kappa$ ratio of the specific heats                     |                                   |
| $\lambda$ normalized air/fuel mass ratio                 |                                   |
| $\omega$ crankshaft speed                                | $\text{s}^{-1}$                   |
| $\phi_{vp}$ relative power per liter coefficient         |                                   |
| $\tau$ stroke number                                     |                                   |
| $\tau_d$ injection-torque time delay                     | s                                 |
| $\tau_{ff}$ fuel film time constant                      | s                                 |
| $\theta$ spark advance                                   | deg BTDC                          |
| $\xi$ control weighting factor                           |                                   |
| $D$ cylinder diameter                                    | m                                 |
| $H_u$ fuel lower heating value                           | $\text{kJ kg}^{-1}$               |
| $i$ number of cylinders                                  |                                   |
| $J$ engine inertia                                       | $\text{kg m}^2$                   |
| $k_f$ proportionality coefficient constant for fuel loss |                                   |
| $l_0$ delivery ratio                                     |                                   |
| $L_{th}$ stoichiometric air/fuel ratio                   |                                   |
| $m_c$ air mass into cylinder per cycle                   | g                                 |
| $n$ engine speed                                         | rpm                               |
| $N_c$ control horizon                                    |                                   |
| $N_p$ prediction horizon                                 |                                   |
| $p_0$ ambient pressure                                   | bar                               |
| $p_m$ absolute manifold pressure                         | bar                               |
| $p_r$ pressure ratio                                     |                                   |
| $p_s$ absolute crankcase pressure                        | bar                               |
| $P_b$ engine load power                                  | kW                                |
| $P_f$ engine mechanical friction loss power              | kW                                |
| $P_p$ engine pumping loss power                          | kW                                |
| $R$ gas constant                                         | $\text{kJ kg}^{-1} \text{K}^{-1}$ |
| $T$ time                                                 | s                                 |
| $T_0$ ambient temperature                                | K                                 |
| $T_m$ intake manifold temperature                        | K                                 |
| $T_s$ intake crankcase temperature                       | K                                 |
| $T_{eng}$ engine output torque                           | Nm                                |
| $T_l$ engine load torque                                 | Nm                                |
| $TPS$ throttle position                                  |                                   |
| $V_d$ engine displacement                                | L                                 |
| $V_m$ manifold volume                                    | $\text{m}^3$                      |
| $V_s$ crankcase volume                                   |                                   |
| $V_z$ crankcase volume with the piston at the top        | $\text{m}^3$                      |
| $X$ piston displacement                                  | m                                 |
| $Z$ cost function of the MPC                             |                                   |