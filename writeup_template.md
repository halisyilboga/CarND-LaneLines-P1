# **Finding Lane Lines on the Road**


#### already existing functions and new one are written for satisfy the need. For example draw_lines function is rewritten in the preceding sections.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/imagePipeline.png "Grayscale"

---

### Reflection

### 1. in this part the pipeline will be described and modification in draw_lines function will be explained.###

 The pipeline of the project consisted of 6 steps.
 * First, images  are converted the images to grayscale and
 * then the images are blurred with 'gaussian_blur' function with kernel size set to 3.
 * canny function is called for detection of edges.
 * specifying the region of interest by deciding the vertices and giving it to region_of_interest function to mask other regions.
 * Then hough parameters are configured like below and hough line detection algorithm is called.
      ``` rho = 1
      theta = np.pi/180
      threshold = 1
      min_line_len = 10
      max_line_gap = 2
      ```
* then draw line function is called for drawing the lines.


In order to draw a single line on the left and right lanes, draw_lines()  modified the  function by:
the lines are separated in to two group according to their slopes. negative and positive slopes are discriminate the grouping. in order to not dealing with straight lines and shorter lines 0.5 threshold is used for both sides slope. After grouping the lines their points are grouped also for fitting lines. opencv's `fitline` function is fed by the points of both side separately and obtained the  slope and points. With simple calculation the x points are obtained for known y points which are determined starting point camera viewport.


![alt text][image1]


### 2.  Potential shortcomings with current pipeline



One potential shortcoming would be what would happen when  when the line are faint or distorted.

Some illumination related improvements must be done. in the optional chalenge video it is clear it goes crazy in realtively brighter areas.


### 3. Suggestions for improvements to pipeline

A possible improvement would be to  detect curved lines also.
Using moving average in between video frames may  help .
Some correction function must be implemented in to the pipeline.

### Optional Challenge
optional Challenge part show that in curved roads this algorithm is not effective and prone to error result. Some parameter adjustments are made the algorithm better but for sure there must be better ways.
