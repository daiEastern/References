# A physics-constrained Informer-LSTM network for battery state-of-charge estimation

Yi Xie

Xiey@sari.ac.cn

Zhenqi Han

Jialu Zhang

Lizhuang Liu

xhangjl@sari.ac.cn Shanghai Advanced Research Institute, Chinese Academy of Sciences, Shanghai, 201210, China University of Chinese Academy of Sciences, Beijing, 100049, China

###### Abstract

Lithium-ion batteries are widely used in energy storage systems due to their high energy density and long cycle life. As a key indicator of remaining battery capacity, the state-of-charge (SOC) is crucial for battery management system (BMS). However, SOC cannot be directly measured and is affected by various nonlinear factors, posing significant challenges for accurate estimation. To enhance estimation accuracy and generalization, this study proposes a deep learning model incorporating physical constraints. The model couples the Informer and long short-term memory (LSTM) architectures: the Informer extracts global temporal features from battery data, while the LSTM models key parameters of a second-order equivalent circuit, embedding them as prior knowledge into the SOC estimation process to ensure physical consistency. Additionally, a temperature-aware weighted loss function is introduced to improve the model's robustness under complex operating conditions. Experimental results demonstrated that the proposed method outperformed existing approaches in both estimation accuracy and stability, showing strong potential for practical engineering applications.

2025 118381

## 1 Introduction

With the escalating crisis of fossil fuel depletion and environmental pollution, the global energy structure is undergoing a rapid transformation. Promoting the upgrading of the energy industry through renewable and clean energy sources has garnered widespread international attention [1]. Lithium-ion batteries, owing to their high energy density, lightweight design, lack of memory effect, and voltage stability, have been widely adopted in energy storage systems and are considered among the most promising energy carriers currently available [2]. Among various battery state parameters, the SOC represents the ratio of the currently available capacity to the nominal capacity, reflecting the remaining energy and sustainable working time of the battery [3]. Accurate SOC estimation plays a vital role in preventing overcharging and overdischarging, enhancing operational safety, and prolonging battery lifespan [4]. However, SOC cannot be measured directly and must be estimated based on measurable variables such as current and voltage [5]. Consequently, achieving high-precision SOC estimation is of great significance for the large-scale deployment of lithium-ion batteries.

Currently, SOC estimation methods are primarily classified into three categories: direct measurement methods, model-based methods, and data-driven methods. Direct measurement methods estimate SOC based on the physical characteristics of the battery, such as the mapping relationships between SOC and open-circuit voltage (OCV) or internal resistance [6]. For instance, the OCV method requires the construction of an OCV-SOC fitting function and the measurement of terminal voltage after the battery has rested for approximately 30 min, from which SOC can be estimated [7]. The coulomb-counting method estimates SOC by integrating the battery's charge and discharge current over time [8]. Despite their structural simplicity and the lack of complex modeling requirements, these methods are generally unsuitable for real-time applications and are highly susceptible to errors caused by initial SOC inaccuracies and battery aging [9, 10].

Model-based methods simulate the internal electrochemical or electro-dynamic behaviors of batteries using mathematical models, often combined with filtering algorithms like extended Kalman filter (EKF) or particle filter (PF) for dynamic SOC estimation. Electrochemical models, which describe internal processes such as electrode reactions and ion transport via partial differential equations, can provide high accuracy [11]. For example, Fan et al. [12] simplified the single particle model (SPM) to develop a reduced-order nonlinear model (ROM-NL) for real-time applications. Wang et al. [13] further improved estimation precision by combining the simplified model with PF. However, these models are computationally intensive and lack real-time feasibility [14]. In contrast, equivalent circuit models (ECMs)use electrical components like voltage sources, resistors, and capacitors to mimic battery behavior [15; 16; 17]. They are more practical but highly sensitive to temperature and charge or discharge rate variations, requiring frequent parameter updates to avoid error accumulation [18].

Data-driven methods treat the battery as a black box and use machine learning or deep learning techniques to estimate SOC from large datasets [19]. These models can effectively capture nonlinear relationships and offer strong adaptability [20]. Common models include support vector machines (SVM) [21], deep neural networks (DNN) [22], LSTM [23], and convolutional neural networks (CNN) [24]. Additionally, Shi et al. [25] proposed a cloud-based SOC estimation framework leveraging a self-supervised transformer network. Yang et al. [26] developed a unified adaptive deep transfer learning model capable of estimating SOC under dynamic operating conditions across the battery's entire lifecycle. Sun et al. [27] proposed a hybrid model combining bidirectional LSTM (BILSTM) and bemual basis expansion analysis for time series (N-BEATS), enhancing both the accuracy and robustness of SOC estimation. Although data-driven methods possess strong learning capabilities, they heavily rely on training data and lack physical constraints, which limits their generalization ability and makes them susceptible to external factors such as aging and temperature fluctuations [28; 29; 30]. Therefore, a method that balances physical interpretability, strong modeling capability, and adaptability to complex operating conditions is urgently needed.

In addition to conventional SOC estimation based on external electrical signals, recent studies have explored techniques for sensing internal cell states. Some researchers embedded fiber-optic sensors in cells to directly monitor internal strain and temperature, providing valuable insight into SOC estimation [31]. However, these invasive approaches may disrupt battery structure and performance [32]. Non-invasive techniques like ultrasonic sensing offer an alternative, being unaffected by voltage or current and suitable for real-time monitoring. For example, Yang et al. [33] proposed a method combining back propagation neural networks (BPNN) with ultrasonic signals to monitor SOC. Tang et al. [34] combined multi-site ultrasonic scanning with deep residual-pooling extreme learning machines (DR-PELM) for SOC estimation. While these methods offer promising directions, they continue to be hindered by issues such as external noise, signal instability, packaging complexity, and high implementation cost. Therefore, methods based on external, measurable electrical parameters remain the most feasible and widely applicable solution in practice.

Motivated by these insights, this study proposes a Physics-constrained Informer-LSTM Network (PILNet) for SOC estimation, which integrates physical modeling with deep learning using externally measurable parameters. The method combines the interpretability and structural advantages of a second-order ECM with the powerful time-series modeling capabilities of the Informer network [35], enabling deep fusion of physical priors and data-driven learning for accurate SOC estimation under complex conditions. The main contributions of this study can be summarized as follows:

1. Introduction of a physics-constrained equivalent circuit modeling module. A LSTM network is employed to estimate the key parameters of the ECM, enabling SOC estimation while preserving the electrochemical structure and inherent constraints of the battery. This integration enhances both the interpretability and robustness of the model.
2. Design of the coupled PILNet architecture. The proposed network integrates Informer and LSTM modules, where the Informer captures global temporal dependencies, and the LSTM models the dynamic parameters of the equivalent circuit. The SOC representation output by the Informer serves as a key physical feature to guide the learning of LSTM parameters, thereby enabling effective information fusion and structural coupling between SOC estimation and physical parameter estimation.
3. Development of a temperature-aware weighted fusion loss function. To account for the sensitivity of battery performance to temperature variations, the proposed method applies adaptive weighting coefficients across different temperature regions. This design enhances the model's adaptability to multi-temperature conditions and improves the accuracy of SOC estimation under varying thermal environments.

