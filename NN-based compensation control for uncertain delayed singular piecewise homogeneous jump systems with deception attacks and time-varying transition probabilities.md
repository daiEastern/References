

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

Contents lists available at ScienceDirect

###### Communications in Nonlinear Science and Numerical Simulation

journal homepage: [www.elsevier.com/locate/cnsns](http://www.elsevier.com/locate/cnsns)![Cover image of the journal Communications in Nonlinear Science and Numerical Simulation](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the journal Communications in Nonlinear Science and Numerical Simulation

###### Research paper

# NN-based compensation control for uncertain delayed singular piecewise homogeneous jump systems with deception attacks and time-varying transition probabilities

![Check for updates button](6ed175c791b5e156d9c98a8dbcc3318c_img.jpg)

Check for updates button

Yanran Fu<sup>a</sup>, Guangming Zhuang<sup>a</sup> ![ORCID icon](faf942dc3e59ce8eb64b4ac481eca7e0_img.jpg)\*, Jun-e Feng<sup>b</sup>, Yanqian Wang<sup>c</sup><sup>a</sup> School of Mathematical Sciences, Liaocheng University, Liaocheng Shandong 252059, PR China<sup>b</sup> School of Mathematics, Shandong University, Jinan Shandong 250100, PR China<sup>c</sup> School of Information and Control Engineering, Qingdao University of Technology, Qingdao Shandong 266520, PR China

##### ARTICLE INFO

##### Keywords:

Singular Markov jump systems  
Event-triggered mechanism  
Deception attacks  
Compensation feedback controller  
Time-varying transition probabilities

## ABSTRACT

This work investigates neural network (NN)-based compensation control for uncertain delayed discrete singular piecewise homogeneous Markov jump systems (PHMJSs) under deception attacks. Considering the unmeasurable system states and limited network bandwidth, the states of the discrete singular PHMJS are estimated via utilizing a state observer and communication resources are saved through an improved event-triggered mechanism (ETM). For Markov chains, time-varying transition probabilities (TPs) resulting from environmental changes and external disturbances are considered to be piecewise homogeneous, whose stochastic variations are regulated by a higher-level transition probability (HTP) matrix. Moreover, in order to alleviate the adverse impact arising from deception attacks over the controller-actuator transmission channel, the NN technique is employed to approximate malicious attacks. Then, an event-triggered compensation feedback controller based on the reconstructed deception attacks is devised to compensate for the negative effect of deception attacks on systems. By taking advantage of singular value decomposition technique and double-mode-dependent Lyapunov-Krasovskii (L-K) functional, fresh conditions of the regularity, causality and boundedness in probability for discrete singular PHMJSs are obtained under the framework of linear matrix inequalities (LMIs). Finally, DC motor is provided to verify the feasibility of the proposed NN and ETM-based compensation control approach.

## 1. Introduction

Singular systems, often called descriptor systems, semistate systems or degenerate systems, etc., are comprised of difference (or differential) equations and algebraic equations that respectively depict the dynamic and static characteristics of given systems [1,2]. From this particular perspective, singular systems offer more concrete and vivid portrayals of the operational processes within physical systems compared to normal systems [3,4]. Considering their vital theoretical contributions and practical relevance, singular systems have achieved outstanding success in diverse applications, including chemical processes, power systems, economic systems, and biological systems, etc., [5,6]. However, studying singular systems is more challenging because it requires considering not only stability, but also regularity and impulse-freeness (for continuous systems) or causality (for discrete systems) so as to successfully complete the physical implementation [7].

\* Corresponding author.

E-mail address: [zgmtsg@126.com](mailto:zgmtsg@126.com) (G. Zhuang).<https://doi.org/10.1016/j.cnsns.2024.108573>

Received 8 August 2024; Received in revised form 13 November 2024; Accepted 24 December 2024

Available online 1 January 2025

1007-5704/© 2025 Elsevier B.V. All rights are reserved, including those for text and data mining, AI training, and similar technologies.

In addition, Markov jump systems (MJJs) have garnered widespread interest for significant application potential and robust modeling capabilities in various domains like biomedicine, economics and aerospace industry, among others [8,9]. Upon abrupt changes in the structure of singular systems, the hybrid systems are typically characterized as singular MJJs [10]. Meanwhile, with rapid development of digital computer technology and the advent of the networked era, the system performance and control methods pertaining to discrete singular MJJs have garnered significant attention [11,12]. It is worth noting that transition probabilities (TPs) of the Markov chain act as a critical factor in determining the behavior and performance of discrete singular MJJs [13,14].

Certainly, in real-world systems, it is imperative to recognize that the characteristic of TPs is inherently time-varying, which underscores the importance of considering the time-varying nature of TPs in real-world applications to ensure accurate modeling and prediction of system behaviors [15]. For instance, in a vertical take-off landing helicopter system, the probabilities of transitioning between various airspeeds are not static and they fluctuate in response to changes in the external environment, such as wind speed and turbulence [8]. To simplify the complexity of time-varying TPs of Markov chains, [14] postulated that TPs changed across time yet remained constant within each interval, which can be aptly modeled with a higher-level Markov chain. Besides, Markov processes whose TPs vary but remain constant within each interval are called piecewise homogeneous Markov processes (PHMPs) [16]. Because PHMPs describe the dynamic changes of systems more accurately, they have a wide range of applications in areas such as helicopter systems, economics, the Internets and so on [17].

Furthermore, cyber-physical systems (CPSs) have received widespread attention due to their strong ability to realize massive information acquisition and smart control by cognition, communication and control in recent years [18,19]. CPSs are large systems with intricate structures that integrate control, communication and computing technologies [20,21]. The utilization of communication networks may introduce security vulnerabilities which make CPSs susceptible to different types of malicious attacks [22,23]. Representing a peculiar category of CPSs, networked singular Markov jump systems are more susceptible to cyber attackers due to the complexity and sudden changes in system structures [24].

Generally speaking, cyber attacks are divided into three main kinds: DoS attacks, replay attacks, and deception attacks [25,26]. Different types of attacks damage or weaken the security and stability of the plants to different degrees [27,28]. Thus, devising appropriate control schemes to make sure that the plants maintain their performance in the face of different types of attacks is necessary [29,30]. Among the various threats to communication networks, deception attacks stand out as a major source of danger to the transmission of control signals [31,32]. In particular, adversaries may alter the control signals that the actuators receive, which can lead to deterioration of system performance or even instability [33,34]. However, researches on control for networked discrete singular Markov systems are relatively scarce. Hence, designing effective control schemes to stabilize discrete singular Markov jump systems against deception attacks is very necessary and important under the networked environment.

In an effort to reduce the load on communication networks, how to improve resource utilization has arisen as a critical design challenge. The application of event-triggered mechanism (ETM) in network systems can significantly reduce network transmission costs [35,36]. In comparison to traditional time-triggered mechanisms, ETM transmits data only when specific criteria are satisfied, thereby effectually alleviating communication burden [37,38]. A special event triggered strategy known as the dynamic ETM can further reduce communication expenditures [39]. Triggering conditions can be flexibly adjusted according to the system states, which allows the considered system to respond more intelligently to different situations [40].

It is worth noting that some existing results consider deception attacks to be bounded and estimate them using bounded functions which are difficult to measure [32,41]. Therefore, when the controller-actuator transmission channel is under deception attacks, how to accurately reconstruct attacks and design an effective compensation feedback controller to mitigate the impact of malicious attacks on discrete singular MJJs becomes a challenging topic for discussion. Furthermore, TPs are often presumed as time-invariant in existing literature, whereas TPs are often time-varying in reality [11,12]. When considering time-varying TPs in discrete singular MJJs, how to construct a Lyapunov-Krasovskii (L-K) functional that captures two kinds of Markov modes and time-varying transition probability information and how to design a mode-dependent dynamic ETM that conserves communication resources are pivotal problems that need to be addressed in this paper.

Motivated by the above analyses, this work will focus on studying the problem of NN and ETM-based compensation control for uncertain delayed discrete singular PHMJJs under deception attacks. In order to estimate unmeasured states of the system and conserve communication resources, a state observer and an improved ETM will be introduced. Then, a NN technique will be used to approximate deception attacks and an event-triggered compensation feedback controller will be designed to mitigate the impact of malicious attacks. By constructing a double-mode-dependent L-K functional and exploiting singular value decomposition technique, fresh conditions will be derived for the regularity, causality and boundedness in probability of the closed-loop discrete singular PHMJJs under the framework of linear matrix inequalities (LMIs). Lastly, DC motor model will be provided to demonstrate the feasibility of the proposed NN and ETM-based compensation control method.

The main contributions of this paper are listed as follows:

(1) The neural network technology with powerful nonlinear modeling capability is utilized to precisely reconstruct deception attacks, freeing the considered deception attacks from the bounded conditions and achieving the expected approximation accuracy for the estimation of deception attacks.

(2) By devising a compensation term based on the reconstructed deception attack, an improved observer-based dynamic event-triggered compensation feedback controller is designed to mitigate the adverse effect of deception attacks on discrete singular PHMJJs, and the mode-dependent dynamic ETM proposed in this paper can effectually save communication resources.

(3) By introducing two Markov chains, a double-mode-dependent L-K functional is established, which can not only capture two kinds of Markov modes and time-varying transition probabilities information to better characterize the dynamic behaviors of

![Figure 1: Framework of discrete singular PHMJSs under deception attacks. The diagram shows a control loop. A 'Discrete singular PHMJSs' block receives input from an 'Actuator' and sends output to a 'Sensor'. The 'Sensor' produces measurement output 'y(k)'. An 'Observer' block takes 'y(k)' and control input 'u_f(k)' to produce state estimate 'x-hat(k)'. An 'Event Generator' block takes 'x-hat(k)' and produces a signal to the 'Controller'. The 'Controller' produces control input 'u(k)'. The 'Actuator' produces control input 'u_f(k)'. A 'Network' block is shown between the 'Controller' and 'Actuator', with 'Deception Attacks' (represented by a hacker icon and red lightning bolts) shown attacking the 'Network' channel.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

Figure 1: Framework of discrete singular PHMJSs under deception attacks. The diagram shows a control loop. A 'Discrete singular PHMJSs' block receives input from an 'Actuator' and sends output to a 'Sensor'. The 'Sensor' produces measurement output 'y(k)'. An 'Observer' block takes 'y(k)' and control input 'u\_f(k)' to produce state estimate 'x-hat(k)'. An 'Event Generator' block takes 'x-hat(k)' and produces a signal to the 'Controller'. The 'Controller' produces control input 'u(k)'. The 'Actuator' produces control input 'u\_f(k)'. A 'Network' block is shown between the 'Controller' and 'Actuator', with 'Deception Attacks' (represented by a hacker icon and red lightning bolts) shown attacking the 'Network' channel.

Fig. 1. Framework of discrete singular PHMJSs under deception attacks.

discrete singular PHMJSs, but also contribute to obtain strict LMI conditions of the boundedness in probability and realize the desired compensation control performance based on singular value decomposition technique.

**Notations.**  $\mathbb{R}^n$  represents the  $n$ -dimensional Euclidean space.  $\lambda_{\max}(\cdot)$  and  $\lambda_{\min}(\cdot)$  mean the maximum and minimum eigenvalues of the corresponding matrix, respectively.  $\mathbb{E}\{\cdot\}$  stands for the mathematical expectation.  $\text{ones}(m, n)$  means a  $m \times n$  matrix with all elements being 1.

## 2. Problem formulation

The framework of discrete singular piecewise homogeneous Markov jump systems (discrete singular PHMJSs), taking into account deception attacks, dynamic ETM and observer simultaneously, is illustrated in Fig. 1, where controller-actuator channel is susceptible to deception attacks.

### 2.1. System descriptions

Consider the following formulated discrete singular PHMJSs:

$$\begin{cases} Ex(k+1) = (A(\delta_k) + \Delta A(\delta_k))x(k) + (A_d(\delta_k) + \Delta A_d(\delta_k))x(k - d(k)) + B(\delta_k)u_f(k), \\ y(k) = C(\delta_k)x(k), \\ x(k) = \eta(k), \quad k = -d_2, -d_2 + 1, \dots, 0, \end{cases} \quad (1)$$

where the system state, initial vector function, control input, measurement output are defined by  $x(k) \in \mathbb{R}^n$ ,  $\eta(k) \in \mathbb{R}^n$ ,  $u_f(k) \in \mathbb{R}^m$ , and  $y(k) \in \mathbb{R}^p$ , separately. Time-varying delay  $d(k)$  meets  $0 \le d_1 \le d(k) \le d_2$ . Matrix  $C(\delta_k)$  is full row rank.  $E$  is singular and  $\text{rank}(E) = r < n$ .

$\{\delta_k\}$  stands for a discrete-time Markov chain with  $\delta_k \in \Pi = \{1, 2, \dots, N\}$ . Transition probabilities are represented as  $\Pr\{\delta_{k+1} = j | \delta_k = i\} = \pi_{ij}^{k+1}$ , where  $\pi_{ij}^{k+1} \ge 0$ ,  $\sum_{j=1}^N \pi_{ij}^{k+1} = 1$ ,  $i, j \in \Pi$ . Similarly,  $\{\varrho_k\}$  is a higher-level homogeneous Markov chain with  $\varrho_k \in \Sigma = \{1, 2, \dots, M\}$ . The higher-level transition probabilities are denoted as  $\Pr\{\varrho_{k+1} = n | \varrho_k = m\} = q_{mn}$ , where  $q_{mn} \ge 0$ ,  $\sum_{n=1}^M q_{mn} = 1$ ,  $m, n \in \Sigma$  [8,14]. For  $\delta_k = i$ ,  $i \in \Pi$ ,  $A(\delta_k)$ ,  $A_d(\delta_k)$ ,  $B(\delta_k)$ ,  $C(\delta_k)$  are marked with  $A_i$ ,  $A_{di}$ ,  $B_i$ ,  $C_i$  for brevity.

**Condition 1 ([14]).** The system uncertain parameters  $\Delta A_{di}$  and  $\Delta A_i$  are constrained by  $[\Delta A_{di} \ \Delta A_i] = S_i G_{ik} [D_{di} \ D_i]$ , where  $S_i$ ,  $D_{di}$ ,  $D_i$  are constant matrices and  $G_{ik}$  satisfies  $G_{ik}^T G_{ik} \le I$ .

**Remark 1.** It should be emphasized that two Markov chains are introduced in this paper, where two kinds of Markov modes and time-varying TPs information are accurately represented. The processes  $\{\delta_k\}$  and  $\{\varrho_k\}$  can imply that the TPs under consideration change across time yet remain constant within each interval [14]. And Fig. 2 visually demonstrates the evolution of the Markov jump modes and piecewise homogeneous nature [8]. When  $\Sigma = \{1\}$ , the PHMJS (1) reduces to homogeneous MJLS.

Considering that some state components of discrete singular PHMJSs may be unmeasured, a discrete singular piecewise homogeneous Markov jump state observer is devised as:

$$\begin{cases} E\hat{x}(k+1) = A(\delta_k)\hat{x}(k) + A_d(\delta_k)\hat{x}(k - d(k)) + B(\delta_k)u_f(k) + L(\delta_k)(\hat{y}(k) - y(k)), \\ \hat{y}(k) = C(\delta_k)\hat{x}(k), \end{cases} \quad (2)$$

where the estimation of  $x(k)$ , observer output and observer gain are represented by  $\hat{x}(k) \in \mathbb{R}^n$ ,  $\hat{y}(k) \in \mathbb{R}^p$  and  $L(\delta_k)$ . When  $\delta_k = i \in \Pi$ ,  $L(\delta_k)$  is abbreviated as  $L_i$ . The state error between system and the observer is defined as  $e(k) = \hat{x}(k) - x(k)$ .

![Figure 2: The evolutionary diagram of Markov jump modes and piecewise homogeneous nature. The figure consists of two vertically stacked plots sharing a common horizontal axis labeled 'k'. The top plot shows the error e_k as a piecewise constant function, jumping between values 1, 2, and 3 at discrete time instants. The bottom plot shows the event generator delta_k as a piecewise constant function, jumping between values 0 and 1. Vertical dashed lines indicate the time instants of these jumps. The plots illustrate the relationship between the error and the event generation process over time.](7fb5215fd72210a2e4cce6df55550c89_img.jpg)

Figure 2: The evolutionary diagram of Markov jump modes and piecewise homogeneous nature. The figure consists of two vertically stacked plots sharing a common horizontal axis labeled 'k'. The top plot shows the error e\_k as a piecewise constant function, jumping between values 1, 2, and 3 at discrete time instants. The bottom plot shows the event generator delta\_k as a piecewise constant function, jumping between values 0 and 1. Vertical dashed lines indicate the time instants of these jumps. The plots illustrate the relationship between the error and the event generation process over time.

Fig. 2. The evolutionary diagram of Markov jump modes and piecewise homogeneous nature.

### 2.2. Dynamic event-triggered mechanism design

For clarity of dynamic ETM, a triggering time sequence is defined as  $0 \le k_0 < k_1 < \dots < k_i < \dots$  and  $e_x(k) = \hat{x}(k) - \hat{x}(k_i)$ ,  $k \in [k_i, k_{i+1})$  stands for error between  $\hat{x}(k)$  and  $\hat{x}(k_i)$ , where  $k_i$  is the latest triggering instant.

Moreover, the event generator function is determined as

$$f(e_x(k), \Omega_k, \theta_i) = \theta_1 e_x^T(k) M_{im1} e_x(k) - \theta_2 \hat{x}^T(k) M_{im2} \hat{x}(k) - \frac{1}{\delta} \Omega(k),$$

where  $M_{im1} > 0$ ,  $M_{im2} > 0$ , and  $\theta_1, \theta_2, \delta$  are given positive scalars.  $\Omega(k) \in \mathbb{R}$  is an internal dynamical variable satisfying

$$\begin{cases} \Omega(k+1) = \beta \Omega(k) + \theta_2 \hat{x}^T(k) M_{im2} \hat{x}(k) - \theta_1 e_x^T(k) M_{im1} e_x(k), \\ \Omega(0) = \Omega, \end{cases} \quad (3)$$

where  $\beta \in (0, 1)$  is a given constant and  $\Omega \ge 0$  is the initial condition. Obviously, the next triggering instant is given by

$$k_{i+1} = \inf \{ k > k_i | \theta_1 e_x^T(k) M_{im1} e_x(k) - \theta_2 \hat{x}^T(k) M_{im2} \hat{x}(k) - \frac{1}{\delta} \Omega(k) > 0 \}.$$

**Remark 2.** It is worth emphasizing that the weighted matrices  $M_{im1}$  and  $M_{im2}$  in (3) are related to two kinds of Markov modes, and this mode-dependent characteristic can more accurately capture and reflect the closed-loop system dynamic behaviors caused by the change of PHMJS modes. The mode-dependent dynamic ETM can not only effectively save communication resources, but also ensure desired compensation control performance [9].

### 2.3. Compensation controller

Under deception attacks, the control input in (1) is modeled as

$$u_f(k) = u(k) + \Psi(\hat{x}(k_i)), \quad (4)$$

where  $u(k)$  denotes control signal and  $\Psi(\hat{x}(k_i))$  is an unknown nonlinear function which represents injected hostile information.

By NN technology, the nonlinear function  $\Psi(\hat{x}(k_i))$  can be reconstructed as follows:

$$\Psi(\hat{x}(k_i)) = W^T \sigma(V^T \hat{x}(k_i)) + \varepsilon(\hat{x}(k_i)), \quad \forall \hat{x}(k_i) \in Y \subset \mathbb{R}^n, \quad (5)$$

where  $Y$  is a compact set, the weight matrix of input-to-hidden layer and hidden-to-output layer are defined by  $V \in \mathbb{R}^{n \times l}$  and  $W \in \mathbb{R}^{l \times m}$  which satisfies  $\|W\|_F \le W_{\max}$ ,  $l$  is the number of NN nodes,  $\sigma(\cdot) \in \mathbb{R}^l$  stands for the basis function with  $\|\sigma(\cdot)\| \le \sigma_{\max}$ ,  $\varepsilon(\hat{x}(k_i)) \in \mathbb{R}^m$  means error signal with  $\|\varepsilon(\cdot)\| \le \varepsilon_{\max}$ .  $W_{\max}, \sigma_{\max}, \varepsilon_{\max}$  are arbitrary constants. Fig. 3 depicts a classic NN structure [21].

Generally, the weight matrix  $W$  is unknown. Let the estimation of  $W$  be  $\hat{W}$ , then  $\tilde{W}(k) = \hat{W}(k) - W$  stands for weight matrix estimation error. The estimation of  $\Psi(\hat{x}(k_i))$  is constructed as

$$\hat{\Psi}(\hat{x}(k_i)) = \hat{W}^T(k) \sigma(V^T \hat{x}(k_i)). \quad (6)$$

Based on the above analyses, the designed compensation feedback controller can be shown by:

$$u(k) = K_i \hat{x}(k_i) - \hat{\Psi}(\hat{x}(k_i)), \quad (7)$$

where  $K_i$  represents controller gain needed to be obtained.

**Remark 3.** It should be pointed out that, in the research on deception attacks, most results obtained are based on bounded condition assumptions and known least upper bounds of deception attacks. However, the least upper bounds are difficult to be obtained in practical applications [32,41]. Therefore, NN technology with its powerful modeling capabilities is utilized to reconstruct the

![Diagram of a Neural Network (NN) structure with three layers: Input Layer, Hidden Layer, and Output Layer. The Input Layer contains nodes $\hat{x}_1(k_i), \hat{x}_2(k_i), \dots, \hat{x}_n(k_i)$. The Hidden Layer contains nodes $\sigma_1, \sigma_2, \dots, \sigma_{l-1}, \sigma_l$. The Output Layer contains nodes $\Psi_1, \dots, \Psi_m$. All nodes in the Input Layer are connected to all nodes in the Hidden Layer. All nodes in the Hidden Layer are connected to all nodes in the Output Layer.](e394c2b5c61344f6a12397f430086072_img.jpg)

Diagram of a Neural Network (NN) structure with three layers: Input Layer, Hidden Layer, and Output Layer. The Input Layer contains nodes \$\hat{x}\_1(k\_i), \hat{x}\_2(k\_i), \dots, \hat{x}\_n(k\_i)\$. The Hidden Layer contains nodes \$\sigma\_1, \sigma\_2, \dots, \sigma\_{l-1}, \sigma\_l\$. The Output Layer contains nodes \$\Psi\_1, \dots, \Psi\_m\$. All nodes in the Input Layer are connected to all nodes in the Hidden Layer. All nodes in the Hidden Layer are connected to all nodes in the Output Layer.

Fig. 3. The diagram of NN structure.

cyber attacks in this paper, where unknown nonlinear deception attack  $\Psi(\hat{x}(k_i))$  is approximated accurately and bounded condition assumptions are removed [31].

**Remark 4.** It is worth noticing that, when PHMJSs are subjected to deception attacks, their stability and various dynamic performances may be severely impacted [26]. To address this challenge, an effective NN-based compensation feedback controller is proposed in this paper, utilizing a compensation term devised by the reconstructed deception attack  $\hat{\Psi}(\hat{x}(k_i))$ . The compensation feedback controller can mitigate the negative effects arising from malicious attacks on desired system performances while ensuring that the controlled systems can continue to operate stably.

When  $\delta_k = i \in \Pi$ , consisting of system (1), observer (2), deception attack (5), estimated attack (6) and controller (7), the closed-loop discrete singular PHMJS can be built as:

$$\begin{cases} \tilde{E}\tilde{x}(k+1) = \tilde{A}_i\tilde{x}(k) + \tilde{A}_{di}\tilde{x}(k-d(k)) + \tilde{B}_i\tilde{e}_x(k) + \tilde{M}_i\overline{W}^T(k)\sigma(V^T\hat{x}(k_i)) - \tilde{M}_i\tilde{e}(\hat{x}(k_i)), \\ \tilde{y}(k) = \tilde{C}_i\tilde{x}(k), \end{cases} \quad (8)$$

where

$$\begin{aligned} \tilde{y}(k) &= \hat{y}(k) - y(k), \quad \tilde{x}(k) = [x^T(k) \ e^T(k)]^T, \quad \tilde{A}_i = \overline{A}_i + \Delta\overline{A}_i, \quad \tilde{A}_{di} = \overline{A}_{di} + \Delta\overline{A}_{di}, \quad \tilde{C}_i = [0 \ C_i], \\ \overline{A}_{di} &= \begin{bmatrix} A_{di} & 0 \\ 0 & A_{di} \end{bmatrix}, \quad \Delta\overline{A}_{di} = \begin{bmatrix} \Delta A_i & 0 \\ -\Delta A_i & 0 \end{bmatrix}, \quad \overline{A}_i = \begin{bmatrix} A_i + B_i K_i & B_i K_i \\ 0 & A_i + L_i C_i \end{bmatrix}, \quad \tilde{E} = \begin{bmatrix} E & 0 \\ 0 & E \end{bmatrix}, \\ \Delta\overline{A}_{di} &= \begin{bmatrix} \Delta A_{di} & 0 \\ -\Delta A_{di} & 0 \end{bmatrix}, \quad \tilde{M}_i = \begin{bmatrix} -B_i & 0 \\ 0 & 0 \end{bmatrix}, \quad \tilde{B}_i = \begin{bmatrix} B_i K_i & 0 \\ 0 & 0 \end{bmatrix}, \quad \tilde{e}_x(k) = \begin{bmatrix} e_x(k) \\ 0 \end{bmatrix}, \\ \tilde{e}(\hat{x}(k_i)) &= \begin{bmatrix} \varepsilon(\hat{x}(k_i)) \\ 0 \end{bmatrix}, \quad \overline{W}^T(k)\sigma(V^T\hat{x}(k_i)) = \begin{bmatrix} \overline{W}^T(k)\sigma(V^T\hat{x}(k_i)) \\ 0 \end{bmatrix}. \end{aligned}$$

### 2.4. NN weight matrix

Eq. (9) constructs update mechanism for  $\hat{W}(k)$  as follows:

$$\hat{W}(k+1) = (1-s)\hat{W}(k) - \frac{\eta\sigma(V^T\hat{x}(k_i))r^T(k+1)}{1 + \|\sigma(V^T\hat{x}(k_i))\|^2 \|r(k+1)\|^2}, \quad (9)$$

where  $\eta > 0$ ,  $s$  are adjusting parameters and

$$r(k+1) = \begin{cases} \text{col}\{\tilde{y}_1(k+1), \dots, \tilde{y}_m(k+1)\}, & m \le p, \\ \text{col}\left\{\tilde{y}(k+1), \underbrace{0, \dots, 0}_{m-p}\right\}, & m > p. \end{cases}$$

Based on (9), Eq. (10) specifies update mechanism for  $\widetilde{W}(k)$  as

$$\widetilde{W}(k+1) = (1-s)\hat{W}(k) - \frac{\eta\sigma(V^T\hat{x}(k))r^T(k+1)}{1 + \|\sigma(V^T\hat{x}(k))\|^2 \|r(k+1)\|^2}, \quad (10)$$

### 2.5. Basic definitions and lemmas

**Definition 1 ([4,10]).**

- (1) The pair  $(\widetilde{E}, \widetilde{A}_i)$  is regular and causal if  $\det(z\widetilde{E} - \widetilde{A}_i)$  is not identically zero and  $\deg(\det(z\widetilde{E} - \widetilde{A}_i)) = \text{rank}(\widetilde{E})$ .
- (2) The closed-loop discrete singular PHMJS (8) is regular and causal if each pair  $(\widetilde{E}, \widetilde{A}_i)$  is regular and causal, for all  $\delta_k = i \in \Pi$ .

**Definition 2 ([9]).** Consider the discrete singular PHMJS (8), if there exist two constants  $c_1 > 0$ ,  $c_2 > 0$ , two  $K_\infty$  functions  $\alpha_1$  and  $\alpha_2$ , and a L-K functional  $V(\widetilde{x}(k), \delta_k, \theta_k) : \mathbb{R}^{2n} \times \Pi \times \Sigma \to \mathbb{R}$ , such that

$$\begin{cases} \alpha_1(\|\widetilde{x}(k)\|) \le V(\widetilde{x}(k), \delta_k, \theta_k) \le \alpha_2(\|\widetilde{x}(k)\|), \\ \Delta V(\widetilde{x}(k), \delta_k, \theta_k) \le -c_1 V(\widetilde{x}(k), \delta_k, \theta_k) + c_2, \end{cases}$$

for all  $\widetilde{x}(k) \in \mathbb{R}^{2n}$ ,  $k > 0$ , then discrete singular PHMJS (8) is bounded in probability.

**Lemma 1 ([12]).** For positive integers  $\beta_1$  and  $\beta_2$  meeting  $1 \le \beta_1 \le \beta_2$ , any real matrices  $\Gamma \ge 0$ ,  $\Gamma \in \mathbb{R}^{n \times n}$ ,  $\Psi_i \in \mathbb{R}^n$ , one has

$$-(\beta_2 - \beta_1 + 1) \sum_{i=\beta_1}^{\beta_2} \Psi_i^T \Psi_i \le -\left(\sum_{i=\beta_1}^{\beta_2} \Psi_i\right)^T \Gamma \left(\sum_{i=\beta_1}^{\beta_2} \Psi_i\right).$$

**Lemma 2 ([12]).** Given  $\Sigma_1$  and  $\Sigma_2$  are real matrices and a scalar  $\epsilon > 0$ . For matrix  $\Delta$  that satisfies  $\Delta^T \Delta \le I$ , then  $\Sigma_1 \Delta \Sigma_2 + (\Sigma_1 \Delta \Sigma_2)^T \le \epsilon \Sigma_1 \Sigma_1^T + \epsilon^{-1} \Sigma_2^T \Sigma_2$  holds.

## 3. Main results

**Theorem 1.** The discrete singular PHMJS (8) is regular, causal and bounded in probability, if for  $\forall \delta_k = i \in \Pi$ ,  $\forall \theta_k = m \in \Sigma$  and given positive scalars  $\theta_1$ ,  $\theta_2$ ,  $\beta$  ( $0 < \beta < 1$ ),  $\delta$ ,  $d_1$ ,  $d_2$  and  $d = d_2 - d_1$ , there exist matrices  $P_{im} > 0$ ,  $J_{im} > 0$ ,  $J_{im2} > 0$ ,  $M_{im1} > 0$ ,  $M_{im2} > 0$ ,  $Z_{im2}$ ,  $Z_{im4}$ ,  $Q_s > 0$  ( $s = 1, 2, 3$ ),  $\widetilde{R}$ , scalars  $0 < \varphi < 0.5$ ,  $v > 0$ ,  $\lambda_1 > 0$ , and  $\lambda_2 > 0$  such that (11)–(14) hold:

$$\begin{bmatrix} \Omega_{im11} & \Omega_{im12} & \Omega_{im13} \\ * & \Omega_{im22} & \Omega_{im23} \\ * & * & \Omega_{im33} \end{bmatrix} < 0, \quad (11)$$

$$\begin{bmatrix} -\lambda_2 I & \widetilde{M}_i^T \\ * & -I \end{bmatrix} < 0, \quad (12)$$

$$\begin{bmatrix} -\lambda_1 I & \widetilde{M}_i^T U_{im} \\ * & -P_{im}^{-1} \end{bmatrix} < 0, \quad (13)$$

$$(16\lambda_1 + 2\lambda_2)\sigma_{\max}^2 - v\varphi < 0, \quad (14)$$

where

$$\begin{aligned} \Omega_{im11} &= \begin{bmatrix} \Omega_{im11}^{11} & \widetilde{R}\widetilde{A}_{di} & 0 & 0 \\ * & -Q_3 & 0 & 0 \\ * & * & -Q_1 & 0 \\ * & * & * & -Q_2 \end{bmatrix}, \quad \Omega_{im22} = \begin{bmatrix} \Omega_{im11}^{22} & Z_{im2}\widetilde{B}_i & 0 & 0 \\ * & \Omega_{im22}^{22} & 0 & 0 \\ 0 & 0 & -P_{im}^{-1} & 0 \\ 0 & 0 & 0 & -P_{im}^{-1} \end{bmatrix}, \\ \Omega_{im23} &= \begin{bmatrix} \hat{F}_{im11} & 0 & \hat{F}_{im13} \\ 0 & 0 & \hat{F}_{i23} \end{bmatrix}, \quad \overline{S}_i = \begin{bmatrix} S_i & 0 \\ -S_i & 0 \end{bmatrix}, \quad \overline{D}_i = \begin{bmatrix} D_i & 0 \\ 0 & D_i \end{bmatrix}, \quad \overline{D}_{di} = \begin{bmatrix} D_{di} & 0 \\ 0 & D_{di} \end{bmatrix}, \\ \Omega_{im12} &= \text{col}\{\Gamma_{im1}, \Gamma_{im2}, 0, 0\}, \quad \Omega_{im13} = \text{col}\{\widetilde{F}_{i1}, \widetilde{F}_{i2}, 0, 0\}, \quad \hat{F}_{im13} = \text{col}\{\hat{F}_{im13}^1, 0\}, \\ \Omega_{im33} &= \text{diag}\left\{-P_{im}^{-1}, -\xi I, -\xi I, -\xi I, -\xi I\right\}, \quad \Gamma_{im1} = [\Omega_{im11}^{12} \quad \widetilde{R}\widetilde{B}_i \quad \Omega_{im13}^{12} \quad 0], \\ \Gamma_{im2} &= [\overline{A}_{di}^T Z_{im2}^T \quad 0 \quad 0 \quad \Omega_{im24}^T], \quad \widetilde{F}_{i1} = [0 \quad \overline{D}_i^T \quad 0 \quad \xi \widetilde{R}\overline{S}_i \quad \xi \widetilde{R}\overline{S}_i], \quad \hat{F}_{im13}^1 = [\Omega_{im14}^{23} \quad \Omega_{im15}^{23}]. \end{aligned}$$

$$\begin{aligned}\tilde{F}_{i2} &= [0 \ 0 \ \bar{D}_{di}^T \ 0], \ \hat{F}_{im11} = \text{col}\{0, \Omega_{im21}^{23}\}, \ \hat{F}_{i23} = \text{diag}\left\{\sqrt{2\xi}\hat{S}_i, \sqrt{2\xi}\hat{S}_i\right\}, \ \Omega_{im11}^{11} = Q_1 \\ &+ 2\tilde{R}\tilde{R}^T - \tilde{E}^T P_{im} \tilde{E} + Q_2 + (d+1)Q_3 + \tilde{R}(\bar{A}_i - \tilde{E}) + (1-\beta + \frac{1}{\delta})\theta_2 H_{im2} + (\bar{A}_i^T - \tilde{E}^T)\tilde{R}^T, \\ \Omega_{im11}^{12} &= Z_{im4}\tilde{S}^T - \tilde{R} + (\bar{A}_i^T - \tilde{E}^T)Z_{im2}^T, \ \Omega_{im13}^{12} = \sqrt{2}\bar{A}_i^T U_{im}, \ \Omega_{im24}^{12} = 2\bar{A}_{di}^T U_{im}, \\ \Omega_{im11}^{22} &= d_1^2 J_{im1} + d_2^2 J_{im2} - Z_{im2}^T - Z_{im2} + 2Z_{im2}^T Z_{im2}, \ \Omega_{im22}^{22} = -(1-\beta + \frac{1}{\delta})\theta_1 H_{im1}, \\ \Omega_{im14}^{23} &= \Omega_{im15}^{23} = \xi Z_{im2}\bar{S}_i, \ \Omega_{im21}^{23} = 2\sqrt{2}\tilde{B}_i^T U_{im}, \ \hat{S}_i = \underbrace{\text{col}\{\bar{S}_i, -\bar{S}_i, \dots, \bar{S}_i, -\bar{S}_i\}}_{2MN},\end{aligned}$$

$$\begin{aligned}\bar{P}_{im} &= \text{diag}\{P_{k_1 p_1}, \dots, P_{k_N p_1}, \dots, P_{k_1 p_M}, \dots, P_{k_N p_M}\}, \ U_{im} = [U_{im1}^T, U_{im2}^T]^T, \\ U_{im2} &= \left[0, \sqrt{q_{mp_1} \pi_{ik_1}^{(p_1)}} I, \dots, 0, \sqrt{q_{mp_1} \pi_{ik_N}^{(p_1)}} I, \dots, 0, \sqrt{q_{mp_M} \pi_{ik_1}^{(p_M)}} I, \dots, \sqrt{q_{mp_M} \pi_{ik_N}^{(p_M)}} I\right], \\ U_{im1} &= \left[\sqrt{q_{mp_1} \pi_{ik_1}^{(p_1)}} I, 0, \dots, \sqrt{q_{mp_1} \pi_{ik_N}^{(p_1)}} I, 0, \dots, \sqrt{q_{mp_M} \pi_{ik_1}^{(p_M)}} I, 0, \dots, \sqrt{q_{mp_M} \pi_{ik_N}^{(p_M)}} I, 0\right],\end{aligned}$$

and  $\tilde{S} \in \mathbb{R}^{2n \times 2(n-r)}$  is full-column rank satisfying  $\tilde{E}^T \tilde{S} = 0$ .

**Proof.** See Appendix.  $\square$

**Theorem 2.** The discrete singular PHMJS (8) is regular, causal and bounded in probability, if for  $\forall \delta_k = i \in \Pi$ ,  $\forall \varrho_k = m \in \Sigma$  and given positive scalars  $\theta_1, \theta_2, \beta$  ( $0 < \beta < 1$ ),  $\delta, d_1, d_2$  and  $d = d_2 - d_1$ , there exist matrices  $Y_{im1} > 0$ ,  $Y_{im2} > 0$ ,  $\hat{J}_{im1} > 0$ ,  $\hat{J}_{im2} > 0$ ,  $\hat{J}_{im21} > 0$ ,  $\hat{J}_{im22} > 0$ ,  $\hat{M}_{im1} > 0$ ,  $\hat{M}_{im2} > 0$ ,  $W_{im2}$ ,  $\hat{S}_{im1}$ ,  $\hat{Q}_{sv} > 0$  ( $s = 1, 2, 3, v = 1, 2$ ),  $W_1$ , scalars  $0 < \varphi < 0.5$ ,  $\nu > 0$ ,  $\lambda_1 > 0$  and  $\lambda_2 > 0$  such that (15)–(18) hold:

$$\begin{bmatrix} \Lambda_{im11} & \Lambda_{im12} & \Lambda_{im13} & \Lambda_{i14} \\ * & \Lambda_{im22} & 0 & \Lambda_{i24} \\ * & * & \Lambda_{im33} & 0 \\ * & * & * & \Lambda_{44} \end{bmatrix} < 0, \quad (15)$$

$$\begin{bmatrix} -\lambda_2 I & 0 & -B_i^T & 0 \\ * & -\lambda_2 I & 0 & 0 \\ * & * & -I & 0 \\ * & * & * & -I \end{bmatrix} < 0, \quad (16)$$

$$\begin{bmatrix} -\lambda_1 I & 0 & -B_i^T U_{im1} \\ * & -\lambda_1 I & 0 \\ * & * & -P_{im}^{-1} \end{bmatrix} < 0, \quad (17)$$

$$(16\lambda_1 + 2\lambda_2)\sigma_{\max}^2 - \nu\varphi < 0, \quad (18)$$

where

$$\begin{aligned}\Lambda_{im12} &= \begin{bmatrix} 0 & \tilde{Y}_{im12} \\ 0 & 0 \end{bmatrix}, \ \Lambda_{i24} = \begin{bmatrix} 0 & 0 \\ \Psi_{i11} & 0 \end{bmatrix}, \ \Lambda_{im13} = \begin{bmatrix} 0 & \bar{Y}_{i12} \\ 0 & 0 \\ \bar{Y}_{im31} & 0 \end{bmatrix}, \\ \Lambda_{im11} &= \begin{bmatrix} Y_{im11} & 0 & Y_{im13} \\ * & Y_{22} & 0 \\ * & * & Y_{im33} \end{bmatrix}, \ Y_{im13} = \begin{bmatrix} \Xi_{im11}^{13} & 0 & B_i \bar{K}_i \\ \bar{K}_i^T B_i^T & \Xi_{im22}^{13} & 0 \\ W_1 A_{di}^T & 0 & 0 \\ 0 & W_1 A_{di}^T & 0 \end{bmatrix},\end{aligned}$$

$$\begin{aligned}
 Y_{im11} &= \begin{bmatrix} \Xi_{im11}^{11} & \Xi_{im12}^{11} & A_{di}W_1^T & 0 \\ * & \Xi_{im22}^{11} & 0 & A_{di}W_1^T \\ * & * & -\hat{Q}_{31} & 0 \\ * & * & * & -\hat{Q}_{32} \end{bmatrix}, \quad Y_{im33} = \begin{bmatrix} \Xi_{im11}^{33} & 0 & B_i\bar{K}_i \\ * & \Xi_{im22}^{33} & 0 \\ * & * & \Xi_{im33}^{33} \end{bmatrix}, \\
 \Lambda_{im22} &= \text{diag}\{\tilde{\Psi}_{im11}, \Theta_{im}, \Theta_{im}\}, \quad \Lambda_{i14} = \text{col}\{\tilde{Y}_{i11}, 0, \tilde{Y}_{i31}, 0\}, \\
 \Lambda_{im33} &= \text{diag}\{\Theta_{im}, -\xi I, -\xi I, -\xi I, -\xi I\}, \quad \Lambda_{44} = \text{diag}\{-\xi I, -\xi I, -\xi I, -\xi I\}, \\
 \bar{Y}_{i12} &= \text{diag}\{W_1 D_i^T, W_1 D_i^T, W_1 D_{di}^T, W_1 D_{di}^T\}, \quad Y_{22} = \text{diag}\{-\hat{Q}_{11}, -\hat{Q}_{12}, -\hat{Q}_{21}, -\hat{Q}_{22}\}, \\
 \bar{Y}_{im12} &= \text{diag}\{\bar{\Xi}_{im11}^{12}, \bar{\Xi}_{im22}^{12}\}, \quad \bar{Y}_{im31} = 2\sqrt{2}\bar{K}_i^T B_i^T U_{im1}, \quad \Theta_{im} = -\bar{P}_{im}^{-1}, \\
 \Psi_{i11}^1 &= [\sqrt{2}\xi S_i \ I \ 0 \ 0], \quad \Psi_{i11}^2 = [0 \ 0 \ \sqrt{2}\xi S_i \ I], \quad I_1 = \underbrace{\text{col}\{I, -I, \dots, I, -I\}}_{2MN}, \quad \Psi_{i11} = \text{col}\{\Psi_{i11}^1, \Psi_{i11}^2\},
 \end{aligned}$$

$$\begin{aligned}
 \bar{\Xi}_{im11}^{11} &= \alpha^2 Y_{im1} - \alpha W_1 E^T - \alpha E W_1^T + A_i W_1^T + B_i \bar{K}_i - E W_1^T + W_1 A_i^T + \bar{K}_i^T B_i^T - W_1 E^T + \hat{Q}_{11} \\
 &+ \hat{Q}_{21} + (d+1)\hat{Q}_{31} + 2I + (1+\beta+\frac{1}{\delta})\theta_2 \hat{M}_{im2}, \quad \bar{\Xi}_{im22}^{11} = \alpha^2 Y_{im2} - \alpha W_1 E^T - \alpha E W_1^T + \bar{L}_i + \bar{L}_i^T \\
 &+ A_i W_1^T - E W_1^T + W_1 A_i^T - W_1 E^T + \hat{Q}_{12} + \hat{Q}_{22} + (d+1)\hat{Q}_{32} + 2I + (1+\beta+\frac{1}{\delta})\theta_2 \hat{M}_{im2}, \\
 \bar{\Xi}_{im12}^{11} &= B_i \bar{K}_i + (1+\beta+\frac{1}{\delta})\theta_2 \hat{M}_{im2}, \quad \bar{\Xi}_{im11}^{13} = W_1 A_i^T + \bar{K}_i^T B_i^T - W_1 E^T - W_2^T + \hat{S}_{im1}, \\
 \bar{\Xi}_{im11}^{13} &= W_1 A_i^T + \bar{L}_i^T - W_1 E^T - W_2^T + \hat{S}_{im1}, \quad \bar{\Xi}_{im11}^{33} = d_1^2 \hat{J}_{im11} + d_2^2 \hat{J}_{im21} - W_2^T - W_2 + 2I, \\
 \bar{\Xi}_{im22}^{13} &= d_1^2 \hat{J}_{im12} + d_2^2 \hat{J}_{im22} - W_2^T - W_2 + 2I, \quad \bar{\Psi}_{im11} = \bar{\Xi}_{im33}^{33} = -(1+\beta+\frac{1}{\delta})\theta_1 \hat{M}_{im1}, \\
 \bar{\Xi}_{im11}^{12} &= \text{col}\{(\sqrt{2}W_1 A_i^T + \sqrt{2}\bar{K}_i^T B_i^T)U_{im1}, \sqrt{2}\bar{K}_i^T B_i^T U_{im1} + (\sqrt{2}W_1 A_i^T + \sqrt{2}\bar{L}_i^T)U_{im2}\}, \\
 \bar{\Xi}_{im22}^{12} &= \text{col}\{2W_1 A_{di}^T U_{im1}, 2W_1 A_{di}^T U_{im2}\}, \quad \hat{Y}_{i11}^1 = [\xi S_i \ 0 \ \xi S_i \ 0], \quad \hat{Y}_{i11} = \hat{Y}_{i31} = \text{col}\{\hat{Y}_{i11}^1, -\hat{Y}_{i11}^1\}.
 \end{aligned}$$

Then, the observer gains in (2) and controller gains in (7) are obtained by  $K_i = \bar{K}_i W_1^{-T}$ ,  $L_i = \bar{L}_i W_1^{-T} C_{iL}^{-1}$ .

**Proof.** It is obvious that we can get (16), (17) and (18) from (12), (13) and (14) in Theorem 1. Next, we need to verify (15).

$$\begin{aligned}
 \text{Let } Z_{im} &= \text{diag}\{\tilde{R}^{-1}, \tilde{R}^{-1}, \tilde{R}^{-1}, \tilde{R}^{-1}, Z_{im2}^{-1}, \tilde{R}^{-1}, I, I, I, I, I, I\}, \quad \Omega_{im} = \begin{bmatrix} \Omega_{im11} & \Omega_{im12} & \Omega_{im13} \\ * & \Omega_{im22} & \Omega_{im23} \\ * & * & \Omega_{im33} \end{bmatrix}, \quad \text{one has} \\
 Z_{im} \Omega_{im} Z_{im}^T &< 0.
 \end{aligned} \tag{19}$$

According to  $Y_{im1} > 0$ ,  $Y_{im2} > 0$ , we obtain  $(E R^{-T} - \alpha Y_{imj})^T Y_{imj}^{-1} (E R^{-T} - \alpha Y_{imj}) \ge 0$ ,  $\forall j = 1, 2$ .

Then

$$-R^{-1} E^T Y_{imj}^{-1} E R^{-T} \le -\alpha R^{-1} E^T - \alpha E R^{-T} + \alpha^2 Y_{imj}, \quad \forall j = 1, 2, \tag{20}$$

where  $Y_{im1} = P_{im1}^{-1}$ ,  $Y_{im2} = P_{im2}^{-1}$ .

$P_{im}$ ,  $Z_{im2}$ ,  $Z_{im4}$ ,  $\bar{R}$ ,  $Q_1$ ,  $Q_2$ ,  $Q_3$ ,  $J_{imj}$ ,  $J_{im2}$ ,  $\tilde{S}$  in Theorem 1 can be written in the following forms:  $P_{im} = \text{diag}\{P_{im1}, P_{im2}\}$ ,  $Z_{imj} = \text{diag}\{Z_{imj1}, Z_{imj2}\}$  ( $j = 2, 4$ ),  $\bar{R} = \text{diag}\{R, R\}$ ,  $Q_j = \text{diag}\{Q_{j1}, Q_{j2}\}$  ( $j = 1, 2, 3$ ),  $J_{imj} = \text{diag}\{J_{imj1}, J_{imj2}\}$  ( $j = 1, 2$ ),  $\tilde{S} = \text{diag}\{S, S\}$ , where  $P_{im1}$ ,  $P_{im2}$ ,  $Q_{j1}$ ,  $Q_{j2}$  ( $j = 1, 2, 3$ ),  $J_{imj1}$ ,  $J_{imj2}$  ( $j = 1, 2$ ) are symmetric positive definite,  $S \in \mathbb{R}^{n \times (n-r)}$  is full-column rank satisfying  $E^T S = 0$ .

Let  $R^{-1} Q_{ij} R^{-T} = \hat{Q}_{ij}$  ( $i = 1, 2, 3$ ,  $j = 1, 2$ ),  $R^{-1} M_{imj} R^{-T} = \hat{M}_{imj}$  ( $j = 1, 2$ ),  $Z_{im2}^{-1} J_{pq} Z_{im2}^{-T} = \hat{J}_{pq}$  ( $p = 1, 2$ ,  $q = 1, 2$ ),  $Z_{im4} = R K_1$ ,  $R^{-1} Z_{im4} S^T Z_{im2}^{-T} = K_1 S^T Z_{im2}^{-T} = \hat{S}_{im1}$ ,  $K R^{-T} = \bar{K}$ ,  $L_i C_i R^{-T} = \bar{L}_i$ ,  $-\bar{P}_{im}^{-1} = \Theta_{im}$  and define  $R^{-1} = W_1$ ,  $Z_{im2} = W_{im2}$ ,  $Z_{im4} = W_{im4}$ . Thus,  $K_i = \bar{K}_i W_1^{-T}$  and  $L_i = \bar{L}_i W_1^{-T} C_{iL}^{-1}$  can be deduced from  $K R^{-T} = \bar{K}$ ,  $L_i C_i R^{-T} = \bar{L}_i$  and  $R^{-1} = W_1$ . Furthermore, it is easy to get (15) from (19) and (20). Then, the proof of Theorem 2 is finished.  $\square$

## 4. Simulation example

The following example demonstrates the effectiveness of the obtained results. Consider a DC motor model driven load as illustrated in Fig. 4 [2]. Let  $i(t)$ ,  $v(t)$  and  $\omega(t)$  denote the electric current, the armature voltage and the angular velocity of shaft, respectively. The dynamic equation is depicted as follows:

$$\begin{cases} v(t) = Ri(t) + K_o \omega(t), \\ \dot{\omega}(t) = \frac{K_s}{J_i} i(t) - \frac{b}{J_i} \omega(t), \end{cases}$$

![Figure 4: The structural schematic of a DC motor. The diagram shows a DC motor with an armature resistor R and input voltage v(t). The motor's angular velocity is omega(t). The motor is connected to a gear system with gear ratio n. The output shaft is connected to a load with moment of inertia J_cl and damping ratio b_c. The motor itself has a moment of inertia J_m and damping ratio b_m. A switch is shown between the motor and the gear system, and another switch is shown between the gear system and the load. The input voltage v(t) is shown with a lightning bolt symbol, indicating it is subject to deception attacks.](562f471e8153729557e6a4ee6343c32c_img.jpg)

Figure 4: The structural schematic of a DC motor. The diagram shows a DC motor with an armature resistor R and input voltage v(t). The motor's angular velocity is omega(t). The motor is connected to a gear system with gear ratio n. The output shaft is connected to a load with moment of inertia J\_cl and damping ratio b\_c. The motor itself has a moment of inertia J\_m and damping ratio b\_m. A switch is shown between the motor and the gear system, and another switch is shown between the gear system and the load. The input voltage v(t) is shown with a lightning bolt symbol, indicating it is subject to deception attacks.

Fig. 4. The structural schematic of DC motor.

Table 1

The numerical contrast for different ETMs.

|             | Average release intervals | Transmitted packet numbers | Bandwidth occupancy ratios |
|-------------|---------------------------|----------------------------|----------------------------|
| Static ETM  | 0.3333                    | 30                         | 60%                        |
| Dynamic ETM | 0.4762                    | 21                         | 42%                        |

where  $K_s$ ,  $K_\omega$  and  $K_o$  denote the torque constant, the electromotive force and the armature resistor, respectively.  $b$  and  $J_i$ ,  $i \in \Pi = \{1, 2\}$  are the damping ratio and converted moment of inertia, separately, which are defined as follows:

$$\begin{cases} b = b_m + \frac{b_c}{n^2}, \\ J_i = J_m + \frac{J_{ci}}{n^2}, \end{cases}$$

where  $b_m$  and  $b_c$  are the damping ratios with gear ratio  $n$ .  $J_{ci}$  and  $J_m$  are the moments of the load and the motor.

Letting  $u(t) = v(t)$ ,  $x_1(t) = i(t)$ ,  $x_2(t) = \omega(t)$ , then the DC model can be written by the following singular PHMJS:

$$\begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix} \dot{x}(t) = \begin{bmatrix} R & K_\omega \\ K_s & -\frac{b}{J_i} \end{bmatrix} x(t) + \begin{bmatrix} -1 \\ 0 \end{bmatrix} u(t) + A_{di}x(t-d(t)).$$

By discretization, we obtain the following discrete singular PHMJS:

$$\begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix} x(k+1) = \begin{bmatrix} RT & K_\omega T \\ \frac{K_s T}{J_i} & 1 - \frac{bT}{J_i} \end{bmatrix} x(k) + \begin{bmatrix} -T \\ 0 \end{bmatrix} u(k) + A_{di}x(k-d(k)),$$

where  $T$  denotes the sampling interval. According to [2], the corresponding parameters are considered as  $R = 1.3 \Omega$ ,  $K_\omega = 2.75 \text{ Vs/rad}$ ,  $K_s = 3.7 \text{ Nm/A}$ ,  $b_m = 1$ ,  $b_c = 220$ ,  $J_{c1} = 50 \text{ kg m}^2$ ,  $J_{c2} = 60 \text{ kg m}^2$ ,  $J_m = 0.5 \text{ kg m}^2$ ,  $T = 0.2 \text{ s}$ ,  $n = 10$ ,  $A_{d1} = \text{diag}\{0, 0.1\}$ ,  $A_{d2} = \text{diag}\{0, 0.15\}$ ,  $\Omega = 1$  and

$$C_1 = \begin{bmatrix} 0.2 & 0.02 \\ 0.15 & -0.2 \end{bmatrix}, \quad C_2 = \begin{bmatrix} 0.17 & 0.05 \\ 0.1 & -0.15 \end{bmatrix}, \quad S_1 = \begin{bmatrix} 0.01 \\ 0.02 \end{bmatrix}, \quad S_2 = \begin{bmatrix} 0.02 \\ 0.01 \end{bmatrix},$$

$$D_1 = [0.08 \ -0.12], \quad D_2 = [0.1 \ -0.08], \quad D_{d1} = [-0.1 \ 0.01], \quad D_{d2} = [-0.07 \ 0.03], \quad G_{1k} = G_{2k} = \sin(0.01k).$$

The TP matrices and HTP matrix are given as

$$TP_1 = \begin{bmatrix} 0.28 & 0.72 \\ 0.48 & 0.52 \end{bmatrix}, \quad TP_2 = \begin{bmatrix} 0.46 & 0.54 \\ 0.25 & 0.75 \end{bmatrix}, \quad HTP = \begin{bmatrix} 0.5 & 0.5 \\ 0.9 & 0.1 \end{bmatrix}.$$

By solving the LMIs (15)–(18) in Theorem 2 with  $d_2 = 2$  and  $d_1 = 1$ , the observer and controller gains are obtained as follows:

$$L_1 = \begin{bmatrix} 13.2347 & -4.5938 \\ 2.2752 & -1.9143 \end{bmatrix}, \quad L_2 = \begin{bmatrix} 11.8336 & -3.1197 \\ 1.7926 & -1.4337 \end{bmatrix}, \quad K_1 = \begin{bmatrix} -2.9343 \\ -1.0843 \end{bmatrix}^T, \quad K_2 = \begin{bmatrix} -2.3757 \\ -1.0468 \end{bmatrix}^T.$$

Given the initial conditions  $x(0) = [-0.6 \ 0.5]^T$ ,  $\hat{x}(0) = [-0.5 \ 0.6]^T$ , state trajectories of  $x(k)$  and their estimation  $\hat{x}(k)$  are plotted in Figs. 5 and 6, respectively, which show that the system states can quickly converge to a small neighborhood under deception attacks. The state error between the system and the observer is shown in Fig. 7, which clearly indicates that the observer is able to effectively track the system states. And Fig. 8 depicts control input of the discrete singular PHMJS (8) under deception attacks.

Let the malicious information  $\Psi(\hat{x}(k_i))$  be defined as  $0.5(\hat{x}_1(k_i)^2 + \hat{x}_2(k_i)^2)^{1/2}$ . The initial condition  $\hat{W}(0)$  is set as  $\hat{W}(0) = 0.03 \times \text{ones}(20, 1)$ , the parameters of (9) are devised as  $s = 0.05$ ,  $\eta = 0.3$  and  $\sigma(V^T \hat{x}(k_i)) = \tanh(V^T \hat{x}(k_i))$ . Fig. 9 displays the deception attacks  $\Psi(\hat{x}(k_i))$  and reconstructed attacks  $\hat{\Psi}(\hat{x}(k_i))$ .

To emphasize the superior performance of dynamic ETM, Table 1 illustrates comparative data between static ETM and dynamic ETM on three key metrics: average event release interval, number of packets transmitted, and bandwidth occupancy ratio. Figs. 10

![Figure 5: State trajectory of x1(k) and its estimation x-hat1(k).](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 5 is a multi-panel plot showing the state trajectory of  $x_1(k)$  and its estimation  $\hat{x}_1(k)$  over time  $k$  from 0 to 10. The main plot shows  $x_1(k)$  (dashed blue line) and  $\hat{x}_1(k)$  (solid magenta line). The y-axis is labeled 'State and estimated state' and ranges from -0.6 to 0.2. The x-axis is labeled 'Time(k)'. Two zoom-in boxes are present: one for  $k \in [3, 4.5]$  showing the initial transient, and another for  $k \in [0, 10]$  showing the 'System Variation of Mode TP matrices' for modes 1 and 2, which are square waves.

Figure 5: State trajectory of x1(k) and its estimation x-hat1(k).

Fig. 5. State trajectory of  $x_1(k)$  and its estimation  $\hat{x}_1(k)$ .![Figure 6: State trajectory of x2(k) and its estimation x-hat2(k).](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 6 is a multi-panel plot showing the state trajectory of  $x_2(k)$  and its estimation  $\hat{x}_2(k)$  over time  $k$  from 0 to 10. The main plot shows  $x_2(k)$  (dashed blue line) and  $\hat{x}_2(k)$  (solid magenta line). The y-axis is labeled 'State and estimated state' and ranges from -0.2 to 0.6. The x-axis is labeled 'Time(k)'. Two zoom-in boxes are present: one for  $k \in [3, 5.5]$  showing the steady-state error, and another for  $k \in [0, 10]$  showing the 'System Variation of Mode TP matrices' for modes 1 and 2, which are square waves.

Figure 6: State trajectory of x2(k) and its estimation x-hat2(k).

Fig. 6. State trajectory of  $x_2(k)$  and its estimation  $\hat{x}_2(k)$ .![Figure 7: Error trajectories of e(k).](33228b4227fa57e1477b27b9e07483e6_img.jpg)

Figure 7 is a multi-panel plot showing the error trajectories of  $e(k)$  over time  $k$  from 0 to 10. The main plot shows  $e_1(k)$  (solid magenta line) and  $e_2(k)$  (dashed blue line). The y-axis is labeled 'Error trajectories' and ranges from -0.1 to 0.2. The x-axis is labeled 'Time(k)'. Two zoom-in boxes are present: one for  $k \in [2, 4.5]$  showing the initial transient, and another for  $k \in [2, 6]$  showing the error on a scale of  $\times 10^{-6}$ .

Figure 7: Error trajectories of e(k).

Fig. 7. Error trajectories of  $e(k)$ .![Figure 8: Control input u(k).](df476ed6ad0bb890c67aa63e7647d071_img.jpg)

Figure 8 is a multi-panel plot showing the control input  $u(k)$  over time  $k$  from 0 to 10. The main plot shows  $u(k)$  (solid blue line). The y-axis is labeled 'Control input' and ranges from 0 to 1.5. The x-axis is labeled 'Time(k)'. A zoom-in box is present for  $k \in [2, 4.5]$  showing the control input on a scale of  $\times 10^{-3}$ .

Figure 8: Control input u(k).

Fig. 8. Control input  $u(k)$ .



![Figure 9: A line graph showing deception attacks and reconstructed attacks over time. The x-axis is Time(k) from 0 to 10. The y-axis is Deception attack from -0.1 to 0.4. A solid magenta line represents the deception attack Ψ(̂x(k_t)) and a dashed blue line represents the reconstructed attack ̂Ψ(̂x(k_t)). An inset zooms in on the region from k=1.5 to 4, showing the reconstructed attack stabilizing near zero.](10c82dcc5f2c237961329dd29d65859c_img.jpg)

Figure 9: A line graph showing deception attacks and reconstructed attacks over time. The x-axis is Time(k) from 0 to 10. The y-axis is Deception attack from -0.1 to 0.4. A solid magenta line represents the deception attack Ψ(̂x(k\_t)) and a dashed blue line represents the reconstructed attack ̂Ψ(̂x(k\_t)). An inset zooms in on the region from k=1.5 to 4, showing the reconstructed attack stabilizing near zero.

Fig. 9. The deception attacks  $\Psi(\hat{x}(k_t))$  and reconstructed attacks  $\hat{\Psi}(\hat{x}(k_t))$ .

![Figure 10: A stem plot showing release moments and intervals for static ETM. The x-axis is Time(k) from 0 to 10. The y-axis is Release intervals from 0 to 0.8. Blue stems indicate release moments at various time steps.](86089bb74e9c313a8c62cd0cb41c3e66_img.jpg)

Figure 10: A stem plot showing release moments and intervals for static ETM. The x-axis is Time(k) from 0 to 10. The y-axis is Release intervals from 0 to 0.8. Blue stems indicate release moments at various time steps.

Fig. 10. Release moments and intervals for static ETM.

![Figure 11: A stem plot showing release moments and intervals for dynamic ETM. The x-axis is Time(k) from 0 to 10. The y-axis is Release intervals from 0 to 1.5. Blue stems indicate release moments, showing fewer and longer intervals compared to static ETM.](b712e7522f1bb7135730c7d1abb46d43_img.jpg)

Figure 11: A stem plot showing release moments and intervals for dynamic ETM. The x-axis is Time(k) from 0 to 10. The y-axis is Release intervals from 0 to 1.5. Blue stems indicate release moments, showing fewer and longer intervals compared to static ETM.

Fig. 11. Release moments and intervals for dynamic ETM.

and 11 depict the triggering instants and release intervals for static ETM and dynamic ETM, respectively. Compared to static ETM, we can observe that dynamic ETM transmits fewer packets and has a lower broadband utilization, while the average release interval is longer. These features make dynamic ETM perform better in terms of saving network bandwidth resources.

# 5. Conclusions

In this paper, the issue of NN-based compensation control for uncertain delayed discrete singular PHMJSs under deception attacks has been investigated. Considering the unmeasurable system states and limited network bandwidth, the states have been estimated via utilizing a state observer and communication resources have been saved through an improved ETM. For Markov chains, time-varying TPs resulting from environmental changes and external disturbances have been considered to be piecewise homogeneous, whose stochastic variations have been regulated by a HTP matrix. Moreover, in order to alleviate the adverse impact arising from deception attacks over the controller-actuator transmission channel, the NN technique has been employed to approximate malicious attacks. Then, an event-triggered compensation feedback controller based on the reconstructed deception attack signals has been devised to compensate for the negative effect of deception attacks on systems. By taking advantage of singular value decomposition technique and double-mode-dependent L-K functional, fresh conditions of the regularity, causality and boundedness in probability

for discrete singular PHMJSs have been obtained under the framework of LMIs. Ultimately, the effectiveness of the obtained NN and ETM-based compensation control approach has been validated by a DC motor.

It is noteworthy that, due to the inevitable factors such as the networked environment and time delay, asynchronization between the modes of plant and the controller is difficult to avoid. On the other hand, the introduction of factors such as piecewise homogeneous Markov jump chain, dynamic event-triggered mechanism and deception attacks is going to result in more intricate calculations. Hence, in the upcoming research endeavors, we will address the asynchronous control for PHMJSs to enhance our research results and concentrate on tackling the computational complexity issues arising from factors such as piecewise homogeneous Markov jump chain, dynamic event-triggered mechanism and deception attacks.

# CRediT authorship contribution statement

**Yanran Fu:** Writing – original draft, Software. **Guangming Zhuang:** Writing – original draft. **Jun-e Feng:** Supervision, Conceptualization. **Yanqian Wang:** Supervision, Conceptualization.

# Declaration of competing interest

The authors declare that they have no conflict of interest.

# Acknowledgments

The authors would like to extend special thanks to the Editors and Reviewers, whose rigorous comments and vital suggestions have assisted us in greatly raising the quality of this paper. This work was supported by National Natural Science Foundation of China under Grants 62173174, 62273201, 61773191; Shandong Provincial Natural Science Foundation, PR China under Grants ZR2024MF081, ZR2022MF252; Liaocheng University Education Reform Project, PR China under Grant G2023023; Graduate Education High-Quality Curriculum Construction Project for Liaocheng University–Introduction to Systems Science, PR China under Grant 202408.

All the authors have read and approved this version of the article, and due care has been taken to ensure the integrity of the work.

# Appendix. Proof of Theorem 1

**Proof.** Firstly, the regularity and causality of the closed-loop discrete singular PHMJS (8) will be verified. Because of  $\text{rank}(\tilde{E}) = 2r$ , there are nonsingular matrices  $\Gamma_1$  and  $\Gamma_2$  such that

$$\Gamma_1 \tilde{E} \Gamma_2 = \begin{bmatrix} I_{2r} & 0 \\ 0 & 0 \end{bmatrix}, \quad \Gamma_1 \bar{A}_i \Gamma_2 = \begin{bmatrix} \bar{A}_{i1} & \bar{A}_{i2} \\ \bar{A}_{i3} & \bar{A}_{i4} \end{bmatrix}, \quad \Gamma_1^{-T} \tilde{S} = \begin{bmatrix} 0 \\ \tilde{S}_1 \end{bmatrix}, \quad \Gamma_2^T Z_{im4} = \begin{bmatrix} Z_{im41} \\ Z_{im42} \end{bmatrix},$$

where  $\tilde{S}_1 \in \mathbb{R}^{2(n-r) \times 2(n-r)}$  is any nonsingular matrix. By inequality (11), one can get

$$\begin{bmatrix} \Gamma_{im11} & \Omega_{im11}^{12} \\ * & \Gamma_{im21} \end{bmatrix} < 0, \quad (21)$$

where  $\Gamma_{im11} = -\tilde{E}^T P_{im} \tilde{E} + \tilde{R}(\bar{A}_i - \tilde{E}^T) \tilde{R}^T$ ,  $\Gamma_{im21} = -Z_{im2}^T - Z_{im2}$ . Then multiplying (21) by  $[I \quad \bar{A}_i^T]$  and  $[I \quad \bar{A}_i^T]^T$ , respectively, it is not hard to obtain that

$$-\tilde{E}^T P_{im} \tilde{E} - \tilde{R} \tilde{E} - \tilde{E}^T \tilde{R}^T + \bar{A}_i^T \tilde{S} Z_{im4}^T + Z_{im4} \tilde{S}^T \bar{A}_i - \bar{A}_i^T Z_{im2} \tilde{E} - \tilde{E}^T Z_{im2}^T \bar{A}_i < 0. \quad (22)$$

Pre- and post-multiplying (22) by  $\Gamma_2^T$  and  $\Gamma_2$ , separately, one can yield

$$\begin{aligned} & - \begin{bmatrix} I_{2r} & 0 \\ 0 & 0 \end{bmatrix} \Gamma_1^{-T} P_{im} \Gamma_1^{-1} \begin{bmatrix} I_{2r} & 0 \\ 0 & 0 \end{bmatrix} - \Gamma_2^T \tilde{R} \Gamma_1^{-1} \begin{bmatrix} I_{2r} & 0 \\ 0 & 0 \end{bmatrix} \\ & - \begin{bmatrix} I_{2r} & 0 \\ 0 & 0 \end{bmatrix} \Gamma_1^{-T} \tilde{R}^T \Gamma_2 + \begin{bmatrix} \bar{A}_{i1}^T & \bar{A}_{i3}^T \\ \bar{A}_{i2}^T & \bar{A}_{i4}^T \end{bmatrix} \Gamma_1^{-T} \tilde{S} \begin{bmatrix} Z_{im41} \\ Z_{im42} \end{bmatrix}^T + \begin{bmatrix} Z_{im41} \\ Z_{im42} \end{bmatrix} \tilde{S}^T \Gamma_1^{-1} \begin{bmatrix} \bar{A}_{i1} & \bar{A}_{i2} \\ \bar{A}_{i3} & \bar{A}_{i4} \end{bmatrix} < 0. \end{aligned}$$

Then, the following inequality can be derived as:

$$\begin{bmatrix} \# & \# \\ \# & \bar{A}_{i4}^T \tilde{S}_1 Z_{im42}^T + Z_{im42} \tilde{S}_1^T \bar{A}_{i4} \end{bmatrix} < 0, \quad (23)$$

where the symbol “#” means that the matrices have no relation with the following discussion. Thus, we get  $\bar{A}_{i4}^T \tilde{S}_1 Z_{im42}^T + Z_{im42} \tilde{S}_1^T \bar{A}_{i4} < 0$ , which implies the nonsingularity of  $\bar{A}_{i4}$ . Hence  $(\tilde{E}, \bar{A}_i)$  is regular and causal. Based on Definition 1, the closed-loop discrete singular PHMJS (8) satisfies regularity and causality.

Next, we will prove boundedness in probability of the discrete singular PHMJS (8). Construct the double-mode-dependent L-K functional:

$$V(\tilde{x}(k), \delta_k, \varrho_k) = \sum_{\sigma=1}^{7} V_{\sigma}(\tilde{x}(k), \delta_k, \varrho_k),$$

where  $V_1(\tilde{x}(k), \delta_k, \varrho_k) = \tilde{x}^T(k) \tilde{E}^T P_{\delta_k, \varrho_k} \tilde{E} \tilde{x}(k),$

$$V_2(\tilde{x}(k), \delta_k, \varrho_k) = \sum_{s=k-d_1}^{k-1} \tilde{x}^T(s) Q_1 \tilde{x}(s) + \sum_{s=k-d_2}^{k-1} \tilde{x}^T(s) Q_2 \tilde{x}(s),$$

$$V_3(\tilde{x}(k), \delta_k, \varrho_k) = \sum_{l=-d_2+1}^{-d_1+1} \sum_{s=k-1+l}^{k-1} \tilde{x}^T(s) Q_3 \tilde{x}(s),$$

$$V_4(\tilde{x}(k), \delta_k, \varrho_k) = d_1 \sum_{l=-d_1}^{-1} \sum_{s=k+l}^{k-1} \tilde{\phi}^T(s) \tilde{E}^T J_{\delta_k, \varrho_k, 1} \tilde{E} \tilde{\phi}(s),$$

$$V_5(\tilde{x}(k), \delta_k, \varrho_k) = d \sum_{l=-d_2}^{-d_1-1} \sum_{s=k+l}^{k-1} \tilde{\phi}^T(s) \tilde{E}^T J_{\delta_k, \varrho_k, 2} \tilde{E} \tilde{\phi}(s),$$

$$V_6(\tilde{x}(k), \delta_k, \varrho_k) = \frac{1}{\delta} \Omega(k),$$

$$V_7(\tilde{x}(k), \delta_k, \varrho_k) = vTr\{\tilde{W}^T(k) \tilde{W}(k)\},$$

$$\tilde{\phi}(k) = \tilde{x}(k+1) - \tilde{x}(k).$$

For  $\delta_k = i \in \Pi$ ,  $\delta_{k+1} = j \in \Pi$ ,  $\varrho_k = m \in \Sigma$  and  $\varrho_{k+1} = n \in \Sigma$ , one has

$$\begin{aligned} \Delta V_1(\tilde{x}(k), \delta_k, \varrho_k) &= \mathbb{E}\{V_1(\tilde{x}(k+1), \delta_{k+1}, \varrho_{k+1}) - V_1(\tilde{x}(k), \delta_k, \varrho_k)\} \\ &= \mathbb{E}\{[\tilde{A}_i \tilde{x}(k) + \tilde{A}_{di} \tilde{x}(k-d(k)) + \tilde{B}_i \tilde{e}_x(k) + \tilde{M}_i \tilde{W}^T(k) \bar{\sigma}(V^T \hat{x}(k_i)) - \tilde{M}_i \bar{\varepsilon}(\hat{x}(k_i))]^T \\ &\times (\sum_{n=1}^{M} q_{nn} \sum_{j=1}^{N} \pi_{ij}^n P_{jn}) [\tilde{A}_i \tilde{x}(k) + \tilde{A}_{di} \tilde{x}(k-d(k)) + \tilde{B}_i \tilde{e}_x(k) + \tilde{M}_i \tilde{W}^T(k) \bar{\sigma}(V^T \hat{x}(k_i))] \\ &- \tilde{M}_i \bar{\varepsilon}(\hat{x}(k_i))] - \tilde{x}^T(k) \tilde{E}^T P_{im} \tilde{E} \tilde{x}(k)\}. \end{aligned}$$

In light of the Cauchy-Schwarz inequality [40], one obtains

$$\begin{aligned} \Delta V_1(\tilde{x}(k), \delta_k, \varrho_k) &\le \tilde{x}^T(k) (2 \tilde{A}_i^T \tilde{P}_{im} \tilde{A}_i - \tilde{E} P_{im} \tilde{E}) \tilde{x}(k) + \tilde{e}_x^T(k) (8 \tilde{B}_i^T \tilde{P}_{im} \tilde{B}_i) \tilde{e}_x(k) \\ &+ \tilde{x}^T(k-d(k)) (4 \tilde{A}_{di}^T \tilde{P}_{im} \tilde{A}_{di}) \tilde{x}(k-d(k)) + 16 \sup_{i \in \Pi, m \in \Sigma} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{P}_{im} \tilde{M}_i) \right\} \varepsilon_{\max}^2 \\ &+ 16 \sup_{i \in \Pi, m \in \Sigma} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{P}_{im} \tilde{M}_i) \right\} \sigma_{\max}^2 \|\tilde{W}(k)\|_F^2. \end{aligned} \quad (24)$$

