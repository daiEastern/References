A hybrid model with a physics-constrained neural network to improve hydrodynamic prediction

Authors: Wangjiayi Liu^a, Guanghua Guan^{a,*}, Xin Tian^b, Xiaonan Chen^c, Liangsheng Shi^a, Guangtao Fu^d

Affiliations:
^a State Key Laboratory of Water Resources Engineering and Management, Wuhan University, Wuhan, 430072, China
^b KWR Water Research Institute, Groningenhaven 7, Nieuwegein, 3443PE, Netherlands
^c Construction and Administration Bureau of the Middle-Route of the South-to-North Water Division Project of China, Beijing, 100038, China
^d Centre for Water Systems, University of Exeter, Exeter, EX4 4QF, UK

Journal: Environmental Modelling and Software, Volume 194, 2025, 106699
DOI: https://doi.org/10.1016/j.envsoft.2025.106699

Abstract

Accurate hydrodynamic prediction is vital for water transfer systems to ensure delivery efficiency and prevent damage. Traditional physics-based models use predefined or estimated offtake discharges as lateral boundaries, neglecting interactions between real-time hydraulic states and future offtake discharge, then causing water level predictive errors. To address this, we propose a hybrid model with a physics-constrained neural network (PcNN) for real-time offtake discharge prediction. The PcNN employs long short-term memory (LSTM), incorporating physical constraints into the input layer and loss function from prior knowledge and a hydrodynamic model. Applied to a large-scale water transfer system in China, the hybrid model improves offtake discharge prediction by 30%–70% over the baseline and boosts water level forecasting, with Nash-Sutcliffe efficiency coefficients reaching 0.84 and 0.92 in upstream and downstream sections. The results demonstrate its effectiveness in integrating system hydrodynamics with data patterns, offering a robust tool for real-time decision support in water resource management.

Keywords: Hybrid modelling, Physics-constrained neural network, Hydrodynamic model, Canal system, LSTM

Introduction

Large-scale inter-basin water transfer facilitated by canal systems plays a critical role in water resource management at both spatial and temporal scales, as it alters regional hydrological processes, surface-groundwater interactions, and ecosystem dynamics (Zhang et al., 2020; Dong et al., 2023). Within canal systems, hydraulic variables, including water levels and discharges, serve as indicators of the available water supply and the risk of system instability (Henonin et al., 2013). Therefore, real-time and high-fidelity predictions from hydrodynamic models are essential for understanding water transfer processes and supporting adaptive water management strategies (Khan and Ghumman, 2008; Fan et al., 2023). As a lateral boundary condition of canal models, water offtake discharge at each offtake gate is necessary to solve hydrodynamic processes (Suresh and Sridharan, 2021).

Conventionally, physics-based hydrodynamic models have been developed and employed to simulate the flow process. For water systems with large-scale longitudinal length and negligible lateral distance, a one-dimensional (1D) model is commonly used to simulate dynamic water levels and discharges in pipe systems, open channels and rivers (Mark et al., 2004; Keylock et al., 2012). Furthermore, various simplified models aim to provide higher accuracy at a lower computational cost for real-time prediction (Achim et al., 2021; Yu et al., 2022). In hydrodynamic models, lateral offtake discharges in the next time step are typically based on assumptions, scheduled plans, or rough estimations (Dejean et al., 2014; Fan et al., 2023). Nevertheless, these values deviate from reality, as offtake discharge through a sluice gate depends not only on pre-set gate operations but also on real-time hydraulic states in canals, i.e., water levels and flow discharges (Shahrokhnia et al., 2008). These variables reflect real-time states of water flow, further affecting the hydraulic conditions at the offtake. Their influence induces complex and nonlinear responses that static equations or empirical formulas may not fully capture. Hence, physics-based models fail to accurately describe hydrodynamic relationships governing offtake discharges in real systems, posing a barrier to precise real-time prediction.

The rapid development of machine learning algorithms provides a promising pathway, with growing applications in enhancing hydrodynamic prediction (Zounemat-Kermani et al., 2019; Chen et al., 2024). Among many machine learning methods, recurrent neural networks (RNN) such as long short-term memory (LSTM) networks proposed by Hochreiter and Schmidhuber (1997) have been widely used for time series prediction problems. Previous studies have demonstrated the effectiveness of LSTM models in rainfall-runoff modelling, achieving satisfactory predictions with large datasets (Kratzert et al. 2018, 2019; Xiang et al., 2020). While these applications focused on the long-term dependencies, some studies have also applied LSTM in real-time scenarios, including daily reservoir inflow forecasting (Qi et al., 2019), real-time water level prediction in open channels (Ye et al., 2022) and real-time control in urban drainage systems (Pei et al., 2025). These applications also support the capacity of LSTM for modeling low-frequency yet complex hydraulic dynamics. In addition, machine learning models are employed to simulate complex spatiotemporal hydrodynamics. Machine learning algorithms have enabled accurate modelling of surface water variations (Tariq and Qin, 2023) and nonlinear wave dynamics (Wedler et al., 2023). Graph neural networks (GNNs) can efficiently forecast the streamflow by aggregating spatio-temporal information (Sun et al., 2021). While data-driven models show efficiency in hydrodynamic prediction, their promising performance heavily relies on large datasets for training, which are often unavailable in large-scale water systems. Moreover, the absence of underlying physical processes limits their explainability and generalizability under varying operational conditions.

