

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the journal Optics Communications](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the journal Optics Communications

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# High-precision time delay compensation to achieve a low noise floor in fiber-optic interferometers by using linear interpolation

Jie Yao<sup>a,b</sup>, Xiaopeng Liu<sup>a,b</sup>, Xuqiang Wu<sup>a,b,c,\*</sup> ![ORCID icon](17413706fd4997a1a4bdf85c6864eee1_img.jpg), Qiliang Xia<sup>a,b</sup>, Siyu Zhang<sup>a,b</sup>,  
Jinhui Shi<sup>a,b,c</sup>, Yumei Pan<sup>d</sup>, Benli Yu<sup>b,c</sup>

<sup>a</sup> Key Laboratory of Opto-Electronic Information Acquisition and Manipulation of Ministry of Education, School of Physics and Optoelectronic Engineering, Anhui University, Hefei, 230601, China

<sup>b</sup> National Key Laboratory of Opto-Electronic Information Acquisition and Protection Technology, Anhui University, Hefei, 230601, China

<sup>c</sup> Information Materials and Intelligent Sensing Laboratory of Anhui Province, Anhui University, Hefei, 230601, China

<sup>d</sup> Changhong Meiling Co., Ltd., No. 2163, Lianhua Road, Hefei, Anhui Province, 230601, China

## ARTICLE INFO

### Keywords:

Phase demodulation  
Linear interpolation  
Delay compensation  
Low noise floor

## ABSTRACT

This paper proposes a linear interpolation compensation reference path scheme to suppress laser relative intensity noise and reduce the noise floor in the  $3 \times 3$  interferometric system, which includes the measurement and compensation of time delay. The traditional reference path scheme requires high optical path simultaneity, otherwise, the denoising effect weakens with time delay. By using the linear interpolation technique to improve compensation accuracy and data shifting to compensate for time delay. After compensating for the time delay, the interference signal is directly divided by the reference optical signal to eliminate the laser relative intensity noise. The experimental results show that compared with the traditional demodulation scheme, the average noise level of the system is reduced to  $-115$  dB, with a maximum reduction of 23.1 dB at 50 kHz. This addresses the shortcomings of the traditional demodulation scheme in fiber optic sensing systems with time delay and significantly improves the detection resolution of long-distance fiber optic transmission.

## 1. Introduction

Fiber optic interferometric sensors (FOIS) are extensively used in defense and civil applications, including hydroacoustic monitoring, pipeline leakage detection, and tunneling construction, due to their high sensitivity, excellent electromagnetic resistance, and good reusability [1–4]. The performance of FOIS is directly affected by the demodulation scheme used. Compared to other demodulation schemes, the  $3 \times 3$  coupler demodulation technique as a passive demodulation scheme with a simpler system and wider dynamic range [5–9], has gradually become a research hotspot.

In fiber optic sensing systems, although semiconductor lasers have low relative intensity noise (RIN), they exhibit high phase noise during frequency modulation due to the requirement of using the unbalanced interferometer for interrogation, which limits their further applications [10,11]. In this case, fiber optic lasers with low phase noise become a better choice.

Many efforts have been made to suppress the impact of RIN on fiber

optic lasers. R.B. et al. developed a dual-channel detection scheme that suppresses the flat band between the two signal peaks to  $-76 \pm 1$  dBV [12]. In this scheme, the direct current (DC) dominates the signal, and noise can be effectively suppressed through dual-channel subtraction. However, in the FOIS system, as the proportion of the DC component decreases, the suppression effect of the original scheme will be less effective. Other studies introduced a reference path to obtain laser intensity fluctuations and use the common-mode characteristics of the signals to suppress RIN [13,14], but this approach requires strict simultaneity between the interference and reference signals, making it difficult to scale for practical applications. Z. Guan et al. found that time delay caused by signal non-simultaneity disrupts common-mode characteristics [15], particularly in long-distance or multiplexed sensor systems, where time delay will lead to degraded noise suppression and even increased noise at high frequencies in the system.

In order to precisely compensate for system time delay, this paper proposes the linear interpolation compensation reference path scheme (REF-LIC) for  $3 \times 3$  coupler interferometric systems. Without increasing

\* Corresponding author. Key Laboratory of Opto-Electronic Information Acquisition and Manipulation of Ministry of Education, School of Physics and Opto-electronic Engineering, Anhui University, Hefei, 230601, China.

E-mail address: [atlaswoo@126.com](mailto:atlaswoo@126.com) (X. Wu).

**Table 1**

The measurement of time delay by the REF-LIC scheme.

| $m$                                                 | $m = 1$              | $m = 2$           | $m = 3$           |
|-----------------------------------------------------|----------------------|-------------------|-------------------|
| Corresponding frequency(Hz)                         | $f_1 = 79,951$       | $f_2 = 159,894$   | $f_3 = 239,569$   |
| Calculated $t_d$ ( $\mu$ s)                         | $t_{d1} = 12.508$    | $t_{d2} = 12.508$ | $t_{d3} = 12.522$ |
| The calculated length difference ( $\Delta L$ , Km) | 2.556                | 2.556             | 2.559             |
| Relative error (%)                                  | 0.312                | 0.312             | 0.195             |
| Calculate the average value of $t_d$ ( $\mu$ s)     | $\bar{t}_d = 12.513$ |                   |                   |

the complexity of the system, the scheme employs the linear interpolation technique to achieve high-precision time delay compensation through arbitrary multiple-point data shifting, effectively suppressing RIN. The stability and effectiveness of this scheme in noise suppression will be demonstrated through theoretical analysis and experimental validation.

## 2. Principles

### 2.1. Principle of relative intensity noise suppression

As shown in Fig.1, the output voltage signal of the interferometer based on a  $3 \times 3$  coupler can be expressed as:

$$\begin{cases} U_1(t) = A(1 + n_i(t))(1 + \nu \cos \varphi(t)) \\ U_2(t) = A(1 + n_i(t))[1 + \nu \cos(\varphi(t) + \theta)] \end{cases} \quad (1)$$

Where  $A$  is the DC bias voltage of the interference signal,  $n_i(t)$  refers to the fluctuations of laser intensity, which is usually much smaller than 1.  $\nu$  denotes the visibility of the fringe.  $\varphi(t)$  represents the phase change induced by the measured physical quantity.  $\theta$  denotes the phase difference introduced by the  $3 \times 3$  coupler. We use the additional photodetector (PD) to obtain the intensity fluctuations of the laser, and the corresponding voltage signal received can be expressed as a reference signal:

$$U_r(t) = A(1 + n_i(t + t_d)). \quad (2)$$

$n_i(t + t_d)$  represents RIN with a time delay, where  $t_d$  denotes the time

![Figure 1: The process of relative intensity noise suppression by the REF-LIC scheme. The diagram shows three input signals: U1(t), U2(t), and Ur(t). U1(t) and U2(t) are processed by FFT blocks to produce U1(ω)' and U2(ω)'. These are then combined with Ur(t) in a mixer block. The output of this mixer is processed by another FFT block, which shows 'dip points appearing' on the spectrum. A 'Calculate the appropriate k' block determines the compensation factor. This factor is used in a 'Linear Interpolation' block, which also takes U1(t) and U2(t) as inputs. The output of the linear interpolation block is used to 'Compensate td'. This compensation is applied to the reference signal Ur(t) in a mixer block. The output of this mixer is processed by an EFA (Envelope Following Amplifier) block, followed by an ATAN block to produce the phase φ(t).](a2dc8d6396228142d4c2c1d3160b47dc_img.jpg)

Figure 1: The process of relative intensity noise suppression by the REF-LIC scheme. The diagram shows three input signals: U1(t), U2(t), and Ur(t). U1(t) and U2(t) are processed by FFT blocks to produce U1(ω)' and U2(ω)'. These are then combined with Ur(t) in a mixer block. The output of this mixer is processed by another FFT block, which shows 'dip points appearing' on the spectrum. A 'Calculate the appropriate k' block determines the compensation factor. This factor is used in a 'Linear Interpolation' block, which also takes U1(t) and U2(t) as inputs. The output of the linear interpolation block is used to 'Compensate td'. This compensation is applied to the reference signal Ur(t) in a mixer block. The output of this mixer is processed by an EFA (Envelope Following Amplifier) block, followed by an ATAN block to produce the phase φ(t).

**Fig. 1.** The process of relative intensity noise suppression by the REF-LIC scheme.

delay caused by the length difference between the reference and the interference optical paths.

In this work, we define the RIN as the superposition of individual frequency noise components:

$$n_i(t) = \sum_{n=1}^{\infty} X_n \cdot \cos(2\pi f_n t + \varphi_n). \quad (3)$$

where  $X_n$ ,  $f_n$  and  $\varphi_n$  represent respectively the amplitude, frequency and initial phase of the noise.  $n_i(t + t_d)$  can be expanded as:

$$n_i(t + t_d) = \sum_{n=1}^{\infty} X_n \cdot \cos(2\pi f_n t + 2\pi f_n t_d + \varphi_n). \quad (4)$$

In the reference path scheme, the interference path signal is divided by the reference path signal to suppress intensity noise. This process can be expressed as Eq. (1) divided by Eq. (2), and the resulting signals can be reformulated as:

$$\begin{cases} U_1(t)' = \frac{1 + \sum_{n=0}^{\infty} X_n \cdot \cos(2\pi f_n t + \varphi_n)}{1 + \sum_{n=0}^{\infty} X_n \cdot \cos(2\pi f_n t + 2\pi f_n t_d + \varphi_n)} [1 + \nu \cos \varphi(t)] \\ U_2(t)' = \frac{1 + \sum_{n=0}^{\infty} X_n \cdot \cos(2\pi f_n t + \varphi_n)}{1 + \sum_{n=0}^{\infty} X_n \cdot \cos(2\pi f_n t + 2\pi f_n t_d + \varphi_n)} [1 + \nu \cos(\varphi(t) + \theta)] \end{cases} \quad (5)$$

Ideally, the time delay between the interference and reference signals is zero ( $t_d$  is equal to zero), in this case,  $f_n t_d$  is zero. Eq. (5) can be rewritten as:

$$\begin{cases} U_1(t)' = 1 + \nu \cos \varphi(t) \\ U_2(t)' = 1 + \nu \cos(\varphi(t) + \theta) \end{cases} \quad (6)$$

The equation shows that the RIN is effectively eliminated. However, this traditional reference path scheme imposes strict simultaneity requirements on the system. In practical applications, especially in long-distance or multiplexed sensor systems, achieving such simultaneity is challenging and time delay becomes non-negligible.

From Eq. (4),  $f_n t_d$  approaches zero and  $n_i(t + t_d)$  approaches  $\sum_{n=1}^{\infty} X_n \cdot \cos(2\pi f_n t + \varphi_n)$  at low frequencies, the RIN suppression remains effective. When the time delay is present, as the frequency increases,  $f_n t_d$  no longer approaches zero, as shown in Eq. (5) and the denoising effect degrades. However, due to the periodic nature of the cosine function, when  $f_n t_d$  is equal to  $m$  ( $m = 1, 2, 3 \dots$ ), an optimal denoising effect can be achieved again, appearing dip points on the spectrum. As  $f_n$  increases further,  $n_i(t + t_d)$  continues to exhibit periodic variation and the RIN suppression effect also undergoes periodic changes.

In this paper, the linear interpolation technique is used to achieve high precision time delay compensation, making the time delay approaches zero and thereby achieving effective RIN suppression.

### 2.2. Principle of linear interpolation digital compensation technique

According to the above theoretical derivation, when  $f_n t_d$  is equal to  $m$ , dip points will appear on the spectrum. Therefore, we can calculate  $t_d$  through this relationship:

$$t_d = \frac{m}{f_n}. \quad (7)$$

The time interval between every two sampling points is denoted by  $\Delta t$ :

$$\Delta t = \frac{1}{M}. \quad (8)$$

Where  $M$  is the sampling rate of the acquisition card. In an ideal case, when  $t_d$  is an integer multiple of the  $\Delta t$ , by shifting the corresponding multiple data points can realize time delay compensation. However, in practical situations,  $t_d$  is usually a non-integer multiple of the  $\Delta t$  obviously, the compensation precision is limited by the sampling rate. To address this, we introduce the linear interpolation technique that inserts

$k$  points between every two sampling points, then the minimum time unit of compensation is reduced to:

$$\Delta t' = \frac{1}{(k+1)M}. \quad (9)$$

Without changing the experimental conditions, we can select an appropriate  $k$  for interpolating to improve compensation precision, which enables precise time delay compensation for any multiple of  $t_d$ . The  $k$  can be determined by the dip points, which will be further experimentally validated in subsequent sections.

After precisely compensating for the time delay using linear interpolation technique, the time delay will approach zero, and the interference signals can be derived as given in Eq. (6). We use the ellipse fitting algorithm (EFA) to obtain a pair of orthogonal signals with zero DC components and normalized alternating current (AC) components. Then, the ATAN algorithm is applied to demodulate the orthogonal signals, deriving the phase information  $\varphi(t)$ .

## 3. Simulation

### 3.1. The measurement of time delay

In the simulation, LabVIEW was employed to simulate the impact of time delay on the RIN suppression effect. The frequency and amplitude of the simulated sinusoidal signals are 500 Hz and 3.6 rad respectively. The intensity noise amplitude was set to 0.001. To simulate the experimental environment more realistically, Gaussian white noise with an amplitude of  $1E-4$  was introduced into the system as additional noise. The sampling rate was set at 400k/s, the number of samples was 400k, and a time delay of  $6.25\mu\text{s}$  was set for the two interference signals.

To validate the theory in Section 2, we averaged multiple times the spectrum data obtained by dividing the interference path by the reference path, as shown in Fig. 2, which illustrates how the denoising effect varies with frequency. When the denoising effect reaches its optimal state, the dip point will appear accordingly. To observe the frequency corresponding to the dip point more clearly, we used Origin for data smoothing and magnified it. Although the frequency of the dip point exhibits slight fluctuations in practice, the time fluctuations caused by such fluctuations are at the nanosecond level or even lower. Moreover, through multiple averaging of the data in the experiment, this difference is further reduced. From the enlarged view, it can be seen that the dip point appears at 159917 Hz. According to Eq. (7), the calculated time delay is  $6.253\mu\text{s}$ , with an error of approximately 0.048 %.

![Figure 2: Spectrum plot showing Amplitude/dB versus Frequency/Hz. The main plot shows a broad noise floor with a dip point at 159917 Hz. An inset shows a magnified view of the dip point, indicating f = 159917 Hz.](3547d8dc1ba9bc8e4bbec26b5724549d_img.jpg)

Figure 2: Spectrum plot showing Amplitude/dB versus Frequency/Hz. The main plot shows a broad noise floor with a dip point at 159917 Hz. An inset shows a magnified view of the dip point, indicating f = 159917 Hz.

**Fig. 2.** The spectrum was obtained by dividing the interference path by the reference path, and the enlarged view near the dip point was used to observe the frequency corresponding to the dip point.

### 3.2. The superiority of high precision compensation

From Eq. (8), the time interval between every two sampling points is  $2.5\mu\text{s}$  at this time. To compensate for the  $6.25\mu\text{s}$  time delay in the system, it is necessary to shift 2.5 data points, but the common digital shifting technique cannot handle non-integer point compensation. By finding the smallest integer multiple of  $\Delta t$  for  $t_d$ , we found that shifting the data by 5 points meets the condition.

$$\Delta t' = \frac{t_d}{5} = 1.25\mu\text{s}. \quad (10)$$

By combining Eq. (9) and Eq. (10), the optimal linear interpolation value  $k$  is calculated to be 1. The limitation caused by the sampling rate can be overcome, enabling compensation for arbitrary multiples of points through linear interpolation. This paper named the traditional EFA demodulation scheme as the Non-denoised scheme and the common digital shifting technique is named as the Common time delay compensation scheme. We shifted 2 data points by using the common digital shifting technique, which could only compensate for the  $5\mu\text{s}$  time delay.

Although the Common time delay compensation scheme compensates for part of the time delay and can effectively suppress RIN at low frequencies, the residual time delay ( $1.25\mu\text{s}$ ) still impacts the system performance. This leads to degraded denoising effectiveness and the effects are particularly obvious in the high frequency regions, as shown in Fig. 3. In contrast, the REF-LIC scheme effectively suppresses the RIN across the entire frequency band. Compared with the Common time delay compensation scheme, it achieves a maximum reduction of 24.2 dB at 50 kHz.

In order to better observe the influence of the time delay on the demodulation system and the suppression effect of the REF-LIC scheme, we have broadened the displayed frequency band, as shown in Fig. 3(b).

![Figure 3: (a) Spectrum comparison of Non-denoised, Common time delay compensation, and REF-LIC schemes from 0 to 50 kHz. (b) Spectrum comparison of the three schemes from 0 to 100 kHz. Both plots show Amplitude/dB vs Frequency/Hz. REF-LIC (red) shows the lowest noise floor. In (a), REF-LIC is 24.2 dB lower than the Common time delay compensation scheme (orange). In (b), REF-LIC is 26.2 dB lower than the Common time delay compensation scheme (orange).](efe05e64cc211c110cbc96718fb54d44_img.jpg)

Figure 3: (a) Spectrum comparison of Non-denoised, Common time delay compensation, and REF-LIC schemes from 0 to 50 kHz. (b) Spectrum comparison of the three schemes from 0 to 100 kHz. Both plots show Amplitude/dB vs Frequency/Hz. REF-LIC (red) shows the lowest noise floor. In (a), REF-LIC is 24.2 dB lower than the Common time delay compensation scheme (orange). In (b), REF-LIC is 26.2 dB lower than the Common time delay compensation scheme (orange).

**Fig. 3.** (a) The spectrum comparison of the Non-denoised scheme demodulation results, the Common time delay compensation scheme demodulation results, and the REF-LIC demodulation results within the range of 0–50 kHz. (b) The spectral comparison of the demodulation results for the three different schemes within the range of 0–100 kHz.

The REF-LIC scheme can still effectively suppress the relative intensity noise (RIN) at higher frequencies. However, in practical applications, it is sufficient to ensure the noise suppression effect in the 0–50 kHz frequency band.

## 4. Experimental setup and results

### 4.1. Experiment setup

The schematic diagram of the experimental configuration is shown in Fig. 4. The output of a 1550 nm low phase noise single-frequency fiber laser (Koheras BASIK X15, NKT Photonics) is split by a  $1 \times 2$  coupler. One output enters the PD as the reference optical path, the other passes through a delay fiber into the interferometer.

This paper uses a Mach-Zehnder interferometer (MZI) composed of a  $1 \times 2$  coupler and a  $3 \times 3$  coupler. One arm of the MZI was wrapped around a piezoelectric tube (PZT) to generate a sinusoidal excitation signal. The output of the  $3 \times 3$  coupler is connected to PDs, which convert the optical signals to electrical signals. These signals are sent to an A/D acquisition card (NI, PXIe-4480), and finally processed by LabVIEW software on a computer.

### 4.2. The effectiveness of time delay measurement

In order to verify the effectiveness of the time delay measurement of our proposed scheme, we apply a 5 V 2 kHz sinusoidal excitation signal to the PZT and set the sampling rate of the data acquisition card to 1 M/s and the number of sampling points to 1 M. Fig. 5 shows the spectrum data obtained by averaging multiple times after dividing the interference path by the reference path.

From Fig. 5, several dip points can be observed. The first dip point appears at 79,951 Hz, where the denoising effect first reaches its optimal, corresponding to  $m$  is equal to 1. We use the same method to obtain the frequency values for the second and third dip points, which are 159,894 Hz and 239,569 Hz respectively, and calculate the corresponding time delay values (see Table 1).

Because  $t_d$  is caused by the length difference between the reference and the interference optical paths, it can also be expressed as:

$$t_d = \frac{n \cdot \Delta L}{c}. \quad (11)$$

Substitute  $\bar{t}_d$  into Eq. (11), and then  $\Delta L$  can be obtained:

$$\Delta L = \frac{c \cdot \bar{t}_d}{n} \approx 2.557 \text{ km}. \quad (12)$$

$c$  is the speed of light in a vacuum.  $\Delta L$  is the length difference between the reference and interference optical paths.  $n$  is the refractive index of the fiber, which is 1.468 provided by the manufacturer. To verify the accuracy of this method, we compared the calculated values with the measured values (2.564 km) from a commercial optical time domain reflectometer (OTDR). The data shows that the maximum measurement error of this method is only 0.312 %. During the experiment, we performed multiple averaging on the data, which further reduced the actual error. The results show that the deviation between

![Schematic diagram of the experimental setup. A laser source emits light through a 1x2 coupler. One path goes to a photodetector (PD1) as the reference path. The other path goes through a delay fiber (labeled with a blue circle and Greek letter Omega) into a Mach-Zehnder Interferometer (MZI). The MZI consists of a 1x2 coupler followed by a piezoelectric tube (PZT) and a 3x3 coupler. The 3x3 coupler has three outputs: one to PD2, one to PD3, and one back to the laser. The signals from PD1, PD2, and PD3 are connected to a Data Acquisition (DAQ) card, which is linked to a PC for processing.](476d6fb9044a040636d52619c7c43b1a_img.jpg)

Schematic diagram of the experimental setup. A laser source emits light through a 1x2 coupler. One path goes to a photodetector (PD1) as the reference path. The other path goes through a delay fiber (labeled with a blue circle and Greek letter Omega) into a Mach-Zehnder Interferometer (MZI). The MZI consists of a 1x2 coupler followed by a piezoelectric tube (PZT) and a 3x3 coupler. The 3x3 coupler has three outputs: one to PD2, one to PD3, and one back to the laser. The signals from PD1, PD2, and PD3 are connected to a Data Acquisition (DAQ) card, which is linked to a PC for processing.

Fig. 4. Schematic diagram of the experimental setup.

![Figure 5: Spectrum plot showing Amplitude in dB versus Frequency in Hz. The main plot shows a noisy signal with periodic dips. An inset provides a magnified view of the dip at 79,951 Hz, labeled 'dip point' with a red arrow. The x-axis ranges from 0 to 280,000 Hz, and the y-axis ranges from -150 to -25 dB.](06509cc49f3023389a3f15c106907140_img.jpg)

Figure 5: Spectrum plot showing Amplitude in dB versus Frequency in Hz. The main plot shows a noisy signal with periodic dips. An inset provides a magnified view of the dip at 79,951 Hz, labeled 'dip point' with a red arrow. The x-axis ranges from 0 to 280,000 Hz, and the y-axis ranges from -150 to -25 dB.

Fig. 5. The spectrum was obtained by dividing the interference path by the reference path, and the enlarged view near the dip point was used to observe the frequency corresponding to the dip point.

the value calculated using Eq. (12) and the measured value is 0.27 %. Therefore, we can measure the time delay using the proposed method and perform subsequent time delay compensation.

### 4.3. The effectiveness of relative intensity noise suppression

According to Eq. (8), the time interval between every two sampling points is 1  $\mu$ s. Using the Common time delay compensation scheme, the optimal compensation can only be achieved by shifting 12 integer data points, yet a residual time delay of approximately 0.5  $\mu$ s still remains. To visually demonstrate the noise reduction effect, we compare the interference signal waveforms, Lissajous figures, and demodulated signal spectrum of three different schemes—the Non-denoised scheme, the Common time delay compensation scheme, and the REF-LIC scheme, and evaluate the noise reduction performance of the proposed method.

With a 5 V 1 kHz sinusoidal signal applied to the PZT, Fig. 6(a) displays the time-domain figure of the interference signal under the Non-denoised scheme, which exhibits noticeable fluctuations and distortions at the amplitude. After noise reduction using the Common time delay compensation scheme, the fluctuations and distortions persist, and the intensity variations are not completely eliminated, as shown in Fig. 6(b). After the REF-LIC scheme noise reduction processing, the interference signals become noticeably smoother, with irregular fluctuations and distortions in the waveform effectively suppressed as shown in Fig. 6(c).

The Lissajous figure generated by the Non-denoised scheme is presented in Fig. 7(a), exhibiting irregular glitches in the elliptical arcs. Glitches along the elliptical arc are reduced after applying the Common time delay compensation scheme, yet they still remain, as shown in Fig. 7(b). In contrast, Fig. 7(c) displays the Lissajous figure composed of the interference signals after REF-LIC noise reduction. Compared with Fig. 7(a) and (b), the irregular glitches along the elliptical arc have been removed, making it appear thinner and smoother. Based on the analysis and comparison above, the REF-LIC scheme can effectively eliminate noise from the interference signals.

According to the derivation in Section 3, we can also calculate the appropriate value of  $k$  for interpolation to compensate for the system time delay. To more rigorously observe the denoising effect of the proposed method, the root mean square (RMS) spectrum obtained from the different demodulation schemes after Fourier transformation is shown in Fig. 8, with 0 dB corresponding to  $1 \text{ rad}/\sqrt{\text{Hz}}$ .

Fig. 8(a) indicates that the Common time delay compensation scheme can suppress the degradation of the noise reduction effect at low frequencies, but it cannot completely suppress it. As the frequency

![Figure 6: Interference signals U1'(t) and U2'(t) over time. (a) Non-denoised scheme: U1'(t) is blue, U2'(t) is red. (b) Common time delay compensation scheme: U1'(t) is blue, U2'(t) is red. (c) REF-LIC scheme: U1'(t) is red, U2'(t) is blue. All plots show Amplitude/V vs Time/s from 0.0000 to 0.0010.](7a3561af571faf036baa93f5f4b1bdb9_img.jpg)

Figure 6: Interference signals U1'(t) and U2'(t) over time. (a) Non-denoised scheme: U1'(t) is blue, U2'(t) is red. (b) Common time delay compensation scheme: U1'(t) is blue, U2'(t) is red. (c) REF-LIC scheme: U1'(t) is red, U2'(t) is blue. All plots show Amplitude/V vs Time/s from 0.0000 to 0.0010.

Fig. 6. (a) The interference signals after the Non-denoised scheme, (b) The interference signal after the Common time delay compensation scheme, (c) The interference signals after the REF-LIC scheme.

![Figure 7: Lissajous figures of U1'(t) vs U2'(t). (a) Non-denoised scheme: a blue circle. (b) Common time delay compensation scheme: an orange circle. (c) REF-LIC scheme: a red circle. All plots have axes from -1.5 to 1.5.](b15e3860e0c96ed16ce77f032da6f107_img.jpg)

Figure 7: Lissajous figures of U1'(t) vs U2'(t). (a) Non-denoised scheme: a blue circle. (b) Common time delay compensation scheme: an orange circle. (c) REF-LIC scheme: a red circle. All plots have axes from -1.5 to 1.5.

Fig. 7. (a) Lissajous figure generated by the Non-denoised scheme, (b) Lissajous figure generated by the Common time delay compensation scheme, (c) Lissajous figure generated by the REF-LIC scheme.

increases, the degradation becomes more obvious. In the frequency range from 35 kHz to 50 kHz, the system noise level exhibits an upward trend, which is consistent with the simulation results mentioned above. However, since the residual time delay is merely  $0.5\mu\text{s}$ , which is smaller than that in the simulation, the noise does not increase as dramatically as in the simulation. This is consistent with our theory, which shows that a larger residual time delay results in more obvious degradation in noise suppression at higher frequencies.

Fig. 8(b) shows that compared with the Common time delay compensation scheme, the REF-LIC scheme can efficiently suppress RIN across the entire frequency range. It effectively reduces the system's average noise level to  $-115\text{ dB}$ , achieving an approximately  $7.2\text{ dB}$  greater maximum reduction at  $50\text{ kHz}$ . In contrast to the Non-denoised scheme, the REF-LIC scheme reduces the system's average noise level more significantly, achieving a maximum reduction of  $23.1\text{ dB}$  at  $50\text{ kHz}$ . Moreover, it also demonstrates a remarkable suppression effect at low frequencies.

![Figure 8: Spectrum comparison of Non-denoised, Common time delay compensation, and REF-LIC schemes. (a) Non-denoised (blue) vs Common time delay compensation (orange): noise floor -107.8dB, reduction 15.9dB. (b) Non-denoised (blue) vs REF-LIC (red): noise floor -115dB, reduction 23.1dB. Both plots show Amplitude/dB vs Frequency/Hz from 0 to 50000.](bc04d002fc79e8a3637b1552ac3361e6_img.jpg)

Figure 8: Spectrum comparison of Non-denoised, Common time delay compensation, and REF-LIC schemes. (a) Non-denoised (blue) vs Common time delay compensation (orange): noise floor -107.8dB, reduction 15.9dB. (b) Non-denoised (blue) vs REF-LIC (red): noise floor -115dB, reduction 23.1dB. Both plots show Amplitude/dB vs Frequency/Hz from 0 to 50000.

Fig. 8. (a) The spectrum comparison of the Non-denoised scheme demodulation results and the Common time delay compensation scheme demodulation results, (b) the spectrum comparison of the Non-denoised scheme demodulation results and the REF-LIC demodulation results.

## 5. Conclusion

In this paper, we propose and experimentally verify a reference path scheme employing linear interpolation compensation, which aims to suppress RIN across the entire frequency range by compensating for the time delay between the optical paths. Equation derivation and experiments demonstrate the effectiveness of the scheme, and the REF-LIC scheme is able to reduce the system noise level to  $-115\text{ dB}$ , with a maximum reduction of  $23.1\text{ dB}$  at  $50\text{ kHz}$ , compared with the traditional demodulation scheme. The experiments show that the REF-LIC scheme can be expanded to long-distance transmission systems and has a broad potential for engineering applications in FOIS. This technology has significant application potential in phase-generated carrier (PGC) systems. In subsequent research, we plan to design a more comprehensive experimental scheme to further verify and improve the simulation results.

## CRediT authorship contribution statement

**Jie Yao:** Writing – review & editing, Writing – original draft, Supervision, Software, Methodology, Investigation, Data curation, Conceptualization. **Xiaopeng Liu:** Supervision, Software. **Xuqiang Wu:** Writing – review & editing, Supervision. **Qiliang Xia:** Supervision, Software. **Siyu Zhang:** Investigation, Data curation. **Jinhui Shi:** Writing – review & editing, Methodology. **Yumei Pan:** Methodology, Investigation. **Benli Yu:** Writing – review & editing, Supervision.

## Disclosures

The authors declare no conflicts of interest.

### Funding

Anhui Provincial Key Research and Development Program in Basic

### **Field Projects (2023z04020012).**

The Hefei Comprehensive National Science Center.  
The University Synergy Innovation Program of Anhui Province  
(GXXT-2023-016).

## **Declaration of competing interest**

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## **Data availability**

Data will be made available on request.

## **References**

- [1] L. Htein, D.S. Gunawardena, W.H. Chung, H.Y. Au, H.Y. Tam, Accelerometer employing a side-hole fiber in a sagnac interferometer, *J. Lightwave Technol.* 39 (10) (2021) 3303–3311.
- [2] G. Wang, J. Dai, M. Yang, Fiber-optic hydrogen sensors: a review, *IEEE Sens. J.* 21 (11) (2020) 12706–12718.
- [3] J. Shi, B. Yu, Phase-shifted demodulation technique with additional modulation based on a 3×3 coupler and EFA for the interrogation of fiber-optic interferometric sensors, *Opt. Lett.* 46 (12) (2021) 2900–2903.
- [4] H.-E. Joe, H. Yun, S.-H. Jo, M.B.G. Jun, B.-K. Min, A review on optical fiber sensors for environmental monitoring, *Int. J. Precis. Eng. Manuf. Technol.* 5 (1) (2018) 173–191.
- [5] Milos C. Tomic, Zoran V. Djinovic, Slobodan J. Petricevic, Demodulation of quasi-quadrature interferometric signals for use in the totally implantable hearing aids, *Opt. Express* 8 (7) (2017) 3404–3409.
- [6] Z. Zhiqiang, M.S. Demokan, M. MacAlpine, Improved demodulation scheme for fiber optic interferometers using an asymmetric 3×3 coupler, *J. Lightwave Technol.* 15 (11) (1997) 2059–2068.
- [7] J. Yi, Stabilized 3×3-coupler based interferometer for the demodulation of fiber Bragg grating sensors, *Opt. Eng.* 47 (1) (2008), 015006–015006-6.
- [8] K.P. Koo, A.B. Tveten, A. Dandridge, Passive stabilization scheme for fiber interferometers using (3×3) fiber directional couplers, *Appl. Phys. Lett.* 41 (7) (1982) 616–618.
- [9] Y. Zhang, J. Liu, L. Li, F. Gao, Denoising using 3×3 coupler demodulation, *Opt. Eng.* 60 (12) (2021) 127113.
- [10] Huicong Li, Bing Lv, Meng Tian, Wenzhu Huang, Wentao Zhang, Temperature compensation of fiber optic unbalanced interferometers for high resolution static strain sensing, *Opt Laser. Eng.* 174 (2024) 107940.
- [11] W. Huang, W. Zhang, L. Li, H. Zhang, F. Li, Review on low-noise broadband fiber optic seismic sensor and its applications, *J. Lightwave Technol.* 41 (13) (2023) 4153–4163.
- [12] J.R. Battig, R. Stierlin, P.-D. Henchoz, H.P. Weber, New monostatic balanced Doppler velocimeter using a high birefringence fiber, *J. Lightwave Technol.* 6 (1) (1988) 8–11.
- [13] J. Zhang, X. Wu, B. Yu, A low noise floor 3×3 coupler phase demodulation scheme, *J. Lightwave Technol.* 42 (1) (2024) 470–476.
- [14] Y. Zhang, J. Wang, M. Chen, M. Wang, Y. Liang, Z. Meng, A method to eliminate the influence of frequency-modulating-induced auxiliary amplitude modulation on the calibration of 3 × 3 coupler asymmetric parameters, *Sensors* 20 (21) (2020) 6180.
- [15] Z. Guan, et al., Time-delay measurement method based on the frequency-spectrum distribution of laser intensity or phase noise signal, *IEEE Sensor. J.* 25 (2025) 618–624, 1.