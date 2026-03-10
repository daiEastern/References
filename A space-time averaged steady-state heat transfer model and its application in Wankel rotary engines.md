

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Applied Thermal Engineering journal cover](390120de4fe440c42fea8154fcaad334_img.jpg)

Applied Thermal Engineering journal cover

## Research Paper

![Check for updates button](4f4b52340aaccb1bcf733468dca9ee03_img.jpg)

Check for updates button

# A space-time averaged steady-state heat transfer model and its application in Wankel rotary engines

Baichuan Chen, Xiaocan Chai, Jinxiang Liu<sup>\*</sup>*School of Mechanical Engineering, Beijing Institute of Technology, Beijing 100081, China*

##### ARTICLE INFO

### Keywords:

Wankel rotary engine  
Thermal boundary condition  
Steady state heat transfer  
CHT  
Space-time averaging method

## ABSTRACT

In response to energy efficiency and emissions reduction demands, downsized Wankel rotary engines (WREs) are used in applications like vehicle range extenders and unmanned aerial vehicle power sources due to their high power-to-weight ratio. Addressing performance and lifespan issues under thermal loads is crucial. However, there is still no efficient solution for the definition of thermal boundary in Wankel rotary engine cooling research. Determining the thermal boundary through one-dimensional simulation is simple and accurate, which is very necessary for the study of cooling problems based on conjugate heat transfer (CHT). This study investigates thermal boundary definition using an one-dimensional to three-dimensional (1D-3D) simulation model under steady state heat transfer, and innovatively uses a space-time averaging method to simulate the temperature distribution according to the thermal load characteristics of the WRE. The results show that the temperature data obtained by this method are in good agreement with the experiments, and the maximum temperature deviation under 4500 rpm is only 1.09 %, which indicates that the temperature distribution of the WRE can be accurately obtained by using the 1D-3D simulation model and the space-time averaging method. This study puts forward the generalized application of this method and the empirical formula for determining the thermal boundary conditions, which provides theoretical guidance and reference for the determination of thermal boundaries in the study of WRE cooling.

## 1. Introduction

A prevailing trend in internal combustion engine development is downsizing for enhanced power density [1,2], which poses fresh cooling challenges. Efficient cooling and thermal management boost engine efficiency, saving energy, fuel, and reducing emissions [3–5]. Ensuring engine component durability under thermal loads and shocks presents challenges [6], emphasizing the importance of cooling research. One example is the Wankel rotary engines (WREs), initially used in automobiles [7] but subsequently scaled down for applications in drones, range extenders, and more, offering benefits like high power-to-weight ratios, reduced mass, structural simplicity, and minimized vibration [8]. WREs feature elongated combustion chambers, leading to increased surface area and greater heat dissipation during combustion, resulting in elevated temperatures and thermal loads within the combustion zone. Consequently, the heat-resistant performance of WRE components faces heightened demands [9]. Air-cooled Wankel rotary engines experience a significant thermal load. During the early stages of engine development, thermal management becomes a crucial research area, as it directly

influences the performance and longevity of WREs.

In current WRE research, scholars mainly emphasize combustion, fuels, performance, and emissions [10–13], with limited attention to cooling and thermal management. Notably, crucial elements for cooling studies, such as establishing thermal boundary conditions, remain largely unexplored. Regarding cooling research for WREs, most scholars concentrate on improving cooling methods and enhancing cooling effectiveness, including the use of fins, liquid cooling, heat pipes, rotor cooling designs, and structures [8,14–17]. Conducting simulations to study cooling allows for the exploration of thermal loads for new, yet-to-be-manufactured engines and provides a reliable basis for improving heat dissipation structures in existing engines. Ji et al. [17] investigated the impact of rotor cooling on emissions and other factors using a combination of 1-D and 3-D simulations. Yang et al. [18] conducted finite element simulations on rotors with thermal barrier coatings to analyze the effects of temperature on rotor thermal stress and deformation. However, there is limited research on simulating cooling for WRE, and the accurate determination and application of thermal boundary conditions remain unclear. Gou et al. [19] proposed using the

\* Corresponding author.

E-mail address: [liujx@bit.edu.cn](mailto:liujx@bit.edu.cn) (J. Liu).

steady-state gas temperature of the three combustion chambers when the rotor is at its top dead center as the boundary condition for thermal source analysis in cooling the cylinder of a WRE. As can be seen from the above discussion, the determination of thermal boundary is the first step in WRE cooling research, and the existing studies focus on the improvement of heat dissipation means, without more detailed research on the precise thermal boundary. The treatment of the thermal boundary still remains in the stage of approximately taking the average gas temperature at a certain time. For WREs, however, the position, volume, and shape of the combustion chamber are constantly changing, which means that thermal boundary conditions for WREs need to consider both temporal and spatial factors. The rotational speeds of WREs are generally high, and their combustion chamber areas are relatively small. To ensure a more precise temperature field, it is necessary to maintain sufficiently accurate thermal boundaries.

Two approaches for simulation exist: combustion simulation and non-combustion simulation. The former involves modeling the engine's combustion process using software such as Fluent or Converge. For example, Taibani et al. [20] imported transient heat flux boundary conditions from the Forte combustion model to predict piston surface temperatures at various crankshaft angles. Fan et al. [21] used Fluent with User defined functions (UDF) and dynamic grids to simulate a single combustion chamber in a WRE, focusing on vortex evolution and average turbulence kinetic energy, but they didn't address WRE cooling. Taskiran et al. [22] employed dynamic grids to study volume efficiency, flow characteristics, and gas temperatures in three combustion chambers, highlighting the challenge of modeling the rotor's eccentric motion through UDFs. Mizuno et al. [23] calculated the heat transfer coefficient (HTC) on the piston top surface using a 3-D combustion model and applied it as a boundary condition. However, a significant issue with this method is the large time-scale difference between the CFD calculations of in-cylinder flow and the solid heat transfer simulations in the chamber components. It may require many cycles to achieve convergence. Regarding the first "combustion simulation" approach, for Fluent, the challenges lie in the development of dynamic grids and the implementation of the combustion process. As for Converge, despite its built-in SuperCycling functionality for solving steady-state temperature fields [24,25], it grapples with difficulties in achieving a well-sealed fluid-solid conjugate heat transfer (CHT) model. Furthermore, employing combustion simulation to obtain temperature fields in WREs incurs substantial computational expenses, making it an inefficient solution. As a result, in reciprocating piston engines, combustion chamber wall temperature is often simplified, neglecting spatial non-uniformity and time-varying characteristics [26]. In the heat transfer simulation of the engine assembly, typically, third type boundary conditions based on empirical equations or 1-D combustion models are used to simplify convective heat transfer on the gas side [27,28]. Ji et al. [17] used this combined 1D-3D simulation approach to simulate the cooling effectiveness of rotor fins for heat dissipation. Some researchers have also studied simplified combustion processes for boundary condition application. Broatch et al. [29] used the rate of heat release (RoHR) obtained from simulations as a source term for the energy equation to optimize the computational time of internal combustion engine conjugate heat transfer simulations. Their research offers some valuable methods for thermal boundary acquisition, which can serve as a reference for Wankel rotary engines. However, their study cannot be directly applied to Wankel rotary engines with space-time transformation characteristics. 3D combustion simulation itself will occupy a lot of computing resources, which is a non-negligible burden for the study of cooling problems. 1D simulation is very convenient to obtain thermal boundary, but the existing research is basically blank in the field of obtaining WRE thermal boundary with space-time transformation characteristics in 1D simulation. Therefore, it is necessary to develop a more reasonable method to obtain accurate thermal boundary conditions through 1D simulation for the existing WRE cooling research.

This study developed a 1-D model of a WRE and used gas chamber

temperature and convective heat transfer coefficient as boundary conditions for the inner wall. It also examined methods for applying boundary conditions considering motion characteristics and investigated thermal boundary conditions accounting for position changes and time averaging. The method proposed in this study combines the characteristics of 1D simulation and convenience, considers the motion law of WRE combustor and the characteristics of combustion occurring at a fixed position, and adopts the space-time averaging method as the thermal boundary applying method under the steady-state working condition of WRE, realizing the innovation of WRE steady-state thermal boundary. The 3D heat transfer simulation obtained the temperature distribution and the temperature value of the temperature measurement point, and its accuracy was verified by experiments. The maximum temperature difference was 1.09 % at 4500 rpm. Finally, based on the simulation data, the empirical formula of space-time averaging method is obtained, which does not depend on the specific fuel used in WRE, and provides a basis for the determination of thermal boundary in future WRE cooling research.

## 2. Methodology

### 2.1. Engine specifications

The experimental validation was conducted on a 70 cc single-rotor, dual-spark plug engine developed in-house by our research team. The engine operates on gasoline as its fuel source and is equipped with six internal temperature sensors located within the cylinder to monitor the temperature of the WRE. The key technical specifications and schematic of the WRE are presented in Table 1 and Fig. 1, respectively.

### 2.2. One-dimensional simulation

The thermal boundary conditions for the 3-D heat transfer simulation are provided by a 1-D model constructed using AVL-BOOST, as depicted in Fig. 2.

In the 1-D simulation, the combustion portion employs the Vibe 2 Zone model, which requires the same inputs as a single Vibe function [30]. This function, also known as Wiebe function, was originally proposed by Wiebe, and translated into German by professor Franz Meissner in 1970 [31]. The Vibe model is used to calculate the Heat Release Rate (HRR) as described in Equation (1):

