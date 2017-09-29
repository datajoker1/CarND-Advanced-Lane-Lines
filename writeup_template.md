## Advanced Lane Finding
In this project, our goal is to write a software pipeline to identify the lane boundaries in a video. Following steps were implemented to acheive the goal :

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


### Camera calibration
Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

1. Convert to grayscale
2. Find the chessboard corners
3. Get objpoints and imgpoints
4. Undistort image uisng cv2.undistort function

![](output_images/undistorted_chessboard.png)



### Pipeline 

1. Provide an example of a distortion-corrected image.
![](output_images/undistorted_road.png)


2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image. Provide an example of a binary image result.

 * I used a combination of color and gradient thresholds to generate a binary image


  * Sobel Absolute Threshold:
    ![](output_images/sobel_abs.png)

  * Sobel Magnitude Threshold:
    ![](output_images/sobel_magnitude.png)

  * Sobel Directional Threshold:
    ![](output_images/sobel_direction.png)

  * HLS S-Channel Threshold:
    ![](output_images/hls-s.png)

  * HLS L-Channel Threshold:
    ![](output_images/hls-l.png)



3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.


  | Source        | Destination   |
  | ------------- |:-------------:| 
  | (580,460)     | (200,0)     |
  | (710,460)     | (520,0)    |
  | (1150,720)     | (520,0)    |
  | (150,720)    | (200,1280)     |

  ![](output_images/perspective_transform.png)



4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

 * Two approaches were implemented for finding lane lines. The first approach is the window sliding method which is used when prior lane information does not exist or missing. Although this appraoch is often more robust, it is also computationally time consuming. The other approach is searching for lane pixels in a target region determined by the previous window frame. The second approach is less compuationally intensive and is used for most of the video frames.

 * function > fit_lanes()



5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

 * I used np.polyfit() function.
 * function > find_lanes() > find_curvature()



6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

 * function > draw_poly() 
 * ![](output_images/result.png)




7. Discussion includes some consideration of problems/issues faced, what could be improved about their algorithm/pipeline, and what hypothetical cases would cause their pipeline to fail.

 * My pipeline looks good in some cases, but I'm not sure if it can be used on a real road.
 * It tends to depend on the color of the lane, but it will be very vulnerable when it comes to rain or snow.
 * It works well on a clear day or in a normal lane.
 * I think the lane detection method that generates the feature using cnn is more robust than the method of extracting the direct feature and detecting the lane.
