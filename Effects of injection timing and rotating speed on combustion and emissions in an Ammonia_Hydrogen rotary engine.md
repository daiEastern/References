Effects of injection timing and rotating speed on combustion and emissions in an Ammonia/Hydrogen rotary engine

PengZhen Li

School of Energy and Power Engineering, Jiangsu University, Zhenjiang 212013, China.

Jianfeng Pan

School of Energy and Power Engineering, Jiangsu University, Zhenjiang 212013, PR China.

Baowei Fan

School of Energy and Power Engineering, Jiangsu University, Zhenjiang 212013, PR China.

Miaoxin Qin

School of Energy and Power Engineering, Jiangsu University, Zhenjiang 212013, PR China.

 Muhammad Nauman

School of Energy and Power Engineering, Jiangsu University, Zhenjiang 212013, PR China.

Wenming Yang

School of Energy and Power Engineering, Jiangsu University, Zhenjiang 212013, PR China.

###### Abstract

Ammonia/hydrogen blending fuel is considered to be one of the ideal zero-carbon fuels that can effectively reduce carbon emissions from rotary engines. In this study, a three-dimensional model of an ammonia/hydrogen rotary engine was developed to investigate the influence of injection timing and rotating speed at different blending ratios on combustion performance and emission performance in the cylinder. The study found that, at an injection timing of 460\(\,\)'C before the top dead center (BTDC), the blending ratio of ammonia significantly affects the peak pressure, with a noticeable reduction in peak pressure. In contrast, at an injection timing of 395\(\,\)'CA (BTDC), the effect of the ammonia blending ratio on peak pressure is less significant, with in-cylinder peak pressures exceeding 1.7 MPa for blending ratios between 0.2 and 0.6. As the ammonia blending ratio increases, the ignition delay, CAS0, and combustion duration gradually lengthen, leading to enhanced work output, with ammonia and hydrogen fuel consumption rates approaching 100 %. The optimal blending ratio and injection timing combination is an ammonia blending ratio of 0.6 with an injection timing of 395\(\,\)'CA (BTDC). Furthermore, engine speed significantly affects combustion and emission characteristics: increasing rotating speed helps reduce the escape rate of ammonia and hydrogen. This study fills some of the research gaps in the field of ammonia-hydrogen rotary engines, providing data support for the development of rotary engines.

+
Footnote †: journal: homepage: www.elsevier.com/locate/apthemeng

+
Footnote †: journal: homepage: www.elsevier.com/locate/apthemeng

## 1 Introduction

In recent years, rotary engine, originally exploited by Dr. Felix Wankel and NSU Motorenwerke in 1951, has increasingly captured scholarly attention worldwide for its straightforward design, improved power-to-weight ratio, and lower production and maintenance costs than conventional piston engines. Recently, the rise of hybrid vehicles has spurred additional research into using rotary engines as range extenders [(1)]. Ammonia is a clean energy source, yielding a carbon-free product upon complete combustion [(2)]. It offers high volumetric energy density, low cost, and high safety [(3; 4; 5)]. Ammonia, however, poses challenges for its use as a fuel in internal combustion engines due to its narrow flammability range (equivalent ratio 0.63-1.40), high minimum ignition energy (2-3 orders of magnitude higher than common hydrocarbons [(6)]) [(7; 8)], and low laminar burning rate more than four times less than methane [(6)] (\(<\) 0.010 m/s). Ammonia combustion results in the formation of nitrogen oxides (NOx), primarily thermal NOx (when the temperature exceeds 1,800 'C) and transient NOx (formed as a result of the reaction between hydrocarbons and nitrogen). Compared to regular fuels, such as methane or natural gas, ammonia possesses a relatively low flame speed. The laminar flame speed of ammonia is typically around 0.35 m/s, while natural gas has a flame speed around 0.4-0.45 m/s. The result is a slower combustion process, making it more difficult to hold a stable flame at lower or medium loads. Ammonia's chemical structure leads to the formation of highly reactive intermediates like NH\({}_{2}\) and NH, which can cause oscillations or instabilities in the flame. Stabilized combustion of ammonia in internal combustion engines requires the combination of other active fuels such as diesel [(9)], biogas [(10; 11)], methane [(12)] and hydrogen [(13)] et al. In contrast to traditional hydrocarbon fuels, the combination of ammonia and hydrogen can achieve completely carbon-free emissions. The addition of hydrogen enhances ignition and flame propagation [(14)], while also reducing NOx and unburned ammonia emissions [(15)]. Table 1 presents the physical and chemical properties of ammonia and hydrogen fuels. Ammonia,compared to hydrogen, has a higher ignition point and autoignition temperature, as well as a lower energy density. However, the stoichiometric air-fuel ratio for hydrogen is over five times greater than that for ammonia [16].

Several scholars have already studied the fuel adaptation of rotary engines, such as gasoline [18], hydrogen, methanol, natural gas, and other biofuels [19]. Phillip et al. [20] developed a natural gas-fueled Wankel rotary engine (WREs) with a rated power of 185 kW that operates stably and exhibits low nitrogen oxide emissions through lean combustion. Meanwhile, Meng Hao et al. [21] compared the performance of hydrogen and gasoline-fueled WRE with a similar reciprocating piston engine, and Stutzenberger [22] corroborated that hydrogen can be effectively used in modified gasoline-specific WREs. Morimoto [23] determined that hydrogen-fueled WREs do not experience backfire under optimal conditions. However, this is contingent upon precisely tuning the spark plug hole diameter; if the hole is too large, flame leakage may occur, leading to premature ignition during the intake stroke and backfire in the intake manifold [24, 25]. Jianfeng Pan and Baowei Fan et al. [26] used both methanol fuel and turbulent jet ignition (TJI) mode to improve the combustion and emission performance of a gasoline rotary engine. By supplying hydrogen to an active pre-combination chamber and premixing ammonia and hydrogen in the intake manifold [27], they achieved stable and efficient combustion in large-bore marine engines. Baowei Fan et al. [28] proposed a new method of the setting of bluff bodies in natural gas rotary engines. The results indicated that in-cylinder bluff-body settings could influence flame propagation by affecting the turbulent kinetic energy and mixture distribution during the process from the late compression stroke to the combustion stroke. Jianfeng Pan et al. [29] also established a PIV flow field testing platform to visualize vortex patterns and unidirectional flow near the top dead center.

Currently, researchers are investigating the blending ratio between ammonia and hydrogen as follows: Youtong Zhang et al. [30] explored how fuel ratios and ignition advanced angles impact engine performance using both experimental and numerical simulation techniques, focusing on an inline four-stroke engine. Their research concluded that a 9:1 ammonia-to-hydrogen ratio achieves the best overall efficiency. Shengli Wei et al. [31] examined the combustion characteristics of ammonia and hydrogen in marine engines. Jinguang Li et al. [32] studied the effects of equivalence ratio and hydrogen-to-ammonia ratio on ignition characteristics in rapid compression machines. Dong Han et al. [33]do some researches on the effects of ambient pressure, ammonia-hydrogen blending ratio and orifice diameter on combustion by turbulent jet ignition. The results show that jet ignition is a more effective means of accelerating the combustion of ammonia-hydrogen mixtures than spark ignition. Changwei Ji et al. [13] explored the combustion and emission characteristics of a turbulent jet ignition ammonia/hydrogen dual-fuel engine through experiments and numerical simulations. Arkadiusz Jamrozik [34] found that hydrogen and ammonia can be effectively co-fired with diesel fuel. A comparative experimental study of the effect of ammonia/hydrogen on the performance, stability and emissions of an industrial dual-fuel compression-ignition engine was further investigated. Their findings show that ammonia-hydrogen blending fuel has a good prospect for application in internal combustion engines. But there is still a large gap in the research of ammonia-hydrogen rotary engine. Meanwhile, for the injection strategy. Xinran Wang et al. [35] investigated the combustion characteristics, emissions and thermal efficiency of a low-pressure injection ammonia-diesel dual-fuel engine at 80 % AER. By optimizing the ammonia injection strategy, a simultaneous reduction of unburned NH\({}_{3}\) by about 11 %, a reduction of N\({}_{2}\)O by about 13 %, and an increase in the indicated thermal efficiency by 1.1 % could be achieved. Xidong Wang, Junheng Liu et al. [36] explored the potential of pre-injection strategies in improving the performance of ammonia/ diesel dual-fuel engines by comprehensively evaluating the effects of four pre-injection parameters (main injection timing, pre-injection quantity and diesel injection pressure) on the in-cylinder combustion process and energy efficiency. injection quantity and diesel injection pressure) on the in-cylinder combustion process, incomplete combustion emissions and energy efficiency were comprehensively evaluated. Baowei Fan et al. [37] optimized the injection strategy for natural gas-fueled WRE. The above study further demonstrates that for ammonia-hydrogen blending fuel, the optimized injection strategy is essential for optimal combustion, efficiency enhancement and emission reduction.

