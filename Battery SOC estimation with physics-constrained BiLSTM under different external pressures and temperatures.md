

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Journal of Energy Storage cover image showing a battery cell and the journal title](390120de4fe440c42fea8154fcaad334_img.jpg)

Journal of Energy Storage cover image showing a battery cell and the journal title

## Research papers

# Battery SOC estimation with physics-constrained BiLSTM under different external pressures and temperatures

![Check for updates button](6ed175c791b5e156d9c98a8dbcc3318c_img.jpg)

Check for updates button

Longxing Wu<sup>a,c,\*</sup>, Xinyuan Wei<sup>a</sup>, Chunsong Lin<sup>b,\*\*</sup>, Zebo Huang<sup>d</sup>, Yuqian Fan<sup>e</sup>, Chunhui Liu<sup>a</sup>, Shuping Fang<sup>a</sup>

<sup>a</sup> College of Mechanical Engineering, Anhui Science and Technology University, Chuzhou 233100, China

<sup>b</sup> School of Mechanical Engineering, Sichuan University of Science and Engineering, Yibin 64400, China

<sup>c</sup> Hubei Key Laboratory for High-Efficiency Utilization of Solar Energy and Operation Control of Energy Storage System, Hubei University of Technology, Wuhan 430068, China

<sup>d</sup> School of Mechanical and Electrical Engineering, Guilin University of Electronic Technology, Guilin 541214, China

<sup>e</sup> School of Computer Science and Technology, Henan Institute of Science and Technology, Xinxiang 453003, China

## ARTICLE INFO

### Keywords:

Lithium-ion battery  
External pressure  
Physics-constrained BiLSTM  
SOC estimation

## ABSTRACT

With the widespread use of electric vehicles and energy storage systems, accurately estimating the state of charge (SOC) of lithium-ion batteries (LIBs) has become one of the core tasks in battery management systems. Traditional SOC estimation methods often overlook the influence of external preload pressure on battery performance and lack certain physical constraints, which still pose challenges in terms of accuracy and robustness. To address this issue, this paper proposes a physics-constrained Bidirectional Long Short-Term Memory (P-BiLSTM) model to achieve accurate SOC estimation of LIBs. Specifically, this approach incorporates external preload pressure and temperature as key input features of the network model based on experimental data analysis. Subsequently, the fundamental physical laws governing the SOC change process are embedded into the model through a loss function, with constraints applied during both the input and output phases to further enhance estimation accuracy and reliability. Experimental results show that preload pressure significantly impacts SOC accuracy, with lower pressure causing a smaller effect. At 600 N, the average absolute error in SOC estimation reaches a maximum of 0.7890, while the minimum mean absolute error (MAE) is 0.1654. Compared to conventional machine learning methods, the proposed P-BiLSTM method, which incorporates external pressure, demonstrates superior performance and higher accuracy in battery SOC estimation.

## 1. Introduction

With their exceptional performance, lithium-ion batteries (LIBs) have been widely adopted in electric vehicles (EVs), energy storage systems, and other portable devices [1–3]. Correspondingly, the importance of their performance management and monitoring has become increasingly prominent. In this context, a reliable battery management system (BMS) is essential for LIBs to operate efficiently and stably in complex environments [4–6]. Considering that State of Charge (SOC) of the battery, as a critical indicator of remaining energy, plays an important role in estimating remaining driving range, the accurate SOC estimation is closely related to system safety and battery lifespan management, serving as the one of most significance functions for BMS

control strategies [7,8]. However, SOC cannot be obtained through direct measurement, making its precise estimation has become one of the core challenges in BMS and has attracted extensive research interest [9].

Generally, the SOC estimation techniques presented in the literatures can be categorized into three main types: direct measurement methods [10], model-based methods [11], and data-driven methods [12]. As illustrated in Ref. [10], the direct measurement methods mainly estimate battery SOC by directly calculating it from field-acquired data. For example, the ampere-hour integration method is a direct estimation approach based on integrating current over time, calculating SOC by accumulating charge and discharge currents. However, it essentially functions as an open-loop system and is susceptible to inaccuracies from

\* Corresponding author at: College of Mechanical Engineering, Anhui Science and Technology University, Chuzhou 233100, China.

\*\* Corresponding author.

E-mail addresses: [batteryywu@163.com](mailto:batteryywu@163.com) (L. Wu), [linchunsong@suse.edu.cn](mailto:linchunsong@suse.edu.cn) (C. Lin).

initial SOC errors and current measurement deviations [10]. Additionally, as another commonly used method, the open-circuit voltage approaches can provide high estimation accuracy but require prolonged inactivity to allow the battery to reach thermodynamic equilibrium, which makes them unsuitable for real-time SOC measurement in vehicles [13], especially for the widely used LiFePO<sub>4</sub> batteries. As a result, direct measurement methods are limited by factors such as environmental conditions and equipment arrangement and they still face challenges in practical applications. In comparison, the model-based SOC estimations are carried out by constructing a mathematical model in conjunction with filtering algorithms and observers [14–16]. In other words, these methods usually utilize real-time collected data to correct and adjust SOC estimation based on the differences between predicted and measured values, which greatly enhance the real-time accuracy and robustness of SOC estimation to a certain extent [17–19]. And the most commonly used models are the equivalent circuit model [20] and the electrochemical model [21,22]. Based on the above developed models, Zhang et al. proposed an adaptive extended Kalman algorithm based on an equivalent circuit model to achieve accurate SOC estimation and addressed the problem that the extended Kalman filter algorithm cannot well track the system state in real-time [20]. In contrast, Wang et al. explored a reduced-order electrochemical models and finished the SOC estimation using a particle filter, which offers a detailed description of the battery's internal electrochemical processes and physical meaning about the SOC of the battery [22]. Although advancements in filtering algorithms can improve prediction accuracy, the feasibility of these methods is constrained essentially by the chosen battery model. In turn, accurate battery modeling increases complexity, as models need to account for different operating conditions, application scenarios, and extreme conditions, which restricts the generalizability and broader applicability of model-based approaches in the field of battery SOC estimation.

In recent years, the rapid development of various machine learning technologies has led to significant achievements for data-driven methods-based SOC estimation of LIBs. Different from traditional SOC estimation methods, the SOC estimation with data-driven approaches can avoid well the need for complex model understanding. Instead, they can directly build the mapping relationship between the various measured quantities (such as current, voltage, and temperature) and SOC, making them less constrained by battery operating conditions and offering strong generalization capabilities [23]. With the help of artificial intelligence technology, the various battery SOC estimation approaches, such as Gaussian Process Regression (GPR) [24] and Support Vector Machines (SVM) [25] have been extensively discussed and applied. However, these conventional machine learning algorithms have limitations in the generalization capability and, only achieve the high accuracy under specific conditions. In contrast, neural network-based SOC estimation has shown more remarkable performance in limited dataset [26]. Common approaches include Long Short-Term Memory (LSTM) networks, Recurrent Neural Networks (RNN) [27,28], and Gated Recurrent Units (GRU) [29]. These time-series neural networks have seen widespread application in SOC estimation due to their ability to capture temporal information. Subsequently, more complex neural network algorithms that integrate convolution and attention mechanisms [30,31] are also investigated to enhance predictive and generalization capabilities of SOC estimation. Unfortunately, the improvements in these methods mainly focus on increasing network complexity, which significantly raises computational costs, making deployment challenging in resource-constrained embedded systems or real-time applications.

Although the data-driven SOC estimation method is a future trend that promises to mitigate battery driving anxiety, the following limitations remain: On the one hand, researchers have observed that traditional deep learning models often lack embedded physical knowledge. Numerous studies have shown that integrating domain-specific expertise into neural networks can further improve prediction accuracy,

reliability, and interpretability. A common approach to achieve this is through physics-informed embedding [32]. Thus, integrating physical knowledge not only enhances prediction accuracy but, more importantly, also strengthens the reliability and interpretability of neural networks, which is especially crucial in high-safety-requirement applications. On the other hand, most of the above data-driven SOC estimation model only adopted the conventional measurements including voltage, current, and temperature as direct or indirect input variables while neglected the effects of external pressures on SOC estimation. Nevertheless, it is reported that the expansion force of LIBs changes when they are subjected to external pressure, which is closely related to the key states of the battery [33]. Moreover, the addition of mechanical signals can also provide a novel method for upgrading the SOC estimation results of LiFePO<sub>4</sub> batteries considering the flat open-circuit voltage variation in the middle of SOC values [34,35]. For example, Dai et al. considered this phenomenon may facilitate the design of mechanics-based states estimation and proposed a novel SOC method based on experimental stress measurement data. Eventually, experimental results shown that the stress-based method performs well with a good accuracy [36]. Subsequently, Xu et al. carried out a novel data-driven SOC estimation approach based on various features, especially incorporating experimental stress signals, which compensates well for the flat OCV problem at the middle SOC region section [37]. Moreover, Samad et al. [38] further demonstrated the relationship between stress variation and SOC by assessing battery capacity degradation using incremental capacity analysis. Accordingly, the results of above researches well support the importance of stress measurements as a complementary indicator for SOC estimation. However, current research primarily focuses on the impact of internal stress on SOC, with insufficient exploration of how external mechanical pressure affects SOC under various ambient temperatures [39]. More importantly, most data-driven method used in the field of mechanics-based SOC estimation did not involve domain knowledge or physical laws in the construction of network models, which will make these methods suffering from poor generalization ability and interpretability in practical applications.

To address the above limitations, this paper develops a deep learning framework incorporating domain knowledge and laws of battery system under different external pressures and temperatures, which is named physics-constrained BiLSTM (P-BiLSTM) for accurate SOC estimation. First, we introduce constant external preload as a mechanical parameter to study the effects of pressure and temperature on battery SOC. Second, a novel P-BiLSTM-based SOC estimation framework incorporating domain knowledge and physical laws is proposed. Compared to existing mainstream research, the innovation of this study lies in analyzing the impact of external pressure and temperature on SOC estimation accuracy, while also incorporating the fundamental physical laws of lithium-ion battery SOC, embedding physical knowledge constraints to improve the accuracy and reliability of SOC estimation. And the main contributions of this paper are summarized as follows:

(1) Incorporating external mechanical signals as input information: To address the current lack of research on external pressure, the critical external preload is integrated into the model to investigate its impact on battery SOC estimation under the combined effects of pressures and temperatures.

(2) Developing a P-BiLSTM-based SOC estimation framework: To improve the generalization ability and interpretability of traditional machine learning models, this paper embeds SOC variation patterns and the law of energy conservation into the neural network's loss function and enforces physical constraint in the data preprocessing and model output stage.

(3) Evaluating the feasibility of the proposed method: To verify the effectiveness of the P-BiLSTM-based SOC estimation, the quantitative evaluations and the superiority comparison are carried out under various pressures and temperatures.

The remainder of this paper is organized as follows: Section 2 gives the details of experimental design and data collection. The P-BiLSTM-

![Figure 1: Experimental test setup. The image shows a laboratory environment with several components labeled 1 through 5. 1: A multi-channel battery testing system (Neware BTS-5V12A) with many red and black cables connected to it. 2: A large blue industrial thermal-controlled chamber. 3: A laptop computer displaying a data logging software interface with a table of experimental results. 4: A portable computer or data acquisition unit connected to the testing system and the chamber. 5: A red arrow pointing to a specific component inside the blue chamber, likely a battery cell or a pressure sensor.](7e2f2d03a5dda38b038fd4884629a2b4_img.jpg)

Figure 1: Experimental test setup. The image shows a laboratory environment with several components labeled 1 through 5. 1: A multi-channel battery testing system (Neware BTS-5V12A) with many red and black cables connected to it. 2: A large blue industrial thermal-controlled chamber. 3: A laptop computer displaying a data logging software interface with a table of experimental results. 4: A portable computer or data acquisition unit connected to the testing system and the chamber. 5: A red arrow pointing to a specific component inside the blue chamber, likely a battery cell or a pressure sensor.

Fig. 1. Experimental test setup.

based SOC estimation framework are proposed specifically in Section 3. And Section 4 presents the results and discussions of proposed method in this paper. Finally, the paper is concluded in Section 5.

## 2. Experimental design and data generation

### 2.1. Experimental design

In this section, the GSP655060Fe battery with a capacity of 1.6 Ah is adopted as the test subject, applying lithium iron phosphate as the cathode material and graphite as the anode material respectively. To ensure the accuracy of the collected data, the experimental bench is composed of (1) a Battery tester Neware BTS-5V12A, which is utilized to conduct charge/discharge test of cells; (2) A thermal-controlled chamber, providing the battery characterization tests at different temperatures; (3) A portable computer for data collection and processing; (4) Test harness for achieving the signal connections; (5) Special test fixtures for applying different external pressures. And it is pertinent to emphasized that, the upper charging voltage limit is 3.65 V, the lower discharge voltage limit is 2.0 V, and the nominal voltage is 3.2 V. The maximum charge current is 0.5C, and the maximum discharge current is 1C. To evaluate battery performance under various application scenarios, different external constraint pressures (300 N, 400 N, 500 N, 600 N) and environmental temperatures (10 °C, 25 °C, 40 °C) were applied.

Table 1

Experimental matrixes under 1C discharging rate for the dataset generation.

| Cell type                                                                   | Temperatures (°C) | Pressure (N) | No.         |
|-----------------------------------------------------------------------------|-------------------|--------------|-------------|
| Type: GSP655060Fe<br>Cutoff voltage: 2.0–3.65 V<br>Nominal capacity: 1.6 Ah | 40                | 300          | No.1 ~ No.6 |
|                                                                             | 40                | 400          | No.1 ~ No.6 |
|                                                                             | 40                | 500          | No.1 ~ No.6 |
|                                                                             | 40                | 600          | No.1 ~ No.6 |
|                                                                             | 25                | 600          | No.1 ~ No.6 |
|                                                                             | 10                | 600          | No.1 ~ No.6 |

Additionally, six batteries of identical model specifications underwent charge-discharge testing at varying rates (0.5C to 2C) to comprehensively assess their performance. The schematic diagram of the experimental bench is shown in Fig. 1 and more details on the experiment can be found in our previous study [40].

In accordance with the experimental design requirements, this study selected data from tests conducted at a 1C rate to investigate SOC estimation under varying pressures and temperatures. Detailed information about the relevant specifications and test matrixes of batteries are presented in Table 1.

![Figure 2: Charge and discharge behavior of the battery. (a) Voltage and Current vs Absolute Time (s). (b) Capacity and Power vs Absolute Time (s).](7fb5215fd72210a2e4cce6df55550c89_img.jpg)

Figure 2 consists of two subplots. Subplot (a) shows Voltage (V) and Current (mA) versus Absolute Time (s). The voltage starts at approximately 3.0 V, rises to 3.6 V, and then drops to 2.8 V. The current starts at 1000 mA, drops to 0 mA, and then drops to -1000 mA. Subplot (b) shows Capacity (mAh) and Power (mWh) versus Absolute Time (s). The capacity starts at 0 mAh, rises to 1500 mAh, and then drops to 0 mAh. The power starts at 0 mWh, rises to 4000 mWh, and then drops to 0 mWh.

Figure 2: Charge and discharge behavior of the battery. (a) Voltage and Current vs Absolute Time (s). (b) Capacity and Power vs Absolute Time (s).

**Fig. 2.** Charge and discharge behavior of the battery under conditions of 40 °C, 300 N, and 1C: (a) Current and voltage variations, (b) Changes in detected capacity and power.

![Figure 3: SOC variation during the charge-discharge process of the battery at 40 °C, 300 N, 1C. (a) SOC vs Absolute Time (Charging Phase). (b) SOC vs Absolute Time (Discharging Phase).](b7251436a2a3c0d1c00c3e935df2a8f5_img.jpg)

Figure 3 consists of two subplots. Subplot (a) shows SOC (%) versus Absolute Time (s) during the charging phase. The SOC starts at 0% and rises to 100% over 4000 seconds. Subplot (b) shows SOC (%) versus Absolute Time (s) during the discharging phase. The SOC starts at 100% and drops to 0% over 15000 seconds. Both subplots show six battery cells (No. 1 to No. 6) with very similar SOC profiles.

Figure 3: SOC variation during the charge-discharge process of the battery at 40 °C, 300 N, 1C. (a) SOC vs Absolute Time (Charging Phase). (b) SOC vs Absolute Time (Discharging Phase).

**Fig. 3.** SOC variation during the charge-discharge process of the battery at 40 °C, 300 N, 1C.

![Figure 4: SOC variation during the charge-discharge process of the battery under different pressures. (a) SOC vs Absolute Time (Charging Phase). (b) SOC vs Absolute Time (Discharging Phase).](954ff3c220707f98bcb2c4b197bd7d9f_img.jpg)

Figure 4 consists of two subplots. Subplot (a) shows SOC (%) versus Absolute Time (s) during the charging phase. The SOC starts at 0% and rises to 100% over 4000 seconds. Subplot (b) shows SOC (%) versus Absolute Time (s) during the discharging phase. The SOC starts at 100% and drops to 0% over 15000 seconds. Both subplots show four charging conditions (300N, 400N, 500N, 600N) and four discharging conditions (300N, 400N, 500N, 600N). The discharging curves show significant differences, with higher pressure leading to faster SOC depletion.

Figure 4: SOC variation during the charge-discharge process of the battery under different pressures. (a) SOC vs Absolute Time (Charging Phase). (b) SOC vs Absolute Time (Discharging Phase).

**Fig. 4.** SOC variation during the charge-discharge process of the battery under different pressures.

### 2.2. Data generation and analysis

To further analyze the variations in the battery's charge-discharge process, we conducted a visual analysis of the experimental data, using the 40 °C, 300 N, and 1C conditions as an example, as shown in Fig. 2. The charge-discharge process followed standard experimental procedures and was carried out in a constant-current constant-voltage (CC-CV) strategy, with a rest period of 2 h. And Fig. 2(a) displays the changes in current and voltage during the charge-discharge process, while Fig. 2(b) shows the variations in capacity and power. The data in Fig. 2(b) were collected from sensor measurements, reflecting the cumulative capacity and power recorded. Thus, both charging and discharging are positive values, with cumulative increases over time.

Next, the SOC variation curve was visualized, as shown in Fig. 3. During the charging process, the SOC trends of different batteries were generally consistent, with only minor differences observed during the final stage of charging, specifically in the constant-voltage phase. However, during the discharge phase, even under identical operating conditions, there were still differences in the charge and discharge curves. These variations arise from inherent differences in battery

characteristics, underscoring the importance of accurate SOC estimation based on data.

To further investigate the effects of different pressures and temperatures on the SOC of the same battery, we analyzed SOC variation during the charge-discharge process using Cell 6 under the conditions of 40 °C, 600 N, and 1C as an example. The discharge curves of Cell 6 under various pressures were visualized, as shown in Fig. 4. Since the tests were conducted on the same battery with accelerated aging, degradation issues are not a factor. Additionally, there were no interval cycles between different force tests on the same battery, so the discharge process should theoretically remain consistent. In practice, however, due to the intrinsic properties of the battery, both temperature and pressure exert some influence, resulting in observable differences. Because the charge-discharge process follows a constant-current protocol, the impact of external pressure is minimal during charging. However, during discharging, SOC differences become more apparent. Based on this observation, we focus on the discharge phase for further analysis in subsequent studies.

