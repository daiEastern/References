

![Check for updates icon](30a26f2d17ca95672702bf50fb4f0242_img.jpg)

Check for updates icon

# Sensorless control with time delay compensation for ultra-high-speed air compressor motors in fuel cell systems

Sung-Ho Kang<sup>1</sup> · Hyun-Jun Lee<sup>2</sup> · Tae-Gyeom Woo<sup>1</sup> · Chang-Seok You<sup>3</sup> · Sang-Hak Lim<sup>3</sup> · Young-Doo Yoon<sup>2</sup> ![ORCID icon](c3d993ca47bfe2a953c700506ce31fa0_img.jpg)

Received: 28 July 2025 / Revised: 9 December 2025 / Accepted: 11 December 2025 / Published online: 13 January 2026  
© The Author(s) under exclusive licence to The Korean Institute of Power Electronics 2026

## Abstract

This study discusses the compensation of time delays in ultra-high-speed applications. Sensorless controls are used to estimate the rotor speed and angle. In model-based sensorless control, the voltage and current signals are used for angle estimation as an input of the observer. A time delay occurs when calculating these signals. Especially in the high-speed operating range, these time delays degrade sensorless control performance. This study proposes a method to compensate for these time delays, which improves accurate angle estimation. The proposed time delay implementation method has been validated through simulations and experiments using a 15 kW, 150 kr/min surface mounted permanent magnet synchronous motor for high-speed air compressors of fuel cell systems, where the ratio of switching frequency to fundamental frequency was 8:1.

**Keywords** Sensorless control · Time delay · Ultra-high-speed · Air compressor · Low-frequency modulation index

## 1 Introduction

In recent years, permanent magnet synchronous motors (PMSMs) have been extensively utilized in various applications, including blowers, pumps, and compressors, due to their superior efficiency, high power density, and dependable performance [1–4]. Electric machines operating at rotational speeds exceeding 90 kr/min are commonly classified as ultra-high-speed machines. In such machines, the fundamental frequency of the phase current typically begins at 1,500 Hz.

Recent advancements in high-speed electric motor technology have progressed rapidly. Increasing motor speed eliminates the need for a gearbox, which enables a more compact and cost-efficient system design. In addition, this approach improves system efficiency while minimizing

maintenance requirements. Such benefits make ultra-high-speed electric motors ideal for applications including machine tool spindles, compressors, vacuum pumps, and turbine generators. They are especially advantageous in the automotive industry, where space and weight limitations are critical factors. For instance, ultra-high-speed electric motors exceeding 100 kr/min are used as air compressors in electric vehicles powered by hydrogen fuel cells [5].

Accurate rotor position angles are essential for control systems in nearly all motor industrial applications, especially for high-speed motor operations. However, position sensors increase system complexity and are also limited by electromagnetic interference and mounting accuracy [6]. Position sensors, such as encoders, resolvers, and discrete, and linear hall effect sensors, require signal cables as well as additional space for installation; these requirements complicate the coupling structure and increase the cost, volume, and weight of motors [7–9]. For these reasons, significant attention and effort have been directed toward sensorless control-based rotor position estimation methods. Furthermore, position sensors face challenges in ultra-high-speed applications due to mechanical vibration and temperature conditions. As a result, sensorless control algorithms have been extensively studied.

Sensorless control determines the position and speed of the rotor by utilizing only the electrical signals of the motor.

✉ Young-Doo Yoon  
yoonyd@hanyang.ac.kr

<sup>1</sup> Department of Automotive Engineering (Automotive-Computer Convergence), Hanyang University, Seoul, Republic of Korea

<sup>2</sup> Department of Automotive Engineering, Hanyang University, Seoul, Republic of Korea

<sup>3</sup> Hyundai Motor Company, Yongin, Republic of Korea

This method reduces the cost, weight, and wiring complexity of systems while improving the reliability and durability of motor control [10]- [11]. Sensorless control techniques can be divided into signal injection and model-based methods. The signal injection method is primarily applied in zero- and low-speed operations [12]- [13]. It involves introducing a high-frequency voltage signal and analyzing the resulting high-frequency current signal to estimate the rotor position based on the magnetic pole characteristics of the motor. Meanwhile, model-based sensorless control is mainly implemented in medium to high-speed operations [14]- [16]. This approach relies on motor modeling and uses voltage and current data to estimate the rotor position. In this study, angle estimation is conducted using a model-based sensorless control method [15].

Although sensorless control technology has advanced significantly, enhancing performance in specific conditions, such as ultra-high-speed operations, remains an essential research area. Furthermore, more accurate and efficient sensorless control algorithms suitable for various motor types and application areas need to be developed.

In some applications where the ratio of switching frequency to fundamental frequency is insufficient, such as ultra-high-speed drive, the rotation of the estimated rotor reference frame during the time delay causes phase and magnitude errors in the voltage output. In sensorless control, a time delay occurs during the computation of the input current and voltage required by the observer for angle estimation. The impact of this time delay on performance becomes more significant as the motor operates at higher speeds. Thus, the time delays in the input current and voltage of the observer, as well as the PWM output delay and digital delay, need to be considered.

This study proposes a method for compensating the appropriate time delay in the inputs of the observer based

on the timing of the current controller and sensorless algorithm operations.

This study was previously presented at the 2024 IEEE 10th International Power Electronics and Motion Control Conference [1]. To ensure a more accurate understanding, a detailed explanation has been added and some figures have been revised. Moreover, additional simulation and experimental waveforms have been included.

## 2 Time delay analysis and compensation

