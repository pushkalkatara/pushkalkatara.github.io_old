---
layout: post
category: post
tags: yolo alexeyab-darknet deep-learning computer-vision object-detection darknet-ros
date: 2018-12-08 13:06
thumbnail: https://pjreddie.com/static/img/darknet.png
title: darket_ros_v3
published: true
---

Robotics Operating System package developed for object detection and tracking on ROS image topics. Object detection based on Yolo v3 and tracking based on Kalman Filter and Optical flow. Implemented multi-threading and thread synchronization techniques with fetch, detect, publish threads to capture, infer and publish results as ROS topics. Solved the issue of memory leak on Jetson TX1 on leggedrobotics repository. Deployed on Jetson TX1 with inference of 4 FPS. I built this as part of SRM Autonomous Underwater Vehicle stack. <strong>[Source Code](https://github.com/pushkalkatara/darknet_ros) | [Live BUOY Underwater Detection Video](https://drive.google.com/open?id=1-1htIKVxDWda37Z7q-qvudrceZefzoxt)</strong>
<!--more-->
