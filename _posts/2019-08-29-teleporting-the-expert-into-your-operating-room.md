---
layout: post
title: Teleporting the Expert Surgeon into Your OR
description: This blog describes our hackathon project "Teleporting the Expert into Your OR" of 2019 Medical Augmented Reality Summer School (MARSS). The summer school was hosted in Balgrist Hospital, Zurich. We use HoloLens2 to visualize a real-time point cloud generated from Azure Kinect.
tags: augmented-reality hololens2 azure-kinect unity3d computer-vision
---

The [Medical Augmented Reality Summer School (MARSS) 2019](https://www.medicalaugmentedreality.org/) was successfully hosted in Balgrist Hospital, Zurich, during Aug 5-16. 

It was a two-week event. Over the second week, participants formed teams and developed medical augmented reality projects. Our team worked on the project **Teleporting the Expert Surgeon into Your OR**. It was a quite successful Hackathon project with many exciting memories, and luckily, we won the **Audience Award** of the summer school.

<div style="position:relative;padding-top:56.25%;">
  <iframe width="100%" src="https://www.youtube.com/embed/Ce_H0Nw0QzQ" frameborder="0" allowfullscreen
    style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

Above is our project demo video. In this blog post, I would like to share with you my experiences of this project and the summer school.

## The Idea

Telepresence is not a new idea in the mixed reality community. Imagine a "3D Skype" app, where you can see your friend walking around in your own 3D space. In the medical domain, such fun idea can be actually very useful. We propose to teleport an expert surgeon into the operating room of a less experienced young surgeon. Via realistic 3D telepresence, the expert surgeon can explain to the young surgeon about the procedure, and provide hand-over-hand guidance.

<p class="full-width">
<img src="/public/image/marss19-sketch.png" width="80%" align="right"/>
</p>

Here is the picture of our project illustration during brainstorming. 

## New Toys

Everyone gets his or her own excitement from the summer school. For me, the most exciting part is to have hands-on experience on the new or even **unreleased** devices: [Azure Kinect](https://azure.microsoft.com/en-us/services/kinect-dk/) and [HoloLens 2](https://www.microsoft.com/en-us/hololens). Thanks to Nassir, Microsoft is convinced to borrow us a few HoloLens 2 devices for development.

The pipeline of our system is pretty clear:

1. With Azure Kinect, we capture the real-time RGB and depth image of the surgeon. 
2. Substract the background of the depth image
3. We convert the RGB and depth image into a colored point cloud, with proper calibration parameters.
4. The point cloud is streamed to the HoloLens
5. Visualize the point cloud on HoloLens.

The GPU of HoloLens 2 is much improved over the first generation, which could support the rendering of **MORE** points. While I was developing ARAMIS (to appear in MICCAI 2019), where a point cloud is streamed to HoloLens 1, the major performance bottleneck I identified is the visualization of points, instead of the bandwidth of streaming. HoloLens 2 perfectly solves this by offering a better GPU.

The field-of-view of HoloLens 2 is great. It becomes even more obvious when I came back in the lab and put on HoloLens 1. The interaction paradigm with HoloLens 2 is completely different. It is so natural that you can interact with holograms with your intuition. The system understands your intention very well by tracking your hands.

## The Iterations

We went through three development phases within the Hackathon week.

In the first phase, we developed a fake PC-based server to generate arbitrary point cloud, and a point cloud client on Unity Editor. The first phase sets a starting point for everyone to separately work on their own parts.

In the second phase, Federica worked on the PC server, including point cloud generation from Azure Kinect, background substraction, interations to tune the behavior of the server. I worked on the HoloLens 2 program to receive, and visualize the point cloud. Arnaud worked on the user interation on HoloLens 2 using [MRTK](https://github.com/microsoft/MixedRealityToolkit-Unity). Christ worked on the clinical part and designed the demo.

In the third phase, everything got combined together, optimized and we made the demo video (of course, over the night).

## The Demo

The last day of summer school was dedicated to demos. We saw the excitement from the faces of our audience.


Dr. Farshad acting the expert surgeon (he is) to his fellow:

<p class="full-width">
<img src="/public/image/marss19-demo1.png" width="80%" align="right"/>
</p>

A virtual me shaking hand with participants:

<p class="full-width">
<img src="/public/image/marss19-demo2.png" width="80%" align="right"/>
</p>


A virtual me doing high-five with participants:

<p class="full-width">
<img src="/public/image/marss19-demo3.png" width="80%" align="right"/>
</p>



## Our Team

I feel very lucky to work with these enthusiastic people during the summer school.

<p class="full-width">
<img src="/public/image/marss19-group.png" width="80%" align="right"/>
</p>

We are group 14. 

- Team mentor： [Prof. Ulrich Eck](http://campar.in.tum.de/Main/UlrichEck).
- Clinical partner: [Dr. Christian Hofsepian](https://www.linkedin.com/in/christian-hofsepian-258a4a18b)
- Industrial partner: [Dr. Federica Bogo](https://www.microsoft.com/en-us/research/people/febogo/)
- Engineering student: [Arnaud Allemang-Trivalle](https://www.linkedin.com/in/arnaud-allemang-trivalle) and me.

Thank you for reading! <img class="inline" src="/public/LQ144x144.png" alt="LQ" style="width:1.5rem;height:1.5rem;" />

