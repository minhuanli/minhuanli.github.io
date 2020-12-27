---
layout: post
title: Unity Native Programming
description: Tutorials on how to use native C++ code, or library in a Unity application. It is how HoloLensARToolKit project is built.
tags: unity3d hololens cpp csharp native-programming hololens-artoolkit
---

Unity is great in terms of the ease to create graphics applications, the wide compatibility with different platforms (thanks to [Mono](http://www.mono-project.com/)), and its pioneering role in the current fast growing AR/VR market. However, most programmers are more comfortable with C++, and Linux, than C# and Windows. As a result, many existing great libraries, especially in the field of computer vision, are C++ projects. Examples include [OpenCV](http://opencv.org/), [ARToolKit](http://artoolkit.org/), etc.

In order to reuse native libraries in Unity projects, here are two options:

- re-implement the algorithm in C# (Javascript)
- find a way to interface native libraries.

I went for the second option, and here comes **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**.
I hope this wiki page will make your life easier when you are faced with this question.

### Managed and Unmanaged Library
Unity builds managed libraries, that is to say, the libraries and applications built by Unity are managed by Common Language Runtime (thanks to Mono again). According to the [Wikipedia page](https://en.wikipedia.org/wiki/Common_Language_Runtime):

> The CLR provides additional services including memory management, type safety, exception handling, garbage collection, security and thread management.

Great! C++ code can be built with CLR as well, as the name "Common Language Runtime" suggests. Therefore, one good way to go is to build your native code using CLR, put your library in Unity asset path, and use it as if it is written in C#.

**However**, it is not quite intuitive to migrate those huge and useful native libraries (OpenCV, ARToolKit) to CLR. If you just hit "build" to build them, the library files that appear in your project folder are **unmanaged** libraries. Some additional work has to be done in order to correctly and safely interface managed and unmanaged libraries: [Marshaling](https://en.wikipedia.org/wiki/Marshalling_(computer_science)) and [PInvoke](http://www.pinvoke.net/).

### Native Code
Let us look at the native C++ code first.

You need and only need to answer the following two questions:

- What is the desired running platform?
- What are the functions that you want to call in C# managed code?

#### Desired running platform
If we take Win32 as example, then the native library should be compatible with Win32. Because the built dll file is shipped with your Unity application to the desired platform, all the dependencies of your library should exist on the target platform.

In the case of **[HoloLensARToolKit](https://github.com/qian256/HoloLensARToolKit)**, the library `ARToolKitUWP.dll` should depend only on UWP and WINRT system libraries, instead of general Win32 libraries (e.g. kernel32.dll). A useful tool is called [Dependency Walker](http://www.dependencywalker.com/) that can help you to check the dependecies of a dynamic link library.

Let's take a look at the dependency of our `ARToolKitUWP.dll`:

<img src="http://longqian.me/public/image/artoolkituwp-depend.png" alt="Dependency" style="width:60%"/>

Basically, in order to successfully link the native library on the target platform, these dependencies must be satisfied on the given device. If your library depends on other third-party libraries, then these third-party libraries should be compatible with the specific platform as well, and make sure they are placed in the searching directory of runtime linker. 
If you are not sure about the directories, just place them at the same location as the .exe or .dll files.

#### What functions to use?
Not all functions in a library can be called by the outside, apparently. It is left to the programmer to design an accessible interface exposed to other libraries. The files `ARToolKitUWP.h` and `ARToolKitUWP.cpp` define such interface for HoloLensARToolKit project.

The keywords to use that specifies exportable functions are `extern "C"` and `__declspec(dllexport)`.
The minimum example is:

```c
#define EXPORT_API __declspec(dllexport)
extern "C" {
    EXPORT_API void HelloWorld();
}
```

A good practice is to design a singleton class representing a controller, so that all the public functions of the singleton object could be called externally, and the native library manages one single object. In the case of ARToolKit, the **ARController** class is designed like this, since there is only need for one controller in general.

`ARToolKitUWP.h` defines the full list of exportable functions for HoloLensARToolKit project.

### Unity Side Scripting
In order to use the exposed function of native libraries, function signatures have to be defined, so that C# finds the function to call inside native libraries. Such function definitions are like this:

```csharp
using System.Runtime.InteropServices;            // system reference
public static class HelloWorldFunctions {
    [Dllimport("HelloWorldLibrary.dll")]         // provide the name of library
    public static extern void HelloWorld();      // entry of function
}
```

Once such function definitions are made and the functions are found in the native library, they can be directly called in C# code. This technology is called **PInvoke**.

In HoloLensARToolKit project, the native function entries are defined in `ARToolKitUWP-Unity/Scripts/ARUWPNative.cs`, for your reference.

### Function Parameters
As you may found out, there are some strange code around parameter definitions, like this:

```csharp
[DllImport("ARToolKitUWP")]
[return: MarshalAsAttribute(UnmanagedType.I1)]
public static extern bool aruwpGetARToolKitVersion([MarshalAs(UnmanagedType.LPStr)]StringBuilder buffer, int length);
```

It is called **Marshaling**. According to Wikipedia, 

> In computer science, marshalling or marshaling is the process of transforming the memory representation of an object to a data format suitable for storage or transmission, and it is typically used when data must be moved between different parts of a computer program or from one program to another.

In the case of C# interfacing native code, the data exchange between managed environment and unmanaged environment only happens at the time when native functions are called and returned. The processing by native code happens in between, but the computation does not affect the managed memory. Therefore, we only need to perform such memory transformation when native functions are called and returned. Marshaling does the trick.

For instance, for the above function, the native code looks like this:

```cpp
EXPORT_API bool aruwpGetARToolKitVersion(char *buffer, int length);
```

The bool type of C++ is marshaled to the bool type of C#, and the char buffer set by native function is returned as StringBuilder object of C#, because of the different representation of data types for both languages. Marshaling is not only about data type conversion, but also creates manageable memory for unmanaged data, so that the data can be later managed by CLR, e.g. garbage collection.



Thanks for reading and happy coding. <i class="em em-lq"></i>
