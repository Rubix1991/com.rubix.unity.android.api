# Rubix C# wrappers for Android Java APIs for Unity

This package provides C# wrappers for [Android Java APIs](http://developer.android.com/reference) for Unity. There are almost __~3000__ wrappers provided.

The wrappers makes the usage of Android APIs in Unity much much easier. You can find the full list of exposed APIs [here](/Docs~/ExposedApi.md).

__Note: This is an experimental package, if you'll find a bug or a missing functionality, please report it. Thank you!__

__Note:__ Android API Level matches package's major version, see [package.json](/package.json).

## Requirements

* Unity 6000.0.47f1 or higher 
* Unity Android Support
* __Note:__ Older Unity versions are not supported, because they're missing necessary fixes for AndroidJavaObject

## Installation

* In Unity, go to Window->Package Manager
* In top left corner click **+** button, choose **Install Package from git URL**
* Enter

```
git@github.com:Rubix1991/com.rubix.unity.android.api.git#release/api-34
```

## Samples

You can find the examples on how the wrappers are used in [this Unity project](https://github.com/Rubix1991/com.rubix.unity.android.api-examples). Simply clone the repo and open it in Unity.

## Examples

Under the hood, the package uses [AndroidJavaObject](https://docs.unity3d.com/ScriptReference/AndroidJavaObject.html) and [AndroidJavaProxy](https://docs.unity3d.com/ScriptReference/AndroidJavaProxy.html) for base functionality.

The following C# code provides an example how to show a [toast](https://developer.android.com/guide/topics/ui/notifiers/toasts) and why the wrappers are useful.

```
using Rubix.Unity.Android.Widget;
using Rubix.Unity.Android.App;
...


using var toast = Toast.MakeText(Activity.CurrentActivity, 
    "This is a short toast",
    Toast.LENGTH_SHORT);
toast.Show();
```

Without the wrappers, you would need to manually resolve class names and methods, and the above code would look like this:

```
using UnityEngine.Android;
...

using var unityPlayer = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
using var currentActivity = unityPlayer.GetStatic<AndroidJavaObject>("currentActivity");
using var toastClass = new AndroidJavaClass("android.widget.Toast");
int lengthShort = toastClass.GetStatic<int>("LENGTH_SHORT");
using var toast = toastClass.CallStatic<AndroidJavaObject>("makeText",
    currentActivity,
    "This is a short toast",
    lengthShort);
toast.Call("show");
```

As you see, with wrappers you write much less code for the same functionality.
