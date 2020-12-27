---
layout: post
title: Eigen in Unity
description: Eigen provides very good support for linear algebra algorithms, but is in general working in C++. On the other hand, Unity game engine does not have ready-to-use packages for linear algebra needs, and only has scripting support for C# and Javascript. This post demonstrates how to use Eigen in Unity.
tags: unity3d eigen native-programming csharp cpp
---

Unity3d has very basic linear algebra support, for example, in [Matrix4x4](https://docs.unity3d.com/ScriptReference/Matrix4x4.html), there are simple multiplication functions with vectors and matrices, however, functions like **inverse** and **eigen value** are not included. **[Eigen](http://eigen.tuxfamily.org)** is the perfect candidate of performing complicated linear algebra algorithms, for example, **Singluar Value Decomposition**, **Sparse Matrix**, **Linear Eqaution Solver**.


### Unity Native Programming

The key idea of integrating Eigen with Unity3d is using the native programming interface of .NET. Here is another example: [Native Programming in Unity](http://longqian.me/2017/01/29/unity-native-programming/). Basically, the native programming interface of unity provides a way for .NET environment to call C functions defined in built dynamic libraries.

What we will do is:

* Build a dynamic library that contains the functions that use Eigen (C++)
* Initiates the call to the functions in Unity scripts (C#)

### A Minimum Example

Here is a minimum example showing how to get the trace of a matrix in Eigen.

#### Dynamic Library using Eigen

* Download [Eigen](http://eigen.tuxfamily.org) and decompress it.
* Create a Visual Studio dynamic library project.
* Add the root path of Eigen package to ```Additional Include Directories```
* Add a CPP file to the project
* Copy the following to the CPP file:

```cpp
#define EXPORT_API __declspec(dllexport)
#include <Eigen/Dense>
using namespace Eigen;
extern "C" {
  EXPORT_API float getTrace() {
    MatrixXf m = MatrixXf::Random(4,4);
    return m.trace();
  }
}
```

* Configure the building so that **it is compatible with targeted platform**.
* Build
* Copy to Unity3D project

#### Call the Function in Unity Script

* Create a script ```EigenTest.cs```.
* Copy the following to the CSharp file:

```csharp
using System.Collections;
using System.Collections.Generic;
using System.Runtime.InteropServices;
using UnityEngine;

public class EigenTest : MonoBehaviour {
  [DllImport("YOURDLLNAME")]
  public static extern float getTrace();
  void Start () {
    Debug.Log("The trace value is: " + getTrace());
  }
}
```

* Attach the script to any GameObject.
* Deploy to the targeted platform.


### Advanced

The above example is the minimal to make things work. If you want to parse a Matrix4x4 to Eigen environment, please refer to [Marshaling](https://en.wikipedia.org/wiki/Marshalling_(computer_science)).

Eigen is perfect for native programming because it is header-only and is potentially platform independent. If you want to understand more about this workflow, please refer to [Unity Native Programming](http://longqian.me/2017/01/29/unity-native-programming/).



Thanks for reading!  <i class="em em-lq"></i>

