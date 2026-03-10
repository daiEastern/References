![Check for updates icon](30a26f2d17ca95672702bf50fb4f0242_img.jpg)

Check for updates icon

# The accuracy of the mean value engine model affected little by the accuracy of compressor mass flow rate model for a marine diesel engine

Yanyuan Tang<sup>1</sup> ![ORCID icon](c3d993ca47bfe2a953c700506ce31fa0_img.jpg) · Yu Xia<sup>2</sup> · Jundong Zhang<sup>1</sup> · Baozhu Jia<sup>3</sup> · Ruizheng Jiang<sup>1</sup>

Received: 9 January 2023 / Accepted: 25 October 2023 / Published online: 3 November 2023

© The Author(s), under exclusive licence to The Japan Society of Naval Architects and Ocean Engineers (JASNAOE) 2023

## Abstract

The digital twin concept proves to be highly advantageous for smart ships as it allows the digital model to adapt in real time with changes in the physical ship. The mean value engine model (MVEM) is investigated with three different compressor mass flow rate models: a 2D interpolation model (2D), an experience-based M-JENSEN (MJ) model, and a physics-based Kang Song (KS) model. Each model is studied on a MAN 7S80ME engine with ABB A270 turbochargers. The root-mean-square errors (RMSE) for the test data are approximately 2.5 m<sup>3</sup>/s for the 2D model, 2.8 m<sup>3</sup>/s for the KS model, and 0.56 m<sup>3</sup>/s for the MJ model. For the training data, the RMSEs are around 0.0, 3.0, and 0.69 m<sup>3</sup>/s, respectively. When coupling each model to the MVEM, it is observed that the calculated values differ only in the turbocharger speed. The RMREs under steady-state processes are 0.54% for MVEM with the 2D model, 1.63% for MVEM with the KS model, and 0.48% for MVEM with the MJ model. Under dynamic processes where the engine load is changed from 100% to 80%, the RMREs are 1.59%, 2.40%, and 1.58%, respectively. Among the studied models, the 2D model exhibits instability, the MJ model shows the highest accuracy, while the KS model performs the worst. However, all models demonstrate comparable results when used in the MVEM. Moreover, the physics-based KS model is a favorable choice for digital twin applications due to its excellent extrapolation ability and low dependence on measured data.

**Keywords** Model · MVEM · Marine · Compressor · Diesel engine · Turbocharger · Digital twin · Mean value · Jensen model · Mass flow rate

## 1 Introduction

Digitalization is the foundation for smart and intelligent ship development. Due to the huge size of vessels, the propulsion source power of ocean-going vessels is still completely dominated by marine diesel engines. The mean value diesel engine model (MVEM) is one of the most popular diesel engine models used in real-time scenarios, like turbocharger matching [1, 2], controller design [3, 4], power

plant optimization [5], engine calibration [6], and so on. The 2D interpolation model and the empirical model are two of the commonly used compressor mass flow rate models in MVEM. The 2D interpolation model is heavily dependent on the compressor map. It should have the best accuracy in impression. Actually, it has no extrapolation ability and its performance of interpolation is also not that good. The empirical model also depends much on the compressor map to determine its parameters. In addition, its accuracy relies on the optimization result and the convergence cannot be guaranteed. The physics-based model depends less on the compressor map but much on geometry data. It is complicated and not very accurate. The compressor map is the static offline data. It causes the model to deviate from the actual performance of turbocharger at the run-time. In the digital twin application, there is a requirement that the digital model should be able to follow up the variation of the physical object. In that case, the physics-based mass flow rate model shows greater potential than the 2D interpolation

✉ Yanyuan Tang  
tangpaper2022@163.com

<sup>1</sup> Marine Engineering College, Dalian Maritime University, Dalian 116000, People's Republic of China

<sup>2</sup> School of Energy and Power Engineering, Dalian University of Technology, Dalian 116000, People's Republic of China

<sup>3</sup> Maritime College, Guangdong Ocean University, Zhanjiang 524088, People's Republic of China

model and the empirical model because of its low map dependence. Therefore, it is necessary to quantify the effect of the accuracy of compressor mass flow rate model on the accuracy of the mean value model of marine diesel engine.

Compressor is widely used in gas turbine [7], diesel engine [8], gasoline engine [9], refrigerator [10], wet gas compressor [11], compressed air energy storage [12], fuel cell [13], and so on. In general, compressor models are different in different media and different plants. These compressor models used in diesel engine generally can be classified into interpolation models including look-up model, empirical models including the conventional empirical models [14, 15], ANN models [16], SVM models [17], and physics-based models, including mean-line model [18], zero-dimensional model [19], 1D model [20], and CFD model [21]. In applications where real-time performance is required, the interpolation models, the empirical models, and some simple physics-based models can be used.

The pressure ratio and revolution speed are two essential parameters to get the mass flow rate from the compressor map. The look-up method is often provided in commercial software, like the AVL BOOST, and GT-Power. There is little research on the look-up method itself, mostly on the application of the method. Serrano et al. [22] analyzed the unsteady energy fluxes in a turbocharger using a holistic model extrapolating standard look-up tables in a full engine operating map. Errors in compressor map data can result in inaccurate engine performance prediction. McMullen et al. [23] proposed a method for conditioning compressor map data by detecting and replacing suspect data points, and interpolating and extrapolating the map data. However, the manufacturer only provides a narrow operating region of the compressor map. This limits the use of the look-up table. Similarly, the 2D interpolation model also encounters the same problem as the look-up table.

To solve the problems encountered in the interpolation model, various empirical models were developed. Jensen et al. [24] proposed a mean value model to determine the normalized mass flow rate by the dimensionless head parameter and the Mach number based on a 1.6L turbocharged indirect injection diesel engine. Karlsen [25] developed an exponential function-based compressor mass flow rate model in which the compressor characteristics are derived from dimensionless pressure head  $\Psi$ , the normalized compressor flow rate  $\Phi$ , and the inlet Mach number. Tsoutsanis [26] developed a compressor modeling method based on elliptical curves and declared that this model improved the accuracy and fidelity of gas turbine engine models. Similarly, Leufven [27] also used an ellipse model to describe the centrifugal compressors that operate in both normal region and restriction region from stagnation speed to maximum speed. Shuang [28] used the Bezier curves to fitting the compressor map. The control points of the Bezier curves

were optimized by the genetic algorithm, so that the model accuracy can be improved at the off-design speed. Yazar [29] investigates various regression models to predict the compressor and turbine map parameters for a gas turbine engine. The empirical model can extend the operating range of compressor map, but it still depends much on the map. It has to use the measured data from the compressor map to determine the model parameters. Meanwhile, convergence cannot be guaranteed.

To reduce the dependency on the compressor map, some physics-based real-time models were proposed, like the 0D model [19], the mean-line model [30], the Moore–Greitzer model [31], the first principle model [32, 33], and the two-zone model [34]. Song [19] proposed a physics-based zero-dimensional model for the mass flow rate of turbocharger compressor. This model can calculate the difference between turbocharger compressors with uniform inlet condition and distorted inlet condition. Powers [32, 33] develop a model for centrifugal compressors based on the first principle. This model can calculate the compressor characteristics, including surge and the reversed flow. Zhang [35] extended the Moore–Greitzer model and established the real-time model of the engine with surge process. The coupling relationship among the rotor speed, the mass flow rate, and the pressure ratio was considered between the component level model and the extended MG model.

From the above review, it can be known that there are many kinds of compressor models. Researchers had investigated the performance of these compressor models. Gooding [7] investigated the impact of various modeling decisions on flow field predictions in a centrifugal compressor for an aero-engine. Gonzalez and Hall [36] reduced the compressor and turbine maps from a cloud of points into a set of equations and evaluated the performance of the equation-based model versus the map-based model. They claimed that the execution time of the equation-based model was about 400 times lower than that of the map-based method. It makes this model ideal for model-based control strategies. Serrano et al. [37] present a comprehensive study that quantifies the errors of using just look-up tables compared with a model that accounts for friction losses, heat transfer, and gas dynamics in a turbocharger and in a conjugated way. The study work is based on a Euro 5 engine. Shen et al. [38] compared some empirical compressor models used in the marine diesel engine. Kaechele et al. [39] extended the limited operating range of compressor to evaluate the potential of different turbocharger models being included in 3D-CFD engine models. Yang et al. [40] reviewed several empirical compressor models used in the jet engine. Fang et al. [41] carried out a comprehensive review of centrifugal compressor models and found that the models for centrifugal compressors of vehicle engines and turbochargers are not satisfactory for refrigerating centrifugal compressors directly.

In this paper, to investigate the effect of the accuracy of mass flow rate on the performance of mean value diesel engine model, a 2D interpolation model, Jensen's empirical model, and KangSong's physics-based model are selected. First, the modeling process and its dependency on the map are introduced. Then, the methods for parameters determining and the performance of models are presented. Finally, the influences of these three models on the mean value diesel engine model are studied and analyzed.

## 2 The mass flow rate models

### 2.1 The interpolation method

The interpolation method is a general numerical method for estimating the value at an unknown point based on the tabulated points. The commonly used interpolation methods include one-dimensional interpolation and two-dimensional interpolation. As the number of dimensions increases, the number of grid points grows explosively. This makes it difficult to build the look-up table. The process for the most widely used bilinear interpolation in the two-dimensional interpolation shows the following.

First, prepare the  $x$  data in a vector of  $m$  size, the  $y$  data in a vector of  $n$  size, and the  $z$  data in a matrix of  $m \times n$  size.

Second, find the four tabulated points  $(x_1, y_1)$ ,  $(x_2, y_1)$ ,  $(x_1, y_2)$ , and  $(x_2, y_2)$  that surround the desired interpolated point  $(x, y)$ .

Third, calculate the estimated values of points  $(x, y_1)$  and  $(x, y_2)$  in  $x$ -direction and the final desired point  $(x, y)$  in  $y$ -direction using linear Lagrange interpolation three times, as shown in Eqs. 1–3

$$f(x, y_1) = \frac{x - x_2}{x_1 - x_2} f(x_1, y_1) + \frac{x - x_1}{x_2 - x_1} f(x_2, y_1) \quad (1)$$

$$f(x, y_2) = \frac{x - x_2}{x_1 - x_2} f(x_1, y_2) + \frac{x - x_1}{x_2 - x_1} f(x_2, y_2) \quad (2)$$

$$f(x, y) = \frac{y - y_2}{y_1 - y_2} f(x, y_1) + \frac{y - y_1}{y_2 - y_1} f(x, y_2). \quad (3)$$

