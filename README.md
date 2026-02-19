## Title:

Stereo Depth Estimation using Harris Corner Detection and Feature Matching

## Executive Summary:

This project implements a stereo vision system that estimates relative depth from a pair of images. The algorithm detects feature points using Harris Corner detection, matches corresponding points between left and right images using region correlation, and computes pixel disparity to estimate depth.

The resulting depth values are normalized and visualized as a relative depth map, where brighter pixels represent closer objects and darker pixels represent distant objects. The project demonstrates how 3D spatial information can be recovered from 2D images using geometric relationships rather than machine learning.

## Methodology:
### 1) Gradient Computation
Image gradients are computed using Sobel operators to measure intensity changes in horizontal and vertical directions.

These gradients describe the local texture structure required for corner detection.

### 2) Harris Corner Detection
For each pixel:
- Build a local structure matrix from gradients
- Compute the Harris response function R
- Apply thresholding
- Apply non-maximum suppression (3×3 neighbourhood)

This produces feature points that are stable across viewpoints.

Parameters tested:
- Window size W (5×5, 7×7)
- Threshold T
- Harris constant k (0.04 – 0.15)

### 3) Feature Matching (Stereo Correspondence)
For each feature in the left image:
- Search along the epipolar row in the right image
- Compare patches using region correlation
- Select the best match based on the similarity score

Matching window size tested between 5×5 and 11×11.

### 4) Disparity Calculation
Depth is derived from the horizontal displacement between matched points:

Relative depth ∝ 1 / disparity

Closer objects -> larger displacement
Farther objects -> smaller displacement

### 5) Depth Map Generation
Depth values are:
- Computed for matched feature points
- Rescaled into range [10, 255]
- Plotted asa  grayscale depth map

Unmatched pixels are assigned 0 (black).

The output includes:
- Feature coordinates (ASCII)
- Matching pairs and correlation scores
- Relative depth values
- Final depth image

## Output Images:
<img width="256" height="256" alt="ball_left_new_corners" src="https://github.com/user-attachments/assets/e0cb806f-67a4-4c8c-b7d0-9c32c8e70a4b" />
<img width="256" height="256" alt="ball_right_new_corners" src="https://github.com/user-attachments/assets/9654fdc3-9293-4344-bca7-320ecf451206" />
<img width="256" height="256" alt="ball_depth" src="https://github.com/user-attachments/assets/8308fc50-fd1c-4a32-a645-942ceb4c2919" />



## Skills:
- **Computer Vision:** Stereo vision geometry, Feature detection, Depth reconstruction
- **Image Processing:** Sobel gradients, Harris corner detection, Non-maximum suppression
- **Algorithms:** Feature matching, Correlation similarity, Disparity calculation
- **Programming:** Python, NumPy matrix operations, Image file processing
- **Mathematics:** Linear algebra, Spatial geometry, Optimization and normalization

## Results
- Successfully detects stable feature points in stereo images
- Correctly matches corresponding features between views
- Generates a relative depth map showing scene structure
- Demonstrates 3D perception using geometric vision principles
