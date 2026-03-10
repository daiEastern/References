

![Cover of the Journal of Hohai University (Natural Sciences)](2dfa6ac3edfe874f68aa0cbccaa42322_img.jpg)

Cover of the Journal of Hohai University (Natural Sciences)

河海大学学报(自然科学版)  
*Journal of Hohai University(Natural Sciences)*  
ISSN 1000-1980,CN 32-1117/TV

# 《河海大学学报(自然科学版)》网络首发论文

题目: 考虑物理约束的 LSTM 在多要素洪水模拟中的应用  
作者: 何畅, 李致家, 牛颢然, 梁世强, 李京兵  
网络首发日期: 2025-09-01  
引用格式: 何畅, 李致家, 牛颢然, 梁世强, 李京兵. 考虑物理约束的 LSTM 在多要素洪水模拟中的应用[J/OL]. 河海大学学报(自然科学版).  
<https://link.cnki.net/urlid/32.1117.tv.20250829.1443.014>

![QR code linking to the article](5fb340ad68b0c71df0b56698b137e35b_img.jpg)

QR code linking to the article

![CNKI logo](390120de4fe440c42fea8154fcaad334_img.jpg)

CNKI logo

**网络首发:** 在编辑部工作流程中, 稿件从录用到出版要经历录用定稿、排版定稿、整期汇编定稿等阶段。录用定稿指内容已经确定, 且通过同行评议、主编终审同意刊用的稿件。排版定稿指录用定稿按照期刊特定版式(包括网络呈现版式)排版后的稿件, 可暂不确定出版年、卷、期和页码。整期汇编定稿指出版年、卷、期、页码均已确定的印刷或数字出版的整期汇编稿件。录用定稿网络首发稿件内容必须符合《出版管理条例》和《期刊出版管理规定》的有关规定; 学术研究成果具有创新性、科学性和先进性, 符合编辑部对刊文的录用要求, 不存在学术不端行为及其他侵权行为; 稿件内容应基本符合国家有关书刊编辑、出版的技术标准, 正确使用和统一规范语言文字、符号、数字、外文字母、法定计量单位及地图标注等。为确保录用定稿网络首发的严肃性, 录用定稿一经发布, 不得修改论文题目、作者、机构名称和学术内容, 只可基于编辑规范进行少量文字的修改。

**出版确认:** 纸质期刊编辑部通过与《中国学术期刊(光盘版)》电子杂志社有限公司签约, 在《中国学术期刊(网络版)》出版传播平台上创办与纸质期刊内容一致的网络版, 以单篇或整期出版形式, 在印刷出版之前刊发论文的录用定稿、排版定稿、整期汇编定稿。因为《中国学术期刊(网络版)》是国家新闻出版广电总局批准的网络连续型出版物 (ISSN 2096-4188, CN 11-6037/Z), 所以签约期刊的网络版上网络首发论文视为正式出版。

# 考虑物理约束的 LSTM 在多要素洪水模拟中的应用

何畅<sup>1</sup>, 李致家<sup>1</sup>, 牛顥然<sup>1</sup>, 梁世强<sup>2</sup>, 李京兵<sup>3</sup>

(1.河海大学水文与水资源学院, 江苏 南京 210098; 2.北京市水文总站, 北京 100089;

3.安徽省水文局, 安徽 合肥 230022)

**摘要:** 针对用数据驱动模型替代传统水动力模型实现快速预报时, 存在的模拟结果单一与缺乏可解释性问题, 基于多任务学习框架, 构建了一种用于多要素联合模拟的 LSTM 模型, 同时将要素间的拟合物理关系作为约束项加入损失函数。而后, 结合随机森林 (Random Forest, RF)、斯皮尔曼秩相关系数法与 PCA 主成分分析法的特征综合评价结果, 进一步探讨模型可解释性的问题。算例基于二维水动力数值模型对研究区 17 场洪水过程模拟结果的数据库, 分别训练添加物理约束前后的 LSTM 模型, 并对比其模拟效果。研究结果表明: 添加物理约束的 LSTM 相比传统的 LSTM, 运算速度并未显著降低, 能够在 1s 内实现多要素的模拟; 对于多场洪水的整体模拟, 添加物理约束的 LSTM 效果更优, 水位、流量、流速和淹没面积的模拟精度分别提升了 20.38%、17.03%、4.02%、14.07%; 以 2015080908 号场次洪水为例, 各要素模拟精度的平均提升比率达 25.29%。总体而言, 约束后 LSTM 模型对小洪水的捕捉能力更强、对常规洪水的模拟精度较高, 但在极端复杂情况下性能仍需提升。

**关键词:** 二维水动力模型; 物理约束; LSTM 模型; 多要素模拟; 快速模拟; 城市洪水

**中图分类号:** TV122+.2

**文献标识码:** A

## Application of LSTM with physical constraints in multi-element flood simulation

He Chang<sup>1</sup>, Li Zhijia<sup>1</sup>, Niu Haoran<sup>1</sup>, Liang Shiqiang<sup>2</sup>, Li Jingbing<sup>3</sup>

(1. College of Hydrology and Water Resources, Hohai University, Nanjing 210098, China;

2. Beijing Hydrological Station, Beijing 100089, China; 3. Anhui Provincial Hydrological Bureau, Hefei 230022, China)

**Abstract:** Aiming at the problem of single simulation results and lack of interpretability when replacing the traditional hydrodynamic model with a data-driven model to achieve fast forecasting, an LSTM model for multi-factor simulation is constructed based on the multi-task learning framework, and the fitted physical relationship between the factors is added into the loss function as a constraint term. Next, by combining the comprehensive feature evaluation results of Random Forest (RF), Spearman's rank correlation coefficient method, and Principal Component Analysis (PCA), we further explore the interpretability of the model. Based on the database of simulation results of 17 flooding processes in the study area from a 2D numerical hydrodynamic model, the examples train the LSTM model before and after adding physical constraints, and compare the simulation effects. The results show that: the LSTM with added physical constraints does not significantly reduce the operation speed compared with the traditional LSTM, and can realize the simulation of multiple elements within 1s; for the overall simulation of multiple floods, the LSTM with added physical constraints is more effective, and the simulation accuracies of the water level, flow rate, flow velocity, and inundation area are improved by 20.38%, 17.03%, 4.02%, respectively, 14.07%; the average enhancement ratio of the simulation accuracy of each element reaches 25.29% in the case of field flood 2015080908. Overall, the constrained LSTM model is more capable of capturing small floods and has higher simulation accuracy for regular floods, but the performance still needs to be improved in extreme complex situations.

**Key words:** Two-dimensional hydrodynamic model; Physical constraints; LSTM; Multi factor simulation; Rapid simulation; Urban floods

**基金项目:** 国家自然科学基金项目 (52079035); 中央高校基本科研业务费项目 (B240203007); 安徽省自然科学基金重点项目 (2208085US06)

**作者简介:** 何畅 (2001—), 女, 硕士研究生, 主要从事水文物理规律模拟及水文预报研究。E-mail: 15110551182@163.com

**通信作者:** 李致家 (1962—), 男, 教授, 博士, 主要从事水文模型与水文预报研究。E-mail: zjl@hhu.edu.cn

受全球气候变化影响,近年我国极端强降水事件频发,呈增多趋势,气候风险指数呈升高趋势<sup>[1]</sup>。与此同时,随着京津冀、长三角、粤港澳、成渝、长江中游等城市群的不断发展,我国城镇化率快速提升,对城市防洪排涝体系建设提出了更高要求。2021年,郑州市遭遇历史罕见“7·20”特大暴雨;2023年7月底8月初,受台风“杜苏芮”影响,京津冀等地遭遇严重洪涝灾害,均凸显了极端天气事件对城市安全构成的重大威胁,也进一步强调了加强城市防洪排涝能力建设的紧迫性。提升城市洪水预报技术不仅关乎城市防洪排涝系统的完善,更是有效精准防控城市极端暴雨洪水、实现高质量发展和高水平安全良性互动的重要基石和必要保障<sup>[2]</sup>。

随着数值模拟技术的发展,一二维水动力模型因能准确地反映出建筑物周围的积水情况以及水流绕过建筑物的具体路径,在城市洪水预报中得到了广泛应用。众多研究表明,一二维耦合的水动力模型在提高洪灾预警的准确性方面具有显著优势<sup>[3-6]</sup>。但其伴随的更精细的网格划分与更为频繁的数据交互无疑给模型的计算带来了更大的负担。即使借助了GPU等高性能加速技术,对于一场降雨事件的完整模拟仍需耗费数小时的时间,这一时间成本对于防洪预报的时效性要求构成了严峻挑战。

