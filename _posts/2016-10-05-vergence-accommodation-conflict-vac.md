---
layout: post
title: Vergence-Accommodation Conflict (VAC)
description: Vergence and accommodation are two types of stereo cues. The conflict between them causes visual fatigue and motion sickness as well. This blog gives you some facts and some trends.
tags: vergence-accommodation-conflict motion-sickness optics virtual-reality
---

[Vergence-accommodation conflict (VAC)](https://vrwiki.wikispaces.com/Vergence%E2%80%93accommodation+conflict) is a major problem for the use of VR / AR head-mounted displays (HMD).

For a **normal** stereoscopic optical see-through (OST) HMD, it is very intuitive for programmers to render two separate images for each display, representing the virtual camera placed in the location of human eyes. Like Unity3D, the default way to deploy stereo AR / VR application is to place two virtual cameras in the scene, and renders to the left and right screen.

Take me as an example, when I first developed the most simplest application to display a stereo wooden cube on Moverio BT-200, where the cube is placed on a desktop, I noticed that

* when I am focusing on the wooden texture, I cannot see the surrounding real environment
* when I am trying my best to perceive the 3D location of the cube, I cannot see the texture clearly.

This effect is caused by **VAC**.

### What is VAC?

[Vergence](https://en.wikipedia.org/wiki/Vergence) is the simultaneous opposite motion of two eyes to maintain binocular vision, in other word, the viewing angle of two eyes are changed in this procedure to fit the depth of objects, as shown in the right part of image. In the case of HMD, vergence is driven by the **retinal disparity**.

<p class="full-width"><img src="/public/image/vac.png" alt="vac" style="width:80%;" align="right"/></p>
<p align="right">Image courtesy of Gregory Kramida and Amitabh Varshney</p>

[Accommodation](https://en.wikipedia.org/wiki/Accommodation_(eye)) is the occulomotor response to the distance of object, like the focusing procedure on a camera, the muscle controls the focus of eye, in order to see the object clearly. It is illustrated in the left part of image. In AR / VR, accommodation is driven by the retinal blur.

As a result, when the user is looking through an HMD, both eyes focal distance is the imaging plane, which is the embedded HMD screen usually, but the angular difference of eyes is adjusted to a further distance formed by the disparity. Thus, **the distance of the object perceived by accommodation and vergence is different**, lead to VAC.

### Solutions
VAC is still an unsolved problem for AR / VR in general, despite a lot of efforts in the academia and industry to tackle it. Gregory Kramida and Amitabh Varshney have a great survey on the existing solutions to VAC: **Resolving the Vergence-Accommodation Conflict in Head Mounted Displays**. The rest of this part is mainly from this paper.

If we took a look at two different categories of HMDs: stereoscopic and multiscopic, the solutions can be summarized:

* Stereoscopic
	* Varifocal
		* Sliding optics
		* Deformable membrane mirrors [t]
		* Liquid lenses [t]
	* Liquid crystal lenses [t]
		* Multifocal (focal plane stacks)
		* Birefringent lenses [s][t]
		* Freeform waveguide stacks [s]
* Multiscopic
	* Multiview retinal displays [t]
	* Microlens arrays [s]
	* Parallex barriers [s]
	* Pinlight displays [s]

[s] represents that the method is time-multiplexed, and [t] corresponds to time-multiplexed. For the detail of each methods, please refer to the original paper.

#### Light Field Optics

[Light field](https://en.wikipedia.org/wiki/Light_field) is a methods to model light as vector, which has both intensity and direction. Two parallel LCD panels can be used to create light field, so that the display is multiscopic. This work came from MIT Media Lab: **Content-Adaptive Parallax Barriers: Optimizing Dual-Layer 3D Displays using Low-Rank Light Field Factorization**.

<p class="full-width"><img src="/public/image/parallex-barrier.png" alt="parallex barrier" style="width:80%;" align="right"/></p>

This image copied from the paper shows how multiscopic is realized.

Another prototype is demonstrated in the paper: Near-Eye Light Field Displays. In this case, Microlens array is used to create light field.

<p class="full-width"><img src="/public/image/near-eye.png" alt="near eye" style="width:80%;" align="right"/></p>

A software-based retinal blur is applied to the source image in this solution, so that the perceived distance from vergence is same as the perceived distance from accommodation.

The video of the project is awesome:
<p class="full-width">
 <iframe style="width:80%;height:20rem" align="right" src="https://www.youtube.com/embed/uwCwtBxZM7g"></iframe>
</p>

### How About Hololens?

The display technology of Hololens remains a mystery for the general public. It is not purely light field technology, since it is not very bulky, and the display resolution is much higher than people's expectation of light field HMDs. There are a few good posts online discussing about it.

* [How hololens display work?](http://www.imaginativeuniversal.com/blog/post/2015/10/17/how-hololens-displays-work.aspx)
* [Hololens patents and the meaning of them](https://www.reddit.com/r/HoloLens/comments/30v4ve/patents_and_what_they_mean_focus_and_opacity/)
* [Five questions about project hololens](http://www.makeuseof.com/tag/five-questions-microsofts-project-hololens/)

### An Experiment

In order to experience vergence-accommodation conflict, I wrote a simple Cardboard application to demonstrate the issue. Codes are on Github: **[vac_demo](https://github.com/qian256/vac_demo)**

#### Building

* Unity3D (v5.0+)
* GVR SDK (v0.6)
	* v0.6 contains the Unity3D GameObject of two virtual eyes, which is easier for the integration of ImageEffect. v1.0+ re-organizes the two virtual eyes in scripts.
* Access to Unity3D asset store
	* For the access of object materials and models.
* Android SDK (with API 19+)

#### Running

* Android Phone (API 19+)
* Google Cardboard

The Android installation file is VAC.apk in this repository, in case you are not customizing the application. I am using Nexus 5 for testing, and the screenshots below are generated by Nexus 5.

#### Demonstration

In this application, there are many objects with texture, placed at different depth of the scene, e.g. books, tables. The rectile that shows the user gaze finds the current focused object. The focus depth is adjusted accordingly, achieved by Unity3D ImageEffect script. With different gaze, user experiences the effect of depth blur, which is correspondent to the retinal blur of different depth.

<p class="full-width"><img src="/public/image/vac-far.png" alt="vac demo far" style="width:80%;" align="right"/></p>
<p class="full-width"><img src="/public/image/vac-near.png" alt="vac demo near" style="width:80%;" align="right"/></p>
<p align="right">Screenshot of vac_demo at near and far range</p>


 
#### Issue

In order to achieve the effect of focus and defocus, Cardboard un-distortion, there are five rendering passes. In general, post rendering is computationally expensive for mobile platforms. In the case of Nexus 5, the frame rate of this application is 7 fps.

#### Acknowledgement

* [Books Pack](https://www.assetstore.unity3d.com/en/#!/content/5484) assets for the models and materials of books
* [Free Furniture Set](https://www.assetstore.unity3d.com/en/#!/content/26678) assets for the models and materials of chairs and tables
* [Wooden Floor Pack](https://www.assetstore.unity3d.com/en/#!/content/31492) assets for the materials and texture of wooden floor

### Reference

1. VRWiki
2. Light field (Wikipedia)
3. Vergence (Wikipedia)
4. Accommodation (Wikipedia)
5. Lanman, Douglas, and David Luebke. "Near-eye light field displays." ACM Transactions on Graphics (TOG) 32.6 (2013): 220.
6. Kramida, Gregory. "Resolving the Vergence-Accommodation Conflict in Head-Mounted Displays." IEEE transactions on visualization and computer graphics 22.7 (2016): 1912-1931.
7. Lanman, Douglas, et al. "Content-adaptive parallax barriers: optimizing dual-layer 3D displays using low-rank light field factorization." ACM Transactions on Graphics (TOG) 29.6 (2010): 163.




Thanks for reading!  <i class="em em-lq"></i>
