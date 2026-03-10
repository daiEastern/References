

![Check for updates button](2dfa6ac3edfe874f68aa0cbccaa42322_img.jpg)

Check for updates button

# Distortion Analysis and Compensation for a Space Contact HIL Simulator with Force Delay and Dead Zone

Dongjin Li<sup>1</sup>; Huayang Li<sup>2</sup>; Chenkun Qi<sup>3</sup>; Yan Hu<sup>4</sup>; Feng Gao<sup>5</sup>; and Xianchao Zhao<sup>6</sup>

**Abstract:** A space contact hardware-in-the-loop (HIL) simulator is a key facility for ground testing of space contact processes. It must faithfully reproduce the dynamics in space. Force delay is known to induce instability. To suppress velocity drift from noisy force signals, a dead zone is often introduced. In this study, we show that a dead zone is able to not only induce divergence, but also induce convergence. To address this issue, we propose an integrated compensator that combines a hybrid Smith predictor with a dead zone disturbance observer. It jointly addresses delay and dead zone distortions. The proposed method is effective for both divergent and convergent distortions. Verifications and applications validate the approach. **DOI: 10.1061/JAEEEZ.ASENG-6727.** © 2026 American Society of Civil Engineers.

**Author keywords:** Hardware-in-the-loop (HIL) simulation; Space contact; Force delay; Dead zone; Distortion compensation.

## Introduction

For space operation tasks, e.g., capturing, docking and assembling, the space contact of two objects is an essential process. Due to the complex contact interfaces and material properties, the space contact process can be very complicated. Therefore, ground-based simulations of the space contact process are indispensable for ensuring the safety and reliability of many space operations (Li et al. 2019; Ding et al. 2020; Opromolla et al. 2024). For ground-based simulations, constructing a zero-gravity environment is a huge challenge. To achieve this goal, we employed hardware-in-the-loop (HIL) simulation (also called hybrid simulation) in our study.

The HIL simulation combines physical and numerical simulations. It takes the advantages of high fidelity, high flexibility, and low cost (Rybus et al. 2019; De Stefano et al. 2021). The HIL simulation is used across many domains, e.g., cyber-physical system test and development (Somers et al. 2023; Li et al. 2024), ground test for space operations (Fallahiazoodar and Zhu 2025). In the HIL simulation for testing space operations, a space contact HIL simulator is a key facility. It performs contact process on real physical contact mechanisms, and numerically emulates dynamics of the spacecraft in zero-gravity environment on computers. The contact force and torque are measured by the sensor, then fed into the spacecraft dynamic model. The resulting motion is executed by motion

simulators, which in turn drive the contact mechanisms to reproduce physical contact. In general, a space contact HIL simulator reproduces the on-orbit spacecraft contact dynamics in a closed loop.

A variety of space contact HIL simulators have been developed. The German Aerospace Center developed the European Proximity Operations Simulator using two robot arms (Boge and Ma 2011; Rems et al. 2021; Renaut et al. 2025). The Canadian Space Agency developed a hydraulic HIL simulator, the Task Verification Facility, for testing the Special Purpose Dexterous Manipulator (Ma et al. 2004; Martin et al. 2005). The National Aeronautics and Space Administration (NASA) Johnson Space Center developed the Six-Degree-of-Freedom Test System for space contact simulation (Mitchell et al. 2008). The Harbin Institute of Technology developed a hydraulic six-degrees-of-freedom (DOFs) contact simulator (Chang et al. 2007). Tsinghua University and Harbin Institute of Technology developed a HIL simulator using two industrial robots (Mou et al. 2018). Tohoku University developed a dual-arm space robot ground experiment system (Takahashi et al. 2008; Osaki et al. 2010; Abiko et al. 2014). These HIL simulators provided experimental testbeds for the development and verification of on-orbit servicing and space contact technologies.

To simulate the space contact process successfully, an ideal space contact HIL simulator is supposed to measure the contact force without delay and error. But in practice, force delay and noise always exist because of the limitation of the force measurement system. The noise comes from the force sensor, analog-to-digital (AD) card, and electromagnetic interference from electric motors. Firstly, force delay will lead to instability and simulation distortion of the HIL system. The definition of the simulation distortion is given subsequently.

Secondly, measurement noise will lead to drift in the HIL system, resulting in simulation error. When there is no physical contact between the simulated spacecraft, the actual contact force should be zero, and the spacecraft is free-floating at constant velocity. But due to the presence of noise, the measured contact force is not zero, and the velocity is no longer constant but experiences an undesired drift. To eliminate the drift caused by measurement noise, a dead zone should be used (Sugai et al. 2013). The dead zone and force delay problems are particularly critical in spacecraft docking simulations because they will generate significant simulation distortion, which affects the simulation accuracy and the stability.

Some previous studies on the impact of force delay or dead zone on the HIL system will now be discussed. Corresponding compensators

<sup>1</sup>Ph.D. Student, School of Mechanical Engineering, Shanghai Jiao Tong Univ., Shanghai 200240, China. Email: ldj0807@sjtu.edu.cn

<sup>2</sup>Engineer, Science and Technology on Space Physics Laboratory, China Academy of Launch Vehicle Technology, Beijing 100076, China. Email: lihuayang231101@163.com

<sup>3</sup>Associate Professor, School of Mechanical Engineering, Shanghai Jiao Tong Univ., Shanghai 200240, China (corresponding author). Email: chenkqi@sjtu.edu.cn

<sup>4</sup>Assistant Professor, School of Mechanical Engineering, Shanghai Jiao Tong Univ., Shanghai 200240, China. Email: humman123@sjtu.edu.cn

<sup>5</sup>Professor, School of Mechanical Engineering, Shanghai Jiao Tong Univ., Shanghai 200240, China. Email: fengg@sjtu.edu.cn

<sup>6</sup>Associate Professor, School of Mechanical Engineering, Shanghai Jiao Tong Univ., Shanghai 200240, China. Email: xczhao@sjtu.edu.cn

Note. This manuscript was submitted on July 29, 2025; approved on December 15, 2025; published online on February 25, 2026. Discussion period open until July 25, 2026; separate discussions must be submitted for individual papers. This paper is part of the *Journal of Aerospace Engineering*, © ASCE, ISSN 0893-1321.

were designed. For the force delay problem, hybrid compensators combining Smith predictor and advanced control were designed to address delay problem (Yu et al. 2022). How the energy of the HIL system is increased by the delay was studied, and the energy compensation method was proposed (Osaki et al. 2010). A delay compensator based on desired coefficient of restitution of the contact was designed, where the delay was regarded as coming from the dead zone and filtering (Abiko et al. 2014). A three-dimensional (3D) non-linear system model with delay was studied, and the stability analysis was validated by energy observation (Sazawal et al. 2019). A force compensation method was proposed, considering a contact model with stiffness and damping (Qi et al. 2017a). A hybrid compensation method integrating the Smith predictor and the phase lead was designed, and its performance was better than that only using first-order phase lead (Qi et al. 2018). From these studies, we can see that energy analysis and phase-lead compensators are commonly used in research on delay.

Currently, only one work (Sugai et al. 2013) in the space contact HIL simulation field has studied the dead zone problem. In their study, two compensation methods, including the virtual damping method and force supplement method, were designed (Sugai et al. 2013). Their study only considered the first case: when the energy of the HIL simulator is generally divergent, the dead zone will make the simulator more divergent. Our study considers two cases, including the second case: when the energy of the HIL simulator is generally convergent, the dead zone will make the simulator more convergent. The definition of divergence and convergence are given subsequently. This second case is missing in their study. Moreover, the two compensation methods in this work have some limitations. The virtual damping method can reduce the divergence by adding virtual damping force, which is only applicable for the first case, and is failed for the second case. The force supplement method is to add supplement force just after the contact. This method changed the experimental result because the supplement force is not applied instantaneously.

The purpose of this paper is to investigate the distortion mechanism of the space contact hybrid simulator caused by the simultaneous existence of force delay and dead zone, and propose an effective distortion compensation method. The proposed method can also be extended to other robotic systems. The application field is the weak collision of space contact, where the contact force is small (about tens of Newtons) and the dead zone (about several Newtons) has significant effect on the HIL simulation accuracy. The cases include micro-nano satellites capture, small free-floating debris capture, and on-orbit maintenance using a space manipulator (Fallahiazarzodar and Zhu 2025; Svotina 2024).

The novelty of our work lies in the following aspects:

- We found that for the HIL simulation with the force delay and dead zone, when the energy of the HIL simulator is generally divergent, the dead zone will generate more divergent distortion; however, when the energy of the HIL simulator is generally convergent, the dead zone will generate less divergent distortion. The distortion mechanism caused by the simultaneous existence of force delay and dead zone is discovered for the first time.
- An integrated compensator combining a hybrid Smith predictor and a dead zone disturbance observer is proposed to compensate the distortion of the space contact hybrid simulator with force delay and dead zone.