$$\begin{aligned} \Delta V_2(\tilde{x}(k), \delta_k, \varrho_k) &= \mathbb{E}\{V_2(\tilde{x}(k+1), \delta_{k+1}, \varrho_{k+1}) - V_2(\tilde{x}(k), \delta_k, \varrho_k)\} \\ &= \tilde{x}^T(k) Q_1 \tilde{x}(k) + \tilde{x}^T(k) Q_2 \tilde{x}(k) - \tilde{x}^T(k-d_2) Q_2 \tilde{x}(k-d_2) - \tilde{x}^T(k-d_1) Q_1 \tilde{x}(k-d_1), \end{aligned} \quad (25)$$

$$\begin{aligned} \Delta V_3(\tilde{x}(k), \delta_k, \varrho_k) &= \mathbb{E}\{V_3(\tilde{x}(k+1), \delta_{k+1}, \varrho_{k+1}) - V_3(\tilde{x}(k), \delta_k, \varrho_k)\} \\ &= (d+1) \tilde{x}^T(k) Q_3 \tilde{x}(k) - \sum_{s=k-d_2}^{k-d_1} \tilde{x}^T(s) Q_3 \tilde{x}(s) \\ &\le (d+1) \tilde{x}^T(k) Q_3 \tilde{x}(k) - \tilde{x}^T(k-d(k)) Q_3 \tilde{x}(k-d(k)). \end{aligned} \quad (26)$$

