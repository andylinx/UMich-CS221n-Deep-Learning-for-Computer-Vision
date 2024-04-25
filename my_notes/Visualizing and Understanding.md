# Visualizing

#### Filters

first layer!

visualize the filter of the very first layer as image 

shows some colors and oriented edges



### Last Layer : Nearest Neighbors

Used after nn, applied to the 4096 dims vector to learn about its neighbors



#### Dimensionality Reduction

PCA : linear

t-SNE : non-linear -> 2d 



### Visualizing Activations

gray scale images -> to find out relu focus on which part of the image



### Maximally Activating Patches

pick a layer and a channel 

run many images through the network, record the values of the chosen channel

visualize the maximal activation patches

it shows what does this filter is looking for



## Which part/pixel matters?

##### Saliency via occlusion

mask part of the image before feeding to CNN, check how much it changed

it can be used to do unsupervised segmentation





##### Backprop

compute the gradient of class score w.r.t. the image pixels



### Intermediate Feature via (guided) backprop

find the part of an image that a neuron responds to



### Gradient Ascent

generate a synthetic image that maximally activate a neuron



like the procedure of generating adversarial datas

so, we also need L2 norm to make it simpler



