## Paper

Physical constraint-based LSTM for pipeline corrosion prediction

To cite this article: Fanjun Su _et al_2025 _Eng. Res. Express_**7** 045294

* Robust optimization of double pendulum mixed mass damper for vibration control of offshore platforms

Thi-y Pham, Xuan-Thuan Nguyen, Noc-An Tran et al.

- Simultaneous allocation of distributed generation and shunt capacitor using multi-objective momentum generation optimizer for technical and economic benefits

Sundry Adekie Salmon, Rekova Olago

Fairman, Olvansky Waski Adebj et al.

- Blockchain-covered healthcare system
- a systematic literature review

Monica Rey F and Priya G

## Abstract
The complex corrosion evolution of pipelines presents a significant challenge forintegrity management, astraditional physical models often fail in long-term prediction and purely data-driven methodsstrugglewith limited, noisy data. To addressthis, thisstudy proposes a novel hybrid physics-informed long short-term memory (PI-LSTM) network. The framework utilizes a physical model to capture the primary corrosion trend,while an LSTM istrained to learn the remaining nonlinearresiduals. To ensure physical plausibility, the model embeds constraints derived from the ordinary differential equation (ODE) governing corrosion kineticsinto the composite lossfunction.
The proposed PI-LSTM modelwas validated on field monitoring data and compared against
multiple benchmarks. The experimentalresults demonstrate itssuperior performance, achieving a mean Root Mean Square Error(RMSE) of 2.46 ± 0.28. Thisresult is not only more accurate than the traditionalVelázquez model(RMSE: 2.74) but also significantly surpasses other data-driven and time-series models.An ablation study further confirmed that the physical constraintwas crucial,improving both accuracy and stability overthe standard LSTM model(RMSE: 2.63 ± 0.51),with a 47% reduction in standard deviation highlighting its powerfulregularization effect. The superior performance across all evaluation metricsindicatesthat the proposed method has high prediction accuracy forthe dataset underinvestigation. While further validation on diverse datasetsisrequired to fully establish its generalizability, thisstudy demonstratesthat the hybrid, physics-informed
framework offers a promising and robust newapproach for pipeline corrosion research.

## 1 Introduction
Oil and gas pipeline is a key infrastructure forlong-distance transportation of natural gas, oil, and other energy sources. The safe and stable operation is directly related to national energy security and economic development.However, buried pipelines and gathering pipelines have been in complex service environmentsfor a long time, high temperature and high-pressureworking conditions, multiphase flow media,soil and transport medium.
This makes preventing pipeline corrosion challenging, especially the phenomenon of internal corrosion is more prominent.Among them, pitting corrosion isregarded as one of the most dangeroustypes of corrosion due to its hidden location,severe local corrosion, and fast perforation speed. Thisleadsto a continuous reduction in pipelinewall thickness, and ultimately leadsto leakage or even fracture. Once pipeline corrosion failure istriggered, itwill cause direct economic loss and environmental pollution, even cause serious accidents such as fires and explosions, threatening public safety. Therefore, it is critical to research technology that can precisely forecast the progression of pipeline corrosion.
Pipeline corrosion prediction haslong been of interest to many researchers, and various modelling methods have been developed. Traditional corrosion models mainly include empirical/semi-empirical models and mechanism-based models. Empirical/semi-empirical models attempt to establish a mathematicalrelationship between corrosion damage based on actual field measurements orlaboratory data using statistical analysis, etc Melchers _et al_[1] focuses on developing empirical models for predicting long-term localized corrosion of cast iron pipes buried in soils. The study proposes models based on field data collected from 67 sites over up to 129 years to understand the progression of corrosion depth in different soil types. Similarly, Zhao _et al_[2] developed a semi-empirical model for internal CO\({}_{2}\) corrosion of oil and gas pipelines, which correlated the corrosion rate with parameters by integrating laboratory experiments and field data, and the applicability of this model was verified in complex fluid environments. Such statistical and empirical-based models can provide practical predictive tools under specific conditions. However, their limitations are more obvious: the model form and parameters are typically highly empirical, making it difficult to fully capture the complex nonlinear dynamics of the corrosion process under the coupling of multi-physical fields; they frequently rely on a large amount of field data for parameter calibration; and the model's ability to extrapolate and adapt to changes in working conditions may be insufficient.

