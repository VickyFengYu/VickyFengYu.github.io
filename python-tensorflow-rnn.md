
TensorFlow Recurrent Neural Networks (RNN) 
===================

Recurrent neural networks are particularly useful for evaluating sequences, so that the hidden layers can learn from previous runs of the neural network on earlier parts of the sequence.

For example, the following figure shows a recurrent neural network that runs four times. Notice that the values learned in the hidden layers from the first run become part of the input to the same hidden layers in the second run. Similarly, the values learned in the hidden layer on the second run become part of the input to the same hidden layer in the third run. In this way, the recurrent neural network gradually trains and predicts the meaning of the entire sequence rather than just the meaning of individual words.

### <i class="icon-file"></i> pad_sequences

```
keras.preprocessing.sequence.pad_sequences(x_train, maxlen=max_review_len)
```

>def pad_sequences(sequences, maxlen=None, dtype='int32',
>                  padding='pre', truncating='pre', value=0.):
>                  
>   Pads sequences to the same length.
>
>   This function transforms a list of
>   `num_samples` sequences (lists of integers)
>   into a 2D Numpy array of shape `(num_samples, num_timesteps)`.
>   `num_timesteps` is either the `maxlen` argument if provided,
>   or the length of the longest sequence otherwise.


### <i class="icon-file"></i> from_tensor_slices

```
tf.data.Dataset.from_tensor_slices((x_train, y_train))
```

>def from_tensor_slices(tensors):
> 
>   Creates a `Dataset` whose elements are slices of the given tensors.
>
>   The given tensors are sliced along their first dimension. This operation
>   preserves the structure of the input tensors, removing the first dimension
>   of each tensor and using it as the dataset dimension. All input tensors
>   must have the same size in their first dimensions.


### <i class="icon-file"></i> shuffle & batch

```
db_train = db_train.shuffle(1000).batch(batchsz, drop_remainder=True)
db_test = db_test.batch(batchsz, drop_remainder=True)
```

>def shuffle(self,
>            buffer_size: Any,
>            seed: Any = None,
>            reshuffle_each_iteration: Any = None) -> DatasetV1Adapter
>Randomly shuffles the elements of this dataset.
>This dataset fills a buffer with buffer_size elements, then randomly samples elements from this buffer, replacing the selected elements with new elements. For perfect shuffling, a buffer size greater than or equal to the full size of the dataset is required.

>def batch(self,
>          batch_size: Any,
>          drop_remainder: bool = False) -> DatasetV1Adapter
>Combines consecutive elements of this dataset into batche
>
>The components of the resulting element will have an additional outer dimension, which will be batch_size (or N % batch_size for the last element if batch_size does not divide the number of input elements N evenly and drop_remainder is False). If your program depends on the batches having the same outer dimension, you should set the drop_remainder argument to True to prevent the smaller batch from being produced.

### <i class="icon-file"></i> layers.Embedding

>Turns positive integers (indexes) into dense vectors of fixed size.
>e.g. [[4], [20]] -> [[0.25, 0.1], [0.6, -0.2]]
>This layer can only be used as the first layer in a model.

### <i class="icon-file"></i> layers.SimpleRNNCell

>Cell class for SimpleRNN.
>See [the Keras RNN API guide](https://www.tensorflow.org/guide/keras/rnn ) for details about the usage of RNN API.
>This class processes one step within the whole time sequence input, whereas tf.keras.layer.SimpleRNN processes the whole sequence

### <i class="icon-file"></i> layers.SimpleRNN

>Fully-connected RNN where the output is to be fed back to input

### <i class="icon-file"></i> tf.unstack(x, axis=1)

>def unstack(value: Any,
>            num: Any = None,
>            axis: int = 0,
>            name: str = "unstack") -> List[Tensor]
>Unpacks the given dimension of a rank-R tensor into rank-(R-1) tensors.
>Unpacks num tensors from value by chipping it along the axis dimension. If num is not specified (the default), it is inferred from value's shape. If value.shape[axis] is not known, ValueError is raised.

### <i class="icon-file"></i> layers.Dense(1)

>Just your regular densely-connected NN layer.
>Dense implements the operation: output = activation(dot(input, kernel) + bias) where activation is the element-wise activation function passed as the activation argument, kernel is a weights matrix created by the layer, and bias is a bias vector created by the layer (only applicable if use_bias is True).

### <i class="icon-file"></i> tf.sigmoid(x)

>Computes sigmoid of x element-wise.
>Specifically, y = 1 / (1 + exp(-x)).

### <i class="icon-file"></i> Adam

```
keras.optimizers.Adam(0.001),

Construct a new Adam optimizer.
```

### <i class="icon-file"></i> tf.losses.BinaryCrossentropy()

```
def __init__(self,
             from_logits: bool = False,
             label_smoothing: int = 0,
             reduction: Any = losses_utils.ReductionV2.AUTO,
             name: str = 'binary_crossentropy') -> None
             
Computes the cross-entropy loss between true labels and predicted labels.
Use this cross-entropy loss when there are only two label classes (assumed to be 0 and 1). For each example, there should be a single floating-point value per prediction.
In the snippet below, each of the four examples has only a single floating-pointing value, and both y_pred and y_true have the shape [batch_size].
```

### <i class="icon-file"></i> model.compile()

```
Configures the model for training.
```

### <i class="icon-file"></i>  model.fit()

>Trains the model for a fixed number of epochs (iterations on a dataset).


### <i class="icon-file"></i> model.evaluate()
 
>Returns the loss value & metrics values for the model in test mode.
Computation is done in batches.
 