$$x_b = 1 - \exp \left\{ -a \left( \frac{\theta - \theta_0}{\Delta\theta} \right)^{m+1} \right\} \quad (1)$$

where  $x_b$  is the cumulative mass fraction,  $\theta$  is the crank angle,  $\theta_0$  is the start of combustion angle,  $\Delta\theta$  represents the duration of combustion,  $a$  is a characteristic parameter related to the degree of complete combustion, and  $m$  represents the shape parameter of the Vibe model [32]. The Vibe 2 Zone model computes not a mass-averaged temperature but two

**Table 1**  
Specifications of the WRE.

| Parameter         | Value             |
|-------------------|-------------------|
| Generating radius | 52.5 mm           |
| Eccentricity      | 7.5 mm            |
| Width of rotor    | 33.75 mm          |
| Number of rotors  | 1                 |
| Cooling method    | Air cooled        |
| Compression ratio | 10.5              |
| Displacement      | 0.07 L            |
| Ignition source   | Double spark plug |
| Ignition timing   | 30 BTDC           |
| Intake opening    | 80 ATDC           |
| Intake closure    | 40 ABDC           |
| Exhaust opening   | 60 BBDC           |
| Exhaust closure   | 70 ATDC           |

temperatures (burned and unburned regions) [33]. Additionally, this model can predict the engine's knocking characteristics [34]. For the shape parameter  $m$ , it is set to 3 based on references [35], while the characteristic parameter  $a$  is set to 5 [36]. These parameter settings account for incomplete combustion scenarios.

The Woschni 1978 model [37] is employed for calculating combustion chamber heat transfer, utilizing the Woschni equation for HTC:

$$\alpha_w = 130 \cdot D^{-0.2} \cdot p_c^{0.8} \cdot T_c^{-0.53} \cdot \left[ C_1 \cdot c_m + C_2 \cdot \frac{V_D \cdot T_{c,1}}{P_{c,1} \cdot V_{c,1}} \cdot (p_c - p_{c,o}) \right]^{0.8} \quad (2)$$

$$\left. \begin{aligned} x &= e \cos \alpha + R \cos \left( \frac{\alpha}{3} + \phi \right) + a \cos \left( \frac{\alpha}{3} + \phi \right) \\ y &= e \sin \alpha + R \sin \left( \frac{\alpha}{3} + \phi \right) + a \sin \left( \frac{\alpha}{3} + \phi \right) \end{aligned} \right\} \quad (3)$$

where  $e$  is the eccentricity,  $R$  is the rotor radius,  $\alpha$  is the eccentric axis rotation angle,  $a_t$  is the translation distance, and  $\phi$  is the oscillation angle. Based on this, the trajectory of a point at a distance  $a'$  from the midpoint of the line connecting the two vertices of the rotor is given by:

$$\left. \begin{aligned} x &= 2e \cos \alpha + R \left[ \cos \frac{\alpha}{3} + \cos \left( \frac{\alpha+2\pi}{3} \right) \right] \\ &+ a_t \left[ \frac{3e \cos \alpha + R \cos \frac{\alpha}{3}}{\left( 9e^2 + R^2 + 6eR \cos \frac{2}{3}\alpha \right)^{1/2}} + \frac{3e \cos(\alpha+2\pi) + R \cos \left( \frac{\alpha+2\pi}{3} \right)}{\left( 9e^2 + R^2 + 6eR \cos \frac{2}{3}(\alpha+2\pi) \right)^{1/2}} \right] + a' \cos \left( \frac{\alpha+\pi}{3} \right) \\ y &= 2e \sin \alpha + R \left[ \sin \frac{\alpha}{3} + \sin \left( \frac{\alpha+2\pi}{3} \right) \right] \\ &+ a_t \left[ \frac{3e \sin \alpha + R \sin \frac{\alpha}{3}}{\left( 9e^2 + R^2 + 6eR \cos \frac{2}{3}\alpha \right)^{1/2}} + \frac{3e \sin(\alpha+2\pi) + R \sin \left( \frac{\alpha+2\pi}{3} \right)}{\left( 9e^2 + R^2 + 6eR \cos \frac{2}{3}(\alpha+2\pi) \right)^{1/2}} \right] + a' \sin \left( \frac{\alpha+\pi}{3} \right) \end{aligned} \right\} \quad (4)$$

where  $C_1 = 2.28 + 0.308 \cdot c_u / c_m$ ;  $C_2 = 0.00324$ ;  $D$  represents the cylinder bore diameter;  $c_m$  is the mean piston velocity;  $c_u$  is the circumferential velocity;  $V_D$  is the displacement volume per cylinder;  $p_{c,o}$  stands for the mean effective pressure in the cylinder, in bar;  $T_{c,1}$  is the cylinder internal temperature at the point of valve closure; and  $P_{c,1}$  is the cylinder internal pressure at the point of valve closure, in bar.

### 2.3. Partitioning and averaging methods

The purpose of partitioning into blocks is to obtain time-averaged boundary conditions for each block. Esfahanian et al. [38] found that using spatially and temporally averaged combustion side heat flux boundary conditions is an appropriate approach within the engineering approximation range. Sun et al. [39] found that under steady-cycle heat flux boundary conditions, the convergence speed of solid temperature is independent of the fluctuation characteristics of the boundary condition, and the fluctuation magnitude of solid temperature quickly establishes and does not change with time. Time-averaged boundary conditions can effectively represent steady-state thermal boundary conditions.

The inner walls of the WRE are divided into blocks. This process consists of two steps: first, depicting the shapes traversed by the combustion chamber, and second, partitioning the geometric region depicted. Heat exchange occurs between the gases inside the combustion chamber and the rotor, cylinder, and housing simultaneously. However, the contact area between the rotor and the housing is very small, so it can be approximated that there is no heat conduction between them. Therefore, when simulating the temperature field of the entire WRE, only convective heat exchange between the gases and the housing is considered. Since the shape and position of the combustion chamber change constantly, the approximate shape it passes through is determined by drawing the trajectory of the midpoint of the line connecting the adjacent two triangular tips on one side of the rotor. The actual cylinder shape is known to be [40]:

The two vertices are actually a planar view of the line segment where the rotor is in contact with the cylinder trochoid curve, and they move on the trajectory described by the cylinder trochoid curve equation. Firstly, the motion trajectory of the midpoint of the connecting line of two vertices is obtained, and then on the basis of the trajectory equation, the parallel motion trajectory with distance  $a'$  can be obtained, which is the trajectory shown by equation (4).

The thermal boundaries will be partitioned and defined on the outer periphery of this shape. Secondly, the partitioned shape will be subdivided into blocks, with the outer region divided into 24 blocks based on polar coordinates with the midpoint of the WRE's eccentric axis as

![Schematic diagram of the WRE (Wankel Rotary Engine) showing the rotor, cylinder wall, eccentric shaft, and intake/exhaust ports. The diagram includes a coordinate system (x, y) and labels for the bottom and top dead centers, T-plug, and L-plug. The rotor is shown in three positions, and the combustion chamber is highlighted with a dashed line. Angles 540°, 270°, 810°, and 0°/1080° are marked around the circle.](ced89c429132a719cb6021326e0bc7a6_img.jpg)

Schematic diagram of the WRE (Wankel Rotary Engine) showing the rotor, cylinder wall, eccentric shaft, and intake/exhaust ports. The diagram includes a coordinate system (x, y) and labels for the bottom and top dead centers, T-plug, and L-plug. The rotor is shown in three positions, and the combustion chamber is highlighted with a dashed line. Angles 540°, 270°, 810°, and 0°/1080° are marked around the circle.

Fig. 1. Schematic of the WRE.

