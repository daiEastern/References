

![Elsevier logo featuring a tree and the word ELSEVIER](935eed7aa61f7777f62cfc032e11bee9_img.jpg)

Elsevier logo featuring a tree and the word ELSEVIER

![Cover image of the journal Energy](390120de4fe440c42fea8154fcaad334_img.jpg)

Cover image of the journal Energy

![Check for updates button](0538daaa5583c23e17db3a12f2281a55_img.jpg)

Check for updates button

# Identification, prediction and classification of hydrogen-fueled Wankel rotary engine knock by data-driven based on combustion parameters

Hao Meng<sup>a,\*</sup>, Qiang Zhan<sup>a</sup>, Changwei Ji<sup>b</sup>, Jinxin Yang<sup>b</sup>, Shuofeng Wang<sup>b</sup>

<sup>a</sup> School of Machinery and Automation, Weifang University, Weifang, 261000, China

<sup>b</sup> College of Mechanical and Energy Engineering, Beijing Lab of New Energy Vehicles and Key Lab of Regional Air Pollution Control, Beijing University of Technology, Beijing, 100124, China

## ARTICLE INFO

Handling Editor: X Ou

### Keywords:

Hydrogen-fueled Wankel rotary engine  
Knock  
Gaussian Mixture Model  
Multiple Linear Regression  
Support vector machine  
Back-propagation Neural Network

## ABSTRACT

Hydrogen-fueled Wankel rotary engine has excellent power density and low backfire possibility, however, as well as the severe knock. The knock is closely related to the in-cylinder combustion process, therefore, the present work is conducted to identify, predict and classify the knock by data-driven based on combustion parameters in the hydrogen-fueled Wankel rotary engine. The results show that: Knock type can be identified well according to knock intensity and crank angle of peak knock pressure through the Gaussian Mixture Model. There are 141 strong knock cycles and 809 weak knock cycles in test data. Compared with Support Vector Machines and Back-propagation Neural Networks, Multiple Linear Regression has a better global performance in knock-level prediction based on combustion parameters. The maximum pressure rising rate and CA50 have more significant impacts on knock, the partial of regression coefficients of which is about 0.42 and -0.58, respectively. In particular, due to different formation mechanisms, the prediction models of two types of knock are recommended to be established separately. In addition, the Support Vector Machine can be applied to conduct knock classification. Among kernel functions in Support Vector Machine, the linear kernel function can achieve optimal mean test accuracy, about 88.66 %.

## 1. Introduction

As the concerns relevant to global warming are increasingly mounting, some countries and regions jointly formulate policies to reduce CO<sub>2</sub> emissions in daily life and production [1,2]. Transportation, as the major section of CO<sub>2</sub> generation [3], has the responsibility to buffer the greenhouse effect. Hydrogen is a renewable eco-friendly energy [4]. Hydrogen-fueled internal combustion engine (ICE) is an interesting potential to alter fossil-fueled ICEs due to the excellent physicochemical characteristics of hydrogen [5,6]. Except for almost zero carbon emissions, hydrogen-fueled ICEs also can achieve superb efficiency [7] and power characteristics [8], however, as well as high NO<sub>x</sub> emission [9] and severe abnormal combustion [10].

In hydrogen-fueled ICEs, knock, as an important role in abnormal combustion, will significantly deteriorate the performance and even endanger the hardware of ICEs [11]. Knock not only reduces the thermal efficiency and limits the ICE compression ratio or vehicle acceleration performance [12], but also results in cylinder body erosion and piston ring breakage [13], therefore, it is urgent to understand the knock

mechanism to seek solutions. There are two formations of knock in hydrogen-fueled ICE [14]: The first one (hereinafter referred to as SK or strong knock) is caused by the auto-ignition end gas, which usually occurs at a certain moment during the combustion and can realize strong impacts on the combustion; the second one (hereinafter referred to as WK or weak knock) is caused by the rapidly advancing hydrogen flame front, which usually accompanies the total combustion process and has weak impacts on the combustion. Meng et al. found that two knocks would produce apparent diversity in heat-release characteristics under the same operating condition. Szwaja et al. [15] concluded that hydrogen-fueled ICE knock is closely related to the burning velocity and crank angle corresponding to the combustion duration. Since the heat release process is sensitive to the operating conditions, such as engine speed, ignition timing [16], excess air ratio [17], compression ratio [12], intake temperature and so on, knock characteristics are also influenced by them. In particular, contrary to fossil-fueled ICEs, the knock intensity of hydrogen-fueled ICEs has a positive relationship with engine speed due to WK.

Due to some random factors during engine operation, the intensity,

\* Corresponding author.

E-mail address: [menghaowfu@163.com](mailto:menghaowfu@163.com) (H. Meng).

timing and even occurrence of knock have great randomness [18]. In particular, there are significant differences between the knock of consecutive cycles even if under strictly constant operating condition [19]. Limited by the global thermodynamics atmosphere, the knock can be characterized by the Gaussian distribution [20], hence, the statistical model is a potential method for quantifying and characterizing hydrogen-fueled ICE knock, which can provide effective guidance for knock detection and control system on engine. Machine learning [21], a powerful data analysis tool, can discover potential patterns and laws in data and perform tasks such as prediction, classification and decision-making, without understanding professional knowledge, which is currently widely used in numerous fields, including ICEs. Wei et al. [22] reviewed the application of Machine Learning techniques in combustion. They concluded that the combination of Machine Learning and engine experiment is a robust method to predict engine combustion and performance. In terms of engine combustion, Issondj et al. [23] found that compared with thermal and transport equations, machine learning algorithms allow a higher accuracy and lower calculation cost in the estimation of in-cylinder turbulent flame speed. Wang et al. [24] obtained a superb ignition delay prediction model of n-butane/hydrogen mixture based on back-propagation neural network (BPNN) coupling Genetic algorithm; in terms of engine performance, Issondj et al. proved that deep neural networks have excellent ability in the prediction of ICE emission [25]. Taghavifar et al. [26] demonstrated that a well-trained artificial neural network has a satisfactory performance in predicting soot and NOx emissions in the diesel engine. Wang et al. [27] certified the potential of a genetic algorithm optimized Support Vector Machine (SVM) on the performance prediction of ICE. Aramburu et al. [28] found that both One-class SVM (OC-SVM) and Convolutional Neural Network (CNN) can effectively detect knock and are better than traditional Maximum amplitude pressure oscillation. In addition, they proposed a knock detection method, which is based on the combination of short-time Fourier transform and SVM [29].

