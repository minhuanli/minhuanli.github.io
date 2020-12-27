---
layout: post
title: HoloLens File Transfer
description: Interacting with HoloLens application via file IO. A useful trick for communicating with HoloLens.
tags: hololens augmented-reality unity3d
---

Tranferring file to and from HoloLens seems non-trivial. It is written in HoloLens official document about [saving and sending your files](https://developer.microsoft.com/en-us/windows/holographic/saving_and_finding_your_files):

> Unlike Windows on a PC or phone, HoloLens does not have a File Explorer application.

Getting access to non-media file is not an easy task. Tools like [file picker](https://developer.microsoft.com/en-us/windows/holographic/saving_and_finding_your_files) and [OneDrive](https://www.microsoft.com/en-us/store/p/onedrive/9wzdncrfj1p3) are definitly over-kill for this task.

### Goal

The goals here are two-folded:

* Save something to a file in HoloLens application, and later access it
* Create a file elsewhere, and make HoloLens application read it

### File Explorer on Device Portal

File explorer on the device portal is used as a bridge. But the directories listed on the device portal is not complete. Therefore, we need to find out the **accessible** directory for both HoloLens application and user on PC.

Luckily I found such a location. The folder `LocalAppData\SOMEAPP\RoamingState` on the device portal is mapped to `ApplicationData.Current.RoamingFolder.Path` in the application at runtime.

<p class="full-width">
<img src="/public/image/hololens-portal.png" alt="Device Portal Screenshot" style="width:100%;" >
</p>

So, when the file is written to this path in UWP application, it will appear here, and you can download it by simply clicking on the download button. On the other hand, if you upload a file to this path, it can be read out by UWP application.

### Scripts

The scripts are adapted from [HoloToolkit](https://github.com/Microsoft/HoloToolkit-Unity/blob/master/Assets/HoloToolkit/SpatialMapping/Scripts/RemoteMapping/MeshSaver.cs).

#### Reading

The sample script for reading file is:

```csharp
public void ReadString() {
  string s;
#if !UNITY_EDITOR && UNITY_METRO
  try {
    using (Stream stream = OpenFileForRead(ApplicationData.Current.RoamingFolder.Path, "filename.txt")) {
      byte[] data = new byte[stream.Length];
      stream.Read(data, 0, data.Length);
      s = Encoding.ASCII.GetString(data);
    }
  }
  catch (Exception e) {
    Debug.Log(e);
  }
#endif
  return s;
}

private static Stream OpenFileForRead(string folderName, string fileName) {
  Stream stream = null;
#if !UNITY_EDITOR && UNITY_METRO
  Task task = new Task(
    async () => {
      StorageFolder folder = await StorageFolder.GetFolderFromPathAsync(folderName);
      StorageFile file = await folder.GetFileAsync(fileName);
      stream = await file.OpenStreamForReadAsync();
    });
  task.Start();
  task.Wait();
#endif
  return stream;
}
```

#### Writing

The sample script for writing file is:

```csharp
public void WriteString(string s) {
#if !UNITY_EDITOR && UNITY_METRO
  using (Stream stream = OpenFileForWrite(ApplicationData.Current.RoamingFolder.Path, "filename.txt")) {
    byte[] data = Encoding.ASCII.GetBytes(s);
    stream.Write(data, 0, data.Length);
    stream.Flush();
  }
#endif
}


private static Stream OpenFileForWrite(string folderName, string fileName) {
  Stream stream = null;
#if !UNITY_EDITOR && UNITY_METRO
  Task task = new Task(
    async () => {
      StorageFolder folder = await StorageFolder.GetFolderFromPathAsync(folderName);
      StorageFile file = await folder.CreateFileAsync(fileName, CreationCollisionOption.ReplaceExisting);
      stream = await file.OpenStreamForWriteAsync();
    });
  task.Start();
  task.Wait();
#endif
  return stream;
}
```

In the above sample code, the file that is queried must exist. In the case when you want to list existing files in a given folder, it is as simple as:

```csharp
StorageFolder folder = await StorageFolder.GetFolderFromPathAsync(folderName);
foreach (StorageFile f in allFiles) {
  Debug.Log(TAG + ": found file " + f.Name + ", " + f.DateCreated);
}
```

The above code snippets are tested with the following configurations:

* **Unity 5.5 + Visual Studio 2015**
* **Unity 5.6 + Visual Studio 2017**


### Further Reading

Apart from the `RoamingState` folder on HoloLens Device Portal, some other folders are accessible as well, for example, `TempState` and `LocalState` etc. More information can be found on [UWP API page](https://docs.microsoft.com/en-us/uwp/api/Windows.Storage.ApplicationData) of `Windows.Storage.ApplicationData`.


Thanks for reading!  <i class="em em-lq"></i>

