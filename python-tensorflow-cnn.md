
TensorFlow Convolutional Neural Networks (CNN) 
===================

There is an input image that we’re working with. We perform a series convolution + pooling operations, followed by a number of fully connected layers. If we are performing multiclass classification the output is softmax.

### <i class="icon-file"></i> Convolution Layer — The Kernel

In the above demonstration, the green section resembles our 5x5x1 input image, I. The element involved in carrying out the convolution operation in the first part of a Convolutional Layer is called the Kernel/Filter, K, represented in the color yellow. We have selected K as a 3x3x1 matrix.

```
Kernel/Filter, K = 
1  0  1
0  1  0
1  0  1
```

The Kernel shifts 9 times because of Stride Length = 1 (Non-Strided), every time performing a matrix multiplication operation between K and the portion P of the image over which the kernel is hovering.


### <i class="icon-file"></i> Pooling Layer

The Pooling layer is responsible for reducing the spatial size of the Convolved Feature. This is to decrease the computational power required to process the data through dimensionality reduction. Furthermore, it is useful for extracting dominant features which are rotational and positional invariant, thus maintaining the process of effectively training of the model.

Max Pooling also performs as a Noise Suppressant.


### <i class="icon-file"></i> Classification — Fully Connected Layer (FC Layer)

There are various architectures of CNNs available, like

> AlexNet

> VGGNet

> GoogLeNet

> ResNet

