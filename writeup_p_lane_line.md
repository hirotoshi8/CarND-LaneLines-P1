# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image_test]: ./examples/grayscale.jpg "Grayscale"
[image1]: ./test_images_output/gray_solidWhiteRight.jpg
[image2]: ./test_images_output/edge_solidWhiteRight.jpg
[image3]: ./test_images_output/edge_masked_solidWhiteRight.jpg
[image4]: ./test_images_output/lines_edges_solidWhiteRight.jpg

---

### Reflection

## 1. This is the pipeline for detecting the lane line on the road.

This concept of this pipelie, I roughly detect the lane line candidates and select the target line with some filters, such as median filter, low pass flter and time-sequence moving average filter.

Based on the concept, my pipeline consisted of 5 steps.

1. Converting the images to grayscale.

![alt text][image1]

2. Removing the spike noise

3. Edge detection with Canny edge detector.

![alt text][image2]

4. Mask of the region of interest

![alt text][image3]

5. Find the lane line
 - First, find the left and right line candidates
 - Second, determin the lane line

![alt text][image4]

### Abuot the draw line function
Especially, in order to draw a single line on the left and right lanes, I modified the draw_lines() function in Step5.

In draw_lines() function, I store the points [x1,x2,y1,y2], which is consist of edge lines calculated by hough transformation and removing the affection with median filter.
Then, I calculate the slope of the left and right lines and extend the lines within the region of interest.


## 2. Potential shortcomings with this pipeline

One potential shortcoming would be what would happen when the road and wether condition is changed, which means the camera image change.

Especialy in pipeline step3 and step5, I mannually set the parameter of the algorithm, such as Canny edge detector. Depending on the world, potentialy this pipeline could not work at all. This is because the optimized parameter changes depending on the condition of the weather, roads and so on. So, it's difficult to set the best parameter to  

Another shortcoming could be occured by the changed direction of the cars against the lane line. I remove the Horizontal line as noise. So, if the car heading is changed, this proess could not detect the lane line. 


## 3. Suggest possible improvements to your pipeline

A possible improvement would be to use the method of machine learning, clursuring and adaptive filterm such as kalman filter.

In this project, I set some parameters of filters manually. However, in the real world, the camera images is often changed by sun, shadow of the bridge, buildings and tunnels and so on. This is why I want to set the paramters automatically with the method of machine learning and maybe adaptive filter is good way.
