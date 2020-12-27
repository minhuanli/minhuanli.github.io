---
layout: post
title: SmartAR on HMD
description: My course project of Computer Vision at Johns Hopkins University. We used Moverio BT-200 to do marker tracking and object recognition. 
tags: computer-vision augmented-reality marker-tracking networking object-recognition aruco robot-operating-system
---

This is a re-post of my project for [EN.600.661 Computer Vision](http://cirl.lcsr.jhu.edu/Vision_Syllabus) at Johns Hopkins University. Team members include me and [Felix Jonathan](https://github.com/fjonath1).

### Demo
<p class="full-width">
 <iframe style="width:80%;height:20rem" align="right" src="https://www.youtube.com/embed/u_Zzou0navE"></iframe>
</p>
The video is taken by a phone camera placed behind the smart glasses.

### What is it?
SmartAR is an augmented reality application on smart glass [Moverio BT-200](https://epson.com/moverio-augmented-reality-smart-glasses?utm_source=marketing&utm_medium=van&utm_campaign=us-moverio-bt200). It is able to recognize the context in front of the glass via [Bag-of-Words](https://en.wikipedia.org/wiki/Bag-of-words_model_in_computer_vision) algorithm, track fiducial marker inside the scene, and display augmentation based on its understanding.

#### Hardware
* A PC with Internet
* Moverio BT-200 head-mounted display

#### Software
* [Robot Operation System](http://www.ros.org/) installed on PC
* [Aruco](http://www.uco.es/investiga/grupos/ava/node/26) and [OpenCV](http://opencv.org/)
* [Python](https://www.python.org/)
* [Android SDK](https://www.android.com/) and [ROS Android](http://wiki.ros.org/android)

System architecture of SmartAR looks like this:
<p class="full-width"><img src="/public/image/smartar-arch.jpg" alt="SmartAR architecture" style="width:50%;" align="right"/></p>
ROS manages the messages within the network between PC and Moverio BT-200.

### Object Recognition
The object recognition algorithm here is very basic bag-of-words algorithm. A database of object images is needed on PC.
<p class="full-width"><img src="/public/image/smartar-object.png" alt="SmartAR object recognition" style="width:60%;" align="right"/></p>

Thanks to the simplicity of Bag-of-Words algorithm, the recognition of known objects in this application is real-time.

### Marker Tracking
[Aruco](https://www.uco.es/investiga/grupos/ava/node/26) is used to track markers in the scene. In order to correctly overlay the graphics on top of the marker seen by the user, an optical see-through display calibration is needed. Here, the traditional [Single Point Active Alignment Method](http://ieeexplore.ieee.org/document/880938/) is applied. Rendering is performed using OpenGL ES in Android OS. The result looks like this:
<p class="full-width"><img src="/public/image/smartar-marker.png" alt="SmartAR marker tracking" style="width:60%;" align="right"/></p>

Both geometric and context augmentation are provided at the same time. The performance is real-time as well.

Thanks!  <i class="em em-lq"></i>