Recently, scholars have developed a series of nonlinear regression models using different corrosion data. Guo _et al_[3] applied FBN and an improved similarity aggregation method, combined with expert judgment and historical data, to assess the risk of storage tank accidents, especially for corrosion-induced leakage scenarios, and provided probabilistic reasoning and risk prioritization. Chen _et al_[4] developed a predictive model for shale gas pipeline internal corrosion probability by using BN in combination with common-cause failure analysis. Liu _et al_[5] extended the use of BN by proposing a fuzzy polymorphic Bayesian network (FPBN) for the reliability analysis of corrosion risk in submarine pipeline systems. The FPBN solves the problem of corrosion risk in submarine pipeline systems by introducing a multi-state fault tree and a fuzzy failure rate, which solves the uncertainty challenge caused by data scarcity and fault polymorphism.

Following the successful use of AI in the disciplines of structural dependability, safety, and risk assessment, researchers have begun to work on using AI methods to pipeline corrosion prediction [6]. Ossai _et al_[7] proposed a feed-forward subspace clustering neural network (SSCN) for prediction of pipeline corrosion defect depths (CDDs), and optimized the weighting parameter in the network using PSO, which significantly improved the accuracy of failure prediction of aging pipelines. In addition, Wang _et al_[8] proposed an SVR model combining grey processing and PSO optimization for predicting the internal corrosion rate of multi-phase flow pipelines. This improved the prediction accuracy by solving the data inhomogeneity problem through grey preprocessing. Similarly, Hatami _et al_[9] developed a hybrid model based on Least Squares Support Vector Machine (LSSVM) to predict CO\({}_{2}\) corrosion rates in the oil industry, demonstrating the applicability of SVM-like models in complex environments. Xiang _et al_[10] proposed the RPGM(1,1) prediction method, which uses PSO algorithm to optimize the background value of the gray model (GM) and greatly improves the accuracy of applying the GM(1,1) model to predict the depth of the pipeline corrosion setup. Despite the emergence of different pipeline corrosion prediction models, data scarcity, interference from complex sounds, and models' limited ability to characterize physical processes continue to be major barriers in this field of research. In the future, data-driven models [11] that combine physical knowledge with interpretable AI algorithms could deliver more reliable pipeline corrosion prediction solutions.

In recent years, Physically Informed Neural Networks (PINNs) [12] have provided an innovative framework for fusing data-driven and physical modeling. The core idea is to embed known physical laws in the form of soft or hard constraints into the structure or loss function of the neural network, thereby training models that fit the observed data and adhere to physical principles. Pipeline corrosion, as a dynamic process evolving, is closely related to its current and historical states. Long-short-term memory (LSTM) networks, a variant of recurrent neural networks, are good at capturing long-term dependencies in time series. This approach significantly improves the model's generalization ability, reduces reliance on large amounts of labeled data [13], and increases the physical confidence of the prediction results. This technique has substantial advantages for pipeline corrosion and mechanical property prediction [14]. The PI-LSTM framework increases pipeline corrosion prediction accuracy by inserting kinetic equations of corrosion reactions [15] and simulating the time-series evolution of corrosion depth using LSTM. This approach, which combines physical constraints with LSTM's time series modeling capability, creates a new paradigm for pipeline corrosion and mechanical property prediction that considers data fitting and physical consistency and is expected to significantly improve prediction accuracy and model credibility. In this research, this study presents a hybrid framework of PI-LSTM and applies it to the problem of pipeline corrosion prediction. This research systematically proves the superiority of the proposed method over regular LSTM and other benchmark models using particular case studies.

## 2 Theoretical basis

### Corrosion depth physical model

Most physical models for predicting pipeline corrosion depth are based on power-law models. Romanoff [16] presented a power law model for pipeline corrosion depth, as shown in equation (1), by studying the relationship between pipeline corrosion crater depth and exposure time.

\[\mathrm{d}_{\mathrm{max}}=\mathrm{kt}^{n} \tag{1}\]

The pipeline corrosion depth is influenced by the corrosion time, and environmental factors [17, 18]. Building upon the power law model, Velazquez _et al_[19] incorporated the pipeline corrosion initiation time as an unknown parameter into the model. They treated parameters and as linear combinations of variables representing environmental characteristics, which resulted in the improved power-law model shown in equation (2), here in after referred to as the Velazquez model.

\[\mathrm{d}_{\mathrm{max}}=\mathrm{k}(\mathrm{t}-\mathrm{t}_{0})^{n} \tag{2}\]

Although the Velazquez model and the power-law physical models it represents have achieved significant progress in describing and predicting corrosion behavior under specific conditions, they still possess certain inherent limitations.