随着多学科交叉研究的深入,专家学者们转向构建具有强大数据分析能力的人工智能替代模型,来提升洪水模拟的速度。但同时,受限于洪泛区内匮乏的逐时段实测数据,替代模型通常需要依赖水动力模型的模拟结果,通过学习其输入与输出数据间的关系<sup>[7]</sup>,实现快速预报。在众多机器学习模型中,卷积神经网络(CNN)<sup>[8]</sup>虽在图像等二维结构数据处理上表现出色,却难以捕捉洪水数据这类序列中的长期依赖关系,且对输入数据位置变化敏感;生成对抗网络(GAN)<sup>[9]</sup>训练过程不稳定,易出现模式崩溃等问题,在洪水模拟所需的精准数据生成上存在挑战。长短记忆神经网络(LSTM)相关研究论文的引用量曾登顶20世纪人工智能领域高引论文的榜首<sup>[10]</sup>。又因其擅长处理时序数据中的长期依赖关系,而被广泛应用于水文要素预报领域<sup>[11-13]</sup>,能有效克服其他模型在洪水模拟数据处理时面临的困境,成为洪水模拟研究中的有力工具。

值得注意的是,多数深度学习模型以数据拟合精度为核心优化目标,常忽略水文水力学基本规律,因此主动引入物理约束十分必要。对此,Fang Yang等<sup>[14]</sup>基于水动力模型生成的城市洪水淹没数据,以及水文站实时水位数据构建的初始条件,开发了一个深度学习模型。该模型能充分考虑洪水淹没的物理机制与输入、输出特征属性,具有较高的鲁棒性。然而,现有的相关研究一方面更倾向于模拟单一洪峰,或者模拟淹没水深的时间序列,难以完整地反映实际情况;另一方面,机器学习本质上属于“黑箱”模型,其决策过程难以直观理解,其预测结果也缺乏明确的物理意义和可解释性。有学者尝试通过降阶近似、归因于输入、发掘内部特征等方法<sup>[15-17]</sup>,分析模型的内部机理以解决这一问题。Kratzert F和Wojciech Samek等<sup>[18-20]</sup>少数学者更是将这种思想沿用到了洪水预报的算法分析中。至此,机器学习模型开始被视作“灰箱”模型<sup>[21]</sup>,针对模型可解释性继续开展研究日渐成为提高其普适性与接受度的重要方向。

基于上述现状,为尽可能在提升计算效率与维持模型可信度之间寻求平衡,本研究仅针对水文-一二维水动力的耦合模型中,对城市复杂地形的洪水模拟效用更好、计算更缓慢的二维水动力模块<sup>[22][23]</sup>搭建LSTM替代模型。首先,在研究区拟选取典型断面,基于二维模拟的次洪数据,以LSTM为主体,嵌入多任务学习模块,搭建多要素的模拟模型。鉴于各要素之间存在客观的物理联系,因此将该联系作为反向约束嵌入模型,使得模拟结果不仅符合数据拟合的要求,还遵循物理规律。

## 1 研究区域与数据

### 1.1 研究区域概况

屯溪区地处皖南山区边缘、位于屯溪流域下游,是安徽省黄山市的中心城区,总面积191 km<sup>2</sup>。该区属亚热带季风气候,雨量丰沛,年降水量约1670 mm。区内河流总长度126.16 km,分布密度为0.8 km/km<sup>2</sup>。河网水系复杂,横江、率水分别由西北、西南入境,受盆地地势影响,由四周丘陵向盆地平原汇集,于镇海桥下汇合为新安江,途中佩琅河汇入,最终在王村出境。二维模型以城市基础

设施分布与居民生活的密集区域（如图 1）为建模范围，计算域边界选取基于实际地形高点或密集建筑群等城市不透水边界。此类条件下，边界外降雨形成的地表径流因地形阻隔无法直接进入计算域，地下渗流也因人工构筑物拦截而通量极小，可近似视为“无水量交换”。并经 50~100 年一遇的洪水过程粗略模拟，确保拟定边界处未发生水量交换，证实了该方案的可行性。

![Figure 1: Schematic of the study area. The left map shows the study area location with a red box highlighting the Tuen Mun River area. The right map is an inset showing the detailed river network and study area boundary. The inset includes labels for the Tuen Mun River, Shing Mun River, Pui Ling River, and Wang Tsui Water Gauge Station. It also shows the calculation section, triangular grid, Tuen Mun Water Gauge Station, Section 20, and the boundary section.](e94f3bbb6f7501b9a1344dd0210e5dd8_img.jpg)

Figure 1: Schematic of the study area. The left map shows the study area location with a red box highlighting the Tuen Mun River area. The right map is an inset showing the detailed river network and study area boundary. The inset includes labels for the Tuen Mun River, Shing Mun River, Pui Ling River, and Wang Tsui Water Gauge Station. It also shows the calculation section, triangular grid, Tuen Mun Water Gauge Station, Section 20, and the boundary section.

图 1 研究区域示意图

Fig. 1 Schematic of the study area

### 1.2 数据资料

为确保所选次洪在洪峰、历时以及峰形分布等方面具备显著代表性，能够涵盖大、中、小不同洪量级，同时囊括陡涨陡落与缓涨缓落、单峰与多峰洪水等多种特性，研究选用 2008 年至 2020 年共 17 场历史洪水数据开展模拟分析。具体包括横江、率水、佩琅河的上游流量边界、王村水位站的下游水位边界与屯溪水文站的时段降雨过程等。基于屯溪流域站点实测的降雨径流数据，率定栅格新安江模型<sup>[24]</sup>参数，再依此确定上边界对应计算网格的流量过程；下边界水位则需在获取流量过程的基础上，根据站点实测的  $Z-Q$  曲线得出。拟选取屯溪城区市政中心处一重要断面（断面 20）作为研究断面，依据二维水动力模型的模拟结果，形成支撑数据驱动模型运作的数据集。其中，将 2008 年~2014 年共 13 场洪水资料作为训练-验证集以训练模型，2015 年~2020 年的 4 场洪水资料作为测试集以验证模拟结果。

![Figure 2: Generalized map of the river channel in the Tuen Mun River urban area. The map shows the river network with labels for the Tuen Mun River, Shing Mun River, Pui Ling River, and Wang Tsui Water Gauge Station. The study area is outlined in green.](954ff3c220707f98bcb2c4b197bd7d9f_img.jpg)

Figure 2: Generalized map of the river channel in the Tuen Mun River urban area. The map shows the river network with labels for the Tuen Mun River, Shing Mun River, Pui Ling River, and Wang Tsui Water Gauge Station. The study area is outlined in green.

图 2 屯溪城区河道概化图

Fig. 2 Generalized map of the river channel in the Tuen Mun River urban area

## 2 研究方案

### 2.1 二维水动力模型

二维水动力模拟模型的控制方程采用浅水方程<sup>[25]</sup>，其矢量表达形式为：

$$\partial U / \partial t + \partial F(U) / \partial x + \partial G(U) / \partial y = S \quad (1)$$

$$U = [h \quad hu \quad hv]^T \quad F(U) = [hu \quad hu^2 + gh^2 / 2 \quad huv]^T ; \quad (2)$$

$$G(U) = [hv \quad huv \quad hv^2 + gh^2/2]^T;$$

$$S = [q \quad gh(S_{0x} - S_{fx}) + qu \quad gh(S_{0y} - S_{fy}) + qv]^T$$

式中:  $U$  是守恒向量, 包括水深  $h$  与  $x$ 、 $y$  方向的流速分量  $u$ 、 $v$ ;  $F$  和  $G$  是通量向量;  $g$  是重力加速度;  $S$  是源项向量;  $S_{0x}$  和  $S_{fx}$  是  $x$  方向的水底坡降和阻力坡降;  $S_{0y}$  和  $S_{fy}$  是  $y$  方向的水底坡降和阻力坡降;  $q$  是单位时间净雨深。

本文采用非结构化网格有限体积法离散二维浅水方程, 并将占地面积约  $20\text{km}^2$  的屯溪区沿河部分城区作为重点模拟区域, 划分成边长为  $100\text{m}$  左右的  $2459$  个三角网格<sup>[26]</sup>。网格糙率值依据 2015 年中国年度土地覆盖数据集 (CLCD) 的土地覆盖类型信息, 按表 1 规则赋值。研究聚焦于短期暴雨积水情况, 不考虑渗透因素。鉴于模拟区域面积较小, 研究采用屯溪站降雨数据作为全区域输入, 得到的网格面雨量即  $q$ 。

表 1 土地覆盖类型及糙率

Table 1 Land cover type and roughness

| 土地利用类型 | 农田   | 森林  | 灌木  | 草地   | 水面    | 裸地   | 不透水层  |
|--------|------|-----|-----|------|-------|------|-------|
| 糙率     | 0.08 | 0.8 | 0.4 | 0.05 | 0.025 | 0.04 | 0.025 |

