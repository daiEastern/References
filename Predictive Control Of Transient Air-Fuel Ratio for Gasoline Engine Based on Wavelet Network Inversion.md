

PAPER • OPEN ACCESS

# Predictive Control Of Transient Air-Fuel Ratio for Gasoline Engine Based on Wavelet Network Inversion

To cite this article: Dandan Song and Yuelin Li 2020 *IOP Conf. Ser.: Earth Environ. Sci.* **508** 012052

View the [article online](#) for updates and enhancements.

You may also like

- [Techniques for measurement of oxygen and air-to-fuel ratio using zirconia sensors. A review](#)  
M Benammar
- [Study on Composite Control Strategy of Transient Air-Fuel Ratio for Gasoline Engine Based on Model](#)  
Dandan Song and Yuelin Li
- [Monitoring the air-fuel ratio of internal combustion engines using a neural network](#)  
S D Walters, M M De Zoysa and R J Howlett

# Predictive Control Of Transient Air-Fuel Ratio for Gasoline Engine Based on Wavelet Network Inversion

**Dandan Song<sup>1\*</sup>, Yuelin Li<sup>2</sup>**

<sup>1</sup> College of Automobile and Mechanical Engineering, Changsha University of Science Technology, Changsha 410076, China

<sup>2</sup> Henan Communication Vocational and Technical College, Institute of Automobile Engineering, Zhengzhou, 450005, China

\*Corresponding author's e-mail: sdd122@163.com

**Abstract.** To achieve accurate control of the transient air-fuel ratio for gasoline engines, a composite predictive control method based on wavelet network is proposed. The inverse system of transient air-fuel ratio system was to identify with wavelet network, which is able to dynamically compensate intake flow with feedforward control, and a pseudo-linear system is formed by cascading the inverse system with the original system. Then the dynamic matrix control(DMC) was used as a compensation for both internal and external disturbance in real time, and the effective control for transient air-fuel ratio system of nonlinear, time-delay and time-variation is realized. Finally simulated with experiment data at transient conditions, the results show that the inverse model based on wavelet network can accurately approximate the air fuel ratio transient process, and this method has stronger robustness and anti-interference. Therefore, the composite predictive control strategy has good control performances and can improve the control precision of air-fuel ratio in transient conditions.

## 1. Introduction

The control accuracy of gasoline engine transient air-fuel ratio is a difficult problem in the current engine control system [1-2]. Under transient conditions, due to the measurement deviation of air intake, the dynamic transmission characteristics of oil film, and the hysteresis of oxygen feedback signal and other factors, the air-fuel ratio control system is nonlinear, time-delay and time-varying, so the traditional closed-loop control based on oxygen sensor is difficult to achieve the accurate control of the instantaneous air-fuel ratio[3]. At present, the research of transient air-fuel ratio control mainly focuses on feedforward or feedback control, for example, using state observer as feedforward control to estimate the air intake in cylinder [4], and then to realize the accurate control of air-fuel ratio; in order to realize the compensation of the fuel injection quantity of air-fuel ratio system, the literature proposes feedforward compensator based on neural network[5]. In the aspect of air-fuel ratio feedback control, the main control methods are PID, fuzzy control and predictive control. For example, in reference [6], the air-fuel ratio control strategy based on generalized predictive control is designed; in order to better compensate the time delay of air-fuel ratio system and adapt to the nonlinearity of the system, a fuzzy PID control strategy with dynamic time delay compensator is proposed in reference [7]. The composite control strategy based on feedforward and feedback provides a new direction for the transient air-fuel ratio control [8], such as the adaptive hybrid algorithm based engine air-fuel ratio controller proposed in literature[9], the chaotic time series LS-SVM prediction model of the transient air-fuel ratio

![Creative Commons Attribution 3.0 licence logo](96fb4373e63be843d9d2dcac2260afff_img.jpg)

The image shows the Creative Commons Attribution 3.0 licence logo, which consists of two circular icons: one with 'cc' and another with a person symbol, followed by the text 'BY'.

Creative Commons Attribution 3.0 licence logo

Content from this work may be used under the terms of the [Creative Commons Attribution 3.0 licence](#). Any further distribution of this work must maintain attribution to the author(s) and the title of the work, journal citation and DOI.

established in literature [10], and so on, all of which have achieved good control results. In order to control the transient air-fuel ratio effectively, a compound control strategy based on inverse model feedforward control and dynamic matrix feedback control is proposed. Firstly, the inverse model of the system is established by using wavelet network, which is used as a feed-forward controller to dynamically compensate the air intake in the transient air-fuel ratio system, and then the inverse system is connected with the original system in series to form a pseudo linear system. Then the disturbance and error of the system are corrected by combining the prediction model, optimization calculation and feedback correction of the dynamic matrix control to realize the nonlinear and time-delay. Finally, the control strategy proposed in this paper is simulated and analyzed by using the transient test data. The results show that the air-fuel ratio predictive control method based on the feedforward feedback composite control strategy proposed in this paper can be effectively applied to the air-fuel ratio system.

## 2. General idea

In this paper, inverse model feed-forward control and dynamic matrix feedback control are used to realize the predictive control of air-fuel ratio system. The block diagram of air-fuel ratio control system is shown in Figure 1. The inverse model of the system is identified by using wavelet network as feed-forward control to compensate the air intake in the transient air-fuel ratio system. The inverse system is connected in series with the original system to form a pseudo linear system. The disturbance and error of the system are corrected by combining the prediction model, optimization calculation and feedback correction of dynamic matrix control. Finally, the nonlinear, time-delay and time-varying transient air-fuel ratio is realized. The system realizes predictive control.

![Figure 1: Block diagram of air fuel ratio control system. The diagram shows a feedback loop. The setpoint y_p enters a summing junction where it is compared with the feedback signal e. The error e goes into an 'Optimization' block, which also receives feedback from a 'Feedback' block. The output of 'Optimization' is u_m. This u_m is added to u_f (from the 'Inverse model') at a summing junction to produce the control signal u. The signal u is sent to the 'Object' block, which also receives disturbance d. The output of the 'Object' block is y. The output y is compared with y_p at the first summing junction to produce the error e. The error e is also fed into the 'Feedback' block, which produces the feedback signal. The 'Inverse model' block takes y_p as input and produces u_f. The 'Predictive model' block takes u as input and produces y_i. The 'Feedback' block takes y_i as input and produces the feedback signal.](2df09d249c38abee55dbf0526dd6da0a_img.jpg)

Figure 1: Block diagram of air fuel ratio control system. The diagram shows a feedback loop. The setpoint y\_p enters a summing junction where it is compared with the feedback signal e. The error e goes into an 'Optimization' block, which also receives feedback from a 'Feedback' block. The output of 'Optimization' is u\_m. This u\_m is added to u\_f (from the 'Inverse model') at a summing junction to produce the control signal u. The signal u is sent to the 'Object' block, which also receives disturbance d. The output of the 'Object' block is y. The output y is compared with y\_p at the first summing junction to produce the error e. The error e is also fed into the 'Feedback' block, which produces the feedback signal. The 'Inverse model' block takes y\_p as input and produces u\_f. The 'Predictive model' block takes u as input and produces y\_i. The 'Feedback' block takes y\_i as input and produces the feedback signal.

Figure 1 block diagram of air fuel ratio control system

![Figure 2: Identification structure of inverse system. The diagram shows the identification of the inverse system. The input u(k) is fed into a 'TDL.m' block. The output of 'TDL.m' is u_f(k). This u_f(k) is fed into the 'Air-fuel ratio system' block. The output of the 'Air-fuel ratio system' block is y(k+τ). This y(k+τ) is fed into a 'TDL.n' block. The output of 'TDL.n' is u(k). The input u(k) and the output y(k+τ) are compared at a summing junction to produce the error e. The error e is fed into the 'Inverse model' block, which produces u_f(k).](b612b838f94982799a69461ffb078a73_img.jpg)

Figure 2: Identification structure of inverse system. The diagram shows the identification of the inverse system. The input u(k) is fed into a 'TDL.m' block. The output of 'TDL.m' is u\_f(k). This u\_f(k) is fed into the 'Air-fuel ratio system' block. The output of the 'Air-fuel ratio system' block is y(k+τ). This y(k+τ) is fed into a 'TDL.n' block. The output of 'TDL.n' is u(k). The input u(k) and the output y(k+τ) are compared at a summing junction to produce the error e. The error e is fed into the 'Inverse model' block, which produces u\_f(k).

Figure 2 identification structure of inverse system

In Figure 1,  $y_p$  is the expected output of the object,  $u$ ,  $y$  is the input and output of the object,  $u_f$  is the identification output of the inverse system,  $u_m$  is the optimized output of the feedback control,  $d$  is the disturbance input of the control object,  $\tilde{y}_1$  is the prediction model output and  $\tilde{y}_{p0}$  is the feedback correction output.

## 3. Identification of inverse system based on Wavelet Network

### 3.1. transient air fuel ratio model [11]

The actual air-fuel ratio  $\lambda$  is the ratio of the air quality  $m_a$  entering the cylinder in each cycle to the fuel quality  $m_f$ , i.e  $\lambda = \frac{m_a}{m_f}$

Intake path model. Including throttle model and intake pipe model, the mass air flow  $\dot{m}_{at}$  at the throttle, then

$$\dot{m}_{at} = f(\alpha, p_m) \quad (1)$$

$\alpha$  is the throttle opening,  $p_m$  is the intake pipe pressure; the air mass flow at the cylinder inlet is  $\dot{m}_{ap}$ , then

$$\dot{m}_{ap} = f(\omega, p_m) \quad (2)$$

$\omega$  is the engine speed; under the transient condition, the air flow velocity of the inlet and outlet pipes is no longer equal. Then the air mass flow in the intake pipe is  $m_a = \frac{p_m V_m}{R T_m}$ , here,  $V_m$  is the volume of the intake pipe,  $R$  is the gas constant,  $T_m$  is the temperature in the intake pipe;  $\dot{m}_a = \dot{m}_{at} - \dot{m}_{ap}$  and the change rate of the air mass flow into the cylinder through the intake pipe is

$$\dot{m}_a = f(\omega, \alpha, p_m) \quad (3)$$

Oil film model

$$\dot{m}_{ff} = -\frac{1}{\tau_{ff}} m_{ff} + X \dot{m}_{fi} \quad (4)$$

$$\dot{m}_{fv} = \dot{m}_{fi}(1 - X) \quad (5)$$

$$\dot{m}_f = \dot{m}_{fv} + \frac{1}{\tau_{ff}} m_{ff} \quad (6)$$

Where,  $\dot{m}_{fv}$  is the fuel evaporation,  $\dot{m}_{fi}$  is the fuel flow rate ejected by the injection nozzle,  $X$  is the proportion of fuel deposited on the wall,  $\dot{m}_{ff}$  is the fuel film evaporation flow rate,  $m_{ff}$  is the mass of the fuel film evaporation,  $\tau_{ff}$  is the time constant of the fuel film evaporation, and  $\dot{m}_f$  is the fuel mass flow into the cylinder.

$$\dot{m}_f = f(\omega, t_i, p_m) \quad (7)$$

Where,  $t_i$  is the fuel injector pulse width time ms

The mathematical model of the air to fuel ratio can be expressed as

$$\lambda = f(\omega, \alpha, t_i, p_m) \quad (8)$$

It can be seen that the transient air fuel ratio system is a complex nonlinear coupling system.

### 3.2. system inverse model

In the transient air-fuel ratio model, the injection pulse width  $t_i$  is taken as the input of the system, and the throttle opening, intake pipe pressure and engine speed are taken as the interference  $d$  of the system, that is to say  $d = [\alpha, p_m, \omega]^T$ , the air-fuel ratio  $\lambda$  is the output of the system. The transient air fuel ratio system can be written as

$$f[y(k + \alpha), \dots, y(k + \alpha - m), u(k), \dots, u(k - m)] = 0 \quad (9)$$

Where,  $m$  is the input order,  $n$  is the output order,  $\alpha$  is the output delay  $\alpha \ge 1$ ,  $f(\cdot)$  is a nonlinear function. Since the injection pulse width is strictly monotonic, the inverse model of the transient air fuel ratio system can be written as

$$u(k) = g[y(k + \alpha), \dots, y(k + \alpha - n), u(k - 1), \dots, u(k - m)] \quad (10)$$

Equation (10) is the inverse model of the transient air fuel ratio system.

### 3.3. identification of inverse system of wavelet network

The inverse model of the system is identified by the wavelet network, that is, the wavelet network is used to replace the  $g(\cdot)$  in equation (11), and then the network weight is adjusted according to the output of the system, so that the response of the wavelet network is the same  $g(\cdot)$ .

The dynamic identification of inverse model is carried out by using the following formula

$$g(t) = \sum_j \omega_j \Psi(D_j(t - a_j)) \quad (11)$$

Where,  $\omega_j$  is the network weight,  $D_j$  is the expansion matrix,  $a_j$  is the translation vector, and the basis function adopts the Gauss mother wavelet

$$\Psi(t) = (1-t)^{\frac{t^2}{2}} \quad (12)$$

Therefore, equation (11) can be used to replace the sigmoid transfer function of neural network for dynamic identification of inverse model.

The inverse system identification structure is shown in Figure 2.

In Figure 2,  $u(k)$ ,  $y(k + \alpha)$  are system input and output, respectively  $T_{DLm}$ ,  $T_{DLn}$  are input and output delay quantities, and  $T_{DLm} = [u(k-1), \dots, u(k-m)]$ ,  $T_{DLn} = [y(k + \alpha - 1), \dots, y(k + \alpha - n)]$ ,  $u_f(k)$  is inverse system identification output, the difference between identification output  $u_f(k)$  and system input  $u(k)$  as  $e(k)$ , used to train wavelet network.

The pseudo linear system is composed of the wavelet network inverse system in series before the original system. The pseudo linear system is shown in Figure 3. It can be seen that the pseudo linear system composed of the wavelet network inverse system and the original object realizes the linearization between the input and output. However, the open-loop control of the pseudo linear system only eliminates the nonlinear characteristics, and has no good control for the external disturbance and error. Therefore, dynamic matrix control [13] is added to eliminate system interference.

## 4. Predictive control of transient air fuel ratio

In this paper, the dynamic matrix control is used to  $\{a(1), a(2), \dots, a(N), \dots, a(\infty)\}$  realize predictive control. The sampling value of the step response of the control object  $N$  is set as the modeling time domain, the length of the dynamic matrix control time domain is  $M$ , the length of the optimization

![Figure 3: Schematic diagram of pseudo linear system. The diagram shows a block diagram where input Φ(k) and TDLn are fed into an 'Inverse system of wavelet network' block. The output of this block is u(k), which is fed into an 'Object' block. A disturbance d(k) is also fed into the 'Object' block. The output of the 'Object' block is y(k). A feedback loop from y(k) to TDLm is also shown.](5bcaa554999322056447df1b81256bfc_img.jpg)

Figure 3: Schematic diagram of pseudo linear system. The diagram shows a block diagram where input Φ(k) and TDLn are fed into an 'Inverse system of wavelet network' block. The output of this block is u(k), which is fed into an 'Object' block. A disturbance d(k) is also fed into the 'Object' block. The output of the 'Object' block is y(k). A feedback loop from y(k) to TDLm is also shown.

Figure 3 Schematic diagram of pseudo linear system

![Figure 4: A line graph showing the input φ(k) and output y(k) responses of the pseudo linear system. The x-axis is labeled k and ranges from 0 to 400. The y-axis is labeled y(k) and ranges from -0.6 to 0.6. The input φ(k) is a step function that jumps from -0.5 to 0.5 at k=100 and returns to -0.5 at k=200. The output y(k) follows the input φ(k) with a delay and some overshoot, reaching a peak of approximately 0.55 at k=150 and returning to -0.5 at k=300.](0f92e96694face0b13a687ec21fb9101_img.jpg)

Figure 4: A line graph showing the input φ(k) and output y(k) responses of the pseudo linear system. The x-axis is labeled k and ranges from 0 to 400. The y-axis is labeled y(k) and ranges from -0.6 to 0.6. The input φ(k) is a step function that jumps from -0.5 to 0.5 at k=100 and returns to -0.5 at k=200. The output y(k) follows the input φ(k) with a delay and some overshoot, reaching a peak of approximately 0.55 at k=150 and returning to -0.5 at k=300.

Figure 4 input  $\varphi(k)$  and output  $y(k)$  responses of pseudo linear system

time domain is  $P$ , and then  $M \le P \le N$ , the predictive model of the object can be expressed as

$$Y_{PM}(k) = Y_{P0}(k) + A\Delta U_M(k) \quad (13)$$

$$\min J(k) = \|Y_P(k) - Y_{PM}(k)\|_Q^2 + \|\Delta U_M(k)\|_R^2 \quad (14)$$

## 5. Analytical results and discussion

### 5.1. simulation scheme design

The specific simulation steps are as follows:

The first step is to acquire the sample set to train the wavelet network. The HL495Q EFI gasoline engine used in this paper is tested. In order to ensure that the sampling data is not distorted, the sampling time is 0.01s. Considering the complexity of the transient condition, the whole process adopts the staged test to obtain the transient sample data such as throttle opening, engine speed, coolant temperature, intake pipe pressure and injection pulse width, and 5 \* 800 groups of test data are obtained; during the deceleration process, and 5 \* 500 groups of test data are obtained; in this way, 5200 groups of data are obtained as training samples. After the training is stable, acceleration is adopted 800 sets of process data and 500 sets of deceleration process data are inspected and tested.

In the second step, the inverse model is identified by wavelet network. The expected output of the air-fuel ratio control system is  $\lambda = 14.7$ , the order of input and output is  $m = 2, n = 3$  respectively, the system delay  $\alpha = 2$ , the wavelet basis function adopts the Gauss mother wavelet, the network structure is determined as a three-layer network of 5-11-2, the wavelet network parameter optimization adopts the steepest descent method, the learning and momentum factors of the wavelet network take 0.05 and 0.9 respectively. In order to verify the effectiveness of the inverse model identified by wavelet network, the transient air-fuel ratio output of the model is tested and compared with the measured value on the bench. As shown in Figure 5, the output of the inverse model can well approximate the output of the actual air-fuel ratio, and the response speed is fast.

![Figure 5: Comparison of model output and actual output for air-fuel ratio under acceleration and deceleration conditions. (a) Acceleration condition: The air-fuel ratio increases from 14.5 to 17.5 over 8 seconds. (b) Deceleration condition: The air-fuel ratio decreases from 14.5 to 11.5 over 6 seconds. In both cases, the model output (dotted line) closely follows the actual output (solid line).](ed2fa033a401564314cdc32fe9732935_img.jpg)

Figure 5 consists of two subplots, (a) and (b), showing the air-fuel ratio over time. Subplot (a) is titled 'acceleration condition' and shows the air-fuel ratio increasing from approximately 14.5 at time 0 to a peak of about 17.5 at time 5, then slightly decreasing. Subplot (b) is titled 'deceleration condition' and shows the air-fuel ratio decreasing from approximately 14.5 at time 0 to a minimum of about 11.5 at time 3, then slightly increasing. Both plots have 'The air-fuel ratio' on the y-axis and 'Time (s)' on the x-axis. A legend in each plot indicates that the dotted line represents 'The model output' and the solid line represents 'The actual output'. The two lines are nearly identical in both plots, indicating a high degree of accuracy in the model.

Figure 5: Comparison of model output and actual output for air-fuel ratio under acceleration and deceleration conditions. (a) Acceleration condition: The air-fuel ratio increases from 14.5 to 17.5 over 8 seconds. (b) Deceleration condition: The air-fuel ratio decreases from 14.5 to 11.5 over 6 seconds. In both cases, the model output (dotted line) closely follows the actual output (solid line).

Figure 5 output based on inverse mode air fuel ratio and actual output

The third step is the verification of pseudo linear system. Combining the inverse model with the air-fuel ratio system, the input square wave signal, input and output response are shown in Figure 5. It can be seen that the pseudo linear system constructed in this paper has realized the linearization function, and the time delay between the input and output is of order 2.

The fourth step is to design dynamic matrix controller. In this paper, the parameter modeling time domain, prediction time domain and control time domain are respectively,  $N = 40, P = 15, M = 6$ , error weight matrix and control weight matrix are respectively,  $Q = 0.023I(P)$ ,  $R = 0.62I(M)$ .

### 5.2. analysis of simulation results

In this paper, two transient conditions are simulated to study the control strategy. The change process of the throttle under these two conditions is shown in Figure 6, and the simulation control results are shown in Figure 7. It can be seen that when the change range of the throttle opening is small, the fluctuation of the excess air coefficient of the system output is small, which is basically maintained near the expected value 1, and the maximum offset is about 1.01, and the response speed is non-linear. When the throttle opening changes greatly, the excess air coefficient fluctuates greatly, but the response speed is very fast, and the change range is within the expected value  $\pm 2.5\%$ , which shows that the control system designed in this paper has the prediction function, improves the situation of large change of air-fuel ratio.

caused by non-linearity and system delay under transient condition, and avoids the engine's too rich or too lean.

![Figure 6: Throttle change curves. (a) Small throttle change: The throttle valve opening (%) starts at 20% for 2 seconds, then ramps up to 40% over 2 seconds, stays at 40% for 2 seconds, and ramps down to 20% over 2 seconds, remaining at 20% until 10 seconds. (b) Large throttle change: The throttle valve opening (%) starts at 20% for 2 seconds, then ramps up to 80% over 2 seconds, stays at 80% for 2 seconds, and ramps down to 20% over 2 seconds, remaining at 20% until 10 seconds.](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 6: Throttle change curves. (a) Small throttle change: The throttle valve opening (%) starts at 20% for 2 seconds, then ramps up to 40% over 2 seconds, stays at 40% for 2 seconds, and ramps down to 20% over 2 seconds, remaining at 20% until 10 seconds. (b) Large throttle change: The throttle valve opening (%) starts at 20% for 2 seconds, then ramps up to 80% over 2 seconds, stays at 80% for 2 seconds, and ramps down to 20% over 2 seconds, remaining at 20% until 10 seconds.

Figure 6 throttle change curve

![Figure 7: Excess air factor output. (a) Small throttle change: The excess air coefficient fluctuates around 1.0 with small peaks and troughs. (b) Large throttle change: The excess air coefficient fluctuates around 1.0 but shows larger peaks and troughs, reaching a peak of approximately 1.12 and a trough of approximately 0.85.](01da0d212fb571933f10f96556157745_img.jpg)

Figure 7: Excess air factor output. (a) Small throttle change: The excess air coefficient fluctuates around 1.0 with small peaks and troughs. (b) Large throttle change: The excess air coefficient fluctuates around 1.0 but shows larger peaks and troughs, reaching a peak of approximately 1.12 and a trough of approximately 0.85.

Figure 7 excess air factor output

## 6. Conclusions

In order to solve the nonlinear and time-delay problems of the transient air-fuel ratio system, a predictive control strategy based on feedforward and dynamic matrix feedback is proposed. The simulation results show that the inverse model system identified by wavelet network has good approximation ability, and the pseudo linear system constructed in this paper has realized the linearization function; the compound control method of feedforward and additional feedback can take into account the advantages of feedforward and feedback, which can not only approach the instantaneous process of air-fuel ratio with high accuracy, but also improve the robustness and anti-interference ability of the system; the compound control method based on this paper. The predictive control method of the control strategy can effectively control the accuracy of the air-fuel ratio system.

## Reference:

- [1] LI G, HE Y, JIANGG, etal. Research on the air-fuel ratio intelligent control method for coke oven combustion energy saving [C]. 2nd International conference on Frontiers of Manufacturing and Design Science. Taichung. Taiwan, 2012: 2873—2877.
- [2] SHAO J J. GAoS. TAN D R, etal. Air-fuel ratio fuzzy PID control for coal-bed gas engine based on fuzzy PID feedforward [C]. ICEEP. GuiLin, china, 2013: 800 — 808.
- [3] WOJNAR s , HONEK M . Nonlinear air-fuel ratio predictive control of spark ignited engines [C]. International conference on Process Control. Strbske Pleso. Slovakia , 2013 : 225—330.
- [4] YILDIZ Y, ANNAASAMY A, YANAKIEV D, etal. Spark ignition engine fuel-to-air ratio control: An adaptive control approach [J]. control Engineering Practice, 2010(18): 1369 — 1378.
- [5] Hou Zhixiang, Wu Yihu, Deng Hua and et al. Study on the neural network control of the air-fuel ratio in the transition condition of vehicle gasoline engine [J]. Chinese Internal Combustion Engine Engineering, 2006, 27 ( 5 ) : 33-36

- [6] Xu Donghui, Li Yuelin, Xie Fu Quan and so on. study of oil film parameter identification in gasoline engine transient condition based on chaos-RBF neural network [J].Chinese Internal Combustion Engine Engineering, 2015,36 (3) : 100-105
- [7] Xu Donghui, Li Yuelin and et al. prediction model of transient air-fuel ratio for gasoline engine based on chaos least squares support vector machine [J].vehicle engine, 2015, (2) : 13-17
- [8] Ling Ai, Ye San. Model Predictive Control for Nonlinear Distributed Parameter Systems based on LS—SVM[J]. Asian Journal ofControl. 2013.5(15): 1407—1416.
- [9] Fan yugang,zhang yaxiong and et al.Composite Control Combining Inverse Control with PID Control Based on online LS—SVM[J]. Control Engineering of China, 2014.21 (6) : 954-957
- [10] Shao jiang, Tian-hongLuo. Bearing degradation process prediction based on the PCA and optimized LS-SVM model[J]. Measurement, 2013. 9(46): 3143-3152.