The prediction accuracy of these models is highly dependent on the accurate estimation of parameters [20] and \(t_{0}\), which exhibit strong sensitivity in long-term corrosion trend prediction. Any minor deviation in the initial assessment can be significantly amplified as the prediction time extends, leading to increased cumulative error. Additionally, although the models incorporate environmental factors through regression coefficients, this linear combination approach may still struggle to fully capture the highly non-linear corrosion dynamics arising from multi-factor coupled interactions. More importantly, the determination of these parameters is often based on datasets from specific regions and periods. This limits the models' generalization capability, and their reliability may decrease, especially when long-term predictions are required or when applied to new scenarios where environmental conditions differ significantly from those during model construction.

To overcome these limitations, this paper proposes a transformation of the formulation of existing physical models. Instead of directly using algebraic equations that describe cumulative corrosion depth, the focus should shift towards a differential form that characterizes the dynamic evolution of the corrosion process. Specifically, The Velazquez model can be differentiated concerning time t, thereby obtaining the expression for the corrosion rate:

\[\frac{dd_{\mathrm{max}}}{dt}=\kappa\cdot\nu\cdot(t-t_{0})^{\nu-1} \tag{3}\]

### Lstm

Long Short-Term Memory (LSTM) [21] are a type of Recurrent Neural Network (RNN), which is designed to predict long-term dependencies in time-series data [22]. It effectively alleviates the vanishing or exploding gradient in traditional RNNs.

The core of LSTM is the cell structure, which comprises three key gating mechanisms: an input gate (\(i_{t}\)), a forget gate (\(f_{t}\)), and an output gate (\(o_{t}\)), along with a cell state (\(C_{t}\)).

The cell state (\(C_{t}\)) transmits information through the entire sequence processing chain. Information can be passed along this state without undergoing significant modification, thereby preserving long-term memory. The gating mechanisms are responsible for controlling the inflow, outflow, and forgetting of information within the cell state.

The forget gate (\(f_{t}\)) determines what information is to be discarded from the cell state. It examines the previous hidden state (\(h_{t-1}\)) and the current input (\(x_{t}\)) and outputs a value between 0 and 1 for each element of the previous cell state (\(C_{t-1}\)).

\[f_{t}=\sigma(W_{f}\cdot[h_{t-1},x_{t}]+b_{f}) \tag{4}\]

The input gate (\(i_{t}\)) determines what new information is to be stored in the cell state. It consists of two parts: a sigmoid layer, whose output (\(i_{t}\)) determines which values are to be updated, and a tanh layer that creates a vector of new candidate values (\(\vec{C}_{t}\)), which can subsequently be added to the cell state.

\[i_{t}=\sigma(W_{i}\cdot[h_{t-1},x_{t}]+b_{i}) \tag{5}\]

\[\vec{C}_{t}=\tanh\left(W_{C}\cdot[h_{t-1},x_{t}]+b_{C}\right) \tag{6}\]

The cell state is updated by multiplying the old cell state (\(C_{t-1}\)) by the forget gate (\(f_{t}\)), thereby discarding the information designated to be forgotten. Subsequently, the product is added, resulting in the new cell state (\(C_{t}\)).

\[C_{t}=f_{t}\odot C_{t-1}+i_{t}\odot\vec{C}_{t} \tag{7}\]

The output gate (\(o_{t}\)) determines what values to output. First, a sigmoid layer is run to decide which parts of the cell state will be output (the output of this layer is \(o_{t}\)). Then, the cell state is processed by a tanh function (e.g., passed through a tanh activation function), and this result is multiplied by the output of the output gate (\(o_{t}\)) to produce the final hidden state (\(h_{t}\)).

\[o_{t}=\sigma(W_{o}\cdot[h_{t-1},x_{t}]+b_{b}) \tag{8}\]

\[h_{t}=o_{t}\odot\tanh{(C_{t})} \tag{9}\]

Where \(\sigma\) is the sigmoid function, \(\tanh\) is the hyperbolic tangent function, \(W_{o}\) and \(b_{b}\) are the weight matrix and bias vector, respectively, and \(\odot\) denotes the element-wise product.

The complete structure and information flow of a single LSTM cell are illustrated in figure 1. LSTM receives a sequence input and updates its hidden state and cell state at each time step \(t\). The hidden state is typically used as the output for the current time step or to predict the input for the next time step. For sequence-to-sequence tasks, LSTM can generate an output sequence or \(\mathbf{Y^{\prime}}=(\mathbf{Y^{\prime}}_{t+1},...\mathbf{Y^{\prime}}_{t+k})\), where each (or \(\mathbf{y^{\prime}}_{t}\)) is computed based on \(h_{t}\).

## 3 Physical information fusion model

