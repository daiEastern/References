

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Automatica journal cover and Elsevier logo](390120de4fe440c42fea8154fcaad334_img.jpg)

Automatica journal cover and Elsevier logo

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Drift compensation of time synchronization in WSNs with random delays: A new threshold based design <sup>☆</sup>

Bo Wang<sup>a,\*</sup>, Xinxin Lv<sup>b</sup>

<sup>a</sup> School of Automation and International Joint Research Laboratory for Autonomous Robotic Systems, Hangzhou Dianzi University, Hangzhou, 310018, China

<sup>b</sup> School of Information Science and Engineering, Zhejiang Sci-Tech University, Hangzhou, 310018, China

## ARTICLE INFO

### Article history:

Received 16 June 2024

Received in revised form 12 October 2024

Accepted 15 October 2024

Available online 6 January 2025

### Keywords:

Time synchronization

WSNs

Random delays

Switching topologies

Drift compensation

## ABSTRACT

This paper investigates the drift compensation problem of time synchronization for wireless sensor networks (WSNs) with random bounded communication delays. The commonly used pseudo-periodic broadcast communication protocol is used to complete the communication between nodes of the WSN. Firstly, a new constant gain drift compensation algorithm is proposed via threshold design, which not only is robust to arbitrarily bounded delay but also has low computational complexity. Then, by modeling this algorithm as a delay-existing consensus model with multiplicative uncertainties, it is rigorously proved that the proposed drift compensation algorithm can ensure all virtual drifts converge to a common positive constant at a rate no slower than  $O(1/k)$  if the interaction topology sequence caused by the pseudo-periodic broadcast communication protocol is uniformly rooted, which is the weakest topology condition to achieve the consensus for the virtual drift. Further, the partial time synchronization error with this new drift compensation algorithm is analyzed. Finally, simulation results are presented to illustrate the effectiveness of the proposed algorithm.

© 2024 Elsevier Ltd. All rights are reserved, including those for text and data mining, AI training, and similar technologies.

## 1. Introduction

Time synchronization as an important problem for WSNs has received a lot of attention from researchers (Fagnani & Zampieri, 2007; Faizulkhakov, 2007; Ganeriwal, Kumar, & Srivastava, 2003; Sundaraman, Buy, & Kshemkalyani, 2005; Tian et al., 2020), due to the fact that many WSN-based applications, such as data fusion and event detection, require global time synchronization for all nodes in the network.

Up to now, many time synchronization algorithms have been constructed (Carli, Chiuso, Schenato, & Zampieri, 2008; Dai & Han, 2004; Elson, Girod, & Estrin, 2002; Li & Rus, 2006; Maróti, Kusy, Simon, & Lédeczi, 2004; Noh, Serpedin, & Qaraqe, 2008), where some early ones, such as Reference Broadcast Synchronization algorithm (Elson et al., 2002), Flooding Time Synchronization Protocol (Maróti et al., 2004), Hierarchy Referencing Time Synchronization algorithm (Dai & Han, 2004) and Pairwise Broadcast Synchronization algorithm (Noh et al., 2008) mainly belong to a class of non-fully distributed algorithm which are usually subject

to the requirement of a common reference node (Elson et al., 2002) or a certain topology structure (Dai & Han, 2004). Thus, these algorithms are usually lack of robustness and network scalability. Considering these reasons, many researchers have tried to design the fully distributed time synchronization algorithm (Bolognani, Carli, Lovisari, & Zampieri, 2016; Du & Wu, 2013; Liao & Barooah, 2013; Stanković, Stanković, & Johansson, 2018; Tian, Zong, & Cao, 2016; Yildirim, Carli, & Schenato, 2018). For example, Du and Wu (2013) propose a belief propagation based asynchronous distributed time synchronization algorithm from the perspective of the parameter estimation. Yildirim, Carli, and Schenato (2018) present an adaptive proportional-integral time synchronization (PI Sync) algorithm for a 2-node network.

Recently, some fully distributed time synchronization algorithms which are constructed from the perspective of the consensus have been proposed (He, Cheng, Shi, Chen, & Sun, 2014; Schenato & Fiorentin, 2011; Tian et al., 2016). Then, the time synchronization problem is equivalent to the consensus problem with respect to the drift compensation and the offset compensation, of which the drift compensation is the key to achieving bounded time synchronization. This point can be seen from the structural modeling of consensus based time synchronization algorithm summarized in Tian, Zong, and Cao (2016), where the main difference between algorithms is reflected in the drift compensation part. In this paper, we will focus on the drift compensation problem of time synchronization. As a typical design, the drift compensation in Average TimeSync (ATS) algorithm

<sup>☆</sup> This work is supported by the National Natural Science Foundation of China (under grants 61903110 and 62073107). The material in this paper was not presented at any conference. This paper was recommended for publication in revised form by Associate Editor Luca Schenato under the direction of Editor Christos G. Cassandras.

\* Corresponding author.

E-mail addresses: [wangbo@hdz.edu.cn](mailto:wangbo@hdz.edu.cn) (B. Wang), [xinxinlv@zstu.edu.cn](mailto:xinxinlv@zstu.edu.cn) (X. Lv).

(Schenato & Fiorentin, 2011) ensures all nodes' virtual drifts can achieve the consensus at an exponential convergence rate as along as the topology sequence of the time-varying interaction network is uniformly rooted (UR). However, this algorithm is proved to be ineffective if random delays are involved (Tian et al., 2016). For the case that there are time-invariant delays in the time synchronization problem, Freris, Graham, and Kumar (2011) show that the clock drift can be determined exactly while only the bounded time synchronization can be achieved. For the case that the delays are random, Tian (2015) proposes a least square estimation based time synchronization (LSTS) algorithm. It is proved in Tian (2017) that the drift compensation part can achieve the consensus for the virtual drift at a rate no smaller than  $O(1/k)$  if the interaction network satisfies some topology conditions, such as the balanced time-varying topology. However, these topology conditions are hard to be satisfied in practice. My co-authors and I once proposed a drift compensation algorithm in Wang and Tian (2017) while this algorithm is subject to a leader-following topology assumption.

More recently, Wang, Chen, Li, and Gong (2020) give a drift compensation algorithm based on the maximum likelihood method, where the delay is assumed to be truncated exponential. My co-authors and I (Tian et al., 2020) propose a delay compensation-based time synchronization (DCBTS) algorithm. Although both numerical simulations and physical experiments show that the DCBTS algorithm can achieve better performance compared with LSTS algorithm and PISync algorithm, what a pity is that the rigorous proof of the drift compensation part is not given. Wang, Gong, and Li (2022) propose a sequential least squares based time synchronization algorithm (SSTS), where the computational complexity of the drift compensation part is high due to the computation of sequential least squares and the network is supposed to be strongly rooted at each node (i.e., the uniformly strongly connected network case). Almost all existed drift compensation part in algorithms (e.g., the LSTS, DCBTS and SSTS algorithm) require an extra dormancy slot assumption in the update process, where the reason behind the introduction of this assumption is only to support the convergence analysis. If this assumption is dropped, it may be difficult to build the rigorous convergence conclusions under these mentioned algorithms due to the loss of methodology. Also, this assumption inevitably leads to more packet drops and lower the synchronization rate. Besides, they may be lack of robustness if the delay has a big variance due to the reason that the convergence value of the virtual drift under these algorithms depend seriously on the delay, where a big convergence value will correspond to a big partial synchronization error.

In summary, the above mentioned drift compensation algorithms with random delays in existed references either have a strong operating condition or are not robust to the effect of delays. A problem is whether there exists a drift compensation algorithm that can integrate the following distinctive features into one: (1) it can achieve the bounded partial time synchronization with random bounded delays as drift compensations of the LSTS, SSTS and DCBTS algorithm do; (2) it can be rigorously proved to be effective under the weakest topology condition (i.e., the UR topology) while the drift compensation of the LSTS, SSTS and DCBTS algorithm cannot; (3) it can operate under a relaxed condition (e.g., without depending on the dormancy slot assumption while the drift compensation of the LSTS, SSTS and DCBTS algorithm cannot); (4) it owes low computational complexity; (5) it is robust to the effect of delays while the drift compensation of the LSTS, SSTS and DCBTS algorithm cannot if the delay has a big variance. To the best of our knowledge, it is still an open problem, which motivates us to this study.

This paper studies the drift compensation problem of time synchronization for WSNs with random bounded communication

delays. Firstly, a new constant gain drift compensation algorithm via threshold design is proposed, which also belongs to a class of consensus based algorithms. Then, by modeling this algorithm as a delay-existing consensus model with multiplicative uncertainties, it is rigorously proved that if the interaction topology sequence is UR, this drift compensation algorithm can ensure all virtual drifts converge to a common positive constant at a rate no slower than  $O(1/k)$  when random bounded delays are involved, which implies that the bounded partial time synchronization can be achieved. Finally, the simulation is provided to verify the effectiveness of the proposed algorithm. Compared with the drift compensation part in LSTS and SSTS algorithm, this new algorithm owes low computational complexity and requires looser topology condition. Compared with the drift compensation part in DCBTS algorithm, this new algorithm is rigorously proved to be effective under the UR topology. Compared with the drift compensation part in LSTS, DCBTS and SSTS algorithm, this new algorithm not only can operate in a relaxed condition that does not require the dormancy slot assumption but also is robust to the effect of delays especially if the delay has a big variance.

The rest of the paper is organized as follows. Section 2 describes the problem. Section 3 gives the algorithm design and convergence conclusion. Section 4 gives the convergence analysis. Section 5 gives the simulation result and Section 6 concludes the paper and discusses related future study.

### 1.1. Notation

The following notations are used in this paper.  $I$  represents the identity matrix.  $\mathbf{0}$  (or  $\mathbf{1}$ ) denotes a vector composed of 0 (or 1).  $\mathbf{0}_{N \times N}$  denotes a  $N \times N$ -dimensional matrix composed of 0.  $\lceil \frac{a}{b} \rceil$  denotes the smallest integer greater than or equal  $\frac{a}{b}$ .  $[\cdot]_{ij}$  denotes the  $ij$ -th entry of a matrix.  $\|\cdot\|$  denotes the spectral norm of a matrix or the 2-norm of a vector.  $\|\cdot\|_\infty$  denotes the induced  $\infty$ -norm of a matrix or the  $\infty$ -norm of a vector.  $|\cdot|$  denotes the module of a scalar.  $v = O(u)$  implies that there exists a constant  $\alpha > 0$  such that  $|v| \le \alpha |u|$ . For two sequences  $\{v(t)\}_{t \ge 0}$  and  $\{u(t)\}_{t \ge 0}$ ,  $v(t) = o(u(t))$  means that  $\lim_{t \to \infty} \frac{|v(t)|}{|u(t)|} = 0$ .

## 2. Preliminaries and problem formulation

### 2.1. Some notions from graph theory

Denote  $\mathcal{G} = \{\mathcal{V}, \mathcal{E}, \mathcal{A}\}$  as a digraph.  $\mathcal{V} = \{1, \dots, N\}$  represents the node set.  $\mathcal{E} \subset \mathcal{V} \times \mathcal{V}$  represents the edge set.  $\mathcal{A}$  represents the weighted adjacency matrix. Node  $i$  is called a neighbor of node  $j$  if  $(i, j) \in \mathcal{E}$ . The set of node  $i$ 's all neighbors is represented by  $\mathcal{N}_i$ . Denote  $a_{ij} \ge 0$  as the weighting on the edge  $(j, i)$ . It is assumed that  $a_{ii} = 0$ .  $\mathcal{A}$  is defined as  $[\mathcal{A}]_{ij} = a_{ij}$ . The Laplacian matrix  $L \in \mathbb{R}^{N \times N}$  of digraph  $\mathcal{G}$  is defined as  $[L]_{ii} = \sum_{j=1}^N a_{ij}$  and  $[L]_{ij} = -a_{ij}$  for  $i \neq j$ . A directed path from nodes  $i_1$  to  $i_l$  is an ordered sequence of distinct edges of  $\mathcal{G}$  in the form of  $(i_1, i_2), (i_2, i_3), \dots, (i_{l-1}, i_l)$ . Digraph  $\mathcal{G}$  is called rooted (at a node  $v \in \mathcal{V}$ ) if for each other node  $j \in \mathcal{V}$ , there exists a directed path from  $v$  to  $j$ .  $\mathcal{G}$  is called a leader-following topology if  $\mathcal{G}$  contains only one root node. The digraph sequence  $\{\mathcal{G}(k) = \{\mathcal{V}, \mathcal{E}(k), \mathcal{A}(k)\}, k \in \mathbb{N}\}$  is called uniformly rooted (UR) if there exists an integer sequence  $0 = s_0 < s_1 < \dots < s_k < s_{k+1} < \dots$  such that  $1 \le s_{k+1} - s_k \le K < \infty, K \in \mathbb{N}^+$  and  $\hat{\mathcal{G}}_{s_k} = \bigcup_{m=0}^{s_{k+1}-s_k-1} \mathcal{G}(s_k + m)$  are rooted for all  $k \in \mathbb{N}$ .

### 2.2. Drift compensation in time synchronization

Consider a WSN of  $N$  nodes described by topology  $\mathcal{G}$ . Each node  $i \in \mathcal{V}$  in the network has its own local clock with dynamics being given by:

$$\tau_i(t) = \alpha_i t + \beta_i, \quad (1)$$

where  $t$ ,  $\tau_i(t)$ ,  $\alpha_i > 0$  and  $\beta_i$  are the absolute reference time, the local clock, the local clock drift and the offset, respectively. The parameters  $\alpha_i$  and  $\beta_i$  are unknown for node  $i$ . The goal of time synchronization of a WSN is to synchronize all nodes with respect to a virtual reference clock  $\bar{\tau}(t) = \bar{\alpha}t + \bar{\beta}$ . To achieve this goal, each node's local clock keeps an estimation of the virtual clock using an affine function described by

$$\hat{\tau}_i(t) = \hat{\alpha}_i(t)\tau_i(t) + \hat{\beta}_i(t), \quad (2)$$

where  $\hat{\alpha}_i(t)$  and  $\hat{\beta}_i(t)$  are compensations of the drift and offset of node  $i$  at time  $t$ , respectively. Since  $\hat{\tau}_i(t) = \bar{\tau}(t)$  implies that the virtual drift  $\hat{\alpha}_i(t)\alpha_i = \bar{\alpha}$  and  $\hat{\beta}_i(t) + \hat{\alpha}_i(t)\beta_i = \bar{\beta}$ . Thus, we can see from the perspective of the consensus that the time synchronization problem is equivalent to the consensus problem with respect to  $\hat{\alpha}_i(t)\alpha_i$  and  $\hat{\beta}_i(t) + \hat{\alpha}_i(t)\beta_i$ . Since the offset compensation problem has been well solved in existing works (e.g., Schenato and Fiorentin (2011), Tian et al. (2020)), here we only consider the drift compensation problem, which means the goal of this paper is to design the drift compensation  $\hat{\alpha}_i(t)$ ,  $\forall i \in \mathcal{V}$ , such that for all  $i \in \mathcal{V}$ , the virtual drift satisfies  $\lim_{t \to \infty} \hat{\alpha}_i(t)\alpha_i = \bar{\alpha}$ . Then, the partial time synchronization error with drift compensation between arbitrary two different nodes  $i, j$  (denoted by  $err_{ij}(t)$ ) can be expressed as

$$err_{ij}(t) = \hat{\alpha}_i(t)\tau_i(t) - \hat{\alpha}_j(t)\tau_j(t). \quad (3)$$

**Definition 1.** The bounded partial time synchronization with drift compensation is said to be achieved in a network if there exist  $\varepsilon > 0$  and  $t_f > 0$  such that  $|err_{ij}(t)| < \varepsilon$  for all  $t > t_f$  and all  $i, j \in \mathcal{V}$ .

### 2.3. Communication protocol

In this paper, the pseudo-periodic broadcast communication protocol is adopted for the network (Fagnani & Zampieri, 2007). Each node  $i$  is assumed to broadcast its local time  $\tau_i(t_l^i)$  with the broadcast period  $\hat{T}$  by its local clock i.e., the transmission instants  $t_l^i$ ,  $l \in \mathbb{N}$  for node  $i$  are defined as  $\tau_i(t_l^i) = l\hat{T}$  or equivalently

$$t_l^i = \frac{l\hat{T} - \beta_i}{\alpha_i} = l\hat{T}_i - \beta_i/\alpha_i, \quad (4)$$

where  $\hat{T}_i = \hat{T}/\alpha_i$ . Obviously,  $\hat{T}$  is pseudo-periodic with the real sending periodic being  $\hat{T}_i$  for node  $i$ . Suppose that the node  $j$  receives the  $l$ th packet  $\tau_i(t_l^i)$  from its neighboring node  $i$  at its local time  $\tau_j(t_l^{id})$  and immediately records in its memory the triple  $(l, \tau_j(t_l^{id}), \tau_i(t_l^i))$ . When considering communication delays, it holds that  $t_l^{id} > t_l^i$ . The time-delay from node  $i$  to node  $j$  is assumed to be unknown, which is denoted as

$$d_{ji}(t_l^{id}) = t_l^{id} - t_l^i. \quad (5)$$

In this paper, it is assumed that  $d_{ji}(t_l^{id})$ ,  $\forall j \in \mathcal{V}, \forall i \in \mathcal{N}_j$ , is a random variable, which takes the value from an interval with the upper bound and lower bound being denoted by  $M_{ji}$  and  $m_{ji}$ , respectively. Here, it is assumed that for all  $i \in \mathcal{N}_j$ , the delay bounds  $M_{ji}$  and  $m_{ji}$  are known for node  $j$ , for example, by detecting the maximal or minimal round-trip delay. Here, denote  $M_d = \max_{i,j \in \mathcal{V}} M_{ji}$  and  $m_d = \min_{i,j \in \mathcal{V}} m_{ji}$  respectively as the maximum and minimum communication delay between arbitrary two nodes in the network.

When the pseudo-periodic broadcast communication protocol is adopted, it will inevitably lead to a time-varying interaction topology  $\mathcal{G}(t_k)$  between nodes even if the WSN's topology  $\mathcal{G}$  is fixed, where  $t_k \in \mathbb{R}$  is the updating instant of the drift compensation algorithm operated in the node. It should be noted that

$\mathcal{G}$  being rooted is a necessary condition to achieve the consensus for all virtual drifts (Cao, Morse, & Anderson, 2008; Olfati-Saber & Murray, 2004). If  $\mathcal{G}$  is rooted, the topology sequence constructed by  $\mathcal{G}(t_k)$  will be UR under such communication protocol, which corresponds to the weakest topology to achieve the consensus with time-varying topologies. Otherwise, there does not exist the information transmission from one node to all other nodes in a bounded interval. As a result, the consensus will not be achieved. Without loss of generality, it is assumed that  $\mathcal{G}$  is a non-leader-following topology. Under the pseudo-periodic broadcast communication protocol, the concern of this paper is to design a fully distributed drift compensation algorithm that can be rigorously proved to achieve the bounded partial time synchronization for the WSN.

## 3. Drift compensation algorithm design and convergence conclusion

### 3.1. Drift compensation algorithm design

Substituting (1) into (3), we can obtain

$$err_{ij}(t) = (\hat{\alpha}_i(t)\alpha_i - \hat{\alpha}_j(t)\alpha_j)t + \hat{\alpha}_i(t)\beta_i - \hat{\alpha}_j(t)\beta_j. \quad (6)$$

To achieve the bounded partial time synchronization with drift compensation, by (6), it is quite clear that the designed drift compensation algorithm should guarantee that  $|\hat{\alpha}_i(t)\alpha_i - \hat{\alpha}_j(t)\alpha_j|$ ,  $\forall i, j \in \mathcal{V}$ , converges to zero at a rate no slower than  $O(1/t)$ .

Under the pseudo-periodic broadcast communication protocol, it is assumed that node  $j$  gets successively the packet from node  $i$  and records in its memory the triples  $(0, \tau_j(t_0^{id}), \tau_i(t_0^i)), (1, \tau_j(t_1^{id}), \tau_i(t_1^i)), \dots, (l, \tau_j(t_l^{id}), \tau_i(t_l^i)), \dots$ , where  $l$  is the sending order of node  $i$ . Let  $t = t_l^{id}$ , the constant gain drift compensation algorithm is designed as follows:

$$\hat{\alpha}_j(t^{+}) = (1 - c)\hat{\alpha}_j(t) + c(\hat{\alpha}_{ij}(l))^{-1}\hat{\alpha}_i(t_l^i), \quad (7)$$

where  $c > 0$  is a constant to be designed and the initial estimation  $\hat{\alpha}_j(0)$  can be set as an arbitrarily given positive constant. In (7),  $\hat{\alpha}_{ij}(l)$  represents the estimation for the relative drift  $\alpha_{ij} \triangleq \alpha_j/\alpha_i$ , which is designed via a threshold strategy shown as follows:

- if  $\hat{\alpha}_j(t_l^{id}) \le h_j^1$  and  $\tau_j(t_l^{id}) - \tau_i(t_0^{id}) - g_{ji} > 0$ ,

$$\hat{\alpha}_{ij}(l) = \frac{\tau_j(t_l^{id}) - \tau_j(t_0^{id}) - g_{ji}}{\tau_i(t_l^i) - \tau_i(t_0^i)}; \quad (8)$$

- if  $h_j^1 < \hat{\alpha}_j(t_l^{id}) \le h_j^2$  and  $\tau_j(t_l^{id}) - \tau_i(t_0^{id}) > 0$ ,

$$\hat{\alpha}_{ij}(l) = \frac{\tau_j(t_l^{id}) - \tau_j(t_0^{id})}{\tau_i(t_l^i) - \tau_i(t_0^i)}; \quad (9)$$

- for other cases,

$$\hat{\alpha}_{ij}(l) = \frac{\tau_j(t_l^{id}) - \tau_j(t_0^{id}) + g_{ji}}{\tau_i(t_l^i) - \tau_i(t_0^i)}. \quad (10)$$

In (8), (9) and (10), the parameter  $g_{ji}$  is a bounded constant to be designed,  $h_j^1$  and  $h_j^2$  with  $h_j^2 \ge h_j^1$ , are two arbitrarily given positive constants. In this paper, (8), (9) and (10) are called the dual-threshold relative drift estimator.

Since  $g_{ji}$  is bounded and  $\tau_j(t_l^{id}) - \tau_j(t_0^{id}) \to \infty$  as  $l \to \infty$ , we can obtain that there exists  $l_0 > 0$  such that  $\tau_j(t_l^{id}) - \tau_j(t_0^{id}) - g_{ji} > 0$  for all  $l \ge l_0$ . Then, the dual-threshold relative drift estimator (8), (9) and (10) will become for all  $l \ge l_0$ :

$$\hat{\alpha}_{ij}(l) = \begin{cases} \frac{\tau_j(t_l^{id}) - \tau_j(t_0^{id}) - g_{ji}}{\tau_i(t_l^i) - \tau_i(t_0^i)}, & \text{if } \hat{\alpha}_j(t_l^{id}) \le h_j^1; \\ \frac{\tau_j(t_l^{id}) - \tau_j(t_0^{id})}{\tau_i(t_l^i) - \tau_i(t_0^i)}, & \text{elseif } h_j^1 < \hat{\alpha}_j(t_l^{id}) \le h_j^2; \\ \frac{\tau_j(t_l^{id}) - \tau_j(t_0^{id}) + g_{ji}}{\tau_i(t_l^i) - \tau_i(t_0^i)}, & \text{else.} \end{cases}$$

**Remark 1.** It should be noted that in the dual-threshold relative drift estimator,  $h_j^1$  and  $h_j^2$  can be set as  $h_j^1 = h_j^2$ . For this case, (9) can be dropped. As for the computational complexity, the proposed algorithm requires each node to run (7) and one of (8)–(10) in each update. Since all updates are finished in one step with basic arithmetic/logical operations on scalars, the computational complexity of our algorithm is  $O(1)$ . As for the space complexity, in addition to the basic algorithm parameters, the proposed algorithm only requires each node to store the first clock information received from its neighbors and the corresponding information of its own, the space complexity in the worst case is  $O(N)$  which corresponds to the case that the node has  $N - 1$  neighbors.

### 3.2. Brief introduction on the drift compensation in LSTS, DCBTS and SSTS algorithms

In LSTS algorithm, the drift compensation part is designed as

$$\hat{\alpha}_j(t^+) = (1 - \frac{\rho_a}{(1+l)^u})\hat{\alpha}_j(t) + \frac{\rho_a}{(1+l)^u}\hat{\alpha}_j^{-1}(t^+)\hat{\alpha}_i(t), \quad (11)$$

where  $u \in (0, 1)$  and  $\rho_a \in (0, 1)$ . In (11),  $\hat{\alpha}_j(t^+)$  is the estimation for  $\alpha_{ij}$ , which is designed as

$$\begin{cases} \hat{\alpha}_j(t^+) = (1 - \rho_e(l))\hat{\alpha}_j(t) + \rho_e(l)\hat{\alpha}_j(l), \\ \hat{\alpha}_j(l) = \frac{\hat{\tau}_j(t_j^{id}) - \hat{\tau}_j(t_0^{id})}{\hat{\tau}_i(t_j^{id}) - \hat{\tau}_i(t_0^{id})}, \end{cases} \quad (12)$$

where  $\rho_e(l) = \frac{l^2}{1+l^2+\dots+l^p}$  and  $\hat{\alpha}_j(0) = 1$ .

In DCBTS algorithm, the drift compensation part is designed as

$$\hat{\alpha}_j(t^+) = (1 - \rho_a)\hat{\alpha}_j(t) + \rho_a\hat{\alpha}_j^{-1}(t^+)\hat{\alpha}_i(t), \quad (13)$$

where  $\rho_a \in (0, 1)$ . In (13),  $\hat{\alpha}_j(t^+)$  is the estimation for  $\alpha_{ij}$ , which is designed as

