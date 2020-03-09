
TensorFlow Convolutional Neural Networks (CNN) 
===================

![enter image description here](https://github.com/VickyFengYu/vickyfengyu.github.io/blob/master/image/tensorflow/cnn.png?raw=true)


There is an input image that we’re working with. We perform a series convolution + pooling operations, followed by a number of fully connected layers. If we are performing multiclass classification the output is softmax.

### <i class="icon-file"></i> Convolution Layer — The Kernel

![enter image description here](https://github.com/VickyFengYu/vickyfengyu.github.io/blob/master/image/tensorflow/cnn-convolution-layer.gif?raw=true)


In the above demonstration, the green section resembles our 5x5x1 input image, I. The element involved in carrying out the convolution operation in the first part of a Convolutional Layer is called the Kernel/Filter, K, represented in the color yellow. We have selected K as a 3x3x1 matrix.

```
Kernel/Filter, K = 
1  0  1
0  1  0
1  0  1
```

The Kernel shifts 9 times because of Stride Length = 1 (Non-Strided), every time performing a matrix multiplication operation between K and the portion P of the image over which the kernel is hovering.


### <i class="icon-file"></i> Pooling Layer

![enter image description here](https://github.com/VickyFengYu/vickyfengyu.github.io/blob/master/image/tensorflow/cnn-pooling-layer.jpeg?raw=true)


The Pooling layer is responsible for reducing the spatial size of the Convolved Feature. This is to decrease the computational power required to process the data through dimensionality reduction. Furthermore, it is useful for extracting dominant features which are rotational and positional invariant, thus maintaining the process of effectively training of the model.

Max Pooling also performs as a Noise Suppressant.


### <i class="icon-file"></i> Classification — Fully Connected Layer (FC Layer)

There are various architectures of CNNs available, like

> AlexNet

> VGGNet

> GoogLeNet

> ResNet


### <i class="icon-file"></i> BatchNormalization

```
@keras_export('keras.layers.BatchNormalization', v1=[])  # pylint: disable=missing-docstring
class BatchNormalization(normalization.BatchNormalizationBase):

  __doc__ = normalization.replace_in_base_docstring([
``` 

>**About setting `layer.trainable = False` on a `BatchNormalization layer:**
>
> The meaning of setting `layer.trainable = False` is to freeze the layer,
> i.e. its internal state will not change during training:
> its trainable weights will not be updated
> during `fit()` or `train_on_batch()`, and its state updates will not be run.
>
> Usually, this does not necessarily mean that the layer is run in inference
> mode (which is normally controlled by the `training` argument that can
> be passed when calling a layer). "Frozen state" and "inference mode"
> are two separate concepts.
>
> However, in the case of the `BatchNormalization` layer, **setting
> `trainable = False` on the layer means that the layer will be
> subsequently run in inference mode** (meaning that it will use
> the moving mean and the moving variance to normalize the current batch,
> rather than using the mean and variance of the current batch).

### <i class="icon-file"></i> class BatchNormalizationBase(Layer)

> Normalize the activations of the previous layer at each batch,
> i.e. applies a transformation that maintains the mean activation
> close to 0 and the activation standard deviation close to 1.
>
> Batch normalization differs from other layers in several key aspects:
>
> 1) Adding BatchNormalization with `training=True` to a model causes the
> result of one example to depend on the contents of all other examples in a
> minibatch. Be careful when padding batches or masking examples, as these can
> change the minibatch statistics and affect other examples.
>
> 2) Updates to the weights (moving statistics) are based on the forward pass
> of a model rather than the result of gradient computations.
>
> 3) When performing inference using a model containing batch normalization, it
> is generally (though not always) desirable to use accumulated statistics
> rather than mini-batch statistics. This is acomplished by passing
> `training=False` when calling the model, or using `model.predict`.

### <i class="icon-file"></i> x = tf.nn.relu(x)

> Computes rectified linear: `max(features, 0)