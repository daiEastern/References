

# Enhanced intelligent proportional-integral-like fuzzy knowledge-based controller using chaos-enhanced accelerated particle swarm optimization algorithm for transient calibration of air-fuel ratio control system

Proc IMechE Part D:

J Automobile Engineering

1–17

© IMechE 2019

Article reuse guidelines:

sagepub.com/journals-permissions

DOI: 10.1177/0954407019862079

journals.sagepub.com/home/pid

![SAGE logo](b4eeff342f60cc7bcd67d869b4fedca2_img.jpg) SAGEZiyang Li<sup>1D</sup>, Quan Zhou, Yunfan Zhang, Ji Li and Hongming Xu

## Abstract

The self-adaptive and highly robust proportional-integral-like fuzzy knowledge-based controller has been developed to regulate air-fuel ratio for gasoline direct injection engines, in order to improve the transient response behaviour and reduce the effort to be spent on calibration of parameter settings. However, even though the proportional-integral-like fuzzy knowledge-based controller can automatically correct the initially calibrated proportional and integral parameters, a more appropriate selection of controller parameter settings will lead to better transient performance. Thus, this article proposes an enhanced intelligent proportional-integral-like fuzzy knowledge-based controller using chaos-enhanced accelerated particle swarm optimization algorithm to automatically define the most optimal parameter settings. An alternative time-domain objective function is applied for the transient calibration programme without the need for prior selection of the search-domain. The real-time transient performance of the enhanced controller is investigated on the air-fuel ratio control system of a gasoline direct injection engine. The experimental results show that the enhanced proportional-integral-like fuzzy knowledge-based controller based on chaos-enhanced accelerated particle swarm optimization is able to damp out the oscillations with less settling time (up to 75% reduction) and less integral of absolute error (up to 64.07% reduction) compared with the conventional self-adaptive proportional-integral-like fuzzy knowledge-based controller. Repeatability tests indicate that the chaos-enhanced accelerated particle swarm optimization algorithm-based proportional-integral-like fuzzy knowledge-based controller is also able to reduce the mean value of objective function by up to 10.61% reduction and the standard deviation of the objective function by up to 28.29% reduction, compared with the conventional accelerated particle swarm optimization algorithm-based proportional-integral-like fuzzy knowledge-based controller.

## Keywords

Gasoline direct injection engine, fuzzy control, air-fuel ratio, multiple-objective optimization, particle swarm algorithm, transient calibration

Date received: 24 October 2018; accepted: 13 March 2019

## Introduction

For the further development of modern gasoline engines, reductions of pollutant emission and fuel consumption are always the main objectives. However, both objectives depend extremely on the precise control of air-fuel ratio (AFR) within a narrow range around the stoichiometric value (14.7).<sup>1–5</sup> The fuel economy, catalyst efficiency and system security will degrade if

---

School of Engineering, The University of Birmingham, Birmingham, UK

###### Corresponding author:

Hongming Xu, School of Engineering, The University of Birmingham, Edgbaston, Birmingham B15 2TT, UK.

Email: h.m.xu@bham.ac.uk

the AFR deviates from stoichiometric value for a long time.<sup>6–8</sup>

To achieve the precise AFR regulation, the fuel injection system is comprised of both feedforward and feedback control loops. The feedforward control loop generates the basic portion of how much fuel should be injected in cylinder for the stoichiometry based on the in-cylinder air mass flow. However, even though many researchers have studied on feedforward control loop through Model Predictive Control (MPC) and neural network, there is still a significant gap that has to be compensated by the feedback control loop based on the exhaust gas oxygen (EGO) sensor installed in the exhaust manifold.<sup>9,10</sup> Besides, MPC control and neural network always require lots of training to optimize the model. Therefore, a feedback control strategy that can handle a wider range of operation conditions and non-model-based dynamics becomes the key to develop the efficient AFR control systems.

In recent years, robust controllers have attracted the attention of researchers to cope with modelling uncertainties, such as the  $H_\infty$  optimized controllers which have shown outstanding robustness.<sup>11–13</sup> However, these robust controllers are still model-based controllers. In other words, to design the controller, an accurate model of the system has to be essential. Therefore, the ‘model-free’ controllers such as fuzzy controllers have been brought into the spotlight. These fuzzy controllers have simple structures, imitate human behaviours, follow the generic ‘if-then’ rules and stay independent of the system structures. They can work efficiently when an accurate model is not available.<sup>14–16</sup> This year, a proportional-integral (PI)-like fuzzy knowledge-based controller (FKBC) has been developed to replace the conventional look-up table-based PI controller for the AFR control of gasoline direct injection (GDI) engines.<sup>17</sup> The proportional and integral terms of the PI-like FKBC are self-tuned in real time and do not rely on constant calibrated values, so that the PI-like FKBC can work efficiently with even poor proportional and integral gains and save the effort to be spent for calibration. The experimental results show that the proposed PI-like FKBC can lead to better transient response behaviour to damp out the oscillations for various operating points, compared with the conventional look-up table-based PI controller. However, more appropriate selection of the initial controller parameter settings will definitely lead to better transient performance. Accordingly, an enhanced PI-like FKBC is supposed to be developed based on automatic transient optimization process which can still save the effort for calibration and offer the most optimal parameter settings as well. Thanks to the development of non-model-based calibration<sup>18</sup> and Rapid Control Prototyping (RCP) technology, an enhanced self-calibrating PI-like FKBC based on rapid and automatic optimization process is developed in this article.

Global optimization algorithms are widely used to resolve nonlinear optimization problems, because they are able to find globally optimal results instead of resulting in multiple locally optimal results.<sup>18–21</sup> Meta-heuristic algorithm is one of the most well-known global optimization methods.<sup>22,23</sup> And swarm intelligence algorithm, such as particle swarm optimization (PSO) algorithm, is one of the main categories of meta-heuristic algorithm. Comparing with other meta-heuristic algorithms such as genetic algorithm and population-based algorithm, the swarm intelligence algorithm is famous for its capabilities as easy implementation, high computational efficiency and fast convergence speed.<sup>24–26</sup> In recent years, accelerated particle swarm optimization (APSO) algorithm is proposed to increase the convergence speed for multi-objective optimization problems.<sup>27,28</sup> Then, an APSO algorithm combined with chaos theory, that is, chaos-enhanced accelerated particle swarm optimization (CAPSO) algorithm, has been developed to improve the randomization and diversification of the solutions, which allows the optimizer to explore the searching space more efficiently and avoid falling into the traps of locally optimal results.<sup>29,30</sup> Many researchers have validated that the CAPSO algorithm performs much better than the conventional PSO algorithm.<sup>24,25,31</sup>

In terms of the swarm intelligence algorithm, the studies show that its performance highly depends on the selection of search-domain and objective function. For most of the algorithm-based optimization problems, a prior knowledge about the search-domain is essential. Otherwise, the optimizer may converge to improper solutions, which may lead to extremely large overshoot of the control signal or cost unpredictably long time to converge.<sup>32</sup> To reduce the impact of different search-domains, an alternative objective function is presented in this article. The simulation results show that the optimizer with proposed objective function can converge to similar optimal results regardless of the size of search-domain. Eventually, this alternative objective function is used to design the enhanced PI-like FKBC for the AFR control system. The controller is built by MATLAB/Simulink and cooperates with ETAS RCP facilities for real-time implementation. The transient performance of the enhanced PI-like FKBC is investigated on a production GDI engine via various operating conditions.

This article is organized as follows: the structure of the PI-like FKBC is presented in the ‘Structure of the PI-like FKBC’ section. A review for the algorithms implemented in this article is given in ‘The optimization algorithm’ section. The ‘Choice of objective functions’ section analyses the impact of various objective functions on time-domain optimization problems. Then, an alternative objective function is applied and validated by simulation studies. Experimental setup is described in the section ‘Experimental setup’ with the

![Figure 1: Structure of the PI-like FKBC. The diagram shows a control loop. The reference signal λ_ref and the system feedback signal λ are compared in a summing junction. The error signal e(k) = λ_ref(k) - λ(k) is scaled by K_i and passed to a Fuzzy Logic Module. The error signal is also passed through a 1/Z block (integrator) and scaled by K_p to the Fuzzy Logic Module. The Fuzzy Logic Module contains a Fuzzification block with inputs e * K_i and Δe * K_p, 'if-then' rules, and a Defuzzification block outputting Δu. The scaled output Δu is multiplied by K_u. The result is added to the feedback signal λ through a 1/Z block to produce the final control signal u_fb. This signal is fed back to the system and also to an 'Engine' block.](69edc2887e907309499ac95b47ab6905_img.jpg)

Figure 1: Structure of the PI-like FKBC. The diagram shows a control loop. The reference signal λ\_ref and the system feedback signal λ are compared in a summing junction. The error signal e(k) = λ\_ref(k) - λ(k) is scaled by K\_i and passed to a Fuzzy Logic Module. The error signal is also passed through a 1/Z block (integrator) and scaled by K\_p to the Fuzzy Logic Module. The Fuzzy Logic Module contains a Fuzzification block with inputs e \* K\_i and Δe \* K\_p, 'if-then' rules, and a Defuzzification block outputting Δu. The scaled output Δu is multiplied by K\_u. The result is added to the feedback signal λ through a 1/Z block to produce the final control signal u\_fb. This signal is fed back to the system and also to an 'Engine' block.

**Figure 1.** Structure of the PI-like FKBC.  
FKBC: fuzzy knowledge-based controller.

experimental procedures. Experimental results and discussions are listed in the section ‘Experimental results and discussion’. Conclusions are drawn in the final section.

## Structure of the PI-like FKBC

Since the enhanced PI-like FKBC in this article is improved based on the PI-like FKBC in literature,<sup>17</sup> details of the controller shown in Figure 1 can be found in the literature.<sup>17</sup> A brief introduction for the structure of PI-like FKBC is listed in this section.

Basically, the PI-like FKBC in Figure 1 is designed based on the equation

