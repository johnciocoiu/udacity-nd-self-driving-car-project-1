# **Finding Lane Lines on the Road** 

### 1. The pipeline

My pipeline is a function (with an image as argument) which contains the following steps I learned in the lessons:
- Take the grayscale of the image
- Take a blur of the grayscale image
- Use the canny function to see high changes in color
- Crop the image into a region of interest (all relative to the image size)
- Draw the lines using the hough function
- Combine the original image with the lines with a certain opacity

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by using every line and calculated its slope. If the slope is > 0, it's the right lane, < 0 is the left lane. Using this slope, I find two points, the most upper and the most lower point. Using this points I calculated new X values, using the image-height Y and the Y on 60% of the top. Using these new coordinates (X-calc-1, Y-bottom) and (X-calc-2, Y-60-from-top), I managed to draw the lines.

### 2. Potential shortcomings

Some shortcomings are:
- It is a linear function and extrapolation, so it is not possible to use this function on curved roads (lines).
- Sometimes the slope is a NaN, so no line could be calculated
- Sometimes the line has some artifacts, this may happen when some not-lines are recognized as line.

### 3. Possible improvements

Possible improvements:
- Using regression functions to fit a line on the lines found with the Hough-function
- Adjust/finetune some parameters to remove the artifacts
- Use previous frames in the video to calculate the lines on the current frame, because when driving, the line could not change extremely compared to the previous frame.