Given these challenges, there is an urgent need for modeling approaches that incorporate both physical insights and data-driven learning, reducing the dependency on datasets while providing more reliable and robust predictions. Therefore, hybrid physics and data-driven models integrating mechanism processes and machine learning have been proposed for hydrodynamic simulation (Reichstein et al., 2019). Some studies utilized data-driven solvers to uncover and compensate for errors and uncertainty within numerical models (Blakseth et al., 2022; Liu et al., 2022), with similar practices in turbulence flow modelling (Duraisamy et al., 2019) and streamflow prediction (Cho and Kim, 2022). To support the calculation based on physical equations, data-driven models optimize model configurations (Chadalawada et al., 2020) and generate boundary conditions at unmeasured locations (Huang et al. 2022, 2023). In addition, other hybrid modelling methods enhance prediction by integrating outputs using a weighting technique (Xiang et al., 2021), mutual data supplementation (Li et al., 2023), and hybrid differential equations (Quaghebeur et al., 2022).

Furthermore, introducing physical knowledge into neural networks is an efficient approach to enhance prediction accuracy and model interpretability under limited datasets, mainly including physics-informed neural networks (PINN) and neural networks with physical constraints. On the one hand, the PINN proposed by Raissi et al. (2019) incorporates physical terms into the loss function, enabling the prediction of nonlinear dynamics from incomplete models and sparse data (Karniadakis et al., 2021). The physical terms cover the explicit physical differential equations, initial and boundary conditions (Lan et al., 2023), enabling mesh-free neural networks to solve complex equations more accurately. In the hydrodynamics field, the PINN has been applied in groundwater flow (Zhang et al., 2022), irrigated watersheds (Li et al., 2022) and pipeline systems (Ye et al., 2022). On the other hand, added physical constraints in neural networks act on the mapping features (Chen and Zhang, 2020), network structure (Hu et al., 2023) and the training target (Song et al., 2024) using known physical laws. To optimize the data-driven model architecture, hidden layers equivalent to an engineering system are conducted and encoded (Darbon and Meng, 2021).

Despite existing hybrid and physics-informed models having advanced hydrodynamic predictions, most approaches rely on well-defined governing equations, static model corrections or empirical constraints. They are inadequate for capturing the real-time relationship between current hydraulic states and future offtake discharges, limiting their capacity in canal dynamics. To fulfill the needs, this study proposes a hybrid model with a novel physics-constrained neural network (PcNN) to support real-time offtake discharge prediction for canal systems. This hybrid model combines a PcNN using the LSTM model with a 1D hydrodynamic model. Compared to PINNs, the proposed PcNN is more flexible and better suited for offtake discharge prediction, as it embeds constraints from physical knowledge and simulations without requiring complete differential equations. The hybrid model is validated on a large-scale water transfer system using real-world datasets, demonstrating enhanced prediction performance.

Methodology

2.1. Baseline model driven by regulated boundary conditions

This study focuses on canal systems that often consist of an open channel, one or multiple control gate(s), and water offtakes (including gates, valves, and weirs). In many canal systems, water level and flow sensors are installed at several observation locations along the channel (Fig. 1). The main hydrodynamic process of a traditional physical model is conventionally driven by a one-dimensional dynamic equation with unsteady discharges through the upstream control gate (Q_u) and/or downstream control gate (Q_d), and offtakes (q) (Clemmens et al., 1998).

In real-world canal systems, water is mostly diverted at the offtake gate located near the downstream end, to minimize the influence of the water level fluctuation caused by the withdrawn water (Hassani and Hashemy Shahdany, 2021). In practice, Q_u and Q_d are often scheduled in advance, especially for irrigation or flood defense purposes, without considering the variation in the unpredicted boundary condition (i.e. q). Therefore, the baseline model is formulated using a mass-balance assumption, with q defined as the difference in discharge between the upstream and downstream sections of the offtake (Islam et al., 2008). To make the calculation feasible, the baseline model adopts the following two assumptions, given the offtake located near the downstream end of the canal:
The downstream section discharge of the offtake is adopted as the planned outflow through the downstream control gate (Q_d).
The upstream section discharge of the offtake equals the planned upstream inflow (Q_u) considering the delay time of water flow.

Therefore, the baseline model can be expressed as Eq. (1), and the calculation of delay time step t_d in Eq. (1) refers to Litrico and Fromion (2004):

q_{t+1} = Q_{u}^{t+1-t_d} - Q_{d}^{t+1} quad (1)

where t is the time step; (t+1) indicates the next time step requiring prediction; t_d is the delay time step of water flow from the upstream end to the downstream end.

Such an assumption of q considers the real-time scheduling plans and the travel time from the upstream gate to the offtake location. However, it overlooks the influence of real-time hydraulic states, leading to cumulative numeric water level deviation caused by the biased prediction of q.

