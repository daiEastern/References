

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Fusion Engineering and Design journal cover](390120de4fe440c42fea8154fcaad334_img.jpg)

Fusion Engineering and Design journal cover

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Compensating control delays in the CFETR Multi-Purpose Overload Robot for divertor maintenance by using transformer-enhanced Temporal Convolutional Network<sup>☆</sup>

Chenhui Wan<sup>a,b</sup>![ORCID icon](17413706fd4997a1a4bdf85c6864eee1_img.jpg), Zibo Qi<sup>a,b</sup>, Hongbin Huang<sup>a,b</sup>, Jie Liu<sup>b,c</sup>, Youmin Hu<sup>a,b</sup>, Hongtao Pan<sup>d,e</sup>, Yong Cheng<sup>d,e</sup>, Yang Cheng<sup>d,e</sup>, Zhongxu Hu<sup>a,b</sup>![ORCID icon](f419710cbe076aa30a9c6c031b5cbe84_img.jpg),\*

<sup>a</sup> School of Mechanical Science and Engineering, Huazhong University of Science and Technology, Wuhan, 430074, China

<sup>b</sup> HUST-Wuxi Research Institute, Huazhong University of Science and Technology, Wuxi, 214100, China

<sup>c</sup> School of Civil and Hydraulic Engineering, Huazhong University of Science and Technology, Wuhan, 430074, China

<sup>d</sup> Institute of Plasma Physics, Hefei Institutes of Physical Science, Chinese Academy of Sciences, Hefei, 230026, China

<sup>e</sup> University of Science and Technology of China, Hefei, 230026, China

## ARTICLE INFO

### Keywords:

CFETR  
Delay compensation  
TransformerTCN  
Robotic control  
Nuclear fusion

## ABSTRACT

Communication delays in the CFETR (China Fusion Engineering Test Reactor) Multi-Purpose Overload Robot (CMOR), designed for divertor maintenance, significantly degrade control precision and operational reliability. This study proposed a Transformer-enhanced Temporal Convolutional Network (TransformerTCN) to address these delays. By integrating the local temporal feature extraction of Temporal Convolutional Networks (TCNs) with the long-range dependency modeling of Transformer's self-attention mechanism, TransformerTCN accurately predicted future robot states and dynamically adjusted control commands. Validation in ROS-based simulations demonstrated that TransformerTCN outperformed traditional models, achieving a Mean Squared Error (MSE) of 0.002 and an  $R^2$  score of 0.994, showcasing its superior accuracy and robustness. These results highlight TransformerTCN as a powerful solution for delay compensation in robotic systems operating in challenging nuclear fusion environments.

## 1. Introduction

The quest for sustainable energy solutions has intensified global interest in nuclear fusion, positioning the China Fusion Engineering Test Reactor (CFETR) as a pivotal project toward achieving commercial fusion power [1]. Fusion reactors like CFETR operate under extreme conditions, requiring the maintenance of critical components, such as the divertor, to ensure operational stability and safety [2]. The divertor, tasked with removing waste heat and particles from the reactor, experiences rapid wear and requires frequent maintenance [3]. Performing these tasks manually is hazardous due to high radiation levels and heat, making robotic remote handling systems indispensable for divertor maintenance in such environments [4].

The CFETR Multi-Purpose Overload Robot (CMOR) was developed to perform autonomous maintenance on the divertor and other critical components [5]. Equipped with seven degrees of freedom and a specialized control system, CMOR is capable of executing complex tasks

such as divertor replacement and inspection with high precision [6]. However, one of the primary challenges CMOR faces is communication delay within its control system, which can significantly impact its responsiveness and accuracy during high-precision operations [7].

Communication delays in robotic systems typically stem from several factors, including data transmission between sensors and control units, signal processing time, and network latency [8,9]. In CMOR's case, these delays can cause discrepancies between the robot's intended actions and its actual movements, leading to positioning inaccuracies and operational risks. Over the years, numerous delay compensation strategies have been developed to address these challenges in robotic control. Traditional methods, such as buffering and predictive control, were widely adopted to mitigate delay effects. Buffering techniques [10], for instance, temporarily stored incoming data to align sensor feedback with control commands, ensuring consistency in real-time operations. However, this method inherently introduced

<sup>☆</sup> This work was supported in part by the National Key Research and Development Program of China (No. 2024YFE03140003), and the National Natural Science Foundation of China (No. 52205104).

\* Corresponding author.

E-mail address: [zhongxu.hu@hust.edu.cn](mailto:zhongxu.hu@hust.edu.cn) (Z. Hu).

additional latency and struggled to handle dynamic and high-stakes environments, such as fusion reactors. Predictive control methods [11,12] aimed to estimate future states based on recent sensor readings and control inputs. While this approach improved system performance in some scenarios, it often failed to capture complex, long-term temporal dependencies, particularly under rapidly changing operating conditions. Adaptive strategies [13–16], including the use of Lyapunov-based delay compensation [17] and predictive displays [18,19], were later proposed to address these issues, but their effectiveness remained constrained by assumptions of delay upper bounds or simplified system models. To further mitigate the effects of communication delays in robotic control, supervisory control and shared control frameworks have been developed. Supervisory control systems [20] removed direct low-level control from human operators or centralized controllers, enabling robots to autonomously execute preprogrammed tasks based on high-level commands. Shared control strategies [21,22] distributed control authority between human operators and machine intelligence, allowing systems to dynamically adjust to changing conditions. However, these approaches introduced new challenges, such as increased computational requirements for real-time adjustments and limited adaptability to complex environments.

Recent advancements in deep learning have introduced models that can better handle temporal dependencies in time-series data, offering promising solutions for delay compensation [23,24]. Temporal Convolutional Networks (TCNs), in particular, have shown success in capturing short-term dependencies using causal convolutions and dilated layers, which ensure that each output relies only on past information [25]. Despite these strengths, TCNs may struggle to capture long-range dependencies, which are essential for accurately compensating delays in real-time robotic applications.

To overcome these limitations, this study introduced TransformerTCN, a hybrid model combining TCN's local feature extraction with Transformer's attention mechanism to enhance delay compensation accuracy. This approach significantly enhanced CMOR's responsiveness and operational reliability during high-stakes maintenance tasks in extreme environments. This study made the following key contributions to the field:

1. A novel delay compensation framework was designed by combining the local temporal modeling capabilities of TCNs with the long-range dependency modeling strengths of Transformers.

2. The proposed method was rigorously validated through experiments, showcasing its superior performance over traditional and machine-learning-based delay compensation methods. Additionally, the TransformerTCN model demonstrated the potential for broader applicability to other real-time control tasks beyond robotic maintenance, offering significant implications for the robotics field.

3. The TransformerTCN was tailored to address the unique challenges of robotic maintenance in nuclear fusion reactors, such as dynamic environments and communication delays, contributing to enhanced control precision and reliability.

The remainder of this paper is organized as follows: Section 2 introduces the CMOR system and provides a detailed examination of the communication delays within its control architecture. Section 3 outlines the proposed TransformerTCN-based delay compensation method, including its design and implementation. Section 4 presents experimental validation and results, comparing the TransformerTCN model's performance with that of other approaches. Finally, Section 5 discusses the study's contributions to the field and examines its implications, while Section 6 concludes the paper, summarizing the findings and highlighting potential directions for future research.

## 2. CMOR system and communication delay analysis

### 2.1. Overview of the cmor's communication delay problem

The CMOR is a specialized robotic system designed to handle the demanding maintenance tasks within the CFETR. Operating in a high-radiation, high-temperature environment, CMOR is equipped with advanced sensors and control mechanisms that enable it to perform

