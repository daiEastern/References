![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Fuel journal cover](390120de4fe440c42fea8154fcaad334_img.jpg)

Fuel journal cover

## Full Length Article

![Check for updates button](4f4b52340aaccb1bcf733468dca9ee03_img.jpg)

Check for updates button

# Comparative analysis of chamber dimension and recess location on combustion behavior in a rotary engine with hydrogen addition

Jianhui Bao<sup>a,\*</sup>, Xiaomeng Wang<sup>a</sup>, Guohong Tian<sup>b</sup>, Fuquan Nie<sup>c,\*</sup>, Xiaodong Yan<sup>c</sup>, Cheng Shi<sup>d,\*</sup><sup>a</sup> Key Laboratory for Microstructural Material Physics of Hebei Province, School of Science, Yanshan University, Qinhuangdao 066004, China<sup>b</sup> Department of Mechanical Engineering Sciences, University of Surrey, Guildford GU2 7XH, United Kingdom<sup>c</sup> School of Mechanical and Electrical Engineering, Henan Institute of Science and Technology, Xinxiang 453003, China<sup>d</sup> School of Vehicle and Energy, Hebei Engineering Research Center for Low Carbon Development and Resource Utilization of Fossil Energy Sources, Yanshan University, Qinhuangdao 066004, China

## ARTICLE INFO

### Keywords:

Rotary engine  
Combustion behavior  
Hydrogen addition  
Flow phenomena  
Recess position  
Chamber volume

## ABSTRACT

The amelioration of the combustion chamber is an important approach in the quest towards a low-carbon and high-efficiency rotary engine and chamber dimension and recess location are two aspects of improvement opportunities. A three-dimensional computational fluid dynamics model was implemented and verified in the CONVERGE solver coupled with the SAGE detailed kinetic mechanisms. The results indicate that by modifying the chamber to a small volume, the combustion initiation is advanced to some extent resulting in a rapid combustion process, which presents better combustion characteristics and indicated efficiency. The investigated rotary engine achieves the highest indicated thermal efficiency and maximum pressure rising rate in the course of the leading recess, while the contrary patterns are witnessed for the trailing recess. Adopting the leading recess within the rotor chamber allows pronounced unburned HC and CO reductions at the price of acceptable NO<sub>x</sub> formation. The findings of the present work helped the designers gain a preferable understanding of the control mechanism of hydrogen-enriched combustion and shall give insights into the effectiveness of reducing the chamber dimension and arranging the recess in the leading part within the rotor chamber for enhancing ignition event and combustion process of this engine concept in engineering applications.

## 1. Introduction

As one of the oscillatory motion rotary engines [1], the Wankel engine is inherently designed with compact architecture, higher power density, lower mechanical vibration, multi-fuel adaptability, and ease of maintenance [2]. Although only this type of rotary-designed philosophy has managed the leap into production, the oscillatory motion engine concept performs attractiveness in certain application areas as usual [3], including the propulsion for UAVs [4], range extenders for BEVs [5], auxiliary power units for military equipment, etc. [6]. However, Wankel engines still have major setbacks that have not allowed the design philosophies to flourish and compete with the reciprocating piston engine to serve as prime movers [7]. Two significant problems involved with Wankel engines are poor efficiency and unwished hydrocarbon (HC) emissions [8]. With the development of new technologies, numerous approaches that have been well documented to date have covered the Wankel engine [9]. For future Wankel design to become a viable and

eco-friendly power plant, they will have to beyond the conventional reciprocating-piston performance criteria [10]. Apparent is the fact that the Wankel philosophy eliminates many parts equipped in a reciprocating-type engine [11]. Many aspects of this engine design are involved in enhancing the efficiency and reducing emission production of Wankel engines [12]. Efforts that concentrate on alternative fuel usage are a large area of research and development [13].

Recently, adequate Wankel engine work has been well-documented to concentrate on hydrogen fuel with high-efficiency and clean usage for Wankel rotary engines, either as a single supplement [14] or as a polyblend to petroleum fuel [15]. This significant work reported that the introduction of hydrogen has made an overall enhancement in engine efficiency [16] and a decrement in carbon monoxide (CO) [17] and unburned HC generations [18]. Compared to the reciprocating-piston engine, hydrogen is identified to be a preferable option for Wankel rotary mechanisms owing to its small quenching gap [19], which makes the flame spread nearly to the edge and corner of the housing wall and

\* Corresponding authors.

E-mail addresses: [baojh@ysu.edu.cn](mailto:baojh@ysu.edu.cn) (J. Bao), [lyywllyx@sina.com](mailto:lyywllyx@sina.com) (F. Nie), [shicheng@ysu.edu.cn](mailto:shicheng@ysu.edu.cn) (C. Shi).

accelerate the total mass combustion rate through higher burning velocity [20]. However, several drawbacks have stalled this engine concept progression when hydrogen usage for Wankel engines alone [21]. For example, the hydrogen-fueled combustion intensifies the heat flux through the walls hence more cooling losses due to higher temperature under the stoichiometric operation condition and higher surface-to-volume ratio of the engine [22]. Another critical challenge for hydrogen Wankel engines lies in the higher heat release rate leading to knock combustion due to the fast flame propagation and unstable conditions involved [23]. Moreover, advanced technologies are urgently needed to solve bottleneck problems such as limited supply infrastructure, lower production efficiency, and expensive storage and transportation costs [24]. Despite this, hydrogen doping is still deemed to be an acceptable fuel for rotary engines and has attracted increasing interest in recent years [25]. Ozcanli et al. [26] summarized that hydrogen doped to gasoline is a preferable practical solution compared with pure hydrogen usage, and enables the powertrain to extend cruising range, address the storage and transporting issue, and restrain the misfire of Wankel engines. Zambalov et al. [27] have demonstrated that hydrogen addition is a feasible method of weakness elimination specific to Wankel engines. In light of this, the role of hydrogen as a combustion enhancer is illustrated in our preliminary study to enhance engine efficiency and decrease pollutant production accordingly [28].

Engine miniaturization is one of the most prospective approaches to improving fuel economy and satisfying pollutant regulations, and decreasing the chamber volume is one of the useful methods to realize engine miniaturization [29]. In the later period of the compression process, the high compression ratio increases the mixture temperature and chamber pressure, which not only promotes the initial kernel and flame propagation but also is conducive to the subsequent thermal efficiency of Wankel engines [30]. Nevertheless, as the compression ratio is too high, the friction of the motion parts aggravates therefore resulting in an unwished mechanical efficiency of the Wankel engine [31]. While, it is possible to cause spontaneous combustion of the mixture and increase the knock propensity, thereby affecting the torque and power output [32]. The compression ratio of the engine is mainly divided into the geometric compression ratio and effective compression ratio [33]. For rotary engines, since there are no valve timing and crank and rod mechanisms compared to reciprocating engines, the intake and exhaust strokes of the rotary mechanism remain constant [34]. Therefore, there is no effective concept in terms of Wankel rotary engines. The geometric compression ratio denotes the ratio of the maximum volume (the volume when the rotor is at the BDC) to the minimum volume (the volume when the rotor is at the TDC) of a certain working chamber of the rotary engine [35]. It manifests the intensity level at which the combustible gas is compressed as the EA position varies from the BDC to the TDC. The geometric compression ratio of the rotary engine can be increased by elevating the trochoid ratio (eccentricity shape factor, K) or reducing the recess (pocket) volume in the rotor chamber without altering the structure of the intake port [36]. As a significant geometric specialization of the Wankel engine, changing the shape factor is inevitable to induce a variation in the architecture of Wankel engines, and its operations are complicated in the actual manufacturing process [37]. Nevertheless, there is no need to review the other fundamental framework by modifying the volumetric displacement of the working chamber [38]. The alteration in compression ratios could be performed only by proper design and modifications of the recess shape. The existing experimental results of the reciprocating piston engine show that the large compression ratio could be obtained by downsizing the volume of the piston recess in the working cylinder, namely, the “recess filling” method [39]. Therefore, it is feasible to evaluate the impact of recess modification on the combustion and flow phenomena of Wankel engines by changing the pocket chamber volumes, which provides a reference and design ideas for engineering applications.

Over the past few decades, extensive work and design optimization has been done on how the recess shape of the cylinder affects the

combustion process of reciprocating piston engines [40]. The considerable interest results from the fact that it can not only enhance the fuel economy and power performance but also decrease the pollutants generation of the engine [41]. For Wankel rotary engines, the mixing quality of intake charge and fresh air within the engine is poor because of the elongated combustion chamber, which makes it more prone to the quenching effect during the growth of the flame front [42]. Therefore, the majority of the unburnt mixture remains around the edge and corner of the rotor chamber [43]. Past approaches have proved that developing a reasonable recess design had great potential to enhance the turbulence and combustion behavior inside the engine [44]. Benefits from the intense directed flow in the rotating direction of the rotor [45], strengthening the turbulence thus could occur by arranging the pocket location within the rotor chamber [46]. Fan et al. [47] compared the impact of different recess locations on the combustion processes of small-sized Wankel engines and gained coherent findings such as the flow field, velocity gradient, and combustion initiation. In a Wankel engine fueled with diesel fuel, the influence of varying pocket geometries on the flow field evolution has been studied by Zhou et al. [48]. They found that superior combustion can be achieved through a recess located in the middle part of the rotor chamber inside the engine. Pisonoy and Tartakovsky [49] evaluated the addition of a slot in the rear part of the rotor recess for performance enhancement of the Wankel engine, and their work found that the presence of a slot is necessary for the prevention of initial flame quenching in the trailing side, while restricting the increased volume to a minimum.

As discussed in the above paragraphs, although multiple significant works on combustion chamber design for rotary engines have been well documented in the literature, there have been no efforts to clarify the potential of the association of recess modification and pocket arrangement applied to the hydrogen-enriched Wankel engine. Optimization of engine output with a higher compression ratio was therefore doubtful. The influence of pocket location in the rotor chamber on the Wankel engine operation with hydrogen enrichment also remains to be clarified. It is imperative to intuitively observe the turbulence motion and combustion phenomena consequently. In this scenario, a detailed non-reactive flow resolution could offer a clear insight into the organization of the flow phenomena inside the Wankel engine. Furthermore, computational fluid dynamics (CFD) provides the inherent merit of carrying out a depth analysis of the fluid mechanics without the restrictions implemented by engine hardware interference. However, to the best of our knowledge, no technical literature has involved any coherent information concerning the relevant research of the Wankel philosophy.

In the course of this research, a detailed chemical reaction mechanism for the combined hydrogen and dual-component gasoline fuel combustion was employed and merged into the numerical simulation platform with the support of *Convergent Science, Inc.* A modified single-rotor hydrogen-enriched gasoline rotary engine was used to obtain the experimental results for validating the computational model and reaction mechanism. Then, variations of combustion characteristics and emissions performance under different rotor chamber dimensions and pocket arrangements are analyzed progressively to assess the impacts of chamber volume and recess position. The inherent mechanisms of how these two elements create these effects are presented. Lastly, the numerical simulation results are discussed and the major findings are summarized.

## 2. Materials and methods

