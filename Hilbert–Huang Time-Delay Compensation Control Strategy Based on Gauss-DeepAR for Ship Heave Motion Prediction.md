

# Hilbert–Huang Time-Delay Compensation Control Strategy Based on Gauss-DeepAR for Ship Heave Motion Prediction

ZHANG Qin, HE Dai-jing, GU Bang-ping, HU Xiong\*

Logistics Engineering College, Shanghai Maritime University, Shanghai 201306, China

Received January 3, 2024; revised May 17, 2024; accepted June 20, 2024

©2025 Chinese Ocean Engineering Society and Springer-Verlag GmbH Germany, part of Springer Nature

## Abstract

The prediction and compensation control of marine ship motion is crucial for ensuring the safety of offshore wind turbine loading and unloading operations. However, the accuracy of prediction and control is significantly affected by the hysteresis phenomenon in the wave compensation system. To address this issue, a ship heave motion prediction is proposed in this paper on the basis of the Gauss-DeepAR (AR stands for autoregressive recurrent) model and the Hilbert–Huang time-delay compensation control strategy. Initially, the zero upward traveling wave period of the level 4–6 sea state ship heave motion is analyzed, which serves as the input sliding window for the Gauss-DeepAR prediction model, and probability predictions at different wave direction angles are conducted. Next, considering the hysteresis characteristics of the ship heave motion compensation platform, the Hilbert–Huang transform is employed to analyze and calculate the hysteresis delay of the compensation platform. After the optimal control action value is subsequently calculated, simulations and hardware platform tests are conducted. The simulation results demonstrated that the Gauss-DeepAR model outperforms autoregressive integrated moving average model (ARIMA), support vector machine (SVM), and longshort-term memory (LSTM) in predicting non-independent identically distributed datasets at a 90° wave direction angle in the level 4–6 sea states. Furthermore, the model has good predictive performance and generalizability for non-independent and non-uniformly distributed datasets at a 180° wave direction angle. The hardware platform compensation test results revealed that the Hilbert–Huang method has an outstanding effect on determining the hysteretic delay and selecting the optimal control action value, and the compensation efficiency was higher than 90% in the level 4–6 sea states.

**Key words:** heave motion, Gauss-DeepAR prediction model, Hilbert–Huang transform, delay compensation control

**Citation:** Zhang, Q., He, D.J., Gu, B.P., Hu, X., 2025. Hilbert–Huang time-delay compensation control strategy based on Gauss-DeepAR for ship heave motion prediction. China Ocean Eng., 39(2): 209–224, doi: <https://doi.org/10.1007/s13344-025-0016-7>

## 1 Introduction

Driven by the marine power strategy and propelled by the ongoing promotion of the offshore wind power initiatives outlined in the “14th Five-Year Plan”, there is a growing demand for more powerful offshore turbines, particularly in the megawatt range. The power scale of offshore turbines is progressively expanding to harness the full efficiency of the ocean. During ship lifting operations in a challenging marine environment characterized by wind, waves, and swells, vessels undergo six degrees of freedom motion—roll, pitch, yaw, sway, surge and heave. Among them, sway, surge and yaw can be effectively alleviated by anchoring, and the adoption of a dynamic positioning system can effectively restrain the longitudinal and lateral motion of a ship (Ding et al., 2023). However, owing to the large variation range of heave motion, the operating platform will shake violently (Wang et al., 2021), and roll and pitch will also

lead to additional heave motion, therefore, the heave motion of the ship is the biggest disturbance to safe and efficient offshore operations. To mitigate the impact on ships’ offshore operations and ensure stable and efficient ship operations in complex sea states, it is imperative to conduct research on wave compensation control (Do and Pan, 2008; Wei et al., 2019). Because the compensation control system involves many links, the control process has a certain hysteresis (Tang et al., 2021a), so the control performance of the wave compensation system decreases, which affects the prediction and compensation accuracy of the ship heave motion. To obtain a dynamic real-time control effect and solve problems such as system hysteresis, researchers have developed a wave compensation control system and optimization strategy for the high-precision prediction of ship heave motion (Tang et al., 2021a, 2021b; Dong et al., 2022). Achieving a dynamic and real-time control effect necessitates high-pre-

Foundation item: The study was financially supported by the National Natural Science Foundation of China (Grant No. 52105466).

\*Corresponding author. E-mail: [huxiong@shmtu.edu.cn](mailto:huxiong@shmtu.edu.cn)

cision prediction of ship heave motion.

Ship heave motion prediction methods can be categorized into three groups: physical methods, statistical methods, and artificial intelligence methods. The calculation process of ship motion models based on physical processes (Dai et al., 2019) is intricate and expensive, leading to a decline in its usage among scholars. Statistical methods involve extracting information from historical time series data for ship prediction. Commonly used statistical forecasting methods include the classic autoregressive model (AR) (Pan et al., 2023), moving average model (MA) (Huang et al., 2021), autoregressive moving average model (ARMA) (Xin et al., 2023; Dong et al., 2022), and ARIMA (Sheikh Khozani et al., 2022; Luzia et al., 2023; Schaffer et al., 2021). While statistical prediction methods are relatively straightforward, they may fail to extract the complex rules inherent in ship heave time series.

With the rapid development of computer technology, many artificial intelligence prediction methods have been introduced into the field of ship motion prediction. These methods use machine learning technologies to dig deep into the complex nonlinear relationships contained in the data, not only achieving high-precision real-time prediction but also showing strong robustness, which provides strong support for safe navigation and efficient operation of ships. The SVM is a common model widely used in machine learning and can be used to solve a variety of problems, such as classification and regression. Liu et al. (2014) proposed a new ship motion prediction method based on empirical mode decomposition and an SVM, aiming at the nonlinearity and nonstationarity of ship motion in waves. Liu et al. (2019) introduced an online ship motion prediction method based on an SVM that uses a genetic algorithm to optimize model parameters. Deep learning is a machine learning method based on nonlinear neural networks aimed at solving complex tasks and improving the accuracy and efficiency of artificial intelligence. Murray and Perera (2021) proposed a deep learning framework for predicting ship area behavior via time series of historical data to forecast likely future trajectories. Recurrent neurons, especially LSTM neural networks, are widely employed in this domain. Hu et al. (2021) integrated a novel dual-channel LSTM neural network model to predict the heave motion of ships. Liu et al. (2023a) proposed an LSTM neural network prediction model for heave, pitch, and surge three-degree-of-freedom motions of large cruise ships. In addition, many scholars have also studied the optimization of the model parameters of neural networks. Peng et al. (2019) used an improved particle swarm optimization algorithm to optimize LSTM neural network model parameters for ship motion attitude prediction. Zhang et al. (2020) proposed an adaptive dynamic particle swarm optimization algorithm to optimize the hyperparameters of the LSTM prediction model for ship motion attitude prediction.

However, actual ship motion is inherently unstable, and a single prediction model may fall short of meeting the complex demands of engineering applications. In recent years, scholars have explored combining different algorithms with neural networks for training purposes. Skulstad et al. (2021) integrated a supervised machine learning (ML) model with LSTM to predict ship position information. Wen et al. (2021) combined a machine learning algorithm with particle swarm optimization (PSO) and introduced a method to determine the optimal range of marine solar power generation for shipboard photovoltaic power systems. This approach considers various environmental variables and the impact of ship movement and rolling. Zhang et al. (2023) proposed a convolutional neural network attention mechanism model based on an improved whale optimization algorithm (WOA) to improve the accuracy and stability of ship motion prediction, aiming at the nonstationarity, nonlinearity and randomness of ship motion and inaccuracy of traditional prediction methods. Liu et al. (2023b) proposed a new combined model based on fully extended empirical mode decomposition and whale optimization algorithm gated cycle unit networks for high-precision ship motion prediction. The DeepAR model is a deep learning application that combines the structure and principle of a neural network with the special processing method of time series data. It can successfully learn the dynamic pattern of data and take its unique quantile loss as the optimization target to generate the probability distribution interval of the predicted value, providing a more comprehensive and reliable basis for prediction. Salinas et al. (2020) trained numerous neural network models related to time series, introducing a probabilistic forecasting with autoregressive recurrent (DeepAR) method that combines deep learning and probabilistic models. Different likelihood functions suitable for various time series are explored, demonstrating accurate forecasting with minimal manual intervention. Jeon and Seong (2022) modified the training process of the DeepAR model to address discontinuities and irregularities in time series and proposed a robust recursive DeepAR model for discontinuous time series prediction.

The hardware test platform is susceptible to noise, missing values, and inconsistent data, and low-quality data complicate the extraction of data features. Therefore, preprocessing and characterizing the data are essential.

Discrete wavelet transformation (DWT) (De-Jun et al., 2016) and variational modal decomposition (VMD) are commonly used data preprocessing methods to process data before further analysis (Dragomiretskiy and Zosso, 2014). Empirical mode decomposition (EMD) can extract different frequencies and residual components of a signal (Nie et al., 2022; Geng et al., 2023) and realize gradual decomposition from high frequency to low frequency (Zhou et al., 2023), which helps reduce random interference in the data series (Nikita and Karan, 2021). Tu et al. (2018) designed a sea

state recognition method using the HHT transformation to classify the surge, sway, roll and yaw of ship attitude motion. Hamad et al. (2009) suggested the use of the Hilbert–Huang transform for travel speed prediction. They combined empirical mode decomposition, a multi-layer feedforward neural network, and backpropagation to achieve unbiased speed predictions.