Applying Lemma 1, we obtain

$$\begin{aligned} \Delta V_4(\tilde{x}(k), \delta_k, \varrho_k) &= \mathbb{E}\{V_4(\tilde{x}(k+1), \delta_{k+1}, \varrho_{k+1}) - V_4(\tilde{x}(k), \delta_k, \varrho_k)\} \\ &= d_1^2 \tilde{\phi}^T(k) \tilde{E}^T J_{im1} \tilde{E} \tilde{\phi}(k) - d_1 \sum_{s=k-d_1}^{k-1} \tilde{\phi}^T(s) \tilde{E}^T J_{im1} \tilde{E} \tilde{\phi}(s) \\ &\le d_1^2 \tilde{\phi}^T(k) \tilde{E}^T J_{im1} \tilde{E} \tilde{\phi}(k) - \left( \sum_{s=k-d_1}^{k-1} \tilde{\phi}^T(s) \tilde{E}^T J_{im1} \tilde{E} \left( \sum_{s=k-d_1}^{k-1} \tilde{\phi}(s) \right) \right) \\ &= d_1^2 \tilde{\phi}^T(k) \tilde{E}^T J_{im1} \tilde{E} \tilde{\phi}(k) - (\tilde{x}(k) - \tilde{x}(k-d_1))^T \tilde{E}^T J_{im1} \tilde{E} (\tilde{x}(k) - \tilde{x}(k-d_1)), \end{aligned} \quad (27)$$