To enhance the physical consistency and predictive accuracy of the LSTM model, especially when dealing with limited and trend-heavy data, this study proposes a hybrid, physics-informed framework. The overall framework of the proposed physically informed LSTM model is shown in figure 2. The core idea is to decouple the prediction task: a deterministic physical trend model is first used to capture the primary, long-term corrosion progression, and the LSTM is then trained to learn the remaining complex, nonlinear residuals. The training process is guided by a composite loss function that synergizes data-driven accuracy with physical principles.

### Physical constraint embedding

The phenomenological corrosion kinetics model [23] is selected to describe the variation of corrosion depth with time \(t\). The corrosion rate is influenced by the current corrosion depth \(d(t)\), the environmental factor vector \(\mathbf{E}\), and some material or environment-related parameters \(\mathbf{p}\). This physical law can be expressed as an ordinary differential equation (ODE):

\[\frac{d(d(t))}{dt}=f(d(t),\,\mathbf{E},\,\mathbf{p};\,t) \tag{10}\]

While this general form acknowledges various influencing factors, the dataset used in this study only contains time-series measurements of corrosion depth. Therefore, this study simplify the physical constraint to enforce a fundamental principle derived from equation (10): the monotonic, cumulative nature of corrosion damage.

### Composite loss function for the Hybrid PI-LSTM

The training of the hybrid PI-LSTM is guided by a composite loss function that synergistically combines data-driven accuracy with physical principles. The total loss, \(L_{mult}\), is a weighted sum of two components: a data-fitting loss (\(L_{data}\)) and a physics-informed loss (\(L_{phy}\)).

Figure 1: Schematic of the LSTM cell structure.

\[L_{total}=\lambda_{data}\cdot L_{data}+\lambda_{phy}\cdot L_{phy} \tag{11}\]

Where \(\lambda_{data}\), \(\lambda_{phy}\), and are the weighting coefficients for the respective loss terms. \(\lambda_{data}\) is implicitly set to 1.0 to prioritize fitting the observational data. \(\lambda_{phy}\) is adaptive. Its base weight is set to 0.05. This study designed a phased weighting scheme: during early corrosion, weights are halved to 0.025, granting the model greater flexibility; during mid-stage corrosion, weights revert to the baseline value of 0.05; and during late-stage corrosion, weights are doubled to 0.10 to strongly constrain the model's long-term behavior, ensuring its physical smoothness and stability. In this hybrid, residual-learning framework, an explicit initial condition loss term (\(L_{k/i}\)) is not required, the model's task is to predict the subsequent residual \(r(t_{i})\) based on the historical sequence \([r(t_{i-1}),...,r(t_{i-1})]\), where \(L\) is the sequence length. This mechanism inherently grounds the model's predictions in the observed starting conditions of the process, making a separate, explicit loss term for \(t_{init}\) and \(d_{init}\) redundant.

### Definition of loss terms

The primary objective of the LSTM in this hybrid framework is to accurately predict the residuals between the physical trend model (Velzquez) and the observed data. Therefore, the data-fitting loss measures the Mean Squared Error (MSE) between the LSTM's predicted residual, \(\hat{r}(t_{i})\), and the true calculated residual, \(r(t_{i})\), across all \(N_{data}\) points in a training batch.

\[L_{data}=\frac{1}{N_{data}}\sum_{i=1}^{N_{data}}\left(\hat{r}(t_{i})-r(t_{i}) \right)^{2} \tag{12}\]

This term enforces physical plausibility on the model's final, combined prediction. This research use a finite-difference approximation to ensure the monotonic, cumulative nature of corrosion is respected. The physics loss [24] is formulated to penalize any instance where the total predicted corrosion depth at time step \(t_{i}\) is less than the depth at the preceding step \(t_{i-1}\).

\[L_{phy}=\frac{1}{N_{batch}}\sum_{i=1}^{N_{batch}}\mathrm{ReLU}(-\Delta d_{i}) \tag{13}\]

To impose physical constraint, this study adopted a finite-difference approximation strategy, which is well-suited for the discrete and non-uniformly sampled nature of industrial data. The constraint is applied to the final combined prediction, which is the sum of the output from the physical trend model and the LSTM's correction of the residual. During the loss function computation for each training sequence, the time derivative is approximated by the difference \(\Delta d=d_{pred}(t_{i})-d_{pred}(t_{i-1})\) between the model's total predicted corrosion depth at the final time point \(t_{i}\); and the preceding time point \(t_{i-1}\). The physical loss term, \(L_{phy}\), then penalizes any instance where this difference is negative (\(\Delta d<0\)), thereby effectively enforcing the physical law of monotonically increasing corrosion at discrete time steps determined by the variable measurement intervals in the dataset.