2.2. Hybrid hydrodynamic data-driven model

To improve model prediction for canal systems, this study proposes a hybrid model combining a physics-based hydrodynamic model with a data-driven PcNN (Fig. 2, details in Sections 2.2.1 and 2.2.2). Specifically, the physics-based model generates system states to guide the training process of the PcNN, and the latter maps the observed and planned hydraulic variables (H and Q) to the future offtake discharge (q).

2.2.1. Physics-based hydrodynamic model

Given that the 1D Saint-Venant Equations (SVEs) are widely used to describe unsteady gradient hydrodynamics in open channels (Cunge et al., 1980; Litrico and Fromion, 2004), this study adopts the discrete SVEs solved by the four-point Preissmann scheme (Szymkiewicz, 1996). The hydrodynamic simulation is conducted using the unsteady solution of the 1D SVEs with transient terms retained. Dynamic boundary conditions are scheduled discharges through the upstream and downstream control gates (Q_u and Q_d), and the initial condition is the observed downstream water level (H_d).

Different from the baseline model, an optimization problem is formulated in the hybrid model to find an optimal q (noted as q_{opt}), by minimizing the gap between the observed water levels and simulated water levels. This optimization is solved at each time step.
A hydraulic model driven by SVEs is first run with a rough scheduling plan, i.e. Q_u, Q_d and q_{init} (q_{init} = Q_u - Q_d), to simulate water levels along the canal H_i, including downstream water levels H_d. The simulated H_d deviates from the observed H_d due to the assumed q_{init}.
An optimization problem is formulated to minimize the absolute value difference between simulated H_d and observed H_d, using q as the argument.
The optimization process iterates until the threshold varepsilon (varepsilon < 10^{-3} m) is reached, yielding the optimized offtake discharge q_{opt}.

After that, the water levels (H_i) and discharges (Q_i) at unmeasured sections can be re-simulated based on q_{opt}. Note that q_{opt} is an inverted value derived from a real scenario instead of a predicted value. It serves only as the training target and a benchmark for comparison with predictions of the data-driven model.

2.2.2. Data-driven model

The data-driven model in this study adopts a neural network with one input layer, two hidden layers, and one output layer. Multiple neurons in each layer are interconnected through pre-defined functions and dynamically computed weights to learn input-output relationships. Depending on whether inputs and the training process are constrained by physics-based hydrodynamic conditions, an unconstrained neural network (UncNN) and a PcNN are developed and compared.

(1) Unconstrained neural network

As a pure data-driven model, the UncNN model considers the following variables in the input layer: Q_u, Q_d, H_d, Delta H_u, Delta H_d, and the final layer only contains one variable (q).

We first add no physical constraints, as the UncNN. At each time step t, the input vector of the UncNN (noted as X_t^{UncNN}) contains all selected characteristic inputs at the t and (t+1) time steps, which are shown in Eq. (2):

X_t^{UncNN} = { Delta H_u^t, Delta H_d^t, H_d^t, Q_u^{t+1}, Q_d^{t+1} } quad (2)

where H_d^t indicates the water depth of the downstream end in m; Delta H_u^t and Delta H_d^t respectively indicate the changes of upstream and downstream water levels in m; Q_u^{t+1} and Q_d^{t+1} indicate the discharge plans through the upstream and downstream control gates at the (t+1) time step in m^3/s.

Next, two hidden layers are set to employ a long short-term memory (LSTM) model. The architecture and theory of the LSTM are briefly introduced in Appendix A. Training errors guide the parameters update iteratively to adjust the data-driven model. The parameters can be optimized by minimizing the following loss function, in terms of the mean squared error (MSE):

Loss_{Data} = frac{1}{N_d} sum_{j=1}^{N_d} (q_j^{sim} - q_j^{tru})^2 quad (3)

where N_d is the total number of training data in the neural network; q_j^{sim} indicates the j-th simulated q value of the trained model; q_j^{tru} indicates the j-th true value of the target q.

In our proposed model, the length of the historical time series data considered in the LSTM layers is denoted as T, implying that T+1 vectors (X_{t-T}, ..., X_t) are used as the input to predict q at t+1 time step (i.e. q_{t+1}). To train a neural network with LSTM layers, the numbers of epochs, neurons in each hidden layer, the learning rate, and the batch size need to be considered (Kratzert et al., 2019).

(2) Physics-constrained neural network

With most layers unchanged, the hybrid PcNN adds a layer between the input and hidden layers, reflecting prior hydraulic knowledge. Additionally, a physical loss term generated from the physics-based model is added to the loss function. In the proposed PcNN, physical constraints are incorporated into both the added layer and the loss function to produce q predictions that better align with physical laws, as illustrated in Fig. 3 and detailed below.