在进行离散的数值计算时, 对于每个控制体  $V$ , 在时间  $[t^n, t^{n+1}]$  上对式 (1) 积分得:

$$\int_V (\partial U / \partial t + \partial F(U) / \partial x + \partial G(U) / \partial y) dV = \int_V A dV \quad (3)$$

根据高斯散度定理, 将通量向量的偏导数转化为控制体积边界上的通量积分, 有  $\int_V \partial F(U) / \partial x dV = \oint_A F(U) \cdot \vec{n}_x dA$ ,  $\int_V \partial G(U) / \partial y dV = \oint_A G(U) \cdot \vec{n}_y dA$ , 其中  $A$  是控制体积的表面,  $\vec{n}_x$  和  $\vec{n}_y$  分别是  $x$  和  $y$  的单位外法向量。

整理式 (3) 得:

$$\int_V \partial U / \partial t dV + \oint_A F(U) \cdot \vec{n}_x dS + \oint_A G(U) \cdot \vec{n}_y dA = \int_V A dV \quad (4)$$

本模型选用 Osher 黎曼近似解<sup>[27]</sup>, 用于计算跨单元的水量、动量的法向数值通量。并结合通量的坐标旋转不变性, 在每个控制体积内, 将二维问题转化为一维问题求解。

### 2.2 搭建多要素模拟的 LSTM 模型

#### 2.2.1 LSTM 模型及参数设定

长短期记忆神经网络 (LSTM) 作为一种由循环神经网络发展而来的具备特殊门结构的模型, 较 RNN 能更好地处理序列数据中的长期依赖关系<sup>[28]</sup>。LSTM 引入了遗忘门  $f_t$ 、输入门  $i_t$ 、输出门  $o_t$  和一个细胞状态  $c_t$ , 工作架构如图 3。  $x_t$  表示输入的信息,  $h_{t-1}$  是基于  $c_{t-1}$  得到的隐藏状态。模型运作时, 原有的记忆先经过遗忘门被部分丢弃, 接着遗留的原始记忆和  $x_t$  经过输入门更新后产生的记忆相加, 形成新的记忆状态。最后, 模型在此记忆状态下完成模拟, 并依据结果准确性获得分数  $h_t$ 。

多任务学习 (Multi - Task Learning)<sup>[29]</sup> 旨在同时学习多个相关任务, 通过利用任务间的共享信息来提高模型的泛化能力与学习效率。在水文要素的模拟中, 搭建多任务学习框架有助于挖掘各个物理量间的内在联系, 进而避免单独学习导致的信息孤立问题。

![图3 LSTM 结构图：展示了LSTM单元的内部结构。输入x_t和前一时刻的隐藏状态h_{t-1}进入门控机制。遗忘门f_t由输入x_t和前一时刻的细胞状态c_{t-1}通过sigmoid激活函数得到，其输出与c_{t-1}相乘。输入门i_t由输入x_t和前一时刻的隐藏状态h_{t-1}通过sigmoid和tanh激活函数得到，其输出与tanh激活后的输入x_t相乘。输出门o_t由输入x_t和前一时刻的隐藏状态h_{t-1}通过sigmoid激活函数得到，其输出与tanh激活后的细胞状态c_t相乘。最终的隐藏状态h_t是o_t的输出，而细胞状态c_t是遗忘门输出与输入门输出的和。](547f726730e589392f239257a833ede3_img.jpg)

图3 LSTM 结构图：展示了LSTM单元的内部结构。输入x\_t和前一时刻的隐藏状态h\_{t-1}进入门控机制。遗忘门f\_t由输入x\_t和前一时刻的细胞状态c\_{t-1}通过sigmoid激活函数得到，其输出与c\_{t-1}相乘。输入门i\_t由输入x\_t和前一时刻的隐藏状态h\_{t-1}通过sigmoid和tanh激活函数得到，其输出与tanh激活后的输入x\_t相乘。输出门o\_t由输入x\_t和前一时刻的隐藏状态h\_{t-1}通过sigmoid激活函数得到，其输出与tanh激活后的细胞状态c\_t相乘。最终的隐藏状态h\_t是o\_t的输出，而细胞状态c\_t是遗忘门输出与输入门输出的和。

图3 LSTM 结构图

Fig.3 LSTM structure

![图4 多任务学习框架的LSTM模型结构图：展示了多任务学习框架。输入数据进入共享编码层，该层由隐藏层1和隐藏层2组成。隐藏层1和隐藏层2的输出被物理约束嵌入模块处理。然后，这些特征被送入多个独立的任务输出层，分别对应任务1、任务2、任务3，直到任务n，每个任务输出一个结果。](88b0f3f4393228e9ea4d6542aef7c399_img.jpg)

图4 多任务学习框架的LSTM模型结构图：展示了多任务学习框架。输入数据进入共享编码层，该层由隐藏层1和隐藏层2组成。隐藏层1和隐藏层2的输出被物理约束嵌入模块处理。然后，这些特征被送入多个独立的任务输出层，分别对应任务1、任务2、任务3，直到任务n，每个任务输出一个结果。

图4 多任务学习框架的 LSTM 模型结构图

Fig.4 LSTM model structure for multi-task learning

用 LSTM 模型基于多任务学习框架，实现多目标协同模拟之前，需要按时间序列组织数据，形成多个任务的输入输出对。输入数据首先进入 LSTM 层实现共享特征提取，同时被转换为一种隐藏状态。这个隐藏状态包含了时间序列中的趋势、周期性等关键信息，并将相关的特征向量进行融合。接着，为每个模拟任务设置独立的输出层，以便于隐藏状态映射到对应的模拟空间。此外，多任务学习的 LSTM 还可以为每个任务定义损失函数，并采用加权相加的方式将其组合。不同的权重能平衡各个子任务的重要性，以达到不同的研究目标<sup>[30]</sup>。

在为搭建好的 LSTM 模型选取特征（输入）与目标（输出）时，需要密切考虑二维水动力模型的运作机理。因此，将暴雨洪水过程的强相关数据选为特征，二维水动力模型对水位（ $Z$ ）、流量（ $Q$ ）、流速（ $v$ ）与淹没面积（ $A_s$ ）时间序列的对应模拟结果作为目标要素。本研究编程环境为 Python 3.10.13，采用 TensorFlow 2.10.0 深度学习框架搭建模型。硬件方面配备 NVIDIA GeForce MX250 GPU，内存 RAM 为 8GB，以此为模型训练与运算提供支持。

超参数的取值会直接影响 LSTM 洪水预报模型拟合（模拟）与外推（预测）的性能。在已有的工程实践中，多采用从具体问题中总结出的经验调参。本文选用试算法来确定最优的超参数组合，现将选用结果列表如下。其中，隐藏层数量与隐藏单元数决定模型的学习能力；结合研究区域小尺度洪水模拟的特点及试算结果，学习率设为 0.001 恰好满足当前数据条件下模型的稳定收敛；训练轮数取值 100 能够确保模型充分学习数据特征。而当验证集损失连续 10 个训练周期未下降时，早停函数被启用，训练提前终止，避免模型过拟合的同时降低了计算成本。

表 2 LSTM 的参数设置

Table 2 Parameter settings of LSTM

| 隐藏层数量 | 隐藏单元数 | 学习率   | 批次大小 | 训练轮数 | 滑动窗口 | 激活函数    | 优化器  |
|-------|-------|-------|------|------|------|---------|------|
| 2     | 64    | 0.001 | 32   | 100  | 20   | Sigmoid | Adam |

#### 2.2.2 添加物理约束的 LSTM 模型

运用 LSTM 实现多目标模拟时，若仅孤立地考量每一项要素的拟合效果往往过于片面。事实上，各模拟要素之间普遍存在着物理相关关系，这种内在联系在提升模拟精度和增强模型可解释性方面具有不可忽视的重要意义。而将其作为约束条件引入模型中，本质上是为模型提供了关于问题的先验知识，有助于模型更合理地学习和模拟。

本文依据训练集上研究断面水位、流量、淹没面积的二维模拟结果，绘制水位-流量过程线与水位-淹没面积关系曲线，并拟合得出相应的物理关系  $y_1 = f(x)$ ， $y_2 = g(x)$ 。在 LSTM 洪水预报模型训练过程中，通常以最小化损失函数为目标进行优化，直至模型在训练集样本上的输出与对应真实值的偏差总体最小<sup>[31]</sup>。鉴于模拟要素间物理关系对提升模型性能的重要性，将上述拟合关系作为约束条件引入损失函数，即在原有的均方误差（MSE）基础上添加一个惩罚项。由此新的损失函数可以定义为：