![Fig. 2. The WRE model in the AVL-BOOST. The diagram shows a schematic of the WRE model with various components: ED1 (Electric Drive), E1 (Electric Motor), MC1 (Mechanical Coupling), PID1 (Proportional-Integral-Derivative controller), MNT1 (Magnetic Bearing), RP1 (Rotor Position Sensor), R1 (Resistor), and PL1 (Power Limit). Below these is a timeline from SB1 to SB2, marked with points 5, 11, 1, 2, 3, 4, and 11, with measuring points MP-1, MP-2, MP-3, MP-4, MP-5, and MP-6 indicated.](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

Fig. 2. The WRE model in the AVL-BOOST. The diagram shows a schematic of the WRE model with various components: ED1 (Electric Drive), E1 (Electric Motor), MC1 (Mechanical Coupling), PID1 (Proportional-Integral-Derivative controller), MNT1 (Magnetic Bearing), RP1 (Rotor Position Sensor), R1 (Resistor), and PL1 (Power Limit). Below these is a timeline from SB1 to SB2, marked with points 5, 11, 1, 2, 3, 4, and 11, with measuring points MP-1, MP-2, MP-3, MP-4, MP-5, and MP-6 indicated.

Fig. 2. The WRE model in the AVL-BOOST.

the origin, and each block spanning 15 degrees. The resulting blocks will be numbered, with the first block located at the top dead center (TDC) and biased towards the rotor's rotational direction assigned the number 1, incrementing in the rotor's rotational direction, sequentially

numbered as 2, 3, and so on, with the final 24th block connected to the first block.

For each block, it is necessary to separately determine the gas temperature and HTC. The specific procedure is as follows. The data for gas temperature and HTC obtained from 1-D simulation will be evenly divided into 24 blocks based on the crankshaft angle from 0 to 1080 degrees. The values within these 24 blocks will be time-averaged to obtain 24 sets of averaged gas temperature and HTC values. The calculation formula is as follows [41]:

$$h_{i,gm} = \frac{\int_{0}^{\frac{1}{4}\pi} h_g d\alpha}{\frac{1}{4}\pi} \quad (5)$$

$$T_{i,gm} = \frac{\int_{0}^{\frac{1}{4}\pi} T_g h_g d\alpha}{\frac{1}{4}\pi h_{i,gm}} \quad (6)$$

where  $h_{i,gm}$  represents the average HTC for the  $i$ -th time block;  $h_g$  represents the actual HTC;  $T_{i,gm}$  represents the average gas temperature for the  $i$ -th time block;  $T_g$  represents the actual gas temperature, and  $\alpha$  represents the crankshaft angle.

For a WRE, each combustion chamber occupies approximately 120° of angular space at any given moment, which corresponds to 8 blocks. This implies that at any given time, approximately 8 of these divided blocks have roughly the same average gas temperature and HTC values. Therefore, the rotational process of the combustion chamber can be approximated as the continuous rotation of these 8 consecutive blocks. For example, at the initial moment, the first, second, third, fourth,

![Fig. 3(a). Blocks numbering rules. A schematic of a WRE combustion chamber showing 24 numbered blocks (1-24) arranged in a circle. A measuring point (MP-1) is indicated at the top. A counter-clockwise rotation arrow is shown in the center.](37a6ab1d23efb9dc00cfae09d353b1da_img.jpg)

Fig. 3(a). Blocks numbering rules. A schematic of a WRE combustion chamber showing 24 numbered blocks (1-24) arranged in a circle. A measuring point (MP-1) is indicated at the top. A counter-clockwise rotation arrow is shown in the center.

(a) Blocks numbering rules

![Fig. 3(b). Blocks locations. Five cross-sectional views of the WRE rotor showing the location of the 24 thermal boundary setting blocks. The blocks are highlighted in orange, showing their spatial distribution around the combustion chamber.](c97b176986d994192dd844e17cd08e3a_img.jpg)

Fig. 3(b). Blocks locations. Five cross-sectional views of the WRE rotor showing the location of the 24 thermal boundary setting blocks. The blocks are highlighted in orange, showing their spatial distribution around the combustion chamber.

(b) Blocks locations

Fig. 3. Schematic of 24 thermal boundary setting blocks.

twenty-first, twenty-second, twenty-third, and twenty-fourth blocks are subjected to the average gas temperature and HTC of the first block. This continues until a full cycle is completed and returns to the initial position, involving the first, second, third, fourth, and twenty-first, twenty-second, twenty-third, and twenty-fourth blocks. For example, for a WRE operating at 4000 rpm, the approximate time it takes to rotate through one block can be calculated as follows:

$$t = \frac{\pi}{4000} \times \frac{1}{60} \times 2\pi \quad (7)$$

At each time interval of 0.001875 s, a change occurs in the combustion chamber's block. For every 0.045 s, the rotor completes one full revolution, and the combustion chamber blocks undergo 24 changes, aligning with the actual process. Furthermore, it's important to note that a WRE typically has three combustion chambers, each phased  $120^\circ$  apart. Therefore, the motion pattern for the next combustion chamber can be obtained by lagging it by  $120^\circ$ , which corresponds to  $360^\circ$  in terms of crankshaft angle. The division of these 24 blocks is illustrated in Fig. 3.

The space-time averaging method is proposed here in order to solve the space-time transformation problem of thermal boundary conditions of WRE. Specifically, when the first combustion chamber is located in blocks 1, 2, 3, 4 and 21, 22, 23, 24, the second combustion chamber is located in blocks 13, 14, 15, 16 and 17, 18, 19, 20, while the third combustion chamber is located in blocks 5, 6, 7, 8 and 9, 10, 11, 12. The variation law of each combustion chamber is the same as that of the first combustion chamber, from which the numerical changes of gas temperature and HTC in each of the 24 blocks can be calculated. The values of gas temperature and HTC of each block can be calculated separately, and the values of gas temperature and HTC of each block can be obtained by averaging them in a rotation period.

As a comparison, another 1D simulation data processing method, partial averaging method, is proposed. The partial averaging method also follows the figure "8" profile and the geometric region of the block, but there are different processing methods for the data of gas temperature and HTC. The data in the range of the average gas temperature or the average HTC applied on each block of the partial averaging method is divided into 24 parts, and each data is directly averaged and assigned to the corresponding numbered block. For example, the average gas temperature and the average HTC in the crankshaft angle of  $0 \sim 45^\circ$  will be directly assigned to the first block, which is the boundary condition application method used in the partial averaging method.

After the engine has been running for some time, the temperature tends to reach a steady state. Regardless of how gas temperature and heat transfer coefficients change within a cycle, as long as the WRE operates under stable conditions, the heat flux absorbed by the flame face from the gases remains constant within each cycle.

![Figure 4: A dual-axis line graph showing Gas temperature (K) and Heat transfer coefficient (W/(m^2·K)) versus Time (s). The Gas temperature (orange line) fluctuates between approximately 1000 K and 1600 K. The Heat transfer coefficient (blue line) fluctuates between approximately 100 W/(m^2·K) and 700 W/(m^2·K). Both show a periodic, figure-8 like pattern.](bc04d002fc79e8a3637b1552ac3361e6_img.jpg)

| Time (s) | Gas temperature (K) | Heat transfer coefficient (W/(m <sup>2</sup> ·K)) |
|----------|---------------------|---------------------------------------------------|
| 0.000    | 1000                | 100                                               |
| 0.002    | 1400                | 700                                               |
| 0.004    | 1600                | 100                                               |
| 0.006    | 1400                | 700                                               |
| 0.008    | 1000                | 100                                               |
| 0.010    | 1000                | 100                                               |
| 0.012    | 1400                | 700                                               |
| 0.014    | 1600                | 100                                               |
| 0.016    | 1400                | 700                                               |
| 0.018    | 1000                | 100                                               |
| 0.020    | 1000                | 100                                               |
| 0.022    | 1400                | 700                                               |
| 0.024    | 1600                | 100                                               |
| 0.026    | 1400                | 700                                               |
| 0.028    | 1000                | 100                                               |
| 0.030    | 1000                | 100                                               |
| 0.032    | 1400                | 700                                               |
| 0.034    | 1600                | 100                                               |
| 0.036    | 1400                | 700                                               |
| 0.038    | 1000                | 100                                               |
| 0.040    | 1000                | 100                                               |
| 0.042    | 1400                | 700                                               |
| 0.044    | 1600                | 100                                               |
| 0.046    | 1400                | 700                                               |
| 0.048    | 1000                | 100                                               |

Figure 4: A dual-axis line graph showing Gas temperature (K) and Heat transfer coefficient (W/(m^2·K)) versus Time (s). The Gas temperature (orange line) fluctuates between approximately 1000 K and 1600 K. The Heat transfer coefficient (blue line) fluctuates between approximately 100 W/(m^2·K) and 700 W/(m^2·K). Both show a periodic, figure-8 like pattern.

Fig. 4. Gas temperature and HTC of the first block in each cycle.

As shown in Fig. 4, the average gas temperature and HTC of the first block obtained by 1D simulation are extracted, which shows the changes of gas temperature and HTC of the first block in each cycle. The periodic fluctuation of gas temperature and HTC in each block is caused by the rotation of the rotor, due to the short duration of block transitions at the studied engine's speed, which is much smaller in time scale compared to the duration of steady-state conditions in the blocks, the corresponding gas temperature and HTC values can be directly averaged. The resulting averages are then applied as the third category of boundary conditions to the corresponding blocks in the 3-D simulation.

### 2.4. Three-dimensional simulation

#### 2.4.1. Governing equation

In the current research, the 3-D heat transfer model for the WRE operates under the following fundamental assumptions: Considering that the temperature variation along the outer surface of the WRE in the direction of airflow is minimal, for the purpose of simplifying calculations, it can be assumed that the physical properties of the cooling air remain constant and incompressible, and the airflow operates in a steady-state condition [42]. Since this study primarily simulates the operation of the WRE under steady-state conditions, mathematical equations for continuity, momentum, and energy are employed to model the behavior of stable, incompressible fluids and heat transfer processes. The expressions are as follows [17,43,44]:

$$\frac{\partial(u_i)}{\partial x_i} = 0 \quad (8)$$

$$\frac{\partial u_i u_j}{\partial x_i} = -\frac{1}{\rho} \frac{\partial p}{\partial x_i} + \frac{\partial}{\partial x_j} \left[ (v + v_t) \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right) \right] \quad (9)$$

$$\frac{\partial u_i T}{\partial x_i} = \rho \frac{\partial}{\partial x_i} \left( \left( \frac{v}{Pr} + \frac{v_t}{Pr_t} \right) \frac{\partial T}{\partial x_i} \right) \quad (10)$$

where  $\rho$  represents density,  $u$  is velocity,  $P$  denotes pressure,  $v$  represents dynamic viscosity,  $v_t$  represents turbulence viscosity,  $Pr$  is the Prandtl number,  $Pr_t$  is the turbulence Prandtl number and  $T$  represents temperature.

