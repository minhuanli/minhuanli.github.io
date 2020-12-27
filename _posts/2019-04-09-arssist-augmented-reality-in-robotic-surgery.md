---
layout: post
title: ARssist - Augmented Reality in Robotic Surgery
description: We developed an augmented reality application for the bed-side assistant in robotic surgery, called ARssist. ARssist is implemented using Microsoft HoloLens and da Vinci robot. The assistant is able to see virtual overlay of robotic instrument, endoscope and its field-of-view indicator, and the endoscopic video through HoloLens.
tags: augmented-reality hololens medical-robot da-vinci-robot
---

Recently I have been working on an augmented reality project: **ARssist**. It stands for "Augmented Reality Assistant" for robotic surgery (with da Vinci robot).

## Bedside Assistant

In a da Vinci robotic surgery, a bedside-assistant (also called First Assistant) stands at the bedside, helpes the surgeon to complete the operation. The surgeon is seated in the surgeon console manipulating the instruments.

<p class="full-width">
<img src="/public/image/arssist-setup.jpg" width="70%" align="right"/>
</p>

The bedside assistant needs to perform various tasks, for example:
- Insufflation and trocar placement
- Dock and undock the robot
- Instrument exchange
- Manipulating laparoscopic instruments, e.g. stapler, grasper

In ARssist, we provide improved augmented reality visualization to the bedside assistant, to help him or her to accomplish the tasks better. We use HoloLens currently. One significant advantage of using HoloLens-like device for surgery task is that, it is fail-safe. Even if the system fails, the user can still finish the task in the same way he/she usually does without augmented reality.

## Augmented Reality Visualization

ARssist provides the following visulizations:
- Virtual robotic instruments
- Virtual endoscope and its field-of-view
- Hand-held instrument if it is tracked
- Endoscopic video

### Example See-Through View

<div style="position:relative;padding-top:56.25%;">
  <iframe width="100%" src="https://www.youtube.com/embed/kiw07KA3FOs" frameborder="0" allowfullscreen
    style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

The above video is captured using a camera behind the HoloLens. The robotic instruments and endoscope are correctly overlaid with the help of [fiducial-tracking](https://github.com/qian256/HoloLensARToolKit), and [robot kinematics](https://github.com/jhu-dvrk/dvrk-xr). The endoscopic video (bottom right corner) is streamed to the HoloLens, and projected in the field-of-view of the virtual endoscope. The system is perfectly real-time.

<div style="position:relative;padding-top:56.25%;">
  <iframe src="https://www.youtube.com/embed/sJt57IYuofA" frameborder="0" allowfullscreen
    style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe>
</div>

In this video, a robotic instrument is controlled by the bedside assistant, and its overlay is maintained well.

## Evaluation

We have conducted experiments with novice users and experienced users, including surgeons and residents. Two specific tasks were chosen: **instrument insertion** and **laparoscopic tool manipulation**. We will publish more results of evaluation in the near future.

## Link to Publications

For more details, please refer to our papers:

```
@article{qian2018arssist,
  title={ARssist: augmented reality on a head-mounted display for the first assistant in robotic surgery},
  author={Qian, Long and Deguet, Anton and Kazanzides, Peter},
  journal={Healthcare technology letters},
  volume={5},
  number={5},
  pages={194--200},
  year={2018},
  publisher={IET}
}

# Another ICRA 2019 paper
}
```


Thank you for reading! <img class="inline" src="/public/LQ144x144.png" alt="LQ" style="width:1.5rem;height:1.5rem;" />

