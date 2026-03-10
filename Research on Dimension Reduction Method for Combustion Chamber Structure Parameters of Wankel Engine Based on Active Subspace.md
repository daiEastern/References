

![Processes journal logo](2dfa6ac3edfe874f68aa0cbccaa42322_img.jpg)

Processes journal logo

# Article

# Research on Dimension Reduction Method for Combustion Chamber Structure Parameters of Wankel Engine Based on Active Subspace

Liangyu Li <sup>1</sup>, Yaoyao Shi <sup>1</sup>, Ye Tian <sup>2</sup> ![ORCID icon](d66ff64371a51729ac8c1cdaa685ba6f_img.jpg), Wenyuan Liu <sup>3</sup> and Run Zou <sup>4,\*</sup>

- <sup>1</sup> School of Mechanical and Electrical Engineering, North University of China, Taiyuan 030051, China; zoyelly@163.com (L.L.); shiyaoyao0522@163.com (Y.S.)
- <sup>2</sup> School of Semiconductors and Physics, North University of China, Taiyuan 030051, China; tianye080t@163.com
- <sup>3</sup> School of Information and Communication Engineering, North University of China, Taiyuan 030051, China; lwy911218@163.com
- <sup>4</sup> School of Energy and Power Engineering, North University of China, Taiyuan 030051, China
- \* Correspondence: zourun@nuc.edu.cn

**Abstract:** The combustion chamber structure of a rotary engine involves a combination of interacting parameters that are simultaneously constrained by engine size, compression ratio, machining, and strength. It is more difficult to study the weight of the effect of the combustion chamber structure on the engine performance using traditional linear methods, and it is not possible to find the combination of structural parameters that has the greatest effect on the engine performance under the constraints. This makes it impossible to optimize the combustion chamber structure of a rotary engine by focusing on important structural parameters; it can only be optimized based on all structural parameters. In order to solve the above problems, this paper proposes a method of dimensionality reduction for the structural parameters of a combustion chamber based on active subspace and combining a probability box and the EDF (Empirical Distribution Function). This method uses engine performance indexes such as explosion pressure, maximum cylinder temperature, and indicated average effective pressure as the influence proportion analysis targets and quantitatively analyzes the influence proportion of combustion chamber structure parameters on engine performance. Eight main structural parameters with an influence of more than 85% on the engine performance indexes were obtained, on the basis of which three important structural parameters with an influence of more than 45% on the engine performance indexes and three adjustable structural parameters with an influence of less than 15% on the engine performance indexes were determined. This quantitative analysis work provides an optimization direction for the further optimization of the combustion chamber structure in the future.

**Keywords:** rotary engine; combustion chamber structure; active subspace; probability box; EDF; parameter dimension reduction

![Check for updates icon](84a1d09fb489061482111515543b60dc_img.jpg)

Check for updates icon

**Citation:** Li, L.; Shi, Y.; Tian, Y.; Liu, W.; Zou, R. Research on Dimension Reduction Method for Combustion Chamber Structure Parameters of Wankel Engine Based on Active Subspace. *Processes* **2024**, *12*, 2238. <https://doi.org/10.3390/pr12102238>

Academic Editor: Cherng-Yuan Lin

Received: 6 September 2024

Revised: 4 October 2024

Accepted: 8 October 2024

Published: 14 October 2024

![Creative Commons Attribution (CC BY) license logo](403aadfa553f530f227ac5d59f5a2e66_img.jpg)

Creative Commons Attribution (CC BY) license logo

