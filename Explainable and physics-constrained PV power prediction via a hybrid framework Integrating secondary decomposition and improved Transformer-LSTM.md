

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the Energy journal](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the Energy journal

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Explainable and physics-constrained PV power prediction via a hybrid framework Integrating secondary decomposition and improved Transformer-LSTM

Jiahao Zou, Zhaocai Wang<sup>\*</sup> ![ORCID icon](17413706fd4997a1a4bdf85c6864eee1_img.jpg), Zhaoyang Zhu, Zuowen Tan ![ORCID icon](f419710cbe076aa30a9c6c031b5cbe84_img.jpg)

College of Information, Shanghai Ocean University, Shanghai, 201306, China

## ARTICLE INFO

### Keywords:

PV power prediction  
Secondary decomposition  
Dreaming optimization algorithm  
Physical constraints  
Deep learning

## ABSTRACT

Photovoltaic power generation (PVPG) is susceptible to meteorological conditions, exhibiting significant randomness and volatility. Therefore, accurate and reliable PVPG prediction is crucial for enhancing grid stability. However, existing data-driven prediction methods often overlook the system's inherent physical mechanism, which can lead to prediction results that violate actual operating laws. This study presents a physics-constrained hybrid model, integrating Transformer and Long Short-Term Memory (LSTM) networks with a secondary decomposition strategy, for the multi-step short-term forecasting of PVPG. Initially, a Seasonal and Trend Decomposition using Loess (STL) method is utilized to decompose the original dataset. Subsequently, variational mode decomposition (VMD), optimized by an improved Dream Optimization Algorithm (DOA), is utilized to decompose the residual term. Subsequently, the decomposed components and the screened features are fed into a hybrid Transformer-LSTM model, with its hyperparameter optimized by an improved Dream Optimization Algorithm, to complete the final power prediction. To ensure the predictions adhere to the physical principles of photovoltaic power generation, the model utilizes a designed physics-constrained loss function specifically. On the Australian dataset, the proposed model is evaluated and is observed to achieve better performance than other methods in both prediction accuracy and robustness. Specifically, on Site 1, the R-squared and RMSE for the overall prediction performance are 0.9423 and 0.2326, respectively, demonstrating superior prediction performance. Moreover, it also exhibits superior prediction capability across different datasets, seasons, and weather conditions. Finally, explainability analysis was conducted using SHAP method. This multi-step short-term PVPG prediction method has the potential to enhance grid stability and the stable regulation of energy.

## 1. Introduction

In response to the depletion of fossil fuels and environmental pollution, the global energy structure is undergoing a transformation. Renewable energy sources have garnered widespread attention, with solar energy being extensively utilized due to its cleanliness and abundance. Photovoltaic power generation (PVPG), characterized by its renewable and clean attributes, is highly valued and has emerged as a strategic alternative to fossil fuels [1]. However, photovoltaic power generation systems are susceptible to the random fluctuations inherent in meteorological conditions, leading to fluctuations in power output [2], which in turn adversely affects the normal operation of the power grid system. Consequently, accurately predicting photovoltaic power

output and mitigating the impact of photovoltaic power generation on the power grid system have become critical issues in the field of PVPG [3].

According to the time horizon, photovoltaic forecasting can be defined according to three categories, encompassing short-term, medium-term, and long-term forecasting [4]. Short-term forecasting generally encompasses a timeframe of less than one day and is used for intraday real-time scheduling of photovoltaic power stations. Medium-term forecasting spans from one day to several weeks [5] and is primarily used for weekly operation arrangement and operation and maintenance plans of the power grid. Long-term forecasting, which is primarily used for strategic planning and decision-making, generally spans several months to years [6]. In addition, photovoltaic power

\* Corresponding author.

E-mail address: [zcwang@shou.edu.cn](mailto:zcwang@shou.edu.cn) (Z. Wang).

generation forecasting methods encompass five categories: physical, statistical, machine learning and deep learning, and hybrid model approaches [7].

Physical methods involve a complex modeling process that uses mathematical calculations to characterize the dynamic changes and physical states of the weather, but they often exhibit poor predictive performance in complex and variable weather scenarios [8]. Statistical methods predict the output of PVPG based on historical time series data, such as exponential smoothing [9] and regression analysis. Despite their simplicity and computational efficiency, these models have difficulty handling the inherently non-linear and non-stationary nature of photovoltaic power generation [10]. With technological advancements, machine learning and deep learning have been shown to be more efficacious than physical and statistical methods in non-linear approximation, leading to their widespread application in the field of photovoltaic power generation. Machine learning models include support vector machines [11] and decision trees. Deep learning models include long short-term memory (LSTM) [12], Transformer [13], and convolutional neural networks (CNN) [14]. Deep learning can extract nonlinear and complex features and has strong generalization ability. LSTM is a variant of recurrent neural network (RNN), which successfully mitigates the challenges of vanishing and exploding gradients. Wang et al. [15] proposed an improved LSTM network model based on bayesian optimization (BO) to design hyperparameters, which are used to predict sub-sequences at different time scales.

In photovoltaic power generation forecasting, single models have limitations, primarily due to their inadequate modeling capability for complex nonlinearities and a noticeable lack of generalization ability in complex and variable scenarios. Therefore, constructing a hybrid model that combines various advantageous techniques is a feasible and highly effective approach. Agga et al. [16] introduced a hybrid CNN-LSTM framework and compared it with several models. Zhang et al. [17] presented a model based on similar day clustering and a combination of a temporal convolutional network (TCN) and a bidirectional LSTM network (BiLSTM), which demonstrates a better understanding of the seasonality, periodicity, and irregularities in the data. Rai et al. [18] introduced a differential attention network built upon the CNN-BiLSTM model and tested it on two different data sets. Liu et al. [19] introduced a regional photovoltaic power prediction model using an improved temporal dense encoder and graph attention network (ITDE-GAT). Studies based on two data sets have demonstrated that the model attains higher prediction accuracy and stronger generalization ability. Wang et al. [20] presented a method for selecting an appropriate machine learning model based on weather type classification, and experiments demonstrated that its performance is superior to other comparative models.

Signal decomposition methods significantly improve the power forecast accuracy of photovoltaic power generation by breaking down complex signals into simpler, more physically meaningful sub-components. Commonly used approaches comprise variational mode decomposition (VMD) [21], empirical mode decomposition (EMD) [22], and complete ensemble empirical mode decomposition (CEEMD) [23]. Lin et al. [24] proposed a novel short-term photovoltaic power prediction model that integrates complete ensemble empirical mode decomposition with adaptive noise (CEEMDAN) to decompose historical data signals and introduces a temporal self-attention mechanism with a gated recurrent unit (GRU) as an encoder, demonstrating excellent performance on the data set. Wang et al. [25] presented an improved variational mode decomposition for data decomposition in modeling, followed by a novel context-embedding causal convolutional Transformer architecture to predict each sub-sequence, evaluating the model's performance across different seasons. Liu et al. [26] developed a selection method for analogous days while using wavelet packet decomposition to decompose the original photovoltaic power and reconstruct it into a series of sub-signals, using similar day signals as the network input GRU model for prediction. Liu et al. [27] used VMD, CEEMD, and singular spectrum analysis (SSA) to decompose the initial data and then

input it into a parallel BiLSTM-CNN model for forecasting.

The hyperparameter configuration of signal decomposition and hybrid models has a significant impact on model performance. An appropriate hyperparameter setting can substantially enhance the prediction accuracy and generalization capability of photovoltaic power generation forecasting models. However, traditional hyperparameter tuning methods exhibit notable limitations. For instance, manual tuning heavily relies on domain expertise and trial-and-error, resulting in low efficiency, while grid search incurs high computational costs and is prone to local optima. Heuristic algorithms offer an effective solution to these challenges, including genetic algorithm (GA) [28], particle swarm optimization (PSO), and whale optimization algorithm (WOA). Zhen et al. [28] employed GA to tune the hyperparameters of a BiLSTM, which demonstrated superior prediction accuracy compared to other models. Chen et al. [29] employed an improved PSO algorithm to optimize the hyperparameters of VMD and Kernel Extreme Learning Machine (KELM). Tang et al. [30] utilized the Fox Optimization Algorithm (FOX) to optimize the hyperparameters of CEEMDAN, effectively addressing the problem of mode mixing and enhancing the decomposition accuracy of Intrinsic Mode Functions (IMFs). Sun et al. [31] tackled the challenge of model parameter configuration, which significantly affects prediction accuracy, by applying a Modified Archimedes Optimization Algorithm (MAOA) to fine-tune the hyperparameters of their multi-channel LSTM model.

In summary, substantial advancements have been made in the research on photovoltaic power prediction; however, there are still some shortcomings, as follows: (1) Many hybrid deep learning models rely on fixed network structures when extracting sequential features and cannot dynamically adjust the importance weights between different time steps or variables. This makes such models prone to ignoring key historical trends or global context when facing rapid changes in meteorological conditions or long-term dependencies during PV power prediction, resulting in weak generalization ability and robustness under complex scenarios. (2) Most data decomposition methods applied in previous research are single decomposition methods, which tend to cause problems of mode mixing and residual component information retention. This leads to the loss of the physical meaning of modes or incomplete decomposition, resulting in ambiguous physical meaning of modes and insufficiently thorough decomposition. (3) The hyperparameter settings of current models are often based on empirical manual selection or use grid search and random search. These methods have high computational costs and cannot perform effective searches in high-dimensional parameter spaces. (4) Most of the existing PV power prediction models are purely data-driven and ignore the physical laws of PV power generation. This causes the models to possibly produce prediction results that do not conform to physical common sense, and these unreasonable predictions may seriously affect the reliability and availability of the models in actual power dispatching.

To overcome the shortcomings identified above, this study proposes a physics-constrained hybrid forecasting model based on the optimization of secondary decomposition and Transformer-LSTM by the Dreamer Optimization Algorithm (DOA) [32]. The model is compared against various models on two datasets from Australia, and its generalization capability is investigated. The primary contributions in this research are outlined below:

- (1) A secondary decomposition strategy, which utilizes Seasonal and Trend Decomposition using Loess (STL) and VMD, is employed to process photovoltaic power generation data. First, the STL method is employed to break down the data into three constituent elements: trend, seasonal, and residual components. Then, VMD is applied to decompose the residual component. The residual component still contains high-frequency and non-stationary signals. This secondary decomposition strategy decomposes the data information more thoroughly, thereby boosting the prediction capability of the model.

- (2) The presented Transformer-LSTM hybrid architecture combines the ability of Transformer to capture long-range dependencies with the local temporal pattern learning capability of LSTM, forming a hierarchical multi-scale feature extraction mechanism.
- (3) This study presents a physics-constrained loss function, formulated by integrating the mean square error and three physical constraint terms, which can dynamically adjust prediction deviations, making the prediction results more closely match the actual characteristics of PVPG.
- (4) The Dream Optimization Algorithm (DOA) is used to optimize the hyperparameters of both VMD and the forecasting model. This study improves DOA by employing ICMIC chaotic mapping instead of uniform random initialization to enhance the diversity of the initial population and reduce the risk of falling into local optima.

The structure of the remainder of this study is outlined as follows. Section 2 explains the working principles of each module within the presented hybrid model. Section 3 introduces the datasets and their processing procedures, along with experimental settings. The experimental findings are detailed in Section 4. Section 5 provides further discussion. Concluding the study, Section 6 summarizes the main conclusions of this research.

## 2. Methods

### 2.1. The Dream Optimization Algorithm

Over the past few years, intelligent optimization algorithms have been extensively employed to optimize model hyperparameters and parameters for sequence decomposition, such as Particle Swarm Optimization (PSO) [33] and Bayesian Optimization [34]. Although PSO offers fast convergence, it is prone to local optima. Bayesian Optimization, while efficient, experiences a significant performance drop in high-dimensional parameter spaces. This study adopts the Dream Optimization Algorithm (DOA) for hyperparameter tuning [32]. The DOA exhibits powerful global search capabilities, mitigating the risk of convergence to local optima and demonstrating high adaptability to high-dimensional hyperparameter spaces. To ensure a more uniform distribution of the initial population across the entire search space, a population initialization method based on Iterative Chaotic Map with Infinite Collapses (ICMIC) chaotic mapping is introduced. This approach enhances global exploration and the capacity to avoid convergence to local optima, replacing random initialization.

The Dream Optimization Algorithm is a metaheuristic optimization algorithm that draws inspiration from the mechanisms of human dreaming. Its central concept involves emulating dream-related phenomena, including memory retention, partial forgetting, self-organization, and information sharing, to balance the algorithm's exploration and exploitation capabilities. The optimization process of DOA is divided into an initialization phase, an exploration phase, and an exploitation phase.

#### 2.1.1. Initialization phase

The ICMIC chaotic map is employed to generate the initial population, enhancing its ergodicity and uniformity. The calculation formula is as Eq. (1):

$$\begin{cases} x_k = \sin\left(\frac{\alpha}{x_{k-1}}\right) \\ x'_k = \frac{x_k + 1}{2} \\ x_{ij} = lb_j + x'_k \times (ub_j - lb_j) \end{cases} \quad (1)$$

Where  $x_k$  is the chaotic value at iteration  $k$ ,  $\alpha$  is a control parameter,  $x'_k$

denotes the normalized chaotic value,  $lb_j$  and  $ub_j$  represent the lower and upper bounds of dimension  $j$ , and  $x_{ij}$  indicates the initial value of dimension  $j$  for individual  $i$ . The generated initial population is as Eq. (2):

$$X = \begin{pmatrix} X_1 \\ X_2 \\ \vdots \\ X_N \end{pmatrix} = \begin{pmatrix} x_{1,1} & \cdots & x_{1,Dim} \\ \vdots & \ddots & \vdots \\ x_{N,1} & \cdots & x_{N,Dim} \end{pmatrix} \quad (2)$$

where  $N$  represents the population size,  $X$  denotes the number of individuals, and  $Dim$  denotes the number of decision variables per individual.

#### 2.1.2. Exploration phase

First, the population is categorized into five groups according to memory capacity, where groups with different memory capacities correspond to different numbers of forgetting dimensions  $k_q$ . The calculation formula for  $k_q$  is as Eq. (3):

$$k_q = \text{randi}\left(\left\lceil \frac{Dim}{8q} \right\rceil, \max\left\{2, \left\lceil \frac{Dim}{3q} \right\rceil\right\}\right), q = 1, 2, 3, 4, 5 \quad (3)$$

where  $\text{randi}(a, b)$  represents an integer chosen at random from the interval  $[a, b]$ .

##### (i) Memory strategies in the exploration phase

Before every iteration, each individual first memorizes the location of the group's historical best individual, then resets its own position to the group's optimum:

$$X_i^{t+1} = X_{\text{best},q}^t \quad (4)$$

where  $X_i^{t+1}$  corresponds to the  $i$ -th individual's position at iteration  $t+1$ , and  $X_{\text{best},q}^t$  represents the best individual in the  $q$ -th group at generation  $t$ .

##### (ii) Forgetting and supplementation strategies in the exploration phase

After memorization, each individual randomly forgets  $k_q$  dimensions and supplements the positions of these dimensions through self-organizing information:

$$x_{ij}^{t+1} = x_{\text{best},q,j}^t + \left(x_{ij}^t + \text{rand} \cdot (x_{u,j} - x_{l,j})\right) \cdot \frac{1}{2} \left(\cos\left(\pi \cdot \frac{t + T_{\max} - T_d}{T_d}\right) + 1\right) \quad (5)$$

where  $j \in \{K_1, K_2, \dots, K_{k_q}\}$  denotes the dimension of forgetting,  $x_{ij}^{t+1}$  indicates the position of the  $j$ -th dimension for the  $i$ -th individual in generation  $t+1$ , and  $x_{\text{best},q,j}^t$  represents the  $j$ -th dimensional position of the  $q$ -th optimal individual group at generation  $t$ ,  $x_{u,j}$  and  $x_{l,j}$  denote the lower and upper bounds of the  $j$ -th dimension,  $t$  corresponds to the current iteration number,  $T_{\max}$  is assigned to the maximum iteration count,  $T_d$  indicates the iteration limit for the exploration phase, and  $\text{rand}$  is a random number between 0 and 1.

##### (iii) Dream-sharing strategy

The dream-sharing strategy operates concurrently with the forgetting and supplementation approach, follows the memory strategy, and enables individuals to randomly acquire positional information from others in the forgotten dimensions. The equation is given as Eq. (6):

$$x_{ij}^{t+1} = \begin{cases} x_{mj}^{t+1}, & m \le i \\ x_{ij}^t, & i < m \le N \end{cases} \quad (6)$$

where  $x_{mj}^{t+1}$  corresponds to the position of the  $m$ -th individual at generation  $t+1$  in the  $j$ -th dimension, with  $m$  being a natural number randomly selected from  $[1, N]$  for updating each dimension.

##### 2.1.1.3. Exploitation phase

In the exploitation phase, the population ceases to be segregated into subgroups. Every individual in the population shares an identical count of forgetting dimensions  $k_r$ , and all individuals are updated based on the global best solution. The calculation formula for  $k_r$  is as Eq. (7):

$$k_r = \text{randi}\left(2, \left\lceil \frac{\text{Dim}}{3} \right\rceil\right) \quad (7)$$

##### (i) Memory strategies in the exploitation phase

The individual resets its own position to the global historical best individual's position, focusing on the local optimal region. The equation is given as Eq. (8):

$$x_i^{t+1} = x_{\text{best}}^t \quad (8)$$

##### (ii) Forgetting and supplementation strategies in the exploitation phase

The quantity of forgetting dimensions for all individuals is uniformly set to  $k_r$  to further strengthen local exploitation. The calculation formula is as Eq. (9):

$$x_{ij}^{t+1} = x_{\text{best}j}^t + \left( x_{ij}^t + \text{rand} \cdot (x_{uj} - x_{lj}) \right) \cdot \frac{1}{2} \left( \cos\left(\pi \cdot \frac{t}{T_{\max}}\right) + 1 \right) \quad (9)$$

### 2.2. A secondary decomposition strategy based on STL and VMD

#### 2.2.1. STL

STL performs smoothing and fitting processing on the data, thereby achieving more accurate seasonal and trend predictions [35]. STL decomposes the time series  $Y_t$  into three core components based on Locally Weighted Regression, defined as follows:

$$Y_t = T_t + S_t + R_t \quad (10)$$

where  $T_t$  denotes the trend component, indicating the long-term, smooth evolution direction of the time series;  $S_t$  represents the seasonal component, reflecting periodically recurring fluctuations in the time series; and  $R_t$  represents the remainder component, reflecting the residual random fluctuations after decomposition. The core procedure of STL decomposition consists of inner and outer loops. The inner loop iteratively refines the seasonal and trend components to gradually improve their accuracy, while the outer loop reduces the impact of outliers on the decomposition by dynamically adjusting sample weights, thereby achieving accurate decomposition.

#### 2.2.2. Secondary decomposition of VMD

While STL decomposition has extracted the primary trend and seasonal components, the resulting remainder component still contains complex, non-stationary short-term fluctuations, such as rapidly moving clouds or localized light rain. Directly using these components for prediction may increase errors. VMD is an adaptive decomposition technique employed to process non-stationary and non-linear signals. It can decompose a complex signal into a series of quasi-orthogonal, finite-bandwidth sub-sequences with distinct center frequencies, known as Intrinsic Mode Functions (IMFs). Each IMF represents a time-series

component at a specific frequency [36]. By applying VMD to further decompose the remainder component obtained from STL decomposition into a finite number of IMFs, non-stationary signals are transformed into a series of relatively stationary sub-signals, thereby providing more favorable features for the model.

The residual component  $f(t)$  is decomposed into  $K$  intrinsic mode functions  $u_k(t)$ . The objective function aims at the minimization of the total bandwidth across all modes, subject to the constraint that their sum equals the original signal. The model is constructed as Eq. (11):

$$\begin{cases} \min_{\{u_k\}, \{\omega_k\}} \left\{ \sum_{k=1}^{K} \left\| \vartheta_t \left[ \left( \delta(t) + \frac{j}{\pi t} \right) * u_k(t) \right] e^{-j\omega_k t} \right\|_2^2 \right\} \\ \text{s.t.} \sum_{k=1}^{K} u_k(t) = f(t) \end{cases} \quad (11)$$

where  $\vartheta_t$  represents the time derivative,  $\delta(t) + \frac{j}{\pi t}$  represents the Hilbert transform kernel,  $e^{-j\omega_k t}$  represents the frequency shift factor,  $\|\cdot\|_2^2$  represents the square of the  $L_2$  norm,  $*$  represents the convolution operation, and  $\omega_k$  represents the center frequency corresponding to  $u_k$ . By introducing the Lagrange multiplier  $\lambda(t)$  and penalty factor  $\alpha$ , the constrained problem is converted into an unconstrained one. The calculation formula is as Eq. (12):

$$L = \alpha \sum_{k=1}^{K} \left\| \vartheta_t \left[ \left( \delta(t) + \frac{j}{\pi t} \right) * u_k(t) \right] e^{-j\omega_k t} \right\|_2^2 + \left\| f(t) - \sum_{k=1}^{K} u_k(t) \right\|_2^2 + \langle \lambda(t), f(t) - \sum_{k=1}^{K} u_k(t) \rangle \quad (12)$$

The alternating direction method of multipliers (ADMM) algorithm is employed to decompose the problem into three subproblems, which are solved iteratively in an alternating manner. When updating one variable, the other two variables remain fixed. The calculation formulas are as Eqs. (13)–(15):

$$\hat{u}_k^{n+1}(\omega) = \frac{\hat{f}(\omega) - \sum_{i \neq k} \hat{u}_i(\omega) + \frac{\hat{\lambda}(\omega)}{2}}{1 + 2\alpha(\omega - \omega_k)^2} \quad (13)$$

$$\omega_k^{n+1} = \frac{\int_0^\infty \omega |\hat{u}_k(\omega)|^2 d\omega}{\int_0^\infty |\hat{u}_k(\omega)|^2 d\omega} \quad (14)$$

$$\hat{\lambda}^{n+1}(\omega) = \hat{\lambda}^n + \tau \left( \hat{f}(\omega) - \sum_{k=1}^{K} \hat{u}_k^{n+1}(\omega) \right) \quad (15)$$

where  $\hat{u}_k^{n+1}(\omega)$ ,  $\hat{f}(\omega)$ ,  $\hat{u}_i(\omega)$ ,  $\hat{\lambda}^{n+1}$  are the Fourier transforms of  $u_k^{n+1}(t)$ ,  $f(t)$ ,  $u_i(t)$  and  $\lambda^{n+1}$ , respectively.  $\hat{u}_k^{n+1}(\omega)$  represents the frequency domain of the  $k$ -th mode at the  $(n+1)$ -th iteration, and  $\tau$  denotes the iteration step size. The iteration stops when the update magnitude for all modes is less than the preset threshold  $\epsilon$ . The formula is as Eq. (16):

$$\sum_{k=1}^{K} \frac{\|\hat{u}_k^{n+1} - \hat{u}_k^n\|_2^2}{\|\hat{u}_k^n\|_2^2} < \epsilon \quad (16)$$

During the iterative solution phase, Eq. (13) updates the modes in the frequency domain, Eq. (14) calculates the energy-weighted center frequencies of the modes to dynamically adapt to the signal's frequency distribution, and Eq. (15) updates the Lagrange multiplier. The iterative process halts when the convergence criterion given by Eq. (16) is fulfilled, ultimately outputting the intrinsic mode functions and completing the adaptive decomposition of the residual component.

#### 2.2.3. Optimization of VMD parameters based on the DOA

When using VMD for modal decomposition, its decomposition per-

formance highly depends on two key parameters: the modal number  $K$  and the bandwidth penalty factor  $\alpha$  [37]. An excessively low value of  $K$  results in under-decomposition and mode mixing, whereas an overly large  $K$  induces over-decomposition, it will lead to over-decomposition, thereby introducing unrelated information that interferes with predictions. If  $\alpha$  is too large, some important detailed information may be lost; if  $\alpha$  is too small, it may result in insufficient frequency separation, causing mode mixing. However, manual parameter tuning is inefficient and makes it difficult to obtain the optimal parameter combination. Therefore, intelligent optimization algorithms are widely used for hyperparameter tuning.

This study employs the DOA to optimize the two hyperparameters of VMD: the mode number  $K$  and the bandwidth penalty factor  $\alpha$ . The DOA helps improve decomposition quality by minimizing the fitness function within a predefined parameter range to find the optimal parameter combination. This study uses envelope entropy as the fitness function. To ensure the algorithm sufficiently explores the solution space and converges stably, we set the maximum number of iterations to 40. The search ranges of the VMD parameters and their final selected values can be found in the Supplementary Information.

### 2.3. Transformer-LSTM with the DOA

#### 2.3.1. Transformer

The Transformer model has demonstrated powerful capabilities in

handling complex problems. Fig. 1 shows the complete structure of the Transformer model. Transformer is a sequence modeling model based on the self-attention mechanism, which can efficiently perform temporal modeling on input multidimensional time series features, extract complex temporal dependencies, especially long-range dependencies, thereby enhancing multi-step prediction capabilities [38].

To effectively capture long-term dependencies and global characteristics of photovoltaic power generation sequences, this study introduces a Transformer encoder module to enhance the features of the input sequence. Based on the self-attention mechanism, this module can capture dependency information between any time steps in the sequence in parallel. The module mainly consists of a positional encoding, a multi-head self-attention, a feed-forward neural network, residual links, and normalization layers. To preserve the temporal order information of the input sequence, positional encoding is integrated into the input to embed positional information. This study adopts sine-cosine positional encoding, calculated as Eq. (17):

$$\begin{cases} PE(pos, 2m) = \sin\left(\frac{pos}{10000^{\frac{2m}{d}}}\right) \\ PE(pos, 2m + 1) = \cos\left(\frac{pos}{10000^{\frac{2m}{d}}}\right) \end{cases} \quad (17)$$

where  $PE(pos, i)$  represents the positional encoding value at the  $pos$ -th

![Complete structural diagram of the Transformer model. The diagram shows two parallel processing paths: an Encoder (left) and a Decoder (right), both consisting of N layers. The Encoder takes an 'Input' and adds 'Positional Encoding' before entering the first layer. Each Encoder layer contains 'Masked Multi-Headed Attention' followed by 'Add&Norm' and a 'Feed-Forward Network' followed by 'Add&Norm'. The Decoder takes an 'Output (Shifted right)' and adds 'Positional Encoding' before entering the first layer. Each Decoder layer contains 'Multi-Headed Attention' (which also receives input from the Encoder's output), 'Add&Norm', a 'Feed-Forward Network' with 'Add&Norm', and a 'Linear' layer at the end. The final output is 'Output Probabilities'.](4d7f667796a8cdcdd745e953ac11e289_img.jpg)

Complete structural diagram of the Transformer model. The diagram shows two parallel processing paths: an Encoder (left) and a Decoder (right), both consisting of N layers. The Encoder takes an 'Input' and adds 'Positional Encoding' before entering the first layer. Each Encoder layer contains 'Masked Multi-Headed Attention' followed by 'Add&Norm' and a 'Feed-Forward Network' followed by 'Add&Norm'. The Decoder takes an 'Output (Shifted right)' and adds 'Positional Encoding' before entering the first layer. Each Decoder layer contains 'Multi-Headed Attention' (which also receives input from the Encoder's output), 'Add&Norm', a 'Feed-Forward Network' with 'Add&Norm', and a 'Linear' layer at the end. The final output is 'Output Probabilities'.

Fig. 1. Complete structural diagram of the Transformer model.

time step and the  $i$ -th feature dimension in the input sequence,  $pos$  denotes the time index step,  $m$  is the dimension index, and  $d$  is the dimensionality of the input features. The positional encoding is fused with the original input sequence through element-wise addition. The mathematical formulation is presented as Eq. (18):

$$X_{pe} = X + PE \quad (18)$$

where  $X$  is the input sequence, and  $X_{pe}$  denotes the sequence with injected positional information.

The self-attention mechanism is the core component of the Transformer. For the input sequence  $X_{pe}$ , it is mapped into three distinct sets of vectors through linear transformations: query (Q), key (K), and value (V) vectors. This is expressed as Eq. (19):

$$\begin{cases} Q = X_{pe}W^Q \\ K = X_{pe}W^K \\ V = X_{pe}W^V \end{cases} \quad (19)$$

where  $W^Q$ ,  $W^K$ , and  $W^V$  are learnable weight matrices. The attention weights are determined by the dot product of the Q and K vectors, as Eq. (20) presented:

$$Attention(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V \quad (20)$$

where  $\sqrt{d_k}$  is the scaling factor, used to mitigate vanishing gradients resulting from an excessively large dot product.

The multi-head attention mechanism maps Q, K, and V into  $i$  separate subspaces. Attention computation is performed independently within each subspace. Following concatenation, the combined outputs from all attention heads are integrated via a linear transformation layer as Eq. (21):

$$MultiHead(Q, K, V) = \text{Concat}(\text{head}_1, \dots, \text{head}_i)W^o \quad (21)$$

where  $\text{head} = \text{Attention}(QW^Q, KW^K, VW^V)$ , and  $W^o$  is the fusion parameter.

Following each attention sublayer, a position-wise fully connected feed-forward neural network is applied to independently perform a nonlinear transformation on the representation at each position as Eq. (22):

$$FFN(x) = \max(0, xW_1 + b_1)W_2 + b_2 \quad (22)$$

where  $W_1$  and  $W_2$  are weight matrices,  $b_1$  and  $b_2$  are the bias terms, and ReLU is the activation function. In order to address the vanishing gradient problem during deep network training and accelerate convergence, residual connections are employed around each sub-layer, fol-

lowed immediately by layer normalization. Ultimately, the output feature vectors of the Transformer will serve as the input to the subsequent LSTM network for further temporal prediction.

#### 2.3.2. LSTM

While the Transformer model excels at modeling long-range dependencies within input sequences, photovoltaic power data also contains important local temporal dynamic characteristics, such as minute-level power fluctuations caused by rapid cloud movement. Therefore, this study introduces a LSTM network module after the Transformer encoder [39].

Building on traditional RNNs, LSTM incorporates a sophisticated gating mechanism to regulate information flow. This gating mechanism addresses the limitations of conventional RNNs in maintaining long-term memory [40] while filtering out irrelevant short-term noise. Its structure is shown in Fig. 2. The LSTM architecture is built upon three core components: the forget gate, input gate, and output gate. The calculation methods of LSTM are provided in the Supplementary Information.

#### 2.3.3. Model parameter optimization based on the DOA

Based on the above content, a Transformer-LSTM prediction model was constructed. The model's overarching framework is delineated in Fig. 3. First, the time series data is input, and the linear projection layer projects it into the model's representation space, mapping all features. Subsequently, to inject temporal order information, positional encoding is added to the projected data. Positional encoding conveys sequence-element position information to the model and is generated using sine and cosine functions, which help the model learn time-dependent patterns more effectively. The data then passes through the Transformer encoder layer to capture long-range dependencies and nonlinear correlations among features in the time series data. The LSTM then receives the feature sequence output by the Transformer to capture its local and fine-grained temporal dynamics. Finally, the fully connected layer maps the LSTM output to the prediction dimension, producing the final prediction result.

Selecting appropriate model hyperparameters profoundly impacts the predictive accuracy of the approach [35]. Frequently employed techniques for hyperparameter adjustment encompass grid search, random search, Bayesian optimization, and heuristic algorithms [41]. This study employs the DOA to optimize the model's hyperparameters, thereby alleviating the detrimental impacts of improper parameter settings on predictions and improving forecasting performance.

### 2.4. Physics-constrained loss function

To address the issue where traditional data-driven models may violate physical principles in photovoltaic power forecasting, this study

![Structure diagram of LSTM showing three sequential LSTM cells. Each cell takes an input x_t and a previous hidden state h_{t-1} to produce the next hidden state h_t. Inside each cell, the input x_t is processed by a linear layer (x) and a sigmoid layer (sigma). The previous hidden state h_{t-1} is processed by a linear layer (x), a sigmoid layer (sigma), a tanh layer, and a linear layer (x). The outputs of these four layers are combined via element-wise multiplication (+) to form the next hidden state h_t. The diagram illustrates the standard LSTM structure with its four gates: input, forget, output, and cell state.](b7c32759f9cc85d4046f176dff1be3fa_img.jpg)

Structure diagram of LSTM showing three sequential LSTM cells. Each cell takes an input x\_t and a previous hidden state h\_{t-1} to produce the next hidden state h\_t. Inside each cell, the input x\_t is processed by a linear layer (x) and a sigmoid layer (sigma). The previous hidden state h\_{t-1} is processed by a linear layer (x), a sigmoid layer (sigma), a tanh layer, and a linear layer (x). The outputs of these four layers are combined via element-wise multiplication (+) to form the next hidden state h\_t. The diagram illustrates the standard LSTM structure with its four gates: input, forget, output, and cell state.

Fig. 2. Structure diagram of LSTM.

![Overall structure diagram of the Transformer-LSTM model. The main flow starts with 'Inputs' entering a 'Linear projection' block, followed by 'Positional Encoding'. This then enters a dashed box containing '*N' stacked blocks, each consisting of 'Multi-Headed Self-Attention' and 'Feed-Forward Network'. The output of this block stack enters 'LSTM Layers', which is a grid of nodes with bidirectional connections. Finally, it enters an 'FC layer' to produce 'Outputs'. Below the main diagram, there is a detailed inset showing the 'Multi-Headed Attention' mechanism. It shows three input blocks (Query, Key, Value) being processed by multiple heads (represented by colored cubes) to produce an 'Aggregated attention output'.](a738993919a50143787084ee7ce6e2f2_img.jpg)

Overall structure diagram of the Transformer-LSTM model. The main flow starts with 'Inputs' entering a 'Linear projection' block, followed by 'Positional Encoding'. This then enters a dashed box containing '\*N' stacked blocks, each consisting of 'Multi-Headed Self-Attention' and 'Feed-Forward Network'. The output of this block stack enters 'LSTM Layers', which is a grid of nodes with bidirectional connections. Finally, it enters an 'FC layer' to produce 'Outputs'. Below the main diagram, there is a detailed inset showing the 'Multi-Headed Attention' mechanism. It shows three input blocks (Query, Key, Value) being processed by multiple heads (represented by colored cubes) to produce an 'Aggregated attention output'.

Fig. 3. Overall structure diagram of the Transformer-LSTM model.

proposes a hybrid loss function incorporating physical mechanisms. Building upon the mean square error (MSE) loss, physical constraint terms are introduced to guide the model toward learning prediction patterns that align with the operational characteristics of photovoltaic systems.

The physical characteristics of photovoltaic power generation determine that its output cannot be negative. To prevent the model from predicting negative power, a non-negativity constraint is designed to penalize the portion of the predicted values that are less than 0. The output power of a photovoltaic array is limited by physical conditions such as the component's rated capacity, irradiance, and temperature, making it impossible to exceed its theoretical maximum output power. To prevent the model from predicting power exceeding the theoretical maximum, a rated power upper limit constraint is designed. Changes in PVPG are limited by the rate of change of irradiance and will not experience drastic and abrupt changes; therefore, a power ramp rate constraint is set. The total loss function is formulated as a weighted combination of mean square error and multiple physical constraints penalty terms, as shown in the following Eq. (23):

$$L_{total} = \lambda_1 L_{MSE} + \lambda_2 L_{non-neg} + \lambda_3 L_{max-power} + \lambda_4 L_{ramp} \quad (23)$$

where  $\lambda$  represents the weight coefficients, and  $L_{MSE}$ ,  $L_{non-neg}$ ,  $L_{max-power}$ , and  $L_{ramp}$  denote the mean square error loss, non-negativity constraint loss, power upper limit constraint loss, and ramp rate loss, respectively. The weight coefficients were determined through grid search optimization. The final selected results in this study are 1, 0.1, 0.01, and 0.1, respectively. The power output of photovoltaic modules cannot be negative. A non-negativity penalty term is adopted, which imposes penalties only when the predicted power is less than 0. The calculation formula is as Eq. (24):

$$L_{non-neg} = \frac{1}{N} \sum_{i=1}^{N} [\max(0, -P_{pred}(t))]^2 \quad (24)$$

where  $P_{pred}$  is the predicted power. The output power of photovoltaic modules is constrained by irradiance and temperature, having a theoretical maximum value. The rated power upper limit constraint is calculated as Eq. (25):

$$L_{max-power} = \frac{1}{N} \sum_{i=1}^{N} [\max(0, P_{pred}(t) - P_{max}(t))]^2 \quad (25)$$

where  $P_{max}(t) = P_{STC} \frac{G(t)}{G_{STC}} [1 - \alpha(T(t) - T_{STC})]$ ,  $P_{max}$  signifies the theo-

retical maximum power,  $P_{STC}$  indicates the photovoltaic module's rated power under standard test conditions,  $G$  represents the actual solar irradiance,  $G_{STC}$  signifies the irradiance under standard test conditions,  $\alpha$  signifies the power temperature coefficient of the photovoltaic module, and  $T_{STC}$  denotes the reference temperature under standard test conditions. The variation of photovoltaic power is constrained by the rate of irradiance change, and the power fluctuation between adjacent time steps cannot be infinitely large. The ramp rate constraint loss is calculated as Eq. (26):

$$L_{ramp} = \frac{1}{N-1} \sum_{i=2}^{N} [\max(0, |P_{pred}(t) - P_{pred}(t-1)| - R_{max} \cdot \Delta t)]^2 \quad (26)$$

where  $\Delta t$  represents the time step length, and  $R_{max}$  represents the maximum ramp rate.

### 2.5. Overall framework of the prediction process for the proposed method

This study proposes a physics-constrained hybrid forecasting model, whose core employs an improved Dream Optimization Algorithm to collaboratively optimize the hyperparameters of both the STL-VMD secondary decomposition structure and the Transformer-LSTM network. Fig. 4 illustrates the overall workflow framework of the model, with the forecasting steps as follows:

First, the Spearman rank correlation coefficient is used to screen input features, retaining variables highly correlated with photovoltaic power output. Subsequently, STL is introduced to decompose the initial power series into three constituents: trend, seasonal, and residual. To further extract effective information from the residual component, DOA-optimized VMD is employed for secondary decomposition, obtaining several Intrinsic Mode Functions to ensure thorough separation of high-frequency and non-stationary components in the sequence.

Finally, the components obtained from STL decomposition, the IMFs generated by VMD decomposition, and the screened meteorological features are collectively fed into a DOA-optimized Transformer-LSTM hybrid forecasting model. This model combines the advantages of the Transformer in capturing prolonged dependencies with the effectiveness of the LSTM in processing sequential dynamics, while incorporating a physics-constrained mechanism to ensure physically plausible prediction results. The framework ultimately generates photovoltaic power forecasts that are both accurate and interpretable. The presented model is evaluated against various other models through a series of comparative experiments, utilizing five distinct evaluation metrics to assess its

![Overall framework of the prediction process for the proposed method. The framework is divided into four main steps: Step 1: Data Preprocessing and Feature Selection; Step 2: Secondary decomposition and signal layered processing; Step 3: Model Construction and Parameter Optimisation; and Step 4: Multi-dimensional predictive performance evaluation.](990567efebf979be51f56d1150012c9d_img.jpg)

**Step 1: Data Preprocessing and Feature Selection**

- Australian DKASC Dataset → Missing value interpolation → Outlier processing → Data normalization
- Weather features: Temperature Celsius, Relative Humidity, Global Horizontal Radiation, Diffuse Horizontal Radiation, Wind Speed, Wind Direction, Daily Rainfall, Others...
- Active Power (circular node) and Key features (circular node) are identified using Spearman coefficient.

**Step 2: Secondary decomposition and signal layered processing**

- STL decomposition → Trend component, Seasonal component, Residual component
- Hyperparameter optimisation → Improved DOA → VMD decomposition → IMF1, IMF2, ..., IMFn
- Transformer Encoder Layer: positional encoding → Multi-head self-attention → Feed forward
- LSTM Layer: Cating mechanism, Forget Gate, Input Gate, Output Gate
- Physical Constraint Loss Function: Non-negative, Rated power, Gradeability

**Step 3: Model Construction and Parameter Optimisation**

**Step 4: Multi-dimensional predictive performance evaluation**

- Foundational Performance Evaluation Metrics: Core Metrics (RMSE, MAE,  $R^2$ , BIAS, KGE), Benchmark Comparison (LSTM, GRU, Transform, LightGBM, Transform-LSTM, SVM, STL-Transform, EMD-Transform-LSTM, ...)
- Validate model generalisation capability: Cross-Sites, Cross-seasonal, Noise Robustness, Cross-weather
- Model Interpretability Analysis: SHAP Feature Importance Assessment, Feature Importance Histogram, Feature Influence Mechanism Analysis, SHAP dependency graph

Overall framework of the prediction process for the proposed method. The framework is divided into four main steps: Step 1: Data Preprocessing and Feature Selection; Step 2: Secondary decomposition and signal layered processing; Step 3: Model Construction and Parameter Optimisation; and Step 4: Multi-dimensional predictive performance evaluation.

Fig. 4. Overall framework of the prediction process for the proposed method.

forecasting performance. Furthermore, the study examines the model's effectiveness across different sites, seasons, and weather conditions, as well as its resilience to noise. Additionally, an interpretability analysis is performed.

## 3. Case study

### 3.1. Data description

The experimental data in this research were obtained from the Desert Knowledge Australia Solar Center (DKASC) website. Data from two sites in the Alice Springs area were selected for validation. The geographical locations and equipment installation configurations of each experimental site are shown in Fig. 5 and Table 1. Data were collected from April 23, 2013, to October 21, 2016. Since power generation at night is zero, data from 8:00 to 17:55 each day were used, with a temporal resolution of 5 min. The original features of the dataset include Active Power, Weather Temperature Celsius, Weather Relative Humidity, Global Horizontal Radiation, Diffuse Horizontal Radiation, Wind Speed, Wind Direction, Weather Daily Rainfall, Radiation Global Tilted, and Radiation Diffuse Tilted.

Table 1

Detailed equipment installation configuration at the experimental site.

|                    | Site 1                           | Site 2                           |
|--------------------|----------------------------------|----------------------------------|
| Array Rating       | 6.3 kW                           | 6 kW                             |
| Panel Rating       | 210 W                            | 60 W                             |
| Number of Panels   | 30                               | 100                              |
| Panel Type         | Sanyo HIP-210NKHE5               | Kaneka G-EA060                   |
| Array Area         | 37.83 $m^2$                      | 95.04 $m^2$                      |
| Type of Tracker    | N/A                              | N/A                              |
| Inverter Size/Type | 7 kW, SMA SMC 7000 TL            | 6 kW, SMA SMC 6000A              |
| Installation       | Thu, 11 Mar 2010                 | Tue, 11 Nov 2008                 |
| Completed          |                                  |                                  |
| Array Tilt/Azimuth | Tilt = 20, Azi = 0 (Solar North) | Tilt = 20, Azi = 0 (Solar North) |

### 3.2. Data preprocessing

As the raw data cannot be fed directly into the model, preprocessing is required. First, interpolation is applied to handle missing values, thereby preserving the continuity of the temporal sequence. Second, the moving window mean substitution method is applied to handle outliers in the data, using the average of the 15 normal points before and after

![Geographical location of the experimental site. The image shows a 3D perspective view of a landscape with two experimental sites. Site 1 is on the left, and Site 2 is on the right. Both sites feature solar panel arrays and small buildings. A north arrow is located at the bottom center of the map.](069bf4f45bd3cf5fc36a67301579bc31_img.jpg)

Geographical location of the experimental site. The image shows a 3D perspective view of a landscape with two experimental sites. Site 1 is on the left, and Site 2 is on the right. Both sites feature solar panel arrays and small buildings. A north arrow is located at the bottom center of the map.

Fig. 5. Geographical location of the experimental site.

the outlier to locally smooth the abnormal values. Additionally, differences in units and numerical ranges among different features in the data can have negative effects and are unfavorable for model training. To accelerate model convergence, the "Min-Max" normalization method is used for data normalization. The calculation formula is as follows:

$$x' = \frac{x - \min(x)}{\max(x) - \min(x)} \quad (27)$$

Where  $x$  corresponds to the unprocessed data before normalization, and  $x'$  corresponds to the normalized data.

To reduce redundant information and noise while improving model performance and prediction accuracy, the correlations between the input features and the target variable were analyzed using the Spearman rank correlation coefficient. For this purpose, a heatmap was generated and is presented in Fig. 6. Fig. 6 reveals that Global Horizontal Radiation and Radiation Global Tilted exhibit the strongest correlation with the target variable Active Power, both above 0.9. This is followed by Weather Temperature Celsius, Weather Relative Humidity, and Wind Speed, with absolute values all greater than 0.2. The absolute values of the remaining features are all below 0.2. This study selects features with an absolute correlation value greater than 0.2 as input features, specifically the five features: Global Horizontal Radiation, Radiation Global Tilted, Weather Temperature Celsius, Weather Relative Humidity, and Wind Speed.

### 3.3. Experiment settings

All experiments in this research were performed on a PC configured with an Intel(R) Core(TM) i5-13500HX processor and an NVIDIA GeForce RTX 4050 Laptop GPU. The system memory (RAM) was 16 GB, with 1.40 TB of storage. The operating system was Windows 11. The model was built with PyTorch and Python 3.13.2, leveraging GPU acceleration for computational tasks. The maximum number of training epochs was set to 100, utilizing the Adam optimizer.

### 3.4. Benchmark models

To validate the effectiveness of the developed model, it was compared with different models. The baseline models encompassed

machine learning models: SVM and LightGBM. Deep learning models included GRU, LSTM, Transformer, PatchTST, TimesNet, Autoformer, STL-Transformer, EMD-Transformer-LSTM, VMD-CNN-LSTM, and STL-VMD-CNN-LSTM. The critical parameter configurations employed in these models are summarized in Table 2. For an objective comparison of model performance, a uniform hyperparameter configuration was applied across all models. The rationale for setting the key parameters is provided in the Supplementary Information.

**Table 2**  
Key parameter settings for the comparison model.

| Model                           | Parameters Settings                 | Value                 |
|---------------------------------|-------------------------------------|-----------------------|
| SVM                             | Kernel Function Type:               | Radial Basis Function |
|                                 | Penalty Parameter C:                | 1                     |
| LightGBM                        | Maximum number of leaves:           | 31                    |
|                                 | Maximum depth of tree:              | -1                    |
|                                 | Minimum number of data in one leaf: | 20                    |
| GRU                             | Hidden dimension:                   | 256                   |
|                                 | Number of layers:                   | 2                     |
| LSTM                            | Hidden dimension:                   | 256                   |
|                                 | Number of layers:                   | 2                     |
| Transformer                     | Hidden dimension:                   | 256                   |
|                                 | Number of Encoder Layers:           | 2                     |
|                                 | Number of Attention Heads:          | 4                     |
| PatchTST                        | Patch_len:                          | 12                    |
|                                 | Hidden dimension:                   | 256                   |
|                                 | Number of Attention Heads:          | 8                     |
| TimesNet                        | Number of Encoder Layers:           | 2                     |
|                                 | Hidden dimension:                   | 256                   |
| Autoformer                      | Number of Attention Heads:          | 8                     |
|                                 | Number of Encoder Layers:           | 2                     |
| CNN in the hybrid model         | Kernel Size:                        | 3                     |
|                                 | Activation Function                 | ReLU                  |
| LSTM in the hybrid model        | Hidden dimension:                   | 128                   |
|                                 | Number of layers:                   | 2                     |
| Transformer in the hybrid model | Hidden dimension:                   | 128                   |
|                                 | Number of Attention Heads:          | 4                     |
|                                 | Number of Encoder Layers:           | 2                     |

![Correlation heatmap of variables. The heatmap shows the correlation coefficients between 11 variables: Active Power, Weather Temperature Celsius, Weather Relative Humidity, Global Horizontal Radiation, Diffuse Horizontal Radiation, Wind Speed, Wind Direction, Weather Daily Rainfall, Radiation Global Tilted, and Radiation Diffuse Tilted. The diagonal elements are all 1.0. The strongest correlations are between Active Power and Global Horizontal Radiation (0.9483), Active Power and Radiation Global Tilted (0.9253), and Global Horizontal Radiation and Radiation Global Tilted (0.9233). Other correlations with absolute values greater than 0.2 include Weather Temperature Celsius (0.2175), Weather Relative Humidity (-0.3241), and Wind Speed (0.2785).](8f93234090c5bc224e4b9d035018a927_img.jpg)

Correlation heatmap of variables. The heatmap shows the correlation coefficients between 11 variables: Active Power, Weather Temperature Celsius, Weather Relative Humidity, Global Horizontal Radiation, Diffuse Horizontal Radiation, Wind Speed, Wind Direction, Weather Daily Rainfall, Radiation Global Tilted, and Radiation Diffuse Tilted. The diagonal elements are all 1.0. The strongest correlations are between Active Power and Global Horizontal Radiation (0.9483), Active Power and Radiation Global Tilted (0.9253), and Global Horizontal Radiation and Radiation Global Tilted (0.9233). Other correlations with absolute values greater than 0.2 include Weather Temperature Celsius (0.2175), Weather Relative Humidity (-0.3241), and Wind Speed (0.2785).

**Fig. 6.** Correlation heatmap of variables.

### 3.5. Evaluation metrics

To evaluate the model's predictive capability via the test set, this study employs five evaluation metrics: root mean square error (RMSE), mean absolute error (MAE), coefficient of determination ( $R^2$ ), bias (BIAS), and Kling-Gupta efficiency (KGE). Among these, RMSE and MAE quantify the deviation between predictions and actual values, with smaller numerical values corresponding to better model performance.  $R^2$  assesses the model fit quality, with values approaching 1 indicating better alignment. BIAS reflects the average deviation of predictions, with values closer to 0 indicating better performance. KGE is a comprehensive efficiency metric that considers correlation, standard deviation, and bias, with values closer to 1 being more desirable. The calculation formulas for these metrics are as follows:

$$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2} \quad (28)$$

$$MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i| \quad (29)$$

$$R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y}_i)^2} \quad (30)$$

$$BIAS = \frac{\sum_{i=1}^{n} (\hat{y}_i - y_i)}{\sum_{i=1}^{n} y_i} \quad (31)$$

$$KGE = 1 - \sqrt{(r - 1)^2 + (\alpha - 1)^2 + (\beta + 1)^2} \quad (32)$$

where  $n$  represents the sample size,  $y_i$  represents the actual observations,  $\hat{y}_i$  stands for the model predictions,  $\bar{y}_i$  indicates the mean value of the observed data,  $r$  is the correlation coefficient between the predicted values and the observed values,  $\alpha$  is the variability ratio (the ratio of the standard deviation of the predicted values to the standard deviation of the observed values), and  $\beta$  is the bias ratio (the ratio of the mean of the predicted values to the mean of the observed values).

## 4. Result

### 4.1. Ablation study

In order to evaluate the contributions of every key component in the proposed model, an ablation study was conducted. The ablation study utilized the dataset from Site 1 and Site 2, with the data allocated to training, validation, and test sets in a 70:15:15 ratio. This experiment is a multi-step direct forecasting task, where the model takes the recent 72 time steps of sequential data as input to predict the subsequent 24 time steps of photovoltaic power generation. For a fair comparison, the hyperparameter settings were maintained identically across all models during experimentation. Table 3 summarizes the performance metrics of different models after the ablation experiments at Site 1. The performance metrics and analysis for different models after the ablation experiments at Site 2 are provided in the Supplementary Information Fig. 7

**Table 3**

Performance metrics of each model after ablation experiments.

| Model                      | RMSE          | MAE           | $R^2$         | BIAS          | KGE           |
|----------------------------|---------------|---------------|---------------|---------------|---------------|
| Transformer-LSTM           | 0.7611        | 0.4639        | 0.8113        | 0.1479        | 0.8711        |
| STL-Transformer-LSTM       | 0.6992        | 0.4177        | 0.8407        | 0.0159        | 0.9017        |
| STL + VMD-Transformer      | 0.4601        | 0.2775        | 0.9310        | 0.0191        | 0.9530        |
| STL + VMD-LSTM             | 0.4315        | 0.2453        | 0.9393        | 0.0158        | 0.9016        |
| STL + VMD-Transformer-LSTM | 0.4256        | 0.2361        | 0.9410        | -0.0138       | 0.9618        |
| The proposed               | <b>0.4209</b> | <b>0.2326</b> | <b>0.9423</b> | <b>0.0124</b> | <b>0.9647</b> |

displays the performance bar charts of the different models following the ablation experiments at Site 1.

As shown in Fig. 7, the model presented in this study demonstrates the best performance. As indicated in Table 3, compared to STL + VMD-Transformer and STL + VMD-LSTM, the STL + VMD-Transformer-LSTM model reduces RMSE by 7.50% and 1.37% and MAE by 14.92% and 3.75%, respectively. Relative to the Transformer-LSTM model, the STL + VMD-Transformer-LSTM model reduces RMSE by 44.08%, MAE by 49.11%, improves  $R^2$  by 15.99%, brings the absolute value of BIAS closer to 0, and enhances KGE by 10.41%. Moreover, the performance of the Transformer-LSTM model is significantly lower relative to other models employing data decomposition. This indicates that models with data decomposition can better capture features at different time scales and more effectively handle non-stationary and nonlinear characteristics, thereby improving overall prediction stability and accuracy. Relative to the STL-Transformer-LSTM model, the STL + VMD-Transformer-LSTM model reduces RMSE by 39.13%, MAE by 43.48%, and improves  $R^2$  by 11.93%. This demonstrates that the secondary decomposition of the residual component can effectively handle complex, non-stationary signals in the residuals, thereby enhancing prediction accuracy. Relative to the STL + VMD-Transformer-LSTM model, the proposed model reduces RMSE by 1.1%, MAE by 1.48%, and brings BIAS closer to 0. Although the proposed model shows only marginal improvements in performance metrics compared to STL + VMD-Transformer-LSTM, the physical constraint module is not primarily aimed at drastically reducing overall error metrics. Instead, it focuses on accurately correcting anomalous predictions that violate the physical principles of photovoltaic power generation. This indicates that the proposed physical constraint loss function effectively suppresses predictions deviating from physical laws, enhances predictive capability, and reliably ensures the engineering practicality and reasonableness of the forecast results.

To validate the performance improvement achieved by the ICMIC chaotic mapping in the DOA algorithm, the optimization effectiveness of the original DOA and the improved DOA was compared in two scenarios: VMD parameter optimization and model hyperparameter optimization. The parameter settings, optimized variables, and their search ranges were kept identical for both algorithms. For VMD parameter optimization, the envelope entropy served as the core evaluation metric, while for model hyperparameter optimization, prediction performance metrics (RMSE, MAE,  $R^2$ ) were used as the evaluation criteria.

Tables S5 and S6 in the Supplementary Information present the comparative results of the two algorithms in optimizing VMD parameters and model hyperparameters, respectively. As shown in Table S5, the VMD envelope entropy optimized by the improved DOA is 6.0483, which is 11.09% lower than that of the original DOA (6.8034). This indicates that the ICMIC chaotic map enhances the global search capability of DOA, enabling it to find a better combination of VMD parameters and reduce mode mixing. Table S6 reveals that after hyperparameter optimization using the improved DOA, the model's RMSE and MAE decrease to 0.4209 and 0.2326, respectively, representing reductions of 12.0% and 18.7% compared to the results from the original DOA (RMSE = 0.4783, MAE = 0.2863). Furthermore, the  $R^2$  increases to 0.9423, an improvement of 2.37% over the 0.9215 achieved by the original DOA. Additionally, the improved DOA achieves an average convergence iteration count of 26, demonstrating a significant increase in convergence speed. These results fully demonstrate that the ICMIC chaotic map effectively enhances the optimization performance of DOA by improving the diversity of the initial population and reducing the risk of falling into local optima, thereby laying a solid foundation for the high-precision prediction of the subsequent model.

### 4.2. Comparison of predictive performance with benchmark model

This study uses the experimental data from Site 1 to assess the presented model in relation to baseline models, highlighting its superior forecasting capability. This experiment is also a multi-step direct 


![Fig. 7. Performance bar chart of different models after ablation experiment. The chart compares six models across four metrics: R^2 (pink), KGE (orange), RMSE (blue), and MAE (green). The left y-axis represents RMSE/MAE (0.3 to 1.2), and the right y-axis represents R^2/KGE (0.8 to 1.2). The models are Transformer-LSTM, STL-Transformer-LSTM, STL+VMD-Transformer, STL+VMD-LSTM, STL+VMD-Transformer-LSTM, and The proposed model. The proposed model shows the best performance with R^2=0.9423, KGE=0.9423, RMSE=0.4209, and MAE=0.04209.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

| Model                    | $R^2$  | KGE    | RMSE   | MAE     |
|--------------------------|--------|--------|--------|---------|
| Transformer-LSTM         | 0.8113 | 0.8113 | 0.7611 | 0.7611  |
| STL-Transformer-LSTM     | 0.8407 | 0.8407 | 0.6992 | 0.6992  |
| STL+VMD-Transformer      | 0.931  | 0.931  | 0.4601 | 0.4601  |
| STL+VMD-LSTM             | 0.9393 | 0.9393 | 0.4315 | 0.4315  |
| STL+VMD-Transformer-LSTM | 0.941  | 0.941  | 0.4256 | 0.4256  |
| The proposed             | 0.9423 | 0.9423 | 0.4209 | 0.04209 |

Fig. 7. Performance bar chart of different models after ablation experiment. The chart compares six models across four metrics: R^2 (pink), KGE (orange), RMSE (blue), and MAE (green). The left y-axis represents RMSE/MAE (0.3 to 1.2), and the right y-axis represents R^2/KGE (0.8 to 1.2). The models are Transformer-LSTM, STL-Transformer-LSTM, STL+VMD-Transformer, STL+VMD-LSTM, STL+VMD-Transformer-LSTM, and The proposed model. The proposed model shows the best performance with R^2=0.9423, KGE=0.9423, RMSE=0.4209, and MAE=0.04209.

Fig. 7. Performance bar chart of different models after ablation experiment.

forecasting task, where the model takes the recent 72 time steps of sequential data as input to predict the subsequent 24 time steps of photovoltaic power generation. Fig. 8 presents the training convergence profile of the proposed model. Table 4 summarizes the evaluation results of these models for the test set.

The presented model attains minimal MAE and RMSE values, as well as the highest  $R^2$  and KGE values. Although the STL-Transformer model performs slightly better in terms of BIAS (0.0046), its overall forecasting accuracy and comprehensive performance remain significantly lower than those of the proposed model. While maintaining controlled bias (BIAS = 0.0124), the proposed model achieves a better balance in error control, correlation retention, and comprehensive efficiency. In terms of RMSE alone, compared to single machine learning models such as SVM and LightGBM, the proposed model reduces RMSE by 54.68% and 42.62%, respectively. Compared to single models such as GRU, LSTM, and Transformer, RMSE is reduced by 42.74%, 42.62%, and 42.00%, respectively. Compared with PatchTST, TimesNet, and Autoformer, the RMSE was reduced by 43.90%, 43.47%, and 42.13%, respectively. Compared to hybrid models such as STL-Transformer, EMD-

Transformer-LSTM, STL + VMD-CNN-LSTM, and VMD-CNN-LSTM, RMSE is reduced by 38.63%, 33.94%, 23.61%, and 10.69%, respectively. These results demonstrate that the proposed model maintains leading forecasting accuracy across different datasets, fully validating its exceptional generalization capability and robustness.

In addition to the overall performance comparison, this experiment further evaluates the forecasting performance at the 1st, 8th, 16th, and 24th steps within the 24 forecasting steps to examine the proposed model's ability to maintain forecasting accuracy and robustness as the time step increases. Table 5 summarizes the performance metrics of different models at these four specific forecasting steps, where the optimal values are emphasized in bold. The proposed model achieves optimal values in 85% of the evaluation metrics, demonstrating dominant performance. Although it slightly underperforms the best result in terms of BIAS, the gap is extremely limited. Moreover, its significant advantages in core error metrics such as RMSE and MAE fully validate the model's exceptional and stable performance in multi-step forecasting tasks.

Fig. 9 presents a boxplot comparison of absolute error distributions

![Fig. 8. The training convergence profile of the proposed model. The graph shows Training Loss (blue line) and Validation Loss (red line) over 100 epochs. The Training Loss starts at 0.0225 and decreases steadily to approximately 0.0035. The Validation Loss starts at 0.0175 and decreases to approximately 0.0065, showing a clear gap between training and validation performance.](1640ec1dfae8bdfa5af950db7623febc_img.jpg)

| Epoch | Training Loss | Validation Loss |
|-------|---------------|-----------------|
| 0     | 0.0225        | 0.0175          |
| 10    | 0.0080        | 0.0100          |
| 20    | 0.0060        | 0.0090          |
| 40    | 0.0045        | 0.0075          |
| 60    | 0.0040        | 0.0070          |
| 80    | 0.0038        | 0.0068          |
| 100   | 0.0035        | 0.0065          |

Fig. 8. The training convergence profile of the proposed model. The graph shows Training Loss (blue line) and Validation Loss (red line) over 100 epochs. The Training Loss starts at 0.0225 and decreases steadily to approximately 0.0035. The Validation Loss starts at 0.0175 and decreases to approximately 0.0065, showing a clear gap between training and validation performance.

Fig. 8. The training convergence profile of the proposed model.

**Table 4**

Present the overall performance metrics for the proposed model and the baseline model.

| Model                | MAE           | RMSE          | R <sup>2</sup> | BIAS          | KGE           | Training Time (s) |
|----------------------|---------------|---------------|----------------|---------------|---------------|-------------------|
| SVM                  | 0.7354        | 0.9288        | 0.7190         | -0.1931       | 0.7808        | None              |
| LightGBM             | 0.4603        | 0.7335        | 0.8247         | 0.0359        | 0.8641        | None              |
| GRU                  | 0.4762        | 0.7351        | 0.8240         | 0.0494        | 0.8601        | 342               |
| LSTM                 | 0.4625        | 0.7335        | 0.8248         | 0.0429        | 0.8650        | 315               |
| Transformer          | 0.4561        | 0.7257        | 0.8285         | 0.0904        | 0.8592        | 357               |
| PatchTST             | 0.4566        | 0.7503        | 0.8166         | 0.0598        | 0.8841        | 339               |
| TimesNet             | 0.4734        | 0.7446        | 0.8194         | 0.1175        | 0.8601        | 550               |
| Autoformer           | 0.4501        | 0.7273        | 0.8277         | 0.1085        | 0.8606        | 428               |
| STL-Transformer      | 0.4210        | 0.6858        | 0.8468         | <b>0.0046</b> | 0.8820        | 364               |
| EMD-Transformer-LSTM | 0.3752        | 0.6371        | 0.8678         | 0.1100        | 0.9191        | 416               |
| STL + VMD-CNN-LSTM   | 0.3397        | 0.5510        | 0.9011         | -0.0062       | 0.9125        | 355               |
| VMD-CNN-LSTM         | 0.2924        | 0.4713        | 0.9276         | -0.0253       | 0.9085        | 383               |
| The proposed         | <b>0.2326</b> | <b>0.4209</b> | <b>0.9423</b>  | 0.0124        | <b>0.9647</b> | 522               |

**Table 5**

The evaluation results for the proposed model and the benchmark models.

| Metric         | Prediction point | The proposed  | M1      | M2      | M3     | M4     | M5     | M6              | M7     | M8      | M9            |
|----------------|------------------|---------------|---------|---------|--------|--------|--------|-----------------|--------|---------|---------------|
| MAE            | 1                | <b>0.1731</b> | 0.4552  | 0.2530  | 0.3151 | 0.3162 | 0.2835 | 0.2526          | 0.2466 | 0.3077  | 0.2943        |
|                | 8                | <b>0.2226</b> | 0.7191  | 0.4195  | 0.4368 | 0.4220 | 0.4169 | 0.3895          | 0.3537 | 0.3014  | 0.2727        |
|                | 16               | <b>0.2482</b> | 0.7131  | 0.5032  | 0.5184 | 0.5000 | 0.4921 | 0.4605          | 0.4043 | 0.3455  | 0.2932        |
| RMSE           | 1                | <b>0.2873</b> | 0.9234  | 0.5688  | 0.5778 | 0.5617 | 0.5672 | 0.5108          | 0.4680 | 0.4516  | 0.3721        |
|                | 8                | <b>0.3033</b> | 0.5861  | 0.4484  | 0.5073 | 0.5207 | 0.4658 | 0.4479          | 0.4041 | 0.4857  | 0.4536        |
|                | 16               | <b>0.3978</b> | 0.9354  | 0.6695  | 0.6811 | 0.6777 | 0.6693 | 0.6389          | 0.5856 | 0.5032  | 0.4472        |
| R <sup>2</sup> | 1                | <b>0.4540</b> | 0.9330  | 0.7910  | 0.7864 | 0.7860 | 0.7822 | 0.7385          | 0.6918 | 0.5633  | 0.4829        |
|                | 8                | <b>0.5024</b> | 1.0702  | 0.8567  | 0.8468 | 0.8434 | 0.8467 | 0.7824          | 0.7588 | 0.6862  | 0.5629        |
|                | 16               | <b>0.9704</b> | 0.8894  | 0.9353  | 0.9171 | 0.9127 | 0.9301 | 0.9354          | 0.9474 | 0.9240  | 0.9338        |
| BIAS           | 1                | <b>0.0065</b> | -0.0976 | -0.0033 | 0.0317 | 0.0369 | 0.0508 | 0.0071          | 0.0791 | 0.0224  | <b>0.0006</b> |
|                | 8                | -0.0097       | -0.1394 | 0.0296  | 0.0478 | 0.0306 | 0.0824 | - <b>0.0041</b> | 0.1132 | -0.0092 | -0.0249       |
|                | 16               | <b>0.0019</b> | 0.0613  | 0.0475  | 0.0436 | 0.0434 | 0.1061 | -0.0034         | 0.1104 | -0.0202 | -0.0408       |
| KGE            | 1                | <b>0.9839</b> | 0.8706  | 0.9527  | 0.9275 | 0.9234 | 0.9296 | 0.9462          | 0.9622 | 0.9070  | 0.8917        |
|                | 8                | <b>0.9730</b> | 0.8531  | 0.8805  | 0.8868 | 0.8892 | 0.8847 | 0.9007          | 0.9334 | 0.9316  | 0.9181        |
|                | 16               | <b>0.9541</b> | 0.6913  | 0.8380  | 0.8352 | 0.8451 | 0.8381 | 0.8603          | 0.9018 | 0.9121  | 0.9101        |
| 24             | <b>0.9423</b>    | 0.6404        | 0.8134  | 0.8088  | 0.8153 | 0.8067 | 0.8428 | 0.8787          | 0.8692 | 0.8888  |               |

**Note:** M1 (SVM), M2 (LightGBM), M3 (GRU), M4 (LSTM), M5 (Transformer), M6 (STL-Transformer), M7 (EMD-Transformer-LSTM), M8 (STL + VMD-CNN-LSTM) and M9 (VMD-CNN-LSTM) are in Table 5.

![Figure 9: Comparative box plots of absolute error distributions for different models. The y-axis is 'Absolute Error' ranging from -0.5 to 4.0. The x-axis lists 15 models: SVM, LightGBM, GRU, LSTM, Transformer, PatchTST, TimesNet, Autoformer, STL-Transformer, EMD-Transformer-LSTM, STL+VMD-CNN-LSTM, VMD-CNN-LSTM, and The proposed. Each model has a box plot showing the distribution of absolute errors. The 'The proposed' model shows the lowest median absolute error (0.17) and the smallest interquartile range, indicating superior performance. Other models like SVM and LightGBM show significantly higher median errors (around 1.2 and 1.3 respectively).](83dedc2074a453d13ce74cc2e1ae4ff5_img.jpg)

Figure 9: Comparative box plots of absolute error distributions for different models. The y-axis is 'Absolute Error' ranging from -0.5 to 4.0. The x-axis lists 15 models: SVM, LightGBM, GRU, LSTM, Transformer, PatchTST, TimesNet, Autoformer, STL-Transformer, EMD-Transformer-LSTM, STL+VMD-CNN-LSTM, VMD-CNN-LSTM, and The proposed. Each model has a box plot showing the distribution of absolute errors. The 'The proposed' model shows the lowest median absolute error (0.17) and the smallest interquartile range, indicating superior performance. Other models like SVM and LightGBM show significantly higher median errors (around 1.2 and 1.3 respectively).

**Fig. 9.** Comparative box plots of absolute error distributions for different models.

across different models, illustrating the characteristics of absolute error distributions in photovoltaic power forecasting for both the proposed model and baseline models. As shown in the figure, the proposed model in this study demonstrates the best performance. It achieves the lowest median error, indicating that prediction deviations are generally concentrated at a low level. Furthermore, its interquartile range and whisker range are the smallest, reflecting a more concentrated error distribution with less variability and highly stable prediction results. Additionally, no noticeable outliers are observed in the plot, indicating a significantly enhanced capability of the model to control predictions under extreme conditions and effectively avoid severe deviations. In summary, the proposed model in this study significantly outperforms the baseline models in all aspects, further validating its notable advantages in photovoltaic power forecasting tasks.

Table 4 presents the average total training time across multiple runs for each deep learning model. Additionally, an algorithmic complexity analysis of the proposed model is provided in the Supplementary Information. As shown in the table, the training time of the proposed model is higher than that of several other models. This is primarily attributed to the additional computational costs introduced by the secondary decomposition and the hybrid model architecture, yet the difference remains relatively modest. This moderate increase in computational cost enhances the reliability and practicality of the prediction results. However, it still represents a limitation, as the model makes a reasonable trade-off in computational efficiency in pursuit of higher predictive performance. Future research will explore the development of more computationally efficient models while striving to preserve their performance advantages.

## 4.3. Performance comparison between the proposed model and existing approaches

This section conducts a comparative analysis between the proposed model and existing forecasting approaches to demonstrate its enhanced performance. This experiment uses data from Site 1 to train and evaluate the overall comprehensive effectiveness of all models. The data allocation follows a 70:15:15 proportion across training, validation, and test partitions. The input sequence length and forecasting horizon are set to 72 and 24, respectively. To ensure comparison reliability, all compared models were constructed according to the original network architectures and parameter configurations as defined in their original literature.

Table 6 presents the comparative models and their descriptions. Su et al. [42] introduced a hybrid model combining Gated Recurrent Unit (GRU), dual attention mechanism, and an encoder-decoder framework for ultra-short-term photovoltaic power forecasting. Chen et al. [43] proposed a dual-perspective deep neural network that parallelly integrates GRU and Temporal Convolutional Network (TCN) for photovoltaic power forecasting. Gong et al. [35] developed a parallel model based on STL decomposition, integrating TimesNet for extracting two-dimensional periodic features and BiLSTM for capturing temporal dependencies. Renold et al. [44] presents a hybrid model combining a Temporal Convolutional Network, Efficient Channel Attention mechanism, and stacked Bidirectional LSTM-GRU. As presented in Table 6 and

the forecasting results of every model in Fig. 10, compared with previous model methods, the model proposed in this study exhibits stronger forecasting capability, achieving the best values in all five key metrics. This fully demonstrates its excellent capability in photovoltaic power forecasting tasks. It is particularly noteworthy that most comparative models in their original papers were designed for single-step or no more than ten-step photovoltaic power forecasting, whereas the forecasting horizon in this experiment is set to 24 steps, increasing the forecasting difficulty. This further highlights the superior robustness and generalization ability of the proposed model in this study.

# 5. Discussion

## 5.1. Predictive performance of the models at various sites

To test the generalization capability and operational stability of the proposed model, experimental data from Site 1 and Site 2 were selected for comparative experiments. The data allocation followed a 70:15:15 distribution across training, validation, and test sets. The experiment uses the most recent 72 time steps of sequential data as model input and directly outputs multi-step photovoltaic power forecasts for the next 24 time steps.

The overall performance metrics of different models evaluated across multiple sites are summarized in Table 7. According to Table 7, the presented model consistently outperforms the baseline models on the test sets of both independent sites (Site 1 and Site 2). Although its performance on the bias metric is slightly inferior to the optimal value, the difference is minimal. Meanwhile, the model demonstrates a clear advantage in key error metrics such as RMSE, MAE, and KGE, indicating significantly higher prediction accuracy compared to the benchmark

![Radar chart comparing the proposed method with previous prediction methods across five metrics: MAE, RMSE, R^2, BIAS, and KGE. The proposed method (red line) shows the best performance, particularly in RMSE, MAE, and KGE, while the baseline models (DA-GRU, Dv-DNN, STL-PA-TimesNet-BiLSTM, TCN-ECANet-Stacked BiLSTM-BiGRU) show relatively similar performance, with the proposed method slightly superior in BIAS.](e77321c92e46f4f20632d48cfebc312c_img.jpg)

Radar chart comparing the proposed method with previous prediction methods across five metrics: MAE, RMSE, R^2, BIAS, and KGE. The proposed method (red line) shows the best performance, particularly in RMSE, MAE, and KGE, while the baseline models (DA-GRU, Dv-DNN, STL-PA-TimesNet-BiLSTM, TCN-ECANet-Stacked BiLSTM-BiGRU) show relatively similar performance, with the proposed method slightly superior in BIAS.

Fig. 10. Radar chart comparing the proposed method with previous prediction methods.

**Table 6**

A comparison of the proposed method with previous prediction methods.

| Model                           | Study              | Description                                                                                                                              | MAE    | RMSE   | R <sup>2</sup> | BIAS   | KGE    |
|---------------------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------|--------|--------|----------------|--------|--------|
| DA-GRU                          | Su et al. [42]     | A GRU-based model integrated with a dual attention mechanism within an Encoder-Decoder framework                                         | 0.4433 | 0.7259 | 0.8284         | 0.1057 | 0.8681 |
| Dv-DNN                          | Chen et al. [43]   | A dual-view deep neural network that parallelly fuses GRU and TCN                                                                        | 0.4378 | 0.7162 | 0.8329         | 0.0664 | 0.8746 |
| STL-PA-TimesNet-BiLSTM          | Gong et al. [35]   | A parallel model combining TimesNet for periodic patterns and BiLSTM for long-term dependencies                                          | 0.4679 | 0.7197 | 0.8313         | 0.0218 | 0.8429 |
| TCN-ECANet-Stacked BiLSTM-BiGRU | Renold et al. [44] | A hybrid model combining Temporal Convolutional Networks, Efficient Channel Attention, stacked Bidirectional LSTM, and Bidirectional GRU | 0.5133 | 0.7542 | 0.8147         | 0.0537 | 0.8345 |
| The proposed                    | Ours               | The proposed model                                                                                                                       | 0.2326 | 0.4209 | 0.9423         | 0.0124 | 0.9647 |

**Table 7**

Overall performance metrics for each model across different sites.

| Model                | Site 1        |               |                |               |               | Site 2        |               |                |         |               |
|----------------------|---------------|---------------|----------------|---------------|---------------|---------------|---------------|----------------|---------|---------------|
|                      | MAE           | RMSE          | R <sup>2</sup> | BIAS          | KGE           | MAE           | RMSE          | R <sup>2</sup> | BIAS    | KGE           |
| SVM                  | 0.7354        | 0.9288        | 0.7190         | -0.1931       | 0.7808        | 0.5971        | 0.7627        | 0.7374         | -0.0630 | 0.7720        |
| LightGBM             | 0.4603        | 0.7335        | 0.8247         | 0.0359        | 0.8641        | 0.3615        | 0.6028        | 0.8360         | 0.0970  | 0.8719        |
| GRU                  | 0.4762        | 0.7351        | 0.8240         | 0.0494        | 0.8601        | 0.3707        | 0.5972        | 0.8390         | 0.0512  | 0.8659        |
| LSTM                 | 0.4625        | 0.7335        | 0.8248         | 0.0429        | 0.8650        | 0.3736        | 0.6142        | 0.8297         | 0.0970  | 0.8719        |
| Transformer          | 0.4561        | 0.7257        | 0.8285         | 0.0904        | 0.8592        | 0.3532        | 0.5924        | 0.8416         | 0.0763  | 0.8849        |
| PatchTST             | 0.4566        | 0.7503        | 0.8166         | 0.0598        | 0.8841        | 0.3760        | 0.6115        | 0.8312         | 0.0749  | 0.8766        |
| TimesNet             | 0.4734        | 0.7446        | 0.8194         | 0.1175        | 0.8601        | 0.4008        | 0.6336        | 0.8188         | 0.1845  | 0.8445        |
| Autoformer           | 0.4501        | 0.7273        | 0.8277         | 0.1085        | 0.8606        | 0.3882        | 0.6262        | 0.8230         | 0.1723  | 0.8765        |
| STL-Transformer      | 0.4210        | 0.6858        | 0.8468         | <b>0.0046</b> | 0.8820        | 0.3378        | 0.5715        | 0.8526         | 0.0258  | 0.8935        |
| EMD-Transformer-LSTM | 0.3752        | 0.6371        | 0.8678         | 0.1100        | 0.9191        | 0.3226        | 0.5210        | 0.8875         | -0.0463 | 0.9075        |
| STL + VMD-CNN-LSTM   | 0.3397        | 0.5510        | 0.9011         | -0.0062       | 0.9125        | 0.3188        | 0.5124        | 0.8815         | 0.0075  | 0.8872        |
| VMD-CNN-LSTM         | 0.2924        | 0.4713        | 0.9276         | -0.0253       | 0.9085        | 0.2485        | 0.4166        | 0.9235         | -0.0032 | 0.9149        |
| The proposed         | <b>0.2326</b> | <b>0.4209</b> | <b>0.9423</b>  | 0.0124        | <b>0.9647</b> | <b>0.2167</b> | <b>0.4012</b> | <b>0.9273</b>  | 0.0153  | <b>0.9534</b> |

models. This highlights its robust generalization capability and strong robustness. The proposed model maintains superior predictive accuracy across different data sets, further validating its exceptional generalization ability and robustness.

A subset of photovoltaic power data was randomly selected from the test sets of Site 1 and Site 2, and line charts comparing the predicted photovoltaic power outputs of ten models with the actual values were plotted, as shown in Figs. 11 and 12. The figures clearly demonstrate that the proposed model closely fits the actual photovoltaic power output. When significant fluctuations occur in the power output, the proposed model demonstrates the ability to approximate the overall trend while capturing most fluctuation details. In contrast, the predictions of other models exhibit noticeable deviations or lag. These results indicate the effectiveness and robustness of the proposed model in handling nonlinear and dynamic photovoltaic power data.

## 5.2. Model prediction capabilities under different weather conditions

To further evaluate the model's forecasting performance under different meteorological conditions, we conducted additional scenario analysis based on Section 4.2. According to the meteorological data, we categorized the test samples into three representative weather patterns: sunny days, cloudy days, and rainy days. We calculated evaluation metrics for each weather type, including RMSE, MAE, R<sup>2</sup>, BIAS, and KGE, to investigate the relationship between model performance and weather conditions. Evaluation results for the proposed model and nine

baseline models for forecasting under different weather conditions are presented in Table 8 and Fig. 13.

As shown in the table and figure results, the proposed model outperforms the nine baseline models across all three weather conditions. Under sunny conditions, while all models generally achieve high prediction accuracy, the proposed model demonstrates the lowest RMSE, MAE, and BIAS, indicating its superior fitting capability. Cloudy and rainy weather conditions present greater forecasting challenges, particularly on rainy days. During cloudy weather, most baseline models exhibit significant performance degradation compared to sunny conditions, suggesting their limited ability to capture rapidly changing patterns. In contrast, the proposed model shows minimal performance decline, maintaining the lowest RMSE and MAE, along with the highest R<sup>2</sup> and KGE values, reflecting its strong temporal feature extraction capability and effective modeling of nonlinear characteristics. Under rainy conditions, which involve complex climatic factors and present substantial forecasting difficulties, most baseline models nearly fail in prediction tasks. However, the proposed model still achieves remarkable performance (R<sup>2</sup> = 0.7958, BIAS = 0.8694) under these challenging conditions, demonstrating its reliable forecasting capability even in adverse weather scenarios.

Furthermore, Fig. 13 visually illustrates the performance distribution characteristics of various prediction models under different weather conditions using violin plots. Subplots (a), (b), and (c) correspond to sunny, cloudy, and overcast/rainy scenarios, respectively. In the sunny scenario, the prediction error distribution of the SVM model exhibits a

![Figure 11: Photovoltaic power prediction results for different models of partial test samples at Site 1. The plot shows PV Power (kW) on the y-axis (0 to 7) versus Time Points (5min-interval) on the x-axis (0 to 120). The legend includes: actual (red solid line), The proposed (blue solid line), SVM (orange dashed line), LightGBM (green dashed line), GRU (purple dashed line), LSTM (brown dashed line), Transformer (pink dashed line), STL-Transformer (cyan dashed line), EMD-Transformer-LSTM (magenta dashed line), STL+VMD-CNN-LSTM (olive dashed line), and VMD-CNN-LSTM (grey dashed line). The proposed model (blue) closely follows the actual power output (red), while other models show significant deviations and lag.](8e4f8c87efc168cac52580ce81583063_img.jpg)

Figure 11: Photovoltaic power prediction results for different models of partial test samples at Site 1. The plot shows PV Power (kW) on the y-axis (0 to 7) versus Time Points (5min-interval) on the x-axis (0 to 120). The legend includes: actual (red solid line), The proposed (blue solid line), SVM (orange dashed line), LightGBM (green dashed line), GRU (purple dashed line), LSTM (brown dashed line), Transformer (pink dashed line), STL-Transformer (cyan dashed line), EMD-Transformer-LSTM (magenta dashed line), STL+VMD-CNN-LSTM (olive dashed line), and VMD-CNN-LSTM (grey dashed line). The proposed model (blue) closely follows the actual power output (red), while other models show significant deviations and lag.

**Fig. 11.** Photovoltaic power prediction results for different models of partial test samples at Site 1.

![Figure 12: Photovoltaic power prediction results for different models of partial test samples at Site 2. The graph plots PV Power (kW) on the y-axis (0 to 7) against Time Points (5min-interval) on the x-axis (0 to 120). It compares actual data (solid black line) with predictions from 11 models: The proposed (solid red line), SVM (dashed orange line), LightGBM (dashed yellow line), GRU (dashed green line), LSTM (dashed blue line), Transformer (dashed purple line), STL-Transformer (dashed dark blue line), EMD-Transformer-LSTM (dashed pink line), STL-VMD-CNN-LSTM (dashed light blue line), STL-VMD-CNN-LSTM (dashed light green line), and VMD-CNN-LSTM (dashed light purple line). The proposed model closely follows the actual data across the entire time period.](177e8bc1c595b7fe3461d9919f87e044_img.jpg)

Figure 12: Photovoltaic power prediction results for different models of partial test samples at Site 2. The graph plots PV Power (kW) on the y-axis (0 to 7) against Time Points (5min-interval) on the x-axis (0 to 120). It compares actual data (solid black line) with predictions from 11 models: The proposed (solid red line), SVM (dashed orange line), LightGBM (dashed yellow line), GRU (dashed green line), LSTM (dashed blue line), Transformer (dashed purple line), STL-Transformer (dashed dark blue line), EMD-Transformer-LSTM (dashed pink line), STL-VMD-CNN-LSTM (dashed light blue line), STL-VMD-CNN-LSTM (dashed light green line), and VMD-CNN-LSTM (dashed light purple line). The proposed model closely follows the actual data across the entire time period.

Fig. 12. Photovoltaic power prediction results for different models of partial test samples at Site 2.

**Table 8**

Performance metrics of different models under varying weather conditions.

| Weather types      | Metric         | The proposed   | M1      | M2      | M3      | M4             | M5      | M6      | M7      | M8      | M9      |
|--------------------|----------------|----------------|---------|---------|---------|----------------|---------|---------|---------|---------|---------|
| Sunny              | MAE            | <b>0.1343</b>  | 0.6707  | 0.2828  | 0.2635  | 0.2475         | 0.2338  | 0.2270  | 0.2128  | 0.2253  | 0.2313  |
|                    | RMSE           | <b>0.2976</b>  | 0.8301  | 0.4785  | 0.4826  | 0.4664         | 0.4513  | 0.4399  | 0.4187  | 0.3994  | 0.3779  |
|                    | R <sup>2</sup> | <b>0.9629</b>  | 0.7116  | 0.9042  | 0.9025  | 0.9089         | 0.9148  | 0.9190  | 0.9266  | 0.9332  | 0.9402  |
| Cloudy             | BIAS           | <b>-0.0016</b> | -0.4756 | -0.0998 | -0.0160 | -0.0239        | -0.0215 | -0.0174 | -0.0183 | -0.0624 | -0.0817 |
|                    | KGE            | <b>0.9798</b>  | 0.8400  | 0.9158  | 0.9480  | 0.9459         | 0.9482  | 0.9508  | 0.9589  | 0.9294  | 0.9082  |
|                    | MAE            | <b>0.2368</b>  | 0.7168  | 0.4433  | 0.4607  | 0.4692         | 0.4338  | 0.4207  | 0.3804  | 0.3413  | 0.3056  |
| Overcast and rainy | RMSE           | <b>0.4302</b>  | 0.9019  | 0.7149  | 0.7160  | 0.7184         | 0.6954  | 0.6870  | 0.6370  | 0.5518  | 0.4863  |
|                    | R <sup>2</sup> | <b>0.9289</b>  | 0.6875  | 0.8037  | 0.8031  | 0.8017         | 0.8143  | 0.8187  | 0.8441  | 0.8831  | 0.9091  |
|                    | BIAS           | <b>0.0058</b>  | -0.3082 | -0.0142 | -0.0225 | <b>-0.0029</b> | 0.0231  | -0.0249 | 0.0620  | -0.0303 | -0.0222 |
|                    | KGE            | <b>0.9611</b>  | 0.7941  | 0.8692  | 0.8693  | 0.8596         | 0.8734  | 0.8922  | 0.9146  | 0.9116  | 0.8817  |
|                    | MAE            | <b>0.3594</b>  | 0.8666  | 0.7517  | 0.7555  | 0.8465         | 0.7932  | 0.6582  | 0.5984  | 0.5000  | 0.4043  |
|                    | RMSE           | <b>0.5311</b>  | 1.1017  | 1.0107  | 1.0152  | 1.0854         | 1.0435  | 0.9252  | 0.8845  | 0.6938  | 0.5707  |
|                    | R <sup>2</sup> | <b>0.7958</b>  | 0.1216  | 0.2607  | 0.2541  | 0.1474         | 0.2119  | 0.3805  | 0.4839  | 0.6516  | 0.7643  |
|                    | BIAS           | <b>0.0170</b>  | 0.4565  | 0.3393  | 0.3474  | 0.5206         | 0.4665  | 0.1934  | 0.2384  | 0.1121  | 0.0841  |
|                    | KGE            | <b>0.8694</b>  | 0.4721  | 0.5523  | 0.5611  | 0.4826         | 0.5270  | 0.6417  | 0.7124  | 0.7477  | 0.7690  |

significantly wider spread, with both the kernel density range and dispersion markedly higher than those of the other models. In contrast, the proposed model and the remaining models show highly concentrated distributions with medians close to zero. This indicates that under favorable solar irradiance conditions, all models yield relatively small and concentrated prediction errors, reflecting stable predictive performance. In the cloudy scenario, the prediction error distributions begin to diverge more noticeably. The proposed model demonstrates the most compact distribution, with the optimal median value closest to zero, clearly indicating its superior predictive performance under cloudy weather conditions. Under the complex weather conditions of overcast and rainy days, the proposed model still maintains the most concentrated error distribution compared to other models, with a median value nearly equal to zero and the lowest degree of dispersion in prediction errors, indicating the strongest adaptability to challenging weather scenarios. Overall, the proposed model demonstrates smaller prediction errors and more stable performance across all weather conditions, highlighting its superiority in photovoltaic power generation forecasting under varying environmental circumstances.

## 5.3. Comparison of predictive performance of various models across various seasons

This work further verifies the dependability of the model's forecasts and evaluates their performance across seasonal changes. The dataset

from Site 1, covering the period from March 2015 to March 2016, was selected and separated into four independent seasonal datasets: spring, summer, autumn, and winter. Each seasonal dataset was partitioned into training, validation, and test sets employing an 8:1:1 ratio. The input and output sequence lengths for this experiment were set to 72 and 12, respectively. The forecasting performance results of the presented model and the nine baseline models across the four seasons are shown in Fig. 14, where the BIAS values are presented as absolute values. The forecasting performance of different models during summer and winter is detailed in Tables 9 and 10, while the corresponding results for spring and autumn are provided in Supplementary Information Table S1 and Table S2.

As shown in the table and figure results, the proposed model exhibits outstanding comprehensive performance throughout all seasons against all benchmark models. During summer forecasting, the proposed model achieves optimal performance in four metrics ( $R^2 = 0.9510$ ,  $MAE = 0.1916$ ,  $RMSE = 0.3190$ ,  $BIAS = 0.0118$ ), with only the KGE metric slightly lower than the EMD-Transformer-LSTM model. In winter, the proposed model still maintains the best comprehensive performance ( $R^2 = 0.8633$ ,  $MAE = 0.4092$ ,  $RMSE = 0.6029$ ,  $KGE = 0.9089$ ). The experimental results on datasets from all four seasons indicate that the proposed model possesses strong forecasting stability and generalization capability when dealing with different seasonal climate characteristics.

Furthermore, to comprehensively evaluate model performance from multiple dimensions, we integrated the correlation coefficient, centered

![Figure 13: Violin plots of the performance distribution features of each model under different weather conditions. The figure consists of three subplots: (a) Sunny, (b) Cloudy, and (c) Rainy. Each subplot shows the performance distribution of ten models: SVM, LightGBM, GRU, LSTM, Transformer, STL-Transformer, EMD-Transformer-LSTM, STL+VMD-CNN-LSTM, VMD-CNN-LSTM, and The proposed. The plots are semi-circular, with the horizontal axis representing the median performance and the vertical axis representing the standard deviation. A reference point is shown at the top of each plot. The 'The proposed' model consistently shows the smallest spread and is closest to the reference point across all weather conditions. A legend on the right explains the symbols: a solid black line for Median, a red triangle for Maximum, a dashed red line for Upper Reference, and a dashed blue line for Lower Reference. A separate legend below the plots identifies the ten models by color.](b3df5964338063224492c01f09e4fed6_img.jpg)

Figure 13: Violin plots of the performance distribution features of each model under different weather conditions. The figure consists of three subplots: (a) Sunny, (b) Cloudy, and (c) Rainy. Each subplot shows the performance distribution of ten models: SVM, LightGBM, GRU, LSTM, Transformer, STL-Transformer, EMD-Transformer-LSTM, STL+VMD-CNN-LSTM, VMD-CNN-LSTM, and The proposed. The plots are semi-circular, with the horizontal axis representing the median performance and the vertical axis representing the standard deviation. A reference point is shown at the top of each plot. The 'The proposed' model consistently shows the smallest spread and is closest to the reference point across all weather conditions. A legend on the right explains the symbols: a solid black line for Median, a red triangle for Maximum, a dashed red line for Upper Reference, and a dashed blue line for Lower Reference. A separate legend below the plots identifies the ten models by color.

Fig. 13. Violin plots of the performance distribution features of each model under different weather conditions.

root mean square error (CRMSE), and standard deviation into Taylor diagrams. These diagrams provide a visual comparison of the correlation, error magnitude, and standard deviation consistency of each model's predictive performance across different seasons, as illustrated in Fig. 15. During the spring, the proposed model most closely approximates the reference point among all models. In contrast, models such as SVM and LSTM exhibit significantly larger CRMSE values, and their correlation coefficients deviate further from the reference line, indicating weaker accuracy and stability in spring predictions. In the summer, both the proposed model and several benchmark models maintain strong predictive accuracy; however, the proposed model still maintains the smallest radial distance. In autumn and winter, the proposed model exhibits a distinct advantage, being the closest to the reference point among all comparison models and demonstrating the strongest correlation, which indicates its strong adaptability and robustness. Overall, the proposed model performs excellently in photovoltaic power generation forecasting across different seasons, demonstrating its robustness and reliability under varying environmental conditions.

## 5.4. Robustness testing

In industrial scenarios, the introduction of noise and outliers during data acquisition and transmission is an inherent phenomenon. Such data contamination leads to degradation in dataset quality, causing distortion in the physical processes reflected by portions of the data [45]. For assessing the model's stability under noise-contaminated conditions, this experiment employs a Gaussian noise injection method to simulate common data perturbations encountered in practical applications. Gaussian noise effectively simulates sensor measurement errors, transient environmental interference, and random fluctuations in data acquisition systems. This experiment uses the dataset from Site 1 for model training. The noise type is zero-mean Gaussian white noise, injected into 2% of the training set data with a noise intensity of 0.5. The evaluation metrics are compared before and after noise injection.

To more intuitively reflect the model's robustness, a weighted comprehensive robustness score is adopted to assess the model's effectiveness in noisy environments. A value closer to 1 indicates stronger model robustness. The calculation formula is as follows:

$$Score = \omega_1 S_{MAE} + \omega_2 S_{RMSE} \quad (33)$$

Where  $S_{MAE} = \min\left(1, \frac{MAE_{clean}}{\max(MAE_{noisy}, 0)}\right)$ ,  $S_{RMSE} = \min\left(1, \frac{RMSE_{clean}}{\max(RMSE_{noisy}, 0)}\right)$ , and  $\omega$  is the weighting factor. The weighting is set based on the practical application value of photovoltaic power prediction in the power grid. Specifically, MAE measures the model's average forecasting precision and is closely related to the long-term economic dispatch of the power grid. However, RMSE is more sensitive to extreme prediction errors. In real-world scenarios, drastic power prediction fluctuations present a significant risk to the frequency stability and power quality of the power grid and may lead to high costs. Therefore, suppressing the occurrence of large errors is crucial for maintaining the secure and reliable functioning of the power system. Thus, in this experiment, the values of  $\omega_1$  and  $\omega_2$  are 0.4 and 0.6, respectively.

As shown in Table 11, under the simulated environment with introduced Gaussian noise, the robustness scores of the comparative models show significant differences. The model developed in this research achieved the highest score of 0.9586 in this test, significantly outperforming all nine benchmark models and demonstrating its exceptional stability and generalization capability under noise interference. The robustness score of the proposed model is approximately 5.25% higher than that of the second-best STL-Transformer model (0.9108), with even more pronounced advantages over other benchmark models. This indicates that the proposed hybrid architecture exhibits low sensitivity to disturbances in input data, possesses strong feature extraction and retention capabilities, and further confirms its effectiveness in noise resistance. These results demonstrate that the model is better suited for practical industrial scenarios with fluctuating data quality.

## 5.5. Explainability analysis

This study also incorporates SHAP analysis during the forecasting process to evaluate the interpretability between input variables and output variables. The analytical findings are presented in Figs. 16 and 17.

As illustrated in Fig. 16, the upper axis corresponds to the bar chart,

![Legend for the radar charts showing performance metrics for various models: SVM (blue), LightGBM (dark blue), GRU (green), LSTM (purple), Transformer (yellow), STL-Transformer (light blue), EMD-Transformer-LSTM (brown), STL+VMD-CNN-LSTM (olive), VMD-CNN-LSTM (orange), and The proposed (red).](f4d72193f77f6646a2a1f4baaa927154_img.jpg)

Legend for the radar charts showing performance metrics for various models: SVM (blue), LightGBM (dark blue), GRU (green), LSTM (purple), Transformer (yellow), STL-Transformer (light blue), EMD-Transformer-LSTM (brown), STL+VMD-CNN-LSTM (olive), VMD-CNN-LSTM (orange), and The proposed (red).

![Four radar charts (a) Spring, (b) Summer, (c) Autumn, and (d) Winter comparing the performance of the proposed model and nine benchmark models across five metrics: BIAS, R², MAE, RMSE, and KGE. The proposed model (red line) consistently shows the best performance across all seasons and metrics.](fed39b841ae2dce01088b84bfc1e2789_img.jpg)

Four radar charts (a) Spring, (b) Summer, (c) Autumn, and (d) Winter comparing the performance of the proposed model and nine benchmark models across five metrics: BIAS, R², MAE, RMSE, and KGE. The proposed model (red line) consistently shows the best performance across all seasons and metrics.

**Fig. 14.** Radar chart of the overall forecasting performance metrics for the proposed model and benchmark models on the complete test set of Site 1 (across all four seasons).

**Table 9**

The overall predictive performance metrics of the proposed model and nine benchmark models on the entire test set of Site 1 (Summer).

| Metrics              | MAE           | RMSE          | R <sup>2</sup> | BIAS          | KGE           |
|----------------------|---------------|---------------|----------------|---------------|---------------|
| SVM                  | 0.8957        | 1.0892        | 0.4292         | -0.2295       | 0.4416        |
| LightGBM             | 0.4061        | 0.5772        | 0.8401         | -0.2279       | 0.8598        |
| GRU                  | 0.3216        | 0.4866        | 0.8861         | -0.1372       | 0.8454        |
| LSTM                 | 0.3707        | 0.5274        | 0.8665         | -0.1278       | 0.8411        |
| Transformer          | 0.3517        | 0.5253        | 0.8672         | <b>0.0038</b> | 0.8018        |
| STL-Transformer      | 0.3265        | 0.4965        | 0.8814         | -0.1507       | 0.9297        |
| EMD-Transformer-LSTM | 0.2889        | 0.4445        | 0.9049         | 0.0172        | <b>0.9382</b> |
| STL + VMD-CNN-LSTM   | 0.3533        | 0.4813        | 0.8885         | -0.1222       | 0.8340        |
| VMD-CNN-LSTM         | 0.2402        | 0.3798        | 0.9306         | 0.0344        | 0.9231        |
| The proposed         | <b>0.1916</b> | <b>0.3190</b> | <b>0.9510</b>  | 0.0118        | 0.9201        |

**Table 10**

The overall predictive performance metrics of the proposed model and nine benchmark models on the entire test set of Site 1 (Winter).

| Metrics              | MAE           | RMSE          | R <sup>2</sup> | BIAS          | KGE           |
|----------------------|---------------|---------------|----------------|---------------|---------------|
| SVM                  | 1.2203        | 1.4176        | 0.2452         | -0.3129       | 0.1901        |
| LightGBM             | 0.6043        | 0.8695        | 0.7158         | 0.1029        | 0.8082        |
| GRU                  | 0.6502        | 0.8767        | 0.7110         | 0.0379        | 0.8006        |
| LSTM                 | 0.6495        | 0.9173        | 0.6837         | 0.2956        | 0.7999        |
| Transformer          | 0.7208        | 0.9106        | 0.6883         | -0.2146       | 0.7533        |
| STL-Transformer      | 0.6017        | 0.8878        | 0.7036         | 0.1135        | 0.8083        |
| EMD-Transformer-LSTM | 0.6500        | 0.9202        | 0.6816         | 0.2320        | 0.7858        |
| STL + VMD-CNN-LSTM   | 0.5473        | 0.8171        | 0.7490         | 0.0239        | 0.8566        |
| VMD-CNN-LSTM         | 0.4700        | 0.7127        | 0.8090         | <b>0.0515</b> | 0.8988        |
| The proposed         | <b>0.4092</b> | <b>0.6029</b> | <b>0.8633</b>  | -0.0528       | <b>0.9089</b> |

indicating feature importance. The lower axis corresponds to the bee swarm plot, showing the distribution of feature impacts. Features with deeper red colors demonstrate higher values, while deeper blue colors demonstrate lower values; positive SHAP values contribute favorably to prediction outcomes, whereas negative values exert an adverse effect on the results. The feature Global Horizontal Radiation has the highest importance, reaching 35.63%. Additionally, components IMF1, Weather Relative Humidity, IMF2, and the seasonal component also contribute significantly to photovoltaic power forecasting, reflecting the multi-dimensional dependencies of photovoltaic output on physical

mechanisms and temporal non-stationarity. It is worth noting that all components obtained through VMD decomposition have substantial impacts on the predictions, further validating the effectiveness of the secondary decomposition strategy for the residual component. Overall, all input variables contribute meaningfully to the forecasting results, demonstrating that the feature selection method adopted in this study effectively retains critical information. As shown in Fig. 17, the specific impacts of changes in each variable on the output can be observed. The figure displays dependency plots for nine key features, with the remaining dependency plots provided in Fig. S1 of the Supplementary

![Figure 15: Taylor diagrams of predictive performance for various models across different seasons. The figure consists of four subplots: (a) Spring, (b) Summer, (c) Autumn, and (d) Winter. Each subplot shows a Taylor diagram with 'Standard Deviation' on the vertical axis and 'Observation' on the horizontal axis. The radial axis represents the 'Correlation Coefficient' from 0.0 to 1.0. Data points for various models are plotted, and the 'RMSE' is indicated for each model. The legend includes: Obs (red triangle), The proposed (red star), SVM (blue square), LightGBM (green diamond), GRU (purple triangle), LSTM (yellow triangle), Transformer (orange triangle), STL-Transformer (pink triangle), EMD-Transformer-LSTM (grey circle), STL+VMD-CNN-LSTM (olive circle), and VMD-CNN-LSTM (cyan cross).](b6750d26d3dd287a4a4d49b3670a44bd_img.jpg)

Figure 15: Taylor diagrams of predictive performance for various models across different seasons. The figure consists of four subplots: (a) Spring, (b) Summer, (c) Autumn, and (d) Winter. Each subplot shows a Taylor diagram with 'Standard Deviation' on the vertical axis and 'Observation' on the horizontal axis. The radial axis represents the 'Correlation Coefficient' from 0.0 to 1.0. Data points for various models are plotted, and the 'RMSE' is indicated for each model. The legend includes: Obs (red triangle), The proposed (red star), SVM (blue square), LightGBM (green diamond), GRU (purple triangle), LSTM (yellow triangle), Transformer (orange triangle), STL-Transformer (pink triangle), EMD-Transformer-LSTM (grey circle), STL+VMD-CNN-LSTM (olive circle), and VMD-CNN-LSTM (cyan cross).

Fig. 15. Taylor diagrams of predictive performance for various models across different seasons.

**Table 11**

Robustness scores of different models in noisy environments.

| Model                | Score  |
|----------------------|--------|
| SVM                  | 0.6223 |
| LightGBM             | 0.7397 |
| GRU                  | 0.8693 |
| LSTM                 | 0.8597 |
| Transformer          | 0.8806 |
| STL-Transformer      | 0.9108 |
| EMD-Transformer-LSTM | 0.8974 |
| STL + VMD-CNN-LSTM   | 0.8046 |
| VMD-CNN-LSTM         | 0.6687 |
| The proposed         | 0.9586 |

Information. Taking IMF1 as an example, the plot shows that when  $IMF2 < 0.55$ , the SHAP value is negative, indicating an inhibitory effect of this feature on the prediction results. When  $IMF2 > 0.55$ , the SHAP value becomes positive, and the feature exhibits a promotive effect on the prediction results. Additionally,  $R^2 = 99.4\%$  reflects the high goodness of fit of this dependency relationship.

The proposed model in this study demonstrates good interpretability and provides an efficient and feasible approach for photovoltaic power forecasting. Overall, these analysis results provide in-depth insights into the importance and impacts of different features in the model, offering valuable references for future model optimization and adjustment.

# 6. Conclusion

Photovoltaic power is influenced by meteorological factors, characterized by high volatility and randomness. This study proposes a physics-constrained multi-step short-term forecasting method for photovoltaic power. In this study, a physics-constrained hybrid Transformer-LSTM model built upon STL and VMD secondary decomposition is presented for short-term photovoltaic power forecasting. An improved DOA is employed to optimize the hyperparameters of both VMD and the forecasting model. Two Australian datasets are selected for experimental validation, and comparisons are made with nine benchmark models. Additionally, ablation experiments are carried out to validate the performance of each constituent module in the presented model. Furthermore, comparative experiments are conducted to assess the forecasting performance of the presented model. We also discuss the model's performance across different seasons and weather conditions. Moreover, noise interference is introduced in experiments to test the model's robustness in distorted data environments. Finally, interpretability analysis is performed to reveal the intrinsic relationships between input features and forecasting results. The primary conclusions are summarized as follows:

- (1) The secondary decomposition strategy combining STL and VMD can capture deeper-level variations in photovoltaic power, significantly enhancing forecasting performance. In the ablation experiments, relative to the Transformer-LSTM model, the STL + VMD-Transformer-LSTM model reduced RMSE by 44.08%,

![SHAP Feature Importance Analysis chart. The chart shows the Mean (SHAP value) and SHAP value (impact on model output) for various features. The features are ranked by their Mean SHAP value, with Global_Horizontal_Radiation having the highest mean value at 0.09. The SHAP values range from -0.15 to 0.33. A color bar on the right indicates the Feature value from Low (blue) to High (red).](7bed2d7c96d86bf922295a1252da52a5_img.jpg)

| Feature                     | Mean (SHAP value) |
|-----------------------------|-------------------|
| Global_Horizontal_Radiation | 0.09              |
| IMF1                        | 0.07              |
| Weather_Relative_Humidity   | 0.06              |
| IMF2                        | 0.05              |
| seasonal                    | 0.04              |
| IMF5                        | 0.03              |
| IMF4                        | 0.02              |
| IMF3                        | 0.01              |
| IMF6                        | 0.01              |
| trend                       | 0.01              |
| Weather_Temperature_Celsius | 0.01              |
| Wind_Speed                  | 0.01              |
| Radiation_Global_Tilted     | 0.01              |

SHAP Feature Importance Analysis chart. The chart shows the Mean (SHAP value) and SHAP value (impact on model output) for various features. The features are ranked by their Mean SHAP value, with Global\_Horizontal\_Radiation having the highest mean value at 0.09. The SHAP values range from -0.15 to 0.33. A color bar on the right indicates the Feature value from Low (blue) to High (red).

Fig. 16. Feature importance analysis chart.

![SHAP dependency graph showing the relationship between SHAP Value and feature values for nine features. Each plot includes the R-squared value and p-value. The features are Global_Horizontal_Radiation (R² = 99.5%, p < 0.01), IMF1 (R² = 99.8%, p < 0.01), Weather_Relative_Humidity (R² = 97.4%, p < 0.01), IMF2 (R² = 99.4%, p < 0.01), seasonal (R² = 99.1%, p < 0.01), IMF5 (R² = 99.9%, p < 0.01), IMF4 (R² = 96.8%, p < 0.01), IMF3 (R² = 94.2%, p < 0.01), and IMF6 (R² = 99.9%, p < 0.01). The plots show a positive correlation for most features, with IMF6 showing a more complex, oscillating relationship.](3468bcffa38de23cef94bfb460ccb301_img.jpg)

SHAP dependency graph showing the relationship between SHAP Value and feature values for nine features. Each plot includes the R-squared value and p-value. The features are Global\_Horizontal\_Radiation (R² = 99.5%, p < 0.01), IMF1 (R² = 99.8%, p < 0.01), Weather\_Relative\_Humidity (R² = 97.4%, p < 0.01), IMF2 (R² = 99.4%, p < 0.01), seasonal (R² = 99.1%, p < 0.01), IMF5 (R² = 99.9%, p < 0.01), IMF4 (R² = 96.8%, p < 0.01), IMF3 (R² = 94.2%, p < 0.01), and IMF6 (R² = 99.9%, p < 0.01). The plots show a positive correlation for most features, with IMF6 showing a more complex, oscillating relationship.

Fig. 17. SHAP dependency graph.

decreased MAE by 49.11%, and improved  $R^2$  by 15.99%. When benchmarked against the STL-Transformer-LSTM model, the proposed model achieved a 39.13% reduction in RMSE, a 43.48% decrease in MAE, and an 11.93% improvement in  $R^2$ .

(2) The proposed physics-constrained loss function effectively ensures the model's predictions adhere to fundamental physical principles, thereby further enhancing its predictive capability. In the ablation experiments, compared to the STL + VMD-

Transformer-LSTM model, the proposed model reduced RMSE by 1.1% and decreased MAE by 1.48%.

- (3) In the comparative experiments, compared against all selected reference models and prior prediction techniques, the proposed approach showed substantially enhanced comprehensive capability, fully validating its advancement and effectiveness.
- (4) In experiments conducted on two distinct data sets, the proposed model exhibited superior overall predictive performance, achieving excellent results on both. This unequivocally proves the model's exceptional generalization capability and stable prediction capability.
- (5) In the comparison of forecasting performance across different weather conditions, the proposed model outperforms the benchmark models under all weather types, particularly demonstrating more significant advantages during rainy conditions compared to other models. On the four seasonal datasets, the comprehensive metrics of the presented model are superior to those of the nine benchmark models. This demonstrates that the presented model maintains high reliability and accuracy across different seasons and weather conditions.
- (6) In the robustness testing, when faced with noisy data, the proposed model in this study achieved the highest comprehensive robustness score. This demonstrates its significant advantage in noise resistance.

In future research, the effects of noise and data preprocessing on forecasting accuracy warrant further investigation. Some components

derived from data decomposition may adversely affect photovoltaic power forecasting accuracy, making refined feature selection a potential direction for future studies. Furthermore, the proposed model still possesses potential for enhancement, with ongoing efforts aimed at improving its precision in subsequent research to enhance overall forecasting performance.

# CRediT authorship contribution statement

**Jiahao Zou:** Writing – review & editing, Writing – original draft, Software, Methodology, Conceptualization. **Zhaocai Wang:** Writing – original draft, Validation, Supervision, Software, Methodology. **Zhaoyang Zhu:** Validation. **Zuowen Tan:** Data curation.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgement

This study was supported by the Humanities and Social Science Fund of Ministry of Education of China, China (No. 24YJAZH167), the Soft Science Project of Shanghai, China (No. 25692108900), and the National Statistical Science Research Project of China, China (No. 2025LY082).

# Appendix A. Supplementary data

Supplementary data to this article can be found online at <https://doi.org/10.1016/j.energy.2026.140314>.

# Appendix A Nomenclature

| Abbreviation | Full name                                                          | Abbreviation | Full name                                  |
|--------------|--------------------------------------------------------------------|--------------|--------------------------------------------|
| PVPG         | Photovoltaic power generation                                      | LSTM         | Long short-term memory                     |
| STL          | Seasonal and trend decomposition using loess                       | MAOA         | Modified Archimedes optimization algorithm |
| DOA          | Dream optimization algorithm                                       | CNN          | Convolutional neural networks              |
| RNN          | Recurrent neural network                                           | BO           | Bayesian optimization                      |
| CEEMD        | Complete ensemble empirical mode decomposition                     | BILSTM       | Bidirectional long short-term memory       |
| EMD          | Empirical mode decomposition                                       | TCN          | Temporal convolutional network             |
| CEEMDAN      | Complete ensemble empirical mode decomposition with adaptive noise | GRU          | Gated recurrent unit                       |
| BiGRU        | Bidirectional gated recurrent unit                                 | MSE          | Mean square error                          |
| SSA          | Singular spectrum analysis                                         | GA           | Genetic algorithm                          |
| PSO          | Particle swarm optimization                                        | WOA          | Whale optimization algorithm               |
| FOX          | Fox optimization algorithm                                         | IMF          | Intrinsic mode function                    |
| VMD          | Variational mode decomposition                                     | KELM         | Kernel extreme learning machine            |
| GAT          | Graph attention network                                            | SVM          | Support vector machine                     |
| LightGBM     | Light gradient boosting machine                                    | MAE          | Mean absolute error                        |
| RMSE         | Root mean square error                                             | KGE          | Kling-Gupta efficiency                     |
| ICMIC        | Iterative Chaotic Map with Infinite Collapses                      | DKASC        | Desert Knowledge Australia Solar Center    |

# Data availability

Data will be made available on request.

# References

- [1] Ma Y, Yu W, Zhu J, You Z, Jia A. Research on ultra-short-term photovoltaic power forecasting using multimodal data and ensemble learning. *Energy* 2025;330: 136831. <https://doi.org/10.1016/j.energy.2025.136831>.
- [2] Luo X, Zhang D, Zhu X. Combining transfer learning and constrained long short term memory for power generation forecasting of newly-constructed photovoltaic plants. *Renew Energy* 2022;185:1062–2077. <https://doi.org/10.1016/j.renene.2021.12.104>.
- [3] Hu Z, Gao Y, Ji S, Mae M, Imaizumi T. Improved multistep ahead photovoltaic power prediction model based on LSTM and self-attention with weather forecast data. *Appl Energy* 2024;359:122709. <https://doi.org/10.1016/j.apenergy.2024.122709>.
- [4] Zhang Z, Wang J, Wei D, Xia Y. An improved temporal convolutional network with attention mechanism for photovoltaic generation forecasting. *Eng Appl Artif Intell* 2023;123:106273. <https://doi.org/10.1016/j.engappai.2023.106273>.
- [5] Weyll A, Kitagawa Y, Araujo M, Ramos D, Lima F, dos Santos T, et al. Medium-term forecasting of global horizontal solar radiation in Brazil using machine learning-based methods. *Energy* 2024;300:131549. <https://doi.org/10.1016/j.energy.2024.131549>.
- [6] Jung Y, Jung J, Kim B, Han S. Long short-term memory recurrent neural network for modeling temporal patterns in long-term power forecasting for solar PV facilities: case study of South Korea. *J Clean Prod* 2020;250:119476. <https://doi.org/10.1016/j.jclepro.2019.119476>.
- [7] Li Q, Zhang X, Ma T, Jiao C, Wang H, Hu W. A multi-step ahead photovoltaic power prediction model based on similar day, enhanced colliding bodies optimization, variational mode decomposition, and deep extreme learning machine. *Energy* 2021;224:120094. <https://doi.org/10.1016/j.energy.2021.120094>.
- [8] Khan Z, Hussain T, Baik S. Dual stream network with attention mechanism for photovoltaic power forecasting. *Appl Energy* 2023;338:120916. <https://doi.org/10.1016/j.apenergy.2023.120916>.
- [9] Zhao Z, Chen N. An exponential smoothing multi-head graph attention network (ESMGAT) method for damage zone localization on wind turbine blades. *Compos Struct* 2024;342:118224. <https://doi.org/10.1016/j.compstruct.2024.118224>.
- [10] Gao X, Zang Y, Ma Q, Liu M, Cui Y, Dang D. A physics-constrained deep learning framework enhanced with signal decomposition for accurate short-term photovoltaic power generation forecasting. *Energy* 2025;326:136220. <https://doi.org/10.1016/j.energy.2025.136220>.
- [11] Jia D, Yang L, Lv T, Liu W, Gao X, Zhou J. Evaluation of machine learning models for predicting daily global and diffuse radiation under different weather/pollution conditions. *Renew Energy* 2022;187:896–906. <https://doi.org/10.1016/j.renene.2022.02.002>.
- [12] Li J, Rao C, Gao M, Xiao X, Goh M. Efficient calculation of distributed photovoltaic power generation power prediction via deep learning. *Renew Energy* 2025;246:122906. <https://doi.org/10.1016/j.renene.2025.122901>.
- [13] Li R, Wang D, Wang Z, Liang S, Li Z, Xie Y, et al. Transformer approach to nowcasting solar energy using geostationary satellite data. *Appl Energy* 2025;377:124387. <https://doi.org/10.1016/j.apenergy.2024.124387>.
- [14] Shi C, Su Z, Zhang K, Xie X, Zhang X. CloudSwinNet: a hybrid CNN-transformer framework for ground-based cloud images fine-grained segmentation. *Energy* 2024;309:133128. <https://doi.org/10.1016/j.energy.2024.133128>.
- [15] Wang L, Mao M, Xie J, Liao Z, Zhang H, Li H. Accurate solar PV power prediction interval method based on frequency-domain decomposition and LSTM model. *Energy* 2023;262:125592. <https://doi.org/10.1016/j.energy.2022.125592>.
- [16] Agga A, Abbou A, Labbadi M, El Houm Y, Ali I. CNN-LSTM: an efficient hybrid deep learning architecture for predicting short-term photovoltaic power production. *Elec Power Syst Res* 2022;208:107908. <https://doi.org/10.1016/j.epsr.2022.107908>.
- [17] Zhang M, Han Y, Wang C, Yang P, Wang C, Zalhaf A. Ultra-short-term photovoltaic power prediction based on similar day clustering and temporal convolutional network with bidirectional long short-term memory model: a case study using DKASC data. *Appl Energy* 2024;375:124085. <https://doi.org/10.1016/j.apenergy.2024.124085>.
- [18] Rai A, Shrivastava A, Jana K. Differential attention net: Multi-directed differential attention based hybrid deep learning model for solar power forecasting. *Energy* 2023;263:125746. <https://doi.org/10.1016/j.energy.2022.125746>.
- [19] Liu J, Li T. Multi-step power forecasting for regional photovoltaic plants based on ITDE-GAT model. *Energy* 2024;293:130468. <https://doi.org/10.1016/j.energy.2024.130468>.
- [20] Wang X, Sun Y, Luo D, Peng J. Comparative study of machine learning approaches for predicting short-term photovoltaic power output based on weather type classification. *Energy* 2022;240:122733. <https://doi.org/10.1016/j.energy.2021.122733>.
- [21] Lin W, Zhang B, Li H, Lu R. Multi-step prediction of photovoltaic power based on two-stage decomposition and BiLSTM. *Neurocomputing* 2022;504:56–67. <https://doi.org/10.1016/j.neucom.2022.06.117>.
- [22] Habib M, Hossain M. Advanced feature engineering in microgrid PV forecasting: a fast computing and data-driven hybrid modeling framework. *Renew Energy* 2024;235:121258. <https://doi.org/10.1016/j.renene.2024.121258>.
- [23] Xiao F, Wang X, Hou W, Zhang X, Wang J. An attention-based Bayesian sequence to sequence model for short-term solar power generation prediction within decomposition-ensemble strategy. *J Clean Prod* 2023;416:137827. <https://doi.org/10.1016/j.jclepro.2023.137827>.
- [24] Lin H, Gao L, Cui M, Liu H, Li C, Yu M. Short-term distributed photovoltaic power prediction based on temporal self-attention mechanism and advanced signal decomposition techniques with feature fusion. *Energy* 2025;315:134395. <https://doi.org/10.1016/j.energy.2025.134395>.
- [25] Wang X, Ma W. A hybrid deep learning model with an optimal strategy based on improved VMD and transformer for short-term photovoltaic power forecasting. *Energy* 2024;295:131071. <https://doi.org/10.1016/j.energy.2024.131071>.
- [26] Liu X, Liu Y, Kong X, Ma L, Besheer A, Lee K. Deep neural network for forecasting of photovoltaic power based on wavelet packet decomposition with similar day analysis. *Energy* 2023;271:126963. <https://doi.org/10.1016/j.energy.2023.126963>.
- [27] Liu Q, Li Y, Jiang H, Chen Y, Zhang J. Short-term photovoltaic power forecasting based on multiple mode decomposition and parallel bidirectional long short term combined with convolutional neural networks. *Energy* 2024;286:129580. <https://doi.org/10.1016/j.energy.2023.129580>.
- [28] Zhen H, Niu D, Wang K, Shi Y, Ji Z, Xu X. Photovoltaic power forecasting based on GA improved Bi-LSTM in microgrid without meteorological information. *Energy* 2021;231:120908. <https://doi.org/10.1016/j.energy.2021.120908>.
- [29] Chen X, Ding K, Zhang J, Han W, Liu Y, Yang Z, et al. Online prediction of ultra-short-term photovoltaic power using chaotic characteristic analysis, improved PSO and KELM. *Energy* 2022;248:123574. <https://doi.org/10.1016/j.energy.2022.123574>.
- [30] Tang H, Kang F, Li X, Sun Y. Short-term photovoltaic power prediction model based on feature construction and improved transformer. *Energy* 2025;320:135213. <https://doi.org/10.1016/j.energy.2025.135213>.
- [31] Sun F, Li L, Bian D, Bian W, Wang Q, Wang S. Photovoltaic power prediction based on multi-scale photovoltaic power fluctuation characteristics and multi-channel LSTM prediction models. *Renew Energy* 2025;246:122866. <https://doi.org/10.1016/j.renene.2025.122866>.
- [32] Lang Y, Gao Y. Dream Optimization Algorithm (DOA): a novel metaheuristic optimization algorithm inspired by human dreams and its applications to real-world engineering problems. *Comput Methods Appl Mech Eng* 2025;436:117718. <https://doi.org/10.1016/j.cma.2024.117718>.
- [33] Zhu J, He Y. A novel hybrid model based on evolving multi-quantile long and short-term memory neural network for ultra-short-term probabilistic forecasting of photovoltaic power. *Appl Energy* 2025;377:124601. <https://doi.org/10.1016/j.apenergy.2024.124601>.
- [34] Chen J, Peng T, Qian S, Ge Y, Wang Z, Nazir M, et al. An error-corrected deep Autoformer model via Bayesian optimization algorithm and secondary decomposition for photovoltaic power prediction. *Appl Energy* 2025;377:124738. <https://doi.org/10.1016/j.apenergy.2024.124738>.
- [35] Gong J, Qu Z, Zhu Z, Xu H. Parallel TimesNet-BiLSTM model for ultra-short-term photovoltaic power forecasting using STL decomposition and auto-tuning. *Energy* 2025;320:135286. <https://doi.org/10.1016/j.energy.2025.135286>.
- [36] Zhai C, He X, Cao Z, Abdou-Tankari M, Wang Y, Zhang M. Photovoltaic power forecasting based on VMD-SSA-Transformer: multidimensional analysis of dataset length, weather mutation and forecast accuracy. *Energy* 2025;324:135971. <https://doi.org/10.1016/j.energy.2025.135971>.
- [37] Wang T, Xu Y, Qin Y, Wang X, Zheng F, Li W. Short-term PV forecasting of multiple scenarios based on multi-dimensional clustering and hybrid transformer-BiLSTM with ECPO. *Energy* 2025;334:137654. <https://doi.org/10.1016/j.energy.2025.137654>.
- [38] Li Y, Wang Z, Liu S. Enhance carbon emission prediction using bidirectional long short-term memory model based on text-based and data-driven multimodal information fusion. *J Clean Prod* 2024;471:143301. <https://doi.org/10.1016/j.jclepro.2024.143301>.
- [39] Wang Z, Zhu Z, Luan H, Wu T. Multi-objective optimal scheduling of cascade reservoirs in complex basin systems: case study of the Jinsha River-Yalong River confluence basin in China. *J Hydrol Reg Stud* 2025;58:102240. <https://doi.org/10.1016/j.ejrh.2025.102240>.
- [40] Guo H, Chen L, Wang Z, Li L. Day-ahead prediction of electric vehicle charging demand based on quadratic decomposition and dual attention mechanisms. *Appl Energy* 2025;381:125198. <https://doi.org/10.1016/j.apenergy.2024.125198>.
- [41] Tan Z, Li H, Song Q, Wang Z, Cao Y. Synergistic optimization and interaction evaluation of water-energy-food-ecology nexus under uncertainty from the perspective of urban agglomeration. *Sustain Cities Soc* 2025;124:106291. <https://doi.org/10.1016/j.scs.2025.106291>.
- [42] Su Z, Gu S, Wang J, Lund P. Improving ultra-short-term photovoltaic power forecasting using advanced deep-learning approach. *Measurement* 2025;239:115405. <https://doi.org/10.1016/j.measurement.2024.115405>.
- [43] Chen Z, Bai Y, Ding L, Qin H, Bi Q. Intra-hour photovoltaic power point-interval prediction using a dual-view deep neural network. *Expert Syst Appl* 2025;260:125368. <https://doi.org/10.1016/j.eswa.2024.125368>.
- [44] Renold AP, Sinha N, Gao XZ. Hybrid machine learning approach for improved short-term PV power forecasting accuracy. *Results Eng* 2025;28:107374. <https://doi.org/10.1016/j.rineng.2025.107374>.
- [45] Zhu Z, Li H, Wang Z, Zhang X, Tan Z. Integration of deep learning and improved multi-objective algorithm to optimize cascade reservoirs operation with consideration of ecological dissolved oxygen needs. *J Hydrol* 2026;667:134899. <https://doi.org/10.1016/j.jhydrol.2025.134899>.