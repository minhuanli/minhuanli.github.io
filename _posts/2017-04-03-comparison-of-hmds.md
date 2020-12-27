---
layout: post
title: Hands on Head-Mounted Displays
description: I have worked with many augmented reality platforms, especially head-mounted displays (HMD). In this post, I would like to share the experience of developing or playing with these head-mounted displays, and hopefully the comparison help you to choose the correct head-mounted display for your applications.
tags: augmented-reality hololens pupil-labs virtual-reality
---


I have worked with many augmented reality platforms, especially [Head-Mounted Displays (HMD)](https://en.wikipedia.org/wiki/Head-mounted_display).

In this post, I would like to share my experience of developing or playing with these devices. Hopefully, this will help you to make the correct decision about which HMD to choose for your specific application. 



### Table of Content

- Epson Moverio BT-200
- Epson Moverio BT-300
- Meta 1
- ODG R-6
- ODG R-7
- Microsoft HoloLens
- Google Glass
- Google Cardboard
- Google Tango
- JINS MEME
- Pupil-Labs
- Oculus Rift DK2 for AR
- ......


### Epson Moverio BT-200

<p class="full-width">
<img src="/public/image/moverio-bt200.jpg" width="80%" align="right"/>
</p>

[Epson Moverio BT-200](https://epson.com/moverio-augmented-reality-smart-glasses) is the first head-mounted display that I worked with, and that was 2 years ago. It is a pretty good HMD to start with, because it has all the fundamental components of an AR HMD: stereoscopic beam-splitter optical display, front-facing camera, IMU, programming interface (Android). Programmers and researchers can do most of the things that they want with BT-200. However, its performance is not very satisfying if your expectation is high. Its field-of-view is very narrow; the front-facing camera is not high quality; it is not powerful in terms of computation.

Given the fact that it appears on the market quite early (3 years ago), and its relatively low price at that time, BT-200 is a reasonable choice for a long time until the appearance of its succesor BT-300. 


### Epson Moverio BT-300

<p class="full-width">
<img src="/public/image/moverio-bt300.jpg" width="80%" align="right"/>
</p>

[Epson Moverio BT-300](https://epson.com/moverio-augmented-reality-smart-glasses) appears on the market at the end of 2016. We received it after almost one-year waiting after the pre-order. It inherited most of Moverio BT-200 features, but with huge improvemnet in most aspects.

* The screen resolution and illuminace is enhanced
* The front-facing camera quality is much better
* Lighter
* Much more computational power
* Support glasses
* Better fixture with repsect to user's head

More surprisingly, the price is still the same as BT-200, which makes it very appealing under budget. 



### Meta 1

<p class="full-width">
<img src="/public/image/meta1.jpg" width="80%" align="right"/>
</p>

Meta 1 is developed by [MetaVision Inc](https://www.metavision.com/), a relatively small but focused team. The idea of Meta 1 is treating the head-mounted display as an external monitor of the computer. In other words, Meta 1 does not have on-chip computation capcability, and should be always tethered to the computer. However, this sacrifice brings clear advantages. Meta 1 has a RGBD front-facing camera, enabling more advanced tracking and interaction with its applications, and since it is using PC's computation resources, it could perform much more complicated algorithms at runtime, that would not be possible without powerful GPUs.

Meta 1 appears on the market 4 years ago, and noticeably, the stereoscopic beam-splitter optical design of Meta 1 is same as that of Moverio BT-200.

Therefore, if your application does not involve people freely walking around, Meta 1 is good choice. Meta 2 is already available now. Similarly, Meta is also tethered HMD, but with an impressively wide-FOV holographic display.



### ODG R-6

[ODG R-6](http://www.osterhoutgroup.com/presskit/R-6-TechSheet.pdf) is manufactured by [Osterhout Group Inc](http://osterhoutgroup.com). My experience with ODG R-6 is not good, because the device assumes a narrower head than mine, and it basically cannot be put on my head at all. Apparently, the company sees the the problem and the R-7 is much more comfortable to wear. 

### ODG R-7

<p class="full-width">
<img src="/public/image/odg-r7.jpg" width="80%" align="right"/>
</p>

[ODG R-7](http://osterhoutgroup.com/products-r7.php) is the successor of ODG R-6. ODG R-7 is more ergonomical friendly, and also slightly more powerful than ODG R-6. The optical design of R-7 and R-6 is same. They operate on a customized Android, called ReticleOS. The mechanical design of them is quite unique, with magnetic connectors everywhere. The front-facing RGB camera is of high quality as well.

However, there is one particular issue with ODG devices, after being used for a while, the device becomes hot. Even though the performance of the device is still normal, it at least makes users uncomfortable or feeling unsafe.


### Microsoft HoloLens

<p class="full-width">
<img src="/public/image/hololens.jpg" width="80%" align="right"/>
</p>

From my opinion, [Microsoft HoloLens](https://www.microsoft.com/microsoft-hololens/en-us) is the most fascinating HMD at present, and is also the HMD that I used most. HoloLens is part of a large project at Microsoft, and is the joint effort of Window Holographic System, Microsoft Holographic Processing Unit (HPU), Universal Windows Platform, and the [SLAM](https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping) (Simultaneous Localization and Mapping) research at Microsoft.

The spatial mapping of HoloLens is probably the most stable SLAM system I have ever seen. It enables the user to place holograms in the room, and staying at the same location however the user moves. This capability makes world-anchored augmented reality applications super easy to implement.

The optics design of HoloLens is special among many off-the-shelf displays, with four waveguides combined and refreshed at 240Hz. The focal plane of HoloLens is close to 1m. With the motion cue provided by spatial mapping, user is able to feel that the virtual objects are fixed at variable distances. However, since there is no official documentation about its optics, and Microsoft markets HoloLens as Holographic waveguide technology, we are not sure about what is exactly going on beneath the goggle.

HoloLens is using Universal Windows Platform, an Operating System that Microsoft develops for portable devices. The APIs are quite complete and well-documented. It is well-integrated with [Unity3D](https://unity3d.com/) game engine. Making applications with Unity3D to run on HoloLens is already stable, in addition, the [native programming interface](http://longqian.me/2017/01/29/unity-native-programming/) in Unity3D enables more advanced use of low-level .NET or DirectX features. I build a package, **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**, taking advantage of it.

Of course HoloLens has its problems, it is heavy; the learning curve is XXX; it is expensive compared to other HMDs.


### Google Glass

<p class="full-width">
<img src="/public/image/google-glass.jpg" width="60%" align="right"/>
</p>

Google starts early in AR, and built maybe the most famous HMD, [Google Glass](https://en.wikipedia.org/wiki/Google_Glass). When we try to explain to people the concept of head-mounted display, we always say **'Google Glass is an AR HMD'**, and people will suddenly understand. Google Glass is famous, but not successful. If we look at medical application involving head-mounted display, there are many early researches and papers dedicated to it.


### Google Cardboard

#### Cardboard v1

<p class="full-width">
<img src="/public/image/cardboard-1.jpg" width="60%" align="right"/>
</p>

#### Cardboard v2

<p class="full-width">
<img src="/public/image/cardboard-2.jpg" width="60%" align="right"/>
</p>

[Google Cardboard](https://vr.google.com/cardboard/) 1 and 2 are virtual reality headsets. It is an impressive idea to take advantage of the popularity of smartphones to make VR applications accessible to everyone. It is not a complicated task to develop VR applications with Google Cardboard, using the [GVR SDK](https://github.com/googlevr/gvr-unity-sdk). The interaction with Google Cardboard is very limited as a tradeoff for its simplicity. For Cardboard 1, there is a magnetic trigger, and for Cardboard 2, there is a touch buttom. IMU is required for navigation in the VR environment. I have another post depicting more details about [my experience with Google Cardboard](/2016/10/16/google-cardboard-as-augmented-reality-headset/).

Google Daydream is the successor for Google Cardboard, in my opinion, with more methods of interaction, and elegant design. But it still remains unknown to me how much can this product achieve.


### Google Tango

<p class="full-width">
<img src="/public/image/tango.jpg" width="80%" align="right"/>
</p>

[Google Tango](https://get.google.com/tango/) is another Google product related to augmented reality. It is a tablet instead of a HMD. Tango is an experiment with **SLAM** on mobile devices. Contrary to what Microsoft is doing, Google focuses more on mobile market, because of the potential of introducing AR infrastructure to Android devices. The first Tango-based smartphone, [Lenovo Phab 2 Pro](http://shop.lenovo.com/us/en/tango), was released last year. I believe it is only the beginning.

The SLAM experience with Tango is not as good as HoloLens for me, I think one of the difference is that, HoloLens environmental understanding cameras covers a significantly larger volumne.


### JINS MEME

<p class="full-width">
<img src="/public/image/jins-meme.jpg" width="80%" align="right"/>
</p>

[JINS](https://www.jins.com/us/) is a large eyewear manufacturer based in Japan. [JINS MEME](https://jins-meme.com/en/products/es/) is a piece of eyewear integrated with some electrooculography sensors. It is able to sense the motion of human eyeball. As can be seen from the picture, JINS MEME is very well designed. It is almost the same as a normal pair of glasses.

You can monitor the raw sensor data via network. Efforts are needed to give meaning to the raw data. For example, if you want to detect the motion of eye, then a training procedure is essential. The stability and feasibility of using  electrooculography sensing data for interaction is not yet proven.


### Pupil-Labs

<p class="full-width">
<img src="/public/image/pupil.jpg" width="80%" align="right"/>
</p>

[Pupil-labs](https://pupil-labs.com/) is a startup company based in Berlin, Germany. The main product of the team is the head-mounted eye-tracking hardware and software. The eyewear frame is 3D-printed, modular-designed; the software is open-source; the plugin interface is very easy to use. Their products are quite modern in many senses. Compared with [Tobii](http://www.tobii.com/), pupil-labs is more open and accessible, although the tracking accuracy might not be as good. You can find all its code on [Github](https://github.com/pupil-labs), from pupil tracking algorithm, to the software infrastructure.

In addition, pupil-labs comes up with the integration with many AR / VR devices, for example, Moverio BT-300, Oculus Rift, and HoloLens.

I enjoyed using and programming with pupil-labs eye-tracker for its beautiful hardware and software! Here is a Github repository **[pupil_ros_plugin](https://github.com/qian256/pupil_ros_plugin))**, to build the bridge between pupil-labs and [ROS](http://www.ros.org/).


### Oculus Rift DK2 for AR

<p class="full-width">
<img src="/public/image/oculus.jpg" width="80%" align="right"/>
</p>

This image shows a customized [Oculus Rift DK2](https://www3.oculus.com/en-us/dk2/) that was done in our lab two years ago. Oculus Rift DK2 is an extremely successful VR headset. By equipting two fish-eye cameras, it is turned to be a video see-through HMD, that is suitable for many AR applications. It is tethered to PC as usual, requiring high-end computer configuration, wide field-of-view, and is easy to program. AR HMDs are typically divided into two categories: optical see-through (OST) and video see-through (VST). VST-HMD has the advantage of good registration between virtuality and reality. We developed a lot of demos using this system.

The drawbacks are quite obvious as well: there are too many cables making the workspace very cumbersome; the processing requirement is very demanding; VST-HMD is not fail-safe for many real-life applications, for example in medical scenarios.


### The Waitlist

* [Meta 2](https://buy.metavision.com/products/meta2)
* [Daqri Smart Helmet](https://daqri.com/products/smart-helmet/)
* [ODG R-9](http://osterhoutgroup.com/products-r9.php)
* [Google Daydream](https://vr.google.com/daydream/)

### Conclusions

As you may see, there are many HMDs come into the arena these years. However, the technology is still far from perfect. None of these devices is absolutely better than anyone else. Tradeoffs exist in many aspects: tethered v.s. non-tethered, OST v.s. VST, binocular v.s. holographic, etc. It is very important for users to identify the exact need and make best choices among all these tradeoffs.

I would like to thank Alexander Barthel for taking many of the photos above, and feel free to use them.

Thanks for reading! <img class="inline" src="/public/LQ144x144.png" alt="LQ" style="width:1.5rem;height:1.5rem;" />

