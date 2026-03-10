

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the Journal of Hydrology](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the Journal of Hydrology

## Research papers

![Check for updates button](4f4b52340aaccb1bcf733468dca9ee03_img.jpg)

Check for updates button

# Short-term optimal scheduling rules extraction for hydro-solar-pumped storage complementary power systems based on orthogonal experimental design and a physics-constrained LSTM model

Lingwei Zhu<sup>a,b,c</sup>, Bin Xu<sup>a,b,\*</sup>, Xinrong Wang<sup>b</sup>, Huili Wang<sup>b</sup>, Xinman Qin<sup>b</sup>, Jiayi Jiang<sup>b</sup>, Jinshu Li<sup>d</sup>, William W.-G. Yeh<sup>c</sup>, Shanshui Yuan<sup>a,e,f</sup>, Wei Zhi<sup>a,b</sup>

<sup>a</sup> National Key Laboratory of Water Disaster Prevention, Hohai University, Xikang Road, Nanjing 210098, China

<sup>b</sup> College of Hydrology and Water Resources, Hohai University, Xikang Road, Nanjing 210098, China

<sup>c</sup> Department of Civil and Environmental Engineering, University of California, Los Angeles, CA 90095, USA

<sup>d</sup> Stantec, Pasadena, CA 91101, USA

<sup>e</sup> Department of Civil Engineering, Monash University, Clayton, Vic. 3800, Australia

<sup>f</sup> Key Laboratory of Hydrologic-Cycle and Hydrodynamic-System of Ministry of Water Resources, Hohai University, Nanjing 210098, China

##### ARTICLE INFO

This manuscript was handled by Dan Lu, Editor-in-Chief, with the assistance of Tiantian Yang, Associate Editor

###### Keywords:

Hydro-solar-pumped storage complementary power system  
Scheduling rules extraction  
Physical mechanisms  
Physics-constrained LSTM  
Efficient solution strategy  
Orthogonal experimental design

## ABSTRACT

To achieve efficient and physically consistent operation of a hydro-solar-pumped storage complementary power system (HSPSCPS), this study proposes a physics-constrained Long Short-Term Memory (PC-LSTM) model that integrates a two-stage scheduling rule and a structured output layer embedded with physical balance relationships. An orthogonal experimental design (OED) is first applied to compress high-dimensional operation scenarios and generate representative samples for model training. The proposed PC-LSTM model is compared with a standard LSTM and a physics-adjusted LSTM (PA-LSTM) in a case study. The conclusions are as follows: (1) The OED realized an 87.5 % scenario reduction; (2) The PC-LSTM model achieves the highest prediction accuracy with evaluation metrics  $R^2$  of 0.94, outperforming the two other models; (3) The constraint violation rate with respect to physical balance ( $PC\_CVR$ ) for LSTM, PA-LSTM, and PC-LSTM are 45.4 %, 2.54 %, and 0.46 %, respectively, demonstrating the superior capability of PC-LSTM in maintaining physical consistency; (4) The PC-LSTM model exhibits the highest model stability among all the three models; and (5) The PC-LSTM model outperforms the other two models in both total power output and grid load demand process. These findings confirm the effectiveness of incorporating a physics-constrained structured output layer into a LSTM model, providing a novel and practical approach for real-time operation of multi-energy power systems.

## 1. Introduction

With the large-scale integration of renewable energy and increasing complexity of power systems, renewable energy-dominated multi-energy complementary power systems face dual challenges (Cao et al., 2024; Fan and Hao, 2020). On the one hand, there are uncertainties associated with both supply and demand — including spatiotemporal fluctuations in runoff, intermittency of wind and solar power generation, and load demand variations, which amplify operational risks (Fan et al., 2024; Li et al., 2023; Fu et al., 2019). On the other hand, the growing diversity and quantity of power sources have increased the complexity of multi-energy operation scenarios, posing severe challenges to traditional scheduling rules. Consequently, there is an urgent

need to develop stable, widely applicable, and economically efficient optimal short-term scheduling strategies for large-scale multi-energy systems (Li et al., 2019; Yang et al., 2018).

Generally, there are two approaches to extract scheduling rules for multi-energy complementary systems: (1) model-driven explicit optimization models (EOMs) and (2) data-driven implicit optimization models (IOMs) (Celeste and Billib, 2009). In the first approach, an EOM generates deterministic scheduling rules from a mathematical model combined with probabilistic distributions or scenarios of inflow, wind and solar power generation, and grid demand load (Zhu et al., 2020; Xu et al., 2019). For example, Wang et al. (Wang et al., 2024) developed a day-ahead comprehensive optimization model for hydro-wind-solar hybrid systems considering renewable energy forecast uncertainties.

\* Corresponding author at: College of Hydrology and Water resources, Hohai University, No. 1 Xikang Road, Nanjing, 210098, PR China.  
E-mail address: [xubin\\_hhu@hhu.edu.cn](mailto:xubin_hhu@hhu.edu.cn) (B. Xu).

Shi et al. (Shi et al., 2024) proposed a stochastic two-stage optimization model for hydro-wind-solar complementary systems to determine the capacity allocation of cascade hydropower and renewable energy power stations. Lu et al. (2024) established an interval optimization model for hydro-solar complementary systems under extreme scenarios. While these models can reflect the physical characteristics of the systems, their complexity introduces critical limitations, and accurate uncertainty quantification remains challenging (Feng et al., 2019). Additionally, with the EOM approach, computational requirements grow exponentially with an increase of the number of state variables, leading to the “curse of dimensionality” (Giuliani et al., 2016), which limits its applicability to large-scale systems, particularly for real-time scheduling.

In the second approach, the IOM relies on a large amount of historical data to derive the relationship between input and output based on data mining techniques. This approach is straightforward but is significantly influenced by the choice of data mining algorithms. Li et al. (2022) formulated a long-term deterministic optimization model for hydro-solar-wind hybrid systems based on dynamic programming (DP) and derived linear scheduling functions via regression analysis. Ávila et al. (2021, 2020) employed Copula functions to jointly simulate runoff and wind speed scenarios as inputs for implicit stochastic optimization of hydro-wind systems. Ding et al. (2024) improved traditional reservoir operation rules by incorporating runoff and renewable energy power generation forecasting information. Zhang et al. (2025) constructed a multi-objective and multi-condition optimization model for a hydro-wind-solar hybrid system through knowledge graphs and proposed a corresponding solution framework. Feng et al. (2019) introduced a novel scheduling rules extraction approach based on the cluster-based evolutionary extreme learning machine (CEELM) model for reservoirs. Li et al. (2022) developed a particle swarm optimization-support vector machine (PSO-SVM) model for mid-to-long-term implicit stochastic scheduling in hydro-wind systems. Despite the rapid response capabilities, most research studies mentioned above are focused on linear models or shallow machine learning methods, which often oversimplify the intricate nonlinear relationships among multi-input and multi-output variables in large-scale systems and struggle to address high uncertainties of input factors in multi-energy complementary systems.

Emerging deep learning models have shown promise in decomposing complex nonlinear relationships and adapting to fluctuations in hydro-wind-solar power generation and load variations (Peng et al., 2019; Ma et al., 2019), with applications to wind and solar power forecasting (Shahid et al., 2023), runoff prediction (Wang et al., 2025), and reservoirs operation (Chen et al., 2025). Among the various machine learning models, the Long Short-Term Memory (LSTM) stands out. LSTM is a specialized recurrent neural network (RNN) algorithm that addresses gradient vanishing and explosion issues in traditional RNNs through memory cells and gating mechanisms (Hochreiter et al., 1996). Its parameter efficiency and physical interpretability make it advantageous for medium-scale data and time-sensitive engineering scenarios. However, when applying it to real-time operation for large-scale power systems, the following challenges remain:

- (1) Poor physical interpretability due to neglecting physical constraints (e.g., energy balance, equipment operational limitations) may lead to infeasible strategies (Nearing et al., 2021; Feng et al., 2022);
- (2) Higher computational requirements are needed with escalating response levels, growing scales, and scenario volumes;
- (3) Limited generalization abilities are exhibited in data-scarce regions or extreme conditions, coupled with overfitting risks (Lu et al., 2021).

Recently, some research studies have handled physical constraints in LSTM models through loss functions (Zheng et al., 2022). However, this approach treats physical constraints as soft penalties, which may still cause constraint violations when the model attempts to balance

prediction accuracy and constraint satisfaction during training. In particular, under complex nonlinear or limited training data, the model may fail to sufficiently enforce physical consistency, resulting in sub-optimal or even physically infeasible solutions.

To address the above-mentioned limitations, this paper proposes a physics-constrained LSTM (PC-LSTM) model with a structured output layer allied with orthogonal experimental design (OED) to develop a two-stage (“current to future”) short-term scheduling rule extraction for a hydro-solar-pumped storage complementary power system (HSPSCPS). First, we consider the high-dimensional nonlinear operational scenario space formed by uncertain inflow, solar, grid demand, and the interactive effects of dynamic constraints among power stations. We use OED to extract representative scenarios that exhibit balanced dispersion and comparability from full factorial experimental combinations. Second, we develop a short-term deterministic optimization model to maximize power generation, providing high-quality optimized results for training and validation of the three LSTM-based models. Third, we develop a two-stage scheduling function to consider decision variables involving the current and future stage and a LSTM model with a structured output layer in which physical constraints are embedded, enabling the internal gating mechanism to adaptively predict physics-constrained scheduling rules. With a proposed well-trained PC-LSTM model, a practical scheduling scheme that adheres to accuracy and physical consistency can be generated promptly for any given input condition. Finally, we compare the extraction results of the proposed PC-LSTM model with two other benchmark models through multi-dimensional evaluation metrics.

The proposed framework initially employs OED to reduce the dimensionality of operation scenarios, effectively mitigating the typically high training costs and computational requirements on machine learning models. Subsequently, the framework incorporates a two-stage scheduling rule formulation to consider decision variables both in the current and future operation time periods, aiming to improve the anticipatory capability and adaptability of the scheduling schemes. Finally, the proposed PC-LSTM model embeds physical relationships directly into the structured output layer, enabling the model to simultaneously exploit both data-driven and physics-informed advantages. This structural design embeds the physical relationships as structural constraints, which function as harder constraints than soft penalties (like loss functions), thereby substantially enhancing physical consistency and ensuring that the extracted scheduling rules are both accurate and physically feasible. The proposed framework provides support for robust real-time scheduling strategies for renewable energy-dominated multi-energy complementary power systems.

## 2. Methodology

This paper proposes a PC-LSTM model to develop a two-stage short-term scheduling rule extraction for a HSPSCPS. The framework of the methodology is shown in Fig. 1.

### 2.1. Orthogonal experimental design in operational scenario space reduction

The HSPSCPS faces complex challenges arising from the coupling of multiple uncertain inputs. Fig. 2 shows the multiple uncertain input factors, including the different inflow distributions, the high stochasticity of solar power, the uncertainty of grid load demand, and the different initial water storages. All these factors form a high-dimensional, nonlinear operational scenario space.

While conventional scenario generation methods, such as Monte Carlo simulation, are capable of capturing stochastic characteristics (Tavakoli and Karimi, 2022), they often lead to a combinatorial explosion in the number of scenarios, resulting in a severe “curse of dimensionality” in subsequent optimization. On the other hand, direct clustering or stochastic simulation approaches (Zhu et al., 2025) may

![A flowchart illustrating the design and evaluation of a physics-constrained LSTM model for hydro-solar pumped storage scheduling. The process starts with 'Orthogonal experimental design in operational scenario spaces reduction', which uses 'Orthogonal experimental design' and 'Multi input factors & levels' (including uncertainty-related and operational boundary factors) to generate 'Representative operation scenarios'. These scenarios are used to define the 'Short-term operation model for hydro-solar-pumped storage complementary power system', which has an 'Objective' (F1: Maximize total daily power generation, F2: Minimize water and solar curtailment) and 'Constraints' (Water/Energy storage balance, Load balance). The model uses 'Decision variables' (Qo_i^h, Qe_i^h, P_j^s_out, P_m_i^s_in, P_m_i^s_out) to find 'Optimized scheduling schemes of representative scenarios' via an optimization block (OC). The next step is 'Scheduling rules extraction for based on a physics-constrained LSTM model', which uses 'Two-stage scheduling rules' (Input variables X: Day index, Current stage, Future stage; Output variables Y: Current stage, Future stage) and 'Benchmark models' (Standard LSTM, PA-LSTM) to train a 'PC-LSTM Model'. The PC-LSTM Model features a 'Structured output layer' and a 'Dynamic weighting loss function'. Finally, the model is evaluated using 'Verification models' (LSTM, PA-LSTM, PC-LSTM) and 'Comprehensive evaluation metrics' (Accuracy, Physical consistency, Stability and generalization). The evaluation includes 'Experimental groups' (Training, Validation, Testing samples).](7055f51feb10ea4ea48b27c36f085286_img.jpg)

**Orthogonal experimental design in operational scenario spaces reduction**

**Orthogonal experimental design**

**Multi input factors & levels**

- (1) Uncertainty-related input factors
- (2) Operational boundary input factors

**Representative operation scenarios.**

**Short-term operation model for hydro-solar-pumped storage complementary power system**

**Objective**

**Constraints**

- Water/Energy storage balance
- Load balance ...

**Decision variables**

$$Q_{o,i}^h, Q_{e,i}^h, P_{j,i}^{s_{out}}, P_{m,i}^{s_{in}}, P_{m,i}^{s_{out}}$$

**Optimized scheduling schemes of representative scenarios.**

**Scheduling rules extraction for based on a physics-constrained LSTM model**

**Two-stage scheduling rules**

**Benchmark models**

Standard LSTM model  
PA-LSTM model

**PC-LSTM Model**

- (1) Structured output layer
- (2) Dynamic weighting loss function

**Verification And evaluation**

**Verification models**

- LSTM
- PA-LSTM
- PC-LSTM

**Comprehensive evaluation metrics**

- Accuracy:**  $RMSE, MAE, R^2$
- Physical consistency:**  $FBE, RFBE, WBE, RWBE, EBE, REBE, LBE, RLBE, CVR$
- Stability and generalization:**  $Loss\ Gap, RMSE\ Gap, AR^2$

**Experimental groups**

- Training samples (2/3)
- Validation samples (1/6)
- Testing samples (1/6)

A flowchart illustrating the design and evaluation of a physics-constrained LSTM model for hydro-solar pumped storage scheduling. The process starts with 'Orthogonal experimental design in operational scenario spaces reduction', which uses 'Orthogonal experimental design' and 'Multi input factors & levels' (including uncertainty-related and operational boundary factors) to generate 'Representative operation scenarios'. These scenarios are used to define the 'Short-term operation model for hydro-solar-pumped storage complementary power system', which has an 'Objective' (F1: Maximize total daily power generation, F2: Minimize water and solar curtailment) and 'Constraints' (Water/Energy storage balance, Load balance). The model uses 'Decision variables' (Qo\_i^h, Qe\_i^h, P\_j^s\_out, P\_m\_i^s\_in, P\_m\_i^s\_out) to find 'Optimized scheduling schemes of representative scenarios' via an optimization block (OC). The next step is 'Scheduling rules extraction for based on a physics-constrained LSTM model', which uses 'Two-stage scheduling rules' (Input variables X: Day index, Current stage, Future stage; Output variables Y: Current stage, Future stage) and 'Benchmark models' (Standard LSTM, PA-LSTM) to train a 'PC-LSTM Model'. The PC-LSTM Model features a 'Structured output layer' and a 'Dynamic weighting loss function'. Finally, the model is evaluated using 'Verification models' (LSTM, PA-LSTM, PC-LSTM) and 'Comprehensive evaluation metrics' (Accuracy, Physical consistency, Stability and generalization). The evaluation includes 'Experimental groups' (Training, Validation, Testing samples).

**Fig. 1.** Framework of the methodology

discard critical extreme operation scenarios, thereby undermining the robustness of the derived scheduling rules.

To balance computational efficiency and scenario fidelity, this study employs an OED for scenario reduction. Taking advantage of the uniform dispersion and comparability properties of orthogonal arrays, the OED systematically selects representative scenarios from the full factorial combinations, which ensures the reduced scenarios maintain statistical consistency and physical completeness, thereby enhancing the efficiency and tractability of the optimization model (Feng et al., 2017).

#### 2.1.1. Orthogonal experimental design

OED is an efficient method for designing experiments involving multiple factors and multiple levels, and has been widely applied across various fields (Yun et al., 2025; Zhang et al., 2025). Rather than exhaustively enumerating all possible scenarios, OED selects a statistically representative subset of orthogonal sample points from full factorial experimental sample points based on orthogonality (as illustrated in Fig. 3). This structured approach significantly reduces the scale of experiments, thereby improving the computational efficiency of the optimization model. Furthermore, the constructed orthogonal arrays strictly

![Figure 2: Four plots showing uncertain input factors for a hydro-solar-pumped storage power system. Top-left: Flow rate (m³/s) vs Hour (h) with 12 probability density functions. Top-right: Input solar power (10⁴kW) vs Hour (h) with multiple time series. Bottom-left: Grid load demand (10⁴kW) vs Hour (h) with a shaded uncertainty region. Bottom-right: Input solar power (10⁴kW) vs Hour (h) with multiple time series.](7fb5215fd72210a2e4cce6df55550c89_img.jpg)

Figure 2: Four plots showing uncertain input factors for a hydro-solar-pumped storage power system. Top-left: Flow rate (m³/s) vs Hour (h) with 12 probability density functions. Top-right: Input solar power (10⁴kW) vs Hour (h) with multiple time series. Bottom-left: Grid load demand (10⁴kW) vs Hour (h) with a shaded uncertainty region. Bottom-right: Input solar power (10⁴kW) vs Hour (h) with multiple time series.

Fig. 2. Examples of multiple uncertain input factors to complementary operation on a hydro-solar-pumped storage power system.

![Figure 3: Illustration of orthogonal experimental design. Left: A 3D cube representing the factor space with axes for Factor 1, Factor 2, and Factor 3, each with three levels. Right: A 3D grid showing sample points (orange circles) and orthogonal sample points (red circles) at the intersections of the factor levels.](b7251436a2a3c0d1c00c3e935df2a8f5_img.jpg)

Figure 3: Illustration of orthogonal experimental design. Left: A 3D cube representing the factor space with axes for Factor 1, Factor 2, and Factor 3, each with three levels. Right: A 3D grid showing sample points (orange circles) and orthogonal sample points (red circles) at the intersections of the factor levels.

Fig. 3. Illustration of orthogonal experimental design.

satisfy two fundamental statistical properties — uniform dispersion and comparability — ensuring that all factor-level combinations are evenly distributed across the sample space. These properties eliminate experimental bias and provide a robust baseline for comparative analysis.

#### 2.1.2. Reducing operational scenario space for model training

The high-dimensional operational scenario space of HSPSCPS arises from the combinatorial expansion of multiple operation factors with multiple levels. In practical operations, there are two main categories of input factors which have to be considered:

- (1) Uncertainty-related input factors: inflow, solar power, and grid load demand;
- (2) Operational boundary input factors: initial water storage of hydropower stations, operational water level limits of hydropower stations, outflow constraints of hydropower stations, power

generation limits of all power stations, initial and ending water storage of pumped-storage power stations, and electricity transmission route capacity.

To enhance the efficiency of model training while maintaining accuracy, this study adopts a simplified treatment of input factors. Most operational boundary conditions are regarded as constant under given system operational conditions and, therefore, do not necessitate the design of multi-level experimental scenarios. Accordingly, the operation scenario space primarily will be constructed based on multiple levels of uncertainty-related input factors and initial water storage of hydropower stations.

### 2.2. Short-term operation model for hydro-solar-pumped storage complementary power system

The short-term and real-time operation objective of a HSPSCPS is to maximize the comprehensive benefit from energy production and enhance stability of power supply with the goal of aligning short-term operational decisions with mid- to long-term requirements of hydro-power stations.

This study develops a short-term (hourly) optimization operation model aimed at maximizing total daily power generation, simultaneously considering practical operational constraints, including water and energy storage constraints, load constraints, and capacity of electricity transmission routes. The deterministic optimized results are obtained through LINGO (Inc, 2021) and the optimized results subsequently are used as input data for training, validation, and testing of the LSTM models.

#### 2.2.1. Objective function

With the objective of maximizing total on-grid power generation, the model also seeks to minimize water and solar curtailment while making full use of electricity transmission route capacity to meet grid load demand. The total on-grid power includes hydropower, on-grid solar power, and pumped-storage generation power. The objective function can be formulated as Eq. (2.1):

$$\begin{aligned} \text{obj} = \max \sum_{t=1}^{T} \left( \sum_{i=1}^{I} P_{i,t}^h + \sum_{j=1}^{J} P_{j,t}^{\text{s-grid}} + \sum_{m=1}^{M} P_{m,t}^{\text{ps-out}} - m_i^h \sum_{i=1}^{I} P_{i,t}^{\text{hs}} - m_j^s \right. \\ \left. \times \sum_{j=1}^{J} P_{j,t}^{\text{ss}} \right) \cdot \Delta t \end{aligned} \quad (2.1)$$

#### 2.2.2. Constraints

The constraints include the following:

- (1) Water storage balance constraints (considering runoff time lag from upstream reservoir to downstream reservoir) can be formulated as Eqs. (2.2)–(2.5).

$$V_{i,t+1}^h = V_{i,t}^h + (Q_{i,t}^h - Q_{i,t}^o) \cdot \Delta t \quad (2.2)$$

$$Q_{i,t}^h = Qn_{i,t}^h + Qr_{i,t}^h \quad (2.3)$$

$$Qo_{i,t}^h = Qe_{i,t}^h + Qs_{i,t}^h \quad (2.4)$$

$$Qr_{i,t}^h = \begin{cases} 0, & i = 1 \\ f_i(Qo_{i-1,t}^h), & i = 2, 3 \dots I \end{cases} \quad (2.5)$$

where  $f_i(\cdot)$  denotes a flow conversion function that describes the hydrological connection between hydropower station  $i$  and  $i-1$ .

- (2) Energy storage balance constraints (for pumped-storage power stations) can be formulated as Eq. (2.6).

$$E_{m,t+1}^{\text{ps}} = E_{m,t}^{\text{ps}} + (\eta \cdot P_{m,t}^{\text{ps-in}} - P_{m,t}^{\text{ps-out}}) \cdot \Delta t \quad (2.6)$$

- (3) Water/Energy storage capacity constraints can be formulated as Eqs. (2.7) and (2.8).

$$V_{i,t}^h \le V_{i,t}^h \le \bar{V}_{i,t}^h \quad (2.7)$$

$$0 \le E_{m,t}^{\text{ps}} \le \bar{E}_m^{\text{ps}} \quad (2.8)$$

- (4) Initial and ending water/ energy storage constraints

According to the designed operational rules of hydropower stations, the ending water storage of annual and seasonal regulation hydropower stations may vary within a reasonable range, whereas water storage of daily regulation hydropower stations must be maintained at a consistent value at both the beginning and end of the operation period. They can be formulated as Eqs. (2.9)–(2.11).

Annual/seasonal regulation:

$$\begin{aligned} V_{i,1}^h &= V_{i,0}^h \\ V_{i,0}^h - \Delta V_i^h &\le V_{i,T+1}^h \le V_{i,0}^h + \Delta V_i^h \end{aligned} \quad (2.9)$$

Daily regulation:

$$\begin{aligned} V_{i,1}^h &= V_{i,0}^h \\ V_{i,T+1}^h &= V_{i,0}^h \end{aligned} \quad (2.10)$$

Energy storage of pumped-storage power stations should remain the same at both the beginning and end of the operation period.

Pumped-storage power stations:

$$\begin{aligned} E_{m,1}^{\text{ps}} &= E_{m,0}^{\text{ps}} \\ E_{m,T+1}^{\text{ps}} &= E_{m,0}^{\text{ps}} \end{aligned} \quad (2.11)$$

- (5) Hydraulic head constraints can be formulated as Eqs. (2.12)–(2.15).

$$H_{i,t}^h \le H_{i,t}^h \le \bar{H}_{i,t}^h \quad (2.12)$$

$$H_{i,t}^h = Zup_{i,t}^h - Zdown_{i,t}^h \quad (2.13)$$

$$Zup_{i,t}^h = f_{vz} \left( \frac{V_{i,t}^h + V_{i,t+1}^h}{2} \right) \quad (2.14)$$

$$Zdown_{i,t}^h = f_{oq} (Qo_{i,t}^h) \quad (2.15)$$

where  $f_{vz}(\cdot)$  denotes the conversion relationship between water storage and water level; and  $f_{oq}(\cdot)$  denotes the conversion relationship between water release and water level.

- (6) Ecological water release constraints can be formulated as Eq. (2.16).

$$Qo_{i,t}^h \ge \underline{Qo}_{i,t}^h \quad (2.16)$$

- (7) Water release for power generation constraints can be formulated as Eq. (2.17).

$$Qe_{i,t}^h \le \bar{Qe}_{i,t}^h \quad (2.17)$$

- (8) Power output constraints can be formulated as Eqs. (2.18)–(2.24).

Hydropower stations:

$$P_{i,t}^h \le P_{i,t}^h \le \bar{P}_{i,t}^h \quad (2.18)$$

$$P_{i,t}^h = k_i \cdot Qe_{i,t}^h \cdot H_{i,t}^h \quad (2.19)$$

In this study, the pumping power is exclusively supplied by solar power output, as represented in Eq. (2.22).

Solar power stations:

$$P_{j,t}^{\text{s-out}} \le P_{j,t}^{\text{s-out}} \le \bar{P}_{j,t}^{\text{s-out}} \quad (2.20)$$

$$p_{j,t}^{s,in} = p_{j,t}^{s,out} + p_{j,t}^{s} \quad (2.21)$$

$$p_{j,t}^{s,out} = p_{j,t}^{s,grid} + p_{j,t}^{s,in} \quad (2.22)$$

Since the pumped-storage power stations are restricted from operating in both pumping and generating modes simultaneously, the Eq. (2.24) is represented in LINGO as a bilinear constraint, the model will be solved through LINGO's Global Solver.

Pumped-storage power stations:

$$\underline{p}_{m,t}^{ps,in} \le p_{m,t}^{ps,in} \le \overline{p}_{m,t}^{ps,in} \quad (2.23)$$

$$\underline{p}_{m,t}^{ps,out} \le p_{m,t}^{ps,out} \le \overline{p}_{m,t}^{ps,out} \quad (2.24)$$

$$p_{m,t}^{ps,in} \cdot p_{m,t}^{ps,out} = 0 \quad (2.24)$$

##### (9) Electricity transmission routes

To prevent overload on transmission routes, the total on-grid power delivered to the external grid cannot exceed the transmission capacity of the electricity transmission routes. All the transmission constraints can be formulated as Eqs. (2.25)–(2.29).

$$p_t^{grid} \le \overline{p} \quad (2.25)$$

$$p_t^{grid} = \sum_{i=1}^{I} p_{i,t}^h + \sum_{j=1}^{J} p_{j,t}^{s,grid} + \sum_{m=1}^{M} p_{m,t}^{ps,out} \quad (2.26)$$

Hydropower stations:

$$p_{i,t}^h \le \overline{chan}_{i,t}^h \quad (2.27)$$

Solar power stations:

$$p_{j,t}^{s,out} \le \overline{chan}_{j,t}^s \quad (2.28)$$

Pumped-storage power stations:

$$p_{j,t}^{s,grid} + p_{m,t}^{ps,out} \le \overline{chan}_{m,t}^{ps} \quad (2.29)$$

$$p_{m,t}^{ps,in} \le \overline{chan}_{m,t}^{ps}$$

##### (10) Grid demand load

The total on-grid power supply from hydropower, solar, and pumped-storage pumping or generation cannot exceed the grid demand load to prevent curtailment at each time step. These constraints can be formulated as Eqs. (2.30) and (2.31).

$$p_t^{grid} \le L_t \quad (2.30)$$

$$D_t = L_t - p_t^{grid} \quad (2.31)$$

#### 2.2.3. Decision variables

This model focuses on the comprehensive benefit and stability of power supply on the short-term (hourly) scheduling rules of HSPSCPS. The decision variables are the total release  $Q_{i,t}^h$  and release for power generation  $Q_{i,t}^h$  of hydropower stations, solar power output  $p_{j,t}^{s,grid}$ ,  $p_{j,t}^{s,out}$  and pumped-storage pumping power output  $p_{m,t}^{ps,in}$ , and generation power output  $p_{m,t}^{ps,out}$  in each time period. All input variables and output variables can be seen in Table 1.

**Table 1**  
Input and output variables of LINGO model.

| Input variables               |                                   | Output variables              |                                                                                      |
|-------------------------------|-----------------------------------|-------------------------------|--------------------------------------------------------------------------------------|
| Hydropower stations           | $V_{i,0}^h, Q_{i,t}^h, Q_{i,t}^h$ | Hydropower stations           | $Q_{i,t}^h, Q_{i,t}^h, V_{i,t}^h$                                                    |
| Solar power stations          | $p_{j,t}^{s,in}$                  | Solar power stations          | $H_{i,t}^h, p_{j,t}^{s,out}$                                                         |
| Pumped-storage power stations | $E_{m,0}^{ps}, E_{m,T+1}^{ps}$    | Pumped-storage power stations | $p_{j,t}^{s,grid}, p_{j,t}^{s,out}, p_{m,t}^{ps,in}, p_{m,t}^{ps,out}, E_{m,t}^{ps}$ |
| Grid load demand              | $L_t$                             | Residual grid load demand     | $D_t$                                                                                |

### 2.3. Scheduling rules extraction for hydro-solar-storage complementary power systems based on a physics-constrained LSTM model

#### 2.3.1. A two-stage scheduling rule considering physical constraints

Short-term operation of a HSPSCPS is influenced by multiple sources of uncertainty, including spatiotemporal variations in inflow, high stochasticity of solar power, and fluctuations in load demand. However, most hourly scheduling methods typically rely on static rules or normal strategies based on predetermined scenarios. These rules usually overlook the physical relationships in the power systems and are inadequate for effectively adapting to real-time changes in system operating conditions. To enhance the physical feasibility and forward-looking insight of scheduling strategies, this study proposes a physics-constrained two-stage scheduling rule through a physics-constrained LSTM output layer and decision variables involving the current and future stages.

##### (1) A general scheduling rule

Fig. 4 shows a typical HSPSCPS. The scheduling rule of the system essentially serves as an output control function under varying input conditions. Considering the short-term operation characteristics of this system, the general input and output variables are exactly the same with the LINGO model, and they can be formulated as Eq. (2.32):

$$(\widehat{Q}_{i,t}^h, \widehat{Q}_{i,t}^h, \widehat{p}_{j,t}^{s,out}, \widehat{p}_{m,t}^{ps,in}, \widehat{p}_{m,t}^{ps,out}) = f_1(t, V_{i,t}^h, Q_{i,t}^h, Q_{i,t}^h, p_{j,t}^{s,in}, E_{m,t}^{ps}, E_{m,T+1}^{ps}, L_t) \quad (2.32)$$

where  $f_1(\cdot)$  denotes a general scheduling rule of the power system; variables with a hat ( $\widehat{\cdot}$ ) denote output variables predicted by the LSTM models.

##### (2) A physics-constrained two-stage scheduling rule

The general scheduling rule in Eq. (2.32) rely solely on the state variables of the current period. The proposed physics-constrained two-stage scheduling rule in Eq. (2.34) will take essential physical constraints — hydraulic connection, water storage balance, energy storage balance, load balance — into account through introducing the physical derived variables  $\widehat{V}_{i,t+1}^h, \widehat{V}_{i,T+1}^h, \widehat{Q}_{i,t}^h, \widehat{RQ}_{i,t}^h, \widehat{P}_{i,t}^h, \widehat{RP}_{i,t}^h, \widehat{E}_{m,t+1}^{ps}, \widehat{D}_t, \widehat{RD}_t$  to ensure the physical feasibility of the scheduling rules. Furthermore, the proposed physics-constrained two-stage scheduling rule requires forecast input variables  $RQ_{i,t}^h, RQ_{i,t}^h, RP_{j,t}^{s,in}$  and decision variables  $\widehat{RQ}_{i,t}^h, \widehat{RQ}_{i,t}^h, \widehat{RP}_{i,t}^h, \widehat{RP}_{j,t}^{s,out}, \widehat{RP}_{m,t}^{ps,out}, \widehat{RP}_{m,t}^{ps,in}, \widehat{RD}_t$  for the remaining operation time periods to concurrently obtain real-time rolling decisions for the current stage and anticipatory decisions for the future stages to realize proactive insight into future operation. These variables can be calculated using Eq. (2.33), representing the average values for the remaining time periods. For example, the term  $\widehat{Q}_{i,t}^h$  denotes the current release and  $\widehat{RQ}_{i,t}^h$  denotes the average release in the remaining 23 hours when  $t = 1$ .

![Fig. 4. Schematic diagram of the system topology. The diagram shows a central 'Operation center' (OC) box. Above it, a blue box represents a 'Hydropower station' with multiple stages (1, 2, ..., i, ..., d) showing inflow (Qn_{i,t}^h), volume (V_{i,t}^h), and outflow (Qo_{i,t}^h) with power P_{i,t}^h. To the left, an orange box represents a 'Solar power station' with multiple stages (1, 2, ..., j, ..., d) showing inflow (Ps_{i,t}^{s,in}) and outflow (Ps_{i,t}^{s,out}) with power Ps_{i,t}^{s,out}. Below the OC, a blue box represents a 'Pumped-storage power station' with multiple stages (1, 2, ..., i, ..., d) showing inflow (Ps_{i,t}^{ps,in}), outflow (Ps_{i,t}^{ps,out}), and energy (E_{i,t}^{ps}) with power Ps_{i,t}^{ps,out}. Arrows indicate electricity transmission routes (solid black) and natural/internal inflow (solid blue) and inflow/release of hydropower stations (dashed blue).](a738993919a50143787084ee7ce6e2f2_img.jpg)

Fig. 4. Schematic diagram of the system topology. The diagram shows a central 'Operation center' (OC) box. Above it, a blue box represents a 'Hydropower station' with multiple stages (1, 2, ..., i, ..., d) showing inflow (Qn\_{i,t}^h), volume (V\_{i,t}^h), and outflow (Qo\_{i,t}^h) with power P\_{i,t}^h. To the left, an orange box represents a 'Solar power station' with multiple stages (1, 2, ..., j, ..., d) showing inflow (Ps\_{i,t}^{s,in}) and outflow (Ps\_{i,t}^{s,out}) with power Ps\_{i,t}^{s,out}. Below the OC, a blue box represents a 'Pumped-storage power station' with multiple stages (1, 2, ..., i, ..., d) showing inflow (Ps\_{i,t}^{ps,in}), outflow (Ps\_{i,t}^{ps,out}), and energy (E\_{i,t}^{ps}) with power Ps\_{i,t}^{ps,out}. Arrows indicate electricity transmission routes (solid black) and natural/internal inflow (solid blue) and inflow/release of hydropower stations (dashed blue).

Fig. 4. Schematic diagram of the system topology.

$$\widehat{RQo}_{it}^h = \begin{cases} \frac{1}{T-t} \sum_{r=t+1}^{T} \widehat{Qo}_{ir}^h, & t = 1, 2, \dots, T-1 \\ 0, & t = T \end{cases} \quad (2.33)$$

$$\begin{aligned} X &= (t, V_{it}^h, Qn_{it}^h, Qo_{it}^h, RQn_{it}^h, RQo_{it}^h, Ps_{jt}^{s,in}, Ps_{jt}^{s,out}, \\ &\quad E_{mt}^{ps,out}, E_{mt}^{ps,in}, E_{m,T+1}^{ps}, RE_{mt}^{ps,out}, RE_{mt}^{ps,in}, L_t, RL_t) \\ Y &= (\widehat{V}_{it+1}^h, \widehat{V}_{it+1}^h, \widehat{Qo}_{it}^h, \widehat{Qe}_{it}^h, \widehat{Qo}_{it}^h, \widehat{RQo}_{it}^h, \widehat{RQe}_{it}^h, \widehat{RQo}_{it}^h, \widehat{P}_{it}^h, \widehat{RP}_{it}^h, \\ &\quad \widehat{P}_{jt}^{s,out}, \widehat{RP}_{jt}^{s,out}, \widehat{E}_{m,T+1}^{ps}, \widehat{P}_{mt}^{ps,out}, \widehat{RP}_{mt}^{ps,out}, \widehat{P}_{mt}^{ps,in}, \widehat{RP}_{mt}^{ps,in}, \widehat{D}_t, \widehat{RD}_t) \\ Y &= f_2(X) \end{aligned} \quad (2.34)$$

where  $f_2(\cdot)$  denotes the proposed scheduling rule of the power system.

#### 2.3.2. Physics-constrained LSTM model with a structured output layer

##### (1) Definition

The Long Short-Term Memory model was proposed by Hochreiter and Schmidhuber in 1997 (Hochreiter Sas, 1997). It is a deep learning network capable of capturing long-range dependencies in time series. LSTM introduces a gating mechanism to regulate the flow of information among the sequences based on the Recurrent Neural Network (RNN). The memory cells are coherently transmitted across sequences, effectively addressing the limitation of long-term dependency in time series data (Kratzert et al., 2019).

The mathematical formulations of an LSTM model are presented in Eqs. (2.35)–(2.37). Let the current memory cell state in the LSTM be denoted as  $C_t$ , the input vector as  $x_t$ , and the predicted output as  $\widehat{y}_t$ . The gating variables — forget gate, input gate, and output gate — are denoted as  $f_t$ ,  $i_t$  and  $o_t$ , respectively.

$$f_t = \sigma(W_f[h_{t-1}, x_t] + b_f) \quad (2.35)$$

![Fig. 5. Illustration of the two-stage rolling scheduling framework. The figure shows three sequential plots of flow Q (m³/s) versus time t (h). The first plot shows the initial state with forecasted inflow Qn_{i,t}^h and outflow Qo_{i,t}^h, and predicted outflow RQo_{i,t}^h. The second plot shows the next time step with updated forecasts and predictions. The third plot shows the final state with the latest forecasts and predictions. Dashed arrows indicate the rolling update process from one time step to the next.](f6c63daa87b1f2bde4b871f3d540e85b_img.jpg)

Fig. 5. Illustration of the two-stage rolling scheduling framework. The figure shows three sequential plots of flow Q (m³/s) versus time t (h). The first plot shows the initial state with forecasted inflow Qn\_{i,t}^h and outflow Qo\_{i,t}^h, and predicted outflow RQo\_{i,t}^h. The second plot shows the next time step with updated forecasts and predictions. The third plot shows the final state with the latest forecasts and predictions. Dashed arrows indicate the rolling update process from one time step to the next.

Fig. 5. Illustration of the two-stage rolling scheduling framework.

$$i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i) \quad (2.36)$$