$$\begin{cases} \hat{\alpha}_j^{-1}(t^+) = (1 - \rho_e)\hat{\alpha}_j^{-1}(t) + \rho_e\hat{\alpha}_j^{-1}(l), \\ \hat{\alpha}_j(l) = \frac{\hat{\tau}_j(t_j^{id}) - \Omega_j(l-1)}{\hat{\tau}_i(t_j^{id}) - \Omega_j(l-1)}, \\ \Omega_j(l) = \frac{1}{l+1}\Omega_j(l-1) + \frac{1}{l+1}\hat{\tau}_j(t_j^{id}), \\ \Omega_j(l) = \frac{1}{l+1}\Omega_j(l-1) + \frac{1}{l+1}\hat{\tau}_j(t_j^{id}), \end{cases} \quad (14)$$

where  $\rho_e \in (0, 1)$ ,  $\hat{\alpha}_j(t_0) = 1$ ,  $\Omega_j(0) = \hat{\tau}_j(t_0^{id})$  and  $\Omega_j(0) = \hat{\tau}_j(t_0^{id})$ .

In SSTS algorithm, the drift compensation part is designed as

$$\hat{\alpha}_j(t^+) = (1 - a(l)\rho_a)\hat{\alpha}_j(t) + a(l)\rho_a\hat{\alpha}_j^{-1}(l)\hat{\alpha}_i(t), \quad (15)$$

where  $\rho_a \in (0, 1)$  and  $a(l) = l^{-u}$  with  $u \in (0, 1)$ . In (15),  $\hat{\alpha}_j(l)$  is the estimation for  $\alpha_{ij}$ , which is estimated by

$$\begin{cases} \hat{\theta}(l) = \hat{\theta}(l-1) + K(l)(\hat{\tau}_j(t_j^{id}) - h^T(l)\hat{\theta}(l-1)), \\ K(l) = \frac{\Sigma(l-1)h(l)}{1+h^T(l)\Sigma(l-1)h(l)}, \\ \Sigma(l) = (I - K(l)h^T(l))\Sigma(l-1), \end{cases} \quad (16)$$

where  $\hat{\theta}$  is the estimation for  $\theta = [\alpha_{ij}, \beta_{ij}]^T$  with  $\beta_{ij} = (\beta_j - \beta_i\alpha_j/\alpha_i)$ ,  $\hat{\theta}(1) = ([\hat{\tau}_j(t_1^{id}) - \hat{\tau}_j(t_0^{id})/\hat{T}, \hat{\tau}_j(t_0^{id})]^T$  and  $\Sigma(1) = (H^T(1)H(1))^{-1}$  with  $H(1) = [h(0), h(1)]^T$ .

**Remark 2.** By comparing the above mentioned drift compensation algorithms and the one proposed in this paper, it can be seen that the design differences are mainly reflected in two aspects: the gain design in the update equation of the drift compensation  $\hat{\alpha}_j(t)$ ,  $\forall j \in \mathcal{V}$  and the estimation for the relative drift  $\alpha_{ij}$ ,  $\forall i, j \in \mathcal{V}$ . For the former, our algorithm and the drift compensation part in DCBTS algorithm adopts the constant gain, which has less storage and computational complexity compared with the decaying gain design adopted in LSTS algorithm and SSTS algorithm. For the later, our algorithm selects one of (8)–(10) to run in each update by adding two comparison operations, which still has less computational complexity especially compared with the relative drift estimator designed in DCBTS algorithm (i.e., (14))

and SSTS algorithm (i.e., (16)). If  $\hat{g}_{ji} = 0$ ,  $\forall i, j \in \mathcal{V}$  in (8) and (10), the dual-threshold relative drift estimator reduces to the unfiltered relative drift estimator in LSTS algorithm (i.e.,  $\hat{\alpha}_j(l)$  given by (12)), which ensures the perturbation caused by the communication delay to be polynomially decaying in the whole consensus process.

### 3.3. Convergence conclusion

Under the pseudo-periodic broadcast protocol, by (4), we have  $t_j^i - t_0^i = l\hat{T}_i$ . Then, by (1) and (5), we have

$$\begin{aligned} \frac{\tau_j(t_j^{id}) - \tau_j(t_0^{id})}{\tau_i(t_j^{id}) - \tau_i(t_0^{id})} &= \frac{\alpha_j(t_j^i + d_{ji}(t_j^{id})) - t_0^i - d_{ji}(t_0^{id})}{\alpha_i(t_j^i - t_0^i)} \\ &= \frac{\alpha_j(t_j^i - t_0^i) + \alpha_j(d_{ji}(t_j^{id}) - d_{ji}(t_0^{id}))}{\alpha_i(t_j^i - t_0^i)} \\ &= \frac{\alpha_j}{\alpha_i}(1 + \frac{d_{ji}(t_j^{id}) - d_{ji}(t_0^{id})}{l\hat{T}_i}). \end{aligned} \quad (17)$$

Then, by (17) and through some simple calculations, (8), (9) and (10) can be rewritten as

$$\hat{\alpha}_{ij}(l) = \frac{\alpha_j}{\alpha_i}(1 - \hat{d}_{ji}(l)), \quad l = 1, 2, \dots, \quad (18)$$

$$\text{where } \hat{d}_{ji}(l) = \begin{cases} \frac{-d_{ji}(t_j^{id}) - \hat{g}_{ji} - d_{ji}(t_0^{id})}{l\hat{T}_i} & \text{under (8),} \\ \frac{-d_{ji}(t_j^{id}) - d_{ji}(t_0^{id})}{l\hat{T}_i} & \text{under (9),} \\ \frac{-d_{ji}(t_j^{id}) + \hat{g}_{ji} - d_{ji}(t_0^{id})}{l\hat{T}_i} & \text{under (10)} \end{cases} \quad \text{and } \hat{g}_{ji} = \frac{\hat{g}_{ji}}{\alpha_j}. \text{ Let}$$

$t = t_j^{id}$ , it follows from (7) that

$$\hat{\alpha}_j(t^+)\alpha_j = (1 - c)\hat{\alpha}_j(t)\alpha_j + c(1 + \frac{\hat{d}_{ji}(l)}{1 - \hat{d}_{ji}(l)})\hat{\alpha}_i(t_j^i)\alpha_i. \quad (19)$$

Let  $\{t_k^j\}_{k \ge 0}$  denote the update time sequence of node  $j$  with respect to the drift compensation. Under the pseudo-periodic broadcast protocol, if each  $j \in \mathcal{V}$  has at least one neighbor, there must exist positive constants  $T_1, T_2$  such that  $T_1 \le t_{k+1}^j - t_k^j \le T_2$ , where an upper bound of  $T_2$  can be determined as  $M_d + \max_{j \in \mathcal{V}} \hat{T}_j$  if there is no packet loss. Now, we can integrate all nodes' update time into one ordered sequence  $\{t_k\}_{k \in \mathbb{N}} = \{t_k^j | j \in \mathcal{V}\}_{k \in \mathbb{N}}$  based on the update instant. Then,  $t_k$  can be regarded as an update instant for the whole network with  $k$  corresponding to the  $k$ th update. It is assumed that at time  $t_k$ ,  $j$  receives the packet  $(l_k^j, \tau_i(t_k^j), \hat{\alpha}_i(t_k^j))$

from its neighbor  $i$ , where  $l_k^j$  represents the sending order of the packet received by  $j$  from  $i$  at  $t_k$ . Note that  $\hat{\alpha}_i(t_k^j)$  can be represented as  $\hat{\alpha}_i(t_{k-p_{ji}(k)})$  due to the boundedness of the delay, where  $p_{ji}(k)$  is a non-negative integer and is bounded by  $\max_{j \in \mathcal{V}} \lceil \frac{M_d}{\hat{T}_j} \rceil (N - 1)$  under the simple calculation. Then, (19) can be represented as

$$\begin{aligned} \hat{\alpha}_j(t_{k+1})\alpha_j &= (1 - c)\hat{\alpha}_j(t_k)\alpha_j \\ &\quad + c(1 + \delta_{ji}(t_k))\hat{\alpha}_i(t_{k-p_{ji}(k)})\alpha_i, \end{aligned} \quad (20)$$

where  $\delta_{ji}(t_k) = \hat{d}_{ji}(l_k^j)/(1 - \hat{d}_{ji}(l_k^j))$  is a multiplicative uncertainty. For convenience of the notation, rewrite  $k$  as  $t_k$  and  $k - p_{ji}(k)$  as  $t_{k-p_{ji}(k)}$  in (20). Denote  $x_j(k) = \hat{\alpha}_j(k)\alpha_j$ , one further have

$$\begin{aligned} x_j(k+1) &= (1 - c)x_j(k) \\ &\quad + c(1 + \delta_{ji}(k))x_i(k - p_{ji}(k)). \end{aligned} \quad (21)$$

For the multiplicative uncertainty  $\delta_{ji}(k)$  caused by the delay, its property is characterized by the following proposition.

**Proposition 1.** Suppose that  $\hat{g}_{ji} \ge (M_{ji} - m_{ji})\alpha_j$ ,  $\forall j \in \mathcal{V}$ ,  $i \in \mathcal{N}_j$ . Then, under the estimator (8), (9) or (10), for all  $j \in \mathcal{V}$ ,  $i \in \mathcal{N}_j$ ,  $k \in$

$\mathbb{N}^+$ , there exists a bounded constant  $K > 0$  such that

$$|\delta_{ji}(k)| \le \frac{K}{k} \left( \frac{g_{ji}}{\alpha_j} + M_{ji} - m_{ji} \right). \quad (22)$$

Besides, it always holds that  $\delta_{ji}(k) > 0$  under estimator (8) and  $\delta_{ji}(k) \in (-1, 0)$  under estimator (10).

The proof of this proposition is given in Appendix A. Based on Proposition 1, we can see that the designed drift compensation algorithm (7) exists the polynomially decaying multiplicative uncertainty. From (21), it can be seen that the multiplicative uncertainty will have a great influence on the convergence of the drift compensation algorithm. It should be noted that in the drift compensation part of LSTS, DCBTS and SSTS algorithms (see, (11), (13) and (15) for details), there also exists the multiplicative uncertainty caused by random delays. Though some filters/estimators (see, (12), (14) and (16) for details) are designed to inhibit the uncertainty, the final convergence value of the virtual drift still be influenced. Sometimes, it may converge to a big positive value, where the worst case is that it may converge to a negative value. Compared with these algorithms, by introducing the constant  $g_{ji}$  in the relative drift estimator together with the threshold strategy, the sign of the uncertainty  $\delta_{ji}(k)$  can be controllable under the estimator (8) or (10), as a result, the final convergence value of drift compensation can be controllable.

When communication delays are considered in the drift compensation problem for the WSN, we can clearly see from (21) that the delay not only leads to the asynchronous update (corresponding to a time-varying interaction topology with time delay) but also brings the multiplicative uncertainty to the algorithm model, which is remarkably different from the model with respect to other problems (e.g., the consensus problem (Olfati-Saber & Murray, 2004) and the node localization problem (Huang & Tian, 2018)) where the considered delay only leads to the asynchronous update without bringing the uncertainty.

For the sake of convergence analysis when the delay is considered, some existing drift compensation algorithms (e.g., the ones summarized in Section 3.2) are modeled as a delay-free model (similar to the case that (21) with  $p_{ji}(k) \equiv 0$ ) by introducing two extra assumptions in the pseudo-periodic broadcast communication protocol. The first one is that  $M_d < \min_{i \in \mathcal{V}} \hat{T}_i$ . This assumption requires that each node's broadcast period should be greater than the maximum delay. The second assumption is the introduction of a dormancy slot, which requires each node not to update its virtual clock in a time slot of width  $M_d$  just after its each broadcast instant (see Tian (2015) for details). This assumption will lead to the package loss and lower the synchronization rate. Here, these two assumptions are no more required. Naturally, analysis methods used in these studies are not suitable for the analysis in this paper and the analysis is more complex.

As for the interaction topology  $\mathcal{G}(t_k)$ , as is shown in Section 2.3, the topology is time-varying under the pseudo-periodic broadcast protocol. For convenience of the notation, we can rewrite  $\mathcal{G}(k) = \{\mathcal{V}, \mathcal{E}(k), \mathcal{A}(k)\}$  as  $\mathcal{G}(t_k) = \{\mathcal{V}, \mathcal{E}(t_k), \mathcal{A}(t_k)\}$ , where  $(i, j) \in \mathcal{E}(k)$  means that node  $j$  successfully receives the package from node  $i$  at  $t_k$  and at the same time operates its local drift compensation algorithm. Obviously, it holds that  $\mathcal{G}(k) \subset \mathcal{G}, \forall k \in \mathbb{N}^+$ , where  $\mathcal{G}$  is the topology of the WSN. The following theorem gives the convergence result with respect to the drift compensation algorithm.

**Theorem 1.** Suppose that the gain  $c$  is designed that  $c \in (0, 1)$ ,  $h_j^1$  and  $h_j^2$  are given two positive constants with  $h_j^2 \ge h_j^1$ ,  $g_{ji}$  is designed such that  $g_{ji} \ge (M_{ji} - m_{ji})\alpha_j, \forall i, j \in \mathcal{V}$ , and the topology sequence  $\{\mathcal{G}(k), k \in \mathbb{N}^+\}$  is UR with  $k$  being the  $k$ th update. Then, the drift compensation algorithm (7) with the dual-threshold relative drift estimator ensures that for all  $i \in \mathcal{V}$ , the virtual drift  $\hat{\alpha}_i(k)\alpha_i$

asymptotically converges to a common positive constant, and for all  $i, j \in \mathcal{V}, k \in \mathbb{N}^+$ , there exist bounded constants  $K > 0$  and  $\bar{\rho} \in (0, 1)$  such that

$$|\hat{\alpha}_i(k)\alpha_i - \hat{\alpha}_j(k)\alpha_j| \le \frac{K}{k} \left( \frac{\bar{g} + M_d - m_d}{(1 - \bar{\rho})^2} \right) + o\left(\frac{1}{k}\right), \quad (23)$$

where  $\bar{g} = \max_{i, j \in \mathcal{V}} \frac{g_{ji}}{\alpha_j}$ .

The proof of Theorem 1 is given in Section 4.1. Through the proof process, it can be clearly seen that the convergence value of  $\hat{\alpha}_i(k)$  is controllable by regulating the value of  $h_j^1$  and  $h_j^2$  and is not affected by the delay.

Now, the partial time synchronization error with the proposed drift compensation algorithm will be considered. By (6) and (23), we can obtain

$$\begin{aligned} |\text{err}_{ij}(k)| &\le |\hat{\alpha}_i(k)\alpha_i - \hat{\alpha}_j(k)\alpha_j| k + |\hat{\alpha}_i(k)\beta_i - \hat{\alpha}_j(k)\beta_j| \\ &\le |\hat{\alpha}_i(k)\alpha_i - \hat{\alpha}_j(k)\alpha_j| k \\ &\quad + |\hat{\alpha}_i(k)\beta_i - \hat{\alpha}_j(k)\beta_j| + |\hat{\alpha}_i(k)\beta_j - \hat{\alpha}_j(k)\beta_j| \\ &\le |\hat{\alpha}_i(k)\alpha_i - \hat{\alpha}_j(k)\alpha_j| k + |\hat{\alpha}_i(k)| |\beta_i - \beta_j| \\ &\quad + |\hat{\alpha}_i(k) - \hat{\alpha}_j(k)| |\beta_j|. \end{aligned} \quad (24)$$

By (23), for all  $i, j \in \mathcal{V}, k \in \mathbb{N}^+$ , we can conclude that

$$\begin{aligned} |\text{err}_{ij}(k)| &\le K \left( \frac{\bar{g} + M_d - m_d}{(1 - \bar{\rho})^2} \right) + \sup_{k \in \mathbb{N}} \max_{i, j \in \mathcal{V}} (|\hat{\alpha}_i(k)| |\beta_i - \beta_j| \\ &\quad + |\hat{\alpha}_i(k) - \hat{\alpha}_j(k)| |\beta_j|) \\ &\le K \left( \frac{\bar{g} + M_d - m_d}{(1 - \bar{\rho})^2} \right) + \sup_{k \in \mathbb{N}} \max_{i, j \in \mathcal{V}} |\hat{\alpha}_i(k)| |\beta_i - \beta_j| + O\left(\frac{1}{k}\right), \end{aligned} \quad (25)$$

where parameters  $\bar{g}, \bar{\rho}$  are the same as ones given in Theorem 1. (25) indicates that the drift compensation algorithm (7) can achieve the bounded partial time synchronization.

**Remark 3.** (25) shows that the value  $\hat{\alpha}_i(k)$ , the delay range  $M_d - m_d$ , the designed  $g_{ji}$  and the parameter  $\bar{\rho}$  all will affect the partial time synchronization accuracy, where  $\bar{\rho}$  reflects the convergence rate of (21) for the multiplicative uncertainty free case (i.e., (21) with  $\delta_{ji}(k) \equiv 0$ ) and the value of  $M_d - m_d$  depends on the range of the delay. If the fluctuation range of delay increases (i.e.,  $M_d - m_d$  increases), the synchronization performance will deteriorate. If  $m_d$  and  $M_d$  are nearly the same, a good synchronization performance can still be achieved even if  $M_d$  is large. The effect of the accuracy caused by parameters  $\bar{\rho}$  and  $M_d - m_d$  is usually uncontrollable. For  $|\hat{\alpha}_i(k)|$  or  $g_{ji}$ , a bigger value may correspond to a bigger synchronization error. It should be noted that if convergence values of  $\hat{\alpha}_i(k)$  obtained under our algorithm and some existing algorithms are nearly the same, our algorithm may have a bigger synchronization error due to the introduction of  $g_{ji}$  in (25). However, for almost all existing algorithms that consider the delay (e.g., the DCBTS algorithm and the SSTS algorithm), the obtained final convergence value  $\hat{\alpha}_i(k)$  will be seriously affected by the delay and there exists the case that a big convergence value of  $|\hat{\alpha}_i(k)|$  can be obtained. Especially if the variance of the delay is big, the probability of occurrence for such case will be big. If the convergence value of  $\hat{\alpha}_i(k)$  is big, the effect of  $g_{ji}$  can be ignored. A remarkable advantage of the new proposed algorithm in this paper is that the convergence value  $\hat{\alpha}_i(k)$  is controllable, which means that it will be robust to the delay and may have smaller partial time synchronization error if the variance of the random delay is big.

## 4. Modeling and convergence analysis

### 4.1. A preliminary lemma

**Lemma 1.** Suppose that  $|f(k)| \le \frac{K}{k}$ ,  $\forall k \in \mathbb{N}^+$  with  $K > 0$  being a bounded constant. Then, given any  $\rho \in (0, 1)$ , the following statements are true:

- (i)  $\sum_{m=1}^{k} \rho^{k-m} |f(m)| \le \frac{1}{k} \frac{K_1}{(1-\rho)^2}$ ;
- (ii)  $\prod_{m=1}^{k} (\rho + f(m))$  is  $O(\gamma^k)$  with  $\gamma \in (0, 1)$ .

This lemma is summarized from Lemma 1 and Lemma 2 given in Wang and Tian (2017).

### 4.2. Augmented model of the drift compensation algorithm

Let  $\mathcal{J}_k$  represent the set of nodes that update the estimation at  $k$ . Let  $p = \sup_{k \in \mathbb{N}} \max_{i, j \in \mathcal{V}} p_{ij}(k)$ . Since the communication delay is bounded, we can obtain that  $p$  is bounded. Given a time-varying matrix  $A(k)$  with  $[A(k)]_{ji}$  being defined as follows:

$$\begin{cases} [A(k)]_{ji} = \begin{cases} c, & i \in \mathcal{N}_j(k), \\ 0, & i \notin \mathcal{N}_j(k), i \neq j, \\ 1-c, & i = j, \end{cases} & \text{if } j \in \mathcal{J}_k, \\ [A(k)]_{ji} = \begin{cases} 0, & i \neq j, \\ 1, & i = j, \end{cases} & \text{if } j \notin \mathcal{J}_k, \end{cases} \quad (26)$$

Given a disturbance matrix  $\Delta(k)$  with  $[\Delta(k)]_{ji}$  being defined as follows:

$$\begin{cases} [\Delta(k)]_{ji} = \begin{cases} c \delta_{ji}(k), & i \in \mathcal{N}_j(k), \\ 0, & \text{otherwise}, \end{cases} & \text{if } j \in \mathcal{J}_k, \\ [\Delta(k)]_{ji} = 0, & i = 1, \dots, N, \quad \text{if } j \notin \mathcal{J}_k. \end{cases} \quad (27)$$

In order to facilitate the description, for a matrix  $C \in \mathbb{R}^{N \times N}$ , let  $\Delta(C) = \{\tilde{C} : [\tilde{C}]_{ij}$  equals  $[C]_{ij}$  or 0}. Now, based on (26) and (27), (21) can be aggregated into

$$\tilde{x}(k+1) = (\tilde{A}(k) + \tilde{\Delta}(k))\tilde{x}(k), \quad (28)$$

where  $\tilde{x}(k) = [x^T(k), \dots, x^T(k-p)]^T$  with  $x(k) = [x_1(k), \dots, x_N(k)]^T$ ,

$$\tilde{A}(k) = \begin{bmatrix} A_0(k) & A_1(k) & \cdots & A_{p-1}(k) & A_p(k) \\ I & \mathbf{0}_{N \times N} & \cdots & \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} \\ \mathbf{0}_{N \times N} & I & \cdots & \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} \\ \vdots & \vdots & \ddots & \vdots & \vdots \\ \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} & \cdots & I & \mathbf{0}_{N \times N} \end{bmatrix}$$

