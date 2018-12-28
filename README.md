# **Finding Lane Lines on the Road** 

Student Name: Bolin Zhao   
Mail： bolinzhao@yahoo.com  

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

The pipeline is consisted of the following steps,

1) Covert the  original pic into graysclae;
2) Apply Gaussian Blur to reduce the infuluence of noise;
3) Canny method to detect all the edegs;
4) Put a ladder-shaped window on the result from Canny to remove the edges which are not in the interested area. The effective edges are in white and the rest are in black.
5) Hough Tranfer is applied to pick up the acceptable lines from the all edegs.


To draw a single line on the left and right lanes, the following measures are taken,

1) the lines which decided by (x<sub>1</sub>,y<sub>1</sub>) and (x<sub>2</sub>,y<sub>2</sub>) from Hough tranfermation are divided into two group named [right] and [left]. The judgement is by slope of the lines.
2) The average coordinate value of the 4 interested points(two lines start point and end point) are calculted. 
3) To draw the lines from top and bottom of tne interested area,the Y value 540 and 320 are choosen as the start and end Y position. Then corresponding X are calculated by the function of line.   


### 2. Identify potential shortcomings with your current pipeline

The shortages are identified as follow,

1) This method is strong depended on the reuslt from hough tranfer. It can be found that in some case the left line or right line suddenly move away from the real target. It may due to the hough transfer do not get the right start or end point;

2) If the curvature of road is big, this method will fail to detect the effective lines.


### 3. Suggest possible improvements to your pipeline

1) In every sample loop, the lines can be checked with last 5 lines. If the different is larger than a threshold, the lines should be rejected as the effective lines. 

2) It is possible to apply the curve fitting to fit the line as a curve.
