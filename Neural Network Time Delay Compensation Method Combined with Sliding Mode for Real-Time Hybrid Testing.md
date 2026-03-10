

# Neural Network Time Delay Compensation Method Combined with Sliding Mode for Real-Time Hybrid Testing

Yuekun Shangguan ![ORCID icon](666e09182d4cd268646ea700ea60dcdf_img.jpg) <sup>\*</sup>,<sup>†</sup>, Huimeng Zhou ![ORCID icon](1ef1ef0bf9af6c6996401964cf280f2d_img.jpg) <sup>\*</sup>, Zhen Wang ![ORCID icon](e9a80c8557f9285916925bd4ac40fff5_img.jpg) <sup>‡</sup>,<sup>§</sup>  
and Hongcan Yao ![ORCID icon](88e2edecff3400e68a80dd08c57d2f9c_img.jpg) <sup>†</sup>,<sup>¶</sup>

<sup>\*</sup>*Earthquake Engineering Research and Test Center  
Guangzhou University  
Guangzhou 510006, P. R. China*

<sup>†</sup>*School of Civil Engineering and Transportation  
Guangzhou University  
Guangzhou 510006, P. R. China*

<sup>‡</sup>*School of Civil Engineering and Architecture  
Wuhan University of Technology  
Wuhan 430070, P. R. China*  
<sup>§</sup>*wang\_zhen@whut.edu.cn*  
<sup>¶</sup>*yao\_hongcan@gzhu.edu.cn*

Received 21 May 2025  
Accepted 4 August 2025  
Published 18 October 2025

In real-time hybrid testing (RTHHT), there is an inevitable time delay in the loading system because of the dynamic characteristics of the loading-specimen system. Time delay can reduce the accuracy or even lead to the instability of the test. Because of the nonlinearity in loading-specimen systems and the uncertainty of the input signals, time delay has significant time-variant characteristics and uncertainty. To guarantee the stability and accuracy of RTHHT, a backpropagation neural network time delay compensation method combined with sliding mode (BPNN-SM) is proposed. The BPNN-SM method uses sliding mode as a feedback controller of the loading system to improve robustness and compensate for part of the time delay. BPNN is used as the inverse compensation to compensate for the residual time delay and further improve robustness. The desired command and displacement responses of the experimental substructure are used as the input and output for training the BPNN inverse model of the loading-specimen system with a sliding mode controller. The BPNN has 4 hidden layers and 50 inputs in the input layer, which is expanded by one input data column to get enough data. BPNN can model highly complex nonlinear dynamic characteristics with a fully connected structure and calculate quickly using the error backpropagation mechanism, which makes the

<sup>§</sup>,<sup>¶</sup>Corresponding authors.

compensation more robust. The time delay compensation tests and RTHT of a single-degree-of-freedom (SDOF) structure based on the mast of SEG Plaza were conducted. The test results show that BPNN-SM has an excellent compensation effect.

**Keywords:** Real-time hybrid testing; time delay compensation; backpropagation neural network; sliding mode; robustness.

## 1. Introduction

In recent years, real-time hybrid testing (RTHT)<sup>1</sup> has become increasingly prevalent in civil engineering, mechanical engineering and so on.<sup>2–5</sup> RTHT takes the strong nonlinear components of structures as experimental substructure tested in large-scale or full-scale, while the remainder part is considered as numerical substructure calculated in computer, these two parts interact with each other in real-time to simulate the dynamic response of the entire structure. RTHT provides an efficient and cost-saving method to investigate the dynamic responses of complex systems with earthquake input. The time delay brings in a significant challenge to the success of RTHT, which arises from the dynamic characteristics of the loading device. The time delay effectively introduces negative damping to the tested structure,<sup>6</sup> which will reduce the accuracy and even lead to the instability of the test. To ensure the stability and accuracy of RTHT, time delay compensation was investigated by many scholars.

The time delay compensation methods based on polynomial extrapolation have been proposed by many scholars. Horiuchi *et al.*<sup>6</sup> assumed that the time delay is fixed and proposed a polynomial extrapolation compensation method. Nakashima and Masaoka<sup>7</sup> applied the third-order polynomial extrapolation method in real-time online testing of single-degree-of-freedom (SDOF) structures and multi-layer base-isolated building models. In their tests, the time delays were estimated through preliminary dynamic loading tests and updated every half cycle during the tests. Chae *et al.*<sup>8</sup> proposed an adaptive time series (ATS) compensation technique, which is adaptive second-order polynomial extrapolation. Alejandro and Marianonieta developed a conditional adaptive time series (CATS) compensator and numerically tested the compensator in the RTHT benchmark problem.<sup>9</sup> At the same time, many robust control methods have been employed by scholars, particularly sliding mode control (SMC)<sup>10–12</sup> or  $H_\infty$  control,<sup>13</sup> compensating time delay to enhance control precision and robustness. Wu *et al.*<sup>14</sup> proposed SMC as an outer controller for equivalent force control in the real-time substructure testing of nonlinear samples. Rajabi *et al.*<sup>15</sup> combined SMC with the extended Kalman filter (EKF) and unscented Kalman filter (UKF) for shaking table control. The EKF/UKF and SMC combination achieved superior tracking control of displacement, velocity and acceleration trajectories. Li *et al.*<sup>16</sup> proposed a robust sliding mode controller as a control strategy for the transmission system in RTHT. The author utilized a benchmark RTHT problem to demonstrate and validate the applicability of the SMC to such

problems, showing that the SMC strategy significantly enhanced the performance and robustness of RTHT testing.

Another idea of time delay compensation methods is the inverse mode compensator.<sup>17</sup> Carrion and Spencer<sup>17</sup> proposed a model-based response prediction method, in which the model is the transfer function of actuator. Philips and Spencer<sup>18</sup> proposed a model-based feedforward-feedback actuator control to compensate for the time delay in an RTHT of MR dampers. Fermandois<sup>19</sup> developed a robust model-based feedforward-feedback compensator and investigated its accuracy and stability through a benchmark RTHT problem. Chen *et al.*<sup>20</sup> proposed an inverse model compensation approach based on the discrete transfer function of the actuator. Chen *et al.*<sup>21</sup> introduced a dual delay compensation strategy combining a phase lead compensator and a restoring force compensation, in which the phase lead compensator is the inverse of a first-order model of the actuator, in essence. Ou *et al.*<sup>22</sup> integrated an additional inverse compensation module into the robust integrated actuator control algorithm. It assumes that system time delay is constant across the entire frequency range and models the  $H_\infty$ -controlled system as a first-order system, utilizing open-loop inverse compensation. Xu *et al.*<sup>23</sup> analyzed the discrete transfer function for inverse compensation from a frequency domain perspective. The author indicated that when the inverse compensation parameter  $\alpha$  is appropriately chosen, the inverse compensation method can effectively mitigate time delays. Due to the inverse model of the actuator, the amplitudes in the high-frequency range are consistently subject to excessive amplification. The inverse compensation may become unstable due to the unmodeled dynamics or noise. A neural network may provide the optimum inverse model to improve stability and accuracy.

Neural networks have been widely employed to construct surrogate models of complex physical or numerical simulations,<sup>24–38</sup> owing to their powerful nonlinear fitting capabilities and self-learning characteristics. Cheon *et al.*<sup>24</sup> proposed a deep learning controller that utilizes deep belief networks to learn the input-output relationships of PID controllers, demonstrating its performance and effectiveness. Guo *et al.*<sup>30</sup> proposed a neural network-based RTHT method, where a long short-term memory (LSTM) model was used to replace complex train-bridge structure models. Zhou *et al.*<sup>31</sup> developed an LSTM neural network to perform real-time calculations of complex numerical substructures, as well as to handle the data exchange between intricate physical and numerical boundaries, in the RTHT for deepwater bridges. Chen *et al.*<sup>32</sup> proposed a deep learning-based RTHT method for nonlinear numerical substructures. A large dataset was generated through extensive nonlinear time history analysis by OpenSees model, and a recursive LSTM neural network model was trained to predict nonlinear structural responses. Tang *et al.*<sup>33</sup> proposed an offline shaking table hybrid test based on backpropagation neural networks (BPNN), aiming to eliminate the real-time data interaction between physical tests and numerical solutions in RTHT. Subaihawi *et al.*<sup>37</sup> proposed a neural network model that

combined an LSTM layer block with parallel rectified linear units, which constructs a soil-foundation system for RTHT considering soil-foundation-structure interaction effects. At the same time, neural networks are widely used to compensate for time delays and enhance robustness.<sup>39–42</sup> Li *et al.*<sup>39</sup> developed a feedforward compensation control method based on deep deterministic policy gradient algorithms for complex systems, such as underwater shaking table control, and conducted dynamic tests confirming the method's superior performance. Lai *et al.*<sup>40</sup> proposed an adaptive compensation method that combined a CATS compensator with an LSTM network in RTHT. The LSTM network is used to predict the actuator response for parameter estimation and to compute the prediction error. Nino *et al.*<sup>41</sup> used deep reinforcement learning as an alternative approach to designing tracking controllers in RTHT. The application of neural networks in surrogate modeling and compensating for time delays in hybrid testing has demonstrated significant advantages. The feedback neural network models, such as LSTM in hybrid testing, have been applied by many scholars. Nevertheless, these feedback neural networks often lead to high costs for training and computation, exhibit sensitivity to noise or outliers in input data, and produce unstable prediction results, which limit their applicability. The BPNN employs a fully connected structure, enabling effective modeling of system characteristics through its multi-layer nonlinear mapping capabilities. BPNN offers faster training speeds and better stability, making it more suitable as an inverse model for loading system dynamics in RTHT.

This study proposes a BPNN time delay compensation method combined with sliding mode (BPNN-SM) for time delay compensation. The method employs BPNN as an inverse compensator to address the time delays, combining with SMC for the loading system to improve the robustness of the compensation system. The remainder of this study is organized as follows. Section 2 outlines the fundamental principles and construction of the BPNN-SM method. Section 3 describes the RTHT platform. Section 4 discusses RTHT results to validate the feasibility and robustness of the BPNN-SM method. Finally, Sec. 5 describes the conclusions.

## 2. BPNN-SM Method

A detailed description of the BPNN-SM method is provided in this section, and the principle is illustrated in Fig. 1. The BPNN-SM method utilizes sliding mode to design the outer loop controller for hydraulic servo actuators and specimens to compensate for time delays and enhance system robustness. On this basis, trained BPNNs are employed to address the remaining time delays in sliding mode and reduce nonlinear effects. During compensation with the BPNN-SM method, the desired command  $y^{\text{DC}}$  is expanded into an input  $y^{\text{BC}}$  for the BPNN through an expansion module. The  $y^{\text{BC}}$  is passed to the trained BPNN to get the actual output

