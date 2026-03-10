

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the journal Energy](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the journal Energy

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Numerical investigation on the effect of ignition timing on a low-temperature hydrogen-fueled Wankel rotary engine with passive pre-chamber ignition

Changwei Ji<sup>\*</sup>, Hanlin Li, Jinxin Yang<sup>\*\*</sup>, Hao Meng

College of Mechanical and Energy Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

## A R T I C L E I N F O

**Keywords:**  
Wankel rotary engine  
Low-temperature hydrogen  
Turbulent jet ignition  
Passive pre-chamber  
Combustion

## A B S T R A C T

Adopting the low-temperature hydrogen evaporated from the liquid hydrogen is capable of improving volumetric efficiency for the Wankel rotary engine (WRE). Considering the difficulty in ignition and slow flame propagation of low-temperature hydrogen-air mixtures, the passive pre-chamber is used to improve ignition and combustion. A three-dimensional computational fluid dynamics model for a turbulent jet ignition (TJI) WRE fueled by low-temperature hydrogen was established. The effects of low temperature and TJI on the in-cylinder flow field, combustion, emissions and leakage in the TJI-WRE fueled by low-temperature hydrogen were studied under different ignition timings. The results indicated that low-temperature tends to suppress the flame propagation, whereas TJI can accelerate the flame speed and promote flame propagation to the unburned zone in the combustion chamber. Combining low-temperature hydrogen with the passive pre-chamber can achieve high engine thermal efficiency and power while significantly reducing leakage. With the ignition timing set at 18 °CA before the top dead center, the indicated thermal efficiency reached 39.49 % and the indicated mean effective pressure peaked at 0.77 MPa. Compared to the original engine, fresh mixture leakage through spark plug cavities and adjacent chambers was reduced by 72.13 % and 78.79 %, respectively.

## Nomenclature

|                 |                                      |
|-----------------|--------------------------------------|
| ABDC            | After bottom dead center             |
| AMR             | Adaptive Mesh Refinement             |
| ATDC            | After top dead center                |
| BBDC            | Before bottom dead center            |
| BTDC            | Before top dead center               |
| CFD             | Computational fluid dynamics         |
| HFCs            | Hydrogen fuel cells                  |
| HICEs           | hydrogen internal combustion engines |
| HIT             | Hydrogen ignition timing             |
| HWRE            | Hydrogen Wankel rotary engine        |
| IMEP            | Indicated mean effective pressure    |
| ITE             | Indicated thermal efficiency         |
| LSP             | Leading Spark Plug                   |
| MAP             | Manifold absolute pressure           |
| MCC             | Main combustion chamber              |
| NO <sub>x</sub> | Nitrogen oxide                       |
| PIV             | Particle Image Velocimetry           |
| PPC             | Passive pre-chamber                  |

(continued)

|           |                                                      |
|-----------|------------------------------------------------------|
| SI        | Spark ignition                                       |
| TDC       | Top dead center                                      |
| TJI       | Turbulent jet ignition                               |
| TJI-HWRE  | Turbulent jet ignition hydrogen Wankel rotary engine |
| TSP       | Trailing Spark Plug                                  |
| WRE       | Wankel rotary engine                                 |
| $\lambda$ | Excess air coefficient                               |
| °CA       | Crank angle                                          |

## 1. Introduction

Countries worldwide have been enacting increasingly stringent environmental protection and emissions regulations in recent years [1]. The use of eco-friendly alternative fuels, particularly zero-carbon energy, to reduce carbon emissions in the transportation industry has been

(continued on next column)

\* Corresponding author.

\*\* Corresponding author.

E-mail addresses: [chwji@bjut.edu.cn](mailto:chwji@bjut.edu.cn) (C. Ji), [yangjinxin@bjut.edu.cn](mailto:yangjinxin@bjut.edu.cn) (J. Yang).

gaining increasing attention globally [2]. Hydrogen as a renewable energy with zero carbon emissions is widely recognized as the ultimate fuel in the future [3]. Hydrogen is characterized by high adiabatic flame temperature [4], high specific mass-energy density [5], high combustion velocity [6], short quenching distance [7], and wide flammability limit [8]. Hydrogen internal combustion engines (HICEs) can achieve better combustion and emission performance. Jeroend's research [9] found that the peak brake thermal efficiency (BTE) of HICEs can reach 45 %, while gasoline engines achieve a peak BTE of 40 % [10]. Hong's research [11] found that optimizing valve timing on HICEs can keep  $\text{NO}_x$  emissions below 20 ppm while significantly increasing BTE. Therefore, hydrogen is expected to achieve commercial application in the internal combustion engine industry.

The Wankel rotary engine (WRE) is a type of internal combustion engine which is structurally distinct from the reciprocating piston engine [12]. Since the WRE removes the gas distribution mechanism [13], its structure is simpler than that of the reciprocating piston engines [14]. The WRE has four independent strokes, but it operates as a two-stroke engine, which results in a high-power density [15]. The WRE uses the rotary motion of the rotor instead of the reciprocating motion of pistons, resulting in less friction and vibration at high speeds compared to traditional reciprocating piston engines [16]. Therefore, the high engine speed and high power-to-weight ratio make the WRE more suitable for hydrogen, considering its high combustion velocity and high diffusion speed. Meng's experimental results [17] showed that the power per displacement of the hydrogen WRE (HWRE) is 1.66 times that of the HICEs and 1.23 times that of the gasoline reciprocating piston engine. Morimoto et al. [18] demonstrated that HWRE is less susceptible to backfire and has greater power than HICEs under the same specifications. Therefore, the WRE is widely used in military drones [19], range extenders for electric vehicles [20], and other fields.

Due to the high cost of in-cylinder direct injection nozzles for current commercial HICEs, most hydrogen engines are fueled with hydrogen port injection. However, this type of hydrogen supply results in reduced volumetric efficiency and abnormal combustion such as backfire and knock [21]. To address the higher propensity for abnormal combustion in hydrogen engines, lean combustion is an effective approach. But lean combustion reduces the engine's power density. Water injection was also demonstrated to suppress knock and lower  $\text{NO}_x$  emissions [22], but it could dilute the lubricant oil.

In addition to the above methods, the method of reducing the intake temperature can also be adopted. Ji et al. [23] investigated the knock of HWRE and found that reducing the inlet temperature eliminated the knock of HWRE. Fridriksson et al. [24] found that lowering the charge temperature can reduce  $\text{NO}_x$  emissions without affecting engine performance. Trombley et al. [25] demonstrated that low emissions and high combustion efficiency can be achieved by lowering the temperature of the fuel and premixed combustion. Since liquid hydrogen has a very low boiling point, it is extremely susceptible to vaporization. Mixing the evaporated low-temperature hydrogen and air in the intake port before entering the cylinder can increase the volumetric efficiency of the engine and reduce the potential for abnormal combustion. However, there are few studies on the application of low temperature hydrogen on WRE at this stage. Since the conventional spark ignition (SI) ignition mode is unstable and prone to encounter long heat release duration under low temperature combustion, a new ignition mode is required to stimulate the ignition and combustion processes.

Compared to SI, turbulent jet ignition (TJI) has several advantages: it can achieve multi-point ignition [26], accelerate the flame speed [27], provide higher ignition energy [28], expand the lean-burn limit of the engine [29], and improve the combustion stability and combustion efficiency [30]. Liu et al. [31] found that compared with SI, TJI reduces the cyclic variations and improves the indicated mean effective pressure (IMEP) in an ammonia-hydrogen engine. Fan et al. [32] found that the use of TJI in WRE promotes flame propagation to the rear of the cylinder, reducing the area of the combustion dead zone and improving the

thermal efficiency.

Applying TJI to HWRE also reduces the leakage of HWRE. The leakage is a critical issue that the HWRE faces. The leakage can adversely affect the gas pressure balance and oil film distribution inside the HWRE [33], significantly impacting lubrication, performance [34], and nitrogen oxide emissions [35]. Meng et al. [13] summarized the leakage mechanisms of WRE, including side leakage, apex leakage, corner leakage and spark plug cavities leakage. Yang et al. [33] concluded that the most significant leakage mechanism in apex leakage is caused by leakage from the spark plug cavities. The most direct approach to reducing leakage is minimizing the leakage area. TJI has a significantly smaller leakage area compared to the original spark plug where the flame is ejected from jet orifices.

In summary, combining low-temperature hydrogen and TJI is expected to enhance the performance of HWRE. However, existing research on the HWRE with pre-chamber has not been adequately studied. Particularly, the combination of low-temperature hydrogen and TJI has rarely been explored in WRE. Therefore, in this study, a three-dimensional computational fluid dynamics (CFD) model of turbulent jet ignition HWRE (TJI-HWRE) is established and the characteristics of the flow field and combustion in the cylinder at low temperature for both SI and TJI ignition modes are compared. At the same time, the effect of TJI on HWRE leakage and the influence of jet ignition timing on TJI-HWRE are investigated. These studies expand the applications of HWRE in aerospace and other fields, providing a reference for the application of TJI-HWRE.

## 2. Methodology

### 2.1. Geometric model generation

The engine used in this study is the Mazda 13B WRE, which has a peripheral intake port and two peripheral exhaust ports, as shown in Fig. 1(a). To investigate the effect of the passive pre-chamber ignition timing on low-temperature HWRE combustion, emissions, and leakage, a TJI-HWRE model was established using CATIA software and a three-dimensional dynamic simulation model was established using CONVERGE software. The simulation model of the TJI-HWRE is divided into 8 computational regions: intake port, exhaust port I, exhaust port II, chamber I, chamber II, chamber III, passive pre-chamber and spark T. Additionally, regions flow between different chambers are provided in Converge, which helps to analyze the leakage of WRE. The flow rate and flow mass between different regions can be selected in the regions flow, and the mass transfer between different regions can be obtained by integrating the flow rate, or directly calculating the flow mass. For example, by integrating the flow rate between region 3 and region 5 in the range of  $280^\circ\text{CA}$  and  $289^\circ\text{CA}$ , the mass of residual gas leaking from region 5 to region 3 can be obtained. The schematic diagram of the TJI-HWRE is shown in Fig. 1(b). Furthermore, the fuel properties of hydrogen are shown in Table 1.

The TJI-HWRE model only replaced the Leading Spark Plug (LSP) with a Passive pre-chamber (PPC), while the Trailing Spark Plug (TSP) remained unchanged. The rest of the model is identical to the actual engine. To achieve multi-point ignition, the PPC was connected to the main combustion chamber (MCC) through six injection channels, with an injection angle of  $40^\circ$ . Three channels are directed towards the front of the MCC, while the other three channels are directed towards the rear of the MCC. The volume ratio of PPC is defined as the ratio of the PPC volume to the MCC volume at the top dead center. The volume ratio of PPC selected in this study was 2.4 %. Table 2 presents the specifications of the TJI-HWRE. Fig. 2 illustrates the phase of the TJI-HWRE and the rotation direction of the rotor. Chamber I is the chamber selected for analysis and the top dead center of the intake stroke of chamber I is marked as  $0^\circ\text{CA}$ . The rotor starts rotating clockwise from  $0^\circ\text{CA}$  and ends with a total rotation of  $1080^\circ\text{CA}$ .

![Figure 1: Geometric models of (a) the Mazda 13B WRE and (b) the TJI-HWRE. (a) Mazda 13B WRE: A cross-sectional view of a Wankel engine rotor. The rotor is divided into three chambers (I, II, III) by two curved walls. The rotor rotates clockwise, as indicated by a curved arrow. The intake port is on the left, and the exhaust port is on the right. Two spark plugs are located on the top of the rotor: a leading spark plug and a trailing spark plug. (b) TJI-HWRE: A cross-sectional view of a hydrogen Wankel engine rotor. It features a passive pre-chamber located in the center of the rotor, which is connected to the main combustion chambers (I, II, III) via a small nozzle. The rotor has the same intake and exhaust ports as the Mazda 13B WRE. The rotor is shown in a similar orientation with a clockwise rotation arrow.](7e2f2d03a5dda38b038fd4884629a2b4_img.jpg)

Figure 1: Geometric models of (a) the Mazda 13B WRE and (b) the TJI-HWRE. (a) Mazda 13B WRE: A cross-sectional view of a Wankel engine rotor. The rotor is divided into three chambers (I, II, III) by two curved walls. The rotor rotates clockwise, as indicated by a curved arrow. The intake port is on the left, and the exhaust port is on the right. Two spark plugs are located on the top of the rotor: a leading spark plug and a trailing spark plug. (b) TJI-HWRE: A cross-sectional view of a hydrogen Wankel engine rotor. It features a passive pre-chamber located in the center of the rotor, which is connected to the main combustion chambers (I, II, III) via a small nozzle. The rotor has the same intake and exhaust ports as the Mazda 13B WRE. The rotor is shown in a similar orientation with a clockwise rotation arrow.

Fig. 1. The geometric model of (a) the Mazda 13B WRE and (b) the TJI-HWRE.

Table 1

Main properties of hydrogen [36].

|                                         | Hydrogen       |
|-----------------------------------------|----------------|
| Molecular Formula                       | H <sub>2</sub> |
| Density (20 °C)/(kg·m <sup>-3</sup> )   | 0.09           |
| Molecular weight (kg/kmol)              | 2.02           |
| Lower heating value (MJ/kg)             | 119.6          |
| Auto-ignition temperature (K)           | 773            |
| Stoichiometric air-fuel ratio by mass   | 34.6           |
| The energy density (MJ/m <sup>3</sup> ) | 4.7            |
| Research Octane Number                  | > 100          |
| Laminar flame velocity (m/s)            | 3.51           |
| Flammability Limits in the air (vol%)   | 4.7–75         |
| Adiabatic flame temperature (°C)        | 2100           |
| Latent heat of vaporization (kJ/kg)     | 461            |

Table 2

Structural parameters of TJI-HWRE.

| Structural parameters     | Value           |
|---------------------------|-----------------|
| Generating radius/(mm)    | 105             |
| Eccentricity/(mm)         | 15              |
| Width of rotor/(mm)       | 80              |
| Compression ratio         | 10              |
| Displacement/L            | 0.654           |
| Jet orifice diameter/(mm) | 1               |
| Number of jet orifices    | 6               |
| Intake timing/(°CA)       | 3 ATDC, 65 ABDC |
| Exhaust timing/(°CA)      | 50 BBDC, 3 BTDC |
| Fuel                      | Hydrogen        |

### 2.2. Boundary and initial conditions

This study was conducted under the operating conditions of the manifold absolute pressure (MAP) at 100 kPa, the engine speed at 3000 rpm, and the excess air coefficient ( $\lambda$ ) of 1.8. Table 3 lists the initial and boundary conditions of the HWRE used for model calibration and simulation. It should be noted that the inlet temperature listed in Table 3 is the value used during the HWRE model calibration. The value of inlet temperature will change when the effect of low temperature is investigated later. Fig. 3 shows the in-cylinder pressure at different inlet temperatures. It can be noticed that the in-cylinder pressure at the end of the compression stroke gradually increases as the inlet temperature decreases. This is because the decrease of the inlet temperature results in an increase of the fresh charge and the mass of hydrogen into the cylinder. After ignition, at the inlet temperature of 173 K, the in-cylinder pressure only rises a little due to the fact that the hydrogen is only

ignited a little, while at the inlet temperature of 123 K, the hydrogen cannot be ignited using SI. Therefore, we selected 223K as the research temperature for this article.

To investigate the impact of the hydrogen ignition timing (HIT) on the performance of low-temperature TJI-HWR, eight different HITs were set up. At the same time, two different inlet temperatures were set for HWRE at the same HIT to compare with the original engine. In summary, the above 10 cases were divided into two groups, Group A and Group B. The ignition mode of SI is used in group A, and the ignition mode of TJI is used in group B. Group A focuses on studying HWRE under different inlet temperatures but with the same HIT. Group B focuses on studying TJI-HWRE under the same inlet temperature but with different HITs. The relevant parameter settings are shown in Table 4.

### 2.3. Mathematical models

In CFD simulation calculations, the flow of the fluid needs to follow the laws of conservation of mass, momentum and energy, and the basic governing equations for these conservation laws are as follows:

The mass and momentum conservation equations:

$$\frac{\partial \rho}{\partial t} + \frac{\partial \rho u_i}{\partial x_i} = S \quad (1)$$

$$\frac{\partial \rho u_i}{\partial t} + \frac{\partial \rho u_i u_j}{\partial x_j} = -\frac{\partial p}{\partial x_i} + \frac{\partial \sigma_{ij}}{\partial x_j} + S_i \quad (2)$$

where  $\rho$  is the fluid density,  $u$  is the fluid velocity,  $S$  is the source item and  $\sigma$  is the stress tensor:

$$\sigma_{ij} = \mu \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right) + \left( \mu' \frac{2}{3} \mu \right) \left( \frac{\partial u_k}{\partial x_k} \right) \delta_{ij} \quad (3)$$

where  $\mu$  is the fluid viscosity,  $\mu'$  is the fluid expansion viscosity.

The energy conservation equation:

$$\frac{\partial \rho e}{\partial t} + \frac{\partial u_i \rho e}{\partial x_i} = -p \frac{\partial u_i}{\partial x_i} + \sigma_{ij} \frac{\partial}{\partial x_i} \left( K \frac{\partial T}{\partial x_i} \right) + \frac{\partial}{\partial x_i} \left( \rho D \sum_m h_m \frac{\partial Y_m}{\partial x_i} \right) + S \quad (4)$$

where  $K$  is the thermal conductivity of the fluid,  $T$  is the fluid temperature,  $D$  is the mass diffusion coefficient of the fluid,  $h$  is the enthalpy of the component and  $Y$  is the mass fraction of the component.

For the turbulence model, due to the rotational motion of the rotor inside the cylinder during WRE operation, the flow field inside it becomes highly complex. Therefore, an appropriate turbulence model needs to be chosen to accurately capture the flow field inside the cylinder. Fan et al. [37] compared the results of Particle Image Velocimetry

![Figure 2: A cross-sectional diagram of the TJI-HWRE engine showing its internal components and combustion chambers. The diagram includes a central rotor, intake and exhaust ports, and three combustion chambers (I, II, III). Key angles are marked: 270° CA for the Major axis, 540° CA for the Y-axis, 0/1080° CA for the Minor axis, and -810° CA for the X-axis. A trailing spark plug and a passive pre-chamber are also indicated. The rotation direction of the rotor is shown with an arrow.](ddfe517a5ad9c77c89a57a5e780b24ca_img.jpg)

Figure 2: A cross-sectional diagram of the TJI-HWRE engine showing its internal components and combustion chambers. The diagram includes a central rotor, intake and exhaust ports, and three combustion chambers (I, II, III). Key angles are marked: 270° CA for the Major axis, 540° CA for the Y-axis, 0/1080° CA for the Minor axis, and -810° CA for the X-axis. A trailing spark plug and a passive pre-chamber are also indicated. The rotation direction of the rotor is shown with an arrow.

Fig. 2. The phase of the TJI-HWRE.

**Table 3**  
 Initial and boundary conditions.

| Specification          | Type        | Value         |
|------------------------|-------------|---------------|
| Air inlet              | Inflow      | 100 kPa/305 K |
| Exhaust outlet         | Outflow     | 100 kPa/900 K |
| Rotor                  | Moving wall | 450 K         |
| Intake port            | Fixed wall  | 305 K         |
| Exhaust port           | Fixed wall  | 900 K         |
| Housing                | Fixed wall  | 450 K         |
| Spark plug             | Fixed wall  | 600 K         |
| Engine speed           | Constant    | 3000 rpm      |
| Excess air coefficient | Constant    | 1.8           |

**Table 4**  
 Summary of different HITs of TJI-HWRE.

| Case | Ignition mode | Inlet temperature /K | LSP/PPC ignition timing/°CA BTDC | TSP ignition timing/°CA ATDC |
|------|---------------|----------------------|----------------------------------|------------------------------|
| A1   | SI            | 305                  | 5                                | 5                            |
| A2   | SI            | 223                  | 5                                | 5                            |
| B1   | TJI           | 223                  | 5                                | 5                            |
| B2   | TJI           | 223                  | 10                               | 5                            |
| B3   | TJI           | 223                  | 15                               | 5                            |
| B4   | TJI           | 223                  | 16                               | 5                            |
| B5   | TJI           | 223                  | 17                               | 5                            |
| B6   | TJI           | 223                  | 18                               | 5                            |
| B7   | TJI           | 223                  | 19                               | 5                            |
| B8   | TJI           | 223                  | 20                               | 5                            |

![Figure 3: A line graph showing In-cylinder pressure (MPa) versus Crank angle (°CA) for different inlet temperatures. The graph includes four curves: 305 K (solid red), 223 K (solid blue), 173 K (dashed blue), and 123 K (dashed red). The operating conditions are N = 3000 rpm, λ = 1.8, MAP = 100 kPa, L-plug = 5 °CA BTDC, and T-plug = -5 °CA BTDC. The pressure peaks around 550 °CA, with higher inlet temperatures resulting in higher peak pressures.](2db53d6ef524be5cde118e647f73ed90_img.jpg)

Figure 3: A line graph showing In-cylinder pressure (MPa) versus Crank angle (°CA) for different inlet temperatures. The graph includes four curves: 305 K (solid red), 223 K (solid blue), 173 K (dashed blue), and 123 K (dashed red). The operating conditions are N = 3000 rpm, λ = 1.8, MAP = 100 kPa, L-plug = 5 °CA BTDC, and T-plug = -5 °CA BTDC. The pressure peaks around 550 °CA, with higher inlet temperatures resulting in higher peak pressures.

Fig. 3. In-cylinder pressure at different inlet temperatures.

(PIV) experiments with CFD simulations and found that the RNG  $k$ - $\epsilon$  turbulence model can accurately capture the turbulence information inside WRE. Therefore, the RNG  $k$ - $\epsilon$  turbulence model was adopted as the turbulence model in this study. The turbulent flow energy transfer

equation is shown below:

$$\frac{\partial \rho k}{\partial t} + \frac{\partial \rho u_i k}{\partial x_i} = \tau_{ij} \frac{\partial u_i}{\partial x_j} + \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_k} \frac{\partial k}{\partial x_j} \right) \rho e + \frac{c_s}{1.5} S_s \quad (5)$$