In summary, existing prediction methods often overlook the significance of probabilistic predictions corresponding to the predicted values in practical engineering, and specific research on the hysteresis delay of hardware platforms is lacking. Consequently, this paper proposes a Hilbert–Huang time-delay compensation control strategy based on Gauss-DeepAR for ship heave motion prediction. The Hilbert–Huang time-delay compensation control strategy based on Gauss-DeepAR ship heave motion prediction is shown in Fig. 1. First, the heave motion data of the level 4–6 sea states are collected, the input sliding window size of the Gauss-DeepAR prediction model is determined, and then, probabilistic predictions of heave motion data at different wave direction angles are completed. Considering the hysteresis characteristics of the ship heave motion compensation platform, the hysteresis delay of the compensation platform is analyzed via the Hilbert–Huang transform. Finally, the optimal control action value is obtained via calculation, which is used in the compensation test on the hardware platform.

The structure of this paper is organized as follows: The

second section introduces the establishment of the Gauss-DeepAR model. The third section focuses on the compensation control of ship heave motion. The fourth section presents the hardware platform test results. The conclusions are given in the final section.

## 2 Gauss-DeepAR model

To ensure the efficiency and safety of offshore operations such as accommodation ladder transportation and crane installation, wave compensation control is needed to maintain platform stability, and high-precision prediction is the basis of compensation control. In this work, the Gauss-DeepAR model is used to predict the ship heave motion.

DeepAR (Salinas et al., 2020) is an autoregressive recurrent neural network model based on a deep learning time series prediction algorithm that is suitable for large-scale time series data prediction with periodic and long-term patterns. It is a model designed for time series prediction in practical engineering application scenarios. Fig. 2 shows the structure diagram of the DeepAR model, which is successively divided into an input layer, an LSTM layer, a likelihood function layer and a predicted value layer from bottom to top. The time series of ship heave motion can be predicted by the four layers of the DeepAR model from top to bottom.

### 2.1 Input layer

The DeepAR model input layer variables are  $Z_t$  and  $x_{i,t}$ .  $Z_t$  represents the value of the heave time series at time  $t$ , and  $x_{i,t}$  are covariates, which are variables used to explain or

![Figure 1: Diagram of the method for the Hilbert–Huang time-delay compensation control strategy based on Gauss-DeepAR for ship heave prediction. The diagram is divided into three main sections: the Gauss-DeepAR model (top left), the calculating mechanism of the optimal control action value (bottom left), and the Hilbert transform (right).](062ad684575a714449a7e040c0e1ec00_img.jpg)

The diagram illustrates the workflow for the Hilbert–Huang time-delay compensation control strategy based on Gauss-DeepAR for ship heave prediction. It is divided into three main sections:

- Gauss-DeepAR model (Top Left):**
  - Train data path:** Train data → Calculate sliding window → Input layer → LSTM layer → Likelihood function layer → Loss function satisfy accuracy? (No → Parameter adjustment → Input layer; Yes → End).
  - Test data path:** Test data → Calculate sliding window → Storage model → Probability prediction interval.
- Calculating mechanism of the optimal control action value (Bottom Left):**
  - Identify known data points → Construct interpolation functions → Apply interpolation functions.
  - Perform interpolation calculations → Verify interpolation results.
- Hilbert transform (Right):**
  - EMD transform (Top):** Find the maximum and minimum → Make their envelope lines → Finding the mean of envelope lines → Subtract the mean of the envelope from raw data to obtain suspected IMF.
  - Decision Loop:** Determine whether the IMF component meets the criteria.
    - If Yes: IMF is the highest frequency component → Subtract IMF from raw data to obtain a signal → Return to EMD transform.
    - If No: IMF is not the highest frequency component → Use the current IMF component as the raw signal → New signal monotonicity? (Yes → End; No → Return to EMD transform).
  - Hilbert transform (Bottom):** Remove residuals → Perform Hilbert transform on data → Extracting analytical signals from Hilbert transform → Calculate the instantaneous phase of the analyzed signal → Calculate the instantaneous frequency of the analyzed signal → Find the Hilbert spectrum of the analyzed signal.

The central flow connects the Gauss-DeepAR model to the calculating mechanism and the Hilbert transform. It involves collecting and determining the input step size, making Deep AR model predictions, determining platform hysteresis delay, calculating the optimal control action value, determining compensation data input, and finally obtaining compensation results.

Figure 1: Diagram of the method for the Hilbert–Huang time-delay compensation control strategy based on Gauss-DeepAR for ship heave prediction. The diagram is divided into three main sections: the Gauss-DeepAR model (top left), the calculating mechanism of the optimal control action value (bottom left), and the Hilbert transform (right).

Fig. 1. Diagram of the method for the Hilbert–Huang time-delay compensation control strategy based on Gauss-DeepAR for ship heave prediction.