![Block diagram of the BPNN-SM method. The process starts with a direct command y^DC entering an 'Expansion module' to produce y^BC. This signal y^BC is fed into a 'Trained BPNN' block, which outputs y^AC. The signal y^AC is then fed into the 'SMC' (Sliding Mode Controller) block. Inside the SMC block, y^AC is compared with the estimated state x-hat (from a 'State observer (KF filter)') to produce an error signal e. This error signal e is integrated (indicated by a 1/s block) to produce a control signal u, which is then multiplied by a gain k_1. The result is added to the estimated state x-hat to produce the external command y^EC. The signal y^EC is then fed into the 'Hydraulic servo actuator and test specimen' block, which has a transfer function G_A(s). The output of this block is the system response y^R, which is fed back to the 'State observer (KF filter)' to update the estimated state x-hat.](690fce4fb5c9cbb8beb560cb2a3fcbeb_img.jpg)

Block diagram of the BPNN-SM method. The process starts with a direct command y^DC entering an 'Expansion module' to produce y^BC. This signal y^BC is fed into a 'Trained BPNN' block, which outputs y^AC. The signal y^AC is then fed into the 'SMC' (Sliding Mode Controller) block. Inside the SMC block, y^AC is compared with the estimated state x-hat (from a 'State observer (KF filter)') to produce an error signal e. This error signal e is integrated (indicated by a 1/s block) to produce a control signal u, which is then multiplied by a gain k\_1. The result is added to the estimated state x-hat to produce the external command y^EC. The signal y^EC is then fed into the 'Hydraulic servo actuator and test specimen' block, which has a transfer function G\_A(s). The output of this block is the system response y^R, which is fed back to the 'State observer (KF filter)' to update the estimated state x-hat.

Fig. 1. Principle of BPNN-SM method.

$y^{\text{AC}}$  of the BPNN, and sends  $y^{\text{AC}}$  to the SMC. After SMC compensation, the external command  $y^{\text{EC}}$  for the hydraulic servo actuator is obtained and applied to the test specimen, with the specimen's response  $y^{\text{R}}$  measured by displacement sensors.  $G_A(s)$  is the transfer function of the hydraulic servo actuator and the test specimen. The hydraulic servo actuator and the test specimen are the controlled system of SMC. Given that the sensor's direct measurements are affected by noise, a state observer is used to achieve a more accurate state vector  $\hat{\mathbf{X}}$  of the hydraulic servo-actuator and test specimen. Additionally, the observed state vector  $\hat{\mathbf{X}}$  is fed back into the SMC, allowing the controller to continuously adjust the control signals to ensure system tracking of the target and adaptation to dynamic changes. The design of the SMC, the principle and construction of BPNN, and implementation of BPNN-SM are presented in Secs. 2.1–2.3, respectively.

### 2.1. Sliding mode controller design

SMC is a nonlinear control method widely used to address control issues involving uncertainty and system disturbances. The BPNN-SM method employs SMC as the feedback controller for the loading system to improve system robustness and compensate for partial time delays.

The principle of the SMC method is shown in Fig. 1. Before designing the SMC, the mathematical model of the controlled system needs to be established. In this paper, we only consider the nonlinearity between the actuator and the test specimen. To be convenient for later analysis, the actuator-test specimen is expressed in the form of a differential equation as follows:

$$\frac{d^3}{dt^3}y^{\text{R}} + a_1 \frac{d^2}{dt^2}y^{\text{R}} + a_2 \frac{d}{dt}y^{\text{R}} + a_3 y^{\text{R}} = b_1 y^{\text{EC}}, \quad (2.1)$$

where  $a_1, a_2, a_3$  and  $b_1$  are the system parameters, which can be identified by white noise excitation tests.

The controlled system transfer function can be described as a state space form, as shown in Eq. (2.2):

$$\begin{aligned}\dot{\mathbf{X}} &= \mathbf{AX} + \mathbf{B}y^{\text{EC}}, \\ y^{\text{R}} &= \mathbf{CX},\end{aligned}\tag{2.2}$$

where  $\dot{\mathbf{X}}$ ,  $\mathbf{A}$ ,  $\mathbf{B}$  and  $\mathbf{C}$  are state space matrices, respectively:

$$\dot{\mathbf{X}} = \begin{bmatrix} y^{\text{R}} \\ \dot{y}^{\text{R}} \\ \ddot{y}^{\text{R}} \end{bmatrix}, \quad \mathbf{A} = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -a_3 & -a_2 & -a_1 \end{bmatrix}^T, \quad \mathbf{B} = \begin{bmatrix} 0 \\ 0 \\ b_1 \end{bmatrix} \quad \text{and} \quad \mathbf{C} = [1 \quad 0 \quad 0].$$

The tracking error term  $e$  is expressed as shown in the following equation:

$$e = y^{\text{AC}} - y^{\text{R}}.\tag{2.3}$$

To improve command tracking performance, the internal model control principle is introduced, as shown in the following equation:

$$\xi = \int_{0}^{t} e(\tau) d\tau\tag{2.4}$$

Combining Eqs. (2.3) and (2.4), the state space equation (2) can be transformed as shown in the following equation:

$$\begin{aligned}\dot{\mathbf{X}}^* &= \mathbf{A}^* \mathbf{X}^* + \mathbf{B}^* y^{\text{EC}}, \\ \dot{y}^{\text{EC}} &= [k_1 - \mathbf{K}] \mathbf{X}^*,\end{aligned}\tag{2.5}$$

where  $\mathbf{X}^* = \begin{pmatrix} e \\ \dot{x} \end{pmatrix}$ ,  $\mathbf{A}^* = \begin{pmatrix} 0 & -\mathbf{C} \\ \mathbf{0}_{r \times 1} & \mathbf{A} \end{pmatrix}$ ,  $\mathbf{B}^* = \begin{pmatrix} 0 \\ \mathbf{B} \end{pmatrix}$ ,  $r$  is the number of state vectors of the controlled system,  $k_1$  is the integral gain coefficient of the SMC and  $\mathbf{K}$  is the state feedback gain coefficient.

A sliding surface is introduced, and the sliding surface is defined as shown in the following equation:

$$\mathbf{s} = \mathbf{P}\mathbf{Y} = 0,\tag{2.6}$$

where  $\mathbf{P}$  is the sliding mode variable.

To ensure that the controlled system operates on the sliding surface, the expression for the input of the controlled system  $y^{\text{EC}}$  is designed as shown in the following equation:

$$\dot{y}^{\text{EC}} = (\mathbf{G}_s - \delta \chi^{\text{T}}) \mathbf{X}^*,\tag{2.7}$$

where  $\mathbf{G}_s = -(\mathbf{P}\mathbf{B}^*)^{-1}\mathbf{P}\mathbf{A}^*$ ,  $\chi = \mathbf{P}^{\text{T}}\mathbf{P}\mathbf{B}^*$  and  $\delta$  is given positive constants, representing the sliding mode margin.

Combining Eq. (2.1)–(2.7), the  $y^{\text{EC}}$  can be described as

$$y^{\text{EC}} = k_1 \xi - \mathbf{K}\hat{\mathbf{X}}. \quad (2.8)$$

The detailed solution process is outlined in Ref. 14.

The system time delay mainly consists of two parts: One is the fixed time delay caused by communication and computing, which has nonlinear characteristics. The second is the frequency-related hysteresis, which shows a linear characteristic. SMC can effectively handle nonlinear problems 9. Its strategy is to regard nonlinear fixed time delays as disturbances, thereby converting them into equivalent linear hysteresis. After SMC compensation, there is still some residual linear hysteresis in the system. For this, it is usually necessary to introduce the reverse compensation method for compensation. However, traditional inverse compensation methods amplify high-frequency signals, which in turn require filters for suppression, and the filters themselves introduce new time delays. Through offline training, BPNN can learn the characteristics of the system after SMC compensation and then construct an optimized inverse compensation model. Therefore, introducing this offline training BPNN inverse compensation based on the SMC can effectively compensate for the system delay while maintaining the good robustness of the system. In BPNN-SM, BPNN is a trained offline neural network, and as a feedforward inverse compensation, it is a leading system that does not introduce additional time delays.

### 2.2. Backpropagation neural network

The RTHHT time delay compensation system in this study is a single-input single-output (SISO) system with time-varying delays. If a BPNN is trained directly using SISO data, it may fail to effectively learn and capture the relationship between inputs and outputs. Therefore, Sec. 2.2.1 primarily focuses on expanding the SISO framework into a multi-input single-output framework. This expansion allows the neural network to better learn and capture the complex nonlinear relationships between inputs and outputs. Following this, Sec. 2.2.2 provides a detailed explanation of the experimental system used to collect the dataset when constructing the inverse model with BPNN. Finally, Sec. 2.2.3 introduces the principles of the BPNN in the context of the practical training system.

#### 2.2.1. Expansion of input data of BPNN

The system used in this study is a SISO system. When the output of the actuator serves as an independent input, it is difficult for the network to capture the temporal correlation between points. The introduction of the extension module converts the one-dimensional displacement response into a multidimensional feature matrix through the sliding window mechanism, as shown in Fig. 2, solving the limitation of BPNN in modeling SISO systems. This design significantly enhances the ability

![Expansion diagram showing the transformation of input data into an expanded input data matrix. The input data matrix is a horizontal sequence of elements y_1^{R'}, y_2^{R'}, y_3^{R'}, ..., y_{n-1}^{R'}, y_n^{R'}, ..., y_{p-n+1}^{R'}, y_{p-n+2}^{R'}, y_{p-n+3}^{R'}, ..., y_{p-1}^{R'}, y_p^{R'}. The expanded input data matrix is a p x n grid where each row contains a shifted version of the input sequence. For example, the first row contains y_1^{R'}, y_2^{R'}, y_3^{R'}, ..., y_{n-1}^{R'}, y_n^{R'}, ..., y_{p-n+1}^{R'}. The second row contains y_2^{R'}, y_3^{R'}, ..., y_n^{R'}, ..., y_{p-n+2}^{R'}, and so on, with the last row containing y_n^{R'}, ..., y_p^{R'}. Arrows show the mapping from the input sequence to the corresponding rows of the expanded matrix.](2ee59e629035d641140e55f4d215b0d7_img.jpg)

Expansion diagram showing the transformation of input data into an expanded input data matrix. The input data matrix is a horizontal sequence of elements y\_1^{R'}, y\_2^{R'}, y\_3^{R'}, ..., y\_{n-1}^{R'}, y\_n^{R'}, ..., y\_{p-n+1}^{R'}, y\_{p-n+2}^{R'}, y\_{p-n+3}^{R'}, ..., y\_{p-1}^{R'}, y\_p^{R'}. The expanded input data matrix is a p x n grid where each row contains a shifted version of the input sequence. For example, the first row contains y\_1^{R'}, y\_2^{R'}, y\_3^{R'}, ..., y\_{n-1}^{R'}, y\_n^{R'}, ..., y\_{p-n+1}^{R'}. The second row contains y\_2^{R'}, y\_3^{R'}, ..., y\_n^{R'}, ..., y\_{p-n+2}^{R'}, and so on, with the last row containing y\_n^{R'}, ..., y\_p^{R'}. Arrows show the mapping from the input sequence to the corresponding rows of the expanded matrix.

