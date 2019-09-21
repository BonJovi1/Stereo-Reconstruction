# Stereo-Reconstruction
Generating a dense 3D point cloud reconstruction of a scene from stereo images

## The question

3D point clouds are very useful in robotics for several tasks such as object detection, motion estimation (3D-3D matching or 3D-2D matching), SLAM, and other forms of scene understanding. Stereo cameras provide us with a convenient way to generate dense point clouds. Dense here, in contrast to sparse, means all the image points are used for the reconstruction. You have to generate a dense 3D point cloud reconstruction of a scene from stereo images. 

The data set includes a set of rectified and synchronized stereo image pairs from a KITTI sequence, the calibration data, and the absolute ground truth poses of each stereo pair. The procedure is as follows,

- Generate a disparity map for each stereo pair. Use OpenCV (e.g. StereoSGBM) for this. Note that the images provided are already rectified and undistorted.
- Then, using the camera parameters and baseline information generate colored point clouds from each disparity map. Some points will have invalid disparity values, so ignore them. Use [Open3D] for storing your point clouds.
- Register (or transform) all the generated point clouds into your world frame by using the provided
ground truth poses.
- Visualize the registered point cloud data, in color. Use Open3D for this.

Report your observations with a screenshot of your reconstruction. 
[Bonus] Compare different stereo matching algorithms.