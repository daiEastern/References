

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of Robotics and Autonomous Systems journal](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of Robotics and Autonomous Systems journal

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Physics-informed LSTM-based delay compensation framework for high-fidelity teleoperation of wheeled mobile robots

Ahmad Abubakar<sup>a</sup>![ORCID icon](17413706fd4997a1a4bdf85c6864eee1_img.jpg)\*, Yahya Zweiri<sup>b,c</sup>, Abdel Gafoor Haddad<sup>a</sup>, Mubarak Yakubu<sup>a</sup>![ORCID icon](f419710cbe076aa30a9c6c031b5cbe84_img.jpg), Ruqayya Alhammadi<sup>a</sup>, Lakmal Seneviratne<sup>a,d,\*</sup>

<sup>a</sup> Center for Autonomous Robotic Systems (KUCARS), Khalifa University, Abu Dhabi, United Arab Emirates

<sup>b</sup> Department of Aerospace Engineering, Khalifa University, Abu Dhabi, United Arab Emirates

<sup>c</sup> Advanced Research and Innovation Center (ARIC), Khalifa University, Abu Dhabi, United Arab Emirates

<sup>d</sup> Department of Mechanical and Nuclear Engineering, Khalifa University, Abu Dhabi, United Arab Emirates

## ARTICLE INFO

### Keywords:

Bilateral teleoperation  
Communication Delays  
Predictor framework  
Physics-informed LSTM  
WMRs  
Soft terrains

## ABSTRACT

Bilateral teleoperation of wheeled mobile robots (WMRs) traversing soft terrains with interaction force feedback is crucial for applications like lunar exploration, as it helps regulate travel reduction and path deviation. However, network-induced communication delays present a challenge in achieving high-fidelity closed-loop integration, degrading slippage awareness and command-tracking performance. To address this, a physics-informed long short-term memory (PiLSTM)-based predictor framework is proposed to predict intended commands and anticipated slippage feedback in WMR teleoperation systems under large delays. Conventional model-free predictors often demonstrate significant prediction errors when compensating for large delays in complex dynamics systems due to their limited adaptability and generalizability. In contrast, the proposed PiLSTM predictor integrates an LSTM network with time-delay dynamics and a feedback mechanism to better capture strong nonlinear and temporal dynamics for improved adaptability and generalizability while ensuring accurate prediction. A series of human-in-the-loop experiments for a track-following task were conducted to validate the effectiveness of the PiLSTM framework in compensating for the large delays, similar to those encountered in lunar exploration. Its performance was compared against first-order time-delay (FOD) and wave variable transformation (WV) approaches for delay compensation. The results demonstrate the robustness of the PiLSTM framework across various test scenarios, achieving up to 29.7% improvement in prediction accuracy compared to the FOD framework. Furthermore, the proposed PiLSTM-based teleoperation system achieved significantly improved tracking performance and force transparency compared to FOD- and WV-based systems, ensuring higher fidelity and more robust closed-loop integration. These findings highlight the PiLSTM framework's adaptability and generalizability for complex teleoperation systems. A supplementary video is available at <https://youtu.be/dMVLEV7qTve>.

## 1. Introduction

Teleoperated wheeled mobile robots (WMRs) have garnered considerable attention across diverse domains such as industrial automation, military operations, and space exploration [1–3]. These platforms are remotely controlled by human operators via a teleoperation system, allowing the execution of complex tasks in hazardous or inaccessible environments while safeguarding the operators [3,4]. Teleoperation systems typically transmit motion commands and relay sensory feedback from the environment. While a conventional teleoperation system relies solely on visual feedback, a bilateral teleoperation system integrates tactile (force) feedback, delivering a nearly 17% improvement in

environmental perception, thus enhancing operators' situational awareness [2,5]. Such systems are particularly well-suited for applications that require precise dynamic interaction feedback in remote environments. Notably, the navigation of space rovers traversing complex, unstructured terrains in planetary exploration missions demands this kind of systems [6].

Terrain traversability presents a critical challenge for the mobility of teleoperated WMRs that rely on look-ahead visual feedback when operating on inclined soft terrains [7]. These terrains induce longitudinal slippage due to complex wheel–terrain interactions, leading to poor command-tracking performance, which in turn results in reduced travel distance and significant path deviation. Such slippage-related

\* Corresponding authors.

E-mail addresses: [100059792@ku.ac.ae](mailto:100059792@ku.ac.ae), [ahmad.abubakar@ku.ac.ae](mailto:ahmad.abubakar@ku.ac.ae) (A. Abubakar), [lakmal.seneviratne@ku.ac.ae](mailto:lakmal.seneviratne@ku.ac.ae) (L. Seneviratne).

challenges are difficult to perceive using visual feedback alone, especially in environments lacking an external viewpoint and poor lighting conditions, thereby impairing terrain interaction awareness [8]. To address this, recent works have increasingly focused on conveying the slippage information through force feedback via the bilateral teleoperator system to supplement the visual feedback [9–12]. This enables the operator to perceive terrain response through haptic cues and adapt control actions accordingly to compensate for the slippage, thereby enhancing command-tracking performance and minimizing travel reduction and path deviation. Notably, the study in [10] demonstrates the effectiveness of slippage awareness through force feedback in enhancing WMR teleoperation performance under low-light conditions, despite relying on discrete feedback to differentiate between slip, slide, and normal states. Other works [13–15] have introduced continuous force feedback to convey a better representation of the slippage information, enabling more effective compensation for slippage and improving overall tracking performance. Furthermore, various techniques for estimating and conveying slippage information have been explored in prior works [6,7], underscoring the importance of effective slippage feedback for effective WMR teleoperation on soft terrains.

However, the effectiveness of slippage awareness via force feedback is significantly compromised in long-distance teleoperation. To enable connectivity over interplanetary distances, specialized communication networks such as the Deep Space Network (DSN) and Kongsberg Satellite Services (KSAT) are typically employed [16,17]. These networks inherently introduce substantial communication delays that degrade the overall performance of the WMR teleoperation. For instance, in the Emirates Lunar Mission (EML) Rashid rover teleoperation, one-way delays ranging from 1.3 to 2.2 s were reported via KSAT ground stations [16]. These delays impair the transmission of both motion commands and the force feedback, compromising the fidelity of the closed-loop teleoperation system necessary for timely and effective slippage compensation [18,19]. The resulting delayed force feedback prevents the operator from perceiving slippage events in real-time, while delayed control commands hinder immediate corrective actions. This asynchrony results in cumulative tracking errors, reduced slippage awareness, and ultimately degraded tracking performance — potentially destabilizing the entire closed-loop system [2,20,21]. Crucially, the threshold of delay that leads to instability varies depending on the system dynamics and application domain [22]. The strong coupling between effective slippage awareness and delayed force feedback thus motivates the need for delay-resilient predictors. These predictors act as virtual feedback generators, predicting future feedback and compensating for the delays in long-distance teleoperation. Recent studies have explored a variety of such techniques, including passivity-based, model-based, and model-free approaches [2–4,9]. Fig. 1 illustrates how the tracking performance of bilateral teleoperated WMRs correlate with degrees of closed-loop fidelity and terrain traversability.

In this paper, we present the first physics-informed deep learning-based delay compensation framework to mitigate the effect of large delays encountered in transmitting motion commands and interaction force feedback during WMRs teleoperation for lunar exploration. This approach seeks to achieve high-fidelity closed-loop integration despite the large delays.

### 1.1. Related work

Extensive research has investigated the impact of network delays and proposed prediction-based compensation strategies for bilateral WMR teleoperation systems to maintain high-fidelity closed-loop integration [4,23–25]. Nevertheless, achieving such integration under significant delays remains a critical challenge [22,23].

Many studies have explored various passivity-based techniques, including the wave variable transformation (WV) method, to address delays in bilateral teleoperated WMRs. For instance, [26] implemented

![Figure 1: A 3D surface plot illustrating the conceptual relationship between WMR Performance, Closed-Loop Fidelity, and Terrain Traversability. The vertical axis represents WMR Performance. The horizontal axis represents Closed-Loop Fidelity, with labels 'No delay Perfect SA' and 'Large delay Poor SA'. The depth axis represents Terrain Traversability, with labels 'Hard soil Flat surface' and 'Soft soil Inclined surface'. The surface shows a peak in performance at high fidelity and high traversability, and a trough at low fidelity and low traversability.](1ac0e11d90bece49015adc89be472a39_img.jpg)

Figure 1: A 3D surface plot illustrating the conceptual relationship between WMR Performance, Closed-Loop Fidelity, and Terrain Traversability. The vertical axis represents WMR Performance. The horizontal axis represents Closed-Loop Fidelity, with labels 'No delay Perfect SA' and 'Large delay Poor SA'. The depth axis represents Terrain Traversability, with labels 'Hard soil Flat surface' and 'Soft soil Inclined surface'. The surface shows a peak in performance at high fidelity and high traversability, and a trough at low fidelity and low traversability.

Fig. 1. The conceptual relationship illustrates how the command-tracking performance of teleoperated WMR is affected by both the closed-loop fidelity and the terrain traversability.

the WV method to compensate for a 450 ms delay in an internet-based teleoperation system. However, their approach was found to be effective only for smaller delays, specifically those less than 280 ms. Similarly, the work presented in [20] utilized the WV method to compensate for round-trip delays of 2 s in the teleoperation system. Although the WV method guarantees stability, one major limitation identified in these studies is its conservative nature [3,4], which results in poor fidelity of closed-loop integration, especially under varying delays. Another study [23] explored alternative techniques based on the time domain passivity method (TDPM) to compensate for varying delays of a mean of 600 ms for WMRs in dynamic environments. This method, also adopted in [13,27], often introduces excessive damping and fails to accurately estimate energy transfer under large and varying delays. As a result, delayed responses accumulate with compensatory adjustments, constraining the system's operational bandwidth and reducing overall fidelity [28].

On the other hand, model-based techniques, model-free techniques, and hybrids of the two techniques have emerged as a prevailing trend and have been extensively studied in teleoperated WMRs [2,3]. Model-based techniques rely on predicting future states based on a predefined system–environment model to compensate for delays. Examples include the use of a simple Smith predictor to counteract delays of 400 ms [19], a modified Smith predictor on a hydraulic test stand to address 100 ms delays [29], a neural-network-based Smith predictor for 500 ms [30], a Kalman filter predictor to handle varying delays of 500 ms in cyber-physical systems [31], extended Kalman filter predictor to compensate for delays of 250 ms in teleoperated WMRs [9], and an adaptive filter-based predictor for 900 ms [32]. In addition to these, more advanced model-based approaches have recently been introduced. For example, the unified contact model (UCM) and hybrid motion/force predictor integrate contact dynamics to compensate for varying delays of up to 300 ms, improving haptic feedback in manipulation tasks performed in unstructured environments [33]. Meanwhile, self-triggered model predictive control (MPC) utilizes high-order state estimations to compensate for control command delays, adaptively managing control updates in the presence of varying delays [34]. While these model-based techniques have proven effective in achieving adequate closed-loop fidelity in known and structured environments, they still face limitations when applied to complex interactions and unstructured environments. First, their prediction performance can be significantly undermined by modeling errors due to varying and unknown parameters for highly dynamic conditions. Additionally, they are mostly used to compensate for small delays, and typically in only one direction. Furthermore, such approaches often rely on conservative derivative gains or damping

of measured system states to ensure stability at the expense of force transparency under delays [2,3,9,35,36].

Due to these limitations of model-based techniques, researchers have increasingly focused on model-free approaches to compensate for network delays without reliance on a system model [3]. These approaches have been extensively applied to compensate for large delays in both directions in teleoperated WMRs, particularly given the complexities involved in modeling human operator driving behavior [32] and the nonlinear dynamics of environmental interactions [4]. Zheng et al. [18] introduced the first-order time-delay (FOD) model-free predictor designed for closed network systems operating below 0.8 Hz, to compensate for small delays of 135 ms while maintaining system stability. It was later validated on teleoperated WMRs on hard terrains to compensate for delays of 300 ms, demonstrating its effectiveness in dynamic environments [37]. Further validation was conducted on soft terrains, confirming the predictor's versatility [38]. Building on this, they further combined the FOD approach with a model-based approach to compensate for large delays of 600 ms in high-speed WMRs [22], achieving more accurate predictions than either approach alone. To address uncertainty in real network delays, the work in [39] introduced an adaptively varying parameter to better accommodate uncertain delays by the predictor. Despite the enhanced robustness, the approach encountered increased oscillatory error in high-frequency variables [3]. This undermined its prediction performance. Subsequent work in [40] further modified the FOD predictor by introducing a regularization parameter to compensate for small delays of 175 ms, which effectively damped the oscillatory error gain and improved the overall performance. However, in the recent work [21], we implemented this modified FOD predictor to compensate for large delays of 1.5 s experienced by lunar teleoperated WMRs [41]. The results show that only a few portion of the delays are compensated, demonstrating the difficulties in addressing large delays and achieving high-fidelity closed-loop integration. This limitation is attributed to significant prediction errors that persist due to the FOD predictor's inability to model the strong nonlinear and temporal dynamics, resulting in limited adaptability in complex systems.

Recent advancements in deep learning have contributed significantly to various aspects of bilateral teleoperation systems, particularly in areas such as modeling strong nonlinear dynamics, handling time-dependent dynamics, and enhancing interaction with complex environments [3]. For instance, deep neural networks (DNNs) have proven effective in solving challenging problems such as modelling complex dynamics using convolutional neural networks (CNNs) [42], which have been employed to adapt teleoperation systems to unpredictable remote environments. Additionally, reinforcement learning (RL) has shown promise in compensating for control errors by optimizing control policies for complex navigation tasks [43]. Similarly, long short-term memory (LSTM) networks have been effectively used to capture the temporal dependencies present in teleoperated tasks, improving robot-environment interaction compensation [44]. Moreover, LSTM networks have been employed for active prediction to model delayed dynamics by effectively capturing nonlinear and temporal dependencies [45,46]. However, despite these promising advancements, several challenges remain in implementing DNNs in real-world teleoperation systems, particularly in scenarios involving highly complex dynamics [47,48]. This is largely because existing works have prioritized improving the prediction accuracy, often overlooking the adaptability and generalization required for real-world deployments. First, while DNNs are excellent at learning complex relationships between input and output data, they often function as “black-box” models, offering little insight into the underlying physical principles driving the system dynamics [49]. This lack of interpretability can limit their adaptability in scenarios where understanding the underlying mechanisms is critical [45,50]. Secondly, the computational cost of training DNNs with large datasets or high-dimensional data is considerable. This can be a limiting factor when dealing with real-time complex teleoperation

systems, where fast and efficient model training is crucial [51,52]. To address the challenges associated with conventional DNN modeling techniques, physics-informed deep neural networks (PiDNNs) have recently emerged as a promising solution for modeling highly nonlinear dynamics in complex systems [50,51,53,54]. By incorporating known physical constraints directly into the learning process, these models offer improved interpretability and generalization under well-defined conditions [52]. Nonetheless, these models may still struggle to adapt to the dynamic variations encountered in real-world systems. Notably, the works in [50,53] primarily focus on modeling deterministic physical systems with synchronized inputs and do not explicitly address the challenges posed by stochastic and interactive teleoperation systems involving complex delay dynamics with high variability. To the best of our knowledge, the application of physics-informed DNN techniques integrating feedback mechanisms for compensating large delays [16], in teleoperation systems has not been previously explored. This presents a significant research gap in developing delay compensation techniques that exhibit both adaptability and generalizability across diverse scenarios within the field of WMR teleoperation.

### 1.2. Contributions

In this paper, we address the aforementioned research gap by developing a new predictor framework that integrates LSTM networks with explicitly modeled time-delay dynamics. Firstly, this framework improves the prediction accuracy of intended motion commands and anticipated force feedback, thereby compensating for large delays in the teleoperation systems. Secondly, physical constraints derived from first-order time-delay (FOD) dynamics are embedded into the LSTM learning process, along with a feedback mechanism to improve the framework's adaptability and generalizability to uncertain delays. The feedback mechanism iteratively refines predictions, allowing the predictor to remain robust against variations in delays. Lastly, our proposed approach achieves more robust and high-fidelity closed-loop integration for the bilateral teleoperation of WMRs, which improves tracking performance and force transparency under large delay conditions. The main contributions of this paper are outlined as follows:

1. We first develop a real-time test platform that enables teleoperation of a WMR on soft terrain with interaction force feedback, capable of reproducing realistic terrain-induced slippage conditions. A data collection framework is introduced to facilitate the generation of synchronized delayed and undelayed datasets for key coupling variables, including motion commands and slippage-based force feedback, which serve as essential features for training LSTM-based predictors to compensate for delays.
2. We propose a physics-informed LSTM (PiLSTM)-based predictor framework that compensates for large bidirectional delays in WMR teleoperation systems. It comprises a forward predictor for estimating undelayed motion commands and a backward predictor for estimating undelayed force feedback, combined together to restore fidelity in the closed-loop system. Each predictor integrates time-delay dynamics as soft physical constraints, and employs a feedback-driven refinement mechanism to improve adaptability to delay variation.
3. Next, we analyze the generalization performance of the PiLSTM predictor on variable delayed data with and without incorporating the feedback mechanisms, demonstrating that feedback improves adaptability and prediction accuracy in unseen scenarios. We conduct online prediction performance comparisons between the PiLSTM framework and the conventional FOD predictor, highlighting its superior effectiveness in compensating large delays.

![Figure 2: Proposed PiLSTM-based teleoperation system architecture. The diagram is divided into three main sections: Operator Station, Remote Environment, and Communication Channel. The Operator Station includes a Master Robot (Haptic device) where the operator applies force f_h(t) and controls joints q_m(t). Motion commands x_m(t) are sent to the Remote Environment via the Communication Channel. The Remote Environment features a Slave Robot (WMR-Rashid rover) on soft terrains, with sensors for slippage estimation, wheels encoder, and IMU sensor. The Communication Channel contains Forward and Backward Predictors, each with a ZOH sampler, Window buffer, and Trained PiLSTM. The Forward Predictor outputs predicted motion commands x_m(t-T(t)), while the Backward Predictor outputs predicted force feedback f_e(t-T(t)). The system uses green lines for the predicted case (with delay compensation) and red lines for the delayed case (without delay compensation).](9e6062272bbe3ddbb7c0606721d64cf0_img.jpg)

Figure 2: Proposed PiLSTM-based teleoperation system architecture. The diagram is divided into three main sections: Operator Station, Remote Environment, and Communication Channel. The Operator Station includes a Master Robot (Haptic device) where the operator applies force f\_h(t) and controls joints q\_m(t). Motion commands x\_m(t) are sent to the Remote Environment via the Communication Channel. The Remote Environment features a Slave Robot (WMR-Rashid rover) on soft terrains, with sensors for slippage estimation, wheels encoder, and IMU sensor. The Communication Channel contains Forward and Backward Predictors, each with a ZOH sampler, Window buffer, and Trained PiLSTM. The Forward Predictor outputs predicted motion commands x\_m(t-T(t)), while the Backward Predictor outputs predicted force feedback f\_e(t-T(t)). The system uses green lines for the predicted case (with delay compensation) and red lines for the delayed case (without delay compensation).

**Fig. 2.** Proposed PiLSTM-based teleoperation system, including a forward predictor and a backward predictor to form the framework, and a blended architecture for the delayed teleoperated WMR subjected to dynamic slippage. The green lines represent the predicted case (with delay compensation), and the red lines represent the delayed case (without delay compensation) for benchmarking. (For interpretation of the references to colour in this figure legend, the reader is referred to the web version of this article.)

4. We finally validate the effectiveness of the PiLSTM-based teleoperation system through human-in-the-loop experiments, demonstrating robust and high-fidelity closed-loop teleoperation of WMRs under large delays and dynamic slippage. Its benchmark the restored closed-loop fidelity and task success rate against FOD- and WV-based teleoperation systems, demonstrating consistent and significant improvements.

The structure of the remainder of this paper is as follows. In Section 2, we present the architecture of the proposed bilateral teleoperation system, and delve into integrated system dynamics and controls for the teleoperated WMR on soft terrains. Section 3 discusses the detailed design of the physics-informed LSTM-based predictor, including problem definition, data generation, model development, integration of physical constraints, and performance evaluation. Section 4 presents the human-in-the-loop experiment test platform and the experimental design protocol. Section 5 details the comparative analysis of delay compensation performance and evaluates overall teleoperation performance. Finally, Section 6 summarizes the findings and their significance, and outlines future research directions.

## 2. Proposed bilateral teleoperation system

The core of this research is the compensation of delay in bilateral teleoperation of WMRs on soft terrains with interaction force feedback. The architecture of the proposed bilateral teleoperation system, as illustrated in Fig. 2, comprises several key components, including the haptic device (master robot), the communication channel, the WMR system (slave robot), the soft terrain (remote environment), PiLSTM-based predictor framework (delay compensator), and teleoperator controllers.

### 2.1. Haptic device (master robot)

The Touch X haptic device was used as the master robot to provide effective force feedback [5,32]. Although the device provides three actuated joints, only two are required for planar WMR teleoperation. Therefore, only the first two joints (joint 1 and joint 2) are employed

to encode the operator's intent, corresponding to translational and rotational motion commands, respectively, as shown on the operator side of Fig. 2. The third joint is constrained using a high-gain virtual constraint, effectively transforming the device into a 2-DOF planar interface. This configuration reduces system complexity, facilitates intuitive operator control and telepresence, and ensures compatibility with the non-holonomic motion constraints of the WMR. The use of joint-space mapping is commonly adopted in WMR teleoperation [8], where the operator's intent is applied via the end-effector of the device to generate the corresponding joint positions (angles). The nonlinear dynamic model of the haptic device, derived in [12,13,20], was eventually reduced to approximate linear dynamics as in

$$\mathbf{M}_m \ddot{q}_m(t) + \mathbf{C}_m \dot{q}_m(t) = u_m(t) + f_h(t) \quad (1)$$

where  $\mathbf{M}_m$  represents the mass matrix of the robot,  $\mathbf{C}_m$  denotes the centrifugal matrix,  $q_m = [q_{mv} \ q_{mo}]^T$  is the joints position variable,  $u_m = [u_{mv} \ u_{mo}]^T$  is the joints control input, and  $f_h = [f_{hv} \ f_{ho}]^T$  represents the external force applied by the human operator. This linearized model is considered valid under the low-speed teleoperation condition, where the effects of friction and inertial coupling are negligible.

Due to the unbounded and larger workspace of the WMRs compared to that of the haptic device, conventional position-position coordination often prove inadequate for its teleoperation system. To address potential instability resulting from this workspace mismatch, a new dynamic variable was introduced by combining the position and velocities of the joints,  $x_m = \lambda \dot{q}_m + q_m$  ( $0 < \lambda < 1$ ) [13,14]. As a result, the robot controller can be expressed as  $u_m = \bar{u}_m + u_m^*$ , where  $\bar{u}_m$  is the teleoperation controller, and  $u_m^*$  is the local controller, given by  $u_m^* = \mathbf{B}_{vl} \dot{q}_m$ . The modified linear dynamics result in a first-order system for velocity commands teleoperation, as in

$$\bar{\mathbf{M}}_m \dot{x}_m(t) + \bar{\mathbf{C}}_m x_m(t) = u_m(t) + f_h(t) \quad (2)$$

where  $\bar{\mathbf{M}}_m = \mathbf{M}_m / \lambda$  and  $\bar{\mathbf{C}}_m = (\mathbf{C}_m / \lambda) + \mathbf{B}_{vl}$  are the equivalent mass and centrifugal force coefficients, respectively.  $x_m = [x_{mv} \ x_{mo}]^T$  is

the new joints control variable, which is used to generate the linear and angular velocity commands for the WMR.

Furthermore, the proposed mapping strategy is extensible to master devices with higher DOF and more complex WMR platforms. The presence of the third joint or more, additional degrees of freedom in advanced master devices can be exploited in future extensions of the approach to accommodate WMR with enhanced mobility capabilities, such as articulated or holonomic platforms [11], without compromising the core teleoperation architecture.

### 2.2. Wheeled mobile robot (slave robot)

For this work, the teleoperated WMR utilized was the Khalifa University Lunar Rover as the slave robot, a replica of the EML's Rashid lunar rover [7], as displayed in the remote environment of Fig. 2. The WMR's motion is governed by kinematic model that dictates the non-holonomic motion. In this concept, the WMR locomotion principle assumes that the velocities of the front and rear wheels are nearly equal when operating on flat terrain [55]. The kinematic control design focuses on velocity-level control aimed at traction enhancement of the WMR in low-speed teleoperations, where a kinematic model is often sufficient and widely adopted for the differential drive WMRs [8,12,13,20]. This approach is also favored because kinematic control offers greater robustness in environments with uncertain interaction dynamics like soft terrain [15,55]. The kinematic model of the WMR on soft terrain is adopted from [13,21] and presented for velocity-controlled teleoperation system as in

$$\begin{bmatrix} v_s(t) \\ \omega_s(t) \end{bmatrix} = \begin{bmatrix} u_{sd}(t) \\ u_{so}(t) \end{bmatrix} - \mathbf{E}(b) \begin{bmatrix} v_{rd}(t) - v_r(t) \\ v_{ld}(t) - v_l(t) \end{bmatrix} \quad (3)$$

where  $v_s(t)$  and  $\omega_s(t)$  represent the measured linear and angular velocities of the WMR, respectively.  $u_{sd}(t)$  and  $u_{so}(t)$  represent the desired linear and angular velocities of the WMR, respectively.  $v_{rd}(t)$  and  $v_{ld}(t)$  are the right and left desired wheel velocities, respectively.  $v_r(t)$  and  $v_l(t)$  are the measured right and left wheel velocities, respectively. The transformation matrix is denoted as  $\mathbf{E}(b) = \begin{bmatrix} 1/2 & 1/2 \\ -1/(2b) & 1/(2b) \end{bmatrix}$ , where  $b$  is the distance between the right and the left wheels.

On soft terrains, like loose soil [14], the relationship between the linear velocity of each wheel and the product of the wheel's angular velocity and radius may not be valid due to wheel longitudinal slippage caused by terrian interaction forces [15]. Here we use (4) to describe the level of wheel slippage.

$$s_r(t) = \frac{v_{rd}(t) - v_r(t)}{v_r(t)}, \quad s_l(t) = \frac{v_{ld}(t) - v_l(t)}{v_l(t)} \quad (4)$$

where  $s_r(t)$  and  $s_l(t)$  represent the measured slippage of the right and left wheels, respectively. Note that we focus only on the case of  $v_{rd} \ge v_r$  in (4), corresponding to  $s_r \ge 0$ , to avoid non-passivity concerns arising from negative slippage. To solve this issue, a built-in feedforward controller (FFC) was adopted from [8] to compensate for the induced slippage and improve low-level command-tracking performance as expressed in (3). Now, the relationship between the WMR's linear and angular velocities is defined based on the induced velocity loss of the WMR adopted from [13]:

$$\begin{bmatrix} f_{ev}(t) \\ f_{eo}(t) \end{bmatrix} = \rho \begin{bmatrix} u_{sv}(t) - v_s(t) \\ u_{so}(t) - \omega_s(t) \end{bmatrix} = \rho \mathbf{E}(b) \begin{bmatrix} s_r(t)v_r(t) \\ s_l(t)v_l(t) \end{bmatrix} \quad (5)$$

where  $f_{ev}(t)$  and  $f_{eo}(t)$  are the slippage-based environmental force feedback on the longitudinal and angular velocity direction, and  $\rho$  is the damping coefficient of the soil. This force represents the friction loss exerted by the soft terrain on the wheel. The WMR is assumed to have a high-precision built-in velocity controller for each wheel motor, thus, the control input is denoted as  $u_s$  yielding the compressed form of (3) as in:

$$\xi_s(t) = u_s(t) - f_e(t) \quad (6)$$

where  $\xi_s = [v_s \quad \omega_s]^T$ . Refer to [15,21] for more details.

The kinematic and dynamics models are presented in this section to define the position-velocity coordination between the master and slave robots, ensuring synchronization of motion intentions rather than direct force interactions. This methodology is well-established in the bilateral teleoperation system [8,12–14,20]. Additionally, this model enables the extraction of terrain-induced velocity loss for the kinematic control, which acts as an indirect effective representation of slippage-induced force loss. This velocity loss is both measurable and intuitive, making it particularly suitable to generate force feedback for effective operator slippage awareness. Notably, in prior work [15], an approximate dynamic model of a WMR on soft terrain was developed, demonstrating that the velocity loss serves as a practical approximation of the slippage-induced force loss. Furthermore, it was shown that this force loss is generally non-intuitive for human operators and cannot be directly measured, as it occurs internally at the wheel-terrain interface. However, it is important to note that the full dynamic behavior of the WMR and its interaction with soft terrain are modeled using the Vortex Studio physics engine for the evaluation and validation of the proposed WMR control. This makes them especially valuable for validating the proposed kinematic control of WMR strategies in realistic soft terrain scenarios.

### 2.3. Designed bilateral teleoperator controllers

Existing proportional-derivative (PD) controllers [20] have established a stable position-velocity mapping coordination between the master and the slave robot expressed in (7), as represented by the red lines in Fig. 2 and referred to as the delayed case [28]. The joint control input  $u_m$  coordinates  $(x_{mv}, v_s)$  and  $(x_{mo}, \omega_s)$  at the operator station, whereas the control input  $u_s$  coordinates  $(x_{mv}, v_s)$  and  $(x_{mo}, \omega_s)$  at the remote environment.

$$\begin{aligned} u_m(t) &= -k_m (f_e(t - T(t))) - d_m x_m(t) \\ u_s(t) &= k_s (x_m(t - T(t))) - d_s \xi_s(t) \end{aligned} \quad (7)$$

where  $(k_s, k_m)$  and  $(d_s, d_m)$  represent the proportional and derivative gains respectively, and  $T$  denotes the large delays. In the master controller  $u_m(t)$ , the term  $-k_m (f_e(t - T(t)))$  represents the proportional control action, which scales the error signal between the desired and the actual state  $(x_m(t - T(t)) - \xi_s(t))$ . On the other hand, the term  $-d_m x_m(t)$  represents the derivative control action, which acts as a damper to resist changes in the commands, thus stabilizing the system. A similar principle applies to the slave controller  $u_s(t)$ . However, the force transparency of the PD-based teleoperation system is significantly undermined by the derivative gains in satisfying stability conditions [20].

To address this limitation, we designed predictor-based teleoperator controllers in the previous work [21] to ensure a stable system with good tracking performance and force transparency without the need for derivative gains under the large delay  $T$ , as expressed in (8). This approach is represented by the green lines in Fig. 2 and is referred to as the predicted case (ours).

$$\begin{aligned} u_m(t) &= -k_m (\hat{f}_e(t)) \\ u_s(t) &= k_s (\hat{x}_m(t)) \end{aligned} \quad (8)$$

where the forward predictor  $\hat{x}_m(t)$  and the backward predictor  $\hat{f}_e(t)$  are outputs of the PILSTM framework designed in Section 3 and implemented in Section 4. The absolute stability condition of the closed-loop teleoperation system derived in the previous work [21] is given by

$$d_m \ge k_m, \quad d_s \ge 0, \quad k_m, k_s > 0 \quad (9)$$

Therefore, in the proposed bilateral teleoperation system in Fig. 2, if the desired linear velocity  $x_{mv}(t)$  is greater than the actual linear velocity  $v_s(t)$ , a push force will be felt by the operator that pushes back on the master robot joint 1. Similarly, for any negative difference in angular velocities  $x_{mo}(t)$  and  $\omega_s(t)$ , a push force will be felt on joint

2. Conversely, if the desired linear velocity  $x_{m0}(t)$  is smaller than the actual linear velocity  $v_s(t)$ , a pull force will be felt by the operator that pulls the master robot joint 1 forward. Likewise, for any positive difference in angular velocities  $x_{m0}(t)$  and  $\omega_s(t)$ , a pull force will be felt on joint 2 [14]. This approach proves to be effective in conveying the slippage to the operator [21].

### 2.4. Proposed bilateral teleoperation hypothesis

As the proposed PiLSTM predictor-based controller well compensates for the large delays  $T$  and achieves high-fidelity closed-loop integration while maintaining overall system stability, the transparency (force feedback tracking) of the teleoperation system improves as expressed in (10) at any time step  $t$ .

$$f_h(t) \xrightarrow{T \to 0} f_e(t) \quad (10)$$

This indicates that the operator can accurately perceive the environmental force feedback, thereby achieving high transparency. Moreover, satisfying the condition in (10) enhances slippage compensation by the FFC. Consequently, the command-tracking performance in (6) becomes ideal in (11), ensuring high-fidelity closed-loop integration.

$$\xi_s \xrightarrow{f_e \to 0} u_s(t) \quad (11)$$

To summarize the role of slippage in the overall bilateral teleoperation system, it is explicitly considered in the control design through the following ways:

- Estimation of wheel–terrain interaction through kinematics, using the deviation between desired and actual wheel velocities.
- Generation of intuitive interaction force feedback to enhance operator slippage awareness, based on terrain-induced velocity loss.
- Real-time delay compensation at both the master and slave control levels, through PiLSTM-based feedback prediction to the operator and the local FFC.

## 3. Proposed PiLSTM-based predictor framework design

The general state space form of the conventional FOD predictor implemented in the previous work [20] was developed based on the first-order time-delay dynamics, as described in

$$\begin{aligned} \dot{y}_p(t) &= \dot{y}(t-T(t)) + \beta [y(t-T(t)) - y(t-T(t))] \\ &+ \alpha [\dot{y}(t-T(t)) - \dot{y}_p(t-T(t))], \end{aligned} \quad (12)$$

$$\dot{y}(t) = y_p(t).$$

the predictor, (12), incorporates the actual state  $y(t-T(t))$  and its derivative  $\dot{y}(t-T(t))$  at a previous time step  $t-T$ ; the predicted state  $y_p(t-T(t))$  and its derivative  $\dot{y}_p(t-T(t))$  at the same previous time step  $t-T$ ; and the predicted state  $y_p(t)$  at the current time step  $t$ , to estimate the predicted undelayed state  $\hat{y}(t)$ , which approximates the true state  $y(t)$ . The performance of the FOD predictor is adjusted using the regularization parameters  $\beta$  and  $\alpha$  for a specific delay  $T$ . Details of the predictor open-loop and closed-loop stability analysis can be found in [21,40]. The variable  $y$  can represent any of the coupling variables (i.e.,  $x_m, f_e$ ).

The primary limitation of the above FOD predictor dynamics lies in their failure to capture the complex nonlinear and temporal dynamic behaviors of the delayed coupling variable, significantly compromising the prediction performance [21]. We offer a promising solution to address this limitation by implementing a new LSTM-based predictor for delay compensation. These predictors, as proven in [48], are effective at learning strong nonlinear and temporal dynamics behaviors, thus making them ideal tools for modeling highly nonlinear and time-dependent systems. Nonetheless, pure LSTM networks often

struggle with generalization to unknown data in highly complex dynamic systems. Capitalizing on this, we integrate physical constraints based on FOD dynamics in (12) with a feedback-driven refinement mechanism into our LSTM-based predictor design to create a new physics-informed LSTM (PiLSTM) predictor. The feedback mechanism forms a closed-loop predictor structure where the predictor learns an implicit correction from its own past predictions to adapt well to varying dynamics and refines its future predictions. Two distinct PiLSTM predictors: a forward predictor tailored to predict motion commands  $\hat{x}_m(t)$  and a backward predictor tailored to force feedback  $\hat{f}_e(t)$ , together form PiLSTM predictor framework, as in Fig. 2.

### 3.1. Problem definition

The proposed predictor is utilized to estimate the undelayed variables from their corresponding delayed variables. The proposed models aim to perform single-step predictions of the coupling variables, particularly in the context of a track-following task. Accurate single-step predictions are crucial for maintaining performance in the track-following task. The problem can be defined as:

$$\mathcal{H}_\Theta(X_t, X_{t-1}, X_{t-2}, \dots, X_{t-n}) = Y_{t+1}, \quad (13)$$

where  $\mathcal{H}_\Theta$  denotes the PiLSTM network with parameters  $\Theta$ , mapping the sequence inputs  $(X_t, X_{t-1}, X_{t-2}, \dots, X_{t-n})$  to a single output  $Y_{t+1}$ , where  $n$  is the predetermined input sequence length. Each input vector is defined as  $X = [y(t-T), y_p(t-T), \dot{y}(t-T), \dot{y}_p(t-T)]$  and corresponds to the one-step ahead actual output  $Y = y(t)$ . It is worth noting that the variable  $y_p$  represents the delayed predicted state used for the feedback refinement mechanism. The variable  $y$  can represent any of the coupling variables of interest (i.e.,  $x_m, f_e$ ).

### 3.2. Data and preprocessing

The dataset was collected from human-in-the-loop experiments conducted using the developed teleoperation test platform, as detailed in Section 4. It comprises delayed data of the key coupling variables in the teleoperation system, acquired through the proposed data collection framework illustrated in Fig. 3. The dataset covers diverse scenarios, including varying track patterns, operator expertise levels, and terrain inclinations. Data collection began by recording motion commands  $x_m(t)$  and force feedback signals  $f_e(t)$ , sampled at 10 Hz. These data comprise five essential variables for each coupling variable: the undelayed actual value  $y(t)$ , the delayed actual value  $y(t-T)$ , the precomputed delayed predicted value  $y_{p,p}(t-T)$ , the derivative of the delayed actual value  $\dot{y}(t-T)$ , and the derivative of the precomputed delayed predicted value  $\dot{y}_{p,p}(t-T)$ . The delayed predicted states are assumed to be available and are utilized as dynamic feedback-aware inputs, enabling the predictor to adaptively refine its estimates based on recent temporal behavior. Collectively, these variables capture the underlying complexity and temporal dependencies necessary for accurate modeling in delayed data.

The training dataset was recorded from three randomly selected operators with a sampling rate of 10 Hz for a total simulation time of 300 s (comprising about 3000 acquisitions). For the testing datasets, three sets were collected from different operators and tracks, with each testing dataset maintaining the same sampling rate as the training set but spanning a shorter simulation duration of 30 s. Furthermore, the training dataset was further partitioned into two distinct segments for training and validation purposes, in the ratio of 70% to 30%, respectively. Each segment contains the input features  $y(t-T)$ ,  $y_p(t-T)$ ,  $\dot{y}(t-T)$ , and  $\dot{y}_p(t-T)$ , and the target output feature  $y(t)$ , which represents the ground truth value that the model aims to learn and predict. Additionally, the input features were preprocessed through normalization and scaling to ensure homogeneity among variables during training, following the approach described in [48].

![Figure 3: Data collection framework for generating delayed data. A 'Teleoperation Test platform' block outputs a 'Coupling Variable' y(t). This signal is fed into four parallel processing paths: 1) A Gaussian noise generator N(0, sigma^2) followed by an exponential decay e^{-T(t)t} to produce y_{pp}(t - T(t)). 2) A direct path for y(t - T(t)). 3) A differentiation block d/dt followed by an exponential decay e^{-T(t)t} to produce y_dot(t - T(t)). 4) A Gaussian noise generator N(0, sigma^2) followed by an exponential decay e^{-T(t)t} to produce y_dot_{pp}(t - T(t)). All four paths converge into a 'Time-Stamped Sequence Buffer' containing features [y_i, y_{i-1}, ..., y_{i-n}]. This buffer then feeds into a 'Data Logger'.](a738993919a50143787084ee7ce6e2f2_img.jpg)

