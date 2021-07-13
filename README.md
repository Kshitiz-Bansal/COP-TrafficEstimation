# Traffic Density Estimation

This is a python-based traffic density estimator, works using OpenCV algorithms and functions. Analyses CCTV footage in real time to estimate the density of traffic. Capable of differentiating between idle and moving traffic. Can be used for automatic switching of traffic lights based on traffic density and can even be upgraded to parametrize pedestrian density for higher safety.

It has been implemented in three stages. Each stage either adds up features or increases the efficiency of the system. The stages are as follows:

## Stage 1: The basic functions
### Perspective correction and frame cropping

This stage implements the most basic and necessary functions. Typically the camera gets an arbitrary view of the road/intersection to be monitored and also contains many unnecessary additional objects in the frame. This stage corrects the camera angle and crops out the unwanted objects from the frame.

The camera angle correction is based on Homography. A Homography is a transformation ( a 3×3 matrix ) that maps the points in one image to the corresponding points in the other image. It can be used for perspective correction, panoramic stitching and virtual advertisments. For more info on homography, please check [this](https://docs.opencv.org/master/d9/dab/tutorial_homography.html) and [this](https://learnopencv.com/homography-examples-using-opencv-python-c/).


These are the video frames at different substages.

<br>
<p align="center">
  <img src="assets/stage1_traffic.jpg" width="400"/><br>
	Unprocessed initial frame
</p>

<p align="center">
  <img src="assets/stage1_traffic_perspective_corrected.jpg" width="400"/><br>
	Perspective corrected
</p>

<p align="center">
  <img src="assets/stage1_traffic_proceseed.jpg" width="200"/><br>
	Final post processing frame
</p>
<br>

## Stage 2: Estimating traffic density
### Idle (queue) and moving (dynamic) density estimation from video file

This stage takes up frames from the input video, processes them using stage 1 functions, and analyses them to estimate the density of traffic. Idle traffic density is referred to as queue density as they would be queuing at the intersection, and moving traffic density is referred to as dynamic density.

Queue density works using background subtraction. Processed empty frame (no traffic, empty road and itnersection) is subtracted from current processed frame to estimate the density of idle traffic.

Dynamic density works on optical flow. It performs optical flow detection across subsequent frames to detect the pixels which moved across frames.


Outputs a graph of both densities with time (or frame number, as required).

<p align="center">
  <img src="assets/stage2_plot.png" width="500"/><br>
	Traffic density vs Frame number
</p>
<br>
