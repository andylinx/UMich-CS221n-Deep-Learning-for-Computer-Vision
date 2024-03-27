# Methods of optimization

### Stochastic Gradient Descent (SGD)  

use mini-batch (32/64/128) to do gradient descent



### SGD + Momentum	

continue moving in the general direction as the previous iterations

Build up “velocity” as a running mean of gradients 

 Rho gives “friction”; typically rho=0.9 or 0.99  

$v_{t+1} = \rho v_t + \nabla f(x_t)$

$x_{t+1} = x_t - \alpha v_{t+1}$



##### Nesterov Momentum

“Look ahead” to the point where updating using velocity would take us  

$v_{t+1} = \rho v_t - \alpha \nabla f(x_t+\rho v_t)$

$x_{t+1} = x_t + v_{t+1}$



#### AdaGrad

缩放每个参数反比于其所有梯度历史平方值总和的平方根

具有损失最大偏导的参数相应地有一个快速下降的学习率，而具有小偏导的参数在学习率上
有相对较小的下降。

净效果是在参数空间中更为平缓的倾斜方向会取得更大的进步。

然而，经验上已经发现，对于训练深度神经网络模型而言，从训练开始时积累梯度平方会导致有
效学习率过早和过量的减小。



#### RMSProp

AdaGrad 根据平方梯度的整个历史收缩学习率，可能使得学习率在达到这样的凸结构前就变得太小了。

RMSProp算法不是像AdaGrad算法那样暴力直接的累加平方梯度，而是加了一个衰减系数来控制历史信息的获取多少。



### Adam

![image-20240327184454163](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240327184454163.png)

对超参数的鲁棒性更强



## Second-Order Optimization

Problem : Hessian has O(N^2) elements Inverting takes O(N^3)N = (Tens or Hundreds of) Millions

#### optimizations：

BGFS  

L-BFGS  ：Does not form/store the full inverse Hessian  
