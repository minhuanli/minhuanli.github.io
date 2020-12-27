---
layout: post
title: ARUWPVideo Options in HoloLensARToolKit v0.2
description: Documentation of project HoloLensARToolKit v0.2, the ARUWPVideo script used in HoloLensARToolKit, including the detailed explanation of its attributes, and common usecases.
tags: hololens hololens-artoolkit artoolkit unity3d marker-tracking documentation augmented-reality
---

This post is part of documentation of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**, version **[v0.2](https://github.com/qian256/HoloLensARToolKit/releases/tag/v0.2)**.

### ARUWPVideo

`ARUWPVideo.cs` is one of the main scripts used in **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**. In this post, the options of this script are listed and discussed, along with common usecases.

> Each Unity project using HoloLensARToolKit package **must and must only have one** ARUWPVideo component.

ARUWPVideo is unique to HoloLensARToolKit v0.2. In previous version: v0.1, the video pipeline is embedded in `ARUWPController.cs`, which inevitably made video capture and rendering in the same thread. Starting v0.2, the video pipeline uses APIs directly from [Windows.Media.Capture](https://docs.microsoft.com/en-us/uwp/api/windows.media.capture.mediacapture), and is asynchronous with rendering and tracking.

When ARUWPVideo script is attached to some Unity GameObject, its inspector window looks like this:

<p class="full-width">
<img src="http://longqian.me/public/image/aruwpvideo-v02.png" width="70%" align="right"/>
</p>

#### Enable Video Preview

This field configures whether video preview is enabled. When it is checked, the video pipeline saves an additional copy of the bitmap, and renders to Unity `Texture2D` object when the next `Update()` function is called.

#### Video Preview Holder

This field will appear when **Enable Video Preview** is checked. Any object with a proper Renderer can be a preview holder. During runtime, the bitmap fetched from video pipeline will be drawn onto this object. In the sample scenes of HoloLensARToolKit, this field is a Quad object anchored to the top-left corner from user's perspective, similar to a debugging windows.

#### Video FPS Holder (optional)

This field is looking for a `Unity.UI.Text` object to print out video frame rate. It is very useful for debugging, or inspecting the performance of the application. In the sample scenes provided by HoloLensARToolKit, this text field is at the top-right corner for the user. Because it is not a required component for tracking to run, this field can be left blank.

Also note that the maximum video preview rate that HoloLens supports is 30 fps. [Really?](https://developer.microsoft.com/en-us/windows/mixed-reality/locatable_camera)


### Finally

You can access more articles describing the implementation details of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)** in my blog, simply clicking on the tag: <a class="no-underline" href="http://longqian.me/tag/hololens-artoolkit/"><code class="highligher-rouge"><nobr>hololens-artoolkit</nobr></code></a>.



Thanks for reading!  <i class="em em-lq"></i>

