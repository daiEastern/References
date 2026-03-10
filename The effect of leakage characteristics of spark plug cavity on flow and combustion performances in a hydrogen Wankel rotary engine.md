

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the International Journal of Hydrogen Energy](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the International Journal of Hydrogen Energy

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# The effect of leakage characteristics of spark plug cavity on flow and combustion performances in a hydrogen Wankel rotary engine

Jinxin Yang<sup>a,b,\*</sup> ![ORCID icon](17413706fd4997a1a4bdf85c6864eee1_img.jpg), Yijin Zhang<sup>a</sup>, Xiaoyu Cong<sup>c</sup>, Yu Sun<sup>a</sup>, Hanlin Li<sup>a</sup>, Zhenyu Yang<sup>a</sup>, Changwei Ji<sup>a</sup>

<sup>a</sup> College of Mechanical and Energy Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, China

<sup>b</sup> National Key Laboratory of Multi-perch Vehicle Driving Systems, Beijing, 100086, China

<sup>c</sup> Aerospace Times FeiHong Technology Company Limited, Beijing, 100094, China

## ARTICLE INFO

Handling Editor: Ramazan Solmaz

### Keywords:

Pure hydrogen  
Wankel rotary engine  
Leakage  
Flow field  
Combustion

## ABSTRACT

The hydrogen Wankel rotary engine (WRE) is an ideal power plant, which can meet the requirement of zero carbon emission and have a highly compatible between the high flame speed of fuel and the good high-speed performance of engine. However, the gas leakage is one of the key problems restricting the development of HWRE, especially the leakage at the spark plug cavity is the most serious. In this work, the effect of leading spark plug (LSP) cavity leakage on the flow and combustion performances of HWRE is investigated by the numerical simulation. The results show that with the decrease of LSP diameter, the values of fresh mixture leakage (FML) and residual gas leakage (RGL) are significantly reduced. The reduction of FML contributes to the improvement of engine economy, and the proper RGL helps to strengthen the flow field and the turbulent combustion process. Therefore, at the original LSP location, the indicated work and indicated thermal efficiency first increase and then decrease as the LSP diameter decreases. When the diameter is reduced to 9 mm, the indicated work and indicated thermal efficiency are the highest, which are 380.19 J and 38.38 %, respectively. In addition, when the LSP is located 6.5 mm to minor axis, which is the optimized position, although the reduction of LSP diameter significantly reduces the FML, the higher RGL results in the decrease of indicated thermal efficiency. This work can provide the design scheme and theoretical support for the application of HWRE in the field of transportation, marine and aerospace.

## 1. Introduction

The internal combustion engine (ICE) stands as a significant consumer of fossil fuels and a substantial contributor to environmental pollution. Alternative fuels such as natural gas, ethanol, and hydrogen are garnering considerable attention for use in ICEs. These alternative fuels can substantially alleviate the reliance on fossil fuels [1] and effectively reduce harmful exhaust emissions from ICEs [2]. Hydrogen possesses many advantages, such as high flame speed [3,4], short quenching distance [5], wide combustion limit [6,7] and so on. Importantly, hydrogen does not generate greenhouse gases such as carbon dioxide in its combustion process. Using hydrogen as a fuel benefits both the thermal efficiency and emissions of ICEs [8].

Due to their high power-to-weight ratio, fast operational speed [9], simple structure, and improved operational stability [10]. Compared

with the traditional reciprocating-piston engine (PE), Wankel rotary engine (WRE) is widely applied in many fields, including unmanned aerial vehicles in the military sector, automobiles, mobile generating unit, and range extenders for electric vehicles in the civilian sector [11]. At the same time, the WRE also possess drawbacks that need to be addressed, including higher emissions [12], lower thermodynamic efficiency and higher tendency for backfiring [13]. By utilizing hydrogen fuel in the WRE, hydrogen demonstrates the capacity to enhance operational efficiency while significantly reducing carbon emissions [14]. The hydrogen-fueled Wankel rotary engine (HWRE) are adapted pure hydrogen fuel properties and the structure of the WRE, which can achieve lower NOx emissions [15] and higher power output. But the gas leakage is a significant issue for HWRE and it significantly impacts

\* Corresponding author. College of Mechanical and Energy Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, China.

E-mail address: [yangjinxin@bjut.edu.cn](mailto:yangjinxin@bjut.edu.cn) (J. Yang).

<https://doi.org/10.1016/j.ijhydene.2025.02.136>

Received 18 November 2024; Received in revised form 2 February 2025; Accepted 8 February 2025

Available online 16 February 2025

0360-3199/© 2025 Hydrogen Energy Publications LLC. Published by Elsevier Ltd. All rights are reserved, including those for text and data mining, AI training, and similar technologies.

unburned mixture emissions [16] and leads to increased fuel consumption [17]. Furthermore, leakage could affect oil film thickness by significantly altering gas pressure [18], resulting in diminished lubrication effectiveness. McCuiston [19] investigated the impact of leakage on nitrogen oxide (NOx) emissions, revealing that an increase in apex seal leakage area leads to a significant reduction in final NOx concentrations. It can be seen that the gas leakage has a significant negative impact on the economy, power and emissions of the WRE.

Numerous reports have shown that the primary source of leakage in WREs is the apex seals [20], accounting for approximately 2/3 to 3/4 of the sum leakage [21]. The leakage of apex seals is affected by many factors, it comes mainly from three parts of leakage: spark plug cavity, side piece and running face [22]. Among them, the leakage of spark plug cavity is the most serious. For the dual spark plug ignited WRE, due to the large diameter of the leading spark plug (LSP) cavity and the high-pressure difference between the adjacent cylinders at the LSP location, the leakage of LSP cavity has the greatest influence on the leakage of the apex seals. Although WREs are designed with spark plugs mounted at the pressure equilibrium point of adjacent cylinders, gas leakage can still occur and directly affect the performance of the WRE.

It has been shown that when the speed is 2000 rpm of WRE, the leakage of spark plug cavity directly affects the flow field properties and flame propagation characteristics of in-cylinder mixtures, and accounting for about 29% of the total leakage [23]. This phenomenon indicates that the design and location and diameter of spark plugs play crucial roles in reducing apex seal leakage. Meanwhile, the leakage of apex seal can also lead to the reduction of in-cylinder pressure and the formation of squish flow, which has a significant impact on the in-cylinder mixture's formation and flow [24]. Near top dead center (TDC), a recirculating flow causes a squish flow weakens due to apex seal leakage [25]. In the WRE, this leakage flow dramatically alters fuel circulation and flame propagation. Jeng [26] investigated the effect of leakage by apex seal on the performance in the WRE through numerical simulations. They revealed that the burned gas with extremely high temperature and pressure leaks into the adjacent combustion chamber, thereby enhancing the fuel/air mixture in those chambers. However, lower pressure caused by combustion chamber leakage can lead to a decrease in indicated mean effective pressure (IMEP) and reduce power performance of the WRE [27]. Besides, Fan [28] explored the leakage effect of apex seal on the formation and variation of the in-cylinder mixtures' flow of WRE. They found that the leakage of apex seal could cause a considerable alteration to both the flow dynamics and flame propagation in the WRE. Furthermore, the fuel-air mixtures' formation and the flame propagation process are significantly impacted by the leakage of apex seal. The leakage of apex seal can both decrease the volumetric efficiency and significantly enhance vortices in the working chamber of the WRE at low speeds. Hsieh [29] compared the leakage properties of air and hydrogen, finding that hydrogen has a higher vortex number and leakage risk compared to air. In essence, HWREs face more serious leakage problems due to the low mass, small molecules and high diffusivity of hydrogen. Although the leakage of apex seal could alter the flow field and decrease the working performance, the LSP is the most crucial position of leakage. There is limited research concentrate on the leakage mechanism of LSP.

In the existing literature reports, most of the research on spark plug is carried out around the optimization of ignition strategy, such as ignition timing, ignition energy, dual spark plugs asynchronous ignition, and so on, which can improve the flame kernel development and flame propagation properties of HWRE [30]. Among them, double spark plugs exhibit fewer cycle-to-cycle variations, ensuring more stable combustion [31], higher maximum pressure [32], and higher maximum heat release rate (HRR) [33]. Harikrishnan's numerical simulation research [34] found that the distance between the spark plug and combustion chamber wall significantly affects the flame propagation speed and combustion efficiency of the WRE. Hwang [35] concluded that advancing the ignition time of LSP could also effectively improve the combustion

efficiency. In addition, Jiao et al. [36] studied the effect of near-wall surface ignition on WRE combustion performance, and the results indicated that it was also an effective method to enhance the turbulent combustion process. Besides, Morimoto's investigation [37] showed that the leakage of spark plug cavity lead to the pre-ignition and further results in the abnormal combustion of HWRE. In summary, although some scholars have already studied the performance of WRE and considered the effect of gas leakage, they have only analyzed it briefly and have not revealed the gas leakage process and mechanism of action in detail.

In order to fill this research gaps, this study investigated the effect of leakage characteristics of spark plug cavity on flow and combustion performances in a HWRE. In previous work [38], the in-cylinder flow and combustion performances in HWRE under different LSP locations are studied. It can be found that the leakage gas is minimized and the flame diffusion, combustion and working performance are facilitated after LSP position moved 6.5 mm to minor axis, which corresponded to optimal indicated thermal efficiency of the HWRE is to 38.29%. In order to further reveal the influence rule of leakage on the performance and the optimization idea of spark plug cavity position and structure design of HWRE. The LSP leakage mechanism are investigated using CONVERGE software and the effect of LSP cavity diameter on the gas leakage, combustion, and performance in a HWRE are examined.

## 2. Methodology

### 2.1. Geometric model of HWRE

This study is based on simulation modeling of Mazda 13B rotary engine using CONVERGE software [39]. The specific geometrical model of prototype WRE with two side exhaust ports is shown in Fig. 1. Due to the software can generates mesh based on the set base grid size automatically, and the function of adaptive mesh refinement (AMR) can refine the grid size according to temperature, velocity and pressure gradients. A 2 mm with AMR mesh is chosen for the investigation after taking calculation accuracy, time expenditure, and combustion results into consideration. In AMR settings, the max embedding level is 2 for temperature and velocity in combustion chamber, the sub-grid criterion for temperature and velocity is 20.0 K and 10.0 m/s, respectively.

Additionally, the 13B WRE utilizes a double spark plug system, comprising the LSP and trailing spark plug (TSP) for ignition. It can be seen from Fig. 1(b) that the LSP is on the exhaust port side and 23 mm from the minor axis, while the TSP is on the intake port side and 30 mm from minor axis. Furthermore, the rotor was rotated in a counterclockwise direction, chamber I is designated as the working chamber (or trailing chamber), whereas chamber II is identified as the leading chamber.

Fig. 1 also shows the location and hole diameters of LSP in this study. As it is shown in Fig. 1(c), the leakage is happened when the apex seal goes through the cavity of LSP. Fig. 1(d) shows the structure of the original LSP cavity, which has a diameter is 12.17 mm. Although five other hole diameters of LSP (3, 6, 8, 9 and 10 mm) are selected for testing, only three of them are displayed in Fig. 1(d) and mainly analyzed in this study.

In this paper, the engine speed, excess air ratio ( $\lambda$ ) and manifold absolute pressure of HWRE is 3000 rpm, 1.6 and 100 kPa respectively. Table 1 shows the specific geometrical model parameters and boundary conditions of the HWRE. Deviation and uncertainty are very important in experimental measurement and parameter setting [40,41], so the parameter setting and selection are carefully carried out in this paper. The structural parameters and the intake/exhaust phases are taken from the actual engine of Mazda 13b. The operating parameters, inlet temperature and exhaust pressure are taken from HWRE bench test. The wall temperature and spark plug area temperature are empirical values derived from HWRE bench test and theoretical calculations.

![Figure 1: Geometric model of HWRE and Leading spark plug. (a) 3D structure of HWRE showing rotor, chambers I, II, III, and ports. (b) 2D cross-section showing spark plug positions and angles (540°CA, 810°CA, 270°CA, 0/1080°CA). (c) Detailed view of spark plugs and rotor housing with dimensions 23 mm and 30 mm. (d) Comparison of spark plug hole diameters (9 mm, 6 mm, 3 mm) and the original diameter.](3cab54230d8ae3b786ddda81346602cc_img.jpg)

(a) Structure of HWRE

(b) Positions of LSP and TSP

(c) Location of LSP

(d) Holes diameters of LSP

Figure 1: Geometric model of HWRE and Leading spark plug. (a) 3D structure of HWRE showing rotor, chambers I, II, III, and ports. (b) 2D cross-section showing spark plug positions and angles (540°CA, 810°CA, 270°CA, 0/1080°CA). (c) Detailed view of spark plugs and rotor housing with dimensions 23 mm and 30 mm. (d) Comparison of spark plug hole diameters (9 mm, 6 mm, 3 mm) and the original diameter.

**Fig. 1.** Geometric model of HWRE and Leading spark plug

(a) Structure of HWRE (b) Positions of LSP and TSP

(c) Location of LSP (d) Holes diameters of LSP.

**Table 1**  
The geometrical parameters and initial & boundary conditions of HWRE.

| Parameters                           | Value                |
|--------------------------------------|----------------------|
| Generating radius/ $R$ (m)           | $105 \times 10^{-3}$ |
| Eccentricity/ $e$ (m)                | $15 \times 10^{-3}$  |
| Width of rotor/(m)                   | $80 \times 10^{-3}$  |
| Compression ratio                    | 10                   |
| Displacement/(L)                     | 0.654                |
| Intake timing/(°CA)                  | 3 (ATDC), 65 (ABDC)  |
| Exhaust timing/(°CA)                 | 50 (BBDC), 3 (BTDC)  |
| Engine speed/(rpm)                   | 3000                 |
| Inlet temperature/(K)                | 305                  |
| Wall temperature/(K)                 | 450                  |
| Exhaust pressure/(kPa)               | 100                  |
| Spark plug area temperature/(K)      | 600                  |
| Ignition timing (L-spark plug)/(°CA) | 5 (BTDC)             |
| Ignition timing (T-spark plug)/(°CA) | 5 (ABDC)             |

### 2.2. Turbulence model

The RNG  $k$ - $\epsilon$  model is a commonly applied model in turbulence simulation [42], which bases on the standard  $k$ - $\epsilon$  model combined with the stochastic perturbation method called Re-Normalization Group (RNG) to improve the equations for the turbulent kinetic energy ( $k$ ) and turbulent dissipation rate ( $\epsilon$ ). The RNG  $k$ - $\epsilon$  turbulence model can accurately describe the separation and reattachment phenomena in turbulent

flows and provide ideal results in calculating both high and low Reynolds number flows, which is suitable for capturing the turbulent flow information in the HWRE.

$$\frac{\partial \rho k}{\partial t} + \frac{\partial \rho u_i k}{\partial x_i} = \tau_{ij} \frac{\partial u_i}{\partial x_j} + \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_k} \frac{\partial k}{\partial x_j} \right) - \rho \epsilon + \frac{C_s}{1.5} S_s \quad (1)$$