The remainder of this paper is organized as follows. Section 2 introduces the architecture of the proposed PILNet model and its physical modeling principles. Section 3 details the experimental dataset and setup. Section 4 reports and analyzes the experimental results. Finally, Section 5 provides a summary of this study.

## 2 Methodology

### Overall framework of the PILNet algorithm

The overall architecture of the proposed PILNet model is illustrated in Fig. 1, which consists of three key modules: a temporal feature extraction network, a physically-based dynamic constraint module, and a jointly optimized objective function.

Firstly, the data-driven component employs a temporal network based on the Informer architecture to capture nonlinear dependencies among current, voltage, temperature, and SOC within multivariate battery operation data. Secondly, to incorporate the inherent physical behavior of battery systems, a second-order resistor-capacitor (RC) model [36] is integrated as prior knowledge. It is formulated as a set of difference-based physical constraint equations to enhance the model's physical consistency and generalization capability. Finally, to balance estimation accuracy and physical interpretability, PILNet utilizes a joint loss function that combines the mean squared error (MSE) of SOC estimation with the physical modeling error. Additionally, a tunable physical consistency coefficient is introduced to facilitate collaborative optimization between data-driven learning and physical modeling.

### Physical constraints based on the second-order RC model

To enhance the physical consistency of neural network predictions, the proposed PILNet incorporates a typical second-order RC model, as illustrated in Fig. 2. This model consists of an OCV (\(V_{\text{OC}}\)), an ohmic resistance (\(R_{0}\)), and two parallel RC branches (\(R_{1}\)-\(C_{1}\) and \(R_{2}\)-\(C_{2}\)), which effectively capture the nonlinear voltage response characteristics of lithium-ion batteries during dynamic charge and discharge processes.

Compared to the first-order RC model, the second-order model introduces an additional polarization branch, enabling more accurate representation of voltage dynamics across different time scales, especially under high-frequency or complex operating conditions. Studies have shown that in applications requiring high-precision battery management, such as electric vehicles and grid energy storage systems, the second-order RC model consistently outperforms the first-order model in both voltage and state estimation accuracy [37].

In this model, the terminal voltage \(U(t)\) of the battery is expressed as follows:

\[U(t)=V_{\text{OC}}(\text{SOC}(t))-R_{0}I(t)-V_{1}(t)-V_{2}(t) \tag{1}\]

Here, \(V_{\text{OC}}(\text{SOC}(t))\) represents the OCV, which is a nonlinear function of SOC. \(I(t)\) is the battery current (positive for discharge). \(V_{1}(t)\) and \(V_{2}(t)\) represent the polarization voltages across the two RC branches \(R_{1}\)-\(C_{1}\) and \(R_{2}\)-\(C_{2}\) respectively.

The polarization voltages evolve according to the following first-order differential equations:

\[\frac{dV_{1}(t)}{dt} =-\frac{1}{R_{1}C_{1}}V_{1}(t)+\frac{1}{C_{1}}I(t) \tag{2}\] \[\frac{dV_{2}(t)}{dt} =-\frac{1}{R_{2}C_{2}}V_{2}(t)+\frac{1}{C_{2}}I(t) \tag{3}\]To facilitate numerical implementation, the polarization voltages are discretized using analytical solutions, as given by the following expression:

\[V_{i}(t)=R_{i}\left(1-e^{-\alpha t/(R,C_{i})}\right)I(t),\quad i=1,2 \tag{4}\]

Here, \(\alpha t\) denotes the sampling interval. Moreover, the relationship between \(V_{\text{OC}}\)(SOC) and SOC is nonlinear. To improve fitting performance and avoid overfitting or oscillations caused by high-order polynomials, this study employs a fifth-order polynomial to approximate this relationship [38], as illustrated below:

\[V_{\text{oc}}(\text{SOC})=a_{0}\text{SOC}^{+}+a_{1}\text{SOC}^{+}+a_{2}\text {SOC}^{+}+a_{3}\text{SOC}^{2}+a_{4}\text{SOC}+a_{5} \tag{5}\]

Where coefficients \(a_{0}\sim a_{5}\) are obtained through offline parameter identification or neural network training, and can be adapted to various cell chemistries and aging states.

This modeling approach offers several advantages. First, it preserves the physical interpretability of RC circuits in characterizing the transient response of batteries. Second, it mitigates the result drift issues that may arise in purely data-driven models. Moreover, by directly incorporating the battery's voltage dynamics into the loss function, it enhances the model's sensitivity to underlying physical mechanisms.

### SOC estimation under physical constraints

#### 2.3.1 Temporal modeling and SOC estimation

Battery systems exhibit pronounced temporal correlations, where state evolution is influenced not only by current inputs but also by extensive historical operating trajectories. To achieve accurate estimation of the SOC evolution, the proposed PILNet model leverages a deep temporal prediction module based on the Informer architecture as its backbone network. This module effectively extracts long-range dependency features from high-dimensional time series data, including current, voltage, and temperature. The network architecture is depicted in Fig. 3.

Compared with traditional recurrent neural networks, Informer, as an improved version of the Transformer [39], offers better computational efficiency and enhanced capability to model long-term dependencies when processing long sequences of battery operation data. The key design features include the following:

1. ProbSparse Attention: Compared to the standard self-attention mechanism, Informer introduces the probabilistic sparse attention (ProbSparse Attention), which retains only the top-K most influential queries for the output. This approach significantly improves inference speed while ensuring accurate capture of key charging and discharging characteristics of the battery.
2. Embedding Module: To incorporate periodicity and external temporal features such as ambient temperature in the SOC evolution, the model integrates positional encoding, value encoding, and time-step encoding at the input stage. This fusion embeds timestamps, historical current, voltage, and temperature data into a unified feature space, enabling the model to effectively recognize the temporal dependencies and seasonal fluctuations inherent in SOC evolution.
3. Encoder-Decoder Structure: The encoder comprises multiple stacked layers of sparse attention modules and feedforward networks, combined with residual connections and normalization techniques to efficiently encode long-term historical information. The decoder aligns the encoded historical data with the latest observed inputs through self-attention and encoder-decoder attention mechanisms to generate accurate SOC predictions.

Throughout the modeling process, the model input consists of current, voltage, and temperature sequences \(X_{t-w:t}\in\mathbb{R}^{n\times d}\) within a historical window of length \(w\), and the output is an SOC sequence \(\hat{y}_{t:t+H}\in\mathbb{R}^{H}\) with a step size of \(H\). This output, together with the terminal voltage predicted by the equivalent circuit model, forms the joint loss function of PILNet, enforcing physical consistency constraints and further enhancing the accuracy and interpretability of SOC estimation under varying operating conditions.

Figure 1: Framework of the proposed PILNet model.

Figure 2: Second-order RC model.

#### 2.3.2 Second-order RC model parameter estimation

