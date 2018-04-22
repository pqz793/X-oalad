# 项目可行性研究报告

## 目录

一、项目介绍

* 1.项目名称
* 2.项目概述
* 3.项目目标

二、技术可行性

三、经济可行性

四、计划日程

## 项目介绍

### 1.项目名称

本项目名称暂定为“眼动追踪技术新方法及其在人机交互中的应用”

### 2.项目概述

本项目旨在建立一个低成本的新方式，利用简单的头戴设备或者桌面设备（包括设备自带设备，如摄像头），对用户的视线信息做出分析，提取出有效信息作为机器输入，从而作为一种新的机器控制方法。具体地说，我们希望能从用户眼部信息中，实时的定位用户关注的屏幕区域、进行注视检测、提供辅助阅读等功能。
我们希望克服目前眼动追踪技术中设备成本高、便携性差的问题，制作出一个“即插即用、随身携带”级别的设备。另外，我们希望方法尽可能的简单，能够用一个精简的驱动乃至集成至操作系统中实现，而不是消耗巨大的计算资源。
我们不会将重点放在精确性和高帧率上，原因是目前眼动追踪技术已经足够精确，采样频率也足够高。而我们项目面向便携设备，难以在这两点上与大型设备或接触式设备相提并论。对于精确性和采样频率，我们将以实用性为标准，在能保证使用的情况下尽可能精简设备、节约计算资源。

### 3.项目目标

根据具体情况，我们为不同时间点拟定了不同的项目目标，基础目标是项目的最低要求，中长期目标是在基础目标的条件下的进一步优化和改进。项目目标也会根据项目实际完成情况进行调整。大致计划如下：

#### 3.1.基础目标

项目的基础目标是在不需要额外硬件设备的条件下，利用设备自带的前置摄像头，完成一个基础的视线分类器。实现对特定用户（或用户组）视线在屏幕上的焦点进行区域归类。这个阶段最基础的目标是二区域分类，即将屏幕划分为两个部分（左右或上下），对用户视线进行二分类判断。在二区域分类的基础上，可尝试实现四区域、九区域的分类功能。
这个阶段对采样率要求在1Hz左右，并保证运算实时性，可以进行前置的训练工作。在这个阶段，我们还会首先才用一些较强假设，如用户在使用过程中头部相对于屏幕的位置没有改变， 所以注视点的改变仅仅是由眼部状态改变导致的。

预计实现算法：

* 1.实时图像提取：在程序中实时地提取摄像头图像并进行处理的功能。预估可用OpenCV内置接口和设备摄像头实现。
* 2.面部分层识别：在图像中分层识别面部、眼部、瞳孔的位置。并能截取出格式较为统一的眼部图像并标记瞳孔位置，以便作为数据使用。可能通过OpenCV提供的层级分类器或其它开源分类器实现。 
* 3.简单分类器：将眼部图像按照注视位置分类的分类器。能够判断特定格式眼部图像所注视的屏幕位置，最简单的为二分类器。可能用各类机器学习算法实现。

#### 3.2.中期目标

中期目标是在基础目标之上完成的。在这个阶段，我们将尝试进行较为准确的注视点定位，定位精度预计应在半径1cm以内（以13英寸屏幕为基准）。计划中我们将改进基础目标中的分类算法，使之可以处理连续的位置信息，同时我们将尝试加入一些桌面外部设备，如利用多个外接摄像头，以取得更多的数据，通过数据之间的互相校验，来提高注视点定位的精度。
在这个阶段，我们还将尝试完成一些除了注视点定位之外的眼神控制功能，可能包括注视唤醒、阅读自动滑动等，进一步丰富预期中眼动人机交互系统的功能。另外，我们将尽可能增加通用性，减少（或消除）新用户使用时的训练时间。我们仍将假设用户的头部在使用过程中没有移动。

预计实现算法：

* 1.相对位置计算：利用摄像头实时画面，根据提取出的数据计算出聚焦点位置和摄像头位置的平面距离。可能用到使用到卷积神经网络（CNN）。
* 2.注视判断：根据实时画面判断用户是否注视摄像头。当用户注视摄像头时，软件能收到提示信号。可能用到和短期目标中相近（也可能不同）的分类算法。
* 3.位置估计：根据多个相对位置（及到固定位置点的距离）估计出对应聚焦点平面位置。可能用到平面三点定位算法及各种误差降低手段。

#### 3.3.长期目标