$$L = MSE + \lambda_1 (y_1 - \hat{y}_1)^2 + \lambda_2 (y_2 - \hat{y}_2)^2 \quad (5)$$

其中:  $y_1$  和  $y_2$  是流量和淹没面积的理论真实值;  $\hat{y}_1$  和  $\hat{y}_2$  是训练集上的预测值;  $\lambda$  是权重系数, 用于平衡数据拟合损失和物理关系约束的损失。当  $\lambda$  较大时, 模型会更加注重满足物理关系; 当  $\lambda$  较小时, 模型更侧重于数据拟合。

在参数选择方面, 考虑物理约束的 LSTM 模型沿用约束前 LSTM 模型的超参数组合, 以便于更直观地呈现物理约束这一变量对模拟结果的作用。对  $\lambda$  的取值, 通过量级敏感性分析发现, 当  $\lambda_1$ 、 $\lambda_2$  取  $10^{-7}$  时, 物理约束项  $(y_1 - \hat{y}_1)^2$ 、 $(y_2 - \hat{y}_2)^2$  的梯度贡献量级与原始  $MSE$  损失项达到动态平衡。具体而言, 由于物理关系约束项本身具有强非线性特征 (如  $Z-Q$  函数的梯度可达  $10^4$  量级), 当  $\lambda > 10^{-5}$  时, 约束项主导梯度更新方向, 导致模型陷入局部最优而丧失数据驱动优势; 反之, 当  $\lambda = 10^{-7}$  时, 约束项在反向传播中的有效梯度权重被控制在  $MSE$  梯度的 1%~5% 范围内, 既能在参数空间中引导物理一致性, 又保留了 LSTM 对复杂水文响应的学习能力。这种弱约束机制与自适应正则化思想相契合, 其有效性通过决定系数提升超过 20% 得以验证, 表明在保持数据驱动优势的同时, 精微的物理导向能提升模型外推能力。

另外, 在现有模型的基础上, 增加随机森林 (Random Forest) [32] 算法来评价特征的重要性。对于流量边界、水位边界、降雨量等输入特征, 其对目标变量预测结果的影响主要依据随机森林中每棵决策树在节点分裂时对不同特征的利用情况, 以及该特征对提升最终模拟结果准确性的实际贡献来综合衡量。评估机理如下:

对于一个包含  $n$  个特征的数据集, 对每一个特征  $X_i$  ( $i=1,2,\dots,n$ ), 在随机森林的每一棵决策树  $T_j$  ( $j=1,2,\dots,m$ ) 中计算该特征的重要性得分。然后, 对所有决策树中该特征的贡献进行平均, 得到特征  $X_i$  在整个随机森林中的重要性得分 [33]。随机森林中的重要性得分通过以下公式计算:

$$FI(X_i) = \frac{1}{m} \sum_{j=1}^{m} \sum_{v \in Nodes(T_j)} \Delta Gini(X_i, v) \quad (6)$$

其中:  $m$  是决策树的数量;  $Nodes(T_j)$  是决策树  $T_j$  中的节点集合;  $\Delta Gini(X_i, v)$  是特征  $X_i$  在节点  $v$  分裂时导致的基尼不纯度减少量。基尼不纯度表示一个节点数据的“混乱程度”, 如果所有样本都属于同一类别, 那么基尼不纯度为 0。

为提升特征评价结果的可信度, 降低使用单一评价方法的局限性, 进一步引入斯皮尔曼秩相关系数法 [34] 与 PCA 主成分分析法 [35], 综合评价特征的重要性。

### 2.3 评价指标

为评估和验证基于 LSTM 的城市暴雨洪水模拟结果的准确性, 本文引入平均绝对误差 ( $MAE$ )、均方根误差 ( $RMSE$ ) 和决定系数 ( $R^2$ ) 作为统一的评价指标。  $MAE$  与  $RMSE$  的值越小, 说明模型的模拟值与真实值越接近, 模型的性能就越好。当  $R^2$  越接近 1 时, 模型对因变量变异的解释程度越高。

$$MAE = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i| \quad (7)$$

$$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2} \quad (8)$$

$$R^2 = 1 - \frac{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}{\sum_{i=1}^{n} (y_i - \bar{y}_i)^2} \quad (9)$$

其中:  $n$  是样本数量;  $y_i$  和  $\hat{y}_i$  是第  $i$  个样本的真实值与模拟值;  $\bar{y}_i = \frac{1}{n} \sum_{i=1}^{n} y_i$ , 是真实值的平均值。

在评估模型的整体精度时, 主要依据熵权法 [36] 将  $RMSE$  和  $R^2$  值的权重均设为 0.4,  $MAE$  值的

权重设置为 0.3。这一权重分配方案基于数据本身离散程度，同时旨在突出  $RMSE$  对极端误差的敏感性以及  $R^2$  对数据拟合的解释能力，兼顾  $MAE$  所反映的平均误差情况。再对单一指标的精度提升比率做加权平均，即可得到能够综合反映模型精度变化的百分比。这种方法能够有效整合不同指标的信息，为评估模型在洪水模拟中的性能改进提供一个全面且量化的依据。

## 3 研究结果分析

### 3.1 模型模拟用时比较

对 17 场洪水过程开展水动力模拟，并求得其平均用时。利用得到的数据分别训练 LSTM 模型和有物理约束的 LSTM 模型，记录训练阶段与测试阶段的平均运算时长（如表 3 所示）。

表 3 二维水动力模型与 LSTM 模型的场次洪水的模拟用时

Table 3 Simulation time for field floods with 2D hydrodynamic and LSTM models

| 二维水动力模型 | LSTM    |        | 有物理约束的 LSTM |        |
|---------|---------|--------|-------------|--------|
|         | 训练阶段    | 测试阶段   | 训练阶段        | 测试阶段   |
| 5 h     | 34.52 s | 0.69 s | 38.12 s     | 0.73 s |

LSTM 模型的平均训练时长为 34.52 s，添加物理约束后的 LSTM 模型平均训练时长为 38.12 s。运算耗时增加了 3.6 s，归因于添加的物理约束一定程度上增加了模型计算的复杂度。在测试阶段，约束前后 LSTM 模型的平均模拟用时分别为 0.69 s 和 0.73 s，差距微弱，不超过 0.1 s。综上可知，虽然改进后的模型较 LSTM 在训练集与测试集上的运算耗时均有一定幅度的增加，但相较二维水动力模拟以小时为单位的模拟时长，添加物理约束的 LSTM 能在 1 s 内完成场次洪水的多要素模拟，结果更全面，也满足了时效性要求。

### 3.2 模拟效果评价

#### 3.2.1 多场次洪水的整体模拟

如图 5 所示，三张箱型图呈现了在表 2 参数设定下，LSTM 模型以及具有物理约束的 LSTM 模型于训练-验证阶段，对  $Z$ 、 $Q$ 、 $v$ 、 $A_s$  模拟结果的总体误差分布态势。分别从平均绝对误差（ $MAE$ ）、均方根误差（ $RMSE$ ）和决定系数（ $R^2$ ）评估了模型表现。

LSTM 模型的  $MAE$  箱体位置较高，中位数约为 0.0225；而有物理约束的 LSTM 模型  $MAE$  箱体位置更低，中位数约 0.0165，平均误差相较小，意味着该模型的模拟结果更接近真实值。对  $RMSE$  指标，LSTM 模型的箱体中位数约 0.0355，有物理约束的 LSTM 中位数约 0.0270，后者数值更小，表明有物理约束的模型精度更高。最后，有物理约束的 LSTM 模型  $R^2$  的中位数约为 0.988，相比 LSTM 模型更趋近于 1，说明其对数据的拟合效果更佳。综合上述指标来看，引入物理约束的 LSTM 模型在性能上均优于普通 LSTM 模型，对四个水力要素的综合模拟效果更好。此外，在超参数直接移用的情况下该模型仍有性能提升，这不仅验证了原 LSTM 模型超参数的可行性，还表明加入物理约束能够有效优化模型性能。

![Figure 5: Three box plots comparing LSTM and physically constrained LSTM models across three metrics: MAE, RMSE, and R^2. The MAE plot shows the constrained model has a lower median error. The RMSE plot shows the constrained model has a lower median error. The R^2 plot shows the constrained model has a higher median R^2 value, closer to 1.000.](68aa26525c9346e4590a15c75d394e9d_img.jpg)