In the typical operation of lithium-ion batteries, key parameters within the equivalent circuit model are not static but evolve dynamically with the battery's operational state. Specifically, variations in the SOC significantly influence the utilization of active materials and the electrochemical reaction rates, thereby altering charge transfer resistance and diffusion impedance. Temperature fluctuations affect the viscosity of the electrolyte and ion mobility, leading to changes in ohmic resistance and the parameters associated with polarization branches. Moreover, the magnitude of the discharge or charge current modulates the degree of polarization, resulting in variations in the equivalent time constants of the polarization branches. Consequently, treating the RC parameters as time-varying dynamic states and identifying them based on sequential input data can more accurately characterize the battery's transient response and terminal voltage behavior under complex operating conditions.

Based on this insight, and to enhance the model's physical consistency, PILNet integrates a parameter estimation submodule on top of the data-driven SOC estimation architecture. This submodule is designed to dynamically identify the key parameters of the second-order RC equivalent circuit and the nonlinear OCV-SOC relationship. It leverages a LSTM [40] architecture, which is capable of modeling temporal dependencies, to extract critical sequential features from observed sequences of current, voltage, SOC, and temperature. These features are then used to infer the internal states constrained by physical principles, which in turn contribute to terminal voltage computation. It is important to note that the estimated parameters are not directly involved in the loss function; rather, they are used to calculate the terminal voltage via Kirchhoff's Voltage Law (as defined in Section 2.2), which serves as the basis for constructing the loss term.

The architecture of this parameter estimation module is illustrated in Fig. 4. Through its integration with the SOC estimation component, the module enhances the accuracy of terminal voltage estimation and improves the model's adaptability and interpretability under diverse operating conditions.

#### 2.3.3 Design of the joint loss function

To achieve a balance between predictive accuracy and physical consistency, PILNet adopts a multi-objective joint loss function that integrates both data-driven error and physics-informed error components. This design guides the model to not only accurately fit the actual SOC trajectory, but also to conform to the physical laws governing the evolution of terminal voltage, thereby enhancing the model's generalizability and interpretability.

1. SOC Estimation Loss. To evaluate the numerical accuracy of SOC estimation, the MSE is used as the primary loss term, defined as: \[\mathcal{L}_{\text{SOC}}=\frac{1}{n}\sum_{k=1}^{n}\left(\text{SO}\hat{c}(k)- \text{SOC}(k)\right)^{2}\] (6) where SO\((k)\) is the estimated SOC at time step \(k\), SOC\((k)\) is the corresponding ground truth value, and \(n\) is the total number of time steps. This loss term directly reflects the model's capability to capture SOC dynamics and serves as the primary objective during training.
2. Terminal Voltage Consistency Loss. To enforce physical consistency in model outputs, a voltage residual term is introduced as an auxiliary supervision signal, defined as: \[\mathcal{L}_{\text{Voltage}}=\frac{1}{n}\sum_{k=1}^{n}\left(\hat{V}(k)-V(k) \right)^{2}\] (7) Here, \(\hat{V}(k)\) denotes the estimated terminal voltage at time step \(k\), derived from the estimated SOC and RC parameters using the second-order equivalent circuit model, while \(V(k)\) is the corresponding measured terminal voltage. By minimizing this discrepancy, the model is encouraged to learn internal states that are more consistent with the underlying physical mechanisms.
3. Overall Optimization Objective. The final training objective combines the above loss terms into a unified formulation via a

Figure 4: Architecture of the LSTM Model.

Figure 3: Architecture of the Informer Model.

weighted sum, given by:

\[\mathcal{L}_{\text{Total}}=\mathcal{L}_{\text{SOC}}+\alpha\cdot\mathcal{L}_{ \text{Voltage}} \tag{8}\]

Here, \(\alpha\) is a tunable physical consistency factor used to balance the trade-off between data fitting accuracy and the strength of physical constraints. A properly chosen \(\alpha\) helps achieve an optimal balance between estimation performance and physical consistency.

## 3 Battery experiments

### Public dataset description

The experiments in this study utilize a publicly available lithium-ion battery dataset released by the Center for Advanced Life Cycle Engineering (CALCE) at the University of Maryland. The tested cells are cylindrical A123 18650-type lithium iron phosphate (LFP) batteries with graphite anodes [41]. The key specifications of the battery are listed in Table 1.

To realistically simulate the dynamic operating conditions of lithium-ion batteries in electric vehicles, this dataset includes three representative discharge profiles tested under a range of ambient temperatures (0 \({}^{\circ}\)C, 10 \({}^{\circ}\)C, 25 \({}^{\circ}\)C, 30 \({}^{\circ}\)C, 40 \({}^{\circ}\)C, and 50 \({}^{\circ}\)C). The selected discharge profiles are the Dynamic Stress Test (DST), US06, and the Federal Urban Driving Schedule (FUDS), all of which were designed by the US Advanced Battery Consortium to emulate typical driving behaviors and associated battery usage [42]. Specifically:

1. The US06 profile simulates highway driving conditions, characterized by aggressive acceleration and rapid speed fluctuations, thereby imposing significant stress on the battery.
2. The FUDS profile replicates frequent stop-and-go traffic in urban environments, involving numerous accelerations and decelerations.
3. The DST profile consists of a sequence of current steps with varying amplitudes and durations, exhibiting an average load similar to FUDS, while incorporating a mechanism to simulate capacity recovery effects.

Each charge-discharge cycle proceeds as follows: the battery is first charged using a Constant Current-Constant Voltage (CC-CV) protocol at 1C rate until the upper voltage limit is reached. The voltage is then held constant until the current drops below 0.01C, at which point charging is terminated. The battery is then discharged continuously according to the designated dynamic load profile until the terminal voltage drops to 2.0 V, marking the end of the discharge phase. Throughout the entire process, current, voltage, and surface temperature are sampled at a rate of 1 Hz. Fig. 5 illustrates the variations in current, voltage, and surface temperature under the three discharge profiles at an ambient temperature of 25 \({}^{\circ}\)C.

### Data analysis and preprocessing

To investigate the distributional characteristics under three representative operating conditions, a statistical analysis of current, voltage, and temperature was conducted at 25 \({}^{\circ}\)C, including the computation of mean and standard deviation. Additionally, kernel density estimation (KDE) was employed to visualize the probability distributions of these features. Table 2 summarizes the mean and standard deviation (Std) values for each condition, while Fig. 6 presents the corresponding KDE curves for current, voltage, and temperature. The results reveal that the discharge load amplitudes are generally consistent across conditions, with the primary distribution peaks of all features closely aligned. The peak density values of current and voltage exhibit minimal variation, and the 5th to 95th percentile coverage ranges largely overlap across different conditions. These observations indicate that the input feature distributions remain stable under typical dynamic operating conditions, thereby supporting the generalizability and robustness of the proposed model in such scenarios.

The original battery dataset comprises four variables: current, voltage, temperature, and SOC, each recorded at every time step with complete observations. Due to the heterogeneous units and varying numerical scales of these features, directly feeding the raw data into deep neural network models may result in poor training efficiency or convergence instability. Therefore, it is necessary to normalize the input data to ensure numerical consistency across features, thereby enhancing model training stability and generalization performance.

