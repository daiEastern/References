

## Article

# Delay-Compensated EKF and Adaptive Delay Threshold Weighting for AUV–MDS Docking

Han Yan <sup>1,2,3</sup> ![ORCID icon](c3d993ca47bfe2a953c700506ce31fa0_img.jpg) and Shuxue Yan <sup>1,2,3,\*</sup> ![ORCID icon](c468cde8f04e2e2a6ba3c2a373e05c45_img.jpg)

- <sup>1</sup> University of Chinese Academy of Sciences, Beijing 100049, China; yanhan220284@163.com  
<sup>2</sup> State Key Laboratory of Robotics and Intelligent Systems, Shenyang Institute of Automation, Chinese Academy of Sciences, Shenyang 110016, China  
<sup>3</sup> Key Laboratory of Marine Robotics, Shenyang 110169, China  
\* Correspondence: yansx@sia.cn; Tel.: +86-186-9865-3850

## Abstract

This study tackles real-time state estimation for autonomous underwater vehicle (AUV)–mobile docking station (MDS) cooperation over low-bandwidth, high-latency, jitter-dominated acoustic links, with the goal of turning delayed/out-of-sequence measurements (OOSM) into consistent and informative constraints without sacrificing online operation. We propose an integrated scheme centered on a delay-compensated extended Kalman filter (DC-EKF): a ring buffer enables backward updates and forward replay so that OOSM are absorbed strictly at their physical timestamps; a data-driven delay threshold is learned from “effective information gain” combined with normalized estimation error squared (NEES) filtering; and dynamic confidence, derived from innovation statistics, delay, and signal-to-noise ratio (SNR) proxies, scales the measurement noise to adapt fusion weights. Simulations show the learned delay threshold converges to about 6.4 s (final 6.35 s), error spikes are suppressed, and the overall position root-mean-square error (RMSE) is 5.751 m; across the full data stream, 1067 station measurements were accepted and 30 rejected, and the fusion weights shifted smoothly from inertial measurement unit (IMU)-dominant to station-dominant ( $\approx 0.16/0.84$ ) over time. On this basis, a cooperative augmented EKF (Co-Aug-EKF) is added as a lightweight upper layer for unified-frame cooperative estimation, further improving relative consistency. The results indicate that the framework reliably maps delayed acoustic measurements into closed-loop useful information, significantly enhancing estimator stability and docking readiness, while remaining practical to deploy and readily extensible.

**Keywords:** autonomous underwater vehicle (AUV); acoustic navigation; extended Kalman filter (EKF); sensor fusion; out-of-sequence measurements (OOSM); time-delay compensation; cooperative localization; underwater docking

![Check for updates button](84a1d09fb489061482111515543b60dc_img.jpg)

Check for updates button

Academic Editor: Dong-Sheng Jeng

Received: 31 October 2025

Revised: 27 November 2025

Accepted: 29 November 2025

Published: 1 January 2026

Copyright: © 2026 by the authors.

Licensee MDPI, Basel, Switzerland.

