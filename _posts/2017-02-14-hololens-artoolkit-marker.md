---
layout: post
title: ARUWPMarker Options in HoloLensARToolKit v0.1
description: Documentation of project HoloLensARToolKit v0.1, the ARUWPMarker script used in HoloLensARToolKit, including the detailed explanation of its attributes, and common usecases.
tags: hololens hololens-artoolkit artoolkit unity3d marker-tracking documentation augmented-reality
---

This post is part of documentation of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**, version **[v0.1](https://github.com/qian256/HoloLensARToolKit/releases/tag/v0.1)**.

### ARUWPMarker

`ARUWPMarker.cs` is one of the main scripts used in **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**. In this post, the options of this script are listed and discussed, along with common usecases.

> In Unity project using HoloLensARToolKit package, each actual marker must have one corresponding ARUWPMarker script.

ARUWPMarker is very similar to ARMarker in ARToolKit. However, because currently HoloLensARToolKit does not support NFT (Natural Feature Marker) of ARToolKit, that part of attributes are not included in ARUWPMarker.

When ARUWPMarker script is attached to some Unity GameObject, its inspector window looks like this:

<p class="full-width">
<img src="http://longqian.me/public/image/aruwpmarker-hiro.png" width="70%" align="right"/>
</p>

and the inspector behavior of `ARUWPMarker.cs` is controlled by `ARUWPMarkerEditor.cs` located at `Assets/Editor/`.

#### Type

This field configures the type of the current marker. Available options are: `single`, `single_barcode`, `single_buffer`, and `multi`.

* `single`: single pattern marker, e.g. Hiro marker and Kanji marker. If `single` is selected, then the field `File Name` will appear. Root path of file name is `Assets/StreamingAssets/`.
* `single_barcode`: single barcode marker (as known as single matrix marker). If it is selected, then the field `Barcode ID` will appear.
* `single_buffer`: single pattern marker, but directly specified by a byte buffer. It should be set at runtime using function `ARUWPMarker::setSingleBufferBuffer`.
* `multi`: multi marker consists of multiple barcode marker. If it is selected, then the field `File Name` will appear to ask for the configuration file. Root path of the configuration file is `Assets/StreamingAssets/` as well.

#### Size in mm

You need to specify the size of the marker (outer border), when `single` or `single_barcode` marker is used.

#### Show Options

If it is checked, filtering options of marker tracking can be configured, including: `Continuous Pose Estimation` and `Confidence Cutoff`. Please refer to ARToolKit documentation for details about filtering.

#### Visualization Target

Marker pose provided by the algorithm contains position and orientation. This information should be applied to some object in the scene so that augmented reality experience is created. This field controls the target GameObject that receives the pose of marker.

#### Anchored to World

> HoloLens is constantly localizing itself in the room.

The default augmented reality experience of HoloLens is creating an AR scenario within the room, and let the user explore it. Therefore, HoloLensARToolKit package takes advantage of its localization algorithm, to make the virtual object appear in the world coordinate system. The benefit of doing it is that, when the marker is occluded, it stays at the same position in the room. It is desired when the line-of-sight of the HoloLens camera is blocked, but the tracked object is not moving in the environment.

If this field is not checked, then all the pose update is achieved in the camera coordinate system. The virtual object stays at the same pose with respect to the camera, when the tracking is lost.

#### Apply Rotation

Whether rotation of tracked marker should be applied to the **Visualization Target**.

#### Apply Translation

Whether translation (position) of tracked marker should be applied to the **Visualization Target**.

#### Confidence Textbox and Confidence Colorbox

If the marker type is `single`, `single_barcode` or `single_buffer`, then ARToolKitUWP provides a score representing the confidence of tracking, ranging from 0 to 1. The score could be visualized in a textbox (`Unity::UI::Text` object) and in a colorbox (`Unity::UI::Image` object).

### Examples

#### Hiro Marker

<p class="full-width">
<img src="http://longqian.me/public/image/aruwpmarker-hiro.png" width="70%" align="right"/>
</p>

#### Matrix Marker (Number 0)

<p class="full-width">
<img src="http://longqian.me/public/image/aruwpmarker-matrix.png" width="70%" align="right"/>
</p>

#### Cube Marker

<p class="full-width">
<img src="http://longqian.me/public/image/aruwpmarker-cube.png" width="70%" align="right"/>
</p>





### Finally

You can access more articles describing the implementation details of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)** in my blog, simply clicking on the tag: <a class="no-underline" href="http://longqian.me/tag/hololens-artoolkit/"><code class="highligher-rouge"><nobr>hololens-artoolkit</nobr></code></a>.



Thanks for reading!  <i class="em em-lq"></i>