This study employed the Adam optimizer to train all LSTM models. The Adam optimizer [25] is widely adopted for its efficiency and robustness in handling deep learning models. The initial learning rate was set to 0.002. Additionally, to enable finer-grained adjustments during the later stages of training, this study integrated

Figure 2: Framework of the proposed PL-LSTM model.

a learning rate scheduler, which multiplies the learning rate by a decay factor of 0.7 after every 500 training epochs [26]. The complete hyperparameter configuration is detailed in table 1.

## 4 Experimental studies

### Dataset description

The data for this study were sourced from field monitoring of internal corrosion on the Tiangao pipeline of Chongqing Gas Mine. The pipeline is a total length of 22.7 km. The pipeline material is L245NCS steel, with a specification of \(\Phi\)273 \(\times\) 11 mm. This steel grade is specifically designed for sour service applications, which is consistent with Carbon (C) content of 0.26%, Silicon (Si) up to 0.45%, and Manganese (Mn) up to 1.15%. Both Phosphorus (P) and Sulfur (S) have a maximum allowable content of 0.030%. Microalloying elements such as Niobium (Nb), Vanadium (V), and Titanium (Ti) are controlled at maximum levels of 0.05%, 0.05%, and 0.04% respectively, with their combined total not exceeding 0.15%.

The transported medium contains hydrogen sulfide (H\({}_{3}\)S) at a concentration of 70.02 g m\({}^{-3}\). The external anti-corrosion coating consists of a three-layer polyethylene (PE) system of ordinary grade.

To monitor the internal corrosion status of pipelines, an electrical resistance (ER) probe monitoring device was installed at the pipeline. The device is positioned at the 12 o'clock orientation on the top of the pipeline, flush with the inner pipe wall. Corrosion data were periodically recorded and remotely transmitted for storage using an MS3510E data acquisition unit. This study collected a total of 56 sets of corrosion monitoring data from this monitoring point, spanning from June 2011 to September 2019, covering a period of 8.25 years. The monitoring location on the natural gas gathering pipeline and the corrosion measurement setup are depicted in figure 3.

For training and evaluating the models, the dataset was divided chronologically to simulate a real-world forecasting scenario. The first 70% of the data points (corresponding to the earlier time measurements) were used as the training set. The remaining 30% of the data points (corresponding to the later time measurements) were reserved as the test set for the final performance evaluation. This strict temporal partitioning ensures that the models are evaluated on their ability to extrapolate and predict future corrosion states based solely on historical data, which mirrors the practical application of such a predictive tool in pipeline integrity management.

### Evaluation indicators

Root Mean Square Error (RMSE), Mean Absolute Error (MAE), and Mean Absolute Percentage Error (MAPE) were employed to evaluate the prediction performance and physical consistency of the models on the test set.

\[RMSE=\sqrt{\frac{1}{N}{\sum_{i=1}^{N}}(\hat{y_{i}}-\hat{y_{i}})^{2}} \tag{14}\]

\[MAE=\frac{1}{N}{\sum_{i=1}^{N}}|\hat{y_{i}}-\hat{y_{i}}| \tag{15}\]

\[MAPE=\frac{1}{N}{\sum_{i=1}^{N}}\left|\begin{array}{c}\hat{y_{i}}-\hat{y_{ i}}\\ \hline\hat{y_{i}}\end{array}\right|\times\,100\% \tag{16}\]

Where \(\hat{y_{i}}\) is the predicted value, \(\hat{y_{i}}\) is the true value, and \(N\) is the number of test samples. Smaller values for these three metrics indicate a better model fit and superior performance.

\begin{table}
\begin{tabular}{l l l} \hline Parameter & Value & Description \\ \hline LSTM Input Dimension & 1 & The model learns from a one-dimensional time series of residuals. \\ LSTM Hidden Units & 32 & The number of neurons in each LSTM layer. \\ LSTM Layers & 2 & The number of stacked LSTM layers. \\ Dropout Rate & 0.1 & Applied between LSTM layers to prevent overfitting. \\ Optimizer & Adam & A standard and robust optimizer for training deep neural networks. \\ Initial Learning Rate & 0.002 & The initial step size is used by the Adam optimizer. \\ Learning Rate Scheduler & Stepl-IR & The learning rate is multiplied by a decay factor of 0.7 every 500 epochs. \\ Epochs & 2500 & The total number of full passes through the entire training dataset. \\ Batch Size & 8 & The number of training sequences utilized in one iteration. \\ Sequence Length & 7 & The number of historical data points used to predict the next step. \\ \hline \end{tabular}
\end{table}
Table 1: PI-LSTM model hyperparameter configuration.