and

$$\tilde{\Delta}(k) = \begin{bmatrix} \Delta_0(k) & \Delta_1(k) & \cdots & \Delta_{p-1}(k) & \Delta_p(k) \\ \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} & \cdots & \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} \\ \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} & \cdots & \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} \\ \vdots & \vdots & \ddots & \vdots & \vdots \\ \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} & \cdots & \mathbf{0}_{N \times N} & \mathbf{0}_{N \times N} \end{bmatrix}.$$

In (28),  $A_0(k), \dots, A_p(k) \in \Lambda(A(k))$  and satisfy that  $A_0(k) + \cdots + A_p(k) = A(k)$ ; All diagonal entries of  $A_0(k)$  are the same as the one in  $A(k)$ ;  $\Delta_0(k), \dots, \Delta_p(k) \in \Lambda(\Delta(k))$  and satisfy that  $\Delta_0(k) + \cdots + \Delta_p(k) = \Delta(k)$ .

It is noted that for the uncertainty-free case (i.e.,  $\tilde{\Delta}(k) = \mathbf{0}_{N(p+1) \times N(p+1)}$ ), model (28) becomes a standard model in studying the consensus problem for discrete-time MASs with bounded delays or finite packet losses under switching topologies (Cao et al., 2008; Xiao & Wang, 2006). However, the analysis methods given in existing works do not directly solve the consensus problem of model (28).

To do the convergence analysis, a state transformation for  $\tilde{x}(k)$  is provided. Let  $\tilde{x}(k) = \tilde{E}\tilde{x}(k)$ , where  $\tilde{E} = \begin{bmatrix} \Gamma_1 \\ \Gamma \end{bmatrix}$  with  $\Gamma_1 = [1, \mathbf{0}_{1 \times (N(p+1)-1)}]$ ,  $\Gamma = \begin{bmatrix} 1 & -I \end{bmatrix}$ . Then, one has  $\tilde{x}(k) = [\tilde{x}_1(k), e^T(k)]^T$ , where  $e(k) = [\tilde{x}_1(k) - \tilde{x}_2(k), \dots, \tilde{x}_1(k) - \tilde{x}_{N(p+1)}(k)]^T$ . Let  $\tilde{A}(k) = \tilde{E}\tilde{A}(k)\tilde{E}^{-1}$  and  $\tilde{\Delta}(k) = \tilde{E}\tilde{\Delta}(k)\tilde{E}^{-1}$ . Under the simple calculation, for  $\tilde{A}(k)$ , it has the form  $\tilde{A}(k) = \begin{bmatrix} 1 & \tilde{A}_1(k) \\ 0 & \tilde{A}_2(k) \end{bmatrix}$ , where  $\tilde{A}_1(k)$  and  $\tilde{A}_2(k)$  are sub-matrices of  $\tilde{A}(k)$ .  $\tilde{\Delta}(k)$  can be written as  $\tilde{\Delta}(k) = \begin{bmatrix} \tilde{\Delta}_1(k) & \tilde{\Delta}_2(k) \\ \tilde{\Delta}_3(k) & \tilde{\Delta}_4(k) \end{bmatrix}$ , where  $\tilde{\Delta}_1(k) = [\tilde{\Delta}(k)]_{11}$ ,  $\tilde{\Delta}_2(k)$ ,  $\tilde{\Delta}_3(k)$  and  $\tilde{\Delta}_4(k)$  are sub-matrices of  $\tilde{\Delta}(k)$ . Then, under this transformation, (28) will become

$$\begin{cases} \tilde{x}_1(k+1) = (1 + \tilde{\Delta}_1(k))\tilde{x}_1(k) + (\tilde{A}_1(k) + \tilde{\Delta}_2(k))e(k), \\ e(k+1) = (\tilde{A}_2(k) + \tilde{\Delta}_3(k))e(k) + \tilde{\Delta}_4(k)\tilde{x}_1(k). \end{cases} \quad (29)$$

To facilitate the convergence analysis of model (29), we introduce two state transition matrices  $\tilde{R}()$  (corresponding to the uncertainty-free case) and  $\tilde{Q}()$  (corresponding to the uncertainty-existing case) for the model with respect to  $e(k)$  in a certain time interval, which are defined as  $\tilde{R}(m, m) = \tilde{Q}(m, m) = I$ ,  $\tilde{R}(m+i, m) = \tilde{A}_2(m+i)\tilde{R}(m+i, m)$  and  $\tilde{Q}(m+i, m) = (\tilde{A}_2(m+i) + \tilde{\Delta}_4(m+i))\tilde{Q}(m+i, m)$ . By choosing a proper gain  $c \in (0, 1)$ , it can be easily verified that  $A(k)$ ,  $\forall k \in \mathbb{N}^+$ , is a stochastic matrix with each non-zero entry having a positive lower bound, which implies that  $\tilde{A}(k)$ ,  $\forall k \in \mathbb{N}^+$ , is a stochastic matrix with each non-zero entry having a positive lower bound. Then, based on Theorem 2 in Cao, Morse, and Anderson (2008), it can be easily concluded that the consensus of (28) with  $\tilde{\Delta}(k) = \mathbf{0}_{N(p+1) \times N(p+1)}$  can be obtained at an exponential convergence rate if  $\{\mathcal{G}(k), k \in \mathbb{N}^+\}$  is UR. As a result, for the model  $e(k+1) = \tilde{A}_2(k)e(k)$ , we can conclude that  $\|e(k)\|$  exponentially converges to zero. Then, for the convergence property of  $\|\tilde{R}(m_2, m_1)\|$ ,  $m_2 \ge m_1$ , we can obtain the following result directly deduced from Theorem 2 in Cao, Morse, and Anderson (2008).

