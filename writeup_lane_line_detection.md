# **Finding Lane Lines on the Road** 

## Writeup Template

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflection on my work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Description of the pipeline

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I blurred the grayscale image with a kernel size of 7 to filter the image and avoid the pipeline to be too sensitiv for gradient detection. The third step is the gradient detection via canny edge detection. This function searches for high gradients in the grayscale image and keeps the rest of the image black. The fourth step is to define an area of interest where the algorithm should look for the lane lines via region masking. This makes the algorithm much more robust because otherwise the algorithm might find lines all over the image where it isn't from interest.
The last set finally is to combine the bright pixels in the image to a real line. This is done via hough transformation, where for each point all possible lines with gradient and bias are defined in the so called hough space. A point where multiple lines are crossing define then the slope and bias of the corresponding line.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by evaluating each detected line for its slope and bias. The sign of the line's slope indictes weather it is the right or left line. To have finally a single line I defined an average slope and bias of each line per side. I also wheight the lines by it's length so that very small lines do not falsify the result. For the same reason I added a deadband around zero to ensure that real lane lines are taken for averaging and extrapolation.

If you'd like to include images to show how the pipeline works, here is how to include an image: 



### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming could be that the algorithm fails when no line is detected.
Another shortcoming could be that curves are not correctly detected, since the algorithm averages all detected lines, so finally the detected line would be somewhere between the start and end of the curve.
Finally the current algorithm is not flexible on camera position which leads to problems in the last challange project, where starting as well as extrapolation limits are not matching at all.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use the lines of the last image as substitude when no lines were detected.

Another potential improvement could be to to not only search for linear lines but also for polynomic curves (which also could be lines). 
Image preprocessing with cutting the image to it's relevant part would be usefull to react more flixible on changed camera positions also relative positions instead of absolute values are helpfull here.