$$o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o) \quad (2.37)$$

where  $t$  denotes the current time step;  $\sigma(\bullet)$  represents the sigmoid activation function;  $h_{t-1}$  is the hidden state of the last time step;  $W_f, W_i, W_o$  are the weight matrices corresponding to the forget gate, input gate, and output gate, respectively; and  $b_f, b_i, b_o$  are the corresponding bias terms for each gate.

Then, based on the gating mechanism of the input gate and forget gate, the memory cell state at the current time step  $C_t$  is calculated through Eqs. (2.38) and (2.39).

$$\tilde{C}_t = \tanh(W_c \cdot [h_{t-1}, x_t] + b_c) \quad (2.38)$$

$$C_t = f_t \cdot C_{t-1} + i_t \cdot \tilde{C}_t \quad (2.39)$$

where  $\tilde{C}_t$  represents the candidate memory at the current time step, and  $C_{t-1}$  denotes the memory cell state from the previous time step.

Finally, based on the gating mechanism of the output gate, the hidden state  $h_t$  is computed through Eq. (2.40), which is then used to generate the final output  $\hat{y}_t$  through Eq. (2.41).

$$h_t = o_t \odot \tanh(C_t) \quad (2.40)$$

$$\hat{y}_t = W_y \cdot h_t + b_y \quad (2.41)$$