$$\begin{aligned}
\Delta V_5(\tilde{x}(k), \delta_k, \varrho_k) &= \mathbb{E}\{V_5(\tilde{x}(k+1), \delta_{k+1}, \varrho_{k+1}) - V_5(\tilde{x}(k), \delta_k, \varrho_k)\} \\
&= d^2 \tilde{\varphi}^{T}(k) \tilde{E}^T J_{im2} \tilde{E} \tilde{\varphi}(k) - d \sum_{s=k-d_2}^{k-d_1-1} \tilde{\varphi}^{T}(s) \tilde{E}^T J_{im2} \tilde{E} \tilde{\varphi}(s) \\
&\le d^2 \tilde{\varphi}^{T}(k) \tilde{E}^T J_{im2} \tilde{E} \tilde{\varphi}(k) - \left( \sum_{s=k-d_2}^{k-d_1-1} \tilde{\varphi}^{T}(s) \right) \tilde{E}^T J_{im2} \tilde{E} \left( \sum_{s=k-d_2}^{k-d_1-1} \tilde{\varphi}(s) \right) \\
&= d^2 \tilde{\varphi}^{T}(k) \tilde{E}^T J_{im2} \tilde{E} \tilde{\varphi}(k) - \left( \tilde{x}(k-d_1) - \tilde{x}(k-d_2) \right)^T \tilde{E}^T J_{im2} \tilde{E} \left( \tilde{x}(kd_1) - \tilde{x}(kd_2) \right).
\end{aligned} \tag{28}$$