Figure 5 consists of three box plots arranged horizontally. The first plot on the left shows the Mean Absolute Error (MAE) for two models: LSTM (blue box) and physically constrained LSTM (pink box). The y-axis ranges from 0.010 to 0.030. The LSTM box has a median around 0.0225, while the constrained LSTM box has a lower median around 0.0165. The second plot in the middle shows the Root Mean Square Error (RMSE) for the same two models. The y-axis ranges from 0.020 to 0.045. The LSTM box has a median around 0.0355, while the constrained LSTM box has a lower median around 0.0270. The third plot on the right shows the coefficient of determination ( $R^2$ ) for the two models. The y-axis ranges from 0.968 to 1.000. The LSTM box has a median around 0.977, while the constrained LSTM box has a higher median around 0.988, closer to 1.000.

Figure 5: Three box plots comparing LSTM and physically constrained LSTM models across three metrics: MAE, RMSE, and R^2. The MAE plot shows the constrained model has a lower median error. The RMSE plot shows the constrained model has a lower median error. The R^2 plot shows the constrained model has a higher median R^2 value, closer to 1.000.

图 5 训练-验证集上两种模型的多要素总体误差分布图

Fig. 5 Multi-factor overall error distribution for both models on the training-validation set

在测试集上，考虑物理约束前后 LSTM 模型的模拟结果如表 4 所示。显然，两种模型模拟结果的  $R^2$  均高于 0.90，最高值达 0.9907，总体表现良好。具体而言，有物理约束的模型  $MAE$  值分别为

0.0887、9.3322、4.0071、3.6464，均低于 LSTM 模型的 0.1247、13.6554、4.5222、4.7499。纵向来看，对  $Z$ 、 $Q$ 、 $A_s$  的模拟结果，有物理约束的 LSTM 模型具有更低的  $RMSE$  值和更高的  $R^2$  值。由此可得，考虑物理约束后，模型的模拟偏差有所降低，表现明显更优。综合以上指标，易求得  $Z$ 、 $Q$ 、 $A_s$  的模拟精度分别提升了 20.38%、17.03%、14.07%。而对于  $v$ ，其模拟精度受模型优化的影响较微弱，仅提升了 4.02%。

表 4 模型在测试集上的多要素模拟结果评价指标

Table 4 Evaluation indicators of the model's multifactor simulation results on the test set

| 评价指标   | 模拟要素        | LSTM     | 有物理约束的 LSTM |
|--------|-------------|----------|-------------|
| $MAE$  | $Z/m$       | 0.1247   | 0.0887      |
|        | $Q/(m^3/s)$ | 13.6554  | 9.3322      |
|        | $v/(m/s)$   | 4.5222   | 4.0071      |
|        | $A_s/m^2$   | 4.7499   | 3.6464      |
| $RMSE$ | $Z/m$       | 0.2585   | 0.1881      |
|        | $Q/(m^3/s)$ | 182.2208 | 153.6061    |
|        | $v/(m/s)$   | 0.0527   | 0.0519      |
|        | $A_s/m^2$   | 56.5735  | 47.0298     |
| $R^2$  | $Z/m$       | 0.9650   | 0.9849      |
|        | $Q/(m^3/s)$ | 0.9166   | 0.9453      |
|        | $v/(m/s)$   | 0.9759   | 0.9759      |
|        | $A_s/m^2$   | 0.9767   | 0.9853      |

#### 3.2.2 典型场次洪水模拟

为探讨模型在场次洪水中的模拟精度，在测试集内选取 3 场典型洪水展开进一步分析。图 6 展示了 2015080908 场次洪水中各要素的模拟结果，其中图线  $L_{Z0}$ 、 $L_{Q0}$ 、 $L_{v0}$ 、 $L_{A_{s0}}$  表示二维水动力模型的模拟结果，曲线  $L_{Z1}$ 、 $L_{Q1}$ 、 $L_{v1}$ 、 $L_{A_{s1}}$  表示 LSTM 模型的模拟结果，曲线  $L_{Z2}$ 、 $L_{Q2}$ 、 $L_{v2}$ 、 $L_{A_{s2}}$  表示考虑物理约束的 LSTM 模拟结果。

![Figure 6: Comparison of simulation results for 2015080908 flood event. The figure consists of two line graphs. The left graph shows water depth (Z/m) over time (时段) from 0 to 80. The right graph shows discharge (Q/(m^3/s)) over the same time period. Both graphs compare three models: 2D hydraulic model (L_{Z0}, L_{Q0}, L_{v0}, L_{A_{s0}}), LSTM (L_{Z1}, L_{Q1}, L_{v1}, L_{A_{s1}}), and LSTM with physical constraints (L_{Z2}, L_{Q2}, L_{v2}, L_{A_{s2}}). In both cases, the LSTM with physical constraints (L_{Z2}, L_{Q2}) shows the highest peak and best fit to the observed data (solid black line).](0f3e3ea50bcceb86f6c524ab2b6f3e7a_img.jpg)

Figure 6: Comparison of simulation results for 2015080908 flood event. The figure consists of two line graphs. The left graph shows water depth (Z/m) over time (时段) from 0 to 80. The right graph shows discharge (Q/(m^3/s)) over the same time period. Both graphs compare three models: 2D hydraulic model (L\_{Z0}, L\_{Q0}, L\_{v0}, L\_{A\_{s0}}), LSTM (L\_{Z1}, L\_{Q1}, L\_{v1}, L\_{A\_{s1}}), and LSTM with physical constraints (L\_{Z2}, L\_{Q2}, L\_{v2}, L\_{A\_{s2}}). In both cases, the LSTM with physical constraints (L\_{Z2}, L\_{Q2}) shows the highest peak and best fit to the observed data (solid black line).

![Figure 6: Schematic of the multi-factor simulation results for the flood of field 2015080908. The figure consists of two line graphs. The left graph plots flow velocity v (m/s) against time period (时段) from 0 to 80. It shows three curves: L_v0 (solid black line), L_v1 (dashed red line), and L_v2 (dashed blue line). All curves show a peak around time 35, with L_v2 being the highest. The right graph plots flow area A (m^2) against time period (时段) from 0 to 80. It shows three curves: L_A0 (solid black line), L_A1 (dashed red line), and L_A2 (dashed blue line). All curves show a peak around time 35, with L_A2 being the highest.](adb1f42239329fa8283d1a40005f989f_img.jpg)

Figure 6: Schematic of the multi-factor simulation results for the flood of field 2015080908. The figure consists of two line graphs. The left graph plots flow velocity v (m/s) against time period (时段) from 0 to 80. It shows three curves: L\_v0 (solid black line), L\_v1 (dashed red line), and L\_v2 (dashed blue line). All curves show a peak around time 35, with L\_v2 being the highest. The right graph plots flow area A (m^2) against time period (时段) from 0 to 80. It shows three curves: L\_A0 (solid black line), L\_A1 (dashed red line), and L\_A2 (dashed blue line). All curves show a peak around time 35, with L\_A2 being the highest.

图 6 2015080908 场次洪水的多要素模拟结果示意图

Fig. 6 Schematic of the multi-factor simulation results for the flood of field 2015080908

如图 6 所示, 考虑物理约束的 LSTM 模拟结果与水动力模型的模拟值更为接近。特别是在流量变化较大的区域,  $L_{Q2}$  相较于  $L_{Q1}$  展现出更优的拟合效果, 充分彰显了物理约束在较小量级、较长历时洪水过程模拟中的显著优势。分析表 5 数据可知, 在施加物理约束后, 模拟结果的  $MAE$ 、 $RMSE$  值降低而  $R^2$  值升高, 各要素的模拟精度平均提升了 25.29%, 与图示情况吻合。改进后的模型在低流量条件下有更高的精度和稳定性。

不难看出, 对同一场洪水而言, 模型对不同要素的模拟效果往往呈现出十分近似的规律。因此, 图 7 仅罗列了余下两场典型洪水中, 更具代表性的水位结果。

![Figure 7: Schematic diagram of water level simulation results for typical field floods. The figure consists of two line graphs. Graph (a) shows water level Z (m) vs time period (时段) for flood 2016071420. Graph (b) shows water level Z (m) vs time period (时段) for flood 2020070604. Both graphs compare three models: L_Z0 (solid black line), L_Z1 (dashed red line), and L_Z2 (dashed blue line). In graph (a), L_Z2 shows the highest peak. In graph (b), L_Z2 shows a higher peak than L_Z1, and L_Z1 shows a higher peak than L_Z0.](8ee3b76dd49f31624d287885bc2c81ee_img.jpg)

Figure 7: Schematic diagram of water level simulation results for typical field floods. The figure consists of two line graphs. Graph (a) shows water level Z (m) vs time period (时段) for flood 2016071420. Graph (b) shows water level Z (m) vs time period (时段) for flood 2020070604. Both graphs compare three models: L\_Z0 (solid black line), L\_Z1 (dashed red line), and L\_Z2 (dashed blue line). In graph (a), L\_Z2 shows the highest peak. In graph (b), L\_Z2 shows a higher peak than L\_Z1, and L\_Z1 shows a higher peak than L\_Z0.

