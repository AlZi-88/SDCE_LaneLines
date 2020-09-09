# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I blurred the grayscale image with a kernel size of 7 to filter the image and avoid the pipeline to be too sensitiv for gradient detection. The third step is the gradient detection via canny edge detection. This function searches for high gradients in the grayscale image and keeps the rest of the image black. The fourth step is to define an area of interest where the algorithm should look for the lane lines via region masking. This makes the algorithm much more robust because otherwise the algorithm might find lines all over the image where it isn't from interest.
The last set finally is to combine the bright pixels in the image to a real line. This is done via hough transformation, where for each point all possible lines with gradient and bias are defined in the so called hough space. A point where multiple lines are crossing define then the slope and bias of the corresponding line.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