It can be known that the two-dimensional interpolation method heavily depends on the measured data. Also, it is not easy in coding and data preparing for the method especially when the measured data need to be changed.

### 2.2 Kang Song's model

The physics-based zero-dimensional model offers greater potential for control-oriented digital twin modeling than empirical model and complex CFD model. Song et al.'s [19]

excellent work in modeling the mass flow rate of a turbo-charger compressor proves the possibility to model the mass flow behavior of compressor in a physics-based control-oriented way.

In Kang Song's model, the mass flow behavior is modeled as an adiabatic convergent-divergent (CD) nozzle. According to the conservation of energy principle, the total inlet energy is equal to the total outlet energy if the control volume is in a steady state. Thus, Eq. 4 can be derived

$$H_1^s + \dot{W}_c = H_2 + \dot{m}_c \frac{C_2^2}{2}. \quad (4)$$

In terms of the velocity triangles of centrifugal compressor, the power of the mass flow acquired from the impeller can be derived in the form of Eq. 5 with the zero inlet swirl assumption

$$\dot{W}_c = \dot{m}_c u_{\text{flow}} U_{\text{ex},c}^2. \quad (5)$$

As the Mach number must be limited to 1 at the exit due to the design of diffuser volute, the critical pressure for the compressor mass flow is shown in Eq. 6

$$p_2^* = p_1^s \left[ \frac{2 \left( 1 + \frac{u_{\text{flow}} U_{\text{ex},c}^2}{c_p T_1^s} \right)}{k+1} \right]^{\frac{k}{k-1}}. \quad (6)$$

Under sonic flow, the Mach number of mass flow equals 1, the pressure at that place keeps constant, equals  $p_2^*$ . According to the definition of mass flow rate, the choked mass flow rate model is derived in Eq. 7 with the ideal-gas equation of state and mathematic manipulations

$$\dot{m}_c = \frac{\hat{C}_d \cdot A \cdot p_1^s}{\sqrt{R \cdot T_1^s}} \sqrt{k \left[ \frac{2 \left( 1 + \frac{u_{\text{flow}} U_{\text{ex},c}^2}{c_p T_1^s} \right)}{k+1} \right]^{\frac{k+1}{k-1}}}. \quad (7)$$

Under subsonic flow, the mass flow rate model is shown in Eq. 8

$$\dot{m}_c = \frac{\hat{C}_d \cdot A \cdot p_1^s}{\sqrt{R \cdot T_1^s}} \left( \frac{p_2}{p_1^s} \right)^{\frac{1}{k}} \sqrt{\frac{2k}{k-1} \left[ 1 - \left( \frac{p_2}{p_1^s} \right)^{\frac{k-1}{k}} + \frac{u_{\text{flow}} U_{\text{ex},c}^2}{c_p T_1^s} \right]}. \quad (8)$$

In the mass flow rate model, Eqs. 7 and 8, the  $u_{\text{flow}}$  and the  $\hat{C}_d$  are parameters that need to be identified. The  $u_{\text{flow}}$  is the work coefficient for the compressor impeller and can be derived as the form of Eq. 9 based on the velocity triangle of compressor

$$u_{\text{flow}} = \sigma \mu_0. \quad (9)$$

The  $\mu_0$  is related to the geometry back sweep angle, as shown in Eq. 10. The  $U_{ex,c}$  is the blade tip speed and can be calculated by geometry data and revolution speed of compressor

$$\mu_0 = \frac{C_{\theta,ex,c,0}}{U_{ex,c}}. \quad (10)$$

The  $\sigma$  is the slip factor and is modeled by an empirical model, as shown in Eq. 11

$$\sigma = a_{\sigma,1} + \frac{a_{\sigma,2}}{U_{ex,c}}. \quad (11)$$

The  $\hat{C}_d$  is the equivalent coefficient for nozzle discharge used for adjusting the discharge area of mass flow. It is proposed as the model shown in Eq. 12

$$\hat{C}_d = C_{d,max} - C_{d,cor} (U_{ex,c} - U_{ex,c,opt})^2. \quad (12)$$

Therefore, for Kang Song's mass flow rate model, Eqs. 7 and 8, five parameters need to be identified from measured data, as shown in Table 1.

### 2.3 Jensen's model

Jensen's model is an empirical model and is one of the most popular models in compressor mass flow rate modeling. It is recommended by Lino Guzzella in his book [42] and gains high acceptance among researchers and engineers [38, 43, 44]. Jensen's model is presented in Eq. 13. The dimensionless pressure head  $\Psi$  is the function of the normalized compressor flow rate  $\Phi$  and the inlet Mach number  $M$

$$\Psi = \frac{k_1 + k_2M + k_3\Phi + k_4M\Phi}{k_5 + k_6M - \Phi}. \quad (13)$$

The dimensionless pressure head  $\Psi$  is calculated from the pressure ratio, as shown in Eq. 14. The normalized compressor flow rate  $\Phi$  is calculated from the volume flow rate, as shown in Eq. 15. The Mach number  $M$  is determined by Eq. 16

$$\Psi = \frac{c_p T_a \left[ \left( \frac{p_2}{p_a} \right)^{\frac{k_a-1}{k_a}} - 1 \right]}{0.5 U_c^2} \quad (14)$$

$$\Phi = \frac{Q_v}{\frac{\pi}{4} D^2 U_c} \quad (15)$$

$$M = \frac{U_c}{\sqrt{k_a R_a T_a}}. \quad (16)$$

The  $U_c$  is the blade tip speed and is calculated by Eq. 17. The same as the  $U_{ex,c}$  in Kang Song's model

$$U_c = \frac{\pi}{60} d_c N_{tc}. \quad (17)$$

The same as the common shortage of empirical models, Jensen's model parameters that need to be identified have no physical meanings. All the parameters are completely determined by the measured data, as shown in Table 2.

## 3 Performance of the mass flow models

### 3.1 The turbocharger specifications

ABB and MAN Diesel&Turbo are two famous companies in marine turbochargers and possess a high market share. Our engine model used in this paper is based on MAN 7S80ME, in which the ABB A270 was installed. To reduce the introduction of uncertainties, the ABB A270 is selected for mass

**Table 1** Model parameters that need to be identified from measured data

| No. | Parameters     | Roles in model                                                           |
|-----|----------------|--------------------------------------------------------------------------|
| 1   | $a_{\sigma,1}$ | Determining the working coefficient $u_{flow}$                           |
| 2   | $a_{\sigma,2}$ | Determining the working coefficient $u_{flow}$                           |
| 3   | $C_{d,max}$    | Determining the equivalent coefficients for nozzle discharge $\hat{C}_d$ |
| 4   | $C_{d,cor}$    | Determining the equivalent coefficients for nozzle discharge $\hat{C}_d$ |
| 5   | $U_{ex,c,opt}$ | Determining the equivalent coefficients for nozzle discharge $\hat{C}_d$ |

**Table 2** Jensen's model parameters that need to be identified from the measured data

| No. | Parameters | Roles in model                               |
|-----|------------|----------------------------------------------|
| 1   | $k_1$      | A general factor having no physical meanings |
| 2   | $k_2$      | A general factor having no physical meanings |
| 3   | $k_3$      | A general factor having no physical meanings |
| 4   | $k_4$      | A general factor having no physical meanings |
| 5   | $k_5$      | A general factor having no physical meanings |
| 6   | $k_6$      | A general factor having no physical meanings |

**Table 3** The turbocharger specifications

| Type                            | ABB A270           |
|---------------------------------|--------------------|
| Turbine type                    | Axial flow turbine |
| Compressor type                 | Centrifugal flow   |
| Rate volume [m <sup>3</sup> /s] | 20.5               |
| Rate speed [rpm]                | 16,000             |
| Pressure rate [–]               | 3.94               |
| Max. permissible temp. [°C]     | 520                |
| Weight [kg]                     | 3800               |

![Figure 1: A compressor map showing the volume flow rate (Qv) in m³/s on the x-axis (0 to 28) versus the pressure ratio (II) in H on the y-axis (1.0 to 5.0). The map displays several isentropic efficiency curves for different pressure ratios: 140, 160, 180, 200, 220, 240, 260, and 280. Each curve consists of measured data points represented by open circles. The curves generally show a decrease in pressure ratio as the volume flow rate increases, with a characteristic bend at higher flow rates.](b15e3860e0c96ed16ce77f032da6f107_img.jpg)

Figure 1: A compressor map showing the volume flow rate (Qv) in m³/s on the x-axis (0 to 28) versus the pressure ratio (II) in H on the y-axis (1.0 to 5.0). The map displays several isentropic efficiency curves for different pressure ratios: 140, 160, 180, 200, 220, 240, 260, and 280. Each curve consists of measured data points represented by open circles. The curves generally show a decrease in pressure ratio as the volume flow rate increases, with a characteristic bend at higher flow rates.

**Fig. 1** The volume flow rate of ABB A270

flow rate model validation, and the engine model of MAN 7S80ME will be used later in model coupling and performance analysis. The specifications of ABB A270 are shown in Table 3.

The compressor map of the volume flow rate of ABB A270 is presented in Fig. 1. In terms of the measured data, it is found that the remaining kinetic energy of the air at the diffuser outlet is less than 10% of its total energy, and more than 90% is converted to internal energy. One part of the data will be used for model calibration and the other will be used for model validation. This map only shows the working region of the compressor. The surge region and chock region are not measured for the physical engine. However, these two regions are also required for the mathematic model to ensure its running, to investigate dynamic performance, to study failure mode and effect analysis, and so on.

### 3.2 Performance of 2D interpolation model

The 2D interpolation model is used directly without any modifications. These measured data are divided into two parts. One part of the measured data is used for the modeling of the interpolation model. The other part is used to check the interpolation performance of the 2D model. Figure 2a shows the comparison of the measured volume flow rate and the calculated volume flow rate from the 2D interpolation model. Figure 2b shows the comparison of the test data and the calculated data from the 2D interpolation model to check its performance.

It can be known from Fig. 2a that the calculated volume flow rates by interpolation are the same as the measured value for the points with the same pressure ratio and

![Figure 2: Two plots comparing the performance of a 2D interpolation model. Plot (a) shows the performance on data used in the model, with measured data (open circles) and calculated data (filled circles) plotted against volume flow rate (Qv) and pressure ratio (II). The RMSE is 0.0000. Plot (b) shows the performance on test data, with test data (open triangles) and calculated data (filled triangles) plotted against volume flow rate (Qv) and pressure ratio (II). The RMSE is 2.5005. Both plots show isentropic efficiency curves for pressure ratios 140, 160, 180, 200, 220, 240, 260, and 280.](c82c7d8107cba121734a9cfba891216d_img.jpg)