The turbulent kinetic energy dissipation equation is shown below:

$$\frac{\partial \rho e}{\partial t} + \frac{\partial (\rho u_i e)}{\partial x_i} = \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_e} \frac{\partial e}{\partial x_j} \right) + C_{\epsilon 3} \rho e \frac{\partial u_i}{\partial x_i} + \left( C_{\epsilon 1} \frac{\partial u_i}{\partial x_i} - C_{\epsilon 2} \rho S + C_S S_s \right) \frac{e}{k} + S - \rho R \quad (6)$$

where  $S$  is the source item,  $S_s$  is the source term interacting with the discrete phase (spray),  $\rho$  is the fluid density and  $\mu$  is the hydrodynamic viscosity. The  $e$  denotes the turbulent dissipation rate,  $Pr$  denotes the Prandtl number and  $k$  denotes the turbulent kinetic energy. The  $C_{\epsilon i}$  terms are model constants that represent compression and expansion. As for the combustion model, the SAGE combustion model was used in this study. The SAGE combustion model is capable of accurately simulating the combustion process of HWRE. In addition, combining the SAGE combustion model with the Stagni's model can effectively predict the  $NO_x$  emissions in HWRE [33]. Because the  $NO_x$  emissions in HWRE is mainly thermal  $NO_x$ , the mechanism of thermal  $NO_x$  generation is as