![Figure 5: The overall architecture of the P-BiLSTM for SOC estimation. The diagram is divided into three main sections: 1 Data acquisition, 2 P-BiLSTM, and 3 Result analysis. Section 1 shows experimental setups for different pressures (300N, 400N, 500N, 600N) and different temperatures (10°C, 25°C, 30°C). Section 2 is the core P-BiLSTM model, which includes an Input Layer, BiLSTM Layers, a Linear Layer, and an Output Layer. It incorporates three constraints: Cons.#1 (Physical rule preprocessing), Cons.#2 (Data filtering module), and Cons.#3 (LOSS_data, LOSS_p-soc, LOSS_range, LOSS_mono). The model uses weight and bias parameters [W, b] and performs backpropagation to calculate the Loss. Section 3 shows a bar chart of MAE for six batteries (No. 1 to No. 6) under different conditions.](e394c2b5c61344f6a12397f430086072_img.jpg)

| Battery No. | MAE (No. 1) | MAE (No. 2) | MAE (No. 3) | MAE (No. 4) | MAE (No. 5) | MAE (No. 6) |
|-------------|-------------|-------------|-------------|-------------|-------------|-------------|
| No. 1       | 0.55        | 0.65        | 0.35        | 0.25        | 0.25        | 0.35        |
| No. 2       | 0.45        | 0.35        | 0.45        | 0.35        | 0.35        | 0.35        |
| No. 3       | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        |
| No. 4       | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        |
| No. 5       | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        |
| No. 6       | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        | 0.35        |

Figure 5: The overall architecture of the P-BiLSTM for SOC estimation. The diagram is divided into three main sections: 1 Data acquisition, 2 P-BiLSTM, and 3 Result analysis. Section 1 shows experimental setups for different pressures (300N, 400N, 500N, 600N) and different temperatures (10°C, 25°C, 30°C). Section 2 is the core P-BiLSTM model, which includes an Input Layer, BiLSTM Layers, a Linear Layer, and an Output Layer. It incorporates three constraints: Cons.#1 (Physical rule preprocessing), Cons.#2 (Data filtering module), and Cons.#3 (LOSS\_data, LOSS\_p-soc, LOSS\_range, LOSS\_mono). The model uses weight and bias parameters [W, b] and performs backpropagation to calculate the Loss. Section 3 shows a bar chart of MAE for six batteries (No. 1 to No. 6) under different conditions.

Fig. 5. The overall architecture of the P-BiLSTM for SOC estimation.

## 3. Methodology

### 3.1. The SOC estimation framework

To improve the generalization ability and interpretability of traditional machine learning models, a novel P-BiLSTM-based SOC estimation framework incorporating domain knowledge and physical laws are proposed in this section. And this proposed deep learning framework for SOC estimation mainly embeds SOC variation patterns and the law of energy conservation into the neural network's loss function and enforces physical constraint in the data preprocessing and model output stage to ensure that outputs remain within the valid SOC range. Fundamentally, it aims to address the limitations of pure machine learning algorithms without considering the impacts of domain knowledge or physical regulations. And the overall architecture of the P-BiLSTM is shown in Fig. 5.

First, we selected six sample batteries under conditions of 1C rate

with external pressures of 300 N, 400 N, 500 N, and 600 N, and temperatures of 10 °C, 25 °C, and 30 °C as the experimental data. The data were visualized to analyze variation patterns, based on which discharge SOC was determined as the focus of this study. Then, overall architecture of the P-BiLSTM for SOC estimation mainly includes three types of constraints (indicated as Cons. #1, Cons. #2, and Cons. #3 in Fig. 5) to inject physical knowledge and laws. That is to say, we integrated the SOC range and energy conservation principles as fundamental physical knowledge into the BiLSTM model. During the input preprocessing stage and output prediction stage, SOC range constraints were applied. Additionally, in the neural network's loss function, we embedded energy conservation, SOC range, and variation patterns into the loss calculation, achieving physical knowledge integration via backpropagation. Finally, a normalization method was used to validate SOC estimation across six batteries under each experimental condition. The experimental results demonstrate the effectiveness of the proposed algorithm.

![Figure 6: Structure of BiLSTM network. The diagram illustrates the flow of data through a BiLSTM network. It shows a sequence of inputs (X_{t-1}, X_t, X_{t+1}, X_{t+2}) entering a Hidden layer. The Hidden layer consists of two parallel paths: a Forward LSTM (top) and a Backward LSTM (bottom). The Forward LSTM processes inputs from left to right, while the Backward LSTM processes inputs from right to left. The outputs of these two paths are combined to produce the final hidden states (h_{t-1}, h_t, h_{t+1}, h_{t+2}).](b4a7906eddfd40aaa750e19e56c94a8b_img.jpg)

Figure 6: Structure of BiLSTM network. The diagram illustrates the flow of data through a BiLSTM network. It shows a sequence of inputs (X\_{t-1}, X\_t, X\_{t+1}, X\_{t+2}) entering a Hidden layer. The Hidden layer consists of two parallel paths: a Forward LSTM (top) and a Backward LSTM (bottom). The Forward LSTM processes inputs from left to right, while the Backward LSTM processes inputs from right to left. The outputs of these two paths are combined to produce the final hidden states (h\_{t-1}, h\_t, h\_{t+1}, h\_{t+2}).

Fig. 6. Structure of BiLSTM network [41].

And key details of each process are discussed in the following subsections.

### 3.2. The principles of BiLSTM

Due to its ability to handle sequential data, the BiLSTM network can consider both past and future information in regression predictions, achieving significant success in fields such as natural language processing, speech recognition, and time series forecasting. Therefore, the BiLSTM network here is applied as the core of proposed deep learning framework for battery SOC estimation.

As shown in Fig. 6, the BiLSTM network consists of two independent Long Short-Term Memory (LSTM) layers: a forward layer and a backward layer. The forward layer processes the input data sequentially from beginning to end, while the backward layer processes it in reverse order, from end to beginning. At each time step, the outputs of both layers are combined to capture comprehensive sequential information. The fundamental computational process of the algorithm can be referenced in [41].

A single LSTM neuron also takes into account memory and forgetting of information. Compared to ordinary neural networks, it has strong nonlinear fitting capabilities. The implementation of this is achieved by adjusting the single neuron to enable memory and forgetting functions. The specific computation process can be referenced in literature [41]. The training process of a BiLSTM involves adjusting the weights and bias parameters of the neurons to minimize the error, achieving optimal fitting performance. To better understand the implementation of the P-BiLSTM method, the training process of the neural network is analyzed below, with the representation of a single neuron shown in Eq. (1):

$$y = \alpha(wx + b) \quad (1)$$

where  $x$  represents the current input,  $w$  is the weight,  $b$  is the bias, and  $\alpha$  is the activation function.

Eq. (1) represents the forward calculation of the neural network. Based on the given weights  $w$  and bias  $b$ , the output of the neuron is calculated, which ultimately leads to the output of the neural network. The training process of the neural network involves adjusting the weights and bias parameters through the loss function, a process commonly known as error backpropagation. The loss function is typically defined as the fitting error, as shown in Eq. (2) below:

$$\text{loss} = \frac{1}{2} \sum_{k=1}^{N} (f(x^k) - y_k)^2 \quad (2)$$

In this context,  $y_k$  represents the actual output, while  $f(x^k)$  is the model's predicted output based on the input features.

The goal of training a neural network is to minimize the loss function. To achieve the fastest parameter adjustment, gradient descent is commonly used. Since neurons are organized in multiple layers, the chain rule is applied to compute the gradient of each parameter. This involves calculating the partial derivatives of each parameter with respect to the loss function, starting from the output layer and working back to the input layer. Then, the weights  $w$  and biases  $b$  are adjusted according to the gradients and a predetermined learning rate. The update rule for a single neuron is given by [42]:

$$\begin{cases} w = w - \eta \frac{\partial \text{loss}}{\partial w} \\ b = b - \eta \frac{\partial \text{loss}}{\partial b} \end{cases} \quad (3)$$

where  $\eta$  represents the learning rate,  $\frac{\partial \text{loss}}{\partial w}$  is the gradient of the loss function with respect to  $w$ , and  $\frac{\partial \text{loss}}{\partial b}$  is the gradient of the loss function with respect to  $b$ .

### 3.3. Physical constraints

(1) Constraints in the prediction phase (Cons. #1 and Cons. #2)

1) Input preprocessing

Due to the presence of random errors, anomalous data may arise that do not conform to fundamental theoretical principles. Therefore, in the data preprocessing stage, it is necessary to handle these outliers by applying basic physical laws governing voltage and capacity changes to preprocess the raw data. During the discharge process, the constant current should result in a relatively stable voltage, although some current fluctuations may occur. The discharge current is set as a negative value, with a consistently decreasing monotonic trend. And data that do not align with this pattern are corrected using interpolation.

2) Range clipping in the testing phase

In battery operation, the actual SOC varies within the range [0,1]. Therefore, we introduce a clipping module to restrict the model's output to this reasonable range, aiming to eliminate physically implausible predictions. To preserve the effects of the training phase, this clipping module is applied only during the testing phase.

For this reason, the proposed above two constraints of processing methods provide an effective solution for the selection of feature variables and ensures appropriate output for network training models.

(2) Physical error constraint module (Cons. #3)

1) Energy conservation

The SOC reflects changes in battery capacity and fundamentally adheres to the law of energy conservation. During discharge, SOC changes not only monotonically but also follows a pattern that can be calculated through ampere-hour integration. The theoretical calculation method of SOC can be expressed as:

$$\text{SOC}_k^* = \text{SOC}_{k-1}^* - \frac{I_k \Delta t}{Q_{\text{actual}}} \quad (4)$$

where  $I_k$  is the current at time step  $k$ ,  $\Delta t$  is the time interval,  $Q_{\text{actual}}$  represents the current capacity of the battery,  $\text{SOC}_k^*$  and  $\text{SOC}_{k-1}^*$  are the theoretical calculation SOC values at the  $k$  and  $k-1$ , respectively.

Using Eq. (4) as prior knowledge for SOC estimation, the SOC constraint loss can be expressed as [43]:

$$\text{loss}_{p\text{-soc}} = \frac{1}{2} \sum_{k=1}^{N} \left[ \text{SOC}_k - \left( \text{SOC}_{k-1} - \frac{I_k \Delta t}{Q_{\text{actual}}} \right) \right]^2 \quad (5)$$

where  $\text{SOC}_k$  and  $\text{SOC}_{k-1}$  represent the estimated SOC values at the  $k$  and  $k-1$  sampling points, respectively.

2) SOC range constraint

