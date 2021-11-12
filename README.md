# Mask RCNN instance segmentation for weeds detection
Deep learning already has the capability to study images that can be used in object detection with instance segmentation. To develop human performance in overcoming weeds detection with deep learning.
instance segmentation can be useful for this project, because weeds can growth with different size and shape, in that case instance segmentation is the proper detection on this project.
Then after MASK RCNN can detect the weeds with shape and location of the weeds, a feature was added to determine the center of the detection or centroid. which can be developed as a herbicide spraying point or can be used for other developments. this centroid point is a very useful feature in this weeds case.

# Image Acquisition
A.	Image acquisition
Images or photos used as training data obtained from several corn crop plantations in Curup, Bengkulu. picture taken by using a mobile phone camera, the picture of corn plants that have weeds around the corn, and the age of corn plants is about 1-2 weeks, when the of corn still small look like the weeds. The appearance of corn plants similar like weed plants. Here are some examples of photos for dataset taken that with differentiating factors.

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/071db9ae0eff4c1a6b5cce510c501b773cca5179/assets/fig%201.png)

Fig.  1. a. separate weeds, b. weeds, c. weeds clustered, d. different lighting

The image is taken from above, to get the position of the image that used to the machine later. Images of corn plants taken about 1000 pictures / photos with different factors. The photo taken has JPG format. With image sizes of 4000x3000, 4608x2128, and 4160x3120. By using different pixel levels, it is expected to get a different calculation level for each image. 

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/f217fdb853e79f1f29b37b4569589db96882df32/assets/fig%202.png)

Fig.  2. example how to take picture for dataset

# Data set Construction and annotation
To reduce the computing and running time of the image training for the model, the size of the photo was reduced to 1280x720 pixel.even though it is converted to the small and same pixel size, but the pixel level of the image is different because it has taken using different ppi(pixel per inch) cameras. To avoid the similarity of images, different images are selected. The number of data is approximately 1000 photos. The image used as training data is 80% and the other used as validation is 20%. 
For the types of weeds is used in this study are Ageratum sp., Commelina sp., Eleusine sp., Sacciolepis sp., here is an example of an image from a weed that became a research dataset:

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/7dfc83ac2b47b4e6622c4571a6286fea9ebcc660/assets/fig%203.png)

Fig.  3. Ageratum sp.

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/7dfc83ac2b47b4e6622c4571a6286fea9ebcc660/assets/fig%204.png)

Fig.  4. Commelina sp.

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/7dfc83ac2b47b4e6622c4571a6286fea9ebcc660/assets/fig%205.png)

Fig.  5. Eleusine sp.

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/7dfc83ac2b47b4e6622c4571a6286fea9ebcc660/assets/fig%206.png)

Fig.  6. Sacciolepis sp.

Data that has been collected, then augmented so that the data used is in accordance with the needs of the RCNN Mask, such as image cleaning, brightness level, and others. After the image is augmented then the image will be annotated in order to be used, the application used to annotate the image is VGGtools. Annotations are pixels of an image taken as a calculation base to detect an image. So that the performance of the training can be seen from the comparison of annotation results and mask prediction results from training. The result of the prediction gives a label to the covered object.

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/7dfc83ac2b47b4e6622c4571a6286fea9ebcc660/assets/fig%207.png)

Fig.  7. How MASK RCNN work

1.	Feature extraction and generation of RoIs(ResNet101 + FPN + RPN)
Deep neural network models there are various, for example such as AlexNet, VGG, GoogleNet and ResNet which are main models of deep neural networks. As more layers in a deep neural network, it will result in higher accuracy. However, it will reduce the speed of the training model and detection model. Because the initial structure cannot improve the parameters of the model, using a backbone network such as ResNet can make it easier to extract features contained in the model. The features extracted on the image depend on convolution layers. Low-level features such as edges/ends and angles, extracted by the underlying network. For high-level features that can describe categories on targets extracted to a higher level. 
For different scales, feature pyramid networks (FPNs) are used to help in the backbone network. The top-level feature of the FPN architecture is combined with the underlying features with up-sampling, where each layer itself predicts feature maps. 
Then the feature map results from the backbone network are used for rpn network. In RPN there are sliding windows, in sliding windows itself has anchors by having different area-scales and length-width ratios to produce Region of Interest (RoIs). For anchors that have been produced, RPN has 2 tasks, namely: (1) SoftMax-Loss layer used for train and classify anchor produced; (2) SmoothL1 layer is used to modify the coordinates of anchors.
2.	Target detection and instance segmentation (RoIAlign + FC/FCN)
The results of RPN and feature map go to RoIAlign, from RoIAlign separated into 2 branches, namely into a box head containing Full Connected Layer into bounding box / regression box and classification / classes. Mask head that contains convolution layer which then processes generate mask. Where this mask is an instance segmentation, which is to recognize pixels as objects of a particular class. RoIAlign extracted several features on each RoI in the feature maps using bilinear interpolation, replacing roi pooling that was in its predecessor Faster R-CNN.

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/7dfc83ac2b47b4e6622c4571a6286fea9ebcc660/assets/fig%208.png)

Fig.  8. Mask and bounding box

3.	Visualize centroid

To determine the location as the midpoint of the image is taken from the result of the segmentation instance of the weed image. It can also show the number of objects in the image and the name of the object. after generating mask from weeds.

![alt text](https://github.com/dp-aji/Mask-RCNN-weeds/blob/7dfc83ac2b47b4e6622c4571a6286fea9ebcc660/assets/fig%209.png)

Fig.  9. Centroid detection

from fig 9. we can see how many objects detected in the image, and also the coordination of the centroid from the each object.
for the use of instance segmentation and centroid are the good combination to detect objects that have different sizes and shapes. the development for the model can be more optimal and have more potential to be developed in many ways.