![A 3D cutaway diagram of the CMOR robotic system inside a vacuum vessel. The diagram shows the robot's end effector positioned near a divertor component. Labels with red arrows point to various parts: 'Inner board Blanket', 'Outboard Blanket', 'Maintenance Port', 'Vacuum Vessel', 'End Effector', 'Divertor', and 'CMOR'.](669865256db7d33e9cb759eac2e226c8_img.jpg)

A 3D cutaway diagram of the CMOR robotic system inside a vacuum vessel. The diagram shows the robot's end effector positioned near a divertor component. Labels with red arrows point to various parts: 'Inner board Blanket', 'Outboard Blanket', 'Maintenance Port', 'Vacuum Vessel', 'End Effector', 'Divertor', and 'CMOR'.

Fig. 1. The CMOR used to maintain the divertor in the 1/8 CFETR experimental prototype.

precise, autonomous operations, such as replacing and inspecting divertor components. With its seven degrees of freedom, CMOR is capable of navigating the confined spaces of the reactor chamber and executing force-sensitive tasks, which are critical for maintaining the integrity and efficiency of the divertor system. The CMOR used to maintain the divertor in the 1/8 CFETR experimental prototype is shown in Fig. 1.

However, achieving such performance introduced significant challenges. Communication delays in the CMOR system profoundly affect its ability to perform precise and responsive operations in the challenging environment of the CFETR. These delays, originating from signal transmission, processing, and sensor responses, disrupt the seamless synchronization required between the robot's sensors, controllers, and actuators, leading to several performance challenges.

One critical impact of communication delays is their role in causing positioning errors. The delays in transmitting control signals and receiving sensor feedback result in discrepancies between the planned trajectories and the robot's actual movements. Such misalignments are particularly problematic during high-precision tasks, such as aligning the end-effector with specific points on the divertor. Even minor deviations could compromise the efficiency of the task and, in severe cases, lead to operational errors or damage to reactor components.

Another significant issue arises in dynamic environments where CMOR must quickly adapt to unexpected changes, such as fluctuating conditions within the reactor chamber. The delays in sensor feedback and processing reduce the robot's responsiveness, impairing its ability to react promptly. This sluggish response compromises the accuracy and safety of maintenance operations, particularly in scenarios requiring split-second decision-making to prevent collisions or to maintain force-sensitive interactions with delicate components.

Communication delays also have a destabilizing effect on the control system, particularly during tasks involving precise force application. For instance, in force-sensitive operations, such as gripping or manipulating components, delays in feedback loops can cause the control system to overcompensate or undercompensate. This can result in oscillatory or unstable behaviors, reducing task efficiency and potentially leading to excessive wear on components or even mechanical damage.

In summary, communication delays challenge the CMOR system's ability to execute precise, reliable, and responsive control. These delays degrade task accuracy, slow down the system's adaptability, and undermine the stability of its control loops. Addressing these challenges requires robust compensation strategies capable of mitigating the effects of delays and ensuring optimal performance under the demanding conditions of CFETR maintenance operations.

![Diagram of the CMOR electrical system architecture showing a multi-layered network of components and communication protocols.](7055f51feb10ea4ea48b27c36f085286_img.jpg)

The diagram illustrates the CMOR electrical system architecture, organized into three main layers of communication protocols:

- Top Layer (Industrial Ethernet):** Connects to WinCC Server, WinCC SCADA Clients, Web Server Data Monitor, and Web Clients Data Monitor. A globe icon with a mouse cursor indicates remote access.
- Middle Layer (PROFINET/PROFIsafe):** Connects to the Master control S7-1500 T PLC, Safety S7-1500 F PLC, and an Industrial Computer.
- Bottom Layer (CAN):** Connects to various field devices including a Photoelectric switch, Temperature Sensor, Motor, S120 Variable frequency drive, SMC10 Sensor module, SMC40 Sensor module, and Heidenhain encoder.

The S120 Variable frequency drive and SMC sensor modules are shown connected to the Industrial Computer via the PROFINET/PROFIsafe layer. The field devices are connected to the CAN layer.

Diagram of the CMOR electrical system architecture showing a multi-layered network of components and communication protocols.

Fig. 2. The electrical system architecture of the CMOR is illustrated. The key components, including the industrial computer, control PLCs, actuators, and sensors, are connected through various communication protocols such as Drive-CLiQ, Profinet, and CAN, which are designed to ensure efficient and deterministic signal transmission during maintenance operations.

### 2.2. Communication delays in the CMOR control system

The CMOR relies on a sophisticated control system for executing its high-precision tasks in the extreme environment of the reactor chamber. However, the system's performance is significantly influenced by communication delays, which arise from signal transmission, processing, and sensor responses. These delays introduce challenges such as reduced responsiveness, positioning errors, and instability in control loops, particularly during force-sensitive operations. Understanding the nature and impact of these delays is critical to developing effective compensation strategies. The electrical system architecture of CMOR is shown in Fig. 2. The CMOR's control system involves three primary sources of communication delays: signal transmission delays, processing delays, and sensor response delays. Each of these categories is discussed in the following subsections.

#### 2.2.1. Signal transmission delays

Signal transmission delays occur during the exchange of information between the CMOR's sensors, controllers, and actuators. These delays are influenced by the communication protocols employed, each designed for specific purposes. High-speed protocols like Industrial Ethernet and Drive-CLiQ ensure minimal delays for critical real-time tasks, enabling efficient communication between the industrial computer and motion controllers. In contrast, Profinet/PROFIsafe prioritizes deterministic communication and safety, often at the expense of slightly higher delays. CAN (Controller Area Network), while suitable for diagnostic and low-priority tasks, exhibits higher latency due to limited bandwidth. The delays introduced by these protocols affect the synchronization of control signals and feedback loops, potentially reducing the

Table 1  
Signal transmission delays in CMOR.

| Protocol        | Transmission rate | Typical delay      |
|-----------------|-------------------|--------------------|
| Profinet [26]   | 100 Mbps          | 250 $\mu$ s–10 ms  |
| PROFIsafe [27]  | 100 Mbps          | 31.25 $\mu$ s–1 ms |
| Drive-CLiQ [28] | 100 Mbps          | ~100 $\mu$ s       |
| CAN [29]        | 1 Mbps            | ~100 $\mu$ s       |

system's ability to perform dynamic operations with precision. Table 1 summarizes the key characteristics of these protocols. The transmission rate is expressed in bps (bits per second).

#### 2.2.2. Processing delays

Processing delays originate from computations carried out by the industrial computer, main control PLC (Programmable Logic Controller), and safety PLC in the CMOR system. The industrial computer, equipped with cutting-edge CPUs (Central Processing Units) and GPUs (Graphics Processing Units), handles computationally intensive tasks such as trajectory planning and visual servoing. These tasks, although vital for ensuring smooth and accurate operations, can introduce delays depending on the algorithmic complexity and hardware utilization. In contrast, the main control PLC focuses on deterministic control tasks with relatively consistent delays, while the safety PLC prioritizes reliability and redundancy for critical operations, resulting in higher delays. These processing delays can disrupt the real-time responsiveness of the system, especially in safety-critical scenarios where rapid adaptation is essential. The specifications and typical delays of these components are detailed in Table 2.

**Table 2**  
Processing delays in CMOR.

| Hardware component  | Specifications                            | Typical delay |
|---------------------|-------------------------------------------|---------------|
| Industrial computer | Intel i9-12900KF,<br>NVIDIA RTX-4090      | 1–5 ms        |
| Main control PLC    | Siemens 1500T [30],<br>CPU 1518T-4 PN/DP  | 10–30 ms      |
| Safety PLC          | Siemens 1500F [30],<br>CPU 1516TF-3 PN/DP | 15–35 ms      |

**Table 3**  
Sensor response delays in CMOR.

| Sensor type                     | Sampling frequency |
|---------------------------------|--------------------|
| LTN RE-21-1-C09 Resolver [31]   | 10 kHz             |
| Heidenhain ECN125 Encoders [32] | ≤16 MHz            |
| Pt100 Temperature Sensors [33]  | ~10 Hz             |

#### 2.2.3. Sensor response delays

Sensor response delays are introduced by the time required for sensors to sample, process, and transmit data. High-performance sensors, such as joint encoders and motor resolvers, deliver high-frequency feedback with minimal delay. These are essential for tasks requiring precise control of joint positions and velocities. Conversely, slower sensors, such as Pt100 temperature sensors, introduce significant latencies due to their lower sampling frequencies, making them unsuitable for dynamic tasks. These delays can hinder the system's ability to react promptly to environmental changes, reducing control accuracy in high-speed operations. The response delays of the key sensors in the CMOR system are presented in Table 3.

Communication delays profoundly impacted CMOR's performance in precision maintenance tasks. These delays caused discrepancies between planned and actual trajectories, reduced responsiveness to dynamic changes, and destabilized force-sensitive control operations. Existing compensation methods, including buffering and predictive control, failed to fully address these challenges. Buffering introduced additional latency, and predictive models struggled to capture complex temporal dependencies, especially in dynamic and high-stakes environments.

To address these challenges, a more advanced delay compensation method was necessary—one that could model both short-term and long-term dependencies in CMOR's control signals. Recent advancements in machine learning provided promising solutions, particularly the TransformerTCN model, which combined the strengths of TCNs for local temporal pattern recognition and Transformers for modeling global dependencies. This hybrid approach offered a robust mechanism for mitigating delays and improving the precision and reliability of CMOR's operations in real-time. The proposed TransformerTCN method is described in the following section.

## 3. TransformerTCN-Based delay compensation method

### 3.1. Overview of delay compensation

Existing methods for compensating communication delays in robotic systems face significant limitations, particularly in dynamic and high-stakes environments like CFETR. Traditional approaches struggle to adapt to rapidly changing conditions or to capture the complex temporal dependencies required for precise and real-time control. These challenges highlight the need for a more advanced delay compensation strategy tailored to the unique demands of CMOR. Such a strategy must not only address short-term and long-term dependencies in control signals but also ensure high accuracy and robustness under variable conditions.

In this section, the TransformerTCN-based delay compensation method was introduced to address communication delays in the CMOR.

This method leveraged the strengths of TCNs for capturing local temporal patterns and the Transformer's self-attention mechanism for modeling long-term dependencies, enabling accurate predictions of future robot states and allowing the system to proactively adjust control commands. The TransformerTCN provided a novel approach to delay compensation by dynamically adjusting CMOR's control commands in real time, ensuring more accurate and reliable performance during critical maintenance tasks. The architectural overview of the TransformerTCN method is depicted in Fig. 3.

### 3.2. Model architecture

To effectively mitigate communication delays that impact CMOR's performance, the TransformerTCN was developed. This model captures both short-term and long-term dependencies in time-series data, allowing it to predict future robot states, thus compensating for control delays. By integrating TCN layers for local temporal feature extraction with the Transformer's self-attention mechanism to model global dependencies, the TransformerTCN model is able to anticipate delays and adjust control commands accordingly. This hybrid approach improves the system's responsiveness and accuracy in real-time operations.

The TransformerTCN-based framework was structured to integrate seamlessly into the CMOR control loop, enhancing its overall performance in delay compensation. The system received input signals  $R(s)$ , including joint positions ( $J1, J2, \dots, J7$ ), tool positions ( $X, Y, Z$ ), and tool orientations ( $w, x, y, z$ ). These inputs were processed by the existing controllers  $G_c(s)$  and the proposed compensators  $G_p(s)$ . After summation and in the presence of external disturbances  $D(s)$ , the signals were passed to the robotic system  $G(s)$ , which generated outputs  $C(s)$ . These outputs were then fed back into the control loop via feedback  $H(s)$ , completing the cycle.

In this framework, the controllers  $G_c(s)$  deployed the standard robotic control algorithms, while the compensators  $G_p(s)$  implemented the TransformerTCN algorithm for delay compensation. Specifically, the TransformerTCN compensators received input signals ( $J1, J2, \dots, J7$ ), ( $X, Y, Z$ ), and ( $w, x, y, z$ ). These signals were first processed by the Temporal Convolutional Network (TCN) block, which extracted local temporal features from the time-series data. The processed features were then passed through the Transformer block, which modeled global dependencies and long-term temporal relationships. The outputs ( $J1, J2, \dots, J7$ ), ( $X, Y, Z$ ), and ( $w, x, y, z$ ) were generated and feedback into the control loop for delay compensation, ensuring precise and robust system performance under varying communication delay conditions.

The TransformerTCN architecture consists of several key components, each tailored to address the unique challenges of delay compensation in robotic control systems:

#### 3.2.1. Temporal convolutional layers

The TCN layers serve as the foundational component for extracting short-term temporal features in sequential data [34]. Unlike standard convolutions, TCN uses causal convolutions, which only consider past time steps for each prediction, thus maintaining the temporal order. Furthermore, dilated convolutions are employed to enlarge the receptive field without increasing model depth. This enables the TCN to efficiently capture local dependencies over longer durations with fewer layers, which is essential for modeling delays caused by short-term signal variations in robotic systems.

Mathematically, for a given input sequence  $x(i)$ , the output  $y(t)$  of a dilated convolution layer is defined as:

$$y(t) = \sum_{i=0}^{k-1} w(i) \cdot x(t - d \cdot i), \quad (1)$$

where  $w(i)$  represents the convolution filter weights,  $d$  is the dilation factor, and  $k$  is the kernel size. The dilation factor  $d$  is increased exponentially with each layer, expanding the receptive field to capture dependencies over longer time intervals without increasing the model's complexity.

![Figure 3: Overview of the proposed compensatory control delay method. The diagram shows a control loop where inputs (Joint Position, Tool Position, Tool Orientation, Disturbance) are processed by Controllers Gc(s) and Compensators Gp(s). The Controllers use TCNs and Transformers to predict future states, which are then fed into the System G(s) (a robotic arm). The System output is compared with the target trajectory to produce feedback H(s), which is used by the Compensators. The Compensators use a Transformer Block to generate output probabilities C(s).](e394c2b5c61344f6a12397f430086072_img.jpg)

The diagram illustrates the proposed compensatory control delay method. It consists of several interconnected components:

- Input R(s):** Includes Joint Position ( $J_1, J_2, \dots, J_7$ ), Tool Position ( $X, Y, Z$ ), Tool Orientation ( $w, x, y, z$ ), and Disturbance  $D(s)$ .
- Controllers  $G_c(s)$ :** Processes the input to generate control commands. It includes three parallel paths for Joint Position, Tool Position, and Tool Orientation, each with TCNs (Temporal Convolutional Networks) and Transformer Blocks.
- TCNs Block:** Uses Residual blocks with dilated causal convolutions to capture temporal dependencies. The dilation factor  $d$  increases exponentially:  $d=1, 2, 2^2, \dots, 2^{n-1}$ .
- Transformer Block:** Incorporates Multi-head Attention and MLPs (Multi-Layer Perceptrons) to model global dependencies. It takes inputs from the TCNs and produces predicted states ( $J_i'', X, Y, Z'', w, x, y, z''$ ).
- System  $G(s)$ :** Represents the robotic arm (CASK) with joints  $J_1$  to  $J_7$  and an End Effector. It receives control commands and produces output.
- Feedback  $H(s)$ :** Compares the system output with the target trajectory to generate feedback.
- Compensators  $G_p(s)$ :** Uses a Transformer Block to generate output probabilities  $C(s)$  based on the feedback and target trajectory.

Figure 3: Overview of the proposed compensatory control delay method. The diagram shows a control loop where inputs (Joint Position, Tool Position, Tool Orientation, Disturbance) are processed by Controllers Gc(s) and Compensators Gp(s). The Controllers use TCNs and Transformers to predict future states, which are then fed into the System G(s) (a robotic arm). The System output is compared with the target trajectory to produce feedback H(s), which is used by the Compensators. The Compensators use a Transformer Block to generate output probabilities C(s).

Fig. 3. An overview of the proposed compensatory control delay method is presented. Communication delays are compensated by integrating TCNs and Transformer self-attention mechanisms, enabling CMOR's control system to anticipate future states and generate timely control commands.

#### 3.2.2. Self-attention mechanism

To model global dependencies, a multi-head self-attention mechanism was incorporated after the TCN layers. This mechanism enables relevant patterns across extended time steps to be identified and emphasized by the model [35].

Given an input sequence  $X = \{x_1, x_2, \dots, x_N\}$ , three projections—queries ( $Q$ ), keys ( $K$ ), and values ( $V$ )—are derived by applying learned linear transformations:

$$Q = XW^Q, \quad K = XW^K, \quad V = XW^V, \quad (2)$$

where  $W^Q$ ,  $W^K$ , and  $W^V$  are the weight matrices learned during training. The attention output is then computed as:

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V, \quad (3)$$

where  $d_k$  is the dimension of the keys used for scaling. By dividing by  $\sqrt{d_k}$ , the softmax function is stabilized, ensuring a balanced distribution of attention weights.

In the multi-head attention mechanism, this attention computation is performed in parallel across multiple heads. This allows various aspects of temporal relationships to be learned simultaneously, thereby improving the model's ability to capture both short-term and long-term dependencies essential for accurate delay compensation.

#### 3.2.3. Residual connections and position encoding

To improve gradient flow and prevent vanishing gradients in deep architectures, residual connections were applied throughout the TransformerTCN. These connections allowed the model to bypass transformation layers when necessary, ensuring that meaningful information was preserved across layers.

For any input  $X$ , the output of a layer employing a residual connection is given by:

$$\text{Output} = F(X) + X, \quad (4)$$

where  $F(X)$  represents the learned transformation. This additive structure enables identity mappings to be preserved when no transformation is required, thus stabilizing training and improving convergence.

In addition, position encoding was introduced to compensate for the lack of inherent temporal order awareness in the Transformer architecture. Temporal context was embedded into the input features by adding sinusoidal position encodings, allowing the model to distinguish different time steps.

The encoding for position  $pos$  and dimension  $i$  was defined as:

$$PE_{(pos,2i)} = \sin\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right), \quad (5)$$

