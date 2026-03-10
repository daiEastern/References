

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Journal of Engineering Research cover image](390120de4fe440c42fea8154fcaad334_img.jpg)

Journal of Engineering Research cover image

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Study on dynamic control system of tunnel variable air volume ventilation based on first-order delay and predictive compensation control model

Rongjun Xing<sup>a,b</sup>, Mingchuan Li<sup>c</sup>, Chao Dai<sup>d</sup>, Pai Xu<sup>a,b,\*</sup>, Jian Zhang<sup>c</sup>, Huichao Wang<sup>d</sup>,  
Wei Wang<sup>d</sup>, Zhengpan Hu<sup>a,b</sup>

<sup>a</sup> State Key Laboratory of Mountain Bridge and Tunnel Engineering, Chongqing Jiaotong University, Chongqing 400074, China

<sup>b</sup> School of Civil Engineering, Chongqing Jiaotong University, Chongqing 400074, China

<sup>c</sup> Yalong River Hydropower Development Co., Ltd, China

<sup>d</sup> China Construction Third Bureau Group Co., Ltd, China

## ARTICLE INFO

### Keywords:

Tunnel ventilation  
Process control  
Variable air volume  
Dynamic control model  
Transfer function

## ABSTRACT

Using a variable air volume ventilation system is an efficient way to save energy in the tunnel. To address the issues of low control parameter accuracy and high operating energy consumption, the transient flow field and ventilation resistance characteristics were analyzed using conservation equations, and the first-order delay mathematical model of tunnel ventilation control was established by taking tunnel and jet fan parameters into account. The airflow dynamic control model's related parameters and transfer function were also solved. The overshoot, steady value, and adjustment time of the control system were evaluated using simulation and experiment. In full-scale experiments, the required wind speed was converted into the frequency of the jet fans to achieve variable air volume ventilation control. The results show that the variable air volume ventilation control system has the characteristics of nonlinear, and the first-order delay time transfer function is related to the 1/2-th power of ventilation resistance and pressure. The control system performs well, and the response parameters are all within the error range. Moreover, the discussion results of the comparative tests also illustrated that the purpose of dynamic wind speed adjustment could be achieved through frequency conversion control.

## Introduction

With the development of road construction worldwide, the scale of large tunnel projects is increasingly growing. The number of tunnels is also growing, and ventilation dynamic control is crucial for the reliability optimization design of tunnel ventilation systems. A well-designed ventilation system of the tunnel, as a part of the improvement of driving comfort, makes not only a great contribution to driving safety, but also energy-saving for tunnel operation [1].

After the mode of ventilation was analyzed and the best mode established, the ventilation control scheme is a vital part of the ventilation system of tunnels to be studied when the design of ventilation proceeds. Thus, in order to separately provide satisfactory control performance for tunnel ventilation systems and tunnel operational environments, it is critical that jet fans are accurately and appropriately controlled [2,3]. The main purpose of controlling the airflow speed with a jet fan during normal operation is to ensure a lower concentration of vehicle exhaust gases inside the tunnel, such as CO or NO<sub>x</sub> [4,5].

Moreover, due to the significant part of electricity costs that is formed by the tunnel ventilation system, it is another equally important goal that reducing electricity costs.

In earlier work, some advanced control methodologies have mainly been studied for tunnel ventilation, and several control strategies that combine different models are applied for normal and emergency ventilation. A method has been proposed to simulate the dynamics of tunnel systems by spatially decomposing the traffic, ventilation, and exhaust tunnel subsystems, thereby providing a highly realistic and detailed behavior of the tunnel system [6]. A controller is designed that keeps pollutant levels below given limits inside the tunnel based on a static model of road tunnel [7]. Vehicle-by-vehicle simulations and validations based on traffic, ventilation, and pollution concentration were conducted for the two models by breaking them down into sub-models discretized in distinct one-dimensional spatial domains. A control scheme for longitudinal ventilation in highway tunnels was proposed [8]. It is used to estimate the value of pollutants such as traffic intensity, weather conditions and tunnel parameters. New air volume

\* Correspondence to: Chongqing Jiaotong University, No.66 Xuefu Rd., Nan'an Dist., Chongqing 400074, China.

E-mail address: [xu.pai@126.com](mailto:xu.pai@126.com) (P. Xu).

requirements are then calculated based on estimates of carbon monoxide, nitrite oxides and small particulate matter pollutants. The method utilizes one-dimensional force equations and fuzzy controllers to predict the number of jet fans to maintain good contaminant levels.

By using predictive fuzzy control methods and controlling jet fans, tunnel ventilation is optimized to maintain the permissible level of pollution and significantly reduce power consumption [9]. Due to the nonlinear complexity of the system, an optimally fuzzy control method by means of the genetic algorithm is redesigned [10]. It is superior to traditional fuzzy controllers in improving energy efficiency and maintaining allowable pollution limits. In addition to achieving the right pollutant levels, both methods have clear advantages in helping to reduce power consumption. The closed-loop algorithm is used to optimize the control ability of passing risk. The method takes into account not only the initial conditions such as wind speed and traffic conditions, but also their development [11]. As well as higher visibility, the key issue is about the ventilation system. A predictive control system model has been established and validated in the MATLAB environment for the design of highway tunnel ventilation systems [12]. This model is based on real ventilation system data for identification and utilizes an autoregressive moving average model describing pollutant concentration to control jet fans.

At present, it is more predominant than the traditional standard linear feedback controllers are mainly used in the tunnel ventilation control system, such as PID/PI controller algorithm. However, these traditional methods can no longer meet the demand for precise control of the ventilation system because when tuning the controller, a trade-off between reference tracking performance and interference suppression capability is necessary. A recent paper presents a nonlinear dynamic feedforward control scheme for longitudinal ventilation with an analytical nonlinear zero-dimensional airflow model [13]. It is demonstrated that the beneficial behavior of the presented method is applying to an Austrian tunnel. A control algorithm based on adaptive critical design is proposed to address the uncertainties associated with time-varying model parameters and unknown systems. A comprehensive dynamic model is developed, which takes into account the static and dynamic nonlinearity between pollutant concentration and jet velocity or air flow in the tunnel. The simulation results confirm its good regulation performance [14]. In order to optimize the tunnel ventilation control method, a method for operating ventilation of road tunnels is proposed with adaptive logic, compensating for deviations between mathematical models and actual measured data, and validated in the Prague Blanka Tunnel, Czech Republic [15]. The fuzzy controller is optimized by random global search particle swarm optimization algorithm, and the input and output fields of the fuzzy controller are dynamically adjusted to improve the tunnel environment parameters [16]. By adding a nonlinear unknown disturbance observer on the basis of the existing two-degree-of-freedom control scheme, a disturbance rejection system was established, thereby improving the disturbance resistance capability of the longitudinal tunnel ventilation system [17]. An adaptive optimal control method is proposed for HTV regulation based on Model Predictive Control to seek the optimal number of operating jet fans and obtain good control performance of pollutant concentration [18]. A nonlinear state feedback active disturbance rejection controller is developed, which is used to adjust the pollutant emission of long highway tunnels to provide compensation for the system [19].

To sum up, many scholars have made significant achievements in tunnel ventilation control research, providing important basis for accurate control and energy-saving methods of tunnel ventilation systems. However, the long tunnel ventilation system has the characteristics of high dynamic characteristics, large delay and inertia, which poses great challenges to the control of the ventilation system. Meanwhile, long tunnels have high air quality, heavy traffic, and long distance between tunnel entrances and exits, resulting in a very low rate of change in airflow velocity in the tunnel, especially when traffic jams and frequent

parking occur in the tunnel. Previous studies were conducted using different control schemes, which cannot effectively address this issue. Therefore, there is an urgent need to establish a dynamic ventilation control system that considers the dynamic behavior of airflow velocity inside the tunnel.

Based on the above, the purpose of this study is to establish a first-order delay time mathematical model for tunnel variable air volume ventilation control, and solve the parameters based on the transient characteristics of the ventilation flow field. The mathematical model takes into account power losses and ventilation resistance caused by jet fans and vehicle operation. Then, a dynamic control system for tunnel ventilation was established through predictive compensation control and parameter fuzzy self-tuning. Finally, various response parameters of the system were tested through simulation and full-scale experiments to verify that the performance of the control system can meet the ventilation requirements of tunnel operation. This provides a basis for the design of tunnel ventilation control systems to achieve efficient ventilation and energy-saving purposes.

## The basic of tunnel variable air volume ventilation control process

The three major equations of mass conservation, energy conservation, and momentum conservation are the theoretical basis for tunnel ventilation control modeling.

