

## Full Length Article

![Check for updates button](4f4b52340aaccb1bcf733468dca9ee03_img.jpg)

Check for updates button

# Physics-constrained hybrid framework for CO<sub>2</sub>-ECBM prediction and optimization in fractured coal reservoirs: A tSEDFM-ATHM-LSTM-BO approach

Tao Zhang<sup>a,\*</sup>, Jianchun Guo<sup>a,\*</sup>, Jie Zeng<sup>a</sup>, Lilong Wang<sup>b</sup>, Zhihong Zhao<sup>a</sup>, Fanhui Zeng<sup>a</sup>, Cong Lu<sup>a</sup>

<sup>a</sup> National Key Laboratory of Oil and Gas Reservoir Geology and Exploitation, Southwest Petroleum University, Xindu Avenue, Chengdu, China

<sup>b</sup> CBM and Gas Storage Business Department of Huabei Oilfield Company, PetroChina, Renqiu Hebei, China

## ARTICLE INFO

### Keywords:

CO<sub>2</sub> sequestration  
Transient EDFM  
Multi-filed coupling  
CO<sub>2</sub>-ECBM  
LSTM-BO

## ABSTRACT

CO<sub>2</sub> injection into coal reservoirs offers dual benefits for enhancing coalbed methane recovery (ECBM) and CO<sub>2</sub> sequestration. However, fracture networks and multi-physics interactions such as CO<sub>2</sub>-CH<sub>4</sub> competitive adsorption and thermal-hydro-mechanical coupling, pose computational challenges that hinder efficient simulation. To overcome these challenges, this study proposes a physics-informed hybrid framework integrating the transient-source-function-based embedded discrete fracture model (tSEDFM), adsorption-thermo-hydro-mechanical coupling (ATHM), and long short-term memory (LSTM) neural networks to rapidly predict CH<sub>4</sub> production and CO<sub>2</sub> sequestration. The tSEDFM-ATHM model is solved using the MATLAB Reservoir Simulation Toolbox (MRST). Its reliability is validated against CO<sub>2</sub>-CH<sub>4</sub> simulation and experiments. The LSTM predictions trained by the proposed model achieve an accuracy rate ( $R^2$ ) of over 96 %. On the above basis, the CO<sub>2</sub>-ECBM simulation considering various mechanisms can be fast and robust applied. The sensitivity of key parameters is also discussed. Using the hybrid framework, the optimal CO<sub>2</sub> injection schedule (injection rate 500 m<sup>3</sup>/d and injection period is 20 days) for the well group in the Qinshui basin was obtained via Bayesian optimization. This study provides a fast and practical method for simulation and evaluation of integrated CO<sub>2</sub> sequestration and ECBM.

## 1. Introduction

With the increasing global demand for clean energy and the push toward carbon neutrality [1,2], coalbed methane (CBM) has emerged as a critical unconventional energy resource [3]. The integrated CO<sub>2</sub> sequestration and ECBM provide a practical way to achieve the goal of clean energy extraction and carbon neutrality. Conventional CBM recovery methods generally suffer from low extraction efficiency. CO<sub>2</sub>-enhanced coalbed methane recovery (CO<sub>2</sub>-ECBM), which involves CO<sub>2</sub> injection into coal seams and CH<sub>4</sub> extraction (see Fig. 1), offers dual benefits by enhancing CH<sub>4</sub> recovery and achieving CO<sub>2</sub> geological sequestration. CO<sub>2</sub>-ECBM has been treated as a promising technology for sustainable energy development and carbon emission reduction [4].

Despite the significant potential benefits of CO<sub>2</sub>-ECBM technology, its field applications and accurate prediction of the injection process face a lot of challenges. First, the CO<sub>2</sub>-ECBM process involves coupled

multiphysics processes within the coal reservoirs [5,6], including adsorption [7], thermal effects [8], mechanical deformation [9], and hydraulic effects [10,11]. The interactions among these physical and chemical fields have substantial impacts on gas transport and coal properties. For instance, CO<sub>2</sub> adsorption releases heat, leading to localized temperature increases, which in turn affects coal mechanical properties and permeability. Meanwhile, the CO<sub>2</sub>-injection-induced stress and swelling strain changes cause fracture opening or closure [12]. Besides, coal matrix deformation further influences gas transport and permeability evolution. Specifically, the CO<sub>2</sub>-ECBM process undergoes complexity permeability evolution due to the superposition of multiple strain changes generated from thermal, mechanical, and CO<sub>2</sub>-methane competitive adsorption effects [13]. CO<sub>2</sub> adsorption-induced coal matrix swelling and CH<sub>4</sub> desorption-induced shrinkage significantly alter the pore size of the coals [14]. Additionally, during the long-term gas injection and production processes, coal creep deformation

\* Corresponding authors.

E-mail addresses: [zhangtao100610@163.com](mailto:zhangtao100610@163.com) (T. Zhang), [guojianchun@vip.163.com](mailto:guojianchun@vip.163.com) (J. Guo).

![Schematic diagram of CO2-ECBM process showing surface equipment, subsurface reservoir, and microscopic mechanisms.](aa9e46d6f962be5cebcbb5c654c9b13e_img.jpg)

The diagram illustrates the CO<sub>2</sub>-ECBM (Enhanced Coalbed Methane) process across three scales:

- Surface Operations:** Includes a **CO<sub>2</sub> Injection pump** and a **CO<sub>2</sub> Tank truck** for injection, and **CH<sub>4</sub> Production well** for extraction.
- Subsurface Reservoir:** Shows the **CO<sub>2</sub> enrichment** and **CO<sub>2</sub>-CH<sub>4</sub> mixture** zones. The process involves **CO<sub>2</sub>-CH<sub>4</sub> Flooding** and **Competitive adsorption**.
- Microscopic Mechanisms:** Depicts the interaction between **Injected CO<sub>2</sub>** and **Adsorbed CH<sub>4</sub>** on coal. The process starts with an **Initial state**, followed by **Competitive adsorption** leading to **Local swelling** and **Permeability loss**. Subsequent **Competitive adsorption + Flooding** leads to **Global swelling** and **Permeability enhancement**.

Schematic diagram of CO2-ECBM process showing surface equipment, subsurface reservoir, and microscopic mechanisms.

Fig. 1. Schematic diagram of CO<sub>2</sub>-ECBM.

further results in a permeability loss [15]. These complexities highlight the need for advanced modeling approaches to accurately describe the inherent multi-physical interactions and dynamic behaviors in CO<sub>2</sub>-ECBM. Extensive research has been conducted to clarify and incorporate the coupled multiphysics processes and permeability evolution in the CO<sub>2</sub>-ECBM processes. Sang and Fang [8] established an adsorption-thermo-hydro-mechanical (ATHM) coupling framework to investigate the influence of thermal and mechanical effects on coal permeability. Their results showed that under varying injection scenarios, coal permeability changes in significantly different ways. Zhu [16] proposes a CO<sub>2</sub> phase-transition-based permeability model, revealing the U-shaped permeability evolution during Sc-CO<sub>2</sub> injection and the trade-offs of stepwise pressure-raising for CO<sub>2</sub> storage. Their research also provides insights for deep coal reservoirs sequestration. Moreover, Liu and Sang [17] put forward a comprehensive adsorption-hydro-thermo-mechanical-chemical (AHTMC) coupled model to explore geochemical ion interactions in formation water and the effect of mineral dissolution on CO<sub>2</sub>-ECBM. However, most prior studies used dual-porosity models for idealized cleat (microfracture) and matrix block systems. This leads to the ignorance of multi-scale fracture distribution's influence and the lack of sufficient consideration of transient mass and heat transfer from matrix to fractures. Furthermore, Liu's [18] findings indicate that fracture systems also serve as effective space for CO<sub>2</sub> storage, highlighting the need of more detailed investigations on fracture-dominated fluid transport processes. The introduction of EDFM [19] offers a promising approach to more realistically describe the fracture system geometry. The EDFM and pEDFM [20] solvers in the MRST have been widely

applied in the simulation of shale gas production and enhanced geothermal systems. However, the steady-state flow assumption in the classical EDFM models will generate errors in matrix-fracture interporosity mass and heat transfer. To address this limitation, Chen [21] and Zhang [22] proposed two transient EDFM models, which are called the AEDFM and tSEDFM. They can effectively address the transient mass transfer and minimize the errors, demonstrating their strong potential for improving CO<sub>2</sub>-ECBM simulation accuracy and efficiency. Meanwhile, given that CO<sub>2</sub>-ECBM is a typical multiphase flow process, incorporating relative permeability corrections into the EDFM framework is essential for accurately characterizing the complex interactions among CO<sub>2</sub>, CH<sub>4</sub>, and water in fractured coals.

Indeed, the computational efficiency in CO<sub>2</sub>-ECBM numerical simulations is frequently suboptimal, particularly in coupled multiphysics simulation. The grid density increment, coupled with the intricate evolution of fracture network fluid transport mechanisms, significantly increases the computational demands. This hinders long-term production simulations. In response to this challenge, some recent research applied deep learning to predict and optimize the simulation outcomes [23,24]. The long short-term memory (LSTM) approaches [25] that capitalize on the periodic and trending characteristics of CO<sub>2</sub>-ECBM were used to yield enhanced prediction ability. Despite their obvious application potential, these deep learning approaches often lack the capacity to provide a robust and explicative framework for the multiphysics process. Therefore, an improved approach that combines deep learning techniques with numerical simulators through incorporation of pertinent physical constraints is proposed to further enhance their