In digital control systems employing microprocessors, digital and PWM delays are inevitable, which start from current sampling to the synthesis of PWM voltages. In model-based sensorless control, the observer estimates the position and speed of the rotor using voltage and current signals derived from the voltage model of the motor. However, given that the observer operates prior to the actual estimation of the position of the rotor, the estimated angle at the time of the operation of the observer is not readily available. To address this limitation, the estimated angle from the previous sampling period is utilized to compensate for the current estimation. However, this process introduces time delays when the input voltage and current of the observer are calculated using the previously estimated angle. Therefore, accurately accounting for and compensating these time delays is essential for ensuring precise sensorless control.

This section analyzes the specific causes of these time delays and presents compensation methods tailored to the specific requirements of high-performance motor control systems.

### 2.1 PWM, sampling, and computation timing

In general digital control systems utilizing the single sampling method, the sequence of current sampling, PWM voltage output, and sensorless control algorithm is illustrated in Fig. 1. At  $(k-2)T_s$ , the current  $i^s[k-2]$  is sampled, and this sampled datum is used to compute the output voltage reference  $u^{s*}[k-2]$ . The inverter voltage is then synthesized based on this voltage reference from  $(k-1)T_s$  to  $kT_s$ . A time delay of  $1T_s$  occurs in the output voltage reference calculation, and an additional  $0.5T_s$  delay arises during the synthesis of the inverter voltage, which results in a total time delay of  $1.5T_s$  [17]. As shown in Fig. 1, when the observer operates at  $kT_s$ , it uses the voltage from  $(k-0.5)T_s$  as its input voltage and the current from  $kT_s$  as its input current. It can be expressed as

$$\hat{u}^{r*}[k] = e^{-\left(\hat{\theta}_r[k]\right)J} u^{s*}[k-2] \quad (1)$$

![Timing diagram showing the sequence of sampling, sensorless algorithm operation, and PWM output over time t. The diagram illustrates the time delay between current sampling and voltage reference calculation, and the subsequent PWM output synthesis.](6d6fd934f0988fdb2e2dd22865e8d8ed_img.jpg)

The diagram illustrates the timing sequence of single sampling. The horizontal axis represents time  $t$ . Key time points are marked:  $(k-2)T_s$ ,  $(k-1)T_s$ , and  $kT_s$ . A blue sawtooth wave at the bottom represents the Carrier Wave. The diagram is divided into three main sections by vertical lines at  $(k-2)T_s$  and  $(k-1)T_s$ . Each section shows a sequence of operations: Sampling (indicated by a red arrow pointing to the Carrier Wave), Sensorless Algorithm (observer) (indicated by a dashed box), and PWM output (indicated by a solid box). The PWM output section is labeled  $u^s((k-2)T_s \le t \le (k-1)T_s)$  and  $u^s((k-1)T_s \le t \le kT_s)$ . The time interval between sampling and the start of PWM output is labeled  $T_{samp}$ . The time interval between the start of one PWM output and the start of the next is also labeled  $T_{samp}$ . The time interval between the end of one PWM output and the start of the next is labeled  $1.5T_s$ .

Timing diagram showing the sequence of sampling, sensorless algorithm operation, and PWM output over time t. The diagram illustrates the time delay between current sampling and voltage reference calculation, and the subsequent PWM output synthesis.

**Fig. 1** Sampling method and algorithm operation timing sequence of single sampling

$$\hat{i}^r[k] = e^{-(\hat{\theta}_r[k])J} i^s[k] \quad (2)$$

However, the inputs of the observer cannot be directly utilized as indicated in (1) and (2) because the estimated rotor position,  $\hat{\theta}_r[k]$  at the input of the observer is still unknown. To address this issue, the time delay must be compensated using the estimated angle  $\hat{\theta}_r[k-1]$  and the estimated speed  $\hat{\omega}_r[k-1]$  from the previous sampling period at  $(k-1)T_s$ . As a result, the input voltage and current of the observer can be adjusted as.

$$u^{\hat{r}*}[k] = e^{-(0.5\hat{\omega}_r[k-1]T_s + \hat{\theta}_r[k-1])J} u^{s*}[k-2] \quad (3)$$

$$i^{\hat{r}}[k] = e^{-(\hat{\omega}_r[k-1]T_s + \hat{\theta}_r[k-1])J} i^s[k] \quad (4)$$

Figure 3 illustrates the sampling and PWM strategy adopted in this study. In the ultra-high-speed electric motor systems analyzed here, a high switching frequency is essential, which can limit the available computation time. To address this problem, as shown in Fig. 3, current sampling and voltage command calculations are performed at the peak of the carrier wave. Meanwhile, the sensorless control algorithms are executed during the valley of the carrier wave. This strategy ensures sufficient computation time, which enables precise control and sensorless operation, even at ultra-high speeds. By efficiently utilizing the switching cycle of the inverter, this method separates tasks and optimizes the available computation time.

Unlike the general sampling method depicted in Fig. 1, the voltage command in Fig. 3 is output with a delay of  $0.5T_s$ . Thereafter, the inverter synthesizes the voltage using the delayed voltage command. The time delay includes

$0.5T_s$  for digital delay and another  $0.5T_s$  for PWM delay, which results in a delay of  $1T_s$ . Given that the total delay for the synthesis of output voltage is reduced from  $1.5T_s$  to  $1T_s$ , the control performance would be increased. The observer operates during the valley of the carrier wave. Thus, its input current and voltage are taken from the peak of the carrier wave, which occurs  $0.5T_s$  earlier. Consequently, the angle estimated by the observer corresponds to the peak of the carrier wave  $0.5T_s$  earlier, as illustrated in Fig. 3. Figure 2 illustrates the conventional method, where only the timing of the current input and output (steps 1 and 2) of the controller is considered, while the operation timing (steps 3 and 4) of the observer is ignored. Furthermore, the step numbers in Fig. 2 indicate the sequence of operations. In Fig. 2, the conventional method was intentionally configured without applying observer input compensation based on the sampling timing. The aim is to clearly demonstrate that improper compensation of the observer inputs can critically affect the stability of sensorless control.