This paper is organized as follows. Firstly, the HIL system is introduced and its models are given. Then by using these models for simulation, the distortion phenomena can be observed and the problem to solve can be found. Next, the distortion mechanism is given to understand the phenomena. Then, the compensation

![Schematic of the space contact HIL simulator. The diagram is divided into two main subsystems: the Physical Subsystem and the Numerical Subsystem. The Physical Subsystem (left) includes an image of the simulator hardware and internal components: Upper Motion Mechanism, Force Sensor, Active Contact Mechanism, Contact Process (Motion→Force), Passive Contact Mechanism, and Lower Motion Mechanism. The Numerical Subsystem (right) includes a Compensation Module, Spacecraft Dynamic model (Force→Motion), and Motion Transformation. Data flow: Measured Force from the Force Sensor goes to the Compensation Module. The Compensation Module sends a signal to the Spacecraft Dynamic model. The Spacecraft Dynamic model outputs a 1 ms delayed Motion Command to the Motion Transformation. The Motion Transformation outputs a Motion Command to the Lower Motion Mechanism. The Lower Motion Mechanism sends a signal back to the Contact Process. The Contact Process sends a signal to the Force Sensor, completing the loop.](715219db84ec2a5622d09f9d822b4550_img.jpg)

Schematic of the space contact HIL simulator. The diagram is divided into two main subsystems: the Physical Subsystem and the Numerical Subsystem. The Physical Subsystem (left) includes an image of the simulator hardware and internal components: Upper Motion Mechanism, Force Sensor, Active Contact Mechanism, Contact Process (Motion→Force), Passive Contact Mechanism, and Lower Motion Mechanism. The Numerical Subsystem (right) includes a Compensation Module, Spacecraft Dynamic model (Force→Motion), and Motion Transformation. Data flow: Measured Force from the Force Sensor goes to the Compensation Module. The Compensation Module sends a signal to the Spacecraft Dynamic model. The Spacecraft Dynamic model outputs a 1 ms delayed Motion Command to the Motion Transformation. The Motion Transformation outputs a Motion Command to the Lower Motion Mechanism. The Lower Motion Mechanism sends a signal back to the Contact Process. The Contact Process sends a signal to the Force Sensor, completing the loop.

Fig. 1. Schematic of space contact HIL simulator.

method is proposed. The verification and application are given too. Finally, we conclude the paper.

## Space Contact HIL Simulator

### Schematic of the Simulator

Fig. 1 shows the schematic of the space contact HIL simulator. The HIL simulator consists of two subsystems, the physical subsystem and the numerical subsystem. The physical subsystem includes a lower motion mechanism, an upper motion mechanism, a force sensor, and two contact interfaces. The contact interfaces include an active contact mechanism and a passive contact mechanism. The lower motion mechanism is a 6-DOF motor-driven parallel platform (Cao et al. 2015), which is used to reproduce the relative motion of the two simulated spacecraft. The upper motion mechanism is a 3-DOF motor-driven parallel platform used for simulating space rendezvous process. In the space contact simulation, it is usually fixed. The parallel platforms have higher structure stiffness and accuracy compared with the serial robot arms, so they are highly suitable for the HIL simulation. The two contact interfaces are the actual contact mechanisms applied on the spacecraft. In the HIL simulation, they are fixed on the motion mechanisms and will generate the complex contact process. The contact force is measured by the force sensor, then fed into the numerical subsystem.

The numerical subsystem simulates the dynamics of the spacecraft in a zero-gravity environment. It includes a dynamic model for the two spacecrafts, a compensation module, and corresponding motion transformation. The measured contact force is compensated for by the compensation module, then input into the dynamic model. The dynamic model calculates the relative motion of the spacecraft. The relative motion will be transformed to the motion command for the lower motion mechanism. In general, our space contact HIL simulator reproduces the space contact process in a closed loop, which runs at a 1-ms period.

To achieve a correct simulation, we need to match the dynamic characteristics of the space contact HIL simulator with the actual dynamic characteristics in space. Compared with the situation in space, the force delay and the dead zone are caused by the imperfection of the force measurement system in the HIL system, which will significantly affect the accuracy of the simulation. There are also many other imperfect factors, e.g., the response delay of the lower motion mechanism or the structure dynamics of two motion mechanisms, which have been discussed elsewhere (Hu et al. 2021; Qi et al. 2023). Here, we consider that they have been well compensated. In order to study the impact of the force delay and the dead

![Block diagram of the space contact HIL simulator system model. The diagram shows a feedback loop. The 'Active Contact Mechanism' block outputs 'Actual Force' F_act to the 'Force Measurement Time Delay' block. The 'Passive Contact Mechanism' block, which includes a spring-damper element with stiffness K_con and damping B_con, receives 'Actual Position' P_act from the 'Lower Motion Mechanism' and outputs 'Actual Force' F_act to the 'Force Measurement Time Delay' block. The 'Force Measurement Time Delay' block outputs 'Measured Force' F_mea to the 'Force Measurement Dead Zone' block. The 'Force Measurement Dead Zone' block outputs 'Force After Dead Zone' F_con to the 'Spacecraft Motion Model' block. The 'Spacecraft Motion Model' block outputs 'Desired Position' P_des to the 'Lower Motion Mechanism' block.](1b7d539e02a202c2cf2d97698b911447_img.jpg)

Block diagram of the space contact HIL simulator system model. The diagram shows a feedback loop. The 'Active Contact Mechanism' block outputs 'Actual Force' F\_act to the 'Force Measurement Time Delay' block. The 'Passive Contact Mechanism' block, which includes a spring-damper element with stiffness K\_con and damping B\_con, receives 'Actual Position' P\_act from the 'Lower Motion Mechanism' and outputs 'Actual Force' F\_act to the 'Force Measurement Time Delay' block. The 'Force Measurement Time Delay' block outputs 'Measured Force' F\_mea to the 'Force Measurement Dead Zone' block. The 'Force Measurement Dead Zone' block outputs 'Force After Dead Zone' F\_con to the 'Spacecraft Motion Model' block. The 'Spacecraft Motion Model' block outputs 'Desired Position' P\_des to the 'Lower Motion Mechanism' block.

Fig. 2. System model of the space contact HIL simulator.

zone on the HIL system, we establish the system models in the following sections.

### System Model Structure

As shown in Fig. 2, related models of the HIL simulator are given for simulation analysis. For the theoretical analysis, the contact between the contact interfaces is assumed to be governed by an elastic-damped contact model

$$F_{act}(t) = -K_{con}P_{act}(t) - B_{con}\dot{P}_{act}(t) \quad (1)$$

where  $K_{con}$  and  $B_{con}$  = contact stiffness and the contact damping, respectively;  $F_{act}(t)$  = actual contact force; and  $P_{act}(t)$  = actual relative position between the contact interfaces. For the force measurement system, the delay between the actual force  $F_{act}(t)$  and the measured force  $F_{mea}(t)$  is called force delay and can be modeled as a pure delay

$$F_{mea}(t) = F_{act}(t - \tau_{fd}) + E(t) \quad (2)$$

where  $\tau_{fd}$  = force delay; and  $E(t)$  = force noise, which is typically modeled as Gaussian noise. A dead zone is introduced to suppress spacecraft velocity drift induced by force noise. The dead zone model is defined as follows:

$$F_{con}(t) = \begin{cases} 0 & \text{if } |F_{mea}| \le D \\ F_{mea}(t) & \text{if } |F_{mea}| > D \end{cases} \quad (3)$$

where  $D$  = width of the dead zone, which is determined by the noise level of the measured contact force. The spacecraft motion model is employed to calculate the dynamics of the two spacecrafts. Both the target spacecraft and the servicing spacecraft under contact forces are in the zero-gravity environment. The motion of the servicing spacecraft can be described as follows:

$$M_{ser}\ddot{P}_{ser}(t) = F_{ser}(t) \quad (4)$$

where  $M_{ser}$  = mass of the service spacecraft;  $P_{ser}(t)$  is the position vector of the service spacecraft; and  $F_{ser}$  = force acting on the center of mass of the service spacecraft. Similarly, the motion model of target spacecraft can be described as follows:

$$M_{tar}\ddot{P}_{tar}(t) = F_{tar}(t) \quad (5)$$

where  $M_{tar}$  = mass of the target spacecraft;  $P_{tar}(t)$  is its position vector; and  $F_{tar}$  = force acting on its center of mass. The forces  $F_{ser}$  and  $F_{tar}$ , acting on the centers of mass of the service spacecraft and the target spacecraft, respectively, can be obtained from the contact force  $F_{con}$  after applying the dead zone