Figure 3: Data collection framework for generating delayed data. A 'Teleoperation Test platform' block outputs a 'Coupling Variable' y(t). This signal is fed into four parallel processing paths: 1) A Gaussian noise generator N(0, sigma^2) followed by an exponential decay e^{-T(t)t} to produce y\_{pp}(t - T(t)). 2) A direct path for y(t - T(t)). 3) A differentiation block d/dt followed by an exponential decay e^{-T(t)t} to produce y\_dot(t - T(t)). 4) A Gaussian noise generator N(0, sigma^2) followed by an exponential decay e^{-T(t)t} to produce y\_dot\_{pp}(t - T(t)). All four paths converge into a 'Time-Stamped Sequence Buffer' containing features [y\_i, y\_{i-1}, ..., y\_{i-n}]. This buffer then feeds into a 'Data Logger'.

**Fig. 3.** The proposed data collection framework for generating delayed data within the test platform. Here,  $y \in \{x_{mv}, \dot{x}_{mv}, f_{ev}, \dot{f}_{ev}\}$ , where  $y(t)$  is the target output feature and  $y(t - T(t)), y_{pp}(t - T(t)), \dot{y}(t - T(t)), \dot{y}_{pp}(t - T(t))$  are the input features.

![Figure 4: PILSTM network architecture. The main 'Deep Neural Network (DNN)' (blue dashed box) consists of an 'Input layer' (green dashed box) receiving 'Input features' Y_{n-1} and 'Delayed prediction' Y_{n-1}. These are concatenated and passed through a 'Dense layer' (orange) with m units, followed by 'Relu layer' (grey) and 'LSTM layer #1' (blue) with l units. This is followed by 'LSTM layer #k' (blue) with l units, another 'Dense layer' (orange) with m units, and a final 'Relu layer' (grey). The 'Output layer' (green dashed box) produces the predicted value Y_n. A 'Feedback refinement path' (dark green) takes Y_n and feeds it back into the input. 'FOD dynamic constraints' (green dashed box) include a 'Differential operator' (d/dt) and a 'DDE constraint' block (R). The 'Optimization process' (yellow box) calculates the loss function L(theta) = L_d(theta) + lambda L_p(theta) and updates parameters theta* = min L(theta).](49ee89a1d5852ab005dbbab6de09a8a6_img.jpg)

