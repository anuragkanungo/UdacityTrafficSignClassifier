## Project: Build a Traffic Sign Recognition Program
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

This is the project submission for traffic sign classification problem in Udacity self driving nano degree program. The dataset contains 34799 training examples = 34799 and 12630 testing examples of image size [32x32x3].

The dataset histogram was visualized to analyze the density of different classes in the training data. 


## Preprocessing and Augmentation
Here I am generating additional training data by changing brightness to simulate day and night conditions.
Images are generated with different brightness by converting them to HSV channel and then scaling the Vue
value using normal distribution. Hence this doubles the training data size and we have to double the ground
truth labels as well.

I used all the 3 color channel and the dataset was normalized by calculation the mean and then subtracting that from each value. This leads to : Training data mean: 1.5060225258608155e-16 and variance: 0.6730098175440252 such as approx 0 mean and 0.67 variance.

I looked into image translation, rotation and shearing (based on capturing the sign from different angles) but those didn't help much.

## Model Architecture

I decided to use the LeNet implementation and without augementation I was able to achieve around 85% accuracy and after data augementation the accuracy increased to around 90%. Therfore to prevent overfitting i added dropout with keep prob 0.5 in layer 4 and that helped to bump the accuracy to 94%.


The LeNet architecture accepts a 32x32xC image as input, where C is the number of color channels. I am passing RGB color images there for the input size was 32x32x3.

Layer 1: Convolutional.  
Input shape: 32x32x3.  
RELU activation and Pooling.  
Output shape: 14x14x6.  

Layer 2: Convolutional.   
Input shape: 14x14x6.  
RELU activation and Pooling and Flatten.  
Output shape: 400.  

Layer 3: Fully Connected.   
Input shape: 400.  
RELU activation.  
Output shape: 120.  

Layer 4: Fully Connected.   
Input shape: 120.  
RELU activation and Dropout with keep_prob 0.5 . 
Output shape: 84.  

Layer 5: Fully Connected.   
Input shape: 84.  
RELU activation and Dropout with keep_prob 0.5 .   
Output shape: 43.  (Num of labels)


## Model Training:

20 Epochs were used with 64 batch size.  
Adam optimizer with rate 0.001 and mean softmax cross entropy loss function was used.  

The training gets above 93% accuracy on the validation data consistently after 5 epoch.  
Previously without data augmentation and dropout in layer 4, the accuracy was limited to 90%.  
Additionally, I tried adding translation and rotation but that didn't help with accuracy.

## Test on New Images

The trained model was run on 6 new images and it got 66.7% accuracy on those images. Although model did seem to be
highly confident about those examples, mostly 99% confident on the prediction, either right or wrong.

Image visualazation in Ipython notebook.   

### Possible difficulties in classification
The first image might be difficulty to classifiy because of background noise whereas
last image can be classified easily as it has no background noise, converted from a png image.

Additionally I guess first and fifth images are hard to classifiy correctly because they are
taken at an angle and while training this particular model, I haven't augmented the data
with rotation or translation.

Fourth image might have some classification problem because of the green background.   
The model might not be highly confident about it being a children crossing, although it's kind of a
unique and easily differentiable sign and the model could have learned that.



### Predictions


| Image | Prediction |
| ------------- | ------------- |
| Double Curve | Right-of-way at the next intersection|
| Roundabout mandatory | Roundabout mandatory|
| Yield | Yield|
| Children crossing | Children crossing|
| Speed limit (20km/h)| Speed limit (30km/h)|
| Yield | Yield|



The model was able to correctly guess 4 of the 6 traffic signs, which gives an accuracy of 66.7%.
This isn't very close to the test set accuracy which is 92.4%, mostly because of missing image
translation and rotation.


### SoftMax


For first example: 99% certain about some other class and almost 0% for ground truth .   
For second example: 100% certain about ground truth .   
For third example: 100% certain about ground truth .  
For fourth example: 77% certain about ground truth .  
For fifth example: 99% certain about some other class and almost 0% for ground truth .  
For sixth example: 100% certain about ground truth .     



Further details are in the Ipython notebook in comments.