This article is an open access article distributed under the terms and conditions of the [Creative Commons Attribution \(CC BY\) license](https://creativecommons.org/licenses/by/4.0/).

## 1. Introduction

In ice-covered and otherwise challenging ocean environments, satellite navigation is largely unavailable and both geomagnetic cues and acoustic propagation can vary unpredictably [1,2]. During long missions and terminal docking, an autonomous underwater vehicle (AUV) must therefore rely primarily on onboard sensors—IMU, DVL, odometry, and a depth sensor—for inertial and relative navigation [3,4]. Although such proprioceptive measurements are high-rate and timely, they are vulnerable to inertial drift, attitude misalignment, and systematic sensor biases; errors accumulate with mission duration and

often manifest at docking as systematic offsets in position and attitude [5,6]. By contrast, exoceptive observations tied to a global reference—for example, relative range/bearing provided by a mobile docking station (MDS)—can bound this drift and are critical to achieving accurate and robust terminal alignment [7,8]. However, underwater acoustic links are low-bandwidth and slow, with significant delay and jitter [9,10]. As a result, station measurements often arrive late, out of order, or intermittently [11,12]. If used directly to correct the current state, such data induce time misalignment, estimator jumps, and loss of filter consistency, and can even trigger numerical instability [11–14].

Against this backdrop, cooperative docking between an AUV and a mobile docking station (MDS) is compelling [15,16]. The MDS supplies globally referenced observations that periodically recalibrate the AUV state, curbing long-horizon drift; at the terminal stage, maintaining both platforms’ estimates in a common reference frame reduces alignment error and improves convergence speed and stability [7,8,17–19]. The challenge is to exploit the value of MDS observations under low-rate, unreliable communications without degrading the filter with delayed/out-of-sequence data, and to achieve joint estimation of both platforms in a unified frame while preserving closed-loop consistency.

Prior work largely follows three directions. First, for out-of-sequence measurements (OOSM), common strategies include timestamp alignment with “as-if-current” updates, offline smoothing (e.g., RTS smoothing), and history-based backward update with forward recomputation [11–14]. The first ignores covariance evolution and is prone to inconsistency; the second helps with timing but offers limited support for real-time closed-loop control. Second, asynchronous multi-sensor fusion often fixes the measurement covariance within an EKF framework or gates outliers with heuristic thresholds [20]. In acoustic settings where delay and link quality vary over time, fixed covariances fail to reflect changing reliability, and fusion weights can become decoupled from true information content. Third, for cooperative localization and docking, many systems adopt a “loosely coupled” approach: the AUV and the MDS filter independently and only register trajectories or align coordinates near the end of the mission [7,8,15–19]. This leaves relative drift to accumulate and makes closed-loop, real-time consistency at docking difficult.

To address these issues, we propose a practical cooperative estimation framework for ocean deployment that integrates a delay-compensated extended Kalman filter (DC-EKF) and a collaborative augmented EKF (Co-Aug-EKF). The core ideas are: (i) maintain a ring buffer of historical states and covariances; when a delayed measurement arrives, perform a rigorous, consistency-preserving update at its original timestamp, then forward-replay the corrected state and covariance to the present, absorbing “late information” without breaking consistency; (ii) introduce a delay threshold and dynamic confidence allocation: measurements exceeding a benefit-cost knee are softly down-weighted or discarded; within the threshold, adapt the measurement covariance using innovation statistics (e.g., Mahalanobis distance/normalized innovation squared, NIS) and link-quality proxies (delay magnitude/jitter) so that fusion weights track information quality; (iii) formulate a cooperative augmented model that estimates AUV and MDS states in a unified frame, explicitly embedding relative kinematics and bidirectional observations in a single filter loop to suppress relative drift and improve alignment consistency at docking.

Relative to existing approaches, our contributions are threefold. First, the DC-EKF handles OOSM in real time, avoiding the inconsistency of treating delayed measurements as current; numerical stability is maintained via Joseph-form covariance updates and spectral projection when needed. Second, we develop dynamic, statistics-driven confidence weighting so that fusion weights adapt to both link delay and residual quality, balancing robustness with information efficiency. Third, the Co-Aug-EKF unifies the two platforms’ states and relative observations in one estimator, enabling closed-loop consistency

tent, real-time cooperative estimation and providing docking-ready aligned states. The framework exposes a clear engineering interface: MDS observations are first time-rectified and consistently absorbed by the DC-EKF, then passed as observations into the collaborative augmented filter, forming an end-to-end loop from delay robustness to coordinate unification.

All numerical simulations and analyses were implemented in Python (version 3.10) with NumPy (version 1.24). The main contributions are summarized as follows:

- (1) A DC-EKF for real-time delay compensation that absorbs delayed/out-of-sequence measurements via ring-buffered backward updates and forward replay under filter-consistency constraints, preventing time-misalignment jumps.
- (2) A delay threshold with dynamic confidence assignment that adapts measurement covariance using innovation statistics and link-delay features, yielding fusion weights matched to information quality with robust gating.
- (3) A Co-Aug-EKF that achieves closed-loop consistent estimation of AUV-MDS states in a unified frame under relative kinematic constraints, significantly reducing terminal relative drift.
- (4) An engineering pathway and consistency checks (NIS/NEES), together with numerical stabilization strategies, that support reliable online operation.

The remainder of this paper is organized as follows. Section 2 reviews related work on AUV navigation, underwater acoustic localization, delayed/OOS measurement handling, and cooperative estimation. Section 3 specifies the cooperative AUV-MDS system, motion and measurement models, and the noise/delay assumptions, and formulates the estimation problem. Section 4 describes the DC-EKF and ring-buffer-based delay compensation. Section 5 introduces delay threshold calibration and adaptive confidence weighting. Section 6 presents the Co-Aug-EKF and cooperative docking experiments together with a scalability discussion. Section 7 summarizes the main findings, discusses practical limitations, and outlines future work.

In summary, the objective is a real-time estimation scheme for AUV-MDS cooperative docking in GNSS-denied ocean environments that jointly achieves delay robustness and closed-loop consistency. By consistently absorbing delayed/out-of-sequence data, modeling measurement reliability adaptively, and estimating both platforms in an integrated fashion, the proposed methods strike a robust balance between practicality and estimator credibility, offering a reusable pathway to high-precision docking in complex ocean conditions.

## 2. Related Work

AUV state estimation has long relied on strapdown inertial navigation (SINS/IMU), DVL, depth, and odometry within a combined navigation framework, where Bayesian estimators—most prominently the extended Kalman filter (EKF)—dominate sea trials and engineering systems [21–23]. Typical designs constrain kinematic evolution through the process model, correct IMU drift using DVL/depth measurements, and tune measurement covariances across operating conditions to trade off robustness and convergence speed [23,24]. To better cope with strong nonlinearity, attitude coupling, and error propagation, recent work has introduced Lie-group/Lie-algebra error formulations and invariant filtering to reduce linearization sensitivity and improve attitude consistency [21,22,25,26]. Mechanisms for event-triggered updates and correlated-noise handling have been explored to enhance disturbance rejection [27,28]. Data-driven components have also been used to complement the model—for example, learning DVL-related dynamics to improve short-horizon prediction and inference in complex waters [29–31]. Overall, the trend is from a

single EKF configuration toward a composite paradigm that blends stronger modeling with robustness mechanisms and selective data-driven augmentation [21,27,29].

For multi-sensor fusion, EKF/UKF and information filters are widely used to incorporate heterogeneous measurements in a unified state space [26]. System-level challenges include time synchronization, clock drift, and asynchronous sampling; engineering practice therefore adds gating (Mahalanobis distance/chi-square thresholds) and consistency checks (NIS/NEES) to mitigate mismatches [24,32]. In underwater settings, fixed measurement covariances often fail to capture time-varying quality, pushing the field toward adaptive “dynamic confidence” weighting driven by innovation statistics, geometry (range/field-of-view changes), or link-quality proxies, to balance stability and information use [24,33]. Back-end methods based on graph optimization/smoothing (batch or sliding-window) have also been applied to absorb irregularly timed measurements and improve global consistency in offline or near-real-time modes; under low-bandwidth, high-delay acoustic links, their computational and communication costs must be weighed carefully [34,35]. In short, fusion research has moved from idealized assumptions—synchronous, homogeneous, fixed confidence—to realistic constraints: asynchronous, heterogeneous, and time-varying confidence [24,26,32].

Acoustic communication is a key external factor shaping fusion strategies [9,36]. Compared with radio, underwater acoustic links have orders-of-magnitude lower bandwidth, data rates on the order of kilobits per second, and slow propagation. Information experiences significant delay, jitter, and instability; on larger-scale networks, propagation delay depends on medium and range and varies with environment and mission, defying a single universal model [9,36,37]. These properties directly exacerbate delayed, out-of-order, and intermittent measurements [9,32]. Any online estimator that seeks to exploit “global” external observations must therefore account for low-speed, uncertain links, or it will inevitably suffer severe time-misalignment errors and inconsistent updates [14,32].

For delayed and out-of-sequence data, target tracking and navigation offer a well-developed toolbox [14,32,38]. Early work derived consistent update rules and first-order optimal approximations for delayed measurements: perform the measurement update at the original measurement time, then propagate the corrected state and covariance forward to the present, thereby avoiding the inconsistency of treating late data as current; this extends naturally to multi-step delays [14,38]. Subsequent studies trade accuracy for latency via model switching, smoothing, and approximate recomputation [14,32]. More recent efforts propose simplified backward-propagation/forward-replay variants of the Kalman filter, or “delay-aware” EKFs in robotic navigation for remote or lagged measurements [14,32,38]. In essence, OOSM handling has evolved from offline smoothing to real-time backward-forward frameworks suitable for engineering systems.

For cooperative localization and docking, traditional long-baseline (LBL), short-baseline (SBL), and ultra-short-baseline (USBL) systems provide mature external positioning in multi-AUV/base configurations [39–41]. In more flexible missions, mobile beacons/stations can yield more favorable geometry and improve access to global references. Distributed or centralized EKF-based frameworks may absorb relative measurements in a loosely coupled fashion within separate filters, or tightly couple/augment the states in a unified estimator that embeds relative kinematics, thereby suppressing relative drift and improving terminal accuracy [40,41]. Prior studies indicate that single-beacon (SLBL) and mobile-LBL concepts can enable effective acoustic guidance and homing with minimal infrastructure, and distributed acoustic navigation shows promise for sharing information and improving global consistency across platforms. For the strongly coupled docking task, however, unified augmented estimation is typically better suited to achieving closed-loop consistent alignment of pose and trajectory [39,41].

In summary, three lines of work have pushed the frontier: (i) stronger modeling and filtering for AUV navigation under complex flow and sensor degradation, (ii) robustness and adaptive weighting for heterogeneous, asynchronous fusion, and (iii) backward–forward OOSM handling and augmented cooperative estimation frameworks. What remains underexplored is combining severe acoustic delay/out-of-sequence effects, online adaptive confidence, and the unified-frame, closed-loop estimation required at docking within a single real-time system. Existing solutions often lack a clean interface between delay compensation and cooperative augmentation, or rely on static weighting that mismatches link quality and innovation statistics. This motivates an integrated method that connects consistent delay absorption (backward–forward replay), dynamic confidence weighting (driven by NIS/delay/observation conditions), and cooperative state–observation augmentation (closed-loop estimation in a unified frame) to move AUV–MDS cooperative docking from proof of concept toward engineering deployment.

## 3. System Model and Problem Formulation

This section specifies the cooperative AUV–mobile docking station (MDS) setup, the reference frames, motion and measurement models, and the delay/out-of-sequence (OOS) characteristics induced by the acoustic link. On this basis we formalize the state-estimation problem that underpins both the DC-EKF and the Co-Aug-EKF.

### 3.1. AUV–MDS System Architecture

The system consists of one AUV and one maneuverable MDS. The AUV carries onboard sensors (IMU, DVL, depth) that provide high-rate but drifting proprioceptive measurements. The MDS carries an acoustic positioning device (e.g., USBL-like range/bearing sensing) that yields globally referenced relative observations of the AUV. The two platforms exchange measurements and lightweight metadata (timestamps, quality indicators) over an acoustic link characterized by low bandwidth, significant propagation delay and jitter, and occasional OOS arrivals. Control inputs and mission planning are not the focus here; we treat “known or measurable body-frame commands” as exogenous inputs to the kinematic models.

To keep the system model concrete, we instantiate it with the parameters of a typical large, ice-capable survey-class AUV and a matching mobile docking station. Vehicles in the Autosub family have also been studied from an engineering-reliability perspective (e.g., formal-methods-based automated diagnosis), which highlights practical constraints in long-duration missions and motivates the representative platform assumptions adopted here [42]. Recent reviews further summarize the unique challenges and applications of polar AUV operations, supporting the “ice-capable, survey-class” mission envelope considered in this work [43]. On the docking-infrastructure side, docking-station concepts for 21-inch-class AUVs have been developed and ocean-tested, informing the representative docking-port geometry and homing-stage assumptions used in our simulations [44]. In the terminal meters, robust visual guidance and positioning using dedicated light/marker arrangements have also been reported, consistent with our assumption that short-range optical aids can refine final alignment when local visibility permits [45]. In addition, surveys on low-cost underwater sensing and communication platforms motivate modeling the station-side sensing as an acoustic range/bearing device with lightweight metadata exchange under constrained links [46]. The AUV is representative of vehicles such as Autosub 6000 and other deep-diving 21-inch-class AUVs used for polar and deep-sea missions [47,48]. These vehicles are about 5–6 m long, 0.7–0.9 m in diameter, and have dry masses on the order of 1–2 t with depth ratings of several thousand meters. In our simulations, the AUV is modeled as a 5.5 m long, 0.9 m diameter hull with a dry mass of about 1.8 t, a cruise speed

of 1.5 m/s ( $\approx 3$  kn), and a maximum operating depth of 6000 m. The onboard navigation package comprises a tactical-grade IMU, a 300–600 kHz DVL, and a pressure depth sensor. The IMU provides measurements at tens of hertz (10 Hz in the simulations below), while the DVL and depth channels operate at a few hertz. Nominal gyro and accelerometer biases are in the ranges  $1\text{--}10^\circ/\text{h}$  and  $50\text{--}500 \mu\text{g}$ , and the DVL delivers bottom-lock velocity with a typical accuracy of 0.2–0.4% of distance traveled, which is consistent with commercially available marine navigation sensors.

The MDS is modeled as a maneuverable mobile docking station built around a square  $4\text{ m} \times 4\text{ m} \times 4\text{ m}$  frame that supports a funnel-type docking port aligned with the AUV’s longitudinal axis. The docking port has an entrance diameter of about 1.5 m and a length of 3 m, i.e., a capture aperture roughly 1.5–2 times the AUV diameter, similar to reported docking-station designs for 21-inch-class AUVs [49,50]. The frame can be mounted on a low-speed carrier or equipped with small corner wheels for repositioning, but in the estimator we simply treat the MDS as a low-speed rigid body as in Section 3.3. The MDS houses a USBL-like acoustic positioning head and a digital acoustic modem operating in the 20–30 kHz band. Typical working ranges are 1–3 km with data rates of a few kilobits per second; one-way propagation delay is about 0.7 s per kilometer, and additional MAC/queuing and processing delays lead to effective measurement delays of several seconds [50]. In the simulations we model the acoustic delay as a bounded random variable  $\tau \in [0, \tau_{\max}]$ , with  $\tau_{\max}$  between 5 and 10 s depending on the experiment (e.g.,  $\tau_{\max} = 5$  s in the delay-distribution study in Section 4). These values are not tuned to any specific vehicle; they are chosen to be representative of large survey-class AUVs and their docking hardware and to provide realistic scales for sensor rates, noise levels, and acoustic delay. The representative specifications of the AUV, the MDS, and the onboard/acoustic sensors used in the simulations are summarized in Table 1.

**Table 1.** Representative AUV, MDS, and sensor specifications used in simulation.

| Subsystem            | Parameter                  | Representative Value/Description                                                                                       |
|----------------------|----------------------------|------------------------------------------------------------------------------------------------------------------------|
| AUV hull             | Length, diameter, dry mass | 5.5 m; 0.9 m; 1.8 t                                                                                                    |
|                      | Max depth, cruise speed    | 6000 m; 1.5 m/s ( $\approx 3$ kn)                                                                                      |
| AUV sensors          | IMU                        | Tactical-grade, 10 Hz in simulations, tens of Hz in practice                                                           |
|                      | DVL                        | 300–600 kHz DVL, 5–10 Hz; velocity accuracy $\approx 0.2\text{--}0.4\%$ of distance traveled; bottom-lock range 0–80 m |
|                      | Depth sensor               | Pressure sensor, 0.1% full-scale accuracy, 10–50 Hz                                                                    |
| MDS structure        | Frame                      | Square lattice frame, $4\text{ m} \times 4\text{ m} \times 4\text{ m}$ , mounted on seabed or a low-speed carrier      |
|                      | Docking port               | Funnel-type tube, entrance diameter 1.5 m, length 3 m; aligned with AUV longitudinal axis                              |
| MDS sensors and link | Acoustic positioning       | USBL-like range/bearing sensor integrated with the docking frame, working range 1–3 km                                 |
|                      | Acoustic modem             | 20–30 kHz band, data rate 1–10 kbit/s, half-duplex                                                                     |
|                      | Delay model                | One-way propagation $\approx 0.7\text{ s/km}$ plus MAC/processing;                                                     |

In a typical mission profile, docking is therefore organized in two regimes. Outside a few tens of meters, only inertial and delayed acoustic information are reliably available, and the estimator described in this paper is responsible for keeping the AUV–MDS relative state within a few meters in this “acoustic homing” corridor [18,50]. Once the vehicle has entered a small capture zone around the docking port and local water clarity permits, short-range optical aids (e.g., cameras and coded visual markers on the funnel) can be used to sharpen the final alignment [50]. The present work focuses on the former, delay-affected

acoustic-inertial regime and provides delay-robust, statistically consistent state estimates to hand over to such optical guidance in the last meters.

### 3.2. Frames and Transformations

Let  $W$  be the global inertial frame (approximately a level-plane inertial frame),  $A$  the AUV body frame, and  $B$  the MDS body frame. Let  $R_{WA} \in \text{SO}(3)$  and  $R_{WB} \in \text{SO}(3)$  denote the direction-cosine (rotation) matrices of  $A$  and  $B$  with respect to  $W$  (equivalently unit quaternions  $q_{WA}, q_{WB}$ ). Positions and velocities in  $W$  are  $\mathbf{p}_A^W, \mathbf{p}_B^W \in \mathbb{R}^3$  and  $\mathbf{v}_A^W, \mathbf{v}_B^W \in \mathbb{R}^3$ . Body-to-inertial vector transforms satisfy

$$x^W = R_{WA} x^A, \quad x^W = R_{WB} x^B. \quad (1)$$

If needed, fixed sensor extrinsics (e.g., IMU/DVL/transducer lever arms and orientations) are represented by rigid transforms  $T_{AX}, T_{BX}$ . We treat them as calibrated constants or include them as slowly drifting states when required.

### 3.3. Kinematic Models

For practicality and estimator consistency we adopt a “simplified 6-DoF rigid body and random-walk bias” continuous-discrete model.

#### (1) AUV dynamics (continuous time)

$$\dot{p}_A^W = v_A^W, \quad \dot{v}_A^W = g^W + R_{WA}(a_A^A - b_{a,A} - n_{a,A}), \quad \dot{q}_{WA} = \frac{1}{2}\Omega(\omega_A^A - b_{g,A} - n_{g,A})q_{WA} \quad (2)$$

where  $g^W$  is gravity,  $a_A^A, \omega_A^A$  are IMU accelerometer/gyroscope readings,  $b_{a,A}, b_{g,A}$  are biases,  $n_{a,A}, n_{g,A}$  are IMU noises, and  $\Omega(\cdot)$  is the quaternion kinematic operator. Biases follow random walks:  $\dot{b}_{a,A} = n_{ba}, \dot{b}_{g,A} = n_{bg}$ . The discrete form is

$$x_{A,k+1} = f_A(x_{A,k}, u_{A,k}) + w_{A,k}, \quad w_{A,k} \sim \mathcal{N}(0, Q_{A,k}). \quad (3)$$

#### (2) MDS dynamics

The MDS executes low-speed maneuvers with a smoother model:

$$\dot{p}_B^W = v_B^W, \quad \dot{v}_B^W = R_{WB}u_B^B + w_{v,B}, \quad \dot{q}_{WB} = \frac{1}{2}\Omega(\omega_B^B)q_{WB}, \quad (4)$$

where  $u_B^B$  is an equivalent thrust/actuation input (from velocity commands or a simplified maneuvering proxy) and  $w_{v,B}$  is process noise. The discrete form is

$$x_{B,k+1} = f_B(x_{B,k}, u_{B,k}) + w_{B,k}, \quad w_{B,k} \sim \mathcal{N}(0, Q_{B,k}). \quad (5)$$

We use different state vectors at two filtering levels:

- (1) DC-EKF (AUV-centric):  $x_A = [p_A^W, v_A^W, q_{WA}, b_{g,A}, b_{a,A}]^\top$ .
- (2) Co-Aug-EKF (collaborative):  $x_{\text{aug}} = [x_A, x_B, \delta_c]^\top$ , where  $\delta_c$  optionally includes small inter-frame alignment errors, clock offset, or slowly drifting extrinsics to enable closed-loop consistent estimation in a unified frame.

### 3.4. Measurement Models (With Delay)

- (1) AUV proprioceptive measurements

IMU outputs drive state propagation; DVL and depth are used for updates. A typical discrete model is

$$z_{\text{DVL},k} = R_{WA,k}^T v_{A,k}^W + v_{\text{DVL},k}, \quad z_{\text{depth},k} = e_3^T p_{A,k}^W + v_{\text{dep},k}, \quad (6)$$

where  $e_3 = [0, 0, 1]^T$ . Noises  $v_{\cdot,k}$  are zero-mean Gaussian; their covariances may vary slowly with conditions (e.g., bottom-lock quality), which we reflect later via time-varying  $R$ .

#### (2) MDS relative observations of the AUV

Using a USBL-like range/bearing model, let

$$\rho_k^B = R_{WB,k}^T (p_{A,k}^W - p_{B,k}^W) \quad (7)$$

be the relative vector in frame B. Then

$$z_{\text{rng},k} = \|\rho_k^B\| + v_r, \quad z_{\text{az},k} = \arctan2(\rho_y^B, \rho_x^B) + v_\alpha, \quad z_{\text{el},k} = \arctan\left(\frac{\rho_z^B}{\sqrt{(\rho_x^B)^2 + (\rho_y^B)^2}}\right) + v_\beta \quad (8)$$

An equivalent “range + unit-bearing vector” model can also be used. We only require that the observation function  $z_k = h(x_{A,k}, x_{B,k}) + v_k$  be continuously differentiable for first-order linearization.

#### (3) Delay and OOS model

Let a measurement be generated at time  $t_m$  and received at time  $t_k$ ; the delay is  $\Delta_k = t_k - t_m \ge 0$ . We assume  $\Delta_k$  is a nonnegative random variable with bounded support  $[0, \Delta_{\max}]$  whose statistics can be estimated online; in simulations we consider several bounded models (uniform, truncated normal, exponential-like, and a short-long mixture) to assess sensitivity to the delay distribution (see Section 4). OOS means measurements with  $t_m < t_{m'}$  may arrive in reverse order. For implementation, each measurement carries its timestamp and quality indicators (e.g., confidence, SNR proxy). A ring buffer over  $\{k - L, \dots, k\}$  covers  $\Delta_{\max}$ . AUV proprioceptive measurements are treated as local near-real-time (small delays may be neglected or explicitly modeled).

### 3.5. Mathematical Problem Statement

Given a prior  $x_0 \sim \mathcal{N}(\bar{x}_0, P_0)$ , input sequences  $\{u_{A,0:k-1}, u_{B,0:k-1}\}$ , and two classes of measurements:

- near-real-time AUV measurements  $\mathcal{Z}_{\text{AUV},0:k} = \{z_{\text{DVL}}, z_{\text{depth}}, \dots\}$ ;
- MDS relative measurements  $\mathcal{Z}_{\text{MDS},0:k} = \{(z_i, t_i)\}$  with physical timestamps  $t_i$  that may be delayed or OOS at receive time  $k$ , the goal at each  $k$  is to compute the posterior estimate  $\hat{x}_k$  with covariance  $P_k$  for either  $x_{A,k}$  (DC-EKF) or  $x_{\text{aug},k}$  (Co-Aug-EKF) by minimizing the conditional negative log-likelihood (MAP):

$$\hat{x}_{0:k} = \underset{x_{0:k}}{\operatorname{argmin}} \left\{ \|x_0 - \bar{x}_0\|_{P_0^{-1}}^2 + \sum_{j=0}^{k-1} \|x_{j+1} - f(x_j, u_j)\|_{Q_j^{-1}}^2 + \sum_{(z_i, t_i) \in \mathcal{Z}_{\text{AUV},0:k}} \|z_i - h_{\text{AUV}}(x_{t_i})\|_{R_{\text{AUV},i}^{-1}}^2 + \sum_{(z_i, t_i) \in \mathcal{Z}_{\text{MDS},0:k}} \|z_i - h_{\text{MDS}}(x_{t_i})\|_{R_{\text{MDS},i}^{-1}}^2 \right\}, \quad (9)$$

where  $\|e\|_{P^{-1}}^2 = e^T P^{-1} e$  and  $x_{t_i}$  is the state at the physical time  $t_i$ . Because  $\mathcal{Z}_{\text{MDS}}$  contains delayed/OOS data, substituting “current time” for  $t_i$  is inappropriate. We therefore implement a two-level mechanism:

- DC-EKF: Use the ring buffer to perform a consistency-preserving measurement update at  $t_i$ , then forward-replay the corrected  $[x_{t_i}, P_{t_i}]$  with cached inputs/noise to time  $k$ ;
- Co-Aug-EKF: In a unified frame, absorb bidirectional observations and relative kinematics with an augmented state to achieve closed-loop consistent estimation.

Additionally, we introduce a delay threshold  $\tau_{\text{th}}$  and a dynamic confidence weight  $w_i \in (0, 1]$ . Measurements with  $\Delta_i > \tau_{\text{th}}$  are softly down-weighted or discarded; for  $\Delta_i \le \tau_{\text{th}}$ , we adapt  $R_{\text{MDS},i}$  (or the equivalent information matrix) online according to innovation Mahalanobis distance/NIS and proxies for range/occlusion and link quality, so that fusion weights track information content.

### 3.6. Noise and Uncertainty Assumptions

Process noises  $w_{A,k}, w_{B,k}$  and measurement noise  $v_k$  are modeled as zero-mean Gaussian white sequences; IMU biases follow random walks. The process and measurement covariances  $Q_k, R_k$  are allowed to be time-varying (heteroscedastic). For acoustic observations,  $R$  typically depends on range, occlusion, and sea state; this variability is later encoded through the dynamic confidence weighting used in the DC-EKF and Co-Aug-EKF layers. Consistency control relies on Mahalanobis/chi-square gating and NIS/NEES monitoring, together with Joseph-form covariance updates and occasional spectral projection to maintain positive definiteness and numerical stability.

Although these assumptions follow the standard EKF practice and enable tractable consistency analysis, actual underwater acoustic channels can exhibit heavy tails, occasional outliers, and slowly drifting biases [10]. To assess the impact of such departures from the Gaussian hypothesis, Section 4 includes a dedicated robustness study in which the DC-EKF is run under Laplace, Gaussian-mixture, and biased-mixture acoustic noise models while still assuming Gaussian measurement noise in the station channel. The results show that moderate non-Gaussian behavior mainly causes a small, bounded inflation relative to the delay-free baseline rather than catastrophic degradation. Collecting the noise and uncertainty assumptions in this subsection provides a common basis for the algorithmic designs and consistency checks developed in Sections 4–6, and avoids repeating them when describing each filtering layer.

### 3.7. Summary of System Model

We have specified a common frame convention, simplified rigid-body dynamics for both platforms, the AUV/MDS observation relations, and an acoustic-link delay/OOS model. The estimation problem is cast as online MAP with timestamped measurements, highlighting two engineering constraints: (i) late measurements must be absorbed at their physical time to preserve consistency; and (ii) measurement quality is time-varying (heteroscedastic). Figure 1 summarizes how these elements are assembled into a single processing chain. Starting from onboard and MDS measurements, delayed/OOS acoustic observations are time-rectified via ring-buffer-based backward-forward replay, admitted according to a learned delay threshold, and fused with dynamic confidence weighting before entering the cooperative augmented EKF together with relative motion constraints. The next sections build on this pipeline in detail: Section 4 presents the DC-EKF, Section 5 elaborates delay threshold calibration and adaptive confidence weighting, and Section 6 introduces the Co-Aug-EKF for unified-frame, closed-loop estimation of both platforms' states.

![Flowchart of the cooperative estimation framework for AUV-MDS docking. The process starts with 'Onboard measurements (IMU, DVL, depth)' and 'MDS acoustic measurements'. Onboard measurements feed into 'AUV prediction (local EKF propagation)' and 'Quality features'. 'Quality features' and 'MDS acoustic measurements' feed into 'Consistency gating (NIS/NEES)'. 'AUV prediction' feeds into a 'Ring buffer'. 'Ring buffer' feeds into 'Backward update at measurement time'. 'Consistency gating' feeds into a decision diamond 'Delay threshold τ*'. If the delay is less than or equal to τ* (≤ τ*), the measurement is admitted and feeds into 'Backward update at measurement time'. If the delay is greater than τ* (> τ*), the measurement is 'Discard measurement'. 'Backward update at measurement time' feeds into 'Forward replay to current time', which then feeds into 'Current estimate'. 'Relative motion constraints' feed into 'Co-Aug-EKF' along with 'Current estimate'. 'Co-Aug-EKF' produces 'Docking-ready absolute' states.](cfda9df1319e04207eb28bcefd1dab7b_img.jpg)

Flowchart of the cooperative estimation framework for AUV-MDS docking. The process starts with 'Onboard measurements (IMU, DVL, depth)' and 'MDS acoustic measurements'. Onboard measurements feed into 'AUV prediction (local EKF propagation)' and 'Quality features'. 'Quality features' and 'MDS acoustic measurements' feed into 'Consistency gating (NIS/NEES)'. 'AUV prediction' feeds into a 'Ring buffer'. 'Ring buffer' feeds into 'Backward update at measurement time'. 'Consistency gating' feeds into a decision diamond 'Delay threshold τ\*'. If the delay is less than or equal to τ\* (≤ τ\*), the measurement is admitted and feeds into 'Backward update at measurement time'. If the delay is greater than τ\* (> τ\*), the measurement is 'Discard measurement'. 'Backward update at measurement time' feeds into 'Forward replay to current time', which then feeds into 'Current estimate'. 'Relative motion constraints' feed into 'Co-Aug-EKF' along with 'Current estimate'. 'Co-Aug-EKF' produces 'Docking-ready absolute' states.

**Figure 1.** Overall processing flow of proposed cooperative estimation framework for AUV-MDS docking. Onboard IMU/DVL/depth measurements drive an AUV-centric EKF and a ring buffer of time-stamped states. Delayed MDS acoustic measurements pass through consistency gating and a learned delay threshold  $\tau^*$ ; admitted measurements are assigned dynamic confidence weights and mapped to an equivalent covariance  $R_{\text{eff}}$ , then applied via a backward update at physical measurement time followed by forward replay to current time (DC-EKF). Time-rectified, adaptively weighted observations together with relative motion constraints feed the cooperative augmented EKF (Co-Aug-EKF), which produces docking-ready absolute and relative states in a unified frame.

## 4. Delay-Compensated EKF (DC-EKF)

Building on the system model, this chapter presents the real-time DC-EKF filtering framework for delayed and out-of-sequence (OOS) acoustic measurements, corresponding to the lower-level delay-compensation block in Figure 1. The key idea is to maintain a ring buffer that covers the maximum admissible delay, apply each late measurement at its original physical time to obtain a consistency-preserving update, and then forward-replay the corrected state and covariance to the current time. By avoiding the misuse of “past information” on the “current state,” the filter prevents time misalignment and estimator jumps, and it naturally accommodates link jitter and OOS arrivals.

We consider a discrete-time nonlinear system

$$x_{k+1} = f(x_k, u_k) + w_k, \quad z_k = h(x_k) + v_k \quad (10)$$

with  $w_k \sim \mathcal{N}(0, Q_k)$ ,  $v_k \sim \mathcal{N}(0, R_k)$ . A nominal EKF proceeds at each step with predict-update:

$$\hat{x}_{k|k-1} = f(\hat{x}_{k-1|k-1}, u_{k-1}) \quad (11)$$

$$P_{k|k-1} = F_{k-1} P_{k-1|k-1} F_{k-1}^T + Q_{k-1} \quad (12)$$

$$K_k = P_{k|k-1} H_k^T (H_k P_{k|k-1} H_k^T + R_k)^{-1} \quad (13)$$



$$\hat{x}_{k|k} = \hat{x}_{k|k-1} + K_k(z_k - h(\hat{x}_{k|k-1})) \quad (14)$$

$$P_{k|k} = (I - K_k H_k) P_{k|k-1} (I - K_k H_k)^T + K_k R_k K_k^T \quad (15)$$

where  $F_{k-1} = \partial f / \partial x|_{\hat{x}_{k-1|k-1}, u_{k-1}}$  and  $H_k = \partial h / \partial x|_{\hat{x}_{k|k-1}}$ . This flow implicitly assumes “measurement time = use time.” When an external observation generated at physical time  $t_i$  is received at step  $k$  with delay  $\Delta = k - t_i \ge 0$  (with  $t_i$  the discrete index associated with the timestamp), a direct update at time  $k$  yields innovation statistics and covariance evolution that are inconsistent, typically producing error spikes, NIS overruns, and even numerical instability. Therefore, a late measurement must be absorbed at  $t_i$  [11,47,48].

DC-EKF implements this with a ring buffer that explicitly carries a short history. The buffer spans the most recent  $L$  steps (set by the maximum admissible delay and the filter rate) and stores, for each step,  $\{\hat{x}_{j|j}, P_{j|j}\}$  together with the information needed to recompute propagation from  $j \to j+1$  (inputs, recomputable Jacobians, and process-noise terms). Upon receiving a timestamped external measurement, the filter locates its generation time  $t_i$  in the buffer. If  $t_i$  lies within the window, it performs a consistency-preserving update at  $t_i$  on  $\{\hat{x}_{t_i|t_i-1}, P_{t_i|t_i-1}\}$  (Joseph-form covariance with Mahalanobis gating to suppress outliers), yielding  $\{\hat{x}_{t_i|t_i}, P_{t_i|t_i}\}$ . It then re-applies the cached propagation operators in chronological order from  $t_i$  to  $k$ , refreshing  $\{\hat{x}_{j|j}, P_{j|j}\}$  along the way. If multiple late measurements fall within the same interval, they are processed in timestamp order to preserve causality. Extremely stale measurements falling outside the window are ignored to avoid disproportionate cost. The mechanism requires no prior assumption on delay statistics and is naturally robust to jitter and OOS [14,32,38].

From a cost and memory standpoint, let  $n$  be the state dimension. One late measurement incurs one update plus  $L' (\le L)$  re-propagations, for a cost of approximately  $\mathcal{O}(n^3) + \mathcal{O}(L'n^2)$ . The average overhead grows roughly linearly with the buffer length. In typical AUV–MDS missions, only a fraction of external observations trigger backward–forward replay; overall real-time performance remains tractable. Implementation stores  $\{\hat{x}_{j|j}, P_{j|j}\}$  and recomputable terms, without retaining full transition matrices, striking a practical balance between memory and numerical stability.

To assess the effect of DC-EKF, we simulated cooperative docking with both AUV proprioceptive measurements and MDS relative observations. External measurement delays vary randomly within a prescribed range and may arrive OOS. Baselines include: an ideal zero-delay “Standard EKF” that fuses onboard IMU and station measurements assuming instantaneous, delay-free arrival; a “no-compensation” scheme that applies delayed external observations at the current step; a “fixed-delay” scheme that assumes a known lag and aligns accordingly; and the proposed DC-EKF. Metrics include position RMSE, time evolution of the estimation error, and average per-step computation time; we also recorded statistics on how late measurements are handled. Experiment 1 uses a moderate delay range and a fixed update rate to illustrate typical behavior, followed by two sensitivity studies: one varying the maximum delay (Figure 2) and another examining the effect of different delay distributions while keeping  $\tau_{\max}$  fixed.

Figure 2 compares RMSE across delay regimes. As the delay bound increases, both “no-compensation” and “fixed-delay” exhibit monotonic error growth, reflecting the inherent risk of treating late data as current under strong jitter. DC-EKF maintains low error for low-to-moderate delays; as delays become large, errors rise but remain clearly below the uncompensated schemes. The trend indicates that as long as late observations fall within the buffer and can be absorbed consistently, backward–forward replay converts them into effective global constraints. As the delay bound increases beyond the buffer window, the marginal utility of additional delayed measurements diminishes; DC-EKF then degrades

gracefully toward the onboard-only dead-reckoning level, while still avoiding the sharp jump behavior seen in uncompensated methods.

![Figure 2: Performance vs. Communication Delay. A bar chart showing Mean position RMSE (m) for four fusion strategies across four delay ranges: 0-1 s, 0-3 s, 0-5 s, 0-7 s, and 0-10 s. The strategies are Standard EKF (blue), No Delay Comp (red), Fixed Delay (green), and DC-EKF (magenta).](42ff8b598a0818ca8b6ef30850ad5f4e_img.jpg)

| Delay Range | Standard EKF | No Delay Comp | Fixed Delay | DC-EKF |
|-------------|--------------|---------------|-------------|--------|
| 0-1 s       | 0.82         | 4.85          | 5.87        | 1.12   |
| 0-3 s       | 0.83         | 11.88         | 13.09       | 1.29   |
| 0-5 s       | 0.83         | 21.61         | 23.24       | 1.29   |
| 0-7 s       | 0.79         | 22.91         | 26.51       | 15.95  |
| 0-10 s      | 0.83         | 38.36         | 42.53       | 20.46  |

Figure 2: Performance vs. Communication Delay. A bar chart showing Mean position RMSE (m) for four fusion strategies across four delay ranges: 0-1 s, 0-3 s, 0-5 s, 0-7 s, and 0-10 s. The strategies are Standard EKF (blue), No Delay Comp (red), Fixed Delay (green), and DC-EKF (magenta).

**Figure 2.** Mean position RMSE (m) of four fusion strategies under increasing acoustic-link delay ranges (0–1 s ... 0–10 s). Delay ranges denote support of a uniformly distributed delay applied to station measurements; onboard sensors are taken as near real-time. Standard EKF fuses onboard IMU and station measurements under an ideal zero-delay assumption and serves as a delay-free reference; No Delay Comp fuses delayed station data at current step; Fixed Delay aligns measurements with a constant lag; DC-EKF performs a backward update at measurement’s physical time followed by forward replay. Values atop bars indicate averaged RMSE across repeated trials (error bars omitted for clarity). DC-EKF preserves near-baseline accuracy at small–moderate delays and avoids the rapid error growth of the two naïve schemes; under very large delays it degrades but remains better than no-compensation and fixed-delay baselines.

Figure 3 shows representative time histories of the estimation error. Uncompensated methods display clustered spikes when bursts of late observations arrive, whereas DC-EKF tracks the delay-free Standard-EKF baseline closely and is markedly smoother. Immediately after late data are received, the backward update and forward replay take effect and the error decays rapidly over the next few steps, evidencing the restoration of temporal consistency. This time-domain view corroborates the aggregate statistics in Figure 2.

![Figure 3: Position Error Over Time. A line plot showing absolute position error (m) over a 100 s run for four fusion strategies. The strategies are Standard EKF (solid blue line), No Delay Comp (dashed red line), Fixed Delay (dashed green line), and DC-EKF (dashed magenta line). The legend also includes RMSE values for each strategy.](dd330f8b8f6c16eae20c3a676b4eb804_img.jpg)

| Strategy      | Line Style     | RMSE (m) |
|---------------|----------------|----------|
| Standard EKF  | Solid Blue     | 0.829    |
| No Delay Comp | Dashed Red     | 23.441   |
| Fixed Delay   | Dashed Green   | 26.434   |
| DC-EKF        | Dashed Magenta | 1.353    |

Figure 3: Position Error Over Time. A line plot showing absolute position error (m) over a 100 s run for four fusion strategies. The strategies are Standard EKF (solid blue line), No Delay Comp (dashed red line), Fixed Delay (dashed green line), and DC-EKF (dashed magenta line). The legend also includes RMSE values for each strategy.

**Figure 3.** Absolute position error (m) over a 100 s run for four fusion strategies: Standard EKF (ideal zero-delay fusion of onboard IMU and station measurements), No Delay Compensation (delayed observations fused at current step), Fixed Delay (constant-lag alignment), and DC-EKF (backward update at observation time followed by forward replay). See legend for RMSE values.

Figure 4 summarizes overall RMSE for the four methods in the same scenario. Relative to uncompensated schemes, DC-EKF markedly reduces error amplification caused by time misalignment; relative to the delay-free Standard-EKF baseline, it retains comparable error levels under moderate delays while avoiding estimator jumps. Runtime counters indicate that under moderate delays only a small portion of external observations trigger replay, with most being absorbed “in place.” As the maximum delay grows, the trigger ratio increases; a few extreme-delay or gated-out cases are rejected, yet the overall error profile remains stable.

![Figure 4: RMSE Comparison bar chart. The chart shows Mean position RMSE (m) for four fusion strategies: Standard EKF (0.829 m), No Delay Comp (23.441 m, +2727.8% increase), Fixed Delay (26.434 m, +3088.9% increase), and DC-EKF (1.353 m, +63.2% increase).](98ee20ceb85cd84e2415b20b1eda1bcf_img.jpg)

| Method        | RMSE (m) | Percentage Increase (vs Standard EKF) |
|---------------|----------|---------------------------------------|
| Standard EKF  | 0.829    | -                                     |
| No Delay Comp | 23.441   | +2727.8%                              |
| Fixed Delay   | 26.434   | +3088.9%                              |
| DC-EKF        | 1.353    | +63.2%                                |

Figure 4: RMSE Comparison bar chart. The chart shows Mean position RMSE (m) for four fusion strategies: Standard EKF (0.829 m), No Delay Comp (23.441 m, +2727.8% increase), Fixed Delay (26.434 m, +3088.9% increase), and DC-EKF (1.353 m, +63.2% increase).

**Figure 4.** Mean position RMSE (m) for four fusion strategies in same scenario as Figure 3. Standard EKF fuses onboard IMU and station measurements under an ideal zero-delay assumption; No-Delay-Comp fuses delayed station data at current step; Fixed-Delay aligns with a constant lag; DC-EKF performs a backward update at observation time followed by forward replay. Numbers atop bars are RMSE; percentages indicate increase relative to Standard-EKF baseline (0.829 m).

Figure 5 reports average per-step computation time. Compared with schemes that do not replay, DC-EKF increases runtime only modestly, with growth roughly linear in buffer length, matching the complexity analysis. Thus, introducing a ring buffer and backward-forward replay does not impose prohibitive overhead for online deployment; window length and step rate can be tuned to preserve margin.

![Figure 5: Computational Efficiency bar chart. The chart shows Average Computation Time (ms) for four fusion strategies: Standard EKF (0.028 ms), No Delay Comp (0.026 ms), Fixed Delay (0.026 ms), and DC-EKF (0.034 ms).](8b79f5ec940d107c246612c2a2ec519f_img.jpg)

| Method        | Average Computation Time (ms) |
|---------------|-------------------------------|
| Standard EKF  | 0.028                         |
| No Delay Comp | 0.026                         |
| Fixed Delay   | 0.026                         |
| DC-EKF        | 0.034                         |

Figure 5: Computational Efficiency bar chart. The chart shows Average Computation Time (ms) for four fusion strategies: Standard EKF (0.028 ms), No Delay Comp (0.026 ms), Fixed Delay (0.026 ms), and DC-EKF (0.034 ms).

**Figure 5.** Average per-step runtime (ms) measured in same scenario and hardware as Figures 3 and 4. Standard EKF fuses onboard IMU and station measurements under an ideal zero-delay assumption; No-Delay-Comp fuses delayed observations at current step; Fixed-Delay aligns with a constant lag; DC-EKF performs a backward update at observation time followed by forward replay. Numbers atop bars denote mean per-step time.

To further examine how strongly the estimator depends on the delay statistics themselves, we conducted an additional sensitivity study in which the maximum delay was fixed while the shape of the delay distribution was varied. Specifically, with  $\tau_{\max} = 5$  s

we considered four bounded models for the acoustic delay  $\tau$ : a uniform law, a truncated normal law, an exponential-like law favoring small delays, and a bimodal mixture of short and long delays. All other simulation settings (trajectory, noise levels, sensor rates) were kept identical to those in Experiment 1, and for each case thirty Monte Carlo runs were performed with a fixed random seed to ensure reproducibility.

Figure 6 reports the resulting position RMSE for all four fusion strategies. The naïve schemes (“No Delay Comp” and “Fixed Delay”) degrade to roughly 19–24 m RMSE and exhibit noticeable variation across delay models, confirming their sensitivity to how late data are injected as if current. By contrast, the proposed DC-EKF maintains a very similar error level around 1.3 m for all four distributions: the average RMSE is  $1.31 \pm 0.04$  m (uniform),  $1.32 \pm 0.05$  m (truncated normal),  $1.27 \pm 0.05$  m (exponential-like), and  $1.32 \pm 0.04$  m (mixture), corresponding to less than about 4% relative variation across models. At the same time DC-EKF remains close to the delay-free Standard-EKF baseline and more than one order of magnitude better than the naïve delayed-fusion schemes. These results indicate that, as long as the delay is bounded by the buffer horizon, performance depends mainly on the delay bound rather than on the exact delay distribution, and the uniform-delay model used in other experiments serves primarily as a convenient bounded stress test rather than a critical assumption.

![Bar chart titled 'RMSE vs. Delay Distribution (tau_max=5.0 s, 30 runs)'. The y-axis is 'Position RMSE (m)' ranging from 0 to 25. The x-axis shows four delay distributions: Uniform, Trunc-Normal, Exp-like, and Mixture. For each distribution, four bars represent: Standard EKF (blue), No Delay Comp (red), Fixed Delay (green), and DC-EKF (magenta). Error bars indicate one standard deviation. The DC-EKF bars are consistently the lowest, around 1.3 m, while the No Delay Comp and Fixed Delay bars are significantly higher, around 19-24 m.](411fa16c3211377525ba37c57784fee0_img.jpg)

| Delay Distribution | Standard EKF | No Delay Comp | Fixed Delay | DC-EKF          |
|--------------------|--------------|---------------|-------------|-----------------|
| Uniform            | ~0.5         | ~19.8         | ~22.0       | $1.31 \pm 0.04$ |
| Trunc-Normal       | ~0.5         | ~19.0         | ~21.0       | $1.32 \pm 0.05$ |
| Exp-like           | ~0.5         | ~18.8         | ~22.5       | $1.27 \pm 0.04$ |
| Mixture            | ~0.5         | ~21.5         | ~24.0       | $1.32 \pm 0.04$ |

Bar chart titled 'RMSE vs. Delay Distribution (tau\_max=5.0 s, 30 runs)'. The y-axis is 'Position RMSE (m)' ranging from 0 to 25. The x-axis shows four delay distributions: Uniform, Trunc-Normal, Exp-like, and Mixture. For each distribution, four bars represent: Standard EKF (blue), No Delay Comp (red), Fixed Delay (green), and DC-EKF (magenta). Error bars indicate one standard deviation. The DC-EKF bars are consistently the lowest, around 1.3 m, while the No Delay Comp and Fixed Delay bars are significantly higher, around 19-24 m.

**Figure 6.** Mean position RMSE (m) for four fusion strategies under different acoustic-delay distributions with fixed maximum delay  $\tau_{\max} = 5$  s (30 Monte Carlo runs per case). Delay distributions include a uniform law (Uniform), a truncated normal law (Trunc-Normal), an exponential-like law favoring small delays (Exp-like), and a bimodal mixture of short and long delays (Mixture). Bars show the average RMSE and error bars indicate one standard deviation. Standard EKF fuses onboard IMU and station measurements under an ideal zero-delay assumption; No-Delay-Comp fuses delayed station data at current step; Fixed-Delay aligns measurements with a constant lag; DC-EKF performs a backward update at observation time followed by forward replay. DC-EKF remains close to Standard-EKF baseline and exhibits less than about 4% RMSE variation across all delay models, whereas naïve schemes are an order of magnitude worse and more sensitive to distribution shape.

To further examine how strongly the proposed estimator depends on the Gaussian-noise assumption in Section 3.6, we conducted an additional robustness study in which the acoustic measurement noise was deliberately made non-Gaussian while the filter still assumed a zero-mean Gaussian model for design and tuning. All other settings (trajectory,

sensor rates, delay range  $\tau \in [0, 5]$  s) were kept identical to Experiment 1. Four noise models were considered for the station/MDS channel:

- Gaussian: The baseline zero-mean Gaussian noise with covariance  $R_{\text{station}}$ .
- Laplace (heavy-tailed): A zero-mean Laplace distribution with a scale parameter chosen so that its variance matches that of the Gaussian case, producing heavier tails but the same nominal second moment.
- Gaussian mixture (outliers): A mixture model in which, with probability 0.95, measurements are drawn from  $\mathcal{N}(0, R_{\text{station}})$  and, with probability 0.05, from  $\mathcal{N}(0, 25R_{\text{station}})$ , mimicking occasional large outliers.
- Biased mixture (slow drift + outliers): A slowly time-varying bias, modeled as a low-bandwidth random walk, is added to the Gaussian-mixture noise in (iii), emulating calibration errors or environmental shifts that introduce systematic offsets in addition to outliers.

For each noise model, twenty Monte Carlo runs over a 100 s docking segment were performed and the position RMSE was computed for the four fusion strategies. Figure 7 summarizes the results. As expected, the delay-free Standard EKF, which fuses onboard IMU and station measurements under an ideal zero-delay assumption, delivers the lowest RMSE ( $\approx 0.82\text{--}0.85$  m) and serves as a best-case reference. The naïve delayed-fusion schemes (No-Delay-Comp and Fixed-Delay) remain in the  $\approx 20\text{--}24$  m range for all four noise models with standard deviations of 2–4 m, confirming that their dominant failure mode is temporal inconsistency rather than the exact noise distribution. By contrast, the proposed DC-EKF stays much closer to the Standard-EKF bound and is remarkably insensitive to the noise model: its RMSE lies between 1.31 m and 1.33 m across all four cases, with less than about 5% relative variation even in the biased-mixture scenario. These results indicate that, under bounded delays and with the proposed gating and confidence-weighting mechanisms, overall performance is governed primarily by how delayed measurements are time-rectified, while moderate deviations from the Gaussian noise assumption mainly cause a small, bounded inflation relative to the ideal zero-delay baseline [20,49].

For reproducibility, Algorithm 1 summarizes the ring-buffer update and backward-forward replay: a delayed measurement is first located in the buffer, then applied at its physical timestamp using a Joseph-form update and NEES/NIS gating, and the corrected state/covariance are replayed forward to the current time using cached inputs.

#### --- **Algorithm 1:** Ring-buffer-based DC-EKF update for delayed/OOS measurements ---

##### **Inputs:**

- Ring buffer B storing entries  $(t_i, \hat{x}_i, P_i, u_i)$  for  $i = k - N_{\text{buf}} + 1, \dots, k$
- New measurement  $z$  with physical timestamp  $t_m$  and covariance  $R$
- Sampling interval  $\Delta t$ , maximum admissible delay  $\tau_{\text{max}}$ ,  $\chi^2$ -gating threshold

##### **Outputs:**

- updated current state  $\hat{x}_k, P_k$
  - Compute the delay  $\tau = t_k - t_m$
  - if  $\tau > \tau_{\text{max}}$  then
  - discard  $z$  (too old), return  $\hat{x}_k, P_k$
  - end if
-

#### --- **Algorithm 1 Cont.** ---

5. Find index  $j$  in  $B$  such that  $t_j \le t_m < t_{j+1}$
  6. Take  $(\hat{x}_j, P_j)$  from  $B$  and form innovation
  7.  $y = z - h(\hat{x}_j), S = HP_j H^T + R$
  8. if  $y^T S^{-1} y > \chi^2_{\text{gate}}$  then
  9. reject  $z$  (NIS/NEES outlier), return  $\hat{x}_k, P_k$
  10. end if
  11. Compute Kalman gain  $K = P_j H^T S^{-1}$
  12. Joseph-form update at time  $t_j$
  13.  $\hat{x}_j^+ = \hat{x}_j + K y$
  14.  $P_j^+ = (I - KH) P_j (I - KH)^T + KR K^T$
  15. Replace  $(\hat{x}_j, P_j)$  in  $B$  by  $(\hat{x}_j^+, P_j^+)$
  16. for  $i = j + 1, \dots, k$  do // forward replay
  17. Propagate  $(\hat{x}_{i-1}^+, \hat{P}_{i-1}^+) \to (\hat{x}_i, P_i)$  according to the process model in Section 3  
using the cached input  $u_{i-1}$
  18. Update entry  $(t_i, \hat{x}_i, P_i, u_i)$  in  $B$
  19. end for
  20. return  $\hat{x}_k, P_k$
- 

In summary, DC-EKF updates at the measurement's physical time and replays forward along the timeline, systematically repairing the consistency violations caused by delayed and OOS acoustic observations. It standardizes the absorption of late information and suppresses estimator jumps. Under moderate delays the method decisively outperforms uncompensated baselines without sacrificing real-time performance; under larger delays it still maintains a clear advantage and yields smoother error trajectories that better support subsequent pose and trajectory alignment. Compared with a delay-free baseline that simply assumes instantaneous access to all measurements (Standard EKF), DC-EKF explicitly handles late information from the MDS and turns it into usable constraints under realistic delayed-link conditions, providing more consistent state inputs at terminal docking. Together, Figures 2–7 and the runtime statistics form a coherent body of evidence: the figures capture delay-dependent trends, the effect of different delay distributions, and time-domain behavior, while the counters show that replay triggers and computational load remain within engineering limits. The next chapter introduces adaptive weighting and threshold calibration to further improve robustness and information efficiency under fluctuating link quality.

![Bar chart titled 'Robustness to Non-Gaussian Acoustic Noise (delay 0-5 s)'. The y-axis is 'Position RMSE (m)' from 0 to 25. The x-axis shows four noise models: Gaussian, Laplace (heavy-tailed), Gaussian mixture (outliers), and Biased mixture (slow drift + outliers). For each model, four fusion strategies are compared: Standard EKF (blue), No Delay Comp (red), Fixed Delay (green), and DC-EKF (magenta). DC-EKF consistently shows the lowest RMSE across all models, while the other three methods show significantly higher RMSE values.](f4d72193f77f6646a2a1f4baaa927154_img.jpg)

| Noise Model                            | Standard EKF | No Delay Comp | Fixed Delay | DC-EKF |
|----------------------------------------|--------------|---------------|-------------|--------|
| Gaussian                               | 0.82         | 20.99         | 23.52       | 1.32   |
| Laplace (heavy-tailed)                 | 0.82         | 19.66         | 21.67       | 1.33   |
| Gaussian mixture (outliers)            | 0.84         | 19.97         | 22.22       | 1.31   |
| Biased mixture (slow drift + outliers) | 0.84         | 21.91         | 24.12       | 1.32   |

Bar chart titled 'Robustness to Non-Gaussian Acoustic Noise (delay 0-5 s)'. The y-axis is 'Position RMSE (m)' from 0 to 25. The x-axis shows four noise models: Gaussian, Laplace (heavy-tailed), Gaussian mixture (outliers), and Biased mixture (slow drift + outliers). For each model, four fusion strategies are compared: Standard EKF (blue), No Delay Comp (red), Fixed Delay (green), and DC-EKF (magenta). DC-EKF consistently shows the lowest RMSE across all models, while the other three methods show significantly higher RMSE values.

**Figure 7.** Mean position RMSE (m) for four fusion strategies under different acoustic-noise models with a fixed uniform delay range  $\tau \in [0, 5]$  s. Acoustic-noise models include Gaussian noise (Gaussian), a zero-mean Laplace law with matched variance (Laplace, heavy-tailed), a Gaussian mixture with 5% high-variance outliers (Gaussian mixture, outliers), and a biased mixture with a slowly drifting bias term plus the Gaussian mixture (Biased mixture, slow drift + outliers). Standard EKF fuses onboard IMU and station measurements under an ideal zero-delay assumption; No-Delay-Comp fuses delayed station data at the current step; Fixed-Delay aligns measurements using a constant lag; DC-EKF performs a backward update at the measurement's physical time followed by forward replay. DC-EKF stays close to the delay-free baseline ( $\approx 1.3$  m vs. 0.82–0.85 m) and exhibits little variation across noise models, whereas the naive schemes degrade to  $\approx 20$ –24 m RMSE regardless of the noise distribution.

# 5. Adaptive Confidence Weighting and Threshold Calibration

The DC-EKF of the previous chapter guarantees temporal consistency by absorbing delayed or out-of-sequence (OOS) measurements at their physical time and replaying forward. Under a low-rate, high-latency acoustic link, however, consistency alone does not ensure fusion quality: measurement reliability varies markedly across sources and over time (e.g., MDS observations fluctuate with range/SNR/occlusion, while IMU-only propagation drifts with time) [1,3,9,10]. Fixed covariances or static gating can therefore decouple fusion weights from actual information quality [20,24,33]. This chapter wraps the DC-EKF with two mechanisms—delay threshold calibration and adaptive confidence weighting—so that both admission to the backward-forward update and the impact of an admitted measurement match its effective information content.

## 5.1. Learning and Interpreting a Delay Threshold

We quantify the “effective information” of a late measurement with delay  $\Delta$  as

$$\mathcal{I}_{\text{eff}}(\Delta) = \|K(\Delta)\| \exp(-\Delta/\tau) \quad (16)$$

where  $K(\Delta)$  is the Kalman gain computed using the prior covariance propagated by  $\Delta$ , and  $\tau$  is a time-decay constant. For reproducibility, the resulting online calibration of the delay threshold  $\tau_{\text{th}}$  based on this effective-information metric and batches of NEES-filtered delay samples is summarized in Algorithm 2.

#### **Algorithm 2:** Online calibration of delay threshold $\tau_{th}$

##### **Inputs:**

1. Initial delay threshold  $\tau_{th}$  (e.g.,  $\tau_{th} = \tau_{max}$ )
2. Batch size  $N_{batch}$  (e.g., 10) and smoothing factor  $\alpha \in (0, 1)$

##### **Outputs:**

1. buffer  $D$  of accepted delay samples

Upon each admitted station measurement  $z$  at receive time  $t_k$ :

1. Compute delay  $\tau = t_k - t_m$  ( $t_m$  is the physical generation time carried in the packet)
2. Apply DC-EKF gating (NEES/NIS); if the measurement is rejected, return
3. Compute effective information  $I_{eff}(\tau)$  using  $(\cdot)$  in Section 5.1
4. if  $I_{eff}(\tau) < I_{min}$  then // below minimum useful gain
5.     Return
6. end if
7. Append  $\tau$  to  $D$
8. if  $|D| = N_{batch}$  then
9.     Compute empirical 95th percentile  $\tau_{95}$  of  $D$
10.     Update delay threshold

$$\tau_{th} \leftarrow (1 - \alpha) \cdot \tau_{th} + \alpha \cdot \tau_{95}$$

11. Clear  $D$

12. end if

Use of  $\tau_{th}$  during operation:

13. For a new station measurement with delay  $\tau$ ,

if  $\tau \le \tau_{th}$ : admit it to the ring-buffer/DC-EKF pipeline with nominal covariance  $R$

if  $\tau > \tau_{th}$ : either discard it, or inflate  $R$  by a factor  $\gamma(\tau) > 1$  according to your dynamic confidence weighting

The definition encodes two facts: (i) as  $\Delta$  grows, the prior typically inflates so the nominal gain  $\|K\|$  can increase; (ii) information that arrives too late loses closed-loop value, hence the exponential penalty. Together with NEES/NIS consistency checks, we learn the delay gate  $\tau_{th}$  online from accepted samples only—those with (i) NEES below the  $\chi^2$  percentile and (ii)  $\mathcal{I}_{eff}$  above a minimal information threshold [20,24,33]. We then set  $\tau_{th}$  to the 95th percentile of the empirical delay distribution and update it in fixed batches (10 accepted samples per update) to avoid jitter. Operationally, this finds the knee of the benefit-cost curve: beyond the knee, marginal information decays rapidly per unit delay.

Figure 8a–d summarizes the online statistics during threshold learning. Panel (a) shows that the nominal gain  $\|K\|$  does not necessarily decrease with  $\Delta$ , so it overvalues late data if used alone. Panel (b), using absolute covariance reduction, still exhibits an apparent increase with  $\Delta$  due to prior inflation. By contrast, panel (d) shows the effective information decreasing monotonically with  $\Delta$ , with a clear knee near 6–7 s. Panel (c) indicates that most NEES samples lie below the  $\chi^2$  95th-percentile for 3 DoF, validating linearization/noise settings and supplying a usable sample pool. In our implementation, three thresholding methods yield 8.65 s (adaptive percentile), 9.99 s (fixed-gain criterion), and 7.01 s (benefit-cost). On mission-like data the threshold converges to 6.35 s (red dashed line in Figure 8c), aligned with the knee of  $\mathcal{I}_{eff}$ . Thus, about 6.4 s is a reasonable divider between “still valuable in closed loop” and “benefit insufficient to offset latency cost” for this scenario.

![Figure 8: Delay Threshold Calibration Analysis. Four subplots (a, b, c, d) showing relationships between acoustic measurement delay (0-10s) and four per-sample statistics. (a) Information Gain vs Delay: Information Gain (0.00-2.00) vs Delay (s). A red dashed line at y=0.01 (Min threshold) and a green dashed line at x=7.01s (Adaptive threshold). (b) Covariance Improvement vs Delay: Covariance Improvement (16-28) vs Delay (s). (c) Normalized Estimation Error Squared: NEES (0-8) vs Delay (s). A red dashed line at y=7.81 (NEES threshold). (d) Effective Information Gain (with decay): Effective Gain (0.2-1.6) vs Delay (s). A green dashed line at x=7.01s (Threshold). All plots show blue dots for individual samples.](7bed2d7c96d86bf922295a1252da52a5_img.jpg)

Figure 8: Delay Threshold Calibration Analysis. Four subplots (a, b, c, d) showing relationships between acoustic measurement delay (0-10s) and four per-sample statistics. (a) Information Gain vs Delay: Information Gain (0.00-2.00) vs Delay (s). A red dashed line at y=0.01 (Min threshold) and a green dashed line at x=7.01s (Adaptive threshold). (b) Covariance Improvement vs Delay: Covariance Improvement (16-28) vs Delay (s). (c) Normalized Estimation Error Squared: NEES (0-8) vs Delay (s). A red dashed line at y=7.81 (NEES threshold). (d) Effective Information Gain (with decay): Effective Gain (0.2-1.6) vs Delay (s). A green dashed line at x=7.01s (Threshold). All plots show blue dots for individual samples.

**Figure 8.** Relationships between acoustic measurement delay and four per-sample statistics used for learning the delay gate: (a) nominal information gain; (b) absolute covariance reduction; (c) NEES with a  $\chi^2_{0.95}(3) = 7.81$  gate (red dashed); (d) effective information gain after exponential time-decay. Dots denote individual samples. Vertical green dashed line marks learned delay threshold ( $\approx 7.01$  s); in (a), red dashed line shows minimum gain required for consideration. While (a–b) can appear flat or increasing with delay due to prior inflation during forward propagation, (d) decreases monotonically and exhibits a knee near 6–7 s, which we adopt for operating threshold.

Engineering-wise,  $\tau_{\text{th}}$  need not imply a hard reject. Measurements beyond the threshold may be discarded or softly down-weighted by inflating their covariance, e.g.,  $R$  to  $R/\lambda$  with  $\lambda \ll 1$ , to retain residual constraints under very sparse observations. Batch updates and percentile smoothing prevent thrashing; because NEES filtering precedes learning, outliers do not bias  $\tau_{\text{th}}$  upward [20,24,32].

## 5.2. Dynamic Confidence and Adaptive Weights

To keep fusion weights in step with information quality, we construct interpretable confidence scores for both IMU and MDS streams. On the IMU side, short- and long-window innovation norms estimate drift/noise level, combined with a mild time decay to reflect the intuitive degradation of pure inertial propagation. On the MDS side, confidence depends on delay (including jitter), SNR/occlusion proxies, and innovation consistency, mapped through sigmoid/exponential functions for numerical smoothness. After normalization, the two confidences produce weights that are then low-pass filtered (exponential smoothing) to avoid abrupt flips; lower/upper bounds (e.g., within  $[0.1, 0.9]$ ) prevent any single source from numerically dominating. In practice the weights also define adaptive measurement covariances

$$R_{\text{imu}} / (w_{\text{imu}} + 0.1), R_{\text{sta}} / (w_{\text{sta}} + 0.1)$$

implicitly tuning the Kalman gain via “noise scaling,” which is simple to implement and numerically stable [20,24,33].

Figure 9 shows the weight trajectories and fractions at three representative times. Early on, the IMU enjoys higher weight thanks to good short-term consistency; as drift accumulates, MDS SNR improves, and delays remain within the admissible range, the weight gradually shifts toward the station and stabilizes near IMU  $\approx 0.47$  and Station  $\approx 0.53$ . In the complete adaptive setting, this trend continues and the weights converge further to IMU  $\approx 0.16$  and Station  $\approx 0.84$ . This interpretable migration—IMU-dominant in the short term and station-calibrated in the long term—avoids the stage-dependent mismatch of fixed weights.

![Figure 9: Dynamic Weight Analysis. The top plot shows the time histories of normalized fusion weights for IMU (blue line) and Station/MDS (red line) over 100 seconds. The IMU weight starts high (~0.85) and gradually decreases, while the Station weight starts low (~0.2) and gradually increases, both stabilizing around 0.5. The bottom part shows three pie charts representing the weight fractions at three time instants: Start (t=0.0s) with IMU 53.4% and Station 46.6%; Middle (t=50.0s) with IMU 68.6% and Station 31.4%; and End (t=99.9s) with IMU 46.8% and Station 53.2%.](f85bf99d372e735d228361bf4d3cf7e6_img.jpg)

Figure 9: Dynamic Weight Analysis. The top plot shows the time histories of normalized fusion weights for IMU (blue line) and Station/MDS (red line) over 100 seconds. The IMU weight starts high (~0.85) and gradually decreases, while the Station weight starts low (~0.2) and gradually increases, both stabilizing around 0.5. The bottom part shows three pie charts representing the weight fractions at three time instants: Start (t=0.0s) with IMU 53.4% and Station 46.6%; Middle (t=50.0s) with IMU 68.6% and Station 31.4%; and End (t=99.9s) with IMU 46.8% and Station 53.2%.

**Figure 9.** Top: time histories of normalized fusion weights assigned to IMU (blue) and station/MDS observation channel (red) over a 100 s run. Bottom: Snapshot fractions at three representative instants ( $t = 0$  s, 50 s, 99.9 s). Weights are computed from innovation statistics together with delay and SNR proxies, smoothed in time, and applied via equivalent scaling of observation covariance.

## 5.3. Coupling with DC-EKF and Stability

The adaptive layer couples to DC-EKF along two paths: the delay threshold decides whether a station measurement enters the backward–forward replay at all, and the weights alter the effective  $R$ , thereby shaping the update gain both at the historical time and after replay to the present. Because a backward update can touch multiple historical frames, we use the Joseph form for covariance updates to preserve positive definiteness; in strongly nonlinear segments we add spectral projection/symmetrization to tame round-off errors [14,32,38]. For stability monitoring, we track the moving averages and exceedance rates of NIS/NEES; if exceedances rise within a short window, we temporarily inflate the affected channel’s covariance ceiling and increase the weight-smoothing factor to break the feedback loop of overconfidence  $\to$  large gain  $\to$  more exceedances  $\to$  further overconfidence [20,24,33].

## 5.4. Results and Discussion

Experiments use the same trajectories and noise settings as in Section 4: IMU at 10 Hz, MDS at 1 Hz; station delays  $\Delta \sim \mathcal{U}(0, 8\text{s})$  with randomized SNR proxies. The threshold is 

updated adaptively every 10 accepted samples, with  $\tau = 5$  s and weight smoothing factor  $\alpha = 0.9$ . Key outcomes appear in Figure 8.

Threshold learning (Figure 8) shows that effective information and NEES gating jointly confine a credible operating band for  $\tau_{\text{th}}$ . Online,  $\tau_{\text{th}}$  converges to 6.35 s (Figure 10, red dashed line), matching the benefit–cost knee. Across the dataset, 1067 station measurements are accepted and 30 rejected, indicating that the gate is neither overly strict nor permissive to stale data.

![Figure 10: Scatter plot titled 'Delay Distribution and Threshold'. The y-axis is 'Delay (s)' ranging from 0 to 8. The x-axis is 'Measurement Index' ranging from 0 to 100. Blue dots represent individual delayed measurement arrivals. A red dashed horizontal line marks the 'Final Threshold = 6.35s'. Points below the line are admitted to the pipeline; points above are hard-gated or softly down-weighted.](79cb7fa0e9c78ec5cd0b0de977824f8d_img.jpg)

Figure 10: Scatter plot titled 'Delay Distribution and Threshold'. The y-axis is 'Delay (s)' ranging from 0 to 8. The x-axis is 'Measurement Index' ranging from 0 to 100. Blue dots represent individual delayed measurement arrivals. A red dashed horizontal line marks the 'Final Threshold = 6.35s'. Points below the line are admitted to the pipeline; points above are hard-gated or softly down-weighted.

**Figure 10.** Scatter of per-measurement delays (s) versus arrival index for a representative run. Blue dots represent individual delayed measurement arrivals. Red dashed line marks final learned delay gate  $\tau_{\text{th}} = 6.35$  s, obtained from effective-information/NEES procedure in Figure 8. Points below line are admitted to backward-update/forward-replay pipeline; points above are hard-gated or softly down-weighted.

Dynamic weights (Figures 9 and 11) shift steadily toward the station as IMU drift becomes visible and link quality improves; in the full run the weights settle near IMU  $\approx 0.16$ , Station  $\approx 0.84$ . Through adaptive  $R$ , this translates into gains that let admitted station measurements act with strength commensurate to their quality. Relative to fixed- $R$ , adaptive weighting markedly lowers NIS/NEES exceedance rates and suppresses error spikes.

Performance-wise, Figure 12 shows a smooth error history with an overall position RMSE of 5.751 m over the 100 s docking segment; even during bursts of late arrivals the spikes typical of uncompensated schemes are absent. For the survey-class geometry in Section 3.1 (4 m frame with a 1.5 m-diameter docking funnel), this level of absolute error is sufficient to keep the vehicle inside the acoustic homing corridor and to bring it into the capture zone of the docking station. The subsequent Co-Aug-EKF layer further reduces the AUV-MDS relative-position RMSE to about 0.28 m (Section 6), and in practical systems the final few meters of approach can be refined by short-range optical aids on the docking port when local visibility allows [18,19,44,45]. Thus, the 5.751 m figure should be interpreted as the accuracy of the delay-robust acoustic-inertial homing stage rather than the ultimate mechanical capture accuracy. Together with Figure 13, the estimated trajectory adheres closely to ground truth near the docking corridor, without jumps that would result from applying late data at the current step.

![Figure 11: Dynamic Weight Evolution plot showing IMU Weight (blue) and Station Weight (red) over 100 seconds. The IMU weight starts at 0.45 and settles to approximately 0.16. The Station weight starts at 0.55 and settles to approximately 0.84.](9a19da4f7fccb96a934411c0bb5a386d_img.jpg)

Figure 11 is a line graph titled "Dynamic Weight Evolution". The y-axis is labeled "Weight" and ranges from 0.0 to 1.0. The x-axis is labeled "Time (s)" and ranges from 0 to 100. There are two data series: "IMU Weight" (blue line) and "Station Weight" (red line). The IMU Weight starts at approximately 0.45 at time 0, drops sharply to a minimum of about 0.12 around 10 seconds, and then settles to a steady-state value of approximately 0.16. The Station Weight starts at approximately 0.55 at time 0, rises sharply to a peak of about 0.88 around 10 seconds, and then settles to a steady-state value of approximately 0.84.

Figure 11: Dynamic Weight Evolution plot showing IMU Weight (blue) and Station Weight (red) over 100 seconds. The IMU weight starts at 0.45 and settles to approximately 0.16. The Station weight starts at 0.55 and settles to approximately 0.84.

**Figure 11.** Normalized fusion weights for IMU (blue) and station/MDS channel (red) during a 100 s run (same scenario as Figure 9). Weights are computed online from innovation statistics with delay/SNR proxies, smoothed in time, and applied via equivalent scaling of observation covariance ( $R$ ). By end of run they settle to approximately IMU  $\approx 0.16$  and Station  $\approx 0.84$ .

![Figure 12: Position Error Over Time plot showing absolute position error (m) over 100 seconds. The error fluctuates between 0 and 16 meters, with a red dashed line indicating an RMSE of 5.751m.](c4c8cd9c58f395c25a2a2b217ca7c2fb_img.jpg)

Figure 12 is a line graph titled "Position Error Over Time". The y-axis is labeled "Position Error (m)" and ranges from 0 to 16. The x-axis is labeled "Time (s)" and ranges from 0 to 100. A blue line represents the absolute position error, which fluctuates significantly between 0 and 16 meters throughout the 100-second run. A red dashed horizontal line is present at approximately 5.75 meters, labeled "RMSE=5.751m".

Figure 12: Position Error Over Time plot showing absolute position error (m) over 100 seconds. The error fluctuates between 0 and 16 meters, with a red dashed line indicating an RMSE of 5.751m.

**Figure 12.** Time history of absolute position error (m) over a 100 s run using DC-EKF with the learned delay gate and dynamic confidence weighting. Red dashed line marks run-level RMSE (5.751 m). Station observations are randomly delayed and may be out of sequence; onboard sensors are treated as near real-time.

![Figure 13: Trajectory Comparison. A line plot showing the overlay of the true path (black solid line) and the estimate from DC-EKF (red dashed line) with learned delay gate and dynamic confidence weighting. The x-axis is 'X Position (m)' ranging from 0 to 600, and the y-axis is 'Y Position (m)' ranging from -50 to 30. The plot shows a series of oscillating paths. The red dashed line closely follows the black solid line, indicating a smooth estimate without jump artifacts.](9b5411fa2d169b66f6185fbf67b49766_img.jpg)

Figure 13: Trajectory Comparison. A line plot showing the overlay of the true path (black solid line) and the estimate from DC-EKF (red dashed line) with learned delay gate and dynamic confidence weighting. The x-axis is 'X Position (m)' ranging from 0 to 600, and the y-axis is 'Y Position (m)' ranging from -50 to 30. The plot shows a series of oscillating paths. The red dashed line closely follows the black solid line, indicating a smooth estimate without jump artifacts.

**Figure 13.** Overlay of true path (black solid) and estimate from DC-EKF with learned delay gate and dynamic confidence weighting (red dashed). Station observations are delayed/jittered but time-aligned via backward-update/forward-replay. Estimated track follows ground-truth corridor smoothly without jump artifacts that arise when late data are applied at current step. Axes in meters.

Computationally, added cost stems mainly from per-sample gain/NEES/  $I_{\text{eff}}$  evaluation and batch updates of weights/thresholds. Because the threshold updates in batches and the weights rely on constant-time recursions, the overhead is well below that of backward-forward replay; in our setting the per-step latency is negligible and does not impair real-time operation.

## 5.5. Summary of Adaptive Delay-Threshold Learning and Weighting

Augmenting the DC-EKF with delay threshold calibration and adaptive confidence weighting restores alignment between fusion weights and information quality. The threshold is learned via a three-step procedure—effective information, NEES filtering, and percentile update—and converges to a value consistent with the benefit-cost knee (about 6.4 s in our case). The weights, driven by drift/noise/delay/SNR/consistency, migrate over time toward the station and materialize as adaptive  $R$  at the update level. In concert with backward-forward replay, the threshold decides admission and the weights decide influence. Experiments under strong delay and fluctuating quality show reduced error spikes, lower NEES exceedance, and improved overall RMSE without sacrificing real-time performance, thereby providing steadier, more credible external inputs for the downstream Co-Aug-EKF.

# 6. Cooperative Augmented EKF (Co-Aug-EKF)

The DC-EKF of the previous chapter absorbs delayed MDS measurements at their physical time via backward-forward replay and admits them with strength matched to information quality through delay thresholds and adaptive weights. Docking, however, is governed not only by each platform's absolute accuracy but, more critically, by their relative consistency in a common reference frame. If the AUV and the MDS estimate states independently, small individual errors can still yield a non-negligible relative offset, which amplifies into pose/trajectory misalignment near docking [7,8,15,41]. To address this, we build a centralized Co-Aug-EKF atop the DC-EKF outputs: in a unified frame it jointly models the AUV and MDS states, fuses bidirectional relative observations together with relative

kinematic constraints in a single loop, and explicitly maintains cross-platform covariances, thereby suppressing relative drift and improving closed-loop consistency [7,8,20,41].

## 6.1. Augmented State and Process Model

We define  $x_{\text{aug}} = [x_A^\top, x_B^\top, \delta_c^\top]^\top$ , where  $x_A$  and  $x_B$  contain the AUV/MDS pose, velocity, and any required slowly varying parameters (e.g., biases). The term  $\delta_c$  collects soft alignment states (small extrinsic/clock offsets or baseline alignment errors) and can be trimmed as needed. With a first-order approximation, the process model is block-structured:

$$x_{\text{aug},k+1} = \begin{bmatrix} f_A(x_{A,k}, u_{A,k}) \\ f_B(x_{B,k}, u_{B,k}) \\ \delta_c \end{bmatrix} + w_k, \quad F_k = \frac{\partial f}{\partial x} \approx \begin{bmatrix} F_{A,k} & 0 & * \\ 0 & F_{B,k} & * \\ 0 & 0 & I \end{bmatrix}, \quad (17)$$

where the “\*” blocks capture weak coupling effects and slow alignment drift; the process noise  $Q_k$  allows correlations within and across the two subblocks. In contrast to independent EKFs, the Co-Aug-EKF explicitly maintains the cross covariance  $P_{AB}$ . Consequently, any update on  $x_A$  or  $x_B$  propagates information across platforms through the cross terms, preventing the loss of correlation that otherwise breaks consistency and risks double-counting information [7,8,20].

## 6.2. Measurements and Bidirectional Relative Sensing

Measurements include each platform’s proprioceptive data and bidirectional relative observations. With a USBL-like range/bearing model, let  $\rho^W = p_A^W - p_B^W$  and  $\rho^B = R_{WB}^\top \rho^W$ . The MDS observation of the AUV is

$$z_{B \to A} = \begin{bmatrix} \|\rho^B\| \\ \text{atan2}(\rho_y^B, \rho_x^B) \\ \text{atan}(\rho_z^B / \sqrt{(\rho_x^B)^2 + (\rho_y^B)^2}) \end{bmatrix} + v_{B \to A}, \quad (18)$$

and  $z_{A \to B}$  has the same form with the roles reversed. Linearization yields Jacobians  $[H_A \ H_B \ H_c]$  with respect to  $(x_A, x_B, \delta_c)$ , so a single update acts on both platforms and the soft-alignment states. When opposite-direction observations are available within a short window, we perform cross-consistency checks: the redundant, geometrically complementary constraints on the same relative pose strengthen gating robustness and mitigate occasional gross errors from occlusion/blind spots. As in Section 5, DC-EKF-derived quality proxies (delay, SNR, innovation consistency) are mapped to time-varying measurement covariances so that each direction’s influence matches its effective information [20,24,33,39–41].

## 6.3. Relative Kinematic Constraints

To further limit relative drift and enforce closed-loop consistency at docking, we add a soft constraint derived from the two-body kinematics:

$$z_{\text{rel}} = \begin{bmatrix} p_A^W - p_B^W \\ v_A^W - v_B^W \end{bmatrix} - \begin{bmatrix} \hat{p}_A^W - \hat{p}_B^W \\ \hat{v}_A^W - \hat{v}_B^W \end{bmatrix} = 0 + v_{\text{rel}}, \quad (19)$$

This acts as a small-covariance pseudo-measurement that regularizes continuity of relative pose/velocity in the unified frame, “gluing” the two estimates in time. The covariance  $R_{\text{rel}}$  reflects confidence in this continuity and can be increased during aggressive relative maneuvers and decreased in gently varying phases. Analogous to relative factors in graph optimization, this constraint strengthens cross-platform coupling at low cost and

moves the engineering requirement of “relative consistency at docking” into the estimation layer [34,35].

## 6.4. Consistency and Numerical Stability

Centralization avoids the “information reuse” pitfall of distributed schemes, but linearization and numerical stability still require care [7,8,32]. We adopt the Joseph form for covariance updates and use symmetrization/spectral projection to maintain positive definiteness. When bidirectional observations arrive together, we process them in timestamp order to preserve causality. In strongly nonlinear segments, we linearize with smaller steps and monitor short-window NIS/NEES averages and exceedance rates; if exceedances rise, we temporarily inflate the affected channel’s covariance and increase weight smoothing to break the overconfidence → large gain → more exceedances feedback [20,24,32,33]. Because the DC-EKF has already time-rectified and down-weighted late measurements upstream, observations entering the Co-Aug-EKF are temporally consistent with more realistic covariances, reducing inconsistency at the source.

## 6.5. Experiments

In a 60 s scenario, initial positions are (0,0) and (20,15), with about 1140 total observations. The baseline (“independent EKFs”) runs separate filters for the AUV and the MDS and aligns results only at the end; the experimental group uses the Co-Aug-EKF.

Figure 14 shows 2-D trajectories: the Co-Aug-EKF tracks the truth closely near docking, and the two estimated trajectories exhibit better relative agreement in the unified frame.

![Figure 14: 2D Trajectories plot showing ground truth and state estimates for AUV and Station platforms. The plot displays X (m) on the horizontal axis (0 to 20) and Y (m) on the vertical axis (-2.5 to 17.5). The legend includes: AUV True (solid blue line), Station True (solid red line), AUV Co-Aug (dashed blue line), Station Co-Aug (dashed red line), AUV Ind (dotted blue line), and Station Ind (dotted red line). The trajectories show a main path from (0,0) to approximately (18,14) and a docking segment at the top right. The Co-Aug trajectories (dashed lines) closely follow the true trajectories (solid lines), while the independent trajectories (dotted lines) show more deviation and misalignment at the docking point.](a52ceaa1a0038c4e12cf866ad1ddd6bb_img.jpg)

Figure 14: 2D Trajectories plot showing ground truth and state estimates for AUV and Station platforms. The plot displays X (m) on the horizontal axis (0 to 20) and Y (m) on the vertical axis (-2.5 to 17.5). The legend includes: AUV True (solid blue line), Station True (solid red line), AUV Co-Aug (dashed blue line), Station Co-Aug (dashed red line), AUV Ind (dotted blue line), and Station Ind (dotted red line). The trajectories show a main path from (0,0) to approximately (18,14) and a docking segment at the top right. The Co-Aug trajectories (dashed lines) closely follow the true trajectories (solid lines), while the independent trajectories (dotted lines) show more deviation and misalignment at the docking point.

**Figure 14.** Overlay of ground truth and state estimates from the co-augmented EKF and independent EKFs for both platforms (AUV and station/MDS). The docking segment is shown at the right of the plot. The co-augmented EKF maintains tighter mutual alignment between the two estimated trajectories. Axes are in meters.

Figure 15 plots the position-error time histories of the AUV and the MDS. For most of the run, the Co-Aug-EKF envelopes lie below those of the baseline and contain fewer

isolated peaks. The resulting overall RMSEs are AUV 0.310 m (baseline 0.395 m, 21.5% improvement) and MDS 0.205 m (baseline 0.228 m, 10.1% improvement).

![Figure 15: Two line plots showing absolute position error (m) over a 60 s run. Plot (a) shows AUV Position Error with Co-Aug RMSE: 0.310m and Ind RMSE: 0.395m. Plot (b) shows Station Position Error with Co-Aug RMSE: 0.205m and Ind RMSE: 0.228m. Both plots compare Co-Augmented EKF (green solid line) and Independent EKF (orange dashed line).](c17eaf807acd5faec68da19dd16929be_img.jpg)

Figure 15 consists of two subplots, (a) and (b), showing the absolute position error (m) over a 60 s run. Both plots compare the Co-Augmented EKF (green solid line) and the Independent EKF (orange dashed line).  
 (a) AUV Position Error: The y-axis ranges from 0.0 to 1.0 m. The Co-Aug RMSE is 0.310m and the Ind RMSE is 0.395m. The error fluctuates between approximately 0.1m and 0.9m.  
 (b) Station Position Error: The y-axis ranges from 0.0 to 0.5 m. The Co-Aug RMSE is 0.205m and the Ind RMSE is 0.228m. The error fluctuates between approximately 0.05m and 0.45m.

Figure 15: Two line plots showing absolute position error (m) over a 60 s run. Plot (a) shows AUV Position Error with Co-Aug RMSE: 0.310m and Ind RMSE: 0.395m. Plot (b) shows Station Position Error with Co-Aug RMSE: 0.205m and Ind RMSE: 0.228m. Both plots compare Co-Augmented EKF (green solid line) and Independent EKF (orange dashed line).

**Figure 15.** Absolute position error (m) over a 60 s run in unified frame (same scenario as Figure 14): (a) AUV estimates from co-augmented EKF (green solid) and independent EKF (orange dashed), with run-level RMSE 0.310 m (Co-Aug) vs. 0.395 m (Ind.); (b) MDS estimates from co-augmented EKF (green solid) and independent EKF (orange dashed), with run-level RMSE 0.205 m (Co-Aug) vs. 0.228 m (Ind.).

More importantly, Figure 16 reports the relative-position error—the key docking metric—with RMSE 0.280 m for the Co-Aug-EKF versus 0.347 m for independent EKFs, indicating that relative drift is effectively suppressed by the unified frame plus relative constraints [7,8,15,18,41].

![Figure 16: A line plot titled 'Relative Position Error (Key for Docking)' showing the error (m) over a 60 s run. The plot compares Co-Augmented EKF (green solid line) and Independent EKF (orange dashed line). The Co-Aug RMSE is 0.280m and the Ind RMSE is 0.347m. The error fluctuates between approximately 0.0m and 0.9m.](62a4c9055642dbb00663e633332f04d3_img.jpg)

Figure 16 is a line plot titled 'Relative Position Error (Key for Docking)'. The y-axis is 'Relative Position Error (m)' ranging from 0.0 to 1.0. The x-axis is 'Time (s)' ranging from 0 to 60. The plot compares the Co-Augmented EKF (green solid line) and the Independent EKF (orange dashed line). The Co-Aug RMSE is 0.280m and the Ind RMSE is 0.347m. The error fluctuates between approximately 0.0m and 0.9m.

Figure 16: A line plot titled 'Relative Position Error (Key for Docking)' showing the error (m) over a 60 s run. The plot compares Co-Augmented EKF (green solid line) and Independent EKF (orange dashed line). The Co-Aug RMSE is 0.280m and the Ind RMSE is 0.347m. The error fluctuates between approximately 0.0m and 0.9m.

**Figure 16.** Time history over a 60 s run for co-augmented EKF (green solid) and independent EKF (orange dashed) in unified frame. Run-level RMSE: 0.280 m (Co-Aug) vs. 0.347 m (Ind.). Errors are computed from inter-platform relative pose; axes in meters.

Figure 17 presents error boxplots: the medians and interquartile ranges shift left, and outliers are markedly fewer, indicating not only better mean-square performance but also improved robustness.

![Figure 17: Boxplots comparing AUV and Station/MDS position error distributions for Co-Augmented and Independent EKF methods. The left plot, 'AUV Error Distribution', shows position error in meters for AUV. The right plot, 'Station Error Distribution', shows position error in meters for Station/MDS. In both cases, the Co-Augmented EKF (green box) has a lower median and narrower interquartile range compared to the Independent EKF (orange box), indicating improved accuracy and robustness. Outliers are shown as markers above the whiskers.](391ab9e5616ba6311161af4d7a93422b_img.jpg)

| Platform    | Method       | Median (m) | IQR (m) | Whiskers (m)   | Outliers (m)   |
|-------------|--------------|------------|---------|----------------|----------------|
| AUV         | Co-Augmented | ~0.22      | ~0.18   | ~0.00 to ~0.65 | ~0.65 to ~0.75 |
|             | Independent  | ~0.30      | ~0.15   | ~0.00 to ~0.85 | ~0.85 to ~1.00 |
| Station/MDS | Co-Augmented | ~0.15      | ~0.08   | ~0.00 to ~0.45 | ~0.45 to ~0.48 |
|             | Independent  | ~0.20      | ~0.10   | ~0.00 to ~0.50 | ~0.50 to ~0.55 |

Figure 17: Boxplots comparing AUV and Station/MDS position error distributions for Co-Augmented and Independent EKF methods. The left plot, 'AUV Error Distribution', shows position error in meters for AUV. The right plot, 'Station Error Distribution', shows position error in meters for Station/MDS. In both cases, the Co-Augmented EKF (green box) has a lower median and narrower interquartile range compared to the Independent EKF (orange box), indicating improved accuracy and robustness. Outliers are shown as markers above the whiskers.

**Figure 17. (Left)** AUV; **(right)** Station/MDS. Boxplots show median (line), interquartile range (box), whiskers ( $1.5 \times \text{IQR}$ ), and outliers (markers). Co-augmented EKF (green) vs. independent EKF (orange). Co-Aug case exhibits lower medians and narrower IQRs with fewer outliers, indicating improved mean-square accuracy and robustness. Axes in meters.

These outcomes follow from the information structure. Independent EKFs project the two-way relative measurements into separate frames and implicitly ignore cross correlation, breaking the information pathway. In the Co-Aug-EKF, any relative observation acts through  $[H_A \ H_B]$  on  $(x_A, x_B)$  and leaves a “shared memory” in  $P_{AB}$ . Subsequent proprioceptive updates on either platform then benefit the other via the cross terms, which sustains low relative drift over long horizons and avoids the paradox of “each looks accurate, but they disagree.” Numerically, the combination of bidirectional observations and relative constraints improves system observability and reduces ill-conditioning along weak directions, yielding a more balanced error spectrum under equal noise [34,35].

The magnitude of improvement depends on geometry and link conditions. When bidirectional observations are sparse, geometry is degenerate, or  $R_{\text{rel}}$  is set too large, the advantage diminishes. Conversely, when the MDS follows an FIM-guided path that improves geometry and maintains effective observation frequency, the gains of the augmented framework increase [7,35,41]. Centralization incurs additional computation and memory that scale with the size of the augmented state (in particular, maintaining the full cross covariance introduces a quadratic term in the state dimension), but in our setting these costs are still well below those of communication and backward-forward replay. By trimming  $\delta_c$  and tuning the soft-constraint strength, one obtains a practical accuracy-latency trade-off.

## 6.6. Summary of Co-Aug-EKF Relative-State Estimation

Without altering the upstream delay-robust machinery of the DC-EKF, the Co-Aug-EKF achieves closed-loop consistent estimation of both AUV and MDS through unified-state modeling, bidirectional fusion, and relative kinematic constraints. Compared with independent EKFs, it improves absolute accuracy (AUV/MDS RMSE gains of 21.5%/10.1%), relative accuracy ( $\approx 19\%$  reduction in relative-position RMSE), and robustness (narrower error distributions and fewer outliers). The result is a more consistent and credible state input for terminal docking, creating favorable conditions for subsequent attitude alignment and control convergence.

# 7. Conclusions

In ice-covered and otherwise challenging acoustic environments with strong latency, jitter, and intermittent availability, we addressed online state estimation for AUV-mobile docking station (MDS) cooperative docking and validated an engineering-ready solution

that balances temporal consistency with closed-loop consistency. The framework comprises: (i) a delay-compensated EKF (DC-EKF) built on a ring buffer with backward-forward replay; (ii) a quality-adaptive layer with learned delay thresholds and dynamic confidence weighting; and (iii) a cooperative augmented EKF (Co-Aug-EKF) that jointly estimates both platforms in a unified reference frame. The layers have clear roles and interfaces: the DC-EKF standardizes the absorption of delayed/OOS observations and preserves consistency; the adaptive layer decides admission and influence; and the Co-Aug-EKF achieves cross-platform closed-loop estimation and suppresses relative drift. Simulations show that, without sacrificing real-time performance, the framework significantly improves absolute and relative accuracy, estimator stability, and tolerance to adverse link conditions.

First, the DC-EKF resolves the structural question of how to inject late information without breaking consistency. By updating at the measurement's physical time and replaying forward, it avoids time misalignment and estimator jumps that arise when stale data are applied to the current state; Joseph-form updates and spectral projection maintain positive definiteness and numerical stability. Under typical moderate delays, experiments show markedly smoother error histories with far fewer spikes. As the maximum delay grows, performance remains superior to the uncompensated and fixed-lag baselines and gradually converges toward the onboard-only dead-reckoning level, exhibiting graceful degradation and operational controllability.

Second, the proposed combination of delay threshold calibration and adaptive confidence weighting bridges information quality and fusion weight in an interpretable, online-learned manner. Using effective information gain, NEES filtering, and percentile updates, the learned threshold converges around 6.35 s; during online operation, 1067 station measurements were admitted and 30 rejected, indicating a gate that is neither overly strict nor permissive. Dynamic weights, driven by innovation statistics, delay, and SNR proxies, shift over time from IMU-dominant to station-dominant and stabilize near  $IMU \approx 0.16$  and  $Station \approx 0.84$ . Implemented as adaptive measurement covariances, this modulation reduces NIS/NEES exceedances and suppresses spike amplitudes, keeping the error history smooth and controllable despite link quality fluctuations. The full adaptive run yields an overall position RMSE of 5.751 m over the 100 s docking segment, demonstrating the joint benefit of thresholding, replay, and weighting. In the context of the large survey-class AUV and 1.5 m-diameter funnel described in Section 3.1, this accuracy is adequate to keep the vehicle within the acoustic homing corridor and to hand over to the sub-meter relative estimates of the Co-Aug-EKF—and, in practice, to short-range optical docking aids in the final meters when water clarity permits.

Third, the Co-Aug-EKF jointly models AUV and MDS states in a unified frame and fuses bidirectional relative observations together with soft relative-kinematics constraints in a single Bayesian update. By explicitly maintaining the cross-covariance block  $P_{AB}$ , information from either platform is passively propagated to the other, avoiding the “correlation forgetting” inherent to independent filters. In our comparison, AUV position RMSE drops from 0.395 m to 0.310 m (21.5%), MDS from 0.228 m to 0.205 m (10.1%), and relative-position RMSE—most directly tied to docking—drops from 0.347 m to 0.280 m ( $\approx 19\%$ ). Boxplots show left-shifted medians and interquartile ranges with fewer outliers, indicating gains in both mean-square performance and robustness. Trajectory overlays confirm markedly improved relative consistency near the docking corridor, yielding cleaner state inputs for terminal attitude alignment and control convergence.

In terms of computational cost, the marginal overhead of delay compensation arises from one historical update plus a limited number of forward replays and grows approximately linearly with the buffer length. The adaptive layer uses batched percentile updates and constant-time recursions, so its cost is well below that of replay. In the proposed

single-AUV–single-MDS configuration, the augmented state collects the pose, velocity, and inertial biases of both platforms together with a small number of soft-alignment states (extrinsic and clock offsets), leading to a state dimension on the order of a few tens (e.g.,  $(n \approx n_A + n_B + n_{\text{align}} \lesssim 30)$ ). The Co-Aug-EKF maintains a dense  $(n \times n)$  covariance matrix, so both memory and the dominant matrix operations scale as  $(O(n^2))$ ; with such a modest  $(n)$ , the resulting cost is negligible compared with the acoustic sampling interval and remains well within real-time limits for typical embedded CPUs. This quadratic behavior is not specific to the proposed method; it arises whenever a centralized EKF maintains a full covariance matrix over an augmented multi-robot state with all pairwise cross-covariances. In a centralized multi-AUV extension with  $(N)$  vehicles and one (or several) stations, the augmented state dimension grows approximately as  $(O(N))$ , while the covariance matrix becomes block dense with  $(O(N^2))$  cross-covariance blocks; both memory and the dominant covariance update operations therefore scale quadratically with  $(N)$ . For small teams, this cost remains acceptable for real-time execution. For larger fleets, one would combine the proposed framework with sparse or clustered covariance structures—keeping only local cross-covariances and relying on distributed or information-form fusion for long-range coupling—to keep computation and communication bounded. Overall, under realistic low-bandwidth, high-latency constraints, the framework achieves a practical balance among real-time operation, accuracy, and consistency, and its scaling behavior is well characterized for multi-agent extensions.

The benefits are modulated by geometry and link conditions. With sparse bidirectional observations, severe geometric degeneracy, or overly weak relative-constraint covariances, the advantage diminishes; conversely, with adequate observation frequency, geometry improved via FIM-guided path design, and effective thresholding/down-weighting of poor-quality data, the cross-covariance “passive gain” becomes more pronounced. A dedicated sensitivity study (Section 4) varying the delay distribution (uniform, truncated normal, exponential-like, and a short-long mixture) under a fixed  $\tau_{\text{max}}$  shows that the DC-EKF RMSE changes by less than about 4%, indicating that performance depends mainly on the delay bound rather than on the precise delay statistics. In addition, a robustness experiment (Section 4) subjects the DC-EKF to heavy-tailed Laplace, Gaussian-mixture, and biased-mixture acoustic noise while the filter still assumes Gaussian measurement noise; in all cases the DC-EKF remains close to the delay-free Standard-EKF baseline ( $\approx 1.3$  m vs. 0.82–0.85 m) and its RMSE varies by less than about 5%, whereas naïve delayed-fusion schemes stay in the  $\approx 20$ –24 m range. Thus, moderate deviations from the Gaussian-noise hypothesis mainly cause a modest, bounded inflation relative to the idealized baseline. Nevertheless, strongly bursty, nonstationary, or extremely heavy-tailed disturbances, together with aggressive maneuvers and significant model mismatch, can still erode consistency and motivate future work on more robust statistics (e.g., Student’s-t or Huber-type updates) or invariant-error formulations.

For deployment, the method exposes clear interfaces and portability. The DC-EKF serves as a front-end for time rectification and consistency-preserving absorption of heterogeneous external observations (USBL, SBL, acoustic bearing, etc.). The adaptive threshold and weights have few hyperparameters and converge online. The Co-Aug-EKF serves as a unified-frame back-end that couples loosely, via information matrices, to upstream outputs, simplifying incremental integration into existing navigation and control stacks. This layered design provides standardized interfaces for future integration with path planning, observability-aware geometry optimization, mission management, and docking control.

Despite these strengths, the present work has several practical limitations. First, all evaluations are simulation-based under numerically realistic but still simplified models; pool and sea trials are needed to verify robustness under real acoustic channels, vehicle–

environment interactions, and implementation imperfections. Second, the study focuses on a single-AUV–single-station configuration; although the layered architecture and block-structured covariance naturally extend to small teams, large fleets would face stricter constraints from the quadratic growth of cross-covariance blocks and from communication budgets. Third, we assume bounded delays and approximately Gaussian noises with first-order linearization; strongly bursty, nonstationary, or heavy-tailed disturbances, as well as aggressive maneuvers and model mismatch, may erode consistency and would require more robust statistics or invariant-filtering variants. These limitations delineate the regime in which the current framework is most applicable and motivate the extensions outlined below.

Promising directions include: (1) robust statistics for heavy-tailed/multimodal noise and Student's  $t$ /mixture residual models, or invariant filtering on Lie groups to improve linearization stability; (2) extension to networked multi-AUV/multi-station localization, where the centralized Co-Aug-EKF would be generalized to larger fleets and combined with sparse or partially decentralized updates to manage the  $O(N^2)$  cross-covariance structure while balancing information consistency against communication and computation budgets; (3) information-guided active sensing and geometry optimization that couple observation selection with platform motion under a communication budget; and (4) sea trials closer to engineering conditions to evaluate threshold convergence, weight migration, and closed-loop performance across sea states, occlusions, and geometries, and to tightly couple estimation with docking control for an end-to-end observe–estimate–control loop.

In summary, by combining temporally consistent absorption in the DC-EKF, quality-matched thresholds and weights, and unified cooperative estimation in the Co-Aug-EKF, we deliver reliable state awareness for AUV–MDS cooperative docking under stringent acoustic constraints. The framework bridges theory and practice: it adheres to clear probabilistic and statistical-consistency principles while remaining simple and deployable in computation and implementation. Although the present study focuses on a single-AUV–single-station configuration, the same layered architecture and block-structured covariance are directly compatible with small multi-AUV fleets, and the accompanying scalability discussion clarifies how computational load and cross-covariance management grow with the number of cooperating vehicles. As tasks and environments grow more demanding, this renders the proposed approach a foundational capability that can be extended and integrated into higher-level planners, offering a reusable pathway to high-precision, robust docking and cooperative operations in the ocean.

**Author Contributions:** Conceptualization, S.Y. and H.Y.; methodology, H.Y. and S.Y.; software, H.Y.; validation, H.Y.; formal analysis, H.Y. and S.Y.; investigation, H.Y. and S.Y.; resources, S.Y.; data curation, H.Y.; writing—original draft preparation, H.Y.; writing—review and editing, H.Y. and S.Y.; visualization, H.Y.; supervision, S.Y.; project administration, S.Y. All authors have read and agreed to the published version of the manuscript.

**Funding:** This research received no external funding.

**Data Availability Statement:** The code and simulation configurations supporting this study are available from the corresponding author upon reasonable request and will be made publicly available upon publication in a public repository.

**Acknowledgments:** The authors thank the laboratory and administrative staff for their support.

**Conflicts of Interest:** The authors declare no conflicts of interest.



# Nomenclature

|                               |                                                                          |
|-------------------------------|--------------------------------------------------------------------------|
| $W$                           | Global inertial (world) frame                                            |
| $A, B$                        | Body-fixed frames of the AUV and the MDS                                 |
| $p_A^W, v_A^W$                | AUV position and velocity in frame $W$                                   |
| $p_B^W, v_B^W$                | MDS position and velocity in frame $W$                                   |
| $q_A^W, q_B^W$                | Unit quaternions representing AUV/MDS attitude with respect to $W$       |
| $x_A, x_B$                    | AUV and MDS state vectors (pose, velocity, inertial-sensor biases, etc.) |
| $x_{align}$                   | Soft alignment states (e.g., inter-frame alignment and clock offset)     |
| $x_{aug}$                     | Augmented state $[x_A^T, x_B^T, x_{align}^T]^T$ used in the Co-Aug-EKF   |
| $u_A, u_B$                    | Control/command inputs to the AUV and MDS kinematic models               |
| $f(\cdot)$                    | State-transition (process) model                                         |
| $h(\cdot)$                    | Measurement model                                                        |
| $z_k$                         | Generic measurement at time step $k$                                     |
| $z_{IMU}, z_{DVL}, z_{depth}$ | Onboard IMU, DVL, and depth measurements                                 |
| $z_{MDS}$                     | Acoustic range/bearing observation of the AUV from the MDS               |
| $F_k, H_k$                    | Jacobians of the process and measurement models                          |
| $w_k, v_k$                    | Process and measurement noise                                            |
| $Q_k, R_k$                    | Process and nominal measurement noise covariance                         |
| $R_{eff}$                     | Effective (adaptively scaled) measurement covariance                     |
| $P_k$                         | State-error covariance                                                   |
| $K_k$                         | Kalman gain                                                              |
| $S_k$                         | Innovation covariance                                                    |
| $P_{AA}, P_{BB}, P_{AB}$      | Covariance and cross-covariance blocks for AUV and MDS                   |
| $t_{gen}, t_{rcv}$            | Generation and reception time of an acoustic measurement                 |
| $\tau$                        | Acoustic link delay $\tau = t_{rcv} - t_{gen}$                           |
| $\tau_{max}$                  | Maximum delay supported by the ring buffer                               |
| $\tau_c$                      | Time-decay constant used in the effective-information metric             |
| $\tau_{thr}$                  | Learned delay threshold for admitting delayed measurements               |
| $I_{eff}(\tau)$               | Effective information of a delayed measurement with delay $\tau$         |
| $c_{IMU}, c_{MDS}$            | Raw confidence scores for onboard and MDS channels                       |
| $w_{IMU}, w_{MDS}$            | Normalized fusion weights for onboard and MDS channels                   |
| $e_k$                         | State estimation error at time step $k$                                  |
| RMSE                          | Root-mean-square error (typically of position)                           |
| NEES                          | Normalized estimation error squared                                      |
| NIS                           | Normalized innovation squared                                            |
| AUV                           | Autonomous underwater vehicle                                            |
| MDS                           | Mobile docking station                                                   |
| IMU                           | Inertial measurement unit                                                |
| DVL                           | Doppler Velocity Log                                                     |
| EKF                           | Extended Kalman filter                                                   |
| DC-EKF                        | Delay-compensated extended Kalman filter                                 |
| Co-Aug-EKF                    | Cooperative augmented extended Kalman filter                             |
| OOS/OOSM                      | Out-of-sequence (measurement)                                            |
| SNR                           | Signal-to-noise ratio                                                    |
| FIM                           | Fisher information matrix                                                |

# References

1. Bhatt, E.S.C.; Viquez, O.; Schmidt, H. Under-ice acoustic navigation using real-time model-aided range estimation. *J. Acoust. Soc. Am.* **2022**, *151*, 2656–2671. [\[CrossRef\]](#)
2. Barker, L.D.L.; Whitcomb, L.L. Performance analysis of ice-relative upward-looking Doppler navigation of underwater vehicles beneath moving sea ice. *J. Mar. Sci. Eng.* **2021**, *9*, 174. [\[CrossRef\]](#)

3. González-García, J.; Gómez-Espinosoa, A.; Cuan-Urquizo, E.; García-Valdovinos, L.G.; Salgado-Jiménez, T.; Escobedo Cabello, J.A. Autonomous underwater vehicles: Localization, navigation, and communication for collaborative missions. *Appl. Sci.* **2020**, *10*, 1256. [\[CrossRef\]](#)
4. Maurelli, F.; Krupiński, S.; Xiang, X.; Petillot, Y. AUV localisation: A review of passive and active techniques. *Int. J. Intell. Robot. Appl.* **2022**, *6*, 246–269. [\[CrossRef\]](#)
5. Zhang, Y.; Zhang, F.; Wang, Z.; Zhang, X. Localization uncertainty estimation for autonomous underwater vehicle navigation. *J. Mar. Sci. Eng.* **2023**, *11*, 1540. [\[CrossRef\]](#)
6. Lv, P.F.; Lv, J.Y.; Hong, Z.C.; Xu, L.X. Integration of deep sequence learning-based virtual GPS model and EKF for AUV navigation. *Drones* **2024**, *8*, 441. [\[CrossRef\]](#)
7. Fernandes, M.; Sahoo, S.R.; Kothari, M. Cooperative localization for autonomous underwater vehicles—A comprehensive review. *arXiv* **2023**, arXiv:2307.06189.
8. Bahr, A.; Leonard, J.J.; Fallon, M.F. Cooperative localization for autonomous underwater vehicles. *Int. J. Robot. Res.* **2009**, *28*, 714–728. [\[CrossRef\]](#)
9. Li, Z.; Li, W.; Sun, K.; Fan, D.; Cui, W. Recent progress on underwater wireless communication methods and applications. *J. Mar. Sci. Eng.* **2025**, *13*, 1505. [\[CrossRef\]](#)
10. Li, Y.; Jia, N.; Han, R.; Qu, S.; Liu, Y.; Guo, Z.; Guo, S. Statistical analysis of intermediate frequency underwater acoustic communication channel characteristics in deep-sea sound channel axis. *Electronics* **2024**, *13*, 4948. [\[CrossRef\]](#)
11. Bar-Shalom, Y. Update with out-of-sequence measurements in tracking: Exact solution. *IEEE Trans. Aerosp. Electron. Syst.* **2002**, *38*, 769–777. [\[CrossRef\]](#)
12. Ullah, I.; Qureshi, M.B.; Khan, U.; Memon, S.A.; Shi, Y.; Peng, D. Multisensor-based target-tracking algorithm with out-of-sequence-measurements in cluttered environments. *Sensors* **2018**, *18*, 4043. [\[CrossRef\]](#)
13. Li, Z.; Sun, M.; Duan, Q.; Mao, Y. Robust state estimation for uncertain discrete linear systems with delayed measurements. *Mathematics* **2022**, *10*, 1365. [\[CrossRef\]](#)
14. Frei, H.; Burri, M.; Rems, F.; Risse, E.A. A robust navigation filter fusing delayed measurements from multiple sensors and its application to spacecraft rendezvous. *Adv. Space Res.* **2023**, *72*, 2874–2900. [\[CrossRef\]](#)
15. Dong, L.; Xu, H.; Feng, X.; Han, X.; Yu, C. A research on the simultaneous localization method in the process of autonomous underwater vehicle homing with unknown varying measurement error. *Appl. Sci.* **2019**, *9*, 4614. [\[CrossRef\]](#)
16. Xie, T.; Li, Y.; Jiang, Y.; Pang, S.; Xu, X. Three-dimensional mobile docking control method of an underactuated autonomous underwater vehicle. *Ocean Eng.* **2022**, *265*, 112634. [\[CrossRef\]](#)
17. Wu, W.; Zhang, W.; Du, X.; Li, Z.; Wang, Q. Homing tracking control of autonomous underwater vehicle based on adaptive integral event-triggered nonlinear model predictive control. *Ocean Eng.* **2023**, *277*, 114243. [\[CrossRef\]](#)
18. Yu, T.; Xu, G.; Zhang, Q.; Liu, T. A dynamic docking system of AUV based on bearings-only acoustic and visual coupled localization. *Ocean Eng.* **2025**, *328*, 121001. [\[CrossRef\]](#)
19. Han, P.; Zhang, W.; Wu, Q.; Shi, Y. Design of UUV underwater autonomous recovery system and controller based on mooring-type mobile docking station. *J. Mar. Sci. Eng.* **2025**, *13*, 1861. [\[CrossRef\]](#)
20. Sun, C.; Zhang, Y.; Wang, G.; Gao, W. A new variational Bayesian adaptive extended Kalman filter for cooperative navigation. *Sensors* **2018**, *18*, 2538. [\[CrossRef\]](#)
21. Potokar, E.R.; Norman, K.; Mangelson, J.G. Invariant extended Kalman filtering for underwater navigation. *IEEE Robot. Autom. Lett.* **2021**, *6*, 5792–5799. [\[CrossRef\]](#)
22. Pei, F.; Xu, H.; Jiang, N.; Zhu, D. A novel in-motion alignment method for underwater SINS using a state-dependent Lie group filter. *Navigation* **2020**, *67*, 451–470. [\[CrossRef\]](#)
23. Sheng, G.; Liu, X.; Zhang, Y.; Shao, Q.; Xu, H.; Cheng, X.; Yuan, X. The EKF-based SINS/DVL integrated navigation for AUV on Lie group under hovering condition. *Ocean Eng.* **2025**, *325*, 120742. [\[CrossRef\]](#)
24. Chen, Z.; Biggie, H.; Ahmed, N.; Julier, S.; Heckman, C. Kalman filter auto-tuning with consistent and robust Bayesian optimization. *IEEE Trans. Aerosp. Electron. Syst.* **2024**, *60*, 2236–2250. [\[CrossRef\]](#)
25. Jeong, D.B.; Ko, N.Y. Sensor fusion for underwater vehicle navigation compensating misalignment using Lie theory. *Sensors* **2024**, *24*, 1653. [\[CrossRef\]](#)
26. Wang, Y.; Xie, C.; Liu, Y.; Zhu, J.; Qin, J. A multi-sensor fusion underwater localization method based on unscented Kalman filter on manifolds. *Sensors* **2024**, *24*, 6299. [\[CrossRef\]](#)
27. Ma, X.; Wei, Z.; Liu, W.; Wang, S. Event-triggered state filter estimation for INS/DVL integrated navigation with correlated noise and outliers. *Sensors* **2025**, *25*, 1545. [\[CrossRef\]](#) [\[PubMed\]](#)
28. Li, X.; Hao, G. Event-triggered Kalman filter and its performance analysis. *Sensors* **2023**, *23*, 2202. [\[CrossRef\]](#) [\[PubMed\]](#)
29. Yang, Y.; Xu, B.; Ye, B.; Li, F. Deep learning-assisted ES-EKF for surface AUV navigation with SINS/GPS/DVL integration. *J. Mar. Sci. Eng.* **2025**, *13*, 2035. [\[CrossRef\]](#)

30. Ma, H.; Mu, X.; He, B. Adaptive navigation algorithm with deep learning for autonomous underwater vehicle. *Sensors* **2021**, *21*, 6406. [\[CrossRef\]](#)
31. Topini, E.; Fanelli, F.; Topini, A.; Pebody, M.; Ridolfi, A.; Phillips, A.B.; Allotta, B. An experimental comparison of deep learning strategies for AUV navigation in DVL-denied environments. *Ocean Eng.* **2023**, *274*, 114034. [\[CrossRef\]](#)
32. Brouk, J.D.; DeMars, K.J. Kalman filtering with uncertain and asynchronous measurement epochs. *Navig. J. Inst. Navig.* **2024**, *71*, navi.652. [\[CrossRef\]](#)
33. Freitas Iglesias, C., Jr.; Bolic, M. Batch Bayesian auto-tuning for nonlinear Kalman estimators. *Sci. Rep.* **2025**, *15*, 33832. [\[CrossRef\]](#)
34. Zhang, L.; Gao, Y.; Guan, L. Optimizing AUV navigation using factor graphs with side-scan sonar integration. *J. Mar. Sci. Eng.* **2024**, *12*, 313. [\[CrossRef\]](#)
35. Du, X.; Pang, X.; Guan, F.; Hu, J.; Zhang, W. A novel multi-source navigation algorithm based on factor graph in complex underwater environments of polar regions. *Ocean Eng.* **2024**, *301*, 117516. [\[CrossRef\]](#)
36. Theocharidis, T.; Kavallieratou, E. Underwater communication technologies: A review. *Telecommun. Syst.* **2025**, *88*, 54. [\[CrossRef\]](#)
37. Kusanur, V.; Desai, P.K.; Hemanth, T.M.; Manjunath, K.M.; HB, S.G. Performance analysis of underwater communication using Li-Fi across different water qualities. *J. Commun.* **2025**, *20*, 589–595. [\[CrossRef\]](#)
38. Silvestrini, S.; Piccinin, M.; Zanotti, G.; Brandonisio, A.; Lungli, P.; Lavagna, M. Implicit extended Kalman filter for optical terrain relative navigation using delayed measurements. *Aerospace* **2022**, *9*, 503. [\[CrossRef\]](#)
39. Zhao, W.; Zhao, H.; Liu, G.; Zhang, G. ANFIS-EKF-based single-beacon localization algorithm for AUV. *Remote Sens.* **2022**, *14*, 5281. [\[CrossRef\]](#)
40. Sekimori, Y.; Noguchi, Y.; Matsuda, T.; Weng, Y.; Maki, T. Bearing, elevation, and depth difference passive inverted acoustic navigation for an AUV fleet. *Appl. Ocean Res.* **2024**, *144*, 103897. [\[CrossRef\]](#)
41. Rypkema, N.R.; Schmidt, H.; Fischell, E.M. Synchronous-clock range-angle relative acoustic navigation: A unified approach to multi-AUV localization, command, control, and coordination. *Field Robot.* **2022**, *2*, 774–806. [\[CrossRef\]](#)
42. Ernits, J.; Dearden, R.; Pebody, M. Formal Methods for Automated Diagnosis of Autosub 6000. In Proceedings of the First NASA Formal Methods Symposium, Moffett Field, CA, USA, 6–8 April 2009.
43. Fan, S.; Bose, N.; Liang, Z. Polar AUV challenges and applications: A review. *Drones* **2024**, *8*, 413. [\[CrossRef\]](#)
44. Hobson, B.W.; McEwen, R.S.; Erickson, J.; Hoover, T.; McBride, L.; Shane, F.; Bellingham, J.G. The development and ocean testing of an AUV docking station for a 21" AUV. In Proceedings of the OCEANS 2007, Vancouver, BC, Canada, 29 September–4 October 2007; pp. 1–6.
45. Wang, Z.; Zhou, X.; Yang, Y.; Hu, Z.; Wei, Q.; Fan, C.; Liao, Z. Robust underwater docking visual guidance and positioning method based on a cage-type dual-layer guiding light array. *Sensors* **2025**, *25*, 6333. [\[CrossRef\]](#) [\[PubMed\]](#)
46. Campagnaro, F.; Steinmetz, F.; Renner, B.C. Survey on low-cost underwater sensor networks: From niche applications to everyday use. *J. Mar. Sci. Eng.* **2023**, *11*, 125. [\[CrossRef\]](#)
47. Larsen, T.D.; Andersen, N.A.; Ravn, O.; Poulsen, N.K. Incorporation of time delayed measurements in a discrete-time Kalman filter. In Proceedings of the 37th IEEE Conference on Decision and Control, Tampa, FL, USA, 18 December 1998; pp. 3972–3977.
48. Goh, S.T.; Tissera, M.S.C.; Tan, R.D.D.; Srivastava, A.; Low, K.S.; Lim, L.S. Simplex back propagation estimation method for out-of-sequence attitude sensor measurements. *Sensors* **2022**, *22*, 7970. [\[CrossRef\]](#)
49. Liang, S.; Xu, G.; Qin, Z. A robust Kalman filter for heavy-tailed measurement noise based on Gamma Pearson VII mixture distribution. *IEEE Access* **2025**, *13*, 47680–47692. [\[CrossRef\]](#)
50. Stojanovic, M.; Preisig, J. Underwater Acoustic Communication Channels: Propagation Models and Statistical Characterization. *IEEE Commun. Mag.* **2009**, *47*, 84–89. [\[CrossRef\]](#)

**Disclaimer/Publisher's Note:** The statements, opinions and data contained in all publications are solely those of the individual author(s) and contributor(s) and not of MDPI and/or the editor(s). MDPI and/or the editor(s) disclaim responsibility for any injury to people or property resulting from any ideas, methods, instructions or products referred to in the content.