# Udacity Self-Driving Car Nanodegree Program 

# **1. Finding Lane Lines on the Road** 

**Goals**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./example_lanes.png "sample result"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps: 

* convert the input color image to grayscale
* smooth the gray image with Gaussian noise kernel 
* run Canny edge detection algorithm
* mask out unwanted regions with poly fill 
* run Hough line detection algorithm
* lay Hough lines onto the input color image

Please see the following for an example result: 

![alt text][image1]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calling a new smooth_line function, which composes two straight lines (left and right) from the lines detected from Hough algorithm:

* splits the lines from Hough algorithm into left and right lines, by positive or negative slopes 
* interpolates a left line by its median slope and median intercept
* interpolates a right line by its median slope and median intercept
* computes the end points of the left line by its intersections to the poly fill region
* computes the end points of the right line by its intersections to the poly fill region

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming is the use of region mask. The ladder shape of the mask assumes the camara is centered to the lower half of the road and the road is almost straight. Those are not going to be true in real world driving conditions.

Another shortcoming is the line interpolation algorithm used in the smooth_lines function. The median slope and intercept is sensitive to outliers. It fails on certain frames of the test videos. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be using deep learning algorithms like covolutional neural networks for lane detection.

For the line interpolation, a possible improvement is to use linear regression to find the slopes and intercepts, which will penalize outliers with least squeres means for example.
