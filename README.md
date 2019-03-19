# Key Takeaways
--------------

## 1. Steps in Training a Neural Network
Let's say there are 100 images and 20 total batches. This gives a ```batch size = 5``` or in other words ```5 images/ batch```.

### 1.1 Forward Propagation

One batch is passed through the neural network to calculate the loss function which constitutes the steps in forward propagation. The batch size is the number of forward propagations. So in the above example, there would be 5 forward propagation steps for each batch. And a total of 100 forward propagation steps in a complete epoch.

### 1.2 Backward Propagation
Next step is back propagation to minimize the loss function. This results in updated weights and biases. The back propagation for the entire batch is done at a single go. So, there would be a total of 20 back propagations in one epoch

-------
## 2. Formula for the size of the output:
$$ N_{output} = \frac{N_{input} +k - 2p}{s}+1 $$
where,
 $N_{output}$ = ```dimension of the output image```
 $N_{input}$ = ```dimension of the input image```
 $k$ = ```dimension of the kernel```
 $p$ = ```padding```
 $s$ = ```stride```

-------
## 3. Receptive Fields
A receptive field of a layer is the size of the input image visible to each pixel of the layer. The visibility might be through multiple layers in between.

A $3*3$ convolution kernel with ```stride=1``` and ```padding=0``` applied on a $100*100$ input image has an output of $98*98$. Each pixel of the output image has a ```receptive field = 3*3```.  However, the complete output image would have a ```receptive field = 100*100```. Similarly a $5*5$ sub-image of the output image would have a ```receptive field = 7*7```.

-------
## 4. Some key points in CNN:

### 4.1 Number of layers
We add as many layers as required to reach the required receptive field

### 4.2 $1*1$ convolution layer
* We almost always use a $3*3$ filter unless in cases where we want to reduce the number of channels (for which we use a $1*1$ filter)
* It is computationally much efficient as compared to a $3*3$ to reduce the number of channels.
* To reduce the number of channels
* Combine a large number of channels into smaller relevant ones

### 4.3 Max-Pooling layer
* To increase the effective receptive field
* To reduce the resolution of the layers
* To reduce the number of layers required in a Network
* We always use $2*2$ max pooling, else we would lose too much information

### 4.4 DON'Ts
* Do not use a $1*1$ convolution layer to increase the number of channels
* Max Pooling:
  * Do not use a Max Pooling layer too early. Have at least 2 convolution layers before applying Max-Pooling
  * Do not use it just before final prediction layers because it will reduce the rich information in the last layers required for accurate predictions
* Obsolete uses
  * Dropouts
  * Fully Connected Layers
    * They lose all spatial information required in CV domain
    * Add a lot more parameters than Convolution and hence slower to process
    * If we use FC we force our network to use only a specific size of input image, but we want a network which can process images of all sizes

--------
## 5. Fully Connected Layer vs ```1*1``` Convolution
An FC layer involves far more number of parameters and hence back propagation is slower. However, the calculations in forward propagation are lesser but they do not improve timings much. Below example shows the difference in the number of parameters between the two processes.
### FC Layer:
There are a total of 32000 parameters involved in the below example:
* $ Image_{none * 10 * 10 * 32} \xrightarrow[\text{no parameters}]{\text{flatten or reshape}} Output^{1}_{none * 3200} $
<br>
* $ [Output^1_{none*3200}][W_{3200*10}]\xrightarrow[\text{32,000 parameters}]{\text{convolution}}Output^2_{none*10} $
### ```1*1``` Convolution
* $ [Image_{none*10*10*32}][W_{1*1*32*10}]\xrightarrow[\text{ 320 parameters}]{\text{convolution}} Output^1_{none * 1 * 1 * 10}$
<br>
* $ Output^1_{none*1*1*10} \xrightarrow[\text{no parameters}]{\text{flatten or reshape}}Output^2_{none*10} $

------------
## 6. Things to revise:
* Dilated convolution
* Deconvolution or fractionally strided or transpose Convolution
* Pixel Shuffle
* Depth-wise convolution
