## Advanced Lane Finding


The steps of this company included:

1. Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
2. Apply a distortion correction to raw images.
3. Use color transforms, gradients, etc., to create a thresholded binary image.
4. Apply a perspective transform to rectify binary image ("birds-eye view").
5. Detect lane pixels and fit to find the lane boundary.
6. Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


### Camera Calibration and Distortion

The first step was to get object points of the 2 dimensional and 3 dimensional part of the checkerboards.  
![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/Screen%20Shot%202017-09-26%20at%206.52.27%20PM.png)


I applied the cv2.calibrateCamera and then undistorted the images using cv2.undistort to normalize the image
https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/image_undistort.png

From there the points on the chessboard were used on the images and videos to Undistort.  The points are give through the cv2.undistort()

### Color Transform and Gradient Thresholds 

By applying various thresholds to alter the images and preprocess a pipeline when applying it on a video, I was able to build a pipeline that had color tranformations. 

Here is adding a Sobel Threshold, Magnitude Threshold, Direction Threshold, and HLS Threshold.

Here is what it looked like adding all the Thresholds:

![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/filterthresh.png)

### Perspective Transform  

I hardcoded the src and dst for transform, this was after working from the points on the Udacity videos.  For a while the pipeline wasn't able to stay on the line.  Although I was initially spending most of my time on the Color and Gradient thresholds, the lines stayed in the lanes after working on the Source and Destination points. 

```
src = np.float32([[475,530],
        [830,530],
        [130,720],
        [1120,720]])
    dst = np.float32([[365,540],
        [990,540],
        [320,720],
        [960,720]])
```

I used cv2.getPerspectiveTransform and cv2.warpPerspective. 
![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/per_transform.png)

### Adding the Lines

I added the lines along with the measuring of the osculating circle inside the image, also showing the green is inside the line. Here is an example of the Line warped before putting it back to the original image: 

![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/Warped_lines.png)

Here is the image after putting it back to the original view, and declaring a mask through a bitwise operator with cv2.bitwise_and

![](https://github.com/jamestouri/Advanced-Lane-Finding/blob/master/finished.png)

The Project video is in the github repository under Project Output. 

### Pipeline Video 

Here is the video of the pipeline: https://www.youtube.com/watch?v=f_X73scM4fc&feature=youtu.be

## Discussion

This project was indeed thrilling and interesting.  There weren't a lot of variables to experiment as the previous projects, and therefore wasn't as frustrating as others when making minor changes. 

The biggest challenge I faced was towards the end of the video when the car in the next lane drove past.  The line kept spreading to that car.  When I looked back on my images.  The car is bright white using the color thresholds of cv2.COLOR_BGR2LUV[:,:,2], and then I changed it to [:,:,0], the green line didn't stretch out to the car, but unfortunately had problems when the ground changed color and when during the video with the shadow.  

In the end I was able to successfully go through the video by changing the src and dst points to zoom closer on the given perspective transformation.

### Changes that could've been made
Something I kept thinking about, if it made sense was to constrain the Green line to a certain width in the image, and see if that worked.  

### Places the pipeline would likely fail
Most likely a overcast weather, or strong amounts of rain, or heavy snow.  Also at night could be a problem for my pipeline.
