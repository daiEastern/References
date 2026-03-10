Investigation of intake closing timing on the flow field and combustion process in a small-scaled Wankel rotary engine under various engine speeds designed for the UAV application

Jinxin Yang

College of Energy and Power Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

Huaiyu Wang

College of Energy and Power Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

Changwei Ji

College of Energy and Power Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

Ke Chang

College of Energy and Power Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

Shuofeng Wang

College of Energy and Power Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, PR China

###### Abstract

This paper aims to reveal the effect of intake closing timing, and engine speed on the flow field, flame propagation, combustion characteristics, and emissions formations of a small-scaled side ported hydrogen-fueled Wankel rotary engine. For this reason, a three-dimensional dynamic simulation model was established using a reasonable turbulent model coupled with a kinetic reaction mechanism and validated by the experimental data. Simulation results show that an earlier intake closing timing increases the volumetric efficiency and increases intake loss. The increasing speed improves the volumetric efficiency while causing a higher intake loss. There are two peaks of the turbulence kinetic energy during the intake stroke. The first one is caused by the airflow hitting the wall, and the other is due to the backflow. During the flame development period, due to the strong unidirectional flow in the combustion chamber, which is not conducive to flame propagation backward. This phenomenon is more pronounced at higher engine speeds, resulting in a merged flame front not exceeding the trailing spark plug. The lean combustion leads to a lower in-cylinder combustion temperature, deteriorating the NOx generation environment. This paper provides a feasible method for matching the operating conditions and intake system.

## 1 Introduction

With the characteristics of high power-to-weight ratio [1], compact design [2], multi-fuel capability [3], and NVH (noise, vibration, and harshness) [4], the Wankel rotary engines (WREs) are more suitable for the application of range extender engine for range extend electric vehicle when compared to reciprocating piston engines (RPEs) [5]. Moreover, these advantages make it widespread in unmanned aerial vehicle (UAV) [6], compressor [7], expander [8], and pump [9]. However, the WREs also suffer the leakage [10] and sealing [11] problems, high pollution emissions [12], and weak fuel economy [13]. Especially, due to the interior property of the narrow and long chamber near the top dead center, the flow field in the chamber is unidirectional flow [14], which deteriorates the flame propagation from the leading to the trailing side [15]. The unburned air-fuel mixture at the rear of the combustion chamber increases incomplete combustion and therefore exacerbates the thermal efficiency and pollution emissions [16]. Consequently, the primary point for optimization of the thermal efficiency and pollution emissions is to promote the flame propagation [17]. Many technologies have been applicated to WREs to enhance thermal efficiency and improve pollution emissions [18].

Hydrogen is an ideal alternative fuel and has been widely used in RPEs [19, 20] and WREs [21, 22]. Unlike other fossil fuels, hydrogen is a zero-carbon secondary energy source, which contributes to the goal of emission peak and carbon neutrality [23, 24]. Researchers have achieved significant achievements in hydrogen enrichment WREs [25, 26]. The experiment and simulation result showed that the thermal efficiency, cyclic variation, and fuel consumption be improved by hydrogen enrichment [27]. Furthermore, hydrocarbon and carbon monoxide emissions were also decreased, while nitrogen oxide (NOx) emissions is increased [28]. However, the application of hydrogen enrichment in WRE needs additional fuel supply system, which increases the complexity of the control system [29]. Moreover, hydrogen enrichment technology cannot fully solve the emissions issue. Hence, the pure 

[MISSING_PAGE_EMPTY:2]

hydrogen engines seem to be a feasible solution to achieve the carbon neutrality aims [30]. The limitation of the pure hydrogen-fueled engines is the poor power density because of the low density of the pure hydrogen, which causes a lower specific volume calorific value [31]. In the ideal condition, the power output of the hydrogen port injection RPE is only 82% compared to the gasoline ones [32]. For the hydrogen-fueled WRE, the power output is 63% of gasoline, while it is only 50% for hydrogen-fueled RPE [33]. Therefore, improving power density without sacrificing NOA emissions is the primary goal of hydrogen-fueled engines [34]. Yang et al. [35] compared the effects of leading and trading spark plugs on the combustion stability of hydrogen WRE, and concluded that leading spark plug is beneficial in reducing cyclic variation. Morimoto et al. [33] showed that hydrogen-fueled WRE can operate at a lean condition with an extremely low NOA emissions. In summary, the application of hydrogen in WRE can not only reduce emissions but also improve thermal efficiency.