图 7 典型场次洪水的水位模拟结果示意图

Fig. 7 Schematic diagram of water level simulation results for typical field floods

编号 2016071420 是陡涨陡落的尖瘦型洪水, 具有一定的代表性和发生频率。水位模拟结果显示, 相较  $L_{Z1}$ ,  $L_{Z2}$  对  $L_{Z0}$  的拟合偏差更大。但不可忽视的是, 即使约束后模型的模拟精度普遍低于约束前, 其整体的拟合情况仍十分理想。结合四个要素的模拟结果评价指标发现,  $R^2$  的最小值高于 0.98, 最大值更是达到 0.9957, 约束前后的模型模拟精度均处于较高水平。这是由于在当前的模型体系与数据条件下, 模型自身已具备较强的模拟能力, 物理约束的作用虽然存在, 但相较于其他影响因素, 其对模拟精度提升的边际效应已被削弱。

对于 2020070604 号大型洪水,  $L_{Z2}$  较  $L_{Z1}$  的拟合程度在水位变化较大的区域有明显提高。然而, 在流量模拟方面,  $L_{Q1}$  与  $L_{Q2}$  对峰值大小与峰现时间的模拟均较差。 $L_{Q2}$  的模拟偏差较  $L_{Q1}$  大, 对于  $A_s$  曲线的拟合情况,  $L_{A2}$  表现却又优于  $L_{A1}$ 。结合表 4 可得, 虽然整体上约束后模型结果的评价指标优于约束前, 但仍存在特殊情况。如添加物理约束后, 模拟流速的  $MAE$ 、 $RMSE$  值反而由 5.6620、0.1051 增至 8.5339、0.1694。究其原因可能是双峰洪水的模拟难度高, 而对于一些复杂的物理过程, 在为模型增加约束条件后, 需要匹配更深层次或更复杂的神经网络结构来捕捉物理规律。本研究基

于控制变量的原则，未对除约束外的模型结构做出相应调整，因此造成模拟精度的下降。

表 5 典型场次洪水的模拟结果评价指标

Table 5 Evaluation indexes of simulation results for typical field floods

| 洪号         | 模拟要素  | MAE     |         | RMSE     |          | $R^2$  |        |
|------------|-------|---------|---------|----------|----------|--------|--------|
|            |       | 约束前     | 约束后     | 约束前      | 约束后      | 约束前    | 约束后    |
| 2015080908 | Z     | 0.0962  | 0.0905  | 0.1740   | 0.1425   | 0.9433 | 0.9571 |
|            | Q     | 58.4749 | 13.2766 | 66.1791  | 56.7884  | 0.9061 | 0.9259 |
|            | v     | 6.7443  | 6.5314  | 0.0515   | 0.0424   | 0.9293 | 0.9481 |
|            | $A_s$ | 7.7682  | 6.0935  | 46.5370  | 41.0116  | 0.9422 | 0.9516 |
| 2016071420 | Z     | 0.0639  | 0.0587  | 0.0898   | 0.0954   | 0.9889 | 0.9867 |
|            | Q     | 5.9100  | 9.4056  | 21.7861  | 32.5906  | 0.9957 | 0.9901 |
|            | v     | 2.5114  | 3.1429  | 0.0149   | 0.0221   | 0.9953 | 0.9893 |
|            | $A_s$ | 2.7993  | 3.8836  | 19.0180  | 23.9742  | 0.9928 | 0.9885 |
| 2020070604 | Z     | 0.4487  | 0.3329  | 0.7113   | 0.5951   | 0.6820 | 0.9060 |
|            | Q     | 20.9793 | 19.0474 | 626.1127 | 575.4035 | 0.4178 | 0.5930 |
|            | v     | 5.6620  | 8.5339  | 0.1051   | 0.1694   | 0.8483 | 0.8413 |
|            | $A_s$ | 6.9813  | 5.8038  | 139.1499 | 123.3115 | 0.8574 | 0.9272 |

## 3.3 特征重要性分析

为提升模型可解释性并探究各输入变量对研究断面水力参数模拟的影响，本研究采用三种方法求解特征重要性：随机森林算法侧重预测贡献，斯皮尔曼秩相关系数法反映统计关联，PCA 主成分分析法体现整体变异贡献。为避免主观偏差，最终通过等权重运算整合三种方法结果，得到各输入特征的综合得分。具体而言，即系统评估横江流量边界 ( $Q_1$ )、率水流量边界 ( $Q_2$ )、佩琅河流量边界 ( $Q_3$ )、王村水位边界 ( $Z_1$ ) 与屯溪站的降雨过程 ( $P$ ) 这五个因素，分别对研究断面水位 ( $Z$ )、流量 ( $Q$ )、流速 ( $v$ ) 与淹没面积 ( $A_s$ ) 模拟结果所产生的贡献程度。旨在通过综合分析，揭示不同边界条件和降雨过程在研究断面水力特性模拟中的相对重要性。

表 6 考虑物理约束的 LSTM 对输入特征的评估

Table 6 Importance assessment of input features by LSTM considering physical constraints

|                       |       | $Q_1$       | $Q_2$       | $Q_3$       | $Z_1$       | $P$         |
|-----------------------|-------|-------------|-------------|-------------|-------------|-------------|
| RF 重要性<br>权重          | Z     | 0.005       | 0.983       | 0.007       | 0.003       | 0.001       |
|                       | Q     | 0.006       | 0.987       | 0.005       | 0.001       | 0.001       |
|                       | v     | 0.007       | 0.979       | 0.008       | 0.004       | 0.001       |
|                       | $A_s$ | 0.006       | 0.983       | 0.007       | 0.003       | 0.001       |
| 斯皮尔曼<br>数绝对值<br>(显著性) | Z     | 0.966 (P=0) | 0.975 (P=0) | 0.947 (P=0) | 0.922 (P=0) | 0.237 (P=0) |
|                       | Q     | 0.967 (P=0) | 0.976 (P=0) | 0.948 (P=0) | 0.922 (P=0) | 0.238 (P=0) |
|                       | v     | 0.969 (P=0) | 0.976 (P=0) | 0.948 (P=0) | 0.923 (P=0) | 0.240 (P=0) |
|                       | $A_s$ | 0.966 (P=0) | 0.975 (P=0) | 0.947 (P=0) | 0.922 (P=0) | 0.237 (P=0) |
| PCA 主成分<br>分析         | 特征值   | 3.609       | 0.954       | 0.261       | 0.108       | 0.069       |
|                       | 解释率%  | 72.16       | 19.07       | 5.22        | 2.17        | 1.38        |
|                       | 平均载荷  | 0.959       | 0.928       | 0.957       | 0.914       | 0.274       |
|                       | 绝对值   |             |             |             |             |             |
| 综合得分                  |       | 0.644       | 0.962       | 0.637       | 0.613       | 0.171       |

如表 6 所示，对于重要性权重与斯皮尔曼秩相关系数的绝对值，每一项输入特征对不同模拟要素的影响差异微弱，最大浮动不超过 0.01。而针对同一要素，不同输入特征的影响权重与相关系数

却呈现出显著差异。具体而言, RF 评价结果显示, 对所有水力要素,  $Q_2$  的权重均接近 0.98, 而  $Q_1$ 、 $Q_3$ 、 $Z_1$ 、 $P$  的权重均低于 0.008, 其中降雨  $P$  的重要性权重最低。这表明  $Q_2$  对下游水力要素的预测影响占绝对主导。斯皮尔曼秩相关系数的结果也呈现出相似的规律, 所有特征与水力要素的关联均显著 ( $P=0$ ), 但系数绝对值存在明显差异, 按从高到低排序依次为  $Q_2$ 、 $Q_1$ 、 $Q_3$ 、 $Z_1$ 、 $P$ , 流量边界  $Q_2$  与下游水力要素的单调关联性最强。不过, 采用 PCA 主成分分析法得到的结论却有所不同, 仅有  $Q_1$  的特征值  $P>1$ , 因此其作为核心信息主导整体变异。同时,  $Q_1$  和  $Q_3$  的平均荷载绝对值相近, 接近 0.96, 二者对特征整体变异的解释力略高于  $Q_2$ , 而  $P$  的解释力仍为最弱。