$$F_{tar}(t) = F_{con}(t) \quad (6)$$

$$F_{ser}(t) = -F_{con}(t) \quad (7)$$

The dynamics of the two spacecrafts are not the orbital dynamics. Because the duration of the space contact studied here is very short (e.g., several seconds), the orbital dynamics can be ignored, and only the relative motion of the two spacecrafts due to contact force is considered. The desired relative position  $P_{des}$  between the two spacecrafts as a result of the contact force can be obtained from Eqs. (4) and (5)

$$P_{des}(t) = P_{ser}(t) - P_{tar}(t) \quad (8)$$

In the numerical emulation, the two spacecrafts can be modeled as a single equivalent system to derive the desired relative position  $P_{des}$ . The equivalent mass is given by

$$M_{equ} = \frac{M_{ser}M_{tar}}{M_{ser} + M_{tar}} \quad (9)$$

From Eqs. (1) and (9), the natural frequency of the contact  $freq_{con}$  and the damping ratio of the contact  $\xi_{con}$  can be obtained as follows:

$$freq_{con} = \frac{1}{2\pi} \sqrt{\frac{K_{con}}{M_{equ}}} \quad (10)$$

$$\xi_{con} = \frac{B_{con}}{2\sqrt{K_{con}M_{equ}}} \quad (11)$$

For the lower motion mechanism, a tracking delay exists between the actual position  $P_{act}(t)$  and the desired position  $P_{des}(t)$ . This delay can be compensated by the response error-based force compensation. Because this study focuses on the force delay and dead zone issues, it is assumed that the tracking delay has been effectively compensated. Therefore,  $P_{act}(t) = P_{des}(t)$  is assumed in the following analysis.

## Force Delay and Dead Zone Problem

Using the system models, the distortion in the space contact HIL simulator caused by the force delay and the dead zone can be observed. A space contact process is emulated under the following conditions. For the spacecraft, the equivalent mass is 300 kg, and the initial relative velocity is 5 mm/s. Regarding the contact dynamics, the natural frequency of the contact is 3 Hz, and the contact damping ratio is chosen as either 0 or 0.1. The corresponding contact stiffness is 106.59 N/mm. The selected parameters refer to an active claw-type capture mechanism for lunar sample return (Wang et al. 2023), which has very low contact stiffness.

*Remark:* Some explanations on coefficient of restitution (CoR), divergence, convergence, and distortion are provided here. The distortion will be illustrated using  $V_{des}(t) = \dot{P}_{des}(t)$ , which is the desired relative velocity of the spacecraft computed by the spacecraft dynamic model. CoR is the ratio of the rebound velocity after the contact and the striking velocity before the contact in the HIL simulation. The HIL simulation is convergent means that the simulated velocity of the spacecraft after the contact is smaller than the simulated velocity before the contact, i.e., CoR is smaller than 1. Divergence means that the CoR is greater than 1.

From a comparative perspective, the CoR error is a quantitative criterion to describe the distortion, which is the difference between the CoR obtained from the HIL system and the ideal CoR of the contact in space. If the CoR error is positive, we say the HIL system

![Figure 3: HIL simulation divergence due to force delay. (a) Contact damping ratio = 0; (b) Contact damping ratio = 0.1. Both plots show desired relative velocity V_des (mm/s) vs Time (s) for force delays of 3ms, 3.5ms, and 4ms, and in-space contact. In (a), the 4ms delay shows significant divergence. In (b), the 4ms delay shows convergence due to damping.](e94f3bbb6f7501b9a1344dd0210e5dd8_img.jpg)

Figure 3: HIL simulation divergence due to force delay. (a) Contact damping ratio = 0; (b) Contact damping ratio = 0.1. Both plots show desired relative velocity V\_des (mm/s) vs Time (s) for force delays of 3ms, 3.5ms, and 4ms, and in-space contact. In (a), the 4ms delay shows significant divergence. In (b), the 4ms delay shows convergence due to damping.