where  $h_t$  denotes the hidden state of the current time step;  $\tanh(\bullet)$  represents the hyperbolic tangent activation function; and  $W_y, b_y$  denote the gating mechanism parameters of the output gate.

##### (2) Physics-constrained LSTM model with a structured output layer

To address the limitation of physical interpretability in data-driven LSTM models, this study proposes a machine learning framework that integrates a bi-directional LSTM network with a structured output layer to extract the scheduling rules for a HSPSCPS.

##### a) Structured output layer of the LSTM Model

A decoupling mechanism between free and physical derived output variables is introduced after the standard LSTM output gate, as shown in Fig. 6. In this framework, the internal gating mechanism of the LSTM is responsible for controlling the free output variables, while the structured output layer is tasked with inferring derived output variables through the physical relationships, as in Eq. (2.43). The final output  $\hat{y}_t$  is formulated through Eq. (2.42).

$$\begin{aligned} \hat{y}_t^{\text{free}} &= W_{\text{free}} \cdot h_t + b_{\text{free}} \\ \hat{y}_t^{\text{derived}} &= F_{\text{physics}}(\hat{y}_t^{\text{free}}, x_t) \\ \hat{y}_t &= [\hat{y}_t^{\text{free}}, \hat{y}_t^{\text{derived}}] \end{aligned} \quad (2.42)$$

where  $\hat{y}_t^{\text{free}}, \hat{y}_t^{\text{derived}}$  represent the free and derived output variables, respectively, and  $W_{\text{free}}, b_{\text{free}}$  denote the gating mechanism parameters of output gate associated with the free output variables.

![Diagram illustrating the LSTM Model with a structured output layer. The model consists of an Input Layer, multiple hidden layers (Layer 1 to Layer L), and an Output Layer. The Input Layer provides inputs x_1, x_2, ..., x_{t-1}, x_t to the LSTM cells. The hidden layers process these inputs sequentially, with Layer 1 receiving x_1 and Layer L receiving x_t. Each layer contains LSTM cells that output hidden states h_t^{l,1}, h_t^{l,2}, ..., h_t^{l,L} and cell states c_t^{l,1}, c_t^{l,2}, ..., c_t^{l,L}. The final hidden and cell states h_t, c_t are passed to the Output Layer. The Output Layer contains two components: a free output component \hat{y}_t^{\text{free}} = W_{\text{free}} \cdot h_t + b_{\text{free}} and a derived output component \hat{y}_t^{\text{derived}} = F_{\text{physics}}(\hat{y}_t^{\text{free}}, x_t). The final output \hat{y}_t is a concatenation of these two components.](f4535959316aea381fb56b9225d8e4bd_img.jpg)

Diagram illustrating the LSTM Model with a structured output layer. The model consists of an Input Layer, multiple hidden layers (Layer 1 to Layer L), and an Output Layer. The Input Layer provides inputs x\_1, x\_2, ..., x\_{t-1}, x\_t to the LSTM cells. The hidden layers process these inputs sequentially, with Layer 1 receiving x\_1 and Layer L receiving x\_t. Each layer contains LSTM cells that output hidden states h\_t^{l,1}, h\_t^{l,2}, ..., h\_t^{l,L} and cell states c\_t^{l,1}, c\_t^{l,2}, ..., c\_t^{l,L}. The final hidden and cell states h\_t, c\_t are passed to the Output Layer. The Output Layer contains two components: a free output component \hat{y}\_t^{\text{free}} = W\_{\text{free}} \cdot h\_t + b\_{\text{free}} and a derived output component \hat{y}\_t^{\text{derived}} = F\_{\text{physics}}(\hat{y}\_t^{\text{free}}, x\_t). The final output \hat{y}\_t is a concatenation of these two components.

Fig. 6. Illustration of the LSTM Model with a structured output layer.

$$F_{physics} = \left\{ \begin{array}{l} \widehat{Q}_{i,t}^h = \begin{cases} Qn_{i,t}^h, i=1 \\ Qn_{i,t}^h + Qr_{i,t}^h, i=2,3\dots I \end{cases} \\ \widehat{RQ}_{i,t}^h = \begin{cases} RQn_{i,t}^h, i=1 \\ RQn_{i,t}^h + RQr_{i,t}^h, i=2,3\dots I \end{cases} \\ \widehat{V}_{i,t+1}^h = V_{i,t}^h + \left( \widehat{Q}_{i,t}^h - \widehat{Q}_{i,t}^h \right) \cdot \Delta t + \left( \widehat{RQ}_{i,t}^h - \widehat{RQ}_{i,t}^h \right) \cdot (T-t) \cdot \Delta t \\ \widehat{P}_{i,t}^h = k \cdot \widehat{Q}_{i,t}^h \cdot H_{i,t}^h \\ \widehat{RP}_{i,t}^h = k \cdot \widehat{RQ}_{i,t}^h \cdot RH_{i,t}^h \\ \widehat{E}_{m,t+1}^{ps} = E_{m,t}^{ps} + \left( \eta \cdot \widehat{P}_{m,t}^{ps.in} - \widehat{P}_{m,t}^{ps.out} \right) \cdot \Delta t \\ E_{m,t}^{ps} = E_{m,t}^{ps} + \left( \eta \cdot \widehat{P}_{m,t}^{ps.in} - \widehat{P}_{m,t}^{ps.out} \right) \cdot \Delta t + \left( \widehat{RP}_{m,t}^{ps.in} - \widehat{RP}_{m,t}^{ps.out} \right) \cdot (T-t) \cdot \Delta t \\ \widehat{D} = L_t - \widehat{P}_{i,t}^h - \widehat{P}_{j,t}^{grid} - \widehat{P}_{m,t}^{ps.out} \\ \widehat{RD} = RL_t - \widehat{RP}_{i,t}^h - \widehat{RP}_{j,t}^{grid} - \widehat{RP}_{m,t}^{ps.out} \end{array} \right. \quad (2.43)$$

where  $F_{physics}(\cdot)$  denotes the physical relationship formulations among the derived output variables, input variables, and free output variables. The physical relationship considered in  $F_{physics}(\cdot)$  includes hydraulic connection, water storage balance, power generation conversion, energy storage balance, and load balance.

##### b) Loss function coupled with dynamic weighting strategy

When the relationship between free output variables and derived output variables is highly nonlinear, training the model merely based on the free output variables may lead to significant errors in the derived quantities, thereby compromising the overall physical rationality of the output variables. To mitigate this problem, this study introduces an auxiliary constraint mechanism based on the error of derived output variables and employs a dynamic weighting strategy to balance the contributions of different loss components, as shown in Eqs. (2.44) and (2.45). This design aims to enhance the model's sensitivity to physical laws and improve convergence efficiency throughout the training process.

$$\begin{aligned} loss_y^{free} &= \frac{1}{n_f} \frac{1}{n_t} \sum_{n=1}^{n_f} \sum_{t=1}^{n_t} |y_{n,t}^{free} - \widehat{y}_{n,t}^{free}| \\ loss_y^{derived} &= \frac{1}{n_d} \frac{1}{n_t} \sum_{n=1}^{n_d} \sum_{t=1}^{n_t} |y_{n,t}^{derived} - \widehat{y}_{n,t}^{derived}| \end{aligned} \quad (2.44)$$

where  $loss_y^{free}$ ,  $loss_y^{derived}$  denote the prediction loss functions for the free and derived output variables, respectively;  $n_f$ ,  $n_d$ ,  $n_t$  represent the number of free output variables, derived output variables, and total samples, respectively;  $y_t^{free}$ ,  $y_t^{derived}$  are the observed values for the free and derived output variables, respectively; and  $\widehat{y}_t^{free}$ ,  $\widehat{y}_t^{derived}$  are the predicted values for the free and derived output variables, respectively.

$$\begin{aligned} loss_y &= loss_y^{free} + \lambda_{phy} \cdot loss_y^{derived} \\ \lambda_{phy}(e) &= \lambda_{phy}(0) \cdot e^{-k \cdot e} \end{aligned} \quad (2.45)$$

where  $loss_y$  denotes the prediction loss function for all output variables;  $\lambda_{phy}$  is the weighting parameter for the derived output variable loss;  $\lambda_{phy}(e)$ ,  $\lambda_{phy}(0)$  represent the current and initial weights for the derived output variable loss, respectively;  $e$  denotes the current training epoch; and  $k$  is the decay rate.

##### (3) Physical mechanism enhancement of gated memory units

In the LSTM model with a structured output layer and dynamic weighting strategy coupled loss functions, the predicted free output variables are required not only to accurately fit observations but also to ensure that the derived output variables — obtained through physical relationships — precisely match the corresponding observations. This physics-guided gating adaptation mechanism indirectly steers the internal state update process of the LSTM model, enabling the network to achieve a dynamic balance between flexible data fitting and adherence to physical laws.

To be specific, under the guidance of physical derivation consistency, the input gate tends to admit new input information that aligns with the expected physical derivation of the system; the forget gate adaptively retains historical memory states that are crucial for subsequent physical derivation; and the output gate enhances the expressiveness of free output variable states, supporting the accurate generation of derived output variables. As a result, all output variables not only attain a high level of predictive accuracy but also naturally satisfy physical relationships embedded into the output layer.

### 2.4. Evaluation metrics

To rigorously evaluate the reliability and predictive capability of the scheduling rules extraction model, a comprehensive evaluation framework is developed. This framework assesses the model from multiple perspectives, including forecasting accuracy, physical consistency, and both stability and generalization performance.

#### 2.4.1. Evaluation metrics for accuracy

Prediction accuracy metrics are designed to assess the precision and reliability of the predicted samples, thereby reflecting the model's numerical forecasting capability. Three widely used standard statistical indicators are employed to evaluate prediction performance: root mean square error (RMSE), mean absolute error (MAE), and the coefficient of determination ( $R^2$ ). These indicators will be calculated based on the normalized values of all output variables to ensure consistency in units across different physical quantities. Consequently, all of the three metrics are dimensionless and directly comparable among different variables.

#### 2.4.2. Evaluation metrics for physical consistency

The evaluation of physical consistency aims to verify the performance of the model in capturing the underlying physical relationships embedded through constrained-based derivations in the structured output layer. These metrics assess the model's physical validity and practical applicability, including the cascade hydraulic connection error (FBE), water storage balance error (WBE), energy storage balance error (EBE), load balance error (LBE), and constraint violation rate (CVR) — both in the current stage and future stages for the remaining operation time periods.

##### (1) Cascade hydraulic connection error

$$FBE_i = \text{abs} \left( \widehat{Q}_{i,t}^h - \left( Qn_{i,t}^h + Qr_{i,t}^h \right) \right), i \ge 2 \quad (2.46)$$

$$RFBE_i = \text{abs} \left( \widehat{RQ}_{i,t}^h - \left( RQn_{i,t}^h + RQr_{i,t}^h \right) \right), i \ge 2 \quad (2.47)$$

where  $FBE$  denotes the hydraulic connection error in the current operation time period, and  $RFBE$  represents the hydraulic connection error for the remaining operation time periods.

##### (2) Water storage balance error

$$WBE_i = \begin{cases} \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs}(\hat{V}_{i,t+1}^h - V_{i,t}^h - (Q_{i,t}^h - \hat{Q}_{i,t}^h) \cdot \Delta t), & i = 1 \\ \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs}(\hat{V}_{i,t+1}^h - V_{i,t}^h - (Q_{i,t}^h + Q_{i,t}^h - \hat{Q}_{i,t}^h) \cdot \Delta t), & i \ge 2 \end{cases} \quad (2.48)$$

$$RWBE_i = \begin{cases} \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs} \left( \left( (Q_{i,t}^h - \hat{Q}_{i,t}^h) + (RQ_{i,t}^h - \hat{RQ}_{i,t}^h) \cdot (T-t) \right) \cdot \Delta t \right), & i=1 \\ \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs} \left( \left( \hat{V}_{i,T+1}^h - V_{i,t}^h - (Q_{i,t}^h + Q_{i,t}^h - \hat{Q}_{i,t}^h) \cdot \Delta t \right) \right. \\ \left. - (RQ_{i,t}^h + RQ_{i,t}^h - \hat{RQ}_{i,t}^h) \cdot (T-t) \cdot \Delta t \right), & i \ge 2 \end{cases} \quad (2.49)$$

where  $WBE$  denotes the water storage balance error in the current operation time period, and  $RWBE$  represents the water storage balance error for the remaining operation time periods.

##### (3) Energy storage balance error

$$EBE_m = \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs} \left( \hat{E}_{m,t+1}^{ps} - \left( E_{m,t}^{ps} + (\eta \cdot \hat{P}_{m,t}^{ps,in} - \hat{P}_{m,t}^{ps,out}) \cdot \Delta t \right) \right) \quad (2.50)$$

$$REBE_m = \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs} \left( \left( (\eta \cdot \hat{P}_{m,t}^{ps,in} - \hat{P}_{m,t}^{ps,out}) + (\eta \cdot \hat{RP}_{m,t}^{ps,in} - \hat{RP}_{m,t}^{ps,out}) \cdot (T-t) \right) \cdot \Delta t \right) \quad (2.51)$$

where  $EBE$  denotes the energy storage balance error in the current operation time period, and  $REBE$  represents the energy storage balance error for the remaining operation time periods.

##### (4) Load balance error

$$LBE = \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs} \left( L_t - \left( \sum_{i=1}^{I} \hat{P}_{i,t}^h + \sum_{j=1}^{J} \hat{P}_{j,t}^{s-grid} + \sum_{m=1}^{M} \hat{P}_{m,t}^{ps-out} + \hat{D}_t \right) \right) \quad (2.52)$$

$$RLBE = \frac{1}{n_t} \sum_{t=1}^{n_t} \text{abs} \left( RL_t - \left( \sum_{i=1}^{I} \hat{RP}_{i,t}^h + \sum_{j=1}^{J} \hat{RP}_{j,t}^{s-grid} + \sum_{m=1}^{M} \hat{RP}_{m,t}^{ps-out} + RD_t \right) \right) \quad (2.53)$$

where  $LBE$  denotes the load balance error in the current operation time period, and  $RLBE$  represents the load balance error for the remaining operation time periods.

##### (5) Constraint violation rate

$CVR$  reflects the effectiveness of physical constraints on the predicted samples, including physical balance constraints and physical boundary constraints. A higher ratio indicates lower constraint adherence. Eq. (2.54) shows the calculation formula:

$$CVR = 1 - \frac{\text{count}\{\hat{y}_t | \underline{y}_t \le \hat{y}_t \le \overline{y}_t\}}{n_t} \times 100\%, t = 1, 2, \dots, n_t \quad (2.54)$$

where  $\underline{y}_t, \overline{y}_t$  denote the lower and upper limits of the model's predicted variables, respectively; and  $\text{count}\{\cdot\}$  is a counting function.

#### 2.4.3. Evaluation metrics for model stability and generalization

Model stability serves as a critical indicator for assessing the extent of

performance variation under different datasets or training conditions. A model with high stability often exhibits strong generalization capability. In this study, a training-validation-testing data split is employed to evaluate model stability and generalization by comparing its performance across different datasets.

##### (1) Loss Gap

$$\text{LossGap} = \text{Loss}_{val} - \text{Loss}_{train} \quad (2.55)$$

where  $\text{Loss}_{val}, \text{Loss}_{train}$  represent the Loss function values on the validation samples and training samples, respectively;

##### (2) RMSE Gap

$$\text{RMSEGap} = \text{RMSE}_{val} - \text{RMSE}_{train} \quad (2.56)$$

where  $\text{RMSE}_{val}, \text{RMSE}_{train}$  represent the  $RMSE$  on the validation samples and training samples, respectively;

##### (3) The Adjusted $R^2$ score ( $AR^2$ )

The term  $AR^2$  is a commonly used indicator for evaluating the performance of regression models. It introduces a penalty for model complexity, making it more suitable for situations with a large number of input variables or complex model structures. This adjustment helps mitigate the risk of overfitting. Eq. (2.57) expresses it as:

$$AR^2 = 1 - \frac{(1 - R^2) \cdot (n_t - 1)}{n_t - N - 1} \quad (2.57)$$

where  $R^2$  denotes the coefficient of determination of the model;  $n_t$  denotes the number of samples; and  $N$  denotes the number of all predicted variables in the model.

## 3. Case study

### 3.1. Overview of the study area

The clean energy base (CEB) is rich in renewable energies, especially in hydropower and solar power, providing favorable conditions for the development of multi-energy complementary system. Figs. 7 and 8 show an overview of CEB.

