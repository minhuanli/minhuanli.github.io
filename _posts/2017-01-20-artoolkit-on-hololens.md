---
layout: post
title: ARToolKit on HoloLens
description: Demonstration of implementing ARToolKit on HoloLens. The capabilit of using the locatable camera of HoloLens to do fiducial marker tracking is exploited.
tags: unity3d hololens hololens-artoolkit artoolkit vuforia marker-tracking augmented-reality
---

[HoloLens](https://www.microsoft.com/microsoft-hololens/en-us) is fascinating in terms of holographic display and in-room localization, but the capability of the front-facing camera ([locatable camera](https://developer.microsoft.com/en-us/windows/holographic/locatable_camera)) is not fully utilized for potential augmented reality applications.

### ARToolKit

Since [ARToolKit](http://artoolkit.org/) has served AR/VR for more than 10 years, and it is open-source, it would be nice to have it running on HoloLens. The obstacles towards this goal are quite clear as well:

* Universal Windows has a whole different set of tools and run-time libraries. The dependencies of existing ARToolKit does not exist on UWP, such as pthreads, video libraries, opencv.
* ARToolKit is written in native C/C++ code, and an additional wrapper is needed for development on Unity, which is recommended for HoloLens. (If you are not good at Direct3D, and Windows App)

**Luckily, after spending some time on this, I successfully get some pieces of code written, and actually make ARToolKit runs on HoloLens.**

The repository is called **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)** on Github.

### Demos

The following videos and screenshots are taken with HoloLensARToolKit [v0.1](https://github.com/qian256/HoloLensARToolKit/releases/tag/v0.1).

#### Samples of HoloLensARToolKit

There are three samples of HoloLensARToolKit, each representing a certain kind of marker that is supported: single marker, cube marker and multi marker.

<p class="full-width">
<iframe width="100%" style="height:24rem" src="https://www.youtube.com/embed/PqT90QfgP-U" frameborder="0" allowfullscreen></iframe>
</p>

#### Minion on the Cube

<p class="full-width">
<iframe width="100%" style="height:24rem" src="https://www.youtube.com/embed/cMzNyJkr3X0" frameborder="0" allowfullscreen></iframe>
</p>

This video is taken on HoloLens Device Portal, also known as **Mixed Reality Capture**. You might have noticed that there is still some lag between the video that is captured and update in the rendering.

#### More Screenshots

- Single Marker

<p class="full-width">
<img src="http://longqian.me/public/image/artoolkit-hololens-single.png" width="70%" align="right"/>
</p>

- Cube Marker

<p class="full-width">
<img src="http://longqian.me/public/image/artoolkit-hololens-cube.png" width="70%" align="right"/>
</p>

- Multi Marker

<p class="full-width">
<img src="http://longqian.me/public/image/artoolkit-hololens-multi.png" width="70%" align="right"/>
</p>


### Finally

You can access more articles describing the implementation details of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)** in my blog, simply clicking on the tag: <a class="no-underline" href="http://longqian.me/tag/hololens-artoolkit/"><code class="highligher-rouge"><nobr>hololens-artoolkit</nobr></code></a>.

With ARToolKit integrated with HoloLens, many more augmented reality applications are possible. If you are AR/VR developer, you must see what I mean here.

Thanks for reading. <i class="em em-lq"></i>