In this study, Z-Score normalization is employed to standardize all feature variables. This method transforms the original data into a distribution with zero mean and unit variance. Let \(x\) denote the raw input value, and \(x^{*}\) the normalized value; the transformation is defined by Eq. (9):

\[x^{*}=\frac{x-\mu}{\sigma} \tag{9}\]

where \(\mu\) and \(\sigma\) represent the mean and standard deviation of each feature calculated from the training set. The same normalization parameters are applied to the test set to maintain consistency.

Moreover, considering the multi-scale temporal dynamics during battery charge-discharge cycles and the strong temporal correlation among observations, a sliding window mechanism is introduced during sample construction. The time series is partitioned into three segments: a historical input sequence fed into the encoder to capture long-term dependencies, and a recent observation sequence together with a prediction sequence, both fed into the decoder. This structure provides short-term contextual information and enables multi-step estimation of electrical parameters.

### Evaluation metrics and experimental setup

To comprehensively evaluate the performance of the proposed model, two widely used regression metrics are employed: Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE). Their mathematical definitions are presented in Eqs. (10) and (11):

\[\text{RMSE}=\sqrt{\frac{1}{n}\sum_{i=1}^{n}(y_{i}-\hat{y}_{i})^{2}} \tag{10}\] \[\text{MAE}=\frac{1}{n}\sum_{i=1}^{n}|y_{i}-\hat{y}_{i}| \tag{11}\]

Where \(y_{i}\) denotes the ground truth, \(\hat{y}_{i}\) is the predicted value, and \(n\) is the total number of samples. RMSE is more sensitive to larger estimation errors, while MAE provides a more balanced evaluation of overall deviation. These two metrics complement each other to offer a comprehensive assessment of model accuracy and robustness.

To enhance the model's robustness during inference and mitigate the training-inference discrepancy, this study employs a hybrid strategy combining teacher forcing and a customized scheduled sampling

\begin{table}
\begin{tabular}{l l} Parameter & Value \\ \hline Type & A123 18650 \\ Cathode Material & LFP \\ Anode Material & Graphite \\ Nominal Capacity & 1.1 Ah \\ Charge Voltage & 3.6 V \\ Discharge Cut-off Voltage & 2.0 V \\ End-of-Charge Current & 0.01 C \\ \hline \end{tabular}
\end{table}
Table 1: Key specifications of the lithium-ion battery.

scheme during training. Specifically, within the circuit parameter estimation module, the model dynamically selects either the ground truth SOC or its own estimated SOC as input. The sampling rate decays linearly with the training epochs according to:

\[\text{sampling\_rate}=\max\left(0.5\times\left(1-\frac{epoch}{epochs}\right),0\right) \tag{12}\]

where _epoch_ denotes the current training epoch and _epochs_ represents the pre-defined maximum number of training epochs. The initial sampling rate is set to 0.5 and gradually decreases to 0 as training progresses, ensuring a smooth transition from reliance on ground truth inputs to complete dependence on the model's own results, thereby improving the adaptability of autoregressive inference.

Experiments use DST and US06 driving cycles as training datasets, while FUDS cycle is reserved for testing to evaluate the model's generalization ability under unseen conditions. All experiments are conducted using PyTorch 1.7.1 on a workstation equipped with an NVIDIA GeForce RTX 3090 GPU. The Adam optimizer is adopted with an initial learning rate of 1e-4. A combined strategy of Early Stopping (patience of 5 epochs) and learning rate scheduling is applied, where the learning rate is halved every epoch to effectively prevent overfitting and accelerate convergence. Each experiment is repeated 8 times, with

\begin{table}
\begin{tabular}{l l l l l l l} \hline Condition & Current (A) & \multicolumn{2}{c}{Voltage (V)} & \multicolumn{2}{c}{Temperature (\({}^{\circ}\) C)} \\  & Mean & Std & Mean & Std & Mean & Std \\ \hline DST & 0.5022 & 0.9050 & 3.1642 & 0.1926 & 27.2745 & 0.1942 \\ US06 & 0.5313 & 0.7525 & 3.1630 & 0.1610 & 27.1217 & 0.1766 \\ FUDS & 0.5036 & 0.9700 & 3.1683 & 0.1950 & 27.2524 & 0.1995 \\ \hline \end{tabular}
\end{table}
Table 2: Mean and Std of current, voltage, and temperature under three typical dynamic conditions at 25 °C.

Figure 5: Current, voltage, and temperature variation during a single discharge cycle at 25 °C under (a) DST, (b) FUDS, and (c) US06 profiles.

Figure 6: KDE curves of current, voltage, and temperature under three typical operating conditions at 25 °C.

a maximum of 30 training epochs per run. Other hyperparameters are summarized in Table 3.

## 4 Results and discussion

### Comparison with other algorithms

To verify the effectiveness and advancement of the PILNet model in the SOC estimation task, a comprehensive set of experiments, including ablation analysis and comparisons with mainstream models, was conducted. Specifically, to evaluate the role of physics-informed constraints in enhancing model performance, a baseline Informer model without any physics-related loss components was constructed. This baseline relies purely on data-driven modules. Its performance is compared with that of PILNet, which incorporates circuit-based physical constraints. In all experiments, the initial SOC is set to 100%. The comparison results under the FUDS at different ambient temperatures are presented in Table 4.

Experimental results demonstrate that PILNet significantly outperforms the original Informer model across various temperature conditions, indicating that the incorporation of the physics-consistency loss term effectively enhances the estimation accuracy. The performance improvement is particularly pronounced under normal and high-temperature conditions, reflecting the adaptability and advantage of the physical constraint in complex thermal environments.

To further assess the overall performance of PILNet compared to representative state-of-the-art models in the battery SOC estimation domain, we selected two recent deep learning models - Mambal Lithium [43] and Informer-LSTM [44] - as baseline algorithms. The experiments were conducted under a unified dataset and identical configurations. The performance comparison results are reported in Table 5.

As shown in Table 5, PILNet consistently achieves the lowest RMSE and MAE across all temperature settings ranging from 0 \({}^{\circ}\) C to 50 \({}^{\circ}\) C. This demonstrates its superior accuracy and robustness in SOC estimation under varying environmental conditions. The average RMSE and MAE of PI LNet are 0.974% and 0.782%, respectively, significantly outperforming Mambal Lithium and Informer-LSTM. These results highlight the advantages of PILNet in capturing the dynamic behavior of batteries more effectively.

To more intuitively illustrate the model's performance across different time steps, 7 presents the SOC estimation curves of various models under the 25 \({}^{\circ}\)C condition, while 8 depicts the corresponding error time series. The results indicate that the trajectory predicted by PILNet closely aligns with the ground truth SOC curve overall. In practical operation, instantaneous fluctuations in battery load induce abrupt changes in terminal voltage and polarization voltage, causing local jumps in the true SOC, which in turn amplify local errors in the model and lead to error clustering at specific time points. Furthermore, the periodic load patterns inherent in discharge conditions cause cyclic variations in current, voltage, and temperature. The multi-physical coupling with periodicity also contributes to noticeable oscillations in the SOC estimation error. Nevertheless, the error magnitude of PILNet is significantly lower than that of the comparative models, further confirming its accuracy and stability under dynamically complex operating conditions.