The energy base has a total installed capacity of 26,130 MW, consisting of three cascade hydropower stations with an installed capacity of 4,820 MW, four solar power stations with an installed capacity of 18,310 MW, and a pumped-storage power station with an installed capacity of 3,000 MW. Detailed information on each power station is provided in Tables 2 and 3. All power output is collected at an operation center (OC) and then transmitted to the power grid through a  $\pm 800$  kV ultra-high-voltage direct current (UHVDC) transmission route, with a rated transmission capacity of 8,000 MW.

### 3.2. Experimental design

Taking the aforementioned CEB as the study area, a PC-LSTM model based on orthogonal experimental design is constructed. The proposed model is compared with two other benchmark LSTM-based models. The three models are as follows:

#### (1) Benchmark model 1 (LSTM)

A standard multi-input multi-output LSTM model is constructed, as shown in Fig. 9, incorporating two-stage input and output variables, but without embedding any physical mechanisms.


![Fig. 7. Overview of the clean energy base. The diagram shows three main energy sources: Solar power stations (S1, S2, S3, S4), Pumped-storage power stations (PS), and Cascade hydropower stations (H1, H2, H3). Solar power stations feed into the Operation Center. Pumped-storage power stations feed into the Operation Center. Cascade hydropower stations show inflow (H1, H2) and release (H3) feeding into the Operation Center. The Operation Center then feeds into the Power grid, represented by two electrical towers.](e9314c83043183351ed74908e9bf2f90_img.jpg)

Fig. 7. Overview of the clean energy base. The diagram shows three main energy sources: Solar power stations (S1, S2, S3, S4), Pumped-storage power stations (PS), and Cascade hydropower stations (H1, H2, H3). Solar power stations feed into the Operation Center. Pumped-storage power stations feed into the Operation Center. Cascade hydropower stations show inflow (H1, H2) and release (H3) feeding into the Operation Center. The Operation Center then feeds into the Power grid, represented by two electrical towers.

Fig. 7. Overview of the clean energy base.

![Fig. 8. Topology of the clean energy base. This detailed diagram shows the flow of energy from various sources to the Operation Center (OC). Solar power stations (S1, S2, S4) provide inflow (Qn1,t^h, Qn2,t^h, Qn4,t^h) to the OC. Pumped-storage power stations (PS) provide inflow (Qn2,t^h, Qn3,t^h) to the OC. Cascade hydropower stations (H1, H2, H3) provide inflow (Qn1,t^h, Qn2,t^h, Qn3,t^h) to the OC. The OC then feeds into the Power grid (Pgrid_t). The diagram includes a legend: triangles for Hydropower station, trapezoids for Pumped-storage power station, circles for Solar power station, a yellow box for Operation center, solid arrows for Electricity transmission routes, blue arrows for Natural/Internal inflow, and grey arrows for Inflow/Release of hydropower stations.](d26959f4514c26ca19c3d6f00da85956_img.jpg)

Fig. 8. Topology of the clean energy base. This detailed diagram shows the flow of energy from various sources to the Operation Center (OC). Solar power stations (S1, S2, S4) provide inflow (Qn1,t^h, Qn2,t^h, Qn4,t^h) to the OC. Pumped-storage power stations (PS) provide inflow (Qn2,t^h, Qn3,t^h) to the OC. Cascade hydropower stations (H1, H2, H3) provide inflow (Qn1,t^h, Qn2,t^h, Qn3,t^h) to the OC. The OC then feeds into the Power grid (Pgrid\_t). The diagram includes a legend: triangles for Hydropower station, trapezoids for Pumped-storage power station, circles for Solar power station, a yellow box for Operation center, solid arrows for Electricity transmission routes, blue arrows for Natural/Internal inflow, and grey arrows for Inflow/Release of hydropower stations.

Fig. 8. Topology of the clean energy base.

$$\begin{aligned}
 X = & (t, V_{1,t}^h, Qn_{1,t}^h, Qi_{1,t}^h, Qn_{2,t}^h, Qn_{3,t}^h, RQn_{1,t}^h, RQi_{1,t}^h, RQn_{2,t}^h, RQi_{2,t}^h, RQn_{3,t}^h, RQi_{3,t}^h, \\
 & P_{j,t}^{s,in}, RP_{j,t}^{s,in}, E_{m,t}^{ps,out}, E_{m,T+1}^{ps,out}, RE_{m,t}^{ps,out}, RP_{m,t}^{s,in}, L_t, RL_t) \\
 Y = & (\hat{V}_{1,t+1}^h, \hat{V}_{1,T+1}^h, \hat{Q}_{2,t}^h, \hat{Q}_{3,t}^h, \hat{Q}_{e_{1,t}}^h, \hat{Q}_{o_{1,t}}^h, \hat{RQ}_{2,t}^h, \hat{RQ}_{3,t}^h, \hat{RQ}_{e_{1,t}}^h, \hat{RQ}_{o_{1,t}}^h, \hat{P}_{1,t}^h, \hat{P}_{2,t}^h, \hat{P}_{3,t}^h, \\
 & \hat{P}_{j,t}^{s,out}, \hat{RP}_{j,t}^{s,out}, \hat{E}_{m,t+1}^{ps}, \hat{P}_{m,t}^{ps,out}, \hat{RP}_{m,t}^{ps,out}, \hat{P}_{m,t}^{s,in}, \hat{RP}_{m,t}^{s,in}, \hat{D}_t, \hat{RD}_t) \\
 Y = & f_{LSTM}(X)
 \end{aligned} \tag{3.1}$$

$$\begin{aligned}
 X = & (t, V_{1,t}^h, Qn_{1,t}^h, Qi_{1,t}^h, Qn_{2,t}^h, Qn_{3,t}^h, RQn_{1,t}^h, RQi_{1,t}^h, RQn_{2,t}^h, RQi_{2,t}^h, RQn_{3,t}^h, RQi_{3,t}^h, \\
 & P_{j,t}^{s,in}, RP_{j,t}^{s,in}, E_{m,t}^{ps,out}, E_{m,T+1}^{ps,out}, RE_{m,t}^{ps,out}, RP_{m,t}^{s,in}, L_t, RL_t) \\
 Y^{free} = & (\hat{Q}_{e_{1,t}}^h, \hat{Q}_{o_{1,t}}^h, \hat{RQ}_{e_{1,t}}^h, \hat{RQ}_{o_{1,t}}^h, \hat{P}_{j,t}^{s,out}, \hat{RP}_{j,t}^{s,out}, \\
 & \hat{P}_{m,t}^{ps,out}, \hat{RP}_{m,t}^{ps,out}, \hat{P}_{m,t}^{s,in}, \hat{RP}_{m,t}^{s,in}) \\
 Y^{free} = & f_{PA-LSTM}(X)
 \end{aligned} \tag{3.2}$$

where  $f_{LSTM}$  denotes scheduling rules of the power system extracted through LSTM.

### (2) Benchmark model 2 (Physics-Adjusted LSTM, PA-LSTM)

The PA-LSTM model is constructed based on free output variables, incorporating two-stage input and output variables, as shown in Fig. 10. The derived output variables are calculated through physical equations based on the model's predicted variables, rather than being obtained directly through the model's output.

where  $f_{PA-LSTM}$  denotes scheduling rules of the power system extracted through PA-LSTM.

$$\begin{aligned}
 Y^{derived} = & (\hat{V}_{1,t+1}^h, \hat{V}_{1,T+1}^h, \hat{Q}_{2,t}^h, \hat{Q}_{3,t}^h, \hat{RQ}_{2,t}^h, \hat{RQ}_{3,t}^h, \\
 & \hat{P}_{1,t}^h, \hat{P}_{2,t}^h, \hat{P}_{3,t}^h, \hat{E}_{m,t+1}^{ps}, \hat{D}_t, \hat{RD}_t) \\
 Y^{derived} = & F_{physics}(X, Y^{free})
 \end{aligned} \tag{3.3}$$

$$Y = (Y^{free}, Y^{derived}) \tag{3.4}$$

#### (3) Proposed model (Physics-Constrained LSTM, PC-LSTM)

A decoupling mechanism between free and derived output variables is introduced into the structured output layer to consider physical

**Table 2**  
Basic information of hydropower stations.

| Parameters                        | Unit                            | Hydropower station |                |                |
|-----------------------------------|---------------------------------|--------------------|----------------|----------------|
|                                   |                                 | H <sub>1</sub>     | H <sub>2</sub> | H <sub>3</sub> |
| Control of watershed area         | 10 <sup>4</sup> km <sup>2</sup> | 7.49               | 7.94           | 8.1            |
| Regulation performance            | /                               | Quarterly          | Annually       | Daily          |
| Normal water level                | m                               | 3054               | 2895           | 2605           |
| Flood control water level         | m                               | 3040               | /              | /              |
| Dead water level                  | m                               | 3014               | 2815           | 2600           |
| Normal water storage              | 10 <sup>9</sup> m <sup>3</sup>  | 8.44               | 37.55          | 0.9            |
| Dead water storage                | 10 <sup>9</sup> m <sup>3</sup>  | 3.7                | 13.21          | 0.75           |
| Installed capacity                | 10 <sup>4</sup> kW              | 150                | 260            | 72             |
| Firm power output                 | 10 <sup>4</sup> kW              | 18.75              | 29.25          | 9              |
| Hydropower generation coefficient | /                               | 8.5                | 8.5            | 8.5            |
| Head loss                         | m                               | 1                  | 1              | 2              |
| Ecological flow                   | m <sup>3</sup> /s               | 95.7               | 98.7 ~ 162     | 66.9           |

**Table 3**  
Basic information of solar and PS power stations.

| Parameters         | Unit               | PS power station | Solar power station |                |                |                |
|--------------------|--------------------|------------------|---------------------|----------------|----------------|----------------|
|                    |                    |                  | PS                  | S <sub>1</sub> | S <sub>2</sub> | S <sub>3</sub> |
| Installed capacity | 10 <sup>4</sup> kW | 300              | 382                 | 155            | 840            | 454            |

mechanisms based on the standard LSTM, as shown in Fig. 11. By incorporating the free and derived output variables into the loss function, the gating mechanisms of the LSTM are guided to adaptively learn hidden state evolution paths that comply with physical constraints, while simultaneously ensuring prediction accuracy.

$$\begin{aligned}
 X = & \left( t, V_{i,t}^h, Qn_{i,t}^h, Ql_{i,t}^h, Qr_{i,t}^h, Qn_{i,t}^h, RQl_{i,t}^h, RQr_{i,t}^h, RQr_{i,t}^h, RQr_{i,t}^h, \right. \\
 & \left. P_{j,t}^{ps-in}, RP_{j,t}^{ps-in}, E_{m,t}^{ps-out}, E_{m,t}^{ps-in}, E_{m,T+1}^{ps}, RE_{m,t}^{ps-out}, RE_{m,t}^{ps-in}, L_t, RL_t \right) \\
 y^{free} = & \left( \widehat{Qe}_{i,t}^h, \widehat{Qo}_{i,t}^h, \widehat{RQe}_{i,t}^h, \widehat{RQo}_{i,t}^h, \widehat{P}_{i,t}^{s-out}, \widehat{RP}_{j,t}^{s-out}, \right. \\
 & \left. \widehat{P}_{m,t}^{ps-out}, \widehat{RP}_{m,t}^{ps-out}, \widehat{P}_{m,t}^{ps-in}, \widehat{RP}_{m,t}^{ps-in} \right) \\
 y^{derived} = & \left( \widehat{V}_{i,T+1}^h, \widehat{V}_{i,T+1}^h, \widehat{Q}_{i,T+1}^h, \widehat{Q}_{i,T+1}^h, \widehat{RQ}_{i,T+1}^h, \widehat{RQ}_{i,T+1}^h, \right. \\
 & \left. \widehat{P}_{i,t}^{s-out}, \widehat{RP}_{i,t}^{s-out}, \widehat{E}_{m,T+1}^{ps}, \widehat{D}_t, \widehat{RD}_t \right) \\
 & (y^{free}, y^{derived}) = f_{PC-LSTM}(X)
 \end{aligned} \quad (3.5)$$

where  $f_{PC-LSTM}$  denotes scheduling rules of the power system extracted through PC-LSTM.

Data of daily inflow (inflow is assumed to remain constant throughout the day), hourly solar power input, hourly grid demand load, initial and boundary conditions, and all relevant engineering data within the study area were collected. Based on the representative scheduling scenario space construction method proposed in Section 2.1, a total of 14,400 experimental operation scenarios were assembled.

These operation scenarios then were used as inputs to the deterministic optimization model proposed in Section 2.2 to obtain baseline scheduling schemes. Since the pumped-storage power stations are restricted from operating in both pumping and generating modes simultaneously, Eq. (2.24) is represented in LINGO as a bilinear constraint, the model was solved through LINGO's Global Solver, which applies branch-and-bound and interval bounding techniques to handle bilinear terms. The approach is mathematically straightforward and ensures mutual exclusivity with negligible computational overhead. In practice, the model can calculate baseline scheduling schemes for 500 operation scenarios less than 900 s at a time.

Those inputs then were used as training, validation, and testing samples for the three LSTM-based models. To evaluate the accuracy and stability of the models, 9,600 samples were used for training, 2,400 for validation, and 2,400 for testing. Table 4 summarizes the architecture and parameters of the three LSTM-based models. All experiments were conducted on a workstation equipped with an Intel® Core™ Ultra 5 125H processor (14 cores, 18 threads, base frequency 1.2 GHz) and 16 GB RAM. All LSTM-based models were implemented in Python 3.12 with TensorFlow 2.10.

# 4. Results and discussion

## 4.1. Deterministic optimization scheduling rules for the hydro-solar-storage complementary power systems

### 4.1.1. Efficiency analysis based on orthogonal experimental design

Based on the methodology in Section 2.1, the main factors — including uncertainty-related input factors and initial water storage of hydropower stations and their corresponding multi-level states — should be considered. Specifically, inflow and input solar power are selected from the same time periods to form hydro-solar combined input factors. The dominant input factors and their level states are illustrated in Tables 5 and 6. Level states include the potential input conditions of corresponding factors. For example, the initial water storage  $H_1$  will be selected from the range between flood control water storage to normal water storage, with four different initial water storage levels. And the initial water storage of  $H_2$ ,  $H_3$  will be selected from the range between dead water storage to normal water storage, with five or three different initial water storage levels. For factors like inflow and input solar power, a set of 20 hydro-solar combined input conditions was designed to capture the full range of joint operation conditions observed in historical data. These scenarios were selected based on the frequency analysis of multi-year observations of inflow and input solar power, ensuring that both typical and extreme events are adequately represented.

As can be seen from Tables 5 and 6, conducting a full factorial experiment would require 115,200 experimental runs, which would require substantial computational requirements and the results obtained would not be practical for real-time scheduling. Therefore, the OED proposed in Section 2.1 is applied to reduce the scenario space.

![Schematic diagram of input and output variables for LSTM. The input variables X are shown in a blue box, and the output variables Y are shown in a red box. An arrow labeled 'LSTM' points from X to Y.](bdfe4e1058d1a0e14bb838771b57254c_img.jpg)

The diagram illustrates the input and output variables for an LSTM model. The input variables  $X$  are grouped into three stages: Day index ( $t$ ), Current stage (containing  $V_{i,t}^h, Qn_{i,t}^h, Ql_{i,t}^h, Qr_{i,t}^h, Qn_{i,t}^h, P_{j,t}^{ps-in}, E_{m,t}^{ps-out}, E_{m,t}^{ps-in}, E_{m,T+1}^{ps}, RE_{m,t}^{ps-out}, RE_{m,t}^{ps-in}, L_t$ ), and Future stage (containing  $RQn_{i,t}^h, RQl_{i,t}^h, RQr_{i,t}^h, RQr_{i,t}^h, RQr_{i,t}^h, RP_{j,t}^{ps-in}, RE_{m,t}^{ps-out}, RE_{m,t}^{ps-in}, RL_t$ ). These inputs are fed into an LSTM block, which then produces the output variables  $Y$ . The output variables  $Y$  are also grouped into three stages: Current stage (containing  $V_{i,T+1}^h, V_{i,T+1}^h, Q_{i,T+1}^h, Q_{i,T+1}^h, Q_{i,T+1}^h, Q_{i,T+1}^h, P_{i,t}^{s-out}, E_{m,T+1}^{ps}, P_{m,t}^{s-out}, P_{m,t}^{s-in}, D_t$ ), and Future stage (containing  $RQ_{i,T+1}^h, RQ_{i,T+1}^h, RQ_{i,T+1}^h, RQ_{i,T+1}^h, RQ_{i,T+1}^h, RP_{i,t}^{s-out}, RP_{m,t}^{s-out}, RP_{m,t}^{s-in}, RD_t$ ).

Schematic diagram of input and output variables for LSTM. The input variables X are shown in a blue box, and the output variables Y are shown in a red box. An arrow labeled 'LSTM' points from X to Y.

**Fig. 9.** Schematic diagram of input and output variables for LSTM.

![Schematic diagram of input and output variables for PA-LSTM. The diagram shows a flow from input variables X to a PA-LSTM block, which then outputs free output variables Y^free and derived output variables Y^derived. The input variables X include Day index t, Current stage (V_{i,t}^h, Q_{i,t}^h, Q_{i,t}^{ps,out}, Q_{i,t}^{ps,in}, E_{m,t}^{ps,out}, E_{m,t}^{ps,in}, L_t), and Future stage (RQ_{i,t}^h, RQ_{i,t}^{ps,out}, RQ_{i,t}^{ps,in}, RP_{i,t}^{ps,out}, RP_{i,t}^{ps,in}, RL_t). The PA-LSTM block outputs Y^free, which is then processed by Physical equations to produce Y^derived. The final output is Y = (Y^free, Y^derived).](eefe19c5e14dc4d6c316b7f7fbb7d7d7_img.jpg)

Schematic diagram of input and output variables for PA-LSTM. The diagram shows a flow from input variables X to a PA-LSTM block, which then outputs free output variables Y^free and derived output variables Y^derived. The input variables X include Day index t, Current stage (V\_{i,t}^h, Q\_{i,t}^h, Q\_{i,t}^{ps,out}, Q\_{i,t}^{ps,in}, E\_{m,t}^{ps,out}, E\_{m,t}^{ps,in}, L\_t), and Future stage (RQ\_{i,t}^h, RQ\_{i,t}^{ps,out}, RQ\_{i,t}^{ps,in}, RP\_{i,t}^{ps,out}, RP\_{i,t}^{ps,in}, RL\_t). The PA-LSTM block outputs Y^free, which is then processed by Physical equations to produce Y^derived. The final output is Y = (Y^free, Y^derived).

Fig. 10. Schematic diagram of input and output variables for PA-LSTM.