At any given time, a battery's SOC should remain within the physical range of 0 % to 100 %. To ensure the physical feasibility of the prediction results, we implemented a range constraint loss that penalizes SOC values predicted outside this range. This constraint applies a squared penalty to output values less than 0 or greater than 1, forcing the model to adjust its weights and avoid generating unrealistic predictions.

Penalty applied to the predicted values below 0 %:

$$\text{loss}_{\text{lower}} = \frac{1}{2} \sum_{k=1}^{N} \left[ \max(0, S_{\min} - S_{\text{pred}}^k) \right]^2 \quad (6)$$

where  $S_{\min}$  represents the lower SOC limit (0 %), and  $S_{\text{pred}}^k$  denotes the SOC value predicted at the times of  $k$  by the model.

Penalty applied to the portion of predicted values exceeding 100 %:

$$\text{loss}_{\text{upper}} = \frac{1}{2} \sum_{k=1}^{N} \left[ \max(0, S_{\text{pred}}^k - S_{\max}) \right]^2 \quad (7)$$

where  $S_{\max}$  represents the upper SOC limit (100 %).

Combining both penalty terms, the final expression for the range constraint loss is:

**Table 2**

Battery SOC estimation errors index on under different pressures.

| No.  | 300 N  |        |                | 400 N  |        |                | 500 N  |        |                | 600 N  |        |                |
|------|--------|--------|----------------|--------|--------|----------------|--------|--------|----------------|--------|--------|----------------|
|      | MAE    | MSE    | R <sup>2</sup> | MAE    | MSE    | R <sup>2</sup> | MAE    | MSE    | R <sup>2</sup> | MAE    | MSE    | R <sup>2</sup> |
| No.1 | 0.4935 | 0.3163 | 0.9996         | 0.6119 | 0.5873 | 0.9993         | 0.2927 | 0.1558 | 0.9998         | 0.7345 | 0.7485 | 0.9991         |
| No.2 | 0.4262 | 0.3857 | 0.9995         | 0.2599 | 0.1688 | 0.9998         | 0.2348 | 0.1191 | 0.9999         | 0.2681 | 0.1549 | 0.9998         |
| No.3 | 0.3576 | 0.1948 | 0.9998         | 0.1550 | 0.0536 | 0.9999         | 0.3275 | 0.1853 | 0.9998         | 0.6673 | 0.6072 | 0.9993         |
| No.4 | 0.3000 | 0.1937 | 0.9998         | 0.3524 | 0.2537 | 0.9997         | 0.3045 | 0.1680 | 0.9998         | 0.2738 | 0.1297 | 0.9998         |
| No.5 | 0.2511 | 0.1121 | 0.9999         | 0.2906 | 0.1468 | 0.9998         | 0.2646 | 0.1654 | 0.9998         | 0.2680 | 0.1201 | 0.9999         |
| No.6 | 0.6046 | 0.5835 | 0.9992         | 0.7772 | 0.9574 | 0.9988         | 0.7890 | 0.9022 | 0.9989         | 0.3968 | 0.2455 | 0.9997         |

$$\text{loss}_{\text{range}} = \text{loss}_{\text{lower}} + \text{loss}_{\text{upper}} \quad (8)$$

#### **3) SOC monotonicity**

Assuming  $\text{SOC}(k)$  represents the SOC value at time  $k$ , a penalty term can be introduced to enforce monotonicity in the model's output over the time series. For the discharge process (where SOC should decrease over time), a penalty term can be defined to ensure that SOC values decrease with time:

$$\text{loss}_{\text{mono}} = \frac{1}{2} \sum_{k=1}^{N} [\max(0, \text{SOC}(k+1) - \text{SOC}(k))]^2 \quad (9)$$

#### **(3) Embedding physical knowledge**

Based on the analysis of neural networks, the loss function propagates learned knowledge back to the model parameters. Therefore, by incorporating physical loss into the loss function and applying error backpropagation, physical knowledge can be used to guide model training. Constructing the neural network's loss function is thus essential for embedding physical knowledge. For clarity, the original loss function Eq. (2) is redefined as the data loss function, denoted as:

$$\text{loss}_{\text{data}} = \frac{1}{2} \sum_{k=1}^{N} (f(x^k) - y_k)^2 \quad (10)$$

By combining data constraints with physical constraints, the loss function for network computation is obtained, allowing for the embedding of physical knowledge:

$$\text{min loss} = \text{min}(\text{loss}_{\text{data}} + \omega_1 \text{loss}_{\text{p-soc}} + \omega_2 \text{loss}_{\text{range}} + \omega_3 \text{loss}_{\text{mono}}) \quad (11)$$

where  $\omega_1$ ,  $\omega_2$ , and  $\omega_3$  are the weights of the physical constraints.

## **4. Results and discussions**

### **4.1. The evaluation criteria**

To assess the effectiveness of the proposed methods, four primary performance metrics were utilized: Mean Square Error (MSE), Coefficient of Determination (R<sup>2</sup>), and Mean Absolute Error (MAE). The mathematical expressions for these metrics are as follows [31]:

$$\text{MSE} = \frac{1}{n} \sum_{k=1}^{n} (\text{SOC}_k - \text{SOC}_k^*)^2 \quad (12)$$

$$\text{MAE} = \frac{1}{n} \sum_{k=1}^{n} \left| \frac{(\text{SOC}_k^* - \text{SOC}_k)}{\text{SOC}_k} \right| \quad (13)$$

$$R^2 = 1 - \frac{\sum_{k=1}^{n} (\text{SOC}_k - \text{SOC}_k^*)^2}{\sum_{k=1}^{n} (\text{SOC}_k - \bar{\text{SOC}}_k)^2} \quad (14)$$

where  $\text{SOC}$ ,  $\text{SOC}_k^*$ ,  $\bar{\text{SOC}}_k$  respectively represent the actual value, predicted value and average value of the SOH of the battery are represented by.  $n$  is the total number of predicted values.

### **4.2. Implementation details**

This experiment aims to develop a BiLSTM model with physical constraints to predict the SOC of lithium-ion batteries under varying temperature and pressure conditions. All experiments were conducted on a workstation with an Intel(R) Core(TM) i9-10850K CPU @ 3.60GHz, 64.0 GB RAM, running a 64-bit Windows operating system. The model employs a leave-one-out cross-validation strategy and is trained on multiple battery discharge datasets containing normalized time, voltage, power, and temperature features. By embedding physical constraints into the loss function, the model's SOC prediction accuracy is ensured.

The model optimization uses the Adam optimizer with gradient clipping, an initial learning rate of 0.001, and a step scheduler that halves the learning rate every 50 epochs. The weight decay coefficient is set to  $1 \times 10^{-4}$  and the model architecture includes three LSTM layers, each with 32 hidden units, capable of learning patterns from both forward and backward time series. These are followed by two fully connected layers with 24 and 12 units, respectively, both using the ReLU activation function. The input feature dimension is 4, corresponding to time, voltage, and power, with temperature and pressure features swapped depending on the model variation. The loss function weights are set as follows: MSE loss weight of 1, physical constraint loss weight of 10, SOC range penalty weight of 10, and SOC monotonicity penalty weight of 10. The weight values were determined through a trial-and-error process, starting with an initial value of 0.1. We systematically

![Figure 7: Error metric histogram. Three bar charts showing MAE, MSE, and R^2 for six battery samples (No. 1 to No. 6) under four pressure conditions (300N, 400N, 500N, 600N). The legend indicates: 300N (green), 400N (orange), 500N (red), 600N (yellow).](6cf7b4fc09974e4f70e7add849fe1702_img.jpg)

Figure 7 consists of three bar charts arranged horizontally, each showing error metrics for six battery samples (No. 1 to No. 6) under four pressure conditions (300N, 400N, 500N, 600N). The legend at the top indicates the colors for each pressure: 300N (green), 400N (orange), 500N (red), and 600N (yellow).

- MAE Chart:** The y-axis ranges from 0.0 to 0.8. Sample No. 1 has the highest MAE (approx. 0.75 for 600N). Sample No. 3 has the lowest MAE (approx. 0.25 for 500N).
- MSE Chart:** The y-axis ranges from 0.00 to 1.00. Sample No. 1 has the highest MSE (approx. 0.75 for 600N). Sample No. 3 has the lowest MSE (approx. 0.15 for 500N).
- R<sup>2</sup> Chart:** The y-axis ranges from 0.00 to 1.00. All samples across all pressure conditions show an R<sup>2</sup> value very close to 1.00, indicating excellent fit.

Figure 7: Error metric histogram. Three bar charts showing MAE, MSE, and R^2 for six battery samples (No. 1 to No. 6) under four pressure conditions (300N, 400N, 500N, 600N). The legend indicates: 300N (green), 400N (orange), 500N (red), 600N (yellow).

**Fig. 7.** Error metric histogram.