From (3), we can obtain

$$\begin{aligned}
\Delta V_6(\tilde{x}(k), \delta_k, \varrho_k) &= \mathbb{E}\{V_6(\tilde{x}(k+1), \delta_{k+1}, \varrho_{k+1}) - V_6(\tilde{x}(k), \delta_k, \varrho_k)\} \\
&= \frac{1}{\delta} \{(\beta-1)\Omega(k) - \theta_1 e_x^T(k) M_{im1} e_x(k) + \theta_2 \hat{x}^T(k) M_{im2} \hat{x}(k)\} \\
&\le (1-\beta+\frac{1}{\delta}) \{ \theta_2 \tilde{x}^T(k) H_{im2} \tilde{x}(k) - \theta_1 \tilde{e}_x^T(k) H_{im1} \tilde{e}_x(k) \},
\end{aligned} \tag{29}$$

$$\text{where } H_{im1} = \begin{bmatrix} M_{im1} & 0 \\ 0 & M_{im1} \end{bmatrix}, H_{im2} = \begin{bmatrix} M_{im2} & M_{im2} \\ M_{im2} & M_{im2} \end{bmatrix}.$$

For convenience, define

$$\mu(k) = \frac{\eta \sigma(V^T \hat{x}(k_i)) r^T(k+1)}{1 + \|\sigma(V^T \hat{x}(k_i))\|^2 \|r(k+1)\|^2}.$$