To achieve accurate angle estimation, this time delay should be compensated appropriately. Applying precise angle compensation is critical to ensuring stable algorithm operation, given the discussed time delay.

### 2.2 Proposed time delay implementation method

As described in Subsection 2.1, a time delay exists, and a method has been proposed to effectively compensate for it. The proposed approach implements time delay compensation for four main components:

1. When determining current in the estimated rotor reference frame, the estimated angle at the present sampling

![Control block diagram of the conventional method showing the timing of sampling, PWM output, and sensorless algorithm execution relative to a carrier wave.](b6e90f8ae3109449704b9b5c7951f631_img.jpg)

The diagram illustrates the control block diagram of the conventional method. It shows a time axis  $t$  with sampling instants  $(k-2)T_s$ ,  $(k-1)T_s$ ,  $kT_s$ , and  $(k+1)T_s$ . A blue sawtooth wave represents the Carrier Wave. The diagram is divided into three main sections by vertical dashed lines:

- Section 1 ( $(k-2)T_s \le t \le (k-0.5)T_s$ ):** Includes a 'Sampling  $i^s[k-2]$ ' block, a 'Calculate  $u^{s*}[k-2]$ ' block, and a 'PWM output  $u^s((k-1.5)T_s \le t \le (k-0.5)T_s)$ ' block. A 'Sensorless Algorithm (observer)' block outputs  $\hat{\theta}[k-2]$ .
- Section 2 ( $(k-0.5)T_s \le t \le (k+0.5)T_s$ ):** Includes a 'Sampling  $i^s[k-1]$ ' block, a 'Calculate  $u^{s*}[k-1]$ ' block, and a 'PWM output  $u^s((k-0.5)T_s \le t \le (k+0.5)T_s)$ ' block. A 'Sensorless Algorithm (observer)' block outputs  $\hat{\theta}[k-1]$ .
- Section 3 ( $(k+0.5)T_s \le t \le (k+1.5)T_s$ ):** Includes a 'Sampling  $i^s[k]$ ' block, a 'Calculate  $u^{s*}[k]$ ' block, and a 'PWM output  $u^s((k+0.5)T_s \le t \le (k+1.5)T_s)$ ' block. A 'Sensorless Algorithm (observer)' block outputs  $\hat{\theta}[k]$ .

Horizontal arrows labeled  $T_{samp}$  indicate the time interval between sampling instants. Vertical arrows labeled 'Update' point from the sampling and calculation blocks to the PWM output blocks. The 'Sensorless Algorithm (observer)' blocks are shown in a dashed box, and their outputs are also dashed boxes.

Control block diagram of the conventional method showing the timing of sampling, PWM output, and sensorless algorithm execution relative to a carrier wave.

Fig. 2 Control block diagram of the conventional method

**Fig. 3** Sampling method and algorithm operation timing sequence of the system in this study![Control block diagram comparing the Conventional Method and the Proposed Method for sensorless control. The Conventional Method (top, red dashed box) shows a current controller outputting u^{s*}[k] to a PWM inverter, which drives a motor M. The output current i^s[k] is transformed to the stationary frame and fed back to the current controller. An observer estimates the rotor angle and speed. The Proposed Method (bottom, purple dashed box) adds a speed controller that takes the estimated speed \hat{\omega}_{rm}[k] and a reference speed \omega_{rm}^*[k] to produce a torque reference T_e^*[k], which is then scaled by 1/K_t to produce a current reference i^{r*}[k]. This reference is fed into the current controller. The diagram also shows the transformation of the input current i^r[k] from the estimated reference frame to the stationary frame for feedback.](d3ca266c298aeb34b019960c6c36f187_img.jpg)

Control block diagram comparing the Conventional Method and the Proposed Method for sensorless control. The Conventional Method (top, red dashed box) shows a current controller outputting u^{s\*}[k] to a PWM inverter, which drives a motor M. The output current i^s[k] is transformed to the stationary frame and fed back to the current controller. An observer estimates the rotor angle and speed. The Proposed Method (bottom, purple dashed box) adds a speed controller that takes the estimated speed \hat{\omega}\_{rm}[k] and a reference speed \omega\_{rm}^\*[k] to produce a torque reference T\_e^\*[k], which is then scaled by 1/K\_t to produce a current reference i^{r\*}[k]. This reference is fed into the current controller. The diagram also shows the transformation of the input current i^r[k] from the estimated reference frame to the stationary frame for feedback.

**Fig. 4** Control block diagram of the proposed method

time is still unknown. Thus, a  $1T_s$  compensation is applied using the estimated angle and speed from the prior sampling time as.

$$\hat{i}^r[k] = e^{-(\hat{\theta}_r[k-1]+\hat{\omega}_r[k-1]T_s)\mathbf{J}} \hat{i}^{s*}[k] \quad (5)$$

- In calculating the output voltage reference of the current controller, a  $1T_s$  time delay between the voltage reference and the actual voltage is compensated. Moreover, given that the estimated angle  $\hat{\theta}_r[k-1]$  is used, an additional  $1T_s$  compensation is applied. Therefore, a total time delay of  $2T_s$  must be compensated as.

$$\hat{u}^{s*}[k] = e^{-(\hat{\theta}_r[k-1]+2\hat{\omega}_r[k-1]T_s)\mathbf{J}} \hat{u}^{r*}[k] \quad (6)$$

- The input voltage of the observer also needs to be transformed from the stationary reference frame to the estimated reference frame. Therefore, similar to the input voltage of the observer, the estimated angle  $\hat{\theta}_r[k]$  must be compensated using the previously output estimated angle  $\hat{\theta}_r[k-1]$  of the observer and the estimated speed  $\hat{\omega}_r[k-1]$  from  $1T_s$  earlier as.

