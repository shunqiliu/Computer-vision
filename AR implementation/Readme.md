# Introduction
In this programming assignment, we will use the concepts of projective geometry and homographies to allow us to project an image onto a scene in a natural way that respects perspective. To demonstrate this, we will project our logo onto the goal during a football
match. For this assignment, we have provided images from a video sequence of a football match, as well as the corners of the goal in each image and an image of the Penn Engineering logo. The task is, for each image in the video sequence, compute the homography between the Penn logo and the goal, and then warp the goal points onto the ones in the Penn logo to generate a projection of the logo onto the video frame

# Technical Details
## Homography Estimation
To project one image patch onto another, we need, for each point inside the goal in the video frame, to find the corresponding point from the logo image to copy over. In other words, we need to calculate the homography between the two image patches. This homography is a 3x3 matrix that satisfies the following:
xlogo ∼Hxvideo (1)
Or, equivalently:
λxlogo =Hxvideo (2)
Where xlogo and xvideo are homogeneous image coordinates from each patch and λ is some scaling constant. To calculate the homography needed for this projection, we provide, for each image, the corners of the patches that we would like you to warp between in each image.  You can then warp each image point using H to find its corresponding point in the logo (note that the homography equation is estimated up to a scalar, so you will need to divide Hximage by the third term, which is λ), and then return the set of corresponding points as a matrix.

## Inverse Warping
You may be wondering why we are calculating the projection from the video frames to the logo image, when we want to project the logo image onto the video frames. We do this because, if we compute the inverse homography, and project all the logo points into the video frame, we will most likely have the case where multiple logo points project to one video frame pixel (due to rounding of the pixels), while other pixels may have no logo points at all. This results in ’holes’ in the video frame where no logo points are mapped. To avoid this, we calculate the projection from video frame points to logo points to guarantee that every video frame gets a point from the logo.
We can then replace every point in the video frame (xvideo) with the corresponding point in the logo (xlogo) using the correspondences (ximage, xlogo).

# Code Files
## est homography.py
This function is responsible for computing the homography given correspondence
## warp pts.py
This function is responsible for computing the warped points given correspondence and
a set of sample points
## utils.py
Include 2 functions: Calculate_interior_pts takes in the size of an image and a set of corners that define a polygon in the image. And inverse warping the picture
## project_logo.py
Main function of project

# Acknowledgement
The project is the homework of the CIS580 of Upenn. What author's work is finish the functions in est homography.py and warp pts.py