### Experimental results and analysis

To comprehensively evaluate the performance of the proposed Physically Constrained Long Short-Term Memory Network (PI-LSTM), This study rigorously compared it against a series of baseline models on a real-world pipeline corrosion monitoring dataset. All random models (LSTM, PI-LSTM) were run independently 10 times. This study reports the mean and standard deviation of their performance metrics to evaluate their average performance and stability. The quantitative results of the experiments are summarized in table 1, and visual comparisons are presented in figures 4-5.

#### 4.3.1 Quantitative performance analysis

The comprehensive performance metrics for all models, aggregated over 10 independent runs for stochastic methods, are presented in table 2. The data reveals that the proposed Physics LSTM (PI-LSTM) model achieves the optimal average performance across all three core evaluation metrics, with a Root Mean Square Error (RMSE) of \(2.46\pm 0.28\,\mathrm{\SIUnitSymbolMicro m}\), a Mean Absolute Error (MAE) of \(1.98\pm 0.30\,\mathrm{\SIUnitSymbolMicro m}\), and a Mean Absolute Percentage Error (MAPE) of \(2.14\pm 0.31\,\mathrm{\SIUnitSymbolMicro m}\). This result strongly demonstrates the superiority of the proposed method.

Both the LSTM and the PI-LSTM models significantly outperform traditional grey models (GM (1,1), RPGM (1,1)) and Gaussian Process Regression (GPR). The latter models performed poorly in the long-term extrapolation task, exhibiting RMSE values as high as 23-71, which indicates their failure to capture the critical dynamics of the accelerating corrosion trend present in the data.

To quantify the specific contribution of the physical constraint, an ablation study was conducted by comparing the PI-LSTM model against the unconstrained LSTM model. The results clearly demonstrate the value of this component in two critical aspects. First, it improves prediction accuracy, with the PI-LSTM outperforming the LSTM across all metrics, achieving an average RMSE reduction of approximately 6.5%. Second, it significantly enhances model stability. The standard deviation of the RMSE for the PI-LSTM was 0.28, a remarkable 47% reduction compared to the LSTM's standard deviation of 0.51. This conclusively demonstrates that the physical constraint acts as an effective regularizer, guiding the model toward a more stable and physically consistent solution space, thereby markedly improving its reliability.

Finally, the analysis provides a deeper insight when comparing the PI-LSTM to the specialized Velazquez physical model. The Velazquez model demonstrated excellent performance (RMSE: 2.74), suggesting the data-set follows a strong power-law growth trend. The fact that the proposed PI-LSTM model achieves even higher accuracy on this basis is significant.

#### 4.3.2 Visualization results analysis

The advantages of quantitative indicators are visually demonstrated in the predictive chart (figures 4-5).

Figure 3: Natural gas gathering pipeline corrosion monitoring.

In figure 4, the Physics LSTM prediction curve most closely aligns with the trajectory of the actual data, successfully predicting the trend of accelerated corrosion during the test phase. In contrast, while the LSTM curve exhibits the correct trend, it shows slight deviation, whereas other benchmark models demonstrate significant divergence.

In figure 6, the Physics LSTM data points cluster most tightly around the ideal diagonal line, indicating the lowest deviation and highest accuracy in its predictions.

In figure 5, the Physics LSTM's relative error curve consistently maintains the lowest value among all models throughout the entire testing period, with minimal fluctuations. This further confirms its high prediction, accuracy and stability.

In summary, whether evaluated by quantitative performance metrics or visual prediction results, the proposed Physics LSTM model demonstrates state-of-the-art performance, proving the effectiveness and superiority of this approach in addressing such industrial time series forecasting problems [27].

Figure 4: Prediction results of PF-LSTM compared with baseline models.

Figure 5: Comparison of relative prediction errors amongmodels.

### Discussion

The experimental results offer several critical insights into the application of hybrid, physics-informed deep learning models for pipeline corrosion prediction.

First, the findings clearly reveal the superiority of the hybrid modeling strategy. Traditional data-driven (GPR) and time-series models (GM (1,1), RPGM (1,1)) demonstrated significant limitations in the long-term extrapolation of the strong corrosion trend present in the data.

