# Training Neural Networks  



## 	Activation Function

##### Sigmoid Function

problems:

1. Saturated neurons “kill” the gradients, making it hard to learn (Most problematics)
2. Sigmoid outputs are notzero-centered (Minibatch may help)

3. compute expensive (for cpu device)



##### tanh

still saturatred neurons “kill” the gradients, making it hard to learn



##### ReLU

efficient computationally

converges faster



problem: not zero centered



value less than zero, it will kill it with no gradient 

to solve this, Leaky ReLU is produced (0.01x for negative x)



##### PReLU

learn the hyperparameter 0.01 instead

maybe seperate for each value



##### ELU

zero centered

add some robustness to noise



problem:

hyperparameter

exp() required



**SELU** help it converges, for very very deep network.





### **Actually, better activation function does not help much!!**

1~2 % difference

##### So, just use ReLU.

##### If trying to squeeze the last 0.1% and try different functions.



## Data processing

##### Normalization:

1. substract by the mean
2. divided by std

this can be done either overall or per channel

can make it less sensitive to changes in weight matrix, making it eaiser to optimize



Other methods: PCA and Whitening

making covariance matrix diagonal / Indentity



## Weight Initialization

 Use gaussian random numbers for small network.

#### Xavier 

random.randn(Din, Dout) / sqrt(dim)

bad for ReLU

#### Kaiming / MSRA 

random.randn(Din, Dout) * sqrt(2 / dim)



##### For Residual Networks

only initalize the first conv 

second to be zero

to prevent the variance grows



## Regularization

#### L2 regularization / L1 / L1+L2



#### Dropout

randomly set some neurons to zeros

usually p = 0.5

to prevent co-adaptation of features



###### For test time:

we want it to give stable answers 

by average out the randomness at test-time

$y= \int p(z)f(x,z)dz$

by considering all the possibilitiesa

scale the activations for each neuron

###### Inverted dropout -> better implementation

![image-20240402142102625](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240402142102625.png)

###### ususally put after fclayers



Batch normalization add randomness by choosing small batches.



### Data argumentation

flips, random crops, scales

it also adds randomness to the dataset

translation

rotation

stretching

shearing

lens distortions

....



#### Other Regularization

DropConnect

Fractional Pooling

Stochastic Depth

Cutout

Mixup







## Learning Rate

#### Deacy 

reduce the learning rate at a few fixed points



But, more hyperparameters are introduced!

So, we can use heuristic ways, to plot the loss, when it comes to a plateaus just decay the lr.



####  Cosine

$a_t =\frac{1}{2} a_0(1+\cos(t\pi /T)) $



##### Linear



##### Inverse Sqrt

$a_t = a_0 /\sqrt{t}$ 



##### Constant

Work quite well for many problems!!!







## How to choose hyperparameters?

1. check initial loss

2. overfit a small sample (get 100% accuracy)

   check the architecture, lr , weight initialization  

   to figure out whether loss goes down, nan / inf occurs ...

   

3. use all the data to find lr that make loss go down

4. Corase grid, train several epochs

5. refine grid, train longer

6. look at loss and accuracy curve

   If acc still goes up ,train longer

   If exists huge gap between train/test -> overfitting -> regularization / early stopping!

   If no gap, train longer/ use larger model.

   



## Model Ensembles

1. train multiple independent models
2. At test time average their results



Another methods: Use multiple snapshots of a single model during training.

##### Polyay average

keep a moving average of parameter vector and use at test time





## Transfer Learning

1. train on ImageNet
2. Use CNN as a feature extractor(Remove the last FClayer, Freeze the rest)



Just add SVM / logestic regression as the last layer!

CNN is used as a feature extractor!

Don't forget to perfom data argumentation after feature extraction.



3. If we have a bigger dataset, we can fine-tuning the model (continue training the model on the new dataset) 

   Trick : reduce lr a lot,

   

## Distributed Training



#### Model Parallelism

bad idea : gpus spend lots of time waiting, costing lots of time communicating between gpus



#### Data Parallelism

by dividing the batch -> less need for communications

only at the end, exchange the sum, gradients, update!



#### Large-Batch Training

scale the learning rate  $\rightarrow k \alpha$ 

Trick : lr warmup to avoid the initial explosion of big gradient!





