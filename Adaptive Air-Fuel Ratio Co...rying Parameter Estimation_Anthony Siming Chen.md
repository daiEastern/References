

# Adaptive Air-Fuel Ratio Control for Spark Ignition Engines with Time-Varying Parameter Estimation

Anthony Siming Chen, Jing Na, *Member, IEEE*, Guido Herrmann, *Senior Member, IEEE*,  
Richard Burke and Chris Brace

**Abstract**—This paper presents a novel adaptive controller of air-fuel ratio (AFR) in spark ignition (SI) engines. The controller robustly estimates unknown time-varying engine parameters and thus improves both the transient and steady-state performance. The objective is to regulate the AFR in the combustion chamber around the stoichiometric value by manipulating the injected fuel mass flow rate so as to improve fuel economy and to reduce emissions. The AFR regulation problem is first reformulated into a tracking control problem of the fuel mass flow. This simplifies the control synthesis, i.e. the number of parameters to be online updated can be reduced. Then a representation of the parameter estimation error is derived by using auxiliary filter operations, and used as a new leakage term in the adaptive law. In this case, exponential convergence of the AFR error and the estimation of the time-varying parameters can be proved simultaneously. The proposed controller is compared with a generic adaptive controller using the gradient descent method based on a well-calibrated mean value engine model (MVEM). Finally, the proposed controller is also validated with a commercial engine simulation software, GT-Power, demonstrating better results than for the gradient descent approach.

**Keywords**—Air-fuel ratio control, spark ignition engines, adaptive control, parameter estimation, GT-Power simulation

## I. INTRODUCTION

In the automotive industry, significant effort has been made to reduce emissions and improve fuel economy, hence the flexibility of engine control units (ECUs) has led to more efficient results [1]. The general solution for spark ignition (SI) engines is to convert the pollutant exhaust gases into innocuous ones by using the three-way catalytic converter (TWCC). However, the conversion efficiency of TWCCs depends crucially on the air-fuel ratio (AFR) in the combustion chamber [2]. It is well documented that the stoichiometric AFR (e.g. 14.67 for petrol) will maximize the steady-state conversion efficiency [3][4]. Moreover, the combustion of the air-fuel mixture in the chamber will deliver

This work was supported by the Marie Curie IEF Project AECE (grant FP7-PEOPLE-2013-IEF-625531) and National Natural Science Foundation of China (grant 61573174).

Jing Na is with the Faculty of Mechanical and Electrical Engineering, Kunming University of Science and Technology, Kunming, China. (Corresponding author. Email: [najing25n@163.com](mailto:najing25n@163.com)).

Anthony Siming Chen and Guido Herrmann are with the Department of Mechanical Engineering, University of Bristol, BS8 1TR, UK. (Email: [sc15280@my.bristol.ac.uk](mailto:sc15280@my.bristol.ac.uk); [G.Herrmann@bristol.ac.uk](mailto:G.Herrmann@bristol.ac.uk)).

Richard Burke and Chris Brace are with the Powertrain Vehicle Research Centre, Department of Mechanical Engineering, University of Bath, BA2 7AY, UK. (Email: [C.J.Brace@bath.ac.uk](mailto:C.J.Brace@bath.ac.uk); [R.D.Burke@bath.ac.uk](mailto:R.D.Burke@bath.ac.uk)).

optimum thermal efficiency and engine performance provided that the AFR is controlled in a narrow window near the stoichiometric value [5]. Therefore, the objective is to regulate the AFR around this stoichiometric value.

To address the AFR control problem for SI engines, the most popular approach is proportional-integral (PI) control together with an open-loop feedforward control element, based on lookup tables [6]. However, the compilation of the lookup tables is time-consuming as it requires significant calibration and tuning phases. Then, several advanced control methods have also been proposed, for example, sliding mode control was suggested to regulate the AFR at the desired value in the presence of model uncertainties and external disturbances [5, 7]. However, sliding mode controllers suffer from the chattering issue, where the oscillations may adversely affect the conversion efficiency of the TWCCs. Model predictive controllers were also designed in combination with a diagonal recurrent neural network (DRNN) [8] and using a relevance vector machine (RVM) technique [9].

To deal with parameter uncertainties, adaptive control methods have been presented for a port-injection SI engine which accounts for the effect of the trapped fuel on the intake manifold wall [3]. A simplified adaptive controller was proposed which shows both simplicity and robustness under the certain conditions [10]. However, this controller requires the in-cylinder pressure sensor, which is very expensive and generally not available in commercial cars.

The objective of this paper is to develop a simple and robust adaptive controller by using the commonly available engine sensors. We will incorporate a recently suggested novel idea for adaptive parameter estimation [11, 12] into the AFR control design. We first revisit SI engine dynamics and reformulate the AFR regulation problem into the tracking control of the fuel mass flow. Another notable idea is that the adaptive algorithm introduces a new leakage term, which guarantees the convergence of both the AFR error and the time-varying parameter estimation error. Finally, the proposed control law is compared to the generic adaptive control with gradient descent method [3] via a well-calibrated engine model and in a commercial software GT-Power.

## II. ENGINE DYNAMICS AND MODELLING

