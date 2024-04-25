# Recurrent Neural Network

Process Sequences!

Sequential processing of non-sequential data



$h_t = f_W(h_{t-1},x_t)$

new state is calculated by f on old state and input $x_t$

$y_t = f_{W_y}(h_t)$

and output is a applying another function f on h_t



**same function and the same set of parms are used at every time step**



#### Vanilla RNN

![image-20240423190844069](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240423190844069.png)



####  Truncated Backpropagation Trough Time

Backpropagation through time takes too much memory for long sequences

Instead, do the backpropagtion in truncated chunks.

Make it feasible to train



### LSTM （Long Short Term Memory）

![image-20240410114637715](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240410114637715.png)



一个LSTM很详细的讲解！

 https://blog.csdn.net/qian99/article/details/88628383