$$\begin{aligned} \frac{\partial \rho \epsilon}{\partial t} + \frac{\partial (\rho u_i \epsilon)}{\partial x_i} &= \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_\epsilon} \frac{\partial \epsilon}{\partial x_j} \right) + C_{\epsilon 1} \rho \epsilon \frac{\partial u_i}{\partial x_i} \\ &+ \left( C_{\epsilon 1} \frac{\partial u_i}{\partial x_j} \tau_{ij} - C_{\epsilon 2} \rho \epsilon + C_{\epsilon 3} S_s \right) \frac{\epsilon}{k} + S - \rho R_\epsilon \end{aligned} \quad (2)$$

Here,  $S$  and  $S_s$  denotes the user-supplied source term and the source term representing interactions with the discrete phase (spray), respectively. It's important to notice that these are two different terms. Model constants for expansion and compression are called the  $C_{\epsilon i}$  terms. The Prandtl number is represented by  $Pr$ , and turbulent viscosity is denoted by  $\mu_t$ .

### 2.3. Combustion and emissions models

The Detailed Chemical Kinetics Solver (SAGE) contains the detailed chemical interactions to accurately predict reaction kinetics in complex combustion environments. Therefore, in this study, the SAGE combustion model was chosen to predict the combustion process for improving the overall calculation accuracy and performance optimization of the

HWRE. Since the generation of NO<sub>x</sub> during the combustion process of the HWRE is influenced by thermal-pathway NO<sub>x</sub>, this model was chosen to be suitable for describing NO<sub>x</sub> emissions. Furthermore, Stagni's [43] comprehensive chemical reaction mechanism is integrated with the SAGE combustion model, which improves prediction accuracy for most fuel-air mixtures combustion characteristics [44]. The main reactions of thermal NO<sub>x</sub> are as follow:

![](d66a303ccad4349249b03ca0865bd34f_img.jpg)

$$\begin{aligned} O + N_2 &\Rightarrow NO + N \\ N + O_2 &\Rightarrow NO + O \\ N + OH &\Rightarrow NO + H \end{aligned} \quad (3)$$

The model parameters of RNG k-ε and SAGE are set according to the default values given in the CONVERGE manual [39].

### 2.4. The experimental verification

In the CFD numerical simulation process, ensuring mesh independence is an important prerequisite to ensure the reliability of numerical simulation results. In CONVERGER software, AMR is a widely used technique for improving the accuracy and efficiency of numerical simulations. In this paper, mesh independence is verified on a HWRE with the speed of 3000 rpm,  $\lambda$  of 1.6, and hydrogen intake port injection.