$$\left\{ \begin{array}{l} u_{fb}(k) = u(k) = u(k-1) + K_u \Delta u(k) \\ \Delta u(k) = [X_1(k), X_2(k)] = [K_i e(k), K_p \Delta e(k)] \\ e(k) = \lambda_{ref}(k) - \lambda(k) \\ \Delta e(k) = \frac{e(k) - e(k-1)}{T} \end{array} \right. \quad (1)$$

where  $e(k)$  is the error between the target value  $\lambda_{ref}(k)$  and the system feedback signal  $\lambda(k)$ . The PI-like FKBC employs two input signals,  $X_1(k)$  and  $X_2(k)$ .  $X_1(k)$  is the error signal  $e(k)$  multiplied by integral scaling factor  $K_i$  and  $X_2(k)$  is the rate of change of error signal  $\Delta e(k)$  multiplied by proportional scaling factor  $K_p$ . Meanwhile,  $\Delta u(k)$  is defined as the single output incremental signal, which is the function in  $[X_1(k), X_2(k)]$ .

The Sugeno-type fuzzy controller is used in this article as its processing speed is much faster than the speed of Mamdani-type fuzzy controller.<sup>32</sup> The output value of Sugeno-type fuzzy controller is transformed to a

![Figure 2: Distribution of the input membership function. The graph shows seven triangular membership functions (NB, NM, NS, Z, PS, PM, PB) plotted against input values from -1.00 to 1.00. The functions are centered at -1.00, -0.67, -0.33, 0.00, 0.33, 0.67, and 1.00 respectively.](50dae0dfbde108cee0040a29f2a42e88_img.jpg)

Figure 2: Distribution of the input membership function. The graph shows seven triangular membership functions (NB, NM, NS, Z, PS, PM, PB) plotted against input values from -1.00 to 1.00. The functions are centered at -1.00, -0.67, -0.33, 0.00, 0.33, 0.67, and 1.00 respectively.

**Figure 2.** Distribution of the input membership function.  
NB: Negative Big; NM: Negative Medium; NS: Negative Small; Z: Zero;  
PS: Positive Small; PM: Positive Medium; PB: Positive Big.

constant value directly by fuzzy rules without the need to calculate the weighted average of output membership functions, which allows the Sugeno-type fuzzy controller to perform more efficiently for real-time implementation.

Figures 2 and 3 give the simplest membership functions for input and output signals of the Sugeno-type fuzzy controller which are defined over  $[-1, 1]$  and occurred at points  $-1.00, -0.65, -0.33, 0.00, 0.33, 0.65$  and  $1.00$ . Fuzzy set of rules is shown in Table 1. Seven fuzzy sets are applied as follows: NB: Negative Big; NM: Negative Medium; NS: Negative Small; Z: Zero; PS: Positive Small; PM: Positive Medium; and PB: Positive Big.

First of all, input signals  $X_1(k)$  and  $X_2(k)$  are normalized by scaling them with  $K_i$  and  $K_p$ , respectively. Then, a set of fuzzy decision rules relating inputs to the output are constructed as Table 1 shows. The rule in column 4 and row 2 can be explained as, if the input  $X_1(k)$  is a

![Figure 3: Distribution of the output membership function. A graph showing eight triangular membership functions (NB, NM, NS, Z, PS, PM, PB) on a scale from -1.00 to +1.00. The functions are centered at -1.00, -0.67, -0.33, 0, +0.33, +0.67, and +1.00 respectively.](f961cbef0f8217e216b553bed270315b_img.jpg)

Figure 3: Distribution of the output membership function. A graph showing eight triangular membership functions (NB, NM, NS, Z, PS, PM, PB) on a scale from -1.00 to +1.00. The functions are centered at -1.00, -0.67, -0.33, 0, +0.33, +0.67, and +1.00 respectively.

**Figure 3.** Distribution of the output membership function.  
NB: Negative Big; NM: Negative Medium; NS: Negative Small; Z: Zero;  
PS: Positive Small; PM: Positive Medium; PB: Positive Big.

**Table 1.** Fuzzy associative rules for the controller.

| X2 | X1 |    |    |    |    |    |    |    |
|----|----|----|----|----|----|----|----|----|
|    |    | NB | NM | NS | Z  | PS | PM | PB |
| NB | PB | PB | PB | PM | PS | PS | Z  |    |
| NM | PB | PB | PM | PS | PS | Z  | NS |    |
| NS | PB | PM | PS | PS | Z  | NS | NS |    |
| Z  | PM | PS | PS | Z  | NS | NS | NM |    |
| PS | PS | PS | Z  | NS | NS | NM | NB |    |
| PM | PS | Z  | NS | NS | NM | NB | NB |    |
| PB | Z  | NS | NS | NM | NB | NB | NB |    |

NB: Negative Big; NM: Negative Medium; NS: Negative Small; Z: Zero;  
PS: Positive Small; PM: Positive Medium; PB: Positive Big.

member of the zero and the input  $X_2(k)$  is a member of the negative medium, then the output signal  $\Delta u_{PI}(k)$  is defined as positive small, that is, +0.33. At last, the output signal  $\Delta u_{PI}(k)$  is scaled with  $K_u$  and transformed to the feedback control signal  $u_{fb}(k)$  as equation (1) shows.

Compared with the conventional look-up table-based PI controller, the scaling terms of PI-like FKBC are nonlinear functions of the gap between stoichiometric and actual AFRs. They are self-tuned in real time based on the change of the gap between stoichiometric and actual AFRs instead of being constant. However, the transient performance of PI-like FKBC is extremely related to the scaling factors  $K_p, K_i, K_u$  which should better be optimized.

## The optimization algorithm

More and more meta-heuristic optimization algorithms have been applied to deal with engineering problems. Each of them has its own advantages. However, as the ‘no free lunch’ theorem said, it is impossible to discover a best algorithm to resolve all kinds of optimization problems.<sup>33</sup> Accordingly, CAPSO algorithm is selected in this article to optimize the scaling factors of PI-like FKBC.

PSO algorithm is inspired from the sociological movement behaviour associated with bird and fish flocking.<sup>34</sup> As the most advanced algorithm of evolutionary PSO algorithms, CAPSO algorithm is modified

![Figure 4: Workflow of the CAPSO algorithm. A flowchart showing the main interaction module and the optimal position retrieve module. The main module includes setup, particle generation, and iteration loops. The retrieve module scales parameters, runs the engine, and stores results.](8d3afc46f415cad96c2eba639730f7c3_img.jpg)

```

graph TD
    subgraph InitialSettings [Initial settings]
        direction TB
        P[Set the amount of particles P]
        N[Set the amount of interactions N]
        B[Set boundary conditions]
    end

    subgraph MainInteractionModule [The main interaction module]
        direction TB
        StartCase{Start of the case}
        Setup[Algorithm setup]
        Generate[Generate the initial particles]
        StartI0((Start interaction, i=0))
        Ii1{i=i+1}
        Retrieve[Retrieve the minimum cost function value and the best positions of the particles]
        Move[Move the particles to new positions]
        Update[Update the global best position]
        EndI{End of the interaction}
        Output[Output the best solutions of the parameter settings]
        EndA[End of the algorithm]
    end

    subgraph OptimalPositionRetrieveModule [Optimal position retrieve module]
        direction TB
        StartJ0((Start interaction, j=0))
        Jj1{j=j+1}
        Scale[Scale the controller parameters with particles]
        Run[Run the engine and calculate the cost function value]
        Store[Store the cost function value and particles]
        EndJ{End of the interaction}
    end

    StartCase --> Setup
    Setup --> Generate
    Generate --> StartI0
    StartI0 --> Ii1
    Ii1 --> Retrieve
    Retrieve --> Move
    Move --> Update
    Update --> Ii1
    Ii1 --> EndI
    EndI --> Output
    Output --> EndA

    StartI0 --> StartJ0
    StartJ0 --> Jj1
    Jj1 --> Scale
    Scale --> Run
    Run --> Store
    Store --> Jj1
    Jj1 --> EndJ
    EndJ --> MainInteractionModule
    MainInteractionModule --> OptimalPositionRetrieveModule
    OptimalPositionRetrieveModule --> MainInteractionModule

```

Figure 4: Workflow of the CAPSO algorithm. A flowchart showing the main interaction module and the optimal position retrieve module. The main module includes setup, particle generation, and iteration loops. The retrieve module scales parameters, runs the engine, and stores results.

**Figure 4.** Workflow of the CAPSO algorithm.  
CAPSO: chaos-enhanced accelerated particle swarm optimization.

from the APSO algorithm. Figure 4 shows the workflow of the CAPSO algorithm.

Generally, the CAPSO algorithm consists of three stages. First of all, initial settings have to be defined, including the number of particles in each swarm, the number of iterations and the boundary conditions for the search-domains. The particles start from initial positions which are generated randomly based on the range of search-domains. Then, the iteration process begins. The value of cost function for each particle is obtained by the real-time measurement. The current locally optimal results corresponding to the most satisfying cost function value will be stored. Afterwards, the position of each particle will be updated at the end of each iteration according to three indicators, that is, the current position of particle, the best position in the swarm and a random factor. The iteration process is

repeated until the pre-set number of iterations or boundary conditions are reached. The final optimal solutions will be obtained from the optimal results of the last iteration.

In this article, each particle's position is defined as

$$x^{(i,j)} = [K_p^{(i,j)}, K_i^{(i,j)}, K_u^{(i,j)}] \quad (2)$$

where  $i = [1, 2, 3, \dots, N]$  is the index of iterations,  $N$  is the number of iterations;  $j = [1, 2, 3, \dots, M]$  is the index of particles in each swarm,  $M$  is the number of particles in each swarm.  $K_p^{(i,j)}, K_i^{(i,j)}, K_u^{(i,j)}$  are the scaling factors  $K_p, K_i, K_u$  of the PI-like FKBC for  $i$ th iteration and  $j$ th particle.

The position of each particle is evolved based on the following equation

$$x^{(i+1,j)} = x^{(i,j)} + \beta(g^{(i,*)} - x^{(i,j)}) + \alpha^{(i)} \cdot r^{(i,j)} \quad (3)$$

where  $g^{(i,*)}$  indicates the current best position at  $i$ th iteration,  $\beta$  represents the attraction parameter of CAPSO algorithm. Here the randomization term  $\alpha^{(i)} \cdot r^{(i,j)}$  provides the ability for the system to escape from any locally optimum results.  $r^{(i,j)}$  is a random movement within the search-domain for the particle;  $\alpha^{(i)}$  indicates the randomness parameter that would be updated at each iteration. An improvement of the CAPSO algorithm is to reduce the randomness as iterations proceed. This means that a monotonically decreasing function can be used for  $\alpha^{(i)}$

$$\alpha^{(i)} = \alpha^{(0)} \cdot \gamma^i \quad (4)$$

Gandomia et al.<sup>30</sup> and Yang<sup>35</sup> have explained that  $\alpha^{(0)} \in [0.5, 1]$  as the initial value of the randomness parameter and  $\gamma \in [0, 1]$  as the control parameter.  $\gamma$  is usually taken as 0.7–0.9 for standard CAPSO cases. A larger  $\alpha^{(0)}$  is able to achieve a larger  $\alpha^{(i)}$  in order to escape from the locally optimum results effectively. Based on authors' repeatability studies and previous works,<sup>24,25</sup>  $\alpha^{(0)} = 0.9$  and  $\gamma = 0.8$  are selected in this article.

As the attraction parameter,  $\beta \in [0, 1]$  is used to adjust the convergence speed. For  $\beta = 0$ , the particles will move and update very slowly. Whereas, for  $\beta = 1$ , the particles will converge directly to the current locally best positions even though they are not the globally optimum results. The conventional APSO algorithm sets  $\beta = 0.5$  as a constant value because some studies have verified that it could allow algorithm to work effectively. However, a variable  $\beta$  value in each iteration could achieve the trade-off between convergence speed and diversification (to avoid being stuck in locally optimum results). Therefore, the CAPSO algorithm employs chaotic mapping strategy to adjust  $\beta$  value after each iteration. In this article, the logistic mapping strategy is applied as chaotic mapping strategy. The  $\beta$  value is updated following the equation

$$\beta^{(i+1)} = \alpha \cdot \beta^{(i)} \cdot (1 - \beta^{(i)}) \quad (5)$$

Based on authors' previous researches,<sup>24,25</sup>  $\alpha$  and initial  $\beta^{(1)}$  are set as  $\alpha = 4$  and  $\beta^{(1)} = 0.7$ , respectively, to highly improve the randomization for the generated particles.

## Choice of objective functions

To design the CAPSO algorithm-based optimizer, the proper search-domain and objective function have to be identified first. On one hand, as the following example shows, different search-domains with the same objective function will lead to totally different transient response behaviours. On the other hand, a wider search-domain may result in more optimal solutions, but lead to larger overshoot of the control signal and more time consumption. Accordingly, an alternative objective function is employed in this article to reduce the impact of different search-domains. As for the objective function, the integral of absolute error (IAE) is one of the most widely used objective functions for the time-domain optimization, since a good PI-like FKBC should minimize the oscillation of the system transient response with less settling time and less overshoot.

To present how the selection of search-domain and objective function will affect the calibration results, this article supposes that a PI-like FKBC is to be designed for a time-varying discrete system as equation (6) shows. The CAPSO algorithm is supposed to look for the optimal scaling factors  $K_p, K_i$  and  $K_u$  of the PI-like FKBC for the following system

$$\begin{cases} \dot{x}_1(t_n) = x_2(t_n) \\ \dot{x}_2(t_n) = -e^{-0.2t_n}x_2(t_n) - e^{-5t_n}\sin(2t_n + 6)x_1(t_n) + u(t_n) \\ t_n = 0, T, 2T, 3T, \dots, nT (T = 0.01\text{ s}) \end{cases} \quad (6)$$

where  $u$  is the control signal and  $x_1$  is the response signal.

Given that the improper calibration results may result in excessively large overshoot of the control signal, the control signal is constrained within a larger range  $[-1000, 1000]$ . The step change of the system is defined as 0 to 1 at the beginning of the running, thus the constraint for the response signal is set as  $[0, 2]$ .

First, IAE is employed as the only objective. The CAPSO algorithm is implemented several times with different search-domains,  $[0, 10]$ ,  $[0, 100]$  and  $[0, 1000]$ . The optimal results for  $K_p, K_i$  and  $K_u$  as well as the transient performance of the system are listed in Table 2 and Figure 5.

As can be seen from the results, the range of search-domain can affect the final optimal solution effectively. Even though all of these optimal scaling factors can reduce the oscillation of the system, search-domain  $[0, 10]$  costs more settling time whereas search-domain  $[0, 1000]$  leads to excessively large overshoot of the control signal. Thus, unless there is sufficient and accurate prior information for the selection of search-domain,

![Figure 5: Step response of the system based on different ranges of search-domains with IAE as the objective. The figure consists of two main plots. The top plot shows the 'Response' (y-axis, 0 to 1.2) versus 'Time(s)' (x-axis, 0 to 5). It contains three curves: a solid blue line for Search-domain [0, 10], a dashed red line for [0, 100], and a dotted black line for [0, 1000]. The bottom plot shows the 'Control signal' (y-axis, -100 to 600) versus 'Time(s)' (x-axis, 0 to 5). It also contains three curves corresponding to the same search-domains. Two zoomed-in insets are shown: the top-left inset zooms in on the initial transient of the control signal for the [0, 1000] search-domain, and the top-right inset zooms in on the steady-state response of the control signal for the [0, 10] and [0, 100] search-domains.](46f43cb4ffd47565e7c0ca306d461435_img.jpg)

Figure 5: Step response of the system based on different ranges of search-domains with IAE as the objective. The figure consists of two main plots. The top plot shows the 'Response' (y-axis, 0 to 1.2) versus 'Time(s)' (x-axis, 0 to 5). It contains three curves: a solid blue line for Search-domain [0, 10], a dashed red line for [0, 100], and a dotted black line for [0, 1000]. The bottom plot shows the 'Control signal' (y-axis, -100 to 600) versus 'Time(s)' (x-axis, 0 to 5). It also contains three curves corresponding to the same search-domains. Two zoomed-in insets are shown: the top-left inset zooms in on the initial transient of the control signal for the [0, 1000] search-domain, and the top-right inset zooms in on the steady-state response of the control signal for the [0, 10] and [0, 100] search-domains.

**Figure 5.** Step response of the system based on different ranges of search-domains with IAE as the objective.

IAE: integral of absolute error.

**Table 2.** Optimal scaling factors based on different ranges of search-domains with IAE as the objective.

| Objective | Search-domain | $K_p$  | $K_i$  | $K_u$  | Settling time (s) | Overshoot of control signal |
|-----------|---------------|--------|--------|--------|-------------------|-----------------------------|
| IAE       | [0, 10]       | 2.95   | 1.00   | 8.98   | 2.31              | 8.97                        |
| IAE       | [0, 100]      | 5.05   | 1.01   | 33.44  | 1.19              | 33.01                       |
| IAE       | [0, 1000]     | 165.16 | 167.49 | 892.54 | 1.08              | 537.25                      |

IAE: integral of absolute error.

the conventional IAE objective function may lead to improper performance of the control signal and actuator saturation.

To reduce the impact by the range of search-domain, the magnitude of the control signal is considered as another objective function. Next case combines the magnitude of the control signal with the IAE as objectives in order to achieve relatively similar optimization results. Hence, the calibration task is formulated into a multi-objective optimization problem with the objective function below

$$\left\{ \begin{array}{l} \min_{K_p, K_i, K_u} J = \text{minimize}(IAE + IAU) = \text{minimize} \\ \left( \sum_{k=1}^{n} R \cdot T \cdot |e(k)| + \sum_{k=1}^{n} Q \cdot T \cdot |u(k)| \right) \\ 0 \le R < 1, 0 < Q \le 1, R + Q = 1 \end{array} \right. \quad (7)$$

where  $e(k)$  is the error between target value and actually measured value;  $u(k)$  is the value of real-time control signal. Both of them are discrete time signals.  $R$  and  $Q$  are the weighting factors on the error and the control signal, respectively. The magnitude of the control signal

is indicated by the integral of absolute control signal (IAU).

The step response of system based on different ranges of search-domains with IAE and IAU as objectives is shown in Figure 6. The optimization results are listed in Table 3. As the figure shows, relatively similar step responses can be obtained regardless of the ranges of search-domains. Even though the settling time becomes a little bit longer, the overshoot of control signal is reduced effectively. Search-domains [0, 10] and [0, 100] achieve similar performances while [0, 10] leads to better trade-off between the settling time and the overshoot of control signal.

To present how the different  $R$  and  $Q$  affect the step response, several cases with search-domain [0, 10] are tested and shown in Figure 7. Meanwhile, the optimum scaling factors are listed in Table 4.

$R$  and  $Q$  can be adjusted by users to achieve desirable trade-off between reducing the settling time and avoiding the extremely large control signal. In this article, the values of  $R$  and  $Q$  are both assigned as 0.5.

Considering that there may be a huge gap between the magnitudes of IAE and IAU in the practical

![Figure 6: Step response of the system based on different ranges of search-domains with IAE and IAU as objectives. The figure consists of two subplots. The top subplot shows the 'Response' (y-axis, 0 to 1.2) versus 'Time(s)' (x-axis, 0 to 10). It contains three curves: a solid blue line for Search-domain [0, 10], a dashed red line for [0, 100], and a dotted black line for [0, 1000]. The bottom subplot shows the 'Control signal' (y-axis, 0 to 100) versus 'Time(s)' (x-axis, 0 to 10). It also contains three curves: a solid blue line for [0, 10], a dashed red line for [0, 100], and a dotted black line for [0, 1000]. Two insets are shown: the top-left inset shows a zoomed-in view of the control signal for the [0, 1000] search domain, and the bottom-right inset shows a zoomed-in view of the response for the [0, 10] search domain. The legend in the top subplot provides the optimal parameters for each search domain: Search-domain [0, 10], Kp=2.82, Ki=2.47, Ku=7.39; Search-domain [0, 100], Kp=21.52, Ki=20.28, Ku=80.15; Search-domain [0, 1000], Kp=665.35, Ki=682.26, Ku=627.78.](a6a8016b231533e7f34b550f4676afc6_img.jpg)

Figure 6: Step response of the system based on different ranges of search-domains with IAE and IAU as objectives. The figure consists of two subplots. The top subplot shows the 'Response' (y-axis, 0 to 1.2) versus 'Time(s)' (x-axis, 0 to 10). It contains three curves: a solid blue line for Search-domain [0, 10], a dashed red line for [0, 100], and a dotted black line for [0, 1000]. The bottom subplot shows the 'Control signal' (y-axis, 0 to 100) versus 'Time(s)' (x-axis, 0 to 10). It also contains three curves: a solid blue line for [0, 10], a dashed red line for [0, 100], and a dotted black line for [0, 1000]. Two insets are shown: the top-left inset shows a zoomed-in view of the control signal for the [0, 1000] search domain, and the bottom-right inset shows a zoomed-in view of the response for the [0, 10] search domain. The legend in the top subplot provides the optimal parameters for each search domain: Search-domain [0, 10], Kp=2.82, Ki=2.47, Ku=7.39; Search-domain [0, 100], Kp=21.52, Ki=20.28, Ku=80.15; Search-domain [0, 1000], Kp=665.35, Ki=682.26, Ku=627.78.

**Figure 6.** Step response of the system based on different ranges of search-domains with IAE and IAU as objectives. IAE: integral of absolute error; IAU: integral of absolute control signal.

**Table 3.** Optimal scaling factors based on different ranges of search-domains with IAE and IAU as objectives.

| Objective | Search-domain | $K_p$  | $K_i$  | $K_u$  | Settling time (s) | Overshoot of control signal |
|-----------|---------------|--------|--------|--------|-------------------|-----------------------------|
| IAE + IAU | [0, 10]       | 2.82   | 2.47   | 7.39   | 4.15              | 3.00                        |
| IAE + IAU | [0, 100]      | 21.52  | 20.28  | 80.15  | 4.08              | 3.95                        |
| IAE + IAU | [0, 1000]     | 665.35 | 682.26 | 627.78 | 5.45              | 95.27                       |

IAE: integral of absolute error; IAU: integral of absolute control signal.

![Figure 7: Step response of the system based on different R and Q with IAE and IAU as objectives. The figure consists of two subplots. The top subplot shows the 'Response' (y-axis, 0 to 1.2) versus 'Time(s)' (x-axis, 0 to 12). It contains five curves for different [R, Q] pairs: [1, 0], [0.9, 0.1], [0.8, 0.2], [0.5, 0.5], and [0.2, 0.8]. The bottom subplot shows the 'Control signal' (y-axis, -2 to 10) versus 'Time(s)' (x-axis, 0 to 12). It also contains five curves for the same [R, Q] pairs. An inset in the bottom-left corner shows a zoomed-in view of the control signal for the [1, 0] and [0.9, 0.1] cases. The legend in the top subplot provides the optimal parameters for each [R, Q] pair: [R, Q]=[1, 0], Kp=2.95, Ki=1.00, Ku=8.98; [R, Q]=[0.9, 0.1], Kp=2.15, Ki=1.00, Ku=5.38; [R, Q]=[0.8, 0.2], Kp=3.74, Ki=1.82, Ku=6.74; [R, Q]=[0.5, 0.5], Kp=2.82, Ki=2.47, Ku=7.39; [R, Q]=[0.2, 0.8], Kp=2.09, Ki=3.15, Ku=7.74; [R, Q]=[0.1, 0.9], Kp=1.09, Ki=2.45, Ku=7.29.](023b142f90e1253702ac88b18380d3ec_img.jpg)

Figure 7: Step response of the system based on different R and Q with IAE and IAU as objectives. The figure consists of two subplots. The top subplot shows the 'Response' (y-axis, 0 to 1.2) versus 'Time(s)' (x-axis, 0 to 12). It contains five curves for different [R, Q] pairs: [1, 0], [0.9, 0.1], [0.8, 0.2], [0.5, 0.5], and [0.2, 0.8]. The bottom subplot shows the 'Control signal' (y-axis, -2 to 10) versus 'Time(s)' (x-axis, 0 to 12). It also contains five curves for the same [R, Q] pairs. An inset in the bottom-left corner shows a zoomed-in view of the control signal for the [1, 0] and [0.9, 0.1] cases. The legend in the top subplot provides the optimal parameters for each [R, Q] pair: [R, Q]=[1, 0], Kp=2.95, Ki=1.00, Ku=8.98; [R, Q]=[0.9, 0.1], Kp=2.15, Ki=1.00, Ku=5.38; [R, Q]=[0.8, 0.2], Kp=3.74, Ki=1.82, Ku=6.74; [R, Q]=[0.5, 0.5], Kp=2.82, Ki=2.47, Ku=7.39; [R, Q]=[0.2, 0.8], Kp=2.09, Ki=3.15, Ku=7.74; [R, Q]=[0.1, 0.9], Kp=1.09, Ki=2.45, Ku=7.29.

**Figure 7.** Step response of the system based on different R and Q with IAE and IAU as objectives.

IAE: integral of absolute error; IAU: integral of absolute control signal.

**Table 4.** Optimal scaling factors based on different  $R$  and  $Q$  with IAE and IAU as objectives.

| $R, Q$   | $K_p$ | $K_i$ | $K_u$ | Settling time (s) | Overshoot of control signal |
|----------|-------|-------|-------|-------------------|-----------------------------|
| 1, 0     | 2.95  | 1.00  | 8.98  | 2.31              | 8.97                        |
| 0.9, 0.1 | 2.15  | 1.00  | 5.38  | 3.25              | 5.38                        |
| 0.8, 0.2 | 3.74  | 1.82  | 6.74  | 3.67              | 3.70                        |
| 0.5, 0.5 | 2.82  | 2.47  | 7.39  | 4.15              | 3.00                        |
| 0.2, 0.8 | 2.09  | 3.15  | 7.74  | 8.02              | 2.46                        |
| 0.1, 0.9 | 1.09  | 2.45  | 7.29  | 13.03             | 2.98                        |

IAE: integral of absolute error; IAU: integral of absolute control signal.

![Figure 8: Workflow of the simplified AFR feedback control system. The diagram shows a block diagram where a Throttle signal (theta) and a Fuel Delivery signal (m_f) are inputs. The Throttle signal goes to an Intake Manifold block, which outputs air mass flow rate (m_o). The Fuel Delivery signal goes to an AFR Controller block, which outputs fuel mass flow rate (m_fb). Both m_o and m_fb enter a Cylinder block. The output of the Cylinder block is the Exhaust Gas Oxygen (lambda) signal, which is fed back to the AFR Controller block.](5860ad6bd2a2dd8d1ab12864b8f90f37_img.jpg)

Figure 8: Workflow of the simplified AFR feedback control system. The diagram shows a block diagram where a Throttle signal (theta) and a Fuel Delivery signal (m\_f) are inputs. The Throttle signal goes to an Intake Manifold block, which outputs air mass flow rate (m\_o). The Fuel Delivery signal goes to an AFR Controller block, which outputs fuel mass flow rate (m\_fb). Both m\_o and m\_fb enter a Cylinder block. The output of the Cylinder block is the Exhaust Gas Oxygen (lambda) signal, which is fed back to the AFR Controller block.

**Figure 8.** The workflow of the simplified AFR feedback control system.

AFR: air–fuel ratio; EGO: exhaust gas oxygen.

engineering problems,  $W$  is applied as the correlation factor to ensure that the IAE and IAU values fall in the same scale of range, in case that the optimization process may be more sensitive to the objective with larger magnitude.

Thus, the final objective function for the optimization process is shown as

$$\min_{K_p, K_i, K_u} J = \text{minimize} \left( \sum_{k=1}^{n} W \cdot 0.5 \cdot T \cdot |e(k)| + \sum_{k=1}^{n} 0.5 \cdot T \cdot |u(k)| \right) \quad (8)$$

It is worth mentioning that, IAU is widely employed in the practical engineering problems against the extremely large control signal and violent system oscillation.

## Experimental setup

### AFR control plant

For GDI engines, AFR is defined as<sup>1,2,36</sup>

$$AFR = \frac{\dot{m}_o}{\dot{m}_{fc}} \quad (9)$$

where  $\dot{m}_{fc}$  indicates the rate of fuel mass injected into the cylinder from the injector directly;  $\dot{m}_o$  indicates the rate of air mass flowing through the cylinder inlet port; and  $\dot{m}_{fc}$  is comprised of both the feedforward estimated fuel injection rate  $\dot{m}_{ff}$  and the feedback corrected fuel injection rate  $\dot{m}_{fb}$ <sup>1,2</sup>

$$\dot{m}_{fc} = \dot{m}_{ff} + \dot{m}_{fb} = \frac{\dot{m}_o}{AFR_{ref}} + \dot{m}_{fb} \quad (10)$$

Basically,  $\dot{m}_{ff}$  is calculated based on the ideal stoichiometric  $AFR_{ref}$  and the air charge signal  $\dot{m}_o$ , in order to reduce the time delay and avoid large deviation of injection signal. However, due to the inaccurate measurement of air charge, there will be error in the estimated fuel injection rate. Then, the stoichiometric AFR cannot be achieved. Hence, the feedback fuel injection signal  $\dot{m}_{fb}$  should correct the error based on the real-time EGO sensor measurement of AFR. That is why an efficient AFR feedback control system is essential for modern GDI engines.

The workflow of the simplified AFR feedback control system is presented in Figure 8.

As Figure 8 shows, AFR is indicated as air to fuel equivalence ratio, lambda ( $\lambda$ ), which is the ratio of actual AFR to the stoichiometric value<sup>1,2,36–38</sup>

$$\lambda = \frac{AFR}{AFR_{stoich}} \quad (11)$$

$\lambda = 1.0$  indicates that AFR has been adjusted as stoichiometric value.

As mentioned in the previous section, IAE and IAU are employed as the objectives for the CAPSO programme. Thus, the AFR close-loop feedback controller is designed as shown in Figure 9:

### RCP test bench setup

As Figure 10 shows, a RCP test bench with a production V6 GDI engine (see Table 5 for engine specifications) is established and applied to validate the performance of the enhanced PI-like FKBC.

Thanks to ETAS's software (INTECRIIO, INCA) and hardware (ES910, ES930), RCP test bench could be set up. INTECRIIO compiles the Simulink-based controller model with the further prototyping settings to C-code for a specific rapid prototyping task. INCA is an interactive interface to execute the instruction for calibration and data measurement. Figure 11 gives the workflow to configure the RCP test.

The  $\lambda$  signal measured by oxygen sensor on exhaust manifold is sent to ES910 (a powerful real-time processor) through ES930 (a multi I/O module) as the

![Figure 9: Structure of PI-like FKBC with IAE and IAU as the objective functions. The diagram shows a control loop where the reference lambda (lambda_ref) is compared with the actual lambda (lambda). The error (e) is integrated (1/S) and used for IAE (Integral of Absolute Error) and IAU (Integral of Absolute Control signal) calculations. These are fed into the 'Objectives' block, which is part of the 'CAPSO algorithm'. The algorithm also interacts with a 'Fuzzy Logic Module' that determines the scaling factors Kp, Ki, and Kd. These factors are used in a PI-like controller block to generate the control signal u_ff, which is then combined with u_rb to produce the final control signal u.](b3baf3a29b67c7425d2562ddbc52f0cc_img.jpg)

Figure 9: Structure of PI-like FKBC with IAE and IAU as the objective functions. The diagram shows a control loop where the reference lambda (lambda\_ref) is compared with the actual lambda (lambda). The error (e) is integrated (1/S) and used for IAE (Integral of Absolute Error) and IAU (Integral of Absolute Control signal) calculations. These are fed into the 'Objectives' block, which is part of the 'CAPSO algorithm'. The algorithm also interacts with a 'Fuzzy Logic Module' that determines the scaling factors Kp, Ki, and Kd. These factors are used in a PI-like controller block to generate the control signal u\_ff, which is then combined with u\_rb to produce the final control signal u.

**Figure 9.** Structure of PI-like FKBC with IAE and IAU as the objective functions.

FKBC: fuzzy knowledge-based controller; IAE: integral of absolute error; IAU: integral of absolute control signal.

feedback signal for PI-like FKBC. Then, ES910 operates the programme of PI-like FKBC and outputs the renewed fuel injection signal to fuel delivery system in real time as the engine control unit is externally bypassed by an ETK cable.

### Experimental procedure

As mentioned above, the proposed CAPSO algorithm is evolved from the APSO algorithm. Therefore, both CAPSO and APSO are implemented for calibration in this article and the comparison of these two algorithms should be considered. Meanwhile, the algorithm-based PI-like FKBC is compared with the conventional self-adaptive PI-like FKBC using random scaling factors in Li et al.<sup>17</sup> to show the improvement.

Based on the experimental studies, the order of magnitude of IAE is 0.01 while it is 1.00 for IAU. Thus,  $W = 100$  is applied in equation (8) to normalize the IAE and IAU with the same resolution.

Throttle position 8% and 12% with engine rotation speed 1400 r/min have been studied for calibration

**Table 5.** Engine specifications.

| Engine type          | V6 GDI     |
|----------------------|------------|
| Displacement volume  | 2995 cc    |
| Maximum engine speed | 6600 r/min |
| Bore                 | 84.5 mm    |
| Stroke               | 89 mm      |
| Rod                  | 154 mm     |
| Compression ratio    | 10.5       |

within the threshold of engine operating conditions. In the first case, a step change of throttle position from 10% to 12% at the time 2 s with engine rotation speed 1400 r/min is picked randomly. In the second case, the throttle position is adjusted from 6% to 8% at the time 2 s as the step change with engine rotation speed 1400 r/min. The performance of the AFR control system with the calibration results (i.e. optimum  $K_p$ ,  $K_i$  and  $K_u$ ) is shown in Figures 14 and 17 and Tables 6 and 7 in the following section.

The last case for throttle positions 11% and 14% with engine rotation speed 1400 r/min is to validate the performance of PI-like FKBC at non-calibration operating conditions. Since the scaling factors of PI-like FKBC have been calibrated at throttle position 8% and 12%, the other throttle positions are regarded as non-calibration operating conditions. The PI-like FKBC should still regulate the signal effectively at all non-calibration conditions based on the calibrated scaling factors at calibration conditions. The details are shown in Figure 18 and Table 9.

For both of the CAPSO and APSO algorithm, the search-domain is selected as [0, 10]. Ten particles in each swarm and 20 iterations are pre-set for calibration.

Based on authors' previous research,<sup>17</sup> the  $\lambda$  value should be regulated back to 1.00 within 2 s. Hence, 5 s are enough for the AFR to become stabilized. Then, the engine is defined to run 5 s with each given group of scaling factors in each iteration for calibration. The

![Figure 10: RCP test bench setup. The left side shows a photograph of the physical setup with labels: 'ETAS ES910 & ES930', 'ECU', 'V6 GDI Engine', 'Oxygen Sensor', and 'PC'. The right side is a schematic diagram showing the data flow: PC connects to INCA-EIP, INTERIO, and SIMULINK. INCA-EIP connects to ETAS ES910. ETAS ES910 connects to the ECU via an ETK cable. ETAS ES910 and ETAS ES930 are connected in a 'Daisy Chain'. ETAS ES930 connects to the Oxygen Sensor. The Oxygen Sensor provides 'Lambda Value' to the ECU. The ECU sends 'Fuel Injection' signals to the 'V6 GDI Engine'. The engine is connected to a 'Dynamometer', which is driven by an 'AC Motor'.](2a0f333f04f8e672bebf288c511c1db5_img.jpg)

Figure 10: RCP test bench setup. The left side shows a photograph of the physical setup with labels: 'ETAS ES910 & ES930', 'ECU', 'V6 GDI Engine', 'Oxygen Sensor', and 'PC'. The right side is a schematic diagram showing the data flow: PC connects to INCA-EIP, INTERIO, and SIMULINK. INCA-EIP connects to ETAS ES910. ETAS ES910 connects to the ECU via an ETK cable. ETAS ES910 and ETAS ES930 are connected in a 'Daisy Chain'. ETAS ES930 connects to the Oxygen Sensor. The Oxygen Sensor provides 'Lambda Value' to the ECU. The ECU sends 'Fuel Injection' signals to the 'V6 GDI Engine'. The engine is connected to a 'Dynamometer', which is driven by an 'AC Motor'.

**Figure 10.** RCP test bench setup.

RCP: Rapid Control Prototyping; ECU: Engine Control Unit.

![Figure 11: The workflow of the RCP system. The diagram shows a sequence of steps: Simulink based model development, Model configuration, and Model compile & *.six file generation. These three steps are connected by horizontal arrows from left to right. Below these, there are three more steps: INTECIO configuration (Daisy Chain, ETK_Bypass, System, OS settings), INTECIO 'Build' and *.a2l file generation, and INCA configuration (Hardware, Projects, Experiment). These three steps are also connected by horizontal arrows from left to right. A vertical line connects the 'Model compile & *.six file generation' box to the 'INCA configuration' box. A horizontal arrow points from the 'INCA configuration' box to the 'Start experiment' box. A vertical line also connects the 'INTECIO configuration' box to the 'Model compile & *.six file generation' box.](e6df2733626a85205c1db682e6259c46_img.jpg)

Figure 11: The workflow of the RCP system. The diagram shows a sequence of steps: Simulink based model development, Model configuration, and Model compile & \*.six file generation. These three steps are connected by horizontal arrows from left to right. Below these, there are three more steps: INTECIO configuration (Daisy Chain, ETK\_Bypass, System, OS settings), INTECIO 'Build' and \*.a2l file generation, and INCA configuration (Hardware, Projects, Experiment). These three steps are also connected by horizontal arrows from left to right. A vertical line connects the 'Model compile & \*.six file generation' box to the 'INCA configuration' box. A horizontal arrow points from the 'INCA configuration' box to the 'Start experiment' box. A vertical line also connects the 'INTECIO configuration' box to the 'Model compile & \*.six file generation' box.

**Figure 11.** The workflow of the RCP system.  
RCP: Rapid Control Prototyping.

calibration process is switched on when the step change happens. After 5 s, the calibration process for the first given group of scaling factors will stop to run with next group of scaling factors. Because there are 10 particles in each swarm, 10 groups of scaling factors ( $K_p$ ,  $K_i$ ,  $K_u$ ) are generated and sent to the PI-like FKBC in each iteration in real time. Therefore, the calibration process will repeat 10 times and cost  $10 \times 5 = 50$  s for one generation of iteration. After that, the scaling factors for next generation of iteration will be calculated based on the algorithm mentioned in above section and fed into the engine. The calibration process will repeat 10 times (50 s) again. Given that 20 iterations are selected initially and calibration process will stop when the optimum results converge, it costs no more than  $20 \times 50 = 1000$  s (16.67 min) for the whole calibration process.

In each case, transient performances of three PI-like FKBCs are tested and compared. CAPSO algorithm is first used to calibrate the scaling factors of the first PI-like FKBC following the above procedures. The optimum results (determined scaling factors) are fed into the first PI-like FKBC and the corresponding real-time engine response is obtained. Then, APSO algorithm is used to calibrate the scaling factors of the second PI-like FKBC from the beginning again. The engine transient response with the optimum scaling factors is measured afterwards. The third PI-like FKBC is the conventional self-adaptive PI-like FKBC in Li et al.<sup>17</sup> where scaling factors are randomly selected rather than initially calibrated.

The  $\lambda$  value is supposed to be regulated within the range  $1.00 \pm 0.01$  with the disturbance. Once the  $\lambda$  value could be maintained within the range  $1.00 \pm 0.01$  after a certain duration of oscillation, it would be regarded as reaching the steady state.

## Experimental results and discussion

The APSO algorithm and CAPSO algorithm-based optimization processes of 12% throttle position are shown in Figures 12 and 13:

The red points in each figure indicate the optimal scaling factors  $K_p$ ,  $K_i$  and  $K_u$  which result in the minimum objective function after each iteration. As can be seen in figures, both APSO algorithm and CAPSO algorithm cost 12 iterations, around 10 min, to converge to the stable optimum results. The time consumption is less than the initially pre-set time. The calibration results and the step responses based on calculated scaling factors are shown in Table 6 and Figure 14:

Obviously, both CAPSO and APSO based PI-like FKBCs can damp out the oscillation more effectively than the conventional PI-like FKBC, while CAPSO-based PI-like FKBC performs better than APSO-based PI-like FKBC. Compared with conventional PI-like FKBC, CAPSO-based PI-like FKBC is able to reduce 19.39% of the total objective function  $IAE + IAU$ , while APSO-based PI-like FKBC could just reduce 12.57%.

The APSO algorithm- and CAPSO algorithm-based optimization processes of 8% throttle position are shown in Figures 15 and 16:

Similarly, the red points in each figure indicate the optimal scaling factors  $K_p$ ,  $K_i$  and  $K_u$  which result in the minimum objective function after each iteration. Both APSO algorithm and CAPSO algorithm cost 12 iterations, around 10 min, to converge to the stable optimal results. The time consumption is less than the initially pre-set time. The calibration results and the step responses based on calculated scaling factors are shown in Table 7 and Figure 17:

Likewise, both CAPSO- and APSO-based PI-like FKBCs can damp out the oscillation more effectively than the conventional PI-like FKBC, while CAPSO-based PI-like FKBC performs better than APSO-based PI-like FKBC. Compared with conventional PI-like FKBC, CAPSO-based PI-like FKBC is able to reduce 25.41% of the total objective function while APSO-based PI-like FKBC reduces 15.68%.

As the experimental results show, even though both CAPSO and APSO algorithms could converge to stable scaling factors within 12 iterations, CAPSO algorithm is able to result in smaller values of the total objective 



![Figure 12: Three subplots showing the convergence of Kp, Ki, and Ku factors over 20 iterations for 12% throttle position using APSO. Kp and Ku start high and converge to low values, while Ki starts high and converges to a stable value around 5.5.](ff2492be4fa814905acbad18f261b8a5_img.jpg)

Figure 12 consists of three subplots showing the convergence of  $K_p$ ,  $K_i$ , and  $K_u$  factors over 20 iterations for a 12% throttle position using APSO. The x-axis for all plots is 'Number of Iteration' (0 to 20). The y-axis for  $K_p$  and  $K_u$  ranges from 0 to 10, while for  $K_i$  it ranges from 0 to 10. Multiple lines with different markers (circles, crosses, squares, etc.) represent different runs or parameter sets. The red line with circles represents the final optimized values.

| Iteration | $K_p$ (Red Circles) | $K_i$ (Red Circles) | $K_u$ (Red Circles) |
|-----------|---------------------|---------------------|---------------------|
| 0         | 5.0                 | 1.0                 | 1.0                 |
| 2         | 1.5                 | 6.0                 | 8.0                 |
| 4         | 1.5                 | 6.0                 | 4.0                 |
| 6         | 2.5                 | 6.0                 | 1.0                 |
| 8         | 3.0                 | 6.0                 | 0.5                 |
| 10        | 2.5                 | 5.5                 | 0.5                 |
| 12        | 2.5                 | 5.5                 | 0.5                 |
| 14        | 2.5                 | 5.5                 | 0.5                 |
| 16        | 2.5                 | 5.5                 | 0.5                 |
| 18        | 2.5                 | 5.5                 | 0.5                 |
| 20        | 2.5                 | 5.5                 | 0.5                 |

Figure 12: Three subplots showing the convergence of Kp, Ki, and Ku factors over 20 iterations for 12% throttle position using APSO. Kp and Ku start high and converge to low values, while Ki starts high and converges to a stable value around 5.5.

**Figure 12.** Calculated  $K_p$ ,  $K_i$  and  $K_u$  factors after 20 iterations for 12% throttle position based on APSO.  
APSO: accelerated particle swarm optimization.

![Figure 13: Three subplots showing the convergence of Kp, Ki, and Ku factors over 20 iterations for 12% throttle position using CAPSO. Kp and Ku start high and converge to low values, while Ki starts high and converges to a stable value around 2.0.](eb903413d070b64f45cd763804ba443f_img.jpg)

Figure 13 consists of three subplots showing the convergence of  $K_p$ ,  $K_i$ , and  $K_u$  factors over 20 iterations for a 12% throttle position using CAPSO. The x-axis for all plots is 'Number of Iteration' (0 to 20). The y-axis for  $K_p$  and  $K_u$  ranges from 0 to 10, while for  $K_i$  it ranges from 0 to 10. Multiple lines with different markers (circles, crosses, squares, etc.) represent different runs or parameter sets. The red line with circles represents the final optimized values.

| Iteration | $K_p$ (Red Circles) | $K_i$ (Red Circles) | $K_u$ (Red Circles) |
|-----------|---------------------|---------------------|---------------------|
| 0         | 5.0                 | 1.0                 | 1.0                 |
| 2         | 2.5                 | 2.0                 | 8.0                 |
| 4         | 1.0                 | 2.0                 | 4.0                 |
| 6         | 1.0                 | 2.0                 | 1.0                 |
| 8         | 1.0                 | 2.0                 | 0.5                 |
| 10        | 0.5                 | 2.0                 | 0.5                 |
| 12        | 0.5                 | 2.0                 | 0.5                 |
| 14        | 0.5                 | 2.0                 | 0.5                 |
| 16        | 0.5                 | 2.0                 | 0.5                 |
| 18        | 0.5                 | 2.0                 | 0.5                 |
| 20        | 0.5                 | 2.0                 | 0.5                 |

Figure 13: Three subplots showing the convergence of Kp, Ki, and Ku factors over 20 iterations for 12% throttle position using CAPSO. Kp and Ku start high and converge to low values, while Ki starts high and converges to a stable value around 2.0.

**Figure 13.** Calculated  $K_p$ ,  $K_i$  and  $K_u$  factors after 20 iterations for 12% throttle position based on CAPSO.  
CAPSO: chaos-enhanced accelerated particle swarm optimization.

![Figure 14: Step response based on calculated scaling factors for 12% throttle position. (a) Lambda value response showing Lambda Value vs Time (s). (b) Air mass flow into the cylinder (kg/h) vs Time (s). (c) Fuel injection signal (kg/h) vs Time (s). Each plot compares Random factors (dotted line), APSO based factors (dashed line), and CAPSO based factors (solid line).](42ff8b598a0818ca8b6ef30850ad5f4e_img.jpg)

Figure 14 consists of three subplots (a), (b), and (c) showing step responses for 12% throttle position. Each subplot compares three methods: Random factors (dotted line), APSO based factors (dashed line), and CAPSO based factors (solid line). The x-axis for all plots is Time (s), ranging from 1.01 to 3.98.

- (a) Lambda Value vs Time (s): The y-axis ranges from 0.97 to 1.07. The response shows a peak around 2.39 seconds. CAPSO based factors (solid red line) show the highest peak, followed by APSO based factors (dashed green line), and Random factors (dotted black line) show the lowest peak.
- (b) Air mass flow into the cylinder (kg/h) vs Time (s): The y-axis ranges from 57 to 69. The response shows a sharp increase starting around 2.0 seconds. CAPSO based factors (solid red line) show the highest flow, followed by APSO based factors (dashed green line), and Random factors (dotted black line) show the lowest flow.
- (c) Fuel injection signal (kg/h) vs Time (s): The y-axis ranges from 3.8 to 4.8. The response shows a sharp increase starting around 2.0 seconds. CAPSO based factors (solid red line) show the highest injection signal, followed by APSO based factors (dashed green line), and Random factors (dotted black line) show the lowest injection signal.

Figure 14: Step response based on calculated scaling factors for 12% throttle position. (a) Lambda value response showing Lambda Value vs Time (s). (b) Air mass flow into the cylinder (kg/h) vs Time (s). (c) Fuel injection signal (kg/h) vs Time (s). Each plot compares Random factors (dotted line), APSO based factors (dashed line), and CAPSO based factors (solid line).

**Figure 14.** Step response based on calculated scaling factors for 12% throttle position: (a)  $\lambda$  value response. (b) Air mass flow into the cylinder (kg/h). (c) Fuel injection (kg/h).

APSO: accelerated particle swarm optimization; CAPSO: chaos-enhanced accelerated particle swarm optimization.

**Table 6.** Calibration result and performance evaluation for 12% throttle position.

| Scaling factors | $K_p$ | $K_i$ | $K_u$ | Settling time (s) | Maximum overshoot of $\lambda$ | IAE    | IAU   | $0.5 \times \text{IAE} + 0.5 \times \text{IAU}$ |
|-----------------|-------|-------|-------|-------------------|--------------------------------|--------|-------|-------------------------------------------------|
| Random          | 5.00  | 10.00 | 0.20  | 1.10              | 0.063                          | 3.143  | 7.045 | 5.094                                           |
| APSO based      | 2.24  | 5.50  | 0.42  | 0.54              | 0.050                          | 1.886  | 7.021 | 4.453                                           |
| Reduction       |       |       |       | 50.91%            | 20.63%                         | 39.99% |       | 12.57%                                          |
| CAPSO based     | 0.37  | 2.10  | 1.28  | 0.47              | 0.043                          | 1.411  | 7.050 | 4.231                                           |
| Reduction       |       |       |       | 57.27%            | 31.75%                         | 55.11% |       | 19.39%                                          |

IAE: integral of absolute error; IAU: integral of absolute control signal; APSO: accelerated particle swarm optimization; CAPSO: chaos-enhanced accelerated particle swarm optimization.

**Table 7.** Calibration result and performance evaluation for 8% throttle position.

| Scaling factors | $K_p$ | $K_i$ | $K_u$ | Settling time (s) | Maximum overshoot of $\lambda$ | IAE    | IAU   | $0.5 \times \text{IAE} + 0.5 \times \text{IAU}$ |
|-----------------|-------|-------|-------|-------------------|--------------------------------|--------|-------|-------------------------------------------------|
| Random          | 5.00  | 10.00 | 0.20  | 1.13              | 0.083                          | 4.973  | 5.461 | 5.217                                           |
| APSO based      | 3.72  | 5.68  | 0.38  | 0.67              | 0.068                          | 3.307  | 5.491 | 4.399                                           |
| Reduction       |       |       |       | 40.71%            | 18.07%                         | 33.50% |       | 15.68%                                          |
| CAPSO based     | 0.66  | 3.56  | 0.77  | 0.45              | 0.058                          | 2.260  | 5.523 | 3.892                                           |
| Reduction       |       |       |       | 60.18%            | 30.12%                         | 54.55% |       | 25.41%                                          |

IAE: integral of absolute error; IAU: integral of absolute control signal; APSO: accelerated particle swarm optimization; CAPSO: chaos-enhanced accelerated particle swarm optimization.

**Table 8.** Mean value and standard deviation of the total cost function using CAPSO and APSO.

| Throttle position | Optimization algorithm | Mean value of cost function | Standard deviation of cost function |
|-------------------|------------------------|-----------------------------|-------------------------------------|
| 12%               | APSO                   | 4.422                       | 0.139                               |
|                   | CAPSO                  | 4.224                       | 0.101                               |
|                   | Reduction              | 4.48%                       | 26.88%                              |
| 8%                | APSO                   | 4.384                       | 0.265                               |
|                   | CAPSO                  | 3.887                       | 0.190                               |
|                   | Reduction              | 10.61%                      | 28.29%                              |

APSO: accelerated particle swarm optimization; CAPSO: chaos-enhanced accelerated particle swarm optimization.

![Figure 15: Three line graphs showing the calculated Kp, Ki, and Ku factors over 20 iterations for an 8% throttle position using the APSO algorithm. The Kp graph shows values fluctuating between 2 and 6, stabilizing around 4. The Ki graph shows values fluctuating between 4 and 6, stabilizing around 5.5. The Ku graph shows values starting high (around 8) and rapidly decreasing to near zero by iteration 4, remaining there.](8b79f5ec940d107c246612c2a2ec519f_img.jpg)

Figure 15: Three line graphs showing the calculated Kp, Ki, and Ku factors over 20 iterations for an 8% throttle position using the APSO algorithm. The Kp graph shows values fluctuating between 2 and 6, stabilizing around 4. The Ki graph shows values fluctuating between 4 and 6, stabilizing around 5.5. The Ku graph shows values starting high (around 8) and rapidly decreasing to near zero by iteration 4, remaining there.

**Figure 15.** Calculated  $K_p$ ,  $K_i$  and  $K_u$  factors after 20 iterations for 8% throttle position based on APSO.

APSO: accelerated particle swarm optimization.

function, namely, better controller performance. Since CAPSO algorithm employs the chaotic mapping strategy with the algorithm, it can improve both the randomization and diversification of the solutions, which allows the optimizer to explore a wider searching space and avoid falling into the trap of locally optimal results.

However, because both CAPSO and APSO algorithms generate random values during the calibration process, it is not fair to compare their performance through a single case. Therefore, Monte Carlo analysis approach is implemented to assess the performance of the algorithm through 20 times repeatability tests and statistical analysis. The results are shown in Table 8,

including the mean value and standard deviation of the total cost function (IAE + IAU).

In terms of the mean value of cost function, CAPSO approach is able to reduce it by up to 10.61% compared with APSO approach. In other words, CAPSO approach can achieve better trade-off between reducing the oscillation effectively and avoiding extremely large control signal. Meanwhile, the CAPSO approach can reduce the standard deviation value by up to 28.29% compared with the conventional APSO approach. The lower standard deviation value indicates that optimization results fall into a narrower range.

![Figure 16: Three line graphs showing the calculated scaling factors Kp, KI, and KU over 20 iterations for 8% throttle position based on CAPSO. The x-axis for all graphs is 'Number of Iteration' (0 to 20). The y-axis for Kp is 0 to 10, for KI is 0 to 8, and for KU is 0 to 10. Each graph compares three methods: Random factors (dotted line with 'x' markers), APSO based factors (dashed line with '+' markers), and CAPSO based factors (solid line with circle markers). In all cases, the CAPSO method converges to a stable value much faster than the other methods.](0332672e127cd13bb6d2fc8d1e27bfa2_img.jpg)

Figure 16: Three line graphs showing the calculated scaling factors Kp, KI, and KU over 20 iterations for 8% throttle position based on CAPSO. The x-axis for all graphs is 'Number of Iteration' (0 to 20). The y-axis for Kp is 0 to 10, for KI is 0 to 8, and for KU is 0 to 10. Each graph compares three methods: Random factors (dotted line with 'x' markers), APSO based factors (dashed line with '+' markers), and CAPSO based factors (solid line with circle markers). In all cases, the CAPSO method converges to a stable value much faster than the other methods.

**Figure 16.** Calculated  $K_p$ ,  $K_I$  and  $K_U$  factors after 20 iterations for 8% throttle position based on CAPSO.

CAPSO: chaos-enhanced accelerated particle swarm optimization.

![Figure 17: Three line graphs showing step response based on calculated scaling factors for 8% throttle position. The x-axis for all graphs is 'Time (s)' (1.01 to 3.98). (a) Lambda value response: y-axis is 'Lambda Value' (0.97 to 1.09). (b) Air mass flow into cylinder response: y-axis is 'Air mass flow into cylinder (kg/h)' (44 to 54). (c) Fuel injection signal response: y-axis is 'Fuel injection signal (kg/h)' (3 to 3.7). Each graph compares three methods: Random factors (dotted line with 'x' markers), APSO based factors (dashed line with '+' markers), and CAPSO based factors (solid line with circle markers). The CAPSO method consistently shows the most accurate and stable response across all three parameters.](fd188843e5acb8e0d76372860b5f5962_img.jpg)

Figure 17: Three line graphs showing step response based on calculated scaling factors for 8% throttle position. The x-axis for all graphs is 'Time (s)' (1.01 to 3.98). (a) Lambda value response: y-axis is 'Lambda Value' (0.97 to 1.09). (b) Air mass flow into cylinder response: y-axis is 'Air mass flow into cylinder (kg/h)' (44 to 54). (c) Fuel injection signal response: y-axis is 'Fuel injection signal (kg/h)' (3 to 3.7). Each graph compares three methods: Random factors (dotted line with 'x' markers), APSO based factors (dashed line with '+' markers), and CAPSO based factors (solid line with circle markers). The CAPSO method consistently shows the most accurate and stable response across all three parameters.

**Figure 17.** Step response based on calculated scaling factors for 8% throttle position: (a)  $\lambda$  value response, (b) air mass flow into the cylinder (kg/h) and (c) fuel injection (kg/h).

APSO: accelerated particle swarm optimization; CAPSO: chaos-enhanced accelerated particle swarm optimization.

![Figure 18: Step response at non-calibration operating conditions. (a) Throttle position step changes from 8% to 11% and then to 14%. (b) Lambda value response showing oscillations around 1.0. (c) Air mass flow into the cylinder (kg/h) response. (d) Fuel injection correlation signal (kg/h) response. Each plot compares Random factors (dotted line), APSO based factors (dashed green line), and CAPSO based factors (solid red line).](0a8d173734e4e46c344178e8d21bcbc3_img.jpg)

Figure 18: Step response at non-calibration operating conditions. (a) Throttle position step changes from 8% to 11% and then to 14%. (b) Lambda value response showing oscillations around 1.0. (c) Air mass flow into the cylinder (kg/h) response. (d) Fuel injection correlation signal (kg/h) response. Each plot compares Random factors (dotted line), APSO based factors (dashed green line), and CAPSO based factors (solid red line).

**Figure 18.** Step response at non-calibration operating conditions: (a) throttle position step changes, (b)  $\lambda$  value response, (c) air mass flow into the cylinder (kg/h) and (d) fuel injection (kg/h).

APSO: accelerated particle swarm optimization; CAPSO: chaos-enhanced accelerated particle swarm optimization.

**Table 9.** Performance evaluation for non-calibration operating conditions.

| Step of throttle position | Controller   | Settling time (s) | Maximum overshoot of $\lambda$ | IAE    | IAU   | $0.5 \times \text{IAE} + 0.5 \times \text{IAU}$ |
|---------------------------|--------------|-------------------|--------------------------------|--------|-------|-------------------------------------------------|
| 8–11%                     | Conventional | 1.11              | 0.070                          | 4.518  | 6.527 | 5.523                                           |
|                           | APSO based   | 0.50              | 0.066                          | 2.705  | 6.621 | 4.663                                           |
|                           | Reduction    | 54.96%            | 5.71%                          | 40.13% |       | 15.57%                                          |
|                           | CAPSO based  | 0.45              | 0.060                          | 2.275  | 6.615 | 4.445                                           |
|                           | Reduction    | 59.46%            | 14.29%                         | 49.65% |       | 19.52%                                          |
|                           | Reduction    |                   |                                |        |       |                                                 |
| 11–14%                    | Conventional | 0.96              | 0.053                          | 2.516  | 6.562 | 4.539                                           |
|                           | APSO based   | 0.30              | 0.049                          | 1.354  | 6.557 | 3.956                                           |
|                           | Reduction    | 68.75%            | 7.55%                          | 46.18% |       | 12.86%                                          |
|                           | CAPSO based  | 0.24              | 0.045                          | 0.904  | 6.571 | 3.738                                           |
|                           | Reduction    | 75.00%            | 15.09%                         | 64.07% |       | 17.66%                                          |
|                           | Reduction    |                   |                                |        |       |                                                 |

As introduced in the ‘Experimental setup’ section, throttle positions 11% and 14% are selected as non-calibration operating conditions. The transient responses of PI-like FKBCs based on APSO and CAPSO algorithms at non-calibration operating conditions are shown in Table 9 and Figure 18:

As can be seen from the experimental results, both CAPSO- and APSO-based PI-like FKBCs can damp out the oscillation more effectively than the conventional self-adaptive PI-like FKBC at non-calibration

operating conditions, while CAPSO-based PI-like FKBC performs better than APSO-based PI-like FKBC. Compared with conventional PI-like FKBC, CAPSO-based PI-like FKBC is able to reduce the total objective function by up to 19.52% while APSO-based PI-like FKBC reduces the total objective function by up to 15.57%. As introduced earlier, because CAPSO algorithm allows the optimizer to find better globally optimum results at calibration operating conditions, more optimal scaling factors at calibration operating

conditions will definitely lead to better transient performance at non-calibration operating conditions.

The transient calibration approach is able to cover a wide range of operation conditions. As introduced in the ‘Choice of objective functions’ section, the calibration result depends more on the selection of objective. For any operation conditions or step changes, once the objectives are defined as IAE and IAU, the calibration programme will repeat running the engine with different groups of scaling factors until the optimum solutions are found to achieve the minimum oscillation and the most stable control signal.

In addition, Li et al.<sup>17</sup> have validated the self-adaptive capability of the PI-like FKBC. The experimental studies in Li et al.<sup>17</sup> and this article have shown that two sets of initially calibrated scaling factors are able to cover all the other non-calibrated conditions. The PI-like FKBC needs to calibrate only two sets of scaling factors as reference. Then, the control signal will be adjusted automatically based on the change of gap between the target value and actual value, no matter how large or small. Thus, the PI-like FKBC is able to regulate the AFR effectively with any unknown step changes. Moreover, due to the application of transient calibration, these two sets of initially calibrated scaling factors are determined as the optimum solutions. Hence, the PI-like FKBC is able to cover a wide range of operation conditions regardless of the size of step change.

More initially calibrated scaling factors may lead to not only more reliable performance but also more time consumption. Since the purpose of developing the PI-like FKBC is to reduce the time and effort for calibration, users can choose the trade-off between the number of initially calibrated scaling factors and the time consumption by themselves.<sup>17</sup>

# Conclusion

An enhanced intelligent PI-like FKBC based on CAPSO algorithm has been designed and developed for GDI engines to improve AFR control system. The scaling factors of the PI-like FKBC are calibrated automatically through CAPSO algorithm. An alternative time-domain objective function is applied for the optimization programme without the need of prior selection of search-domain. The real-time transient performance of the enhanced PI-like FKBC is investigated through experimental studies. The conclusions are listed as follows:

- The proposed enhanced PI-like FKBC based on CAPSO algorithm can lead to better transient response behaviour to damp out the oscillation with less settling time (up to 75% reduction) and less IAE (up to 64.07% reduction) for various operating points, compared with the conventional self-adaptive PI-like FKBC.

- Since both the IAE and IAU are employed as objectives, the proposed enhanced PI-like FKBC is able to achieve better trade-off between reducing the oscillation effectively and avoiding large overshoot of control signal. It is able to reduce the total objective function (IAE + IAU) by up to 25.41% reduction, compared with the conventional self-adaptive PI-like FKBC.
- The enhanced PI-like FKBC based on CAPSO algorithm outperforms the one based on APSO algorithm. The repeatability tests indicate that the CAPSO algorithm-based PI-like FKBC is able to reduce the mean value of optimization objective function by up to 10.61% reduction compared with the APSO algorithm-based PI-like FKBC. Meanwhile, the standard deviation of the objective function using CAPSO algorithm is lower (up to 28.29% reduction) than that using APSO algorithm.

Overall, the proposed enhanced PI-like FKBC is capable of both self-adaptive capability and non-model-based automatic transient calibration capability. It can reduce the effort to be spent on calibrating controller parameters and regulate AFR more effectively for various engine operation conditions.

# Declaration of conflicting interests

The author(s) declared no potential conflicts of interest with respect to the research, authorship and/or publication of this article.

# Funding

The author(s) received no financial support for the research, authorship and/or publication of this article.

# ORCID iD

Ziyang Li ![ORCID icon](646a0208e347b1bb57cd3819f48da9ae_img.jpg) <https://orcid.org/0000-0001-6052-9246>

# References

1. Heywood JB. *Internal combustion engine fundamentals*. Illustrated ed. New York: McGraw-Hill, 1988.
2. Stone R. *Introduction to internal combustion engines*. 4th rev. ed. Basingstoke: Palgrave Macmillan, 2012.
3. Shi Y, Yu DL, Tian Y, et al. Air-fuel ratio prediction and NMPC for SI engines with modified Volterra model and RBF network. *Eng Appl Artif Intel* 2015; 45: 313–324.
4. Kumar M and Shen T. In-cylinder pressure-based air-fuel ratio control for lean burn operation mode of SI engines. *Energ* 2017; 120: 106–116.
5. Yildiz Y, Annaswamy AM, Yanakiev D, et al. Spark ignition engine fuel-to-air ratio control: an adaptive control approach. *Control Eng Pract* 2010; 18: 1369–1378.
6. Banerjee R and Kumar S. Numerical investigation of stratified air/fuel preparation in a GDI engine. *Appl Therm Eng* 2016; 104: 414–428.

7. Costa M, Catapano F, Sementa P, et al. Mixture preparation and combustion in a GDI engine under stoichiometric or lean charge: an experimental and numerical study on an optically accessible engine. *Appl Energ* 2016; 180: 86–103.
8. Kumaravel K, Anand BP, Anusha K, et al. Evaluation of lean operation limit on performance features of stratified charge gasoline direct injection (GDI) engine. *Int J Eng Innov Res* 2014; 3: 635–641.
9. Lin J, Chen H and Wang P. AFR control of a gasoline engine using triple-step method. In: *29th Chinese control and decision conference (CCDC)*, Chongqing, China, 28–30 May 2017, pp.1976–1981. New York: IEEE.
10. Ebrahimi B, Tafreshi R, Mohammadpour J, et al. Second-order sliding mode strategy for air–fuel ratio control of lean-burn SI engines. *IEEE T Contr Syst T* 2014; 22: 1374–1384.
11. Rigatos G, Siano P, Melkikh A, et al. A nonlinear H-infinity control approach to stabilization of distributed synchronous generators. *IEEE Syst J* 2018; 12: 2654–2663.
12. Liu C, Jiang B, Zhang K, et al. Adaptive fault-tolerant H-infinity output feedback control for lead-wing close formation flight. *IEEE T Syst Man Cybern: Syst*. Epub ahead of print 11 May 2018. DOI: 10.1109/TSMC.2018.2830511.
13. Zheng Y, Li SE, Li K, et al. Platooning of connected vehicles with undirected topologies: robustness analysis and distributed H-infinity controller synthesis. *IEEE T Intell Transp* 2018; 19: 1353–1364.
14. Askari MR, Shahrokhi M and Talkhoncheg MK. Observer-based adaptive fuzzy controller for nonlinear systems with unknown control directions and input saturation. *Fuzzy Set Syst* 2017; 314: 24–45.
15. Liu H, Li S, Cao J, et al. Adaptive fuzzy prescribed performance controller design for a class of uncertain fractional-order nonlinear systems with external disturbances. *Neurocomput* 2017; 219: 422–430.
16. Pasieka M, Grzesik N and Kuźma K. Simulation modeling of fuzzy logic controller for aircraft engines. *Int J Comput* 2017; 16: 27–33.
17. Li Z, Li J, Zhou Q, et al. Intelligent air/fuel ratio control strategy with a PI-like fuzzy knowledge-based controller for gasoline direct injection engines. *Proc IMechE Part D: J Automobile Engineering* 2018; 233: 2161–2173.
18. Ma H, Li Z, Tayarani M, et al. Computational intelligence nonmodel-based calibration approach for internal combustion engines. *J Dyn Sys Meas Contr* 2017; 140: 041002.
19. Gomez J. Stochastic global optimization algorithms: a systematic formal approach. *Inform Sciences* 2019; 472: 53–76.
20. Bartz-Beielstein T and Zaefferer M. Model-based methods for continuous and discrete global optimization. *Appl Soft Comput* 2017; 55: 154–167.
21. Ma H, Li Z, Tayarani M, et al. Model-based computational intelligence multi-objective optimization for gasoline direct injection engine calibration. *Proc IMechE Part D: J Automobile Engineering* 2018; 233: 1391–1402.
22. Tayarani M, Yao X and Xu H. Meta-heuristic algorithms in car engine design: a literature survey. *IEEE T Evolut Comput* 2015; 19: 609–629.
23. Yang XS, Chien SF and Ting TO. Computational intelligence and metaheuristic algorithms with applications. *Sci World J* 2014; 2014: 425853.
24. Zhang Y, Zhou Q, Li Z, et al. Intelligent transient calibration of a dual-loop EGR diesel engine using chaos-enhanced accelerated particle swarm optimization algorithm. *Proc IMechE Part D: J Automobile Engineering* 2019; 233: 1698–1711.
25. Zhou Q, Zhang W, Cash S, et al. Intelligent sizing of a series hybrid electric power-train system based on chaos-enhanced accelerated particle swarm optimization. *Appl Energ* 2017; 189: 588–601.
26. Slowik A and Kwasnicka H. Nature inspired methods and their industry applications – swarm intelligence algorithms. *IEEE T Ind Inform* 2018; 14: 1004–1015.
27. Fong S, Wong R and Vasilakos AV. Accelerated PSO swarm search feature selection for data stream mining big data. *IEEE T Serv Comput* 2016; 9: 33–45.
28. Talatahari S, Khalili E and Alavizadeh SM. Accelerated particle swarm for optimum design of frame structures. *Math Probl Eng* 2013; 2013: 649857.
29. Yang D, Liu Z, Yi P, et al. Computational efficiency of accelerated particle swarm optimization combined with different chaotic maps for global optimization. *Neural Comput Appl* 2017; 28: 1245–1264.
30. Gandomia AH, Yun GJ, Yang XS, et al. Chaos-enhanced accelerated particle swarm optimization. *Commun Nonlinear Sci* 2013; 18: 327–340.
31. Gou J, Lei TX and Guo WP. A novel improved particle swarm optimization algorithm based on individual difference evolution. *Appl Soft Comput* 2017; 57: 468–481.
32. Noshadi A, Shi J and Lee WS. Optimal PID-type fuzzy logic controller for a multi-input multi-output active magnetic bearing system. *Neural Comput Appl* 2016; 27: 2031–2046.
33. Wolpert DH and Macready WG. No free lunch theorems for optimization. *IEEE T Evolut Comput* 1997; 1: 67–82.
34. Netjinda N, Achalakul T and Sirinaovakul B. Particle swarm optimization inspired by starling flock behavior. *Appl Soft Comput* 2015; 35: 411–422.
35. Yang XS. *Nature-inspired optimization algorithms*. Amsterdam: Elsevier, 2014.
36. Isermann R. *Engine modeling and control: modeling and electronic management of internal combustion engines*. Berlin; Heidelberg: Springer-Verlag, 2014.
37. Xue W, Bai W, Yang S, et al. ADRC with adaptive extended state observer and its application to air–fuel ratio control in gasoline engines. *IEEE T Ind Electro* 2015; 62: 5847–5857.
38. Karvountzis-Kontakiotis A, Dimaratos A, Ntziachristos L, et al. Exploring the stochastic and deterministic aspects of cyclic emission variability on a high speed spark-ignition engine. *Energ* 2017; 118: 68–76.