$$PE_{(pos,2i+1)} = \cos\left(\frac{pos}{10000^{2i/d_{\text{model}}}}\right), \quad (6)$$

where  $d_{\text{model}}$  is the dimension of the model's hidden representations. These encodings ensured that the model was informed of the relative and absolute positions within a sequence, which is essential for capturing timing-related patterns in delay compensation.

The next section will provide a detailed experimental evaluation, highlighting the TransformerTCN's performance in comparison with traditional models such as RNN (Recurrent Neural Network), LSTM (Long-Short Term Memory), and standard TCN.

## 4. Experimental validation and results

### 4.1. Experimental setup

To validate the proposed TransformerTCN-based delay compensation method, experiments were conducted to simulate CMOR's maintenance tasks in a realistic operational environment. The experimental setup replicated CMOR performing critical operations, such as the installation and removal of divertor components, within the 1/8 vacuum chamber modeled in ROS1 Melodic. Using RViz, CMOR's trajectory planning was designed to execute precise movements along planned paths while adhering to temporal constraints. This simulation environment emphasized precise joint motion, tool positioning, and adaptability to dynamic conditions, which are essential for maintaining the integrity of CFETR's divertor system. The scene when using RViz to simulate CMOR maintaining the divertor is shown in Fig. 4.

The trajectory planning process was carried out using RViz, where CMOR's motion paths were designed to navigate the constrained spaces

