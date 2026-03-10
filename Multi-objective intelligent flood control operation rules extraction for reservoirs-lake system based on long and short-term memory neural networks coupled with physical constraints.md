[MISSING_PAGE_FAIL:1]

## 1 Introduction

The joint flood-control operation of reservoirs-lake systems requires developing flood retention, storage regulation, and flood discharge plans based on real-time flood forecasts. Such joint operation is an effective measure for reducing flood disasters. Even with rapid advancements in numerical computational capability, reducing the computational difficulty of solving high-dimensional, nonlinear mathematical models for real-time flood control operation of reservoirs system and making informed and rapid flood-control decision is in need (Huang et al., 2022; Li et al., 2020; Xu et al., 2022; Yang et al., 2017). Joint flood-control operation must simultaneously ensure safety of all infrastructures and protected regions within the system, constituting a large-scale, multi-objective nonlinear optimization problem.

Multi-objective optimization models were conventionally established for tackling flood control operations (Chen et al., 2022; Lu et al., 2022; Ning et al., 2024; Wan et al., 2023; Yang et al., 2022). However, the practical application of multi-objective optimization operations remain suffers from challenges such as low computational efficiency, excessive solution alternatives, and difficulties in identifying the trade-offs between flooding and drainage objectives. Particularly under the context of frequent extreme flood events and a large number of scenarios to be considered, relying solely on optimization methods to generate operational schemes is not only time-consuming but also insufficient to support flood risk analysis and dynamic decision-making.

In practical reservoir operations, the implementation of reservoir operation generally relies on established reservoir operation rules as operational guidelines (Zheng et al., 2022). Reservoir operation rules are derived by analyzing optimal operational regulations based on optimal operation or historical operation samples, considering operational objectives and operational constraints. These rules provide guidelines to rationalize reservoir operation. Operation rules for reservoir can be classified into empirical rules (or conventional rules), optimization-based rules, and intelligent rules according to their extraction methods. Empirical operation rules mainly rely on statistical analysis on historical operation samples or designed flood scenarios. Optimization-based operation rules adopt numerical simulation and optimization algorithms to identify optimal flood-control operation patterns. However, existing studies have shown that traditional empirical rules lack optimality and have limited applicability, while rule-extraction models based on optimization approaches can generate improved operational schemes but require substantial computational time, making them unsuitable for real-time and complex flood control scenarios. Moreover, under complex physical constraints and multi-objective operation conditions, such rules often fail to effectively capture the complexity, nonlinearity, and dynamic characteristics of reservoir operations (Diao et al., 2021; Lei et al., 2018). In contrast, intelligent operation rules offer greater flexibility and are better suited to such high-dimensional, multi-objective, and dynamic conditions. Intelligent operation rules use artificial intelligence and machine learning techniques to generate operation strategies by extracting implicit functions between reservoir operation decision variables and input variables through machine learning on given samples. Niu et al. (2019) derived and compared reservoir operation rules for hydropower operations using artificial neural networks and traditional methods such as multiple linear regression. They found that artificial neural networks outperformed traditional multiple linear regression and other similar methods. Feng et al. (2023) developed an artificial intelligence approach that combines a fuzzy clustering iterative method with dual-support vector regression (DSVR) to derive reservoir operation strategies. The applicability and effectiveness of the method were evaluated through case studies of two large hydropower stations in China.

Deep learning is a branch of artificial intelligence (LeCun et al., 2015; Shen, 2018; Zhu et al., 2025), wherein the Long Short-Term Memory (LSTM) (Hochreiter and Schmidhuber, 1997) constitutes a representative model. The LSTM network incorporates unique memory cells and a forget-gate mechanism, which contribute to higher accuracy and stability in complex time-series predictions (Kratzert et al., 2019; Xu et al., 2021). Reservoir operation processes are influenced by hydrological factors such as precipitation and runoff, as well as social, economic, and ecological water uses. Traditional data mining methods often are unable to simulating under multiple influencing factors simultaneously. To contrast, LSTM is capable of effectively assimilating extensive data and capturing data characteristics, thus providing superior performance in addressing nonlinear fitting problems. Zhang et al. (2018) utilized Back-Propagation (BP) neural networks, Support Vector Regression (SVR), and Long Short-Term Memory (LSTM) models to simulate reservoir operations at various time scales. This study indicated that the LSTM model effectively reduced computational time and memory consumption, demonstrating superior performance in simulating both peak and low-flow conditions. Shi et al. (2015) proposed a convolutional LSTM model, this study extended the application of the LSTM model from one-dimensional time series to two-dimensional spatial-temporal data. Wu et al. (2024) integrated a distributed hydrological model with LSTM model based on water-use activities, and they demonstrated that the integrated model outperformed the original model in streamflow simulation, providing a new perspective for coupling distributed hydrological modeling approaches. Fan et al. (2025) developed a digital twin-based drainage pump scheduling platform that optimization through an LSTM-NSGA-III algorithm. The proposed system achieved high water level prediction accuracy and low operational error, significantly improving scheduling efficiency. Tang et al. (2022) proposed a time-series deep learning model based on wavelet transformation and long short-term memory (WT-LSTM) to enhance the extraction of reservoir scheduling rules and improve the accuracy of outflow prediction. The LSTM model has achieved considerable progress in hydrological simulation and prediction (Mo et al., 2023, 2021). However, LSTM still faces certain limitations: (1) The "black-box" characteristics of artificial intelligence models fails to directly consider the complex physical constraints involved in the real-world reservoir operations, resulting in low interpretability and applicability (Kheyruri et al., 2025; Tandon and Sen, 2025; Wang et al., 2025; Ye et al., 2024; Zhang et al., 2025); (2) Existing studies on operation rules extraction have primarily focused on single-objective situations, lacking research on multi-objective operation rules.

To address these challenges, this study proposes a multi-objective flood-control operation rule extraction method for reservoir-lake systems, which couples LSTM with physical mechanisms. The research framework consists of several key steps. First, flood samples areexpanded through stochastic flood simulation, and deterministic optimization models are employed to generate optimized flood-control operation schemes. Secondly, design the input factors and output vector for the multi-objective operation rule extraction model. At this point, borrowing the design of two-stage risk hedging model and epsilon relaxation method (Chankong and Haimes, 1983), the operation support information for the remaining future time periods is introduced into the current time period, thereby achieving physical constraints and correction of decision variables. Furthermore, a Physical Constrained Long Short-Term Memory (CP-LSTM) model is developed by integrating hydrological physical constraints--such as water balance constraints, weighted penalty on high-flow sequences, and outflow capacity constraints--into the loss function of LSTM model. In this way, physical constraints are incorporated from both the perspective of input samples and the model structure, enhancing interpretability and physical consistency of model. Finally, a comprehensive evaluation of the model's predictive performance is conducted in both solution space and objective space. Taking the Chaohu Basin in China as a case study, the proposed method is validated for its applicability and robustness in multi-objective flood control rules extraction. More importantly, the method enables the rapid generation of near-optimal strategies across large-scale scenarios, thereby overcoming the computational bottleneck of traditional deterministic optimization and providing a scientific tool for supporting real-time flood-control decision-making and sample generation in flood risk analysis.