The intake system impacts the cylinder mass, swirl intensity, gas mixture formation as well as combustion, performance, and emissions [36]. Therefore, the design of a proper intake system design is crucial for the performance improvement of WRE [37]. Zou et al. [38] studied the influence of intake channel angle and chamber structure on flow field

\begin{table}
\begin{tabular}{l c} \hline Specification & Value \\ \hline Displacement [1] & 0.082 \\ Eccentricity [mm] & 7.5 \\ Generating Radius [mm] & 52.5 \\ Width [mm] & 40 \\ Compression ratio & 10.0 \\ Intake open [ATDC] & 3 \(\,\)’EA \\ Intake close [LABG] & 65 \(\,\)’EA \\ Exhaust open [BDBC] & 50 \(\,\)’EA \\ Exhaust close [BITDC] & 3 \(\,\)’EA \\ \hline \end{tabular}
\end{table}
Table 1: Major specifications of the engine.

Figure 1: Summary of the working routine.

Figure 3: Simplified engine geometric model.

Figure 2: Schematic of the WRE [43].

[MISSING_PAGE_EMPTY:4]

and combustion process in a small-scaled WRE. The result showed that the combination of 15\({}^{\circ}\) channel angle and middle baffle resulted in the optimal solution. Jeng et al. [39] concluded that a larger pipe diameter with a converging intake pipe can increase the power output by more than 10%. Turner et al. [40] found that eliminating the intake and exhaust overlap helps reduce HC emissions. Taskiran et al. [41] demonstrated that multiple ports facilitate optimal volumetric efficiency at different speeds. Deng [42] optimlzed a diesel-fueled WRE with response surface and genetic algorithm. Wang et al. [43] studied the performance and emissions trade-off of a hydrogen-fueled WRE using an one dimensional (1-D) simulation model.

The result showed that an early intake closing timing could reduce the gasflow backflow, which resulted a higher in-cylinder mass and power output. Based on this, they optimized the intake and exhaust phases using a parallel computing optimization platform [44, 45]. The studies listed indicate that the intake system is important for increasing the power of the hydrogen-fueled WRE.

In summary, the design of the intake system of hydrogen-fueled WRE is very important, especially for small-scaled engines. In the current study, there is no combination study for small-scaled WRE at different speeds with intake closing timings. This is essential for the determination of the operating parameters of small-scaled WRE in UAVs. Especially for hybrid UAVs, in which the WRE as a power source can output power continuously at a fixed speed [46]. Therefore, in this paper, a three-dimensional kinetic model of a small-scaled WRE coupled with the reaction mechanism is developed and calibrated under experimental conditions. The intake closing timing is varied from the original engine using a developed port phase control model, and calculations are performed at different speeds. Based on this, the optimal match between intake closing timing and speed is explored to provide theoretical guidance for WRE fueled with hydrogen optimization.

## 2 Materials and methods

The summary of the working routine of this paper is shown in Fig. 1. In section 2.1, the designed engine specifications are introduced. The computational domain and boundary conditions are described in section 2.2. Section 2.3 introduces the simulation model and validation method. Section 2.4 describes the research schemes and port diagram.

### Engine specifications

A small-scaled side ported hydrogen-fueled WRE with one intake port, two exhaust port, and two spark plugs are studied in this research. The engine specifications and schematic diagram are illustrated in Table 1 and Fig. 2. In fact, to build a small-scaled model quickly, this model is scaled from Mazda 13B [43]. The displacement of this hydrogen-fueled WRE is about 82 cc, and the compression ratio is 10:1.

\begin{table}
\begin{tabular}{l l l} \hline Region & Type & Value \\ \hline Air inlet & Inflow & 1 bar/300 K \\ Ezhust outlet & Outflow & 1 bar/900 K \\ Rotor & Moving wall & 550 K \\ inlet port & Fixed wall & 300 K \\ Outlet port & Fixed wall & 900 K \\ Housing & Fixed wall & 550 K \\ Spark plug & Fixed wall & 600 K \\ Spark electrode & Fixed wall & 650 K \\ Engine speed & Constant & 3000 rpm \\ Workflow & Fresh air & O2: NZ (0.233: 0.767, mass fraction) \\ Fuel & Hydrogen & \(\lambda=1.8\) \\ \hline \end{tabular}
\end{table}
Table 2: Initial and boundary conditions.