Added layer driven by physical constraints:

    An additional layer connects the input layer to the LSTM layer, incorporating a nonlinear combination and two auto-encoders. First, we add H_d Delta H_d as a neuron in this added layer, considering its representation of the hydraulic condition near the downstream end. Then, to reduce potential input redundancy and enhance the representation of underlying hydraulic patterns, unsupervised learning is developed to extract features from the original inputs (Suryawati et al., 2021). This study assumes that inputs with similar physical characteristics should be grouped and processed through an encoding part of an unsupervised network using an AutoEncoder. In the first unsupervised network, Delta H_u and Delta H_d are clustered to describe the change in water levels of the canal, and the extracted feature is noted as S_1. Meanwhile, Q_u and Q_d are encoded to represent the scheduling plans in the second unsupervised network, and the extracted feature is noted as S_2. These extracted features are passed to the LSTM with minimal added computation, improving the model's ability to capture nonlinear interactions among related inputs.

    In the added layer, the input vector of PcNN at the t time step (noted as X_t^{PcNN}) has been modified as Eq. (4) and Eq. (5):

    X_t^{PcNN} = { S_1^t, S_2^t, H_d^t, (H_d Delta H_d)^t } quad (4)

    begin{bmatrix} S_1^t \ S_2^t end{bmatrix} = begin{bmatrix} g_1(omega_1(Delta H_u^t, Delta H_d^t)) + beta_1 \ g_2(omega_2(Q_u^{t+1}, Q_d^{t+1})) + beta_2 end{bmatrix} quad (5)

    where S_1^t and S_2^t are the extracted feature values of the two unsupervised networks, respectively; omega_1, omega_2, beta_1 and beta_2 are the weights and biases of the two unsupervised network, respectively; g_1(cdot) and g_2(cdot) indicate the functions of the 1st and 2nd unsupervised network, respectively.

Loss function with physical constraints:

    Following a mass balance principle, the predicted q from the PcNN model is supposed to be equal to the deviation between the inflow (Q_{in}) and the outflow (Q_{out}) within the same calculation grid involving the offtake, which forms an additional loss function in the last layer of the PcNN (see Eq. (6) and Eq. (7)).

    Loss_{Physics} = frac{1}{N_d} sum_{j=1}^{N_d} (q_j^{sim} - (Q_j^{in} - Q_j^{out}))^2 quad (6)

    Loss = (1 - alpha) Loss_{Data} + alpha Loss_{Physics} quad (7)

    where alpha is the weight to balance the physics loss term and the data loss term. This loss function comprises the sum of data loss and physics loss, both of comparable magnitude, so alpha is set as 0.5 in this paper.

2.3. Evaluation metrics

The baseline model (Model 1), the UncNN model (Model 2), and the hybrid PcNN model (Model 3) are evaluated based on predictions of q and H_i, using the mean absolute error (MAE), the root mean square error (RMSE), the Nash-Sutcliffe efficiency coefficient (NSE) and the percent bias (PBIAS). MAE and RMSE measure the average absolute and squared errors between predictions and observations, respectively; NSE evaluates the predictive accuracy, with values closer to 1 indicating better performance; PBIAS measures the average bias of predictions, with positive values indicating underestimation and negative values indicating overestimation. Those four metrics are calculated over the results at all timesteps, which are shown as Eq. (8)–(11), respectively:

MAE = frac{1}{N_p} sum_{t=1}^{N_p} |Y_t^{tru} - Y_t^{pre}| quad (8)

RMSE = sqrt{frac{1}{N_p} sum_{t=1}^{N_p} (Y_t^{tru} - Y_t^{pre})^2} quad (9)

NSE = 1 - frac{sum_{t=1}^{N_p} (Y_t^{tru} - Y_t^{pre})^2}{sum_{t=1}^{N_p} (Y_t^{tru} - overline{Y^{tru}})^2} quad (10)

PBIAS = sum_{t=1}^{N_p} frac{Y_t^{pre} - Y_t^{tru}}{Y_t^{tru}} times 100 quad (11)

where N_p is the total number of data points, Y^{tru} and Y^{pre} indicate the observation and prediction of a predicted variable; overline{Y^{tru}} is the mean value of Y^{tru}. These four metrics are calculated for both q and H_i.

Case Study

3.1. Study area and field data

In this paper, two canal reaches with different scales of water offtake discharge are selected as study cases. They belong to the Beijing–Shijiazhuang (BS) section of the Middle Route of the South-to-North Water Diversion Project in China, and the location and schematic diagram of the reaches are shown in Fig. 4. The dataset comprises 9 consecutive days of water level observations and discharge plans under normal operation, without significant transitions or emergency scheduling. During the studying period, one reach witnessed a normal discharge (85–95 m^3/s) with a small offtake discharge (0–5 m^3/s), namely Reach A; while the other contained the diversion to Tianjin and experienced a normal discharge (78–88 m^3/s) with a large offtake discharge (30–35 m^3/s), namely Reach B. The delay time t_d in Reach A and Reach B is 40min and 20min, respectively. In addition, the study cases have the following common characteristics: (1) trapezoidal cross-sections of varying sizes, (2) offtakes near the downstream end, and (3) mild, nearly constant bottom slopes of 0.00004. Due to the limited sensors and monitoring data, this paper does not consider the impact of water loss from evaporation, leakage, or other factors on offtake discharge prediction.

