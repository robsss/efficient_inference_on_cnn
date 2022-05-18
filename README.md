# efficient_inference_on_cnn


## [cs231n 2017 lecture 15](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture15.pdf) 

### Algorithms for efficient inference

1. Pruning
2. Weight Sharing
3. Quantization
4. Low Rank Approximation
5. Binary/Ternary Net
6. Winograd Transformation 


## [Algorithms for efficient inference in convolutional neural networks](https://pure.tudelft.nl/ws/portalfiles/portal/96451845/doctoral_dissertation.pdf)

![image](https://user-images.githubusercontent.com/29032883/168947986-e9ebbc72-0406-4e1d-a514-a4b569e7ad36.png)

### Acceleration

Acceleration2 means reducing the number of operations used for inference by using fast algorithms [35–38]. Fast algorithms for convolution mainly include Fast
Fourier Transform (FFT) [35, 36], Strassen algorithm [37], and Winograd Transform [38].

#### Fast Fourier Transform (FFT)
#### Strassen algorithm
#### Winograd Transform

### Pruning

Pruning is a process to remove redundant connections or neurons, which does not contribute significantly to accuracy. Pruning can reduce both the number of parameters and the number of FLOPs required to compute DNNs.

#### second derivative of the loss function
#### the magnitude of the weights
#### the magnitude of the activations
#### LASSO penalty term

### Quantization

Quantization means reducing the bit-width to represent the weights and activations. In the forward propagation, the quantization error is the distance between fullprecision numbers and discrete values. There are mainly uniform quantization [46, 47] and non-uniform quantization [48, 49] to minimize the quantization error.

#### uniform quantization
#### non-uniform quantization


### Knowledge distillation

Knowledge distillation transfers the knowledge from a teacher model to a student model. The accuracy of the student model improves without additional
parameters or FLOPs needed to compute inference. 


### Efficient neural network architecture design

Current network engineering considers both the accuracy and efficiency of neural networks. Given an accuracy constraint, designing efficient neural network architecture means reducing the number of parameters and the number of FLOPs

#### Feature Reuse
#### 1x1 Convolution
#### Depthwise Separable Convolution
#### Attention Mechanism (design attentional module)
#### Neural Architecture search


## [深度学习模型轻量化(上)](https://www.cnblogs.com/wujianming-110117/p/12898599.html) [深度学习模型轻量化（下）](https://www.cnblogs.com/wujianming-110117/p/12898602.html)

移动端模型必须满足**模型尺寸小、计算复杂度低、电池耗电量低、下发更新部署灵活**等条件。

模型压缩和加速是两个不同的话题，有时候压缩并不一定能带来加速的效果，有时候又是相辅相成的。压缩重点在于减少网络参数量，加速则侧重在降低计算复杂度、提升并行能力等。模型压缩和加速可以从多个角度来优化。总体来看，个人认为主要分为三个层次：

1.  算法层压缩加速。这个维度主要在算法应用层，也是大多数算法工程师的工作范畴。主要包括结构优化（如矩阵分解、分组卷积、小卷积核等）、量化与定点化、模型剪枝、模型蒸馏等。
  - 结构优化
    - 矩阵分解
    - 权值共享
    - 分组卷积
      -  深度可分离卷积
      -  1x1卷积
    - 分解卷积
    - 其他
      - 全局平均池化代替全连接层
      - 1x1卷积核的使用
      - 使用小卷积核代替大卷积核（7*7=49 >> 3*3*2=18）
  - 量化
     - 伪量化（存储权重时使用低精度，推理的时候还原为高精度）
     - 聚类与伪量化
         1. 将大小相近的参数聚在一起，分为一类。 
         2. 每一类计算参数的平均值，作为它们量化后对应的值。 
         3. 每一类参数存储时，只存储它们的聚类索引。索引和真实值（也就是类内平均值）保存在另外一张表中 
         4. 推理时，利用索引和映射表，恢复为真实值。
     - 定点化（不同于伪量化，定点化不需要还原为浮点数。这需要框架实现算子的定点化运算支持）
  - 剪枝 （按照剪枝粒度可分为**突触剪枝、神经元剪枝、权重矩阵剪枝**）
      - 突触剪枝
      - 神经元剪枝
      - 权重矩阵剪枝
  - 蒸馏（student对teacher的拟合）
    - distillBERT
    - TinyBERT
 
2.  框架层加速。这个维度主要在算法框架层，比如tf-lite、NCNN、MNN等。主要包括编译优化、缓存优化、稀疏存储和计算、NEON指令应用、算子优化等

原文有更加详细的说明

3.  硬件层加速。这个维度主要在AI硬件芯片层，目前有GPU、FPGA、ASIC等多种方案，各种TPU、NPU就是ASIC这种方案，通过专门为深度学习进行芯片定制，大大加速模型运行速度。
  
  ![image](https://user-images.githubusercontent.com/29032883/168981365-faab5723-5bbb-4c51-9f61-6e48dfe77d23.png)
  
  ![image](https://user-images.githubusercontent.com/29032883/168981404-ecdb345d-9d52-4c23-92d0-7f4758ec8f3f.png)

