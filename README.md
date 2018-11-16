# VINS-Mono

[MYNT-EYE-D-SDK]: https://github.com/slightech/MYNT-EYE-D-SDK.git
[MYNT-EYE-VINS-Sample]:https://code.slightech.com:666/sweeper/VINS-Mono.git
[make ros]:https://slightech.github.io/MYNT-EYE-D-SDK/md_guide_ros.html

## If you wanna run VINS-Mono with MYNT EYE camera, please follow the steps:

1. Download [MYNT-EYE-D-SDK][] and [make ros][].
2. Follow the normal procedure to install VINS-Mono.
3. Update distortion_parameters and projection_parameters to  [here](./config/mynteye/mynteye_config.yaml)
4. Run mynteye_wrapper_d & VINS-Mono to start.

---

## Install ROS Kinetic conveniently (if already installed, please ignore)

```
cd ~
wget https://raw.githubusercontent.com/oroca/oroca-ros-pkg/master/ros_install.sh && \
chmod 755 ./ros_install.sh && bash ./ros_install.sh catkin_ws kinetic
```
## Install MYNT-EYE-VINS-Sample

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
git clone -b mynteye-d https://github.com/slightech/MYNT-EYE-VINS-Sample.git
cd ..
catkin_make
source devel/setup.bash
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc

```
## Get image calibration parameters
Assume that the left eye of the mynteye camera is used with imu.Through the GetMotionIntrinsics() and GetMotionExtrinsics() function of the [MYNT-EYE-D-SDK][] API.
After running the above type, pinhole's distortion_parameters and projection_parameters is obtained , and then update to [here](./config/mynteye/mynteye_config.yaml).



## Run VINS-Mono with MYNT EYE camera

```
cd ~/catkin_ws

roslaunch mynt_eye_ros_wrapper mynteye.launch

roslaunch vins_estimator mynteye.launch
```

**Note**: If you want to use a fish-eye camera model,please click [here](./calibration_images)


---
## A Robust and Versatile Monocular Visual-Inertial State Estimator
**29 Dec 2017**: New features: Add map merge, pose graph reuse, online temporal calibration function, and support rolling shutter camera. Map reuse videos:

<a href="https://www.youtube.com/embed/WDpH80nfZes" target="_blank"><img src="http://img.youtube.com/vi/WDpH80nfZes/0.jpg"
alt="cla" width="240" height="180" border="10" /></a>
<a href="https://www.youtube.com/embed/eINyJHB34uU" target="_blank"><img src="http://img.youtube.com/vi/eINyJHB34uU/0.jpg"
alt="icra" width="240" height="180" border="10" /></a>

VINS-Mono is a real-time SLAM framework for **Monocular Visual-Inertial Systems**. It uses an optimization-based sliding window formulation for providing high-accuracy visual-inertial odometry. It features efficient IMU pre-integration with bias correction, automatic estimator initialization, online extrinsic calibration, failure detection and recovery, loop detection, and global pose graph optimization, map merge, pose graph reuse, online temporal calibration, rolling shutter support. VINS-Mono is primarily designed for state estimation and feedback control of autonomous drones, but it is also capable of providing accurate localization for AR applications. This code runs on **Linux**, and is fully integrated with **ROS**. For **iOS** mobile implementation, please go to [VINS-Mobile](https://github.com/HKUST-Aerial-Robotics/VINS-Mobile).

**Authors:** [Tong Qin](http://www.qintonguav.com), [Peiliang Li](https://github.com/PeiliangLi), [Zhenfei Yang](https://github.com/dvorak0), and [Shaojie Shen](http://www.ece.ust.hk/ece.php/profile/facultydetail/eeshaojie) from the [HUKST Aerial Robotics Group](http://uav.ust.hk/)

**Videos:**

<a href="https://www.youtube.com/embed/mv_9snb_bKs" target="_blank"><img src="http://img.youtube.com/vi/mv_9snb_bKs/0.jpg"
alt="euroc" width="240" height="180" border="10" /></a>
<a href="https://www.youtube.com/embed/g_wN0Nt0VAU" target="_blank"><img src="http://img.youtube.com/vi/g_wN0Nt0VAU/0.jpg"
alt="indoor_outdoor" width="240" height="180" border="10" /></a>
<a href="https://www.youtube.com/embed/I4txdvGhT6I" target="_blank"><img src="http://img.youtube.com/vi/I4txdvGhT6I/0.jpg"
alt="AR_demo" width="240" height="180" border="10" /></a>

EuRoC dataset;                  Indoor and outdoor performance;                         AR application;

<a href="https://www.youtube.com/embed/2zE84HqT0es" target="_blank"><img src="http://img.youtube.com/vi/2zE84HqT0es/0.jpg"
alt="MAV platform" width="240" height="180" border="10" /></a>
<a href="https://www.youtube.com/embed/CI01qbPWlYY" target="_blank"><img src="http://img.youtube.com/vi/CI01qbPWlYY/0.jpg"
alt="Mobile platform" width="240" height="180" border="10" /></a>

 MAV application;               Mobile implementation (Video link for mainland China friends: [Video1](http://www.bilibili.com/video/av10813254/) [Video2](http://www.bilibili.com/video/av10813205/) [Video3](http://www.bilibili.com/video/av10813089/) [Video4](http://www.bilibili.com/video/av10813325/) [Video5](http://www.bilibili.com/video/av10813030/))

**Related Papers**
* **VINS-Mono: A Robust and Versatile Monocular Visual-Inertial State Estimator**, Tong Qin, Peiliang Li, Zhenfei Yang, Shaojie Shen [arXiv:1708.03852](https://arxiv.org/abs/1708.03852v1)
* **Autonomous Aerial Navigation Using Monocular Visual-Inertial Fusion**, Yi Lin, Fei Gao, Tong Qin, Wenliang Gao, Tianbo Liu, William Wu, Zhenfei Yang, Shaojie Shen, J Field Robotics. 2017;00:1–29. [https://doi.org/10.1002/rob.21732](https://doi.org/10.1002/rob.21732)
```
@article{qin2017vins,
  title={VINS-Mono: A Robust and Versatile Monocular Visual-Inertial State Estimator},
  author={Qin, Tong and Li, Peiliang and Shen, Shaojie},
  journal={arXiv preprint arXiv:1708.03852},
  year={2017}
}
```
```
@article{Lin17,
  Author = {Y. Lin and F. Gao and T. Qin and W. Gao and T. Liu and W. Wu and Z. Yang and S. Shen},
  Journal = jfr,
  Title = {Autonomous Aerial Navigation Using Monocular Visual-Inertial Fusion},
  Volume = {00},
  Pages = {1-29},
  Year = {2017}}
