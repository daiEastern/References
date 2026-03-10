

## ORIGINAL RESEARCH

# Active disturbance rejection current controller with time delay compensation predictive ESO for aircraft PMSM drive

Chunqiang Liu<sup>1</sup> ![ORCID icon](003082e50e3009141f59bd5df831749f_img.jpg) | Zhiwen Zhao<sup>1</sup> | Yanfei You<sup>2</sup> | Xuechao Duan<sup>1</sup> | Lijun Chen<sup>3</sup> | Xi Xiao<sup>3</sup><sup>1</sup>Hangzhou Institute of Technology, Xidian University, Xi'an, China<sup>2</sup>Hebei Vocational University of Technology and Engineering, Xingtai, China<sup>3</sup>Aviation Key Laboratory of Science and Technology on Aero Electromechanical System Integration, Nanjing, China

## Correspondence

Chunqiang Liu, Hangzhou Institute of Technology, Xidian University, No.2 South Taibai Road, Xi'an, China.  
Email: liuchunqiang@xidian.edu.cn

## Funding information

National Natural Science Foundation of China, Grant/Award Number: 52407064

## Abstract

In this paper, the authors propose a novel active disturbance rejection current control method aimed at resolving inherent issues within the digital control system of an aircraft's permanent magnet synchronous motor (PMSM). These issues include a one-sample time delay and low-pass filter in the current measurement channel. The proposed method involves estimating the time delay using a predictive extended state observer (ESO) within the current loop of the PMSM to enhance anti-disturbance capabilities and robustness. Initially, a discrete-time model that takes current loop time delay into consideration is established. Subsequently, a predictive ESO is designed to estimate disturbances within the current loop. This ESO incorporates known model information to improve the accuracy and speed of disturbance estimation. Furthermore, compensation is made for the time delay stemming from the low-pass filter in the current measurement channel to enable real-time current detection. Lastly, the disturbance estimated by predictive ESO is combined with the feedback control law to form a model-enhanced active disturbance rejection current controller. The results from simulations and experiments validate the feasibility and accuracy of the proposed methodology.

## KEYWORDS

AC motor drives, active disturbance rejection control, permanent magnet motors

## 1 | INTRODUCTION

The aviation field is experiencing an increasing need for high-dynamic electro-mechanical actuation servo drive systems due to the rapid advancement of more electric aircraft [1, 2]. Figure 1 is a schematic diagram of the electro-mechanical actuation (EMA), comprising the flight control computer, actuator control unit, inverter power supply, and mechanical transmission device (reducer and screw). EMA drives the control surface by controlling the motor that drives the mechanical transmission device, such as the reducer and screw. The actuator control unit collects the position information of the permanent magnet synchronous motor and the linear variable differential transformer (LVDT)'s linear displacement information to complete high-speed position or speed closed-

loop control. The flight control computer issues a position or speed command to make the control surface deflect to the specified angle.

In aircraft applications, where weight and space constraints are critical, permanent magnet synchronous motors (PMSMs) offer exceptional advantages, including high torque density, efficiency, and reliability. The demand for high dynamic response of PMSM in aircraft electro-mechanical actuators is paramount [3]. These actuators are crucial components in aircraft actuation systems, requiring precise and rapid control over various manoeuvres and functions. The high dynamic response of PMSM currents ensures swift and accurate adjustments, enabling rapid and precise control of the actuators during critical flight operations, such as flight surface adjustments, landing gear deployment, and thrust vectoring.