Overall, Machine Learning is a potential tool for the prediction of engine characteristic parameters. As mentioned above, some random factors and cyclic variation of ICEs endow knock with randomness, therefore, it is unable to intuitively obtain the patterns of knock with some parameters. In particular, two natures of knock greatly complex the knock mechanism in hydrogen-fueled ICEs. Wankel rotary engine (WRE) has high power density [30] and compact structure [31], which fueled by hydrogen can achieve satisfactory power [32] and negligible backfire [33], however, as well as severe knock due to the elongated combustion chamber and high thermal-load power stroke. At present, few works are reporting on the application of Machine Learning in the research on knock, especially hydrogen-fueled ICEs knock. The present work utilized advancing Machine Learning algorithms to identify, predict and classify the knock in hydrogen-fueled Wankel rotary engine through combustion parameters, in order to understand the influence mechanism of knock on the combustion process and establish knock type identification, knock level prediction and knock type classification model.

## Nomenclature

|             |                                        |               |                                          |
|-------------|----------------------------------------|---------------|------------------------------------------|
| <b>ATDC</b> | After top dead center                  | <b>MLR</b>    | Multiple linear regression               |
| <b>BPNN</b> | Back-propagation neural network        | <b>MPPRR</b>  | Maximum in-cylinder pressure rising rate |
| <b>BTDC</b> | Before top dead center                 | <b>OC-SVM</b> | One-class SVM                            |
| <b>CAKI</b> | Crank angle of peak knock pressure     | <b>OLS</b>    | Ordinary least squares                   |
| <b>CA10</b> | Crank angle of 10 % total heat release | <b>PDF</b>    | Probability density function             |
| <b>CA50</b> | Crank angle of 50 % total heat release | <b>R2</b>     | Coefficient of determination             |
| <b>CA90</b> | Crank angle of 90 % total heat release | <b>RBf</b>    | Radial basis function                    |

(continued on next column)

(continued)

|            |                              |            |                        |
|------------|------------------------------|------------|------------------------|
| <b>CNN</b> | Convolutional neural network | <b>SK</b>  | Strong knock           |
| <b>ECU</b> | Electronic control unit      | <b>SVM</b> | Support vector machine |
| <b>GMM</b> | Gaussian mixture model       | <b>TDC</b> | Top dead center        |
| <b>ICE</b> | Internal combustion engine   | <b>WK</b>  | Weak knock             |
| <b>KI</b>  | Knock intensity              | <b>WRE</b> | Wankel rotary engine   |

## 2. Experiment and applied algorithms

### 2.1. Experiment

The Mazda 13B WRE is applied in this work, the specifications of which are shown in Table 1. To achieve fuel substitution, some works were done before the experiment: (1) Design and develop a hydrogen supply system, including a high-pressurized hydrogen tank, pressure regulator, smart control box (adjust and monitor hydrogen flow), backfire arrestor of hydrogen, hydrogen common rail and port-injected hydrogen nozzles. The original gasoline supply system is completely removed; (2) An in-cylinder pressure sensor is coupled to the leading spark plug; (3) The self-developed electronic control unit (ECU) interacts with the original ECU and sensors to accurately control the signals relevant to ignition and fuel supply; (4) Additional trigger wheel and engine speed sensor are installed to allow recognition by the combustion analyzer. Fig. 1 shows the detailed modification and the test bench. The detailed information of the experimental system can refer to previous work [34].

The test was conducted at 2000 r/min, wide-open throttle, 1.2 excess air ratio and 7°CA before top dead center (BTDC) ignition timing with synchronous ignition, and 1000 consecutive cycles were recorded. In hydrogen-fueled WRE, knock sometimes leads to backfire, hence, there are some meaningless cycles [33]. After data filtering, 950 cycles were used in the present work.

### 2.2. Knock and combustion parameters

In ICEs, the knock signal can be separated from the combustion signal by a digital filter [35]. Based on previous work, a 3–20 kHz band-pass filter was adopted in the present work [16]. After filtering the combustion pressure with the band-pass filter, the knock pressure as shown in Fig. 2 can be obtained. Usually, knock intensity (KI) is defined to characterize the level of knock. In addition, the crank angle of peak knock pressure (CAKI) is applied to represent the strongest moment of knock.

In this work, some combustion parameters, including peak in-cylinder pressure ( $P_{max}$ ), crank angle of  $P_{max}$ , maximum in-cylinder pressure rising rate (MPPRR), CA10, CA50 and CA90, are used to investigate the impacts of knock on the combustion process and establish knock prediction and classification model.

**Table 1**  
Engine specifications.

| Specification        | Value/Form                      |
|----------------------|---------------------------------|
| Number of rotors     | 2                               |
| Cooling method       | Water-cooled                    |
| Ignition source      | Spark plug                      |
| Intake method        | Side-ported, natural aspiration |
| Exhaust method       | Side-ported                     |
| Generating radius/mm | 105                             |
| Width of rotor/mm    | 80                              |
| Displacement/L       | 0.654 L                         |
| Compression ratio    | 10                              |
| Eccentricity/mm      | 15                              |
| Power output         | 121 kW/5500 rpm                 |
| Intake timing/(°CA)  | 3° ATDC, 38° ABDC               |
| Exhaust timing/(°CA) | 80° BBDC, 3° BTDC               |

![Figure 1: Detailed modifications of WRE. The image shows a composite of three photographs of an engine setup. The left photo shows a '23 gears trigger wheel' and a 'Photoelectron magnetic sensor' connected by a red cable. The middle photo shows an 'Intake manifold' and a 'Hydrogen nozzle'. The right photo shows a 'Piezoelectric pressure sensor' mounted on a pipe. Yellow arrows point to each of these components.](7e2f2d03a5dda38b038fd4884629a2b4_img.jpg)

Figure 1: Detailed modifications of WRE. The image shows a composite of three photographs of an engine setup. The left photo shows a '23 gears trigger wheel' and a 'Photoelectron magnetic sensor' connected by a red cable. The middle photo shows an 'Intake manifold' and a 'Hydrogen nozzle'. The right photo shows a 'Piezoelectric pressure sensor' mounted on a pipe. Yellow arrows point to each of these components.

Fig. 1. The detailed modifications of WRE.

![Figure 2: Knock pressure, KI and CAKI. A dual-axis plot showing engine performance. The left y-axis is 'In-cylinder pressure/bar' (0 to 50) and the right y-axis is 'Knock pressure/bar' (-8 to 12). The x-axis is 'Crank angle/°CA ATDC' (-40 to 80). A red line represents 'In-cylinder pressure' and a blue line represents 'Knock pressure'. A dashed black line indicates 'Knock intensity' and a vertical dashed line marks the 'Crank angle of peak knock pressure' at approximately 15°CA ATDC.](a854aa286b14d26d27047ee5893ffaa7_img.jpg)

Figure 2: Knock pressure, KI and CAKI. A dual-axis plot showing engine performance. The left y-axis is 'In-cylinder pressure/bar' (0 to 50) and the right y-axis is 'Knock pressure/bar' (-8 to 12). The x-axis is 'Crank angle/°CA ATDC' (-40 to 80). A red line represents 'In-cylinder pressure' and a blue line represents 'Knock pressure'. A dashed black line indicates 'Knock intensity' and a vertical dashed line marks the 'Crank angle of peak knock pressure' at approximately 15°CA ATDC.