In this section, there is an introduction to the materials and methods utilized in the present work. On one hand, the prototype Wankel regime was mounted on a customized test bench, which serves as the basis for the subsequent numerical simulation and model validation. On the other hand, a three-dimensional CFD calculation model was implemented to acquire intuitively the curial combustion and flow phenomena during

the Wankel engine running and secure the gained knowledge into general statements for results analysis.

### 2.1. Tested engine specifications

In the course of the present work, a single-rotor spark-ignition Wankel engine with ball-bearing was used to acquire the experimental information for the verification of the simulative CFD model and chemical kinetics mechanism. The schematic of the tested Wankel rotary engine, as depicted in Fig. 1, for an instantaneous moment as the combustion chamber (Chamber II) is at the ignition timing (335°EA). The type of cooling is air-cooled, and the prototype has a single spark plug arranged on the leading wall of the rotor chamber inside the Wankel engine. Fig. 2 compares the Wankel operation and the four-stroke reciprocating operation. The major technical specifications of the tested Wankel rotary engine are summarized in Table 1. The mentioned speed of 4200 rpm is that of the eccentric shaft. The electronic engine management system controlled the spark timing as well as the gasoline/hydrogen dual-fuel injection parameters simultaneously. The combustion analyzer system could record variations of the fuel-air ratio fully transient while the Wankel engine was running.

### 2.2. Computational mesh establishment

As shown in Fig. 3, the computer-aided design model of the Wankel operation originates from the prototype employing the CATIA platform. Besides, the numerical CFD model was integrated into the CONVERGE program package. Benefits from the technology of automatically generating orthogonal-structured grids, the meshes are automatically encrypted on account of temperature and velocity fields, among others with the support of the CONVERGE code. The mesh independence has been calibrated and validated in our preliminary study [51], as shown schematically in Fig. 4. To strike a compromise between the prediction reliability and computational expense, the base grid scale of 2 mm with the adaptive mesh refinement was used throughout the computational domain. A minimum grid scale of 0.125 mm is imposed in regions such as spark-plug location, surface of the wall, and intake port and exhaust port. The total number of meshes is almost 90,000 per working chamber on calculations of a realistic engine running. Fig. 5 provides the automatically simulated and built-up grid of the entire CFD model and the local combustion chamber. An overview of the technical route for ongoing investigation is depicted in Fig. 6.

![Fig. 1. Schematic of the tested Wankel rotary engine. The diagram shows a cross-section of the engine with labels for Intake port, Exhaust port, Chamber I, Chamber II, Chamber III, Recess, Rotor, Stator, Spark plug, Leading side, and Trailing side. A green arrow indicates the Direction of rotation.](df9888cdd1e5419ec477e8775e234f33_img.jpg)

Fig. 1. Schematic of the tested Wankel rotary engine. The diagram shows a cross-section of the engine with labels for Intake port, Exhaust port, Chamber I, Chamber II, Chamber III, Recess, Rotor, Stator, Spark plug, Leading side, and Trailing side. A green arrow indicates the Direction of rotation.

Fig. 1. Schematic of the tested Wankel rotary engine.

![Fig. 2. Comparison of the Wankel operation and four-stroke reciprocating operation [50]. The figure consists of two rows of four engine diagrams each. The top row shows the four strokes of a Wankel engine: Intake (0-180°), Compression (180-360°), Expansion (360-540°), and Exhaust (540-720°). The bottom row shows the four strokes of a four-stroke reciprocating engine: Intake (0-270°), Compression (270-540°), Expansion (540-810°), and Exhaust (810-1080°). A pressure graph is overlaid, showing a single peak during the expansion stroke of the Wankel engine.](9ccd03fe518c562a3fe2d3119f50935e_img.jpg)

Fig. 2. Comparison of the Wankel operation and four-stroke reciprocating operation [50]. The figure consists of two rows of four engine diagrams each. The top row shows the four strokes of a Wankel engine: Intake (0-180°), Compression (180-360°), Expansion (360-540°), and Exhaust (540-720°). The bottom row shows the four strokes of a four-stroke reciprocating engine: Intake (0-270°), Compression (270-540°), Expansion (540-810°), and Exhaust (810-1080°). A pressure graph is overlaid, showing a single peak during the expansion stroke of the Wankel engine.

Fig. 2. Comparison of the Wankel operation and four-stroke reciprocating operation [50].

Table 1  
Specification of the tested Wankel rotary engine.

| Parameter         | Value                  |
|-------------------|------------------------|
| Generating radius | 69 mm                  |
| Eccentricity      | 11 mm                  |
| Rotor width       | 40 mm                  |
| Displacement      | 160 cc                 |
| Compression ratio | 8:1                    |
| Power output      | 3.8 kW@4200 rpm        |
| Inlet mode        | Side-ported            |
| Intake timing     | 75°EA ATDC, 61°EA ABDC |
| Outlet mode       | Peripheral-ported      |
| Exhaust timing    | 62°EA BBDC, 70°EA ATDC |

### 2.3. Mathematical model formulation

Benefit from the support of the three-dimensional CFD calculation, this ongoing work conducted modeling to address the flow phenomena calculated by the Navier-Stokes governing expressions, which resolve the conservation of amount (continuity), momentum, and energy in the definition below:

$$\frac{\partial \rho}{\partial t} + \frac{\partial \rho u_i}{\partial x_i} = S \quad (1)$$

$$\frac{\partial \rho u_i}{\partial t} + \frac{\partial \rho u_i u_j}{\partial x_j} = -\frac{\partial P}{\partial x_i} + \frac{\partial \sigma_{ij}}{\partial x_j} + S_i \quad (2)$$

$$\begin{aligned} \frac{\partial \rho e}{\partial t} + \frac{\partial u_i \rho e}{\partial x_i} = & -P \frac{\partial u_i}{\partial x_i} + \sum_j \frac{\partial u_i}{\partial x_j} + \frac{\partial}{\partial x_j} \left( \frac{K}{c_v} \frac{\partial e}{\partial x_j} \right) + \frac{\partial}{\partial x_j} \left[ \left( \sum_m h_{mp} D \right. \right. \\ & \left. \left. - \sum_m e_m \gamma \frac{K}{c_p} \right) \frac{\partial Y_m}{\partial x_j} \right] \end{aligned} \quad (3)$$

To describe the turbulence motion inside the Wankel engine, the Reynolds-Averaged Navier Stokes renormalized group (RNG) k- $\epsilon$  model was utilized, which comprised the other two transport formats. In light of this, the turbulent kinetic energy (TKE) k and the dissipation of the TKE  $\epsilon$  could be calculated by

![Figure 3: Contour of the realistic Wankel engine model. The figure consists of five 3D CAD models of engine components: 'Side plate (front)', 'Stator (housing)', 'Rotary engine' (the main assembly), 'Rotor', and 'Side plate (rear)'. Each model is shown from a perspective view, highlighting the complex internal geometry of the Wankel engine's combustion chambers and rotor paths.](ddfe517a5ad9c77c89a57a5e780b24ca_img.jpg)

Figure 3: Contour of the realistic Wankel engine model. The figure consists of five 3D CAD models of engine components: 'Side plate (front)', 'Stator (housing)', 'Rotary engine' (the main assembly), 'Rotor', and 'Side plate (rear)'. Each model is shown from a perspective view, highlighting the complex internal geometry of the Wankel engine's combustion chambers and rotor paths.

Fig. 3. Contour of the realistic Wankel engine model.

![Figure 4: Mesh independence validation for chamber pressure profiles. The graph plots Pressure (MPa) on the y-axis (0.0 to 1.8) against Eccentric angle (°EA) on the x-axis (300 to 510). The graph shows four curves: 3 mm (solid red), 2 mm (dashed blue), 2 mm with AMR (dashed green), and 1 mm (dotted orange). All curves show a peak pressure around 1.35 MPa at approximately 390°EA, which is labeled as 'Firing TDC'. A legend in the top left corner specifies: Speed: 4500 rpm, MAP: 0.035 MPa, Ignition: 335°EA.](b7251436a2a3c0d1c00c3e935df2a8f5_img.jpg)

Figure 4: Mesh independence validation for chamber pressure profiles. The graph plots Pressure (MPa) on the y-axis (0.0 to 1.8) against Eccentric angle (°EA) on the x-axis (300 to 510). The graph shows four curves: 3 mm (solid red), 2 mm (dashed blue), 2 mm with AMR (dashed green), and 1 mm (dotted orange). All curves show a peak pressure around 1.35 MPa at approximately 390°EA, which is labeled as 'Firing TDC'. A legend in the top left corner specifies: Speed: 4500 rpm, MAP: 0.035 MPa, Ignition: 335°EA.

Fig. 4. Mesh independence validation for chamber pressure profiles.

$$\frac{\partial \rho k}{\partial t} + \frac{\partial \rho u_i k}{\partial x_i} = \tau_{ij} \frac{\partial u_i}{\partial x_j} + \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_k} \frac{\partial k}{\partial x_j} \right) - \rho e + \frac{C_s}{1.5} S_s \quad (4)$$

$$\frac{\partial \rho e}{\partial t} + \frac{\partial (\rho u_i e)}{\partial x_i} = \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_e} \frac{\partial e}{\partial x_j} \right) + C_{e1} \rho e \frac{\partial u_i}{\partial x_i} + \left( C_{e1} \frac{\partial u_i}{\partial x_j} \tau_{ij} - C_{e2} \rho e + C_{e3} S_s \right) \frac{\epsilon}{k} + S - \rho R_e \quad (5)$$

With regard to the RNG k- $\epsilon$  turbulence equation, the Reynolds stress could be expressed by

$$\tau_{ij} = -\rho \bar{u}_i \bar{u}_j + 2\mu_t S_{ij} - \frac{2}{3} \delta_{ij} \left( \rho k + \mu_t \frac{\partial \bar{u}_i}{\partial x_i} \right) \quad (6)$$

In close cooperation with the CONVERGE platform, the SAGE detail chemistry solver coupled with the multi-zone model [52] addressed the reactant transition formula in the duration of the combustion in detail. The mentioned SAGE approach was according to Senecal et al. research accompanied by a predictive combustion model [53]. The SAGE approach takes advantage of a collection of CHEMKIN-formatted program packages to solve detailed reaction mechanisms. The multi-zone

![Figure 5(a): Entire CFD model. This is a 3D mesh of the entire Wankel engine. Labels point to the 'Exhaust port', 'Intake port', 'Rotor', 'Cylinder', and 'Spark plug'. An inset shows a magnified view of the combustion chamber area.](4676c063222d5d8f1cd1204331748b72_img.jpg)

Figure 5(a): Entire CFD model. This is a 3D mesh of the entire Wankel engine. Labels point to the 'Exhaust port', 'Intake port', 'Rotor', 'Cylinder', and 'Spark plug'. An inset shows a magnified view of the combustion chamber area.

(a) Entire CFD model

![Figure 5(b): Local combustion chamber. This is a detailed 3D mesh of the combustion chamber area. Labels point to the 'Spark plug', 'Stator', 'Recess', and 'Rotor'.](c97b176986d994192dd844e17cd08e3a_img.jpg)