This section will introduce the main dynamics of SI engines. For AFR control, we revisit a physically based analytical engine model named ‘mean value engine model

(MVEM) [13, 14].

### A. Intake Manifold Dynamics

It has been found that the air filling dynamics of the intake manifold can be represented as an adiabatic process [13]. Hence, the pressure variation can be determined based on the ideal gas law and the conservation of mass as

$$\dot{p}_m = \frac{\kappa R}{V_m} (\dot{m}_{ai} T_a - \dot{m}_{ao} T_m + \dot{m}_{EGR} T_{EGR}) \quad (1)$$

where  $p_m$  is the intake manifold pressure,  $V_m$  is the intake manifold volume,  $\kappa$  is the ratio of specific heats ( $\kappa = 1.4$  for air),  $R$  is the ideal gas constant.  $\dot{m}_{ai}$  and  $\dot{m}_{ao}$  is the air mass flow rate into and out of the intake manifold and  $\dot{m}_{EGR}$  is the exhaust gas recirculation (EGR) mass flow rate.  $T_m$  and  $T_{EGR}$  are the intake manifold temperature and the EGR temperature, respectively.

Moreover, the air mass flow rate into the cylinders can be calculated as

$$\dot{m}_{ao} = c_m N p_m \quad (2)$$

where  $c_m = \sqrt{\frac{T_m}{T_a} \frac{V_d \eta_{vol}(N, p_m)}{120 R T_m}} > 0$ ,  $V_d$  is the engine displacement, and  $\eta_{vol}(N, p_m)$  is the volumetric efficiency which usually depends on the engine speed  $N$  and the intake manifold pressure  $p_m$ .

### B. Fuelling Dynamics

For port-injection SI engines, the fuel flow is injected at the port in the intake manifold. A considerable portion of fuel will be trapped on the manifold wall. The issue is known as the ‘wall-wetting’ phenomenon, where the deposited fuel is usually called ‘fuel film’ or ‘fuel puddles’ in the literature [3, 14, 15]. An empirical equation of the fuelling dynamics [15] is given as

$$\begin{cases} \dot{m}_f = \chi u_f + \dot{m}_{ff} \\ \tau_f \dot{m}_{ff} + \dot{m}_{ff} = (1 - \chi) u_f \end{cases} \quad (3)$$

where  $\dot{m}_f$  is the actual fuel mass flow rate into the cylinders,  $\dot{m}_{ff}$  is the mass flow rate of the fuel film deposited on the intake manifold wall,  $\chi$  represents the portion of the fuel that directly enters the cylinders as vapour while  $1 - \chi$  denotes the portion of the fuel deposited on the wall as fuel film. The value  $\tau_f$  is the fuel lag time constant, and  $u_f$  is the fuel injection command. For simplicity, (3) can be written as

$$\ddot{m}_f = -\frac{1}{\tau_f} \dot{m}_f + \chi \dot{u}_f + \frac{1}{\tau_f} u_f = -\frac{1}{\tau_f} \dot{m}_f + u_d \quad (4)$$

where  $u_d = (\chi s + 1/\kappa) u_f$  is the control input. It will be used in the following for AFR control.

The AFR can be calculated as the ratio of the air mass flow rate  $\dot{m}_{ao}$  to the fuel mass flow rate  $\dot{m}_f$  into the cylinders, which can be written as

$$AFR = \frac{\dot{m}_{ao}}{\dot{m}_f} \quad (5)$$

More commonly, the air-fuel equivalence ratio  $\lambda$  is used for engineering purpose. It is defined as

$$\lambda = \frac{AFR}{L_{th}} = \frac{\dot{m}_{ao}}{\dot{m}_f L_{th}} \quad (6)$$

where  $L_{th}$  is the stoichiometric value (i.e.  $L_{th} = 14.67$ ).

### C. Combustion Dynamics

The combustion of the air-fuel mixture generates the indicated torque  $\tau_i$ , which can be formulated as a function of the fuel mass flow rate  $\dot{m}_f$  and the engine speed  $N$ :

$$\tau_i = c_T \frac{\dot{m}_f}{N} \quad (7)$$

where  $c_T = H_u \eta_i > 0$ ,  $H_u$  is the fuel energy constant, and  $\eta_i$  is the thermal efficiency. Generally,  $\eta_i$  is a complex function of the engine speed  $N$ , the intake manifold pressure  $p_m$ , the spark advance (SA)  $\theta_{SA}$ , and the air-fuel equivalence ratio  $\lambda$  [14].

### D. Crankshaft Dynamics

The rotation of the crankshaft can be modelled by using Newton’s second law as

$$J \dot{N} = \tau_i - \tau_f - \tau_p - \tau_l \quad (8)$$

where  $J$  is the scaled moment of inertia,  $\dot{N}$  is the angular acceleration of the crankshaft,  $\tau_f$ ,  $\tau_p$ , and  $\tau_l$  are the friction torque, the pumping torque, and the load torque, respectively [16]. The above engine model will be calibrated based on experimental mapping data and employed for AFR control simulation in section 5.1.

## III. PROBLEM STATEMENT AND REFORMULATION

This section will define the AFR control problem and reformulate the AFR regulation problem into a fuel mass flow tracking problem for the sake of simplicity.

### A. Problem Statement