The validations of grid independence and in-cylinder combustion pressure are shown in Fig. 2. As it is depicted in Fig. 2(a), due to the calculated result of 1 mm grid size is almost coincide with that of 2 mm with AMR, the grid independence is verified. In order to balance simulation accuracy and calculation time, the grid side of 2 mm with AMR is selected for subsequent numerical simulation. Fig. 2(b) displays the comparison of in-cylinder combustion pressure curves between calculated and experimental values. The experimental data are from the HWRE experiments, the details of the experimental system are described in our previous works [5]. Considering the important influence of test equipment and uncertainty [45,46], Table 2 is listed below. The calculated peak in-cylinder pressure is 0.2 bar higher than the experimental peak in-cylinder pressure. The error of crankshaft angle corresponding to peak in-cylinder is less than 1.5 °CA. The differences between the calculated value and the experimental value both of the peak in-cylinder pressure and the crank angle of peak in-cylinder pressure indicate that the verification is acceptable for HWRE.

## 3. Results and discussions

### 3.1. Influence of diameter of LSP cavity on leakage

The leakage affects the performance of HWRE obviously, especially when the apex seal passes the LSP cavity. For the LSP leakage, the process of residual gas leakage (RGL) is displayed in Fig. 3(a), and the

**Table 2**  
Experimental equipment information and their uncertainties.

| Parameter                     | Uncertainty          | Manufacturer | Type      |
|-------------------------------|----------------------|--------------|-----------|
| Engine speed                  | $\le \pm 1$ rpm      | Power link   | CAC6      |
| Torque                        | $\le \pm 0.4\%$ F.S. | Power link   | CAC6      |
| Hydrogen volumetric flow rate | $\le \pm 0.02$ L/min | Seven star   | D07-60B   |
| Air volume flow rate          | $\le \pm 0.1$ L/min  | Tociel       | 20 N060   |
| Air-to-fuel ratio             | $\le \pm 0.007$      | Horiba       | MEXA-730λ |
| In-cylinder pressure          | $\le \pm 0.03$ MPa   | Kistler      | 6117BFD17 |
| Inlet temperature             | $\le \pm 0.2$ °C     | Power Link   | PT1000    |
| Exhaust pressure              | 0.5%                 | Power Link   | ZXP800    |

process of fresh mixture leakage (FML) is depicted in Fig. 3(b). As is shown in Fig. 3(a), the first-half stage leakage is mainly the RGL, which leaks from the leading chamber (Chamber II) and LSP cavity to the working chamber (Chamber I). A small amount of RGL is through path I (from Chamber II to Chamber I), and most of the RGL is through path II (from LPS cavity to Chamber I). The residual gases entering the working chamber through leakage possess a higher temperature, which has been demonstrated to improve the thermal atmosphere of the mixture in chamber I. Concurrently, this phenomenon also affects the content of hydrogen, resulting in a slightly higher excess air ratio. Meanwhile, as is shown in Fig. 3(b), the second-half stage leakage is mostly the FML. The leakage process of fresh mixture is from the working chamber to the LSP cavity and the leading chamber. A small amount of FML is through path III (from Chamber I to Chamber II), while most of the FML is through path IV (from Chamber I to LPS cavity). During the second-half stage leakage, fresh mixture leaves the working chamber resulting in the escape of hydrogen, which can cause a reduction in the total energy in chamber I, resulting in a reduction in economy. In order to more clearly evaluate the influence of LSP cavity leakage, two leakage modes are defined in this study. Path I and Path III are applied to analyses the leakage between adjacent chambers (Leakage mode I), Path II and Path IV are applied to assess the leakage between LSP cavity and working chamber (Leakage mode II).

The leakage characteristics under different diameters of LSP cavity are displayed in Fig. 4. It can be seen that the leakage flow rates through the two leakage modes are the same order of magnitude, but the corresponding crank angle at which the leakage occurs is not consistent.

Fig. 4(a) and (b) display the leakage flow rate and mass in leakage mode I, respectively. As the diameter of LSP cavity reduces from 12.17 to 3 mm, the leakage gas mass decreases from  $4.04 \times 10^{-7}$  to  $2.84 \times 10^{-8}$  kg, and this value is decreased by 92.96 %, and the mass of FML is decreased from  $3.14 \times 10^{-7}$  to  $2.84 \times 10^{-8}$  kg (in color blue). Meanwhile, the mass of RGL is 0 kg when the diameter of LSP cavity is reduced to 3 mm (in color red). Fig. 4(c) and (d) show the leakage flow rate and mass in leakage mode II. The leakage mass decreases form  $4.75 \times 10^{-6}$  to

![Figure 2: (a) Validation of grid independence showing pressure vs crank angle for different grid sizes (2 mm grid with AMR, 1 mm grid, 2 mm grid, 4 mm grid). (b) Comparison of in-cylinder pressure between simulation and experiment.](2e24de1b1a3df92537debdd0e71f0e3f_img.jpg)

Figure 2 consists of two subplots. Subplot (a) shows the in-cylinder pressure (MPa) versus crank angle (°CA) from 460 to 620. It compares four grid configurations: '2 mm grid with AMR' (red line with circles), '1 mm grid' (yellow line with squares), '2 mm grid' (blue line with triangles), and '4 mm grid' (cyan line with diamonds). A vertical dashed line marks the Top Dead Center (TDC) at approximately 560 °CA. The curves for the 2 mm grid with AMR and the 1 mm grid are nearly identical, peaking at approximately 3.3 MPa at TDC. The 2 mm grid and 4 mm grid curves are slightly lower, peaking at approximately 3.1 MPa and 3.0 MPa respectively. Subplot (b) shows the in-cylinder pressure (MPa) versus crank angle (°CA) from 440 to 680. It compares 'Simulation' (red line with circles) and 'Experiment' (open circles). The simulation curve peaks at approximately 3.3 MPa at TDC, while the experimental data points are slightly lower, peaking at approximately 3.1 MPa at TDC. A vertical dashed line marks the TDC at approximately 560 °CA.

Figure 2: (a) Validation of grid independence showing pressure vs crank angle for different grid sizes (2 mm grid with AMR, 1 mm grid, 2 mm grid, 4 mm grid). (b) Comparison of in-cylinder pressure between simulation and experiment.

Fig. 2. The validations of grid independence (a) and in-cylinder pressure (b).

![Figure 3: Schematic diagrams of the RGL (a) and FML (b) processes. (a) RGL: A cross-section of a combustion chamber with a leading spark plug. Leakage path I shows residual gas leaking from Chamber II to Chamber I. Leakage path II shows gas leaking from Chamber I to Chamber II. (b) FML: A cross-section of a combustion chamber with a leading spark plug. Leakage path III shows fresh mixture leaking from Chamber II to Chamber I. Leakage path IV shows gas leaking from Chamber I to Chamber II. Both diagrams show a rotation direction arrow.](edd10d3006553f0a7a5a7f844ed8cd01_img.jpg)

Figure 3: Schematic diagrams of the RGL (a) and FML (b) processes. (a) RGL: A cross-section of a combustion chamber with a leading spark plug. Leakage path I shows residual gas leaking from Chamber II to Chamber I. Leakage path II shows gas leaking from Chamber I to Chamber II. (b) FML: A cross-section of a combustion chamber with a leading spark plug. Leakage path III shows fresh mixture leaking from Chamber II to Chamber I. Leakage path IV shows gas leaking from Chamber I to Chamber II. Both diagrams show a rotation direction arrow.

Fig. 3. The process of RGL (a) and FML(b).

![Figure 4: Leakage characteristics of LSP cavity under different diameters. (a) Line graph of leakage flow rate vs crank angle for different LSP diameters (12.17 mm, 9.0 mm, 6.0 mm, 3.0 mm). (b) Bar chart of leakage mass vs LSP diameter for leakage of fresh mixture and residual gas. (c) Line graph of leakage flow rate vs crank angle for different LSP diameters. (d) Bar chart of leakage mass vs LSP diameter for leakage of fresh mixture and residual gas.](b15e3860e0c96ed16ce77f032da6f107_img.jpg)

| Diameter of leading spark plug cavity (mm) | Leakage of fresh mixture (kg) | Leakage of residual gas (kg) |
|--------------------------------------------|-------------------------------|------------------------------|
| 12.17                                      | ~3.8 × 10 <sup>-7</sup>       | ~1.0 × 10 <sup>-7</sup>      |
| 9.0                                        | ~3.2 × 10 <sup>-7</sup>       | ~0.8 × 10 <sup>-7</sup>      |
| 6.0                                        | ~1.5 × 10 <sup>-7</sup>       | ~0.3 × 10 <sup>-7</sup>      |
| 3.0                                        | ~0.3 × 10 <sup>-7</sup>       | ~0.1 × 10 <sup>-7</sup>      |