Figure 4: Mesh grid of the hydrogen-fueled WRE.

Figure 5: Model validation for in-cylinder pressure and AHR.

\begin{table}
\begin{tabular}{l l l l} \hline Num. & Case name & ICT/EA & Engine Speed/ppm \\ \hline
1 & 10 \(\times\) R3000 & 0 & 3000 \\
2 & 10 \(\times\) R5000 & 0 & 5000 \\
3 & 10 \(\times\) R8000 & 0 & 8000 \\
4 & 15 \(\times\) R3000 & \(-\)5 & 3000 \\
5 & 15 \(\times\) R5000 & \(-\)5 & 5000 \\
6 & 15 \(\times\) R8000 & \(-\)5 & 8000 \\
7 & 15 \(\times\) R3000 & \(+\)5 & 3000 \\
8 & 15 \(\times\) R5000 & \(+\)5 & 5000 \\
9 & 15\(\times\) R8000 & \(+\)5 & 8000 \\ \hline \end{tabular}
\end{table}
Table 3: Summary of different calculated schemes.

Figure 6: Port shape and area with different ICTs.

Figure 7: Comparison of the velocity distribution and the streamlines.

[MISSING_PAGE_EMPTY:8]

The width, generating radius, and eccentricity is 40, 52.5, and 7.5 mm, respectively.

### Computational domain

In this percent work, a 3-D geometry model of the WRE is built in SolidWorks software. In the numerical calculations, the geometry needs to simplified, as illustrated in Fig. 3, the apex seal is also modeled in the computation [41]. This work mainly concerns about the influence of the intake port shape and timing on the flow field, flame propagation, and combustion process. Due to the change in the intake structure, three cycles are calculated to ensure stability, i.e. 3240 \({}^{\circ}\)EA, and chamber I in the last cycle is used as a reference [37]. The initial and boundary conditions of the hydrogen-fueled WRE for model calibration and calculation is exposed in Table 2. The adequate setting could enhance the calculation accuracy and save calculation time [15]. The initial and boundary conditions are according to the similar CFD model and test conations.

Figure 8: Comparison of the in-cylinder mass.

Figure 9: Comparison of the mean in-cylinder TKE.

[MISSING_PAGE_EMPTY:10]

Figure 11: Comparison of the mass fraction of burned fuel.

Figure 12: Comparison of the flame contours and OH distribution.

Figure 10: Comparison the charge ratio of the intake loss and volumetric efficiency.

[MISSING_PAGE_EMPTY:12]

### Model validation

In order to verify the accuracy of the 3-D CFD model, the original hydrogen-fueled WRE was simulated under the same operation condition. Detailed descriptions of the experimental system and test procedures is available in the literature [35]. The RNG \(\kappa-\varepsilon\) turbulence model is chosen in this paper as its widely used in WRE [28] and most consistent with particle image velocimetry (PIV) results [22]. The SAGE combustion model coupled with a detail hydrogen reaction mechanism is activated in the CFD model to calculated the combustion process [47]. The adaptive zoning and extended Zeldovich model are applied to accelerate calculation speed and predict the NOx emissions [48]. The base grid is 2 mm with the 1 level fixed refined mesh in the boundary and 2 levels adaptive mesh refinement (AMR) in regions of intake, chamber, and ignition chambers. Therefore, the minimum size of the chamber regions is 0.5 mm, which is fine enough to simulate the WRE [20]. In addition, during the ignition period, the 3 levels fixed refinement is active. The mesh grid of the hydrogen-fueled WRE is shown in Fig. 4. The comparison of simulated in-cylinder pressure and apparent heat release rate (AHRR) and measured results are illustrated in Fig. 5.

### Research schemes