The control problem to be addressed is to regulate the AFR around the stoichiometric value  $L_{th} = 14.67$ , i.e. to regulate the air-fuel equivalence ratio  $\lambda$  to follow the desired value  $\lambda_d = 1$  by designing the fuel injection control input  $u_d$ .

Typically, the feedback error of an AFR controller is directly derived as

$$e_\lambda(t) = \lambda_d - \lambda(t) = \lambda_d - \frac{\dot{m}_{ao}}{\dot{m}_f L_{th}} \quad (9)$$

The measurement of  $e_\lambda$  itself is straightforward. However, the dynamics of  $\lambda(t)$  is an indirect function of most engine variables. Thus, the derivative of  $e_\lambda$  can be written as

$$\dot{e}_\lambda(t) = -\dot{\lambda}(t) = -\frac{d}{dt} \left( \frac{\dot{m}_{ao}}{\dot{m}_f L_{th}} \right). \quad (10)$$

The derivative of  $\lambda(t)$  is an indirect function of almost all the engine variables, which will complicate the control design and analysis. The complexity of the calculation of the term  $\frac{d}{dt}\left(\frac{\dot{m}_{ao}}{\dot{m}_f L_{th}}\right)$  has been shown in [3]. This can be avoided by reformulating the problem in Section 3.2. The objective is to accurately control the AFR under wide engine operating conditions and in the presence of model uncertainties, sensor noises and disturbances. In the literature, three difficulties in the AFR control have been stated: a) the engine model parameters have uncertainties and some of them such as  $c_m$  and  $c_T$  are likely to be time-varying in practice; b) the effect of the 'wall-wetting' phenomenon cannot be underestimated; c) the air mass flow rate  $\dot{m}_{ao}$  and the fuel mass flow rate  $\dot{m}_f$  are not measurable due to limited sensor configuration.

In this paper, the corresponding strategies to tackle these three difficulties above are: a) the parameter uncertainties can be handled by using adaptive control, where the time-varying parameters can be estimated using a new adaptive algorithm in Section 4.3; b) the effect of the fuel film is modelled in (3)-(4) and taken into account in the control design; c) the air mass flow rate  $\dot{m}_{ao}$  can be estimated from available engine variables  $\dot{m}_{ai}$  and  $p_m$  by using a recent idea of unknown input observer (UIO) [17], where the estimation error converges to a small compact set around zero. Then, the fuel mass flow rate  $\dot{m}_f$  can be calculated simply from (6) by using the estimated  $\dot{m}_{ao}$  and the measured  $\lambda$ .

### B. Problem Reformulation

In this paper, we reformulate the error dynamics of (9) in order to simplify the control design and to reduce the number of adaptive parameters in comparison to [3]. Considering that the control input  $u_d$  is related to the fuel mass flow rate  $\dot{m}_f$ , the regulation of  $\lambda$  can be reformulated into the tracking problem of fuel mass flow. Hence, the new feedback error can be defined as the difference between the ideal fuel mass flow rate  $\dot{m}_{fd}$  and the actual fuel mass flow rate  $\dot{m}_f$ , i.e.

$$e(t) = \dot{m}_{fd} - \dot{m}_f = \frac{\dot{m}_{ao}}{\lambda_d L_{th}} - \dot{m}_f \quad (11)$$

Clearly, the AFR can be regulated at the stoichiometric value provided that the fuel mass flow  $\dot{m}_f$  tracks the time-varying reference  $\dot{m}_{fd} = \dot{m}_{ao} / (\lambda_d L_{th})$  as [17]. Thus, the derivative of  $e(t)$  can be presented as

$$\dot{e}(t) = \frac{d}{dt}(\dot{m}_{fd} - \dot{m}_f) = \frac{\ddot{m}_{ao}}{\lambda_d L_{th}} - \ddot{m}_f \quad (12)$$

Compared to (10) where the derivative of  $\dot{m}_f$  appears in the denominator, the calculation of derivatives in (12) is much easier. In (12),  $\dot{m}_f$  can be obtained from (4) and  $\dot{m}_{ao}$  can be determined by differentiating (2) using (1), (7) - (8) as

$$\begin{aligned} \ddot{m}_{ao} = & \frac{c_m c_T}{J} \frac{\dot{m}_f p_m}{N} - \frac{c_m}{J} p_m (\tau_f + \tau_p + \tau_l) \\ & + \frac{c_m \kappa R}{V_m} N (\dot{m}_{ai} T_a - \dot{m}_{ao} T_m + \dot{m}_{EGR} T_{EGR}) \end{aligned} \quad (13)$$

Thus, the error dynamics can be given as

$$\begin{aligned} \dot{e}(t) = & \frac{c_m c_T}{\lambda_d L_{th} J} \frac{\dot{m}_f p_m}{N} - \frac{c_m}{\lambda_d L_{th} J} p_m (\tau_f + \tau_p + \tau_l) \\ & + \frac{c_m \kappa R}{\lambda_d L_{th} V_m} N (\dot{m}_{ai} T_a - \dot{m}_{ao} T_m + \dot{m}_{EGR} T_{EGR}) + \frac{1}{\tau_f} \dot{m}_f - u_d \end{aligned} \quad (14)$$