Fig. 2. Expansion diagram.

of BPNN to learn the inverse dynamics of the loading system, enabling BPNN to more accurately approximate the inverse model of the loading system. This study expands the original training input data  $\mathbf{y}_{1 \times p}^{R'}$  to  $\mathbf{y}_{n \times (p-n+1)}^{R'}$ , as shown in Eqs. (2.9) and (2.10). The specific expansion is shown in Fig. 2, and the original single input is expanded to multiple inputs according to the way shown in the figure.

$$\mathbf{y}_{1 \times p}^{R'} = \begin{bmatrix} y_1^{R'} \\ \vdots \\ y_p^{R'} \end{bmatrix}^T, \quad (2.9)$$

where  $p$  is the length of each test sample before expansion,  $y_p^{R'}$  is the  $p$ th output of the test specimen during training of the BPNN.

$$\mathbf{y}_{n \times (p-n+1)}^{R'} = \begin{bmatrix} y_1^{R'} & y_2^{R'} & \cdots & y_n^{R'} \\ y_2^{R'} & y_3^{R'} & \cdots & y_{n+1}^{R'} \\ \vdots & \vdots & \ddots & \vdots \\ y_{p-n+1}^{R'} & y_{p-n+2}^{R'} & \cdots & y_p^{R'} \end{bmatrix}^T, \quad n < p, \quad (2.10)$$

where  $n$  is the number of expanded rows.

#### 2.2.2. Training system for dataset establishment

The core of the reverse training in this study is to take the response displacement  $y^{R'}$  of the specimen as the input and the expected command  $y^{\text{DC}'}$  as the target output. It is to train the BPNN through reverse data mapping and construct the inverse model of the SMC system. The function of this inverse model lies in generating control instructions with leading characteristics, thereby effectively compensating for the residual time delay of the original SMC. Dataset establishment was conducted

![Block diagram of the test system using the SMC method. The diagram shows a flow from left to right. On the far left, the input y^{DC'} enters a yellow box labeled 'Delay module'. The output of this module enters a green dashed box labeled 'SMC'. Inside the SMC box, the signal enters a white box labeled 'Sliding mode controller'. A feedback loop from the output of the controller to the input of the controller is labeled with a tilde over x, \tilde{x}. Below the controller is a white box labeled 'State observer (KF filter)'. The output of the controller enters a blue box labeled 'Hydraulic servo actuator and test specimen'. The output of this blue box is y^{R'}. A feedback line from y^{R'} loops back to the input of the 'Sliding mode controller'.](acfc53eca625d62b38aa2563efa95c3e_img.jpg)

Block diagram of the test system using the SMC method. The diagram shows a flow from left to right. On the far left, the input y^{DC'} enters a yellow box labeled 'Delay module'. The output of this module enters a green dashed box labeled 'SMC'. Inside the SMC box, the signal enters a white box labeled 'Sliding mode controller'. A feedback loop from the output of the controller to the input of the controller is labeled with a tilde over x, \tilde{x}. Below the controller is a white box labeled 'State observer (KF filter)'. The output of the controller enters a blue box labeled 'Hydraulic servo actuator and test specimen'. The output of this blue box is y^{R'}. A feedback line from y^{R'} loops back to the input of the 'Sliding mode controller'.

Fig. 3. Test system using SMC method as compensation method.

within an experimental system that employs only the SMC method as a compensation technique, as illustrated in Fig. 3.  $y^{DC'}$ ,  $y^{EC'}$  and  $y^{R'}$  are the variables in the system used for BPNN training corresponding to Fig. 1. During the process of extending the input for the BPNN, a fixed time delay is introduced, and the original system inherently possesses a time delay as well. To address this issue, this study introduces a delay module and employs a backward training method. As shown in Fig. 3, a delay module is appended to the desired command, with the delay steps of the module set to  $n/1024$  s. The primary function of the delay module is to mitigate the fixed time delay introduced during the extension process. The reverse training method is utilized to address the inherent time delay in the original system and to learn the system's dynamic characteristics.

#### 2.2.3. The principle of BPNN based on training system

The BPNN is a type of multi-layer feedforward neural network trained using the backpropagation algorithm.<sup>43,44</sup> Its core idea is to employ the gradient descent method, where the gradients of the loss function with respect to the network parameters are computed to iteratively adjust the weights and biases, thereby minimizing the loss function. The topology of the BPNN consists of an input layer, hidden layers and an output layer, as illustrated in Fig. 4. In this structure,  $y^{AC'}$  corresponds to the output value of the BPNN during training;  $l$  denotes the  $l$ th layer (current layer);  $i$  represents the  $i$ th neuron in the  $(l-1)$ th layer;  $j$  represents the  $j$ th neuron in the  $l$ th layer;  $z_j^l$  is the weighted sum of the  $j$ th neuron in the  $l$ th layer;  $a_j^l$  is the output value of the  $j$ th neuron in the  $l$ th layer;  $\omega_{ij}^l$  is the weight from the  $i$ th neuron in the  $(l-1)$ th layer to the  $j$ th neuron in the  $l$ th layer, and  $m$  represents the  $m$ th neuron in the  $(l+1)$ th layer. The learning process of a BPNN mainly consists of two stages: Forward propagation and error backpropagation. In the forward propagation stage, input data is processed through the activation functions of the hidden layers, ultimately reaching the output layer to generate output values. Subsequently, in the error backpropagation stage, the error between the actual output and the desired output is computed and propagated backward along the original connection paths. Using algorithms such as gradient descent, the network adjusts the connection weights and thresholds of each node to minimize the error between

![Diagram of a BPNN structure showing three layers: Input, Hidden, and Output. The Input layer has nodes y1^R, y2^R, ..., yn^R. The Hidden layer has nodes z1^{l-1}, a1^{l-1}, z2^{l-1}, a2^{l-1}, ..., zi^{l-1}, ai^{l-1}. The Output layer has nodes z1^l, a1^l, z2^l, a2^l, ..., zj^l, aj^l, z_{m}^{l+1}, a_{m}^{l+1}. Connections are shown between layers, with weights w_{ij}^l and w_{jm}^{l+1}. The final output is y^{AC}.](f4fdd410cdb84df81274da55721e56fb_img.jpg)

Diagram of a BPNN structure showing three layers: Input, Hidden, and Output. The Input layer has nodes y1^R, y2^R, ..., yn^R. The Hidden layer has nodes z1^{l-1}, a1^{l-1}, z2^{l-1}, a2^{l-1}, ..., zi^{l-1}, ai^{l-1}. The Output layer has nodes z1^l, a1^l, z2^l, a2^l, ..., zj^l, aj^l, z\_{m}^{l+1}, a\_{m}^{l+1}. Connections are shown between layers, with weights w\_{ij}^l and w\_{jm}^{l+1}. The final output is y^{AC}.

Fig. 4. A BPNN structure.

the actual and desired output values until convergence is achieved. This process durably reduces the error, enabling the neural network to effectively learn complex relationships.

In the forward propagation process, the input signal propagates from the input layer through the hidden layers to the output layer. The output of each layer is computed as the weighted sum of the outputs from the previous layer plus a bias term, followed by processing through an activation function. The output of each neuron in a layer is calculated as shown in the following equations:

$$z_j^l = \sum_i \omega_{ij}^l \cdot a_i^{l-1} + b_j^l \quad (2.11)$$

$$a_j^l = f^l(z_j^l) \quad (2.12)$$

where  $a_i^{l-1}$  is the output value of the  $i$ th neuron in the  $(l-1)$ th layer,  $b_j^l$  is the bias term of the  $j$ th neuron in the  $l$ th layer,  $f^l(\cdot)$  is the activation function used in the  $l$ th layer, which typically includes functions such as Sigmoid.

During backpropagation, the error gradient is computed and propagated from the output layer back to the input layer. The chain rule is applied to determine the gradients of the weights and biases, and the parameters are updated along the negative gradient direction using gradient descent to minimize the loss function. The loss function, the error gradient of the output layer, and the error gradient of the hidden layers are calculated as shown in Eqs. (2.13)–(2.15):

$$E = \frac{1}{2} \sum_1^p (y^{\text{DC}'} - y^{\text{AC}'})^2, \quad (2.13)$$



$$\delta^L = \left[ \sum_1^p (y^{AC'} - y^{DC'}) \right] \cdot \dot{f}^L(z^L), \quad (2.14)$$

$$\delta_j^l = \left( \sum_m \delta_m^{l+1} \cdot w_{jm}^{l+1} \right) \cdot \dot{f}^l(z_j^l), \quad (2.15)$$

where  $L$  is the output layer,  $\delta^L$  is the error term of the output layer,  $\delta_j^l$  represents the error term of the  $j$ th neuron in the  $l$ th layer and  $w_{jm}^{l+1}$  denotes the weight from the  $j$ th neuron in the  $l$ th layer to the  $m$ th neuron in the  $(l+1)$ th layer.

After computing the error terms  $\delta_j^l$ , the gradients of the weights and biases are calculated. Then, according to the gradient descent rule, the parameters are adjusted along the negative gradient direction. The updates for the weights and biases are shown in the following equations:

$$w_{ij}^l \leftarrow w_{ij}^l - \eta \left( \frac{\partial E}{\partial w_{ij}^l} \right), \quad (2.16)$$

$$b_j^l \leftarrow b_j^l - \eta \left( \frac{\partial E}{\partial b_j^l} \right), \quad (2.17)$$

where  $\eta$  is the learning rate, a small positive value that can be determined through trial and error,  $\frac{\partial E}{\partial w_{ij}^l} = \delta_j^l \cdot a_i^{l-1}$ , and  $\frac{\partial E}{\partial b_j^l} = \delta_j^l$ .

In order to improve the learning efficiency and convergence speed, this study introduces the Levenberg-Marquardt (LM) algorithm,<sup>45</sup> which is based on approximate second-order derivatives, to optimize the BPNN during the parameter update phase.

Although BPNN is a powerful nonlinear function approximator, its performance is highly dependent on the quality and coverage of the training data. For complex time delays with strong nonlinearity, time-varying or unseen operating conditions, the training data may be difficult to fully cover them, resulting in insufficient generalization ability of the model. If unexpected time-varying disturbances or new nonlinear characteristics not covered by the training data occur in the real-time system, the BPNN controller alone may not be able to handle them effectively, leading to performance degradation or even system instability. Therefore, it needs to be combined with SMC.

### 2.2.4. Selection of input layer and hidden layer

To better select the number of neurons in the input layer and the number of nodes in the hidden layer of BPNN, after collecting the training dataset obtained from the pre-test using the system shown in Fig. 3 in this section, the network was tested using MATLAB. To more effectively evaluate the performance of neural network

training, 70% of the input and output datasets will be used as the training set, 15% as the test set and 15% as the prediction set. The training performance will be assessed through the coefficient of determination ( $R^2$ ) to compare the difference between the predicted output and the actual output.

Figures 5(a)–5(d) indicate that the BPNN with 40 input neurons and 4 hidden layers, as well as 50 input neurons and 3 hidden layers, performs well, but there is

![Four scatter plots showing neural network regression results. (a) Training: R^2=0.98184, (b) Test: R^2=0.98097, (c) Training: R^2=0.97975, (d) Test: R^2=0.98104. Each plot shows Data (black dots), Fit (solid line), and Y=T (dashed green line).](252ea48d02dce93965b91746fb376f35_img.jpg)

Figure 5 consists of four scatter plots arranged in a 2x2 grid, labeled (a) through (d). Each plot shows the relationship between 'Target' (x-axis) and 'Output' (y-axis), both ranging from 0 to 1. The plots include three data series: 'Data' represented by black dots, 'Fit' represented by a solid line, and 'Y = T' represented by a dashed green line. The R-squared values for each plot are as follows:

- (a) Training:  $R^2=0.98184$
- (b) Test:  $R^2=0.98097$
- (c) Training:  $R^2=0.97975$
- (d) Test:  $R^2=0.98104$

Four scatter plots showing neural network regression results. (a) Training: R^2=0.98184, (b) Test: R^2=0.98097, (c) Training: R^2=0.97975, (d) Test: R^2=0.98104. Each plot shows Data (black dots), Fit (solid line), and Y=T (dashed green line).

Fig. 5. Neural network training regression. (a) Regression with 40 input neurons and a 4-layer hidden layer training set, (b) Regression with 40 input neurons and a 4-layer hidden layer testing set, (c) Regression with 50 input neurons and a 3-layer hidden layer training set, (d) Regression with 50 input neurons and a 3-layer hidden layer testing set, (e) Regression with 50 input neurons and a 4-layer hidden layer training set and (f) Regression with 50 input neurons and a 4-layer hidden layer testing set

![Figure 5 (Continued) showing two scatter plots: (e) Training and (f) Test. Both plots show Output vs Target with R-squared values very close to 1, indicating a near-perfect fit.](2236272d3b3db6e6363337f5a8db72f6_img.jpg)

Figure 5 (Continued) consists of two scatter plots, (e) and (f), showing the relationship between Output and Target. Both plots include data points (black dots), a fitted line (solid blue line in (e), solid red line in (f)), and a target line  $Y = T$  (dashed green line). Plot (e) is titled 'Training:  $R^2=0.99717$ ' and has axes from 0 to 1. Plot (f) is titled 'Test:  $R^2=0.99668$ ' and has axes from 0 to 1 for Output and from 0.2 to 0.8 for Target. In both cases, the data points are tightly clustered around the fitted line, which is nearly identical to the target line  $Y = T$ .

Figure 5 (Continued) showing two scatter plots: (e) Training and (f) Test. Both plots show Output vs Target with R-squared values very close to 1, indicating a near-perfect fit.

Fig. 5. (Continued)

still a slight underfitting, and the deviation between the fitting line and the target line can still be reduced. As can be seen from (e) and (f) in Fig. 5, the  $R^2$  of BPNN is very close to 1, and the data points almost completely conform to the target line  $Y = T$ , indicating that the fitting effect is the best. It indicates that the network structure of 50 input neurons and 4 hidden layers achieves nearly perfect fitting effect and generalization ability in the regression task, and is significantly superior to other combinations. Therefore, the BPNN structure used in this paper consists of 50 input neurons and 4 hidden layers.

## 2.3. Implementation procedure

The controller proposed in this study consists of two core components: An inverse model trained using BPNN and SMC. The design methodology of the controller is as follows:

- (i) In the system shown in Fig. 3, without the delay module, conduct the test and input the desired command, recording the response of the specimen. Use the response data as the input set for training the BPNN and the desired command as the output set. Perform backward training to obtain the inverse model.
- (ii) As described in Sec. 2.2.1, gradually expand the input set until a well-trained BPNN is achieved (that is, the coefficient of determination  $R^2$  satisfies  $0.99 \le R^2 < 1$ ). At this stage, the input data is expanded from 1 row to  $n$  rows.
- (iii) As outlined in Sec. 2.2.2, add a delay module before the SMC, setting the time delay of the delay module to  $n/1024$ s. Conduct the experiment again in the system shown in Fig. 3, recording the response of the specimen. Use the

Y. Shangguan *et al.*

response data from this test as the input set and the desired command as the output set to retrain the BPNN, thereby obtaining a higher-precision inverse model.

- (iv) Integrate the trained BPNN with SMC as shown in Fig. 1 to form the BPNN-SM method.

Through the above steps, the controller design is completed and can be applied to tests.

# 3. MTS-Speedgoat-Based RTHT Platform

In this study, the delay compensation performance tests for predefined loading targets and RTHT were conducted using the MTS-Speedgoat RTHT platform at the Earthquake Engineering Research and Test Center of Guangzhou University. The hardware and software integration schematic of the RTHT system is illustrated in Fig. 6. The platform comprises a host computer, a Speedgoat RTHT target computer, Scramnet shared memory cards, an MTS controller and an MTS hydraulic servo actuator. The hydraulic servo actuator used in the testing is MTS 244.22, and its time delay under excitation of 15 Hz sine wave with amplitude 0.5 mm is 28.6 ms. The Speedgoat target computer is equipped with highperformance real-time processing capabilities, enabling the execution of complex control and simulation tasks with minimal latency. The Scramnet shared memory cards facilitate real-time communication among the devices via optical fiber connections.

The software utilized in the RTHT system includes MATLAB/Simulink and its associated real-time operation tool, MATLAB/xPC-Target. The experimental program is pre-established in the MATLAB/Simulink environment on the host

![Hardware and software integration schematic of the MTS-Speedgoat-based RTHT system. The diagram shows a flow from the Host Computer (MATLAB/Simulink) to the Speedgoat real-time hybrid test target computer (xPC-Target) via Exclusive C language. The target computer interacts with Scramnet shared memory cards. The MTS Controller and MTS hydraulic servo actuator and specimen are connected to the Scramnet cards. The control loop involves Ground motion acceleration, Numerical substructure (M_N), Desired command, Expansion module, Trained BP, SMC (Sliding Mode Control), and External command to the Actuator. The Experimental substructure provides Displacement feedback signals and Force feedback signals back to the Trained BP and SMC modules.](f6e8acf9f931452d01688d311b5c0364_img.jpg)

The diagram illustrates the hardware and software integration of the MTS-Speedgoat-based RTHT platform. It shows the following components and their interactions:

- Host Computer:** Runs MATLAB/Simulink and provides the **Desired command** to the target computer via **Exclusive C language**.
- Speedgoat real-time hybrid test target computer:** Executes the real-time control algorithm using **xPC-Target**.
- Scramnet shared memory card:** Facilitates real-time communication between the target computer and the MTS controller.
- MTS Controller:** Manages the hydraulic servo actuator.
- MTS hydraulic servo actuator and specimen:** The physical test subject.
- Control Loop:**
  - Ground motion acceleration** is scaled by  $\times M_N$  and fed into the **Numerical substructure**.
  - The **Numerical substructure** outputs a **Desired command** to the **Expansion module**.
  - The **Expansion module** feeds into the **Trained BP** (BPNN-SM method).
  - The **Trained BP** and **SMC** (Sliding Mode Control) modules are part of the **BPNN-SM method**.
  - The **SMC** module outputs an **External command** to the **Actuator**.
  - The **Actuator** is connected to the **Experimental substructure**.
  - The **Experimental substructure** provides **Displacement feedback signals** and **Force feedback signals** back to the **Trained BP** and **SMC** modules.
- Scramnet:** Provides **Displacement and force feedback signals** from the MTS controller and actuator to the target computer.

Hardware and software integration schematic of the MTS-Speedgoat-based RTHT system. The diagram shows a flow from the Host Computer (MATLAB/Simulink) to the Speedgoat real-time hybrid test target computer (xPC-Target) via Exclusive C language. The target computer interacts with Scramnet shared memory cards. The MTS Controller and MTS hydraulic servo actuator and specimen are connected to the Scramnet cards. The control loop involves Ground motion acceleration, Numerical substructure (M\_N), Desired command, Expansion module, Trained BP, SMC (Sliding Mode Control), and External command to the Actuator. The Experimental substructure provides Displacement feedback signals and Force feedback signals back to the Trained BP and SMC modules.

Fig. 6. MTS-Speedgoat-based RTHT platform.

computer and compiled into C language format files, which are then transmitted to the Speedgoat target computer via optical fiber. The target computer solves the motion differential equations based on the numerical substructure model and the force feedback from the experimental substructure to derive the desired command. The time delay compensation method generates the output command by compensating based on the desired command and displacement feedback.

The output command is sent to the MTS controller through the Scramnet shared memory cards, which control the hydraulic servo actuator to perform the loading operation. Displacement sensors and force sensors sample in real-time, transmitting displacement feedback to the Scramnet shared memory cards. Upon receiving the feedback, the target computer recalculates the output command, and the process is repeated until the experiment concludes.

The controlled object of the SMC method is a nonlinear system consisting of the hydraulic servo actuator and the specimen. A band-limited white noise with a 20 Hz cutoff frequency and an amplitude of 1 mm is used as the input to the controlled object in order to obtain the output data. The system identification toolbox in MATLAB is then used to identify the transfer function. The identified controlled system transfer function  $G_A(s)$  is shown in the following equation:

$$G_A(s) = \frac{1.5758 \times 10^6}{s^3 + 4.4111 \times 10^2 s^2 + 1.1534 \times 10^5 s + 1.1534 \times 10^5}. \quad (3.1)$$

Figure 7 compares the Bode diagrams of the actual actuator and experimental substructure system with the identified transfer function system. It can be

![Figure 7: System Bode diagram comparison. The figure consists of two subplots. The top subplot shows the Amplitude (dB) versus Frequency (Hz) from 0 to 20 Hz. The bottom subplot shows the Phase (degree) versus Frequency (Hz) from 0 to 25 Hz. Both plots compare the 'Actual system' (blue dashed line) and the 'Transfer function system' (red dashed line). In the amplitude plot, both systems are nearly flat at 1 dB. In the phase plot, both systems show a linear decrease from 0 degrees at 0 Hz to approximately -60 degrees at 25 Hz.](239211fa511b4ffa685b54b5132ec927_img.jpg)

Figure 7: System Bode diagram comparison. The figure consists of two subplots. The top subplot shows the Amplitude (dB) versus Frequency (Hz) from 0 to 20 Hz. The bottom subplot shows the Phase (degree) versus Frequency (Hz) from 0 to 25 Hz. Both plots compare the 'Actual system' (blue dashed line) and the 'Transfer function system' (red dashed line). In the amplitude plot, both systems are nearly flat at 1 dB. In the phase plot, both systems show a linear decrease from 0 degrees at 0 Hz to approximately -60 degrees at 25 Hz.

Fig. 7. System Bode diagram comparison.

observed that within the frequency range of 20 Hz, the amplitude and phase frequency responses of the transfer function system closely align with the actual system. The transfer function identified in this study is highly accurate within the frequency range of 20 Hz.

# 4. Experimental Validation

To better assess the stability and robustness of the BPNN-SM method, this section presents validation through delay compensation performance tests for pre-defined loading targets and RTHT. The working condition table in this study is shown in Table 1. And the span of the tests was set to 50s, with a sampling time of 1/1024s. Three different waveforms are used as excitation signals in both tests, and the incentives used in the tests are inconsistent with those used in the training of the BPNN. The parameters used in this study were selected through multiple experiments to form the optimal parameter combination. The testing parameters for the BPNN-SM method are summarized as follows: For delay compensation performance tests, the input excitations are a sine wave and band-limited white noise, with  $Q$  set to  $\text{diag}([3 \times 10^6, 1 \times 10^{-4}, 9 \times 10^{-7}])$  and  $\text{diag}([1.8 \times 10^9, 1 \times 10^{-4}, 9 \times 10^{-7}])$ , respectively. For the El-Centro earthquake excitation,  $Q$  is  $\text{diag}([5.65 \times 10^8, 1 \times 10^{-4}, 9 \times 10^{-7}])$ . In RTHT, the input excitations include band-limited white noise and the El-Centro earthquake, with  $Q$  set to  $\text{diag}([6.3 \times 10^9, 1 \times 10^{-4}, 9 \times 10^{-7}])$  and  $\text{diag}([1.7 \times 10^8, 1 \times 10^{-4}, 9 \times 10^{-7}])$ , respectively. For all tests, the parameter  $\delta$  is set to  $10^{-9}$ ,  $Q_e$  is  $10^{-2}$  and  $R_e$  is  $10^{-3}$ . And the hyperparameters of BPNN were fine-tuned through multiple trainings using MATLAB code, and ultimately, the parameter combination that made  $R^2$  closest to 1 was selected. The topology of this BPNN model is illustrated in Fig. 8. BPNN has four hidden layers, with specific parameter settings as follows: the number of neurons in the four hidden layers is 12, 12, 12 and 15, respectively; the activation functions for the hidden and output layers are “logsig” and “purelin”, respectively;

Table 1. Working conditions.

| Command type             | Frequency (HZ) | Amplitude (mm) | Application                          |
|--------------------------|----------------|----------------|--------------------------------------|
| Band-limited white noise | 0-20           | 1              | Training BPNN                        |
| Band-limited white noise | 0-20           | 0.5            |                                      |
| El-Centro earthquake     | /              | 5              |                                      |
| El-Centro earthquake     | /              | 2              |                                      |
| Sine wave                | 7.5            | 0.2            | Delay compensation performance tests |
| Band-limited white noise | 0-20           | 0.3            | Delay compensation performance tests |
| El-Centro earthquake     | /              | 3              | and RTHT                             |

![Diagram of a BPNN structure with four hidden layers. The input layer has 50 nodes labeled y1^R, y2^R, ..., y50^R. The first hidden layer has 15 nodes labeled z1^1, z2^1, ..., z15^1 and a^1_1, a^1_2, ..., a^1_15. The second hidden layer has 12 nodes labeled z1^2, z2^2, ..., z12^2 and a^2_1, a^2_2, ..., a^2_12. The third hidden layer has 8 nodes labeled z1^3, z2^3, ..., z8^3 and a^3_1, a^3_2, ..., a^3_8. The fourth hidden layer has 5 nodes labeled z1^4, z2^4, ..., z5^4 and a^4_1, a^4_2, ..., a^4_5. The output layer has 1 node labeled y^AC. All nodes in adjacent layers are fully connected. Brackets below the layers label them as 'Input layer', 'Hiden layer', 'Hiden layer', 'Hiden layer', and 'Output layer'.](c85ded401105f62f2d6ff26b3b5eb4af_img.jpg)

Diagram of a BPNN structure with four hidden layers. The input layer has 50 nodes labeled y1^R, y2^R, ..., y50^R. The first hidden layer has 15 nodes labeled z1^1, z2^1, ..., z15^1 and a^1\_1, a^1\_2, ..., a^1\_15. The second hidden layer has 12 nodes labeled z1^2, z2^2, ..., z12^2 and a^2\_1, a^2\_2, ..., a^2\_12. The third hidden layer has 8 nodes labeled z1^3, z2^3, ..., z8^3 and a^3\_1, a^3\_2, ..., a^3\_8. The fourth hidden layer has 5 nodes labeled z1^4, z2^4, ..., z5^4 and a^4\_1, a^4\_2, ..., a^4\_5. The output layer has 1 node labeled y^AC. All nodes in adjacent layers are fully connected. Brackets below the layers label them as 'Input layer', 'Hiden layer', 'Hiden layer', 'Hiden layer', and 'Output layer'.

Fig. 8. BPNN structure of four hidden layers.

the input layer consists of 50 feature vectors, while the output layer has 1 feature vector; the learning rate is set to 0.001, the maximum number of iterations is 1000, and the target minimum error for training is  $10^{-5}$ ; the backpropagation training algorithm employs the LM algorithm.

Before conducting delay compensation performance tests for predefined loading targets and RTHT, this section defines the quantitative analysis indicators  $J_1 - J_5$  to facilitate a more intuitive assessment of the compensation performance of the control methods and the reliability of the RTHT results.  $J_1 - J_3$  are used to evaluate the compensation performance of the methods, while  $J_4 - J_5$  assess the reliability of the RTHT results.<sup>46</sup>

The tracking delay of the system is defined as  $J_1$ :

$$J_1 = \arg_k \max \left( \sum_p (y^{\text{DC}}(p) - y^{\text{R}}(p - k))^2 \right). \quad (4.1)$$

The normalized root mean square error between the response displacement  $y^{\text{R}}$  and the desired command  $y^{\text{DC}}$  is defined as  $J_2$ :

$$J_2 = \sqrt{\frac{\sum_{p=1}^{N} [y^{\text{R}}(p) - y^{\text{DC}}(p)]^2}{\sum_{p=1}^{N} [y^{\text{DC}}(p)]^2}} \times 100\%. \quad (4.2)$$

The normalized peak error of the instantaneous error between the response displacement  $y^{\text{R}}$  and the desired command  $y^{\text{DC}}$  is defined as  $J_3$ :

$$J_3 = \frac{\max |y^{\text{R}}(p) - y^{\text{DC}}(p)|}{\max |y^{\text{DC}}(p)|} \times 100\%. \quad (4.3)$$

The normalized root mean square error between the experimental substructure displacement and the reference model calculated displacement  $y^r$  is defined as  $J_4$ :

$$J_4 = \sqrt{\frac{\sum_{p=1}^{N} [y^R(p) - y^r(p)]^2}{\sum_{p=1}^{N} [y^r(p)]^2}} \times 100\%. \quad (4.4)$$

The peak tracking error between the experimental substructure displacement and the reference model calculated displacement is defined as  $J_5$ :

$$J_5 = \frac{\max |y^R(p) - y^r(p)|}{\max |y^r(p)|} \times 100\%. \quad (4.5)$$

## 4.1. Division of substructure

The prototype of the main part of experimental substructure in the RTHT is one of the two mast structures located at the top of the SEG Plaza in Shenzhen,<sup>47,48</sup> with an actual and simplified structural diagrams shown in Fig. 9. One of the masts at the top of the SEG Plaza is scaled down by a geometric ratio of 1/20, and the loading point is positioned at two-thirds of the mast model's height, according to its first mode of vibration. To better validate the feasibility of the proposed method, the numerical substructure is assumed to be an equivalent SDOF system with mass and stiffness nine times that of the experimental substructure. The reference model is also modeled as an equivalent SDOF system, with a rigid connection between the numerical and experimental substructures. The schematic of the structure is shown

![Figure 9: Actual and simplified diagrams of the SEG Plaza and the mast structure. (a) Actual diagram of the SEG Plaza showing its components: Mast, Tar-macadam, Tower, and Podium. Dimensions include 50m for the podium, 292m for the tower, and 346m for the total height. (b) Simplified diagrams showing the cantilever beam section of the mast and the prototype of the main part of the experimental substructure.](7d066b8cdb123b3cba3584e8bb66f557_img.jpg)

Figure 9 consists of two parts. Part (a) is a photograph of the SEG Plaza in Shenzhen, with a red box highlighting the mast structure. Labels point to the Mast, Tar-macadam, Tower, and Podium. Dimensions of 50m, 292m, and 346m are indicated. Part (b) shows a simplified structural diagram. On the left, a 3D model of the mast is shown with a red box highlighting the cantilever beam section. On the right, a 2D schematic of the mast structure is shown, with a dashed box highlighting the prototype of the main part of the experimental substructure.

Figure 9: Actual and simplified diagrams of the SEG Plaza and the mast structure. (a) Actual diagram of the SEG Plaza showing its components: Mast, Tar-macadam, Tower, and Podium. Dimensions include 50m for the podium, 292m for the tower, and 346m for the total height. (b) Simplified diagrams showing the cantilever beam section of the mast and the prototype of the main part of the experimental substructure.

Fig. 9. Actual and simplified diagrams of the SEG Plaza and the mast structure. (a) Actual diagram of the SEG Plaza. (b) Simplified diagrams of the SEG Plaza and the mast structure

![Diagram of the substructure division of the Reference Test Hammer Test (RTH). The diagram shows a reference mass M_R on a base. A numerical substructure, consisting of a mass M_N, a spring K_N, and a damper C_N, is attached to the base. An experimental substructure, consisting of a mass M_E, a spring K_E, and a damper C_E, is attached to the numerical substructure. A force F(t) is applied to the reference mass M_R.](7f25db95ce3916c0e09803b861a2f7bc_img.jpg)

Diagram of the substructure division of the Reference Test Hammer Test (RTH). The diagram shows a reference mass M\_R on a base. A numerical substructure, consisting of a mass M\_N, a spring K\_N, and a damper C\_N, is attached to the base. An experimental substructure, consisting of a mass M\_E, a spring K\_E, and a damper C\_E, is attached to the numerical substructure. A force F(t) is applied to the reference mass M\_R.

Fig. 10. Substructure division of RTHT.

Table 2. Structural parameters.

|                           | Mass (kg) | Stiffness (N/m)    | Damping (N · s/m)  | Damping ratio (%) |
|---------------------------|-----------|--------------------|--------------------|-------------------|
| Experimental substructure | 225.1     | $7.19 \times 10^5$ | 254.44             | 1                 |
| Numerical substructure    | 2025.9    | $6.47 \times 10^6$ | $2.29 \times 10^3$ | 1                 |
| Reference model           | 2251      | $7.19 \times 10^6$ | $2.54 \times 10^3$ | 1                 |

in Fig. 10.  $M_R$  represents the mass of the reference model, while  $M_N$ ,  $C_N$  and  $K_N$  denote the mass, damping and stiffness of the numerical substructure, respectively.  $M_E$ ,  $C_E$  and  $K_E$  refer to the mass, damping and stiffness of the experimental substructure. The specific parameters are shown in Table 2.

The actual experimental setup and substructure are depicted in Fig. 11, where the experimental substructure consists of a scaled mast model with added

![Photograph of the experimental equipment and experimental substructure. The setup includes a large red vertical mast (Experimental substructure) with a spring and damper assembly. A force sensor is attached to the top of the mast. A displacement sensor is mounted on a horizontal beam. An actuator is visible on the left side of the setup.](67af94a7c462e85f3a310c9a45c0980d_img.jpg)

Photograph of the experimental equipment and experimental substructure. The setup includes a large red vertical mast (Experimental substructure) with a spring and damper assembly. A force sensor is attached to the top of the mast. A displacement sensor is mounted on a horizontal beam. An actuator is visible on the left side of the setup.

Fig. 11. Experimental equipment and experimental substructure.

counterweights and a spring. To obtain more accurate force feedback, a force sensor is placed between the experimental substructure and the actuator.

## 4.2. Delay compensation performance tests for predefined loading targets

### 4.2.1. Displacement response

To ensure the safety of the tests and validate the feasibility of the method in hybrid tests, delay compensation performance tests for predefined loading targets were conducted. Compared with RTHT in Fig. 6, the delay compensation performance tests have no numerical substructure. Figures 12–14 display the desired command and displacement time-history curves under various excitations, including sine wave, EL-Centro earthquake and band-limited white noise with a 20 Hz cutoff frequency. These curves compare the desired command and the actuator displacement responses using the BPNN-SM method, ATS method, adaptive discrete model method (ADM), SMC method and no compensation method. It is evident that the actual actuator displacement responses closely match the desired commands

![Figure 12: Comparison between desired command and actuator displacement responses under sine wave excitation. The figure consists of three subplots: (a) shows a long-term time-history plot from 0 to 45 seconds, demonstrating that all compensation methods (SMC, ATS, ADM, BPNN-SM) closely follow the desired command (blue line) and significantly outperform the 'No comp.' (black line) case. (b) and (c) are zoomed-in views of specific time intervals (7.75–7.9 s and 34.9–35.1 s, respectively), further illustrating the high tracking accuracy of the proposed methods compared to the un-compensated response.](c531b0e7e06671c980f2ed0d753d2fbc_img.jpg)

Figure 12: Comparison between desired command and actuator displacement responses under sine wave excitation. The figure consists of three subplots: (a) shows a long-term time-history plot from 0 to 45 seconds, demonstrating that all compensation methods (SMC, ATS, ADM, BPNN-SM) closely follow the desired command (blue line) and significantly outperform the 'No comp.' (black line) case. (b) and (c) are zoomed-in views of specific time intervals (7.75–7.9 s and 34.9–35.1 s, respectively), further illustrating the high tracking accuracy of the proposed methods compared to the un-compensated response.

Fig. 12. Comparison between desired command and actuator displacement responses under sine wave excitation.



![Figure 13: Comparison between desired command and actuator displacement responses under band-limited white noise excitation. (a) Long-term response (0-45s), (b) Zoomed-in response (14.08-14.26s), (c) Zoomed-in response (38.6-38.8s).](f8630b0582d6e5b1d81f877880ef0dda_img.jpg)

Figure 13 consists of three subplots (a), (b), and (c) comparing the displacement response (mm) over time (s) for six methods: No comp. (black solid line), Desire comm. (blue solid line), SMC (green dashed line), ATS (orange dashed line), ADM (pink dashed line), and BPNN-SM (red solid line). The y-axis for all plots is 'Displacement/mm' and the x-axis is 'Time/s'.

- (a) Long-term response (0 to 45 seconds). The y-axis ranges from -0.5 to 0.5. The 'No comp.' and 'Desire comm.' lines show high-frequency noise around ±0.25 mm. The 'SMC', 'ATS', 'ADM', and 'BPNN-SM' lines are tightly clustered around the zero line, with 'BPNN-SM' showing the lowest noise level.
- (b) Zoomed-in response (14.08 to 14.26 seconds). The y-axis ranges from -0.1 to 0.15. The 'No comp.' and 'Desire comm.' lines show a peak around 0.15 mm. The 'SMC', 'ATS', 'ADM', and 'BPNN-SM' lines follow the 'Desire comm.' line very closely, with 'BPNN-SM' being the most accurate.
- (c) Zoomed-in response (38.6 to 38.8 seconds). The y-axis ranges from -0.2 to 0.3. The 'No comp.' and 'Desire comm.' lines show a peak around 0.25 mm. The 'SMC', 'ATS', 'ADM', and 'BPNN-SM' lines follow the 'Desire comm.' line very closely, with 'BPNN-SM' being the most accurate.

Figure 13: Comparison between desired command and actuator displacement responses under band-limited white noise excitation. (a) Long-term response (0-45s), (b) Zoomed-in response (14.08-14.26s), (c) Zoomed-in response (38.6-38.8s).

Fig. 13. Comparison between desired command and actuator displacement responses under band-limited white noise excitation.

when using the BPNN-SM compensation method. Additionally, compared to the other cases, the BPNN-SM method provides a more consistent actuator displacement response with the desired command. The results indicate that the proposed BPNN-SM method can be safely applied in hybrid tests, offering high compensation accuracy and robustness.

### 4.2.2. Evaluation criteria values

Table 3 summarizes the comparison of evaluation criteria values  $J_1 - J_3$  for various time delay compensation methods under four types of excitations in the delay compensation performance tests for predefined loading targets. The bold values serve as a visual indicator of optimal performance in time delay compensation and hybrid testing accuracy. In Table 3, the errors between the desired command and actuator displacement response are compared for each time delay compensation method. The SMC method has the poorest compensation performance. For instance, under El-Centro earthquake excitation, the time delay  $J_1$  between the desired command and actuator displacement response reached 20.5 ms, with root mean square error

![Figure 14: Comparison between desired command and actuator displacement responses under El-Centro earthquake excitation. (a) Long-term displacement response (0-45s). (b) Zoomed-in view of the first peak (5.56-5.72s). (c) Zoomed-in view of the second peak (26-26.2s).](ed75e80b1e08237f7e90b65357de84d5_img.jpg)

Figure 14 consists of three subplots (a), (b), and (c) comparing displacement responses over time. The legend for all plots is: No comp. (black solid line), Desire comm. (blue solid line), SMC (green dashed line), ATS (red dashed line), ADM (purple dashed line), and BPNN-SM (red solid line).

- (a) Long-term displacement response (0 to 45 seconds). The y-axis is Displacement/mm (-3 to 4) and the x-axis is Time/s (0 to 45). The BPNN-SM method (red solid line) closely follows the desired command (blue solid line), while other methods show significant oscillations and larger errors.
- (b) Zoomed-in view of the first peak (5.56 to 5.72 seconds). The y-axis is Displacement/mm (0.5 to 2) and the x-axis is Time/s (5.56 to 5.72). The BPNN-SM method (red solid line) shows the smallest error between the desired command (blue solid line) and the actuator response.
- (c) Zoomed-in view of the second peak (26 to 26.2 seconds). The y-axis is Displacement/mm (-0.5 to 1.5) and the x-axis is Time/s (26 to 26.2). The BPNN-SM method (red solid line) again shows the best tracking performance, closely following the desired command (blue solid line).

Figure 14: Comparison between desired command and actuator displacement responses under El-Centro earthquake excitation. (a) Long-term displacement response (0-45s). (b) Zoomed-in view of the first peak (5.56-5.72s). (c) Zoomed-in view of the second peak (26-26.2s).

Fig. 14. Comparison between desired command and actuator displacement responses under El-Centro earthquake excitation.

$J_2$  and peak error  $J_3$  of 47.59% and 80.31%, respectively, representing the largest errors among all methods. When the SMC method is combined with BPNN, significant improvements in time delay compensation are achieved. For El-Centro excitation, the BPNN-SM method shows the best compensation performance compared to other methods, with a time delay  $J_1$  of 0 ms between desired command and actuator displacement response, and root mean square error  $J_2$  and peak error  $J_3$  of 16.59% and 40.96%, respectively, the smallest among all methods. The BPNN-SM method shows relatively small errors between the desired command and actuator displacement responses under the excitations, indicating its high compensation accuracy and robustness in experimental applications.

Among them, when the SMC method is adopted alone, its  $J_1$  index value is relatively large and close to the result of the non-compensation scheme. This is because the SMC feedback controller designed in this study mainly targets system uncertainties, and its core objective is to enhance robustness rather than directly compensate for time delays. Therefore, SMC can only partially offset the time delay

Table 3. Quantitative analysis index of delay compensation performance tests.

| External command                    | Time delay compensation method | $J_1$ (ms) | $J_2$ (%)    | $J_3$ (%)    |
|-------------------------------------|--------------------------------|------------|--------------|--------------|
| Sine wave excitation                | No compensation                | 30.3       | 71.26        | 129.32       |
|                                     | SMC                            | 26.4       | 50.60        | 84.03        |
|                                     | ATS                            | 14.6       | 39.65        | 92.78        |
|                                     | ADM                            | 1          | 9.49         | 78.68        |
|                                     | BPNN-SM                        | <b>0</b>   | <b>7.50</b>  | <b>75.25</b> |
| Band-limited white noise excitation | No compensation                | 27.3       | 138.94       | 144.43       |
|                                     | SMC                            | 25.4       | 79.87        | 112.64       |
|                                     | ATS                            | <b>1</b>   | 70.75        | 83.53        |
|                                     | ADM                            | 3.9        | 90.1         | 89.46        |
|                                     | BPNN-SM                        | 2          | <b>34.19</b> | <b>56.55</b> |
| El-Centro earthquake excitation     | No compensation                | 21.5       | 62.20        | 102.23       |
|                                     | SMC                            | 20.5       | 47.59        | 80.31        |
|                                     | ATS                            | 4.9        | 40.98        | 56.86        |
|                                     | ADM                            | 10.7       | 30.79        | 53.47        |
|                                     | BPNN-SM                        | <b>0</b>   | <b>16.59</b> | <b>40.96</b> |

effect, resulting in limited improvement to  $J_1$ . However, in  $J_2$  and  $J_3$ , SMC performs better than the uncompensated method. The SMC controller can still maintain the stable operation of the RTHT system in the case of significant time delay with limited white noise and El-Centro earthquake excitations. This is mainly attributed to the inherent characteristic of SMC as a nonlinear control method, which can effectively deal with system uncertainties and external disturbances.

It should be pointed out that the excitation signals used to train the BPNN are different from those of the sine wave, band-limiting white noise and El-Centro earthquake excitation used in the tests of this section. As shown in Table 3, the BPNN-SM method demonstrates excellent compensation performance under these offset excitations, generally outperforming other methods in  $J_1$ ,  $J_2$  and  $J_3$  metrics. This preliminarily verifies the method's adaptability and robustness to complex signals different from the training excitations.

## 4.3. RTHT validation

### 4.3.1. Displacement response

To further verify the effectiveness of BPNN-SM in RTHT and the reliability of the test results, this section compares the actual displacement of the experimental substructure in the RTHT with the displacement of the reference model. Figures 15 and 16 show the displacement time-history curves under El-Centro earthquake excitation and band-limited white noise with a 20 Hz cutoff frequency using different time delay compensation methods, along with the reference displacement. The displacement response obtained from exciting the entire structural model is taken as the reference displacement. These curves compare the

![Figure 15: Comparison between reference displacement and experimental substructure displacement under El-Centro earthquake excitation. (a) Time history plot from 0 to 45 seconds. (b) Zoomed-in plot from 6.75 to 7.05 seconds. (c) Zoomed-in plot from 21 to 21.35 seconds. The legend for all plots is: Reference (solid blue line), SMC (dashed green line), ATS (dashed red line), ADM (dashed magenta line), and BPNN-SM (solid red line).](df0685d2d1176d617ed1e642de4e5425_img.jpg)

Figure 15 consists of three subplots (a), (b), and (c) comparing the displacement responses of five methods: Reference (solid blue line), SMC (dashed green line), ATS (dashed red line), ADM (dashed magenta line), and BPNN-SM (solid red line). The y-axis for all plots is 'Displacement/mm' and the x-axis is 'Time/s'.

- (a) A time history plot from 0 to 45 seconds. The displacement fluctuates between approximately -1.0 and 1.0 mm. The BPNN-SM method (solid red line) closely follows the reference (solid blue line) throughout the entire duration.
- (b) A zoomed-in plot from 6.75 to 7.05 seconds. The displacement is positive, peaking around 0.25 mm. The BPNN-SM method (solid red line) tracks the reference (solid blue line) very closely, while the other methods (SMC, ATS, ADM) show some deviation.
- (c) A zoomed-in plot from 21 to 21.35 seconds. The displacement is positive, peaking around 0.3 mm. The BPNN-SM method (solid red line) tracks the reference (solid blue line) very closely, while the other methods (SMC, ATS, ADM) show some deviation.

Figure 15: Comparison between reference displacement and experimental substructure displacement under El-Centro earthquake excitation. (a) Time history plot from 0 to 45 seconds. (b) Zoomed-in plot from 6.75 to 7.05 seconds. (c) Zoomed-in plot from 21 to 21.35 seconds. The legend for all plots is: Reference (solid blue line), SMC (dashed green line), ATS (dashed red line), ADM (dashed magenta line), and BPNN-SM (solid red line).

Fig. 15. Comparison between reference displacement and experimental substructure displacement under El-Centro earthquake excitation.

displacement responses using the BPNN-SM, ATS, ADM and SMC time delay compensation methods with the reference displacement. As can be seen from Figs. 15 and 16, after using the BPNN-SM compensation method, the actuator's actual displacement response is very close to the reference displacement response. Moreover, compared to the SMC, ATS and ADM methods, the BPNN-SM method's actual displacement response curve is more consistent with the reference displacement curve, better tracking the response of the overall model. The results demonstrate that the proposed BPNN-SM method has higher compensation accuracy and robustness in RTHT and validates the reliability of the RTHT results presented in this study.

### 4.3.2. Evaluation criteria values

Table 4 summarizes the comparison of evaluation metrics  $J_1 - J_5$  under several time delay compensation methods using El-Centro earthquake excitation and band-limited white noise excitation with a 20 Hz cutoff frequency. In Table 4, the SMC method has the poorest compensation performance. For example, under El-Centro earthquake excitation, the time delay  $J_1$  between the SMC method's experimental

![Figure 16: Comparison between reference displacement and experimental substructure displacement under band-limited white noise excitation. (a) Time-domain plot showing displacement (mm) vs. time (s) from 0 to 45s. (b) Zoomed-in plot from 5.6 to 5.9s. (c) Zoomed-in plot from 20.65 to 20.95s. All plots compare Reference (blue solid line), SMC (green dashed line), ATS (pink dash-dot line), ADM (red dashed line), and BPNN-SM (red solid line).](1d3994bfe548ae7545d57df703e32a02_img.jpg)

Figure 16 consists of three subplots (a), (b), and (c) comparing the performance of five time delay compensation methods under band-limited white noise excitation. The methods are: Reference (blue solid line), SMC (green dashed line), ATS (pink dash-dot line), ADM (red dashed line), and BPNN-SM (red solid line).

- Subplot (a):** A time-domain plot showing Displacement (mm) on the y-axis (ranging from -3 to 3) versus Time (s) on the x-axis (ranging from 0 to 45). The plot shows high-frequency oscillations. The BPNN-SM method (red solid line) closely follows the Reference signal (blue solid line), while the other methods show significant deviation.
- Subplot (b):** A zoomed-in view of the displacement response from 5.6 to 5.9 seconds. The y-axis ranges from -0.5 to 1.5 mm. The BPNN-SM method (red solid line) shows the best tracking performance, closely following the Reference signal (blue solid line).
- Subplot (c):** A zoomed-in view of the displacement response from 20.65 to 20.95 seconds. The y-axis ranges from -0.2 to 1.2 mm. The BPNN-SM method (red solid line) again shows the best tracking performance, closely following the Reference signal (blue solid line).

Figure 16: Comparison between reference displacement and experimental substructure displacement under band-limited white noise excitation. (a) Time-domain plot showing displacement (mm) vs. time (s) from 0 to 45s. (b) Zoomed-in plot from 5.6 to 5.9s. (c) Zoomed-in plot from 20.65 to 20.95s. All plots compare Reference (blue solid line), SMC (green dashed line), ATS (pink dash-dot line), ADM (red dashed line), and BPNN-SM (red solid line).

Fig. 16. Comparison between reference displacement and experimental substructure displacement under band-limited white noise excitation.

substructure response and the desired command reached 24.4 ms, with the RMSE  $J_2$  and peak error  $J_3$  between the experimental substructure and the target signal being 30.78% and 53.64%, respectively, the largest among all time delay compensation methods. However, when the SMC method is combined with the BPNN, the time delay compensation performance is significantly improved. For instance, under band-limited white noise excitation, the BPNN-SM method achieves the best compensation effect compared to other compensation methods, with a time delay  $J_1$  of 9.8 ms, and RMSE  $J_2$  and peak error  $J_3$  of 11.49% and 9.07%, respectively. The ADM method can effectively compensate for time delays. For example, under El-Centro earthquake excitation, the time delay  $J_1$  is 0 ms, but the amplitude compensation is insufficient. The ADM method's response is generally slightly lower than the desired command throughout the process, resulting in a slightly higher RMSE  $J_2$  of 16.91%. In contrast to the ADM method, the BPNN-SM method does not require parameter identification in the early stages, allowing for stable compensation in the early test stages and resulting in the smallest peak error  $J_3$ . This indicates that the BPNN-SM method achieves higher compensation accuracy and robustness in RTHHT.

Table 4. Quantitative analysis index of RTHT.

| External command                    | Time delay compensation method | $J_1$ (ms) | $J_2$ (%)    | $J_3$ (%)    | $J_4$ (%)    | $J_5$ (%)    |
|-------------------------------------|--------------------------------|------------|--------------|--------------|--------------|--------------|
| Band-limited white noise excitation | SMC                            | 29.3       | 35.65        | 34.07        | 36.85        | 35.54        |
|                                     | ATS                            | 13.7       | 18.6         | 14.85        | 19.43        | 17.43        |
|                                     | ADM                            | 0          | 17.21        | 13.52        | 21.26        | 17.08        |
|                                     | BPNN-SM                        | 3.7        | <b>14.06</b> | <b>11.92</b> | <b>14.12</b> | <b>14.99</b> |
| El-Centro earthquake excitation     | SMC                            | 24.4       | 30.78        | 53.64        | 31.9         | 32.53        |
|                                     | ATS                            | 8.8        | 13.68        | 27.39        | 11.87        | 10.95        |
|                                     | ADM                            | 0          | 16.91        | 21.04        | 21.48        | 22.05        |
|                                     | BPNN-SM                        | 3.8        | <b>11.49</b> | <b>9.07</b>  | <b>7.73</b>  | <b>8.04</b>  |

Table 4 compares the RMSE  $J_4$  and peak tracking error  $J_5$  between the reference displacement and the experimental substructure displacement for each time delay compensation method. Except for the SMC method, the errors of the other methods are all below 23%, indicating that the test results meet the requirements of RTHT. Among them, the BPNN-SM method exhibits the lowest RMSE  $J_4$  and peak tracking error  $J_5$  for the experimental substructure response. For instance, under band-limited white noise excitation, the RMSE  $J_4$  and peak tracking error  $J_5$  of the BPNN-SM method are 14.12% and 14.99%, respectively, both lower than those of other compensation methods, demonstrating the high accuracy of the BPNN-SM method's RTHT results. Under the excitation of band-limited white noise, the ATS method predicts future states through polynomial extrapolation. Although it introduces a 13.7 ms delay, it better adapts to the nonlinear dynamics of the system, making  $J_4$  and  $J_5$  superior to ADM. Seismic excitation, with its specific spectral characteristics and strong non-stationary transient features, exacerbates the model mismatch problem of ADM. The high-precision models of ATS in capturing key nonlinear and transient responses are significantly superior to those of ADM. The final performance is that the overall performance indicators of  $J_2$  to  $J_5$  are superior to those of  $J_1$ , which is “0 ms”, but the model accuracy is relatively low.

Similar to Sec. 4.2.2, the excitation used in this RTHT is also different from the excitation signal used in training the BPNN model. As shown in Table 4, the BPNN-SM method not only performs excellently in compensating for performance indicators  $J_1$ ,  $J_2$  and  $J_3$  when dealing with these unseen complex excitations, but also has RTHT results  $J_4$  and  $J_5$  that are closest to the reference model, significantly outperforming other comparison methods. This further confirms the effective compensation ability of the BPNN-SM method for different types of incentives outside the training data range and the robustness of the overall system.

# 5. Conclusion

To better address the nonlinearity and uncertainty inherent in RTHT systems, this study combines BPNN with sliding mode. The sliding mode, as feedback controller

of the loading system, improves the robustness and compensates for part of the time delay. BPNN is used as the inverse compensation to compensate for the residual time delay and improve robustness further. The effectiveness and robustness of the BPNN-SM are validated through delay compensation performance tests for predefined loading targets and RTHT on an SDOF structure, and the conclusions are as follows:

- (1) The results of delay compensation performance tests for predefined loading targets show that integrating sliding mode with the BPNN significantly improves time delay compensation performance. Compared to other time delay compensation methods, the BPNN-SM method exhibits smaller evaluation criteria values  $J_1 - J_3$  in most cases, indicating the delay compensation accuracy and control robustness, preliminarily.
- (2) The RTHT results indicate that  $J_1 - J_5$ , except for a slightly larger value of criterion  $J_1$  compared to the ADM method, the values of criteria  $J_2 - J_5$  for the BPNN-SM method are all smaller than ATS, ADM and SMC compensation methods. The results further demonstrate that the BPNN-SM method exhibits high time delay compensation accuracy and control robustness in RTHT, and its results are more reliable.
- (3) The input excitation used for training the BPNN is different from that used in actual delay compensation performance tests and RTHT. The test results obtained under these different excisions prove the feasibility of the BPNN-SM method and its certain generalization ability. Results demonstrate that combining BPNN with sliding mode enables accurate compensation for a variety of complex excitations beyond the range of the training dataset in practical applications and has strong robustness.

# Acknowledgments

The authors thank the National Key Research and Development Program (2022YFC3801201), the National Natural Science Foundation of China (51878630, 52378142, 52078398), the Natural Science Foundation of Guangdong Province (2022A1515010500), the Tertiary Education Scientific Research Project of Guangzhou Municipal Education Bureau (Grant No. 2024312283), Youth Innovation Talent Program for Ordinary Universities in Guangdong Province (Grant No. 2024KQNCX099) and Guangdong Basic and Applied Basic Research Foundation (Grant No. 2025A1515012839).

# ORCID

Yuekun Shangguan ![ORCID icon](675ef7f53d3bd4a69f2bfe6acc6c2026_img.jpg) <https://orcid.org/0009-0002-2667-6407>

Huimeng Zhou ![ORCID icon](ab38aa34d7fd9612c4ea4d0692132800_img.jpg) <https://orcid.org/0000-0001-9738-9427>

# References

1. M. Nakashima, H. Kato and E. Takaoka, Development of real - time pseudo dynamic testing, *Earthq. Eng. Struct. Dyn.* **21**(1) (1992) 79–92.
2. W. Huang *et al.*, A novel actuation dynamics adaptive compensation strategy for realtime hybrid simulation based on unscented Kalman filter, *Int. J. Struct. Stab. Dyn.* **23**(10) (2023) 2350107.
3. G. Xu *et al.*, A real-time hybrid simulation method for vehicle-bridge interaction systems considering vehicle jumping, *Int. J. Struct. Stab. Dyn.* **24**(12) (2023) 2450129.
4. Y. Liu *et al.*, Implementation and verification of real-time hybrid simulation for the dynamic performance assessment of base-isolated structures, *Int. J. Struct. Stab. Dyn.* **24**(9) (2023) 2450091.
5. G. Xu *et al.*, A real-time hybrid testing method based on partial restart loading technology, *Int. J. Struct. Stab. Dyn.* **26**(26) (2025) 2650264.
6. T. Horiuchi *et al.*, Real-time hybrid experimental system with actuator delay compensation and its application to a piping system with energy absorber, *Earthq. Eng. Struct. Dyn.* **28**(10) (1999) 1121–1141.
7. M. Nakashima and N. Masaoka, Real-time on-line test for MDOF systems, *Earthq. Eng. Struct. Dyn.* **28**(4) (1999) 1–23.
8. Y. Chae, K. Kazembidokhti and J. M. Ricles, Adaptive time series compensator for delay compensation of servo-hydraulic actuator systems for real-time hybrid simulation, *Earthq. Eng. Struct. Dyn.* **42**(11) (2013) 1697–1715.
9. P. Alejandro and G. Marianonieta, Adaptive tracking control for real-time hybrid simulation of structures subjected to seismic loading, *Mech. Syst. Signal Process.* **134**(12) (2019) 106345.
10. H. Yao, P. Tan, T. Yang and F. Zhou, Acceleration-based sliding mode hierarchical control algorithm for shake table tests, *Earthq. Eng. Struct. Dyn.* **50**(13) (2021) 3670–3691.
11. X. Zheng, H. Yao and P. Tan, A discrete fractional sliding mode control algorithm for vibration mitigation of building structures considering nonlinearities and uncertainties, *Int. J. Struct. Stab. Dyn.* **26**(27) (2025) 2650277.
12. D. Xu *et al.*, Performance study of sliding mode controller with improved adaptive polynomial-based forward prediction, *Mech. Syst. Signal Process.* **133**(1) (2019) 106263.
13. X. Ning *et al.*, Robust actuator dynamics compensation method for real-time hybrid simulation, *Mech. Eng. Signal Process.* **131**(15) (2019) 49–70.
14. B. Wu and H. Zhou, Sliding mode for equivalent force control in real-time substructure testing, *Struct. Control Health Monit.* **21**(10) (2014) 1284–1303.
15. N. Rajabi, H. A. Abolmasoumi and M. Soleymani, Sliding mode trajectory tracking control of a ball-screw-driven shake table based on online state estimations using EKF/UKF, *Struct. Control Health Monit.* **25**(4) (2018) 2133.
16. H. Li *et al.*, Sliding mode control design for the benchmark problem in real-time hybrid simulation, *Mech. Syst. Signal Process.* **151** (2021) 107364.
17. J. E. Carrion and B. F. Spencer, Real-time hybrid testing using model-based delay compensation, *Smart Struct. Syst.* **4**(6) (2006) 809–828.

18. B. M. Philips and B. F. Spencer, Model-based feedforward-feedback tracking control for real-time hybrid simulation, *J. Struct. Eng.* **139**(7) (2011) 1205–1214.
19. A. G. Femandois, Application of model-based compensation methods to real-time hybrid simulation benchmark, *Mech. Syst. Signal Process.* **131** (2019) 394–416.
20. C. Chen, J. Ricles, R. Sause and R. Christenson, Experimental evaluation of an adaptive inverse compensation technique for real-time simulation of a large-scale magnetorheological fluid damper, *Smart Mater. Struct.* **19**(2) (2010) 25–17.
21. P. Chen *et al.*, Dual compensation strategy for real-time hybrid testing, *Earthq. Eng. Struct. Dyn.* **35**(2) (2013) 1–23.
22. G. Ou *et al.*, Robust integrated actuator control: Experimental verification and real time hybrid — simulation implementation, *Earthq. Eng. Struct. Dyn.* **44**(3) (2015) 441–460.
23. W. Xu, T. Guo and C. Chen, Comparison of delay compensation methods for real-time hybrid simulation using frequency-domain evaluation index, *Earthq. Eng. Eng. Vib.* **15**(1) (2016) 129–143.
24. K. Cheon *et al.*, On replacing PID controller with deep learning controller for DC motor system, *J. Autom. Control Eng.* **3**(6) (2015) 452–456.
25. W. Mucha, Application of artificial neural networks in hybrid simulation, *Appl. Sci.* **9**(21) (2019) 4495.
26. J. Wu, R. Zhang and M. B. Phillips, Structural seismic resilience evaluation through real-time hybrid simulation with online learning neural networks, *Int. J. Lifecycle Perform. Eng.* **4**(1–3) (2020) 184–214.
27. E. Bas and M. Moustafa, Communication development and verification for python-based machine learning models for real-time hybrid simulation, *Front. Built Environ.* **6** (2020) 574965.
28. Y. Xu, Y. Fei, Y. Tian and X. Lu, Advanced corrective training strategy for surrogating complex hysteretic behavior, *Structures* **41** (2022) 1792–1803.
29. Y. Tian *et al.*, Real-time model calibration with deep reinforcement learning, *Mech. Syst. Signal Process.* **165**(3) (2022) 108284.
30. W. Guo *et al.*, Research on numerical solution algorithm for real-time hybrid simulation of high-speed railway on suspension bridge, *Earthq. Eng. Resil.* **1**(3) (2022) 336–349.
31. Z. Zhou *et al.*, Real-time hybrid simulation incorporating machine learning for deep-water bridges subjected to seismic ground motion with fluid-structure dynamic interaction, *Soil Dyn. Earthq. Eng.* **175**(1) (2023) 108263.
32. C. Chen *et al.*, Experimental evaluation of low fidelity models on co-kriging meta-modeling of global structural response through real-time hybrid simulation, *J. Struct. Eng.* **149**(4) (2023) 11352.
33. Z. Tang *et al.*, Implementation of shaking table based offline hybrid testing through neural networks, *Structures* **48** (2023) 21–30.
34. G. Yu, C. Chen, H. Hou, C. Peng and R. Zhang, Integrating adaptive kriging with expansion optimal linear estimation into real-time hybrid simulation for time-variant experimental analysis of structures with deterioration, *J. Build. Eng.* **64** (2023) 105658.
35. P. Chen, S. Hsu and C. Ma, Development and verification of real-time hybrid simulation with deep learning-based nonlinear numerical substructure, *Earthq. Eng. Struct. Dyn.* **53**(6) (2024) 2141–2161.
36. P. Chen, C. Chou and W. Wang, Rapid controller generation for vibration suppression of structures using direct excitation with machine learning, *J. Struct. Eng.* **150**(3) (2024) 101–112.

37. A. Subaihawi *et al.*, Real-time hybrid simulation of structural systems with soil-foundation interaction effects using neural networks, *Earthq. Eng. Struct. Dyn.* **53**(15) (2024) 4688–4718.
38. G. Yu *et al.*, A novel global prediction framework for multi-response models in reliability engineering using adaptive sampling and active subspace methods, *Comput. Methods Appl. Mech. Eng.* **433**(PA) (2025) 117506.
39. N. Li *et al.*, Reinforcement learning control method for real-time hybrid simulation based on deep deterministic policy gradient algorithm, *Struct. Control Health Monit.* **29** (2022) 3035.
40. Z. Lai, Y. Liu, Z. Zhai and J. Zhang, Adaptive compensation using long short-term memory networks for improved control performance in real-time hybrid simulation, *Comput.-Aided Civ. Infrastruct. Eng.* **40**(9) (2024) 13378.
41. A. Nino *et al.*, Deep reinforcement learning-based control for real-time hybrid simulation of civil structures, *Int. J. Robust Nonlinear Control* **0** (2025) 1–14.
42. H. Yao *et al.*, Deep reinforcement learning-based active mass driver decoupled control framework considering control-structure interaction effects, *Comput.-Aided Civ. Infrastruct. Eng.* **39**(11) (2024) 1573–1596.
43. D. E. Rumelhart, G. E. Hinton and R. J. Williams, Learning representations by back-propagating errors, *Nature* **323**(6088) (1986) 533–536.
44. T. Hegazy, P. Fazio and O. Moselhi, Developing practical neural network applications using back-propagation, *Comput.-Aided Civ. Infrastruct. Eng.* **9**(2) (1994) 145–159.
45. J. J. Moré, The Levenberg-Marquardt algorithm: Implementation and theory, *Lect. Notes Math.* **630** (1978) 105–106.
46. E. C. Silva *et al.*, Benchmark control problem for real-time hybrid simulation, *Mech. Syst. Signal Process.* **135** (2020) 106381.
47. H. Zhou, X. Shao and J. Zhang, Real-time hybrid model test to replicate high-rise building resonant vibration under wind loads, *Thin-Walled Struct.* **197** (2024) 111559.
48. J. Tang, J. Zhang and H. Zhou, Exploring the abnormal vibration of SEG Plaza via wind-tunnel substructure hybrid simulation, *J. Build. Eng.* **98** (2024) 111372.