![Figure 2: Coupled processes of the ATHM model. The diagram shows four interconnected fields: Hydraulic Field (blue circle), Mechanical Field (orange circle), Thermal Field (red circle), and Adsorption Field (green circle). Arrows indicate the direction of influence between them. From Hydraulic to Mechanical: 'Enhanced flooding due to increased desorbed gas', 'Enhanced desorption due to increased pressure drop', 'Enhanced flooding due to increased permeability', 'Multi-strain induced permeability evolution'. From Hydraulic to Thermal: 'Thermal induced viscosity and density evolution', 'Convective enhanced thermal energy exchange'. From Mechanical to Hydraulic: 'Competitive adsorption', 'swelling strain'. From Mechanical to Thermal: 'Thermal induced desorption', 'Enhanced thermal convection due to increased permeability'. From Thermal to Hydraulic: 'Thermal induced desorption'. From Thermal to Adsorption: 'Competitive adsorption thermal energy evolution'. From Adsorption to Hydraulic: 'Competitive adsorption thermal energy evolution'.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

Figure 2: Coupled processes of the ATHM model. The diagram shows four interconnected fields: Hydraulic Field (blue circle), Mechanical Field (orange circle), Thermal Field (red circle), and Adsorption Field (green circle). Arrows indicate the direction of influence between them. From Hydraulic to Mechanical: 'Enhanced flooding due to increased desorbed gas', 'Enhanced desorption due to increased pressure drop', 'Enhanced flooding due to increased permeability', 'Multi-strain induced permeability evolution'. From Hydraulic to Thermal: 'Thermal induced viscosity and density evolution', 'Convective enhanced thermal energy exchange'. From Mechanical to Hydraulic: 'Competitive adsorption', 'swelling strain'. From Mechanical to Thermal: 'Thermal induced desorption', 'Enhanced thermal convection due to increased permeability'. From Thermal to Hydraulic: 'Thermal induced desorption'. From Thermal to Adsorption: 'Competitive adsorption thermal energy evolution'. From Adsorption to Hydraulic: 'Competitive adsorption thermal energy evolution'.

Fig. 2. Coupled processes of the ATHM model.

prediction accuracy and computational efficiency [26]. Li et al. [27] gives a data-driven BiGRU-DHNN for predicting long-term CBM production. Sagheer et al. [28] applied the deep long-short term memory (DLSTM) approach and successfully conducted time-dependent forecasting of oil production. Palash et al. [27] demonstrated the capability of the LSTM networks in accurate calculation of oil, gas, and water production. This finding suggests that LSTM-based methodologies hold significant promise for application in the quantitative analysis of unconventional reservoir dynamics, such as shale formations and other tight geological structures [29]. While the LSTM-based models capture temporal dependencies in monitoring time data, their purely data-driven nature fails to embed physical constraints, leading to physically implausible predictions under complex multiphase interactions. Chen et al. [30] achieved the rapid prediction of CO<sub>2</sub> huff-n-puff processes in shale gas reservoirs through the combined application of numerical simulation methods and deep learning algorithms. Yan and Zeisha [31–34] developed pioneering hybrid frameworks integrating physical constraints. Their work demonstrates excellent performance in carbon sequestration prediction and enhanced geothermal system (EGS) optimization. Notably, their ED-ConvLSTM [31] and CNN-transformer [32] surrogate models enable fast simulation of CO<sub>2</sub> plume dynamics. However, existing fast prediction of CO<sub>2</sub>-ECBM is mainly based on data-driven deep learning methods. These methods are lack of appropriate physical constraints [35] or simply consider micro-scale competitive adsorption [36]. The physics-constrained framework with numerical methods explicitly integrates domain knowledge (e.g., conservation laws or governing equations) to ensure mechanistic interpretability and bridge the gap between data-driven performance and explainable scientific reasoning. Therefore, it is important to establish a physical-constraint-based intelligent prediction and optimization framework for CH<sub>4</sub> production and CO<sub>2</sub> sequestration in the CO<sub>2</sub>-ECBM process to improve the applicability at the field scale.

This study proposes a hybrid physical-constraint-based framework combining the transient-source-function-based embedded discrete fracture model (tSEDFM) with adsorption-thermo-hydro-mechanical coupling (ATHM) (see Fig. 2) and LSTM neural networks to predict CH<sub>4</sub> production dynamics and CO<sub>2</sub> sequestration capacity. The proposed tSEDFM-ATHM can accurately simulate multiple fluid flow and rock deformation processes during CO<sub>2</sub>-ECBM and improve the interpretable time series for LSTM to train. Meanwhile, after training, long short term memory and Bayesian optimization (LSTM-BO) can replace the original

numerical model to achieve rapid prediction and optimization. This work offers a solid foundation for the field applications of CO<sub>2</sub>-ECBM. provides strong support for achieving the goal of carbon peaking and carbon neutrality, as well as relatively clean energy supply.

## 2. Methodology

### 2.1. Modified tSEDFM for fractured coal reservoirs

To accurately address mass and heat transfer in fractured coal reservoirs, we proposed the tSEDFM for characterizing the transient matrix-fracture flow and incorporating the spatial distribution of the fracture system. According to previously mentioned framework, this study introduces relative permeability functions to describe multiphase flow dynamics within fractures during CO<sub>2</sub>-ECBM.

Based on the tSEDFM, the fracture distribution was characterized by stochastic discrete fracture network model [22], the transient mass exchange between fracture-matrix and fracture-fracture systems can be formulated as:

$$Q_i^{m-f} = T_{g,i}^{m-f} \Delta p_{g,i}^{m-f} \quad (1)$$

$$Q_i^{f-f} = T_{g,i}^{f-f} \Delta p_{g,i}^{f-f} \quad (2)$$

$$T_{g,i}^{m-f} = -T_{g,i}^{f-m} = \frac{T_{g,i}^m T_{g,i}^f}{T_{g,i}^m + T_{g,i}^f} \quad (3)$$

$$T_{g,i}^{f-f} = \frac{\prod_{j=1}^{k} T_{g,i,j}^f}{\sum_{j=1}^{k} T_{g,i,j}^f} \quad (4)$$

where  $Q_i^{m-f}$  and  $Q_i^{f-f}$  are the matrix-fracture and fracture-fracture mass exchange rates, m<sup>3</sup>/s, respectively;  $\Delta p_{g,i}^{m-f}$  and  $\Delta p_{g,i}^{f-f}$  are the matrix-fracture and fracture-fracture pressure differences, MPa;  $T_{g,i}^{m-f}$  and  $T_{g,i}^{f-m}$  are the matrix-fracture transient transmissibility, m<sup>3</sup>/(s·MPa);  $T_{g,i}^m$  and  $T_{g,i}^f$  are the matrix and fracture transient transmissibility, m<sup>3</sup>/(s·MPa), respectively.

Here,  $i$  represents the gas composition,  $i = 1$  for CH<sub>4</sub>, and  $i = 2$  for CO<sub>2</sub>.

The matrix and fracture transient transmissibility terms can be written as [22]:

$$T_{g,i}^m = \frac{4\pi k_m k_{r,g,i} h}{\mu_{g,i} B_{g,i}} \left[ -\text{Ei} \left( -\frac{d_{\text{NNC}}^2}{4\eta_{g,i} t} \right) \right] \quad (5)$$

$$T_{g,i}^f = \frac{4\pi k_f k_{r,g,i} w_f}{\mu_{g,i} B_{g,i} \sqrt{\eta_{g,i} t} \text{erf} \left[ \frac{d_{\text{NNC}}}{4\eta_{g,i} t} \right]} \quad (6)$$

where  $k_m$  is the coal matrix permeability, mD;  $k_f$  is the fracture permeability, mD;  $k_{r,g,i}$  is the gas-phase relative permeability, dimensionless;  $d_{\text{NNC}}$  is the distance of the non-neighboring connection, m;  $h$  is the grid height, m;  $w_f$  is the fracture width, m;  $\mu_{g,i}$  is the gas viscosity, mPa·s;  $B_{g,i}$  is the gas volume factor, dimensionless;  $\eta_{g,i} = k_m / \phi_m \mu_{g,i} c_m$  is pressure transmitting coefficient, m<sup>2</sup>/s;  $\phi_m$  is the coal porosity, dimensionless;  $c_m$  is the matrix compressibility, 1/MPa; and  $t$  is the simulation time, s.

### 2.2. Coupled multi-field ATHM model

#### 2.2.1. Governing equation of the adsorption field

The coal matrix is the major porous media for gas storage. The binary gases adsorption of CH<sub>4</sub> and CO<sub>2</sub> in the coal matrix can be expressed by the extended Langmuir equation [17], and the non-Langmuir behavior

was ignored. The gas adsorption volume and strain of coal can be defined as:

$$Q_{g,i}^s = \frac{V_{L,i} p_{g,i}^m}{p_{L,i} \left( 1 + \sum_{i=1}^2 \frac{p_{g,i}^m}{p_{L,i}} \right)} \exp \left[ \frac{d_2 (T - T_0)}{1 + d_1 p_{g,i}^m} \right] \quad (7)$$

$$\varepsilon_s = \sum_{i=1}^2 \frac{\varepsilon_{L,i} p_{g,i}^m}{p_{L,i} \left( 1 + \sum_{i=1}^2 \frac{p_{g,i}^m}{p_{L,i}} \right)} \exp \left[ \frac{d_2 (T - T_0)}{1 + d_1 p_{g,i}^m} \right] \quad (8)$$

where  $Q_{g,i}^s$  is the adsorption content,  $\text{m}^3/\text{t}$ ;  $V_{L,i}$  is the Langmuir volume,  $\text{m}^3/\text{t}$ ;  $\varepsilon_s$  is adsorption-induced swelling strain, dimensionless;  $\varepsilon_{L,i}$  is the Langmuir strain constant, dimensionless;  $p_{L,i}$  is the Langmuir pressure,  $\text{MPa}$ ;  $p_{g,i}^m$  is the matrix pressure,  $\text{MPa}$ ;  $T$  is the coal reservoir temperature,  $\text{K}$ ;  $T_0$  is the initial temperature of the coal reservoir,  $\text{K}$ ;  $d_1$  is the pressure coefficient,  $1/\text{MPa}$ ; and  $d_2$  is the temperature coefficient,  $1/\text{K}$ .

In particular, the physical assumptions in the multi-field ATHM modeling of  $\text{CO}_2$ -ECBM are consistent with Liu's work, please see details in the reference [17].

#### 2.2.2. Governing equation of the temperature field

During the  $\text{CO}_2$ -ECBM process, accounting for binary gas competitive adsorption and thermal expansion in coal seams, the governing equations of the temperature field can be expressed based on heat conservation principles as follows [8,37]:

$$\frac{\partial((\rho C_p)_T T)}{\partial t} + \eta_T \nabla T - \nabla \cdot (\lambda_T T) = K \alpha_T \frac{\partial \varepsilon_s}{\partial t} + \sum_{i=1}^2 q_{T,i} \frac{\rho_i \rho_{g,i}}{M_{g,i}} \frac{\partial Q_{g,i}^s}{\partial t} \quad (9)$$

$$(\rho C_p)_T = (1 - \phi_m) \rho_c C_c + \sum_{i=1}^2 \phi_m s_{g,i} \rho_{g,i} C_{g,i} \quad (10)$$

$$\eta_T = - \sum_{i=1}^2 s_{g,i} \rho_{g,i} C_{g,i} \frac{k_i k_{r,g,i}}{B_{g,i} \mu_{g,i}} \nabla p_{g,i}^f - \sum_{i=1}^2 s_{g,i} \rho_{g,i} C_{g,i} \frac{k_m k_{r,g,i}}{B_{g,i} \mu_{g,i}} \nabla p_{g,i}^m \quad (11)$$

$$\lambda_T = (1 - \phi_m) \lambda_c + \sum_{i=1}^2 \phi_m s_{g,i} \lambda_{g,i} \quad (12)$$

where  $(\rho C_p)_T$  is the effective specific heat capacity of the coal reservoir,  $\text{J}/(\text{m}^3 \cdot \text{K})$ ;  $\eta_T$  is the effective heat convective coefficient,  $\text{J}/(\text{m}^2 \cdot \text{s})$ ;  $\lambda_T$  is the effective thermal conductivity,  $\text{W}/(\text{m} \cdot \text{K})$ ;  $q_{T,i}$  is the adsorption heat of the gas component  $i$ ,  $\text{J}/\text{mol}$ ;  $\rho_c$  is the coal density,  $\text{kg}/\text{m}^3$ ;  $\rho_{g,i}$  is the density of gas component  $i$ ,  $\text{kg}/\text{m}^3$ ;  $M_{g,i}$  is the molar mass of gas component  $i$ ,  $\text{kg}/\text{mol}$ ;  $\alpha_T$  is the thermal expansion coefficient,  $1/\text{K}$ ;  $K$  is the coal bulk modulus,  $\text{GPa}$ ;  $C_c$  and  $C_{g,i}$  are the specific heat capacities of coal and gas component  $i$ ,  $\text{J}/(\text{kg} \cdot \text{K})$ ;  $s_{g,i}$  are the saturation of gas component  $i$ , dimensionless;  $p_{g,i}^f$  is partial fracture pressure of gas component  $i$ , respectively,  $\text{MPa}$ ;  $\lambda_c$  and  $\lambda_{g,i}$  are the heat conduction coefficients of coal and gas component  $i$ ,  $\text{W}/(\text{m} \cdot \text{K})$ .

Specifically, the transient convective heat transfer is denoted by the convection term in Eq. (11) and realized via the application of the tSEDFM to fracture system flow.

#### 2.2.3. Governing equation of the hydraulic field

The  $\text{CO}_2$ -ECBM process in fractured coal reservoirs includes two key mechanisms: competitive adsorption and dynamic flooding. Here, the fracture propagation was ignored during the injection and production processes. Incorporating transient fracture-matrix flow interactions, the flux exchange is computed via a modified tSEDFM [22], while the two-phase flow governing equations within the coal matrix and fractures are expressed as:

$$\frac{\partial}{\partial t} \left( \frac{\phi_m s_{g,i}^m}{B_{g,i}} \right) = \nabla \cdot \frac{k_m k_{r,g,i}}{B_{g,i} \mu_{g,i}} \nabla p_{g,i}^m + \sum_{i=1}^2 Q_{g,i}^s + \sum_{k=1}^{n_f} Q_{i,k}^{m-f} \quad (13)$$

$$\frac{\partial}{\partial t} \left( \frac{\phi_m s_{g,i}^f}{B_{g,i}} \right) = \nabla \cdot \frac{k_f k_{r,g,i}}{B_{g,i} \mu_{g,i}} \nabla p_{g,i}^f + \sum_{k=1}^{n_f} Q_{i,k}^{f-f} + \sum_{k=1}^{n_f} Q_{i,k}^{m-f} \quad (14)$$

By neglecting the water phase flow in coal reservoirs, the Brooks-Corey and X models are adopted to characterize the relative permeability curves for  $\text{CO}_2$  displacing  $\text{CH}_4$  in both matrix and fracture systems, as shown below [38,39]:

$$k_{r,g,i} = k_{r,g,i}^{\max} \left[ \frac{s_{g,i} - s_{g,i}^r}{1 - s_{g,i}^r - s_{g,i}^r} \right]^{n_{g,i}} \quad (15)$$

$$k_{r,g,i} = k_{r,g,i}^{\max} s_{g,i} \quad (16)$$

The capillary pressure of two-phase flow is as follows:

$$p_c = p_{g,1} - p_{g,2} = p_{c0} \left[ \frac{s_{g,1} - s_{g,1}^r}{1 - s_{g,1}^r - s_{g,2}^r} \right]^{n_{g,1}} \quad (17)$$

where  $k_{r,g,i}^{\max}$  is the maximum relative permeability of gas component  $i$ , dimensionless;  $s_{g,i}$  is the saturations of the residual gas component  $i$ , dimensionless;  $p_c$  is the capillary pressure,  $\text{MPa}$ ;  $p_{c0}$  is the initial capillary pressure,  $\text{MPa}$ ; and  $n_{g,i}$  is the relative permeability index, dimensionless.

#### 2.2.4. Governing equation of the mechanical field

The coal reservoirs is simplified as an elastic medium composed of matrix and fracture domains. Its deformation is governed by binary-gas-competitive-adsorption-induced swelling, effective stress, and reservoir temperature. The equivalent stress-strain constitutive equation can be expressed as: [7,17,22]

$$\Delta \varepsilon_{ij} = \frac{\Delta \sigma_{ij}}{2G} - \left( \frac{1}{6G} - \frac{1}{9K} \right) \Delta \sigma_{ii} \delta_{ij} + \frac{\alpha}{3K} \Delta p_{ij} + \frac{(1 - \phi_m)(1 - f)}{3} \Delta \varepsilon_s \delta_{ij} + \delta_{ij} \alpha_T \Delta T_{ij} + \delta_{ij} \sum_{i=1}^2 \alpha_s Q_{g,i}^s \quad (18)$$

where  $G = E/1 - 2\nu$  is the shear modulus,  $\text{GPa}$ ;  $E$  is the Young's modulus,  $\text{GPa}$ ;  $\nu$  is the Poisson's ratio, dimensionless;  $f$  is the matrix-fracture connection coefficient, dimensionless;  $\sigma_{ii} = \sigma_{xx} + \sigma_{yy} + \sigma_{zz}$ ;  $\alpha$  is the Biot's coefficient;  $\delta_{ij}$  is the Kronecker delta function;  $\varepsilon_{ij}$  is the strain tensor, dimensionless;  $\sigma_{ij}$  is the stress tensor,  $\text{MPa}$ ; and  $T_{ij}$  is the temperature tensor,  $\text{K}$ .

The reduction and increase in effective stress during injection and production are known as the dominant driver for stress evolution. The prolonged injection-production operations under high stress conditions induce creep deformation within coals. This leads to the continuous fracture aperture evolution throughout the injection period. Under the isotropy assumption, the multi-strain governing equations for coals are be given by:

$$\begin{aligned} \Delta \varepsilon &= \sum_{i=1}^3 \Delta \varepsilon_{ii} / 3 \\ &= - \frac{\Delta \sigma_e}{3K} + \frac{(1 - \phi_m)(1 - f) \Delta \varepsilon_s}{3} + \alpha_T \Delta T + \sum_{i=1}^2 \alpha_s Q_{g,i}^s + c_f \Delta \sigma_e + \Delta \varepsilon_c \end{aligned} \quad (19)$$

The linear elastic strain term  $\Delta \sigma_e/3K$ , which can incorporate a time-dependent three-stage creep constitutive equation, allows Eq. (19) to be reformulated as [22,40]:

$$\Delta \varepsilon = -\Delta \sigma_e \left( \frac{1}{E} - \frac{1}{E_{ve}} - \frac{1}{E_{ve}} E_{r,1} \left[ -E_{ve} \left( \frac{t}{\eta_{ve}} \right)^\gamma \right] + \frac{t^\gamma E_{1,1+\gamma}(\alpha_0 t)}{\eta_{vp}^\gamma} \right) + \frac{(1-\phi_m)(1-f)\Delta \varepsilon_s}{3} + \alpha_1 T + \sum_{i=1}^{2} \alpha_s Q_{g,i}^s + c_f \Delta \sigma_e \quad (20)$$

where  $\varepsilon$  is average strain of coal, dimensionless;  $\sigma_e = \sigma - \alpha p_g$  is the effective stress, MPa;  $E_{ve}$  is the viscoelastic modulus of the coal rock, GPa;  $\gamma$  is the fractional derivative;  $\eta_{ve}$  and  $\eta_{vp}$  are the viscoelastic and viscoplastic coefficients, Pa·h $^\gamma$ ;  $\alpha_0$  is the viscosity coefficient, 0.17;  $c_f$  is the fracture compressibility, 1/MPa;  $E_{\alpha,\beta}(x)$  are the Mittag-Leffler functions,  $\alpha$  is for  $\gamma$  and 1; and  $\beta$  is for 1 and  $1 + \gamma$ .

#### 2.2.5. Permeability evolution induced by multiple strains

Porosity and permeability, as the key parameters of fluid flow in coal reservoirs, exhibit dynamic evolution behavior throughout both primary production and CO<sub>2</sub>-ECBM operations. This evolution is governed by coupled adsorption-thermo-hydro-mechanical processes, including coal deformation, CO<sub>2</sub>-CH<sub>4</sub> competitive adsorption/desorption, effective stress evolution, and reservoir temperature fluctuations.

We employ a dual-porosity medium model to incorporate both pores and microfractures within the matrix, the porosity is expressed as [17]:

$$\phi_m = \frac{1}{1 + \varepsilon} [(1 + \varepsilon_0)\phi_{m0} + \alpha(\varepsilon - \varepsilon_0)] \quad (21)$$

Based on the cubic law, permeability can be expressed as:

$$k_m = k_{m0} \left( \frac{\phi_m}{\phi_{m0}} \right)^3 \quad (22)$$

where  $\varepsilon_0$  is the initial average strain of coal, dimensionless;  $\phi_{m0}$  is the initial coal matrix porosity, dimensionless;  $k_{m0}$  is the initial coal matrix permeability, mD.

By further considering the gas rarefaction effect, Eq. (22) can be rewritten as [41]:

$$k_m = k_{m0} \left( \frac{\phi_m}{\phi_{m0}} \right)^3 (1 + \beta Kn) \left( 1 + \frac{6Kn}{1 + Kn} \right) \quad (23)$$

$$Kn = K_B T / \left( 2 \pi \left( \prod_{i=1}^{2} d_i / \sum_{i=1}^{2} d_i \right)^2 p_g^m \right) / r \quad (24)$$

$$\beta = (128/15\pi^2) \cdot \tan^{-1}(4Kn^{0.4}) \quad (25)$$

where  $Kn$  is the Knudsen number, dimensionless;  $K_B$  is the Boltzmann constant, J/K;  $d_i$  is the molecular diameter of gas component  $i$ , nm; and  $r$  is the average pore size, m.

Specifically, the permeability evolution of large-scale fractures follows a power-law relationship:

$$k_f = k_{f0} \exp(c_f \Delta \sigma_e) \quad (26)$$

where  $k_{f0}$  is the initial fracture permeability, mD;

### 2.3. CH<sub>4</sub> production and CO<sub>2</sub> sequestration

Note that the analytical solutions of the strains improve the model's solvability and couple the adsorption-thermo-hydro interactions via the permeability term, as shown in Fig. 2. Using the MRST, we integrated ad-blackoil, ad-props, CO<sub>2</sub>lab, modified hfm, geothermal module, and the user-defined strain-induced permeability function to solve the multi-field coupling equation. Thus, after solving the field variables, we can further calculate CH<sub>4</sub> production and CO<sub>2</sub> sequestration, as shown below [30].

**Table 1**  
Basic parameter for simulation.

| Parameter                                  | Value                                             | Parameter                                       | Value                                                 |
|--------------------------------------------|---------------------------------------------------|-------------------------------------------------|-------------------------------------------------------|
| Physical model's dimension (m)             | 200 × 200 × 10                                    | Coal specific heat capacity (J/(kg·K))          | 1350                                                  |
| Grid size (m)                              | 2 × 2 × 5                                         | Gas specific heat capacity (J/(kg·K))           | 840 for CO <sub>2</sub> , 2220 for CH <sub>4</sub>    |
| Initial reservoir pressure (MPa)           | 10                                                | Coal heat conduction coefficient (W/(m·K))      | 0.191                                                 |
| Initial reservoir temperature (K)          | 302                                               | Gas heat conduction coefficient (W/(m·K))       | 0.015 for CO <sub>2</sub> , 0.031 for CH <sub>4</sub> |
| Production well bottom-hole pressure (MPa) | 1                                                 | Adsorption heat (J/mol)                         | 19.2 for CO <sub>2</sub> , 16.4 for CH <sub>4</sub>   |
| Injection rate (m <sup>3</sup> /d)         | 400                                               | Coefficient of thermal expansion (1/K)          | 0.000024                                              |
| Injection period (d)                       | 50                                                | Molecular weight (g/mol)                        | 28 for CO <sub>2</sub> , 14 for CH <sub>4</sub>       |
| Initial coal matrix permeability (mD)      | 0.1                                               | Molecular diameter (nm)                         | 0.33 for CO <sub>2</sub> , 0.38 for CH <sub>4</sub>   |
| Initial coal matrix porosity (%)           | 7.2                                               | Average pore size (nm)                          | 50                                                    |
| Initial coal fracture permeability (mD)    | 1000                                              | Boltzmann constant (J/K)                        | 1.3806 × 10 <sup>-23</sup>                            |
| Fracture width (m)                         | 0.0001 ~ 0.0003                                   | Young's modulus (GPa)                           | 1.2                                                   |
| Fracture length in x dimension (m)         | 0 ~ 100                                           | Poisson's ratio (–)                             | 0.28                                                  |
| Fracture length in y dimension (m)         | 0 ~ 100                                           | Matrix-fracture connection coefficient (–)      | 0.6                                                   |
| Fracture length in z dimension (m)         | 0 ~ 10                                            | Coal viscoelastic modulus (GPa)                 | 3.64                                                  |
| Fracture vertices (–)                      | 3 ~ 6                                             | Coal viscoelastic coefficient (Pa·h $^\gamma$ ) | 3.24                                                  |
| Fracture number (–)                        | 5 ~ 20                                            | Coal viscoplastic coefficient (Pa·h $^\gamma$ ) | 13.24                                                 |
| Coal matrix compressibility (1/MPa)        | 0.0035                                            | Fractional derivative (–)                       | 0.9                                                   |
| Coal fracture compressibility (1/MPa)      | 0.01                                              | viscosity coefficient (–)                       | 0.17                                                  |
| Maximum relative permeability              | 1 for CO <sub>2</sub> , 0.8 for CH <sub>4</sub>   | Biot's coefficient (–)                          | 0.8                                                   |
| Saturations of residual gas (–)            | 0 for CO <sub>2</sub> , 0.15 for CH <sub>4</sub>  | Pressure coefficient (1/MPa)                    | 0.071                                                 |
| Relative permeability index                | 2 for CO <sub>2</sub> , 1.8 for CH <sub>4</sub>   | Temperature coefficient (1/K)                   | 0.021                                                 |
| Langmuir volume (m <sup>3</sup> /t)        | 10 for CO <sub>2</sub> , 38 for CH <sub>4</sub>   | Well number (–)                                 | 4 for train, 5 for optimization                       |
| Langmuir pressure (MPa)                    | 1.2 for CO <sub>2</sub> , 2.2 for CH <sub>4</sub> | Initial capillary pressure (MPa)                | 0.01                                                  |
| Langmuir strain (–)                        | 0.03                                              | Coal density (kg/m <sup>3</sup> )               | 1350                                                  |

$$Q_{pro,i} = \frac{2k_{f,i}k_m(p_{g,i} - p_{wf})}{\mu_{g,i}B_{g,i}\ln\left(\sum_j^{x,y,z}(\Delta j)^2/r_w^2\right)} \quad (27)$$

$$Q_{seq,2} = Q_{inj,2} - \sum_{i=1}^{N_{well}} Q_{pro,2} \quad (28)$$

where  $Q_{pro,i}$  is the production term of gas component  $i$ , m<sup>3</sup>/d;  $p_{wf}$  is the bottom-hole pressure, MPa;  $r_w$  is the well radius, m;  $Q_{seq,2}$  is the CO<sub>2</sub> sequestration rate, m<sup>3</sup>/d;  $Q_{inj,2}$  is the CO<sub>2</sub> injection rate, m<sup>3</sup>/d; and  $N_{well}$  is the number of production wells.

![Figure 3: CO2 saturation (%) comparison results (proposed model vs. pEDFM). The figure consists of a 3x3 grid of heatmaps. The top row shows results for the pEDFM model at 5d, 6d, and 10d. The middle row shows results for the tSEDFM model at the same time steps. The bottom row shows the RMSE (Root Mean Square Error) between the proposed model and pEDFM at 5d, 6d, and 10d. Each plot has X (m) and Y (m) axes ranging from 0 to 10. A color bar on the right indicates the saturation percentage from 0 to 100. The pEDFM and tSEDFM plots show a similar pattern of CO2 saturation, with a high-concentration region (yellow/red) spreading from the bottom left over time. The RMSE plots show the error distribution, with a color bar ranging from 0 to 2.](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 3: CO2 saturation (%) comparison results (proposed model vs. pEDFM). The figure consists of a 3x3 grid of heatmaps. The top row shows results for the pEDFM model at 5d, 6d, and 10d. The middle row shows results for the tSEDFM model at the same time steps. The bottom row shows the RMSE (Root Mean Square Error) between the proposed model and pEDFM at 5d, 6d, and 10d. Each plot has X (m) and Y (m) axes ranging from 0 to 10. A color bar on the right indicates the saturation percentage from 0 to 100. The pEDFM and tSEDFM plots show a similar pattern of CO2 saturation, with a high-concentration region (yellow/red) spreading from the bottom left over time. The RMSE plots show the error distribution, with a color bar ranging from 0 to 2.

Fig. 3. CO<sub>2</sub> saturation (%) comparison results (proposed model vs. pEDFM).

![Figure 4: Comparison results of the ATHM model at different scales. (a) proposed model vs. experiment data: A line graph showing CO2 concentration (%) over Time (min) from 0 to 30. The y-axis ranges from 0 to 90. It includes experimental data (triangles) and model predictions (lines) for 2 MPa (red) and 1.5 MPa (blue). Two insets show zoomed-in views of the initial phase with 5 cm and 2.5 cm spatial scales. (b) proposed model vs. field data: A dual-axis plot showing CH4 production (m³/d) on the left y-axis (0 to 1500) and Error (%) on the right y-axis (0 to 30) over Time (d) from 0 to 400. The plot compares the proposed model (red line), field data (blue circles), and error (black line).](ac99eff233b8fe51d30f499e7413c345_img.jpg)

Figure 4: Comparison results of the ATHM model at different scales. (a) proposed model vs. experiment data: A line graph showing CO2 concentration (%) over Time (min) from 0 to 30. The y-axis ranges from 0 to 90. It includes experimental data (triangles) and model predictions (lines) for 2 MPa (red) and 1.5 MPa (blue). Two insets show zoomed-in views of the initial phase with 5 cm and 2.5 cm spatial scales. (b) proposed model vs. field data: A dual-axis plot showing CH4 production (m³/d) on the left y-axis (0 to 1500) and Error (%) on the right y-axis (0 to 30) over Time (d) from 0 to 400. The plot compares the proposed model (red line), field data (blue circles), and error (black line).

(a) proposed model vs. experiment data

(b) proposed model vs. field data

Fig. 4. Comparison results of the ATHM model at different scales.

![Figure 5: LSTM structure. The top part shows a high-level view of an LSTM network processing a time sequence of inputs (x_{t-1}, x_t, x_{t+1}, ..., x_n) through an input layer, a hidden layer with nodes h_{t-1}, h_t, h_{t+1}, and an output layer. The bottom part shows the internal structure of a single LSTM cell. It takes input x_t and previous hidden state h_{t-1} to produce current hidden state h_t and cell state C_t. The cell consists of three gates: the Forget Gate (sigmoid function sigma) multiplying the previous cell state C_{t-1} by the input gate (sigmoid function sigma) and the input (tanh function tanh). The Output Gate (sigmoid function sigma) then multiplies the result by the tanh of the cell state C_t to produce the hidden state h_t.](a738993919a50143787084ee7ce6e2f2_img.jpg)

Figure 5: LSTM structure. The top part shows a high-level view of an LSTM network processing a time sequence of inputs (x\_{t-1}, x\_t, x\_{t+1}, ..., x\_n) through an input layer, a hidden layer with nodes h\_{t-1}, h\_t, h\_{t+1}, and an output layer. The bottom part shows the internal structure of a single LSTM cell. It takes input x\_t and previous hidden state h\_{t-1} to produce current hidden state h\_t and cell state C\_t. The cell consists of three gates: the Forget Gate (sigmoid function sigma) multiplying the previous cell state C\_{t-1} by the input gate (sigmoid function sigma) and the input (tanh function tanh). The Output Gate (sigmoid function sigma) then multiplies the result by the tanh of the cell state C\_t to produce the hidden state h\_t.

Fig. 5. LSTM structure.

## 3. Validation

To evaluate the accuracy and reliability of the proposed tSEDFM-ATHM model, comprehensive validation was conducted using the classical pEDFM and experiment data. This is aimed at ensuring the model's robustness across different scenarios and scales. The key parameters required for validation cases are consistent with the references [17,20], and the basic parameters of the model are shown in Table 1.

### 3.1. Validation of tSEDFM

By conducting comparative validation using tSEDFM and pEDFM [20], this section delved into the differences between the two models in simulating the flow characteristics of fractured coal reservoirs. The tSEDFM model, incorporating transient flow effects, significantly enhances simulation accuracy. In a  $10\text{ m} \times 10\text{ m}$   $\text{CO}_2\text{-CH}_4$  displacement simulation scenario with an injection pressure of 10 MPa and a BHP of 1 MPa, the tSEDFM demonstrates a clear advantage over the pEDFM in calculating the carbon dioxide saturation at the central cross-shaped fracture (4 m), as shown in Fig. 3. In the proposed tSEDFM model, a broader diffusion range of  $\text{CO}_2$  along the fracture walls can be observed. This advantage enables tSEDFM to more accurately reflect the transient inter-porosity flow phenomenon, providing a more reliable simulation

tool for the fluid flow analysis of fractured coal reservoir.

### 3.2. Validation of the ATHM model

Liu's experimental data [17] is used to verify the accuracy of the proposed ATHM model. As shown in Fig. 4(a), the calculation results of  $\text{CO}_2$  concentration are in good agreement with the experimental data obtained under 2 MPa and 1.5 MPa. For  $\text{CO}_2$  injection, the total average errors of the  $\text{CO}_2$  concentration are all less than 10 %. The production data of a coalbed methane well in the No. 3 coal seam in the southern Qinshui Basin were further utilized for history matching. The initial pressure and BHP are 11.28 MPa and 0.25 MPa, respectively. The average permeability is 0.06mD. Fig. 4(b) indicates that the relative error is less than 10 %. The above validations can be fully illustrate the reliability of the tSEDFM-ATHM model for  $\text{CO}_2$ -ECBM simulation. It can serve as physical constraints for the deep learning framework.

## 4. Hybrid deep learning framework

The LSTM framework demonstrates advanced prediction capabilities for periodic-trend time series, particularly in predicting  $\text{CH}_4$  production and  $\text{CO}_2$  sequestration under the cyclical injection-production strategy [30]. This is attributed to its intrinsic memory-gated architecture that

![Figure 6: Physical model for CO2-ECBM simulation. (a) Well group layout showing injection (P2) and production (P1) wells, and fractures (J1, J2). (b) Permeability (mD) distribution. (c) Porosity (-) distribution. All plots show spatial distribution over a 200m x 200m area with a 10m depth.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 6: Physical model for CO2-ECBM simulation. (a) Well group layout showing injection (P2) and production (P1) wells, and fractures (J1, J2). (b) Permeability (mD) distribution. (c) Porosity (-) distribution. All plots show spatial distribution over a 200m x 200m area with a 10m depth.

Fig. 6. Physical model for CO<sub>2</sub>-ECBM simulation(a) well group, (b) permeability (mD), and (c) porosity (-).

captures long-term dependencies This section uses the numerical simulator proposed above as the physical constraint and introduces the LSTM-BO to establish a deep learning framework to improve the computational efficiency of traditional numerical simulation.

### 4.1. LSTM structure

The LSTM is a special recurrent neural network (RNN) [42], which consists of an input layer, an hidden layer, the cell state, and an output layer. The cell state, as illustrated in Fig. 5, includes the forget gate, input gate, and output gate.

The forget gate is a key computational unit that determines the amount of long-term information  $C$  that would be retained. Its mathematical essence is to assign  $f_t$  between [0,1] to  $C_{t-1}$  passed from the previous time step, as shown in Eq. (29).

$$f_t = \sigma(x)(W_f[h_{t-1}, x_t] + b_f) \quad (29)$$

The input gate is a computational unit that determines the amount of new information that would be incorporated into the long-term memory  $C$ . Its mathematical essence is to assign a weight between [0,1] to all the input information at the current time step (see Eq. (30)), filter out some of the new information, and integrate the remaining new information into  $C_t$ .

$$C_t = f_t C_{t-1} + \sigma(x)(W_i[h_{t-1}, x_t] + b_i) \tanh(W_C[h_{t-1}, x_t] + b_C) \quad (30)$$

The output gate is a computational unit that selects the most suitable short-term information  $h_t$  from the newly updated  $C_t$  for the current time step. Its mathematical essence is to assign a weight between [0,1] to the already computed  $C_t$  (see Eq. (31)) and select the most effective information for the current time step. That effective information will be used to make predictions for that step.

$$h_t = \sigma(x)(W_o[h_{t-1}, x_t] + b_o) \tanh(C_t) \quad (31)$$

where the definition of  $\tanh(x)$  and activation functions  $\sigma(x)$  is:

$$\tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}} \quad (32)$$

$$\sigma(x) = \frac{1}{1 + e^{-x}} \quad (33)$$

Here,  $W$  and  $b$  represent the weight and bias respectively;  $x_t$  is the time sequence;  $C_t$  is the cell state; and  $h_t$  is the hidden state.

In particular, the time sequence needs to eliminate variability of different feature magnitudes through data min-max normalization:

$$X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}} \quad (34)$$