angle  $\hat{\theta}_r[k-1]$  of the observer and the estimated speed  $\hat{\omega}_r[k-1]$  from  $1T_s$  earlier as.

$$\hat{u}^{r*}[k] = e^{-(\hat{\theta}_r[k-1]+\hat{\omega}_r[k-1]T_s)\mathbf{J}} \hat{u}^{s*}[k-1] \quad (7)$$

- The input current of the observer also needs to be transformed from the stationary reference frame to the estimated reference frame. Therefore, similar to the input voltage of the observer, the estimated angle  $\hat{\theta}_r[k]$  must be compensated using the previously output estimated angle  $\hat{\theta}_r[k-1]$  of the observer and the estimated speed  $\hat{\omega}_r[k-1]$  from  $1T_s$  earlier as.

$$\hat{i}^r[k] = e^{-(\hat{\theta}_r[k-1]+\hat{\omega}_r[k-1]T_s)\mathbf{J}} \hat{i}^{s*}[k] \quad (8)$$

The time delay implementation method can be illustrated in a control block diagram, as shown in Fig. 4.

## 3 Simulation and experiment results

The sensorless control algorithm used in the simulation and experimental validation was based on the flux observer method described in [15]. The observer is composed of a

**Table 1** Simulation conditions

| Parameter                     | Value [unit] |
|-------------------------------|--------------|
| Switching frequency           | 20 [kHz]     |
| Sampling frequency            | 20 [kHz]     |
| Maximum fundamental frequency | 2.5 [kHz]    |
| Current control bandwidth     | 500 [Hz]     |
| Speed control bandwidth       | 2 [Hz]       |
| PLL bandwidth                 | 25 [Hz]      |

**Table 2** 15 kW SPMSM motor parameters

| PMSM          | Value [unit]           |
|---------------|------------------------|
| Rated power   | 15 [kW]                |
| Maximum speed | 150 [kr/min]           |
| Rated current | 55 [A <sub>rms</sub> ] |
| Polepair      | 1                      |
| $R_s$         | 0.0125 [ $\Omega$ ]    |
| $\lambda_f$   | 0.017 [V·s]            |
| $L_s$         | 108 [ $\mu$ H]         |

flux observer and a PLL. The flux observer gain is adaptively adjusted according to the rotor speed.

### 3.1 Simulations

Simulation conditions for the target system are summarized in Table 1, and motor parameters of 15-kW SPMSM are listed in Table 2. The current controller bandwidth was set to 500 Hz to achieve a fast torque response while maintaining acceptable current ripple. It is set considering the fundamental frequency of approximately 2.5 kHz. By contrast, the speed controller bandwidth was intentionally limited to 2 Hz. At maximum speed, the estimated speed signal contains significant noise because the ratio of switching to fundamental frequency is approximately 8:1. Therefore, a lower speed-control bandwidth helps suppress this estimation noise and ensures stable operation of the system.

The simulation results are presented in Fig. 5. In the conventional method, no time delay compensation is applied to the input current and voltage of the observer. To reflect actual system conditions, the current of the simulation is limited to 75 A. The application analyzed in this study is an air compressor for fuel cell systems, where the load torque is proportional to the square of the speed.

In the conventional method, the angle error increases up to a maximum of 41° as the speed rises. As the angle error increases, the difference between the current in rotor reference frame and the current in the estimated reference frame also becomes apparent. As shown in Fig. 5a, the angle error increases with speed, which leads to a reduction in the actual q-axis current in the rotor reference frame compared with the q-axis current in the estimated rotor reference frame. Consequently, the torque required for acceleration up to 150 kr/min becomes insufficient, which makes sensorless

![Figure 5(a): Simulation results for the conventional method. The figure consists of four vertically stacked plots sharing a common x-axis of Time [s] from 0.0 to 5.0. The top plot shows Speed [r/min] (scaled by 10^5) increasing from 0 to 131 kr/min. The second plot shows Current [A] with four curves: i_d^* (blue), i_d^r (red), i_q^* (green), and i_q^r (purple). The third plot shows Torque [Nm] with two curves: T_e^* (red) and T_e^r (blue). The bottom plot shows Angle error [degree] (labeled theta) starting at 0 and increasing to a peak of 41 degrees. The plot is labeled 'Plot 4'.](c82c7d8107cba121734a9cfba891216d_img.jpg)

Figure 5(a): Simulation results for the conventional method. The figure consists of four vertically stacked plots sharing a common x-axis of Time [s] from 0.0 to 5.0. The top plot shows Speed [r/min] (scaled by 10^5) increasing from 0 to 131 kr/min. The second plot shows Current [A] with four curves: i\_d^\* (blue), i\_d^r (red), i\_q^\* (green), and i\_q^r (purple). The third plot shows Torque [Nm] with two curves: T\_e^\* (red) and T\_e^r (blue). The bottom plot shows Angle error [degree] (labeled theta) starting at 0 and increasing to a peak of 41 degrees. The plot is labeled 'Plot 4'.

![Figure 5(b): Simulation results for the proposed method. The figure consists of four vertically stacked plots sharing a common x-axis of Time [s] from 0.0 to 5.0. The top plot shows Speed [r/min] (scaled by 10^5) increasing from 0 to 150 kr/min. The second plot shows Current [A] with four curves: i_d^* (blue), i_d^r (red), i_q^* (green), and i_q^r (purple). The third plot shows Torque [Nm] with two curves: T_e^* (red) and T_e^r (blue). The bottom plot shows Angle error [degree] (labeled theta) starting at 0 and increasing to a peak of 1 degree. The plot is labeled 'Plot 4'.](867fce43c58fda6178b06e454b4ed73a_img.jpg)