### Influence of temperature on the loss weight coefficient a

To enhance the generalization capability and estimation accuracy of the model across varying temperature conditions, this study introduces a loss weighting mechanism in the objective function. The proper setting of the loss weight coefficient \(\alpha\) plays a critical role in determining final model performance. Given the significant influence of temperature on the electrochemical characteristics of batteries, employing a uniform weighting scheme across all temperature ranges fails to capture performance nuances. Therefore, a segmented parameter tuning strategy is adopted, in which the value of \(a\) is optimized individually for each temperature interval. This approach balances the fitting precision of both SOC and voltage, thereby improving the overall performance.

Experimental results reveal that the optimal value of \(\alpha\) varies with temperature, which aligns with the observed changes in the battery's dynamic response characteristics. For instance, in the low-temperature range, batteries exhibit higher internal resistance and more unstable voltage fluctuations. In such cases, increasing the weight of the voltage

\begin{table}
\begin{tabular}{l l l l} \hline \hline Dataset & Temperature & Algorithm & RMSE (\%) & MAE (\%) \\ \hline FUDS & 0 \({}^{\circ}\)C & PILNet & 1.008 & 0.844 \\  & & Informer & 1.135 & 0.961 \\  & 10 \({}^{\circ}\)C & PILNet & 1.220 & 0.901 \\  & 10 \({}^{\circ}\)C & Informer & 1.301 & 1.016 \\  & 25 \({}^{\circ}\)C & PILNet & 1.037 & 0.834 \\  & & Informer & 1.523 & 1.158 \\  & 30 \({}^{\circ}\)C & PILNet & 0.867 & 0.727 \\  & & Informer & 1.131 & 0.887 \\  & 40 \({}^{\circ}\)C & PILNet & 0.860 & 0.707 \\  & & Informer & 1.012 & 0.812 \\  & 50 \({}^{\circ}\)C & PILNet & 0.850 & 0.678 \\  & & Informer & 0.863 & 0.707 \\ \hline \hline \end{tabular}
\end{table}
Table 4: Performance comparison between PILNet and Informer under FUDS at different temperatures.

\begin{table}
\begin{tabular}{l l l} \hline \hline Parameter & Value \\ \hline Batch size & 32 \\ Dropout rate & 0.05 \\ Model dimension (\(t_{\text{data}}\)) & 512 \\ Number of attention heads (\(n_{\text{best}}\)) & 8 \\ ProbSparse factor & 5 \\ Fully connected layer dimension & 2048 \\ \hline \hline \end{tabular}
\end{table}
Table 3: Model hyperparameters.

Figure 8: Residual time series of SOC estimation at 25\({}^{\circ}\) C.

Figure 7: Comparison of estimated and actual SOC curves at 25\({}^{\circ}\) C.

error term facilitates learning stronger physical consistency and enhances robustness. Under ambient conditions, the battery operates in a more stable state, with a clearer coupling relationship between voltage and SOC, making the voltage error less influential. In the mild high-temperature zone, the battery reaches its optimal working condition, where the overall system error is minimized, and thus the weight on the voltage term can be further reduced. In the high-temperature range, although the electrochemical reaction rate increases, which favors learning temperature-dependent patterns, the accompanying rise in measurement noise makes the model more vulnerable to voltage fluctuations.

Table 6 summarizes the optimal \(a\) values determined for each temperature range. Meanwhile, Fig. 9 illustrates the variation trends of estimation errors across different temperature regions under varying \(a\) weightings. It can be observed that independently adjusting the \(a\) weight for each temperature region enables the model to achieve better estimation accuracy within that region compared to using a single fixed value. This demonstrates the effectiveness of the partitioned weighting strategy in enhancing multi-condition adaptability.

### Robustness experiments of the model

In this section, while keeping the model structure and hyperparameter settings unchanged, two groups of robustness experiments are conducted based on the FUDS dataset at 25 \({}^{\circ}\)C to systematically evaluate the model's stability and anti-interference capability under different operating conditions.

Firstly, in practical BMS applications, the initial SOC state of the battery may vary significantly due to user habits, load conditions, and task requirements. Therefore, the robustness and generalization ability of the model under different initial SOC levels is an important metric for assessing its engineering applicability. To test the model's adaptability across different SOC dynamic ranges, discharge data sequences with SOC ranging from 80% to 0% and from 60% to 0% were selected for experiments. Fig. 10 shows the estimation results of the model under different initial SOCs. It can be observed that regardless of whether the initial SOC is set to 80% or 60%, the predicted curves closely track the true SOC trend without noticeable bias drift. Fig. 11 further presents the corresponding estimation errors, which exhibit small fluctuations and maintain a low overall error level. Fig. 12 depicts the model's MAE and RMSE performance for both initial SOC conditions under varying ambient temperatures. The results indicate that with temperature changes, the error fluctuation range remains limited, maintaining a low error level overall, and the differences in errors between the two initial SOC conditions are insignificant. Specifically, for the discharge task from 80% SOC to 0%, the average MAE and RMSE are 0.79% and 0.96%, respectively; for the discharge task from 60% SOC to 0%, the average MAE and RMSE are 0.72% and 0.86%, respectively.

Secondly, considering that in practical battery monitoring systems, sensor faults, communication anomalies, or storage limitations may lead to temporal data loss, a periodic segment missing data experiment is designed to verify the model's robustness against incomplete data. Based on the original 7,378 time steps dataset, 100 consecutive time steps are removed every 1,000 time steps to simulate realistic scenarios of periodic communication interruption or sampling loss. Since periodic consecutive missing data may cause local accumulation and propagation of errors, the estimation performance of both SOC and terminal voltage are analyzed. Fig. 13 shows the SOC estimation curves, while Fig. 14 shows the terminal voltage estimation curves. Table 7 summarizes the comparison data of terminal voltage and SOC. The results demonstrate that even under partial data loss, the model can still accurately estimate the battery's state of charge, and it can partially adapt to trends before and after the missing segments without severe error accumulation.

## 5 Conclusion

In this study, a physics-informed deep learning model, termed PILNet, is proposed for accurate SOC estimation of lithium-ion batteries under complex operating conditions. The model integrates the long-sequence modeling capabilities of the Informer architecture with the strength of LSTM networks in second-order equivalent circuit parameter estimation, thereby achieving an effective fusion of data-driven and physics-based approaches. Additionally, a temperature-aware weighted loss mechanism is introduced to enhance the model's adaptability and estimation stability across various thermal environments.

Experimental evaluations across multiple temperatures and driving profiles demonstrate that PILNet consistently achieves high estimation