长期目标旨在完成一个功能完整的设备以及配套驱动，能够对计算机进行简单操作（可能的操作包括移动光标、点击、唤醒、显示边缘菜单等）。这要求注视点定位更加精确，以及更多操作功能的完成。为了达成这个目的，我们可能会加入头戴式设备来与桌面设备进行配合。

重要的一点是，在前两个目标中，我们都假设了用户头部与屏幕的相对位置保持恒定，这在日常使用中很难保证。在我们的长期规划中，将初步解决这个问题。而头戴式设备与这个问题有着密不可分的联系，头戴式设备的设计和配套软件的设计将是长期目标中的重要一环。

预计实现算法：

* 1.头部定位：根据设备摄像头对头部相对于屏幕位置进行定位的算法。如果可能还将给出头部的偏向角。
* 2.近距离视线角：利用头戴设备上的摄像头或其它传感器，在近距离对视线偏向角进行计算，给出较精确数据。
* 3.操作检测：将以上各个算法的数据进行处理，从大量的实时数据中快速提取出相应操作。

## 技术可行性

该章将对项目目标中的提到的预计实现算法的实现方法进行探讨，分析项目可行性。

### 1.算法可行性分析
#### 1.1 项目需求分析

本项目内容为通过眼球运动控制鼠标，因此需要较快的响应速度以及准确率为评价指标。在目前阶段，我们还要考虑训练数据较少，硬件条件问题，因此需要综合考虑算法运用。

#### 1.2 主要挑战
 
图像识别看似很直接。但实际上包含很多挑战，人类可是经过数亿年的进化才获得如此强大的大脑，对于各种物体有着精准的视觉理解力。总体而言，我们想『教』会计算机去认识一类图，会有下面这样一些困难：
•	视角不同，每个事物旋转或者侧视最后的构图都完全不同
•	尺寸大小不统一，相同内容的图片也可大可小
•	变形，很多东西处于特殊的情形下，会有特殊的摆放和形状
•	光影等干扰/幻象
•	背景干扰
•	同类内的差异(比如椅子有靠椅/吧椅/餐椅/躺椅…)

#### 1.3 算法调研

##### 1.3.1 特征提取部份

众所周知，计算机不认识图像,只认识数字。为了使计算机能够“理解”图像，从而具有真正意义上的“视觉”，本章我们将研究如何从图像中提取有用的数据或信息，得到图像的“非图像” 的表示或描述，如数值、向量和符号等。这一过程就是特征提取，而提取出来的这些“非图像”的表示或描述就是特征。有了这些数值或向量形式的特征我们就可以通过训练过程教会计算机如何懂得这些特征， 从而使计算机具有识别图像的本领。
其中，可以通过归纳“词袋”（bag of words）,人工提取特征；也可以利用卷积，滤波等方法提取特征。工具如python的scikit-learn等有工具包用于特征提取，可用于基本机器学习算法。

##### 1.3.2 特征编码部分

对于提取的特征，进行编码后才能送入分类器。常见的如灰度编码，黑白编码，独热码，以及决策树的标签等等。

##### 1.3.3 分类器部分

本次实验中，我们会主要利用机器学习方法进行分类，并尝试少量深度学习如卷积神经网络。

###### 1.3.3.1 决策树

主要内容
决策树是机器学习中一类常见算法，其核心思想是通过构建一个树状模型来对新样本进行预测。树的叶结点是决策结果，而所有非叶结点对应于一个个决策过程。
基本流程
一般的，一颗决策树包含一个根结点、若干内部结点和若干个叶结点；叶结点对应于决策结果，其它每个内部结点（包括根结点）则对应一个属性测试。决策树根据内部结点的属性测试结果将该结点所包含的样本集按照属性测试的结果被划分到不同的子结点中。这是一种简单且直观的“分而治之”（divide-and-conquer）策略。
决策树学习的目的是为了产生一颗泛化能力强的决策树。
 
