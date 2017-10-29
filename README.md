## Project: Build a Traffic Sign Recognition Program
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

This is the project submission for traffic sign classification problem in Udacity self driving nano degree program. The dataset contains 34799 training examples = 34799 and 12630 testing examples of image size [32*32*3].

The dataset histogram was visualized to analyze the density of different classes in the training data. 


## Preprocessing and Augmentation
Here I am generating additional training data by changing brightness to simulate day and night conditions.
Images are generated with different brightness by converting them to HSV channel and then scaling the Vue
value using normal distribution. Hence this doubles the training data size and we have to double the ground
truth labels as well.

I used all the 3 color channel and the dataset was normalized by calculation the mean and then subtracting that from each value. This leads to : Training data mean: 1.5060225258608155e-16 and variance: 0.6730098175440252 such as approx 0 mean and 0.67 variance.

I looked into image translation, rotation and shearing (based on capturing the sign from different angles) but those didn't help much.

## Model Architecture

I decided to use the LeNet implementation and without augementation I was able to achieve around 85% accuracy and after data augementation the accuracy increased to around 90%. Therfore to prevent overfitting i added a dropout layer at then end and that helped to bump the accuracy to 94%.


The LeNet architecture accepts a 32x32xC image as input, where C is the number of color channels. I am passing RGB color images there for the input size was 32*32*3.

Layer 1: Convolutional. 
Input shape: 32x32x3.
RELU activation and Pooling.
Output shape: 14x14x6.

Layer 2: Convolutional. 
Input shape: 14x14x6.
RELU activation and Pooling and Flatten
Output shape: 400.

Layer 3: Fully Connected. 
Input shape: 400.
RELU activation 
Output shape: 120.

Layer 4: Fully Connected. 
Input shape: 120.
RELU activation and Dropout with keep_prob 0.5
Output shape: 84.

Layer 4: Fully Connected. 
Input shape: 84.
RELU activation and Dropout with keep_prob 0.5
Output shape: 43.