Based on the literature review, ammonia-hydrogen blending fuel in the rotary engine still has a big gap in research, further, the ammonia-hydrogen blending ratio and injection strategy could greatly influence the combustion and emission performance. Therefore, the combustion and emission characteristics under the coupling of the ammonia-hydrogen blending ratio and injection strategy need to be studied in depth. This paper addresses this gap by employing a combination of experimental and numerical simulation methods [38] to investigate the effects of ammonia-hydrogen blending ratio and injection timing on the combustion and emission performance of rotary engines with intake manifold premixing.

## 2 Methodology

In this study, a premix rotary engine fueled with ammonia-hydrogen was selected as the research object. Specific parameters and components are presented in Table 2. The Z16OF rotary engine was initially equipped with a carputer and a magneto ignition system but was modified with electronic controls to meet experimental requirements. Fig. 1 shows the schematic of the updated ammonia/hydrogen rotary engine test platform. Once the engine stabilized after warm-up, a measurement system with pressure sensors and a combustion analyzer was used to record the pressure inside the combustion chamber. From this data, the heat release curve was calculated. The test rig assessed the engine's combustion performance at low injection pressures (3 bar) and speeds (1400 rpm and 2000 rpm) with various ammonia/hydrogen blending ratios. Hydrogen and ammonia were mixed and injected into the cylinder after being pre-mixed in the intake manifold at a temperature of 300 K. This study initially focused on optimizing the ammonia/hydrogen blend ratio

\begin{table}
\begin{tabular}{l l l} \hline Type of gas & Ammonia & Hydrogen \\ \hline Molecular formula & NH\({}_{3}\) & H\({}_{2}\) \\ Density (20 C) ( kg\(\cdot\)m\({}^{-3}\)) & 0,77 (liquid ) & 0.089 \\ Combustion point (\(\mathbb{C}\)) & 800 & 400 \\ Minimum Ignition Energy ( MJ) & 680 & 0,02 \\ Low heat ( ML/kg) & 18.8 & 119.6 \\ Latent heat of evaporation ( kJ/kg) & 1370 & — \\ Molecular mass & 17.31 & 2.016 \\ Spontaneous combustion temperature ( K ) & 923 & 773 \\ Energy density ( ML/m\({}^{3}\)) & 11.3 & 10.7 \\ Flash point ( \(\mathbb{C}\)) & 11 & — \\ Chemometric air–fuel ratio ( kg/kg) & 6.14 & 34.3 \\ \hline \end{tabular}
\end{table}
Table 1: Comparison of physical and chemical properties of ammonia and hydrogen [17].

\begin{table}
\begin{tabular}{l l} \hline Number of rotors & 1 \\ cooling mode & air cooling \\ ignition type & spark plug ignition \\ Displacement & 160 cm\({}^{3}\) \\ Compression ratio & 8 \\ Generating radius & 69 mm \\ Eccentricity & 11 mm \\ Chamber width & 40 mm \\ Intake timing & 615’CA ( BTDC ),207’CA ( BTDC ) \\ Exhaust timing & 208’CA ( ATDC ),610’CA ( ATDC ) \\ \hline \end{tabular}
\end{table}
Table 2: Major parameters of Z16OF gasoline rotary engine.

