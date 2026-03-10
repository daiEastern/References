

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

Available online at [www.sciencedirect.com](http://www.sciencedirect.com)**ScienceDirect**journal homepage: [www.elsevier.com/locate/he](http://www.elsevier.com/locate/he)![Cover image of the International Journal of Hydrogen Energy](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the International Journal of Hydrogen Energy

![Check for updates icon](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates icon

# Effectiveness of hydrogen enrichment strategy for Wankel engines in unmanned aerial vehicle applications at various altitudes

Merve Kucuk<sup>a,\*</sup>, Ramazan Sener<sup>b</sup>, Ali Surmen<sup>c</sup>

<sup>a</sup> Department of Mechanical Engineering, Bursa Technical University, Bursa, 16310, Turkey

<sup>b</sup> Department of Marine Engineering, Bandirma Onyedi Eylul University, Balikesir, 10200, Turkey

<sup>c</sup> Department of Automotive Engineering, Bursa Uludag University, Bursa, 16059, Turkey

## H I G H L I G H T S

- A hydrogen-enriched Wankel engine for UAVs was simulated at various altitudes.
- The effectiveness of the hydrogen-enrichment on a Wankel engine was investigated.
- Performance parameters reduce with altitude yet enhance with hydrogen addition.
- Despite emissions worsening with altitude, they improve with hydrogen addition.

## A R T I C L E I N F O

### Article history:

Received 15 April 2023

Received in revised form

10 July 2023

Accepted 26 August 2023

Available online 16 September 2023

### Keywords:

CFD

Combustion

High altitude

Hydrogen enrichment

UAV

Rotary engine

## A B S T R A C T

This study investigates the effectiveness of the hydrogen-enrichment strategy on a Wankel engine for unmanned aerial vehicles (UAVs). The primary motivation behind this study is to contribute to the Wankel-type rotary engine designs by revealing the influences of the hydrogen enrichment method on the Wankel engine performance at various altitudes. To achieve these objectives, CFD simulations were conducted by applying a hydrogen enrichment method to a neat gasoline Wankel engine model at sea level, 5000 ft and 15,000 ft altitudes. The hydrogen energy fraction at the intake was gradually increased from 0% to 10%. The decrease in ambient air temperature, pressure, density, and insufficient fresh charge with the increase in altitude leads to the reduced reference chamber temperature and pressure of the Wankel engine. Thus, the combustion worsens, the heat release rate (HRR) and performance decrease, also emissions deteriorate in these colder operating conditions. On the other hand, the unique physicochemical properties of hydrogen such as wide flammability limits, high homogeneity, relatively small quenching distance and high flame speed allow hydrogen-enriched mixture flames to propagate toward the narrower gaps in the combustion chamber and make up for some drawbacks of Wankel engines. As a result, flame propagation is accelerated and fuel burning rate, peak pressure and temperature values in the reference chamber are increased by hydrogen addition. For the cases at sea level with 5% and 10% hydrogen energy fraction, IMEP is increased by 6.59%, 8.50%, and the indicated power is increased by 35.51% and 52.47%. In the cases with the same energy fraction at 15,000 ft, IMEP is increased by 26.61% and 48.75%, and the indicated power is reduced by 26.61% and 48.75%, respectively. It has been proven that a small amount of hydrogen by energy fraction improves combustion efficiency and performance. The findings show that hydrogen has excellent compatibility with

\* Corresponding author.

E-mail address: [merve.altay@btu.edu.tr](mailto:merve.altay@btu.edu.tr) (M. Kucuk).

<https://doi.org/10.1016/j.ijhydene.2023.08.304>

0360-3199/© 2023 Hydrogen Energy Publications LLC. Published by Elsevier Ltd. All rights reserved.

Wankel engines and hydrogen enrichment is a very practical concept for the improvement of the performance of these engines for UAVs. Thus, Wankel engines, which are already a very favorable power source for UAVs, become even more favorable by the hydrogen-blending strategy.

© 2023 Hydrogen Energy Publications LLC. Published by Elsevier Ltd. All rights reserved.

## 1. Introduction

The Wankel-type rotary engines are lightweight and have more compact designs with fewer components compared to reciprocating engines [1–3]. Since rotary motion can be obtained in Wankel engines directly, there is no need to convert reciprocating motion into rotational motion as in conventional piston engines. Furthermore, Wankel engines can provide favorable energy-to-weight and energy-to-size ratios even at high operating speeds. Due to these advantageous characteristics, Wankel engines have a broad range of applications, from the marine industry to the light aircraft industry. On the other hand, they have some drawbacks, such as, ring frictions, sealing problems, high heat transfer from the housing walls and high emissions. Many authors have conducted experimental [4–9] or numerical [10–17] studies to eliminate these drawbacks of the Wankel engine, enhance their performance and decrease emissions by reducing seal leakage, improving combustion, and minimizing heat loss in the working chambers. Wang et al. [18] developed a 1-D Wankel engine model considering gas leakage, especially from the apex seals. They discussed the influence of different leakage patterns on the volumetric efficiency of a hydrogen-fueled Wankel engine. Peden et al. [19] compared 1-D modeling approaches for the performance of the Wankel engine. They established a rotary engine model using AVL Boost as well. They applied low-pressure charge direct injection to their engine model to enhance the performance and fuel economy. Their simulation results, validated by experimental data, showed that the direct injection (DI) method improved the power output. Zou et al. [20] carried out numerical studies to investigate the knocking characteristics of a downsized rotary engine. They also analyzed auto ignition development under different inlet pressures. Rose and Yang [21] developed a new method named deviation function (DF). The contact between the housing and the apex seal was increased due to this method because they were designed as a conjugate pair. Therefore, their proposed method enhanced their engine efficiency and seal effectiveness. Since the combustion process was slower in Wankel engines than the others, combustion proceeded toward the expansion stroke. Cihan et al. [22] dealt with the heat release and combustion of four engines with different combustion chamber geometry (one was a Wankel engine, and the others were piston engines). They conducted experiments on these engines by changing engine speed and ambient pressure. The Wankel engine had the lowest cylinder pressure of any of these engines, and combustion occurred further away from the top-dead-center (TDC). Boughou et al. [23] examined the fluid flow characteristics of the Wankel combustion chamber using different computational fluid

dynamics (CFD) tools. They compared the effects of some design parameters, such as spark plug arrangement, recess size, and shape factor on Wankel engine performance. Hwang et al. [24] studied the effects of such parameters as spark plug location, ignition timing, and intake port location on combustion in a rotary engine. Their findings revealed that using two spark plugs in different ignition advances provided better combustion performance.

Some disadvantages and limitations of the Wankel engines that have prevented them from becoming as widespread as piston engines, can be disregarded in their UAV applications. For instance, sealing issues that are crucial in automobiles, especially in long-term use, can be negligible in kamikaze UAVs. Therefore, Wankel engines, which have many prominent features for UAVs such as high power to size ratio, are becoming progressively more popular over time and attracting the interest of many researchers. Furthermore, the growing demand for unmanned aerial vehicles (UAVs) in the Defense Industry over the over the past twenty-five years has established a new and alternative field for Wankel engines. Boretti [25] evaluated the advantages and challenges of using the Wankel engine for UAV applications. They used CAE and CFD models of a Wankel engine to determine engine characteristics. Incomplete and slow combustion due to low combustion chamber temperatures at high altitudes was presented as the main problem of these engines. Also, in their subsequent work, they developed a new jet ignition system for the Wankel engine, which is used in UAVs instead of traditional spark ignition systems to achieve complete combustion. Numerical analyzes were performed on the CFD model of the Wankel engine to demonstrate the feasibility and difficulties of this system. The effects of rapid and more complete combustion allowed by jet ignition UAVs were evaluated. Finkelberg et al. [26] numerically examined the Wankel engine's combustion properties for aviation applications. Their simulation results revealed that there is a significant role of the geometry of the rotor recess on the engine performance. In order to enhance the Wankel engine performance, they offered an alternative chamber geometry. Spreitzer et al. [27] developed a Wankel engine CFD model using Converge CFD software. They confirmed the well-known disadvantages and problems (low thermal efficiency, high emissions) of the Wankel engines and suggested some solutions to these problems. Additionally, they set up a rotary engine test bench and developed a methodology for the simulation tool, validated by experimental results.

Current research studies have revealed that the methods aiming to improve fuel properties and mixture formation in the Wankel engines have significant effects in mitigating many of their drawbacks [28–39]. As a result, the disadvantages of Wankel engines such as misfire issues and reduced engine

performance at higher altitudes in their UAV applications, have been improved and the utilization benefits of Wankel engines in UAVs have been further enhanced. One of the most effective methods for improving performance by enhancing combustion in Wankel engines is the utilization of hydrogen addition. Considering the problem of hydrogen storage and transportation, hydrogen is preferred as an auxiliary fuel to improve the main fuel combustion. In addition, hydrogen addition to the Wankel engines is more suitable compared to the piston engines [40]. Fan et al. [41] studied the impacts of different hydrogen injection methods on Wankel engine performance. They compared two injection methods: direct injection of hydrogen and port injection of natural gas. Amrouche et al. [42] conducted experimental studies using a rotary engine fueled with neat gasoline and they modified their engine with hydrogen enrichment method. Yang and Fan examined in-cylinder flame propagation numerically in their studies [43–47]. They revealed that utilizing the hydrogen addition method in the rotary engine increased flame propagation velocity and eliminated the incombustible region at the combustion chamber's rear side. Su et al. investigated the effects of hydrogen enrichment on the combustion process of a gasoline fueled rotary engine [30,48,49]. They conducted experimental examination of hydrogen's role in improving combustion under various operating conditions. They utilized a modified hydrogen-gasoline dual-fuel rotary engine equipped with an electronically controlled fuel injection system. Their overall results showed that hydrogen addition had a prominent effect on the combustion stability of the gasoline rotary engine and improving its performance. Gao et al. [50] performed a numerical study to explore the equivalence ratio effects on the combustion and emission characteristics of the hydrogen-added opposed rotary piston engines (ORP). Their simulation results revealed the impact of the equivalence ratio on combustion and emissions of their engine under the specific operating conditions. Yang and Ji [51] carried out a comparative study to evaluate the performance of hydrogen/n-butanol and hydrogen/gasoline fueled rotary engines. Their results demonstrated that hydrogen enrichment had a positive impact on the performance of both gasoline and n-butanol rotary engines. The hydrogen/n-butanol rotary engine exhibited similar performance to the hydrogen/gasoline rotary engine. Meng et al. [52] discussed the potential of hydrogen/methane dual-fueled Wankel rotary engines in their study. They highlighted that using dual fuel was beneficial compared to using a single fuel in terms of engine power and emissions. Ji et al. [53] focused on the impact of intake modes on mixture formation and combustion efficiency in the hydrogen blended Wankel engine. Yontar [54] carried out experimental research to examine the effects of gasoline, methyl tert-butyl ether, ethanol and a gasoline-hydrogen mixture on a Wankel engine performance and its hydrocarbon emissions. Hsieh et al. [55] studied on hydrogen-fueled rotary engines, including the triangular rotary engine and liquid piston engine. They examined and compared the internal flow characteristics of these engines.

The effectiveness of hydrogen enrichment methods on the Wankel engine at various altitudes should be considered to offer a power source design suitable for UAV applications. However, as noted above, studies on hydrogen addition to

rotary engines for UAV applications have generally been conducted under sea-level conditions. There has yet to be an attempt to examine neat gasoline fueled Wankel engine performance at high altitudes. Even the studies investigating the effects of altitude increase on reciprocating engines [56–60], which have been discussed in all aspects for years, are also limited. Moreover, studies on Wankel engines are often performed by modeling a single combustion chamber of the Wankel engine to reduce computational cost. Due to its unique geometry, there is an interaction between the sequential combustion chambers of the Wankel engine. Therefore, performing analyses on a full Wankel engine model with three chambers is another important factor to ensure a more accurate engine design.

The aforementioned gaps in the existing literature have been addressed by the presented study. Therefore, this study differs from the previous studies in that it numerically finds out the potential of the hydrogen enrichment concept on the Wankel engine for UAV applications at various altitudes using a full engine model.

The main objectives of the present study are as follows:

1. Revealing the effects of the altitude on the combustion behavior, performance characteristics and emissions of a Wankel-type rotary engine.
2. Investigating the effectiveness of the hydrogen-enrichment method on combustion efficiency and performance of a Wankel engine.
3. Contributing to the Wankel engine designs for UAVs, by demonstrating the potential of the hydrogen enrichment method on a Wankel engine performance at various altitudes.

The rest of this paper takes the following form. CFD model establishment and validation of the Wankel research engine are provided in the next section. Following this, the results are presented and subsequently discussed. Finally, the main findings are summarized, and conclusions are drawn.

## 2. CFD model establishment and validation

### 2.1. Geometrical model

The research engine in the present study is a gasoline-fueled, single-rotor, air/oil-cooled, naturally aspirated four-stroke Wankel engine. This aviation Wankel engine and some of the test data of it were supplied by LENTATEK. It is located at the ICEs Laboratory of the Bursa Uludag University and is shown in Fig. 1.

The Wankel research engine's CAD and CFD mesh models are demonstrated in Fig. 2. Eccentricity, parallel transfer trochoid length and generating radius of the presented engine are 11.5 mm, 1.05 mm and 71.89 mm. The k-factor and generating radius ( $R_g$ ) values were calculated as;  $k\text{-factor} = (R_g)/e$  and  $R_g = (R+a)$ , respectively [27].

The air/oil-cooled research engine has a 9.6 compression ratio. It has two spark plugs with a sphere radius of 1.0 mm. Some engine specifications of the research engine are listed in Table 1.

![Figure 1: Research engine. (a) Definition of some parts: exhaust manifold, coolant channel, air pump drive, engine air entry, torque reducer, and alternator. (b) Disassembled engine showing various components laid out on a table.](ddfe517a5ad9c77c89a57a5e780b24ca_img.jpg)

Figure 1: Research engine. (a) Definition of some parts: exhaust manifold, coolant channel, air pump drive, engine air entry, torque reducer, and alternator. (b) Disassembled engine showing various components laid out on a table.

Fig. 1 – Research engine (a) Definition of some parts, (b) Disassembled engine.

![Figure 2: Demonstration of (a) CAD model and (b) CFD mesh model of the Wankel research engine. (a) shows a cross-sectional CAD model with coordinate axes. (b) shows a detailed CFD mesh model with labels for Exhaust outlet, Minor Axis, and Intake inlet.](b615ff07e8a0f467f0a6f4783c4463eb_img.jpg)

Figure 2: Demonstration of (a) CAD model and (b) CFD mesh model of the Wankel research engine. (a) shows a cross-sectional CAD model with coordinate axes. (b) shows a detailed CFD mesh model with labels for Exhaust outlet, Minor Axis, and Intake inlet.

Fig. 2 – Demonstration of (a) CAD model, (b) CFD mesh model of the Wankel research engine.

**Table 1 – Research engine specifications.**

| Engine Type                                 | Rotary engine   |
|---------------------------------------------|-----------------|
| Radius, R [mm]                              | 71.89           |
| Generating Radius, ( $R_g$ )                | 72.94           |
| Parallel transfer trochoid length, (a) [mm] | 1.05            |
| k-factor                                    | 6.34            |
| Eccentricity (e) [mm]                       | 11.5            |
| Width [mm]                                  | 74.4            |
| Inlet/outlet ports                          | In the trochoid |
| Power [kW]                                  | 35 @ 6000 rpm   |
| Rotor cooling                               | Air             |
| Housing cooling                             | Water           |
| Spark plugs radius[mm]/shape                | 1/Sphere        |

### 2.2. Boundary conditions

CFD simulations were performed on the Wankel research engine at different hydrogen mass fractions and altitudes of 0 ft, 5000 ft, and 15,000 ft (0 m, 1524.0 m, and 4572.0 m). These altitudes correspond to the typical altitude ranges in UAV flight operations. Performing Wankel engine simulations for the altitudes frequently preferred in UAV operations facilitates informed decision-making regarding Wankel engine design, adjustments, and operational parameters, ultimately

leading to optimum performance and efficiency in its UAV applications.

The fluid domain of the research engine was imported to the CFD software as a surface file. The surfaces of the research engine are demonstrated schematically in Fig. 3.

Temperature values of the housing and rotor walls at sea level were adjusted to 443 K and 488 K, respectively. The surface temperature of the two plugs, located on the minor axis and in the same position, was set to 625 K. These spark plugs' energy was 0.03 and 0.04 J. Inlet pressures and temperatures of the intake port at various altitudes are given in Fig. 4.

Isooctane ( $IC_8H_{18}$ ) was used as the primary fuel in simulations, this fuel is commonly used in simulations as a proxy for gasoline; furthermore, it was assumed that the mixture was homogeneous. Hydrogen was employed as an auxiliary fuel. The hydrogen added was modeled as pure and supposed to be stored in the liquid form. The fuel supply method adopted for the Wankel research engine involved port injection of a dual fuel mixture of gasoline and hydrogen. For intake port injection, the injected fuels (gasoline and hydrogen) mixed with air in the intake port, resulting in a homogeneous mixture in the combustion chamber that was easy to ignite [38,61,62]. The energy fractions of hydrogen in the intake inlet were adjusted as hydrogen input in the CFD model, and this value differed from 0% to 10% in the simulated cases.

![Fig. 3 – Schematic demonstration of the research engine surfaces. The diagram shows a cross-section of a Wankel engine. It features a triangular rotor inside a housing with three curved sides. The rotor is divided into three chambers (Chamber 1, Chamber 2, Chamber 3). Key components labeled include the Exhaust port, Intake port, Housing sides, Rotor, Rotor flank 2, and Spark plugs. A coordinate system (Y, X, Z) is shown in the bottom left corner.](edd10d3006553f0a7a5a7f844ed8cd01_img.jpg)

Fig. 3 – Schematic demonstration of the research engine surfaces. The diagram shows a cross-section of a Wankel engine. It features a triangular rotor inside a housing with three curved sides. The rotor is divided into three chambers (Chamber 1, Chamber 2, Chamber 3). Key components labeled include the Exhaust port, Intake port, Housing sides, Rotor, Rotor flank 2, and Spark plugs. A coordinate system (Y, X, Z) is shown in the bottom left corner.

**Fig. 3 – Schematic demonstration of the research engine surfaces.**

Mass flow rates corresponding to 0%, 5% and 10% of the energy fractions of hydrogen in the mixture are set as hydrogen input in the CFD model. Table 2 shows the mass flow rates of the hydrogen and iso-octane fuels in the mixture ( $\dot{m}_{H_2}$  and  $\dot{m}_{C_8H_{18}}$ ) of the simulations. In the given table “S” represents the cases at sea level (0 ft), “L” represents the cases at 5000 ft, and “H” represents the cases at 15,000 ft.

Some boundary conditions and operating parameters of the Wankel research engine are summarized in Table 3.

The equivalence ratio of the hydrogen enriched iso-octane (representing gasoline) and air mixture was calculated by Eq. (1) [31,42,63];

$$\lambda = \dot{m}_{air} / (\dot{m}_{C_8H_{18}} \cdot AF_{st,C_8H_{18}} + \dot{m}_{H_2} \cdot AF_{st,H_2}) \quad (1)$$

where  $\dot{m}_{air}$ ,  $\dot{m}_{C_8H_{18}}$  and  $\dot{m}_{H_2}$  are the mass flow rates (kg/h) of air, iso-octane and hydrogen, respectively.  $AF_{st,C_8H_{18}}$  and  $AF_{st,H_2}$  represent the stoichiometric air-fuel ratios of iso-octane and hydrogen ( $AF_{st,C_8H_{18}} = 14.7$  and  $AF_{st,H_2} = 34.3$ ).

Hydrogen energy contribution in the intake is expressed as energy fraction of hydrogen and calculated as follows;

$$H_2\% = \left[ \frac{\dot{m}_{H_2} \cdot LHV_{H_2}}{(\dot{m}_{C_8H_{18}} \cdot LHV_{C_8H_{18}}) + (\dot{m}_{H_2} \cdot LHV_{H_2})} \right] \times 100 \quad (2)$$

**Table 2 – Fuels' mass flow rates in the mixtures of the simulated cases.**

| Cases | Altitude [ft] | Reference chamber $H_2\%$ | Mass flow rates of the fuels |                        |
|-------|---------------|---------------------------|------------------------------|------------------------|
|       |               |                           | $\dot{m}_{C_8H_{18}}$ [kg/h] | $\dot{m}_{H_2}$ [kg/h] |
| S0    | 0 ft          | 0%                        | 11.88                        | 0.00                   |
| S5    | 0 ft          | 5%                        | 10.42                        | 0.55                   |
| S10   | 0 ft          | 10%                       | 9.18                         | 1.02                   |
| L0    | 5000 ft       | 0%                        | 8.33                         | 0.00                   |
| L5    | 5000 ft       | 5%                        | 7.91                         | 0.16                   |
| L10   | 5000 ft       | 10%                       | 7.50                         | 3.10                   |
| H0    | 15,000 ft     | 0%                        | 4.43                         | 0.00                   |
| H5    | 15,000 ft     | 5%                        | 4.21                         | 0.08                   |
| H10   | 15,000 ft     | 10%                       | 3.99                         | 0.16                   |

**Table 3 – Some boundary conditions and operating parameters of the Wankel research engine.**

| Subject                                      | Input                        |
|----------------------------------------------|------------------------------|
| Compression ratio                            | 9.6                          |
| Energy of spark plugs                        | 0.03 and 0.04 J              |
| Surface temperature of spark pugs            | 625 K                        |
| Surface temperatures of intake/exhaust ports | 323 K/500 K                  |
| Wall temperatures of rotor/housing           | 488 K/433 K                  |
| Pressure-velocity coupling                   | PISO algorithm               |
| Mesh method                                  | Modified cut-cell cartesian  |
| Reaction mechanism                           | 152 reactions and 48 species |

Where  $LHV_{H_2}$  and  $LHV_{C_8H_{18}}$  represent the lower heating value of hydrogen and iso-octane, respectively ( $LHV_{H_2} = 120.1$  MJ/kg and  $LHV_{C_8H_{18}} = 44.651$  MJ/kg). Energy fractions of the fuels in the intake charge used in the CFD simulated cases are summarized in Fig. 5.

Hydrogen-gasoline blends in the simulated cases were assumed to be perfectly mixed before the intake process. The air-fuel mixture in the mixture was kept at stoichiometric condition ( $\lambda = 1$ ). For the cases at the same altitude, the total energy of the mixtures was kept the same as seen in Fig. 5; however, each of these cases had different hydrogen energy fractions. Total energy fractions of fuel were  $5.30 \times 10^5$ ,  $3.72 \times 10^5$ ,  $1.98 \times 10^5$  [kJ/h] for the cases at the altitudes of 0 ft (S0, S5, S10), 5000 ft (L0, L5, L10), and 15000 ft (H0, H5, H10), respectively.

![Fig. 4 – Pressure and temperature values of the intake port at various altitudes. (a) Inlet pressure: A line graph showing Intake Port Pressure [bar] vs. Eccentric Shaft Angle [°EA] for 0 ft (blue), 5000 ft (red), and 15000 ft (green). Pressure is relatively constant around 0.9-1.0 bar for 0 ft, 0.6 bar for 5000 ft, and 0.3 bar for 15000 ft. (b) Inlet temperature: A line graph showing Intake Port Temperature [K] vs. Eccentric Shaft Angle [°EA] for the same altitudes. Temperature is relatively constant around 285 K for 0 ft, 260 K for 5000 ft, and 235 K for 15000 ft.](0f92e96694face0b13a687ec21fb9101_img.jpg)

Fig. 4 – Pressure and temperature values of the intake port at various altitudes. (a) Inlet pressure: A line graph showing Intake Port Pressure [bar] vs. Eccentric Shaft Angle [°EA] for 0 ft (blue), 5000 ft (red), and 15000 ft (green). Pressure is relatively constant around 0.9-1.0 bar for 0 ft, 0.6 bar for 5000 ft, and 0.3 bar for 15000 ft. (b) Inlet temperature: A line graph showing Intake Port Temperature [K] vs. Eccentric Shaft Angle [°EA] for the same altitudes. Temperature is relatively constant around 285 K for 0 ft, 260 K for 5000 ft, and 235 K for 15000 ft.

**Fig. 4 – Pressure and temperature values of the intake port at various altitudes (a) inlet pressure, (b) inlet temperature.**

![Bar chart showing Total Energy of Fuel [kJ/h] for Gasoline and Hydrogen across various cases at 0 ft, 5000 ft, and 15000 ft altitudes. Gasoline is represented by red bars and Hydrogen by blue bars. The cases are S0, S5, S10, L0, L5, L10, H0, H5, and H10.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

| Case | Altitude | Gasoline (kJ/h) | Hydrogen (kJ/h) |
|------|----------|-----------------|-----------------|
| S0   | 0 ft     | ~5.2E+05        | 0               |
| S5   | 0 ft     | ~5.1E+05        | ~0.5E+05        |
| S10  | 0 ft     | ~5.1E+05        | ~0.5E+05        |
| L0   | 5000 ft  | ~3.6E+05        | 0               |
| L5   | 5000 ft  | ~3.5E+05        | ~0.4E+05        |
| L10  | 5000 ft  | ~3.5E+05        | ~0.4E+05        |
| H0   | 15000 ft | ~2.0E+05        | 0               |
| H5   | 15000 ft | ~2.0E+05        | ~0.2E+05        |
| H10  | 15000 ft | ~2.0E+05        | ~0.2E+05        |

Bar chart showing Total Energy of Fuel [kJ/h] for Gasoline and Hydrogen across various cases at 0 ft, 5000 ft, and 15000 ft altitudes. Gasoline is represented by red bars and Hydrogen by blue bars. The cases are S0, S5, S10, L0, L5, L10, H0, H5, and H10.

**Fig. 5 – Energy fractions of hydrogen and gasoline in the mixtures of the simulated cases.**

### 2.3. Modelling procedure

The presented simulations were performed in the multi-dimensional domain using the Converge CFD commercial code. The solution algorithm of the transport equations is essential for simulation parameters configuration. The modified Pressure Implicit with Splitting of Operator (PISO) algorithm starts with a prediction stage in which the momentum equation is solved [35,64]. Then, the pressure equation is solved to correct the momentum equation. Resolving and correcting processes of the momentum equation are reiterated to reach convergence. Then, other transport equations are solved [64–66].

The appropriate turbulence model should be selected for the simulation accuracy of the in-cylinder flows of rotary engines. The RNG k- $\epsilon$  turbulence model was adopted to the model. It can be assumed that this turbulence model is well applied to Wankel engines and is in good agreement with the experimental data considering related studies in the literature [67,68]. Fig. 6 shows the general form of the transport equations utilized in this study.

A detailed chemical kinetics solver (SAGE) was preferred as the combustion model in the simulated CFD models. The SAGE model is a general combustion model including adaptive zoning and solving the chemical reaction equations in detail during the combustion [69]. The SAGE model divides chemistry cells into regions and solves the chemistry once per region instead of once per cell, thanks to its adaptive zoning feature.

Combustion regions were defined in the simulation setup process because of the considerable pressure and temperature variations between each chamber of the Wankel engine. To simulate gasoline oxidation, a chemical reaction mechanism was applied to the simulations for primary reference fuel (PRF), which is commonly used in gasoline fuel research [70]. The selected reaction mechanism for the simulations, which contains 48 species and 152 reactions, was developed by Jia et al. [71]. It was assumed that the fuel was evaporated completely, and the air/fuel mixture was homogeneous.

The thermal NO<sub>x</sub> mechanism depends on the reaction temperature. When the local temperature reaches the specific value (~2200 K), NO<sub>x</sub> forms. The expanded Zeldovich model was used to calculate NO formation [35].

### 2.4. Grid selection and independence study

During the simulations, Converge CFD software automatically generate grids at run-time and the computational domain is re-meshed for moving boundaries at each time step. In the grid generation process in this study, modified cut-cell cartesian method was applied. In addition, the fixed embedding and the adaptive mesh refinement (AMR) techniques have been applied to the presented Wankel engine CFD model. Fixed embedding technique was used for grid generations on the critical locations such as surfaces of its rotor blades, housing and spark plugs. AMR technique was utilized for grid generation in the regions characterized by high species concentration and turbulent flame front gradients. Grid structures at critical locations in the CFD domain was refined by means of fixed embedding method. Grid size based on moving and fluctuating boundary conditions such as velocity, or temperature was controlled by AMR method [64]. Selecting the appropriate mesh size and method in the CFD model is very significant for a better resolution of temperature and velocity gradients, thereby improving the simulation accuracy and reducing computational cost. A grid independence study was performed for the mesh model of the reference engine (the engine with 6000 rpm at 0 ft altitude). Within the scope of the grid independence check, four grid structures named finer, fine, medium, and coarse were used separately in each test. These grid structures (finer, fine, medium, coarse) were constructed with a base grid size of 1 mm, 2 mm, 3 mm, and 4 mm, respectively, with the fixed embedding and AMR

![Diagram showing the General Form of Transport Equations branching into Continuity Equation, Momentum Equation, and Energy Equation. The RNG k-epsilon Turbulence Model Equations are shown on the right, including the k and epsilon equations.](68ca7669d38a3c31f5a2c3a06fa802e3_img.jpg)

**General Form of Transport Equations**

**Continuity Equation**

$$\frac{\partial \rho}{\partial t} + \frac{\partial \rho \bar{u}_j}{\partial x_j} = 0$$

**Momentum Equation**

$$\frac{\partial \rho \bar{u}_i}{\partial t} + \frac{\partial \rho \bar{u}_i \bar{u}_j}{\partial x_j} = -\frac{\partial \bar{P}}{\partial x_i} + \frac{\partial}{\partial x_j} \left[ \mu \left( \frac{\partial \bar{u}_i}{\partial x_j} + \frac{\partial \bar{u}_j}{\partial x_i} \right) - \frac{2}{3} \mu \frac{\partial \bar{u}_k}{\partial x_k} \delta_{ij} \right] + \frac{\partial}{\partial x_j} (-\rho \bar{u}_i \bar{u}_j) + S$$

**Energy Equation**

$$\frac{\partial \rho e}{\partial t} + \frac{\partial \rho e \bar{u}_j}{\partial x_j} = -P \frac{\partial \bar{u}_j}{\partial x_j} + \frac{\partial}{\partial x_j} \left( K \frac{\partial T}{\partial x_j} \right) + \sigma_{ij} \frac{\partial \bar{u}_i}{\partial x_j} + \frac{\partial}{\partial x_j} \left( \rho \sum_m D_{m} h_m \frac{\partial Y_m}{\partial x_j} \right) + S$$

**RNG k- $\epsilon$  Turbulence Model Equations**

k (Turbulent kinetic energy) Equation

$$\frac{\partial \rho k}{\partial t} + \frac{\partial \rho \bar{u}_j k}{\partial x_j} = \tau_{ij} \frac{\partial \bar{u}_i}{\partial x_j} + \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_k} \frac{\partial k}{\partial x_j} \right) - \rho \bar{e} + \frac{C_\epsilon}{1.5} S_k$$

$\epsilon$  (Dissipation of turbulent kinetic energy) Equation

$$\frac{\partial \rho \epsilon}{\partial t} + \frac{\partial (\rho \bar{u}_j \epsilon)}{\partial x_j} = \frac{\partial}{\partial x_j} \left( \frac{\mu + \mu_t}{Pr_\epsilon} \frac{\partial \epsilon}{\partial x_j} \right) + C_{\epsilon 1} \rho \bar{e} \frac{\partial \bar{u}_i}{\partial x_j} + \left( C_{\epsilon 1} \frac{\partial \bar{u}_i}{\partial x_j} \tau_{ij} - C_{\epsilon 2} \rho \bar{e} + C_{\epsilon 3} S_k \right) \frac{\epsilon}{k} + S - \rho R_\epsilon$$

Diagram showing the General Form of Transport Equations branching into Continuity Equation, Momentum Equation, and Energy Equation. The RNG k-epsilon Turbulence Model Equations are shown on the right, including the k and epsilon equations.

**Fig. 6 – Transport equations.**

![Figure 7: Grid independence test results. (a) Reference chamber pressure vs. Eccentric Shaft Angle. (b) Heat Release Rate (HRR) vs. Eccentric Shaft Angle. Both plots show results for Finer, Fine, Medium, and Coarse grid structures, with the 'Fine' grid showing the highest accuracy.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 7 consists of two line graphs. Graph (a) plots 'Ref. Chamber Pressure [bar]' on the y-axis (0 to 40) against 'Eccentric Shaft Angle [°EA]' on the x-axis (180 to 630). It shows four curves for different grid sizes: Finer (yellow), Fine (blue), Medium (red), and Coarse (green). All curves peak at approximately 35 bar at 360°EA, which is marked as TDC. Graph (b) plots 'HRR [J/°EA]' on the y-axis (0 to 30) against 'Eccentric Shaft Angle [°EA]' on the x-axis (315 to 495). It shows the same four grid sizes. The curves peak at approximately 25 J/°EA at 390°EA, also marked as TDC.

Figure 7: Grid independence test results. (a) Reference chamber pressure vs. Eccentric Shaft Angle. (b) Heat Release Rate (HRR) vs. Eccentric Shaft Angle. Both plots show results for Finer, Fine, Medium, and Coarse grid structures, with the 'Fine' grid showing the highest accuracy.

**Fig. 7 – Grid independence test results (a) reference chamber pressure, (b) HRR.**

methods. All the properties of these grid structures, except grid size, were kept the same. Pressure and HRR values of different grid structures are compared with each other, as seen in Fig. 7.

The best balance between the grid mesh performance parameters, such as simulation accuracy, data set resolution, and computational cost, was obtained with the "fine" grid structure. Therefore, the "fine" grid was selected for the simulations.

### 2.5. Model validation

In the present study, CFD simulations of the four-stroke Wankel engine were carried out with a full engine model. The Wankel engine CFD case with 6000 rpm engine speed and at sea level condition was assumed to be a baseline case (S0 case). Pressure and HRR results of the baseline case were compared with those of the experimental findings of Spreitzer et al. [27]. When developing the solid model and constructing the CFD model in this study, all structural details were considered and preserved. It is noteworthy that there was a cavity on the outer body for the spark plug. Naturally, there happens a charge leakage during the travel of rotor over this gap between 180°EA and 205°EA. Consequently, the estimated values from the model appear slightly lower than the experimental data, as observed in Fig. 8(a). Nevertheless, the simulated reference chamber pressure results at 6000 rpm under sea level conditions exhibit good consistency with the experimental findings. According to the HRR results in Fig. 8(b), the combustion in the simulation seems faster than in the experiments. The primary

cause of this discrepancy is that the residual exhaust temperature in the combustion chamber and heat emission of the special coating on the actual rotary surface and rotary pocket was ignored in the simulation. However, the discrepancy between the HRR results was within the acceptable level. In general, these validations proved that the Wankel engine CFD model used here could predict the reference Wankel engine performance with satisfying accuracy. The effects of engine operation at various altitudes and different fuel content on the combustion process and performance characteristics were investigated based on the model validated.

## 3. Results and discussion

This study aims to demonstrate the high-altitude influence on performance, combustion, and emission characteristics of the Wankel engine. Wankel engine CFD simulations with different hydrogen enrichment levels and at different altitudes were performed here, and these simulation results were compared with the baseline case's simulation results. Although the simulations were performed utilizing a full-engine geometry with three combustion chambers, "Chamber 2" was chosen as a reference chamber. Only the "Chamber 2" results were discussed here to avoid repetition.

### 3.1. Combustion analysis

The combustion duration and flame development period are strong indicators of the Wankel engine combustion quality

![Figure 8: CFD model validation results. (a) Reference chamber pressure vs. Eccentric Shaft Angle. (b) Heat Release Rate (HRR) vs. Eccentric Shaft Angle. Both plots compare Experimental data (red dashed line) with CFD results (blue solid line).](4ae1b32e57b3072ef112b19e647dfead_img.jpg)

Figure 8 consists of two line graphs. Graph (a) plots 'Ref. Chamber Pressure [bar]' on the y-axis (0 to 40) against 'Eccentric Shaft Angle [°EA]' on the x-axis (180 to 630). It compares 'Experimental' data (red dashed line) with 'CFD' results (blue solid line). Both curves peak at approximately 35 bar at 360°EA, marked as TDC. Graph (b) plots 'HRR [J/°EA]' on the y-axis (0 to 30) against 'Eccentric Shaft Angle [°EA]' on the x-axis (315 to 495). It compares 'Experimental' data (red dashed line) with 'CFD' results (blue solid line). The CFD results show a higher peak HRR of approximately 25 J/°EA at 390°EA, while the experimental data peaks at approximately 22 J/°EA at 380°EA.

Figure 8: CFD model validation results. (a) Reference chamber pressure vs. Eccentric Shaft Angle. (b) Heat Release Rate (HRR) vs. Eccentric Shaft Angle. Both plots compare Experimental data (red dashed line) with CFD results (blue solid line).

**Fig. 8 – CFD model validation results (a) reference chamber pressure, (b) HRR [27].**

![Figure 9: Comparison of EA10, EA50, and EA90 times and combustion duration at various altitudes. (a) EA10, EA50, EA90 at sea level (S0, S5, S10). (b) EA10, EA50, EA90 at 5000 ft (L0, L5, L10). (c) EA10, EA50, EA90 at 15,000 ft (H0, H5, H10). (d) Combustion duration at 0 ft, 5000 ft, and 15,000 ft for 0% H2, 5% H2, and 10% H2.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 9 consists of four subplots (a, b, c, d) showing the relationship between eccentric shaft angle (EA) and combustion duration at different altitudes and hydrogen enrichment levels.

**(a) EA10, EA50, EA90 at sea level (S0, S5, S10):**

| Altitude  | Case | EA10 [°EA] | EA50 [°EA] | EA90 [°EA] |
|-----------|------|------------|------------|------------|
| Sea Level | S0   | ~350       | ~350       | ~350       |
|           | S5   | ~350       | ~380       | ~380       |
|           | S10  | ~350       | ~380       | ~400       |

**(b) EA10, EA50, EA90 at 5000 ft (L0, L5, L10):**

| Altitude | Case | EA10 [°EA] | EA50 [°EA] | EA90 [°EA] |
|----------|------|------------|------------|------------|
| 5000 ft  | L0   | ~350       | ~350       | ~350       |
|          | L5   | ~350       | ~380       | ~380       |
|          | L10  | ~350       | ~380       | ~400       |

**(c) EA10, EA50, EA90 at 15,000 ft (H0, H5, H10):**

| Altitude  | Case | EA10 [°EA] | EA50 [°EA] | EA90 [°EA] |
|-----------|------|------------|------------|------------|
| 15,000 ft | H0   | ~350       | ~350       | ~350       |
|           | H5   | ~350       | ~380       | ~380       |
|           | H10  | ~350       | ~380       | ~400       |

**(d) Combustion Duration [°EA] vs Altitude (0 ft, 5000 ft, 15,000 ft) for 0% H<sub>2</sub>, 5% H<sub>2</sub>, and 10% H<sub>2</sub>:**

| Altitude  | 0% H <sub>2</sub> [°EA] | 5% H <sub>2</sub> [°EA] | 10% H <sub>2</sub> [°EA] |
|-----------|-------------------------|-------------------------|--------------------------|
| 0 ft      | ~88                     | ~72                     | ~68                      |
| 5000 ft   | ~92                     | ~80                     | ~74                      |
| 15,000 ft | ~95                     | ~84                     | ~80                      |

Figure 9: Comparison of EA10, EA50, and EA90 times and combustion duration at various altitudes. (a) EA10, EA50, EA90 at sea level (S0, S5, S10). (b) EA10, EA50, EA90 at 5000 ft (L0, L5, L10). (c) EA10, EA50, EA90 at 15,000 ft (H0, H5, H10). (d) Combustion duration at 0 ft, 5000 ft, and 15,000 ft for 0% H2, 5% H2, and 10% H2.

**Fig. 9 – Comparison of EA10, EA50, and EA90 times (a) at sea level, (b) at 5000 ft, (c) at 15,000 ft (d) combustion duration at various altitudes.**

[72]. EA10, EA50, and EA90 times and combustion durations of the simulated cases are presented in Fig. 9 to determine the combustion behavior in the combustion chamber of the simulated cases. EA10 and EA90 represent the eccentric shaft angle where 10% and 90% of the total heat release occurs, respectively. These two parameters can be assumed to be the start and end of the combustion in the combustion chamber. The duration from ignition timing to 10% total heat release and the duration from total heat release of 10%–90% are named the flame development period (EA0-10) and combustion duration (EA10-90), respectively [9].

EA10-90 value of the S0 case (baseline case) is 89.77 ° EA, and this value is increased by 18.40% and 23.41% for the S5 case and the S10 case. EA10-90 value of the L0 case is 93.13 ° EA, and this value is increased by 14.09% and 20.12% for L5 and L10. EA10-90 value of the H0 case is 96.00 ° EA, and this value is increased by 12.71% and 16.36% for the H5 case and the H10 case.

When the results are evaluated in terms of altitude increase, it is clear from Fig. 9(d) that the combustion duration, in the cases with the same fuel content (e.g., S0, L0, H0), increases as the altitude increases. With a prolonged flame development period (EA0-10) and postponed ending of combustion (EA90) at higher altitudes, it is obvious from the simulation results of Fig. 9 that combustion duration (EA10-90) is extended at higher altitude cases [72].

On the other hand, it is seen from Fig. 9(a)–(c) that EA10 is advanced as the hydrogen enrichment levels increase. Therefore, it is obvious from the figure that the flame development period is shortened in the hydrogen-blended cases compared with that of the baseline case. The low ignition energy, high diffusivity properties of the mixture contribute to

the shortening of the flame development and propagation durations [30]. The existence of such a particularly reactive fuel as hydrogen in the mixture can give it such distinct properties. Another factor shortening the flame development period is reducing the homogeneity fluctuations combustion chamber due to hydrogen's high molecular diffusion coefficient [35].

Investigating the reference chamber temperature, pressure, and HRR changes due to the altitude increase is vital for the Wankel engine designs for UAVs. Because the high surface-to-volume ratio of the Wankel engine causes very high heat transfer from the housing walls. Furthermore, the long and narrow geometry of the rotary engine combustion chamber worsens heat losses and inhibits heat utility. As the altitude increases in the Wankel engine UAV applications, the increasing temperature differences between the ambient temperature and the combustion chamber make the aforementioned adverse effects more pronounced. For these reasons, the impacts of altitude increase on the parameters in Fig. 10 are examined first, and then the influence of hydrogen addition on these parameters are evaluated.

- The influences of altitude increase on temperature, pressure and HRR of the reference chamber;

According to the reference chamber pressure data from Fig. 10(a)–(c), the peak pressure is observed slightly earlier and closer to the TDC at sea level than at high altitudes. In addition, the peak pressure values in the reference chambers, with the same fuel contents, decrease as the altitude increases. For instance, the peak pressure of the S0 case is 33.92 bar and it is decreased by 45.01%, and 71.23% in the L0 and H0 cases. Even

![Figure 10: Comparison of pressure, temperature and HRR of the reference chamber at varying altitudes and hydrogen addition conditions. The figure is divided into three columns representing altitudes: 0 ft, 5000 ft, and 15000 ft. Each column contains three rows of plots: (a), (b), (c) for pressure; (d), (e), (f) for temperature; and (g), (h), (i) for HRR. The x-axis for all plots is 'Eccentric Shaft Angle [°EA]' ranging from 315 to 585. The y-axes are: Ref. Chamber Pressure [bar] (0-50 for 0 ft, 0-35 for 5000 ft, 0-16 for 15000 ft), Ref. Chamber Temperature [K] (400-2400), and HRR [J/°EA] (0-40 for 0 ft, 0-20 for 5000 ft, 0-15 for 15000 ft). Each plot shows four curves: S0 (blue), S5 (red), S10 (green) for 0 ft; L0 (blue), L5 (red), L10 (green) for 5000 ft; and H0 (blue), H5 (red), H10 (green) for 15000 ft.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 10: Comparison of pressure, temperature and HRR of the reference chamber at varying altitudes and hydrogen addition conditions. The figure is divided into three columns representing altitudes: 0 ft, 5000 ft, and 15000 ft. Each column contains three rows of plots: (a), (b), (c) for pressure; (d), (e), (f) for temperature; and (g), (h), (i) for HRR. The x-axis for all plots is 'Eccentric Shaft Angle [°EA]' ranging from 315 to 585. The y-axes are: Ref. Chamber Pressure [bar] (0-50 for 0 ft, 0-35 for 5000 ft, 0-16 for 15000 ft), Ref. Chamber Temperature [K] (400-2400), and HRR [J/°EA] (0-40 for 0 ft, 0-20 for 5000 ft, 0-15 for 15000 ft). Each plot shows four curves: S0 (blue), S5 (red), S10 (green) for 0 ft; L0 (blue), L5 (red), L10 (green) for 5000 ft; and H0 (blue), H5 (red), H10 (green) for 15000 ft.

**Fig. 10 – Comparison of pressure, temperature and HRR of the reference chamber at varying altitudes and hydrogen addition conditions; (a.), (b.), (c.) pressure, (d.), (e.), (f.) temperature, (g.), (h.), (i.) HRR.**

if the static compression ratio of a given engine remains the same, the pressure developed during compression is lower at higher altitudes. This phenomenon stems from the reduced oxygen content in the combustion chamber, which was affected by the lower intake pressure, leading to a more extended ignition delay period as the altitude increased. The other reason causes this phenomenon is that the air pressure and density difference between the combustion chamber and the outside increases as the altitude increases, and the ability of gas inside the chamber to escape also increases.

As seen in Fig. 10(d)–(f), the mean reference chamber temperature of the S0 case is the highest, and its peak value is obtained earlier than the L0 and H0 cases. As shown in Fig. 10(g)–(i), the HRR value of the S0 case peaks dramatically and drops earlier than in the L0 and H0 cases. The slope of these plots indicates the prolonged combustion duration and flame development period, and also the delayed ending of combustion in the reference chamber with the altitude increase.

- The influences of hydrogen addition on temperature, pressure and HRR of the reference chamber;

The peak pressures of the hydrogen-blended cases are observed earlier compared with the neat gasoline cases as can

be seen in Fig. 10(a)–(c). On the other hand, there is a rapid downward trend in the pressure curves of hydrogen-blended cases compared to the neat gasoline cases. This trend in the pressure curves reveals that the post-ignition temperature and combustion duration are reduced by hydrogen addition. Also, the maximum value of the reference chamber pressure rises with the hydrogen energy fraction increase. For instance, the maximum value of the reference chamber pressure is increased by 10.81% and 18.91% for the S5 and S10 cases, respectively, in comparison with the S0 case. Hydrogen addition increases the homogeneity of the mixture and laminar flame-burning speed [35,42]. HRR and temperature of the reference chamber are lower in neat gasoline-fueled cases compared to hydrogen-blended cases, as shown in Fig. 10(d)–(f), and Fig. 10(g)–(i). This is likely because the heat produced by the combustion process of the hydrogen-blended cases can prevail over the aforementioned heat losses of the Wankel engine.

OH radicals (hydroxyl radicals) play a critical role in the combustion process of hydrocarbon fuels [73]. These highly reactive molecules that participate in many of the critical reactions during combustion are excellent markers for the chemical structures and mechanisms of combustion in various applications, including internal combustion engines.

![Figure 11: OH mass fraction iso-surfaces at EA10 and EA50. The figure is a 3x6 grid of cross-sectional plots of a rotary engine combustion chamber. The rows represent altitudes: 0 ft, 5000 ft, and 15000 ft. The columns represent hydrogen addition levels: 0.0% H2, 5.0% H2, and 10.0% H2. The left side of the grid is labeled EA10 and the right side is labeled EA50. Each plot shows the OH mass fraction distribution, with a color scale on the left ranging from 0.000 (blue) to 0.005 (red). The plots are labeled with codes: S0, S5, S10 for the top row; L0, L5, L10 for the middle row; and H0, H5, H10 for the bottom row. The OH mass fraction iso-surfaces are generally more concentrated and larger in the lower altitude (0 ft) and higher hydrogen addition (10.0% H2) cases, and smaller and more dispersed in the higher altitude (15000 ft) and lower hydrogen addition (0.0% H2) cases.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 11: OH mass fraction iso-surfaces at EA10 and EA50. The figure is a 3x6 grid of cross-sectional plots of a rotary engine combustion chamber. The rows represent altitudes: 0 ft, 5000 ft, and 15000 ft. The columns represent hydrogen addition levels: 0.0% H2, 5.0% H2, and 10.0% H2. The left side of the grid is labeled EA10 and the right side is labeled EA50. Each plot shows the OH mass fraction distribution, with a color scale on the left ranging from 0.000 (blue) to 0.005 (red). The plots are labeled with codes: S0, S5, S10 for the top row; L0, L5, L10 for the middle row; and H0, H5, H10 for the bottom row. The OH mass fraction iso-surfaces are generally more concentrated and larger in the lower altitude (0 ft) and higher hydrogen addition (10.0% H2) cases, and smaller and more dispersed in the higher altitude (15000 ft) and lower hydrogen addition (0.0% H2) cases.

**Fig. 11 – OH mass fraction iso-surfaces at EA10 and EA50.**

Therefore, OH radical distribution analysis has become a widely preferred method for investigating combustion processes. OH mass fraction iso-surfaces for the simulations at EA10 and EA50 are shown in Fig. 11.

Understanding the effects of altitude on the combustion process is crucial for optimizing engine design and performance at varying altitudes. The mass fraction of OH is lower at high altitudes compared to sea level conditions. This is due to several factors, such as the cooler wall effect, lower oxygen content, and deteriorating fuel ignition characteristics at high altitudes. These factors contribute to slower flame propagation at high altitudes, making it more difficult for the flame to spread into the narrower gaps of the engine, as illustrated in Fig. 11. As the altitude increases, the air density decreases, which results in less oxygen being available for combustion. This can lead to a slower combustion process and a lower mass fraction of OH being produced. The decrease in air density at higher altitudes can also result in the flame front propagating more slowly. The flame propagates faster in hydrogen-enriched cases compared with neat gasoline-fueled cases. This is likely because hydrogen has a higher flame speed compared to gasoline, meaning that when hydrogen is blended with gasoline, the resulting mixture has a higher flame speed than gasoline. Hydrogen-enriched mixtures have been shown to exhibit several advantages over neat gasoline in terms of combustion performance, including faster flame propagation and improved combustion stability. On the other hand, the cooler walls of the housing of the rotary engine act as a heat sink, which causes incomplete combustion regions within the crevice or close to the walls. The flame can propagate easier into the narrower gaps in the combustion chamber due to its low quenching distance. This means that previously unburnt fuel in the combustion chamber can also

undergo combustion. While cooler walls can hinder the combustion process in conventional combustion systems, the excellent features of hydrogen, such as wide flammability and diffusivity range enable hydrogen-enriched mixtures to minimize this adverse effect. The low quenching distance of the hydrogen-enriched mixture flame allows it to reach the unburnt fuel in the narrower gaps of the rotary engine and complete the combustion process. This can lead to reduced emissions and improved fuel economy, making hydrogen-enriched mixtures a promising option for future engine design and optimization.

Fig. 12 provides a detailed view of the temperature distributions and combustion behavior of a rotary engine under varying altitudes and hydrogen addition conditions at EA50 and EA90. As the altitude increases, the ambient air density, temperature, and pressure decrease, resulting in colder engine operating conditions and a corresponding decrease in reference chamber temperature in the combustion chamber. Furthermore, the angular position of spark plugs towards the leading edge of the rotor, combined with the rotor's rotation direction, causes the bulk flow of gases to move toward the leading edge. This flow pattern causes the flame propagation to move towards the rotor's leading edge, as depicted in this figure. Additionally, Fig. 12 together with Fig. 13 demonstrates the effects of high altitude on fuel combustion by highlighting the slow burning of fuel and extended combustion duration that occur under such conditions. The depicted figures reveal that the flame can effortlessly propagate toward the lateral walls of the enclosure when hydrogen is blended into the fuel mixture. The remarkable characteristics of hydrogen enable the hydrogen blended mixtures to effectively spread even in the narrower gaps of the operational chamber, resulting in a more efficient and effective combustion process.



![Figure 12: Temperature distribution in the central plane and bottom views of the Wankel engine at EA50 and EA90. The figure is a 3x6 grid of heatmaps. The columns are labeled EA50 and EA90, and the sub-columns are 0.0% H2, 5.0% H2, and 10.0% H2. The rows are labeled 0 ft, 5000 ft, and 15000 ft. Each cell contains two heatmaps: a central plane view (top) and a bottom view (bottom). A color bar on the left indicates temperature in Kelvin (K) from 300 to 2700. The heatmaps show the temperature distribution across the combustion chamber, with colors ranging from blue (cold) to red (hot).](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 12: Temperature distribution in the central plane and bottom views of the Wankel engine at EA50 and EA90. The figure is a 3x6 grid of heatmaps. The columns are labeled EA50 and EA90, and the sub-columns are 0.0% H2, 5.0% H2, and 10.0% H2. The rows are labeled 0 ft, 5000 ft, and 15000 ft. Each cell contains two heatmaps: a central plane view (top) and a bottom view (bottom). A color bar on the left indicates temperature in Kelvin (K) from 300 to 2700. The heatmaps show the temperature distribution across the combustion chamber, with colors ranging from blue (cold) to red (hot).

Fig. 12 – Temperature distribution in the central plane and bottom views of the Wankel engine at EA50 and EA90.

![Figure 13: C8H18 mass fraction distribution in the central plane and bottom views of the Wankel engine at EA50 and EA90. The figure is a 3x6 grid of heatmaps. The columns are labeled EA50 and EA90, and the sub-columns are 0.0% H2, 5.0% H2, and 10.0% H2. The rows are labeled 0 ft, 5000 ft, and 15000 ft. Each cell contains two heatmaps: a central plane view (top) and a bottom view (bottom). A color bar on the left indicates C8H18 mass fraction from 0.005 to 0.06. The heatmaps show the mass fraction distribution of C8H18 across the combustion chamber, with colors ranging from blue (low mass fraction) to red (high mass fraction).](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

Figure 13: C8H18 mass fraction distribution in the central plane and bottom views of the Wankel engine at EA50 and EA90. The figure is a 3x6 grid of heatmaps. The columns are labeled EA50 and EA90, and the sub-columns are 0.0% H2, 5.0% H2, and 10.0% H2. The rows are labeled 0 ft, 5000 ft, and 15000 ft. Each cell contains two heatmaps: a central plane view (top) and a bottom view (bottom). A color bar on the left indicates C8H18 mass fraction from 0.005 to 0.06. The heatmaps show the mass fraction distribution of C8H18 across the combustion chamber, with colors ranging from blue (low mass fraction) to red (high mass fraction).

Fig. 13 –  $C_8H_{18}$  mass fraction distribution in the central plane and bottom views of the Wankel engine at EA50 and EA90.

$C_8H_{18}$  mass fraction distributions and combustion characteristics of the rotary engine under varying altitudes and hydrogen addition conditions are illustrated in Fig. 13.  $C_8H_{18}$  mass fraction profiles of the different hydrogen ratios and varying altitude cases at EA50 and EA90 are shown, providing a means of comparison.

The less fuel mass fraction in the reference chamber is observed towards the end of the combustion process at 0 ft than those of higher altitudes in Fig. 13. This means that fuel is depleted rapidly due to the fast combustion process at 0 ft. On the other hand, there are still some regions with high  $C_8H_{18}$  concentrations at higher altitudes at the time of EA90, especially at the neat gasoline cases. The main reason for this phenomenon is that flame quenching can occur when a flame propagates close to the chamber wall of the engine. In the hydrogen blended cases,  $C_8H_{18}$  is depleted even in the narrower regions in the combustion chamber.

## 3.2. Engine performance

Fig. 14 Shows the performance characteristics of the Wankel research engine. Although the performance parameters tend to decrease with altitude increase, the presence of hydrogen in the mixture improves these parameters remarkably. Because improved premixed fuel conditions and better combustion behavior can be observed in the hydrogen-blended rotary engines even at high altitudes due to the high flame speed, high diffusion rate, and calorific value properties of the hydrogen. Compared to the results of the S0 case IMEP values are increased by 6.59% and 8.50%, and the indicated power values are increased by 6.15% and 7.99% in the S5 case and S10 case, respectively.

![Figure 14: Performance parameters of simulated cases. The figure consists of three vertically stacked line graphs (a, b, c) sharing a common x-axis representing hydrogen addition levels: 0% H2, 5% H2, and 10% H2. Three data series are shown for each altitude: 0 ft (blue squares), 5000 ft (red triangles), and 15000 ft (green circles). (a) IMEP [bar]: Values range from 2 to 6. IMEP increases with hydrogen addition and decreases with altitude. (b) Indicated Power [kW]: Values range from 0 to 60. Power increases with hydrogen addition and decreases with altitude. (c) Specific Fuel Cons. [g/kWh]: Values range from 0 to 600. Fuel consumption decreases with hydrogen addition and increases with altitude.](dd330f8b8f6c16eae20c3a676b4eb804_img.jpg)

| Parameter                   | Altitude | 0% H <sub>2</sub> | 5% H <sub>2</sub> | 10% H <sub>2</sub> |
|-----------------------------|----------|-------------------|-------------------|--------------------|
| IMEP [bar]                  | 0 ft     | ~5.5              | ~5.8              | ~5.8               |
|                             | 5000 ft  | ~3.2              | ~3.8              | ~4.5               |
|                             | 15000 ft | ~1.8              | ~2.2              | ~3.8               |
| Indicated Power [kW]        | 0 ft     | ~10               | ~10               | ~10                |
|                             | 5000 ft  | ~12               | ~18               | ~25                |
|                             | 15000 ft | ~15               | ~22               | ~35                |
| Specific Fuel Cons. [g/kWh] | 0 ft     | ~280              | ~250              | ~220               |
|                             | 5000 ft  | ~380              | ~320              | ~280               |
|                             | 15000 ft | ~350              | ~280              | ~220               |

Figure 14: Performance parameters of simulated cases. The figure consists of three vertically stacked line graphs (a, b, c) sharing a common x-axis representing hydrogen addition levels: 0% H2, 5% H2, and 10% H2. Three data series are shown for each altitude: 0 ft (blue squares), 5000 ft (red triangles), and 15000 ft (green circles). (a) IMEP [bar]: Values range from 2 to 6. IMEP increases with hydrogen addition and decreases with altitude. (b) Indicated Power [kW]: Values range from 0 to 60. Power increases with hydrogen addition and decreases with altitude. (c) Specific Fuel Cons. [g/kWh]: Values range from 0 to 600. Fuel consumption decreases with hydrogen addition and increases with altitude.

Fig. 14 – Performance parameters of (a.) IMEP, (b) indicated power, (c.) specific fuel consumption of simulated cases.

case, respectively. Compared to the results of the L0 case IMEP values are increased by 19.86% and 37.71%, and the indicated power values are increased by 26.53% and 45.17% in the L5 case and L10 case, respectively. Compared to the results of the H0 case IMEP values are increased by 27.27% and 61.90%, and the indicated power values are increased by 26.62% and 48.75% in the L5 case and L10 case, respectively. On the contrary, an upward trend can be observed for specific fuel consumption parameters with the increase in altitude. The total fuel consumption of the S5 case and the S10 case are reduced by 14.38% and 27.89%, respectively, compared to the fuel consumption of the S0 case.

## 3.3. Exhaust emissions

The mass fraction profiles of CO, CO<sub>2</sub>, and NO<sub>x</sub> of the different hydrogen ratios and varying altitude cases are given in Fig. 15. These are the exhaust emission values emitted at the opening time of the exhaust port (566 °EA) shown in the dashed lines in Fig. 15. Combustion is worsened and emissions deteriorate as the altitude increase, however, they are improved with the hydrogen addition.

CO<sub>2</sub> and CO emissions are shown in Fig. 15(a)–(c) and Fig. 5(d)–(f). Lower CO emissions indicate complete combustion process. Due to insufficient oxygen at higher altitudes, oxidation reactions cannot convert CO to CO<sub>2</sub> during combustion. For instance, in pure gasoline cases (S0, L0, H0 cases), the CO<sub>2</sub> mass fractions decrease by 14.28% and 30.95% at altitudes of 5000 ft and 15000 ft, respectively, compared to sea level operation (Fig. 15(a)–(c)). In terms of CO emissions, pure gasoline cases exhibit emissions approximately three times higher at 5000 ft and slightly over four times higher at 15000 ft compared to sea level, as depicted in Fig. 15(d)–(f). On the other hand, CO and CO<sub>2</sub> productions are lower at all altitudes in hydrogen-enriched cases due to the carbon-free nature of hydrogen. As for NO<sub>x</sub> emissions, the mean temperature of the reference chamber (Fig. 10(g)–(i)) and the mass of NO<sub>x</sub> increase rapidly. Because the thermal NO<sub>x</sub> formation is highly correlated with the combustion chamber temperature. NO<sub>x</sub> emissions are decreased at higher altitudes due to the delayed reference chamber temperature peaks. In contrast, rising pressures and temperatures of the reference chamber in the hydrogen-enriched Wankel engine cases stimulate thermal NO<sub>x</sub> formation, as illustrated in Fig. 10.

## 3.4. Discussion

The findings of the presented study reveal that the utilization of hydrogen is very compatible with Wankel engines for UAVs. When hydrogen is utilized as an auxiliary fuel, mixture formation can be improved, and the mixture properties and combustion efficiency can be enhanced by taking advantage of the properties of both fuels. Therefore, utilization of the excellent properties of hydrogen as an auxiliary fuel can compensate for some disadvantages of the Wankel engine: (i) Flame propagation path is very long in this engine due to the crescent geometry of the combustion chamber. Also, the unidirectional flow field hinders backward flame propagation due to the constant rotational direction. For these reasons, an inaccessible and incombustible flame zone

![Figure 15: Comparison of combustion products of the reference chamber of the simulated cases for a cycle. The figure is divided into three columns representing altitudes: 0 ft, 5000 ft, and 15000 ft. Each column contains three rows of plots: (a), (b), (c) for CO2 mass fraction; (d), (e), (f) for CO mass fraction; and (g), (h), (i) for NOx mass fraction. Each plot shows the mass fraction of the respective product against the Eccentric Shaft Angle [°EA] from 315 to 585. The plots compare three cases: S0 (blue), S5 (red), and S10 (green) at 0 ft; L0 (blue), L5 (red), and L10 (green) at 5000 ft; and H0 (blue), H5 (red), and H10 (green) at 15000 ft. A vertical dashed line is present at approximately 500°EA in each plot.](b05a8a3551db31147979064952179990_img.jpg)

Figure 15: Comparison of combustion products of the reference chamber of the simulated cases for a cycle. The figure is divided into three columns representing altitudes: 0 ft, 5000 ft, and 15000 ft. Each column contains three rows of plots: (a), (b), (c) for CO2 mass fraction; (d), (e), (f) for CO mass fraction; and (g), (h), (i) for NOx mass fraction. Each plot shows the mass fraction of the respective product against the Eccentric Shaft Angle [°EA] from 315 to 585. The plots compare three cases: S0 (blue), S5 (red), and S10 (green) at 0 ft; L0 (blue), L5 (red), and L10 (green) at 5000 ft; and H0 (blue), H5 (red), and H10 (green) at 15000 ft. A vertical dashed line is present at approximately 500°EA in each plot.

**Fig. 15 – Comparison of combustion products of the reference chamber of the simulated cases for a cycle; (a), (b), (c)  $\text{CO}_2$  mass fraction, (d), (e), (f)  $\text{CO}$  mass fraction, (g), (h), (i)  $\text{NO}_x$  mass fraction.**

occurs in the combustion chamber's trailing side. The high flame speed of hydrogen increases mass transport. Therefore, the flame can propagate on the trailing side of the combustion chamber in the hydrogen-blended Wankel engine [30–35]. (ii) Local residual gas coefficient is very high in the housing of the Wankel engine, and the spark plug is located in the housing. Therefore, there is a severe spark atmosphere in this engine. The large flammability and diffusivity of hydrogen provide a smooth ignition. (iii) High surface-to-volume ratio of the rotary engine causes high heat transfer from the casing walls and increases the quenching phenomenon. As a result, the combustion efficiency is reduced, and the HC emissions deteriorate. Hydrogen utilization improves these drawbacks because of the short quenching distance of hydrogen.

On the other hand, some advantages of the Wankel engine can compensate for some disadvantages of hydrogen [28]: (i) Due to the limitations of their low specific volume heat value, the maximum braking torque of the hydrogen-fueled ICEs are generally lower than that of fossil-fueled ICEs. This drawback of the Wankel engine can be compensated by its significant power density. (ii) Hydrogen utilization in ICEs leads to some abnormal combustion behavior such as backfiring, auto-ignition, or pre-ignition since hydrogen has large flammability and high

ignition energy. However, these kinds of abnormal combustions do not occur in hydrogen-fueled Wankel engines. Because each stroke of the Wankel engine is performed in physically separated regions. For instance, the physical separation of the chambers, where combustion and exhaust strokes are carried out, can prevent or backfire and pre-ignition. (iii) Bigger stores are required for hydrogen gaseous compared with liquid fuels due to hydrogen's low volumetric energy density (28). Besides, hydrogen-fueled engines' storage problem is a major technical drawback, especially in UAV applications. On the other hand, the compact structure of the Wankel engine gives it a benefit in powertrains of hydrogen-fueled vehicles. In addition, the hydrogen blending strategy may be a practical choice to make up for the storage problems, because the amount of hydrogen stored is quite lower.

# 4. Conclusion

In this research, a full Wankel engine model was simulated using Converge CFD and validated with the experimental data. This study demonstrates that the hydrogen-blended Wankel engine is a very promising power source option for aviation applications. Because the hydrogen enrichment

strategy allows improving combustion in the combustion chamber even at high altitudes.

The main findings of the present study are listed below:

1. Flame propagation and combustion duration in the reference chamber are prolonged at higher altitudes and this phenomenon decreases the burning speed of fuel at higher altitude cases. However, the distinct properties of hydrogen such as wide flammability limits, high flame speed, small quenching distance, high diffusivity and homogeneity enable hydrogen-enriched cases to have a more stable combustion process. Furthermore, the hydrogen enrichment shortens the combustion durations and increases combustion velocity due to the O, H and OH concentrations increasing with the hydrogen addition.
2. The decrease in ambient air temperature, pressure, density, and insufficient fresh charge as the altitude increases leads to the reduced reference chamber pressure and temperature for the Wankel engine. Thus, the combustion worsens, the HRR value decreases, engine performance decreases, and emissions deteriorate in these colder operating conditions. As a result, the IMEP and indicated power decrease due to the altitude increase. In contrast, the performance parameters of the Wankel engine are improved by hydrogen addition.
3. Emissions worsen with the altitude increase. However, hydrogen addition reduces engine instability and emissions, so the emission productions are lower in the hydrogen-blended Wankel engine. Because the hydrogen-enriched Wankel engine essentially eliminates the carbon-based emissions (CO, CO<sub>2</sub>, and HC emissions) due to hydrogen's carbonless structure. However, thermal NO<sub>x</sub> emissions decrease at high altitudes because of the lower ambient temperatures. On the contrary, NO<sub>x</sub> formation increases due to the higher operating temperatures in the hydrogen-blended cases. Therefore, NO<sub>x</sub> emissions are relatively lower in the hydrogen-blended Wankel engines for UAV applications.

In future work, the profits of the hydrogen utilization will be improved further by applying direct injection of hydrogen to the combustion chamber of the Wankel research engine. Besides, spark plug positions and ignition timing will be optimized to improve the combustion process, particularly at high altitude cases.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgment

The authors thank LENTATEK for the donation of the Wankel research engine, Convergent Science Company for the Converge CFD academic license, the High-Performance Computing Laboratory of Bursa Technical University, and

the Internal Combustion Engine Laboratory of Bursa Uludag University for their technical support.

# REFERENCES

- [1] Ji C, Wang H, Shi C, Wang S, Yang J. Multi-objective optimization of operating parameters for a gasoline Wankel rotary engine by hydrogen enrichment. *Energy Convers Manag* 2021;229:113732. <https://doi.org/10.1016/J.enconman.2020.113732>.
- [2] Kutlar OA, Cihan O. Investigation of parameters affecting rotary engine by means of a one zone thermodynamic model. *J Energy Resour Technol* 2021;144(4):042304. <https://doi.org/10.1115/1.4052615>.
- [3] Cihan O, Dogan HE, Kutlar OA, Demirci A, Javadzadehkalkhoran M. Evaluation of heat release and combustion analysis in spark ignition Wankel and reciprocating engine. *Fuel* 2020;261:116479. <https://doi.org/10.1016/j.fuel.2019.116479>.
- [4] Dhyani V, Subramanian KA. Experimental investigation on effects of knocking on backfire and its control in a hydrogen fueled spark ignition engine. *Int J Hydrogen Energy* 2018;43:7169–78.
- [5] Meng H, Ji C, Yang J, Wang S, Xin G, Chang K, Wang H. Experimentally investigating the asynchronous ignition on a hydrogen-fueled Wankel rotary engine. *Fuel* 2022;312:122988. <https://doi.org/10.1016/j.fuel.2021.122988>.
- [6] Amrouche F, Erickson P, Park J, Varnhagen S. An experimental investigation of hydrogen-enriched gasoline in a Wankel rotary engine. *Int J Hydrogen Energy* 2014;39(16):8525–34. <https://doi.org/10.1016/j.ijhydene.2014.03.172>.
- [7] Meng H, Ji C, Yang J, Wang S, Chang K, Xin G. Experimental study of the effects of excess air ratio on combustion and emission characteristics of the hydrogen-fueled rotary engine. *Int J Hydrogen Energy* 2021;46:32261–72. <https://doi.org/10.1016/j.ijhydene.2021.06.208>.
- [8] Shi C, Chai S, Di L, Ji C, Ge Y, Wang H. Combined experimental-numerical analysis of hydrogen as a combustion enhancer applied to Wankel engine. *Energy* 2023;263:125896. <https://doi.org/10.1016/j.energy.2022.125896>.
- [9] Meng H, Ji C, Yang J, Wang S, Gao C, Shen X, Xin G, Hong C. Assessment of the application of oxygen enrichment in the hydrogen-fueled Wankel rotary engine. *Fuel* 2023;341:127732. <https://doi.org/10.1016/j.fuel.2023.127732>.
- [10] Harikrishnan TV, Challa S, Radhakrishna D. Numerical investigation on the effects of flame propagation in rotary engine performance with leakage and different recess shapes using three-dimensional computational fluid dynamics. *J Energy Resour Technol Trans ASME* 2016;138:052210.
- [11] Yang J, Ji C, Wang S, Wang D, Shi C, Ma Z, Zhang B. Numerical study of hydrogen direct injection strategy on mixture formation and combustion process in a partially premixed gasoline Wankel rotary engine. *Energy Convers Manag* 2018;176:184–93.
- [12] Chen W, Pan J, Fan B, Otchere P, Miao N, Lu Y. Numerical investigation of dual-fuel injection timing on air-fuel mixing and combustion process in a novel natural gas-diesel rotary engine. *Energy Convers Manag* 2018;176:334–48.
- [13] Gao J, Tian G, Ma C, Balasubramanian D, Xing S, Jenner P. Numerical investigations of combustion and emissions characteristics of a novel small scale opposed rotary piston engine fuelled with hydrogen at wide open throttle and stoichiometric conditions. *Energy Convers Manag* 2020;221:113178.
- [14] Gao J, Xing S, Tian G, Ma C, Zhao M, Jenner P. Numerical simulation on the combustion and NO<sub>x</sub> emission

- characteristics of a turbocharged opposed rotary piston engine fuelled with hydrogen under wide open throttle conditions. *Fuel* 2021;285:119210.
- [15] Fan B, Zeng Y, Pan J, Fang J, Salami HA, Wang Y. Numerical study of injection strategy on the combustion process in a peripheral ported rotary engine fueled with natural gas/hydrogen blends under the action of apex seal leakage. *Energy* 2022;242:122532.
- [16] Otchere P, Pan J, Fan B, Chen W, Lu Y, Jianxing L. Mixture formation and combustion process of a biodiesel fueled direct injection rotary engine (DIRE) considering injection timing, spark timing and equivalence ratio- CFD study. *Energy Convers Manag* 2020;217:112948.
- [17] Tartakovsky L, Baibikov V, Gutman M, Veinblat M, Reif J. Simulation of Wankel engine performance using commercial software for piston engines. *SAE Technical Paper* 2012. <https://doi.org/10.4271/2012-32-0098>. 2012-32-0098.
- [18] Wang H, Ji C, Shi C, Ge Y, Meng H, Yang J, Chang K, Yang Z, Wang S, Wang X. Modeling and parametric study of the performance-emissions trade-off of a hydrogen Wankel rotary engine. *Fuel* 2022;318:123662. <https://doi.org/10.1016/j.fuel.2022.123662>.
- [19] Peden M, Turner M, Turner JWG, Bailey N. Comparison of 1-D modelling approaches for Wankel engine performance simulation and initial study of the direct injection limitations. *SAE Technical Paper* 2018. <https://doi.org/10.4271/2018-01-1452>. 2018-01-1452.
- [20] Zou R, Liu J, Jiao H, Wang N, Zhao J. Numerical study on auto-ignition development and knocking characteristics of a downsized rotary engine under different inlet pressures. *Fuel* 2022;309:122046. <https://doi.org/10.1016/j.fuel.2021.122046>.
- [21] Rose SW, Yang DCH. Wide and multiple apex seals for the rotary engine: (Abbr.: multi-Apex-Seals for the Rotary Engine). *Mech Mach Theor* 2014;74:202–15. <https://doi.org/10.1016/j.mechmachtheory.2013.12.011>.
- [22] Cihan O, Kutlar OA. Effect of leading and trailing spark plugs on combustion, fuel consumption and exhaust emission in a Wankel engine. *Arabian J Sci Eng* 2021;46(8):7471–82. <https://doi.org/10.1007/s13369-021-05456-3>.
- [23] Boughou S, Mohiuddin AKM. Combustion chamber design effect on the rotary engine performance- A review. *International Journal of Automotive Engineering* 2020;11(4):200–12.
- [24] Hwang PW, Chen XC, Cheng HC. Influences of ignition timing, spark plug and intake port locations on the combustion performance of a simulated rotary engine. *Journal of Mechanics* 2016;32(5):579–91. <https://doi.org/10.1017/jmech.2016.39>.
- [25] Boretti A. Modeling unmanned aerial vehicle jet ignition Wankel engines with CAE/CFD. *Advances in Aircraft and Spacecraft Science* 2015;2(4):445–67. <https://doi.org/10.12989/aas.2015.2.4.445>.
- [26] Finkelberg L, Kostuchenkov A, Zelentsov A, Minin V. Improvement of combustion process of spark-ignited aviation Wankel engine. *Energies* 2019;12(12):2292. <https://doi.org/10.3390/en12122292>.
- [27] Spreitzer J, Zahradnik F, Geringer B. Implementation of a rotary engine (Wankel engine) in a CFD simulation tool with special emphasis on combustion and flow phenomena. *SAE Technical Paper* 2015. <https://doi.org/10.4271/2015-01-0382>. 2015-01-0382.
- [28] Meng H, Ji C, Wang S, Yang J. A review: centurial progress and development of Wankel rotary engine. *Fuel* 2023;335:127043. <https://doi.org/10.1016/j.fuel.2022.127043>.
- [29] Meng H, Ji C, Wang S, Wang D, Yang J. Optimizing the idle performance of an n-butanol fueled Wankel rotary engine by hydrogen addition. *Fuel* 2021;288:119614.
- [30] Su T, Ji C, Wang S, Shi L, Yang J, Cong X. Effect of spark timing on performance of a hydrogen-gasoline rotary engine. *Energy Convers Manag* 2017;148:120–7. <https://doi.org/10.1016/j.enconman.2017.05.064>.
- [31] Taskiran OO. Improving burning speed by using hydrogen enrichment and turbulent jet ignition system in a rotary engine. *Int J Hydrogen Energy* 2021;46:29649–62. <https://doi.org/10.1016/j.ijhydene.2020.11.142>.
- [32] Dhole AE, Yarasu RB, Lata DB, Priyam A. Effect on performance and emissions of a dual fuel diesel engine using hydrogen and producer gas as secondary fuels. *Int J Hydrogen Energy* 2014;39:8087–97.
- [33] Dhole AE, Yarasu RB, Lata DB. Effect of hydrogen and producer gas as secondary fuels on combustion parameters of a dual fuel diesel engine. *Appl Therm Eng* 2016;108:764–73.
- [34] Wang J, Huang Z, Tang C, Zheng J. Effect of hydrogen addition on early flame growth of lean burn natural gas-air mixture. *Int J Hydrogen Energy* 2010;35:7246–52.
- [35] Kucuk M, Surmen A, Sener R. Effects of hydrogen enrichment strategy on combustion and emissions in a gasoline fuelled rotary engine. *Proceedings of INCOS 2022*;2022.
- [36] Amrouche F, Erickson PA, Park JW, Varnhagen S. Extending the lean operation limit of a gasoline Wankel rotary engine using hydrogen enrichment. *Int J Hydrogen Energy* 2016;41:14261–71.
- [37] Meng H, Ji C, Su T, Yang J, Chang K, Xin G, Wang S. A study on the effect of qualitative control coupling variable engine speed on the hydrogen-fueled Wankel rotary engine at wide-open throttle. *Int J Hydrogen Energy* 2022;47(20):11028–38. <https://doi.org/10.1016/j.ijhydene.2021.12.262>.
- [38] Yang J, Ji C, Wang S, Meng H. An experimental study on ignition timing of hydrogen Wankel rotary engine. *Int J Hydrogen Energy* 2022;47. <https://doi.org/10.1016/j.ijhydene.2022.03.223>. 17564-17478.
- [39] Kucuk M. Performance analysis and improvement of a Wankel engine suitable for UAV flight atmosphere. *Phd Thesis. Bursa: Bursa Technical University*; 2022.
- [40] Ozcanli M, Bas O, Akar MA, Yildizhan S, Serin H. Recent studies on hydrogen usage in Wankel SI engine. *Int J Hydrogen Energy* 2018;43(38):18037–45. <https://doi.org/10.1016/j.ijhydene.2018.01.202>.
- [41] Fan B, Pan J, Liu Y, Zhu Y, Pan Z, Chen W, Otchere P. Effect of hydrogen injection strategies on mixture formation and combustion process in a hydrogen direct injection plus natural gas port injection rotary engine. *Energy Convers Manag* 2018;160:150–64.
- [42] Amrouche F, Erickson PA, Varnhagen S, Park JW. An experimental study of a hydrogen-enriched ethanol fueled Wankel rotary engine at ultra lean and full load conditions. *Energy Convers Manag* 2016;123:174–84.
- [43] Yang J, Ji C, Wang S, Wang D, Ma Z, Ma L. A comparative study of mixture formation and combustion processes in a gasoline Wankel rotary engine with hydrogen port and direct injection enrichment. *Energy Convers Manag* 2018;168:21–31. <https://doi.org/10.1016/j.enconman.2018.04.105>.
- [44] Yang J, Ji C, Wang S, Wang D, Ma Z, Zhang B. Numerical investigation on the mixture formation and combustion processes of a gasoline rotary engine with direct injected hydrogen enrichment. *Appl Energy* 2018;224:34–41. <https://doi.org/10.1016/j.apenergy.2018.04.092>.
- [45] Fan B, Wang Y, Zhang Y, Pan J, Yang W, Zeng Y. Numerical investigation on the combustion performance of a natural gas/hydrogen dual fuel rotary engine under the action of apex seal leakage. *Energy & Fuels* 2021;35(1):770–84. <https://doi.org/10.1021/acs.energyfuels.0c03498>.
- [46] Fan B, Zeng Y, Zhang Y, Pan J, Yang W, Wang Y. Research on the hydrogen injection strategy of a direct injection natural

- gas/hydrogen rotary engine considering apex seal leakage. *Int J Hydrogen Energy* 2021;46:9234–51. <https://doi.org/10.1016/j.ijhydene.2020.12.214>.
- [47] Fan B, Pan J, Liu Y, Chen W, Lu Y, Otchere P. Numerical investigation of mixture formation and combustion in a hydrogen direct injection plus natural gas port injection (HDI + NGPI) rotary engine. *Int J Hydrogen Energy* 2018;43:4632–44.
- [48] Su T, Ji C, Wang S, Cong X, Shi L. Improving the combustion performance of a gasoline rotary engine by hydrogen enrichment at various conditions. *Int J Hydrogen Energy* 2018;43(3):1902–8. <https://doi.org/10.1016/j.ijhydene.2017.11.175>.
- [49] Su T, Ji C, Wang S, Shi L, Yang J, Cong X. Reducing cyclic variation of a gasoline rotary engine by hydrogen addition under various operating conditions. *Int J Hydrogen Energy* 2017;42(40):25428–35. <https://doi.org/10.1016/j.ijhydene.2017.08.158>.
- [50] Gao J, Tian G, Ma C, Zhang Y, Xing S, Jenner P. Lean-burn characteristics of a turbocharged opposed rotary piston engine fueled with hydrogen at low engine speed conditions. *Int J Hydrogen Energy* 2021;46(1):1219–33. <https://doi.org/10.1016/j.ijhydene.2020.09.167>.
- [51] Yang J, Ji C. A comparative study on performance of the rotary engine fueled hydrogen/gasoline and hydrogen/n-butanol. *Int J Hydrogen Energy* 2018;43(50):22669–75. <https://doi.org/10.1016/j.ijhydene.2018.10.129>.
- [52] Meng H, Ji C, He Y, Li H, Yang J, Wang H, Wang S. Discussion on the potential of methane-hydrogen dual-fueled Wankel rotary engine. *Energy* 2023;279:128121. <https://doi.org/10.1016/j.energy.2023.128121>.
- [53] Ji C, Meng H, Wang S, Wang D, Yang J, Shi C, Ma Z. Realizing stratified mixtures distribution in a hydrogen-enriched gasoline Wankel engine by different compound intake methods. *Energy Convers Manag* 2020;203:112230. <https://doi.org/10.1016/j.enconman.2019.112230>.
- [54] Yontar AA. Effects of ethanol, methyl tert-butyl ether and gasoline-hydrogen blend on performance parameters and HC emission at Wankel engine. *Biofuels* 2019;11(3):377–88. <https://doi.org/10.1080/17597269.2019.1613765>.
- [55] Hsieh CF, Chen KT, Johar T. Fluid flow characteristics of two types rotary engines. *Int J Hydrogen Energy* 2021;46(80):40154–74. <https://doi.org/10.1016/j.ijhydene.2021.09.250>.
- [56] Zervas E. Impact of altitude on fuel consumption of a gasoline passenger car. *Fuel* 2011;90(6):2340–2. <https://doi.org/10.1016/j.fuel.2011.02.004>.
- [57] Moore CS, Collins JH. Compression-ignition engine performance at altitude. *SAE Technical Papers* 1937;32:263–72. <https://doi.org/10.4271/370154>.
- [58] Wang X, Ge Y, Yu L. Combustion and emission characteristics of a heavy-duty diesel engine at idle at various altitudes. *SAE International Journal of Engines* 2013;6(2):1145–51. <https://doi.org/10.4271/2013-01-1516>.
- [59] Ding H, Liu R, Zhang Z, Yang C, Jiao Y, Hu L. Study on the influence of high-altitude on performance of an opposed-piston gasoline engine. In: Proceedings of 2020 Asia-Pacific Conference on image processing Electronics and Computers; 2020. p. 164–71. <https://doi.org/10.1109/IEPEC49694.2020.9115160>.
- [60] Perez PL, Boehman AL. Performance of a single-cylinder diesel engine using oxygen-enriched intake air at simulated high-altitude conditions. *Aero Sci Technol* 2010;14(2):83–94. <https://doi.org/10.1016/j.ast.2009.08.001>.
- [61] Gao J, Tian G, Ma C, Huang L, Xing S. Explorations of the impacts on a hydrogen fuelled opposed rotary piston engine performance by ignition timing under part load conditions. *Int J Hydrogen Energy* 2021;46(21):11994–2008. <https://doi.org/10.1016/j.ijhydene.2021.01.030>.
- [62] Verhelst S, Sierens R. Hydrogen engine-specific properties. *Int J Hydrogen Energy* 2001;26(9):987–90. [https://doi.org/10.1016/S0360-3199\(01\)00026-X](https://doi.org/10.1016/S0360-3199(01)00026-X).
- [63] Wang S, Ji C, Zhang B. Effects of hydrogen addition and cylinder cutoff on combustion and emissions performance of a spark-ignited gasoline engine under a low operating condition. *Energy* 2010;35:4754–60.
- [64] Richards KJ, Senecal PK, Pomraning E. *Converge 3.0*. Madison, WI: Convergent Science; 2023.
- [65] Sener R, Yangaz MU, Gul MZ. Effects of injection strategy and combustion chamber modification on a single-cylinder diesel engine. *Fuel* 2020;266:117122. <https://doi.org/10.1016/j.fuel.2020.117122>.
- [66] Koç MA, Şener R. Prediction of emission and performance characteristics of reactivity-controlled compression ignition engine with the intelligent software based on adaptive neural-fuzzy and neural-network. *J Clean Prod* 2021;318:128642.
- [67] Fan B, Pan J, Tang A, Pan Z, Zhu Y, Xue H. Experimental and numerical investigation of the fluid flow in a side-ported rotary engine. *Energy Convers Manag* 2015;95:385–97. <https://doi.org/10.1016/j.enconman.2015.02.047>.
- [68] Ji C, Chang K, Wang S, Yang J, Wang D, Meng H, Wang H. Effect of injection strategy on the mixture formation and combustion process in a gasoline direct injection rotary engine. *Fuel* 2021;304:121428. <https://doi.org/10.1016/j.fuel.2021.121428>.
- [69] Senecal PK, Pomraning E, Richards KJ, Briggs TE, Choi CY, McDavid RM. Multi-dimensional modeling of direct-injection diesel spray liquid length and flame lift-off length using CFD and parallel detailed chemistry. *SAE Technical Paper* 2003. <https://doi.org/10.4271/2003-01-1043>.
- [70] Liu Y, Jia M, Xie M, Pang B. Improvement on a skeletal chemical kinetic model of iso-octane for internal combustion engine by using a practical methodology. *Fuel* 2013;103:884–91. <https://doi.org/10.1016/j.fuel.2012.07.046>.
- [71] Jia M, Xie M. A chemical kinetics model of iso-octane oxidation for HCCI engines. *Fuel* 2006;85(17–18):2593–604. <https://doi.org/10.1016/j.fuel.2006.02.018>.
- [72] Kan Z, Hu Z, Lou D, Cao Z, Cao J. Effect of the altitude on the combustion characteristics of a low-compression-ratio diesel engine during the start-up process. *Proc Inst Mech Eng - Part D J Automob Eng* 2017;231:1838–47.
- [73] Şener R. Ducted fuel injection: numerical study of soot formation and oxidation using detailed soot modeling approach in a compression ignition engine at different loads. *J Braz Soc Mech Sci Eng* 2022;44(1):45.