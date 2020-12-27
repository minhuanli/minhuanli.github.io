---
layout: post
title: ISMAR 2016 Highlight
description: A blog giving you some insights about what is happening in the field of augmented reality research, by looking at the highlights of ISMAR (IEEE International Symposium on Mixed and Augmented Reality) 2016, at Merida, Mexico.
tags: ismar conference augmented-reality
---


The 15th IEEE International Symposium on Mixed and Augmented Reality (ISMAR) was held in Merida, Mexico last month. It is the most attractive conference for people working on Augmented Reality technologies, either from academia or from industry.

<img src="/public/image/merida-monumnet.jpg" alt="merida" style="width:100%;"/>

Many interesting hardware, algorithms, ideas and discussions happened in this conference. Here I summarized some of them that aroused my interest, both from the aspects of research and engineering, because in this area, research and engineering are sometimes aiming for the same target: expanding the impact of AR technology.

### Keynote

The keynote is presented by [Dr. Andrew Davison](https://www.doc.ic.ac.uk/~ajd/), who is well-known for his contribution to the research in SLAM (Simultaneous Localization and Mapping). The talk topic was **The History and Future of SLAM**.

The progress of SLAM in the past decades involves:

* Open-source
* Real-time performance enhancement with support of advanced hardware
* Became a crucial enabling technology for AR, robotics and mobile devices

In terms of general market, Pokemon Go achieved such great success with the simplest idea of AR, the augmentation is still not registering with reality. For the later vision to come true, SLAM is exactly the enabling technology, since general public generally dislike any fiducial markers, no matter for gaming or smart house applications.

According to Dr. Davison, the future of SLAM is:

* Fully dense
* Semantically aware
* Lifelong mapping
* Always-on, low power operation

The first two are basically research problem, and the later two, are clearly the need driven by the general market. During the conference, I talked with some mobile software companies; they showed extreme interest for AR applications, and eyeing for the academia advances, especially SLAM technology.

He also talked about how new hardware can facilitate SLAM technologies, e.g. [DVS](https://inilabs.com/products/dynamic-vision-sensors/), [DAVIS](https://inilabs.com/products/dynamic-vision-sensors/) and IPU, and the possibility of integrating deep learning to SLAM.

### Interesting Papers

I selected a few papers that especially attract me here. The selection is biased on my preference of course, and is largely based on their presentation on ISMAR, rather than purely focusing on the paper itself.

#### Do You See What I See? The Effect of Gaze Tracking on Task Space Remote Collaboration

This paper is one of the seven papers in this ISMAR conference selected to TVCG journal. Through a user study, two hypothesis are proved:

* **Co-presense**: There is significant difference in co-presence measure by providing additional attention cues.
* **Performance**: There is significant difference in performance time by providing additional attention cues.

The result is not surprising, but in demo session, the author showed their HMD devices: a Epson Moverio BT-200, plus [AffectiveWear](http://im-lab.net/affectivewear/), and plus [Pupil-Labs](https://pupil-labs.com/) gaze tracking cameras. The two additional hardware are quite interesting.

**AffectiveWear glasses** are developed from Keio University, Japan, taking its first appearance on 2015 SIGGRAPH. It takes several proximity sensor readings of the distance to the face, distributed over the frame of the glasses, and computes the emotion of the person, via a trained deep learning model. One issue with this device is the user-specific calibration, which can also be viewed as the training of learning model, that suits the specific user. General model is a bit inaccurate since the facial structure can varies a lot for different people.

**Pupil-labs** is doing perfect engineering work for providing gaze tracking capability for different head-mounted displays, both VR and AR. It is clearly a huge demand. It is amazing that they provide a solution that can be generalized: the hardware with specific add-on kit suites a variety of HMDs, and the software is open-source. Noticeably, AffectiveWear is also taking the possibility of generalization into account, because the proximity sensors are attached to the glass frame. Hopefully, there will be a test report of Pupil-lab tracking soon.

#### Gaussian Light Field: Estimation of Viewpoint-Dependent Blur for Optical See-Through Head-Mounted Displays

This paper wins the "Best Paper Runner Up Award", and is one of the seven as well.

The blur on HMD is clearly a problem for the manufacturers and users. The blur is viewpoint specific, and is pixel specific. If the image blur is modeled as a Gaussian ellipse on the image plane, then the input of the "blur function" is 5 DOF (pixel location + viewing direction + viewing distance), and the output of the "blur function" is 3 DOF. The mapping is again learned, in order to ignore the complicated optics physical analysis of course. This is an interesting paper because people are discovering problems and finding out solutions for it.

#### Automated Spatial Calibration of HMD Systems with Unconstrained Eye-cameras

This paper is taking advantage of the reflection of IR-led on humans' eyeball, to calculate the spatial relationship between the devices and the eye, potentially this work can facilitate the calibration of optical see-through HMD as well.

### Interesting Ideas

* **Rolling Shutter Camera**, can be used to expedite visual tracking, since the image is not taken as a whole at same time, but the arrival of pixel information is more interpolated, thus the incremental information can help maintain the tracking at a fairly high frame rate.
* Deep learning can help doing sensor fusion of IMU and marker-based visual tracking. Although the performance at this time is not satisfying, I guess it will inspire a lot of research in applying deep learning to sensor fusion. How about collecting a dataset on this?

### One Awesome Work

Check this video: [Reality-Skins](http://www.liors.net/reality-skins).

An example of how awesome AR can be!

### Finally

ISMAR is a great conference. Merida and Cancun are nice places!

<p class="full-width"><img src="/public/image/ismar-me.jpg" alt="Me at ISMAR" style="width:60%;" align="right"/></p>




Thanks for reading!  <i class="em em-lq"></i>