Figure 5(b): Local combustion chamber. This is a detailed 3D mesh of the combustion chamber area. Labels point to the 'Spark plug', 'Stator', 'Recess', and 'Rotor'.

(b) Local combustion chamber

Fig. 5. Computational grid of the simulative Wankel engine model.

model is integrated into the simulation environment to accelerate the solution of chemical reaction kinetics after the start of the combustion forward. The function of multi-zone, at every discrete time, each mesh in CONVERGE is at some thermodynamic state. As for the thermodynamic state of the meshes, the meshes are grouped in zones [54]. Additionally, the set of elementary equations constituting the chemical kinetics is depicted as follows:

$$\sum_{m=1}^{M} v'_{m,r} \chi_m \Leftrightarrow \sum_{m=1}^{M} v'_{m,r} \chi_m, r = 1, 2, \dots, R \quad (7)$$

The net production rate of every component can be expressed by

![Flowchart of the technical route for ongoing investigation. The process starts with 'Parametric modeling' (Define rotor, housing, intake, exhaust port with Matlab & export discrete points; Create a 3-D geometric model by CATIA). This leads to 'Pre-treatment' (Import CAD file to CONVERGE Studio; Fix surface errors & allocate boundary; Seal moving boundary & define rotor motion; Define simulation parameters & physical models). Next is 'Solve' (Export CFD model & run CONVERGE Solve). Finally, 'Post-processing' (Draw line & contour diagram). Icons represent each stage: a gear for parametric modeling, a document for pre-treatment, a blue circle with waves for solve, and a bar chart for post-processing.](e394c2b5c61344f6a12397f430086072_img.jpg)

Flowchart of the technical route for ongoing investigation. The process starts with 'Parametric modeling' (Define rotor, housing, intake, exhaust port with Matlab & export discrete points; Create a 3-D geometric model by CATIA). This leads to 'Pre-treatment' (Import CAD file to CONVERGE Studio; Fix surface errors & allocate boundary; Seal moving boundary & define rotor motion; Define simulation parameters & physical models). Next is 'Solve' (Export CFD model & run CONVERGE Solve). Finally, 'Post-processing' (Draw line & contour diagram). Icons represent each stage: a gear for parametric modeling, a document for pre-treatment, a blue circle with waves for solve, and a bar chart for post-processing.

Fig. 6. Overview of the technical route for ongoing investigation.

$$\dot{\omega} = \sum_{r=1}^{R} v_{m,r} q_r, m = 1, 2, \dots, M \quad (8)$$

$$v_{m,r} = v'_{m,r} - v'_r \quad (9)$$

The calculation of the rate of progress data for every individual reaction equation is given in the following Eq. 10. Moreover, the coefficients of forward and reverse rates for every kinetic equation were through the Arrhenius formula by Eq. 11 as follows:

$$q_r = k_f \prod_{m=1}^{M} [X_m]^{v_{m,r}} - k_r \prod_{m=1}^{M} [X_m]^{v_{m,r}} \quad (10)$$

$$k_{i,f} = A_i T^{b_i} \exp\left(\frac{-E_i}{RT}\right) \quad (11)$$

For the conducted simulation, the Han et al. model [55] and spark-energy deposition model [56] were used to model the wall heat transfer and map the ignition, respectively. The classical Extended Zel'dovich emission model was employed for simulating the formation of nitrogen oxide ( $\text{NO}_x$ ) emission [57]. In addition, a detailed reaction kinetic mechanism for primary reference fuel (PRF) blends was based on significant work [58] that consisted of 41 species, and 124 reactions were selected as the representative of gasoline for this CFD simulation. PRF92 was chosen as the surrogate for #92 gasoline corresponding to the fuel usage for the experimental test bench, which comprises 92 % (vol) isooctane and 8 % (vol) *n*-heptane. The computational models and chemical reaction kinetics adopted in the current work are given in Table 2.

### 2.4. Boundary & initial condition

In the case of this investigation, the boundary condition and initial condition settings for the implemented CFD model, as listed in Table 3. The simplifications for the present work were assumed as follows: Firstly, the standard ‘perfect mixing’ scavenging model was implemented for intake and exhaust charge, and the air-hydrogen-gasoline vapor mixture was considered to be homogeneous inside the engine.

Table 2

Summary of computational models and reaction kinetics.

| Description             | Models and mechanism          |
|-------------------------|-------------------------------|
| Turbulence              | RNG $k-\epsilon$ model        |
| Wall heat transfer      | Han and Reitz model           |
| Ignition                | Spark-energy deposition model |
| Combustion              | SAGE & multi-zone mechanism   |
| $\text{NO}_x$ formation | Extended Zel'dovich mechanism |
| Reaction kinetics       | PRF skeletal mechanism        |

Table 3

Summary of boundary and initial conditions.

| Region          | Type        | Temperature | Pressure  |
|-----------------|-------------|-------------|-----------|
| Air intake      | Inflow      | 293 K       | 0.035 MPa |
| Inlet port      | Fixed wall  | 293 K       | NA        |
| Exhaust outlet  | Outflow     | 700 K       | 0.1 MPa   |
| Outlet port     | Fixed wall  | 293 K       | NA        |
| Hydrogen port   | Fixed wall  | 293 K       | NA        |
| Rotor           | Moving wall | 550 K       | NA        |
| Housing         | Fixed wall  | 550 K       | NA        |
| Spark plug      | Fixed wall  | 750 K       | NA        |
| Spark electrode | Fixed wall  | 850 K       | NA        |

Secondly, the gasoline spray atomizes and evaporates completely before the initiation of the combustion. Finally, the mass of residual exhaust gas produced by the duration of the previous working cycle was not taken into account [59].

To guarantee the global equivalence ratio ( $\Phi$ ) and hydrogen-doping ratio ( $\alpha_{\text{H}_2}$ ) remain the same in this study, the  $\Phi$  and  $\alpha_{\text{H}_2}$  used here are inspired in the following manner [60]:

$$\Phi = \frac{1}{\lambda} = \frac{V_{\text{H}_2} \rho_{\text{H}_2} A_{\text{F,St,H}_2} + m_{\text{PRF}} A_{\text{F,St,PRF}}}{V_{\text{air}} \rho_{\text{air}}} \quad (12)$$

$$\alpha_{\text{H}_2} = \frac{V_{\text{H}_2}}{V_{\text{air}} + V_{\text{H}_2}} \times 100\% \quad (13)$$

where  $\lambda$  serves as the excess air coefficient in experiments.  $V_{\text{H}_2}$  and  $\rho_{\text{H}_2}$  are the volumetric flow rate and density of hydrogen (1 atm@300 K), respectively. The terms  $V_{\text{air}}$  and  $\rho_{\text{air}}$  represent the volumetric flow rate and density of air (1 atm@300 K).  $A_{\text{F,St,H}_2}$  and  $A_{\text{F,St,PRF}}$  severally denote the stoichiometric air/fuel ratio of hydrogen and PRF.  $m_{\text{PRF}}$  is the mass flow rate of PRF.

## 3. Model validation

### 3.1. Validation of turbulence model

To accurately describe the airflow process of the Wankel engine, it is imperative to explicit turbulence patterns inside the engine to ensure that the validated turbulence model can satisfy the criteria for the CFD simulation [61]. According to the previous experimental work by Fan et al. [62], a particle image velocimetry (PIV) test has been done on the flow field coherent information concerning the Wankel design philosophies. It should be highlighted that the prototype of the Wankel engine used for the PIV measurement is consistent with the current research. Fig. 7 contrasts the PIV-measured geometry model and the currently tested geometry model. The remaining majority of the PIV measurement information has been demonstrated in their published work by Ref. [7,63]. It is noticeable from Fig. 8 that he simulated flow field shows agreement with PIV experiment data. Although some slight discrepancies are presented because of the simplification of the intake port, the numerical models can capture the important features of the flow field, which indicates the RNG  $k-\epsilon$  model as the turbulence model used for this ongoing research is acceptable.

![Figure 7: Comparison of the PIV-measured Wankel engine (a) and this ongoing Wankel engine (b).](8e592c58b5074d79831ff650c2c636df_img.jpg)

Figure 7 consists of two parts. Part (a) shows two 3D cutaway diagrams of a Wankel engine. The left diagram is labeled 'PIV-measured Wankel engine' and includes labels for 'Exhaust port', 'Intake port', 'Side plate (rear)', 'Spark plug', 'Stator', and 'Side plate (front)'. The right diagram is labeled 'this ongoing Wankel engine'. Both diagrams show the internal geometry of the engine, including the rotor and combustion chamber. Part (b) shows a 3D cutaway diagram of a different Wankel engine, colored with a red-to-white gradient, likely representing a flow field or pressure distribution.

Figure 7: Comparison of the PIV-measured Wankel engine (a) and this ongoing Wankel engine (b).

Fig. 7. Comparison of the PIV-measured Wankel engine (a) and this ongoing Wankel engine (b).

![Figure 8: Validation of turbulence model at varying EA positions. The figure shows two sets of plots for 350 °EA bTDC and 300 °EA bTDC. Each set includes a color bar for PIV experimental data (m/s) and simulated data (m/s), followed by a 2D vector field plot showing flow direction and magnitude.](ac99eff233b8fe51d30f499e7413c345_img.jpg)

Figure 8 displays the validation of the turbulence model at two different engine positions: 350 °EA bTDC and 300 °EA bTDC. For each position, there are two color bars: 'PIV experimental data (m/s)' and 'Simulated data (m/s)'. The experimental data color bar ranges from 0 to 6 m/s, while the simulated data color bar ranges from 0 to 15 m/s. Below these color bars are 2D vector field plots showing the flow velocity vectors. The vectors are color-coded according to the simulated data, with colors ranging from blue (low velocity) to red (high velocity). The plots show complex flow patterns within the engine combustion chamber.

Figure 8: Validation of turbulence model at varying EA positions. The figure shows two sets of plots for 350 °EA bTDC and 300 °EA bTDC. Each set includes a color bar for PIV experimental data (m/s) and simulated data (m/s), followed by a 2D vector field plot showing flow direction and magnitude.

Fig. 8. Validation of turbulence model at varying EA positions.

### 3.2. Validation of combustion model

The high precision and robustness of the used SAGE detail chemistry solver coupled with the multi-zone model also need to be validated against the experimental results under different engine operating conditions. Fig. 9 depicts the physical image and sketch diagram of the operated Wankel engine system. The uncertainties analysis was taken into account for experimental data. In order to ensure the correctness of all measured values and calculation results in the experiment, the average of three measured results of each testing point was used as the acceptable data. In addition, all test equipment used in the experiment were calibrated before the test. The physical error of the indirect-measured object is calculated by:

$$\Delta u = \sqrt{\sum_{i=1}^{k} \left( \frac{\partial y}{\partial x_i} \bigg|_{x_i=\bar{x}_i} \right)^2 (\Delta x_i)^2} \quad (14)$$

where,  $x_i$  is the measured value of the  $i_{th}$  direct-measured object in the test;  $\bar{x}_i$  is the average value of  $k$  testing points of the  $i_{th}$  direct-measured object in the test;  $\Delta x_i$  is the error value of the  $i_{th}$  direct-measured object in the test. The measurement uncertainties have been listed in Table 4. The remaining majority of the measurement information on test-bench