and the timing of injection. At various speeds, the effects of airflow on combustion and emissions were examined in an ammonia-hydrogen rotary engine.

### Geometric modeling and mesh generation

The engine under discussion was developed by modifying and prototyping the Z160F air-cooled gasoline rotary engine and is described as a single-rotor end-face intake rotary engine. Fig. 2 (a) shows the geometric model. The computational domain for simulation was segmented into six distinct areas: the intake manifold, exhaust manifold, three combustion chambers, and the spark plug, as depicted in Fig. 2 (b).

Mesh generation for these regions is shown in Fig. 2 (b), with a base mesh size of 4 mm, the result of mesh independence analysis is shown in Fig. 3. The mesh was refined based on the computational requirements for different areas. Adaptive mesh refinement [40] was applied across all regions, with additional constraints for temperature gradient, velocity gradient, and mixture concentration gradient of adjacent meshes set at 20 K, 5 m/s, and 0.1, respectively. The overall mesh refinement level was set to 3, which corresponds to a 0.5 mm mesh size. These mesh settings are sufficient to meet the accuracy requirements of the computation.

Figure 1: Schematic diagram of experimental setup.

Figure 2: Rotary engine geometry modeling and meshing.

### Selection and validation of calculation models

In this simulation, boundary conditions and parameters are assigned to various components to accurately model the system. At the intake duct's inlet, the surface mesh is designated as a pressure boundary with an intake pressure of 0.063 MPa, while the wall temperature of the duct is set to 330 K. For the exhaust duct outlet, which is exposed to the external environment, the surface mesh is also a pressure boundary, with the pressure fixed at one atmosphere. The wall temperature of the exhaust duct is set to 800 K to account for the high temperature of the exhaust gases. The triangular rotor is configured with its surface mesh as both a wall and a moving boundary. The rotor's motion is defined by its dimensional parameters, and its wall temperature is set to 430 K. For other boundaries, the spark plug wall temperature is set to 650 K, the electrode to 800 K, the throttle to 300 K, and all other fixed boundaries to 400 K. Additionally, the mixture composition must be adjusted according to the type of fuel, mixing ratio, and equivalence ratio. The simulation uses a minimum time step of 1e\({}^{-8}\)s and a maximum time step of 1e\({}^{5}\)s [41], with computations conducted at the minimum time step for precision.

For turbulence model, RNG k-e turbulence model was selected due to its balance between fluid compressibility, accuracy requirements, and computational efficiency. This model excels in simulating high-speed flows, vortex dynamics, and near-wall regions. Validation of the flow field using this model is detailed in our previous work [42, 43, 44, 29].

For the combustion model, we employed the SAGE combustion model [45] from CONVERGE software for numerical simulations. We used the simplified reaction mechanism proposed by Gabriel J. Gotama [46], which features 26 species and 119 steps, to accurately predict flame combustion speed across various equivalence ratios. To validate the chemical mechanism and the SAGE combustion model, we compared experimental data with simulation results under the conditions specified in Table 3. The choose of ignition timing is 15'CA BTDC in simulation condition, because of the experimental results show a better combustion performance in cylinder. Fig. 4 illustrates the comparison between pressure curves from experiments and simulations. The figure shows that the trends in both experimental and simulated pressure curves are generally consistent, with a maximum error in-cylinder pressure of less than 10 %. This indicates that the SAGE combustion model provides a reliable and accurate representation of the combustion process in the rotary engine using ammonia/hydrogen fuel.

### Design of calculation scheme

The timing of fuel injection is pivotal in engine research, significantly influencing engine performance, efficiency, and emissions. Incorrect timing can lead to incomplete combustion, reducing engine efficiency and increasing fuel consumption. Moreover, variations in injection timing alter engine power and torque output. By precisely controlling injection timing, it is possible to enhance the engine's dynamic response and acceleration. Optimal injection timing varies with different operating conditions, making it essential to study and refine these timings to recognize the engine performs effectively across various scenarios. This study examines the Z160F rotary engine to determine the most effective fuel injection strategy with different ammonia mass ratios. The ammonia blending ratios explored range from 0.2 to 0.7, with injection timings set at 460degCA, 425degCA, and 395degCA BTDC. The injection timing for Case A is 460deg CA BTDC, just before the intake valve opens. For Case B, the injection timing is 425deg CA BTDC, when the intake valve opens one-third of the way. In Case C, the injection timing is 395deg CA BTDC, with the intake valve opened two-thirds of the way. Numerical simulations with further delayed injection timing show that combustion cannot be achieved in the cylinder. A-0.2 applies for 460degCA BTDC cases; B-0.2 applies for 425degCA BTDC cases; C-0.2 applies for 395degCA BTDC cases, where "0.2" is ammonia mass ratio.

Figure 4: Experimental-Simulated Cylinder Pressure Comparison Chart.

Figure 3: Mesh independency analysis of in-cylinder pressure.

\begin{table}
\begin{tabular}{l l} \hline Engine parameters & Value \\ \hline Rotating speed & 1400r/min \\ Throttle opening & 13 * \\ ignition time & 15°CA(BTDC) \\ Ammonia/hydrogen injection time & 425°CA ( BTDC ) \\ \hline \end{tabular}
\end{table}
Table 3: Numerical simulation of working conditions.

## 3 Calculation results and analysis

### Effect of injection timing on rotary engine

Ammonia has superior anti-knock properties, making it a valuable additive to hydrogen as it can help reduce engine knock. However, Hydrogen burns at a much higher rate than ammonia, which can greatly enhance the combustion process. To investigate these effects, we used numerical simulations to analyze the combustion process and emissions in the rotary engine cylinder. Since the fuel structure did not include any carbon-containing components, we measured only the emissions of NO, NO\({}_{2}\), and N\({}_{2}\)O.

#### 3.1.1 Effect on combustion performance

