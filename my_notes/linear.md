# Revision for Assignment 1

### KNN 

##### Difficiencies:

1. Train $O(1)$ Predict $O(n)$
2. ignore the position information, as well as the connection between pixels



##### K-fold validation





### Linear Classifier

##### Loss funtions

1. SVM loss: $\sum_{j \neq y_i} \max(0,s_j-s_{y_i}+1)$

​      Intuition: If the probability of the correct label is far beyond(1) the others, no loss added

​					    Otherwise, add the distance into the loss

​	2.softmax loss: $L_i = - \log(\frac{exp(s_{y_i})}{\sum exp(s_j)})$

​	Intuition: result from maximum likelihood estimation.



 

### Q1: What if we find a W s.t. SVM loss = 0?

这会导致 $kW$ 都能使loss为0，所以也体现了Regularization 的重要性。



### Q2: Why nan appear?



#### Numerical Instability

在计算机中表示实数时，几乎总会引入一些近似误差。在许多情况下，这仅仅是舍入误差。舍入误差会导致一些问题，特别是当许多操作复合时，即使是理论上可行的算法，如果在设计时没有考虑最小化舍入误差的累积，在实践时也可能会导致算法失效。

A2在实现softmax的时候，就涉及了这个问题：

$softmax(x) = \frac{e^{x_i}}{\sum_{j=1}^n e^{x_j}}$

如果所有的 $x_i$ 都是常数 c 的话，正常输出应该都是 $\frac{1}{n}$，但当$c \rightarrow -\inf$ 的时候，就会发生下溢(underflow)：趋近于0的一个很小的正数，作为分母可能会导致 $nan$。同样的当 $ c \rightarrow \inf$ 的时候会发生上溢(overflow)，导致$nan$的出现。

##### 解决方法

$x_i -= \max\{x_j\}$，这样最大项是0，不会上溢，分母存在1这项，不会下溢！