of the reactor chamber while adhering to the operational requirements of high precision and safety. The computational platform hosting the simulation and training processes consisted of an Intel i9-12900KF CPU, NVIDIA RTX-4090 GPU, and 64 GB of RAM. The software environment included Python 3.8, PyTorch 2.4.1, and CUDA 11.8, ensuring sufficient computational resources for real-time trajectory planning and model training.

#### 4.1.1. Data preprocessing

The dataset consisted of time-series sequences collected from CMOR's sensors, which included joint positions, end-effector positions, and orientations. The dataset was divided into training and test sets for training and evaluating the models, respectively.

The training dataset consisted of time-series data from CMOR's sensors, including joint positions ( $J_1 - J_7$ ), end-effector positions ( $X, Y, Z$ ), and orientations represented as quaternions ( $w, x, y, z$ ). The data was preprocessed using interpolation techniques to ensure consistent time intervals, and MinMax scaling was applied to normalize the data within a specific range:

$$X' = \frac{X - X_{\min}}{X_{\max} - X_{\min}}, \quad (7)$$

where  $X_{\min}$  and  $X_{\max}$  denote the minimum and maximum values in the dataset, respectively. This normalization enhanced model convergence during training.

#### 4.1.2. Model training

The TransformerTCN model was trained to predict future states of the CMOR, allowing it to proactively compensate for delays. The training objective minimized the Mean Squared Error (MSE) between predicted and actual future positions. The Adam optimizer was employed for efficient convergence, and the model was trained over 100 epochs with an early stopping criterion to prevent overfitting. During training, TCN layers captured short-term dependencies, while the self-attention mechanism learned long-term patterns, both of which are essential for robust delay compensation.

#### 4.1.3. Testing and validation

After training, the model was evaluated on a separate test set that contained sequences not previously seen by the model. Metrics such as MSE, Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), and R-Square ( $R^2$ ) were used to assess the model's accuracy in predicting future states, as well as its effectiveness in compensating for control delays. These metrics are defined as follows:

$$\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2, \quad (8)$$

$$\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2}, \quad (9)$$

$$\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |\hat{y}_i - y_i|, \quad (10)$$

$$R^2 = 1 - \frac{\sum_{i=1}^{n} (\hat{y}_i - y_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y})^2}, \quad (11)$$

where  $y_i$  is the actual value,  $\hat{y}_i$  is the predicted value,  $\bar{y}$  is the mean of actual values, and  $n$  is the number of samples. High  $R^2$  and low MSE, RMSE, and MAE values indicate better model performance.

### 4.2. Results

The experimental results (summarized in Table 4) indicate that the TransformerTCN model consistently outperformed the RNN, LSTM, and TCN models across all metrics. The TransformerTCN demonstrated the lowest errors, indicating its superior ability to predict CMOR's future states accurately and effectively compensate for control delays.

![Screenshot of the RViz software interface showing a 3D simulation of a CMOR robot inside a vacuum chamber. The interface includes a top menu bar, a left-hand 'Displays' panel with settings for 'Fixed Frame' and 'RobotModel', a central 3D visualization window, and a right-hand 'Views' panel with camera settings. At the bottom, a 'Time' status bar shows ROS Time, ROS Elapsed, Wall Time, and Wall Elapsed.](1dba94e9a65ea5fbd805e44a5a2c8cd5_img.jpg)

Screenshot of the RViz software interface showing a 3D simulation of a CMOR robot inside a vacuum chamber. The interface includes a top menu bar, a left-hand 'Displays' panel with settings for 'Fixed Frame' and 'RobotModel', a central 3D visualization window, and a right-hand 'Views' panel with camera settings. At the bottom, a 'Time' status bar shows ROS Time, ROS Elapsed, Wall Time, and Wall Elapsed.

Fig. 4. A divertor maintenance scenario is simulated using RViz within a ROS-based environment. The CMOR is shown performing planned motion trajectories inside a virtual 1/8-scale vacuum chamber, where time-synchronized joint and tool position data are collected for training and evaluating the delay compensation models.