3.2. LSTM setup

Given that q is primarily influenced by short-term scheduling conditions, the historical time series input in LSTM layers covers 6 time steps (2 h), i.e. T= 6. The model is trained using the adaptive moment estimation (Adam) optimizer (Chang et al., 2019) with a learning rate of 0.01, a momentum decay rate of 0.9, and an adaptive term decay rate of 0.999. Hyper-parameters in LSTM hidden layers were searched in a set range referring to previous studies (Stathakis, 2009) and determined by 6-fold cross-validation (Geisser, 1975). The set range for neurons is (12, 18, 24,... , 60) with step size equaling to 6, and it for numbers of epochs is (50, 100, 200, 400). As a result, 12 neurons are set in both LSTM layers in Reach A, and 24 neurons in Reach B. Besides, the training process employs a full batch size (216 data points) and 100 epochs. The ratio of the sample size of the training set to the test set is 75%:25% in this paper. Using a rolling horizon scheme, each training dataset spans 216 data points (72h), each validation dataset contains 36 data points (12h), and each test dataset covers 72 data points (24h). These settings apply to both UncNN and PcNN.

3.3. Simulation setup

The discrete simulation length of canal sections used in SVEs is set as 100 m. However, within 100 m upstream and downstream of the canal nodes (section size changes or offtakes), the length is reduced to 10 m, resulting in 222 and 146 calculated sections in Reaches A and B, respectively. The simulation time step of the physics-based model is set to 5 min, while the results are output every 20 min to maintain consistency with the field data collection frequency. Similarly, the prediction time step of the data-driven model is also set to 20 min. Geometric and hydraulic parameters used in the model, including section size, bottom slope and roughness, are set or calibrated from field observations to mirror real-world scenarios. All numerical experiments are carried out via Matlab R 2019b on a Windows system with an Intel Core i7-9700 3.00 GHz CPU and 16 GB of RAM.

Results

4.1. Comparison of the predicted offtake discharge

4.1.1. Effect of feature extraction using AutoEncoders

To evaluate the effect of feature extraction via autoencoders, the predictive errors using raw inputs and those using encoded features (S_1 and S_2) in the PcNN are compared. As shown in Fig. 5, the model using encoded inputs yields lower prediction errors and narrower distributions both in Reach A and Reach B. In Reach A with small offtake discharges, feature extraction notably reduces prediction errors (22.7% lower MAE). In Reach B with larger discharges, the encoded-input model yields a slightly lower MAE but a noticeably narrower error distribution. These results suggest that feature extraction enhances model robustness, especially under irregular or low-flow conditions. These results suggest that the extracted features preserve more efficient information for model training, thereby improving prediction accuracy. However, the improvement from feature extraction is limited when the baseline error is already low, as observed in Reach B.

4.1.2. Evaluation of overall prediction performance

In this section, the performances of three models (Model 1, Model 2 and Model 3) in predicting q are compared. Prediction errors in Reach A (small offtake discharge) and Reach B (large offtake discharge) are shown in Fig. 6. Compared to the baseline model (Model 1), the UncNN model (Model 2) shows increased MAE and wider error distribution in Reach A. However, the hybrid model with the proposed PcNN (Model 3) exhibits a lower MAE and a shorter box length. In contrast to Reach A, both the UncNN model and the hybrid PcNN model in Reach B show a sharp reduction in MAE and box length compared to the baseline model. This suggests that machine learning performs better under large offtake conditions. Overall, the hybrid PcNN model (Model 3) yields the smallest errors, with values concentrated below 0.5 m^3/s and the narrowest distribution among the three models. It demonstrates its superior ability to enhance data-driven model predictions.

Meanwhile, the improvement ranges of the hybrid model in terms of MAE, RMSE and NSE are demonstrated in Fig. 7. Compared to Model 1, Model 2 performs worse with negative improvement of the MAE and RMSE in Reach A, while Model 3 reduces the MAEs by 25.36% and 62.47% in Reach A and Reach B, respectively. Similarly, the improvement ranges of RMSEs using Model 3 also reach 31.37% and 67.09% in two reaches, showing a better performance in model stability. Moreover, the NSEs of Model 2 witness an obvious drop in Reach A and a smaller rise in Reach B, while there is a significant increase in the NSEs of Model 3. Using the hybrid model with the PcNN, the NSEs of Model 3 in both study cases reach 0.7, showing significant upward trends (Delta NSE = 0.348 and 0.710) compared to Model 1. As shown in Table 1, the hybrid PcNN model shows consistent improvement direction in MAE, RMSE, NSE and PBIAS, indicating the robustness of predictions. To further explain the effect of the PcNN on prediction enhancement, the importance of independent variables, extracted features and the input combination are compared in Appendix B.

In addition, the computational efficiency of the UncNN and the PcNN is also assessed. In both Reach A and Reach B, the average training time per prediction window is about 4s for the UncNN and 5s for the PcNN. While physical constraints introduce a slight increase in training time, the overall overhead is minimal. Both models maintain high efficiency in practical applications, and the inference time is negligible compared to the 20-min prediction interval.

