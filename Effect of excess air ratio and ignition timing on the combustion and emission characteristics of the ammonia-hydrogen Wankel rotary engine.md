

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the journal Energy](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the journal Energy

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Effect of excess air ratio and ignition timing on the combustion and emission characteristics of the ammonia-hydrogen Wankel rotary engine

Shuofeng Wang<sup>a,\*</sup>, Yu Sun<sup>a</sup>, Jinxin Yang<sup>a,\*\*</sup>, Huaiyu Wang<sup>b</sup>

<sup>a</sup> College of Mechanical and Energy Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

<sup>b</sup> School of Mechanical Engineering, Beijing Institute of Technology, Beijing, 100081, PR China

## ARTICLE INFO

### Keywords:

Ammonia-hydrogen  
Wankel rotary engine  
Excess air ratio  
Ignition timing  
Combustion and emissions

## ABSTRACT

As a hydrogen carrier, ammonia can suppress knock and enhance thermal efficiency of the hydrogen-fueled Wankel rotary engine (WRE), and achieve zero carbon emissions. This research established a three-dimensional fluid dynamics model coupled with detailed reaction kinetics of ammonia and hydrogen and verified it based on experiments. Incorporating 10% volume fraction of ammonia into the hydrogen-fueled WRE eliminates knock and decreases the excess air ratio ( $\lambda$ ) from 1.8 to 1.4, effectively improving the indicated mean effective pressure (IMEP). The results indicate that when  $\lambda$  exceeds 1.4, flame propagation accelerates with higher concentration of the mixture. This enhances peak in-cylinder pressure and heat release rate, but it results higher NOx emissions. As  $\lambda$  varies from 1.8 to 1.4, NOx emission levels rise by 47.4%. At  $\lambda \le 1.2$ , the rapid flame propagation leads to short combustion duration, diminishing the power output. At this stage, the NO formation is dominated by H radicals, and the NOx production reaches its minimum value at  $\lambda$  of 1.0. In summary, the ammonia-hydrogen WRE achieves optimal performance at  $\lambda$  of 1.4 and ignition timing of  $-5^\circ$ CA after top dead center, the indicated thermal efficiency reaches 36.9% and the IMEP achieves 0.683 MPa.

## Nomenclature

(continued)

|         |                                             |
|---------|---------------------------------------------|
| ABDC    | After bottom dead center                    |
| AMR     | Adaptive mesh refinement                    |
| ARPE    | Ammonia-fueled reciprocating piston engine  |
| ATDC    | After top dead center                       |
| BBDC    | Before bottom dead center                   |
| BTDC    | Before top dead center                      |
| CFD     | Computational Fluid Dynamic                 |
| CA0-10  | Flame development period                    |
| CA10-90 | Flame propagation period                    |
| EGR     | Exhaust gas recirculation                   |
| HRPE    | Hydrogen-fueled reciprocating piston engine |
| HRR     | Heat release rate                           |
| IMEP    | Indicated mean effective pressure           |
| IT      | Ignition timing                             |
| ITE     | Indicated thermal efficiency                |
| LSP     | Leading spark plug                          |
| LBV     | Laminar burning velocity                    |
| MAP     | Manifold absolute pressure                  |
| NO      | Nitric oxide                                |

(continued on next column)

|                  |                      |
|------------------|----------------------|
| NO <sub>2</sub>  | Nitrogen dioxide     |
| N <sub>2</sub> O | Nitrous oxide        |
| NOx              | Nitrogen oxide       |
| TSP              | Trailing spark plug  |
| TDC              | Top dead center      |
| WRE              | Wankel rotary engine |
| $\lambda$        | Excess air ratio     |

## 1. Introduction

Currently, with the extensive consumption of fossil fuels, a series of climate issues such as ozone layer depletion, glacial melting, and tropical cyclones caused by greenhouse gas emissions are receiving widespread attention [1]. The goals of “carbon peak and carbon neutrality” have highlighted the importance of optimizing energy consumption structures, accelerating the development of the clean energy industry, and adopting zero-carbon fuels as crucial strategy for the energy

\* Corresponding author.

\*\* Corresponding author.

E-mail addresses: [shfwang@bjut.edu.cn](mailto:shfwang@bjut.edu.cn) (S. Wang), [yangjinxin@bjut.edu.cn](mailto:yangjinxin@bjut.edu.cn) (J. Yang).

transition [2]. Energy consumption in the transportation sector accounts for a significant portion of global total energy use [3]. Therefore, using low-carbon and zero-carbon alternative fuels in the transportation is crucial for cutting carbon emissions and combating global climate warming [4]. At present, numerous researchers have achieved ideal results using alternative fuels such as alcohol fuels [5], natural gas [6], dimethyl ether [7], and biomass fuels [8] in internal combustion engines. However, the carbon content in these fuels limits their contribution in reducing carbon emissions [9].

Hydrogen, as a zero-carbon fuel, has many advantages such as fast flame propagation [10], short quenching distance [11], wide combustion concentration limit [12]. Moreover, its combustion product is solely water, thus it will not cause pollution to the environment [13]. The Wankel rotary engine (WRE) has the advantages of small volume, light weight, high power density [14], and excellent high-speed performance. It holds broad application prospects in many fields including drones, mobile power generators, and electric vehicle range extenders [15]. Hydrogen enrichment facilitates combustion, allowing for stable operation and rapid combustion under high-speed conditions [16], despite with high heat transfer losses, extensive quenching zones, and elongated combustion chambers in the WRE. This strategy achieves higher thermal efficiency and zero carbon emissions. At present, many people have conducted research on the application of hydrogen fuel to rotary engines [17]. Su et al. [18] conducted experimental investigations into the effects of varying excess air ratios on the performance of hydrogen-fueled WRE and found that the fuel energy flow rate and the stability of the engine are inversely proportional to the excess air ratio [19]. Employing lean combustion control strategy can achieve higher effective thermal efficiency. Meng et al. [20] found that oxygen enrichment enhances the brake torque of the hydrogen-fueled WRE and reduces NO emission effectively, but it will decrease the brake thermal efficiency. Chen et al. [21] and Yang et al. [22] established a simulation model of hydrogen direct-injection WRE and explored the optimal air intake and hydrogen injection methods, which can effectively improve the charging efficiency of the hydrogen WRE and further improve the thermal efficiency. In order to reduce carbon emissions, Shi et al. [23] found that hydrogen two-stage direct injection can improve combustion characteristics and the thermal efficiency at the tail of combustion chamber, and suppress abnormal combustion in the hydrogen-fueled WRE.

Due to the complex flow dynamics in the cylinder of WRE and the rapid combustion speed of hydrogen [24], the ignition and combustion processes is highly transient. It can lead to abnormal combustion phenomena such as knock and backfiring [25], which makes it unable for the rotary engine to operate stably under high-speed conditions, resulting in high NOx emissions. In their experimental research, Meng et al. [26] found that the hydrogen-fueled WRE is less prone to backfire due to its structural advantages than the hydrogen-fueled reciprocating piston engine (HRPE). However, they noted that the knock intensity in the hydrogen-fueled WRE is significantly higher than in HRPE under similar operating conditions, due to combustion fluctuations and the auto-ignition of hydrogen in end-gas mixtures [27]. Szwaja et al. [28] identified strong correlation between the knock intensity and the combustion speed and duration. They highlighted that decreasing the flame combustion speed and flow rate in the cylinder, and suppressing the intensity of the knock, is key to enhance the work capacity and combustion efficiency. Despite many people have made efforts to suppress abnormal combustion in rotary engines, the power density output is significantly constrained by the low energy density of the single hydrogen fuel and strict operational requirement.

Ammonia, recognized for its safe, efficient, and economical systems for production, transportation, and storage, is an effective hydrogen carrier [29]. Meanwhile, ammonia exhibits lower reaction activity, higher ignition energy, and slower combustion speed make it a feasible alternative fuel for internal combustion engines [30]. Liu et al. [31] conducted experimental research on the impact of ammonia addition on combustion performance and knock suppression in a high compression

ratio gasoline engine. They found that blending ammonia can reduce cylinder temperature and mixture's reactivity, suppress knock, and enhance both thermal efficiency and fuel economy. Wei et al. [32] applied ammonia fuel to a spark-ignition marine natural gas engine. They found that ammonia addition effectively reduced the peak pressure and HRR in the cylinder of engine, decreased combustion temperature and heat transfer losses, and enhanced the optimum brake thermal efficiency by 1% relative to a pure natural gas engine. A consensus among scholars through research found that ammonia-hydrogen fuel demonstrates good compatibility in terms of physical and chemical properties [33]. The amalgamation of ammonia and hydrogen fuels is recognized as a key technological approach to prevent abnormal combustion in pure hydrogen fuels, thereby enabling stable ignition and efficient combustion in zero-carbon internal combustion engines [34]. In the research of ammonia-hydrogen fusion fuel, on the one hand, hydrogen is used as a combustion enhancer to facilitate stable ignition and efficient combustion in the ammonia-fueled reciprocating piston engine (ARPE). Lhuillier et al. [30] found through experiments that the addition of hydrogen can effectively enhance the laminar burning velocity (LBV) of the mixture. When the hydrogen volume fraction is 20%, it can improve the operation stability and avoid misfire in the ARPE. M. H. Dinesh et al. [35] found that the addition of hydrogen can effectively enhance combustion, leading to increase pressure and peak temperature. They determined the optimal ammonia-hydrogen mixture ratio for the engine performance under the experimental condition [36]. On the other hand, ammonia is utilized as an additive to suppress the abnormal combustion in the HRPE, thereby improving the combustion stability and power of the engine. Xin et al. [37] conducted experiments to explore the effect of ammonia addition on the combustion and emission characteristics of the HRPE. They found that the inclusion of ammonia can reduce the heat release rate (HRR), prolong the flame development period (CA0-10) and flame propagation period (CA10-90) [38], effectively suppress abnormal combustion and increase the indicated mean effective pressure (IMEP) and indicated thermal efficiency (ITE) in the HRPE. Yu et al. [39] experimentally investigated the impact of different excess air ratios on the performance of ammonia-hydrogen blended injection internal combustion engine. They discovered that the engine demonstrates optimal overall performance when the hydrogen ratio is 27.3%, with the  $\lambda$  ranging between 1 and 1.2. The aforementioned research indicates the feasibility of using ammonia-hydrogen blended fuel in internal combustion engines. The zero-carbon, high-efficiency and stable combustion can be achieved by rationally controlling the ammonia-hydrogen mixture ratio and operating conditions in the engine. Previous studies have predominantly focused on reciprocating internal combustion engines. Wang et al. [40] explored the innovative use of carbon-free ammonia and hydrogen fuels in the WRE. Their main goal was to enhance the ammonia fuel ratio to improve energy efficiency and emission reduction potentialities in the WRE. Currently, there is limited research on using ammonia blending to prevent abnormal combustion in the hydrogen-fueled WRE. Common strategies to control abnormal combustion in hydrogen-fueled engines including lean combustion [41], water injection [42], and exhaust gas recirculation (EGR) [43]. However, these techniques significantly restrict the engine's power output [44]. The addition of ammonia into the hydrogen-fueled engine can effectively reduce knock and enhance thermal efficiency [45].

Based on the above findings, in order to enhance the power and thermal efficiency of the ammonia-hydrogen WRE, this study is to utilize ammonia as a neutralizing agent to prevent abnormal combustion and ensure stable operation of the WRE under richer fuel mixtures. This approach effectively broadens the operating boundary of ammonia-hydrogen WRE. Initially, building a model of ammonia-hydrogen fueled WRE by Computational Fluid Dynamic (CFD) numerical simulation software, calibrated based on bench test data (as described in Section 2). Section 3 analyzes the effects of varying  $\lambda$  and ignition timing (IT) on flow characteristics, turbulence combustion process, and the mechanisms and distribution patterns of NOx in the cylinder of the

ammonia-hydrogen WRE. This provides essential data and reference for the practical application for zero-carbon, high-efficiency, and stable operation of the WRE.

## 2. The CFD model establishment and validation

### 2.1. Engine geometric model

This article presents a three-dimensional model constructed with CONVERGE software, based on the Mazda 13B rotary engine. The specific model parameters of the WRE are as shown in Table 1, while Fig. 1 illustrates the geometric schematic of the WRE. Different from the reciprocating piston engine, the cylinder is divided into three independent combustion chambers by the triangular rotor in the WRE [46]. The configuration relies on the triangular rotor to achieve synchronous changes in the volume of three different combustion chambers by rotating clockwise. This mechanism facilitates the intake, compression, power, and exhaust strokes. The ignition system consists of two spark plugs, where the front spark plug is a leading spark plug (LSP) and the rear spark plug is a trailing spark plug (TSP). The intake and exhaust ports are situated on the cylinder head, with air intake through the end face [47]. Before entering the combustion chamber, ammonia, hydrogen, and air are mixed in the intake passage. When the rotor approaches its top dead center (TDC), spark plugs ignite the fuel-air mixture by releasing energy. The study conducted multi-cycle simulations and analyzed the flow field and combustion characteristics in-cylinder of the ammonia-hydrogen WRE after achieving stable combustion.

### 2.2. Initial conditions and mathematical model

In this study, the grid cutting technology in the CONVERGE software was used to generate appropriate grids. Subsequently, grid control techniques were applied for grid refinement. The base grid size is adopted to 4 mm, with boundary regions undergoing 1-scale fixed refinement and the entire combustion area is subjected to Adaptive mesh refinement (AMR), equivalent to 2 mm+ AMR, as depicted in Fig. 2. This configuration ensures computational accuracy while maintaining higher computational efficiency. Specific grid independence validation is discussed in previous work [48]. Based on experimental measurements and empirical calculations, the surface meshes of the intake and exhaust ports are set as the flow inlet and outlet boundaries, the wall temperatures of the rotor and cylinder are assumed to be 450 K, and temperatures of the spark plug and the electrode are set to be 600 K and 650 K respectively. The CONVERGE software provides extensive array of turbulence, breakup and combustion models. This study selects the RNG K- $\epsilon$  turbulence model, which overlooks the volume and inertia force of the fluid flow, more effectively considers the influence of the swirling flows and accurately captures the flow field characteristics in the WRE [49]. The O'Rourke and Amsden wall heat transfer model was chosen [50]. Utilizing the SAGE combustion model, this study incorporates the ammonia-hydrogen chemical reaction mechanism by Zhang et al., which includes 38 species and 263 reactions [51].

**Table 1**

Major model parameters of the WRE.

| Structural parameters | Value       |
|-----------------------|-------------|
| Number of rotors      | 2           |
| Eccentricity/mm       | 15          |
| Generating radius/mm  | 105         |
| Width of rotor/mm     | 80          |
| Compression ratio     | 10:1        |
| Intake open/°CA       | 3 °CA ATDC  |
| Intake close/°CA      | 65 °CA ABDC |
| Exhaust open/°CA      | 50 °CA BBDC |
| Exhaust close/°CA     | 3 °CA BTDC  |

![Simplified geometric schematic of the WRE. The diagram shows a cross-section of the rotary engine with a triangular rotor inside a cylindrical housing. The rotor divides the cylinder into three combustion chambers labeled Chamber I, Chamber II, and Chamber III. Two spark plugs are shown: a Leading spark plug at the front and a Trailing spark plug at the rear. Intake and exhaust ports are also visible on the cylinder head. A clockwise rotation arrow indicates the rotor's movement.](f5fd8a6b12eff431b5d2cc73cad225b0_img.jpg)

Simplified geometric schematic of the WRE. The diagram shows a cross-section of the rotary engine with a triangular rotor inside a cylindrical housing. The rotor divides the cylinder into three combustion chambers labeled Chamber I, Chamber II, and Chamber III. Two spark plugs are shown: a Leading spark plug at the front and a Trailing spark plug at the rear. Intake and exhaust ports are also visible on the cylinder head. A clockwise rotation arrow indicates the rotor's movement.

**Fig. 1.** Simplified geometric schematic of the WRE.

![Three-dimensional grid model of the WRE. This image shows a detailed mesh of the engine components. The rotor and cylinder walls are shown with a fine grid. The intake and exhaust ports are also meshed. Labels include 'Intake port', 'Exhaust port I', 'Rotor', 'Fixed Embedding', 'Adaptive Mesh Refinement', 'Cylinder', 'Trailing spark plug', and 'Leading spark plug'. An inset shows a magnified view of the mesh around a spark plug.](de09a3bb7d77b9108650b10e8df0e7c8_img.jpg)

Three-dimensional grid model of the WRE. This image shows a detailed mesh of the engine components. The rotor and cylinder walls are shown with a fine grid. The intake and exhaust ports are also meshed. Labels include 'Intake port', 'Exhaust port I', 'Rotor', 'Fixed Embedding', 'Adaptive Mesh Refinement', 'Cylinder', 'Trailing spark plug', and 'Leading spark plug'. An inset shows a magnified view of the mesh around a spark plug.

**Fig. 2.** Three-dimensional grid model of the WRE.

### 2.3. Model validation

The specific technical parameters of the rotary engine are shown in Table 2. To achieve ammonia-hydrogen fuel operation in the prototype rotary engine, the experiment has modified the original test system. Ammonia and hydrogen supply lines were designed, with heating tape wrapped around the ammonia storage tank to vaporize the liquid ammonia. This allows ammonia enters the intake manifold by the pressure difference and is controlled by thermal mass flowmeters for the

**Table 2**

Adoption of the WRE calibration conditions.

| Specification       | Value                          |
|---------------------|--------------------------------|
| Intake pressure/kPa | 100                            |
| Engine speed/rpm    | 3000                           |
| $\lambda$           | 1.8                            |
| IT                  | TDC                            |
| Cooling method      | Water-cooled                   |
| Ignition source     | Spark plug                     |
| Intake method       | Side-ported/Natural aspiration |
| Exhaust method      | Dual side-ported               |

flow rate [52]. The instruments and uncertainties used in experiment are shown in Table 3.

The volume fraction of ammonia in the total fuel is defined as the volume fraction of ammonia in the ammonia-hydrogen mixtures [53]. The excess air ratio ( $\lambda$ ) is the ratio of the actual to the theoretical air volume required for fuel combustion, as detailed in equations (1) and (2).

$$\alpha_{NH_3} = \frac{V_{NH_3}}{V_{NH_3} + V_{H_2}} \times 100\% \quad (1)$$

$$\lambda = \frac{m_{air}}{m_{NH_3}AF_{st,NH_3} + m_{H_2}AF_{st,H_2}} \quad (2)$$

In this context,  $V_{NH_3}$  and  $V_{H_2}$  respectively denote the volumetric flow rates (L/min) of ammonia and hydrogen into the combustion chamber under the standard condition. Meanwhile,  $m_{NH_3}$ ,  $m_{H_2}$ , and  $m_{air}$  represent the mass of ammonia, hydrogen, and air entering the combustion chamber. The terms  $AF_{st,NH_3}$  and  $AF_{st,H_2}$  refer to the stoichiometric air-fuel ratios of hydrogen and ammonia, respectively.

Fig. 3 shows the comparison curves between experimental and simulation results for three different ammonia/hydrogen volume ratios in the ammonia-hydrogen WRE under engine speed of 3000 rpm,  $IT = 4^\circ CA$  BTDC, and excess air ratio of 1.8, which are pure hydrogen ( $\alpha_{NH_3} = 0\%$ ), ammonia volume fractions of 10% and 20%. It can be seen that with different ammonia-hydrogen ratios, the absolute errors in the peak cylinder pressures between experimental and numerical simulation are all below 0.1 bar, with the crank angles corresponding to the peak cylinder pressures are all less than  $3^\circ CA$ . The above findings validate the accuracy of the established model, confirming its suitability in analyzing the turbulent combustion characteristics of the ammonia-hydrogen WRE.

### 2.4. Research matrix

The operating conditions are shown in Table 4. In order to improve the performance of the WRE as much as possible, the effect of different  $\lambda$  on the combustion and emission under the condition of 10% ammonia volume fraction was firstly explored. To clearly demonstrate the changes and differences between different operating conditions, the step size of  $\lambda$  is set to 0.2. The  $IT$  was adjusted in a step of 5 under condition  $\lambda = 1.4$  to find the optimal performance of the WRE.

## 3. Results and discussion

### 3.1. The effect of the excess air ratio

#### 3.1.1. Flow characteristics analysis

The flow field within the combustion chamber of significantly influences mixture formation and combustion process. Accordingly, this study conducts detailed formation and evolution analysis of vortex structures within the combustion chamber, as well as the variations and

![Figure 3: Model validation for in-cylinder pressure at different alpha_NH3. The graph plots In-cylinder pressure (MPa) on the y-axis (0.0 to 3.0) against Crank angle (°CA) on the x-axis (-100 to 150). Four data series are shown: alpha_NH3 = 0% (Exp. and Cal.), alpha_NH3 = 10% (Exp. and Cal.), and alpha_NH3 = 20% (Exp. and Cal.). The curves show a peak pressure around 2.8 MPa at approximately 25° CA. The experimental data (Exp.) are represented by open squares, and the calculated data (Cal.) are represented by solid lines of the same color. The legend also includes IT=4°CA BTDC, Speed=3000 rpm, and MAP=100 kPa.](4dd8d88230d428bc0cb93152bb714af2_img.jpg)

Figure 3: Model validation for in-cylinder pressure at different alpha\_NH3. The graph plots In-cylinder pressure (MPa) on the y-axis (0.0 to 3.0) against Crank angle (°CA) on the x-axis (-100 to 150). Four data series are shown: alpha\_NH3 = 0% (Exp. and Cal.), alpha\_NH3 = 10% (Exp. and Cal.), and alpha\_NH3 = 20% (Exp. and Cal.). The curves show a peak pressure around 2.8 MPa at approximately 25° CA. The experimental data (Exp.) are represented by open squares, and the calculated data (Cal.) are represented by solid lines of the same color. The legend also includes IT=4°CA BTDC, Speed=3000 rpm, and MAP=100 kPa.

Fig. 3. Model validation for in-cylinder pressure at different  $\alpha_{NH_3}$ .

Table 4  
Numerical simulation case settings.

| Conditions                 | $\lambda$             | $IT$ ( $^\circ CA$ ATDC) |
|----------------------------|-----------------------|--------------------------|
| Test 1 different $\lambda$ | 1.8 to 1.0 (step 0.2) | 0                        |
| Test 2 different $IT$      | 1.4                   | -10 to 10 (step 5)       |

distribution of the velocity field. Fig. 4 shows the evolution of the vorticity field and streamline changes in the cylinder during the intake and compression phases. As the intake port progressively opens, the mixture of fuel and air enters the combustion chamber from the end-face intake port, impacting the opposite cylinder end-face to form vortex groups. By  $420^\circ CA$  BTDC, two obvious vortexes formed, such as Vortex A and B. With the clockwise rotation of the rotor, vortex A is squeezed by the radius is gradually reduced, while the increasing volume of the cylinder around Vortex B leads to an enlargement of its radius. At  $340^\circ CA$  BTDC, vortex A almost dissipates and vortex B almost full of the entire cylinder, making the average vorticity of the cylinder is reduced. At  $180^\circ CA$  BTDC, vortex A has entirely vanished, and vortex B gradually converge towards the front part of the combustion chamber with the compression stroke. By  $100^\circ CA$  BTDC, a directed main flow field gradually forms within the combustion chamber. Although Vortex B remains, it is significantly reduced and dispersed due to the end of compression stroke and the minimization of the combustion chamber volume.

Fig. 5 depicts the changes in the velocity field within the combustion chamber before ignition. In the diagram, blue area represents the low-velocity region, while red area represents high-velocity region. It is observable that at  $80^\circ CA$  BTDC, the low-velocity region occupies more extensive area at higher  $\lambda$ , and the flow velocity within the cylinder gradually increases as  $\lambda$  decreases. With the rotation of the rotor, the volume within the cylinder decreases, leading to an increase in-cylinder pressure and mixture concentration. This leads to an increase in the flow velocity within the cylinder. The region of high velocity is predominantly located near the LSP and continues to expand in size up until ignition as the compression stroke progresses. This phenomenon is mainly attributed to the smaller cross-sectional area at the short axis of the WRE, the airflow will be squeezed when it passes through, results in a rapid increase in the flow velocity. In addition, influenced by the unidirectional airflow within the combustion chamber, the center of the high-speed area is closer to the front part of the chamber, ultimately appeared near the LSP.

#### 3.1.2. Combustion process analysis

Fig. 6 shows the curves of in-cylinder pressure and HRR under

Table 3  
Professional instrument list.

| Parameters                | Uncertainty                           | Manufacturer | Type          |
|---------------------------|---------------------------------------|--------------|---------------|
| Engine speed              | $\le \pm 1$ rpm                       | Power link   | CAC6          |
| Torque                    | $\le \pm 0.4$ % F.S.                  | Power link   | CAC6          |
| Hydrogen volume flow rate | $\le \pm 0.02$ L/min                  | Seven star   | D07-60B       |
| Ammonia volume flow rate  | $\le \pm 0.1$ L/min                   | Air boost    | AB-13         |
| Air volume flow rate      | $\le \pm 0.1$ L/min                   | Tociel       | 20N060        |
| Air-to-fuel ratio         | $\le \pm 0.007$                       | Horiba       | MEXA-730A     |
| In-cylinder pressure      | $\le \pm 0.3$ bar                     | Kistler      | 6117BFD17     |
| NO concentration          | $\le \pm 0.1$ % of the measured value | Horiba       | MEXA-7100DEGR |

![Figure 4: Streamline and vorticity field within combustion chamber of the WRE. The figure is a 2x2 grid of 3D visualizations. The top row shows the combustion chamber at 420°CA BTDC (left) and 340°CA BTDC (right). The bottom row shows the combustion chamber at 180°CA BTDC (left) and 100°CA BTDC (right). A color bar on the right indicates Vorticity (s⁻¹) ranging from 0 (blue) to 20000 (red). In the top row, Vortex A and Vortex B are labeled. In the bottom row, Vortex B is labeled. The visualizations show streamlines (blue lines) and vorticity fields (color maps) within the combustion chamber geometry.](7a3561af571faf036baa93f5f4b1bdb9_img.jpg)

Figure 4: Streamline and vorticity field within combustion chamber of the WRE. The figure is a 2x2 grid of 3D visualizations. The top row shows the combustion chamber at 420°CA BTDC (left) and 340°CA BTDC (right). The bottom row shows the combustion chamber at 180°CA BTDC (left) and 100°CA BTDC (right). A color bar on the right indicates Vorticity (s⁻¹) ranging from 0 (blue) to 20000 (red). In the top row, Vortex A and Vortex B are labeled. In the bottom row, Vortex B is labeled. The visualizations show streamlines (blue lines) and vorticity fields (color maps) within the combustion chamber geometry.

Fig. 4. Streamline and vorticity field within combustion chamber of the WRE.

different  $\lambda$  at IT = TDC with  $\alpha_{\text{NH}_3} = 10\%$ . Additionally, for comparative analysis, the graph includes the in-cylinder pressure curve for  $\alpha_{\text{NH}_3} = 0\%$  at  $\lambda$  of 1.4. The graph reveals that there is a gradual increase in peak cylinder pressure, and the crank angle corresponding to the peak pressure advances after ignition as  $\lambda$  decreases. This is primarily due to an increase in the total fuel mass within the cylinder as  $\lambda$  decreases, which accelerates the flame propagation speed and concentrates the heat release process. Consequently, this results in more complete combustion of the fuel, releasing a large amount of heat in a short time under specific volume condition. At  $\lambda = 1.0$ , rapid fuel combustion causes a sharp increase in HRR, so only the HRR for the other cases are compared. As  $\lambda$  decreases, the peak of the HRR progressively rises, and its rate of increase accelerates. When  $\lambda = 1.8$ , the crank angle corresponding to the peak HRR is approximately around 22 °CA ATDC. In contrast, this peak HRR advances to around 5 °CA ATDC at  $\lambda = 1.0$ , followed by a rapid decline after the peak.

The above phenomenon can be more clearly reflected through flame development and propagation contour diagram. The flame kernel development is shown in Fig. 7. The flame kernel contour is visible in the cross section of the center region of the LSP and TSP at 5 °CA ATDC. As indicated by the high-temperature areas, the initial flame kernel forms immediately after the spark plug ignites the surrounding mixture. The area and temperature of the flame kernel are inversely proportional to  $\lambda$ . A decrease in  $\lambda$  leads to faster formation and development of the initial flame kernel, which is conducive to improving the ignition stability. Fig. 8 shows the flame propagation contour under different  $\lambda$  conditions, providing an intuitive visualization of the aforementioned results. The velocity streamline reveals the formation of a unidirectional flow field within the combustion chamber in the same direction as the rotor rotation [54]. The flow velocity is higher in the middle of the combustion chamber and lower at the front and rear. With the combustion

progresses and the release of heat, the flame gradually expands and propagates to the surrounding area, following the main propagation direction of the flow field. Under lower  $\lambda$  conditions, where the surrounding mixture concentration is higher and the flame front can propagate more rapidly, accelerating the combustion process. For example, the flame of TSP propagates toward the front of the combustion chamber and merges with the LSP flame at  $\lambda = 1.6$  probably at 15 °CA ATDC, and the similar scenario occurs at  $\lambda$  of 1.4 at 10 °CA ATDC. When the flames merge, the main propagation direction is towards the front of the combustion chamber. The flame front reaches the cylinder wall at 25 °CA ATDC under  $\lambda = 1.4$ , and the flame propagation is hindered due to the squish effect in the combustion chamber. The figure reveals that as  $\lambda$  increases, the flame propagation to the end of the combustion chamber is significantly enhanced, and the higher of mixture concentration the more obvious this trend. Thus, increasing the mixture concentration not only aids in enhancing the power in the WRE but also improves the combustion efficiency of the mixture.

Indicative performance can reflect the quality of the thermal work conversion process within the internal combustion engine cylinder [55]. The ITE is a ratio of the thermal equivalent of the effective power in the engine to the heat content of the fuel consumed per unit time, serving as a measure of the economic performance of the internal combustion engine [56]. Enhancing the ITE is a crucial strategy for fuel conservation and reducing pollutant emissions. Meanwhile, the IMEP represents the indicated work per unit volume of the cylinder, which can reflect the working capacity and serve as an indicator for evaluating the power performance of the internal combustion engine. Fig. 9 shows the trend of the ITE and IMEP under different  $\lambda$  conditions. As  $\lambda$  decreases, the ITE and IMEP initially increase and then decrease, which is due to the fact that their obvious positive correlation with the peak cylinder pressure. With the decrease of  $\lambda$ , the combustion heat release and the resultant

![Figure 5: Velocity field in-cylinder before ignition of the WRE. The figure consists of a 5x4 grid of velocity vector plots. The columns represent crank angles: 80°CA BTDC, 40°CA BTDC, 20°CA BTDC, and TDC. The rows represent lambda values: 1.0, 1.2, 1.4, 1.6, and 1.8. A color bar on the right indicates velocity in m/s, ranging from 0 (blue) to 40 (red). A black arrow at the bottom indicates the rotor rotating direction. The plots show the evolution of the velocity field as the crank angle approaches TDC and as the air-fuel ratio (lambda) changes.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 5: Velocity field in-cylinder before ignition of the WRE. The figure consists of a 5x4 grid of velocity vector plots. The columns represent crank angles: 80°CA BTDC, 40°CA BTDC, 20°CA BTDC, and TDC. The rows represent lambda values: 1.0, 1.2, 1.4, 1.6, and 1.8. A color bar on the right indicates velocity in m/s, ranging from 0 (blue) to 40 (red). A black arrow at the bottom indicates the rotor rotating direction. The plots show the evolution of the velocity field as the crank angle approaches TDC and as the air-fuel ratio (lambda) changes.

Fig. 5. Velocity field in-cylinder before ignition of the WRE.

![Figure 6: In-cylinder pressure and HRR profiles at different lambda. (a) In-cylinder pressure (MPa) vs Crank angle (°CA). (b) Heat Release Rate (HRR) (J/°CA) vs Crank angle (°CA). Both plots show curves for lambda = 1.8, 1.6, 1.4, 1.2, 1.0, and 0.8. The legend indicates lambda values and alpha_ND values (10% or 0%).](ac99eff233b8fe51d30f499e7413c345_img.jpg)

Figure 6: In-cylinder pressure and HRR profiles at different lambda. (a) In-cylinder pressure (MPa) vs Crank angle (°CA). (b) Heat Release Rate (HRR) (J/°CA) vs Crank angle (°CA). Both plots show curves for lambda = 1.8, 1.6, 1.4, 1.2, 1.0, and 0.8. The legend indicates lambda values and alpha\_ND values (10% or 0%).

Fig. 6. In-cylinder pressure and HRR profiles at different  $\lambda$ .

increase in cylinder pressure enhance the work output of the engine. However, at excessively low  $\lambda$  values, resulting in an overly rich mixture and the combustion process occurs rapidly, markedly shortening the combustion duration. The cylinder pressure drops rapidly after reaching its peak value, leading to a decrease in work capacity. For optimal balance between economy and power, the WRE reaches its optimum performance near  $\lambda = 1.4$ , with a 4.2% increase in the ITE compared to  $\lambda$  of 1.8 and the IMEP rises by 29.2%. Subsequent sections will delve into detailed investigations under the  $\lambda$  equal to 1.4 condition.

#### 3.1.3. Formation and distribution of NOx

The main components of NOx include NO, N<sub>2</sub>O, and NO<sub>2</sub>. Notably, N<sub>2</sub>O and NO<sub>2</sub> are derived as intermediate products from NOx with mass fraction are two and four orders lower than NO, respectively. The concentration of N<sub>2</sub>O declines as the excess air ratio decreases, whereas NO<sub>2</sub> increases with the decrease of excess air ratio, showing an initial increase then decrease. Fig. 10 shows the evolution profiles of NOx mass fraction with crank angle at different  $\lambda$ . It can be seen that the rate of NOx formation gradually accelerates and its quantity increases as  $\lambda$  decreases at leaner mixture concentrations. However, a different trend emerges when  $\lambda$  is reduced to 1.2. At this time, the generation of NOx

![Figure 7: Comparison of flame kernel at different lambda values. The figure is a 4x5 grid of circular cross-sections of a combustion chamber. The columns represent lambda values: 1.8, 1.6, 1.4, 1.2, and 1.0. The rows represent different measurement planes: LSP (top), TSP (second), LSP (third), and TSP (bottom). A color bar on the right indicates temperature in Kelvin (K) from 400 to 2400. The flame kernel is shown as a colored region within the chamber, with the color representing temperature. As lambda decreases, the flame kernel becomes more compact and centered.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 7: Comparison of flame kernel at different lambda values. The figure is a 4x5 grid of circular cross-sections of a combustion chamber. The columns represent lambda values: 1.8, 1.6, 1.4, 1.2, and 1.0. The rows represent different measurement planes: LSP (top), TSP (second), LSP (third), and TSP (bottom). A color bar on the right indicates temperature in Kelvin (K) from 400 to 2400. The flame kernel is shown as a colored region within the chamber, with the color representing temperature. As lambda decreases, the flame kernel becomes more compact and centered.

Fig. 7. Comparison of flame kernel at different  $\lambda$ .![Figure 8: Comparison of flame propagation at different lambda values. The figure is a 3x5 grid of cross-sectional views of the combustion chamber. The columns represent crank angles: 5°CA ATDC, 10°CA ATDC, 15°CA ATDC, 20°CA ATDC, and 25°CA ATDC. The rows represent lambda values: 1.8, 1.6, and 1.4. A color bar on the right indicates velocity in m/s from 0 to 40. The flame front is shown as a red/pink region. As lambda decreases, the flame propagation is more rapid and covers a larger area of the chamber.](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 8: Comparison of flame propagation at different lambda values. The figure is a 3x5 grid of cross-sectional views of the combustion chamber. The columns represent crank angles: 5°CA ATDC, 10°CA ATDC, 15°CA ATDC, 20°CA ATDC, and 25°CA ATDC. The rows represent lambda values: 1.8, 1.6, and 1.4. A color bar on the right indicates velocity in m/s from 0 to 40. The flame front is shown as a red/pink region. As lambda decreases, the flame propagation is more rapid and covers a larger area of the chamber.

Fig. 8. Comparison of flame propagation at different  $\lambda$ .![Figure 9: Comparison of the ITE and IMEP at different lambda values. The figure is a bar chart with lambda values on the x-axis (1.8, 1.6, 1.4, 1.2, 1). The left y-axis is ITE (%) and the right y-axis is IMEP (MPa). ITE is represented by red bars and IMEP by blue bars. The values for ITE are 35.3, 37.6, 36.8, 31.3, and 24.9 respectively. The values for IMEP are 0.527, 0.625, 0.681, 0.656, and 0.596 respectively.](01da0d212fb571933f10f96556157745_img.jpg)

| $\lambda$ | ITE (%) | IMEP (MPa) |
|-----------|---------|------------|
| 1.8       | 35.3    | 0.527      |
| 1.6       | 37.6    | 0.625      |
| 1.4       | 36.8    | 0.681      |
| 1.2       | 31.3    | 0.656      |
| 1         | 24.9    | 0.596      |

Figure 9: Comparison of the ITE and IMEP at different lambda values. The figure is a bar chart with lambda values on the x-axis (1.8, 1.6, 1.4, 1.2, 1). The left y-axis is ITE (%) and the right y-axis is IMEP (MPa). ITE is represented by red bars and IMEP by blue bars. The values for ITE are 35.3, 37.6, 36.8, 31.3, and 24.9 respectively. The values for IMEP are 0.527, 0.625, 0.681, 0.656, and 0.596 respectively.

Fig. 9. Comparison of the ITE and IMEP at different  $\lambda$ .![Figure 10: Evolution profiles of NOx at different lambda values. The figure is a line graph with crank angle (°CA) on the x-axis (-25 to 125) and mass fraction of NOx on the y-axis (0.000 to 0.014). Five curves represent different lambda values: 1.8 (black), 1.6 (red), 1.4 (blue), 1.2 (green), and 1.0 (purple). The curves show the peak NOx mass fraction occurring at different crank angles, with higher lambda values generally corresponding to higher NOx mass fractions and earlier peak timing.](023b142f90e1253702ac88b18380d3ec_img.jpg)

Figure 10: Evolution profiles of NOx at different lambda values. The figure is a line graph with crank angle (°CA) on the x-axis (-25 to 125) and mass fraction of NOx on the y-axis (0.000 to 0.014). Five curves represent different lambda values: 1.8 (black), 1.6 (red), 1.4 (blue), 1.2 (green), and 1.0 (purple). The curves show the peak NOx mass fraction occurring at different crank angles, with higher lambda values generally corresponding to higher NOx mass fractions and earlier peak timing.

Fig. 10. Evolution profiles of  $\text{NO}_x$  at different  $\lambda$ .

still rises first and then undergoes a rapid decline. The decline being more significant at lower  $\lambda$  values and higher mixture concentrations. After 50 °CA ATDC, the NO<sub>x</sub> content at  $\lambda = 1.2$  is lower than that at  $\lambda = 1.4$ , eventually remains stable. The same conclusion can also be drawn from the NO<sub>x</sub> distribution contour in the cylinder. Given that NO<sub>x</sub> mainly consists of NO, with only a small portion of NO<sub>2</sub> and N<sub>2</sub>O [57]. Fig. 11 shows the distribution of NO in the cylinder after ignition under different  $\lambda$  conditions. At  $\lambda = 1.8$ , NO begins to generate at 10 °CA ATDC, with its quantity gradually increasing with combustion progresses and the high concentration of NO is primarily distributed in area of higher temperature near the flame front. Until 100 °CA ATDC, NO almost pervades the whole area of the cylinder space, maintaining a stable quantity. A comparison of NO distribution contours at  $\lambda = 1.4$  and  $\lambda = 1.0$  shows that faster rate of NO formation at  $\lambda$  is 1.0, filling the whole combustion chamber by 10 °CA ATDC. However, a noticeable decrease in NO levels follows, especially in the front and middle sections of the combustion chamber. This suggests that the reactions leading to the decrease of NO predominantly occurs in area of intense combustion.

During the combustion of NH<sub>3</sub> and H<sub>2</sub> mixed fuels, the abundance of N radicals supplied by NH<sub>3</sub> facilitates the formation of NO<sub>x</sub>, predominantly as fuel-type NO<sub>x</sub>, which primarily consisting of NO. To explain the reason for the above trend, an analysis of the NO generation pathway is subsequently conducted. Initially, NH<sub>3</sub> undergoes dehydrogenation reactions (R1-R5) to generate NH<sub>2</sub> within the cylinder. Then NH<sub>2</sub> reacts with oxygen-containing species such as OH and O to produce NH and HNO (R6, R7), which are key precursors for the generation of NO. On the one hand, NH can continue to dehydrogenation reactions (R8, R9) with O, O<sub>2</sub> to generate NO. On the other hand, HNO can form NO either through the thermal decomposition or the reactions (R10-R12) with H and OH. At higher  $\lambda$ , the O content is higher, and the process of NH<sub>3</sub> dehydrogenation is mainly dominated by the oxygen-containing radical OH. As the  $\lambda$  decrease, the combustion of the fuel becomes more complete, enhancing the rate of OH radical generation. This, in turn, promotes the production of NH<sub>2</sub> and its subsequent oxidation to NH and HNO, leading to significant NO formation.

When  $\lambda$  decreases to below 1.2, the generation of NO is reduced by the influence of fuel-NO pathway, and increased by the influence of thermal-NO pathway. The concentration of N and H radicals increases and the O component decreases in the mixture. The increase of H radical

and coupled with their stronger diffusion effect gradually replacing the role of OH radicals. The initial increase and subsequent decrease in NO production can be attributed to three main factors:

1. The increase in N radical leads to the direct oxidation of NH<sub>2</sub> to N<sub>2</sub>, resulting in a decrease in the amount of NH<sub>2</sub> that can provide key radicals for the NO<sub>x</sub> production. This reduction leads to a decrease in the amount of NO generation.
2. The increase of H radical can promote the conversion of NH<sub>2</sub> to NNH, subsequently oxidizing to N<sub>2</sub> and preventing the generation of NO. On the other hand, it can enhance the transformation of NH<sub>2</sub> to NH. The NH is a crucial intermediate that undergo post-oxidation with NO at the end, thereby reducing the content of NO.
3. The reduction in O<sub>2</sub> and O atoms inhibits the forward progression of oxidation reactions (R7-R9), resulting in a significant reduction in the relative flux of HNO. NH is unlikely to oxidize to form NO at this time.

When  $\lambda = 1.0$ , the generation of NO<sub>x</sub> initially increases and then decreases, which is predominantly influenced by post-oxidation [58]. The concentration of NH<sub>i</sub> components continually rises, leading to intense post-oxidation in the burned zone, predominantly governed by temperature. More complete combustion releases a significant amount of heat at  $\lambda = 1.0$ , elevating the temperature sufficiently to intensify the post-oxidation. Consequently, NO is consumed in this process, resulting in a decrease in NO<sub>x</sub> concentration.

![](b786c4df74397a77344802fd8425a260_img.jpg)

$$\text{NH}_3 + \text{OH} \rightleftharpoons \text{NH}_2 + \text{H}_2\text{O} \quad (\text{R1})$$

![](15de2e86149a9e72f4dad2a3b54eb59d_img.jpg)

$$\text{NH}_3 + \text{H} \rightleftharpoons \text{NH}_2 + \text{H}_2 \quad (\text{R2})$$

![](ee122f3017955603a456009c8ea953b8_img.jpg)

$$\text{NH}_3 + \text{O} \rightleftharpoons \text{NH}_2 + \text{OH} \quad (\text{R3})$$

![](45b2eaa89af6addfe5ecaf7b94549b4e_img.jpg)

$$\text{NH}_3 + \text{O}_2 \rightleftharpoons \text{NH}_2 + \text{HO}_2 \quad (\text{R4})$$

![](6e3b7ec25eaf67a6ca6438dd7216bd24_img.jpg)

$$\text{NH}_3 + \text{HO}_2 \rightleftharpoons \text{NH}_2 + \text{H}_2\text{O}_2 \quad (\text{R5})$$

![](e4a63568c613e6b509936be7a284a78f_img.jpg)

$$\text{NH}_2 + \text{OH} \rightleftharpoons \text{NH} + \text{H}_2\text{O} \quad (\text{R6})$$

![](f6e63d1e60d17cf49914fd1691e87d2d_img.jpg)

$$\text{NH}_2 + \text{O} \rightleftharpoons \text{HNO} + \text{H} \quad (\text{R7})$$

![](63f36d888aab6164c70335ccc4f42e08_img.jpg)

$$\text{NH} + \text{O} \rightleftharpoons \text{NO} + \text{H} \quad (\text{R8})$$

![Figure 11: Comparison of NO distribution at different lambda. The figure is a 4x4 grid of contour plots showing the mass fraction of NO in a combustion chamber at four crank angles (10°CA ATDC, 30°CA ATDC, 50°CA ATDC, 100°CA ATDC) for four equivalence ratios (lambda = 1.8, 1.6, 1.4, 1.2, 1.0). The color scale for mass fraction of NO ranges from 0 (blue) to 0.006 (red). The plots show that NO distribution is more uniform and higher at lambda = 1.0 compared to higher lambda values. A color bar on the right indicates the mass fraction of NO from 0 to 0.006. An arrow at the bottom indicates the rotor rotating direction.](d6dce9b1cbed572f4183e3090cfdbd34_img.jpg)

Figure 11: Comparison of NO distribution at different lambda. The figure is a 4x4 grid of contour plots showing the mass fraction of NO in a combustion chamber at four crank angles (10°CA ATDC, 30°CA ATDC, 50°CA ATDC, 100°CA ATDC) for four equivalence ratios (lambda = 1.8, 1.6, 1.4, 1.2, 1.0). The color scale for mass fraction of NO ranges from 0 (blue) to 0.006 (red). The plots show that NO distribution is more uniform and higher at lambda = 1.0 compared to higher lambda values. A color bar on the right indicates the mass fraction of NO from 0 to 0.006. An arrow at the bottom indicates the rotor rotating direction.

Fig. 11. Comparison of NO distribution at different  $\lambda$ .

![](aec74fefb14e3d01662a703e5db4bad3_img.jpg)

$$\text{NH} + \text{O}_2 \rightleftharpoons \text{NO} + \text{OH} \quad (\text{R9})$$

![](67b64a213d4be0daaaadf4e8295dd59e_img.jpg)

$$\text{HNO} \rightleftharpoons \text{NO} + \text{H} \quad (\text{R10})$$

![](49f91568da0ec0096075117b1fef3e85_img.jpg)

$$\text{HNO} + \text{H} \rightleftharpoons \text{NO} + \text{H}_2 \quad (\text{R11})$$

![](ce2ad4bdbdde5c7767950a4fec9ddd68_img.jpg)

$$\text{NH}_3 + \text{OH} \rightleftharpoons \text{NH}_2 + \text{H}_2\text{O} \quad (\text{R12})$$

### 3.2. Effect of the ignition timing

The IT plays crucial role in combustion and heat release. To enhance the output power and thermal efficiency of the WRE, IT is optimized at  $\lambda = 1.4$  to investigate the effects on the combustion, performance and emission of the WRE based on the analysis in the above chapters. Fig. 12 shows the in-cylinder pressure and the HRR under different ITs. With the advancement of IT, there is a corresponding advancement in the combustion phase, leading to a rapid increase in-cylinder pressure and an earlier crank angle relative to the peak cylinder pressure. Meanwhile, the peak HRR rises continuously and the corresponding crank angle shifts forward. However, the peak HRR declines when IT is advanced to  $-10^\circ\text{CA ATDC}$ , which is attributed to an excessively early IT, the lower pressure and temperature create an unfavorable thermal environment for the rapid combustion and heat release of the mixture. Fig. 13 shows the significant impact of the IT on flame propagation. The flame propagation contour at  $10^\circ\text{CA}$  after ignition is all hemispherical shape. However, delaying the IT leads to a gradual reduction in the radius of the flame profile, especially when IT is  $10^\circ\text{CA ATDC}$ , the flame propagation area at the LSP markedly narrows. At IT is  $-5^\circ\text{CA ATDC}$ , the flame propagates most rapidly, with the flame front reaching the cylinder wall of the combustion chamber  $20^\circ\text{CA}$  after ignition, and subsequently spreading further forward.

Fig. 14 (a) shows the pressure-volume curves at different ITs, which is an important index to respond to the work capacity and combustion efficiency of internal combustion engine. When IT is advanced to  $-10^\circ\text{CA ATDC}$ , early ignition leads to a rapid increase in cylinder pressure. However, due to the advanced combustion, the trend of decreasing the pressure in cylinder also in advance, resulting in smaller integral area compared to IT of  $-5^\circ\text{CA ATDC}$ . When IT =  $10^\circ\text{CA ATDC}$ , which occurs later than TDC, there is a period of cylinder pressure decreasing tendency with volume increase after TDC. This results in the minimal area within the pressure-volume diagram under this condition. The magnitude of the indicated work is directly related to ITE and IMEP. Fig. 14 (b) represents the variation of ITE and IMEP at different ITs. It is observed that they initially increase and then decrease with the IT is delayed,

exhibiting optimal performance at IT =  $-5^\circ\text{CA ATDC}$ , with the ITE reaches 36.9% and IMEP attains 0.683 MPa. Fig. 15 displays the evolution profiles of NOx at different ITs. The trend of NOx formation is generally consistent under different IT conditions, but a relative slowdown in NOx formation is observed at IT is  $10^\circ\text{CA ATDC}$ . Fig. 16 shows NO distribution contour in the cylinder. At  $50^\circ\text{CA ATDC}$ , NO distribution has not yet spread throughout the entire cylinder under IT is  $10^\circ\text{CA ATDC}$ . This phenomenon is mainly related to the thermal environment within the cylinder. The generation of NO is directly proportional to the temperature in the combustion chamber. The delay of IT is not conducive to the oxidation of  $\text{NH}_2$  to form HNO, thereby inhibiting the generation of NO.

## 4. Conclusions

This study investigated the turbulent combustion and emission characteristics of the ammonia-hydrogen WRE through numerical simulations, with  $\alpha_{\text{NH}_3}$  of 10%. The performance of the WRE based on the mixture gas concentration and IT was evaluated. The main conclusions are as follows:

1. Using ammonia in the hydrogen-fueled WRE significantly prevent the issue of abnormal combustion, enhancing power and thermal efficiency. The simulation results show that adding 10% volume fraction of ammonia into the hydrogen-fueled rotary engine can ensure stable operation at  $\lambda$  of 1.4, and improve power and thermal efficiency. In the ammonia-hydrogen WRE, as  $\lambda$  decreases, results in the increase in the gas flow velocity within the combustion chamber. The propagation and development of the flame are influenced by the flow field and temperature. Decreasing  $\lambda$  stabilizes initial flame kernel formation and accelerates flame propagation, leading to in-cylinder pressure and HRR increased, with the peak corresponding crank angle advancing. However, the impact of  $\lambda$  on the performance of the WRE does not follow a monotonic linear trend. Under the current ammonia-hydrogen mixture ratio, the optimal performance of the WRE can be achieved at  $\lambda = 1.4$ . Compared to  $\lambda = 1.8$ , the ITE can reach up to 36.8% (a 4.2% increase) and the IMEP to 0.681 MPa (a 29.2% increase).
2. At  $\lambda = 1.4$ , altering the IT significantly impacts the flame kernel formation and flame propagation. With the advancement of IT, the peak cylinder pressure initially increases and then decreases, potentially enhancing the IMEP and ITE. It is found that under the current working conditions, an optimal IT of  $-5^\circ\text{CA ATDC}$ . Compared to the original IT, the ITE increases to 36.9% and the IMEP to 0.683 MPa.

![Figure 12: In-cylinder pressure and HRR profiles at different ITs. (a) In-cylinder pressure (MPa) vs Crank angle (°CA). (b) HRR (J/°CA) vs Crank angle (°CA). Both plots show curves for IT = -10°CA ATDC, -5°CA ATDC, TDC, 5°CA ATDC, and 10°CA ATDC.](8f93234090c5bc224e4b9d035018a927_img.jpg)

Figure 12 consists of two subplots. Subplot (a) shows the in-cylinder pressure (MPa) on the y-axis (0 to 5) versus the crank angle (°CA) on the x-axis (-75 to 150). Five curves represent different ignition timings (IT): -10°CA ATDC (black), -5°CA ATDC (red), TDC (blue), 5°CA ATDC (green), and 10°CA ATDC (purple). The curves show a peak pressure that shifts to earlier crank angles as IT advances. Subplot (b) shows the heat release rate (HRR) in J/°CA on the y-axis (0 to 120) versus the crank angle (°CA) on the x-axis (-50 to 100). The same five ITs are plotted, showing that the peak HRR increases and shifts to earlier crank angles as IT advances, with the peak HRR being highest for -5°CA ATDC.

Figure 12: In-cylinder pressure and HRR profiles at different ITs. (a) In-cylinder pressure (MPa) vs Crank angle (°CA). (b) HRR (J/°CA) vs Crank angle (°CA). Both plots show curves for IT = -10°CA ATDC, -5°CA ATDC, TDC, 5°CA ATDC, and 10°CA ATDC.

Fig. 12. In-cylinder pressure and HRR profiles at different ITs.

![Figure 13: Comparison of flame propagation at different Intake Timings (ITs). The figure is a 5x5 grid of flame propagation maps. The columns represent ITs: 5°CA AIT, 10°CA AIT, 15°CA AIT, 20°CA AIT, and 25°CA AIT. The rows represent different ITs: IT = -10°CA ATDC, IT = -5°CA ATDC, IT = TDC, IT = 5°CA ATDC, and IT = 10°CA ATDC. A color bar on the right indicates velocity in m/s, ranging from 0 (blue) to 40 (dark blue). A black arrow at the bottom indicates the rotor rotating direction.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 13: Comparison of flame propagation at different Intake Timings (ITs). The figure is a 5x5 grid of flame propagation maps. The columns represent ITs: 5°CA AIT, 10°CA AIT, 15°CA AIT, 20°CA AIT, and 25°CA AIT. The rows represent different ITs: IT = -10°CA ATDC, IT = -5°CA ATDC, IT = TDC, IT = 5°CA ATDC, and IT = 10°CA ATDC. A color bar on the right indicates velocity in m/s, ranging from 0 (blue) to 40 (dark blue). A black arrow at the bottom indicates the rotor rotating direction.

Fig. 13. Comparison of flame propagation at different ITs.

![Figure 14: Comparison of work capacity curves at different ITs. (a) In-cylinder pressure (MPa) vs. Volume × 10³ (m³). (b) Indicated Thermal Efficiency (ITE) (%) and Indicated Mean Effective Pressure (IMEP) (MPa) vs. IT (°CA ATDC).](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 14 consists of two subplots. Subplot (a) shows the in-cylinder pressure (MPa) on the y-axis (0 to 5) versus the volume  $\times 10^3$  (m³) on the x-axis (0.0 to 0.7). Five curves represent different intake timings: IT = -10°CA ATDC (black), IT = -5°CA ATDC (red), IT = TDC (blue), IT = 5°CA ATDC (green), and IT = 10°CA ATDC (purple). Subplot (b) shows ITE (%) on the left y-axis (35.5 to 38.0) and IMEP (MPa) on the right y-axis (0.65 to 0.69) versus IT (°CA ATDC) on the x-axis (-10 to 10). ITE is represented by blue stars and IMEP by red triangles.

Figure 14: Comparison of work capacity curves at different ITs. (a) In-cylinder pressure (MPa) vs. Volume × 10³ (m³). (b) Indicated Thermal Efficiency (ITE) (%) and Indicated Mean Effective Pressure (IMEP) (MPa) vs. IT (°CA ATDC).

Fig. 14. Comparison of work capacity curves at different ITs.

![Figure 15: Evolution profiles of NOx at different ITs. The plot shows the mass fraction of NOx on the y-axis (0.000 to 0.012) versus crank angle (°CA) on the x-axis (-50 to 125). Five curves represent ITs: IT = -10°CA ATDC (black), IT = -5°CA ATDC (red), IT = TDC (blue), IT = 5°CA ATDC (green), and IT = 10°CA ATDC (purple). An inset shows a zoomed-in view of the NOx mass fraction between 0.006 and 0.012 for crank angles between 25 and 75 °CA.](33228b4227fa57e1477b27b9e07483e6_img.jpg)

Figure 15: Evolution profiles of NOx at different ITs. The plot shows the mass fraction of NOx on the y-axis (0.000 to 0.012) versus crank angle (°CA) on the x-axis (-50 to 125). Five curves represent ITs: IT = -10°CA ATDC (black), IT = -5°CA ATDC (red), IT = TDC (blue), IT = 5°CA ATDC (green), and IT = 10°CA ATDC (purple). An inset shows a zoomed-in view of the NOx mass fraction between 0.006 and 0.012 for crank angles between 25 and 75 °CA.

Fig. 15. Evolution profiles of NO<sub>x</sub> at different ITs.

3. The generation of NO<sub>x</sub> is significantly influenced by variations in  $\lambda$ , with a reduction of  $\lambda$  leading to an increase in NO<sub>x</sub> production. However, when  $\lambda \le 1.2$ , the NO<sub>x</sub> variation exhibits an initial increase followed by a decrease. It is primarily due to the dominance of N and H atoms in reaction and the effect of post-oxidation. Different ITs mainly affect the sequence of NO<sub>x</sub> formation rather than its total amount. However, delayed IT results in lower cylinder pressures and temperatures, which can partially inhibit the forward progression of  $\text{NH}_2 + \text{O} = \text{HNO} + \text{H}$ , thereby reducing NO production.

In this work, the influence of excess air coefficient on the turbulent combustion characteristics of ammonia hydrogen rotary engine was revealed through numerical simulation, and higher power performance was achieved through early ignition. Future efforts will focus on optimizing intake methods and reducing NO<sub>x</sub> emissions.

## CRediT authorship contribution statement

**Shuofeng Wang:** Supervision, Resources, Funding acquisition. **Yu Sun:** Writing – review & editing, Writing – original draft, Methodology, Investigation, Conceptualization. **Jinxin Yang:** Supervision, Conceptualization. **Huaiyu Wang:** Software, Methodology, Formal analysis.



![Figure 16: Comparison of NO distribution at different ITs. The figure is a 5x4 grid of heatmaps showing NO mass fraction in a Wankel engine combustion chamber at five different intake timings (ITs): 10°CA ATDC, 30°CA ATDC, 50°CA ATDC, 100°CA ATDC, and IT=10°CA ATDC. The columns represent ITs, and the rows represent different ITs. A color bar on the right indicates the mass fraction of NO from 0 to 0.006. The rotor rotating direction is indicated by an arrow at the bottom. The NO distribution is highest (red) near the combustion chamber walls and lowest (blue) in the center, with the distribution shifting as the IT changes.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 16: Comparison of NO distribution at different ITs. The figure is a 5x4 grid of heatmaps showing NO mass fraction in a Wankel engine combustion chamber at five different intake timings (ITs): 10°CA ATDC, 30°CA ATDC, 50°CA ATDC, 100°CA ATDC, and IT=10°CA ATDC. The columns represent ITs, and the rows represent different ITs. A color bar on the right indicates the mass fraction of NO from 0 to 0.006. The rotor rotating direction is indicated by an arrow at the bottom. The NO distribution is highest (red) near the combustion chamber walls and lowest (blue) in the center, with the distribution shifting as the IT changes.

Fig. 16. Comparison of NO distribution at different ITs.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Data availability

Data will be made available on request.

# Acknowledgments

This work was financially supported by the National Natural Science Foundation of China (No. 52276097), and the “JBGS” Project of Inner Mongolia Autonomous Region, China (No. 2022JBGS0008).

# References

- [1] Woon KS, Phuang ZX, Taler J, Varbanov PS, Chong CT, Klemeš JJ, et al. Recent advances in urban green energy development towards carbon emissions neutrality. *Energy* 2023;267:126502.
- [2] Yang X, Liu J, Li M. Transportation energy consumption decreases despite urban sprawl: evidence from Chinese household survey. *Cities* 2024;146:104738.
- [3] Feng X, Zhao Y, Yan R. Does carbon emission trading policy has emission reduction effect?—An empirical study based on quasi-natural experiment method. *J Environ Manag* 2024;351:119791.
- [4] Kim M, Won W, Kim J. Integration of carbon capture and sequestration and renewable resource technologies for sustainable energy supply in the transportation sector. *Energy Convers Manag* 2017;143:227–40.
- [5] Lin Z, Liu S, Qi Y, Chen Q, Wang Z. Experimental study on the performance of a high compression ratio SI engine using alcohol/ammonia fuel. *Energy* 2024;289:129998.
- [6] Tan Y, Kou C, E J, Feng C, Han D. Effect of different exhaust parameters on conversion efficiency enhancement of a Pd-Rh three-way catalytic converter for heavy-duty natural gas engines. *Energy* 2024;292:130483.
- [7] Kakoe A, Bakshan Y, Gharehghani A, Salahi MM. Numerical comparative study of hydrogen addition on combustion and emission characteristics of a natural-gas/dimethyl-ether RCCI engine with pre-chamber. *Energy* 2019;186:115878.
- [8] Alruqi M, Sharma P, Agbulut Ü. Investigations on biomass gasification derived producer gas and algal biodiesel to power a dual-fuel engines: application of neural networks optimized with Bayesian approach and K-cross fold. *Energy* 2023;282:128336.
- [9] Bao J, Qu P, Wang H, Zhou C, Zhang L, Shi C. Implementation of various bowl designs in an HPDI natural gas engine focused on performance and pollutant emissions. *Chemosphere* 2022;303:135275.
- [10] Shen X, Shen J, Liu H, Wen JX, Ma Y, Zou X, et al. Numerical investigation on dynamic behavior of premixed hydrogen/air flame propagation in a closed tube. *Fuel* 2023;354:129295.
- [11] Shi C, Chai S, Di L, Ji C, Ge Y, Wang H. Combined experimental-numerical analysis of hydrogen as a combustion enhancer applied to wankel engine. *Energy* 2023;263:125896.
- [12] Duan Y, Sun B, Li Q, Wu X, Hu T, Luo Q. Combustion characteristics of a turbocharged direct-injection hydrogen engine. *Energy Convers Manag* 2023;291:117267.
- [13] Sun Z, Li G. Propagation characteristics of laminar spherical flames within homogeneous hydrogen-air mixtures. *Energy* 2016;116:116–27.
- [14] Chang K, Ji C, Wang S, Yang J, Meng H, Wang H, et al. Comparative study on different spark plug positions of a rotary engine with gasoline port and direct injection. *Fuel* 2022;310:122376.
- [15] Meng H, Ji C, Wang S, Yang J. A review: centurial progress and development of Wankel rotary engine. *Fuel* 2023;335:127043.
- [16] Wang H, Ji C, Shi C, Yang J, Ge Y, Wang S, et al. Parametric modeling and optimization of the intake and exhaust phases of a hydrogen Wankel rotary engine using parallel computing optimization platform. *Fuel* 2022;324:124381.
- [17] Shi C, Chai S, Wang H, Ji C, Ge Y, Di L. An insight into direct water injection applied on the hydrogen-enriched rotary engine. *Fuel* 2023;339:127352.
- [18] Su T, Ji C, Wang S, Shi L, Yang J, Cong X. Idle performance of a hydrogen rotary engine at different excess air ratios. *Int J Hydrogen Energy* 2018;43:2443–51.
- [19] Su T, Ji C, Wang S, Cong X, Shi L. Research on performance of a hydrogen/n-butanol rotary engine at idling and varied excess air ratios. *Energy Convers Manag* 2018;162:132–8.
- [20] Meng H, Ji C, Yang J, Wang S, Gao C, Shen X, et al. Assessment of the application of oxygen enrichment in the hydrogen-fueled Wankel rotary engine. *Fuel* 2023;341:127732.
- [21] Chen W, Yu S, Zuo Q, Zhu G, Zhang B, Yang X. Combined effect of air intake method and hydrogen injection timing on airflow movement and mixture formation in a hydrogen direct injection rotary engine. *Int J Hydrogen Energy* 2022;47:12739–58.
- [22] Yang J, Ji C, Wang S, Meng H. An experimental study on ignition timing of hydrogen Wankel rotary engine. *Int J Hydrogen Energy* 2022;47:17468–78.
- [23] Shi C, Ji C, Ge Y, Wang S, Wang H, Yang J. Parametric analysis of hydrogen two-stage direct-injection on combustion characteristics, knock propensity, and emissions formation in a rotary engine. *Fuel* 2021;287:1119418.
- [24] Zou R, Liu J, Jiao H, Wang N, Zhao J. Numerical study on auto-ignition development and knocking characteristics of a downsized rotary engine under different inlet pressures. *Fuel* 2022;309:122046.
- [25] Wang H, Ji C, Shi C, Wang S, Yang J, Ge Y. Investigation of the gas injection rate shape on combustion, knock and emissions behavior of a rotary engine with hydrogen direct-injection enrichment. *Int J Hydrogen Energy* 2021;46:14790–804.
- [26] Meng H, Ji C, Xin G, Yang J, Chang K, Wang S. Comparison of combustion, emission and abnormal combustion of hydrogen-fueled Wankel rotary engine and reciprocating piston engine. *Fuel* 2022;318:123675.
- [27] Meng H, Ji C, Yang J, Xin G, Wang S. Statistically discussing impacts of knock type on the heat release process in hydrogen-fueled Wankel rotary engine. *Int J Hydrogen Energy* 2023;48:7927–37.

- [28] Szwaja S. Dilution of fresh charge for reducing combustion knock in the internal combustion engine fueled with hydrogen rich gases. *Int J Hydrogen Energy* 2019; 44:19017–25.
- [29] Shah ZA, Mehdi G, Congedo PM, Mazzeo D, De Giorgi MG. A review of recent studies and emerging trends in plasma-assisted combustion of ammonia as an effective hydrogen carrier. *Int J Hydrogen Energy* 2024;51:354–74.
- [30] Lhuillier C, Brequigny P, Contino F, Mounaim-Rousselle C. Experimental investigation on ammonia combustion behavior in a spark-ignition engine by means of laminar and turbulent expanding flames. *Proc Combust Inst* 2021;38: 5859–68.
- [31] Liu S, Lin Z, Zhang H, Lei N, Qi Y, Wang Z. Impact of ammonia addition on knock resistance and combustion performance in a gasoline engine with high compression ratio. *Energy* 2023;262:125458.
- [32] Wei W, Li G, Zhang Z, Long Y, Zhang H, Huang Y, et al. Effects of ammonia addition on the performance and emissions for a spark-ignition marine natural gas engine. *Energy* 2023;272:127092.
- [33] Qi Y, Liu W, Liu S, Wang W, Peng Y, Wang Z. A review on ammonia-hydrogen fueled internal combustion engines. *Transportation* 2023;18:100288.
- [34] Hong C, Ji C, Wang S, Xin G, Qiang Y, Liu Q. A comprehensive experimental study to analyze the cyclic variation of a hydrogen-blended ammonia engine with the Miller cycle. *Int J Hydrogen Energy* 2024;55:1335–46.
- [35] Dinesh MH, Pandey JK, Kumar GN. Study of performance, combustion, and NOx emission behavior of an SI engine fueled with ammonia/hydrogen blends at various compression ratio. *Int J Hydrogen Energy* 2022;47:25391–403.
- [36] Dinesh MH, Kumar GN. Experimental investigation of variable compression ratio and ignition timing effects on performance, combustion, and NOx emission of ammonia/hydrogen-fuelled SI engine. *Int J Hydrogen Energy* 2023;48:35139–52.
- [37] Xin G, Ji C, Wang S, Hong C, Meng H, Yang J. Experimental study on the effect of hydrogen substitution rate on combustion and emission characteristics of ammonia internal combustion engine under different excess air ratio. *Fuel* 2023;343:127992.
- [38] Xin G, Ji C, Wang S, Meng H, Chang K, Yang J. Effect of ammonia addition on combustion and emission characteristics of hydrogen-fueled engine under lean-burn condition. *Int J Hydrogen Energy* 2022;47:9762–74.
- [39] Yu X, Li Y, Zhang J, Guo Z, Du Y, Li D, et al. Effects of hydrogen blending ratio on combustion and emission characteristics of an ammonia/hydrogen compound injection engine under different excess air coefficients. *Int J Hydrogen Energy* 2024;49:1033–47.
- [40] Wang H, Ji C, Wang D, Wang Z, Yang J, Meng H, et al. Investigation on the potential of using carbon-free ammonia and hydrogen in small-scaled Wankel rotary engines. *Energy* 2023;283:129166.
- [41] Hong C, Ji C, Wang S, Xin G, Meng H, Yang J, et al. An experimental study of a strategy to improve the combustion process of a hydrogen-blended ammonia engine under lean and WOT conditions. *Int J Hydrogen Energy* 2023;48:33719–31.
- [42] Liu Z, Zhang Z, Rao S, Zheng Z. Study of water injection on suppressing knock in a high compression ratio and supercharged hybrid gasoline engine. *Energy* 2024; 287:129702.
- [43] Liang B, Cheng L, Zhang M, Huang Y, Wang J, Liu Y, et al. Effects of chamber geometry, hydrogen ratio and EGR ratio on the combustion process and knocking characters of a HCNG engine at the stoichiometric condition. *Applications in Energy and Combustion Science* 2023;15:100189.
- [44] Chen L, Wei H, Chen C, Feng D, Zhou L, Pan J. Numerical investigations on the effects of turbulence intensity on knocking combustion in a downsized gasoline engine. *Energy (Oxford)* 2019;166:318–25.
- [45] Liu S, Lin Z, Zhang H, Lei N, Qi Y, Wang Z. Impact of ammonia addition on knock resistance and combustion performance in a gasoline engine with high compression ratio. *Energy* 2023;262:125458.
- [46] Ji C, Chang K, Wang S, Yang J, Wang D, Meng H, et al. Effect of injection strategy on the mixture formation and combustion process in a gasoline direct injection rotary engine. *Fuel* 2021;304:121428.
- [47] Gao J, Zhang H, Li J, Wang Y, Tian G, Ma C, et al. Simulation on the effect of compression ratios on the performance of a hydrogen fueled opposed rotary piston engine. *Renew Energy* 2022;187:428–39.
- [48] Yang Z, Ji C, Yang J, Wang H, Huang X, Wang S. The optimization of leading spark plug location and its influences on combustion and leakage in a hydrogen-fueled Wankel rotary engine. *Int J Hydrogen Energy* 2023;48:20465–82.
- [49] Zhang M, Shen Y. Three-dimensional simulation of meandering river based on 3-D RNG k- $\epsilon$  turbulence model. *J Hydrodyn Series B* 2008;20:448–55.
- [50] Ji C, Qiang Y, Wang S, Xin G, Wang Z, Hong C, et al. Numerical investigation on the combustion performance of ammonia-hydrogen spark-ignition engine under various high compression ratios and different spark-ignition timings. *Int J Hydrogen Energy* 2024;56:817–27.
- [51] Zhang X, Moosakutty SP, Rajan RP, Younes M, Sarathy SM. Combustion chemistry of ammonia/hydrogen mixtures: jet-stirred reactor measurements and comprehensive kinetic modeling. *Combust Flame* 2021;234:111653.
- [52] Meng H, Ji C, Yang J, Wang H, Wang Z, Zambalov S, et al. Performance analysis of the ammonia-enriched hydrogen-fueled Wankel rotary engine. *Int J Hydrogen Energy* 2024;49:462–72.
- [53] Ji C, Xin G, Wang S, Cong X, Meng H, Chang K, et al. Effect of ammonia addition on combustion and emissions performance of a hydrogen engine at part load and stoichiometric conditions. *Int J Hydrogen Energy* 2021;46:40143–53.
- [54] Shi C, Ji C, Wang S, Yang J, Ma Z, Ge Y. Combined influence of hydrogen direct-injection pressure and nozzle diameter on lean combustion in a spark-ignited rotary engine. *Energy Convers Manag* 2019;195:1124–37.
- [55] Gong C, Li Z, Yi L, Huang K, Liu F. Research on the performance of a hydrogen/methanol dual-injection assisted spark-ignition engine using late-injection strategy for methanol. *Fuel* 2020;260:116403.
- [56] Prasada Rao G, Sathya Vara Prasad L. Combined influence of compression ratio and exhaust gas recirculation on the diverse characteristics of the diesel engine fueled with novel palmira biodiesel blend. *Energy Convers Manag X* 2022;14:100185.
- [57] Zhu Y, Curran HJ, Girhe S, Murakami Y, Pitsch H, Senecal K, et al. The combustion chemistry of ammonia and ammonia/hydrogen mixtures: a comprehensive chemical kinetic modeling study. *Combust Flame* 2024;260:113239.
- [58] Wang D, Ji C, Wang S, Yang J, Wang Z. Numerical study of the premixed ammonia-hydrogen combustion under engine-relevant conditions. *Int J Hydrogen Energy* 2021;46:2667–83.