Figure 2: Two plots comparing the performance of a 2D interpolation model. Plot (a) shows the performance on data used in the model, with measured data (open circles) and calculated data (filled circles) plotted against volume flow rate (Qv) and pressure ratio (II). The RMSE is 0.0000. Plot (b) shows the performance on test data, with test data (open triangles) and calculated data (filled triangles) plotted against volume flow rate (Qv) and pressure ratio (II). The RMSE is 2.5005. Both plots show isentropic efficiency curves for pressure ratios 140, 160, 180, 200, 220, 240, 260, and 280.

**Fig. 2** The performance of 2D interpolation model on data used in the model (a) and on test data (b)

revolution speed as the measured data. The 2D interpolation method shows very good performance. However, for the test points, the performance of 2D interpolation model reduces, as shown in Fig. 2b. The RMSE increases from 0 to 2.5. This performance deterioration is caused by the 2D interpolation method itself. When the pressure ratio of the interpolated point is bigger than the maximum pressure ratio of the nearest grid point, the volume flow rate will be zero. However, the volume flow rate should not be the linear relationship, cubic relationship, or spline relationship with the pressure ratio in practice. This fact leads to the deterioration of performance as shown in Fig. 2b. This error will be bigger if the grid of the modeling points is bigger.

### 3.3 Performance of Kang Song's model

As aforementioned, both Kang Song's (KS) model and Jensen's model have parameters to be identified from measured data. The parameters in Jensen's model can be determined directly from the measured data. While Kang Song's model is more complex. There are five parameters to be determined. Parameters  $a_{\sigma,1}$  and  $a_{\sigma,2}$  are used only for estimating the work. While the other parameters  $C_{d,max}$ ,  $C_{d,cor}$ , and  $U_{ex,c,opt}$ , are used only for estimating the discharge area. In this case, the specific work and the discharge area will be estimated directly in this paper rather than identifying these 5 parameters alone as shown in his paper.

Substituting Eqs. 10 and 11 into Eq. 9 and product by blade tip speed, the specific work can be obtained with some simple mathematic manipulations, as shown in Eq. 18

$$u_{flow} U_{ex,c}^2 = \frac{C_{\theta,ex,c,0}}{U_{ex,c}} \left( a_{\sigma,1} + \frac{a_{\sigma,2}}{U_{ex,c}} \right) U_{ex,c}^2 = C_{\theta,ex,c,0} (a_{\sigma,1} U_{ex,c} + a_{\sigma,2}). \quad (18)$$

The  $C_{\theta,ex,c,0}$  is a geometry-related constant. The  $a_{\sigma,1}$  and the  $a_{\sigma,2}$  are parameters to be identified. This reveals that the specific work is a linear function of blade tip speed, as described by Eq. 18. Therefore, the specific work can be written in the following linear form for simplicity, as shown in Eq. 19:

$$u_{flow} U_{ex,c}^2 = a U_{ex,c} + b. \quad (19)$$

For ABB, the turbocharger speed is given in its map instead of blade tip speed and there is a linear relationship between blade tip speed and turbocharger speed. Therefore, the specific work in Eq. 19 is written as a function of turbocharger speed, as shown in Eq. 20

$$u_{flow} U_{ex,c}^2 = a N_{tc} + b. \quad (20)$$

In Eqs. 19 and 20, there are only two parameters,  $a$  and  $b$ , to be determined. The actual work that the flowing air

obtained from the impeller can be calculated directly from the measured data using Eq. 21. Then, parameters  $a$  and  $b$  can be determined

$$u_{flow} U_{ex,c}^2 = h_2 + \frac{1}{2} c_2^2 - h_1^s = h_2^s - h_1^s. \quad (21)$$

Figure 3 shows the actual work of the flowing air obtained from the impeller of compressor according to the measured data from ABB A270. Obviously, the actual work obtained is not only a function of blade tip speed but also the ratio of pressure. While, in Kang Song's model, the influence of the pressure ratio is neglected, as Eq. 18 shows.

The stagnation entropy has to be used to determine the specific work as shown in Eq. 21. In case of insufficient power reserve making calculation failure, the maximum stagnation entropy among the iso-speed points is selected to determine the parameters in Eq. 20. From the observation of the compressor mass flow rate curves, the points at the surge line can be used as the maximum stagnation entropy as an approximation. The points of the stagnation entropy at the surge line versus turbocharger speed are presented in Fig. 4a.

These points show a quadratic curve-like line instead of a strictly linear line. In that case, a quadratic model is also checked, as shown in Eq. 22, as a comparison of the linear model. The fitness curve is presented in Fig. 4b

$$u_{flow} U_{ex,c}^2 = a N_{tc}^2 + b N_{tc} + c. \quad (22)$$

To determine the parameters in the linear model and quadratic model, the fitting method is used. The algorithm

![Figure 3: A scatter plot showing the actual work done by the compressor. The y-axis is 'Work [kJ/kg]' ranging from 20 to 200. The x-axis is 'Turbocharger speed [r/s]' ranging from 120 to 300. Data points are represented by circles with numbers indicating pressure ratios (1.4, 1.5, 1.6, 1.7, 1.8, 1.9, 2.1, 2.4, 2.5, 2.7, 2.9, 3.2, 3.4, 3.6, 4.0, 4.7). The points form a curve that increases with turbocharger speed and then levels off or slightly decreases at higher speeds. A legend indicates 'Work done by compressor'.](cca618c1ee620e865e566356b9fc9fb8_img.jpg)

Figure 3: A scatter plot showing the actual work done by the compressor. The y-axis is 'Work [kJ/kg]' ranging from 20 to 200. The x-axis is 'Turbocharger speed [r/s]' ranging from 120 to 300. Data points are represented by circles with numbers indicating pressure ratios (1.4, 1.5, 1.6, 1.7, 1.8, 1.9, 2.1, 2.4, 2.5, 2.7, 2.9, 3.2, 3.4, 3.6, 4.0, 4.7). The points form a curve that increases with turbocharger speed and then levels off or slightly decreases at higher speeds. A legend indicates 'Work done by compressor'.

**Fig. 3** The actual work done by the compressor is related to speed and pressure ratio

