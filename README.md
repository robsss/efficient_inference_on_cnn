# efficient_inference_on_cnn


## cs231n 2017 lecture 15 

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