Fig. 5 illustrates the impact of varying ammonia mixing ratios and different injection timings on the in-cylinder pressure of a rotary engine. Panels 5(a), 5(b), and 5(c) present the cylinder pressure curves for Cases A, B, and C, corresponding to ammonia ratios ranging from 0.2 to 0.7. Panel 5(d) provides a summary of the peak pressure and its timing for each case. At an injection timing of 460\({}^{\circ}\) CA before the top dead center (Case A), the ammonia ratio has a substantial effect on peak pressure. Increasing the ammonia ratio leads to a significant decrease in peak pressure. In contrast, at an injection timing of 395\({}^{\circ}\) CA before the top dead center (Case C), the ammonia ratio's impact on peak pressure is less pronounced. Here, peak pressures for ammonia ratios between 0.2 and 0.6 remain above 1.7 MPa. For the same ammonia ratio, Case B shows the highest peak pressure when the ratio is below 0.6, while Case C performs best when the ratio is 0.6 or higher. The observed differences are due to the lower calorific value of ammonia compared to hydrogen. As the ammonia ratio increases, the overall calorific value per unit volume of the fuel mixture decreases [47], resulting in reduced energy release and lower peak pressure. Additionally, ammonia produces nitrogen (N\({}_{2}\)) during combustion, which is inert and does not contribute to further reactions. An increase in the ammonia ratio thus raises the nitrogen content, which can dilute the active components of the combustion mixture, further lowering combustion efficiency and peak pressure. Ammonia's slower flame propagation also delays flame spread within the combustion chamber, affecting the combustion process and causing lower peak pressures as well as a shift in peak pressure timing downstream of the top dead center. In summary, a higher ammonia mass ratio leads to lower peak pressure and a delay in peak pressure timing. This is because delayed injection timing can reduce the uniformity of the fuel mixture, potentially causing fuel stratification, which shortens ignition delay, increases in-cylinder pressure, and advances the timing of peak pressure.

In ammonia/hydrogen rotary engines, the blending ratio of fuel and its uniformity can significantly impact flame propagation and combustion rate, which in turn affects the possibility of engine knock (as seen in Case B-0.2, 0.3; Case C-0.2, 0.3). Therefore, optimizing the fuel injection timing is essential for ensuring stable combustion of the ammonia-hydrogen mixture. By refining the design and making appropriate adjustments, it is possible to improve engine performance, reduce knock, and lower pollutant emissions.

Fig. 6 illustrates how varying the ammonia blend ratio and injection timing affects engine performance metrics such as ignition delay, CAS0 ( Crank angle at 50 % of total heat release ), combustion duration, and work output. With a constant injection timing, increasing the ammonia blend ratio results in longer ignition delay, CAS0, and combustion duration. Increasing the ammonia blend ratio can also improve gross work. Conversely, delaying the injection timing from 460\({}^{\circ}\) CA (BTDC) to 425\({}^{\circ}\) CA (BTDC) significantly reduces ignition delay, CAS0, and combustion duration. Further delay to 395\({}^{\circ}\) CA (BTDC) continues to reduce these metrics, though the reductions are less pronounced. This effect arises because a later injection timing shortens the fuel's residence time in the combustion chamber, leading to longer mixing time in the cylinder and a richer fuel-air mixture that accelerates the reaction rate.

Figure 5: In-cylinder pressure at different injection time with varying ammonia blending ratio.

Additionally, delaying the timing shifts the combustion process to the expansion stroke, enhancing work output by utilizing more of the combustion energy for work instead of losing it during compression. This timing also reduces the high-temperature duration in the chamber, minimizing heat loss. For an ammonia blend ratio of 0.6, delaying injection timing from 460\({}^{\circ}\) CA (BTDC) to 395\({}^{\circ}\) CA (BTDC) decreases ignition delay by 7.23\({}^{\circ}\) CA, CA50 by 28.31\({}^{\circ}\) CA, and combustion duration by 47.86\({}^{\circ}\) CA, while boosting work output by 15 %.

#### 3.1.2 Effect on fuel consumption rate

Fig. 7 illustrates how altering the ammonia blending ratio and injection timing affects the ammonia/hydrogen consumption rate in a rotary engine. Delaying the injection timing significantly influences the hydrogen consumption rate. At 460\({}^{\circ}\) CA (BTDC), the hydrogen consumption rate is about 40 %. It rises to approximately 60 % at 425\({}^{\circ}\) CA (BTDC) and nearly reaches 100 % at 395\({}^{\circ}\) CA (BTDC). In contrast, the ammonia consumption rate remains relatively high across different timings. Delaying injection timing reduces fuel uniformity, which can improve combustion through some degree of fuel stratification. The stratification of the fuel somewhat promotes combustion in the ammonia-hydrogen rotary engine because: Stratification creates areas of higher ammonia concentration within the combustion chamber, resulting in better control of ammonia ignition. Since ammonia ignites at higher temperatures, this localized enrichment helps ensure that

Figure 6: Ignition delay, CA50, combustion duration and Gross work for varying ammonia blending ratio at different injection time.

Figure 7: Ammonia/hydrogen consumption rate for varying ammonia blending ratio at different injection time.

\begin{table}
\begin{tabular}{c c c} \hline \hline
0.2 & 0.4 & 0.6 \\ \hline
0.2 & 0.4 & 0.6 \\ \hline
0.3 & 0.6 \\ \hline
0.4 & 0.6 \\ \hline \hline \end{tabular}
\end{table}
Table 4: Temperature field in the cylinder.

ammonia ignites at the right time, reducing the risk of misfiring or incomplete combustion. It also provides better control of combustion timing, ensuring smoother engine operation. The rapid combustion characteristics of hydrogen can be positively used to further ignite the ammonia. This prevents the hydrogen from burning too quickly and provides a more controlled, even combustion process. Consequently, this delay increases the hydrogen consumption rate, indicating that adjusting injection timing can enhance fuel consumption efficiency and economic performance.

#### 3.1.3 Effect on the temperature field