Fig. 2. Knock pressure, KI and CAKI.

### 2.3. Applied algorithms

In the present work, four advancing Machine Learning algorithms are applied. All the calculations are done through Matlab R2023b.

#### 2.3.1. GMM

The Gaussian Mixture Model (GMM) [36] is a probabilistic model for representing normally distributed subpopulations within an overall population. GMM assumes that the data is generated from a mixture of several probability distributions, each representing a different cluster or subpopulation. In the case of GMM, each component of the mixture is a Gaussian (normal) distribution, characterized by its mean value and covariance. The GMM is used to identify the knock type in the present work.

The GMM is defined as a weighted sum of  $K$  Gaussian components, each described by a mean vector  $\mu_k$ , a covariance matrix  $\Sigma_k$ , and a mixture weight  $\pi_k$ . The probability density function (PDF) of the GMM is given by:

$$p(X|\lambda) = \sum_{k=1}^{K} \pi_k \mathcal{N}(X|\mu_k, \Sigma_k) \quad (2.1)$$

Where  $\lambda = \{\pi_k, \mu_k, \Sigma_k\}_{k=1}^{K}$  are the parameters of the model,  $X$  is the data vector, and  $\mathcal{N}(X|\mu_k, \Sigma_k)$  is the PDF of the  $k$ -th Gaussian component defined as:

$$\mathcal{N}\left(X \middle| \mu_k, \Sigma_k\right) = \frac{1}{(2\pi)^{\frac{d}{2}} |\Sigma_k|^{\frac{1}{2}}} \exp\left(-\frac{1}{2}(X - \mu_k)^T \Sigma_k^{-1} (X - \mu_k)\right) \quad (2.2)$$

Here,  $d$  is the dimensionality of the data.

#### 2.3.2. MLR

Multiple linear regression (MLR) [37] is a fundamental statistical model that describes the relationship between one dependent variable and two or more independent variables. Multiple Linear Regression extends simple linear regression by allowing for the inclusion of multiple predictors, thereby providing a more comprehensive understanding of the relationship between variables. In the present work, the MLR algorithm is applied to establish the knock predictive model.

The MLR model can be expressed as:

$$y = X\beta + e \quad (2.3)$$

Where  $y$  is an  $n \times 1$  vector of the dependent variable;  $X$  is an  $n \times (p+1)$  matrix of the independent variables (including a column of ones for the intercept);  $\beta$  is a  $(p+1) \times 1$  vector of the coefficients;  $e$  is an  $n \times 1$  vector of the errors.

The coefficients  $\beta$  in the MLR model are typically estimated using the Ordinary Least Squares (OLS) method. The OLS method aims to minimize the sum of the squared differences between the observed values and the values predicted by the model. The estimated coefficients  $\hat{\beta}$  can be computed as:

$$\hat{\beta} = (X^T X)^{-1} X^T y \quad (2.4)$$

Here,  $X^T$  is the transpose of the matrix  $X$ , and  $(X^T X)^{-1}$  is the inverse of the matrix  $X^T X$ .

#### 2.3.3. SVM

SVM [38] aims to identify the optimal hyperplane that distinctly separates data points belonging to different classes in a high-dimensional space. The optimal hyperplane is defined as the one that maximizes the margin, which is the distance between the hyperplane and the nearest data points from each class, known as support vectors. The principle schematic diagram of SVM is shown in Fig. 3. Except for establishing the knock predictive model, SVM also is applied to establish the knock classifying model in the present work.

In scenarios where data is not linearly separable, SVM employs kernel functions to transform the data into a higher-dimensional space, facilitating linear separation. Commonly used kernels include:

(1) Linear Kernel:

$$K(x_i, x_j) = x_i^T x_j \quad (2.5)$$

![Support Vector Machine (SVM) schematic diagram showing a linear decision boundary separating two classes of data points (Class 1 in blue and Class 2 in orange) in a 2D feature space (Feature 1 vs Feature 2). The diagram includes support vectors (circled points on the boundary), a decision hyperplane (solid black line), and a margin (dashed lines).](7fb5215fd72210a2e4cce6df55550c89_img.jpg)

Support Vector Machine (SVM) schematic diagram showing a linear decision boundary separating two classes of data points (Class 1 in blue and Class 2 in orange) in a 2D feature space (Feature 1 vs Feature 2). The diagram includes support vectors (circled points on the boundary), a decision hyperplane (solid black line), and a margin (dashed lines).

Fig. 3. The principle schematic diagram of SVM.

##### (2) Polynomial Kernel

$$K(x_i, x_j) = (x_i \cdot x_j + c)^d \quad (2.6)$$

##### (3) Radial Basis Function (rbf) Kernel:

$$K(x_i, x_j) = \exp(-\gamma \|x_i - x_j\|^2) \quad (2.6)$$

The selection of the kernel function and its parameters significantly impacts the SVM model's performance. All these three kernel functions were applied in the present work. And the box constraint of SVM model is selected as 1.

#### 2.3.4. BPNN

BPNN [39] is a class of artificial neural networks that utilize a supervised learning algorithm called backpropagation for training. The training of a BPNN involves two main phases: forward propagation and backward propagation. In forward propagation, input data is passed through the network layer by layer. Each neuron computes a weighted sum of its inputs, adds a bias and applies an activation function to produce an output, which becomes the input for the next layer. In backward propagation, the weights and biases are adjusted to minimize the error between the predicted output and the actual output. This is done by propagating the error backward through the network. The error is computed using a loss function (e.g., mean squared error for regression tasks or cross-entropy for classification tasks). Gradients of the loss function concerning each weight and bias are calculated using the chain rule of calculus. These gradients are then used to update the weights and biases via an optimization algorithm, typically gradient descent. The process diagram of BPNN is shown in Fig. 4. The learning rate of BPNN in this work is 0.01.

![Process diagram of BPNN showing the flow from Input X to Hidden layer H, then to Output Y. The output Y is compared with the Expected output. If 'Yes', the process ends; if 'No', the weights and biases are updated layer by layer backwards, and the process loops back to the Input X stage.](37a6ab1d23efb9dc00cfae09d353b1da_img.jpg)

Process diagram of BPNN showing the flow from Input X to Hidden layer H, then to Output Y. The output Y is compared with the Expected output. If 'Yes', the process ends; if 'No', the weights and biases are updated layer by layer backwards, and the process loops back to the Input X stage.

Fig. 4. Process diagram of BPNN.

## 3. Results and discussion

### 3.1. Knock identification