This indicates that for degradation processes governed by distinct physical laws, relying solely on historical pattern mining is insufficient for reliable forecasting [28]. The proposed hybrid framework, which decouples the primary physical trend using the Velazquez model and employs an LSTM to learn the nonlinear residuals, effectively overcomes this challenge. The superior performance of the LSTM and PI-LSTM models validates this 'physics-trend and residual-learning' approach as a robust paradigm for such engineering problems.

Second, a key contribution of this work, quantified through the ablation study, is the demonstration of the dual role of the physical constraint. The constraint not only improves prediction accuracy by acting as a regularizer that guides the model towards physically plausible solutions [29], but it also significantly enhances model stability and reliability. As shown in table 1, the standard deviation of the RMSE for the PI-LSTM (0.28) was nearly 47% lower than that of the unconstrained LSTM (0.51). For risk-sensitive industrial decision-making, this enhanced stability is paramount, as it signifies a more dependable and consistent prediction model.

\begin{table}
\begin{tabular}{l c c c} \hline \hline Model & RMSE (\(\mu\)m) & MAE (\(\mu\)m) & MAPE (\%) \\ \hline PhysicsLSTM & \(2.46\pm 0.28\) & \(1.98\pm 0.30\) & \(2.14\pm 0.31\) \\ LSTM & \(2.63\pm 0.51\) & \(2.09\pm 0.47\) & \(2.31\pm 0.49\) \\ Velázquez & 2.74 & 2.14 & 2.27 \\ RPGM(1,1) & 23.16 & 20.91 & 22.38 \\ GM(1,1) & 26.81 & 24.56 & 26.38 \\ GPR & 70.88 & 58.06 & 60.74 \\ \hline \hline \end{tabular}
\end{table}
Table 2: Comparison of performance metrics across different models on the test set.

Figure 6: Scatter plot of PI-LSTM predicted values versus actual values.

Furthermore, the highly competitive performance of the Velazquez physical model is an insightful finding. It suggests that the corrosion process at this specific monitoring point follows highly regular, power-law behavior. In this context, the ability of the PI-LSTM to further reduce the prediction error highlights its advanced capability: it not only captures the primary physical trend but also accurately models the subtle, real-world fluctuations that a pure physical formula cannot describe. This suggests greater generalization potential for the PI-LSTM. In more complex industrial scenarios [30] with higher noise or varying operational conditions, where a simple physical model would likely fail, the LSTM's capacity to learn complex residuals would become even more critical, making the PI-LSTM a more robust and adaptable solution.

Finally, the limitations of this study illuminate directions for future research [31]. The model's validation on data from a single probe, while successful, necessitates further testing on more diverse datasets from different pipelines and environments to fully establish its generalizability.

## 5 Conclusion

This study addressed the significant challenge of long-term internal corrosion prediction for pipelines, particularly under conditions of limited and trend-heavy monitoring data. A novel hybrid, physics-informed long short-term memory (PI-LSTM) network was proposed and validated. The framework effectively decouples the prediction task by using a physical model to capture the primary corrosion trend, while an LSTM is trained to learn and correct the remaining nonlinear residuals.

The main findings and contributions of this work are as follows:

1. The proposed hybrid PI-LSTM model demonstrated state-of-the-art performance on a real-world industrial dataset, achieving the lowest prediction error (mean RMSE of \(2.46\pm 0.28\)) among all tested benchmarks, including traditional physical, time-series, and standard data-driven models.
2. A key contribution, confirmed via a rigorous ablation study, is the demonstration of the dual role of the physical constraint. It was quantitatively proven that the physics-informed loss term not only improves the model's prediction accuracy but also acts as a powerful regularizer that significantly enhances model stability and reliability, reducing performance variance by nearly 47%.
3. The study highlights the superiority of the hybrid modeling paradigm. The model's ability to outperform even the highly accurate Velazquez physical model indicates its advanced capability to capture both the primary degradation trend and the subtle, real-world fluctuations that purely physical formulas cannot describe, suggesting strong generalization potential.

Despite the positive results, this study has limitations that illuminate clear directions for future research. A primary limitation is the validation on a single-probe dataset; further testing on diverse datasets is needed to fully establish generalizability. Future work should also prioritize the following:

1. For practical risk management, quantifying prediction confidence is crucial. Future work should integrate uncertainty quantification (UQ) techniques, such as Monte Carlo Dropout or model assembling, to provide probabilistic forecasts and confidence intervals, significantly enhancing the model's value for industrial decision-making.
2. Acquiring richer datasets that include synchronous environmental parameters would allow for their integration as input features, potentially enhancing the model's accuracy and interpretability.