Differ from the RPEs, the port shape is variable with the port timing of WREs. To solve the problem of balancing the air demand at different engine speeds, Mazda applies the multi-side port system to control the different intake ports opening timings [49]. To examine the effect of intake closing timing (ICT) at various engine speeds on the flow field, combustion process, and emissions formation, a total number of 9 cases are calculated and compared in this paper, as given in Table 3. It should be noted that the size of the side ported WRE is related to the port closing timing, as illustrated in Fig. 6, the delayed port closing timing accompanies a high port area [50]. In addition, the boundary and initial conditions in all simulations is the same as the original model, as listed in Table 2.

## 3 Results and discussion

### Analysis of flow behavior

Due to the long and narrow chamber of the WRE caused by the unique structure. The in-cylinder flow field of WREs is different from RPEs, especially for the side ported WREs. Therefore, it is necessary to analyze the flow field of the combustion chamber. To clearly describe the flow field, the surface connected with the intake port is defined as the front wall, and another wall is called as the rear wall. The surface connected with the spark plus is named upper wall, and the recess surface is named the inner wall [21]. The swirl is defined as parallel rotation, with its vortex parallel to the WRE rotation center; tumble is defined as perpendicular rotation, with its vortex perpendicular to the WRE rotation center [41]. The velocity distribution and the streamlines at different engine speeds is presented in Fig. 7. The eccentric angle in Fig. 7 is based on chamber I. Therefore the 0/540 "EA is the top dead

Figure 14: Comparison of the in-cylinder pressure.

Figure 13: Illustration of the flame propagation pattern.

[MISSING_PAGE_EMPTY:14]

center, and 270 'EA bottom dead ceneter. Over all, the flow field is similar at various engine speeds. In the intake stroke, the airflow inters to the combustion chamber and impings the rear wall. The two opposite rotating direction large-scaled vortexes are formed. The flow field velocity is higher at a higher engine speed. When the eccentric angle is 270 'EA, the volume of the combustion chamber is largest. The rear vortex begins to break up and the front vortex fills the combustion chamber. Due to the slight pressure difference between the intake channel and rear part of the combustion chamber and the relatively larger in-cylinder pressure of the front part, the airflow begins to backflow. When at 400 'EA, the vortex cluster starts to breakdown due to the squeeze of the upper and inner walls. At 520 'EA, the main flow field forms a unidirectional airflow in the combustion chamber.

The comparison of the in-cylinder mass is illustrated in Fig. 8. The small intake port decreases the intake backflow, which causes a higher in-cylinder mass. It should be noted that there are two pressure drops in the intake and compression strokes. The first is caused by the backflow, and another is formed by the gas leakage via the spark plugs [43]. When at a higher engine speed, the gas leakage is decreases due to the lower pressure difference between adjacent cylinders [51]. Another reason is that the higher speed causes a short connection time; thus, the gas leakage is smaller.

The vortex formed in the combustion chamber must affect the variation of the turbulence kinetic energy (TKE). The comparison of TKE according to the eccentric angle in intake and compression strokes are illustrated in Fig. 9. There are two peaks in the intake and compression strokes. The first peak is caused by the significant pressure difference in the intake stroke. The second peak is formed by the backflow when the chamber volume becomes small. The early intake closing timing causes a small area of the intake port, which causes a higher in-cylinder velocity, thus increases the TKE. The TKE at 8000 rpm is higher than the lower engine speed. This is because of the higher velocity caused by the large pressure difference.

Fig. 10 compares the change ratio of the intake loss and volumetric efficiency. The change trends of intake loss and volumetric efficiency are same. The larger intake port causes the lower intake loss and volumetric efficiency. When at a higher speed, the intake loss increases significantly, while the increasing trend of volumetric efficiency is small. However, the intake loss and volumetric efficiency have the opposite influence on the performance of the WRE [43]. Therefore, it is necessary to optimize the intake characteristics further to balance the intake loss and volumetric efficiency [52].

### Analysis of flame propagation