**Table 4**  
The experimental results.

| Network               | MSE          | RMSE         | MAE          | $R^2$        |
|-----------------------|--------------|--------------|--------------|--------------|
| RNN                   | 0.013        | 0.112        | 0.073        | 0.970        |
| LSTM                  | 0.014        | 0.119        | 0.075        | 0.966        |
| TCN                   | 0.008        | 0.088        | 0.065        | 0.967        |
| <b>TransformerTCN</b> | <b>0.002</b> | <b>0.043</b> | <b>0.027</b> | <b>0.994</b> |

To evaluate the statistical significance of the differences among models, standard statistical methods were employed, including the Analysis of Variance (ANOVA) and pairwise t-tests. ANOVA is a statistical technique used to determine whether there are significant differences between the means of three or more groups. A p-value obtained from ANOVA indicates whether the observed differences are statistically significant. A smaller p-value (typically less than 0.05) suggests that the differences are unlikely to have occurred by chance. Additionally, pairwise t-tests were used to perform detailed comparisons between each pair of models. This test evaluates whether the means of two independent samples differ significantly. The resulting p-values provide evidence of whether the differences between models are statistically meaningful. These methods allow for a comprehensive and rigorous evaluation of the proposed model's performance compared to other baseline approaches. The ANOVA results showed a significant F-statistic of 39.608 with a p-value of less than  $10^{-22}$ , indicating that there were statistically significant differences among the models. Pairwise comparisons (Table 5) revealed that the TransformerTCN model significantly outperformed the RNN, LSTM, and TCN models (all p-values  $< 10^{-15}$ ). Furthermore, LSTM and TCN also exhibited statistically significant differences (p-value = 0.0003), while the difference between RNN and TCN was not statistically significant (p-value = 0.182). This statistical evidence strongly supported the superiority of the TransformerTCN model.

Both RNN and LSTM showed relatively higher error values compared to TCN and TransformerTCN, especially for tasks requiring long-term dependency modeling. The RNN struggled to capture complex temporal dependencies, leading to higher variability in error, while

**Table 5**  
P-values from pairwise comparisons between models.

| Comparison              | P-value     | Statistical significance (p < 0.05) |
|-------------------------|-------------|-------------------------------------|
| RNN vs. LSTM            | 0.025       | Yes                                 |
| RNN vs. TCN             | 0.182       | No                                  |
| RNN vs. TransformerTCN  | $<10^{-15}$ | Yes                                 |
| LSTM vs. TCN            | 0.0003      | Yes                                 |
| LSTM vs. TransformerTCN | $<10^{-21}$ | Yes                                 |
| TCN vs. TransformerTCN  | $<10^{-19}$ | Yes                                 |

LSTM performed slightly better due to its inherent memory capabilities but still faced limitations in long-range delay compensation. The TCN model improved upon RNN and LSTM in accuracy, benefiting from causal and dilated convolutions that enhanced its ability to capture short- and medium-term dependencies. However, its lack of attention mechanisms limited its performance in tasks requiring global dependency modeling.

The TransformerTCN achieved the highest accuracy, displaying consistently lower errors across all metrics. Its combination of TCN for local pattern recognition and Transformer's self-attention for global dependencies allowed it to capture complex temporal relationships effectively. This hybrid model demonstrated the best capacity for delay compensation, resulting in lower prediction errors and stable performance across all sequences.

The training loss curves for each model are shown in Fig. 5. The TransformerTCN model converged faster and reached the lowest final loss, underscoring its efficiency in learning temporal dependencies from the data. In comparison, the RNN and LSTM models showed slower convergence, while the TCN model exhibited moderate performance.

The performance of the proposed TransformerTCN model was rigorously analyzed through multiple evaluation metrics, demonstrating its superiority in mitigating communication delays. To illustrate its effectiveness, the distribution of Mean Absolute Error (MAE) across different models was compared. As shown in Fig. 6., the TransformerTCN achieved a highly concentrated and narrow error distribution, which

