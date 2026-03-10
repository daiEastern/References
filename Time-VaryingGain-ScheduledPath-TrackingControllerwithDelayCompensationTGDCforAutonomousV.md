

# Time-Varying Gain-Scheduled Path-Tracking Controller with Delay Compensation (TGDC) for Autonomous Vehicles

XuePeng Hu,<sup>1</sup> Yu Zhang,<sup>1</sup> Yuxuan Hu,<sup>1</sup> Zhenfeng Wang,<sup>2</sup> and Yechen Qin<sup>1</sup>

<sup>1</sup>Beijing Institute of Technology, School of Mechanical Engineering, China

<sup>2</sup>BYD Automotive Industry Co., Ltd., China

## Abstract

Path-tracking control occupies a critical role within autonomous driving systems, directly reflecting vehicle motion and impacting both safety and user experience. However, the ever-changing vehicle states, road conditions, and delay characteristics of control systems present new challenges to the path tracking of autonomous vehicles, thereby limiting further enhancements in performance. This article introduces a path-tracking controller, time-varying gain-scheduled path-tracking controller with delay compensation (TGDC), which utilizes a linear parameter-varying system and optimal control theory to account for time-varying vehicle states, road conditions, and steering control system delays. Subsequently, a polytopic-based path-tracking model is applied to design the control law, reducing the computational complexity of TGDC. To evaluate the effectiveness and real-time capability of TGDC, it was tested under a series of complex conditions using a hardware-in-the-loop platform. The results demonstrate that through the polytopic-based path-tracking model and delay compensation strategy in TGDC, it can effectively enhance path-tracking performance with minimal computational load, even under conditions of parameter variability and control delays.

## History

Received: 26 Aug 2024  
 Revised: 19 Dec 2024  
 Accepted: 24 Jan 2025  
 e-Available: 19 Feb 2025

## Keywords

Path tracking control, Time-varying parameters, Control delay, Vehicle dynamics control, Hardware-in-the-loop platform

## Citation

Hu, X., Zhang, Y., Hu, Y., Wang, Z. et al., "Time-Varying Gain-Scheduled Path-Tracking Controller with Delay Compensation (TGDC) for Autonomous Vehicles," SAE Int. J. Veh. Dyn., Stab., and NVH 9(2):2025, doi:10.4271/10-09-02-0012.

ISSN: 2380-2162

e-ISSN: 2380-2170

This article is part of a focus issue on Recent Advances in Dynamics and Control of Automotive Chassis-by-Wire.