![Figure 5: A 3D cutaway view of a WRE housing showing the internal mesh for Fluent meshing. The mesh is composed of small, uniform hexahedral elements. The housing has a central circular opening and several radial cooling channels. The mesh is finer in the combustion chamber area and coarser in the cooling channels.](3cf4f743ab1967f5b295d4a954a3ad6d_img.jpg)

Figure 5: A 3D cutaway view of a WRE housing showing the internal mesh for Fluent meshing. The mesh is composed of small, uniform hexahedral elements. The housing has a central circular opening and several radial cooling channels. The mesh is finer in the combustion chamber area and coarser in the cooling channels.

Fig. 5. Mesh of housing in fluent meshing.

![Fig. 6. Schematic of inlet and outlet air flow. The diagram shows a 3D model of a WRE (Waste Heat Recovery Exchanger) within a rectangular housing. Blue arrows on the left side indicate the inlet air flow entering the housing. Red arrows on the right side indicate the outlet air flow exiting the housing. The WRE itself is a complex, finned structure mounted on a central shaft.](8e592c58b5074d79831ff650c2c636df_img.jpg)

Fig. 6. Schematic of inlet and outlet air flow. The diagram shows a 3D model of a WRE (Waste Heat Recovery Exchanger) within a rectangular housing. Blue arrows on the left side indicate the inlet air flow entering the housing. Red arrows on the right side indicate the outlet air flow exiting the housing. The WRE itself is a complex, finned structure mounted on a central shaft.

Fig. 6. Schematic of inlet and outlet air flow.

![Fig. 7. Independent test of mesh number. This is a dual-axis line graph. The x-axis represents the Grid number on a logarithmic scale from 1x10^6 to 5x10^6. The left y-axis is Maximum temperature (K) ranging from 523.0 to 524.4. The right y-axis is Pressure drop (Pa) ranging from 11.0 to 13.8. Two data series are plotted: Maximum temperature (orange line) and Pressure drop (blue line). Both series show a sharp increase from 1x10^6 to 2x10^6 and then remain relatively constant for higher grid numbers.](ac99eff233b8fe51d30f499e7413c345_img.jpg)

Fig. 7. Independent test of mesh number. This is a dual-axis line graph. The x-axis represents the Grid number on a logarithmic scale from 1x10^6 to 5x10^6. The left y-axis is Maximum temperature (K) ranging from 523.0 to 524.4. The right y-axis is Pressure drop (Pa) ranging from 11.0 to 13.8. Two data series are plotted: Maximum temperature (orange line) and Pressure drop (blue line). Both series show a sharp increase from 1x10^6 to 2x10^6 and then remain relatively constant for higher grid numbers.

Fig. 7. Independent test of mesh number.

The solid region of the model is described using the steady-state heat conduction equation, as given by [45]:

$$\frac{\lambda}{\rho c} \left( \frac{\partial^2 T}{\partial x^2} + \frac{\partial^2 T}{\partial y^2} + \frac{\partial^2 T}{\partial z^2} \right) \Big|_{solid} = 0 \quad (11)$$

where  $\lambda$  represents thermal conductivity,  $c$  represents specific heat capacity.

The description of the fluid-solid coupling at the interface between the fluid and solid regions is based on the Fourier heat equation and the convective heat transfer control equation, defined as:

$$-\lambda \left( \frac{\partial T}{\partial n} \right) \Big|_{solid} = h(T_w - T_c) \Big|_{fluid} \quad (12)$$

#### 2.4.2. Grid independence test

In this study, Fluent Meshing was utilized as the grid generation software. Polyhedral meshing was employed, which offers advantages over tetrahedral meshing, including a lower total number of elements, which can save computational costs. The final mesh model is depicted in Fig. 5. In the investigation of mesh independence, the flow field pressure drop and the maximum temperature were evaluated, with definitions for the inlet and outlet shown in Fig. 6. The relationship between pressure drop and maximum temperature with respect to five different grid sizes

![Fig. 8(a). 1D-3D temperature iteration curve at 3500 rpm. This line graph plots Average temperature (K) on the y-axis (450 to 500) against Calculation order on the x-axis (0 to 18). Two data series are shown: 1-D wall temperature data iteration (orange line) and 3-D wall temperature data iteration (blue line). Both series show a fluctuating trend, starting around 460 K and 460 K respectively, and converging towards a stable value of approximately 477 K by calculation order 14.](67020988167474f5810b295ba0fdc993_img.jpg)

Fig. 8(a). 1D-3D temperature iteration curve at 3500 rpm. This line graph plots Average temperature (K) on the y-axis (450 to 500) against Calculation order on the x-axis (0 to 18). Two data series are shown: 1-D wall temperature data iteration (orange line) and 3-D wall temperature data iteration (blue line). Both series show a fluctuating trend, starting around 460 K and 460 K respectively, and converging towards a stable value of approximately 477 K by calculation order 14.

(a) 1D-3D temperature iteration curve at 3500 rpm

![Fig. 8(b). Iterative circumferential temperature curve at 3500rpm. This line graph plots Temperature (K) on the y-axis (420 to 540) against Block number on the x-axis (0 to 25). Multiple data series are plotted for different temperatures: 489.82 K, 467.39 K, 485.72 K, 471.15 K, 481.78 K, 471.83 K, 478.23 K, 477.61 K, and 477.34 K. All series follow a similar U-shaped curve, starting at high temperatures (around 520-540 K) at block 0, decreasing to a minimum (around 435-440 K) between block 15 and 20, and then increasing back towards 520-540 K at block 25.](eba8385d0983fbda9dc1df0812273269_img.jpg)

Fig. 8(b). Iterative circumferential temperature curve at 3500rpm. This line graph plots Temperature (K) on the y-axis (420 to 540) against Block number on the x-axis (0 to 25). Multiple data series are plotted for different temperatures: 489.82 K, 467.39 K, 485.72 K, 471.15 K, 481.78 K, 471.83 K, 478.23 K, 477.61 K, and 477.34 K. All series follow a similar U-shaped curve, starting at high temperatures (around 520-540 K) at block 0, decreasing to a minimum (around 435-440 K) between block 15 and 20, and then increasing back towards 520-540 K at block 25.

(b) Iterative circumferential temperature curve at 3500rpm

Fig. 8. Schematic of circumferential temperature iteration data.

is illustrated in Fig. 7. It can be observed that there was minimal change in both evaluation metrics when the grid number increased from  $2.54 \times 10^6$  to  $4.96 \times 10^6$ . Therefore, for subsequent simulations, the model with a grid size of  $2.54 \times 10^6$  was chosen.

#### 2.4.3. Material properties and solution methods

In the simulation model, the cooling gas used is air, and the overall material of the engine is AlSi9Mg, with thermal properties as shown in Table 2. The simulation of the WRE's temperature field adopts a steady-state calculation method. The numerical computation methods in this paper include 1-D and 3-D simulations. The 1-D simulation primarily relies on AVL-BOOST to provide thermal boundary conditions for CFD simulation. As shown in Fig. 10, the accuracy of the model was verified through comparisons with the cylinder pressure and exhaust gas temperature of the WRE.

The 3-D simulation relies on FLUENT to obtain the temperature field of the entire WRE. Conjugate Heat Transfer methods provide a more convenient and accurate calculation approach for analyzing and calculating the temperature field of WREs [46]. The initial temperature values of the housing obtained from the 1-D simulation and the WRE temperature field obtained from the 3-D simulation are iterated multiple times to keep the numerical values within a reasonable error range. The specific method is as follows: the initial uniform temperature field is set in 1D simulation, the gas temperature and convective heat transfer coefficient are set to the thermal boundary conditions of three-dimensional

