![Cover image of the journal 'Computer Technology and Development' (计算机技术与发展). The cover features a blue-toned abstract image of circuitry or data flow.](2dfa6ac3edfe874f68aa0cbccaa42322_img.jpg)

Cover image of the journal 'Computer Technology and Development' (计算机技术与发展). The cover features a blue-toned abstract image of circuitry or data flow.

计算机技术与发展  
*Computer Technology and Development*  
ISSN 1673-629X, CN 61-1450/TP

## 《计算机技术与发展》网络首发论文

题目： 基于多变量 LSTM 的湖泊藻密度预测算法  
作者： 邱浩宇, 孙泽慧, 陆海霞, 张欣, 刘天赐  
DOI: 10.20165/j.cnki.ISSN1673-629X.2025.0341  
收稿日期: 2025-09-15  
网络首发日期: 2025-12-30  
引用格式: 邱浩宇, 孙泽慧, 陆海霞, 张欣, 刘天赐. 基于多变量 LSTM 的湖泊藻密度预测算法[J/OL]. 计算机技术与发展.  
<https://doi.org/10.20165/j.cnki.ISSN1673-629X.2025.0341>

![QR code linking to the article's DOI.](5fb340ad68b0c71df0b56698b137e35b_img.jpg)

QR code linking to the article's DOI.

![CNKI (China National Knowledge Infrastructure) logo with the text '中国知网' and 'www.cnki.net'.](390120de4fe440c42fea8154fcaad334_img.jpg)

CNKI (China National Knowledge Infrastructure) logo with the text '中国知网' and 'www.cnki.net'.

**网络首发:** 在编辑部工作流程中, 稿件从录用到出版要经历录用定稿、排版定稿、整期汇编定稿等阶段。录用定稿指内容已经确定, 且通过同行评议、主编终审同意刊用的稿件。排版定稿指录用定稿按照期刊特定版式(包括网络呈现版式)排版后的稿件, 可暂不确定出版年、卷、期和页码。整期汇编定稿指出版年、卷、期、页码均已确定的印刷或数字出版的整期汇编稿件。录用定稿网络首发稿件内容必须符合《出版管理条例》和《期刊出版管理规定》的有关规定; 学术研究成果具有创新性、科学性和先进性, 符合编辑部对刊文的录用要求, 不存在学术不端行为及其他侵权行为; 稿件内容应基本符合国家有关书刊编辑、出版的技术标准, 正确使用和统一规范语言文字、符号、数字、外文字母、法定计量单位及地图标注等。为确保录用定稿网络首发的严肃性, 录用定稿一经发布, 不得修改论文题目、作者、机构名称和学术内容, 只可基于编辑规范进行少量文字的修改。

**出版确认:** 纸质期刊编辑部通过与《中国学术期刊(光盘版)》电子杂志社有限公司签约, 在《中国学术期刊(网络版)》出版传播平台上创办与纸质期刊内容一致的网络版, 以单篇或整期出版形式, 在印刷出版之前刊发论文的录用定稿、排版定稿、整期汇编定稿。因为《中国学术期刊(网络版)》是国家新闻出版广电总局批准的网络连续型出版物(ISSN 2096-4188, CN 11-6037/Z), 所以签约期刊的网络版上网络首发论文视为正式出版。

# 基于多变量 LSTM 的湖泊藻密度预测算法

邱浩宇，孙泽慧，陆海霞，张欣，刘天赐

(宿迁学院 数理学院，江苏 宿迁 223800)

**摘 要：**中国内陆湖泊长期遭受蓝藻水华问题的困扰，为科学应对这一挑战、有效治理水华并保护水环境，本研究构建了多变量长短时记忆（M-LSTM）模型，通过皮尔逊相关系数筛选出水温、pH 值、电导率、溶解氧、浊度和叶绿素 a 这些关键环境因子作为模型输入特征。此外，为进一步提升模型对水体藻密度动态变化的捕捉与预测能力，该模型创新性地采用了双层 LSTM 结构。同时，引入批量归一化层对数据进行标准化处理，加速模型收敛；结合丢弃层随机丢弃部分神经元，防止过拟合。在模型训练环节，用顺序预测确保学习顺序合理，采用早停法避免过度训练，通过不断试验筛选出最佳参数组合，进一步提升预测精度。实验结果显示，该模型在藻密度预测上表现出卓越性能，均方误差（MSE）和平均绝对误差（MAE）分别低至 0.0005 和 0.0179，精准捕捉并有效预测了藻密度的动态变化。这一技术手段不仅验证了模型的高效性和可靠性，更为水体中藻密度的实时监测与预测提供了科学依据，对预防和治理蓝藻水华具有极其重要的意义。

**关键词：**长短期记忆网；藻密度；预测；蓝藻；水华

**中图分类号：**TP391 **文献标志码：**A

**doi:**10.20165/j.cnki.ISSN1673-629X.2025.0341

# Research on lake algae density prediction algorithm based on multivariate LSTM

QIU Hao-yu, SUN Ze-hui, LU Hai-xia, ZHANG Xin, LIU Tian-ci

(School of Mathematics and Physics, Suqian University, Suqian 223800, China)

**Abstract:** Inland lakes in China have long suffered from the problem of cyanobacterial blooms. In order to scientifically cope with this challenge, effectively manage blooms and protect the water environment, this study constructed a multivariate Long Short-Term Memory (M-LSTM) model. Key environmental factors, encompassing water temperature, pH value, dissolved oxygen, conductivity, turbidity, and chlorophyll-a, were sifted out as input features for the model by employing the Pearson correlation coefficient. In addition, to further enhance the model's ability to capture and predict the dynamic changes in water body algae density, the model innovatively adopts a two-layer LSTM (Long Short-Term Memory) structure. Meanwhile, a Batch Normalization layer is introduced to standardize the data and accelerate model convergence, while a Dropout layer is paired to randomly discard some neurons and prevent overfitting. During the model training process, sequential prediction is employed to ensure a reasonable learning sequence, the early stopping method is adopted to avoid overtraining, and the optimal parameter combination is identified through continuous experimentation. These strategies work together to improve prediction accuracy. The experimental results show that the model exhibits excellent performance in algal density prediction, with mean square error (MSE) and mean absolute error (MAE) as low as 0.0005 and 0.0179, respectively, which accurately captures and effectively predicts the dynamics of algal density. This technique not only verifies the efficiency and reliability of the model, but also provides a scientific basis for the real-time monitoring and prediction of algal density in water bodies, which is of great significance for the prevention and management of cyanobacterial blooms.

**Key words:** long short-term memory; algal density; prediction; cyanobacteria; bloom

收稿日期：2025-09-15

基金项目：大规模复杂系统数值模拟教育部重点实验室开放课题基金资助项目（202510）；江苏省大学生创新创业训练计划项目（202414160017Z）；宿迁市科技计划资助项目（M202206）。

作者信息：邱浩宇（2004-），男，本科生，CCF 会员(A08371G)，研究方向为深度学习；通信作者：张欣（1984-），女，副教授，博士，研究方向为运筹优化，深度学习。

## 0 引言

蓝藻<sup>[1]</sup>过度增殖致水华, 威胁河湖生态, 降低透明度、减少溶氧, 危及水生生物。化学药剂处理虽暂有效, 但长期使用会积累致中毒、恶化水质和二次污染。

为了更有效地应对水华问题, 减少化学溶液的使用并降低对水环境的影响, 加强藻密度的预测显得尤为重要。近年来, 神经网络在预测领域的应用日益广泛, 为蓝藻密度的预测提供了新的思路。

在众多的神经网络模型中, BP 神经网络、基于小波分析的 ANN 神经网络以及基于遥感图像和卷积神经网络的模型等, 都已被应用于蓝藻密度的预测中。例如, 刘恒等<sup>[2]</sup>研究者利用 BP 神经网络成功预测了千岛湖的叶绿素浓度; Xiao 等<sup>[3]</sup>则通过小波分析改进了一种基于 ANN 的神经网络, 对美国 Winnebago 湖的蓝藻密度进行了有效的预测; 吴羽溪<sup>[4]</sup>则基于遥感图像和卷积神经网络技术, 提出了 3D-CNN、改进的 4D-CNN 及 4D-FractalNet 模型, 徐虹等研究者<sup>[5]</sup>基于 2001-2021 年逐日 MODIS 数据和随机森林算法, 构建了滇池复苏期与高发期蓝藻水华发生气象概率预测模型, 定量评估了气象条件对滇池蓝藻水华发生的影响并实现有效预测此外, 陈斐等<sup>[6]</sup>利用 BP-RNN 模型预测了崂山水库的蓝藻; 邹阳等<sup>[7]</sup>利用 RF-LSTM 模型预测了滇池蓝藻水华; 谢如意等<sup>[8]</sup>基于主成分分析法与 RBF 神经网络耦合模型进行了水华预测研究; 王雪晴<sup>[9]</sup>提出了

Bi-LSTM-ARIMA 模型; 林永琪等<sup>[10]</sup>基于 GEE 平台进行了太湖水华的遥感分析与预测。

上述各类模型在蓝藻预测方面取得了一定成果, 特别是长短期记忆网络(LSTM)<sup>[11-14]</sup>, 以其捕捉长时间序列的优越性和处理高度非线性大规模数据集时的优势, 成功克服了原始循环神经网络的缺陷, 成为目前最受欢迎的 RNN 之一, 并在语音识别、图片描述、自然语言处理等多个领域取得了显著成就。

在以上研究成果的基础上, 本研究基于 TensorFlow<sup>[15]</sup>深度学习框架, 构建了多变量 LSTM (M-LSTM) 蓝藻密度预测方法。该方法综合考虑了水温、pH 值、溶解氧、电导率、浊度、叶绿素、藻密度、风向、风速等多个因素作为输入因子, 对蓝藻密度进行精确预测。为验证该方法的有效性, 本研究将预测结果与三种模型进行了对比, 这三种模型分别是: 仅以蓝藻密度作为输入因子构建的单变量 LSTM (S-LSTM) 模型、BP 神经网络模型, 以及 GRU 门控循环神经网络模型<sup>[16]</sup>。

## 1 数据与方法

### 1.1 数据来源

数据来自江苏省环境监测中心, 采集的数据包括水温(℃)、pH(无量纲)、溶解氧(mg/L)、电导率( $\mu\text{S}/\text{cm}$ )、浊度(NTU)、叶绿素 a(mg/L)、藻密度(万个/L)、风向(度)、风速(m/s)。表 1 为五里湖监测点各因子在 2021 年到 2023 年的统计量指标。

表 1 监测数据各因子统计量指标

| 统计量                            | 最小值   | 平均值     | 最大值   | 标准差     |
|--------------------------------|-------|---------|-------|---------|
| 水温(℃)                          | 3.2   | 19.377  | 32.7  | 8.551   |
| pH(无量纲)                        | 7     | 8.082   | 9     | 0.456   |
| 溶解氧(mg/L)                      | 3.9   | 9.544   | 14.3  | 2.317   |
| 电导率( $\mu\text{S}/\text{cm}$ ) | 289.2 | 382.518 | 455.5 | 39.038  |
| 浊度(NTU)                        | 4.3   | 22.001  | 71.4  | 14.405  |
| 叶绿素(mg/L)                      | 0.002 | 0.014   | 0.056 | 0.008   |
| 藻密度(万个/L)                      | 116   | 831.647 | 3792  | 769.057 |
| 风向(度)                          | 89    | 188.632 | 319   | 28.716  |
| 风速(m/s)                        | 0.5   | 2.640   | 8.3   | 1.365   |

### 1.2 研究方法

构如图 1 所示:

LSTM<sup>[17]</sup>是一种特殊的递归神经网络(RNN), 用于解决传统 RNN 中存在的长期依赖问题, 即 RNN 难以记住较强时间间隔的信息。LSTM 主要由遗忘门、输入门、候选门和输出门组成, 其基本结

![Diagram of an LSTM cell structure. It shows inputs x_t and h_{t-1} entering the cell. The input x_t goes through a sigmoid layer (sigma) to produce the input gate i_t. The previous hidden state h_{t-1} and current input x_t are combined (represented by a box with a plus sign) and then passed through a tanh layer to produce the candidate cell state C'_t. The previous cell state C_{t-1} and the candidate cell state C'_t are combined (represented by a box with a plus sign) and then passed through a sigmoid layer (sigma) to produce the forget gate f_t. The forget gate f_t and the previous cell state C_{t-1} are combined (represented by a box with a multiplication sign) to produce the current cell state C_t. Finally, the current cell state C_t is passed through a tanh layer and then multiplied by the output gate o_t (which is produced by combining h_{t-1} and x_t through a sigmoid layer) to produce the current hidden state h_t.](2763901b7a1fd1b5d704cdc450d12ed0_img.jpg)

Diagram of an LSTM cell structure. It shows inputs x\_t and h\_{t-1} entering the cell. The input x\_t goes through a sigmoid layer (sigma) to produce the input gate i\_t. The previous hidden state h\_{t-1} and current input x\_t are combined (represented by a box with a plus sign) and then passed through a tanh layer to produce the candidate cell state C'\_t. The previous cell state C\_{t-1} and the candidate cell state C'\_t are combined (represented by a box with a plus sign) and then passed through a sigmoid layer (sigma) to produce the forget gate f\_t. The forget gate f\_t and the previous cell state C\_{t-1} are combined (represented by a box with a multiplication sign) to produce the current cell state C\_t. Finally, the current cell state C\_t is passed through a tanh layer and then multiplied by the output gate o\_t (which is produced by combining h\_{t-1} and x\_t through a sigmoid layer) to produce the current hidden state h\_t.

图 1 LSTM 结构图

遗忘门的作用是决定当前哪些信息需要从记忆单元中丢弃。遗忘门接受前一时刻的隐状态  $h_{t-1}$  和当前输入  $x_t$ , 并通过一个 sigmoid<sup>[18]</sup>激活函数输出一个值在 0 到 1 之间的标量矩阵, 表示当前单元需要“遗忘”多少信息。

计算公式如下:

$$f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f), \quad (1)$$