**Lemma 2.** Suppose that the gain  $c$  is designed that  $c \in (0, 1)$  and the topology sequence  $\{\mathcal{G}(k), k \in \mathbb{N}^+\}$  is UR. Then, for all  $m_2 \ge m_1$ , there exist bounded constants  $K > 0$  and  $\rho \in (0, 1)$  such that  $\|\tilde{R}(m_2, m_1)\| \le K\rho^{m_2-m_1}$ .

Now, based on Lemma 2, the following lemma with respect to the convergence property of  $\|\tilde{Q}(m_2, m_1)\|$  are provided when multiplicative uncertainties are assumed to be polynomially decaying.

**Lemma 3.** Suppose that the gain  $c$  is designed that  $c \in (0, 1)$  and the topology sequence  $\{\mathcal{G}(k), k \in \mathbb{N}^+\}$  is UR. Then, for all  $m_2 \ge m_1$ , there exist bounded constants  $K > 0$  and  $\bar{\rho} \in (0, 1)$  such that  $\|\tilde{Q}(m_2, m_1)\| \le K\bar{\rho}^{m_2-m_1}$  if for all  $i, j \in \mathcal{V}$ ,  $\delta_{ij}(k)$  is  $O(\frac{1}{(1+k)^\mu})$  with  $\mu > 0$ .

Proof of this lemma is given in Appendix B.

Now, it is ready to give the complete proof of Theorem 1.

### 4.3. Proof of Theorem 1

If  $c$  is designed such that  $c \in (0, 1)$ , by (26), we can obtain that  $A(k)$ ,  $\forall k \in \mathbb{N}^+$ , is a stochastic matrix.

Now, the augmented model (28) will be considered. Firstly, it will be proved that  $\|\tilde{x}(k)\|$ ,  $k \in \mathbb{N}$ , is bounded under the given conditions in this theorem. By (26), (27) and Proposition 1, we can conclude that  $[A(k) + \Delta(k)]_{ij} \ge 0$ ,  $\forall i, j \in \mathcal{V}$ , under the relative drift estimator (8) or (10), which implies that in (28),

each entry of  $\bar{A}(k) + \bar{\Delta}(k)$  is non-negative. Together with the fact that  $\hat{\alpha}_i(0) > 0, \forall i \in \mathcal{V}$ , we can conclude that  $\hat{\alpha}_i(k)\alpha_i \ge 0, \forall i \in \mathcal{V}, k \in \mathbb{N}^+$ . Suppose that there exists  $i \in \mathcal{V}$  such that the virtual drift  $\hat{\alpha}_i(k)\alpha_i$  is divergent as  $k \to \infty$ . Then, the virtual drifts of both  $i$ 's neighbors and followers in  $\mathcal{G}$  must be divergent too. Since  $\{\mathcal{G}(k) \subset \mathcal{G}, k \in \mathbb{N}\}$  is UR, it must have that  $\hat{\alpha}_i(k)\alpha_i, \forall i \in \mathcal{V}$  is divergent. Then, there exists a bounded integer  $k_0 > 0$  such that for all  $k \ge k_0$  and  $i \in \mathcal{V}$ ,  $\hat{\alpha}_i(k) > h_i^2$ . Then, for all nodes, the estimator (10) will be adopted. Then, by Proposition 1, we know  $\delta_{ij}(k)$  is  $O(1/k)$  with  $\delta_{ij}(k) \in (-1, 0)$ . Further, by (26) and (27), we can conclude that  $\|A(k) + \Delta(k)\|_\infty \le 1, \forall k \ge k_0$ . Then, we can obtain  $\|\bar{A}(k) + \bar{\Delta}(k)\|_\infty \le 1, \forall k \ge k_0$ , which implies that  $\|\bar{x}(k+1)\|_\infty \le \|\bar{x}(k_0)\|_\infty, \forall k \ge k_0$ . Since  $k_0$  is bounded, we can obtain  $\|\bar{x}(k)\|$  is bounded. Then, we can obtain  $\|\bar{x}(k)\|, \forall k \ge k_0$ , is bounded (i.e.,  $\hat{\alpha}_i(k)\alpha_i$  is bounded), which contradicts the assumption that  $\hat{\alpha}_i(k)\alpha_i$  is divergent. Thus, we can obtain that for all  $k \in \mathbb{N}^+$ , both  $\|x(k)\|$  and  $\|\bar{x}(k)\|$  are bounded.

Now, for model (29), by the second equation in (29), we can obtain that

$$e(k) = \tilde{Q}(k, 0)e(0) + \sum_{m=0}^{k-1} \tilde{Q}(k, m+1)\tilde{\Delta}_3(m)\bar{x}_1(m). \quad (30)$$

Since  $\|\bar{x}(k)\|, \forall k \in \mathbb{N}^+$ , is bounded, we can obtain  $\|\bar{x}_1(k)\|, \forall k \in \mathbb{N}^+$ , is bounded. Then, there exists a bounded constant  $K_1 > 0$  such that

$$\|e(k)\| \le \|\tilde{Q}(k, 0)\| \|e(0)\| + K_1 \sum_{m=0}^{k-1} \|\tilde{Q}(k, m+1)\| \|\tilde{\Delta}_3(m)\|. \quad (31)$$

Based on Proposition 1, we can obtain Lemma 3 holds under the condition in this theorem. Also, by (22) and based on the definitions of  $\Delta(k)$  given by (27),  $\bar{\Delta}(k)$  given by (28),  $\tilde{\Delta}(k)$  and  $\|\tilde{\Delta}_i(k)\|, i = 1, 2, 3, 4$  given above (29), we can further conclude that  $\tilde{\Delta}(k)$ ,  $\bar{\Delta}(k)$  and  $\|\tilde{\Delta}_i(k)\|, i = 1, 2, 3, 4$ , are all  $O(1/k)$  since  $\delta_{ij}(k)$  is  $O(1/k)$ . Then, there must exist a bounded constant  $K_2 > 0$  such that

$$\|\tilde{\Delta}_i(k)\| \le \frac{K_2}{k} (\bar{g} + M_d - m_d), \forall i = 1, 2, 3, 4, \quad (32)$$

where  $\bar{g} = \max_{i,j \in \mathcal{V}} \frac{g_{ij}}{\alpha_j}$ . Then, based on Lemma 3 and Lemma 1, we can conclude that there exist bounded constants  $\bar{\rho} \in (0, 1)$  and  $K_3 > 0$  such that  $\|\tilde{Q}(k, 0)\| \le K_3 \bar{\rho}^k$  and

$$\sum_{m=0}^{k-1} \|\tilde{Q}(k, m+1)\| \|\tilde{\Delta}_3(m)\| \le \frac{K_2 K_3}{k} \left( \frac{\bar{g} + M_d - m_d}{(1 - \bar{\rho})^2} \right), \quad (33)$$

Then, we can obtain that

$$\|e(k)\| \le K_3 \bar{\rho}^k \|e(0)\| + \frac{K_1 K_2 K_3}{k} \left( \frac{\bar{g} + M_d - m_d}{(1 - \bar{\rho})^2} \right). \quad (34)$$

(34) implies that (23) holds.

Now, we will show that  $\bar{x}_1(k), \forall i = 1, \dots, N(p+1)$  finally converges to a common constant. By the first equation in (29), we can obtain

$$|\bar{x}_1(k+1) - \bar{x}_1(k)| \le \|\tilde{\Delta}_1(k)\bar{x}_1(k)\| + \|\bar{A}_1(k) + \tilde{\Delta}_2(k)\| \|e(k)\|. \quad (35)$$

Note that  $\|\tilde{\Delta}_2(k)\|$  is  $O(\frac{1}{k})$  and  $\|\bar{A}_1(k)\|$  is bounded, we can obtain  $\|\bar{A}_1(k) + \tilde{\Delta}_2(k)\|$  is bounded. Since  $\|\bar{x}(k)\|$  is bounded and  $\|\tilde{\Delta}_1(k)\|$  is  $O(\frac{1}{k})$ , we can obtain that  $|\tilde{\Delta}_1(k)\bar{x}_1(k)|$  is  $O(\frac{1}{k})$ . Together with the fact that  $\|e(k)\|$  is  $O(\frac{1}{k})$ , we can obtain that  $|\bar{x}_1(k+1) - \bar{x}_1(k)| \to 0$  at a rate no slower than  $O(\frac{1}{k})$ . Further, together with the fact that  $\bar{x}_1(k)$  is bounded, we can obtain  $\bar{x}_1(k)$  converges to a constant as  $k \to \infty$ . Based on the definition of  $e(k)$  and together with the fact that  $\|e(k)\|$  is  $O(\frac{1}{k})$ , we can conclude that for all  $i = 1, \dots, N(p+1)$ ,  $\bar{x}_1(k)$  converges to a common constant as  $k \to \infty$ .

![Figure 1: The interaction topology of the WSN. It shows two directed graphs, G1 and G2, with 20 nodes each. G1 is a 4x5 grid where each node points to its right and down neighbors. G2 is a rooted tree structure where node 1 is the root, and nodes 2-20 are arranged in levels: level 2 (2,3,4,5), level 3 (6,7,8,9,10), level 4 (11,12,13,14,15), and level 5 (16,17,18,19,20). Root 1 points to nodes 2,3,4,5. Node 2 points to 6,7; 3 to 7,8; 4 to 8,9; 5 to 9,10. Node 6 points to 11,12; 7 to 12,13; 8 to 13,14; 9 to 14,15; 10 to 15. Nodes 11-15 point to nodes 16-20 respectively.](21c78ed8eb23eb76d4a2c9edbe5626bb_img.jpg)

Figure 1: The interaction topology of the WSN. It shows two directed graphs, G1 and G2, with 20 nodes each. G1 is a 4x5 grid where each node points to its right and down neighbors. G2 is a rooted tree structure where node 1 is the root, and nodes 2-20 are arranged in levels: level 2 (2,3,4,5), level 3 (6,7,8,9,10), level 4 (11,12,13,14,15), and level 5 (16,17,18,19,20). Root 1 points to nodes 2,3,4,5. Node 2 points to 6,7; 3 to 7,8; 4 to 8,9; 5 to 9,10. Node 6 points to 11,12; 7 to 12,13; 8 to 13,14; 9 to 14,15; 10 to 15. Nodes 11-15 point to nodes 16-20 respectively.

Fig. 1. The interaction topology of the WSN.

Now, we will show that the common constant is positive. Since all entries of  $\bar{A}(k) + \bar{\Delta}(k)$  are non-negative and  $\hat{\alpha}_i(0) > 0, \forall i \in \mathcal{V}$ , one only needs to show that the common constant is not zero. Suppose that there exists  $i \in \mathcal{V}$  such that the virtual drift  $\hat{\alpha}_i(k)\alpha_i$  converges to zero as  $k \to \infty$ , then the virtual drifts of both  $i$ 's neighbors and followers converge to zero as  $k \to \infty$ . Since  $\{\mathcal{G}(k) \subset \mathcal{G}, k \in \mathbb{N}\}$  is UR, it must have that  $\hat{\alpha}_i(k)\alpha_i, \forall i \in \mathcal{V}$ , converges to zero as  $k \to \infty$ . Then, there exists a bounded integer  $k_1 > 0$  such that for all  $k \ge k_1$  and  $i, j \in \mathcal{V}$ ,  $\hat{\alpha}_i(k) \le h_i^1$  and  $\tau_j(t_i^{id}) - \tau_j(t_i^{td}) - g_{ji} > 0$ . Then, for all nodes, the estimator (8) will be adopted. Then, by Proposition 1, together with (26) and (27), we can conclude that  $\|A(k) + \Delta(k)\|_\infty > 1, \forall k \ge k_1$ . Then, we can obtain  $\|\bar{A}(k) + \bar{\Delta}(k)\|_\infty > 1, \forall k \ge k_1$ , which implies that  $\|\bar{x}(k)\|_\infty$  will increase as  $k$  increases until  $\hat{\alpha}_i(k) > h_i^2$  for some  $i \in \mathcal{V}$ . Since  $\hat{\alpha}_i(k)\alpha_i$  cannot converge to zero under finite iterations with the positive initial value, we can obtain  $\|\bar{x}(k_1)\| > 0$ . Then, we can obtain  $\|\bar{x}(k)\| \ge \|\bar{x}(k_1)\|, \forall k \ge k_1$ , which contradicts the assumption that  $\hat{\alpha}_i(k)\alpha_i$  converges to zero as  $k \to \infty$ . Then, we can conclude that  $\hat{\alpha}_i(k)\alpha_i, \forall i \in \mathcal{V}$ , asymptotically converges to a common positive constant. This completes the proof of Theorem 1.

## 5. Simulation results

In this section, the numerical simulation results will be provided to illustrate the effectiveness of the proposed drift compensation algorithm.