| Diameter of leading spark plug cavity (mm) | Leakage of fresh mixture (kg) | Leakage of residual gas (kg) |
|--------------------------------------------|-------------------------------|------------------------------|
| 12.17                                      | ~4.2 × 10 <sup>-6</sup>       | ~1.0 × 10 <sup>-6</sup>      |
| 9.0                                        | ~1.5 × 10 <sup>-6</sup>       | ~0.5 × 10 <sup>-6</sup>      |
| 6.0                                        | ~0.5 × 10 <sup>-6</sup>       | ~0.2 × 10 <sup>-6</sup>      |
| 3.0                                        | ~0.2 × 10 <sup>-6</sup>       | ~0.1 × 10 <sup>-6</sup>      |

Figure 4: Leakage characteristics of LSP cavity under different diameters. (a) Line graph of leakage flow rate vs crank angle for different LSP diameters (12.17 mm, 9.0 mm, 6.0 mm, 3.0 mm). (b) Bar chart of leakage mass vs LSP diameter for leakage of fresh mixture and residual gas. (c) Line graph of leakage flow rate vs crank angle for different LSP diameters. (d) Bar chart of leakage mass vs LSP diameter for leakage of fresh mixture and residual gas.

Fig. 4. The leakage characteristics of LSP cavity under different diameters

(a) Leakage flow rate in leakage mode I (b) Leakage mass in leakage mode I  
(c) Leakage flow rate in leakage mode II (d) Leakage mass in leakage mode II.

$9.33 \times 10^{-8}$  kg with the diameter of LSP cavity reduces from 12.17 to 3 mm, which is decreased by 98.04%. At the same time, the mass of RGL decreases from  $9.33 \times 10^{-7}$  to  $1.50 \times 10^{-8}$  kg, and the mass of FML decreases from  $3.81 \times 10^{-6}$  to  $7.83 \times 10^{-8}$  kg when the diameter of LSP cavity is reduced from 12.17 to 3 mm. Therefore, reducing the diameter of LSP cavity could significantly reduce leakage through the LSP cavity. In terms of the total amount of gas leakage, the results of study by Picard [22] are reliable. Lower FML reduces hydrogen leakage and contributes to engine economy. However, while reducing RGL can decrease the concentration of residual gas in the working chamber, it also adversely affects the thermal atmosphere in chamber I, potentially reducing combustion efficiency.

### 3.2. Influence of diameter of LSP cavity on combustion

The diameter of LSP cavity could significantly affect gas leakage, which in turn would have impact on the turbulent combustion process of HWRE. The influence of diameter of LSP cavity on working performance are illustrated in Fig. 5. The curves of in-cylinder pressure (P), pressure to volume (P-V), indicated thermal efficiency (ITE) and mass of in-cylinder hydrogen are listed in Fig. 5(a)–(d), respectively. As it is shown in Fig. 5(a), after reducing the diameter of LSP cavity from 12.17

to 3 mm, the peak pressure ( $P_{\max}$ ) decreases to 3.00 MPa, the corresponding crank angle is postponed from 567.12 to 572.21 °CA. These can be explained by the follow reasons: One is the reduced diameter of LSP hinders the flame propagation to the working chamber resulting in lower peak in-cylinder pressure. Another reason is that the amount of RGL decreases with smaller LSP diameter, which inhibits the acceleration of the combustion process by the thermal atmosphere. This can also be confirmed by the study of Jeng [26]. Thus, the maximum in-cylinder pressure decreases and the corresponding crank angle postpones with the reduction of LSP diameter. It can be seen from Fig. 5(b) that, with the diameter of LSP hole decreases from 12.17 to 3 mm, the indicated work improves from 375.70 to 378.17 J, and the indicated work is 380.19 J when the diameter of LSP cavity is 9 mm. Higher peak in-cylinder pressure does not mean higher indicated work. As the LSP diameter decreases, the proper slowing of the combustion rate and heat release process of the hydrogen-air mixture contributes to the increase in indicated work. At the same time, the reduction in fresh mixture leakage also increases the total heat release, which also contributes to the increase in indicated work. The influence of diameter of LSP cavity on the ITE is illustrated in Fig. 5(c). As the diameter decreases from 12.17 to 3 mm, the ITE initially increases and then decreases. The maximum ITE of 38.38% is achieved when the diameter is 9 mm. It exhibits the same

