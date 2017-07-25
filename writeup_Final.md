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

My pipeline consisted of 5 steps. 

1. Added a gray scale mask to deal with shaded regions.
2. Convert the image to grayscale.
3. Smoothen the image.
4. Identify edges using Canny Edge detection.
5. Define the region of interest and exclude the edges outside of it.
6. Run Hough Transform to find line segments.
7. Split the lines into left and right based on slope direction.
8. Exclude line segments based on slope range (0.3 to 0.8). Also exclude line segments which deviates too much from the mean slope.  
9. Find the mean of all points in the line segments and extrapolate a line based on this.
10. Use the previous frame slope information and determine the final slope.
10a. First find the mean of the slopes of current and previous frame.
10b. If the slope mean deviates too much from the previous frame then use the slope of the previous frame.  
11. Concatenate and draw then lanes


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when 
1. there are highly curvy roads the hough transform might not work because of the parameters provided.
2. there are sharp turns, the logic of using previous frame information needs to be weighted.
3. Also see at times the avg means of points to extrapolate shifts the line segment.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to do a weighted average when find the mean of line segments for extrapolation.
We could more weights to the segments at the bottom of the image. 