```
*If you use VINS-Mono for your academic research, please cite at least one of our related papers.*

## 1. Prerequisites
1.1 **Ubuntu** and **ROS**
Ubuntu  16.04.
ROS Kinetic. [ROS Installation](http://wiki.ros.org/ROS/Installation)
additional ROS pacakge
```
    sudo apt-get install ros-YOUR_DISTRO-cv-bridge ros-YOUR_DISTRO-tf ros-YOUR_DISTRO-message-filters ros-YOUR_DISTRO-image-transport
```


1.2. **Ceres Solver**
Follow [Ceres Installation](http://ceres-solver.org/installation.html), remember to **make install**.
(Our testing environment: Ubuntu 16.04, ROS Kinetic, OpenCV 3.3.1, Eigen 3.3.3)

## 2. Build VINS-Mono on ROS
Clone the repository and catkin_make:
```
    cd ~/catkin_ws/src
    git clone https://github.com/HKUST-Aerial-Robotics/VINS-Mono.git
    cd ../
    catkin_make
    source ~/catkin_ws/devel/setup.bash
```

## 3. Visual-Inertial Odometry and Pose Graph Reuse on Public datasets
Download [EuRoC MAV Dataset](http://projects.asl.ethz.ch/datasets/doku.php?id=kmavvisualinertialdatasets). Although it contains stereo cameras, we only use one camera. The system also works with [ETH-asl cla dataset](http://robotics.ethz.ch/~asl-datasets/maplab/multi_session_mapping_CLA/bags/). We take EuRoC as the example.

**3.1 visual-inertial odometry and loop closure**

3.1.1 Open three terminals, launch the vins_estimator , rviz and play the bag file respectively. Take MH_01 for example
```
    roslaunch vins_estimator euroc.launch
    roslaunch vins_estimator vins_rviz.launch
    rosbag play YOUR_PATH_TO_DATASET/MH_01_easy.bag
```
(If you fail to open vins_rviz.launch, just open an empty rviz, then load the config file: file -> Open Config-> YOUR_VINS_FOLDER/config/vins_rviz_config.rviz)

3.1.2 (Optional) Visualize ground truth. We write a naive benchmark publisher to help you visualize the ground truth. It uses a naive strategy to align VINS with ground truth. Just for visualization. not for quantitative comparison on academic publications.
```
    roslaunch benchmark_publisher publish.launch  sequence_name:=MH_05_difficult
```
 (Green line is VINS result, red line is ground truth).

3.1.3 (Optional) You can even run EuRoC **without extrinsic parameters** between camera and IMU. We will calibrate them online. Replace the first command with:
```
    roslaunch vins_estimator euroc_no_extrinsic_param.launch
