---
layout: post
title: HoloLens Video Streaming
description: An applicaiton to stream video output to HoloLens, and to display the virtual video in 3D environment. TCP communication and JPEG compression are applied.
tags: hololens augmented-reality video streaming tcp networking unity3d
---

There have been lots of discussion about streaming on HoloLens. Here is a demo of my implementation.

### Demo

<p class="full-width">
<iframe width="100%" style="height:20rem" src="https://www.youtube.com/embed/RJ2GBQWfjvg?cc_load_policy=1" frameborder="0" allowfullscreen></iframe>
</p>

This is the soccer match between Barcelona and Atlético Madrid today. The screen on the right is the real monitor, and the left one is a virtual screen showing streamed video. 
The application runs at a reasonably frame rate and resolution (20fps with 896x594 frame resolution). Video is taken via [HoloLens Device Portal](https://developer.microsoft.com/en-us/windows/holographic/using_the_windows_device_portal).

### Implementation

This application is implemented using the following toolset:

#### On PC

* Epiphan DVI2USB 3.0 and its SDK
* Python for `socket`, `queue`, and interfacing Epiphan SDK via `ctypes`
* Network connection

#### On HoloLens

* Made with Unity 5.5.0f3
* `Windows.Networking.Sockets.StreamSocket`
* [HoloToolkit](https://github.com/Microsoft/HoloToolkit-Unity)
* Network connection




Thanks for reading!  <i class="em em-lq"></i>