CA50-CAKI is defined as the crank angle intervals from CA50 to CAKI to represent the order and distance of occurrence between the strongest knock timing and combustion center. Fig. 5 shows the relationship between KI and CA50-CAKI. It can be found from Fig. 5 that there is usually a large KI when the CAKI approaches CA50 and higher KI is obtained when the CAKI is later than CA50. The reasons are as follows: For the WK, the KI of it is mainly affected by the burning velocity, which is impacted by the balance between pressure and fuel molar concentration (combustion chamber space). For the SK, the KI of it is closely related to the amount of auto-ignition end gas. If knock occurs earlier, it means that more end gas would spontaneously burn, thus resulting in severe knock. Besides, it also can be found from Fig. 5 that under the same condition, SK can achieve significantly larger KI than WK, which is the reason that they are named strong and weak knock, respectively.

Although knock categories can be qualitatively analyzed based on CAKI and KI combined with the generation mechanism, quantitative identification is still not possible. Given that the two types of knock are caused by different mechanisms and can be seen as two independent events, therefore, both of them theoretically follow the respective Gaussian distribution (normal distribution). In this work, GMM is applied to distinguish data according to some features and identify the knock type. Fig. 6a and b shows the histogram and scatter plot of GMM training results based on CAKI. It can be found that GMM successfully separates the data into two Gaussian distributions, named SK and WK according to their generation mechanisms. The mean value and covariance of SK are  $-7.23$  and  $24.42$  and those of WK are  $4.25$  and  $22.22$ . However, it can be seen from Fig. 6b that the separated data is

![Scatter plot showing the relationship between Knock intensity (KI) in bar (y-axis, 0 to 7) and CA50-CAKI in degrees CA (x-axis, -25 to 20). The data points are clustered into two groups: a lower group (WK) and a higher group (SK). A vertical red dashed line at approximately -2.5 degrees CA separates the two groups.](06509cc49f3023389a3f15c106907140_img.jpg)

Scatter plot showing the relationship between Knock intensity (KI) in bar (y-axis, 0 to 7) and CA50-CAKI in degrees CA (x-axis, -25 to 20). The data points are clustered into two groups: a lower group (WK) and a higher group (SK). A vertical red dashed line at approximately -2.5 degrees CA separates the two groups.

Fig. 5. The relationship between KI and CA50-CAKI.

![Figure 6: Training results of GMM based on CAKI. (a) Histogram showing the distribution of CA50-CAKI/°CA for Strong knock (blue hatched) and Weak knock (red solid). (b) Scatter plot of Knock intensity/bar versus CA50-CAKI/°CA, with Strong knock (orange dots) and Weak knock (blue dots).](7a3561af571faf036baa93f5f4b1bdb9_img.jpg)

Figure 6 consists of two subplots. Subplot (a) is a histogram showing the frequency distribution of the normalized CA50-CAKI value. The x-axis ranges from -25 to 20, and the y-axis (Count) ranges from 0 to 100. The histogram shows two distinct peaks: a smaller one around -10 (labeled 'Strong knock' with a blue hatched fill) and a larger one around 5 (labeled 'Weak knock' with a red solid fill). Subplot (b) is a scatter plot of Knock intensity (y-axis, 0 to 7 bar) versus CA50-CAKI/°CA (x-axis, -25 to 20). The data points are colored by knock type: orange for 'Strong knock' and blue for 'Weak knock'. The orange points are concentrated at higher knock intensities (above 1 bar) and negative CA50-CAKI values, while the blue points are mostly at lower knock intensities (below 1 bar) and positive CA50-CAKI values.

Figure 6: Training results of GMM based on CAKI. (a) Histogram showing the distribution of CA50-CAKI/°CA for Strong knock (blue hatched) and Weak knock (red solid). (b) Scatter plot of Knock intensity/bar versus CA50-CAKI/°CA, with Strong knock (orange dots) and Weak knock (blue dots).

Fig. 6. The training results of GMM based on CAKI: (a) histogram and (b) scatter plot.

unreasonable. Due to only CAKI as the standard, some apparent SK is mistakenly assigned to WK and vice versa. Hence, CAKI alone can not be used as the criterion for knock-type identification.

Fig. 7a and b displays the histogram and scatter plot of GMM training results based on the criterion of both KI and CAKI. In this model, the mean value and covariance of SK are  $-3.21$  and  $54.12$  while those of WK are  $4.17$  and  $22.85$ . It can be found that compared with CAKI alone as the criterion, the combination of KI and CAKI as the criterion has a better effect. On the one hand, the addition of KI enables the GMM to take into account the combination of KI and CAKI during calculation, making data with high KI more easily classified as SK. On the other hand, the division of WK becomes more reasonable, especially for WK with CAKI later than CA50. Although a datum is clearly misclassified into SK, this does not affect the global rationality of the identification model. According to the calculation results, there are 141 SK cycles and 809 WK cycles in the given data.

### 3.2. Relationship between knock and combustion parameters

In this subsection, the relationships between KI and some

![Figure 8: 3D surface plot showing Knock intensity/bar as a function of Pmax (bar) and MPRR/(bar/°CA). The surface is colored by knock intensity, ranging from blue (low) to red (high).](bc04d002fc79e8a3637b1552ac3361e6_img.jpg)

Figure 8 is a 3D surface plot showing the relationship between Knock intensity (y-axis, 0 to 6 bar) and two combustion parameters: Pmax (x-axis, 40 to 0 bar) and MPRR/(bar/°CA) (z-axis, 45 to 25 bar/°CA). The surface is colored with a gradient from blue (low knock intensity) to red (high knock intensity). The surface shows a sharp increase in knock intensity as Pmax decreases and MPRR/(bar/°CA) increases, forming a steep wall-like structure.

Figure 8: 3D surface plot showing Knock intensity/bar as a function of Pmax (bar) and MPRR/(bar/°CA). The surface is colored by knock intensity, ranging from blue (low) to red (high).

Fig. 8. KI at different Pmax and MPRR.

![Figure 7: Training results of GMM based on KI and CAKI. (a) Histogram showing the distribution of CA50-CAKI/°CA for Strong knock (blue hatched) and Weak knock (red solid). (b) Scatter plot of Knock intensity/bar versus CA50-CAKI/°CA, with Strong knock (orange dots) and Weak knock (blue dots).](1a6d75c94d3fd49936527eadd25e9278_img.jpg)

Figure 7 consists of two subplots. Subplot (a) is a histogram showing the frequency distribution of the normalized CA50-CAKI value. The x-axis ranges from -25 to 20, and the y-axis (Count) ranges from 0 to 100. The histogram shows two distinct peaks: a smaller one around -10 (labeled 'Strong knock' with a blue hatched fill) and a larger one around 5 (labeled 'Weak knock' with a red solid fill). Subplot (b) is a scatter plot of Knock intensity (y-axis, 0 to 7 bar) versus CA50-CAKI/°CA (x-axis, -25 to 20). The data points are colored by knock type: orange for 'Strong knock' and blue for 'Weak knock'. The orange points are concentrated at higher knock intensities (above 1 bar) and negative CA50-CAKI values, while the blue points are mostly at lower knock intensities (below 1 bar) and positive CA50-CAKI values.

