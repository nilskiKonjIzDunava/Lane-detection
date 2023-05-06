# Lane-detection

This repository provides an algorithm to detect the lanes separating the road lanes on a dashcam video (video_road.mp4). The car moves in one lane on the highway, where the lane is limited by a solid or broken white line, or a solid yellow line. The detected lines (one for each dividing line) are drawn as extensions over the existing video frames. 

The task was divided into several parts:

1. segment_lanes function which for the input image extracts as best as possible the segment of the image containing the lines that separate the traffic lanes

2. canny_edge_detection function, which for the input image, the standard deviation of the Gaussian function and the values of the lower and higher threshold detects edges using the Canny algorithm.

3. function get_line_segments which, based on the matrix of extracted edges and the direction of the line given in the normal representation, extracts all the lengths of the given minimum length that are located in the given direction. A length represents a set of edge points that are adjacent and are all located on a given direction. Each length is defined by a start and an end point. In order for a length to be valid, it needs to meet the following criteria:
    - All points of the length between the start and end are located on the given direction
    - It is allowed to ignore missing segments of the maximum length that is given when calling the function 
    - It is considered that a certain pixel on the given direction belongs to an edge if there is an edge pixel in its environment, the size of which is given as a parameter of the function

    + Input parameters:
     - img_edges: image with detected edge pixels from which lines are detected line - an 	array of two elements (theta, rho) specifying the direction of the line
      - min_size: the minimum segment length (in pixels) to be detected, all lines smaller than 	this size should be ignored. The return argument of this function are all lengths whose 	length is greater than this parameter
     - max_gaps: the maximum size of gaps (in pixels) that can be ignored when detecting 	longer tolerance – the radius of the environment within which edge pixels are searched
    
    + Output parameters:
     - line_segments: array of detected lines where each line is represented with the coordinates of the start and end point of the line


4. lane_detection function that accepts an image (one video frame) as the only input argument and returns two arrays of 4 elements each [xl1, yl1, xl2, yl2], [xr1, yr1, xr2, yr2] representing the coordinates points that unambiguously determine the left and right lane lines in which the car is moving.