其中  $f_t$  是遗忘门的输出;  $W_f$  是权重矩阵;  $b_f$  是偏置项;  $h_{t-1}$  是前一个时间步的隐藏状态;  $x_t$  是当前时间步的输入;  $\sigma$  是 Sigmoid 函数, 它将输入压缩到 0-1 之间。

输入门决定当前时刻的新信息有多少被加入细胞状态。输入门包括两个部分: 输入门  $i_t$  和决定候选信息中哪些可以更新到记忆单元中候选记忆  $C'_t$ , 公式如下:

$$i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i), \quad (2)$$

$$C'_t = \tanh(W_c \cdot [h_{t-1}, x_t] + b_c). \quad (3)$$

新的记忆单元状态  $C_t$  是前一时间步的状态

$C_{t-1}$  和当前时间步的候选记忆  $C'_t$  的加权和:

公式 (4) 表明了 LSTM 如何决定哪些信息需要遗忘、哪些信息需要记住, 并将新的信息结合到记忆单元中。

输出门决定当前时刻的隐藏状态输出是什么。

$$C_t = f_t \cdot C_{t-1} + i_t \cdot C'_t. \quad (4)$$

通过遗忘部分不重要的信息, 并结合当前输入, 生成一个新的隐藏状态用于后续的时间公式如下:

$$o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o), \quad (5)$$

$$h_t = o_t \cdot \tanh(C_t). \quad (6)$$

隐藏状态  $h_t$  是经过激活函数处理后的记忆单元状态  $C_t$ , 并由输出门  $o_t$  决定输出多少。

### 1.3 模型评价标准

本研究采用均方误差、均方根误差和平均绝对误差来评价预测模型的优劣程度。

(1) 均方误差 (Mean Square Error -MSE) 均方误差是误差平方和的平均值。

$$MSE = \frac{1}{n} \sum_{i=1}^{n} (Y'_i - Y_i)^2. \quad (7)$$

(2) 均方根误差 (Root Mean Square

Error-RMSE) 均方根误差是所有误差平方的平均值的平方根(RMSE)。

$$RMSE = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (Y'_i - Y_i)^2}. \quad (8)$$

(3) 平均绝对误差(MAE) 平均绝对误差是所有误差的绝对值的平均值。MAE 数值越小, 模型预测结果与真实值偏差越小, 结果也就越准确。

$$MAE = \frac{1}{n} \sum_{i=1}^{n} |Y'_i - Y_i|, \quad (9)$$

其中,  $Y'_i$  代表单位面积藻密度的预测值;  $Y$  代表单位面积藻密度实际值;  $n$  为测试样本的个数。评价指标的值越接近于 0, 模型预测精度越高。

## 2 模型建立与求解

本研究构建了基于多变量 LSTM 的蓝藻密度预测模型, 其系统框架如图 2 所示。首先, 利用皮尔逊(Pearson)<sup>[19]</sup>相关系数从原始数据中筛选关键预测因子, 然后基于箱型图法剔除异常值并实施 Z-Score 标准化, 确保模型输入的稳健性与可比性。最终, 构建双层 LSTM 网络, 实现对藻密度的精准预测。

![Figure 2: Model Structure Diagram. The diagram illustrates the workflow from raw data to prediction. On the left, '原始数据' (Raw Data) includes time-series plots for '水温' (Water Temperature), 'pH', and '风向' (Wind Direction). An arrow points to '预测因子选择' (Prediction Factor Selection), which then leads to '关键预测因子' (Key Prediction Factors) containing '水温' and 'pH'. These factors are processed by '箱型图法数据标准化' (Box Plot Data Standardization). The standardized data is then input into a '双层 LSTM' (Double-layer LSTM) model. The LSTM model structure is detailed on the right, showing a cell with inputs $x_t$, $h_{t-1}$, and $C_{t-1}$. The cell calculates gates $f_t$, $i_t$, and $o_t$ using sigmoid and tanh functions, and then updates the cell state $C_t$ and hidden state $h_t$. The LSTM layers are shown as a sequence of cells. The final output is '预测结果' (Prediction Result) with a 'Loss' indicator.](f9a14fbfecbd7d059226cc93677d721b_img.jpg)

Figure 2: Model Structure Diagram. The diagram illustrates the workflow from raw data to prediction. On the left, '原始数据' (Raw Data) includes time-series plots for '水温' (Water Temperature), 'pH', and '风向' (Wind Direction). An arrow points to '预测因子选择' (Prediction Factor Selection), which then leads to '关键预测因子' (Key Prediction Factors) containing '水温' and 'pH'. These factors are processed by '箱型图法数据标准化' (Box Plot Data Standardization). The standardized data is then input into a '双层 LSTM' (Double-layer LSTM) model. The LSTM model structure is detailed on the right, showing a cell with inputs \$x\_t\$, \$h\_{t-1}\$, and \$C\_{t-1}\$. The cell calculates gates \$f\_t\$, \$i\_t\$, and \$o\_t\$ using sigmoid and tanh functions, and then updates the cell state \$C\_t\$ and hidden state \$h\_t\$. The LSTM layers are shown as a sequence of cells. The final output is '预测结果' (Prediction Result) with a 'Loss' indicator.

图 2 模型结构图

### 2.1 预测因子的选择

皮尔逊(Pearson)<sup>[19]</sup>相关系数可以衡量两个变量  $X$ 、 $Y$  之间的线性相关程度, 通常  $\gamma$  来表示, 其定义如下式所示:

$$\gamma = \frac{\sum_{i=1}^{n} (X_i - \bar{X})(Y_i - \bar{Y})}{\sqrt{\sum_{i=1}^{n} (X_i - \bar{X})^2} \sqrt{\sum_{i=1}^{n} (Y_i - \bar{Y})^2}}, \quad (10)$$

其中,  $n$  为样本量;  $\gamma$  代表皮尔逊相关系数。若  $\gamma > 0$ , 表示 2 个变量是正相关的; 若  $\gamma < 0$ , 则代表 2 个变量是负相关的。各因素与藻密度的相关系数如表 2 所示。

表 2 各要素的线性相关性

|       | 水温     | pH     | 溶解氧    | 电导率    | 浊度     | 叶绿素 a  | 藻密度    | 风向     | 风速     |
|-------|--------|--------|--------|--------|--------|--------|--------|--------|--------|
| 水温    | 1      | 0.283  | -0.655 | -0.563 | 0.456  | -0.204 | 0.713  | 0.357  | -0.238 |
| pH    | 0.283  | 1      | 0.354  | 0.011  | -0.245 | 0.334  | 0.372  | 0.069  | -0.077 |
| 溶解氧   | -0.655 | 0.354  | 1      | 0.0504 | -0.743 | 0.497  | -0.293 | -0.277 | 0.087  |
| 电导率   | -0.563 | 0.011  | 0.504  | 1      | -0.640 | 0.371  | -0.535 | -0.172 | 0.304  |
| 浊度    | 0.456  | -0.245 | -0.743 | -0.640 | 1      | -0.524 | 0.335  | 0.130  | -0.158 |
| 叶绿素 a | -0.204 | 0.334  | 0.497  | 0.371  | -0.524 | 1      | -0.254 | 0.026  | 0.125  |
| 藻密度   | 0.713  | 0.372  | -0.293 | -0.535 | 0.335  | -0.254 | 1      | 0.206  | -0.229 |
| 风向    | 0.357  | 0.069  | -0.277 | -0.172 | 0.130  | 0.026  | 0.206  | 1      | 0.213  |
| 风速    | -0.238 | -0.077 | 0.087  | 0.304  | -0.158 | 0.125  | -0.229 | 0.213  | 1      |

从表 2 可以看出, 水温与藻密度呈现出较显著的正相关, 相关系数为 0.713, 当水温处于 24°C-30°C 的适宜区间时, 蓝藻细胞内酶活性提升、光合作用效率提高, 代谢活动增强从而大量增殖<sup>[20]</sup>, 所以水温是预测蓝藻水华发生的关关键指标, 监测其变

化可有效预判藻密度走向。pH 值与藻密度正相关, 相关系数为 0.372, 偏碱性水体环境利于蓝藻细胞内生理生化过程顺利进行, 提高其对营养物质的吸收利用效率, 进而促进生长繁殖, 监测 pH 值的变化能辅助了解蓝藻生长环境适宜性。电导率与藻密

度呈负相关, 相关系数-0.535, 电导率反映水体离子浓度, 其升高使离子环境变化, 某些离子有毒性会抑制蓝藻生长, 某些营养元素过量或不足会影响代谢, 从而影响藻密度。浊度与藻密度正相关, 相关系数 0.335, 适度浊度下, 水体悬浮颗粒物可携带氮、磷等营养物质为蓝藻生长提供养分, 还能作为附着载体利于其聚集生长。溶解氧与藻密度负相关, 相关系数为-0.293, 虽为负相关, 但适量溶解氧参与蓝藻细胞内氧化还原反应提供能量, 含量异常会影响其呼吸与代谢, 过高可能产生氧化应激损伤细胞, 过低会抑制呼吸作用。叶绿素 a 虽与藻密度负相关, 相关系数为-0.254, 但从生物学意义讲, 其含量增加通常反映蓝藻生物量上升, 能直接体现光合作用强度, 对预警水华爆发意义重大。风向、风速与藻密度相关性较弱, 它们也会通过水体流动间接影响藻密度变化, 但其影响较弱。因此, 本研究将主要考虑水温、pH 值、电导率、浊度、溶解氧及叶绿素 a 作为预测蓝藻水华密度的关键输入变量。

### 2.2 箱型图法剔除异常值

箱型图<sup>[21]</sup>是一种统计图表, 专门用于展示数据集的分散特性, 其名称源自其独特的箱状形态。它在多个领域有着广泛的应用, 特别是在质量控制和快速识别异常数据点方面。箱型图的主要优势在于, 它能够有效地反映数据的离散分布情况, 并且不会受到异常值的干扰, 这对于数据清洗工作特别有帮助。箱型图的制作基于几个关键的统计数据: 最大值、最小值、中位数、第一四分位数和第三四分位数。利用这些统计数据, 箱型图设定了异常值的界限。上限为  $Q_3 + k(Q_3 - Q_1)$ , 下限为  $Q_1 - k(Q_3 - Q_1)$ , 其中  $Q_1$  代表上四分位数,  $Q_3$  代表下四分位数,  $k$  一般取 1.5。如果某个数据点位于上限之上或下限之下, 则被视为异常值, 如图 3 所示。

![Figure 3: A box plot diagram illustrating the detection of outliers. The plot shows a central box representing the interquartile range (IQR) between the first quartile (Q1) and the third quartile (Q3). A horizontal line inside the box represents the median. Whiskers extend from the box to the minimum and maximum values within the outlier boundaries. The upper boundary is labeled '上限' (Upper Limit) and the lower boundary is labeled '下限' (Lower Limit). A red triangle below the lower whisker is labeled '异常值' (Outlier).](46f43cb4ffd47565e7c0ca306d461435_img.jpg)

Figure 3: A box plot diagram illustrating the detection of outliers. The plot shows a central box representing the interquartile range (IQR) between the first quartile (Q1) and the third quartile (Q3). A horizontal line inside the box represents the median. Whiskers extend from the box to the minimum and maximum values within the outlier boundaries. The upper boundary is labeled '上限' (Upper Limit) and the lower boundary is labeled '下限' (Lower Limit). A red triangle below the lower whisker is labeled '异常值' (Outlier).

图 3 箱型图法检测异常值

### 2.3 数据标准化

为确保数据分析的准确性和模型训练的有效性, 需要对监测数据进行标准化处理, 以消除不同变量间因量纲和数量级差异带来的影响, 从而提升数据间的可比性, 使模型能够更公平地处理各变量信息。本文采用数据 Z-Score 标准化处理。

$$X'_i = \frac{(X_i - \mu)}{\sigma}, \quad (11)$$

其中,  $X_i$ ---原始值;  $\mu$ ---均值;  $\sigma$ ---标准差;

$X'_i$ ---标准化后的值。原始数据经过标准化处理

后, 符合标准正态分布。

### 2.4 多变量 LSTM(M-LSTM)模型的构建

为了充分利用已采集信息, 使预测结果更加合理准确, 在模型构建时, 将 2.1 节确定的预测因子作为输入层, 构建多变量 LSTM(简称为 M-LSTM)模型, 并基于 TensorFlow 框架实现具体算法。

与仅依赖单一特征序列的单变量 LSTM 相比, 多变量 LSTM 能同步融合多维输入, 挖掘变量间潜藏的耦合关系, 全方位刻画各因子对目标的协同作用, 从而显著提升预测精度。凭借多元信息的互补增益, 模型在面对复杂时序场景时展现出更优的泛化性能与稳健性。

TensorFlow<sup>[22]</sup>, 是以图计算为核心, 张量沿数据流图传递并完成运算, 天然兼具灵活性与可扩展性。框架内置的 LSTMCell 将遗忘门、输入门、输出门完整封装, 用户只需调用高级 API 即可构建深层网络, 免去繁琐的梯度推导与参数管理。得益于此, 本文基于 TensorFlow 仅用少量代码即实现多变量 LSTM 模型, 显著缩短研发周期, 并为进一步调优留出空间。

本研究以当日水温、pH、溶解氧、电导率、浊度及前日藻密度共六维变量为输入, 以当日藻密度为应变量, 构建时序预测框架。数据集按时间顺序划分为训练集(涵盖 2021-01-01—2023-10-02 数据)与测试集(包含 2023-10-03—2023-12-31 数据), 并实施 Z-Score 标准化以保证跨集分布一致性。网络架构采用双层 LSTM, 其中首层配置 `return_sequences=True`, 后接 BatchNormalization 与 Dropout 以加速收敛并抑制过拟合; 次层输出经 ReLU 激活函数映射至单神经元线性输出层, 预测结果通过逆标准化还原真实尺度。同时训练过程引入早停回调, 并以最优超参数组合进行顺序迭代, 辅以全程可视化分析验证模型稳健性与泛化性能。

### 2.5 模型架构与参数设置

模型采用双层 LSTM 结构处理数据，其中第一层 LSTM 通过 88 个神经元输出每个时间步的隐藏状态，为第二层 LSTM 提供低级时序特征；第二层 LSTM 以 53 个神经元整合这些特征，仅输出最后一个时间步的隐藏状态用于最终预测。这种设计旨在捕捉各要素的长期依赖关系，例如温度变化对藻类生长的滞后影响——通过逐层提取时序模式，模型能够识别跨时间步的复杂关联。

在模型训练和参数设置方面，首先，为防止过拟合，引入 BatchNormalization，设置 batch\_size 为 51，为每个批次的样本做整体作标准化，该策略与数据标准化（Z-score）共同作用，确保输入特征与目标变量在均值为 0、方差为 1 的尺度下训练，不仅消除了量纲差异对模型的影响，更提升了 LSTM 的梯度传播效率。其次，通过 13% 的 Dropout 随机丢弃神经元连接，这里的 Dropout 率 0.13 低于常规值 0.2~0.5，是因为数据量较大且模型复杂度适中，无需强烈正则化。在此基础上，通过 32 个神经元的 Dense 层（ReLU 激活）进一步做非线性变换，最终由单神经元输出预测值（无激活函数，适配回归任务），形成从时序特征提取到空间特征压缩的完整流程。最后，模型选用 Adam 优化器自适应调整模型的学习率，免去手动调参需求，适合本研究中水质数据的非平稳特征。

在模型收敛和终止准则方面，本研究采用早停机制和固定最大轮次相结合的终止准则来平衡模型收敛性与训练效率。具体而言，早停机制通过监控训练损失和验证损失的动态变化实现自适应终止；训练损失与验证损失主要有以下三种状态：若训练损失与验证损失同步下降，说明该模型的训练成果有效且收敛；若训练损失持续下降而验证损失不降反增，说明模型过度拟合；若训练损失持续下降而验证损失停滞不降，则说明模型容量不足（网络层数太少、神经元数量有限），无法获取更复杂的关系。根据以上三种状态，在模型训练过程中，当连续 10 个轮次验证损失的值没有降低，则停止训练。此外，设置固定最大轮次 epochs 为 88，以确保训练流程的鲁棒性。

### 2.6 实验与结果分析

为了验证本文提出的 M-LSTM 模型在预测藻密度时的有效性和准确性，选取另外三种深度学习模型对同样的数据集进行训练和预测。一是基于单一变量（藻密度）的 LSTM（简称为 S-LSTM）模型，即仅依赖单一变量（如藻密度）的预测模型；

二是 BP 神经网络模型，三是 GRU 门控循环神经网络模型。在评估模型性能时，采用了多种评估指标，包括均方误差（MSE）、均方根误差（RMSE）、以及平均绝对误差（MAE），这些指标为模型的优化与验证提供了坚实、可靠的依据。图 4-7 直观地展示了这些模型在预测藻密度方面的具体表现，通过对比，可以清晰地观察到不同模型在预测精度上的差异。图 4 展示了 M-LSTM 模型在测试数据集上的表现。

![Figure 4: A line chart titled '基于M-LSTM模型的预测值与实际值对比'. The y-axis is labeled '藻密度' (Algae Density) with a scale from 200 to 1000. The x-axis is labeled '日期' (Date) with a scale from 2023-10-01 to 2024-01-01. The chart shows two lines: a red dashed line for '实际值' (Actual Value) and a blue solid line for '预测值' (Predicted Value). The two lines are nearly perfectly overlapping, indicating high prediction accuracy.](84e2ac543ffc4145dc85b05a48ec62e3_img.jpg)

Figure 4: A line chart titled '基于M-LSTM模型的预测值与实际值对比'. The y-axis is labeled '藻密度' (Algae Density) with a scale from 200 to 1000. The x-axis is labeled '日期' (Date) with a scale from 2023-10-01 to 2024-01-01. The chart shows two lines: a red dashed line for '实际值' (Actual Value) and a blue solid line for '预测值' (Predicted Value). The two lines are nearly perfectly overlapping, indicating high prediction accuracy.

图 4 基于 M-LSTM 模型的预测值与实际值对比

从图 4 可以看出“实际值”曲线和“预测值”曲线近乎重合，这一现象表明 M-LSTM 模型在湖泊藻密度预测领域具有较高预测精度，进一步验证了 M-LSTM 模型在处理复杂时间序列数据方面的强大能力，同时为湖泊水藻密度预测提供了更为精准、可靠的工具。

![Figure 5: A line chart titled '基于S-LSTM模型的预测值与实际值对比'. The y-axis is labeled '藻密度' (Algae Density) with a scale from 200 to 1000. The x-axis is labeled '日期' (Date) with a scale from 2023-10-01 to 2024-01-01. The chart shows two lines: a red dashed line for '实际值' (Actual Value) and a blue solid line for '预测值' (Predicted Value). The two lines are very close but show some noticeable deviation compared to the M-LSTM model in Figure 4.](112f3fc5dde002caf1c91da443844204_img.jpg)

Figure 5: A line chart titled '基于S-LSTM模型的预测值与实际值对比'. The y-axis is labeled '藻密度' (Algae Density) with a scale from 200 to 1000. The x-axis is labeled '日期' (Date) with a scale from 2023-10-01 to 2024-01-01. The chart shows two lines: a red dashed line for '实际值' (Actual Value) and a blue solid line for '预测值' (Predicted Value). The two lines are very close but show some noticeable deviation compared to the M-LSTM model in Figure 4.

图 5 基于 S-LSTM 模型的预测值与实际值对比

从图 5 可以看出，该模型在测试集上的预测结果与实际值具有一致的走向，但与图 4 相比，仍有一定差距。这一结果表明，S-LSTM 模型可以在一定程度上捕捉湖泊藻密度的动态变化特征，但与 M-LSTM 模型相比，预测精度不够高。

![Figure 6: Comparison of predicted and actual values based on the BP neural network model. The chart shows algae density (藻密度/万/L) on the y-axis (200 to 1000) against dates (2023-10-01 to 2024-01-01) on the x-axis. Two lines are plotted: a red dashed line for actual values and a blue solid line for predicted values. The lines are closely aligned, indicating high prediction accuracy.](c3c305cefbac2e7b13be34ab87054d1e_img.jpg)

Figure 6: Comparison of predicted and actual values based on the BP neural network model. The chart shows algae density (藻密度/万/L) on the y-axis (200 to 1000) against dates (2023-10-01 to 2024-01-01) on the x-axis. Two lines are plotted: a red dashed line for actual values and a blue solid line for predicted values. The lines are closely aligned, indicating high prediction accuracy.

图 6 基于 BP 神经网络的预测值与实际值对比

图 6 展示了采用 BP 神经网络对藻密度进行预测的结果。从图 6 可以清晰地看出，实际值所在曲线与预测值曲线之间存在较大的误差，预测值与实际值之间存在较为明显的偏离情况。

![Figure 7: Comparison of predicted and actual values based on the GRU model. The chart shows algae density (藻密度/万/L) on the y-axis (200 to 1000) against dates (2023-10-01 to 2024-01-01) on the x-axis. Two lines are plotted: a red dashed line for actual values and a blue solid line for predicted values. The lines are closely aligned, indicating high prediction accuracy.](d864789b0d8384da1d22fd6a5d76bbdf_img.jpg)

Figure 7: Comparison of predicted and actual values based on the GRU model. The chart shows algae density (藻密度/万/L) on the y-axis (200 to 1000) against dates (2023-10-01 to 2024-01-01) on the x-axis. Two lines are plotted: a red dashed line for actual values and a blue solid line for predicted values. The lines are closely aligned, indicating high prediction accuracy.

图 7 基于 GRU 模型的预测值与实际值对比

从图 7 的对比结果可见，GRU 模型在测试集上的预测值与实际观测值存在显著偏差，其预测性能明显弱于 M-LSTM 模型。

图 4-7 直观展示了预测结果与实际值的误差。为了更科学地评估各模型的预测能力，表 3 列出不同模型预测结果的 MSE（均方误差）、RMSE（均方根误差）以及 MAE（平均绝对误差）。

表 3 评价标准结果

| 模型      | MSE    | RMSE   | MAE    |
|---------|--------|--------|--------|
| M-LSTM  | 0.0005 | 0.0226 | 0.0179 |
| S-LSTM  | 0.0126 | 0.1123 | 0.0856 |
| BP 神经网络 | 0.0115 | 0.1071 | 0.0766 |
| GRU     | 0.0150 | 0.1225 | 0.0912 |

从表 3 可以看出，M-LSTM 模型在藻密度预测上有显著优势。具体地，当采用 M-LSTM 模型进行预测时，其预测的 MAE（平均绝对误差）极低，仅为 0.0179，同时 RMSE（均方根误差）也保持在较低的水平，为 0.0226。结果表明，与 BP 神经网络和 GRU 门控循环神经网络相比，LSTM 模型更适合预测具有明显时间序列属性的数据。而同样是 LSTM，M-LSTM 在输入层输入多个变量，更加充

分地利用了与藻密度相关的因子数据，比 S-LSTM 模型的预测结果更加准确。

## 3 结束语

本文根据江苏省环境监测中心提供的真实数据进行分析，发现其具有较强的时间序列特性，且各因素之间呈现较强的非线性关系，故采用长短期记忆网络（LSTM）模型作为预测工具。因为 LSTM 模型通过其非线性激活函数能够捕获这些非线性关系，从而提高预测的准确性。进一步，为了更加充分地利用各因素之间的长期依赖关系，对数据进一步做因子分析，选取了水温、pH 值、电导率、浊度、溶解氧及叶绿素 a 以及前一天的藻密度作为输入变量，构建了多变量 LSTM（M-LSTM）模型。

通过对比 M-LSTM 模型、S-LSTM 模型、BP 神经网络和 GRU 模型这四种模型预测藻密度的结果，验证了 M-LSTM 模型的有效性和准确性。与传统的 BP 神经网络相比，M-LSTM 具有强大的提取非线性关系和长时间序列特征的能力，与 GRU 模型相比，M-LSTM 模型通过引入更精细的三门控机制（输入门、遗忘门、输出门），在处理长序列依赖任务时展现出更优的记忆保持能力，并实现了更高的预测准确性。与 S-LSTM 模型相比，M-LSTM 模型更加充分地利用了监测中心站长期连续监测到的多因素数据，并深度挖掘了其长期依赖关系，因此，具有更高的预测精度。

本研究提出的 M-LSTM 模型在预测湖泊藻密度具有高精度和可靠性，为湖泊水藻密度预测提供了更为精准、可靠的工具，有助于相关部门及时采取有效措施，预防和控制湖泊水华事件的发生。未来，可以进一步探索 M-LSTM 模型在其他时间序列预测领域的应用，以充分发挥其在处理复杂时间序列数据方面的优势。

## 参考文献：

- [1] WANG C, XU D, ZHU B, et al. Effect of temperature on surface fluid sediment properties with cyanobacterial bloom biomass accumulation[J]. Journal of Environmental Sciences, 2025, 152: 111-121.
- [2] 刘恒, 严力蛟. BP神经网络在千岛湖水体富营养化变化预测中的应用[J]. 科技通报, 2008(03): 411-416.
- [3] XIAO X, HE J, HUANG H, et al. A novel single-parameter approach for forecasting algal blooms[J]. Water Research, 2017, 108: 222-231.
- [4] 吴羽溪. 基于遥感图像和CNN的蓝藻水华预测方法[D].

北京工商大学,2021.

- [5] 徐虹,戴丛蕊,何雨芩,等.基于随机森林定量评估气象条件对滇池蓝藻水华发生的影响及预测[J/OL].水生态学杂志,1-8[2025-10-24].
- [6] 陈斐.基于机器学习的藻类水华预测研究[D]. 山东师范大学, 2025.
- [7] 邹阳,刘祎,段玮,等.滇池蓝藻水华的RF-LSTM预测模型[J].软件导刊,2024,23(09):70-75.
- [8] 谢如意,李伦,冯振鹏,等.基于主成分分析法及RBF神经网络耦合模型的水华预测研究[J]. 四川环境,2024,43(05):51-56.
- [9] 王雪晴.基于改进Bi-LSTM-ARIMA模型的蓝藻水华预测及决策方法研究[D]. 中国石油大学(华东), 2021.
- [10] 林永琪.基于GEE的太湖水华遥感分析与预测[D].山东大学,2024.
- [11] 刘敏毅,崔博文,王宇坤,等. 基于注意力机制的Transformer 模型预测 PM2.5 浓度[J]. 环境科学,2024,45(12):6993-7002.
- [12] CHICHANI Y S, KASAR S L. An efficient IoT enabled heart disease prediction model using Finch hunt optimization modified BiLSTM classifier[J]. Biomedical Signal Processing and Control,2025,100(PC):107170.
- [13] 张博群, 孙倩, 沈虹. 基于集成分解的农产品价格预测[J]. 扬州大学学报(自然科学版), 2024, 27(04): 47-55.
- [14] ZHU L, HUANG X, ZHANG Z, et al. A novel U-LSTM-AFT model for hourly solar irradiance forecasting[J]. Renewable Energy, 2025, 238:121955.
- [15] PALOMO-ALONSO A, COSTAG V G, MORENO-SAAVEDRA L M, et al. TensorCRO: A TensorFlow - based implementation of a multi - method ensemble for optimization[J]. Expert Systems, 2024, 41(12): e13713.
- [16] 王向前,王琴,徐宁可.基于GRU与非参数核密度估计的煤矿工作面瓦斯浓度区间预测模型[J].矿业安全与环保,2025,52(5):8-15.
- [17] 勾志竟, 宫志宏, 刘布春. 基于TensorFlow的LSTM算法在农业中的应用[J]. 计算机技术与发展, 2021, 31(08): 215-220.
- [18] 高卓凡,郭文利.一种新的基于Sigmoid函数的分布式深度Q网络概率分布更新策略[J]. 计算机科学,2024,51(12):277-285.
- [19] ZOU Y, HUANG Q, QI H. Automatic threshold selection guided by maximizing Pearson correlation[J]. Computers and Electrical Engineering, 2024, 120(PC): 109815.
- [20] 蒙凌凌.水—热—盐变化下太湖蓝藻水华情势预测[D].

重庆交通大学,2024.

- [21] 徐凯, 袁蒋鹏. 粗泛化箱型图法在大中跨径桥梁监测异常值剔除的应用[J]. 广东公路交通, 2024, 50(1):66-71.
- [22] GUNN D J, LIU Z, DAVE R, et al. Touch-Based Active Cloud Authentication Using Traditional Machine Learning and LSTM on a Distributed Tensorflow Framework[J]. International Journal of Computational Intelligence and Applications, 2019, 18(04):16.