Consider a WSN with 20 nodes, whose interaction topology is described in Fig. 1. Here, two topologies  $\mathcal{G}_1$  and  $\mathcal{G}_2$  will be considered. It can be easily verified that both  $\mathcal{G}_1$  and  $\mathcal{G}_2$  are all the rooted topology.

We use 1 denoting the nominal frequency of the crystal oscillator. The local clock drifts  $\alpha_i, \forall i \in \mathcal{V}$  can be assumed to follow the uniform distribution  $U(0.9, 1.1)$  due to the typical errors for the crystal oscillator. It is expected from the drift compensation algorithm to reach a consensus value of/around 1 for the virtual drift. The broadcast period  $\hat{T}$  is set as 1s. Let  $\text{err}(t) = \max_{i,j \in \mathcal{V}} |\text{err}_{ij}(t)|$ . We will consider the delay that follows uniform distribution or Gaussian distribution with three different means/variances shown as follows:

- (i) all delays follow the uniform distribution  $U(1, 4)$ ;
- (ii) all delays follow the uniform distribution  $U(0.1, 0.4)$ ;
- (iii) all delays follow the Gaussian distribution  $N(3, 1)$ .

In order to guarantee that the virtual drift can finally reach a consensus value of/around 1, the gain  $c$  can be set as  $c = 0.5$ , the parameter  $h_i^1, h_i^2, \forall j \in \mathcal{V}$  can be set as  $h_i^1 = h_i^2 = 1$  to constrain the convergence value of  $\hat{\alpha}_j(t), \forall j \in \mathcal{V}$  based on (8), (9) and (10). As for the parameter  $g_{ji}, \forall i, j \in \mathcal{V}$ , based on Theorem 1, it should satisfy that  $g_{ji} \ge (M_{ji} - m_{ji})\alpha_j$ . Then, for case (i), we can obtain  $M_{ji} = 4, m_{ji} = 1, \forall i, j \in \mathcal{V}$  by a simple calculation and we can set  $g_{ji} = 3.3, \forall i, j \in \mathcal{V}$ . Similarly, for case (ii), we can set

**Table 1**  
Parameters in our algorithm.

| Cases      | $c$ | $h_j^1, \forall j \in \mathcal{V}$ | $h_j^2, \forall j \in \mathcal{V}$ | $g_{ji}, \forall i, j \in \mathcal{V}$ |
|------------|-----|------------------------------------|------------------------------------|----------------------------------------|
| case (i)   | 0.5 | 1                                  | 1                                  | 3.3                                    |
| case (ii)  | 0.5 | 1                                  | 1                                  | 0.33                                   |
| case (iii) | 0.5 | 1                                  | 1                                  | 4.4                                    |

![Figure 2: Trajectories of virtual drifts ̂α_i(t)α_i with three delay cases under the topology G_1. The figure consists of three subplots. The top subplot is for Case i) where the delay follows a uniform distribution U(1,4). The middle subplot is for Case ii) where the delay follows a uniform distribution U(0,1,0.4). The bottom subplot is for Case iii) where the delay follows a Gaussian distribution N(3,1). In all cases, the virtual drifts start at 1 and converge to a steady-state value. The steady-state values are approximately 1 for Case i) and Case iii), and approximately 1.1 for Case ii). The x-axis for all plots is time t/s from 0 to 600. The y-axis is virtual drifts. Each plot includes a legend for the Algorithm in this paper (dashed blue line), Drift compensation part of DCBTS algorithm (dotted red line), and Drift compensation part of SSTS algorithm (solid black line).](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 2: Trajectories of virtual drifts ̂α\_i(t)α\_i with three delay cases under the topology G\_1. The figure consists of three subplots. The top subplot is for Case i) where the delay follows a uniform distribution U(1,4). The middle subplot is for Case ii) where the delay follows a uniform distribution U(0,1,0.4). The bottom subplot is for Case iii) where the delay follows a Gaussian distribution N(3,1). In all cases, the virtual drifts start at 1 and converge to a steady-state value. The steady-state values are approximately 1 for Case i) and Case iii), and approximately 1.1 for Case ii). The x-axis for all plots is time t/s from 0 to 600. The y-axis is virtual drifts. Each plot includes a legend for the Algorithm in this paper (dashed blue line), Drift compensation part of DCBTS algorithm (dotted red line), and Drift compensation part of SSTS algorithm (solid black line).

**Fig. 2.** Trajectories of virtual drifts  $\hat{\alpha}_i(t)\alpha_i$  with three delay cases under the topology  $\mathcal{G}_1$ .

**Table 2**  
Drift compensation parameters in DCBTS, SSTS algorithm.

|       | $\rho_e$     | $\rho_a$ | $a(n)$       |
|-------|--------------|----------|--------------|
| DCBTS | 0.5          | 0.5      | $\backslash$ |
| SSTS  | $\backslash$ | 0.5      | $n^{0.5}$    |

$g_{ji} = 0.33, \forall i, j \in \mathcal{V}$ . For case (iii), since the Gaussian distribution is considered, we can set  $g_{ji} = 4.4, \forall i, j \in \mathcal{V}$  to guarantee that  $g_{ji} \ge (d_{ji}(t_i^{id}) - d_{ji}(t_0^{id}))\alpha_j$  holds with a high probability. The initial estimation of  $\hat{\alpha}_i(0)$  is set as  $\hat{\alpha}_i(0) = 1, \forall i \in \mathcal{V}$ . The parameter in our algorithm is summarized in Table 1.

Firstly, a simulation under topology  $\mathcal{G}_1$  will be provided to verify the effectiveness of the drift compensation algorithm proposed in this paper. By running algorithm (7) with the dual-threshold relative drift estimator (8), (9) and (10) under three different delay cases, we can get the simulation result shown by Fig. 2. One can see from Fig. 2 that all trajectories of virtual drifts  $\hat{\alpha}_i(t)\alpha_i, i \in \mathcal{V}$ , asymptotically converge to a non-zero positive constant under each of three delay cases, where convergence values of the virtual drift under the three cases are nearly the same and all belong to a small neighborhood of 1. This simulation clearly shows that the drift compensation algorithm proposed in this paper is robust to the delay effect.

Next, a comparison among the drift compensation algorithm in this paper, the drift compensation part of DCBTS algorithm (i.e., (13) and (14)) and SSTS algorithm (i.e., (15) and (16)) will be provided. The simulation set and the parameter settings of the algorithm in this paper are the same as ones described in Table 1. For the parameter settings of the drift compensation part of DCBTS algorithm and SSTS algorithm, as corresponding Refs. Tian et al. (2020), Wang et al. (2022) do, they are given in Table 2.

We firstly consider the simulation under topology  $\mathcal{G}_1$ . By respectively running three different drift compensation algorithms under three different delay cases, we can get a simulation result shown by Fig. 3 and Fig. 4. Similarly, we can obtain the simulation shown by Fig. 5 and Fig. 6 if topology  $\mathcal{G}_2$  is considered. One

![Figure 3: Trajectories of virtual drifts ̂α_i(t)α_i with three delay cases under the topology G_1. The figure consists of three subplots. The top subplot is for Case i) where the delay follows a uniform distribution U(1,4). The middle subplot is for Case ii) where the delay follows a uniform distribution U(0,1,0.4). The bottom subplot is for Case iii) where the delay follows a Gaussian distribution N(3,1). In all cases, the virtual drifts start at 1 and converge to a steady-state value. The steady-state values are approximately 1 for Case i) and Case iii), and approximately 1.1 for Case ii). The x-axis for all plots is time t/s from 0 to 600. The y-axis is virtual drifts. Each plot includes a legend for the Algorithm in this paper (dashed blue line), Drift compensation part of DCBTS algorithm (dotted red line), and Drift compensation part of SSTS algorithm (solid black line).](68aa26525c9346e4590a15c75d394e9d_img.jpg)

Figure 3: Trajectories of virtual drifts ̂α\_i(t)α\_i with three delay cases under the topology G\_1. The figure consists of three subplots. The top subplot is for Case i) where the delay follows a uniform distribution U(1,4). The middle subplot is for Case ii) where the delay follows a uniform distribution U(0,1,0.4). The bottom subplot is for Case iii) where the delay follows a Gaussian distribution N(3,1). In all cases, the virtual drifts start at 1 and converge to a steady-state value. The steady-state values are approximately 1 for Case i) and Case iii), and approximately 1.1 for Case ii). The x-axis for all plots is time t/s from 0 to 600. The y-axis is virtual drifts. Each plot includes a legend for the Algorithm in this paper (dashed blue line), Drift compensation part of DCBTS algorithm (dotted red line), and Drift compensation part of SSTS algorithm (solid black line).

**Fig. 3.** Trajectories of virtual drifts  $\hat{\alpha}_i(t)\alpha_i$  with three delay cases under the topology  $\mathcal{G}_1$ .

can clearly see from Fig. 3 and Fig. 5 that if the variance of the delay is big whether it follows uniform distribution or Gaussian distribution, for the drift compensation part of DCBTS algorithm or SSTS algorithm, there exists the case that the convergence value of the virtual drift will no more belong to a small neighborhood of 1 (see the top/bottom subgraph of Fig. 3 or Fig. 5 for details) compared with the algorithm in this paper. Besides, if the variance of the delay is small, there still exists the case that the convergence value under the drift compensation part of SSTS algorithm is still big compared with other two algorithms (see the middle subgraph of Fig. 3 or Fig. 5 for details). One can clearly see from the top/bottom subgraph of Fig. 4 or Fig. 6 that there exists the case that the partial time synchronization error with the drift compensation part of DCBTS algorithm or SSTS algorithm is bigger than the one under the drift compensation part of this paper, where the main reason is that a bigger  $\hat{\alpha}_i(t)\alpha_i$  value is obtained under the two algorithms. One can clearly see from the middle subgraph of Fig. 4 or Fig. 6 that the partial time synchronization error with the drift compensation part of SSTS algorithm is the biggest and the error under algorithms in this paper and DCBTS algorithm are nearly the same. The reason behind is that if the convergence value of the virtual drift is big, a big error will be obtained. Besides, if the convergence value of the virtual drift under algorithms are nearly the same, the introduction of  $g_{ji}$  in our algorithm may lower the partial time synchronization accuracy. This simulation shows that the algorithm in this paper can have a smaller partial time synchronization error in some cases especially if the variance of the delay is big. This simulation verifies the illustration in Remark 3.

## 6. Conclusion

In this paper, the drift compensation problem of time synchronization for WSNs with random bounded communication delays is studied. A new constant gain drift compensation algorithm via threshold design has been proposed while the rigorous convergence analysis has been provided. Also, the partial time synchronization error with this new drift compensation algorithm has been analyzed. Besides, simulations have been provided to illustrate the effectiveness of the proposed algorithm. Compared with most existing algorithms, this new drift compensation algorithm not only can be rigorously proved to be effective under the weakest topology condition (i.e., the UR topology sequence)

![Figure 4: Trajectories of the synchronization error err(t) with three delay cases under the topology G1. The figure consists of three subplots: Case i) delay follows U(1,4), Case ii) delay follows U(0,1,0.4), and Case iii) delay follows N(3,1). Each subplot shows the synchronization error err(t)/s on the y-axis against time t/s on the x-axis (0 to 600). Three algorithms are compared: 'Algorithm in this paper' (blue dashed line), 'Drift compensation part of DCBTS algorithm' (red dotted line), and 'Drift compensation part of SSTS algorithm' (black solid line). In Case i, the error decreases from ~800 to ~200. In Case ii, it decreases from ~20 to ~1. In Case iii, it decreases from ~400 to ~100. All cases show a sharp increase in error around t=480s, with the proposed algorithm maintaining the lowest error.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 4: Trajectories of the synchronization error err(t) with three delay cases under the topology G1. The figure consists of three subplots: Case i) delay follows U(1,4), Case ii) delay follows U(0,1,0.4), and Case iii) delay follows N(3,1). Each subplot shows the synchronization error err(t)/s on the y-axis against time t/s on the x-axis (0 to 600). Three algorithms are compared: 'Algorithm in this paper' (blue dashed line), 'Drift compensation part of DCBTS algorithm' (red dotted line), and 'Drift compensation part of SSTS algorithm' (black solid line). In Case i, the error decreases from ~800 to ~200. In Case ii, it decreases from ~20 to ~1. In Case iii, it decreases from ~400 to ~100. All cases show a sharp increase in error around t=480s, with the proposed algorithm maintaining the lowest error.

**Fig. 4.** Trajectories of the synchronization error  $err(t)$  with three delay cases under the topology  $G_1$ .