Figure 7: Training results of GMM based on KI and CAKI. (a) Histogram showing the distribution of CA50-CAKI/°CA for Strong knock (blue hatched) and Weak knock (red solid). (b) Scatter plot of Knock intensity/bar versus CA50-CAKI/°CA, with Strong knock (orange dots) and Weak knock (blue dots).

Fig. 7. The training results of GMM based on KI and CAKI: (a) histogram and (b) scatter plot.

combustion parameters are discussed to understand the influence mechanism of combustion on knock. Fig. 8 shows the KI at different Pmax and MPRR. It can be found from Fig. 8 that high KI usually corresponds to high Pmax and MPRR. The reasons are as follows: For the operation cycles, on the premise of constant ignition timing, engine speed and load, high Pmax and MPRR mean high temperature and fuel molar concentration during the combustion process, which typically results in rapid burning velocity [40] and a high tendency for spontaneous combustion of end gas, therefore, high KI is prone to be achieved. However, due to some random factors or cyclic variation, high Pmax or MPRR may also correspond to low KI as shown in Fig. 8, especially Pmax, hence, more parameters need to be introduced to establish the knock prediction model.

Fig. 9 shows the KI at varied CA10 and CA50. It can be found that although the randomness of knock results in disorder within a certain range, earlier CA10 and CA50 usually correspond to higher KI in the global distribution. Since the ignition timing is near the top dead center (TDC), earlier CA10 means that the combustion may occur at a smaller combustion chamber, corresponding to higher fuel molar concentration and consequent combustion temperature. On the one hand, it accelerates the burning velocity [41] and thus leads to more severe WK; on the other hand, it enhances the in-cylinder temperature and pressure and provides an ideal thermal atmosphere related to the spontaneous combustion of hydrogen/air mixture, thus resulting in stronger SK.

### 3.3. Knock prediction

Based on the analysis in the previous section, it can be seen that there is a certain regularity between knock parameters and combustion parameters. However, due to the randomness of knock, it is not possible to characterize knock characteristics well by single combustion parameters. Therefore, in this section, Pmax, crank angle of Pmax, MPRR, CA10, CA50 and CA90 are jointly adopted to more accurately predict knock level. In this section, MLR, SVM with linear, rbf and polynomial kernel functions and BPNN are compared to find a more suitable computational model relevant to knock prediction. In addition, when dividing the training and testing sets, random seeds ranging from 1 to 50 are used to compare the global performance of the calculation model under the same training and testing sets.

Fig. 10 shows the coefficient of determination ( $R^2$ ) for the incremental order of different models.  $R^2$  can be used to quantify the model performance and the closer it is to 1, the better the model performance. It can be intuitively observed that although the maximum  $R^2$  of BPNN and SVM with polynomial kernel function are higher than that of those three, they have poor global prediction accuracy. More than 50 % of  $R^2$  is less than 0 and some are even lower than -100. Compared with these

two, MLR and SVM with linear and rbf kernel functions have better performance. In particular, MLR has the best global performance and exceeds 50 %  $R^2$  in MLR is apparently higher than that of SVM with linear and rbf kernel functions. Hence, it is recommended to use MLR as the knock prediction algorithm.

Since SK and WK have different generation mechanisms, the simultaneous prediction of SK and WK by a single model may cause a reduction in model accuracy. Therefore, based on the identification in section 3.1, the SK and WK are trained independently. Fig. 11a and b shows the  $R^2$  for the incremental order of SK and WK, respectively. Similar to the results in Fig. 10, SVM with polynomial kernel function and BPNN still have poor performance in individual prediction of SK and WK, especially SK. For SK prediction, MLR and SVM with linear kernel function have similar excellent performance and are significantly better than SVM with the rbf kernel function. For WK prediction, MLR and SVM with linear and rbf kernel functions have similar performance, however, their predictive performances are not as good as those in SK prediction. The maximum  $R^2$  of all of them are lower than 0.25.

It can be concluded from Figs. 10 and 11 that among the given models, MLR has the optimal global performance. Fig. 12 compared the  $R^2$  for incremental order of the MLR model in all knock, SK and WK predictions, respectively. It can be illustrated from Fig. 12 that the prediction of SK is slightly better than that of all knock, which is mainly due to the poor predictive ability of the MLR model for WK, resulting in a decrease in all knock predictive performance. Therefore, it is necessary to conduct independent predictions for SK and WK. More combustion parameters or more suitable prediction models need to be introduced to achieve accurate prediction of WK. In addition, Fig. 12 displays the partial regression coefficient of the trained MLR model. It can be found that the absolute value of the partial regression coefficients of MPRR and CA50 are obviously higher than that of other parameters, illustrating that MPRR and CA50 play a more important role in influencing knock level. And CA90 has the lowest impact weight.

### 3.4. Knock classification

As mentioned in section 3.3, it is necessary to establish the individual prediction model of WK and SK, therefore, a knock classification model is significant to identify the knock type in advance. Except for regressive tasks, SVM can also be applied to classified tasks well. In Fig. 13, the test accuracy of train and test set at the SVM model with linear, rbf and polynomial kernel functions are shown. Similar to knock prediction, random seeds ranging from 1 to 50 are set when dividing the train and test sets. It can be found from Fig. 13 that for all three kernel functions, the test accuracy of the train set is higher than that of the test set, as well as a lower standard deviation. It is reasonable since the model is trained by the train set. For the test set, the SVM with linear kernel function has the highest meaning test accuracy, about 88.66 %, which is 1.52 % and 2.03 % higher than that of the SVM with rbf and polynomial kernel function, respectively, illustrating that SVM with linear kernel function has better performance in knock classification. In addition, there is a minimum test accuracy difference between the train set and test set at SVM with the linear kernel function. On the one hand, this indicates that the model has good generalization ability and moderate complexity, and on the other hand, it also proves the consistency of data partitioning.

Fig. 14 shows the test set in one of the partitions based on SVM with linear kernel function, as well as annotated real SK and predictive SK. It can be found that the model has good classification ability for SK, especially for SK with high KI. However, for the SK with low KI, the classification ability of the model is relatively poor, which requires further improvement of the model or integration with other advanced Machine Learning algorithms.

## 4. Conclusions

The present work focuses on the relationship between knock and

![Figure 9: A 3D surface plot showing Knock intensity (bar) as a function of CA50 (°CA ATDC) and CA10 (°CA ATDC). The surface is predominantly blue, indicating low knock intensity, with a sharp, high-intensity peak (red/yellow) located at approximately CA50 = 22.5 and CA10 = 8.5. The x-axis (CA50) ranges from 18 to 26, and the y-axis (CA10) ranges from 10 to 6. The z-axis (Knock intensity) ranges from 0 to 6.](eba8385d0983fbda9dc1df0812273269_img.jpg)