4.2. Comparison of the predicted water level

With the predicted lateral boundary condition q, the hybrid model is used to predict water levels along the canal in the next time step. In this section, the results in Reach B (large offtake discharge) are selected to be analyzed. To illustrate the model's ability in different change rates of water levels, data are grouped into three stages based on observed variation: low stage (0~0.5 cm/h), middle stage (0.5~1 cm/h) and high stage (1~3.5 cm/h). Prediction errors for all models in each stage are shown in Fig. 8. In the low stage, in which Model 3 maintains a mostly equivalent MAE but a wider box length compared with Model 2. In the middle stage, the MAEs experienced a sharp drop from 0.159m to 0.021m via the hybrid PcNN model. Furthermore, Model 2 and Model 3 outperform the baseline model in the high variation stage with lower MAEs and smaller box lengths. Notably, the prediction accuracy of Model 3 is slightly worse than Model 2 in the high-stage variation. Since water level change reflects q variation, this suggests the hybrid PcNN may be less responsive to rapid flow changes, possibly due to physical constraints limiting sensitivity to local input variations.

Limited to the observed sections, the predicted water levels at the most upstream and downstream sections are selected to be compared with observations and explain the model ability. As shown in Fig. 9, the MAE, RMSE and NSE of the baseline model are all improved with different ranges by the UncNN and the hybrid PcNN. Model 3 performs better than Model 2 with larger improvement ranges, explaining the promotion of physical constraints on data-driven model prediction. Compared to Model 1, Model 3 improves the MAEs by 59.66% and 76.16% in the upstream and downstream sections, respectively. It also shows a similar reduction range in RMSEs, of which NSEs increase significantly to 0.84 and 0.92 for upstream and downstream water levels, respectively. As shown in Table 1, the PBIAS values decrease from −20.28% to 1.29% in the upstream section, and from −41.06% to −0.44% in the downstream section. Across all evaluation metrics, the downstream section exhibits greater improvements compared to the upstream section.

Table 1: Summary of metrics (MAE, RMSE, NSE, and PBIAS) for offtake discharge and water level predictions.
Metric   Reach A (q)         Reach B (H, Upstream)
MAE (m^3/s)   RMSE (m^3/s)   NSE   PBIAS (%)   MAE (cm)   RMSE (cm)   NSE   PBIAS (%)

Baseline   0.53   0.72   0.31   −20.65   Baseline   4.94   6.41   −0.18   −20.28

UncNN   0.71   0.90   0.26   28.87   UncNN   2.42   2.89   0.78   1.58

Hybrid PcNN   0.39   0.49   0.70   11.85   Hybrid PcNN   1.99   2.38   0.84   1.29
Metric   Reach B (q)         Reach B (H, Downstream)
MAE (m^3/s)   RMSE (m^3/s)   NSE   PBIAS (%)   MAE (cm)   RMSE (cm)   NSE   PBIAS (%)

Baseline   0.51   0.94   0.02   33.29   Baseline   8.83   11.23   −0.44   −41.06

UncNN   0.34   0.48   0.51   12.24   UncNN   3.22   4.09   0.81   −5.94

Hybrid PcNN   0.19   0.28   0.71   −4.80   Hybrid PcNN   2.11   2.73   0.92   −0.44

Discussion

5.1. Neural networks adopted as the data-driven model

This study selected the LSTM as the data-driven time series model, in which the temporal dependency between historical water levels, discharges, and predicted lateral flows was considered. Practically, in canal systems impacted by manual operations, the long-term memory property of the LSTM may be less pronounced compared to its application in hydrological processes driven by natural conditions (Kratzert et al., 2019), as the input time series in the LSTMs only lasts 2h in this paper. Other recurrent machine learning models, such as gated recurrent unit (GRU), which offers a simpler structure and lower computational cost (Gao et al., 2020), can also be considered for real-time forecasting. However, for canal systems with nonlinear and delayed responses, LSTM models temporal dependencies more effectively than simpler recurrent networks, with acceptable computational cost.

To further discuss model selection, a GRU-based model is implemented in the PcNN for comparison, as shown in Fig. 10. The hyper-parameters of the GRU were adjusted based on the LSTM setup. For Reach A, the hyper parameters of the GRU were tuned to 18 hidden units, a learning rate of 0.005, and 150 epochs. For Reach B, the hyper-parameters were consistent with those of the LSTM. Overall, LSTM and GRU achieved comparable accuracy, but GRU showed more outliers and a wider error spread, indicating slightly weaker robustness. Training a single prediction window in Reach A took on average 5s for LSTM and 8s for GRU, with the longer time due to the increased number of epochs (100 vs. 150 epochs). In Reach B, both models were trained for 100 epochs, with LSTM requiring approximately 5s and GRU requiring 4s. Therefore, GRU exhibited an efficiency advantage over LSTM in Reach B, while training times for both models remained far below the 20-min prediction interval. Regardless of the model used, the proposed hybrid framework integrating data-driven and physics-based components remains flexible and extensible.