![Schematic diagram of input and output variables for PC-LSTM. The diagram shows a flow from input variables X to a PC-LSTM block, which then outputs free output variables Y^free and derived output variables Y^derived. The input variables X include Day index t, Current stage (V_{i,t}^h, Q_{i,t}^h, Q_{i,t}^{ps,out}, Q_{i,t}^{ps,in}, E_{m,t}^{ps,out}, E_{m,t}^{ps,in}, L_t), and Future stage (RQ_{i,t}^h, RQ_{i,t}^{ps,out}, RQ_{i,t}^{ps,in}, RP_{i,t}^{ps,out}, RP_{i,t}^{ps,in}, RL_t). The PC-LSTM block outputs Y^free, which is then processed by a Physics-constrained output layer to produce Y^derived. The final output is Y = (Y^free, Y^derived).](cab0834804fb031b43865554cc8d06ab_img.jpg)

Schematic diagram of input and output variables for PC-LSTM. The diagram shows a flow from input variables X to a PC-LSTM block, which then outputs free output variables Y^free and derived output variables Y^derived. The input variables X include Day index t, Current stage (V\_{i,t}^h, Q\_{i,t}^h, Q\_{i,t}^{ps,out}, Q\_{i,t}^{ps,in}, E\_{m,t}^{ps,out}, E\_{m,t}^{ps,in}, L\_t), and Future stage (RQ\_{i,t}^h, RQ\_{i,t}^{ps,out}, RQ\_{i,t}^{ps,in}, RP\_{i,t}^{ps,out}, RP\_{i,t}^{ps,in}, RL\_t). The PC-LSTM block outputs Y^free, which is then processed by a Physics-constrained output layer to produce Y^derived. The final output is Y = (Y^free, Y^derived).

Fig. 11. Schematic diagram of input and output variables for PC-LSTM.

Among these factors, *Factor*<sub>5</sub> and *Factor*<sub>6</sub> have significantly more numbers of level states than the other factors, making them unsuitable for inclusion in the OED according to the design of orthogonal arrays. Instead, they will be combined directly with the scenario space obtained by the orthogonal experimental design of the other four factors.

A small subset of 25 scenarios characterized by uniform distribution is selected from the full factorial scenario space (formed by *Factor*<sub>1</sub> ~ *Factor*<sub>4</sub>) through OED. The 25 scenario schemes are shown in Table 7, where  $G_{ij}$  denotes the  $i$ -th input factor and  $j$ -th level state,  $E(\bullet)$  denotes the combination schemes of each factor and its corresponding level state. The subset is combined directly with *Factor*<sub>5</sub> and *Factor*<sub>6</sub>, reducing

the number of experimental schemes from 115,200 to 14,400, thereby improving model computational efficiency up to 87.5 %.

### 4.1.2. Baseline scheduling schemes

The training effectiveness of the LSTM-based models relies on high-quality input samples. In this study, a high-dimensional, nonlinear

Table 5

Level state of input factors.

| Input factors                          | Level state                  |
|----------------------------------------|------------------------------|
| Initial water storage of $H_1$ (m)     | $V_{1,fc}^h \sim V_{1,n}^h$  |
| Initial water storage of $H_2$ (m)     | $V_{2,d}^h \sim V_{2,n}^h$   |
| Initial water storage of $H_3$ (m)     | $V_{3,d}^h \sim V_{3,n}^h$   |
| Inflow (m <sup>3</sup> /s)             | Typical designed inflow      |
| Input solar power (10 <sup>4</sup> kW) | Typical designed solar power |
| Grid load demand (10 <sup>4</sup> kW)  | Typical load demand          |
| Operation time period (h)              | Hour                         |

Table 6

Number of level states of input factors.

| Input factors                                                      | Number of levels |
|--------------------------------------------------------------------|------------------|
| <i>Factor</i> <sub>1</sub> : Initial water storage of $H_1$ (m)    | 4                |
| <i>Factor</i> <sub>2</sub> : Initial water storage of $H_2$ (m)    | 5                |
| <i>Factor</i> <sub>3</sub> : Initial water storage of $H_3$ (m)    | 3                |
| <i>Factor</i> <sub>4</sub> : Grid load demand (10 <sup>4</sup> kW) | 4                |
| <i>Factor</i> <sub>5</sub> : hydro-solar combined input            | 20               |
| <i>Factor</i> <sub>6</sub> : Operation time period (h)             | 24               |

Table 4

Architecture and parameters of three LSTM models.

| Architecture and parameters          | LSTM                                                | PA-LSTM         | PC-LSTM         |
|--------------------------------------|-----------------------------------------------------|-----------------|-----------------|
| Number of Hidden layers              | 3                                                   | 3               | 3               |
| Number of Units in each hidden layer | First layer 64<br>Second layer 32<br>Third layer 16 | 64<br>32<br>16  | 64<br>32<br>16  |
| Activation function                  | Hidden layer: relu<br>Output layer: sigmoid         | relu<br>sigmoid | relu<br>sigmoid |
| Loss function                        | MAE                                                 | MAE             | MAE             |
| Optimizer                            | Adam                                                | Adam            | Adam            |
| Epochs                               | 1000                                                | 1000            | 1000            |
| Batch size                           | 96                                                  | 96              | 96              |
| Learning rate                        | 0.001                                               | 0.001           | 0.001           |
| Training time (s)                    | 835                                                 | 760             | 810             |
| Prediction time (s)                  | 4.19                                                | 2.85            | 3.77            |

**Table 7**  
Orthogonal experimental design schemes.

| Schemes | Scenario space                          |
|---------|-----------------------------------------|
| 1       | $E(C_{1,1}, C_{2,1}, C_{3,1}, C_{4,1})$ |
| 2       | $E(C_{1,1}, C_{2,2}, C_{3,3}, C_{4,4})$ |
| 3       | $E(C_{1,1}, C_{2,3}, C_{3,1}, C_{4,2})$ |
| 4       | $E(C_{1,1}, C_{2,4}, C_{3,2}, C_{4,1})$ |
| 5       | $E(C_{1,1}, C_{2,5}, C_{3,2}, C_{4,3})$ |
| 6       | $E(C_{1,2}, C_{2,1}, C_{3,3}, C_{4,4})$ |
| 7       | $E(C_{1,2}, C_{2,2}, C_{3,2}, C_{4,2})$ |
| 8       | $E(C_{1,2}, C_{2,3}, C_{3,1}, C_{4,2})$ |
| 9       | $E(C_{1,2}, C_{2,4}, C_{3,1}, C_{4,3})$ |
| 10      | $E(C_{1,2}, C_{2,5}, C_{3,3}, C_{4,1})$ |
| 11      | $E(C_{1,3}, C_{2,1}, C_{3,2}, C_{4,2})$ |
| 12      | $E(C_{1,3}, C_{2,2}, C_{3,1}, C_{4,3})$ |
| 13      | $E(C_{1,3}, C_{2,3}, C_{3,3}, C_{4,3})$ |
| 14      | $E(C_{1,3}, C_{2,4}, C_{3,3}, C_{4,1})$ |
| 15      | $E(C_{1,3}, C_{2,5}, C_{3,2}, C_{4,4})$ |
| 16      | $E(C_{1,4}, C_{2,1}, C_{3,3}, C_{4,4})$ |
| 17      | $E(C_{1,4}, C_{2,2}, C_{3,1}, C_{4,3})$ |
| 18      | $E(C_{1,4}, C_{2,3}, C_{3,2}, C_{4,1})$ |
| 19      | $E(C_{1,4}, C_{2,4}, C_{3,2}, C_{4,4})$ |
| 20      | $E(C_{1,4}, C_{2,5}, C_{3,1}, C_{4,2})$ |
| 21      | $E(C_{1,5}, C_{2,1}, C_{3,2}, C_{4,3})$ |
| 22      | $E(C_{1,5}, C_{2,2}, C_{3,3}, C_{4,1})$ |
| 23      | $E(C_{1,5}, C_{2,3}, C_{3,1}, C_{4,4})$ |
| 24      | $E(C_{1,5}, C_{2,4}, C_{3,3}, C_{4,2})$ |
| 25      | $E(C_{1,5}, C_{2,5}, C_{3,2}, C_{4,3})$ |

representative operation scenario space that accounts for uncertainties in inflow, input solar power, grid load demand, and dynamic operational interactions among power stations was constructed based on OED. The selected scenario space not only covers typical operating conditions, but also incorporates extreme combinations—such as high inflow, high input solar power, and low system load to ensure broad representativeness and improve the model's generalization capability. These

operation scenarios were applied to the deterministic operation model proposed in Section 2.2 to obtain baseline scheduling schemes, which then were used for the LSTM-based models training. The following figures present some baseline optimal scheduling rules under different representative operation scenarios.

#### (1) Low grid demand load

Figs. 12–14 present the baseline operation schemes corresponding to low, moderate, and high inflow scenarios with corresponding input solar power under low grid load demand, respectively, highlighting the impact of inflow variations on system scheduling rules. Fig. 15 illustrates the water storage variations of hydropower stations  $H_1$  and  $H_2$  under three different inflow conditions.

First, it can be observed that solar power dominates during daytime hours due to the large installed capacity of solar power stations in the study area. With higher solar power during daytime, the pumped-storage power station can store more energy. At night, hydropower becomes the primary source for meeting the grid load demand, supplemented by the PS power station for additional flexibility and regulation in the absence of solar input.

Second, the grid load demands are effectively met under all three inflow scenarios. However, the share of hydropower varies significantly. In the low inflow scenario, the daily hydropower generation reaches  $2,726 \times 10^4$  kWh, which is considerably lower than the  $3,548 \times 10^4$  kWh and  $3,466 \times 10^4$  kWh observed in the moderate and high inflow scenarios, respectively, indicating that inflow variation is a key limiting factor for hydropower production.

#### (2) High grid demand load

Figs. 16 and 17 present the baseline operation schemes under high grid load demand for two different inflow scenarios. The results indicate

![Figure 12: Operation schemes under low inflow scenario. (a) Power (10^4 kW) vs Hour (h) showing p^h, p^s_out, p^ps_out, p^ps_in, and load L. (b) Flow rate (m^3/s) vs Hour (h) showing inflow Q_i, outflow Q_o, and hydropower generation H_1, H_2, H_3. (c) Input solar power (10^4 kW) vs Hour (h) showing four scenarios S_1, S_2, S_3, S_4.](8e4f8c87efc168cac52580ce81583063_img.jpg)

Figure 12: Operation schemes under low inflow scenario. (a) Power (10^4 kW) vs Hour (h) showing p^h, p^s\_out, p^ps\_out, p^ps\_in, and load L. (b) Flow rate (m^3/s) vs Hour (h) showing inflow Q\_i, outflow Q\_o, and hydropower generation H\_1, H\_2, H\_3. (c) Input solar power (10^4 kW) vs Hour (h) showing four scenarios S\_1, S\_2, S\_3, S\_4.

Fig. 12. Operation schemes under low inflow scenario.

![Figure 13: Operation schemes under moderate inflow scenario. (a) Power (10^4 kW) vs Hour (h) showing p^h, p^s_out, p^ps_out, p^ps_in, and load L. (b) Flow rate (m^3/s) vs Hour (h) showing inflow Q_i, outflow Q_o, and hydropower generation H_1, H_2, H_3. (c) Input solar power (10^4 kW) vs Hour (h) showing four scenarios S_1, S_2, S_3, S_4.](df6238566a9642e7a4f25074c508f8a4_img.jpg)

Figure 13: Operation schemes under moderate inflow scenario. (a) Power (10^4 kW) vs Hour (h) showing p^h, p^s\_out, p^ps\_out, p^ps\_in, and load L. (b) Flow rate (m^3/s) vs Hour (h) showing inflow Q\_i, outflow Q\_o, and hydropower generation H\_1, H\_2, H\_3. (c) Input solar power (10^4 kW) vs Hour (h) showing four scenarios S\_1, S\_2, S\_3, S\_4.

Fig. 13. Operation schemes under moderate inflow scenario.

![Figure 14: Operation schemes under high inflow scenario. (a) Power output schemes: A stacked bar chart showing power components (p^h, p^s_out, p^ps_out, p^ps_in) and load L over 24 hours. (b) Inflow Q_i and water release Q_o of three hydropower stations (H1, H2, H3): A line chart showing flow rate (m^3/s) over 24 hours. (c) Input solar power condition of four solar power stations (S1, S2, S3, S4): A line chart showing input solar power (10^4 kW) over 24 hours.](177e8bc1c595b7fe3461d9919f87e044_img.jpg)

Figure 14: Operation schemes under high inflow scenario. (a) Power output schemes: A stacked bar chart showing power components (p^h, p^s\_out, p^ps\_out, p^ps\_in) and load L over 24 hours. (b) Inflow Q\_i and water release Q\_o of three hydropower stations (H1, H2, H3): A line chart showing flow rate (m^3/s) over 24 hours. (c) Input solar power condition of four solar power stations (S1, S2, S3, S4): A line chart showing input solar power (10^4 kW) over 24 hours.

Fig. 14. Operation schemes under high inflow scenario.

(a) Power output schemes; (b) Inflow  $Q_i$  and water release  $Q_o$  of three hydropower stations; (c) Input solar power condition of four solar power stations.

that when solar power drops to zero while load demand remains high, power shortages occur regardless of the inflow condition. Magnitudes of the residual load are  $533 \times 10^4$  kWh and  $612 \times 10^4$  kWh for the low inflow and high inflow scenarios, respectively. This is primarily due to the installed capacity of hydropower stations and pumped-storage power stations, which are insufficient to meet the grid load demand even when they are at installed power output in the absence of solar power.

As shown in Fig. 18, the water storages of  $H_1$  and  $H_2$  exhibit significant intraday fluctuations to meet the high grid load demand, reflecting their high degree of regulation under the low inflow scenario. In contrast, the hydropower stations can meet the high grid load demand

while still retaining part of the inflow under the high inflow condition.

## 4.2. Comprehensive evaluation for LSTM-based models

### 4.2.1. Evaluation results for accuracy

The prediction accuracy of the three LSTM-based model is evaluated through the  $RMSE$ ,  $MAE$ , and  $R^2$ . Table 8 compares the prediction accuracy of the three LSTM-based models across training, validation, and testing samples. The results indicate that the PC-LSTM model shows the best performance among all indicators.

Specifically, the  $RMSE$  of PC-LSTM on the testing samples is 44.136, which is much lower than that of the standard LSTM (71.241) and PA-LSTM (52.463), demonstrating superior error control. In terms of the  $MAE$ , PC-LSTM records a value of 21.355 for testing samples, markedly outperforming LSTM (40.841) and PA-LSTM (26.285), indicating stronger robustness and prediction stability. Furthermore, the  $R^2$  for PC-LSTM reaches 0.939 on the testing samples, surpassing the LSTM (0.843) and PA-LSTM (0.721), which reflects better model fitting and generalization ability.

These findings collectively confirm that the PC-LSTM outperforms the other two models in accuracy and stability, validating the effectiveness of its physics-constrained structured design in enhancing predictive performance.

Fig. 19 compares the  $R^2$  for 43 output variables predicted by the LSTM, PA-LSTM, and PC-LSTM models, and Figs. 20–22 illustrate the scatter plots of several free output variables, comparing predicted and observed values. Points that lie closer to the diagonal indicate better agreement between predictions and observations, thus reflecting higher model accuracy.

It is evident that both the PA-LSTM and PC-LSTM models substantially outperform the standard LSTM models across most derived output variables. The standard LSTM exhibits relatively poor  $R^2$  performance in

![Figure 15: Water storage variations of two main hydropower stations under three inflow scenarios. A dual-axis line chart showing H1 and H2 water storage (10^3 m^3) over 24 hours for Low, Moderate, and High inflow scenarios.](88362167d90777ecb0aeb145832e78c2_img.jpg)

Figure 15: Water storage variations of two main hydropower stations under three inflow scenarios. A dual-axis line chart showing H1 and H2 water storage (10^3 m^3) over 24 hours for Low, Moderate, and High inflow scenarios.

Fig. 15. Water storage variations of two main hydropower stations under three inflow scenarios.

![Figure 16: Operation schemes under low inflow scenario. (a) Power output schemes: A stacked bar chart showing power components (p^h, p^s_out, p^ps_out, p^ps_in) and load L over 24 hours. (b) Inflow Q_i and water release Q_o of three hydropower stations (H1, H2, H3): A line chart showing flow rate (m^3/s) over 24 hours. (c) Input solar power condition of four solar power stations (S1, S2, S3, S4): A line chart showing input solar power (10^4 kW) over 24 hours.](d29d72755dd131d215d854aaf90fea3e_img.jpg)

Figure 16: Operation schemes under low inflow scenario. (a) Power output schemes: A stacked bar chart showing power components (p^h, p^s\_out, p^ps\_out, p^ps\_in) and load L over 24 hours. (b) Inflow Q\_i and water release Q\_o of three hydropower stations (H1, H2, H3): A line chart showing flow rate (m^3/s) over 24 hours. (c) Input solar power condition of four solar power stations (S1, S2, S3, S4): A line chart showing input solar power (10^4 kW) over 24 hours.

Fig. 16. Operation schemes under low inflow scenario.

![Figure 17: Operation schemes under high inflow scenario. (a) Power output schemes: A stacked bar chart showing power output in 10^4 kW over 24 hours. The legend includes p^h (blue), p^s_out (orange), p^s_out (green), p^s_in (purple), and L (grey). (b) Inflow Q_i and water release Q_o of three hydropower stations: A line chart showing flow rate in m^3/s over 24 hours. The legend includes Q_i (dashed), Q_o (solid), and three stations: H_1 (red), H_2 (blue), and H_3 (green). (c) Input solar power condition of four solar power stations: A line chart showing input solar power in 10^4 kW over 24 hours. The legend includes S_1 (orange), S_2 (yellow), S_3 (green), and S_4 (red).](b3df5964338063224492c01f09e4fed6_img.jpg)

Figure 17: Operation schemes under high inflow scenario. (a) Power output schemes: A stacked bar chart showing power output in 10^4 kW over 24 hours. The legend includes p^h (blue), p^s\_out (orange), p^s\_out (green), p^s\_in (purple), and L (grey). (b) Inflow Q\_i and water release Q\_o of three hydropower stations: A line chart showing flow rate in m^3/s over 24 hours. The legend includes Q\_i (dashed), Q\_o (solid), and three stations: H\_1 (red), H\_2 (blue), and H\_3 (green). (c) Input solar power condition of four solar power stations: A line chart showing input solar power in 10^4 kW over 24 hours. The legend includes S\_1 (orange), S\_2 (yellow), S\_3 (green), and S\_4 (red).

Fig. 17. Operation schemes under high inflow scenario.

(a) Power output schemes; (b) Inflow  $Q_i$  and water release  $Q_o$  of three hydropower stations; (c) Input solar power condition of four solar power stations.

![Figure 18: Water storage variations of two main hydropower stations under three inflow scenarios. The figure consists of two side-by-side line charts. The left chart shows H_1 Water storage (10^9 m^3) from 7.80 to 7.88 over 24 hours for Low inflow (solid blue), High inflow (dashed blue), H_1 (solid red), and H_2 (dashed red). The right chart shows H_2 Water storage (10^9 m^3) from 29.835 to 29.860 over 24 hours for the same four scenarios.](fc857414626a8d94d132e12d9afe52a4_img.jpg)