follows:

![](cda0cdebbbfc2356ef6553dfbba9a8ba_img.jpg)

$$O + N_2 \rightleftharpoons NO + N \quad N + O_2 \rightleftharpoons NO + O \quad N + OH \rightleftharpoons NO + H \quad (7)$$

### 2.4. The grid independence study and model validation

Fig. 4 illustrates the physical and schematic diagrams of the HWRE experimental test bench. The HWRE experiments were conducted under conditions of constant speed at 3000 rpm,  $\lambda$  maintained at 1.8, and constant ignition timing. Additionally, the HWRE experimental test bench was equipped with an electric dynamometer for speed control and torque monitoring. Furthermore, the original gasoline supply system was converted to a hydrogen supply system. To meet the need for precise control of hydrogen injection and ignition timing, an HECU (Hydrogen Electronic Control Unit) was developed to control the HWRE. The specific equipment information and their uncertainties are presented in Table 5.

**Table 5**

Experimental equipment information and their uncertainties.

| Parameter                     | Uncertainty          | Manufacturer | Type      |
|-------------------------------|----------------------|--------------|-----------|
| Engine speed                  | $\le \pm 1$ rpm      | Power link   | CAC6      |
| Torque                        | $\le \pm 0.4$ % F.S. | Power link   | CAC6      |
| Hydrogen volumetric flow rate | $\le \pm 0.02$ L/min | Seven star   | D07-60B   |
| Air volume flow rate          | $\le \pm 0.1$ L/min  | Tociel       | 20 N060   |
| Air-to-fuel ratio             | $\le \pm 0.007$      | Horiba       | MEXA-730λ |
| In-cylinder pressure          | $\le \pm 0.03$ MPa   | Kistler      | 6117BFD17 |

In three-dimensional CFD simulations, different grid sizes and refinement levels can result in varying numbers of grid cells, which have a significant impact on the simulation results. In the CONVERGE software, grids can be automatically generated based on the set grid size levels. Through adaptive mesh refinement (AMR), grids can be automatically refined to achieve accurate calculations when dealing with complex flow fields and temperature distributions inside the cylinder

![Figure 4: (a) Physical diagram and (b) schematic diagram of the HWRE experimental test bench. (a) shows a photograph of the test bench with labels: Intake port, Rotary engine, Dynamometer, Oxygen sensor, Exhaust port, and Exhaust sampling. (b) is a schematic diagram with numbered components: 1. Hydrogen container, 2. Hydrogen pressure governor, 3. Hydrogen pressure reducing valve, 4. Air filter, 5. Hydrogen flowmeter, 6. Air flowmeter, 7. Hydrogen arrester, 8. Hydrogen injector, 9. Crank angle sensor, 10. Rotary engine, 11. Trailing spark plug, 12. Leading spark plug, 13. HECU (Hydrogen Electronic Control Unit), 14. Calibration computer, 15. Combustion analyzer, 16. Dynamometer, 17. Dynamometer console, 18. Exhaust sampling, 19. Oxygen sensor, 20. Lambda analyzer, 21. Emissions analyzer. Signal lines (dashed red) and data lines (dashed black) connect the sensors and analyzers to the HECU and computers.](1a6d75c94d3fd49936527eadd25e9278_img.jpg)

1. Hydrogen container  
2. Hydrogen pressure governor  
3. Hydrogen pressure reducing valve  
4. Air filter  
5. Hydrogen flowmeter  
6. Air flowmeter  
7. Hydrogen arrester  
8. Hydrogen injector  
9. Crank angle sensor  
10. Rotary engine  
11. Trailing spark plug  
12. Leading spark plug  
13. HECU (Hydrogen Electronic Control Unit)  
14. Calibration computer  
15. Combustion analyzer  
16. Dynamometer  
17. Dynamometer console  
18. Exhaust sampling  
19. Oxygen sensor  
20. Lambda analyzer  
21. Emissions analyzer

Figure 4: (a) Physical diagram and (b) schematic diagram of the HWRE experimental test bench. (a) shows a photograph of the test bench with labels: Intake port, Rotary engine, Dynamometer, Oxygen sensor, Exhaust port, and Exhaust sampling. (b) is a schematic diagram with numbered components: 1. Hydrogen container, 2. Hydrogen pressure governor, 3. Hydrogen pressure reducing valve, 4. Air filter, 5. Hydrogen flowmeter, 6. Air flowmeter, 7. Hydrogen arrester, 8. Hydrogen injector, 9. Crank angle sensor, 10. Rotary engine, 11. Trailing spark plug, 12. Leading spark plug, 13. HECU (Hydrogen Electronic Control Unit), 14. Calibration computer, 15. Combustion analyzer, 16. Dynamometer, 17. Dynamometer console, 18. Exhaust sampling, 19. Oxygen sensor, 20. Lambda analyzer, 21. Emissions analyzer. Signal lines (dashed red) and data lines (dashed black) connect the sensors and analyzers to the HECU and computers.

**Fig. 4.** (a) The physical diagram and (b) schematic diagram of the HWRE experimental test bench.

