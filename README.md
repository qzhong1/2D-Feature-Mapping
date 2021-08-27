# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

## Mid-Term Report
* MP.1 Data Buffer Optimization
  * To make sure the buffer size stays constant, the first element is earsed if the size exceeds the predefined number
  after pushing new frames to the queue. For code efficiency deque is used instead of a vector.
* MP.2 Keypoint detection
  * The original functions in the header file matching2D.hpp is used for implementation of the detectors. IF statement 
  is used to select detectors. OpenCV library is used to create detectors. Non maximal suppression is used for Harris.
* MP.3 Keypoint removal
  * Each detected keypoints are checked against the boundary. It'll only be pushed into a new keypoint vector if it's inside the boundary. Finally replace the old vector with the new. 
* MP.4 Keypoint descriptor
  * Similarly to MP.2, OpenCV library is used to create each descriptor. IF statement is used for selection.
* MP.5 Descriptor matching
  * OpenCV library is used to create the FLANN descriptor matcher and KNN selection. Both selectable by IF statement. 
* MP.6 Descriptor Distance Ratio
  * For KNN, the ratio of top 2 best matches is compared against a threshold. The match will be rejected if the ratio is higher than the threshold. 
