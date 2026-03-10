![Logo of The Society of Naval Architects of Korea (SNAOK)](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Logo of The Society of Naval Architects of Korea (SNAOK)

Contents lists available at ScienceDirect

###### International Journal of Naval Architecture and Ocean Engineering

journal homepage: [http://www.journals.elsevier.com/  
international-journal-of-naval-architecture-and-ocean-engineering/](http://www.journals.elsevier.com/international-journal-of-naval-architecture-and-ocean-engineering/)![Cover image of the International Journal of Naval Architecture and Ocean Engineering](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the International Journal of Naval Architecture and Ocean Engineering

# Mean value first principle engine model for predicting dynamic behaviour of two-stroke marine diesel engine in various ship propulsion operations

![Check for updates button](4f4b52340aaccb1bcf733468dca9ee03_img.jpg)

Check for updates button

Congbiao Sui <sup>a, b</sup>, Peter de Vos <sup>b</sup>, Douwe Stapersma <sup>b</sup>, Klaas Visser <sup>b</sup>, Hans Hopman <sup>b</sup>, Yu Ding <sup>a, \*</sup><sup>a</sup> College of Power and Energy Engineering, Harbin Engineering University, Harbin, China<sup>b</sup> Faculty of Mechanical, Maritime and Materials Engineering, Delft University of Technology, Delft, the Netherlands

## A R T I C L E I N F O

### Article history:

Received 28 June 2021

Received in revised form

6 December 2021

Accepted 24 December 2021

Available online 30 December 2021

### Keywords:

Two-stroke marine diesel engine mean

value first principle model

Two-zone scavange model

Engine dynamic performance

Thermal loading

1D ship propulsion system model

## A B S T R A C T

Analysis of ship propulsion system performance is often performed using detailed hydrodynamic models to assess load changes, which are subsequently compared to static engine limits, or by detailed engine models that are rarely integrated with sufficiently detailed propulsion models for load change estimation. To investigate the *dynamic* engine (overloading) behaviour and ship propulsion performance under *various heavy* operating conditions, a Mean Value First Principle Parametric (MVFP) engine model is integrated into a ship propulsion system model in this paper. An upgraded thermodynamic-based MVFP model for two-stroke marine diesel engines is presented, in particular a newly developed MVFP gas exchange model. Based on the integrated propulsion system model of a benchmark ocean-going chemical tanker, the engine dynamic behaviour during ship acceleration, deceleration and crash stop has been investigated. Results show that, during dynamic processes, the engine could be thermally overloaded even if the engine power trajectory is inside the static engine operating envelope. The paper contributes to finding proper indicators for thermal overloading of modern two-stroke marine diesel engines. It is demonstrated that when matching the engine with the propeller and designing the ship propulsion control system, not only the static engine operating envelope, but also the dynamic engine behaviour should be considered.

© 2021 Society of Naval Architects of Korea. Production and hosting by Elsevier B.V. This is an open access article under the CC BY-NC-ND license (<http://creativecommons.org/licenses/by-nc-nd/4.0/>).

## 1. Introduction

Due to the well-developed technology and high propulsion efficiency, two-stroke marine diesel engines have been dominantly used as the main propulsion engines of large ocean-going cargo ships such as tankers, bulk carriers and container ships (MAN, 2018), which together account for 91% of the world cargo-carrying fleet in terms of dead-weight tons (dwt) (Carlton et al., 2013; UNCTAD, 2019). In the coming decades, two-stroke marine diesel engines will continue to provide the largest part of most propulsion power for the international shipping (Geertsma et al., 2018; IMO, 2020). When investigating the ship performance in various operating conditions, among others the capability of the

ship propulsion plant to accelerate the ship, to carry out a crash-stop of the ship, to turn the bow of the ship into head sea, and to respond to the dynamic seaway in adverse sea conditions, etc., needs to be evaluated. Since the interactions between the engine, the propeller, the ship and the high sea states are highly dynamic rather than static, not only static but also dynamic behaviour of the ship and the propulsion system should be evaluated, taking not only the static load limits of the main engine but also the dynamic load limits into account (Holt and Nielsen, 2021). However, research in this regard is still limited in published literature. A static engine model that only considers static engine torque or power and only takes the static engine operational profile into account is inadequate for predicting the engine's dynamic (over)loading conditions, and may lead to misleadingly optimistic predictions. So, correctly modelling the main engine as well as the ship propulsion system is a critical aspect when investigating ship propulsion performance in various operating conditions.

In order of complexity, engine models can be recognized as:

\* Corresponding author.

E-mail address: [dingyu@hrbeu.edu.cn](mailto:dingyu@hrbeu.edu.cn) (Y. Ding).

Peer review under responsibility of The Society of Naval Architects of Korea.

| <b>Nomenclature</b>      |                                                               |
|--------------------------|---------------------------------------------------------------|
| <b>Abbreviations</b>     |                                                               |
| AC                       | alternating current                                           |
| AG                       | auxiliary generator                                           |
| Aux. Eng                 | auxiliary engine                                              |
| Aux. Gen                 | auxiliary generator                                           |
| BDC                      | bottom dead centre                                            |
| blld                     | blowdown                                                      |
| CPP                      | controllable pitch propeller                                  |
| DWT                      | dead weight tonnage                                           |
| EC                       | exhaust valve close                                           |
| EO                       | exhaust valve open                                            |
| exp                      | expelling                                                     |
| GB                       | gearbox                                                       |
| Gen                      | generator                                                     |
| IC                       | inlet ports close                                             |
| IO                       | inlet ports open                                              |
| MCR                      | maximum continuous rating                                     |
| mep                      | mean effective pressure                                       |
| MG                       | (shaft) motor/generator                                       |
| Mot                      | motor                                                         |
| MVFPP                    | mean value first principle parametric                         |
| P/D                      | pitch/diameter ratio                                          |
| PTO                      | power take off                                                |
| PTI                      | power take in                                                 |
| scav                     | scavenge                                                      |
| SI                       | surge index                                                   |
| SLC                      | single lever command                                          |
| TDC                      | top dead centre                                               |
| <b>Roman Symbols</b>     |                                                               |
| <i>a</i>                 | isochoric combustion parameter (–); constant coefficients (–) |
| <i>b</i>                 | isobaric combustion parameter (–); constant coefficients (–)  |
| <i>c</i>                 | isothermal combustion parameter (–)                           |
| <i>c<sub>p</sub></i>     | specific heat at constant pressure (J/kg/K)                   |
| <i>c<sub>v</sub></i>     | specific heat at constant volume (J/kg/K)                     |
| <i>i</i>                 | number of cylinders of the engine (–)                         |
| <i>k</i>                 | number of revolutions per cycle (–)                           |
| <i>m</i>                 | mass (kg)                                                     |
| <i>M</i>                 | torque (Nm)                                                   |
| <i>m<sub>fuel</sub></i>  | injected fuel mass per cycle (kg)                             |
| <i>N</i>                 | engine rotational speed (r/s)                                 |
| <i>n<sub>eng</sub></i>   | engine rotational speed (r/s)                                 |
| <i>n<sub>comp</sub></i>  | polytropic compression exponent (–)                           |
| <i>n<sub>exp</sub></i>   | polytropic expansion exponent (–)                             |
| <i>n<sub>p</sub></i>     | propeller rotational speed (r/s)                              |
| <i>n<sub>TC</sub></i>    | turbocharger rotational speed (r/s)                           |
| <i>p</i>                 | pressure (Pa)                                                 |
| <i>P<sub>AG,e</sub></i>  | electrical power of auxiliary generator (W)                   |
| <i>P<sub>B,aux</sub></i> | auxiliary engine power (W)                                    |
| <i>P<sub>e</sub></i>     | ship effective power (W)                                      |
| <i>P<sub>Elec</sub></i>  | electrical power of onboard grid (W)                          |
| <i>P<sub>S</sub></i>     | shaft power (W)                                               |
| <i>p<sub>max</sub></i>   | maximum in-cylinder pressure (Pa)                             |
| <i>P<sub>MG,e</sub></i>  | electrical power of shaft motor/generator (W)                 |
| <i>P<sub>MG,m</sub></i>  | mechanical power of shaft motor/generator (W)                 |
| <i>q</i>                 | specific heat (J)                                             |
| <i>R</i>                 | gas constant (J/kg/K)                                         |
| <i>s</i>                 | slip factor (–)                                               |
| <i>sfc</i>               | specific fuel consumption (g/kWh)                             |
| <i>t</i>                 | thrust deduction fraction (–); time (s)                       |
| <i>T</i>                 | temperature (K); thrust (N)                                   |
| <i>V</i>                 | cylinder volume (m <sup>3</sup> )                             |
| <i>V<sub>S</sub></i>     | ship speed (m/s)                                              |
| <i>V<sub>A</sub></i>     | propeller advance speed (m/s)                                 |
| <i>w</i>                 | wake fraction (–); specific work (J)                          |
| <i>x</i>                 | air mass ratio (–)                                            |
| <i>X</i>                 | fuel rack position (–)                                        |
| <i>y</i>                 | temperature ratio (–)                                         |
| <b>Greek symbols</b>     |                                                               |
| <i>δ</i>                 | fuel addition factor (–)                                      |
| <i>η</i>                 | efficiency (–)                                                |
| <i>κ</i>                 | specific heat ratio (–)                                       |
| <i>γ</i>                 | specific heat ratio (–)                                       |
| <i>χ</i>                 | ratio between specific heats of exhaust gas and air (–)       |
| <i>λ</i>                 | air excess ratio (–)                                          |
| <i>π</i>                 | compression ratio (–)                                         |
| <i>τ</i>                 | temperature ratio (–)                                         |
| <i>ε</i>                 | heat exchanger effectiveness (–)                              |
| <i>Φ</i>                 | mass flow (kg/s)                                              |
| <b>Subscripts</b>        |                                                               |
| <i>I, II</i>             | first, second scavenge stage                                  |
| <i>a</i>                 | air                                                           |
| <i>A</i>                 | A zone during scavenge process                                |
| <i>ac</i>                | air cooler                                                    |
| <i>amb</i>               | ambient                                                       |
| <i>blld-out</i>          | blowdown-out                                                  |
| <i>eng</i>               | engine                                                        |
| <i>EV</i>                | exhaust valve                                                 |
| <i>g</i>                 | gas                                                           |
| <i>nom</i>               | nominal condition                                             |
| <i>r</i>                 | ratio; relative                                               |
| <i>sc</i>                | scavenge                                                      |
| <i>sc-in</i>             | scavenge-in                                                   |
| <i>sc-out</i>            | scavenge-out                                                  |
| <i>sc-tr</i>             | trapped condition after scavenge                              |

models only consisting of lookup tables and/or best-fit polynomials, transfer function models, mean value models, filling and emptying (zero- or one-dimensional crank angle models), phenomenological multizone models, and CFD (Computational Fluid Dynamics) models (Baldi et al., 2015; Schulten, 2005; Theotokatos et al., 2018). Generally, an engine model with higher fidelity (which is different from accuracy) is more complex, requiring more input parameters, longer calculation time and always are more difficult to adapt to different operating conditions

(Baldi et al., 2015; Guan et al., 2014; Payri et al., 2011).

Since the subject of research in this paper is the ship dynamic propulsion performance, especially the engine performance in various operating conditions is important. Then an appropriate engine model, capable of predicting the overall engine parameters in both steady (static) and transient (dynamic) operating conditions, must be integrated into the ship propulsion system model. The engine model must be able to calculate, for instance, the fuel consumption, air mass flow, scavenge efficiency, air excess ratio,

temperatures and pressures in different component volumes, engine torque and speed, heat and mechanical losses, etc. All these variables have a time scale of the complete engine operating cycle rather than a small crank angle, for relevant time scales refer to Fig. 6.1 in (Shi, 2013). In that case a mean value first principle model is considered a good choice since it is capable of calculating the overall engine performance with the time scale of each operating cycle with a satisfactory accuracy and low computation time (Schulten, 2005; Sui et al., 2017). Another requirement of the engine model is that, being part of a larger ship model intended for exploring research, it should fully parametric like the rest of the model. For these reasons, a thermodynamic-based Mean Value First Principle Parametric (MVFPP) engine model has been used in this research.

The thermodynamic-based MVFPP model was originally developed by Delft University of Technology (the Netherlands) and Netherlands Defence Academy (Grimmelius et al., 2007; Sui et al., 2017). The model has been updated and used for many different research applications. In (Grimmelius and Stapersma, 2000) the engine thermal loading prediction and control optimization for marine diesel engines using the MVFPP model has already been studied. In (Schulten and Stapersma, 2003), the mean value model of the gas exchange process for four-stroke diesel engines has been updated. In (Schulten, 2005), the updated MVFPP model for four-stroke diesel engines has been integrated into the ship propulsion and manoeuvring system and the interaction between diesel engines, ship and propellers during manoeuvring has been investigated. Later an analytic parametric turbocharger model replacing the compressor and turbine maps was introduced into the MVFPP model making it fully parametric. In (Stapersma, 2008) this model was used for investigating the influence of turbocharger matching on ship propulsion performance. In (Geertsma et al., 2017) and (Geertsma et al., 2018) an MVFPP engine model with a simplified gas exchange process model has been used to investigate the influence of different propeller control strategies on the performance of the ship propulsion performance. In (Sapra et al., 2017), using the MVFPP engine model, the influence of the engine back pressure on the thermal loading has been investigated to define the back pressure limits. The above-mentioned MVFPP engine models have been mainly applied for four-stroke engines. This paper will present the changes made, especially of the gas exchange process, in order to use the model for two-stroke marine diesel engines. In particular a novel mean value scavenging model has been developed that will be presented in this paper.

For two-stroke diesel engines, the scavenging process, which is driven by the pressure difference between the inlet receiver and the outlet receiver, is a crucial part of the engine cycle (He and Wei, 2017; Liu et al., 2014). To predict the scavenging process of the two-stroke diesel engines for various applications, scavenging models can be divided into three categories: one-stage models, multi-zone models and CFD models (Ding et al., 2019; Sher, 1990). One-stage models, which include a perfect displacement model and a perfect mixing model, are not realistic for predicting the scavenging process of modern two-stroke diesel engines as the perfect displacement model overestimates while the perfect mixing model underestimates the scavenging performance (Sher, 1990). Due to the large stroke/bore ratios of modern two-stroke marine diesel engines, multi-zone models are preferable for accurate predictions of the scavenging performance (Ding et al., 2019; Fotinos et al., 2019; Sher, 1990). However, most of the multi-zone models are empirical or semi-empirical models, which need empirical or experimental parameters of the engine, rather than first principle models. CFD models are not very practical for predicting the overall engine performance (Sher, 1990), as the computational cost remains high in terms of both resources and time (Cagin et al., 2016).

In this paper, a two-zone mean value first principle model of the scavenging process of a two-stroke marine diesel engine will be proposed that is suitable to be integrated in a MVFPP engine model.

The engine thermal loading, mechanical loading and compressor surge limits are the important features in relation to the engine and ship operational safety. The engine operating envelope in particular the torque/speed limit of a turbocharged diesel engine is shaped mainly by the engine thermal loading limit (MAN, 2018). During engine operations, to protect the engine from being overloaded, the engine is not allowed to operate outside the engine envelope, which is specified by the engine manufacturer, and this is normally controlled by the engine governor with a fuel rack limiter (Grimmelius and Stapersma, 2000; Schulten, 2005). In order to investigate the influence of various operating conditions on the thermal loading of the engine, quantitative thermal loading indicators need to be defined. To define and quantify the engine thermal loading, a number of thermal loading indicators have been introduced in (Grimmelius and Stapersma, 2000) when investigating the influence of irregular waves as well as different control strategies on the thermal loading of a turbocharged diesel engine. These thermal loading indicators includes the air excess ratio, charge pressure, engine slip factor, maximum in-cylinder temperature, cylinder temperature just before exhaust valve opening (EO), gas temperature directly after exhaust valve, exhaust receiver temperature and gas exhaust temperature (after turbine), etc. Among others, the air excess ratio can be used as the indicator of both engine smoke-limit and thermal loading (Stapersma, 2010a). Visible (black) smoke in the engine exhaust will be observed when the air excess ratio is lower than the smoke-limit as the combustion is incomplete due to the insufficient air. A low air excess ratio will also cause high surface temperature of engine components that could lead to a reduction of operational life or catastrophic failure of the components (Nanda et al., 2017).

Summarising, the objective of this paper is to integrate an MVFPP engine model into the ship propulsion system model of a 13,000 DWT ocean-going chemical tanker to investigate the dynamic engine (overloading) behaviour and ship propulsion performance under various (heavy) operating conditions, for which there is limited research in published literature. In order to do so, an upgraded thermodynamic-based Mean Value First Principle Parametric (MVFP) model for two-stroke marine diesel engines is presented, in particular a newly developed mean value first principle gas exchange model. Before integrating the engine model in the ship system model, it is tested for static performance and operational limits. Finally, this paper provides an integrated ship propulsion system model that has been calibrated and validated using measurement data from engine testbed trial, ship model tests in towing tank and a full-scale ship test during sea trial, which is rare as these data are difficult to obtain in the public domain.

The outline of this paper is:

- (1) To introduce the benchmark ocean-going chemical tanker and the ship propulsion system model used in this research (section 2);
- (2) To introduce the mean value first principle parametric model for two-stroke marine diesel engine, including the closed cylinder process model, gas exchange process model, turbocharger model, air cooler model, auxiliary blower model, engine mechanical and heat losses models with the main focus on the recent additions to the model (section 3 and Appendix A and B);
- (3) To calibrate and validate the engine model and the integrated ship propulsion system model using engine test data, ship model test and sea trial test data (section 4);

- (4) Using this MVFPP engine model, to investigate the engine static thermal loading and operational limits in the whole engine operating envelope and using the integrated ship propulsion system model, to investigate the dynamic engine behaviour during ship acceleration, deceleration and crash stop operations (section 5);
- (5) Conclusions and limitations of this research and recommendations for future work will be provided in section 6.

## 2. A benchmark ocean-going chemical tanker and the ship propulsion system model

### 2.1. A benchmark ocean-going chemical tanker

The 13000 DWT chemical tanker introduced in (Sui et al., 2019, 2020) has been chosen as the benchmark ocean-going cargo ship in this paper to investigate the engine dynamic behaviour during ship propulsion operations. The general information of this ship is presented in Table 1. The main engine of the benchmark chemical tanker is a low speed two-stroke marine diesel engine, which drives a Controllable Pitch Propeller (CPP) and a shaft generator (power take off, PTO). In (Sui et al., 2020), it has been conceptually modified such that the shaft generator can also work as a shaft motor (power take in, PTI) (Fig. 1).

### 2.2. Ship propulsion system model

The ship propulsion system model of the benchmark chemical tanker (Fig. 2) that has been introduced in (Sui et al., 2020), will be used in this paper to investigate the ship propulsion system performance in various operating conditions. The applied sub-models of ship resistance, propeller open water characteristics, wake factor, thrust deduction factor and relative rotative efficiency have been introduced in (Sui et al., 2019). These models will not be elaborated in this paper. However, section 4.2 does provide a brief verification and validation of these models.

Thus, in this paper, the emphasis will be on the engine modelling as the engine model introduced in (Sui et al., 2019) and (Sui et al., 2020), which is a regression model based on engine measurement data, has here been replaced by a mean value first principle parametric model.

## 3. Mean Value First Principle Parametric (MVFPP) model of two-stroke marine diesel engine

### 3.1. Concepts and definitions of MVFPP engine model

#### 3.1.1. In-cylinder processes of two-stroke marine diesel engine

The in-cylinder processes in a diesel engine cycle on the highest level consist of the closed cylinder process and the gas exchange process (Fig. 3). For a two-stroke diesel engine in the case where the exhaust valve closes (EC) after the inlet ports closes (IC), the closed

![Diagram of the updated chemical tanker propulsion system and electric generating system. The Main Engine is connected to a shaft generator (MG) and a Controllable Pitch Propeller (CPP). The MG is connected to the PTO/PTI GB (Power Take Off/Power Take In Gearbox). The PTO/PTI GB is connected to an Auxiliary Engine (Aux. Engine) and an Electric Load. The Aux. Engine is connected to an Alternator (AG), which is connected to the AC Grid. The AC Grid is also connected to the Electric Load.](8d3afc46f415cad96c2eba639730f7c3_img.jpg)

Diagram of the updated chemical tanker propulsion system and electric generating system. The Main Engine is connected to a shaft generator (MG) and a Controllable Pitch Propeller (CPP). The MG is connected to the PTO/PTI GB (Power Take Off/Power Take In Gearbox). The PTO/PTI GB is connected to an Auxiliary Engine (Aux. Engine) and an Electric Load. The Aux. Engine is connected to an Alternator (AG), which is connected to the AC Grid. The AC Grid is also connected to the Electric Load.

Fig. 1. Layout of the updated chemical tanker propulsion system and electric generating system (Sui et al., 2020).

cylinder process starts from EC and ends at EO (exhaust valve opens). The closed cylinder process of four-stroke diesel engines has been modelled by the 6-point Seiliger process (1-2-3-4-5-6) (Seiliger, 1922, 1926) in (Sui et al., 2017). In this paper, the same 6-point Seiliger process model with some updates is applied for modelling the closed cylinder process of the two-stroke marine diesel engine. According to the 6-point Seiliger process, the closed cylinder process is characterised by the following five stages: (1–2) polytropic compression; (2–3) isochoric combustion; (3–4) isobaric combustion and expansion; (4–5) isothermal combustion and expansion; (5–6) polytropic expansion.

The gas exchange process (6-7-I–II–III) (Fig. 3) starts immediately when the exhaust valve opens (EO) after the closed cylinder process and ends at EC and for a two-stroke diesel engine three processes, i.e. blowdown, scavenging and an expelling process (Fig. 3), are distinguished based on theories in (Stapersma, 2010b) and (Ding et al., 2019).

- Blowdown (6–7)

When the exhaust valve opens, due to the higher pressure in the cylinder than the pressure in the outlet receiver, part of the gases in the cylinder will blow out entering the outlet receiver automatically. The remaining gases in the cylinder continue their expansion process while the blowdown gases entering the outlet receiver together with the outgoing gases from the cylinder during the following processes will build up the pressure in the outlet receiver before the turbine.

- Scavenging (IO–IC)

When the inlet ports open, due to the pressure difference

Table 1

General information of the chemical tanker and the propulsion system (Sui et al., 2019).

| Particulars of the Chemical Tanker    | Main Engine |                               | Propeller             |                  |
|---------------------------------------|-------------|-------------------------------|-----------------------|------------------|
| Length Between Perpendiculars [m]     | 113.80      | Type                          | MAN 6S35ME (2-stroke) | MAN ALPHA        |
| Breadth Molded [m]                    | 22.00       | Rated Power [kW]              | 4170                  | CPP              |
| Depth Molded [m]                      | 11.40       | Rated Speed [rpm]             | 167                   | 167              |
| Design Draught [m]                    | 8.50        | Stroke [m]                    | 1.55                  | Number of Blades |
| Design Displacement [m <sup>3</sup> ] | 16988       | Bore [m]                      | 0.35                  | 4                |
| Capacity DWT [ton]                    | 13021       | p <sub>max</sub> at MCR [MPa] | 18.5                  | Diameter [m]     |
| Design Speed [kn]                     | 13.30       | Number of Cylinders [-]       | 6                     | 4.30             |

![Structure scheme of integrated ship propulsion and electric generating systems model of the chemical tanker. The diagram is divided into three main sections: Ship Propulsion System, PTO/PTI System, and Electric Generation System. The Ship Propulsion System includes a Main Engine, Shaftline, and Propeller, with inputs for n_eng,set, n_eng, M_eng, M_shaft, M_del, n_p, P/D_prop, V_A, and T_prop. The PTO/PTI System includes a PTO/PTI Gearbox and Shaft Gen./Mot., with inputs for M_PTO/PTI, n_PTO/PTI, P_MG,m, and P_MG,e. The Electric Generation System includes Auxiliary Gensets (Aux.Eng. and Aux.Gen.) and a Main Switchboard, with inputs for P_B,aux, P_AG,e, and P_Elec. A central 'Propulsion and Electric Systems Control' block manages the system. The Ship block outputs T_ship and V_s, with a 1-t block and a 1-w block for efficiency calculations.](e394c2b5c61344f6a12397f430086072_img.jpg)

Structure scheme of integrated ship propulsion and electric generating systems model of the chemical tanker. The diagram is divided into three main sections: Ship Propulsion System, PTO/PTI System, and Electric Generation System. The Ship Propulsion System includes a Main Engine, Shaftline, and Propeller, with inputs for n\_eng,set, n\_eng, M\_eng, M\_shaft, M\_del, n\_p, P/D\_prop, V\_A, and T\_prop. The PTO/PTI System includes a PTO/PTI Gearbox and Shaft Gen./Mot., with inputs for M\_PTO/PTI, n\_PTO/PTI, P\_MG,m, and P\_MG,e. The Electric Generation System includes Auxiliary Gensets (Aux.Eng. and Aux.Gen.) and a Main Switchboard, with inputs for P\_B,aux, P\_AG,e, and P\_Elec. A central 'Propulsion and Electric Systems Control' block manages the system. The Ship block outputs T\_ship and V\_s, with a 1-t block and a 1-w block for efficiency calculations.

Fig. 2. Structure scheme of integrated ship propulsion and electric generating systems model of the chemical tanker (Sui et al., 2020).

![Conceptual model of in-cylinder pressure of a two-stroke turbocharged diesel engine, IC before EC. The figure shows a cross-section of a cylinder with exhaust gas exiting and fresh air entering. The pressure curve (P) vs. crank angle shows the cycle from BDC to BDC. The cycle is divided into the Closed Cylinder Process (1-2-3-4) and Gas Exchange (4-5-6-7). Key points include BDC, IC, EC, TDC, EO, IO, bld, scav, and exp. The pressure levels PIR, Psc, and POR are indicated. The Main Switchboard is shown as a central control point for the gensets.](b15e3860e0c96ed16ce77f032da6f107_img.jpg)

Conceptual model of in-cylinder pressure of a two-stroke turbocharged diesel engine, IC before EC. The figure shows a cross-section of a cylinder with exhaust gas exiting and fresh air entering. The pressure curve (P) vs. crank angle shows the cycle from BDC to BDC. The cycle is divided into the Closed Cylinder Process (1-2-3-4) and Gas Exchange (4-5-6-7). Key points include BDC, IC, EC, TDC, EO, IO, bld, scav, and exp. The pressure levels PIR, Psc, and POR are indicated. The Main Switchboard is shown as a central control point for the gensets.

Fig. 3. Conceptual model of in-cylinder pressure of a two-stroke turbocharged diesel engine, IC before EC.

between the inlet receiver and the outlet receiver, scavenging gases will flow through the cylinder, driving the remaining exhaust gases out of the cylinder and providing fresh air in the cylinder.

##### - Expelling (IC-EC)

When the inlet ports are closed and the exhaust valve is still open (IC before EC), a part of the gases in the cylinder will be expelled by the upward moving piston. There will be an air loss during the expelling process.

#### 3.1.2. vol and resistance elements in MVFPP engine model

According to the information in the project guide of MAN 6S35ME two-stroke diesel engine (MAN, 2014a), the layout diagram of the engine is shown in Fig. 4. The model structure of the

two-stroke marine diesel engine is shown in Fig. 5. Different components in the model, including the air filter, compressor, air cooler, auxiliary blow/non-return valve, inlet receiver, cylinder(s), outlet receiver, turbine and silencer, are connected with each other by the mass flow, temperature and pressure. When modelling the components, the resistance element and volume element method introduced in (Schulten and Stapersma, 2003), which is akin to the lumped parameters modelling approach (Barton, 1992; Colonna and van Putten, 2007; Hangos and Cameron, 2001; van Putten and Colonna, 2007), has been used. The mass flows are calculated as a function of the pressure differences over the components using resistance elements, which actually are algebraic remnants of the momentum balance, while the mass, composition, temperature and pressure in a volume are calculated using volume elements, which actually are integrators (breaking the algebraic loops), based

![Layout diagram of MANGS35ME two-stroke marine diesel engine. The diagram shows a vertical flow from top to bottom: AF (Air Filter) -> COM (Compressor) -> CAC (Air Cooler) -> NRV (Non Return Valve) and AB (Auxiliary Blower) -> IR (Inlet Receiver) -> CYL (Cylinder) -> OR (Outlet Receiver) -> TUR (Turbine) -> SIL (Silencer). A feedback loop from TUR to COM is shown with a red arrow.](a7d78d22e465dea388b31d0739f9d0cd_img.jpg)

AF: Air Filter  
COM: Compressor  
CAC: Air Cooler  
NRV: Non Return Valve  
AB: Auxiliary Blower  
IR: Inlet Receiver  
CYL: Cylinder  
OR: Outlet Receiver  
TUR: Turbine  
SIL: Silencer

Layout diagram of MANGS35ME two-stroke marine diesel engine. The diagram shows a vertical flow from top to bottom: AF (Air Filter) -> COM (Compressor) -> CAC (Air Cooler) -> NRV (Non Return Valve) and AB (Auxiliary Blower) -> IR (Inlet Receiver) -> CYL (Cylinder) -> OR (Outlet Receiver) -> TUR (Turbine) -> SIL (Silencer). A feedback loop from TUR to COM is shown with a red arrow.

Fig. 4. Layout diagram of MANGS35ME two-stroke marine diesel engine.

on the overall and partial mass balance, energy balance and the ideal gas law.

In a volume element, the mass ' $m$ ' is accumulated at a certain temperature ' $T$ ' and pressure ' $p$ ' and it consists of pure air ' $m_a$ ' and the stoichiometric exhaust gas ' $m_g$ ' as shown in Eq. (1). The composition of the mass is specified by the air mass ratio ' $x$ ' defined by Eq. (2). So, ' $x$ ' indicates the purity of the mass and ' $x = 1$ ' implies pure air while ' $x = 0$ ' implies stoichiometric combustion gas.

$$m = m_a + m_g. \quad (1)$$

$$x \stackrel{\text{def}}{=} \frac{m_a}{m}. \quad (2)$$

Through the resistance element, the ingoing or outgoing mass flows with certain temperature and composition enter or exit the volume elements. For instance, there is an ingoing mass flow ' $\dot{m}_{in}$ ', with temperature ' $T_{in}$ ' and composition ' $x_{in}$ ' entering the cylinder volume through the inlet ports; and an outgoing mass flow ' $\dot{m}_{out}$ ', with temperature ' $T_{out}$ ' and composition ' $x_{out}$ ' exiting the cylinder

**Table 2**  
Seiliger process definition and parameters (Stapersma, 2010a).

| Seiliger stage | Volume $V$              | Pressure $p$                       | Temperature $T$                      | Seiliger parameters |
|----------------|-------------------------|------------------------------------|--------------------------------------|---------------------|
| 1–2            | $\frac{V_1}{V_2} = r_c$ | $\frac{p_2}{p_1} = r_c^{n_{comp}}$ | $\frac{T_2}{T_1} = r_c^{n_{comp}-1}$ | $r_c, n_{comp}$     |
| 2–3            | $\frac{V_3}{V_2} = 1$   | $\frac{p_3}{p_2} = a$              | $\frac{T_3}{T_2} = a$                | $a$                 |
| 3–4            | $\frac{V_4}{V_3} = b$   | $\frac{p_4}{p_3} = 1$              | $\frac{T_4}{T_3} = b$                | $b$                 |
| 4–5            | $\frac{V_5}{V_4} = c$   | $\frac{p_4}{p_5} = c$              | $\frac{T_5}{T_4} = 1$                | $c$                 |
| 5–6            | $\frac{V_6}{V_5} = r_e$ | $\frac{p_5}{p_6} = r_e^{n_{exp}}$  | $\frac{T_6}{T_5} = r_e^{1-n_{exp}}$  | $r_e, n_{exp}$      |

volume through the outlet valves.

The sub-models of engine components including turbocharger, air cooler, auxiliary blower, non-return valve, as well as the models of exhaust valve temperature, engine mechanical and heat losses are presented in Appendix B.

### 3.2. Closed cylinder process model

The five Seiliger stages (Seiliger, 1922, 1926) are parameterised by the Seiliger parameters as shown in Table 2. The three combustion stages, i.e., the isochoric combustion, the isobaric combustion and the isothermal combustion are characterised by the combustion parameters  $a$ ,  $b$  and  $c$  respectively. The polytropic compression is parameterised by the polytropic compression exponent  $n_{comp}$  and the effective compression ratio  $r_c$ ; while the polytropic expansion is indicated by the polytropic expansion exponent  $n_{exp}$  and the expansion ratio  $r_e$ . The pressures, temperatures, specific work and heat of each Seiliger stage are determined by the Seiliger parameters as shown in Tables 2 and 3. Models determine the Seiliger combustion parameters  $a$  and  $b$ , which are functions of engine rotational speed, injected fuel mass per cycle and ignition delay, etc. The Seiliger combustion parameter  $c$  is determined based on the energy balance of the combustion process, i.e., the heat input during stage 4–5 equals the total heat input minus the heat inputs during stages 2–3 and 3–4. It is the authors'

![Model structure of two-stroke marine diesel engine. The diagram shows a complex network of components: AF (Air Filter), IV (Inlet Volume), CAC (Charge Air Cooler), AC (Air Cover), COM (Compressor), BV (Volume before NRV), NRV/AB (Non-Return Valve / Auxiliary Blower), IR (Inlet Receiver), CIP (Cylinder Inlet Ports), CYL (Cylinder volume), COV (Cylinder Outlet Valve), OR (Outlet Receiver), TUR (Turbine), SV (Silencer Volume), SIL (Silencer), and a Fuel pump. Mass flows (m_dot) and temperatures (T) are indicated with arrows. A feedback loop for rotational speed (n_RC) is shown at the bottom.](cfbf0f2ddbc35370b0b8c6d043f25eb2_img.jpg)

AB: Auxiliary Blower  
CAC: Charge Air Cooler  
CYL: Cylinder volume  
OR: Outlet Receiver  
AC: Air Cover  
CIP: Cylinder Inlet Ports  
IR: Inlet Receiver  
SIL: Silencer  
AF: Air Filter  
COM: Compressor  
IV: Inlet Volume  
SV: Silencer Volume  
BV: Volume before NRV  
COV: Cylinder Outlet Valve  
NRV: Non-Return Valve  
TUR: Turbine

Model structure of two-stroke marine diesel engine. The diagram shows a complex network of components: AF (Air Filter), IV (Inlet Volume), CAC (Charge Air Cooler), AC (Air Cover), COM (Compressor), BV (Volume before NRV), NRV/AB (Non-Return Valve / Auxiliary Blower), IR (Inlet Receiver), CIP (Cylinder Inlet Ports), CYL (Cylinder volume), COV (Cylinder Outlet Valve), OR (Outlet Receiver), TUR (Turbine), SV (Silencer Volume), SIL (Silencer), and a Fuel pump. Mass flows (m\_dot) and temperatures (T) are indicated with arrows. A feedback loop for rotational speed (n\_RC) is shown at the bottom.

Fig. 5. Model structure of two-stroke marine diesel engine (updated from (Schulten, 2005)).

**Table 3**  
Specific work and heat in Seiliger process (Stapersma, 2010a).

| Seiliger stage | Specific work $w$ (J)                                               | Specific heat $q$ (J)                                                                            |
|----------------|---------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| 1–2            | $w_{12} = \frac{R_{g,12}}{n_{\text{comp}} - 1} \cdot (T_1 - T_2)$   | $q_{12} = \frac{k_{12} - n_{\text{comp}}}{n_{\text{comp}} - 1} \cdot c_{v,12} \cdot (T_2 - T_1)$ |
| 2–3            | $w_{23} = 0$                                                        | $q_{23} = c_{v,23} \cdot (T_3 - T_2)$                                                            |
| 3–4            | $w_{34} = R_{g,34} \cdot (T_4 - T_3)$                               | $q_{34} = c_{p,34} \cdot (T_4 - T_3)$                                                            |
| 4–5            | $w_{45} = R_{g,45} \cdot T_4 \cdot \ln\left(\frac{V_5}{V_4}\right)$ | $q_{45} = R_{g,45} \cdot T_4 \cdot \ln\left(\frac{V_5}{V_4}\right)$                              |
| 5–6            | $w_{56} = \frac{R_{g,56}}{n_{\text{exp}} - 1} \cdot (T_5 - T_6)$    | $q_{56} = \frac{n_{\text{exp}} - k_{56}}{n_{\text{exp}} - 1} \cdot c_{v,56} \cdot (T_6 - T_5)$   |

experience that the three combustion parameters of the extended Seiliger cycle give sufficient freedom to characterize combustion (Ding, 2011). Modeling gas combustion has proven to be possible (Georgescu et al., 2016). In fact, a single Wiebe model has not essentially more parameters, although a double Wiebe model has. However, it has been found (Sapra et al., 2020) that Seiliger modeling may give better results than double Wiebe modeling.

The effective compression ratio  $r_c$  is determined by the geometry of the engine combustion chamber and the timing of inlet valve closing (IC) for 4-stroke engine, while exhaust valve closing (EC) for 2-stroke engine. So, for a certain engine the effective compression ratio  $r_c$  will be constant. The polytropic compression exponent  $n_{\text{comp}}$  and the polytropic expansion exponent  $n_{\text{exp}}$  are all set as constant in the model. The expansion ratio  $r_e$  is determined by the combustion parameters  $b$ ,  $c$  and the timing of the exhaust valve opening (EO). Finally, the gas properties (gas constant, specific heat and isentropic index) are determined at mean values of temperature and composition of the Seiliger stage. The closed cylinder process model has been investigated and analysed extensively in (Ding, 2011; Schulten, 2005; Sui et al., 2017), and it will not be elaborated in this paper. The focus of the two-stroke marine diesel engine model in this paper lies on the gas exchange process model.

### 3.3. Gas exchange process model

#### 3.3.1. Blowdown model

The blowdown process (6–7) starts immediately when the exhaust valve opens (EO) after the closed cylinder process. During the blowdown process, a part of the gases leaves the cylinder and the rest of the gases remain in the cylinder. It is assumed that the remaining gases in the cylinder continue the polytropic expansion with an increasing cylinder volume (from  $V_6$  to  $V_7$ ). The pressure in the cylinder  $p_7$  after blowdown is assumed to be equal to the scavenging pressure  $p_{\text{scav}}$ , which due to flow losses is somewhat higher than the pressure in the outlet receiver  $p_{\text{or}}$ . The part of the gases that blows down out of the cylinder expands during outflow into the outlet receiver.

The temperature and the mass left in the cylinder after blowdown are calculated by Eqs. (3) and (4) respectively. The mass and temperature of the blowdown-out gases into the outlet receiver during blowdown are calculated by Eqs. (5) and (6) respectively.

$$T_7 = T_6 \cdot \left(\frac{p_7}{p_6}\right)^{\frac{n_{\text{exp}}-1}{n_{\text{exp}}}} \quad (3)$$

$$m_7 = \frac{p_{\text{scav}} \cdot V_{10}}{R_7 \cdot T_7} \quad (4)$$

$$m_{\text{bld-out}} = m_6 - m_7 \quad (5)$$

$$T_{\text{bld-out}} = \frac{m_6 \cdot T_{\text{bld}} - m_7 \cdot T_7}{m_{\text{bld-out}}} \cdot \left( \frac{1}{k_{\text{bld}}} + \frac{k_{\text{bld}} - 1}{k_{\text{bld}}} \cdot \frac{p_{\text{or}}}{p_{\text{scav}}} \right) \quad (6)$$

The composition of the gases during blowdown is the same as that in cylinder at the end of the closed cylinder process, which is calculated by the closed cylinder process model.

$$x_7 = x_{\text{bld-out}} = x_6 \quad (7)$$

#### 3.3.2. Scavenging model

In this paper, the newly developed two-zone mean value first principle model of the scavenging process of a two-stroke marine diesel engine is described. According to the novel scavenging model, the cylinder is divided into two zones, namely A zone and B zone (Fig. 6). A zone is close to the exhaust valve and contains only 'pure' exhaust gas that is left from the previous cycle after blowdown, i.e. the initial existing exhaust gas. B zone is close to the inlet ports and contains a perfect mixture of the initially existing exhaust gas and the incoming fresh air. As mentioned previously, neither a perfect displacement model (with B zone containing pure fresh air) nor a perfect mixing model (without A zone) is realistic for long-stroke two-stroke marine diesel engines. So, in order to make it more realistic for predicting the scavenge process of two-stroke engines, the new model combines the perfect displacement model and perfect mixing model (Fig. 6). Two scavenging stages, i.e., stage I and stage II, are distinguished according to the

![Diagram of the two zones of scavenging model for a two-stroke uniflow marine diesel engine. The cylinder is divided into two zones: A Zone (top) containing 'Exhaust gas' and B Zone (bottom) containing a 'Perfect mixture of exhaust gas & fresh air'. Fresh air is shown entering from the bottom. The diagram illustrates the transition between the two zones during the scavenging process.](fb139b01fa81528410fe1d28fbb60486_img.jpg)

Diagram of the two zones of scavenging model for a two-stroke uniflow marine diesel engine. The cylinder is divided into two zones: A Zone (top) containing 'Exhaust gas' and B Zone (bottom) containing a 'Perfect mixture of exhaust gas & fresh air'. Fresh air is shown entering from the bottom. The diagram illustrates the transition between the two zones during the scavenging process.

Fig. 6. Two zones of scavenging model for two-stroke uniflow marine diesel engine.

developments of the two zones. During stage I, B zone grows from an initial size gradually pushing A zone out of the cylinder and A zone disappears at the end of stage I. During stage II, A zone has been removed from the cylinder and only B zone exists in the cylinder. Note that stage II will not occur if the scavenging time is insufficiently long and, in that case, only stage I exists during the scavenging process. The scavenging model is representative for the type of models required in a mean value approach. The main idea is presented below and details can be found in [Appendix A](#).

In the mean value scavenging model, the scavenging time of the whole scavenging process has been made nondimensional as the relative scavenging time  $t_{sc,r}$  by Eq. (8). For details of the relative scavenging time, please refer to [Appendix A.1](#).

$$t_{sc,r} = \frac{\dot{V}_{sc-in}}{i \cdot V} \cdot t_{cycle} = \frac{R_{sc-in} \cdot T_{sc-in} \cdot \dot{m}_{sc-in}}{p \cdot V} \cdot \frac{k}{i \cdot N} \quad (8)$$

where,  $V$  is the volume of the cylinder, which is assumed to be constant during the scavenging process ( $V = V_{10}$ );  $p$  is the pressure in the cylinder;  $\dot{V}_{sc-in}$  and  $\dot{m}_{sc-in}$  are the mean value scavenging air volume and mass flow of the engine;  $T_{sc-in}$  and  $R_{sc-in}$  are the temperature and gas constant of the ingoing scavenging air flow respectively;  $t_{cycle}$  is the time of a full cylinder cycle,  $i$  is the number of the cylinders of the engine;  $N$  is the engine rotational speed and  $k$  is the number of revolutions per cycle (for two-stroke engine  $k = 1$ , and for four-stroke engine  $k = 2$ ).

The size of A zone  $S_A$  is quantified by the ratio of the mass in A zone  $m_A$  to that in the whole cylinder volume  $m$ , i.e.  $S_A = m_A/m$ . The relative scavenging time of stage I  $t_{sc,r,I}$  is determined by the initial size of A zone  $S_A(0)$ , namely  $t_{sc,r,I} = S_A(0)$ . So, the scavenging stage I is indicated by  $t_{sc,r} \le t_{sc,r,I}$  and stage II by  $t_{sc,r} > t_{sc,r,I}$  ([Appendix A.2.4](#)).

According to the mean value scavenging model, the temperature  $T$ , mass  $m$  and composition  $x$  of the gases in the cylinder are calculated by Eqs. (9)–(11) respectively. For details of how these equations are derived, please refer to [Appendix A.2 and A.3](#). Note that the temperature  $T$  and the mass  $m$  in the cylinder have been normalised as the temperature ratio  $y = T/T_{sc-in}$  and the mass ratio  $m/m(0)$  by dividing ingoing scavenging air temperature  $T_{sc-in}$  and the initial mass in the cylinder  $m(0)$  respectively as shown in Eqs. (9) and (10).

$$y \stackrel{\text{def}}{=} \frac{T}{T_{sc-in}} = \begin{cases} \frac{y(0)}{1 + t_{sc,r} \cdot [y(0) - 1]} & t_{sc,r} \le t_{sc,r,I} \\ \frac{y_{II}(0)}{1 + [y_{II}(0) - 1] \cdot [1 - e^{-(t_{sc,r} - t_{sc,r,I})}]} & t_{sc,r} > t_{sc,r,I} \end{cases} \quad (9)$$

$$\frac{m}{m(0)} = \begin{cases} 1 + t_{sc,r} \cdot [y(0) - 1] & t_{sc,r} \le t_{sc,r,I} \\ y(0) \cdot \left\{ 1 - \left[ 1 - \frac{1}{y_{II}(0)} \right] \cdot e^{-(t_{sc,r} - t_{sc,r,I})} \right\} & t_{sc,r} > t_{sc,r,I} \end{cases} \quad (10)$$

$$x = \frac{m_a}{m} = \begin{cases} \frac{[y(0) - x(0)] \cdot t_{sc,r} + x(0)}{1 + t_{sc,r} \cdot [y(0) - 1]} & t_{sc,r} \le t_{sc,r,I} \\ 1 - \frac{[1 - x_{II}(0)] \cdot e^{-(t_{sc,r} - t_{sc,r,I})}}{1 + [y_{II}(0) - 1] \cdot [1 - e^{-(t_{sc,r} - t_{sc,r,I})}]} & t_{sc,r} > t_{sc,r,I} \end{cases} \quad (11)$$

where,  $y(0)$  and  $x(0)$  are the initial temperature ratio and the initial air mass ratio in the cylinder respectively;  $y_{II}(0)$  and  $x_{II}(0)$  are the

initial temperature ratio and the initial air mass ratio of stage II respectively.

The initial size of A zone  $S_A(0)$  has a significant influence on the scavenging process, which is shown in [Fig. 7 to Fig. 9](#). For analysing the influence of the initial size of A zone, the in-cylinder temperature, mass and purity for a case, where  $T_{in} = 50^\circ\text{C}$ ,  $T(0) = 550^\circ\text{C}$  and  $x(0) = 0.2$  has been assumed, are presented in [Figs. 7–9](#). The two-zone scavenging model will go to the limit of a ‘perfect displacement’ model when  $S_A(0)$  is unity and to a ‘perfect mixing’ model when  $S_A(0)$  is zero. During the scavenging process, the in-cylinder temperature will drop faster in stage I than in stage II as shown in [Fig. 7](#). With a higher  $S_A(0)$ , the temperature will drop faster and the final temperature will be lower within a limited scavenging time. In particular, if  $S_A(0) = 1$  (a perfect displacement model) the in-cylinder temperature will drop to the temperature of the ingoing scavenging flow when the relative scavenging time  $t_{sc,r}$  is unity ( $t_{sc}/\tau_{sc} = 1$ ). The in-cylinder mass ([Fig. 8](#)) actually has an inverse trend as that of the temperature because  $m \cdot T$  in the cylinder is constant according to the model. In stage I, both the mass in B zone and mass in the whole cylinder volume increase linearly.

The purity (air mass ratio or air fraction) in cylinder ([Fig. 9](#)) increases from an initial value higher than zero, which in this case is assumed as 0.2, due to the fact that there will be unburnt air in the residual gas from last cycle as a result of air excess. The purity after scavenging process will be higher with a larger  $S_A(0)$  if the scavenging time is sufficiently long.

Even more important for use in a mean value engine model, is the mean value of mass  $m_{sc-out}$ , temperature  $\bar{T}_{sc-out}$  and composition  $\bar{x}_{sc-out}$  flowing into the outlet receiver. These are found to be:

$$\frac{m_{sc-out}}{m(0)} = 1 + y(0) \cdot t_{sc,r} - \frac{m}{m(0)} \quad (12)$$

$$\bar{y}_{sc-out} \stackrel{\text{def}}{=} \frac{\bar{T}_{sc-out}}{T_{sc-in}} = \frac{y(0) \cdot t_{sc,r}}{1 + y(0) \cdot t_{sc,r} - \frac{m}{m(0)}} \quad (13)$$

$$\bar{x}_{sc-out} = \frac{x(0) + y(0) \cdot t_{sc,r} - \frac{m}{m(0)} \cdot x}{1 + y(0) \cdot t_{sc,r} - \frac{m}{m(0)}} \quad (14)$$

For details of how these equations are derived, please refer to [Appendix A.4](#).

![Figure 7: Normalised temperature in cylinder. The graph plots Normalised temperature y = T/T_in (y-axis, 0.8 to 2.6) against Relative scavenging time t_sc,r (x-axis, 0 to 3). Multiple curves are shown for different initial A zone sizes S_A(0) (0, 0.25, 0.50, 0.75, 1.0) for both the B zone (dashed lines) and the whole cylinder volume (solid lines). The curves show a rapid initial drop in temperature followed by a slower decay. Higher S_A(0) values result in lower final temperatures. A red circle marks the 'End of stage I (Start of stage II)' at t_sc,r = 1.0.](90864f8e2844459829af942ef5dc6bc5_img.jpg)

Figure 7: Normalised temperature in cylinder. The graph plots Normalised temperature y = T/T\_in (y-axis, 0.8 to 2.6) against Relative scavenging time t\_sc,r (x-axis, 0 to 3). Multiple curves are shown for different initial A zone sizes S\_A(0) (0, 0.25, 0.50, 0.75, 1.0) for both the B zone (dashed lines) and the whole cylinder volume (solid lines). The curves show a rapid initial drop in temperature followed by a slower decay. Higher S\_A(0) values result in lower final temperatures. A red circle marks the 'End of stage I (Start of stage II)' at t\_sc,r = 1.0.

Fig. 7. Normalised temperature in cylinder.

![Figure 8: Normalised mass in cylinder. The graph plots Normalised mass m/m₀ (0 to 3) against Relative scavenging time t_{sc,r} (=t_{sc}/τ_{sc}) (0 to 3). It shows curves for S_A(0) values of 0, 0.25, 0.50, 0.75, and 1.0 for both the B zone (dashed lines) and the whole cylinder volume (solid lines). Red circles mark the 'End of stage I (Start of stage II)' at t_{sc,r} ≈ 1.0. The curves show that mass increases with scavenging time, reaching a plateau around 2.5-2.6.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 8: Normalised mass in cylinder. The graph plots Normalised mass m/m₀ (0 to 3) against Relative scavenging time t\_{sc,r} (=t\_{sc}/τ\_{sc}) (0 to 3). It shows curves for S\_A(0) values of 0, 0.25, 0.50, 0.75, and 1.0 for both the B zone (dashed lines) and the whole cylinder volume (solid lines). Red circles mark the 'End of stage I (Start of stage II)' at t\_{sc,r} ≈ 1.0. The curves show that mass increases with scavenging time, reaching a plateau around 2.5-2.6.

Fig. 8. Normalised mass in cylinder.

![Figure 9: Air mass ratio (purity) in cylinder. The graph plots Air mass ratio x = m_a/m_g (0 to 1) against Relative scavenging time t_{sc,r} (=t_{sc}/τ_{sc}) (0 to 3). It shows curves for S_A(0) values of 0, 0.25, 0.50, 0.75, and 1.0 for both the B zone (dashed lines) and the whole cylinder volume (solid lines). Red circles mark the 'End of stage I (Start of stage II)' at t_{sc,r} ≈ 1.0. The curves show that air mass ratio increases with scavenging time, reaching a plateau around 0.95-1.0.](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 9: Air mass ratio (purity) in cylinder. The graph plots Air mass ratio x = m\_a/m\_g (0 to 1) against Relative scavenging time t\_{sc,r} (=t\_{sc}/τ\_{sc}) (0 to 3). It shows curves for S\_A(0) values of 0, 0.25, 0.50, 0.75, and 1.0 for both the B zone (dashed lines) and the whole cylinder volume (solid lines). Red circles mark the 'End of stage I (Start of stage II)' at t\_{sc,r} ≈ 1.0. The curves show that air mass ratio increases with scavenging time, reaching a plateau around 0.95-1.0.

Fig. 9. Air mass ratio (purity) in cylinder.

#### 3.3.3. Expelling process model

During the expelling process the inlet ports are closed while the exhaust valves are still open and the upward moving piston expels gases out of the cylinder. For modern engines this is a large amount since the exhaust valve is closed very late. It is assumed that during the expelling process the gas state in the cylinder is homogeneous and the in-cylinder condition and composition remain the same as the trapped in-cylinder condition and composition after the scavenging process, although the cylinder volume and mass is decreasing due to the upward moving piston. So, the trapped in-cylinder condition after the expelling process, which is the starting condition of the closed-cylinder process, is the same as the trapped in-cylinder condition after the scavenging process, however with a smaller volume and mass. The mass of the gases expelled from the cylinder and entering the outlet receiver is calculated by Eq. (15), and the composition and temperature are calculated by Eqs. (16) and (17) respectively. The trapped mass after scavenging process  $m_{sc-tr}$  is calculated by the scavenging model, i.e., Eq. (10). The trapped mass after the gas exchange process  $m_1$  is calculated by Eq. (18).

$$m_{exp} = m_{sc-tr} - m_1 \quad (15)$$

$$x_{exp} = x_1 = x_{sc-tr} \quad (16)$$

$$T_{exp} = T_1 = T_{sc-tr} \text{ and also } p_{exp} = p_1 = p_{sc-tr} \quad (17)$$

$$m_1 = \frac{p_1 \cdot V_1}{R_1 \cdot T_1} \quad (18)$$

Finally, the slip factor  $s$  of the gas exchange process is defined as the total mass of the fresh air flowing through the cylinder volume  $m_{slip}$  divided by the fresh air mass trapped in the cylinder volume at the end of the gas exchange process  $m_{fresh}$  (Stapersma, 2010a) as shown in Eq. (19). The slip factor of the two-stroke diesel engine can be calculated using Eq. (20).

$$s \stackrel{\text{def}}{=} \frac{m_{slip}}{m_{fresh}} \quad (19)$$

$$s = \frac{V_{IC}}{V_{EC}} \cdot \frac{1 - x(0)}{x - x(0)} \cdot y \cdot t_{sc,r} - 1 \quad (20)$$

where,  $V_{IC}$  and  $V_{EC}$  are the cylinder volumes at IC (Inlet ports close) and EC (Exhaust valve close) respectively. Note that, during scavenging process, fresh air slip can only occur in the two-zone scavenging model if the scavenging time is sufficient to reach stage II.

## 4. Model calibration, verification and validation

The ship propulsion system model of the benchmark chemical tanker introduced in (Sui et al., 2019, 2020) has been adopted in this paper. The models of ship resistance, propeller open water characteristics, wake factor, thrust deduction factor and relative rotative efficiency have been calibrated in (Sui et al., 2019). Therefore, only the engine model calibration will be presented in this paper. Despite the asymmetry in model calibration, both models, i.e. the engine model and the ship propulsion system model, are validated in this section. Considering the fact that detailed measurement information of ship and engine in actual operations is missing, it should be noted that validation efforts in this research are restricted to the available measurement information. The latter is another reason why this research applies Mean Value First Principle Parametric (MVFPP) models. The number of parameters that need to be calibrated in such models is typically smaller than in more detailed models and require less detailed measurement information in the first place. Finally, it should be noted that both models are also verified, in this section and the next, meaning that general trends in the simulation results are reviewed against expected and generally known behaviour of engines and ship propulsion systems. The applied model verification and validation philosophy is based on (Thacker et al., 2004).

### 4.1. Engine model calibration, verification and validation

The mean value model of the two-stroke marine diesel engine MANGS35ME-B9.3 (4170 kW @ 167 rpm) is calibrated and validated before it is integrated into the ship propulsion system model, using the engine test data provided by the engine manufacturer. Some of parameters calibrating the engine model at nominal operating point are shown in Table 4. Note that, only calibration in nominal operating point is required to calibrate the MVFPP model, while the parameters of off-design points will be determined by the model.

The engine model is validated by comparing the simulation

results with the engine test data of the mass flows, Buchi pressures and temperatures, turbocharger speed, in-cylinder compression and maximum pressures and the specific fuel consumption as shown in Fig. 10 to Fig. 15. The engine performance has been measured at different loads (100%, 90%, 75%, 50% and 10%) while keeping the engine rotational speed constant at nominal speed (167 rpm). The simulation results are generated by running the engine model (quasi-)statically with decreasing engine load (from 100% to 10% of nominal power) along the generator law (constant engine rotational speed at 167 rpm). Thus, only (quasi-)static simulation results of the engine model along the generator law have been validated and the simulation results have shown a good consistency with the engine test data. Although the simulation results along the propeller law have not been validated due to the lack of test data of the same engine, the results have been checked and verified with the test data of another engine from the same engine family, which has the same nominal rotational speed but a higher nominal power. Note that, the 'sharp changes' in the simulation results occurring at around 35% of nominal engine power, as shown in Figs. 10–15, are caused by the operation of the auxiliary blower.

When reducing the engine load, the fuel mass flow injected into the engine cylinders for combustion will decrease (Fig. 10), and consequently the energy in the exhaust gas flowing out of the cylinders into the outlet receiver also decreases. As a result, the temperature and pressure in the outlet receiver before the turbine decreases (Fig. 11 and Fig. 12). The turbocharger rotational speed will drop (Fig. 13) due to the lower enthalpy of the exhaust flow into the turbine. The compressor that is driven by the turbine has less power to charge the air, so, the temperature and pressure after the compressor as well as the charging air mass flow will decrease (Figs. 10, Figs. 11 and 12). The in-cylinder compression pressure and the maximum combustion pressure are also dropping with the decreasing engine load (Fig. 14). The engine specific fuel consumption will, however, first decrease and then increase sharply at low loads and reaches the lowest at around 70% nominal power (Fig. 15). Note that, the temperature after turbine will first decrease slightly and then increase at low loads before the blower starts operating (Fig. 11), and that is caused by the dropping turbine efficiency at low engine loads. The auxiliary blower operating at low engine loads helps to boost the air charging when the turbocharger is not able to provide sufficient air to the engine. As a result, the air and exhaust mass flows increase sharply, while the temperatures in the outlet receiver and after the turbine will drop.

According to the above, the engine model is considered to be verified, i.e. the model simulates engine behaviour to an acceptable degree. Furthermore, Figs. 10–15 show that simulation results are close to the available measurement data and the model is thus also considered to be validated to a certain extent. Note that it is impossible to calibrate the model such that all simulation results exactly match the available measurement data. With more detailed models, i.e. even higher fidelity models, this would perhaps be

![Figure 10: Mass flows. A line graph showing mass flows (kg/s) versus Engine power (%). The y-axis ranges from 0 to 9 kg/s, and the x-axis ranges from 0 to 110%. Four data series are plotted: m_air (Simulation) and m_air (Measured) in blue; m_exh (Simulation) and m_exh (Measured) in red; m_fuel (Simulation) and m_fuel (Measured) in black. The m_fuel series is nearly flat at 0 kg/s. The m_air and m_exh series show a sharp increase in mass flow as engine power increases, with a notable jump around 35% engine power.](8ee3b76dd49f31624d287885bc2c81ee_img.jpg)

Figure 10: Mass flows. A line graph showing mass flows (kg/s) versus Engine power (%). The y-axis ranges from 0 to 9 kg/s, and the x-axis ranges from 0 to 110%. Four data series are plotted: m\_air (Simulation) and m\_air (Measured) in blue; m\_exh (Simulation) and m\_exh (Measured) in red; m\_fuel (Simulation) and m\_fuel (Measured) in black. The m\_fuel series is nearly flat at 0 kg/s. The m\_air and m\_exh series show a sharp increase in mass flow as engine power increases, with a notable jump around 35% engine power.

Fig. 10. Mass flows.

![Figure 11: Buchi temperatures. A line graph showing temperatures (K) versus Engine power (%). The y-axis ranges from 250 to 800 K, and the x-axis ranges from 0 to 110%. Six data series are plotted: T_ir (Simulation) and T_ir (Measured) in blue; T_or (Simulation) and T_or (Measured) in red; T_com (Simulation) and T_com (Measured) in cyan; T_tur (Simulation) and T_tur (Measured) in magenta. T_ir is constant at ~300 K. T_or increases from ~520 K to ~690 K. T_com increases from ~300 K to ~460 K. T_tur is relatively flat around 520 K.](7c2f0efb2c5d10a52ce19ba33d9d3cec_img.jpg)

Figure 11: Buchi temperatures. A line graph showing temperatures (K) versus Engine power (%). The y-axis ranges from 250 to 800 K, and the x-axis ranges from 0 to 110%. Six data series are plotted: T\_ir (Simulation) and T\_ir (Measured) in blue; T\_or (Simulation) and T\_or (Measured) in red; T\_com (Simulation) and T\_com (Measured) in cyan; T\_tur (Simulation) and T\_tur (Measured) in magenta. T\_ir is constant at ~300 K. T\_or increases from ~520 K to ~690 K. T\_com increases from ~300 K to ~460 K. T\_tur is relatively flat around 520 K.

Fig. 11. Buchi temperatures.

possible, if all parameters are carefully calibrated. However, the cost of additional calibration efforts and significantly increased computational times are reasons to not pursue this path. Moreover, the engine model will be utilised in a larger simulation environment (including the ship propulsion) to simulate large time periods, i.e. multiple hours or even days (not in this paper, but in other parts of the research). A model that has acceptable predictive capabilities while being fast at the same time, is therefore preferred.

Table 4

Selected calibration parameters of the engine model (nominal engine operating point).

| Parameters in closed cylinder process model |        | Parameters in gas exchange process model |        | Parameters in turbocharger and air cooler model |        |
|---------------------------------------------|--------|------------------------------------------|--------|-------------------------------------------------|--------|
| $r_c$ [-]                                   | 16.842 | $S_A(0)$ [-]                             | 0.8237 | $\pi_{com}$ [-]                                 | 3.8640 |
| $n_{comp}$ [-]                              | 1.321  | $y(0)$ [-]                               | 2.6110 | $\pi_{tur}$ [-]                                 | 3.4960 |
| $a$ [-]                                     | 1.169  | $x(0)$ [-]                               | 0.4642 | $\eta_{TC}$ [-]                                 | 0.6278 |
| $b$ [-]                                     | 1.609  | $s$ [-]                                  | 0.4263 | $\tau_{TC}$ [-]                                 | 2.3969 |
| $c$ [-]                                     | 2.927  | $t_{scr}$ [-]                            | 0.7971 | $a_{TC}$ [-]                                    | 0.7    |
| $r_e$ [-]                                   | 4.195  |                                          |        | $b_{TC}$ [-]                                    | 0.5    |
| $n_{exp}$ [-]                               | 1.330  |                                          |        | $\epsilon_{TC}$ [-]                             | 0.9569 |




![Figure 12: Buchi pressures. A line graph showing Buchi pressures (p_ir, p_or, p_iv, p_svy) in bar versus Engine power in percent. The y-axis ranges from 0.5 to 4.0 bar. The x-axis ranges from 0 to 110 percent. Simulation results are shown as solid lines (blue for p_ir, red for p_or, cyan for p_iv, magenta for p_svy). Measured results are shown as markers (blue circles for p_ir, red circles for p_or, cyan circles for p_iv, magenta circles for p_svy).](10c82dcc5f2c237961329dd29d65859c_img.jpg)

| Engine power [%] | $p_{ir}$ (Simulation) [bar] | $p_{or}$ (Simulation) [bar] | $p_{iv}$ (Simulation) [bar] | $p_{svy}$ (Simulation) [bar] | $p_{ir}$ (Measured) [bar] | $p_{or}$ (Measured) [bar] | $p_{iv}$ (Measured) [bar] | $p_{svy}$ (Measured) [bar] |
|------------------|-----------------------------|-----------------------------|-----------------------------|------------------------------|---------------------------|---------------------------|---------------------------|----------------------------|
| 10               | 1.2                         | 1.2                         | 1.0                         | 1.0                          | -                         | -                         | -                         | -                          |
| 20               | 1.4                         | 1.4                         | 1.0                         | 1.0                          | 1.5                       | 1.4                       | 1.0                       | 1.0                        |
| 30               | 1.7                         | 1.6                         | 1.0                         | 1.0                          | 1.7                       | 1.6                       | 1.0                       | 1.0                        |
| 40               | 2.0                         | 1.8                         | 1.0                         | 1.0                          | 2.0                       | 1.8                       | 1.0                       | 1.0                        |
| 50               | 2.3                         | 2.0                         | 1.0                         | 1.0                          | 2.3                       | 2.0                       | 1.0                       | 1.0                        |
| 60               | 2.6                         | 2.3                         | 1.0                         | 1.0                          | -                         | -                         | 1.0                       | 1.0                        |
| 70               | 3.0                         | 2.7                         | 1.0                         | 1.0                          | 3.0                       | 2.7                       | 1.0                       | 1.0                        |
| 80               | 3.3                         | 3.0                         | 1.0                         | 1.0                          | 3.3                       | 3.0                       | 1.0                       | 1.0                        |
| 90               | 3.6                         | 3.4                         | 1.0                         | 1.0                          | 3.6                       | 3.4                       | 1.0                       | 1.0                        |
| 100              | 3.9                         | 3.7                         | 1.0                         | 1.0                          | 3.9                       | 3.7                       | 1.0                       | 1.0                        |

Figure 12: Buchi pressures. A line graph showing Buchi pressures (p\_ir, p\_or, p\_iv, p\_svy) in bar versus Engine power in percent. The y-axis ranges from 0.5 to 4.0 bar. The x-axis ranges from 0 to 110 percent. Simulation results are shown as solid lines (blue for p\_ir, red for p\_or, cyan for p\_iv, magenta for p\_svy). Measured results are shown as markers (blue circles for p\_ir, red circles for p\_or, cyan circles for p\_iv, magenta circles for p\_svy).

Fig. 12. Buchi pressures.

![Figure 15: Specific fuel consumption (sfc). A line graph showing sfc in g/kWh versus Engine power in percent. The y-axis ranges from 170 to 200 g/kWh. The x-axis ranges from 0 to 110 percent. Simulation results are shown as a solid blue line. Measured results are shown as blue circles.](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

| Engine power [%] | $sfc$ (Simulation) [g/kWh] | $sfc$ (Measured) [g/kWh] |
|------------------|----------------------------|--------------------------|
| 10               | 200                        | -                        |
| 20               | 182                        | 181                      |
| 30               | 178                        | -                        |
| 40               | 177                        | -                        |
| 50               | 176                        | 176                      |
| 60               | 175.5                      | -                        |
| 70               | 175                        | 174                      |
| 80               | 175                        | -                        |
| 90               | 176                        | 176                      |
| 100              | 177                        | 177                      |

Figure 15: Specific fuel consumption (sfc). A line graph showing sfc in g/kWh versus Engine power in percent. The y-axis ranges from 170 to 200 g/kWh. The x-axis ranges from 0 to 110 percent. Simulation results are shown as a solid blue line. Measured results are shown as blue circles.

Fig. 15. Specific fuel consumption.

![Figure 13: Turbocharger rotational speed (TC speed). A line graph showing TC speed in rpm (scaled by 10^4) versus Engine power in percent. The y-axis ranges from 0 to 2.5 x 10^4 rpm. The x-axis ranges from 0 to 110 percent. Simulation results are shown as a solid blue line. Measured results are shown as blue circles.](b712e7522f1bb7135730c7d1abb46d43_img.jpg)

| Engine power [%] | $TC\ speed$ (Simulation) [ $\times 10^4$ rpm] | $TC\ speed$ (Measured) [ $\times 10^4$ rpm] |
|------------------|-----------------------------------------------|---------------------------------------------|
| 10               | 0.7                                           | -                                           |
| 20               | 1.0                                           | 1.0                                         |
| 30               | 1.2                                           | -                                           |
| 40               | 1.3                                           | -                                           |
| 50               | 1.5                                           | -                                           |
| 60               | 1.6                                           | -                                           |
| 70               | 1.8                                           | 1.8                                         |
| 80               | 1.9                                           | -                                           |
| 90               | 2.0                                           | -                                           |
| 100              | 2.1                                           | 2.1                                         |

Figure 13: Turbocharger rotational speed (TC speed). A line graph showing TC speed in rpm (scaled by 10^4) versus Engine power in percent. The y-axis ranges from 0 to 2.5 x 10^4 rpm. The x-axis ranges from 0 to 110 percent. Simulation results are shown as a solid blue line. Measured results are shown as blue circles.

Fig. 13. Turbocharger rotational speed.

![Figure 14: In-cylinder pressures. A line graph showing in-cylinder pressures (p_comp, p_max) in bar versus Engine power in percent. The y-axis ranges from 0 to 220 bar. The x-axis ranges from 0 to 110 percent. Simulation results are shown as solid lines (blue for p_comp, red for p_max). Measured results are shown as markers (blue circles for p_comp, red circles for p_max).](0ac183e926716c7de215c87c38e61dbc_img.jpg)

| Engine power [%] | $p_{comp}$ (Simulation) [bar] | $p_{max}$ (Simulation) [bar] | $p_{comp}$ (Measured) [bar] | $p_{max}$ (Measured) [bar] |
|------------------|-------------------------------|------------------------------|-----------------------------|----------------------------|
| 10               | 50                            | 70                           | -                           | -                          |
| 20               | 65                            | 90                           | 70                          | 110                        |
| 30               | 75                            | 105                          | -                           | -                          |
| 40               | 85                            | 120                          | -                           | -                          |
| 50               | 100                           | 140                          | 100                         | 140                        |
| 60               | 110                           | 155                          | -                           | -                          |
| 70               | 120                           | 165                          | -                           | -                          |
| 80               | 130                           | 175                          | 130                         | 170                        |
| 90               | 145                           | 185                          | 145                         | 185                        |
| 100              | 160                           | 190                          | 160                         | 190                        |

Figure 14: In-cylinder pressures. A line graph showing in-cylinder pressures (p\_comp, p\_max) in bar versus Engine power in percent. The y-axis ranges from 0 to 220 bar. The x-axis ranges from 0 to 110 percent. Simulation results are shown as solid lines (blue for p\_comp, red for p\_max). Measured results are shown as markers (blue circles for p\_comp, red circles for p\_max).

Fig. 14. In-cylinder pressures.

## 4.2. Ship resistance and propulsion model verification and validation

As discussed in section 2.2, the ship resistance and propulsion model is not explained in detail in this paper. Still, a few remarks about updates of the models introduced in (Sui et al., 2019) and (Sui et al., 2020) are necessary. The propeller model used in (Sui et al., 2019) has been updated from considering only the first quadrant of the propeller open water diagram to taking the four quadrants open water characteristics into account. The four quadrants open water diagram is required when investigating the whole field of operation for the propeller during ship manoeuvring, including running astern and dynamic behaviour such as stopping and acceleration (Carlton, 2019; Klein Woud and Stapersma, 2002). To update the propeller model, the original MAN Alpha propeller that is actually installed on the chemical tanker has been replaced by a Wageningen C-series Controllable Pitch Propeller (CPP) (Dang et al., 2013), which is developed by MARIN (the Maritime Research Institute Netherlands). The Wageningen C-series CPP comprises 4- and 5-bladed propellers with blade area ratios of 0.40, 0.55, 0.60, 0.70 and 0.75. The 4-bladed C-series propellers including C4-40, C4-55 and C4-70 have four quadrants open water diagrams for nominal pitches of  $P/D = 0.8, 1.0, 1.2$  and  $1.4$ . The C4-55 propeller with nominal pitch of  $P/D = 0.8$  has been selected for modelling the propeller of the chemical tanker, as it has a blade area ratio (0.55) and design pitch (0.8) close to those of the MAN Alpha propeller installed in the benchmark ship (blade area ratio = 0.52 and  $P/D = 0.71$ ). However, to model the propeller of the benchmark ship using the data of C4-55, the open water characteristics of the chosen C4-55 propeller need to be slightly corrected to reduce the differences between the two different propellers as much as possible. Unfortunately, only data of the open water diagram at design pitch in the first quadrant is available for the MAN Alpha propeller. Thus, the four quadrant characteristics of the C4-55 propeller has been corrected based on the first quadrant open water diagram of the original MAN Alpha propeller at design pitch ( $P/D = 0.71$ ).

The ship resistance and propulsion model has subsequently been verified and validated using the sea trial measurement data and the ship model test data as shown in Fig. 16. Note that the simulation results are generated by running the ship propulsion model under constant propeller pitch control mode (Sui et al., 2019, 2020), where the propeller pitch is kept constant (at design pitch  $P/D = 0.71$ ).

$D = 0.71$ ) until the engine revolution reaches the minimum rotational speed limit (81.83 rpm, 49% of the engine nominal rotational speed) that is set in the combinator curve. The simulation results show that the ship velocity and shaft power (Fig. 16(b)) will increase at constant shaft revolutions when the ship sails slowly. A good consistency between the propulsion simulation results and the ship propulsion model test results as well as the sea trial test data is shown in Fig. 16, while general trends in the simulation results are as expected. For example, an approximately cubic power relationship can be noticed between ship speed and shaft or ship effective towing power. Furthermore, an almost linear relationship can be noticed between propeller rotational speed (shaft speed) and ship velocity for the part of the combinator curve where propeller pitch is kept constant. The main reason that these relationships are not exactly cubic and linear is because the ship resistance is modelled quite accurately with variable specific resistance values, see (Sui et al., 2019), rather than a simple square relationship between ship resistance and ship speed. The latter would have resulted in the traditional propeller law when combined with low-fidelity assumptions with regards to propeller-hull interaction coefficients and constant pitch operation of the CPP.

# 5. Results and discussion

## 5.1. Engine stationary behaviour and operational limits

Based on the MVFPP engine model, static operating points covering the entire engine envelope (Fig. 17) specified by the engine manufacturer (MAN, 2014a, 2018) have been simulated to investigate the engine stationary behaviour. In particular the engine mechanical loading, thermal loading and compressor surge across the whole engine operating envelope will be investigated. In the engine model the fuel rack limiter is switched off, so that the engine can also run outside the envelope to reveal both the causes and consequences of engine overloading. It can also provide an insight on how the engine operating limits are specified. For these purposes, the contour plots of the indicators of the engine mechanical loading, thermal loading and compressor surge across the entire engine operating envelope have been presented in Fig. 18 to Fig. 28.

![Figure 17: Simulated (stationary) operating points across the engine envelope. The graph plots Engine power [kW] on the y-axis (0 to 5000) against Engine speed [rpm] on the x-axis (60 to 180). It shows a dense field of simulated operating points (blue dots). Key boundaries are indicated: a green solid line for 'Load limit', a red solid line for 'Overload limit', and a black dashed line for '100% mep'. A red circle marks the MCR [4170kW@167rpm].](dd330f8b8f6c16eae20c3a676b4eb804_img.jpg)

Figure 17: Simulated (stationary) operating points across the engine envelope. The graph plots Engine power [kW] on the y-axis (0 to 5000) against Engine speed [rpm] on the x-axis (60 to 180). It shows a dense field of simulated operating points (blue dots). Key boundaries are indicated: a green solid line for 'Load limit', a red solid line for 'Overload limit', and a black dashed line for '100% mep'. A red circle marks the MCR [4170kW@167rpm].

Fig. 17. Simulated (stationary) operating points across the engine envelope.

### 5.1.1. Engine mechanical loading

The engine torque (or the mean effective pressure, mep) and the maximum in-cylinder pressure have been selected as the indicators of the engine mechanical loading. The engine torque is almost proportional to the injected fuel per cycle that is proportionally determined by the fuel rack position (Fig. 18), which is controlled by the engine governor. According to the simulation results, the highest maximum in-cylinder pressure happens in high engine speed area (Fig. 19) and the maximum in-cylinder pressure will drop when the engine speed and engine torque decrease. So, the engine mechanical overloading is not the limiting factor of the engine torque and power when operating (statically) in low speed and/or low power area, where the engine thermal overloading is the real limiting factor as will be shown in the next section.

### 5.1.2. Engine thermal loading

The air excess ratio  $\lambda$ , inlet receiver pressure  $p_{IR}$ , maximum in-cylinder temperature  $T_{max}$ , in-cylinder temperature just before opening of the exhaust valve (EO)  $T_{EO}$ , exhaust valve temperature

![Figure 16: Ship propulsion validation results. (a) Ship effective power & shaft power vs Ship velocity. The top plot shows Ship effective power [kW] (0 to 4000) vs Ship velocity [kn] (0 to 16). The bottom plot shows Shaft power [kW] (0 to 6000) vs Ship velocity [kn] (0 to 16). Both plots compare Simulation (blue solid line), Model test prediction (red dashed line with open circles), and Sea trial measurement (black solid line with filled circles). (b) Ship Velocity & shaft power vs shaft speed. The top plot shows Ship velocity [kn] (0 to 15) vs Shaft Speed [rpm] (80 to 200). The bottom plot shows Shaft power [kW] (0 to 6000) vs Shaft Speed [rpm] (80 to 200). Both plots compare Simulation (blue solid line), Model test prediction (red dashed line with open circles), and Sea trial measurement (black solid line with filled circles).](d7346a28f4ba53888f72648cface9da9_img.jpg)

Figure 16: Ship propulsion validation results. (a) Ship effective power & shaft power vs Ship velocity. The top plot shows Ship effective power [kW] (0 to 4000) vs Ship velocity [kn] (0 to 16). The bottom plot shows Shaft power [kW] (0 to 6000) vs Ship velocity [kn] (0 to 16). Both plots compare Simulation (blue solid line), Model test prediction (red dashed line with open circles), and Sea trial measurement (black solid line with filled circles). (b) Ship Velocity & shaft power vs shaft speed. The top plot shows Ship velocity [kn] (0 to 15) vs Shaft Speed [rpm] (80 to 200). The bottom plot shows Shaft power [kW] (0 to 6000) vs Shaft Speed [rpm] (80 to 200). Both plots compare Simulation (blue solid line), Model test prediction (red dashed line with open circles), and Sea trial measurement (black solid line with filled circles).

Fig. 16. Ship propulsion validation results.

![](b05a8a3551db31147979064952179990_img.jpg)

![Figure 22: Maximum in-cylinder temperature T_max (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T_max [K] are shown in yellow and blue, ranging from 1300 to 1900K. The contours are highest near the MCR point.](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 22: Maximum in-cylinder temperature T\_max (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T\_max [K] are shown in yellow and blue, ranging from 1300 to 1900K. The contours are highest near the MCR point.

Fig. 22. Maximum in-cylinder temperature  $T_{max}$  (Stationary behaviour).![Figure 23: In-cylinder temperature just before EO T_EO (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T_EO [K] are shown in yellow and blue, ranging from 600 to 1400K. The contours are highest near the MCR point.](411fa16c3211377525ba37c57784fee0_img.jpg)

Figure 23: In-cylinder temperature just before EO T\_EO (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T\_EO [K] are shown in yellow and blue, ranging from 600 to 1400K. The contours are highest near the MCR point.

Fig. 23. In-cylinder temperature just before EO  $T_{EO}$  (Stationary behaviour).![Figure 24: Exhaust valve temperature T_EV (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T_EV [K] are shown in yellow and blue, ranging from 500 to 820K. The contours are highest near the MCR point.](fd188843e5acb8e0d76372860b5f5962_img.jpg)

Figure 24: Exhaust valve temperature T\_EV (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T\_EV [K] are shown in yellow and blue, ranging from 500 to 820K. The contours are highest near the MCR point.

Fig. 24. Exhaust valve temperature  $T_{EV}$  (Stationary behaviour).

manufacturers limit in the static performance diagram. It equates the turbine inlet temperature, which in this case according to manufacturer specification has a limit for continuous operation of 923 K. The slip factor is the highest when the engine runs in the operating area where the air excess ratio is the lowest, and the possible highest exhaust valve temperature and outlet receiver temperature have been cooled down due to the high slip factor in that area. As a result, the highest exhaust valve temperature and outlet receiver temperature happen in the area that is close to MCR. Due to the influence of the turbine pressure ratio and turbine efficiency, the trend of the temperature after turbine (Fig. 26) is different from that of the temperature before the turbine (the outlet receiver temperature). When the engine power drops, the temperature after turbine will first slightly drop and then go up until the auxiliary blower starts operating.

It may be concluded that for an indicator of 2-stroke engine static thermal loading it is wiser to consider the in-cylinder temperatures, particularly the one just before EO, rather than e.g. the exhaust valve temperature for this model.

### 5.1.3. Compressor surge

The engine operations could also be limited by the compressor surge, especially for four-stroke diesel engines operating along the propeller law (constant propeller pitch) (Stapersma, 2010b). However, for the two-stroke marine diesel engine for which the air swallow characteristic is independent of engine speed the situation is less severe. For the engine investigated in this paper, the compressor surge index is negative across the entire engine operating envelope (Fig. 28) indicating that in static operations the compressor will not surge. The constant surge index lines are almost parallel to the constant power lines and the surge index decreases (the compressor operating point gets closer to the surge line) when the engine power reduces until the auxiliary blower starts operating. It indicates that the compressor surge is influenced almost equally by the engine torque and the engine speed, and the operation of the auxiliary blower helps to prevent the compressor from surging when the engine is running at low engine speed and/or torque. Without the auxiliary blower, the engine will surge when operating below certain power and the surge limit line locates somewhere below the 'separating lines' and is parallel with the constant surge index lines.

![Figure 25: Outlet receiver temperature T_OR (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T_OR [K] are shown in yellow and blue, ranging from 500 to 700K. The contours are highest near the MCR point.](8e4f8c87efc168cac52580ce81583063_img.jpg)

Figure 25: Outlet receiver temperature T\_OR (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several performance curves: Load limit (solid green), Overload limit (solid red), 100% mep (dashed black), and MCR (red dot at 4170kW@167rpm). Contour lines for T\_OR [K] are shown in yellow and blue, ranging from 500 to 700K. The contours are highest near the MCR point.

Fig. 25. Outlet receiver temperature  $T_{OR}$  (Stationary behaviour).

![Figure 26: Temperature after turbine T_TUR (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several curves: a green solid line for 'Load limit', a red solid line for 'Overload limit', a black dashed line for '100% mep', and a red dot for 'MCR [4170kW@167rpm]'. A legend indicates that the yellow and blue lines represent T_TUR [K] for different engine speeds. The curves show that temperature increases with engine speed and power, with the overload limit being the highest.](177e8bc1c595b7fe3461d9919f87e044_img.jpg)

Figure 26: Temperature after turbine T\_TUR (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows several curves: a green solid line for 'Load limit', a red solid line for 'Overload limit', a black dashed line for '100% mep', and a red dot for 'MCR [4170kW@167rpm]'. A legend indicates that the yellow and blue lines represent T\_TUR [K] for different engine speeds. The curves show that temperature increases with engine speed and power, with the overload limit being the highest.

Fig. 26. Temperature after turbine  $T_{TUR}$  (Stationary behaviour).

![Figure 27: Slip factor s (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows the same engine limits as Fig. 26. The slip factor is represented by blue curves labeled with values: 2.2, 1.8, 1.6, 1.4, 1.2, 1.1, 1.0, 0.9, 0.8, 0.7, 0.6, 0.5, 0.427, and 0.45. The slip factor generally decreases as engine speed and power increase.](fe753d01ad5fe6cf150018c958173c6d_img.jpg)

Figure 27: Slip factor s (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows the same engine limits as Fig. 26. The slip factor is represented by blue curves labeled with values: 2.2, 1.8, 1.6, 1.4, 1.2, 1.1, 1.0, 0.9, 0.8, 0.7, 0.6, 0.5, 0.427, and 0.45. The slip factor generally decreases as engine speed and power increase.

Fig. 27. Slip factor  $s$  (Stationary behaviour).

![Figure 28: Compressor surge index (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows the same engine limits as Fig. 26. The compressor surge index is represented by yellow curves labeled with values: -0.05, -0.085, -0.1, -0.12, -0.15, -0.18, -0.2, -0.25, -0.27, -0.0707, -0.075, -0.085, -0.09, -0.0979, -0.1, -0.12, -0.15, -0.18, -0.2, -0.25, -0.27, -0.0707, -0.075, -0.085, -0.09, -0.0979, -0.1, -0.12, -0.15, -0.18, -0.2, -0.25, -0.27. The surge index generally decreases as engine speed and power increase.](239211fa511b4ffa685b54b5132ec927_img.jpg)

Figure 28: Compressor surge index (Stationary behaviour). The graph plots Engine power [kW] on the y-axis (0 to 4500) against Engine speed [rpm] on the x-axis (60 to 180). It shows the same engine limits as Fig. 26. The compressor surge index is represented by yellow curves labeled with values: -0.05, -0.085, -0.1, -0.12, -0.15, -0.18, -0.2, -0.25, -0.27, -0.0707, -0.075, -0.085, -0.09, -0.0979, -0.1, -0.12, -0.15, -0.18, -0.2, -0.25, -0.27, -0.0707, -0.075, -0.085, -0.09, -0.0979, -0.1, -0.12, -0.15, -0.18, -0.2, -0.25, -0.27. The surge index generally decreases as engine speed and power increase.

Fig. 28. Compressor surge index (Stationary behaviour).

## 5.2. Engine dynamic behaviour during different ship operations

The dynamic engine behaviour during ship acceleration, deceleration and crash stop have been investigated based on the integrated ship propulsion model. The ship operations are implemented by changing the engine (propeller) and propeller pitch setting. These two control inputs are controlled by a single lever command (SLC) using the pre-defined combinator curve (Sui et al., 2019, 2020), and the SLC has a range from  $-100$  (full astern) to  $100$  (full ahead). In the simulations of the above-mentioned ship operations, the actual sea condition is set as normal, i.e., with 15% sea margin, and the shaft generator (PTO) is switched on. The PTO power is set as constant at 350 kW.

### 5.2.1. Ship acceleration

In the simulations of ship acceleration and deceleration, the constant pitch propulsion control mode has been applied. The propeller pitch (angle) is set at  $16.6^\circ$ , which is 93% of the design pitch ( $17.83^\circ$  or equivalently  $P/D = 0.7075$ ), and the ship acceleration and deceleration are implemented by changing the propeller revolution through SLC.

To accelerate the ship, the SLC command is increased from 60 to 90 and the corresponding propeller revolution is increased from 100 rpm to 150 rpm (Fig. 29(a)). The ship speed will be consequently increased from 8.1 knots to 12 knots finally. The engine brake performance including the engine speed, torque, power and fuel rack behaviour during the ship acceleration is shown in Fig. 29(b). The engine power trajectory during ship acceleration is inside the engine operating envelope during the dynamic process. The dynamic behaviour of the engine thermal loading during ship acceleration are compared with the corresponding static results (Fig. 29(c)), which are read (interpolated) directly from the static engine performance maps (Figs. 20–28) according to the engine power trajectory.

From the comparison, obvious differences between the dynamic and static results are observed especially during the transient process, while they coincide with each other when the process becomes steady. During the transient process of ship acceleration, the air excess ratio drops from 2 to the lowest 1.7 and exceeds the air excess ratio limit assumed in the model, which is 1.7. The dynamic value of the air excess ratio is much lower than the static value read from the static map (Fig. 20). Thus, there is a real chance of black smoke development during this acceleration manoeuvre, which may also cause engine fouling obviously. The maximum in-cylinder temperature  $T_{max}$  and in-cylinder temperature just before EO  $T_{EO}$ , exhaust valve temperature  $T_{EV}$ , outlet receiver temperature  $T_{OR}$  and temperature after turbine  $T_{TUR}$  will all first increase to the highest values during the transient process before dropping to the steady (static) values. The dynamic increases of the temperatures are higher than the static values. For instance, the in-cylinder EO temperature  $T_{EO}$ , is higher than the static value by 82 K.  $T_{EO}$  reaches as high as 1072 K and it exceeds according to Fig. 23 the static thermal load limit of the engine, which, according to the previous section, was 1050 K and coincided with the load limit in the static performance diagram. Whether this limit also is required under dynamic conditions remains an issue for further research. As expected the turbocharger speed, air mass flow, compressor pressure ratio, and consequently the inlet receiver pressure and the maximum in-cylinder pressure will increase during ship acceleration. The (negative) compressor surge index will drop, indicating that the compressor operating points are moving away from the surge line, so the compressor will not surge during ship acceleration.

![Figure 29(a): Simulation results of ship acceleration. This figure contains four subplots: 'Combinator curve' showing propeller speed (RPM) and pitch (deg) vs SLC; 'SLC' showing SLC [-] vs Time [s]; 'Propeller revolution' showing propeller revolution [rpm] vs Time [s]; and 'Ship velocity' showing ship velocity [kn] vs Time [s].](b3df5964338063224492c01f09e4fed6_img.jpg)

**Combinator curve**

| SLC [-] | Propeller speed [RPM] | Propeller pitch [deg] |
|---------|-----------------------|-----------------------|
| -100    | 150                   | 5                     |
| -80     | 150                   | 5                     |
| -60     | 150                   | 5                     |
| -40     | 150                   | 5                     |
| -20     | 150                   | 5                     |
| 0       | 150                   | 5                     |
| 20      | 150                   | 5                     |
| 40      | 150                   | 5                     |
| 60      | 150                   | 5                     |
| 80      | 150                   | 5                     |
| 100     | 150                   | 5                     |

**SLC**

| Time [s] | actual SLC [-] | demand SLC [-] |
|----------|----------------|----------------|
| 0        | 100            | 100            |
| 50       | 100            | 100            |
| 100      | 100            | 100            |
| 200      | 100            | 100            |
| 300      | 100            | 100            |
| 400      | 100            | 100            |
| 500      | 100            | 100            |
| 600      | 100            | 100            |

**Propeller revolution**

| Time [s] | actual prop. revolution [rpm] | demand prop. revolution [rpm] |
|----------|-------------------------------|-------------------------------|
| 0        | 100                           | 100                           |
| 50       | 100                           | 100                           |
| 100      | 150                           | 150                           |
| 200      | 150                           | 150                           |
| 300      | 150                           | 150                           |
| 400      | 150                           | 150                           |
| 500      | 150                           | 150                           |
| 600      | 150                           | 150                           |

**Ship velocity**

| Time [s] | Ship velocity [kn] |
|----------|--------------------|
| 0        | 8                  |
| 100      | 9                  |
| 200      | 10                 |
| 300      | 11                 |
| 400      | 11.5               |
| 500      | 12                 |
| 600      | 12.5               |

Figure 29(a): Simulation results of ship acceleration. This figure contains four subplots: 'Combinator curve' showing propeller speed (RPM) and pitch (deg) vs SLC; 'SLC' showing SLC [-] vs Time [s]; 'Propeller revolution' showing propeller revolution [rpm] vs Time [s]; and 'Ship velocity' showing ship velocity [kn] vs Time [s].

(a) Combinator curve, SLC, propeller revolution, propeller pitch, ship velocity during ship acceleration

![Figure 29(b): Simulation results of ship acceleration. This figure contains four subplots: 'Engine speed' showing engine speed [RPM] vs Time [s]; 'Governor fuel rack' showing fuel rack position [-] vs Time [s]; 'Engine torque & PTO (+)/PTI (-) torque' showing engine torque [kNm] vs Time [s]; and 'Engine power & PTO (+)/PTI (-) power' showing engine power [kW] vs Time [s].](e95f47f7a4c01c8889d6d46919b4c73d_img.jpg)

**Engine speed**

| Time [s] | actual engine speed [RPM] | demand engine speed [RPM] | set engine speed [RPM] |
|----------|---------------------------|---------------------------|------------------------|
| 0        | 100                       | 100                       | 100                    |
| 50       | 100                       | 100                       | 100                    |
| 100      | 150                       | 150                       | 150                    |
| 200      | 150                       | 150                       | 150                    |
| 300      | 150                       | 150                       | 150                    |

**Governor fuel rack**

| Time [s] | Dynamic fuel rack position [-] | Static fuel rack position [-] |
|----------|--------------------------------|-------------------------------|
| 0        | 0.5                            | 0.5                           |
| 50       | 0.5                            | 0.5                           |
| 100      | 1.0                            | 1.0                           |
| 200      | 0.8                            | 0.8                           |
| 300      | 0.8                            | 0.8                           |

**Engine torque & PTO (+)/PTI (-) torque**

| Time [s] | Engine torque [kNm] | PTO/PTI torque [kNm] |
|----------|---------------------|----------------------|
| 0        | 100                 | 50                   |
| 50       | 100                 | 50                   |
| 100      | 220                 | 50                   |
| 200      | 200                 | 50                   |
| 300      | 200                 | 50                   |

**Engine power & PTO (+)/PTI (-) power**

| Time [s] | Engine power [kW] | PTO/PTI power [kW] |
|----------|-------------------|--------------------|
| 0        | 1000              | 500                |
| 50       | 1000              | 500                |
| 100      | 3500              | 500                |
| 200      | 3500              | 500                |
| 300      | 3500              | 500                |

**Engine Power/Speed (Sea Margin: 15%)**

| Engine speed [rpm] | Engine power [kW] | Load limit [kW] | Overload limit [kW] |
|--------------------|-------------------|-----------------|---------------------|
| 60                 | 500               | 500             | 500                 |
| 70                 | 800               | 800             | 800                 |
| 80                 | 1100              | 1100            | 1100                |
| 90                 | 1400              | 1400            | 1400                |
| 100                | 1700              | 1700            | 1700                |
| 110                | 2000              | 2000            | 2000                |
| 120                | 2300              | 2300            | 2300                |
| 130                | 2600              | 2600            | 2600                |
| 140                | 2900              | 2900            | 2900                |
| 150                | 3200              | 3200            | 3200                |
| 160                | 3500              | 3500            | 3500                |
| 170                | 3800              | 3800            | 3800                |
| 180                | 4100              | 4100            | 4100                |

Figure 29(b): Simulation results of ship acceleration. This figure contains four subplots: 'Engine speed' showing engine speed [RPM] vs Time [s]; 'Governor fuel rack' showing fuel rack position [-] vs Time [s]; 'Engine torque & PTO (+)/PTI (-) torque' showing engine torque [kNm] vs Time [s]; and 'Engine power & PTO (+)/PTI (-) power' showing engine power [kW] vs Time [s].

(b) Engine speed, fuel rack, torque and power during ship acceleration

Fig. 29. Simulation results of ship acceleration.

These results show that using static engine performance maps to investigate the engine dynamic behaviour could lead to misleading results.

### 5.2.2. Ship deceleration

To decelerate the ship, the SLC is reduced from 90 to 60 and the corresponding propeller revolution is decreased from 150 rpm to 100 rpm (Fig. 30(a)). Again, obvious differences between the

dynamic simulation results and the static results interpolated from the static engine performance maps can be found (Fig. 30(c) and (d)). During the transient process of the ship deceleration, the air excess ratio will go up as high as 3.3 before dropping back to around 2; the maximum in-cylinder temperature, in-cylinder temperature just before EO, exhaust valve temperature, outlet receiver temperature and temperature after turbine will first drop before gradually going up to a steady value (Fig. 30(c)). During ship deceleration, although the engine will be neither mechanically nor thermally overloaded (Fig. 30(b) and (c)), the compressor can surge, i.e., the compressor surge index becomes positive (Fig. 30(d)). A positive compressor surge index indicates that the compressor

operating line has crossed the surge line and runs in the unstable surge area as can be seen in the compressor map (Fig. 30(d)). The results have shown again that static engine performance maps cannot be directly used (interpolated) to predict the engine dynamic behaviour, as it will provide misleading results.

### 5.2.3. Ship crash stop

In the simulations of ship crash stop, the constant revolution propulsion control mode has been applied. The propeller revolution is set at 163.7 rpm and kept constant. The full ahead (SLC = 100) propeller pitch angle is set at 16.6°, which is 93% of the design pitch (17.83° or equivalently  $P/D = 0.7075$ ); while the full

![Figure 30(c): Five subplots showing engine parameters over time (0-300s) during ship acceleration. The parameters are: Air excess ratio λ, Exhaust valve temperature T_EV, Maximum in-cylinder temperature T_max, Outlet receiver temperature T_OR, and In-cylinder temperature just before EO T_EO. Each plot compares Dynamic (solid blue line) and Static (dashed red line) results. A horizontal dashed line indicates the limit for each parameter.](62ad98a4bc47922b5cf47de04571dae8_img.jpg)

Figure 30(c): Five subplots showing engine parameters over time (0-300s) during ship acceleration. The parameters are: Air excess ratio λ, Exhaust valve temperature T\_EV, Maximum in-cylinder temperature T\_max, Outlet receiver temperature T\_OR, and In-cylinder temperature just before EO T\_EO. Each plot compares Dynamic (solid blue line) and Static (dashed red line) results. A horizontal dashed line indicates the limit for each parameter.

(c) Air excess ratio, exhaust valve temperature, maximum in-cylinder temperature, outlet receiver temperature, in-cylinder temperature just before EO and turbine outlet temperature during ship acceleration

![Figure 30(d): Four subplots showing engine parameters over time (0-300s) during ship acceleration. The parameters are: Maximum in-cylinder pressure p_max, Compressor surge index SI, Inlet receiver pressure p_IR, and Turbocharger speed n_Tc. The first three plots compare Dynamic (solid blue line) and Static (dashed red line) results. The last plot is a compressor map showing Comp. pressure ratio π_com vs Air mass flow ḋ_com. It includes a surge line (solid black), a nominal point (blue circle), and a best efficiency point (red circle).](67518cfe156890dac13b5e67abd10dc1_img.jpg)

Figure 30(d): Four subplots showing engine parameters over time (0-300s) during ship acceleration. The parameters are: Maximum in-cylinder pressure p\_max, Compressor surge index SI, Inlet receiver pressure p\_IR, and Turbocharger speed n\_Tc. The first three plots compare Dynamic (solid blue line) and Static (dashed red line) results. The last plot is a compressor map showing Comp. pressure ratio π\_com vs Air mass flow ḋ\_com. It includes a surge line (solid black), a nominal point (blue circle), and a best efficiency point (red circle).

(d) Maximum in-cylinder pressure, inlet receiver pressure, turbocharger rotational speed, compressor surge index and compressor behaviour during ship acceleration

Fig. 29. (continued).

![Figure 30(a): Simulation results of ship deceleration. This figure contains four subplots showing the relationship between various parameters and the SLC (Ship Load Curve) over time. The top subplot, 'Combinator curve', shows Propeller speed [RPM] (0-200) and Propeller pitch [deg] (-20 to 20) versus SLC [-] (-100 to 100). The second subplot, 'Propeller revolution', shows Prop. revolution [rpm] (60-180) versus Time [s] (0-600), comparing actual (solid red) and demand (dashed black) values. The third subplot, 'Ship velocity', shows Ship velocity [kn] (0-15) versus Time [s] (0-600). The bottom subplot, 'SLC', shows SLC [-] (-100 to 100) versus Time [s] (0-600), comparing actual (solid red) and demand (dashed black) values. The final subplot, 'Propeller pitch', shows Propeller pitch [deg] (-20 to 20) versus Time [s] (0-600), comparing actual (solid red) and demand (dashed black) values.](b6750d26d3dd287a4a4d49b3670a44bd_img.jpg)

Figure 30(a): Simulation results of ship deceleration. This figure contains four subplots showing the relationship between various parameters and the SLC (Ship Load Curve) over time. The top subplot, 'Combinator curve', shows Propeller speed [RPM] (0-200) and Propeller pitch [deg] (-20 to 20) versus SLC [-] (-100 to 100). The second subplot, 'Propeller revolution', shows Prop. revolution [rpm] (60-180) versus Time [s] (0-600), comparing actual (solid red) and demand (dashed black) values. The third subplot, 'Ship velocity', shows Ship velocity [kn] (0-15) versus Time [s] (0-600). The bottom subplot, 'SLC', shows SLC [-] (-100 to 100) versus Time [s] (0-600), comparing actual (solid red) and demand (dashed black) values. The final subplot, 'Propeller pitch', shows Propeller pitch [deg] (-20 to 20) versus Time [s] (0-600), comparing actual (solid red) and demand (dashed black) values.

(a) Combinator curve, SLC, propeller revolution, propeller pitch, ship velocity during ship deceleration

![Figure 30(b): Simulation results of ship deceleration. This figure contains four subplots showing engine parameters over time. The top subplot, 'Engine speed', shows Engine speed [RPM] (60-180) versus Time [s] (0-300), comparing actual (solid blue), demand (dashed black), and set (dashed red) values. The second subplot, 'Engine torque & PTO (+)/PTI (-) torque', shows Engine torque [kNm] (0-200) versus Time [s] (0-300), comparing Engine (solid blue) and PTO/PTI (solid red) values. The third subplot, 'Engine power & PTO (+)/PTI (-) power', shows Engine power [kW] (0-3000) versus Time [s] (0-300), comparing Engine (solid blue) and PTO/PTI (solid red) values. The right subplot, 'Governor fuel rack', shows Fuel rack position [-] (0-1) versus Time [s] (0-300), comparing Dynamic (solid blue) and Static (dashed red) values. The bottom right subplot, 'Engine Power/Speed (Sea Margin: 15%)', shows Engine power [kW] (0-5000) versus Engine speed [rpm] (50-180), plotting the Load limit (green solid), Overload limit (red solid), MCR (4170kW@167rpm) (red dot), and Trajectory (blue solid line).](ef25c3cf1fdb334fc8679e85ab5265ca_img.jpg)

Figure 30(b): Simulation results of ship deceleration. This figure contains four subplots showing engine parameters over time. The top subplot, 'Engine speed', shows Engine speed [RPM] (60-180) versus Time [s] (0-300), comparing actual (solid blue), demand (dashed black), and set (dashed red) values. The second subplot, 'Engine torque & PTO (+)/PTI (-) torque', shows Engine torque [kNm] (0-200) versus Time [s] (0-300), comparing Engine (solid blue) and PTO/PTI (solid red) values. The third subplot, 'Engine power & PTO (+)/PTI (-) power', shows Engine power [kW] (0-3000) versus Time [s] (0-300), comparing Engine (solid blue) and PTO/PTI (solid red) values. The right subplot, 'Governor fuel rack', shows Fuel rack position [-] (0-1) versus Time [s] (0-300), comparing Dynamic (solid blue) and Static (dashed red) values. The bottom right subplot, 'Engine Power/Speed (Sea Margin: 15%)', shows Engine power [kW] (0-5000) versus Engine speed [rpm] (50-180), plotting the Load limit (green solid), Overload limit (red solid), MCR (4170kW@167rpm) (red dot), and Trajectory (blue solid line).

(b) Engine speed, fuel rack, torque and power during ship deceleration

Fig. 30. Simulation results of ship deceleration.

astern (SLC = -100) propeller pitch is set at  $-11.6^\circ$ , which is  $-65\%$  of the design pitch.

The ship crash stop is implemented by reducing SLC from 100 to  $-100$  (full ahead to full astern), so the propeller pitch will

consequently change from  $16.6^\circ$  to  $-11.6^\circ$  (Fig. 31(a)). During ship crash stop, the engine mechanical load (torque and maximum in-cylinder pressure) will first drop due to the decreasing positive propeller pitch; and then increase again (slightly overloaded) due to

the increasing negative pitch (Fig. 31(b) and (d)). The engine thermal load will also first drop and then go up again during the transient process of ship crash stop (Fig. 31(c)). In particular, when the engine load goes up, the air excess ratio drops below the limit as low as 1.47, and the engine could produce black smoke and be thermally overloaded. Furthermore, before the engine is thermally overloaded, the compressor may surge first when the engine load drops, making the engine dynamic behaviour even worse during the ship crash stop, exceeding all limits in one manoeuvre.

From the simulation results of ship acceleration, deceleration and crash stop, it is learnt that when the engine is under dynamic operations, although the engine power is within the (static)

operating envelope, the engine could still exceed the operating limits, especially the thermal overloading limit, black-smoke limit and compressor surge limit. To protect the engine from overloading, black smoking and compressor surge during ship acceleration, deceleration and (crash) stop, the changing rates of propeller revolution and pitch should be carefully controlled based on the real dynamic engine performance rather than the static engine performance maps, as the latter could provide misleading results on engine dynamic behaviour prediction.

![Figure 30(c): Five subplots showing engine parameters during ship deceleration. The x-axis for all plots is Time [s] from 0 to 300. The y-axes are: Air excess ratio λ (1 to 4), Exhaust valve temperature T_EV [K] (400 to 800), Cylinder temperature T_max [K] (1400 to 1800), Outlet receiver temperature T_OR [K] (400 to 1000), Cylinder temperature T_EO [K] (600 to 1200), and Temperature after turbine T_TUR [K] (450 to 550). Each plot compares Dynamic (solid blue line) and Static (dashed red line) results. A limit line is shown in each plot: λ limit (dashed black), T_EV limit (dashed black), T_EO limit (dashed black), and T_TUR limit (dashed black).](93587f920736a2fdcefeba94b29f302a_img.jpg)

Figure 30(c): Five subplots showing engine parameters during ship deceleration. The x-axis for all plots is Time [s] from 0 to 300. The y-axes are: Air excess ratio λ (1 to 4), Exhaust valve temperature T\_EV [K] (400 to 800), Cylinder temperature T\_max [K] (1400 to 1800), Outlet receiver temperature T\_OR [K] (400 to 1000), Cylinder temperature T\_EO [K] (600 to 1200), and Temperature after turbine T\_TUR [K] (450 to 550). Each plot compares Dynamic (solid blue line) and Static (dashed red line) results. A limit line is shown in each plot: λ limit (dashed black), T\_EV limit (dashed black), T\_EO limit (dashed black), and T\_TUR limit (dashed black).

(c) Air excess ratio, exhaust valve temperature, maximum in-cylinder temperature, outlet receiver temperature, in-cylinder temperature just before EO and turbine outlet temperature during ship deceleration

![Figure 30(d): Five subplots showing engine parameters during ship deceleration. The x-axis for all plots is Time [s] from 0 to 300. The y-axes are: Maximum in-cylinder pressure p_max [bar] (50 to 200), Compressor surge index SI (-0.1 to 0.1), Inlet receiver pressure p_IR [bar] (1 to 3), Turbocharger speed n_Tc [rpm] × 10^4 (1 to 2.5), and Compressor map (Comp. pressure ratio π_com [-] vs Air mass flow φ_com [kg/s]). Each plot compares Dynamic (solid blue line) and Static (dashed red line) results. A surge line is shown in the Compressor surge index SI plot. The Compressor map plot shows the surge line (solid black), nominal point (blue circle), and best efficiency point (red circle).](8a597e344d10e36bbb2f243f6c4e74c6_img.jpg)

Figure 30(d): Five subplots showing engine parameters during ship deceleration. The x-axis for all plots is Time [s] from 0 to 300. The y-axes are: Maximum in-cylinder pressure p\_max [bar] (50 to 200), Compressor surge index SI (-0.1 to 0.1), Inlet receiver pressure p\_IR [bar] (1 to 3), Turbocharger speed n\_Tc [rpm] × 10^4 (1 to 2.5), and Compressor map (Comp. pressure ratio π\_com [-] vs Air mass flow φ\_com [kg/s]). Each plot compares Dynamic (solid blue line) and Static (dashed red line) results. A surge line is shown in the Compressor surge index SI plot. The Compressor map plot shows the surge line (solid black), nominal point (blue circle), and best efficiency point (red circle).

(d) Maximum in-cylinder pressure, inlet receiver pressure, turbocharger rotational speed, compressor surge index and compressor behaviour during ship deceleration

Fig. 30. (continued).

![Four subplots showing ship control parameters during a crash stop. Top-left: Combinator curve with Propeller speed [RPM] (0-200) and Propeller pitch [deg] (-20 to 20) vs SLC [-100 to 100]. Top-right: SLC [-100 to 100] vs Time [s] (0 to 600) with actual (solid red) and demand (dashed black) lines. Bottom-left: Propeller revolution [rpm] (60-180) vs Time [s] (0 to 600) with actual (solid red) and demand (dashed black) lines. Bottom-right: Propeller pitch [deg] (-20 to 20) vs Time [s] (0 to 600) with actual (solid red) and demand (dashed black) lines. Bottom-most: Ship velocity [kn] (0-15) vs Time [s] (0 to 600) showing a smooth deceleration curve.](96a7eac66ef72bb016c280278506ac63_img.jpg)

Four subplots showing ship control parameters during a crash stop. Top-left: Combinator curve with Propeller speed [RPM] (0-200) and Propeller pitch [deg] (-20 to 20) vs SLC [-100 to 100]. Top-right: SLC [-100 to 100] vs Time [s] (0 to 600) with actual (solid red) and demand (dashed black) lines. Bottom-left: Propeller revolution [rpm] (60-180) vs Time [s] (0 to 600) with actual (solid red) and demand (dashed black) lines. Bottom-right: Propeller pitch [deg] (-20 to 20) vs Time [s] (0 to 600) with actual (solid red) and demand (dashed black) lines. Bottom-most: Ship velocity [kn] (0-15) vs Time [s] (0 to 600) showing a smooth deceleration curve.

(a) Combinator curve, SLC, propeller revolution, propeller pitch, ship velocity during ship crash stop

![Four subplots showing engine parameters during a crash stop. Top-left: Engine speed [RPM] (60-180) vs Time [s] (0 to 300) with actual (solid blue), demand (dashed black), and set (dashed red) lines. Top-right: Governor fuel rack position [-1 to 1] vs Time [s] (0 to 300) with Dynamic (solid blue) and Static (dashed red) lines. Bottom-left: Engine torque & PTO (+)/PTI (-) torque [kNm] (0-300) vs Time [s] (0 to 300) with Engine (solid blue) and PTO/PTI (solid red) lines. Bottom-right: Engine power & PTO (+)/PTI (-) power [kW] (0-6000) vs Time [s] (0 to 300) with Engine (solid blue) and PTO/PTI (solid red) lines. A separate plot on the right shows Engine Power/Speed (Sea Margin: 15%) with Engine power [kW] (0-5000) vs Engine speed [rpm] (50-180), including Load limit (green), Overload limit (red), MCR (4170kW@167rpm) (red dot), and Trajectory (blue line).](f85bf99d372e735d228361bf4d3cf7e6_img.jpg)

Four subplots showing engine parameters during a crash stop. Top-left: Engine speed [RPM] (60-180) vs Time [s] (0 to 300) with actual (solid blue), demand (dashed black), and set (dashed red) lines. Top-right: Governor fuel rack position [-1 to 1] vs Time [s] (0 to 300) with Dynamic (solid blue) and Static (dashed red) lines. Bottom-left: Engine torque & PTO (+)/PTI (-) torque [kNm] (0-300) vs Time [s] (0 to 300) with Engine (solid blue) and PTO/PTI (solid red) lines. Bottom-right: Engine power & PTO (+)/PTI (-) power [kW] (0-6000) vs Time [s] (0 to 300) with Engine (solid blue) and PTO/PTI (solid red) lines. A separate plot on the right shows Engine Power/Speed (Sea Margin: 15%) with Engine power [kW] (0-5000) vs Engine speed [rpm] (50-180), including Load limit (green), Overload limit (red), MCR (4170kW@167rpm) (red dot), and Trajectory (blue line).

(b) Engine speed, fuel rack, torque and power during ship crash stop

Fig. 31. Simulation results of ship crash stop.



# 6. Conclusions and recommendations

This paper has introduced a Mean Value First Principle Parametric (MVFPP) engine model of the two-stroke marine diesel engine. The MVFPP engine model has been integrated into a ship propulsion system model of the benchmark ocean-going chemical tanker. Based on the Mean Value First Principle Parametric (MVFPP) engine model and the integrated ship propulsion model, the engine behaviour including mechanical loading, thermal loading, and compressor surge of the benchmark chemical tanker under both static and dynamic operating conditions has been investigated. It

has been demonstrated that the MVFPP engine model can be considered adequate to predict the engine behaviour in ship propulsion system with detailed information and satisfactory accuracy and calculation speed.

For the two-stroke marine diesel engine, the torque/speed limit is mainly limited by the engine thermal load at lower engine speeds and mechanical load at high speeds, although the latter is rarely exceeded. The air excess ratio and the in-cylinder temperature just before exhaust valve opening (EO) both are effective indicators for 2-stroke engine thermal loading. This contradicts earlier findings for 4-stroke engines where the exhaust valve temperature indicator

![Figure 31(c): Five subplots showing engine parameters over time (0 to 300 seconds). The top subplot shows the Air excess ratio λ, with Dynamic (solid blue) and Static (dashed red) lines, and a limit (dashed black) at approximately 2.2. The second subplot shows Cylinder temperature T_max in Kelvin, with Dynamic and Static lines. The third subplot shows Cylinder temperature T_EO in Kelvin, with Dynamic and Static lines, and a limit (dashed black) at approximately 1000 K. The fourth subplot shows Exhaust valve temperature T_EV in Kelvin, with Dynamic and Static lines. The bottom subplot shows Outlet receiver temperature T_OR in Kelvin, with Dynamic and Static lines, and a limit (dashed black) at approximately 1000 K. The fifth subplot shows Temperature after turbine T_TUR in Kelvin, with Dynamic and Static lines.](bd4617f25d15430eb78c2d6d75a99dde_img.jpg)

Figure 31(c): Five subplots showing engine parameters over time (0 to 300 seconds). The top subplot shows the Air excess ratio λ, with Dynamic (solid blue) and Static (dashed red) lines, and a limit (dashed black) at approximately 2.2. The second subplot shows Cylinder temperature T\_max in Kelvin, with Dynamic and Static lines. The third subplot shows Cylinder temperature T\_EO in Kelvin, with Dynamic and Static lines, and a limit (dashed black) at approximately 1000 K. The fourth subplot shows Exhaust valve temperature T\_EV in Kelvin, with Dynamic and Static lines. The bottom subplot shows Outlet receiver temperature T\_OR in Kelvin, with Dynamic and Static lines, and a limit (dashed black) at approximately 1000 K. The fifth subplot shows Temperature after turbine T\_TUR in Kelvin, with Dynamic and Static lines.

(c) Air excess ratio, exhaust valve temperature, maximum in-cylinder temperature, outlet receiver temperature, in-cylinder temperature just before EO and turbine outlet temperature during ship crash stop

![Figure 31(d): Five subplots showing engine parameters over time (0 to 300 seconds) and a compressor map. The top subplot shows Maximum in-cylinder pressure p_max in bar, with Dynamic (solid blue) and Static (dashed red) lines. The second subplot shows Inlet receiver pressure p_IR in bar, with Dynamic and Static lines. The third subplot shows Turbocharger speed n_T in rpm (scaled by 10^4), with Dynamic and Static lines, and a Max speed limit (dashed black) at approximately 2.5 x 10^4 rpm. The fourth subplot shows Compressor surge index SI, with Dynamic and Static lines, and a surge line (dashed black). The bottom subplot is a Compressor map showing Comp. pressure ratio π_com (y-axis, 1 to 4.5) versus Air mass flow ḋ_com in kg/s (x-axis, 1 to 9). It includes Dynamic (solid blue) and Static (dashed red) compressor curves, a surge line (thick black), a nominal point (blue circle), and a best efficiency point (red circle).](47e75dc9e83054b2dac3df8bf3e57019_img.jpg)

Figure 31(d): Five subplots showing engine parameters over time (0 to 300 seconds) and a compressor map. The top subplot shows Maximum in-cylinder pressure p\_max in bar, with Dynamic (solid blue) and Static (dashed red) lines. The second subplot shows Inlet receiver pressure p\_IR in bar, with Dynamic and Static lines. The third subplot shows Turbocharger speed n\_T in rpm (scaled by 10^4), with Dynamic and Static lines, and a Max speed limit (dashed black) at approximately 2.5 x 10^4 rpm. The fourth subplot shows Compressor surge index SI, with Dynamic and Static lines, and a surge line (dashed black). The bottom subplot is a Compressor map showing Comp. pressure ratio π\_com (y-axis, 1 to 4.5) versus Air mass flow ḋ\_com in kg/s (x-axis, 1 to 9). It includes Dynamic (solid blue) and Static (dashed red) compressor curves, a surge line (thick black), a nominal point (blue circle), and a best efficiency point (red circle).

(d) Maximum in-cylinder pressure, inlet receiver pressure, turbocharger rotational speed, compressor surge index and compressor behaviour during ship crash stop

Fig. 31. (continued).

performed better and this needs further investigation. The large slip factor of two-stroke diesel engines helps cooling the exhaust valve temperature and the temperature in the outlet receiver before the turbine. Compressor surge is not a limiting factor of the operations of the two-stroke engine under static conditions even at low loads, especially for two-stroke marine diesel engines with auxiliary blowers. During transient process of dynamic operations, the engine behaviour cannot be directly read (interpolated) from the static engine behaviour maps (the static performance plotted in engine power/revolution envelope). The engine could still be thermally overloaded during for instance ship acceleration, while the compressor could surge during deceleration, even if the engine power trajectory is still inside the static engine power/revolution envelope during such dynamic processes. Thus, the engine static performance maps are inadequate for predicting the engine dynamic performance.

When matching the engine with the propeller and/or when designing the ship propulsion control system, not only the static engine operating envelope, but also the dynamic engine behaviour should be taken into account. To protect the engine from overloading during ship dynamic and/or heavy operations and as a result improve the ship and engine operational safety, the rate of change of the engine speed and propeller pitch normally is controlled using feed forward schedules. Of course, this may result in longer acceleration, deceleration and/or crash stop times, which is something the crew of the ship should be aware of. More intelligent control schemes are possible when based on simulations using the realistic dynamic engine and propulsion models as presented in this paper.

Note that, when investigating the dynamic engine behaviour during ship acceleration, deceleration and crash stop, only normal sea condition has now been considered. The sea condition is simply modelled by the Sea Margin (SM), which indicates the increase of ship resistance due to actual sea conditions compared to the sea trial condition (calm sea). In future work, a more detailed sea state model, especially the wind and waves models, the latter also comprising the dynamic effect on the wake fraction that through the propeller directly affects the load of the engine, will be applied and integrated into the ship propulsion and manoeuvring model. Based on the model, effects of adverse sea conditions on the ship propulsion and manoeuvring performance as well as the engine behaviour will be explored with a view on the concerns about low installed power in ships after introduction of IMO's EEDI rulings.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgements

This project partly is financially supported by the International Science and Technology Cooperation Program of China, 2014DFA71700; Marine Low-Speed Engine Project-Phase I; China High-tech Ship Research Program.

The authors would like to thank CSSC Marine Power Co., Ltd. (CMP) for providing the ample data of the benchmark ship and the engines, and the support for the measurements of the two-stroke marine diesel engines.

# Appendix A. Two-stage scavenging model

## A.1 Relative scavenging time and scavenging time constant.

### A.1.2 Mean value scavenging mass flow of the engine.

In the mean value model, all the mass flows in the engine have been averaged over the full cycle (Stapersma, 2010c). Accordingly, the mean value scavenging mass flow is calculated by Eq. (A.1).

$$\dot{m}_{sc-in} \stackrel{\text{def}}{=} \frac{i \cdot \int_{t_{i0}}^{t_{iC}} \tilde{m}_{sc-in} \cdot dt}{t_{cycle}} \quad (\text{A.1})$$

where,  $i$  is the number of the cylinders of the engine;  $\tilde{m}_{sc-in}$  is the real ingoing scavenging mass flow per cylinder of the engine;  $t_{cycle}$  is the time of the full cycle and is calculated by  $t_{cycle} = k/N$ , in which  $N$  is the engine rotational speed and  $k$  is the number of revolutions per cycle (for two-stroke engine  $k = 1$ , and for four-stroke engine  $k = 2$ );  $t_{i0}$  and  $t_{iC}$  are the time when the inlet ports open and close respectively.

It is assumed that EO and IC are instantaneous and that the pressures in both the cylinder and the inlet receiver are constant during the scavenging process. As a result, the scavenging mass flow  $\tilde{m}_{sc-in}$ , which can be calculated by the resistance element of the inlet ports, is also constant. So, the mean value scavenging mass flow of the engine is calculated by Eq. (A.2).

$$\dot{m}_{sc-in} = \tilde{m}_{sc-in} \cdot \frac{t_{sc} \cdot N \cdot i}{k} \quad (\text{A.2})$$

where,  $t_{sc} (=t_{iC} - t_{i0})$  is the real time interval over the scavenging process, which can be calculated by the scavenging valve timing and the engine speed.

### A.1.3 Scavenging time constant.

The ideal scavenging process can be modelled by the 'perfect displacement model', where the volume of B zone containing only fresh air increases from zero to the size of whole cylinder volume, pushing A zone containing only exhaust gas out of the cylinder. Based on the perfect displacement model, all the exhaust gases will be perfectly pushed out of the cylinder volume by the fresh scavenging air and there will be no residual gas left in the cylinder after scavenging. To express the scavenging time in a mean value model, the scavenging time constant  $\tau_{sc}$  is defined by Eq. (A.3) based on the time when A zone disappears from the cylinder volume in a perfect displacement model.

$$\tau_{sc} \stackrel{\text{def}}{=} \frac{V}{\tilde{V}_{sc-in}} \quad (\text{A.3})$$

where,  $V$  is the volume of the cylinder, which is assumed to be constant during the scavenging process ( $V=V_{i0}$ );  $p$  is the pressure in the cylinder;  $\tilde{V}_{sc-in}$  is the real scavenging volume flow per cylinder of the engine entering the cylinder at pressure  $p$  after the inlet, which is calculated by Eq. (A.4);

$$\tilde{V}_{sc-in} = \frac{R_{sc-in} \cdot T_{sc-in} \cdot \dot{m}_{sc-in}}{p} \quad (\text{A.4})$$

### A.1.3 Relative scavenging time.

The scavenging time  $t_{sc}$  has been made nondimensional against the scavenging time constant  $\tau_{sc}$  as the relative scavenging time  $t_{sc,r}$  as shown in Eq. (A.5). Combining Eq. (A.2) to Eq. (A.5), the relative scavenging time  $t_{sc,r}$  is calculated by Eq. (A.6).

$$t_{sc,r} \stackrel{\text{def}}{=} \frac{t_{sc}}{\tau_{sc}} \quad (\text{A.5})$$

$$t_{sc,r} = \frac{R_{sc-in} \cdot T_{sc-in} \cdot \dot{m}_{sc-in}}{p \cdot V} \cdot \frac{k}{i \cdot N} \quad (\text{A.6})$$

## A.2 Stage I: Two-zone scavenging model.

The two-zone scavenging model is applied during stage I, as the cylinder is divided into two zones, namely A zone and B zone. Parameters in A zone and B zone are calculated individually based on the mass balance, air (or composition) balance, gas law and the energy balance. The average value of the state parameters of the whole cylinder volume are calculated by mixing A zone and B zone. It is assumed that there is no mass and heat exchange between A zone and B zone, and there is no heat exchange between the two zones and the cylinder wall.

### A.2.1 B zone.

According to the definition of B zone, there is only an ingoing mass flow entering B zone and there is no mass flow flowing out. According to the mass balance, the mass accumulation within B zone is equal to the net inflow as shown in equation Eq. (A.7). The final solution for the normalised mass of B zone after a certain scavenging time is expressed by equation Eq. (A.8).

$$\frac{dm_B}{dt} = \dot{m}_{sc-in} \quad (A.7)$$

$$\frac{m_B}{m(0)} = S_B(0) + t_{sc,r} \cdot y(0) \quad (A.8)$$

where,  $m(0)$  is the initial mass of the whole cylinder volume when the scavenging starts;  $S_B(0)$  is the initial mass ratio of B zone;  $y(0)$  is the initial temperature ratio of the temperature in the cylinder to that of the ingoing mass flow;  $t_{sc,r}$  is the relative scavenging time.

The temperature is normalised against the temperature of the ingoing scavenging mass flow as the temperature ratio, which is defined by equation Eq. (A.9).

$$y \stackrel{\text{def}}{=} \frac{T}{T_{sc-in}} \quad (A.9)$$

where,  $T_{sc-in}$  is the temperature of the ingoing scavenging mass flow, which is equal to the temperature in the inlet receiver  $T_{ir}$ .

The ideal gas law for B zone is shown in equation Eq. (A.10).

$$p_B \cdot V_B = m_B \cdot R_B \cdot T_B \quad (A.10)$$

According to the energy balance, the accumulation of internal energy in B zone is equal to the net inflow of enthalpy plus the work done, assuming no heat exchange with the wall.

$$\frac{dU_B}{dt} = \dot{H}_{sc-in} - p \cdot \frac{dV_B}{dt} \quad (A.11)$$

It is assumed that the specific heats of the gases in B zone and the ingoing scavenging air are the same and constant during the scavenging process. Combining equations Eq. (A.7), Eq. (A.10) and Eq. (A.11), the final solution for the temperature in B zone in a normalised form is shown in equation Eq. (A.12). According to gas law, combining equations Eq. (A.10), Eq. (A.8) and Eq. (A.12), the normalised volume of B zone is calculated by equation Eq. (A.13).

$$y_B \stackrel{\text{def}}{=} \frac{T_B}{T_{sc-in}} = 1 + \frac{S_B(0) \cdot [y_B(0) - 1]}{S_B(0) + t_{sc,r} \cdot y(0)} \quad (A.12)$$

$$\frac{V_B}{V} = S_B(0) + t_{sc,r} \quad (A.13)$$

According to the air balance, the air mass accumulation in B zone is equal to the net air inflow as shown in equation Eq. (A.14). The final solution for composition in B zone is calculated by equation Eq. (A.15).

$$\frac{dm_{a,B}}{dt} = \dot{m}_{a,sc-in} \quad (A.14)$$

$$x_B = x_{sc-in} - \frac{S_B(0) \cdot [x_{sc-in} - x(0)]}{S_B(0) + y(0) \cdot t_{sc,r}} \quad (A.15)$$

### A.2.2 A zone.

There is no mass exchange between A zone and B zone, so, the composition in A zone is constant during stage I. Assume that the composition of the outgoing scavenging mass flow is the same as that in A zone during stage I as shown in equation Eq. (A.16).

$$x_A = x(0) = x_{sc-out} \quad (A.16)$$

According to the mass balance, the mass accumulation within A zone is equal to the net inflow.

$$\frac{dm_A}{dt} = -\dot{m}_{sc-out} \quad (A.17)$$

The ideal gas law for A zone:

$$p_A \cdot V_A = m_A \cdot R_A \cdot T_A \quad (A.18)$$

According to the energy balance, the accumulation of internal energy in A zone is equal to the net inflow of enthalpy plus the work done, assuming no heat exchange with the wall.

$$\frac{dU_A}{dt} = -\dot{H}_{sc-out} - p \cdot \frac{dV_A}{dt} \quad (A.19)$$

Combining equations Eq. (A.17), Eq. (A.18) and Eq. (A.19), it is proved that the temperature in A zone is constant.

$$T_A = T(0) = \text{constant} \quad (A.20)$$

With the relationship of the volumes in the cylinder, i.e.,  $V = V_A + V_B$ , the volume of A zone is calculated by equation Eq. (A.21). According to the gas law, the mass of A zone is calculated by equation Eq. (A.22).

$$\frac{V_A}{V} = S_A(0) - t_{sc,r} \quad (A.21)$$

$$\frac{m_A}{m(0)} = S_A(0) - t_{sc,r} \quad (A.22)$$

### A.2.3 The whole cylinder volume

The mean parameters of the whole cylinder volume are calculated by mixing the two zones based on the mass balance, air (or composition) balance, gas law and the energy balance.

With the mass relationship in the cylinder volume, i.e.,  $m = m_A + m_B$ , the total mass in the cylinder volume is calculated by equation Eq. (A.23). According to the ideal gas law for the whole (constant) cylinder volume, the average temperature in the cylinder is calculated by equation Eq. (A.24).

$$\frac{m}{m(0)} = 1 + t_{sc,r} \cdot [y(0) - 1] \quad (A.23)$$

$$y \stackrel{\text{def}}{=} \frac{T}{T_{sc-in}} = \frac{y(0)}{1 + t_{sc,r} \cdot [y(0) - 1]} \quad (A.24)$$

The average composition of the whole cylinder volume is calculated by equation Eq. (A.25). So, the final solution for the composition of the mass in the cylinder is shown in equation Eq. (A.26).

$$x = \frac{m_A \cdot x_A + m_B \cdot x_B}{m} \quad (A.25)$$

$$x = \frac{[x_{sc-in} \cdot y(0) - x(0)] \cdot t_{sc,r} + x(0)}{1 + t_{sc,r} \cdot [y(0) - 1]} \quad (A.26)$$

### A.2.4 End time of stage I.

A zone will disappear at the end of stage I and the mass in A zone becomes zero as shown in equation Eq. (A.27).

$$\frac{m_A}{m(0)} = S_A(0) - t_{sc,r} = 0 (t_{sc,r} = t_{sc,r,I}) \quad (A.27)$$

During stage I,  $\frac{m_A(0)}{m(0)} \ge 0$  and  $t_{sc,r} \le S_A(0)$ , so, stage I will end at  $t_{sc,r,I} = S_A(0)$ .

## A.3 Stage II: Perfect mixing model.

The perfect mixing model for a constant control volume (the cylinder volume) will be applied in stage II as only the perfect mixing zone (B zone) exists in the cylinder in this stage. The perfect mixing model is also based on the mass balance, air (or composition) balance, gas law and the energy balance. In the perfect mixing model introduced in (Stapersma, 1999) the heat exchange between the gas and the cylinder wall has been taken into account. However, in order to keep the assumptions consistent in this paper, the perfect mixing model in stage II also neglects the heat exchange with the cylinder wall. The final solution for the temperature, composition and mass in the whole cylinder volume including only B zone (perfect mixing zone) is shown in equations Eq. (A.28), Eq. (A.29) and Eq. (A.30).

$$y = \frac{y_{II}(0)}{1 + [y_{II}(0) - 1] \cdot [1 - e^{-(t_{sc,r} - t_{sc,r,I})}]} \quad (A.28)$$

$$x = x_{sc-in} - \frac{[x_{sc-in} - x_{II}(0)] \cdot e^{-(t_{sc,r} - t_{sc,r,I})}}{1 + [y_{II}(0) - 1] \cdot [1 - e^{-(t_{sc,r} - t_{sc,r,I})}]} \quad (A.29)$$

$$\frac{m}{m(0)} = y(0) \cdot \left\{ 1 - \left[ 1 - \frac{1}{y_{II}(0)} \right] \cdot e^{-(t_{sc,r} - t_{sc,r,I})} \right\} \quad (A.30)$$

where,  $x_{II}(0)$  and  $y_{II}(0)$  are the initial air mass ratio and temperature ratio of stage II, which are calculated by the two-zone scavenging model at the end of stage I ( $t_{sc,r} = t_{sc,r,I}$ ).

## A.4 Mean value parameters of outgoing scavenging flow.

To calculate the condition in the outlet receiver, the parameters of the outgoing scavenging flow, such as the mass  $m_{sc-out}$ , mean value composition  $\bar{x}_{sc-out}$  and mean value temperature of the outgoing flow  $\bar{T}_{sc-out}$  need to be calculated.

### A.4.1 Mass of outgoing scavenging flow.

According to the composition balance in the cylinder volume expressed by Eq. (A.31), the average air mass ratio of the outgoing scavenging flow is calculated by Eq. (A.32).

$$m = m(0) + m_{sc-in} - m_{sc-out} \quad (A.31)$$

$$\frac{m_{sc-out}}{m(0)} = 1 + y(0) \cdot t_{sc,r} - \frac{m}{m(0)} \quad (A.32)$$

### A.4.2 Mean value composition of outgoing scavenging flow.

According to the composition balance in the cylinder volume expressed by Eq. (A.33), the average air mass ratio of the outgoing scavenging flow is calculated by Eq. (A.34).

$$m \cdot x = m(0) \cdot x(0) + m_{sc-in} - m_{sc-out} \cdot \bar{x}_{sc-out} \quad (A.33)$$

$$\bar{x}_{sc-out} = \frac{x(0) + y(0) \cdot t_{sc,r} - m/m(0) \cdot x}{1 + y(0) \cdot t_{sc,r} - m/m(0)} \quad (A.34)$$

### A.4.3 Mean value temperature of outgoing scavenging flow.

The energy balance for the cylinder volume with the assumption of no work and no heat exchange with the cylinder wall is expressed by Eq. (A.35).

$$c_v \cdot [m \cdot T - m(0) \cdot T(0)] = c_{p,sc-in} \cdot T_{sc-in} \cdot m_{sc-in} - \bar{c}_{p,sc-out} \cdot \bar{T}_{sc-out} \cdot m_{sc-out} \quad (A.35)$$

According to the assumption that the pressure in the (constant) cylinder volume is constant ( $p \cdot V = \text{constant}$ ) during scavenging process and based on the ideal gas law ( $p \cdot V = m \cdot R \cdot T$ ), it can be concluded that the internal energy change in the cylinder volume is zero, i.e.,  $c_v \cdot [m \cdot T - m(0) \cdot T(0)] = 0$ . So, the mean temperature of the scavenging flow out of the cylinder over the total outgoing mass is calculated by Eq. (A.36) assuming the mean value specific heat ratio of outgoing scavenging mass is the same as that of the ingoing scavenging air ( $\bar{c}_{p,sc-out} = c_{p,sc-in}$ ). The normalised mean temperature of the outgoing scavenging flow is calculated by Eq. (A.37).

$$\bar{T}_{sc-out} = \frac{T_{sc-in} \cdot m_{sc-in}}{m_{sc-out}} \quad (A.36)$$

$$\bar{y}_{sc-out} \stackrel{\text{def}}{=} \frac{\bar{T}_{sc-out}}{T_{sc-in}} = \frac{y(0) \cdot t_{sc,r}}{1 + y(0) \cdot t_{sc,r} - m/m(0)} \quad (A.37)$$

# Appendix B. Engine components model

## B.1 Turbocharger model.

### B.1.1 Buchi balance.

The most crucial physics for a turbocharged diesel engine is the Buchi balance since it defines the cooperation between the three components that actually make up the diesel engine: the cylinder, the compressor and the turbine. The latter are directly cooperating through the Buchi power balance but the mass flow and turbine entry temperature in this balance interact with the cylinder process, in particular with its gas exchange. The power balance between the compressor and the turbine is governed by the “Buchi equation” (Eq. (B.1)) (Stapersma, 2010b). In the Buchi balance, the turbocharger efficiency requires a good prediction of compressor and turbine efficiency and thus good models for these components and further a satisfactory model for the turbocharger mechanical losses.

$$\pi_{com} = \left[ 1 + \delta \cdot \chi \cdot \eta_{TC} \cdot \tau_{TC} \cdot \left( 1 - \frac{1}{\pi_{tur}^{\frac{\gamma_{gas}-1}{\gamma_{gas}}}} \right) \right]^{\frac{\gamma_{air}}{\gamma_{air}-1}} \quad (B.1)$$

where,  $\pi_{com}$  is the compressor pressure ratio;  $\pi_{tur}$  is the turbine pressure ratio;  $\delta$  is the fuel addition factor ( $\delta = 1/(1 + \lambda)$ ,  $\lambda$  is the air excess ratio);  $\chi$  is the ratio between specific heats of exhaust gas and air ( $\chi = c_{p,gas}/c_{p,air}$ );  $\eta_{TC}$  is the turbocharger efficiency;  $\tau_{TC}$  is the turbocharger temperature ratio (turbine inlet temperature divided by compressor inlet temperature);  $\gamma_{gas}$  and  $\gamma_{air}$  are the specific heat ratios of gas and air respectively.

### B.1.2 Compressor and turbine characteristics

To predict the off-design performance, including part loads and

transient operation performance, of the turbocharger as well as the turbocharged engine, first principle parametric compressor and turbine models developed in (Stapersma, 2013) have been used in this paper. The compressor and turbine models are capable of modelling the turbocharger characteristics, including the compressor surge, turbine choking and compressor choking at high rotational speeds. Since both the compressor and turbine models in the overall engine model (Fig. 5) are analogous to resistance models and represent flow momentum balance, the inputs are the pressure ratio and the turbocharger rotational speed while the outputs are the mass flow, temperature ratio and the compressor or turbine efficiency.

One of the potential safety threats to the turbocharged engine is compressor surge, especially in part loads and dynamic operation conditions. To quantify compressor surge behaviour, a compressor surge index (SI) indicating the non-dimensional distance between the compressor operating line and the surge line is defined as illustrated in Fig. B.1. The compressor surge index is negative when the compressor operates in non-surg ing area, positive when working in surging area, while zero when it is hitting the surge line (Fig. B.1).

![Figure B.1: Compressor Surge Index (SI). A graph showing the relationship between Nondimensional air mass flow [-] on the x-axis and Comp. pressure ratio [-] on the y-axis. A solid black curve represents the 'Surge line', and a dashed blue line represents the 'Operating line'. The area between them is labeled 'Surge Index SI < 0'. The point where they intersect is labeled 'Surge Index SI = 0'. To the left of the intersection, the area is labeled 'Surge Index SI > 0'.](cb74fd9f5ec715dd3e2e325b864b48bc_img.jpg)

Figure B.1: Compressor Surge Index (SI). A graph showing the relationship between Nondimensional air mass flow [-] on the x-axis and Comp. pressure ratio [-] on the y-axis. A solid black curve represents the 'Surge line', and a dashed blue line represents the 'Operating line'. The area between them is labeled 'Surge Index SI < 0'. The point where they intersect is labeled 'Surge Index SI = 0'. To the left of the intersection, the area is labeled 'Surge Index SI > 0'.

Fig. B.1. Compressor Surge Index (SI).

### B.1.3 Turbocharger mechanical efficiency.

In order to model the turbocharger mechanical efficiency at various operating conditions, it is assumed that the turbocharger torque loss is a function of the turbocharger rotational speed and the compressor outlet pressure as shown in Eq. (B.2).

$$M_{\text{loss,TC}}^* = 1 + a_{\text{TC}} \cdot (n_{\text{TC}}^* - 1) + b_{\text{TC}} \cdot (p_{\text{com}}^* - 1) \quad (\text{B.2})$$

Where,  $a_{\text{TC}}$  and  $b_{\text{TC}}$  are constants;  $M_{\text{loss,TC}}^*$ ,  $n_{\text{TC}}^*$  and  $p_{\text{com}}^*$  are the normalised torque loss, turbocharger rotational speed and the compressor outlet pressure as shown in Eq. (B.3), Eq. (B.4) and Eq. (B.5).

$$M_{\text{loss,TC}}^* = \frac{M_{\text{loss,TC}}}{M_{\text{loss,TC,nom}}} \quad (\text{B.3})$$

$$n_{\text{TC}}^* = \frac{n_{\text{TC}}}{n_{\text{TC,nom}}} \quad (\text{B.4})$$

$$p_{\text{com}}^* = \frac{p_{\text{com}}}{p_{\text{com,nom}}} \quad (\text{B.5})$$

Where,  $M_{\text{loss,TC,nom}}$ ,  $n_{\text{TC,nom}}$  and  $p_{\text{com,nom}}$  are the turbocharger torque loss, turbocharger rotational speed and the compressor outlet pressure at nominal operating condition.

## B.2 Air cooler model.

The outlet temperature of the air cooler is calculated by Eq. (B.6) according to the definition of the heat exchanger effectiveness  $\epsilon_{\text{AC}}$  of the air cooler in Eq. (B.7).

$$T_{\text{CAC}} = T_{\text{ac}} - \epsilon_{\text{AC}} \cdot (T_{\text{ac}} - T_{\text{water}}) \quad (\text{B.6})$$

$$\epsilon_{\text{AC}} \stackrel{\text{def}}{=} \frac{T_{\text{ac}} - T_{\text{CAC}}}{T_{\text{ac}} - T_{\text{water}}} \quad (\text{B.7})$$

Where,  $T_{\text{ac}}$  is the inlet temperature of the cooler;  $T_{\text{CAC}}$  is the outlet temperature of the cooler;  $T_{\text{water}}$  is the temperature of the cooling water of low temperature.

The heat exchange effectiveness  $\epsilon_{\text{AC}}$  is modelled as a function of the air mass flow  $\Phi_{\text{CAC}}$  through the air cooler based on the theory of the effectiveness of a counter flow heat exchangers, as shown in Eq. (B.8).

$$\epsilon_{\text{AC}} = \frac{1 - \exp \left[ -a \cdot (\Phi_{\text{CAC}}^*)^{-0.2} \cdot (1 - b \cdot \Phi_{\text{CAC}}^*) \right]}{1 - b \cdot \Phi_{\text{CAC}}^* \cdot \exp \left[ -a \cdot (\Phi_{\text{CAC}}^*)^{-0.2} \cdot (1 - b \cdot \Phi_{\text{CAC}}^*) \right]} \quad (0 \le b \le 1) \quad (\text{B.8})$$

with,

$$a = \begin{cases} \frac{\ln \left( \frac{1 - \epsilon_{\text{AC,nom}}}{1 - b \cdot \epsilon_{\text{AC,nom}}} \right)}{b - 1} & (0 \le b < 1) \\ \frac{\epsilon_{\text{AC,nom}}}{1 - \epsilon_{\text{AC,nom}}} & (b = 1) \end{cases} \quad (\text{B.9})$$

Where,  $a$  and  $b$  are constants;  $\epsilon_{\text{AC,nom}}$  is the heat exchange effectiveness at the nominal condition; and  $\Phi_{\text{CAC}}^*$  is the normalised air mass flow through the cooler as shown in Eq. (B.10).

$$\Phi_{\text{CAC}}^* = \frac{\Phi_{\text{CAC}}}{\Phi_{\text{CAC,nom}}} \quad (\text{B.10})$$

Where,  $\Phi_{\text{CAC,nom}}$  is the air mass flow through the cooler at the nominal operating condition.

## B.3 Auxiliary blower and non-return valve models.

The auxiliary blower is located in parallel with the non-return valve between the charged air cooler and the inlet receiver. The blower will assist the air supply when the turbocharger is not capable of delivering sufficient air at low engine loads (Yum et al., 2017). During engine operations, when the scavenging pressure drops below a pre-set pressure (corresponding to an engine load of approximately 25–35%) the blower will start and continue to run until the scavenging pressure exceeds a certain value higher than the pre-set pressure (corresponding to an engine load of approximately 30–40%) resulting in an appropriate hysteresis (MAN, 2014b). The closing and opening of the non-return valve are automatically controlled by the pressures at two sides of the valve, i.e., the pressures at the air cooler outlet and in the inlet receiver. When the blower is not in operation, the air cooler outlet pressure is higher than the inlet receiver pressure and the valve will be open, so, the air flow will enter into the inlet receiver through the valve; otherwise, the valve is closed and the air flow will enter into the inlet receiver through the blower. The auxiliary blower is modelled

as a 'fixed speed compressor' using the same model as that of the compressor. It is assumed that the blower will operate at only two speeds, i.e., nominal speed ('run') and zero speed ('stop') and the transient processes between 'run' and 'stop' has been neglected. The non-return valve is modelled as a 'flow resistance' element with pressure ratio across the valve as the input and mass flow through the valve as the output.

## B.4 Exhaust valve temperature model.

In (Grimmelius and Stapersma, 2000), a model of the exhaust valve temperature for four-stroke diesel engines has been derived from first principles. In this paper, the model of the exhaust valve temperature for two-stroke diesel engines is upgraded from that for four-stroke diesel engines introduced in (Grimmelius and Stapersma, 2000) taking the differences between the gas exchange processes of two-stroke and four-stroke diesel engines into account. It is assumed that the heating of the exhaust valve of the two-stroke engine happens during the blowdown process and the cooling of the exhaust valve happens in the second stage of the scavenging process and the expelling process. The exhaust valve temperature is calculated by Eq. (B.11). Note that, the exhaust valve temperature calculated by Eq. (B.12) is in effect the average temperature over the engine cycle weighted by the heating and cooling effects.

$$T_{ev} = \frac{T_6 + r \cdot T_{sc-in}}{1 + r} \quad (B.11)$$

$$r = \begin{cases} s^{0.8} \cdot \left( \frac{T_{sc-in}}{T_6} \right)^{0.25} \cdot \left( \frac{EC-IC}{IO-EO} \right)^{0.2} & t_{sc,r} < t_{sc,r,I} \\ s^{0.8} \cdot \left( \frac{T_{sc-in}}{T_6} \right)^{0.25} \cdot \left\{ \frac{EC - \left[ (IC-IO) \cdot \frac{t_{sc,r,I}}{t_{sc,r}} + IO \right]}{IO-EO} \right\}^{0.2} & t_{sc,r} \ge t_{sc,r,I} \end{cases} \quad (B.12)$$

Where,  $s$  is the slip factor of the engine;  $t_{sc,r}$  is the relative scavenging time;  $t_{sc,r,I}$  is the relative time of first stage of the scavenging process.

## B.5 Engine mechanical and heat losses models.

In the MVFPP engine model, the engine mechanical losses are modelled as a frictional mean effective pressure using the structure of the Chen & Flynn model (Chen and Flynn, 1965) with adaptable constants, while the engine heat losses during combustion are modelled using the Woschni's model (Woschni, 1967) at one point in the Seiliger cycle, i.e. point 4, with a correction factor to allow for the possible error of this simplification. The heat losses during compression and expansion are allowed for by the polytopic exponents in the Seiliger stages 1–2 and 5–6.

# References

- Baldi, F., Theotokatos, G., Andersson, K., 2015. Development of a combined mean value–zero dimensional model and application for a large marine four-stroke diesel engine simulation. Appl. Energy 154, 402–415.
- Barton, P.I., 1992. The Modelling and Simulation of Combined Discrete/Continuous Processes. Imperial College of Science, Technology and Medicine, London.
- Cagin, S., Fischer, X., Delacourt, E., Bourabaa, N., Morin, C., Coutellier, D., Carré, B., Loumé, S., 2016. A new reduced model of scavenging to optimize cylinder design. Simulation 92 (6), 507–520.
- Carlton, J., Aldwinke, J., Anderson, J., 2013. Future Ship Powering Options: Exploring Alternative Methods of Ship Propulsion. Royal Academy of Engineering, London.
- Carlton, J.S., 2019. Marine Propellers and Propulsion, fourth ed. Butterworth-Heinemann, Kidlington, Oxford.
- Chen, S.K., Flynn, P.F., 1965. Development of a single cylinder compression ignition research engine. SAE Technical Paper, 650733.
- Colonna, P., van Putten, H., 2007. Dynamic modeling of steam power cycles.: Part I—modeling paradigm and validation. Appl. Therm. Eng. 27 (2), 467–480.
- Dang, J., Van den Boom, H., Ligtelijn, J.T., 2013. The Wageningen C-And D-Series Propellers. 12th International Conference on Fast Sea Transportation FAST2013, Amsterdam, The Netherlands.
- Ding, Y., 2011. Characterising Combustion in Diesel Engines Using Parameterised Finite Stage Cylinder Process Models. Delft University of Technology.
- Ding, Y., Li, J., Xiang, L., Zhang, Y., 2019. Two-zone simulation modeling of gas exchange process of super-long-stroke low-speed diesel engine (in Chinese). J. Harbin Eng. Univ. 40 (1), 210–216.
- Foteinos, M.I., Papazoglou, A., Kyrtatos, N.P., Stamatelos, A., Zogou, O., Stamatellou, A., 2019. A three-zone scavenging model for large two-stroke uniflow marine engines using results from CFD scavenging simulations. Energies 12 (9), 1719.
- Geertsma, R.D., Negenborn, R.R., Visser, K., Loonstijn, M.A., Hopman, J.J., 2017. Pitch control for ships with diesel mechanical and hybrid propulsion: modelling, validation and performance quantification. Appl. Energy 206, 1609–1631.
- Geertsma, R.D., Visser, K., Negenborn, R.R., 2018. Adaptive pitch control for ships with diesel mechanical and hybrid propulsion. Appl. Energy 228, 2490–2509.
- Georgescu, I., Stapersma, D., Mestemaker, B., 2016. Dynamic Behaviour of Gas and Dual-Fuel Engines: Using Models and Simulations to Aid System Integration. CIMAC Congress 2016. Finland, Helsinki.
- Grimmelius, H., Mesbahi, E., Schulten, P., Stapersma, D., 2007. The Use of Diesel Engine Simulation Models in Ship Propulsion Plant Design and Operation. CIMAC Congress, Vienna.
- Grimmelius, H.T., Stapersma, D., 2000. Control Optimisation and Load Prediction for Marine Diesel Engines Using a Mean Value Simulation Model. ENSUS Conference 2000, Newcastle upon Tyne.
- Guan, C., Theotokatos, G., Zhou, P., Chen, H., 2014. Computational investigation of a large container propulsion engine operation at slow steaming conditions. Appl. Energy 130, 370–383.
- Hangos, K., Cameron, I., 2001. Process Modelling and Model Analysis. Academic Press, London, UK.
- He, F., Wei, J., 2017. Numerical Simulation of Scavenging Process of Large 2-Stroke Marine Diesel Engine. 2nd International Conference on Automatic Control and Information Engineering. ICACIE 2017).
- Holt, P., Nielsen, U.D., 2021. Preliminary assessment of increased main engine load as a consequence of added wave resistance in the light of minimum propulsion power. Appl. Ocean Res. 108, 102543.
- IMO, 2020. Fourth IMO GHG Study 2020 - Final Report. International Maritime Organization (IMO), London.
- Klein Woud, H., Stapersma, D., 2002. Design of Propulsion and Electric Power Generation Systems. IMarEST, Institute of Marine Engineering, Science and Technology, London.
- Liu, H., Lu, L., Wang, Z., 2014. Evaluation analysis of scavenging process of two-stroke marine diesel engine by experiment and simulation. J. Therm. Sci. Technol. 9 (2), T12.
- MAN, 2014a. MAN B&W S35ME-B9.3-TII Project Guide - Electronically Controlled Two-Stroke Engines with Camshaft Controlled Exhaust Valves. MAN Diesel & Turbo, Copenhagen, Denmark.
- MAN, 2014b. MAN B&W S35ME-B9.5-TII Project Guide - Electronically Controlled Two-Stroke Engines.
- MAN, 2018. Basic Principles of Ship Propulsion. MAN Diesel & Turbo, Copenhagen, Denmark.
- Nanda, K.S., Jia, B., Smallbone, A., Roskilly, P.A., 2017. Fundamental analysis of thermal overload in diesel engines: hypothesis and validation. Energies 10 (3), 329.
- Payri, F., Olmeda, P., Martín, J., García, A., 2011. A complete 0D thermodynamic predictive model for direct injection diesel engines. Appl. Energy 88 (12), 4632–4641.
- Sapra, H., Godjevac, M., De Vos, P., Van Sluijs, W., Linden, Y., Visser, K., 2020. Hydrogen-natural gas combustion in a marine lean-burn SI engine: a comparative analysis of seiliger and double Wiebe function-based zero-dimensional modelling. Energy Convers. Manag. 207, 112494.
- Sapra, H., Godjevac, M., Visser, K., Stapersma, D., Dijkstra, C., 2017. Experimental and simulation-based investigations of marine diesel engine performance against static back pressure. Appl. Energy 204, 78–92.
- Schulten, P., 2005. The Interaction between Diesel Engines, Ship and Propellers during Manoeuvring. Delft University of Technology.
- Schulten, P.J.M., Stapersma, D., 2003. Mean value modeling of the gas exchange of a 4-stroke diesel engine for use in powertrain applications. SAE Technical Paper. No. 2003-01-0219.
- Seiliger, M., 1922. Graphische Thermodynamik Und Berechnen Der Verbrennungs-Maschinen Und Turbinen. Julius Springer, Berlin.
- Seiliger, M., 1926. Die Hochleistungs-Dieselmotoren. Julius Springer, Berlin.
- Sher, E., 1990. Scavenging the two-stroke engine. Prog. Energy Combust. Sci. 16 (2), 95–124.
- Shi, W., 2013. Dynamics of Energy System Behaviour and Emissions of Trailingsuction Hopper Dredgers. Delft University of Technology, Delft, the Netherlands.
- Stapersma, D., 1999. Scavenge Model for Diesel Engine Simulation: Simultaneous Cooling and Cleaning in Perfect Mixing Element (Internal Report). Royal Netherlands Naval College.
- Stapersma, D., 2008. The Influence of Turbo Charger Matching on Propulsion Performance. INEC 2008, Embracing the Future. HT Grimelius, Hamburg, Germany, 1–3 April 2008.
- Stapersma, D., 2010a. Diesel Engines - a Fundamental Approach to Performance

- Analysis, Turbocharging, Combustion, Emissions and Heat Transfer. Performance Analysis, Part I: Diesel Engines a - Performance Analysis and Turbocharging. Lecture Notes NLDA/TUDelft. April 2010.
- Stapersma, D., 2010b. Diesel Engines - a Fundamental Approach to Performance Analysis, Turbocharging, Combustion, Emissions and Heat Transfer. Turbocharging, Part I: Diesel Engines a - Performance Analysis and Turbocharging. Lecture Notes NLDA/TUDelft. April 2010.
- Stapersma, D., 2010c. Diesel Engines - a Fundamental Approach to Performance Analysis, Turbocharging, Combustion, Emissions and Heat Transfer. Emissions and Heat Transfer, Part II: Diesel Engines B - Combustion, Emissions and Heat Transfer. Lecture Notes NLDA/TUDelft April 2010. NLDA & Delft UT, Delft.
- Stapersma, D., 2013. A General Model for Off-Design Performance of a Single Stage Turbomachine (KIM-PFS-97-111, Issue D) (Internal Report). Delft University of Technology, Delft.
- Sui, C., de Vos, P., Stapersma, D., Visser, K., Ding, Y., 2020. Fuel consumption and emissions of ocean-going cargo ship with hybrid propulsion and different fuels over voyage. *J. Mar. Sci. Eng.* 8, 8.
- Sui, C., Song, E., Stapersma, D., Ding, Y., 2017. Mean value modelling of diesel engine combustion based on parameterized finite stage cylinder process. *Ocean Eng.* 136, 218–232.
- Sui, C., Stapersma, D., Visser, K., de Vos, P., Ding, Y., 2019. Energy effectiveness of ocean-going cargo ship under various operating conditions. *Ocean Eng.* 190, 106473.
- Thacker, B.H., Doebling, S.W., Hemez, F.M., Anderson, M.C., Pepin, J.E., Rodriguez, E.A., 2004. Concepts of Model Verification and Validation, p. 41. United States.
- Theotokatos, G., Guan, C., Chen, H., Lazakis, I., 2018. Development of an extended mean value engine model for predicting the marine two-stroke engine operation at varying settings. *Energy* 143, 533–545.
- UNCTAD, 2019. Review of Maritime Transport 2019. UNITED NATIONS PUBLICATION, Geneva.
- van Putten, H., Colonna, P., 2007. Dynamic modeling of steam power cycles: Part II – simulation of a small simple Rankine cycle system. *Appl. Therm. Eng.* 27 (14), 2566–2582.
- Woschni, G., 1967. A universally applicable equation for the instantaneous heat transfer coefficient in the internal combustion engine. SAE Technical paper.
- Yum, K.K., Taskar, B., Pedersen, E., Steen, S., 2017. Simulation of a two-stroke diesel engine for propulsion in waves. *Int. J. Naval Architecture Ocean Eng.* 9 (4), 351–372.