The comparison of the mass fraction of burned fuel is shown in Fig. 11. The difference between each ICT is similar at a constant engine speed. This because the same level of TEK and in-cylinder mass. However, when the engine speed is high, the rapid combustion duration (EA10-90) is prolonged. Therefore, it is necessary to analyze the flame propagation at different engine speeds. Fig. 12 displays the flame contours and OH spatial distribution in the combustion chamber vary from 540 to 560 'EA in increments of 5'EA. The iso-surface of temperature of 2000 K can be viewed as the flame surface. As shown in Fig. 12, the flame propagation slows down as engine speed is increased. When at 555 'EA, the two flames begins to merge at the engine speed of 3000 rpm. The flame propagation direction is opposite to the flow field from the combustion chamber to spark plug chamber when at the ignition timing. In all the simulation, the ignition timing is kept constant. The higher engine speed results a higher in-cylinder flow field. Therefore, it causes a prolonged EA10-90.

Since the flame propagation process is similar, it is necessary to further generalize the flame propagation pattern. The flame front caused by the two spark plugs is illustrated in Fig. 13. Firstly, the L-spark plug ignites the hydrogen mixture, so only a flame contour is formed in the front combustion chamber. Secondary, the T-spark plug ignites the rear combustion chamber. Then, the two flame contours are merged. The merged flame contour is similar to a racket shape. As the rotor continues rotation, the tail of the flame begins to develop. Due to the larger velocity and unidirectional flow field in the combustion chamber, and lean combustion resulting in a slower combustion rate, the trailing of the flame propagates backward no further than the T-spark plug position. Finally, the trailing flame propagates to both sides, as shown by the red arrow in Fig. 13.

Figure 16: Comparison of the mole fraction of NOx emissions.

Figure 15: Comparison of peak radical of H, O, and OH.

### Analysis of combustion and emissions

Fig. 14 illustrates the in-cylinder pressure for different cases. It is clear that the ICT contributes to the compression pressure and peak combustion pressure, which is consistent with the in-cylinder mass. When compared the engine speed, the compression pressure of higher engine speed is higher than the lower engine speed. However, the peak combustion pressure for ICT0 cases at different speeds is similar which is because of the later combustion phases of higher engine speed. Another reason is that the small-scaled WRE has a larger surface-to-volume ratio, which leads to more heat transfer loss. The expansion stroke of higher engine speed is above the lower engine speed, which causes more power output. This research uses the fixed ignition timing in all the cases, which is not conducive to reaching the maximum torque timing (MBT). Therefore, further work should optimize the ignition timing to maintain the MBT. The above result can be explained by the peak radical of H, O, and OH. For the hydrogen combustion, the concentration of active radicals of OH, H and O has a decisive effect on combustion transfer according to the reaction mechanism. As shown in Fig. 15, when the intake port area is small, the peak radicals of H, O and OH are higher. However, due to the similar level, the difference in in-cylinder pressure is minor.

Fig. 16 depicts the mole fraction of NOx emissions for each cases. Compared with later ICT, the NOx emissions of early ICT is higher. This is due to the higher in-cylinder temperature of ICT-5 cases. When comparing the NOx emissions for different engine speeds, the NOx emissions is lower at a higher engine speed. Fig. 17 shows the in-cylinder temperature profile. The mean in-cylinder temperature is lower than 1800 K in all the cases, which is not conducive to NOx generation. Another reason is the relatively rich in-cylinder mass. Compared with the lower engine speed, the in-cylinder mass of the higher engine speed is higher. Therefore, the NOx mole fraction for higher speeds is lower. It should be noted that the level of NOx is minor, which is a promising method for clean power output via lean combustion.

## 4 Conclusions

In this study, a 3-D CFD model of a small-scaled WRE coupled with a hydrogen chemical reaction mechanism was developed. The combination of intake closing timing and engine speed on flow, flame propagation, combustion characteristics, and pollutant generation was numerically investigated. The main conclusion are summarized as follows:

1. For the flow behavior, the in-cylinder flow field exhibits consistency at different engine speeds. The high speed promotes the formation of unidirectional main flow field in the combustion chamber. When at 20 'EA BTDC, the main flow field forms unidirectional flow. At different engine speeds, both the intake loss and volumetric efficiency increase at an earlier intake closing timing. The volumetric efficiency increases with engine speed and the leakage decreases.
2. For early intake closing timing, ignition is earlier and flame propagation is faster at different engine speeds. However, as the engine speed increases, the ignition delay increases. This is due to the large heat transfer losses and the strong in-cylinder flow field, which makes it more difficult for the flame to propagate from the ignition chamber to the combustion chamber.
3. Due to asynchronous ignition, two flames are formed in different phases and eventually merge. When ignited, a steady flame first develops within the leading spark plug ignition chamber and propagates to the combustion chamber. As the flame from the trailing spark plug propagates, the two flames begin to merge. However, the flame does not propagate backward due to the stronger main flow field in the cylinder.
4. The levels of O,H and OH radicals in the cylinder are similar at different speeds due to the lean combustion. This results in similar maximum combustion temperatures and peak combustion pressures. When the hydrogen-fueled WRE operates at the lean condition, the NOx generation levels is extremely low.