It is valid that airflow is incompressible when the Mach number is considerably low than 1 although the real airflow is compressible [20]. Generally, the value is not higher than 0.03, which is effective for the airflow velocity in the tunnel [21]. So, the study considers that it is incompressible in the following text.

### Continuity equation

As shown in Fig. 1, the simplest case of tunnel ventilation control system model is taken into account that longitudinally ventilated, uni-directional traffic and without any ramps.

In this model, the flow velocity represents the average value over the cross-section, and due to the assumptions of incompressibility and frictionless, the air density is constant.

For a given section of a tunnel with no entrance and exit ramps, according to the law of mass conservation under steady-state airflow conditions, the total air mass remains constant. In other words, in steady-state airflow, within the given cross-section of the tunnel, there is zero change in airflow at the entrance and exit. This means that the amount of air entering the tunnel cross-section is equal to the amount exiting. Then, in the steady-state airflow, the basic mathematical model of the tunnel ventilation control process can be described as follows [22]:

$$Q_1 = Q_2 \quad (1)$$

Where  $Q_1$  and  $Q_2$  are the mass flow rates of the first and second cross-sections of the given segment, kg/s, respectively.

$$\nu_1 A_1 = \nu_2 A_2 \quad (2)$$

where  $\nu_1$  and  $\nu_2$  are the airflow velocity of the 1st and 2nd cross-section of the given section respectively, m/s,  $A_1$  and  $A_2$  are the area of 1st and 2nd cross-section of the given segment respectively,  $m^2$ .

The change of pressure  $P$  in the tunnel reflects the energy storage process caused by the difference between  $Q_1$  and  $Q_2$ . It means that electric energy is converted into kinetic energy through the fans, and then converted into pressure energy through pressurization.

When the ventilation system is in a transient state, the difference between the inflow and outflow is not zero when the air in the tunnel is in an unstable state due to adjustment of the fan operating speed, or the strong influence of natural wind and traffic wind. The dynamic