experiments can be obtained in our previous study [28,60].

As illustrated in Fig. 10, the chamber pressure curve and instantaneous heat release ratio (HRR) evolutions by simulations almost overlapped with the experimental data under various engine operations, indicating the high precision and robustness of the current CFD simulations for the prediction of the spark-ignition event and combustion behavior. It should be highlighted that to ensure the robustness and reasonableness of the subsequent ongoing work, the implemented mathematical models are rigorously kept constant for all calculation schemes.

## 4. Results and discussion

In this section, variations of the turbulence movement, flame propagation, combustion behavior, and pollutant generation under varying recess dimensions are first evaluated step-by-step to reveal the impact of chamber volume. Then, the influencing mechanism of how recess position arrangement on combustion and flow phenomena of Wankel engines is presented.

![Figure 9: Experimental setup for the operated Wankel engine system. (a) Engine physical image showing the engine mounted on a dynamometer, with intake and exhaust ports labeled. (b) Engine system sketch showing a detailed schematic of the fuel and air systems, including tanks, filters, pumps, injectors, and sensors, with numbered components 1-24.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

(a) Engine physical image

(b) Engine system sketch

1. Gasoline tank. 2. Gasoline filter. 3. Gasoline flowmeter. 4. Gasoline pump.  
5. Air filter. 6. Hydrogen container. 7. Pressure governor. 8. Pressure reducer.  
9. Hydrogen flowmeter. 10. Backfire arrester. 11. Hydrogen injector. 12. Gasoline injector.  
13. Crank angle sensor. 14. HECU. 15. Calibration computer. 16. Pressure sensor.  
17. Rotary engine. 18. Dynamometer. 19. Combustion analyzer. 20. Dynamometer console.  
21. Emissions analyzer. 22. Oxygen sensor. 23. A/F analyzer. 24. Backpressure valve.

Figure 9: Experimental setup for the operated Wankel engine system. (a) Engine physical image showing the engine mounted on a dynamometer, with intake and exhaust ports labeled. (b) Engine system sketch showing a detailed schematic of the fuel and air systems, including tanks, filters, pumps, injectors, and sensors, with numbered components 1-24.

Fig. 9. Experimental setup for the operated Wankel engine system.

**Table 4**  
The uncertainties and resolutions of the measurement instruments.

| Parameter                     | Instrument    | Manufacturer | Uncertainty                                           |
|-------------------------------|---------------|--------------|-------------------------------------------------------|
| Engine speed                  | CAC6          | Power link   | $\le \pm 1$ rpm                                       |
| Torque                        | CAC6          | Power link   | $\le \pm 0.4$ % F.S.                                  |
| Cylinder pressure             | 6117BCD17     | Kistler      | $\le \pm 0.3$ bar                                     |
| Gasoline mass flow rate       | FC2210        | Power link   | $\le 0.8$ % F.S                                       |
| Hydrogen volumetric flow rate | D07-19BM      | Seven star   | $\le \pm 0.02$ L/min                                  |
| Air volumetric flow rate      | 20 N060       | Tociel       | $\le \pm 0.1$ L/min                                   |
| Air-to-fuel ratio             | MEXA-730A     | Horiba       | $\le \pm 0.007$                                       |
| Exhaust emissions             | MEXA-7100DEGR | Horiba       | $\le \pm 1\%$ of the measured value Sensitivity:1 ppm |

### 4.1. Analysis of chamber dimension on combustion behavior

According to the findings of our published technical literature, the advantage of the turbulence-induced blade as a prominent configuration has been demonstrated in improving engine performance under varying operating conditions [51]. As such, based on the original Wankel engine with turbulence-induced blade configuration, various recess volumes of the combustion chamber are proposed and compared by modifying the pocket depth and length in this sub-section. Fig. 11 exhibits the combustion chamber designs with different recess volumes and compression ratios in the current study. Here, the following conditions remained constant for each scheme: 4500 rpm engine speed, 0.35 bar Manifolds absolute pressure (MAP),  $\lambda = 1.1$ , 335°EA ignition timing, and  $\alpha_{H2} = 6$  %.

To quantitatively characterize the turbulence intensity, Fig. 12 gives the evolution of the mean TKE inside the engine as a function of EA

![Figure 10: Validation of combustion model as a function of EA position. Six subplots (a-f) show Pressure (MPa) and HRR (J·s⁻¹) vs. Eccentric angle (°EA) for different H2 mass fractions (αH2) and lambda values. Each plot compares Experiment (red solid line) and Simulation (blue dashed line).](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 10 consists of six subplots arranged in a 2x3 grid, labeled (a) through (f). Each subplot shows two y-axes: Pressure (MPa) on the left (0.0 to 1.5) and HRR (J·s⁻¹) on the right (0.0 to 6.3). The x-axis for all plots is the Eccentric angle (°EA), ranging from 330 to 480. Each plot includes a legend for 'Experiment' (red solid line) and 'Simulation' (blue dashed line). A box in the top right of each plot provides operational parameters: Speed: 4500 rpm, MAP: 0.035 MPa, Ignition: 335°EA. Arrows indicate the direction of the combustion process across the angle range.

- (a)  $\alpha_{H_2} = 0\%$ ,  $\lambda = 1.0$
- (b)  $\alpha_{H_2} = 3\%$ ,  $\lambda = 1.0$
- (c)  $\alpha_{H_2} = 6\%$ ,  $\lambda = 1.0$
- (d)  $\alpha_{H_2} = 0\%$ ,  $\lambda = 1.3$
- (e)  $\alpha_{H_2} = 3\%$ ,  $\lambda = 1.3$
- (f)  $\alpha_{H_2} = 6\%$ ,  $\lambda = 1.3$

Figure 10: Validation of combustion model as a function of EA position. Six subplots (a-f) show Pressure (MPa) and HRR (J·s⁻¹) vs. Eccentric angle (°EA) for different H2 mass fractions (αH2) and lambda values. Each plot compares Experiment (red solid line) and Simulation (blue dashed line).

Fig. 10. Validation of combustion model as a function of EA position.

![Figure 11: Schematic of various recess volume modifications. Three rows show different recess sizes: Large (CR=8.0), Medium (CR=8.8), and Small (CR=9.6). Each row includes a cross-sectional diagram of the combustion chamber and a corresponding simulation image showing the flame kernel location.](e0ebcd8fdcfd34b12de3601b59505fdd_img.jpg)

Figure 11 shows three rows of combustion chamber schematics. Each row represents a different recess volume modification: Large (CR=8.0), Medium (CR=8.8), and Small (CR=9.6). The left column shows cross-sectional diagrams of the combustion chamber with a recess, indicating the rotor rotating direction (clockwise) and the dimensions of the recess: height and width. The right column shows simulation images of the flame kernel location at ignition. A legend indicates the rotor rotating direction with an arrow pointing left.

Figure 11: Schematic of various recess volume modifications. Three rows show different recess sizes: Large (CR=8.0), Medium (CR=8.8), and Small (CR=9.6). Each row includes a cross-sectional diagram of the combustion chamber and a corresponding simulation image showing the flame kernel location.

Fig. 11. Schematic of various recess volume modifications.

position. It is noteworthy to highlight that the mean TKE within the combustion chamber reduces with the proceeding of the compression stroke. This is mainly due to the unique structure of the combustion chamber and the kinematics of the rotor, and a strong one-way flow from the trailing to the leading side is created evenly in the rotor chamber. Then, the mean TKE traces of all three schemes appear to perform an inflection point after 325°EA and prone to be a slight upward tendency during the later period of the compression stroke. The phenomenon can be derived from an elongated chamber geometry near the minor axis of the engine, thus the strong one-way flow can be squished in this area and the local turbulence is strengthened distinctly. At the ignition moment, the average TKE for the small recess volume scheme is distinctly higher than that of medium and large schemes as already shown in Fig. 12, indicating a stronger turbulence intensity around the spark-ignition position and thus the faster flame propagation accordingly. Apparent is the fact that with decreasing recess volume, the iso-

![Figure 12: Evolution of the mean TKE as a function of EA position. The plot shows Turbulent kinetic energy (m²·s⁻²) vs. Eccentric angle (°EA) for Large, Medium, and Small recess volumes. A vertical dashed line marks the Ignition timing.](aa14b9ec884bf40ce06c161be468cd84_img.jpg)

Figure 12 is a line graph showing the evolution of mean TKE (m²·s⁻²) as a function of Eccentric angle (°EA) from 280 to 350. Three data series are plotted: Large (red solid line), Medium (blue dashed line), and Small (green dashed line). All three series show a general downward trend in TKE as the eccentric angle increases, reaching a minimum around 325°EA. At this point, the TKE for the Small scheme is significantly higher than for the Large and Medium schemes. A vertical dashed line at approximately 335°EA is labeled 'Ignition timing'.

Figure 12: Evolution of the mean TKE as a function of EA position. The plot shows Turbulent kinetic energy (m²·s⁻²) vs. Eccentric angle (°EA) for Large, Medium, and Small recess volumes. A vertical dashed line marks the Ignition timing.

Fig. 12. Evolution of the mean TKE as a function of EA position.

volume of the fuel combustion reduces somewhat during the later period of the compression stroke. The more intense combustible mixture and the stronger the turbulence level shift earlier, resulting in a rapid heat release process.

Fig. 13 describes the chamber iso-thermal contour of 2000 K and streamlines at 350°EA position for various recess volumes. The flame for all schemes is wrinkled, this phenomenon can be explained by the turbulence intensity and the unfavorable shape of the combustion chamber [61,64]. Benefiting from the intense one-way flow from the trailing side to the leading edge, the flame spreads primarily in the leading part of the

![Figure 13: Contour of flame spread and streamlines at 350°EA position. The figure consists of three vertically stacked panels showing the rotor chamber at different compression ratios (CR): Large CR=8.0, Medium CR=8.8, and Small CR=9.6. Each panel shows streamlines (black arrows) and a flame kernel (red area). A legend at the top indicates the rotor rotating direction with an arrow pointing left. The flame kernel is more confined and has higher turbulence intensity in the small CR scheme.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 13: Contour of flame spread and streamlines at 350°EA position. The figure consists of three vertically stacked panels showing the rotor chamber at different compression ratios (CR): Large CR=8.0, Medium CR=8.8, and Small CR=9.6. Each panel shows streamlines (black arrows) and a flame kernel (red area). A legend at the top indicates the rotor rotating direction with an arrow pointing left. The flame kernel is more confined and has higher turbulence intensity in the small CR scheme.

Fig. 13. Contour of flame spread and streamlines at 350°EA position.

rotor chamber and the penetration in the opposite direction is hardly extended because of the intensive unidirectional flow. By comparing the flame area of different recess modifications, it should be highlighted that faster growth of the initial kernel is found at the small volume scheme, which is attributed to the relatively higher turbulence level as already analyzed in Fig. 12. This confirms that the turbulence intensity has a favorable effect on the growth of the initial flame. Additionally, with the decrease in the pocket volume, the streamlines around the spark-ignition location become scarce and separate into the sides of the rotor width direction, as shown schematically in Fig. 13. This is because the recess depth inside the engine becomes shallower with the decrease in the pocket volume, the leading part has less space for flow motion, which confines the extension of the flame area around the spark-ignition position. Meanwhile, this phenomenon is partly responsible for the high unburnt HC formation of the engine.

Fig. 14 depicts the pressure traces for different recess schemes in the working housing as a function of the EA position. The peak chamber explosion pressure increases and its corresponding EA position shifts to

earlier as the pocket volume is modified to smaller. Specifically, the peak chamber pressure exceeds 1.41 MPa and its corresponding EA position is 393.96°EA at a large volume scheme. As calculated, differences in the peak pressure for medium and small schemes are greater by 0.13 MPa and 0.39 MPa than that for the large scheme. Their corresponding EA positions are earlier by 1.96°EA and 4.97°EA than that for the large scheme, respectively. The responsible for the combustion behavior originates from the turbulence intensity in the rotor chamber around the ignition TDC. Decreasing the pocket volume is beneficial to enhance the chamber pressure along with combustion temperature (Fig. 15) before the ignition moment and improve reactivity activation and thermal atmosphere, it is prone to shift forward at the onset of the combustion process and the combustion stability can be guaranteed accordingly. On the negative side, however, the significant increment in the peak chamber pressure owing to the smaller recess volume caused an additional mechanical load on Wankel engines, resulting in worse operating stability and life span. As depicted in Fig. 15, the peak combustion temperature for the small scheme is lower than other schemes, while the medium scheme is the highest. A probable cause lies in the improved ignition ambient of the mixture and the shortened ignition delay after reducing the pocket volume. This indicates a larger thermal load and higher cooling loss of the engine, and therefore the in-cylinder temperature decreases.

Fig. 16 gives the discrepancy of indicated mean effective pressure (IMEP) and EA50 position for varying recess modification. It should be explained here that EA50 represents a corresponding EA position whose percentage of heat release amount is at 50 % of the total heat release amount, which is commonly referred to main combustion phase. As expected, there is a great correlation between the EA50 and IMEP of the engine. When the pocket volume of the rotor chamber reduces, the EA50 position shifts closer to the ignition TDC, thus increasing the iso-volumetric degree of the combustion, which contributes to presenting a higher IMEP of this investigated Wankel rotary engine. It can also be known from Fig. 16 that the difference in the EA50 position for the large scheme and the medium scheme is minimal, which originates from the turbulence intensity and flame development, as already revealed above.

To evaluate the effect of pocket modification on the emission characteristics of Wankel rotary engines, the formations of  $\text{NO}_x$ , unburnt HC, and CO mass fractions within the rotor chamber at the exhaust moment as depicted in Fig. 17. As the investigations determined, it is observed that as the pocket volume reduced, the increment in unburnt HC mass fraction becomes larger than the decrease in CO mass fraction, while the increase in  $\text{NO}_x$  formation is slight. The reason for this emission characteristic results from the increased surface-volume ratio and lower

![Figure 14: Evolution of the chamber pressure as a function of EA position. The graph plots Pressure (MPa) on the y-axis (0.0 to 2.1) against Eccentric angle (°EA) on the x-axis (300 to 510). Three curves are shown: Large (solid red), Medium (dashed blue), and Small (dotted green). All curves show a peak pressure around 390-400°EA. A vertical dashed line at 330°EA is labeled 'Ignition timing'.](9d8d3d909d7fdccb631c519df2b86e61_img.jpg)

Figure 14: Evolution of the chamber pressure as a function of EA position. The graph plots Pressure (MPa) on the y-axis (0.0 to 2.1) against Eccentric angle (°EA) on the x-axis (300 to 510). Three curves are shown: Large (solid red), Medium (dashed blue), and Small (dotted green). All curves show a peak pressure around 390-400°EA. A vertical dashed line at 330°EA is labeled 'Ignition timing'.

Fig. 14. Evolution of the chamber pressure as a function of EA position.

![Figure 15: Evolution of the chamber temperature as a function of EA position. The graph plots Temperature (K) on the y-axis (400 to 2400) against Eccentric angle (°EA) on the x-axis (300 to 510). Three curves are shown: Large (solid red), Medium (dashed blue), and Small (dotted green). All curves show a peak temperature around 420°EA. A vertical dashed line at 330°EA is labeled 'Ignition timing'.](ae21ece48844b14b230832cbb6fcf735_img.jpg)

Figure 15: Evolution of the chamber temperature as a function of EA position. The graph plots Temperature (K) on the y-axis (400 to 2400) against Eccentric angle (°EA) on the x-axis (300 to 510). Three curves are shown: Large (solid red), Medium (dashed blue), and Small (dotted green). All curves show a peak temperature around 420°EA. A vertical dashed line at 330°EA is labeled 'Ignition timing'.

Fig. 15. Evolution of the chamber temperature as a function of EA position.

![Figure 16: Comparison of IMEP and EA50 position. A dual-axis bar chart showing Indicated mean effective pressure (MPa) on the left y-axis and EA50 (EA) on the right y-axis for three recess modifications: Large, Medium, and Small. The bars are red for IMEP and blue for EA50.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

| Recess modification | IMEP (MPa) | EA50 (EA) |
|---------------------|------------|-----------|
| Large               | 0.35533    | 390.919   |
| Medium              | 0.3646     | 390.412   |
| Small               | 0.36831    | 384.521   |

Figure 16: Comparison of IMEP and EA50 position. A dual-axis bar chart showing Indicated mean effective pressure (MPa) on the left y-axis and EA50 (EA) on the right y-axis for three recess modifications: Large, Medium, and Small. The bars are red for IMEP and blue for EA50.

Fig. 16. Comparison of IMEP and EA50 position.

![Figure 17: Comparison of pollutant formation at exhaust moment. A line graph showing Mass fraction (%) for NOx, HC, and CO across three recess modifications: Large, Medium, and Small.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

| Recess modification | NOx (%) | HC (%) | CO (%) |
|---------------------|---------|--------|--------|
| Large               | ~0.22   | ~0.20  | ~0.11  |
| Medium              | ~0.22   | ~0.21  | ~0.10  |
| Small               | ~0.23   | ~0.26  | ~0.09  |

Figure 17: Comparison of pollutant formation at exhaust moment. A line graph showing Mass fraction (%) for NOx, HC, and CO across three recess modifications: Large, Medium, and Small.

Fig. 17. Comparison of pollutant formation at exhaust moment.

charge temperature at a small scheme, reducing residual gas fraction and lower exhaust temperature, ultimately increasing HC formation. Moreover, a higher combustion temperature has a decisive influence in improving reactant consumption, and thereafter promoting further oxidation of CO to carbon dioxide ( $\text{CO}_2$ ), hence the amount of CO presents relatively lower in the small scheme.

### 4.2. Analysis of recess location on combustion behavior

To further understand the influence of recess location arrangement on the mixture formation, combustion behavior, and pollutant emissions of hydrogen-doping Wankel engines, four different pocket geometries within the rotor chamber are considered in this section, as described schematically in Fig. 18. Due to Wankel engines are characterized by an elongated shape of the combustion chamber, the pocket should be avoided as much as possible in the recess designs, hence the modification and optimization of the rotor width are not taken into consideration in this study. To ensure the compression ratio for all these schemes is fixed at 8.8, the medium pocket design is realized by reducing the recess depth or shortening the recess length when the pocket width of the original engine remains constant. Based on the location and geometry of the recess, the investigated four different schemes in Fig. 18 are severally called shallow pocket, leading pocket, middle pocket, and trailing pocket for the sake of brevity. In addition, it should be stated here that the operating conditions and parameter settings of the Wankel engine are consistent with those of this engine concept in the previous section.

The in-cylinder flow field is an intense transient process during the compression stroke of the engine, which not only affects the airflow movement, mixture generation, and concentration inside the engine but also influences the subsequent flame spread, combustion progress, thermal efficiency, heat transfer loss, and emissions performance, especially for the port fuel injection spark-ignition engine. Fig. 19 plots the velocity magnitude and direction with different pocket arrangements at  $200^\circ\text{EA}$ ,  $300^\circ\text{EA}$ , and ignition timing of  $335^\circ\text{EA}$ . In the initial period of the compression process ( $200^\circ\text{EA}$ ), the extrusion effect is generated due to the smaller working chamber. The intake charge no longer offers the energy supplement for the vortex and tumble formed in the intake stroke, which contributes to weakening the turbulence in the combustion chamber continuously. By comparing the investigated four schemes, the anticlockwise vortex for the leading scheme is the most obvious, followed by the middle and trailing schemes, while the vortex for the shallow scheme has basically dissipated. In the later period of this stroke ( $300^\circ\text{EA}$ ), the surrounding vortex of the rotor surface is further compressed, and the small-scale vortex can still be seen in the leading and middle schemes. For other schemes, the main flow phenomenon inside the engine has been presented to be an intense one-way flow from the trailing to the leading side of Wankel engines. At the ignition moment, the velocity fields around the spark plug under these four schemes are obviously different. Compared with other schemes, due to the recess being at the leading part within the combustion chamber under the leading scheme, the local volume of the combustion chamber is larger, and the airflow velocity is relatively low.

Fig. 20 contrasts the distribution of the average TKE within the rotor chamber at the ignition moment. With the alteration to the pocket location arrangement, the variation trend in the gradient and distribution of the average TKE is distinct. The average TKE of these schemes inside the engine is in the order from small to large: leading < shallow

![Figure 18: Schematic of various pocket location arrangements. Four 3D cross-sectional diagrams of a Wankel engine rotor chamber showing the location of the recess: (a) Shallow, (b) Leading, (c) Middle, and (d) Trailing.](80ce3e357acc809fec0f2b0d6f20f362_img.jpg)

Figure 18: Schematic of various pocket location arrangements. Four 3D cross-sectional diagrams of a Wankel engine rotor chamber showing the location of the recess: (a) Shallow, (b) Leading, (c) Middle, and (d) Trailing.

Fig. 18. Schematic of various pocket location arrangements.



![Figure 19: A 3x4 grid of velocity magnitude and direction contours for a Wankel rotor at 200°EA, 300°EA, and 335°EA. The columns represent Shallow, Leading, Middle, and Trailing schemes. A color bar at the top right indicates Velocity / m·s⁻¹ from 0 to 50. A black arrow at the top left points left, labeled 'Rotor rotating direction'. The contours show the flame front and velocity vectors, with colors representing magnitude and arrows showing direction.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 19: A 3x4 grid of velocity magnitude and direction contours for a Wankel rotor at 200°EA, 300°EA, and 335°EA. The columns represent Shallow, Leading, Middle, and Trailing schemes. A color bar at the top right indicates Velocity / m·s⁻¹ from 0 to 50. A black arrow at the top left points left, labeled 'Rotor rotating direction'. The contours show the flame front and velocity vectors, with colors representing magnitude and arrows showing direction.

Fig. 19. Contour of the velocity magnitude and direction at different EA positions.

![Figure 20: A 4x1 grid of average TKE contours at ignition moment for Shallow, Leading, Middle, and Trailing schemes. A color bar at the top right indicates TKE / m²·s⁻² from 0 to 20. Each plot shows the rotor shape and a color-coded flame front. The TKE values are: Shallow (7.25 m²·s⁻²), Leading (6.58 m²·s⁻²), Middle (7.99 m²·s⁻²), and Trailing (7.42 m²·s⁻²).](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

Figure 20: A 4x1 grid of average TKE contours at ignition moment for Shallow, Leading, Middle, and Trailing schemes. A color bar at the top right indicates TKE / m²·s⁻² from 0 to 20. Each plot shows the rotor shape and a color-coded flame front. The TKE values are: Shallow (7.25 m²·s⁻²), Leading (6.58 m²·s⁻²), Middle (7.99 m²·s⁻²), and Trailing (7.42 m²·s⁻²).

Fig. 20. Contour of the average TKE at ignition moment.

< trailing < middle. In the vicinity of the spark-ignition location, the local TKE for the shallow, middle, and trailing schemes is obviously higher than that for the leading scheme due to the influences of turbulence intensity and pocket location, which is more favorable to the fast development of the flame.

Fig. 21 shows the temperature distribution profile concerning the presented CFD modeling of the initial flame and combustion process immediately after the ignition timing inside the operated Wankel rotary engine. In the initial combustion stage (355°EA), the growth of the combustion initiation for the leading scheme is slower than that for other schemes because of the local flow field within the rotor chamber. As the EA position continues, the initial flame transforms from a quasi-laminar flame to a turbulent flame, which is basically obedient to the variation of small-scale weak turbulent combustion. Meanwhile, the velocity of the flame spread is greatly impacted by the diffusion coefficient of turbulence and the diffusion coefficient of molecular. At 375°EA, the flame speed increases gradually, and the location of the turbulent flame front has no significant difference from other schemes. Apparent is the fact that the recess is arranged at the leading part of the combustion chamber, which extends the available space for flame propagation and increases the actual internal area of the flow field. Besides, a more combustible mixture escapes from the trailing to the leading part inside the engine. The flame front combusts the mixture in the leading part and continuously releases heat. The formed high-temperature–pressure burned gas will effectively compress the unburnt mixture and squeeze it into the wall of the rotor chamber. Along with the impact of a large surface-to-volume ratio and crescent-shaped design of the rotor chamber, a more unburned mixture collides with the wall and hence exhibits an intensive return flow, which further strengthens the turbulence movement inside the engine. Thereafter, a new large-scale vortex is formed and then broken into a small-scale vortex, which in turn imposes on the flame surface to perform a series of island-burning or block-burning regions [65]. As a result, the flame area is increasingly extended, elevating the flame speed, thus forming a cycle of accelerating flame propagation accordingly. Additionally, it is observed from Fig. 21 that the turbulent flame front for middle and trailing schemes is protracted and retarded in the direction of rotation of the rotor. The flame surface spreads more toward the direction of both sides of the rotor width, especially for the trailing scheme. On the one hand, the space for

![Figure 21: A 3x4 grid of contour plots showing chamber temperature distribution. The rows represent Eccentric Angle (EA) positions: 355°EA, 365°EA, and 375°EA. The columns represent rotor positions: Shallow, Leading, Middle, and Trailing. A color bar at the top right indicates Temperature × 10² / K, ranging from 5 (blue) to 25 (red). An arrow at the top left points left, labeled 'Rotor rotating direction'. The plots show a flame front with high temperature (red) moving from the trailing edge towards the leading edge as EA increases.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 21: A 3x4 grid of contour plots showing chamber temperature distribution. The rows represent Eccentric Angle (EA) positions: 355°EA, 365°EA, and 375°EA. The columns represent rotor positions: Shallow, Leading, Middle, and Trailing. A color bar at the top right indicates Temperature × 10² / K, ranging from 5 (blue) to 25 (red). An arrow at the top left points left, labeled 'Rotor rotating direction'. The plots show a flame front with high temperature (red) moving from the trailing edge towards the leading edge as EA increases.

Fig. 21. Contour of chamber temperature distribution at different EA positions.

the leading side within the combustion chamber is confined in the cause of the middle and trailing schemes, and although the turbulence level is high, the mixture mass and oxygen content are relatively low [66]. Because the flame surface can be stretched, wrinkled, and folded by the complex turbulent flow field within the rotor chamber, the majority of the flame front does not reach the leading edge of the rotor chamber of the Wankel rotary engine. On the other side, the unburned mixture is chiefly transported by the unidirectional mainstream flow field. However, due to the small available space for flow motion around the leading part of the middle and trailing pocket chambers, it must be considered that the unburned mixture in the trailing edge can not be replaced immediately on the leading side, which makes it prone to prevent the flame continues to spread.

As the intermediate products, free radicals such as OH, H, and O serve as key indicators of hydrogen-doping combustion chain transfer intensity, and the variation of their concentrations can reflect the combustion progress to a large extent [67]. It can be appreciated from Fig. 22 that the curve slopes of these three free radicals for the leading scheme exhibit the steepest and their peak mass fractions are the highest as well, indicating that the global combustion rate is relatively faster under the scenario. The contrary pattern is witnessed for the trailing scheme. Obviously, the curve slope of these free radicals and the peak mass fraction are the lowest compared with other schemes, which enables the combustion rate to reduce at a slow level. For shallow and middle schemes, the discrepancy in combustion rate is very slight. It should obtain an insight into the root causes of how recess arrangement leads to the evolution of intermediate products and combustion forward. That fact is described even clearer by assessing the increment in the growth of the initial flame for the leading scheme and increasing the contact surface between the unburned mixture and the combustible gas, which promotes the formation of active radicals on the flame front. It also strengthens the heat flux of the unburned mixture, reducing the

![Figure 22: Three vertically stacked line plots showing the evolution of intermediate products (OH, H, O) as a function of Eccentric Angle (EA) from 320 to 460 degrees. The left y-axis is Mass fraction (%) for OH and H, and the right y-axis is Mass fraction × 10³ (%) for O. Four schemes are compared: Shallow (red solid), Leading (blue dashed), Middle (green dash-dot), and Trailing (magenta dotted). The Leading scheme shows the highest peak mass fractions for all three radicals, while the Trailing scheme shows the lowest.](dd330f8b8f6c16eae20c3a676b4eb804_img.jpg)

Figure 22: Three vertically stacked line plots showing the evolution of intermediate products (OH, H, O) as a function of Eccentric Angle (EA) from 320 to 460 degrees. The left y-axis is Mass fraction (%) for OH and H, and the right y-axis is Mass fraction × 10³ (%) for O. Four schemes are compared: Shallow (red solid), Leading (blue dashed), Middle (green dash-dot), and Trailing (magenta dotted). The Leading scheme shows the highest peak mass fractions for all three radicals, while the Trailing scheme shows the lowest.

Fig. 22. Evolution of intermediate products as a function of EA position.

activation energy required for the fuel combustion and therefore accelerating the combustion rate of Wankel engines.

Fig. 23 compares the evolution of mean pressure as a function of chamber volume on the whole working process of the Wankel engine under various recess arrangement schemes. It is noticeable that when the pocket is located at the leading part of the rotor chamber, the local area enclosed by the pressure-volume profile is larger partly because of the higher peak chamber pressure during the later period of the

![Fig. 23. Evolution of mean pressure as a function of chamber volume. The graph shows four pressure-volume (P-V) loops for different recess schemes: Shallow (red solid line), Leading (blue dashed line), Middle (green dash-dot line), and Trailing (magenta dotted line). The y-axis is Pressure (MPa) from 0.0 to 1.8, and the x-axis is Volume (cm³) from 0 to 210. The Leading scheme shows the highest peak pressure, followed by Middle, Shallow, and Trailing.](b05a8a3551db31147979064952179990_img.jpg)

Fig. 23. Evolution of mean pressure as a function of chamber volume. The graph shows four pressure-volume (P-V) loops for different recess schemes: Shallow (red solid line), Leading (blue dashed line), Middle (green dash-dot line), and Trailing (magenta dotted line). The y-axis is Pressure (MPa) from 0.0 to 1.8, and the x-axis is Volume (cm³) from 0 to 210. The Leading scheme shows the highest peak pressure, followed by Middle, Shallow, and Trailing.

Fig. 23. Evolution of mean pressure as a function of chamber volume.

compression process and the early period of the expansion stroke. Moreover, the pressure trace does not drop rapidly in the later period of the expansion process, which results in a higher indicated efficiency of the Wankel engine. For quantitative analysis of heat-work conversion efficiency among various recess arrangement schemes, the closed profile in Fig. 24 is resolved by means of integration and indicated thermal efficiency (ITE) and the maximum pressure rising rate (MPRR) can be obtained, as plotted in Fig. 25. As the investigations determined, the MPRR for the leading scheme is the highest while the MPRR for the trailing scheme is the lowest. The MPRR is closely related to the peak combustion pressure. Arranging the recess at the leading part can increase the peak value of active radicals within the rotor chamber, such as OH, H, and O, and enhance the branch-chain reaction, which further facilitates the reaction and formation of other active radicals, thus increasing the combustion rate and promoting the release of chemical energy of the fuel mixture simultaneously. As a result, both the chamber mean pressure and combustion temperature rise quickly, and the corresponding MPRR increases accordingly. Additionally, the investigated Wankel engine also achieves the highest ITE in the course of the leading scheme. This is because the velocity of the fuel reaction is accelerated, and the combustion phase is advanced closer to the ignition TDC, which is beneficial for improving the heat-work conversion efficiency of the Wankel rotary engine. Therefore, the reasonable arrangement of the

![Fig. 25. Comparison of pollutant formation at exhaust moment. The graph shows the mass fraction (%) of NOx (red squares), HC (blue circles), and CO (green triangles) for four schemes: Shallow, Leading, Middle, and Trailing. NOx is highest for Leading and Shallow, HC is highest for Leading, and CO is highest for Trailing.](8791f79b259a7463279c1aeb14c31580_img.jpg)

| Scheme   | NO <sub>x</sub> (%) | HC (%) | CO (%) |
|----------|---------------------|--------|--------|
| Shallow  | ~0.22               | ~0.21  | ~0.10  |
| Leading  | ~0.30               | ~0.21  | ~0.09  |
| Middle   | ~0.22               | ~0.24  | ~0.10  |
| Trailing | ~0.15               | ~0.30  | ~0.13  |

Fig. 25. Comparison of pollutant formation at exhaust moment. The graph shows the mass fraction (%) of NOx (red squares), HC (blue circles), and CO (green triangles) for four schemes: Shallow, Leading, Middle, and Trailing. NOx is highest for Leading and Shallow, HC is highest for Leading, and CO is highest for Trailing.

Fig. 25. Comparison of pollutant formation at exhaust moment.

pocket location helps Wankel rotary engines get better fuel economy and engine performance.

To evaluate the influence of pocket arrangement on the emission formations of the Wankel regime, the mass fractions of NO<sub>x</sub>, unburnt HC, and CO productions inside the rotor chamber at the beginning of the exhaust opening as plotted in Fig. 25. It is imperative to explore the intrinsic mechanism how recess arrangement causes these phenomena. Table 5 describes the spatial distribution of NO<sub>x</sub>, HC, and CO within the combustion chamber at the exhaust moment (568°EA). Compared with the four schemes, it is noticeable that the NO<sub>x</sub> production for the leading scheme presents the highest, covering almost the leading and middle parts of the rotor chamber, meanwhile, the amounts of unburned HC and CO for this scheme remained at a relatively lower level, and only distributed at a small region around the spark-ignition location in the trailing edge of the rotor chamber at exhaust moment. As a major component of NO<sub>x</sub> emission, the generation of nitric oxide (NO) is chiefly influenced by combustion temperature, oxygen concentration, and high-temperature duration [68]. As plotted in Fig. 26, the peak chamber combustion temperature and the maximum value of the high-temperature domain (> 2500 K) for the leading scheme are notably higher than those of the other three schemes, thus presenting the most amount of NO<sub>x</sub> formation. It is noteworthy to highlight the results from the trailing scheme in Fig. 25 that mass fractions of CO and unburned HC for this scheme are higher than those for other schemes. This is mainly due to the unreasonable arrangement of the pocket location, leading to a large amount of unburned mixture in the trailing part of the rotor chamber and the flame propagation is retarded and protracted against the rotating direction of the rotor and accumulates more unburned HC, which is considered as the main source of HC emissions. Nevertheless, a probable cause of CO emission is the combustion chamber temperature is relatively low, and the combustible mixture can not be fully and completely burned, resulting in a decrease in indicated efficiency, which is adverse to the further oxidation of CO.

![Fig. 24. Comparison of MPRR and ITE. The graph shows Maximum pressure rising rate (bar·°EA⁻¹) on the left y-axis (0.0 to 0.5) and Indicated thermal efficiency (%) on the right y-axis (21 to 28) for four schemes: Shallow, Leading, Middle, and Trailing. MPRR is shown as red bars with a cross-hatch pattern, and ITE is shown as a blue line with open square markers.](9d1abc573e35610946ece87a18cbe862_img.jpg)

| Scheme   | MPRR (bar·°EA⁻¹) | ITE (%) |
|----------|------------------|---------|
| Shallow  | ~0.26            | ~26.5   |
| Leading  | ~0.29            | ~27.0   |
| Middle   | ~0.26            | ~26.5   |
| Trailing | ~0.22            | ~24.5   |

Fig. 24. Comparison of MPRR and ITE. The graph shows Maximum pressure rising rate (bar·°EA⁻¹) on the left y-axis (0.0 to 0.5) and Indicated thermal efficiency (%) on the right y-axis (21 to 28) for four schemes: Shallow, Leading, Middle, and Trailing. MPRR is shown as red bars with a cross-hatch pattern, and ITE is shown as a blue line with open square markers.

Fig. 24. Comparison of MPRR and ITE.

# 5. Conclusions

1. It is highly recommended that a smaller recess volume can be modified by reducing the pocket depth and length, hence presenting superior combustion characteristics and indicated efficiency. The turbulence intensity in the small recess chamber is notably higher than that in the larger recess chamber, and the discrepancy shows an increasing trend with the increase in the compression ratio. With the decrement in the recess volume, the peak chamber pressure increases and its corresponding EA position towards early. By modifying the

**Table 5**  
Contours of NO,  $\text{IC}_8\text{H}_8$ , and CO spatial distribution at exhaust moment.

![Contour plot of NO mass fraction for the shallow scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the shallow scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the shallow scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber. Contour plot of NO mass fraction for the leading scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the leading scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the leading scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber. Contour plot of NO mass fraction for the middle scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the middle scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the middle scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber. Contour plot of NO mass fraction for the trailing scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the trailing scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the trailing scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber.](0332672e127cd13bb6d2fc8d1e27bfa2_img.jpg)

| Scheme   | NO | $\text{IC}_8\text{H}_8$ | CO |
|----------|----|-------------------------|----|
| Shallow  |    |                         |    |
| Leading  |    |                         |    |
| Middle   |    |                         |    |
| Trailing |    |                         |    |

Contour plot of NO mass fraction for the shallow scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the shallow scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the shallow scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber. Contour plot of NO mass fraction for the leading scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the leading scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the leading scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber. Contour plot of NO mass fraction for the middle scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the middle scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the middle scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber. Contour plot of NO mass fraction for the trailing scheme. The plot shows a color gradient from blue (0%) to red (0.5%) across the combustion chamber. High NO concentrations are concentrated near the top right corner of the chamber. Contour plot of IC8H8 mass fraction for the trailing scheme. The plot shows a color gradient from blue (0%) to red (4.5%) across the combustion chamber. High IC8H8 concentrations are concentrated near the top right corner of the chamber. Contour plot of CO mass fraction for the trailing scheme. The plot shows a color gradient from blue (0%) to red (1.5%) across the combustion chamber. High CO concentrations are concentrated near the top right corner of the chamber.

recess to a small volume, it is prone to shift forward at the onset of the combustion process.

- In the early period of the compression process, the anticlockwise vortex for the leading scheme is the most obvious, followed by the middle and trailing schemes, while the vortex in the shallow pocket has basically dissipated. At the end of this stroke, a small-scale vortex can still be seen in the leading and middle schemes, while the main flow field has been transformed to be a unidirectional flow from the trailing to the leading side of the rotor chamber. Because the pocket is arranged at the leading part, the local chamber volume is large, thus the flow velocity is relatively low. The average TKE of these

pocket locations at ignition timing is in the order from small to large: leading < shallow < trailing < middle.

- The curve slope of H, O, and OH free radicals for the leading scheme performs the largest, and its peak mass fraction is the highest as well, indicating that the global combustion rate is relatively faster under the scenario. The contrary pattern is witnessed for the trailing scheme. For shallow and middle schemes, the discrepancy in combustion rate is very slight. The investigated Wankel engine achieves the highest ITE and MPRR in the course of the leading scheme, while the MPRR and ITE for the trailing scheme are the lowest.

![Figure 26: Evolution of combustion temperature and high-temperature domain as a function of EA position. The graph plots Temperature (K) on the left y-axis (0 to 2100) and Mass fraction of high-temperature domain (> 2500 K) on the right y-axis (0.0 to 0.8) against Eccentric angle (°EA) on the x-axis (300 to 570). Four schemes are shown: Shallow (red solid line), Leading (blue dashed line), Middle (green solid line), and Trailing (magenta dashed line). The Leading scheme shows the highest peak temperature (~2100 K) and the largest high-temperature domain (~0.8). The Trailing scheme shows the lowest peak temperature (~1500 K) and the smallest high-temperature domain (~0.6).](177e8bc1c595b7fe3461d9919f87e044_img.jpg)

Figure 26: Evolution of combustion temperature and high-temperature domain as a function of EA position. The graph plots Temperature (K) on the left y-axis (0 to 2100) and Mass fraction of high-temperature domain (> 2500 K) on the right y-axis (0.0 to 0.8) against Eccentric angle (°EA) on the x-axis (300 to 570). Four schemes are shown: Shallow (red solid line), Leading (blue dashed line), Middle (green solid line), and Trailing (magenta dashed line). The Leading scheme shows the highest peak temperature (~2100 K) and the largest high-temperature domain (~0.8). The Trailing scheme shows the lowest peak temperature (~1500 K) and the smallest high-temperature domain (~0.6).

**Fig. 26.** Evolution of combustion temperature and high-temperature domain as a function of EA position.

4. The  $\text{NO}_x$  generation for the leading scheme presents the highest, covering almost the leading and middle parts inside the engine, while the mass fractions of unburned HC and CO for this scheme are relatively lower, and only distributed in a small region around the spark plug in the trailing side of the rotor chamber at the exhaust moment. The amount of HC and CO for the trailing scheme is higher and the formation of  $\text{NO}_x$  is the least.
5. Considering that it is easy to increase the compression by reducing the chamber volume of the rotor chamber in engineering applications. It is highly recommended that the ignition, combustion, and pollutant formation can be effectively improved by appropriately reducing the chamber volume and arranging the pocket in the leading part of the rotor chamber of the Wankel engine.

# CRediT authorship contribution statement

**Jianhui Bao:** Investigation, Writing – original draft, Data curation. **Xiaomeng Wang:** Formal analysis, Methodology. **Guohong Tian:** Resources, Supervision. **Fuquan Nie:** Software, Supervision. **Xiaodong Yan:** Validation, Visualization. **Cheng Shi:** Project administration, Conceptualization, Writing – original draft, Funding acquisition.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgments

The authors would like to acknowledge the financial support provided by the Chunhui Project Foundation of the Education Department of China through its Project of HZKY20220239, the Science Research Project of Hebei Education Department through its Project of QN2023224 and Natural Science Foundation of Hebei Province through its Project of E2025203113.

# Data availability

Data will be made available on request.

# References

- [1] Thompson GJ, Wowczuk ZS, Smith JE. Rotary engines - A concept review. SAE Technical Paper 2003-01-3206, 2003.
- [2] Dost T, Getzlaff J. Design and simulation of a multi fuel gas mixture system of a Wankel rotary engine. SAE Technical Paper 2020-01-0548, 2020.
- [3] Bao J, Lei J, Tian G, et al. A review of the application development and key technologies of rotary engines under the background of carbon neutrality. *Energy* 2024;311:133447.
- [4] Kucuk M, Surmen A, Sener R. Combustion characteristics and performance of a Wankel engine for unmanned aerial vehicles at various altitudes. *Fuel* 2024;355:129483.
- [5] Meng H, Ji C, Wang S, et al. A review: centurial progress and development of Wankel rotary engine. *Fuel* 2023;335:127043.
- [6] Jiménez-Espadafor Aguilar FJ, Vélez Godíño JA. Innovative power train configurations for aircraft auxiliary power units focused on reducing carbon footprint. *Aerosp Sci Technol* 2020;106:106109.
- [7] Fan BW, Pan JF, Pan ZH, et al. Effects of pocket shape and ignition slot locations on the combustion processes of a rotary engine fueled with natural gas. *Appl Therm Eng* 2015;89:11–27.
- [8] Tartakovsky L, Baibikov V, Gutman M, et al. Simulation of Wankel engine performance using commercial software for piston engines. SAE Technical Paper 2012-32-0098, 2012.
- [9] Kutlar OA, Malkaz F. Two-stroke Wankel type rotary engine: a new approach for higher power density. *Energies* 2019;12(21):4096.
- [10] Chen W, He W, Ma Y, et al. Numerical investigation of flow and combustion process in a hydrogen direction injection rotary engine. *Fuel* 2025;379:133100.
- [11] Shi C, Duan R, Cheng T, et al. Understanding the role of ammonia combined injection in improving combustion and emissions characteristics for heavy-duty CI engine. *Energy* 2025;324:135959.
- [12] Kucuk M, Sener R, Surmen A. Effectiveness of hydrogen enrichment strategy for Wankel engines in unmanned aerial vehicle applications at various altitudes. *Int J Hydrogen Energy* 2024;52:1534–49.
- [13] Bao J, Wang H, Wang R, et al. Comparative experimental study on macroscopic spray characteristics of various oxygenated diesel fuels. *Energy Sci Eng* 2023;11(5):1579–88.
- [14] Lei J, Niu J, Tian G, et al. Advances in hydrogen as a zero-carbon fuel for rotary engines: a review. *Fuel* 2025;381:133681.
- [15] Otchere P, Pan J, Fan B, et al. Recent studies of fuels used in Wankel rotary engines. *J Energy Res Technol* 2021;143(3):030801.
- [16] Wang H, Ji C, Wang D, et al. Investigation on the potential of using carbon-free ammonia and hydrogen in small-scaled Wankel rotary engines. *Energy* 2023;283:129166.
- [17] Moreno Cabezas K, Vorraro G, Liu X, et al. Numerical analysis of hydrogen injection and mixing in Wankel rotary engines. SAE Technical Paper 2023-24-0069, 2023.
- [18] Yang J, Ji C, Wang S, et al. An experimental study on ignition timing of hydrogen Wankel rotary engine. *Int J Hydrogen Energy* 2022;47:17468–78.
- [19] Du YL, Sun ZY, Huang Q. Leakage process and spontaneous ignition of hydrogen within a tube after releasing from the storage container with pressure up to 20 MPa. *Process Saf Environ Prot* 2025;193:217–27.
- [20] Jaber N, Mukai M, Kagawa R, et al. Amelioration of combustion of hydrogen rotary engine. *Int J Automot Eng* 2012;3:81–8.
- [21] Verhelst S, Sierens R, Versraeten S. A critical review of experimental research on hydrogen fueled SI engines. SAE Technical Paper 2006-01-04320, 2006.
- [22] Wang H, Ji C, Shi C, et al. Multi-objective optimization of a hydrogen-fueled Wankel rotary engine based on machine learning and genetic algorithm. *Energy* 2023;263:125961.
- [23] Sun ZY. Structure of turbulent rich hydrogen-air premixed flames. *Int J Energy Res* 2018;42:2845–58.
- [24] Shi C, Cheng T, Yang X, et al. Implementation of various injection rate shapes in an ammonia/diesel dual-fuel engine with special emphasis on combustion and emission characteristics. *Energy* 2024;304:132035.
- [25] Amrouche F, Erickson PA, Park JW, et al. Extending the lean operation limit of a gasoline Wankel rotary engine using hydrogen enrichment. *Int J Hydrogen Energy* 2016;41(32):14261–71.
- [26] Ozcanli M, Bas O, Akar MA, et al. Recent studies on hydrogen usage in Wankel SI engine. *Int J Hydrogen Energy* 2018;43(38):18037–45.
- [27] Zambalov SD, Yakovlev IA, Ji C, et al. Effect of dual port-direct injection of syngas in a rotary engine. *Fuel* 2023;354:129243.
- [28] Shi C, Chai S, Di L, et al. Combined experimental-numerical analysis of hydrogen as a combustion enhancer applied to Wankel engine. *Energy* 2023;263:125896.
- [29] Sadiq GA, Al-Dadah R, Mahmoud S. Development of rotary Wankel devices for hybrid automotive applications. *Emerg Conver Manage* 2019;202:112159.
- [30] Wang W, Zuo Z, Liu J. Miniaturization limitations of rotary internal combustion engines. *Emerg Conver Manage* 2016;112:101–14.
- [31] Tozer G, Al-Dadah R, Mahmoud S. Simulating apex gap sizes in a small scale Wankel expander for air liquefaction. 2019;154:476–484.
- [32] Yang J, Wang H, Ji C, et al. Investigation of intake closing timing on the flow field and combustion process in a small-scaled Wankel rotary engine under various engine speeds designed for the UAV application. *Energy* 2023;273:127147.
- [33] Su J, Xu M, Li T, et al. Combined effects of cooled EGR and a higher geometric compression ratio on thermal efficiency improvement of a downsized boosted spark-ignition direct-injection engine. *Emerg Conver Manage* 2014;78:65–73.
- [34] Turner J, Turner M, Vorraro, G, et al. Initial investigations into the benefits and challenges of eliminating port overlap in Wankel rotary engines. SAE Technical Paper 2020-01-0280, 2020.
- [35] Smail B, Mohiuddin AKM. Combustion chamber design effect on the rotary engine performance - a review. *Int J Automot Eng* 2020;4(11):200–12.

- [36] Jeng DZ, Hsieh MJ, Lee CC, et al. The Numerical Investigation on the performance of rotary engine with leakage, different fuels and recess sizes. SAE Technical Paper 2013-32-9160, 2013.
- [37] Zhang Y, Wang W. Efficiency enhancement in a meso-Wankel compressor with overflow. Proceedings of the Institution of Mechanical Engineers-Part C: Journal of Mechanical Engineering Science 2012;226:1550-1567.
- [38] Oh S, Kim C, Lee Y, et al. Experimental investigation of the hydrogen-rich offgas spark ignition engine under the various compression ratios. *Emerg Conver Manage* 2019;201:112136.
- [39] Gong C, Liu F, Sun J, et al. Effect of compression ratio on performance and emissions of a stratified-charge DISI (direct injection spark ignition) methanol engine. *Energy* 2016;96:166-75.
- [40] Fan B, Song A, Liu W, et al. Potential improvement in combustion performance of a natural gas rotary engine mixed with hydrogen by novel bluff-body. *Energy* 2024; 15:131077.
- [41] Taghavifar H, Khalilarya S, Jafarmadar S. Engine structure modifications effect on the flow behavior, combustion, and performance characteristics of DI diesel engine. *Emerg Conver Manage* 2014;85:20-32.
- [42] King P. Analysis of the design features of the Wankel and szorenyi rotary engines. SAE Technical Paper 2022-01-1109, 2022.
- [43] King P. Analysis of the design features of the Wankel and szorenyi rotary engines. SAE Technical Paper 2022-01-1109, 2022.
- [44] Huo S, Fan B, Xu L, et al. Combined effect of cylinder shape and turbulence blade on the combustion performance of a turbulent jet ignition rotary engine using hydrogen/natural gas blends. *Int J Hydrogen Energy* 2024;61:513-27.
- [45] Chen W, Yu S, Zuo Q, et al. Combined effect of air intake method and hydrogen injection timing on airflow movement and mixture formation in a hydrogen direct injection rotary engine. *Int J Hydrogen Energy* 2022;47:12739-58.
- [46] Harikrishnan TV, Challa S, Radhakrishna D. Numerical investigation on the effects of flame propagation in rotary engine performance with leakage and different recess shapes using three-dimensional computational fluid dynamics. *J Energy Res Technol* 2016;138:052210.
- [47] Fan BW, Pan JF, Liu YX, et al. Effect of pocket location on combustion process in natural gas-fueled rotary engine. *Appl Mech Mater* 2013;316-317:73-9.
- [48] Zhou NJ, Pei HL, Gao HL, et al. Effects of rotor recess geometries on combustion process in diesel rotary engine, 255-259. ASME; 2008.
- [49] Pisony S, Tartakovsky L. Numerical investigation of the combined influence of three-plug arrangement and slot positioning on Wankel engine performance. *Energies* 2021;14:11130.
- [50] Wang H, Ji C, Yang J, et al. Parametric modeling and analysis of intake phases for side-ported Wankel rotary engines. *Heliyon* 2023;9(11):e21710.
- [51] Shi C, Lei J, Tian G, et al. Numerical investigation recess geometry amelioration of an ammonia-hydrogen zero-carbon Wankel engine. *Renew Energy* 2025;242: 122497.
- [52] Shi C, Zhang Z, Wang H, et al. Parametric analysis and optimization of the combustion process and pollutant performance for ammonia-diesel dual-fuel engines. *Energy* 2024;296:131171.
- [53] Senecal P, Pomraning E, Richards K, et al. Multi-dimensional modeling of direct-injection diesel spray liquid length and flame lift-off length using CFD and parallel detailed chemistry. SAE Technical Paper 2003-01-1043, 2003.
- [54] Babajimopoulos A, Asanis DN, Flowers DL, et al. A fully coupled computational fluid dynamics and multi-zone model with detailed chemical kinetics for the simulation of premixed charge compression ignition engines. *Int J Engine Res* 2005;6(5):497-512.
- [55] Han Z, Reitz R. A temperature wall function formulation for variable-density turbulent flows with application to engine convective heat transfer modeling. *International Journal of Heat Mass and Transfer* 1997;40:613-265.
- [56] Yang X, Solomon A, Kuo TW. Ignition and combustion simulations of spray-guided SIDI engine using arrhenius combustion with spark-energy deposition model. SAE Technical Paper 2012-01-0147, 2012.
- [57] Heywood JB. Internal combustion engine fundamentals. New York: McGraw-Hill; 1988.
- [58] Liu Y, Ji M, Xie M, et al. Enhancement on a skeletal kinetic model for primary reference fuel oxidation by using a semidecoupling methodology. *Energy Fuel* 2012;26:7069-83.
- [59] Zambalov SD, Yakovlev IA, Skripnyak VA. Numerical simulation of hydrogen combustion process in rotary engine with laser ignition system. *Int J Hydrogen Energy* 2017;42:172510-9.
- [60] Shi C, Ji C, Wang S, et al. Experimental and numerical study of combustion and emissions performance in a hydrogen-enriched Wankel engine at stoichiometric and lean operations. *Fuel* 2021;291:120181.
- [61] Spreitzer J, Zahradnik F, Geringer B. Implementation of a rotary engine (Wankel engine) in a CFD simulation tool with special emphasis on combustion and flow phenomena. SAE Technical Paper 2015-01-0382, 2015.
- [62] Fan B, Zhang Y, Pan J, et al. Experimental and numerical study on the formation mechanism of flow field in a side-ported rotary engine considering apex seal leakage. *J Energy Res Technol* 2021;143(2):022303.
- [63] Fan B, Wang J, Pan J, et al. Computational study of hydrogen injection strategy on the combustion performance of a direct injection rotary engine fueled with natural gas/hydrogen blends. *Fuel* 2022;328:125190.
- [64] Chen W, Lu C, Zuo Q, et al. Combustion characteristics analysis and performance evaluation of a hydrogen engine under direct injection plus lean burn mode. *J Clean Prod* 2024;470:143323.
- [65] Zuo Q, Yang D, Shen Z, et al. Effect of premixed ratio on combustion and emission characteristics in a spark ignition engine with hydrogen-ammonia direct injection. *Fuel* 2025;393:135051.
- [66] Wang S, Sun Y, Yang J, et al. Effect of excess air ratio and ignition timing on the combustion and emission characteristics of the ammonia-hydrogen Wankel rotary engine. *Energy* 2024;302:131779.
- [67] Wang S, Yang H, Wang Z, et al. An investigation of the pre-chamber induced oxygen jet diffusion into hydrogen combustion: towards the upper stage ICE application. *Emerg Conver Manage* 2024;315:118746.
- [68] Cheng T, Duan R, Li X, et al. Progressive split injection strategies to combustion and emissions improvement of a heavy-duty diesel engine with ammonia enrichment. *Energy* 2025;316:134660.