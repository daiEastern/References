

## Article

# Real-Time Inductance Estimation of Sensorless PMSM Drive System Using Wavelet Denoising and Least-Order Observer with Time-Delay Compensation

Gwangmin Park <sup>1</sup> and Junhyung Bae <sup>2,\*</sup>

<sup>1</sup> Division of Mobility Technology, Daegu Gyeongbuk Institute of Science and Technology, Techno Jungang Dae-ro 333, Hyeonpung-eup, Dalseong-gun, Daegu 42988, Republic of Korea; gmpark@dgist.ac.kr

<sup>2</sup> Department of Electrical Engineering, Daegu Catholic University, Hayang-ro 13-13, Hayang-eup, Gyeongsan-si 38430, Republic of Korea

\* Correspondence: baejh80@cu.ac.kr

## Abstract

In this paper, the inductance of a sensorless PMSM (Permanent Magnet Synchronous Motor) drive system equipped with a periodic load torque compensator based on a wavelet denoising and least-order observer with time-delay compensation is estimated in real-time. In a sensorless PMSM system with constant load torque, the magnetically saturated inductance value remains constant. This constant inductance error causes minor performance degradation, such as a constant rotor position estimation error and non-optimal torque current, but it does not introduce a speed estimation error. Conversely, in a sensorless PMSM motor system subjected to periodic load torque, the magnetically saturated inductance error fluctuates periodically. This fluctuation leads to periodic variations in both the estimated position error and the speed error, ultimately degrading the load torque compensation performance. This paper applies the maximum energy-to-Shannon entropy criterion for the optimal selection of the mother wavelet in the wavelet transform to remove the motor signal noise and achieve more accurate inductance estimation. Additionally, the coherence and correlation theory is proposed to address the time delay in the least-order observer and improve the time delay. A self-saturation compensation method is also proposed to minimize periodic speed fluctuations and improve control accuracy through inductance parameter estimation. Finally, experiments were conducted on a sensorless PMSM drive system to verify the inductance estimation performance and validate the effectiveness of vibration reduction.

**Keywords:** PMSM; inductance; wavelet denoising; least-order observer; coherence- and correlation-based time-delay estimation

![check for updates icon](d3294dc879b451b369c0b06f42e9b39f_img.jpg)

check for updates icon

Academic Editor: Ningfei Jiao and Hang Zhang

Received: 16 October 2025

Revised: 14 November 2025

Accepted: 23 November 2025

Published: 28 November 2025

**Citation:** Park, G.; Bae, J. Real-Time Inductance Estimation of Sensorless PMSM Drive System Using Wavelet Denoising and Least-Order Observer with Time-Delay Compensation.

*Machines* **2025**, *13*, 1102.