In this paper, the proposed PcNN explored and tested the applications of physical constraints on the input layer and the loss function. Other neural networks forced by physical process can be considered and compared in hydrodynamic prediction. For the commonly used PINN, it requires corresponding physical equations to help the data-driven model describe mechanism process in the reality (Raissi et al., 2019). Standard PINNs are unsuitable for predicting offtake discharge due to the lack of explicit governing equations linking q with hydraulic inputs. Nevertheless, the modified loss function of the PcNN is inspired by the PINN, but adopts a more flexible form of physical constraint, enhancing its applicability to canal systems. For other type of physical constraints, some studies design hidden layers to reflect engineering behaviors (Darbon and Meng, 2021; Hu et al., 2023), but such approaches need further exploration on the mechanism process between q and historical hydraulic states. Beyond canal operations, the PcNN shows potential for broader use in hydrodynamic systems where control and physical processes are coupled but not fully defined. Relevant applications include overflow prediction in urban drainage, real-time flow forecasting in flood routing, and reservoir scheduling under hydraulic and demand constraints. Applying the PcNN to these domains requires adaptation to system-specific inputs and prior knowledge.

5.2. Limitations and future work of the hybrid model

One of the limitations is that the assumption of the location of the offtakes (near the downstream end) in the hybrid model deviates from some real-world scenarios. The water offtakes can also be set at multiple points along the canal in real water transfer systems to meet the delivery goals (Shah et al., 2016). In such cases, upstream and downstream observations may not capture mid-reach hydraulic states. For a single distant offtake located far from observed points, simulated water levels from a hydrodynamic model can replace observed inputs without changing the PcNN structure. In the scenarios involving multiple offtakes distributed along the canal, each offtake may operate under different schedules and couple with others via the canal hydraulics. This can lead to coupling effects, where water levels reflect the combined impact of multiple offtakes, complicating the learning of individual discharge behaviors (Zhu et al., 2023). Addressing such cases may require more complex network architectures and proper physical constraints to improve model adaptation.

In addition, the PcNN exhibits diminished predictive accuracy during high water-level variation, as shown in Fig. 8. It may be attributed to the fixed weighting (alpha= 0.5) between physical constraints and data fidelity in the loss function. Future research could explore adaptive weighting strategies or attention mechanisms to improve model responsiveness to transient hydraulic dynamics (Ren et al., 2025; Yan et al., 2025). Although physical constraints partially enhance reliability by ensuring that outputs align with hydrodynamic principles, the decision-making process of neural networks remains obscure in explaining the attribution of hydraulic relationships to discharge predictions. Therefore, further efforts are needed to enhance interpretability, such as employing Shapley Additive Explanation (SHAP) (Fan et al., 2023) or exploring more transparent model architectures.

Lastly, this study only investigated deterministic model predictions with known scheduling plans. However, model prediction uncertainty may arise from various resources, including input data, parameter settings and structural simplifications (Song et al., 2011), and unpredictable water demands in canal systems (Basupi and Kapelan, 2015). To better capture potential system states and ensure operational safety, uncertainty estimation and probabilistic forecasting via Bayesian neural network (Li et al., 2021) or mixture density network (Klotz et al., 2022) can be employed and explored.

Conclusion

This study presents a novel hybrid modelling approach for hydrodynamic prediction in canal systems, integrating a 1D physics-based SVE model with a PcNN based on LSTM. The hybrid model with the PcNN efficiently predicts the dynamic lateral boundary condition (offtake discharge q) based on scheduling plans and real-time hydraulic states. By incorporating physical constraints into both the input layer and loss function, the PcNN significantly improves the performance of the data-driven model. Tested on the real case, the proposed hybrid model efficiently forecasts q values in real time, improving water level predictions.

The main conclusions are as follows:
Compared with the baseline model, the utilization of a data-driven model improves the accuracy of prediction of q with lower error distributions, especially in the large offtake condition.
The hybrid model with the proposed PcNN performs best among all analyzed models, with a 30%–70% reduction in MAEs and RMSEs of the prediction of q compared to the baseline model. Additionally, the hybrid PcNN model achieves significantly lower PBIAS, indicating it has less prediction bias.
Using the hybrid PcNN improves the water level prediction performance, with a 60%–80% improvement in MAEs and RMSEs, indicating 0.84 and 0.92 of NSEs in upstream and downstream ends, respectively. Furthermore, the proposed model performs better in the middle and high variation rates of water levels.

This study highlights the potential benefits of a hybrid model for hydrodynamic prediction and suggests that incorporating physical constraints into neural networks can significantly improve data-driven model performance. As a result, the proposed hybrid model with the PcNN presented great accuracy and adaptability, supporting daily scheduling and risk warning in canal systems. This investigation may also inspire broader research on integrating machine learning with mechanism models for better decision-making in water resource management.

CRediT Authorship Contribution Statement

Wangjiayi Liu: Writing – original draft, Visualization, Software, Methodology, Formal analysis, Conceptualization.
Guanghua Guan: Writing – review & editing, Supervision, Software, Funding acquisition, Conceptualization.
Xin Tian: Writing – review & editing, Methodology.
Xiaonan Chen: Resources, Data curation.
Liangsheng Shi: Validation, Project administration.
Guangtao Fu: Writing – review & editing, Supervision.