![Figure 5: (a) Grid independence verification and (b) model validation of in-cylinder pressure and heat release rate. (a) shows mean in-cylinder pressure vs crank angle for various grid sizes (0.5 mm, 1 mm, 2 mm, 4 mm) and a 2 mm grid with AMR. (b) compares experimental and calculated mean in-cylinder pressure and heat release rate vs crank angle for lambda = 1.8.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 5(a) is a line graph showing Mean in-cylinder pressure (MPa) on the y-axis (0.5 to 3.5) versus Crank angle (°CA) on the x-axis (460 to 620). It compares five grid sizes: 4 mm grid (red solid line), 2 mm grid (yellow solid line), 2 mm grid with AMR (purple solid line), 1 mm grid (green solid line), and 0.5 mm grid (blue solid line). An inset graph zooms in on the peak pressure region (555 to 575 °CA). All curves are nearly identical, peaking around 3.3 MPa at 565 °CA. A legend box in the top left specifies: N = 3000 rpm, MAP = 100 kPa, LSP = 5 °CA BTDC, TSP = -5 °CA BTDC,  $\lambda = 1.6$ .

Figure 5(b) is a dual-axis line graph. The left y-axis is Mean in-cylinder pressure (MPa) (0 to 3.5) and the right y-axis is Heat release rate (J/°CA) (0 to 30). The x-axis is Crank angle (°CA) (-90 to 150). It compares experimental data (blue stars and red crosses) with calculated data (blue solid line and red dashed line) for  $\lambda = 1.8$ . The calculated pressure curve peaks at approximately 3.2 MPa at 30 °CA. The heat release rate curve peaks at approximately 20 J/°CA at 30 °CA. A legend box in the top left specifies: N = 3000 rpm, MAP = 100 kPa, LSP = 5 °CA BTDC, TSP = -5 °CA BTDC.

Figure 5: (a) Grid independence verification and (b) model validation of in-cylinder pressure and heat release rate. (a) shows mean in-cylinder pressure vs crank angle for various grid sizes (0.5 mm, 1 mm, 2 mm, 4 mm) and a 2 mm grid with AMR. (b) compares experimental and calculated mean in-cylinder pressure and heat release rate vs crank angle for lambda = 1.8.

Fig. 5. (a) The grid independence verification and (b) model validation of in-cylinder pressure and heat release rate.

[38]. In this study, five grid sizes are selected for grid independence verification: 0.5 mm, 1 mm, 2 mm, 4 mm and 2 mm with AMR. Among them, the 2 mm with AMR can automatically accurate the local mesh size to 0.25 mm according to the needs of the simulation process. It should be noted that the grid independence validation was carried out at  $\lambda$  of 1.6, engine speed of 3000 rpm, MAP of 100 kPa, LSP ignition timing of 5 °CA BTDC and TSP ignition timing of -5 °CA BTDC. The results are shown in Fig. 5(a). It can be observed that the computational results of the 2 mm grid with AMR are basically the same as those of the 0.5 mm and 1 mm grids, and the maximum difference in mean peak in-cylinder pressure is no more than 0.5 %. In addition, previous research [39] has demonstrated that using a grid size of 2 mm with AMR can effectively meet the computational requirements for HWRE. Therefore, considering both computational accuracy and computational time, this study selects the 2 mm grid with AMR. Since the in-cylinder pressure and heat release rate are widely used for model validation in engine simulation studies [40–44], these two parameters are selected for model validation in this study. The model validation was carried out at  $\lambda$  of 1.8, engine speed of 3000 rpm, MAP of 100 kPa, LSP ignition timing of 5 °CA BTDC and TSP ignition timing of -5 °CA BTDC. Fig. 5(b) shows the comparison of the simulated cylinder pressure and heat release rate with the experimental results at the same conditions. The results indicate that the simulated peak value of cylinder pressure and heat release rate have relatively small errors compared to the experiment, which can verify that the Mazda 13B HWRE model established in CONVERGE software can predict the engine performance with satisfying accuracy.

Some selected parameters, such as cylinder and wall temperatures, are derived from equations and experience using the measured in-cylinder pressure data. These parameter settings may affect the accuracy of the results. The experimental data used for calibration can also have an impact on the accuracy of the results due to uncertainties in the experimental equipment used for the measurements. The calibration experiments were conducted without a pre-chamber and this study mainly focused on numerical simulations for exploratory studies.

## 3. Results and discussion

### 3.1. Flow field and flame propagation analysis

The flow field characteristics in the MCC have a significant influence on the distribution and combustion of the charge. Thus, analyzing the flow field in the MCC is crucial. Vorticity characterizes the flow field inside the cylinder. Under the same operating conditions, vorticity represents the velocity streamlines within the cylinder [45]. The formation of the flow field in the MCC mainly forms during the intake and

compression strokes. Therefore, Fig. 6 depicts the variation of the flow field and vorticity inside the MCC at two different intake temperatures.

As shown in Fig. 6, at 430 °CA BTDC, the fresh charge forms two counter-directional vortices, labelled as Vortex I and Vortex II, after impacting the cylinder wall at both temperatures. Vortex I is in the upper part of the MCC, while Vortex II is in the lower part of the MCC. At this time, the average vorticity in the MCC is  $10175.70 \text{ s}^{-1}$  for ordinary intake temperature and  $10067.60 \text{ s}^{-1}$  for low intake temperature. From 310 °CA BTDC to 190 °CA BTDC, the engine transitions from the intake stroke to the compression stroke. The rotational motion of the rotor has a progressively greater influence on the main flow field. At both intake temperatures, the radii of Vortex I and Vortex II increase, indicating that both vortices are constantly dissipating. At 190 °CA BTDC, vortex II dissipates. The average vorticity in the MCC decreases from 4386.82 to  $1543.40 \text{ s}^{-1}$  at ordinary intake temperature. Similarly, the average vorticity in the MCC decreases from 4369.69 to  $1520.80 \text{ s}^{-1}$  under low intake temperature. From 70 °CA BTDC, due to the squeezing effect of the MCC, Vortex I gradually moves upward, its radius further increases, and it gradually merges into the main flow field. Consequently, the streamlines inside the MCC become smoother and more regular. At 70 °CA BTDC, the average vorticity in the MCC is  $1460.59 \text{ s}^{-1}$  at ordinary intake temperature and  $1189.84 \text{ s}^{-1}$  at low intake temperature. In general, during the intake stroke, the in-cylinder vorticity is mainly influenced by the intake airflow. The difference in intake airflow between Case A1 and Case A2 is mainly due to the intake temperature difference. From 430 °CA BTDC to 310 °CA BTDC, during the intake stroke, the difference in in-cylinder vorticity does not exceed 2 %. Hence, it can be inferred that the low temperature has a small effect on the average in-cylinder vorticity during the intake stroke. However, from 190 °CA BTDC to 70 °CA BTDC, the engine is in the compression stroke. With the MCC nearing the top dead center, the mainstream flow field is gradually formed, and the in-cylinder vorticity is mainly affected by both rotor movement and MCC compression. Since the effects of rotor movement and MCC compression are less influenced by intake airflow, the in-cylinder vorticity difference in this stage gradually increases under low temperature, reaching 18.54 % at 70 °CA BTDC. Thus, it can be concluded that the low temperature has a significant effect on the average in-cylinder vorticity during the compression stroke.

The distribution and concentration of OH radicals characterize the combustion location and the intensity of chemical reactions. Fig. 7 shows the combustion and velocity streamline changes in the MCC under SI and TJI. Since the ignition timings in various cases are before TDC, there are already OH radicals present at TDC. After TDC, with the consumption of hydrogen, the vorticity within the MCC initially increases and then decreases. From TDC to 30 °CA ATDC, the average

![Figure 6: Flow field and vorticity in the MCC in Case A1 and Case A2. The figure is a 2x4 grid of plots. The columns represent crank angles: 430°CA BTDC, 310°CA BTDC, 190°CA BTDC, and 70°CA BTDC. The rows represent cases: Case A1 (top) and Case A2 (bottom). Each plot shows a cross-section of the MCC with streamlines and a color map for vorticity. A color bar at the top indicates vorticity values from 0 to 11000 s⁻¹. Specific vorticity values are labeled for each plot: Case A1 (10175.70, 4386.82, 1543.40, 1460.59 s⁻¹) and Case A2 (10067.60, 4369.69, 1520.80, 1189.84 s⁻¹). Arrows labeled 'Vortex I' and 'Vortex II' point to specific regions of high vorticity. A horizontal arrow at the bottom indicates the 'Rotation direction'.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 6: Flow field and vorticity in the MCC in Case A1 and Case A2. The figure is a 2x4 grid of plots. The columns represent crank angles: 430°CA BTDC, 310°CA BTDC, 190°CA BTDC, and 70°CA BTDC. The rows represent cases: Case A1 (top) and Case A2 (bottom). Each plot shows a cross-section of the MCC with streamlines and a color map for vorticity. A color bar at the top indicates vorticity values from 0 to 11000 s⁻¹. Specific vorticity values are labeled for each plot: Case A1 (10175.70, 4386.82, 1543.40, 1460.59 s⁻¹) and Case A2 (10067.60, 4369.69, 1520.80, 1189.84 s⁻¹). Arrows labeled 'Vortex I' and 'Vortex II' point to specific regions of high vorticity. A horizontal arrow at the bottom indicates the 'Rotation direction'.

Fig. 6. Flow field and vorticity in the MCC in Case A1 and Case A2.

![Figure 7: Distribution of OH radicals and streamlines in the MCC for Case A1, Case A2, and Case B1. The figure is a 4x4 grid of plots. The columns represent crank angles: TDC, 10°CA ATDC, 20°CA ATDC, and 30°CA ATDC. The rows represent cases: Case A1 (top), Case A2 (second), Case B1 (third), and Case B1 (bottom). Each plot shows a cross-section of the MCC with streamlines and a color map for MOLEFRAC OH. A color bar at the top indicates OH concentration from 0 to 0.003. Specific vorticity values are labeled for each plot: Case A1 (1460.44, 1821.92, 2533.40, 2030.27 s⁻¹), Case A2 (1368.11, 1383.00, 1541.57, 1720.42 s⁻¹), and Case B1 (1299.36, 1730.40, 3208.15, 2530.60 s⁻¹). A horizontal arrow at the bottom indicates the 'Rotation direction'.](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 7: Distribution of OH radicals and streamlines in the MCC for Case A1, Case A2, and Case B1. The figure is a 4x4 grid of plots. The columns represent crank angles: TDC, 10°CA ATDC, 20°CA ATDC, and 30°CA ATDC. The rows represent cases: Case A1 (top), Case A2 (second), Case B1 (third), and Case B1 (bottom). Each plot shows a cross-section of the MCC with streamlines and a color map for MOLEFRAC OH. A color bar at the top indicates OH concentration from 0 to 0.003. Specific vorticity values are labeled for each plot: Case A1 (1460.44, 1821.92, 2533.40, 2030.27 s⁻¹), Case A2 (1368.11, 1383.00, 1541.57, 1720.42 s⁻¹), and Case B1 (1299.36, 1730.40, 3208.15, 2530.60 s⁻¹). A horizontal arrow at the bottom indicates the 'Rotation direction'.

Fig. 7. Distribution of OH radicals and streamlines in the MCC for Case A1, Case A2, and Case B1.

vorticity in the MCC is  $1961.51 \text{ s}^{-1}$  for Case A1,  $1503.27 \text{ s}^{-1}$  for Case A2, and  $2192.13 \text{ s}^{-1}$  for Case B1. This is because TJI can increase the vorticity in the MCC, which is beneficial for improving turbulent kinetic energy. Between 10 and 30 °CA ATDC, the distribution area and concentration of OH radicals in the MCC for Case A1 are both greater than those for Case A2. Thus, for SI, the flame kernel development and flame speed of the low-temperature hydrogen-air mixture are

much lower than those of the ordinary-temperature hydrogen-air mixture. After using TJI, the distribution area and concentration of OH radicals in the MCC for Case B1 are greater than those for Case A2. Therefore, for low-temperature hydrogen-air mixture, TJI can improve combustion. To achieve the same distribution area of OH radicals, Case B1 takes 20 °CA, while Case A2 takes 30 °CA, indicating that TJI can accelerate the flame speed. Additionally, after the jet flame hits the

rotor, the jet flame develops in both forward and backward directions. The airflow generated by the jet flame collides with the main airflow in the MCC, forming vortices that accelerate the gas flow, promote flame propagation towards the unburned zone in front of the cylinder, and reduce the area of the unburned zone.

As the temperature field can be used to characterize the flame front, it is also a way to characterize combustion. Fig. 8 illustrates the propagation of the flame front in the MCC at different ignition timings. Due to the ignition delay of TJI [46], to achieve the same or better performance, the ignition timing of TJI needs to be advanced compared to SI, as can be seen from the distribution area of OH radicals in Case A2 and Case B1 in Fig. 7. With the advancement of ignition timing, the flame development period becomes shorter and combustion becomes more adequate. At 35 °CA ATDC, Case B6 has a larger burned zone and a smaller unburned zone than other cases, indicating the most adequate combustion. Although the ignition timing of TSP remains constant at 5 °CA ATDC, flame fronts appear near the TSP for Case B5, Case B6, and Case B7. This is because the airflow formed by the jet flame entrains some combustible mixtures and propagates towards the TSP, which is ignited near the TSP. The jet flame strengthens the flame propagation to the end of the combustion chamber, improves the thermal atmosphere of the mixture near the TSP and accelerates the flame propagation at the TSP.

### 3.2. Leakage analysis

The leakage of WRE is an important factor affecting its performance. As mentioned earlier, the most significant leakage in apex leakage is the leading spark plug cavities leakage. Meanwhile, the leading spark plug cavities leakage includes leakage between adjacent chambers and leakage through the spark plug cavities. Therefore, this paper mainly analyzes these two leakage pathways under the two ignition modes. Fig. 9 illustrates the leakage pathways of residual gas and fresh mixture in the leading spark plug cavities leakage. The leakage through the spark plug cavities (Leakage pathway I and III) occurs between the working

chamber (Chamber I) and the LSP, as well as between the leading chamber (Chamber III) and the LSP. The leakage between adjacent chambers (Leakage pathway II and IV) occurs between Chamber I and Chamber III. The leakage of residual gas is from Chamber III, mostly to the LSP (Leakage pathway I), with a small portion leaking directly into Chamber I (Leakage pathway II). Similarly, the leakage of fresh mixture is from Chamber I, mostly to the LSP (Leakage pathway III), with a small portion leaking directly into Chamber III (Leakage pathway IV).

Fig. 10 shows the mass flow rate and the total mass of leakage gas between adjacent chambers for different cases. Fig. 11 displays the mass fraction of fresh mixture and residual gas in the leakage gas between adjacent chambers for different cases. Comparing Case A1 with Case A2, the introduction of a low-temperature hydrogen-air mixture into the original engine increases the total leakage between adjacent chambers by 8.94 %, from 1.23 to 1.34 mg. This is attributed to the rise in the total mass of hydrogen-air mixture entering the cylinder. Specifically, the leakage of fresh mixture rises from 0.66 to 0.83 mg, while the leakage of residual gas decreases from 0.57 to 0.51 mg. After replacing LSP with PPC, the total leakage between adjacent chambers is reduced due to the smaller leakage area. With the ignition timing unchanged, the total leakage between adjacent chambers decreases from 1.34 to 0.35 mg, a decrease of 73.88%. Specifically, the leakage of fresh mixture decreases from 0.83 to 0.10 mg, while the leakage of residual gas decreases from 0.51 to 0.25 mg. However, the change in ignition timing does not significantly affect the total leakage between adjacent chambers. The primary change is observed in the mass fraction of the fresh mixture and residual gas. As shown in Fig. 11, with the advancement of ignition timing, the mass fraction of residual gas in the leakage gas between adjacent chambers decreases, while the mass fraction of the fresh mixture increases. The mass fraction of residual gas in Case B6 is the smallest, while the mass fraction of the fresh mixture is the largest. This is because the mass fraction of fresh mixture and residual gas leakage between adjacent chambers is a process of one increasing as the other decreases. As previously mentioned, the combustion in the cylinder becomes more adequate as the ignition timing is advanced, and the combustion is most adequate at Case B6, and deteriorates thereafter due to too

![Figure 8: Temperature field in the MCC in different cases. The figure is a 4x5 grid of heatmaps showing temperature distribution in the MCC for five cases (Case B1, Case B2, Case B5, Case B6, Case B7) at four different ignition timings (10°CA ATDC, 20°CA ATDC, 30°CA ATDC, 35°CA ATDC). A color bar at the top indicates temperatures from 400 to 2300 K. The heatmaps show a flame front propagating from the spark plug (TSP) towards the unburned zone. At 35°CA ATDC, Case B6 shows the most complete combustion with a large 'Burned' area and a small 'Unburned' area. A rotation direction arrow points downwards on the right side of the grid.](643d86ebba41e16a88461bfcb3741de6_img.jpg)

Figure 8: Temperature field in the MCC in different cases. The figure is a 4x5 grid of heatmaps showing temperature distribution in the MCC for five cases (Case B1, Case B2, Case B5, Case B6, Case B7) at four different ignition timings (10°CA ATDC, 20°CA ATDC, 30°CA ATDC, 35°CA ATDC). A color bar at the top indicates temperatures from 400 to 2300 K. The heatmaps show a flame front propagating from the spark plug (TSP) towards the unburned zone. At 35°CA ATDC, Case B6 shows the most complete combustion with a large 'Burned' area and a small 'Unburned' area. A rotation direction arrow points downwards on the right side of the grid.

Fig. 8. Temperature field in the MCC in different cases.

![Figure 9: (a) Leakage pathway of fresh mixture and (b) leakage pathway of residual gas. Diagram (a) shows leakage pathways I and II from Chamber I to the spark plug cavity and then to Chamber III. Diagram (b) shows leakage pathways III and IV from the spark plug cavity to Chamber III. Both diagrams indicate the rotation direction of the cylinder.](0ba998c66ef6a980bac9c0c12e9452bf_img.jpg)

Figure 9: (a) Leakage pathway of fresh mixture and (b) leakage pathway of residual gas. Diagram (a) shows leakage pathways I and II from Chamber I to the spark plug cavity and then to Chamber III. Diagram (b) shows leakage pathways III and IV from the spark plug cavity to Chamber III. Both diagrams indicate the rotation direction of the cylinder.

Fig. 9. (a) The leakage pathway of fresh mixture and (b) the leakage pathway of residual gas.

![Figure 10: (a) Leakage gas mass flow rate between adjacent chambers and (b) leakage gas mass between adjacent chambers under different cases. Graph (a) is a line plot of mass flow rate vs. crank angle for cases A1, A2, B1, B2, B5, B6, and B7, showing leakage from chamber I to III and from III to I. Graph (b) is a bar chart of total leakage mass for the same cases, showing leakage of fresh mixture (blue) and residual gas (red).](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 10: (a) Leakage gas mass flow rate between adjacent chambers and (b) leakage gas mass between adjacent chambers under different cases. Graph (a) is a line plot of mass flow rate vs. crank angle for cases A1, A2, B1, B2, B5, B6, and B7, showing leakage from chamber I to III and from III to I. Graph (b) is a bar chart of total leakage mass for the same cases, showing leakage of fresh mixture (blue) and residual gas (red).

Fig. 10. (a) Leakage gas mass flow rate between adjacent chambers and (b) leakage gas mass between adjacent chambers under different cases.

![Figure 11: Mass fraction of fresh mixture and residual gas in the leakage gas between adjacent chambers under different cases. A dual-axis line plot showing mass fraction of fresh mixture (left axis, blue dashed line with stars) and mass fraction of residual gas (right axis, red solid line with squares) for cases B1, B2, B3, B4, B5, B6, B7, and B8.](0f3e3ea50bcceb86f6c524ab2b6f3e7a_img.jpg)

Figure 11: Mass fraction of fresh mixture and residual gas in the leakage gas between adjacent chambers under different cases. A dual-axis line plot showing mass fraction of fresh mixture (left axis, blue dashed line with stars) and mass fraction of residual gas (right axis, red solid line with squares) for cases B1, B2, B3, B4, B5, B6, B7, and B8.

Fig. 11. Mass fraction of fresh mixture and residual gas in the leakage gas between adjacent chambers under different cases.

early ignition moment. Therefore, as the ignition timing advances, less residual gas is generated in the chamber III (leading chamber), while the total leakage between adjacent chambers is almost the same. Consequently, the mass fraction of residual gas leaked from chamber III to the working chamber (chamber I) decreases, while the mass fraction of fresh mixture leaked from chamber I to chamber III increases, with both reaching their extreme values at Case B6. Afterwards, the mass fraction of residual gas leakage increases, while the mass fraction of fresh mixture leakage decreases. Secondly, there is a pressure equilibrium point between

chamber I and chamber III when the apex seal passes over the spark plug cavities. As the combustion in the cylinder improves, the time for chamber I and chamber III to reach pressure equilibrium is earlier, which leads to the leakage of fresh mixture from chamber I to chamber III starting earlier. As a result, the mass fraction of fresh mixture leakage increases and the mass fraction of residual gas leakage decreases, both reaching their extreme values at Case B6. When the combustion inside the cylinder deteriorates, the time to reach pressure equilibrium is delayed, the mass fraction of residual exhaust gas leakage increases, and the mass fraction of fresh mixture leakage decreases.

Fig. 12 shows the mass flow rate and the total mass of leakage gas between Chamber I and the spark plug cavities or PPC under different cases. Fig. 13 displays the mass fraction of fresh mixture and residual gas in the leakage gas between Chamber I and the spark plug cavities or PPC under different cases. As shown in Fig. 12, the introduction of low-temperature hydrogen-air mixture into the original engine increases the total leakage between Chamber I and the spark plug cavities by 17.81 %, from 5.11 to 6.02 mg. Specifically, the leakage of fresh mixture increases from 4.27 to 5.38 mg, while the leakage of residual gas decreases from 0.84 to 0.64 mg. Upon replacing LSP with PPC, the total leakage between Chamber I and PPC significantly decreased. The total leakage between Chamber I and PPC decreases from 6.02 to 1.00 mg, an 83.39 % reduction with constant ignition timing. Specifically, the leakage of fresh mixture is reduced from 5.38 to 0.96 mg and the leakage of residual gas is reduced from 0.64 to 0.04 mg. As the ignition timing is advanced, the total leakage between Chamber I and PPC initially increases and then decreases. The total leakage at Case B6 reaches its peak, which increases by 19.87 % compared with that of Case B1. At the same time, the mass fraction of fresh mixture in the leakage gas between Chamber I and PPC also increases and then decreases, while the mass fraction of residual gas decreases and then increases, both reaching their

![Figure 12: (a) Line graph of leakage gas mass flow rate vs crank angle for cases A1-A7. (b) Bar chart of total leakage gas mass for cases A1-A7.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 12(a) is a line graph showing the leakage gas mass flow rate between chamber I and the spark plug cavity or PPC (in kg/s) versus crank angle (in °CA) for seven cases (A1 to A7). The y-axis ranges from -0.010 to 0.010. The x-axis ranges from 240 to 480 °CA. The graph shows two main leakage events: 'Leading spark plug leakage' around 420 °CA and 'Trailing spark plug leakage' around 280 °CA. An inset shows a zoomed-in view of the trailing leakage between 284 and 288 °CA. Figure 12(b) is a bar chart showing the total leakage gas mass (in kg) for the same cases. The y-axis ranges from 0 to 7.0 × 10<sup>-6</sup>. The chart shows that Case A2 has the highest total leakage, followed by Case A1, while Cases B1 through B7 have significantly lower leakage.

Figure 12: (a) Line graph of leakage gas mass flow rate vs crank angle for cases A1-A7. (b) Bar chart of total leakage gas mass for cases A1-A7.

**Fig. 12.** (a) Leakage gas mass flow rate between chamber I and spark plug cavity or PPC and (b) leakage gas mass between chamber I and spark plug cavity or PPC under different cases.

![Figure 13: Dual-axis line graph showing mass fraction of fresh mixture and residual gas vs case name.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 13 is a dual-axis line graph showing the mass fraction of fresh mixture (left y-axis, 0 to 100%) and residual gas (right y-axis, 0 to 5%) versus case name (B1 to B8). The mass fraction of fresh mixture (blue dashed line with diamond markers) starts at approximately 96% for B1, drops to about 96.5% for B2, and then remains relatively stable around 99.5% for cases B3 through B8. The mass fraction of residual gas (red solid line with circle markers) starts at approximately 99.2% for B1, drops sharply to about 95.5% for B2, and then remains relatively stable around 95.5% for cases B3 through B8.

Figure 13: Dual-axis line graph showing mass fraction of fresh mixture and residual gas vs case name.

**Fig. 13.** Mass fraction of fresh mixture and residual gas in the leakage gas between chamber I and spark plug cavity or PPC under different cases.

peak at Case B6. Additionally, the combustion within the cylinder becomes more adequate with the advancement of ignition timing. The leakage gas between Chamber I and PPC is predominantly the fresh mixture leaked from Chamber I to PPC. In contrast, the leakage of residual gas from PPC to Chamber I is almost negligible, accounting for only 0.34 % of the total leakage at least.

### 3.3. Combustion and emissions performance analysis

The in-cylinder pressure is a crucial indicator of the combustion process, affecting both combustion efficiency and emissions performance. Fig. 14 presents the in-cylinder pressure and peak in-cylinder pressure for different cases. Comparing Case A1 and Case A2, the peak in-cylinder pressure in Case A2 decreases by 19.24 % due to the inhibitory effect of low-temperature combustion. After adopting TJI, the peak in-cylinder pressure increased by 13.20 % under the same conditions. This is because TJI enhances the ignition energy and ignites more low-temperature hydrogen with lower reaction activity. The high-speed flame from the jet orifices forms a secondary flame that propagates towards the rear of the MCC after striking the rotor, reducing the unburned area inside the cylinder together with the flame initially propagated towards the rear of the MCC. This is evident from the in-cylinder pressure curves of Case A2 and Case B1, where the pressure rise rate in Case B1 is greater than in Case A2. In addition, it can also be noticed that TJI

![Figure 14: (a) In-cylinder pressure vs crank angle for cases A1-A8. (b) Peak in-cylinder pressure vs case name.](64bacf564ff025df294b6d30341c76df_img.jpg)

Figure 14(a) is a line graph showing the in-cylinder pressure (in MPa) versus crank angle (in °CA) for eight cases (A1 to A8). The y-axis ranges from 1.0 to 4.0 MPa. The x-axis ranges from 480 to 620 °CA. The graph shows that the in-cylinder pressure peaks around 560-580 °CA. Cases A1 and A2 show the lowest pressure, while Cases B1 through B8 show significantly higher pressure. Figure 14(b) is a line graph showing the peak value of in-cylinder pressure (in MPa) for the same cases. The y-axis ranges from 2.4 to 4.0 MPa. The x-axis shows case names A1, A2, B1, B2, B3, B4, B5, B6, B7, and B8. The peak pressure starts at approximately 3.2 MPa for A1, drops to about 2.6 MPa for A2, and then increases to a peak of approximately 3.8 MPa for B6 before slightly decreasing for B7 and B8.

Figure 14: (a) In-cylinder pressure vs crank angle for cases A1-A8. (b) Peak in-cylinder pressure vs case name.

**Fig. 14.** (a) In-cylinder pressure and (b) peak in-cylinder pressure under different cases.



is characterized by the long ignition delay, with the pressure rise starting at 7° CA ATDC for Case A2 and 10° CA ATDC for Case B1 at the same ignition timing. With the advancement of the ignition timing, the peak in-cylinder pressure initially rises and then decreases. Case B6 has the highest peak in-cylinder pressure, 29.30 % higher than that of Case B1 and 18.21 % higher than that of Case A1. This is because advancing the ignition timing results in more fuel being combusted near TDC. However, excessive advancement of the ignition timing causes too much fuel to combust before TDC, producing negative work on the rotor motion, so the peak in-cylinder pressure decreases after Case B6.

The indicated thermal efficiency (ITE) and IMEP for various cases are presented in Fig. 15. For SI, using the low-temperature hydrogen-air mixture increases the IMEP from 0.5813 to 0.7053 MPa, resulting in a 21.33 % improvement in the engine's indicated power due to the

increase in total fuel mass. However, the ITE decreases from 38.07 % to 36.27 % due to poor combustion caused by insufficient ignition energy. After changing the ignition method to TJI, the IMEP increases from 0.7053 to 0.7218 MPa. Simultaneously, the ITE also increases from 36.27 % to 37.12 %. As the ignition timing advances, both ITE and IMEP increase and then decrease, reaching their peaks in Case B6. Compared to Case A1, Case B6 exhibits a 3.73 % increase in ITE and a 32.22 % improvement in IMEP. The increase in fuel amount in the cylinder improves the engine's indicated power, while the reduction in fresh mixture leakage also contributes to the increase in ITE and IMEP. The  $\text{NO}_x$  generated by hydrogen-air combustion are primarily thermal  $\text{NO}_x$ , and temperature has a significant impact on their formation, with most of it being NO [47]. Therefore, an analysis of the in-cylinder temperature field and the NO generation has been conducted. Fig. 16 shows the

![Figure 15: (a) Bar chart of Indicated thermal efficiency (%) for cases A1 through B8. (b) Bar chart of Indicated mean effective pressure (MPa) for cases A1 through B8. Data values are labeled on each bar.](eb903413d070b64f45cd763804ba443f_img.jpg)

Figure 15 consists of two bar charts. Chart (a) shows the Indicated thermal efficiency (%) for cases A1 through B8. The values are: A1: 38.07, A2: 36.27, B1: 37.12, B2: 38.69, B3: 39.18, B4: 39.30, B5: 39.40, B6: 39.49, B7: 39.03, B8: 38.66. Chart (b) shows the Indicated mean effective pressure (MPa) for cases A1 through B8. The values are: A1: 0.5813, A2: 0.7053, B1: 0.7218, B2: 0.7545, B3: 0.7625, B4: 0.7649, B5: 0.7669, B6: 0.7686, B7: 0.7625, B8: 0.7518.

Figure 15: (a) Bar chart of Indicated thermal efficiency (%) for cases A1 through B8. (b) Bar chart of Indicated mean effective pressure (MPa) for cases A1 through B8. Data values are labeled on each bar.

Fig. 15. (a) ITE and (b) IMEP under different cases.

![Figure 16: In-cylinder temperature field distribution at 80° CA ATDC for cases A1, A2, B1, B5, B6, and B7. Each case has a top cross-sectional view and a bottom planar view of the combustion chamber.](72d357d406618f3f884c3876fc3058ee_img.jpg)

Figure 16 displays in-cylinder temperature field distributions at 80° CA ATDC for six cases: Case A1, Case A2, Case B1, Case B5, Case B6, and Case B7. Each case is represented by two plots: a top cross-sectional view and a bottom planar view of the combustion chamber. A color bar at the top indicates the temperature scale from 1200 K (blue) to 2000 K (red). The specific temperatures for each case are: Case A1: 1755.42 K; Case A2: 1682.25 K; Case B1: 1686.63 K; Case B5: 1698.06 K; Case B6: 1711.87 K; Case B7: 1693.45 K.

Figure 16: In-cylinder temperature field distribution at 80° CA ATDC for cases A1, A2, B1, B5, B6, and B7. Each case has a top cross-sectional view and a bottom planar view of the combustion chamber.

Fig. 16. In-cylinder temperature field distribution at 80 °CA ATDC under different cases.

![Figure 17: (a) NO production and (b) mass of NO produced at 80 °CA ATDC under different cases. (a) Line graph showing NO mass/kg vs Crank angle/°CA for 8 cases (A1 to B8). (b) Bar chart showing NO mass at 80 °CA ATDC/kg for the same 8 cases.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 17(a) is a line graph showing NO mass (kg) on the y-axis (ranging from 0 to  $1.0 \times 10^{-7}$ ) versus Crank angle ( $^{\circ}$ CA) on the x-axis (ranging from 480 to 820). It displays the NO production profiles for eight cases: Case A1 (red solid line), Case A2 (blue solid line), Case B1 (cyan dashed line), Case B2 (green dashed line), Case B3 (dark green dashed line), Case B4 (red dashed line), Case B5 (yellow dashed line), Case B6 (purple dashed line), Case B7 (teal dashed line), and Case B8 (dark teal dashed line). The graph shows that NO production begins around 565  $^{\circ}$ CA and peaks between 650 and 750  $^{\circ}$ CA. Case A1 shows the highest NO production, peaking near  $1.0 \times 10^{-7}$  kg. Cases B1 through B8 show significantly lower NO production, with Case B6 being the lowest.

Figure 17(b) is a bar chart showing the NO mass at 80  $^{\circ}$ CA ATDC (kg) on the y-axis (ranging from 0 to  $1.1 \times 10^{-7}$ ) for the same eight cases. The bars are color-coded to match the cases in (a). Case A1 has the highest NO mass at approximately  $9.5 \times 10^{-8}$  kg. Case A2 is the lowest at approximately  $1.5 \times 10^{-8}$  kg. Cases B1 through B8 show intermediate values, with Case B6 being the lowest among them at approximately  $3.0 \times 10^{-8}$  kg.

Figure 17: (a) NO production and (b) mass of NO produced at 80 °CA ATDC under different cases. (a) Line graph showing NO mass/kg vs Crank angle/°CA for 8 cases (A1 to B8). (b) Bar chart showing NO mass at 80 °CA ATDC/kg for the same 8 cases.

Fig. 17. (a) NO production and (b) mass of NO produced at 80  $^{\circ}$ CA ATDC under different cases.

in-cylinder temperature field and average temperature at 80  $^{\circ}$ CA ATDC under different cases. The process of NO production at different cases and the mass of NO produced at 80  $^{\circ}$ CA ATDC are shown in Fig. 17. Introducing the low-temperature hydrogen-air mixture into the original machine reduces NO generation at 80  $^{\circ}$ CA ATDC by 85.86 %, even though the average in-cylinder temperature of Case A2 is only 73.17 K lower than that of Case A1. After using TJI, compared with SI, the average in-cylinder temperature increases slightly and NO generation is 17.83 % higher at 80  $^{\circ}$ CA ATDC. As the ignition timing advances, the NO generation first increases and then decreases, reaching its maximum at Case B6, which is consistent with the variation in the average in-cylinder temperature. Compared to Case A1, the NO generation in Case B6 also decreases by 59.03 %. The above analysis shows that low-temperature has a strong inhibitory effect on the NO generation.

# 4. Conclusions

In this paper, a three-dimensional simulation model of TJI-HWRE fueled by a low-temperature hydrogen-air mixture is developed and validated based on CONVERGE software. The in-cylinder flow field at different temperatures is explored. The effect of different ignition timings on combustion, leakage, and emission characteristics is then investigated under the wide-open throttle, 3000 r/min and the  $\lambda$  of 1.8 conditions. The main conclusions are as follows.

1. The flow fields in the MCC are not significantly different when the hydrogen-air mixture of different temperatures is fed into the cylinder. However, during the intake stroke, the low temperature has minimal impact on the in-cylinder vorticity, whereas during the compression stroke, it significantly affects the in-cylinder vorticity. The combustion performance of the low-temperature hydrogen-air mixture ignited by the spark plug is found to be unsatisfactory. Additionally, there is an increase in leakage between adjacent chambers and through the spark plug cavities under low-temperature condition.
2. The use of passive pre-chamber jet ignition for low-temperature hydrogen-air mixture improves combustion and significantly reduces leakage. Compared to SI, there is a 73.88 % reduction in leakage between adjacent chambers and an 83.39 % reduction in leakage through the spark plug cavities.
3. Changing the ignition timing of passive pre-chamber jet ignition affects the in-cylinder temperature, influencing the leakage and emission characteristics of TJI-HWRE. Advancing the ignition timing does not significantly change the total leakage between adjacent chambers, mainly due to the change in the proportion of fresh mixture and residual exhaust gas. The majority of the leakage gas

between Chamber I and PPC is the fresh mixture, with almost no residual exhaust gas. Advancing the ignition timing to 18  $^{\circ}$ CA BTDC results in a 59.03 % reduction in NO emissions compared to the original engine.

4. Changes in the ignition timing of passive pre-chamber jet ignition significantly impact flame development and propagation within the cylinder, affecting the performance of TJI-HWRE. Advancing the ignition timing to 18  $^{\circ}$ CA BTDC increases the peak in-cylinder pressure from 2.93 to 3.79 MPa, and the ITE reaches 39.49 %. Compared with the original engine, the IMEP increases by 32.22 %.

In summary, the combination of low-temperature hydrogen and passive pre-chamber jet ignition improves combustion performance and reduces NO emissions. However, the simulations in this study are only conducted under lean combustion conditions. Exploration under rich combustion and stoichiometric ratio conditions remains to be investigated. Future work will modify the structural parameters of the passive pre-chamber to study the impact of different structures on combustion, leakage, and emissions of HWRE. Furthermore, exploration can be extended to the application of passive pre-chamber jet ignition in an ammonia-hydrogen dual-fuel WRE.

# CRediT authorship contribution statement

Changwei Ji: Writing – review & editing. Hanlin Li: Writing – original draft, Methodology, Investigation, Data curation. Jinxin Yang: Supervision, Conceptualization. Hao Meng: Resources, Formal analysis.

# Declaration of competing interest

The authors declare the following financial interests/personal relationships which may be considered as potential competing interests: None.

# Acknowledgments

This work was financially supported by the National Natural Science Foundation of China (No. 52276097) and the "JBGS" Project of Inner Mongolia Autonomous Region, China (No. 2022JBGS0008).

# Data availability

Data will be made available on request.

# References

- [1] Karali HI, Energy H Caliskan. exergy, sustainability, thermoeconomic, exergoeconomic, environmental and environmental-economic effects of novel boron-containing open cell geopolymer filter of a diesel engine on exhaust emissions. *Energy* 2024;290:130247. <https://doi.org/10.1016/j.energy.2024.130247>.
- [2] Wang H, Ji C, Shi C, Wang S, Yang J, Ge Y. Investigation of the gas injection rate shape on combustion, knock and emissions behavior of a rotary engine with hydrogen direct-injection enrichment. *Int. J. Hydrog. Energy* 2021;46:14790–804. <https://doi.org/10.1016/j.ijhydene.2021.01.234>.
- [3] Huang J, Gao J, Yang C, Tian G, Ma C. The effect of ignition timing on the emission and combustion characteristics for a hydrogen-fuelled ORP engine at lean-burn conditions. *Processes* 2022;10:1534. <https://doi.org/10.3390/pr10081534>.
- [4] Ji C, Meng H, Wang S, Wang D, Yang J, Shi C, et al. Realizing stratified mixtures distribution in a hydrogen-enriched gasoline Wankel engine by different compound intake methods. *Energy Conv. Manag.* 2020;203:112230. <https://doi.org/10.1016/j.enconman.2019.112230>.
- [5] Li J, Gao J, Tian G, Ma C, Xing S. An effective approach of dropping the backfire possibilities of a hydrogen-fuelled opposed rotary piston engine. *Energy Sci Eng* 2021;9:1061–7. <https://doi.org/10.1002/ese3.893>.
- [6] Sun Z, Li G. Propagation characteristics of laminar spherical flames within homogeneous hydrogen-air mixtures. *Energy* 2016;116:116–27. <https://doi.org/10.1016/j.energy.2016.09.103>.
- [7] Meng H, Ji C, Yang J, Chang K, Xin G, Wang S. Experimental understanding of the relationship between combustion/flow/flame velocity and knock in a hydrogen-fueled Wankel rotary engine. *Energy* 2022;258:124828. <https://doi.org/10.1016/j.energy.2022.124828>.
- [8] Oh S, Kim C, Lee Y, Yoon S, Lee J, Kim J. Experimental investigation of the hydrogen-rich offgas ignition engine under the various compression ratios. *Energy Conv. Manag.* 2019;201:112136. <https://doi.org/10.1016/j.enconman.2019.112136>.
- [9] Vancilie J, Demuynck J, Sileghem L, Van De Ginste M, Verhelst S. Comparison of the renewable transportation fuels, hydrogen and methanol formed from hydrogen, with gasoline – engine efficiency study. *Int. J. Hydrog. Energy* 2012;37:9914–24. <https://doi.org/10.1016/j.ijhydene.2012.03.145>.
- [10] Carney D. Toyota unveils more new gasoline ICEs with 40% thermal efficiency. *SAE Report* 2018.
- [11] Hong C, Ji C, Wang S, Xin G, Wang Z, Meng H, et al. Assessment of a synergistic control of intake and exhaust VVT for airflow exchange, combustion, and emissions in a DI hydrogen engine. *Int. J. Hydrog. Energy* 2023;48:20495–506. <https://doi.org/10.1016/j.ijhydene.2023.03.002>.
- [12] Meng H, Ji C, Li H, Yang J, Wang S. Insights into syngas-fueled Wankel rotary engine performance from varied CO/H<sub>2</sub> ratio. *Int. J. Hydrog. Energy* 2023. <https://doi.org/10.1016/j.ijhydene.2023.07.260>.
- [13] Meng H, Ji C, Wang S, Yang J. A review: centurial progress and development of Wankel rotary engine. *Fuel* 2023;335:127043. <https://doi.org/10.1016/j.fuel.2022.127043>.
- [14] Zambalov SD, Yakovlev IA, Maznoy AS. Effect of multiple fuel injection strategies on mixture formation and combustion in a hydrogen-fueled rotary range extender for battery electric vehicles. *Energy Conv. Manag.* 2020;220:113097. <https://doi.org/10.1016/j.enconman.2020.113097>.
- [15] Chen W, Pan J, Yang W, Liu Y, Fan B, Lu Y, et al. Stratified combustion characteristics analysis and assisted-ignition strategy optimization in a natural gas blended diesel Wankel engine. *Fuel* 2021;292:120192. <https://doi.org/10.1016/j.fuel.2021.120192>.
- [16] Fan B, Wang Y, Zhang Y, Pan J, Yang W, Zeng Y. Numerical investigation on the combustion performance of a natural gas/hydrogen dual fuel rotary engine under the action of apex seal leakage. *Energy Fuels* 2021;35:770–84. <https://doi.org/10.1021/acs.energyfuels.0c03498>.
- [17] Meng H, Ji C, Xin G, Yang J, Chang K, Wang S. Comparison of combustion, emission and abnormal combustion of hydrogen-fueled Wankel rotary engine and reciprocating piston engine. *Fuel* 2022;318:123675. <https://doi.org/10.1016/j.fuel.2022.123675>.
- [18] Morimoto K, Teramoto T, Takamori Y. Combustion characteristics in hydrogen fueled rotary engine. *Sae* 1992.
- [19] Fan B, Pan J, Yang W, Zhu Y, Chen W. Effects of hydrogen blending mode on combustion process of a rotary engine fueled with natural gas/hydrogen blends. *Int. J. Hydrog. Energy* 2016;41:4039–53. <https://doi.org/10.1016/j.ijhydene.2016.01.006>.
- [20] Jiao H, Zou R, Wang N, Luo B, Pan W, Liu J. Optimization design of the ignition system for Wankel rotary engine considering ignition environment, flow, and combustion. *Appl Therm Eng* 2022;201:117713. <https://doi.org/10.1016/j.applthermaleng.2021.117713>.
- [21] Gao J, Wang X, Song P, Tian G, Ma C. Review of the backfire occurrences and control strategies for port hydrogen injection internal combustion engines. *Fuel* 2022;307:121553. <https://doi.org/10.1016/j.fuel.2021.121553>.
- [22] Shi C, Chai S, Wang H, Ji C, Ge Y, Di L. An insight into direct water injection applied on the hydrogen-enriched rotary engine. *Fuel* 2023;339:127352. <https://doi.org/10.1016/j.fuel.2022.127352>.
- [23] Meng H, Ji C, Shen J, Yang J, Yang G, Chang K, et al. Analyzing the effects of cooled EGR on the knock of hydrogen-fueled Wankel rotary engine. *Int. J. Hydrog. Energy* 2022;47:33094–104. <https://doi.org/10.1016/j.ijhydene.2022.07.185>.
- [24] Fridriksson H, Sundén B, Tunér M, Andersson Ö. Heat transfer in diesel and partially premixed combustion engines: A computational fluid dynamics study. *Heat Transf. Eng.* 2017;38:1481–95. <https://doi.org/10.1080/01457632.2016.1255086>.
- [25] Trombley G, Toulson E. A fuel-focused review of pre-chamber initiated combustion. *Energy Conv. Manag.* 2023;298:117765. <https://doi.org/10.1016/j.enconman.2023.117765>.
- [26] Malé Q, Vermorel O, Ravet F, Poinsot T. Direct numerical simulations and models for hot burnt gases jet ignition. *Combust Flame* 2021;223:407–22. <https://doi.org/10.1016/j.combustflame.2020.09.017>.
- [27] Chen L, Zhang S, Zhang R, Li J, Yang P, Pan J, et al. Optical experiments on the effect of turbulent jet ignition on lean burning and engine knocking. *Fuel* 2022;307:121869. <https://doi.org/10.1016/j.fuel.2021.121869>.
- [28] Toulson E, Schock HJ. A review of pre-chamber initiated jet ignition combustion systems. *SAE Technical Paper* 2010. <https://doi.org/10.4271/2010-01-2263>.
- [29] Shah A, Tuenstal P, Johansson B. Effect of pre-chamber volume and nozzle diameter on pre-chamber ignition in heavy duty natural gas engines. *SAE Technical Paper* 2015. <https://doi.org/10.4271/2015-01-0867>.
- [30] Benajes J, Novella R, Gomez-Soriano J, Martinez-Hernandez PJ, Libert C, Dabiri M. Evaluation of the passive pre-chamber ignition concept for future high compression ratio turbocharged spark-ignition engines. *Appl Energy* 2019;248:576–88. <https://doi.org/10.1016/j.apenergy.2019.04.131>.
- [31] Liu Z, Zhou L, Zhong L, Wei H. Enhanced combustion of ammonia engine based on novel air-assisted pre-chamber turbulent jet ignition. *Energy Conv. Manag.* 2023;276:116526. <https://doi.org/10.1016/j.enconman.2022.116526>.
- [32] Fan B, Wu X, Pan J, Zeng Y, He R, Fang J, et al. Numerical investigation of the effect of jet orifice parameters on the combustion process of a turbulent jet ignition rotary engine fueled with methanol/gasoline blends. *Fuel Process Technol* 2023;245:107723. <https://doi.org/10.1016/j.fuproc.2023.107723>.
- [33] Yang Z, Ji C, Yang J, Wang H, Huang X, Wang S. The optimization of leading spark plug location and its influences on combustion and leakage in a hydrogen-fueled Wankel rotary engine. *Int. J. Hydrog. Energy* 2023;48:20465–82. <https://doi.org/10.1016/j.ijhydene.2023.02.099>.
- [34] Yang Z, Ji C, Huang X, Yang J, Wang H, Wang S. Modeling and analysis of apex seal leakage in a hydrogen fueled Wankel rotary engine. *Fuel* 2023;331:125848. <https://doi.org/10.1016/j.fuel.2022.125848>.
- [35] Zhang S, Liu J, Zuo Z, Zhang Y. An analytical investigation of oil film thickness for the apex seal in a small Wankel rotary engine. *Tribol Int* 2017;116:383–93. <https://doi.org/10.1016/j.triboint.2017.07.031>.
- [36] Qiang Y, Ji C, Wang S, Xin G, Hong C, Wang Z, et al. Study on the effect of variable valve timing and spark timing on the performance of the hydrogen-fueled engine with passive pre-chamber ignition under partial load conditions. *Energy Conv. Manag.* 2024;302:118104. <https://doi.org/10.1016/j.enconman.2024.118104>.
- [37] Fan B, Wu X, Pan J, Qi X, Fang J, Lu Q, et al. Research on the structure of pre-chamber and jet orifice of a turbulent jet ignition rotary engine fueled with methanol/gasoline blends. *Appl Therm Eng* 2023;229:120588. <https://doi.org/10.1016/j.applthermaleng.2023.120588>.
- [38] Chang K, Ji C, Wang S, Yang J, Meng H, Wang H, et al. Comparative study on different spark plug positions of a rotary engine with gasoline port and direct injection. *Fuel* 2022;310:122376. <https://doi.org/10.1016/j.fuel.2021.122376>.
- [39] Chang K, Ji C, Wang S, Yang J, Wang H, Xin G, et al. Numerical investigation of the combined effect of injection angle and injection pressure in a gasoline direct injection rotary engine. *Energy* 2022;254:124371. <https://doi.org/10.1016/j.energy.2022.124371>.
- [40] Gong C, Sun J, Liu F. Numerical research on combustion and emissions behaviors of a medium compression ratio direct-injection twin-spark plug synchronous ignition methanol engine under steady-state lean-burn conditions. *Energy* 2021;215:119193. <https://doi.org/10.1016/j.energy.2020.119193>.
- [41] Kakoe A, Bakshian Y, Ghareghani A, Salahi MM. Numerical comparative study of hydrogen addition on combustion and emission characteristics of a natural-gas/dimethyl-ether RCCI engine with pre-chamber. *Energy* 2019;186:115878. <https://doi.org/10.1016/j.energy.2019.115878>.
- [42] Mrzljak V, Medica V, Bukovac O. Volume agglomeration process in quasi-dimensional direct injection diesel engine numerical model. *Energy* 2016;115:658–67. <https://doi.org/10.1016/j.energy.2016.09.055>.
- [43] Wei W, Li G, Zhang Z, Long Y, Zhang H, Huang Y, et al. Effects of ammonia addition on the performance and emissions for a spark-ignition marine natural gas engine. *Energy* 2023;272:127092. <https://doi.org/10.1016/j.energy.2023.127092>.
- [44] Zhu Z, Mu Z, Wei Y, Du R, Guan W, Liu S. Cylinder-to-cylinder variation of knock and effects of mixture formation on knock tendency for a heavy-duty spark ignition methanol engine. *Energy* 2022;254:124197. <https://doi.org/10.1016/j.energy.2022.124197>.
- [45] Yang J, Ji C, Wang S, Wang D, Shi C, Ma Z, et al. Numerical study of hydrogen direct injection strategy on mixture formation and combustion process in a partially premixed gasoline Wankel rotary engine. *Energy Conv. Manag.* 2018;176:184–93. <https://doi.org/10.1016/j.enconman.2018.09.008>.
- [46] Wang Z, Ji C, Zhang T, Wang S, Yang H, Zhai Y, et al. Effect of ammonia addition on combustion characteristics of hydrogen/air using passive turbulent jet ignition. *Appl Therm Eng* 2024;236:121827. <https://doi.org/10.1016/j.applthermaleng.2023.121827>.
- [47] Stagni A, Cavallotti C, Arunthanayothin S, Song Y, Herbinet O. An experimental, theoretical and kinetic-modeling study of the gas-phase oxidation of ammonia. *React Chemistry & Engineering* 2020;696–711.