[https://doi.org/10.3390/](https://doi.org/10.3390/machines13121102)

*machines*13121102

**Copyright:** © 2025 by the authors.

Licensee MDPI, Basel, Switzerland.

This article is an open access article

distributed under the terms and

conditions of the Creative Commons

Attribution (CC BY) license

([https://creativecommons.org/](https://creativecommons.org/licenses/by/4.0/)

[licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/)).

## 1. Introduction

Electrical motors have played a crucial role in technological advancements for over a century. As technological progress accelerates, the applications of electrical motors are rapidly expanding. Advances in modern digital computers, along with recent developments in power electronics and semiconductor devices, have made groundbreaking contributions to the design and control of electric motors. Among them, permanent magnet synchronous motors (PMSMs) are widely used due to their high efficiency and lightweight characteristics, in applications ranging from household appliances to automotive drives. Field-Oriented Control (FOC) is primarily employed for high-performance operation in

PMSM drive systems, which necessitates real-time knowledge of the rotor's position. However, practical issues such as mounting constraints, high sensor cost, and the risk of catastrophic control failure in the event of a fault have spurred intensive research into sensorless control methods that eliminate the need for a direct position sensor. Sensorless control techniques mainly fall into two categories: current model-based methods and extended back-EMF-based methods. Recently, the latter has been increasingly applied due to the use of ArcTan calculations in microprocessors, which eliminate the limitations of input variables and provide fast tracking ability [1–4].

When the external load torque is constant, the rotor position estimation error is constant because the torque component current and inductance parameter error due to magnetic saturation are constant. This constant rotor position error has a negligible effect on the estimation speed error. However, when periodic load torque occurs, the inductance parameters also undergo periodic fluctuations, resulting in periodic fluctuation components in both the position and speed estimation errors. That is, in environments with a large magnitude and high fluctuation rate of the load torque, rather than the ideal situation of a small and stable load torque, the change in inductance increases, leading to larger estimation position errors and a degradation of the overall motor system's control precision. Particularly in environments directly exposed to external vibrations and loads, such as motors near engines and powertrain systems, household pumps, and compressors, the control performance can rapidly deteriorate [2].

Analyzing the external load pattern and applying an appropriate compensation current can mitigate the effects of load torque fluctuation. However, applying this method may increase the ripple in the estimated speed due to the magnetic saturation of the inductance as the amount of compensation current increases. If appropriate compensation control considering this is not performed, it can lead to mechanical instability and NVH (Noise, Vibration, and Harshness) issues in the entire motor system. Therefore, the precision of sensorless control can be improved by accurately estimating the actual inductance magnitude and performing real-time control in a closed-loop manner [5,6].

Previously, attempts were made to estimate the magnitude of the inductance using mathematical model-based observers to compensate for the magnetic saturation problem caused by inductance variation. However, such approaches were sensitive to the back-EMF (electromotive force constant) and drive output voltage fluctuations because they used the estimated rotor position and speed information during sensorless control. Furthermore, even with an appropriate back-EMF constant, when exposed to periodic load torque fluctuations, the estimated inductance faced problems such as noise and time delay, which could degrade system stability and speed estimation performance [7–9].

Wavelet transform is increasingly being used for modeling, analysis, and control of electric motor drives in high-performance applications. Unlike traditional Fast Fourier Transform (FFT) and Short-Time Fourier Transform (STFT), wavelet transform has been implemented in several technologies for high-performance control and diagnostics of systems like Permanent Magnet Synchronous Motor (PMSM) drives, Brushless DC motor drives, and induction motor drives. Chaplais et al. [10] developed an online wavelet-based noise reduction algorithm for a 3-phase PM Brushless DC motor drive used in a reaction wheel system. This wavelet-based algorithm was implemented to denoise the feedback signal of the Brushless DC motor drive. Khorbottly et al. [11] developed a wavelet-based real-time noise reduction technique implemented for position sensorless control of Switched Reluctance Motor (SRM) drive systems. Song et al. [12] proposed a Wavelet Neural Network (WNN) based speed estimation method for sensorless control of PM Brushless DC (BLDC) motor drives. However, the drive system integrated with the WNN-based speed estimator showed unsatisfactory performance during high-speed operation

of the Brushless DC motor due to the offline training of the network. Khan et al. [13] developed and implemented a hybrid Wavelet Packet Transform (WPT) and Artificial Neural Network (ANN) based fault diagnosis and protection technique for inverter-fed IPM synchronous motors. The stator currents of various fault and healthy conditions of IPMSM were pre-processed by WPT. The second-level WPT coefficients of the stator current were used as inputs to a 3-layer feedforward neural network. Additionally, Khan et al. [14] proposed a new wavelet-based multi-resolution PID controller for precise speed control of IPMSM drives under system uncertainties. The proposed controller is based on the multi-resolution decomposition of speed error between the command and actual speed using Discrete Wavelet Transform (DWT). Control signals were generated using wavelet transform coefficients of speed error at various frequency sub-bands of the DWT tree. Based on the above discussions, it can be concluded that there is a trend of recent research activities focusing on the application of wavelet transform in motor drives.

Selection of an appropriate wavelet and the optimal decomposition level are important criteria in signal denoising. A major challenge when using wavelet transforms is choosing the most suitable mother wavelet for a given task, because different mother wavelets applied to the same signal can yield different results. To judge the similarity between a signal and a mother wavelet more precisely, quantitative approaches have been proposed in recent years. Minimum Description Length (MDL) was proposed by N. Saito [15] as a criterion for selecting the optimal mother wavelet for noise suppression and signal compression. MDL theory states that, among a set of candidate models, the best model is the one that provides the shortest combined description of the data and the model itself. Hamid et al. [16] applied MDL as a guideline for selecting the most suitable mother wavelet to compress power disturbance data. Using the MDL criterion, Symlet7 was found to outperform other mother wavelets for most power disturbance signals. Khan et al. [14] applied the MDL criterion in a study on protection of three-phase interior permanent magnet synchronous motors and selected the most suitable mother wavelet for that analysis; db3 was chosen as the mother wavelet for the wavelet packet transform. In addition, the maximum cross-correlation criterion has been applied for denoising ECG signals. Singh and Tiwari [17] investigated ECG denoising using db8, which was selected according to the maximum correlation criterion. Yan [18] proposed the energy-to-Shannon-entropy ratio criterion and the MinMax information criterion to select the most suitable mother wavelet for bearing fault detection. The energy-to-Shannon-entropy ratio criterion refers to maximizing the amount of energy while minimizing the Shannon entropy of the corresponding wavelet coefficients. The MinMax information criterion considers a combination of criteria including minimum joint entropy, minimum conditional entropy, minimum elastic entropy, maximum mutual information, and maximum correlation coefficient. Using the energy-to-Shannon entropy ratio and the MinMax information criteria, reverse biorthogonal 5.5 was chosen as the mother wavelet. Kankar et al. [19] also applied the maximum energy-to-Shannon entropy criterion for bearing fault detection. For thresholding approaches, all wavelets within each wavelet family must be considered to test denoising performance. Therefore, performance-based wavelet selection methods are inefficient and time-consuming when optimizing between selecting lower vanishing moments and performance measures. To avoid this cumbersome procedure, this paper uses the maximum energy-to-Shannon entropy criterion as the method for selecting the optimal mother wavelet for wavelet denoising.

This paper investigates a real-time inductance estimation method for a sensorless PMSM drive based on wavelet denoising and a least-order observer to minimize rotor position and speed errors and compensate for external periodic load-torque variations. To reduce uncertainty caused by flux saturation and improve real-time control performance, motor currents are filtered using a wavelet transformation. The motor inductance is then

estimated using a least-order observer that incorporates coherence- and correlation-based time-delay estimation to reduce time delay, and a compensation control for flux-saturation is applied. The proposed least-order observer with coherence- and correlation-based time-delay estimation aims to shorten the delay of observer and thereby improve the accuracy of the estimated inductance. To validate the flux saturation compensation method and assess control performance, a sensorless PMSM drive system is modeled, and experiments are conducted. Under periodic load-torque conditions, applying the estimated inductance from the proposed method for compensation control is shown to reduce sensorless speed estimation errors and to improve the system's frequency response characteristics and NVH performance.

## 2. Magnetic Saturation of Sensorless Control

Generally, the voltage equations in the  $dq$  synchronous frame for vector control of a PMSM are given by (1),

$$\begin{bmatrix} v_d \\ v_q \end{bmatrix} = \begin{bmatrix} R_a + pL_d & -\omega L_q \\ \omega L_q & R_a + pL_d \end{bmatrix} \begin{bmatrix} i_d \\ i_q \end{bmatrix} + \begin{bmatrix} 0 \\ \omega\psi \end{bmatrix} \quad (1)$$

where  $R_a$ ,  $\psi$ , and  $p$  denote the stator resistance, the back-EMF constant, and the differential operator, respectively.  $L_d$ ,  $L_q$  are the  $d$ - and  $q$ -axis inductances,  $v_d$ ,  $v_q$  are the stator voltages, and  $i_d$  and  $i_q$  are the stator currents in the  $dq$  synchronous reference frame. Ignoring the difference between the estimated rotor speed and the actual rotor speed, (1) can be transformed into the  $\gamma\delta$ -axes using the extended back-EMF representation.

The voltage equation can then be written as [2]

$$\begin{bmatrix} v_\gamma \\ v_\delta \end{bmatrix} = \begin{bmatrix} R_a + pL_d & -\omega L_q \\ \omega L_q & R_a + pL_d \end{bmatrix} \begin{bmatrix} i_\gamma \\ i_\delta \end{bmatrix} + \begin{bmatrix} e_\gamma \\ e_\delta \end{bmatrix} \quad (2)$$

where  $e_\gamma = -E_{ex}\sin\theta_e$ ,  $e_\delta = -E_{ex}\cos\theta_e$ , and  $E_{ex} = \omega[(L_d - L_q)i_d + \psi] - (L_d - L_q)\frac{di_q}{dt}$ . Here  $v_\gamma$  and  $v_\delta$  are the stator voltages,  $i_\gamma$  and  $i_\delta$  are the stator currents, and  $e_\gamma$  and  $e_\delta$  are the extended back-EMFs in the estimated  $\gamma\delta$  synchronous reference frame, which account for the rotor position error.

Using  $e_\gamma$  and  $e_\delta$ , the rotor position error can be determined.

$$\hat{\theta}_e = \tan^{-1}\left(-\frac{\hat{\theta}_\gamma}{\hat{\theta}_\delta}\right) \cong -\frac{\hat{e}_\gamma}{E_{ex}} \quad (3)$$

The estimated speed, denoted as  $\hat{\omega}_r$ , can be acquired through a PI controller by using the estimated rotor position error,  $\hat{\theta}_e$ , as the input. To reduce noise, a low-pass filter is applied. Additionally, the estimated rotor position,  $\hat{\theta}$ , can be calculated by integrating the estimated speed.

Ensuring precise sensorless control requires accurate identification of parameters such as resistance and inductance, as described in (2). In systems subjected to significant periodic loads, such as pumps or compressors, magnetic saturation causes a mismatch between the actual  $q$ -axis inductance  $L_q$  and its estimated value  $\hat{L}_q$ , which in turn introduces errors in rotor position estimation.

To compensate for these deviations caused by magnetic saturation, (2) can be reformulated in terms of the extended back-EMF components  $e_\gamma$ ,  $e_\delta$ :

$$\begin{bmatrix} e_\gamma \\ e_\delta \end{bmatrix} = \begin{bmatrix} v_\gamma \\ v_\delta \end{bmatrix} - \begin{bmatrix} R_a + pL_d & -\omega\hat{L}_q \\ \omega\hat{L}_q & R_a + pL_d \end{bmatrix} \begin{bmatrix} i_\gamma \\ i_\delta \end{bmatrix} + \begin{bmatrix} \Delta e_\gamma \\ \Delta e_\delta \end{bmatrix} \quad (4)$$

where  $\Delta e_\gamma = -p\Delta L_d i_\gamma + \omega\Delta L_q i_\delta$ , and  $\Delta e_\delta = -p\Delta L_d i_\delta - \omega\Delta L_q i_\gamma$ . Here,  $\Delta L_d$  and  $\Delta L_q$  represent the errors in the  $d$ - and  $q$ -axis inductances, respectively, defined as the difference between the actual inductance and its estimated value. In practical systems,  $e_\gamma$  and  $e_\delta$  are affected by  $\Delta e_\gamma$  and  $\Delta e_\delta$ , which incorporate the inductance errors. As a result, both rotor position error and speed ripple increase.

Consequently, since the dominant term contributing to position estimation error is  $\omega\Delta L_q i_\delta$ , compensating for variations in the  $q$ -axis inductance which is the primary parameter affected by magnetic saturation can effectively reduce rotor position error and mitigate speed ripple [2].

## 3. Real-Time Inductance Estimation Using Wavelet Denoising and Least-Order Observer with Time-Delay Compensation

### 3.1. Signal Denoising by Discrete Wavelet Transform

When wavelet transform is applied to signal processing, the general procedure is as follows. First, the signal is decomposed using the wavelet transform to obtain the wavelet coefficients. Then, depending on the requirements, the wavelet coefficients are processed. Finally, the signal is reconstructed through the inverse wavelet transform [2].

The application of wavelet transform in signal denoising can be described as follows. When the noise is stationary, an empirically recorded signal corrupted by additive noise can be expressed as [20]

$$x(t) = s(t) + \sigma n(t) \quad (5)$$

where  $x(t)$  is the noisy signal,  $s(t)$  is the true noise-free signal,  $n(t)$  is an independent normal random signal, and  $\sigma$  represents the noise intensity in  $x(t)$ . The noise is generally modeled as a stationary, independent, zero-mean white Gaussian variable.

The objective of denoising is to reconstruct the original signal  $s(t)$  from a finite set of values of  $x(t)$ , without assuming any specific structure of the signal. A common approach to denoising models the noise as a high-frequency component superimposed on the original signal. Several wavelet-based denoising techniques have been proposed, among which thresholding is a simple and effective method. In practice, the fundamental principle of wavelet denoising for extracting the ideal components of a signal corrupted by noise lies in estimating the noise level. The estimated noise level is then used to set a threshold for the small coefficients, which are assumed to correspond to noise.

The signal denoising procedure based on the Discrete Wavelet Transform (DWT) consists of three stages: signal decomposition, thresholding, and signal reconstruction. Orthogonal DWT is particularly well suited for denoising, since the decomposition is additive; consequently, the analysis of the noisy signal is equivalent to the sum of the analyses of the true signal and the additive noise. Moreover, when the noise is assumed to be white, the detail coefficients at all scales essentially correspond to white noise with the same variance.

The core of wavelet denoising lies in selecting an appropriate threshold. In general, the threshold is determined by the noise intensity  $\sigma$ , as defined in (5). Once the noise intensity has been estimated, various mathematical models can be employed to determine the threshold value. Thresholding is typically applied in one of the following two ways. Let  $\omega$  denote the original wavelet coefficient,  $\eta(\omega)$  the thresholded coefficient, and  $T$  the threshold value. Define the indicator function as [20–22]

$$I(x) = \begin{cases} 1, & x \text{ is true} \\ 0, & x \text{ is false} \end{cases} \quad (6)$$

(1) Hard Thresholding: In this method, wavelet coefficients with absolute values below the threshold are set to zero. This approach leaves coefficients larger than the threshold unaffected, which may cause instability and sensitivity to small changes in the signal.

$$\eta(\omega) = \omega I(|\omega| > T) \quad (7)$$

(2) Soft Thresholding: In this method, the retained wavelet coefficients are reduced by the threshold value:

$$\eta(\omega) = (\omega - \operatorname{sgn}(\omega)T)I(|\omega| > T) \quad (8)$$

### 3.2. Mother Wavelet Selection Using Maximum Energy-to-Shannon Entropy Criterion

The mother wavelet serves as the basis for analyzing a given signal in wavelet transform. Since the results obtained from the wavelet transform are influenced by the choice of the mother wavelet, selecting an optimal one is of critical importance. In this study, the energy-to-Shannon entropy criterion, which is relatively simple to compute and widely used for condition monitoring and fault diagnosis, was adopted.

The energy content of a signal is a measure that uniquely characterizes the signal. The amount of energy in a continuous-time signal  $x(t)$  can be calculated as [18]

$$E_{x(t)} = \int |x(t)|^2 dt \quad (9)$$

When the signal is represented by discrete samples  $x(i)$ , where  $i = 1, 2, \dots, N$ , the signal energy can be expressed as

$$E_{x(i)} = \sum_{i=1}^{N} |x(i)|^2 \quad (10)$$

Here,  $N$  denotes the length of the signal expressed as the number of data points, and  $x(i)$  represents the signal amplitude.

The energy content of a signal can be calculated using its wavelet coefficients and is expressed as

$$E_{energy} = \iint |W(s, \tau)|^2 ds d\tau \quad (11)$$

This indicates that the energy associated with a specific scaling parameter  $s$  can be written as

$$E_{energy}(s) = \int |W(s, \tau)|^2 d\tau \quad (12)$$

For sampled data, the energy can be expressed as

$$E_{energy}(s) = \sum_{i=1}^{N} |W(s, i)|^2 \quad (13)$$

where  $N$  is the number of wavelet coefficients and  $W(s, i)$  denotes the wavelet coefficient. If the signal contains a dominant frequency component corresponding to a specific scale  $s$ , the wavelet coefficients at that scale will exhibit relatively high magnitudes at the time when this frequency component occurs. Consequently, applying the wavelet transform to a signal enables the extraction of the energy associated with such frequency components.

The energy distribution of wavelet coefficients can be quantitatively described using Shannon entropy. The Shannon entropy of a signal is defined as

$$E_{entropy}(s) = - \sum_{i=1}^{N} p_i \log_2 p_i \quad (14)$$

where  $p_i$  represents the energy probability distribution of the wavelet coefficients and is given by

$$p_i = \frac{|W(s,i)|^2}{E_{Energy}(s)} \quad (15)$$

Since the criterion for selecting a mother wavelet aims at maximization, the objective is to extract the maximum possible energy from the analyzed signal while simultaneously minimizing the Shannon entropy of the corresponding wavelet coefficients. Accordingly, the energy-to-Shannon entropy ratio  $R(s)$  is defined as

$$R(s) = \frac{E_{Energy}(s)}{E_{Entropy}(s)} \quad (16)$$

A larger value of  $R(s)$  indicates that the corresponding mother wavelet is more suitable for signal analysis.

### 3.3. Proposed Least-Order Observer with Coherence- and Correlation-Based Time-Delay Compensation

In conventional model-based compensation methods for addressing flux saturation errors, the PMSM voltage equations are typically expressed in terms of inductance. The inductance is then predicted through an observer and fed back to compensate for flux saturation. For observer modeling, the input and output variables of the target control system are defined, and specific internal parameters are indirectly estimated based on a mathematical model [3].

When the system is represented by a state equation with two states, the state-space model can be expressed in matrix form as follows:

$$\begin{bmatrix} \dot{x}_1 \\ \dot{x}_2 \end{bmatrix} = \begin{bmatrix} A_{11} & A_{12} \\ A_{21} & A_{22} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} + \begin{bmatrix} B_1 \\ B_2 \end{bmatrix} u + K \begin{bmatrix} 0 \\ \hat{y} - \hat{\dot{y}} \end{bmatrix} \quad (17)$$

$$y = Cx$$

where  $x_1$  and  $x_2$  denote the variables to be estimated,  $u$  represents the input of the state equation, and  $y$  is the output.  $A$ ,  $B$ , and  $C$  are weighting constants associated with each state variable,  $K$  denotes the observer gain, and the symbol  $\hat{\cdot}$  indicates estimated variables.

In a sensorless system, since the variable to be estimated for flux saturation compensation is the inductance, the state  $x_1$  can be considered measurable, and only a single state  $x_2$  needs to be estimated. Thus, the observer can be configured as a least-order observer. Compared to a full-order observer, the least-order observer offers the advantage of a simpler structure, as fewer states need to be estimated.

By reformulating (17) such that  $\dot{x}_2$  becomes the state to be estimated, the dynamics of the estimated state  $\hat{x}_2$  can be expressed as follows, considering the error between the estimated and actual parameters:

$$\hat{x}_2 = A_{21}x_1 + A_{22}\hat{x}_2 + b_2u + K(\hat{y} - \hat{\dot{y}}) \quad (18)$$

The derivative of estimation error  $\dot{e}$  can then be derived as

$$\dot{e} = (\dot{x}_2 - \dot{\hat{x}}_2) = (A_{22} - KA_{12})e \quad (19)$$

Here, if  $A_{12}$  and  $A_{22}$  satisfy the observability condition, the placement of the observer poles can be determined according to the design of the observer gain  $K$ . Therefore,

$K$  must be selected such that the system remains stable, ensuring that the estimation error  $e$  converges to zero.

To eliminate the derivative term in (19) and simplify the expression, a new parameter  $\xi$  is introduced, redefining  $\hat{x}_2$  as

$$\hat{x}_2 = \xi + Ky \quad (20)$$

Substituting (20) into (19) and rearranging yields

$$\dot{\xi} = \dot{\hat{x}}_2 - K\dot{y} = (A_{22} - KA_{12})\xi + (B_2 - KB_1)u + (A_{21} - KA_{11})y \quad (21)$$

The value of the parameter  $\xi$  can be obtained by applying an integrator to the result of (21). Finally, substituting  $\xi$  into (20) allows the estimation of the target variable  $\hat{x}_2$ .

For sensorless PMSM drive model-based inductance estimation, by applying the  $d$ -axis voltage equation from (1) to (17), a state-space model for estimating the  $q$ -axis inductance which primarily affects flux saturation can be expressed as follows:

$$\begin{bmatrix} \dot{i}_\gamma \\ \dot{\hat{L}}_q \end{bmatrix} = \begin{bmatrix} -\frac{R_a}{L_d} & \frac{\omega i_\delta}{L_d} \\ 0 & s \end{bmatrix} \begin{bmatrix} i_\gamma \\ \hat{L}_q \end{bmatrix} + \begin{bmatrix} \frac{1}{L_d} \\ 0 \end{bmatrix} v_\gamma + K \begin{bmatrix} 0 \\ \dot{y} - \hat{y} \end{bmatrix} \quad (22)$$

$$y = Cx = \begin{bmatrix} 1 & 0 \end{bmatrix} \begin{bmatrix} i_\gamma \\ \hat{L}_q \end{bmatrix} = i_\gamma$$

where  $i_\gamma$  corresponds to the observable variable  $y$ , which represents the output of the state equation;  $\hat{L}_q$  corresponds to the variable  $x_2$ , which represents the  $q$ -axis inductance to be estimated; and  $v_\gamma$  corresponds to the input variable  $u$  of the state equation, representing the  $\gamma$ -axis voltage. In addition, each component of the state matrix, serves as weighting constants of the state equation, is represented as  $A_{11}$ ,  $A_{12}$ ,  $A_{22}$ , and  $B_1$  in (17).

Using (20) and (21), the derivative of the parameter  $\xi$  can be expressed as

$$\dot{\xi} = \hat{L}_q - K\dot{i}_\gamma \quad (23)$$

$$\dot{\xi} = \left( s - K\frac{\omega i_\delta}{L_d} \right) \xi - \frac{K}{L_d} v_\gamma + \left( \left( s + \frac{R_a}{L_d} \right) K - \frac{\omega i_\delta K^2}{L_d} \right) i_\gamma \quad (24)$$

From (24), the parameter  $\xi$  can be approximated as

$$\xi \simeq \frac{R_a i_\gamma + L_d \dot{i}_\gamma - v_\gamma}{\omega i_\delta} \quad (25)$$

Therefore, by substituting (23) into (25), the estimated  $q$ -axis inductance, which is the observer's target variable, is obtained as

$$\hat{x}_2 = \hat{L}_q = \xi + Ky = \frac{R_a i_\gamma + L_d \dot{i}_\gamma - v_\gamma}{\omega i_\delta} + K i_\gamma \quad (26)$$

If this estimation equation is directly applied, the derivative term introduces significant noise and degrades the harmonic characteristics. Therefore, as expressed in (27), introducing a first-order low-pass filter minimizes the influence of the pole term in the numerator, thereby improving the noise performance of the estimated parameter. Furthermore, by adding the component obtained by multiplying the observer gain  $K$  with the state

equation output variable  $i_\gamma$ , the offset and gain of the estimated parameter can be adjusted, leading to a reduction in system error.

$$\hat{L}'_q = \left( \frac{R_a i_\gamma + L_a \dot{i}_\gamma - v_\gamma}{\omega i_\delta} \right) \left( \frac{1}{1 + \tau_0 s} \right) + K i_\gamma \quad (27)$$

where  $\tau_0$  denotes the time constant of the first-order low-pass filter.

However, the additional lag components and signal distortion introduced by the low-pass filter and the associated computational process increase the time delay, thereby degrading the accuracy of the real-time control loop. In particular, when periodic load signals or overloads are applied due to external conditions, cumulative errors caused by the time delay occur, leading to deviations from the actual values.

To address these issues, this study applies a time-delay compensation method based on coherence and correlation slope to the least-order observer. This approach aims to improve the accuracy of parameter estimation while maintaining the simplicity and efficiency of the observer structure.

When the original reference signal is defined as

$$y_1(t) = A \sin(2\pi f_0 t) \quad (28)$$

the signal estimated through the observer,  $y_2(t)$ , exhibits distortion along with a delay of  $d$  steps and can be expressed as

$$y_2(t) = \hat{y}_1(t) = s_1(t - dT_s) + \varepsilon(t) \quad (29)$$

where  $f_0 = 16.67$  Hz is the fundamental frequency,  $T_s$  is the sampling period,  $d$  represents the actual delay in steps, and  $\varepsilon(t)$  denotes measurement noise and DC offset. By accurately estimating the time delay  $\hat{d} = d$  and applying time-delay compensation, the performance of the observer-based inductance estimation can be significantly improved.

The target signal was selected as a periodic signal with at least  $n$  cycles to ensure estimation accuracy and averaging. The delayed signal  $y_2(t)$  can be defined as a set of  $N = n + 1$  segments as follows:

$$y_2(t) = \bigcup_{k=1}^{N} y_{2,k}(t), \quad k = 1, \dots, n + 1 \quad (30)$$

The magnitude-squared coherence between the original signal  $y_1(t)$  and the delay-compensated signal  $y_{2,k}(t + \delta T_s)$  is calculated as [23]

$$C_{xy}(f, \delta) = \frac{|P_{xy}(f, \delta)|^2}{P_{xx}(f)P_{yy}(f, \delta)}, \quad 0 \le C_{xy}(f, \delta) \le 1 \quad (31)$$

where  $P_{xy}(f, \delta)$  is the cross-spectral density, and  $P_{xx}(f)$  and  $P_{yy}(f, \delta)$  are the auto-spectral densities of  $y_1(t)$  and  $y_{2,k}(t + \delta T_s)$ , respectively.

For each segment  $k$ , by varying the delay compensation step  $\delta \in [1, 2, \dots, \delta_{max}]$ , the candidate step  $\delta_k^{coh}$  that maximizes the coherence for each segment is determined as

$$\delta_k^{coh} = \arg \max_{\delta \in [1, 2, \dots, \delta_{max}]} C_{xy}(f, \delta) \quad (32)$$

While applying coherence alone can reveal the linear relationship between two signals in specific frequency bands, it represents a statistical average over frequency and does not capture noise, nonlinear distortion, or local variations in the time domain. Therefore, to

compensate not only for frequency-domain linearity but also for signal nonlinearity and real-time degradation, the Pearson correlation coefficient between the two signals in the time domain is analyzed and corrected, as expressed in [24]

$$\rho_k(\delta) = \frac{\sum_t (y_1(t) - \bar{y}_1)(y_{2,k}(t + \delta T_s) - \bar{y}_{2,k})}{\sqrt{\sum_t (y_1(t) - \bar{y}_1)^2} \sqrt{\sum_t (y_{2,k}(t + \delta T_s) - \bar{y}_{2,k})^2}} \quad (33)$$

To further enhance the sensitivity of signal alignment and improve the precision of time-delay estimation, the slope (first derivative) of the correlation curve is estimated to identify the inflection point, as defined by

$$g_k(\delta) = \left| \frac{d}{d\delta} \rho_k(\delta) \right| \quad (34)$$

From this analysis, the step  $\delta_k^{cor}$  that minimizes the average slope of the correlation curve for each segment is selected:

$$\delta_k^{cor} = \min_{\delta} g_k(\delta) \quad (35)$$

The reference step  $\bar{\delta}^{cor}$  is obtained by averaging the results across all segments:

$$\bar{\delta}^{cor} = \frac{1}{N-1} \sum_{k=1}^{N-1} \delta_k^{cor} \quad (36)$$

Finally, among the coherence-based candidate steps, the value closest to the average Pearson correlation step  $\bar{\delta}^{cor}$  is selected as the final estimated delay step  $\hat{d}$ . Based on (36), the estimated time delay is then determined as:

$$\hat{d} = \arg \min_{\delta_k^{coh}} \left| \delta_k^{coh} - \bar{\delta}^{cor} \right| \quad (37)$$

Thus, by first setting a candidate region using coherence and then refining the estimate using the slope of the Pearson correlation to ensure robustness against noise and distortion, the precision of the time-delay estimation is improved.

$$\hat{\tau}_m = \hat{d} T_s \quad (38)$$

Based on the previously estimated time-delay information, a time-delay compensator including the feedback path was implemented to correct the observer output. By utilizing the dynamic model of the observer, the output is advanced by the estimated delay  $\hat{\tau}_m$ , enabling a real-time estimation model. This can be expressed as

$$\frac{\hat{Y}(s)}{Y(s)} = G_m(s) e^{-\hat{\tau}_m s} \quad (39)$$

where  $G_m(s)$  is the transfer function of the original model, and  $e^{-\hat{\tau}_m s}$  represents the delay compensation term.

Consequently, the final model output including the time-delay compensator can be expressed in the time domain as

$$\hat{y}_{1,comp}(t) = y_2(t + \hat{\tau}_m) \quad (40)$$

By compensating the observer signal  $s_2(t)$  by  $\hat{\tau}_m$ ,  $\hat{y}_1(t)$  becomes time-aligned with the original signal  $y_1(t)$ . As a result, the compensated output  $\hat{y}_{1,comp}(t)$  estimates the original 

signal instantaneously, significantly reducing estimation errors caused by the observer output delay.

Based on the algorithms presented in this chapter, the overall block diagram of the flux-saturation-compensated sensorless PMSM drive system designed to enhance inductance estimation performance is illustrated in Figure 1. In the inductance estimator, wavelet denoising selected according to the maximum energy-to-Shannon entropy criterion is employed to minimize distortions in the input signal of the least-order observer. In addition, a coherence- and correlation-based real-time delay compensator is applied to correct the time delay and offset errors in the observer output signal. Through this approach, inductance can be estimated with high accuracy, and the estimated flux value is fed back to suppress speed ripple and vibration.

![Figure 1: Overall block diagram of the flux-saturation-compensated sensorless PMSM drive system. The diagram shows a control loop starting with a reference speed ω_ref. This is compared with the estimated speed ω̂ in a Speed Controller, which outputs current references i_ys and i_δs. These are fed into a Current Controller, which produces voltage references V_ys and V_δs. These voltages are converted to three-phase voltages V_u, V_v, and V_w by a Vector Rotator. These voltages are then applied to a PMSM motor, which drives a Torque Load. The motor's stator currents i_as and i_δs are measured and fed back. A second Vector Rotator converts these currents into d-q components i_δ and i_γ. These are fed into a Sensorless Position and Speed Estimator, which also receives the estimated speed ω̂. The estimator outputs the estimated flux components Δê_γ and Δê_δ. These are fed into a Magnetic Saturation Compensator, which also receives the estimated speed ω̂. The compensator outputs the corrected flux components ΔL_d and ΔL_q. These are fed into an Inductance Estimator block. The Inductance Estimator block contains a Wavelet Denoising stage, a Least-Order Observer, and a Low-pass Filter. The output of the Low-pass Filter is fed into a Proposed Coherence- and Correlation-based Time Delay Compensator. The output of this compensator is fed back into the Sensorless Position and Speed Estimator. The Inductance Estimator block is also shown in detail, showing the flow from the current signals through the denoising and observer stages to the final estimation output.](d26959f4514c26ca19c3d6f00da85956_img.jpg)

Figure 1: Overall block diagram of the flux-saturation-compensated sensorless PMSM drive system. The diagram shows a control loop starting with a reference speed ω\_ref. This is compared with the estimated speed ω̂ in a Speed Controller, which outputs current references i\_ys and i\_δs. These are fed into a Current Controller, which produces voltage references V\_ys and V\_δs. These voltages are converted to three-phase voltages V\_u, V\_v, and V\_w by a Vector Rotator. These voltages are then applied to a PMSM motor, which drives a Torque Load. The motor's stator currents i\_as and i\_δs are measured and fed back. A second Vector Rotator converts these currents into d-q components i\_δ and i\_γ. These are fed into a Sensorless Position and Speed Estimator, which also receives the estimated speed ω̂. The estimator outputs the estimated flux components Δê\_γ and Δê\_δ. These are fed into a Magnetic Saturation Compensator, which also receives the estimated speed ω̂. The compensator outputs the corrected flux components ΔL\_d and ΔL\_q. These are fed into an Inductance Estimator block. The Inductance Estimator block contains a Wavelet Denoising stage, a Least-Order Observer, and a Low-pass Filter. The output of the Low-pass Filter is fed into a Proposed Coherence- and Correlation-based Time Delay Compensator. The output of this compensator is fed back into the Sensorless Position and Speed Estimator. The Inductance Estimator block is also shown in detail, showing the flow from the current signals through the denoising and observer stages to the final estimation output.

**Figure 1.** Overall block diagram of the flux-saturation-compensated sensorless PMSM drive system.

# 4. Experiment Results

Simulations were carried out using PSIM software to analyze and compare the inductance estimation performance and speed ripple characteristics according to inductance estimation and compensation methods under flux-saturation conditions in sensorless PMSM control. As shown in the control simulation block diagram in Figure 2, the main MCU-based controller equivalent to the actual dual-motor drive system was implemented. The dual motors share identical specifications: Motor model 1 corresponds to the machine employed for the sensorless drive, while motor model 2 serves as the load-torque generation machine. The controller was modeled and compiled in C language using the General DLL block in PSIM, generating a DLL file for co-simulation. In addition, specific signal-processing functions, such as wavelet denoising and time delay analysis, were interfaced with MATLAB R2024b for data processing and system integration.

The main parameters of the PMSM applied to the simulation and experiments are presented as shown in Table 1.

![Figure 2: Detailed Block Diagram for the Control Simulation Environment. The diagram shows two main software environments: Matlab Software and PSIM Software. Matlab Software contains 'Wavelet Denoising with Shannon Entropy' and 'Coherence- and Correlation-based Time Delay Analysis' blocks. PSIM Software contains 'Motor Model 1', 'Inverter for Sensorless Drive', 'Inverter for Load Torque', and 'Motor Model 2' blocks. A 'Main MCU Controller (DLL Block)' is located within PSIM Software, containing 'Dual Motor Drives', 'Sensor Interface', 'Parameter Definition', and 'Theta Estimation' sub-blocks. Bidirectional arrows indicate data exchange between Matlab Software and the Main MCU Controller, and between the Main MCU Controller and the PSIM blocks.](042733dc5e8e7f5f30b60adba3266cde_img.jpg)

Figure 2: Detailed Block Diagram for the Control Simulation Environment. The diagram shows two main software environments: Matlab Software and PSIM Software. Matlab Software contains 'Wavelet Denoising with Shannon Entropy' and 'Coherence- and Correlation-based Time Delay Analysis' blocks. PSIM Software contains 'Motor Model 1', 'Inverter for Sensorless Drive', 'Inverter for Load Torque', and 'Motor Model 2' blocks. A 'Main MCU Controller (DLL Block)' is located within PSIM Software, containing 'Dual Motor Drives', 'Sensor Interface', 'Parameter Definition', and 'Theta Estimation' sub-blocks. Bidirectional arrows indicate data exchange between Matlab Software and the Main MCU Controller, and between the Main MCU Controller and the PSIM blocks.

**Figure 2.** Detailed Block Diagram for the Control Simulation Environment.

**Table 1.** Motor parameters.

| Parameter            | Value | Unit     |
|----------------------|-------|----------|
| Rated power          | 3     | kW       |
| DC link voltage      | 400   | V        |
| Winding resistance   | 0.3   | $\Omega$ |
| Number of poles      | 6     | -        |
| Number of slots      | 27    | -        |
| $d$ -axis inductance | 1.5   | mH       |
| $q$ -axis inductance | 2.0   | mH       |

Figure 3 shows the simulation results of the inductance magnitude and the corresponding speed when the motor is operated at 1000 rpm (16.67 Hz) under load-torque compensation current. When the load-torque compensation current along the  $q$ -axis varies from 0 A to 30 A due to external periodic loads, as shown in Figure 3a, the real inductance continuously changes due to flux saturation, as indicated by the black line in Figure 3b. The blue line in Figure 3b represents the inductance estimated using the conventional least-order observer model, which is used to compensate for the inductance variation caused by flux saturation. In this least-order observer-based inductance estimation, the influence of the low-pass filter and integration introduces time delay and DC offset, increasing the uncertainty of the parameter estimation. If this varying inductance component is not properly estimated and compensated, the estimated speed exhibits significant ripples exceeding  $\pm 100$  rpm, accounting for more than 10% of the speed reference, as shown in Figure 3c.

The primary cause of the issues is, as previously described, the distortion of the input signal to the conventional least-order observer and the time delay in its output. To minimize the distortion of the observer input signal, a wavelet filter was applied as a preprocessing stage. Wavelet denoising was performed on the collected voltage and current data using the maximum energy-to-Shannon entropy criterion to select the optimal mother wavelet function. The candidate mother wavelets tested for this purpose included Daubechies, Symlet, Coiflet, and Biorthogonal wavelets. In addition, considering the signal's noise level for the selected mother wavelet, the decomposition level was set to 4 for current and 8 for voltage.

Table 2 presents the set of candidate mother wavelets and the mother wavelets selected based on the maximum energy-to-Shannon entropy criterion. For each candidate, the energy and Shannon entropy of the motor signals were computed, and the corresponding maximum energy-to-Shannon entropy ratio  $R(s)$  was evaluated. The selected mother wavelets, db1 as a Daubechies variant and Sym4 as a Symlet variant, were subsequently

employed for real-time noise filtering of current and voltage signals in the sensorless PMSM drive system.

![Figure 3: Simulation results showing (a) δ-axis current, (b) q-axis inductance, and (c) estimated speed over time (0.1 to 0.5 s) under load fluctuation at 16.7 Hz. (a) shows current oscillating between -10 and 40 A. (b) shows inductance oscillating between 0.0016 and 0.0032 H, comparing real (black) and least-order observer (blue) signals. (c) shows speed oscillating between 800 and 1200 rpm.](98ee20ceb85cd84e2415b20b1eda1bcf_img.jpg)

Figure 3: Simulation results showing (a) δ-axis current, (b) q-axis inductance, and (c) estimated speed over time (0.1 to 0.5 s) under load fluctuation at 16.7 Hz. (a) shows current oscillating between -10 and 40 A. (b) shows inductance oscillating between 0.0016 and 0.0032 H, comparing real (black) and least-order observer (blue) signals. (c) shows speed oscillating between 800 and 1200 rpm.

**Figure 3.** Simulation results when the load fluctuated at 16.7 Hz for (a)  $\delta$ -axis current, (b)  $q$ -axis inductance, and (c) estimated speed.

**Table 2.** Selection of mother wavelets for currents and voltage.

| Candidate Wavelet | $R(s)$ (for Currents) |
|-------------------|-----------------------|
| db1               | 392,069               |
| db2               | 236,824               |
| Sym4              | 259,718               |
| Coif1             | 309,098               |
| Bior1.3           | 267,255               |
| Candidate Wavelet | $R(s)$ (for Voltage)  |
| db1               | 106,884               |
| db2               | 94,556                |
| Sym4              | 244,786               |
| Coif1             | 121,543               |
| Bior1.3           | 54,602                |

Figure 4 presents the results with and without applying the wavelet filter using the selected mother wavelet db1 for denoising the least-order observer input variables  $I_\gamma$  and  $I_\delta$ .

![Figure 4: Comparison of input current signals I_gamma and I_delta. (a) with wavelet filtering and (b) without wavelet filtering. Both plots show Current [A] on the y-axis (ranging from -10 to 40) and Time [sec] on the x-axis (ranging from 0.1 to 0.5). In (a), the signal I_gamma (solid black line) is smooth, while I_delta (dashed blue line) is noisy. In (b), both signals are highly noisy.](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 4: Comparison of input current signals I\_gamma and I\_delta. (a) with wavelet filtering and (b) without wavelet filtering. Both plots show Current [A] on the y-axis (ranging from -10 to 40) and Time [sec] on the x-axis (ranging from 0.1 to 0.5). In (a), the signal I\_gamma (solid black line) is smooth, while I\_delta (dashed blue line) is noisy. In (b), both signals are highly noisy.

**Figure 4.** Comparison of input current signals  $I_\gamma$  and  $I_\delta$  (a) with wavelet filtering and (b) without wavelet filtering.

Similarly, Figure 5 presents the results with and without applying the wavelet filter using the selected mother wavelet Sym4 for denoising another input variable,  $V_\gamma$ .

![Figure 5: Comparison of voltage signal V_gamma. (a) with wavelet filtering and (b) without wavelet filtering. Both plots show Voltage [V] on the y-axis (ranging from -20 to 5) and Time (s) on the x-axis (ranging from 0.1 to 0.5). In (a), the signal is smooth. In (b), the signal is highly noisy.](bafe3c344aef7f6f79dab49c9eca89a9_img.jpg)

Figure 5: Comparison of voltage signal V\_gamma. (a) with wavelet filtering and (b) without wavelet filtering. Both plots show Voltage [V] on the y-axis (ranging from -20 to 5) and Time (s) on the x-axis (ranging from 0.1 to 0.5). In (a), the signal is smooth. In (b), the signal is highly noisy.

**Figure 5.** Comparison of voltage signal  $V_\gamma$  (a) with wavelet filtering and (b) without wavelet filtering.

To improve the estimation accuracy of the conventional least-order observer, reliable estimates are required not only to compensate for distortions in the input signals but also for the time delay in the output signals. Therefore, to address the time-delay issue in the output signals, simulations and experiments were carried out based on the proposed methodology presented in Section 3.

First,  $y_1(t)$ ,  $y_2(t)$  in (28) and (29) were divided into multiple segments, and candidate values of the time delay were obtained by varying the delay in each segment and identifying the point at which the coherence reached its maximum. In addition, within the time domain, the transition region of the slope, where the correlation coefficient between the two signals was maximized in each segment, was identified and corrected, thereby enabling accurate estimation of the time delay even under non-stationary signals.

Figure 6 presents the coherence comparison results across segments for compensating the output signal time delay in the least-order observer model. The number of segments  $N$  in (30) was set to 10, and by varying the size of the time step for time-delay compensation, the step size at which the maximum coherence occurred in each segment was identified as a candidate time-delay step. Among these, the segments corresponding to the minimum and maximum delay steps were excluded, and the remaining eight segment delay steps were selected as the final candidate step  $\delta_k^{coh}$ .

![Figure 6: Bar chart showing Estimated Delay (Step) versus No. of Segment. The y-axis ranges from 0 to 30. The x-axis shows segments 1 through 10. Each segment has a blue bar representing 'Steps' and a red dashed line representing 'Average'. The average values are approximately: Segment 1: 22.5, Segment 2: 21.5, Segment 3: 22.5, Segment 4: 22.0, Segment 5: 18.5, Segment 6: 20.5, Segment 7: 23.5, Segment 8: 24.5, Segment 9: 22.5, Segment 10: 23.5.](fe753d01ad5fe6cf150018c958173c6d_img.jpg)

Figure 6: Bar chart showing Estimated Delay (Step) versus No. of Segment. The y-axis ranges from 0 to 30. The x-axis shows segments 1 through 10. Each segment has a blue bar representing 'Steps' and a red dashed line representing 'Average'. The average values are approximately: Segment 1: 22.5, Segment 2: 21.5, Segment 3: 22.5, Segment 4: 22.0, Segment 5: 18.5, Segment 6: 20.5, Segment 7: 23.5, Segment 8: 24.5, Segment 9: 22.5, Segment 10: 23.5.

**Figure 6.** Comparison of estimated time-delay steps obtained from segment-based coherence analysis.

Figure 7 presents the segment-based comparison results for selecting the step that shows the highest linearity and correlation in the time domain, which cannot be fully captured by coherence analysis. By considering the first derivative of the correlation coefficient, the inflection point where the average slope of the curve was minimized was identified, thereby enabling the determination of the exact time at which the time delay was minimized in the time domain. Finally, based on the average of the results from the ten segments, the reference step  $\delta^{cor}$  was determined to be 22.3.

![Figure 7: Line graph showing Correlation Coefficient versus No. of delay steps. The y-axis ranges from 0.85 to 1.0. The x-axis ranges from 0 to 40. Ten segments are plotted as colored lines. A red dashed vertical line at approximately 22.3 is labeled with the symbol delta^{cor}. The correlation coefficients for the segments are: Segment 1: ~0.87, Segment 2: ~0.88, Segment 3: ~0.89, Segment 4: ~0.90, Segment 5: ~0.91, Segment 6: ~0.92, Segment 7: ~0.93, Segment 8: ~0.94, Segment 9: ~0.95, Segment 10: ~0.96.](cc8bec39d25eb0aafb5382c05f0d5deb_img.jpg)

Figure 7: Line graph showing Correlation Coefficient versus No. of delay steps. The y-axis ranges from 0.85 to 1.0. The x-axis ranges from 0 to 40. Ten segments are plotted as colored lines. A red dashed vertical line at approximately 22.3 is labeled with the symbol delta^{cor}. The correlation coefficients for the segments are: Segment 1: ~0.87, Segment 2: ~0.88, Segment 3: ~0.89, Segment 4: ~0.90, Segment 5: ~0.91, Segment 6: ~0.92, Segment 7: ~0.93, Segment 8: ~0.94, Segment 9: ~0.95, Segment 10: ~0.96.

**Figure 7.** Inflection-point analysis of correlation coefficients across segments.

Finally, among the candidate steps obtained from the coherence-based analysis, the value closest to the average correlation-based step  $\delta^{cor}$  was selected and determined as the final estimated delay step  $\hat{d}$ . Accordingly, the final output delay time  $\hat{\tau}_m$  was obtained using (38), and the estimated time delay of the signals was compensated by applying (39) and (40).

Figure 8 presents the comparison results of the real and estimated inductance. Compared to the uncompensated case, the compensated inductance estimate closely follows the real signal without delay, and the estimation error caused by the observer output delay is significantly reduced.

![Figure 8: Comparison of real and estimated inductances. The plot shows Inductance (H) on the y-axis (scaled by 10^-3) versus Time (sec) on the x-axis. Three curves are shown: 'Real' (black solid line), 'Least-order observer' (blue dashed line), and 'Proposed' (red solid line). The 'Real' and 'Proposed' curves are nearly identical, while the 'Least-order observer' curve shows a noticeable delay and deviation.](cbc4516eb885829fe8c9dabc0946dcbe_img.jpg)

Figure 8: Comparison of real and estimated inductances. The plot shows Inductance (H) on the y-axis (scaled by 10^-3) versus Time (sec) on the x-axis. Three curves are shown: 'Real' (black solid line), 'Least-order observer' (blue dashed line), and 'Proposed' (red solid line). The 'Real' and 'Proposed' curves are nearly identical, while the 'Least-order observer' curve shows a noticeable delay and deviation.

Figure 8. Comparison of real and estimated inductances.

Figure 9 and Table 3 present a comparison of the mean error (MSE) and root mean square error (RMSE) of the time-delay estimates obtained by applying the proposed coherence- and correlation-based approach and the conventional least-order observer. The experimental results show that the proposed coherence- and correlation-based time-delay estimation method significantly improves accuracy by simultaneously considering both frequency- and time-domain signal characteristics.

![Figure 9: Comparison of time-delay compensation results. A bar chart showing Performance Metrics (scaled by 10^-4) for RMSE (blue bars) and MAE (orange bars) for two cases: 'Least-order observer' and 'Proposed'. The 'Proposed' method shows significantly lower error metrics.](011fecb4a85637472f0c697a6cbdb15d_img.jpg)

| Case                 | RMSE [H] ( $\times 10^{-4}$ ) | MAE [H] ( $\times 10^{-4}$ ) |
|----------------------|-------------------------------|------------------------------|
| Least-order observer | ~1.6                          | ~1.4                         |
| Proposed             | ~0.6                          | ~0.5                         |

Figure 9: Comparison of time-delay compensation results. A bar chart showing Performance Metrics (scaled by 10^-4) for RMSE (blue bars) and MAE (orange bars) for two cases: 'Least-order observer' and 'Proposed'. The 'Proposed' method shows significantly lower error metrics.

Figure 9. Comparison of time-delay compensation results.

Table 3. Numerical results of time-delay compensation.

| Case                 | Metrics                 |                         |
|----------------------|-------------------------|-------------------------|
|                      | RMSE [H]                | MAE [H]                 |
| Least-order observer | $1.6256 \times 10^{-4}$ | $1.3710 \times 10^{-4}$ |
| Proposed             | $6.1186 \times 10^{-5}$ | $4.8803 \times 10^{-4}$ |

Figure 10 illustrates the experimental setup based on a motor testbed. For the experiment, the compressor of a Sonata hybrid vehicle was disassembled, and two motors were fabricated and utilized. A dual inverter was also developed to independently control each motor. In addition, since the load was represented through torque control, a periodic load torque current was generated by supplying  $q$ -axis current to the load motor, thereby

emulating a varying load-torque environment. The inverter system for driving the motor was implemented using a TI TMS320F28335 MCU. The IRFP4868PbF was employed as the power MOSFET for the three-phase inverter, while ACS758KCB-150B sensors were used for three-phase current measurement, providing sufficient margin to withstand potential spike components during inverter switching. In addition, auxiliary circuits, including noise-reduction filters and communication interfaces for motor drive control, were incorporated into the experimental setup. Real-time data communication and monitoring between the MCU and the PC were established via a serial communication interface. The output signals of key variables, such as the estimated inductance and speed, were continuously monitored using a four-channel digital-to-analog converter (DAC) and observed on an oscilloscope to verify system performance.

![Figure 10: Experimental testbed for real-time inductance estimation. The setup includes an Oscilloscope, a Control PC, an Inverter, a Motor Testbed, and a Power Supply.](6cc4a2d5ea0462e4825d57bd689bd2b3_img.jpg)

The image shows a laboratory setup for motor control experiments. On the left, a desk holds an oscilloscope and a computer monitor displaying data. Cables connect these to an inverter unit. To the right, a motor testbed is mounted on a stand, connected to a power supply unit. Labels with leader lines identify each component: Oscilloscope, Control PC, Inverter, Motor Testbed, and Power Supply.

Figure 10: Experimental testbed for real-time inductance estimation. The setup includes an Oscilloscope, a Control PC, an Inverter, a Motor Testbed, and a Power Supply.

**Figure 10.** Experimental testbed for real-time inductance estimation.

Figure 11 shows the experimental rotor speed results of the sensorless PMSM drive under magnetic saturation induced by an external load. The motor was operated at a constant speed of 1000 rpm, and without inductance estimation compensation, a ripple of approximately  $\pm 100$  rpm was observed in the estimated speed. In the case of sensorless control using the conventional least-order observer scheme based on the least-order observer, the speed ripple was reduced to less than half compared with the uncompensated case; however, its magnitude still exceeded  $\pm 50$  rpm. In contrast, when the proposed compensation control was applied, the ripple amplitude was significantly reduced to within  $\pm 40$  rpm. These results demonstrate that the proposed control strategy effectively suppresses speed fluctuations by approximately 20%, owing to its accurate estimation and compensation of magnetic saturation.

![Figure 11: Experimental results under magnetic saturation. (a) q-axis current vs. time, showing a sinusoidal waveform with amplitude around 30A. (b) Speed (rpm) vs. time, comparing three cases: Without compensation (solid black line), Least-order observer (dashed blue line), and Proposed (dashed red line). The proposed method shows the lowest speed ripple.](62ad98a4bc47922b5cf47de04571dae8_img.jpg)

Figure 11 consists of two subplots. Subplot (a) shows the q-axis current in Amperes (A) versus time in seconds (s). The current is a sinusoidal waveform with a peak amplitude of approximately 30 A, centered around 20 A. Subplot (b) shows the rotor speed in revolutions per minute (rpm) versus time in seconds (s). The speed is compared for three cases: 'Without compensation' (solid black line), 'Least-order observer' (dashed blue line), and 'Proposed' (dashed red line). All three cases start at approximately 1000 rpm. The 'Without compensation' case shows significant speed ripple, fluctuating between approximately 900 and 1100 rpm. The 'Least-order observer' case shows a reduction in ripple, fluctuating between approximately 950 and 1050 rpm. The 'Proposed' case shows the smallest ripple, fluctuating between approximately 980 and 1020 rpm.

Figure 11: Experimental results under magnetic saturation. (a) q-axis current vs. time, showing a sinusoidal waveform with amplitude around 30A. (b) Speed (rpm) vs. time, comparing three cases: Without compensation (solid black line), Least-order observer (dashed blue line), and Proposed (dashed red line). The proposed method shows the lowest speed ripple.

**Figure 11.** Experimental results under magnetic saturation for (a)  $q$ -axis current and (b) speed comparison with and without compensation.

Figure 12 presents the experimental results comparing the vibration magnitude with and without the proposed real-time magnetic saturation compensation. The motor speed was increased from a low speed of 200 rpm up to 2400 rpm, and the tests were conducted in both the horizontal and vertical directions. The experimental results show that when the real-time inductance estimation-based flux-saturation compensation was applied, the vibration magnitude was reduced by an average of 2–3 dB compared with the baseline, which corresponds to the ‘Without compensation’ case. In particular, a reduction exceeding 5 dB relative to the baseline was observed in the low-speed region below 500 rpm. Since the fluctuating load currents are applied under the same conditions regardless of speed, the influence of inductance variation caused by flux saturation becomes more pronounced at low speeds. Consequently, flux-saturation compensation is particularly effective in reducing vibration in the low-speed region.

![Figure 12(a): Horizontal vibration characteristics. The graph plots Acceleration (dB) on the y-axis (50 to 90) against Speed (rpm) on the x-axis (200 to 2400). Two lines are shown: 'Without compensation' (solid black line) and 'Proposed' (dashed blue line). The 'Proposed' line is consistently lower than the 'Without compensation' line, indicating reduced vibration. A significant peak in the 'Without compensation' line occurs around 600 rpm, which is notably lower in the 'Proposed' line.](1a6a826cc13d4e964b7bda69508d78e6_img.jpg)

Figure 12(a): Horizontal vibration characteristics. The graph plots Acceleration (dB) on the y-axis (50 to 90) against Speed (rpm) on the x-axis (200 to 2400). Two lines are shown: 'Without compensation' (solid black line) and 'Proposed' (dashed blue line). The 'Proposed' line is consistently lower than the 'Without compensation' line, indicating reduced vibration. A significant peak in the 'Without compensation' line occurs around 600 rpm, which is notably lower in the 'Proposed' line.

(a)

![Figure 12(b): Vertical vibration characteristics. The graph plots Acceleration (dB) on the y-axis (50 to 100) against Speed (rpm) on the x-axis (200 to 2400). Two lines are shown: 'Without compensation' (solid black line) and 'Proposed' (dashed blue line). Similar to the horizontal case, the 'Proposed' line shows a reduction in vibration magnitude across the speed range, with a prominent peak around 600 rpm that is significantly suppressed.](df7cb4ea9bd6c3f445f3e264773b125f_img.jpg)

Figure 12(b): Vertical vibration characteristics. The graph plots Acceleration (dB) on the y-axis (50 to 100) against Speed (rpm) on the x-axis (200 to 2400). Two lines are shown: 'Without compensation' (solid black line) and 'Proposed' (dashed blue line). Similar to the horizontal case, the 'Proposed' line shows a reduction in vibration magnitude across the speed range, with a prominent peak around 600 rpm that is significantly suppressed.

(b)

**Figure 12.** Vibration characteristics of sensorless PMSM drives with and without magnetic saturation compensation in (a) horizontal and (b) vertical directions (dB reference:  $10^{-5}$  (g)).

# 5. Conclusions

In this paper, a coherence- and correlation-based time delay compensation method is proposed following wavelet denoising preprocessing to achieve accurate real-time inductance estimation in a sensorless PMSM drive system. First, we employed a systematic approach to select the optimal mother wavelet using the maximum energy-to-Shannon entropy criterion in order to reduce noise in the PMSM drive system signals. Then, the time delay in the output of the least-order observer is compensated using a coherence- and correlation-based time delay estimation method. By applying the proposed technique, we could achieve a relatively simple yet accurate real-time estimation performance for the inductance parameters and experimentally verified that the sensorless control performance was efficiently enhanced compared to the conventional method. The proposed technique is expected to be utilized for parameter estimation and compensation control in various types of motor control systems in the future, as it is suitable for real-time embedded control system implementation due to its ability to adapt to diverse operating conditions, relatively fast computation speed, and high accuracy.

**Author Contributions:** Conceptualization, G.P. and J.B.; methodology, G.P. and J.B.; software, G.P.; validation, G.P. and J.B.; formal analysis, G.P. and J.B.; investigation, G.P. and J.B.; resources, G.P.; data curation, G.P.; writing—original draft preparation, G.P.; writing—review and editing, J.B.; visualization, G.P.; supervision, J.B.; project administration, J.B.; funding acquisition, G.P. and J.B. All authors have read and agreed to the published version of the manuscript.

**Funding:** This research was supported by the DGIST R&D Program of the Ministry of Science, ICT and Future Planning of Korea (25-IT-01) and research grants from Daegu Catholic University in 2025 (No. 20251084).

**Data Availability Statement:** The original contributions presented in the study are included in the article; further inquiries can be directed to the corresponding author.

**Conflicts of Interest:** The authors declare no conflicts of interest.

# References

- Morimoto, S.; Kawamoto, K.; Sanada, M.; Takeda, Y. Sensorless control strategy for salient-pole PMSM based on extended EMF in rotating reference frame. *IEEE Trans. Ind. Appl.* **2002**, *38*, 1054–1061. [\[CrossRef\]](#)
- Park, G.; Bae, J. Inductance Estimation Based on Wavelet-GMDH for Sensorless Control of PMSM. *Appl. Sci.* **2024**, *14*, 4386. [\[CrossRef\]](#)
- Zhu, Y.; Tao, B.; Xiao, M.; Yang, G.; Zhang, X.; Lu, K. Luenberger position observer based on deadbeat-current predictive control for sensorless PMSM. *Electronics* **2020**, *9*, 1325. [\[CrossRef\]](#)
- Hoia, H.K.; Chen, S.C.; Chang, C.F. Realization of the Neural Fuzzy Controller for the Sensorless PMSM Drive Control System. *Electronics* **2020**, *9*, 1371. [\[CrossRef\]](#)
- Morimoto, S.; Sanada, M.; Takeda, Y. Effects and Compensation of Magnetic Saturation in Flux-Weakening Controlled Permanent Magnet Synchronous Motor Drives. *IEEE Trans. Ind. Appl.* **1994**, *30*, 1632. [\[CrossRef\]](#)
- Bianchini, C.; Bisceglie, G.; Torreggiani, A.; Davoli, M.; Macrelli, E.; Bellini, A.; Frigieri, M. Effects of the Magnetic Model of Interior Permanent Magnet Machine on MTPA, Flux Weakening and MTPV Evaluation. *Machines* **2023**, *11*, 77. [\[CrossRef\]](#)
- Ahn, H.; Park, H.; Kim, C.; Lee, H. A Review of State-of-the-art Techniques for PMSM Parameter Identification. *J. Electr. Eng. Tech.* **2020**, *15*, 1177–1187. [\[CrossRef\]](#)
- Jeong, I.J.; Gu, B.G.; Kim, J.; Nam, K.; Kim, Y. Inductance Estimation of Electrically Excited Synchronous Motor via Polynomial Approximations by Least Square Method. *IEEE Trans. Ind. Appl.* **2015**, *51*, 1526–1537. [\[CrossRef\]](#)
- Ye, S.; Yao, X. A Modified Flux Sliding-Mode Observer for the Sensorless Control of PMSMs with Online Stator Resistance and Inductance Estimation. *IEEE Trans. Power Electron.* **2020**, *35*, 8652–8662. [\[CrossRef\]](#)
- Chaplaïs, F.; Tsiotras, P.; Jung, D. On-line wavelet denoising with application to the control of a reaction wheel system. In Proceedings of the American Institute of Aeronautics and Astronautics (AIAA) Guidance, Navigation, and Control Conference, Providence, RI, USA, 16–19 August 2004.
- Khorbotly, S.; Khalil, A.; Carletta, J.; Husain, I. A wavelet based denoising approach for real-time signal processing in switched reluctance motor drives. In Proceedings of the IEEE Industrial Electronics Society Annual Conference (IECON), Raleigh, NC, USA, 6–10 November 2005.
- Song, Y.; Ponci, F.; Monti, A.; Gao, L.; Dougal, R.A. A novel brushless DC motor speed estimator based on space frequency localized wavelet neural networks. In Proceedings of the IEEE Applied Power Electronics Conference and Exposition, Austin, TX, USA, 6–10 March 2005.
- Khan, M.; Radwan, T.S.; Rahman, M.A. Wavelet Packet Transform Based Protection of Three-Phase IPM Motor. In Proceedings of the IEEE International Symposium on Industrial Electronics, Montreal, QC, Canada, 9–13 July 2006.
- Khan, M.; Rahman, M.A. Implementation of a new wavelet controller for interior permanent magnet motor drives. *IEEE Trans. Ind. Appl.* **2008**, *44*, 1957–1965. [\[CrossRef\]](#)
- Saito, N. Simultaneous noise suppression and signal compression using a library of orthonormal bases and the minimum description length criterion. *Wavelet Anal. Its Appl.* **1994**, *4*, 299–324.
- Hamid, E.Y.; Mardiana, R.; Kawasaki, Z.I. Wavelet-based compression of power disturbances using the minimum description length criterion. In Proceedings of the IEEE Power Engineering Society Summer Meeting, Vancouver, BC, Canada, 15–19 July 2001.
- Singh, B.N.; Tiwari, A.K. Optimal selection of wavelet basis function applied to ECG signal denoising. *Digit. Signal Process.* **2006**, *16*, 275–287. [\[CrossRef\]](#)
- Yan, R.; Gao, R.X. Base Wavelet Selection for Bearing Vibration Signal Analysis. *Int. J. Wavelets Multiresolut. Inf. Process.* **2009**, *7*, 411–426. [\[CrossRef\]](#)

19. Kankar, P.K.; Sharma, S.C.; Harsha, S.P. Fault diagnosis of ball bearings using continuous wavelet transform. *Appl. Soft Comput.* **2011**, *11*, 2300–2312. [\[CrossRef\]](#)
20. Donoho, D.L. De-noising by soft-thresholding. *IEEE Trans. Inf. Theory* **1995**, *41*, 613–627. [\[CrossRef\]](#)
21. Donoho, D.L.; Johnstone, I.M. Ideal spatial adaptation by wavelet shrinkage. *Biometrika* **1994**, *81*, 425–455. [\[CrossRef\]](#)
22. Jonhstone, I.M.; Silverman, B.W. Wavelet threshold estimators for data with correlated noise. *J. R. Statis. Soc. Ser. B* **1997**, *59*, 319–351. [\[CrossRef\]](#)
23. Carter, G.C. Coherence and time delay estimation. *Proc. IEEE* **1987**, *75*, 236–255. [\[CrossRef\]](#)
24. Tóth, B.; Kertész, J. Accurate estimator of correlations between asynchronous signals. *Phys. A Stat. Mech. Its Appl.* **2009**, *389*, 5138–5149. [\[CrossRef\]](#)

**Disclaimer/Publisher’s Note:** The statements, opinions and data contained in all publications are solely those of the individual author(s) and contributor(s) and not of MDPI and/or the editor(s). MDPI and/or the editor(s) disclaim responsibility for any injury to people or property resulting from any ideas, methods, instructions or products referred to in the content.