*(这里有一张图）*
 
上图是一棵结构简单的决策树，用于预测贷款用户是否具有偿还贷款的能力。
能力评估
	决策树的逻辑清晰，训练较简单，对于简单的分类问题可能性能较好。缺点在于，对于动态的跟踪，较难归纳特征；难以处理精确要求。算法性能可能随着精确度要求上升下降很多
  
###### 1.3.3.2 KNN（K-nearest-neighbor)

kNN算法的核心思想是如果一个样本在特征空间中的k个最相邻的样本中的大多数属于某一个类别，则该样本也属于这个类别，并具有这个类别上样本的特性。

基本流程
1.	算距离：给定测试对象，计算它与训练集中每个对象的距离
2.	找邻居：圈定距离最近的K个训练对象，作为测试对象的近邻
3.	做分类：根据这K个近邻归属的主要类别，来对测试对象分类
 
*这里有一张图

能力评估
KNN算法可以对图像进行降维，且特征提取过程可以十分简单，仅需对像素进行划分，对于简单的分类也十分常用。缺点在于其对图像意义没有关注，分类标准较为单一。

###### 1.3.3.3 卷积神经网络

主要内容
卷积神经网络（Convolutional Neural Network,CNN）是一种前馈神经网络，它的人工神经元可以响应一部分覆盖范围内的周围单元，对于大型图像处理有出色表现。 它包括卷积层(convolutional layer)和池化层(pooling layer)。

基本流程

卷积神经网络充分利用了输入由图像组成的事实，并以更合理的方式约束了体系结构。特别是，与常规的神经网络不同，ConvNet的各层具有三维排列的神经元：宽度，高度，深度。 （请注意，这里的词深度是指激活体积的第三维，而不是指完整神经网络的深度，可以指网络中的图层总数。）例如，CIFAR- 10是激活的输入量，并且体积具有32×32×3（分别为宽度，高度，深度）的尺寸。正如我们将很快看到的，一层中的神经元只会连接到它之前层的一个小区域，而不是以完全连接的方式连接到所有神经元。此外，CIFAR-10的最终输出层的尺寸为1x1x10，因为在ConvNet体系结构的末尾，我们会将整个图像缩减为沿深度维度排列的单个分数向量。这是一个可视化：

*这里有一张图*

左：常规h的3层神a经网络。右：一个CongvNet在n三个维度a（宽度，高度，深度）上排列它的神经元，如其中一个图层中的可视化。 ConvNet的每一层都将3D输入音量转换为神经元激活的3D输出音量。在这个例子中，红色输入层保存图像，所以它的宽度和高度将是图像的尺寸，并且深度将是3（红色，绿色，蓝色通道）。
ConvNet由图层组成。每个图层都有一个简单的API：它将输入的3D音量转换为具有可能有或没有参数的可微函数的输出3D音量。

用于构建ConvNets的层
正如我们上面所描述的，一个简单的ConvNet是一系列图层，ConvNet的每一层通过可微函数将一个激活体积转换为另一个激活体积。我们使用三种主要类型的层来构建ConvNet体系结构：卷积层，池化层和完全连接层（正如在常规神经网络中所见）。
示例架构：简单ConvNet可以具有体系结构[INPUT - CONV - RELU - POOL - FC]。
用一些具体的数字来说明：
INPUT [32x32x3]将保存图像的原始像素值，在这种情况下，图像的宽度为32，高度为32，并具有三个颜色通道R，G，B。
CONV层将计算连接到输入中局部区域的神经元的输出，每个计算它们的权重与它们在输入体积中连接的一个小区域之间的点积。如果我们决定使用12个滤镜，这可能导致[32x32x12]的volume。
RELU层将应用针对每个元素的激活函数，例如将MAX（0，x）的
阈值设为零。这会使volume大小不变（[32x32x12]）。
POOL层将沿着空间维度（宽度，高度）执行下采样操作，从而产生诸如[16x16x12]的volume。
FC（即完全连接）层将计算每个类别的分数，从而得到大小为[1×1×10]的数量，其中每个数字对应于每个类别的分数，例如10个类别的CIFAR-10。和普通的神经网络一样，顾名思义，这个层中的每个神经元都将连接到前一volume中的所有数字。
通过这种方式，ConvNets将原始图像逐层从原始像素值转换为最终的类别分数。请注意，某些图层包含参数，其他图层则不包含。具体而言，CONV / FC层执行转换，这些转换不仅是输入图像中的激活，而且也是参数（神经元的权重和偏差）的函数。另一方面，RELU / POOL层将实现一个固定的功能。 CONV / FC图层中的参数将使用梯度下降进行训练，以便ConvNet计算的类别分数与每个图像的训练集中的标签一致。

能力评估
相比传统神经网络，卷积神经网络减少网络各层之间的连接，同时又降低了过拟合的风险，简化了模型复杂度，减少了模型的参数。其并行处理图像特征的方式也更符合动物行为。同时，其对特征的提取全面深入，因此在应用中取得了较好的成果。然而，其对象主要是大型图像处理，依然需要大量数据防止过拟合，所需训练时间也较长。针对此问题，我们或许可以通过采用视频截图的方式来训练。