where  $u_d$  is the control input to be designed.

## IV. CONTROL DESIGN

This section will present the design and analysis of the AFR controllers.

### A. Feedback Linearization

Ideally, if all the engine parameters are exactly known, we can design the feedback linearization control law for (14) as

$$\begin{aligned} u_d = & ke(t) + \frac{1}{\tau_f} \dot{m}_f + \frac{c_m c_T}{\lambda_d L_{th} J} \frac{\dot{m}_f p_m}{N} - \frac{c_m}{\lambda_d L_{th} J} p_m (\tau_f + \tau_p + \tau_l) \\ & + \frac{c_m \kappa R}{\lambda_d L_{th} V_m} N (\dot{m}_{ai} T_a - \dot{m}_{ao} T_m + \dot{m}_{EGR} T_{EGR}) \end{aligned} \quad (15)$$

where  $k > 0$  is a feedback control gain. Then the derivative of the closed-loop error can be determined by substituting the control input (15) into (14) as

$$\dot{e}(t) = -ke(t) \quad (16)$$

**Proposition 1:** Considering the SI engine system (1)-(8) with the control input (15), then the error  $e(t)$  will exponentially converge to zero, i.e. the AFR can be regulated at the stoichiometric value.

**Proof:** A Lyapunov function can be chosen as  $V(t) = \frac{1}{2} e^2(t)$ , then it is obvious from (16) that its time derivative can be determined as

$$\dot{V}(t) = e(t)\dot{e}(t) = -ke^2(t) \le 0 \quad (17)$$

Since  $V(t)$  is positive definite, it is clear that  $V(t), e(t) \to 0$  exponentially for  $t \to \infty$ , i.e.  $\lambda \to \lambda_d$  as  $t \to \infty$ .

However, the assumption (i.e. all dynamics in (15) are exactly known) for this feedback linearization is stringent as, in practice, not all the engine parameters can be exactly obtained. Thus, we will present two adaptive AFR control laws, where unknown parameters will be online updated.

### B. Adaptive Control with Gradient Method

Considering the parameters  $c_m$  and  $c_T$  are likely to be time-varying in practice, we will use an adaptive update law to online update the unknown parameters. For this purpose, we first rewrite (13) into a compact parameterized expression as

$$\ddot{m}_{ao} = \begin{bmatrix} \dot{m}_f p_m / N \\ p_m (\tau_f + \tau_p + \tau_l) \\ N (\dot{m}_{ai} T_a - \dot{m}_{ao} T_m + \dot{m}_{EGR} T_{EGR}) \end{bmatrix}^T \begin{bmatrix} c_m(t) c_T(t) / J \\ -c_m(t) / J \\ c_m(t) \kappa R / V_m \end{bmatrix} = \Phi \Theta(t) \quad (18)$$

where  $\Phi$  is the known regressor vector, and  $\Theta(t)$  is the unknown time-varying parameter vector. Clearly, there are only three parameters to be online updated.

Then, the control law (15) can be modified by using the estimated parameters as

$$u_d = ke(t) + \frac{1}{\tau_f} \dot{m}_f + \frac{1}{\lambda_d L_{th}} \Phi \hat{\Theta}(t) \quad (19)$$

where  $k > 0$  is a feedback control gain and  $\hat{\Theta}(t)$  is the estimate of  $\Theta(t)$ . The adaptive update law is given by

$$\dot{\hat{\Theta}}(t) = \Gamma \left[ \frac{1}{\lambda_d L_{th}} \Phi^T e(t) - \sigma \hat{\Theta}(t) \right] \quad (20)$$

where  $\Gamma = \text{diag}[\gamma_1 \ \gamma_2 \ \gamma_3] > 0$  is a constant gain and  $\sigma$  is a constant forgetting factor. Then the derivative of the closed-loop error dynamics can be determined by substituting the control input (19) into (14) as

$$\dot{e}(t) = -ke(t) + \frac{1}{\lambda_d L_{th}} \Phi \tilde{\Theta}(t) \quad (21)$$

where  $\tilde{\Theta}(t) = \Theta(t) - \hat{\Theta}(t)$  is the parameter estimation error.

**Assumption 1:** The unknown time-varying parameter vector  $\Theta(t)$  and its time derivative are bounded by  $\|\Theta(t)\| \le \bar{h}_m$  and  $\|\dot{\Theta}(t)\| \le \bar{h}_d$  for constants  $\bar{h}_m, \bar{h}_d > 0$ .

**Proposition 2:** Considering the SI engine system (1)-(8) with the control input (19) and the adaptive law (20), the error  $e(t)$  will exponentially converge to a compact set defined by

$$|e(t)| \le \sqrt{\frac{m \bar{h}_d^2 / \lambda_{\min}^2(\Gamma) + m \sigma^2 \bar{h}_m^2}{\min\{2k, 2(\sigma-1/m) / \lambda_{\max}(\Gamma^{-1})\}}}, \text{ whose size depends}$$

on the bounds of  $\|\Theta(t)\| \le \bar{h}_m$  and  $\|\dot{\Theta}(t)\| \le \bar{h}_d$ . Thus, the AFR is regulated around the stoichiometric value.

**Proof:** We choose a Lyapunov candidate function as