This is an open access article under the terms of the [Creative Commons Attribution-NonCommercial-NoDerivs](https://creativecommons.org/licenses/by-nc-nd/4.0/) License, which permits use and distribution in any medium, provided the original work is properly cited, the use is non-commercial and no modifications or adaptations are made.

© 2025 The Author(s). *IET Electric Power Applications* published by John Wiley & Sons Ltd on behalf of The Institution of Engineering and Technology.

![Schematic diagram of aircraft electro-mechanical actuation system. The diagram shows a Flight control computer (green box) sending a Position command (1) to a Servo control unit (pink box). The Servo control unit also receives Control unit state (2), PMSM (3), and Nut-screw (4) signals. It is connected to an Electric power network (red box) and a Reducer (grey box). The Reducer is connected to an Airframe (yellow box) which has a PMSM Angle position (blue box) and an LVDT position (blue box). The Airframe is connected to a Surface (grey box) which shows Surface angle, Aerodynamic disturbance, Rotational motion, and Translational motion. A dashed line labeled 'Aircraft Response' points from the Flight control computer to the Surface.](aa9e46d6f962be5cebcbb5c654c9b13e_img.jpg)

Schematic diagram of aircraft electro-mechanical actuation system. The diagram shows a Flight control computer (green box) sending a Position command (1) to a Servo control unit (pink box). The Servo control unit also receives Control unit state (2), PMSM (3), and Nut-screw (4) signals. It is connected to an Electric power network (red box) and a Reducer (grey box). The Reducer is connected to an Airframe (yellow box) which has a PMSM Angle position (blue box) and an LVDT position (blue box). The Airframe is connected to a Surface (grey box) which shows Surface angle, Aerodynamic disturbance, Rotational motion, and Translational motion. A dashed line labeled 'Aircraft Response' points from the Flight control computer to the Surface.

**FIGURE 1** Schematic diagram of aircraft electro-mechanical actuation system.

Therefore, high-dynamic PMSM current controller to meet these demanding requirements is essential for enhancing aircraft performance, safety, and operational efficiency [4].

Current control is crucial for achieving high-dynamic torque control in PMSMs for aircraft EMA. The classical Proportional Integral (PI) controller is widely used in PMSM current control [5]. However, in complex operating environments, the performance of PI controllers may deteriorate due to variations in resistance and inductance parameters as well as the presence of unmodelled dynamics. A commonly used approach is variable-gain PI current control, where the control gains are adjusted to accommodate different operating conditions [6].

In order to improve the anti-interference performance of the current loop, various anti-disturbance control methods have been introduced. Active disturbance rejection control (ADRC) is an active control method, and multiple research studies have demonstrated its effectiveness in high-performance current control of PMSM drives [7, 8]. In ref. [9], a PMSM current loop strategy combining ADRC and sliding mode control is proposed and compared with PI control. Tian et al. [10] combine discrete-time repetitive control with ADRC to enhance the suppression capability of periodic disturbances. Chen et al. [11] propose a proportional resonant-type ADRC method for the current loop, introducing a proportional resonant term into the extended state observer (ESO) to effectively suppress current harmonics caused by inverter dead zones and motor magnetic field distribution harmonics. A non-linear extended state observer is designed to observe the current loop's disturbance to avoid the influence of PMSM parameters variation [12]. A quasi-proportional resonance error feedback controller and a disturbance differential compensation linear ESO are combined for suppressing the ac disturbance [13].

A primary factor limiting the further performance improvement of the ADRC-based current controller is the presence of time delays within the current loop, including the inherent one-sample time delay in digital control and the current measurement filter's time delay. Prediction mechanisms are effective measures to reduce the impact of the inherent one-sample delay in digital control and improve dynamic control performance [14–16]. Bai et al. [17] design a current prediction controller based on augmented internal model disturbance observer, achieving excellent transient response and disturbance

suppression in the presence of variations in resistance and inductance parameters. In current prediction control, compensation for the inherent one-sample time delay in digital control systems is achieved through one-sample prediction [18]. Gao et al. [19] discuss the impact of one-sample time delay on the performance of PMSM current control and proposes a time delay compensation method.

In addition to the one-sample ahead prediction approach, it is also possible to establish a mathematical model for the time delay in the current loop, including the one-sample delay and the delay introduced by pulse width modulation, and then design current controllers based on this time-delayed mathematical model [20]. Pan and Zhida [21] analyse the adverse effects of time delay elements on current control performance from a frequency domain perspective. To address this issue, a smith predictor-based current controller is proposed to improve the dynamic response of the PMSM current loop. Dongye [22] addresses the impact of one-sample delay in PMSM current loop using a second-order terminal sliding mode digital control and designs a Smith predictor. Wei et al. [23] propose a model predictive current control method using the Smith predictor mechanism to compensate for the one-sample delay. The deadbeat predictive current control performance damage caused by the parameter mismatches and time delay is discussed [24]. Xu et al. [25] propose a deadbeat predictive current controller with time-delay compensation.

The aforementioned studies on one-sample prediction and time-delay mathematical models focused on the inherent one-sample delay in digital control, without considering the influence of low-pass filters in current measurement channels. Within the framework of ADRC control, Liu et al. [26] address the influence of low-pass filters in current measurement channels. It inserts a low-pass filter with the same time constant as the current measurement into the control signal input channel of the current loop's ESO. This action aims to eliminate the time-delay mismatch between the two input channels of the ESO, resolving inaccuracies in disturbance compensation during dynamic processes. However, the time delay characteristics of the low-pass filter still exist. A comprehensive high-dynamic current control method considering the inherent one-sample delay in digital control, current measurement delay, and variations in motor parameters still requires further research.

This paper proposes an ADRC method for the current loop of PMSMs, incorporating predictive ESO to compensate for time delays. Considering both the inherent one-sample delay in the digital control system and the time delay of low-pass filters in current measurement channels, a discrete-time model of the PMSM current loop is established. An model compensated enhanced ESO is developed, which compensates for time delays in the current loop and reduces the negative impact of time delays on disturbance estimation by ESO. An ADRC current controller is designed, and its dynamic response as well as its robustness to variations in motor parameters are studied through simulation and experimental research.

## 2 | DESCRIPTION OF THE DISCRETE-DOMAIN MODEL OF THE CURRENT LOOP

### 2.1 | Analysis of current loop's time delays and disturbances

The mathematical model of a permanent magnet synchronous motor in the rotating coordinate system is as (1).

$$\begin{cases} u_d = R_s i_d + L_d \frac{di_d}{dt} - \omega_e L_q i_q + d_{d1}(t) \\ u_q = R_s i_q + L_q \frac{di_q}{dt} + \omega_e (\psi_r + L_{dq} i_d) + d_{q1}(t) \end{cases} \quad (1)$$

Where  $u_d$  and  $u_q$  are the voltages in the dq coordinate system,  $R_s$  is the motor resistance,  $i_d$  and  $i_q$  are the currents in the d-axis and q-axis,  $L_d$  and  $L_q$  are the d-axis and q-axis inductances,  $\omega_e$  is the electrical angular velocity,  $\psi_r$  is the magnetic flux of the permanent magnet,  $d_{d1}(t)$  and  $d_{q1}(t)$  are the unmodelled dynamics of the d-axis and q-axis respectively.

When considering variations in motor parameters due to factors such as temperature and load torque, the above model can be described as follows:

$$\begin{cases} u_d = R_{sn} i_d + L_{dn} \frac{di_d}{dt} - \omega_e L_{qn} i_q + d_d(t) \\ u_q = R_{sn} i_q + L_{qn} \frac{di_q}{dt} + \omega_e (\psi_m + L_{dn} i_d) + d_q(t) \\ d_d(t) = \Delta R i_d + \Delta L_d \frac{di_d}{dt} - \omega_e \Delta L_q i_q + d_{d1}(t) \\ d_q(t) = \Delta R i_q + \Delta L_q \frac{di_q}{dt} + \omega_e (\Delta L_d i_d + \Delta \psi_r) + d_{q1}(t) \end{cases} \quad (2)$$

Where  $R_{sn}$  is the nominal resistance value,  $\Delta R$  is the resistance perturbation value,  $L_{dn}$  and  $L_{qn}$  are the nominal values of the d-axis and q-axis inductances,  $\Delta L_d$  and  $\Delta L_q$  are the perturbation values of the d-axis and q-axis inductances,  $\psi_m$  is the nominal value of the permanent magnet flux,  $\Delta \psi_r$  is the perturbation value of the permanent magnet flux,  $d_d(t)$  and  $d_q(t)$  are the total disturbances on the d-axis and q-axis respectively.

The schematic diagram of the current loop time delay analysis for PMSM is shown in Figure 2, including the inherent one-sample time delay of digital control and the time delay caused by the low-pass filter for current measurement. In this paper, current measurement adopts a first-order low-pass filter  $1/(T_i s + 1)$ , where  $T_i$  represents the time constant of the low-pass filter.

The impact of time delay on current control mainly manifests in two aspects: firstly, it affects the stability of the current loop. Time delay decreases the phase margin of the current loop, weakening the stability of the control system, and causing oscillations in the step response of the current closed-loop.

![Figure 2: Analysis of time delay in PMSM current control. The diagram shows a block diagram of the current control loop. It starts with a 'Current control' block that outputs reference voltages u_d* and u_q*. These are fed into a 'one-baet delay' block. The outputs of the delay block are the actual voltages u_d and u_q. These voltages are then fed into a 'Motor model' block, which produces the currents i_d and i_q. The currents i_d and i_q are fed into a 'First-order low pass filter for current measurement channel' block, which outputs the filtered currents i_df and i_qf. These filtered currents are fed back into the 'Current control' block, completing the loop.](8239bdc2ad69faed67c2741625a1ca79_img.jpg)

Figure 2: Analysis of time delay in PMSM current control. The diagram shows a block diagram of the current control loop. It starts with a 'Current control' block that outputs reference voltages u\_d\* and u\_q\*. These are fed into a 'one-baet delay' block. The outputs of the delay block are the actual voltages u\_d and u\_q. These voltages are then fed into a 'Motor model' block, which produces the currents i\_d and i\_q. The currents i\_d and i\_q are fed into a 'First-order low pass filter for current measurement channel' block, which outputs the filtered currents i\_df and i\_qf. These filtered currents are fed back into the 'Current control' block, completing the loop.

FIGURE 2 Analysis of time delay in PMSM current control.

Secondly, it affects the dynamic control performance by slowing down the motor torque response.

### 2.2 | Modelling current loop with discrete domain analysis

By utilising Euler's method to discretise (1) and considering the one-sample time delay during the execution of the digital controller, the discrete-domain mathematical model of the permanent magnet synchronous motor with one-sample update time delay can be established as follows:

$$\begin{cases} i_d(k+1) = \left(1 - \frac{T_s R_s}{L_d}\right) i_d(k) + T_s \frac{\omega_e L_q i_q(k)}{L_d} \\ \quad + \frac{T_s}{L_d} u_d(k) - \frac{T_s}{L_d} d_{d1}(k) \\ i_{d1}(k+1) = i_d(k) \\ i_q(k+1) = \left(1 - \frac{T_s R_s}{L_q}\right) i_q(k) - T_s \frac{\omega_e (\psi_r + L_d i_d(k))}{L_q} \\ \quad + \frac{T_s}{L_q} u_q(k) - \frac{T_s}{L_q} d_{q1}(k) \\ i_{q1}(k+1) = i_q(k) \end{cases} \quad (3)$$

Where  $i_d(k+1)$  and  $i_q(k+1)$  represent the d-axis current and q-axis current at time  $k+1$ ,  $i_d(k)$  and  $i_q(k)$  represent the d-axis current and q-axis current at time  $k$ ,  $i_{d1}(k+1)$  and  $i_{q1}(k+1)$  represent the d-axis current and q-axis current after one-sample delay,  $T_s$  is the discretisation period, and  $u_d(k)$  and  $u_q(k)$  are the d-axis voltage and q-axis voltage at time  $k$ .

Taking into account the first-order low-pass filter in the current measurement channel, the expression for the filtered current is as follows:

$$\begin{cases} i_{df}(k+1) = \frac{T_i}{T_i + T_s} i_{df}(k) + \frac{T_s}{T_i + T_s} i_{d1}(k+1) \\ i_{qf}(k+1) = \frac{T_i}{T_i + T_s} i_{qf}(k) + \frac{T_s}{T_i + T_s} i_{q1}(k+1) \end{cases} \quad (4)$$

Where  $i_{df}(k+1)$  and  $i_{qf}(k+1)$  represent the d-axis current and q-axis current after passing through the low-pass filter at time  $k+1$ , and  $T_i$  is the time constant of the first-order low-pass filter.

## 3 | DISCRETE-TIME PREDICTIVE EXTENDED STATE OBSERVER WITH TIME DELAY COMPENSATION

To address the inherent one-sample time delay in digital control systems and the phase lag induced by current sampling low-pass filters, a predictive mechanism ESO is proposed to mitigate the delay effects.

Firstly, establish a current estimator based on known model information and measured currents as shown in Equation (5).

$$\begin{cases} \hat{i}_d^p(k+1) = \left(1 - \frac{T_s R_{sn}}{L_{dn}}\right) i_d(k) + T_s \frac{\omega_e L_{qn} i_q(k)}{L_{dn}} \\ \quad + \frac{T_s}{L_{dn}} u_d(k) \\ \hat{i}_q^p(k+1) = \left(1 - \frac{T_s R_{sn}}{L_{qn}}\right) i_q(k) - T_s \frac{\omega_e (\psi_m + L_{dn} i_d(k))}{L_{qn}} \\ \quad + \frac{T_s}{L_{qn}} u_q(k) \end{cases} \quad (5)$$

Where  $\hat{i}_d^p(k+1)$  and  $\hat{i}_q^p(k+1)$  represent the estimated d-axis current and q-axis current at time  $k+1$ .

Taking into account the inherent one-sample digital control time delay in the current loop control system, combined with the estimated current values represented by (5), the discrete time domain estimated values after one-sample delay are obtained as follows:

$$\begin{cases} \hat{i}_d^{p1}(k+1) = \hat{i}_d^p(k) \\ \hat{i}_q^{p1}(k+1) = \hat{i}_q^p(k) \end{cases} \quad (6)$$

Where  $\hat{i}_d^{p1}$  and  $\hat{i}_q^{p1}$  represent the predicted currents after one-sample time delay.

Further considering the influence of first-order low pass filters on the d-axis and q-axis current feedback channels,  $\hat{i}_d^{p1}(k+1)$  and  $\hat{i}_q^{p1}(k+1)$  pass through low-pass filters again as shown in (7).

$$\begin{cases} \hat{i}_d^{p2}(k+1) = \frac{T_i}{T_i + T_s} \hat{i}_d^{p1}(k) + \frac{T_s}{T_i + T_s} \hat{i}_d^{p1}(k+1) \\ \hat{i}_q^{p2}(k+1) = \frac{T_i}{T_i + T_s} \hat{i}_q^{p1}(k) + \frac{T_s}{T_i + T_s} \hat{i}_q^{p1}(k+1) \end{cases} \quad (7)$$

Where  $\hat{i}_d^{p2}$  and  $\hat{i}_q^{p2}$  represent the predicted currents after passing through the first-order low-pass filter.

To compensate for the time delay, it is necessary to extract the current lag information caused by the time delay of low

pass filters. This is achieved by subtracting the estimated currents based on the known model (5) from the current estimates considering the control system one-sample time delay and low-pass filter time delay (7). This yields the current lag error information as (8).

$$\begin{cases} e_d(k+1) = \hat{i}_d^p(k+1) - \hat{i}_d^{p2}(k+1) \\ e_q(k+1) = \hat{i}_q^p(k+1) - \hat{i}_q^{p2}(k+1) \end{cases} \quad (8)$$

Where  $e_d$  represents the influence of the time delay on the d-axis current, and  $e_q$  represents the influence of the time delay on the q-axis current.

The expression for the measured currents  $i_d(k)$  and  $i_q(k)$  after passing through a first-order low-pass filter is:

$$\begin{cases} i_{df}(k) = \frac{T_i}{T_i + T_s} i_{df}(k-1) + \frac{T_s}{T_i + T_s} i_d(k) \\ i_{qf}(k) = \frac{T_i}{T_i + T_s} i_{qf}(k-1) + \frac{T_s}{T_i + T_s} i_q(k) \end{cases} \quad (9)$$

Where  $i_{df}(k)$  and  $i_{qf}(k)$  represent the d-axis and q-axis current values after low-pass filtering at time  $k$ , and  $i_{df}(k-1)$  and  $i_{qf}(k-1)$  represent the d-axis and q-axis current values after low-pass filtering at time  $k-1$ .

The final predicted currents after compensating for the one-sample time delay in digital control and the low-pass filter time delay in current measurement are:

$$\begin{cases} \hat{i}_d^{p3}(k+1) = i_{df}(k) + e_d(k+1) \\ \hat{i}_q^{p3}(k+1) = i_{qf}(k) + e_q(k+1) \end{cases} \quad (10)$$

Where  $\hat{i}_d^{p3}$  and  $\hat{i}_q^{p3}$  represent the predicted current values after compensating for the time delay.

Based on the current prediction values after time delay compensation,  $\hat{i}_d^{p3}$  and  $\hat{i}_q^{p3}$ , the predictive ESO is designed as follows.

$$\begin{cases} \hat{e}_d(k) = \hat{i}_d(k) - \hat{i}_d^{p3}(k+1) \\ \hat{i}_d(k+1) = \hat{i}_d(k) + T_s \left( \frac{\left( -\frac{R_{sn} \hat{i}_d(k)}{L_{dn}} + \frac{\omega_e L_{qn} \hat{i}_q(k)}{L_{dn}} + \hat{d}_d(k) \right)}{\frac{u_d(k)}{L_{dn}} - l_1 \hat{e}_d(k)} \right) \\ \hat{d}_d(k+1) = \hat{d}_d(k) - T_s l_2 \hat{e}_d(k) \\ \hat{e}_q(k) = \hat{i}_q(k) - \hat{i}_q^{p3}(k+1) \\ \hat{i}_q(k+1) = \hat{i}_q(k) + T_s \left( \frac{\left( -\frac{R_{sn} \hat{i}_q(k)}{L_{qn}} - \frac{\omega_e (\psi_m + L_{dn} \hat{i}_d(k))}{L_{qn}} \right)}{\frac{u_q(k)}{L_{qn}} + \hat{d}_q(k) - l_1 \hat{e}_q(k)} \right) \\ \hat{d}_q(k+1) = \hat{d}_q(k) - T_s l_2 \hat{e}_q(k) \end{cases} \quad (11)$$

Where  $l_1$  and  $l_2$  are the ESO's gains.

The block diagram of the time delay compensation predictive ESO is depicted in Figure 3. Initially, prediction is conducted based on known model information to obtain the current prediction without time delay. Subsequently, considering the one-sample time delay and the time delay caused by the first-order low-pass filter in current measurement, the filtered predicted current is derived. The difference between the current prediction without delay and the filtered predicted current yields the influence of time delay. Then, this influence is combined with the current from the sampling channel after passing through a first-order low-pass filter to obtain the time delay compensated current, which is fed into the model-enhanced extended state observer for disturbance estimation.

## 4 | MODEL-ENHANCED ACTIVE DISTURBANCE REJECTION CURRENT CONTROLLER DESIGN AND ANALYSIS

### 4.1 | Model-enhanced ADRC controller design

Based on the aforementioned predictive ESO, design the model-enhanced active disturbance rejection current controller as in equation (12), which includes current error feedback, disturbance compensation, and known model information compensation.

$$\begin{cases} u_d^*(k+1) = k_1(i_d^* - \hat{i}_d(k)) - \frac{1}{L_{dn}}\hat{d}_d(k) + R_{sn}\hat{i}_d(k) \\ \quad - \omega_e L_{qn}\hat{i}_q(k) \\ u_q^*(k+1) = k_2(i_q^* - \hat{i}_q(k)) - \frac{1}{L_{qn}}\hat{d}_q(k) + R_{sn}\hat{i}_q(k) \\ \quad + \omega_e(\psi_m + L_{dn}\hat{i}_d(k)) \end{cases} \quad (12)$$

Where  $k_1$  and  $k_2$  are feedback control gains.

Therefore, based on the predictive ESO compensating for time delay, the block diagram of the ADRC for the current loop of PMSM is shown in Figure 4. The inputs are the desired values of the d-axis current  $i_d^*$  and the q-axis current  $i_q^*$ , while the outputs are the desired d-axis voltage  $u_d^*$  and q-axis voltage  $u_q^*$ .

### 4.2 | Frequency domain analysis

To compare the current control characteristics before and after time delay compensation, this section employs a frequency domain approach and analyses through Bode plots. The parameters of the PMSM used in frequency domain analysis, simulation and experiments are listed in Table 1. The control period  $T_s$  of the current loop is 100 us. The time constant of first-order low-pass filter  $T_1 = 0.0002$ . The first-order low-

![Block diagram of predictive ESO with time delay compensation. The diagram shows a 'Predictive ESO' block (dashed line) containing a 'model-enhanced ESO' (Eq.11). Inputs to the ESO are from a 'PMSM model' (Eq.1) and a 'predicting currents using known model' (Eq.5). The ESO outputs 'estimated current' and 'estimated disturbance'. The 'estimated current' is fed into a 'Model-enhanced ADRC current control' (Eq.12) block. This block also receives 'estimated disturbance' and 'current error feedback'. The output of the ADRC block is 'u_d^*' and 'u_q^*'. These are fed into a 'one-beat delay' block (Eq.6) and then a 'first order low-pass filter delay' block (Eq.7). The output of the low-pass filter delay block is fed back into the ESO. The 'u_d^*' and 'u_q^*' are also fed into a 'PMSM model' (Eq.1) for sampling.](84a01685710d24f113b18758ed3c6fcb_img.jpg)

Block diagram of predictive ESO with time delay compensation. The diagram shows a 'Predictive ESO' block (dashed line) containing a 'model-enhanced ESO' (Eq.11). Inputs to the ESO are from a 'PMSM model' (Eq.1) and a 'predicting currents using known model' (Eq.5). The ESO outputs 'estimated current' and 'estimated disturbance'. The 'estimated current' is fed into a 'Model-enhanced ADRC current control' (Eq.12) block. This block also receives 'estimated disturbance' and 'current error feedback'. The output of the ADRC block is 'u\_d^\*' and 'u\_q^\*'. These are fed into a 'one-beat delay' block (Eq.6) and then a 'first order low-pass filter delay' block (Eq.7). The output of the low-pass filter delay block is fed back into the ESO. The 'u\_d^\*' and 'u\_q^\*' are also fed into a 'PMSM model' (Eq.1) for sampling.

FIGURE 3 Block diagram of predictive ESO with time delay compensation.

![Block diagram of the ADRC current controller for PMSM. The diagram shows a 'Model-enhanced ADRC current control' (Eq.12) block. Inputs to this block are 'i_d^*', 'i_q^*', 'estimated current', and 'estimated disturbance'. The output is 'u_d^*' and 'u_q^*'. These are fed into a '2r/2s' block, which then feeds into an 'SVPWM' block. The 'SVPWM' block feeds into an 'Inverter'. The 'Inverter' feeds into a 'PMSM' block. A 'Sensor' block measures the motor's current and speed. The 'Sensor' feeds into a 'Calculation of electrical angular velocity' block, which outputs 'omega_e'. The 'omega_e' is fed back into the 'Model-enhanced ADRC current control' block. The 'Sensor' also feeds into a 'Predictive ESO with delay compensation' block. This block outputs 'i_d1' and 'i_q1', which are fed into a 'low pass filter' block. The output of the low pass filter is 'i_d' and 'i_q', which are fed back into the 'Model-enhanced ADRC current control' block. The 'Predictive ESO with delay compensation' block also receives 'i_d^*', 'i_q^*', and 'omega_e'.](f11b8f19a9a2518acf8ea2482a5579d2_img.jpg)

Block diagram of the ADRC current controller for PMSM. The diagram shows a 'Model-enhanced ADRC current control' (Eq.12) block. Inputs to this block are 'i\_d^\*', 'i\_q^\*', 'estimated current', and 'estimated disturbance'. The output is 'u\_d^\*' and 'u\_q^\*'. These are fed into a '2r/2s' block, which then feeds into an 'SVPWM' block. The 'SVPWM' block feeds into an 'Inverter'. The 'Inverter' feeds into a 'PMSM' block. A 'Sensor' block measures the motor's current and speed. The 'Sensor' feeds into a 'Calculation of electrical angular velocity' block, which outputs 'omega\_e'. The 'omega\_e' is fed back into the 'Model-enhanced ADRC current control' block. The 'Sensor' also feeds into a 'Predictive ESO with delay compensation' block. This block outputs 'i\_d1' and 'i\_q1', which are fed into a 'low pass filter' block. The output of the low pass filter is 'i\_d' and 'i\_q', which are fed back into the 'Model-enhanced ADRC current control' block. The 'Predictive ESO with delay compensation' block also receives 'i\_d^\*', 'i\_q^\*', and 'omega\_e'.

FIGURE 4 Block diagram of the ADRC current controller for PMSM.

TABLE 1 Parameters of the PMSM.

| Parameter                      | Value                                             |
|--------------------------------|---------------------------------------------------|
| Rated voltage                  | 24 V                                              |
| Rated speed                    | 1600 rpm                                          |
| Resistance $R_{sn}$            | 0.1763 $\Omega$                                   |
| d-axis inductance $L_{dn}$     | 195.185 $\mu$ H                                   |
| q-axis inductance $L_{qn}$     | 195.185 $\mu$ H                                   |
| Moment of inertia              | $0.58 \times 10^{-4} \text{ kg} \cdot \text{m}^2$ |
| Pole pairs                     | 5                                                 |
| Permanent magnet flux $\psi_m$ | 0.0109 Wb                                         |

pass filter for current measurement is primarily used to filter out high-frequency fluctuations in current caused by MOSFET switching on and off, as well as high-frequency noise in the measurements. Its cutoff frequency is  $1/T_1$  rad/s. In this paper,  $T_1 = 0.0002$  corresponds to a cutoff frequency of 5000 rad/s. For different motor drive systems, the selection of this filter can be based on a combination of the desired dynamic response of the current loop and the switching frequency.

The control parameters are as follows: feedback control gains  $k_1 = k_2 = 2.5$ , predictive ESO parameters  $l_1 = 2\omega_o$ ,  $l_2 = \omega_o^2$ , and  $\omega_o = 1500$ . Figure 5 shows the closed-loop characteristics when the control gains are 0.5, 1.5, and 2.5,

respectively. The expected current control bandwidth can be selected first, and then these two parameters can be chosen based on the frequency response.

The results with matched motor parameters are shown in Figure 6. When using an ESO without time delay compensation, the amplitude-frequency characteristics are greater than zero in the high-frequency range, showing a trend of rising first and then falling. This is due to the presence of a first-order low-pass filter in the current feedback channel, which increases the order of the current loop closed-loop system. Figure 7 shows the effect of different filtering time constants on the current closed-loop control performance during current measurement. We can observe that as the filtering time constant decreases, the amplitude near the 3000 rad/s frequency significantly decreases, indicating that the increase in amplitude is caused by the low-pass filter used in current measurement. However, when using a predictive ESO with time delay compensation, the current closed-loop system exhibits frequency domain characteristics closer to those of a first-order system and has greater phase margin in the high-frequency range, which is beneficial for enhancing stability and reducing oscillation.

The frequency domain characteristics of the current closed-loop system with mismatched resistance parameter are shown in Figure 8. The solid line represents the Bode plot when the parameters are matched, while the dashed line represents the Bode plot when the resistance changes to twice the nominal value ( $R_s = 2R_{sn}$ ). Due to the mismatch between the predictive model and the actual model, the frequency domain characteristics change. As shown in Figure 8a, for the ADRC current controller without time delay compensation, the amplitude-frequency characteristic starts to decrease at frequencies greater than 200 rad/s and then increases again at frequencies greater than 1000 rad/s. In contrast, in Figure 8b, after time delay compensation, the bandwidth of the current closed-loop system slightly decreases, but the amplitude-frequency characteristic still approaches that of an ideal first-order system. The phase lag at 9424 rad/s (corresponding to frequency 1500 Hz) is  $-80^\circ$ , which is less than the  $-95^\circ$  lag before time delay compensation. The frequency domain characteristics indicate that the proposed predictive ESO can still achieve effective time delay compensation under resistance variation, ensuring the stability of the PMSM current loop.

The frequency domain characteristics of the current closed-loop system with mismatched inductance parameter are shown in Figure 9. The dashed line represents the Bode plot when the inductance parameter is reduced to half of its nominal value,  $L_d = 0.5L_{dn}$ ,  $L_q = 0.5L_{qn}$ . For Figure 9a, the amplitude-frequency characteristic starts to decrease at frequencies greater than 2000 rad/s, and the phase shows an upward trend. The characteristics differ significantly from those when the inductance parameters are matched. In the ADRC current controller shown in equation (12), the coefficients of  $\hat{d}_d(k)$  and  $\hat{d}_q(k)$  in the disturbance rejection term use the nominal inductance values  $L_{dn}$  and  $L_{qn}$ . When the actual inductance values decrease, the disturbance rejection effect will undergo changes. For Figure 9b, after time delay

![Figure 5: Bode plot showing the impact of control gain k1 and k2 on the ADRC current closed-loop system. The plot consists of two subplots: Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a logarithmic scale from 10^1 to 10^4. Three curves are shown for different gain combinations: k1=k2=2.5 (solid red line), k1=k2=1.5 (dashed blue line), and k1=k2=0.5 (dotted purple line). The magnitude plot shows that as gains increase, the amplitude-frequency characteristic starts to decrease at lower frequencies. The phase plot shows that higher gains result in a more negative phase lag at high frequencies.](e1dda754c2c88a8ad0b968aea4fc0786_img.jpg)

Figure 5: Bode plot showing the impact of control gain k1 and k2 on the ADRC current closed-loop system. The plot consists of two subplots: Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a logarithmic scale from 10^1 to 10^4. Three curves are shown for different gain combinations: k1=k2=2.5 (solid red line), k1=k2=1.5 (dashed blue line), and k1=k2=0.5 (dotted purple line). The magnitude plot shows that as gains increase, the amplitude-frequency characteristic starts to decrease at lower frequencies. The phase plot shows that higher gains result in a more negative phase lag at high frequencies.

**FIGURE 5** The impact of control gain  $k_1$  and  $k_2$  on the Bode plot of the ADRC current closed-loop system.

![Figure 6: Bode plot showing the impact of time delay compensation on the ADRC current closed-loop system. The plot consists of two subplots: Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a logarithmic scale from 10^1 to 10^4. Two curves are shown: 'Time delay uncompensated ESO' (solid red line) and 'Time delay compensated ESO' (dashed blue line). The uncompensated ESO shows a peak in magnitude around 1000 rad/s and a phase lag that reaches -90° at high frequencies. The compensated ESO shows a much flatter magnitude response and a phase lag that is less negative at high frequencies.](80530169c7b6298ce012a85b906caeb3_img.jpg)

Figure 6: Bode plot showing the impact of time delay compensation on the ADRC current closed-loop system. The plot consists of two subplots: Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a logarithmic scale from 10^1 to 10^4. Two curves are shown: 'Time delay uncompensated ESO' (solid red line) and 'Time delay compensated ESO' (dashed blue line). The uncompensated ESO shows a peak in magnitude around 1000 rad/s and a phase lag that reaches -90° at high frequencies. The compensated ESO shows a much flatter magnitude response and a phase lag that is less negative at high frequencies.

**FIGURE 6** The impact of time delay compensation on the Bode plot of the ADRC current closed-loop system.

![Figure 7: Bode plot showing the impact of different filtering time constants on the ADRC current closed-loop system. The plot consists of two subplots: Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a logarithmic scale from 10^1 to 10^4. Three curves are shown for different filtering time constants: Tf=200 us (solid red line), Tf=100 us (dashed blue line), and Tf=50 us (dotted purple line). The magnitude plot shows that as the filtering time constant decreases, the amplitude-frequency characteristic starts to decrease at lower frequencies. The phase plot shows that a smaller filtering time constant results in a more negative phase lag at high frequencies.](29ac39bfd74e57a92045649f83cad949_img.jpg)

Figure 7: Bode plot showing the impact of different filtering time constants on the ADRC current closed-loop system. The plot consists of two subplots: Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a logarithmic scale from 10^1 to 10^4. Three curves are shown for different filtering time constants: Tf=200 us (solid red line), Tf=100 us (dashed blue line), and Tf=50 us (dotted purple line). The magnitude plot shows that as the filtering time constant decreases, the amplitude-frequency characteristic starts to decrease at lower frequencies. The phase plot shows that a smaller filtering time constant results in a more negative phase lag at high frequencies.

**FIGURE 7** The impact of different filtering time constant on the Bode plot of the ADRC current closed-loop system.

compensation, the changes in the amplitude-frequency characteristics are reduced, with a maximum value of 3 dB, which is less than the 7 dB before time delay compensation. Similarly, it can be observed from the high-frequency range that even with inductance perturbations, the phase lag of the current closed-loop system after time delay compensation is still less than that before compensation. The frequency domain characteristics of the current closed-loop system with mismatched flux linkage

![Figure 8a: Bode plot of the ADRC current controller with time delay uncompensated. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for R_s = R_sn and a dashed blue line for R_s = 2R_sn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 8a: Bode plot of the ADRC current controller with time delay uncompensated. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for R\_s = R\_sn and a dashed blue line for R\_s = 2R\_sn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies.

a

![Figure 8b: Bode plot of the ADRC current controller with time delay compensated. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for R_s = R_sn and a dashed blue line for R_s = 2R_sn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies, similar to the uncompensated case but with improved stability.](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 8b: Bode plot of the ADRC current controller with time delay compensated. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for R\_s = R\_sn and a dashed blue line for R\_s = 2R\_sn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies, similar to the uncompensated case but with improved stability.

b

**FIGURE 8** Bode plot of the ADRC current controller with  $R_s = 2R_{sn}$ : (a) Time delay uncompensated; (b) Time delay compensated.

parameter are shown in Figure 10. The dashed line represents the Bode plot when the flux linkage changes to 0.75 times the nominal value ( $\psi_r = 0.75\psi_{rn}$ ). It can be observed that regardless of whether time delay compensation is applied, the impact of flux linkage parameter changes on the current closed-loop characteristics is minimal.

## 5 | SIMULATION AND EXPERIMENTAL RESEARCH

The simulation and experimental conditions are as follows: the supply voltage of the DC bus is 24 V, the switching frequency is set to 10 kHz, and the current loop's control period  $T_s$  is 100  $\mu$ s. The PMSM operates in current control mode, with a specified d-axis current command  $i_d^* = 0$  A. The q-axis command  $i_q^*$  changes over time. The control parameters used in the simulations and experiments are consistent with those used in the frequency domain analysis.

### 5.1 | Simulation verification of time delay compensation

The simulation results of current loop time delay compensation are shown in Figure 11, with a given q-axis current

![Figure 9a: Bode plot of the ADRC current closed-loop system with time delay uncompensated, showing the impact of inductance parameter perturbations. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for L_d = L_dn, L_q = L_qn and a dashed blue line for L_d = 0.5L_dn, L_q = 0.5L_qn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies.](f6c63daa87b1f2bde4b871f3d540e85b_img.jpg)

Figure 9a: Bode plot of the ADRC current closed-loop system with time delay uncompensated, showing the impact of inductance parameter perturbations. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for L\_d = L\_dn, L\_q = L\_qn and a dashed blue line for L\_d = 0.5L\_dn, L\_q = 0.5L\_qn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies.

a

![Figure 9b: Bode plot of the ADRC current closed-loop system with time delay compensated, showing the impact of inductance parameter perturbations. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for L_d = L_dn, L_q = L_qn and a dashed blue line for L_d = 0.5L_dn, L_q = 0.5L_qn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies, showing improved stability compared to the uncompensated case.](bd4e83fb391d10fb5f7595a1cf5f3f05_img.jpg)

Figure 9b: Bode plot of the ADRC current closed-loop system with time delay compensated, showing the impact of inductance parameter perturbations. The plot shows Magnitude (dB) and Phase (°) versus Frequency (rad/s) on a log scale from 10^1 to 10^4. Two curves are shown: a solid red line for L\_d = L\_dn, L\_q = L\_qn and a dashed blue line for L\_d = 0.5L\_dn, L\_q = 0.5L\_qn. The magnitude remains near 0 dB, and the phase starts near 0° and drops to -90° at high frequencies, showing improved stability compared to the uncompensated case.

b

**FIGURE 9** The impact of inductance parameter perturbations on the frequency domain characteristics of the ADRC current closed-loop system: (a) Time delay uncompensated; (b) Time delay compensated.

command of 2 A. Figure 11a depicts the simulation results of ADRC without time delay compensation, where  $i_q$  exhibits overshoot, reaching a maximum value of 2.2 A. After time delay compensation, as shown in Figure 11b, there is no overshoot in the q-axis current response. Under the same control parameters, the phase margin is greater, indicating higher stability.

The detailed waveforms in the current step response are shown in Figure 12. Here,  $i_q$  represents the actual q-axis current,  $i_{qf}$  represents the q-axis current after passing through the first order low-pass filter, and  $i_q^{p3}$  represents the q-axis current output from the predictive ESO. In Figure 12a, the current command steps from 0 to 2 A, and the time delay between the filtered current  $i_{qf}$  and the actual current  $i_q$  reaches a maximum of 230  $\mu$ s. However, the predictive ESO output  $i_q^{p3}$  accurately predicts the q-axis current in each switching cycle, effectively compensating for the effects of the low-pass filter and the inherent one-sample delay in digital control. The simulation waveform of the sudden decrease in the current command (from 2 to 0 A) is shown in Figure 12b. Similar to the case of a sudden increase in the current command, the predictive ESO demonstrates good time delay compensation during the dynamic process.

![Figure 10: Bode plots showing the impact of flux linkage parameter perturbations on the frequency domain characteristics of the ADRC current closed-loop system. (a) Time delay uncompensated: Magnitude plot shows a peak around 1000 rad/s, and the Phase plot shows a phase margin of approximately 45 degrees. (b) Time delay compensated: Both Magnitude and Phase plots are much flatter, indicating improved stability and performance. The plots compare two cases: ψr = ψrn (red solid line) and ψr = 0.75ψrn (blue dashed line).](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 10: Bode plots showing the impact of flux linkage parameter perturbations on the frequency domain characteristics of the ADRC current closed-loop system. (a) Time delay uncompensated: Magnitude plot shows a peak around 1000 rad/s, and the Phase plot shows a phase margin of approximately 45 degrees. (b) Time delay compensated: Both Magnitude and Phase plots are much flatter, indicating improved stability and performance. The plots compare two cases: ψr = ψrn (red solid line) and ψr = 0.75ψrn (blue dashed line).

**FIGURE 10** The impact of flux linkage parameter perturbations on the frequency domain characteristics of the ADRC current closed-loop system: (a) Time delay uncompensated; (b) Time delay compensated.

### 5.2 | Experimental verification of current step command tracking

The experimental platform is depicted in Figure 13. It employs the STM32G474 microcontroller as the main control chip, and the rotor position is obtained through a 2500-line ABZ encoder. In the test bench, the three-phase lines of the motor under test are connected to a three-phase uncontrolled rectifier bridge, followed by a resistive load.

The experimental results of the proposed ADRC current control with predictive ESO time delay compensation are shown in Figure 14, with the q-axis current command  $i_q^*$  step changing between  $\pm 2$  A. It can be observed that the feedback current  $i_q$  can effectively track the command  $i_q^*$ , demonstrating high-performance dynamic current control.

The experimental results of current loop for a sudden increase in current command are compared in Figure 15, where the q-axis step current command increases from 0 to 2 A. When the time delay is uncompensated, as shown in Figure 15a, the phase lag caused by the time delay reduces the phase margin of the current loop, resulting in oscillations in the  $i_q$  step response, and the fluctuation of the d-axis current is 0.62 A. In contrast, the experimental results with time delay compensation using predictive ESO, as shown in Figure 15b, exhibit significantly reduced oscillations during the dynamic

![Figure 11: Simulation results of current step response. (a) Time delay uncompensated: Shows significant oscillations in the q-axis current (i_q) and d-axis current (i_d) during the step response. (b) Time delay compensated: Shows a smooth step response for i_q and minimal fluctuation for i_d. Both plots also show disturbance estimation (d_hat) and actual disturbance (d_hat) which track each other closely.](643d86ebba41e16a88461bfcb3741de6_img.jpg)

Figure 11: Simulation results of current step response. (a) Time delay uncompensated: Shows significant oscillations in the q-axis current (i\_q) and d-axis current (i\_d) during the step response. (b) Time delay compensated: Shows a smooth step response for i\_q and minimal fluctuation for i\_d. Both plots also show disturbance estimation (d\_hat) and actual disturbance (d\_hat) which track each other closely.

**FIGURE 11** Simulation results of current step response: (a) Time delay uncompensated; (b) Time delay compensated.

process, indicating larger stability margins. Additionally, the fluctuation of the d-axis current decreases to 0.18 A.

The experimental results comparing ADRC with and without time delay compensation for a sudden decrease in current command are shown in Figure 16, where the q-axis step current command decreases from 2 A to  $-2$  A. When the time delay is uncompensated, oscillations occur in the  $i_q$  during the dynamic process, and the fluctuation of  $i_d$  reaches 1.38 A. After delay compensation using predictive ESO, the oscillations in the q-axis current are eliminated, and the fluctuation of  $i_d$  is reduced to 0.52 A, achieving better dynamic control performance.

### 5.3 | Experimental validation of robustness to motor parameter perturbation

To verify the effect of motor parameter variations on current control performance, the resistance value in the control algorithm is set to twice the nominal value. The-step response experimental results are shown in Figure 17. Comparing the results with those shown in Figure 15b, where the resistance parameter matches the nominal value, it can be observed that there is little change in the q-axis current response when the

![Figure 12: Current detail simulation waveform of predictive ESO with time delay compensation during step response. (a) Time delay uncompensated: shows current (A) vs Time (s) x 10^-3. The q-axis current i_q (orange dashed line) rises from 0 to 1.8 A with significant overshoot and oscillations. The i_q^* (blue dashed line) and i_q^p3 (yellow dashed line) are also shown. (b) Time delay compensated: shows a zoomed-in view of the transition from 0.0095 to 0.012 s. The i_q (orange dashed line) rises smoothly from 0 to 2 A, following the i_q^* (blue dashed line) and i_q^p3 (yellow dashed line) closely.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 12: Current detail simulation waveform of predictive ESO with time delay compensation during step response. (a) Time delay uncompensated: shows current (A) vs Time (s) x 10^-3. The q-axis current i\_q (orange dashed line) rises from 0 to 1.8 A with significant overshoot and oscillations. The i\_q^\* (blue dashed line) and i\_q^p3 (yellow dashed line) are also shown. (b) Time delay compensated: shows a zoomed-in view of the transition from 0.0095 to 0.012 s. The i\_q (orange dashed line) rises smoothly from 0 to 2 A, following the i\_q^\* (blue dashed line) and i\_q^p3 (yellow dashed line) closely.

**FIGURE 12** Current detail simulation waveform of predictive ESO with time delay compensation during step response: (a) Time delay uncompensated; (b) Time delay compensated.

![Figure 13: Experimental platform. A photograph of the hardware setup including a laptop running monitoring software, a DC power supply, an energy dissipation resistor, a rectifier bridge, a driver, and a loading experimental motor.](a86610f7a0e579fec9f34dea52fa088b_img.jpg)

Figure 13: Experimental platform. A photograph of the hardware setup including a laptop running monitoring software, a DC power supply, an energy dissipation resistor, a rectifier bridge, a driver, and a loading experimental motor.

**FIGURE 13** Experimental platform.

resistance value in the control algorithm is doubled. This indicates that the proposed method is insensitive to resistance parameter variations, ensuring robust performance in the presence of resistance parameter perturbations.

To verify the control effectiveness when the motor inductance parameters are mismatched, the inductance value used in the control algorithm is set to 1.5 times or 0.75 times the nominal inductance value. The experimental results are shown in Figure 18. The tested motor operates in current control mode, with a specified d-axis current of 0 A. The q-axis current is specified as  $-2$  A and suddenly changes to 2 A at 12.01 s. Without time delay compensation, severe oscillations occur in the q-axis current as shown in Figure 18a, with the fluctuation of the d-axis current reaching 1.4 A, indicating a significant degradation in dynamic performance. Figure 18b presents the experimental results of ADRC using time delay compensation with predictive ESO. It can be observed that the

![Figure 14: Experimental results of ADRC current controller with predictive ESO. Three stacked plots showing: (top) q-axis current i_q^* (blue dashed) and i_q (orange solid) vs Time (s) from 7 to 15; (middle) d-axis current i_d (red solid) vs Time (s); (bottom) electrical speed omega_e (red solid) in rad/s vs Time (s) from 7 to 15. The q-axis current steps from 0 to 2 A at t=8.5s and back to 0 at t=12.5s.](0d5fdb87a392819c7d2e3b6230912a0b_img.jpg)

Figure 14: Experimental results of ADRC current controller with predictive ESO. Three stacked plots showing: (top) q-axis current i\_q^\* (blue dashed) and i\_q (orange solid) vs Time (s) from 7 to 15; (middle) d-axis current i\_d (red solid) vs Time (s); (bottom) electrical speed omega\_e (red solid) in rad/s vs Time (s) from 7 to 15. The q-axis current steps from 0 to 2 A at t=8.5s and back to 0 at t=12.5s.

**FIGURE 14** Experimental results of ADRC current controller with predictive ESO.

![Figure 15: Comparison of ADRC experimental results with and without time delay compensation (i_q^* : 0 A -> 2 A). (a) Time delay uncompensated ESO: shows large oscillations in i_q (orange solid) and i_d (red solid) around the step change at t=8.02s. (b) Time delay compensated ESO: shows smooth tracking of i_q^* (blue dashed) by i_q (orange solid) and i_d (red solid) with minimal fluctuation. Arrows indicate the peak d-axis current fluctuation of 0.62 A in (a) and 0.18 A in (b).](4495fbec19aac6861f1a0b35c4dc38bc_img.jpg)

Figure 15: Comparison of ADRC experimental results with and without time delay compensation (i\_q^\* : 0 A -> 2 A). (a) Time delay uncompensated ESO: shows large oscillations in i\_q (orange solid) and i\_d (red solid) around the step change at t=8.02s. (b) Time delay compensated ESO: shows smooth tracking of i\_q^\* (blue dashed) by i\_q (orange solid) and i\_d (red solid) with minimal fluctuation. Arrows indicate the peak d-axis current fluctuation of 0.62 A in (a) and 0.18 A in (b).

**FIGURE 15** Comparison of ADRC experimental results with and without time delay compensation ( $i_q^* : 0 \text{ A} \to 2 \text{ A}$ ): (a) Time delay uncompensated ESO; (b) Time delay compensated ESO.

oscillations in the q-axis current during the transition process are significantly reduced, and the fluctuation of the d-axis current decreases from 1.4 to 0.53 A. This demonstrates the strong robustness of the proposed method against mismatched inductance parameters.

![Figure 16(a): Comparison of ADRC experimental results without time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i_q* (dashed blue line) and the actual current i_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i_d in Amperes (A), with a zoom-in inset showing a transient change of 1.38 A. The bottom subplot shows the estimated electrical angular velocity omega_e in rad/s, which drops from 500 to -500 rad/s at t=10 s.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 16(a): Comparison of ADRC experimental results without time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i\_q\* (dashed blue line) and the actual current i\_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i\_d in Amperes (A), with a zoom-in inset showing a transient change of 1.38 A. The bottom subplot shows the estimated electrical angular velocity omega\_e in rad/s, which drops from 500 to -500 rad/s at t=10 s.

![Figure 16(b): Comparison of ADRC experimental results with time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i_q* (dashed blue line) and the actual current i_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i_d in Amperes (A), with a zoom-in inset showing a transient change of 1.4 A. The bottom subplot shows the estimated electrical angular velocity omega_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.](f519a5be118c846f631c992412353fb9_img.jpg)

Figure 16(b): Comparison of ADRC experimental results with time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i\_q\* (dashed blue line) and the actual current i\_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i\_d in Amperes (A), with a zoom-in inset showing a transient change of 1.4 A. The bottom subplot shows the estimated electrical angular velocity omega\_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.

![Figure 16(c): Comparison of ADRC experimental results with time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i_q* (dashed blue line) and the actual current i_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i_d in Amperes (A), with a zoom-in inset showing a transient change of 0.52 A. The bottom subplot shows the estimated electrical angular velocity omega_e in rad/s, which drops from 500 to -500 rad/s at t=10 s.](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 16(c): Comparison of ADRC experimental results with time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i\_q\* (dashed blue line) and the actual current i\_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i\_d in Amperes (A), with a zoom-in inset showing a transient change of 0.52 A. The bottom subplot shows the estimated electrical angular velocity omega\_e in rad/s, which drops from 500 to -500 rad/s at t=10 s.

![Figure 16(d): Comparison of ADRC experimental results with time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i_q* (dashed blue line) and the actual current i_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i_d in Amperes (A), with a zoom-in inset showing a transient change of 0.53 A. The bottom subplot shows the estimated electrical angular velocity omega_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.](8ee3b76dd49f31624d287885bc2c81ee_img.jpg)

Figure 16(d): Comparison of ADRC experimental results with time delay compensation. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i\_q\* (dashed blue line) and the actual current i\_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i\_d in Amperes (A), with a zoom-in inset showing a transient change of 0.53 A. The bottom subplot shows the estimated electrical angular velocity omega\_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.

**FIGURE 16** Comparison of ADRC experimental results with and without time delay compensation ( $i_q^* : 2\text{A} \to -2\text{A}$ ): (a) Time delay uncompensated ESO; (b) Time delay compensated ESO.

![Figure 17: Experimental results of the resistance value in the control algorithm being twice the nominal value. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i_q* (dashed blue line) and the actual current i_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i_d in Amperes (A), with a zoom-in inset showing a transient change of 0.45 A. The bottom subplot shows the estimated electrical angular velocity omega_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.](7c2f0efb2c5d10a52ce19ba33d9d3cec_img.jpg)

Figure 17: Experimental results of the resistance value in the control algorithm being twice the nominal value. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i\_q\* (dashed blue line) and the actual current i\_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i\_d in Amperes (A), with a zoom-in inset showing a transient change of 0.45 A. The bottom subplot shows the estimated electrical angular velocity omega\_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.

![Figure 18: Experimental results of the inductance value in the control algorithm being unmatched the nominal value. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i_q* (dashed blue line) and the actual current i_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i_d in Amperes (A), with a zoom-in inset showing a transient change of 0.45 A. The bottom subplot shows the estimated electrical angular velocity omega_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.](df476ed6ad0bb890c67aa63e7647d071_img.jpg)

Figure 18: Experimental results of the inductance value in the control algorithm being unmatched the nominal value. The figure consists of three vertically stacked subplots. The top subplot shows the reference current i\_q\* (dashed blue line) and the actual current i\_q (solid orange line) in Amperes (A), with a zoom-in inset showing the transient response. The middle subplot shows the d-axis current i\_d in Amperes (A), with a zoom-in inset showing a transient change of 0.45 A. The bottom subplot shows the estimated electrical angular velocity omega\_e in rad/s, which drops from 500 to -500 rad/s at t=12 s.

**FIGURE 17** Experimental results of the resistance value in the control algorithm being twice the nominal value.

**FIGURE 18** Experimental results of the inductance value in the control algorithm being unmatched the nominal value: (a) Time delay uncompensated ESO,  $1.5L_{qn}$ ; (b) Time delay compensated ESO,  $1.5L_{qn}$ ; (c) Time delay compensated ESO,  $0.75L_{qn}$ .

Figure 19 presents the experimental results where the permanent magnet flux linkage is reduced to 0.75 times the nominal value in the control algorithm. Similar to the inductance perturbation, the ADRC with time delay compensation demonstrates better control performance.

## 6 | CONCLUSION

The inherent one-sample time delay in digital control and the time delay caused by the low-pass filter in current measurement introduce phase lag into the current closed-loop, thus reducing the stability and dynamic performance of the PMSM current loop. To address this issue, a predictive ESO



![Figure 19: Experimental results of the permanent magnet flux value. Subplot (a) shows the uncompensated ESO, where the current i_q* and i_q show a delay of approximately 0.2 seconds after a step change, and the flux omega_e shows a delay of approximately 0.5 seconds. Subplot (b) shows the time delay compensated ESO, where the current i_q* and i_q respond immediately to the step change, and the flux omega_e shows a much smaller delay of approximately 0.1 seconds. Both subplots show the d-axis current i_d, which is relatively constant at 1.2 A in (a) and 0.46 A in (b). The x-axis for both is Time (s) from 11.9 to 12.3.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 19: Experimental results of the permanent magnet flux value. Subplot (a) shows the uncompensated ESO, where the current i\_q\* and i\_q show a delay of approximately 0.2 seconds after a step change, and the flux omega\_e shows a delay of approximately 0.5 seconds. Subplot (b) shows the time delay compensated ESO, where the current i\_q\* and i\_q respond immediately to the step change, and the flux omega\_e shows a much smaller delay of approximately 0.1 seconds. Both subplots show the d-axis current i\_d, which is relatively constant at 1.2 A in (a) and 0.46 A in (b). The x-axis for both is Time (s) from 11.9 to 12.3.

**FIGURE 19** Experimental results of the permanent magnet flux value in the control algorithm being 0.75 times the nominal value: (a) Time delay uncompensated ESO; (b) Time delay compensated ESO.

considering the inherent one-sample time delay in digital control and the delay caused by the low-pass filter in current measurement is designed. Furthermore, a model-enhanced active disturbance rejection current control method is proposed to compensate for the time delay, aiming to improve the robustness of performance in the presence of parameter perturbations. Simulation and experimental results validate the effectiveness of the predictive ESO for time delay compensation in the ADRC method for the PMSM current loop, providing valuable insights for research on high-dynamic PMSM drives.

# AUTHOR CONTRIBUTIONS

**Chunqiang Liu:** Funding acquisition; writing-original draft. **ZhiWen Zhao:** validation; writing-original draft. **Yanfei You:** writing-review & editing. **Xuechao Duan:** project administration; writing-review & editing. **Lijun Chen:** writing-review & editing. **Xiao Xi:** writing-review & editing.

# ACKNOWLEDGEMENTS

This project is supported by the National Natural Science Foundation of China, grant number is 52,407,064.

# CONFLICT OF INTEREST STATEMENT

The authors declare no conflicts of interest.

# DATA AVAILABILITY STATEMENT

Research data are not shared.

# ORCID

Chunqiang Liu ![ORCID icon](2c272f92eedd646336bf3d1161a690e1_img.jpg) <https://orcid.org/0000-0002-6739-5110>

# REFERENCES

- Jian, F., et al.: Multi-level virtual prototyping of electromechanical actuation system for more electric aircraft. *Chin. J. Aeronaut.* 31(5), 892–913 (2018). <https://doi.org/10.1016/j.cja.2017.12.009>
- Mare, J.C., Fu, J.: Review on signal-by-wire and power-by-wire actuation for more electric aircraft. *Chin. J. Aeronaut.* 30(3), 857–870 (2017). <https://doi.org/10.1016/j.cja.2017.03.013>
- Gao, Y., et al.: Neural Network aided PMSM multi-objective design and optimization for more-electric aircraft applications. *Chin. J. Aeronaut.* 35(10), 233–246 (2022). <https://doi.org/10.1016/j.cja.2021.08.006>
- Liu, C., Luo, G., Tu, W.: Survey on active disturbance rejection control of permanent magnet synchronous motor for aviation electro-mechanical actuator. *J. Electr. Eng.* 16(4), 12–24 (2021)
- Fartash Toloue, S., Kamali, S.H., Moallem, M.: Multivariable sliding-mode extremum seeking PI tuning for current control of a PMSM. *IET Electr. Power Appl.* 14(3), 348–356 (2020). <https://doi.org/10.1049/iet-epa.2019.0033>
- Liu, C., et al.: A linear ADRC-based robust high-dynamic double-loop servo system for aircraft electro-mechanical actuators. *Chin. J. Aeronaut.* 32(9), 2174–2187 (2019). <https://doi.org/10.1016/j.cja.2019.03.036>
- Yang, J., et al.: Disturbance/uncertainty estimation and attenuation techniques in PMSM drives—a survey. *IEEE Trans. Ind. Electron.* 64(4), 3273–3285 (2017). <https://doi.org/10.1109/TIE.2016.2583412>
- Yin, Z., et al.: Research on autodisturbance-rejection control of induction motors based on an ant colony optimization algorithm. *IEEE Trans. Ind. Electron.* 65(4), 3077–3094 (2018). <https://doi.org/10.1109/TIE.2017.2751008>
- Qu, L., Qiao, W., Qu, L.: Active-disturbance-rejection-based sliding-mode current control for permanent-magnet synchronous motors. *IEEE Trans. Power Electron.* 36(1), 751–760 (2021). <https://doi.org/10.1109/TPEL.2020.3003666>
- Tian, M., et al.: Discrete repetitive control-based ADRC for current loop disturbances suppression of PMSM drives. *IEEE Trans. Ind. Inf.* 18(5), 3138–3149 (2022). <https://doi.org/10.1109/TII.2021.3107635>
- Chen, Z., et al.: Research on current decoupling and harmonic suppression strategy of permanent magnet synchronous motor based on proportional resonance type ADRC. *Proceedings of the CSEE* 42(24), 9062–9072 (2022). <https://doi.org/10.13334/j.0258-8013.pcsee.211791>
- Zhang, Z., et al.: Robust model predictive current control of PMSM based on nonlinear extended state observer. *IEEE Journal of Emerging and Selected Topics in Power Electronics* 11(1), 862–873 (2023). <https://doi.org/10.1109/JESTPE.2022.3192064>
- Cui, Y., et al.: Linear active disturbance rejection control of IPMSM based on quasi-proportional resonance and disturbance differential compensation linear extended state observer. *IEEE Trans. Ind. Electron.* 71(10), 11910–11924 (2024). <https://doi.org/10.1109/TIE.2024.3352154>
- Zhang, X., Xu, L.: A simple motor-parameter-free model predictive voltage control for PMSM drives based on incremental model. *IEEE Journal of Emerging and Selected Topics in Power Electronics* 12(3), 2845–2854 (2024). <https://doi.org/10.1109/JESTPE.2024.3387454>
- Huang, S.D., et al.: Nonlinear-disturbance-observer-based predictive control for trajectory tracking of planar motors. *IET Electr. Power Appl.* 18(4), 389–399 (2024). <https://doi.org/10.1049/elp2.12398>
- Kawai, H., et al.: Model predictive current control with a finite set of novel voltages and modulator in permanent magnet synchronous motor

- drives. IET Electr. Power Appl. 17(9), 1197–1211 (2023). <https://doi.org/10.1049/elp2.12335>
17. Bai, C., et al.: Robust predictive control for linear permanent magnet synchronous motor drives based on an augmented internal model disturbance observer. IEEE Trans. Ind. Electron. 69(10), 9771–9782 (2022). <https://doi.org/10.1109/TIE.2022.3140532>
  18. Zhang, X., Zhang, L., Zhang, Y.: Model predictive current control for PMSM drives with parameter robustness improvement. IEEE Trans. Power Electron. 34(2), 1645–1657 (2019). <https://doi.org/10.1109/TPEL.2018.2835835>
  19. Gao, J., et al.: Novel compensation strategy for calculation delay of finite control set model predictive current control in PMSM. IEEE Trans. Ind. Electron. 67(7), 5816–5819 (2020). <https://doi.org/10.1109/TIE.2019.2934060>
  20. Hu, M., et al.: Discrete-time frequency-domain disturbance observer to mitigate harmonic current in PMSM drives and the implementation with reduced delay. IEEE Trans. Power Electron. 38(8), 9482–9493 (2023). <https://doi.org/10.1109/TPEL.2023.3271651>
  21. Pan Zihao, X.F., Zhida, Y.: High-dynamic-response current loop control strategy of permanent magnet motor based on smith predictor. Trans. China Electrotech. Soc. 35(09), 1921–1930 (2020)
  22. Dongye Yalan, W.Q.: Second order terminal sliding mode current control of permanent magnet synchronous motor with low chattering and high disturbance rejection based on enhanced extended state observer. Trans. China Electrotech. Soc. 39(08), 2434–2448 (2024)
  23. Wei, Y., et al.: A smith structure-based delay compensation method for model predictive current control of PMSM system. IEEE Journal of Emerging and Selected Topics in Power Electronics 10(4), 4090–4101 (2022). <https://doi.org/10.1109/JESTPE.2021.3137299>
  24. Wang, F., Kong, W., Qu, R.: Model parameter self-correcting deadbeat predictive current control for SPMSM drives. IEEE Trans. Ind. Electron., 1–12 (2024). <https://doi.org/10.1109/TIE.2024.3436609>
  25. Xu, Y., Li, S., Zou, J.: Integral sliding mode control based deadbeat predictive current control for PMSM drives with disturbance rejection. IEEE Trans. Power Electron. 37(3), 2845–2856 (2022). <https://doi.org/10.1109/TPEL.2021.3115875>
  26. Liu, C., et al.: Measurement delay compensated LADRC based current controller design for PMSM drives with a simple parameter tuning method. ISA (Instrum. Soc. Am.) Trans. 101, 482–492 (2020). <https://doi.org/10.1016/j.isatra.2020.01.027>

**How to cite this article:** Liu, C., et al.: Active disturbance rejection current controller with time delay compensation predictive ESO for aircraft PMSM drive. IET Electr. Power Appl. e12522. (2025). <https://doi.org/10.1049/elp2.12522>