where  $X_{norm}$  is the normalized time sequence;  $X$  is the input time sequence;  $X_{max}$  is the maximum value of the time sequence; and  $X_{min}$  is the minimum value of the time sequence.

### 4.2. LSTM-BO parameter optimization

To obtain the optimal structure hyperparameters of the LSTM model, the Bayesian optimization (BO) [43] is applied due to its ability in quickly optimizing nonlinear problems. This feature can strike a balance between model performance and training efficiency. The number of initial seed points is 4. The expected improvement (EI) is adopted as the acquisition function. The maximum convergence epoch are 30. The maximum convergence tolerance is 0.01.

The search space, which includes learning rate (0.01–0.1), hidden layers (8–64), and LSTM layers (1–5), is established. The time step is set as 15 days. the Adam method is selected as the optimizer. The number of training epochs is set as 1000. In particular, Eq. (34) is adopted to normalize the input time series. The root mean squared error (RMSE) is selected as the optimization target, as demonstrated in Eq. (35). Based on the proposed tSEDFM-ATHM model, we established a CO<sub>2</sub>-ECBM well group with 15 fractures (see Fig. 6). The initial average matrix permeability and porosity are 0.1 mD and 7.2 %. The production well bottom-hole pressure is 1 MPa. The injection period is 50 days, while the