```
**No extrinsic parameters** in that config file.  Waiting a few seconds for initial calibration. Sometimes you cannot feel any difference as the calibration is done quickly.

**3.2 map merge**

After playing MH_01 bag, you can continue playing MH_02 bag, MH_03 bag ... The system will merge them according to the loop closure.

**3.3 map reuse**

3.3.1 map save

Set the **pose_graph_save_path** in the config file (YOUR_VINS_FOLEDER/config/euroc/euroc_config.yaml). After playing MH_01 bag, input **s** in vins_estimator terminal, then **enter**. The current pose graph will be saved.

3.3.2 map load

Set the **load_previous_pose_graph** to 1 before doing 3.1.1. The system will load previous pose graph from **pose_graph_save_path**. Then you can play MH_02 bag. New sequence will be aligned to the previous pose graph.

## 4. AR Demo
4.1 Download the [bag file](https://www.dropbox.com/s/s29oygyhwmllw9k/ar_box.bag?dl=0), which is collected from HKUST Robotic Institute. For friends in mainland China, download from [bag file](https://pan.baidu.com/s/1geEyHNl).

4.2 Open three terminals, launch the ar_demo, rviz and play the bag file respectively.
```
    roslaunch ar_demo 3dm_bag.launch
    roslaunch ar_demo ar_rviz.launch
    rosbag play YOUR_PATH_TO_DATASET/ar_box.bag
```
We put one 0.8m x 0.8m x 0.8m virtual box in front of your view.

## 5. Run with your device

Suppose you are familiar with ROS and you can get a camera and an IMU with raw metric measurements in ROS topic, you can follow these steps to set up your device. For beginners, we highly recommend you to first try out [VINS-Mobile](https://github.com/HKUST-Aerial-Robotics/VINS-Mobile) if you have iOS devices since you don't need to set up anything.

5.1 Change to your topic name in the config file. The image should exceed 20Hz and IMU should exceed 100Hz. Both image and IMU should have the accurate time stamp. IMU should contain absolute acceleration values including gravity.

5.2 Camera calibration:

We support the [pinhole model](http://docs.opencv.org/2.4.8/modules/calib3d/doc/camera_calibration_and_3d_reconstruction.html) and the [MEI model](http://www.robots.ox.ac.uk/~cmei/articles/single_viewpoint_calib_mei_07.pdf). You can calibrate your camera with any tools you like. Just write the parameters in the config file in the right format. If you use rolling shutter camera, please carefully calibrate your camera, making sure the reprojection error is less than 0.5 pixel.

5.3 **Camera-Imu extrinsic parameters**:

If you have seen the config files for EuRoC and AR demos, you can find that we can estimate and refine them online. If you familiar with transformation, you can figure out the rotation and position by your eyes or via hand measurements. Then write these values into config as the initial guess. Our estimator will refine extrinsic parameters online. If you don't know anything about the camera-IMU transformation, just ignore the extrinsic parameters and set the **estimate_extrinsic** to **2**, and rotate your device set at the beginning for a few seconds. When the system works successfully, we will save the calibration result. you can use these result as initial values for next time. An example of how to set the extrinsic parameters is in[extrinsic_parameter_example](https://github.com/HKUST-Aerial-Robotics/VINS-Mono/blob/master/config/extrinsic_parameter_example.pdf)

5.4 **Temporal calibration**:
Most self-made visual-inertial sensor sets are unsynchronized. You can set **estimate_td** to 1 to online estimate the time offset between your camera and IMU.

5.5 **Rolling shutter**:
For rolling shutter camera (carefully calibrated, reprojection error under 0.5 pixel), set **rolling_shutter** to 1. Also, you should set rolling shutter readout time **rolling_shutter_tr**, which is from sensor datasheet(usually 0-0.05s, not exposure time). Don't try web camera, the web camera is so awful.

5.6 Other parameter settings: Details are included in the config file.

5.7 Performance on different devices:

(global shutter camera + synchronized high-end IMU, e.g. VI-Sensor) > (global shutter camera + synchronized low-end IMU) > (global camera + unsync high frequency IMU) > (global camera + unsync low frequency IMU) > (rolling camera + unsync low frequency IMU).


## 6. Acknowledgements
We use [ceres solver](http://ceres-solver.org/) for non-linear optimization and [DBoW2](https://github.com/dorian3d/DBoW2) for loop detection, and a generic [camera model](https://github.com/hengli/camodocal).

## 7. Licence
The source code is released under [GPLv3](http://www.gnu.org/licenses/) license.

We are still working on improving the code reliability. For any technical issues, please contact Tong QIN <tong.qinATconnect.ust.hk> or Peiliang LI <pliapATconnect.ust.hk>.

For commercial inquiries, please contact Shaojie SHEN <eeshaojieATust.hk>