最后等权重整合三种评价方法发现, 率水流量  $Q_2$  的综合得分显著领先,  $P$  始终为最次要特征。相较 RF 单独评估时过度突出  $Q_2$ , 可能忽略其他特征的协同作用, 组合评价结果使得  $Q_1$ 、 $Q_3$ 、 $Z_1$  的重要性被合理识别。结合客观事实剖析可知: 屯溪流域的上游地势落差大、下游河道较为顺直且水系连通, 为水流下泄创造了便利条件; 加之多发的短历时暴雨使得洪水在河道内停留时间较短, 下游水位便不会出现大幅上升, 难以形成持续显著的顶托; 降雨分布相对均匀, 周边丰富的植被覆盖也可以减缓暴雨对城市的影响, 再经过复杂的流域汇流等过程后, 降雨对研究断面处的影响会受到明显削弱。此时, 上有入流特别是率水的流量成为影响模拟结果的最主要因素。这与率水的年径流量居新安江各支流之首, 对新安江水量补给作用突出的事实相呼应。因此, 新安江下游断面的水力要素对率水流量变化更为敏感。上述分析既有助于理解智能模型的运算思维, 也能为城市洪水响应工作提供参考。

# 4 总结与讨论

## 4.1 结论

本研究搭建了一个考虑物理约束的 LSTM 多要素洪水模拟模型, 旨在提升传统智能模型的洪水模拟效率。并通过引入物理约束, 增强模型的科学性与合理性。同时, 针对机器学习缺乏可解释性的问题, 从事前解释与事后解释两个角度进行剖析<sup>[37]</sup>; 一方面, 在模型构建阶段充分考量物理机制与数据特征之间的内在联系, 为模型的参数设定和结构优化提供坚实的理论依据; 另一方面, 通过对模型模拟结果的深入挖掘与分析, 揭示模型决策过程中的关键因素和影响机制。通过上述研究工作, 实现对河道单一断面多要素的高时效性、高精度与高可靠性模拟。研究结论如下:

a. 添加物理约束的 LSTM 能在 1 s 内完成场次洪水的多要素模拟, 实现高效运算。与传统的 LSTM 模型相比, 该模型还显著提升了模型的模拟精度、稳定性和对数据的拟合能力。具体而言, 水位、流量、流速和淹没面积的模拟精度提升百分比分别为 20.38%、17.03%、4.02%、14.07%。

b. 物理约束对 LSTM 在场次洪水各要素模拟中的影响较为复杂。通常施加物理约束后, 模拟结果的  $MAE$ 、 $RMSE$  值下降而  $R^2$  值上升, 各要素的平均模拟精度提升约 25.29%。但在部分场次的流量和流速模拟中, 物理约束效果欠佳, 这可能是由于不同场次的洪水特性各异, 导致现有物理约束难以全面适配所有复杂情形。

c. 探讨模型的可解释性, 不仅加深了对算法逻辑的理解, 还能指导实践。本文一方面将物理约束加入 LSTM 模型, 赋予深度学习算法的决策过程以物理内涵; 另一方面, 特征综合评估结果表明, 在本研究模拟中, 必须高度重视率水上边界入流的测量精度。而其他重要性相对较低的特征如降雨, 依模型复杂度与计算资源许可的要求, 允许被适当简化处理。

## 4.2 讨论

本研究在一定程度上, 为如何将深度学习模型更好地应用于水文模拟及预报领域提供了新的思考, 但仍存在局限性。尽管模型在小洪水与常规洪水模拟中表现良好, 但在极端复杂工况下性能仍待优化, 可能归因于极端事件的样本稀缺性导致模型泛化能力不足, 或物理约束未能完全覆盖复杂水动力过程的动态变化。此外, 当前模型对空间特征的刻画能力有限, 尚未充分反映河道多断面间的水力联系与洪水演进的时空耦合关系。

未来的研究将从以下方面展开: 其一, 通过数据增强技术合成极端工况数据, 结合遥感影像等

多源异构数据扩充训练样本，提升模型对复杂场景的适应性。其二，基于现有成果，搭建融合空间特征学习的深度学习模型，捕捉河道网络的拓扑结构与洪水传播规律，实现时空协同模拟。在此技术框架成熟后，再进一步尝试从内部神经元层面解析模型的决策逻辑，探究更深层次的可解释性，最终构建兼具高适应性、强解释性的水动力预报模型体系。

# 参考文献：