Figure 4: PILSTM network architecture. The main 'Deep Neural Network (DNN)' (blue dashed box) consists of an 'Input layer' (green dashed box) receiving 'Input features' Y\_{n-1} and 'Delayed prediction' Y\_{n-1}. These are concatenated and passed through a 'Dense layer' (orange) with m units, followed by 'Relu layer' (grey) and 'LSTM layer #1' (blue) with l units. This is followed by 'LSTM layer #k' (blue) with l units, another 'Dense layer' (orange) with m units, and a final 'Relu layer' (grey). The 'Output layer' (green dashed box) produces the predicted value Y\_n. A 'Feedback refinement path' (dark green) takes Y\_n and feeds it back into the input. 'FOD dynamic constraints' (green dashed box) include a 'Differential operator' (d/dt) and a 'DDE constraint' block (R). The 'Optimization process' (yellow box) calculates the loss function L(theta) = L\_d(theta) + lambda L\_p(theta) and updates parameters theta\* = min L(theta).

**Fig. 4.** Our PILSTM network architecture for the proposed predictor with the feedback refinement path in dark green. The network parameters includes: number of fixed-length input sequence  $n$ , number of dense layer hidden units  $m$ , number of LSTM layers  $k$ , number of LSTM layer hidden units  $l$ , and a single-step target output at  $n$ . (For interpretation of the references to colour in this figure legend, the reader is referred to the web version of this article.)

### 3.3. Model development

Here, we discuss the detailed design of the four distinct models (predictors), each tailored to one of the four coupling variables of the bilateral teleoperation system. These include the desired linear velocity  $x_{mv}(t)$ , desired angular velocity  $x_{mo}(t)$ , longitudinal force feedback  $f_{ev}(t)$ , and angular force feedback  $f_{eo}(t)$ .

#### 3.3.1. Network architecture

The architecture of our PiLSTM network is designed to handle non-linear and time-dependent data, similar to the architecture proposed in [51]. The network is composed of an input layer, a dense layer, an activation layer, LSTM layers, an output layer, and physical constraint integration, as depicted in Fig. 4. Each LSTM layer captures different levels of abstraction within the sequence data.

The input layer receives the input sequence, composed of a feature vector of fixed length, denoted as  $(X_1, X_2, \dots, X_n)$ , where each  $X_i$  is defined as  $X_i = [y(t_i - T), y_{pp}(t_i - T), \dot{y}(t_i - T), \dot{y}_{pp}(t_i - T)]$  for  $i = 1, \dots, n$ . Each LSTM layer consists of multiple recurrent units that share internal parameters, each employing a sigmoid activation function  $\sigma$  for gate operations and a hyperbolic tangent  $\tanh$  for updating cell

states. Its unique recurrent structure propagates hidden and cell states across time steps, enabling the network to capture long-term temporal dependencies within the input sequence. The output layer produces single-step predicted values, represented by  $\hat{Y}_n$ , where  $\hat{Y} = \hat{y}(t_i) = y_p$ . Thus, each of our four models shares the same architectural structure but may vary in the number of layers and units according to their complexity.

#### 3.3.2. Integration of FOD dynamics with embedded feedback refinement

Following the architectural design, we now define the method for optimizing network parameters  $\Theta$ . For this, the optimization problem is formulated as:

$$\Theta^* = \min \mathcal{L}(\Theta) \quad (14)$$

where  $\mathcal{L}$  represents a custom loss function, which must be differentiable with respect to its parameters. In neural networks addressing this kind of regression problem, the mean absolute error is the most commonly used for data loss given by

$$\mathcal{L}_d(\Theta) = \frac{1}{N} \sum_{i=1}^{N} |\hat{y}(t_i) - y(t_i)| \quad (15)$$

where  $N$  represents the total number of samples in a run. This loss function is selected due to its robustness against outliers. To further guide the learning process, physical constraints are introduced by enforcing delay differential equations (DDEs) into the optimization process. By employing the method in [52] to approximate the temporal derivative of past states on the right-hand side of the FOD dynamics in (12), it is transformed into a standard DDE. This results in the compact DDE form shown in (16), with  $\psi(t) = t - T$ . In turn, the loss function assimilates the DDE constraint, which introduces a soft regularization in the optimization process to ensure compliance with known delayed dynamics. Thus, the physics-informed loss is defined based on the L2-norm of the DDE residual, as presented in (17).

$$\begin{aligned}\dot{y}_p(t) &= F(t, y(\psi(t)), \dot{y}_p(\psi(t))) \\ \hat{y}(t) &= y_p(t)\end{aligned}\quad (16)$$

$$\mathcal{L}_p(\Theta) = \frac{1}{M} \sum_{j=1}^{M} \left\| \dot{\hat{y}}(t_j) - F(t_j, y(\psi(t_j)), \dot{y}_p(\psi(t_j))) \right\|^2 \quad (17)$$

where  $M$  represents the number of collocation points where the DDE constraint is enforced, where the predictor uses its past outputs,  $y_p(\psi(t_j))$ , as part of the input for future predictions and iteratively refines its estimates. The overall cost function  $\mathcal{L}(\Theta)$  is a weighted sum of the two loss terms, i.e.,  $\mathcal{L}_d(\Theta)$  and  $\mathcal{L}_p(\Theta)$ , and is minimized with respect to the network parameters  $\Theta$  during the training process, as in (18). By optimizing this loss, the network learns a model  $H_\Theta$  that not only fits the observed data but also aligns with the specified dynamics of the system.

$$\mathcal{L}(\Theta) = \mathcal{L}_d(\Theta) + \lambda \mathcal{L}_p(\Theta) \quad (18)$$

The coefficient  $\lambda$  in the total loss function  $L(\Theta)$  serves as a regularization hyperparameter that controls the balance between data fitting and physical constraint adherence during training as depicted in Fig. 4. A high value of  $\lambda$  places more emphasis on physical consistency, potentially sacrificing some data fit to ensure the model adheres to known dynamics. Conversely, a low value of  $\lambda$  prioritizes minimizing the data loss at the cost of potentially violating the system's physical behavior. The optimal value of  $\lambda$  is typically determined through cross-validation or grid search, ensuring a trade-off that best generalizes the model to unseen data and dynamics [54].

Apart from enforcing delayed dynamics DDE constraints from the back end, such as in standard PiLSTM, our PiLSTM uniquely embeds a closed-loop feedback mechanism directly into the network architecture to refine predictions from the front end. At each timestep, the network feeds back its delayed prediction  $y_p(t-T(t))$  and its derivative  $\dot{y}_p(t-T(t))$  as additional input features to the PiLSTM network, as described by:

$$\begin{aligned}y_p(t_i - T(t_i)) &= (1 - \beta) \cdot \hat{y}(\psi(t_i)) + \beta \cdot y_{p,p}(t_i - T(t_i)) \\ \dot{y}_p(t_i - T(t_i)) &= (1 - \beta) \cdot \dot{\hat{y}}(\psi(t_i)) + \beta \cdot \dot{y}_{p,p}(t_i - T(t_i))\end{aligned}\quad (19)$$

where  $\hat{y}(t - T(t))$  and  $\dot{\hat{y}}(t - T(t))$  are the delayed model prediction and its derivative at a previous timestep. The feedback blending coefficient,  $\beta$ , typically decaying over training epochs (e.g.,  $\beta = \max(0, 1 - \text{epoch}/\text{total\_epochs})$ ). This structural feedback loop enables the network to learn implicit corrections from its past predictions and evolving dynamic behavior, thereby allowing it to adapt to varying dynamics and refine future predictions without solely relying on static regularization of the physical constraints. As such, the process during the optimization is described as:

- Hybrid collocation learning: reduced physical model error by enforcing FOD dynamics at  $M$  collocation points via  $\mathcal{L}_p$
- Recursive feedback loop: reduced temporal variation error by re-ingesting past predictions at  $N$  sample points.

Together, this allows the network to learn consistent temporal-spatial dynamics in the variable-delayed data. In addition, this embedded feedback structure is inherently suited for adaptive online

prediction, where past predictions are utilized to refine future predictions based on evolving temporal behavior in real-time (e.g., like a Kalman filter update), without requiring retraining or external compensation. This enhances the model's robustness and adaptability to variable delays in real-world scenarios.

#### 3.3.3. Training

Training for each predictor begins with a time-series window of 50 data points (equivalent to 5 s of history) for each model. This predetermined sequence length, denoted as  $n$ , serves as the input vector for the network. The training is conducted offline using the preprocessed dataset of delayed coupling variables acquired from the teleoperation experiments. During this training, the network parameters undergo iterative refinement through an optimization routine predicated on a composite loss function, as delineated in (18). Back-propagation Through Time (BPTT) is applied to compute the parameter gradients, and the Adam optimizer is used to update the network parameters due to its stable convergence behavior and adaptive learning rate mechanism. Algorithm 1 outlines the pseudo-code of the training process and the computational steps involved in model learning.

##### Algorithm 1 Our Developed PiLSTM Training Pseudo Code

```

1: INPUT:  $X = [X_1, \dots, X_n]$ , each  $X_i = [y(t-T(t)), y_{p,p}(t-T(t)), \dot{y}(t-T(t)), \dot{y}_{p,p}(t-T(t))] \in \mathbb{R}^n$ 
2: OUTPUT:  $Y = Y_n$ , where  $Y_n \in \mathbb{R}^n$ 
3: PARAMETERS:  $\Theta = [W_{in}, b_{in}, W_f, b_f, W_c, b_c, b_E, W_f, U_f, b_f, W_o, b_o, W_{out}, b_{out}]$ 
4: INITIALIZE: LSTM hidden state  $h_0 = \vec{0}$ , cell state  $c_0 = \vec{0}$ , learning rate  $\alpha$ , total loss weight  $\lambda$ 
5: DEFINE: differential operator  $D$ , DDE constraint  $\mathcal{R}$ , Blending coefficient  $\beta$ 
6: SETUP: initialize prediction buffers  $\mathcal{B}[t] = 0$ ,  $\dot{\mathcal{B}}[t] = 0$ 
7: TRAIN and VALIDATE ( $X_{train}, Y_{train}, X_{val}, Y_{val}, D, \mathcal{R}$ )
8: for each epoch do
9:    $\beta = \max(0, 1 - \text{epoch}/\text{total\_epochs})$ 
10:  for each batch ( $X_{batch}, Y_{batch}$ ) in ( $X_{train}, Y_{train}$ ) do
11:   Compute delay:  $\tau = t - T(t)$ 
12:   Retrieve prediction:  $\hat{y}(\tau) = \text{Interpolate}(\mathcal{B}, \tau)$ 
13:   Retrieve prediction derivative:  $\dot{\hat{y}}(\tau) = \text{Interpolate}(\dot{\mathcal{B}}, \tau)$ 
14:   Retrieve precomputed:  $y_{p,p}(\tau), \dot{y}_{p,p}(\tau)$ 
15:   Compute blended prediction using (19):  $y_{p,p}(\tau), \dot{y}_{p,p}(\tau) \leftarrow X_{batch}$ 
16:   New augmented input:  $X_{batch} = [y(t-T), y_p(\tau), \dot{y}(t-T), \dot{y}_p(\tau)]$ 
17:   Compute LSTM outputs for batch:  $H_{batch}$ 
18:   Compute Dense output for batch:  $\hat{Y}_{batch}$ 
19:   Apply  $D$  in (16) to get  $\dot{\hat{Y}}_{batch}$ 
20:   Compute data loss in (15):  $\mathcal{L}_d(\Theta) = f(\hat{Y}_{batch}, Y_{batch})$ 
21:   Compute FOD-physics loss in (17):  $\mathcal{L}_p(\Theta) = f(\dot{\hat{Y}}_{batch}, \mathcal{R}(Y_{batch}))$ 
22:   Compute total loss (18):  $\mathcal{L}(\Theta) = \mathcal{L}_d(\Theta) + \lambda \mathcal{L}_p(\Theta)$ 
23:   Update  $\Theta$  using gradient descent:
24:    $\Theta = \Theta - \alpha \nabla_{\Theta} \mathcal{L}(\Theta)$ 
25: end for
26: Take ( $X_{val}, Y_{val}$ )
27: Compute output for validation:  $\hat{Y}_{val}$ 
28: Compute validation loss:  $\left\| \hat{Y}_{val} - Y_{val} \right\|_2$ 
29: end for
30: CHECKPOINT:  $\Theta^* = \Theta_{best}$ 
```

The training was implemented using MATLAB's Deep Learning Toolbox in conjunction with the Parallel Computing Toolbox to accelerate computation and efficiently utilize available GPU resources. The computational complexity of the proposed PiLSTM network architecture in Fig. 4 is quantified in terms of per-iteration cost using the multiply-accumulate operation count (MAC) [56,57].

$$\text{Cost per iteration} = \mathcal{O}(n f m + n k l^2 + n k l m + n l m + n p) \quad (20)$$

**Table 1**  
Optimal Hyperparameters with their corresponding Cost per iteration for the Predictors.

| Coupling Variables | Initial Learn Rate | Dense Hidden Units, $m$ | LSTM Depth, $k$ | LSTM Hidden Units, $l$ | Threshold | Forward MACs ( $\times 10^6$ ) |
|--------------------|--------------------|-------------------------|-----------------|------------------------|-----------|--------------------------------|
| $x_{mv}$           | 0.00230            | 118                     | 2               | 162                    | 0.11      | 5.523                          |
| $x_{mo}$           | 0.00016            | 174                     | 3               | 179                    | 0.97      | 11.078                         |
| $f_{ev}$           | 0.00095            | 151                     | 2               | 188                    | 0.95      | 7.822                          |
| $f_{eo}$           | 0.00076            | 207                     | 3               | 207                    | 0.95      | 13.38                          |

where  $n$  is the sequence length,  $f$  is the input features dimensionality,  $m$  is the width of the dense layers (input and output),  $k$  is the number of LSTM layers,  $l$  is the size of each LSTM units, and  $p$  is the cost of the differential operator per time step. In practice, if  $p \ll l^2$ ,  $l m$ , the LSTM term dominates and  $T \cdot p$  becomes insignificant. This training procedure is computationally efficient and typically completes within a few minutes on modern GPU-equipped platforms. The forward-pass MACs per iteration for the four trained predictors is summarized in Table 1. These MACs values are directly linked to the computational demand during inference, as the inference time quantifies the duration required to complete a forward-pass MACs operation [58]. The inference time (lower-bound latency) can be computed as:

$$\text{Inference Time} = \frac{\text{MACs per iteration}}{\text{Compute Throughput (MACs per sec)}} \quad (21)$$

Where MACs per iteration is the forward MACs to process a single input (as reported in Table 1), Compute Throughput (also referred to as the MAC rate) is the number of MAC operations the system can perform per second, typically dependent on the hardware specifications such as the GPU or CPU [56].

For our experiments, the predictor inference was executed on the workstation (AMD Ryzen™ 5 5600H, NVIDIA GeForce RTX 3050 GPU), whose compute throughput is commonly expressed in GFLOPs (Giga Floating-Point Operations per Second). The theoretical GFLOPs can be computed using:  $\text{GFLOP} = (\text{Clock Rate} \times \text{CUDA Cores} \times 2)$ , where Clock Rate is the GPU's clock rate in GHz (1.21 GHz), the Multiprocessor Count is 16, and the CUDA Cores per Multiprocessor for RTX 3050 is typically 128. Thus, the total number of CUDA cores is  $16 \times 128 = 2048$ . Thus, the computed GFLOPs is 4936 GFLOPs (MACs per sec). Overall, the inference time for the trained predictors are computed to be ( $\tau_{x_{mv}} = 1.12$  ms,  $\tau_{x_{mo}} = 2.24$  ms,  $\tau_{f_{ev}} = 1.57$  ms,  $\tau_{f_{eo}} = 2.71$  ms) as the lower-bound latencies on NVIDIA GeForce RTX 3050 GPU.

To evaluate deployment feasibility in resource-constrained systems, we assess the inference performance on a real-world teleoperation platform — the EML Rashid-1 — equipped with an NVIDIA Jetson Nano (128-core Maxwell GPU, 472 GFLOPs peak throughput, 921 MHz clock speed) [16]. Under this hardware configuration, the estimated inference times become: ( $\tau_{x_{mv}} = 11.71$  ms,  $\tau_{x_{mo}} = 23.5$  ms,  $\tau_{f_{ev}} = 16.57$  ms,  $\tau_{f_{eo}} = 28.3$  ms). This confirms that the trained predictors can well compensate for teleoperation delays above 200 ms, typically encountered in real-world teleoperation applications [3].

#### 3.3.4. Hyperparameter tuning

Bayesian optimization is employed to determine optimal hyperparameters for each network model. Table 1 summarizes the optimal hyperparameters as obtained for each of the four distinct predictors.

### 3.4. Predictor evaluation

During the training process, our methodology entailed a comprehensive evaluation of various architectures, including the proposed PiLSTM with and without the feedback mechanism, and the pure LSTM [45,46,50,53], to identify the best-performing predictor. For rigorous validation of the proposed predictors, we utilized testing datasets that were entirely distinct from those used during the training phase. This was done to demonstrate the effectiveness of the PiLSTM predictors in terms of adaptability and generalizability on previously unseen delayed data. To assess potential overfitting and evaluate the predictive performance,

the developed models were quantitatively assessed using the root mean square error (RMSE) [53], which is defined as:

$$RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (\hat{y}(t_i) - y(t_i))^2} \quad (22)$$

where  $N$  represents the total number of samples within the dataset. The evaluation was conducted offline, allowing for a comprehensive analysis of the predictors' performance without the constraints of real-time processing. This setup enables efficient and detailed benchmarking of the proposed PiLSTM predictors. The performance results of the proposed models and baseline benchmarks are summarized in Table 2.

The error analysis in Table 2 reveals that the average generalization error for  $x_m$  (i.e., 23.9% for PiLSTM<sub>+</sub>) is consistently lower than that for  $f_e$  (i.e., 33.6% for PiLSTM<sub>+</sub>), indicating that the predictors are more effective at predicting motion commands than force feedback. This disparity may be attributed to the inherent characteristics of the data, where motion commands follow more regular and predictable patterns, while force feedback exhibits greater complexity and variability. Although the pure LSTM model achieves the lowest training error, it suffers from substantially higher testing errors, consistent with prior observations in [45,51,53]. In contrast, PiLSTM<sub>+</sub> consistently outperforms both PiLSTM<sub>-</sub> and the standard LSTM across all test datasets for both  $x_m$  and  $f_e$ , as evidenced by its lower RMSE values. Furthermore, PiLSTM<sub>+</sub> demonstrates the smallest variation in testing error across the three datasets, indicating superior generalization and adaptability to diverse variable delayed data. On the other hand, the LSTM hybrid exhibits the highest testing errors overall. Notably, Test 2 yields the most accurate predictions across all models, while Test 3 consistently results in the poorest performance. This trend suggests that the proximity of testing data to the training distribution significantly influences predictor performance, as also reported in [45]. The overall generalization error for PiLSTM<sub>+</sub> is  $34.61 \times 10^{-3}$ , compared to  $55.22 \times 10^{-3}$  for PiLSTM<sub>-</sub>, and  $86.81 \times 10^{-3}$  for the pure LSTM. These clearly demonstrate performance improvements of 37.32% and 60.13%, respectively, which are attributed to the feedback-integrated architecture of PiLSTM<sub>+</sub>. Overall, the PiLSTM<sub>+</sub> architecture exhibits greater robustness and generalization than both PiLSTM<sub>-</sub> and the pure LSTM, consistently delivering the most accurate and adaptable predictions across all four coupling variables:  $x_{mv}(t)$ ,  $x_{mo}(t)$ ,  $f_{ev}(t)$ , and  $f_{eo}(t)$ . This improvement is primarily attributed to the integration of the feedback refinement mechanism, which allows the predictor to adapt to variations in delay dynamics. As a result, PiLSTM<sub>+</sub> is the most suitable candidate for deployment in real-time teleoperation systems.

