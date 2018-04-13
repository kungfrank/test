# Ardrone indoor slam and navigation

This repository contains all necessary file to make ARDrone antonomously navigate in indoor environment.

The demo video: https://youtu.be/r9LegSK6MfU

Since this is one of my bachelor project and I have graduated 2 years ago, I can not guarantee that it is still fully functional. Plus, I don' have an ARDrone to verify it, so I am not planning to write any document about how to reproduce the same experiment.

If you have any question, please use Issue, I will try to find time to answer it.

For any collaboration plan, please send me a email: f44006076@gmail.com

For all modified/original codes in this repository are following License GPL ( GNU Lesser General Public License v3.0 )

Author is HaoChih, LIN

----------------------------------

This project is the first section of my bachelor project. I simplified and arranged the source code form origin version which developed by LIN. However, those packages including tum_ardrone and lsd_slam are kind of out of date. Since there are more efficient algorithm can be applied in this project now, I will continue improving my project in the future.

If you are interesting in the usage, the brief tutorial is below.

If you have any question, please do not hesitate to send me an email: k3083518729@gmail.com

Last developer and code maintainer Frank, Kung

----------------------------------

Brief introduction
-----

This project uses recursive least square algorithm to caculate the transfer function of tum_ardrone/pose (in real size) and LSD_slam/pose(nonscale). After recursive least square converges completely, we used this transfer function to convert nonscale point cloud map from LSD_slam to real world's map which is used for navigation.

(Because there are some modifications in both tum_ardrone and LSD_slam source code, we compressed them to .tar file. You can  easily use them after decompressing and compiling directly, but don't forget to install the dependences of them.)

Usage
-----

### 1. TUM_Ardone

https://github.com/tum-vision/tum_ardrone

``` bash
roslaunch tum_ardrone ardrone_driver.launch
```
connect our computer to ardrone
```bash
roslaunch tum_ardrone tum_ardrone.launch
```
Initial PTAM and ensure pose estimate is correct (first fly up 1m and then down 1m to facilitate a good scale estimate).

### 2. LSD_Slam

https://github.com/tum-vision/lsd_slam


``` bash
rosrun lsd_slam_viewer viewer
rosrun lsd_slam_core live_slam image:=/ardrone/front/image_rect camera_info:=/ardrone/front/camera_info
```
Ensure pose estimate is correct.

### 3. Hypharos_Ardrone

``` bash
rosrun Hypharos_ardrone conversion
```
Do conversion. Flying Ardrone around until dq and dx value converges completely, press "l" to lock them, and press "p" to publish point cloud.
 
```bash
roslaunch ar_drone_moveit demo.launch
```
Launch Moveit. After octomap display in Moveit, you can start path planning with motion planner.

``` bash
rosrun Hypharos_ardrone tum_position_3.cpp
```
Press "p" and "s" to let Ardrone follow the path.