![Diagram of a tunnel ventilation control system model. The tunnel is shown in cross-section with length L and height H. Two jet fans are located at the 1st and 2nd portals. Airflow Q1 and Q2 enter at velocities v1 and v2 through areas A1 and A2 respectively. Two cars are shown inside the tunnel. The diagram illustrates the simplest case of tunnel ventilation control system model.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

Diagram of a tunnel ventilation control system model. The tunnel is shown in cross-section with length L and height H. Two jet fans are located at the 1st and 2nd portals. Airflow Q1 and Q2 enter at velocities v1 and v2 through areas A1 and A2 respectively. Two cars are shown inside the tunnel. The diagram illustrates the simplest case of tunnel ventilation control system model.

Fig. 1. The simplest case of tunnel ventilation control system model.

mathematical model of airflow velocity can be obtained according to the law of the mass balance:

$$Q_1 - Q_2 = V \frac{dy}{dt} \quad (3)$$

where  $V$  is the volume of the tunnel clearance,  $\text{m}^3$ ,  $\gamma$  represents the density of air in the tunnel,  $\text{kg}/\text{m}^3$ .

### Bernoulli equation

#### (1) Generalized Bernoulli equation

For incompressible and unsteady flow, the generalized Bernoulli equation is expressed for different forms [23]. The pressure balance equation can be obtained:

$$\rho L \frac{dv}{dt} = \Delta p \quad (4)$$

where  $L$  is the length of the given section of the tunnel,  $\text{m}$ ,  $\rho$  is the density of the air,  $\text{kg}/\text{m}^3$ ,  $\Delta p$  describes the total change of the given section,  $\text{Pa}$ ,  $v$  denotes the airflow velocity,  $\text{m}/\text{s}$ ,  $dv/dt$  represents the change of the air velocity,  $\text{m}/\text{s}^2$ .

The term  $\Delta p$  in Eq. (4) on the right-hand side indicates the total pressure change in the given section of the tunnel,  $\text{Pa}$ . It can be divided into pressure change due to running jet fans  $\Delta p_j$ ,  $\text{Pa}$ , piston effect of vehicles  $\Delta p_b$ ,  $\text{Pa}$ , changes in tunnel geometry  $\Delta p_f$  and pressure losses caused by air friction  $\Delta p_b$ ,  $\text{Pa}$ .

According to the force characters of airflow in the tunnel, the equilibrium equations is as follows:

$$\rho A_t L \frac{dv}{dt} = F_j + F_t + F_f + F_l \quad (5)$$

where  $A_t$  is the cross-section area of the given section,  $\text{m}^2$ ,  $F_j$  denotes the thrust of jet fans,  $N$ ,  $F_t$  represents the force of vehicles passing through the tunnel,  $N$ ,  $F_f$  denotes the force of local area losses,  $N$ ,  $F_l$  is the frictional resistance along the longitudinal in tunnel,  $N$ .

In this study, due to the altitude change at tunnel portals is not significant, the authors neglect the pressure change of stack effect caused by temperature differences at tunnel portals. Similar to the stack effect, compared to the piston effect or air friction, it is negligible pressure change that pressure changes caused by wind at tunnel portals.

#### (2) Extended Bernoulli equation

In many references to other articles and books [24–28], the Extended Bernoulli equation is derived for incompressible and unsteady flow. It can be expressed in different forms and the authors use the form as Eq. (6) for our study purpose.

As shown by Eq. (6), the airflow velocity in a tunnel can be described using the mathematical model defined by the Extended Bernoulli equation. Substituting  $F_j$ ,  $F_b$ ,  $F_f$ , and  $F_l$  into Eq. (5) and thus it is expressed into the following form:

$$\rho A_t L \frac{dv}{dt} = N_j \rho k_j A_f v_j \left( v_j - v \right) + \frac{\rho}{2} K L A_{vm} \left( v_v - v \right) |v_v - v| - \frac{\rho}{2} A_t \left( \lambda \frac{L}{d_e} + \zeta_{in} + \zeta_{out} \right) v^2 \quad (6)$$

The first sum term in Eq. (6) on the right-hand side indicates airflow velocity of jet fans, where  $N_j$  is the number of all the running jet fans,  $k_j$  denotes the pressure coefficient of the jet fan,  $A_f$  represents the cross-sectional area at the outlet of jet fan,  $\text{m}^2$ ,  $v_j$  describes the wind flow velocity at the outlet of jet fan,  $\text{m}/\text{s}$ ,  $v$  is the airflow velocity in the tunnel,  $\text{m}/\text{s}$ .

The second sum term in Eq. (6) on the right-hand side characterizes the pressure change due to the piston effect of vehicles, where  $v_v$  is the speed of vehicle passing through the tunnel,  $\text{m}/\text{s}$ ,  $A_{vm}$  represents ratio of vehicle windward area to tunnel section area,  $\text{m}^2$ ,  $KL$  represents the number of vehicles inside the tunnel.

The last sum term in Eq. (6) on the right-hand side describes the total losses which decelerate the airflow, where  $\lambda$  is the wall friction resistance coefficient, which considers obstructing installations in the tunnel,  $d_e$  is the equivalent diameter of the tunnel section,  $\text{m}$ , the factors  $\zeta_{in}$  and  $\zeta_{out}$  represent the influx and outflux losses respectively for the airflow entering into or exiting from the tunnel.

## The establishment of dynamic control system in tunnel ventilation

The accuracy and reasonableness of the mathematical model of the tunnel ventilation system play a decisive role in the controller performance. So, it is also vital that the establishment of the airflow dynamics control model and clarify its characteristics.

### First-order delay control model of the variable air volume ventilation

Under the assumption of an ideal airflow in the tunnel, it is frictionless and incompressible. Then, the equation can be obtained as follows. Arnaud et al. [29]:

$$pV' = R_0 T_0 \quad (7)$$

where  $p$  is the absolute pressure of the air in the tunnel,  $\text{Pa}$ ,  $V'$  represents air specific volume,  $\text{m}^3$ ,  $R_0$  describes gas constant,  $T_0$  denotes the absolute temperature of the air in the tunnel,  $\text{K}$ .

According to the gas characteristics, the following relationship can be obtained:

$$\gamma = \frac{1}{V'} = \frac{p}{R_0 T_0} \quad (8)$$

$$\frac{dy}{dt} = \frac{1}{R_0 T_0} \frac{dp}{dt} \quad (9)$$

$$Q_1 - Q_2 = V \frac{dy}{dt} = \frac{V}{R_0 T_0} \frac{dp}{dt} \quad (10)$$

Rewritten into an incremental expression, the following equation is

obtained:

$$\Delta Q_1 - \Delta Q_2 = \frac{V}{R_0 T_0} \frac{d\Delta p}{dt} \quad (11)$$

Eq. (11) Simplification:

$$k_2 \Delta f - \frac{\Delta p}{R_2} = C \frac{d\Delta p}{dt} \quad (12)$$

Taking the Laplace transform of the Eq. (12), it can be rewritten as:

$$\frac{P(s)}{F(s)} = \frac{k_2 R_2}{1 + C \cdot R_2 s} = \frac{K}{1 + Ts} \quad (13)$$

where  $K$  is the magnification factor,  $T$  is the time constant,  $\tau$  is the delay time. And  $K$  and  $T$  can be calculated using the following equation:

$$K = k_2 \cdot R_2 \quad (14)$$

$$T = C \cdot R_2 \quad (15)$$

From this, the first-order delay time transfer function of the system can be obtained as:

$$G_p(s) = \frac{K}{1 + Ts} e^{-\tau s} \quad (16)$$

### The time delay characteristic of the dynamic control system

When jet fans are driven with invert, the transient-state model of airflow is used, one can put  $dv/dt=0$ . Now, the values of both  $F_j$  and  $F_t$  depend on airflow velocity in the tunnel. Then, for the induced wind speed in the tunnel, Eq. (6) is to form the simplified equation which can be rewritten as:

$$\frac{dv}{dt} = av^2 + bv + c \quad (17)$$

Eq. (17) is a nonlinear first-order ordinary differential equation with variable coefficients. In order to prove the nonlinearity of the system, two steps should be carried out.

For one, the non-uniformity of the system. Considering the system of the Eq. (6) with signal  $e(t)$  acting on it and the response  $V(t)$ , the system is expressed into the following form:

$$\frac{dv(t)}{dt} - av(t)^2 + bv(t) + c = e(t) \quad t > 0 \quad (18)$$

Multiplying both sides of the Eq. (18) by  $A_t$ , it can be rewritten as:

$$A_t \left( \frac{dv(t)}{dt} - av(t)^2 + bv(t) + c \right) = A_t e(t) \quad t > 0 \quad (19)$$

When  $A_t e(t)$  acts on the system, if the system of the Eq. (18) is linear:

$$A_t \frac{dv(t)}{dt} - aA_t^2 v(t)^2 + bA_t v(t) + c = A_t e(t) \quad t > 0 \quad (20)$$

Obviously, Eq. (19) contradicts to Eq. (20), it indicates that the system does not satisfy the uniformity.

For another, the non-additivity of the system. Considering the system of the Eq. (6) with two signals  $e_1(t)$  and  $e_2(t)$  acting on it and the response  $V_1(t)$  and  $V_2(t)$  respectively, the system is expressed into the following form:

$$\frac{dv_1(t)}{dt} - av_1(t)^2 + bv_1(t) + c = e_1(t) \quad t > 0 \quad (21)$$

$$\frac{dv_2(t)}{dt} - av_2(t)^2 + bv_2(t) + c = e_2(t) \quad t > 0 \quad (22)$$

Adding these two equalities together and the following equation is obtained:

$$\frac{d}{dt} [v_1(t) + v_2(t)] - a[v_1(t)^2 + v_2(t)^2] + b[v_1(t) + v_2(t)] + 2c = e_1(t) + e_2(t) \quad t > 0 \quad (23)$$

When signal  $e_1(t) + e_2(t)$  excites the system at the same time, the following equation is obtained if the system is linear:

$$\frac{d}{dt} [v_1(t) + v_2(t)] - a[v_1(t) + v_2(t)]^2 + b[v_1(t) + v_2(t)] + c = e_1(t) + e_2(t) \quad t > 0 \quad (24)$$

Obviously, Eq. (23) contradicts to Eq. (24), it indicates that the system does not satisfy the additivity.

From the above, it means that the system is nonlinear.

If jet fans with the variable speed drive are in operation, the output airflow of a jet fan has the velocity jump, the following equation must be taken into account.

$$dv/dt = a \quad (25)$$

When the airflow field reaches a new steady-state, the following relationship is obtained since the steady-state model of airflow is used.

$$dv/dt = 0 \quad (26)$$

Assuming that the steady airflow velocity along the whole tunnel tube is  $v_\infty$ , then one obtains the final relationship for steady airflow velocity:

$$a(v^2 - v_\infty^2) + b(v - v_\infty) = \frac{dv}{dt} \quad (27)$$

The variation regularity of ventilation in the tunnel has obtained after application of variable frequency regulating velocity:

$$v(t) = \frac{2v_\infty + b/a}{1 - \left( \frac{v_0 - v_\infty}{v_0 + v_\infty + b/a} \right) \exp \left[ (2av_\infty + b)t \right]} - v_\infty - b/a \quad (28)$$

According to the basic principle of process control theory, the transition time of process refers to the time from the time when the system is disturbed to the time when the controlled parameters enter the new stable value.

## Parameter values of the dynamic control model

In order to obtain the parameter values of the airflow dynamic control model in the actual tunnel, the full-scale experiment of variable air volume longitudinal ventilation is carried out. The experimental

![A photograph of a long, narrow, arched tunnel structure. A red line with arrows indicates the length of the tunnel as 200m. A red vertical line with arrows indicates the width of the tunnel as 9.6m. The tunnel is surrounded by greenery and a paved area.](32510653d1983ab5e63ce1f9f4be54cc_img.jpg)

A photograph of a long, narrow, arched tunnel structure. A red line with arrows indicates the length of the tunnel as 200m. A red vertical line with arrows indicates the width of the tunnel as 9.6m. The tunnel is surrounded by greenery and a paved area.

Fig. 2. The full-scale experimental tunnel.

tunnel is 200 m long, 9.6 m wide, 7.4 m high, as shown in Fig. 2.

The variable air volume ventilation is realized by the frequency converter to control the jet fans. And the two jet fans in the experimental tunnel are bidirectional with a power of 15 kW, as shown in Fig. 3.

The model of the jet fans in this experiment is SDS-11.2-4P-6-24<sup>0</sup>, the air volume is 30.5 m<sup>3</sup>/s when running at full speed, the wind speed is 31.1 m/s, and the fan diameter is 1120 mm with 6 blades.

According to the characteristics of tunnel ventilation resistance, the ventilation resistance  $R$  can be expressed by the following relationship:

$$R = \lambda \frac{l}{d} \frac{\rho}{2A_f^2} + \zeta_{in} \frac{\rho}{2A_f^2} + \zeta_{out} \frac{\rho}{2A_f^2} = \left( \lambda \frac{l}{d_e} + \zeta_{in} + \zeta_{out} \right) \frac{\rho}{2A_f^2} \quad (29)$$

And the significance and value of various physical parameters are shown in Table 1 [30].

Bringing the parameters into Eq. (29),  $R$  is obtained:

$$R = \left( \lambda \frac{l}{d} + \zeta_{in} + \zeta_{out} \right) \frac{\rho}{2A_f^2} = \left( 0.02 \frac{200}{2.05} + 1 + 0.6 \right) \frac{1.2}{2 \cdot 63^2} = 0.0003 \quad (30)$$

Therefore, the transfer function is:

$$G_P(s) = \frac{P(s)}{F(s)} e^{-\tau s} = \frac{K}{1 + Ts} e^{-\tau s} = \frac{520.279}{1 + 57.2574s} e^{-\tau s} \quad (31)$$

According to the basic principles of process control theory, the transition time  $t$  of a process refers to the time that the system experiences from the time when it is disturbed until the controlled parameters enter the range of  $\pm 5\%$  of the new stable values. Therefore, assuming that  $(v - v_{\infty})/(v_0 - v_{\infty}) \le 5\%$  is used as the basic constant standard, the time required for the transition process can be obtained as

$$\tau = \frac{1}{2av_{\infty} + b} \ln \left( \frac{0.05(v_0 + v_{\infty} + b/a)}{(1.95v_{\infty} + 0.05v_0 + b/a)} \right) \quad (32)$$

The mathematical model distinguishes between two main types of vehicles: passenger cars and commercial vehicles. Representative values for the drag coefficient and frontal area of these main vehicle types are provided in Tables 2 and 3 [31]. Therefore, the parameters such as  $a$  and  $b$  can be calculated.

According to the estimating formula for the transition time of the flow field shown in the formula and substituting the corresponding parameters, the delay time  $\tau = 116.2069s$  can be obtained.

Then the transfer function of the system is

$$G_P(s) = \frac{520.279}{1 + 57.2574s} e^{-\tau s} = \frac{520.279}{1 + 57.2574s} e^{-116.2069s} \quad (33)$$

![Figure 3: The jet fans in the experiment. The image shows two large industrial jet fans mounted on metal stands in a tunnel. Red arrows point to the 'Outlet side' and 'Inlet side' of the fans. The tunnel floor is visible, and a vehicle is seen in the distance.](3cf4f743ab1967f5b295d4a954a3ad6d_img.jpg)

Figure 3: The jet fans in the experiment. The image shows two large industrial jet fans mounted on metal stands in a tunnel. Red arrows point to the 'Outlet side' and 'Inlet side' of the fans. The tunnel floor is visible, and a vehicle is seen in the distance.

Fig. 3. The jet fans in the experiment.

**Table 1**

Significance and value of various physical parameters.

| Parameter     | Numerical value | Physical Significance                         |
|---------------|-----------------|-----------------------------------------------|
| $\lambda$     | 0.02            | The resistance coefficient along the way      |
| $d_e$         | 2.05            | The equivalent diameter of the tunnel section |
| $\zeta_{in}$  | 1               | Local loss coefficient of tunnel entrance     |
| $\zeta_{out}$ | 0.6             | Local loss coefficient of tunnel exit         |
| $L$           | 200             | The length of tunnel                          |
| $N_j$         | 1               | Total number of jet fans                      |
| $A_f$         | 0.985           | Sectional area of jet fan outlet              |
| $A_t$         | 63              | The sectional area of the tunnel              |
| $K_j$         | 0.7             | The pressurization coefficient of jet fan     |
| $v_j$         | 18.66           | Outlet wind speed of jet fan                  |

*Predictive compensation control of the system and fuzzy self-tuning of parameters*

Due to the existence of the time delay, the control system cannot respond in time when it is disturbed by the outside world. To mitigate the negative effects of the time delay, an ideal predictive compensation control strategy should be selected and designed. The Smith prediction compensation control strategy [32] can make the controller work in advance, improving the dynamic performance of the control system. It has been widely popularized and applied, demonstrating its excellent qualities in the compensation strategy.

The basic idea is that, based on the process characteristics, an estimated model is added in the feedback control system to compensate for the process's dynamic characteristics. And the basic principle is shown in Fig. 4: dividing  $G_P(s)e^{-\tau s}$ , using  $G_P(s)$  as the transfer function of the process control channel, and the output signal of  $G_P(s)$  as the feedback signal.

According to the characteristics of the tunnel ventilation control system and the control model established above, a control scheme based on the Smith predictive compensation control strategy can be constructed, as shown in Fig. 5.

Because the characteristics of the tunnel ventilation control system's control object change with traffic, the original working state of the control system will be deviated. As a result, an online self-tuning method must be developed in order to improve the speed of parameter tuning and control system performance. To adjust the parameters of  $K_p$ ,  $T_i$  and  $T_d$ , a method of adding a designed specific fuzzy control loop to the classical PID controller is used in this paper. This control method not only retains the classical PID controller's excellent stability and low static error, but it also has the characteristics of a simple control principle, good robustness, and excellent dynamic quality. The basic principle is shown in Fig. 6.

The established control system is shown in Fig. 7, which is based on the above analysis and the characteristics of the dynamic control system in tunnel ventilation.

## The performance evaluation of tunnel variable air volume ventilation control system

### The indicators of performance evaluation

The dynamic characteristics of the controlled object are determined after the tunnel ventilation control system is established through mechanism analysis. The main link in the design of the control system becomes determining the optimal working state of the system and making the system run in the optimal state.

One of the most popular methods is the trial and error method. The basic idea is to apply a step signal to the system, measure and analyze the system's step response curve parameters, and then combine it with mechanism analysis to determine the influence of the regulator parameters on characteristics. Make the system work in the optimal state to achieve a satisfactory control effect, and then determine the optimal

**Table 2**  
Windward area and air resistance coefficient of passenger cars and commercial vehicles.

| Type                       | Passenger cars      |           |                     | Commercial vehicles |           |                             |
|----------------------------|---------------------|-----------|---------------------|---------------------|-----------|-----------------------------|
| Subtype                    | Basic passenger car | MPV/SUV   | Cross passenger car | Bus                 | Truck     | Semi-trailer towing vehicle |
| $A_{vm}$ ( $m^3$ )         | 1.7–2.1             | 2.2–5.0   | 2.5–6.0             | 4.0–7.0             | 3.0–7.0   | 6.5–9.0                     |
| Air resistance coefficient | 0.25–0.41           | 0.30–0.51 | 0.35–0.51           | 0.50–0.80           | 0.60–1.00 | 0.60–1.00                   |

**Table 3**  
Windward area and air resistance coefficient of commercial freight vehicles.

| Type                              | $A_{vm}$ ( $m^3$ ) | Air resistance coefficient |
|-----------------------------------|--------------------|----------------------------|
| Semi-trailer truck (Flat truck)   | 6.5                | 0.7                        |
| Semi-trailer truck (Canvas truck) | 8.0                | 0.9                        |
| Semi-trailer truck (Box truck)    | 8.0                | 0.7                        |
| Semi-trailer truck with box       | 9.0                | 1.1                        |
| Average value                     | /                  | 0.85                       |

![Figure 4: Equivalent block diagram of Smith predictive compensation control. The diagram shows a feedback loop where the input X(s) is compared with Y1(s) to produce an error signal. This error signal is multiplied by the controller Gc(s) to produce the control signal U(s). U(s) is then compared with Y2(s) to produce another error signal, which is multiplied by the plant model Gp(s)(1-e^{-Ts}) to produce the output Y(s). The output Y(s) is also fed back through a delay block e^{-Ts} to Y1(s).](1be8e9cad5f38fa47bdb81e549a3bec9_img.jpg)

Figure 4: Equivalent block diagram of Smith predictive compensation control. The diagram shows a feedback loop where the input X(s) is compared with Y1(s) to produce an error signal. This error signal is multiplied by the controller Gc(s) to produce the control signal U(s). U(s) is then compared with Y2(s) to produce another error signal, which is multiplied by the plant model Gp(s)(1-e^{-Ts}) to produce the output Y(s). The output Y(s) is also fed back through a delay block e^{-Ts} to Y1(s).

Fig. 4. Equivalent block diagram of Smith predictive compensation control.

![Figure 5: Smith estimate compensate control project. This block diagram shows a control system where the reference current I_T* is compared with the sum of the measured current I_m and the estimated current I_E to produce the error signal e. This error signal is multiplied by the controller Gc(s) to produce the control signal I_m. The control signal I_m is then compared with the measured current I_m to produce the error signal e_E. This error signal e_E is multiplied by the Smith estimate compensator block, which contains a delay e^{-116.2s} and a transfer function (520.279 / (1 + 57.2574s)), to produce the estimated current I_E. The estimated current I_E is then added to the measured current I_m to produce the total current I_S.](6df5629bc2fc6d82f1a1edf9d7340113_img.jpg)

Figure 5: Smith estimate compensate control project. This block diagram shows a control system where the reference current I\_T\* is compared with the sum of the measured current I\_m and the estimated current I\_E to produce the error signal e. This error signal is multiplied by the controller Gc(s) to produce the control signal I\_m. The control signal I\_m is then compared with the measured current I\_m to produce the error signal e\_E. This error signal e\_E is multiplied by the Smith estimate compensator block, which contains a delay e^{-116.2s} and a transfer function (520.279 / (1 + 57.2574s)), to produce the estimated current I\_E. The estimated current I\_E is then added to the measured current I\_m to produce the total current I\_S.

Fig. 5. Smith estimate compensate control project.

![Figure 6: Parameter fuzzy self-tuning control system. The diagram shows a feedback loop where the reference signal R is compared with the output signal C to produce the error signal e. This error signal e is fed into a fuzzy logic controller block. The fuzzy logic controller block contains a 'fuzzy reasoning' block and is used to tune the parameters K_p, K_i, and K_d of a PID controller. The error signal e is also differentiated to produce the derivative signal de/dt, which is fed into the PID controller. The output of the PID controller is fed into a 'controlled object' block, which produces the output signal C.](47e8c2042061e08a14e012472e9fdbaa_img.jpg)

Figure 6: Parameter fuzzy self-tuning control system. The diagram shows a feedback loop where the reference signal R is compared with the output signal C to produce the error signal e. This error signal e is fed into a fuzzy logic controller block. The fuzzy logic controller block contains a 'fuzzy reasoning' block and is used to tune the parameters K\_p, K\_i, and K\_d of a PID controller. The error signal e is also differentiated to produce the derivative signal de/dt, which is fed into the PID controller. The output of the PID controller is fed into a 'controlled object' block, which produces the output signal C.

Fig. 6. Parameter fuzzy self-tuning control system.

parameters through repeated debugging.

When a step signal affects a system, the following indicators are typically used to evaluate its response performance:

#### (1) Residual

When the system reaches steady-state, the deviation between the steady-state value and the given value is the residual, which is an important indicator of the static analysis of the system. It is also known as the static deviation of the system, denoted by  $C$ . In general, the residual of the system is required to be less than a given value or close to zero.

#### (2) Decay rate

The decay rate is an important indicator when performing dynamic analysis of the system, which is defined as Eq. (61).

$$\psi = \frac{B_1 - B_2}{B_1} = 1 - \frac{B_2}{B_1} \quad (61)$$

As can be seen, the value of  $\psi$  has a significant impact on the system's stability. The appropriate value of  $\psi$  in engineering analysis should generally be chosen based on the specific characteristics of the engineering system. The decay rate is typically assumed to be 0.75–0.9.

#### (3) Maximum deviation and overshoot

The difference between the first peak of the controlled parameter and the given value is the maximum deviation of the fixed value system. It is represented by the overshoot in the follow-up system and is defined as Eq. (62).

$$\sigma = \frac{y(t_p) - y(\infty)}{y(\infty)} \times 100\% \quad (62)$$

The maximum deviation of the fixed value system and the overshoot of the follow-up system are important indicators to measure the dynamic performance of the system, which indicate the degree of deviation between the controlled parameter and the given value.

#### (4) Transition time

Transition time  $t_s$  is an important indicator to measure the control response speed. The smaller the value of  $t_s$ , the better the performance of the system. It is the time between when the system is disturbed and when the controlled parameter reaches  $\pm 5\%$  error of the new stable value.

### *Simulation analysis of the performance*

In this section, the simulation software MATLAB is used to simulate and analyze the control system. The simulation model of the tunnel variable air volume ventilation control is shown in Fig. 8.

The step response parameter curve of the system is shown in Fig. 9. The analysis results are shown in Table 4.

The key parameters in Fig. 9 are presented in table form, as shown in Table 4. Through the simulation analysis, the parameters such as residual, overshoot and transition time of the system are all within the allowable error range, which can meet the needs of tunnel variable air volume ventilation control.

## *Experimental analysis of the performance*

In this section, a full-scale experiment is carried out in the experimental tunnel (as shown in Fig. 2) to demonstrate the controllability of the wind speed by using the variable air volume ventilation control system to adjust the working frequency of the jet fan in real time. The response parameters and system stability are tracked and recorded based on the proposed target wind speed.

The frequency converter, the new filter device, the cable, the jet fans, the anemometer, and other components comprise the experimental

![General diagram of control system](a738993919a50143787084ee7ce6e2f2_img.jpg)

The diagram illustrates a multi-input control system. Five input sources are shown at the top: 'Traffic collection', 'VI concentration measurement', 'CO concentration measurement', 'Wind speed and direction measurement', and 'Operation status of ventilation equipment'. These feed into an 'Input information processing' block. The 'Traffic collection' input also feeds into a separate 'Input information processing' block, which then leads to 'Traffic estimate' and 'Required air volume calculation'. The 'Required air volume calculation' block feeds into 'Calculate dynamic concentration and wind speed according to traffic operation'. This block also interacts with the 'Ventilation Control Model' and feeds into 'Output information processing'. The 'Ventilation Control Model' contains 'Fuzzy parameter tuning' and a 'PID controller'. The 'PID controller' is represented by the transfer function  $\frac{520.279}{1+57.2574s}e^{-\tau s}$ . The 'Operation status of ventilation equipment' feeds into 'Abnormal working condition control', which also feeds into 'Output information processing'. Finally, 'Output information processing' leads to the 'Fan frequency' output.

General diagram of control system

Fig. 7. General diagram of control system.

![Simulation model about the system](49ee89a1d5852ab005dbbab6de09a8a6_img.jpg)

This is a Simulink block diagram of the control system. A 'Step' block (labeled '阶跃信号') provides the reference input. The error signal 'e' is calculated by subtracting the output from the reference. This error signal is fed into two parallel paths. The first path involves a gain 'k1', a 'Saturation' block, and a 'Zero-Order Hold' block, which then feeds into a 'Fuzzy Logic Controller' block. The second path involves a 'Derivative2' block, a gain 'k2', a 'Saturation1' block, and a 'Zero-Order Hold' block, which also feeds into the 'Fuzzy Logic Controller'. The output of the 'Fuzzy Logic Controller' is fed into a 'Transport Delay' block. The error signal 'e' also feeds into a 'PID Controller1' block, which has parameters k, k1, k2, kpe, kie, and kde. The output of 'PID Controller1' is fed into an 'Add1' block. The output of the 'Transport Delay' block is also fed into 'Add1'. The result of 'Add1' is fed into a 'Transfer Fcn3' block with the transfer function  $\frac{520.279}{57.2574s+1}$ . The output of 'Transfer Fcn3' is fed into a 'Transport Delay2' block. The output of 'Transport Delay2' is fed back into the summing junction for error 'e'. A 'Scope' block is connected to the output of 'Transfer Fcn3'.

Simulation model about the system

Fig. 8. Simulation model about the system.

system. The system composition is shown in Fig. 10.

The measuring instrument includes an airflow velocity sensor and an airflow velocity acquisition system, as shown in Fig. 11 and Fig. 12. The accuracy of the sensor is  $\pm 3\%$  with a model of D-FL 210 T-MK2 B, the allowable airflow velocity is 0.4–60 m/s, and the allowable air volume is 0–99,999 m<sup>3</sup>/s. And the model of the airflow velocity acquisition system is D-FL200.

Two conditions are designed to study the characteristics of the jet fans driven by the frequency converter under special conditions and to realize dynamic control of the wind speed in the tunnel, as shown in Table 5. The parameters of the jet fans are shown in Table 6.

The measured wind speed in the tunnel and the real-time frequency

of the fan are shown in Fig. 13. When the target wind speed is set to 1.0 m/s, the overshoot of the system is 20%, the rise time is 50 s, the transition time is 210 s, and the residual is 0.2. It can be seen from Fig. 13 (a) that when the target wind speed in the tunnel is 1.0 m/s, the actual wind speed in the tunnel mainly fluctuates in the range of 0.8–1.2 m/s.

When the target wind speed is set to 1.5 m/s, the overshoot of the system is 6.67%, the rise time is 75 s, the transition time is 181 s, and the residual is 0.22. It can be seen from Fig. 13 (b) that when the target wind speed in the tunnel is 1.8 m/s, the actual wind speed in the tunnel mainly fluctuates in the range of 1.38–1.6 m/s.

When the target wind speed is set to 1.8 m/s, the overshoot of the

![Figure 9: Wind speed controlled by converter test in tunnel. Five subplots (a) through (e) show wind speed (m/s) versus time (s) for different target speeds and transitions. Each plot includes a yellow step function for the target speed and a brown line for the transport delay response. Subplots (a), (b), and (c) show step responses to constant target speeds of 1.0m/s, 1.5m/s, and 1.8m/s respectively. Subplots (d) and (e) show transitions from 1.0m/s to 1.4m/s and from 1.4m/s to 1.8m/s respectively. Each plot displays the residual and decay rate of the transport delay response.](a71911ad87414271aeb190e0eebcb989_img.jpg)

**(a) target wind speed 1.0m/s**  
 Wind speed(m/s): 0 to 1.0  
 Time(s): 0 to 300  
 Step: 100s  
 Transport Delay: 130s  
 residual:0.0004  
 decay rate:0.04

**(b) target wind speed 1.5m/s**  
 Wind speed(m/s): 0 to 1.6  
 Time(s): 0 to 300  
 Step: 100s  
 Transport Delay: 130s  
 residual:0.001  
 decay rate:0.075

**(c) target wind speed 1.8m/s**  
 Wind speed(m/s): 0 to 2.0  
 Time(s): 0 to 300  
 Step: 100s  
 Transport Delay: 130s  
 residual:0.002  
 decay rate:0.243

**(d) target wind speed 1.0m/s→1.4m/s**  
 Wind speed(m/s): -0.2 to 1.8  
 Time(s): 0 to 300  
 Step: 100s  
 Transport Delay: 130s  
 residual:0.002  
 decay rate:0.16

**(e) target wind speed 1.4m/s→1.8m/s**  
 Wind speed(m/s): 0 to 2.0  
 Time(s): 0 to 300  
 Step: 100s  
 Transport Delay: 130s  
 residual:0.004  
 decay rate:0.15

Figure 9: Wind speed controlled by converter test in tunnel. Five subplots (a) through (e) show wind speed (m/s) versus time (s) for different target speeds and transitions. Each plot includes a yellow step function for the target speed and a brown line for the transport delay response. Subplots (a), (b), and (c) show step responses to constant target speeds of 1.0m/s, 1.5m/s, and 1.8m/s respectively. Subplots (d) and (e) show transitions from 1.0m/s to 1.4m/s and from 1.4m/s to 1.8m/s respectively. Each plot displays the residual and decay rate of the transport delay response.

Fig. 9. Wind speed controlled by converter test in tunnel.

**Table 4**

The parameters of different working conditions.

| target wind speed (m/s) | overshoot | stable value | rise time (s) | transition time (s) | peak time (s) | residual | decay rate |
|-------------------------|-----------|--------------|---------------|---------------------|---------------|----------|------------|
| 1.0                     | 6.2%      | 0.9996       | 123.111       | 203.325             | 129.433       | 0.0004   | 0.04       |
| 1.5                     | 10.6%     | 1.499        | 121.040       | 183.867             | 125.739       | 0.001    | 0.075      |
| 1.8                     | 15.9%     | 1.798        | 120.030       | 164.955             | 123.884       | 0.002    | 0.243      |
| 1.0→1.4                 | 22.7%     | 1.398        | 119.581       | 157.020             | 122.291       | 0.002    | 0.16       |
| 1.4→1.8                 | 20.33%    | 1.804        | 119.625       | 159.729             | 123.276       | 0.004    | 0.15       |

![Diagram of the experimental system composition. It shows a 200m long tunnel with a 220v 50Hz power supply and a 380v 50Hz power supply. An anemometer is mounted on the left wall. A PLC receives wind speed feedback (4-20mA) from the anemometer. The PLC controls an inverter (INV) which drives a jet fan (JF2). A filter is also connected to the inverter. Another jet fan (JF1) is connected to the system via a cable (100-10000m). Below the diagram are five photographs showing the physical components: the anemometer, the PLC, the inverter, the filter, and the jet fans.](367926125450c2bc3f4bdca9d59a62ba_img.jpg)

Diagram of the experimental system composition. It shows a 200m long tunnel with a 220v 50Hz power supply and a 380v 50Hz power supply. An anemometer is mounted on the left wall. A PLC receives wind speed feedback (4-20mA) from the anemometer. The PLC controls an inverter (INV) which drives a jet fan (JF2). A filter is also connected to the inverter. Another jet fan (JF1) is connected to the system via a cable (100-10000m). Below the diagram are five photographs showing the physical components: the anemometer, the PLC, the inverter, the filter, and the jet fans.

**Fig. 10.** Composition of experimental system.![Close-up photograph of the airflow velocity sensor (anemometer) by DURAG. The sensor is a cylindrical device with a label indicating the model and specifications.](f5aaecb6473222e3d65f65164fab048e_img.jpg)

Close-up photograph of the airflow velocity sensor (anemometer) by DURAG. The sensor is a cylindrical device with a label indicating the model and specifications.

**Fig. 11.** The airflow velocity sensor.![Photograph of the acquisition system, which is a DURAG data logger unit with a digital display and several buttons. It is housed in a metal enclosure with various cables connected to the back.](b7c99649d8de39a814e0bad989d50b12_img.jpg)

Photograph of the acquisition system, which is a DURAG data logger unit with a digital display and several buttons. It is housed in a metal enclosure with various cables connected to the back.

**Fig. 12.** The acquisition system.**Table 5**

Working conditions in the experiment.

| Conditions  | Contents                                                                   |
|-------------|----------------------------------------------------------------------------|
| Condition 1 | Application of frequency converter to control wind speed in highway tunnel |
| Condition 2 | Two jet fans are driven by inverter and filter                             |

**Table 6**

The parameters of the jet fans.

| Fan model         | Air volume (m <sup>3</sup> /s) | Outlet wind speed (m/s) | Power (kW) | Thrust (N) | Weight (kg) |
|-------------------|--------------------------------|-------------------------|------------|------------|-------------|
| SDS-6.3-2 P-4-27° | 10.8                           | 34.7                    | 15         | 439        | 190         |
| SDS-6.3-2 P-4-30° | 11.7                           | 37.5                    | 15         | 513        | 190         |

mainly fluctuates in the range of 1.62–1.88 m/s.

When the target wind speed is set to 0→1.0→1.4→1.8 m/s, the test parameter curve of the system is shown in Fig. 13 (d). The analysis shows that when the target wind speed is 0→1.0 m/s, the overshoot of the system is 20%, the rise time is 63 s, the transition time is 121 s, and the residual is 0.2. When the target wind speed is 1.0→1.4 m/s, the overshoot of the system is 14.29%, the rise time is 65 s, the transition time is 119 s, and the residual is 0.13. When the target wind speed is 1.4→1.8 m/s, the overshoot of the system is 11.11%, the rise time is 69 s, the transition time is 121 s, and the residual is 0.17. It can be seen from Fig. 13 that the cross-sectional wind speed in the tunnel can basically be stabilized at the set target wind speed, which can meet the actual needs of tunnel operation.

The experimental results show that the changing trend of the measured wind speed in the tunnel lags behind the change of the fan operating frequency for a period of time, reflecting the tunnel ventilation control system's large time delay.

The wind speed monitor installed in the tunnel and the variable

system is 11.11%, the rise time is 72 s, the transition time is 192 s, and the residual is 0.2. It can be seen from Fig. 13 (c) that when the target wind speed in the tunnel is 1.8 m/s, the actual wind speed in the tunnel

![Figure 13: Wind speed test about variable air volume ventilation system. Four subplots (a, b, c, d) show Target velocity (red line), velocity (blue line), and JF (black line) over time (min) and JF (Hz).](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 13 consists of four subplots (a, b, c, d) showing the performance of a variable air volume ventilation system under different wind speed conditions. Each subplot has two y-axes: the left axis represents 'Target velocity/m/s' (ranging from -0.2 to 1.4 in a) and 0.6 to 2.4 in (c), and the right axis represents 'JF/Hz' (ranging from -10 to 55 in a) and 0 to 55 in (d). The x-axis for all plots is 'Time/min'.

- (a) target wind speed 1m/s:** The target velocity is a red line at 1.0 m/s. The velocity (blue line) starts at 0, rises to 1.0 m/s with an overshoot of 20% (indicated by a red arrow), and then fluctuates around the target. The JF (black line) fluctuates between approximately 10 and 45 Hz.
- (b) target wind speed 1.5m/s:** The target velocity is a red line at 1.5 m/s. The velocity (blue line) starts at 0, rises to 1.5 m/s with an overshoot of 6.67% (indicated by a red arrow), and then fluctuates around the target. The JF (black line) fluctuates between approximately 15 and 50 Hz.
- (c) target wind speed 1.8m/s:** The target velocity is a red line at 1.8 m/s. The velocity (blue line) starts at 0, rises to 1.8 m/s with an overshoot of 11.11% (indicated by a red arrow), and then fluctuates around the target. The JF (black line) fluctuates between approximately 20 and 55 Hz.
- (d) target wind speed 0→1.0→1.4→1.8m/s:** The target velocity (red line) changes in steps: 0 m/s for 2 min, 1.0 m/s for 2 min, 1.4 m/s for 2 min, and 1.8 m/s for 2 min. The velocity (blue line) follows these steps with overshoots of 20% at 1.0 m/s, 14.29% at 1.4 m/s, and 11.11% at 1.8 m/s (all indicated by red arrows). The JF (black line) fluctuates between approximately 10 and 55 Hz.

Figure 13: Wind speed test about variable air volume ventilation system. Four subplots (a, b, c, d) show Target velocity (red line), velocity (blue line), and JF (black line) over time (min) and JF (Hz).

Fig. 13. Wind speed test about variable air volume ventilation system.

frequency adjustment controller, which can monitor the wind speed status in the tunnel in real-time, comprise the closed-loop wind speed control system. And, using the control system, the inverter's output frequency is adjusted in real-time to the fan, allowing for real-time wind speed adjustment in the tunnel and achieving the goal of dynamic control.

## Conclusions

This paper proposes a tunnel variable air volume ventilation dynamic control system. For process control of the system, a first-order delay time mathematical model is established, and the characteristics of the dynamic control system are analyzed to obtain the transfer function. Furthermore, the system is built using predictive compensation control and parameter fuzzy self-tuning. Besides, the performance of the system is verified through simulation and full-scale experiments. In this study, a mathematical model is established to realize the risk control system of tunnel variable air volume. Long tunnel ventilation can be operated with more accuracy, energy savings, and increased ventilation efficiency by utilizing this control method. The main conclusions are as follows:

- (1) The airflow velocity of the variable air volume ventilation system in the tunnel is affected by the local loss and resistance along the way, the speed of vehicles and the pressure change due to running jet fans, etc. From this, the functional expression of the airflow

velocity and the delay time of the flow field in the tunnel can be obtained.

- (2) The variable air volume ventilation control system in the tunnel does not meet the linear system's uniformity and additivity requirements. It is a nonlinear system, reflecting the large time-delay characteristics.
- (3) The first-order delay time transfer function of the tunnel ventilation control system is a composite function of the magnification factor  $K$ , the time constant  $T$ , and the delay time  $\tau$ . The magnification factor  $K$  and the time constant  $T$  are both positively correlated with the 1/2-th power of ventilation resistance and pressure. The delay time  $\tau$  is affected not only by the length of the tunnel, the number of fans, and the resistance along the tunnel, but also by the volume of traffic in the tunnel.
- (4) The control system performs well, and the parameters such as overshoot, stable value, and adjustment time are all within the allowable error range, allowing it to meet the needs of tunnel wind speed control. Real-time wind speed adjustment in the tunnel can be realized by adjusting the output frequency of the inverter to the fan via the control system, and the goal of dynamic wind speed control can be achieved.

Finally, it is worth emphasizing that the proposed dynamic control system for variable air volume ventilation in tunnels is based on experimental data and theoretical derivation, and its effectiveness is well verified in the present experimental test range. Once in a tunnel 

environment with variable traffic flow, special validations need to be carefully performed, and the mathematical model needs to be optimized for different congestion situations.

# Declaration of Competing Interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgement

The authors gratefully acknowledge the support extended by the

Chongqing Nature Science Foundation (No. CSTB2023NSCQ-MSX0960), the State Key Laboratory of Mountain Bridge and Tunnel Engineering Fund Project (No. SKLBT-19-013), the Major Science and Technology Special Project of Xinjiang Uygur Autonomous Region (No. 2020A03003-4), and the Postdoctoral Special Funding Project of Chongqing (No. 01.02.9901212074) for funding this research. The authors would like to thank the editor and reviewers for their helpful comments and constructive suggestions, which have significantly improved the quality of this paper.

# Appendix

## (1) Detailed derivation process of Eqs. (11) and (12).

According to the characteristics of ventilation resistance in the tunnel, the relationship between the ventilation resistance and the pressure can be obtained as follows:

$$p = RQ_2^2$$

$$Q_2 = \sqrt{\frac{p}{R}}$$

$$\Delta Q_2 = \frac{1}{\sqrt{R}} \left( \sqrt{p} - \sqrt{p_0} \right)$$

$$\Delta Q_2 = \frac{1}{\sqrt{R}} \frac{(\sqrt{p} - \sqrt{p_0})(\sqrt{p} + \sqrt{p_0})}{\sqrt{p} + \sqrt{p_0}} = \frac{1}{\sqrt{R}} \frac{p - p_0}{\sqrt{p} + \sqrt{p_0}} = \frac{1}{\sqrt{R}} \frac{1}{2\sqrt{p_0}} (p - p_0) = \frac{1}{\sqrt{R}} \frac{1}{2\sqrt{p_0}} \Delta p$$

where  $R$  is the ventilation resistance.  $R_2$  and  $\Delta Q_2$  are defined respectively as follows:

$$R_2 = 2\sqrt{p_0}\sqrt{R}$$

$$\Delta Q_2 \approx \frac{1}{\sqrt{R}} \frac{1}{2\sqrt{p_0}} (p - p_0) = \frac{\Delta p}{R_2}$$

Using both the above equations and Eq. (11), the following relationship between  $\Delta Q_1$  and  $\Delta p$  is obtained:

$$\Delta Q_1 - \frac{\Delta p}{R_2} = \frac{V}{R_0 T_0} \frac{d\Delta p}{dt}$$

The inflow  $Q_1$  is calculated using the following equation:

$$Q_1 = k_f \cdot f \cdot A_r \cdot p$$

where  $k_f$  is the frequency coefficient of the fan can be obtained from the characteristic parameters of the fan,  $f$  represents the operation frequency of the fan.

According to the characteristics of the fan, the following equations are obtained:

$$\Delta Q_1 = k_f \cdot \Delta f \cdot A_r \cdot p$$

$$k_f \cdot \Delta f \cdot A_r \cdot p - \frac{\Delta p}{R_2} = \frac{V}{R_0 T_0} \frac{d\Delta p}{dt}$$

Here,  $k_2$  and  $C$  are defined respectively as follows:

$$k_2 = k_f \cdot A_r \cdot p$$

$$C = \frac{V}{R_0 T_0}$$

$$k_2 \cdot \Delta f - \frac{\Delta p}{R_2} = C \frac{d\Delta p}{dt}$$

- (2) The values of coefficients a, b and c in Eq. (17).

A variable separating scheme is employed to solve Eq. (6), thus the absolute value in Eq. (6) captures the two situations. One of the situations is when the average velocity of vehicles is lower than the airflow velocity in the tunnel, the airflow of the vehicle acts as the pressure loss. The opposite situation is that it acts as the pressure acceleration.

Regarding these parameters of the traffic, the mechanical ventilation system, tunnel geometric dimensioning, the airflow in the tunnel, and so on, the coefficients a, b, and c in Eq. (17) are expressed explicitly in terms of two situations flows:

Situation 1,  $v_v > v$

$$a = \frac{KLA_{vm} - A_f \left( \lambda \frac{L}{d_e} + \zeta_{in} + \zeta_{out} \right)}{2A_f L}$$

$$b = -\frac{N_f k_f A_f v_j + KLA_{vm} v_v}{A_f L}$$

$$c = \frac{N_f k_f A_f v_j^2 + \frac{1}{2} KLA_{vm} v_v^2}{A_f L}$$

Situation 2,  $v_v < v$

$$a = -\frac{KLA_{vm} + A_f \left( \lambda \frac{L}{d_e} + \zeta_{in} + \zeta_{out} \right)}{2A_f L}$$

$$b = -\frac{N_f k_f A_f v_j - KLA_{vm} v_v}{A_f L}$$

$$c = \frac{N_f k_f A_f v_j^2 - \frac{1}{2} KLA_{vm} v_v^2}{A_f L}$$

- (3) Detailed derivation process of Eqs. (27) and (28).

After some reasonable simplicity and assumption, the authors have been working for dealing with the modeling of Eq. (27) with separation of variables, and the following relationship has been obtained:

$$\frac{dv}{a(v^2 - v_{\infty}^2) + b(v - v_{\infty})} = dt$$

Integrating both sides of the Upper equation separately, the mathematical expression of transition time is reduced to the following form:

$$t = \frac{1}{2av_{\infty} + b} \ln \left| \frac{v - v_{\infty}}{v + v_{\infty} + b/a} \right| + C$$

Here C is the integration constant.

Assuming that the initial speed is C, integration constant C is found from the initial condition,  $v(t=t_0^+) = v_0$ :

$$C = -\frac{1}{2av_{\infty} + b} \ln \left| \frac{v_0 - v_{\infty}}{v_0 + v_{\infty} + b/a} \right|$$

one obtains the final formula of transition time as follows:

$$t(v) = \frac{1}{2av_{\infty} + b} \ln \left| \frac{(v - v_{\infty})(v_0 + v_{\infty} + b/a)}{(v_0 - v_{\infty})(v + v_{\infty} + b/a)} \right|$$

Finding the inverse function of the Upper equation, the variation regularity of ventilation in the tunnel has obtained after application of variable frequency regulating velocity:

$$v(t) = \frac{2v_{\infty} + b/a}{1 - \left( \frac{v_0 - v_{\infty}}{v_0 + v_{\infty} + b/a} \right) \exp \left[ \left( 2av_{\infty} + b \right) t \right]} - v_{\infty} - b/a$$

- (4) Detailed derivation process of Eq. (31).

$R_2$ ,  $k_2$  and C are obtained:

$$R_2 = 2\sqrt{p_0} \sqrt{R} = 2 \cdot \sqrt{101325} \cdot \sqrt{0.0003} = 11.0698$$

$$k_2 = k_f \cdot A_f \cdot \rho = 0.622 \cdot 63 \cdot 1.2 = 47$$

$$C = \frac{V}{R_0 T_0} = \frac{63 \cdot 200}{8.314 \cdot 293} = 5.17241$$

Then  $K$  and  $T$  are obtained:

$$K = k_2 \cdot R_2 = 47 \cdot 11.0698 = 520.279$$

$$T = C \cdot R_2 = 5.17241 \cdot 11.0698 = 57.2574$$

$$G_P(s) = \frac{P(s)}{F(s)} e^{-Ts} = \frac{K}{1 + Ts} e^{-Ts} = \frac{520.279}{1 + 57.2574s} e^{-Ts}$$

# References

- [1] K.Y. Liu, J.Q. Guo, L.Y. Wan, C. Xu, A model test study to optimize the ventilation system of a long expressway tunnel, *J. Wind Eng. Ind. Aerodyn.* 207 (2020), 104393, <https://doi.org/10.1016/j.jweia.2020.104393>.
- [2] A. Chatterjee, L.J. Zhang, X.H. Xia, Optimization of mine ventilation fan speeds according to ventilation on demand and time of use tariff, *Appl. Energy* 146 (2015) 65–73, <https://doi.org/10.1016/j.apenergy.2015.01.134>.
- [3] Y.H. Lin, L.N. Ling, J.T. Chen, Combined grey prediction fuzzy control law with application to road tunnel ventilation system science direct, *J. Appl. Res. Technol.* 13 (2) (2015) 313–320, <https://doi.org/10.1016/j.jart.2015.06.009>.
- [4] M.N. Wang, X. Wang, L. Yu, T. Deng, Field measurements of the environmental parameter and pollutant dispersion in urban undersea road tunnel, *Build. Environ.* 149 (2019) 100–108, <https://doi.org/10.1016/j.buildenv.2018.11.036>.
- [5] Q. Li, C. Chao, H. Yuan, L. Wang, Y. Xu, S.H. Li, Y. R, Prediction of pollutant concentration and ventilation control in urban bifurcate tunnel, China, *Tunn. Undergr. Space Technol.* 82 (2018) 406–415, <https://doi.org/10.1016/j.tust.2018.06.002>.
- [6] L. Kurka, L. Ferkl, O. Sladek, J. Porizek, Simulation of traffic ventilation and exhaust in a complex road tunnel, *IFAC Proc. Vol.* 38 (1) (2005) 60–65, <https://doi.org/10.3182/20050703-6-CZ-1902.02033>.
- [7] L. Ferkl, G. Meinsma, Finding optimal ventilation control for highway tunnels, *Tunn. Undergr. Space Technol.* 22 (2) (2007) 222–229, <https://doi.org/10.1016/j.tust.2006.04.002>.
- [8] S. Bogdan, B. Birgmaier, Z. Kovacic, Model predictive and fuzzy control of a road tunnel ventilation system, *Transp. Res. Part C Emerg. Technol.* 16 (5) (2008) 574–592, <https://doi.org/10.1016/j.trc.2007.11.004>.
- [9] E. Karakas, The control of highway tunnel ventilation using fuzzy logic, *Eng. Appl. Artif. Intell.* 16 (7/8) (2003) 717–721, [https://doi.org/10.1016/S0952-1976\(03\)00068-X](https://doi.org/10.1016/S0952-1976(03)00068-X).
- [10] B. Chu, D. Kim, D. Hong, J. Park, J.T. Chung, J.H. Chung, T.H. Kim, GA-based fuzzy controller design for tunnel ventilation systems, *Autom. Constr.* 17 (2) (2008) 130–136, <https://doi.org/10.1016/j.autcon.2007.05.011>.
- [11] Antelo, I.E., Martin, S.F., Llorente, I.R., Álvarez, E.A., 2010. Experiences on the specification of algorithms for fire and smoke control in road tunnels. Graz University of Technology. (<http://oa.upm.es/20941/>).
- [12] Hrbeek, J., Spalek, J., Šimak, V., 2010. Process model and implementation the multivariable model predictive control to ventilation system. 2010 IEEE 8th International Symposium on Applied Machine Intelligence and Informatics (SAMI). IEEE, 211–214. <https://doi.org/10.1109/SAMI.2010.5423738>.
- [13] N. Euler-rolle, M. Fuhrmann, M. Reinwald, S. Jakubek, Longitudinal tunnel ventilation control: part 1: modelling and dynamic feedforward control, *Control Eng. Pract.* 63 (2017) 91–103, <https://doi.org/10.1016/j.conengprac.2017.03.017>.
- [14] K. Wu, Q.M. Yang, C. Kang, X. Zhang, Z.Y. Huang, Adaptive critic design based control of tunnel ventilation system with variable jet speed, *J. Signal Process. Syst. Signal Image Video Technol.* 86 (2) (2017) 269–278, <https://doi.org/10.1007/s11265-016-1123-8>.
- [15] J. Šulc, L. Ferkl, J. Cigler, J. Porizek, Optimization-based control of ventilation in a road tunnel complex, *Control Eng. Pract.* 69 (2017) 141–155, <https://doi.org/10.1016/j.conengprac.2017.09.011>.
- [16] Y.G. Huang, G. Fang, X.H. Li, An optimal control method of long tunnel ventilation based on variable domain fuzzy control, in: Chinese Automation Congress (CAC), 2018, IEEE, 2018, pp. 2626–2630, <https://doi.org/10.1109/CAC.2018.8623544>.
- [17] M. Fuhrmann, N. Euler-rolle, M. Killian, M. Reinwald, S. Jakubek, Longitudinal tunnel ventilation control. part 2: non-linear observation and disturbance rejection, *Control Eng. Pract.* 63 (2017) 44–56, <https://doi.org/10.1016/j.conengprac.2017.03.016>.
- [18] C. Peng, G.C. Jiang, Q.Z. Zou, Modeling and adaptive optimal control of highway tunnel ventilation system, in: American Control Conference (ACC), 2019, IEEE, 2019, pp. 5851–5856, <https://doi.org/10.23919/ACC.2019.8814700>.
- [19] L.Y. Si, W.P. Cao, X.P. Chen, Active disturbance rejection control of a longitudinal tunnel ventilation system, *Energies* 13 (8) (2020) 1871, <https://doi.org/10.3390/en13081871>.
- [20] D. Drikakis, W. Rider, High-resolution methods for incompressible and low-speed flows, Springer Science & Business Media, 2006, <https://doi.org/10.1007/b137615>.
- [21] J. Šulc, L. Ferkl, J. Cigler, et al., Model-based airflow controller design for fire ventilation in road tunnels, *Tunn. Undergr. Space Technol.* 60 (2016) 121–134, <https://doi.org/10.1016/j.tust.2016.08.006>.
- [22] A. Novotn, M. Pokorn, Continuity equation and vacuum regions in compressible flows, *J. Evol. Equ.* 21 (3) (2021) 2891–2922, <https://doi.org/10.1007/s00028-021-00704-3>.
- [23] J. Šulc, S. Skogestad, A systematic approach for airflow velocity control design in road tunnels, *Control Eng. Pract.* 69 (2017) 61–72, <https://doi.org/10.1016/j.conengprac.2017.09.005>.
- [24] W.Y. Sun, Hydraulic jump and bernoulli equation in nonlinear shallow water model, *Dyn. Atmos. Oceans* 82 (2018) 37–53, <https://doi.org/10.1016/j.dynamatoc.2018.02.003>.
- [25] S.F. Leonardo, Santos, The energy density distribution of an ideal gas and bernoulli's equations, *Eur. J. Phys.* 39 (3) (2018), 035102, <https://doi.org/10.1088/1361-6404/aaa34c>.
- [26] H.R. Ali-akbari, S. Ceballes, A. Abdelkefi, Nonlinear performance analysis of forced carbon nanotube-based bio-mass sensors, *Int. J. Mech. Mater. Des.* 15 (2) (2019) 291–315, <https://doi.org/10.1007/s10999-018-9414-9>.
- [27] S.E. Bouzdi, M. Hassan, S. Ziada, Characterization of flow-sound-structure coupling in spring-loaded valves. Pressure Vessels and Piping Conference, American Society of Mechanical Engineers, 2017, <https://doi.org/10.11115/PVP2017-65767>.
- [28] P.K. Mishra, A.S. Darbari, A. Ali, Optimisation of performance of multi bladed vertical axis wind turbine by using nozzle, *Int. J. Emerg. Technol. Adv. Eng.* 4 (1) (2014) 177–183 (<https://doi.org/ijetae.com>).
- [29] J. Arnaud, L. Chusseau, F. Philippe, On classical ideal gases, *Entropy* 15 (3) (2011) 960–971, <https://doi.org/10.3390/e15030960>.
- [30] Ministry of Communications of the People's Republic of China, Guidelines for Design of Ventilation of Highway Tunnels, China Communications Press, Beijing, 2014. ISBN:978-7-11-411546-2.
- [31] P.K. Kundu, I.M. Cohen, D.R. Dowling, *Fluid Mechanics*, Fifth ed., 2012. ISBN: 978-0-12-382100-3.
- [32] Z.N. Hong, X.D. Wang, Smith predictive compensator and its application, *Control Eng. China* 05 (2002) 69–71, <https://doi.org/10.3969/j.issn.1671-7848.2002.05.023>.