Figure 18: Water storage variations of two main hydropower stations under three inflow scenarios. The figure consists of two side-by-side line charts. The left chart shows H\_1 Water storage (10^9 m^3) from 7.80 to 7.88 over 24 hours for Low inflow (solid blue), High inflow (dashed blue), H\_1 (solid red), and H\_2 (dashed red). The right chart shows H\_2 Water storage (10^9 m^3) from 29.835 to 29.860 over 24 hours for the same four scenarios.

Fig. 18. Water storage variations of two main hydropower stations under three inflow scenarios.

several key derived output variables — such as  $\widehat{Q}_i$ ,  $\widehat{RQ}_i$ ,  $\widehat{p}^h$  — highlighting its limitations in capturing strongly coupled variables or those variables driven by complex physical mechanisms.

The PC-LSTM enables more comprehensive and balanced fitting across all 43 output variables by incorporating physics-constrained architecture. It achieves  $R^2$  values approaching 1 in nearly all dimensions, demonstrating superior prediction performance among different variables.

### 4.2.2. Evaluation results for physical consistency

Considering the poor physical interpretability of machine learning models, it is also necessary to validate the physical constraint errors — which includes the cascade hydraulic balance error ( $FBE$ ,  $RFBE$ ), water storage balance error ( $WBE$ ,  $RWBE$ ), energy storage balance error ( $EBE$ ,  $REBE$ ), and load balance error ( $LBE$ ,  $RLBE$ ) of the three models — to assess their physical applicability. All these metrics are computed based on the results from the testing samples.

Table 9 summarizes the physical consistency evaluation results of the

three LSTM-based models on the testing samples. It indicates that the PC-LSTM model outperforms the other two models across all indicators, demonstrating the strongest capability in maintaining physical consistency. These results highlight that the standard LSTM model, which lacks any physical constraints, exhibits significant deviations from physical balance except for water storage balance, making it unsuitable for applications.

Due to the inclusion of physical relationships in both PA-LSTM and PC-LSTM, these models generally exhibit strong physical interpretability, except for slight deviations observed in  $REBE$ . The deviation in  $REBE$  primarily arises from the fact that the predicted variable  $\widehat{RP}_{m,t}^{ps\_out}$  involved are simultaneously constrained by two interacting physical balance equations, as shown in Eq. (4.1). When conflicts occur between the two equations, the model prioritizes satisfying the load balance,

![Figure 19: Radar chart of R^2 for all output variables of three LSTM-based models. The chart shows the R^2 values for various variables across three models: LSTM (orange), PA-LSTM (green), and PC-LSTM (blue). The variables include E_{t+1}^{ps}, D, RD, Q_e, Q_o, RP^h, p^h, RQ_i, Q_i, V_T^h, V_{t+1}^h, RP^{ps\_out}, p^{ps\_out}, RP^{ps\_in}, p^{ps\_in}, RQ_e, and RQ_o. The PC-LSTM model consistently shows the highest R^2 values across most variables.](a3c02bfac05114bb808134408d67f20b_img.jpg)

Figure 19: Radar chart of R^2 for all output variables of three LSTM-based models. The chart shows the R^2 values for various variables across three models: LSTM (orange), PA-LSTM (green), and PC-LSTM (blue). The variables include E\_{t+1}^{ps}, D, RD, Q\_e, Q\_o, RP^h, p^h, RQ\_i, Q\_i, V\_T^h, V\_{t+1}^h, RP^{ps\\_out}, p^{ps\\_out}, RP^{ps\\_in}, p^{ps\\_in}, RQ\_e, and RQ\_o. The PC-LSTM model consistently shows the highest R^2 values across most variables.

Fig. 19. Radar chart of  $R^2$  for all output variables of three LSTM-based models.

Table 8

Accuracy evaluation metrics of three LSTM-based models across different samples.

| Model/<br>Indicators | LSTM             |                    |                 | PA-LSTM          |                    |                 | PC-LSTM          |                    |                 |
|----------------------|------------------|--------------------|-----------------|------------------|--------------------|-----------------|------------------|--------------------|-----------------|
|                      | Training samples | Validation samples | Testing samples | Training samples | Validation samples | Testing samples | Training samples | Validation samples | Testing samples |
| RMSE                 | 94.050           | 72.813             | 71.241          | 60.255           | 74.329             | 52.463          | 53.081           | 46.863             | 44.136          |
| MAE                  | 36.309           | 41.792             | 40.841          | 20.630           | 41.114             | 26.285          | 16.124           | 22.287             | 21.355          |
| $R^2$                | 0.836            | 0.839              | 0.843           | 0.734            | 0.654              | 0.721           | 0.942            | 0.929              | 0.939           |

![Figure 20: Six scatter plots (a-f) comparing observed vs. predicted water release for three LSTM models (LSTM, PA-LSTM, PC-LSTM) at three hydropower stations (H1, H2, H3). The top row (a-c) shows current water release, and the bottom row (d-f) shows future average water release. The x-axis is 'Observation (m³/s)' and the y-axis is 'Prediction (m³/s)'. A dashed diagonal line represents perfect prediction. The PC-LSTM model (blue dots) consistently follows the diagonal line more closely than the other models.](f4d72193f77f6646a2a1f4baaa927154_img.jpg)

Figure 20: Six scatter plots (a-f) comparing observed vs. predicted water release for three LSTM models (LSTM, PA-LSTM, PC-LSTM) at three hydropower stations (H1, H2, H3). The top row (a-c) shows current water release, and the bottom row (d-f) shows future average water release. The x-axis is 'Observation (m³/s)' and the y-axis is 'Prediction (m³/s)'. A dashed diagonal line represents perfect prediction. The PC-LSTM model (blue dots) consistently follows the diagonal line more closely than the other models.

**Fig. 20.** Scatter plots of observations and predictions for hydropower stations decision variables of three LSTM-based models.

(a)–(c) Current water release; (d)–(f) Future average water release.

![Figure 21: Six scatter plots (a-f) comparing observed vs. predicted solar power output for three LSTM models (LSTM, PA-LSTM, PC-LSTM) at three solar power stations (H1, H2, H3). The top row (a-d) shows current solar power output, and the bottom row (e-h) shows future average solar power output. The x-axis is 'Observation (m³/s)' and the y-axis is 'Prediction (m³/s)'. A dashed diagonal line represents perfect prediction. The PC-LSTM model (blue dots) shows the highest correlation with the diagonal line.](a706c91f074ac2840c161a3d4a7c0f91_img.jpg)

Figure 21: Six scatter plots (a-f) comparing observed vs. predicted solar power output for three LSTM models (LSTM, PA-LSTM, PC-LSTM) at three solar power stations (H1, H2, H3). The top row (a-d) shows current solar power output, and the bottom row (e-h) shows future average solar power output. The x-axis is 'Observation (m³/s)' and the y-axis is 'Prediction (m³/s)'. A dashed diagonal line represents perfect prediction. The PC-LSTM model (blue dots) shows the highest correlation with the diagonal line.

**Fig. 21.** Scatter plots of observations and predictions for solar power stations decision variables of three LSTM-based models.

(a)–(d) Current solar power output; (e)–(h) Future average solar power output.

which is directly tied to real-time system operation and power supply reliability. Consequently, minor violations are propagated into the *REBE*, resulting in a small but acceptable deviation. This trade-off reflects the model's emphasis on maintaining operational feasibility over perfect equality across coupled constraints.

$$RD = f\left(RL_t, \widehat{RP}_{it}^h, \widehat{RP}_{jt}^s, \widehat{RP}_{mt}^{ps-out}\right)$$

$$E_m^{T+1} = f\left(t, \widehat{P}_{mt}^{ps-out}, \widehat{P}_{mt}^{ps-in}, \widehat{RP}_{mt}^{ps-out}, \widehat{RP}_{mt}^{ps-in}\right) \quad (4.1)$$

Although neither PA-LSTM nor PC-LSTM fully meets energy storage balance, PC-LSTM still outperforms PA-LSTM in terms of error magnitude. This suggests that the physics-constrained structured design of PC-

![Figure 22: Four scatter plots (a, b, c, d) comparing observations and predictions for three LSTM-based models (LSTM, PA-LSTM, PC-LSTM). The x-axis for all plots is 'Observation (10^4 kW)'. (a) Current generation power output, (b) Current pumping power output, (c) Future average generation power output, and (d) Future average pumping power output. The y-axis for (a), (b), and (c) is 'Prediction (10^4 kW)', while for (d) it is 'Prediction (10^4 kW)'. The PC-LSTM model (blue dots) consistently shows the highest correlation with the observation line.](b6750d26d3dd287a4a4d49b3670a44bd_img.jpg)

Figure 22: Four scatter plots (a, b, c, d) comparing observations and predictions for three LSTM-based models (LSTM, PA-LSTM, PC-LSTM). The x-axis for all plots is 'Observation (10^4 kW)'. (a) Current generation power output, (b) Current pumping power output, (c) Future average generation power output, and (d) Future average pumping power output. The y-axis for (a), (b), and (c) is 'Prediction (10^4 kW)', while for (d) it is 'Prediction (10^4 kW)'. The PC-LSTM model (blue dots) consistently shows the highest correlation with the observation line.

**Fig. 22.** Scatter plots of observations and predictions for PS power station decision variables of three LSTM-based models.

(a) Current generation power output; (b) Current pumping power output; (c) Future average generation power output; (d) Future average pumping power output.

**Table 9**

Evaluation metrics for physical consistency of three LSTM-based models on testing samples.

| PBE/Model               | LSTM    | PA-LSTM | PC-LSTM |
|-------------------------|---------|---------|---------|
| $FBE_2$ ( $m^3/s$ )     | 278.814 | 0       | 0       |
| $FBE_3$ ( $m^3/s$ )     | 228.744 | 0       | 0       |
| $RFBE_2$ ( $m^3/s$ )    | 33.432  | 0       | 0       |
| $RFBE_3$ ( $m^3/s$ )    | 48.020  | 0       | 0       |
| $WBE_1$ ( $10^9 m^3$ )  | 0.029   | 0       | 0       |
| $WBE_2$ ( $10^9 m^3$ )  | 0.081   | 0       | 0       |
| $WBE_3$ ( $10^9 m^3$ )  | 0.002   | 0       | 0       |
| $RWBE_1$ ( $10^9 m^3$ ) | 0.026   | 0       | 0       |
| $RWBE_2$ ( $10^9 m^3$ ) | 0.086   | 0       | 0       |
| $RWBE_3$ ( $10^9 m^3$ ) | 0.002   | 0       | 0       |
| $EBE$ (kW-h)            | 72.504  | 0       | 0       |
| $REBE$ (kW-h)           | 93.259  | 97.043  | 38.592  |
| $LBE$ (kW)              | 90.210  | 0       | 0       |
| $RLBE$ (kW)             | 13.320  | 0       | 0       |

LSTM effectively promotes the evolution of model predictions toward greater physical interpretability.

To further assess violations of physical constraints, the constraint violation rate was calculated with respect to physical balance ( $PC\_CVR$ ) and upper and lower boundaries ( $BC\_CVR$ ). In this study, model predictions are considered compliant with physical constraints if the deviation remains within  $\pm 5\%$ .

Table 10 and Fig. 23(a) present a comparison of  $PC\_CVR$  under physical balance constraints for the three LSTM-based models. Overall, the PC-LSTM model exhibits superior performance, achieving lower violation rates across all physical balance constraints compared to PA-LSTM and the standard LSTM. Notably, for the  $REBE$ , only 6.46 % of the scheduling rules generated by PC-LSTM exhibit violations, whereas both PA-LSTM and standard LSTM show violation rates exceeding 30 %.

Table 11 and Fig. 23(b) present a comparison of  $BC\_CVR$  under physical upper and lower boundary constraints for the three LSTM-based models. Among the 43 output variables, only seven variables exhibit boundary violations. It is obvious that the standard LSTM model

shows the lowest violation rate, as all its output variables are predicted directly by the model without involving any physically derived relationships, making it easier to maintain variable bounds in a purely data-driven framework.

In contrast, both the PA-LSTM and PC-LSTM models incorporate physical derivation mechanisms, resulting in low violation rates for a few variables. Generally, the PC-LSTM model effectively guides the predicted results toward physically feasible space, demonstrating greater practicality in the modeling and operation of multi-energy systems through its physics-constrained structured design.

### 4.2.3. Evaluation results for stability and generalization

#### (1) Training process

Fig. 24 illustrates the evolution of the loss function during the training process of the three LSTM-based models. Both the training loss and validation loss decrease rapidly as the number of iterations increases and gradually stabilize after approximately 100 iterations, ultimately

![Figure 23: Statistical comparison of CVR for three LSTM-based models. (a) PC_CVR and (b) BC_CVR. The x-axis is CVR (%). The y-axis lists variables: RLBE, LBE, REBE, EBE, RFBE3, RFBE2, FBE3, FBE2, P1^h, P2^h, RP1^h, RP2^h, RP3^h, D, and RD. The legend indicates LSTM (orange), PA-LSTM (green), and PC-LSTM (blue). PC-LSTM consistently shows the lowest CVR across most variables.](3d827c43b44a567da971c01073295d3d_img.jpg)

Figure 23: Statistical comparison of CVR for three LSTM-based models. (a) PC\_CVR and (b) BC\_CVR. The x-axis is CVR (%). The y-axis lists variables: RLBE, LBE, REBE, EBE, RFBE3, RFBE2, FBE3, FBE2, P1^h, P2^h, RP1^h, RP2^h, RP3^h, D, and RD. The legend indicates LSTM (orange), PA-LSTM (green), and PC-LSTM (blue). PC-LSTM consistently shows the lowest CVR across most variables.

**Fig. 23.** Statistical comparison of CVR for three LSTM-based models. (a)  $PC\_CVR$ ; (b)  $BC\_CVR$ .

**Table 11**

$BC\_CVR$  of three LSTM-based models on testing samples.

| $BC\_CVR$ (%)/Model | LSTM | PA-LSTM | PC-LSTM |
|---------------------|------|---------|---------|
| $P_1^h$             | 0    | 12.8    | 12.5    |
| $P_2^h$             | 0    | 1.1     | 0.6     |
| $RP_1^h$            | 0.7  | 0.3     | 0.4     |
| $RP_2^h$            | 0.1  | 0       | 0.1     |
| $RP_3^h$            | 0.6  | 0.3     | 0.2     |
| $D$                 | 0    | 5.7     | 1.3     |
| $RD$                | 0    | 0.5     | 0.4     |

![Figure 24: Training process of three LSTM-based models. The figure consists of three vertically stacked subplots labeled (a) LSTM, (b) PA-LSTM, and (c) PC-LSTM. Each subplot shows 'Evolution loss' on the y-axis (ranging from 0.00 to 0.24) against 'Iterations' on the x-axis (ranging from 0 to 1000). Each plot contains two lines: a blue line for the 'Training process' and an orange line for the 'Validation process'. In all three cases, the loss decreases rapidly and then plateaus at a low value, with the training and validation losses being very close to each other, indicating good generalization.](7bed2d7c96d86bf922295a1252da52a5_img.jpg)

Figure 24: Training process of three LSTM-based models. The figure consists of three vertically stacked subplots labeled (a) LSTM, (b) PA-LSTM, and (c) PC-LSTM. Each subplot shows 'Evolution loss' on the y-axis (ranging from 0.00 to 0.24) against 'Iterations' on the x-axis (ranging from 0 to 1000). Each plot contains two lines: a blue line for the 'Training process' and an orange line for the 'Validation process'. In all three cases, the loss decreases rapidly and then plateaus at a low value, with the training and validation losses being very close to each other, indicating good generalization.

Fig. 24. Training process of three LSTM-based models.

**Table 12**  
Evaluation metrics for model stability and generalization of three LSTM-based models.

| Indicators/Model | LSTM  | PA-LSTM | PC-LSTM |
|------------------|-------|---------|---------|
| Loss Gap         | 0.003 | 0.004   | 0.004   |
| RMSE Gap         | 21.24 | 14.07   | 6.22    |
| AR <sup>2</sup>  | 0.841 | 0.717   | 0.938   |

converging to a low level after around 1000 iterations. This indicates that the model achieves a good fit on both the training and validation samples. The small gap between the two curves suggests the absence of significant overfitting. These results confirm the effectiveness of the proposed models' architecture and parameters.

#### (2) Evaluation metrics for model stability and generalization

**Table 12** presents a comparison of the three LSTM models based on three evaluation metrics for model stability and generalization, which includes *Loss Gap* and *RMSE Gap* between training samples and validation samples as well as *AR<sup>2</sup>* on training samples.

All three LSTM-based models achieve very low values on *Loss Gap*, suggesting smaller performance deviation between training and validation samples, and reflecting stronger robustness and generalization. In terms of *RMSE Gap* and *AR<sup>2</sup>*, the PC-LSTM clearly demonstrates better performance than the other two models, implying strong interpretability even after accounting for the high dimensionality of input and output variables.

#### (3) Operation schemes extracted by three LSTM-based models

To further evaluate the specific schemes extracted by the LSTM-based models, an operation scenario has been chosen to make several comparisons. First, **Fig. 25** presents the baseline operation schemes (which can be regarded as true observations) and operation schemes extracted by the three LSTM-based models on a representative operation scenario. It is evident that the grid load demand cannot be completely met in this scenario from the baseline schemes, and schemes extracted by PC-LSTM are closer to baseline schemes, which means the PC-LSTM

![Figure 25: Comparison of operation schemes for current stage between baseline schemes and schemes extracted by three LSTM-based models. The figure consists of four subplots: (a) Baseline, (b) LSTM, (c) PA-LSTM, and (d) PC-LSTM. Each subplot shows 'Power (10^4 kW)' on the y-axis (ranging from -200 to 1200) against 'Hour (h)' on the x-axis (ranging from 3 to 24). The legend for each plot includes: p^h (blue), p^s_out (orange), p^s_out (green), p^s_in (purple), and L (red dashed line). The baseline (a) shows a significant gap between the total power and the load L. The LSTM (b) and PA-LSTM (c) also show gaps, but the PC-LSTM (d) shows power levels that closely follow the load L, indicating better extraction of operation schemes.](8f223b4a29a6070b2489baf2ca803465_img.jpg)

Figure 25: Comparison of operation schemes for current stage between baseline schemes and schemes extracted by three LSTM-based models. The figure consists of four subplots: (a) Baseline, (b) LSTM, (c) PA-LSTM, and (d) PC-LSTM. Each subplot shows 'Power (10^4 kW)' on the y-axis (ranging from -200 to 1200) against 'Hour (h)' on the x-axis (ranging from 3 to 24). The legend for each plot includes: p^h (blue), p^s\_out (orange), p^s\_out (green), p^s\_in (purple), and L (red dashed line). The baseline (a) shows a significant gap between the total power and the load L. The LSTM (b) and PA-LSTM (c) also show gaps, but the PC-LSTM (d) shows power levels that closely follow the load L, indicating better extraction of operation schemes.