Then, the difference of  $V_7(\tilde{x}(k), \delta_k, \varrho_k)$  can be derived as

$$\begin{aligned}
\Delta V_7(\tilde{x}(k), \delta_k, \varrho_k) &= \mathbb{E}\{V_7(\tilde{x}(k+1), \delta_{k+1}, \varrho_{k+1}) - V_7(\tilde{x}(k), \delta_k, \varrho_k)\} \\
&= vTr\{-\tilde{W}^T(k) \tilde{W}(k) + \tilde{W}^T(k+1) \tilde{W}(k+1)\} \\
&= vTr\{s^2 \tilde{W}^T(k) \tilde{W}(k) + \eta^2 \mu^T(k) \mu(k) r(k+1) r^T(k+1) \\
&\quad - 2s \tilde{W}^T(k) \tilde{W}(k) - 2\eta \tilde{W}^T(k) \mu(k) r^T(k+1) + 2s\eta \tilde{W}^T(k) \mu(k) r^T(k+1)\}.
\end{aligned} \tag{30}$$

Utilizing  $Tr\{\mu^T(k) \mu(k) r(k+1) r^T(k+1)\} \le \frac{1}{4}$  and Young's inequality, we can get

$$\begin{cases} Tr\{\eta^2 \mu^T(k) \mu(k) r(k+1) r^T(k+1)\} \le \frac{\eta^2}{4}, \\ Tr\{-2\eta \tilde{W}^T(k) \mu(k) r^T(k+1)\} \le Tr\{\frac{\tilde{W}^T(k) \tilde{W}(k)}{4r} + r\eta^2\}, \\ Tr\{2s\eta \tilde{W}^T(k) \mu(k) r^T(k+1)\} \le Tr\{s^2 \tilde{W}^T(k) \tilde{W}(k) + \frac{\eta^2}{4}\}. \end{cases} \tag{31}$$