Table 4 shows how the temperature field within the cylinder changes with varying ammonia addition ratios. With consistent injection timing, increasing the ammonia ratio slows the formation rate and reduces the size of high-temperature regions. Fig. 8 shows the mean temperature in-cylinder, Case B-0.2 shows the highest peak value of temperature after ignition, Combined with Table 5, it can also be seen that the CaseB-0.2 flame develops very rapidly, with the high-temperature region being the largest. Meanwhile Case C-0.6 has the highest temperature at rear part of the combustion. This occurs because a higher ammonia ratio decreases the reactivity of the ammonia-hydrogen mixture, leading to a slower combustion rate. Ammonia has a lower calorific value and flame temperature than hydrogen, so a higher ammonia proportion reduces the overall energy produced during combustion. Additionally, ammonia has the following characteristics: ammonia has a relatively high ignition temperature (about 651 'C') ; ammonia has a lower energy density by volume than traditional fuels; ammonia has relatively narrow blimbility limits (15-28 % in air) and laminar flow combustion is slow. These factors combine to reduce the rate of ammonia combustion.

Delaying the injection timing results in an earlier development of high-temperature regions. This happens because a delay in injection timing causes uneven fuel distribution within the combustion chamber, leading to earlier high temperatures in the upstream area due to fuel buildup. Additionally, if the injection timing is delayed while ignition timing remains the same, the time between fuel injection and ignition decreases. This shorter interval raises the temperature and pressure of the mixed gas in the combustion chamber at ignition, which speeds up the combustion reaction and accelerates the formation of high-temperature regions.

#### 3.1.4 Effect on emission performance

Ammonia fuel contains nitrogen, which leads to the formation of nitrogen-containing intermediates during combustion. Due to ammonia's poor combustion and ignition characteristics, these intermediates are not fully oxidized, resulting in increased NO\({}_{2}\) and N\({}_{2}\)O emissions in the exhaust gas, NO, NO\({}_{2}\) and N\({}_{2}\)O emission are shown in Fig. 9. When the ammonia blend ratio remains constant, delaying the injection timing of the ammonia/hydrogen blend fuel, as shown in Table 4, causes the high-temperature region in the cylinder to form earlier and last longer. This increases the production of NO under Case C conditions. Reaction path (a) is the dissociation of oxygen by atomic hydrogen represents one of the most important acts in combustion, resulting in hydroxyl radical species (OH) which are highly reactive because they can participate in the formation of NO. The formation of HO\({}_{2}\) by reaction path (e) also enhance NO formation via high-temperature mechanism in hydrogen-rich flames. Reaction pathway (b) and (c), gives birth to NH\({}_{2}\) radicals that further reacts with oxygen and forms NO or NO\({}_{2}\) hence giving birth to NOx. NH\({}_{2}\) generated in reaction pathway (c) and (d) react with oxygen to form H\({}_{2}\)NO, which eventually can decompose to form N\({}_{2}\)O, thus contributing to the N\({}_{2}\)O emissions. Reaction path (f) shows that hydrogen can play the role of a radical scavenger, possibly decreasing the concentration of the OH and HO\({}_{2}\) radicals, but also affecting the overall reactivity and intermediate species involved in the NOx formation. Reaction (g) is part of the chain propagation in combustion, where the OH radicals can regenerate HO\({}_{2}\) to increase the radical concentration available for NO formation. For example, in Case C-0.6, compared to

\begin{table}
\begin{tabular}{c c} \hline \hline Applied Thermal Engineering 262 (2025) 125172 \\ \hline \hline \end{tabular}
\end{table}
Table 4: (continued)

[MISSING_PAGE_EMPTY:9]

[MISSING_PAGE_FAIL:10]

Fig. 11 (a) and 11 (b) illustrate that increasing engine speed results in a prolonged combustion duration, particularly when speeds exceed 2000 rpm. This increase is accompanied by a notable rise in ignition delay, CA50, and overall combustion duration. The primary reason for this phenomenon is that ammonia, with its higher auto-ignition temperature and greater minimum ignition energy, presents greater challenges for ignition and combustion at elevated speeds. Furthermore, ammonia's slower laminar flame speed means that at higher engine speeds, the flame propagation cannot be completed efficiently, thereby extending the combustion period.

Fig. 12 illustrates how varying engine speed affects indicated power. The data show that indicated power and Indicated Mean Effective Pressure (IMEP) peak at 1800 rpm. This optimal performance occurs because higher speeds enhance combustion efficiency by increasing turbulence within the combustion chamber. This improved turbulence aids in the mixing of fuel and air, thus accelerating and refining the combustion process. Additionally, higher speeds may lower internal mechanical losses, as the lubrication film improves, reducing friction and contributing to better engine performance.

#### 3.2.2 Effect on fuel consumption rate

Fig. 12 illustrates how changes in engine speed affect the ammonia and hydrogen escape rates and consumption rates, given an ammonia ratio of 0.6 and an injection timing of 395'CA (BTDC). Fig. 13 (a) shows

Fig. 11: Ignition delay, CA50, combustion duration at different rotating speed.

Fig. 10: In-cylinder pressure and heat release rate at different rotating speeds.

that increasing engine speed reduces the escape rates of ammonia and hydrogen, which enhances economic performance. This improvement is due to the increased turbulence at higher speeds, which promotes better mixing of fuel and air and decreases the escape of unburned gases. Fig. 13 (b) depicts the consumption curves of ammonia and hydrogen within the cylinder. The mass of in-cylinder gases peaks around 800degCA before decreasing, which is attributed to the recirculation phenomenon occurring at the intake port as the intake stroke of the end-face rotary engine nears its end. This decrease is an inherent characteristic of the engine. A second decrease in gas mass is observed around 940degCA (140degCA BTDC), attributed to the introduction of a leakage model that simulates real operating conditions. This model causes some gases to flow into the next combustion chamber due to unidirectional flow. Following ignition timing (15degCA BTDC), there is a significant reduction in ammonia and hydrogen levels. Notably, as engine speed increases, the rate of ammonia and hydrogen consumption decreases.