![Figure 9: Schematic overview and photograph of the experimental apparatus. (a) Photos of experimental equipment showing a dynamometer setup with a fan, ECU, CDI, EFI, WRE, air intake, and exhaust pipe. (b) Schematic of engine test bench showing the flow of air through a throttle valve, fuel injection, combustion chamber, and exhaust pipe, with sensors for in-cylinder pressure, K-type thermocouple, and oxygen sensor.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

(a) Photos of experimental equipment

(b) Schematic of engine test bench

Figure 9: Schematic overview and photograph of the experimental apparatus. (a) Photos of experimental equipment showing a dynamometer setup with a fan, ECU, CDI, EFI, WRE, air intake, and exhaust pipe. (b) Schematic of engine test bench showing the flow of air through a throttle valve, fuel injection, combustion chamber, and exhaust pipe, with sensors for in-cylinder pressure, K-type thermocouple, and oxygen sensor.

Fig. 9. Schematic overview and photograph of the experimental apparatus.

**Table 2**  
The property parameters of model material.

| Material                     | AlSi9Mg | Air                    |
|------------------------------|---------|------------------------|
| Density (kg/m <sup>3</sup> ) | 2650    | 1.225                  |
| Heat conductivity [W/(m-K)]  | 147     | 0.0242                 |
| Specific heat [J/(kg-K)]     | 753     | 1006.43                |
| Viscosity [kg/(m-s)]         | —       | $1.789 \times 10^{-5}$ |

simulation by space-time averaging method, and then the first wall temperature distribution is obtained by three-dimensional simulation. after processing, the temperature distribution is set to the wall temperature of 1D simulation, and iterated in this order until the average wall temperature converges. Fig. 8 shows the 1D-3D iteration process under 3500 rpm. A coupled algorithm is used for simulating the steady-state heat transfer model, and a second-order upwind discretization

scheme is applied for iterating the control equations. As a convergence criterion, the residual values of the equations are required to be less than  $10^{-6}$ .

#### 2.4.4. Boundary conditions

The gas temperature and HTC obtained from the 1-D simulation serve as the thermal boundary conditions for the CFD simulation. Air is introduced from the side of the WRE at a 45° angle, with the inlet boundary condition for the external flow around the rotor being a velocity inlet, with a temperature of 305 K and a flow velocity of 8.0 m/s, as determined experimentally. The outlet boundary condition is set as a pressure outlet, which is determined based on actual experimental conditions.

## 3. Results and discussion

### 3.1. Experimental validation

The experiments were conducted on an air-cooled, naturally aspirated, single-rotor WRE using gasoline as fuel. The main specifications and schematic diagram of the WRE are presented in Table 1 and Fig. 1. During the experiments, the air-fuel ratio was controlled to be around 14.7, the throttle valve opening remained stable at 35 %, and the fan's steady-state airflow velocity was set at 8.0 m/s. Steady-state cylinder pressures and temperatures at six measurement points were recorded at engine speeds of 3500, 4000, 4500 rpm. To enhance the accuracy of the experiments, all temperature data were measured at the same ambient temperature (305 K). Measurements were taken after reaching steady-state temperature and continued for more than 2 min. The thermocouple for measuring temperature in the test has been professionally calibrated to ensure that the error is within the marked range. At the same time, in order to further prevent the influence of errors, the thermocouple measurement positions were randomly exchanged in repeated tests to maximize the credibility of the test. The experimental equipment is shown in Fig. 9. In Fig. 9 (b), ECU is the abbreviation of electronic control unit, and EFI represents electric fuel injection, CDI represents capacitor discharge ignition. The uncertainties of the experimental instruments are detailed in Table 3.

**Table 3**  
Uncertainties of the experimental instruments.

| Instrument           | Accuracy          | Type             | Manufacturer |
|----------------------|-------------------|------------------|--------------|
| In-cylinder pressure | $\le \pm 0.5$ bar | KISTLER6052 CU20 | Kistler      |
| Temperature          | $\le \pm 0.15$ °C | WRNK-191         | —            |

![Figure 10(a): In-cylinder pressure (bar) vs. Eccentric angle (°EA) for simulation and experiment at 3500, 4000, and 4500 rpm. The plot shows a periodic pressure wave with a peak around 18 bar at 550°EA.](497bdee680ec2986bd4ec23f03fdec7a_img.jpg)

(a) In-cylinder pressure

Figure 10(a): In-cylinder pressure (bar) vs. Eccentric angle (°EA) for simulation and experiment at 3500, 4000, and 4500 rpm. The plot shows a periodic pressure wave with a peak around 18 bar at 550°EA.

![Figure 10(b): Exhaust gas temperature (K) vs. Engine speed (r/min) for simulation and experiment at 3500, 4000, and 4500 rpm. The temperature is approximately constant around 690 K.](09f2805f8f02dd446045cc4869422a78_img.jpg)

(b) Exhaust gas temperature

Figure 10(b): Exhaust gas temperature (K) vs. Engine speed (r/min) for simulation and experiment at 3500, 4000, and 4500 rpm. The temperature is approximately constant around 690 K.

Fig. 10. Model validation for in-cylinder pressure and exhaust gas temperature at different speed.

To validate the accuracy of the 1-D simulation, a comparison was made between the cylinder pressure and exhaust gas temperature obtained through simulation and the experimental results, as shown in Fig. 10. Experimental measurements were taken for cylinder pressures of the WRE at 3500, 4000, 4500 rpm, with the average air-fuel ratio sensor reading at 14.7. It can be observed that the 1-D simulation results for combustion chamber pressure and exhaust gas temperature closely match the experimental data. This indicates that the model is capable of effectively representing the operational processes of the WRE in question and possesses a high degree of simulation accuracy. The 3-D simulations have been validated by subsequent experimental procedures.

### 3.2. Temperature comparison between simulation and experiment

This section primarily analyzes the experimentally measured temperatures at six measurement points and compares them with the simulated temperatures to assess the correctness and reasonableness of the research methodology described in this paper. The experimental conditions included an ambient temperature of 305 K, atmospheric pressure, a fan airspeed of 8.0 m/s, an engine air-fuel ratio of 14.7, and engine speeds of 3500, 4000, 4500 rpm. Due to the heat resistance limitations of the WRE's materials, tests were not conducted at higher temperatures.

The temperature distribution obtained using the space-time averaging method is more uniform and relatively lower compared to the partial averaging method in Fig. 11. This difference is attributed to variations in the calculation principles and application methods of thermal boundaries.

The results shown in Fig. 12 indicate that the space-time averaging method exhibits good consistency between simulated and experimental temperatures at different speeds, with a maximum deviation of 1.09 % at 4500 rpm. In contrast, the maximum deviation for the partial averaging method is 6.07 %. Among the six measurement points, the highest temperature is observed at measurement point four, as it is located in the block with the highest heat release during combustion. The lowest temperature among the six measurement points is found at measurement point one, as it is distant from the combustion zone and closer to the intake, where fresh air provides some cooling.

In contrast, the partial averaging method results in a more inhomogeneous temperature distribution, with a maximum temperature of 578.9 K, which is 21.7 K (3.9 %) higher than the maximum temperature obtained using the space-time averaging method at 4500 rpm. As for

temperature measurement point 1, the difference reaches 5.7 %. This is due to the space-time averaging method's calculation of boundary conditions, which takes into account both spatial and temporal factors, providing a better representation of the temperature field under realistic engine operating conditions. Additionally, it's worth noting that although the partial averaging method's simulation results are relatively close to experimental results at some measurement points, its principles are not comparable to actual heat transfer conditions.

### 3.3. Method evaluation

#### 3.3.1. Comparison of two heat boundary methods

Directly assigning the mean temperature and heat transfer coefficient for a certain block for a given period of time inevitably leads to the problem of excessively high temperatures in the primary combustion region and lower temperatures in other regions. This is because during periods of relatively intense convective heat transfer, more blocks should participate in convective heat transfer, but this method assumes that only one block is involved in convective heat transfer during that time, resulting in noticeable errors.

The space-time averaging method, on the other hand, statistically considers the varying degrees of convective heat transfer experienced by different blocks through each cycle. It calculates the average gas temperature and heat transfer coefficient for each block within a certain time after reaching steady state, fully taking into account three factors: the combustion chamber shape, position, and steady-state time course. Therefore, it can obtain more accurate temperature results through a relatively simple approach.

#### 3.3.2. Analysis of the present heat boundary method

By comparing the gas temperature and HTC between the two methods, the relative relationship between them can be determined. Fig. 13 shows the relationship curves of the average gas temperature and average HTC ratio for each block between the partial averaging method and the space-time averaging method. It can be observed that the curve for the partial averaging method is steeper. This is because the values with significant variations are mainly concentrated in a few blocks. In contrast, the curve for the space-time averaging method is smoother due to better uniformity and continuity of the values.

For example, in the case of the first block at 4000 rpm, the HTC value for the partial averaging method is 1.97 times that of the space-time

![Figure 11: Temperature field of side housing and rotor housing at different speed. The figure consists of six hexagonal heatmaps arranged in two rows. The top row is labeled 'Time-Space Average' and the bottom row is labeled 'Partial Average'. Each row contains three heatmaps for engine speeds of 3500rpm, 4000rpm, and 4500rpm. A color bar on the right of each row indicates the temperature in Kelvin (K), ranging from 3.80e+02 (blue) to 5.70e+02 (red). The 'Time-Space Average' row shows more uniform temperature distributions, while the 'Partial Average' row shows more localized high-temperature spots, particularly near the combustion zone.](d6dce9b1cbed572f4183e3090cfdbd34_img.jpg)

Figure 11: Temperature field of side housing and rotor housing at different speed. The figure consists of six hexagonal heatmaps arranged in two rows. The top row is labeled 'Time-Space Average' and the bottom row is labeled 'Partial Average'. Each row contains three heatmaps for engine speeds of 3500rpm, 4000rpm, and 4500rpm. A color bar on the right of each row indicates the temperature in Kelvin (K), ranging from 3.80e+02 (blue) to 5.70e+02 (red). The 'Time-Space Average' row shows more uniform temperature distributions, while the 'Partial Average' row shows more localized high-temperature spots, particularly near the combustion zone.

Fig. 11. Temperature field of side housing and rotor housing at different speed.

![Figure 12: Temperature of simulation and experimental at different engine speeds. Three subplots (a) 3500 rpm, (b) 4000 rpm, and (c) 4500 rpm show Temperature (K) vs. Measuring point number (1 to 6). Each plot compares Time-Space Average (orange solid line), Partial Average (blue solid line), and Experiment (black dotted line).](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 12 consists of three subplots showing the temperature distribution across six measuring points for different engine speeds. The y-axis represents Temperature (K) and the x-axis represents Measuring point number (1 to 6). The legend for all plots indicates three data series: Time-Space Average (orange solid line), Partial Average (blue solid line), and Experiment (black dotted line).

| Engine Speed (rpm) | Measuring Point | Time-Space Average (K) | Partial Average (K) | Experiment (K) |
|--------------------|-----------------|------------------------|---------------------|----------------|
| 3500               | 1               | 435                    | 415                 | 435            |
|                    | 2               | 465                    | 430                 | 465            |
|                    | 3               | 490                    | 475                 | 490            |
|                    | 4               | 515                    | 535                 | 515            |
|                    | 5               | 505                    | 505                 | 505            |
|                    | 6               | 475                    | 465                 | 475            |
| 4000               | 1               | 455                    | 425                 | 455            |
|                    | 2               | 475                    | 440                 | 475            |
|                    | 3               | 505                    | 485                 | 505            |
|                    | 4               | 535                    | 565                 | 535            |
|                    | 5               | 525                    | 525                 | 525            |
|                    | 6               | 495                    | 480                 | 495            |
| 4500               | 1               | 460                    | 430                 | 460            |
|                    | 2               | 480                    | 450                 | 480            |
|                    | 3               | 505                    | 485                 | 505            |
|                    | 4               | 555                    | 575                 | 555            |
|                    | 5               | 535                    | 535                 | 535            |
|                    | 6               | 495                    | 495                 | 495            |

Figure 12: Temperature of simulation and experimental at different engine speeds. Three subplots (a) 3500 rpm, (b) 4000 rpm, and (c) 4500 rpm show Temperature (K) vs. Measuring point number (1 to 6). Each plot compares Time-Space Average (orange solid line), Partial Average (blue solid line), and Experiment (black dotted line).

Fig. 12. Temperature of simulation and experimental at different engine speeds.

averaging method. Similarly, for block 2, the gas temperature value for the partial averaging method is 1.49 times that of the space-time averaging method. These discrepancies are the primary sources of error in the partial averaging method.

However, as shown in the Fig. 13, it becomes clearer that due to the completely different distributions of gas temperature and HTC in the two methods' blocks, the temperature distributions obtained, even if they have similar trends, lack factors that can be directly compared. The similarity in trends is primarily because the size of each block is relatively small compared to the entire engine, and the differences in the third type boundary conditions do not lead to very noticeable differences in temperature simulation results. In addition, Fig. 13 also shows the circumferential distribution of WRE thermal boundary conditions composed of 24 blocks obtained by the space-time averaging method and the partial averaging method. The data obtained by the space-time averaging method is relatively flat, while the data obtained by the partial averaging method changes sharply, depending on whether the time change factor is taken into account.

### 3.4. Theoretical extensions

#### 3.4.1. Similarity to the Seale-Taylor formula

Similar to the heat boundary condition zoning method studied in this paper, Seale and Taylor proposed a radial zoning formula for heat transfer coefficient applied to the top surface to address the issue of varying heat boundary conditions at different positions in the piston top surface in 1970.

Seale and Taylor investigated the radial variation of heat transfer coefficients at the piston crown and the radial variation of fuel spray relative to the piston position. Fig. 14 shows the radial distribution of HTC along the piston crown in steady-state working conditions. The difference between their study of piston zoning and the zoning method described in this paper lies in the fact that Seale and Taylor's piston zoning method is focused on the radial position of the piston, while the method in this paper studies the distribution of circumferential heat boundary conditions in the WRE. Their research only focused on the distribution of HTC, while this study also examined the distribution of gas temperatures.

#### 3.4.2. The generalized universal equation

The gas temperature and heat transfer coefficient of each block on the inner wall of the WRE proposed in this study are proportional to the average of the gas temperature and heat transfer coefficient, each multiplied by a proportionality factor, similar to the empirical formula proposed by Seale and Taylor, as follows:

$$h_i = c_{i,h} \cdot h_{gm} \quad (13)$$

$$T_i = c_{i,T} \cdot T_{gm} \quad (14)$$

where  $h_i$  is the HTC for the  $i$ -th block,  $c_{i,h}$  is the HTC proportionality 

![Figure 13: Six subplots showing Gas temperature, HTC, and ratio of blocks under different engine speeds (3500, 4000, 4500 rpm) for two averaging methods (Space-Time Averaged and Partial Averaged).](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 13 consists of six subplots arranged in a 3x2 grid, showing the comparison of Space-Time Averaged and Partial Averaged methods for Gas temperature and Heat Transfer Coefficient (HTC) across 25 engine blocks at three different engine speeds: 3500 rpm, 4000 rpm, and 4500 rpm. Each subplot includes a Ratio plot showing the ratio of the two methods.

- (a) 3500 rpm, Gas temperature:** Gas temperature (K) ranges from 200 to 1800. Space-Time Averaged (orange solid line) and Partial Averaged (blue solid line) show similar trends, with the Partial Averaged method exhibiting higher peaks and lower troughs. The Ratio (dotted line) fluctuates between 0.50 and 1.50.
- (b) 3500 rpm, HTC:** Heat transfer coefficient (W/(m<sup>2</sup>·K)) ranges from 0 to 800. The Partial Averaged method (blue solid line) shows significantly higher peaks (up to ~600 W/(m<sup>2</sup>·K)) compared to the Space-Time Averaged method (orange solid line, peaks around 300 W/(m<sup>2</sup>·K)). The Ratio (dotted line) fluctuates between 0.0 and 2.5.
- (c) 4000 rpm, Gas temperature:** Similar to (a), but with more pronounced fluctuations in both Gas temperature and the Ratio, which reaches higher peaks (up to ~1.50).
- (d) 4000 rpm, HTC:** Similar to (b), but the Partial Averaged method shows even higher peaks (up to ~700 W/(m<sup>2</sup>·K)). The Ratio fluctuates between 0.0 and 2.5.
- (e) 4500 rpm, Gas temperature:** Similar to (a) and (c), with high-frequency fluctuations. The Ratio fluctuates between 0.50 and 1.50.
- (f) 4500 rpm, HTC:** Similar to (b) and (d), with the Partial Averaged method showing the highest peaks (up to ~800 W/(m<sup>2</sup>·K)). The Ratio fluctuates between 0.0 and 2.5.

Figure 13: Six subplots showing Gas temperature, HTC, and ratio of blocks under different engine speeds (3500, 4000, 4500 rpm) for two averaging methods (Space-Time Averaged and Partial Averaged).

Fig. 13. Gas temperature, HTC and ratio of blocks under different engine speeds of the two methods.



factor for the  $i$ -th block,  $h_{gm}$  is the average HTC.  $T_i$  is the gas temperature for the  $i$ -th block,  $c_{i,T}$  is the object temperature proportionality factor for the  $i$ -th block, and  $T_{gm}$  is the average gas temperature.

The HTC calculation equation proposed by Seale and Taylor is as follows [41]:

$$h(R_r) = \begin{cases} \frac{2h_{gm}}{[1 + \exp(C_0 \cdot L^{1.5})]} \exp(C_0 \cdot R_r^{1.5}) & , 0 < R_r < L \\ \frac{2h_{gm}}{[1 + \exp(C_0 \cdot L^{1.5})]} \exp[C_0 \cdot (2L - R_r)^{1.5}] & , R_r \ge L \end{cases} \quad (15)$$

where  $R_r$  represents the radial distance from the piston center,  $L$  represents the distance from the piston center to the location of maximum heat transfer coefficient on the surface, typically equal to the radius length of the combustion chamber throat, and  $C_0$  is a constant determined from experimental values, with a value of  $0.1 \text{ mm}^{-1.5}$  as taken in the article.

By comparing the gas temperature and HTC of each block using the space-time averaging method with the average gas temperature and average HTC over the entire process, the curve shown in Fig. 15 is obtained. It can be observed that the gas temperature from the space-time averaging method exhibits a trend of decreasing first and then increasing with crankshaft angle compared to the average gas temperature. Similarly, the HTC from the space-time averaging method shows a trend of decreasing first, followed by a slow increase, and finally a rapid increase with crankshaft angle compared to the average HTC. This trend aligns with the previous observations and represents the variations in boundary conditions over time and space.

Following the form of equation (15), based on the gas temperature ratio and HTC ratio obtained by space-time averaging method and partial averaging method, combined with Fig. 15, the following equations are fitted:

$$\begin{aligned} Ratio_{T_{\text{gas}}} = & 0.9809 \times e^{-\left(\frac{x-2.878}{7.567}\right)^2} + 0.7011 \times e^{-\left(\frac{x-24.39}{3.555}\right)^2} - 0.07721 \times e^{-\left(\frac{x-6.722}{1.428}\right)^2} + \\ & 0.0939 \times e^{-\left(\frac{x-12.04}{2.959}\right)^2} + (1.151 \times 10^6) \times e^{-\left(\frac{x-2254}{386.5}\right)^2} \end{aligned} \quad (16)$$

$$\begin{aligned} Ratio_{HTC} = & 1.247 \times e^{-\left(\frac{x-26.16}{3.556}\right)^2} + 1.334 \times e^{-\left(\frac{x-1.386}{3.466}\right)^2} + 0.8015 \times e^{-\left(\frac{x-15.58}{12.98}\right)^2} + \\ & 0.6195 \times e^{-\left(\frac{x-11.64}{2133}\right)^2} \end{aligned} \quad (17)$$

where  $x$  represents the block numbers,  $Ratio_{T_{\text{gas}}}$  represents the converted gas temperature ratio, and  $Ratio_{HTC}$  represents the converted convective heat transfer coefficient ratio, as shown in Fig. 16. Utilizing this relationship, the gas temperature and HTC obtained from 1-D simulations can be rapidly converted into applicable third-type boundary conditions, which account for both temporal and spatial averaging.

By using the Gaussian fitting formula, a fitting equation for the mean transformation of gas temperature and HTC has been derived. Its significance lies in the ability to calculate third-type thermal boundary conditions applicable to the entire inner wall surface of the WRE based on the average gas temperature or HTC obtained through simulations

![Figure 14: Radial variation of heat transfer coefficient across piston crown relative to piston. The graph plots HTC/HTCmax (Y-axis, 0.3 to 1.0) against Radius/Half Bore Diameter (X-axis, 0.0 to 1.0). A blue line represents the HTC/HTCmax-Fitting, and red dots represent HTC/HTCmax-Experiment. The curve shows a peak of 1.0 at a radius of approximately 0.65, with experimental data points closely following the fitted curve.](fdcbd505a623f39366aa8a18ed847f84_img.jpg)

Figure 14: Radial variation of heat transfer coefficient across piston crown relative to piston. The graph plots HTC/HTCmax (Y-axis, 0.3 to 1.0) against Radius/Half Bore Diameter (X-axis, 0.0 to 1.0). A blue line represents the HTC/HTCmax-Fitting, and red dots represent HTC/HTCmax-Experiment. The curve shows a peak of 1.0 at a radius of approximately 0.65, with experimental data points closely following the fitted curve.

Fig. 14. Radial variation of heat transfer coefficient across piston crown relative to piston.[41].

over the entire rotation process. Moreover, the block numbers can be converted into crankshaft angles for broader applicability.

# 4. Conclusion

This study investigated a new thermal boundary condition application method for WREs by combining 1-D and 3-D simulations. The key findings and conclusions of this research are summarized as follows:

1. Combining 1-D and 3-D simulations provides a fast and accurate approach to simulate engine performance and cooling studies in WREs. Applying thermal boundaries by partitioning allows for obtaining highly realistic temperature distributions within the WRE, facilitating further investigations into heat dissipation.
2. Applying thermal boundaries to partitioned blocks cannot be accomplished solely through straightforward parameter averaging; it requires consideration of both time and the spatial location of the combustion chamber. The maximum temperature difference between the two calculation methods was found to be up to 5.7 % at 4500-rpm.

![Figure 15(a): Gas temperature ratio vs Block number. The y-axis is 'Gas temperature/Average gas temperature' (0.0 to 2.0) and the x-axis is 'Block number' (1 to 24). Three curves are shown for 3500rpm (blue), 4000rpm (orange), and 4500rpm (red). All curves start around 1.4, dip to a minimum around block 18 (approx. 0.6), and then rise back up to 1.4 by block 24.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 15(a): Gas temperature ratio vs Block number. The y-axis is 'Gas temperature/Average gas temperature' (0.0 to 2.0) and the x-axis is 'Block number' (1 to 24). Three curves are shown for 3500rpm (blue), 4000rpm (orange), and 4500rpm (red). All curves start around 1.4, dip to a minimum around block 18 (approx. 0.6), and then rise back up to 1.4 by block 24.

(a) Gas temperature ratio

![Figure 15(b): HTC ratio vs Block number. The y-axis is 'HTC/Average HTC' (0.0 to 2.0) and the x-axis is 'Block number' (1 to 24). Three curves are shown for 3500rpm (blue), 4000rpm (orange), and 4500rpm (red). All curves start around 1.6, dip to a minimum around block 10 (approx. 0.6), and then rise back up to 1.6 by block 24.](252ea48d02dce93965b91746fb376f35_img.jpg)

Figure 15(b): HTC ratio vs Block number. The y-axis is 'HTC/Average HTC' (0.0 to 2.0) and the x-axis is 'Block number' (1 to 24). Three curves are shown for 3500rpm (blue), 4000rpm (orange), and 4500rpm (red). All curves start around 1.6, dip to a minimum around block 10 (approx. 0.6), and then rise back up to 1.6 by block 24.

(b) HTC ratio

Fig. 15. Ratio of gas temperature and HTC to average value.

![Figure 16: Fitting curve and simulation ratio. The y-axis is 'Ratio' (0.0 to 2.0) and the x-axis is 'Block number' (1 to 24). The legend shows: Temperature fitting curve (orange solid line), HTC fitting curve (blue solid line), Temperature ratio-Simulation (orange open circles), and HTC ratio-Simulation (blue open circles). The temperature ratio follows the orange fitting curve, while the HTC ratio follows the blue fitting curve.](6279fafb3a874e174648eb907385c954_img.jpg)

Figure 16: Fitting curve and simulation ratio. The y-axis is 'Ratio' (0.0 to 2.0) and the x-axis is 'Block number' (1 to 24). The legend shows: Temperature fitting curve (orange solid line), HTC fitting curve (blue solid line), Temperature ratio-Simulation (orange open circles), and HTC ratio-Simulation (blue open circles). The temperature ratio follows the orange fitting curve, while the HTC ratio follows the blue fitting curve.

Fig. 16. Fitting curve and simulation ratio.

3. A systematic summary of the thermal boundary condition application method studied in this paper has been developed, leading to the formulation of basic empirical equations. Since these thermal boundary conditions do not involve heat dissipation, the equations can be applied to general single-rotor WREs. To utilize these equations, it is necessary to conduct 1-D simulations for the specific WRE of interest to obtain data on how cylinder gas temperature and HTC change with crankshaft angles.

# CRediT authorship contribution statement

**Baichuan Chen:** Conceptualization, Data curation, Methodology, Software, Validation, Writing – original draft. **Xiaocan Chai:** Writing – review & editing. **Jinxiang Liu:** Funding acquisition, Project administration, Supervision, Writing – review & editing.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Data availability

Data will be made available on request.

# References

- [1] R. Dhingra, S. Das, Life cycle energy and environmental evaluation of downsized vs. lightweight material automotive engines, *J. Clean. Prod.* 85 (2014) 347–358, <https://doi.org/10.1016/j.jclepro.2014.08.107>.
- [2] K. Ju, J. Kim, J. Park, Numerical prediction of the performance and emission of downsized two-cylinder diesel engine for range extender considering high boosting, heavy exhaust gas recirculation, and advanced injection timing, *Fuel* 302 (2021) 121216, <https://doi.org/10.1016/j.fuel.2021.121216>.
- [3] R. Burke, C. Brace, The effects of engine thermal conditions on performance, emissions and fuel consumption, *SAE International* (2010), <https://doi.org/10.4271/2010.01.0802>.
- [4] R. Rahmani, H. Rahnejat, B. Fitzsimons, D. Dowson, The effect of cylinder liner operating temperature on frictional loss and engine emissions in piston ring conjunction, *Appl. Energy* 191 (2017) 568–581, <https://doi.org/10.1016/j.apenergy.2017.01.098>.
- [5] C. Dere, C. Deniz, Effect analysis on energy efficiency enhancement of controlled cylinder liner temperatures in marine diesel engines with model based approach, *Energ. Conver. Manage.* 220 (2020) 113015, <https://doi.org/10.1016/j.enconman.2020.113015>.
- [6] Z. Li, J. Li, Y. Zhu, J. Guo, M. Li, Y. Luo, Evaluation of plastic deformation and prediction of thermal mechanical fatigue life of an Al-Si alloy piston for diesel engines, *Fatigue Fract. Eng. Mater. Struct.* 44 (2021), <https://doi.org/10.1111/ffe.13553>.
- [7] G.J. Thompson, Z.S. Wowczuk, J.E. Smith, Rotary engines – a concept review, *SAE International* (2003), <https://doi.org/10.4271/2003-01-3206>.
- [8] H. Meng, C. Ji, S. Wang, J. Yang, A review: Centorial progress and development of Wankel rotary engine, *Fuel* 335 (2023) 127043, <https://doi.org/10.1016/j.fuel.2022.127043>.
- [9] J. Nagahiro, Cooling and Durability of Air-cooled Wankel Rotary Engine for General Use (1) Problems on Cooling as well as Measures, *Japanese Soc. Agric. Mach.* 45 (1983) 169–176, <https://doi.org/10.11357/jsam1937.45.169>.
- [10] C. Ji, T. Su, S. Wang, B. Zhang, M. Yu, X. Cong, Effect of hydrogen addition on combustion and emissions performance of a gasoline rotary engine at part load and stoichiometric conditions, *Energ. Conver. Manage.* 121 (2016) 272–280, <https://doi.org/10.1016/j.enconman.2016.05.040>.
- [11] T. Su, C. Ji, S. Wang, L. Shi, J. Yang, X. Cong, Effect of spark timing on performance of a hydrogen-gasoline rotary engine, *Energ. Conver. Manage.* 148 (2017) 120–127, <https://doi.org/10.1016/j.enconman.2017.05.064>.
- [12] B. Fan, J. Pan, W. Yang, W. Chen, S. Bani, The influence of injection strategy on mixture formation and combustion process in a direct injection natural gas rotary engine, *Appl. Energy* 187 (2017) 663–674, <https://doi.org/10.1016/j.apenergy.2016.11.106>.
- [13] R. Zou, J. Liu, H. Jiao, J. Zhao, N. Wang, Combined effect of intake angle and chamber structure on flow field and combustion process in a small-scaled rotary engine, *Appl. Therm. Eng.* 203 (2022) 117652, <https://doi.org/10.1016/j.applthermaleng.2021.117652>.
- [14] K. Yamaoka, H. Tado, Improvements of the Rotary Engine with a Charge Cooled Rotor, *SAE International* (1972), <https://doi.org/10.4271/720466>.
- [15] J. Turner, R. Islam, G. Vorraro, M. Turner, S. Akhurst, N. Bailey, S. Addy, Investigations into steady-state and stop-start emissions in a wankel rotary engine with a novel rotor cooling arrangement, *SAE International* (2021), <https://doi.org/10.4271/2021-24-0097>.

- [16] W. Wu, Y.-R. Lin, L. Chow, A heat pipe assisted air-cooled rotary wankel engine for improved durability, power and efficiency, SAE International (2014), <https://doi.org/10.4271/2014-01-2160>.
- [17] C. Ji, X. Huang, Z. Yang, J. Yang, S. Wang, Potential improvement in performance and emissions of air-cooled rotary engine using novel enhanced cooling fins, Fuel 334 (2023) 126718, <https://doi.org/10.1016/j.fuel.2022.126718>.
- [18] Z. Yang, G. He, Effect of thermal barrier coating on thermal load of the rotor of the small aviation wankel engine, J. Phys. Conf. Ser. 2125 (2021) 012064, <https://doi.org/10.1088/1742-6596/2125/1/012064>.
- [19] Y. Gou, X. Zhong, Heat Transfer Simulation and Optimization of Cooling System for Micro Wankel Engines, Adv. Mat. Res. 490–495 (2012) 1237–1240, <https://doi.org/10.4028/www.scientific.net/AMR.490-495.1237>.
- [20] A. Taibani, M. Visaria, S. Krishnan, A combined Combustion-Conjugate heat transfer analysis for Design of partially insulated pistons, Appl. Therm. Eng. 208 (2022) 118210, <https://doi.org/10.1016/j.applthermaleng.2022.118210>.
- [21] B. Fan, J. Pan, A. Tang, Z. Pan, Y. Zhu, H. Xue, Experimental and numerical investigation of the fluid flow in a side-ported rotary engine, Energ. Conver. Manage. 95 (2015) 385–397, <https://doi.org/10.1016/j.enconman.2015.02.047>.
- [22] O.O. Taskiran, A.T. Calik, O. Akin Kutlar, Comparison of flow field and combustion in single and double side ported rotary engine, Fuel 254 (2019) 115651, <https://doi.org/10.1016/j.fuel.2019.115651>.
- [23] H. Mizuno, K. Ashida, A. Teraji, K. Ushijima, S. Takemura, Transient Analysis of the Piston Temperature with Consideration of In-cylinder Phenomena Using Engine Measurement and Heat Transfer Simulation Coupled with Three-dimensional Combustion Simulation, SAE Int J. Engines 2 (2009) 83–90, <https://doi.org/10.4271/2009-01-0187>.
- [24] S.P.K. Richards K., Pomraning E., CONVERGE v24 Manual, Convergent Science, Inc, 2018.
- [25] A.T.S. Wu, S. Keum, V. Sick, Large Eddy Simulations with Conjugate Heat Transfer (CHT) modeling of Internal Combustion Engines (ICEs), Oil Gas Sci. Technol. 74 (2019) 51, <https://doi.org/10.2516/ogst/2019029>.
- [26] Y. Li, H. Li, H. Guo, Y. Li, M. Yao, A numerical investigation on methane combustion and emissions from a natural gas-diesel dual fuel engine using CFD model, Appl. Energy 205 (2017) 153–162, <https://doi.org/10.1016/j.apenergy.2017.07.071>.
- [27] L. Liu, L. Zhang, D. Yang, Q. Zhang, D. Yu, L. Chen, Two-phase flow-based numerical investigation of the temperature maps of sodium-cooled exhaust valves in a turbocharged engine, Appl. Therm. Eng. 181 (2020) 115977, <https://doi.org/10.1016/j.applthermaleng.2020.115977>.
- [28] X. Margot, P. Quintero, J. Gomez-Soriano, J. Escalona, Implementation of 1D–3D integrated model for thermal prediction in internal combustion engines, Appl. Therm. Eng. 194 (2021) 117034, <https://doi.org/10.1016/j.applthermaleng.2021.117034>.
- [29] A. Broatch, P. Olmeda, X. Margot, J. Escalona, New approach to study the heat transfer in internal combustion engines by 3D modelling, Int. J. Therm. Sci. 138 (2019) 405–415, <https://doi.org/10.1016/j.ijthermalsci.2019.01.006>.
- [30] H. Wang, C. Ji, C. Shi, Y. Ge, H. Meng, J. Yang, K. Chang, Z. Yang, S. Wang, X. Wang, Modeling and parametric study of the performance-emissions trade-off of a hydrogen Wankel rotary engine, Fuel 318 (2022) 123662, <https://doi.org/10.1016/j.fuel.2022.123662>.
- [31] I.I. Vibe, *Brennverlauf und kreisprozess von verbrennungsmotoren*, VEB Verlag Technik, Berlin, 1970.
- [32] A. Kutlar, Ö. Cihan, Investigation of Parameters Affecting Rotary Engine by Means of a One Zone Thermodynamic Model, J. Energy Res. Technol. 144 (2021) 1–34, <https://doi.org/10.11115/1.4052615>.
- [33] A. Ibrahim, Optimizing a spark-ignition engine fuelled with methane using a two-zone combustion model, Energy Storage and Saving 1 (2022) 272–283, <https://doi.org/10.1016/j.enss.2022.09.002>.
- [34] A. Boost, Theory and users guide documentation, AVL List GmbH, 2016.
- [35] T.J. Norman, A performance model of a spark ignition Wankel engine: including the effects of crevice volumes, gas leakage, and heat transfer, Massachusetts Institute of Technology (1983).
- [36] M. Peden, M. Turner, J.W. Turner, N. Bailey, Comparison of 1-D modelling approaches for Wankel engine performance simulation and initial study of the direct injection limitations, SAE Technical Paper (2018).
- [37] G. Woschni, A Universally Applicable Equation for the Instantaneous Heat Transfer Coefficient in the Internal Combustion Engine, SAE International (1967), <https://doi.org/10.4271/670931>.
- [38] V. Esfahani, A. Javaheri, M. Ghaffarpour, Thermal analysis of an SI engine piston using different combustion boundary condition treatments, Appl. Therm. Eng. 26 (2006) 277–287, <https://doi.org/10.1016/j.applthermaleng.2005.05.002>.
- [39] C. Sun, B. Deng, J. Yang, R. Feng, C. Chen, A multi-time scales semi-decoupled CHT (Coupled Heat Transfer) model and its application on piston transient heat transfer simulation, Appl. Therm. Eng. 229 (2023) 120548, <https://doi.org/10.1016/j.applthermaleng.2023.120548>.
- [40] K. Yamamoto, *Rotary Engine*, Sankaido Co., Ltd, 1981.
- [41] W. Seale, D. Taylor, Spatial variation of heat transfer to pistons and liners of some medium speed diesel engines, Proc. Inst. Mech. Eng. 185 (1970) 203–218, [https://doi.org/10.1243/PIME\\_PROC\\_1970\\_185\\_030\\_02](https://doi.org/10.1243/PIME_PROC_1970_185_030_02).
- [42] W. Yaici, M. Ghorab, E. Entchev, 3D CFD analysis of the effect of inlet air flow maldistribution on the fluid flow and heat transfer performances of plate-fin-and-tube laminar heat exchangers, Int. J. Heat Mass Transf. 74 (2014) 490–500, <https://doi.org/10.1016/j.ijheatmasstransfer.2014.03.034>.
- [43] J.-F. Yang, M. Zeng, Q.-W. Wang, Numerical investigation on combined single shell-pass shell-and-tube heat exchanger with two-layer continuous helical baffles, Int. J. Heat Mass Transf. 84 (2015) 103–113, <https://doi.org/10.1016/j.ijheatmasstransfer.2014.12.042>.
- [44] A. El Maakoul, A. Laknizi, S. Saadeddine, M. El Metoui, A. Zaite, M. Meziane, A. Ben Abdellah, Numerical comparison of shell-side performance for shell and tube heat exchangers with trefoil-hole, helical and segmental baffles, Appl. Therm. Eng. 109 (2016) 175–185, <https://doi.org/10.1016/j.applthermaleng.2016.08.067>.
- [45] X. Chen, X. Yu, Y. Lu, R. Huang, Z. Liu, Y. Huang, A.P. Roskilly, Study of different cooling structures on the thermal status of an internal combustion engine, Appl. Therm. Eng. 116 (2017) 419–432, <https://doi.org/10.1016/j.applthermaleng.2017.01.037>.
- [46] A. Naderi, A. Qasemian, M.H. Shojaeefard, S. Sameizadeh, M. Younesi, A. Sohani, S. Hoseinzadeh, A smart load-speed sensitive cooling map to have a high-performance thermal management system in an internal combustion engine, Energy 229 (2021) 120667, <https://doi.org/10.1016/j.energy.2021.120667>.