In addition, the term  $Tr\{-2s \tilde{W}^T(k) \tilde{W}(k)\}$  is expressed as

$$Tr\{-2s \tilde{W}^T(k) \tilde{W}(k)\} = Tr\{s(W^T W - \tilde{W}^T(k) \tilde{W}(k) - \tilde{W}^T(k) \tilde{W}(k))\}. \tag{32}$$

From (30) to (32), the difference of  $V_7(\tilde{x}(k), \delta_k, \varrho_k)$  leads to

$$\Delta V_7(\tilde{x}(k), \delta_k, \varrho_k) \le -v(s - \frac{1}{4r}) \|\tilde{W}(k)\|_F^2 - v s(1-2s) \|\tilde{W}(k)\|_F^2 + v \zeta_W, \tag{33}$$

where  $\zeta_W = s \|W(k)\|_F^2 + (r+0.5)\eta^2$ .

For  $\frac{1}{4r} < s < \frac{1}{2}$  with  $r > 1$ , (33) can be rewritten as

$$\Delta V_7(\tilde{x}(k), \delta_k, \varrho_k) \le -v\varphi \|\tilde{W}(k)\|_F^2 + v \zeta_W, \tag{34}$$

where  $\varphi = s - \frac{1}{4r}$ .

Considering (8) and  $\tilde{E}^T \tilde{S} = 0$ , it can be verified that for any matrices  $\tilde{R}$ ,  $Z_{im2}$  and  $Z_{im4}$  with suitable dimensions, the following three equations hold.

$$2\tilde{x}^T(k) Z_{im4} \tilde{S}^T \tilde{E} \tilde{\varphi}(k) = 0. \tag{35}$$

$$\begin{aligned}
2\tilde{x}^T(k) \tilde{R} \left[ (\tilde{A}_i - \tilde{E})\tilde{x}(k) - \tilde{E}\tilde{\varphi}(k) + \tilde{B}_i \tilde{e}_x(k) - \tilde{M}_i \tilde{e}(\hat{x}(k_i)) \right. \\
\left. + \tilde{M}_i \tilde{W}^T(k) \tilde{\sigma}(V^T \hat{x}(k_i)) + \tilde{A}_{di} \tilde{x}(k-d(k)) \right] = 0,
\end{aligned} \tag{36}$$

$$\begin{aligned}
2(\tilde{E}\tilde{\varphi}(k))^T Z_{im2} \left[ (\tilde{A}_i - \tilde{E})\tilde{x}(k) - \tilde{E}\tilde{\varphi}(k) - \tilde{M}_i \tilde{e}(\hat{x}(k_i)) + \tilde{B}_i \tilde{e}_x(k) \right. \\
\left. + \tilde{M}_i \tilde{W}^T(k) \tilde{\sigma}(V^T \hat{x}(k_i)) + \tilde{A}_{di} \tilde{x}(k-d(k)) \right] = 0,
\end{aligned} \tag{37}$$

Applying the young's inequality, (36) and (37) can be derived as

$$2\tilde{x}^T(k) \left( \tilde{R}(\tilde{A}_i - \tilde{E}) + \tilde{R}\tilde{R}^T \right) \tilde{x}(k) + 2\tilde{x}^T(k) \tilde{R}\tilde{A}_{di} \tilde{x}(k - d(k)) - 2\tilde{x}^T(k) \tilde{R}\tilde{E}\tilde{\phi}(k) + 2 \times \tilde{x}^T(k) \tilde{R}\tilde{B}_i \tilde{e}_x(k) + \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{M}_i) \right\} \sigma_{\max}^2 \|\tilde{W}(k)\|_F^2 + \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{M}_i) \right\} \varepsilon_{\max}^2 \ge 0,$$

$$2(\tilde{E}\tilde{\phi}(k))^T Z_{im2}(\tilde{A}_i - \tilde{E})\tilde{x}(k) + 2(\tilde{E}\tilde{\phi}(k))^T Z_{im2}\tilde{A}_{di}\tilde{x}(k - d(k)) + 2(\tilde{E}\tilde{\phi}(k))^T Z_{im2}\tilde{B}_i\tilde{e}_x(k) + 2(\tilde{E}\tilde{\phi}(k))^T (Z_{im2}Z_{im2}^T - Z_{im2}) \tilde{E}\tilde{\phi}(k) + \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{M}_i) \right\} \sigma_{\max}^2 \|\tilde{W}(k)\|_F^2 + \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{M}_i) \right\} \varepsilon_{\max}^2 \ge 0.$$

Based on the above analysis, one has

$$\Delta V(\tilde{x}(k), \delta_k, \theta_k) \le \varepsilon^T(k) \tilde{\Omega}_{im} \varepsilon(k),$$

where

$$\begin{aligned} \tilde{\Omega}_{im} &= \begin{bmatrix} \tilde{\Omega}_{im}^1 & \tilde{\Omega}_{im}^2 \\ * & \tilde{\Omega}_{im}^3 \end{bmatrix}, \quad \tilde{\Omega}_{im}^1 = \begin{bmatrix} \tilde{\Xi}_{im11} & \tilde{R}\tilde{A}_{di} & 0 \\ * & \tilde{\Xi}_{im22} & 0 \\ * & * & -Q_1 \end{bmatrix}, \quad \tilde{\Omega}_{im}^2 = \begin{bmatrix} 0 & \tilde{\Xi}_{im15} & \tilde{R}\tilde{B}_i \\ 0 & \tilde{A}_{di}^T Z_{im2}^T & 0 \\ 0 & 0 & 0 \end{bmatrix}, \\ \tilde{\Omega}_{im}^3 &= \begin{bmatrix} -Q_2 & 0 & 0 \\ * & \Omega_{im11}^{22} & Z_{im2}\tilde{B}_i \\ * & * & \tilde{\Xi}_{im66} \end{bmatrix}, \quad \begin{aligned} \tilde{\Xi}_{im15} &= (\tilde{A}_i^T - \tilde{E}^T) Z_{im2}^T - \tilde{R} + Z_{im4} \tilde{S}^T, \\ \tilde{\Xi}_{im66} &= 8\tilde{B}_i^T \tilde{P}_{im} \tilde{B}_i - (1 - \beta + \frac{1}{\delta}) \theta_1 H_{im1}, \\ \tilde{\Xi}_{im22} &= 4\tilde{A}_{di}^T \tilde{P}_{im} \tilde{A}_{di} - Q_3, \end{aligned} \\ \tilde{\Xi}_{im11} &= -\tilde{E}^T P_{im} \tilde{E} + \tilde{R}(\tilde{A}_i - \tilde{E}) + (1 - \beta + \frac{1}{\delta}) \theta_2 H_{im2} + (\tilde{A}_i^T - \tilde{E}^T) \tilde{R}^T + 2\tilde{R}\tilde{R}^T + 2\tilde{A}_i^T \tilde{P}_{im} \tilde{A}_i \\ &+ (d+1)Q_3 + Q_1 + Q_2, \quad \varepsilon(k) = \left[ \tilde{x}^T(k), \tilde{x}^T(k - d(k)), \tilde{x}^T(k - d_1), \tilde{x}^T(k - d_2), (\tilde{E}\tilde{\phi}(k))^T, \tilde{e}_x^T(k) \right]^T. \end{aligned}$$

By Schur complement,  $\tilde{\Omega}_{im} < 0$  is equivalent to  $\hat{\Omega}_{im} + \Theta_{im1} \hat{G}_{ik} \Theta_{i2} + (\Theta_{im1} \hat{G}_{ik} \Theta_{i2})^T < 0$ , where