Fig. 25. Comparison of operation schemes for current stage between baseline schemes and schemes extracted by three LSTM-based models.

![Figure 26: Bar chart comparing daily hydropower output (P^h) for current stage (H1, H2, H3) between Baseline, LSTM, PA-LSTM, and PC-LSTM models. The y-axis is Daily hydropower output P^h (10^4 kW) from 0 to 4500. The x-axis shows three stages: H1, H2, and H3. In H1, Baseline is ~2500, LSTM is ~2700, PA-LSTM is ~2600, and PC-LSTM is ~2600. In H2, Baseline is ~4800, LSTM is ~4700, PA-LSTM is ~4800, and PC-LSTM is ~4800. In H3, Baseline is ~1500, LSTM is ~1200, PA-LSTM is ~1200, and PC-LSTM is ~1200.](96a7eac66ef72bb016c280278506ac63_img.jpg)

Figure 26: Bar chart comparing daily hydropower output (P^h) for current stage (H1, H2, H3) between Baseline, LSTM, PA-LSTM, and PC-LSTM models. The y-axis is Daily hydropower output P^h (10^4 kW) from 0 to 4500. The x-axis shows three stages: H1, H2, and H3. In H1, Baseline is ~2500, LSTM is ~2700, PA-LSTM is ~2600, and PC-LSTM is ~2600. In H2, Baseline is ~4800, LSTM is ~4700, PA-LSTM is ~4800, and PC-LSTM is ~4800. In H3, Baseline is ~1500, LSTM is ~1200, PA-LSTM is ~1200, and PC-LSTM is ~1200.

Fig. 26. Comparison of daily hydropower output for current stage between baseline schemes and schemes extracted by three LSTM-based models.

![Figure 27: Bar chart comparing daily solar power output (P^s_out) for current stage (S1, S2, S3, S4) between Baseline, LSTM, PA-LSTM, and PC-LSTM models. The y-axis is Daily solar power output P^s_out (10^4 kW) from 0 to 4000. The x-axis shows four stages: S1, S2, S3, and S4. In S1, Baseline is ~1500, LSTM is ~1500, PA-LSTM is ~1500, and PC-LSTM is ~1500. In S2, Baseline is ~500, LSTM is ~500, PA-LSTM is ~500, and PC-LSTM is ~500. In S3, Baseline is ~3500, LSTM is ~3500, PA-LSTM is ~3500, and PC-LSTM is ~3500. In S4, Baseline is ~2000, LSTM is ~1800, PA-LSTM is ~1800, and PC-LSTM is ~1800.](f85bf99d372e735d228361bf4d3cf7e6_img.jpg)

Figure 27: Bar chart comparing daily solar power output (P^s\_out) for current stage (S1, S2, S3, S4) between Baseline, LSTM, PA-LSTM, and PC-LSTM models. The y-axis is Daily solar power output P^s\_out (10^4 kW) from 0 to 4000. The x-axis shows four stages: S1, S2, S3, and S4. In S1, Baseline is ~1500, LSTM is ~1500, PA-LSTM is ~1500, and PC-LSTM is ~1500. In S2, Baseline is ~500, LSTM is ~500, PA-LSTM is ~500, and PC-LSTM is ~500. In S3, Baseline is ~3500, LSTM is ~3500, PA-LSTM is ~3500, and PC-LSTM is ~3500. In S4, Baseline is ~2000, LSTM is ~1800, PA-LSTM is ~1800, and PC-LSTM is ~1800.

Fig. 27. Comparison of daily solar power output for current stage between baseline schemes and schemes extracted by three LSTM-based models.

performs much better than two other models in extracting operation schemes. Figs. 26 and 27 compare the daily hydropower and solar power output for the current stage. The power output of the PC-LSTM model is almost identical to that of the baseline schemes, whereas the power output of the other two models deviate to some extent.

Second, Fig. 28 shows the objectives of the four operation schemes. The PC-LSTM model matches significantly better in both total power

![Figure 28: Two line charts comparing objectives. (a) Total power output process: The y-axis is Total power output (10^4 kW) from 400 to 1000. The x-axis is Hour (h) from 3 to 24. Baseline (dashed red), LSTM (solid orange), PA-LSTM (solid green), and PC-LSTM (solid blue) are plotted. PC-LSTM closely follows the Baseline. (b) Residual grid demand load: The y-axis is Residual grid demand load (10^4 kW) from -150 to 450. The x-axis is Hour (h) from 3 to 24. Baseline (dashed red), LSTM (solid orange), PA-LSTM (solid green), and PC-LSTM (solid blue) are plotted. PC-LSTM closely follows the Baseline.](58f42a91047786934d8a7e258d581ca2_img.jpg)

Figure 28: Two line charts comparing objectives. (a) Total power output process: The y-axis is Total power output (10^4 kW) from 400 to 1000. The x-axis is Hour (h) from 3 to 24. Baseline (dashed red), LSTM (solid orange), PA-LSTM (solid green), and PC-LSTM (solid blue) are plotted. PC-LSTM closely follows the Baseline. (b) Residual grid demand load: The y-axis is Residual grid demand load (10^4 kW) from -150 to 450. The x-axis is Hour (h) from 3 to 24. Baseline (dashed red), LSTM (solid orange), PA-LSTM (solid green), and PC-LSTM (solid blue) are plotted. PC-LSTM closely follows the Baseline.

Fig. 28. Comparison of objectives between baseline schemes and schemes extracted by three LSTM-based models.

(a) Total power output process; (b) Residual grid demand.

![Figure 29: Three line charts comparing release (m^3/s) for current stage (H1, H2, H3) between Baseline, LSTM, PA-LSTM, and PC-LSTM models. The y-axis is Release (m^3/s) from 0 to 1500. The x-axis is Hour (h) from 3 to 24. (a) H1: Baseline is ~1200, LSTM is ~1100, PA-LSTM is ~1100, and PC-LSTM is ~1100. (b) H2: Baseline is ~1100, LSTM is ~1000, PA-LSTM is ~1000, and PC-LSTM is ~1000. (c) H3: Baseline is ~1100, LSTM is ~1000, PA-LSTM is ~1000, and PC-LSTM is ~1000. PC-LSTM closely follows the Baseline in all cases.](13a4a158a9595280857f51d81e23e776_img.jpg)

Figure 29: Three line charts comparing release (m^3/s) for current stage (H1, H2, H3) between Baseline, LSTM, PA-LSTM, and PC-LSTM models. The y-axis is Release (m^3/s) from 0 to 1500. The x-axis is Hour (h) from 3 to 24. (a) H1: Baseline is ~1200, LSTM is ~1100, PA-LSTM is ~1100, and PC-LSTM is ~1100. (b) H2: Baseline is ~1100, LSTM is ~1000, PA-LSTM is ~1000, and PC-LSTM is ~1000. (c) H3: Baseline is ~1100, LSTM is ~1000, PA-LSTM is ~1000, and PC-LSTM is ~1000. PC-LSTM closely follows the Baseline in all cases.

Fig. 29. Comparison of release for current stage between baseline schemes and schemes extracted by three LSTM-based models.

output and grid load demand, and the residual load demand is much more stable compared with the other two models.

Third, Fig. 29 compares the water release for the current stage of three hydropower stations on the representative operation scenario. Overall, all three LSTM-based models demonstrate satisfactory performance in capturing the release variation, with predictions all closely following the baseline schemes. The PC-LSTM performs better than the other two models.

As for the operation schemes for future stages, as shown in Fig. 30, all three models perform comparably well. This is largely because the operation data for future stages are averaged. The averaged value results in smooth variations, which makes it easier for machine learning models to learn and generalize the underlying patterns, thereby enhancing prediction accuracy.

Generally, in the operation schemes for the current stage, PC-LSTM outperforms the other two models in terms of both total power output and grid load demand tracking performance, followed by LSTM and PA-LSTM. Notably, for variables with strong discontinuities — such as PS power output, which often contains many 0–1 switching values — LSTM and PA-LSTM struggle to accurately predict. In contrast, PC-LSTM benefits from a physics-constrained output layer, significantly improving the prediction accuracy and physical infeasibility.

#### (4) Sensitivity analysis of uncertain input conditions

To evaluate the effect of inflow forecast uncertainty on model performance, random noises ranging from  $-10\%$  to  $+10\%$  were added to the inflow inputs, and the trained models were tested without retraining.

As shown in Table 13, all models experienced a gradual decline in  $R^2$  and maintained a stable range in PC-CVR as the noise level increased. However, the degree of degradation varied substantially among the 


![Figure 30: Comparison of operation schemes for future stage between baseline schemes and schemes extracted by three LSTM-based models. The figure consists of four subplots: (a) Baseline, (b) LSTM, (c) PA-LSTM, and (d) PC-LSTM. Each subplot shows Power (10^4 kW) on the y-axis (ranging from -200 to 1200) versus Hour (h) on the x-axis (ranging from 3 to 21). The power is decomposed into four components: RP^h (blue), RP^s_out (orange), RP^s_in (purple), and RL (red dashed line). The PC-LSTM model (d) shows the most stable and consistent power output across the 24-hour period.](2a77eb32ef4c4d8a5c1758a53a908336_img.jpg)

Figure 30: Comparison of operation schemes for future stage between baseline schemes and schemes extracted by three LSTM-based models. The figure consists of four subplots: (a) Baseline, (b) LSTM, (c) PA-LSTM, and (d) PC-LSTM. Each subplot shows Power (10^4 kW) on the y-axis (ranging from -200 to 1200) versus Hour (h) on the x-axis (ranging from 3 to 21). The power is decomposed into four components: RP^h (blue), RP^s\_out (orange), RP^s\_in (purple), and RL (red dashed line). The PC-LSTM model (d) shows the most stable and consistent power output across the 24-hour period.

Fig. 30. Comparison of operation schemes for future stage between baseline schemes and schemes extracted by three LSTM-based models.

**Table 13**  
Robustness of three LSTM-based models under different inflow forecast noise levels.

| Indicators | Noise Level (%) | LSTM  | PA-LSTM | PC-LSTM |
|------------|-----------------|-------|---------|---------|
| $R^2$      | 0               | 0.843 | 0.721   | 0.939   |
|            | -5              | 0.797 | 0.684   | 0.927   |
|            | -10             | 0.721 | 0.622   | 0.870   |
|            | 5               | 0.818 | 0.709   | 0.913   |
|            | 10              | 0.745 | 0.644   | 0.891   |
|            | 15              | 0.681 | 0.581   | 0.865   |
| $PC_{CVR}$ | 0               | 45.4  | 2.54    | 0.46    |
|            | -5              | 40.7  | 1.97    | 0.55    |
|            | -10             | 44.1  | 2.03    | 0.34    |
|            | 5               | 48.2  | 3.62    | 0.49    |
|            | 10              | 50.2  | 2.98    | 0.51    |
|            | 15              | 52.1  | 3.12    | 0.53    |

three models.

As shown in Fig. 31, the PC-LSTM model clearly demonstrated the highest robustness across all noise levels. Even under  $\pm 10\%$  noise level, its  $R^2$  remained above 0.89. In contrast, the other two LSTM models

showed a notable drop in  $R^2$ . Moreover, the PC-LSTM model exhibited lowest  $PC_{CVR}$  under perturbations, indicating that its structured physical constraints effectively mitigate bias propagation regardless of the perturbation direction.

# 5. Conclusions

To achieve stable, widely applicable, and economically efficient optimal scheduling strategies for a HSPSCPS, this study proposes a PC-LSTM model with a structured output layer allied with an OED and a two-stage scheduling framework. Upon completion of training, the proposed model effectively captures the complex nonlinear relationships between system inputs and outputs, enabling the generation of physically consistent scheduling schemes in real-time for any given input condition.

The proposed PC-LSTM model is applied to the *CEB* and benchmarked against two reference models—a standard LSTM and a PA-LSTM. The main conclusions are as follows:

![Figure 31: Comparison of R^2 and PC-CVR of three LSTM-based models under different inflow noise levels. The figure consists of two subplots. The left subplot shows R^2 (ranging from 0.6 to 1.0) versus Noise Level (%) (ranging from -10 to 10). The right subplot shows PC_CVR (%) (ranging from 0 to 50) versus Noise Level (%). Both plots compare LSTM (orange line with circles), PA-LSTM (green line with circles), and PC-LSTM (blue line with triangles). The PC-LSTM model consistently shows the highest R^2 and the lowest PC_CVR across all noise levels.](d7963aa42787a89916410bcc1a36900f_img.jpg)

Figure 31: Comparison of R^2 and PC-CVR of three LSTM-based models under different inflow noise levels. The figure consists of two subplots. The left subplot shows R^2 (ranging from 0.6 to 1.0) versus Noise Level (%) (ranging from -10 to 10). The right subplot shows PC\_CVR (%) (ranging from 0 to 50) versus Noise Level (%). Both plots compare LSTM (orange line with circles), PA-LSTM (green line with circles), and PC-LSTM (blue line with triangles). The PC-LSTM model consistently shows the highest R^2 and the lowest PC\_CVR across all noise levels.

Fig. 31. Comparison of  $R^2$  and  $PC_{CVR}$  of three LSTM-based models under different inflow noise levels.

- (1) The OED successfully reduces the original 115,200 operation scenarios to 14,400 representative cases, achieving an 87.5 % reduction in training workload while maintaining comprehensive coverage of both typical and extreme operating conditions.
- (2) The PC-LSTM model exhibits the highest prediction accuracy and stability among the three models, as verified by  $RMSE$ ,  $MAE$ , and  $R^2$  metrics. This confirms the effectiveness of embedding physical constraints into the structured output layer.
- (3) In terms of physical consistency, the constraint violation rate  $PC\_CVR$  is reduced from 45.4 % (LSTM) and 2.54 % (PA-LSTM) to only 0.46 % (PC-LSTM), demonstrating the strongest capability in maintaining physical consistency of PC-LSTM.
- (4) Analyses of training loss curves,  $Loss\ Gap$ ,  $RMSE\ Gap$ , and  $AR^2$  show that PC-LSTM achieves stable convergence and strong generalization ability, confirming its robustness under dynamic conditions.
- (5) The PC-LSTM also achieves better total power output and load-tracking performance even under extreme operating conditions, benefiting from the explicit enforcement of physical constraints in the output layer.
- (6) In addition, the model demonstrates excellent computational efficiency: training on 9,600 hourly samples requires approximately 800 s, while predicting 2,400 hourly steps takes about 10 s. With a sufficiently large and continuously updated training database, the model can further evolve through offline learning, continuously improving its adaptability and long-term performance.

Overall, the proposed PC-LSTM framework achieves a well-balanced combination of accuracy, physical consistency, stability, and computational efficiency, making it a promising and scalable solution for intelligent scheduling of multi-energy complementary systems. Future work will focus on extending this framework to large-scale regional applications, incorporating uncertainty modeling and reinforcement learning to enable dynamic, adaptive optimization under complex and uncertain conditions.

# CrediT authorship contribution statement

**Lingwei Zhu:** Writing – original draft, Visualization, Validation, Software, Methodology, Formal analysis, Conceptualization. **Bin Xu:** Writing – review & editing, Validation, Supervision, Funding acquisition, Conceptualization. **Xinrong Wang:** Visualization, Software, Investigation. **Huili Wang:** Methodology, Investigation. **Xinman Qin:** Software, Methodology. **Jiayi Jiang:** Software, Methodology. **Jinshu Li:** Validation, Supervision. **William W.-G. Yeh:** Writing – review & editing, Supervision, Funding acquisition. **Shanshui Yuan:** Funding acquisition. **Wei Zhi:** Funding acquisition.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Acknowledgement

This study was supported by the National Natural Science Foundation of China (Grant No. 52322902, 52279010), the Fundamental Research Funds for the Central Universities (B250205006), the Foundation of National Key Laboratory of Water Disaster Prevention (Grant No. 5240152L2). Partial support also was provided by an AECOM

# endowment.Glossary

| Abbreviations                      |                                                                         |
|------------------------------------|-------------------------------------------------------------------------|
| EOM                                | Explicit Optimization Model                                             |
| IOM                                | Implicit Optimization Model                                             |
| LSTM                               | Long Short-Term Memory                                                  |
| PA-LSTM                            | Physics-Adjusted Long Short-Term Memory                                 |
| PC-LSTM                            | Physics-Constrained Long Short-Term Memory                              |
| OED                                | Orthogonal Experimental Design                                          |
| OA                                 | Orthogonal Array                                                        |
| HSPSCPS                            | Hydro-Solar-Pumped Storage Complementary Power System                   |
| PS                                 | pumped-storage                                                          |
| CEB                                | clean energy base                                                       |
| FBE                                | hydraulic balance error in the current operation time period            |
| RFBE                               | hydraulic balance error for the remaining operation time periods        |
| WBE                                | water storage balance error in the current operation time period        |
| RWBE                               | water storage balance error for the remaining operation time periods    |
| EBE                                | energy storage balance error                                            |
| REBE                               | energy storage balance error                                            |
| LBE                                | load balance error                                                      |
| RLBE                               | load balance error                                                      |
| PC_CVR                             | Constraint violation rate with respect to physical balance              |
| BC_CVR                             | Constraint violation rate with respect to upper and lower boundaries    |
| Indices                            |                                                                         |
| $i$                                | index of hydropower stations, from 1 to $I$                             |
| $j$                                | index of solar power stations, from 1 to $J$                            |
| $m$                                | index of pumped-storage power stations, from 1 to $M$                   |
| $t$                                | index of operation time periods                                         |
| Parameters                         |                                                                         |
| $I$                                | total number of hydropower stations                                     |
| $J$                                | total number of solar power stations                                    |
| $M$                                | total number of pumped-storage power stations                           |
| $\Delta t$                         | time interval ( $h$ ), $\Delta t = 1h$                                  |
| $T$                                | total operation time periods, $T = 24$                                  |
| $T-t$                              | the remaining operation periods                                         |
| $k$                                | efficiency coefficient of hydropower station                            |
| $\eta$                             | pumping efficiency coefficient, $\eta = 0.75$                           |
| Variables                          |                                                                         |
| $\tau_i$                           | runoff time lag ( $h$ )                                                 |
| $m_i^h$                            | penalty for hydropower curtailment                                      |
| $m_j^s$                            | penalty for solar power curtailment                                     |
| $\overline{\text{chan}}_{it}^h$    | capacity of hydropower output transmission route ( $10^4\ kW$ )         |
| $\overline{\text{chan}}_{jt}^s$    | capacity of solar power output transmission route ( $10^4\ kW$ )        |
| $\overline{\text{chan}}_{mt}^{ps}$ | capacity of pump-storage power output transmission route ( $10^4\ kW$ ) |
| $D_t$                              | residual grid demand load ( $10^4\ kW$ )                                |
| $E_{m,t}^{ps}$                     | energy storage ( $10^4\ kW\cdot h$ )                                    |
| $E_{m,0}^{ps}$                     | initial energy storage set by models ( $10^4\ kW\cdot h$ )              |
| $E_{m,1}^{ps}$                     | initial storage energy ( $10^4\ kW\cdot h$ )                            |
| $E_{m,T+1}^{ps}$                   | ending storage energy ( $10^4\ kW\cdot h$ )                             |
| $E_{m,t}^{ps,in}$                  | available pumping storage energy ( $10^4\ kW\cdot h$ )                  |
| $E_{m,t}^{ps,out}$                 | available generation storage energy ( $10^4\ kW\cdot h$ )               |
| $\overline{E}_m^{ps}$              | upper limit of energy storage ( $10^4\ kW\cdot h$ )                     |
| $H_{it}^h$                         | hydraulic head ( $m$ )                                                  |
| $\overline{H}_{it}^h$              | upper limit of hydraulic head ( $m$ )                                   |
| $\underline{H}_{it}^h$             | lower limit of hydraulic head ( $m$ )                                   |
| $L_t$                              | grid demand load ( $10^4\ kW$ )                                         |
| $p_{it}^h$                         | hydropower output ( $10^4\ kW$ )                                        |
| $p_{it}^{h,s}$                     | spilled hydropower output ( $10^4\ kW$ )                                |
| $\overline{p}_{it}^h$              | upper limit of hydropower output ( $10^4\ kW$ )                         |
| $\underline{p}_{it}^h$             | lower limit of hydropower output ( $10^4\ kW$ )                         |
| $p_{jt}^{s,in}$                    | input solar power ( $10^4\ kW$ )                                        |
| $p_{jt}^{s,out}$                   | solar power output ( $10^4\ kW$ )                                       |
| $p_{jt}^{s,grid}$                  | on-grid solar power output ( $10^4\ kW$ )                               |
| $p_{jt}^{s,s}$                     | spilled solar power ( $10^4\ kW$ )                                      |
| $\overline{p}_{jt}^{s,out}$        | upper limit of solar power output ( $10^4\ kW$ )                        |
| $\underline{p}_{jt}^{s,out}$       | lower limit of solar power output ( $10^4\ kW$ )                        |
| $p_{mt}^{ps,in}$                   | pumping power output ( $10^4\ kW$ )                                     |
| $p_{mt}^{ps,out}$                  | generation power output ( $10^4\ kW$ )                                  |
| $\overline{p}_{mt}^{ps,in}$        | upper limit of pumping power output ( $10^4\ kW$ )                      |
| $\underline{p}_{mt}^{ps,in}$       | lower limit of pumping power output ( $10^4\ kW$ )                      |