![Figure 7: RMSE solution sets in hyper parameter optimization. (a) RMSE vs. learning rate and hidden layer. (b) RMSE vs. learning rate and LSTM layer. (c) RMSE vs. LSTM layer and hidden layer. All plots show RMSE (0 to 0.025) on the vertical axis.](ffe022f31d53e7067d16f39f82e1fb68_img.jpg)

Figure 7: RMSE solution sets in hyper parameter optimization. (a) RMSE vs. learning rate and hidden layer. (b) RMSE vs. learning rate and LSTM layer. (c) RMSE vs. LSTM layer and hidden layer. All plots show RMSE (0 to 0.025) on the vertical axis.

Fig. 7. RMSE solution sets in hyper parameter optimization((a) learning rate vs. hidden layer, (b) learning rate vs. LSTM layer, and (c) LSTM layer vs. hidden layer).

![Figure 8: LSTM training and test results. (a) CH4 production (m³/d) vs Time (d). (b) CO2 sequestration (10⁴ m³/d) vs Time (d). (c) R² in CH4 production. (d) R² in CO2 sequestration. (e) CH4 adsorption content (m³/t) 3D plot. (f) CO2 adsorption content (m³/t) 3D plot.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 8 consists of six subplots. Subplots (a) and (b) are line graphs showing real data (solid black line) and LSTM training and test data (dashed lines) over time (0 to 2000 days). (a) shows CH<sub>4</sub> production (m<sup>3</sup>/d) from 0 to 3200, with a clear downward trend. (b) shows CO<sub>2</sub> sequestration (10<sup>4</sup> m<sup>3</sup>/d) from 0 to 600, showing a sawtooth pattern. Subplots (c) and (d) are scatter plots of training and test data (black squares and red triangles) against real data (blue line), showing a strong linear correlation. (c) is for CH<sub>4</sub> production (0 to 500) and (d) is for CO<sub>2</sub> sequestration (0 to 3200). Subplots (e) and (f) are 3D surface plots of adsorption content (m<sup>3</sup>/t) over a spatial domain (X, Y, Z in meters). (e) is for CH<sub>4</sub> adsorption content (0 to 8 m<sup>3</sup>/t) and (f) is for CO<sub>2</sub> adsorption content (5 to 35 m<sup>3</sup>/t). Both show spatial variations over time (100 d, 1000 d, 2000 d).

Figure 8: LSTM training and test results. (a) CH4 production (m³/d) vs Time (d). (b) CO2 sequestration (10⁴ m³/d) vs Time (d). (c) R² in CH4 production. (d) R² in CO2 sequestration. (e) CH4 adsorption content (m³/t) 3D plot. (f) CO2 adsorption content (m³/t) 3D plot.

**Fig. 8.** LSTM training and test results(a) CH<sub>4</sub> production, (b) CO<sub>2</sub> sequestration, (c)  $R^2$  in CH<sub>4</sub> production, (d)  $R^2$  in CO<sub>2</sub> sequestration, (e) CH<sub>4</sub> adsorption content, and (f) CO<sub>2</sub> adsorption content.

injection rate is 400 m<sup>3</sup>/d. The simulated CH<sub>4</sub> production and CO<sub>2</sub> sequestration serve as input time sequence for LSTM training and optimization, where the ratio of training set to test is 8:2.

After 8 rounds of training on the LSTM neural network using BO, we obtained the optimal parameters: 0.08 learning rate, 15 hidden layers, and 2 LSTM layers, as shown in Fig. 7. The training results of the P1 well are shown in Fig. 8 with the coefficients of determination ( $R^2$  in Eq. (36)) at 96.5 % and 96.1 %, respectively. This ensures the accuracy of the proposed hybrid deep learning framework.

$$RMSE = \sqrt{\frac{\sum_{t=1}^{n} (Q_{train} - Q_{real})^2}{n}} \quad (35)$$

$$R^2 = \frac{\sum_{t=1}^{n} (Q_{train} - \bar{Q}_{train})^2}{\sum_{t=1}^{n} (Q_{real} - \bar{Q}_{real})^2} \quad (36)$$

where  $Q_{train}$  is the trained production/sequestration sequence;  $Q_{real}$  is the simulated production/sequestration sequence;  $\bar{Q}_{train}$  is the average value of  $Q_{train}$ ;  $\bar{Q}_{real}$  is the average value of  $Q_{real}$ ; and  $n$  is the number of

![LSTM recursive prediction workflow diagram](cfda9df1319e04207eb28bcefd1dab7b_img.jpg)

The diagram illustrates the LSTM recursive prediction workflow. It starts with three input sequences: a Value sequence (green), a Time sequence (grey), and a Label sequence (yellow). The Value sequence is normalized using the formula: 
$$X_{norm} = \frac{X - X_{min}}{X_{max} - X_{min}}$$
. The normalized Value sequence is then used to form an Input sequence (orange dashed box) and a Predict sequence (green solid box). The workflow shows a recursive process where the Predict sequence is fed back into the Input sequence for the next step, as indicated by the red curved arrows. The final output is a sequence of length  $n$ .

LSTM recursive prediction workflow diagram

Fig. 9. LSTM recursive prediction workflow.

![LSTM recursive prediction results for CH4 production, CO2 sequestration, and their cumulative values.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 10 displays four plots comparing real data (solid black line) and prediction data (dashed red line) over a time period from 0 to 3200 days.

(a) CH<sub>4</sub> production (m<sup>3</sup>/d): The y-axis ranges from 0 to 3200. The real data shows high-frequency oscillations that decay over time. The prediction data closely follows the real data. A table below the plot compares the performance of two methods:

| Method             | Time     | Time saving |
|--------------------|----------|-------------|
| tSEDM-ATHM         | 18.4 min |             |
| tSEDM-ATHM-LSTM-BO | 8.35 min | 54.6 %      |

(b) CO<sub>2</sub> sequestration (10<sup>4</sup> m<sup>3</sup>/d): The y-axis ranges from 0 to 600. The real data shows high-frequency oscillations that increase over time. The prediction data closely follows the real data.

(c) CH<sub>4</sub> cumulative production (10<sup>4</sup> m<sup>3</sup>): The y-axis ranges from 0 to 80. The real data shows a smooth, increasing curve. The prediction data closely follows the real data.

(d) CO<sub>2</sub> cumulative sequestration (10<sup>4</sup> m<sup>3</sup>): The y-axis ranges from 0 to 18. The real data shows a smooth, increasing curve. The prediction data closely follows the real data.

LSTM recursive prediction results for CH4 production, CO2 sequestration, and their cumulative values.

Fig. 10. LSTM recursive prediction results(a) CH<sub>4</sub> production, (b) CO<sub>2</sub> sequestration, (c) CH<sub>4</sub> cumulative production, and (d) CO<sub>2</sub> cumulative sequestration).


![Figure 11: CH4 production and CO2 sequestration with different fracture number. (a) CH4 cumulative production (10^4 m^3) vs Time (d) for fracture numbers 5, 15, and 25. (b) CO2 cumulative sequestration (10^4 m^3) vs Time (d) for fracture numbers 5, 15, and 25. (c) Capacity comparison of CH4 cumulative production and CO2 cumulative sequestration vs Fracture number (5, 15, 25).](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 11: CH4 production and CO2 sequestration with different fracture number. (a) CH4 cumulative production (10^4 m^3) vs Time (d) for fracture numbers 5, 15, and 25. (b) CO2 cumulative sequestration (10^4 m^3) vs Time (d) for fracture numbers 5, 15, and 25. (c) Capacity comparison of CH4 cumulative production and CO2 cumulative sequestration vs Fracture number (5, 15, 25).

Fig. 11. CH<sub>4</sub> production and CO<sub>2</sub> sequestration with different fracture number ((a) CH<sub>4</sub> cumulative production, (b) CO<sub>2</sub> cumulative sequestration, and (c) capacity comparison).

![Figure 12: 3D surface plots of CH4 and CO2 adsorption content profile with different fracture number. (a) CH4 with 5 fractures, (b) CH4 with 15 fractures, (c) CH4 with 25 fractures, (d) CO2 with 5 fractures, (e) CO2 with 15 fractures, and (f) CO2 with 25 fractures. The plots show adsorption content (m^3/t) on the vertical axis against X (m) and Y (m) on the horizontal axes.](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

Figure 12: 3D surface plots of CH4 and CO2 adsorption content profile with different fracture number. (a) CH4 with 5 fractures, (b) CH4 with 15 fractures, (c) CH4 with 25 fractures, (d) CO2 with 5 fractures, (e) CO2 with 15 fractures, and (f) CO2 with 25 fractures. The plots show adsorption content (m^3/t) on the vertical axis against X (m) and Y (m) on the horizontal axes.

Fig. 12. CH<sub>4</sub> and CO<sub>2</sub> adsorption content profile with different fracture number ((a) CH<sub>4</sub> with 5 fractures, (b) CH<sub>4</sub> with 15 fractures, (c) CH<sub>4</sub> with 25 fractures, (d) CO<sub>2</sub> with 5 fractures, (e) CO<sub>2</sub> with 15 fractures, and (f) CO<sub>2</sub> with 25 fractures).

time sequence.

is introduced. The conceptual model is shown in Fig. 9, using a trained LSTM model to predict the value of the next time step. The predicted data was used as part of the input to continue predicting subsequent time steps. Thus, we set the time step length and one injection-production cycle as 15 days and 50 days respectively. We predicted the CH<sub>4</sub>

## 4.3. Physical-constraint-based recursive prediction

To further predict the time sequence, a recursive prediction method

![Figure 13: CH4 production and CO2 sequestration at different injection rate. (a) CH4 cumulative production (10^4 m^3) vs Time (d) for injection rates of 200, 400, and 600 m^3/d. (b) CO2 cumulative sequestration (10^4 m^3) vs Time (d) for injection rates of 200, 400, and 600 m^3/d. (c) Capacity comparison of CH4 cumulative production and CO2 cumulative sequestration vs Injection rate (m^3/d).](2f73c3f1961c12d27d0d18fe7befbf0c_img.jpg)

Figure 13: CH4 production and CO2 sequestration at different injection rate. (a) CH4 cumulative production (10^4 m^3) vs Time (d) for injection rates of 200, 400, and 600 m^3/d. (b) CO2 cumulative sequestration (10^4 m^3) vs Time (d) for injection rates of 200, 400, and 600 m^3/d. (c) Capacity comparison of CH4 cumulative production and CO2 cumulative sequestration vs Injection rate (m^3/d).

Fig. 13. CH<sub>4</sub> production and CO<sub>2</sub> sequestration at different injection rate ((a) CH<sub>4</sub> cumulative production, (b) CO<sub>2</sub> cumulative sequestration, and (c) capacity comparison).

![Figure 14: Six 3D surface plots (a-f) showing CH4 and CO2 adsorption content profiles. The plots are arranged in a 2x3 grid. The axes are X (m), Y (m), and Z (m). A color bar on the right indicates the adsorption content in m³/t, ranging from 0 to 8 for (a-c) and 0 to 35 for (d-f). (a) CH4 at 200 m³/d, (b) CH4 at 400 m³/d, (c) CH4 at 600 m³/d, (d) CO2 at 200 m³/d, (e) CO2 at 400 m³/d, (f) CO2 at 600 m³/d. The surfaces show complex patterns of high and low adsorption content across the spatial domain.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 14: Six 3D surface plots (a-f) showing CH4 and CO2 adsorption content profiles. The plots are arranged in a 2x3 grid. The axes are X (m), Y (m), and Z (m). A color bar on the right indicates the adsorption content in m³/t, ranging from 0 to 8 for (a-c) and 0 to 35 for (d-f). (a) CH4 at 200 m³/d, (b) CH4 at 400 m³/d, (c) CH4 at 600 m³/d, (d) CO2 at 200 m³/d, (e) CO2 at 400 m³/d, (f) CO2 at 600 m³/d. The surfaces show complex patterns of high and low adsorption content across the spatial domain.

**Fig. 14.** CH<sub>4</sub> and CO<sub>2</sub> adsorption content profiles with different injection rates (a) CH<sub>4</sub> at a 200 m<sup>3</sup>/d injection rate, (b) CH<sub>4</sub> at a 400 m<sup>3</sup>/d injection rate, (c) CH<sub>4</sub> at a 600 m<sup>3</sup>/d injection rate, (d) CO<sub>2</sub> at a 200 m<sup>3</sup>/d injection rate, (e) CO<sub>2</sub> at a 400 m<sup>3</sup>/d injection rate, and (f) CO<sub>2</sub> at a 600 m<sup>3</sup>/d injection rate).

production and CO<sub>2</sub> sequestration based on the trained LSTM model with physical-constraint offered by tSEDFM-ATHM simulator, as shown in Fig. 10. Based on the computer platform of RYZEN 5950x CPU with 128 G memory, the hybrid framework reduces the calculation time by about 54.6 % (see Fig. 10(a)) compared with the proposed tSEDFM-ATHM simulation. The excellent prediction results have been fully achieved.

# 5. Discussion and application

The trend and periodicity patterns of production and sequestration are influenced by fractures, injection rate, injection time, and reservoir parameters. Benefiting from the tSEDFM-ATHM model, the generated time sequences are constrained by the physical-model-involved mechanisms. When integrating the hybrid tSEDFM-ATHM-LSTM-BO deep learning framework, rapid and robust predictions can be achieved. This offers a balance among interpretability, high accuracy, and computational efficiency.

## 5.1. Sensitivity analysis

In this section, based on the previous well group model and the

established hybrid deep learning framework, the influencing factors of CH<sub>4</sub> production and CO<sub>2</sub> sequestration in the CO<sub>2</sub>-ECBM process are discussed. Note that CH<sub>4</sub> production is the sum of three wells (P1 + P2 + P3).

### 5.1.1. Effect of fracture number

Fig. 11 show the CH<sub>4</sub> production and CO<sub>2</sub> sequestration with different fracture number. The injection rate is 400 m<sup>3</sup>/d, and the injection period is 50 days. The cumulative CH<sub>4</sub> production reaches its maximum value with 25 fractures, while CO<sub>2</sub> sequestration peaks with only 5 fractures. This phenomenon occurs because fractures accelerate methane flow and heat transfer during CO<sub>2</sub>-ECBM, thereby promoting methane desorption. However, more fractures also facilitate earlier CO<sub>2</sub> breakthrough to the production well, impairing sequestration efficiency (see Fig. 11a to Fig. 11c). The production performance is jointly determined by the dual effects of fractures: positive enhancement of methane recovery versus negative impacts on CO<sub>2</sub> sequestration. As demonstrated in Figs. 12 and 13, fracture density exhibits a more significant influence on methane production. The residual methane adsorption shows an inverse correlation to the fracture number. Increased CO<sub>2</sub> adsorption in coal reservoirs indicates the improved methane displacement. The fracture number, orientation, and size simultaneously

![Figure 15: Three line graphs (a-c) showing the effect of injection period. (a) CH4 cumulative production (10^6 m^3) vs Time (d) for injection periods of 25, 50, and 100 days. (b) CO2 cumulative sequestration (10^6 m^3) vs Time (d) for the same injection periods. (c) Capacity comparison showing CH4 cumulative production (10^6 m^3) and CO2 cumulative sequestration (10^6 m^3) vs Injection period (d).](d7346a28f4ba53888f72648cface9da9_img.jpg)

Figure 15: Three line graphs (a-c) showing the effect of injection period. (a) CH4 cumulative production (10^6 m^3) vs Time (d) for injection periods of 25, 50, and 100 days. (b) CO2 cumulative sequestration (10^6 m^3) vs Time (d) for the same injection periods. (c) Capacity comparison showing CH4 cumulative production (10^6 m^3) and CO2 cumulative sequestration (10^6 m^3) vs Injection period (d).

**Fig. 15.** CH<sub>4</sub> production and CO<sub>2</sub> sequestration with different injection periods ((a) CH<sub>4</sub> cumulative production, (b) CO<sub>2</sub> cumulative sequestration, and (c) capacity comparison).

![Figure 16: Six 3D surface plots (a-f) showing CH4 and CO2 adsorption content profiles. (a), (b), and (c) show CH4 adsorption for 25-d, 50-d, and 100-d injection periods respectively. (d), (e), and (f) show CO2 adsorption for 25-d, 50-d, and 100-d injection periods respectively. The plots show a color gradient from blue (low) to red (high) representing adsorption content in m³/t. The axes are X (m), Y (m), and Z (m).](b05a8a3551db31147979064952179990_img.jpg)

Figure 16: Six 3D surface plots (a-f) showing CH4 and CO2 adsorption content profiles. (a), (b), and (c) show CH4 adsorption for 25-d, 50-d, and 100-d injection periods respectively. (d), (e), and (f) show CO2 adsorption for 25-d, 50-d, and 100-d injection periods respectively. The plots show a color gradient from blue (low) to red (high) representing adsorption content in m³/t. The axes are X (m), Y (m), and Z (m).

**Fig. 16.** CH<sub>4</sub> and CO<sub>2</sub> adsorption content profiles with different injection periods ((a) CH<sub>4</sub> with 25-d injection, (b) CH<sub>4</sub> with 50-d injection, (c) CH<sub>4</sub> with 100-d injection, (d) CO<sub>2</sub> with 25-d injection, (e) CO<sub>2</sub> with 50-d injection, and (f) CO<sub>2</sub> with 100-d injection).

generate flow heterogeneity, emphasizing the necessity of using the tSEDFM for accurately describing fluid flow in fracture networks.

### 5.1.2. Effect of the injection rate

Fig. 13 shows the CH<sub>4</sub> production and CO<sub>2</sub> sequestration at different injection rates. The fracture number is 25, and the injection period is 50 days. Fig. 13(a) and (b) demonstrate that when the injection rate exceeds 400 m<sup>3</sup>/d, a 19.3 % increase in methane production and a near-linear 106 % growth in CO<sub>2</sub> sequestration can be observed. Combined with appropriate cyclic injection and well shut-in strategies, moderately increasing the CO<sub>2</sub> injection rate can enhance displacement efficiency. This promotes competitive adsorption between CO<sub>2</sub> and CH<sub>4</sub>. This process facilitates methane desorption and migration, and ensures CO<sub>2</sub> diffusion and adsorption in coal reservoirs, achieving efficient sequestration (see Fig. 14). However, fracture network constraint sustains the CO<sub>2</sub> production rate increase due to early CO<sub>2</sub> breakthrough at production wells, undermining long-term sequestration.

### 5.1.3. Effect of the injection period

Fig. 15 show the CH<sub>4</sub> production and CO<sub>2</sub> sequestration under different injection periods. The injection rate is 400 m<sup>3</sup>/d, and the fracture number is 25. As shown in Fig. 15(a), CH<sub>4</sub> cumulative production peaks using the 25-day injection schedule, reaching  $244.8 \times 10^4$  m<sup>3</sup>/d at 3200 days. Longer injection periods result in lower CH<sub>4</sub> production. A 38.8 % reduction is observed when it changes from the 25-day injection schedule to 50-day injection schedule. This counterintuitive trend suggests that shorter injection cycles cause rapid CH<sub>4</sub>

desorption and migration before CO<sub>2</sub> breakthrough dominates the flow pattern. Frequent injection leads to fluctuations in temperature and pressure, which significantly enhances the desorption of methane. Simultaneously, given the strong competitive adsorption advantage of carbon dioxide, methane is desorbed in substantial quantities at shorter injection cycles during this process. Similarly, CO<sub>2</sub> sequestration exhibits a linear increase with the injection period reduction, rising from  $11.2 \times 10^4$  m<sup>3</sup> (100 day) to  $21.6 \times 10^4$  m<sup>3</sup> (25 day). Thus, nearly 92 % of the CO<sub>2</sub> is further sequestrated, as less breakthrough enhances CO<sub>2</sub> adsorption in coal reservoirs (Fig. 15b and Fig. 15c). The adsorption content profile shown in Fig. 16 further demonstrates that shorter injection periods enhance CO<sub>2</sub> adsorption in coal reservoirs, while CH<sub>4</sub> production exhibits a growth inflection point. This is attributed to insufficient injection time within an ultra-short period, which hinders CH<sub>4</sub> migration and restricts rapid production. Therefore, during the CO<sub>2</sub>-ECBM, the CO<sub>2</sub> injection period should be optimized according to the actual reservoir condition.

## 5.2. Optimization of an actual reservoir in the Qinshui basin

To further demonstrate the field applicability of the proposed hybrid framework, an actual geological model from the Qinshui basin is used. The injection period and the rate of CO<sub>2</sub>-ECBM for a 5-point well group are optimized based on the hybrid tSEDFM-ATHM-LSTM-BO framework. The well pattern and the basic parameters are shown in Fig. 17. The parameters and their ranges for optimization include the injection rate (200 m<sup>3</sup>/d–800 m<sup>3</sup>/d) and the injection period (10d–120d). The

![Figure 17: (a) 3D schematic of a 5-point well group with production wells P1, P2, P3, P4 and an injection well I. (b) 3D surface plot of permeability (mD) with a color scale from 0.3 to 0.8. (c) 3D surface plot of porosity (-) with a color scale from 0.02 to 0.08. (d) 3D surface plot of CH4 adsorption content (m³/t) with a color scale from 4 to 16. The axes are X (m), Y (m), and Z (m).](e77321c92e46f4f20632d48cfebc312c_img.jpg)

Figure 17: (a) 3D schematic of a 5-point well group with production wells P1, P2, P3, P4 and an injection well I. (b) 3D surface plot of permeability (mD) with a color scale from 0.3 to 0.8. (c) 3D surface plot of porosity (-) with a color scale from 0.02 to 0.08. (d) 3D surface plot of CH4 adsorption content (m³/t) with a color scale from 4 to 16. The axes are X (m), Y (m), and Z (m).

**Fig. 17.** 5-point well group and its property ((a) well group, (b) permeability (mD), (c) porosity (-), and (d) CH<sub>4</sub> adsorption content (m<sup>3</sup>/t)).

![Figure 18: Optimization results of the injection strategy. (a) Optimization trajectory of F showing a step-like increase from 0 to 120 over 12 rounds. (b) 3D surface plot of F (10^4 m^3) as a function of injection period (d) and injection rate (m^3/d), with a blue dot at (500, 20, 108.6). (c) Optimal CH4 production curve showing production (10^4 m^3/d) and cumulative production (10^4 m^3) over 3200 days. (d) Optimal CO2 sequestration curve showing sequestration (m^3/d) and cumulative sequestration (10^4 m^3) over 3200 days.](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 18: Optimization results of the injection strategy. (a) Optimization trajectory of F showing a step-like increase from 0 to 120 over 12 rounds. (b) 3D surface plot of F (10^4 m^3) as a function of injection period (d) and injection rate (m^3/d), with a blue dot at (500, 20, 108.6). (c) Optimal CH4 production curve showing production (10^4 m^3/d) and cumulative production (10^4 m^3) over 3200 days. (d) Optimal CO2 sequestration curve showing sequestration (m^3/d) and cumulative sequestration (10^4 m^3) over 3200 days.

Fig. 18. Optimization results of the injection strategy (a) optimization trajectory of  $F$ , (b) solution sets of  $F$ , (c) optimal  $\text{CH}_4$  production curve, and (d) optimal  $\text{CO}_2$  sequestration curve).

![Figure 19: CH4 and CO2 adsorption content profiles. (a) CH4 with 10-d injection, (b) CH4 with 100-d injection, (c) CH4 with 1000-d injection, (d) CO2 with 10-d injection, (e) CO2 with 100-d injection, and (f) CO2 with 1000-d injection. The plots show 3D spatial distributions of adsorption content (m^3/t) over a domain of X (m), Y (m), and Z (m).](411fa16c3211377525ba37c57784fee0_img.jpg)

Figure 19: CH4 and CO2 adsorption content profiles. (a) CH4 with 10-d injection, (b) CH4 with 100-d injection, (c) CH4 with 1000-d injection, (d) CO2 with 10-d injection, (e) CO2 with 100-d injection, and (f) CO2 with 1000-d injection. The plots show 3D spatial distributions of adsorption content (m^3/t) over a domain of X (m), Y (m), and Z (m).

Fig. 19.  $\text{CH}_4$  and  $\text{CO}_2$  adsorption content profiles with the optimal injection strategy (a)  $\text{CH}_4$  with 10-d injection, (b)  $\text{CH}_4$  with 100-d injection, (c)  $\text{CH}_4$  with 1000-d injection, (d)  $\text{CO}_2$  with 10-d injection, (e)  $\text{CO}_2$  with 100-d injection, and (f)  $\text{CO}_2$  with 1000-d injection).

maximum  $\text{CH}_4$  production and  $\text{CO}_2$  sequestration are the objective function as follow.

$$F = \max \left( \xi_1 \sum_{i=1}^{N_{\text{well}}} Q_{\text{pro},1} + \xi_2 \left( Q_{\text{inj},2} - \sum_{i=1}^{N_{\text{well}}} Q_{\text{pro},2} \right) \right) \quad (37)$$

where  $\xi_1$  and  $\xi_2$  are the weighting factors for the objective function,  $\xi_1 +$

$\xi_2 = 1$ ; and  $F$  is the objective function,  $\text{m}^3/\text{d}$ .

Fig. 18(a) illustrates the well group converged after 12 rounds of optimization, with the objective function value of  $F$  reaching  $108.6 \times 10^4 \text{ m}^3$ . The weighting factors of  $\xi_1$  and  $\xi_2$  are both 0.5. The optimal injection rate is  $500 \text{ m}^3/\text{d}$ , and the injection period turns out to be 20 days. Fig. 18(b) demonstrates that when the injection rate changes from  $460 \text{ m}^3/\text{d}$  to  $520 \text{ m}^3/\text{d}$ , and the injection period extends from 10 d to 22

d, the global objective function  $F$  attains a high value ( $>100 \times 10^4 \text{ m}^3$ ). Conversely, when the injection rate varies between  $200 \text{ m}^3/\text{d}$  and  $260 \text{ m}^3/\text{d}$ , and the injection period is between 40 d and 60 d, the global objective function  $F$  reaches its lowest values ( $<60 \times 10^4 \text{ m}^3$ ). Fig. 18 (c) and (d) further exhibit the curves representing  $\text{CH}_4$  production and  $\text{CO}_2$  sequestration for the well group in the Qinshui basin under the optimal operation strategy. In this situation, a maximum methane production of  $195.7 \times 10^4 \text{ m}^3$  and a peak sequestration of  $21.5 \times 10^4 \text{ m}^3$  during 3200 days can be achieved.

With the help of the physical constraints imposed by the tSEDFM-ATHM model and the accelerated prediction enabled by the LSTM-BO deep learning, the  $\text{CO}_2$ -ECBM injection strategy for well groups in other regions can also be optimized using the hybrid framework. Fig. 19 further illustrates the evolution of the adsorption content calculated based on the optimal solution. Under the combined influence of natural fractures, heterogeneous permeability, porosity, and adsorption,  $\text{CH}_4$  adsorption further weakens with  $\text{CO}_2$  injection. This reveals the migration and storage processes of  $\text{CH}_4$  and  $\text{CO}_2$  under multi-field coupling and interaction conditions. It explains the evolution of the  $\text{CH}_4$  production curve and the characteristics of  $\text{CO}_2$  sequestration. Compared with other traditional methods in the literature, it further enhances the interpretability of deep learning's prediction results.

# 6. Conclusion

This study addresses the computational bottlenecks in  $\text{CO}_2$ -ECBM processes caused by multi-physics processes coupling (e.g., adsorption-thermal-hydro-mechanical interactions) and fracture network complexity. We establish a hybrid framework (tSEDFM-ATHM-LSTM-BO), which enables accurate prediction and automatic optimization of  $\text{CH}_4$  production and  $\text{CO}_2$  sequestration. A  $R^2 > 96\%$  in validation tests was achieved. Key conclusions are as follows:

(1) This study developed a numerical model that couples the transient-source-function-based tSEDFM with the ATHM. By adding the transient fracture flow corrections and multiple-strain-change-induced complex permeability evolution, the simulation accuracy of  $\text{CO}_2$ - $\text{CH}_4$  flow in fractured coal reservoirs was significantly enhanced. Numerical and experimental validation confirmed the model's capability of capturing  $\text{CO}_2$ - $\text{CH}_4$  competitive adsorption and multiphysics coupling, with an average error below 10 %.

(2) A physics-constrained hybrid deep learning framework of the tSEDFM-ATHM-LSTM-BO is proposed. The LSTM network is trained with high-fidelity data generated by the tSEDFM-ATHM. The Bayesian optimization is utilized to automatically tune the network hyper-parameters (such as the learning rate and number of hidden layers). A  $R^2$  value of over 96 % for the prediction of  $\text{CH}_4$  production and  $\text{CO}_2$  sequestration was achieved. Meanwhile, combined with the recursive prediction method, long-term prediction of  $\text{CH}_4$  production and  $\text{CO}_2$  sequestration in the  $\text{CO}_2$ -ECBM process was conducted and applied in the field. This framework greatly shortens the calculation time and considers both physical mechanism interpretability and computational efficiency.

(3) Based on the proposed hybrid deep learning framework, a parametric sensitivity analysis of the  $\text{CO}_2$ -ECBM process was conducted. Results revealed that natural fractures enhance  $\text{CH}_4$  and  $\text{CO}_2$  transportation and production, but constrain the long-term  $\text{CO}_2$  sequestration due to easy breakthrough. The injection rate positively correlates with both production and sequestration capacity, whereas the injection period inversely impacts these metrics. The two operation parameters generate the most pronounced control on production-storage efficiency. Short-period injections enhance  $\text{CH}_4$  production through flow-dominant displacement, whereas long-term  $\text{CO}_2$  sequestration requires long-term adsorption stability without  $\text{CO}_2$  breakthrough;

(4) Field application involving a Qinshui Basin well-group model demonstrates that the hybrid framework achieves rapid optimization of  $\text{CO}_2$  injection operation parameters. The optimal injection rate ( $500 \text{ m}^3/\text{d}$ ) and period (20 days) were obtained, achieving a cumulative  $\text{CH}_4$  production of  $195.7 \times 10^4 \text{ m}^3$  and  $\text{CO}_2$  sequestration of  $21.5 \times 10^4 \text{ m}^3$  after 3200 days. This approach provides an efficient decision-making tool for  $\text{CO}_2$ -ECBM field operations.

# CRediT authorship contribution statement

**Tao Zhang:** Writing – original draft, Visualization, Validation, Methodology, Conceptualization. **Jianchun Guo:** Writing – review & editing, Supervision, Funding acquisition, Conceptualization. **Jie Zeng:** Writing – review & editing, Funding acquisition. **Lilong Wang:** Writing – review & editing. **Zhihong Zhao:** Writing – review & editing, Supervision. **Fanhui Zeng:** Supervision, Funding acquisition, Methodology. **Cong Lu:** Writing – review & editing.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgment

The authors gratefully acknowledge the support of the National Natural Science Foundation of China (U23B6004, 52374045 and 52404045), and the CAST Young Talent Support Program, Doctoral Student Special Project. We are very grateful to all those who have helped to improve this work. We also would like to express our sincere appreciation to the open-source software package, MRST, generously, provided by the Computational Geosciences group at SINTEF Digital.

# Data availability

Data will be made available on request.

# References

- [1] Xiang X, et al. *Investment feasibilities of CCUS technology retrofitting China's coal chemical enterprises with different CO2 geological sequestration and utilization approaches*. Int J Greenhouse Gas Control 2023;128:103960.
- [2] Clark A, Zhang W. *Estimating the Employment and Fiscal Consequences of Thermal Coal Phase-Out in China*. Energies 2022;15(3):800.
- [3] Moore TA. *Coalbed methane: A review*. Int J Coal Geol 2012;101:36–81.
- [4] Jia A, et al. *Forecast of natural gas supply and demand in China under the background of "Dual Carbon Targets"*. Pet Explor Dev 2023;50(2):492–504.
- [5] Li Q, et al. *Evolution characteristics of reservoir parameters during coalbed methane drainage via in-seam horizontal boreholes*. Powder Technol 2020;362:591–603.
- [6] Busch A, Gensterblum Y. *CBM and CO2-ECBM related sorption processes in coal: A review*. Int J Coal Geol 2011;87(2):49–71.
- [7] Liu T, et al. *Coal Permeability Evolution and Gas Migration Under Non-equilibrium State*. Transp Porous Media 2017;118(3):393–416.
- [8] Fang H, et al. *Numerical analysis of temperature effect on CO2 storage capacity and CH4 production capacity during the CO2-ECBM process*. Energy 2024;289:130022.
- [9] Yuan M, et al. *Modelling multicomponent gas diffusion and predicting the concentration-dependent effective diffusion coefficient of coal with application to carbon geo-sequestration*. Fuel 2023;339:127255.
- [10] Yang R, et al. *Modeling fishbones in coalbed methane reservoirs using a hybrid model formulation: Gas/water production performance in various lateral-cleat-network geometries*. Fuel 2019;244:592–612.
- [11] Zhu J, et al. *Two-phase flow model of coalbed methane extraction with different permeability evolutions for hydraulic fractures and coal reservoirs*. Energy Fuel 2021;35(11):9278–93.
- [12] Tan Y, et al. *Laboratory characterisation of fracture compressibility for coal and shale gas reservoir rocks: A review*. Int J Coal Geol 2019;204:1–17.
- [13] Liu Z, et al. *Effects of coal permeability rebound and recovery phenomenon on CO2 storage capacity under different coalbed temperature conditions during CO2-ECBM process*. Energy 2023;284:129196.
- [14] Tian J, et al. *An effective stress-dependent dual-fractal permeability model for coal considering multiple flow mechanisms*. Fuel 2023;334:126800.
- [15] Zhou HW, et al. *Effects of matrix-fracture interaction and creep deformation on permeability evolution of deep coal*. Int J Rock Mech Min Sci 2020;127:104236.
- [16] Liu Z, et al. *Effect of coal permeability evolution on CO2 storage capacity under phase partial pressure in ScCO2-ECBM processes*. Energy 2024;297:131298.
- [17] Liu X, et al. *Coupled adsorption-hydro-thermo-mechanical-chemical modeling for CO2 sequestration and well production during CO2-ECBM*. Energy 2023;262:125306.

- [18] Liu M, Mostaghimi P. Pore-scale modelling of CO<sub>2</sub> storage in fractured coal. Int J Greenhouse Gas Control 2017;66:246–53.
- [19] Lee SH, Lough MF, Jensen CL. Hierarchical modeling of flow in naturally fractured formations with multiple length scales. Water Resour Res 2001;37(3):443–55.
- [20] Olorode O, Wang B, Rashid HU. Three-Dimensional Projection-Based Embedded Discrete-Fracture Model for Compositional Simulation of Fractured Reservoirs. SPE J 2020;25(04):2143–61.
- [21] Zhou B, et al. A new analytically modified embedded discrete fracture model for pressure transient analysis in fluid flow. J Hydrol 2024;636:131330.
- [22] Zhang T, et al. A transient source-function-based embedded discrete fracture model for simulation of multiscale-fractured reservoir: Application in coalbed methane extraction. Gas Sci Eng 2025;133:205500.
- [23] Tan Q, et al. Energy-constrained production optimization for the in-situ conversion process of oil shale based on deep learning algorithms. Fuel 2024;368:131633.
- [24] Wang S, et al. A framework for predicting the production performance of unconventional resources using deep learning. Appl Energy 2021;295:117016.
- [25] Song X, et al. Time-series well performance prediction based on Long Short-Term Memory (LSTM) neural network model. J Pet Sci Eng 2020;186:106682.
- [26] Yang R, et al. Long short-term memory suggests a model for predicting shale gas production. Appl Energy 2022;322:119415.
- [27] Li X, et al. A physics-constrained long-term production prediction method for multiple fractured wells using deep learning. J Pet Sci Eng 2022;217:110844.
- [28] Sagheer A, Kotb M. Time series forecasting of petroleum production using deep LSTM recurrent networks. Neurocomputing 2019;323:203–13.
- [29] Xue Z, et al. A Combined Neural Network Forecasting Approach for CO<sub>2</sub>-Enhanced Shale Gas Recovery. SPE J 2024;29(08):4459–70.
- [30] Chen Z, et al. Engineering factor analysis and intelligent prediction of CO<sub>2</sub> storage parameters in shale gas reservoirs based on deep learning. Appl Energy 2025;377:124642.
- [31] Feng Z, et al. An encoder-decoder ConvLSTM surrogate model for simulating geological CO<sub>2</sub> sequestration with dynamic well controls. Gas Sci Eng 2024;125:205314.
- [32] Feng Z, et al. A hybrid CNN-transformer surrogate model for the multi-objective robust optimization of geological carbon sequestration. Adv Water Resour 2025;196:104897.
- [33] Yan B, et al. A robust deep learning workflow to predict multiphase flow behavior during geological CO<sub>2</sub> sequestration injection and Post-Injection periods. J Hydrol 2022;607:127542.
- [34] Yan B, et al. Physics-informed machine learning for reservoir management of enhanced geothermal systems. Geoenergy Sci Eng 2024;234:212663.
- [35] Xue H, et al. Predictive combination model for CH<sub>4</sub> separation and CO<sub>2</sub> sequestration with CO<sub>2</sub> injection into coal seams: VMD-STA-BiLSTM-ELM hybrid neural network modeling. Energy 2024;313:133744.
- [36] Wang H, et al. Lattice Boltzmann prediction of CO<sub>2</sub> and CH<sub>4</sub> competitive adsorption in shale porous media accelerated by machine learning for CO<sub>2</sub> sequestration and enhanced CH<sub>4</sub> recovery. Appl Energy 2024;370:123638.
- [37] Fang H, et al. Numerical analysis of permeability rebound and recovery evolution with THM multi-physical field models during CBM extraction in crushed soft coal with low permeability and its indicative significance to CO<sub>2</sub> geological sequestration. Energy 2023;262:125395.
- [38] Ye Z, et al. Two-phase flow properties in aperture-based fractures under normal deformation conditions: Analytical approach and numerical simulation. J Hydrol 2017;545:72–87.
- [39] Yang R, et al. A Semianalytical Approach To Model Two-Phase Flowback of Shale-Gas Wells With Complex-Fracture-Network Geometries. SPE J 2017;22(06):1808–33.
- [40] Zeng, J., et al. Characterization of Stress, Time-, and Temperature-Dependent Anisotropic Permeability for Deep Coal Rocks: A Strain-Driven and Multi-Mechanism Modelling Approach. in APOGCE. 2024. Perth, Australia: Society of Petroleum Engineers (SPE).
- [41] Zeng J, et al. Anisotropic Permeability Model for Coal Considering Stress Sensitivity, Matrix Anisotropic Internal Swelling/Shrinkage, and Gas Rarefaction Effects. Energy Fuel 2023;37(4):2811–32.
- [42] Sherstinsky A. Fundamentals of Recurrent Neural Network (RNN) and Long Short-Term Memory (LSTM) network. Physica D 2020;404:132306.
- [43] Mockus J. Application of Bayesian approach to numerical methods of global and stochastic optimization. J Glob Optim 1994;4(4):347–65.