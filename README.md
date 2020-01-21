# **Finding Lane Lines on the Road** 

## Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_videos_output/gray.png "Grayscale"
[image2]: ./test_videos_output/canny.png "Canny"
[image3]: ./test_videos_output/roi.png "Roi"
[image4]: ./test_videos_output/hough.png "Hough"
[image5]: ./test_videos_output/final.png "Final"

---

### Reflection

### 1. My Pipeline for Lane Detection

* Convert the image from RGB colorspace to Gray colorspace using `cv2.cvtColor`
* Blur the gray image using a Gaussian Filter of kernel size of 5

![alt text][image1]

* Detect the edges from the blurred image using the Canny Algorithm. Canny filter internally uses Sobel filters to detect all the edges in the image. Canny can be extremely sensitive to noise, hence Gaussian Blur is used first.

![alt text][image2]

* Reject all the edges detected by Canny which do not lie in the Region of Interest. The Region of Interest is provided by the user for that particular case. Hence this is another parameter that needs to be tuned depending on the usecase.

![alt text][image3]

* Convert the image from Cartesian space to Hough Space and detect lines in Hough Space. Hough Space are used as line detection is easier as the lines are represented as points and points are represented as lines. Hence we can specify the number of lines intersecting in the Hough Space to consider it as a line.

![alt text][image4]

* Use interpolation to find complete dotted lines to represent a single line and merge it to the input image.

![alt text][image5]

### 2. Shortcomings of current pipeline

* As the pipeline depends a lot on the canny algorithm, the parameters we use for this algorithm have to be really accurate. And as we finetune it for one particular usecase it might not work with other usecases.
* The region of interest also will change with different use cases and as we are using a trapezoidal ROI here, an edge case can be when the lane takes a sharp turn.

### 3. Possible improvements of current pipeline

* We can implement an algorithm which detects the ROI itself on the basis of horizon detection. We only need to consider the area below the horizon.