Figure 5(b): Simulation results for the proposed method. The figure consists of four vertically stacked plots sharing a common x-axis of Time [s] from 0.0 to 5.0. The top plot shows Speed [r/min] (scaled by 10^5) increasing from 0 to 150 kr/min. The second plot shows Current [A] with four curves: i\_d^\* (blue), i\_d^r (red), i\_q^\* (green), and i\_q^r (purple). The third plot shows Torque [Nm] with two curves: T\_e^\* (red) and T\_e^r (blue). The bottom plot shows Angle error [degree] (labeled theta) starting at 0 and increasing to a peak of 1 degree. The plot is labeled 'Plot 4'.

**Fig. 5** Simulation results of sensorless drive performance to 150 kr/min: **a** conventional method; **b** proposed method

control infeasible at high speeds. The estimated speed failed to reach 150 kr/min, and a significant speed error exists even under the maximum current of 75 A. This result is attributed to the angle estimation error, which generates the d-axis current in the rotor reference frame. This deduction is illustrated in Fig. 6, which shows that, if angle errors exist, then the q-axis current in the estimated reference frame appears as the d-axis current in the actual rotor reference frame.

By contrast, the proposed method compensates for the time delay in the input current and voltage of the observer, which significantly reduces estimated angle errors even at ultra-high speeds in Fig. 5b. The angle error is mitigated to only around  $1^\circ$ , which is a reduction of approximately  $40^\circ$  compared with the conventional method. Owing to these improvements, the proposed method can generate sufficient torque for acceleration up to 150 kr/min, which ensures stable sensorless control even at ultra-high speeds. Furthermore, despite the low frequency modulation index

( $F_{ratio}$ , defined as  $\frac{f_{sw}}{f_{fundamental}}$ ), which is only 8, stable sensorless control remains achievable.

When using the proposed method, an angle error of approximately  $1^\circ$  exists. However, this angle error can be attributed to the low  $F_{ratio}$ , which is only 8. A low  $F_{ratio}$  can cause distortion in the measured current signals.

(The first subplot shows the speeds. The second subplot displays the currents. The third subplot depicts the torque reference in the estimated reference frame. The last subplot presents the angle error.)

Table 3; Fig. 7 show the difference between the actual and measured currents at speeds of 30, 90, and 150 kr/min. These results indicate that the error between the actual and measured currents increases as the speed rises. At high speeds, such current signal distortions can lead to estimation errors. Further research is needed to reduce errors caused by current sampling for enhancing the performance of the proposed method at high speeds.

### 3.2 Experiments

In the experiments, verifying the angle error between the actual rotor angle and the estimated angle was challenging due to system limitations, such as the incapability to attach position sensors caused by mechanical vibrations and temperature constraints. Furthermore, without position sensors, the actual speed could not be directly measured, and the feasibility of sensorless control was confirmed using the estimated speed.

Experiments were conducted on an ultra-high-speed motor used for the air compressor in fuel cell systems to verify the performance of the proposed method. However, due to mechanical vibrations, temperature effects, and bearing

![Diagram illustrating the rotor reference frame and estimated rotor reference frame with angle errors. It shows two sets of axes: the actual rotor reference frame (d^s, q^s) and the estimated rotor reference frame (d^r, q^r). The angle between them is labeled as theta_r. The estimated q-axis current (q^r) is shown as a dashed blue vector, and the estimated d-axis current (d^r) is shown as a solid red vector. The actual q-axis current (q^s) is shown as a dashed blue vector, and the actual d-axis current (d^s) is shown as a solid red vector. The angle error theta_r is indicated between the q^s and q^r axes.](43fec6623ab9cb223a9ff74e2d2a4402_img.jpg)

Diagram illustrating the rotor reference frame and estimated rotor reference frame with angle errors. It shows two sets of axes: the actual rotor reference frame (d^s, q^s) and the estimated rotor reference frame (d^r, q^r). The angle between them is labeled as theta\_r. The estimated q-axis current (q^r) is shown as a dashed blue vector, and the estimated d-axis current (d^r) is shown as a solid red vector. The actual q-axis current (q^s) is shown as a dashed blue vector, and the actual d-axis current (d^s) is shown as a solid red vector. The angle error theta\_r is indicated between the q^s and q^r axes.

**Fig. 6** Rotor reference frame and estimated rotor reference frame with angle errors

**Table 3** Phase current sampling error

| Speed                  | 30 [kr/min] | 90 [kr/min] | 150 [kr/min] |
|------------------------|-------------|-------------|--------------|
| $i_{as}$ , actual [A]  | 3.82        | 28.28       | 75.41        |
| $i_{as}$ , sampled [A] | 3.84        | 27.72       | 71.20        |
| Error [%]              | -0.52       | 1.98        | 5.58         |

![Figure 7: Simulation results of phase current sampling error. It consists of three subplots (a, b, c) showing Current [A] vs Time [s] for speeds of 30 kr/min, 90 kr/min, and 150 kr/min respectively. Each subplot compares the actual current (i_as,actual) shown as a green line and the sampled current (i_as,sampled) shown as a red line. The error between them increases with speed.](eba8385d0983fbda9dc1df0812273269_img.jpg)

Figure 7: Simulation results of phase current sampling error. It consists of three subplots (a, b, c) showing Current [A] vs Time [s] for speeds of 30 kr/min, 90 kr/min, and 150 kr/min respectively. Each subplot compares the actual current (i\_as,actual) shown as a green line and the sampled current (i\_as,sampled) shown as a red line. The error between them increases with speed.

**Fig. 7** Simulation results of phase current sampling error: a 30 kr/min; b 90 kr/min; c 150 kr/min

limitations, operation at speeds above 150 kr/min could not be verified. As a result, the proposed method algorithm was validated at speeds below 150 kr/min.