In conclusion, this study provides strong evidence that the proposed hybrid, physics-informed framework offers a promising and robust new approach for pipeline corrosion research, providing a more accurate and reliable tool for enhancing pipeline integrity management.

## Data availability statement

The data cannot be made publicly available upon publication because no suitable repository exists for hosting data in this field of study. The data that support the findings of this study are available upon reasonable request from the authors.

## References

* (1)
* R. E. Petersen R. B and Wells T. 2019 Empirical models for long-term localised corrosion of cast iron pipes buried in soils _Gorros. Eng. Sci. Technol._ 54 678-87
* (2) Zhao L, Yan Y and Yan X. 2021 A semi-empirical model for CO2 erosion-corrosion of carbon steel pipelines in wet gas-solid flow _J. Pet. Sci. Eng._ 196 107992
* (3) Guo X. Ji, Khan F, Ding L and Yang Y. 2021 Fuzzy Bayesian network based on an improved similarity aggregation method for risk assessment of storage tank accident _Process Saf. Environ. Prot._ 149 817-30
* (4) Chen K _et al_. 2022 Risk classification of shale gas gathering and transportation pipelines running through high consequence areas _Process_ 10 923
* (5) Liu C _et al_. 2025 Reliability analysis of subsea pipeline system based on fuzzy polymorphic bayesian network _Sci. Rep._ 15 11523
* (6) Seglier M E A B, Keshtegar B, Taleb-Berrouane M, Abbassi R and Trung N-T 2021 Advanced intelligence frameworks for predicting maximum pitting corrosion depth in oil and gas pipelines _Process Saf. Environ. Prot._ 147 818-33
* (7) Ossai C 12020 Corrosion defect modelling of aged pipelines with a feed-forward multi-layer neural network for leak and burst failure estimation _Eng. Fail. Anal._ 110 104397
* (8) Wang P and Quan Q 2019 Prediction of corrosion rate in submarine multiphase flow pipeline based on PSO-SVM model _IOP Conf. Ser. Mater. Sci. Eng._ 688 40145
* (9) Hatami S, Schaeri-Ardakani A, Niknejad-Khomami M, Karimi-Malekabadi F, Rasaei M R and Mohammadi A H 2016 On the prediction of CO2 corrosion in petroleum industry _J. Supercrit. Fluids_ 117 108-12
* Protection_ 41 18-22
* (11) Li X, Zhang L, Khan F and Han Z 2021 A data-driven corrosion prediction model to support digitization of subsea operations _Process Saf. Environ. Prot._ 153 413-21
* (12) Zhang C and Shidezadeh A. 2023 Nested physics-informed neural network for analysis of transient flows in natural gas pipelines _Eng. Appl. Artif. Intell._ 122 106073
* (13) Stewart M G and Al-Harty A 2008 Fitting corrosion and structural reliability of corroding RC structures: Experimental data and probabilistic analysis _Reliab. Eng. Syst. Saf._ 93 373-82
* (14) Yang Y and Perdkaris P 2019 Conditional deep surrogate models for stochastic, high-dimensional, and multi-fidelity systems _Comput. Mech._ 64 417-34
* (15) Dourado A and Viana F A C 2019 Physics-informed neural networks for corrosion-fatigue prognosis _Proc. Annu. Conf. PHM Society_ 1184 1184
* (16) Romanoff M 1957 _Underground Corrosion_ 579 (US Government Printing Office)
* (17) Mughabghab S F and Sullivan T M 1989 Evaluation of the pitting corrosion of carbon steels and other ferrous metals in soil systems _Water Manag_ 9 239-51
* (18) Kim C, Chen L, Wang H and Castaneda H 2021 Global and local parameters for characterizing and modeling external corrosion in underground coated steel pipelines: a review of critical factors _J. Pipeline Sci. Eng._ 117-35
* (19) Velzquez J C, Calcey F, Valor A and Hallen J M 2009 Predictive model for pitting corrosion in buried oil and gas pipelines _Corrosion_ 65 332-42
* (20) Turnbull A, McCartney L N and Zhou S 2008 A model to predict the evolution of pitting corrosion and the pit-to-crack transition incorporating statistically distributed input parameters _Environment-Induced Cracking of Materials_ ed S A Shipilov, R H Jones, J-M Miow and R B Rekus (Elsevier) 19-45
* (21) Gers F A, Schmidhuber J and Cummins F 1999 Learning to forget: continual prediction with LSTM, _Ninth International Conference on Artificial Neural Networks ICANN 99. (Conf. Publ. No. 470) (Edinburgh, UK)_ 850-52
* (22) Agarwal M, Mahalan G, Shrotris A and Sh Shch