$$V_1(t) = V(t) + \frac{1}{2} \tilde{\Theta}^T(t) \Gamma^{-1} \tilde{\Theta}(t) \quad (22)$$

The time derivative of  $V_1$  can be calculated using (20) and (21) together with  $\dot{\tilde{\Theta}}(t) = \dot{\Theta}(t) - \dot{\hat{\Theta}}(t)$  as

$$\begin{aligned} \dot{V}_1(t) &= e(t) \dot{e}(t) + \tilde{\Theta}^T(t) \Gamma^{-1} \dot{\tilde{\Theta}}(t) = e(t) \left[ -ke(t) + \frac{1}{\lambda_d L_{th}} \Phi \tilde{\Theta}(t) \right] \\ &+ \tilde{\Theta}^T(t) \Gamma^{-1} \dot{\Theta}(t) - \tilde{\Theta}^T(t) \left[ \frac{1}{\lambda_d L_{th}} \Phi^T e(t) - \sigma \hat{\Theta}(t) \right] \\ &= -ke^2(t) + \tilde{\Theta}^T(t) \Gamma^{-1} \dot{\Theta}(t) + \sigma \tilde{\Theta}^T(t) \Theta(t) - \sigma \tilde{\Theta}^T(t) \hat{\Theta}(t) \end{aligned} \quad (23)$$

We apply Young's inequality  $ab \le \alpha^2 / 2m + mb^2 / 2$ , ( $m > 0$ ), then

$$\begin{aligned} \dot{V}_1(t) &\le -ke^2(t) - (\sigma - 1/m) \|\tilde{\Theta}(t)\|^2 + \frac{m \bar{h}_d^2}{2 \lambda_{\min}^2(\Gamma)} + \frac{m \sigma^2 \bar{h}_m^2}{2} \\ &\le -\alpha V_1 + \beta \end{aligned} \quad (24)$$

where the constants  $\alpha = \min\{2k, 2(\sigma-1/m) / \lambda_{\max}(\Gamma^{-1})\}$  and  $\beta = m \bar{h}_d^2 / 2 \lambda_{\min}^2(\Gamma) + m \sigma^2 \bar{h}_m^2 / 2$  are positive for any  $m \ge \sigma$ . According to Lyapunov's theorem,  $V_1(t)$  is uniformly ultimately bounded, i.e.  $V_1(t) \le [V_1(0) - \beta / \alpha] e^{-\alpha t} + \beta / \alpha$ . This implies that the control error  $e(t)$  will exponentially converge to a small compact set defined by  $|e(t)| \le \sqrt{2\beta / \alpha} = \sqrt{\frac{m \bar{h}_d^2 / \lambda_{\min}^2(\Gamma) + m \sigma^2 \bar{h}_m^2}{\min\{2k, 2(\sigma-1/m) / \lambda_{\max}(\Gamma^{-1})\}}}$  as  $t \to \infty$ .

With the adaptive law (20), the estimation of time-varying parameters (i.e.  $\dot{\Theta}(t) \neq 0$ ) cannot be achieved [18]. Moreover, the forgetting factor introduces an inherent estimation and tracking control error due to the magnitude of  $\Theta(t)$ . This drives the motivation of the following new adaptive law, which can achieve time-varying parameter estimation.

### C. Adaptive Control with Parameter Estimation

This section will present a new adaptive law for estimating time-varying parameters by further exploiting our previous work [11, 12]. Thus, we define filtered variables as  $\dot{m}_{aof}$ ,  $\Phi_f$  of  $\dot{m}_{ao}$ ,  $\Phi$  as

$$\begin{cases} \zeta \dot{m}_{aof} + \dot{m}_{aof} = \dot{m}_{ao}, & \dot{m}_{aof}(0) = 0 \\ \zeta \Phi_f + \Phi_f = \Phi, & \Phi_f(0) = 0 \end{cases} \quad (25)$$

where  $\zeta > 0$  is the filter parameter. The filter operation (25) is equivalent to adding a low-pass filter  $1/(\zeta s + 1)$  on the both sides of (18) as

$$\frac{s}{\zeta s + 1} [\dot{m}_{ao}] = \frac{1}{\zeta s + 1} [\Phi \Theta] \quad (26)$$

Considering (25) and the Swapping Lemma [18], then (26) can be written as

$$\frac{\dot{m}_{ao} - \dot{m}_{aof}}{\zeta} = \Phi_f \Theta - \frac{\zeta}{\zeta s + 1} [\Phi_f \dot{\Theta}] \quad (27)$$

It is obvious that  $\Phi$  is bounded within a sufficiently large bounded set related to the engine operating region; then,  $\Phi_f$  is bounded, i.e.  $\|\Phi_f\| \le \bar{\lambda}$  for a constant  $\bar{\lambda} > 0$ . Since  $\|\dot{\Theta}(t)\| \le \bar{h}_d$  holds according to Assumption 1, the term  $\psi = \frac{\zeta}{\zeta s + 1} [\Phi_f \dot{\Theta}]$  is also bounded, i.e.  $\|\psi\| \le \mu$  for a constant  $\mu > 0$  [11].

Then we define two auxiliary variables  $P$  and  $Q$  as