![A collage of four images related to automotive technology: a close-up of a car's interior button, a car driving on a road, a car wheel, and a tire being tested on a machine.](31cdb383e9cc2643a547f2500ed3cd08_img.jpg)

A collage of four images related to automotive technology: a close-up of a car's interior button, a car driving on a road, a car wheel, and a tire being tested on a machine.

## 1. Introduction

Autonomous vehicles (AVs) have garnered significant attention due to their immense potential in enhancing traffic safety, improving traffic efficiency, and reducing energy consumption. Perception, decision-making, and path planning technologies are essential in enhancing the intelligence level of AVs [1, 2]. Moreover, accurate and smooth path-tracking control is crucial, as it directly impacts both safety and user experience [3–5]. Numerous methods have been proposed, continuously improving the performance of path-tracking controllers. However, the time-varying vehicle states, road conditions, and chassis control delay characteristics continue to pose notable challenges to the path-tracking performance of current AVs [6, 7].

The primary task of path tracking is to control AVs and track the desired path outputted by the planning layer accurately and smoothly [8]. To achieve this, the path-tracking methods used can be categorized into model-free methods, kinematics model-based methods, and dynamics model-based methods. Among the model-free methods, proportion–integration–differentiation (PID) control is widely utilized in the industrial sector. Nonetheless, fine-tuning PID controller parameters becomes increasingly difficult when dealing with complex and varying path-tracking issues. Kinematics model-based methods are favored for their effective control and low computational load at low speeds. However, their performance deteriorates under large curvature and high-speed conditions due to a lack of consideration for vehicle dynamics [9]. Dynamics model-based methods achieve superior control outcomes and represent the primary approach currently in use. These methods require integration with vehicle dynamics to model the path-tracking problem, making the control law dependent on the model. Consequently, when model parameters are uncertain, the performance of the path-tracking controller declines. Robust control strategies effectively address parameter perturbation issues; however, sliding mode control necessitates a balance between reducing the controller order and system chattering to ensure stability and real-time capability; robust model predictive control (RMPC) [10] faces limitations due to its low computational efficiency and conservative nature. An alternative effective method involves modeling using linear parameter-varying (LPV) approaches [11] to mitigate the effects of time-varying parameters in the model, as demonstrated in [12], which is based on  $H_\infty$  and LPV system theory, where controllers utilizing four-wheel steering and direct yaw moment control have been designed to enhance path-tracking performance and maneuver stability under varying road adhesion conditions. However, the high order of the designed controllers presents challenges for implementation in vehicle electronic control units (ECUs). In contrast, Liang et al. [13] employed RMPC to ensure path-tracking precision and enhance the system's disturbance rejection

capabilities. However, in the LPV modeling, only the impact of time-varying vehicle velocity is considered, neglecting changes in road conditions. To facilitate real-time control, reference [14] combines LPV model with optimal controllers to design a gain-scheduled path-tracking controller. However, the establishment of the LPV model did not account for issues such as high conservativeness. Therefore, in the path-tracking process, where vehicle states and road conditions continually change, considering the impact of time-varying parameters on the model and ensuring the real-time performance of the control algorithm are crucial for enhancing path-tracking performance.

The implementation of path tracking relies on chassis actuators to execute control commands. Currently, intelligent chassis systems are increasingly utilized as platforms for AVs, providing autonomous driving systems with greater degrees of freedom [15, 16]. Existing path-tracking control methods fully utilize the actuation capabilities of various intelligent chassis components [17–20]. However, a frequently overlooked aspect is the control delay characteristic of the chassis, which refers to the latency between issuing a control signal and the completion of actuation. This study focuses on the path-tracking issue, particularly on the steer-by-wire system, and the delays are mainly composed of two parts: the signal transmission delay in the control system [21] and the mechanical delay in the steering mechanism [22]. Significant delays can lead to steering hysteresis or even instability, thereby degrading the vehicle's path-tracking performance [23]. Xu et al. [24, 25] designed a preview path-tracking controller that incorporates delay compensation, capable of achieving accurate and smooth tracking under conditions of delay with a relatively low online computational cost. However, higher levels of delay increase the system's dimensionality, posing challenges to online computation. Furthermore, Shi et al. [26] treated delay as a stochastic disturbance and uses a LPV system to design a PID-based path-tracking controller, demonstrating high robustness against varying signal transmission delays, but it does not account for mechanical delays. In summary, it is essential to consider chassis control delay characteristics and implement delay compensation in path-tracking algorithms, which is also a focus of this study.

To tackle the aforementioned challenges, this article presents a time-varying gain-scheduled path-tracking control with delay compensation (TGDC). A novel polytopic-based path-tracking model is introduced to mitigate the impact of time-varying model parameters caused by vehicle states and road conditions. This model enhances robustness to time-varying parameters by comprehensively considering the range of variations in vehicle velocity and road adhesion coefficients, and it reduces the conservativeness of the polytopic by utilizing the relationships between different time-varying parameters. Based on the established model, the control system's delay characteristics are integrated into the model, and time-delay

control theory is employed to transform the delayed system into a delay-free system, thereby compensating for the delays. Furthermore, TGDC combines optimal control with polytopic characteristics to formulate controller design strategies. By computing control gains for different combinations of polytopic vertices and delay levels offline, and calculating the weights of different polytopic vertices online, relying on gain scheduling to obtain the current optimal control input. This method has demonstrated to enhance path-tracking performance under varying vehicle states, road conditions, and the presence of delays. The main contributions of this article are summarized below:

1. A gain-scheduled path-tracking controller has been developed, which simultaneously accounts for time-varying vehicle state, road condition, and chassis control delay characteristics, improving the path-tracking performance of AVs under complex conditions.
2. A novel polytopic-based path-tracking model is employed in TGDC design. This model integrates time-varying parameters to reduce their impact on the model and diminish the conservatism associated with LPV modeling.
3. The hardware-in-the-loop (HiL) platform utilizing a real-time target machine has been developed to evaluate the algorithm under multiple operational conditions, validating TGDC's effectiveness and real-time capabilities.

The rest of this article is organized as follows. The system models are introduced in [Section 2](#). The delay compensation strategy and the TGDC design are illustrated in [Section 3](#). [Section 4](#) introduces the verification results of the TGDC based on HiL platform, involving effectiveness and real-time performance. Finally, the article is summarized, and conclusions are drawn in [Section 5](#).

## 2. System Modeling

This section introduces the vehicle lateral dynamic model, path-tracking model, and polytopic-based path-tracking model for TGDC design. [Figure 1](#) illustrates the schematic of the single-track dynamics model with a desired path, with definitions provided in [Table 1](#).

### A. Vehicle Lateral Dynamic Model

Vehicle model needs to strike a balance between model accuracy and computational efficiency. The single-track dynamics model is employed to reflect the basic characteristics of the vehicle lateral and yaw motion. The lateral vehicle dynamic is formulated as

$$m(\dot{v}_y + v_x \dot{\phi}) = F_{yf} \cos \delta_f + F_{yr} \quad (1)$$

**FIGURE 1** Single-track dynamics model with a desire path.

![Figure 1: Single-track dynamics model with a desire path. The diagram shows a vehicle's lateral dynamics in a coordinate system (x, y). A 'Desire path' is shown as a curved line. The vehicle's center of gravity (C.G.) is at (Xcg, Ycg). The vehicle's orientation is defined by yaw angle phi and yaw rate phi-dot. The front wheel steering angle is delta_f. The lateral velocity is v_y and longitudinal velocity is v_x. The lateral tire forces are F_yf and F_yr. The distance from the front/rear axle to the C.G. is l_f/l_r. The lateral error is e_y and the longitudinal error is e_x. The desired path coordinates are (X_des, Y_des) and the desired yaw angle is phi_des.](50dae0dfbde108cee0040a29f2a42e88_img.jpg)

Figure 1: Single-track dynamics model with a desire path. The diagram shows a vehicle's lateral dynamics in a coordinate system (x, y). A 'Desire path' is shown as a curved line. The vehicle's center of gravity (C.G.) is at (Xcg, Ycg). The vehicle's orientation is defined by yaw angle phi and yaw rate phi-dot. The front wheel steering angle is delta\_f. The lateral velocity is v\_y and longitudinal velocity is v\_x. The lateral tire forces are F\_yf and F\_yr. The distance from the front/rear axle to the C.G. is l\_f/l\_r. The lateral error is e\_y and the longitudinal error is e\_x. The desired path coordinates are (X\_des, Y\_des) and the desired yaw angle is phi\_des.

$$l_z \dot{\phi} = l_f F_{yf} \cos \delta_f - l_r F_{yr} \quad (2)$$

where  $m$  and  $l_z$  are the mass and yaw inertia of the vehicle, respectively;  $v_x/v_y$  is vehicle longitudinal/lateral velocity;  $\phi$  and  $\dot{\phi}$  are vehicle yaw angle and yaw rate. While  $l_f/l_r$  denotes the distance from front/rear axle to C.G.,  $\delta_f$  is the front wheel steering angle.  $F_{yf}/F_{yr}$  is the lateral tire force of the front/rear axles. Under the small slip-angle assumption, they are functions of tire slip angles and can be expressed as

$$F_{yf} = 2C_{af} \alpha_f \quad (3)$$

$$F_{yr} = 2C_{ar} \alpha_r \quad (4)$$

where  $C_{af}$  and  $C_{ar}$  are the cornering stiffness of front and rear tires, and  $\alpha_f$  and  $\alpha_r$  denote the front and rear tire slip angles, given by:

$$\alpha_f = \delta_f - \theta_f \approx \delta_f - \frac{v_y + l_f \dot{\phi}}{v_x} \quad (5)$$

$$\alpha_r = -\theta_r \approx -\frac{v_y - l_r \dot{\phi}}{v_x} \quad (6)$$

**TABLE 1** The benchmarks of verification.

| -          | Controller name | Consider time-varying parameters | Consider delay compensation |
|------------|-----------------|----------------------------------|-----------------------------|
| Main       | TGDC            | Yes (with Novel Polytopic)       | Yes                         |
| Benchmarks | LQR             | No                               | No                          |
|            | LQR-T           | Yes (with Normal Polytopic)      | No                          |
|            | LQR-D           | No                               | Yes                         |
|            | LQR-TD          | Yes (with Normal Polytopic)      | Yes                         |

Substituting (3)–(6) into (1)–(2) yields:

$$\dot{v}_y = -\frac{2\dot{\varphi}(C_{arf} - C_{arl})}{mv_x} + \frac{2v_y(C_{af} + C_{ar})}{m} + \frac{2C_{arf}\delta_r}{m} - v_x\dot{\varphi} \quad (7)$$

$$\dot{\varphi} = -\frac{2\dot{\varphi}(C_{arf}^2 + C_{arl}^2)}{l_z v_x} + \frac{2v_y(C_{arf} - C_{arl})}{l_z} + \frac{2C_{arf}\delta_r}{l_z} \quad (8)$$

### B. Path-Tracking Model

As shown in Figure 1, the desired vehicle direction is the tangential direction of the desired path. Defining counterclockwise as the positive direction for angular terms, the lateral error and the yaw angle error are defined as follows

$$e_y = (Y_{cg} - Y_{des})\cos\varphi - (X_{cg} - X_{des})\sin\varphi \quad (9)$$

$$\epsilon_\varphi = \varphi - \varphi_{des} \quad (10)$$

Given road curvature  $C_{des}$ , the desired yaw rate is

$$\dot{\varphi}_{des} = C_{des}v_x \quad (11)$$

And the derivatives of  $e_y$  and  $\epsilon_\varphi$  can be expressed as

$$\dot{e}_y = v_y + v_x\epsilon_\varphi \quad (12)$$

$$\dot{\epsilon}_\varphi = \dot{\varphi} - \dot{\varphi}_{des} = \dot{\varphi} - C_{des}v_x \quad (13)$$

$$\ddot{e}_y = (\dot{v}_y + v_x\dot{\varphi}) - v_x\dot{\varphi}_{des} = \dot{v}_y + v_x\dot{\epsilon}_\varphi \quad (14)$$

$$\ddot{\epsilon}_\varphi = \dot{\varphi} - \dot{\varphi}_{des} \quad (15)$$

By combining (7)–(8) and (12)–(15), the path-tracking model can be rewritten in the state space form:

$$\dot{x}_0 = A_0x_0 + B_0\delta_r + C_0C_{des} \quad (16)$$

where the state variables  $x_0 = [e_y, \dot{e}_y, \epsilon_\varphi, \dot{\epsilon}_\varphi]^T$ , the front wheel steering angle  $\delta_r$  is the control input, and the desired path curvature  $C_{des}$  is an external time-varying disturbance. The coefficient matrices  $A_0$ ,  $B_0$ , and  $C_0$  are given by:

$$A_0 = \begin{bmatrix} 0 & 1 & 0 & 0 \\ 0 & -\frac{2(C_{af} + C_{ar})}{mv_x} & \frac{2(C_{af} + C_{ar})}{m} & -\frac{2(C_{arf}^2 - C_{arl}^2)}{mv_x} \\ 0 & 0 & 0 & 1 \\ 0 & -\frac{2(C_{arf} - C_{arl})}{l_z v_x} & \frac{2(C_{arf} - C_{arl})}{l_z} & -\frac{2(C_{arf}^2 + C_{arl}^2)}{l_z v_x} \end{bmatrix}$$

$$B_0 = \left[ 0, \frac{2C_{af}}{m}, 0, \frac{2C_{arf}}{l_z} \right]^T$$

$$C_0 = \left[ 0, -\frac{2(C_{arf} - C_{arl})}{m} - v_x^2, 0, -\frac{2(C_{arf}^2 + C_{arl}^2)}{l_z} \right]^T$$

### C. Polytopic-Based Path-Tracking Model

To reduce the impact of the time-varying parameters, the LPV system is employed to establish a polytopic-based path-tracking model for TGDC design. From the coefficient matrix in (16), it is observed that the time-varying parameters in path-tracking model include vehicle longitudinal velocity and tire cornering stiffness. Moreover, tire cornering stiffness is primarily influenced by the road adhesion coefficient, allowing the uncertainty of tire cornering stiffness can be translated into that of the road adhesion coefficient. Therefore, the cornering stiffness of the front and rear tires can be expressed as follows:

$$C_{af} = \mu C_{af0}, \quad C_{ar} = \mu C_{ar0} \quad (17)$$

where  $\mu$  represents the road adhesion coefficient, and  $C_{af0}$  and  $C_{ar0}$  denote the nominal cornering stiffness of the front and rear tires, respectively.

According to the structure of Equation 16, the auxiliary time-varying parameters are chosen as  $\lambda_1 = \mu$ ,  $\lambda_2 = v_x^2$ ,  $\lambda_3 = \frac{\mu}{v_x}$ , bounded with:

$$\begin{cases} \mu_{\min} \le \lambda_1 \le \mu_{\max} \\ v_{x\min}^2 \le \lambda_2 \le v_{x\max}^2 \\ \frac{\mu_{\min}}{v_{x\max}} \le \lambda_3 \le \frac{\mu_{\max}}{v_{x\min}} \end{cases} \quad (18)$$

where  $\mu_{\min}$  and  $\mu_{\max}$  represent the minimum and maximum road adhesion coefficients in the whole path-tracking process, respectively, and  $v_{x\min}$  and  $v_{x\max}$  denote the minimum and maximum vehicle longitudinal velocity in the whole path-tracking process, respectively. These values are parameters that the autonomous driving system can access during perception and planning [27].

Construct parameter-varying vector  $\Delta = [\lambda_1, \lambda_2, \lambda_3]$  as the polytopic working point, and all the possible values can be represented through a linear combination of the coordinates from the eight vertices of polytopic  $a_0b_0c_0d_0 - e_0f_0g_0h_0$  [12], as Figure 2(a) shows, with each vertex coordinate being:  $a_0 = \left( \mu_{\max}, v_{x\max}^2, \frac{\mu_{\max}}{v_{x\min}} \right)$ ,

**FIGURE 2** Different polytopic.![Figure 2 shows two 3D plots of polytopes in a parameter space defined by axes λ1, λ2, and λ3. Plot (a) shows a polytope defined by vertices a0, b0, c0, d0, e0, f0, g0, h0, which is a large, conservative volume. Plot (b) shows a polytope defined by vertices a, b, c, d, e, f, g, h, which is a smaller, more accurate volume that better fits the teal surface representing the actual working point surface. The teal surface is a curved, elongated shape along the λ1 axis.](b15e3860e0c96ed16ce77f032da6f107_img.jpg)

(a) Polytopic  $a_0b_0c_0d_0 - e_0f_0g_0h_0$ 
(b) Polytopic  $abcd - efgh$

Figure 2 shows two 3D plots of polytopes in a parameter space defined by axes λ1, λ2, and λ3. Plot (a) shows a polytope defined by vertices a0, b0, c0, d0, e0, f0, g0, h0, which is a large, conservative volume. Plot (b) shows a polytope defined by vertices a, b, c, d, e, f, g, h, which is a smaller, more accurate volume that better fits the teal surface representing the actual working point surface. The teal surface is a curved, elongated shape along the λ1 axis.

$$\begin{aligned}
 b_0 &= \left( \mu_{\max}, V_{x \min}^2, \frac{\mu_{\max}}{V_{x \min}} \right), \quad c_0 = \left( \mu_{\min}, V_{x \min}^2, \frac{\mu_{\max}}{V_{x \min}} \right), \\
 d_0 &= \left( \mu_{\min}, V_{x \max}^2, \frac{\mu_{\max}}{V_{x \min}} \right), \quad e_0 = \left( \mu_{\max}, V_{x \max}^2, \frac{\mu_{\min}}{V_{x \max}} \right), \\
 f_0 &= \left( \mu_{\max}, V_{x \min}^2, \frac{\mu_{\min}}{V_{x \max}} \right), \quad g_0 = \left( \mu_{\min}, V_{x \min}^2, \frac{\mu_{\min}}{V_{x \max}} \right), \\
 h_0 &= \left( \mu_{\min}, V_{x \max}^2, \frac{\mu_{\min}}{V_{x \max}} \right).
 \end{aligned}$$

Although this approach is straightforward and effective, the parameters  $\lambda_1, \lambda_2, \lambda_3$  remain isolated. By considering the relationships among these time-varying parameters, the parameter-varying vector's working point can be constrained to the teal surface shown in Figure 2(a) [identical to the teal surface in Figure 2(b)], meaning that most of the volume within polytope  $a_0b_0c_0d_0 - e_0f_0g_0h_0$  is unrealizable. Consequently, describing the parameter-varying vector's working point using polytope  $a_0b_0c_0d_0 - e_0f_0g_0h_0$  is conservative. On the other hand, increasing the number of vertices to reduce the conservativeness of the polytope significantly raises the computational complexity [28]. To address this issue without adding more vertices, this article proposes a novel polytope, as shown in Figure 2(b) (polytope  $abcd - efgh$ ). Compared to the normal polytope  $a_0b_0c_0d_0 - e_0f_0g_0h_0$ , the novel polytope  $abcd - efgh$  reduces the description space of the parameter-varying vector to more closely approximate the actual working point surface. When representing actual parameters through combinations of multiple vertices, the novel polytope  $abcd - efgh$  confines the working point within a smaller, more accurate range, thus reducing the conservativeness of the established polytope model. The vertex coordinates of the novel polytope are:

$$a = \left( \mu_{\max}, V_{x \max}^2, \frac{\mu_{\max}}{V_{x \min}} \right), \quad b = \left( \mu_{\max}, V_{x \min}^2, \frac{\mu_{\max}}{V_{x \min}} \right),$$

$$\begin{aligned}
 c &= \left( \mu_{\min}, V_{x \min}^2, \frac{\mu_{\min}}{V_{x \min}} \right), \quad d = \left( \mu_{\min}, V_{x \max}^2, \frac{\mu_{\min}}{V_{x \min}} \right), \\
 e &= \left( \mu_{\max}, V_{x \max}^2, \frac{\mu_{\min}}{V_{x \max}} \right), \quad f = \left( \mu_{\max}, V_{x \max}^2, \frac{\mu_{\max}}{V_{x \max}} \right), \\
 g &= \left( \mu_{\min}, V_{x \min}^2, \frac{\mu_{\min}}{V_{x \max}} \right), \quad h = \left( \mu_{\min}, V_{x \max}^2, \frac{\mu_{\min}}{V_{x \max}} \right).
 \end{aligned}$$

Let  $\Lambda_1, \Lambda_2, \dots, \Lambda_8$  represent the auxiliary time-varying parameter vectors established based on vertices  $a, b, \dots, h$ , respectively, and  $\rho_j$  denotes the weights of  $\Lambda_j$ , then the polytopic working point can be expressed as

$$\Lambda = \sum_{j=1}^{8} \rho_j \Lambda_j \quad (19)$$

which satisfies:  $\sum_{j=1}^{8} \rho_j = 1$  and  $\rho_j \ge 0$ . For simplification, the weights for eight vertexes are given as

$$\rho_1 = \rho_\mu \rho_{v_x^2} \rho_{\frac{\mu}{v_x}}, \quad \rho_2 = \rho_\mu \left( 1 - \rho_{v_x^2} \right) \rho_{\frac{\mu}{v_x}}$$

$$\rho_3 = \left( 1 - \rho_\mu \right) \left( 1 - \rho_{v_x^2} \right) \rho_{\frac{\mu}{v_x}}, \quad \rho_4 = \left( 1 - \rho_\mu \right) \rho_{v_x^2} \rho_{\frac{\mu}{v_x}}$$

$$\rho_5 = \rho_\mu \rho_{v_x^2} \left( 1 - \rho_{\frac{\mu}{v_x}} \right), \quad \rho_6 = \rho_\mu \left( 1 - \rho_{v_x^2} \right) \left( 1 - \rho_{\frac{\mu}{v_x}} \right)$$

$$\rho_7 = \left( 1 - \rho_\mu \right) \left( 1 - \rho_{v_x^2} \right) \left( 1 - \rho_{\frac{\mu}{v_x}} \right), \quad \rho_8 = \left( 1 - \rho_\mu \right) \rho_{v_x^2} \left( 1 - \rho_{\frac{\mu}{v_x}} \right)$$

where the weighting factors are  $\rho_u = \frac{\mu - \mu_{\min}}{\mu_{\max} - \mu_{\min}}$ ,  $\rho_{v_x^2} = \frac{v_x^2 - v_{x\min}^2}{v_{x\max}^2 - v_{x\min}^2}$ ,  $\rho_{\frac{u}{v_x}} = \frac{\frac{\mu}{v_x} - \frac{\mu_{\min}}{v_{x\max}}}{\frac{\mu_{\max}}{v_{x\min}} - \frac{\mu_{\min}}{v_{x\max}}}$ .

In calculating weights, given that the precise acquisition of road adhesion coefficients and vehicle longitudinal velocity was not the primary focus of this study, this article approximated the adhesion coefficients based on general road types (e.g., dry, wet, icy surfaces), and vehicle longitudinal velocity was assumed to be approximately measurable [29].

Based on the path-tracking model and eight auxiliary time-varying parameter vectors  $\Lambda_j$ , the system (16) can be formulated with an affine relationship to the time-varying parameter vector  $\Lambda$ . Thus, the polytopic-based path-tracking model for TGDC design can be described as

$$\dot{x}_1 = A_1 x_1 + B_1 \delta_r + C_1 C_{\text{des}} \quad (20)$$

where state variables  $x_1 = x_0$  and the coefficient matrices  $A_1$ ,  $B_1$ , and  $C_1$  are given by

$$A_1 = \sum_{j=1}^{8} \rho_j \left( A_{\lambda 0} + \sum_{i=1}^{3} \lambda_{ij} A_{\lambda i} \right)$$

$$B_1 = \sum_{j=1}^{8} \rho_j \left( B_{\lambda 0} + \sum_{i=1}^{3} \lambda_{ij} B_{\lambda i} \right)$$

$$C_1 = \sum_{j=1}^{8} \rho_j \left( C_{\lambda 0} + \sum_{i=1}^{3} \lambda_{ij} C_{\lambda i} \right)$$

where  $\lambda_{ij}$  represents the  $i$ th element of  $\Lambda_j$ , with coefficient matrices  $A_{\lambda i}$ ,  $B_{\lambda i}$ , and  $C_{\lambda i}$  as follows:

$$A_{\lambda 0} = \begin{bmatrix} 0 & 1 & 0 & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 0 \end{bmatrix}, \quad A_{\lambda 2} = O_{4 \times 4}$$

$$A_{\lambda 1} = \begin{bmatrix} 0 & 0 & 0 & 0 \\ 0 & 0 & \frac{2(C_{\alpha f 0} + C_{\alpha r 0})}{m} & 0 \\ 0 & 0 & 0 & 0 \\ 0 & 0 & \frac{2(C_{\alpha f 0} l_f - C_{\alpha r 0} l_r)}{l_z} & 0 \end{bmatrix}$$

$$A_{\lambda 3} = \begin{bmatrix} 0 & 0 & 0 & 0 \\ 0 & -\frac{2(C_{\alpha f 0} + C_{\alpha r 0})}{m} & 0 & -\frac{2(C_{\alpha f 0} l_f - C_{\alpha r 0} l_r)}{l_z} \\ 0 & 0 & 0 & 0 \\ 0 & -\frac{2(C_{\alpha f 0} l_f - C_{\alpha r 0} l_r)}{l_z} & 0 & -\frac{2(C_{\alpha f 0} l_f^2 + C_{\alpha r 0} l_r^2)}{l_z} \end{bmatrix}$$

$$B_{\lambda 0} = O_{4 \times 1}, \quad B_{\lambda 1} = \left[ 0, \frac{2C_{\alpha f 0}}{m}, 0, \frac{2C_{\alpha f 0} l_f}{l_z} \right]^T, \quad B_{\lambda 2} = O_{4 \times 1}$$

$$B_{\lambda 3} = O_{4 \times 1}, \quad C_{\lambda 0} = O_{4 \times 1}, \quad C_{\lambda 2} = [0, -1, 0, 0]^T, \quad C_{\lambda 3} = O_{4 \times 1}$$

$$C_{\lambda 1} = \left[ 0, -\frac{2(C_{\alpha f 0} l_f - C_{\alpha r 0} l_r)}{m}, 0, -\frac{2(C_{\alpha f 0} l_f^2 + C_{\alpha r 0} l_r^2)}{l_z} \right]^T$$

where  $O/E$  stands for the zero/identity matrix. Consequently, the development of the polytopic-based path-tracking model, meticulously considering the temporal variations in vehicle states and road conditions, and will be employed as the underlying system model for the forthcoming design of the TGDC.

## 3. TGDC Design with Delay Compensation

The depiction of TGDC is illustrated in Figure 3. Building on the established polytopic-based path-tracking model, delay characteristics are integrated into the model, and through delay compensation strategies, the system is transformed into a delay-free system. Subsequently, the path-tracking optimization problem is formulated and solved offline to determine gains, and the optimal control input is generated through online computation of state variables and weights.

### A. Delay Characteristics Analysis

As described in the introduction, steering control delay characteristics include both signal transmission delay and mechanical delay. As shown in Figure 3, the steering command  $\delta$ , after a signal transmission delay of  $t_d$  seconds to the steering actuator, the corresponding steering actuator command is denoted as  $\delta_d$ . Subsequently, after a mechanical delay of  $t_l$  seconds, the steering wheel

**FIGURE 3** Flowchart of TGDC.![Flowchart of TGDC (Time-Varying Polytopic-based Delay Compensation) showing the integration of vehicle dynamics, path-tracking, polytopic optimization, and delay compensation for autonomous vehicle control.](49ee89a1d5852ab005dbbab6de09a8a6_img.jpg)

The flowchart illustrates the TGDC framework, which integrates vehicle dynamics, path-tracking, and delay compensation for autonomous vehicle control. The process is divided into several main components:

- Polytypic-based path-tracking model:** This section includes the vehicle lateral dynamics model and the path-tracking model. It calculates the time-varying parameters vector  $\lambda = [\mu, v_x^2, \frac{\mu}{v_x}]^T$  and uses polytopic optimization to find 8 vertices of a polytope. The state vector  $x_1$  is then calculated as  $x_1 = A_1 x_1 + B_1 \delta_r + C_1 C_{des}$ .
- State and weights calculate:** This block calculates the state vector  $x$  and model weights  $\rho_j$ .
- Control command calculate:** This block calculates the control command  $\delta$  using the formula  $K = \sum_{j=1}^{8} \rho_j K_j$ , where  $\delta = -Kx$ .
- Offline gain calculate:** This block formulates an optimal control problem to solve the Riccati equation  $K_j = \text{dlqr}(A, B, Q, R)$  to find the gain matrix  $K_j$ .
- Steer control delay characteristics:** This section models the delay in the steering system, including signal transmission delay and mechanical delay, to determine the delay characteristics  $\delta_r(t) = -\frac{1}{t_l} \delta_r(t) + \frac{1}{t_l} \delta(t - t_d)$ .
- Desire path:** Shows the desired path and yaw angle over Global X [m].
- Autonomous vehicle:** Represents the vehicle states and the steering actuator command  $\delta_d$  and steering wheel angle  $\delta_r$ .

The flowchart shows the iterative process of calculating the control command  $\delta$  based on the current state  $x$  and weights  $\rho_j$ , which is then used to calculate the steering actuator command  $\delta_d$  and the steering wheel angle  $\delta_r$ , taking into account the delay characteristics.

Flowchart of TGDC (Time-Varying Polytopic-based Delay Compensation) showing the integration of vehicle dynamics, path-tracking, polytopic optimization, and delay compensation for autonomous vehicle control.

completes the steering command, with the corresponding steering wheel angle denoted as  $\delta_r$ .

The relationship among the steering command  $\delta$  and steering actuator command  $\delta_d$  can be represented as follows

$$\delta_d(t) = \delta(t - t_d) \quad (21)$$

The relationship between the steering actuator command  $\delta_d$  and the steering wheel angle  $\delta_r$  is commonly approximated by a first-order linear system [22]:

$$\delta_r = \frac{1}{t_l s + 1} \delta_d \quad (22)$$

where  $s$  represents the Laplace operator. Combining (21) and (22), delay characteristics can be summarized as

$$\dot{\delta}_r(t) = -\frac{1}{t_l} \delta_r(t) + \frac{1}{t_l} \delta(t - t_d) \quad (23)$$

### B. Delay Compensation Strategy

To compensate for the delay, it is necessary to incorporate the delay characteristics into the model. By integrating with (23), the polytypic-based path-tracking model with delay characteristics can be formulated as

$$\dot{x}_2 = A_2 x_2 + B_2 \delta(t - t_d) + C_2 C_{des} \quad (24)$$

where state variables  $x_2 = [x_1, \delta_d]^T$  and the coefficient matrices  $A_2$ ,  $B_2$ , and  $C_2$  are given by

$$A_2 = \begin{bmatrix} A_1 & B_1 \\ 0_{4 \times 4} & -\frac{1}{t_l} \end{bmatrix}, \quad B_2 = \begin{bmatrix} 0_{4 \times 1} & \frac{1}{t_l} \end{bmatrix}^T, \quad C_2 = [C_1, 0]^T$$

To facilitate the design and implementation of TGDC, it is necessary to convert the continuous-time system into a discrete-time system. We discrete (24) using the forward Euler method with a fixed sampling period  $T$ , specifically:

$$x_3(k+1) = A_3 x_3(k) + B_3 \delta(k - N) + C_3 C_{des}(k) \quad (25)$$

where  $x_3(k) = [x_1(k), \delta_r(k)]^T$  represents the current system state variables,  $\delta(k - N)$  denotes the delayed steering command control input,  $k$  is the step sequence,  $N = t_d/T$  is the number of delay steps, and  $C_{des}(k)$  is the desired path curvature. The coefficient matrices  $A_3$ ,  $B_3$ , and  $C_3$  are as follows

$$A_3 = \left( E + \frac{TA_2}{2} \right), \quad B_3 = TB_2, \quad C_3 = TC_2$$

Equation 25 represents a typical delayed system. The core of the delay compensation strategy is to convert the delayed system into a delay-free system before the controller design. The two main strategies for converting

a delayed system to a delay-free system are the delay augmentation strategy [30] and state predictor [31]. The delay augmentation strategy leverages optimal control theory of discrete time–delay system by augmenting the delayed control input into the system state vector, converting the delayed system into a delay-free one. The state predictor, on the other hand, uses predicted control inputs (usually fixed) to forecast future system states, thus converting the delayed system into a delay-free system. The delay augmentation strategy accounts for the system's state and corresponding control inputs at each step, resulting in a system that theoretically reflects the real system without prediction errors. In contrast, the state predictor assumes preset system states as the future real system state, which may hinder the guarantee of global optimality in controllers based on this strategy [25].

The delay augmentation strategy can result in a sharp increase in system dimensions when the system delay time is large, which presents significant challenges for controller design and implementation. However, as shown in Figure 3, this article combined the delay augmentation strategy with LPV system theory. By predefining the polytopic vertices and incorporating different delay combinations, then solve the gain matrix of the control input offline. Through gain scheduling, this work can implement real-time optimal control. Therefore, this article successfully leverages the theoretical optimality of the delay augmentation strategy while avoiding the issue of “dimension explosion”.

Based on the delay augmentation strategy, let  $x_4(k) = [x_3(k), \delta(k - N), \delta(k - N + 1), \dots, \delta(k - 2), \delta(k - 1)]^T \in \mathbb{R}^{(5+N) \times 1}$ , then the delayed system (25) can be rewritten as a delay-free system

$$x_4(k+1) = A_4 x_4(k) + B_4 \delta(k) + C_4 C_{\text{des}}(k) \quad (26)$$

with coefficient matrices  $A_4$ ,  $B_4$ , and  $C_4$  as follows

$$A_4 = \begin{bmatrix} A_3 & B_3 & O_{5 \times (N-1)} \\ O_{(N-1) \times 5} & O_{(N-1) \times 1} & E_{(N-1) \times (N-1)} \\ O_{1 \times 5} & 0 & O_{1 \times (N-1)} \end{bmatrix} \in \mathbb{R}^{(5+N) \times (5+N)}$$

$$B_4 = \begin{bmatrix} O_{(4+N) \times 1} \\ 1 \end{bmatrix} \in \mathbb{R}^{(5+N) \times 1}, C_4 = \begin{bmatrix} C_3 \\ O_{N \times 1} \end{bmatrix} \in \mathbb{R}^{(5+N) \times 1}$$

### C. Formulation of the Path-Tracking Optimal Control Problem

Describing the path-tracking problem using optimal control theory offers distinct advantages such as precision, directness, and completeness. However, after

incorporating polytopic and considering delay compensation, the constructed system state space equation (26) becomes a high-dimensional nonlinear equation, posing challenges to the application of optimal control algorithms. Drawing on the concept of state augmentation, this study incorporates the disturbance terms into the system state variables, which can be rewritten as

$$x(k+1) = Ax(k) + B\delta(k) \quad (27)$$

where state variables  $x(k) = [x_4(k), C_{\text{des}}(k)]^T \in \mathbb{R}^{(6+N) \times 1}$  and the coefficient matrices  $A$  and  $B$  are given by

$$A = \begin{bmatrix} A_4 & C_4 \\ O_{1 \times (5+N)} & 0 \end{bmatrix} \in \mathbb{R}^{(6+N) \times (6+N)}$$

$$B = \begin{bmatrix} B_4 \\ 0 \end{bmatrix} \in \mathbb{R}^{(6+N) \times 1}$$

The path-tracking problem is modeled as an optimal control problem (OCP). A cost function oriented toward accuracy and smoothness over the infinite time horizon is designed as

$$J(x, \delta) = \frac{1}{2} \sum_{k=0}^{k_N} \left[ x(k)^T Q x(k) + \delta(k)^T R \delta(k) \right] \quad (28)$$

where  $Q$  denotes positive semi-definite state weighting matrix, and  $R$  represents positive definite control weighting matrix,  $Q$  and  $R$  should be tuned to compromise between accuracy and smoothness. The term  $k_N$  refers to the number of control sequences required to reach the final state. The saturation of control input  $\delta$  and  $\Delta\delta$  is formulated as a hard constraint:

$$\delta_{\min} \le \delta \le \delta_{\max} \quad (29)$$

$$\Delta\delta_{\min} \le \Delta\delta \le \Delta\delta_{\max} \quad (30)$$

Combining Equations 27, 28, 29, and 30, the construction of the path-tracking OCP, taking into account variations in velocity and road adhesion coefficients with delay compensation, is formulated as follows

$$\left\{ \begin{array}{l} \min J(x, \delta) = \frac{1}{2} \sum_{k=0}^{k_N} \left[ x(k)^T Q x(k) + \delta(k)^T R \delta(k) \right] \\ \text{s.t.:} \\ x(k+1) = Ax(k) + B\delta(k) \\ \delta_{\min} \le \delta \le \delta_{\max} \\ \Delta\delta_{\min} \le \Delta\delta \le \Delta\delta_{\max} \end{array} \right. \quad (31)$$

### D. TGDC Design with Closed-Loop System Stability Analysis

In the TGDC control law design process, control constraints (29) and (30) are initially disregarded and will be considered at the end of this section. And OCP (31) essentially represents a linearly constrained LQR problem.

First, the Hamiltonian function is constructed as follows

$$H = \frac{1}{2} (x^T Q x + \delta^T R \delta) + \lambda^T (A x + B \delta) \quad (32)$$

where  $\lambda$  is a Lagrange multiplier vector. According to the optimal control conditions, the control equations and the Euler equations are defined as follows

$$\frac{\partial H}{\partial \delta} = R \delta + B^T \lambda = 0 \quad (33)$$

$$\frac{\partial H}{\partial x} = -\dot{\lambda} = A^T \lambda + Q x \quad (34)$$

The optimal control law is obtained as

$$\delta^* = -R^{-1} B^T \lambda = -R^{-1} B^T P x = -K x \quad (35)$$

where  $P$  is the solution to the following Riccati equation

$$P = -A^T P B (R + B^T P B)^{-1} B P A + A^T P A + Q \quad (36)$$

Substitution Equation 35 into Equation 27 yields the closed-loop system:

$$x(k+1) = (A - B R^{-1} B^T P) x(k) \quad (37)$$

To analyze the stability of the closed-loop system equation (37), define Lyapunov function  $V$ :

$$V[x(k)] = x(k)^T P x(k) \quad (38)$$

With  $V[0] = 0$ ;  $\forall x(k) \neq 0$ ,  $V[x(k)] > 0$ . Combining (37) and (38), the increment of  $V[x(k)]$  between two adjacent steps can be obtained

$$\Delta V = -x(k)^T (Q + P B R^{-1} B^T P) x(k) \quad (39)$$

Since  $Q$  is positive semi-definite and  $R$  is positive definite, thus  $\Delta V < 0$ . Therefore, the closed-loop system is asymptotic and stable globally.

From (35) and (36), it can be observed that when the matrices  $A$ ,  $B$ ,  $Q$ ,  $R$  are fixed, the gain matrix  $K$  of the optimal control law is also determined. Given that this study also incorporates delay compensation, the system inevitably possesses a higher dimensionality, which makes online solutions prone to issues of dimensional explosion, thus compromising the real-time feasibility of the control algorithm. The TGDC ingeniously utilizes the characteristic of the polytopic-based path-tracking model being a weighted sum of the eight vertexes model, solving for the gain matrices based on these eight vertices offline. Subsequent online calculation of vertex weights yields the final optimal control law. By considering changes in vehicle states, road conditions, and implementing delay compensation, this approach achieves optimal control with a significantly reduced computational cost. In handling constraints, the optimal control inputs are validated post-solution. If these exceed the constraints, the corresponding boundary values are adopted. It is important to note that, except in very low-speed scenarios, control saturation does not occur [24].

## 4. Verification Results and Discussion

Three cases are conducted based on HiL platform, each involving different configurations. These cases serve to verify the proposed TGDC in terms of its effectiveness and real-time performance under complex scenarios.

### A. HiL Platform, Benchmarks, and Vehicle Model Verification

As depicted in Figure 4, the real-time HiL platform consists of a host PC. The host PC provides the double lane change (DLC) path-tracking scenarios and offers a high-fidelity vehicle dynamics model. A Speedgoat real-time target machine serves as the computational platform for TGDC to control the vehicle. The host PC and the Speedgoat real-time target machine communicate via UDP to exchange necessary environmental information and vehicle state data for the control algorithm, which are displayed in real-time on a monitor. Furthermore, the real-time target machine generates control commands at a rate of 1000 Hz.

To provide a clear and concise comparison of the characteristics of TGDC, the features and abbreviations of the controllers slated for comparison are summarized in Table 1. “Normal polytopic” refers to the polytopic depicted in Figure 2(a), while “novel polytopic” refers to the polytopic shown in Figure 2(b). The parameters of the ego vehicle are detailed in Table 2.

To validate the correctness and effectiveness of the previously established single-track dynamics model, a comparison was conducted with the CarSim model. In the comparison, the control input was a rapid steering wheel angle, with a vehicle velocity set at 17.5 m/s. Figure 5(a) shows the control input configuration, while Figure 5(b)

**FIGURE 4** The HiL platform.![Diagram of the HiL platform setup. A Host PC (tower) is connected via a UDP link to a Real-time target machine (ruggedized box). The Host PC displays a simulation of an 'Ego vehicle' on a monitor. The monitor shows a car on a road. A steering wheel and pedals are also visible. Red lines indicate connections between the Host PC and the monitor, and between the monitor and the real-time target machine.](cfda9df1319e04207eb28bcefd1dab7b_img.jpg)

Diagram of the HiL platform setup. A Host PC (tower) is connected via a UDP link to a Real-time target machine (ruggedized box). The Host PC displays a simulation of an 'Ego vehicle' on a monitor. The monitor shows a car on a road. A steering wheel and pedals are also visible. Red lines indicate connections between the Host PC and the monitor, and between the monitor and the real-time target machine.

**TABLE 2** Parameters of the ego vehicle.

| Parameters | Definition                                         | Value  |
|------------|----------------------------------------------------|--------|
| $m$        | Vehicle mass (kg)                                  | 1412   |
| $I_z$      | Vehicle yaw inertia ( $\text{kg}\cdot\text{m}^2$ ) | 1536.7 |
| $l_f$      | Distance from front axle to C.G. (m)               | 1.015  |
| $l_r$      | Distance from rear axle to C.G. (m)                | 1.895  |
| $C_{af0}$  | Front tires' nominal cornering stiffness (N/rad)   | 56300  |
| $C_{ar0}$  | Rear tires' nominal cornering stiffness (N/rad)    | 44750  |


**FIGURE 5** Vehicle model verification.![Figure 5: Vehicle model verification. (a) Control input verification showing steering angle delta [rad] vs time t [s]. (b) Lateral dynamic responses showing lateral velocity V_y [m/s] and yaw rate [rad/s] vs time t [s]. Both plots compare the Carsim model (solid line) and the Single-track dynamics model (dashed line).](7c2f0efb2c5d10a52ce19ba33d9d3cec_img.jpg)

(a) The control input of vehicle model verification

(b) The lateral dynamic responses of vehicle model verification

Figure 5: Vehicle model verification. (a) Control input verification showing steering angle delta [rad] vs time t [s]. (b) Lateral dynamic responses showing lateral velocity V\_y [m/s] and yaw rate [rad/s] vs time t [s]. Both plots compare the Carsim model (solid line) and the Single-track dynamics model (dashed line).



illustrates the resulting responses of the lateral velocity and yaw rate. By comparing the responses of the established single-track dynamics model with those from the CarSim model, the results show that the single-track dynamics model closely matches the dynamics of the CarSim model under high-speed and rapid steering conditions. This indicates that the single-track dynamics model effectively reflects the dynamic behavior of a real vehicle. Therefore, it can be used for further controller design.

## B. Case 1: Verification of Time-Varying Parameters

In this simulation case, the controller is required to track a DLC path with varying road adhesion coefficients under changing vehicle velocity. The objective is to validate the path-tracking performance of TGDC under time-varying parameter conditions. The vehicle's initial longitudinal velocity is set at 17.5 m/s, with an applied acceleration allowing the vehicle to gradually increase its velocity. The road surface is a docking surface with adhesion coefficients changing through values of 0.85, 0.6, and 0.35, corresponding to dry, wet, and icy conditions, respectively.

The path-tracking results for different controllers are shown in Figure 6, where the gray, light blue, and white areas represent dry, wet, and icy road conditions, respectively. It can be observed that, even under varying road adhesion coefficients and vehicle velocity, TGDC accurately and stably tracks the desired path at high velocity. At points where road adhesion coefficients change

abruptly, TGDC exhibits smaller deviations from the desired path.

To further analyze tracking errors across controllers, Figure 7 presents the lateral error and yaw angle error, and Table 3 lists the root mean square (RMS) values of these errors. The results indicate that TGDC outperforms the LQR controller, which does not account for parameter variations, in terms of path-tracking performance under time-varying conditions.

Additionally, the vehicle's lateral dynamic response (Figure 8) and control input variations (Figure 9) demonstrate that TGDC achieves smooth control implementation. The velocity variation of TGDC under Case 1 conditions is also shown in Figure 9. Compared to LQR, TGDC reduces peak lateral dynamic responses, enhancing vehicle stability. Furthermore, compared to the LQR-T controller, which also considers parameter variations, TGDC demonstrates superior tracking accuracy due to its use of a less conservative polytopic model, leading to improved tracking performance.

## C. Case 2: Verification of Delay

As previously mentioned, the delay consists of two main components: signal transmission delay is usually within a few milliseconds, but may reach up to 0.05–0.2 s in severe conditions [32, 33, 34]; and mechanical delay typically hovers around 0.1 s [22, 35]. In this case, the delay is manually set within the control system, and the simulations are conducted with total delay levels

**FIGURE 6** Path-tracking results under Case 1.

![Figure 6: Path-tracking results under Case 1. The figure consists of two subplots. The top subplot shows the Global Y [m] versus Global X [m]. The path is a curved line with three segments representing different road adhesion coefficients: dry (gray, μ = 0.85), wet (light blue, μ = 0.6), and icy (white, μ = 0.35). The legend shows the 'Desire path' (dashed orange line) and the trajectories for 'TGDC' (solid blue line), 'LQR' (solid red line), and 'LQR-T' (solid green line). The bottom subplot shows the Yaw [rad] versus time t [s]. The legend is the same as the top plot. The yaw rate fluctuates, with insets showing the values for each road condition: dry (0.195), wet (0.19), and icy (0.185). The TGDC trajectory (blue) closely follows the desire path (orange dashed line) in both plots, while the LQR (red) and LQR-T (green) trajectories show larger deviations, especially during the transition between road conditions.](fef288b92fc7299b718bb8d6107421c0_img.jpg)

Figure 6: Path-tracking results under Case 1. The figure consists of two subplots. The top subplot shows the Global Y [m] versus Global X [m]. The path is a curved line with three segments representing different road adhesion coefficients: dry (gray, μ = 0.85), wet (light blue, μ = 0.6), and icy (white, μ = 0.35). The legend shows the 'Desire path' (dashed orange line) and the trajectories for 'TGDC' (solid blue line), 'LQR' (solid red line), and 'LQR-T' (solid green line). The bottom subplot shows the Yaw [rad] versus time t [s]. The legend is the same as the top plot. The yaw rate fluctuates, with insets showing the values for each road condition: dry (0.195), wet (0.19), and icy (0.185). The TGDC trajectory (blue) closely follows the desire path (orange dashed line) in both plots, while the LQR (red) and LQR-T (green) trajectories show larger deviations, especially during the transition between road conditions.

**FIGURE 7** Path-tracking error under Case 1.![Figure 7: Path-tracking error under Case 1. Two plots showing lateral error e_y [m] and yaw angle error e_ψ [rad] over time t [s].](f176174c2978785e86a8352bd45e322e_img.jpg)

Figure 7 consists of two vertically stacked plots showing path-tracking error over time  $t$  [s] from 0 to 10. The top plot shows the lateral error  $e_y$  [m] on the y-axis, ranging from -0.4 to 0.4. The bottom plot shows the yaw angle error  $e_\psi$  [rad] on the y-axis, ranging from -0.1 to 0.05. Both plots compare three controllers: TGDC (blue line), LQR (red line), and LQR-T (green line). An inset in the bottom plot zooms in on the error between 2 and 4 seconds, with a y-axis scale from 0.045 to 0.055. The TGDC controller shows the smallest errors in both plots.

Figure 7: Path-tracking error under Case 1. Two plots showing lateral error e\_y [m] and yaw angle error e\_ψ [rad] over time t [s].

**TABLE 3** Path-tracking error under Case 1.

| Controller | Lateral error [m] |        | Yaw angle error [rad] |        |
|------------|-------------------|--------|-----------------------|--------|
|            | Max               | RMS    | Max                   | RMS    |
| TGDC       | 0.3012            | 0.0890 | -0.0535               | 0.0135 |
| LQR        | -0.4800           | 0.1398 | -0.1097               | 0.0283 |
| LQR-T      | 0.3654            | 0.0898 | -0.0648               | 0.0162 |

© SAE International

**FIGURE 8** Path-tracking lateral dynamic responses under Case 1.![Figure 8: Path-tracking lateral dynamic responses under Case 1. Two plots showing lateral velocity V_y [m/s] and yaw rate over time t [s].](6279fafb3a874e174648eb907385c954_img.jpg)

Figure 8 consists of two side-by-side plots showing lateral dynamic responses over time  $t$  [s] from 0 to 10. The left plot shows the lateral velocity  $V_y$  [m/s] on the y-axis, ranging from -0.5 to 0.5. The right plot shows the yaw rate on the y-axis, ranging from -0.4 to 0.4. Both plots compare three controllers: TGDC (blue line), LQR (red line), and LQR-T (green line). The TGDC controller shows the most stable and smallest dynamic responses.

Figure 8: Path-tracking lateral dynamic responses under Case 1. Two plots showing lateral velocity V\_y [m/s] and yaw rate over time t [s].

**FIGURE 9** The control input and vehicle velocity of TGDC under Case 1.![Figure 9: The control input and vehicle velocity of TGDC under Case 1. Two plots showing steering angle delta and longitudinal velocity V_x over time t [s].](83dedc2074a453d13ce74cc2e1ae4ff5_img.jpg)

Figure 9 consists of two side-by-side plots showing the control input and vehicle velocity of the TGDC controller over time  $t$  [s] from 0 to 10. The left plot shows the steering angle  $\delta$  [deg] on the y-axis, ranging from -40 to 20. The right plot shows the longitudinal velocity  $V_x$  [m/s] on the y-axis, ranging from 18 to 22. Both plots show the TGDC controller's response (blue line). The steering angle shows a significant transient response around 4 seconds, while the longitudinal velocity shows a steady increase.

Figure 9: The control input and vehicle velocity of TGDC under Case 1. Two plots showing steering angle delta and longitudinal velocity V\_x over time t [s].

© SAE International

**FIGURE 10** Path-tracking results under Case 2.![Figure 10: Path-tracking results under Case 2. (a) Delay levels of 0.15 s. (b) Delay levels of 0.3 s. Both plots show Global X [m] vs Global Y [m] and Yaw [rad] vs t [s].](e6b5ee67ac260b0a3ed3e3c5ad7ea19c_img.jpg)

Figure 10 consists of two subplots, (a) and (b), showing path-tracking results under Case 2. Both plots compare the performance of four controllers: Desire path (dashed orange line), TGDC (solid blue line), LQR (solid red line), and LQR-D (solid green line). The top plot in each subplot shows the vehicle's position (Global X [m] on the x-axis, ranging from 0 to 120, and Global Y [m] on the y-axis, ranging from -2 to 4). The bottom plot shows the yaw angle (Yaw [rad] on the y-axis, ranging from -0.5 to 0.5) versus time (t [s] on the x-axis, ranging from 0 to 10). In subplot (a), the delay is 0.15 s. The LQR controller (red) fails to converge to the straight segments of the path, while TGDC (blue) and LQR-D (green) maintain tracking. In subplot (b), the delay is 0.3 s. The LQR controller (red) shows sustained oscillations and fails to converge. TGDC (blue) and LQR-D (green) maintain good tracking performance. An inset in subplot (b) shows a zoomed-in view of the path tracking between X=40 and X=80, with a scale bar indicating a distance of 3.75 m and yaw angles of -1.66 and -1.68 rad. The adhesion coefficient  $\mu = 0.85$  is indicated in both plots.

Figure 10: Path-tracking results under Case 2. (a) Delay levels of 0.15 s. (b) Delay levels of 0.3 s. Both plots show Global X [m] vs Global Y [m] and Yaw [rad] vs t [s].

of 0.15 s (0.05 s + 0.1 s) and 0.3 s (0.2 s + 0.1 s). The vehicle velocity is set at 20 m/s with a constant road adhesion coefficient of 0.85 to verify the path-tracking performance of the controller in the presence of delays.

The path-tracking results of different controllers under two delay conditions at high velocity are shown in [Figure 10](#). It is evident that without delay compensation ([Figure 10\(a\)](#)), the LQR controller fails to converge the vehicle to the straight segments of the DLC, resulting in a loss of vehicle stability. In contrast, as shown in [Figure 10\(a\)](#) and [10\(b\)](#), both the TGDC and LQR-D controllers maintain tracking performance and ensure stability under delays of 0.15 s and 0.3 s.

Additionally, the tracking error in [Figure 11\(a\)](#) reveals that the LQR controller performs poorly in path tracking, with sustained oscillations in tracking error and a lack of convergence. However, with the introduction of delay compensation, the controllers maintain good path-tracking performance even under larger delays. The detailed tracking error results in [Figure 11](#) and [Table 4](#) indicate that both TGDC and LQR-D controllers ensure error convergence and maintain vehicle steering stability,

thereby offering superior path-tracking performance compared to controllers without delay compensation.

Furthermore, the lateral dynamic responses under both delay conditions are shown in [Figure 12\(a\)](#) and [12\(b\)](#), confirming that a lack of delay compensation leads to vehicle stability loss in the presence of delays. [Figure 13](#) displays the control input variations of TGDC under two different delay conditions, indicating that the control execution by TGDC is smooth. The velocity variation of TGDC under Case 2 conditions is also shown in [Figure 14](#). Additionally, compared to the LQR-D controller, which only considers delay compensation, TGDC exhibits marginally lower tracking precision and slightly higher peak lateral dynamic responses. This is because direct modeling is more precise under conditions of known parameters than modeling using a polytopic.

However, from a practical application perspective, the minor accuracy trade-off in exchange for greater adaptability of the controller is highly beneficial.

## D. Case 3: Comprehensive Performance Analysis

To comprehensively analyze the overall capabilities of the TGDC, this case sets the initial vehicle velocity at 15 m/s and applies a certain acceleration to the simulation vehicle, allowing for a continuous increase in velocity. The road conditions are the same as in Case 1, transitioning from an adhesion coefficient of 0.85 to 0.6 and then to 0.35. The delay is set at 0.15 s (0.05 s + 0.1 s).

The simulation results shown in [Figure 15](#) demonstrate that, under high-speed conditions with time-varying road adhesion coefficients, vehicle velocity, and control system delays, both TGDC and LQR-TD closely match the desired path, and the yaw angle tracks the expected trajectory well, validating the effectiveness of TGDC. However, due to the use of the normal polytopic model, the tracking accuracy of the LQR-TD controller does not achieve the same level as TGDC.

[Figure 16](#) and [Table 5](#) accurately describe the lateral error and yaw angle error. It can be observed that TGDC not only maintains the vehicle's steering stability but also ensures tracking accuracy. Under the complex conditions set, the maximum lateral error of TGDC is within 0.52 m, and the maximum yaw angle error is approximately 0.12 radians, indicating that TGDC improves the vehicle's path-tracking performance under complex conditions. The lateral dynamic response of the vehicle in [Figure 17](#) further confirms this observation. [Figure 18](#) demonstrates the smooth control process executed by TGDC.

The real-time performance of TGDC and LQR-TD is shown in [Figure 19](#). It is evident that even under complex conditions, due to the offline computation characteristics of gain scheduling, both TGDC and LQR-TD exhibit outstanding real-time performance, with each step computation time on the order of  $10^{-6}$  s. Both TGDC and LQR-TD are capable of tracking the desired path under

**FIGURE 11** Path-tracking error under Case 2.![Figure 11: Path-tracking error under Case 2. The figure consists of four subplots showing the path-tracking error e_y [m] and e_psi [rad] over time t [s] for three controllers: TGDC (blue), LQR (red), and LQR-D (green). The top two subplots show the error during a maneuver with vertical red lines indicating obstacles. The bottom two subplots show the error for delay levels of 0.15 s and 0.3 s.](c2b98986bdf45e15707f6b2bd7ade2bd_img.jpg)

Figure 11 displays the path-tracking error under Case 2, comparing three controllers: TGDC (blue line), LQR (red line), and LQR-D (green line). The figure is divided into two main sections: (a) Delay levels of 0.15 s and (b) Delay levels of 0.3 s. Each section contains two subplots: one for lateral error  $e_y$  [m] and one for heading error  $e_\psi$  [rad].

**(a) Delay levels of 0.15 s**

- Top subplot ( $e_y$  [m]):** The x-axis is time  $t$  [s] from 0 to 10. The y-axis is lateral error  $e_y$  [m] from -0.2 to 0.2. Vertical red lines at  $t \approx 1.8, 2.2, 3.2, 3.6, 4.0, 5.0, 5.4, 6.4, 6.8, 7.2, 8.2, 8.6$  s indicate obstacles. The LQR controller (red) shows large oscillations and collisions. The LQR-D controller (green) shows a small peak at  $t \approx 4.2$  s. The TGDC controller (blue) shows a small peak at  $t \approx 4.2$  s and then remains near zero. An inset shows a zoomed-in view of the error between  $t=4.5$  and  $t=5.5$  s, with values ranging from -0.065 to -0.055 rad.
- Bottom subplot ( $e_\psi$  [rad]):** The x-axis is time  $t$  [s] from 0 to 10. The y-axis is heading error  $e_\psi$  [rad] from -0.05 to 0.05. The LQR controller (red) shows large oscillations. The LQR-D controller (green) shows a small peak at  $t \approx 4.2$  s. The TGDC controller (blue) shows a small peak at  $t \approx 4.2$  s and then remains near zero. An inset shows a zoomed-in view of the error between  $t=4.5$  and  $t=5.5$  s, with values ranging from -0.065 to -0.055 rad.

**(b) Delay levels of 0.3 s**

- Top subplot ( $e_y$  [m]):** The x-axis is time  $t$  [s] from 0 to 10. The y-axis is lateral error  $e_y$  [m] from -0.2 to 0.6. The LQR controller (red) shows a large peak at  $t \approx 4.2$  s. The LQR-D controller (green) shows a large peak at  $t \approx 4.2$  s. The TGDC controller (blue) shows a large peak at  $t \approx 4.2$  s. An inset shows a zoomed-in view of the error between  $t=4.5$  and  $t=5.5$  s, with values ranging from 0.6 to 0.7 rad.
- Bottom subplot ( $e_\psi$  [rad]):** The x-axis is time  $t$  [s] from 0 to 10. The y-axis is heading error  $e_\psi$  [rad] from -0.1 to 0.05. The LQR controller (red) shows a large peak at  $t \approx 4.2$  s. The LQR-D controller (green) shows a large peak at  $t \approx 4.2$  s. The TGDC controller (blue) shows a large peak at  $t \approx 4.2$  s.

© SAE International

Figure 11: Path-tracking error under Case 2. The figure consists of four subplots showing the path-tracking error e\_y [m] and e\_psi [rad] over time t [s] for three controllers: TGDC (blue), LQR (red), and LQR-D (green). The top two subplots show the error during a maneuver with vertical red lines indicating obstacles. The bottom two subplots show the error for delay levels of 0.15 s and 0.3 s.

**TABLE 4** Path-tracking error under Case 2.

| Delay [s] | Controller | Lateral error [m] |        | Yaw angle error [rad] |        |
|-----------|------------|-------------------|--------|-----------------------|--------|
|           |            | Max               | RMS    | Max                   | RMS    |
| 0.15      | TGDC       | 0.2131            | 0.0734 | -0.0632               | 0.0252 |
|           | LQR        | -5.9191           | 2.4050 | -0.5947               | 0.2620 |
|           | LQR-D      | 0.1899            | 0.0654 | 0.0604                | 0.0243 |
| 0.3       | TGDC       | 0.6711            | 0.2421 | -0.1127               | 0.0424 |
|           | LQR-D      | 0.6472            | 0.2334 | -0.1103               | 0.0416 |

**FIGURE 12** Path-tracking lateral dynamic responses under Case 2.![Figure 12: Path-tracking lateral dynamic responses under Case 2. The figure consists of four subplots arranged in a 2x2 grid. The top row shows results for a delay level of 0.15 s, and the bottom row shows results for a delay level of 0.3 s. The left column plots lateral velocity V_y [m/s] against time t [s], and the right column plots yaw rate [rad/s] against time t [s]. Each plot compares three controllers: TGDC (blue line), LQR (red line), and LQR-D (green line). In the 0.15 s delay plots, V_y ranges from -2 to 2 and yaw rate from -2 to 2. In the 0.3 s delay plots, V_y ranges from -0.2 to 0.2 and yaw rate from -0.4 to 0.4. The LQR controller shows significantly higher oscillations and larger errors compared to TGDC and LQR-D, especially at the 0.3 s delay level. Insets in the bottom row plots show zoomed-in views of the initial transient response for TGDC and LQR-D.](fe753d01ad5fe6cf150018c958173c6d_img.jpg)

Figure 12: Path-tracking lateral dynamic responses under Case 2. The figure consists of four subplots arranged in a 2x2 grid. The top row shows results for a delay level of 0.15 s, and the bottom row shows results for a delay level of 0.3 s. The left column plots lateral velocity V\_y [m/s] against time t [s], and the right column plots yaw rate [rad/s] against time t [s]. Each plot compares three controllers: TGDC (blue line), LQR (red line), and LQR-D (green line). In the 0.15 s delay plots, V\_y ranges from -2 to 2 and yaw rate from -2 to 2. In the 0.3 s delay plots, V\_y ranges from -0.2 to 0.2 and yaw rate from -0.4 to 0.4. The LQR controller shows significantly higher oscillations and larger errors compared to TGDC and LQR-D, especially at the 0.3 s delay level. Insets in the bottom row plots show zoomed-in views of the initial transient response for TGDC and LQR-D.

**FIGURE 13** The control input of TGDC under Case 2.![Figure 13: The control input of TGDC under Case 2. The figure consists of two subplots. Subplot (a) shows the control input delta [deg] versus time t [s] for a delay level of 0.15 s. Subplot (b) shows the control input delta [deg] versus time t [s] for a delay level of 0.3 s. In both cases, the control input is zero until approximately t=1.5 s, then follows a similar profile with a peak around t=4.5 s and a dip around t=4 s. The y-axis for delta [deg] ranges from -5 to 5, and the x-axis for t [s] ranges from 0 to 10.](239211fa511b4ffa685b54b5132ec927_img.jpg)

Figure 13: The control input of TGDC under Case 2. The figure consists of two subplots. Subplot (a) shows the control input delta [deg] versus time t [s] for a delay level of 0.15 s. Subplot (b) shows the control input delta [deg] versus time t [s] for a delay level of 0.3 s. In both cases, the control input is zero until approximately t=1.5 s, then follows a similar profile with a peak around t=4.5 s and a dip around t=4 s. The y-axis for delta [deg] ranges from -5 to 5, and the x-axis for t [s] ranges from 0 to 10.

**FIGURE 14** The vehicle velocity of TGDC under Case 2.![Figure 14: A line graph showing the vehicle velocity Vx [m/s] versus time t [s]. The y-axis ranges from 19.8 to 20.2 m/s, and the x-axis ranges from 0 to 10 seconds. The velocity starts at 20.0 m/s, fluctuates between 19.9 and 20.1 m/s until t=4s, then rises sharply to a peak of approximately 20.15 m/s at t=4.5s, and finally settles to a steady state of 20.0 m/s by t=7s.](b3df5964338063224492c01f09e4fed6_img.jpg)

Figure 14: A line graph showing the vehicle velocity Vx [m/s] versus time t [s]. The y-axis ranges from 19.8 to 20.2 m/s, and the x-axis ranges from 0 to 10 seconds. The velocity starts at 20.0 m/s, fluctuates between 19.9 and 20.1 m/s until t=4s, then rises sharply to a peak of approximately 20.15 m/s at t=4.5s, and finally settles to a steady state of 20.0 m/s by t=7s.

**FIGURE 15** Path-tracking results under Case 3.![Figure 15: Path-tracking results under Case 3. The top plot shows Global Y [m] versus Global X [m]. The y-axis ranges from -2 to 4 m, and the x-axis ranges from 0 to 120 m. A dashed yellow line represents the 'Desire path'. A solid blue line represents 'TGDC', and a solid red line represents 'LQR-TD'. The path starts at (0,0), follows the desire path until X=40m where it deviates downwards, and then follows it again until X=80m where it deviates downwards once more. Insets show zoomed-in views of the tracking performance at different points. The bottom plot shows Yaw [rad] versus time t [s]. The y-axis ranges from -0.4 to 0.2 rad, and the x-axis ranges from 0 to 10 s. The yaw angle follows the desire path (dashed yellow) with the TGDC (blue) and LQR-TD (red) controllers. Insets show zoomed-in views of the yaw angle tracking performance.](e95f47f7a4c01c8889d6d46919b4c73d_img.jpg)

Figure 15: Path-tracking results under Case 3. The top plot shows Global Y [m] versus Global X [m]. The y-axis ranges from -2 to 4 m, and the x-axis ranges from 0 to 120 m. A dashed yellow line represents the 'Desire path'. A solid blue line represents 'TGDC', and a solid red line represents 'LQR-TD'. The path starts at (0,0), follows the desire path until X=40m where it deviates downwards, and then follows it again until X=80m where it deviates downwards once more. Insets show zoomed-in views of the tracking performance at different points. The bottom plot shows Yaw [rad] versus time t [s]. The y-axis ranges from -0.4 to 0.2 rad, and the x-axis ranges from 0 to 10 s. The yaw angle follows the desire path (dashed yellow) with the TGDC (blue) and LQR-TD (red) controllers. Insets show zoomed-in views of the yaw angle tracking performance.

**FIGURE 16** Path-tracking error under Case 3.![Figure 16: Path-tracking error under Case 3. The top plot shows the lateral error e_y [m] versus time t [s]. The y-axis ranges from -0.5 to 0.5 m, and the x-axis ranges from 0 to 10 s. The error for both TGDC (blue) and LQR-TD (red) controllers starts at 0, remains near 0 until t=2s, then increases to a peak of approximately 0.5 m at t=4.5s, and then decreases back towards 0. The bottom plot shows the yaw error e_psi [rad] versus time t [s]. The y-axis ranges from -0.1 to 0.1 rad, and the x-axis ranges from 0 to 10 s. The error for both controllers starts at 0, remains near 0 until t=2s, then increases to a peak of approximately 0.08 rad at t=4.5s, and then decreases back towards 0.](011fecb4a85637472f0c697a6cbdb15d_img.jpg)

Figure 16: Path-tracking error under Case 3. The top plot shows the lateral error e\_y [m] versus time t [s]. The y-axis ranges from -0.5 to 0.5 m, and the x-axis ranges from 0 to 10 s. The error for both TGDC (blue) and LQR-TD (red) controllers starts at 0, remains near 0 until t=2s, then increases to a peak of approximately 0.5 m at t=4.5s, and then decreases back towards 0. The bottom plot shows the yaw error e\_psi [rad] versus time t [s]. The y-axis ranges from -0.1 to 0.1 rad, and the x-axis ranges from 0 to 10 s. The error for both controllers starts at 0, remains near 0 until t=2s, then increases to a peak of approximately 0.08 rad at t=4.5s, and then decreases back towards 0.

**TABLE 5** Path-tracking error under Case 3.

| Controller | Lateral error [m] |        | Yaw angle error [rad] |        |
|------------|-------------------|--------|-----------------------|--------|
|            | Max               | RMS    | Max                   | RMS    |
| TGDC       | 0.5151            | 0.1637 | -0.1204               | 0.0325 |
| LQR-TD     | 0.5496            | 0.1901 | -0.1324               | 0.0362 |

© SAE International

**FIGURE 17** Path-tracking lateral dynamic responses under Case 3.![Figure 17: Path-tracking lateral dynamic responses under Case 3. Two side-by-side plots show lateral velocity (V_y) and yaw rate over 10 seconds. The left plot shows V_y [m/s] ranging from -0.6 to 0.4. The right plot shows Yaw rate [rad/s] ranging from -0.4 to 0.4. Both plots compare TGDC (blue line) and LQR-TD (red line).](a706c91f074ac2840c161a3d4a7c0f91_img.jpg)

Figure 17 consists of two side-by-side plots showing lateral dynamic responses over a time period of 0 to 10 seconds. The left plot displays the lateral velocity  $V_y$  in  $\text{m/s}$  on the y-axis, ranging from -0.6 to 0.4. The right plot displays the yaw rate in  $\text{rad/s}$  on the y-axis, ranging from -0.4 to 0.4. Both plots compare the performance of two controllers: TGDC (represented by a blue line) and LQR-TD (represented by a red line). In both cases, the LQR-TD controller exhibits significantly larger oscillations and higher peak values compared to the TGDC controller, which shows smoother and more controlled responses.

Figure 17: Path-tracking lateral dynamic responses under Case 3. Two side-by-side plots show lateral velocity (V\_y) and yaw rate over 10 seconds. The left plot shows V\_y [m/s] ranging from -0.6 to 0.4. The right plot shows Yaw rate [rad/s] ranging from -0.4 to 0.4. Both plots compare TGDC (blue line) and LQR-TD (red line).

**FIGURE 18** The control input and vehicle velocity of TGDC under Case 3.![Figure 18: The control input and vehicle velocity of TGDC under Case 3. Two side-by-side plots show steering angle (delta) and longitudinal velocity (V_x) over 10 seconds. The left plot shows delta [deg] ranging from -5 to 10. The right plot shows V_x [m/s] ranging from 14 to 22.](250cf77a1cd51989da09fca796b3e4ea_img.jpg)

Figure 18 consists of two side-by-side plots showing the control input and vehicle velocity of the TGDC controller over a time period of 0 to 10 seconds. The left plot displays the steering angle  $\delta$  in degrees on the y-axis, ranging from -5 to 10. The right plot displays the longitudinal velocity  $V_x$  in  $\text{m/s}$  on the y-axis, ranging from 14 to 22. Both plots show the TGDC controller's response (blue line). The steering angle plot shows significant oscillations, particularly between 2 and 5 seconds, before settling. The longitudinal velocity plot shows a steady increase from approximately 15  $\text{m/s}$  to 21  $\text{m/s}$  over the 10-second period.

Figure 18: The control input and vehicle velocity of TGDC under Case 3. Two side-by-side plots show steering angle (delta) and longitudinal velocity (V\_x) over 10 seconds. The left plot shows delta [deg] ranging from -5 to 10. The right plot shows V\_x [m/s] ranging from 14 to 22.

**FIGURE 19** The computing time under Case 3.![Figure 19: The computing time under Case 3. A plot showing computing time (s) x 10^-6 versus Time [s] from 0 to 10. The plot compares TGDC (blue line) and LQR-TD (red line).](dbc1673750fd53d4203f4d93963fdab6_img.jpg)

Figure 19 is a plot showing the computing time in seconds (scaled by  $10^{-6}$ ) versus time in seconds from 0 to 10. The y-axis ranges from 3.9 to 4.2. The plot compares the computing time of two controllers: TGDC (blue line) and LQR-TD (red line). Both controllers exhibit fluctuating computing times throughout the 10-second period. The LQR-TD controller generally shows higher and more frequent peaks in computing time compared to the TGDC controller, which has a more consistent but slightly lower average computing time.

Figure 19: The computing time under Case 3. A plot showing computing time (s) x 10^-6 versus Time [s] from 0 to 10. The plot compares TGDC (blue line) and LQR-TD (red line).

time-varying parameters and control delays, and since both utilize the gain scheduling principle, their computation times remain extremely low (on the order of  $10^{-6}$  s). This demonstrates that both TGDC and LQR-TD, with gain scheduling, have a very low computational load.

In summary, results under various validation conditions have demonstrated that the TGDC achieves high path-tracking accuracy and smooth control, even in the presence of time-varying vehicle states, road conditions, and control delays. This enhances both the vehicle's path-tracking performance and stability, while also facilitating real-time implementation.

# 5. Conclusion

This article introduces a gain-scheduled path-tracking controller, TGDC, which accounts for time-varying vehicle states, road conditions, and control system delays, aimed at enhancing the path-tracking performance of AVs under complex conditions. To mitigate the impact of time-varying parameters and reduce the conservatism of the LPV system, a novel polytopic-based path-tracking model has been developed for the design of TGDC, enhancing its robustness against time-varying parameters. A delay compensation strategy, integrated with optimization theory, has been constructed to compensate for control system delays. In line with the characteristics of the established model, the TGDC employs a strategy of offline gain computation and online weight calculation to ensure a low computational burden. Experiments conducted on a HiL platform have demonstrated the effectiveness and reliability of the TGDC.

# Acknowledgements

This work was supported in part by the National Natural Science Foundation of China under Grant 52272386, in part by the Fundamental Research Funds for the Central Universities, in part by the China Postdoctoral Science Foundation under Grant Numbers 2024T171128 and 2024M764122, and in part by the Postdoctoral Fellowship Program of CPSF under Grant GZC20233402.

# Contact Information

**Yechen Qin**, corresponding author  
[qinyechen@bit.edu.cn](mailto:qinyechen@bit.edu.cn)

# References

- Chen, L., Teng, S., Li, B., Na, X. et al., "Milestones in Autonomous Driving and Intelligent Vehicles—Part II: Perception and Planning," *IEEE Transactions on Systems, Man, and Cybernetics: Systems* 53, no. 10 (2023): 6401-6415.
- Zhang, Y., Xu, M., Qin, Y., Dong, M. et al., "Mile: Multiobjective Integrated Model Predictive Adaptive Cruise Control for Intelligent Vehicle," *IEEE Transactions on Industrial Informatics* 19, no. 7 (2022): 8539-8548.
- Jiang, S., Wu, G., Li, Y., Mao, L. et al., "Intelligent Vehicle Path Tracking and Stability Cooperative Control Strategy Based on Stable Domain," *SAE Int. J. Veh. Dyn., Stab., and NVH* 8, no. 4 (2024): 445-465, doi:<https://doi.org/10.4271/10-08-04-0025>.
- Qin, Y., Hashemi, E., and Khajepour, A., "Integrated Crash Avoidance and Mitigation Algorithm for Autonomous Vehicles," *IEEE Transactions on Industrial Informatics* 17, no. 11 (2021): 7246-7255.
- Negash, N. and Yang, J., "Anticipation-Based Autonomous Platoon Control Strategy with Minimum Parameter Learning Adaptive Radial Basis Function Neural Network Sliding Mode Control," *SAE Int. J. Veh. Dyn., Stab., and NVH* 6, no. 3 (2022): 247-265, doi:<https://doi.org/10.4271/10-06-03-0017>.
- Lu, X., Xing, Y., Guirog, Z., Bo, L. et al., "Review on Motion Control of Autonomous Vehicles," *Journal of Mechanical Engineering* 56, no. 10 (2020): 127-143.
- Tian, Y., Yao, Q., Hang, P., and Wang, S., "A Gain-Scheduled Robust Controller for Autonomous Vehicles Path Tracking Based on LPV System with MPC and  $H_\infty$ ," *IEEE Transactions on Vehicular Technology* 71, no. 9 (2022): 9350-9362.
- Zha, Y., Deng, J., Qiu, Y., Zhang, K. et al., "A Survey of Intelligent Driving Vehicle Trajectory Tracking Based on Vehicle Dynamics," *SAE Int. J. Veh. Dyn., Stab., and NVH* 7, no. 2 (2023): 221-248, doi:<https://doi.org/10.4271/10-07-02-0014>.
- Rokonuzzaman, M., Mohajer, N., Nahavandi, S., and Mohamed, S., "Review and Performance Evaluation of Path Tracking Controllers of Autonomous Vehicles," *IET Intelligent Transport Systems* 15, no. 5 (2021): 646-670.
- Sun, C., Dong, H., Zhang, X., and Geng, C., "Path Tracking Controller Design for Autonomous Vehicle Based on Robust Tube MPC," *International Journal of Vehicle Design* 82, no. 1-4 (2020): 120-139.
- Li, P., Nguyen, A.-T., Du, H., Wang, Y. et al., "Polytopic LPV Approaches for Intelligent Automotive Systems: State of the Art and Future Challenges," *Mechanical Systems and Signal Processing* 161 (2021): 107931.
- Hang, P., Chen, X., and Luo, F., "LPV/ $H_\infty$  Controller Design for Path Tracking of Autonomous Ground Vehicles through Four-Wheel Steering and Direct Yaw-Moment Control," *International Journal of Automotive Technology* 20 (2019): 679-691.
- Liang, J., Tian, Q., Feng, J., Pi, D. et al., "A Polytopic Model-Based Robust Predictive Control Scheme for Path Tracking of Autonomous Vehicles," *IEEE Transactions on Intelligent Vehicles* 9, no. 2 (2024): 3928-3939.
- Hang, P. and Chen, X., "Path Tracking Control of 4-Wheel-Steering Autonomous Ground Vehicles Based

- on Linear Parameter-Varying System with Experimental Verification," *Proceedings of the Institution of Mechanical Engineers, Part I: Journal of Systems and Control Engineering* 235, no. 3 (2021): 411-423.
15. Chu, H., Meng, D., Huang, S., Tian, M. et al., "Autonomous High-Speed Overtaking of Intelligent Chassis Using Fast Iterative Model Predictive Control," *IEEE Transactions on Transportation Electrification* 10, no. 1 (2023): 1244-1256.
  16. Aouadj, N., Hartani, K., and Fatih, M., "New Integrated Vehicle Dynamics Control System Based on the Coordination of Active Front Steering, Direct Yaw Control, and Electric Differential for Improvements in Vehicle Handling and Stability," *SAE Int. J. Veh. Dyn., Stab., and NVH* 4, no. 2 (2020): 119-133, doi:<https://doi.org/10.4271/10-04-02-0009>.
  17. Peng, H., Wang, W., An, Q., Xiang, C. et al., "Path Tracking and Direct Yaw Moment Coordinated Control Based on Robust MPC with the Finite Time Horizon for Autonomous Independent-Drive Vehicles," *IEEE Transactions on Vehicular Technology* 69, no. 6 (2020): 6053-6066.
  18. Hang, P., Chen, X., Luo, F., and Fang, S., "Robust Control of a Four-Wheel-Independent-Steering Electric Vehicle for Path Tracking," *SAE Int. J. Veh. Dyn., Stab., and NVH* 1, no. 2 (2017): 307-316, doi:<https://doi.org/10.4271/2017-01-1584>.
  19. Zhang, Y., Lin, Y., Qin, Y., Dong, M. et al., "A New Adaptive Cruise Control Considering Crash Avoidance for Intelligent Vehicle," *IEEE Transactions on Industrial Electronics* 71, no. 1 (2023): 688-696.
  20. Zhang, Y., Hu, Y., Hu, X., Qin, Y. et al., "Adaptive Crash-Avoidance Predictive Control under Multi-vehicle Dynamic Environment for Intelligent Vehicles," *IEEE Transactions on Intelligent Vehicles* (2024).
  21. Wang, R., Jing, H., Hu, C., Yan, F. et al., "Robust H $\infty$  Path Following Control for Autonomous Ground Vehicles with Delay and Data Dropout," *IEEE Transactions on Intelligent Transportation Systems* 17, no. 7 (2016): 2042-2050.
  22. Yu, Z., Mingfan, X., Guangyu, B., Mingming, D. et al., "Intelligent Vehicle Switching Control Considering Dynamic Stability Constraints," *Automotive Engineering* 45, no. 5 (2023): 709-718.
  23. Wenlong, D., Li, C., Wentong, L., and Ju, C., "2DOF Internal Model Control for Steer-by-Wire Systems with Time Delay," *China Mechanical Engineering* 32, no. 16 (2021): 1904-1911.
  24. Xu, S. and Peng, H., "Design, Analysis, and Experiments of Preview Path Tracking Control for Autonomous Vehicles," *IEEE Transactions on Intelligent Transportation Systems* 21, no. 1 (2019): 48-58.
  25. Xu, S., Peng, H., and Tang, Y., "Preview Path Tracking Control with Delay Compensation for Autonomous Vehicles," *IEEE Transactions on Intelligent Transportation Systems* 22, no. 5 (2020): 2979-2989.
  26. Shi, Q. and Zhang, H., "Road-Curvature-Range-Dependent Path Following Controller Design for Autonomous Ground Vehicles Subject to Stochastic Delays," *IEEE Transactions on Intelligent Transportation Systems* 23, no. 10 (2022): 17440-17450.
  27. Yurtsever, E., Lambert, J., Carballo, A., and Takeda, K., "A Survey of Autonomous Driving: Common Practices and Emerging Technologies," *IEEE Access* 8 (2020): 58443-58469.
  28. Zhang, H., Zhang, X., and Wang, J., "Robust Gain-Scheduling Energy-to-Peak Control of Vehicle Lateral Dynamics Stabilisation," *Vehicle System Dynamics* 52, no. 3 (2014): 309-340.
  29. Singh, K.B., Ali Arat, M., and Taheri, S., "An Intelligent Tire Based Tire-Road Friction Estimation Technique and Adaptive Wheel Slip Controller for Antilock Brake System," *Journal of Dynamic Systems, Measurement, and Control* 135, no. 3 (2013): 031002.
  30. Fridman, E., *Introduction to Time-Delay Systems: Analysis and Control* (Cham, Switzerland: Springer, 2014).
  31. Deng, Y., Léchappé, V., Moulay, E., Chen, Z. et al., "Predictor-Based Control of Time-Delay Systems: A Survey," *International Journal of Systems Science* 53, no. 12 (2022): 2496-2534.
  32. Seiffer, A., Frey, M., and Gauterin, F., "Pragmatic and Effective Enhancements for Stanley Path-Tracking Controller by Considering System Delay," *Vehicles* 5, no. 2 (2023): 615-636.
  33. Yu, J., Guo, X., Pei, X., Chen, Z. et al., "Path Tracking Control Based on Tube MPC and Time Delay Motion Prediction," *IET Intelligent Transport Systems* 14, no. 1 (2020): 1-12.
  34. Zhang Y., Niu R., Wang J., Liang H., Chen Z., and Huang Z., "Path Tracking Control Algorithm Considering Delay Compensation," in *2022 7th Asia-Pacific Conference on Intelligent Robot Systems (ACIRS)*, Tianjin, China, 64-69, IEEE, 2022.
  35. Zhang, H., Heng, B., and Zhao, W., "Path Tracking Control for Active Rear Steering Vehicles Considering Driver Steering Characteristics," *IEEE Access* 8 (2020): 98009-98017.