![Structural diagram of the DeepAR model. The diagram illustrates the flow of data through the model layers. It starts with an 'Input layer' containing a circle for Z_{t-w+1} and a rectangle for X_{i,t-w}. This feeds into an 'LSTM layer' which consists of multiple cells. Each cell takes inputs Z_{t-1}, x_{i,t-1}, h_{t-1}, and c_{t-1} to produce h_t and c_t. The LSTM layer feeds into a 'Likelihood function layer' which contains a rectangle for l(Z_{t-w} | \theta_{t-w}). This layer feeds into a 'Predicted value layer' containing a circle for Z_{t-w}. The diagram shows a sequence of these layers for different time steps, with ellipses indicating the continuation of the sequence.](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

Structural diagram of the DeepAR model. The diagram illustrates the flow of data through the model layers. It starts with an 'Input layer' containing a circle for Z\_{t-w+1} and a rectangle for X\_{i,t-w}. This feeds into an 'LSTM layer' which consists of multiple cells. Each cell takes inputs Z\_{t-1}, x\_{i,t-1}, h\_{t-1}, and c\_{t-1} to produce h\_t and c\_t. The LSTM layer feeds into a 'Likelihood function layer' which contains a rectangle for l(Z\_{t-w} | \theta\_{t-w}). This layer feeds into a 'Predicted value layer' containing a circle for Z\_{t-w}. The diagram shows a sequence of these layers for different time steps, with ellipses indicating the continuation of the sequence.

Fig. 2. Structural diagram of the DeepAR model.

predict the change in the time series. As shown in Fig. 2, the size of the input sliding window in the input layer is  $w$ , which is determined by the zero upward traveling wave period  $T_z$ . The expression is as follows:

$$w = T_z = \frac{1}{n} \sum_{i=1}^{N} T_i. \quad (1)$$

In Eq. (1),  $T_i$  is a signal part between two adjacent upper span zeros,  $i=1, 2, \dots, N$ , and the period  $T_z$  of the traveling wave on zero is the mean value of  $NT_i$ .

### 2.2 LSTM layer

The DeepAR model used in this paper captures dynamic patterns in time series via LSTM neural networks, an improved RNN that selectively adds or removes information through input gates, forget gates, and output gates. The LSTM neural network structure is shown in the LSTM layer in Fig. 2, which has four inputs: the network input value  $Z_{t-1}$  and  $x_i$  at time  $t$ , the hidden layer state  $h_{t-1}$  and the cell state  $c_{t-1}$  at time  $t-1$ ; two outputs: the hidden layer state  $h_t$  and the cell state  $c_t$  at time  $t$ . The LSTM neural network is calculated as follows:

$$f_t = \sigma(\mathbf{W}_f \cdot [h_{t-1}, Z_t, x_{i,t}] + \mathbf{b}_f); \quad (2)$$

$$i_t = \sigma(\mathbf{W}_i \cdot [h_{t-1}, Z_t, x_{i,t}] + \mathbf{b}_i); \quad (3)$$

$$o_t = \sigma(\mathbf{W}_o \cdot [h_{t-1}, Z_t, x_{i,t}] + \mathbf{b}_o); \quad (4)$$

$$\tilde{c}_t = \tanh(\mathbf{W}_c \cdot [h_{t-1}, Z_t, x_{i,t}] + \mathbf{b}_c); \quad (5)$$

$$c_t = f_t \odot c_{t-1} + i_t \odot \tilde{c}_t; \quad (6)$$

$$h_t = o_t \odot \tanh(c_t). \quad (7)$$

In Eqs. (2)–(7),  $f_t$  represents the forgetting gate;  $i_t$  indicates the input gate;  $o_t$  represents the output gate;  $c_t$  represents the cell state;  $\sigma$  indicates the sigmoid function;  $\odot$  means Hadamard product.  $\mathbf{W}_f$ ,  $\mathbf{W}_i$ ,  $\mathbf{W}_o$ ,  $\mathbf{W}_c$ ,  $\mathbf{b}_f$ ,  $\mathbf{b}_i$  and  $\mathbf{b}_o$  are the weight coefficient matrix and bias vector of the forgetting gate,

input gate and output gate, respectively, and  $\tanh$  is the hyperbolic tangent activation function.

### 2.3 Likelihood function layer

The likelihood function layer in DeepAR not only provides the model with the ability to make probabilistic predictions but also provides the model with greater flexibility to adapt to a variety of different data and problem scenarios. The likelihood function  $l(Z_t|\theta_t)$  needs to be selected on the basis of the statistical characteristics of the data themselves, including the beta distribution, Bernoulli distribution, studentT distribution, negative binomial distribution, etc. In this simulation, the Gauss distribution function  $l_G(Z_t|\theta_t)$  is used for real-valued data, and  $\theta_t$  of the Gauss distribution is parameterized via mathematical expectation and standard deviation, i.e.,  $\theta_t=(\mu_0, \sigma_0)$ . The mathematical expectation  $\mu_0$  and standard deviation  $\sigma_0$  are calculated by the output parameters of the fully connected layer output of the LSTM network, but to ensure that the standard deviation  $\sigma_0$  is greater than zero, a softplus activation function is used to map the LSTM output  $h_t$ , Gauss distribution function  $l_G(Z_t|\theta_t)$ , and the parameters are calculated as follows:

$$l_G(Z_t|\theta_t) = l_G(Z_t|\mu_0, \sigma_0) = \frac{1}{\sqrt{2\pi\sigma_0^2}} e^{-\frac{(Z_t-\mu_0)^2}{2\sigma_0^2}}; \quad (8)$$

$$\mu_0(h_{i,t}) = \mathbf{W}_0^T h_{i,t} + \mathbf{b}_0; \quad (9)$$

$$\sigma_0(h_{i,t}) = \log(1 + e^{\mathbf{W}_0^T h_{i,t} + \mathbf{b}_0}). \quad (10)$$

The weight coefficient matrix  $\mathbf{W}_0$ , bias vector  $\mathbf{b}_0$  and LSTM network output  $h_t$  of the fully connected layer of the LSTM network output are subsequently saved to calculate  $\mu_0$  and  $\sigma_0$  of  $\theta_t$  in the Gauss likelihood function  $l_G(Z_t|\theta_t)$  in Eq. (8).

### 2.4 Training and prediction

In the Gauss-DeepAR model structure diagram shown in

Fig. 2, the solid line represents the training process of the model, and the dashed line represents the prediction process. Let  $t_1 \in [1, t_0-1]$  be the training interval and  $t_2 \in [t_0, T]$  be the prediction interval. In the training process, the zero upward traveling wave period  $w$  determined by Eq. (1) is used as the input window. In each time step  $t$ , the network input includes ship heave motion  $Z_{t-1}$ , covariate  $x_t$  and the output  $h_{t-1}$  of the LSTM at the previous time. The output  $h_t$  can be obtained through LSTM as follows:

$$h_t = \text{LSTM}(Z_{t-1}, x_t, h_{t-1}). \quad (11)$$

Finally, the maximum value of  $l_G(Z_t|\theta)$  is obtained as the loss function to further train the network:

$$l_* = \max \sum_t \log l_G(Z_t|\theta). \quad (12)$$

After training, the current network structure and parameters as well as the output result of the LSTM layer  $h_{t_0-1}$  are saved. For the prediction interval  $t \in [t_0, T]$ , the heave motion data  $Z_{t_0}$  can be obtained by using the network structure saved by training, and the predicted value  $Z_{t_0} \cdots Z_T$  can be obtained as the input of the next time  $t_0+1$  for further prediction. The process of ship heave motion prediction with the Gauss-DeepAR model is complete.

## 3 Ship heave motion compensation control

After the heave motion values of the 4–6 sea states are predicted via the Gauss-DeepAR model, wave compensation control should be carried out. In this work, a platform with six degrees of freedom for Stewart ship heave motion is used to conduct a compensation control hardware platform test.

### 3.1 Heave motion compensation platform description

The heave motion compensation test system used in this paper is shown in Fig. 3a, where ①–⑥ represent the Stewart platform, servo driver, servo motor and encoder, electric cylinder, laser sensor, industrial computer and motion control card, respectively. The first-stage platform is the Stewart platform, which is composed of six servo electric cylinders

![Figure 3a: A photograph of the heave motion compensation test system. The system consists of a Stewart platform (①) at the bottom, supported by six electric cylinders (②). Above the platform is a second-stage platform (③) with a servo motor and encoder (④). A laser sensor (⑤) is mounted on the second-stage platform. An industrial computer and motion control card (⑥) is connected to the system.](e6751f2eb226d6663ce80a2cb1603dec_img.jpg)

Figure 3a: A photograph of the heave motion compensation test system. The system consists of a Stewart platform (①) at the bottom, supported by six electric cylinders (②). Above the platform is a second-stage platform (③) with a servo motor and encoder (④). A laser sensor (⑤) is mounted on the second-stage platform. An industrial computer and motion control card (⑥) is connected to the system.

(a) Heave motion compensation test system

and static and dynamic platforms to simulate the movement of the ship in real time. The second-stage platform is a heave control system used to maintain the stability of offshore operations. It is composed of a servo drive, servo motor, encoder and electric cylinder. It is controlled by an industrial computer and motion control card to compensate for ship motion. The function of the laser sensor is to provide feedback on the position of the second-stage platform to the industrial computer to achieve a closed loop of control. The flow chart of the whole heave motion compensation test system is shown in Fig. 3b. The Stewart platform is used to simulate the heave direction motion of the ship and is transmitted to the industrial computer at the same time. The heave displacement signal can be accurately detected, and the C# language control strategy algorithm program is written on the industrial computer and transmitted to the motion control card through the PCI bus. The motion control card receives the command and sends the command to the servo driver to make the servo driver drive the electric cylinder to compensate for the heave displacement of the first-stage platform. Finally, the compensated motion of the cylinder is detected by the laser sensor, and the compensated displacement data are transmitted back to the industrial computer to detect the compensation accuracy and form a closed loop of compensation control.

In the heave motion compensation platform, hysteresis delay (Tang et al., 2021b) may arise during the transmission of data between the mechanical structure and motion control of the platform. This can lead to suboptimal effects or even instability on the compensation platform, significantly affecting compensation accuracy. Consequently, investigating the hysteresis delay on the heave compensation platform is essential to guarantee high-precision compensation outcomes.

### 3.2 Heave compensation for the hysteresis of the platform

During the operation of the heave compensation platform, an input displacement value  $x(t)$  is applied to the

![Figure 3b: Flow chart of the heave motion compensation test system. The process starts with the Stewart platform simulating ship motion. This signal goes to the Industrial computer and motion control card. The card sends a control signal to the Servo driver, which outputs a pulse signal to the Servo motor and encoder. The motor and encoder send a transmission signal to the Electric cylinder, which produces compensating displacement. Laser sensors detect this displacement and feed it back to the Industrial computer and motion control card to detect compensation accuracy.](047bc23b4e0706cbc0ff323b15fff184_img.jpg)

Figure 3b: Flow chart of the heave motion compensation test system. The process starts with the Stewart platform simulating ship motion. This signal goes to the Industrial computer and motion control card. The card sends a control signal to the Servo driver, which outputs a pulse signal to the Servo motor and encoder. The motor and encoder send a transmission signal to the Electric cylinder, which produces compensating displacement. Laser sensors detect this displacement and feed it back to the Industrial computer and motion control card to detect compensation accuracy.

(b) Flow chart of heave motion compensation test system

Fig. 3. Heave motion compensation platform.

Stewart platform, causing the platform to shift from its initial steady state to an alternative stable state. During this process, the output displacement value  $y(t)$  of the platform is collected and aggregated into the hysteresis characteristic curve of the heave compensation platform, as shown in Fig. 4. The input displacement value is  $x(t_1)$ , and the monitored output displacement values are  $y_1(t_1)$  and  $y_2(t_1)$ . In the hysteresis characteristic curve, the output signal does not simply increase or decrease monotonically with the change in the input signal but takes on a circular shape. Red represents the reverse direction of the hysteresis characteristic curve, and blue represents the positive direction of the hysteresis characteristic curve. In the positive direction, when the input gradually increases, the output gradually increases with increasing input, accompanied by a certain lag or nonlinear relationship. In the reverse direction, as the input decreases gradually, the delay of the output decreases, and the rate of decline is also different from that in the forward direction; the red curve and blue curve together form the hysteresis characteristic curve of the heave compensation platform.

![Figure 4: Hysteresis characteristic curve of the heave compensation platform. The graph shows input displacement x(t) on the horizontal axis and output displacement y(t) on the vertical axis. A blue curve represents the forward direction (increasing input), and a red curve represents the reverse direction (decreasing input). At input x(t_1), the output is y_1(t_1) in the forward direction and y_2(t_1) in the reverse direction. The curves form a closed loop, illustrating the hysteresis effect.](46f43cb4ffd47565e7c0ca306d461435_img.jpg)

Figure 4: Hysteresis characteristic curve of the heave compensation platform. The graph shows input displacement x(t) on the horizontal axis and output displacement y(t) on the vertical axis. A blue curve represents the forward direction (increasing input), and a red curve represents the reverse direction (decreasing input). At input x(t\_1), the output is y\_1(t\_1) in the forward direction and y\_2(t\_1) in the reverse direction. The curves form a closed loop, illustrating the hysteresis effect.

Fig. 4. Hysteresis characteristic curve of the heave compensation platform.

However, the hysteresis delay of the heave compensation platform cannot be obtained only by analyzing the input and output displacement of the compensation platform hysteresis characteristic curve in the time domain. In this work, the Hilbert–Huang transform method is used to analyze the hysteresis delay of the heave compensation platform from the angle of the frequency domain.

### 3.3 Hilbert–Huang transformation

The Hilbert–Huang transform, which is composed of EMD and the Hilbert transform, is a highly adaptive time series analysis method (Hamad et al., 2009). The hysteresis delay of the heave compensation platform is set to  $t_{Dt}$ , which can be determined via the Hilbert–Huang transform.

#### 3.3.1 EMD decomposition

In the heave compensation platform, the fixed settings of some components may change slightly with the influence of environmental variables such as temperature, humidity,

noise and atmospheric pressure, and the performance of the laser sensor may decline after long-term operation, which may lead to random errors in the test results of the heave compensation platform. Furthermore, baseline drift and environmental variables may have impacts on the heave motion data of the compensated platform. To eliminate these effects, the EMD decomposition method is adopted in this paper to process the 4–6 level heave motion data of the compensated platform.

EMD decomposes the compensation platform heave motion data into a series of inherent modal function IMFs  $c_1(t)$  and  $c_2(t) \dots c_n(t)$  and a combination of residual  $r_n(t)$ :

$$z(t) = \sum_{i=1}^{n} c_i(t) + r_n(t); \quad (13)$$

$$f(t) = \sum_{i=1}^{n} c_i(t). \quad (14)$$

The IMFs are components of different frequencies, the sum of components at different frequencies is denoted as  $f(t)$ , and the residuals are the baseline drift and environmental errors of the signal. After compensating for the ship heave motion data and eliminating residual  $r_n(t)$ , the environmental error is reduced, and the signal is more accurate.

#### 3.3.2 Hilbert transformation

The heave motion data of the compensation platform after EMD processing are processed as the sum of the components  $f(t)$  of different frequencies, and the Hilbert transformation is as follows:

$$\hat{f}(t) = \int_{-\infty}^{\infty} \frac{f(\tau)}{\pi(t-\tau)} d\tau = f(t) \frac{1}{\pi t}. \quad (15)$$

Then, the analysis signal  $Z(t)$  of the heave motion data of the compensation platform is extracted from the Hilbert transform, and the instantaneous amplitude  $A(t)$ , instantaneous phase diameter  $\Phi(t)$  and instantaneous frequency  $F(t)$  are obtained:

$$Z(t) = f(t) + j\hat{f}(t) = A(t)e^{-j\varphi(t)}; \quad (16)$$

$$A(t) = \sqrt{f^2(t) + \hat{f}^2(t)}; \quad (17)$$

$$\phi(t) = \arctan \left[ \frac{\hat{f}(t)}{f(t)} \right]; \quad (18)$$

$$F(t) = \frac{1}{2\pi} \frac{d\phi(t)}{dt}. \quad (19)$$

The Hilbert spectrum is the angular frequency–time distribution of the analyzed signal  $Z(t)$ , namely:

$$H(\omega, t) = A(t)e^{-j\int F(t)dt}. \quad (20)$$

The Hilbert spectra  $H_0(\omega, t)$  and  $H(\omega, t)$  of the heave motion data of the ship before compensation and the heave motion data of the compensation platform are compared, and the corresponding angular frequent-time distribution curve is analyzed. The instantaneous angular frequency turning time of  $H(\omega, t)$  is  $t_{Dt}$  of the heave motion compensation platform.

### 3.4 Calculating mechanism of the optimal control action value

To solve the problem of mismatch between the hysteresis delay  $t_{Dt}$  of the heave motion platform and the sampling time  $T$  of the acquisition system composed of a servo drive, servo motor, encoder, electric cylinder, laser sensor, etc., this paper adopts the linear interpolation method to select the optimal control action value  $Z(t_m)$ ,  $t_m \in (t_k, t_{k+1})$ . The calculation formula is as follows:

$$Z(t_m) = \lambda_k^- Z(t_k) + \lambda_k^+ Z(t_{k+1}); \quad (21)$$

$$\lambda_k^- = \frac{t_{k+1} - t_m}{t_{k+1} - t_k}; \quad (22)$$

$$\lambda_k^+ = \frac{t_m - t_k}{t_{k+1} - t_k}. \quad (23)$$

In Eqs. (21)–(23),  $m=t_{Dt}/T$ , where  $m \in \mathbb{R}$  is the actual multiple relation between the hysteresis delay of the platform and the sampling interval,  $t_{Dt}$  is the hysteresis delay of the heave compensation platform,  $T$  is the sampling interval, and  $k=\text{INT}(m)=\text{INT}(t_{Dt}/T)$  is the integer value of  $m$ , which is adjusted downward. The function  $\text{INT}()$  is the nearest integer value obtained by rounding down the data. After the optimal control action value  $Z(t_m)$  is determined, it is input to the heave motion compensation platform for further compensation control tests in level 4–6 sea states.

## 4 Numerical simulations

### 4.1 Data description

#### 4.1.1 Introduction to the P–M spectrum

The P–M spectrum, proposed by Pearson and Moskitch in 1964, is a single-direction propagation long-peak spectrum for the open ocean, which is generated on the basis of large amounts of data measured at certain locations in the North Atlantic Ocean. The P–M spectrum is an empirical data spectrum with sufficient data support, a reasonable analysis method, is easy to use, and has been applied in many fields; it is defined as:

$$S(\omega) = 0.0081 \frac{g^2}{\omega^5} \exp \left[ -0.032 \left( \frac{g}{\omega^2 H_s} \right)^2 \right], \quad (24)$$

where  $S(\omega)$  denotes the wave energy ( $\text{m}^2\text{s}$ );  $\omega$  is the wave circular frequency ( $\text{rad/s}$ );  $g$  is the gravitational acceleration ( $\text{m/s}^2$ ); and  $H_s$  represents the meaningful wave height (m) of an ocean wave.

#### 4.1.2 Data source of ship heave motion

To obtain a practical theoretical calculation method for engineering, it is usually adopted to slice the ship's hull at each section and approximate the real terrain flow around the hull with binary flow. Fig. 5 shows a schematic diagram of the hull based on nonlinear slice theory, and Table 1 lists the engineering ship and hydrodynamic parameters based on nonlinear slice theory.

![Figure 5: Engineering ship model based on nonlinear slice theory. The diagram shows a top-down view of a ship's hull with a coordinate system (x, y, z) and a scale bar at the bottom. The scale bar is labeled with values: 0.39, 20.00, 40.00, 60.00, 80.00 (m).](a612b25163221507295cc3d2fb679c10_img.jpg)

Figure 5: Engineering ship model based on nonlinear slice theory. The diagram shows a top-down view of a ship's hull with a coordinate system (x, y, z) and a scale bar at the bottom. The scale bar is labeled with values: 0.39, 20.00, 40.00, 60.00, 80.00 (m).

Fig. 5. Engineering ship model based on nonlinear slice theory.

Table 1. Main hydrodynamic parameters of the engineering ship

| Parameter                                     | Value     |
|-----------------------------------------------|-----------|
| Length (m)                                    | 109       |
| Width (m)                                     | 24        |
| Depth (m)                                     | 6.5       |
| Quality (t)                                   | 7292.9555 |
| Draft (m)                                     | 5.7       |
| Waterline area ( $\text{m}^2$ )               | 1407.2635 |
| Fully loaded drainage volume ( $\text{m}^3$ ) | 7115.0786 |
| Traveling speed (m/s)                         | 0         |

In this paper, the sea level is defined as the base level. In accordance with the basic principles of the slice method, ship motion data are generated via the hydrodynamics AQWA simulation software. The wave height and period of the P–M spectrum parameters are input into the software: the input wave height of the level 4 sea state is 2.01 m, and the period is 5.1 s. The input wave height of the level 5 sea state is 3.32 m, and the period is 6.6 s. The level 6 sea state input wave height is 5.15 m, and the period is 8.2 s. Finally, 20000 data points of the level 4–6 sea state heave motion based on the time interval of 0.01 s in the P–M spectrum are collected.

#### 4.1.3 Data analysis of the ship heave motion

Because operations at sea, such as installing a suspended fan, typically cease during the at-ry state, the wave direction angle is  $180^\circ$ , and the ship speed is 0. In practical scenarios, the wave direction angle changes due to natural laws and ship maneuvers. The  $90^\circ$  wave direction angle represents the most challenging state for the six degrees of freedom ship's attitude movement. The hydrodynamic analysis revealed that lateral waves have the most significant influence on and damage ships. Therefore, the data collected in this simulation are the heave motion data of ships with wave direction angles of  $90^\circ$  and  $180^\circ$  of the level 4–6 sea states.

Fig. 6 shows the analysis diagrams of the ship heave motion of the level 4–6 sea state data at a  $90^\circ$  wave direction angle. Fig. 6a and Fig. 6b depict the line and box diagrams of the ship heave motion of the level 4–6 sea state data, respectively. Through the analysis of the line chart of sea state changes at all levels, it can be seen that the higher the sea state, the larger the average wave height. It also shows the range of data variations: the box diagram for the sea state 4 is short, indicating a small range of data distributions, whereas the box diagram for the sea states 5–6 is long, indicating a relatively discrete data distribution with

![Figure 6: Analysis diagrams of the ship heave motion of the level 4–6 sea state data at the 90° wave direction angle. (a) Line diagram showing wave height (m) vs. number of data (x 10^4) for Level 4 (green), Level 5 (purple), and Level 6 (blue) sea states. (b) Box diagram showing wave height (m) vs. sea state level (Level 4, Level 5, Level 6) for the same three sea states.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 6: Analysis diagrams of the ship heave motion of the level 4–6 sea state data at the 90° wave direction angle. (a) Line diagram showing wave height (m) vs. number of data (x 10^4) for Level 4 (green), Level 5 (purple), and Level 6 (blue) sea states. (b) Box diagram showing wave height (m) vs. sea state level (Level 4, Level 5, Level 6) for the same three sea states.

**Fig. 6.** Analysis diagrams of the ship heave motion of the level 4–6 sea state data at the 90° wave direction angle.

large differences between data points. Therefore, the box diagram helps visually identify outliers in the ship heave motion time series for the sea states 5 and 6, making predictions more challenging. From Fig. 6b, because the upper and lower dashed lines of the level 5–6 data are relatively long, the variance and standard deviation of the overall data are also relatively large. The red line in each color block of the box diagram indicates the value of the data median, and the red line in the level 4–6 sea states is near the 0 value, indicating that the data are not skewed much. Although Fig. 6 can show the trend and distribution skew of the data through analysis; it cannot provide an accurate measurement of the data, and further analysis is needed.

Table 2 shows detailed descriptive statistics (20000 for all the data, 16000 for the training set, and 4000 for the test set) of the 4–6 heave movements at a 90° wave direction angle, the kurtosis index, the skewness index, and the run test probability index. Since the kurtosis of the normal distribution is 3 and the skewness is 0, the kurtosis index of the level 4–6 sea states of the wave direction angle of 90° is close to 3, and the skewness is close to 0, indicating that the data of each group are close to the normal distribution. From the complexity index value, the heave motion data have a relatively low complexity. The MLYE value describes the chaotic characteristics of the heave motion data, which are all positive values in the dataset, indicating that the data are a chaotic time series.  $P$  is an indicator that describes the independence of the data. When  $P$  is larger than 0.05, the data are independent and irrelevant. The analysis of Table 2 shows that  $P$  values are all smaller than 0.05,

indicating that the training set and test set of the sea state at each level are all non-independent data. The data of the 90° wave direction angle are then taken as the training set and test set to verify the accuracy of different models in predicting the non-independent identically distributed data.

Fig. 7 presents the analysis diagrams of the ship heave motion of the level 4–6 sea state data at the 180° wave direction angle. Comparative analysis with the 90° wave direction angle reveals that the heave motion of the ship with the 180° wave direction angle exhibits smoother changes, with less pronounced fluctuations and the absence of abnormal values.

In Fig. 8, the distribution histogram shows the ship heave motion data corresponding to the training set and test set for the level 4–6 sea states at different wave direction angles. For the histogram, normal, logistic, and extreme distributions were selected for data fitting simulation. Table 3 lists the three distribution fitting parameters for the heave motion data of the level 4–6 sea states at different wave direction angles for both the training set and test set. Considering the variability in the sea state, it is crucial for the model to demonstrate good generalizability. Therefore, two sets of different distribution data are selected for simulation in this paper: the 90° wave direction angle as the training set and the 180° wave direction angle as the test set. As evident from Fig. 8 and Table 3, under the level 4–6 sea state, the data center value for the 90° wave direction angle is 0, indicating a peak distribution. The average population means for the training sets of the three distributions are 0.0951, 0.1431, and 0.2136, with average population variances of

**Table 2** Descriptive statistics of the level 4–6 sea states with the wave direction angles of 90°

| Sea state | Data     | Numbers | Kurtosis | Skewness | MLYE   | Complexity | $P$    |
|-----------|----------|---------|----------|----------|--------|------------|--------|
| Level 4   | All data | 20000   | 3.0289   | 0.0014   | 0.0291 | 0.1845     | 0.0356 |
|           | Training | 16000   | 2.9898   | 0.0016   | 0.0291 | 0.1538     | 0.0349 |
|           | Testing  | 4000    | 3.1941   | -0.0028  | 0.0208 | 0.1538     | 0.0294 |
| Level 5   | All data | 20000   | 2.8569   | -0.0033  | 0.0143 | 0.1691     | 0.0319 |
|           | Training | 16000   | 2.9674   | 0.0011   | 0.0155 | 0.1538     | 0.0284 |
|           | Testing  | 4000    | 2.8534   | -0.0211  | 0.0280 | 0.1384     | 0.0267 |
| Level 6   | All data | 20000   | 3.1238   | 0.0681   | 0.0156 | 0.1538     | 0.0342 |
|           | Training | 16000   | 2.8561   | 0.0407   | 0.0172 | 0.1538     | 0.0381 |
|           | Testing  | 4000    | 3.0332   | 0.0218   | 0.0129 | 0.1231     | 0.0266 |

![Figure 7: Analysis diagrams of the ship heave motion of the level 4–6 sea state data at the 180° wave direction angle. (a) Line diagram showing Wave height (m) vs. Number of data (x10^4) for Level 4 (green), Level 5 (purple), and Level 6 (blue) sea states. (b) Box diagram showing Wave height (m) vs. Sea state level (Level 4, Level 5, Level 6).](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 7: Analysis diagrams of the ship heave motion of the level 4–6 sea state data at the 180° wave direction angle. (a) Line diagram showing Wave height (m) vs. Number of data (x10^4) for Level 4 (green), Level 5 (purple), and Level 6 (blue) sea states. (b) Box diagram showing Wave height (m) vs. Sea state level (Level 4, Level 5, Level 6).

Fig. 7. Analysis diagrams of the ship heave motion of the level 4–6 sea state data at the 180° wave direction angle.

![Figure 8: Distribution histogram of the heave motion data in the training set and test set at different wave direction angles of the level 4–6 sea states. The figure consists of six subplots arranged in a 2x3 grid. The top row shows the 'Training set' (a) and the bottom row shows the 'Testing set' (b). The columns represent 'Level 4', 'Level 5', and 'Level 6' sea states. Each subplot shows 'Density' vs. 'Wave height (m)' and compares 'Data' (blue bars), 'Normal' (red curve), 'Logistic' (green curve), and 'Extreme' (purple curve) distributions.](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 8: Distribution histogram of the heave motion data in the training set and test set at different wave direction angles of the level 4–6 sea states. The figure consists of six subplots arranged in a 2x3 grid. The top row shows the 'Training set' (a) and the bottom row shows the 'Testing set' (b). The columns represent 'Level 4', 'Level 5', and 'Level 6' sea states. Each subplot shows 'Density' vs. 'Wave height (m)' and compares 'Data' (blue bars), 'Normal' (red curve), 'Logistic' (green curve), and 'Extreme' (purple curve) distributions.

Fig. 8. Distribution histogram of the heave motion data in the training set and test set at different wave direction angles of the level 4–6 sea states.

0.4674, 0.6934, and 0.9926, respectively. On the other hand, the 180° wave direction angle has no absolute center, with a flat distribution. The average population means for the test set of the three distributions are 0.0214, 0.0612, and 0.1772, with average population variances of 0.1032, 0.2921, and 0.6549, respectively, indicating differences in distributions from the means and variances of the three distributions. Moreover, the wave direction angle data for 90° are consistently larger than those for 180°. The model is subsequently trained on the 90° data as the training set and tested on the 180° data to evaluate the generalizability of the different prediction methods.

### 4.2 Comparison of prediction results

#### 4.2.1 Predictive comparison of non-independent identically distributed datasets

Gauss-DeepAR model predictions can produce a probability distribution, and an important feature of this distribution

is the confidence interval (CI), which provides a quantitative measure of the uncertainty of the prediction. The CI is a range of predictions that contains high probability truth values. Fig. 9 shows the 90%CI prediction diagram of the level 4–6 sea states at the 90° wave direction angle. The CI is represented by the red shaded area, the width of the shadow represents the range of prediction uncertainty, and the blue line represents the raw data of the test set. Fig. 9 shows that the red shaded area is narrow and that the model has an excellent degree of calibration. Moreover, the raw data of the test set are all in the red shaded region of the 90%CI of the prediction, indicating that the Gauss-DeepAR model in this paper has an outstanding ability to capture the uncertainty of the prediction.

The prediction value of the Gauss-DeepAR model used in this paper was selected as the median of 90%CI prediction, and the comparison model was selected among the studentT-DeepAR model, other neural network models SVM

**Table 3** Three distribution fitting parameters of the heave motion in the training set and test set at different wave direction angles of the level 4–6 sea states

| Sea state | Data     | Distribution | Overall mean | Overall variance |
|-----------|----------|--------------|--------------|------------------|
| Level 4   | Training | Normal       | 0.0035       | 0.5515           |
|           |          | Logistic     | 0.0025       | 0.3229           |
|           |          | Extreme      | 0.2792       | 0.5279           |
|           | Testing  | Normal       | 0.0009       | 0.1227           |
|           |          | Logistic     | 0.0013       | 0.0730           |
|           |          | Extreme      | 0.0619       | 0.1138           |
| Level 5   | Training | Normal       | 0.0074       | 0.8137           |
|           |          | Logistic     | 0.0078       | 0.4768           |
|           |          | Extreme      | 0.4142       | 0.7897           |
|           | Testing  | Normal       | 0.0047       | 0.3401           |
|           |          | Logistic     | 0.0058       | 0.1904           |
|           |          | Extreme      | 0.1752       | 0.3457           |
| Level 6   | Training | Normal       | 0.0190       | 1.1549           |
|           |          | Logistic     | 0.0259       | 0.6593           |
|           |          | Extreme      | 0.5960       | 1.1637           |
|           | Testing  | Normal       | 0.0483       | 0.7674           |
|           |          | Logistic     | 0.0499       | 0.4419           |
|           |          | Extreme      | 0.4334       | 0.7553           |

![Figure 9: Three line charts showing 90% CI prediction of heave motion for Level 4, Level 5, and Level 6 sea states. Each chart plots Height (m) on the y-axis (ranging from -1 to 1 for Level 4, -2 to 2 for Level 5, and -2 to 2 for Level 6) against Time (s) on the x-axis (ranging from 0 to 40). The charts show Raw data (blue line) and the 90% confidence band (red shaded area). The prediction accuracy decreases as the sea state level increases.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 9: Three line charts showing 90% CI prediction of heave motion for Level 4, Level 5, and Level 6 sea states. Each chart plots Height (m) on the y-axis (ranging from -1 to 1 for Level 4, -2 to 2 for Level 5, and -2 to 2 for Level 6) against Time (s) on the x-axis (ranging from 0 to 40). The charts show Raw data (blue line) and the 90% confidence band (red shaded area). The prediction accuracy decreases as the sea state level increases.

**Fig. 9.** 90% CI prediction of the level 4–6 sea states at the 90° wave direction angle.

and LSTM and the statistical model ARIMA. The error indices of the prediction results were selected within the root mean square error (RMSE), mean absolute error (MAE) and mean absolute percentage error (MAPE). After the zero upward traveling wave period  $T_z$  of each set of data was calculated, the sizes of the input sliding windows for the heave motion of the level 4–6 sea states with the 90° wave direction angle were 37, 58 and 62, respectively. The error indices of each group of simulations and the prediction comparison line charts of each model were recorded, and the performance of the ship heave motion prediction methods under different sea states was measured according to the RMSE, MAE, MAPE and line charts. The model with close tracking to the original data and small RMSE, MAE and MAPE values was ideally selected.

Fig. 10 shows the comparison line diagram of each model test set for level 4–6 sea states when the wave direction angles of the training set and test set data are both 90°. The average error was obtained via several controlled simulations. According to the analysis of Fig. 10a, at the level 4 sea state, the ARIMA, studentT-DeepAR, SVM and LSTM models have poor prediction effects at the peaks and troughs of the test set. According to the analysis of Fig. 10b and 10c, the predicted values of the ARIMA and studentT-DeepAR models have a larger amplitude and lag compared with the raw data of the test set at the level 5–6 sea states, and the predicted values of the SVM and LSTM cannot track the raw data of the test set well at the peaks and troughs. The Gauss-DeepAR model has the best prediction effect for the level 4–6 sea states. Table 4 lists the error indicators for each model of the level 4–6 sea states, with the minimum values shown in bold. The analysis reveals that the errors of the ARIMA and student T-DeepAR model are very large. Compared with the SVM and LSTM models, the Gauss-DeepAR model has the smallest RMSE at the level 4 sea state, with a value of 0.4166, and the corresponding MAE and MAPE are also optimal. When the sea state level increases, the error index of the same model gradually increases. The RMSE, MAE and MAPE of the level 5 sea state are larger than those of the level 4 sea state, but they are the smallest among all the models of the same level of sea state, with values of 1.0036, 0.7400 and 0.6873, respectively. In the context of the level 6 sea state, the Gauss-DeepAR model shows even greater performance, achieving a substantial 61.02% reduction in the RMSE compared with that of the SVM and a 59.60% reduction compared with that of the LSTM. Furthermore, the MAE decreased by 61.78% and 60.33%, whereas the MAPE decreased by 66.79% and 66.73%, respectively. The Gauss-DeepAR model excelled in predicting outcomes within a non-independent identically distributed dataset, confirming its superior predictive capabilities.

#### 4.2.2 Predictive comparison of non-independent and non-uniformly distributed data sets

As the conventional lifting operation of a ship involves complete cessation at zero speed, the ship stabilizes in the aty state with a wave direction angle of 180°. Retraining the model at these states is time-consuming, impacting both the prediction accuracy and compensation effectiveness. Thus, achieving high-precision offshore operations becomes unfeasible. Hence, a well-trained model with the 90° wave direction angle is desirable. Direct prediction of the ship heave motion data at the 180° wave direction angle. Moreover, since the ship heave motion is variable, there is a large difference between the 90° wave direction angle and 180° wave direction angle data of the ship heave motion, the generalization performance of the model can be verified by using the 90° wave direction angle data in the training set



![Figure 10: Line charts comparing the test sets of five models (Raw data, Gauss-DeepAR, SVM, LSTM, ARIMA, StudentT-DeepAR) for Level 4, Level 5, and Level 6 sea states. Each chart plots Height (m) against Times (s) from 0 to 40. Insets show zoomed-in views of specific time intervals. The Gauss-DeepAR model consistently shows the closest fit to the raw data across all sea states.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 10: Line charts comparing the test sets of five models (Raw data, Gauss-DeepAR, SVM, LSTM, ARIMA, StudentT-DeepAR) for Level 4, Level 5, and Level 6 sea states. Each chart plots Height (m) against Times (s) from 0 to 40. Insets show zoomed-in views of specific time intervals. The Gauss-DeepAR model consistently shows the closest fit to the raw data across all sea states.

Fig. 10. Line chart of the comparison among the test sets of each model at the 90° wave direction angle.

**Table 4** Prediction error indices of each model test set at a 90° wave direction angle

| Sea state | Model           | Error indicator |               |               |
|-----------|-----------------|-----------------|---------------|---------------|
|           |                 | RMSE (mm)       | MAE (mm)      | MAPE (%)      |
| Level 4   | SVM             | 1.0305          | 0.8273        | 0.5776        |
|           | LSTM            | 0.5990          | 0.6570        | 0.4622        |
|           | ARIMA           | 1.5033          | 1.2442        | 0.9763        |
|           | studentT-DeepAR | 2.0003          | 1.6733        | 1.3471        |
|           | Gauss-DeepAR    | <b>0.4166</b>   | <b>0.3435</b> | <b>0.2304</b> |
| Level 5   | SVM             | 1.9961          | 1.5055        | 0.9930        |
|           | LSTM            | 1.3031          | 1.1729        | 0.8822        |
|           | ARIMA           | 4.1362          | 3.3075        | 1.8446        |
|           | studentT-DeepAR | 2.6052          | 2.3006        | 2.7005        |
|           | Gauss-DeepAR    | <b>1.0036</b>   | <b>0.7400</b> | <b>0.6873</b> |
| Level 6   | SVM             | 9.7149          | 7.8047        | 7.2969        |
|           | LSTM            | 9.3725          | 7.5203        | 7.2843        |
|           | ARIMA           | 13.7023         | 11.5253       | 8.3477        |
|           | studentT-DeepAR | 20.4066         | 17.5118       | 8.6635        |
|           | Gauss-DeepAR    | <b>3.7864</b>   | <b>2.9826</b> | <b>2.4231</b> |

and 180° wave direction angle data in the test set.

Fig. 11 shows the probability prediction graph of the Gauss-DeepAR model predicted at the 90° wave direction angle for the training set data and 180° wave direction angle data for the test set. A 90%CI is used for probability prediction. The blue line represents the original data of the test set, the red shaded area represents the CI, and the shadow width represents the range of prediction uncertainty. As shown in

Fig. 11, the widths of the shadows of the level 4–6 sea states are relatively narrow, and the original data are all within the red shadow region of the 90%CI prediction, indicating that the Gauss-DeepAR model has a good calibration degree and an excellent estimate of the uncertainty of the data.

Fig. 12 shows the line chart of the comparison of the test sets of each model for the level 4–6 sea states when the training set data have a 90° wave direction angle and the test set data have a 180° wave direction angle, and the error is the average error of multiple simulations. According to the

![Figure 11: Three line charts showing the 90%CI prediction of the level 4, 5, and 6 sea states at the 180° wave direction angle. Each chart plots Height (m) against Times (s) from 0 to 40. The blue line is the raw data, and the red shaded area is the 90% confidence bond. The Gauss-DeepAR model's prediction is shown to be very close to the raw data within the confidence interval.](2f73c3f1961c12d27d0d18fe7befbf0c_img.jpg)

Figure 11: Three line charts showing the 90%CI prediction of the level 4, 5, and 6 sea states at the 180° wave direction angle. Each chart plots Height (m) against Times (s) from 0 to 40. The blue line is the raw data, and the red shaded area is the 90% confidence bond. The Gauss-DeepAR model's prediction is shown to be very close to the raw data within the confidence interval.

Fig. 11. 90%CI prediction of the level 4–6 sea states at the 180° wave direction angle.

![Figure 12: Line charts comparing the performance of five models (Raw data, Gauss-DeepAR, SVM, LSTM, ARIMA, StudentT-DeepAR) across three sea states (Level 4, Level 5, Level 6). The charts show Height (m) versus Time (s). Gauss-DeepAR consistently shows the best fit to the raw data across all sea states.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 12 consists of three subplots labeled (a), (b), and (c), each showing a line chart of Height (m) versus Time (s) for different sea states. Each chart compares the performance of six models: Raw data, Gauss-DeepAR, SVM, LSTM, ARIMA, and StudentT-DeepAR. The x-axis for all charts ranges from 0 to 40 seconds. The y-axis ranges from -0.20 to 0.15 m for (a), -0.4 to 0.8 m for (b), and -2 to 3 m for (c). Each chart includes an inset showing a magnified view of the first 10 seconds. In all cases, the Gauss-DeepAR model (blue line) closely follows the raw data (black line), while the other models (SVM, LSTM, ARIMA, StudentT-DeepAR) show varying degrees of deviation, lag, or overreach.

Figure 12: Line charts comparing the performance of five models (Raw data, Gauss-DeepAR, SVM, LSTM, ARIMA, StudentT-DeepAR) across three sea states (Level 4, Level 5, Level 6). The charts show Height (m) versus Time (s). Gauss-DeepAR consistently shows the best fit to the raw data across all sea states.

Fig. 12. Line chart of the comparison among the test sets of the models at the 180° wave direction angle.

analysis of Fig. 12a, at the level 4 sea state, the predicted values of the ARIMA model and studentT-DeepAR model have a certain overreach, the predicted value of the SVM model has a certain lag, and the predicted value of the LSTM model has a poor prediction result at the wave peaks and troughs. As shown in Figs. 12b and 12c, at the level 5–6 sea states, the predicted values of the ARIMA model and the studentT-DeepAR model differ greatly from the original data, and the predicted values of the SVM and LSTM models cannot be tracked well at the peaks and troughs of the original data. The Gauss-DeepAR model has the best prediction results for level 4–6 sea states. Table 5 lists the error indicators for each model of the level 4–6 sea states, with the minimum values shown in bold. The analysis reveals that the error index of the same model increases with the increasing sea state grade. The prediction error of the Gauss-DeepAR model is the smallest under the same level of sea state. Compared with the SVM and LSTM models, the Gauss DeepAR model has the smallest RMSE at the level 4 sea state, with a value of 0.8815, and the corresponding MAE and MAPE are also optimal. The RMSE, MAE, and MAPE in the level 5 sea state are the smallest among all the models under the same level of sea state, with values of 1.9843, 1.2654, and 0.8475, respectively. At the level 6 sea state, the Gauss-DeepAR model continues to show remarkable performance, with a considerable decrease in the RMSE of 53.04% compared with that of the SVM and 52.68% compared with that of the LSTM. Additionally, the MAE decreases by 59.34% and 52.58%, whereas the MAPE

**Table 5** Prediction error indices of each model test set at the 180° wave direction angle

| Sea state | Model           | Error indicator |               |               |
|-----------|-----------------|-----------------|---------------|---------------|
|           |                 | RMSE (mm)       | MAE (mm)      | MAPE (%)      |
| Level 4   | SVM             | 1.8739          | 0.8529        | 0.8744        |
|           | LSTM            | 0.9942          | 0.8571        | 0.7622        |
|           | ARIMA           | 1.8733          | 1.5920        | 1.7765        |
|           | studentT-DeepAR | 2.0533          | 1.6993        | 1.3291        |
|           | Gauss-DeepAR    | <b>0.8815</b>   | <b>0.7143</b> | <b>0.6314</b> |
| Level 5   | SVM             | 3.9161          | 2.9755        | 1.9930        |
|           | LSTM            | 2.3537          | 2.1753        | 1.9923        |
|           | ARIMA           | 6.4762          | 6.3745        | 2.8923        |
|           | studentT-DeepAR | 9.6552          | 8.3636        | 5.7083        |
|           | Gauss-DeepAR    | <b>1.9843</b>   | <b>1.2654</b> | <b>0.8475</b> |
| Level 6   | SVM             | 8.4209          | 8.8871        | 4.2962        |
|           | LSTM            | 8.3577          | 7.6205        | 5.2398        |
|           | ARIMA           | 12.8726         | 11.2348       | 8.7157        |
|           | studentT-DeepAR | 19.6598         | 18.6971       | 9.3415        |
|           | Gauss-DeepAR    | <b>3.9546</b>   | <b>3.6135</b> | <b>1.9671</b> |

decreases by 54.21% and 62.46%, respectively. The outstanding generalization performance of the Gauss-DeepAR model is evident from these results.

## 4.3 Compensation test and results

### 4.3.1 Determination of the hysteresis delay and optimal control action value of the heave motion compensation platform

Before the compensation control test of the ship heave

motion, it is necessary to determine the hysteresis delay of the heave motion compensation platform and the optimal control action value. Taking the heave motion data of a ship at the wave direction angle of  $180^\circ$  as an example, the heave motion data of the level 4–6 sea states in 40 s were randomly selected and input into the platform, the heave motion data of the compensation platform were collected without delay, and the EMD transformation and Hilbert spectrum analysis were performed on the heave motion data of the compensation platform. In Fig. 13, the first column displays the original raw data. The second column shows the Hilbert spectrum data with no delay compensation, which are collected after the original ship heave motion is directly input to the compensation platform. In the third column, the Gauss-DeepAR prediction data with delay compensation control are input into the heave motion compensation platform, and the Hilbert spectrum of the compensation data is collected. According to the first and second columns of Fig. 13, the hysteresis delay  $t_{Dt}$  of the heave motion compensation platform in our laboratory is 0.3 s.

Given that the system sampling time of the heave compensation platform is  $T=0.01$  s, the action value  $Z(t_m)$  selected by the optimal control is calculated according to Eqs. (20)–(22).  $Z(t_m)$  is then input into the heave motion compensation platform for compensation control. The Hilbert spectrum with delay compensation control in the third column of Fig. 13 is compared with the first and second columns. The Hilbert instantaneous frequency spectrum controlled by delay compensation eliminates short-term oscillation and is essentially the same as the Hilbert instantaneous frequency spectrum corresponding to the raw ship

heave motion data, which proves that this method can eliminate the influence of the hysteresis delay of the heave motion compensation platform, and accurate compensation control has been achieved.

### 4.3.2 Comparison of the compensation results

Fig. 14 shows the curves of the original data of the level 4–6 sea states and the compensation data of different models. According to the analysis, the SVM, LSTM, ARIMA and studentT-DeepAR models all have obvious compensation hysteresis at the level 4–6 sea states. The Gauss-DeepAR model with the Hilbert–Huang delay compensation control strategy has an outstanding compensation control tracking effect. On the basis of the analysis of the compensation result error indicators RMSE, MAE, MAPE and compensation efficiency  $\eta$  in Table 6, at the level 4–6 sea states of the same model, the higher the sea state level, the larger the error index and the lower the compensation efficiency. Under the condition of the same sea state level, the RMSE, MAE and MAPE values of the compensation results of the Gauss-DeepAR model using the Hilbert–Huang delay compensation control strategy are all smaller than those of the LSTM model, and the compensation efficiency is higher than that of the LSTM model and is larger than 90%. In accordance with the Hilbert–Huang time-delay compensation control strategy, the ship heave motion predicted by the Gauss-DeepAR model is input into the heave motion compensation platform to achieve accurate compensation control.

# 5 Conclusions

To accurately predict and compensate for the ship heave

![Figure 13: Delay compensation comparison of the Hilbert spectrum. The figure consists of a 3x3 grid of plots. The rows represent sea states: Level 4 (top), Level 5 (middle), and Level 6 (bottom). The columns represent different stages of processing: 'Raw data' (left), 'No delay compensation' (middle), and 'After delay compensation' (right). Each plot shows Frequency (Hz) on the y-axis (scaled by 10^-3) versus Time (s) on the x-axis (0 to 4). The 'Raw data' column shows the original heave motion. The 'No delay compensation' column shows the Hilbert spectrum with a significant delay and oscillation. The 'After delay compensation' column shows a much smoother spectrum that closely follows the 'Raw data' spectrum, demonstrating the effectiveness of the delay compensation strategy.](9d1abc573e35610946ece87a18cbe862_img.jpg)

Figure 13: Delay compensation comparison of the Hilbert spectrum. The figure consists of a 3x3 grid of plots. The rows represent sea states: Level 4 (top), Level 5 (middle), and Level 6 (bottom). The columns represent different stages of processing: 'Raw data' (left), 'No delay compensation' (middle), and 'After delay compensation' (right). Each plot shows Frequency (Hz) on the y-axis (scaled by 10^-3) versus Time (s) on the x-axis (0 to 4). The 'Raw data' column shows the original heave motion. The 'No delay compensation' column shows the Hilbert spectrum with a significant delay and oscillation. The 'After delay compensation' column shows a much smoother spectrum that closely follows the 'Raw data' spectrum, demonstrating the effectiveness of the delay compensation strategy.

Fig. 13. Delay compensation comparison of the Hilbert spectrum.

![Figure 14: Curves of the raw data and compensation data of different models for level 4–6 sea states. The figure consists of three subplots: (a) Level 4 sea state, (b) Level 5 sea state, and (c) Level 6 sea state. Each subplot shows Height (m) on the y-axis and Times (s) on the x-axis (0 to 40). The legend for each plot includes: Raw data (blue line), Gauss-DeepAR (orange line), SVM (green line), LSTM (purple line), ARIMA (yellow line), and StudentT-DeepAR (red line). Each plot features two zoomed-in insets showing detailed compensation results for specific time intervals.](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 14: Curves of the raw data and compensation data of different models for level 4–6 sea states. The figure consists of three subplots: (a) Level 4 sea state, (b) Level 5 sea state, and (c) Level 6 sea state. Each subplot shows Height (m) on the y-axis and Times (s) on the x-axis (0 to 40). The legend for each plot includes: Raw data (blue line), Gauss-DeepAR (orange line), SVM (green line), LSTM (purple line), ARIMA (yellow line), and StudentT-DeepAR (red line). Each plot features two zoomed-in insets showing detailed compensation results for specific time intervals.

Fig. 14. Curves of the raw data and compensation data of different models for level 4–6 sea states.

Table 6 Compensation result of the error indices

| Sea state | Model            | Error indicator |               |               |              |
|-----------|------------------|-----------------|---------------|---------------|--------------|
|           |                  | RMSE (mm)       | MAE (mm)      | MAPE (%)      | $\eta$ (%)   |
| Level 4   | SVM              | 1.8682          | 1.5461        | 1.1018        | 73.70        |
|           | LSTM             | 1.0489          | 0.8509        | 0.5534        | 80.67        |
|           | ARIMA            | 1.4751          | 1.2595        | 1.4633        | 79.07        |
|           | studentT-DeepAR  | 1.8338          | 1.5165        | 0.6974        | 74.08        |
|           | HHT-Gauss-DeepAR | <b>0.4990</b>   | <b>0.3570</b> | <b>0.2322</b> | <b>96.57</b> |
| Level 5   | SVM              | 3.7852          | 3.3066        | 1.5941        | 72.66        |
|           | LSTM             | 4.5702          | 4.0402        | 2.7591        | 74.10        |
|           | ARIMA            | 5.5201          | 4.4642        | 0.7472        | 72.39        |
|           | studentT-DeepAR  | 5.2277          | 4.7436        | 1.0359        | 70.02        |
|           | HHT-Gauss-DeepAR | <b>0.9893</b>   | <b>0.6570</b> | <b>0.5622</b> | <b>95.13</b> |
| Level 6   | SVM              | 18.283          | 15.398        | 4.8159        | 83.94        |
|           | LSTM             | 21.718          | 16.5761       | 4.8574        | 66.61        |
|           | ARIMA            | 27.988          | 25.143        | 6.7846        | 84.17        |
|           | studentT-DeepAR  | 27.291          | 23.719        | 6.8127        | 76.30        |
|           | HHT-Gauss-DeepAR | <b>3.6003</b>   | <b>2.6733</b> | <b>1.3471</b> | <b>93.92</b> |

motion at the level 4–6 sea states and address the hysteresis problem in the wave compensation system, this paper proposes a ship heave motion prediction and Hilbert–Huang time-delay compensation control strategy based on the Gauss-DeepAR model. The approach involves determining the input sliding window of the DeepAR prediction model as the zero-upward traveling wave period of the ship heave motion sequence. The ship heave motion data, considering

different wave direction angles, are then predicted probabilistically. The Hilbert–Huang transform is subsequently used to determine the hysteresis delay of the heave motion compensation platform. The optimal control action value is then chosen, and a compensation control test is conducted. The simulation results demonstrate that the proposed Gauss-DeepAR model exhibits excellent generalizability and superior prediction accuracy compared with the ARIMA, SVM, and LSTM at the level 4–6 sea states. Then, using the first-stage platform of the heave motion compensation platform to simulate ship motion, the second-stage platform detects the compensation effect of Gauss-DeepAR prediction values and uses the Hilbert–Huang transform to effectively determine the hysteresis delay of the compensation platform. Further analysis indicates that selecting the appropriate prediction value on the basis of the optimal control action value of the compensation platform has an excellent compensation control effect. Furthermore, the compensation accuracy and efficiency of the Hilbert–Huang time-delay compensation control strategy, which is based on Gauss-DeepAR ship heave motion prediction, surpass those of the LSTM model, which achieves a compensation efficiency that exceeds 90%. This indicates its potential applicability in actual compensation systems. Future work will test the effectiveness of the Hilbert–Huang time-delay compensation control strategy on different platforms and apply it in multi-variable situations to provide further decision support for the existing model to solve more ship prediction compensation problems.

# Competing interests

The authors declare no competing interests.

# References

- Dai, Y.T., Cheng, R., Yao, X. and Liu, L.Q., 2019. Hydrodynamic coefficients identification of pitch and heave using multi-objective evolutionary algorithm, *Ocean Engineering*, 171, 33–48.
- De-Jun, Qin, S.Q. and Wu, W., 2016. A hybrid AR-DWT-EMD model for the short-term prediction of nonlinear and non-stationary ship motion, *Chinese Control and Decision Conference (CCDC)*, IEEE, Yinchuan, China, pp. 4042–4047.
- Ding, S.F., Ma, Q., Zhou, L., Han, S. and Dong, W.B., 2023. Multipoint heave motion prediction method for ships based on the PSO-TGCN Model, *China Ocean Engineering*, 37(6), 1022–1031.
- Do, K.D. and Pan, J., 2008. Nonlinear control of an active heave compensation system, *Ocean Engineering*, 35(5-6), 558–571.
- Dong, Y.X., Ma, S.D., Zhang, H.C. and Yang, G.H., 2022. Wind power prediction based on multi-class autoregressive moving average model with logistic function, *Journal of Modern Power Systems and Clean Energy*, 10(5), 1184–1193.
- Dragomiretskiy, K. and Zosso, D., 2014. Variational mode decomposition, *IEEE Transactions on Signal Processing*, 62(3), 531–544.
- Geng, X.Y., Li, Y.B. and Sun, Q., 2023. A novel short-term ship motion prediction algorithm based on EMD and adaptive PSO-LSTM with the sliding window approach, *Journal of Marine Science and Engineering*, 11(3), 466.
- Hamad, K., Shourijeh, M.T., Lee, E. and Faghri, A., 2009. Near-term travel speed prediction utilizing Hilbert–Huang transform, *Computer-Aided Civil and Infrastructure Engineering*, 24(8), 551–576.
- Hu, X., Zhang, B.Y. and Tang, G., 2021. Research on ship motion prediction algorithm based on dual-pass long short-term memory neural network, *IEEE Access*, 9, 28429–28438.
- Huang, J.H., Wang, S.L., Xu, W.H., Shi, W.H. and Fernandez, C., 2021. A novel autoregressive rainflow—integrated moving average modeling method for the accurate state of health prediction of lithium-ion batteries, *Processes*, 9(5), 795.
- Jeon, Y. and Seong, S., 2022. Robust recurrent network model for intermittent time-series forecasting, *International Journal of Forecasting*, 38(4), 1415–1425.
- Liu, R.X., Li, H., Zou, J. and Ong, M.C., 2023a. Reconstruction and prediction of global whipping responses on a large cruise ship based on LSTM neural networks, *Ocean Engineering*, 285, 115393.
- Liu, S.B., Shi, P.A. and Wu, L., 2014. Short-term prediction of ship motion based on EMD-SVM, *Applied Mechanics and Materials*, 571–572, 252–257.
- Liu, X.X., Wang, Q.M., Huang, R., Wang, S.B. and Liu, X.J., 2019. A prediction method for deck-motion based on online least square support vector machine and genetic algorithm, *Journal of Marine Science and Technology*, 24(2), 382–397.
- Liu, X.Y., He, X.D. and Yi, Y.H., 2023b. Prediction of ship motion attitude based on combined model, *Proceedings of the 2023 10th International Conference on Wireless Communication and Sensor Networks*, ACM, Chengdu, China.
- Luzia, R., Rubio, L. and Velasquez, C.E., 2023. Sensitivity analysis for forecasting Brazilian electricity demand using artificial neural networks and hybrid models based on Autoregressive Integrated Moving Average, *Energy*, 274, 127365.
- Murray, B. and Perera, L.P., 2021. An AIS-based deep learning framework for regional ship behavior prediction, *Reliability Engineering & System Safety*, 215, 107819.
- Nie, Z.H., Lu, Z.F., Lai, P., Zhou, J.P. and Yao, F.J., 2022. Short-term prediction of large ship motion based on empirical mode decomposition and autoregressive model, *2022 IEEE 6th Advanced Information Technology, Electronic and Automation Control Conference*, IEEE, Beijing, China, pp. 933–937.
- Nikita, J. and Karan, V., 2021. Performance comparison of denoising methods for fetal phonocardiography using fir filter and empirical mode decomposition (EMD), in: Chatterjee, P. and Panchal, D. (eds.), *Frontiers of Mechanical and Industrial Engineering*, AAP-CRC Press.
- Pan, J., Liu, Y.Q. and Shu, J., 2023. Gradient-based parameter estimation for a nonlinear exponential autoregressive time-series model by using the multi-innovation, *International Journal of Control, Automation and Systems*, 21(1), 140–150.
- Peng, X.Y., Zhang, B. and Zhou, H.G., 2019. An improved particle swarm optimization algorithm applied to long short-term memory neural network for ship motion attitude prediction, *Transactions of the Institute of Measurement and Control*, 41(15), 4462–4471.
- Salinas, D., Flunkert, V., Gasthaus, J. and Januschowski, T., 2020. DeepAR: Probabilistic forecasting with autoregressive recurrent networks, *International Journal of Forecasting*, 36(3), 1181–1191.
- Schaffer, A.L., Dobbins, T.A. and Pearson, S.A., 2021. Interrupted time series analysis using autoregressive integrated moving average (ARIMA) models: A guide for evaluating large-scale health interventions, *BMC Medical Research Methodology*, 21(1), 58.
- Sheikh Khozani, Z., Barzegari Banadkooki, F., Ehteram, M., Najah Ahmed, A. and El-Shafie, A., 2022. Combining autoregressive integrated moving average with Long Short-Term Memory neural network and optimisation algorithms for predicting ground water level, *Journal of Cleaner Production*, 348, 131224.
- Skulstad, R., Li, G.Y., Fossen, T.I., Vik, B. and Zhang, H.X., 2021. A hybrid approach to motion prediction for ship docking—integration of a neural network model into the ship dynamic model, *IEEE Transactions on Instrumentation and Measurement*, 70, 2501311.
- Tang, G., Lei, J.M., Shao, C.T., Hu, X., Cao, W.D. and Men, S.Y., 2021a. Short-term prediction in vessel heave motion based on improved LSTM Model, *IEEE Access*, 9, 58067–58078.
- Tang, G., Lu, P., Hu, X. and Men, S.Y., 2021b. Control system research in wave compensation based on particle swarm optimization, *Scientific Reports*, 11(1), 15316.
- Tu, F.W., Ge, S.S., Choo, Y.S. and Hang, C.C., 2018. Sea state identification based on vessel motion response learning via multi-layer classifiers, *Ocean Engineering*, 147, 318–332.
- Wang, H.L., Wu, F. and Lei, D.G., 2021. Prediction of ship heave motion using regularized BP neural network with cross entropy error function, *International Journal of Computational Intelligence Systems*, 14(1), 192.
- Wei, Y.H., Wang, A.Q. and Han, H., 2019. Ocean wave active compensation analysis of inverse kinematics for hybrid boarding system based on fuzzy algorithm, *Ocean Engineering*, 182, 577–583.
- Wen, S.L., Zhang, C., Lan, H., Xu, Y., Tang, Y. and Huang, Y.Q., 2021. A hybrid ensemble model for interval prediction of solar power output in ship onboard power systems, *IEEE Transactions on Sustainable Energy*, 12(1), 14–24.
- Xin, Y., Gao, J.W., Yang, X.F. and Yang, J., 2023. Maximum likelihood estimation for uncertain autoregressive moving average model with application in financial market, *Journal of Computational and Applied Mathematics*, 417, 114604.
- Zhang, B., Wang, S., Deng, L.W., Jia, M.Q. and Xu, J.Z., 2023. Ship motion attitude prediction model based on IWOA-TCN-Attention,

*Ocean Engineering*, 272, 113911.

Zhang, G.Y., Tan, F. and Wu, Y.X., 2020. Ship motion attitude prediction based on an adaptive dynamic particle swarm optimization algorithm and bidirectional LSTM neural network, *IEEE Access*, 8, 90087–90098.

Zhou, H., Yan, P., Huang, Q., Yuan, Y.F., Pei, J. and Yang, Y., 2023. Hob vibration signal denoising and effective features enhancing using improved complete ensemble empirical mode decomposition with adaptive noise and fuzzy rough sets, *Expert Systems with Applications*, 233, 120989.