$$\begin{cases} \dot{P} = -(\zeta P + \Phi_f^T \Phi_f), & P(0) = 0 \\ \dot{Q} = -(\zeta Q + \Phi_f^T [(\dot{m}_{ao} - \dot{m}_{aof}) / \zeta]), & Q(0) = 0 \end{cases} \quad (28)$$

where  $\ell > 0$  is a design parameter.

Denote a new leakage term  $W(t)$  to be used as

$$W(t) = P\hat{\Theta}(t) - Q \quad (29)$$

Now we can design the same control input as (19) but with a new adaptive law given by

$$\dot{\hat{\Theta}}(t) = \Gamma \left[ \frac{1}{\lambda_d L_{th}} \Phi^T e(t) - \sigma W(t) \right] \quad (30)$$

where  $\sigma > 0$  is a design constant. The derivative of the closed-loop error is the same as (21)

From (27) and (28), it can be found that

$$W(t) = -P\tilde{\Theta}(t) + \Omega \quad (31)$$

where  $\Omega = \int_0^t e^{-\ell(t-r)} \Phi_f^T(r) \psi(r) dr$  is a bounded residual error, i.e.  $\|\Omega\| \le \|\Phi_f\| \|\psi\| / \ell = \bar{\lambda}_f \mu / \ell$ . Hence,  $W(t)$  contains the information of the parameter estimation error  $\tilde{\Theta}(t)$ , in particular for  $\dot{\hat{\Theta}}(t) = 0$ .

**Lemma 1** [11, 12]: If the regressor  $\Phi$  satisfies Persistent Excitation (PE) condition, i.e.  $\int_t^{t+\tau} \Phi^T(r) \Phi(r) dr \ge \varepsilon I$ ,  $\forall t \ge 0$  for  $\tau > 0$ ,  $\varepsilon > 0$ , then the matrix  $P$  in (28) is positive definite, i.e.  $\lambda_{\min}(P) > \sigma_1 > 0$ .

**Proof:** Please refer to [11] for detailed proof.

**Proposition 3:** Considering the SI engine system (1)-(8) with the control input (19) and adaptive law (30) under Assumption 1, then  $e(t)$ ,  $\tilde{\Theta}(t)$  will exponentially converge to the compact sets  $|e(t)| \le \sqrt{\frac{\sigma m \bar{\lambda}^2 \mu^2 / \ell^2 + m \bar{h}_d^2 / \lambda_{\min}^2(\Gamma)}{\min\{2k, 2(\sigma\sigma_1 - 1/m) / \lambda_{\max}(\Gamma^{-1})\}}}$

and  $\|\tilde{\Theta}(t)\| \le \sqrt{\frac{[\sigma m \bar{\lambda}^2 \mu^2 / \ell^2 + m \bar{h}_d^2 / \lambda_{\min}^2(\Gamma)] \lambda_{\max}(\Gamma^{-1})}{\lambda_{\min}(\Gamma^{-1}) \min\{2k, 2(\sigma\sigma_1 - 1/m) / \lambda_{\max}(\Gamma^{-1})\}}}$ . Thus, the AFR can be regulated around the stoichiometric value.

**Proof:** We select the same Lyapunov function  $V_1(t)$  as (22). Its time derivative can be calculated using (21) and (30) as

$$\begin{aligned} \dot{V}_1(t) &= e(t) \left[ -ke(t) + \frac{1}{\lambda_d L_{th}} \Phi \tilde{\Theta}(t) \right] + \tilde{\Theta}^T(t) \Gamma^{-1} \dot{\hat{\Theta}}(t) \\ &\quad - \tilde{\Theta}^T(t) \left[ \frac{1}{\lambda_d L_{th}} \Phi^T e(t) - \sigma W(t) \right] \\ &= -ke^2(t) + \tilde{\Theta}^T(t) \Gamma^{-1} \dot{\hat{\Theta}}(t) - \sigma \tilde{\Theta}^T(t) P \tilde{\Theta}(t) + \sigma \tilde{\Theta}^T(t) \Omega \end{aligned} \quad (32)$$

By applying Young's inequality, we have

$$\begin{aligned} \dot{V}_1(t) &\le -ke^2(t) - (\sigma\sigma_1 - 1/m) \|\tilde{\Theta}(t)\|^2 + \frac{m\sigma^2 \bar{\lambda}^2 \mu^2}{2\ell^2} + \frac{m \bar{h}_d^2}{2\lambda_{\min}^2(\Gamma)} \\ &\le -\alpha_1 V_1(t) + \beta_1 \end{aligned} \quad (33)$$

where the constants  $\alpha_1 = \min\{2k, 2(\sigma\sigma_1 - 1/m) / \lambda_{\max}(\Gamma^{-1})\}$  and  $\beta_1 = \sigma m \bar{\lambda}^2 \mu^2 / 2\ell^2 + m \bar{h}_d^2 / 2\lambda_{\min}^2(\Gamma)$  are positive for