![Figure 8: Trajectory tracking of the estimated and actual SOC on 300 N for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents 'Predicted SOC' and a blue line represents 'Actual SOC'. A zoomed-in view is shown in an inset for each plot, highlighting the initial discharge phase. The zoomed-in x-axis ranges from 2700 to 2800s for batteries 1-4, and from 2850 to 2950s for batteries 5-6. The zoomed-in y-axis ranges from 0 to 20% for batteries 1-4, and from 0 to 22% for batteries 5-6.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 8: Trajectory tracking of the estimated and actual SOC on 300 N for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents 'Predicted SOC' and a blue line represents 'Actual SOC'. A zoomed-in view is shown in an inset for each plot, highlighting the initial discharge phase. The zoomed-in x-axis ranges from 2700 to 2800s for batteries 1-4, and from 2850 to 2950s for batteries 5-6. The zoomed-in y-axis ranges from 0 to 20% for batteries 1-4, and from 0 to 22% for batteries 5-6.

Fig. 8. Trajectory tracking of the estimated and actual SOC on 300 N, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

![Figure 9: Trajectory tracking of the estimated and actual SOC on 400 N for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents 'Predicted SOC' and a blue line represents 'Actual SOC'. A zoomed-in view is shown in an inset for each plot, highlighting the initial discharge phase. The zoomed-in x-axis ranges from 2700 to 2800s for batteries 1-4, and from 2850 to 2950s for batteries 5-6. The zoomed-in y-axis ranges from 0 to 20% for batteries 1-4, and from 0 to 18% for batteries 5-6.](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 9: Trajectory tracking of the estimated and actual SOC on 400 N for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents 'Predicted SOC' and a blue line represents 'Actual SOC'. A zoomed-in view is shown in an inset for each plot, highlighting the initial discharge phase. The zoomed-in x-axis ranges from 2700 to 2800s for batteries 1-4, and from 2850 to 2950s for batteries 5-6. The zoomed-in y-axis ranges from 0 to 20% for batteries 1-4, and from 0 to 18% for batteries 5-6.

Fig. 9. Trajectory tracking of the estimated and actual SOC on 400 N, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

tested both smaller weights (such as 0.05, 0.01) and larger weights to observe their effects on training stability and constraint satisfaction. The final weights were selected based on validation performance metrics.

### 4.3. Results

#### 4.3.1. Validation at different pressures

To investigate SOC estimation accuracy under different external pressures, we conducted validation tests at a temperature of 40 °C and a 1C discharge rate under constant external pressures of 300 N, 400 N, 500 N, and 600 N. The error metrics are presented in Table 2. For a visual comparison of these error metrics, a visualization analysis is provided in Fig. 7. To further examine the error tracking in SOC predictions, we plotted the SOC tracking curves for each test battery, as shown in Fig. 8–11. Fig. 12 illustrates the absolute error for each case.

From Table 2 and Fig. 7, it can be observed that the  $R^2$  values for all battery error metrics are close to 1, ranging from 0.9988 to 0.9999. This

indicates that the model achieves an exceptionally high fit for battery SOC predictions, accurately reflecting the actual SOC variation. However, the MAE values range from 0.1550 to 0.7890, and the MSE values range from 0.0536 to 0.9574. Overall, the relatively low MAE and MSE values indicate minimal prediction error by the model, though some variability exists across different batteries and pressure conditions. Notably, Batteries 4 and 5 exhibit excellent error metrics across the board, whereas Battery 6 shows relatively poorer performance on all error metrics. This suggests inconsistencies in individual battery performance, highlighting the model's current limitations in capturing subtle distinctions in external performance characteristics—an area for potential algorithmic optimization. Additionally, different external pressures impact SOC estimation accuracy. Under 600 N, the error metrics are the worst, while pressures between 400 N and 500 N show better performance. This variation may be attributed to external pressure affecting the internal physical and electrochemical reactions of the battery, thereby impacting the model's predictive performance.

![Figure 10: Trajectory tracking of the estimated and actual SOC on 500 N. Six subplots (a-f) show SOC (%) vs. Absolute Time (s) for Batteries 1 through 6. Each plot compares 'Actual SOC' (blue line) and 'Predicted SOC' (red line). A zoomed-in view is shown in an inset for each plot, highlighting the initial and final points of the discharge cycle.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 10 consists of six subplots labeled (a) through (f), each showing the State of Charge (SOC) in percentage on the y-axis (0 to 100) against Absolute Time in seconds on the x-axis (0 to 3000) for a battery operating at 500 N. Each subplot corresponds to a different battery (Battery No. 1 to Battery No. 6). The main plot shows a linear discharge from 100% to approximately 10% over 3000 seconds. A legend in each plot indicates that the blue line represents 'Actual SOC' and the red line represents 'Predicted SOC'. An inset plot in each main plot provides a zoomed-in view of the initial discharge phase, typically from 20.0% to 17.5% SOC over a time interval of approximately 2700 to 2950 seconds. The predicted SOC closely follows the actual SOC in all cases.

Figure 10: Trajectory tracking of the estimated and actual SOC on 500 N. Six subplots (a-f) show SOC (%) vs. Absolute Time (s) for Batteries 1 through 6. Each plot compares 'Actual SOC' (blue line) and 'Predicted SOC' (red line). A zoomed-in view is shown in an inset for each plot, highlighting the initial and final points of the discharge cycle.

Fig. 10. Trajectory tracking of the estimated and actual SOC on 500 N, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

![Figure 11: Trajectory tracking of the estimated and actual SOC on 600 N. Six subplots (a-f) show SOC (%) vs. Absolute Time (s) for Batteries 1 through 6. Each plot compares 'Actual SOC' (blue line) and 'Predicted SOC' (red line). A zoomed-in view is shown in an inset for each plot, highlighting the initial and final points of the discharge cycle.](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 11 consists of six subplots labeled (a) through (f), each showing the State of Charge (SOC) in percentage on the y-axis (0 to 100) against Absolute Time in seconds on the x-axis (0 to 3000) for a battery operating at 600 N. Each subplot corresponds to a different battery (Battery No. 1 to Battery No. 6). The main plot shows a linear discharge from 100% to approximately 10% over 3000 seconds. A legend in each plot indicates that the blue line represents 'Actual SOC' and the red line represents 'Predicted SOC'. An inset plot in each main plot provides a zoomed-in view of the initial discharge phase, typically from 20.0% to 17.5% SOC over a time interval of approximately 2700 to 2950 seconds. The predicted SOC closely follows the actual SOC in all cases.

Figure 11: Trajectory tracking of the estimated and actual SOC on 600 N. Six subplots (a-f) show SOC (%) vs. Absolute Time (s) for Batteries 1 through 6. Each plot compares 'Actual SOC' (blue line) and 'Predicted SOC' (red line). A zoomed-in view is shown in an inset for each plot, highlighting the initial and final points of the discharge cycle.

Fig. 11. Trajectory tracking of the estimated and actual SOC on 600 N, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

However, under all tested conditions, the proposed algorithm achieves accurate SOC estimation.

Additionally, we applied a leave-one-out approach, with predictions made on previously unseen batteries, ensuring the model's generalization capability. By making predictions on new batteries, we demonstrated that the model's predictive ability extends beyond merely fitting known data. The model's performance remained generally stable across various pressure conditions, indicating its adaptability to new batteries and differing external environments. However, under the high pressure of 600 N, prediction errors increased, suggesting that the model's adaptability to internal changes in the battery under high pressure could be improved. Although the incorporation of physical constraints

enhances predictive accuracy, further optimization is needed to accommodate a wider range of battery characteristics and external pressure variations.

Figs. 8 through 11 show the tracking trajectory of each point under different pressures. As observed in the figures, the prediction model achieves excellent tracking accuracy, successfully estimating SOC variations with only minor errors. These small errors primarily occur at the start of discharge and near the end of discharge. For instance, Fig. 7(a) and 7(d) demonstrate such variations, as do similar patterns in other figures. This phenomenon is mainly attributed to the strong correlation between discharge voltage and SOC; due to internal electrochemical effects, voltage changes exhibit pronounced nonlinearity at the

![Figure 12: Error trajectory tracking for six batteries (No.1 to No.6) at four different pressures (300N, 400N, 500N, 600N). Each plot shows Absolute Error (SOC) vs. Absolute Time (s).](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 12 consists of four subplots (a, b, c, d) showing the absolute error trajectory tracking for six batteries (Battery No.1 to No.6) under different pressure conditions. The x-axis for all plots is 'Absolute Time (s)' ranging from 0 to 3500. The y-axis is 'Absolute Error (SOC)'.

- (a) 300N - Absolute Error: The error fluctuates between 0 and 3.0 SOC.
- (b) 400N - Absolute Error: The error fluctuates between 0 and 2.0 SOC.
- (c) 500N - Absolute Error: The error fluctuates between 0 and 3.0 SOC.
- (d) 600N - Absolute Error: The error fluctuates between 0 and 2.0 SOC.

The legend at the top indicates: Battery No.1 (blue), Battery No.2 (green), Battery No.3 (red), Battery No.4 (magenta), Battery No.5 (cyan), and Battery No.6 (yellow).

Figure 12: Error trajectory tracking for six batteries (No.1 to No.6) at four different pressures (300N, 400N, 500N, 600N). Each plot shows Absolute Error (SOC) vs. Absolute Time (s).

Fig. 12. Error trajectory tracking. (a) ~ (d) correspond to the results at 300 N, 400 N, 500 N, and 600 N, respectively.

**Table 3**  
Battery SOC estimation errors index on under different temperatures.

| No.  | 10 °C  |        |                | 25 °C  |        |                | 40 °C  |        |                |
|------|--------|--------|----------------|--------|--------|----------------|--------|--------|----------------|
|      | MAE    | MSE    | R <sup>2</sup> | MAE    | MSE    | R <sup>2</sup> | MAE    | MSE    | R <sup>2</sup> |
| No.1 | 0.2265 | 0.0947 | 0.9998         | 0.5004 | 0.3458 | 0.9996         | 0.3111 | 0.1678 | 0.9998         |
| No.2 | 0.4650 | 0.2957 | 0.9995         | 0.3993 | 0.2878 | 0.9997         | 0.2446 | 0.1664 | 0.9998         |
| No.3 | 0.1891 | 0.0571 | 0.9999         | 0.1439 | 0.0491 | 0.9999         | 0.3518 | 0.1850 | 0.9998         |
| No.4 | 0.1821 | 0.0775 | 0.9999         | 0.3009 | 0.1609 | 0.9998         | 0.7175 | 0.8209 | 0.9990         |
| No.5 | 0.1932 | 0.0639 | 0.9999         | 0.3094 | 0.1851 | 0.9998         | 0.2816 | 0.1485 | 0.9998         |
| No.6 | 0.3286 | 0.1519 | 0.9998         | 0.1660 | 0.0607 | 0.9999         | 0.5772 | 0.5732 | 0.9993         |

![Figure 13: Error metric histogram showing MAE, MSE, and R^2 for six batteries at three different temperatures (10°C, 25°C, 40°C).](33228b4227fa57e1477b27b9e07483e6_img.jpg)

Figure 13 displays three bar charts showing error metrics (MAE, MSE, and R<sup>2</sup>) for six batteries (No.1 to No.6) at three different temperatures (10 °C, 25 °C, and 40 °C). The legend indicates: 10 °C (green), 25 °C (orange), and 40 °C (red).

- MAE (Mean Absolute Error) chart: Battery No.4 shows the highest error at 40 °C.
- MSE (Mean Squared Error) chart: Battery No.4 shows the highest error at 40 °C.
- R<sup>2</sup> (Coefficient of Determination) chart: All batteries show a high R<sup>2</sup> value, close to 1.0, across all temperatures.

Figure 13: Error metric histogram showing MAE, MSE, and R^2 for six batteries at three different temperatures (10°C, 25°C, 40°C).

Fig. 13. Error metric histogram.

beginning and end of discharge, which significantly impacts the proposed method, leading to points with larger estimation **errors**. This behavior is particularly evident in Battery No.4, which shows rapid error variations across all pressure conditions. While these variations can be partially attributed to manufacturing and testing variability, they follow the same general trend as other batteries, indicating normal rather than anomalous behavior. The more pronounced end-of-discharge errors in Battery No.4 highlight the challenges in accurately modeling the complex battery dynamics during this phase. This limitation highlights an area for improvement in the current algorithm. However, Battery No.3 appears less affected by these nonlinearity-induced errors, displaying a relatively stable error profile. Only Fig. 10(e) clearly illustrates this

pattern, and the absolute error variations in Fig. 12 also visually reflect this trend. The inclusion of physical constraints allows the model to converge more quickly to an accurate range during training, and no unrealistic results are observed.

#### 4.3.2. Validation at different temperatures

To further evaluate the effect of temperature on the proposed method, we conducted SOC validation tests at 10 °C, 25 °C, and 40 °C under a constant pressure of 600 N and a 1C rate. Since the pressure condition was kept constant, temperature was used as the variable input. All other experimental conditions were held consistent to ensure comparability of results. Error metrics are shown in Table 3, with a 


![Figure 14: Trajectory tracking of the estimated and actual SOC on 10 °C for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents the Predicted SOC and a blue line represents the Actual SOC. Both lines show a linear decrease from 100% to approximately 20% over 3000 seconds. Each plot includes a zoomed-in view of the initial 250-2600 seconds, where the SOC starts at 100% and drops to about 25%.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 14: Trajectory tracking of the estimated and actual SOC on 10 °C for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents the Predicted SOC and a blue line represents the Actual SOC. Both lines show a linear decrease from 100% to approximately 20% over 3000 seconds. Each plot includes a zoomed-in view of the initial 250-2600 seconds, where the SOC starts at 100% and drops to about 25%.

Fig. 14. Trajectory tracking of the estimated and actual SOC on 10 °C, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

![Figure 15: Trajectory tracking of the estimated and actual SOC on 25 °C for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents the Predicted SOC and a blue line represents the Actual SOC. Both lines show a linear decrease from 100% to approximately 20% over 3000 seconds. Each plot includes a zoomed-in view of the initial 2750-2850 seconds, where the SOC starts at 100% and drops to about 15%.](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

Figure 15: Trajectory tracking of the estimated and actual SOC on 25 °C for six batteries. Each subplot (a-f) shows SOC (%) on the y-axis (0-100) versus Absolute Time (s) on the x-axis (0-3000). A red line represents the Predicted SOC and a blue line represents the Actual SOC. Both lines show a linear decrease from 100% to approximately 20% over 3000 seconds. Each plot includes a zoomed-in view of the initial 2750-2850 seconds, where the SOC starts at 100% and drops to about 15%.

Fig. 15. Trajectory tracking of the estimated and actual SOC on 25 °C, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

visualization of these metrics in Fig. 13–16 display the SOC tracking curves for each test battery, while Fig. 17 illustrates the absolute error for each battery.

The histogram of SOC error metrics shows the MAE, MSE, and  $R^2$  values for SOC estimation across different temperatures. For example, it illustrates that under 10 °C, most batteries have relatively low MAE and MSE, whereas errors increase at 25 °C and 40 °C. Notably, at 25 °C, Battery No.1 exhibits the highest MAE and MSE, while No.4 and No.6 show a sharp increase in error metrics at 40 °C. Specifically, Battery No.4 reaches an MSE of 0.8209 at 40 °C, significantly higher than under other temperature conditions. This may be attributed to the high temperature accelerating chemical reaction rates in the battery, combined with the substantial external pressure and the lack of pressure as an input feature, leading to larger estimation errors. However, the errors remain within a reasonable range, and the proposed algorithm achieves accurate SOC predictions across all temperatures, keeping errors well-

controlled. Compared to varying pressure conditions, the model delivers more accurate predictions across temperature variations, indicating that temperature, relative to pressure, serves as a more critical input variable.

Trajectory tracking in Figs. 14, 15, and 16 provides detailed results for each temperature condition, showing the relationship between actual and predicted SOC for each battery. As seen in the Fig., the predicted trajectory closely matches the actual trajectory under 10 °C, 25 °C, and 40 °C conditions. Similar to the experiments under varying pressure, the primary sources of error are concentrated at the beginning and end of the discharge phase.

As temperature increases, the model's prediction accuracy declines. Under low (10 °C) and moderate (25 °C) temperature conditions, the model generally tracks SOC variations well, despite occasional deviations. However, at high temperatures (40 °C), deviations become more frequent and pronounced, especially toward the later stages of

![Figure 16: Trajectory tracking of the estimated and actual SOC on 40 °C for six batteries. Each subplot (a-f) shows SOC (%) vs. Absolute Time (s) from 0 to 3000. A blue line represents 'Actual SOC' and a red line represents 'Predicted SOC'. Both lines show a linear decrease from 100% to approximately 10% over the 3000-second period. Each plot includes a zoomed-in view of the initial 1000 seconds, showing the high accuracy of the prediction model.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 16: Trajectory tracking of the estimated and actual SOC on 40 °C for six batteries. Each subplot (a-f) shows SOC (%) vs. Absolute Time (s) from 0 to 3000. A blue line represents 'Actual SOC' and a red line represents 'Predicted SOC'. Both lines show a linear decrease from 100% to approximately 10% over the 3000-second period. Each plot includes a zoomed-in view of the initial 1000 seconds, showing the high accuracy of the prediction model.

Fig. 16. Trajectory tracking of the estimated and actual SOC on 40 °C, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

![Figure 17: Error trajectory tracking for six batteries at three different temperatures. The legend identifies the batteries by color: No.1 (blue), No.2 (red), No.3 (green), No.4 (magenta), No.5 (cyan), and No.6 (yellow). Subplots (a), (b), and (c) show the Absolute Error (SOC) vs. Absolute Time (s) for 10 °C, 25 °C, and 40 °C, respectively. The error fluctuates over time, with higher temperatures generally showing larger and more frequent peaks in error.](252ea48d02dce93965b91746fb376f35_img.jpg)

Figure 17: Error trajectory tracking for six batteries at three different temperatures. The legend identifies the batteries by color: No.1 (blue), No.2 (red), No.3 (green), No.4 (magenta), No.5 (cyan), and No.6 (yellow). Subplots (a), (b), and (c) show the Absolute Error (SOC) vs. Absolute Time (s) for 10 °C, 25 °C, and 40 °C, respectively. The error fluctuates over time, with higher temperatures generally showing larger and more frequent peaks in error.

Fig. 17. Error trajectory tracking. (a) ~ (d) correspond to the results at 10 °C, 25 °C, 40 °C, respectively.

testing. This indicates that temperature is a critical factor affecting SOC estimation accuracy, particularly under extreme high-temperature conditions.

The absolute error plots—(a) 10 °C, (b) 25 °C, and (c) 40 °C—show the absolute SOC estimation error for each battery throughout the test period. The figures reveal considerable fluctuations in error across different batteries at various time points, with larger deviations occurring at the beginning and end of the test. For instance, in plot (a), Batteries No.1 and No.2 reach peak error around 150 s, then rapidly decrease, only to show larger errors again near the end. In contrast, under 40 °C conditions in plot (c), errors fluctuate more significantly throughout the entire test period, particularly for Battery No.4, whose

error curve exhibits multiple peaks, indicating that high temperature severely impacts the stability of SOC estimation.

In summary, different temperatures significantly impact battery SOC estimation. Under low-temperature conditions (10 °C), although some fluctuations in error are observed, the overall estimation accuracy remains high. However, at high temperatures (40 °C), error variability increases, with certain batteries (such as No.4) being more significantly affected. This may be due to high temperatures accelerating internal chemical reactions within the battery, thereby increasing the challenge for the prediction model in dynamic tracking.

**Table 4**  
Battery SOC estimation errors index on under different method.

| No.  | MAE      |        |        | MSE      |        |        | R <sup>2</sup> |        |        | Time     |        |       |
|------|----------|--------|--------|----------|--------|--------|----------------|--------|--------|----------|--------|-------|
|      | P-BiLSTM | BiLSTM | LSTM   | P-BiLSTM | BiLSTM | LSTM   | P-BiLSTM       | BiLSTM | LSTM   | P-BiLSTM | BiLSTM | LSTM  |
| No.1 | 0.7136   | 0.8968 | 0.9908 | 0.6269   | 1.2044 | 1.4686 | 0.9992         | 0.9985 | 0.9982 | 87.02    | 40.89  | 19.68 |
| No.2 | 0.2704   | 0.7252 | 0.4553 | 0.1916   | 0.7451 | 0.3524 | 0.9998         | 0.9991 | 0.9996 | 84.18    | 40.64  | 19.31 |
| No.3 | 0.5960   | 0.4320 | 0.5282 | 0.5134   | 0.2480 | 0.3934 | 0.9994         | 0.9997 | 0.9995 | 83.14    | 40.33  | 19.61 |
| No.4 | 0.5739   | 0.3092 | 0.5804 | 0.5850   | 0.1251 | 0.6192 | 0.9993         | 0.9998 | 0.9993 | 84.57    | 40.55  | 19.33 |
| No.5 | 0.2781   | 0.3654 | 0.3965 | 0.1465   | 0.2157 | 0.3238 | 0.9998         | 0.9997 | 0.9996 | 88.32    | 41.10  | 19.49 |
| No.6 | 0.6424   | 0.8095 | 0.8919 | 0.5903   | 0.8805 | 1.1988 | 0.9993         | 0.9989 | 0.9985 | 86.49    | 41.15  | 19.51 |
| Avg. | 0.5124   | 0.5897 | 0.6405 | 0.4423   | 0.5698 | 0.7260 | 0.9995         | 0.9993 | 0.9991 | 85.62    | 40.78  | 19.49 |

![Figure 18: Histogram of error metrics comparing P-BiLSTM, BiLSTM, and LSTM across MAE, MSE, and R^2.](b05a8a3551db31147979064952179990_img.jpg)

Figure 18 consists of three subplots comparing the performance of three methods: P-BiLSTM (blue), BiLSTM (orange), and LSTM (green) across three error metrics: (a) MAE, (b) MSE, and (c)  $R^2$ . The x-axis for all subplots represents battery numbers 1 through 6. In subplot (a) MAE, P-BiLSTM generally shows the lowest error, followed by BiLSTM and then LSTM. In subplot (b) MSE, P-BiLSTM again shows the lowest error, with BiLSTM and LSTM having higher errors. In subplot (c)  $R^2$ , all three methods show very high correlation, with P-BiLSTM consistently achieving the highest  $R^2$  values across all batteries.

Figure 18: Histogram of error metrics comparing P-BiLSTM, BiLSTM, and LSTM across MAE, MSE, and R^2.

Fig. 18. Histogram of error metrics: comparison of different method, (a) MAE, (b)MSE, (c)  $R^2$ .

![Figure 19: Trajectory tracking of estimated and actual SOC for six batteries, with zoomed-in views.](e6b5ee67ac260b0a3ed3e3c5ad7ea19c_img.jpg)

Figure 19 displays the trajectory tracking of State of Charge (SOC) for six different batteries, labeled (a) through (f). Each subplot shows the Actual SOC (black line) and the estimated SOC for P-BiLSTM (blue line), BiLSTM (orange line), and LSTM (green line). The main plot shows SOC (%) on the y-axis (0 to 100) versus Absolute Time (s) on the x-axis (0 to 3000). Each subplot includes a zoomed-in view in the top right corner, showing a detailed comparison of the estimated SOC trajectories during a specific time interval. The zoomed-in views highlight the superior tracking performance of P-BiLSTM, which closely follows the actual SOC trajectory with minimal deviation.

Figure 19: Trajectory tracking of estimated and actual SOC for six batteries, with zoomed-in views.

Fig. 19. Trajectory tracking of the estimated and actual SOC on different methods, (a) ~ (f) is corresponding results for each battery, with the zoomed-in view.

### 4.3.3. Comparative analysis

To further analyze the superiority of the proposed algorithm, we conducted comparison experiments under the conditions of 600 N, 1C, and 40 °C. The proposed P-BiLSTM was compared with standard BiLSTM and LSTM algorithms. Error metrics are presented in Table 4, with a visual representation in Fig. 18. Fig. 19 shows the SOC tracking curves for each test battery, and Fig. 20 illustrates the absolute error for each battery.

From Table 4, it is evident that the P-BiLSTM method outperforms the other two methods in terms of error metrics, demonstrating the effectiveness of the proposed physics-based constraints. For example, in the case of No.1 battery, the MAE of P-BiLSTM is 0.7136, which is lower than BiLSTM (0.8968) and LSTM (0.9908), representing reductions of 20.45 % and 27.96 %, respectively. This indicates that the predictions of P-BiLSTM are closer to the actual values. Regarding the MSE metric, P-BiLSTM achieves a value of 0.6269, which is significantly lower than BiLSTM (1.2044) and LSTM (1.4686), with reductions of 47.93 % and 57.30 %, respectively, further confirming the superiority of P-BiLSTM in reducing prediction errors. The comparison of these results can be visually observed in Fig. 18.

In terms of computational efficiency, P-BiLSTM requires more computational resources, with an average training time of 85.62 s compared to 40.78 s for BiLSTM and 19.49 s for LSTM. This increased training time reflects the additional computational complexity introduced by the physical constraints and bidirectional architecture. Specifically, P-BiLSTM takes approximately 110 % longer than BiLSTM and

339 % longer than LSTM.

When comparing different batteries, the advantage of P-BiLSTM is not consistently reflected across all metrics. However, the overall trend shows that P-BiLSTM provides more stable and accurate predictions for battery SOC estimation tasks. Particularly under conditions of low error (MAE) and lower MSE, P-BiLSTM performs outstandingly. This trend can be visually observed in Fig. 18. Except for No.3 and No.4, P-BiLSTM achieves the best performance across the batteries. Even in these two cases where it is not the best, the errors remain relatively small and fall around the median error range. This could indicate that the P-BiLSTM algorithm has reached its performance limit, further emphasizing its robustness.

From Fig. 19 and Fig. 20, it is clear that all three methods can effectively track the actual SOC trajectory, with P-BiLSTM achieving the most accurate and stable predictions. Specifically, P-BiLSTM maintains the lowest absolute error, consistently keeping it within 1 %, outperforming both BiLSTM and LSTM across all test batteries. Notably, during the initial discharge and end-of-discharge phases, the incorporation of physics-based constraints enables P-BiLSTM to control errors effectively, closely following the true SOC values with minimal deviations. In contrast, BiLSTM and LSTM exhibit larger errors and greater variability, particularly during periods of rapid SOC changes or when errors accumulate over time. These results underscore that P-BiLSTM not only improves prediction accuracy but also enhances robustness and adaptability under varying battery conditions, establishing it as a superior method for SOC estimation.

![Figure 20: Error trajectory tracking for six batteries (No.1 to No.6). Each plot shows Absolute Error (SOC) vs. Absolute Time (s). The legend indicates three methods: P-BiLSTM (blue), BiLSTM (orange), and LSTM (green). Each plot includes an inset showing a zoomed-in view of the error between 2250 and 2750 seconds. The P-BiLSTM method consistently shows the lowest error across all batteries.](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 20: Error trajectory tracking for six batteries (No.1 to No.6). Each plot shows Absolute Error (SOC) vs. Absolute Time (s). The legend indicates three methods: P-BiLSTM (blue), BiLSTM (orange), and LSTM (green). Each plot includes an inset showing a zoomed-in view of the error between 2250 and 2750 seconds. The P-BiLSTM method consistently shows the lowest error across all batteries.

Fig. 20. Error trajectory tracking. (a) ~ (d) correspond to the results at Different Methods.

# 5. Conclusion

Considering that the existing data-driven methods overlook the influence of external preload pressure on battery performance while lacking certain physical limitations, this study proposes a P-BiLSTM method for accurate SOC estimation. The proposed approach first incorporates external pressure and temperature as key feature inputs of the network model by experimental data analysis, then embeds SOC variation patterns into the loss function and enforces physical constraints in the data preprocessing and model output stage to ensure that outputs remain within the valid SOC range. The quantitative evaluations and the superiority comparison of the proposed SOC estimation are carried out under various pressures and temperatures. The experimental results demonstrate that preload pressure significantly impacts SOC accuracy, with lower pressure causing less effect, and at 600 N, the average absolute error in SOC estimation reaches a maximum of 0.7890, while the minimum MAE is 0.1654. These findings provide strong support for the performance improvement of BMS. In addition, the insights from our study can guide practical applications by offering manufacturers clear benchmarks for preload pressure during assembly, ensuring optimal battery pack design and assembly. The inclusion of external pressure signals in the P-BiLSTM model enhances the accuracy and reliability of SOC estimation across fluctuating environmental conditions, such as those experienced in electric vehicles.

In summary, the P-BiLSTM proposed in this paper effectively addresses the issues of insufficient accuracy and neglect of physical laws found in traditional SOC estimation methods. By introducing external pressure signals, embedding physical knowledge, and applying constraint mechanisms, the accuracy, robustness, and adaptability of battery SOC estimation are improved. Future work can focus on applicability of the proposed SOC method in complex working conditions. Additionally, the impact of different initial SOC values on estimation accuracy is also the important direction to focus on research in the future.

# CRediT authorship contribution statement

**Longxing Wu:** Writing – review & editing, Writing – original draft, Supervision, Methodology, Investigation, Funding acquisition. **Xinyuan**

**Wei:** Visualization, Methodology, Investigation, Conceptualization. **Chunsong Lin:** Writing – original draft, Validation, Supervision, Project administration. **Zebo Huang:** Visualization, Conceptualization. **Yuqian Fan:** Methodology, Data curation. **Chunhui Liu:** Writing – review & editing, Validation. **Shuping Fang:** Writing – review & editing, Visualization.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgments

This work is supported by Anhui Province Applied Peak Discipline Mechanical Engineering (NO. XK-XJGF004) and Open Foundation of Hubei Key Laboratory for High-efficiency Utilization of Solar Energy and Operation Control of Energy Storage System (NO. HBSEES202308).

# Data availability

The data is available for download from Ref. [40].

# References

- [1] H. Pang, K. Chen, Y. Geng, et al., Accurate capacity and remaining useful life prediction of lithium-ion batteries based on improved particle swarm optimization and particle filter, *Energy* 130555 (2024).
- [2] M. Wei, M. Ye, C. Zhang, et al., Integrating mechanism and machine learning based capacity estimation for LiFePO4 batteries under slight overcharge cycling, *Energy* 296 (2024) 131208.
- [3] L. Wu, K. Liu, J. Liu, H. Pang, Evaluating the heat generation characteristics of cylindrical lithium-ion battery considering the discharge rates and N/P ratio, *J. Energy Storage* 64 (2023) 107182.
- [4] Z. Li, Y. Yang, L. Li, et al., A weighted Pearson correlation coefficient based multi-fault comprehensive diagnosis for battery circuits, *J. Energy Storage* 60 (2023) 106584.
- [5] L. Lyu, L. Wu, M. Lyu, et al., Towards an intelligent battery management system for electric vehicle applications: dataset considerations, algorithmic approaches, and future trends, *J. Energy Storage* 101 (2024) 113827.

- [6] L. Wu, Z. Lyu, Z. Huang, C. Zhang, et al., Physics-based battery SOC estimation methods: recent advances and future perspectives, *J. Energy Chem.* 89 (2024) 27–40.
- [7] F. Berger, D. Joest, E. Barbers, et al., Benchmarking battery management system algorithms—requirements, scenarios and validation for automotive applications, *ETransportation* 22 (2024) 100355.
- [8] A.K. Singh, K. Kumar, U. Choudhury, et al., Applications of artificial intelligence and cell balancing techniques for battery management system in electric vehicles: a comprehensive review, *Process. Saf. Environ. Prot.* 191 (2024) 2247–2265.
- [9] M. Sudarshan, A. Serov, C. Jones, et al., Data-driven autoencoder neural network for onboard BMS Lithium-ion battery degradation prediction, *J. Energy Storage* 82 (2024) 110575.
- [10] Y. Wang, J. Tian, Z. Sun, et al., A comprehensive review of battery modeling and state estimation approaches for advanced battery management systems, *Renew. Sust. Energ. Rev.* 131 (2020) 110015.
- [11] H. Pang, Y. Geng, X. Liu, et al., A composite state of charge estimation for electric vehicle lithium-ion batteries using back-propagation neural network and extended Kalman particle filter, *J. Electrochem. Soc.* 169 (11) (2022) 110516.
- [12] D. Sesidhar, C. Badachi, R.C. Green II, A review on data-driven SOC estimation with Li-ion batteries: implementation methods & future aspirations, *J. Energy Storage* 72 (2023) 108420.
- [13] K. Zhang, R. Xiong, Q. Li, et al., A novel pseudo-open-circuit voltage modeling method for accurate state-of-charge estimation of LiFePO4 batteries, *Appl. Energy* 347 (2023) 121406.
- [14] H. Dai, X. Wei, Z. Sun, et al., Online cell SOC estimation of Li-ion battery packs using a dual time-scale Kalman filtering for EV applications, *Appl. Energy* 95 (2012) 227–237.
- [15] H. Yu, H. Lu, Z. Zhang, et al., A generic fusion framework integrating deep learning and Kalman filter for state of charge estimation of lithium-ion batteries: analysis and comparison, *J. Power Sources* 623 (2024) 235493.
- [16] S. Barik, B. Saravanan, Recent developments and challenges in state-of-charge estimation techniques for electric vehicle batteries: a review, *J. Energy Storage* 100 (2024) 113623.
- [17] J. Xiao, Y. Xiong, Y. Zhu, et al., Multi-innovation adaptive Kalman filter algorithm for estimating the SOC of lithium-ion batteries based on singular value decomposition and Schmidt orthogonal transformation, *Energy* 312 (2024) 133597.
- [18] C. Zhu, S. Wang, C. Yu, et al., An improved Cauchy robust correction-sage Husa extended Kalman filtering algorithm for high-precision SOC estimation of lithium-ion batteries in new energy vehicles, *J. Energy Storage* 88 (2024) 111552.
- [19] Z. He, X. Fu, C. Pan, et al., Research on lithium battery state of charge estimation based on improved adaptive iterative eXogenous Kalman filter and multidimensional estimation scheme, *J. Energy Storage* 97 (2024) 112763.
- [20] M. Zhan, B. Wu, G. Xu, et al., Application of adaptive extended Kalman algorithm based on strong tracking fading factor in state-of-charge estimation of lithium-ion battery, *Energy* 284 (2023) 129095.
- [21] L. Wu, K. Liu, H. Pang, Evaluation and observability analysis of an improved reduced-order electrochemical model for lithium-ion battery, *Electrochim. Acta* 368 (2021) 137604.
- [22] Y. Wang, X. Zhang, K. Liu, et al., System identification and state estimation of a reduced-order electrochemical model for lithium-ion batteries, *Etransportation* 18 (2023) 100295.
- [23] S. Oh, J. Kim, I. Moon, Hybrid data-driven deep learning model for state of charge estimation of Li-ion battery in an electric vehicle, *J. Energy Storage* 97 (2024) 112887.
- [24] Z. Deng, X. Hu, X. Lin, et al., Data-driven state of charge estimation for lithium-ion battery packs based on Gaussian process regression, *Energy* 205 (2020) 118000.
- [25] B. Liu, H. Wang, M.L. Tseng, et al., State of charge estimation for lithium-ion batteries based on improved barnacle mating optimizer and support vector machine, *J. Energy Storage* 55 (2022) 105830.
- [26] H. Srourui, A. Oshnoei, Y. Che, et al., A comprehensive review of hybrid battery state of charge estimation: exploring physics-aware AI-based approaches, *J. Energy Storage* 100 (2024) 113604.
- [27] F. Yang, W. Li, C. Li, et al., State-of-charge estimation of lithium-ion batteries based on gated recurrent neural network, *Energy* 175 (2019) 66–75.
- [28] J. Wang, Z. Zuo, Y. Wei, et al., State of charge estimation of lithium-ion battery based on GA-LSTM and improved IAKF, *Appl. Energy* 368 (2024) 123508.
- [29] Y.X. Wang, Z. Chen, W. Zhang, Lithium-ion battery state-of-charge estimation for small target sample sets using the improved GRU-based transfer learning, *Energy* 244 (2022) 123178.
- [30] M.S.H. Lipu, M.A. Hannan, A. Hussain, et al., Data-driven state of charge estimation of lithium-ion batteries: algorithms, implementation factors, limitations and future trends, *J. Clean. Prod.* 277 (2020) 124110.
- [31] Z. Sherkatghanad, A. Ghazanfari, V. Makarenkov, A self-attention-based CNN-bi-LSTM model for accurate state-of-charge estimation of lithium-ion batteries, *J. Energy Storage* 88 (2024) 111524.
- [32] J. Tian, R. Xiong, J. Lu, et al., Battery state-of-charge estimation amid dynamic usage with physics-informed deep learning, *Energy Storage Mater.* 50 (2022) 718–729.
- [33] H. Lv, D. Kong, P. Ping, et al., Anomaly detection of LiFePO4 pouch batteries expansion force under preload force, *Process Saf. Environ. Prot.* 176 (2023) 1–11.
- [34] P. Xu, J. Li, Q. Xue, et al., A syncrotic state-of-charge estimator for LiFePO4 batteries leveraging expansion force, *J. Energy Storage* 50 (2022) 104559.
- [35] E. Kwak, D.S. Son, S. Jeong, et al., Characterization of the mechanical responses of a LiFePO4 battery under different operating conditions, *J. Energy Storage* 28 (2020) 101269.
- [36] H. Dai, C. Yu, X. Wei, Z. Sun, State of charge estimation for lithium-ion pouch batteries based on stress measurement, *Energy* 129 (2017) 16–27.
- [37] M. Liu, J. Xu, Y. Jiang, et al., Multi-dimensional features based data-driven state of charge estimation method for LiFePO4 batteries, *Energy* 274 (2023) 127407.
- [38] N.A. Samad, Y. Kim, J.B. Siegel, et al., Battery capacity fading estimation using a force-based incremental capacity analysis, *J. Electrochem. Soc.* 163 (2016) A1584–A1594.
- [39] S. Niu, G. Zhu, J. Xu, et al., Analysis on the effect of external press force on the performance of LiNi0.8Co0.1Mn0.1O2/graphite large pouch cells, *J. Energy Storage* 44 (2021) 103425.
- [40] C. Yan, X. Wu, Y. Yuan, et al., Experimental data simulating lithium battery charging and discharging tests under different external constraint pressure conditions, *Data Brief* 55 (2024) 110616.
- [41] C. Lin, X. Tuo, L. Wu, et al., Accurate capacity prediction and evaluation with advanced SSA-CNN-BiLSTM framework for lithium-ion batteries, *Batteries* 10 (3) (2024) 71.
- [42] P.V.D.C. Souza, M. Dragoni, IFNN: enhanced interpretability and optimization in FNN via Adam algorithm, *Inf. Sci.* 678 (2024) 1–12.
- [43] B. Yan, W. Zheng, D. Tang, et al., A knowledge-constrained CNN-BiLSTM model for lithium-ion batteries state-of-charge estimation, *Microelectro42nics Reliability* 150 (2023) 115112.