- [1] 中国气象局气候变化中心, 2023.中国气候变化蓝皮书 (2023) .北京: 科学出版社.(CMA Climate Change Centre, 2024. Blue Book on Climate Change in China (2024). Beijing: Science Press.(in Chinese))
- [2] 黄一为.全国政协委员仲志余: 加强城市极端暴雨洪水有效精准防控[N].中国水利报,2024-03-09(001).(Huang Yiwei. Zhong Zhiyu, a National Committee Member of the Chinese People's Political Consultative Conference: Strengthening the Effective and Precise Prevention and Control of Urban Extreme Rain-storm Floods [N]. China Water Resources News, 2024-03-09(001).(in Chinese))
- [3] 陈朝晖,李鹏,张煜洲,等.耦合一二维水动力模型的城市社区暴雨内涝模拟研究[J].水利水电技术(中英文),2024,55(07):55-69.(Chen Zhaohui, Li Peng, Zhang Yuzhou, et al. Simulation Study on Rainstorm Waterlogging in Urban Communities Using Coupled One- and Two-Dimensional Hydrodynamic Models [J]. Water Resources and Hydropower Engineering, 2024,55(07):55-69.(in Chinese))
- [4] 彭锋,柴福鑫,张红萍,等.复杂地形的城市地表二维水动力模拟方法[C]//《中国防汛抗旱》杂志社,中国水利学会城市水利专业委员会,水利部防洪抗旱减灾工程技术研究中心.第五届城市水安全与水管理学术研讨会暨第六届城市防洪排涝学术研讨会论文集.中国水利水电科学研究院,水利部防洪抗旱减灾工程技术研究中心,2022:6.(Peng Feng, Cai Fuxin, Zhang Hongping, et al. Two-Dimensional Hydrodynamic Simulation Method for Urban Surface in Complex Terrain [C]//China Flood & Drought Management Magazine, Urban Water Conservancy Committee of China Hydraulic Engineering Society, Engineering Technology Research Center for Flood Control and Drought Relief of the Ministry of Water Resources. Proceedings of the 5th Academic Symposium on Urban Water Security and Water Management & 6th Academic Symposium on Urban Flood Control and Drainage. China Institute of Water Resources and Hydropower Research; Engineering Technology Research Center for Flood Control and Drought Relief of the Ministry of Water Resources, 2022:6.(in Chinese))
- [5] 卢兴超,徐宗学,李永坤,等.基于SWMM与LISFLOOD-FP耦合模型的城市街区 内涝模拟研究[J].水资源保护,2024,40(03):98-105+124.(Lu Xingchao, Xu Zongxue, Li Yongkun, et al. Simulation Study on Urban Block Waterlogging Based on SWMM and LISFLOOD-FP Coupled Model [J]. Water Resources Protection,2024,40(03):98-105+124.(in Chinese))
- [6] 廖如婷,徐宗学,叶陈雷,等.基于SWMM和InfoWorks ICM模型的大红门排水区暴雨内涝模拟[J].水资源保护,2023,39(03):109-117.(Liao Ruting, Xu Zongxue, Ye Chenlei, et al. Simulation of Rainstorm Waterlogging in Dahongmen Drainage Area Based on SWMM and InfoWorks ICM Models [J]. Water Resources Protection,2023,39(03):109-117.(in Chinese))
- [7] 李致家.现代水文模拟与预报技术[M].南京:河海大学出版社,2021.(Li ZhiJia. Modern Hydrological Modelling and Forecasting Techniques [M]. Nanjing: Hohai University Press,2021.(in Chinese))
- [8] Yaoxing L, Zhaoli W ,Xiaohong C , et al.Fast simulation and prediction of urban pluvial floods using a deep convolutional neural network model[J].Journal of Hydrology,2023,624
- [9] 庄潇然,刘梅,蔡凝昊,等.基于深度学习的降水临近预报方法及其在2023年江苏汛期的应用评估[J].暴雨灾害,2025,44(01):1-8.(Zhuang Xiaoran, Liu Mei, Cai Ninghao, et al. Nowcasting Methods for Precipitation Based on Deep Learning and Their Application Evaluation During the 2023 Flood Season in Jiangsu Province [J]. Torrential Rain and Disasters, 2025,44(01):1-8.(in Chinese))
- [10] 纪守领,李进锋,杜天宇,等.机器学习模型可解释性方法、应用与安全研究综述[J].计算机研究与发展,2019,56(10):2071-2096.(Ji Shouling, Li Jinfeng, Du Tianyu, et al. A Review of Interpretability Methods, Applications, and Security for Machine Learning Models [J]. Journal of Computer Research and Development,2019,56(10):2071-2096.(in Chinese))
- [11] 夏弘.深度学习和水动力学模型结合的中小河流洪水预报研究[D].山东大学,2022.(Xia Hong. Study on Flood

Forecasting in Medium and Small Rivers by Combining Deep Learning and Hydrodynamic Models [Dissertation]. Shandong University, 2022. (in Chinese)

[ 12 ] Pan X , Hou J , Gao X , et al. LSTM Model-Based Rapid Prediction Method of Urban Inundation with Rainfall Time Series [J]. Water Resources Management, 2024, (prepublish): 1-28.

[ 13 ] Chen J , Li Y , Zhang S . Fast Prediction of Urban Flooding Water Depth Based on CNN-LSTM [J]. Water, 2023, 15(7):

[ 14 ] Yang F , Ding W , Zhao J , et al. Rapid urban flood inundation forecasting using a physics-informed deep learning approach [J]. Journal of Hydrology, 2024, 643: 131998-131998.

[ 15 ] Ribeiro T M , 0001 S S , Guestrin C . "Why Should I Trust You?": Explaining the Predictions of Any Classifier [J]. CoRR, 2016, abs/1602.04938.

[ 16 ] Sebastian B , Alexander B , Grégoire M , et al. On Pixel-Wise Explanations for Non-Linear Classifier Decisions by Layer-Wise Relevance Propagation [J]. PLoS one, 2015, 10(7): e0130140.

[ 17 ] Karpathy A , Johnson J , Li F . Visualizing and Understanding Recurrent Networks [J]. CoRR, 2015, abs/1506.02078.

[ 18 ] Kratzert F , Klotz D , Brenner C , et al. Rainfall-runoff modelling using Long Short-Term Memory (LSTM) networks [J]. Hydrology and Earth System Sciences, 2018, 22(11): 6005-6022.

[ 19 ] Wojciech Samek , Grégoire Montavon , Andrea Vedaldi , et al. Explainable AI: Interpreting, Explaining and Visualizing Deep Learning [M]. Springer, Cham:

[ 20 ] A.A. AM , C. R.D , Qi F , et al. Deep learning hybrid model with Boruta-Random forest optimiser algorithm for streamflow forecasting with climate mode indices, rainfall, and periodicity [J]. Journal of Hydrology, 2021, 599.

[ 21 ] 吴剑. 基于长短时记忆网络的山丘区中小河流洪水预报研究 [D]. 大连理工大学, 2021. (Wu Jian. Study on Flood Forecasting in Small and Medium-Sized Rivers in Mountainous and Hilly Regions Based on Long Short-Term Memory (LSTM) Network [D]. Dalian University of Technology, 2021. (in Chinese))

[ 22 ] 王雨洁, 李致家, 姚成, 等. 基于分布式水文水动力耦合模型的秦淮河流域洪水模拟 [J/OL]. 河海大学学报 (自然科学版), 1-13 [2024-12-11]. (Wang Yujie, Li Zhijia, Yao Cheng, et al. Study on Flood Simulation in the Qinhuai River Basin Based on a Coupled Distributed Hydrological-Hydrodynamic Model [J/OL]. Journal of Hohai University (Natural Sciences), 1-13 [2024-12-11]. (in Chinese))

[ 23 ] 汪昊燃, 王容, 黄鹏年, 等. 水文水力学结合的秦淮河流域洪水模拟与实时校正 [J]. 河海大学学报 (自然科学版), 2023, 51(03): 25-30+64. (Wang Haoran, Wang Rong, Huang Pengnian, et al. Flood Simulation and Real-Time Calibration in the Qinhuai River Basin Based on a Coupled Hydrological-Hydraulic Model [J]. Journal of Hohai University (Natural Sciences), 2023, 51(03): 25-30+64. (in Chinese))

[ 24 ] 李致家, 姚成, 章玉霞, 等. 栅格型新安江模型的研究 [J]. 水力发电学报, 2009, 28(02): 25-34. (Li Zhijia, Yao Cheng, Zhang Yuxia, et al. Study on Grid-based Xin'anjiang Model [J]. Journal of Hydroelectric Engineering, 2009, 28(02): 25-34. (in Chinese))

[ 25 ] 韩龙喜. 求解守恒形式的二维浅水方程的SIMPLE类程式 [J]. 水力学报, 2000, (07): 91-95. (Han Longxi, et al. SIMPLE-like Program for Solving the Conservative Form of Two-Dimensional Shallow-Water Equations [J]. Journal of Hydraulic Engineering, 2000, (07): 91-95. (in Chinese))

[ 26 ] 王双涛. 基于非结构化网格的1D-2D水动力模型耦合研究及应用 [D]. 长安大学, 2023. (Wang Shuangtao. Study on the Coupling and Application of 1D-2D Hydrodynamic Model Based on Unstructured Grids [D]. Chang'an University, 2023. (in Chinese))

[ 27 ] 蒋艳, 杨珏, 赵棣华, 等. 浅水流动有限体积法/Osher格式的二维水流-水质模拟 [J]. 农村生态环境, 2002, (03): 30-33. (Jiang Yan, Yang Jue, Zhao Dihua, et al. Two-Dimensional Flow-Quality Simulation of Shallow-Water Flows with Finite-Volume Method/Osher Scheme [J]. Rural Eco-Environment, 2002, (03): 30-33. (in Chinese))

[ 28 ] Staudemeyer C R , Morris R E . Understanding LSTM - a tutorial into Long Short-Term Memory Recurrent Neural Networks [J]. CoRR, 2019, abs/1909.09586

[ 29 ] Ruder S. An overview of multi-task learning in deep neural networks [J]. arXiv preprint arXiv: 1706.05098, 2017.

- [30] 周恒安,成乐,施克权,等.基于多任务图神经网络的非定常流体预测[J].科学技术与工程,2024,24(27):11733-11740.(Zhou Heng'an, Cheng Le, Shi Kequan, et al. Unsteady Fluid Prediction Based on Multi-Task Graph Neural Network [J]. Science Technology and Engineering,2024,24(27):11733-11740.(in Chinese))
- [31] 孟涵,姚成,郑爱民,等.不同情景下LSTM及其变体模型的洪水模拟研究[J/OL].中国农村水利水电,1-13[2024-12-14].(Meng Han, Yao Cheng, Zheng Aimin, et al. Study on Flood Simulation with LSTM and Its Variant Models under Different Scenarios [J/OL]. China Rural Water and Hydropower,1-13[2024-12-14].(in Chinese))
- [32] 吕红燕,冯倩.随机森林算法研究综述[J].河北省科学院学报,2019,36(03):37-41.(Lü Hongyan, Feng Qian. A Review of Random Forest Algorithm Research [J]. Journal of Hebei Academy of Sciences,2019,36(03):37-41.(in Chinese))
- [33] 赵润泽.基于随机森林的特征选择算法研究[D].华中科技大学,2023.(Zhao Runze. Research on Feature Selection Algorithm Based on Random Forest [D]. Huazhong University of Science and Technology,2023.(in Chinese))
- [34] 刘娟,彭剑虹,曹伟,等.县域城市质量效益指数与城市综合竞争力相关性研究——基于斯皮尔曼秩相关系数的实证分析[J].质量与认证,2024,(12):63-65.(Liu Juan, Peng Jianhong, Cao Wei, et al. Research on the Correlation between Quality-Benefit Index of County-Level Cities and Comprehensive Urban Competitiveness: An Empirical Analysis Based on Spearman's Rank Correlation Coefficient [J]. Quality and Certification,2024,12(12):63-65.(in Chinese))
- [35] 代硕,苏怀智,谷宇,等.基于PCA-GO-BP-AdaBoost的大坝变形监控模型[J].人民黄河,2025,47(S1):100-102+104.(Dai Shuo, Su Huaizhi, Gu Yu, et al. Dam Deformation Monitoring Model Based on PCA-GO-BP-AdaBoost [J]. Yellow River,2025,47(S1):100-102+104.(in Chinese))
- [36] 胡嘉玮,徐宗学,陈浩,等.基于精细化GDP格局的城市洪涝风险评估——以济南市黄台桥流域为例[J/OL].南水北调与水利科技(中英文),1-14[2025-07-06].(Hu Jiawei, Xu Zongxue, Chen Hao, et al. Urban Flood Risk Assessment Based on Refined GDP Spatial Distribution: A Case Study of Huang Tai Qiao Drainage Basin in Jinan City [J/OL]. South-to-North Water Transfers and Water Science & Technology (Chinese & English),1-14[2025-07-06].(in Chinese))
- [37] 化盈盈,张岱墀,葛仕明.深度学习模型可解释性的研究进展[J].信息安全学报,2020,5(03):1-12.(Hua Yingying, Zhang Daichi, Ge Shiming, et al. Research Progress on Interpretability of Deep Learning Models [J]. Journal of Cyber Security,2020,5(03):1-12.(in Chinese))