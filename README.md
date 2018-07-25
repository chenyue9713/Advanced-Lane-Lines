# Advanced-Lane-Lines


## Overview
In this project, I will implement computer vision technologies to achieve lane boundaries lane identification
by using a video from a front-facing camera on a car. 

The goals/steps of this project are the folloing:
  * Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
  * Apply a distortion correction to raw images.
  * Use color transforms, gradients, etc., to create a thresholded binary image.
  * Apply a perspective transform to rectify binary image ("birds-eye view").
  * Detect lane pixels and fit to find the lane boundary.
  * Determine the curvature of the lane and vehicle position with respect to center.
  * Warp the detected lane boundaries back onto the original image.
  * Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


## Camera Calibration
In the real world, there is always a distortion when cameras use curved lenses to form an image. So it is necessary to 
use a method to reduce or remove the effect of distortion. Checkerboard patterns are useful for this tasks. I applied 
OpenCV functions **_findChessboardCorners_** and **_drawChessboardCorners_** to automatically find the draw corners in an image of
a chessboard pattern, like following figure:
![png](Figures/chessboard.png)

Then I applied function **_calibrateCamera_** to measure distortion coefficients. After that **_undistort_** is used for
correcting distortion of image. The result like the below figure:
![png](Figures/chessboard_undist.png)

And I applied the camera calibration method on test images collected from real world,
![png](Figures/test_images_undist.png)

## Color Transforms and Gradient Thresholded
In order to filter out the road lanes in each frame of video, Sobel operator is a good way to achieve it. In my project I applied Gradient threshold combination for these images, like following figures:
![png](Figures/test_images_Gradient_Thresholded.png)
Also, I set a threshold for s parameter on hls color space and region of interest to filter the surrounding noise.
The points for region I am interested show on following table:


| Points                         |     Value                       |
|:---------------------:|:---------------------------------------------:|
| Lower Left                 | (Width x 0.1, Height)                                     |
| Upper Left              | (580,440) |
| Upper right         | (750,420)   |
| Lower right     | (Width x 0.95, Height)  |

The output figures is following:
![png](Figures/roi_image.png)

## Perspective Transform


