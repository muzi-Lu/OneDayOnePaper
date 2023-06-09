#  A Probabilistic Framework for Visual Localization in Ambiguous Scenes

## Date:23_4_11至23_4_12

## Abstract

视觉定位的解决方案使得智能机器人在丢失定位的时候通过当前观察进行重定位。但是模糊不确定的多场景的出现使得我们只输出一个相机位姿的假设不够合理。我们提出了一个概率模型框架对于给定的一张图片输出其相机位姿的后验概率，我们通过创造了一个新的位姿回归器从预测的分布中来进行变分推理，我们的方法优于目前在模糊重复场景下的方法。



## 1. Introduction

视觉定位





## 2. Related Work

回归方法尝试解决的问题就是通过找到图片到位姿的映射来快速解决，他主要提升的地方是神经网络所带来的运动模糊的提升。在早期的工作中，Shotton等人提了场景坐标回归的想法，也即把像素点和场景坐标关联起来，然后通过RANSAC and Kabsch算法来进行回归位姿。然后直接位姿回归的问题初步提出方案是在2015年的PoseNet,他们的主要想法就是通过一张图片直接回归我的位姿，也即图片特征和地图在我的神经网络里面共同进行编码。

最近新的工作也有很多好的想法。Naseer（老文章了）提出了RGB图片可以产生新的不同视角来对数据集进行补充，相同思想的还有运用Nerf的Lens（2022 CoRL）。

和我们工作最近的也是Deng等人提出的Deep Bingham Network还有16年的Baysian Conv Nerual Network,其中BCN可以去预测位姿的不确定性，虽然他对于复杂分布的预测还是很有限（Bingham分布里面提及，具体的请去看Deep Bingham Network），从本质上而言，**Deng等人的工作虽然可以产生不同模态的分布，但是对于这个工作的混合模型的下行而言，是很难从挑选正确的模态进行预测。为了解决这种问题，他们提出了一种Winner takes all的策略来监督最好的一个预测。**但是我们的工作不同于预测一系列的参数，我们采取了变分的模式，从理论上来看，他可以通过学习产生任意形状的位姿分布。

与我们工作相似的还有Murphy等人的工作（***这篇文章周末有空可以看一下***），通过MLP预测给定SO（3）旋转的的任意概率密度，我们的目的也是预测任意分布，但是我们提出的是一个采样的方法，也就是在潜在空间的样本转换为SE（3）的位姿。从逻辑上来说，他简化了推断，因为他不需要很多查询支持来找到这个分布的模型，从方法上来说是直接采样的。

## 3. Method

从方法上说两个步骤：



1. 推断在这个场景中对视觉定位有用的特征的潜在空间位姿分布。

2. 执行随机变量变换以获得查询图像的相机位姿分布。

   什么是随机变量变换：一个随机变量通过函数映射到另一个随机变量。

   随机变量转换（Variable Transformation）是指将一个随机变量通过一个函数映射成另一个随机变量的过程。在概率统计学中，随机变量转换常常被用于将一个随机变量的概率分布转换成另一个随机变量的概率分布。这种转换可以帮助我们更好地理解和分析数据，并且可以使一些复杂的分布更容易处理。

   例如，在计算机视觉领域中，我们可能希望通过对摄像机姿态的随机变量进行变换来获得查询图像的摄像机姿态分布。这个随机变量转换可以通过一个函数来实现，这个函数将查询图像的特征向量作为输入，并映射到摄像机姿态分布的空间中。这样，我们就可以在这个分布中采样，从而生成一些与查询图像相似的姿态。

   那么可以通过一个具体的映射函数f从潜在空间的来把映射到SE（3），从潜在空间的后验分布中提取样本：y=f(z), z~p(z|x)来实现



3.1 定式：

让从相机位姿y（SE(3)）拍出来的X（图片）,在定位任务中，场景是事先已知的。













































​	

​	

​	、、	、





## 4. Proposed Model





## 5. Deeply modeling μ(·) and Λ(·)