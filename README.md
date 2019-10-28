# Stereo-Reconstruction
Generating a dense 3D point cloud reconstruction of a scene from stereo images \
If the notebook doesn't load, use the jupyter nbviewer  
https://nbviewer.jupyter.org/github/BonJovi1/Stereo-Reconstruction/blob/master/code.ipynb

## The question

3D point cloud generation is very useful in robotics for several tasks such as object detection, motion estimation (3D-3D matching or 3D-2D matching), SLAM, and other forms of scene understanding. Stereo cameras provide us with a convenient way to generate dense point clouds. Dense here, in contrast to sparse, means all the image points are used for the reconstruction. You have to generate a dense 3D point cloud reconstruction of a scene from stereo images. 

The data set includes a set of rectified and synchronized stereo image pairs from a KITTI sequence, the calibration data, and the absolute ground truth poses of each stereo pair. The procedure is as follows,

- Generate a disparity map for each stereo pair. Use OpenCV (e.g. StereoSGBM) for this. Note that the images provided are already rectified and undistorted.
- Then, using the camera parameters and baseline information generate colored point clouds from each disparity map. Some points will have invalid disparity values, so ignore them. Use [Open3D] for storing your point clouds.
- Register (or transform) all the generated point clouds into your world frame by using the provided
ground truth poses.
- Visualize the registered point cloud data, in color. Use Open3D for this.

Report your observations with a screenshot of your reconstruction. 
[Bonus] Compare different stereo matching algorithms.

Second question:

Using the generated reconstruction from the previous part, synthesize a new image taken by a virtual monocular camera fixed at any arbitrary position and orientation. Your task in this part is to recover this pose using an iterative Perspective-from-n-Points (PnP) algorithm. The steps are as follows,
- Obtain a set of 2D-3D correspondences between the the image and the point cloud. Since here you’re generating the image, this should be easy to obtain. 
- For this set of correspondences compute the total reprojection error c = 􏰂i ∥xi − PkXi∥2 where Pk = K[Rk|tk], Xi is the 3D point in the world frame, xi is its corresponding projection. 
- Solve for the pose Tk that minimizes this non-linear reprojection error using a Gauss-Newton (GN) scheme. Recall that in GN we start with some initial estimated value xo and iteratively refine the estimate using x1 = ∆x +x0, where ∆x is obtained by solving the normal equations JT J∆x = −JT e, until convergence.

The main steps in this scheme are computing the corresponding Jacobians and updating the es- timates correctly. For our problem, use a 12 × 1 vector parameterization for Tk (the top 3 × 4 submatrix). Run the optimization for different choices of initialization and report your observations.
