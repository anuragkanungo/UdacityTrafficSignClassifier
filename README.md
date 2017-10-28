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

I decided to use the default LeNet implementation 