Figure 1: The flowchart of methodology.

## 2 Methodology

Fig. 1 shows the flowchart of the proposed method, which consists of the following five steps:(1) Data processing; (2) Constructing a multi-objective flood control operation model (Section 2.1.1); (3) Designing a multi-objective operation rules framework (Section 2.1.2); (4) Building a CP-LSTM intelligent operation rules extraction model for multi-objective flood control which coupled with physical constraints (Section 2.2); (5) Analyzing the model outputs using evaluation metrics (Section 2.3).

Multi-objective problem of reservoirs-lake system flood control and multi-objective operation rules framework

The flood control system of the reservoirs-lake systems consists of reservoirs, lake, and river channels, and the system structure is generalized as follows: 1 The upstream part of system consists of several reservoirs, mainly regulating the flood in the upstream hilly area; 2 The midstream part of system includes lake and uncontrolled rivers, mainly regulating the flood in the midstream; 3 The downstream part of system is the river channel for discharging excessive floods. Fig. 2 is a schematic diagram of a typical reservoirs-lake system flood control structure. In the diagram, \(Q_{1,n}\),..., \(Q_{l,m}\),..., \(Q_{n,t}\), \(Q_{n+1,t}\) and \(QQ_{1,n}\),..., \(QQ_{1,t}\),..., \(QQ_{n,t}\), \(QQ_{n+1,t}\) represent the inflow and outflow of reservoirs \(1\)\(-\)\(n\) and lake at period \(t\), respectively (m\({}^{3}\)/s); \(U_{1,2}\),..., \(U_{i,t}\),..., \(U_{n,t}\), \(U_{n+1,t}\) is the lateral inflow of reservoirs \(1\)\(-\)\(n\) and lake at period \(t\) (m\({}^{3}\)/s); \(V_{1,n}\),..., \(V_{n,t}\), \(V_{n+1,t}\) is the storage of reservoirs \(1\)\(-\)\(n\) and lake at period \(t\) (m\({}^{3}\)); \(Z_{t}\) is the water level of the river at period \(t\) (m).

#### 2.1.1 Multi-objective optimization and generation of non-inferior solutions set

Multi-objective flood control operation to coordinating flood storage and discharge strategies over reservoirs in upstream, lake in midstream, and flood conveyance in downstream rivers. The goal is to simultaneously ensure the overall flood safety of reservoirs, lake, and critical flood control points. Accordingly, the objective functions are defined as follows:

1. Minimize reservoir storage utilization rate: \[\min F_{1}=\sum_{t=1}^{n}\big{[}\big{(}V_{t,obs}-V_{t,max}\big{)}\big{/} \big{(}V_{t,obs}-V_{t,max}\big{)}\big{]}\] (1) where \(V_{t,obs}\) is the storage capacity corresponding to the design water level of reservoir \(i\) (m\({}^{3}\)); \(V_{t,max}\) is the maximum storage capacity during the operation horizon of reservoir \(i\) (m\({}^{3}\)); \(V_{t,min}\) is the storage capacity corresponding to the flood control limit water level of reservoir \(i\) (m\({}^{3}\)); \(n\) is the number of reservoirs. \(F_{1}\) focus the flood control safety of the reservoirs system.
2. Minimize the average excess flood volume of the system: \[\min F_{2}=\left\{\begin{array}{l}\sum_{t=0}^{t_{0}}\big{(}V_{n+1,t}-V_{n+1,obs}\big{)}\big{/}T,V_{n+1,t}>V_{n+1,obs}\\ \max V_{n+1,t},V_{n+1,t}\leq V_{n+1,obs}\end{array}\right.\] (2) where \(t_{0}\) is the starting period of \(V_{n+1,t}>V_{n+1,obs}\); \(t_{1}\) is the ending period of \(V_{n+1,t}>V_{n+1,obs}\); \(T\) is operation horizon; \(V_{n+1,obs}\) is the safe storage capacity of the lake (m\({}^{3}\)). \(F_{2}\) is designed to reduce the inundation loss caused by high lake water level and long inundation time periods.
3. Minimize maximum flows at flood control point \[\min F_{3}=\ \max\ \sum_{i=1}^{n}\big{(}qm_{i,t}+U_{i,t}\big{)}\] (3) where \(qm_{i,t}\) is the routed flow of the outflow from reservoir \(i\) to the flood control point at period \(t\) (m\({}^{3}\)/s); \(F_{3}\) is mainly designed to reduce the maximum flow or maximum water level of flood control points.

Figure 2: Schematic diagram of the reservoirs-lake system topology.

The constraints are set as water balance constraints, characteristic water level constraints, initial/boundary condition constraints for the operation horizon, outflow capacity constraints, outflow variation constraints, and non-negative variable constraints.

With physical constraints of reservoir operations considered, a multi-objective optimization model is established with the considered objectives. Using historical and design flood as input data, non-inferior solutions (Deb, 2001) set are obtained by epsilon relaxation method wherein \(F_{1}\) and \(F_{3}\) are treated as epsilon constraints while \(F_{2}\) is considered as the primary objective.

#### 2.1.2 Design of multi-objective operation rules

##### 2.1.2.1 Multi-objective operation rules formulation

Decision makers can use reservoir operation rules to guide decision-making by determining how much water to release or store during each time period, based on conditions of reservoir storage or inflow.

For the reservoirs-lake system, this study designs a multi-input, multi-output two-stage operation rules formulation, which can be expressed as follows:

\[\mathbf{Y}=f(\mathbf{X}) \tag{4}\]

where \(\mathbf{X}\) is the input factors of the operation rules; \(\mathbf{Y}\) is the output vector of the operation rules; \(f(\,\cdot\,)\) is the operation rules of system, which is extracted from the given operation samples.

##### 2.1.2.2 Selection of input factors \(X\)

The selection of input factors directly influences the rationality and physical interpretability of the operation rules. To adequately represent the hydrological conditions, system boundaries, and objective preferences of the reservoirs-lake system, it is essential to construct an input set that is both representative and physically meaningful. In this study, the selected input factors are as follows:

\[\mathbf{X}=\left\{V_{it},Q_{it},U_{it},Z_{t},V_{i,T+1},F_{1,x},F_{3,x},WU_{it}\right\} \tag{5}\]

where \(V_{i,T+1}\) is the ending storage of reservoir \(i\) (or lake) (m\({}^{3}\)); \(F_{1,x}\) and \(F_{3,x}\) are the objective values of reservoir storage utilization rate and maximum flows at flood control point, respectively, introduced via the epsilon relaxation method to reflect decision-maker preferences; \(WU_{it}\) is the remaining inflow volume from the current time to the end for the operation horizon of reservoir \(i\) (or lake), which is obtained based on flood forecasting (m\({}^{3}\)) and it is evaluated as:

\[WU_{it}=\sum_{i=k+1}^{T}Q_{it}\cdot\Delta t \tag{6}\]

and \(\Delta t\) is the duration of a time period (s).

In Eq. (5), \(V_{it}\), \(Q_{it}\), \(U_{it}\), \(Z_{t}\) and \(V_{i,T+1}\) are variables using to represent the system state; \(F_{1,x}\) and \(F_{3,x}\) are preference variables, which allow the rule to generate non-inferior solutions consistent with multi-objective decision making;

\(WU_{it}\) is an auxiliary variable that addresses temporal water balance constraints relating to future flood volume in reservoir

Figure 3: Schematic diagram of the two-stage model formulation and operation in a rolling horizon.

operation.

Under the same scenario, multiple sets of flood forecasting information were introduced by varying the value of the input factor \(W\!U_{\!L}\), so that the resulting operation schemes account for the ensemble of forecast scenarios, thereby reflecting the interval impact of forecast errors on operation analysis. Fig. 3

#### 2.1.2.3 Formulation of output vector \(Y\)

Based on the requirements of practical operation decisions, commonly used decision variables include the outflow of reservoirs and lake \(QQ_{\!U}\) in the current period \(t\). Additionally, to satisfy the water balance constraints in two-stage operation, the remaining outflow volume of reservoirs and lake \(W\!O_{\!U}\) (\(\text{m}^{3}\)) from the current time to the end of the operation horizon is incorporated into the decision variables. Therefore, the output vector constructed in this study is as follows:

\[\mathbf{Y}=\{QQ_{\!U_{\!L}},W\!O_{\!U_{\!L}}\} \tag{7}\] \[W\!O_{\!U_{\!L}}=\sum_{t=\text{h-1}}^{T}QQ_{\!U_{\!L}}\cdot \Delta t\]

### A CP-LSTM model for extracting multi-objective flood control operation rules

#### 2.2.1 Basic principles of the model

Long Short-Term Memory (LSTM) (Hochreiter and Schmidhuber, 1997) is a deep learning network model capable of effectively capturing long-term dependencies in time series, the detailed structure of the LSTM model can be found in A. In the LSTM model, each cell unit acts as a container for storing long-term information, retaining information from previous time periods until the next time period, when it is passed to other units. This design allows LSTM to capture the mapping relationships between input vector and output vector within a certain time periods. Therefore, this study selects LSTM as the base model and incorporates physical constraints involved in reservoirs-like system operation to enhance its performance.

#### 2.2.2 Construction of the CP-LSTM Model

Since the LSTM model is essentially a "black-box" model, it does not directly involve the complex physical constraints within operation of reservoirs and lake, and this could lead to deviations between the model predictions and the actual results. Therefore, to enhance the applicability and accuracy of the LSTM model in extracting operation rules, it is essential to incorporate core physical constraints of reservoirs-like operations. Specifically, operation support information reflecting water balance (see Section 2.1.1) is incorporated into the model's input vector. In addition, the loss function is integrated hydrological physical constraints--such as water balance constraints, weighted penalty on high-flow sequences, and outflow capacity constraints. By introducing penalty terms, the solution space of the LSTM model can be effectively constrained or bounded when solving real-world problems, ensuring that the rules' applicability.

The loss function of the CP-LSTM model is formulated as follows:

\[\begin{split}&\text{TotalLoss}=\alpha_{1}\text{L}_{\text{BASE}}+ \alpha_{2}\sum_{t=1}^{n}\text{L}1_{\!R_{\!t}}+\alpha_{3}\text{L}1_{\!L}\alpha_ {t}+\alpha_{4}\sum_{t=1}^{n}\text{L}2_{\!R_{\!t}}\\ &+\alpha_{5}\text{L}2_{\!L}\alpha_{t}+\alpha_{6}\sum_{t=1}^{n} \text{L}3_{\!R_{\!t}}+\alpha_{7}\text{L}3_{\!

[MISSING_PAGE_FAIL:7]

[MISSING_PAGE_FAIL:8]

\[\text{AOR}_{i}=\frac{\text{SC}_{i}}{\text{A}_{i}}\cdot 100\% \tag{15}\]

where \(F_{i}^{\prime}\) is the predicted objective value; \(F_{i}\) is the true objective value;\(\text{A}_{i}\) is the area of shape formed by the blue lines in Fig. 4, corresponding to the true objective space; and \(\text{SC}_{i}\) is the gray-shaded area in Fig. 4, which means the overlap area between the predicted and true objective spaces; (3) Mean Distance between Boundary Points (MDBP): The mean distance between the boundary points of the true objective values and the predicted objective values. This metric quantifies the average Euclidean distance between the boundary points of the true objective values and those predicted by the deep learning model. A lower MDBP value indicates that the predicted Pareto front is closer to the samples of Pareto front.

## 3 Case study

### Study area

This study takes the Chaohu Basin as the study area, which consists of reservoirs, lake, and river channels (Fig. 5). In the upstream mountainous area, three large reservoirs--Longhekou (LHK), Dongpu (DP), and Dafangying (DFY) have been constructed to effectively reduce flood peaks entering the lake by intercepting and storing floods in hilly regions. In the midstream part of system, Chaohu Lake (CH) receives flood generated from multiple tributaries within the basin, including the Nankei River and Hangbu River, and discharges flood through the Chaohu Sluice and Zhaohe Sluice. In the downstream part of system, flood discharge channels include control projects such as Yuxi Gate and Fenghuangjing Gate. Flood is finally discharged into the Yangtze River after joint operation of the systems of projects. Additionally, hydrological stations such as Sanchahe Station and Sanhe Station are also set up in the basin. The fundamental characteristic parameters of the reservoirs and the lake are presented in Appendix C.

### Data sources and sample processing

#### 3.2.1 Data sources and processing

The data used in this study were obtained from the official website of the Chaohu Management Bureau of Anhui Province ([https://chgli.hefei.gov.cn/](https://chgli.hefei.gov.cn/)) and the Digital Chaohu Platform. Historical flood processes with different return period were selected from the historical hydrological data from 2005 to 2023. Both typical historical flood processes and designed flood processes were used as input data for the multi-objective optimization operation model described in Section 2.1.1. The designed flood processes were constructed by proportionally scaling the historical flood hydrographs based on return period magnitudes, allowing for the generation of representative flood scenarios across various design conditions.

Based on the epsilon relaxation method described in Section 2.1.1, \(F_{2}\) was set as the primary goal, while the others were incorporated as epsilon constrained objectives to construct a constrained single-objective optimization problem. To solve this problem, this study employed the global solver of Lingo 17.0, a widely used commercial optimization software capable of handling large-scale nonlinear programs, solving optimized operation scheme samples for each flood event.

From the optimization results, input and output variables were extracted based on the multi-objective operation rule formulation described in Section 2.1.2. The input factors \(\mathbf{X}\) are determined as follow:

\[\mathbf{X}=\left\{V_{it},Q_{it},U_{it},Z_{Ti},V_{(iT+1)},F_{1x},F_{3x},WU_{it}\right\} \tag{16}\]

The corresponding output vector \(\mathbf{Y}\) consisted of two decision variables:

\[\mathbf{Y}=\left\{QQ_{it},WU_{it}\right\} \tag{17}\]

After extracting the required data from the optimized operation scheme set, min-max normalization was applied as a preprocessing step. The processed data were then organized into a multi-dimensional matrix (see Appendix D) with \(M\times T\) rows--where \(M\) represents the number of flood events, \(T\) is operation horizon of a flood event--and \(10\times i\) columns, corresponding to \(8\times i\) input factors and \(2\times i\) output factors. The samples represented in the multi-dimensional matrix serves as the input to the LSTM and CP-LSTM models and is utilized for models training and learning to extract physically interpretable multi-objective operation rules.

#### 3.2.2 Training and Testing Set Division

The training set consists of the optimized operation scheme samples of partial flood processes, which includes varied flood with different return periods, providing diverse samples for model training.

To evaluate the model's applicability and generalization capability, the optimized operation scheme samples of four representative historical flood events--corresponding to return periods of 10 years (Flood ID: 03/08/2018), 20 years (Flood ID: 26/06/2010), 50 years (Flood ID: 15/06/2016), and 100 years (Flood ID: 06/07/2020)--were selected as the testing set.

### Comparative experiment design

The main focus of this study is to evaluate the improvement effect of incorporating physical constraints into operation rule extraction model. To verify the effectiveness of incorporating physical constraints, comparative experiments were designed as follows:Model 1 (LSTM): The LSTM model without physical constraints was constructed for the intelligent extraction of multi-objective operation rules, serving as the benchmark model.

Model 2 (CP-LSTM): Based on the LSTM model, the physical constraints was introduced to construct the CP-LSTM model for intelligent extraction of the intelligent extraction of multi-objective operation rules, so as to evaluate the impact of the physical constraints on the performance of operation rules extraction.

Both models were developed using Python's PyTorch framework.

It is worth noting that existing literature has shown that traditional rule extraction methods have low performance in capturing the nonlinear and dynamic characteristics of systems under multi-objective constraints. In addition, previous studies have demonstrated the performance advantages of intelligent rule extraction methods based on deep learning, such as LSTM, over traditional methods. Therefore, this study focuses on comparing two intelligent models, LSTM and CP-LSTM, to evaluate the contribution of adding physical constraints to the model structure to improve model accuracy and physical interpretability, rather than revealing the performance gap that already exists between traditional and intelligent methods.

### Model structure and parameters

The model parameters were optimized using coupled sub-sample cross-validation and the Beluga Whale Optimization Algorithm (Zhu et al., 2024). The specific model structure and parameters are detailed in Appendix E.

## 4 Results analysis and discussion

### Analysis of flood control operation rules for reservoirs-lake system

To further show the results of the model-derived operation rules, the relationship among storage volume, inflow, and remaining inflow volume (represented by different return periods) was visualized under the condition that all other input variables in the input factors are fixed (see Fig. 6). Based on this simplification, a set of flood control operation rule curves was constructed for the three upstream reservoirs and the downstream lake, reflecting the outflow decisions under different inflow-storage scenarios. This operation rules diagram provides an intuitive perspective for understanding the decision approach of deep learning operation rules extraction models and to some extent validates the consistency between the rules learned by the model and the actual hydrological and physical mechanisms.

However, it should be noted that the graph only reflects the rule expression associated with a subset of input factors, while the operation rules learned by the model are determined with complex structure and multiple indices. Due to the large number of input factors and their nonlinear interactions, it is not feasible to visualize the complete mapping from all input factors to operational

Figure 6: Partial extracted Multi-objective intelligent flood control operation rules for reservoirs-lake system under varied flood volume.

[MISSING_PAGE_FAIL:11]

error distribution through physical constraints. In the DP (KL=0.056) and LHK (KL=0.282) regions, there is little difference in performance between the two models, but CP-LSTM still maintains a smaller fluctuation range and higher symmetry. In summary, the visual analysis in Fig. 7 and the quantitative evaluation of KL divergence jointly indicate that the CP-LSTM model outperforms the traditional LSTM model in both WBE and PE metrics. By introducing physical constraints, it not only improves prediction accuracy but also enhances the robustness of the model.

As illustrated in Fig. 8, the CP-LSTM model, which incorporates physical constraints, consistently exhibits lower POOC compared to the LSTM model, indicating its superior performance.

The performance of the LSTM and CP-LSTM models was analyzed in terms of prediction accuracy in the outflow processes and peak flow (Figs. 9-11). Tracking the trend of outflow, the CP-LSTM model demonstrates greater sensitivity to fluctuations in the outflow series.

Considering the simulation in peak outflow, the CP-LSTM model also demonstrates superior performance compared to the LSTM model. As shown in Fig. 9(a), the first peak flow at LHK Reservoir is 758 m\({}^{3}\) /s. The LSTM model predicts 719 m\({}^{3}\) /s (PE =-5.1 %), whereas the CP-LSTM model yields 748 m\({}^{3}\) /s (PE =1.3 %), providing a result closer to the sample value. The multi-peak processes in Fig. 10(a) also supports the observation: CP-LSTM accurately captures both the timing and magnitude of the peaks, while LSTM underestimates the second peak. A similar improvement is observed in Fig. 11(a), where the model provides a more accurate estimation of the peak flow. Moreover, in Figs. 10(b), (c), 11(a), (b), and (c), LSTM generally tends to overestimate peak flow magnitudes, whereas CP-LSTM produces predictions more consistent with the sample values. These results collectively highlight the enhanced

Figure 8: Bar chart of POOC for different models.

Figure 7: Raincloud plot of WBE and PE for different models.

[MISSING_PAGE_EMPTY:13]

By evaluating the similarity between the true objective space and predicted objective space, not only can the effectiveness of the operation rules extraction model be tested, but also the generalization ability of the model under multi-objective constraints can be measured. This analysis provides a key basis for determining whether the extracted operation rules have robustness and practical feasibility. Therefore, analyzing the predicted objective space is not only an evaluation of model accuracy, but also a necessary step to ensure the credibility, interpretability, and applicability of the proposed operation framework.

In this study, multi-objective optimization calculation was conducted for flood events of varying magnitudes. The results indicate that there are contradictory relationships between the reservoir storage utilization rate (\(F_{1}\)) and the average excess flood volume of the system (the lake's maximum storage capacity) (\(F_{2}\)), as well as between the reservoir storage utilization rate (\(F_{1}\)) and the maximum flows at flood control point (\(F_{3}\)). Specifically, in order to decrease the reservoir storage utilization rate, additional floodwater must be released downstream. This strategy inevitably increases both the maximum flows at flood control point and the average excess flood volume of the system (the lake's maximum storage capacity). Conversely, lowering the maximum flows at flood control point and the average excess flood volume of the system (the lake's maximum storage capacity) requires storing more flood in the upstream reservoirs, which increases the reservoir storage utilization rate. The optimization provides candidate solutions on the Pareto front.

The objective space prediction performance is analyzed using the OVE, AOR and MDBP metrics. According to Fig. 12, the CP-LSTM model, which incorporates physical constraints in the loss function, exhibits a lower OVE compared to the LSTM model. Among the three objectives, both the CP-LSTM and LSTM models achieve the lowest prediction error for \(F_{2}\), with a minimum OVE value of 1.1 %, followed by \(F_{3}\), while the highest prediction error occurs in \(F_{1}\). A comparison between the CP-LSTM and LSTM models shows that incorporating physical constraints into the loss function reduces in objective value prediction errors, with decreases of 0.20 %, 0.10 %, and 8.00 %, respectively.

The relatively high prediction error for \(F_{1}\) is primarily attributed to the dependence of reservoir storage utilization rate on the

Figure 11: Comparison of sampled outflow and predicted outflow for the flood event with a 20 years return period (Flood ID: 26/06/2010) in the testing set using different models.

Figure 12: Histogram of OVE of different models.

maximum storage volume during the operation period, which is strongly influenced by the reservoirs' outflow. Given that both models assign the highest weight to RMSE in the loss function, there is a tendency to overestimate low outflow values and underestimate high outflow in an effort to minimize the overall loss. This underestimation of peak outflow values subsequently affects the prediction of maximum reservoir storage, ultimately impacting the accuracy of reservoir storage utilization rate results.

Figure 13: Comparison of objective spaces for the flood event with a 100-year return period (Flood ID: 06/07/2020) in the testing set.

Fig. 13 presents a comparison of the objective values for the flood event which return periods is 100 years in the testing set, as computed by the Lingo, LSTM, and CP-LSTM models. Figs. 13(a) and 13(e) show the distribution of the Lingo optimization results and the predicted values of LSTM and CP-LSTM in three-dimensional space. It can be observed that both LSTM and CP-LSTM models generally capture the variation trends of the Lingo optimization values. However, the CP-LSTM model exhibits a higher degree of agreement with the Lingo optimization values compared to the LSTM model.

Fig. 13(b)-(d) and (f)- (h) show the projections of the objective spaces in Figs. 13(a) and 13(e), corresponding to the \(F_{1}\)-\(F_{2}\), \(F_{2}\)-\(F_{3}\), and \(F_{1}\)-\(F_{3}\)pairs, respectively. In Figs. 13(b) and 13 (b), the LSTM model achieves an AOR of 89.58 %, its prediction performance accuracy deviates significantly from the sample values in the regions wherein \(F_{1}>0.7\) and \(F_{2}>855\), as indicated by the scattered distribution of its predictions. In contrast, the CP-LSTM model's predicted values closely match with the sample values, achieving a higher area overlap rate of 91.02 %. As shown in Fig. 13 (c) and (g), the CP-LSTM model achieves an AOR that is 15.55 % higher than that of the LSTM model. Additionally, the LSTM model exhibits a systematic underestimation in the prediction of \(F_{3}\). Further analysis of Fig. 13 (d) and (h) reveals that the LSTM model's area overlap rate is below 60 %, with lower prediction performance in the lower-left and upper-right regions of the objective space. In contrast, the CP-LSTM model achieves an area overlap rate of 78.83 %, demonstrating better overall prediction accuracy relative to the sample values.

Fig. 14 illustrates the predictive performance of the two models on the objective space of small magnitude flood event. As shown in Fig. 14 (a), although the LSTM model captures the general shape of the objective space, it exhibits noticeable deviation and fails to predict the lower range of \(F_{3}\). In contrast, the predictions from the CP-LSTM model closely match the sample values generated by Lingo, demonstrating higher consistency and superior predictive accuracy. Fig. 14 (b) and (f) depict the relationship between \(F_{1}\) and \(F_{2}\). In this projection, the LSTM model yields an AOR of 0.00 %, indicating no overlap with the Lingo sample values. Conversely, the CP-LSTM model achieves an AOR of 65.95 %, aligning well with the majority of the sample. Fig. 14 (c) and (g) show the relationship between \(F_{2}\) and \(F_{3}\). The LSTM model's prediction is concentrated in the upper-right region of the sample values, with an AOR of 53.10 %. However, the CP-LSTM model attains a significantly higher AOR of 89.49 %, highlighting its advantage in capturing the objectives. Fig. 14 (d) and (h) illustrate the relationship between \(F_{1}\) and \(F_{3}\). The LSTM model fails to predict the lower ranges of both \(F_{1}\) and \(F_{3}\), resulting in an AOR of 93.00 %. In contrast, the CP-LSTM model aligns well with the Lingo results across the full range of values, achieving an AOR of 79.13 %, demonstrating a better predictive performance in the objective space.

From the above analysis, it can be seen that the LSTM model has prediction errors at the boundaries of some sample points, whereas the CP-LSTM model can better predict the sample values and reproduce the multi-objective non-inferior solution set in the objective space. These findings demonstrate that the proposed rules extraction method for multi-objective flood control operation in the reservoirs-lake system, which incorporates physical constraints, effectively improves the model's prediction accuracy.

The Mean Distance between Boundary Points (MDBP) was calculated to quantitatively assess the accuracy of the predicted objective space boundaries for both the LSTM and CP-LSTM models. The results indicate that the CP-LSTM model is significantly better than the LSTM model in capturing the true boundaries of the objective space. For the flood event with a 100 years return period (Flood ID: 06/07/2020) the MDBP of CP-LSTM is 39.23, which is much lower than the MDBP of LSTM model (77.80). Similarly, for the flood event with a 10 years return period (Flood ID: 03/08/2018), the MDBP of the CP-LSTM model is 21.50, while the MDBP of the LSTM model is 49.28. Compared to the LSTM model, the MDBP of the CP-LSTM model has been reduced by over 50 %. These results indicate that introducing physical constraints improves overall prediction accuracy.

## 5 Conclusion

This study addresses the challenges of multi-objective, high-dimensional complexity in joint flood control operation of reservoirs-lake system by proposing a multi-objective intelligent method for extracting operation rules, integrating Long Short-Term Memory (LSTM) networks with physical constraint, which objective is to achieve accurate, efficient, and interpretable extraction of multi-objective operation rules. The main contributions are summarized as follows:

1. Borrowing the design of two-stage reservoir operation model and epsilon relaxation method, operation decision variables during the remaining future periods is introduced as auxiliary variables in the input vector. This provides physical constraints and corrections to the current decision variables, enabling them to better adapt to multi-objective operation requirements.
2. Improving the loss function by introducing hydrological physical constraints, the penalty terms of water balance constraints, weighted penalty on high-flow sequences, and outflow capacity constraints are embedded into the loss function. These additions enhance the physical interpretability and practical applicability of operation rules extraction model.
3. Expending the model of operation rules extraction to multi-objective operation problems. The model's performance is evaluated in both the solution space and the objective space, with prediction accuracy of the multi-objective solution set quantified using the metrics system.

An analysis of the evaluation metrics indicates that the CP-LSTM model outperforms the LSTM model across multiple dimensions. In the solution space, the RMSE of the CP-LSTM model is decreased by 0.33 % and the NSE is increased by 1.12 %, indicating that the overall prediction accuracy of the CP-LSTM model has improved. More significantly, in terms of peak flow prediction, the PE of LHK Reservoir predicted by the CP-LSTM model is 3.8 % lower than that of the LSTM model, which effectively improves the problem of peak flow values underestimation. Additionally, the POOC is decreased by up to about 2.00 %, indicating enhanced applicability of the operation rules extraction. In the objective space, the CP-LSTM model achieves a maximum reduction of 8.00 % in OVE. The AOR of the three-dimensional objective space reaches up to 94.05 %, representing a 21.50 % improvement over the LSTM model. The MDBPof the CP-LSTM model has been reduced by over 50 % compared to the LSTM model. These results suggest that the CP-LSTM model provides higher accuracy in predicting the multi-objective solution set and is more capable of reconstructing the Pareto front.

The multi-objective intelligent method for extracting operation rules, integrating Long Short-Term Memory (LSTM) networks with physical constraints improves the drawback of lacking physical mechanism of LSTM models and enhances model performance. By

Figure 14: Comparison of objective spaces for the flood event with a 10-year return period (Flood ID: 03/08/2018) in the testing set.

[MISSING_PAGE_FAIL:18]

## Appendix B : Equations for Penalty terms

### Penalty terms for violating water balance constraints

\(L1_{R,i}\) and \(L1_{labx}\) are used to verify the water balance during the time period by calculating the difference between inflow and outflow as well as the variation in reservoir and lake storage. The expressions are as follows:

\[\begin{split} L1_{R,i}=\sqrt{\frac{1}{S}\sum_{t=1}^{S}\left( \left(Q_{it}-QQ_{i,t}^{*}\right)\cdot\Delta t+\left(WU_{it}-WO_{it}^{*}\right) -\left(V_{i,T+1}-V_{it}\right)\right)^{2}}\\ L1_{labx}=\sqrt{\frac{1}{S}\sum_{t=1}^{S}\left(\left(Q_{o+1,t}^{ *}-QQ_{o+1,t}^{*}\right)\cdot\Delta t+\left(WU_{n+1,t}-W0_{o+1,t}^{*}\right)- \left(V_{n+1,T+1}-V_{n+1,t}\right)\right)^{2}}\end{split} \tag{24}\]

Where \(S\) is the length of time series in the training set; \(QQ_{it}^{*}\) and \(QQ_{o+1,t}^{*}\) are the predicted outflow of reservoir \(i\) and the lake at period \(t\), respectively (m\({}^{2}\)/s); \(\Delta t\) is the duration of a time period (s); \(Q_{o+1,t}^{*}\) is the predicted inflow of the lake at period \(t\) (m\({}^{2}\)/s); \(WO_{it}^{*}\) and \(WO_{o+1,t}^{*}\) are the predicted remaining outflow volume from the current time to the end of the operation horizon for reservoir \(i\) and the lake, respectively (m\({}^{2}\)) ; \(V_{i,T+1}\) and \(V_{n+1,T+1}\) are the ending storage for reservoir \(i\) and the lake, respectively (m\({}^{2}\)).

### Weighted penalty on high-flow sequences

In general, training models with the objective of minimizing the root mean square error (RMSE) tends to underestimate high flow results and overestimate low flow results. However, high flow (i.e., flood peaks) results are typically the primary focus during flood control operations. To improve the model's accuracy in capturing high flow samples, a variable weight is assigned to the prediction error in the loss function, thereby increasing the penalty for errors during high-flow periods. The expressions for the high-flow weights penalty terms \(L2_{R,i}\) and \(L2_{labx}\) are as follows:

\[\begin{split} L2_{R,i}=\sqrt{\frac{1}{S}\sum_{t=1}^{S}\left( \frac{QQ_{it}}{qw_{i}}\left(QQ_{t,t}-QQ_{i,t}^{*}\right)\right)^{2}}\\ L2_{labx}=\sqrt{\frac{1}{S}\sum_{t=1}^{S}\left(\frac{QQ_{n+1,t} }{qx}\left(QQ_{o+1,t}-QQ_{o+1,t}^{*}\right)\right)^{2}}\end{split} \tag{25}\]

where \(QQ_{it}\) and \(QQ_{o+1,t}\) are the sample outflow for reservoir \(i\) and the lake at period \(t\), respectively (m\({}^{3}\)/s); \(qw_{i}\) is the maximum value of \(QQ_{it}\) for all time periods (m\({}^{3}\)/s); and \(qx\) is the maximum value of \(QQ_{n+1,t}\) for all time periods (m\({}^{3}\)/s).

### Penalty terms for violating outflow capacity constraints

The penalty terms expression for violating the outflow capacity constraints is expressed as follows:

\[\begin{split} L3_{R,i}=\frac{1}{S}\sum_{t=1}^{S}\max\left\{0, \left(QQ_{it}^{*}-QQ_{it}\right)\right\}^{2}\\ L3_{labx}=\frac{1}{S}\sum_{t=1}^{S}\max\left\{0,\left(QQ_{o+1,t} ^{*}-QQ_{t}\right)\right\}^{2}\end{split} \tag{26}\]

where \(Q_{it}\) is the outflow capacity of reservoir \(i\) at period \(t\) (m\({}^{2}\)/s); and \(Qb_{t}\) is the outflow capacity of the lake at period \(t\) (m\({}^{3}\)/s).

## Appendix C

\begin{table}
\begin{tabular}{l l l l l l l l} \hline Reservoirs/ & Dead Storage & Normal Water & Flood Limited & Flood Control High & Design Flood & Check Flood & Flood Control \\ Lake & Level (m) & Level (m) & Water (m) & Water Level (m) & Level (m) & Level (m) & Capacity (10\({}^{8}\) m\({}^{3}\)) \\ \hline LIK & 53.00 & 68.30 & 65.00 & 69.00 & 71.17 & 72.00 & 1.80 \\ DP & 18.50 & 29.00 & 28.00 & 29.50 & 31.50 & 34.50 & 0.28 \\ DFY & 18.00 & 28.00 & 27.00 & 28.50 & 30.74 & 33.60 & 0.21 \\ CH &

[MISSING_PAGE_FAIL:20]

* Deb (2001) Deb, K., 2001. _multi-objective optimization using evolutionary algorithms_ (1st ed. John Wiley & Sons. Publisher edition. ([http://www.loc.gov/~developers/negligible/034/2001022514.html](http://www.loc.gov/~developers/negligible/034/2001022514.html)). Table of Contents [http://www.loc.gov/cattid/toc/conid06/2001022514.html](http://www.loc.gov/cattid/toc/conid06/2001022514.html).
* Zhao et al. (2021) Zhao, Y., Wang, C., Wang, H., Liu, Y., 2021. Construction and application of reservoir flood control operation rules using the decision tree algorithm. Water 13 (24). Fan, C., Hou, J., Li, X., Song, G., Yang, Y., Liang, X., Zhou, Q., Imran, M., Chen, G., Wang, Z., Lu, P., 2025. Efficient urban flood control and drainage management framework based on digital twin technology and optimization scheduling algorithm. Water Res 282, 123711. [https://doi.org/10.1016/j.watres.2005.123711](https://doi.org/10.1016/j.watres.2005.123711).
* Peng et al. (2023) Peng, Z., Liu, W.-J., Zhang, T.-H., Wang, C.-W., Yang, T., 2023. Deriving hydropower reservoir operation policy using data-driven artificial intelligence model based on pattern recognition and metaheuristic optimizer. J. Hydrol. 624, 129961. [https://doi.org/10.11016/j.hydrol.2023.129961](https://doi.org/10.11016/j.hydrol.2023.129961).
* Hochreiter and Schmidhuber (1997) Hochreiter, S., Schmidhuber, J., 1997. Long Short-Term memory. Neural Comput. 9 (8), 1735-1780. [https://doi.org/10.1162/neco.1997.9.8.1735](https://doi.org/10.1162/neco.1997.9.8.1735).
* Huang et al. (2022) Huang, X., Xu, B., Zhong, P., Yao, H., Yu, Z., Liu, P., Lu, Q., Sun, Y., Mo, R. L., 2022. Robust multiobjective reservoir operation and risk decision-making model for real-time flood control coping with forecast uncertainty. J. Hydrol. 605, 127334. [https://doi.org/10.1016/j.hydrol.2021.27334](https://doi.org/10.1016/j.hydrol.2021.27334).
* Khepvint et al. (2025) Khepvint, V., Sharafati, A., Mohajeri, S.H., Hameed, A.S., Mehraei, M., 2025. A comparative study for predicting lake evaporation at chah nimeh reservoirs in Iran: employing the ADPLS-LSTM model with an attention mechanism. Earth Sci. Inform. 18 (1), 166. [https://doi.org/10.1007/s12145-024-01682-z](https://doi.org/10.1007/s12145-024-01682-z).
* Kartart et al. (2019) Kartart, F., Kot, D., Shalev, G., Rambuear, G., Hochreiter, S., Nearing, G., 2019. Benchmarking a catchment-aware hose short-term memory network (LSTM) for large-scale hydrological modeling. Hydrol. Earth Syst. Sci. Discuss. 2019, 1-32. [https://doi.org/10.48550/arXiv.1907.08456](https://doi.org/10.48550/arXiv.1907.08456).
* Leun et al. (2015) Leun, Y., Bengio, Y., Hinton, G., 2015. Deep learning nature 521 (7553), 436-444. [https://doi.org/10.1038/nature14539](https://doi.org/10.1038/nature14539).
* Lei et al. (2018) Lei, X., Zhang, J., Wang, H., Wang, M., Shu, S.T., Li, Z., Tan, Q., 2018. Deriving higher reservoir operating rules for flood control based on weighted non-dominated sorting genetic algorithm I. J. Hydrol. 564, 967-983. [https://doi.org/10.1016/j.hydrol.2018.07.075](https://doi.org/10.1016/j.hydrol.2018.07.075).
* Li et al. (2020) Li, H., Liu, P., Guo, S., Cheng, L., Yin, J., 2020. Climatic control of upper Yangtze river flood hazard diminished by reservoir groups. Environ. Res. Lett. 15 (12), 124013. [https://doi.org/10.1083/1748-93236.x46](https://doi.org/10.1083/1748-93236.x46).
* Lu et al. (2022) Lu, Q., Zhong, P., Xu, B., Huang, X., Zhu, P., Wang, H., Ma, Y., 2022. Multi-objective risk analysis for flood control operation of a complex reservoir system under multiple time-space correlated uncertainties. J. Hydrol. 606, 127419. [https://doi.org/10.1016/j.hydrol.2021.27419](https://doi.org/10.1016/j.hydrol.2021.27419).
* Mo et al. (2021) Mo, R., Xu, B., Zhong, P., Zhu, P., Huang, X., Liu, W., Xu, S., Wang, G., Zhang, J., 2021. Dynamic long-term streamflow probabilistic forecasting model for a multisite system considering real-time forecast updating through spatio-temporal dependent error correction. J. Hydrol. 601, 126666. [https://doi.org/10.1016/j.hydrol.2021.26666](https://doi.org/10.1016/j.hydrol.2021.26666).
* Mo et al. (2023) Mo, R., Xu, B., Zhong, P., Dong, Y., Wang, H., Yue, H., Zhu, J., Wang, H., Wang, G., Zhang, J., 2023. Long-term probabilistic streamflow forecast model with "inputs-structure-parameters" hierarchical optimization framework. J. Hydrol. 622, 129736. [https://doi.org/10.1016/j.hydrol.2023.129736](https://doi.org/10.1016/j.hydrol.2023.129736).
* Ning et al. (2024) Ning, Y., Ren, M., Guo, S., Liang, G., He, B., Liu, X., Yang, R., 2024. An advanced Multi-Objective ant lion algorithm for reservoir flood control operation. Water 16 (6), 852. [https://doi.org/10.3390/w16060852](https://doi.org/10.3390/w16060852).
* Niu et al. (2019) Niu, W.-J., Feng, Z.-K., Feng, B.-F., Min, Y.-W., Cheng, C.-T., Zhou, J.-Z., 2019. Comparison of multiple linear regression, artificial neural network, extreme learning machine, and support vector machine in deriving operation end-to-end low-resource reservoir. Water 11 (1), 88. [https://doi.org/10.3390/w11010088](https://doi.org/10.3390/w11010088).
* Shen (2018) Shen, C., 2018. A transdisciplinary review of deep learning research and its relevance for water resources scientists. Water Res. 54 (11), 8558-8593. [https://doi.org/10.1020/s10870826243](https://doi.org/10.1020/s10870826243).
* Shi et al. (2015) Shi, X., Chen, Z., Wang, H., Yeung, D.-Y., Wong, W.-K., Woo, W.-C., 2015. Convolutional LSTM network: a machine learning approach for precipitation nowcasting. Adv. Neural Inf. Process. Syst. 28, [https://doi.org/10.1007/978-3-319-21233-3.6](https://doi.org/10.1007/978-3-319-21233-3.6).
* Tandon and Sen (2025) Tandon, K., Sen, S., 2025. A probabilistic integration of LSTM and Gaussian process regression for uncertainty-aware reservoir water level predictions. Hydrol. Sci. J. 70 (1), 144-161. [https://doi.org/10.1080/0256667-2024-248268](https://doi.org/10.1080/0256667-2024-248268).
* Tang et al. (2022) Tang, J., Yang, R., Yuan, G., Mao, Y., 2022. Time-Series deep learning models for reservoir scheduling problems based on LSTM and wavelet transformation. Electronics 11 (19). [https://doi.org/10.3390/electronics119322](https://doi.org/10.3390/electronics119322).
* Wan et al. (2023) Wan, W., Liu, Y., Zheng, H., Zhao, J., Zhao, P., Lu, Y., 2023. Optimization of multi-reservoir flood control operating rules: a case study for the chaohai river basin in China, Water 15 (15), 2817. [https://doi.org/10.3390/w15152817](https://doi.org/10.3390/w15152817).
* Wang et al. (2025) Wang, Z., Fang, X., Zhang, W., Wang, L., Wang, H., Chen, 2025. Dynamic intelligent prediction approach for landslide displacement based on biological growth models and CNN-LSTM. J. Mol. Sci. 22 (1), 71-88. [https://doi.org/10.1007/s11629-024-91133-y](https://doi.org/10.1007/s11629-024-91133-y).
* Wu et al. (2024) Wu, M., Liu, P., Liu, L., Zou, K., Luo, X., Wang, J., Xia, Q., Wang, H., 2024. Improving a hydrological model by coupling it with an LSTM water use forecasting model. J. Hydrol. 636, 131215. [https://doi.org/10.1016/j.hydrol.2024.131215](https://doi.org/10.1016/j.hydrol.2024.131215).
* Xu et al. (2022) Xu, B., Sun, Y., Huang, X., Zhong, P., 2022. A, Zhu, P., Zhang, J., Wang, X., Wang, G., Ma, Y., Lu, Q., 2022. Scenario-based multiobjective robust optimization and decision-making framework for optimal operation of a cascade hydropower system under multiple uncertainties. Water Res. 58 (4), e2021WR030965. [https://doi.org/10.10129/2021WR030965](https://doi.org/10.10129/2021WR030965).
* Xu et al. (2021) Xu, W., Liu, P., Cheng, L., Zhou, Y., Xia, Q., Gong, Y., Liu, Y., 2021. Multi-step wind speed prediction by combining a WRF simulation and an error correction strategy. Renew. Energy 163, 772-782. [https://doi.org/10.1016/j.renene.2020.09.032](https://doi.org/10.1016/j.renene.2020.09.032).
* Yang et al. (2020) Yang, G., Guo, S., Liu, P., Li, Xu, C., 2021. Multiobjective reservoir operating rules based on cascade reservoir input variable selection method. Water Res. 53 (43), 436-436. [https://doi.org/10.1007/s1020201301](https://doi.org/10.1007/s1020201301).
* Yang et al. (2022) Yang, R., Qi, Y., Lei, J., Ma, X., Zhang, H., 2022. A parallel multi-objective optimization algorithm based on coarse-to-fine decomposition for real-time large-scale reservoir flood control operation. Water Resour. Mag. 36 (9), 3207-3219. [https://doi.org/10.1007/s11269-022-03196-z](https://doi.org/10.1007/s11269-022-03196-z).
* Ye et al. (2024) Ye, H., Liu, P., Zhang, X., Xu, H., Liu, W., 2024. Regarding reservoirs as switches deriving restored and regulated runoff with one long short-term memory model. J. Hydrol. Reg. Stud. 56, 102062. [https://doi.org/10.1016/j.hydrol.2024.1020626](https://doi.org/10.1016/j.hydrol.2024.1020626).
* Zhang et al. (2018) Zhang, D., Lin, J., Peng, Q., Wang, D., Yang, T., Sonoghsian, S., Liu, X., Zhuang, J., 2018. Modeling and simulating of reservoir operation using the artificial neural network, support vector regression, deep learning algorithm. J. Hydrol. 565, 270-276. [https://doi.org/10.1016/j.hydrol.2018.08500](https://doi.org/10.1016/j.hydrol.2018.08500).
* Zhang et al. (2025) Zhang, J., Hong, Y., Wang, L., Li, X., Lei, H., Gao, B., Zheng, J., 2025. LSTM-based proxy model with wellbore-reservoir coupling simulations for predicting multi-dimensional state parameters in depleted gas reservoirs. Comput. Geosci. 196, 105824. [https://doi.org/10.1016/j.cago.2024.105824](https://doi.org/10.1016/j.cago.2024.105824).
* Zheng et al. (2022) Zheng, Y.