**Copyright:** © 2024 by the authors. Licensee MDPI, Basel, Switzerland. This article is an open access article distributed under the terms and conditions of the Creative Commons Attribution (CC BY) license (<https://creativecommons.org/licenses/by/4.0/>).

## 1. Introduction

As a reliable power system, the internal combustion engine is widely used in many fields. Nowadays, inexpensive and reliable small engines are widely used as propulsion or auxiliary systems in motorcycles, all-terrain vehicles, boats, and small airplanes [1,2]. Although small piston engines are heavily used, they are less efficient compared to large piston engines [3–5]. And unlike a four-stroke reciprocating engine, where the piston stops briefly four times per cycle as the direction of motion changes, the moving parts of a rotary engine maintain a continuous, unidirectional rotary motion, which results in smoother work and less vibration [6–8]. At the same time, the rotary engine also has the advantages of higher power density, simple design, compact structure, and light weight [9–11]. These advantages make rotary engines strong competitors to reciprocating piston engines in areas such as supercharged vehicles and small unmanned aerial vehicles [12–14].

However, due to the narrow and flat combustion chamber shape, high surface area, and low compression ratio, it is difficult for rotary engines to achieve the fuel economy of reciprocating engines [15–18], which restricts the application of rotary engines in various fields [19,20]. In order to improve fuel economy and optimize rotary engine performance, scholars in various countries have conducted a series of investigations on engine structure [21–24]. For example, Kuo et al. investigated the effect of rotor profile on the compression flow of an engine by numerical analysis and found that increasing the shape factor  $K$  can benefit the compression efficiency and mixture formation [25]. Tartakovsky et al. started with the in-cylinder flow field and improved the engine performance by optimizing the rotor combustion chamber structure [26]. Jeng et al. further took the degree of mixing between fuel and air as the entry point and improved the engine performance by optimizing the rotor combustion chamber structure [27]. Wei et al. noticed that the position of the rotor combustion chamber has an effect on flame propagation and improved the engine performance by optimizing the rotor combustion chamber position [28–30]. Shi Cheng et al. investigated the role of turbulent blade position in the combustion process of a rotary engine and found that the closer the turbulent blade is to the spark plug chamber, the higher the turbulence velocity and turbulence dissipation rate are in the spark region. It was shown that the combustion rate of the mixture in the combustion chamber with a turbulent blade was accelerated, and it was able to exhibit better combustion characteristics and emission performance [31–34]. Zeng et al. [35] studied the influence of a turbulent blade on flow and combustion performance in the combustion chamber by numerically analyzing the total pressure loss, combustion efficiency, in-cylinder flow, and cylinder temperature changes of the combustion chamber under different spoiler structure parameters. It was found that adding a turbulent blade to the combustion chamber is beneficial to stabilize the combustion and gas mixing, which can further improve the combustion efficiency, improve the outlet temperature distribution, and reduce the pollutant emissions.

However, the above study only focuses on the influence of a certain structural parameter on engine performance and does not quantitatively analyze the proportions of the influence of all combustion chamber structural parameters on engine performance. This leads to the problem of dimensional catastrophe due to too many parameters to be optimized and the problem of not being able to determine the direction of optimization due to unclear parameter optimization priorities when optimizing the combustion chamber structure. Aiming at the combustion chamber structure, which is a complex physical system involving multiple disciplines and multidimensional uncertainties, domestic and foreign scholars have proposed a number of methods for dimensionality reduction. Among them, the gradient solver represented by Sensitivity Analysis (SA) [36] achieves dimensionality reduction by determining the magnitude of the influence of design and state variables on the objective or constraint functions and then filtering out the inputs with less influence. Linear projection methods represented by Classical Multidimensional Scaling (MDS) [37], Principal Component Analysis (PCA) [38], Linear Discriminant Analysis (LDA) [39], and Random Projection (RP) [40] complete the dimensionality reduction and sensitivity analysis processing by mapping the high-latitude problem to the low-latitude space. However, the above methods are not ideal for the dimensionality reduction and quantification of complex nonlinear problems. In this case, a nonlinear method is needed for dimensionality reduction. Common nonlinear methods include Kernel Principal Component Analysis (KPCA) [41], Local Linear Embedding (LLE) [42], Hessian Locally Linear Embedding (HLLE) [43], Laplacian Eigenmaps (LE) [44], and so on. However, the above methods are less computationally efficient in the face of complex, high-dimensional problems, especially in the face of mixed uncertainty problems, and are more sensitive to the selection of samples required for dimensionality reduction, which leads to the limited application of the above methods. In order to solve the problem of mixed uncertainty dimensionality reduction for complex systems, Paul et al. proposed a special dimensionality reduction structure, the Active Subspace (AS), in 2013 [45]. An AS is a low-dimensional action subspace defined by the sensitive directions of the input space, along which input perturbations maximize

the effect on the output. By identifying and utilizing the AS, the dimensionality reduction process can be accelerated while ensuring the analysis accuracy.

In this paper, on the basis of previous research, based on the AS, by combining the probability box with the interval variable Empirical Distribution Function (EDF) [46,47], a method of dimensionality reduction of the structural parameters of the combustion chamber of a rotary engine is proposed. A total of 14 combustion chamber structural parameters, including the turbulent blade, were subjected to eigenvalue estimation and dimensionality reduction, and the weights of the effects of different structural parameters on the maximum cylinder pressure, the maximum cylinder temperature, and the average effective pressure were obtained. Eight main structural parameters, including the angle  $\theta 1$  between the bottom edge of the middle part of the combustion chamber and the Y-Z plane were further obtained, and the influence of these structural parameters on the engine performance indexes accounted for more than 85%. Three important structural parameters, including the angle  $\theta 2$  between the bottom edge of the rear part of the combustion chamber and the Y-Z plane, were obtained on this basis, and the influence of these structural parameters on the engine performance indexes accounted for more than 45%. Three adjustable structural parameters, including the length  $l$  of the bottom edge of the front of the combustion chamber, were obtained. The influence of these three structural parameters on the engine performance index accounts for a relatively small percentage, below 15%, but their influence on the compression ratio and other structural requirements is larger and can be adjusted according to the compression ratio, process, and strength requirements after determining the main structural parameters. This quantitative analysis work provides an optimization direction and theoretical support for the further optimization of the combustion chamber structure in the future. At the same time, this study provides a reference basis for eigenvalue estimation and dimension reduction methods for multidimensional complex engineering problems.

## 2. Uncertainty Analysis of Combustion Chamber Structure Parameters

In practical engineering, the probability distribution is divided into random uncertainty and cognitive uncertainty [48,49]. The former has a known distribution function, and the latter lacks such a function.

This study investigates how structural parameter uncertainty in the combustion chamber impacts single-cylinder gasoline Wankel engine performance. Table 1 lists the engine's structural parameters.

**Table 1.** Rotor engine structure parameters.

| Parameter                   | Value                 |
|-----------------------------|-----------------------|
| Creation radius (mm)        | 60                    |
| Eccentricity (mm)           | 10                    |
| Rotor width (mm)            | 42                    |
| Translational distance (mm) | 1.45                  |
| Speed (r/min)               | 8000                  |
| Single cylinder volume (cc) | 133                   |
| Compression ratio           | 10                    |
| Ignition advance angle      | 30° BTDC              |
| Ignition source             | Single spark plug     |
| Fuel type                   | Gasoline              |
| Jet strategy                | Pre-mixed intake duct |
| Air-fuel ratio              | 1                     |
| Ignition diameter (mm)      | 8                     |
| Ignition energy (J)         | 0.08                  |
| Engine power (kw)           | 12.3                  |
| Torque (N.m)                | 15.66                 |
| Oil consumption (g/kw·h)    | 402.3                 |

The rotor engine combustion is categorized into four parts: leading, middle, trailing, and spoiler. Rounded corners smooth the bottom surfaces. The cross sections of the leading, middle, and trailing parts of the combustion chamber are ovals formed by two semicircles and a rectangle, while the spoiler plate is a cuboid with a height below the rotor profile (Figure 1).

![Figure 1: Wankel engine combustion chamber structure. The diagram shows a top-down view of the combustion chamber with a central rotor. The rotor is divided into three sections: the Leading part of combustion chamber, the Middle of combustion chamber, and the Trailing part of combustion chamber. A spoiler plate is attached to the leading edge of the rotor. A coordinate system is shown with a yellow arrow for 'Rotation direction' along the Y-axis and a red arrow for the X-axis. Labels point to the spoiler, the three combustion chamber parts, and the rotation and axis directions.](16d86083b7ebdc40c0647a1d3d46ace7_img.jpg)

Figure 1: Wankel engine combustion chamber structure. The diagram shows a top-down view of the combustion chamber with a central rotor. The rotor is divided into three sections: the Leading part of combustion chamber, the Middle of combustion chamber, and the Trailing part of combustion chamber. A spoiler plate is attached to the leading edge of the rotor. A coordinate system is shown with a yellow arrow for 'Rotation direction' along the Y-axis and a red arrow for the X-axis. Labels point to the spoiler, the three combustion chamber parts, and the rotation and axis directions.

**Figure 1.** Wankel engine combustion chamber structure.

The Wankel engine's combustion chamber consists of three elliptical cross sections and an oblong spoiler plate. The middle and trailing parts share the same cross-sectional dimensions but differ in inclination angles. Figures 2 and 3 depict the size schematics, and Table 2 compares the variables and structural parameters.

![Figure 2: Variable comparison table. This diagram shows the Wankel engine combustion chamber with three cross-sections labeled A-A, B-B, and C-C. A yellow arrow indicates the 'Rotation direction' along the Y-axis. A red arrow indicates the X-axis. The cross-sections A-A and B-B are vertical, while C-C is horizontal. The diagram illustrates the geometric variables used for comparison.](d0baec9a9191662196c3f3be304ee01c_img.jpg)

Figure 2: Variable comparison table. This diagram shows the Wankel engine combustion chamber with three cross-sections labeled A-A, B-B, and C-C. A yellow arrow indicates the 'Rotation direction' along the Y-axis. A red arrow indicates the X-axis. The cross-sections A-A and B-B are vertical, while C-C is horizontal. The diagram illustrates the geometric variables used for comparison.

**Figure 2.** Variable comparison table.

To maintain the same compression ratio, the rotor combustion chamber must meet eight structural, process, and performance requirements:

- (1) The distance from the deepest part of the rotor combustion chamber to its center of gravity on the  $x$ - $z$  plane must not exceed  $h_a$ , considering structural strength, heat dissipation structure arrangement, and spindle assembly.
- (2) The maximum width of the chamber must not exceed  $l_a$ , addressing seal arrangement and structural strength.
- (3) The distance between the chamber ends and the rotor tip on the  $y$ - $z$  plane must not exceed  $k_a$ , addressing radial seal arrangement and structural strength.

- (4) The width of the rotor spoiler plate must not exceed  $c_a$ , ensuring spoiler plate strength.
- (5) According to research, the spoiler plate height should be at least  $\frac{4b_a}{5}$  [26–30], where  $b_a$  signifies the vertical distance from the chamber bottom to the rotor profile at the spoiler plate position.
- (6) To simplify processing, the rotor spoiler should be positioned centrally or toward the rear of the combustion chamber, avoiding overlap between chamber sections.
- (7) The leading and middle parts of the combustion chamber must be connected, with a single recess on the rotor surface.
- (8) The arc radius of the transition section must not exceed  $q_a$ .

![Figure 3: Combustion chamber dimensions. (a) A-A section size showing length l and distance h. (b) B-B section size showing trailing arc radius R and length L. (c) C-C section angle showing angles theta1, theta2, and theta3. (d) C-C section size showing total height H, bottom edge distance b, spoiler plate distance a, and width c.](17a042ee648d9fdaddb609aead503980_img.jpg)

Figure 3 consists of four diagrams (a, b, c, d) illustrating the dimensions of a combustion chamber. (a) A-A section size: A cross-section of the combustion chamber showing the leading edge. The length of the leading bottom edge is labeled  $l$ , and the vertical distance from the bottom of the leading section to the rotor's center of gravity is labeled  $h$ . (b) B-B section size: A cross-section of the combustion chamber showing the trailing edge. The trailing arc radius is labeled  $R$ , and the length of the trailing bottom edge is labeled  $L$ . (c) C-C section angle: A cross-section of the combustion chamber showing the transition section. The angles between the bottom edges and the  $y$ - $z$  plane are labeled  $\theta_1$ ,  $\theta_2$ , and  $\theta_3$ . (d) C-C section size: A cross-section of the combustion chamber showing the transition section. The total height is labeled  $H$ , the distance from the bottom to the rotor's center of gravity is labeled  $b$ , the vertical distance from the spoiler plate to the bottom edge is labeled  $a$ , and the width of the spoiler plate is labeled  $c$ .

Figure 3: Combustion chamber dimensions. (a) A-A section size showing length l and distance h. (b) B-B section size showing trailing arc radius R and length L. (c) C-C section angle showing angles theta1, theta2, and theta3. (d) C-C section size showing total height H, bottom edge distance b, spoiler plate distance a, and width c.

**Figure 3.** Combustion chamber dimensions. (a) A-A section size. (b) B-B section size. (c) C-C section angle. (d) C-C section size.

**Table 2.** Variable comparison.

| Variable   | Structure Name                                                                                                                         |
|------------|----------------------------------------------------------------------------------------------------------------------------------------|
| $r$        | Combustion chamber leading arc radius                                                                                                  |
| $l$        | Length of the leading bottom edge of the combustion chamber                                                                            |
| $h$        | The distance from the bottom of the combustion chamber's leading section to the rotor's center of gravity at the $x$ - $z$ plane       |
| $\theta_3$ | The angle between the combustion chamber's leading bottom edge and the $y$ - $z$ plane                                                 |
| $R$        | Trailing arc radius in the combustion chamber                                                                                          |
| $L$        | Trailing bottom edge length of the combustion chamber                                                                                  |
| $H$        | The distance from the bottom of the trailing section of the combustion chamber to the rotor's center of gravity at the $x$ - $z$ plane |
| $\theta_1$ | The angle between the middle bottom edge of the combustion chamber and the $y$ - $z$ plane                                             |
| $\theta_2$ | The angle between the trailing bottom edge of the combustion chamber and the $y$ - $z$ plane                                           |
| $a$        | The vertical distance between the spoiler plate and the rotor $x$ - $z$ section                                                        |
| $b$        | The distance from the spoiler's top center to the combustion chamber's bottom edge                                                     |
| $c$        | The spoiler plate's width                                                                                                              |
| $q_1$      | The excessive arc radius from the leading part to the middle of the combustion chamber                                                 |
| $q_2$      | The excessive arc radius from the middle to the trailing part of the combustion chamber                                                |

To ensure that the generated structural parameter combination meets the above requirements, the entire combustion chamber structure is parameterized first, so that a series of formulas can be used to calculate whether a certain structural combination meets the

requirements of compression ratio, size, processing, and strength. When generating structural combinations, the values of several structural parameters are randomly generated within the required range of size, processing, and strength. Based on this, the compression ratio is used as the optimization objective; the size, processing, and strength requirements are used as the range; and the remaining structural parameters are used as the solving parameters for optimization iteration using optimization algorithms.

Using the parameters in Table 3, 100 sets of structural parameter combinations were generated, including the 14 parameters listed. Figures 4–17 depict their distribution and probabilities. From these figures,  $c$ ,  $q1$ , and  $q2$  follow a uniform distribution, while  $a$  follows a normal distribution. The distributions of  $r$ ,  $l$ ,  $h$ ,  $\theta3$ ,  $R$ ,  $L$ ,  $H$ ,  $\theta1$ ,  $\theta2$ , and  $b$  are unclear, representing cognitive uncertainty. Consequently, the dimension reduction problem involves 14 dimensions with 4 random and 10 cognitive uncertainty variables.

**Table 3.** Constraints.

| Constraint Name                                                                                                         | Variable Name | Value |
|-------------------------------------------------------------------------------------------------------------------------|---------------|-------|
| The minimum distance from the bottom of the combustion chamber to the center of gravity of the rotor                    | $h_\alpha$    | 42 mm |
| Maximum width of the combustion chamber                                                                                 | $l_\alpha$    | 40 mm |
| The projection distance between the two ends of the rotor combustion chamber and the rotor tip on the $y$ - $z$ section | $k_\alpha$    | 10 mm |
| Maximum width of the spoiler plate                                                                                      | $c_\alpha$    | 3 mm  |
| The maximum radius of the excessive arc                                                                                 | $q_\alpha$    | 2 mm  |

![Figure 4: Distribution of the arc radius (r) at the leading edge of the combustion chamber. (a) Distribution conditions: A line plot showing the arc radius r/mm (0 to 100) versus Sampling frequency (0 to 100). The data points are scattered around a mean of approximately 50 mm. (b) Distribution probability: A bar chart showing Frequency/% (0 to 50) versus Values (0 to 100). The distribution is roughly bell-shaped, peaking at approximately 48% for the value 15.](e1dda754c2c88a8ad0b968aea4fc0786_img.jpg)

Figure 4: Distribution of the arc radius (r) at the leading edge of the combustion chamber. (a) Distribution conditions: A line plot showing the arc radius r/mm (0 to 100) versus Sampling frequency (0 to 100). The data points are scattered around a mean of approximately 50 mm. (b) Distribution probability: A bar chart showing Frequency/% (0 to 50) versus Values (0 to 100). The distribution is roughly bell-shaped, peaking at approximately 48% for the value 15.

**Figure 4.** Distribution of the arc radius ( $r$ ) at the leading edge of the combustion chamber. (a) Distribution conditions. (b) Distribution probability.

![Figure 5: Distribution of the length (l) at the leading bottom edge of the combustion chamber. (a) Distribution conditions: A line plot showing the length l/mm (0 to 15) versus Sampling frequency (0 to 100). The data points are scattered around a mean of approximately 5 mm. (b) Distribution probability: A bar chart showing Frequency/% (0 to 40) versus Values (0 to 11). The distribution is roughly bell-shaped, peaking at approximately 38% for the value 1.](80530169c7b6298ce012a85b906caeb3_img.jpg)

Figure 5: Distribution of the length (l) at the leading bottom edge of the combustion chamber. (a) Distribution conditions: A line plot showing the length l/mm (0 to 15) versus Sampling frequency (0 to 100). The data points are scattered around a mean of approximately 5 mm. (b) Distribution probability: A bar chart showing Frequency/% (0 to 40) versus Values (0 to 11). The distribution is roughly bell-shaped, peaking at approximately 38% for the value 1.

**Figure 5.** Distribution of the length ( $l$ ) at the leading bottom edge of the combustion chamber. (a) Distribution conditions. (b) Distribution probability.

![Figure 6: Distribution of the distance (h) from the front section bottom of the combustion chamber to the rotor's center of gravity in the x-z plane. (a) Distribution conditions: A line plot showing h/mm (40-70) vs Sampling frequency (0-100). (b) Distribution probability: A histogram showing Frequency/% (0-40) vs Values (45-65).](c0843c6d138705289960d9f53a6e72a1_img.jpg)

Figure 6 consists of two subplots. Subplot (a) is a line graph showing the distribution of distance  $h$  (in mm) versus sampling frequency (0 to 100). The y-axis ranges from 40 to 70 mm. The data points show a fluctuating distribution with peaks around 15, 25, 45, 65, and 85 sampling frequencies. Subplot (b) is a histogram showing the frequency distribution of  $h$  values. The x-axis is labeled 'Values' and ranges from 45 to 65. The y-axis is labeled 'Frequency/%' and ranges from 0 to 40. The distribution is skewed towards lower values, with a peak frequency of approximately 38% at a value of 50.

Figure 6: Distribution of the distance (h) from the front section bottom of the combustion chamber to the rotor's center of gravity in the x-z plane. (a) Distribution conditions: A line plot showing h/mm (40-70) vs Sampling frequency (0-100). (b) Distribution probability: A histogram showing Frequency/% (0-40) vs Values (45-65).

**Figure 6.** Distribution of the distance ( $h$ ) from the front section bottom of the combustion chamber to the rotor's center of gravity in the  $x$ - $z$  plane. (a) Distribution conditions. (b) Distribution probability.

![Figure 7: Distribution of the angle (θ3) between the leading bottom edge of the combustion chamber and the y-z plane. (a) Distribution conditions: A line plot showing θ3/° (0-30) vs Sampling frequency (0-100). (b) Distribution probability: A histogram showing Frequency/% (0-25) vs Values (0-25).](c64e9e9f3b0b828a5f6ac70441877764_img.jpg)

Figure 7 consists of two subplots. Subplot (a) is a line graph showing the distribution of angle  $\theta_3$  (in degrees) versus sampling frequency (0 to 100). The y-axis ranges from 0 to 30 degrees. The data points show a fluctuating distribution with peaks around 15, 25, 45, 65, and 85 sampling frequencies. Subplot (b) is a histogram showing the frequency distribution of  $\theta_3$  values. The x-axis is labeled 'Values' and ranges from 0 to 25. The y-axis is labeled 'Frequency/%' and ranges from 0 to 25. The distribution is relatively uniform, with a peak frequency of approximately 24% at values of 5 and 10.

Figure 7: Distribution of the angle (θ3) between the leading bottom edge of the combustion chamber and the y-z plane. (a) Distribution conditions: A line plot showing θ3/° (0-30) vs Sampling frequency (0-100). (b) Distribution probability: A histogram showing Frequency/% (0-25) vs Values (0-25).

**Figure 7.** Distribution of the angle ( $\theta_3$ ) between the leading bottom edge of the combustion chamber and the  $y$ - $z$  plane. (a) Distribution conditions. (b) Distribution probability.

![Figure 8: Distribution of the length (R) at the trailing bottom of the combustion chamber. (a) Distribution conditions: A line plot showing R/mm (0-100) vs Sampling frequency (0-100). (b) Distribution probability: A histogram showing Frequency/% (0-50) vs Values (0-100).](01da0d212fb571933f10f96556157745_img.jpg)

Figure 8 consists of two subplots. Subplot (a) is a line graph showing the distribution of length  $R$  (in mm) versus sampling frequency (0 to 100). The y-axis ranges from 0 to 100 mm. The data points show a fluctuating distribution with peaks around 15, 25, 45, 65, and 85 sampling frequencies. Subplot (b) is a histogram showing the frequency distribution of  $R$  values. The x-axis is labeled 'Values' and ranges from 0 to 100. The y-axis is labeled 'Frequency/%' and ranges from 0 to 50. The distribution is skewed towards lower values, with a peak frequency of approximately 46% at a value of 20.

Figure 8: Distribution of the length (R) at the trailing bottom of the combustion chamber. (a) Distribution conditions: A line plot showing R/mm (0-100) vs Sampling frequency (0-100). (b) Distribution probability: A histogram showing Frequency/% (0-50) vs Values (0-100).

**Figure 8.** Distribution of the length ( $R$ ) at the trailing bottom of the combustion chamber. (a) Distribution conditions. (b) Distribution probability.

![Figure 9: Distribution of the length (L) at the trailing bottom of the combustion chamber. (a) Distribution conditions: A scatter plot showing L/mm (0 to 15) versus Sampling frequency (0 to 100). (b) Distribution probability: A bar chart showing Frequency/% (0 to 60) versus Values (0 to 14).](a71911ad87414271aeb190e0eebcb989_img.jpg)

Figure 9 consists of two subplots. Subplot (a) is a scatter plot showing the distribution conditions of length  $L$  in mm against sampling frequency from 0 to 100. The y-axis ranges from 0 to 15 mm. Subplot (b) is a bar chart showing the distribution probability of  $L$  in percentage against discrete values from 0 to 14. The y-axis ranges from 0 to 60%.

Figure 9: Distribution of the length (L) at the trailing bottom of the combustion chamber. (a) Distribution conditions: A scatter plot showing L/mm (0 to 15) versus Sampling frequency (0 to 100). (b) Distribution probability: A bar chart showing Frequency/% (0 to 60) versus Values (0 to 14).

**Figure 9.** Distribution of the length ( $L$ ) at the trailing bottom of the combustion chamber. (a) Distribution conditions. (b) Distribution probability.

![Figure 10: Distribution of the distance (H) from the trailing chamber bottom to the rotor's center of gravity in the x-z plane. (a) Distribution conditions: A scatter plot showing H/mm (40 to 54) versus Sampling frequency (0 to 100). (b) Distribution probability: A bar chart showing Frequency/% (0 to 18) versus Values (42 to 51).](ecb25d766719ce041cf4cc390791a098_img.jpg)

Figure 10 consists of two subplots. Subplot (a) is a scatter plot showing the distribution conditions of distance  $H$  in mm against sampling frequency from 0 to 100. The y-axis ranges from 40 to 54 mm. Subplot (b) is a bar chart showing the distribution probability of  $H$  in percentage against discrete values from 42 to 51. The y-axis ranges from 0 to 18%.

Figure 10: Distribution of the distance (H) from the trailing chamber bottom to the rotor's center of gravity in the x-z plane. (a) Distribution conditions: A scatter plot showing H/mm (40 to 54) versus Sampling frequency (0 to 100). (b) Distribution probability: A bar chart showing Frequency/% (0 to 18) versus Values (42 to 51).

**Figure 10.** Distribution of the distance ( $H$ ) from the trailing chamber bottom to the rotor's center of gravity in the  $x$ - $z$  plane. (a) Distribution conditions. (b) Distribution probability.

![Figure 11: Distribution of the angle (θ1) between the combustion chamber's middle bottom edge and the y-z plane. (a) Distribution conditions: A scatter plot showing θ1/° (0 to 20) versus Sampling frequency (0 to 100). (b) Distribution probability: A bar chart showing Frequency/% (0 to 18) versus Values (0 to 15).](27b22513fc27a0ff5f230b062ad3112f_img.jpg)

Figure 11 consists of two subplots. Subplot (a) is a scatter plot showing the distribution conditions of angle  $\theta_1$  in degrees against sampling frequency from 0 to 100. The y-axis ranges from 0 to 20 degrees. Subplot (b) is a bar chart showing the distribution probability of  $\theta_1$  in percentage against discrete values from 0 to 15. The y-axis ranges from 0 to 18%.

Figure 11: Distribution of the angle (θ1) between the combustion chamber's middle bottom edge and the y-z plane. (a) Distribution conditions: A scatter plot showing θ1/° (0 to 20) versus Sampling frequency (0 to 100). (b) Distribution probability: A bar chart showing Frequency/% (0 to 18) versus Values (0 to 15).

**Figure 11.** Distribution of the angle ( $\theta_1$ ) between the combustion chamber's middle bottom edge and the  $y$ - $z$  plane. (a) Distribution conditions. (b) Distribution probability.

![Figure 12: Distribution of the angle (θ2) between the trailing bottom of the combustion chamber and the y-z plane. (a) Distribution conditions: A scatter plot showing θ2 (°) on the y-axis (0 to 20) versus Sampling frequency on the x-axis (0 to 100). (b) Distribution probability: A histogram showing Frequency/% on the y-axis (0 to 20) versus Values on the x-axis (0 to 15).](91be14371a97fb5ce9eeb29ae18d07c3_img.jpg)

Figure 12 consists of two subplots. Subplot (a) is a scatter plot showing the distribution conditions of the angle  $\theta_2$  (in degrees) over 100 sampling frequencies. The y-axis ranges from 0 to 20, and the x-axis ranges from 0 to 100. The data points are scattered, with a general trend of fluctuating between 5 and 15 degrees. Subplot (b) is a histogram showing the distribution probability of  $\theta_2$ . The y-axis is Frequency/% (0 to 20) and the x-axis is Values (0 to 15). The distribution is unimodal, peaking at approximately 18% for the value 1.

Figure 12: Distribution of the angle (θ2) between the trailing bottom of the combustion chamber and the y-z plane. (a) Distribution conditions: A scatter plot showing θ2 (°) on the y-axis (0 to 20) versus Sampling frequency on the x-axis (0 to 100). (b) Distribution probability: A histogram showing Frequency/% on the y-axis (0 to 20) versus Values on the x-axis (0 to 15).

**Figure 12.** Distribution of the angle ( $\theta_2$ ) between the trailing bottom of the combustion chamber and the y-z plane. (a) Distribution conditions. (b) Distribution probability.

![Figure 13: Distribution of the vertical distance (a) between the spoiler plate and the rotor x-z section. (a) Distribution conditions: A scatter plot showing a/mm on the y-axis (-40 to 40) versus Sampling frequency on the x-axis (0 to 100). (b) Distribution probability: A histogram showing Frequency/% on the y-axis (0 to 50) versus Values on the x-axis (-30 to 40).](891ff9b651838b7f59e9a1612a739e15_img.jpg)

Figure 13 consists of two subplots. Subplot (a) is a scatter plot showing the distribution conditions of the vertical distance  $a$  (in mm) over 100 sampling frequencies. The y-axis ranges from -40 to 40, and the x-axis ranges from 0 to 100. The data points show a fluctuating pattern around zero. Subplot (b) is a histogram showing the distribution probability of  $a$ . The y-axis is Frequency/% (0 to 50) and the x-axis is Values (-30 to 40). The distribution is unimodal, peaking at approximately 48% for the value 0.

Figure 13: Distribution of the vertical distance (a) between the spoiler plate and the rotor x-z section. (a) Distribution conditions: A scatter plot showing a/mm on the y-axis (-40 to 40) versus Sampling frequency on the x-axis (0 to 100). (b) Distribution probability: A histogram showing Frequency/% on the y-axis (0 to 50) versus Values on the x-axis (-30 to 40).

**Figure 13.** Distribution of the vertical distance ( $a$ ) between the spoiler plate and the rotor  $x$ - $z$  section. (a) Distribution conditions. (b) Distribution probability.

![Figure 14: Distribution of the distance (b) from the spoiler top center to the chamber bottom edge. (a) Distribution conditions: A scatter plot showing b/mm on the y-axis (40 to 55) versus Sampling frequency on the x-axis (0 to 100). (b) Distribution probability: A histogram showing Frequency/% on the y-axis (0 to 70) versus Values on the x-axis (46 to 52).](0f3e3ea50bcceb86f6c524ab2b6f3e7a_img.jpg)

Figure 14 consists of two subplots. Subplot (a) is a scatter plot showing the distribution conditions of the distance  $b$  (in mm) over 100 sampling frequencies. The y-axis ranges from 40 to 55, and the x-axis ranges from 0 to 100. The data points are tightly clustered around 51 mm. Subplot (b) is a histogram showing the distribution probability of  $b$ . The y-axis is Frequency/% (0 to 70) and the x-axis is Values (46 to 52). The distribution is unimodal, peaking at approximately 65% for the value 51.

Figure 14: Distribution of the distance (b) from the spoiler top center to the chamber bottom edge. (a) Distribution conditions: A scatter plot showing b/mm on the y-axis (40 to 55) versus Sampling frequency on the x-axis (0 to 100). (b) Distribution probability: A histogram showing Frequency/% on the y-axis (0 to 70) versus Values on the x-axis (46 to 52).

**Figure 14.** Distribution of the distance ( $b$ ) from the spoiler top center to the chamber bottom edge. (a) Distribution conditions. (b) Distribution probability.

![Figure 15: Distribution of the spoiler plate width (c). (a) Distribution conditions: A line plot showing c/mm (0.0 to 3.0) versus Sampling frequency (0 to 100). (b) Distribution probability: A histogram showing Frequency/% (0 to 25) versus Values (0.5 to 2.5).](7801d00a216dc4dc8a7d210dcb5fe3c5_img.jpg)

Figure 15 consists of two subplots. Subplot (a) is a line graph showing the distribution conditions of the spoiler plate width  $c$  in mm. The y-axis ranges from 0.0 to 3.0 mm, and the x-axis represents the sampling frequency from 0 to 100. The data points are connected by vertical lines, showing a fluctuating distribution. Subplot (b) is a histogram showing the distribution probability of  $c$ . The y-axis is Frequency/% from 0 to 25, and the x-axis is Values from 0.5 to 2.5. The histogram shows a distribution with peaks around 1.0, 1.5, 2.0, and 2.5 mm.

Figure 15: Distribution of the spoiler plate width (c). (a) Distribution conditions: A line plot showing c/mm (0.0 to 3.0) versus Sampling frequency (0 to 100). (b) Distribution probability: A histogram showing Frequency/% (0 to 25) versus Values (0.5 to 2.5).

**Figure 15.** The distribution of the spoiler plate width ( $c$ ). (a) Distribution conditions. (b) Distribution probability.

![Figure 16: Distribution of the excessive arc radius (q1) between the leading and middle chamber sections. (a) Distribution conditions: A line plot showing q1/mm (0.0 to 2.5) versus Sampling frequency (0 to 100). (b) Distribution probability: A histogram showing Frequency/% (0 to 25) versus Values (0.2 to 2.0).](6b32b7b928d34eeccb15c29cdf9d2cb3_img.jpg)

Figure 16 consists of two subplots. Subplot (a) is a line graph showing the distribution conditions of the excessive arc radius  $q1$  in mm. The y-axis ranges from 0.0 to 2.5 mm, and the x-axis represents the sampling frequency from 0 to 100. The data points are connected by vertical lines, showing a fluctuating distribution. Subplot (b) is a histogram showing the distribution probability of  $q1$ . The y-axis is Frequency/% from 0 to 25, and the x-axis is Values from 0.2 to 2.0. The histogram shows a distribution with peaks around 0.4, 1.0, 1.4, and 1.8 mm.

Figure 16: Distribution of the excessive arc radius (q1) between the leading and middle chamber sections. (a) Distribution conditions: A line plot showing q1/mm (0.0 to 2.5) versus Sampling frequency (0 to 100). (b) Distribution probability: A histogram showing Frequency/% (0 to 25) versus Values (0.2 to 2.0).

**Figure 16.** Distribution of the excessive arc radius ( $q1$ ) between the leading and middle chamber sections. (a) Distribution conditions. (b) Distribution probability.

![Figure 17: Distribution of the excessive arc radius (q2) between the middle and trailing chamber sections. (a) Distribution conditions: A line plot showing q2/mm (0.0 to 2.0) versus Sampling frequency (0 to 100). (b) Distribution probability: A histogram showing Frequency/% (0 to 25) versus Values (0.2 to 2.0).](33228b4227fa57e1477b27b9e07483e6_img.jpg)

Figure 17 consists of two subplots. Subplot (a) is a line graph showing the distribution conditions of the excessive arc radius  $q2$  in mm. The y-axis ranges from 0.0 to 2.0 mm, and the x-axis represents the sampling frequency from 0 to 100. The data points are connected by vertical lines, showing a fluctuating distribution. Subplot (b) is a histogram showing the distribution probability of  $q2$ . The y-axis is Frequency/% from 0 to 25, and the x-axis is Values from 0.2 to 2.0. The histogram shows a distribution with peaks around 0.4, 1.0, 1.4, and 1.8 mm.

Figure 17: Distribution of the excessive arc radius (q2) between the middle and trailing chamber sections. (a) Distribution conditions: A line plot showing q2/mm (0.0 to 2.0) versus Sampling frequency (0 to 100). (b) Distribution probability: A histogram showing Frequency/% (0 to 25) versus Values (0.2 to 2.0).

**Figure 17.** Distribution of the excessive arc radius ( $q2$ ) between the middle and trailing chamber sections. (a) Distribution conditions. (b) Distribution probability.

## 3. Estimation Method of Active Subspace Eigenvalues Based on Probability Box-EDF

Recent advancements in dimensionality reduction techniques such as principal component analysis, factor analysis, topological mapping regression, and random projection have been significant [50–52]. Building on principal component analysis, the active subspace method evaluates input parameters through the output covariance matrix. This 

technique has been used in transonic wing design optimization, hydrological model construction, and satellite optimization, demonstrating benefits for complex system problems at high latitudes.

Unlike principal component analysis, which focuses on eigenvalue size impact on the covariance, the active subspace method constructs a new subspace by adjusting eigenvectors to significantly alter the system output direction [53,54]. For a system  $f$  with initial dimension  $n$ , its input  $x$ , output  $f$ , output function gradient  $f\nabla$ , and reduced dimension input  $v$  can be expressed as follows:

$$\begin{cases} x = [x_1, x_2, x_3, \dots, x_n]^T \\ f = f(x) \\ f\nabla = f\nabla(x) \\ v' = [v'_1, v'_2, v'_3, \dots, v'_m]^T \\ n > m \end{cases} \quad (1)$$

Normalizing each boundary of the standard parameter space to  $[0, 1]$  allows the non-standard parameter space to be transformed through regularization. The input parameter  $x$  with  $N$  samples can be expressed as follows:

$$X = \{x_{i,j}; 1 \le i \le n, 1 \le j \le N\} \quad (2)$$

Any member of matrix  $X$  can be regularized as follows:

$$\begin{cases} x'_{i,j} = \frac{x_{i,j} - \hat{\mu}_i}{\hat{\sigma}_i} \\ \hat{\mu}_i = \frac{1}{N} \sum_{j=1}^{N} x_{i,j} \\ \hat{\sigma}_i = \sqrt{\frac{1}{N} \sum_{j=1}^{N} (x_{i,j} - \bar{x}_i)^2} \end{cases} \quad (3)$$

The gradient covariance matrix of  $f$  is as follows:

$$\begin{cases} C = \int f\nabla(x) f\nabla(x)^T \rho(x) dx = W\Lambda W^T \\ \Lambda = \text{diag}(\lambda_1, \lambda_2, \lambda_3, \dots, \lambda_n) \end{cases} \quad (4)$$

where  $W$  signifies an orthogonal matrix,  $\Lambda$  represents a non-negative eigenvalue matrix, and the eigenvalue's relative size indicates the variables' contribution to the objective function. In practical engineering, obtaining the transfer function  $f(x)$  for the gradient covariance matrix is challenging, so the limited difference computation method is often used to calculate the sample outputs to derive  $f\nabla$  and  $C$  [55,56]. The gradient covariance matrix can be expressed as follows:

$$C = \frac{1}{N} \sum_{i=1}^{N} f\nabla_i(x) f\nabla_i(x)^T \quad (5)$$

The eigenvalues in matrix  $\Lambda$  are arranged in descending order, yielding  $\Lambda' = \text{diag}(\lambda_1, \lambda_2, \lambda_3, \dots, \lambda_n)$ . The first  $m$  eigenvalues are chosen as the new active subspace dimensions, with the selection criteria shown in Equation (6).

$$\begin{cases} \frac{\lambda_m}{\sum_{i=1}^{n} \lambda_i} \ge k \\ \frac{\lambda_{m+1}}{\sum_{i=1}^{n} \lambda_i} \le k \end{cases} \quad (6)$$

where  $k$  denotes the proportional coefficient. The eigenvalue matrix  $\Lambda'$  is divided into the first  $m$  order  $\Lambda'_1$  and the last  $n-m$  order  $\Lambda'_2$ .

$$\Lambda' = \begin{bmatrix} \Lambda'_1 & \\ & \Lambda'_2 \end{bmatrix} \quad (7)$$

Equation (4) can be expressed as

$$C = W\Lambda W^T = [U \ V] \begin{bmatrix} \Lambda'_1 & \\ & \Lambda'_2 \end{bmatrix} [U \ V]^T \quad (8)$$

where  $U$  denotes the basis vector for the active eigenvalue. After dimension reduction, the input  $v$  can be expressed as follows:

$$v = U^T x \quad (9)$$

The objective function can be approximated as follows:

$$f(x) \approx g(U^T x) \quad (10)$$

The error between the original and the dimension-reduced objective functions can be expressed as shown below:

$$\int f(x) - g(U^T x) \rho dx \quad (11)$$

The active subspace method, widely used across various fields, faces limitations due to input variable uncertainty. From Equation (4), the gradient covariance matrix of  $f$  can only be calculated if the probability distribution  $\rho(x)$  of all input variables is known. Once this distribution is clear, the gradient covariance matrix can be calculated using the transfer function or samples, leading to the eigenvalue matrix  $\Lambda$ . Consequently, the subspace method for dimension reduction is applicable only if all input independent variables are random with a clear probability distribution. This limitation restricts the active subspace method's use in engineering. Further research is needed on dimensionality reduction for cognitive and mixed uncertainty problems in engineering [57].

An objective function  $f$  with  $p$  random uncertainty variables,  $q$  cognitive uncertainty input independent variables, and  $n$  mixed uncertainty input independent variables can be expressed as follows:

$$\begin{cases} f = f(x_a, x_e) \\ x_a \sim \rho(x_a) \\ x_e \in [x_e^L, x_e^U] \\ x_a = \{x_{a1}, x_{a2}, x_{a3}, \dots, x_{ap}\} \\ x_e = \{x_{e1}, x_{e2}, x_{e3}, \dots, x_{eq}\} \end{cases} \quad (12)$$

The gradient of each independent variable can be expressed as

$$\nabla_x f^I = \left[ \frac{\partial f}{\partial x_{a1}} \dots \frac{\partial f}{\partial x_{ap}} \frac{\partial f}{\partial x_{e1}} \dots \frac{\partial f}{\partial x_{eq}} \right]^T \quad (13)$$

where the real interval vector  $\nabla_x f^I$ , its upper limit  $\bar{c}_i$ , and its lower limit  $\underline{c}_i$  can be expressed as follows:

$$\begin{cases} \bar{c}_i = \max \left\{ \frac{\partial f}{\partial x_i}, x_a \sim \rho(x_a), x_e \in [x_e^L, x_e^U] \right\} \\ \underline{c}_i = \min \left\{ \frac{\partial f}{\partial x_i}, x_a \sim \rho(x_a), x_e \in [x_e^L, x_e^U] \right\} \end{cases} \quad (14)$$

Combining Equations (13) and (14) indicates that when  $q = 0$ ,  $\nabla_x f^I = \nabla_x f$ . When  $q \neq 0$ , the gradient covariance matrix  $C$  in Equation (4) can be expressed as

$$C = \hat{C}^I = \frac{1}{M} \sum_{k=1}^{M} (\nabla_x f_k^I) \cdot (\nabla_x f_k^I)^T \quad (15)$$

where  $\hat{C}^I$  is a real symmetric interval matrix with  $M$  samples. Each element in  $\hat{C}^I$  can be expressed as

$$\begin{aligned} \hat{C}_{ij}^I &= \frac{1}{M} \sum_{k=1}^{M} \left( \frac{\partial f_k^I}{\partial x_i} \right) \cdot \left( \frac{\partial f_k^I}{\partial x_j} \right) \\ &= \left[ \hat{C}_{ij}, \hat{C}_{ij} \right] \\ &= \left[ \frac{1}{M} \sum_{k=1}^{M} c_{ij}^k, \frac{1}{M} \sum_{k=1}^{M} \bar{c}_{ij}^k \right] \\ &\quad i, j = 1, \dots, n \end{aligned} \quad (16)$$

where  $\left[ c_{ij}^k, \bar{c}_{ij}^k \right]$  can be expressed as follows:

$$\begin{aligned} \left[ c_{ij}^k, \bar{c}_{ij}^k \right] &= \left[ c_i^k, \bar{c}_i^k \right] \times \left[ c_j^k, \bar{c}_j^k \right] \\ &= \left[ \min \left( c_i^k c_j^k, c_i^k \bar{c}_j^k, \bar{c}_i^k c_j^k, \bar{c}_i^k \bar{c}_j^k \right), \max \left( c_i^k c_j^k, c_i^k \bar{c}_j^k, \bar{c}_i^k c_j^k, \bar{c}_i^k \bar{c}_j^k \right) \right] \end{aligned} \quad (17)$$

Each feature pair in  $\hat{C}^I$  can be expressed as shown below:

$$\left( \lambda_i^I, w_i^I \right) \quad i = 1, \dots, n \quad (18)$$

Based on the analysis, the mixed uncertainty dimension reduction problem is transformed into the eigenvalue interval problem of  $\hat{C}^I$  expressed as follows:

$$\begin{aligned} \lambda^I &= [\lambda, \bar{\lambda}] \\ &= [\lambda_i, \bar{\lambda}_i] \\ &\quad i = 1, \dots, n \end{aligned} \quad (19)$$

According to the Deif theorem, if a matrix retains the eigenvector component's sign within the interval, the upper and lower bounds of the eigenvalues can be determined. The sign matrix that remains unchanged on  $\hat{C}^I$  is expressed as follows [58].

$$S^i = \text{diag}(\text{sgn}(w_i)) \quad i = 1, \dots, n \quad (20)$$

$$\begin{cases} (\hat{C}^c - S^i \Delta \hat{C} S^i) w_i = \lambda_i w_i \\ (\hat{C}^c + S^i \Delta \hat{C} S^i) \bar{w}_i = \bar{\lambda}_i \bar{w}_i \end{cases} \quad i = 1, \dots, n \quad (21)$$

where  $\hat{C}^c$  signifies the median matrix of  $\hat{C}^I$ , and  $\Delta \hat{C}$  represents the radius matrix of  $\hat{C}^I$ , expressed as

$$\begin{cases} \hat{C}^c = (\hat{C}_{ij}^c) = \frac{\hat{C}_{ij} + \bar{C}_{ij}}{2} \\ \hat{C}_{ij}^c = \frac{\hat{C}_{ij} + \bar{C}_{ij}}{2} \\ i = 1, \dots, n \\ \Delta \hat{C} = (\Delta \hat{C}_{ij}^c) = \frac{\hat{C}_{ij} - \bar{C}_{ij}}{2} \\ \Delta \hat{C}_{ij}^c = \frac{\hat{C}_{ij} - \bar{C}_{ij}}{2} \\ i = 1, \dots, n \end{cases} \quad (22)$$

where  $\text{sgn}(w_i)$  denotes the vector of the symbol function for each element of  $w_i$ . If all elements in  $w_i$  have the same sign, then the following is true:

$$\begin{cases} \hat{C} w_i = \lambda_i w_i \\ \hat{C} \bar{w}_i = \bar{\lambda}_i \bar{w}_i \\ i = 1, \dots, n \end{cases} \quad (23)$$

The maximum and minimum values of  $|w_i|$  can be computed as follows, where  $I$  is the unit matrix.

$$\begin{cases} \lambda_i - \Delta \hat{C} |w_i| \le (\lambda_i I - S^i \hat{C}^c S^i) |w_i| \le \Delta \hat{C} |w_i| \\ \left[ \lambda_i I - S^i \hat{C}^c S^i - \Delta \hat{C} \right] |w_i| \le 0 \\ i = 1, \dots, n \end{cases} \quad (24)$$

A positive semi-definite real symmetric matrix  $C$  has an orthogonal matrix  $W$ , such that

$$W^T \hat{C} W = \text{diag}(\lambda_1, \lambda_2, \dots, \lambda_n) \quad (25)$$

For  $\Lambda = \text{diag}(\lambda_1, \lambda_2, \dots, \lambda_n)$ , we have

$$\begin{cases} (W w_i)^T \hat{C} W w_i = w_i^T \Lambda w_i = \lambda_1 w_1^2 + \lambda_2 w_2^2 + \dots + \lambda_n w_n^2 \ge 0 \\ w_i = [w_1, w_2, \dots, w_n]^T \\ \lambda_i \ge 0 \\ i = 1, \dots, n \end{cases} \quad (26)$$

where

$$\begin{aligned} \lambda_i &= w_i^T \hat{C} w_i \\ &= w_i^T \left[ \frac{1}{M} \sum_{k=1}^{M} (\nabla_x f_k^l) \cdot (\nabla_x f_k^l)^T \right] w_i \\ &= \frac{1}{M} \sum_{k=1}^{M} \left[ (\nabla_x f_k)^T w_i \right]^2 \ge 0 \\ i &= 1, \dots, n \end{aligned} \quad (27)$$

where  $w_i$  denotes the effect of the  $i$ -th input variable on the objective function. Combined with Equations (4)–(11), it yields dimensionality reduction of mixed uncertainty.

In deriving a mixed uncertainty dimension reduction problem from Equations (20)–(27), a key requirement is that the gradient covariance matrix  $\hat{C}^l$  must satisfy the Deif theorem, maintaining the sign of eigenvector components within the interval. In practice, it is challenging to verify without the objective function ( $f$ ) or sufficient data. To tackle large computational load, dimensionality, and prior condition challenges in mixed uncertainty reduction, eigenvalue estimation techniques and gradient response estimation approaches have been proposed. The former include the disc method, perturbation method, and spectral radius method. The latter represent direct optimization, eigenvalue analysis, and modal decomposition. Eigenvalue methods only approximate ranges and cannot obtain upper and lower bounds, while gradient response methods lose accuracy with high system uncertainty [50].

This study proposes a mixed uncertainty eigenvalue estimation method using the EDF and probability boxes [59–61] for dimension reduction, as illustrated in Figure 18.

The EDF describes variable distributions by approximating sample frequencies to the probability distribution of random variables as a step function, resulting in the Cumulative Distribution Function (CDF). This method converts the mixed uncertainty dimension reduction into a random uncertainty problem. Figure 19 shows a CDF with an EDF distribution, where the black line shows the EDF fit and the histogram indicates variable probabilities [62,63].

![Flowchart of Eigenvalue estimation of the mixed uncertainty active subspace using the EDF and probability box.](724c7777b608e53be38b12b6fb3c43bc_img.jpg)

```

graph TD
    A[Independent variable to be reduced] --> B[Generate analysis samples]
    B --> C[Distinguish random/Cognitive uncertain independent variables]
    C --> D[Calculate the probability density function of random uncertain independent variables.]
    C --> E[The corresponding EDF is generated by the probability distribution of the cognitive uncertain independent variables in the sample to be analyzed.]
    D --> F[Calculate the eigenvalue vector]
    E --> F
    F --> G[According to the set threshold, the independent variables of the active subspace output after dimension reduction are]
  
```

Flowchart of Eigenvalue estimation of the mixed uncertainty active subspace using the EDF and probability box.

**Figure 18.** Eigenvalue estimation of the mixed uncertainty active subspace using the EDF and probability box.

![Figure 19: EDF distribution. A dual-axis plot showing a histogram of probability and a line graph of cumulative probability density.](fe753d01ad5fe6cf150018c958173c6d_img.jpg)

The figure is a dual-axis plot. The x-axis is labeled 'Values' and ranges from 0 to 100. The left y-axis is labeled 'Probability/%' and ranges from 0 to 60. The right y-axis is labeled 'Cumulative probability density' and ranges from 0.0 to 1.0. The legend indicates that the orange bars represent 'Probability' and the black line with square markers represents 'Cumulative probability density'. The data points are approximately: (15, 20), (35, 30), (55, 10), and (75, 40). The cumulative probability reaches 1.0 at a value of 80.

| Values | Probability/% | Cumulative probability density |
|--------|---------------|--------------------------------|
| 15     | 20            | 0.20                           |
| 35     | 30            | 0.50                           |
| 55     | 10            | 0.60                           |
| 75     | 40            | 1.00                           |

Figure 19: EDF distribution. A dual-axis plot showing a histogram of probability and a line graph of cumulative probability density.

**Figure 19.** EDF distribution.

In practice, due to randomness in input variables, the empirical density is fitted using an equal distribution model. The empirical density function for mixed uncertainty is

$$\hat{F}_n(x) = \frac{\sum_{i=1}^{n} I(X_i \le x_i)}{n} \quad (28)$$

where the EDF is fitted by  $\hat{F}_n(x)$ ;  $X_i$  represents an independent and identically distributed random variable;  $x_i$  denotes the function value of the empirical distribution function at  $x$ ; and  $n$  signifies the number of samples. The accuracy of the empirical density function increases with more samples.

All cognitive uncertainty variables can be expressed as random uncertainty variables.

$$\begin{aligned} y &= \hat{W}_1^T(x_a, x_e) \\ x_a &\sim \rho_{x_a}, x_e \sim \rho_{x_e} \end{aligned} \quad (29)$$

where  $\rho_{x_a}$  and  $\rho_{x_e}$  denote the sampling weights of random and cognitive uncertainties based on the distribution function and fitted differential EDF, respectively. Integrating these variables into the equation yields the following:

$$C = \frac{1}{N} \sum_{i=1}^{N} y \nabla_i(x) y \nabla_i(x)^T \quad (30)$$

Eigenvalues for the mixed uncertainty active subspace are determined using Equation (27), enabling mixed uncertainty dimensionality reduction. Probability boxes representing variable distributions are used to obtain EDF curves. These boxes incorporate interval concepts for both random and cognitive uncertainties. Figure 20 illustrates a probability box variable  $x$  with cumulative distribution function  $\hat{F}_n(x)$ , upper bound  $\hat{F}_n(x)$ , and lower bound  $\hat{F}_n(x)$ . The probability box requires only upper and lower distribution bounds to split the boundary around the variable distribution function, eliminating the need for specific distribution forms and ensuring that the cumulative distribution function lies within the defined boundaries.

![Figure 20: A graph illustrating a probability box. The horizontal axis is labeled 'x' and the vertical axis is labeled 'F'. The origin is marked '0'. Two S-shaped curves are shown, representing the upper and lower bounds of the probability box. The area between these two curves is shaded light blue. The upper curve is labeled 'F' and the lower curve is labeled 'F-bar'.](a430996a9e8993deb0c6b25da234744b_img.jpg)

Figure 20: A graph illustrating a probability box. The horizontal axis is labeled 'x' and the vertical axis is labeled 'F'. The origin is marked '0'. Two S-shaped curves are shown, representing the upper and lower bounds of the probability box. The area between these two curves is shaded light blue. The upper curve is labeled 'F' and the lower curve is labeled 'F-bar'.

**Figure 20.** Probability box.

To obtain the probability box of variables, we use the D-S theory composed of multiple focal elements. For a sample in space  $R$ , any D-S structure can be expressed as

$$\begin{cases} m : 2^R \to [0, 1] \\ m(\emptyset) \neq 0, \sum_{A \subseteq R} m(A) = 1 \end{cases} \quad (31)$$

where each interval  $A$  is a focal element;  $m(A)$  denotes the reliability value corresponding to this focal element; and  $2^R$  signifies the power set of  $R$ . The trust function  $Bel$  and the likelihood function  $Pl$  can be expressed as follows:

$$\begin{cases} Bel(A) = \sum\{m(B) | B \subseteq A, B \neq \emptyset\} \\ Pl(A) = \sum\{m(B) | A \cap B, B \neq \emptyset\} \end{cases} \quad (32)$$

Probability boxes consist of multiple D-S structures, the upper and lower bounds of which are accumulated to attain the left boundary of the upper and lower bounds of the probability box. The D-S structure represents a discretized probability box. Figure 21 illustrates the relationship between the probability box and the structure. EDF fitting using probability boxes is conducted as follows:

Step 1: Resample  $N$  samples into  $N$  groups, and divide each group into  $M$  segments from largest to smallest.

- Step 2: Use each segment's maximum and minimum values as upper and lower bounds, respectively. If the distribution aligns with a certain distribution model, the upper and lower bounds of each group's probability are obtained based on the distribution model; otherwise, the bounds are obtained based on the EDF probability distribution in Equation (28).
- Step 3: Average the maximum upper bounds and minimum lower bounds across  $N$  groups to obtain the fitted cumulative probability curve.

![Figure 21: Probability box and structure. The diagram shows a coordinate system with x on the horizontal axis and a vertical axis. A smooth S-shaped curve represents the cumulative distribution function (CDF). A shaded region between two parallel curves, one above and one below the CDF, represents the probability box. The upper boundary is labeled with a bar over F (F-bar) and the lower boundary is labeled with a bar under F (F-underline).](fed39b841ae2dce01088b84bfc1e2789_img.jpg)

Figure 21: Probability box and structure. The diagram shows a coordinate system with x on the horizontal axis and a vertical axis. A smooth S-shaped curve represents the cumulative distribution function (CDF). A shaded region between two parallel curves, one above and one below the CDF, represents the probability box. The upper boundary is labeled with a bar over F (F-bar) and the lower boundary is labeled with a bar under F (F-underline).

**Figure 21.** Probability box and structure.

To verify the accuracy of the above methods, this study evaluates an objective function with random and cognitive uncertainties, as shown in Equation (33), where  $x_1$  denotes a random variable uniformly distributed in  $[0, 1]$ , and  $x_2$  represents a cognitive variable in  $[0, 3]$ . Figure 22 shows the distribution and probabilities from 100 samples, which do not fit any standard distribution model.

$$f(x_1, x_2) = e^{x_1} + x_2 + x_1 x_2 \quad (33)$$

![Figure 22: Distribution of the independent variable x2. (a) Distribution conditions: A scatter plot showing 100 samples of x2. The x-axis is 'Sampling frequency' (0 to 100) and the y-axis is 'Values' (0.0 to 3.0). The points are scattered across the range. (b) Distribution probability: A histogram showing the frequency of x2 values. The x-axis is 'Values' (0.4 to 2.8) and the y-axis is 'Frequency/%' (0 to 25). The distribution is skewed towards lower values.](250cf77a1cd51989da09fca796b3e4ea_img.jpg)

Figure 22: Distribution of the independent variable x2. (a) Distribution conditions: A scatter plot showing 100 samples of x2. The x-axis is 'Sampling frequency' (0 to 100) and the y-axis is 'Values' (0.0 to 3.0). The points are scattered across the range. (b) Distribution probability: A histogram showing the frequency of x2 values. The x-axis is 'Values' (0.4 to 2.8) and the y-axis is 'Frequency/%' (0 to 25). The distribution is skewed towards lower values.

**Figure 22.** Distribution of the independent variable  $x_2$ . (a) Distribution conditions. (b) Distribution probability.

Equation (4) shows that with  $M$  samples, the gradient covariance matrix  $C$  of  $f(x_1, x_2)$  can be expressed as follows:

$$C = \hat{C}^I = \frac{1}{M} \sum_{k=1}^{M} (\nabla_x f_k^I) \cdot (\nabla_x f_k^I)^T \quad (34)$$

$$= \frac{1}{M} \sum_{k=1}^{M} \left[ \begin{bmatrix} e^{2x_1} & e^{2x_1} + 6e^{x_1} + 9 \\ [(x_1 + 1)e^{x_1}, (x_1 + 1)e^{x_1} + 3(x_1 + 1)e^{x_1} + 3] \\ x_1^2 + 2x_1 + 1 \end{bmatrix} \begin{bmatrix} [(x_1 + 1)e^{x_1}, (x_1 + 1)e^{x_1} + 3(x_1 + 1)e^{x_1} + 3] \end{bmatrix} \right]$$

The EDF obtained by probability box fitting is shown in Figure 23.

![Figure 23: A line graph showing the Cumulative probability versus Values. The x-axis (Values) ranges from 0.0 to 3.0 with increments of 0.5. The y-axis (Cumulative probability) ranges from 0.0 to 1.0 with increments of 0.2. The data points are connected by a smooth curve that starts at (0.0, 0.0) and ends at (3.0, 1.0), showing a typical sigmoidal shape of an Empirical Distribution Function (EDF).](b6750d26d3dd287a4a4d49b3670a44bd_img.jpg)

Figure 23: A line graph showing the Cumulative probability versus Values. The x-axis (Values) ranges from 0.0 to 3.0 with increments of 0.5. The y-axis (Cumulative probability) ranges from 0.0 to 1.0 with increments of 0.2. The data points are connected by a smooth curve that starts at (0.0, 0.0) and ends at (3.0, 1.0), showing a typical sigmoidal shape of an Empirical Distribution Function (EDF).

**Figure 23.** Fit EDF depicting the EDF fitted using the probability box.

With  $M = 100$  samples, eigenvalues  $\lambda_1$ ,  $\lambda_2$ , and their proportions, obtained using computation Equations 33 and 34 probability box–EDF estimation, are shown in Table 4. The proposed method achieves high accuracy, with a deviation of only 1.2931%, making it effective for eigenvalue calculation and dimensionality reduction in rotor engine combustion chambers.

**Table 4.** Eigenvalue calculation results.

| Eigenvalue Calculation Method  | $\lambda_1$ | $\lambda_1$ Proportion | $\lambda_2$ | $\lambda_2$ Proportion |
|--------------------------------|-------------|------------------------|-------------|------------------------|
| Formula calculation            | 12.3058     | 62.1078%               | 7.5078      | 37.8922%               |
| Probability box–EDF estimation | 12.8423     | 60.8148%               | 8.2748      | 39.1852%               |

# 4. Dimensionality Reduction Analysis of Combustion Chamber Structure Parameters

This paper uses peak cylinder pressure and temperature as performance indicators. With Table 5 showing the boundary conditions, the RNG K- $\epsilon$  model calculates cylinder air-flow [64–66]. The PRF skeleton mechanism with 41 components and 124 chemical reactions is combined with the SAGE chemical kinetic model for combustion calculations [67,68]. Figure 24 depicts solid model parameters [58].

**Table 5.** Rotor engine boundary conditions.

| Boundary      | Type        | Temperature (K) | Pressure (MPa) |
|---------------|-------------|-----------------|----------------|
| Inlet         | Inflow      | 300             | 0.101325       |
| Intake port   | Fixed wall  | 300             | /              |
| Outlet        | Outflow     | 570             | 0.101325       |
| Exhaust port  | Fixed wall  | 550             | /              |
| Rotor         | Moving wall | 400             | /              |
| Rotor flank 1 | Fixed wall  | 624             | 0.117210       |
| Rotor flank 2 | Fixed wall  | 600             | /              |

Grid number affects calculation results. To eliminate this influence, ensure accuracy, and select the optimal grid number to reduce computation time, grid independence analysis of the simulation model is necessary. This study compares in-cylinder pressure changes under four different grid sizes with constant boundary conditions set as shown in Table 5. Figure 25 shows pressure change curves for different grid sizes. Adaptive mesh refinement (AMR) [69–71] is applied to a 2 mm mesh, producing results consistent with a 1 mm mesh size and achieving stable calculations. Considering efficiency, accuracy, and calculation time, a 2 mm mesh is selected, resulting in approximately 200,000 hexahedral element grids,

as shown in Figure 26. The 100 parameter combinations obtained in Section 2 are calculated with performance indices (Figure 27).

![Figure 24: Three-dimensional model. (a) Cylinder fluid domain. (b) Rotor entity.](78ebfe3116918cd317b54c861da8d8d2_img.jpg)

Figure 24 consists of two 3D CAD models. (a) shows a cylinder head with a central combustion chamber and two ports. (b) shows a separate rotor component with a triangular combustion chamber and a central spark plug hole.

Figure 24: Three-dimensional model. (a) Cylinder fluid domain. (b) Rotor entity.

**Figure 24.** Three-dimensional model. (a) Cylinder fluid domain. (b) Rotor entity.

![Figure 25: Cylinder pressure change curve under different grid numbers. (a) Ignition state. (b) Non-ignition state.](93587f920736a2fdcefeba94b29f302a_img.jpg)

Figure 25 contains two line graphs. Graph (a) shows cylinder pressure (MPa) vs. crank angle (°CA) for the ignition state, with a peak pressure of approximately 3.1 MPa. Graph (b) shows the non-ignition state, with a peak pressure of approximately 1.8 MPa. Both graphs compare four grid sizes: 3 mm (solid blue), 2 mm (dashed green), 2 mm with AMR (dotted red), and 1 mm (dash-dot black). The curves are nearly identical across all grid sizes.

Figure 25: Cylinder pressure change curve under different grid numbers. (a) Ignition state. (b) Non-ignition state.

**Figure 25.** The cylinder pressure change curve under different grid numbers. (a) Ignition state. (b) Non-ignition state.

![Figure 26: Rotor engine computational grid.](67af94a7c462e85f3a310c9a45c0980d_img.jpg)

Figure 26 is a 2D cross-section of the rotor engine showing a computational grid. Labels include: Exhaust port, Intake port, Combustion chamber III, Combustion chamber II, Spark plug chamber, and Combustion chamber I. A coordinate system (x, y) and a rotation direction arrow are also shown.

Figure 26: Rotor engine computational grid.

**Figure 26.** Rotor engine computational grid.

The eigenvalue estimation method from the earlier section is applied to the generated 100-size combinations. Figures 28–37 present the EDFs obtained by fitting all 10 cognitive uncertainty variables using a probability box.

![Figure 27: Performance index. (a) Maximum cylinder pressure. (b) Maximum cylinder temperature.](96a7eac66ef72bb016c280278506ac63_img.jpg)

Figure 27 consists of two vertically stacked line plots. Plot (a) shows the maximum cylinder pressure in MPa on the y-axis (ranging from 1 to 7) against the sample number on the x-axis (ranging from 0 to 100). The data points are connected by vertical lines, showing significant fluctuations between approximately 1.5 and 7.0 MPa. Plot (b) shows the maximum cylinder temperature in Kelvin on the y-axis (ranging from 500 to 2500) against the sample number on the x-axis (ranging from 0 to 100). The data points are connected by vertical lines, showing fluctuations between approximately 1800 and 2300 K.

Figure 27: Performance index. (a) Maximum cylinder pressure. (b) Maximum cylinder temperature.

**Figure 27.** Performance index. (a) Maximum cylinder pressure. (b) Maximum cylinder temperature.

![Figure 28: EDF fitting of the arc radius r in the combustion chamber.](f85bf99d372e735d228361bf4d3cf7e6_img.jpg)

Figure 28 is a line plot showing the cumulative probability in percentage on the y-axis (ranging from 0 to 100) against the values on the x-axis (ranging from 0 to 120). The data points are connected by a smooth curve, showing a rapid increase in probability from about 18% at a value of 10 to about 95% at a value of 100.

Figure 28: EDF fitting of the arc radius r in the combustion chamber.

**Figure 28.** EDF fitting of the arc radius  $r$  in the combustion chamber.



![Figure 29: EDF fitting for the combustion chamber leading bottom length l. The graph shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 30). The data points are approximately (2, 10), (4, 25), (6, 32), (8, 48), (10, 58), (12, 68), (14, 80), (16, 85), (18, 90), (20, 93), (22, 95), (24, 96), and (26, 97).](2a77eb32ef4c4d8a5c1758a53a908336_img.jpg)

| Values | Cumulative probability/% |
|--------|--------------------------|
| 2      | 10                       |
| 4      | 25                       |
| 6      | 32                       |
| 8      | 48                       |
| 10     | 58                       |
| 12     | 68                       |
| 14     | 80                       |
| 16     | 85                       |
| 18     | 90                       |
| 20     | 93                       |
| 22     | 95                       |
| 24     | 96                       |
| 26     | 97                       |

Figure 29: EDF fitting for the combustion chamber leading bottom length l. The graph shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 30). The data points are approximately (2, 10), (4, 25), (6, 32), (8, 48), (10, 58), (12, 68), (14, 80), (16, 85), (18, 90), (20, 93), (22, 95), (24, 96), and (26, 97).

**Figure 29.** EDF fitting for the combustion chamber leading bottom length  $l$ .

![Figure 30: EDF fitting for the distance (h) between the combustion chamber bottom and the rotor's center of gravity in the x-z plane. The graph shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (46 to 70). The data points are approximately (46, 5), (48, 10), (50, 30), (52, 48), (54, 70), (56, 80), (58, 90), (60, 95), (62, 96), (64, 97), and (66, 98).](79cb7fa0e9c78ec5cd0b0de977824f8d_img.jpg)

| Values | Cumulative probability/% |
|--------|--------------------------|
| 46     | 5                        |
| 48     | 10                       |
| 50     | 30                       |
| 52     | 48                       |
| 54     | 70                       |
| 56     | 80                       |
| 58     | 90                       |
| 60     | 95                       |
| 62     | 96                       |
| 64     | 97                       |
| 66     | 98                       |

Figure 30: EDF fitting for the distance (h) between the combustion chamber bottom and the rotor's center of gravity in the x-z plane. The graph shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (46 to 70). The data points are approximately (46, 5), (48, 10), (50, 30), (52, 48), (54, 70), (56, 80), (58, 90), (60, 95), (62, 96), (64, 97), and (66, 98).

**Figure 30.** EDF fitting for the distance ( $h$ ) between the combustion chamber bottom and the rotor's center of gravity in the  $x$ - $z$  plane.

![Figure 31: EDF fitting for the angle (θ3) between the bottom edge of the combustion chamber's leading section and the y-z plane. The graph shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 12). The data points are approximately (1, 30), (2, 40), (3, 52), (4, 62), (5, 72), (6, 82), (7, 85), (8, 92), (9, 95), and (10, 98).](bd4617f25d15430eb78c2d6d75a99dde_img.jpg)

| Values | Cumulative probability/% |
|--------|--------------------------|
| 1      | 30                       |
| 2      | 40                       |
| 3      | 52                       |
| 4      | 62                       |
| 5      | 72                       |
| 6      | 82                       |
| 7      | 85                       |
| 8      | 92                       |
| 9      | 95                       |
| 10     | 98                       |

Figure 31: EDF fitting for the angle (θ3) between the bottom edge of the combustion chamber's leading section and the y-z plane. The graph shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 12). The data points are approximately (1, 30), (2, 40), (3, 52), (4, 62), (5, 72), (6, 82), (7, 85), (8, 92), (9, 95), and (10, 98).

**Figure 31.** EDF fitting for the angle ( $\theta_3$ ) between the bottom edge of the combustion chamber's leading section and the  $y$ - $z$  plane.

![Figure 32: EDF fitting of the arc radius (R) in the combustion chamber's trailing section. The plot shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 100). The data points are approximately (10, 20), (20, 45), (30, 70), (40, 78), (50, 85), (60, 88), (70, 92), (80, 94), (90, 96), and (100, 98).](9a19da4f7fccb96a934411c0bb5a386d_img.jpg)

| Values | Cumulative probability/% |
|--------|--------------------------|
| 10     | 20                       |
| 20     | 45                       |
| 30     | 70                       |
| 40     | 78                       |
| 50     | 85                       |
| 60     | 88                       |
| 70     | 92                       |
| 80     | 94                       |
| 90     | 96                       |
| 100    | 98                       |

Figure 32: EDF fitting of the arc radius (R) in the combustion chamber's trailing section. The plot shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 100). The data points are approximately (10, 20), (20, 45), (30, 70), (40, 78), (50, 85), (60, 88), (70, 92), (80, 94), (90, 96), and (100, 98).

**Figure 32.** EDF fitting of the arc radius ( $R$ ) in the combustion chamber's trailing section.

![Figure 33: EDF fitting of the trailing bottom edge length (L) of the combustion chamber. The plot shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 15). The data points are approximately (0.5, 28), (1.5, 55), (2.5, 62), (3.5, 65), (4.5, 75), (5.5, 80), (7.5, 88), (8.5, 89), (10.5, 92), (11.5, 94), and (13.5, 98).](c4c8cd9c58f395c25a2a2b217ca7c2fb_img.jpg)

| Values | Cumulative probability/% |
|--------|--------------------------|
| 0.5    | 28                       |
| 1.5    | 55                       |
| 2.5    | 62                       |
| 3.5    | 65                       |
| 4.5    | 75                       |
| 5.5    | 80                       |
| 7.5    | 88                       |
| 8.5    | 89                       |
| 10.5   | 92                       |
| 11.5   | 94                       |
| 13.5   | 98                       |

Figure 33: EDF fitting of the trailing bottom edge length (L) of the combustion chamber. The plot shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 15). The data points are approximately (0.5, 28), (1.5, 55), (2.5, 62), (3.5, 65), (4.5, 75), (5.5, 80), (7.5, 88), (8.5, 89), (10.5, 92), (11.5, 94), and (13.5, 98).

**Figure 33.** EDF fitting of the trailing bottom edge length ( $L$ ) of the combustion chamber.

![Figure 34: EDF fitting of the distance (H) from the combustion chamber's trailing bottom to the rotor's center of gravity in the x-z plane. The plot shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (40 to 54). The data points are approximately (41.5, 0), (42.5, 5), (43.5, 10), (44.5, 15), (45.5, 20), (46.5, 25), (47.5, 30), (48.5, 35), (49.5, 40), (50.5, 45), (51.5, 50), (52.5, 55), (53.5, 60), (54.5, 65), (55.5, 70), (56.5, 75), (57.5, 80), (58.5, 85), (59.5, 90), (60.5, 95), and (61.5, 100).](f630450865788387c4821c6d5760c850_img.jpg)

| Values | Cumulative probability/% |
|--------|--------------------------|
| 41.5   | 0                        |
| 42.5   | 5                        |
| 43.5   | 10                       |
| 44.5   | 15                       |
| 45.5   | 20                       |
| 46.5   | 25                       |
| 47.5   | 30                       |
| 48.5   | 35                       |
| 49.5   | 40                       |
| 50.5   | 45                       |
| 51.5   | 50                       |
| 52.5   | 55                       |
| 53.5   | 60                       |
| 54.5   | 65                       |
| 55.5   | 70                       |
| 56.5   | 75                       |
| 57.5   | 80                       |
| 58.5   | 85                       |
| 59.5   | 90                       |
| 60.5   | 95                       |
| 61.5   | 100                      |

Figure 34: EDF fitting of the distance (H) from the combustion chamber's trailing bottom to the rotor's center of gravity in the x-z plane. The plot shows cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (40 to 54). The data points are approximately (41.5, 0), (42.5, 5), (43.5, 10), (44.5, 15), (45.5, 20), (46.5, 25), (47.5, 30), (48.5, 35), (49.5, 40), (50.5, 45), (51.5, 50), (52.5, 55), (53.5, 60), (54.5, 65), (55.5, 70), (56.5, 75), (57.5, 80), (58.5, 85), (59.5, 90), (60.5, 95), and (61.5, 100).

**Figure 34.** EDF fitting of the distance ( $H$ ) from the combustion chamber's trailing bottom to the rotor's center of gravity in the  $x$ - $z$  plane.

![Figure 35: EDF fitting of the angle (θ1) between the bottom edge of the combustion chamber's middle section and the y-z plane. The plot shows a cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 18). The data points are approximately: (1, 5), (2, 10), (3, 18), (4, 25), (5, 35), (6, 45), (7, 50), (8, 58), (9, 65), (10, 70), (11, 75), (12, 78), (13, 85), (14, 90), (15, 100).](9b5411fa2d169b66f6185fbf67b49766_img.jpg)

Figure 35: EDF fitting of the angle (θ1) between the bottom edge of the combustion chamber's middle section and the y-z plane. The plot shows a cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 18). The data points are approximately: (1, 5), (2, 10), (3, 18), (4, 25), (5, 35), (6, 45), (7, 50), (8, 58), (9, 65), (10, 70), (11, 75), (12, 78), (13, 85), (14, 90), (15, 100).

**Figure 35.** EDF fitting of the angle ( $\theta_1$ ) between the bottom edge of the combustion chamber's middle section and the  $y$ - $z$  plane.

![Figure 36: EDF fitting of the angle (θ2) between the rear bottom edge of the combustion chamber and the y-z plane. The plot shows a cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 18). The data points are approximately: (1, 15), (2, 18), (3, 20), (4, 25), (5, 30), (6, 38), (7, 45), (8, 50), (9, 55), (10, 65), (11, 75), (12, 80), (13, 85), (14, 90), (15, 100).](50fecd0e7c9bf4ebf321d8367d42cc94_img.jpg)

Figure 36: EDF fitting of the angle (θ2) between the rear bottom edge of the combustion chamber and the y-z plane. The plot shows a cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (0 to 18). The data points are approximately: (1, 15), (2, 18), (3, 20), (4, 25), (5, 30), (6, 38), (7, 45), (8, 50), (9, 55), (10, 65), (11, 75), (12, 80), (13, 85), (14, 90), (15, 100).

**Figure 36.** EDF fitting of the angle ( $\theta_2$ ) between the rear bottom edge of the combustion chamber and the  $y$ - $z$  plane.

![Figure 37: EDF fitting of the distance (b) between the center of the spoiler plate top and the bottom of the combustion chamber. The plot shows a cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (45 to 52). The data points are approximately: (46, 2), (46.5, 3), (47, 3), (47.5, 4), (48, 6), (48.5, 8), (49, 12), (49.5, 18), (50, 25), (50.5, 35), (51, 55), (51.5, 100).](65a9654ccb3d0d452378b0f4c0c392f7_img.jpg)

Figure 37: EDF fitting of the distance (b) between the center of the spoiler plate top and the bottom of the combustion chamber. The plot shows a cumulative probability (%) on the y-axis (0 to 100) versus Values on the x-axis (45 to 52). The data points are approximately: (46, 2), (46.5, 3), (47, 3), (47.5, 4), (48, 6), (48.5, 8), (49, 12), (49.5, 18), (50, 25), (50.5, 35), (51, 55), (51.5, 100).

**Figure 37.** EDF fitting of the distance ( $b$ ) between the center of the spoiler plate top and the bottom of the combustion chamber.

Taking the maximum cylinder pressure, the maximum cylinder temperature, and the indicated average effective pressure as the performance indexes, the EDF and eigenvalue estimation methods of each parameter obtained above are used to calculate the eigenvalue matrix of the function composed of 14 structural parameters, including the

radius  $r$  of the front arc of the combustion chamber. The calculation results are shown in Table 6. The larger the eigenvalues in the table, the greater the impact on the corresponding performance indicators.

**Table 6.** The calculated eigenvalues.

| Structural Parameter | Performance Index         |                              |                                      |
|----------------------|---------------------------|------------------------------|--------------------------------------|
|                      | Maximum Cylinder Pressure | Maximum Cylinder Temperature | Indicated Average Effective Pressure |
| $r$                  | 2.1339                    | 3.3178                       | 2.5761                               |
| $l$                  | 3.1528                    | 4.7906                       | 1.6218                               |
| $h$                  | 4.6812                    | 6.3345                       | 3.7114                               |
| $\theta 3$           | 2.3218                    | 8.2688                       | 8.0427                               |
| $R$                  | 2.8055                    | 6.7792                       | 4.1701                               |
| $L$                  | 2.2952                    | 4.3389                       | 4.0759                               |
| $H$                  | 14.2391                   | 16.9644                      | 14.4644                              |
| $\theta 1$           | 18.1673                   | 18.1360                      | 13.5508                              |
| $\theta 2$           | 16.6057                   | 17.0970                      | 14.9315                              |
| $a$                  | 8.5642                    | 9.3406                       | 7.9712                               |
| $b$                  | 16.8614                   | 17.7883                      | 8.6039                               |
| $c$                  | 1.3363                    | 1.2064                       | 0.8551                               |
| $q1$                 | 0.5012                    | 0.7131                       | 0.5182                               |
| $q2$                 | 0.3877                    | 0.9580                       | 0.0224                               |

Figure 38 illustrates the radar plot of each structural parameter's impact on the performance index using the eigenvalue ratio. The coordinate axis indicates the influence percentage, and the larger structural parameters have a greater effect on the performance index.

From the figure, it can be seen that the effect of each structural parameter on the same performance index and that of the same structural parameter on different performance indexes is slightly different. However, whether the performance index is based on the maximum cylinder pressure, the maximum cylinder temperature, or the indicated average effective pressure, the three structural parameters that have the greatest influence on it are the angle  $\theta 2$  between the rear bottom of the combustion chamber and the Y-Z plane, the distance  $b$  between the center of the top of the turbulent blade and the bottom of the combustion chamber, and the angle  $\theta 1$  between the bottom of the middle of the combustion chamber and the Y-Z plane. The three structural parameters that have the least influence on the performance index are the spoiler width  $c$ , the radius of the excessive arc between the front of the combustion chamber and the middle of the combustion chamber  $q1$ , and the radius of the excessive arc between the middle of the combustion chamber and the rear of the combustion chamber  $q2$ . The vertical distance  $a$  between the spoiler and the rotor X-Z section and the distance  $b$  between the top center of the spoiler and the bottom edge of the combustion chamber have a greater influence on the maximum cylinder pressure and the maximum cylinder temperature but have a smaller influence on the indicated average effective pressure.

![Figure 38: Three radar charts (a, b, c) showing the impact of structural parameters on performance metrics. Each chart has axes for parameters a, b, c, q1, q2, r, H, L, and R. The radial axis is labeled from 0 to 20. Chart (a) shows maximum cylinder pressure, (b) shows peak cylinder temperature, and (c) shows indicated mean effective pressure.](5500ab73cf84ccc0055eecf28889b4db_img.jpg)

Figure 38 consists of three radar charts, labeled (a), (b), and (c), each plotting performance metrics against structural parameters. The parameters are represented by axes labeled a, b, c, q1, q2, r, H, L, and R. The radial axis for each chart is marked from 0 to 20 in increments of 2. Each chart contains a set of red data points connected by lines, forming a polygon that indicates the relative impact of each parameter.

- Chart (a):** Shows the impact of numerous structural parameters on maximum cylinder pressure. The polygon is relatively flat, indicating that many parameters have a similar impact.
- Chart (b):** Shows the effect of different structural parameters on peak cylinder temperature. The polygon is more peaked, indicating that some parameters have a significantly higher impact than others.
- Chart (c):** Shows the effect of each structural parameter on the indicated mean effective pressure. The polygon is more rounded, indicating a more balanced impact across the parameters.

Figure 38: Three radar charts (a, b, c) showing the impact of structural parameters on performance metrics. Each chart has axes for parameters a, b, c, q1, q2, r, H, L, and R. The radial axis is labeled from 0 to 20. Chart (a) shows maximum cylinder pressure, (b) shows peak cylinder temperature, and (c) shows indicated mean effective pressure.

**Figure 38.** Impact of structural parameters on various performance metrics. (a) Impact of numerous structural parameters on maximum cylinder pressure. (b) Effect of different structural parameters on peak cylinder temperature. (c) Effect of each structural parameter on the indicated mean effective pressure.

Through the above chart, the main structural parameter combination can be obtained, which is composed of the angle  $\theta 1$  between the bottom edge of the middle part of the combustion chamber and the Y-Z plane, the distance b between the center of the spoiler top and the bottom edge of the combustion chamber, the angle  $\theta 2$  between the bottom edge of the rear part of the combustion chamber and the Y-Z plane, the distance H between the bottom of the middle and rear part of the combustion chamber at the X-Z section of the rotor and the center of gravity of the rotor, the vertical distance a between the spoiler and the X-Z section of the rotor, the angle  $\theta 3$  between the bottom edge of the front part

of the combustion chamber and the Y-Z plane, the radius  $R$  of the middle and rear part of the combustion chamber, and the distance  $h$  between the bottom of the front part of the combustion chamber at the X-Z section of the rotor. The influence of this parameter combination on the maximum cylinder pressure, the maximum cylinder temperature, and the indicated average effective pressure is 89.5728%, 86.7924%, and 89.0677%, respectively. The influence of structural parameters such as the bottom edge length  $l$  of the front part of the combustion chamber, the bottom edge length  $L$  of the middle and rear part of the combustion chamber, the arc radius  $r$  of the front part of the combustion chamber, the width  $c$  of the spoiler, the excessive arc radius  $q_2$  between the middle part of the combustion chamber and the rear part of the combustion chamber, and the excessive arc radius  $q_1$  between the front part of the combustion chamber and the middle part of the combustion chamber is small and can be ignored in the study of combustion chamber structure optimization. This is consistent with the current research trend regarding the structural parameters of the combustion chamber of the rotary engine. On this basis, three structural parameters can be obtained, which are the angle  $\theta_2$  between the bottom edge of the combustion chamber and the Y-Z plane, the distance  $H$  between the bottom of the middle and rear section of the combustion chamber at the X-Z section of the rotor and the center of gravity of the rotor, and the angle  $\theta_1$  between the bottom edge of the middle of the combustion chamber and the Y-Z plane. These three structural parameters should be used as important structural parameters for the study of the combustion chamber structure of the rotary engine. These three parameters have a great influence on each performance index, and the influence on the maximum cylinder pressure, the maximum cylinder temperature, and the indicated average effective pressure are 52.1109%, 45.9847%, and 50.4569%, respectively.

Since the design of the combustion chamber structure demands a variety of requirements, including compression ratio, process, and structure, after optimizing the above structural parameters that have the greatest impact on performance, it is necessary to change some structural parameters at the same time to make them meet many requirements, including compression ratio. It can be seen from the above charts that the three structural parameters, such as the length  $l$  of the front bottom of the combustion chamber, the length  $L$  of the rear bottom of the combustion chamber, and the radius  $r$  of the front arc of the combustion chamber, have a small proportion of influence on each performance index. The influence of these three parameters on the maximum cylinder pressure, the maximum cylinder temperature, and the indicated mean effective pressure is 8.7753%, 13.7104%, and 11.5934%, respectively, and the range of parameters is large. Because the change in parameters has a great influence on the compression ratio, process, and strength requirements, the above three structural parameters can be used as adjustable structural parameters in the study of combustion chamber structure optimization. When the main structural parameters are determined, the adjustable structural parameters are adjusted to make the combustion chamber meet many requirements, including compression ratio, process, and structure.

# 5. Conclusions

In order to reduce the dimension in the optimization process of the combustion chamber structure of the rotary engine and clarify the optimization priority and direction, this paper proposes a dimension reduction method for the structural parameters of the combustion chamber of the rotary engine based on the AS, referring to the probability box and EDF. The main research contents of this paper are as follows:

1. By analyzing the generation process of the active subspace and the composition of rotor structure parameters, based on active subspace, combined with the probability box and EDF, a dimension reduction method for rotary engine combustion chamber structure parameters is proposed, and the accuracy of the method is verified. The results show that the deviation between the calculated eigenvalues and the actual eigenvalues is only 1.2931%, and the estimation accuracy is high, which can be used

- for eigenvalue calculation and parameter dimension reduction of high-dimensional mixed uncertainty problems.
2. Using the dimension reduction method proposed above, the dimension combination composed of 14 structural parameters is reduced to an important structural parameter composed of 8 structural parameters, including  $\theta 1$ ,  $b$ ,  $\theta 2$ ,  $H$ ,  $a$ ,  $\theta 3$ ,  $R$ , and  $h$ . The effects of the above eight structural parameters on the maximum cylinder pressure, the maximum cylinder temperature, and the indicated mean effective pressure are 89.5728%, 86.7924%, and 89.0677%, respectively.
  3. On this basis, three main structural parameters, with the influence of  $\theta 2$  accounting for more than 45%, are obtained. And three adjustable structural parameters, including  $l$ , are obtained. The influence of the latter on the total proportion of each performance index is small, and the influence on the maximum cylinder pressure, the maximum cylinder temperature, and the indicated average effective pressure is 8.7753%, 13.7104%, and 11.5934%, respectively. Moreover, the change in parameters has a great influence on the compression ratio, process, and strength requirements. Therefore, the above three structural parameters can be used as adjustable structural parameters in the optimization of combustion chamber structure. When the main structural parameters are determined, the adjustable structural parameters are adjusted to make the combustion chamber meet many requirements, including compression ratio, process, and structure.

In the future, based on the research in this paper, the research group will deeply study the influencing law of combustion chamber structure parameters on engine performance and quantitatively analyze it, hoping to obtain the influence proportions of different combustion chamber structure parameters and different levels of the same structure parameters on engine performance. Furthermore, the dimension reduction method based on AS proposed in this paper will be applied to the research of other structure or control parameters of rotary engines, which provides a reference and basis for further improving the performance of rotary engines and broadening the application field of rotary engines.

**Supplementary Materials:** The following supporting information can be downloaded at: <https://www.mdpi.com/article/10.3390/pr12102238/s1>, Figure S1: Sectional View of Combustion Chamber Pit; Figure S2: Schematic diagram of the segmented structure of the front, middle, and rear parts of the combustion chamber; Figure S3: Schematic diagram of segmented structure of spoiler; Figure S4: Parametric modeling flow chart; Figure S5: Macro Command; Figure S6: Ompression ratio of solid model; Figure S7: Distribution of parameters for the radius  $R$  of the rear arc in the combustion chamber and the length  $L$  of the bottom edge in the rear of the combustion chamber; Figure S8: Solid model of rotor.

**Author Contributions:** Validation, Y.S.; formal analysis, L.L.; investigation, Y.T. and W.L.; resources, R.Z. All authors have read and agreed to the published version of the manuscript.

**Funding:** This work was supported by the Postdoctoral Fellowship Program of CPSF under Grant Number (GZC20241576) and the Applied Basic Research Programs of Shanxi Province in China (202403021212341, 202203021222038, 202203021222045).

**Data Availability Statement:** The original contributions presented in the study are included in the article/Supplementary Materials, further inquiries can be directed to the corresponding author.

**Conflicts of Interest:** The authors declare no conflict of interest.

# References

1. Wang, S. The Status of the Power Plants for UAVs in China. *Aerosp. Power* **2019**, *2*, 9–12.
2. Dong, Y.; Huang, M.; Li, R. Overview of the Development of General Aviation Engines. *J. Xi'an Aeronaut. Univ.* **2017**, *35*, 8–13.
3. Yin, Z.; Li, S.; Li, G. Current State and Development of the Unmanned Aerial Vehicle Power plant. *Aeroengine* **2007**, *33*, 10–15.
4. Lu, D.; Zheng, J.; Hu, C.; Bian, S. Research on the development status of general aviation piston engine. *Intern. Combust. Engine Parts* **2019**, *8*, 64–66.
5. Feng, G.; Zhou, M. Assessment of heavy fuel aircraft piston engine type. *J. Tsinghua Univ.* **2016**, *56*, 1114–1121.

6. Jiao, H.; Liu, J.; Zou, R.; Wang, N. Combined influence of ignition chamber volume and spark plug channel diameter on the performance of small-scale natural gas Wankel rotary engine. *Eng. Appl. Comput. Fluid Mech.* **2021**, *15*, 1775–1791. [\[CrossRef\]](#)
7. Kong, X.; Liu, H. Research Progress of Key Technologies of Aviation Piston Engine for UAV. *Small Intern. Combust. Engine Veh. Tech.* **2021**, *50*, 79–87.
8. Johar, T.; Hsieh, C.F. Design Challenges in Hydrogen-Fueled Rotary Engine-A Review. *Emergies* **2023**, *16*, 607. [\[CrossRef\]](#)
9. Wu, S. Research on Technical Characteristics and Application of Unmanned Aerial Vehicle Power Unit. *Shanghai Energy Sav.* **2022**, 1536–1540.
10. Wang, X.; Liu, J. GE Aerospace's Roadmap for Next-Generation Aerospace Power Technology. *Aerosp. Power* **2023**, 24–27.
11. Li, H.; Sun, F. The Application Development and Key Technologies of Wankel engine. *Small Intern. Combust. Engine Veh.* **2023**, *52*, 68–74.
12. Kotsiopoulos, P.; Yfantis, E.; Lois, E.; Hountalas, D. Diesel and JP-8 fuel performance on a Petter AVI diesel engine. In Proceedings of the 39th Aerospace Sciences Meeting and Exhibit (AIAA), Reno, NV, USA, 8–11 January 2001. [\[CrossRef\]](#)
13. Dutczaak, J. Heavy fuel engines. *Combust. Engines* **2015**, *163*, 34–46. [\[CrossRef\]](#)
14. Wu, H.; Wang, L.L.; Wu, Y.; Sun, B.; Zhao, Z.; Liu, F. Spray performance of air-assisted kerosene injection in a constant volume chamber under various in-cylinder GDI engine conditions. *Appl. Therm. Eng.* **2019**, *150*, 762–769. [\[CrossRef\]](#)
15. Li, Z. Simulation Analysis on Cooperative Control of Ignition and Knock of Light-Weight, Spark Ignition, Heavy Oil Aeroengine. Master's Thesis, Beijing Jiao Tong University, Beijing, China, 2016.
16. Wang, Z. Experimental Study on Performance of 15kW Two-Stroke Ignited PFI Kerosene Piston Engine. Master's Thesis, Nanjing University of Aeronautics and Astronautics, Nanjing, China, 2018.
17. Attard, W.P.; Blaxill, H.; Anderson, E.K.; Litke, P. Knock limit extension with a gasoline fueled pre -chamber jet igniter in a modern vehicle powertrain. *SAE Int. J. Engines* **2012**, *5*, 1201–1215. [\[CrossRef\]](#)
18. Wang, C.Y.; Zhang, F.J.; Wang, E.H.; Yu, C.; Gao, H.; Liu, B.; Zhao, Z.; Zhao, C. Experimental study on knock suppression of spark -ignition engine fueled with kerosene via water injection. *Appl. Energy* **2019**, *242*, 248–259. [\[CrossRef\]](#)
19. Chen, L.F.; Raza, M.; Xiao, J.H. Combustion analysis of an aviation compression ignition engine burning pentanol kerosene blends under different injection timings. *Energy Fuel* **2017**, *31*, 9429–9437. [\[CrossRef\]](#)
20. Ning, L.; Duan, Q.M.; Wei, Y.H.; Zhang, X.; Yu, K.; Yang, B.; Zeng, K. Effects of injection timing and compression ratio on the combustion performance and emissions of a two -stroke DISI engine fuelled with aviation kerosene. *Appl. Therm. Eng.* **2019**, *161*, 114–124.
21. Lu, Y.; Pan, J.F.; Fan, B.W.; Otchere, P.; Chen, W.; Cheng, B. Research on the application of aviation kerosene in a direct injection wankel engine -Part 1: Fundamental spray characteristics and optimized injection strategies. *Energy Convers. Manag.* **2019**, *195*, 519–532. [\[CrossRef\]](#)
22. Yang, J.; Ji, C.; Wang, S.; Wang, D.; Ma, Z.; Zhang, B. Numerical investigation on the mixture formation and combustion processes of a gasoline wankel engine with direct injected hydrogen enrichment. *Appl. Energy* **2018**, *224*, 34–41. [\[CrossRef\]](#)
23. Cao, B.W.; Liu, J.X. Design and optimization of orifice plates in the air-assisted kerosene injection system applied in the wankel rotary engine. *Proc. Inst. Mech. Eng. Part C-J. Mech. Eng. Sci.* **2023**, *237*, 2945–2953. [\[CrossRef\]](#)
24. Zhao, Y.; Deng, X.; Feng, Z.; Zhu, R.; Su, X. Effects of Combustion Chamber Pit Shape on Combustion Process for Gasoline Wankel engine. *Veh. Engine* **2022**, *40*–46.
25. Kuo, C.H.; Ma, H.L.; Chen, C.C. Chamber contour design and compression flow calculations of wankel engine. *J. CCIT* **2010**, *39*, 35–50.
26. Tartakovsky, L.; Baibikov, V.; Gutman, M.; Veinblat, M.; Reif, J. Simulation of Wankel engine performance using commercial software for piston engines. In Proceedings of the 2012 Small Engine Technology Conference & Exhibition, Madison, WI, USA, 16–18 October 2012. SAE Technical Paper 2012–32-0098.
27. Jeng, D.Z.; Hsieh, M.J.; Lee, C.C.; Han, Y. The numerical investigation on the performance of wankel engine with leakage, different fuels and recess sizes. In Proceedings of the JSAE/SAE 2013 Small Engine Technology Conference, Taipei, Taiwan, 8–10 October 2013. SAE Technical Paper 2013–32-9160.
28. Wei, F.B.; Feng, P.J.; Xian, L.Y.; Rui, C.; Di, W.U. Effect of pocket location on combustion process in natural gas-fueled wankel engine. *Appl. Mech. Mater.* **2013**, *316*–317, 73–79. [\[CrossRef\]](#)
29. Fan, B.W.; Pan, J.F.; Pan, Z.H.; Tang, A.K.; Zhu, Y.J.; Xue, H. Effects of pocket shape and ignition slot locations on the combustion processes of a wankel engine fueled with natural gas. *Appl. Therm. Eng.* **2015**, *89*, 11–27. [\[CrossRef\]](#)
30. Ji, C.W.; Su, T.; Zhang, S.F.; Yu, M.; Cong, X. Effect of hydrogen addition on combustion and emissions performance of a gasoline wankel engine at part load and stoichiometric conditions. *Energy Convers. Manag.* **2016**, *121*, 272–280. [\[CrossRef\]](#)
31. Amrouche, F.; Varnhagen, S.; Erickson, P.A.; Park, J. An experimental study of a hydrogen-enriched ethanol fueled Wankel wankel engine at ultra lean and full load conditions. *Energy Convers. Manag.* **2016**, *123*, 174–184. [\[CrossRef\]](#)
32. Su, T.; Ji, C.; Wang, S.; Shi, L.; Cong, X. Effect of ignition timing on performance if a hydrogen-enriched n-butanol wankel engine at lean condition. *Energy Convers. Manag.* **2018**, *161*, 27–34. [\[CrossRef\]](#)
33. Chen, W.; Pan, J.; Fan, B.; Liu, Y.; Peter, O. Effect of injection strategy on fuel-air mixing and combustion process in a direct injection diesel wankel engine (DI-DRE). *Energy Convers. Manag.* **2017**, *154*, 68–80. [\[CrossRef\]](#)
34. Shi, C.; Zhang, P.; Ji, C. Understanding the role of turbulence-induced blade configuration in improving combustion process for hydrogen-enriched wankel engine. *Fuel* **2022**, *319*, 123807. [\[CrossRef\]](#)

35. Bienner, A.; Gloerfelt, X.; Cinnella, P. Leading-Edge Effects on Freestream Turbulence Induced Transition of an Organic Vapor. *Flow Turbul. Combust.* **2024**, *224*, 345–373. [\[CrossRef\]](#)
36. Li, M.; Hamel, J.; Azarm, S. Optimal uncertainty reduction for multi-disciplinary multi-output systems using sensitivity analysis. *Struct. Multidiscip. Optim.* **2010**, *40*, 77–96. [\[CrossRef\]](#)
37. Davey, K.; Sadeghi, H.; Darvizeh, R. The theory of scaling. *Contin. Mech. Thermodyn.* **2023**, *35*, 471–496. [\[CrossRef\]](#)
38. Jolliffe, I. *Principal Component Analysis*; Wiley Online Library: Hoboken, NJ, USA, 2002.
39. Duda, R.O.; Hart, P.E.; Stork, D.G. *Pattern Classification*; John Wiley & Sons: Hoboken, NJ, USA, 2012.
40. Wang, J. *Geometric Structure of High-Dimensional Data and Dimensionality Reduction*; Springer: Berlin/Heidelberg, Germany, 2012.
41. Schölkopf, B.; Smola, A.; Müller, K.-R. Nonlinear component analysis as a kernel eigenvalue problem. *Neural Comput.* **1998**, *10*, 1299–1319. [\[CrossRef\]](#)
42. Roweis, S.T.; Saul, L.K. Nonlinear dimensionality reduction by locally linear embedding. *Science* **2000**, *290*, 2323–2326. [\[CrossRef\]](#)
43. Donoho, D.L.; Grimes, C. Hessian eigenmaps: Locally linear embedding techniques for high-dimensional data. *Proc. Natl. Acad. Sci. USA* **2003**, *100*, 5591–5596. [\[CrossRef\]](#)
44. Belkin, M.; Niyogi, P. Laplacian Eigenmaps for Dimensionality Reduction and Data Representation. *Neural Comput.* **2003**, *15*, 1373–1396. [\[CrossRef\]](#)
45. Constantine, P.G. *Active Subspaces: Emerging Ideas for Dimension Reduction in Parameter Studies*; SIAM: Philadelphia, PA, USA, 2015.
46. Scott, D.W. The Curse of Dimensionality and Dimension Reduction. In *Multivariate Density Estimation*; Wiley: Hoboken, NJ, USA, 2008.
47. Wang, B.X.; Huang, X.Z.; Chang, M.X. Regional reliability sensitivity analysis based on dimension reduction technique. *Probabilistic Eng. Mech.* **2023**, *74*, 1394–1419. [\[CrossRef\]](#)
48. Russi, T.M. Uncertainty Quantification with Experimental Data and Complex System Models. Ph.D. Thesis, University of California, Berkeley, CA, USA, 2010.
49. Stewart, G.W. Error and perturbation bounds for subspaces associated with certain eigenvalue problems. *SIAM Rev.* **1973**, *15*, 727–764. [\[CrossRef\]](#)
50. Davey, K.; Abd Malek, M.I.; Ali, Z.; Sadeghi, H.; Darvizeh, R. The theory of scaled electromechanics. *Int. J. Eng. Sci.* **2024**, *203*, 1041–1068. [\[CrossRef\]](#)
51. Fujimori, K.; Goto, Y.; Liu, Y.; Taniguchi, M. Sparse principal component analysis for high-dimensional stationary time series. *Scand. J. Stat.* **2023**, *50*, 1953–1983. [\[CrossRef\]](#)
52. Wang, M.; Lu, Y.; Pan, W. An improved pattern-based prediction model for a class of industrial processes. *Trans. Inst. Meas. Control.* **2022**, *44*, 1410–1423. [\[CrossRef\]](#)
53. Chib, S.; Greenberg, E. Understanding the metropolis-hastings algorithm. *Am. Stat.* **1995**, *49*, 327–335. [\[CrossRef\]](#)
54. Ray, T. Golinski's speed reducer problem revisited. *AIAA J.* **2003**, *41*, 556–558. [\[CrossRef\]](#)
55. Allen, M.; Maute, K. Reliability-based design optimization of aeroelastic structures. *Struct. And. Multidiscip. Optim.* **2004**, *27*, 228–242. [\[CrossRef\]](#)
56. Lillacci, G.; Khramash, M. A distribution-matching method for parameter estimation and model selection in computational biology. *Int. J. Robust Nonlinear Control* **2012**, *22*, 1065–1081. [\[CrossRef\]](#)
57. Seshadri, P.; Constantine, P.; Iaccarino, G.; Parks, G. Aggressive design: A density-matching approach for optimization under uncertainty. *arXiv* **2014**, arXiv:1409.7089.
58. Ferson, S.; Kreinovich, V.; Ginzburg, L.; Myers, D.S.; Sentz, K. *Constructing Probability Boxes and Dempster-Shafer Structures*; SAND2003-4015; Sandia National Laboratories: Albuquerque, NM, USA, 2003.
59. Yang, X. Research on Highly Efficient and Precise Methods for Reliability Analysis with Epistemic Uncertainties. Master's Thesis, Northwestern Polytechnical University, Xi'an, China, 2016.
60. Huang, X.; Wang, Q.; Ding, J. Faculty of Information Engineering and Automation: Index Uncertainty Modeling in Grid Planning Based on Probability Box Theory. *Inf. Control* **2016**, *45*, 272–277.
61. Ferson, S.; Tucker, W.T. *Sensitivity in Risk Analyses with Uncertain Numbers*; Sandia National Laboratories: Albuquerque, NM, USA, 2006; pp. 156–159.
62. Crespo, L.G.; Kenny, S.P.; Giesy, D.P. Reliability analysis of polynomial systems subject to p-box uncertainties. *Mech. Syst. Signal Process.* **2013**, *37*, 121–136. [\[CrossRef\]](#)
63. Beer, M.; Ferson, S.; Kreinovich, V. Imprecise probabilities in engineering analyses. *Mech. Syst. Signal Process.* **2013**, *37*, 4–29. [\[CrossRef\]](#)
64. Jiao, H.; Ye, X.; Zou, R.; Wang, N.; Liu, J. Comparative study on ignition and combustion between conventional spark-ignition method and near-wall surface ignition method for small-scale Wankel rotary engine. *Energy* **2022**, *255*, 1049–1072. [\[CrossRef\]](#)
65. Zou, R.; Liu, J.; Jiao, H.; Zhao, J.; Wang, N. Combined effect of intake angle and chamber structure on flow field and combustion process in a small-scaled rotary engine. *Appl. Therm. Eng.* **2022**, *203*, 1497–1521. [\[CrossRef\]](#)
66. Hege, J. *The Wankel Wankel Engine: A History*; McFarland and Company Inc.: Jefferson, NC, USA, 2006.
67. Władysław, M. Modelling and Simulation of Working Processes in Wankel Engine with Direct Hydrogen Injection System. *Combust. Engines* **2015**, *161*, 42–52.
68. Peden, M. Study of Direct Injection Limitations on a Wankel Engine. Master's Thesis, University of Bath, Bath, UK, 2017.
69. Wendeker, M.; Grabowski, L.; Pietrykowski, K.; Margryta, P. *Phenomenological Model of a Wankel Engine*; Lublin University of Technology: Lublin, Poland, 2012.

70. Tomlinson, A. Modelling of Wankel Engine Performance in Commercial Piston Engine Software. Master's Thesis, University of Bath, Bath, UK, 2016.
71. Georgios, Z. Mathematical and Numerical Modelling of Flow and Combustion Processes in a Spark Ignition Engine. Master's Thesis, Department of Applied Mathematics, University of Wisconsin, Madison, WI, USA, 2005.

**Disclaimer/Publisher's Note:** The statements, opinions and data contained in all publications are solely those of the individual author(s) and contributor(s) and not of MDPI and/or the editor(s). MDPI and/or the editor(s) disclaim responsibility for any injury to people or property resulting from any ideas, methods, instructions or products referred to in the content.