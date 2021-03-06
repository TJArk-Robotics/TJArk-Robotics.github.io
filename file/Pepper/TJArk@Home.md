---
layout: page
title: TJArk@Home
subtitle: 
bigimg: ../../../img/big-imgs/hellopepper2.jpg
---

## **Introduction**
### The RoboCup@Home League

The [RoboCup@Home league](http://athome.robocup.org/) aims to develop service and assistive robot technology with high relevance for future personal domestic applications. It is the largest international annual competition for autonomous service robots and is part of the [RoboCup](http://www.robocup.org/) initiative. A set of benchmark tests is used to evaluate the robots' abilities and performance in a realistic non-standardized home environment setting. Focus lies on the following domains but is not limited to: Human-Robot-Interaction and Cooperation, Navigation and Mapping in dynamic environments, Computer Vision and Object Recognition under natural light conditions, Object Manipulation, Adaptive Behaviors, Behavior Integration, Ambient Intelligence, Standardization and System Integration. It is colocated with the RoboCup symposium.

###  TJArk@Home

The Robotics and Artificial Intelligence Lab (RAIL) of Tongji University was founded in 1992, Team TJArk of RAIL was founded in 2004 and participated in RoboCup World Cup from 2006 to 2019. We have got seven winning streak in China RoboCup SPL and once won the third place in RoboCup2018 SPL.

In December 2018, we founded an energetic new team to participate in RoboCup @Home League, called TJArk@Home. Main goal of TJArk@Home is to explore the limit of how well can robots serve people during common life with acceptable cost. Under the guidance of such wish, we are doing many research on the [Pepper](https://www.softbank.jp/en/robot/) platform, such as

- SLAM(Simultaneous Localizaiton and Mapping)
- Auto navigation of robot
- Object Detection and Recognition
- Human-face detection and analysis
- Human-Robot interaction
- Motion control
- Trajectory teaching
- Design of laptop GUI
- ...

April 2019, the first time TJArk@Home involved in China RoboCup@Home League, we got the first-place in SSPL(Social Standard Platform League). During the competition, we show a lot of abilities, including Autonomous navigation, Follow an operator to the given position, Recognize speech and response, Detect humans in vision and summarize their features.

####  Visual Simultaneous Localization and Mapping 

Pepper needs a model (a map) of the environment to support other tasks, mainly auto-navigation, but a prior map is often not available in various home scenarios, so SLAM find its application. The stereo camera data is mainly used by a visual SLAM module, together with laser (very limited) and odom (has significant error) data. Our VSLAM algorithm is based on [RTAB-Map](http://introlab.github.io/rtabmap/), a graph-optimized based VSLAM algorithm, and have been modified for Pepper's sensors. Odom and laser scan data make the initial pose estimation, then stereo data serves for appearance-based loop closure detection to optimize local and global pose. VSLAM can get a 3D point cloud, we make a projection to get a 2D grid map for navigation. Having map and Pepper’s size parameters, we use DWA (Dynamic Window Apporach) to plan the path and fuse vision, laser and sonar data to make real-time obstacle avoidance (mainly for dynamic scene), a series of motion command will be sent to NAOqi APIs, so Pepper can navigate to its goal points itself.

![slam](../../../img/pepper/vslam.png)

#### Computer Vision

Various vision algorithms are needed for more careful perception and analysis of Pepper’s environment on object and human level. Usually, to start a certain task, our Pepper can detect and recognize different people, remember their names and some other features, and tracking them. Then, more skills will be shown for complex goals. For object-level environment reasoning, we build an object detection and recognition framework based on [YOLO](https://pjreddie.com/darknet/yolo/), which is an interesting real-time algorithm. According to the competition scenario of RoboCup@Home, our object detection system can detect 50 classes of indoor objects in real time. To train our object detection network, we make a great dataset from OpenImages. We also match adjacent input frames to increase the robust of detection.

In some tasks we need a wide field of view, but the top 2D camera makes us disappointed. So we need to take some measures to expand Pepper’s original “eyes”. The method we choose is to stitch images from different perspectives, and a fusion algorithm follows to decrease the influence of illumination and geometric change. Now more visual candidates can be included for further processing.

![vision1](../../../img/pepper/vision1.png)

A more exciting visual module is human pose estimation. For this feature, we use [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) model to get a robust and real-time performance. With a non-parametric representation, we can detect associate body parts of multiple people in the input image stream. 

![vision2](../../../img/pepper/vision2.png)

#### Graphical User Interface

As a domestic service robot, smooth GUI interaction is neccesary. One of the advantages of Pepper is that it has a laptop on its breast, which makes GUI possible. We designed a user-friendly and cross-platform interface so even people unfamiliar to robotics can quickly operate on Pepper. 

We have put twenty applications on the GUI so far, including Motion, Conversation, Vision, Joints, etc. In Motion, the operator can make the robot move a given distance to a given direction, or just move by a constant velocity.In Conversation, the operator can chat with Pepper using English or Chinese.In Vision, camera information is integrated. All images Pepper captured will be displayed here and the resolution is modifiable.In Joints, all joints' status are listed for developer to debug.We wish such GUI can help Pepper more powerful and useful.

<table class="img-container" align="center" style="border:0;">
    <tr>
        <th> <img src="../../../img/pepper/gui1.png" alt="GUI1"/> </th>
        <th> <img src="../../../img/pepper/gui2.png" alt="GUI2"/> </th>
    </tr>
    <tr>
        <th> <img src="../../../img/pepper/gui3.png" alt="GUI3"/> </th>
        <th> <img src="../../../img/pepper/gui4.png" alt="GUI4"/> </th>
    </tr>
    <tr>
        <th> <img src="../../../img/pepper/gui5.png" alt="GUI5"/> </th>
        <th> <img src="../../../img/pepper/gui6.png" alt="GUI6"/> </th>
    </tr>
</table>

#### Software Framework

We have developed a Python framework, which is a high-level package of [NAOqi APIs](http://doc.aldebaran.com/2-5/index.html) and [ROS](https://www.ros.org/)-based components. Every team member can write his/her own lib files, such as "LibMoiton", "LibDetection", and add it to the framework easily. At the game site, Pepper can use these lib files to perform various, more complex tasks. The framework is still in developing, so we don't open its source yet.

<img id="architecture" align="middle" src="../../../img/pepper/architecture.png" width="50%" />

## **Team Members**

| Name        | Introduction                                                            |
| ----        | ----                                                                    |
| Deng Xiuqi  | Graduate student, Department of Control Science and Engineering         |
| He Zongtao  | Leader, Graduate student, Department of Control Science and Engineering |
| Xu Weihan   | Graduate student, Department of Control Science and Engineering         |
| Zhou Xun    | Graduate student, Department of Control Science and Engineering         |
| Liu Zhihao  | Graduate student, Department of Control Science and Engineering         |
| Wang Liuyi  | Senior student, Automation                                              |
| Wang Naijia | Senior student, Automation                                              |
| Du Jiayuan  | Senior student, Automation                                              |
| Lu Liwen    | Senior student, Automation                                              |

## **Lab Publications**

![IROS2017](../../../img/pepper/new31.jpg)

1. Zhang, Tong & Liu, Chengju & Chen, Qijun. (2017). Rebalance control for humanoid walking based on online foot position compensation. 4605-4610. 10.1109/IROS.2017.8206330. 
2. Chengju Liu, Tong Zhang, Changzhu Zhang, Ming Liu, Qijun Chen. Foot Placement Compensator Design for Humanoid Walking Based on Discrete Control Lyapunov Function. IEEE Transactions on Systems, Man, and Cybernetics: Systems, doi: 10.1109/TSMC.2019.2912417 (SCI)

2. Liu Chengju, Yang Jing, An Kang, Chen Qijun. Robust Control of Semi-passive Biped Dynamic Locomotion based on a Discrete Control Lyapunov Function. Robotica, 2019. (accepted) (SCI)

3. Peng Yun, Lei Tai, Yuan Wang, Chengju Liu, Ming Liu. Focal Loss in 3D Object Detection. IEEE ROBOTICS AND AUTOMATION LETTERS. PREPRINT VERSION. ACCEPTED JANUARY, 2019

4. Zhang C., Lam H. K., Qiu J., Liu C. et al., A new design of membership-function-dependent controller for TS fuzzy systems under imperfect premise matching. *IEEE Transactions on Fuzzy System*s, 2018 

5.  Liu C., Xia L., Zhang C., et al., Multi-layered CPG for adaptive walking of quadruped robots. *Journal of Bionic Engineering*, 2018, 15(2): 341-355. 

6. Liu C., Ning J., and Chen Q., Dynamic walking control of humanoid robots combining linear inverted pendulum mode with parameter optimization. *International Journal of Advanced Robotic Systems*, 2018, 1-15.

## **Contact Information**

Address:

Robotics and Artificial Intelligence Lab (RAIL) 

Tongji University 

4800 Cao'an Road, Jiading, Shanghai, P.R. China 

Email: 

He Zongtao <a href="mailto:1930719@tongji.edu.cn" >1930719@tongji.edu.cn

Zhou Xun <a href="mailto:1930722@tongji.edu.cn" >1930722@tongji.edu.cn

Xu Weihan <a href="mailto:1552360@tongji.edu.cn" >1552360@tongji.edu.cn

## **Link**s

RoboCup: [http://www.robocup.org/](http://www.robocup.org/)

RoboCup@Home: [https://athome.robocup.org/](https://athome.robocup.org/)

TJArk@Home video channel: [https://www.youtube.com/channel/UCE5ceR_uX-Hz3IIJx70lOrQ](https://www.youtube.com/channel/UCE5ceR_uX-Hz3IIJx70lOrQ)

TJArk@Home Team Description Paper: [https://github.com/tjarkpepper/TDP](https://github.com/tjarkpepper/TDP)

## **Media**

<table id="media-photos" class="img-container" style="border:0;" align="center">
    <tr>
        <th> <img src="../../../img/pepper/teamphoto.jpg" alt="team-photo"/> </th>
        <th> <img src="../../../img/pepper/certificate.jpg" alt="certificate"/> </th>
    </tr>
</table>

<div id="video-container">
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/7Xo4WKivYSA?controls=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/8wui0WZROrg?controls=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/CNtgHpX_gMk?controls=0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>