# Depth Estimation using Stereo Camera
 This repository contains code to find disparity and depth map of two image sequences of a given subject by leveraging the concepts of epipolar geometry, Fundamental Matrix, Essential Matrix and its decomposition to get Rotation and Translation matrices, epipolar lines, rectification correspondence using SSD, and triangulation.

## Pipeline
### 1. Calibration 
- Compare the two images and select the set of matching feature. Tune the Lowe's ration to reject the outliers
- Estimate the Fundamental matrix using the obtained matching feature. Use the RANSAC to make your estimation more robust. Enforce the rank 2 condition for the fundamental matrix.
- Estimate the Essential matrix(E) from the Fundamental matrix(F) and instrinsic camera parameter.
- Decompose the E into a translation T and rotation R
- Disambugiate the T and R using triangulation.

### 2. Rectification
- Apply perspective transfomation to make sure that the epipolar lines are horizontal for both the images. This will limit the search space to horizontal line during the corrospondace matching process in the later stage.

### 3. Correspondence
- For each epipolar line, apply the sliding window with SSD to find the corrospondence and calulate disparity.
- Rescale the disparity to be from 0-255 for visualization

### 4. Compute Depth Image
- Using the disparity calculated above, compute the depth map. The resultant image has a depth image instead of disparity.

## Dataset
[MiddleBury Stereo Dataset](https://drive.google.com/drive/folders/1wkjEqhttgPs0nDvFVnsBeinE7ukYL2-f?usp=drive_link)
## Requirement:
- Python 2.0 or above

## Dependencies:
- OpenCV
- NumPy


##  Results
- Epipolar line corrosponding to the obtained matching features
![](epipolar_lines.png)

- Disparity Map
![](disparity_maps.png)

- Depth heat map
![](depth_maps.png)