![Figure 8: 15 kW air compressor motor. (a) Experimental set I: A photograph of the motor assembly with labels for 'Air outlet', 'SPMSM', and 'Air intake filter'. (b) Experimental set II: A photograph of the motor assembly with labels for 'Air outlet', 'Air intake filter', 'SPMSM', and 'Air intake filter'.](1dba94e9a65ea5fbd805e44a5a2c8cd5_img.jpg)

Figure 8: 15 kW air compressor motor. (a) Experimental set I: A photograph of the motor assembly with labels for 'Air outlet', 'SPMSM', and 'Air intake filter'. (b) Experimental set II: A photograph of the motor assembly with labels for 'Air outlet', 'Air intake filter', 'SPMSM', and 'Air intake filter'.

**Fig. 8** 15 kW air compressor motor: **a** experimental set I; **b** Experimental set II

**Table 4** Experimental conditions of set I

| Contents            | VALUE [UNIT] |
|---------------------|--------------|
| DC-link voltage     | 310 [V]      |
| Switching Frequency | 10 [kHz]     |
| Sampling Frequency  | 10 [kHz]     |
| Dead time           | 3 [ $\mu$ s] |

**Table 5** Experimental conditions of set II

| Contents            | VALUE [UNIT] |
|---------------------|--------------|
| DC-link voltage     | 600 [V]      |
| Switching Frequency | 20 [kHz]     |
| Sampling Frequency  | 20 [kHz]     |
| Dead time           | 2 [ $\mu$ s] |

(The first subplot shows estimated speed. The second subplot presents the torque in the estimated reference frame. The third and last subplots display the d-q axis currents in the estimated reference frame.)

The test motor is shown in Fig. 8, and motor parameters of the 15 kW SPMSM used for the experimental verification are shown in Table 2.

Experimental set I was designed for the development stage, and the maximum speed was limited to 75 kr/min considering mechanical instability at high speeds. Given that the maximum speed was reduced to half, the inverter switching frequency was also halved to 10 kHz to maintain the same frequency modulation index ( $F_{ratio}$ ). On the contrary, experimental set II utilized the final-stage test equipment that allows mechanical and thermal testing, where the maximum speed and switching frequency were set to 150 kr/min and 20 kHz. The experimental conditions for both setups are summarized in Tables 4 and 5, respectively.

![Figure 9: Experiment results of sensorless drive performance. (a) Conventional method: A four-panel oscilloscope screenshot showing speed, torque, and d-q axis currents. A red 'Drive fail' label is present. (b) Proposed method: A four-panel oscilloscope screenshot showing speed, torque, and d-q axis currents up to 75 kr/min.](ab9eb65dcbc2696ec77b66f70f9e0e91_img.jpg)

Figure 9: Experiment results of sensorless drive performance. (a) Conventional method: A four-panel oscilloscope screenshot showing speed, torque, and d-q axis currents. A red 'Drive fail' label is present. (b) Proposed method: A four-panel oscilloscope screenshot showing speed, torque, and d-q axis currents up to 75 kr/min.

**Fig. 9** Experiment results of sensorless drive performance for experimental set I up to 75 kr/min: **a** conventional method; **b** proposed method

In experimental set I, debugging was convenient due to the use of a setup for development stage. Every control variable can be monitored. However, in experimental set II, the final product inverter made debugging more challenging, given that only CAN communication was available. The communication interval was 10 ms, which allowed verification only for operation feasibility at the maximum speed.

In experimental set I, as shown in Fig. 9a, the q-axis current in the estimated reference frame increased sharply at speeds above 60 kr/min when using the conventional method. This result can be attributed to the growing angle error, which causes a rapid rise in the q-axis current of the estimated reference frame. When an angle error occurs, the q-axis current in the estimated reference frame must be larger than the actual q-axis current required for operation at the given speed. Moreover, as the angle error increases, the q-axis current in the estimated reference frame continues to grow, as illustrated in Fig. 6. As a result, due to the significantly large angle error, sensorless operation failed before reaching a speed of 75 kr/min.

On the contrary, when using the proposed method, as shown in Fig. 9b, the q-axis current at speeds above 60 kr/min was significantly smaller than that of the conventional method. This finding indirectly indicates a reduction in angle error. Furthermore, sensorless operation was confirmed to remain stable even at speeds up to 75 kr/min.

