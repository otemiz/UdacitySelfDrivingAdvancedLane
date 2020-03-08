[image1]: ./camera_cal/calibration5.jpg "Distorted"
[image2]: ./output_images/undistorted.jpg "Undistorted"
[image3]: ./output_images/thresholded.jpg "Thresholded"
[image4]: ./output_images/warped.jpg "Warped"
[image5]: ./output_images/fitted.jpg "Fitted"
[image6]: ./output_images/final.jpg "Final"
[video1]: ./project2.mp4 "Video"

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

For camera calibration first obect points and image points needs to be found. This operation is done by using cv2.findChessboardCorners function in OpenCV. Then these points are stored in an array to be used in cv2.calibrateCamera. This function uses the given points and optimizes the calibration matrix. Lastly with the resulting calibration mamtrix we can undistort the images. Distorted and undistorted images can be seen in image 1 and 2.

![alt text][image1]
![alt text][image2]


### Pipeline (single images)

#### 1. Provide an example of a distortion-corrected image.

Undistorted image can be seen in image 2.
![alt text][image2]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I used a combination of color and gradient thresholds to generate a binary image. Sobel is used for detecting edges while direction of edges is used to chooserelated edges. Then this threshold is combined with saturation threshold which can also detect lines. Resulting binary image can bee seen in image 3.

![alt text][image3]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

A warp function is created for this purpose. This function choses source and destination points in correct order then by using getPerspectiveTransform, M matrix is found. Lastly warped  image has been created with M matrix and image. Resulting warped image can be seen in image 4.

![alt text][image4]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

fit_polynomial and search_around_poly functions are used  for fitting curves to lanes. Theese approaches are same as previous quizes. fit_polynomial uses sliding windows and histogram for detecting lines while search_around_poly uses previous polynomial to efficiently fit the curve. After we fit the curve by using these functions created lane area is unwarped by using unwarp function. Resulting image can be seen in image 5.

![alt text][image5]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.
For calculating real-time lane infrmation car_offset and radius functions are written which use same principle as in the previous quizzes.

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

Resulting image after using all pipeline is

![alt text][image6]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

Here's a [link to my video result](./project_video.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

Project highly depends on the threshold values. Although light dependency is reduced thanks to using gradients and different color spaces still roads with different colors schemes  and color gradients can affect the performance of the algorithm. However addition of HSV and Sobel thresholds highly increased the accuracy of lane finding as well as using 2nd order polynomial instead of first order. As a result in this project we developed much more capable algorithm to detect lines compared to first one.