In this work, numerical simulations are applied to expose the fact

Figure 17: Comparison of the temperature curves.

[MISSING_PAGE_EMPTY:18]

that a higher engine speed and an earlier intake closing timing can increase the power output. This conclusion can facilitate the development of small hydrogen-fueled WRE.

## Author contribution

**Jinxin Yang:** Conceptualization, Validation, Writing - review & editing, Visualization; **Huaiyu Wang:** Conceptualization, Investigation, Methodology, Software, Resources, Writing - original draft preparation, Validation; **Changwei Ji:** Funding acquisition, Supervision, Project administration, Writing - review & editing; **Ke Chang:** Formal analysis, Supervision, Writing - review & editing; **Shuofeng Wang:** Formal analysis, Validation, Data curation, Supervision.

## Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Data availability

The authors do not have permission to share data.

## Acknowledgements

This work was financially supported by the National Natural Science Foundation of China (Grant Nos. 52276097, 51976003), the BIT Research and Innovation Promoting Project (Grant No. 2022YCXZ004), and the China Scholarship Council (Grant No. 202206030086).

## References

* [1] Yonter MA. Effects of ethanol, methyl tert-butyl ether and gasoline-hydrogen blend on performance parameters and HC emission at Wankel engine. Biofuels 2020;11 (3):277-88.
* [2] Shi C, Chai S, Di L, et al. Combined experimental-numerical analysis of hydrogen as a combustion enhancer applied to Wankel engine. Energy 2023;263:125896.
* [3] Meng H, Ji C, Xing G, Yang J, Chang K, Wang S, Comparison of combustion, emission and abnormal combustion of hydrogen-fueled Wankel rotary engine and reciprocating fusion engine. Fuel 2022;218:123675.
* [4] Di Lio G, Jamrelli E, Bella G. Performance evaluation of extended-range electric vehicles equipped with hydrogen-fueled rotary engine. SAE Technical Paper, 2020;20:204-4011.
* [5] Fried H, Praid G, Hubmann C, et al. Range extended technology for electric vehicles. In: Sth International Conference on Electric Vehicular Technology (ICEVT), 2018, p. 1-8.
* [6] Yamada T, Moriyoshi Y. Numerical analysis of combustion and flow inside a small rotary engine for developing an unmanned helicopter. SAE Technical Paper, 2007; 307-32-0098.
* [7] Sadiq GA, Al-Dada R, Mahmoud S. Development of rotary Wankel devices for hybrid automotive applications. Energy Converse Mange 2019;2021:11259.
* [8] Torre O, Al-Isdahda S, Mahmoud S. Simulating ages gap sizes in a small scale urban expander for air liquefaction. Appl Therm Eng 2019;54:476-84.
* [9] Li M, Li S, Zhang X, et al. Performance evaluation and flow analysis of two-cylinder triangular rotor pump based on experimental and numerical simulation. J. Adv. Mech. Design, Syst. Matmac. 2019;13(1):ADMS00003 (ADMSM).
* [10] Chen W, Pan J, Yang W, et al. Stratified combustion characteristics analysis and assisted-joint density optimization in a natural gas blended diesel Wankel engine. Fuel 2021;2922:12192.
* [11] Fan R, Zeng Y, Zhang Y, et al. Research on the hydrogen injection strategy of a direct injection natural gas/hydrogen rotary engine considering apex seal leakage. Int J Hydrogen Energy 2021;96(13):9234-51.
* [12] Wang H, Ji C, Shi C, et al. Comparison and evaluation of advanced machine learning methods for performance and emissions prediction of a gasoline Wankel rotary engine. Energy 2022;228:123611.
* [13] J. C, Wang H, Shi C, et al. Multi-objective optimization of operating parameters for a gasoline Wankel rotary engine by hydrogen enrichment. Energy Convers Manag 2021;229:113732.
* [14] Wang H, Ji C, Shi C, et al. Investigation of the gas injection rate shape on combustion, knock and emissions behavior of a rotary engine with hydrogen direct injection enrichment. Int J Hydrogen Energy 2021;64(27):14790-804.
* [15] Shi C, Chai S, Wang H, et al. An insight into direct water injection applied on the hydrogen-enriched rotary engine. Fuel 2023;339:127352.
* [16] Turner J, Islam R, Voraro G, et al. Investigations into steady-state and stop-start emissions in a Wankel rotary engine with a novel rotor cooling arrangement. SAE Technical Paper 2021;2021:204-0097.
* [17] Chen W, Pan J, Fan B, et al. Numerical investigation of dual-fuel injection timing on an self-aligned mixing and combustion process in a novel natural gas-diesed rotary engine. Energy Converse Mange 2018;176:3344-48.
* [18] Wang H, Ji C, Su T, et al. Comparison and implementation of machine learning models for the combustion phases of hydrogen-enriched Wankel rotary engines. Fuel 2022;310. Part B(15).
* [19] Duan X, Li N, Liu J, et al. Experimental and numerical investigation of the effects of low-pressure, high-pressure and internal EUR configurations on the performance, combustion and emission characteristics in a hydrogen-enriched heavy-dump natural gas SI engine. Energy Conversion and Management 2019;196:1319-33.
* [20] Sun X, Li H, Duan X, et al. Effect of hydrogen enrichment on the flame propagation, emissions formation and energy balance of the natural gas spark ignition engine. Fuel 2022;307:121843.
* [21] Chen W, Yu S, Zoo O, et al. Combined effect of air intake method and hydrogen injection timing on airflow movement and mixture formation in a hydrogen direct injection rotary engine. Int J Hydrogen Energy 2022;47(25):12739-58.
* [22] Han B, Zeng Y, Pan J, et al. Evaluation and analysis of injection strategy in a peripheral ported rotary engine failed with natural gas/hydrogen blends under the action of apex seal leakage. Fuel 2022;310:1223518.
* [23] Ma Y, Wang X, Li T, et al. Hydrogen and ethanol: production, storage, and transportation. Int J Hydrogen Energy 2021;64(54):27330-48.
* [24] Luo Q, Hu J, Sun B, et al. Experimental investigation of combustion characteristics and NOx emission of structured hydrogen internal combustion engine. Int J Hydrogen Energy 2019;41(14):5573-84.
* [25] Wang H, Ji C, Shi C, et al. Development of cyclic variation prediction model of the gasoline and a-butanol rotary engines with hydrogen enrichment. Fuel 2021;299:12091.
* [26] Su T, Ji C, Wang S, et al. Improving performance of a gasoline Wankel rotary by hydrogen enrichment at different conditions. Energy Convers Manag 2018;171:21-8.
* [27] Anrouche F, Erickson P, Varnshagen S, et al. An experimental analysis of hydrogen enrichment on combustion characteristics of gasoline Wankel engine at full load and lean burn regime. Int J Hydrogen Energy 2018;43(41):19250-9.
* [28] Yang J, Ji C, Wang S, et al. Numerical investigation on the mixture formation and combustion processes of a gasoline rotary engine with direct injected hydrogen enrichment. Appl Energy 2018;224:34-41.
* [29] Gong C, Li Z, Sun J, et al. Evaluation on combustion and lean-burn limit of a median conversion ratio hydrogen-methanol dual-liquid sensor-ignition engine under methanol late-injection. Appl Energy 2020;277:115622.
* [30] Gao J, Wang X, Song Y, et al. Review of the headlife occurrences and control strategies for ported hydrogen injection internal combustion engines. Fuel 2022;307:121553.
* [31] Zhang P, Xu G, Li Y, et al. Collaborative optimization of fuel composition and operating parameters of gasoline compression ignition (GCI) engine in a wide load range. Fuel 2022;301:112366.
* a highly promising combustion concept. SAE Technical Paper, 2005; 2005-01-0108.
* [33] Morimoto K, Teramoto T, Takamori Y. Combustion characteristics in hydrogen fueled rotary engine. SAE Technical Paper, 1992; 2002.
* [34] Yu X, Li G, Du Y, et al. A comparative study on effects of homogeneous or stratified hydrogen on combustion and emission of a gasoline/hydrogen SI engine. Int J Hydrogen Energy 2019;84(47):2597-84.
* [35] Yang J, Meng H, Ji C, et al. Comparatively investigating the leading and trailing spark plug on the hydrogen rotary engine. Fuel 2022;308:122005.
* [36] Ji C, Meng H, Wang S, et al. Realizing stratified mixtures distribution in a hydrogen-enriched gasoline Wankel engine by hydrogen component inside methods. Energy Convers Manag 2020;203:112230.
* [37] Svetiert J, Zahnstrom J F, Geringer R. Implementation of a rotary engine (Wankel engine) in a CPD simulation tool with special emphasis on combustion and flow phenomena. SAE Technical Paper, 2015; 2015-01-082.
* [38] Zou R, Liu J, Jiao H, et al. Combined effect of intake angle and chamber structure on flow field and combustion process in a small-steady rotary engine. Appl Therm Eng 2022;301:17652.
* [39] Jang D, Hsieh J, Lee C, et al. The intake and exhaust pipe effect on rotary engine performance. SAE Technical Paper; 2013, p. 32. 9161.
* [40] Turner J, Turner J, Turner M, Voraro G, et al. Initial investigations into the benefits and challenges of eliminating port overlap in Wankel rotary engines. SAE Int. J. Adv. Curr. Practices in Mobility 2020;2024;1800-17.
* [41] Taskina O, Celik A, Velatatat O. Comparison of flow field and combustion in single and double side ported rotary engine. Fuel 2019;254:115651.
* [42] Deng X, Liu X, Li J, et al. Optimization of fully variable valve system in a diesel rotary engine. Trans Clin Soc Agric Eng 2021;307:114-12.
* [43] Wang H, Ji C, Shi C, et al. Modeling and parametric study of the performance-ensensembles trade-off of a hydrogen Wankel rotary engine. Fuel 2022;318:123662.
* [44] Wang H, Ji C, Shi C, et al. Parametric modeling and optimization of the intake and exhaust phases of a hydrogen Wankel rotary engine using parallel computing optimization platform. Fuel 2022;232:124381.
* [45] Wang H, Ji C, Shi C, et al. Multi-objective optimization of a hydrogen-fueled Wankel rotary engine based on machine learning and genetic algorithm. Energy 2023;263:125961.
* [46] Donato T, Fiorellis A, De Pascalis GL. Energy management-based design of a Wankel hybrid-electric UAV. Aircraft Eng Aero Technol 2020;92(5):701-15.