$m \ge 1 / \sigma\sigma_1$ . According to Lyapunov's theorem,  $V_1(t)$  follows  $V_1(t) \le [V_1(0) - \beta_1 / \alpha_1] e^{-\alpha_1 t} + \beta_1 / \alpha_1$ , which is uniformly ultimately bounded. Moreover, this implies that the error  $e(t)$  and the parameter estimation error  $\tilde{\Theta}(t)$  will exponentially converge to the compact sets defined in Proposition 3 as  $t \to \infty$ , respectively.

## V. SIMULATION AND VALIDATION

This section will first present simulation results based on an SI engine model in Matlab/Simulink. Then we also validate this new adaptive control via a commercial engine simulation software, GT-Power.

### A. Simulations

The SI engine model is built based on the MVEM in Matlab/Simulink, where the model parameters are calibrated based on experimental data sets. The AFR controllers (19) with two different adaptive laws (20) and (30) are compared. The parameters are set as  $k_1 = 100$ ,  $\Gamma = \text{diag}[1000 \ 10 \ 10]$ ,  $\ell = 1$ ,  $\zeta = 0.001$ , and  $\sigma = 1$ . The simulation results are presented in Fig. 1. It is found that both adaptive controllers can regulate the AFR around the stoichiometric value  $L_{th} = 14.67$ , where the controller with the new adaptive law (30) has better transient and steady-state performance than that with the gradient descent adaptive law (20).

![Figure 1(a): Response AFR control. A line graph showing Air-Fuel Ratio (AFR) over time t [s] from 0 to 40. The AFR is centered around 14.67. Three curves are shown: Reference (red dashed line), Proposed (blue solid line), and Gradient (black dashed line). The Proposed controller shows a faster and smoother convergence to the reference value compared to the Gradient controller.](046dbe0c717e69d73120adc7d2089356_img.jpg)

Figure 1(a): Response AFR control. A line graph showing Air-Fuel Ratio (AFR) over time t [s] from 0 to 40. The AFR is centered around 14.67. Three curves are shown: Reference (red dashed line), Proposed (blue solid line), and Gradient (black dashed line). The Proposed controller shows a faster and smoother convergence to the reference value compared to the Gradient controller.

(a) Response AFR control

![Figure 1(b): Profiles of estimated parameters. Three subplots showing estimated parameters e1, e2, and e3 over time t [s] from 0 to 40. Each subplot compares the Reference (red dashed line) with the Proposed (blue solid line) and Gradient (black dashed line) controllers. The Proposed controller tracks the reference parameters more accurately and with less noise than the Gradient controller.](715e9a41b836f84233baee876b6d060b_img.jpg)

Figure 1(b): Profiles of estimated parameters. Three subplots showing estimated parameters e1, e2, and e3 over time t [s] from 0 to 40. Each subplot compares the Reference (red dashed line) with the Proposed (blue solid line) and Gradient (black dashed line) controllers. The Proposed controller tracks the reference parameters more accurately and with less noise than the Gradient controller.

(b) Profiles of estimated parameters.

Fig. 1. Simulation results based on MVEM

More importantly, it is obvious that the adaptive law (30) can track the time-varying parameters, which is superior over (20). This is due to the leakage term  $W(t)$  used in (30) which contains the information of the parameter errors.

### B. GT-Power Validation

The proposed adaptive AFR controllers are also tested in a more realistic engine model built in an industrial-grade engine simulation software GT-Power. The model built in GT-Power is a commercial car-used turbocharged 2.0 litre four-cylinder SI engine, which is calibrated based on the geometric measurement and practical engine tests. The proposed AFR controllers (19) with adaptive law (30) is implemented in GT-Power.

![Figure 2: Validation results based on GT-Power engine model. (a) Response AFR control: A plot of Air-Fuel Equivalence Ratio vs time t [s] showing the reference (red dashed line), proposed controller (blue solid line), and gradient descent (blue dashed line). (b) Profiles of estimated parameters: Two plots showing the estimated parameters θ1 and θ3 vs time t [s]. The y-axis for θ3 is scaled by 10^-4. Both plots show the proposed controller (blue solid line) and gradient descent (blue dashed line) compared to the reference (red dashed line).](55d2bfe1c3d04e86df8d7a104d802172_img.jpg)

Figure 2: Validation results based on GT-Power engine model. (a) Response AFR control: A plot of Air-Fuel Equivalence Ratio vs time t [s] showing the reference (red dashed line), proposed controller (blue solid line), and gradient descent (blue dashed line). (b) Profiles of estimated parameters: Two plots showing the estimated parameters θ1 and θ3 vs time t [s]. The y-axis for θ3 is scaled by 10^-4. Both plots show the proposed controller (blue solid line) and gradient descent (blue dashed line) compared to the reference (red dashed line).

Fig. 2. Validation results based on GT-Power engine model.

The AFR controllers (19) with two different adaptive laws (20) and (30) are implemented and compared in GT-Power. The parameters of the controllers are set as  $k_1 = 10$ ,  $\Gamma = \text{diag}[10 \ 10 \ 10]$ ,  $\ell = 1$ ,  $\zeta = 0.001$ , and  $\sigma = 0.1$ . Fig. 2 presents the validation results of the AFR response and the profiles of the estimated parameters. It is found that the AFR is correctly controlled with a 7% error boundary while the time-varying parameters are estimated. It can be verified again that the controller with the proposed adaptive law (30) obtains better transient performance than that with the gradient descent adaptive law (20), where the transient errors arise from the engine speed changes at the time instants 5s, 10s, 15s, and 20s. Moreover, although the actual parameters are not known in this case, we can speculate that the proposed method (30) tracks the unknown parameters better than (20) since the parameters are inherently time-varying.