Software and Data Availability

Name of software: Hybrid PcNN model
Developers: Wangjiayi Liu and Guanghua Guan
Contact: liuwangjiayi@whu.edu.cn and GGH@whu.edu.cn
Data first available: March 31, 2025
Program language: MATLAB
Source code at: https://github.com/W-Liu1030/Hybrid-PcNN-model. The code is transferable to other systems with modified inputs/outputs, and scalable to larger-scale simulations with sufficient computational resources.
Documentation: Detailed documentation for application installation, testing, and deployment can be found at https://github.com/W-Liu1030/Hybrid-PcNN-model/blob/main/README.md
Data required for local installation and use of software is accessed through the cloud. See Data Availability Statement.

Software availability: The codes of the proposed hybrid PcNN model have been deposited in GitHub and are freely available via https://github.com/W-Liu1030/Hybrid-PcNN-model.

Declaration of Competing Interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

Acknowledgement

This work is funded by the National Key Research and Development Program of China [grant 2022YFC3202504], and would also need to acknowledge the Construction and Administration Bureau of the Middle-Route of the South-to-North Water Division Project of China that supported the data collection.

Appendix A. Long short-term memory network

The LSTM network has an additional cell-state structure in the hidden layer compared to the recurrent neural network, to enable to handle the problem of time dependencies. Each LSTM layer has multiple hidden units (neurons), and each neuron stores a hidden state and a cell state. In this paper, LSTM is carried out twice in two hidden layers in the forward propagation process, and the process follows Eqs. (A1) and (A2):

G = f(W_h X + b_h) quad (A1)
q = W_o G + b_o quad (A2)

where X is the input vector, G is the output of the hidden layer; f(cdot) is the activation function in LSTM layers; W_h and W_o are the weights of the hidden and output layers, and b_h and b_o are the biases of the hidden and output layers, respectively.

The hidden state is the output of a hidden unit, which the cell state contains the memory at previous time steps. Those hidden units are governed by an input gate, a forget gate, an output gate and cell candidate. The main principle of LSTM can be explained using memory cells and these nonlinear gates, as demonstrated in Eq. (A3)~(A8) and depicted in Fig. A1.

h_t = o_t odot tanh(c_t) quad (A3)
c_t = f_t odot c_{t-1} + i_t odot g_t quad (A4)
i_t = sigma(W_{input} X_t + R_{input} h_{t-1} + b_{input}) quad (A5)
f_t = sigma(W_{forget} X_t + R_{forget} h_{t-1} + b_{forget}) quad (A6)
g_t = tanh(W_{cell} X_t + R_{cell} h_{t-1} + b_{cell}) quad (A7)
o_t = sigma(W_{output} X_t + R_{output} h_{t-1} + b_{output}) quad (A8)

where h_t denotes the hidden state, and c_t denotes the cell state; i_t, f_t, g_t, o_t are the input gate, forget gate, cell candidate and output gate, respectively; W_{input}, W_{forget}, W_{cell}, W_{output} are the input weights, R_{input}, R_{forget}, R_{cell}, R_{output} are the recurrent weights, and b_{input}, b_{forget}, b_{cell}, b_{output} are the bias; odot indicates the element-wise multiplication of vectors, sigma(cdot) indicates the sigmoid function, and tanh(cdot) indicates the hyperbolic tangent function.
(Fig. A1. Schematic of the LSTM network structure)

Appendix B. Input feature importance of the PcNN

To explain the effect of physical constraints on inputs of the neural network, Fig. B1 illustrates the importance rank of input features in prediction accuracy from the hybrid model with the PcNN (Model 3). Based on the better performance of the hybrid model in Reach B (seen in Section 4.1.2), datasets under the large offtake condition (Reach B) are used in this section. The importance of one input is measured by the increased percent in the RMSEs of model predictions after removing this input. Notably, removing S_1 or S_2 means that the inputs of the 1st or 2nd unsupervised network are used in the LSTM without feature extraction.

It can be seen that the extracted feature S_1 (from Delta H_u and Delta H_d) contributes more than its original variables Delta H_u and Delta H_d, indicating a 38.64% increase in RMSEs. Similar results occur in the other extracted feature S_2 (from Q_u and Q_d), with a slighter difference between S_2 (34.13%) and its original variables Q_u (33.42%) and Q_d (33.98%). This result implies that S_1 and S_2 retain and explore more useful information contained in the original variables. Moreover, the added nonlinear combination H_d Delta H_d is ranked as the most important input in the PcNN, for which there is a 67.6% increase in RMSEs without this one.
(Fig. B1. Importance rank of input features in prediction accuracy)

Data Availability

Data will be made available on request.

References
(Note: Full reference list omitted for brevity in this summary, but includes all citations mentioned in the text such as Zhang et al., 2020; Hochreiter and Schmidhuber, 1997; Raissi et al., 2019, etc.)