![Figure 5: Performance of HWRE under different diameters of LSP. (a) P-V diagram showing pressure (MPa) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm. (b) P-V diagram showing pressure (MPa) vs volume (m³) for Original diameter (12.17 mm), 9.0 mm, 6.0 mm, and 3.0 mm. (c) Bar chart of Indicated thermal efficiency (%) vs Diameter of leading spark plug (12.17 mm, 0.0 mm, 9.0 mm, 8.0 mm, 6.0 mm, 3.0 mm). (d) H2 mass (kg) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm, with an inset showing a zoomed-in view of the combustion process.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 5 consists of four subplots. (a) is a P-V diagram with pressure (MPa) on the y-axis (0.0 to 3.5) and crank angle (°CA) on the x-axis (360 to 720). It shows four cycles: Original diameter (red solid), Diameter 9.0 mm (blue dashed), Diameter 6.0 mm (yellow dotted), and Diameter 3.0 mm (cyan dash-dot). A vertical dashed line marks TDC at 540°CA. (b) is a P-V diagram with pressure (MPa) on the y-axis (0.0 to 3.5) and volume (m³) on the x-axis (0.0000 to 0.0008). It shows the same four cycles. (c) is a bar chart of Indicated thermal efficiency (%) on the y-axis (30 to 40) versus Diameter of leading spark plug (12.17 mm, 0.0 mm, 9.0 mm, 8.0 mm, 6.0 mm, 3.0 mm) on the x-axis. The values are 37.924, 38.151, 38.378, 38.147, 38.094, and 37.945 respectively. (d) is a plot of H<sub>2</sub> mass (kg) on the y-axis (0.0 to 1.0 × 10<sup>-5</sup>) versus crank angle (°CA) on the x-axis (0 to 1080). It shows the same four cycles. An inset zooms in on the combustion process between 200 and 600°CA.

Figure 5: Performance of HWRE under different diameters of LSP. (a) P-V diagram showing pressure (MPa) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm. (b) P-V diagram showing pressure (MPa) vs volume (m³) for Original diameter (12.17 mm), 9.0 mm, 6.0 mm, and 3.0 mm. (c) Bar chart of Indicated thermal efficiency (%) vs Diameter of leading spark plug (12.17 mm, 0.0 mm, 9.0 mm, 8.0 mm, 6.0 mm, 3.0 mm). (d) H2 mass (kg) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm, with an inset showing a zoomed-in view of the combustion process.

Fig. 5. The performance of HWRE under different diameters of LSP

(a) P (b) P-V (c) ITE (d) H<sub>2</sub> mass.

pattern of change as the indicated work. From this, it can be concluded that appropriately reducing the diameter of LSP cavity is beneficial for improving the working performance of HWRE. Fig. 5(d) depicts the influence of diameter of LSP cavity on the mass of working medium. It can be seen from this figure that the mass of in-cylinder hydrogen increases with the diameter of LSP cavity decreases, but the mass of hydrogen is the highest in the working chamber when the diameter of LSP cavity is 6 mm. This is partly because the reduced diameter of LSP decreases the amount of fresh mixture that can escape. On the other hand, a better combustion process also results in a fuller exhaust stroke and more fresh mixture enters the cylinder during the intake stroke. The combined effect results in the highest in-cylinder hydrogen mass at 6 mm diameter of LSP. In summary, it is not that the smaller the diameter of LSP cavity, the more advantageous it is. Reducing the diameter of LSP cavity appropriately is beneficial for working performance.

The effect of LSP cavity diameter on heat release is illustrated in

Fig. 6. As the diameter of the LSP cavity decrease, the whole heat release process of the in-cylinder mixtures is delayed. The peak HRR is significantly higher than that of the original LSP cavity diameter. The peak instantaneous HRR is highest when the LSP cavity diameter is 6 mm. This is because more hydrogen is involved in combustion at small LSP diameters. Fig. 6(b) displays the integrated heat release in the working chamber under different diameters of LSP cavity. It can be seen that the integrated heat release increases when the diameter of the LSP cavity is reduced compared to the original diameter (12.17 mm). The integrated heat release is similarly maximum at 6 mm diameter of the LSP cavity and reaches 990.73 J, which is an increase of 16.37 J as compared to the original diameter of the LSP cavity. More hydrogen is involved in the combustion resulting in more integrated heat release.

Fig. 7 depicts the spread process of the flame in the working chamber. Flames L and T indicate the flames spreads from the LSP cavity and TSP cavity. Meanwhile, four small diagrams showing the flame spread

![Figure 6: Heat release characteristics of HWRE under different diameters of LSP. (a) HRR (J/s) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm. (b) Integrated heat release (J) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm, with an inset showing a zoomed-in view of the combustion process.](92c6488dfdf125bc1b7bb6a235394652_img.jpg)

Figure 6 consists of two subplots. (a) is a plot of Heat release rate (J/s) on the y-axis (0 to 40) versus crank angle (°CA) on the x-axis (486 to 702). It shows four cycles: Original diameter (red solid), Diameter 9.0 mm (blue dashed), Diameter 6.0 mm (yellow dotted), and Diameter 3.0 mm (cyan dash-dot). (b) is a plot of Integrated heat release (J) on the y-axis (0 to 1080) versus crank angle (°CA) on the x-axis (0 to 1080). It shows the same four cycles. An inset zooms in on the combustion process between 600 and 800°CA.

Figure 6: Heat release characteristics of HWRE under different diameters of LSP. (a) HRR (J/s) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm. (b) Integrated heat release (J) vs crank angle (°CA) for Original diameter, 9.0 mm, 6.0 mm, and 3.0 mm, with an inset showing a zoomed-in view of the combustion process.

Fig. 6. The heat release characteristics of HWRE under different diameters of LSP

(a) HRR (b) the integrated heat release.

![Figure 7: The flame spread process in the working chamber. The diagram is divided into two main parts. The left part, titled 'Flame propagation in working chamber', shows a cross-section of a curved combustion chamber with a leading spark plug and a trailing spark plug. It illustrates four stages of flame spread: 'Only L spread' (flame L spreads from the leading plug), 'Both L and T separated' (flames L and T are separate), 'L and T merged' (flames L and T meet), and 'L and T merged front' (the merged flame front moves forward). The right part, titled 'Combustion chamber structure', shows a 3D perspective of the combustion chamber with the leading and trailing spark plugs, a recess, and a rotation direction arrow. The chamber is labeled 'Chamber I'.](a738993919a50143787084ee7ce6e2f2_img.jpg)

Figure 7: The flame spread process in the working chamber. The diagram is divided into two main parts. The left part, titled 'Flame propagation in working chamber', shows a cross-section of a curved combustion chamber with a leading spark plug and a trailing spark plug. It illustrates four stages of flame spread: 'Only L spread' (flame L spreads from the leading plug), 'Both L and T separated' (flames L and T are separate), 'L and T merged' (flames L and T meet), and 'L and T merged front' (the merged flame front moves forward). The right part, titled 'Combustion chamber structure', shows a 3D perspective of the combustion chamber with the leading and trailing spark plugs, a recess, and a rotation direction arrow. The chamber is labeled 'Chamber I'.

Fig. 7. The flame spread process in the working chamber.

process are also listed in Fig. 7, which indicates that the diffusion of flames includes four stages, flame L spread, flames L and T separated, flames L and T merged, and flames L and T merged front. Besides, according to the different positions of flame fronts, the two flame fronts of flame L are marked as LL and LT. Similarly, the two flame fronts of flame T are marked as TL and TT.

The influence of hole diameter of LSP cavity on temperature field is illustrated in Fig. 8. Analysis of the working chamber's combustibility could be achieved with the temperature field there. Fig. 8(a)–(d) show that the temperature field with original diameter of LSP cavity. The temperature field variations with the 9 mm diameter of LSP cavity are shown in Fig. 8(e)–(h). At the same time, Fig. 8(i)–(l) show the specific patterns in the temperature field when the diameter of LSP cavity is 6 mm, and the temperature field variations when the diameter of LSP cavity is 3 mm are illustrated in Fig. 8(m)–(p). Compared to the original diameter of LSP cavity, the reduction of the diameter of LSP cavity reduces the velocity of flame diffusion. This phenomenon is also a good explanation for the decrease in peak in-cylinder pressure with reducing the diameter of LSP. At 555 °CA, the flame fronts TL and LT intersect with the original diameter of the LSP cavity, while the flame fronts of TL and LT still have a certain distance at 560 °CA after the diameter of the LSP cavity decreases. The delay in flame diffusion becomes more pronounced as the diameter of LSP cavity decreases. Compared to the LSP cavity with 6 mm or 3 mm apertures, the flame diffusion at 9 mm apertures is better. However, based on the previous conclusion, the delaying of flame diffusion is not detrimental to working performance, which is beneficial for the improving of indicated work and integrated heat release.

### 3.3. Influence of diameter of LSP cavity on flow field

The diameter of the LSP cavity has an important influence on the gas leakage. As the diameter of LSP cavity decreases, the gas leakage between adjacent chambers decreases, the flow field in the working chamber is also affected in turn. Fig. 9 demonstrates the flow field changes in the working chamber under different LSP cavity diameters. At the original LSP cavity diameter of 12.7 mm, the RGL forms an airflow boundary, and then intersects with the main flow field to form an airflow collision zone, which is displayed in Fig. 9(a) and (b). During the FML stage, the vortex clusters in the middle area of the working chamber and gradually weaken due to the effect of FML, which is displayed in Fig. 9(c) and (d). The same conclusion as in this study were also obtained by Li [24]. Fig. 9(e)–(h) show the flow field change process under 9 mm diameter of LSP cavity. Although the RGL forms an airflow collision zone

in front of the mainstream area, the RGL could not significantly change the structure of main flow area. When the diameter of LSP cavity is further reduced to 6 mm and 3 mm, the quality of leakage gas is significantly reduced, resulting in the negligible impact of gas leakage on the flow field changes in the working chamber. In addition, it can be concluded from Fig. 9(i)–(p), a tumble flow is formed in front of the working chamber, and the strength of rolling flow with 3 mm diameter LSP cavity is greater than that with 6 mm diameter LSP cavity. This is due to the fact that the smaller the diameter of LSP, the greater the squeezing effect on the airflow movement, and therefore the higher the flow speed and the greater the area of influence.

The influence of diameter of LSP cavity on vorticity is illustrated in Fig. 10. As the diameter of the LSP hole decreases from 12.17 mm to 6 mm, the vorticity in working chamber decreases during the gas leakage stage. This is because the reduction in gas leakage makes the vorticity lower. However, after the diameter of LSP cavity is reduced from 6 mm to 3 mm, the vorticity in working chamber has increased. This is because the improvement in gas leakage speed makes the vorticity higher.

### 3.4. Influence of diameter of LSP cavity at optimum location

The influence of various diameters of LSP on its working performance is discussed in the previous sections. According to previous research, the optimum LSP location on combustion efficiency and performance is moved 6.5 mm to minor axis. In this paper, the effect of different diameters of LSP cavity on working performance at optimum location of LSP would be given. The leakage characteristics under different diameters of LSP cavity at optimum location are displayed in Fig. 11. Meanwhile, Fig. 11(a) and (b) display the leakage flow rate and mass in leakage mode I, respectively. As the diameter of LSP hole decreases from 12.17 to 3 mm, the leakage mass between adjacent chambers decreases from  $5.20 \times 10^{-7}$  to  $7.50 \times 10^{-8}$  kg, and this value is reduced by 85.58 %. In addition, Fig. 11(c) and (d) show the leakage flow rate and mass in leakage mode II. As the diameter of LSP cavity is reduced to 3 mm, the leakage gas mass between LSP cavity and working chamber decreases from  $5.59 \times 10^{-6}$  kg to  $1.66 \times 10^{-7}$  kg, and this value is decreased by 97.02 %. In summary, at the optimum LSP location, as the diameter of LSP cavity decreases, the mass of FML is almost 0 kg, and the mass of RGL significantly decreases. According to the results of the above study, a decrease in FML is helpful in increasing the indicated work. However, higher levels of residual gas are likely to lead to deterioration of the combustion process, which is not conducive to improved HWRE performance.

The diameter of LSP cavity would have an impact on the RGL. Based

![Figure 8: A 4x4 grid of 16 heatmaps showing the temperature field of a spark plug at 555°C, 560°C, 565°C, and 570°C CA for four different Leading Spark Plug (LSP) diameters: Original, 9.0 mm, 6.0 mm, and 3.0 mm. The color scale on the right indicates temperature from 400 to 2300 K. The heatmaps show the temperature distribution across the spark plug components, with the LSP being the hottest part. As the LSP diameter increases, the temperature in the LSP region decreases significantly, while the temperature in the combustion chamber increases.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 8 displays the temperature field of a spark plug at four crank angles (CA) (555°CA, 560°CA, 565°CA, and 570°CA) for four different Leading Spark Plug (LSP) diameters: Original diameter, 9.0 mm diameter, 6.0 mm diameter, and 3.0 mm diameter. The color bar on the right indicates the temperature range from 400 K to 2300 K.

The heatmaps show the temperature distribution across the spark plug components, including the Trailing spark plug, Leading spark plug, and combustion chamber. The temperature in the Leading spark plug is highest, reaching up to 2300 K at 555°CA for the Original diameter. As the LSP diameter increases, the temperature in the LSP region decreases, while the temperature in the combustion chamber increases.

The heatmaps are labeled as follows:

- (a) 555°CA, Original diameter
- (b) 560°CA, Original diameter
- (c) 565°CA, Original diameter
- (d) 570°CA, Original diameter
- (e) 555°CA, 9.0 mm diameter
- (f) 560°CA, 9.0 mm diameter
- (g) 565°CA, 9.0 mm diameter
- (h) 570°CA, 9.0 mm diameter
- (i) 555°CA, 6.0 mm diameter
- (j) 560°CA, 6.0 mm diameter
- (k) 565°CA, 6.0 mm diameter
- (l) 570°CA, 6.0 mm diameter
- (m) 555°CA, 3.0 mm diameter
- (n) 560°CA, 3.0 mm diameter
- (o) 565°CA, 3.0 mm diameter
- (p) 570°CA, 3.0 mm diameter

Figure 8: A 4x4 grid of 16 heatmaps showing the temperature field of a spark plug at 555°C, 560°C, 565°C, and 570°C CA for four different Leading Spark Plug (LSP) diameters: Original, 9.0 mm, 6.0 mm, and 3.0 mm. The color scale on the right indicates temperature from 400 to 2300 K. The heatmaps show the temperature distribution across the spark plug components, with the LSP being the hottest part. As the LSP diameter increases, the temperature in the LSP region decreases significantly, while the temperature in the combustion chamber increases.

Fig. 8. The temperature field under different diameters of LSP.

![Figure 9: Flow field under different diameters of LSP. The figure consists of 16 subplots arranged in a 4x4 grid, labeled (a) through (p). Each subplot shows a cross-section of the combustion chamber with flow field lines. The subplots are organized by LSP diameter: 12.17mm (a, b, c, d), 9.0mm (e, f, g, h), 6.0mm (i, j, k, l), and 3.0mm (m, n, o, p). Each subplot includes labels for 'Leading spark plug', 'Chamber I', 'Airflow boundary', 'Vortex I', 'Vortex II', 'Airflow collision zone', and 'Tumble'. The crank angle (CA) is indicated in the top left of each plot: 408 °CA, 418 °CA, 425 °CA, and 432 °CA.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 9: Flow field under different diameters of LSP. The figure consists of 16 subplots arranged in a 4x4 grid, labeled (a) through (p). Each subplot shows a cross-section of the combustion chamber with flow field lines. The subplots are organized by LSP diameter: 12.17mm (a, b, c, d), 9.0mm (e, f, g, h), 6.0mm (i, j, k, l), and 3.0mm (m, n, o, p). Each subplot includes labels for 'Leading spark plug', 'Chamber I', 'Airflow boundary', 'Vortex I', 'Vortex II', 'Airflow collision zone', and 'Tumble'. The crank angle (CA) is indicated in the top left of each plot: 408 °CA, 418 °CA, 425 °CA, and 432 °CA.

Fig. 9. Flow field under different diameters of LSP.

![Figure 10: Vorticity curve under different diameters of LSP. The main plot shows Vorticity (1/s) on the y-axis (0 to 25000) versus Crank angle (°CA) on the x-axis (0 to 1080). Four curves are shown: Original diameter (solid red line), Diameter 9.0 mm (dashed blue line), Diameter 6.0 mm (dashed yellow line), and Diameter 3.0 mm (dashed green line). All curves show a sharp peak in vorticity around 120 °CA. An inset plot zooms in on the region between 380 and 440 °CA, showing the vorticity values for the four diameters in more detail.](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 10: Vorticity curve under different diameters of LSP. The main plot shows Vorticity (1/s) on the y-axis (0 to 25000) versus Crank angle (°CA) on the x-axis (0 to 1080). Four curves are shown: Original diameter (solid red line), Diameter 9.0 mm (dashed blue line), Diameter 6.0 mm (dashed yellow line), and Diameter 3.0 mm (dashed green line). All curves show a sharp peak in vorticity around 120 °CA. An inset plot zooms in on the region between 380 and 440 °CA, showing the vorticity values for the four diameters in more detail.

Fig. 10. Vorticity curve under different diameters of LSP.

on the earlier analysis [38], the appropriate RGL is beneficial for improving the working performance of WRE. As it is shown in Fig. 12(a), after reducing the diameter of LSP cavity from 12.17 to 3 mm at optimum position, the  $P_{\max}$  decreases to 3.02 MPa, the corresponding crank angle is postponed from 567.12 to 572.21 °CA. This can be explained by the reason that the reduced diameter of LSP hole hinders the flame propagation to the working chamber resulting in lower peak in-cylinder pressure. Fig. 12(b) lists the indicator diagram (P-V) under different diameters of LSP cavity at optimum position, which illustrates that the effect of reducing LSP diameter on indicated work is negligible. The indicated work is 378.80 J when the diameter of LSP cavity is 12.17 mm, and this value is 378.23 J when the diameter of LSP cavity is 3 mm. This is because there is only RGL without FML at the optimum location of LSP, and the reduction of diameter of LSP cavity could not affect the quality of working medium ( $H_2$ ), so the influence of the diameter of LSP cavity on indicated work could be ignored. In Fig. 12(c), the combustion process of working medium ( $H_2$ ) is delayed by the reduction of diameter of LSP cavity, which has a certain beneficial effect on combustibility and leads to an increase in the integrated heat release. Compared to the original diameter of LSP cavity, the integrated heat release reaches 988.02 J with an increase of 10.13 J when the diameter of LSP cavity is reduced to 6 mm. Fig. 12(d) shows the ITE of HWRE under different diameters of LSP cavity at optimum position, which indicated that the ITE decreases with reduction of the LSP diameter. The ITE of working

![Figure 11: Leakage characteristics of LSP cavity under different diameters at optimum position. (a) Leakage flow rate between adjacent chambers vs Crank angle (°CA) for Leakage mode I. (b) Leakage gas mass between adjacent chambers (kg) vs Diameter of leading spark plug cavity. (c) Leakage flow rate between leading spark plug cavity and working chamber vs Crank angle (°CA) for Leakage mode II. (d) Leakage gas mass between leading spark plug cavity and working chamber (kg) vs Diameter of leading spark plug cavity.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 11 consists of four subplots (a, b, c, d) showing leakage characteristics for different LSP cavity diameters (12.17 mm, 9.0 mm, 6.0 mm, 3.0 mm) compared to the original diameter.

(a) Line plot of Leakage flow rate between adjacent chambers (kg/s) vs Crank angle (°CA). The y-axis ranges from -0.0015 to 0.0005. The x-axis ranges from 240 to 480 °CA. A vertical line at 320 °CA indicates the moving distance of -6.5 mm. The plot shows fluctuations for different diameters, with a red arrow pointing to a negative peak at 320 °CA labeled "Leakage from leading chamber to trailing chamber".

(b) Bar chart of Leakage gas mass between adjacent chambers (kg) vs Diameter of leading spark plug cavity. The y-axis ranges from 0 to  $6 \times 10^{-7}$  kg. The x-axis shows diameters of 12.17 mm, 9.0 mm, 6.0 mm, and 3.0 mm. The chart compares "Leakage of fresh mixture" (blue bars) and "Leakage of residual gas" (red bars).

(c) Line plot of Leakage flow rate between leading spark plug cavity and working chamber (kg/s) vs Crank angle (°CA). The y-axis ranges from -0.008 to 0.002 kg/s. The x-axis ranges from 360 to 480 °CA. A vertical line at 380 °CA indicates the moving distance of -6.5 mm. The plot shows a significant negative peak at 380 °CA for the original diameter, labeled "Leakage from leading spark plug cavity to trailing chamber".

(d) Bar chart of Leakage gas mass between leading spark plug cavity and working chamber (kg) vs Diameter of leading spark plug cavity. The y-axis ranges from 0.0 to  $6.0 \times 10^{-6}$  kg. The x-axis shows diameters of 12.17 mm, 9.0 mm, 6.0 mm, and 3.0 mm. The chart compares "Leakage of fresh mixture" (blue bars) and "Leakage of residual gas" (red bars).

Figure 11: Leakage characteristics of LSP cavity under different diameters at optimum position. (a) Leakage flow rate between adjacent chambers vs Crank angle (°CA) for Leakage mode I. (b) Leakage gas mass between adjacent chambers (kg) vs Diameter of leading spark plug cavity. (c) Leakage flow rate between leading spark plug cavity and working chamber vs Crank angle (°CA) for Leakage mode II. (d) Leakage gas mass between leading spark plug cavity and working chamber (kg) vs Diameter of leading spark plug cavity.

Fig. 11. The leakage characteristics of LSP cavity under different diameters at optimum position

(a) Leakage flow rate in leakage mode I (b) Leakage mass in leakage mode I  
(c) Leakage flow rate in leakage mode II (d) Leakage mass in leakage mode II.

![Figure 12: The performance of HWRE under different diameters of LSP at optimum position. (a) P-V diagram. (b) P-V diagram with zoomed-in view of the combustion process. (c) Heat release diagram. (d) Indicated thermal efficiency bar chart.](8ee3b76dd49f31624d287885bc2c81ee_img.jpg)

Figure 12 consists of four subplots (a, b, c, d) showing engine performance for different LSP cavity diameters (12.17 mm, 10.0 mm, 9.0 mm, 8.0 mm) compared to the original diameter.

(a) P-V diagram showing Pressure (MPa) vs Crank angle (°CA). The y-axis ranges from 0.0 to 3.5 MPa. The x-axis ranges from 320 to 720 °CA. TDC is marked at 560 °CA. The plot shows the expansion process for different diameters.

(b) P-V diagram with a zoomed-in view of the combustion process. The y-axis ranges from 0.0 to 3.5 MPa. The x-axis ranges from 0.0000 to 0.0008 m<sup>3</sup>. The zoomed-in view shows the pressure peak and the expansion process in detail.

(c) Heat release diagram showing Integrated heat release (J) vs Crank angle (°CA). The y-axis ranges from 0 to 1080 J. The x-axis ranges from 0 to 1080 °CA. The plot shows the heat release curve for different diameters, with a zoomed-in view of the initial combustion phase.

(d) Bar chart of Indicated thermal efficiency (%) vs Diameter of leading spark plug. The y-axis ranges from 30 to 40%. The x-axis shows diameters of 12.17 mm, 10.0 mm, 9.0 mm, and 8.0 mm. The values for each diameter are: 12.17 mm (38.292%), 10.0 mm (38.0873%), 9.0 mm (38.0095%), and 8.0 mm (37.952%).

Figure 12: The performance of HWRE under different diameters of LSP at optimum position. (a) P-V diagram. (b) P-V diagram with zoomed-in view of the combustion process. (c) Heat release diagram. (d) Indicated thermal efficiency bar chart.

Fig. 12. The performance of HWRE under different diameters of LSP at optimum position

(a) P (b) P-V (c) Heat release (d) ITE.


chamber is decreased from 38.29 % to 37.95 % when the diameter of LSP cavity is reduced from 12.17 to 3 mm. The above conclusion indicates that reducing the diameter of LSP cavity at optimum location of LSP would reduce the thermal efficiency.

# 4. Conclusions

The current study investigates the influence of the diameter of leading spark plug (LSP) cavity on gas leakage, combustion, and working efficiency in a hydrogen-fueled Wankel rotary engine (HWRE). The effects of LSP cavity diameter on gas leakage and working performance at optimum location were systematically analyzed. The results are summarized as follows:

## 1) Impact of LSP diameter on gas leakage

The diameter of the LSP cavity has a great influence on gas leakage in the HWRE. As the LSP diameter decreases, the residual gas leakage (RGL) and fresh mixture leakage (FLM) decrease simultaneously. With the diameter of LSP cavity is reduced from 12.17 to 3 mm, the leakage between adjacent chambers is reduced by 92.96 %, between LSP cavity and working chamber is decreased by 98.04 %.

## 2) Influence on combustion process, indicated work and indicated thermal efficiency

As the decrease of LSP diameter hinders the flame propagation process, the peak in-cylinder pressure ( $P_{max}$ ) reduces. After the diameter of LSP cavity is reduced from 12.17 to 3 mm, the  $P_{max}$  decreases from 3.35 to 3.00 MPa. However, properly slow combustion and heat release processes, the thermal atmosphere provided by a proper RGL, and the increased total energy from the FLM reduction all contribute to the increase in indicated work and indicated thermal efficiency (ITE). Thus, the indicated work and ITE first increase and then decrease with the diameter of LSP cavity decrease from 12.17 to 3 mm. The indicated work and ITE reached 380.19 J and 38.38% respectively when the diameter of LSP cavity is 9 mm.

## 3) Influence of LSP diameter at optimum location

The mass of FLM was very low at the optimum location. As the diameter of LSP decreases, the mass of FLM is almost 0 kg, and the mass of RGL significantly decreases. With the diameter of LSP cavity decreases from 12.17 to 3 mm, under the influence of small LSP diameter restricting the combustion process and high residual gas concentration, the  $P_{max}$  decreases from 3.51 to 3.02 MPa, the indicated work reduces from 378.80 to 378.23 J and the ITE of working chamber is dropped from 38.29% to 37.95%.

In conclusion, a shift in the LSP position can only reduce either the RGL or the FLM, whereas a reduction in the LSP diameter can reduce both the RGL and the FLM. Considering the influence rule of RGL and FLM on the performance of HWRE, the simultaneous optimization of the LSP cavity diameter and position is crucial for enhancing HWRE performance. The design must ensure an adequate flame propagation rate and optimal residual gas content while minimizing fresh mixture leakage. Balancing these factors is key to improving combustion efficiency, power output, and economic performance of HWRE.

# CRediT authorship contribution statement

**Jinxin Yang:** Writing – original draft, Software, Project administration, Data curation. **Yijin Zhang:** Writing – review & editing, Software. **Xiaoyu Cong:** Software, Formal analysis. **Yu Sun:** Validation, Software. **Hanlin Li:** Writing – review & editing, Visualization. **Zhenyu Yang:** Writing – review & editing, Validation, Software. **Changwei Ji:** Project administration, Conceptualization.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgment

This work was financially supported by the S&T Program of Hebei (246Z4001G), the Open Foundation of National Key Laboratory of Multi-perch Vehicle Driving Systems (QDXT-WY-202407-12), the National Natural Science Foundation of China (Grant No. 52276097), the R&D Program of Beijing Municipal Education Commission (Grant No. KM202410005016), and the "JBGS" Project of Inner Mongolia Autonomous Region, China (Grant No. 2022JBGS0008).

# References

- [1] Li W, Fan B, Jiang P, Liu W, Pan J, Huo S, et al. Exploring the coupling mechanism between piston structure and turbulent jet ignition mode in hydrogen mixed natural gas rotary engines. *Int J Hydrogen Energy* 2024;63:905–17. <https://doi.org/10.1016/j.ijhydene.2024.03.149>.
- [2] Feng Z, Pan J, Li P, Fan B, Nauman M, Yang W. Numerical study of the mixture formation and combustion process of an ammonia/hydrogen rotary engine. *Int J Hydrogen Energy* 2024;69:1469–80. <https://doi.org/10.1016/j.ijhydene.2024.04.339>.
- [3] Chen W, Yu S, Zuo Q, Zhu G, Zhang B, Yang X. Combined effect of air intake method and hydrogen injection timing on airflow movement and mixture formation in a hydrogen direct injection rotary engine. *Int J Hydrogen Energy* 2022;47:12739–58. <https://doi.org/10.1016/j.ijhydene.2022.02.045>.
- [4] Sun Z-Y. Experimental studies on the explosion indices in turbulent stoichiometric H<sub>2</sub>/CH<sub>4</sub>/air mixtures. *Int J Hydrogen Energy* 2019;44:469–76. <https://doi.org/10.1016/j.ijhydene.2018.02.094>.
- [5] Yang J, Ji C, Wang S, Meng H. An experimental study on ignition timing of hydrogen Wankel rotary engine. *Int J Hydrogen Energy* 2022;47:17468–78. <https://doi.org/10.1016/j.ijhydene.2022.03.223>.
- [6] Fan B, Qi X, Pan J, Wu X, Fang J, Lu Q, et al. Research on the hydrogen injection strategy of a turbulent jet ignition (TJI) rotary engine fueled with natural gas/hydrogen blends. *Int J Hydrogen Energy* 2023;48:20041–58. <https://doi.org/10.1016/j.ijhydene.2023.02.037>.
- [7] Gao J, Wang X, Song P, Tian G, Ma C. Review of the backfire occurrences and control strategies for port hydrogen injection internal combustion engines. *Fuel* 2022;307:121553. <https://doi.org/10.1016/j.fuel.2021.121553>.
- [8] Kucuk M, Sener R, Surmen A. Effectiveness of hydrogen enrichment strategy for Wankel engines in unmanned aerial vehicle applications at various altitudes. *Int J Hydrogen Energy* 2024;52:1534–49. <https://doi.org/10.1016/j.ijhydene.2023.08.304>.
- [9] Fan B, Wang J, Pan J, Zeng Y, Fang J, Lu Q, et al. Computational study of hydrogen injection strategy on the combustion performance of a direct injection rotary engine fueled with natural gas/hydrogen blends. *Fuel* 2022;328:125190. <https://doi.org/10.1016/j.fuel.2022.125190>.
- [10] Wang S, Sun Y, Yang J, Wang H. Effect of excess air ratio and ignition timing on the combustion and emission characteristics of the ammonia-hydrogen Wankel rotary engine. *Energy* 2024;131779. <https://doi.org/10.1016/j.energy.2024.131779>.
- [11] Jiao H, Zou R, Wang N, Luo B, Pan W, Liu J. Optimization design of the ignition system for Wankel rotary engine considering ignition environment, flow, and combustion. *Appl Therm Eng* 2022;201:117713. <https://doi.org/10.1016/j.applthermaleng.2021.117713>.
- [12] Amrouche F, Erickson PA, Varnhagen S, Park JW. An experimental analysis of hydrogen enrichment on combustion characteristics of a gasoline Wankel engine at full load and lean burn regime. *Int J Hydrogen Energy* 2018;43:19250–9. <https://doi.org/10.1016/j.ijhydene.2018.08.110>.
- [13] Ozcanli M, Bas O, Akar MA, Yildizhan S, Serin H. Recent studies on hydrogen usage in Wankel SI engine. *Int J Hydrogen Energy* 2018;43:18037–45. <https://doi.org/10.1016/j.ijhydene.2018.01.202>.
- [14] Otchere P, Pan J, Fan B, Chen W, Lu Y. Recent studies of fuels used in wankel rotary engines. *J Energy Resour Technol Trans ASME* 2021;143. <https://doi.org/10.11115/1.4047971>.
- [15] Meng H, Ji C, Xin G, Yang J, Chang K, Wang S. Comparison of combustion, emission and abnormal combustion of hydrogen-fueled Wankel rotary engine and reciprocating piston engine. *Fuel* 2022;318:123675. <https://doi.org/10.1016/j.fuel.2022.123675>.
- [16] Burley HA, Meloey MR, Stark TL. Sources of hydrocarbon emissions in rotary engines. *SAE Tech Pap* 1978;87:1996–2011. <https://doi.org/10.4271/780419>.
- [17] Eberle MK, Klomp ED. An evaluation of the potential performance gain from leakage reduction in rotary engines. *SAE Tech Pap* 1973;82:454–60. <https://doi.org/10.4271/730117>.
- [18] Zhang S, Liu J, Zuo Z, Zhang Y. An analytical investigation of oil film thickness for the apex seal in a small Wankel rotary engine. *Tribol Int* 2017;116:383–93. <https://doi.org/10.1016/j.triboint.2017.07.031>.

- [19] McCuiston FD. An analytical evaluation of the effect of leakage on no emissions from a rotary engine. SAE Tech Pap 1975;84:135–40. <https://doi.org/10.4271/750023>.
- [20] Nagao A, Ohzeki H, Niura Y. Present status and future view of rotary engines. *Automot. Engine altern.* Springer; 1987. p. 183–201.
- [21] Prasae HF, McCormick HE, Anderson RD. A critical analysis of the rotary engine sealing problem. SAE Technical Paper; 1973. p. 730118. <https://doi.org/10.4271/730118>.
- [22] Picard M, Tian T, Nishino T. Predicting gas leakage in the rotary engine-Part I: apex and corner seal. *J Eng Gas Turbines Power* 2016;138:1–8. <https://doi.org/10.1115/1.4031873>.
- [23] Picard M, Tian T, Nishino T. Predicting gas leakage in the rotary engine-Part II: side seals and summary. *J Eng Gas Turbines Power* 2016;138. <https://doi.org/10.1115/1.4031874>.
- [24] Li Z, Shih TIP, Schock HJ, Willis EA. A numerical study on the effects of apex seal leakage on wankel engine flow fields. SAE Tech Pap 1991. <https://doi.org/10.4271/910703>.
- [25] Fan B, Zeng Y, Pan J, Fang J, Salami HA, Wang Y. Numerical study of injection strategy on the combustion process in a peripheral ported rotary engine fueled with natural gas/hydrogen blends under the action of apex seal leakage. *Energy* 2022; 242:122532. <https://doi.org/10.1016/j.energy.2021.122532>.
- [26] Jeng DZ, Hsieh MJ, Lee CC, Han Y. The numerical investigation on the performance of rotary engine with leakage, different fuels and recess sizes. SAE Tech Pap 2013;2013. <https://doi.org/10.4271/2013-32-9160>.
- [27] Fan B, Zeng Y, Pan J, Fang J, Hammed AS, Wang Y. Evaluation and analysis of injection strategy in a peripheral ported rotary engine fueled with natural gas/hydrogen blends under the action of apex seal leakage. *Fuel* 2022;310:122315. <https://doi.org/10.1016/j.fuel.2021.122315>.
- [28] Fan B, Zhang Y, Pan J, Wang Y, Otchere P. Experimental and numerical study on the formation mechanism of flow field in a side-ported rotary engine considering apex seal leakage. *J Energy Resour Technol Trans ASME* 2021;143:1–15. <https://doi.org/10.1115/1.4047787>.
- [29] Hsieh CF, Chen KT, Johar T. Fluid flow characteristics of two types rotary engines. *Int J Hydrogen Energy* 2021;46:40154–74. <https://doi.org/10.1016/j.ijhydene.2021.09.250>.
- [30] Zeng Y, Fan B, Pan J, He R. Research on the ignition strategy of a methanol/gasoline blends rotary engine using turbulent jet ignition mode. *Energy* 2022; 124921. <https://doi.org/10.1016/j.energy.2022.124921>.
- [31] Yamamoto K, Muroki T, Kobayakawa T. Combustion characteristics of rotary engines. *SAE Trans* 1972;1296–302.
- [32] Cihan Ö, Kutlar OA. Effect of leading and trailing spark plugs on combustion, fuel consumption and exhaust emission in a wankel engine. *Arabian J Sci Eng* 2021;46: 7471–82. <https://doi.org/10.1007/s13369-021-05456-3>.
- [33] Watanabe S, Hamai Y. Investigation of cyclic combustion variation in rotary engine. SAE Tech Pap 1989;98:490–501. <https://doi.org/10.4271/890327>.
- [34] Harikrishnan TV, Challa S, Radhakrishna D. Numerical investigation on the effects of flame propagation in rotary engine performance with leakage and different recess shapes using three-dimensional computational fluid dynamics. *J Energy Resour Technol Trans ASME* 2016;138:1–17. <https://doi.org/10.1115/1.4033572>.
- [35] Hwang PW, Chen XC, Cheng HC. Influences of ignition timing, spark plug and intake port locations on the combustion performance of a simulated rotary engine. *J Mech* 2016;32:579–91. <https://doi.org/10.1017/jmech.2016.39>.
- [36] Jiao H, Ye X, Zou R, Wang N, Liu J. Comparative study on ignition and combustion between conventional spark-ignition method and near-wall surface ignition method for small-scale Wankel rotary engine. *Energy* 2022;255:124500. <https://doi.org/10.1016/j.energy.2022.124500>.
- [37] Morimoto K, Teramoto T, Takamori Y. Combustion characteristics in hydrogen fueled rotary engine. SAE Tech Pap 1992;101:459–65. <https://doi.org/10.4271/920302>.
- [38] Yang Z, Ji C, Yang J, Wang H, Huang X, Wang S. The optimization of leading spark plug location and its influences on combustion and leakage in a hydrogen-fueled Wankel rotary engine. *Int J Hydrogen Energy* 2023;48(53):20465–82. <https://doi.org/10.1016/j.ijhydene.2023.02.099>.
- [39] Richards KJ, Senecal PK, Pomraning E. CONVERGE studio 4 manual[R]. Madison, WI: Convergent Science; 2024.
- [40] Li H, Yazdi M. Stochastic game theory approach to solve system safety and reliability decision-making problem under uncertainty. In: advanced decision-making methods and applications in system safety and reliability problems. *Stud. Syst. Decis. Control* 2022;211:127–51. [https://doi.org/10.1007/978-3-031-07430-1\\_8](https://doi.org/10.1007/978-3-031-07430-1_8). Springer Cham.
- [41] Yazdi M, Zarei E, Adumene S, et al. Chapter Eleven - uncertainty modeling in risk assessment of digitalized process systems. *Method Chem Process Safety* 2022;6: 389–416. <https://doi.org/10.1016/bs.mcps.2022.04.005>. Elsevier.
- [42] Fan B, Pan J, Tang A, et al. Experimental and numerical investigation of the fluid flow in a side-ported rotary engine. *Energy Convers Manag* 2015;95:385–97. <https://doi.org/10.1016/j.enconman.2015.02.047>.
- [43] Stagni A, Cavallotti C, Arunthanayothin S, Song Y, Herbinet O, Battin-Leclerc F, et al. An experimental, theoretical and kinetic-modeling study of the gas-phase oxidation of ammonia. *React Chem Eng* 2020;5:696–711. <https://doi.org/10.1039/c9re00429g>.
- [44] Wang Z, Ji C, Wang D, Hou R, Zhang T, Wang S. Experimental and numerical study on premixed partially dissociated ammonia mixtures. Part II: numerical study of premixed combustion characteristics. *Fuel* 2021;306:121660. <https://doi.org/10.1016/j.fuel.2021.121660>.
- [45] Yazdi M, Khan F, Abbassi R. Operational subsea pipeline assessment affected by multiple defects of microbiologically influenced corrosion. *Process Saf Environ Prot* 2021;158:159–71. <https://doi.org/10.1016/j.pspe.2021.11.032>.
- [46] Yazdi M, Golilarz N, Adesina K, et al. Probabilistic risk analysis of process systems considering epistemic and aleatory uncertainties: a comparison study. *Int J Uncertain Fuzziness Knowledge-Based Syst* 2021;29:181–207. <https://doi.org/10.1142/S0218488521500098>.