## VI. CONCLUSIONS

This paper proposes an improved and simplified adaptive AFR controller for SI engines, where the involved time-varying parameters can be estimated by using a new adaptive law. The AFR regulation problem is first reformulated into the tracking control of the fuel mass flow, which simplifies the control design and reduces the number of parameters to be online updated. A new leakage term including the estimation error is derived and incorporated into

the adaptive law, such that both the AFR error and the parameter error can achieve exponential convergence, simultaneously. Numerical simulations based on the MVEM in Matlab and validation in the realistic engine built in an engine simulation software GT-Power are carried out to show that the AFR can be regulated around the stoichiometric value and the time-varying parameters are fast tracked under wide engine operation regimes. Future research will focus on the implementation of the proposed adaptive AFR controller on practical engines.

## REFERENCES

- [1] Y. Yasui, J. Iwamoto, and H. Oghara, "Exhaust gas purifying apparatus and method for internal combustion engine, and engine control unit," Google Patents, 2007.
- [2] Y. Yildiz, A. M. Annaswamy, D. Yanakiev, and I. Kolmanovsky, "Spark ignition engine fuel-to-air ratio control: An adaptive control approach," *Control Engineering Practice*, vol. 18, pp. 1369-1378, 2010.
- [3] X. Jiao, J. Zhang, T. Shen, and J. Kako, "Adaptive air - fuel ratio control scheme and its experimental validations for port - injected spark ignition engines," *International Journal of Adaptive Control and Signal processing*, vol. 29, pp. 41-63, 2015.
- [4] A. Ghaffari, A. H. Shamekhi, A. Saki, and E. Kamrani, "Adaptive fuzzy control for air-fuel ratio of automobile spark ignition engine," *World Academy of Science, Engineering and Technology*, vol. 48, pp. 284-292, 2008.
- [5] B. Ebrahimi, R. Tafreshi, J. Mohammadpour, M. Franchek, K. Grigoriadis, and H. Masudi, "Second-Order Sliding Mode Strategy for Air-Fuel Ratio Control of Lean-Burn SI Engines," *Control Systems Technology, IEEE Transactions on*, vol. 22, pp. 1374-1384, 2014.
- [6] B. Ebrahimi, R. Tafreshi, H. Masudi, M. Franchek, J. Mohammadpour, and K. Grigoriadis, "A parameter-varying filtered PID strategy for air-fuel ratio control of spark ignition engines," *Control Engineering Practice*, vol. 20, pp. 805-815, 2012.
- [7] J. Pieper and R. Mehrotra, "Air/fuel ratio control using sliding mode methods," in *American Control Conference, 1999. Proceedings of the 1999*, 1999, pp. 1027-1031.
- [8] Y. J. Zhai, D. W. Yu, H. Y. Guo, and D. L. Yu, "Robust air/fuel ratio control with adaptive DRNN model and AD tuning," *Engineering Applications of Artificial Intelligence*, vol. 23, pp. 283-289, 2010.
- [9] H. C. Wong, P. K. Wong, and C. M. Vong, "Model predictive engine air-ratio control using online sequential relevance vector machine," *Journal of Control Science and Engineering*, vol. 2012, p. 2, 2012.
- [10] C. Khajorntraiet and K. Ito, "Simple adaptive air-fuel ratio control of a port injection SI engine with a cylinder pressure sensor," *Control Theory and Technology*, vol. 13, pp. 141-150, 2015.
- [11] J. Na, M. N. Mahyuddin, G. Herrmann, X. Ren, and P. Barber, "Robust adaptive finite-time parameter estimation and control for robotic systems," *International Journal of Robust and Nonlinear Control*, vol. 25, pp. 3045-3071, 2015.
- [12] J. Na, G. Herrmann, and R. Burke, "Adaptive input and parameter estimation with application to engine torque estimation," *Adaptive input and parameter estimation with application to engine torque estimation*, 2015.
- [13] E. Hendricks, A. Chevalier, M. Jensen, and S. C. Sorenson, "Modelling of the Manifold Filling Dynamics," *SAE Technical Paper*, 1996.
- [14] E. Hendricks, "A generic mean value engine model for spark ignition engines," in *Proceedings of the 41st Simulation Conference, Sims 2000*, 2000.
- [15] E. W. Curtis, C. F. Aquino, D. K. Trumpy, and G. C. Davis, "A new port and cylinder wall wetting model to predict transient air/fuel excursions in a port fuel injected engine," *SAE Technical Paper 0148-7191*, 1996.
- [16] R. Rajamani, *Vehicle dynamics and control*: Springer Science & Business Media, 2011.
- [17] J. Na, G. Herrmann, C. Rames, R. Burke, and C. Brace, "Air-Fuel-Ratio Control of Engine System with Unknown Input Observer" in *2016 UKACC 11th International Conference on Control*, 2016.
- [18] P. A. Ioannou and J. Sun, *Robust adaptive control*: Courier Corporation, 2012.