\begin{table}
\begin{tabular}{l c c c c c c} \hline \hline \multicolumn{1}{l}{Test dataset} & Temperature & PILNet & \multicolumn{3}{c}{MambalLihium} & \multicolumn{2}{c}{Informer-LSTM} \\ \cline{3-7}  & RMSE & MAE & RMSE & MAE & RMSE & MAE \\ \hline FUDS & 0 °C & 1.008 & 0.844 & 1.356 & 1.137 & 1.135 & 0.942 \\  & 10 °C & 1.220 & 0.901 & 1.372 & 1.098 & 1.495 & 1.077 \\  & 25 °C & 1.037 & 0.834 & 1.409 & 1.167 & 1.412 & 1.092 \\  & 30 °C & 0.867 & 0.727 & 1.468 & 1.228 & 1.195 & 0.898 \\  & 40 °C & 0.860 & 0.707 & 1.114 & 0.906 & 1.042 & 0.880 \\  & 50 °C & 0.850 & 0.678 & 1.208 & 1.008 & 0.938 & 0.775 \\ \hline
**Average** & & **0.974** & **0.782** & **1.321** & **1.091** & **1.203** & **0.944** \\ \hline \hline \end{tabular}
\end{table}
Table 5: Performance comparison of different models on FUDS dataset at various temperature (%).

\begin{table}
\begin{tabular}{l c c c c c c} \hline \hline \multicolumn{1}{l}{Temperature (°C)} & 0 & 10 & 25 & 30 & 40 & 50 \\ Optimal \(a\) & 0.3 & 0.7 & 0.2 & 0.1 & 0.4 & 0.1 \\ \hline \hline \end{tabular}
\end{table}
Table 6: Optimal values of loss weight coefficient \(a\) under different temperature conditions.

Figure 9: Effect of the loss weight coefficient \(a\) on SOC estimation accuracy under different temperatures.

accuracy, with an average MAE of 0.782% and RMSE of 0.974%, significantly outperforming several existing mainstream methods. Moreover, under scenarios with substantial initial SOC deviation, the model exhibits strong error correction capability and robustness, indicating its promising potential for real-world deployment.

It is worth noting, however, that SOC estimation accuracy is inherently influenced by the battery's state-of-health (SOH), particularly as the battery ages. Under extreme temperatures, severe degradation, or significant distribution shifts, the generalization ability of the model may still be challenged. To address these limitations, future research will focus on the integration of SOH estimation with SOC modeling, aiming to develop a unified health-state joint modeling framework. This direction is expected to improve the model's reliability and applicability under long-term degradation scenarios. In addition, efforts will be devoted to model compression and inference efficiency optimization, thereby enhancing its deployment feasibility and real-time performance on embedded or edge-computing platforms.

In summary, the proposed physics-guided deep neural network provides a novel technical pathway for achieving high-precision SOC estimation. PILNet is particularly suitable for application scenarios such as electric vehicles and energy storage systems, which are characterized by highly dynamic loads, frequent charge-discharge cycles, and fluctuating ambient temperatures. It effectively addresses the limitations of traditional methods such as the OCV technique and coulomb counting, which tend to suffer from cumulative errors and poor temperature adaptability under dynamic conditions. With low requirements on input data and strong engineering portability, the proposed method demonstrates excellent practical viability. Furthermore, the physics-informed design principles and model architecture of PILNet offer valuable insights for state estimation in other types of electrochemical energy storage devices, though further parameter adaptation and scenario-specific validation are necessary based on their respective electrochemical mechanisms.

\begin{table}
\begin{tabular}{l l l l l} \hline Condition & Terminal voltage & \multicolumn{3}{c}{SOC} \\ \cline{2-5}  & RMSE (V) & MAE (V) & RMSE (\%) & MAE (\%) \\ \hline No Missing Data & 0.062 & 0.039 & 1.037 & 0.834 \\ Periodic Missing Data & 0.064 & 0.040 & 1.112 & 0.879 \\ \hline \end{tabular}
\end{table}
Table 7: Estimation performance under normal and periodic missing data conditions.

Figure 11: Estimation error at 25 ‘C under different initial SOC conditions.

Figure 10: Estimation results at 25 ‘C under different initial SOC conditions.

### CRediT authorship contribution statement

**Yi Xie:** Writing - original draft, Visualization, Validation, Methodology, Investigation, Formal analysis, Data curation, Conceptualization. **Zhenqi Han:** Writing - review & editing, Validation, Supervision. **Jialu Zhang:** Writing - review & editing, Supervision, Project administration, Funding acquisition. **Lizhuang Liu:** Funding acquisition, Conceptualization.

### Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

### Data availability

