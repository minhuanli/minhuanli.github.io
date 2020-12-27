---
layout: post
title: ARUWPController Options in HoloLensARToolKit v0.2
description: Documentation of project HoloLensARToolKit v0.2, the ARUWPController script used in HoloLensARToolKit, including the detailed explanation of its attributes, and common usecases.
tags: hololens hololens-artoolkit artoolkit unity3d marker-tracking documentation augmented-reality
---

This post is part of documentation of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**, version **[v0.2](https://github.com/qian256/HoloLensARToolKit/releases/tag/v0.2)**. 
The ARUWPController options documentation for [v0.1](https://github.com/qian256/HoloLensARToolKit/releases/tag/v0.1) is [here](http://longqian.me/2017/02/14/hololens-artoolkit-controller/).

### ARUWPController

`ARUWPController.cs` is one of the main scripts used in **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**. In this post, the options of this script are listed and discussed, along with common usecases.

> Each Unity project using HoloLensARToolKit package **must and must only have one** ARUWPController component.

ARUWPController is very similar to ARController in ARToolKit, one of the major difference is that ARUWPController targets only at Universal Windows Platform, while ARController also handles Android, iOS, standalone and even editor. Therefore, ARUWPController has fewer attributes than ARController in general.

When ARUWPController script is attached to some Unity GameObject, its inspector window looks like this:

<p class="full-width">
<img src="http://longqian.me/public/image/aruwpcontroller-v02-sim.png" width="70%" align="right"/>
</p>

#### Use Camera Param

- The checkbox to indicate how to initialize the camera parameters
- If this box is check, then the field **Camera Param Filename** will appear. If not, then users must manually initialize the camera parameter via setting a byte buffer, by calling `ARUWPController.SetCameraParamBuffer()` 

#### Camera Param Filename

- This field specifies the name of camera calibration file, contained in the path `Assets/StreamingAssets/`. 
- The camera calibration file must be ARToolKit format. It is a binary file, instead of XML or YAML for OpenCV. Please refer to **[HoloLens Camera Calibration](https://github.com/qian256/HoloLensCamCalib)** project for more details.

#### Pattern Detection Mode

This field configures what kind of marker does the detection algorithm look for.

- If pattern markers only, e.g. Hiro or Kanji, then `AR_TEMPLATE_MATCHING_COLOR` or `AR_TEMPLATE_MATCHING_MONO` is enough.
- If matrix marker only, e.g. 3x3 code marker, then `AR_MATRIX_CODE_DETECTION` is sufficient.
- If there is need to detect both kinds of marker, then `AR_TEMPLATE_MATCHING_COLOR_AND_MATRIX` pr `AR_TEMPLATE_MATCHING_MONO_AND_MATRIX` must be chosen.

#### Matrix Code Type

This field will appear if the **Pattern Detection Mode** involves the detection of matrix marker. There are many types of matrix marker, some of them are supported by ARToolKit and this project. The most common marker set is `AR_MATRIX_CODE_3x3`. All available options are:

- `AR_MATRIX_CODE_3x3`
- `AR_MATRIX_CODE_3x3_PARITY65`
- `AR_MATRIX_CODE_3x3_HAMMING63`
- `AR_MATRIX_CODE_4x4`
- `AR_MATRIX_CODE_4x4_BCH_13_9_3`
- `AR_MATRIX_CODE_4x4_BCH_13_5_5`

#### Track FPS Holder (optional)

This field is looking for a `Unity.UI.Text` object to print out tracking frame rate. It is very useful for debugging, or inspecting the performance of the application. In the sample scenes provided by HoloLensARToolKit, this text field is at the top-right corner for the user. Because it is not a required component for tracking to run, this field can be left blank.

#### Render FPS Holder (optional)

Similar to **Track FPS Holder (optional)**, this field is optional, and is able to visualize the frame rate of rendering of the application. The rendering here means the refreshing of the whole application, but not the refreshing of video.

#### Advanced Options

The above options are essential, and should be taken care for each application. If **Advanced Options** is checked, more options will be listed for users to configure the performance of ARUWPController. The following screenshot shows the full list of options:

<p class="full-width">
<img src="http://longqian.me/public/image/aruwpcontroller-v02-adv.png" width="70%" align="right"/>
</p>

#### Border Size

The percentage of border of the marker, by default, it is 0.25. For example, in a 80cm width marker, the border is 20cm (25%). 

#### Labeling Mode

It configures the color of the border of the marker. `AR_LABELING_BLACK_REGION` is the default.

#### Image Proc Mode

The mode of image processing, by default, `AR_IMAGE_PROC_FRAME_IMAGE` is chosen.

According to ARToolKit documentation, 

> When the mode is `AR_IMAGE_PROC_FIELD_IMAGE`, ARToolKit processes pixels in only every second pixel row and column. This is useful both for handling images from interlaced video sources (where alternate lines are assembled from alternate fields and thus have one field time-difference, resulting in a "comb" effect) such as Digital Video cameras.

#### Thresholding Mode

You can choose different thresholding algorithm from the droplist, same as ARToolKit. Available options are:

- `AR_LABELING_THRESH_MODE_MANUAL`
- `AR_LABELING_THRESH_MODE_AUTO_MEDIAN`
- `AR_LABELING_THRESH_MODE_AUTO_OTSU`
- `AR_LABELING_THRESH_MODE_AUTO_ADAPTIVE`
- `AR_LABELING_THRESH_MODE_AUTO_BRACKETING`

#### Threshold

This field appears when the **Thresholding Mode** is set to `AR_LABELING_THRESH_MODE_MANUAL`. ARToolKit first thresholds the grayscale image before corner extraction. It is easy to understand that the value applied here will be used as the threshold to obtain black and white image.


### Finally

You can access more articles describing the implementation details of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)** in my blog, simply clicking on the tag: <a class="no-underline" href="http://longqian.me/tag/hololens-artoolkit/"><code class="highligher-rouge"><nobr>hololens-artoolkit</nobr></code></a>.



Thanks for reading!  <i class="em em-lq"></i>

