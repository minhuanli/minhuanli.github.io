---
layout: post
title: Coorindate Systems in HoloLensARToolKit v0.1
description: Documentation of project HoloLensARToolKit v0.1, the coordinate systems used in HoloLensARToolKit, including the difference between unity3d coordinates, ARToolKit coordinates and HoloLensARToolKit coordinates.
tags: hololens hololens-artoolkit artoolkit unity3d marker-tracking coordinate-system documentation augmented-reality
---

This post is part of documentation of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**, version **[v0.1](https://github.com/qian256/HoloLensARToolKit/releases/tag/v0.1)**.

### Coordinate System of Unity3D
[Unity3D](https://unity3d.com/) uses **left-hand coordinate systems** to define transformations. Yes, it is.

<p class="full-width">
<img src="http://longqian.me/public/image/unity-coord.png" width="70%" align="right"/>
</p>

The above is a screenshot of a Unity transformation. The x, y, z axis directions are visualized with different colors, and are following left-land rules. In addition, rotation along axis is applied **clockwise**, unlike counter-clockwise in right-hand coordinate systems. If you are accustomed to right-hand coordinate systems as I do, please pay more attention when working with raw 4x4 matrices.



### Coordinate System of ARToolKit
[ARToolKit](http://artoolkit.org/) uses **right-hand coordinate systems**. Since [OpenGL](https://www.opengl.org/) is right-handed as well, it is very comfortable to visualize the tracking result of ARToolKit by OpenGL.

In the official Unity package of ARToolKit, [arunity](https://github.com/artoolkit/arunity5), there exists a utility function

```csharp
public static Matrix4x4 LHMatrixFromRHMatrix(Matrix4x4 rhm)
```

that converts the tracking result of ARToolKit to Unity environment.

### Coordinate System of HoloLensARToolKit
It took me a while to figure out the complicated conversions happened inside ARToolKit, inside Unity, and in-between.

In this project, left-hand coordinate system is applied **everywhere**. That means, the multi-marker configuration, the tracking algorithm, the returned tracking result from native code, and of course, the visualization inside Unity. It will be elaborated by the following examples.

#### Single Pattern Marker
Hiro marker and Kanji marker are examples of single pattern marker. They are defined using binary files.

The coordinate system associated with a single pattern marker looks like this:

<p class="full-width">
<img src="http://longqian.me/public/image/hiro-coord.png" width="70%" align="right"/>
</p>

#### Single Matrix Marker
Single matrix marker is pre-defined in ARToolKit. User is only required to provide the ID and type of matrix code associated when using them in applications. The coordinate system associated with a matrix marker looks like this:

<p class="full-width">
<img src="http://longqian.me/public/image/matrix-coord.png" width="70%" align="right"/>
</p>

#### Multi Matrix Marker
Multi matrix marker is defined by a configuration file, that contains

* total number of matrix markers
* the ID of each matrix marker
* the transformation from the multi-matrix marker to individual matrix marker.

Multi-matrix marker is useful for robust tracking, thus is much more useful for accuracy-critical augmented reality applications. [Iterative Closest Point (ICP)](https://en.wikipedia.org/wiki/Iterative_closest_point) algorithm is the underlying method for the fusion of tracking information.

The transformation field in the configuration file is also left-handed, which is different from original ARToolKit. That is to say, you have to modify the marker configuration file you used before.

For example, for a **multi-barcode-4x3** configuration, the coordinate system of the multi-marker looks like this:

<p class="full-width">
<img src="http://longqian.me/public/image/multi-coord.png" width="70%" align="right"/>
</p>

Thus, the transformation field of marker 0 (top-left), will be:

```
1.0  0.0  0.0  -105.00
0.0  1.0  0.0  -70
0.0  0.0  1.0  0.0
```

instead of

```
1.0  0.0  0.0  -105.00
0.0  1.0  0.0  70
0.0  0.0  1.0  0.0
```

in original ARToolKit.

### Finally

You can access more articles describing the implementation details of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)** in my blog, simply clicking on the tag: <a class="no-underline" href="http://longqian.me/tag/hololens-artoolkit/"><code class="highligher-rouge"><nobr>hololens-artoolkit</nobr></code></a>.



Thanks for reading!  <i class="em em-lq"></i>