![Figure 5: Trajectories of virtual drifts ̂α_i(t) with three delay cases under the topology G2. The figure consists of three subplots: Case i) delay follows U(1,4), Case ii) delay follows U(0,1,0.4), and Case iii) delay follows N(3,1). Each subplot shows the virtual drifts on the y-axis against time t/s on the x-axis (0 to 600). Three algorithms are compared: 'Algorithm in this paper' (blue dashed line), 'Drift compensation part of DCBTS algorithm' (red dotted line), and 'Drift compensation part of SSTS algorithm' (black solid line). In Case i, drifts are low (~10). In Case ii, drifts are higher (~15). In Case iii, drifts are significantly higher (~200). All cases show a sharp increase in drifts around t=480s, with the proposed algorithm maintaining the lowest drifts.](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 5: Trajectories of virtual drifts ̂α\_i(t) with three delay cases under the topology G2. The figure consists of three subplots: Case i) delay follows U(1,4), Case ii) delay follows U(0,1,0.4), and Case iii) delay follows N(3,1). Each subplot shows the virtual drifts on the y-axis against time t/s on the x-axis (0 to 600). Three algorithms are compared: 'Algorithm in this paper' (blue dashed line), 'Drift compensation part of DCBTS algorithm' (red dotted line), and 'Drift compensation part of SSTS algorithm' (black solid line). In Case i, drifts are low (~10). In Case ii, drifts are higher (~15). In Case iii, drifts are significantly higher (~200). All cases show a sharp increase in drifts around t=480s, with the proposed algorithm maintaining the lowest drifts.

**Fig. 5.** Trajectories of virtual drifts  $\hat{\alpha}_i(t)$  with three delay cases under the topology  $G_2$ .

by a constant gain design, but also is robust to random bounded delays.

In practice, the quantification/communication noise is usually inevitable due to the data processing and transmission. The study of the time synchronization problem for WSNs with the effect of quantification/communication noise will be our future work.

## Appendix A. Proof of Proposition 1

Under the pseudo-periodic broadcast protocol, if node  $j$  receives the  $k_{ji}$ -th package from node  $i$ , based on the fact that  $t_j^i - t_0^i = lT_i$ , we know the current update time  $t_k < lT_i + M_d$  due to the delay, where  $M_d = \max_{i,j \in \mathcal{V}} M_{ji}$ . Then, up to  $t_k$ , the maximum number of packets sent by each node can be calculated as  $\max_{i,j \in \mathcal{V}} \left\lceil \frac{k_{ji}T_i + M_d}{\hat{T}_j} \right\rceil$ . If we consider all nodes' interaction up to  $t_k$ , we can obtain that  $k \le \max_{i,j \in \mathcal{V}} N \left\lceil \frac{k_{ji}T_i + M_d}{\hat{T}_j} \right\rceil$ . Since  $M_d$  is

![Figure 6: Trajectories of the synchronization error err(t) with three delay cases under the topology G2. The figure consists of three subplots: Case i) delay follows U(1,4), Case ii) delay follows U(0,1,0.4), and Case iii) delay follows N(3,1). Each subplot shows the synchronization error err(t)/s on the y-axis against time t/s on the x-axis (0 to 600). Three algorithms are compared: 'Algorithm in this paper' (blue dashed line), 'Drift compensation part of DCBTS algorithm' (red dotted line), and 'Drift compensation part of SSTS algorithm' (black solid line). In Case i, error is low (~100). In Case ii, error is very low (~1). In Case iii, error is high (~10^4) and decreases to ~100. All cases show a sharp increase in error around t=480s, with the proposed algorithm maintaining the lowest error.](4495fbec19aac6861f1a0b35c4dc38bc_img.jpg)

Figure 6: Trajectories of the synchronization error err(t) with three delay cases under the topology G2. The figure consists of three subplots: Case i) delay follows U(1,4), Case ii) delay follows U(0,1,0.4), and Case iii) delay follows N(3,1). Each subplot shows the synchronization error err(t)/s on the y-axis against time t/s on the x-axis (0 to 600). Three algorithms are compared: 'Algorithm in this paper' (blue dashed line), 'Drift compensation part of DCBTS algorithm' (red dotted line), and 'Drift compensation part of SSTS algorithm' (black solid line). In Case i, error is low (~100). In Case ii, error is very low (~1). In Case iii, error is high (~10^4) and decreases to ~100. All cases show a sharp increase in error around t=480s, with the proposed algorithm maintaining the lowest error.

**Fig. 6.** Trajectories of the synchronization error  $err(t)$  with three delay cases under the topology  $G_2$ .

bounded, there must exist a bounded constant  $K_1 > 0$  such that  $M_d \le K_1 \max_{i \in \mathcal{V}} \hat{T}_i$ . Together with the fact that  $k \ge k_{ji}$ , we can obtain

$$k \in \left[ k_{ji}, \max_{i,j \in \mathcal{V}} N \left\lceil \frac{\hat{T}_i}{\hat{T}_j} \right\rceil (k_{ji} + K_1) \right]. \quad (A.1)$$

If estimator (8) is adopted, based on the expression of  $\hat{d}_{ji}(t_{ji}^{id})$  defined in (18) and the expression of  $\delta_{ji}(k)$  defined in (20), we can obtain

$$\delta_{ji}(k) = - \frac{d_{ji}(t_{ji}^{id}) - \hat{g}_{ji} - d_{ji}(t_0^{id})}{k_{ji} \hat{T}_i + d_{ji}(t_{ji}^{id}) - \hat{g}_{ji} - d_{ji}(t_0^{id})}. \quad (A.2)$$

Under the operation condition of (8), we can obtain  $\tau_j(t_{ji}^{id}) - \tau_j(t_0^{id}) - g_{ji} > 0$ . Then, by (8), we can obtain  $\hat{\alpha}_{ij}(k_{ji}) > 0$ , which together with (18) implies that  $1 - \hat{d}_{ji}(k_{ji}) > 0$ . Further, based on the definition of  $\hat{d}_{ji}(k_{ji})$ , we can obtain that  $k_{ji} \hat{T}_i + (d_{ji}(t_{ji}^{id}) - \hat{g}_{ji} - d_{ji}(t_0^{id})) > 0$ . Since  $d_{ji}(t_{ji}^{id}) \in [m_{ji}, M_{ji}]$  and  $d_{ji}(t_0^{id}) \in [m_{ji}, M_{ji}]$ , together with  $\hat{g}_{ji} = \frac{g_{ji}}{\alpha_j}$  and  $g_{ji} \ge (M_{ji} - m_{ji})\alpha_j$ , we can conclude that  $d_{ji}(t_{ji}^{id}) - \hat{g}_{ji} - d_{ji}(t_0^{id})$  is non-positive. Further, based on the fact that the probability of a random variable which takes a certain value from a continuous interval is zero, we can obtain that  $d_{ji}(t_{ji}^{id}) - \hat{g}_{ji} - d_{ji}(t_0^{id})$  belongs to the interval  $(m_{ji} - M_{ji} - \hat{g}_{ji}, M_{ji} - m_{ji} - \hat{g}_{ji})$ . Since  $M_{ji}$ ,  $m_{ji}$  and  $\hat{g}_{ji}$  are all bounded, by (A.2), we can conclude that  $\delta_{ji}(k)$  is positive and satisfies

$$\delta_{ji}(k) \in \left( \frac{m_{ji} + \hat{g}_{ji} - M_{ji}}{k_{ji} \hat{T}_i + M_{ji} - m_{ji} - \hat{g}_{ji}}, \frac{M_{ji} + \hat{g}_{ji} - m_{ji}}{k_{ji} \hat{T}_i + m_{ji} - M_{ji} - \hat{g}_{ji}} \right). \quad (A.3)$$

If estimator (10) is adopted, we can obtain

$$\delta_{ji}(k) = - \frac{d_{ji}(t_{ji}^{id}) + \hat{g}_{ji} - d_{ji}(t_0^{id})}{k_{ji} \hat{T}_i + d_{ji}(t_{ji}^{id}) + \hat{g}_{ji} - d_{ji}(t_0^{id})}. \quad (A.4)$$

Then, if  $g_{ji} \ge (M_{ji} - m_{ji})\alpha_j$ , by (A.4), we can obtain that  $\delta_{ji}(k) \in (-1, 0)$ . Further, similar to the above analysis for the case that

estimator (8) is adopted, we can conclude that

$$\delta_{ji}(k) \in \left( \frac{m_{ji} - \hat{g}_{ji} - M_{ji}}{l_{ji}^k \hat{T}_i + m_{ji} + \hat{g}_{ji} - M_{ji}}, \frac{M_{ji} - \hat{g}_{ji} - m_{ji}}{l_{ji}^k \hat{T}_i + M_{ji} + \hat{g}_{ji} - m_{ji}} \right). \quad (\text{A.5})$$

Similarly, we can conclude for estimator (9) that

$$|\delta_{ji}(k)| \le \left| \frac{M_{ji} - m_{ji}}{l_{ji}^k \hat{T}_i + m_{ji} - M_{ji}} \right|. \quad (\text{A.6})$$

Since parameters  $N, K_1, \hat{T}_i, \forall i \in \mathcal{V}$  in (A.1) are all bounded and  $l_{ji}^k$  is increasing, we can conclude that there exists a bounded constant  $K_2 > 0$  such that  $\max_{i,j \in \mathcal{V}} N \lceil \frac{\hat{T}_i}{T_j} \rceil (l_{ji}^k + K_1) < K_2 l_{ji}^k$ . Then, by (A.1), we can conclude that  $1/l_{ji}^k$  is  $O(1/k)$ . Further, by (A.3), (A.5) and (A.6), we can conclude that for all  $j \in \mathcal{V}, i \in \mathcal{N}_j$ , there exists a bounded constant  $K > 0$  such that

$$|\delta_{ji}(k)| \le \frac{K}{k} (\frac{g_{ji}}{\alpha_j} + M_{ji} - m_{ji}). \quad (\text{A.7})$$

This completes the proof.

## Appendix B. Proof of Lemma 3

Consider a sequence  $1 = \bar{s}_0 < \bar{s}_1 < \dots < \bar{s}_k < \bar{s}_{k+1} < \dots$  such that  $\hat{g}_{\bar{s}_k} = \bigcup_{m=0}^{\bar{s}_{k+1}-\bar{s}_k-1} g(\bar{s}_k + m)$  are rooted for all  $k \in \mathbb{N}$ . Now, we introduce two state transition matrices  $R()$  (corresponding to the uncertainty-free case) and  $Q()$  (corresponding to the uncertainty-existing case) for model (28) in a certain time interval, which is defined as  $R(m, m) = Q(m, m) = I$ ,  $R(m + i + 1, m) = \bar{A}(m + i)R(m + i, m)$  and  $Q(m + i + 1, m) = (A(m + i) + \Delta(m + i))Q(m + i, m)$ . Then, for (28) in the interval  $[\bar{s}_k, \bar{s}_{k+1}]$ , we have

$$\begin{aligned} \bar{x}(\bar{s}_{k+1}) &= Q(\bar{s}_{k+1}, \bar{s}_k) \bar{x}(\bar{s}_k) \\ &= (R(\bar{s}_{k+1}, \bar{s}_k) + \hat{\Delta}_1(\bar{s}_k)) \bar{x}(\bar{s}_k), \end{aligned} \quad (\text{B.1})$$

where  $\hat{\Delta}_1(\bar{s}_k) = Q(\bar{s}_{k+1}, \bar{s}_k) - R(\bar{s}_{k+1}, \bar{s}_k)$ . If  $c \in (0, 1)$ , it can be easily verified that  $A(k), \forall k \ge 0$ , is a stochastic matrix, which implies that  $\bar{A}(k), \forall k \ge 0$ , is a stochastic matrix. Then, for all  $m_1, m_2 > 0$ , we can obtain

$$\|\bar{A}(m_1)\bar{\Delta}(m_2)\|_\infty \le \|\bar{\Delta}(m_2)\|_\infty. \quad (\text{B.2})$$

Denote  $S_i(\bar{s}_{k+1}, \bar{s}_k)$  as the set composed of the different combination of the product of some matrices, where each product contains  $i$  different error matrices belonging to the set  $\{\Delta(\bar{s}_k), \bar{\Delta}(\bar{s}_k + 1), \dots, \bar{\Delta}(\bar{s}_{k+1} - 1)\}$  and  $\bar{s}_{k+1} - \bar{s}_k - i$  different stochastic matrices belonging to the set  $\{\bar{A}(\bar{s}_k), \bar{A}(\bar{s}_k + 1), \dots, \bar{A}(\bar{s}_{k+1} - 1)\}$ . For example, if  $i = 1$ , one element in  $S_1(\bar{s}_{k+1}, \bar{s}_k)$  is  $\bar{A}(\bar{s}_{k+1} - 1)\bar{A}(\bar{s}_{k+1} - 2) \dots \bar{A}(\bar{s}_k + 1)\bar{\Delta}(\bar{s}_k)$ . Then,  $\hat{\Delta}_1(\bar{s}_k)$  can be expressed as

$$\begin{aligned} \hat{\Delta}_1(\bar{s}_k) &= \sum_j W_{1j}(\bar{s}_{k+1}, \bar{s}_k) + \sum_j W_{2j}(\bar{s}_{k+1}, \bar{s}_k) + \dots \\ &\quad + \sum_j W_{(\bar{s}_{k+1}-\bar{s}_k)j}(\bar{s}_{k+1}, \bar{s}_k), \end{aligned} \quad (\text{B.3})$$

where  $W_{ij}(\bar{s}_{k+1}, \bar{s}_k) \in S_i(\bar{s}_{k+1}, \bar{s}_k)$ . Then, together with (B.2), we can obtain