![Figure 4: Two plots comparing measured data with linear and quadratic models for compressor work. Plot (a) shows a linear fit with RMSE = 3.9678 and R-square = 0.9919. Plot (b) shows a quadratic fit with RMSE = 0.2339 and R-square = 1.0000. Both plots show Work [kJ/kg] on the y-axis (20 to 200) and Turbocharger speed [r/s] on the x-axis (120 to 300).](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 4: Two plots comparing measured data with linear and quadratic models for compressor work. Plot (a) shows a linear fit with RMSE = 3.9678 and R-square = 0.9919. Plot (b) shows a quadratic fit with RMSE = 0.2339 and R-square = 1.0000. Both plots show Work [kJ/kg] on the y-axis (20 to 200) and Turbocharger speed [r/s] on the x-axis (120 to 300).

**Fig. 4** The maximum work done by the compressor is more like a quadratic line

**Table 4** The fitting parameters of the specific work in Kang Song's model

| Model                 | Linear model | Quadratic model |
|-----------------------|--------------|-----------------|
| <i>a</i>              | 0.9557       | 0.0022          |
| <i>b</i>              | -96.0403     | 0.0482          |
| <i>c</i>              | —            | -5.2856         |
| <i>R</i> <sup>2</sup> | 0.9919       | 1.0000          |
| RMSE                  | 3.9678       | 0.2339          |
| Iterations            | 6            | 3               |

of the fitness is trust-region-reflective and the iterations start from [0, 0] or [0, 0, 0], after less than six times of iterations, it converged. The model performance is presented in Fig. 4 and the values of parameters are presented in Table 4. Apparently, as shown in Table 4, the quadratic model shows better performance. While linear model fitness is not bad from the view of the *R*<sup>2</sup>. This quadratic model will then be used for mass flow rate calculation.

The last parameter that needs to be determined is the  $\hat{C}_d$ , as shown in Eq. (12). As this is a parameter to adjust the flow area and  $C_{d,\max}$ ,  $C_{d,\text{cor}}$ ,  $U_{\text{ex},c,\text{opt}}$  are not easy to be determined since lacking of design data, a flow factor  $\mu$  is used instead of  $\hat{C}_d$ , as shown in Eq. (23). Try-and-error method is used to determine the flow factor for simplicity

$$\hat{C}_d A = \mu A. \quad (23)$$

After the determination of the specific work and the flow factor, the performance of Kang Song's model is presented in Fig. 5. Figure 5a shows the performance of model on data

used for model calibration. Figure 5b shows the performance of model on test data. The RMSE is about 3 m<sup>3</sup>/s in both cases. It can be known from Fig. 5 that KS model offers almost the same accuracy for data used for model calibration or used for model test. This fact shows that the KS model is more stable than the 2D interpolation model.

### 3.4 Performance of Jensen's model

Jensen's model is a famous empirical model in mass flow rate calculation, as shown in Eq. 13. Six parameters having no physical meaning need to be identified so that the fitness method is used directly. However, optimizing Eq. 13 is less accurate than optimizing Eq. 24

$$\Phi = \frac{(k_5 + k_6 M) \Psi - (k_1 + k_2 M)}{k_3 + k_4 M + \Psi}. \quad (24)$$

Equation 24 is hard to converge making it almost cannot be used. Thus, the improved JENSEN model, called M-JENSEN, is used in this study as shown in Eq. 25. The details about M-JENSEN can be found in another paper of ours

$$\Phi = \frac{(k_5 + k_6 \Psi) M - (k_1 + k_2 \Psi)}{k_3 + k_4 \Psi + M}. \quad (25)$$

As the parameter identification uses the normalized data, the measured data have to be transformed to and from the normalized data. The calculation process of M-JENSEN model is shown in Fig. 6. First, measured values of pressure ratio  $\Pi$ , volume flow rate  $Q_v$  and turbocharger speed

![Figure 5: Performance of Kang Song's model. (a) Calibration data: Measured data (open circles) and Calculated data (filled circles) plotted against volume flow rate Qv [m³/s] (0 to 30) and pressure ratio Π [-] (1.0 to 5.0). Curves are labeled 140, 160, 180, 200, 220, 240, 260, 280. RMSE = 3.0377 for KS model. (b) Test data: Test data (open triangles) and Calculated data (filled triangles) plotted against Qv [m³/s] (0 to 30) and Π [-] (1.0 to 5.0). Curves are labeled 150, 170, 190, 210, 230, 250, 270. RMSE = 2.8234 for KS model.](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 5: Performance of Kang Song's model. (a) Calibration data: Measured data (open circles) and Calculated data (filled circles) plotted against volume flow rate Qv [m³/s] (0 to 30) and pressure ratio Π [-] (1.0 to 5.0). Curves are labeled 140, 160, 180, 200, 220, 240, 260, 280. RMSE = 3.0377 for KS model. (b) Test data: Test data (open triangles) and Calculated data (filled triangles) plotted against Qv [m³/s] (0 to 30) and Π [-] (1.0 to 5.0). Curves are labeled 150, 170, 190, 210, 230, 250, 270. RMSE = 2.8234 for KS model.

**Fig. 5** The performance of Kang Song's model on data used in model calibration (a) and on test data (b)

![Figure 6: Calculation process of the M-JENSEN model. The diagram is divided into 'Model fitting' and 'Model usage' sections. Model fitting: Look up Π, Qv, Uc from compressor map -> Derive Ψ, Φ, M from Π, Qv, and Uc -> Fit Φ=f(M, Ψ) by optimization method -> Parameters k1~k6. Model usage: Arbitrary Π, Uc -> Derive Ψ, M from Π, and Uc -> M-JENSEN model Φ=f(M, Ψ) -> Obtain Φ -> Derive Qv from Φ. A feedback arrow points from the 'Parameters k1~k6' box to the 'M-JENSEN model' box.](35a7554182eb055209552843f341a1ae_img.jpg)

Figure 6: Calculation process of the M-JENSEN model. The diagram is divided into 'Model fitting' and 'Model usage' sections. Model fitting: Look up Π, Qv, Uc from compressor map -> Derive Ψ, Φ, M from Π, Qv, and Uc -> Fit Φ=f(M, Ψ) by optimization method -> Parameters k1~k6. Model usage: Arbitrary Π, Uc -> Derive Ψ, M from Π, and Uc -> M-JENSEN model Φ=f(M, Ψ) -> Obtain Φ -> Derive Qv from Φ. A feedback arrow points from the 'Parameters k1~k6' box to the 'M-JENSEN model' box.

**Fig. 6** Calculation process of the M-JENSEN model

$N_{tc}$  or blade tip speed  $U_c$  are looked up from compressor map. Then, the dimensionless process of the measured data is carried out to determine the dimensionless pressure head  $\Psi$ , the normalized volume flow rate  $\Phi$ , and the inlet Mach number  $M$ . After that, the M-JENSEN model is to be fitted by an optimal algorithm and the six parameters  $k_1$  to  $k_6$  are determined. Thus, the M-JENSEN model is ready for use. To use the M-JENSEN model, the arbitrary pressure ratio and arbitrary blade tip speed have to be known first. Then, the corresponding dimensionless pressure head and the inlet Mach number are to be calculated. Thus, the normalized

**Table 5** The fitting parameters and values of M-JENSEN model

| Parameter | Value    |
|-----------|----------|
| $k_1$     | -3.8739  |
| $k_2$     | 3.2300   |
| $k_3$     | 38.0897  |
| $k_4$     | -30.3947 |
| $k_5$     | 1.8884   |
| $k_6$     | -1.3594  |

volume flow rate can be calculated by M-JENSEN model. Finally, the desired volume flow rate  $Q_v$ , is derived from the normalized volume flow rate  $\Phi$ .

To check the performance of M-JENSEN model and compare its performance with the KS model and 2D interpolation model, the same data are used to calibrate the M-JENSEN model and to test the prediction capability. The initial values of the six parameters are assigned zeros and the optimal algorithm is trust-region-reflective. The final fitting values of the six parameters of M-JENSEN model are presented in Table 5.

The performance curves of M-JENSEN model on data used for model calibration and on test data are presented in Fig. 7. It can be easily known that the M-JENSEN model is very good, and the RMSE is less than 1 both for data used in model calibration and for test data. For the data used in model calibration, the performance of M-JENSEN model is a little worse than the 2D model but better than the KS model. For the test data, its prediction performance is better than both the 2D model and the KS model.

![Figure 7: Performance of the M-JENSEN model. (a) Calibration data: Measured data (open circles) and Calculated data (filled circles) for engine loads of 140, 160, 180, 200, 220, 240, 260, and 280 kW. (b) Test data: Test data (open triangles) and Calculated data (filled triangles) for engine loads of 150, 170, 190, 210, 230, 250, and 270 kW. Both plots show engine speed Π [-] on the y-axis (1.0 to 5.0) versus mass flow rate Qv [m³/s] on the x-axis (0 to 28). The RMSE for calibration is 0.6881 and for test data is 0.5644. The model is labeled 'M-JENSEN model' in both plots.](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 7: Performance of the M-JENSEN model. (a) Calibration data: Measured data (open circles) and Calculated data (filled circles) for engine loads of 140, 160, 180, 200, 220, 240, 260, and 280 kW. (b) Test data: Test data (open triangles) and Calculated data (filled triangles) for engine loads of 150, 170, 190, 210, 230, 250, and 270 kW. Both plots show engine speed Π [-] on the y-axis (1.0 to 5.0) versus mass flow rate Qv [m³/s] on the x-axis (0 to 28). The RMSE for calibration is 0.6881 and for test data is 0.5644. The model is labeled 'M-JENSEN model' in both plots.

**Fig. 7** The performance of M-JENSEN model on data used for model calibration (a) and on test data (b)

**Table 6** Specifications of diesel engine (MCR)

| Parameter                      | Value         |
|--------------------------------|---------------|
| Cylinder number [-]            | 7             |
| Cylinder diameter [mm]         | 800           |
| Stroke [mm]                    | 3450          |
| Power [kW]                     | 25,190        |
| Speed [r·min <sup>-1</sup> ]   | 72.0          |
| Explosion pressure [MPa]       | 17.1          |
| Mean effective pressure [MPa]  | 1.73          |
| SFOC [g·(kW·h) <sup>-1</sup> ] | 165.9         |
| Fire order [-]                 | 1-7-2-5-4-3-6 |

## 4 Influence of the mass flow rate model on the diesel engine model

### 4.1 Engine specifications

To prove the accuracy of compressor mass flow rate model having less effect on the accuracy of the marine diesel engine mean value model, the mean value model of MAN 7S80ME is studied. MAN 7S80ME is an electronically controlled two-stroke marine diesel engine. The specifications at MCR are presented in Table 6.

### 4.2 Mean value engine model

The mean value engine model and 0D engine model are two of the most widely used models for scenarios in that

real-time running is required. The mean value engine model is less complex than the 0D model. It averages the cylinder cycles and omits the details of in-cylinder processes. To check the mass flow rate model of compressor, the mean value model is selected. The calculation skeleton and parameters of the mean value model are presented in Fig. 8. The models will be briefly introduced in the next, the details can be found in our previous papers.

#### (1) Compressor

In the compressor model, there are three parameters that need to be calculated. They are the output temperature, the output mass flow rate, the power consumed. In MVEM, the compression process is modeled as an isentropic process. Considering the actual losses, the theory process is modified with factors. Then, the output temperature is calculated according to Eq. 26. The power consumed is calculated according to Eq. 27

$$T_{2\_CP} = T_{1\_CP} + T_{1\_CP} \left[ \left( \left( \frac{p_{2\_CP}}{p_{1\_CP}} \right)^{\frac{k-1}{k}} - 1 \right) \frac{1}{\eta_c} \right] \quad (26)$$

$$Pw_{\_CP} = dm_{2\_CP} * C_p * (T_{2\_CP} - T_{1\_CP}). \quad (27)$$

In Eqs. 26 and 27, the  $T_{1\_CP}$  and  $p_{1\_CP}$  are the input temperature and input pressure. The  $T_{2\_CP}$  and  $p_{2\_CP}$  are the output temperature and output pressure.  $k$  is the ratio of specific heat,  $\eta_c$  is the isentropic efficiency, and  $C_p$  is the specific heat capacity at constant pressure.  $dm_{2\_CP}$  is the mass flow rate, which is calculated according to the models discussed in this paper.

![Figure 8: The calculation skeleton and parameters of MVEM. The diagram shows a thermodynamic cycle with components: Compressor, Shaft, Turbine, Air Cooler, Intake Manifold, Cylinder, and Exhaust Manifold. Arrows indicate the flow of mass and energy between these components. Parameters are color-coded: Blue for input, Orange for output, Black for steady-state processes, and Green for dynamic processes. A legend box in the center explains these color codes.](cfda9df1319e04207eb28bcefd1dab7b_img.jpg)

Blue = Input of model  
Orange = Output of model  
Black = Steady-state process  
Green = Dynamic process

Figure 8: The calculation skeleton and parameters of MVEM. The diagram shows a thermodynamic cycle with components: Compressor, Shaft, Turbine, Air Cooler, Intake Manifold, Cylinder, and Exhaust Manifold. Arrows indicate the flow of mass and energy between these components. Parameters are color-coded: Blue for input, Orange for output, Black for steady-state processes, and Green for dynamic processes. A legend box in the center explains these color codes.

**Fig. 8** The calculation skeleton and parameters of MVEM

#### (2) Turbine

The exhaust gas passing through the turbine is modeled as the gas passing through an adiabatic nozzle. The output temperature and the generated power are modeled the same as the compressor, as shown in Eqs. 28 and 29. The mass flow rate is modeled the same as the air passing through a throat

$$T2_Tb = T1_Tb + T1_Tb \left[ \left( \left( \frac{p2_Tb}{p1_Tb} \right)^{\frac{k-1}{k}} - 1 \right) \eta_T \right] \quad (28)$$

$$Pw_{Tb} = dm2_Tb * C_p * (T1_Tb - T2_Tb). \quad (29)$$

In Eqs. 28 and 29, the  $T1_Tb$  and  $p1_Tb$  are the input temperature and input pressure. The  $T2_Tb$  is the output temperature. The  $p2_Tb$  is the output pressure, the atmospheric pressure.  $k$  is the ratio of specific heat,  $\eta_T$  is the isentropic efficiency, and  $C_p$  is the specific heat capacity at constant pressure.  $dm2_Tb$  is the mass flow rate, which is calculated according to the models discussed in this paper.

#### (3) Air cooler

The air cooler is modeled as a steady-state process. With the introduction of the heat exchange factor,  $\eta_c$ , the output temperature and output pressure can be easily obtained, as shown in Eqs. 30 and 31

$$T2_AC = T1_AC - \eta_c(T1_AC - T_w) \quad (30)$$

$$p2_{AC} = p1_{AC} + \Delta p. \quad (31)$$

The  $T1_{AC}$  and  $p1_{AC}$  are the input temperature and pressure. The  $T2_{AC}$  and  $p2_{AC}$  are the output temperature and pressure.  $\eta_c$  is the heat exchange factor and  $T_w$  is the temperature of water.

#### (4) Cylinder

For the MVEM, the cylinder model averages the cycles of engine. The detailed in-cylinder temperature and pressure cannot be obtained. The generated power is modeled using an interpolation model. It is treated as the average power according to the SFOC. The output temperature and the output mass flow rate are modeled as the mean value of several engine cycles in terms of the principle of energy conservation and the principle of mass conservation, as shown in Eqs. 32 and 33

$$T2_{Cd} = \frac{1}{dm2_{Cd} * C_p} (dm1_{Cd} * h_1 + dm_{FL} * H_u - P_{w-EG} - dQ) \quad (32)$$

$$dm2_{Cd} = dm1_{Cd} + dm_{FL}. \quad (33)$$



The  $dm1_Cd$ ,  $dm2_Cd$ ,  $dmf_FL$  are the mass flow rate of scavenging air, the mass flow rate of exhaust gas, and the mass flow rate of injected fuel.  $c_p$  is the specific heat at constant pressure,  $h_1$  is the specific entropy of scavenging air,  $H_u$  is the lower heating value of fuel,  $P_{w\_EG}$  is the output power of engine, and  $dQ$  is the rate of dissipated heat.

### (5) Mass flow rate of air

The flow process is modeled as the adiabatic process. It is used to calculate the output mass flow rate of the intake manifold and the output mass flow rate of turbine. This flow is divided into the subsonic flow and the choked flow. When

$$\frac{p_2-PF}{p_1-PF} \le \left( \frac{2}{k+1} \right)^{\frac{k}{k-1}}. \quad (34)$$

The flow is choked. At the throat, the speed of air flow reaches its maximum value and cannot increase anymore. In that case, the flow rate is calculated according to Eq. 35

$$\frac{dm2_{-PF}}{dt} = \mu \cdot A \cdot \frac{p_1-PF}{\sqrt{R \cdot T_1-PF}} \left( \frac{2}{k+1} \right)^{\frac{1}{k-1}} \sqrt{\frac{2k}{k+1}}. \quad (35)$$

Otherwise, the mass flow is subsonic. The speed of airflow is lower than its limit speed. The flow rate is calculated according to Eq. 36

$$\frac{dm2_{-PF}}{dt} = \mu \cdot A \cdot \frac{p_1-PF}{\sqrt{R \cdot T_1-PF}} \sqrt{\frac{2k}{k-1} \left[ \left( \frac{p_2-PF}{p_1-PF} \right)^{\frac{2}{k}} - \left( \frac{p_2-PF}{p_1-PF} \right)^{\frac{k+1}{k}} \right]}. \quad (36)$$

The  $p_2-PF$  is the pressure downstream of the flow, and the  $p_1-PF$ ,  $T_1-PF$  are the pressure and temperature upstream of the flow. The  $R$  is the gas constant of air,  $A$  is the flow area,  $\mu$  is the flow factor, and  $k$  is the ratio of specific heat.

### (6) The shaft of turbocharger

The shaft is modeled as a dynamic process. The work done on the shaft is converted to its kinetic energy. For a finite small time segment, the change of revolution is equal to the value calculated by Eq. 37. The  $Pw1_{-TC}$  is the driving power,  $Pw2_{-TC}$  is the resistance power, and  $J$  is the rotational inertia

$$n2_{-TC} = \sqrt{\frac{1800}{J\pi^2} \int (Pw1_{-TC} - Pw2_{-TC})dt + n_{-TC}^2}. \quad (37)$$

### (7) The intake manifold

The intake manifold is modeled as an open control volume. In terms of the principle of energy conservation and the principle of mass conservation, the temperature change and the mass change in the control volume can be calculated by Eqs. 38 and 39

$$\frac{dT_{-IM}}{dt} = \frac{1}{dm_{-IM} \cdot c_v} (dm1_{-IM} \cdot c_p \cdot T1_{-IM} - dm2_{-IM} \cdot c_p \cdot T2_{-IM} - u \cdot dm_{-IM}) \quad (38)$$

$$dm_{-IM} = dm1_{-IM} - dm2_{-IM}. \quad (39)$$

The  $dT_{-IM}$  and  $dm_{-IM}$  are the temperature change rate and the mass change rate of the intake manifold. The  $dm1_{-IM}$ ,  $dm2_{-IM}$  are the inlet mass flow rate and outlet mass flow rate. The  $T1_{-IM}$  and  $T2_{-IM}$  are the inlet temperature and outlet temperature of gas. The  $dm_{-IM}$  is the mass in the control volume,  $c_v$  is the specific heat at constant volume of intake air, and  $u$  is the specific internal energy of intake air.

### (8) The exhaust manifold

The exhaust manifold is modeled as an open control volume. In terms of the principle of energy conservation and the principle of mass conservation, the temperature change and the mass change in the control volume can be calculated by Eqs. 40 and 41

$$\frac{dT_{-EM}}{dt} = \frac{1}{dm_{-EM} \cdot c_v} (dm1_{-EM} \cdot c_p \cdot T1_{-EM} - dm2_{-EM} \cdot c_p \cdot T2_{-EM} - u \cdot dm_{-EM}) \quad (40)$$

$$dm_{-EM} = dm1_{-EM} - dm2_{-EM}. \quad (41)$$

The  $dT_{-EM}$  and  $dm_{-EM}$  are the temperature change rate and the mass change rate of the intake manifold. The  $dm1_{-EM}$  and  $dm2_{-EM}$  are the inlet mass flow rate and outlet mass flow rate. The  $T1_{-EM}$  and  $T2_{-EM}$  are the inlet temperature and outlet temperature of gas. The  $dm_{-EM}$  is the mass in the control volume,  $c_v$  is the specific heat at constant volume of exhaust gas, and  $u$  is the specific internal energy of exhaust gas.

## 4.3 Steady performance analysis

To investigate the influences of the compressor mass flow rate model on the mean value diesel engine model, the MVEMs embedded with three different compressor mass flow rate models are compared, respectively. The model's performance under the steady process and the dynamic process is also studied. Since M-JENSEN model has the

best overall performance, the MVEM embedded with M-JENSEN model is calibrated only and its parameters are used in the other models.

After the calibration of the MVEM, the simulation is carried out. The setting of the simulation under the steady state is shown in Table 7. The initial values are assigned according to the measured values and our experience.

The results of the MVEM embedded with 2D interpolation model, Kang Song's model, M-JENSEN model are presented in Table 8. The "M" denotes the measured value, "C" denotes the calculated value, and "E" denotes the error between the measured value and the calculated value. The calculation processes of the three cases are presented in Fig. 9. The value in the x-axis is the simulation time, from 0 to 15 s. The meaning of value in the y-axis can be obtained from the title of figure. The symbol in the title of this figure is the same as the symbol in Fig. 8. The RMRE in Fig. 9 is the root-mean-square relative error, which is defined as Eq. 42, similar to RMSE. The  $\hat{y}_i$  is the calculated value of the model, the  $y_i$  is the measured value, and  $n$  is the number of data. RMRE makes it easier to compare values of different sizes

$$\text{RMRE} = \sqrt{\frac{1}{n} \sum_{1}^{n} \left( \frac{\hat{y}_i - y_i}{y_i} \right)^2}. \quad (42)$$

**Table 7** Setting of simulation for the steady process

| Parameters            | Values |
|-----------------------|--------|
| Load [%]              | 100    |
| Calculation time [s]  | 15     |
| Step size [s]         | 0.01   |
| Output start time [s] | 0      |
| Output stop time [s]  | 15     |
| Output interval [s]   | 0.5    |

**Table 8** The final values of MVEM embedded with different compressor mass flow rate models

| Parameters                | M     | 2D IP   |       | KS      |       | M-JENSEN |       |
|---------------------------|-------|---------|-------|---------|-------|----------|-------|
|                           |       | C       | E (%) | C       | E (%) | C        | E (%) |
| dV_CP [m <sup>3</sup> /s] | 19.7  | ~19.8   | 0.54  | ~19.8   | 0.54  | ~19.8    | 0.54  |
| T2_Tb [K]                 | 546   | ~550.3  | 0.80  | ~550.3  | 0.80  | ~550.3   | 0.80  |
| n_TC [krpm]               | 16.0  | ~16.1   | 0.79  | ~16.8   | 4.69  | ~16.0    | 0.08  |
| Pw_Cd [kW]                | 25.2  | ~25.2   | 0.01  | ~25.2   | 0.01  | ~25.2    | 0.01  |
| p_IM [bar]                | 3.94  | ~3.95   | 0.28  | ~3.95   | 0.28  | ~3.95    | 0.28  |
| T_IM [K]                  | 317.0 | ~319.5  | 0.78  | ~319.5  | 0.78  | ~319.5   | 0.78  |
| p_EM [bar]                | 3.76  | ~3.74   | -0.40 | ~3.74   | -0.40 | ~3.74    | -0.40 |
| T_EM [K]                  | 726   | ~728.7  | 0.37  | ~728.7  | 0.37  | ~728.7   | 0.37  |
| dm1_Cd [kg/s]             | –     | ~46.3   | –     | ~46.3   | –     | ~46.3    | –     |
| Pw_Tb [kW]                | –     | ~3351.1 | –     | ~3351.1 | –     | ~3351.1  | –     |

From the data in Table 8 and the curves of calculation process in Fig. 9, the convergent paths are different, but, amazingly, the convergent values of MVEM are only different in the turbocharger speed, even though the mass flow rate model of compressor is different. According to the measurement of RMRE, the MVEM embedded with M-JENSEN has the best performance, and the MVEM embedded with the KS model has the worst performance. Actually, this comparison can only serve as a reference. It is because the MVEM embedded with the KS model is not calibrated. It uses the calibrated parameters of MVEM embedded with M-JENSEN. However, it is meaningful to realize that even though the mass flow rate model of compressor is not precise enough, it does not affect the accuracy of MVEM much.

## 4.4 Dynamic performance analysis

To further verify the results obtained from the steady process, the performance of MVEM under a dynamic process is carried out. The dynamic process checks the engine performance when the engine load changes from 100% to 80%. The load change occurs when the process almost reaches a steady state at 100% load. The setting of simulation is shown in Table 9. The initial values are assigned the same as that in steady process calculation.

The results of the MVEM embedded with 2D interpolation model, Kang Song's model, and M-JENSEN model are presented in Table 10. The "M" denotes the measured value, "C" denotes the calculated value, and "E" denotes the error between the measured value and the calculated value. The calculation processes of the three cases are presented in Fig. 10. The value on the x-axis is the simulation time, from 20 to 30 s. The value on the y-axis is corresponding to the value of the parameter shown in figure title. The meaning of symbol in the figure title is the same as the meaning of symbol in Fig. 8.

From the data in Table 10 and the curves of calculation process, it can be seen that the convergent paths of the three

![Figure 9: A 4x4 grid of 16 subplots showing the convergent process of MVEM with three different submodels (2D IP, KS, and M-JENSEN) over a simulation time of 15 seconds. Each subplot compares the three models using a legend at the top: blue triangles for 2D IP (RMRE = 0.54%), red circles for KS (RMRE = 1.63%), and green asterisks for M-JENSEN (RMRE = 0.48%). The subplots are labeled (1) through (16) and show various parameters: (1) T2_CP = 441.3K, (2) dV_CP = 19.8m³/s e = 0.54%, (3) Pw_CP = 3351.2kW, (4) T2_Tb = 550.3K e = 0.79%, (5) dm2_Tb = 23.8kg/s, (6) Pw_Tb = 3351.1kW, (7) n_Tc [krpm] with a legend for MJ (e=0.08%), KS (e=4.69%), and 2D (e=0.79%), (8) Pw_EG = 25.2MW e = 0.01%, (9) dm1_Cd = 46.3kg/s, (10) dm2_Cd = 47.5kg/s, (11) T2_Cd = 728.7K e = 0.37%, (12) p_IM = 3.95bar e = 0.28%, (13) T_IM = 319.5K e = 0.78%, (14) p_EM = 3.74bar e = -0.40%, (15) T_EM = 728.7K e = 0.37%, and (16) T2_AC = 319.5K. The x-axis for all plots is 'Simulation time [s]' from 0 to 15.](b05a8a3551db31147979064952179990_img.jpg)

Figure 9: A 4x4 grid of 16 subplots showing the convergent process of MVEM with three different submodels (2D IP, KS, and M-JENSEN) over a simulation time of 15 seconds. Each subplot compares the three models using a legend at the top: blue triangles for 2D IP (RMRE = 0.54%), red circles for KS (RMRE = 1.63%), and green asterisks for M-JENSEN (RMRE = 0.48%). The subplots are labeled (1) through (16) and show various parameters: (1) T2\_CP = 441.3K, (2) dV\_CP = 19.8m³/s e = 0.54%, (3) Pw\_CP = 3351.2kW, (4) T2\_Tb = 550.3K e = 0.79%, (5) dm2\_Tb = 23.8kg/s, (6) Pw\_Tb = 3351.1kW, (7) n\_Tc [krpm] with a legend for MJ (e=0.08%), KS (e=4.69%), and 2D (e=0.79%), (8) Pw\_EG = 25.2MW e = 0.01%, (9) dm1\_Cd = 46.3kg/s, (10) dm2\_Cd = 47.5kg/s, (11) T2\_Cd = 728.7K e = 0.37%, (12) p\_IM = 3.95bar e = 0.28%, (13) T\_IM = 319.5K e = 0.78%, (14) p\_EM = 3.74bar e = -0.40%, (15) T\_EM = 728.7K e = 0.37%, and (16) T2\_AC = 319.5K. The x-axis for all plots is 'Simulation time [s]' from 0 to 15.

**Fig. 9** The convergent process of MVEM with three different submodels under steady state

**Table 9** Setting of simulation for the dynamic process

| Parameters            | Values    |
|-----------------------|-----------|
| Load [%]              | 100 to 80 |
| Calculation time [s]  | 30        |
| Step size [s]         | 0.01      |
| Output start time [s] | 20        |
| Step time [s]         | 21        |
| Output stop time [s]  | 30        |
| Output interval [s]   | 0.2       |

models are almost the same. It can be observed from the data in Table 10 and the curves of the calculation process that the final convergent values of MVEM are also different in the turbocharger speed only. The results of model's performance are consistent with the results obtained from the steady process. The MVEM embedded with M-JENSEN has the best overall performance, and the MVEM embedded with the KS model has the worst overall performance. Although it is the worst, its maximum error is about 5.70%. It is still very accurate. The reason for that results is the

same as that in a steady process. It is meaningful to know from the results that even though the mass flow rate model of compressor is not precise enough, it does not affect the accuracy of MVEM much no matter for the steady process or the dynamic process.

## 4.5 Stability performance analysis

In real-time applications, the step size plays a crucial role in determining the simulation speed. Generally, using a larger step size results in faster calculations. However, it also leads to a decrease in accuracy and can even cause instability issues. To evaluate the stability performance of three models, both steady-state and dynamic processes were simulated with a step size of 0.03. The simulation settings are presented in Table 11.

The results of the three different models are presented in Figs. 11 and 12, representing the steady process and dynamic process, respectively. From these figures, it is evident that when the step size is increased, the convergent processes of the MVEM with MJ model and KS model remain almost the

**Table 10** The final values of the dynamic process show the only difference in turbocharger speed

| Parameters                         | <i>M</i> | 2D IP    |              | KS       |              | M-JENSEN |              |
|------------------------------------|----------|----------|--------------|----------|--------------|----------|--------------|
|                                    |          | <i>C</i> | <i>E</i> (%) | <i>C</i> | <i>E</i> (%) | <i>C</i> | <i>E</i> (%) |
| <i>dV_{CP}</i> [m <sup>3</sup> /s] | 17.7     | ~17.9    | 1.22         | ~17.9    | 1.22         | ~17.9    | 1.22         |
| <i>T2_Tb</i> [K]                   | 493      | ~500.5   | 1.52         | ~500.5   | 1.52         | ~500.5   | 1.52         |
| <i>n_{TC}</i> [krpm]               | 15.2     | ~15.3    | 0.39         | ~16.1    | 5.70         | ~15.2    | 0.12         |
| <i>Pw_Cd</i> [kW]                  | 20.1     | ~20.1    | 0.17         | ~20.1    | 0.17         | ~20.1    | 0.17         |
| <i>p_{IM}</i> [bar]                | 3.54     | ~3.57    | 0.97         | ~3.57    | 0.97         | ~3.57    | 0.97         |
| <i>T_{IM}</i> [K]                  | 311.0    | ~312.3   | 0.41         | ~312.3   | 0.41         | ~312.3   | 0.41         |
| <i>p_{EM}</i> [bar]                | 3.41     | ~3.43    | 0.64         | ~3.43    | 0.64         | ~3.43    | 0.64         |
| <i>T_{EM}</i> [K]                  | 671      | ~670.1   | -0.13        | ~670.1   | -0.13        | ~670.1   | -0.13        |
| <i>dm1_Cd</i> [kg/s]               | —        | ~42.0    | —            | ~42.0    | —            | ~42.0    | —            |
| <i>Pw_Tb</i> [kW]                  | —        | ~2276.9  | —            | ~2276.9  | —            | ~2276.9  | —            |

![Figure 10: A 4x4 grid of 16 subplots showing the dynamic process of MVEM with three different submodels (2D IP, KS, and M-JENSEN) over a simulation time of 30 seconds. The submodels are compared based on their Root Mean Relative Error (RMRE): 2D IP (RMRE = 1.59%), KS (RMRE = 2.40%), and M-JENSEN (RMRE = 1.58%). The plots show various parameters: (1) T2_CP, (2) dV_CP, (3) Pw_CP, (4) T2_Tb, (5) dm2_Tb, (6) Pw_Tb, (7) n_Tc, (8) Pw_EG, (9) dm1_Cd, (10) dm2_Cd, (11) T2_Cd, (12) p_IM, (13) T_IM, (14) p_EM, (15) T_EM, and (16) T2_AC. Most plots show a step change from 100% to 80% load at t=20s, followed by a transient response and steady-state. The M-JENSEN model generally shows the most accurate results, closely following the reference values.](411fa16c3211377525ba37c57784fee0_img.jpg)

Figure 10: A 4x4 grid of 16 subplots showing the dynamic process of MVEM with three different submodels (2D IP, KS, and M-JENSEN) over a simulation time of 30 seconds. The submodels are compared based on their Root Mean Relative Error (RMRE): 2D IP (RMRE = 1.59%), KS (RMRE = 2.40%), and M-JENSEN (RMRE = 1.58%). The plots show various parameters: (1) T2\_CP, (2) dV\_CP, (3) Pw\_CP, (4) T2\_Tb, (5) dm2\_Tb, (6) Pw\_Tb, (7) n\_Tc, (8) Pw\_EG, (9) dm1\_Cd, (10) dm2\_Cd, (11) T2\_Cd, (12) p\_IM, (13) T\_IM, (14) p\_EM, (15) T\_EM, and (16) T2\_AC. Most plots show a step change from 100% to 80% load at t=20s, followed by a transient response and steady-state. The M-JENSEN model generally shows the most accurate results, closely following the reference values.

**Fig. 10** The dynamic process of MVEM with three different submodels. The load changes from 100% to 80%

same as that shown in Figs. 9 and 10. However, the MVEM with the 2D IP model becomes unstable. Analyzing Fig. 11, we observe that the parameters directly or indirectly related to the mass flow rate of the compressor exhibit turbulent behavior. These parameters include the compressor output temperature, volume flow rate, consumption power of the

compressor, turbocharger speed, and mass flow rate through the engine air path. On the other hand, the indirect parameters are affected to a lesser extent, such as the pressure of the intake manifold, temperature of the intake manifold, and so on.

**Table 11** Setting of simulation for the stability analysis

| Parameter             | Steady process | Dynamic process |
|-----------------------|----------------|-----------------|
| Load [%]              | 100            | 100 to 80       |
| Calculation time [s]  | 15             | 30              |
| Step size [s]         | 0.03           | 0.03            |
| Output start time [s] | 0              | 20              |
| Step time [s]         | —              | 21              |
| Output stop time [s]  | 15             | 30              |
| Output interval [s]   | 0.5            | 0.2             |

The turbulence observed in the simulation results can be attributed to the characteristics of the model itself and the shape of the compressor map. Specifically, the working area of compressor map is quite narrow. This means that when there are changes in pressure ratio and turbocharger speed, the compressor is more prone to operate in the choke region and surge region, which can lead to instability. On the other hand, the 2D IP model exhibits poor extrapolation ability, as evident from its discontinuous behavior, as shown in Fig. 2.

When the compressor operates beyond the normal operating region, disturbances occur, and this can lead to the observed turbulence and instability in the results. In contrast, the MJ model and KS model display smoother behavior than the 2D IP model. Their stability performance is better, because they can handle operating conditions outside the normal region more effectively, reducing the chances of turbulence and instability in the simulation results.

Similar turbulence of MVEM with 2D IP model is also occurred in the dynamic process, as shown in Fig. 12. However, the amplitude of disturbance is different with the steady process. An obvious parameter is the output temperature of compressor,  $T2_{CP}$ . It is much smaller. It can also be observed from Fig. 12 that the amplitude of turbulence is gradually decrease. It is obvious for the volume flow rate of compressor, the turbocharger speed, and the consumption power of compressor. Another difference is that the turbulent disappear at about 26 s. This disappearance is because that in a calculation step, the increases of pressure ratio and turbocharger speed will not make the 2D IP model running out of the normal working area at 80% load.

![Figure 11: A 4x4 grid of 16 subplots showing the steady process of MVEM with three different submodels (2D IP, KS, and MJ) over a simulation time of 15 seconds. The submodels are compared based on their Root Mean Square Relative Error (RMRE): 2D IP (RMRE = 3.10%), KS (RMRE = 1.63%), and MJ (RMRE = 0.48%). The subplots show various parameters: (1) T2_CP, (2) dV_CP, (3) Pw_CP, (4) T2_Tb, (5) dm2_Tb, (6) Pw_Tb, (7) n_Tc, (8) Pw_EG, (9) dm1_Cd, (10) dm2_Cd, (11) T2_Cd, (12) p_IM, (13) T_IM, (14) p_EM, (15) T_EM, and (16) T2_AC. The 2D IP model (blue triangles) shows significant turbulence and discontinuities, while the KS (red circles) and MJ (green squares) models show much smoother behavior.](cc8bec39d25eb0aafb5382c05f0d5deb_img.jpg)

Figure 11: A 4x4 grid of 16 subplots showing the steady process of MVEM with three different submodels (2D IP, KS, and MJ) over a simulation time of 15 seconds. The submodels are compared based on their Root Mean Square Relative Error (RMRE): 2D IP (RMRE = 3.10%), KS (RMRE = 1.63%), and MJ (RMRE = 0.48%). The subplots show various parameters: (1) T2\_CP, (2) dV\_CP, (3) Pw\_CP, (4) T2\_Tb, (5) dm2\_Tb, (6) Pw\_Tb, (7) n\_Tc, (8) Pw\_EG, (9) dm1\_Cd, (10) dm2\_Cd, (11) T2\_Cd, (12) p\_IM, (13) T\_IM, (14) p\_EM, (15) T\_EM, and (16) T2\_AC. The 2D IP model (blue triangles) shows significant turbulence and discontinuities, while the KS (red circles) and MJ (green squares) models show much smoother behavior.

**Fig. 11** The steady process of MVEM with three different submodels whose step size is changed to 0.03

![Figure 12: A 4x4 grid of 16 subplots showing the dynamic process of MVEM with three different submodels (2D IP, KS, and M-JENSEN) over a 30-second simulation. Each subplot compares the three models using a legend: blue triangles for 2D IP (RMRE = 1.59%), red circles for KS (RMRE = 2.40%), and green asterisks for M-JENSEN (RMRE = 1.58%). The subplots are labeled (1) through (16) and show various parameters: (1) T2_CP, (2) dV_CP, (3) Pw_CP, (4) T2_Tb, (5) dm2_Tb, (6) Pw_Tb, (7) n_TC, (8) Pw_EG, (9) dm1_Cd, (10) dm2_Cd, (11) T2_Cd, (12) p_IM, (13) T_IM, (14) p_EM, (15) T_EM, and (16) T2_AC. Most parameters show a step change at 20s followed by a gradual decay or stabilization, with the M-JENSEN model generally showing the smoothest results.](b3df5964338063224492c01f09e4fed6_img.jpg)

Figure 12: A 4x4 grid of 16 subplots showing the dynamic process of MVEM with three different submodels (2D IP, KS, and M-JENSEN) over a 30-second simulation. Each subplot compares the three models using a legend: blue triangles for 2D IP (RMRE = 1.59%), red circles for KS (RMRE = 2.40%), and green asterisks for M-JENSEN (RMRE = 1.58%). The subplots are labeled (1) through (16) and show various parameters: (1) T2\_CP, (2) dV\_CP, (3) Pw\_CP, (4) T2\_Tb, (5) dm2\_Tb, (6) Pw\_Tb, (7) n\_TC, (8) Pw\_EG, (9) dm1\_Cd, (10) dm2\_Cd, (11) T2\_Cd, (12) p\_IM, (13) T\_IM, (14) p\_EM, (15) T\_EM, and (16) T2\_AC. Most parameters show a step change at 20s followed by a gradual decay or stabilization, with the M-JENSEN model generally showing the smoothest results.

**Fig. 12** The dynamic process of MVEM with three different submodels whose step size is changed to 0.03

The turbulence observed in the steady process is also present in the dynamic process, as depicted in Fig. 12. However, the amplitude of the disturbances is different. Notably, the output temperature of the compressor,  $T2_{CP}$ , exhibits a much smaller amplitude of disturbance during the dynamic process. Additionally, it can be observed from Fig. 12 that the amplitude of turbulence gradually decreases over time. This behavior is also noticeable for other parameters such as the volume flow rate of the compressor, turbocharger speed, and the consumption power of the compressor. Another amazing difference is that the turbulent behavior disappears at around 26 s. This disappearance can be attributed to the fact that, when closing to the 80% load, the increases in pressure ratio and turbocharger speed during a calculation step do not cause the 2D IP model outside its normal working range.

## 4.6 Study on the accuracy improvement of the physics-based KS model

Although the physics-based compressor mass flow rate model is not the most accurate, its performance in MVEM is also very good. Its properties of high accuracy and low measured data dependence will make this model to be used widely in the future. To investigate the potential for accuracy improvement, the MVEM with the KS model is tuned meticulously at 100% load. The final results are presented in Fig. 13. Compared these results with the results in Fig. 9, the overall RMRE decreases to 1.62% from 1.63%. This proves that the MVEM with the KS model has the potential to be improved further. This improvement is due to the error of turbocharger speed, the major contributor to the RMRE, falling from 4.69% to 4.55%. However, it can also be known

![Figure 13: A 4x4 grid of 16 subplots showing simulation results for various parameters over a 15-second period. Each subplot contains orange data points and a red line. A legend at the top states: 'Fine tuned MVEM with KS model (RMRE = 1.62% < 1.63%). The major error produced by n_Tc has been transferred to other parameters to lower the RMRE'. The subplots are labeled (1) through (16) and show parameters such as T2_CP, dV_CP, Pw_CP, T2_Tb, dm2_Tb, Pw_Tb, n_Tc, Pw_EG, dm1_Cd, dm2_Cd, T2_Cd, p_IM, T_IM, p_EM, T_EM, and T2_AC.](f4d72193f77f6646a2a1f4baaa927154_img.jpg)

Figure 13: A 4x4 grid of 16 subplots showing simulation results for various parameters over a 15-second period. Each subplot contains orange data points and a red line. A legend at the top states: 'Fine tuned MVEM with KS model (RMRE = 1.62% < 1.63%). The major error produced by n\_Tc has been transferred to other parameters to lower the RMRE'. The subplots are labeled (1) through (16) and show parameters such as T2\_CP, dV\_CP, Pw\_CP, T2\_Tb, dm2\_Tb, Pw\_Tb, n\_Tc, Pw\_EG, dm1\_Cd, dm2\_Cd, T2\_Cd, p\_IM, T\_IM, p\_EM, T\_EM, and T2\_AC.

**Fig. 13** The MVEM with physics-based KS model has the potential to be further improved, but it is limited

that the error decrease of  $n_{TC}$  causes the errors of  $T2_{Tb}$ ,  $T2_{Cd}$ ,  $T_{EM}$ , and  $p_{EM}$  increase. The error of  $n_{TC}$  has been transferred to other parameters. This action of averaging errors among parameters leads to a reduction of the overall RMRE. This behavior also explains the limitation of accuracy improvement for MVEM with the KS model. No matter how to tune the model meticulously, the accuracy of MVEM with the KS model cannot be improved much again. It will always be lower than the MVEM with a highly accurate compressor mass flow rate model. However, the MVEM with the KS model has already been of adequate accuracy to meet most of the cases.

# 5 Conclusions

To investigate the effect of the compressor mass flow rate model on the MVEM, the performance of mean value engine model embedded with different compressor mass flow rate models is studied. The interpolation-based 2D interpolation model, the physics-based Kang Song's model, and the

experience-based M-JENSEN model are used in MVEM. The KS model needs the least measured data and the M-JENSEN model has the best accuracy. Except for the mass flow rate model, all the other submodels, parameters, initial values are the same in the MVEM. After calibration and simulation, results show that the accuracy of mass flow rate model has little effect on the MVEM. The compressor mass flow rate model that needs the least measured data is more attractive to be used in MVEM. Detailed conclusions are presented in the following.

- (1) Although the accuracies of compressor mass flow rate models are different the final convergent values of MVEM only differ in turbocharger speed. For the mass flow rate models, the experience-based M-JENSEN model shows the best accuracy. Its root-mean-square error (RMSE) is about  $0.6 \text{ m}^3/\text{s}$ . While for the 2D interpolation model and KS model, its RMSE is about  $2.5 \text{ m}^3/\text{s}$  and  $3 \text{ m}^3/\text{s}$ . Although the models are different much in value and trend, the MVEM is affected little. The largest error in MVEM is the turbocharger

speed. However, it also shows good accuracy for the three models. Its error is 4.69% for the MVEM with KS model and it is 0.07% for the MVEM with M-JENSEN model at 100% load.

- (2) The interpolation model should be the best in the aspect of accuracy in our mind, but it shows a bad accuracy and presents a little instability for the 2D interpolation model. In the model test section, the RMSE of 2D interpolation model is about  $2.5 \text{ m}^3/\text{s}$  for data within the 2D grid and it will get nothing for data extrapolation. It is worse than the empirical model, the M-JENSEN model, whose RMSE is about  $0.6 \text{ m}^3/\text{s}$  and can be extrapolated. This degradation also makes the MVEM show a little worse accuracy than the MVEM with M-JENSEN model and shows a little disturbance during the dynamic process when the load changes from 100% to 80%. If the step size changed to 0.03, the 2D IP model causes great turbulence to MVEM.
- (3) It is more attractive to use a physics-based compressor mass flow rate model in MVEM for its low measured data dependence and good accuracy, especially in the case of lacking measured data. The physics-based KS model shows nearly the same accuracy and the same dynamic process as the interpolation model and empirical model. Its RMRE is about 1.63% at 100% load. Although it is larger than other models, it requires the least measured data. Only the data on the surge line are required for KS model. While for the other two models, the data over all the region of map are required. The error can be transferred from one parameter to other parameters to make the overall error of MVEM smaller, although it is limited. Through careful calibration, the RMRE of MVEM decreases from 1.63% to 1.62% at 100% load.

**Acknowledgements** The authors would like to thank Dr. Haosheng Shen for the inspiring discussions on the characteristics of the existing compressor models and for providing the data sets. Also, thanks to the reviewers for their valuable and specialized suggestions and rigorous academic attitude.

**Funding** The authors disclosed receipt of the following financial support for the research, authorship, and/or publication of this article: this work was supported by National Natural Science Foundation of China (52071090), China Postdoctoral Science Foundation (2021M690495), National Key R&D Program of China (2022YFB4301400), and High-Technology Ship Research Program (CBG3N21-3-3).

**Data availability** The test data has been provided in the figures.

# Declarations

**Conflict of interest** The authors declare no potential conflicts of interest with respect to the research, authorship, and/or publication of this article.

# References

1. Mousavi S, Nejat A, Alaviyoun SS, Nejat M (2021) An integrated turbocharger matching program for internal combustion engines. *J Appl Fluid Mech* 14:1209–1222
2. Mitzylthras P, Boulougouris E, Theotokatos G (2021) A novel objective oriented methodology for marine engine-turbocharger matching. *Int J Engine Res* 23(12):2105–2127
3. Wang QP, Yao HM, He YH, Yu YH, Yang JG (2021) Research on rail pressure control of high-pressure common rail system for marine diesel engine based on controlled object model. *IEEE Access* 9:125384–125392
4. Tang HY, Copeland C, Akehurst S, Brace C, Davies P, Pohorelsky L et al (2017) A novel predictive semi-physical feed-forward turbocharging system transient control strategy based on mean-value turbocharger model. *Int J Engine Res* 18:765–775
5. Bolbot V, Triviza NL, Theotokatos G, Boulougouris E, Rentzelas A, Vassalos D (2020) Cruise ships power plant optimisation and comparative analysis. *Energy* 196:117061
6. Ayad S, Vago CL, Belchior CRP, Sodre JR (2021) Cylinder pressure based calibration model for engines using ethanol, hydrogen and natural gas as alternative fuels. *Energy Rep* 7:7940–7954
7. Gooding WJ, Meier MA, Key NL (2021) The impact of various modeling decisions on flow field predictions in a centrifugal compressor. *J Turbomach Trans ASME*. <https://doi.org/10.11115/1.4050674>
8. Taylor AH, Odstreil TE, Ramesh AK, Shaver GM, Koerblein E, Farrell L et al (2021) Model-based compressor surge avoidance algorithm for internal combustion engines utilizing cylinder deactivation during motoring conditions. *Int J Engine Res* 22:1357–1366
9. Salameh G, Goumy G, Chesne P (2021) Water cooled turbocharger heat transfer model initialization: turbine and compressor quasi-adiabatic maps generation. *Appl Therm Eng* 185:116430
10. Zhu ZN, Liang K, Li ZH, Jiang HY, Meng ZW (2021) A numerical model of a linear compressor for household refrigerator. *Appl Therm Eng* 198:117467
11. Kristoffersen TT, Holden C (2021) Modeling and control of a wet-gas centrifugal compressor. *IEEE Trans Control Syst Technol* 29:1175–1190
12. Khaljani M, Vennard A, Harrison J, Surplus D, Murphy A, Mahmoudi Y (2021) Experimental and modelling analysis of efficiency enhancement in a liquid piston gas compressor using metal plate inserts for compressed air energy storage application. *J Energy Storage* 43:103240
13. Ahsan N, Al Rashid A, Zaidi AA, Imran R, Qadir SA (2021) Performance analysis of hydrogen fuel cell with two-stage turbo compressor for automotive applications. *Energy Rep* 7:2635–2646
14. Llamas X, Eriksson L (2017) Parameterizing compact and extensible compressor models using orthogonal distance minimization. *J Eng Gas Turbines Power Trans ASME*. <https://doi.org/10.11115/1.4034152>
15. Li X, Yang CL, Wang YY, Wang HC, Zu XH, Sun YR et al (2018) Compressor map regression modelling based on partial least squares. *Roy Soc Open Sci* 5:172454
16. Hu JW, Liu HR, Wang YG, Chen WX, Ma Y (2021) Reduced order model for unsteady aerodynamic performance of compressor cascade based on recursive RBF. *Chin J Aeronaut* 34:341–351
17. Ying YL, Xu SY, Li JC, Zhang B (2020) Compressor performance modelling method based on support vector machine nonlinear regression algorithm. *Roy Soc Open Sci* 7:191596
18. Sakellaridis NF, Raptotasios SI, Antonopoulos AK, Mavropoulos GC, Hountalas DT (2015) Development and validation of a new

- turbocharger simulation methodology for marine two stroke diesel engine modelling and diagnostic applications. *Energy* 91:952–966
19. Song K, Zhao B, Sun H, Yi WL (2019) A physics-based zero-dimensional model for the mass flow rate of a turbocharger compressor with uniform/distorted inlet condition. *Int J Engine Res* 20:624–639
  20. De Bellis V, Bontempo R (2018) Development and validation of a 1D model for turbocharger compressors under deep-surge operation. *Energy* 142:507–517
  21. Borovkov A, Galerkin Y, Petukhov E, Drozdov A, Yadikin V, Rekstin A et al (2022) CFD researches of centrifugal compressor stage vane diffusers in interests of math modeling. *Int J Adv Manuf Technol* 118:1–13
  22. Serrano JR, García-Cuevas LM, Inhestern LB, Guilain S, Tartoussi H (2018) Analysis of unsteady energy fluxes in a turbocharger by using a holistic model extrapolating standard lookup tables in full engine operating map. In: ASME turbo expo: turbomachinery technical conference and exposition. Oslo, Norway
  23. McMullen R, Pino Y (2018) Conditioning turbocharger compressor map data for use in engine performance simulation. *SAE Int J Engines* 11:491–507
  24. Jensen J, Kristensen A, Sorenson S, Houbak N (1991) Mean value modeling of a small turbocharged diesel engine. *SAE Technical Paper* 910070
  25. Karlson AT (2012) On modeling of a ship propulsion system for control purposes. Norwegian University of Science and Technology, Norwegian
  26. Tsoutsanis E, Meskin N, Benammar M, Khorasani K (2014) A component map tuning method for performance prediction and diagnostics of gas turbine compressors. *Appl Energy* 135:572–585
  27. Leufven O, Eriksson L (2016) Measurement, analysis and modeling of centrifugal compressor flow for low pressure ratios. *Int J Engine Res* 17:153–168
  28. Sun S, Wang ZP, Sun XP, Zhao HL, Wang ZP (2021) An adaptive compressor characteristic map method based on the Bezier curve. *Case Stud Therm Eng* 28:101512
  29. Yazar I, Yavuz HS, Yavuz AA (2017) Comparison of various regression models for predicting compressor and turbine performance parameters. *Energy* 140:1398–1406
  30. Faltin Z, Beneda K (2020) Establishment of meanline compressor mathematical model with active blade load distribution control. In: 18th IEEE world symposium on applied machine intelligence and informatics (SAMI). IEEE, Herlany, Slovakia, pp 63–68
  31. Grapow F, Liskiewicz G (2020) Study of the Greitzer model for centrifugal compressors: variable L-c parameter and two types of surge. *Energies* 13:6072
  32. Powers KH, Kennedy JJ, Brace CJ, Milewski PA, Copeland CD (2021) Development and validation of a model for centrifugal compressors in reversed flow regimes. *J Turbomach Trans ASME*. <https://doi.org/10.11115/1.4050668>
  33. Powers KH, Brace CJ, Budd CJ, Copeland CD, Milewski PA (2020) Modeling axisymmetric centrifugal compressor characteristics from first principles. *J Turbomach Trans ASME*. <https://doi.org/10.11115/1.4047616>
  34. Xu PC, Zou ZP, Xuan LM (2021) A hybrid performance prediction method for centrifugal compressors based on single-zone and two-zone models. *Aerosp Sci Technol* 108:106358
  35. Zhang XL, Li LW, Zhang TH (2022) Research on real-time model of turboshaft engine with surge process. *Appl Sci Basel* 12:744
  36. Pulpeiro Gonzalez J, Hall C (2018) Equation-based compressor and turbine modeling for variable geometry turbochargers. *SAE International*, USA
  37. Serrano JR, Arnau FJ, Gonzalez L, Gomez-Vilanova A, Guilain S (2018) Impact of a holistic turbocharger model in the prediction of engines performance in transient operation and in steady state with LP-EGR. In: ASME internal combustion engine fall technical conference, San Diego, CA
  38. Shen HS, Zhang C, Zhang JD, Yang BC, Jia BZ (2020) Applicable and comparative research of compressor mass flow rate and isentropic efficiency empirical models to marine large-scale compressor. *Energies* 13:1–47
  39. Kaechele A, Chioldi M, Bargende M (2018) Virtual full engine development: 3D-CFD simulations of turbocharged engines under transient load conditions. *SAE Int J Engines* 11:697–713
  40. Yang B, Fang XD, Zhang LS, Zhuang FT, Bi MH, Chen C et al (2019) Applicability of empirical models of isentropic efficiency and mass flow rate of dynamic compressors to jet engines. *Prog Aerosp Sci* 106:32–42
  41. Fang XD, Chen WW, Zhou ZR, Xu Y (2014) Empirical models for efficiency and mass flow rate of centrifugal compressors. *Int J Refrigeration Rev Int Du Froid* 41:190–199
  42. Guzzella L, Onder CH (2010) Introduction to modeling and control of internal combustion engine systems. Springer, New York
  43. Martin G (2010) 0D–1D modeling of the airpath of IC engines for control purposes. Université D’Orléans, France
  44. Moraal PE, Kolmanovsky I (1999) Turbocharger modeling for automotive control applications. *SAE Trans*. <https://doi.org/10.4271/1999-01-0908>

**Publisher's Note** Springer Nature remains neutral with regard to jurisdictional claims in published maps and institutional affiliations.

Springer Nature or its licensor (e.g. a society or other partner) holds exclusive rights to this article under a publishing agreement with the author(s) or other rightsholder(s); author self-archiving of the accepted manuscript version of this article is solely governed by the terms of such publishing agreement and applicable law.