[MISSING_PAGE_EMPTY:20]

* [47] Bao J, Qu P, Wang H, et al. Implementation of various bouf designs in an HPDI natural gas engine focused on performance and pollutant emissions. Chemosphere 2022:303135275.
* [48] Wang H, Gan H, Theotelkato G. Parametric investigation of pre-injection on the combustion, smoothing and emissions behaviour of a large marine four-stroke dual-fuel engine. Fuel 2020;28:118744.
* [49] Meng H, H, C, Wang S, Yang J. A review: Central progress and development of Walled rotary engine. Fuel 2003;335:127043. [https://doi.org/10.1016/j.fuel.202.21.127043](https://doi.org/10.1016/j.fuel.202.21.127043).
* [50] Wang H, Ji C, Yang J, et al. Implementation of a novel dual-layer machine learning structure for predicting the intake characteristics of a side-operated Walled rotary engine. Aero 561 Technical 2023;132:108042.
* [51] Fan B, Zhang Y, Pan J, et al. Experimental and numerical study on the formation mechanism of flow field in a side-ported rotary engine considering apex seal leakage. J Energy Resour Technol 2020;14(32).
* [52] Wang H, Ji C, Yang J, et al. Towards a comprehensive optimization of the intake characteristics for side period Walled rotary engines by coupling machine learning with genetic algorithm. Energy 2022;261:125334.

[MISSING_PAGE_EMPTY:22]