(continued on next page)

## Glossary (continued)

|                                |                                                                                                |
|--------------------------------|------------------------------------------------------------------------------------------------|
| $\bar{P}_{m,t}^{ps-out}$       | upper limit of generation power output ( $10^4$ kW)                                            |
| $\underline{P}_{m,t}^{ps-out}$ | lower limit of generation power output ( $10^4$ kW)                                            |
| $\bar{P}^{grid}$               | total on-grid power output ( $10^4$ kW)                                                        |
| $\bar{P}$                      | capacity of on-grid electricity transmission routes ( $10^4$ kW)                               |
| $Q_{i,t}^h$                    | inflow ( $m^3/s$ )                                                                             |
| $Q_{i,t}^0$                    | water release ( $m^3/s$ )                                                                      |
| $Q_{i,t}^{h,n}$                | nature/internal inflow ( $m^3/s$ )                                                             |
| $Q_{i,t}^{h,l}$                | time lag release ( $m^3/s$ )                                                                   |
| $Q_{i,t}^{h,g}$                | water release for power generation ( $m^3/s$ )                                                 |
| $Q_{i,t}^{h,s}$                | spilled water release ( $m^3/s$ )                                                              |
| $Q_{i,t}^{h,e}$                | ecological water release ( $m^3/s$ )                                                           |
| $\bar{Q}_{i,t}^h$              | upper limit of water release for power generation ( $m^3/s$ )                                  |
| $RD_t$                         | average residual grid demand load for the remaining operation periods ( $10^4$ kW)             |
| $R_{m,t}^{ps-in}$              | average available pumping storage energy for the remaining operation periods ( $10^4$ kW-h)    |
| $R_{m,t}^{ps-out}$             | average available generation storage energy for the remaining operation periods ( $10^4$ kW-h) |
| $RL_t$                         | average grid demand load for the remaining operation periods ( $10^4$ kW)                      |
| $R_{i,t}^{ph}$                 | average hydropower output for the remaining operation periods ( $10^4$ kW)                     |
| $R_{j,t}^{ps-out}$             | average solar power output for the remaining operation periods ( $10^4$ kW)                    |
| $R_{i,t}^{ps-in}$              | average pumping power output for the remaining operation periods ( $10^4$ kW)                  |
| $R_{m,t}^{ps-out}$             | average generation power output for the remaining operation periods ( $10^4$ kW)               |
| $RQ_{i,t}^h$                   | average inflow for the remaining operation periods ( $m^3/s$ )                                 |
| $RQ_{i,t}^0$                   | average water release for the remaining operation periods ( $m^3/s$ )                          |
| $RQ_{i,t}^{h,n}$               | average nature/internal inflow for the remaining operation periods ( $m^3/s$ )                 |
| $RQ_{i,t}^{h,l}$               | average time lag release for the remaining operation periods ( $m^3/s$ )                       |
| $RQ_{i,t}^{h,g}$               | average water release for power generation for the remaining operation periods ( $m^3/s$ )     |
| $V_{i,t}^h$                    | forebay water storage ( $10^9$ $m^3$ )                                                         |
| $\bar{V}_{i,t}^h$              | upper limit of forebay water storage ( $10^9$ $m^3$ )                                          |
| $\underline{V}_{i,t}^h$        | lower limit of forebay water storage ( $10^9$ $m^3$ )                                          |
| $V_{i,0}^h$                    | initial forebay water storage set by models ( $10^9$ $m^3$ )                                   |
| $V_{i,1}^h$                    | initial forebay water storage ( $10^9$ $m^3$ )                                                 |
| $V_{i,T+1}^h$                  | ending forebay water storage ( $10^9$ $m^3$ )                                                  |
| $V_{i,d}^h$                    | dead water storage ( $10^9$ $m^3$ )                                                            |
| $V_{i,fc}^h$                   | flood control water storage ( $10^9$ $m^3$ )                                                   |
| $V_{i,n}^h$                    | normal water storage ( $10^9$ $m^3$ )                                                          |
| $\Delta V_i^h$                 | water storage variation ( $10^9$ $m^3$ )                                                       |
| $Zup_{i,t}^h$                  | forebay water level (m)                                                                        |
| $Zdown_{i,t}^h$                | tailwater level (m)                                                                            |
| $Z_{i,d}^h$                    | dead control water level (m)                                                                   |
| $Z_{i,fc}^h$                   | flood control water level (m)                                                                  |
| $Z_{i,n}^h$                    | normal water level (m)                                                                         |

\*Additionally, variables with a hat ( $\hat{\cdot}$ ) denote output variables predicted by the LSTM models.

## Data availability

The authors do not have permission to share data.

# References

- Ávila, L., Mine, M.R.M., Kaviski, E., 2020. Probabilistic long-term reservoir operation employing copulas and implicit stochastic optimization. *Stoch. Env. Res. Risk A* 34, 931–947. <https://doi.org/10.1007/s00477-020-01826-9>.
- Ávila, L., Mine, M.R.M., Kaviski, E., Detzel, D.H.M., 2021. Evaluation of hydro-wind complementarity in the medium-term planning of electrical power systems by joint simulation of periodic streamflow and wind speed time series: a Brazilian case study. *Renew. Energy* 167, 685–699. <https://doi.org/10.1016/j.renene.2020.11.141>.
- Cao, Y., Mu, Y., Jia, H., Yu, X., Hou, K., Wang, H., 2024. A multi-objective stochastic optimization approach for planning a multi-energy microgrid considering unscheduled islanded operation. *IEEE Trans. Sustainable Energy* 15, 1300–1314. <https://doi.org/10.1109/tste.2023.3341898>.
- Celeste, A.B., Billib, M., 2009. Evaluation of stochastic reservoir operation optimization models. *Adv. Water Resour.* 32, 1429–1443. <https://doi.org/10.1016/j.advwatres.2009.06.008>.
- Chen, R., Wang, D., Mei, Y., Lin, Y., Lin, Z., Zhang, Z., et al., 2025. A knowledge-guided LSTM reservoir outflow model and its application to streamflow simulation in reservoir-regulated basins. *J. Hydrol.* 658. <https://doi.org/10.1016/j.jhydrol.2025.133164>.
- Ding, Z., Fang, G., Wen, X., Tan, Q., Mao, Y., Zhang, Y., 2024. Long-term operation rules of a hydro-wind-photovoltaic hybrid system considering forecast information. *Energy* 288. <https://doi.org/10.1016/j.energy.2023.129634>.
- Fan, W., Hao, Y., 2020. An empirical research on the relationship amongst renewable energy consumption, economic growth and foreign direct investment in China. *Renew. Energy* 146, 598–609. <https://doi.org/10.1016/j.renene.2019.06.170>.
- Fan, Y., Liu, W., Zhu, F., Wang, S., Yue, H., Zeng, Y., et al., 2024. Short-term stochastic multi-objective optimization scheduling of wind-solar-hydro hybrid system considering source-load uncertainties. *Appl. Energy* 372. <https://doi.org/10.1016/j.apenergy.2024.123781>.
- Feng, D., Liu, J., Lawson, K., Differentiable, S.C., 2022. Learnable, regionalized process-based models with multiphysical outputs can approach state-of-the-art hydrologic prediction accuracy. *Water Resour. Res.* 58. <https://doi.org/10.1029/2022wr032404>.
- Feng, Z.-k., Niu, W.-j., Cheng, C.-t., Liao, S.-l., 2017. Hydropower system operation optimization by discrete differential dynamic programming based on orthogonal experiment design. *Energy* 126, 720–732. <https://doi.org/10.1016/j.energy.2017.03.069>.
- Feng, Z.-k., Niu, W.-j., Zhang, R., Wang, S., Cheng, C.-t., 2019. Operation rule derivation of hydropower reservoir by k-means clustering method and extreme learning machine based on particle swarm optimization. *J. Hydrol.* 576, 229–238. <https://doi.org/10.1016/j.jhydrol.2019.06.045>.
- Fu, Y., Lu, Z., Hu, W., Wu, S., Wang, Y., Dong, L., et al., 2019. Research on joint optimal dispatching method for hybrid power system considering system security. *Appl. Energy* 238, 147–163. <https://doi.org/10.1016/j.apenergy.2019.01.034>.
- Giuliani, M., Castelletti, A., Mason, F., Mason, E., Curses, R.P.M., 2016. Tradeoffs, and scalable management: advancing evolutionary multiobjective direct policy search to improve water reservoir operations. *J. Water Resour. Plan. Manag.* 142. [https://doi.org/10.1061/\(asce\)wr.1943-5452.0000570](https://doi.org/10.1061/(asce)wr.1943-5452.0000570).
- Hochreiter, S.S., Jürgen, L.S.T.M., 1996. Can solve hard long time lag problems. *Neural Inf. Process. Syst. Found.* 473–479.
- Hochreiter SaS, Jürgen. Long short-term memory. *Neural Comput.* 1997;9:1735–1780. <https://doi.org/10.1162/neco.1997.9.8.1735>.
- Inc. I.S. LINGO – The modeling language and optimizer. Version 18.0 ed. Chicago, IL, USA: LINDO Systems Inc.; 2021.
- Kratzert, F.K., Daniel, Shalev, G., Klambauer, G., Hochreiter, S., Nearing, G., 2019. Towards learning universal, regional, and local hydrological behaviors via machine learning applied to large-sample datasets. *Hydrol. Earth Syst. Sci.* 23, 5089–5110. <https://doi.org/10.5194/hess-23-5089-2019>.
- Li, F., Chen, S., Ju, C., Zhang, X., Ma, G., Huang, W., 2023. Research on short-term joint optimization scheduling strategy for hydro-wind-solar hybrid systems considering uncertainty in renewable energy generation. *Energy. Strat. Rev.* 50. <https://doi.org/10.1016/j.esr.2023.101242>.
- Li, H., Liu, P., Guo, S., Ming, B., Cheng, L., Yang, Z., 2019. Long-term complementary operation of a large-scale hydro-photovoltaic hybrid power plant using explicit stochastic optimization. *Appl. Energy* 238, 863–875. <https://doi.org/10.1016/j.apenergy.2019.01.111>.
- Li, J., Luo, G., Hu, W., Chen, S., Liu, X., Gao, L., 2022. A SVM-based implicit stochastic joint scheduling method for ‘wind-photovoltaic-cascaded hydropower stations’ systems. *Energy Rep.* 8, 811–823. <https://doi.org/10.1016/j.egyr.2022.10.273>.
- Li, Y., Ming, B., Huang, Q., Wang, Y., Liu, P., Guo, P., 2022. Identifying effective operating rules for large hydro-solar-wind hybrid systems based on an implicit stochastic optimization framework. *Energy* 245. <https://doi.org/10.1016/j.energy.2022.123260>.
- Liu, D., Konapala, G., Painter, S.L., Kao, S.-C., Gangrade, S., 2021. Streamflow simulation in data-scarce basins using Bayesian and physics-informed machine learning models. *J. Hydrometeorol.* <https://doi.org/10.1175/jhm-d-20-0082.1>.
- Liu, N., Wang, G., Su, C., Ren, Z., Peng, X., Sui, Q., 2024. Medium- and long-term interval optimal scheduling of cascade hydropower-photovoltaic complementary systems considering multiple uncertainties. *Appl. Energy* 353. <https://doi.org/10.1016/j.apenergy.2023.122085>.
- Ma, L., Liu, Y., Zhang, X., Ye, Y., Yin, G., Johnson, B.A., 2019. Deep learning in remote sensing applications: a meta-analysis and review. *ISPRS J. Photogramm. Remote Sens.* 152, 166–177. <https://doi.org/10.1016/j.isprsjprs.2019.04.015>.
- Nearing, G.S., Kratzert, F., Sampson, A.K., Pelissier, C.S., Klotz, D., Frame, J.M., et al., 2021. What role does hydrological science play in the age of machine learning? *Water Resour. Res.* 57. <https://doi.org/10.1029/2020wr028091>.
- Peng, S., Jiang, H., Wang, H., Alwageed, H., Zhou, Y., Sebdani, M.M., et al., 2019. Modulation classification based on signal constellation diagrams and deep learning. *IEEE Trans. Neural Netw. Learn. Syst.* 30, 718–727. <https://doi.org/10.1109/TNNLS.2018.2850703>.
- Shahid, F., Mehmood, A., Khan, R., Al Smadi, A., Yaquib, M., Alsmadi, M.K., et al., 2023. 1D Convolutional LSTM-based wind power prediction integrated with PkNN data imputation technique. *J. King Saud Univ. - Comput. Inf. Sci.* 35. <https://doi.org/10.1016/j.jksuci.2023.101816>.
- Shi, Y., Wang, H., Li, C., Negnevitsky, M., Wang, X., 2024. Stochastic optimization of system configurations and operation of hybrid cascade hydro-wind-photovoltaic with battery for uncertain medium- and long-term load growth. *Appl. Energy* 364. <https://doi.org/10.1016/j.apenergy.2024.123127>.
- Tavakoli, A., Karimi, A., 2022. Development of Monte-Carlo-based stochastic scenarios to improve uncertainty modelling for optimal energy management of a renewable

- energy hub. IET Renew. Power Gener. 17, 1139–1164. <https://doi.org/10.1049/rpg2.12671>.
- Wang, Y., Zhang, L., Erichson, N.B., Yang, T., 2025. Investigating the streamflow simulation capability of a new mass-conserving long short-term memory (MC-LSTM) model across the contiguous United States. J. Hydrol. 658. <https://doi.org/10.1016/j.jhydrol.2025.133161>.
- Wang, J., Zhao, Z., Zhou, J., Cheng, C., Su, H., 2024. Co-optimization for day-ahead scheduling and flexibility response mode of a hydro–wind–solar hybrid system considering forecast uncertainty of variable renewable energy. Energy 311. <https://doi.org/10.1016/j.energy.2024.133379>.
- Xu, B., Zhu, F., Zhong, P.-a., Chen, J., Liu, W., Ma, Y., et al., 2019. Identifying long-term effects of using hydropower to complement wind power uncertainty through stochastic programming. Appl. Energy 253. <https://doi.org/10.1016/j.apenergy.2019.113535>.
- Xu, B., Huang, X., Zhong, P.-a., Wu, Y., 2020. Two-phase risk hedging rules for informing conservation of flood resources in reservoir operation considering inflow forecast uncertainty. Water Resour. Manag. 34, 2731–2752. <https://doi.org/10.1007/s11269-020-02571-y>.
- Yang, Z., Liu, P., Cheng, L., Wang, H., Ming, B., Gong, W., 2018. Deriving operating rules for a large-scale hydro-photovoltaic power system using implicit stochastic optimization. J. Clean. Prod. 195, 562–572. <https://doi.org/10.1016/j.jclepro.2018.05.154>.
- Yun, P., Fu, H., Zhang, H., Sun, J., Zhao, M., Xie, J., 2025. Rapid design of high-end copper alloy processes combining orthogonal experiments, machine learning, and Pareto analysis. J. Mater. Res. Technol. 36, 1005–1016. <https://doi.org/10.1016/j.jmrt.2025.03.119>.
- Zhang, Y., Bai, P., Li, Z., Zhang, J., 2025. Rapid optimization of iron-based alloy laser cladding process based on orthogonal experiment and machine learning for Q345. Opt. Laser Technol. 182. <https://doi.org/10.1016/j.optlastec.2024.112086>.
- Zhang, Z., Dai, H., Jiang, D., Yu, Y., 2025. Multi-objective operation rule optimization of wind-solar-hydro hybrid power system based on knowledge graph structure. J. Clean. Prod. 486. <https://doi.org/10.1016/j.jclepro.2024.144514>.
- Zheng, Y., Liu, P., Cheng, L., Xie, K., Lou, W., Li, X., et al., 2022. Extracting operation behaviors of cascade reservoirs using physics-guided long-short term memory networks. J. Hydrol.: Reg. Stud. 40. <https://doi.org/10.1016/j.ejrh.2022.101034>.
- Zhu, L., Xu, B., Wang, X., Yue, H., Mo, R., Wang, S., et al., 2025. Stochastic simulation framework for renewable power output: integrating hybrid discrete-continuous distributions with vine copula function. Renew. Energy 251. <https://doi.org/10.1016/j.renene.2025.123444>.
- Zhu, F., Zhong, P.-a., Xu, B., Liu, W., Wang, W., Sun, Y., et al., 2020. Short-term stochastic optimization of a hydro-wind-photovoltaic hybrid system under multiple uncertainties. Energ. Conver. Manage. 214. <https://doi.org/10.1016/j.enconman.2020.112902>.