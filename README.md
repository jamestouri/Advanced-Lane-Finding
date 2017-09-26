## Advanced Lane Finding

The steps of this company included:

1. Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
2. Apply a distortion correction to raw images.
3. Use color transforms, gradients, etc., to create a thresholded binary image.
4. Apply a perspective transform to rectify binary image ("birds-eye view").
5. Detect lane pixels and fit to find the lane boundary.
6. Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


### Camera Calibration and Distortion

The first step was to get object points of the 2 dimensional and 3 dimensional part of the checkerboards.  I applied the cv2.calibrateCamera and then undistorted the images using cv2.undistort to normalize the image

![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/download.png)

From there the points on the chessboard were used on the images and videos to Undistort.  The points are give through the cv2.undistort()

### Color Transform and Gradient Thresholds 

By applying various thresholds to alter the images and preprocess a pipeline when applying it on a video, I was able to build a pipeline that had color tranformations. 

Here is adding a Sobel Threshold, Magnitude Threshold, Direction Threshold, and HLS Threshold.

Here is what it looked like adding all the Thresholds:

![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/filterthresh.png)

### Perspective Transform  

I hardcoded the src and dst for transform, this was after working from the points on the Udacity videos.  I used cv2.getPerspectiveTransform and cv2.warpPerspective. 
![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/per_transform.png)

### Adding the Lines

I added the lines along with the measuring of the curvature inside the image, also showing the green is inside the line. Here is an example of the Lane. 

![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/finished.png)

The Project video is in the github repository under Project Output. 