![Figure 5: Training loss curves over epochs for RNN, LSTM, TCN, and the proposed method. The proposed method shows the fastest convergence and lowest final loss.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 5 is a line graph showing the training loss over 60 epochs for four models: RNN (blue), LSTM (orange), TCN (green), and the Proposed method (red). The y-axis represents 'Loss' from 0 to 8, and the x-axis represents 'Epoch' from 0 to 60. The Proposed method starts with a loss of approximately 5.5 and drops to near zero by epoch 20. The RNN and LSTM start with losses around 8.5 and 7.5 respectively, and converge to near zero by epoch 40. The TCN starts with a loss of approximately 8.5 and converges to near zero by epoch 50.

Figure 5: Training loss curves over epochs for RNN, LSTM, TCN, and the proposed method. The proposed method shows the fastest convergence and lowest final loss.

**Fig. 5.** Training loss curves over epochs are compared for all models. Faster convergence and lower final loss values are observed for the proposed TransformerTCN model, indicating that temporal dependencies were learned more effectively than with RNN, LSTM, or standard TCN.

![Figure 7: Violin plot of mean absolute errors across models (RNN, LSTM, TCN, and Proposed method). The Proposed method has the narrowest and lowest distribution.](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 7 is a violin plot showing the distribution of mean absolute errors for four models: RNN (blue), LSTM (orange), TCN (green), and the Proposed method (red). The y-axis represents 'Mean Absolute Error' from -0.05 to 0.30. The Proposed method has the narrowest and lowest distribution, centered around 0.03. The RNN and LSTM have broader distributions centered around 0.22 and 0.28 respectively. The TCN has a distribution centered around 0.18.

Figure 7: Violin plot of mean absolute errors across models (RNN, LSTM, TCN, and Proposed method). The Proposed method has the narrowest and lowest distribution.

**Fig. 7.** Violin plot of mean absolute errors across models (RNN, LSTM, TCN, and Proposed method), showing the distribution and variability of errors. The plot illustrates the consistency and accuracy of each model, with narrower and lower distributions indicating better performance.

![Figure 6: Mean absolute error comparison across various parameters (J1, J2, J3, J4, J5, J6, J7, X, Y, Z, w, x, y, z). The Proposed method generally shows the lowest error.](27b22513fc27a0ff5f230b062ad3112f_img.jpg)

Figure 6 is a line graph showing the mean absolute error for four models across 14 comparison parameters. The y-axis represents 'Mean Absolute Error' from 0.025 to 0.200. The x-axis lists the parameters: J1, J2, J3, J4, J5, J6, J7, X, Y, Z, w, x, y, z. The Proposed method (red) generally shows the lowest error across most parameters, particularly for the joint positions J1-J7 and the tool orientation parameters w, x, y, z. The RNN (blue) and LSTM (orange) show higher errors, especially for J1 and J2. The TCN (green) shows moderate errors.

Figure 6: Mean absolute error comparison across various parameters (J1, J2, J3, J4, J5, J6, J7, X, Y, Z, w, x, y, z). The Proposed method generally shows the lowest error.

**Fig. 6.** Mean absolute error comparison across the seven joint positions (J1 (m), J2–J7 (rad)), three axes of tool positions (X, Y, Z (m)), and the tool orientation represented by a quaternion with four parameters ( $w, x, y, z$ ).

![Figure 8: Heatmap visualization of the attention matrix for TransformerTCN (Layer 1, Head 1). The heatmap shows attention weights across 20 time steps for queries and keys.](643d86ebba41e16a88461bfcb3741de6_img.jpg)

Figure 8 is a heatmap visualization of the attention matrix for TransformerTCN (Layer 1, Head 1). The y-axis represents 'Time Steps (Query)' and the x-axis represents 'Time Steps (Key)', both ranging from 1 to 19. The color scale represents the magnitude of attention weights, ranging from 0.02 (purple) to 0.10 (yellow). The heatmap shows a strong diagonal pattern, indicating consistent column-wise attention and localized diagonal patterns, with some off-diagonal weights indicating long-range dependencies.

Figure 8: Heatmap visualization of the attention matrix for TransformerTCN (Layer 1, Head 1). The heatmap shows attention weights across 20 time steps for queries and keys.

**Fig. 8.** Visualization of the attention matrix for TransformerTCN (Layer 1, Head 1). The heatmap represents the attention weights across a sequence length of 20, highlighting consistent column-wise attention and localized diagonal patterns.

reflects its consistent and reliable performance in handling communication delays. In contrast, broader distributions observed in RNN and LSTM models, along with higher error variances, highlight their limitations in capturing the complex temporal dependencies required for precise delay compensation. The TCN model showed moderate improvements but still fell short in terms of error concentration and magnitude, further underscoring the effectiveness of TransformerTCN in achieving stable and accurate predictions.

Additionally, Fig. 7 highlights the density and distribution shape of errors across models. The concentrated and minimal error distribution observed for TransformerTCN aligns with its demonstrated stability and accuracy, while the broader distributions for RNN and LSTM emphasize their lack of consistency. These findings reinforce the TransformerTCN's robustness in scenarios involving dynamic and high-stakes environments.

To further understand the internal mechanisms of TransformerTCN, the attention matrix of its Transformer layer was analyzed, as depicted in Fig. 8. The heatmap revealed that the model assigns relatively consistent attention across time steps while emphasizing immediate temporal

neighbors. This dual focus on local and long-term dependencies enables the TransformerTCN to effectively balance global information with local temporal patterns. These characteristics are critical for accurately compensating delays in control systems. The intensity of colors in the heatmap corresponds to the magnitude of attention weights, ranging from low (purple) to high (yellow). The visualization highlights several key observations:

The attention weights for each column exhibit relatively consistent intensities. This suggests that the model assigns similar importance to multiple query steps when focusing on a particular key step. Such behavior reflects the model's ability to distribute attention evenly across time steps, ensuring robustness in capturing temporal patterns. While column-wise uniformity is prominent, the diagonal exhibits higher attention weights, indicating a stronger emphasis on the current time step and its immediate temporal neighbors. This focus supports the short-term temporal dependencies critical for predictive tasks. Some off-diagonal weights remain significant, demonstrating the model's capacity to capture long-range dependencies. This characteristic enables the TransformerTCN to balance local and global information, which is

![Figure 9: Absolute error comparison across various parameters. The figure consists of 14 subplots arranged in a 7x2 grid. The left column (a-g) shows absolute error for joint positions J1-J7 in radians. The right column (h-n) shows absolute error for tool positions (X, Y, Z) and tool orientation (w, x, y, z) in meters and radians. Each subplot compares four models: RNN (blue), LSTM (orange), TCN (green), and the Proposed method (red). The x-axis for all plots is 'Time Step (s)' from 0 to 50. The y-axis scales vary by subplot, generally ranging from 0.00 to 0.50 or 1.00.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 9: Absolute error comparison across various parameters. The figure consists of 14 subplots arranged in a 7x2 grid. The left column (a-g) shows absolute error for joint positions J1-J7 in radians. The right column (h-n) shows absolute error for tool positions (X, Y, Z) and tool orientation (w, x, y, z) in meters and radians. Each subplot compares four models: RNN (blue), LSTM (orange), TCN (green), and the Proposed method (red). The x-axis for all plots is 'Time Step (s)' from 0 to 50. The y-axis scales vary by subplot, generally ranging from 0.00 to 0.50 or 1.00.

**Fig. 9.** Absolute error comparison across various parameters: (a)–(g) the seven joint positions (J1–J7), (h)–(j) the three axes of tool positions ( $X$ ,  $Y$ ,  $Z$ ), and (k)–(n) the tool orientation represented by the quaternion parameters ( $w$ ,  $x$ ,  $y$ ,  $z$ ). Each subfigure highlights the performance of different models (RNN, LSTM, TCN, and Proposed method) in terms of absolute error across these parameters.

essential for accurately compensating delays in control systems. Across rows, variations in color intensity reveal the model's adaptive nature, where specific time steps dynamically receive more or less attention depending on the temporal context. This flexibility allows the model to prioritize relevant patterns in complex sequential data.

The attention matrix provides a valuable visualization of how the TransformerTCN processes input sequences. By leveraging consistent attention across columns and capturing dependencies at multiple temporal scales, the model effectively integrates both short-term and long-term information to improve delay compensation in the CMOR system.

![Figure 10: Four residual plots (a, b, c, d) showing the relationship between predicted values and residuals for RNN, LSTM, TCN, and Proposed method (TransformerTCN) respectively. Each plot has 'Predicted Values' on the x-axis (ranging from -2 to 10) and 'Residuals' on the y-axis (ranging from -0.4 to 0.8). A horizontal red dashed line at y=0 represents the ideal residual. Plot (a) RNN shows a wide scatter of residuals. Plot (b) LSTM shows a moderate scatter. Plot (c) TCN shows a moderate scatter. Plot (d) Proposed method shows a very tight and unbiased distribution of residuals around the zero line, indicating superior prediction accuracy.](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 10: Four residual plots (a, b, c, d) showing the relationship between predicted values and residuals for RNN, LSTM, TCN, and Proposed method (TransformerTCN) respectively. Each plot has 'Predicted Values' on the x-axis (ranging from -2 to 10) and 'Residuals' on the y-axis (ranging from -0.4 to 0.8). A horizontal red dashed line at y=0 represents the ideal residual. Plot (a) RNN shows a wide scatter of residuals. Plot (b) LSTM shows a moderate scatter. Plot (c) TCN shows a moderate scatter. Plot (d) Proposed method shows a very tight and unbiased distribution of residuals around the zero line, indicating superior prediction accuracy.

**Fig. 10.** Residual plots for different models, illustrating the relationship between predicted values and residuals: (a) RNN, (b) LSTM, (c) TCN, and (d) Proposed method (TransformerTCN). Each plot demonstrates the residual distribution, with the TransformerTCN exhibiting the most concentrated and unbiased residuals around zero, indicating superior prediction accuracy.

The absolute errors for joint positions (J1–J7), tool positions ( $X$ ,  $Y$ ,  $Z$ ), and tool orientations ( $w$ ,  $x$ ,  $y$ ,  $z$ ) across different models were evaluated and visualized in Fig. 9. TransformerTCN consistently demonstrated lower error values compared to other models, indicating its superior accuracy in delay compensation. The RNN and LSTM models exhibited higher and more variable errors, reflecting their reduced reliability in dynamic environments. While the TCN model performed reasonably well, it could not match the precision of the TransformerTCN.

Residual plots for all models are presented in Fig. 10. TransformerTCN exhibited a narrow and random distribution of residuals around zero, signifying unbiased predictions and accurate model performance. In contrast, structured residual patterns observed in RNN, LSTM, and TCN models highlight the presence of systematic prediction errors in these methods.

Finally, the model's ability to handle communication delays across various joints and axes was further validated through the heatmap shown in Fig. 11. The consistently lower error values achieved by TransformerTCN for all joints and tool axes demonstrate its capability to provide precise and reliable delay compensation across all degrees of freedom in the CMOR system.

The results indicate that the TransformerTCN model provides significant advantages over traditional RNN, LSTM, and TCN models in terms of delay compensation. The combination of TCN and Transformer architectures enables the model to capture both local and global dependencies, making it well-suited for predicting future states and compensating for delays in real-time control tasks. The consistently low error values across all metrics suggest that TransformerTCN offers robust performance, which is essential for high-stakes environments like nuclear fusion reactors where precise control is critical.

In summary, the TransformerTCN model demonstrated substantial improvements over other models in mitigating communication delays in the CMOR system. Its superior performance underscores the potential of combining convolutional and attention-based architectures for time-series prediction tasks requiring comprehensive temporal modeling.

## 5. Discussion

The TransformerTCN model provides a groundbreaking solution to the challenges posed by communication delays in the CMOR system, effectively addressing limitations of traditional methods. By combining the local temporal modeling capabilities of TCN with the global dependency modeling strengths of the Transformer's self-attention mechanism, this hybrid approach achieves precise and robust delay compensation critical for CMOR's operations in dynamic nuclear fusion environments.

One of the core strengths of TransformerTCN lies in its dual ability to efficiently handle short- and long-term dependencies. The TCN component models immediate changes in control signals, enabling rapid response to time-sensitive operations, while the self-attention mechanism accounts for long-term dependencies, capturing cumulative effects of delays across extended sequences. This integration ensures that the model dynamically adapts to both immediate and persistent challenges posed by communication delays, providing smoother control signals and reducing discrepancies between planned and executed trajectories.

Experimental results confirm the model's superior prediction accuracy, with TransformerTCN achieving significantly lower MAE, MSE, and RMSE values compared to traditional models such as RNN, LSTM, and standard TCN. Additionally, residual analysis revealed that the TransformerTCN produces unbiased predictions with random distributions around zero, minimizing systematic errors. This robustness is particularly valuable for CMOR's application in nuclear fusion maintenance, where variations in environmental conditions necessitate adaptable control strategies.

The findings demonstrate that TransformerTCN effectively mitigates communication delays in the CMOR system, significantly enhancing control precision and operational reliability. By leveraging multi-head self-attention to balance local and global temporal features, the model excels in capturing complex dependencies inherent in time-series data.



![Heatmap of mean absolute errors across various parameters for four models: RNN, LSTM, TCN, and Proposed method. The parameters are J1, J2, J3, J4, J5, J6, J7, X, Y, Z, w, x, y, z. The color scale ranges from 0.025 (yellow) to 0.200 (dark blue).](10c82dcc5f2c237961329dd29d65859c_img.jpg)

| Model           | J1    | J2    | J3    | J4    | J5    | J6    | J7    | X     | Y     | Z     | w     | x     | y     | z     |
|-----------------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|
| RNN             | 0.151 | 0.031 | 0.052 | 0.059 | 0.032 | 0.065 | 0.063 | 0.184 | 0.077 | 0.153 | 0.024 | 0.030 | 0.025 | 0.035 |
| LSTM            | 0.214 | 0.037 | 0.054 | 0.065 | 0.039 | 0.100 | 0.071 | 0.211 | 0.062 | 0.155 | 0.022 | 0.039 | 0.029 | 0.031 |
| TCN             | 0.097 | 0.033 | 0.062 | 0.072 | 0.035 | 0.082 | 0.065 | 0.129 | 0.066 | 0.134 | 0.031 | 0.044 | 0.028 | 0.035 |
| Proposed method | 0.094 | 0.035 | 0.019 | 0.018 | 0.020 | 0.029 | 0.050 | 0.097 | 0.057 | 0.086 | 0.011 | 0.015 | 0.021 | 0.022 |

Heatmap of mean absolute errors across various parameters for four models: RNN, LSTM, TCN, and Proposed method. The parameters are J1, J2, J3, J4, J5, J6, J7, X, Y, Z, w, x, y, z. The color scale ranges from 0.025 (yellow) to 0.200 (dark blue).

Fig. 11. Heatmap of mean absolute errors across various parameters, with units specified: J1 (m), J2–J7 (rad), X, Y, Z (m), and quaternion parameters  $w, x, y, z$ . This visualization highlights the performance of different models (RNN, LSTM, TCN, and Proposed method) across the seven joint positions, three axes of tool positions, and tool orientation.

This capability ensures accurate state predictions and timely adjustments, resulting in more stable and efficient operations under the high-stakes conditions of CFETR maintenance tasks.

The TransformerTCN's ability to outperform traditional models can be attributed to its architectural advantages. Compared to RNN and LSTM, it avoids the vanishing gradient problem while maintaining long-term dependencies. Unlike standard TCN, which struggles with global patterns, the TransformerTCN successfully integrates local and global information, ensuring comprehensive delay compensation. The consistently lower prediction errors and higher  $R^2$  values across all evaluation metrics underscore its superior performance and reliability.

Furthermore, visualizations of attention weights highlight the TransformerTCN's adaptive nature, as it assigns dynamic importance to input sequences depending on temporal context. This flexibility enables the model to adapt to both immediate disturbances and gradual environmental changes, ensuring reliable performance even in unpredictable scenarios.

While the TransformerTCN demonstrated exceptional results, its relatively complex architecture demands higher computational resources compared to simpler models. This requirement may limit its real-time applicability in resource-constrained environments. Future research could focus on optimizing the model to reduce computational overhead while maintaining accuracy, possibly through techniques such as pruning, quantization, or the integration of lightweight attention mechanisms.

In summary, the TransformerTCN-based delay compensation framework effectively addresses the specific challenges posed by communication delays in CMOR's control system. Its hybrid architecture delivers accurate predictions, robust performance, and enhanced adaptability, making it a transformative solution for real-time control in nuclear fusion environments and beyond.

# 6. Conclusion

This study introduces the TransformerTCN model as an effective solution for control delay compensation in the CMOR system, a robotic

platform essential for maintenance tasks within the CFETR fusion reactor. By integrating TCN with Transformer-based self-attention, the proposed model captures both short-term and long-term temporal dependencies, providing accurate predictions of CMOR's future states despite communication delays. The experimental validation demonstrated that TransformerTCN consistently outperforms traditional models in terms of error metrics, thereby enhancing the reliability and precision of robotic control in time-sensitive environments.

The contributions of this study to the field of robotic control systems are threefold. First, it provides a detailed examination of CMOR's delay challenges within the context of nuclear fusion maintenance. Second, it highlights the limitations of traditional predictive models in delay compensation and presents a robust alternative in the form of TransformerTCN. Third, this study lays the groundwork for future research on hybrid models that combine convolutional and attention-based architectures, offering a promising direction for applications requiring real-time decision-making under uncertainty.

In future research, further optimizations of the TransformerTCN model could focus on reducing computational complexity without sacrificing accuracy, potentially through model pruning or efficient attention mechanisms. Additionally, real-world testing across various operational scenarios within CFETR or similar fusion environments could further validate and refine this model's applicability. Exploring hybrid models that incorporate reinforcement learning could also enhance the adaptability of TransformerTCN, allowing for even more robust performance in dynamic, high-stakes applications.

In conclusion, the TransformerTCN-based delay compensation model offers a substantial improvement over traditional models, paving the way for more precise and reliable robotic control systems in nuclear fusion maintenance and other complex environments. The integration of temporal convolutions with self-attention provides a powerful framework that could inspire future innovations in time-series prediction and real-time control applications.

# **CRediT authorship contribution statement**

**Chenhui Wan:** Writing – original draft, Visualization, Validation, Methodology, Data curation, Conceptualization. **Zibo Qi:** Validation, Software. **Hongbin Huang:** Methodology. **Jie Liu:** Supervision, Project administration. **Youmin Hu:** Supervision, Project administration. **Hongtao Pan:** Supervision, Project administration. **Yong Cheng:** Supervision. **Yang Cheng:** Conceptualization. **Zhongxu Hu:** Writing – review & editing, Supervision, Methodology, Conceptualization.

# **Declaration of competing interest**

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

# **Data availability**

Data will be made available on request.

# **References**

- [1] J. Zheng, J. Qin, K. Lu, M. Xu, X. Duan, G. Xu, J. Hu, X. Gong, Q. Zang, Z. Liu, L. Wang, Recent progress in Chinese fusion research based on superconducting tokamak configuration, *Innov.* 3 (4) (2022).
- [2] Y. Wan, J. Li, Y. Liu, X. Wang, V. Chan, C. Chen, X. Duan, P. Fu, X. Gao, K. Feng, S. Liu, Overview of the present progress and activities on the CFETR, *Nucl. Fusion* 57 (10) (2017) 102009.
- [3] P. Zheng, X. Liu, Z. Zhang, J. Chen, S. Sun, A preliminary work on the preparation for neutron irradiation of advanced fusion materials using small samples in China, *J. Fusion Energy* 40 (2021) 1–13.
- [4] W. Zhao, Y. Cheng, X. Lin, H. Sun, J. Huang, Z. Gong, Y. Song, J. Li, X. Gao, H. Wu, Reliability based assessment of remote maintenance system for CFETR divertor, *Fusion Eng. Des.* 146 (2019) 2777–2780.
- [5] C. Wan, C. Zuo, X. Zhang, Y. Hu, Z. Qi, T. Huang, CMOR-DT: Tokamak device maintenance manipulator based on digital twin, in: 2023 IEEE Smart World Congress, SWC, IEEE, 2023, pp. 1–4.
- [6] H. Huang, H. Wang, Y. Wang, Y. Hu, F. Zhao, H. Zhong, C. Wan, B. Wu, P. Su, H. Pan, Y. Cheng, Engineering design and analysis of the root joints for the CFETR multi-purpose overload robot, *Fusion Eng. Des.* 205 (2024) 114557.
- [7] Z. Yao, H. Wu, Y. Song, Y. Cheng, H. Pan, M. Wu, M. Li, G. Qin, Q. Wang, X. Zhang, Surrogate model-based cognitive digital twin for smart remote maintenance of fusion reactor: modeling and implementation, *Nucl. Fusion* 64 (12) (2024) 126007.
- [8] M. Emami, A. Bayat, R. Tafazolli, A. Quddus, A survey on haptics: Communication, sensing and feedback, *IEEE Commun. Surv. Tutor.* (2024).
- [9] K. Darvish, L. Penco, J. Ramos, R. Cisneros, J. Pratt, E. Yoshida, S. Ivaldi, D. Pucci, Teleoperation of humanoid robots: A survey, *IEEE Trans. Robot.* 39 (3) (2023) 1706–1727.
- [10] B. Ning, Q.L. Han, L. Ding, Distributed finite-time secondary frequency and voltage control for islanded microgrids with communication delays and switching topologies, *IEEE Trans. Cybern.* 51 (8) (2020) 3988–3999.
- [11] X. Zhang, Y. Yang, H. Pan, Y. Cheng, Y. Song, An efficient NMPC-based multi-task control toolkit for remote handling applications, *Fusion Eng. Des.* 187 (2023) 113377.
- [12] Z. Yi, Y. Xu, W. Gu, Z. Fei, Distributed model predictive control based secondary frequency regulation for a microgrid with massive distributed resources, *IEEE Trans. Sustain. Energy* 12 (2) (2020) 1078–1089.
- [13] Y. Wang, J. Tian, Y. Liu, B. Yang, S. Liu, L. Yin, W. Zheng, Adaptive neural network control of time delay teleoperation system based on model approximation, *Sensors* 21 (22) (2021) 7443.
- [14] J. Wang, M. Krstic, Regulation-triggered adaptive control of a hyperbolic PDE-ode model with boundary interconnections, *Internat. J. Adapt. Control Signal Process.* 35 (8) (2021) 1513–1543.
- [15] S. Wang, M. Diagne, J. Qi, Delay-adaptive predictor feedback control of reaction–advection–diffusion PDEs with a delayed distributed input, *IEEE Trans. Autom. Control* 67 (7) (2021) 3762–3769.
- [16] Y. Zhu, M. Krstic, H. Su, Adaptive output feedback control for uncertain linear time-delay systems, *IEEE Trans. Autom. Control* 62 (2) (2016) 545–560.
- [17] S. Wang, J. Qi, M. Krstic, Delay-adaptive control of first-order hyperbolic partial integro-differential equations, *Internat. J. Robust Nonlinear Control* 34 (10) (2024) 6784–6803.
- [18] G. Graf, H. Xu, D. Schitz, X. Xu, Improving the prediction accuracy of predictive displays for teleoperated autonomous vehicles, in: 2020 6th International Conference on Control, Automation and Robotics (ICCAR). IEEE, 2020, pp. 440–445.
- [19] H. Dybvik, M. Løland, A. Gerstenberg, K.B. Slåttsveen, M. Steinert, A low-cost predictive display for teleoperation: Investigating effects on human performance and workload, *Int. J. Hum.-Comput. Stud.* 145 (2021) 102536.
- [20] X. Zhang, H. Lin, Performance guaranteed human-robot collaboration with POMDP supervisory control, *Robot. Comput.-Integr. Manuf.* 57 (2019) 59–72.
- [21] J. Storms, K. Chen, D. Tilbury, A shared control method for obstacle avoidance with mobile robots and its interaction with communication delay, *Int. J. Robot. Res.* 36 (5–7) (2017) 820–839.
- [22] J. Luo, Z. Lin, Y. Li, C. Yang, A teleoperation framework for mobile robots based on shared control, *IEEE Robot. Autom. Lett.* 5 (2) (2019) 377–384.
- [23] K.I. Yoon, D.K. Ko, S.C. Lim, Real-time video prediction using gans with guidance information for time-delayed robot teleoperation, *Int. J. Control. Autom. Syst.* 21 (7) (2023) 2387–2397.
- [24] J. Su, L. Wang, C. Liu, H. Qiao, Robotic inserting a moving object using visual-based control with time-delay compensator, *IEEE Trans. Ind. Informatics* 20 (2) (2023) 1842–1852.
- [25] S. Tan, J. Yang, H. Ding, A prediction and compensation method of robot tracking error considering pose-dependent load decomposition, *Robot. Comput.-Integr. Manuf.* 80 (2023) 102476.
- [26] P. Ferrari, A. Flammini, S. Vitturi, Performance analysis of PROFINET networks, *Comput. Stand. Interfaces* 28 (4) (2006) 369–385.
- [27] PROFIBUS & PROFINET International, n.d. PROFIsafe [Online]. Available at: <https://www.profinet.com/technologies/profisafe> (Accessed: 26 November 2024).
- [28] A.G. Siemens, DRIVE-CLiQ – the New Communication Interface for SINAMICS, Siemens Technical Publications, 2015.
- [29] ISO, ISO 11898-1:2015 Road Vehicles - Controller Area Network (CAN) - Part 1: Data Link Layer and Physical Signaling, International Organization for Standardization, 2015.
- [30] A.G. Siemens, 2023, Siemens [Online]. Available at: <https://www.siemens.com/> (Accessed: 26 November 2024).
- [31] LTN Servotechnik GmbH, 2023, LTN Servotechnik GmbH [Online]. Available at: <https://www.ltn-servotechnik.com/> (Accessed: 26 November 2024).
- [32] D.R. JOHANNES HEIDENHAIN GmbH, 2023, HEIDENHAIN | Controls, encoders, and digital readouts [Online]. Available at: <http://www.heidenhain.com/> (Accessed: 26 November 2024).
- [33] REISSMANN Sensortechnik GmbH, 2023, REISSMANN Sensortechnik GmbH [Online]. Available at: <https://www.reissmann.com/> (Accessed: 26 November 2024).
- [34] S. Bai, J.Z. Kolter, V. Koltun, An empirical evaluation of generic convolutional and recurrent networks for sequence modeling, 2018, arXiv preprint arXiv: 1803.01271.
- [35] A. Vaswani, Attention is all you need, *Adv. Neural Inf. Process. Syst.* (2017).