![Figure 10: Current ripple for experimental set I. Three oscilloscope-like plots (a, b, c) showing current ripple at 15, 50, and 75 kr/min respectively. Each plot has two channels: i_{ds}^* (blue) and i_{ds}^{\hat{}} (red) on top, and i_{qs}^* (green) and i_{qs}^{\hat{}} (purple) on bottom. The time base is 5 ms/div. The ripple magnitude increases with speed.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 10: Current ripple for experimental set I. Three oscilloscope-like plots (a, b, c) showing current ripple at 15, 50, and 75 kr/min respectively. Each plot has two channels: i\_{ds}^\* (blue) and i\_{ds}^{\hat{}} (red) on top, and i\_{qs}^\* (green) and i\_{qs}^{\hat{}} (purple) on bottom. The time base is 5 ms/div. The ripple magnitude increases with speed.

**Fig. 10** Current ripple for experimental set I: **a** 15 kr/min; **b** 50 kr/min; **c** 75 kr/min

Figure 10 illustrates the magnitude of current ripple according to the speed. As the speed increases, the current ripple also exhibits a rising trend. Several factors may contribute to this phenomenon. First, given that the air compressor for fuel cell systems operates at extremely high speeds, mechanical vibrations may lead to increased current ripple. Second, as shown in the results of Fig. 7, a low  $F_{ratio}$  makes accurate average current sampling challenging, which can lead to current ripple [18].

(The first subplot shows speeds. The second subplot presents the currents.)

Figure 11a shows the sensorless control results for the conventional method. Sensorless control fails at speeds above 130 kr/min. The failure of sensorless control is likely due to the lack of accurate angle compensation, which

![Figure 11: Experiment results of sensorless drive performance for experimental set II. (a) Conventional method: Speed vs Time plot shows a failure at 130 kr/min. Current vs Time plot shows large fluctuations. (b) Proposed method: Speed vs Time plot shows stable acceleration to 150 kr/min. Current vs Time plot shows stable current control. Both plots show reference (blue) and estimated (red) values for speed and currents.](aa14b9ec884bf40ce06c161be468cd84_img.jpg)

Figure 11: Experiment results of sensorless drive performance for experimental set II. (a) Conventional method: Speed vs Time plot shows a failure at 130 kr/min. Current vs Time plot shows large fluctuations. (b) Proposed method: Speed vs Time plot shows stable acceleration to 150 kr/min. Current vs Time plot shows stable current control. Both plots show reference (blue) and estimated (red) values for speed and currents.

**Fig. 11** Experiment results of sensorless drive performance for experimental set II: **a** conventional method; **b** proposed method

causes the angle error to increase significantly as speed rises. Consequently, sensorless control cannot operate correctly, and current control cannot be maintained.

However, as shown in Fig. 11b, the proposed method enables stable sensorless control even under a steep acceleration profile. Specifically, it achieves a maximum speed of 150 kr/min. The torque available during the acceleration is restricted due to the system's current limit. Only the current required by the compressor load is maintained after the acceleration ends and the system reaches the steady state.

## 4 Conclusion

This study presents a method to address the time delay introduced by PWM and current sampling. The proposed approach compensates for the time delays associated with current sampling, the output voltage reference of the current controller, and the input current and voltage of the observer to ensure precise angle estimation. By improving sensorless control stability in ultra-high-speed motors, the method enables accurate angle estimation, which would otherwise be challenging without it. Without this compensation, angle estimation errors increase with speed, which makes ultra-high-speed operation unfeasible. Implementing the proposed method enhances control performance in ultra-high-speed sensorless motor drive systems. The effectiveness of the proposed time-delay compensation has been validated through simulations and experiments. The results demonstrate its capability to enable sensorless operation at an ultra-high speed of 150 kr/min, where the  $F_{ratio}$  is as low as 8.

**Acknowledgements** This work was supported by the National Research Foundation of Korea (NRF) grant funded by the Korea government (MSIT) (No. RS-2023-00207865) and by Hanwha Aerospace through the E-Drive Hub.

## Declarations

**Conflict of interest** While conducting this study, Young-Doo Yoon served as an Editor of the Journal of Power Electronics. Editorial Board Member status has no bearing on editorial consideration.

## References

- Kang, S.-H., Lee, H.-J., Woo, T.-G., You, C.-S., Lim, S.-H., Yoon, Y.-D.: Time Delay Implementation in Sensorless Control for Ultra-High-Speed Air Compressor Motor of Fuel-Cell Systems, 2024 IEEE 10th International Power Electronics and Motion Control Conference (IPEMC2024-ECCE Asia), Chengdu, China, pp. 2332–2337, (2024). <https://doi.org/10.1109/IPEMC-ECCEAsia60879.2024.10567890>
- Hu, D., Wang, J., Hu, L., Zhou, J., Liu, J.: Research on the Damping Effect Mechanism and Optimization of Super-High-Speed Electric Air Compressors for Fuel Cell Vehicles Under the Stiffness Softening Effect. *IEEE Access* **8**, 179789–179797 (2020). <https://doi.org/10.1109/ACCESS.2020.3015850>
- Yi, F., et al.: Response Analysis and Stator Optimization of Ultra-high-Speed PMSM for Fuel Cell Electric Air Compressor. *IEEE Transactions on Transportation Electrification* **9**(4), 5098–5110 (2023). <https://doi.org/10.1109/TTE.2022.3216925>
- Floris, A., Damiano, A., Serpi, A.: A combined design procedure of High-Speed/High-Power PMSMs for an adiabatic compressed air energy storage system. *IEEE Trans. Ind. Appl.* **60**(1), 256–268 (2024). <https://doi.org/10.1109/TIA.2023.3336312>
- Sheianov, A., Xiao, X.: Fast sensorless startup method for ultra-high-speed PMSMs with air bearings. *J. Power Electron.* **24**, 55–67 (2024). <https://doi.org/10.1007/s43236-023-00686-0>
- Zhang, Q., Feng, M.: Combined commutation optimisation strategy for brushless DC motors with misaligned hall sensors. *IET Electric Power Applications* **12**, 301–307 (2018). <https://doi.org/10.1049/iet-epa.2017.0276>
- Akrami, M., Jamshidpour, E., Frick, V.: Application of Hall Position Sensor in Control and Position Estimation of PMSM - A Review, *IEEE International Conference on Environment and Electrical Engineering and 2023 IEEE Industrial and Commercial Power Systems Europe (EEEIC / I&CPS Europe)*, Madrid, Spain, 2023, pp. 1–6, (2023). <https://doi.org/10.1109/EEEIC/ICPSEurope57605.2023.10194763>
- Yoo, A., Sul, S.-K., Lee, D.-C., Jun, C.-S.: Novel Speed and Rotor Position Estimation Strategy Using a Dual Observer for Low-Resolution Position Sensors. *IEEE Transactions on Power Electronics* **24**(12), 2897–2906 (2009). <https://doi.org/10.1109/TPEL.2009.202296>
- Yim, Chong-Hyuk., Ha, In-Joong., Ko, Myoung-Sam.: A resolver-to-digital conversion method for fast tracking. *IEEE Transactions on Industrial Electronics* **39**(5), 369–378 (1992). <https://doi.org/10.1109/41.161468>
- Wang, G., Valla, M., Solsona, J.: Position Sensorless Permanent Magnet Synchronous Machine Drives—A Review. *IEEE Transactions on Industrial Electronics* **67**(7), 5830–5842 (2020). <https://doi.org/10.1109/TIE.2019.2955409>
- Wu, C., Sha, W., Zhu, C.: Online correction method for phase current gain errors in permanent magnet synchronous motor sensorless control. *J. Power Electron.* **24**, 1778–1790 (2024). <https://doi.org/10.1007/s43236-024-00850-0>
- Yoon, Y.-D., Sul, S.-K., Morimoto, S., Ide, K.: High-Bandwidth Sensorless Algorithm for AC Machines Based on Square-Wave-Type Voltage Injection. *IEEE Transactions on Industry Applications* **47**(3), 1361–1370 (2011). <https://doi.org/10.1109/TIA.2011.2126552>
- Kwon, Y.-C., Lee, J., Sul, S.-K.: Extending Operational Limit of IPMSM in Signal-Injection Sensorless Control by Manipulation of Convergence Point. *IEEE Transactions on Industry Applications* **55**(2), 1574–1586 (2019). <https://doi.org/10.1109/TIA.2018.2882483>
- Morimoto, S., Kawamoto, K., Sanada, M., Takeda, Y.: Sensorless control strategy for salient-pole PMSM based on extended EMF in rotating reference frame. *IEEE Trans. Ind. Appl.* **38**(4), 1054–1061 (2002). <https://doi.org/10.1109/TIA.2002.800777>
- Tuovinen, T., Ali Awan, H.A., Kukkola, J., Saarakkala, S.E., Hinkkanen, M.: Permanent-Magnet Flux Adaptation for Sensorless Synchronous Motor Drives, 2018 IEEE 9th International Symposium on Sensorless Control for Electrical Drives (SLED), Helsinki, Finland, pp. 138–143, (2018). <https://doi.org/10.1109/SLED.2018.8485899>
- Hinkkanen, M., Saarakkala, S.E., Awan, H.A.A., Mölsä, E., Tuovinen, T.: Observers for Sensorless Synchronous Motor Drives: Framework for Design and Analysis. *IEEE Transactions on Industry Applications* **54**(6), 6090–6100 (2018). <https://doi.org/10.1109/TIA.2018.2858753>
- Bae, B.-H., Sul, S.-K.: A compensation method for time delay of full-digital synchronous frame current regulator of PWM AC drives. *IEEE Trans. Ind. Appl.* **39**(3), 802–810 (2003). <https://doi.org/10.1109/TIA.2003.810660>
- Yim, J.-S., Sul, S.-K., Bae, B.-H., Patel, N.R., Hiti, S.: Modified Current Control Schemes for High-Performance Permanent-Magnet AC Drives With Low Sampling to Operating Frequency Ratio. *IEEE Transactions on Industry Applications* **45**(2), 763–771 (2009). <https://doi.org/10.1109/TIA.2009.2013600>

Springer Nature or its licensor (e.g. a society or other partner) holds exclusive rights to this article under a publishing agreement with the author(s) or other rightsholder(s); author self-archiving of the accepted manuscript version of this article is solely governed by the terms of such publishing agreement and applicable law.

**Sung-Ho Kang** was born in South Korea. He received his B.S degree in Automotive Engineering from Kyungpook National University, Dague, South Korea, in 2021. He has been working toward his Ph.D. degree in Automotive Engineering at the Power Electronics Laboratory, Hanyang University, Seoul, South Korea. His research interests include power electronic control of electric machines, high-efficiency control, and sensorless control.

**Hyun-Jun Lee** was born in South Korea. He received a B.S. degree in Electrical Engineering in 2017 from Myongji University, Yongin, South Korea, and a Ph.D. degree in Automotive Engineering in 2023 from Hanyang University, Seoul, South Korea. In 2023, he was a researcher at the Research Institute of Automotive Electronics and Control at Hanyang University. Since 2024, he has been a senior research engineer at Hyundai Motor Company. His research interests encompass position sensorless control of electric machines, electric/hybrid vehicle drives, and high-power/multi-level converters.

**Tae-Gyeom Woo** was born in South Korea. He received the B.S. degree in Mechanical Engineering from the Korea Aerospace University, Goyang, South Korea, in 2018, and the Ph.D. degree in Automotive Engineering from Hanyang University, Seoul, South Korea, in 2024. Since 2024, he has been a senior research engineer with Hyundai Motor Company, Namyang, South Korea. His research interests comprise control systems, electric drives, and power converters.

**Chang-Seok You** was born in South Korea. He received his B.S. degree in Electrical Engineering from Korea University, Seoul, South Korea in 2003. He has been working at the Hyundai Motor Company, Yong-in, South Korea. His primary responsibility is developing control algorithms for air compressor motor in fuel cell systems.

**Sanghak Lim** was born in South Korea. He is a research engineer with expertise in power electronic control and sensorless control systems. He earned his B.S. in Electrical Engineering from Myongji University in 2019 and continued his studies with an M.S. in Automotive Engineering from Hanyang University. Currently, he works at Hyundai Motor Company. He specializes in the advancement of fuel cell system control development.

**Young-Doo Yoon** received the B.S., M.S., and Ph.D. degrees in Electrical Engineering from Seoul National University, Seoul, South Korea, in 2002, 2005, and 2010, respectively. From 2010 to 2013, he was at Samsung Electronics Company, South Korea, as a senior engineer. From 2013 to 2017, he was an Assistant Professor in the Department of Electrical Engineering, Myongji University, Yongin, South Korea. Since 2017, he has been a faculty member of the Department of Automotive Engineering, Hanyang University, Seoul, South Korea, where he is currently a Professor. His current research interests include power electronic control of electric machines, highpower converters, electric vehicles, and electric home appliances.