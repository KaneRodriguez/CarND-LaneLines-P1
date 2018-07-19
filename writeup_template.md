# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

My pipeline consists of 8 steps. 

  1. First, I convert an image to HSL (HLS) so that I can better detect the colors of the lane lines, white and yellow, in the image. ([HSV vs HSL Discussion](https://stackoverflow.com/questions/11396782/is-hsl-superior-over-hsi-and-hsv))
  2. Then, I convert the image to grayscale because I want to ignore the "noise" of color information present and therefore reducing the time it takes to do further processing on it. ([Why grayscale for image processing?](https://stackoverflow.com/questions/12752168/why-we-should-use-gray-scale-for-image-processing))
  3. With the grayscale image, I run a slight Gaussian blur to further reduce image noise.
  4. Canny edge detection is then applied to the blurred grayscale image in order to detect the edges within our image. I chose to use a 1:3 ratio for the low to high pixel gradient thresholds. [Canny pipeline](https://en.wikipedia.org/wiki/Canny_edge_detector#Process_of_Canny_edge_detection_algorithm)
  5. I apply a region mask on the image because I want to ignore all sections of the image that don't have a possibility of containing the lane lines.
  6. Then, I apply a Hough Transform to turn these sequences of pixels detected by the Canny into lines with start and end (x, y) coordinates.
  7. I then assign the lines as left or right based on their slope (ignoring lines that have a nearly horizontal slope) and perform a 1 degree polynomial fit on each of the lines. This results in left and right lines that represent our left and right lanes. In addition, I keep track of the last used previous left and right lane lines so that if there are not any right or left lines detected in the next iteration of the pipeline, the previous lines will be used at most one time to as a substitute. This is to help smooth out the intermittent detecting of left or right lines.
  8. Finally, I draw the detected lines onto a blank copy of the original image and overlay this new lane lines image over the original image.


### Shortcomings

One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

TODO - double gassian blur, improve memory, improve line detection for region masking

A possible improvement would be to ...

Another potential improvement could be to ...