#### 3.2.3 Effects on fuel distribution and temperature field

Fig. 14 illustrates how varying engine speeds affect fuel distribution within the cylinder, with an ammonia ratio of 0.6 and injection timing

Figure 12: IMEP and gross work of rotary engine at different rotating speed.

Figure 13: Ammonia/hydrogen escape and consumption rates at different rotating speeds.

set at 395\({}^{\circ}\)CA (BTDC). The ammonia and hydrogen distribution depicted at 180\({}^{\circ}\)CA, 120\({}^{\circ}\)CA, and 60\({}^{\circ}\)CA before top dead center. At speeds below 1200 r/min, ammonia is mostly concentrated upstream and downstream of the combustion chamber. When speeds range from 1200 r/min to 2000 r/min, ammonia shifts to the upper stream of the chamber. At speeds above 2000 r/min, ammonia distribution becomes more even throughout the chamber. At speeds below 1200 r/min, ammonia and hydrogen are well-mixed and evenly distributed. Between 1200 r/min and 1800 r/min, the mixing quality slightly decreases, but hydrogen distribution remains consistent, with reduced stratification. Above 2000 r/min, the stratification of both ammonia and hydrogen diminishes, leading to a uniform distribution. This change is due to the shorter cycle time at higher speeds, which accelerates fuel and air mixing and decreases stratification. Increased turbulence at high speeds, as shown in Fig. 15, disrupts laminar flow, enhancing the mixing process and promoting a more uniform distribution of fuel. In a rotary engine, the shape of combustion chamber varies continuously as the rotor moves. The turbulence can vary from one area to another depending on the position of the rotor and the intake/exhaust phases. Turbulence is essential for promoting mixing of the air-fuel mixture, but when it becomes excessive or poorly distributed, it can cause problems: excessive turbulence can lead to local flame quenching, where the flame front is prematurely extinguished in certain areas of the combustion chamber. This phenomenon occurs when the local air-fuel mixture is too lean, too rich, or not uniformly mixed, leading to uneven combustion; another consequence of excessive or poorly controlled turbulence is non-uniform combustion, where different areas of the chamber burn at different rates, non-uniform combustion can also result in knocking, which occurs when parts of the fuel-air mixture ignite prematurely due to high local temperature, further exacerbating engine performance issues.

Table 5 presents the impact of varying engine speeds on thecylinder temperature field with an ammonia blend ratio of 0.6 and injection timing at 395\({}^{\circ}\)CA (BTDC). The data reveal that increasing engine speed generally reduces the formation of high-temperature regions, particularly when speeds exceed 2000 rpm, where such regions are nearly nonexistent. This occurs because ammonia burns more slowly

Figure 14: In-cylinder fuel distribution at different rotating speed.

Figure 15: Turbulent kinetic energy at different rotating speed.

than hydrogen, and while hydrogen can accelerate combustion, high engine speeds limit the time available for the mixture to achieve optimal combustion conditions, thereby reducing the development of high-temperature areas. Although higher speeds usually increase turbulence and improve mixing, excessive turbulence can disrupt the high-temperature flame core, further inhibiting the formation of high-temperature zones. Moreover, as engine speed rises, the duration of each cycle shortens, necessitating quicker completion of the combustion process. This reduced time may prevent the gaseous mixture from reaching sufficient temperatures to form high-temperature regions effectively.

#### 3.2.4 Effects on emission performance

Fig. 16 illustrates the impact of varying engine speeds on emissions with an ammonia ratio of 0.6 and an injection timing of 395' CA (BTDC), more details of the contaminant generation process can be found in Fig. 17. It shows that NO emissions initially rise with increasing engine speed but then decrease. This pattern occurs because, at higher speeds, improved intake efficiency elevates the oxygen concentration in the cylinder, and faster airflow enhances fuel-air mixing, creating better conditions for NO formation. However, as engine speed continues to rise, NO\({}_{2}\)and N\({}_{2}\)O emissions also increase due to shorter combustion times, which can lead to incomplete combustion. Unburned products may then react with nitrogen oxides during the exhaust phase, forming additional N\({}_{2}\)O.

## 4 Conclusion

This work investigates the effect of injection timing and rotating speed on combustion and emission characteristics in an ammonia-hydrogen dual fuel rotary engine. The key findings are as follows:

1. With the same injection timing, higher ammonia ratios generally reduce peak pressure and shift the peak pressure timing downstream of the top dead center. For ammonia mass ratio \(\leq\) 0.5, peak pressure is highest at 425'CA (BTDC), while for ratios \(>\) 0.5, it peaks at 395'CA (BTDC). Increasing the ammonia ratio eatents ignition delay, CA50, and combustion duration, thereby enhancing work output. For a constant ammonia ratio, delaying injection timing from 460'CA to 425'CA before the top dead center reduces ignition delay, CA50, and combustion duration. Further delay to 395'CA before the top dead center shortens these parameters even more, though the reduction becomes less significant.
2. Delaying the injection timing improves the fuel consumption rate of ammonia and hydrogen, approaching 100% at 395'CA (BTDC). Higher ammonia ratios delay the formation of high-temperature regions, extending ignition delay, CA50, and combustion duration. This enhancement of work output leads to increased NO formation. Considering cylinder pressure, temperature, work output, and emissions, the optimal blend ratio was0.6 with injection timing at 395'CA (BTDC).
3. At an ammonia ratio of 0.6 and injection timing of 395'CA (BTDC), higher peak pressures are observed at 1400 rpm and 1800 rpm. At this blend ratio, peak pressure timing shifts after top dead center with increasing speed. Higher speeds reduce the instantaneous heat release rate and lengthen fuel combustion time in the cylinder. Particularly above 1800 rpm, ignition delay, CA50, and combustion duration are significantly extended.
4. Increasing speed reduces the escape rate of ammonia and hydrogen. Below 1200 rpm, ammonia was mainly distributed upstream and downstream of the combustion chamber. Between 1200 rpm and 2000 rpm, ammonia concentrates in the upstream part of the chamber. Above 2000 rpm, ammonia distributes more evenly within the chamber. Below 1200 rpm, mixing of ammonia and hydrogen was relatively good; between 1200 rpm and 1800 rpm, mixing quality begins to decline; and above 2000 rpm, the quality further deteriorates with reduced H\({}_{2}\) stratification. Similarly, NH\({}_{3}\) stratification diminishes above 2000 rpm.