$$\begin{aligned} \hat{\Omega}_{im} &= \begin{bmatrix} \Omega_{im11} & \hat{\Omega}_{i12} \\ * & \hat{\Omega}_{im22} \end{bmatrix}, \quad \bar{G}_{ik} = \begin{bmatrix} G_{ik} & 0 \\ * & G_{ik} \end{bmatrix}, \quad \hat{G}_{ik} = \begin{bmatrix} \bar{G}_{ik} & 0 \\ * & \bar{G}_{ik} \end{bmatrix}, \\ \hat{\Omega}_{i12} &= \left[ \overline{\mathcal{D}}_{i11}^{21}, \overline{\mathcal{D}}_{i12}^{21}, \overline{\mathcal{D}}_{i13}^{21} \right], \quad \hat{\Omega}_{22} = \text{diag} \left\{ -\tilde{P}_{im}^{-1}, -\tilde{P}_{im}^{-1}, -\tilde{P}_{im}^{-1} \right\}, \\ \overline{\mathcal{D}}_{i11}^{21} &= \text{col} \left\{ \sqrt{2} \tilde{A}_i^T, 0, 0, 0, 0, 0 \right\}, \quad \overline{\mathcal{D}}_{i12}^{21} = \text{col} \left\{ 0, \sqrt{2} \tilde{A}_{di}^T, 0, 0, 0, 0 \right\}, \\ \overline{\mathcal{D}}_{i13}^{21} &= \text{col} \left\{ 0, 0, 0, 0, 0, 2\sqrt{2} \tilde{B}_i^T \right\}, \quad \Theta_{im1} = \left\{ \bar{\Theta}_{im11}, \bar{\Theta}_{im12} \right\}, \quad \Theta_{i2} = \text{col} \left\{ \bar{\Theta}_{i21}, \bar{\Theta}_{i22} \right\}, \\ \bar{\Theta}_{im11} &= \text{col} \left\{ \tilde{R}\tilde{S}_i, 0, 0, 0, Z_{im2}\tilde{S}_i, 0, (\sqrt{2} \tilde{S}_i)^T, 0, 0 \right\}, \quad \bar{\Theta}_{i21} = \text{col} \left\{ \bar{D}_i, 0, 0, 0, 0, 0, 0, 0, 0 \right\}, \\ \bar{\Theta}_{im12} &= \text{col} \left\{ \tilde{R}\tilde{S}_i, 0, 0, 0, Z_{im2}\tilde{S}_i, 0, 0, 2\tilde{S}_i, 0 \right\}, \quad \bar{\Theta}_{i22} = \text{col} \left\{ 0, \bar{D}_{di}, 0, 0, 0, 0, 0, 0, 0 \right\}. \end{aligned}$$

According to Lemma 2, if there exists a scalar  $\xi$  making  $\hat{\Omega}_{im} + \xi \Theta_{im1} \hat{G}_{ik} \Theta_{i2} + \xi^{-1} \Theta_{i2}^T \hat{G}_{ik}^T \Theta_{im1} < 0$ , then  $\hat{\Omega}_{im} + \Theta_{im1} \hat{G}_{ik} \Theta_{i2} + (\Theta_{im1} \hat{G}_{ik} \Theta_{i2})^T < 0$  holds.

Similarly,  $\hat{\Omega}_{im} + \xi \Theta_{im1} \hat{G}_{ik} \Theta_{i2} + \xi^{-1} \Theta_{i2}^T \hat{G}_{ik}^T \Theta_{im1} < 0$  is equivalent to

$$\tilde{\Omega}_{im} = \begin{bmatrix} \hat{\Omega}_{im} & \Theta_{i2}^T \\ * & -\xi I \\ * & * & -\xi I \end{bmatrix} < 0. \quad (38)$$

Obviously, (38) can be written as (11) for all  $i \in \Pi, m \in \Sigma$ . Likewise, using the Schur complement, (12), (13) and (14) ensure (39) for  $i \in \Pi, m \in \Sigma$ .

$$\left( 16 \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{P}_{im} \tilde{M}_i) \right\} + 2 \sup_{m \in \Sigma} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{M}_i) \right\} \right) \sigma_{\max}^2 - \nu \varphi < 0. \quad (39)$$

Therefore, sufficient conditions (11), (12), (13) and (14) can guarantee that

$$\begin{aligned} \Delta V &\le \inf_{i \in \Pi} \sup_{m \in \Sigma} \left\{ \lambda_{\max}(\Omega) \right\} \|\varepsilon(k)\|^2 + \zeta_M + \left( \left( 16 \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{P}_{im} \tilde{M}_i) \right\} \right. \right. \\ &+ 2 \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{M}_i) \right\} \left. \right) \sigma_{\max}^2 - \nu \varphi \left. \right\} \|\tilde{W}(k)\|_F^2, \end{aligned} \quad (40)$$

where

$$\zeta_M = \nu \zeta_W + \left( 16 \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{P}_{im} \tilde{M}_i) \right\} + 2 \sup_{i \in \Pi} \left\{ \lambda_{\max}(\tilde{M}_i^T \tilde{M}_i) \right\} \right) \varepsilon_{\max}^2.$$

According to the inequality (40), there exists a small constant  $\tau > 0$  meeting  $\Delta V \le -\tau V(k) + \zeta_M$ , which implies that discrete singular PHMJS (8) is bounded in probability. Then, the proof of Theorem 1 is finished.  $\square$

# Data availability

No data was used for the research described in the article.

# References

- [1] Zhang Y, Mu X. Event-triggered output quantized control of discrete Markovian singular systems. *Automatica* 2022;135:109992.
- [2] Cheng J, Xie L, Zhang D, Yan H. Novel event-triggered protocol to sliding mode control for singular semi-Markov jump systems. *Automatica* 2023;151:111096.
- [3] Zhang L, Zhao X, Zhao N. Real-time reachable set control for neutral singular Markov jump systems with mixed delays. *IEEE Trans Circuits Syst II Express Briefs* 2022;69(3):1367–71.
- [4] Xu S, Lam J. Robust control and filtering of singular systems. Berlin: Springer; 2006.
- [5] Zhuang G, Wang Z, Xie X, Xia J. Embedded-adaptive-observer-based  $H_\infty$  integrated fault estimation and memory fault-tolerant control for nonlinear delayed implicit robotic arm. *IEEE Trans Industr Inform* 2024;20(6):8317–27.
- [6] Hu J, Wang C, Caballero-Águila R, Liu H. Distributed optimal fusion filtering for singular systems with random transmission delays and packet dropout compensations. *Commun Nonlinear Sci Numer Simul* 2023;119:107093.
- [7] Jafari E, Binazadeh T. Robust output regulation in discrete-time singular systems with actuator saturation and uncertainties. *IEEE Trans Circuits Syst II Express Briefs* 2020;67(2):340–4.
- [8] Zhang L. H<sub>∞</sub> estimation for discrete-time piecewise homogeneous Markov jump linear systems. *Automatica* 2009;45(11):2570–6.
- [9] Gao X, Deng F, Zeng P, Zhang H. Adaptive neural event-triggered control of networked Markov jump systems under hybrid cyberattacks. *IEEE Trans Neural Netw Learn Syst* 2023;34(3):1502–12.
- [10] Lam J, Shu Z, Xu S, Boukas E. Robust control of descriptor discrete-time Markovian jump systems. *Internat J Control* 2007;80(3):374–85.
- [11] Chavez-Fuentes J, Costa E, Terra M, Rocha K. The linear quadratic optimal control problem for discrete-time Markov jump linear singular systems. *Automatica* 2021;127:109506.
- [12] Han Y, Kao Y, Gao C. Robust sliding mode control for uncertain discrete singular systems with time-varying delays and external disturbances. *Automatica* 2017;75:210–6.
- [13] Wang J, Zhuang G, Xia J, Chen G, Zhao J. Asynchronous dissipative control and robust exponential mean square stabilization for uncertain fuzzy neutral Markov jump systems. *J Syst Sci Complex* 2022;35(4):1374–97.
- [14] Kao Y, Han Y, Zhu Y, Shu Z. Stability analysis of delayed discrete singular piecewise homogeneous Markovian jump systems with unknown transition probabilities via sliding-mode approach. *IEEE Trans Autom Control* 2024;69(1):315–22.
- [15] Tian Y, Yan H, Zhang H, Wang M, Yi J. Time-varying gain controller synthesis of piecewise homogeneous semi-Markov jump linear systems. *Automatica* 2022;146:110594.
- [16] Wang L, Wu Z, Shen Y. Asynchronous mean stabilization of positive jump systems with piecewise-homogeneous Markov chain. *IEEE Trans Circuits Syst II Express Briefs* 2021;68(10):3266–70.
- [17] Men Y, Sun J. Output feedback control of piecewise homogeneous semi-Markov jump systems. *IEEE Trans Circuits Syst II* 2023;70(2):546–50.
- [18] Xiao M, Chen S, Zheng W, Wang Z, Lu Y. Tipping point prediction and mechanism analysis of malware spreading in cyber-physical systems. *Commun Nonlinear Sci Numer Simul* 2023;122:107247.
- [19] Yan S, Gu Z, Park J. Lyapunov-function-based event-triggered control of nonlinear discrete-time cyber-physical systems. *IEEE Trans Circuits Syst II Express Briefs* 2022;69(6):2817–21.
- [20] Ji Y, Gao Q, Liu J. Adaptive resilient control for cyber-physical systems against unknown injection attacks in sensor networks. *Nonlinear Dynam* 2023;111(12):11105–14.
- [21] Shao X, Ye D. Neural-network-based adaptive secure control for nonstrict-feedback nonlinear interconnected systems under DoS attacks. *Neurocomputing* 2021;448:263–75.
- [22] Zhuang G, Zhu Q, Xie X, Xia J. Event-based  $H_\infty$  fuzzy control for implicit hybrid AVS systems embedding acceleration characteristic under random deception and DoS attacks. *IEEE Trans Autom Sci Eng* <http://dx.doi.org/10.1109/TASE.2024.3439705>.
- [23] Gao Z, Zhao N, Zhao X, Niu B, Xu N. Event-triggered prescribed performance adaptive secure control for nonlinear cyber physical systems under denial-of-service attacks. *Commun Nonlinear Sci Numer Simul* 2024;131:107793.
- [24] Cuan Z, Ding D, Yang Y, Xia Y. Adaptive neural network finite-time control for nonlinear cyber-physical systems with external disturbances under malicious attacks. *Neurocomputing* 2023;518:133–41.
- [25] Liu X, Chen L, Zhao Y, Li H. Event-triggered hybrid impulsive control for synchronization of fractional-order multilayer signed networks under cyber attacks. *Neural Netw* 2024;172:106124.
- [26] Tian E, Peng C. Memory-based event-triggering  $H_\infty$  load frequency control for power systems under deception attacks. *IEEE Trans Cybern* 2020;50(11):4610–8.
- [27] Zhang T, Ye D. False data injection attacks with complete stealthiness in cyber-physical systems: A self-generated approach. *Automatica* 2020;120:109117.
- [28] Zhao N, Zhao D, Liu Y. Resilient event-triggering adaptive neural network control for networked systems under mixed cyber attacks. *Neural Netw* 2024;174:106249.
- [29] Tyukin I, Higham D, Bastounis A, Woldegeorgis E, Gorban A. The feasibility and inevitability of stealth attacks. *IMA J Appl Math* 2024;89(1):44–84.
- [30] Tyukin I, Prokhorov D, Terekhov V. Adaptive control with nonconvex parameterization. *IEEE Trans Autom Control* 2003;48(4):554–67.
- [31] Tyukin I, Gorban A, Green S, Prokhorov D. Fast construction of correcting ensembles for legacy artificial intelligence systems: Algorithms and a case study. *Inform Sci* 2019;485:230–47.
- [32] Xiao S, Han Q, Ge X, Zhang Y. Secure distributed finite-time filtering for positive systems over sensor networks under deception attacks. *IEEE Trans Cybern* 2020;50(3):1220–9.
- [33] Chao Z, Wang C, Yao W. Quasi-synchronization of stochastic memristive neural networks subject to deception attacks. *Nonlinear Dynam* 2023;111(3):2443–62.
- [34] Si X, Wang Z, Huang X, Fan Y, Shen H. Resilient-sampling-based bipartite synchronization of cooperative-antagonistic neural networks with hybrid attacks: designing interval-dependent functions. *IEEE Trans Autom Sci Eng* 2024. <http://dx.doi.org/10.1109/TASE.2024.3386699>.

- [35] Zhuang G, Sun W, Su S, Xia J. Asynchronous feedback control for delayed fuzzy degenerate jump systems under observer-based event-driven characteristic. *IEEE Trans Fuzzy Syst* 2021;29(12):3754–68.
- [36] Peng C, Li F. A survey on recent advances in event-triggered communication and control. *Inform Sci* 2018;457:113–25.
- [37] Yao W, Wang C, Sun Y, Gong S, Lin H. Event-triggered control for robust exponential synchronization of inertial memristive neural networks under parameter disturbance. *Neural Netw* 2023;164:67–80.
- [38] Yao L, Huang X, Wang Z, Liu K. Secure control of markovian jumping systems under deception attacks: An attack-probability-dependent adaptive event-triggered mechanism. *IEEE Trans Control Netw Syst* 2023;10(4):1818–30.
- [39] Mu C, Wang K, Ni Z. Adaptive learning and sampled-control for nonlinear game systems using dynamic event-triggering strategy. *IEEE Trans Neural Netw Learn Syst* 2022;33(9):4437–50.
- [40] Sahoo A, Xu H, Jagannathan S. Adaptive neural network-based event-triggered control of single-input single-output nonlinear discrete-time systems. *IEEE Trans Neural Netw Learn Syst* 2016;27(1):151–64.
- [41] Bansal K, Mukhija P. Aperiodic sampled-data control of distributed networked control systems under stochastic cyber-attacks. *IEEE/CAA J Autom Sin* 2020;7(4):1064–73.