The publicly available dataset used in this study can be accessed at the following link: [https://calec.umd.edu/battery-data](https://calec.umd.edu/battery-data).

## References

* (1) R. Li, H. Wang, H. Dai, J. Hong, G. Tong, X. Chen, Accurate state of charge prediction for real-world battery systems using a novel dual-dropout-based neural network, Energy 250 (2022) 1238853, [http://dx.doi.org/10.1016/j.energy.2022.123853](http://dx.doi.org/10.1016/j.energy.2022.123853).
* (2) Z. Wang, S. Wang, C. Yu, J. Qiao, Improved long short-term memory: Statistical regression model for high precision SOC estimation of lithium-ion batteries adaptive to complex current variation conditions, J. Electrochem. Soc. 170 (5) (2023) [http://dx.doi.org/10.1149/1945-7111/acce71](http://dx.doi.org/10.1149/1945-7111/acce71).
* (3) Y. Che, Z. Deng, X. Lin, L. Hu, X. Hu, Predictive battery health management with transfer learning and online model correction, IEEE Trans. Veh. Technol. 70 (2021) 1269-1277, [http://dx.doi.org/10.1109/TVT.2021.3055811](http://dx.doi.org/10.1109/TVT.2021.3055811).
* (4) J.-H. Lee, I.-S. Lee, Lithium battery SOM monitoring and SOC estimation algorithm based on the SOH result, Energies 14 (15) (2021) [http://dx.doi.org/10.3390/en141540506](http://dx.doi.org/10.3390/en141540506).
* (5) H. Zhang, Y. Bai, S. Yang, C. Li, State-of-charge prediction of lithium-ion batteries based on sparse autoencoder and gated recurrent unit neural network, Energy Technol. 11 (6) (2023).
* (6) M. Ull Hassan, S. Saha, M.E. Haque, S. Islam, A. Mahmud, N. Mendis, A comprehensive review of battery state of charge estimation techniques, Sustain. Energy Technol. Assess. 54 (2022) [http://dx.doi.org/10.1016/j.sena.2022.10201](http://dx.doi.org/10.1016/j.sena.2022.10201).
* (7) J. Tao, S. Wang, W. Cao, T. Pajayi-Ainshukwe, C. Fernandez, J.M. Guerrero, A comprehensive review of state-of-charge and state-of-health estimation for lithium-ion battery energy storage systems, locs 30 (10) (2024) 5903-5927, [http://dx.doi.org/10.1007/s11581-024-05686-z](http://dx.doi.org/10.1007/s11581-024-05686-z).
* (8) E. Alan, Y. Yass, A review on the battery state of charge estimation methods for electric vehicle battery management systems, in: 2019 11th International Conference on Electrical and Electronics Engineering (EECO 2010), Chamber Brief Engineers Bureau, Bursa Udug Univ, Dept Elect Elect Repn; Isaubal Tech Univ, Pace Elect Elect Repn; Engr; Isaubal Tech Univ, Pace Elect Elect Repn; Engr; Isaubal Tech. doi.org/10.2391/e05770.2019.8990643, 11th International Conference on Electrical and Electronics Engineering (EECO), BOX 20-30, Pittsburgh, Pittsburgh, 2007, New 28-30, 2019.
* (9) M.U. Ali, A. Zafar, S.H. Nengroso, S. Hussain, M.J. Ndi, H.-J. Kim, Towards a smarter battery management system for electric vehicle applications: A critical review of lithium-ion battery state of charge estimation, Energies 12 (3) (2019) [http://dx.doi.org/10.3390/en12030466](http://dx.doi.org/10.3390/en12030466).
* (10) M.R. Massim, W.A.W., Jamil, R.M. Sabri, State-of-charge (SOC) and state-of-health (SOH) estimation methods in battery management systems for electric vehicles, in: 2021 IEEE International Conference on Computing, ICOCO, IEEE Comp Soc, Malaysia Chapter, 2021, pp. 91-96, [http://dx.doi.org/10.1109/IOCOCO53166.2021.9673580](http://dx.doi.org/10.1109/IOCOCO53166.2021.9673580), IEEE International Conference on Computing (OOCO), Elect Elect Network, Nov 17-19, 2021.
* (11) M. Adalalappan, N. Subsimporuty, Modeling, state of charge estimation, and charging of lithium-ion battery in electric vehicle: A review, Int. J. Energy Res. 46 (3) (2022) 2141-2165, [http://dx.doi.org/10.1002/cr.7339](http://dx.doi.org/10.1002/cr.7339).

Fig. 14: Terminal voltage estimation under missing data condition at 25 \({}^{\circ}\)C.

Fig. 12: SOC estimation RMSE and MAE under different ambient temperatures and initial SOC values.

Fig. 13: SOC estimation under missing data conditions at 25 \({}^{\circ}\)C.

* [12] C. Fan, M.D. Higgins, W.D. Widanage, Real-time state of charge estimation of electrochemical model for lithium-ion battery, in 2019 IEEE Vehicle Power and Propulsion Conference, VPP, in: IEEE Vehicle Power and Propulsion Conference, IEEE; Bach KNC, CIT, Univ Tokyo, IEEE VNS, 2019, [http://dx.doi.org/10.1109/vpp2646532.2019.8952284](http://dx.doi.org/10.1109/vpp2646532.2019.8952284), 16th IEEE Vehicle Power and Propulsion Conference (VPPC), Hanod, Vietnam, ACM, 14-17, 2019.
* [13] J. Wang, J. Meng, O. Peng, T. Liu, X. Zeng, G. Chen, Y. Li, Lithium-ion battery state-of-charge estimation using electrochemical model with sensitive parameters adjustment, Batteries-Based 9 (3) (2023) [http://dx.doi.org/10.3390/b](http://dx.doi.org/10.3390/b) batteries9030180.
* [14] L. Wu, Z. Lyu, Z. Huang, C. Zhang, C. Wei, Physics-based battery SOC estimation methods: Recent advances and future perspectives, J. Energy Chem. 89 (2024) 27-40, [http://dx.doi.org/10.1016/j.jchem.2023.09.045](http://dx.doi.org/10.1016/j.jchem.2023.09.045).
* [15] H. Pang, J. Jin, L. Wu, F. Zhang, K. Liu, A comprehensive physics-based equivalent-circuit model and state of charge estimation for lithium-ion batteries, J. Electrochem. Soc. 168 (9) (2021) [http://dx.doi.org/10.1149/1945711/ac2701](http://dx.doi.org/10.1149/1945711/ac2701).
* [16] Y. Li, H. Qi, X. Shi, Q. Jian, F. Ian, J. Chen, A physico-based equivalent circuit model and state of charge estimation for lithium-ion batteries, Energies 17 (15) (2024) [http://dx.doi.org/10.3390/en17153782](http://dx.doi.org/10.3390/en17153782).
* [17] S. Cho, H. Jeong, G. Han, S. Jin, J.H. Lim, J. Oh, State-of-charge estimation for lithium-ion batteries under various operating conditions using an equivalent circuit model, Comput. Chem. Eng. 41 (2012) 1-9, [http://dx.doi.org/10.1016/j.compchemence.2012.02.003](http://dx.doi.org/10.1016/j.compchemence.2012.02.003).
* [18] Z. Tao, Z. Zhao, C. Wang, L. Huang, H. Jie, H. Li, Q. Hao, Y. Zhou, K.Y. See, State of charge estimation of lithium batteries: Review for equivalent circuit model methods, Measurement 236 (2024) [http://dx.doi.org/10.1016/j.measurement.2024.115148](http://dx.doi.org/10.1016/j.measurement.2024.115148).
* [19] H.M. Hussein, A. Aghammal, M.S. Abdelrahman, S.M.S.Hafafu, G. Mohammed, A review of battery state of charge estimation and management systems: Models and future prospective, Wiley Interdiscribel. Rev.-Energy Environ. 13 (1) (2024) [http://dx.doi.org/10.1002/wene.507](http://dx.doi.org/10.1002/wene.507).
* [20] A. Manoharan, K.M. Begam, V.R. Apawny, D. Sooriamoorthy, Artificial neural networks, gradient boosting and support vector machines for electric vehicle battery state estimation: A review, J. Energy Storage 55 (A) (2022) [http://dx.doi.org/10.1016/j.eis.2022.105384](http://dx.doi.org/10.1016/j.eis.2022.105384).
* [21] M. Stibezza, V. Bianchi, I. De Munari, FPGA implementation of an ant colony optimization based SST algorithm for state of charge estimation in li-ion batteries, Energies 14 (21) (2021) ([http://dx.doi.org/10.3390/en14217064](http://dx.doi.org/10.3390/en14217064).
* [22] J. Tian, R. Xiong, W. Shen, J. Lu, State-of-charge estimation of LiFePO4 batteries in electric vehicles: A deep-learning enabled approach, Appl. Energy 291 (2021) [https://dx.doi.org/10.1016/j.aepnery.2021.116812](https://dx.doi.org/10.1016/j.aepnery.2021.116812).
* [23] F. Yang, S. Zhang, H. Li, Q. Miao, State-of-charge estimation of lithium-ion batteries using lSTMA and UKP, Energy 201 (2020) [http://dx.doi.org/10.1016/j.energy.2020.117664](http://dx.doi.org/10.1016/j.energy.2020.117664).
* [24] J. Tian, R. Xiong, W. Shen, J. Lu, F. Sun, Flexible battery state of health and state of charge estimation using partial charging data and deep learning, Energy Storage Mater. 51 (2022) 372-381, [http://dx.doi.org/10.1016/j.enmin.2022.06.053](http://dx.doi.org/10.1016/j.enmin.2022.06.053).
* [25] D. Shi, J. Zhao, Z. Wang, H. Zhao, C. Eze, J. Wang, Y. Lian, A.F. Burke, Gaoud-based deep learning for co-estimation of battery state of charge and state of health, Energies 16 (9) (2023) [http://dx.doi.org/10.3390/en16093855](http://dx.doi.org/10.3390/en16093855).
* [26] Y. Yang, Y. Xu, Y. Nie, J. Li, S. Liu, L. Zhao, Q. Yu, C. Zhang, Deep transfer learning enables battery state of charge and state of health estimation, Energy 294 (2024) [http://dx.doi.org/10.1016/j.energy.2024.130779](http://dx.doi.org/10.1016/j.energy.2024.130779).
* [27] W. Sun, H. Xu, B. Zhou, Y. Guo, Y. Tang, W. Yao, Z. Yang, State-of-charge estimation of sodium ion batteries: A fusion deep learning approach, J. Energy Storage 91 (2024) [http://dx.doi.org/10.1016/j.estr.2024.111527](http://dx.doi.org/10.1016/j.estr.2024.111527).
* [28] K. Luo, X. Chen, H. Zheng, Z. Shi, A review of deep learning approach to predicting the state of health and state of charge of lithium-ion batteries, J. Energy Chem. 74 (2022) 159-173, [http://dx.doi.org/10.1016/j.jechem.2022.06.049](http://dx.doi.org/10.1016/j.jechem.2022.06.049).
* [29] M.S.H. Lipu, S. Ansari, M.S. Miah, S.T. Merry, K. Hassan, A.S.M. Shhawuddin, M.A. Hannam, K.M. Mottag, A. Hussain, Deep learning enabled state of charge, state of health and renaining useful life estimation for smart battery management system: Methods, implementations, issues and prospects, J. Energy Storage 55 (C) (2022) [http://dx.doi.org/10.1016/j.eis.2022.105752](http://dx.doi.org/10.1016/j.eis.2022.105752).
* [30] D. Zhang, C. Zhong, P. Xu, Y. Tian, Deep learning in the state of charge estimation for li-ion batteries of electric vehicles A review, Machines 10 (10) (2022) [http://dx.doi.org/10.3390/mollers100912](http://dx.doi.org/10.3390/mollers100912).
* [31] W. Mei, Z. Liu, C. Wang, C. Wu, Y. Liu, P. Liu, X. Xia, X. Xue, X. Han, J. Sun, G. Xiao, H.-Y. Tam, J. Albert, Q. Wang, T. Guo, Operando monitoring of thermal runaway in commercial lithium-ion cells via advanced lab-on fiber technologies, Nature Commun. 14 (2023) [http://dx.doi.org/10.1038/s/s4167-023-04995-3](http://dx.doi.org/10.1038/s/s4167-023-04995-3).
* [32] S. Sampathi, Y. Xin, Z.W. Tham, Y. Chen, L. Zhang, Real-time and non-contact estimation of state of charge for lithium-ion batteries using laser ultrasonics, J. Power Sources 605 (2024) [http://dx.doi.org/10.1016/j.powsonur.2024.234544](http://dx.doi.org/10.1016/j.powsonur.2024.234544).
* [33] F. Yang, Q. Mao, J. Zhang, G. Bao, K.W.E. Cheng, K.-H. Lam, Novel joint algorithm for state-of-charge estimation of rechargeable batteries based on the back propagation neural network combining ultrasonic inspection method, J. Energy Storage 99 (B) (2024) [http://dx.doi.org/10.1016/j.estr.2024.113391](http://dx.doi.org/10.1016/j.estr.2024.113391).
* [34] T. Tang, Q. Xia, M. Xu, Z. Deng, F. Jiang, Z. Yu, Y. Ren, D. Yang, C. Qian, Unveren internal SOC distribution estimation of lithium-ion batteries using ultrasonic transmission signals: A new data screening technique and an improved deep residual network, FERMIEUR, Transportation 24 (2025) [http://dx.doi.org/10.1016/j.eis.2025.100406](http://dx.doi.org/10.1016/j.eis.2025.100406).
* [35] H. Zhou, S. Zhang, J. Peng, S. Zhang, J. Li, H. Xiong, W. Zhang, Informer: Beyond efficient transformer for long sequence time-series forecasting, in: Thirty-Fifth AAAI Conference on Artificial Intelligence, Thirty-Third Conference on Innovative Applications of Artificial Intelligence and the Eleventh Symposium on Educational Advances in Artificial Intelligence, in AAAI Conference on Artificial Intelligence, vol. 35, 2021, pp. 11106-11115.
* [36] B. Xu, W. Zheng, R. Zhang, Z. Luo, Z. Sun, A novel observer for lithium-ion battery state of charge estimation in electric vehicles based on a second-order equivalent circuit model, Energies 10 (8) (2017) [http://dx.doi.org/10.3390/en10081150](http://dx.doi.org/10.3390/en10081150).
* [37] L. Zhang, H. Peng, Z. Ning, Z. Mu, C. Sun, Comparative research on RC equivalent circuit models for lithium-ion batteries of electric vehicles, Appl. Sci.-Based 7 (10) (2017) [http://dx.doi.org/10.3390/en/9710020](http://dx.doi.org/10.3390/en/9710020).
* [38] R. Zhang, R. Xia, B. Li, L. Cao, Y. Lai, W. Zheng, H. Wang, W. Wang, M. Wang, A study on the open circuit voltage and state of charge characterization of high capacity lithium-ion battery under different temperature, Energies 11 (9) (2018) [http://dx.doi.org/10.3390/en/1092048](http://dx.doi.org/10.3390/en/1092048).
* [39] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A.N. Gomez, L. Kaiser, I. Poloszhnin, Attention 8 in all you need, 2023, arXiv:1706.03762, URL [https://arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762).
* [40] Y. Xie, L. Liu, Z. Han, J. Zhang, MSCL-attention: A multi-scale convolutional long short-term memory (LSTM) attention network for predicting O2G emissions from vehicles, Sustainability 16 (919) (2020) [http://dx.doi.org/10.3390/en/10918957](http://dx.doi.org/10.3390/en/10918957).
* [41] M. Pecht, Battery data set, 2017, [https://calce.umd.edu/~battery-data](https://calce.umd.edu/~battery-data). (Accessed July).
* [42] G. Hunt, et al., USABC Electric Vehicle Battery Test Procedures Manual, United States Department of Energy, Washington, DC, USA, 1996.
* [43] Z. Shi, Marshall lithium: Selective state space model for remaining-useful life, state-of-health, and state-of-charge estimation of lithium-ion batteries, 2024, arXiv:2403.05430, URL [https://arxiv.org/abs/2403.05430](https://arxiv.org/abs/2403.05430).
* [44] K. Guo, Y. Zhu, Y. Zhong, K. Wu, F. Yang, An informed-LSTM network for state-of-charge estimation of lithium-ion batteries, in: 2023 Global Reliability and Prognostics and Health Management Conference, PHH-Hanghou, 2023, pp. 1-7, [http://dx.doi.org/10.1109/PHRI-Hanghou5879.2023.10482544](http://dx.doi.org/10.1109/PHRI-Hanghou5879.2023.10482544).