

PAPER • **OPEN ACCESS**

# Study on Composite Control Strategy of Transient Air-Fuel Ratio for Gasoline Engine Based on Model

To cite this article: Dandan Song and Yuelin Li 2020 *IOP Conf. Ser.: Earth Environ. Sci.* **513** 012027

View the [article online](#) for updates and enhancements.

You may also like

- [Techniques for measurement of oxygen and air-to-fuel ratio using zirconia sensors. A review](#)  
M Benammar
- [Predictive Control Of Transient Air-Fuel Ratio for Gasoline Engine Based on Wavelet Network Inversion](#)  
Dandan Song and Yuelin Li
- [Monitoring the air-fuel ratio of internal combustion engines using a neural network](#)  
S D Walters, M M De Zoysa and R J Howlett

# Study on Composite Control Strategy of Transient Air-Fuel Ratio for Gasoline Engine Based on Model

**Dandan Song<sup>1\*</sup>, Yuelin Li<sup>2</sup>**

<sup>1</sup> College of Automobile and Mechanical Engineering, Changsha University of Science Technology, Changsha 410076, China

<sup>2</sup> Henan Communication Vocational and Technical College, Institute of Automobile Engineering, Zhengzhou, 450005, China

\*Corresponding author's e-mail: sdd122@163.com

**Abstract.** The control accuracy of transient air-fuel ratio of gasoline engine is a difficult problem in the current engine control system. To achieve effective control of transient air-fuel ratio for gasoline engines, a composite control method is proposed, which consists of inverse model feedforward based on least squares support vector machine(LS-SVM)and feedback control with model-free adaptive control(MFAC).Feedforward control can accurately estimate the intake air volume in the cylinder. Neither feedforward or feedback control can achieve better control results. A composite control strategy based on feedforward + feedback is proposed. The feedforward model is used to perform dynamic feedforward compensation of the intake air amount in the transient air-fuel ratio, and in combination with feedback control, the air-fuel ratio is feedback-controlled by modifying the fuel injection amount, and system disturbances and errors are corrected. In this paper, two composite control strategies are designed for the air-fuel ratio of the engine under transient conditions. The results show that the inverse model based on LS-SVM can accurately approximate the air fuel ratio transient process, and this method has stronger robustness and anti-interference combined the MFAC feedback control. Therefore, the composite control strategy has good control performances and can improve the control precision of air-fuel ratio in transient conditions.

## 1. Introduction

Air fuel ratio is an important indicator of engine emission, economy and power. Due to the measurement deviation of air intake, dynamic transmission characteristics of oil film and hysteresis of oxygen feedback signal, there is a large deviation in air-fuel ratio control in engine transient condition, which affects the accuracy of air-fuel ratio control under transient conditions[1][2]. In recent years, many scholars have studied the air fuel ratio system in gasoline engine, which are mainly focused on feedforward or feedback control[3]. Feed forward control can accurately estimate the air intake in the cylinder, such as the estimation of the intake volume in the cylinder by using the state observer as the feedforward control[4]. In order to realize the effective control of air fuel ratio system, neural network is used as feedforward control in the literature, the fuel injection rate of air-fuel ratio system is compensated[5]. For feedback control, the main purpose is to correct the error of air-fuel ratio control system[6]. The main research methods are PID, fuzzy control, etc[7]. But a single feedforward or feedback control can not achieve a better control effect for the transient air fuel ratio[8]. Therefore, in order to effectively control the transient air fuel ratio, a compound control strategy based on the inverse model feedforward control plus adaptive feedback control is proposed in this paper. The intake

![Creative Commons Attribution 3.0 licence logo](96fb4373e63be843d9d2dcac2260afff_img.jpg)

The image shows the Creative Commons Attribution 3.0 licence logo, which consists of two circular icons: one with 'cc' and another with a person symbol, followed by the text 'BY'.

Creative Commons Attribution 3.0 licence logo

Content from this work may be used under the terms of the [Creative Commons Attribution 3.0 licence](#). Any further distribution of this work must maintain attribution to the author(s) and the title of the work, journal citation and DOI.

air quantity measurement deviation, first using least squares support vector machine (LS-SVM) to establish the air-fuel ratio system of inverse model, dynamic feedforward compensation than the air intake in the model of transient burning empty, and combined with model free adaptive feedback control (MFAC), by modifying the fuel injection quantity of the air-fuel ratio feedback control system of disturbance and error correction. Finally, the LS-SVM inverse model is tested and the transient air fuel ratio inverse model is used to test the air fuel ratio output of the transient process and compare with the measured value of the bench. And the composite control strategy proposed in this paper is simulated and analyzed by using the transient test data. The results show that the LS-SVM inverse model can accurately approach the transient process of air fuel ratio, and improve the robustness and anti-interference ability of the system with the combination of MFAC feedback control. The compound control strategy can be realized and is suitable for the precise control of the air-fuel ratio in the transient state of the engine.

## 2. General idea

The transient air fuel ratio control system adopts the compound control strategy of the inverse model feedforward control and the additional adaptive feedback control. Least squares support vector machine (LS-SVM) is applied to establish the inverse model of air-fuel ratio system. Dynamic feedforward compensation is carried out for the intake air volume in the transient air-fuel ratio model, combined with MFAC feedback control, the system disturbance and error are corrected. The control frame of the transient air fuel ratio system is shown in Figure 1.

![Figure 1: Control block diagram of transient air fuel ratio system. The diagram shows a feedback loop. The setpoint y_d is fed into an LS-SVM block (G_f) and a summing junction. The output of G_f is u_f. The output of the summing junction is u, which is fed into an 'Object' block (P). The 'Object' block also receives disturbance d_k. The output of the 'Object' block is y. The output y is fed back through a TDL (Time Delay Line) block and a summing junction to produce u_c. The output u_c is fed into an MFAC block (G_c). The output of G_c is fed back into the summing junction. Figure 2: Structure diagram of air fuel ratio inverse model identification. This diagram shows the LS-SVM block receiving inputs u(k), u(k-1), ..., u(k-m) and d(k), d(k-1), ..., d(k-m) from TDL blocks. The output of the LS-SVM block is u(k).](2df09d249c38abee55dbf0526dd6da0a_img.jpg)

Figure 1: Control block diagram of transient air fuel ratio system. The diagram shows a feedback loop. The setpoint y\_d is fed into an LS-SVM block (G\_f) and a summing junction. The output of G\_f is u\_f. The output of the summing junction is u, which is fed into an 'Object' block (P). The 'Object' block also receives disturbance d\_k. The output of the 'Object' block is y. The output y is fed back through a TDL (Time Delay Line) block and a summing junction to produce u\_c. The output u\_c is fed into an MFAC block (G\_c). The output of G\_c is fed back into the summing junction. Figure 2: Structure diagram of air fuel ratio inverse model identification. This diagram shows the LS-SVM block receiving inputs u(k), u(k-1), ..., u(k-m) and d(k), d(k-1), ..., d(k-m) from TDL blocks. The output of the LS-SVM block is u(k).

Figure 1 control block diagram of transient air fuel ratio system

Figure 2 structure diagram of air fuel ratio inverse model identification

In Figure 1,  $G_f$  is the feedforward controller,  $G_c$  is the feedback controller,  $y_d$  is the expected output of the system,  $u_f$  is the feed forward control rate,  $u_c$  is the feedback control rate,  $d_k$  is the disturbance of control object, and the feedforward controller  $G_f$  is the inverse model of the controlled object.

## 3. Model identification based on LS-SVM

### 3.1 Transient Air Fuel Ratio Model

The actual air fuel ratio  $\lambda$  is the ratio of air mass  $m_{ac}$  to the fuel mass  $m_{fc}$  per cycle into the cylinder[9], that is,  $\lambda = \frac{m_{ac}}{m_{fc}}$

#### Intake channel model

Including the throttle model and the intake pipe model, the air mass flow at the throttle is  $\dot{m}_{at}$ ,

$$\dot{m}_{at} = f_1(\alpha, p_m) \quad (1)$$

The  $\alpha$  is the throttle opening and the  $p_m$  is the inlet pipe pressure, and the air mass flow at the entrance of the cylinder is  $\dot{m}_{ac}$ ,

$$\dot{m}_{ac} = f_2(\omega, p_m) \quad (2)$$

$\omega$  is the engine speed; in the transient condition, the air velocity of the inlet and outlet is no longer equal. The intake pipe air mass flow is  $\dot{m}_{am} = \frac{p_m V_m}{R T_m}$ ,  $V_m$  is the volume of inlet pipe,  $R$  gas constant,

$T_m$  intake pipe temperature,  $\dot{m}_{am} = \dot{m}_{at} - \dot{m}_{ac}$ , that is to change the air mass flow rate of the cylinder through the air inlet pipe

$$\dot{m}_{ac} = f_3(\omega, \alpha, p_m) \quad (3)$$

#### *Oil film model*

$$\dot{m}_{ff} = -\frac{1}{\tau_{ff}} m_{ff} + X \cdot \dot{m}_{fi} \quad (4)$$

$$\dot{m}_{fv} = (1 - X) \cdot \dot{m}_{fi} \quad (5)$$

$$\dot{m}_{fc} = \dot{m}_{fv} + \frac{1}{\tau_{ff}} m_{ff} \quad (6)$$

$\dot{m}_{ff}$  for the oil film evaporation rate of g/s;  $\tau_{ff}$  is oil film evaporation time constant of s;  $m_{ff}$  for oil film quality of g;  $X$  is deposited on the wall surface of the fuel ratio;  $\dot{m}_{fi}$  is fuel flow injection of g/s;  $\dot{m}_{fv}$  is fuel evaporation of g/s;  $\dot{m}_{fc}$  as the fuel flow into the combustion room of g/s;  $t_i$  injector pulse width ms;;

The quality of the fuel into the cylinder can be expressed as

$$m_{fc} = f_4(\omega, t_i, p_m) \quad (7)$$

In summary the air fuel ratio mathematical model can be expressed as

$$\lambda = f(\omega, \alpha, p_m, t_i) \quad (8)$$

It can be seen that the transient air fuel ratio control system is a complex nonlinear coupling system.

### 3.2 Identification Of Inverse Model Based On LS-SVM

The transient air-fuel ratio model of fuel injection pulse width  $t_i$  as the input of system, solar term door opening, intake manifold pressure, engine speed as the system interference  $d$ , namely  $d = [\alpha, p_m, \omega]^T$ , the air-fuel ratio for the system output.

The transient air fuel ratio system can be written as follows:

$$y(k+1) = f[y(k), \dots, y(k-n), u(k), \dots, u(k-m)] \quad (9)$$

In the form,  $y$  and  $u$  are the output and input of the system, the  $n$  is the order of the system, the  $m$  is the input delay, and the  $f$  is a nonlinear function. In the form, the transient air fuel ratio system is reversible because the injection pulse width of the input is strictly monotonous. The inverse model of the system can be written

$$u(k) = g[y(k+1), \dots, y(k-n), u(k-1), \dots, u(k-m)] \quad (10)$$

The inverse model is approximated by LS-SVM (10), then the inverse model of LS-SVM is

$$u(k) = g(X) = \sum_{i=1}^{p} a_i K(X, x_i) + b \quad (11)$$

In the formula,  $a_i$  is the Lagrange multiplier, and  $\sum_{i=1}^{p} a_i = 0$ ,  $b$  is offset,  $K(X, x_i) = \varphi(X)^T \varphi(x_i)$ ,  $\varphi(\cdot)$  is a nonlinear mapping function. Here, set the sample as  $\{X(k), u(k)\}$ ,

$X(k) = (u(k-1), u(k-2), \dots, u(k-m), d(k-1), d(k-2), \dots, d(k-m), y(k), y(k-1), \dots, y(k-n))$ , using the training data of  $p$ ,  $\{X(k), u(k)\}$  ( $k = 1, 2, \dots, p$ ) to train the LS-SVM, in order to track the dynamic characteristics of system, the establishment of online dynamic LS-SVM,  $a_i$  and  $b$  of the corresponding parameter is obtained through the study of the LS-SVM system and sample  $\{X(k), u(k)\}$ , the inverse model of online correction system. The system inverse model identification structure is shown in Figure 2.

## 4. Model of adaptive feedback control

In this paper, a model free adaptive control method is used as a feedback controller. MFAC is a new theory and technology in the field of automatic control. It does not need the mathematical model structure of the controlled process, does not need the identification process, only uses the system I/O data to complete the controller design. There is no need for the complex manual tuning of the controller parameters, and a certain system stability analysis to ensure the closed-loop stability of the system.

The MFAC control scheme adopts a method based on tight format linearization [10].

$$\hat{\theta}(k) = \hat{\theta}(k-1) + \frac{\eta_k \Delta u(k-1)}{\mu + (\Delta u(k-1))^2} [\Delta y(k) - \hat{\theta}(k-1) \Delta u(k-1)] \quad (12)$$

$$\hat{\phi}(k) = \hat{\phi}(1), \text{ if } |\hat{\phi}(k)| \le \varepsilon \text{ or } |\Delta u(k-1)| \le \varepsilon \text{ that} \quad (13)$$

$$u(k) = u(k-1) + \frac{p_k \phi(k)}{\lambda + \phi(k)^2} \times [y_d(k+1) - y(k)] \quad (14)$$

Here,  $\eta_k$ ,  $p_k$  is the step sequence, and  $\eta_k$ ,  $p_k \in (0, 2)$ ,  $\phi(k)$  for pseudo partial derivative,  $\mu$  as the penalty factor,  $\lambda$  weighting factor for epsilon,  $\varepsilon$  is positive and very small,  $\hat{\theta}(1)$  is the initial value of  $\hat{\theta}(k)$ ,  $y_d$  is the reference trajectory.

So the controller simply set then  $\eta_k$ ,  $p_k$ ,  $\mu$  and  $\lambda$  parameter, has nothing to do with the mathematical model of the controlled system.

## 5. Analytical results and discussion

### 5.1 Inverse System Model

The inverse model has the function of feedforward controller and can actively compensate the deviation of the system. The concrete steps are as follows:

Step1 LS-SVM training sample set. The test engine adopts the HL495Q EFI gasoline engine, the compression ratio is 7.8, the cylinder working volume is 2.835L, the calibration power is 75KW (3800r/min), the idle speed 750r/min, the dynamometer is the CW260 type eddy current dynamometer, the air flow meter uses the hot wire type flow sensor. Sampling time of 0.01s, the phase of the experiment, get the solar term door opening, engine speed, coolant temperature, intake manifold pressure and injection pulse width of transient parameter data, to accelerate the process of solar term door is composed of idle position open to 85% (1s, 2s, 3s, 4s, 5s), 5\*800 group of test data; the deceleration process for solar term door is composed of 85% closed to the idle position (0.5s, 1s, 1.5s, 2s, 3s), 5\*500 were obtained from experimental data; it received a total of 5200 sets of data as training samples, training stable after the accelerated process of 800 group, 500 group of Deceleration Test data. All data were normalized before training.

Step2 LS-SVM inverse model identification. The LS-SVM kernel function selected radial kernel function  $K(X, x_i) = \exp[-\|X - x_i\|^2/(2\sigma^2)]$ , and the network search method is determined based on the penalty factor  $C = 204$ ,  $\sigma = 3$ . Through LS-SVM learning, the corresponding parameters  $a_i$  and  $b$  are obtained, and the inverse model output of the system can be identified according to the current input  $X$ .

Step3 Inverse system model verification. From Fig. 3, it can be seen that the air-fuel ratio output based on LS-SVM inverse system method can well match the actual air-fuel ratio output, the maximum error is less than 2%, the average error is less than 1%, the approximation performance is high, and the response speed is fast.

### 5.2 Compound Control

The controller of the compound control system consists of the inverse model output and the MFAC control output, and the total control rate of the system is the same.

$$u(k) = u_f(k) + u_c(k)$$

$u_f(k)$  is the output of the LS-SVM inverse model, and  $u_c(k)$  is the control rate of MFAC. Here, the MFAC controller parameters:  $\eta_k = 1.9$ ,  $p_k = 1.9$ ,  $\mu = 1$ ,  $\lambda = 2$ ,  $\hat{\theta}(1) = 2$ .

![Figure 3: Two plots showing air-fuel ratio output and actual output over time. Plot (a) shows the air-fuel ratio increasing from 14.5 to a peak of 17.5 and then decreasing, representing an acceleration condition. Plot (b) shows the air-fuel ratio decreasing from 14.5 to a minimum of 11.5 and then increasing, representing a deceleration condition. Both plots compare 'The model output' (dotted line) and 'The actual output' (solid line).](46f43cb4ffd47565e7c0ca306d461435_img.jpg)

Figure 3: Two plots showing air-fuel ratio output and actual output over time. Plot (a) shows the air-fuel ratio increasing from 14.5 to a peak of 17.5 and then decreasing, representing an acceleration condition. Plot (b) shows the air-fuel ratio decreasing from 14.5 to a minimum of 11.5 and then increasing, representing a deceleration condition. Both plots compare 'The model output' (dotted line) and 'The actual output' (solid line).

(a) acceleration condition

(b) deceleration condition

Figure 3. based on reverse mode air fuel ratio output and actual output

### 5.3 Combined control simulation of air fuel ratio of gasoline engine

In order to verify the effectiveness of the composite controller, a simulation study is carried out in matlab/simulink based on the transient condition of HL495 engine.

Simulation of two transient conditions, throttle change process is shown in figures4 and 5, respectively. The above compound control method is used to get the excess air coefficient, and the simulation result is shown in Figure6. It can be seen that the solar term door opening slow changes, the excess air coefficient change is very small, a maximum of not more than 1.04; solar term door quick change, the excess air coefficient increases volatility, but in the range of + 0.15, and in the door after the mutation of 1.1s solar term rapid return to the expected value, the overall volatility of excess air coefficient not, it shows that the composite control method has fast response speed, high control accuracy and good; and for the change of system parameters such as strong robustness, it proves that the application of the composite control method for transient air-fuel ratio system is effective.

![Figure 4: A plot showing a small amplitude change of valve opening over time. The throttle valve opening starts at 20%, increases linearly to 40% at 4 seconds, remains at 40% until 7 seconds, and then decreases linearly back to 20% at 9 seconds.](29ac39bfd74e57a92045649f83cad949_img.jpg)

Figure 4: A plot showing a small amplitude change of valve opening over time. The throttle valve opening starts at 20%, increases linearly to 40% at 4 seconds, remains at 40% until 7 seconds, and then decreases linearly back to 20% at 9 seconds.

Figure4.small amplitude change of valve opening

![Figure 5: A plot showing a large change in the opening of the valve over time. The throttle valve opening starts at 20%, increases linearly to 80% at 4 seconds, remains at 80% until 7 seconds, and then decreases linearly back to 20% at 9 seconds.](096d7a8a21933900dad68d82ae8a97fb_img.jpg)

Figure 5: A plot showing a large change in the opening of the valve over time. The throttle valve opening starts at 20%, increases linearly to 80% at 4 seconds, remains at 80% until 7 seconds, and then decreases linearly back to 20% at 9 seconds.

Figure5.a large change in the opening of the valve

![Figure 6(a): A plot showing the excess air coefficient over time for a small change in the throttle. The coefficient fluctuates around 1.0, with a maximum value of approximately 1.04.](6a412ce0ee3ac6bd290d214edd54c1da_img.jpg)

Figure 6(a): A plot showing the excess air coefficient over time for a small change in the throttle. The coefficient fluctuates around 1.0, with a maximum value of approximately 1.04.

(a) a small change in the throttle

![Figure 6(b): A plot showing the excess air coefficient over time for a large change in the throttle. The coefficient fluctuates around 1.0, with a maximum value of approximately 1.1 and a minimum value of approximately 0.9.](4e082c2115caa030a9d5b38f91bfd015_img.jpg)

Figure 6(b): A plot showing the excess air coefficient over time for a large change in the throttle. The coefficient fluctuates around 1.0, with a maximum value of approximately 1.1 and a minimum value of approximately 0.9.

(b) a greatly changed in the throttle

Figure 6.based on composite control of excessive air coefficient output

## 6. Conclusions

In order to realize the transient air-fuel ratio control, this paper presents an inverse model feed-forward control composite control strategy based on adaptive feedback control with the use of online LS-SVM, establishes the inverse model of air-fuel ratio system and combines MFAC feedback control to form a compound control method, which is applied to the transient air-fuel ratio control system. Then, the air-to-air ratio inverse system model and composite control method are simulated by using transient test data, and compared with the actual test data. The following conclusions are obtained:

- (1) under the transient condition, it is feasible to adopt the LS-SVM reverse mode feedforward controller, which has better tracking performance for air fuel ratio.
- (2) compound control method can take into account both the advantages of feed-forward and feedback, and it can approach the transient process of air-fuel ratio with high accuracy, and improve the robustness and anti-interference ability of the system.
- (3) the simulation results show that the combined control strategy can be effectively applied to the transient process of air fuel ratio.

## Acknowledgment

This research was sponsored by the China National Natural Science Fund (#51176014), Project of Science and Technology of Henan Province (182102210278) and Hunan Provincial Natural Science Fund (#2016JJ2003). The supports are gratefully acknowledged.

## Reference:

- [1] LI G, HE Y, JIANGG,etal. Research on the air-fuel ratio intelligent control method for coke oven combustion energysaving[C].2nd International conference on Frontiers of Manufacturing and Design Science. Taichung. Taiwan, 2012: 2873—2877.
- [2] SHAO J J. GAO S. TAN D R, etal. Air-fuel ratio fuzzy PID control for coal-bed gas engine based on fuzzy PID feedforward [C].ICEEP. GuiLin, china, 2013: 800 — 808.
- [3] WOJNAR S, HONEK M. Nonlinear air-fuel ratio predictive control of spark ignited engines[C].International conference on Process Control. Strbske Pleso.Slovakia, 2013: 225—330.
- [4] YILDIZ Y, ANNAASAMY A, YANAKIEV D, etal. Spark ignition engine fuel-to-air ratio control: An adaptive control approach[J]. control Engineering Practice, 2010(18): 1369 — 1378.
- [5] Hou Zhixiang, Wu Yihu, Deng Hua and et al. Study on the neural network control of the air-fuel ratio in the transition condition of vehicle gasoline engine[J].Chinese Internal Combustion Engine Engineering, 2006,27 (5) : 33-36
- [6] Xu Donghui, Li Yuelin, Xie Fu Quan and so on. study of oil film parameter identification in gasoline engine transient condition based on chaos-RBF neural network [J].Chinese Internal Combustion Engine Engineering, 2015,36 (3) : 100-105
- [7] Xu Donghui, Li Yuelin and et al.prediction model of transient air-fuel ratio for gasoline engine based on chaos least squares support vector machine [J].vehicle engine, 2015, (2) : 13-17
- [8] Ling Ai, Ye San. Model Predictive Control for Nonlinear Distributed Parameter Systems based on LS—SVM[J]. Asian Journal of Control. 2013.5(15): 1407—1416.
- [9] Fan yugang,zhang yaxiong and et al.Composite Control Combining Inverse Control with PID Control Based on online LS—SVM[J]. Control Engineering of China, 2014.21 (6) : 954-957
- [10] Shao jiang, Tian-hong Luo. Bearing degradation process prediction based on the PCA and optimized LS-SVM model[J]. Measurement, 2013. 9(46): 3143-3152.