# CNN



### Convolutional Layer

We use a filter to slide over the image spatially (computing dot products)

![请添加图片描述](https://img-blog.csdnimg.cn/direct/9a45e09c6f484a69bc6c333c693dfe05.png)

Interspersed with activation function as well



What it learns?

First-layer conv filters: local image templates (Often learns oriented edges, opposing colors)  



##### Problems:

1. For large images, we need many layers to get information about the whole image

​		Solution:  Downsample inside the network

2. Feature map shrinks with each layer

   Solution: Padding : adding zeros around the input



### Pooling layer

-> downsampling

Without parameters that needs to be learnt.

ex:

max pooling

Aver pooling

....





### FC layer(Fully Connected)

The last layer should always be a FC layer.



### Batch normalization

we need to force inputs to be nicely scaled at each layer so that we can do the optimization more easily.

Usually inserted after FC layer / Convolutional layer, before non-linearity



#### Pros:

make the network easier to train

robust to initialization

#### Cons:

behaves differently during training and testing 



![请添加图片描述](https://img-blog.csdnimg.cn/direct/ceb8ed0e015a4a2cb484c3c56b978e01.png)

###### Implementation in Assignment2

求反向传播的方式，画图求解，倒着处理每一条边加起来，可以从两个维度开始推广，并且通过矩阵的size来进行助力。





## Architechtures (History of ImageNet Challenge)



#### AlexNet

Input 3 * 277 * 277

Layer filters 64 kernel 11 stride 4 pad 2



We need to pay attention to the **Memory, pramas, flop** size

![请添加图片描述](https://img-blog.csdnimg.cn/direct/827f4114c57945a19b9263e033df21d0.png)

##### ZFNet

larger AlexNet



#### VGG

Rules:

1. All conv 3*3 stride 1 pad 1
2. max pool 2*2 stride 2
3. after pool double channels



Stages:

conv-conv-pool

conv-conv-pool

conv-conv-pool

conv-conv-[conv]-pool

conv-conv-[conv]-pool



### GoogLeNet 

Stem network: aggressively downsamples input 

Inception module:

![请添加图片描述](https://img-blog.csdnimg.cn/direct/c1b963d5035744e08b8cbee655f91dfe.png)

Use such local unit with different kernal size

Use 1*1 Bottleneck to reduce channel dimensions

 

At the end, rather than flatting to destroy the spatial information with giant parameters

GoogLeNet use average pooling: 7 * 7  * 1024 -> 1024

There is only on FClayer at the last.



**找到瓶颈位置，尽可能降低需要学习的参数数量/内存占用**



Auxiliary Classifiers:

To help the deep network converge (batch normalization was not invented then): Auxiliary classification outputs to inject additional gradient at lower layers  





### Residual Networks

We find out that, somtimes we make the net deeper but it turns out to be underfitted.

Deeper network should strictly have the capability to do whatever a shallow one can, but it's hard to learn the parameters.



So we need the residual network!



![请添加图片描述](https://img-blog.csdnimg.cn/direct/81195c63e3cb476d99dd386ec6973f10.png)

This can help learning Identity, with all the parameters to be 0.



The still imitate VGG with its sat b



### ResNeXt

Adding grops improves preforamance with same computational complexity.



### MobileNets

reduce cost to make it affordable on mobile devices



## Transfer learning

We can pretrain the model on a dataset.

When applying it to a new dataset, just finetune/Use linear classifier on the top layers.

Froze the main body of the net.



**有一定争议，不需要预训练也能在2-3x的时间达到近似的效果**