Figure 16: Emission characteristics at different rotating speed.

Figure 17: Emission generating process at different rotating speed.

### Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Acknowledgements

This work was supported by the National Natural Science Foundation of China (Grant Nos.52276117; Nos.51976083), Qing Lan Project, Project funded by China Postdoctoral Science Foundation (No. 2023T160550).

## Data availability

No data was used for the research described in the article.

## References

* [1] L. Fa, Triangular rotary engine, National Defense Industry Press (1990).
* [2] M.C. Chiong, C.T. Chong, J.H. Ng, S. Mashruk, A. Valae-Medina, Advancements of combustion technologies in the ammonia-fuelled engines, Energy. Conner. Manage. 2044 (2021) 11460.
* [3] W.H. Avery, Arole for ammonia in the hydrogen economy, Int. J. Hydrogen Energy 13 (8038) 764-779.
* [4] C. Kurien, M. Mittal, Review on the production and utilization of green ammonia as an alternate fuel in dual-fuel compression ignition engines, Energy. Conner. Manage. 251 (2022) 114909.
* [5] A. Valera-Medina, P. Amer-Hsatom, A.K. Azad, I.C. Dodoussi, M. Costa, Review on ammonia as a potential fuel: from synthesis to economics, Energy Fuel (2021).
* [6] A. Valera-Medina, H. Xiao, M. Owen-Jones, W.H. David, P.J. Bowen, Anmonia for power, Prog. Energy Combt. Sci. 69 (2018) 63-102.
* [7] W. Gornelis, L.W. Hullenstam, H.R. Mitchell, Almmonia as an Engine, Fuel (1965).
* [8] W.S. Chai, Y. Bao, P. Jin, G. Tang, L. Zhou, A review on ammonia, ammonia-hydrogen and ammonia-methane fuels, Renew. Sustain. Energy Rev. 147 (2021).
* [9] L. Chen, W. Zhao, R. Zhang, H. Wei, P. J. J. Jugiro, Flame characteristics and abnormal combustion of ammonia-diegal dual-fuel engine with considering ammonia energy fractions, Appl. Therm. Eng. 245 (2024).
* [10] L.B. Dahra, M. Said, Z.A. Abdul Karim, M. El-Adawy, Effects of pure mixing and high carbon dioxide contents in power generation and emission characteristics of biogas-diegal RCOL combustion, Appl. Therm. Eng. 198 (2021).
* [11] Y. Zhang, M. Zhu, Z. Zhang, Y. Liu, C. Zhang, Dong, Combustion and emission characteristics of stimulated biogas from Two-Phase Anaerobic Digestion (T-PAD) in a spatial ignition engine, Appl. Therm. Eng. 129 (2018) 927-933.
* [12] F. Guo, C. Li, X. Niu, K. Cheng, J. Jin, Comprehensive technical analyses of a solid oxide fuel cell turbine-less hybrid aircraft propulsion system using ammonia and methane as alternative fuels, Appl. Therm. Eng. 230 (2023).
* [13] Y. Qiang, S. Zhao, F. Su, P. J. Jugiro, J. Yang, S. Wang, et al., Experimental and numerical assessment on co-combustion of hydrogen with ammonia in passive pre-chamber engines, Appl. Therm. Eng. 259 (2025).
* [14] J. Li, R. Zhang, J. Pan, H. Wei, G. Shu, L. Chen, Ammonia and hydrogen blending effects on combustion stabilities in optical SI engines, Energy. Conner. Manage. 280 (2023).
* [15] J.J. Verlang, M.C. Hardin, J.R. Williams, Ammonia combustion properties and performance in gas-turbine burners, Symp. Combt. 11 (1967) 985-992.
* [16] B. Wang, C. Yang, H. Wang, D. Hu, B. Duan, Y. Wang, Study on injection strategy of ammonia/hydrogen dual fuel engine under different compression ratios, Fuel 334 (2023).
* [17] Lei Zhou LZ, Zongkuan Liu, Hiiqiao Wei. Toward highly-efficient combustion of ammonia-hydrogen engine: Prechamber turbulent jet ignition, **2023**.
* [18] J. Yang, C. Ji, A comparative study on performance of the rotary engine fueled hydrogen/gasoline and hydrogen/n-butanol, Int. J. Hydrogen Energy 43 (2018) 22669-22675.
* [19] A.A. Yontar, Effects of ethanol, methyl tert-butyl ether and gasoline-hydrogen blend on performance parameters and 1IC emission at Wankel engine, Hotels (2019).
* [20] P.M. Dimpelfeld, J.R. Mack. Design and Testing of a Natural Gas Fueled 5.8 Lifer Rquiry Engine, **1992**.;1.
* [21] H. Meng, C. Ji, G. Xin, J. Yang, K. Chang, S. Wang, Comparison of combustion, emission and abnormal combustion of hydrogen-to-feed Wankel rotary engine and reciprocating piston engine, Fuel 313 (2022) 12675.
* [22] H.B.V. Stutzenberger, R. van Bashshypers, F. Pitchinger, Suitability of rotary engines for hydrogen operation, Met z. 44 (1963).
* [23] K. Morimoto, T. Teramoto, Y. Takamori. Combustion characteristics in hydrogen fueled rotary engine, 1992.
* [24] H. Stutzenberger, INVESTIMATION OF THE OPERATING CHARACTERISTICS OF A HYDROGEN-PUELLED WANELENG, Gasoline. (1983).
* [25] H. Meng, C. Ji, Y. Su, J. Yang, K. Chang, G. Xin, et al., Analyzing characteristics of knock in hydrogen-enabled Wankel rotary engine, Energy 250 (2022) 123828.
* [26] B. Fan, X. Wu, J. Pan, X. Qi, J. Fang, Q. Liu, et al., Research on the structure of pre-chamber and jet orifice of a turbulent jet ignition rotary engine fueled with methanol/gasoline blends, Appl. Therm. Eng. 229 (2023).
* State-of-the-art and challenges, Int. J. Hydrogen Energy 60 (2024) 188-205.
* [28] Fan B, Song, A. Liu, W. Jiang, P. Xu, L. Pan, J. et al., Potential improvement in combustion performance of a natural gas rotary engine mixed with hydrogen by novel fluid-body, Energy. 2024.Fe31077,1-15.
* [29] B. Fan, Y. Zhang, J. Pan, Y. Wang, P. Ordner, Experimental and Numerical Study on the Formation Mechanism of Flow Field in a Side-Toward Range Engineering Considering Avea Scel Leakage, J. Energy Res. Technol. 143 (2020) 1-26.
* [30] Z.-N.-C. Yu-Tong Zhang, H.S. Do, et al., Effects of fuel ratio and ignition advance angle on the performance of ammonia-hydrogen engine. Journal of Changing University, of Technology 38 (2022) 2040-2047.
* [31] S.Z. Shengliwell, S. Yan, et al., Combustion characteristics of ammonia/hydrogen fuel jet ignition marine engine, J. X'an Jiaotong Univ. (2024).
* [32] J. Li, L. Wang, G. Shu, J. Pan, H. Wei, X. Hu, et al., ignition characteristics of ammonia-hydrogen passive pre-chamber: Emissions on equivalence ratio and hydrogen/ammonia ratio, Energy. Conner. Manage. 315 (2024).
* [33] D. Han, K. Song, J. Hua, X. Li, C. Xu, Combustion characteristics of ammonia-hydrogen mixture with turbulent jet ignition, Appl. Therm. Eng. (2024).
* [34] A. Jammetik, W. Tutuk, The impact of ammonia and hydrogen additives on the combustion characteristics, performance, stability and emissions of an industrial DI diesel engine, Appl. Therm. Eng. 257 (2024).
* [35] X. Wang, T. Li, X. Zhou, S. Huang, R. Chen, P. Yi, et al., Reductions in GHG and und undreumented ammonia of the pilot diesel-gated ammonia engines by diesel injection strategies, Appl. Therm. Eng. (2024).
* [36] X. Wang, J. Liu, W. Zhang, Q. Ji, L. P. Xiang, et al., Experimental investigation on in-cylinder working process and thermal efficiency of ammonia/diegal low-carbon engine with pre-injection strategy, Appl. Therm. Eng. 488 (2024).
* [37] B. Fan, Y. Zeng, J. Pan, J. Fang, H.A. Salam, V. Wang, Numerical study of injection strategy on the combustion process in a peripheral protect rotary engine fueled with natural gas/hydrogen blends under the action of apex seal leakage, Energy 242 (2022).
* [38] J. Obottal, S. Bhagwat, G. Mohan, Gdd mining's environmental footprints, drivers, and future predictions in Ghana. Remote Sens. Appl. Soc. Environ. 2024-33.
* [39] R. Fan, Y. Wang, J. Pan, Y. Zhang, Y. Zeng, Numerical Study on Flow Field in a Peripheral Ported Raysing Under the Action of Apex Soil Leakage, J. Fluids Eng. 143 (2020).
* [40] A.Cl, A.K. AC, ASW, A.J.Y, ADW, A.H, et al. Effect of injection strategy on the mixture formation and combustion process in a gasoline direct injection rotary engine, Fuel.304.
* [41] H. Meng, C. Ji, J. Yang, H. Wang, Z. Wang, S. Zambalov, et al., Performance analysis of the ammonia-enriched hydrogen-fanded Wankel rotary engine, Int. J. Hydrogen Energy 49 (2024) 462-472.
* Part 2: Spray combustion characteristics and combustion process under optimized injection strategies, Energy. Conner. Manage. 203 (2020).
* [43] Y. Liu, J. Pan, B. Fan, P. Ordner, W. Chen, B. Cheng, Research on the application of aviation response in a direct injection rotary engine-Part 1: Fundamental spray characteristics and optimized injection strategies, Energy. Conner. Manage. 195 (2019) 519-52.
* [44] W. Chen, J. Pan, Y. Liu, B. Fan, H. Liu, P. Ordner, Numerical investigation of direct injection stratified change combustion in a natural gas-diegal rotary engine, Appl. Energy 233-243 (2015) 653-667.
* [45] Z.-P. Jiang, J. Pan, P. Li, B. Fan, M. Naumann, W. Yang, Numerical study of the mixture formation and combustion process of an ammonia/hydrogen rotary engine, Int. J. Hydrogen Energy 69 (2024) 1469-1480.
* [46] G. Gotama, A. Hayakawa, E.C. Olafator, R. Kanoshima, M. Hayashi, T. Kudo, et al., Measurement of the laminar burning velocity and kinetics study of the importance of the hydrogen recovery mechanism of ammonia/hydrogen/air premited flames, Combt. Flame 236 (2022).
* [47] B. Fan, A. Song, W. Liu, P. Jiang, L. Xu, J. Pan, et al., Potential improvement in combination performance of a natural gas rotary engine mixed with hydrogen by novel fluid-body, Energy 295 (2024).
* [48] S.T.P. Purayal, M.O. Rhamda, S.A. Al-Omaari, M.V.E. Selim, E. Elasjjar, Influence of ethanol-guosoline-hydrogen and methanol-guosoline-hydrogen blends on the performance and hydrogen knock limit of a lean-burn spark ignition engine, Fuel 337 (2024).
* [49] R. Fan, X. Wu, J. Pan, Numerical investigation of the effect of jet orifice parameters on the combustion process of a turbulent jet ignition rotary engine fueled with methanol/gasoline blends, Fuel Process. Technol. (2023).