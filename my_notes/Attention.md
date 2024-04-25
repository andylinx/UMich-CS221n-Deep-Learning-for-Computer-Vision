# Attention

### For Sequence-to-Sequence With RNNs and Attention

Compute alignment scores

 $e_{t,i} = f_{att}(s_{i-1},h_i)$ $f_{att}$ is a MLP

apply a softmax to scale them to a probability distribution

Computer context vector as linear combination of hidden states

$c_t = \sum_ia_{t,i}h_i$

Use context vector in decoder : $s_t = g_U(y_{t-1}, h_{t-1},c_t)$

Intuition : Context vector attends to relevant part of the input sequences

![image-20240418172737073](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240418172737073.png)



However, we didn't use the fact that input vector is an ordered sequence.

 

## Image Captioning with RNNs and Attention



Use CNN to compute a gird of features for an image

compute alignment scores $e = f_{att}(s_{t-1},h)$-> softmax attention weights

 ![image-20240418202653095](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240418202653095.png)

![image-20240418203329469](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240418203329469.png)



##### Positional encoding

concatenate special positional encoding $p_j$ to input vector $x_j$ 



##### Masked self-attention layer

Prevent vectors from looking at future vectors

By setting their alignment scores to -inf 



##### Multi-head self attention layer

Use H independent Attention Heads in parallel



![image-20240418204157347](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240418204157347.png)

# Transformer for CV

![image-20240418205104876](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240418205104876.png)

![image-20240418205208545](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240418205208545.png)

![image-20240418205322305](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240418205322305.png)

