# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I define a kernel size and apply Gaussian smoothing. After that I define parameters for Canny Edge Detection and apply it. Next I created a masked edges image using cv2.fillPoly(), and then I defined a four sided polygon to mask. Later on I define the Hough transform parameters and ran Hough on edge detected image. Lastly, I draw the lines on the original image.

![Alt text](https://raw.githubusercontent.com/zpy016/CarND_P1/master/raw/Lane-detect-solidWhiteRight.jpg "Raw Lines after Hough Transformation")

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by picking out lines that has positive slope and negative slope and doing linear regression on them seperately. Linear regression is done using np.linalg.lstsq(). Finally, two lines were drawn on the original graph using cv2.line().

![Alt text](https://raw.githubusercontent.com/zpy016/CarND_P1/master/raw/thick_Lane-detect-solidWhiteCurve.jpg "Final Output: Single Lines")



### 2. Identify potential shortcomings with your current pipeline

This pipeline runs perfectly for all the videos provided including the optional challenge. One potential shortcoming would be what would happen when the car is shifting lines there may be only one line detected.

Another shortcoming could be the parameters for Hough transform is fine-tuned so that this pipeline works on all three videos. However, I'm not sure if it will work on all possible situaltions. 

Also, when the car is having a sharp turn, e.g. 90-degree turn, the lane detection region may not be working well.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to mark the line to be either the left lane or the right lane when there is only one line in the region. A vitual lane can also be drawn in case that only one lane is visible.

Another potential improvement could be to test the pipeline on more videos so that parameters for Hough transform can be tuned to be more robust.