Figure 9: A 3D surface plot showing Knock intensity (bar) as a function of CA50 (°CA ATDC) and CA10 (°CA ATDC). The surface is predominantly blue, indicating low knock intensity, with a sharp, high-intensity peak (red/yellow) located at approximately CA50 = 22.5 and CA10 = 8.5. The x-axis (CA50) ranges from 18 to 26, and the y-axis (CA10) ranges from 10 to 6. The z-axis (Knock intensity) ranges from 0 to 6.

Fig. 9. KI at different CA10 and CA50.

![Figure 10: A line graph showing the Coefficient of determination (R²) for incremental order of different models (MLR, SVM-linear, SVM-rbf, SVM-polynomial, BPNN) across 50 serial numbers. The main plot shows R² values ranging from -170 to 10. An inset plot zooms in on the range -150 to -70, showing the initial performance of the models. MLR starts at approximately -10 and remains stable. SVM-linear starts at approximately -10 and increases to about -30. SVM-rbf starts at approximately -10 and increases to about -40. SVM-polynomial starts at approximately -10 and increases to about -60. BPNN starts at approximately -10 and increases to about -80.](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 10: A line graph showing the Coefficient of determination (R²) for incremental order of different models (MLR, SVM-linear, SVM-rbf, SVM-polynomial, BPNN) across 50 serial numbers. The main plot shows R² values ranging from -170 to 10. An inset plot zooms in on the range -150 to -70, showing the initial performance of the models. MLR starts at approximately -10 and remains stable. SVM-linear starts at approximately -10 and increases to about -30. SVM-rbf starts at approximately -10 and increases to about -40. SVM-polynomial starts at approximately -10 and increases to about -60. BPNN starts at approximately -10 and increases to about -80.

Fig. 10. The R2 for incremental order of different model.

![Figure 11(a): A line graph showing the Coefficient of determination (R²) for incremental order of different models (MLR, SVM-linear, SVM-rbf, SVM-polynomial, BPNN) for SK (Spark Knock) across 50 serial numbers. The main plot shows R² values ranging from -400 to 20. An inset plot zooms in on the range -380 to -60, showing the initial performance of the models. MLR starts at approximately -10 and remains stable. SVM-linear starts at approximately -10 and increases to about -30. SVM-rbf starts at approximately -10 and increases to about -40. SVM-polynomial starts at approximately -10 and increases to about -60. BPNN starts at approximately -10 and increases to about -80.](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 11(a): A line graph showing the Coefficient of determination (R²) for incremental order of different models (MLR, SVM-linear, SVM-rbf, SVM-polynomial, BPNN) for SK (Spark Knock) across 50 serial numbers. The main plot shows R² values ranging from -400 to 20. An inset plot zooms in on the range -380 to -60, showing the initial performance of the models. MLR starts at approximately -10 and remains stable. SVM-linear starts at approximately -10 and increases to about -30. SVM-rbf starts at approximately -10 and increases to about -40. SVM-polynomial starts at approximately -10 and increases to about -60. BPNN starts at approximately -10 and increases to about -80.

(a)

![Figure 11(b): A line graph showing the Coefficient of determination (R²) for incremental order of different models (MLR, SVM-linear, SVM-rbf, SVM-polynomial, BPNN) for WK (Wave Knock) across 50 serial numbers. The main plot shows R² values ranging from -3.0 to 0.5. An inset plot zooms in on the range -2.5 to -0.5, showing the initial performance of the models. MLR starts at approximately -10 and remains stable. SVM-linear starts at approximately -10 and increases to about -30. SVM-rbf starts at approximately -10 and increases to about -40. SVM-polynomial starts at approximately -10 and increases to about -60. BPNN starts at approximately -10 and increases to about -80.](01da0d212fb571933f10f96556157745_img.jpg)

Figure 11(b): A line graph showing the Coefficient of determination (R²) for incremental order of different models (MLR, SVM-linear, SVM-rbf, SVM-polynomial, BPNN) for WK (Wave Knock) across 50 serial numbers. The main plot shows R² values ranging from -3.0 to 0.5. An inset plot zooms in on the range -2.5 to -0.5, showing the initial performance of the models. MLR starts at approximately -10 and remains stable. SVM-linear starts at approximately -10 and increases to about -30. SVM-rbf starts at approximately -10 and increases to about -40. SVM-polynomial starts at approximately -10 and increases to about -60. BPNN starts at approximately -10 and increases to about -80.

(b)

Fig. 11. The R2 for incremental order of different models: (a) SK and (b) WK.

combustion parameters, and establishes the knock identification, prediction and classification model based on the experimental combustion parameters, including peak in-cylinder pressure and corresponding crank angle, maximum pressure rising rate, CA10, CA50 and CA90. The main conclusions are as follows:

- (1) Compared with the crank angle of peak knock pressure, according to the combination of knock intensity and crank angle of peak knock pressure, knock type can be identified well by the Gaussian Mixture Model. Based on the given experimental data, the mean value and covariance of SK are  $-3.21$  and  $54.12$  while those of WK are  $4.17$  and  $22.85$ .
- (2) This work compared the performance of Multiple Linear Regression, Support Vector Machines with different kernel functions and Backpropagation neural Networks in hydrogen-fueled knock prediction. Based on 50 dataset partitions, it was

found that the Multiple Linear Regression model has better global predictive performance than other algorithms. Besides, due to different generation mechanisms, it is necessary to establish predictive models for SK and WK separately. SK also can be accurately predicted by the Multiple Linear Regression model, but WK cannot, the prediction of which needs to explore more advanced Machine Learning algorithms or train by more parameters.

- (3) Except for knock prediction, the Support Vector Machine also can be applied to conduct knock classification. Compared with rbf and polynomial kernel function, Support Vector Machine with linear kernel function has the highest mean test accuracy, about  $88.66\%$ , and it is  $1.52\%$  and  $2.03\%$  higher than those two, respectively.

On the whole, Machine Learning methods are of great help in the

![Figure 12: A line graph showing the coefficient of determination (R²) based on the incremental order of the MLR model. The x-axis is 'Serial Number/' (0 to 50) and the y-axis is 'Coefficient of determination based on MLR/' (-2.0 to 1.0). Three series are plotted: ALL (black squares), Strong Knock (red circles), and Weak Knock (blue triangles). A table of partial regression coefficients is also included.](a71911ad87414271aeb190e0eebcb989_img.jpg)

| Parameter | All      | SK       | WK       |
|-----------|----------|----------|----------|
| MPRR      | 0.42288  | 0.61604  | 0.29315  |
| Pmax      | -0.02828 | 0.03646  | -0.04297 |
| CAPmax    | 0.11186  | 0.07972  | 0.03895  |
| CA10      | 0.07415  | -0.0334  | -0.13694 |
| CA50      | -0.5854  | -0.44437 | -0.04334 |
| CA90      | -0.04457 | 0.01497  | -0.01319 |

Figure 12: A line graph showing the coefficient of determination (R²) based on the incremental order of the MLR model. The x-axis is 'Serial Number/' (0 to 50) and the y-axis is 'Coefficient of determination based on MLR/' (-2.0 to 1.0). Three series are plotted: ALL (black squares), Strong Knock (red circles), and Weak Knock (blue triangles). A table of partial regression coefficients is also included.

Fig. 12. The R2 for incremental order of MLR model.

![Figure 14: A scatter plot comparing real SK (blue circles) and predictive SK (red stars) against the crank angle of peak knock pressure (°CA ATDC). The x-axis ranges from 0 to 35 and the y-axis from 0 to 7. A legend indicates the data series.](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 14: A scatter plot comparing real SK (blue circles) and predictive SK (red stars) against the crank angle of peak knock pressure (°CA ATDC). The x-axis ranges from 0 to 35 and the y-axis from 0 to 7. A legend indicates the data series.

Fig. 14. The real SK and predictive SK.

![Figure 13: A bar chart showing test accuracy (%) for SVM with varied kernel functions (linear, rbf, polynomial). The y-axis ranges from 0 to 100. For each kernel, the test set accuracy (blue) and train set accuracy (red) are compared. Error bars are shown for the test set.](27b22513fc27a0ff5f230b062ad3112f_img.jpg)

| Kernel function of SVM | Test set (%) | Train set (%) |
|------------------------|--------------|---------------|
| linear                 | ~88          | ~88           |
| rbf                    | ~88          | ~94           |
| polynomial             | ~87          | ~92           |

Figure 13: A bar chart showing test accuracy (%) for SVM with varied kernel functions (linear, rbf, polynomial). The y-axis ranges from 0 to 100. For each kernel, the test set accuracy (blue) and train set accuracy (red) are compared. Error bars are shown for the test set.

Fig. 13. The test accuracy of train and test sets at SVM with varied kernel functions.

research of the knock of hydrogen-fueled WRE. In future work, more methods and operating conditions will be investigated. In addition, the research method will be applied to reciprocating piston engines and other ICEs to understand its universality.

## CRediT authorship contribution statement

**Hao Meng:** Writing – original draft, Methodology, Investigation, Conceptualization. **Qiang Zhan:** Writing – original draft, Investigation. **Changwei Ji:** Project administration. **Jinxin Yang:** Investigation. **Shuofeng Wang:** Investigation.

## Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Data availability

Data will be made available on request.

## Acknowledgements

This work was supported by the National Natural Science Foundation of China (51976003).

## References

- [1] Marouani I. Contribution of renewable energy technologies in combating phenomenon of global warming and minimizing GHG emissions. *Clean Energy Science and Technology* 2024;2:164. <https://doi.org/10.18686/cest.v2i2.164>.
- [2] Wang X, Gao J, Chen H, Chen Z, Zhang P, Chen Z. Diesel/methanol dual-fuel combustion: an assessment of soot nanostructure and oxidation reactivity. *Fuel Process Technol* 2022;237. <https://doi.org/10.1016/j.fuproc.2022.107464>.
- [3] Chen Z, Wang L, Wei Z, Wang Y, Deng J. Effect of components on the emulsification characteristic of glucose solution emulsified heavy fuel oil. *Energy* 2022;244. <https://doi.org/10.1016/j.energy.2022.123147>.
- [4] Zhang Y, Xiao Y, Abuelgasim S, Liu C. A brief review of hydrogen production technologies. *Clean Energy Science and Technology* 2024;2:117. <https://doi.org/10.18686/cest.v2i1.117>.
- [5] Gao J, Zhang H, Li J, Wang Y, Tian G, Ma C, et al. Simulation on the effect of compression ratios on the performance of a hydrogen fueled opposed rotary piston engine. *Renew Energy* 2022;187:428–39. <https://doi.org/10.1016/j.renene.2022.01.091>.
- [6] Fan B, Zeng Y, Pan J, Fang J, Adeniyi H. Evaluation and analysis of injection strategy in a peripheral ported rotary engine fueled with natural gas/hydrogen blends under the action of apex seal leakage. *Fuel* 2022;310:122315. <https://doi.org/10.1016/j.fuel.2021.122315>.
- [7] Verhelst S, Wallner T. Hydrogen-fueled internal combustion engines. *Prog Energy Combust Sci* 2009;35:490–527. <https://doi.org/10.1016/j.pecs.2009.08.001>.
- [8] Huang J, Gao J, Wang Y, Yang C, Ma C, Tian G. Effect of asymmetric fuel injection on combustion characteristics and NOx emissions of a hydrogen opposed rotary piston engine. *Energy* 2023;262. <https://doi.org/10.1016/j.energy.2022.125544>.
- [9] Ma DS, Sun ZY. Progress on the studies about NOx emission in PFI-H<sub>2</sub>ICE. *Int J Hydrogen Energy* 2020;45:10580–91. <https://doi.org/10.1016/j.ijhydene.2019.11.065>.
- [10] Gao J, Wang X, Song P, Tian G, Ma C. Review of the backfire occurrences and control strategies for port hydrogen injection internal combustion engines. *Fuel* 2022;307. <https://doi.org/10.1016/j.fuel.2021.121553>.
- [11] Dhyani V, Subramanian KA. Experimental investigation on effects of knocking on backfire and its control in a hydrogen fueled spark ignition engine. *Int J Hydrogen Energy* 2018;43:7169–78. <https://doi.org/10.1016/j.ijhydene.2018.02.125>.
- [12] Li H, Karim GA. Knock in spark ignition hydrogen engines. *Int J Hydrogen Energy* 2004;29:859–65. <https://doi.org/10.1016/j.ijhydene.2003.09.013>.
- [13] Szwaja S, Naber JD. Dual nature of hydrogen combustion knock. *Int J Hydrogen Energy* 2013;38:12489–96. <https://doi.org/10.1016/j.ijhydene.2013.07.036>.
- [14] Das LM. Hydrogen-oxygen reaction mechanism and its implication to hydrogen engine combustion. *Int J Hydrogen Energy* 1996;21:703–15. [https://doi.org/10.1016/0360-3199\(95\)00138-7](https://doi.org/10.1016/0360-3199(95)00138-7).

- [15] Szwaja S. Knock and combustion rate interaction in a hydrogen fuelled combustion engine. *Journal of KONES* 2011;18:431–8.
- [16] Meng H, Ji C, Yang J, Chang K, Xin G, Wang S. A knock study of hydrogen-fueled Wankel rotary engine. *Fuel* 2022;321. <https://doi.org/10.1016/j.fuel.2022.124121>.
- [17] Salvi BL, Subramanian KA. Experimental investigation on effects of exhaust gas recirculation on flame kernel growth rate in a hydrogen fuelled spark ignition engine. *Appl Therm Eng* 2016;107:48–54. <https://doi.org/10.1016/j.applthermaleng.2016.06.125>.
- [18] Leppard WR. Individual-cylinder knock occurrence and intensity in multicylinder engines. n.d..
- [19] Jeffrey D, Naber SS. Statistical approach to characterize combustion knock in the hydrogen fuelled SI engine. *Journal of KONES Powertrain and Transport* 2007; 443–50.
- [20] Naber JD, Blough JR, Frankowski D, Goble M, Szpytman JE. Analysis of combustion knock metrics in spark-ignition engines. <https://doi.org/10.4271/2002-2-01-0400>; 2002.
- [21] Wang H, Ji C, Shi C, Ge Y, Meng H. Comparison and evaluation of advanced machine learning methods for performance and emissions prediction of a gasoline Wankel rotary engine. *Energy* 2022;248:123611. <https://doi.org/10.1016/j.energy.2022.123611>.
- [22] Zhou L, Song Y, Ji W, Wei H. Machine learning for combustion. *Energy and AI* 2022;7. <https://doi.org/10.1016/j.egyai.2021.100128>.
- [23] Issondj Banta NJ, Patrick N, Offole F, Mouangue R. Machine learning models for the prediction of turbulent combustion speed for hydrogen-natural gas spark ignition engines. *Heliyon* 2024;10:e30497. <https://doi.org/10.1016/j.heliyon.2024.e30497>.
- [24] Cui Y, Wang Q, Liu H, Zheng Z, Wang H, Yue Z, et al. Development of the ignition delay prediction model of n-butane/hydrogen mixtures based on artificial neural network. *Energy and AI* 2020;2. <https://doi.org/10.1016/j.egyai.2020.100033>.
- [25] Issondj Banta NJ, Offole F, Essola D, Tchato Yotchou VG, Ngayihi Abbe CV, Mouangue R. Simulation of performance and emissions related parameters in a thermal engine using a deep learning approach. *SN Comput Sci* 2022;3. <https://doi.org/10.1007/s42979-021-00976-z>.
- [26] Taghavifar H, Taghavifar H, Mardani A, Mohebbi A. Exhaust emissions prognostication for di diesel group-hole injectors using a supervised artificial neural network approach. *Fuel* 2014;125:81–9. <https://doi.org/10.1016/j.fuel.2014.02.016>.
- [27] Ji C, Wang H, Shi C, Wang S, Yang J. Multi-objective optimization of operating parameters for a gasoline Wankel rotary engine by hydrogen enrichment. *Energy Convers Manag* 2021;229:113732. <https://doi.org/10.1016/j.enconman.2020.113732>.
- [28] Aramburu A, Guido C, Bares P, Pla B, Napolitano P, Beatrice C. Knock detection in spark ignited heavy duty engines: an application of machine learning techniques with various knock sensor locations. *Measurement* 2024;224. <https://doi.org/10.1016/j.measurement.2023.113860>.
- [29] Pla B, De la Morena J, Bares P, Aramburu A. An unsupervised machine learning technique to identify knock from a knock signal time-frequency analysis. *Measurement* 2023;211. <https://doi.org/10.1016/j.measurement.2023.112669>.
- [30] Fan B, Zeng Y, Pan J, Fang J, Adeniyi H, Wang Y. Numerical study of injection strategy on the combustion process in a peripheral ported rotary engine fueled with natural gas/hydrogen blends under the action of apex seal leakage. *Energy* 2022; 242:122532. <https://doi.org/10.1016/j.energy.2021.122532>.
- [31] Ji C, Meng H, Wang S, Wang D, Yang J, Shi C, et al. Realizing stratified mixtures distribution in a hydrogen-enriched gasoline Wankel engine by different compound intake methods. *Energy Convers Manag* 2020;203. <https://doi.org/10.1016/j.enconman.2019.112230>.
- [32] Meng H, Ji C, Xin G, Yang J, Chang K, Wang S. Comparison of combustion, emission and abnormal combustion of hydrogen-fueled Wankel rotary engine and reciprocating piston engine. *Fuel* 2022;318. <https://doi.org/10.1016/j.fuel.2022.123675>.
- [33] Meng H, Ji C, Su T, Yang J, Chang K, Xin G, et al. Analyzing characteristics of knock in a hydrogen-fueled Wankel rotary engine. *Energy* 2022;250. <https://doi.org/10.1016/j.energy.2022.123828>.
- [34] Meng H, Ji C, Yang J, Xin G, Wang S. Statistically discussing impacts of knock type on the heat release process in hydrogen-fueled Wankel rotary engine. *Int J Hydrogen Energy* 2023;48:7927–37. <https://doi.org/10.1016/j.ijhydene.2022.11.259>.
- [35] Brunt MFJ, Pond CR, Biundo J. Gasoline engine knock analysis using cylinder pressure data. *SAE Technical Papers* 1998. <https://doi.org/10.4271/980896>.
- [36] Dong W, Sun H, Tan J, Li Z, Zhang J, Yang H. Multi-degree-of-freedom high-efficiency wind power generation system and its optimal regulation based on short-term wind forecasting. *Energy Convers Manag* 2021;249. <https://doi.org/10.1016/j.enconman.2021.114829>.
- [37] Piloto-Rodríguez R, Sánchez-Boroto Y, Lapuerta M, Goyos-Pérez L, Verhelst S. Prediction of the cetane number of biodiesel using artificial neural networks and multiple linear regression. *Energy Convers Manag* 2013;65:255–61. <https://doi.org/10.1016/j.enconman.2012.07.023>.
- [38] Jiang H, Dong Y. A nonlinear support vector machine model with hard penalty function based on glowworm swarm optimization for forecasting daily global solar radiation. *Energy Convers Manag* 2016;126:991–1002. <https://doi.org/10.1016/j.enconman.2016.08.069>.
- [39] Feng Y, qiang, Liu YZ, Wang X, He ZX, Hung TC, Wang Q, et al. Performance prediction and optimization of an organic Rankine cycle (ORC) for waste heat recovery using back propagation neural network. *Energy Convers Manag* 2020; 226. <https://doi.org/10.1016/j.enconman.2020.113552>.
- [40] Westbrook CK, Dryer FL. Prediction of laminar flame properties of methanol-air mixtures. *Combust Flame* 1980;37:171–92. [https://doi.org/10.1016/0010-2180\(80\)90084-X](https://doi.org/10.1016/0010-2180(80)90084-X).
- [41] Sun ZY, Li GX. Propagation characteristics of laminar spherical flames within homogeneous hydrogen-air mixtures. *Energy* 2016;116:116–27. <https://doi.org/10.1016/j.energy.2016.09.103>.