**Fig. 3.** HIL simulation divergence due to force delay: (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1.

**Table 1.** CoR under varying force delays

| Damping ratio | In space | $\tau_{fd} = 3.0$ ms | $\tau_{fd} = 3.5$ ms | $\tau_{fd} = 4.0$ ms |
|---------------|----------|----------------------|----------------------|----------------------|
| 0             | 1.0000   | 1.0928               | 1.1090               | 1.1255               |
| 0.1           | 0.7292   | 0.7973               | 0.8093               | 0.8216               |

has divergent distortion. If the CoR error is negative, we say the HIL system has convergent distortion. The CoR in the HIL simulation system can be larger than 1 because there is energy input due to delay and dead zone, but the CoR in most real physical systems cannot be larger than 1 because there is no energy input during the contact.

### Force Delay Problem

Figs. 3(a and b) illustrate the distortion phenomena under two conditions, where the contact damping ratio is set to 0 and 0.1, respectively.  $V_{des}(t)$  denotes the desired relative velocity of the spacecraft computed by the spacecraft dynamic model. The force delay alone leads to divergent distortion in the HIL system, i.e., a larger CoR than that in space. As the force delay increases, the divergent distortion becomes more severe, resulting in larger errors. The CoR of these cases are summarized in Table 1.

### Dead Zone Problem under Force Delay

In the presence of a dead zone, two types of distortion behaviors can be observed. Figs. 4(a and b) illustrate the distortion when  $\xi_{con}$  is

**Table 2.** CoR under varying dead zone when the force delay is 3 ms

| Damping ratio | In space | $D = 0$ N | $D = 4$ N | $D = 8$ N | $D = 12$ N |
|---------------|----------|-----------|-----------|-----------|------------|
| 0             | 1.0000   | 1.0928    | 1.0938    | 1.0963    | 1.1001     |
| 0.1           | 0.7292   | 0.7973    | 0.7718    | 0.6771    | 0.4432     |

0 and 0.1, respectively, under the influence of a dead zone. The force delay is 3 ms. A peak is locally enlarged for clearer exhibition. When  $\xi_{con}$  is zero, a dead zone will make the simulator more divergent, i.e., a larger CoR over 1. For example, the CoR at a 3-ms delay is 1.0928, which will increase to 1.0963 by adding a dead zone of 8 N. A larger dead zone will result in a larger CoR, as indicated in Table 2.

In contrast, when  $\xi_{con}$  is 0.1, a dead zone will make the simulator more convergent, i.e., a smaller CoR below 1. For example, the CoR at 3-ms delay is 0.7973, which will decrease to 0.6771 by adding a dead zone of 8 N. A larger dead zone will result in a smaller CoR as indicated in Table 2. Moreover, in the damped case there are two types of CoR error between the CoR of the HIL system and the ideal CoR of the contact in space. In Table 2, when the dead zone is 0 or 4 N, the CoR error is positive, so the HIL system has divergent distortion. When the dead zone is 8 or 12 N, the CoR error is negative, so the HIL system has convergent distortion. We can observe that the dead zone may reduce the system energy.

It can be discovered that the distortion caused by the dead zone varies under different contact dynamics. In the case of undamped contact ( $\xi_{con} = 0$ ), the HIL system is divergent due to force delay,

![Figure 4: HIL simulation divergence due to force delay and dead zone. (a) Contact damping ratio = 0; (b) Contact damping ratio = 0.1. Both plots show desired relative velocity V_des (mm/s) vs Time (s) for dead zones of 0N, 4N, 8N, and 12N, and in-space contact. In (a), the 12N dead zone shows convergence. In (b), the 12N dead zone shows convergence due to damping.](10ac14a735447206df16a3124982177a_img.jpg)

Figure 4: HIL simulation divergence due to force delay and dead zone. (a) Contact damping ratio = 0; (b) Contact damping ratio = 0.1. Both plots show desired relative velocity V\_des (mm/s) vs Time (s) for dead zones of 0N, 4N, 8N, and 12N, and in-space contact. In (a), the 12N dead zone shows convergence. In (b), the 12N dead zone shows convergence due to damping.

**Fig. 4.** HIL simulation divergence due to force delay and dead zone: (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1.

![Figure 5: Single collision in HIL simulation at 3-ms force delay. (a) Contact damping ratio = 0. The plot shows Position (mm) on the left y-axis (0 to 0.4) and Force (N), Velocity (mm/s) on the right y-axis (-40 to 40) versus Time (s) on the x-axis (0 to 0.15). The curves include P_des (mm) (solid blue), P'_des (mm) (dotted green), F_con (N) (solid black), and V_des (mm/s) (dashed red). A vertical line marks the deepest point. The striking phase work W_in is negative and the rebounding phase work W_out is positive, with W_in > W_out. (b) Contact damping ratio = 0.1. The plot is similar to (a), but the contact force F_con (N) peaks before the relative velocity V_des (mm/s) reaches zero. The striking phase work W'_in is positive and the rebounding phase work W'_out is negative, with W'_in > W'_out.](e0d425c8e4eef259e4c52d81426d93fa_img.jpg)

Figure 5: Single collision in HIL simulation at 3-ms force delay. (a) Contact damping ratio = 0. The plot shows Position (mm) on the left y-axis (0 to 0.4) and Force (N), Velocity (mm/s) on the right y-axis (-40 to 40) versus Time (s) on the x-axis (0 to 0.15). The curves include P\_des (mm) (solid blue), P'\_des (mm) (dotted green), F\_con (N) (solid black), and V\_des (mm/s) (dashed red). A vertical line marks the deepest point. The striking phase work W\_in is negative and the rebounding phase work W\_out is positive, with W\_in > W\_out. (b) Contact damping ratio = 0.1. The plot is similar to (a), but the contact force F\_con (N) peaks before the relative velocity V\_des (mm/s) reaches zero. The striking phase work W'\_in is positive and the rebounding phase work W'\_out is negative, with W'\_in > W'\_out.

**Fig. 5.** Single collision in HIL simulation at 3-ms force delay: (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1.

and the system energy increases. Here, the dead zone leads to more divergence. This phenomenon reverses in the case of damped contact ( $\xi_{con} = 0.1$ ). The HIL system is convergent, and its energy decreases. Here, the dead zone leads to more convergence. These results indicate that the effect of the dead zone differs under these two types of system energy changes.

Overall, the simulation distortion caused by force delay and dead zone can be summarized as follows:

1. The force delay introduces divergent distortion into the space contact HIL simulator.
2. At the presence of the force delay, when the energy of the HIL simulator is generally divergent, the dead zone will make the simulator more divergent.
3. At the presence of the force delay, when the energy of the HIL simulator is generally convergent, the dead zone will make the simulator more convergent.

To explain why the dead zone can produce two different distortions, we analyze the underlying distortion mechanisms from an energy changes perspective.

## Space Contact HIL Simulator Distortion Mechanism

### Force Delay Distortion Mechanism

Figs. 5(a and b) show a single collision process in the space contact HIL simulator at 3-ms force delay. It will be used to analyze the system's energy changes.  $P_{des}(t)$  is the relative position of the spacecraft during the collision. In this case, it is the depth of the collision.  $V_{des}(t)$  is the relative velocity. A vertical vertical line marks the moment when the contact reaches the deepest point. At this moment  $P_{des}(t)$  reaches its peak and  $V_{des}(t)$  is zero. The contact force

$F_{con}(t)$  should have reached its peak at the deepest point simultaneously. But actually, it is delayed by the force sensor and reaches peak after the vertical line, as shown in Fig. 5(a).

$P'_{des}(t)$  is the delayed relative position generated from the delayed contact force. It indicates the delay by comparing with  $P_{des}(t)$ . In one collision, the spacecraft decelerates during the striking phase and accelerates during the rebounding phase. The two phases are separated by the vertical line and marked by the dotted line at the bottom. In the HIL simulation, the work done by the spacecraft is calculated as follows:

$$W = \int F_{con}(t)V_{des}(t)dt \quad (12)$$

The negative work during the striking phase and the positive work during the rebounding phase are denoted by  $W_{in}$  and  $W_{out}$ , respectively.

From Fig. 5(a), when  $\xi_{con}$  is zero, the contact force reaches peak after the relative velocity drops to zero. It indicates that the HIL simulator performs less negative work during striking phase than positive work during rebounding phase. It can be calculated as  $W_{in} = 3.75 \times 10^{-3} < W_{out} = 4.46 \times 10^{-3}$ . Therefore, the total energy of the system increases, leading to divergence. In contrast, Fig. 5(b) shows that due to the effect of contact damping, the contact force reaches peak before the relative velocity drops to zero. The system performs net negative work, i.e.,  $W_{in} = 3.75 \times 10^{-3} > W_{out} = 2.43 \times 10^{-3}$ . Therefore, the total energy of the system decreases, leading to convergence.

### Dead Zone Distortion Mechanism

Figs. 6(a and b) illustrate the distortion mechanism under the condition of 3-ms force delay and 12 N dead zone. In this case, the

![Figure 6: Single collision in HIL simulation at 3-ms force delay and 12-N dead zone. (a) Contact damping ratio = 0. The plot shows Position (mm) on the left y-axis (0 to 0.4) and Force (N), Velocity (mm/s) on the right y-axis (-40 to 40) versus Time (s) on the x-axis (0 to 0.15). The curves include P_des (mm) (solid blue), P'_des (mm) (dotted green), F_con (N) (solid black), and V_des (mm/s) (dashed red). A vertical line marks the deepest point. The striking phase work W'_in is positive and the rebounding phase work W'_out is negative, with W'_in > W'_out. (b) Contact damping ratio = 0.1. The plot is similar to (a), but the contact force F_con (N) peaks before the relative velocity V_des (mm/s) reaches zero. The striking phase work W'_in is positive and the rebounding phase work W'_out is negative, with W'_in > W'_out.](0f92e96694face0b13a687ec21fb9101_img.jpg)

Figure 6: Single collision in HIL simulation at 3-ms force delay and 12-N dead zone. (a) Contact damping ratio = 0. The plot shows Position (mm) on the left y-axis (0 to 0.4) and Force (N), Velocity (mm/s) on the right y-axis (-40 to 40) versus Time (s) on the x-axis (0 to 0.15). The curves include P\_des (mm) (solid blue), P'\_des (mm) (dotted green), F\_con (N) (solid black), and V\_des (mm/s) (dashed red). A vertical line marks the deepest point. The striking phase work W'\_in is positive and the rebounding phase work W'\_out is negative, with W'\_in > W'\_out. (b) Contact damping ratio = 0.1. The plot is similar to (a), but the contact force F\_con (N) peaks before the relative velocity V\_des (mm/s) reaches zero. The striking phase work W'\_in is positive and the rebounding phase work W'\_out is negative, with W'\_in > W'\_out.

**Fig. 6.** Single collision in HIL simulation at 3-ms force delay and 12-N dead zone: (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1.

work done during the collision process is denoted by  $W'_{in}$  and  $W'_{out}$ , corresponding to the striking phase and the rebounding phase, respectively. Firstly, because the force within the dead zone is filtered out to zero, the mechanical work done during both phases is reduced. Secondly, the duration of the dead zone differs between the two contact phases. Fig. 6(a) shows the case when  $\xi_{con}$  is zero.

The dead zone lasts longer when striking owing to the force delay. In consequence, compared with Fig. 5(a), more work is filtered out by the dead zone during the striking phase than during the rebounding phase. It can be expressed as  $W_{in} - W'_{in} = 4.71 \times 10^{-4} > W_{out} - W'_{out} = 4.07 \times 10^{-5}$ . Then we can derive the inequation  $W'_{out} - W'_{in} > W_{out} - W_{in}$ , which implies that the dead zone causes a greater amount of net positive work under the dead zone. Therefore, when the energy of the HIL simulator is generally divergent, the dead zone will make the simulator more divergent.

Fig. 6(b) shows the case when  $\xi_{con}$  is 0.1. Less work is filtered out during the striking phase, because the contact damping causes the contact force to shift before the deepest point. It can be calculated as  $W_{in} - W'_{in} = 8.90 \times 10^{-7} < W_{out} - W'_{out} = 2.32 \times 10^{-4}$ . We can derive  $W'_{in} - W'_{out} > W_{in} - W_{out}$ , which implies that the dead zone leads to a greater amount of net negative work. Therefore, when the energy of the HIL simulator is generally convergent, the dead zone will make the simulator more convergent.

## Space Contact HIL Simulator Compensation

The preceding analysis of the distortion mechanism aims to reveal the inherent reasons for the distortion phenomena caused by the force delay and the dead zone. We can see that the dead zone has a dual effect. In this section, an integrated compensation strategy is proposed as a practical solution, including a hybrid Smith predictor compensator and a dead zone disturbance observer compensator.

### Hybrid Smith Predictor Compensator for Force Delay

For force delay distortion, we have proposed a hybrid Smith predictor and phase-lead-based divergence compensation method (Qi et al. 2018). In our space contact HIL simulator, the force delay is known, which can be written as  $e^{-Tds}$  in the frequency domain. Its inverse model derived from the first-order Taylor expansion can be employed for compensation as follows:

$$F_{lead}(t) = (1 + T_{lead}s)F_{con}(t) \quad (13)$$

where  $T_{lead}$  = leading time, ideally matching the delay time. Using only this phase lead compensation is insufficient to fully eliminate the force delay distortion, and the system remains divergent. According to the first-order Padé approximation of the delay model, a serial Smith predictor can be designed as follows:

$$F_{smith}(t) = \left( 1 + \frac{T_{smith}s}{1 + T_{smith}s/2} (1 + T_{lead}s) \right) F_{con}(t) \quad (14)$$

where  $T_{smith}$  is also ideally equal to the system delay time. Nevertheless, this method may lead to overcompensation (Qi et al. 2018). Ultimately, we combine both compensation methods to achieve a balanced and effective compensation performance. The hybrid Smith predictor compensator can be expressed as follows:

$$F_{hybrid}(t) = (F_{lead}(t) + F_{smith}(t))/2 \quad (15)$$

### Disturbance Observer Compensator for Dead Zone

However, the hybrid Smith predictor compensation method is incapable of dealing with the distortion caused by the dead zone. First, the

![Figure 7: Equivalent external dead zone disturbance. The diagram shows two parallel paths. The left path represents the 'Striking' phase: 'Contact Dynamics' (F_act(t) = -K_con P_act(t) - B_con P_dot_act(t)) leads to 'Force Delay' (F_mea(t) = F_act(t - tau_d) + E(t)), which then enters the 'Dead Zone' (F_con(t) = DZ(F_mea(t), D)). The right path represents the 'Rebounding' phase: 'Contact Dynamics' (F_act(t) = -K_con P_act(t) - B_con P_dot_act(t)) leads to 'Force Delay' (F_mea(t) = F_act(t - tau_d) + E(t)), which then enters a summing junction. An external disturbance D_dz is added to the output of the summing junction to produce F_con(t).](cfbf0f2ddbc35370b0b8c6d043f25eb2_img.jpg)

Figure 7: Equivalent external dead zone disturbance. The diagram shows two parallel paths. The left path represents the 'Striking' phase: 'Contact Dynamics' (F\_act(t) = -K\_con P\_act(t) - B\_con P\_dot\_act(t)) leads to 'Force Delay' (F\_mea(t) = F\_act(t - tau\_d) + E(t)), which then enters the 'Dead Zone' (F\_con(t) = DZ(F\_mea(t), D)). The right path represents the 'Rebounding' phase: 'Contact Dynamics' (F\_act(t) = -K\_con P\_act(t) - B\_con P\_dot\_act(t)) leads to 'Force Delay' (F\_mea(t) = F\_act(t - tau\_d) + E(t)), which then enters a summing junction. An external disturbance D\_dz is added to the output of the summing junction to produce F\_con(t).

Fig. 7. Equivalent external dead zone disturbance.

force delay compensator essentially acts as a first-order differentiator. Applying it to the force signal that has already been cut by the dead zone can generate undesired impulses. These impulses exert unintended impact forces on the spacecraft dynamic model in the HIL system, resulting in emulation errors. Second, the dead zone eliminates the contact force within its duration, and the force delay compensation does not recover the missing force information. Moreover, although the dead zone is artificially applied, the measured signals within the dead zone consists mainly of noise, and the true contact force cannot be directly measured. Therefore, a dedicated compensator for dead zone distortion is necessary.

A compensation method based on disturbance observer for dead zone is proposed. As employing a dead zone inverse to cancel the dead zone is a commonly used method (Gang and Kokotovic 1994; Zhou et al. 2006), we first obtain the inverse signal after the dead zone

$$D_{dz}(t) = \begin{cases} -F_{mea}(t) & \text{if } |F_{mea}| \le D \\ 0 & \text{if } |F_{mea}| > D \end{cases} \quad (16)$$

This signal is unable to be measured directly.

Based on Eq. (16), in the space contact HIL simulator, the internal dead zone in the closed loop can be equivalently transformed into an external disturbance introduced by the inverse signal of the dead zone, as illustrated in Fig. 7. In this study, we refer to this disturbance  $D_{dz}(t)$  as a dead zone disturbance.

The dead zone disturbance can be observed using the following method. Assume that the actual motion of the lower motion mechanism is compensated. It is the same as the desired motion generated by the spacecraft dynamic model. According to the contact dynamic model, the actual contact force can be estimated as follows:

$$\hat{F}_{act}(t) = -\hat{K}_{con}P_{des}(t) - \hat{B}_{con}\dot{P}_{des}(t) \quad (17)$$

where  $\hat{K}_{con}$  and  $\hat{B}_{con}$  = identified values of the contact stiffness and the contact damping, respectively. By approximating the pure force delay using a first-order Taylor expansion, the dead zone disturbance observer can be designed as follows:

$$\hat{D}_{dz}(t) = F_{con}(t) - \frac{1}{1 + T_{lead}s} \hat{F}_{act}(t) \quad (18)$$

Before applying the hybrid Smith predictor compensation, the distortion caused by the dead zone is compensated using the dead zone disturbance observer. The force signal transferred to the hybrid Smith predictor is expressed as follows:

$$\hat{F}_{mea}(t) = F_{con}(t) - Q(s)\hat{D}_{dz}(t) \quad (19)$$

![Fig. 8. Schematic of the compensation method. The diagram shows a control loop. The 'Lower Motion Mechanism' provides 'Actual Motion' to the 'Space Contact Process'. The 'Space Contact Process' provides 'Actual Force' to the 'Force Measurement' block. The 'Force Measurement' block outputs 'Force With Distortion'. The 'Motion Transform' block takes 'Motion Command' and outputs 'Desired Motion' to the 'Spacecraft Dynamic model'. The 'Spacecraft Dynamic model' outputs 'Force Delay Compensated'. The 'Dead Zone Disturbance Observer' takes 'Actual Force' and 'Desired Motion' to estimate 'Dead Zone Disturbance'. The 'Hybrid Smith Predictor Compensator' takes 'Force With Distortion', 'Dead Zone Disturbance', and 'Force Delay Compensated' to produce 'Dead Zone Compensated'. The 'Integrated Compensator' (dashed red box) contains the 'Dead Zone Disturbance Observer' and the 'Hybrid Smith Predictor Compensator'. The 'Dead Zone Compensated' signal is fed back to the 'Force Measurement' block.](1956f44611abd5c3c41049836aa78ad8_img.jpg)

Fig. 8. Schematic of the compensation method. The diagram shows a control loop. The 'Lower Motion Mechanism' provides 'Actual Motion' to the 'Space Contact Process'. The 'Space Contact Process' provides 'Actual Force' to the 'Force Measurement' block. The 'Force Measurement' block outputs 'Force With Distortion'. The 'Motion Transform' block takes 'Motion Command' and outputs 'Desired Motion' to the 'Spacecraft Dynamic model'. The 'Spacecraft Dynamic model' outputs 'Force Delay Compensated'. The 'Dead Zone Disturbance Observer' takes 'Actual Force' and 'Desired Motion' to estimate 'Dead Zone Disturbance'. The 'Hybrid Smith Predictor Compensator' takes 'Force With Distortion', 'Dead Zone Disturbance', and 'Force Delay Compensated' to produce 'Dead Zone Compensated'. The 'Integrated Compensator' (dashed red box) contains the 'Dead Zone Disturbance Observer' and the 'Hybrid Smith Predictor Compensator'. The 'Dead Zone Compensated' signal is fed back to the 'Force Measurement' block.

Fig. 8. Schematic of the compensation method.

where  $Q(s)$  = low-pass filter applied to suppress the identification noise. To ensure the compensator performance within the typical frequency range of space contact simulations,  $Q(s)$  is designed to be approximately equal to one below 15 Hz in this study.

The contact stiffness and the damping are identified in real time. Neglecting the effect of friction, the stiffness and the damping parameters can be estimated using the recursive least-squares (RLS) method (Qi et al. 2017b). Here, it is assumed that the physical characteristics of the contact model remain constant over a very short time interval. A one-step RLS estimation is formulated through the following set of difference equations at the  $i$ th step:

$$L_i = \frac{R_{i-1}\varphi_i}{\lambda + \varphi_i^T R_{i-1} \varphi_i} \quad (20)$$

$$R_i = \frac{1}{\lambda} (R_{i-1} - L_i \varphi_i^T R_{i-1}) \quad (21)$$

$$\theta_i = \theta_{i-1} + L_i (\Delta F_i - \varphi_i^T \theta_{i-1}) \quad (22)$$

This method has two inputs. The first one is  $\varphi_i = [\Delta P_i, \Delta V_i]^T$ , a vector representing the first-order backward differences of the desired position  $P_{des}(t)$  and velocity of the spacecraft  $V_{des}(t)$ . The second one is  $\Delta F_i$ , the first-order backward difference of the measured force  $F_{mea}(t)$  before the dead zone. The output of this method is  $\theta_i = [\hat{K}_i, \hat{B}_i]^T$ , a vector containing the estimated contact stiffness and damping.  $L_i$  is the updating factor,  $\lambda$  is the forgetting factor, and  $R_i$  is the second-order inverse covariance matrix.

Each of the relevant position, velocity, and contact force data will be acquired at a sampling frequency higher than that of the HIL simulation cycle. In a single HIL simulation cycle at moment  $t$ , a set of data will be available. The contact stiffness and damping at

moment  $t$  can be accurately identified by applying the RLS algorithm for two or three steps on the sampled data set.

### Control Block Diagram for Distortion Compensation

To clarify the logic, a concise schematic of the compensation method is given in Fig. 8. The output of the force measurement system has distortions caused by dead zone and force delay. To compensate the dead zone distortion, the first step of the integrated compensation method is to estimate the dead zone disturbance using the proposed dead zone disturbance observer. In the dead zone disturbance observer, the contact stiffness and damping are identified by the measured force and the desired motion of the spacecraft. Then, the contact force can be estimated by the estimated contact stiffness and damping.

By comparing the estimated contact force with the output force with distortion, the dead zone disturbance can be obtained. It is used for compensation subsequently. To compensate the force delay distortion, the second step is to compensate the force delay using the hybrid Smith predictor. After the distortions caused by dead zone and force delay have been compensated, the force is fed into the spacecraft dynamic model. The proposed method is applicable to different force delay lengths and dead zone widths.

## Verification

### MATLAB Verification

To validate the proposed compensation method for the space contact HIL simulator, a series of emulations are conducted using MATLAB version 2024. The test conditions as a verification example are the same as that in the section “Force Delay and Dead Zone Problem.” The force delay is 3 ms, and the dead zone is 8 N. In the compensator module, the hybrid Smith predictor employs parameters  $T_{lead}$  and  $T_{smith}$ , both of which are 3 ms. The gain of  $Q(s)$  is set to one.

The performance of the proposed compensator is verified on MATLAB. Figs. 9(a and b) present the desired velocity of the spacecraft under force delay. For the undamped contact, the CoR of the case in space is 1.0000. The system without compensation exhibits divergent distortion when the force delay is 3 ms, and the dead zone is 0 N (CoR = 1.0895). Applying the hybrid Smith predictor compensator can compensate this distortion effectively (CoR = 0.9841). However, when an 8 N dead zone exists, the hybrid Smith predictor compensator cannot work well. The divergent distortion still exists (CoR = 1.0148). For the damped contact, the CoR of the case in space is 0.7293. The system without compensation exhibits divergent

![Fig. 9. Performance of the hybrid Smith predictor compensator. (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1. Both plots show desired velocity V_des (mm/s) vs Time (s) from 0 to 2 seconds. The legend indicates: without compensation (red solid line), hybrid Smith, D:8N (blue solid line), hybrid Smith, D:0N (green solid line), and in space (dashed line). Plot (a) shows the undamped case where the 'without compensation' curve diverges significantly, while the compensated curves remain stable. Plot (b) shows the damped case where the 'without compensation' curve also diverges, but the compensated curves are much closer to the 'in space' reference line.](8841664c26347b9ad66df5ee1b120eb1_img.jpg)

Fig. 9. Performance of the hybrid Smith predictor compensator. (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1. Both plots show desired velocity V\_des (mm/s) vs Time (s) from 0 to 2 seconds. The legend indicates: without compensation (red solid line), hybrid Smith, D:8N (blue solid line), hybrid Smith, D:0N (green solid line), and in space (dashed line). Plot (a) shows the undamped case where the 'without compensation' curve diverges significantly, while the compensated curves remain stable. Plot (b) shows the damped case where the 'without compensation' curve also diverges, but the compensated curves are much closer to the 'in space' reference line.

Fig. 9. Performance of the hybrid Smith predictor compensator: (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1.

![Figure 10: Performance of the integrated compensator. (a) Contact damping ratio = 0; (b) Contact damping ratio = 0.1. Both plots show desired velocity V_des (mm/s) vs Time (s). The legend indicates: without compensation (red solid line), integrated, D:8N (green solid line), hybrid Smith, D:8N (blue solid line), and in space (dashed line).](3121afa7ca030b22ee0345864ca6f38b_img.jpg)

Figure 10 consists of two line graphs, (a) and (b), plotting the desired velocity  $V_{\text{des}}$  (mm/s) against time (s). Both graphs show four data series: 'without compensation' (red solid line), 'integrated, D:8N' (green solid line), 'hybrid Smith, D:8N' (blue solid line), and 'in space' (dashed line). In graph (a), where the contact damping ratio is 0, the 'without compensation' series shows significant high-frequency oscillations, while the 'integrated' and 'hybrid Smith' series track the 'in space' dashed line closely. In graph (b), where the damping ratio is 0.1, the oscillations are reduced, and the integrated compensator continues to perform well. An inset in graph (a) shows a zoomed-in view of the initial 0.5 seconds.

Figure 10: Performance of the integrated compensator. (a) Contact damping ratio = 0; (b) Contact damping ratio = 0.1. Both plots show desired velocity V\_des (mm/s) vs Time (s). The legend indicates: without compensation (red solid line), integrated, D:8N (green solid line), hybrid Smith, D:8N (blue solid line), and in space (dashed line).

Fig. 10. Performance of the integrated compensator: (a) contact damping ratio = 0; and (b) contact damping ratio = 0.1.

![Figure 11: Verification experiment on the rod-frame contact device. The image shows a mechanical setup with labels: Upper Motion Mechanism, Undamped Elastic Rod, Lower Motion Mechanism, and High-stiffness Frame.](efca2dce0095c9dc2a68e9af6b2bfd40_img.jpg)

Figure 11 is a photograph of a mechanical test rig. It features a vertical 'Undamped Elastic Rod' connected to an 'Upper Motion Mechanism' at the top and a 'Lower Motion Mechanism' at the bottom. The rod is mounted on a 'High-stiffness Frame'. Yellow arrows point to these components, which are labeled with text boxes.

Figure 11: Verification experiment on the rod-frame contact device. The image shows a mechanical setup with labels: Upper Motion Mechanism, Undamped Elastic Rod, Lower Motion Mechanism, and High-stiffness Frame.

Fig. 11. Verification experiment on the rod-frame contact device.

![Figure 12: Verification experiment results on the rod-frame contact device. The plot shows desired velocity V_des (mm/s) vs Time (s). The legend indicates: without compensation (red solid line), integrated method (green solid line), and hybrid Smith (blue solid line).](7ff005f9556dc6518981bb92091d36ab_img.jpg)

Figure 12 is a line graph showing the desired velocity  $V_{\text{des}}$  (mm/s) over time (s). The graph displays three step functions: 'without compensation' (red solid line), 'integrated method' (green solid line), and 'hybrid Smith' (blue solid line). The 'integrated method' and 'hybrid Smith' lines closely follow the 'without compensation' line, which has a step change from 0 to 10 mm/s at 5s and back to 0 at 15s.

Figure 12: Verification experiment results on the rod-frame contact device. The plot shows desired velocity V\_des (mm/s) vs Time (s). The legend indicates: without compensation (red solid line), integrated method (green solid line), and hybrid Smith (blue solid line).

Fig. 12. Verification experiment results on the rod-frame contact device.

distortion when the force delay is 3 ms, and the dead zone is 0 N ( $\text{CoR} = 0.9380$ ). The hybrid Smith predictor compensator can compensate this distortion well ( $\text{CoR} = 0.7292$ ). However, it cannot compensate the convergent distortion caused by an 8 N dead zone ( $\text{CoR} = 0.6527$ ).

Figs. 10(a and b) present the desired velocity of the spacecraft in the presence of the force delay and the dead zone. Four cases are

![Figure 13: Application experiment on the claw-type capture mechanism. The image shows a complex mechanical setup with labels: Upper Motion Mechanism, Capture Mechanisms, Passive Target, Mechanical Claw, Lower Motion Mechanism, and Capture Mechanism.](89986656b45c3b6896256f1a22f7c186_img.jpg)

Figure 13 is a photograph of a claw-type capture mechanism. It includes an 'Upper Motion Mechanism' and a 'Lower Motion Mechanism' connected by a 'Mechanical Claw'. A 'Passive Target' is positioned to the right. Yellow arrows point to these components, which are labeled with text boxes.

Figure 13: Application experiment on the claw-type capture mechanism. The image shows a complex mechanical setup with labels: Upper Motion Mechanism, Capture Mechanisms, Passive Target, Mechanical Claw, Lower Motion Mechanism, and Capture Mechanism.

Fig. 13. Application experiment on the claw-type capture mechanism.

given, including the case without compensation, with only the hybrid Smith predictor compensator, with the integrated compensator, and the ideal case in space. For the undamped contact, the  $\text{CoR}$  of the case in space is 1.0000. The system without compensation exhibits severe divergent distortion ( $\text{CoR} = 1.1625$ ). Applying only the hybrid Smith predictor compensator is insufficient to compensate for this divergent distortion ( $\text{CoR} = 1.0148$ ). By using the integrated compensator, the divergent distortion is well compensated ( $\text{CoR} = 0.9989$ ).

For the damped contact, the  $\text{CoR}$  of the case in space is 0.7293. The system without compensation exhibits divergent distortion ( $\text{CoR} = 0.8005$ ). The hybrid Smith predictor compensator is insufficient ( $\text{CoR} = 0.6527$ ). By using the integrated compensator, the divergent distortion is well compensated ( $\text{CoR} = 0.7294$ ). It can be concluded that the hybrid-Smith-predictor-based compensation method does not compensate well for force delay and dead zone. However, the proposed method works well.

### Experiment Verification

A rod-frame verification experiment was performed on the space contact HIL simulator to assess the proposed compensation method. As shown in Fig. 11, the simulator employed an undamped elastic contact device. It consists of an undamped elastic rod fixed to the lower motion mechanism and a high-stiffness rectangular frame fixed to the upper motion mechanism. The bending stiffness of the elastic rod can be calculated accurately because the rod is precisely manufactured. The stiffness of the frame far exceeds that of the rod. By performing contact process at different lengths of the rod, different contact stiffnesses can be achieved. Experiments on this contact prototype can evaluate the performance of the HIL simulator.

![Figure 14: Space contact simulation on the claw-type capture mechanism. (a) Linear velocities Vx, Vy, Vz (mm/s) vs Time (s). (b) Angular velocities wx, wy, wz (rad/s) vs Time (s).](b93cbfb52e37619e688175a6aad9edd9_img.jpg)

Figure 14 consists of two subplots, (a) and (b), showing the time history of velocities during a 2-second contact process. Subplot (a) displays linear velocities  $V_x$  (blue solid line),  $V_y$  (green dotted line), and  $V_z$  (red dashed line) in mm/s. The  $V_x$  and  $V_y$  velocities show high-frequency oscillations between approximately -2 and 4 mm/s, while  $V_z$  remains near zero. Subplot (b) displays angular velocities  $\omega_x$  (blue solid line),  $\omega_y$  (green dotted line), and  $\omega_z$  (red dashed line) in rad/s, scaled by  $10^{-3}$ . The  $\omega_x$  and  $\omega_y$  velocities show oscillations between approximately -4 and 6  $\times 10^{-3}$  rad/s, while  $\omega_z$  remains near zero. Both plots show a series of contact events occurring at approximately 0.25 s, 0.75 s, 1.25 s, and 1.75 s.

Figure 14: Space contact simulation on the claw-type capture mechanism. (a) Linear velocities Vx, Vy, Vz (mm/s) vs Time (s). (b) Angular velocities wx, wy, wz (rad/s) vs Time (s).

**Fig. 14.** Space contact simulation on the claw-type capture mechanism: (a) linear velocities; and (b) angular velocities.

If the simulator is properly compensated to reproduce the dynamics in space, the single-axis contact on this undamped elastic device should yield a constant-amplitude oscillation ( $\text{CoR} = 1$ ). In our experiment, the initial relative velocity was 10 mm/s, the equivalent mass was 300 kg, and the contact stiffness was 100 N/mm. The corresponding natural frequency of contact was about 3 Hz. In our HIL system, a JR3 force sensor (Woodland, California) force sensor (JR3) and AD card and computer (National Instruments, Austin, Texas) are used. The noise can be described by Gaussian distribution, and the  $3\sigma$  value is about 8 N. In our experiment setup, the force delay is about 3 ms, and the dead zone is about 8 N.

Fig. 12 reports the results on the vertical axis for three cases, without compensation, with only hybrid Smith predictor compensator, and with integrated compensator. Without compensation, the system was divergent ( $\text{CoR} = 1.0892$ ). Using the hybrid Smith predictor compensator only, the divergence still exists ( $\text{CoR} = 1.0218$ ). With the proposed integrated compensator, the system is compensated effectively ( $\text{CoR} = 0.9987$ ). Results on the other two axes were consistent with these findings and are omitted for brevity.

### Experimental Application

An application experiment was conducted on the developed space contact HIL simulator, as shown in Fig. 13. It used the active claw-type capture mechanism and belong to the case of weak collision of space contact. For the claw-type capture mechanism, the stiffness is about several hundreds of Newtons per millimeter. The damping ratio is about 0.1. It is not equipped with dampers or springs. The active capture mechanism was fixed on the lower motion mechanism, and the passive target was fixed on the upper motion mechanism. During the experiment, the mechanical claw actively moved and captured the passive target. Then, the target was grasped by the claw and mechanically fixed, thus completing the contact process. The objective of this experiment was to validate the capability of the claw-type capture mechanism to perform space contact operations under specific conditions. A 6-DOF control system was designed and employed into this experimental setup.

Figs. 14(a and b) illustrate a representative 2-s contact process observed during the experiment. The initial relative conditions are an equivalent mass of 350 kg, a position of  $(-40, 0, 53)$  mm, a relative orientation of zero, and both the relative linear velocity and angular velocity equal to zero. The reference frame of the relative motion is illustrated in Fig. 13. The three-dimensional relative linear and angular velocities between the active and passive contact interfaces are plotted. At this stage, the active capture mechanism has already approached and constrained the passive target, and repeated collisions occur within a confined spatial region. It can be observed

![Figure 15: Kinetic energy variation of the simulated spacecraft. Kinetic energy Ek (J) vs Time (s).](0d5fdb87a392819c7d2e3b6230912a0b_img.jpg)

Figure 15 is a plot of the kinetic energy  $E_k$  in Joules versus time in seconds. The kinetic energy fluctuates between approximately 0.02 J and 0.04 J throughout the 2-second period. The fluctuations correspond to the contact events seen in Fig. 14, with peaks occurring at approximately 0.25 s, 0.75 s, 1.25 s, and 1.75 s.

Figure 15: Kinetic energy variation of the simulated spacecraft. Kinetic energy Ek (J) vs Time (s).

**Fig. 15.** Kinetic energy variation of the simulated spacecraft.

that the relative motion decelerates during striking, accelerates during rebounding, and remains approximately constant when passing through the clearance. Each contact lasts approximately 0.1 to 0.2 s, corresponding to a contact frequency of about 3 Hz over the 2-s period. These results show that the contact collision dynamics remain convergent.

Fig. 15 depicts the kinetic energy variation during the same contact process. It can be observed that under the proposed compensation method, the total kinetic energy exhibits a decreasing trend throughout the simulation. This indicates that, despite variations in local contact conditions, the space contact HIL simulator maintains an overall convergent behavior.

## Conclusion

An integrated compensator combining a hybrid Smith predictor and a dead zone disturbance observer has been proposed to compensate for the simulation distortion in the developed space contact HIL simulator. Two primary sources of the simulation distortion in force measurement system including the force delay and the dead zone are analyzed. The associated distortion phenomena and distortion mechanism are investigated. The force delay is compensated by the hybrid Smith predictor, but the dead zone is addressed using the dead zone disturbance observer. Verifications and application demonstrated that the proposed distortion compensation approach can effectively compensate the simulation distortion and improve the fidelity of the HIL simulation.

## Data Availability Statement

Some or all data, models, or code that support the findings of this study are available from the corresponding author upon reasonable request.

## Acknowledgments

The work is partially supported by grants from the National Natural Science Foundation of China (Grant Nos. 51975351 and 51927809).

## Author Contributions

Dongjin Li: Conceptualization; Formal analysis; Investigation; Methodology; Software; Validation; Visualization; Writing – original draft. Huayang Li: Investigation; Methodology; Software. Chenkun Qi: Conceptualization; Funding acquisition; Investigation; Methodology; Supervision; Writing – review and editing. Yan Hu: Methodology; Software; Validation. Feng Gao: Conceptualization; Funding acquisition; Project administration; Supervision. Xianchao Zhao: Conceptualization; Data curation; Investigation; Software; Supervision.

## References

- Abiko, S., Y. Satake, X. Jiang, T. Tsujita, and M. Uchiyama. 2014. "Delay time compensation based on coefficient of restitution for collision hybrid motion simulator." *Adv. Rob.* 28 (17): 1177–1188. <https://doi.org/10.1080/01691864.2014.913501>.
- Boge, T., and O. Ma. 2011. "Using advanced industrial robotics for spacecraft rendezvous and docking simulation." In *Proc., 2011 IEEE Int. Conf. on Robotics and Automation*, 1–4. New York: IEEE.
- Cao, R., F. Gao, Y. Zhang, D. Pan, and W. Chen. 2015. "A new parameter design method of a 6-DOF parallel motion simulator for a given workspace." *Mech. Based Des. Struct. Mach.* 43 (1): 1–18. <https://doi.org/10.1080/15397734.2014.904234>.
- Chang, T., D. Cong, Z. Ye, and J. Han. 2007. "Time problems in HIL simulation for on-orbit docking and compensation." In *Proc., 2nd IEEE Conf. on Industrial Electronics and Applications*. New York: IEEE.
- De Stefano, M., H. Mishra, A. M. Giordano, R. Lampariello, and C. Ott. 2021. "A relative dynamics formulation for hardware-in-the-loop simulation of on-orbit robotic missions." *IEEE Rob. Autom. Lett.* 6 (2): 3569–3576. <https://doi.org/10.1109/LRA.2021.3064510>.
- Ding, X., Y. Wang, Y. Wang, and K. Xu. 2020. "A review of structures, verification, and calibration technologies of space robotic systems for on-orbit servicing." *Sci. China Technol. Sci.* 64 (3): 462–480. <https://doi.org/10.1007/s11431-020-1737-4>.
- Fallahiazad, N., and Z. H. Zhu. 2025. "Review of autonomous space robotic manipulators for on-orbit servicing and active debris removal." *Space Sci. Technol.* 5 (Jul): 0291. <https://doi.org/10.34133/space.0291>.
- Gang, T., and P. V. Kokotovic. 1994. "Adaptive control of plants with unknown dead-zones." *IEEE Trans. Autom. Control* 39 (1): 59–68. <https://doi.org/10.1109/9.273339>.
- Hu, Y., F. Gao, C. Qi, X. Zhao, and Q. Wang. 2021. "A force and moment compensation method for a hardware-in-the-loop docking simulator based on the stiffness identification of the docking mechanism." *Mechatronics* 76 (Jun): 102513. <https://doi.org/10.1016/j.mechatronics.2021.102513>.
- Li, G., Z. Yang, Y. Fu, Z. O'Neill, L. Ren, O. Pradhan, and J. Wen. 2024. "A hardware-in-the-loop (HIL) testbed for cyber-physical energy systems in smart commercial buildings." *Sci. Technol. Built Environ.* 30 (5): 415–432. <https://doi.org/10.1080/23744731.2024.2336839>.
- Li, W. J., et al. 2019. "On-orbit service (OOS) of spacecraft: A review of engineering developments." *Prog. Aerosp. Sci.* 108 (Jul): 32–120. <https://doi.org/10.1016/j.paerosci.2019.01.004>.
- Ma, O., J. Wang, S. Misra, and M. Liu. 2004. "On the validation of SPDM task verification facility." *J. Robot. Syst.* 21 (5): 219–235. <https://doi.org/10.1002/rob.20011>.
- Martin, É., M. Doyon, Y. Gonthier, and C. Lange. 2005. "Validation process of the STVF hardware-in-the-loop simulation facility." In *Proc., 8th Int. Symp. on Artificial Intelligence, Robotics and Automation in Space*. Noordwijk, Netherlands: ESA Publication Division.
- Mitchell, J. D., S. P. Cryan, K. Baker, T. Martin, R. Goode, K. W. Key, T. Manning, and C. H. Chien. 2008. "Integrated docking simulation and testing with the Johnson space center six-degree-of-freedom dynamic test system." *AIP Conf. Proc.* 969 (1): 709–716. <https://doi.org/10.1063/1.2845035>.
- Mou, F., X. Xiao, T. Zhang, Q. Liu, D. Li, C. Hu, and W. Ma. 2018. "A HIL simulation facility for task verification of the Chinese space station manipulator." In *Proc., 2018 IEEE Int. Conf. on Mechatronics and Automation*, 2138–2144. New York: IEEE.
- Opromolla, R., et al. 2024. "Future in-orbit servicing operations in the space traffic management context." *Acta Astronaut.* 220 (Jul): 469–477. <https://doi.org/10.1016/j.actaastro.2024.05.007>.
- Osaki, K., A. Konno, and M. Uchiyama. 2010. "Delay time compensation for a hybrid simulator." *Adv. Rob.* 24 (8–9): 1081–1098. <https://doi.org/10.1163/016918610X501246>.
- Qi, C., F. Gao, X. Zhao, Q. Wang, and A. Ren. 2018. "Hybrid Smith predictor and phase lead based divergence compensation for hardware-in-the-loop contact simulation with measurement delay." *Acta Astronaut.* 147 (Jun): 175–182. <https://doi.org/10.1016/j.actaastro.2018.04.010>.
- Qi, C., F. Gao, X. C. Zhao, A. Ren, and Q. Wang. 2017a. "A force compensation approach towards divergence of hardware-in-the-loop contact simulation system for damped elastic contact." *IEEE Trans. Ind. Electron.* 64 (4): 2933–2943. <https://doi.org/10.1109/TIE.2016.2643625>.
- Qi, C., D. Li, Y. Hu, F. Gao, W. Wang, and W. Ma. 2023. "Stability analysis and distortion compensation of robot structure dynamics for a hybrid simulator." *J. Mech. Des.* 145 (7): 073302. <https://doi.org/10.1111/1.4062148>.
- Qi, C., A. Ren, F. Gao, X. Zhao, Q. Wang, and Q. Sun. 2017b. "Compensation of velocity divergence caused by dynamic response for hardware-in-the-loop docking simulator." *IEEE Trans. Mechatron.* 22 (1): 422–432. <https://doi.org/10.1109/TMECH.2016.2601219>.
- Reims, F., H. Frei, E.-A. Risse, and M. Burri. 2021. "10-year anniversary of the European proximity operations simulator 2.0—Looking back at test campaigns, rendezvous research and facility improvements." *Aerospace* 8 (9): 235. <https://doi.org/10.3390/aerospace8090235>.
- Renaut, L., K. Klonovska, M. Albracht, and H. Frei. 2025. "EPoS-Lid: Lidar benchmark dataset for pose estimation during non-cooperative rendezvous." *Acta Astronaut.* 238 (Part A): 414–423. <https://doi.org/10.1016/j.actaastro.2025.09.030>.
- Rybus, T., et al. 2019. "Application of a planar air-bearing microgravity simulator for demonstration of operations required for an orbital capture with a manipulator." *Acta Astronaut.* 155 (Feb): 211–229. <https://doi.org/10.1016/j.actaastro.2018.12.004>.
- Sazawal, P., D. Choukroun, H. Benninghoff, and E. Gill. 2019. "Three-dimensional modeling and time-delay stability analysis for robotics docking simulation." *Proc. Inst. Mech. Eng., Part G: J. Aerosol. Eng.* 233 (14): 5438–5455. <https://doi.org/10.1177/0954410019846049>.
- Somers, R. J., J. A. Douthwaite, D. J. Wagg, N. Walkinshaw, and R. M. Hierons. 2023. "Digital-twin-based testing for cyber-physical systems: A systematic literature review." *Inf. Softw. Technol.* 156 (Apr): 107145. <https://doi.org/10.1016/j.infsof.2022.107145>.
- Sugai, F., S. Abiko, X. Jiang, A. Konno, and M. Uchiyama. 2013. "Compensation for dead band of force measurement based on the coefficient of restitution in a hybrid simulator." *Adv. Rob.* 27 (12): 907–917. <https://doi.org/10.1080/01691864.2013.797134>.
- Svotina, V. V. 2024. "Space debris removal—Review of technologies and techniques. Rigid coupling between space debris and service spacecraft." *J. Space Saf. Eng.* 11 (2): 252–267. <https://doi.org/10.1016/j.jsse.2024.04.002>.
- Takahashi, R., H. Ise, A. Konno, M. Uchiyama, and D. Sato. 2008. "Hybrid simulation of a dual-arm space robot colliding with a floating object." In *Proc., 2008 IEEE Int. Conf. on Robotics and Automation*. New York: IEEE.

Wang, W., C. Zhang, C. Qi, L. Fu, and S. Wang. 2023. "Stiffness design of active capture claw-type docking mechanism for lunar sample return." *Aerospace* 10 (9): 794. <https://doi.org/10.3390/aerospace10090794>.
Yu, S., J. Han, W. Zhang, and D. Xu. 2022. "Smith predictor compensation and fuzzy incremental control for delay of space docking hardware-in-the-loop simulation system." *Proc. Inst. Mech. Eng., Part G: J. Aerosp. Eng.* 236 (11): 2179–2193. <https://doi.org/10.1177/09544100211053305>.
Zhou, J., C. Wen, and Y. Zhang. 2006. "Adaptive output control of nonlinear systems with uncertain dead-zone nonlinearity." *IEEE Trans. Autom. Control* 51 (3): 504–511. <https://doi.org/10.1109/TAC.2005.864200>.