$$\begin{aligned} \|\hat{\Delta}_1(\bar{s}_k)\|_\infty &\le \sum_{i=0}^{\bar{s}_{k+1}-\bar{s}_k-1} \|\bar{\Delta}(\bar{s}_k + i)\|_\infty \\ &\quad + \sum_{j=0}^{\bar{s}_{k+1}-\bar{s}_k-2} \sum_{j>i} \|\bar{\Delta}(\bar{s}_k + j)\|_\infty \|\bar{\Delta}(\bar{s}_k + i)\|_\infty + \dots \\ &\quad + \prod_{i=0}^{\bar{s}_{k+1}-\bar{s}_k-1} \|\bar{\Delta}(\bar{s}_k + i)\|_\infty. \end{aligned} \quad (\text{B.4})$$

If  $\delta_{ij}(k), \forall i, j \in \mathcal{V}$ , is  $O(\frac{1}{(1+k)^\mu})$  with  $\mu > 0$ , based on the definition of  $\bar{\Delta}(k)$  given by (28), we can conclude that  $\|\bar{\Delta}(k)\|_\infty$  is  $O(\frac{1}{(1+k)^\mu})$ . Further, for all  $m_2 \ge m_1$ , we can conclude that  $\prod_{m=m_1}^{m_2} \|\bar{\Delta}(m)\|_\infty$  is  $O(\frac{1}{(1+m_1)^\mu})$ . Then, based on the equivalence of norms  $\|\cdot\|_\infty$  and  $\|\cdot\|$ , by (B.4), we can conclude that there exists a constant  $K_2 > 0$  such that

$$\begin{aligned} \|\hat{\Delta}_1(\bar{s}_k)\| &\le K_2 \left( \frac{1}{(1 + \bar{s}_k)^\mu} + \frac{1}{(1 + \bar{s}_k)^\mu} + \dots + \frac{1}{(1 + \bar{s}_k)^{\bar{s}_{k+1}-\bar{s}_k}} \right), \end{aligned} \quad (\text{B.5})$$

which implies that  $\|\hat{\Delta}_1(\bar{s}_k)\|$  is  $O(\frac{1}{(1+\bar{s}_k)^\mu})$ . If the switching topology is UR, by Lemma 2, we can conclude that there exists a bounded positive integer  $m_2$ , such that for all  $k \ge 0$ ,

$$\|\tilde{R}(\bar{s}_{k+m_2}, \bar{s}_k)\| < 1. \quad (\text{B.6})$$

Then, there must exist an integer sequence  $1 = \bar{s}_0 < \bar{s}_1 < \dots < \bar{s}_k < \bar{s}_{k+1} < \dots$ , which can be selected from  $1 = \bar{s}_0 < \bar{s}_1 < \dots < \bar{s}_k < \bar{s}_{k+1} < \dots$ , such that  $\|\tilde{R}(\bar{s}_{k+1}, \bar{s}_k)\| < 1$  for all  $k \ge 0$ . Now, for (29) with  $\hat{\Delta}_3(k) = \mathbf{0}$ , we can obtain

$$\begin{aligned} e(\bar{s}_{k+1}) &= \tilde{Q}(\bar{s}_{k+1}, \bar{s}_k)e(\bar{s}_k) \\ &= (\tilde{R}(\bar{s}_{k+1}, \bar{s}_k) + \hat{\Delta}_2(\bar{s}_k))e(\bar{s}_k), \end{aligned} \quad (\text{B.7})$$

where  $\hat{\Delta}_2(\bar{s}_k) = \tilde{Q}(\bar{s}_{k+1}, \bar{s}_k) - \tilde{R}(\bar{s}_{k+1}, \bar{s}_k)$ . Based on the above analysis for  $\|\hat{\Delta}_1(\bar{s}_k)\|$ , we can conclude that  $\|\hat{\Delta}_1(\bar{s}_k)\|$  is  $O(\frac{1}{(1+\bar{s}_k)^\mu})$ . Together with the fact that the linear transformation for a matrix does not change its convergence property, we can conclude that  $\|\hat{\Delta}_2(\bar{s}_k)\|$  is  $O(\frac{1}{(1+\bar{s}_k)^\mu})$ , which implies that  $\|\hat{\Delta}_2(\bar{s}_k)\|$  is  $O(\frac{1}{(1+\bar{s}_k)^\mu})$ . By (B.7), we can obtain

$$\begin{aligned} \|e(\bar{s}_{k+1})\| &\le \|\tilde{R}(\bar{s}_{k+1}, \bar{s}_k) + \hat{\Delta}_2(\bar{s}_k)\| \|e(\bar{s}_k)\| \\ &\le (\gamma_1 + \|\hat{\Delta}_2(\bar{s}_k)\|) \|e(\bar{s}_k)\| \\ &\le \left( \prod_{m=0}^k (\gamma_1 + \|\hat{\Delta}_2(\bar{s}_m)\|) \right) \|e(\bar{s}_0)\|, \end{aligned} \quad (\text{B.8})$$

where  $\gamma_1 = \sup_{k \ge 0} \|\tilde{R}(\bar{s}_{k+1}, \bar{s}_k)\| < 1$ . By statement (ii) of Lemma 1, we can obtain that there exists a constant  $\hat{\rho} \in (0, 1)$  such that  $\prod_{m=0}^k (\gamma_1 + \|\hat{\Delta}_2(\bar{s}_m)\|) \to 0$  at a rate no slower than  $O(\hat{\rho}^k)$ . Let  $\zeta = \sup_{k \ge 0} (\bar{s}_{k+1} - \bar{s}_k)$ , we can obtain that  $\zeta$  is a bounded integer. Let  $\bar{\rho} = \sqrt[\zeta]{\hat{\rho}}$ . Since  $\bar{\rho} \in (0, 1)$ , we can obtain  $\bar{\rho} \in (0, 1)$ . Then, for (29) with  $\hat{\Delta}_3(k) = \mathbf{0}$ , together with (B.8), we can conclude that  $\|e(k)\| \to 0$  at a rate no slower than  $O(\bar{\rho}^k)$ , which implies that for all  $m_2 \ge m_1$ , there exist constants  $K_3 > 0$  and  $\bar{\rho} \in (0, 1)$  such that

$$\|\tilde{Q}(m_2, m_1)\| \le K_3 \bar{\rho}^{m_2-m_1}. \quad (\text{B.9})$$

This completes the proof.

## References

- Bolognani, S., Carli, R., Lovisari, E., & Zampieri, S. (2016). A randomized linear algorithm for clock synchronization in multi-agent systems. *IEEE Transactions on Automatic Control*, 61(7), 1711–1726.
- Cao, M., Morse, A. S., & Anderson, B. D. O. (2008). Reaching a consensus in a dynamically changing environment: Convergence rates, measurement delays, and asynchronous events. *SIAM Journal on Control and Optimization*, 47(2), 601–623.
- Carli, R., Chiuso, A., Schenato, L., & Zampieri, S. (2008). A PI consensus controller for networked clocks synchronization. *IFAC Proceedings Volumes*, 41(2), 10289–10294, 17th IFAC World Congress.


- Dai, H., & Han, R. (2004). TSync: a lightweight bidirectional time synchronization service for wireless sensor networks. *SIGMOBILE Mobile Computing and Communications Review*, 8(1), 125–139.
- Du, J., & Wu, Y.-C. (2013). Distributed clock skew and offset estimation in wireless sensor networks: Asynchronous algorithm and convergence analysis. *IEEE Transactions on Wireless Communications*, 12(11), 5908–5917.
- Elson, J., Girod, L., & Estrin, D. (2002). Fine-grained network time synchronization using reference broadcasts. *SIGOPS Operating Systems Review*, 36(SI), 147–163.
- Fagnani, F., & Zampieri, S. (2007). Randomized consensus algorithms over large scale networks. *IEEE Journal on Selected Areas in Communications*, 26(4), 634–649.
- Fazlulhakov, Y. R. (2007). Time synchronization methods for wireless sensor networks: A survey. *Programming and Computer Software*, 33(4), 214–226.
- Freris, N. M., Graham, S. R., & Kumar, P. (2011). Fundamental limits on synchronizing clocks over networks. *IEEE Transactions on Automatic Control*, 56(6), 1352–1364.
- Ganeriwal, S., Kumar, R., & Srivastava, M. B. (2003). Timing-sync protocol for sensor networks. In *Proceedings of 4th ACM conference on embedded networked sensor systems* (pp. 138–149). ACM.
- He, J., Cheng, P., Shi, L., Chen, J., & Sun, Y. (2014). Time synchronization in WSNs: a maximum-value-based consensus approach. *IEEE Transactions on Automatic Control*, 59(3), 660–675.
- Huang, X.-Z., & Tian, Y.-P. (2018). Asynchronous distributed localization in networks with communication delays and packet losses. *Automatica*, 96, 134–140.
- Li, Q., & Rus, D. (2006). Global clock synchronization in sensor networks. *Institute of Electrical and Electronics Engineers. Transactions on Computers*, 55(2), 214–226.
- Liao, C., & Barooah, P. (2013). Distributed clock skew and offset estimation from relative measurements in mobile networks with Markovian switching topology. *Automatica*, 49(10), 3015–3022.
- Maróti, M., Kusy, B., Simon, G., & Lédeczi, Á. (2004). The flooding time synchronization protocol. In *Proceedings of 4th ACM conference on embedded networked sensor systems* (pp. 39–49). ACM.
- Noh, K.-I., Serpedin, E., & Qaraqe, K. (2008). A new approach for time synchronization in wireless sensor networks: Pairwise broadcast synchronization. *IEEE Transactions on Wireless Communications*, 7(9), 3318–3322.
- Olfati-Saber, R., & Murray, R. M. (2004). Consensus problems in networks of agents with switching topology and time-delays. *IEEE Transactions on Automatic Control*, 49(9), 1520–1533.
- Schenato, L., & Fiorentin, F. (2011). Average TimeSynch: A consensus-based protocol for clock synchronization in wireless sensor networks. *Automatica*, 47(9), 1878–1886.
- Stanković, M. S., Stanković, S. S., & Johansson, K. H. (2018). Distributed time synchronization for networks with random delays and measurement noise. *Automatica*, 93, 126–137.
- Sundaraman, B., Buy, U., & Kshemkalyani, A. D. (2005). Clock synchronization for wireless sensor networks: A survey. *Ad Hoc Networks*, 3(3), 281–323.
- Tian, Y.-P. (2015). LSTS: a new time synchronization protocol for networks with random communication delays. In *Proceedings of 54st IEEE conference on decision and control* (pp. 7404–7409). IEEE.
- Tian, Y.-P. (2017). Time synchronization in WSNs with random bounded communication delays. *IEEE Transactions on Automatic Control*, 62(10), 5445–5450.
- Tian, Y.-P., Chun, S., Chen, G., Zong, S., Huang, Y., & Wang, B. (2020). Delay compensation-based time synchronization under random delays: Algorithm and experiment. *IEEE Transactions on Control Systems Technology*, 29(1), 80–95.
- Tian, Y.-P., Zong, S., & Cao, Q. (2016). Structural modeling and convergence analysis of consensus-based time synchronization algorithms over networks: Non-topological conditions. *Automatica*, 65, 64–75.
- Wang, H., Chen, L., Li, M., & Gong, P. (2020). Consensus-based clock synchronization in wireless sensor networks with truncated exponential delays. *IEEE Transactions on Signal Processing*, 68, 1425–1438.
- Wang, H., Gong, P., & Li, M. (2022). Consensus-based time synchronization via sequential least squares for strongly rooted wireless sensor networks with random delays. *Automatica*, 136, Article 110045.
- Wang, B., & Tian, Y.-P. (2017). Time synchronization in WSNs with random communication delays: A constant gain design. *IFAC-PapersOnLine*, 50(1), 657–662.
- Xiao, F., & Wang, L. (2006). State consensus for multi-agent systems with switching topologies and time-varying delays. *International Journal of Control*, 79(10), 1277–1284.
- Yıldırım, K. S., Carli, R., & Schenato, L. (2018). Adaptive proportional-integral clock synchronization in wireless sensor networks. *IEEE Transactions on Control Systems Technology*, 26(2), 610–623.

![Portrait photo of Bo Wang, a man with glasses and short dark hair, wearing a dark jacket.](3668a836db39d25d24b56180a9c9a7fb_img.jpg)

Portrait photo of Bo Wang, a man with glasses and short dark hair, wearing a dark jacket.

**Bo Wang** received the M.Sc. degree in circuits and systems from the University of Electronic Science and Technology of China, Chengdu, China, in 2014 and the Ph.D. degree in control science and engineering from Southeast University, Nanjing, China, in 2018. He is currently an Associate Professor with the School of Automation, Hangzhou Dianzi University, Hangzhou, China. His current research interests include swarm and autonomous robotic systems.

![Portrait photo of Xinxin Lv, a woman with long dark hair, wearing a white shirt and a dark blazer.](b5b16a821754dab72447d00e17ee376a_img.jpg)

Portrait photo of Xinxin Lv, a woman with long dark hair, wearing a white shirt and a dark blazer.

**Xinxin Lv** received the Ph.D. degree in Electrical Engineering from Hohai University in 2021. She is currently a lecturer with the School of Information Science and Engineering, Zhejiang Sci-Tech University. In 2019 and 2020, she was a Joint Ph.D. Student in RTX Lab, University of Alberta, Edmonton, AB, Canada. Her research interests include power system modeling and application, stability analysis and control of power systems, load frequency control of power system.