## 4. Human-in-the-loop experiment

Human-in-the-loop experiments, as described in [15,20,41] were performed on a test platform to evaluate the effectiveness of our developed PiLSTM-based predictor framework for teleoperated WMRs on soft terrain under large delays.

### 4.1. Test platform

A real-time human-in-the-loop test platform was developed by integrating a Touch X haptic device with MATLAB/Simulink, Vortex Studio simulator, and a high-performance workstation (AMD Ryzen™ 5 5600H CPU, 16 GB of RAM, and an NVIDIA GeForce RTX 3050 Laptop GPU

**Table 2**  
RMSE metrics for different predictor network architectures.

| Coupling Variables | Features/ Target | Predictor Architecture | Train RMSE $\times 10^{-3}$ | Test #1 RMSE $\times 10^{-3}$ | Test #2 RMSE $\times 10^{-3}$ | Test #3 RMSE $\times 10^{-3}$ |
|--------------------|------------------|------------------------|-----------------------------|-------------------------------|-------------------------------|-------------------------------|
| $x_{mv}$           | 1                | PiLSTM <sub>+</sub>    | 3.04                        | 3.71                          | 3.26                          | 3.86                          |
|                    | 2                | PiLSTM <sub>-</sub>    | 2.93                        | 7.49                          | 6.84                          | 8.84                          |
|                    | 3                | LSTM                   | 3.97                        | 14.36                         | 14.97                         | 15.91                         |
| $x_{mo}$           | 1                | PiLSTM <sub>+</sub>    | 50.7                        | 65.9                          | 62.1                          | 68.3                          |
|                    | 2                | PiLSTM <sub>-</sub>    | 48.2                        | 93.1                          | 87.2                          | 97.6                          |
|                    | 3                | LSTM                   | 56.5                        | 107.2                         | 129.9                         | 134.6                         |
| $f_{ev}$           | 1                | PiLSTM <sub>+</sub>    | 16.3                        | 21.4                          | 19.9                          | 25.6                          |
|                    | 2                | PiLSTM <sub>-</sub>    | 15.2                        | 44.8                          | 35.5                          | 47.7                          |
|                    | 3                | LSTM                   | 15.9                        | 65.2                          | 64.9                          | 76.5                          |
| $f_{eo}$           | 1                | PiLSTM <sub>+</sub>    | 36.1                        | 47.9                          | 42.1                          | 51.3                          |
|                    | 2                | PiLSTM <sub>-</sub>    | 35.4                        | 69.7                          | 74.8                          | 88.1                          |
|                    | 3                | LSTM                   | 39.0                        | 128.7                         | 134.9                         | 154.6                         |

Feature/Target Set Legend:

<sup>1</sup>  $y(t-T(t)), \hat{y}(t-T(t)), \dot{y}(t-T(t)), \dot{\hat{y}}(t-T(t)) \to y(t)$  (used in PiLSTM<sub>+</sub>): with feedback mechanism

<sup>2</sup>  $y(t-T(t)), \hat{y}(t-T(t)) \to y(t)$  (used in PiLSTM<sub>-</sub>): without feedback mechanism

<sup>3</sup>  $y(t-T(t)), \hat{y}(t-T(t)) \to y(t)$  (used in LSTM): without feedback mechanism and FOD constraints

![Diagram of the Human-in-the-loop test platform for remote teleoperation of a WMR. The diagram shows three main components: Operator Station, Virtual Environment, and Comm. Channel. The Operator Station includes a trained operator using a touch X device, high-level slippage compensation, and a visual interface. The Virtual Environment includes a wheeled robot (WMR) on soft terrain, slippage estimation, FFC controller, and a mast-mounted camera. The Comm. Channel includes a haptic interface, UDP receive and send, network delays, and the PiLSTM Predictor Framework. A Camera Field View shows the WMR's perspective camera view. The WMR (Rashed Rover) is shown in a virtual environment with slippage indicators: Low-slippage, Moderate-slippage, High-slippage, and Lose self. Slippage is also indicated on the ground: Left wheel slippage, Right wheel slippage, and All wheels slippage.](54fabc351eda5228d2fa28cd9ba07971_img.jpg)

Diagram of the Human-in-the-loop test platform for remote teleoperation of a WMR. The diagram shows three main components: Operator Station, Virtual Environment, and Comm. Channel. The Operator Station includes a trained operator using a touch X device, high-level slippage compensation, and a visual interface. The Virtual Environment includes a wheeled robot (WMR) on soft terrain, slippage estimation, FFC controller, and a mast-mounted camera. The Comm. Channel includes a haptic interface, UDP receive and send, network delays, and the PiLSTM Predictor Framework. A Camera Field View shows the WMR's perspective camera view. The WMR (Rashed Rover) is shown in a virtual environment with slippage indicators: Low-slippage, Moderate-slippage, High-slippage, and Lose self. Slippage is also indicated on the ground: Left wheel slippage, Right wheel slippage, and All wheels slippage.

**Fig. 5.** Human-in-the-loop test platform for remote teleoperation of a WMR traversing soft terrain under dynamic slippage, with operator awareness of slippage conditions.

with 4 GB VRAM, a Dell 32" S3222DGM Curved Gaming Monitor). This test platform enables teleoperation of a WMR on soft terrain that reproduces real-world slippage and potential tip-over scenarios on inclined surfaces, as shown in Fig. 5. The choice of Vortex Studio was based on previous work in [14,21], which demonstrated its high-fidelity and realistic simulation of terrain responses, reducing the reliance on classical analytical modeling. Moreover, the dynamic wheel–terrain interactions were experimentally validated in the previous work [7].

The operator station is equipped with a Touch X haptic device to generate motion commands and perceive slippage-based force feedback, as well as a virtual interface (monitor) to provide look-ahead visual feedback from the virtual environment. The device has three joints, with only the first two (1 & 2) activated for real-time operation, while the third is locked with a high-gain virtual constraint to encode non-holonomic driving commands and slippage awareness. The haptic device is connected as a force control interface to the virtual environment via a communication channel. To regulate the observed high-frequency commands and feedback, a first-order low-pass filter

with a cutoff frequency of 0.7 Hz is applied to the coupling variables to avoid exceeding the maximum effective predictor bandwidth of 0.8 Hz.

The virtual environment, created in Vortex Studio, receives motion commands from the operator station to control the WMR. The WMR model is based on a high-fidelity 3D representation of the Rashid rover in Vortex Studio, equipped with a differential drive kinematic model, terra-mechanic models, an inertial measurement unit (IMU), wheel encoders, a feedforward controller [8], and a mast-mounted perspective camera. The physical configuration of the WMR includes a total mass of 20 kg, wheel radius of 0.1 m, wheelbase of 0.28 m, track width of 0.25 m, and a mast height of 0.56 m. The moments of inertia are internally computed by the physics engine based on the mesh geometry. Moreover, the virtual environment itself incorporates a soft (deformable) terrain roadmap as detailed in Section 4.2, enabling simulation of slippage challenges. The FFC functions as an embedded low-level velocity controller that minimizes tracking error, while the mast-mounted camera provides visual cues of the look-ahead environment. Slippage is estimated using the velocity loss in (5), based on 

inputs from the IMU (located at the WMR's center of mass), wheel encoder data, and reference input commands. The estimated slippage is used to generate environmental force feedback, which is transmitted back to the operator station to provide real-time slippage awareness.

The communication channel enables bidirectional data exchange between the operator station and the virtual environment. It includes a network interface for transmitting motion commands from the operator station and receiving environmental force feedback from the virtual environment in real time. To account for inherent network delays and their fluctuations, a UDP-based communication protocol is implemented in Simulink, ensuring the timely delivery and synchronization of control and feedback signals. The haptic interface is supported by the QUARC toolbox, which generates motion commands from joint angle measurements and renders feedback forces to the device inputs. To enhance system performance and robustness under delay conditions, the communication channel incorporates a delay compensation framework based on the PILSTM predictors. This module compensates for the delay effects in both the transmitted motion commands and received force feedback signals.

The working principles of the developed test platform are summarized as follows:

- The operator sends motion commands and receives the WMR's responses in the form of slippage-based force feedback and forward-looking visual feedback.
- When the desired command exceeds the measured response (i.e., slippage), the operator experiences a push force on the haptic device joints, prompting a compensatory effort to counteract it. Conversely, when the desired command is equal to the measured response (i.e., pure rolling), no force is perceived by the operator, indicating ideal wheel–terrain interaction.
- The adverse effects of delayed force feedback, which results in delayed operator reactions and reduced situational awareness, is compensated by predicting the anticipated motion commands and force feedback, thereby restoring system fidelity.

It is worth noting that the force feedback scaling used in the test platform was based on an established methodology from previous research [8,12,13,20,21]. Specifically, we adopted the force feedback scaling approach from our prior work [20,21], which provides a well-tested framework for scaling slippage-based force feedback according to human perceptual thresholds. The master controller gains in (7) and (8) were used to scale the force feedback:  $k_m = 10$  and  $d_m = 10.5$ . This scaling was adopted directly to ensure that the intensity of the force feedback matched the operator's ability to perceive different levels of slippage, without overwhelming their control actions. This approach has been proven to be effective for conveying slippage feedback to operators in similar applications.

## 4.2. Experiment design

We designed a  $10\text{ m} \times 10\text{ m}$  virtual roadmap, in a virtual environment to simulate a diverse array of test tracks, to replicate lunar terrain conditions, as depicted in Fig. 6. These tracks simulate paths generated by a space path planner, guiding navigation from a designated start point to an end point. The roadmap consists of three distinct track patterns, labeled A, B, and C (shown in gray), which are designed as soft terrains, starting from the green mark (4.1, 0.1, 0.0) and ending at the red mark (−4.1, 0.1, 0.4), with a slope angle of  $8^\circ$ . Track A is a straight pattern, measuring 9 m in length and 2 m in width. Track B features right turns, while Track C includes both right and left turns. The non-track area (in brown) serves as a landmark, giving operators a visual cue for estimating distance to turns and relative speed. The safe speed on the tracks is predetermined as a maximum allowable linear velocity of  $0.1\text{ m/s}$  and an angular velocity of  $0.97\text{ rad/s}$  for a wheelbase of  $0.22\text{ m}$ , allowing the WMR to traverse soft terrain smoothly and safely.

The soft terrain tracks are implemented in the Vortex Studio physics engine using the terramechanics and deformable terrain modules [59]. Specifically, the Reece pressure–sinkage model and the Wong shear stress model are utilized to simulate the vertical resistance (normal pressure) and shear stress distribution (lateral displacement) from the dynamic interaction between the wheels and the soil [60,61]. The normal pressure beneath the wheels, based on the modified Reece model, is described by [7,59,60] as follows:

$$p(z) = (ck'_c + \gamma bk'_\phi) \left( \frac{z}{b} \right)^n + (A_\sigma + A_\gamma) \sin \left( \frac{\omega_w t + \Phi}{n_g} \right) \quad (23)$$

The shear stress at the contact interface, based on the Wong model, is given by:

$$s(j) = (c + \sigma(z) \tan \phi) K_r \left\{ 1 + \left( \frac{1}{K_r \left( 1 - \frac{1}{c} \right)} - 1 \right) e^{-\frac{j}{K_w}} \right\} \left( 1 - e^{-\frac{j}{K_w}} \right) \quad (24)$$

where  $n = n_0 + n_1 s$  and  $j = r[\theta_1 - \theta - (1-s)\sin\theta]$  defines the slippage-dependent sinkage exponent and shear displacement, respectively. The parameters and variables used in the terramechanics models are summarized in Table 3. Among these, the most sensitive parameters influencing slippage are the internal friction angle and cohesion, both of which vary inversely with slippage [13,14].

The models are embedded into the Vortex terramechanic module to dynamically compute terrain deformation and traction losses under varying soil conditions [59]. The parameter values are set to the South Pole lunar soil parameters, provided by the Mohammed Bin Rashid Space Centre in [7,60]. Furthermore, the soft terrain tracks are designed to exhibit position-dependent variable slippage, characterized by a spatially varying internal friction angle  $\phi(x)$  and soil cohesion  $c(x)$ , as defined in (25). This formulation captures the realistic behavior of WMR traversing soft terrain, where deformability transitions from hard to moderate to highly soft regions, especially along sloped profiles [21, 62].

$$\phi(x), c(x) = \begin{cases} 0.85, 1.5; & x > 2.5 \\ 0.5 + 0.07(x + 2.5), 0.5 + 0.2(x + 2.5); & -2.5 \le x \le 2.5 \\ 0.50, 0.5; & x < -2.5 \end{cases} \quad (25)$$

where  $x$  is the position of the WMR on the track,  $\phi(x)$  is in radians, and  $c(x)$  in kilopascals (kPa). As the WMR ascends the inclined terrain, it encounters a decrease in the internal friction angle  $\phi(x)$  and cohesion  $c(x)$ , which increases slippage. This effect is illustrated by the slippage gradient variation along the track in Fig. 6.

The calibration of this spatially varying terrain model is grounded in established terramechanics principles and informed by empirical data [59,60]. Specifically, we adopted and extended the position-sensitive terrain variation strategies proposed in [15,20], with experimental validation procedures reported in [63]. The chosen parameter ranges for cohesion (0.5–1.5 kPa) and internal friction angle (0.5–0.85 rad) reflect values reported for lunar regolith and soft terrestrial soils, which exhibit spatial variability due to compaction, depth, and slope angle [20,63]. A linear spatial gradient was introduced to dynamically model these parameter changes, ensuring that the resulting velocity loss and inertial responses align with real-world WMR behavior over deformable terrain.

Furthermore, the one-way communication delay from the operator to the remote environment is assumed to be 1.25 s, representing the communication latency over the Earth-to-Moon distance (380,000 km) [16,41]. These delays are implemented using a software buffer on a

![Figure 6: Designated roadmap showing soft terrain tracks (A, B, and C) with dynamic slippage and non-track zone in the virtual environment, with a slope angle of 8°. The left panel shows a 3D perspective view of a rover (WMR) on a lunar-like surface with tracks A, B, and C. The right panel is a top-down map view showing the tracks as gray lines, centerlines as black lines, and boundaries as white lines. A color bar at the bottom indicates slippage gradient variation φ(x), c(x) from 0.5 to 1.5.](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 6: Designated roadmap showing soft terrain tracks (A, B, and C) with dynamic slippage and non-track zone in the virtual environment, with a slope angle of 8°. The left panel shows a 3D perspective view of a rover (WMR) on a lunar-like surface with tracks A, B, and C. The right panel is a top-down map view showing the tracks as gray lines, centerlines as black lines, and boundaries as white lines. A color bar at the bottom indicates slippage gradient variation φ(x), c(x) from 0.5 to 1.5.

**Fig. 6.** Designated roadmap showing soft terrain tracks (A, B, and C) with dynamic slippage and non-track zone in the virtual environment, with a slope angle of 8°. The right panel presents a top-down map view with visible slippage gradient variation, track centerlines, and track boundaries.

**Table 3**

Terramechanics model parameters for soft terrain simulation [13,59,60].

| Symbol     | Description                                  | Typical value | Unit              |
|------------|----------------------------------------------|---------------|-------------------|
| $c$        | Soil cohesion                                | 1.5           | kPa               |
| $\gamma$   | Soil weight density                          | 15.6          | kN/m <sup>3</sup> |
| $b$        | Wheel width                                  | 0.08          | m                 |
| $z$        | Sinkage depth                                | Variable      | m                 |
| $k'_c$     | Cohesive pressure-sinkage coefficient        | 0.63          | –                 |
| $k'_\phi$  | Frictional pressure-sinkage coefficient      | 80            | –                 |
| $n_0$      | Static sinkage exponent                      | 1.1           | –                 |
| $n_1$      | Dynamic sinkage exponent                     | Variable      | –                 |
| $A_\sigma$ | Lug excitation amplitude due to stress       | 3.4           | Pa                |
| $A_\gamma$ | Lug excitation amplitude due to soil density | 0.73          | Pa                |
| $\omega_w$ | Wheel angular velocity                       | Variable      | rad/s             |
| $n_g$      | Number of lugs                               | 14            | –                 |
| $\phi$     | Initial phase                                | 0             | rad               |
| $j$        | Shear displacement                           | Variable      | cm                |
| $K_w$      | Shear deformation modulus                    | 3.75          | cm                |
| $K_r$      | Residual shear stress ratio                  | 0.65          | –                 |
| $\phi$     | Internal friction angle                      | 0.85          | rad               |
| $\sigma$   | Normal stress acting at the soil             | Variable      | kPa               |
| $s$        | Slip ratio                                   | Variable      | –                 |

User Datagram Protocol (UDP) network, with variable delays modeled as

$$T(t) = 1.1 + \epsilon, \quad \epsilon \sim \mathcal{U}(-0.15, 0.15) \quad (26)$$

for both forward and backward communication, with  $T(t)$  in s. The visual interface simulates south-pole lunar low-light conditions at approximately 2.7 lux [64]. This is achieved by adjusting the screen brightness to 7% of its maximum level, as verified using a mobile light meter application positioned 40 cm from the screen. The simulation environment is also configured with lunar gravity of 1.633 m/s<sup>2</sup> [13].

Although the high-fidelity simulation environment developed in this study offers a robust emulation of the lunar environment, there are inherent limitations that may not fully capture the challenges of actual lunar scenarios. Some of these limitations includes:

- (1) The terramechanics model assumes spatial continuity of soil parameters, but actual lunar regolith exhibits abrupt transitions in compaction and grain size, which can significantly affect wheel–terrain interaction and slippage behavior.
- (2) The simulation does not replicate the abrasive and adhesive behavior of lunar dust. In practice, lunar dust can degrade sensor accuracy, actuator performance, and thermal behavior over time, which could impact the system's long-term reliability.
- (3) While an approximate lunar gravity is enforced, fine-grained inertial dynamics and contact force variations in 1/6th gravity conditions may not be fully captured in the simulator, particularly during traction loss and tip-over scenarios.

## 4.3. Task description

Five operators participated in the experiments for point-to-point track-following tasks. Three (3) of them are experts with prior experience in teleoperating wheeled rovers, while the remaining two (2) are non-experts but had experience with driving in video games. Each operator was tasked with completing the track as quickly as possible at a safe speed of 0.1 m/s, while minimizing lateral deviation from the centerline, staying within the track boundary, and using the first-person camera view.

To ensure the operators could effectively perceive slippage using this scaling in the experimental design, we first conducted preliminary trials for the track-following task. These trials allowed operators to familiarize themselves with the scaled force feedback and adapt to the slippage perception within the context of the experiment. The objective was to ensure that the adopted force feedback was appropriately perceptible and scaled for operators to effectively detect slippage of the WMR on soft terrain during the teleoperation tasks, without the need for additional fine-tuning of the scaling parameters. After the trials, all operators agreed that the magnitude of the force feedback was perceptible and comfortable, offering a balance between slippage awareness and operator fatigue.

Each of the operators performed three experimental cases under different conditions: (I) **Ideal case**, without any delays with only P controllers, serving as a baseline for performance; (II) **Delayed case**, with round-trip delays and with PD controllers in (7), to assess

the impact of delays on the performance; and (III) **Predicted case**, with the same amount of delays and with our PiLSTM predictor-based controllers in (8) against the benchmark controllers based on FOD and WV predictors, to assess performance improvement due to delay compensation. Before data collection, these operators received training to familiarize them with the test platform and practice operating under different conditions. After the training, each operator repeated each of the three cases once for each of the three tracks in a randomized order of the experimental case to minimize the human learning effect. Thus, each operator completed 9 trials, resulting in a total of 45 experimental trials. A portion of the collected data on coupling variables has been allocated for the training and testing phases of the predictors  $\hat{x}_m(t)$  and  $\hat{f}_e(t)$  in Section 3

## 4.4. Proposed PiLSTM predictor framework implementation

Each of our PiLSTM predictors, outlined in Section 3, is tailored to a specific coupling variable for long-horizon predictions. The predictors  $\hat{x}_{m}(t)$  and  $\hat{x}_{m,o}(t)$  are implemented on the remote environment as the forward predictor, while  $\hat{f}_{e}(t)$  and  $\hat{f}_{e,o}(t)$  are implemented on the operator station as the backward predictor. Each of these predictors feeds its delayed past outputs back into the inputs for future predictions. This feedback mechanism enables the predictors to continuously adapt to variations in delays during operation. To enable hardware-compatible real-time operation, each trained PiLSTM predictor is deployed using Simulink. The predictors are encapsulated in MATLAB Function blocks that leverage the Deep Learning Toolbox to load and evaluate the trained LSTM networks at runtime. This integration allows GPU-accelerated inference using the Parallel Computing Toolbox during operation and facilitates future deployment to embedded platforms via Simulink Coder. The measured runtime for each predictor (in ms) is:  $(\tau_{x_m} = 11.3, \tau_{x_{m,o}} = 19.7, \tau_{f_e} = 15.5, \tau_{f_{e,o}} = 21.2)$ , which includes overheads due to inference, kernel launches, data transfer, and activation. These results confirm the computational feasibility of deploying the PiLSTM predictors within real-time feedback loops, supporting closed-loop integration with minimal latency overhead.

Together, the Simulink-integrated predictors form the complete PiLSTM framework, as shown in Fig. 2. The outputs of this framework are applied to the designed teleoperator controllers in (8), to achieve robust and high-fidelity closed-loop integration. Finally, the developed predictor-based controllers together with the blended architecture for the teleoperated WMR is evaluated in closed-loop case studies discussed in Section 4.

## 4.5. Benchmarking predictors frameworks implementation

Two well-known model-free predictors, FOD and WV, were implemented as benchmarks to evaluate delay compensation effectiveness. The FOD predictor framework was implemented in the proposed teleoperation system as described in the previous work [41]. Additionally, since the variables  $x_m(t)$  and  $f_e(t)$  of the proposed teleoperation system form a power conjugate pair, the state-of-the-art WV approach [20,40] was selected as an alternative delay compensation method to serve as a benchmark for the developed PiLSTM predictor framework. This comparison further validates the effectiveness of the framework in terms of robust delay compensation and achieving high-fidelity closed-loop integration.

## 4.6. Evaluation metrics

The experiments, conducted in closed-loop case studies, are evaluated through three performance metrics as follows.

![Figure 7: Operator #1 on track A. Tracking performance comparison of motion commands (top) and force feedbacks (bottom) among the ideal case, our PiLSTM predicted case, FOD predicted case, and delayed case in a closed-loop scenario. The top row shows motion commands x_m1 (m/s) and x_m2 (rad/s) over 30 seconds. The bottom row shows force feedbacks f_e1 (N) and f_e2 (N) over 30 seconds. Each plot compares four cases: Ideal (green solid line), PiLSTM (blue solid line), FOD (red dashed line), and Delayed (black dashed line). The PiLSTM case shows the closest performance to the ideal case.](ae05c5a58b4f9ae5751c216b280b0f72_img.jpg)

Figure 7: Operator #1 on track A. Tracking performance comparison of motion commands (top) and force feedbacks (bottom) among the ideal case, our PiLSTM predicted case, FOD predicted case, and delayed case in a closed-loop scenario. The top row shows motion commands x\_m1 (m/s) and x\_m2 (rad/s) over 30 seconds. The bottom row shows force feedbacks f\_e1 (N) and f\_e2 (N) over 30 seconds. Each plot compares four cases: Ideal (green solid line), PiLSTM (blue solid line), FOD (red dashed line), and Delayed (black dashed line). The PiLSTM case shows the closest performance to the ideal case.

Fig. 7. Operator #1 on track A: Tracking performance comparison of motion commands (top) and force feedbacks (bottom) among the ideal case, our PiLSTM predicted case, FOD predicted case, and delayed case in a closed-loop scenario. Our PiLSTM predictors provide improved delay compensation performance over FOD, producing outputs that are closer to the ideal case.

### 4.6.1. Delay compensation performance metrics

The prediction performance of our PiLSTM predictor framework for delay compensation performance is evaluated. The output of the ideal case is considered the reference for the other two cases. The compensation based on the prediction performance of each predictor is quantified by normalized performance metrics, in percentage (%), denoted as  $\Delta_n$  [40]. This metric is computed as the ratio of the L2 norm of the difference between the predicted output  $\hat{y}(t)$  and the ideal output  $y(t)$  to the L2 norm of the difference between the delayed output  $y(t-T)$  and the ideal output  $y(t)$  as follows:

$$\Delta_n = \frac{\|\hat{y}(t) - y(t)\|_2}{\|y(t-T) - y(t)\|_2} \times 100\% \quad (27)$$

where  $y$  symbolizes the coupling variable of interest ( $x_m, f_e$ ). A  $\Delta_n = 0\%$  indicates that the predictor perfectly predicts the ideal output and compensates for the entire delays, achieving an ideal performance. A  $\Delta_n < 100\%$  suggests that the predictor predicts the ideal output and compensates the delay to some meaningful amount, with its proximity to zero reflecting the extent of better prediction and compensation. Conversely,  $\Delta_n > 100\%$  indicates that the predictor poorly predicts the ideal output and amplifies the negative effect of the delay.

Finally, to evaluate the overall prediction and delay compensation performance for the predictor framework as a whole, a normalized average performance metric,  $\Delta_{n,avg}$ , is further defined as

$$\Delta_{n,avg} = \frac{1}{N_o} \sum_{j=1}^{N_o} \Delta_{n,j} \quad (28)$$

where  $N_o$  is the number of outputs of the predictor framework in a given configuration, and  $j$  is an index for the outputs in that configuration.

### 4.6.2. Teleoperation performance metrics

The teleoperation performance of the PiLSTM predictor-based approach is evaluated. The ideal case and delayed case are considered as the baseline for the predicted case. Two metrics quantify the teleoperation performance [5,27]: tracking performance, and force transparency. The tracking performance metric — velocity tracking error,  $\Omega_n$ , is quantified by the deviations between the given motion commands  $x_m(t)$  and the WMR's actual measured states  $\xi_m(t)$ . The force transparency metrics — force feedback tracking error,  $\Gamma_n$ , in contrast, is quantified by the deviation between what force the operator perceives  $f_h(t)$  and the

actual environmental force-induced slippage  $f_e(t)$ . These two metrics directly reflect the fidelity of the closed-loop integration, where smaller values indicate higher fidelity and larger values indicate lower fidelity. The mathematical expressions for these metrics are as follows:

$$\begin{aligned}\Omega_n &= \|x_m(t) - \xi_s(t)\|_2, \\ \Gamma_n &= \|f_h(t) - f_e(t)\|_2\end{aligned}\quad (29)$$

However, the force applied by the operator  $f_h$  cannot be directly measured due to the position-based nature of the teleoperation scheme. Thus, a computationally efficient estimation approach is employed using the linearized master dynamics in (2), consistent approach with prior works [13,21]. Although simplified, this model enables accurate real-time force estimation for performance evaluation in the WMR teleoperation experiments [12,15,27]. To evaluate the overall performance improvement of the predicted output, the tracking performance and force transparency were normalized with the delayed output. Thus, we define the average tracking performance metric,  $\Omega_{n,\text{avg}}$ , and average force transparency metric,  $\Gamma_{n,\text{avg}}$ , as follows:

$$\begin{aligned}\Omega_{n,\text{avg}} &= \frac{1}{M_o} \sum_{j=1}^{M_o} \frac{\Omega_{n,j}}{\Omega_{n,d}} \times 100\% \\ \Gamma_{n,\text{avg}} &= \frac{1}{M_o} \sum_{j=1}^{M_o} \frac{\Gamma_{n,j}}{\Gamma_{n,d}} \times 100\%\end{aligned}\quad (30)$$

where  $M_o$  is the number of degrees of freedom for the teleoperated WMR system,  $j$  is an index for the present degree of freedom in that system, and  $\Omega_{n,d}$  and  $\Gamma_{n,d}$  are the tracking performance and force transparency metrics for the delayed case.

### 4.6.3. Task performance metrics

The performance of the operators on the track-following task of the WMR using the bilateral teleoperation system is evaluated using two key metrics, as the task depends on both spatial and temporal accuracy: centerline-following Score and time efficiency score. The centerline-following score,  $S_c$ , quantifies the deviation of WMR trajectory from the centerline throughout the course of the track. The overall centerline-following score is given by:

$$S_c = \frac{1}{C_o} \sum_{i=1}^{C_o} \max(0, 1 - |d(t_i)|) \quad (31)$$

where  $d(t_i)$  represents the lateral deviation from the centerline at time step  $t_i$ , and  $C_o$  is the number of time steps. A score of 1 indicates perfect adherence to the centerline, while a score of 0 signifies that the operator never traversed the test track (completely outside the track). Intermediate scores reflect the extent of lateral deviations from the centerline.

On the other hand, the time efficiency score,  $S_t$  evaluates how quickly the operator moves the WMR to accomplish the task relative to an optimal benchmark time. It is defined as:

$$S_t = \max \left( 0, 1 - \frac{T_a - T_o}{T_o} \right) \quad (32)$$

where  $T_a$  is the actual time taken to complete the task,  $T_o$  is the pre-defined optimal completion time. This metric ensures that completing the task within the optimal time yields a score of 1, while exceeding the optimal time reduces the score proportionally. If the actual time surpasses twice the optimal time, the score becomes 0, indicating suboptimal efficiency.

Therefore, the success rate is determined by combining the  $S_c$  and the  $S_t$  into a single composite metric. This approach ensures fair evaluation of operators considering both trajectory adherence and task completion efficiency. The success metric,  $S_{\text{success}}$  is formulated as:

$$S_{\text{success}} = \begin{cases} 1, & \lambda_c S_c + \lambda_t S_t \ge 0.8 \\ 0, & \text{otherwise.} \end{cases} \quad (33)$$

where  $\lambda_c$  and  $\lambda_t$  are the respective weighting factors that determine the relative importance of trajectory adherence and time efficiency, ensuring  $\lambda_c + \lambda_t = 1$ . A trial is scored as successful (=1) if the computed  $S_{\text{success}}$  meets or exceeds 80%, ensuring that the WMR has followed the trajectory effectively while completing the task within an acceptable time frame. Otherwise, the trial is considered unsuccessful (=0).

# 5. Result and discussion

The gains of the proposed bilateral teleoperator controllers in (7) and (8) were set to  $k_m = 10$ ,  $d_m = 10.5$ ,  $k_s = 1$ , and  $d_s = 0.2$ . These values were chosen to satisfy the stability conditions established in (9), while also achieving a balanced trade-off between system stability and transparency. The parameter values for the conventional FOD predictors in (12) were set to  $\alpha = 0.21$  and  $\beta = 1.16$  to achieve optimal prediction performance for both forward and backward delays as given by (26). Moreover, the design parameter in the benchmarking wave variable method is set to  $b = 0.95$  to minimize wave reflection and preserve passivity [20].

## 5.1. Delay compensation performance evaluation

This study compares the prediction performance between our developed PiLSTM predictor and the conventional FOD predictor framework [21,40] for robust delay compensation and to support our key claims.

A comparative analysis of the coupling variables for Operator #1 performing the task on track A is depicted in Fig. 7. The predicted outputs from both our PiLSTM and the FOD are aligned with the ideal output consistently. However, the PiLSTM outputs are closer to the ideal outputs than those of the FOD, indicating better prediction performance by PiLSTM. Notably, the PiLSTM demonstrated a smoother curve, while the FOD showed more fluctuation, as evidenced by the curves. These performance differences are clearly observed in the corresponding error metrics presented in Fig. 8. It can be observed that our PiLSTM maintains a lower prediction error margin compared to the FOD and the delayed, with fewer and lower spikes throughout the observed period. In contrast, the FOD exhibits higher peaks at specific instances, indicating less accurate prediction performance. This results in prediction errors even higher than the delayed outputs, for instance, in the FOD predicted motion commands  $\hat{x}_{mv}$  and  $\hat{x}_{mvo}$  at 8.2 s and at 23.5 s, and for the force feedbacks  $\hat{f}_{mv}$  and  $\hat{f}_{mvo}$  at 5.1 s and 15.8 s, respectively. These peaks typically occur in response to sudden changes in operator input, where the linear FOD model fails to capture underlying nonlinearities as discussed in [40].

Further encapsulating the PiLSTM prediction performance analysis, the normalized delay compensation performance metrics are summarized in Table 4. For Operator #1, the PiLSTM predicted output  $\hat{x}_{mv}$  demonstrates a lower error,  $\Delta_n$ , of 18.3% compared to the FOD error of 48.5%. Similarly, the predicted output  $\hat{f}_{mv}$  from PiLSTM shows a lower error, of 19.2% compared to the 48.9% of FOD output.

Similarly, performance comparisons for Operators 2, 3, 4, and 5 were conducted in the remaining experiments on the different tracks (A, B, and C). The comparative analysis of the coupling variables for Operator #2 on track C is displayed in Fig. 9, along with the corresponding error metrics in Fig. 10, respectively. Supplementing these visual results, the normalized performance metrics for this operator and the remaining operators are summarized in Table 4 to support the delay compensation evaluation. The highest prediction accuracy for the PiLSTM framework was achieved by Operator 2 on Track B, with a normalized average metric,  $\Delta_n$ , of 9.6%, compared to the best performance for the FOD framework for Operator 1 on Track B, which had a normalized average metric of 29.3%, as highlighted in green. However, the FOD predictor often exhibits poor prediction with normalized metrics exceeding 100%, such as 102.7%, 100.3%, and 116.2%, which are shaded in brown. Furthermore, we computed the

**Table 4**  
c PILSTM framework vs. FOD framework [40].

| Operators              | Tracks  | $\Delta_n - x_{mp} (\%)$ |      | $\Delta_n - x_{mo} (\%)$ |       | $\Delta_n - f_{ev} (\%)$ |      | $\Delta_n - f_{eo} (\%)$ |       |
|------------------------|---------|--------------------------|------|--------------------------|-------|--------------------------|------|--------------------------|-------|
|                        |         | PiLSTM                   | FOD  | PiLSTM                   | FOD   | PiLSTM                   | FOD  | PiLSTM                   | FOD   |
| Expert Operator #1     | Track A | 18.3                     | 48.5 | 22.5                     | 50.7  | 19.2                     | 48.9 | 28.5                     | 58.7  |
|                        | Track B | 11.1                     | 29.3 | 17.2                     | 38.1  | 21.0                     | 42.3 | 27.0                     | 50.9  |
|                        | Track C | 21.0                     | 51.1 | 23.2                     | 57.2  | 34.2                     | 53.5 | 34.9                     | 58.7  |
| Expert Operator #2     | Track A | 16.9                     | 43.6 | 21.8                     | 52.4  | 20.2                     | 48.7 | 23.6                     | 57.2  |
|                        | Track B | 9.4                      | 31.2 | 14.1                     | 35.6  | 17.7                     | 33.0 | 20.8                     | 42.9  |
|                        | Track C | 18.5                     | 40.5 | 20.1                     | 52.7  | 28.2                     | 48.9 | 30.0                     | 52.9  |
| Expert Operator #3     | Track A | 19.7                     | 50.7 | 24.6                     | 52.1  | 22.0                     | 47.3 | 26.2                     | 59.2  |
|                        | Track B | 11.6                     | 30.1 | 13.9                     | 47.8  | 19.9                     | 38.2 | 24.5                     | 51.8  |
|                        | Track C | 21.9                     | 54.2 | 26.1                     | 58.7  | 27.2                     | 56.7 | 30.6                     | 62.4  |
| Non-expert Operator #4 | Track A | 22.3                     | 43.1 | 37.0                     | 102.7 | 27.3                     | 47.6 | 37.5                     | 89.9  |
|                        | Track B | 17.9                     | 34.5 | 23.4                     | 46.0  | 19.9                     | 42.0 | 27.7                     | 57.2  |
|                        | Track C | 25.8                     | 50.0 | 29.2                     | 68.7  | 26.4                     | 56.3 | 34.5                     | 100.3 |
| Non-expert Operator #5 | Track A | 21.4                     | 49.2 | 34.1                     | 58.7  | 29.6                     | 58.8 | 36.2                     | 69.9  |
|                        | Track B | 18.3                     | 31.1 | 22.2                     | 40.7  | 21.2                     | 43.9 | 28.6                     | 58.1  |
|                        | Track C | 24.4                     | 53.3 | 30.1                     | 59.7  | 25.2                     | 62.8 | 44.5                     | 116.2 |

![Figure 8: Absolute prediction error comparison for Operator #1 on track A. The figure consists of six subplots arranged in a 3x2 grid. The top row shows motion commands: error in x_mv (m/s) on the left and x_mv (m/s) on the right. The bottom row shows force feedbacks: error in f_mv (N) on the left and f_mv (N) on the right. All plots compare PiLSTM (Ours) in blue, FOD in red, and a delayed case in black. The x-axis for all plots is 'Joint1-time (s)' and 'Joint2-time (s)' from 0 to 30. PiLSTM consistently shows the lowest error across all metrics.](fe753d01ad5fe6cf150018c958173c6d_img.jpg)

Figure 8: Absolute prediction error comparison for Operator #1 on track A. The figure consists of six subplots arranged in a 3x2 grid. The top row shows motion commands: error in x\_mv (m/s) on the left and x\_mv (m/s) on the right. The bottom row shows force feedbacks: error in f\_mv (N) on the left and f\_mv (N) on the right. All plots compare PiLSTM (Ours) in blue, FOD in red, and a delayed case in black. The x-axis for all plots is 'Joint1-time (s)' and 'Joint2-time (s)' from 0 to 30. PiLSTM consistently shows the lowest error across all metrics.

**Fig. 8.** Operator #1 on track A: Absolute prediction error comparison of motion commands (top) and force feedbacks (bottom) among our PiLSTM predicted case, FOD predicted case, and delayed case. Our PiLSTM exhibits the least prediction error, whereas the FOD predictor yields relatively poor prediction and delay compensation performance approaching the delayed case.

![Figure 9: Tracking performance comparison for Operator #2 on track C. The figure consists of six subplots arranged in a 3x2 grid. The top row shows motion commands: x_mv (m/s) on the left and x_mv (rad/s) on the right. The bottom row shows force feedbacks: f_mv (N) on the left and f_mv (N) on the right. All plots compare PiLSTM (Ours) in blue, FOD in red, and a delayed case in black. The x-axis for all plots is 'Joint1-time (s)' and 'Joint2-time (s)' from 0 to 30. PiLSTM tracks the ideal case (green dashed line) most closely.](239211fa511b4ffa685b54b5132ec927_img.jpg)

Figure 9: Tracking performance comparison for Operator #2 on track C. The figure consists of six subplots arranged in a 3x2 grid. The top row shows motion commands: x\_mv (m/s) on the left and x\_mv (rad/s) on the right. The bottom row shows force feedbacks: f\_mv (N) on the left and f\_mv (N) on the right. All plots compare PiLSTM (Ours) in blue, FOD in red, and a delayed case in black. The x-axis for all plots is 'Joint1-time (s)' and 'Joint2-time (s)' from 0 to 30. PiLSTM tracks the ideal case (green dashed line) most closely.

**Fig. 9.** Operator #2 on track C: Tracking performance comparison of motion commands (top) and force feedbacks (bottom) among ideal case, our PiLSTM predicted case, FOD predicted case, and delayed case in a closed-loop scenario. The PiLSTM predicted output is closer to the Ideal case, thus yielding better prediction performance.

normalized average performance metrics,  $\Delta_{n,avg}$ , as presented in Fig. 11. It can be seen that the PiLSTM framework outperforms the FOD across all the cases. The mean of the normalized average performance metrics for all operators is 23.5% for the PiLSTM framework, compared to 53.3% for the FOD framework. This indicates a prediction performance improvement of 29.7% in terms of the normalized average performance metric,  $\Delta_{n,avg}$ , highlighting the robustness of the PiLSTM framework in compensating for large delays across various test scenarios.

Some of the key observations from the delay compensation analysis are as follows: (i) the PiLSTM predictor has the best prediction performance with the least normalized metrics for Track B among all the operators. This is attributed to the straight-line pattern of Track B, where delays have less impact on the coupling variables due to the straight-line trajectory; (ii) the predictors are more accurate at predicting motion commands than force feedback, likely due to the greater regularity and predictability in motion commands compared to the less predictable nature of force feedback; (iii) the predictors performed better when applied to data from trained operators compared to non-trained operators. This is attributed to the more consistent and predictable behavior exhibited by expert operators, resulting in smoother coupling variables. Additionally, the PiLSTM is trained based on the data from trained operators.

![Figure 10: Absolute prediction error comparison for Operator #2 on track C. The figure consists of six subplots arranged in a 3x2 grid. The top row shows motion commands: error in x_mv (m/s) on the left and error in x_mv (rad/s) on the right. The bottom row shows force feedbacks: error in f_mv (N) on the left and error in f_mv (N) on the right. All plots compare PiLSTM (Ours) in blue, FOD in red, and a delayed case in black. The x-axis for all plots is 'Joint1-time (s)' and 'Joint2-time (s)' from 0 to 30. PiLSTM shows the lowest error, followed by FOD, then the delayed case.](ba2fa04727a9b45fb9afd1af3e3e905b_img.jpg)

Figure 10: Absolute prediction error comparison for Operator #2 on track C. The figure consists of six subplots arranged in a 3x2 grid. The top row shows motion commands: error in x\_mv (m/s) on the left and error in x\_mv (rad/s) on the right. The bottom row shows force feedbacks: error in f\_mv (N) on the left and error in f\_mv (N) on the right. All plots compare PiLSTM (Ours) in blue, FOD in red, and a delayed case in black. The x-axis for all plots is 'Joint1-time (s)' and 'Joint2-time (s)' from 0 to 30. PiLSTM shows the lowest error, followed by FOD, then the delayed case.

**Fig. 10.** Operator #2 on track C: Absolute prediction error comparison of motion commands (top) and force feedbacks (bottom) among our PiLSTM predicted case, FOD predicted case, delayed case. Our PiLSTM exhibits the least prediction error, followed by the FOD predictor case, then the delayed case.

![Figure 11: Bar charts showing normalized average performance metrics Δ_n,avg (%) across five operators (Operator #1 to Operator #5) and three tracks (Track A, Track B, Track C). The legend indicates four cases: Ideal Case (green), PiLSTM (Ours) (yellow), FOD (orange), and Delayed Case (red). The y-axis ranges from 0 to 100. In all cases, the performance is near 100% for the Ideal Case. PiLSTM (Ours) shows significantly lower values than FOD, especially for Operator #1 and Operator #5. The Delayed Case consistently shows the highest values across all operators and tracks.](b3df5964338063224492c01f09e4fed6_img.jpg)

Figure 11: Bar charts showing normalized average performance metrics Δ\_n,avg (%) across five operators (Operator #1 to Operator #5) and three tracks (Track A, Track B, Track C). The legend indicates four cases: Ideal Case (green), PiLSTM (Ours) (yellow), FOD (orange), and Delayed Case (red). The y-axis ranges from 0 to 100. In all cases, the performance is near 100% for the Ideal Case. PiLSTM (Ours) shows significantly lower values than FOD, especially for Operator #1 and Operator #5. The Delayed Case consistently shows the highest values across all operators and tracks.

**Fig. 11.** Normalized average performance metrics  $\Delta_{n,avg}$  across all operators and tracks. Smaller  $\Delta_{n,avg}$  indicates better prediction and delay compensation performance by the framework. The PiLSTM framework achieved an average improvement of 29.7% in prediction performance over the FOD framework in all cases, demonstrating robust delay compensation.

## 5.2. Teleoperation performance evaluation

The teleoperation performance of the developed PiLSTM-based system is benchmarked against the conventional FOD [21,40] and the state-of-the-art Wave Variable (WV)-based system [20], within the integrated teleoperated WMR framework.

The velocity and force feedback tracking teleoperation performance in the ideal case for Operator #1 on Track A is shown in Fig. 12. The deviation between the WMR states  $\xi_s$  and the commanded motion  $x_m$  is almost negligible. Similarly, the deviation between the environmental force  $f_e$  and the operator force  $f_h$  is minimal. Although a small non-zero delay of 0.08 s is observed in the zoomed plots due to the selected control gains, the performance and transparency metrics converge to near-zero values. This indicates the highest level of fidelity in the closed-loop integration. As a result, the command-tracking performance becomes nearly perfect, aligning with the results obtained in [15,27]. The observed rapid spikes in the environmental force  $f_e$  are attributed to measurement noise in the estimation of slippage information in the virtual environment.

However, when the forward and backward delays defined in (26) are introduced into the ideal case for the same operator — the delayed case — a significant lag is observed between the WMR states  $\xi_s$  and the motion commands  $x_m$ , as well as between the environmental force feedback  $f_e$  and the operator force  $f_h$ . This lag is evident in the velocity and force tracking performance shown in Fig. 13. For example, the output trajectories of the velocities exhibit a lag of 1.32 s relative to the reference for Joint 1 at 9 s, and a lag of 1.29 s relative to the reference for Joint 2 at 52 s. Consequently, the performance and transparency metrics exhibit substantial increases, demonstrating a significant deterioration in the fidelity of the closed-loop integration compared to the ideal case. Additionally, larger gain errors between  $f_e$  and  $f_h$  in the force feedback response are observed, attributed to the conservative derivative gain in the controller in (7). This makes the system completely non-transparent, as evidenced by the force feedback metrics in Fig. 13. Consequently, the operator may attempt to exceed the WMR's

![Figure 12: Performance and transparency metrics comparison for Operator #1 on Track A. The figure consists of four subplots: Velocity tracking (m/s) for Joint1-time (s) and Joint2-time (s); and Force feedback tracking (N) for Joint1-time (s) and Joint2-time (s). Each subplot compares the commanded motion x_m(t) (red solid line) and the WMR state v_s(t) (blue dashed line) for velocity, and the environmental force f_e(t) (red solid line) and the operator force f_h(t) (blue dashed line) for force feedback. Zoomed-in insets show the details of the tracking performance over time.](0bd23f00e0632855cfef9274f1ab93d8_img.jpg)

Figure 12: Performance and transparency metrics comparison for Operator #1 on Track A. The figure consists of four subplots: Velocity tracking (m/s) for Joint1-time (s) and Joint2-time (s); and Force feedback tracking (N) for Joint1-time (s) and Joint2-time (s). Each subplot compares the commanded motion x\_m(t) (red solid line) and the WMR state v\_s(t) (blue dashed line) for velocity, and the environmental force f\_e(t) (red solid line) and the operator force f\_h(t) (blue dashed line) for force feedback. Zoomed-in insets show the details of the tracking performance over time.

**Fig. 12.** Ideal case — Operator #1 on track A: Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. Baseline performance for the teleoperation system with only a proportional controller.

safe speed (i.e.,  $v_s = 0.1$  m/s and turn  $\omega_s = 0.87$  rad/s), compromising overall system stability. This manifests as rapid fluctuations in velocity output tracking, persisting until the operator reduces their pace and initiates the process again, particularly evident around the 32-second mark. This cumulative effect results in more severe command-tracking performance and poses a risk of tip-over. This finding is consistent with the results in [20].

To address the significant deterioration in the fidelity of closed-loop integration observed in the presence of the delays, our PiLSTM predictor-based controllers are incorporated into the delayed case, forming what we refer to as the predicted case. This integration leads

**Table 5**

Teleoperation performance metrics: Our PiLSTM-based Approach vs. Other approaches ( $\Omega_{n,d} - x_{mv} = 0.25$  m/s,  $\Omega_{n,d} - x_{mo} = 6.35$  rad/s,  $\Gamma_{n,d} - f_{ev} = 1.9$  N,  $\Gamma_{n,d} - f_{eo} = 8.52$  N).

| Operators                 | Tracks  | $\Omega_n - x_{mv}$ (m/s) |      |      | $\Omega_n - x_{mo}$ (rad/s) |      |      | $\Gamma_n - f_{ev}$ (N) |      |      | $\Gamma_n - f_{eo}$ (N) |      |      |
|---------------------------|---------|---------------------------|------|------|-----------------------------|------|------|-------------------------|------|------|-------------------------|------|------|
|                           |         | PiLSTM                    | FOD  | WV   | PiLSTM                      | FOD  | WV   | PiLSTM                  | FOD  | WV   | PiLSTM                  | FOD  | WV   |
| Expert<br>Operator #1     | Track A | 0.04                      | 0.11 | 0.17 | 1.71                        | 2.96 | 3.73 | 0.14                    | 0.30 | 0.42 | 1.65                    | 2.86 | 3.37 |
|                           | Track B | 0.03                      | 0.09 | 0.11 | 1.02                        | 2.23 | 2.63 | 0.10                    | 0.21 | 0.29 | 0.96                    | 2.09 | 2.88 |
|                           | Track C | 0.07                      | 0.13 | 0.19 | 1.82                        | 3.06 | 5.98 | 0.15                    | 0.32 | 0.43 | 1.74                    | 3.19 | 3.47 |
| Expert<br>Operator #2     | Track A | 0.05                      | 0.11 | 0.21 | 1.69                        | 2.99 | 3.84 | 0.16                    | 0.28 | 0.46 | 1.71                    | 2.85 | 3.94 |
|                           | Track B | 0.02                      | 0.10 | 0.11 | 1.10                        | 2.24 | 2.99 | 0.14                    | 0.22 | 0.28 | 1.21                    | 2.15 | 3.36 |
|                           | Track C | 0.07                      | 0.12 | 0.23 | 1.80                        | 2.97 | 3.91 | 0.17                    | 0.33 | 0.43 | 1.82                    | 2.96 | 4.06 |
| Expert<br>Operator #3     | Track A | 0.04                      | 0.12 | 0.19 | 1.77                        | 3.16 | 4.81 | 0.13                    | 0.32 | 0.47 | 0.99                    | 2.73 | 4.14 |
|                           | Track B | 0.03                      | 0.11 | 0.18 | 1.04                        | 2.31 | 2.77 | 0.11                    | 0.24 | 0.31 | 1.17                    | 2.00 | 3.11 |
|                           | Track C | 0.08                      | 0.16 | 0.20 | 1.86                        | 3.03 | 3.62 | 0.15                    | 0.32 | 0.39 | 1.82                    | 3.07 | 3.95 |
| Non-expert<br>Operator #4 | Track A | 0.09                      | 0.14 | 0.26 | 2.92                        | 3.46 | 4.76 | 0.21                    | 0.33 | 0.43 | 1.78                    | 3.41 | 4.52 |
|                           | Track B | 0.04                      | 0.12 | 0.17 | 1.39                        | 2.28 | 2.71 | 0.18                    | 0.27 | 0.38 | 1.55                    | 2.70 | 3.54 |
|                           | Track C | 0.12                      | 0.15 | 0.24 | 3.47                        | 3.41 | 6.72 | 0.33                    | 0.39 | 0.51 | 2.02                    | 3.54 | 4.46 |
| Non-expert<br>Operator #5 | Track A | 0.10                      | 0.13 | 0.21 | 2.23                        | 3.31 | 4.17 | 0.22                    | 0.40 | 0.49 | 1.91                    | 3.22 | 4.19 |
|                           | Track B | 0.04                      | 0.11 | 0.17 | 1.45                        | 2.89 | 3.41 | 0.18                    | 0.29 | 0.36 | 1.62                    | 2.99 | 3.57 |
|                           | Track C | 0.11                      | 0.14 | 0.25 | 3.59                        | 3.87 | 5.12 | 0.31                    | 0.35 | 0.37 | 1.99                    | 3.11 | 4.49 |

**Table 6**

Task performance metrics of our PiLSTM-based approach and other approaches ( $T_{o,A} = 150$  s,  $T_{o,B} = 90$  s,  $T_{o,C} = 250$  s,  $\lambda_c = 0.5$ ,  $\lambda_t = 0.5$ )

| Operators                 | Tracks  | $S_c$ (-) |      |      | $S_t$ (-) |      |      | $S_{success}$ (-) |     |    |
|---------------------------|---------|-----------|------|------|-----------|------|------|-------------------|-----|----|
|                           |         | PiLSTM    | FOD  | WV   | PiLSTM    | FOD  | WV   | PiLSTM            | FOD | WV |
| Expert<br>Operator #1     | Track A | 0.85      | 0.76 | 0.66 | 0.89      | 0.84 | 0.74 | 1                 | 1   | 0  |
|                           | Track B | 0.88      | 0.80 | 0.77 | 0.96      | 0.89 | 0.86 | 1                 | 1   | 1  |
|                           | Track C | 0.81      | 0.76 | 0.66 | 0.84      | 0.81 | 0.73 | 1                 | 0   | 0  |
| Expert<br>Operator #2     | Track A | 0.84      | 0.74 | 0.69 | 0.87      | 0.78 | 0.73 | 1                 | 0   | 0  |
|                           | Track B | 0.87      | 0.78 | 0.75 | 0.91      | 0.88 | 0.85 | 1                 | 1   | 1  |
|                           | Track C | 0.79      | 0.75 | 0.65 | 0.80      | 0.79 | 0.69 | 0                 | 0   | 0  |
| Expert<br>Operator #3     | Track A | 0.86      | 0.79 | 0.77 | 0.88      | 0.84 | 0.83 | 1                 | 1   | 1  |
|                           | Track B | 0.89      | 0.79 | 0.75 | 0.93      | 0.87 | 0.85 | 1                 | 1   | 1  |
|                           | Track C | 0.84      | 0.76 | 0.64 | 0.87      | 0.84 | 0.73 | 1                 | 1   | 0  |
| Non-expert<br>Operator #4 | Track A | 0.78      | 0.63 | 0.52 | 0.82      | 0.59 | 0.55 | 1                 | 0   | 0  |
|                           | Track B | 0.79      | 0.76 | 0.74 | 0.89      | 0.87 | 0.86 | 1                 | 1   | 1  |
|                           | Track C | 0.69      | 0.53 | 0.48 | 0.72      | 0.57 | 0.53 | 0                 | 0   | 0  |
| Non-expert<br>Operator #5 | Track A | 0.71      | 0.59 | 0.50 | 0.89      | 0.74 | 0.56 | 1                 | 0   | 0  |
|                           | Track B | 0.79      | 0.77 | 0.61 | 0.81      | 0.85 | 0.78 | 1                 | 1   | 0  |
|                           | Track C | 0.65      | 0.51 | 0.47 | 0.76      | 0.69 | 0.56 | 0                 | 0   | 0  |

to a significant improvement in both performance and transparency metrics for Operator #1, despite the presence of delays, as illustrated by the velocity and force feedback tracking metrics presented in Fig. 14. Specifically, the lag between the WMR states  $\xi_s$  and the motion commands  $x_m$ , as well as between the environmental force feedback  $f_e$  and the operator force  $f_h$ , is markedly reduced — approaching the ideal case. For instance, at 20 s and 25 s, the delays  $T$  were compensated to approximately 0.32 s and 0.19 s for joint 1 and joint 2 in the velocity tracking, respectively. Similarly,  $T$  reduced to 0.23 s and 0.12 s at 35 s and 42 s in the force tracking, respectively. This demonstrates that the PiLSTM predictor successfully reconstructs undelayed motion commands and force feedback in the teleoperation system. Hence, it indicates a near recovery of closed-loop fidelity, with both velocity tracking and force transparency approaching the ideal case. Furthermore, the higher gain error observed in the force feedback tracking performance for delayed cases is also eliminated, thanks to our predictor-based controllers in (8). Examining the force feedback tracking of  $f_e$  against  $f_h$ , we conclude that the system becomes more transparent than in the delayed case, thereby validating the hypothesis in (10). As a result, the command-tracking performance of  $\xi_s$  against  $x_m$  approached more stable and effective levels close to the ideal case, thereby satisfying (11).

To benchmark the teleoperation performance of our PiLSTM-based teleoperation system against other methods, we also integrated the FOD and WV-based approaches into the delayed case, sequentially. The

velocity and force feedback tracking metrics for operator #1 using the FOD-based system are depicted in Fig. 15, and for the WV-based system in Fig. 16. Although these methods achieved lower tracking errors compared to the delayed case, they still exhibit significantly higher tracking errors compared to the PiLSTM-based system. This discrepancy is due to larger lags between the output trajectories of velocities and the force feedback compared to those of the PiLSTM-based system. For example, the delays  $T$  were compensated to approximately 0.62 s and 1.09 s for velocity tracking in joint 1 using FOD and WV, respectively, compared to 0.32 s for the PiLSTM. Similarly,  $T$  reduced to 0.75 s and 1.1 s for force tracking in joint 1 using FOD and WV, respectively, compared to 0.23 s for the PiLSTM.

Furthermore, to provide a comprehensive comparison of the effectiveness of our PiLSTM-based system against the FOD and WV, the tracking performance,  $\Omega_n$ , and force transparency,  $\Gamma_n$ , metrics for all operators and tracks are summarized in Table 5. The results demonstrate that the PiLSTM-based system consistently achieves the lowest error in both performance and transparency metrics compared to the other two methods. The best performance and transparency metrics for the PiLSTM-based system were achieved by Operator #1 and Operator #2 on Track B with a  $\Omega_n$  of 0.02 m/s, and a  $\Gamma_n$  of 0.1 N. Notably, the WV-based system even underperforms the baseline delayed case in some instances. Such as the performance metrics,  $\Omega_n$ , shaded in brown (0.26 m/s and 6.72 rad/s), indicate that this method can amplify the negative effects of delays. The relative errors across the three methods,

**Table 7**

Comparative analysis of the various delay compensation techniques [2–4].

| Criteria                                 | Smith predictor             | Adaptive control                         | Robust control                                     | Proposed PiLSTM predictor                                                            |
|------------------------------------------|-----------------------------|------------------------------------------|----------------------------------------------------|--------------------------------------------------------------------------------------|
| Model dependency                         | High (exact model required) | Moderate (adaptive updates)              | High (uncertainty bounds)                          | None (model-free, relies on historical data)                                         |
| Nonlinear and temporal dynamics handling | Poor (uses linear model)    | Moderate (struggles with rapid dynamics) | Limited (handles bounded uncertainty)              | Strong (LSTM learns complex nonlinearity and temporal patterns)                      |
| Delay adaptability                       | Poor (fixed delay mostly)   | Good (adaptive under fixed condition)    | Moderate (robust bounds at expense of performance) | High (learned and adapts to variable delays through recursive feedback in real-time) |
| Sensitivity to mismatch                  | High (suffers model error)  | High (degrade with unmodeled dynamics)   | Moderate (induced uncertainty)                     | Low (robust against modeling error)                                                  |
| Computational complexity                 | Low                         | Moderate                                 | High                                               | Moderate (LSTM inference)                                                            |
| Force feedback fidelity                  | Low (no haptic modeling)    | Moderate (possible with added observer)  | Low (focus on stability over transparency)         | High (enhances transparency via learned feedback prediction)                         |
| Generalization across unknown trajectory | Poor (task-specific)        | Moderate                                 | Poor (no adaptation to unknown)                    | Strong (learn spatiotemporal behavior from various scenario)                         |
| Implementation flexibility               | Easy                        | Moderate (tuning required)               | Complex (LMI solvers)                              | Moderate (requires training)                                                         |

**Table 8**

Works related to WMR bilateral teleoperation with learning-based approach.

| Author                                 | DNN type and purpose                                        | Delay type and value               | Incorporating wheel–terrain interaction | Force feedback                              | Operational variability                                  | Robustness and adaptability                                                        |
|----------------------------------------|-------------------------------------------------------------|------------------------------------|-----------------------------------------|---------------------------------------------|----------------------------------------------------------|------------------------------------------------------------------------------------|
| E. Ślawniński et al. [44]              | LSTM on remote site: wheel–terrain interaction compensation | Small constant delays: 0.5 s       | Yes                                     | Based on lateral velocity and damping force | 3 operators, 1 pre-defined track                         | Limited adaptability varying delays and diverse trajectories                       |
| C. Tian et al. [43]                    | RL on local site: control error compensation                | Small constant delays: 0.1 s       | Yes                                     | No                                          | 0 operators, 3 trajectories                              | Limited performance for different operators                                        |
| X. Zhou et al. [45]                    | LSTM on both local and remote site: Delay compensation      | Small varying delays: up to 0.5s   | No                                      | No                                          | 1 operator, 2 pre-defined and 3 non-defined trajectories | Poor precision for human-input trajectory                                          |
| A. Abubakar et al. [46]                | LSTM on both local and remote site: Delay compensation      | large Constant delays: up to 1 s   | Yes                                     | Based on terrain-induced velocity loss      | 1 operator, 1 pre-defined trajectory                     | Lacks adaptability to variation in delays and generalization to unknown trajectory |
| Our proposed PiLSTM predictor approach | PiLSTM on both local and remote sites: Delay compensation   | Large variable delay: up to 1.25 s | Yes                                     | Based on slippage-induced velocity loss     | 5 operators, 3 tracks                                    | Robust across varied scenarios, with higher adaptability to delay variations       |

with the ideal and delayed cases serving as baselines, are depicted in Figs. 17 and 18 for the average tracking performance ( $\Omega_{n,avg}$ ) and force transparency metrics ( $\Gamma_{n,avg}$ ), respectively. As illustrated, the PiLSTM-based system consistently achieves the lowest errors, approaching the ideal case for all operators and tracks. Specifically, for the average performance metrics,  $\Omega_{n,avg}$ , the PiLSTM-based system records a mean error of 27.55%, significantly outperforming the FOD and WV methods, which exhibit mean errors of 47.72% and 70.64%, respectively. This indicates a tracking performance improvement of 20.17% and 43.09% over the FOD and WV methods, respectively. Similarly, for the average force transparency metrics,  $\Gamma_{n,avg}$ , the PiLSTM-based system demonstrates a mean error of 14.07%, compared to 24.79% for the FOD method and 32.72% for the WV method, representing transparency improvements of 10.72% and 18.65%, respectively. Thus, the lowest metrics observed in the PiLSTM-based system highlight its effectiveness

in achieving more robust and high-fidelity closed-loop integration with improved measurement accuracy.

Moreover, the linear tracking performance metrics  $\Omega_n - x_{mv}$  directly influence the longitudinal slippage, which often leads to path deviations quantified by the angular tracking performance metrics  $\Omega_n - x_{mo}$ . Higher values of these metrics indicate higher slippage and greater travel reduction and path deviations, while lower values correspond to lower slippage and minimal travel reduction and path deviation by the WMR system. For instance, as shown in Table 5, Operator 1 achieved an  $\Omega_n - x_{mv}$  of 0.07 m/s and an  $\Omega_n - x_{mo}$  of 1.82 rad/s with the PiLSTM-based WMR system on Track C. These values are significantly lower than those recorded for the FOD and WV-based WMR systems on the same track, which observed  $\Omega_n - x_{mv}$  values of 0.13 m/s and 0.19 m/s, and  $\Omega_n - x_{mo}$  values of 3.06 rad/s and 5.98 rad/s, respectively. This improvement can be attributed to the relatively lower force transparency metrics,  $\Gamma_n - x_{mv}$ , observed with the

![Figure 13: Delayed case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.](7bed2d7c96d86bf922295a1252da52a5_img.jpg)

Figure 13: Delayed case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.

**Fig. 13.** Delayed case — Operator #1 on track A: Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. Due to the introduced communication delay of 1.25 s, force tracking performance is significantly undermined in the system response by the PD-like controller.

![Figure 14: PiLSTM Predicted case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.](3468bcffa38de23cef94bfb460ccb301_img.jpg)

Figure 14: PiLSTM Predicted case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.

**Fig. 14.** PiLSTM Predicted case — Operator #1 on track A: Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. With the same delays, the PiLSTM predictor framework achieves better force tracking performance, resulting in a more stable and transparent system response.

PiLSTM-based WMR system, resulting in enhanced slippage awareness. The consistent trend across all cases demonstrates that the PiLSTM-based WMR system exhibits significantly reduced slippage and minimal path deviations compared to the FOD and WV-based WMR systems, thereby leading to better command-tracking performance.

The teleoperation performance analysis revealed several notable observations, including: (i) the PiLSTM-based system has the best performance and transparency metrics on Track B, attributed to the straight-line trajectory; (ii) the average transparency metrics were more adversely impacted by delays compared to the average performance metrics, primarily due to the diminished force feedback as undermined by the derivative gain.

## 5.3. Task performance evaluation

This section evaluates the task performance improvement of the proposed PiLSTM-based teleoperation system over the benchmark appro

![Figure 15: FOD Predicted case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.](4e7f11ebd82a34bb69e271477038b901_img.jpg)

Figure 15: FOD Predicted case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.

**Fig. 15.** FOD Predicted case — Operator #1 on track A: Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. With delays, the FOD predictor framework still exhibits greater lags than PiLSTM, resulting in a less transparent system response.

![Figure 16: WV Predicted case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.](8f223b4a29a6070b2489baf2ca803465_img.jpg)

Figure 16: WV Predicted case — Operator #1 on track A. Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. The figure consists of four subplots: Velocity tracking (m/s) vs Joint1-time (s), Velocity tracking (rad/s) vs Joint2-time (s), Force feedback tracking (N) vs Joint1-time (s), and Force feedback tracking (N) vs Joint2-time (s). Each subplot compares the motion command (red solid line) and the predicted motion command (blue dashed line) for velocity, and the force feedback (red solid line) and the predicted force feedback (blue dashed line) for force. Insets show zoomed-in views of specific time intervals with delay markers.

**Fig. 16.** WV Predicted case — Operator #1 on track A: Performance and transparency metrics comparison of motion commands (top) and force feedbacks (bottom), respectively. With the delays, the WV framework maintains stability but lacks transparency in system response (no lag reduction).

aches — FOD and WV systems — based on the task performance metrics. The ideal case is still adopted as the baseline to extract accurate waypoints along the centerlines and establish the optimal track completion time for each of the three tracks (A, B, and C).

The task performance metrics are computed and summarized in Table 6 among the three comparative approaches. The results demonstrate the practical impact of the PiLSTM-based system in terms of centerline following adherence score ( $S_c$ ), time efficiency score ( $S_t$ ), and overall success rate ( $S_{\text{success}}$ ). Across all operators and tracks, the PiLSTM approach consistently achieved the highest  $S_c$  scores, reflecting better adherence to the predefined track centerline. Concurrently, it maintained higher  $S_t$  values, ensuring faster task completion without excessive deviations.

Notably, PiLSTM exhibited strong performance even for non-expert operators, highlighting its robustness in assisting users with minimal teleoperation experience. The success rate analysis further confirms PiLSTM's advantage, achieving full success in 12 out of 15 cases, significantly outperforming FOD, which succeeded in only 8 out of 15

![Figure 17: Average tracking performance metrics Ω_n,avg (%) across all operators and tracks. The figure consists of five subplots for Operator #1 to Operator #5. Each subplot shows bars for Track A, Track B, and Track C for five cases: Ideal Case (green), PiLSTM (Ours) (yellow), FOD (orange), WV (dark red), and Delayed Case (red). The y-axis ranges from 0 to 100. PiLSTM consistently shows the lowest values, indicating better tracking performance.](96a7eac66ef72bb016c280278506ac63_img.jpg)

| Operator    | Track   | Ideal Case | PiLSTM (Ours) | FOD | WV  | Delayed Case |
|-------------|---------|------------|---------------|-----|-----|--------------|
| Operator #1 | Track A | 0          | 22            | 46  | 64  | 100          |
|             | Track B | 0          | 15            | 36  | 43  | 100          |
|             | Track C | 0          | 28            | 51  | 85  | 100          |
| Operator #2 | Track A | 0          | 24            | 46  | 72  | 100          |
|             | Track B | 0          | 13            | 37  | 46  | 100          |
|             | Track C | 0          | 28            | 47  | 77  | 100          |
| Operator #3 | Track A | 0          | 22            | 49  | 76  | 100          |
|             | Track B | 0          | 15            | 40  | 58  | 100          |
|             | Track C | 0          | 30            | 56  | 69  | 100          |
| Operator #4 | Track A | 0          | 41            | 55  | 89  | 100          |
|             | Track B | 0          | 19            | 42  | 56  | 100          |
|             | Track C | 0          | 51            | 56  | 100 | 100          |
| Operator #5 | Track A | 0          | 37            | 52  | 74  | 100          |
|             | Track B | 0          | 20            | 45  | 61  | 100          |
|             | Track C | 0          | 50            | 58  | 90  | 100          |

Figure 17: Average tracking performance metrics Ω\_n,avg (%) across all operators and tracks. The figure consists of five subplots for Operator #1 to Operator #5. Each subplot shows bars for Track A, Track B, and Track C for five cases: Ideal Case (green), PiLSTM (Ours) (yellow), FOD (orange), WV (dark red), and Delayed Case (red). The y-axis ranges from 0 to 100. PiLSTM consistently shows the lowest values, indicating better tracking performance.

**Fig. 17.** Average tracking performance metrics  $\Omega_{n,avg}$  across all operators and tracks. Smaller  $\Omega_{n,avg}$  indicates better command-tracking performance in the teleoperation. The PiLSTM-based system achieved an improved average performance metric of 20.17% and 43.09% compared to the FOD and WV-based systems, respectively.

![Figure 18: Average force transparency metrics Γ_n,avg (%) across all operators and tracks. The figure consists of five subplots for Operator #1 to Operator #5. Each subplot shows bars for Track A, Track B, and Track C for five cases: Ideal Case (green), PiLSTM (Ours) (yellow), FOD (orange), WV (dark red), and Delayed Case (red). The y-axis ranges from 0 to 100. PiLSTM consistently shows the lowest values, indicating better slippage awareness.](f85bf99d372e735d228361bf4d3cf7e6_img.jpg)

| Operator    | Track   | Ideal Case | PiLSTM (Ours) | FOD | WV | Delayed Case |
|-------------|---------|------------|---------------|-----|----|--------------|
| Operator #1 | Track A | 0          | 14            | 25  | 31 | 100          |
|             | Track B | 0          | 8             | 18  | 25 | 100          |
|             | Track C | 0          | 15            | 27  | 32 | 100          |
| Operator #2 | Track A | 0          | 15            | 25  | 36 | 100          |
|             | Track B | 0          | 11            | 18  | 27 | 100          |
|             | Track C | 0          | 16            | 27  | 36 | 100          |
| Operator #3 | Track A | 0          | 10            | 25  | 37 | 100          |
|             | Track B | 0          | 10            | 18  | 27 | 100          |
|             | Track C | 0          | 15            | 27  | 34 | 100          |
| Operator #4 | Track A | 0          | 16            | 29  | 38 | 100          |
|             | Track B | 0          | 14            | 23  | 31 | 100          |
|             | Track C | 0          | 21            | 31  | 40 | 100          |
| Operator #5 | Track A | 0          | 17            | 29  | 38 | 100          |
|             | Track B | 0          | 15            | 26  | 29 | 100          |
|             | Track C | 0          | 20            | 27  | 36 | 100          |

Figure 18: Average force transparency metrics Γ\_n,avg (%) across all operators and tracks. The figure consists of five subplots for Operator #1 to Operator #5. Each subplot shows bars for Track A, Track B, and Track C for five cases: Ideal Case (green), PiLSTM (Ours) (yellow), FOD (orange), WV (dark red), and Delayed Case (red). The y-axis ranges from 0 to 100. PiLSTM consistently shows the lowest values, indicating better slippage awareness.

**Fig. 18.** Average force transparency metrics  $\Gamma_{n,avg}$  across all operators and tracks. Smaller  $\Gamma_{n,avg}$  indicates better slippage awareness in the teleoperation. The PiLSTM-based system achieved improved average transparency metrics of 10.72% and 18.65% compared to the FOD and WV-based systems, respectively.



cases, and WV, which succeeded in just 5 out of 15 cases. Overall, the PiLSTM approach achieved the highest success rate of 80.0%, compared to 53.3% for FOD and 33.3% for WV, underscoring its effectiveness as the most reliable teleoperation approach. Therefore, these experimental results further underscore the adaptability and generalizability of the PiLSTM framework for WMR teleoperation systems, as demonstrated by its consistently superior tracking and task performance metrics.

Furthermore, the statistical validity of the observed improvements is essential to ensure that the differences are meaningful and not due to chance or operator variability. Accordingly, a paired t-tests were conducted to compare the task performance metrics between the PiLSTM-based approach and the baseline FOD and WV approaches. The paired t-tests were selected for this study, as it compares two related samples (i.e., each operator performed the same tracks under different conditions), thus allowing us to assess whether the differences in task performance metrics are significant and practically meaningful [4]. The following hypotheses were tested for each pairwise comparison:

- Null Hypothesis ( $H_0$ ): There is no statistically significant difference in performance between the PiLSTM-based approach and the respective baseline method (FOD or WV).
- Alternative Hypothesis ( $H_A$ ): There exists a statistically significant difference in performance between the PiLSTM-based approach and the respective baseline method.

A significance level of  $\alpha = 0.05$  was adopted, following standard statistical practice [10,37]. A  $p$ -value less than 0.05 indicates statistical significance, justifying rejection of the null hypothesis in favor of the alternative. In addition to hypothesis testing, the effect size for each comparison is used to quantify the magnitude of the observed differences, providing insight into interpreting the practical meaningful of the results. Specifically, Cohen's  $d$  was employed as the effect size measure, calculated as:  $d = \frac{\mu_1 - \mu_2}{\sigma}$ , where  $\mu_1$  and  $\mu_2$  are the sample means for the PiLSTM-based approach and the baseline method, respectively, and  $\sigma$  is the pooled standard deviation. According to established interpretation guidelines,  $d \ge 0.6$  indicates a moderate to large effect, and  $d \ge 0.9$  signifies a large effect.

Based on the reported performance metrics in Table 6, all pairwise comparisons between the PiLSTM approach and the other approaches yielded  $p$ -values below 0.05, confirming the statistical significance of the improvements in  $S_c$ ,  $S_t$ , and  $S_{\text{success}}$ . Moreover, the effect size analysis for each comparison supports these findings. Specifically, comparisons between PiLSTM and FOD predominantly demonstrated moderate to large effect ( $d \ge 0.7$ ), with few reaching large-effect. Whereas comparisons with WV yielded large effect sizes in all cases. These results collectively affirm that the task performance improvement introduced by the PiLSTM-based approach are both statistically significant and practically meaningful, rather than being due to random variability. The consistency of these performance gains across operators and task tracks indicates that the improvements are systematic and unlikely to have occurred by chance. Therefore, the statistical analysis confirms that the PiLSTM-based approach significantly outperforms both FOD and WV approaches in terms of teleoperation task performance.

## 5.4. Comparative analysis with other teleoperation approaches

In addition to benchmarking the proposed learning-based PiLSTM predictor against other model-free approaches, such as FOD [21] and passivity-based methods like WV [20], it is important to compare our approach with other model-based delay compensation techniques. This includes Smith predictors [29], adaptive control [9, 32,34], and robust control frameworks [33,65]. These model-based methods have been widely used in the literature to handle communication delays in teleoperated WMR systems. Table 7 summarizes the key performance and design characteristics distinguishing the proposed learning-based PiLSTM framework from existing model-based delay

compensation techniques. This comparative analysis draws from [2–4], classical control theory, and empirical evidence from experimental results of this work.

Furthermore, Table 8 presents a comprehensive comparison between the proposed learning-based approach and existing learning approaches applied to delayed WMR teleoperation. The comparison highlights the unique contributions and enhanced versatility of our framework, particularly in its integration of DNN-based techniques for delay-resilient and slippage-aware control.

## 5.5. Limitations of the PiLSTM framework in actual lunar settings

The proposed PiLSTM framework is a data-driven predictor that does not depend on empirical models like the terramechanic or dynamics models for WMR on soft terrains. Consequently, the framework is less sensitive to the exact terrain or robot model and is designed to handle uncertain dynamics and unknown conditions. The primary limitation we foresee is that slippage estimation, which could be impacted by terrain heterogeneity, might be less accurate in actual lunar conditions. While this issue is outside the scope of this current work, it represents a potential avenue for future research. Also, the abrupt transitions in regolith composition may lead to sudden changes in slippage, which could result in non-transparent force feedback during bilateral teleoperation.

# 6. Conclusion

In this work, a PiLSTM-based delay compensation framework is presented for bilateral teleoperation of WMRs on soft terrain with interaction force feedback subjected to large network delays. These large delays degrade the fidelity of the closed-loop integration, resulting in reduced slippage awareness and poor command-tracking performance. We leverage the sequence-learning capabilities of LSTM to infer strong complex and temporal dynamics from delayed data to improve prediction performance over the conventional predictors. Due to the inability of purely LSTM models to extrapolate complex dynamics, we integrate FOD dynamics constraints into the learning process and a feedback mechanism to enhance the predictor's adaptability and generalization for complex systems and delay variation. After conducting a series of human-in-the-loop experiments, our results reveal that the developed PiLSTM predictor framework improves prediction performance by 29.7% compared to the FOD framework, demonstrating robustness in large delay compensation across varied scenarios. We further validate the PiLSTM framework's effectiveness in the bilateral teleoperation system. The PiLSTM-based teleoperation system achieves tracking performance metric improvements of 20.17% and 43.09%, and force transparency metric improvements of 10.72% and 18.65% over the FOD and WV-based teleoperation systems, respectively. These results prove the PiLSTM framework's ability to restore closed-loop teleoperation fidelity, which enhance slippage awareness through a more transparent force feedback. Consequently, the system achieved significantly better command-tracking performance, characterized by reduced travel loss, minimized path deviation, and improved task success rates — 26.7% and 46.7% higher than those of the FOD and WV-based systems, respectively — during WMR teleoperation.

This research highlights the PiLSTM framework's potential to enhance closed-loop fidelity for terrain traversability of teleoperated WMRs in planetary exploration in presence of network delays. However, the framework presents some limitations: its real-time deployment on resource-constrained hardware platforms — such as Jetson Nano or FPGAs — may be hindered by inference latency. The predictor requires retraining for different teleoperation system under stationary delay profiles, and its performance may degrade when exposed to non-stationary delay profile. Moreover, the requirement for explicit delay acquisition is often impractical in real deployments.

Future work may explore reducing the network's structural complexity to enable efficient embedded deployment. A hybrid approach combining PiLSTM with model-based techniques could enhance performance under complex and unforeseen delay conditions. Additionally, integrating online learning would enable the predictor to adapt well in real time based on the evolving behavior of the coupling variables, thereby improving long-term robustness in highly dynamic scenarios. Further experimental validation under varying payload conditions and across diverse terrain types — such as ice, mud, or inclined surfaces — can be pursued to broaden the applicability and demonstrate the generalization capability of the proposed framework. Although obstacle avoidance was not addressed in the current study due to the constraints of the bilateral teleoperation setup, it remains critical to ensure safe teleoperation in cluttered and narrow passage environments. Notably, the modular architecture of the proposed PiLSTM system allows for seamless integration with force feedback-based obstacle avoidance, a direction to be explored in future work for enhancing system safety and operator situational awareness.

# CRediT authorship contribution statement

**Ahmad Abubakar:** Writing – original draft, Validation, Methodology, Investigation, Formal analysis, Conceptualization. **Yahya Zweiri:** Writing – review & editing, Supervision. **Abdel Gafoor Haddad:** Validation, Investigation. **Mubarak Yakubu:** Software, Formal analysis. **Ruqayya Alhammadi:** Writing – review & editing, Visualization. **Lakmal Seneviratne:** Writing – review & editing, Supervision, Investigation, Funding acquisition, Conceptualization.

# Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# Acknowledgments

This work was funded by the Khalifa University Center for Autonomous Robotic Systems under Award No. RC1-2018-KUCARS and partly supported by Mohammed Bin Rashid Space Centre. The author(s) wish to acknowledge the Advanced Research and Innovation Center (ARIC) and technical support provided by the team from Mohammed Bin Rashid Space Centre (MBRSC) during their visits. We extend our thanks to Prof. Kaspar Althoefer, Prof. Jorge .M. Dias, and Dr. Irfan Hussain for their constructive comments and suggestions.

# Data availability

Data will be made available on request.

# References

- [1] C. Li, Y. Tang, Y. Zheng, P. Jayakumar, T. Ersal, Modeling human steering behavior in teleoperation of unmanned ground vehicles with varying speed, *Hum. Factors* 64 (3) (2022).
- [2] M. Moniruzzaman, A. Rassau, D. Chai, S.M.S. Islam, Teleoperation methods and enhancement techniques for mobile robots: A comprehensive survey, *Robot. Auton. Syst.* 150 (2022) 103973.
- [3] S.N.F. Nahri, S. Du, B.J. Van Wyk, A review on haptic bilateral teleoperation systems, *J. Intell. Robot. Syst. Theory Appl.* 104 (1) (2022).
- [4] S. Opiyo, J. Zhou, E. Mwangi, W. Kai, I. Sumusi, A review on teleoperation of mobile ground robots: Architecture and situation awareness, *Int. J. Control. Autom. Syst.* 19 (3) (2021) 1384–1407.
- [5] F. Sasaki Aoki, R. Yamashina, R. Kurazume, Teleoperation by seamless transitions in real and virtual world environments, *Robot. Auton. Syst.* 164 (2023) 104405.
- [6] R. Alhammadi, Y. Zweiri, A. Abubakar, M. Yakubu, L. Abuassi, L. Seneviratne, Event-based slip estimation framework for space rovers traversing soft terrains, *IEEE Access* (2024) Access-2024-26979.
- [7] A. Abubakar, R. Alhammadi, Y. Zweiri, L. Seneviratne, Advance simulation method for wheel-terrain interactions of space rovers: A case study on the UAE rashid rover, in: 21st International Conference on Advanced Robotics, No. December, (2023) 526–532 Abu Dhabi, UAE, 2023.
- [8] W. Li, N. Yang, J. Wang, D. Ren, Kinematic teleoperation of wheeled mobile robot with slippage compensation on soft terrains, *IEEE Access* 7 (2019) 110982–110991.
- [9] B. Das, G. Dobie, Delay compensated state estimation for telepresence robot navigation, *Robot. Auton. Syst.* 146 (2021) 103890.
- [10] R. Luz, J. Corujeira, J.L. Silva, R. Ventura, Traction awareness through haptic feedback for the teleoperation of UGVs, in: 27th IEEE International Symposium on Robot and Human Interactive Communication, RO-MAN, Nanjing, China, 2018, pp. 313–331.
- [11] M. Sajjadi, M. Chahari, H. Salarieh, Haptic tele-driving design of vehicle steering control system with communication delay under complicated driving and road conditions, *Proc. Inst. Mech. Eng. Part D: J. Automob. Eng.* (2024) 09544070241261111.
- [12] W. Li, et al., Semi-autonomous bilateral teleoperation of six-wheeled mobile robot on soft terrains, *Mech. Syst. Signal Process.* 133 (2019) 106234.
- [13] W. Li, N. Yang, J. Wang, Z. Deng, Teleoperation of wheeled mobile robots subject to longitudinal slipping and lateral sliding by time-domain passivity controller, *Mechatronics* 81 (2022).
- [14] W. Li, J. Guo, L. Ding, J. Wang, H. Gao, Slippage-dependent teleoperation of wheeled mobile robots on soft terrains, *IEEE Robot. Autom. Lett.* 6 (3) (2021) 4962–4969.
- [15] W. Li, J. Guo, L. Ding, J. Wang, H. Gao, Z. Deng, Teleoperation of wheeled mobile robot with dynamic longitudinal slippage, *IEEE Trans. Control Syst. Technol.* 31 (1) (2023) 99–113.
- [16] M. Alzaabi, et al., Operational concepts and rehearsal results of the first emirates lunar rover: Rashid-1, *Space Sci. Rev.* 220 (8) (2024) 84, <http://dx.doi.org/10.1007/s11214-024-01118-6>.
- [17] M. Höyhtyä, Satellite communications and networks, in: Textbooks in Telecommunication Engineering, Springer Nature Switzerland, Cham, 2025, <http://dx.doi.org/10.1007/978-3-031-72927-0>.
- [18] Y. Zheng, M.J. Brudnak, P. Jayakumar, J.L. Stein, T. Ersal, A predictor-based framework for delay compensation in networked closed-loop systems, *IEEE/ASME Trans. Mechatronics* 23 (5) (2018) 2482–2493.
- [19] M. Tonutti, E. Ruffaldi, A. Cattaneo, C.A. Avizzano, Robust and subject-independent driving manoeuvre anticipation through domain-adversarial recurrent neural networks, *Robot. Auton. Syst.* 115 (2019) 162–173.
- [20] W. Li, L. Ding, H. Gao, M. Tavakoli, Haptic tele-driving of wheeled mobile robots under nonideal wheel rolling, kinematic control and communication time delay, *IEEE Trans. Syst. Man Cybern. Syst.* 50 (1) (2020) 336–347.
- [21] A. Abubakar, Y. Zweiri, R. Alhammadi, M.B. Mohiuddin, M. Yakubu, L. Seneviratne, Predictor-based control for delay compensation in bilateral teleoperation of wheeled rovers on soft terrains, *IEEE Access* 12 (2024) 111593–111610.
- [22] Y. Zheng, M.J. Brudnak, P. Jayakumar, J.L. Stein, T. Ersal, A delay compensation framework for predicting heading in teleoperated ground vehicles, *IEEE/ASME Trans. Mechatronics* 24 (5) (2019) 2365–2376.
- [23] H.V. Quang, I. Farkhatdinov, J.-H. Ryu, Passivity of delayed bilateral teleoperation of mobile robots with ambiguous causalities: Time domain passivity approach, in: 2012 IEEE/RSJ International Conference on Intelligent Robots and Systems, Vilamoura-Algarve, Portugal, 2012, pp. 2635–2640.
- [24] M. Sierotowicz, B. Weber, R. Belder, K. Bussmann, H. Singh, M. Panzirsch, Investigating the influence of haptic feedback in rover navigation with communication delay, in: Haptics: Science, Technology, Applications: 12th International Conference, Leiden, Netherlands, 2020, pp. 527–535.
- [25] Y.-J. Pan, C. Canudas-de Wit, O. Senane, A new predictive approach for bilateral teleoperation with applications to drive-by-wire systems, *IEEE Trans. Robot.* 22 (6) (2006) 1146–1162.
- [26] I. Hassanzadeh, S.S. Moosapour, S. Mansouria, Implementation and investigation of internet-based teleoperation of a mobile robot using wave variable approach, *Proc. Inst. Mech. Eng. Part I: J. Syst. Control. Eng.* 224 (4) (2010) 471–477.
- [27] W. Li, Z. Liu, H. Gao, X. Zhang, M. Tavakoli, Stable kinematic teleoperation of wheeled mobile robots with slippage using time-domain passivity control, *Mechatronics* 39 (2016) 196–203.
- [28] E. Sławinski, V. Mut, D. Santiago, PD-like controller for delayed bilateral teleoperation of wheeled robots, *Internat. J. Control* 89 (8) (2016) 1622–1631.
- [29] M. Saków, K. Marchelek, Model-free and time-constant prediction for closed-loop systems with time delay, *Control Eng. Pract.* 81 (2018) 1–8.
- [30] H.J. Choi, S. Jung, Neural network-based smith predictor design for the time-delay in a tele-operated control system, *Artif Life Robot.* 14 (4) (2009) 578–583, <http://dx.doi.org/10.1007/s10015-009-0750-6>.
- [31] Y. Pang, H. Xia, M.J. Grimble, Resilient nonlinear control for attacked cyber-physical systems, *IEEE Trans. Syst. Man Cybern. Syst.* 50 (6) (2020) 2129–2138, <http://dx.doi.org/10.1109/TSMC.2018.2801868>.
- [32] J. Luo, D. Huang, Y. Li, C. Yang, Trajectory online adaption based on human motion prediction for teleoperation, *IEEE Trans. Autom. Sci. Eng.* 19 (4) (2022) 3184–3191.

- [33] F. Huang, X. Yang, D. Mei, Z. Chen, Unified contact model and hybrid motion/force control for teleoperated manipulation in unknown environments, *IEEE/ASME Trans. Mechatron.* (2024) 1–12, <http://dx.doi.org/10.1109/TMECH.2024.3461968>.
- [34] J. Xu, Z. Liu, M. Ge, Y. Wang, D. He, Self-triggered MPC for teleoperation of networked mobile robotic system via high-order estimation, *IEEE Trans. Autom. Sci. Eng.* 22 (2025) 6037–6049, <http://dx.doi.org/10.1109/TASE.2024.3436922>.
- [35] X. Yang, F. Huang, J. Gu, Z. Chen, Bilateral teleoperation control using unified interactive model for manipulation in contact environment\*, in: 2023 IEEE International Conference on Robotics and Biomimetics, ROBIO, IEEE, Koh Samui, Thailand, 2023, pp. 1–6.
- [36] Y. Lin, Z. Chen, B. Yao, Unified motion/force/impedance control for manipulators in unknown contact environments based on robust model-reaching approach, *IEEE/ASME Trans. Mechatron.* 26 (4) (2021) 1905–1913.
- [37] Y. Zheng, M.J. Brudnak, P. Jayakumar, J.L. Stein, T. Ersal, Evaluation of a predictor-based framework in high-speed teleoperated military UGVs, *IEEE Trans. Human-Machine Syst.* 50 (6) (2020) 561–572.
- [38] D.J. Gorsich, P. Jayakumar, M.P. Cole, C.M. Crean, A. Jain, T. Ersal, Evaluating mobility vs. latency in unmanned ground vehicles, *J. Terramechanics* 80 (2018) 11–19.
- [39] N. Sridhar, R. Lima, U. Rai, V. Vakharia, K. Das, B. P., Transparency enhancement in teleoperation: An improved model-free predictor for varying network delay in telerobotic application, in: 2021 European Control Conference, Delft, Netherlands, 2021.
- [40] S. Guo, Y. Liu, Y. Zheng, T. Ersal, A delay compensation framework for connected testbeds, *IEEE Trans. Syst. Man Cybern.: Syst.* 52 (7) (2022) 4163–4176.
- [41] S. Timman, M. Landgraf, C. Haskamp, S. Lizy-destrez, F. Dehais, Effect of time-delay on lunar sampling tele-operations : Evidences from cardiac, ocular and behavioral measures, *Appl. Ergon.* 107 (2020) (2023) 103910.
- [42] H. Su, W. Qi, C. Yang, J. Sandoval, G. Ferrigno, E.D. Momi, Deep neural network approach in robot tool dynamics identification for bilateral teleoperation, *IEEE Robot. Autom. Lett.* 5 (2) (2020) 2943–2949.
- [43] C. Tian, S. Shaik, Y. Wang, Deep reinforcement learning for shared control of mobile robots, *IET Cyber-Syst. Robot.* 3 (4) (2021) 315–330.
- [44] E. Śląwiński, F. Rossomando, F.A. Chicaiza, J. Moreno-Valenzuela, V. Mut, LSTM network in bilateral teleoperation of a skid-steering robot, *Neurocomputing* 602 (2024) 128248.
- [45] X. Zhou, Z. Yang, Y. Ren, W. Bai, B. Lo, E.M. Yeatman, Modified bilateral active estimation model: A learning-based solution to the time delay problem in robotic tele-control, *IEEE Robot. Autom. Lett.* 8 (5) (2023) 2653–2660.
- [46] A. Abubakar, Y. Zweiri, M. Yakubu, R. Alhammadi, M. Mohiuddin, A. Haddad, J. Dias, L. Seneviratne, Deep learning-based delay compensation framework for teleoperated wheeled rovers on soft terrains, in: 2024 IEEE/RSJ International Conference on Intelligent Robots and Systems, Abu-Dhabi, UAE, 2024.
- [47] S. Hutangkabodee, Y.H. Zweiri, L.D. Seneviratne, K. Althoefer, Performance prediction of a wheeled vehicle on unknown terrain using identified soil parameters, in: Proceedings 2006 IEEE International Conference on Robotics and Automation, 2006, ICRA 2006. Orlando, FL, USA, 2006, pp. 3356–3361.
- [48] Y. Zou, L. Ding, H. Zhang, T. Zhu, L. Wu, Vehicle acceleration prediction based on machine learning models and driving behavior analysis, *MDPI Appl. Sci.* (2022).
- [49] W. Li, H. Gao, L. Ding, M. Tavakoli, Trilateral predictor-mediated teleoperation of a wheeled mobile robot with slippage, *IEEE Robot. Autom. Lett.* 1 (2) (2016) 738–745.
- [50] W. Gu, S. Primatessa, A. Rizzo, Physics-informed neural network for quadrotor dynamical modeling, *Robot. Auton. Syst.* 171 (2024) 104569.
- [51] S. Cai, C. Gray, G.E. Karniadakis, Physics-informed neural networks enhanced particle tracking velocimetry: An example for turbulent jet flow, *IEEE Trans. Instrum. Meas.* 73 (2024) 1–9.
- [52] X.A. Ji, G. Orosz, Learning time delay systems with neural ordinary differential equations, *IFAC-PapersOnLine* 55 (36) (2022) 79–84.
- [53] J. Zhang, Z. Ruan, Q. Li, Z.-Q. Zhang, Toward robust and efficient musculoskeletal modeling using distributed physics-informed deep learning, *IEEE Trans. Instrum. Meas.* 72 (2023) 1–11.
- [54] F. Djeumou, C. Neary, E. Goubault, Neural networks with physics-informed architectures and constraints for dynamical systems modeling, in: Learning for Dynamics and Control Conference, PMLR, 2022, pp. 263–277.
- [55] J.Y. Wong, *Terramechanics and Off-Road Vehicle Engineering: Terrain Behaviour, Off-Road Vehicle Performance and Design*, second ed. Butterworth-Heinemann, Oxford, UK, 2010.
- [56] I. Goodfellow, Y. Bengio, A. Courville, *Deep learning*, in: Adaptive Computation and Machine Learning, The MIT Press, Cambridge, Massachusetts, 2016.
- [57] A.S. Ali, A.A. Al-Habob, S. Naser, L. Bariah, O.A. Dobre, S. Muhaidat, Deep reinforcement learning for energy-efficient data dissemination through UAV networks, *IEEE Open J. Commun. Soc.* 5 (2024) 5567–5583.
- [58] N.P. Jouppi, et al., In-datacenter performance analysis of a tensor processing unit, in: Proceedings of the 44th Annual International Symposium on Computer Architecture, ACM, Toronto ON Canada, 2017, pp. 1–12, <http://dx.doi.org/10.1145/3079856.3080246>.
- [59] Vortex Studio, Tire models – technical notes, vortex studio documentation, 2025, (Accessed 18 April 2025), [Online]. Available: <https://vortexstudio.atlassian.net/wiki/spaces/VSD2409/pages/3758339602/Tire+Models+Technical+Notes>.
- [60] R.A. Irani, R.J. Bauer, A. Warkentin, A dynamic terramechanic model for small lightweight vehicles with rigid wheels and grousers operating in sandy soil, *J. Terramechanics* 48 (4) (2011) 307–318, <http://dx.doi.org/10.1016/j.jterra.2011.05.001>.
- [61] S. Al-Milli, L.D. Seneviratne, K. Althoefer, Track–terrain modelling and traversability prediction for tracked vehicles on soft terrain, *J. Terramechanics* 47 (3) (2010) 151–160.
- [62] Zibin Song, Y.H. Zweiri, L.D. Seneviratne, K. Althoefer, Non-linear observer for slip estimation of skid-steering vehicles, in: Proceedings 2006 IEEE International Conference on Robotics and Automation, 2006. ICRA 2006, IEEE, Orlando, FL, USA, 2006, pp. 1499–1504.
- [63] W. Li, L. Ding, H. Gao, Z. Deng, N. Li, ROSTDyn: Rover simulation based on terramechanics and dynamics, *J. Terramechanics* 50 (3) (2013) 199–210.
- [64] H.L. Litaker Jr., O.S. Beaton, E.Z. Bekdash, E.J. Crues, B.A.J. Paddock, M.L. Rohde, C.M. Reagan, K.H. Van Velson, S.F. Everett, South pole lunar lighting studies for driving exploration on the lunar surface, in: Proc. 46th Int. IEEE Aerospace Conf. Big Sky, MT, USA, Mar, 2025, pp. 1–8.
- [65] P.M. Kebría, A. Khosravi, S. Nahavandi, P. Shi, R. Alizadehsani, Robust adaptive control scheme for teleoperation systems with delay and uncertainties, *IEEE Trans. Cybern.* 50 (7) (2020) 3243–3253.

**Ahmad Abubakar**, (Member, IEEE) a Ph.D. candidate at Khalifa University (KU), UAE, focuses on robotic system, with specific emphasis on Teleoperated and Autonomous wheeled mobile robots, Deep learning-based system, and controls of time-delay systems. Holding a B.Eng. in Electrical Engineering from Bayero University Kano in 2014 and an M.Sc. in System, Control, and IT from the University Grenoble Alpes (UGA), France in 2018. During his master's program, he gained significant expertise in the modeling, analysis, and control of complex systems. Ahmad's pursuits extend to practical applications through an internship at GIPSA-Lab in France. His work at Khalifa University has been pivotal in advancing the operation and control of Space rovers.

![Portrait of Ahmad Abubakar](893f3e40a8607bd256b676392d228f2a_img.jpg)

Portrait of Ahmad Abubakar

**Yahya Zweiri**, Ph.D. (Member, IEEE), obtained his Ph.D. degree from King's College London. He is currently a Professor at the Department of Aerospace Engineering and the Director of the Advanced Research and Innovation Center, Khalifa University, United Arab Emirates. Over the past two decades, he has actively participated in defense and security research projects at institutions such as the Defense Science and Technology Laboratory, King's College London, and the King Abdullah II Design and Development Bureau in Jordan. Dr. Zweiri has a prolific publication record, with over 130 refereed journals and conference papers, as well as ten filed patents in the USA and UK. His primary research focus centers around robotic systems for challenging environments, with a specific emphasis on applied AI and neuromorphic vision systems.

![Portrait of Yahya Zweiri](c2749f79dd1fc9bd2dce52bcbb2fb3ef_img.jpg)

Portrait of Yahya Zweiri

**Abdel Gafour Haddad** a Ph.D. candidate at Khalifa University (KU), UAE, focuses on robotics, with speciality in reinforcement learning-based navigation, and UAV controls. He earned his M.Sc. degree from Khalifa University, Abu Dhabi, United Arab Emirates. He is currently pursuing his Ph.D. degree in Engineering Robotics concentration at Khalifa University. His research focuses on control systems and reinforcement learning for robotics applications.

![Portrait of Abdel Gafour Haddad](2c165c8324557740c73b756866a585fa_img.jpg)

Portrait of Abdel Gafour Haddad

**Mubarak Yakubu** a Ph.D. candidate at Khalifa University (KU), UAE, focuses on robotics, with speciality in mobility concepts, reinforcement learning-based navigation, and controls. Holding a B.Eng. in Mechanical Engineering from Bayero University Kano in 2016 and an M.Sc. in Mechanical Engineering from King Fahd University of Petroleum and Minerals (KFUPM), Saudi Arabia in 2020.

![Portrait of Mubarak Yakubu](69cc2fcd39ed24264ca4981dfb4c8955_img.jpg)

Portrait of Mubarak Yakubu

![Portrait of Ruqayya Alhamadi, a woman wearing a black hijab.](05c9994c1f5daf53d0d9b107657d7a17_img.jpg)

Portrait of Ruqayya Alhamadi, a woman wearing a black hijab.

**Ruqayya Alhamadi** is currently a Ph.D. candidate at the Khalifa University (KU), Abu Dhabi, United Arab Emirates (UAE), specializing in the application of robotics in space related projects, with specific emphasis particularly wheel soil interaction in space rovers. Her primary research focus centers around neuromorphic vision systems. Holding a B.Eng. in Mechanical Engineering with minor in UAVs from Khalifa University in 2018 and an M.Sc. in Mechanical Engineering with concentration in spacecraft system from Khalifa University in 2020.

![Portrait of Lakmal Seneviratne, a man wearing glasses and a suit.](ca81500b365ed30190cb2d9c38fc1f84_img.jpg)

Portrait of Lakmal Seneviratne, a man wearing glasses and a suit.

**Lakmal Seneviratne** is Professor of Mechanical Engineering and the founding Director of the Centre for Autonomous Robotic Systems (KUCARS) at Khalifa University, UAE. Prior to joining Khalifa University, he was Professor of Mechatronics, the founding Director of the Centre for Robotics Research and the Head of the Division of Engineering, at King's College London. He has published over 400 peer reviewed publications. He is a member of the Mohammed Bin Rashid Academy of Scientists in the UAE.

