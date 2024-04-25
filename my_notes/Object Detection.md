# Object Detection

Output:

1. category label from fixed, known set of categories
2. bounding box (x, y, width, height)



If only one object is needed to be detected -> add FC layer to the Net pretrianed on ImageNet



### Sliding Window

apply a CNN to many different crops of the image, CNN classifies each crop as object / backgroud

but too many windows!! and may detect repeatedly



we need region proposals to find a small set of boxes that are likely to cover all the objects

"Selective Search" quick to generate 2000 regions 



### R-CNN : Region-Based CNN 

1. Region proposals
2. warped the image to fixed size 224*224
3. forward each region through ConvNet independently
4. output a classification score and also a Bbox of 4 numbers, using the following algorithm

![image-20240413201508200](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240413201508200.png)



#### Measurement of boxes (IoU)

$IoU = \frac{\text{Area of Intersection}}{\text{Area of Union}}$

$IoU > 0.5$ is decent

$IoU > 0.7$ pretty good

$IoU > 0.9$ perfect

#### Overlapping Boxes: Non-Max Suppression (NMS)

1. select next highest-scoring box
2. eliminate lower-scoring boxes with IoU>0.7 (with the box we selected in step1)
3. If any boxes remain goto 1



### Evaluating Object Detectors: mAP(Mean Average Precision)

1. run detector on all test images + NMS

2. for each category, computer AP = area under precision vs Recall Curve

    	1.	for each detection (high -> low)
    		1.	If it matches some GT(Ground-Truth) box with IoU>0.5 mark it as positive and eliminate the GT
    		2.	otherwise mark is as nagative
    		3.	plot a point on PR curve
    	2.	AP = area under PR Curve

3. mAP = average of AP for each category

4. COCO mAP: compute mAP for each IoU threshold and take average

   



How to get AP = 1.0 -> hit all GT boxes with IoU > 0.5, no false positive ranked above any true positive





## Fast R-CNN

1. ConvNet (Backbone network)-> convolutional features for entire high resolution image
2. Regions of Interest (Rols)
3. Crop + Resize features
4. Per-Region Network (light-weight -> fast)
5. output category and box

 

### Cropping Features: Rol Pool

1. project proposal onto features
2. snap to gird cells
3. divide into 2*2 gird of (roughly) equal subregions
4. max-pool within each subregions
5. output the region features (always the same size even if we have different sizes of input regions)

## Rol Align

Rol Align -> better align to avoid snapping 

![image-20240415170750208](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240415170750208.png)

#### Faster R-CNN

Insert Region Proposal Network (RPN) to predict proposals from features

after the backbone network -> RPN -> regional proposals



Imagine an anchor box of fixed size at each point in the feature map

At each point predict whether the corresponding anchor contains an object 

for positive boxes, also predict a box transform to regress from anchor box to object box



Use k different anchor boxes at each point



![image-20240414145442436](C:\Users\13123\AppData\Roaming\Typora\typora-user-images\image-20240414145442436.png)







### Single stage Faster R-CNN

just use anchor to make classification and object boxes predictions





## Semantic Segmentation: Fully Convolutional Network



Input -> Convolutions -> Scores C * H * W -> argmax H * W



use cross-entropy loss of every pixel to train the network



#### Trick: Downsampling and Upsampling

Downsampling : Pooling, strided convolution

### Upsampling

### Unpooling

Bed of nails : fill 0

Nearest Neighbour: same numbers in small blocks

##### Bilinear Interpolation

$f_{x,y} = \sum_{i,j}{f_{i,j} \max(0, 1-|x-i|) \max(0,1-|y-j|)}$

i,j in Nearest neighbours

Use two closest neighbours in x and y to construct linear approximations

##### Bicubic Interpolation

three closest neighbours in x and y to construct cubic approximation



##### Max Unpooling

##### Learnable Upsampling



## Mask R-CNN

Just add Conv layers to predict a mask for each of C classes on the region proposals



#### Panoptic Segmentation

speperate different objects in the same category



#### Human Keypoints

Represent the pose of a human by locating a set of keypoints



#### Joint Instance Segmentation and Pose Estimation





-> General Idea: Add Per-Region "Heads" to Faster / Mask R-CNN



Dense captioning -> nlp -> visual reasoning



3D shape prediction ...





