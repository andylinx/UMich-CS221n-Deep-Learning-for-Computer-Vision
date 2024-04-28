# Generative models

##### Supervised vs. Unsupervised

##### Discriminative Model vs. Generative Models vs. Conditional Generative

Discriminative: only label compete for probability mass, no competition between images

Generative: images compete with each other for probability mass



#### usage

Discriminative:

1. Feature learning
2. Assign labels to data

Generative: 

1. detect outliers
2. feature learning
3. sample to generate new data

Conditional Generative:

1. assign labels while rejecting outliers
2. generate new data conditioned on input labels



![image-20240427113157274](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240427113157274.png)



## Autoregressive 

**Goal**: Write down an explicit function for $p(x) = f(x,W)$

We can break down the probability function to get $p(x) = p(x_1,x_2,...,x_T) = \Pi_{t=1}^Tp(x_t|x_1,x_2,...x_{t-1})$

We can use RNN to train a density function



### PixelRNN

generate image pixels one at a time, staring at the upper left corner

compute a hidden state for each pixel that depends on hidden state and RGB values from the left and above (LSTM recurrence)

$h_{x,y} = f(h_{x-1,y},h_{x,y-1},W)$

At each pixel, predict red, then blue, then green

Each pixel depends implicitly on all pixels above and to the left



**Problem**: Really slow both training and testing



### PixelCNN

Dependency on previous pixel now modeled using a CNN over context

on new CIFAR images



## Autoregressive Models: PixelRNN/CNN

Pros:

1. can explicitly compute likelihood
2. gives good evaluation metric
3. good samples

Cons:

1. sequential generation -> slow



## Variational Autoencoders

VAE define an intractable density.

we can optimize a lower bound on this density instead.

### (non-variational) Autoencoders

Features should extract useful information that can use for downstream tasks



**Problem**: how can we learn this feature transform from raw data?

**idea**: use the features to reconstruct the input data with a decoder

**loss**: L2 distance between input and reconstructed data



### Variational Autoencoders

1. learn latent features z from raw data
2. sample from the model to generate new data



![image-20240427172126782](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240427172126782.png)

How to train this model: maximize the likelihood of data

However, we can't get full access to all the x

so, we need to find a computable lower bound of the likelihood

Hopefully, with the growing of lower-bound, the real likelihood will increase

![image-20240428163954685](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240428163954685.png)

 

Process:

1. run input data through encoder to get a distribution over latent codes
2. encoder output should match the prior $p(z)$

​		Here, we assume the distribution we learn and the prior $p(z)$ are both diagonal Gaussian distribution for computational convenience.

3. sample code z from encoder output
4. run sampled code through decoder to get a distribution over data samples
5. original input data should be likely under the distribution output from step 4

Step 2, 5 are the two terms of loss we try to minimize



## Generative Adversarial Networks

**Setup**: Assume we have data $x$ drawn  from distribution $p_{data}(x)$. We want to sample from  $p_{data}(x)$.



**Idea**: Introduce a latent variable z with simple prior $p(z)$.

sample z from $p(z)$ and pass to a Generator Network $x = G(z)$

Then x is a sample from the generator distribution $p_G$ , we want $p_G = p_{data}$ 



We train the Generator Network to convert z into fake data x sampled from $p_G$

by fooling the discriminator D

Train D to classify data as real or fake

We will train the two networks jointly, they are fighting against each other.

#### loss

![image-20240428184511584](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240428184511584.png)



**problem**: At the beginning of training, vanishing gradients for G

**solution**: change minimize log(1-D(G(z))) to maximize -log(D(G(z))) then G gets strong gradients at the beginning of training ! **nice idea**



We can do some math calculations to prove GAN can get the optimal $p_{data}$.

But there are still caveats about the capability of our fixed architecture to reach the optimal and its convergence.



##### DC-GAN

interpolating between points in latent z space



##### We can even do latent vector math!



#### Conditional GANs

we can use conditional Batch Normalization

learn parameters for different labels

##### Spectral Normalization

we can generate images in specific labels

....

