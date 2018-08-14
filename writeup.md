# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps.
1. I converted the copy of images to grayscale
2. Apply Gaussian blur to grayscale images
3. Used Canny transformation on those blurred images
4. Masked the edges from Canny transformation with a trapezoidal region which server as our area of interest
5. Then comes the Hough transformation on the masked edges. This step includes multiple process: 
    - find lines from the canny edges, and
    - draw those lines on a blank image for same shape as original image
6. Draw the line image from Hough transformation over original image frame 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ... 
- First separating each line into two categories (left and right lane). to do this I used slope and image's center_x
- Then find coefficient for each lane (A and B) using polyfit 
- Then we have to find extreme edges and we already know Y coordinate for them which is predefined based on region of interest. And we can find the X coordinate by reducing polyfit function (y=Ax+B) to (x=(y-B)/A)
- Finally drawing a single line thick enough to cover lanes using OpenCV library

[image2]: ./test_images_output/solidWhiteCurve.jpg "Converted Image with Lane"


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when lanes are rounded. We might have to redo some logic inside draw_line() function and draw curved line probably by interpolating all points returned from Canny Transformation. 

Another shortcoming could be the scenario when Canny transformation can't find edges or Hough trans. can't find lines that satisfy the required criteria for slope the end image would not display any marking over lanes.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use ploylines function from OpenCV to draw curved lines.

Another potential improvement could be to interpolate array of points to draw lane as compared to just a straight line.
